<a href="https://evilmartians.com/chronicles/optimizing-react-virtual-dom-explained">https://evilmartians.com/chronicles/optimizing-react-virtual-dom-explained</a><div id="articleHeader"><h1><b>Optimizing React:</b> Virtual DOM explained</h1></div><div>March 28, 2018</div></article><section><div><div><div>Andy Barnov</div><div>Writer at Evil Martians. Teacher at Le Wagon. Former international TV correspondent</div></section><div>
  <p>Learn about React’s Virtual DOM and use this knowledge to speed up your applications. In this thorough beginner-friendly introduction to framework’s internals, we will demystify JSX, show you how React makes rendering decisions, explain how to find bottlenecks, and share some tips to avoid common mistakes.</p>
</div>

<p>One of the reasons React keeps rocking the front-end world and shows no sign of decline is its approachable learning curve: after wrapping your head around <a href="https://reactjs.org/docs/introducing-jsx.html" target="_blank">JSX</a> and the whole “<a href="https://reactjs.org/docs/state-and-lifecycle.html" target="_blank">State</a> vs. <a href="https://reactjs.org/docs/components-and-props.html" target="_blank">Props</a>” concept, you are good to go.</p>

<article>
  <p>If you are already familiar with the way React works, you can skip straight to <a href="#fixing-things-mountingunmounting" target="_blank">“Fixing things”</a>.</p>
</article>

<p>But to truly master React, you need to <em>think in React</em>. This article is an attempt to help you with that. Take a look at the React table made for <a href="https://ebaymag.com/" target="_blank">one of our projects</a>:</p>

<figure>
  <p><div class="readableLargeImageContainer"><img src="https://cdn.evilmartians.com/front/posts/optimizing-react-virtual-dom-explained/ebay_table-4023632.png"   alt="A huge React table" /></div></p>
  <figcaption>
    <p>A huge React table on <a href="https://ebaymag.com/" target="_blank">eBay for business</a>.</p>
  </figcaption>
</figure>

<p>With hundreds of dynamic, filterable rows, understanding framework’s finer points becomes essential to guarantee smooth user experience.</p>

<blockquote>
  <p>And you can certainly feel when things go wrong. Input fields get laggy, checkboxes take a second to be checked, modals have a hard time showing up.</p>
</blockquote>

<p>To be able to solve these kinds of problems, we need to cover the whole journey a React component takes from being defined by you to being rendered (and then updated) on a page. Buckle up!</p>

<h2 id="behind-jsx">Behind JSX</h2>

<article>
  <p>Process known in front-end circles as “transpiling”, even though “compilation” would be a more correct term.</p>
</article>

<p>React developers urge you to use a mix of HTML and JavaScript known as JSX when you write your components. Browsers, though, have no clue about JSX and its syntax. Browsers only understand plain JavaScript, so JSX will have to be transformed into it. Here is the JSX code for a <code>div</code> that has a class and some content:</p>

<div>
<pre><code>&lt;div className='cn'&gt;
  Content!
&lt;/div&gt;
</code></pre>
</div>

<p>The same code in “formal” JavaScript is just a function call with a number of arguments:</p>

<div>
<pre><code>React.createElement(
  'div',
  { className: 'cn' },
  'Content!'
);
</code></pre>
</div>

<p>Let’s take a closer look at these arguments. The first one is a <em>type of element</em>. For HTML tags it will be a string with a tag’s name. A second argument is an object with all of the <em>element’s attributes</em>. It can also be an empty object if there are none. All the following arguments are <em>element’s children</em>. Text inside an element also counts as a child, so a string ‘Content!’ is placed as the third argument to a function call.</p>

<p>You can already imagine what happens when we have more children:</p>

<div>
<pre><code>&lt;div className='cn'&gt;
  Content 1!
  &lt;br /&gt;
  Content 2!
&lt;/div&gt;
</code></pre>
</div>

<div>
<pre><code>React.createElement(
  'div',
  { className: 'cn' },
  'Content 1!',              // 1st child
  React.createElement('br'), // 2nd child
  'Content 2!'               // 3rd child
)
</code></pre>
</div>

<p>Our function now has five arguments: an element’s type, an attributes object, and three children. As one of our children is also an HTML tag known to React, it will be portrayed as a function call as well.</p>

<p>By now, we have covered two types of children: a plain <code>String</code> or another call to <code>React.createElement</code>. However, other values can also serve as arguments:</p>

<ul>
  <li>Primitives <code>false</code>, <code>null</code>, <code>undefined</code> and <code>true</code>
</li>
  <li>Arrays</li>
  <li>React <em>components</em>
</li>
</ul>

<p>Arrays are used because children can be grouped and passed as one argument:</p>

<div>
<pre><code>React.createElement(
  'div',
  { className: 'cn' },
  ['Content 1!', React.createElement('br'), 'Content 2!']
)
</code></pre>
</div>

<p>The power of React comes, of course, not from the tags described in the HTML spec, but from the user-created components such as:</p>

<div>
<pre><code>function Table({ rows }) {
  return (
    &lt;table&gt;
      {rows.map(row =&gt; (
        &lt;tr key={row.id}&gt;
          &lt;td&gt;{row.title}&lt;/td&gt;
        &lt;/tr&gt;
      ))}
    &lt;/table&gt;
  );
}
</code></pre>
</div>

<p>Components allow us to break our templates into reusable chunks. In the example of a <a href="https://reactjs.org/docs/components-and-props.html#functional-and-class-components" target="_blank">“functional”</a> component above we accept an array of objects holding table row data and return a single <code>React.createElement</code> call for a <code>&lt;table&gt;</code> element and its rows as children.</p>

<p>Whenever we place our component into a layout like so:</p>

<div>
<pre><code>&lt;Table rows={rows} /&gt;
</code></pre>
</div>

<p>from the browsers’ perspective, we wrote this:</p>

<div>
<pre><code>  React.createElement(Table, { rows: rows });
</code></pre>
</div>

<p>Note that this time our first argument is not a <code>String</code> describing an HTML element, but <em>a reference to a function that we defined</em> when we coded our component. Our attributes are now our <a href="https://reactjs.org/docs/components-and-props.html" target="_blank"><code>props</code></a>.</p>

<h2 id="putting-components-on-a-page">Putting components on a page</h2>

<p>So, we have transpiled all our JSX components into pure JavaScript, and now we have a bunch of function calls with arguments that are other function calls, holding yet other function calls… How does it all get transformed into DOM elements that form a web page?</p>

<p>For that, we have a <code>ReactDOM</code> library and its <code>render</code> method:</p>

<div>
<pre><code>function Table({ rows }) { /* ... */ } // defining a component

// rendering a component
ReactDOM.render(
  React.createElement(Table, { rows: rows }), // "creating" a component
  document.getElementById('#root') // inserting it on a page
);
</code></pre>
</div>

<p>When <code>ReactDOM.render</code> is called, <code>React.createElement</code> is finally called too and it returns the following object:</p>

<div>
<pre><code>// There are more fields, but these are most important to us
{
  type: Table,
  props: {
    rows: rows
  },
  // ...
}
</code></pre>
</div>

<blockquote>
  <p>These objects constitute Virtual DOM in React’s sense.</p>
</blockquote>

<p>They will be compared to each other on all further renders and eventually translated into a <em>real</em> DOM (as opposed to <em>virtual</em>).</p>

<p>Here’s another example: this time with a <code>div</code> that has a class attribute and several children:</p>

<div>
<pre><code>React.createElement(
  'div',
  { className: 'cn' },
  'Content 1!',
  'Content 2!',
);
</code></pre>
</div>

<p>Turns into:</p>

<div>
<pre><code>{
  type: 'div',
  props: {
    className: 'cn',
    children: [
      'Content 1!',
      'Content 2!'
    ]
  }
}
</code></pre>
</div>

<p>Note that children who used to be separate arguments to the <code>React.createElement</code> function have found their place under a <code>children</code> key inside <code>props</code>. So it <em>does not matter</em> whether children are passed as an array or a list of arguments—in a resulting Virtual DOM object they will all end up together anyway.</p>

<p>What’s more, we could add children to the props directly in the JSX code, and the result would still be the same:</p>

<div>
<pre><code>&lt;div className='cn' children={['Content 1!', 'Content 2!']} /&gt;
</code></pre>
</div>

<p>After a Virtual DOM object is built, <code>ReactDOM.render</code> will try to transform it into a DOM node our browser can display according to those rules:</p>

<ul>
  <li>
    <p>If a <code>type</code> attribute holds a <em>string</em> with a tag name—create a tag with all attributes listed under <code>props</code>.</p>
  </li>
  <li>
    <p>If we have a function or a class under <code>type</code>—call it and repeat the process recursively on a result.</p>
  </li>
  <li>
    <p>If there are any <code>children</code> under <code>props</code>—repeat the process for each child one by one and place results inside the parent’s DOM node.</p>
  </li>
</ul>

<p>As a result, we get the following HTML (for our table example):</p>

<div>
<pre><code>&lt;table&gt;
  &lt;tr&gt;
    &lt;td&gt;Title&lt;/td&gt;
  &lt;/tr&gt;
  ...
&lt;/table&gt;
</code></pre>
</div>

<h2 id="rebuilding-the-dom">Rebuilding the DOM</h2>

<article>
  <p>In practice, <code>render</code> is usually called on a root element once and further updates are applied through <code>state</code>.</p>
</article>

<p>Note that “re” in the heading! The real magic in React starts when we want to <em>update</em> a page without replacing everything. There are few ways how we can achieve it. Let’s start with the simplest one—call <code>ReactDOM.render</code> for the same node <em>again</em>.</p>

<div>
<pre><code>// Second call
ReactDOM.render(
  React.createElement(Table, { rows: rows }),
  document.getElementById('#root')
);
</code></pre>
</div>

<p>This time, the piece of code above will behave differently to what we’ve already seen. Instead of creating all DOM nodes from scratch and putting them on the page, React will start the <a href="https://reactjs.org/docs/reconciliation.html" target="_blank">reconciliation</a> (or “diffing”) algorithm to determine which parts of the node tree have to be updated and which can be left untouched.</p>

<p>So, how does it work? There is just a handful of simple scenarios and <em>understanding them</em> will help us a lot with our optimization. Keep in mind that we are now looking at objects that serve as a representation of a node in the React Virtual DOM.</p>

<ul>
  <li><strong>Scenario 1: <code>type</code> is a string, <code>type</code> stayed the same across calls, <code>props</code> did not change either.</strong></li>
</ul>

<div>
<pre><code>// before update
{ type: 'div', props: { className: 'cn' } }

// after update
{ type: 'div', props: { className: 'cn' } }
</code></pre>
</div>

<p>That is the simplest case: DOM stays the same.</p>

<ul>
  <li><strong>Scenario 2: <code>type</code> is still the same string, <code>props</code> are different.</strong></li>
</ul>

<div>
<pre><code>// before update:
{ type: 'div', props: { className: 'cn' } }

// after update:
{ type: 'div', props: { className: 'cnn' } }
</code></pre>
</div>

<p>As our <code>type</code> still represents an HTML <em>element</em>, React knows how to change its properties through standard DOM API calls, without removing the node from a DOM tree.</p>

<ul>
  <li><strong>Scenario 3: <code>type</code> has changed to a different <code>String</code>, or from <code>String</code> to a component.</strong></li>
</ul>

<div>
<pre><code>// before update:
{ type: 'div', props: { className: 'cn' } }

// after update:
{ type: 'span', props: { className: 'cn' } }
</code></pre>
</div>

<p>As React now sees that the type is different, it would not even try to update our node: old element will be removed (<em>unmounted</em>) <strong>together with all its children</strong>. Thus, replacing an element for something entirely different high up the DOM tree can be quite expensive. Luckily, that rarely happens in the real world.</p>

<p>It is important to remember that React uses <code>===</code> (triple equals) to compare <code>type</code> values, so they have to be the same <em>instances</em> of the same class or the <em>same</em> function.</p>

<p>Next scenario is much more interesting, as that is how we use React most often.</p>

<ul>
  <li><strong>Scenario 4: <code>type</code> is a component.</strong></li>
</ul>

<div>
<pre><code>// before update:
{ type: Table, props: { rows: rows } }

// after update:
{ type: Table, props: { rows: rows } }
</code></pre>
</div>

<blockquote>
  <p>“But nothing had changed!”, you might say, and you will be wrong.</p>
</blockquote>

<article>
  <p>Note that a component’s <code>render</code> (only class components have this method explicitly defined) is not the same as <code>ReactDOM.render</code>. The word “render” is indeed a bit overused in React’s world.</p>
</article>

<p>If <code>type</code> is a reference to a function or a class (that is, your regular React component), and we started tree reconciliation process, then React will always try to look <em>inside</em> the component to make sure that the values returned on <code>render</code> did not change (sort of a precaution against side-effects). Rinse and repeat for each component down the tree—yes, with complicated renders that might become expensive too!</p>

<h2 id="taking-care-of-children">Taking care of children</h2>

<p>Besides four common scenarios described above, we also need to account for React’s behavior when an element has more than one child. Let’s say we have such an element:</p>

<div>
<pre><code>// ...
props: {
  children: [
      { type: 'div' },
      { type: 'span' },
      { type: 'br' }
  ]
},
// ...
</code></pre>
</div>

<p>And we want to shuffle those children around:</p>

<div>
<pre><code>// ...
props: {
  children: [
    { type: 'span' },
    { type: 'div' },
    { type: 'br' }
  ]
},
// ...
</code></pre>
</div>

<p>What happens then?</p>

<p>If, while “diffing”, React sees <em>any</em> array inside <code>props.children</code>, it starts comparing elements in it with the ones in the array it saw before by looking at them in order: index 0 will be compared to index 0, index 1 to index 1, etc. For each pair, React will apply the set of rules described above. In our case, it sees that <code>div</code> became a <code>span</code> so <em>Scenario 3</em> will be applied. That is not very efficient: imagine that we have removed the first row from a 1000-row table. React will have to “update” remaining 999 children, as their content will now not be equal if compared to previous representation index-by-index.</p>

<p>Luckily, React has a <a href="https://reactjs.org/docs/lists-and-keys.html" target="_blank">built-in way</a> to solve this problem. If an element has a <code>key</code> property, elements will be compared by a value of a <code>key</code>, not by index. As long as keys are unique, React will move elements around <em>without</em> removing them from DOM tree and then putting them back (a process known in React as <em>mounting/unmounting</em>).</p>

<div>
<pre><code>// ...
props: {
  children: [ // Now React will look on key, not index
    { type: 'div', key: 'div' },
    { type: 'span', key: 'span' },
    { type: 'br', key: 'bt' }
  ]
},
// ...
</code></pre>
</div>

<h2 id="when-state-changes">When state changes</h2>

<p>Up until now we only touched the <code>props</code> part of React philosophy but ignored the <code>state</code>. Here is a simple “stateful” component:</p>

<div>
<pre><code>class App extends Component {
  state = { counter: 0 }

  increment = () =&gt; this.setState({
    counter: this.state.counter + 1,
  })

  render = () =&gt; (&lt;button onClick={this.increment}&gt;
    {'Counter: ' + this.state.counter}
  &lt;/button&gt;)
}
</code></pre>
</div>

<p>So, we have a <code>counter</code> key in our state object. A click on a button increments its value and changes button text. But what happens in a DOM when we do that? Which part of it will be recalculated and updated?</p>

<p>Calling <code>this.setState</code> causes a re-render too, but not of the whole page, but <em>only of a component itself and its children</em>. Parents and siblings are spared. That is convenient when we have a large tree, and we want to redraw only a part of it.</p>

<h2 id="pinning-down-problems">Pinning down problems</h2>

<p>We have prepared a <a href="https://iadramelk.github.io/optimizing-react-demo/dist/before.html" target="_blank">little demo app</a> so you can see most common problems in the wild before we go about fixing them. You can take a look at its source code <a href="https://github.com/iAdramelk/optimizing-react-demo" target="_blank">here</a>. You will also need <a href="https://github.com/facebook/react-devtools" target="_blank">React Developer Tools</a>, so make sure you have them installed for your browser.</p>

<p>The first thing we want to take a look at is <em>which elements and when</em> cause Virtual DOM to be updated. Navigate to the React panel in your browser’s Dev Tools and select the “Highlight Updates” checkbox:</p>

<figure>
  <p><div class="readableLargeImageContainer"><img src="https://cdn.evilmartians.com/front/posts/optimizing-react-virtual-dom-explained/react_dev_tools-e78197e.png"   alt="React DevTools in Chrome with 'Highlight updates' checkbox selected" /></div></p>
  <figcaption>
    <p>React DevTools in Chrome with “Highlight updates” checkbox selected</p>
  </figcaption>
</figure>

<p>Now try adding a row to the table. As you can see, a border appears around each element on the page. That means that React is calculating and comparing the whole Virtual DOM tree each time we add a row. Now try to hit a counter button inside a row. You see how Virtual DOM updates on change of <code>state</code>—only the concerned element and its children are affected.</p>

<p>React DevTools hints at where the problem might be, but tells us nothing about details: especially whether the update in question means “diffing” elements or mounting/unmounting them. To find out more, we need to use React’s built-in <a href="https://reactjs.org/docs/optimizing-performance.html#profiling-components-with-the-chrome-performance-tab" target="_blank">profiler</a> (note it won’t work in production mode).</p>

<p>Add <code>?react_perf</code> to any URL of your app and go to “Performance” tab in your Chrome DevTools. Hit the recording button and click around the table. Add some rows, change some counters, then hit “stop”.</p>

<figure>
  <p><div class="readableLargeImageContainer"><img src="https://cdn.evilmartians.com/front/posts/optimizing-react-virtual-dom-explained/react_perf_tools-ba86f5e.png"   alt="React DevTools' 'performance' tab" /></div></p>
  <figcaption>
    <p>React DevTools’ “Performance” tab</p>
  </figcaption>
</figure>

<p>In the resulting output, we are interested in “User timing”. Zoom onto timeline until you see “React Tree Reconciliation” group and its children. These are all names of our components with <em>[update]</em> or <em>[mount]</em> next to them.</p>

<blockquote>
  <p>Most of our performance problems fall into one of those two categories.</p>
</blockquote>

<p>Either a component (and everything branching from it) is for some reason re-mounted on each update, and we didn’t want it (re-mounting is slow), or we are performing an expensive reconciliation on large branches, even though nothing has changed.</p>

<h2 id="fixing-things-mountingunmounting">Fixing things: Mounting/Unmounting</h2>

<p>Now when we have caught up on some theory about how React makes decisions to update Virtual DOM and figured out how to see what is happening behind the scenes, we are finally ready to fix things! First, let’s deal with mounts/unmounts.</p>

<p>You can get a very noticeable speed improvement if you simply mind the fact that multiple children of any element/component are represented as an <em>array</em> internally.</p>

<p>Consider this:</p>

<div>
<pre><code>&lt;div&gt;
  &lt;Message /&gt;
  &lt;Table /&gt;
  &lt;Footer /&gt;
&lt;/div&gt;
</code></pre>
</div>

<p>Inside our Virtual DOM that will be represented as:</p>

<div>
<pre><code>// ...
props: {
  children: [
    { type: Message },
    { type: Table },
    { type: Footer }
  ]
}
// ...
</code></pre>
</div>

<p>We have a simple <code>Message</code> which is a <code>div</code> holding some text (think your garden variety notification) and a huge <code>Table</code> spanning, let’s say, 1000+ rows. They are both children of the enclosing <code>div</code>, so they are placed under <code>props.children</code> of the parent node, and they don’t happen to have a key. And React will not even remind us to assign keys through console warnings, as children are being passed to the parent’s <code>React.createElement</code> as a list of arguments, not an array.</p>

<p>Now our user has dismissed a notification and <code>Message</code> is removed from a tree. <code>Table</code> and <code>Footer</code> are all that’s left.</p>

<div>
<pre><code>// ...
props: {
  children: [
    { type: Table },
    { type: Footer }
  ]
}
// ...
</code></pre>
</div>

<p>How does React see it? It sees it as an array of children changing shape: <code>children[0]</code> held a <code>Message</code> and now it holds <code>Table</code>. There were no keys to compare against, so it compares <code>type</code>s, and as they are both references to functions (and <em>different</em> functions), it <em>unmounts</em> the whole <code>Table</code> and mounts it again, rendering all its children: 1000+ rows!</p>

<p>So, you can either add unique keys (but in this particular case using keys is not the best choice) or go for a smarter trick: use <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators" target="_blank">short circuit boolean evaluation</a>, which is a feature of JavaScript and many other modern languages. Look:</p>

<div>
<pre><code>// Using a boolean trick
&lt;div&gt;
  {isShown && &lt;Message /&gt;}
  &lt;Table /&gt;
  &lt;Footer /&gt;
&lt;/div&gt;
</code></pre>
</div>

<p>Even if the <code>Message</code> goes out of the picture, <code>props.children</code> of a parent <code>div</code> will still hold <em>three</em> elements, <code>children[0]</code> having a value <code>false</code> (a boolean primitive). Remember that <code>true</code>/<code>false</code>, <code>null</code> and <code>undefined</code> are all permitted values of a Virtual DOM object’s <code>type</code> property? We end up with something like that:</p>

<div>
<pre><code>// ...
props: {
  children: [
    false, //  isShown && &lt;Message /&gt; evaluates to false
    { type: Table },
    { type: Footer }
  ]
}
// ...
</code></pre>
</div>

<p>So, <code>Message</code> or not, our indexes will not change, and <code>Table</code> will, of course, still be compared to <code>Table</code> (having references to components as <code>type</code> starts reconciliation anyway), but <em>just comparing Virtual DOM is often a lot faster than removing DOM nodes and creating them from scratch again</em>.</p>

<p>Now let’s look at something more evolved. We know you like <a href="https://reactjs.org/docs/higher-order-components.html" target="_blank">HOC</a>s. A higher-order component is a function that takes a component as an argument, does something, and returns a different function:</p>

<div>
<pre><code>function withName(SomeComponent) {
  // Computing name, possibly expensive...
  return function(props) {
    return &lt;SomeComponent {...props} name={name} /&gt;;
  }
}
</code></pre>
</div>

<p>That is a very common pattern, but you need to be careful with it. Consider:</p>

<div>
<pre><code>class App extends React.Component() {
  render() {
    // Creates a new instance on each render
    const ComponentWithName = withName(SomeComponent);
    return &lt;SomeComponentWithName /&gt;;
  }
}
</code></pre>
</div>

<p>We are creating a HOC inside of a parent’s <code>render</code> method. When we re-render the tree, our Virtual DOM will look like this:</p>

<div>
<pre><code>// On first render:
{
  type: ComponentWithName,
  props: {},
}

// On second render:
{
  type: ComponentWithName, // Same name, but different instance
  props: {},
}
</code></pre>
</div>

<p>Now, React would love to just run a diffing algorithm on <code>ComponentWithName</code>, but as this time the same name references a <em>different instance</em>, triple equals comparison fails and, instead of a reconciliation, a full re-mount has to happen. Note it will also result in a loss of state, <a href="https://github.com/facebook/react/blob/044015760883d03f060301a15beef17909abbf71/docs/docs/higher-order-components.md#dont-use-hocs-inside-the-render-method" target="_blank">as described here</a>. Luckily, it is easy to fix: you need to always create a HOC outside of <code>render</code>:</p>

<div>
<pre><code>// Creates a new instance just once
const ComponentWithName = withName(Component);

class App extends React.Component() {
  render() {
    return &lt;ComponentWithName /&gt;;
  }
}
</code></pre>
</div>
<h2 id="fixing-things-updating">Fixing things: Updating</h2>

<p>So, now we make sure not to re-mount stuff, unless necessary. However, any change to a component located close to the root of the DOM tree will cause diffing and reconciliation of all its children. With complicated structures that is expensive and can often be avoided.</p>

<blockquote>
  <p>Would be great to have a way to tell React not to look at a certain branch, as we are confident there were no changes in it.</p>
</blockquote>

<p>That way exists, and it involves a method called <code>shouldComponentUpdate</code> which is a part of the <a href="https://reactjs.org/docs/react-component.html#the-component-lifecycle" target="_blank">component’s lifecycle</a>. This method is called  <em>before</em> each call to a component’s <code>render</code> and receives new values of props and state. Then we are free to compare them with our current values and decide whether we should update our component or not (return <code>true</code> or <code>false</code>). If we return <code>false</code>, React will not re-render the component in question and will not look at its children.</p>

<p>Usually to compare both sets of <code>props</code> and <code>state</code> a simple <em>shallow</em> comparison is enough: if values at the top level are different, we don’t have to update. Shallow comparison is not a feature of JavaScript, but there are numerous <a href="https://github.com/dashed/shallowequal" target="_blank">utilities</a> for that.</p>

<p>With their help, we can write our code like this:</p>

<div>
<pre><code>class TableRow extends React.Component {

  // will return true if new props/state are different from old ones
  shouldComponentUpdate(nextProps, nextState) {
    const { props, state } = this;
    return !shallowequal(props, nextProps)
           && !shallowequal(state, nextState);
  }

  render() { /* ... */ }
}
</code></pre>
</div>

<p>But you don’t even have to code it yourself, as React has this feature built-in in a <a href="https://reactjs.org/docs/react-api.html#reactpurecomponent" target="_blank">class called</a> <code>React.PureComponent</code>. It is similar to <code>React.Component</code>, only <code>shouldComponentUpdate</code> is already implemented for you with a <em>shallow</em> props/state comparison in mind.</p>

<p>It sounds like a no-brainer, just swap <code>Component</code> for <code>PureComponent</code> in the <code>extends</code> part of your class definition and enjoy efficiency. Not so fast, though! Consider these examples:</p>

<div>
<pre><code>&lt;Table
    // map returns a new instance of array so shallow comparison will fail
    rows={rows.map(/* ... */)}
    // object literal is always "different" from predecessor
    style={ { color: 'red' } }
    // arrow function is a new unnamed thing in the scope, so there will always be a full diffing
    onUpdate={() =&gt; { /* ... */ }}
/&gt;
</code></pre>
</div>

<p>The code snippet above demonstrates three most common <nobr>anti-patterns</nobr>. Try to avoid them!</p>

<blockquote>
  <p>If you are mindful of creating all objects, arrays, and functions outside of <code>render</code> definition and making sure they don’t change between calls—you are safe.</p>
</blockquote>

<p>You can observe the effect of <code>PureComponent</code> in the <a href="https://iadramelk.github.io/optimizing-react-demo/dist/after.html" target="_blank">updated demo</a> where all table’s <code>Row</code>s are “purified”. If you turn on “Highlight Updates” in React DevTools, you will notice that only the table itself and the new row are being rendered on row insertion, all other rows stay untouched.</p>

<p>However, if you can not wait to <em>go all in</em> on pure components and implement them everywhere in your app—stop yourself. Comparing two sets of <code>props</code> and <code>state</code> is not free and for most basic components is not even worth it: it will take more time to run <code>shallowCompare</code> than the diffing algorithm.</p>

<p>Use this rule of thumb: pure components are good for complicated forms and tables, but they generally slow things down for simpler elements like buttons or icons.</p>

<hr />

<p>Thank you for reading! Now you are ready to apply these insights in your applications. You can use the <a href="https://github.com/iAdramelk/optimizing-react-demo" target="_blank">repository</a> for our little demo (<a href="https://iadramelk.github.io/optimizing-react-demo/dist/after.html" target="_blank">with</a> and <a href="https://iadramelk.github.io/optimizing-react-demo/dist/before.html" target="_blank">without</a> <code>PureComponent</code>) as a starting point for your experiments. Also, stay tuned for the next part of the series, where we plan to cover Redux and optimizing your <em>data</em> to increase the application’s general performance.</p>

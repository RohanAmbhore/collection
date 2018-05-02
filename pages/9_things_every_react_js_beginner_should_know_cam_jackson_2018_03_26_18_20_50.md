<a href="https://camjackson.net/post/9-things-every-reactjs-beginner-should-know">https://camjackson.net/post/9-things-every-reactjs-beginner-should-know</a><div id="articleHeader"><h1>9 things every React.js beginner should know</h1></div><time><em>24th January 2016</em></time><hr /><div><p>I've been using <a href="https://facebook.github.io/react/index.html" target="_blank">React.js</a> for about 6 months now. In the grand scheme of
things that's not very long at all, but in the ever-churning world of JavaScript frameworks, that just about qualifies
you as a bearded elder! I've helped out a few people lately with React starter tips, so I thought it would be a good
idea to write some of them up here to share more broadly. These are all either things that I wish I'd known when I
started out, or things that really helped me 'get' React.</p>
<p>I'm going to assume that you know the absolute basics; if the words component, props, or state are unfamiliar to you,
then you might want to read the official <a href="https://facebook.github.io/react/docs/getting-started.html" target="_blank">Getting started</a> or
<a href="https://facebook.github.io/react/docs/tutorial.html" target="_blank">Tutorial</a> pages. I'm also going to use <a href="https://facebook.github.io/jsx/" target="_blank">JSX</a>,
because it's a much more succinct and expressive syntax for writing components.</p>
<h3 id="-1-it-s-just-a-view-library-its-just-a-view-library-"><a href="#its-just-a-view-library" target="_blank">1. It's just a view library</a></h3>
<p>Let's get the basics out of the way. React is not another MVC framework, or any other kind of framework. It's just a
library for rendering your views. If you're coming from the MVC world, you need to realise that React is just the 'V',
part of the equation, and you need to look elsewhere when it comes to defining your 'M' and 'C', otherwise you're going
to end up with some really yucky React code. More on that later.</p>
<h3 id="-2-keep-your-components-small-keep-your-components-small-"><a href="#keep-your-components-small" target="_blank">2. Keep your components small</a></h3>
<p>This might seem like an obvious one, but it's worth calling out. Every good developer knows that small classes/modules/whatever
are easier to understand, test, and maintain, and the same is true of React components. My mistake when starting out
with React was under-estimating just how small my components should be. Of course, the exact size will depend upon many
different factors (including you and your team's personal preference!), but in general my advice would be to make
your components significantly smaller than you think they need to be. As an example, here is the component that shows
my latest blog entries on the <a href="https://camjackson.net" target="_blank">home page</a> of my website:</p>
<pre><code>const LatestPostsComponent = props =&gt; (
  &lt;section&gt;
    &lt;div&gt;&lt;h1&gt;Latest posts&lt;/h1&gt;&lt;/div&gt;
    &lt;div&gt;
      { props.posts.map(post =&gt; &lt;PostPreview key={post.slug} post={post}/&gt;) }
    &lt;/div&gt;
  &lt;/section&gt;
);
</code></pre>
<p>The component itself is a <code>&lt;section&gt;</code>, with only 2 <code>&lt;div&gt;</code>s inside it. The first one has a heading, and second one just
maps over some data, rendering a <code>&lt;PostPreview&gt;</code> for each element. That last part, extracting the <code>&lt;PostPreview&gt;</code> as
its own component, is the important bit. I think this is a good size for a component.</p>
<h3 id="-3-write-functional-components-write-functional-components-"><a href="#write-functional-components" target="_blank">3. Write functional components</a></h3>
<p>Previously there were two choices for defining React components, the first being <code>React.createClass()</code>:</p>
<pre><code>const MyComponent = React.createClass({
  render: function() {
    return &lt;div className={this.props.className}/&gt;;
  }
});
</code></pre>
<p>... and the other being ES6 classes:</p>
<pre><code>class MyComponent extends React.Component {
  render() {
    return &lt;div className={this.props.className}/&gt;;
  }
}
</code></pre>
<p>React 0.14 <a href="https://facebook.github.io/react/blog/2015/10/07/react-v0.14.html#stateless-functional-components" target="_blank">introduced</a>
a new syntax for defining components, as functions of props:</p>
<pre><code>const MyComponent = props =&gt; (
  &lt;div className={props.className}/&gt;
);
</code></pre>
<p>This is by far my favourite method for defining React components. Apart from the more concise syntax, this approach can
really help make it obvious when a component needs to be split up. Let's revisit the earlier example, and imagine that we
hadn't split it up yet:</p>
<pre><code>class LatestPostsComponent extends React.Component {
  render() {
    const postPreviews = renderPostPreviews();

    return (
      &lt;section&gt;
        &lt;div&gt;&lt;h1&gt;Latest posts&lt;/h1&gt;&lt;/div&gt;
        &lt;div&gt;
          { postPreviews }
        &lt;/div&gt;
      &lt;/section&gt;
    );
  }

  renderPostPreviews() {
    return this.props.posts.map(post =&gt; this.renderPostPreview(post));
  }

  renderPostPreview(post) {
    return (
      &lt;article&gt;
        &lt;h3&gt;&lt;a href={`/post/${post.slug}`}&gt;{post.title}&lt;/a&gt;&lt;/h3&gt;
        &lt;time pubdate&gt;&lt;em&gt;{post.posted}&lt;/em&gt;&lt;/time&gt;
        &lt;div&gt;
          &lt;span&gt;{post.blurb}&lt;/span&gt;
          &lt;a href={`/post/${post.slug}`}&gt;Read more...&lt;/a&gt;
        &lt;/div&gt;
      &lt;/article&gt;
    );
  }
}
</code></pre>
<p>This class isn't too bad, as far as classes go. We've already extracted a couple of methods out of the render method,
to keep things small and well-named. And we've encapsulated the idea of rendering the latest post previews pretty well.
Let's rewrite the same code using the functional syntax:</p>
<pre><code>const LatestPostsComponent = props =&gt; {
  const postPreviews = renderPostPreviews(props.posts);

  return (
    &lt;section&gt;
      &lt;div&gt;&lt;h1&gt;Latest posts&lt;/h1&gt;&lt;/div&gt;
      &lt;div&gt;
        { postPreviews }
      &lt;/div&gt;
    &lt;/section&gt;
  );
};

const renderPostPreviews = posts =&gt; (
  posts.map(post =&gt; this.renderPostPreview(post))
);

const renderPostPreview = post =&gt; (
  &lt;article&gt;
    &lt;h3&gt;&lt;a href={`/post/${post.slug}`}&gt;{post.title}&lt;/a&gt;&lt;/h3&gt;
    &lt;time pubdate&gt;&lt;em&gt;{post.posted}&lt;/em&gt;&lt;/time&gt;
    &lt;div&gt;
      &lt;span&gt;{post.blurb}&lt;/span&gt;
      &lt;a href={`/post/${post.slug}`}&gt;Read more...&lt;/a&gt;
    &lt;/div&gt;
  &lt;/article&gt;
);
</code></pre>
<p>The code is mostly the same, other than that we now have bare functions, rather than methods in a class. However, for
me, that makes a big difference. In the class-based example, my eyes see <code>class LatestPostsComponent {</code>, and
naturally scan all the way down to the closing curly bracket, concluding "that's the end of the class, and so the end
of the component". By comparison, when I read the functional component, I see <code>const LatestPostsComponent = props =&gt; {</code>,
and scan only to the end of that function. "There's the end of the function, and so the end of the component", I think
to myself. "But wait, what's all this other code sitting outside of my component, in the same module? Aha! It's another
function that takes data and renders a view! I can extract that out into a component all of it's own!"</p>
<p>Which is a very long-winded way of saying that functional components help us identify ways to follow point #2.</p>
<p>There are also optimisations coming to React in the future, which will make functional components more efficient than class-based ones.
(<strong>Update:</strong> It turns out that the performance implications of functional components are much more complicated than I
realised. I still recommend writing functional components by default, but if performance is a big concern, then you should
read and understand <a href="https://github.com/facebook/react/issues/5677" target="_blank">this</a> and <a href="https://github.com/rackt/redux/issues/1176" target="_blank">this</a>,
and figure out what works best for you.)</p>
<p>It's important to note that functional components have a few 'limitations', which I consider to be their greatest
strengths. The first is that a functional component cannot have a <code>ref</code> assigned to it. While a <code>ref</code> can be a convenient
way for a component to 'look up' it's children and communicate with them, my feeling is that this is The Wrong Way to
write React. <code>ref</code>s encourage a very imperative, almost jquery-like way of writing components, taking us away from
the functional, one-way data flow philosophy for which we chose React in the first place!</p>
<p>The other big difference is that functional components cannot have state attached to them, which is also a huge
advantage, because my next tip is to...</p>
<h3 id="-4-write-stateless-components-write-stateless-components-"><a href="#write-stateless-components" target="_blank">4. Write stateless components</a></h3>
<p>I would have to say that by far, the vast, vast majority of pain that I've felt when writing React-based apps, has been
caused by components that have too much state.</p>
<h4 id="state-makes-components-difficult-to-test">State makes components difficult to test</h4>
<p>There's practically nothing easier to test than pure, data-in data-out functions, so why would we throw away the
opportunity to define our components in such a way by adding state to them? When testing stateful components, now
we need to get our components into "the right state" in order to test their behaviour. We also need to come up with all
of the various combinations of state (which the component can mutate at any time), and props (which the component has no
control over), and figure out which ones to test, and how to do so. When components are just functions of input props,
testing is a lot easier. (More on testing later).</p>
<h4 id="state-makes-components-difficult-to-reason-about">State makes components difficult to reason about</h4>
<p>When reading the code for a very stateful component, you have to work a lot harder, mentally, to keep track of everything
that's going on. Questions like "Has that state been initialised yet?", "What happens if I change this state here?",
"How many other places change this state", "Is there a race condition on this state?", to mention a few, all become
very common. Tracing through stateful components to figure out how they behave becomes very painful.</p>
<h4 id="state-makes-it-too-easy-to-put-business-logic-in-the-component">State makes it too easy to put business logic in the component</h4>
<p>Searching through components to determine behaviour is not really something we should be doing anyway. Remember, React
is a <strong>view library</strong>, so while <em>render</em> logic in the components is OK, <em>business</em> logic is a massive code smell. But
when so much of your application's state is right there in the component, easily accessible by <code>this.state</code>, it can
become really tempting to start putting things like calculations or validation into the component, where it does not
belong. Revisiting my earlier point, this makes testing that much harder - you can't test render logic without the
business logic getting in the way, and vice versa!</p>
<h4 id="state-makes-it-difficult-to-share-information-to-other-parts-of-the-app">State makes it difficult to share information to other parts of the app</h4>
<p>When a component owns a piece of state, it's easy to pass it further down the component hierarchy, but any other
direction is tricky.</p>
<p>Of course, sometimes it makes sense for a particular component to totally own a particular piece of state. In which
case, fine, go ahead use <code>this.setState</code>. It's a legitimate part of the React component API, and I don't want to give
the impression that it should be off-limits. For example, if a user is typing into a field, it might not make sense to
expose every keypress to the whole app, and so the field may track its own intermediate state until a blur event
happens, whereupon the final input value is sent outwards to become state stored somewhere else. This scenario was
mentioned to me by a colleague recently, and I think it's a great example.</p>
<p>Just be very conscious of every time you add state to a component. Once you start, it can become very easy to add 'just
one more thing', and things get out of control before you know it!</p>
<h3 id="-5-use-redux-js-use-redux-js-"><a href="#use-redux-js" target="_blank">5. Use Redux.js</a></h3>
<p>In point #1, I said that React is just for views. The obvious question then is, "Where do I put all my state and logic?"
I'm glad you asked!</p>
<p>You may already be aware of <a href="https://facebook.github.io/flux/" target="_blank">Flux</a>, which is a style/pattern/architecture for
designing web applications, most commonly ones that use React for rendering. There are several frameworks out there that
implement the ideas of Flux, but without a doubt the one that I recommend is <a href="http://redux.js.org/" target="_blank">Redux.js</a>*.</p>
<p>I'm thinking of writing a whole separate blog post on the features and merits of Redux, but for now I'll just recommend
you read through the official tutorial at the above link, and provide this very brief description of how Redux works:</p>
<ol>
<li><strong>Components</strong> are given callback functions as props, which they call when a UI event happens</li>
<li>Those callbacks <strong>create and dispatch actions</strong> based on the event</li>
<li><strong>Reducers</strong> process the <strong>actions</strong>, computing the new <strong>state</strong></li>
<li>The new <strong>state</strong> of the whole application goes into a <strong>single store</strong>.</li>
<li><strong>Components</strong> receive the new state as <strong>props</strong> and re-render themselves where needed.</li>
</ol>
<p>Most of the above concepts are not unique to Redux, but Redux implements them in a very clean and simple way, with a
<a href="http://redux.js.org/docs/api/index.html" target="_blank">tiny API</a>. Having switched a decent sized project over from Alt.js to Redux,
some of the biggest benefits I've found are:</p>
<ul>
<li>The reducers are pure functions, which simply do <code>oldState + action = newState</code>. Each reducer computes a separate
piece of state, which is then all composed together to form the whole application. This makes all your business logic
and state transitions <em>really</em> easy to test.</li>
<li>The API is smaller, simpler, and better-documented. I've found it much quicker and easier to learn all of the concepts,
and therefore much easier to understand the flow of actions and information in my own projects.</li>
<li>If you use it the recommended way, only a very small number of components will depend upon Redux; all the other
components just receive state and callbacks as props. This keeps the components very simple, and reduces framework
lock-in.</li>
</ul>
<p>There are a few other libraries that complement Redux extremely well, which I also recommend you use:</p>
<ul>
<li><a href="https://facebook.github.io/immutable-js/" target="_blank">Immutable.js</a> - Immutable data structures for JavaScript! Store your state
in these, in order to make sure it isn't mutated where it shouldn't be, and to enforce reducer purity.</li>
<li><a href="https://github.com/gaearon/redux-thunk" target="_blank">redux-thunk</a> - This is used for when your actions need to have a side effect
other than updating the application state. For example, calling a REST API, or setting routes, or even dispatching other
actions.</li>
<li><a href="https://github.com/rackt/reselect" target="_blank">reselect</a> - Use this for composable, lazily-evaluated, views into your state. For
example, for a particular component you might want to:<ul>
<li>inject only the relevant part of the global state tree, rather than the whole thing</li>
<li>inject extra derived data, like totals or validation state, without putting it all in the store</li>
</ul>
</li>
</ul>
<p>You don't necessarily need all of these from day one. I would add Redux and Immutable.js as soon you have any state, reselect
as soon you have derived state, and redux-thunk as soon as you have routing or asynchronous actions. Adding them sooner
rather than later will save you the effort of retro-fitting them in later on.</p>
<p>* Depending on who you ask, Redux may or may not be 'true' Flux. Personally I feel that it's aligned well-enough with
the core ideas to call it a Flux framework, but the argument is a semantic one anyway.</p>
<h3 id="-6-always-use-proptypes-always-use-proptypes-"><a href="#always-use-proptypes" target="_blank">6. Always use propTypes</a></h3>
<p><a href="https://facebook.github.io/react/docs/reusable-components.html#prop-validation" target="_blank">propTypes</a> offer us a really easy way
to add a bit more type safety to our components. They look like this:</p>
<pre><code>const ListOfNumbers = props =&gt; (
  &lt;ol className={props.className}&gt;
    {
      props.numbers.map(number =&gt; (
        &lt;li&gt;{number}&lt;/li&gt;)
      )
    }
  &lt;/ol&gt;
);

ListOfNumbers.propTypes = {
  className: React.PropTypes.string.isRequired,
  numbers: React.PropTypes.arrayOf(React.PropTypes.number)
};
</code></pre>
<p>When in development (not production), if any component is not given a required prop, or is given the wrong type for one
of its props, then React will log an error to let you know. This has several benefits:</p>
<ul>
<li>It can catch bugs early, by preventing silly mistakes</li>
<li>If you use <code>isRequired</code>, then you don't need to check for <code>undefined</code> or <code>null</code> as often</li>
<li>It acts as documentation, saving readers from having to search through a component to find all the props that it needs</li>
</ul>
<p>The above list looks a bit like one you might see from someone advocating for static typing over dynamic typing.
Personally, I usually prefer dynamic typing for the ease and speed of development it provides, but I find that propTypes
add a lot of safety to my React components, without making things any more difficult. Frankly I see no reason <em>not</em> to
use them all the time.</p>
<p>One final tip is to make your tests fail on any propType errors. The following is a bit of a blunt instrument, but it's
simple and it works:</p>
<pre><code>beforeAll(() =&gt; {
  console.error = error =&gt; {
    throw new Error(error);
  };
});
</code></pre>
<h3 id="-7-use-shallow-rendering-use-shallow-rendering-"><a href="#use-shallow-rendering" target="_blank">7. Use shallow rendering</a></h3>
<p>Testing React components is still a bit of a tricky topic. Not because it's hard, but because it's still an evolving
area, and no single approach has emerged as the 'best' one yet. At the moment, my go-to method is to use
<a href="https://facebook.github.io/react/docs/test-utils.html#shallow-rendering" target="_blank">shallow rendering</a> and prop assertions.</p>
<p>Shallow rendering is nice, because it allows you to render a single component completely, but without delving into any
of its child components to render those. Instead, the resulting object will tell you things like the type and props of
the children. This gives us good isolation, allowing testing of a single component at a time.</p>
<p>There are three types of component unit tests I find myself most commonly writing:</p>
<h4 id="render-logic">Render logic</h4>
<p>Imagine a component that should conditionally display either an image, or a loading icon:</p>
<pre><code>const Image = props =&gt; {
  if (props.loading) {
    return &lt;LoadingIcon/&gt;;
  }

  return &lt;img src={props.src}/&gt;;
};
</code></pre>
<p>We might test it like this:</p>
<pre><code>describe('Image', () =&gt; {
  it('renders a loading icon when the image is loading', () =&gt; {
    const image = shallowRender(&lt;Image loading={true}/&gt;);

    expect(image.type).toEqual(LoadingIcon);
  });

  it('renders the image once it has loaded', () =&gt; {
    const image = shallowRender(&lt;Image loading={false} src="https://example.com/image.jpg"/&gt;);

    expect(image.type).toEqual('img');
  });
});
</code></pre>
<p>Easy! I should point out that the API for shallow rendering is slightly more complicated than what I've shown. The
<code>shallowRender</code> function used above is our own helper, which wraps the real API to make it easier to use.</p>
<p>Revisiting our <code>ListOfNumbers</code> component above, here is how we might test that the map is done correctly:</p>
<pre><code>describe('ListOfNumbers', () =&gt; {
  it('renders an item for each provided number', () =&gt; {
    const listOfNumbers = shallowRender(&lt;ListOfNumbers className="red" numbers={[3, 4, 5, 6]}/&gt;);

    expect(listOfNumbers.props.children.length).toEqual(4);
  });
});
</code></pre>
<h4 id="prop-transformations">Prop transformations</h4>
<p>In the last example, we dug into the children of the component being tested, to make sure that they were rendered
correctly. We can extend this by asserting that not only are the children there, but that they were given the correct
props. This is particulary useful when a component does some transformation on its props, before passing them on. For
example, the following component takes CSS class names as an array of strings, and passes them down as a single,
space-separated string:</p>
<pre><code>const TextWithArrayOfClassNames = props =&gt; (
  &lt;div&gt;
    &lt;p className={props.classNames.join(' ')}&gt;
     {props.text}
    &lt;/p&gt;
  &lt;/div&gt;
);

describe('TextWithArrayOfClassNames', () =&gt; {
  it('turns the array into a space-separated string', () =&gt; {
    const text = 'Hello, world!';
    const classNames = ['red', 'bold', 'float-right'];
    const textWithArrayOfClassNames = shallowRender(&lt;TextWithArrayOfClassNames text={text} classNames={classNames}/&gt;);

    const childClassNames = textWithArrayOfClassNames.props.children.props.className;
    expect(childClassNames).toEqual('red bold float-right');
  });
});
</code></pre>
<p>One common criticism of this approach to testing is the proliferation of <code>props.children.props.children</code>...
While it's not the prettiest code, personally I find that if I'm being annoyed by writing <code>props.children</code> too much in
the one test, that's a sign that the component is too big, complex, or deeply nested, and should be split up.</p>
<p>The other thing I often hear is that your tests become too dependant on the component's internal implementation, so that
changing your DOM structure slightly causes all of your tests to break. This is definitely a fair criticism, and a brittle
test suite is the last thing that anyone wants. The best way to manage this is to (wait for it) keep your components
small and simple, which should limit the number of tests that break due to any one component changing.</p>
<h4 id="user-interaction">User interaction</h4>
<p>Of course, components are not just for display, they're also interactive:</p>
<pre><code>const RedInput = props =&gt; (
  &lt;input className="red" onChange={props.onChange} /&gt;
)
</code></pre>
<p>Here's my favourite way to test these:</p>
<pre><code>describe('RedInput', () =&gt; {
  it('passes the event to the given callback when the value changes', () =&gt; {
    const callback = jasmine.createSpy();
    const redInput = shallowRender(&lt;RedInput onChange={callback}/&gt;);

    redInput.props.onChange('an event!');
    expect(callback).toHaveBeenCalledWith('an event!');
  });
});
</code></pre>
<p>It's a bit of a trivial example, but hopefully you get the idea.</p>
<h4 id="integration-testing">Integration testing</h4>
<p>So far I've only covered unit testing components in isolation, but you're also going to want some higher level tests in
order to ensure that your application connects up properly and actually works. I'm not going to go into too much detail
here, but basically:</p>
<ol>
<li><a href="https://facebook.github.io/react/docs/test-utils.html#renderintodocument" target="_blank">Render your entire tree of components</a>
(instead of shallow rendering).</li>
<li>Reach into the DOM (using the <a href="https://facebook.github.io/react/docs/test-utils.html" target="_blank">React TestUtils</a>, or
<a href="https://jquery.com/" target="_blank">jQuery</a>, etc) to find the elements you care about the most, and then<ol>
<li>assert on their HTML attributes or contents, or</li>
<li><a href="https://facebook.github.io/react/docs/test-utils.html#simulate" target="_blank">simulate DOM events</a> and then assert on the side
effects (DOM or route changes, AJAX calls, etc)</li>
</ol>
</li>
</ol>
<h4 id="on-tdd">On TDD</h4>
<p>In general, I don't use TDD when writing React components.</p>
<p>When working on a component, I often find myself churning its structure quite a bit, as I try to land on the simplest
HTML and CSS that looks right in whatever browsers I need to support. And because my component unit testing approach
tends to assert on the component structure, TDD would cause me to be constantly fixing my tests as I tweak the DOM,
which seems like a waste of time.</p>
<p>The other factor to this is that the components should be so simple that the advantages of test-first are diminished.
All of the complex logic and transformations are pulled out into action creators and reducers, which is where I can (and
do) reap the benefits of TDD.</p>
<p>Which brings me to my final point about testing. In this whole section, I've been talking about testing the components,
and that's because there's no special information needed for testing the rest of a Redux-based app. As a framework,
Redux has very little 'magic' that goes on behind the scenes, which I find reduces the need for excessive mocking or
other test boilerplate. Everything is just plain old functions (many of them pure), which is a real breath of fresh air
when it comes to testing.</p>
<h3 id="-8-use-jsx-es6-babel-webpack-and-npm-tooling-"><a href="#tooling" target="_blank">8. Use JSX, ES6, Babel, Webpack, and NPM</a></h3>
<p>The only React-specific thing here is JSX. For me JSX is a no-brainer over manually calling <code>React.createElement</code>. The
only disadvantage is that we add a small amount of build-time complexity, which is easily solved with
<a href="https://babeljs.io/" target="_blank">Babel</a>.</p>
<p>Once we've added Babel though, there's no reason not to go all out and use all the great <a href="http://es6-features.org/" target="_blank">ES6 features</a>,
like constants, arrow functions, default arguments, array and object destructuring, spread and rest operators, string
interpolation, iterators and generators, a decent module system, etc. It really feels like JavaScript is beginning to
'grow up' as a language these days, as long as you're prepared to spend a little bit of time setting up the tools.</p>
<p>We round things out with <a href="https://webpack.github.io/" target="_blank">Webpack</a> for bundling our code, and <a href="https://www.npmjs.com/" target="_blank">NPM</a>
for package management, and we're now fully JavaScript buzzword compliant :)</p>
<h3 id="-9-use-the-react-and-redux-dev-tools-dev-tools-"><a href="#dev-tools" target="_blank">9. Use the React and Redux dev tools</a></h3>
<p>Speaking of tooling, the development tools for React and Redux are pretty awesome. The
<a href="https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en" target="_blank">React dev tools</a>
let you inspect the rendered tree of React elements, which is incredibly useful for seeing how things actually look in the
browser. The Redux dev tools are <a href="https://www.youtube.com/watch?v=xsSnOQynTHs" target="_blank">even more impressive</a>, letting you see
every action that has happened, the state changes that they caused, and even giving you the ability to travel back in
time! You can add it either <a href="https://github.com/gaearon/redux-devtools" target="_blank">as a dev dependency</a>, or as a
<a href="https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en" target="_blank">browser extension</a>.</p>
<p>You can also set up hot module replacement with webpack, so that your page updates as soon as you save your code - no
browser refresh required. This makes the feedback loops a lot more efficient when tweaking your components and reducers.</p>
<h3 id="that-s-it-">That's it!</h3>
<p>Hopefully that will give you a bit of a head-start on React, and help you avoid some of the more common mistakes. If you
enjoyed this post, you might like to <a href="https://twitter.com/thecamjackson" target="_blank">follow me on Twitter</a>, or <a href="https://camjackson.net/atom.xml" target="_blank">subscribe to my RSS
feed</a>.</p>
<p>Thanks for reading!</p>
</div>
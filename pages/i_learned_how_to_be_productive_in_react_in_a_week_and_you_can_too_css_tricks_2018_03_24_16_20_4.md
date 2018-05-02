<a href="https://css-tricks.com/productive-in-react/">https://css-tricks.com/productive-in-react/</a><div id="articleHeader"><h1>                I Learned How to be Productive in React in a Week and You Can, Too              </h1></div>

    <p>

      
                By
        <a href="https://css-tricks.com/author/sdrasner/" target="_blank">
                    
            Sarah Drasner          
        </a>
                On
        <time>
          February 8, 2016        </time>
      

              
          <a href="https://css-tricks.com/tag/beginning-react/" target="_blank">beginning react</a>, <a href="https://css-tricks.com/tag/practical-react/" target="_blank">practical react</a>, <a href="https://css-tricks.com/tag/react/" target="_blank">react</a>, <a href="https://css-tricks.com/tag/react-keys/" target="_blank">react keys</a>, <a href="https://css-tricks.com/tag/react-props/" target="_blank">react props</a>, <a href="https://css-tricks.com/tag/react-refs/" target="_blank">react refs</a>        
      
    </p>

    

      
      <p>This article is not intended for seasoned <a href="https://facebook.github.io/react/" target="_blank">React</a> pros, but rather, those of us who make websites for a living and are curious how React can help us reason about updating user interfaces. I’ve been intrigued by React for some time, and now that it has gained some standing in the community as well as good reviews, the time to learn it seemed justified. There are so many new technologies constantly emerging in front end development that it’s sometimes hard to know if effort into learning something new will pay off. I’ll spend this article going over what I think some of the most valuable practical takeaways are so that you can get started.</p>
<h3 id="article-header-id-0"><a href="#article-header-id-0" target="_blank">#</a>Fair warning</h3>
<p>I’ve only spent about a week working with this material. That's on purpose. I'm writing this while I'm fresh with the technology and can write about it from that perspective. In this state I'm much better at remembering the tumbling blocks and findings along the way. </p>
<p>I used Wes Bos’ <a href="https://reactforbeginners.com/" target="_blank">React for Beginners</a> course, as well as <a href="http://reactfordesigners.com/labs/reactjs-introduction-for-people-who-know-just-enough-jquery-to-get-by/" target="_blank">React.js Introduction For People Who Know Just Enough jQuery To Get By</a>. I could not recommend these resources more highly. </p>
<p>In two days, I made this:</p>

<p>It is imperfect, but it goes much farther than I would have gotten on my own in that amount of time.</p>
<p>If you’re the kind of person who wants to dive right in and learn it all, including the build and requisite tooling, that’s awesome! <a href="http://facebook.github.io/react/downloads.html" target="_blank">Here’s where to start.</a> I would also suggest this pretty great Frontend Masters course: <a href="https://frontendmasters.com/courses/modern-web-apps/" target="_blank">Modern Web Apps</a>.</p>
<h3 id="article-header-id-1"><a href="#article-header-id-1" target="_blank">#</a>Mythbusters: Practicality in React Edition</h3>
<p>Before we get started, there are a couple of key myths I’d like to debunk that I think are blockers for a lot of people.</p>
<h4 id="article-header-id-2"><a href="#article-header-id-2" target="_blank">#</a>Myth #1: You have to use inline styles to use React.</h4>
<p>Nope! Not at all. You can use CSS just as you normally do. Having just spent a lot of time refactoring a giant CSS codebase, I would say that this is pretty important to establish. React, being fairly new, has not yet had to stand the test of design refreshes like other technologies have. If I had had to go back through thousands of lines of inline styles just to update things like <code>padding</code> and <code>line-height</code>, that would make me a sad developer indeed.</p>
<p>That said, there are times when inline styles do make sense. If you have a component that will change styles depending on its state (for instance: a data visualization) it would make absolute sense to work with inline styles so that you’re not maintaining an impractical number of static styles (in multiple places) to handle all possible states.</p>
<p>I’d think, though, that this would be on top of a base CSS that the application uses and be an exception rather than a rule. The web is a big place, though, so there are no absolutes.</p>
<h4 id="article-header-id-3"><a href="#article-header-id-3" target="_blank">#</a>Myth #2: You have to use JavaScript syntax for element attributes, which is not at all like HTML.</h4>
<p>One of the things I really love about Wes Bos’ teaching style is that he guides the viewer towards the more familiar approach and implementation. I generally like to err on the side of simple, and less obfuscated code, though I understand that others like higher degrees of abstraction.</p>
<p>He suggests that we write our markup with <a href="https://facebook.github.io/react/docs/jsx-in-depth.html" target="_blank">JSX</a>, which more closely resembles our friend, traditional HTML, so I found it to be much more clear. So, instead of this:</p>
<pre><code>return React.createElement("p", {className: "foo"}, "Hello, world!");</code></pre>
<p>We would write this:</p>
<pre><code>return (&lt;p className="foo"&gt;Hello, world!&lt;/p&gt;);</code></pre>
<p>Either works. But when we start to have more and more complexity in our markup, I found that the familiarity of HTML in the form of JSX served my understanding. Please keep in mind, though, that even with JSX, there are minor differences.</p>
<h4 id="article-header-id-4"><a href="#article-header-id-4" target="_blank">#</a>Myth #3: In order to try React, you have to understand all of the build tools.</h4>
<p>It’s true that in order to <em>use</em> React, you need to use build tools, so this is usually what tutorials start with. I would recommend, though, that as a total beginner, you should muck around on <a href="http://codepen.io/" target="_blank">CodePen</a>. It’s a good way to iterate quickly and learn before investing a lot of time in a brand new technology.</p>
<h3 id="article-header-id-5"><a href="#article-header-id-5" target="_blank">#</a>Using React in Typical Applications</h3>
<p>In typical applications using React 1.14+ we would start out by requiring React and ReactDOM:</p>
<pre><code>var React = require('react');
var ReactDOM = require('react-dom');</code></pre>
<p>And then call <code>ReactDOM.render</code>:</p>
<pre><code>ReactDOM.render(routes, document.querySelector('#main'));</code></pre>
<h3 id="article-header-id-6"><a href="#article-header-id-6" target="_blank">#</a>Using React in CodePen</h3>
<p>In our case, we will simply be selecting React from the dropdown in the JS panel (click the cog icon at the top of the panel), and then using <a href="https://babeljs.io/" target="_blank">Babel</a> as the compiler. </p>
<figure id="post-236625"><div class="readableLargeImageContainer"><img src="//cdn.css-tricks.com/wp-content/uploads/2016/01/react.gif" /></div></figure>
<p>We don’t need to <code>require</code> React or React DOM, since we haven’t routed anything, we’re using the app component directly. Our code will be amended simply to:</p>
<pre><code>React.render(&lt;App/&gt;, document.querySelector("#main"));</code></pre>
<pre><code>&lt;div id="main"&gt;&lt;/div&gt;</code></pre>
<p>Also, in order to get started, you’re going to need the <a href="https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en" target="_blank">React Devtools extension for Chrome</a>, or <a href="https://addons.mozilla.org/en-us/firefox/addon/react-devtools/" target="_blank">React Devtools Extension for Firefox</a> which is great for debugging our virtual DOM.</p>
<p>If CodePen, you can use <a href="http://blog.codepen.io/documentation/views/debug-view/" target="_blank">Debug View</a> and it will find React properly:</p>
<figure id="post-236626"><div class="readableLargeImageContainer"><img src="//cdn.css-tricks.com/wp-content/uploads/2016/01/react-devtools.jpg" /></div></figure>
<h3 id="article-header-id-7"><a href="#article-header-id-7" target="_blank">#</a>Up and running</h3>
<p>The basic building blocks that you need to know to make something is as follows:</p>
<pre><code>// App
var App = React.createClass({
  render: function() {
    return (
      &lt;div className="foo"&gt;Hello, world!&lt;/div&gt;
    )
  }
});
 
ReactDOM.render(&lt;App/&gt;, document.querySelector("#main"));</code></pre>

<p>Let’s break this down. On the last line we find the <code>main</code> div id, and on that we render the <code>&lt;App /&gt;</code> component, which will load all of our React application. You can use your React tab in Devtools to now see the DOM element we’ve created.</p>
<p>We’ve attached <code>&lt;App /&gt;</code> as the first component. The first thing to note here is that this tag is capitalized — while this isn’t required it’s a best practice with React components. The second is that it is self-closing. Tags in react must be closed, either by an additional closing tag (e.g. <code>&lt;/div&gt;</code>), or a self closing tag (e.g. <code>&lt;hr&gt;</code> would become <code>&lt;hr /&gt;</code>). This is just how JSX works and an error will be thrown otherwise.</p>
<p>Note the structure for creating the app component at the top. You will get very used to this syntax moving forward, as everything we will build today will work off of this key building block.</p>
<p>The last thing to note is that rather than using class, we’re using <code>className</code> on the element. This is a gotcha if you’re used to writing HTML markup for a webpage. Luckily, it’s easily solved. For more information on JSX and its syntax, <a href="https://facebook.github.io/react/docs/jsx-in-depth.html" target="_blank">these docs</a> are really good resources.</p>
<pre><code>// App
var App = React.createClass({
  render: function() {
    return (
      &lt;Header /&gt;
    )
  }
});
 
// Header
var Header = React.createClass({
 render: function() {
   return (
     &lt;div className="foo"&gt;Hello, world!&lt;/div&gt;
   )
 }
});
 
ReactDOM.render(&lt;App/&gt;, document.querySelector("#main"));</code></pre>

<p>In the next step, we’re extending app with a component. Header can be named whatever you would like it to be named, for clarity, we’ve named it the role it has in the document. You can see that if we also wanted to add a navigation element, that would be quite simple to add. Here’s the same page with just a standard bootstrap row of buttons for a <code>&lt;Nav /&gt;</code> component, and the more semantic <code>h1</code> for our "Hello, World!" instead of a <code>div</code>:</p>
<pre><code>// App
var App = React.createClass({
render: function() {
 return (
   &lt;div&gt;
     &lt;Nav /&gt;
     &lt;Header /&gt;
   &lt;/div&gt;
  )
 }
});
 
// Nav
var Nav = React.createClass({
 render: function() {
   return (
    &lt;ul className="nav nav-pills"&gt;
      &lt;li role="presentation" className="active"&gt;Home&lt;/li&gt;
      &lt;li role="presentation"&gt;Profile&lt;/li&gt;
      &lt;li role="presentation"&gt;Messages&lt;/li&gt;
    &lt;/ul&gt;
  )
 }
});
 
// Header
var Header = React.createClass({
 render: function() {
   return (
     &lt;h1 className="foo"&gt;Hello, world!&lt;/h1&gt;
   )
 }
});
 
ReactDOM.render(&lt;App/&gt;, document.querySelector("#main"));</code></pre>

<p>Pretty straightforward, huh? It’s just like building blocks of any web page. We make the nav and the header, and apply these components to the app component, which is rendered on the body. The only real gotcha of this last example would be the strange extra div you see around <code>&lt;Header /&gt;</code> and <code>&lt;Nav /&gt;</code>. This is because we must always return a single element. We can’t have two sibling elements, so we wrap them in a single div.</p>
<p>Now that you understand the building blocks, you can probably pretty easily piece together a page using React and React components. I’d suggest refactoring a page layout you’ve already made just to learn. Throw the stylesheet in there, and piece out the rest bit by bit until you’ve reconstructed its bones. It’s great practice.</p>
<p>There is a way to <a href="http://www.overreact.io/" target="_blank">automate this process</a>, but I would not suggest using a tool like this until you have already gone through the steps of building things out for yourself first. That way if you run into problems down the line, you know what’s going on.</p>
<h3 id="article-header-id-8"><a href="#article-header-id-8" target="_blank">#</a>The Usual Suspects: Variables & Event Handling</h3>
<p>Let’s do some small event handling and put in some simple variables first just to see how that goes.</p>
<p>Consider the first demo again (we'll use this throughout the article):</p>

<p>The blog post component has some pretty simple markup, so let’s start with that:</p>
<pre><code>// Blog Post
var Post = React.createClass({
  render : function() {
    return (
      &lt;div className="blog-post"&gt;
        &lt;h3 className="ptitle"&gt;{this.props.ptitle}&lt;small&gt;{this.props.date}&lt;/small&gt;&lt;/h3&gt;
        &lt;img className="thumbnail" src={this.props.pimg} /&gt;
        &lt;p&gt;{this.props.postbody}&lt;/p&gt;
        &lt;div className="callout callout-post"&gt;
          &lt;ul className="menu simple"&gt;
          &lt;li&gt;Author: {this.props.author}&lt;/li&gt;
          &lt;li&gt;Comments: {this.props.comments}&lt;/li&gt;
          &lt;li&gt;Tags: {h.getTaggedName()}&lt;/li&gt;
          &lt;/ul&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    )
  }
});</code></pre>
<p>Let's add an arbitrary variable and event handler to see how that works. First thing to think about is that if we're using JSX, curly brackets will let React know that we're ready to use some JavaScript. Therefore our variable will look like <code>{var}</code>. </p>
<p>We’re going to add the variable statement inside the render function call, but before we return the markup. We can then access it by calling the variable, in this case, <code>{com}</code>. The click event is an inline <code>onClick</code> handler, which probably goes against best practices you're used to. This is a name we chose, whereas render is a framework method. We call <code>{this.tryClick}</code>, and write a method stored as <code>tryClick</code> (an arbitrary name) within the same component, like so:</p>
<pre><code>// Blog Post
var Post = React.createClass({
  tryClick : function() {
    alert('just trying out click events lalala');
  },
  render : function() {
    var com = "Comments";
    return (
      &lt;div className="blog-post"&gt;
        &lt;h3 className="ptitle"&gt;{this.props.ptitle}&lt;small&gt;{this.props.date}&lt;/small&gt;&lt;/h3&gt;
        &lt;img className="thumbnail" src={this.props.pimg} /&gt;
        &lt;p&gt;{this.props.postbody}&lt;/p&gt;
        &lt;div className="callout callout-post"&gt;
          &lt;ul className="menu simple"&gt;
          &lt;li&gt;Author: {this.props.author}&lt;/li&gt;
          &lt;li&gt;{com}: {this.props.comments}&lt;/li&gt;
          &lt;li&gt;Tags: {h.getTaggedName()}&lt;/li&gt;
          &lt;/ul&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    )
  }
});</code></pre>
<p>The syntax for events in React begins with “on” and is camelCased. For example:</p>
<ul>
<li>click = onClick</li>
<li>mouseEnter = onMouseEnter</li>
<li>keyPress = onKeyPress</li>
</ul>
<p>You can find <a href="http://facebook.github.io/react/docs/events.html#supported-events" target="_blank">a full list</a> of all the supported events.</p>
<h3 id="article-header-id-9"><a href="#article-header-id-9" target="_blank">#</a>Combining React and Other Libraries (Greensock, in this case)</h3>
<p>I love <a href="http://greensock.com/" target="_blank">GSAP</a> for animation. You can use other libraries within React, so let’s combine GSAP and React and see how that goes. </p>
<p>We want to access other libraries at the correct time, so we have to make sure they are called immediately after the first render method. The method we use for this is called <code>componentDidMount</code>. We’ll explain a little more about other lifecycle methods further on, but what you need to know right now is this method is called immediately after the component is inserted into the document.</p>
<p>If you're used to jQuery, you're familiar with grabbing elements right out of the DOM. In this case, even though we are tweening DOM elements, we're going to use React's getDOMNode() instead of just grabbing them. You'll also see that we're actually calling the function to tween in the app component, and simply passing it down to our boxes. (You may have to hit rerun to see the animation.)</p>

<pre><code>// App
var App = React.createClass({
 componentDidMount: function() {
    var sq1 = this.refs.first.getDOMNode();
    var sq2 = this.refs.second.getDOMNode();
    var sq3 = this.refs.third.getDOMNode();
    var sq4 = this.refs.fourth.getDOMNode();
    var sq5 = this.refs.fifth.getDOMNode();
    var allSq = [sq1, sq2, sq3, sq4, sq5];
   
    TweenLite.set(allSq, {css:{transformPerspective:400, perspective:400, transformStyle:"preserve-3d"}}); 

    TweenMax.to(sq1, 2.5, {css:{rotationX:230, z:-600}, ease:Power2.easeOut}, "+=0.2");
    TweenMax.to(sq2, 2.5, {css:{rotationY:230, z:-150}, ease:Power4.easeOut}, "+=0.2");
    TweenMax.to(sq3, 2.5, {css:{rotationX:500, z:150}, ease:Power2.easeInOut}, "+=0.2");
    TweenMax.to(sq4, 2.5, {css:{rotationY:500, z:-150}, ease:Power4.easeOut}, "+=0.2");
    TweenMax.to(sq5, 2.5, {css:{rotationX:1000, z:100}, ease:Power2.easeOut}, "+=0.2");
 },
 render: function() {
   return (
     &lt;div className="scene"&gt;
        &lt;Box ref="first"&gt;&lt;/Box&gt;
        &lt;Box ref="second"&gt;&lt;/Box&gt;
        &lt;Box ref="third"&gt;&lt;/Box&gt;
        &lt;Box ref="fourth"&gt;&lt;/Box&gt;
        &lt;Box ref="fifth"&gt;&lt;/Box&gt;
    &lt;/div&gt;
   )
 }
});

// Box
var Box = React.createClass({
  render: function() {
    return (
      &lt;div className="squares"&gt;&lt;/div&gt;
    )
  }
});
 
ReactDOM.render(&lt;App/&gt;, document.querySelector("#main"));</code></pre>
<p>You may be used to accessing the DOM through jQuery or vanilla JavaScript. We can still do so, but here we're accessing pieces of the DOM through <code>getDOMNode()</code> and <code>refs</code>, on this line: <code>var sq1 = this.refs.squares1.getDOMNode();</code>. You can read a little more about this in the <a href="https://facebook.github.io/react/docs/working-with-the-browser.html" target="_blank">React docs</a>.</p>
<p>There are more React-specific ways to include motion in your projects- a really great one is Cheng Lou's <a href="https://github.com/chenglou/react-motion" target="_blank">React-Motion</a> and another good mention is <a href="https://github.com/azazdeaz/react-gsap-enhancer" target="_blank">React-GSAP-Enhancer</a>.</p>
<h3 id="article-header-id-10"><a href="#article-header-id-10" target="_blank">#</a>Creating a Global Helper Function</h3>
<p>You can even write helper functions that can be accessed by multiple components easily. We would use these with the same dot notation that we used with <code>this.functionName</code>. We store the helper function (in this CodePen demo we will do so at the start of the file, but in real applications, they would be stored in a separate file) and declare each function as an object the same way you do within the component structure.</p>
<p>Something like the correctly formatted date in the first demo with the blog posts would be:</p>
<pre><code>var h =  {
  getTime: function() {
     var month = ["jan", "feb", "march"]; // …. and so on
     var d = new Date();
     var mon = month[d.getMonth()];
     var day = d.getDate();
     var year = d.getFullYear();
     var dateAll = mon + " " + day + ", " + year;
   
     return dateAll;
  }
};</code></pre>
<p>And used like so: <code>{h.getTime()}</code></p>
<h3 id="article-header-id-11"><a href="#article-header-id-11" target="_blank">#</a>The Good Stuff: Managing State</h3>
<p>Ok! Now that we have the building blocks down, let’s get to some of the cool stuff.</p>
<p>React is surely good at building apps with easy-to-understand bite sized components, but what it’s really good at is managing state for these components. Let’s dive into that a little.</p>
<h4 id="article-header-id-12"><a href="#article-header-id-12" target="_blank">#</a>For this part, we’re going to go over two pretty key parts of understanding how to access and work with things that change.</h4>
<ol>
<li>The first is <strong>state</strong>. The component itself possesses it, which means that it’s scoped to the component, and we will refer to it like this <code>{this.state.foo}</code>. We can update state by calling <code>this.setState()</code>.</li>
<li>The second is refers to how we pass read-only data along from the parent to the component (think like app is the parent to <code>header</code> in the first example). We refer to this as <strong>props</strong>, as in property, and will use it directly in the components with <code>{this.props.foo}</code>. This data can’t be changed by its children.</li>
</ol>
<h4 id="article-header-id-13"><a href="#article-header-id-13" target="_blank">#</a>Any time we change either of these two things and our component relies on it, React will re-render the pieces of your component that it needs to.</h4>
<p>The beauty of the virtual DOM is that React figures out only which DOM Nodes need to be updated.</p>
<p>I’ve read a bunch on state now, but I think Wes said it the most clearly so I’m going to paraphase him: <strong>if you’re used to jQuery, you’re storing all of your data in the DOM. React avoids this entirely by by storing the data in an object (state), and then rendering things based off the object. It’s like one big master that everything is based off of.</strong></p>
<h3 id="article-header-id-14"><a href="#article-header-id-14" target="_blank">#</a>Trying Props Out</h3>
<p>Let’s try just <code>this.props</code> first, we’ll add <code>{this.props.title}</code> to the <code>Header</code> component, and then we can access it within the app. We’ll add a string to create the title:</p>
<pre><code>// App
var App = React.createClass({
  render: function() {
    return (
      &lt;Header greeting="Hello, world!" /&gt;
    )
  }
});
 
// Header
var Header = React.createClass({
  render: function() {
    return (
      &lt;div className="foo"&gt;
        &lt;h1&gt;{this.props.greeting}&lt;/h1&gt;
      &lt;/div&gt;
    )
  }
});
 
ReactDOM.render(&lt;App/&gt;, document.querySelector("#main"));</code></pre>
<p>We can also add a default for props, in the aptly named <code>getDefaultProps</code> lifecycle method. This is great because sometimes you don’t want to have to specify props for every component. An example of this would be a default profile avatar if the user hasn’t set one yet, like the egg on Twitter, or setting a list to be an empty array which will be filled up later.</p>
<pre><code>var ProfilePic = React.createClass({
  getDefaultProps: function() {
    return {
      value: 'twitter-egg.jpg'
    };
   ...
});</code></pre>
<h3 id="article-header-id-15"><a href="#article-header-id-15" target="_blank">#</a>Doin’ Stuff</h3>
<p>Now let’s build off of that to work with state a little. If we’re going eventually change <code>this.state</code>, we have to get it ready. To do so, we’ll use <code>getInitialState</code>, which lets us define what the state is at the get-go. We can’t add state without this.</p>
<p>Let’s just change the background based on user selection.</p>

<pre><code>// App
var App = React.createClass({
  /*setting state*/
  getInitialState: function() {
    return {
      bgColor: "teal"
    };
  },
  /*changes state*/
  handleColorChange: function (color) {
    // when we set state directly, react doesn't know
    // about it. that's why we use setState
    this.setState({ bgColor: color });
  },
  /*for the lifecycle methods*/
  updateBackgroundColor: function () {
    var body = document.querySelector('body')
    body.style.background = this.state.bgColor
  },
  /*lifecycle methods*/
  componentDidMount: function () { 
    this.updateBackgroundColor()
  },
  componentDidUpdate: function () { 
    this.updateBackgroundColor()
  },
  render: function() {
    return (
    /* by calling the title here on the component, we can access this.props on header */
      &lt;div className="foo"&gt;
        &lt;h1&gt;Hello, World!&lt;/h1&gt;
        &lt;label&gt;What color?
          &lt;ColorPicker value={this.state.bgColor} onColorChange={this.handleColorChange}/&gt;
        &lt;/label&gt;
      &lt;/div&gt;
    )
  }
});

// ColorPicker component
var ColorPicker = React.createClass({
  propTypes: {
    value: React.PropTypes.string.isRequired,
    onColorChange: React.PropTypes.func
  },
  handleChange: function(e) {
    e.preventDefault();
    var color = e.target.value
    
    // If whoever rendered us (the ColorPicker) is interested
    // when the color changes, let them know
    if (this.props.onColorChange)
      this.props.onColorChange(color);
  },
  render: function() {
    return (
      &lt;select value={this.props.value} onChange={this.handleChange}&gt;
        &lt;option value="orangered"&gt;orangered&lt;/option&gt;
        &lt;option value="teal"&gt;teal&lt;/option&gt;
        &lt;option value="orange"&gt;orange&lt;/option&gt;
        &lt;option value="indigo"&gt;indigo&lt;/option&gt;
        &lt;option value="red"&gt;red&lt;/option&gt;
      &lt;/select&gt;
    )
  }
});

ReactDOM.render(&lt;App/&gt;, document.querySelector('#main'));</code></pre>
<h4 id="article-header-id-16"><a href="#article-header-id-16" target="_blank">#</a>An important part of this to consider is that we need the <code>handleChange</code> function.</h4>
<p>In regular DOM life, native selects would not require you to do something like this because it would automatically be updating to the users selection. In React <em>all of the state</em> is being managed by the component, so if you need an input or a select to listen for changes, you have to write it. This means that the component is in charge of the state, not the user.</p>
<p>This may seem like a lot of work for a small amount of reward, but we’ve purposefully kept these examples pretty slim. The cool parts of React really come in when you’re dealing with a lot of complexity. As much as I love jQuery (and I still do love jQuery, it’s not a boolean), you have to perform checks pretty frequently when something is changing. React solves this by removing this need because of the simplicity of the direction of data-flow, which also makes it easier in highly complex applications to reason about.</p>
<h3 id="article-header-id-17"><a href="#article-header-id-17" target="_blank">#</a>State Concepts</h3>
<p>So now that we have the very basics down, let’s take a look really quickly at why we’re doing what we’re doing, as well as some best practices.</p>
<p>React works the best when we are updating states and rerendering the lower-level components. Fundamentally, we want these components to be mostly stateless, and receive data from the higher-level components. The components at the top of our hierarchy, like our app, work best when they are mostly stateful. That way they manage most of the interaction logic and pass state down using props. That said, there still will be times where each component will have it’s own state. It's important to remember, though, that siblings shouldn't talk to eachother directly, they should talk to their parent component.</p>
<figure id="post-236618"><div class="readableLargeImageContainer"><img src="//cdn.css-tricks.com/wp-content/uploads/2016/01/image01.jpg" /></div></figure>
<p>Therefore, we want to keep the state in the component as much as we possibly can. You don't ever actually have to worry about <em>when</em> stuff gets rendered. All you need to worry about is when state changes, and React takes care of rendering for you.</p>
<p>That kind of best practice ideology leads directly to why I’ll also advise you to not use props in <code>getInitialState</code>, and there’s more information here on why this is<a href="https://facebook.github.io/react/tips/props-in-getInitialState-as-anti-pattern.html" target="_blank"> considered an anti-pattern</a>.</p>
<p>We don’t want to abuse state too much. The rendering of the components is pretty fast, but performance can sink if you begin to try to manage too much state. There are some <a href="https://facebook.github.io/react/docs/update.html" target="_blank">ways to get around this</a> once it’s actually a problem, but best bet just to not get in that predicament to begin with.</p>
<p>The rest of this article is about how to best manage these states and keep the immutable concerns higher in the hierarchy, while still referencing our stateless components lower down.</p>
<h3 id="article-header-id-18"><a href="#article-header-id-18" target="_blank">#</a>Refs</h3>
<p>We can also access information about the element with something called ref. We use refs by attaching it to any component. It is then returned during the <code>render()</code> method, and we can then refer to it outside of the <code>render()</code> method. This is incredibly useful.</p>
<p>Consider <a href="http://codepen.io/sdras/full/RrKLqL/" target="_blank">the first Pen</a> again. Let’s think for a minute how we’re making these new blog posts, and use refs while doing so.</p>
<p>In each form input we have a ref, like:</p>
<pre><code>&lt;input type="text" ref="name" placeholder="Full Name required" required /&gt;</code></pre>
<p>On the form element itself, we call:</p>
<pre><code>onSubmit={this.createPost}</code></pre>
<p>which references the <code>createPost</code> function above the render function, and uses refs to store information from that submission:</p>
<pre><code>var post = {
 name : this.refs.name.value,
 ...
}</code></pre>
<p>and then we have a way to refer to it in the app state using <code>this.props</code>:</p>
<pre><code>this.props.addPost(post);</code></pre>
<figure id="post-236961"><div class="readableLargeImageContainer"><img src="https://cdn.css-tricks.com/wp-content/uploads/2016/01/refs-overview.jpg" alt="refs-overview" /></div></figure>
<p>That’s pretty handy because now we have a variable post, with objects that are storing its name (shown here), date, details, and so on. We still haven't stored any of this in the App state yet, we've only created a way for App to use it. Let's go over that next, along with <code>keys</code>.</p>
<p>I've used this example as a way of talking about refs in general, but in real-life applications, you might want to consider using something like <a href="https://www.npmjs.com/package/form-serialize" target="_blank">form-serialize</a> to serialize form fields to submit over AJAX.</p>
<h3 id="article-header-id-19"><a href="#article-header-id-19" target="_blank">#</a>Keys and Using Refs</h3>
<p>In our last section we made a way to store the data we collected in the form without passing it off. That's because in React, we want to manage this state in the top-level of our hierarchy. In order to store this state, we’re starting up our initial state with an empty object. That’s where we’ll eventually store our post data.</p>
<pre><code>getInitialState : function() {
  return {
    posts: {}
  }
},</code></pre>
<p>Then we have our addPost function. Note that we’re managing this here instead of on the form, even though we called it from the form. We’re giving the state a timestamp to keep the posts unique and also setting the state for the posts.</p>
<pre><code>addPost: function(post) {
  var timestamp = (new Date()).getTime();
  // update the state object
  this.state.posts['post-' + timestamp] = post;
  // set the state
  this.setState({ posts : this.state.posts });
},</code></pre>
<p>Each child in an array should have a unique <code>key.prop</code>. This is important because React will reuse as much of the existing DOM as possible. React uses <code>keys</code> to keep track of which elements in the DOM it should update. It keeps us from having to redraw all of the DOM elements when we rerender. That helps the performance of our app.</p>
<p>Now let’s take a look at the App again, and see what we do with our newly stored data from the form:</p>
<pre><code>// App
var App = React.createClass({
  getInitialState : function() {
    return {
      posts : {}
    }
  }, 
  addPost : function(post) {
    var timestamp = (new Date()).getTime();
    // update the state object
    this.state.posts['post-' + timestamp] = post;
    // set the state
    this.setState({ posts : this.state.posts });
  },
  renderPost : function(key){
    return &lt;NewPost key={key} index={key} details={this.state.posts[key]} /&gt;
  },
  render : function() {
   ...
    return (
      &lt;div&gt;
        &lt;Banner /&gt;
	    ...
          &lt;div className="list-of-posts"&gt;
              {Object.keys(this.state.posts).map(this.renderPost)}
          &lt;/div&gt;
          &lt;Submissions addPost={this.addPost}/&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    )
  }
});</code></pre>
<p>You can see that when we render the app, we use the Object.keys to create a new array. We then use <code>.map()</code> with the <code>renderPost</code> function we made earlier. For those unfamiliar with <code>.map()</code>, it’s useful for creating an array out of an existing one, you can think about it like a loop.</p>
<pre><code>&lt;div className="list-of-posts"&gt;
  {Object.keys(this.state.posts).map(this.renderPost)}
&lt;/div&gt;</code></pre>
<p>Now let's make that renderPost function we just called. We pass the key as a parameter and assign it as the key, the index, and create an object we’re calling details to hold information about the state of the posts.</p>
<pre><code>renderPost: function(key) {
  return &lt;NewPost key={key} index={key} details={this.state.posts[key]} /&gt;
},</code></pre>
<p>It might seem odd that we pass a <code>key</code> and an <code>index</code>, but inside a component we are unable to access the key <code>prop</code> so we pass another one called <code>index</code>. This renderPost function is simply creating a <code>&lt;NewPost /&gt;</code> component for every item in our array, with details passed down that we can access. This is pretty awesome because it means that if something in our state updates, it's propagating down and we can manage it in one spot.</p>
<p>Here's the <code>&lt;NewPost /&gt;</code> component, where we use details handed down from app to render all of the information. You can see that helper function we made earlier used for the correctly formatted date used here as <code>{h.getTime()}</code>:</p>
<pre><code>/*
  NewPost
  &lt;NewPost /&gt;
*/
var NewPost = React.createClass({
  render : function() {
    var details = this.props.details;
    return (
      &lt;div className="blog-post"&gt;
        &lt;h3 className="ptitle"&gt;{details.title}&lt;small&gt;{h.getTime()}&lt;/small&gt;&lt;/h3&gt;
        &lt;img className="thumbnail" src={details.image} alt={details.name}/&gt;
        &lt;p&gt;{details.desc}&lt;/p&gt;
        &lt;div className="callout callout-post"&gt;
          &lt;ul className="menu simple"&gt;
          &lt;li&gt;Author: {details.name}&lt;/li&gt;
          &lt;li&gt;Comments: 0&lt;/li&gt;
          &lt;li&gt;Tags: {h.getFunName()}&lt;/li&gt;
          &lt;/ul&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    )
  }
});</code></pre>
<figure id="post-236963"><div class="readableLargeImageContainer"><img src="//cdn.css-tricks.com/wp-content/uploads/2016/01/keys-overview-cropped.jpg" alt="Keys Overview" /></div></figure>

<h3 id="article-header-id-20"><a href="#article-header-id-20" target="_blank">#</a>All Together Now</h3>
<p>Now that we understand keys, let’s take a look at the big picture for a minute. We discussed <code>getInitialState</code>, <code>componentDidMount</code>, and <code>render</code>, but there is one more mounting method for React. It’s called <code>componentWillMount</code>. It’s similar to <code>componentDidMount</code>, but it executes immediately <em>before</em> the component renders for the first time. </p>
<figure id="post-236619"><div class="readableLargeImageContainer"><img src="//cdn.css-tricks.com/wp-content/uploads/2016/01/image00.jpg" /></div></figure>
<p>This diagram does not include everything that is available in React at all, but rather a glimpse at what we’ve covered thus far and enough to get you started playing around.</p>
<h3 id="article-header-id-21"><a href="#article-header-id-21" target="_blank">#</a>Conclusion</h3>
<p>There’s a lot more than this article to learn about React, this is just the start. Hopefully this beginner’s journey gives others a little insight into how to get up and running. This post was 20 pages long and we didn't even get to a ton of other important and related subjects, including but not limited to ES6, Browserify, Gulp, Webpack, or a myriad of alternative implementations. </p>
<p>For further learning, again, I <em>highly</em> suggest diving into <a href="https://reactforbeginners.com/" target="_blank">Wes Bos’ course</a>, and he's offering a 10% discount to CSS-Tricks readers with the code CSSTRICKS, as well as watching some videos on <a href="https://frontendmasters.com/courses/" target="_blank">Frontend Masters</a>. Michael Jackson has a wonderful <a href="https://reactjs-training.com." target="_blank">training course</a> that you can register for (we're having him come to Trulia in San Francisco in March! Stay tuned for sign ups). There’s also a great book by Artemij Fedosejev called <a href="http://www.amazon.com/React-js-Essentials-Artemij-Fedosejev/dp/1783551623/" target="_blank">React Essentials</a> and <a href="https://medium.com/@sapegin/react-and-redux-single-page-applications-resources-22cd859b0c1d#.rmw5bun9o" target="_blank">this list</a> that's worth bookmarking by Artem Sapegin. It shouldn't be understated that the <a href="https://facebook.github.io/react/docs/getting-started.html" target="_blank">React Docs</a> are quite good resources. Happy learning!</p>
<p><em>Many thanks to <a href="https://twitter.com/mjackson" target="_blank">Michael Jackson</a>, <a href="https://twitter.com/wesbos" target="_blank">Wes Bos</a>, and <a href="https://twitter.com/vlh" target="_blank">Val Head</a> for proofing this article.</em></p>

<div id="jp-relatedposts">
	<h3 id="article-header-id-22"><a href="#article-header-id-22" target="_blank">#</a><em>Related</em></h3>
<div><div><a href="https://css-tricks.com/projects-need-react/" title="Which Projects Need React? All Of Them!

When does a project need React? That's the question Chris Coyier addressed in a recent blog post. I'm a big fan of Chris' writing, so I was curious to see what he had to say. In a nutshell, Chris puts forward a series of good and bad reasons why one…" target="_blank" class="readableLinkWithMediumImage"><img src="https://i0.wp.com/css-tricks.com/wp-content/uploads/2017/04/tools.jpg?resize=350%2C200&ssl=1" width="350" alt="Which Projects Need React? All Of Them!" /></a><h4><a href="https://css-tricks.com/projects-need-react/" title="Which Projects Need React? All Of Them!

When does a project need React? That's the question Chris Coyier addressed in a recent blog post. I'm a big fan of Chris' writing, so I was curious to see what he had to say. In a nutshell, Chris puts forward a series of good and bad reasons why one…" target="_blank">Which Projects Need React? All Of Them!</a></h4><p>When does a project need React? That's the question Chris Coyier addressed in a recent blog post. I'm a big fan of Chris' writing, so I was curious to see what he had to say. In a nutshell, Chris puts forward a series of good and bad reasons why one…</p></div><div><h4><a href="https://css-tricks.com/css-modules-part-3-react/" title="CSS Modules and React

In this final post of our series on CSS Modules, I’ll be taking a look at how to make a static React site with the thanks of Webpack. This static site will have two templates: a homepage and an about page with a couple of React components to explain how…" target="_blank">CSS Modules and React</a></h4><p>In this final post of our series on CSS Modules, I’ll be taking a look at how to make a static React site with the thanks of Webpack. This static site will have two templates: a homepage and an about page with a couple of React components to explain how…</p></div><div><h4><a href="https://css-tricks.com/creating-svg-icon-system-react/" title="Creating an SVG Icon System with React

I recently went to Michael Jackson and Ryan Florence’s ReactJS Training. I was really excited to attend, partially because I had so many questions about SVG and React. There are a lot of bits about working with React and SVG, and especially manipulating it, that aren’t quite supported yet. One…" target="_blank">Creating an SVG Icon System with React</a></h4><p>I recently went to Michael Jackson and Ryan Florence’s ReactJS Training. I was really excited to attend, partially because I had so many questions about SVG and React. There are a lot of bits about working with React and SVG, and especially manipulating it, that aren’t quite supported yet. One…</p></div></div></div>
    
<a href="https://javascriptplayground.com/context-in-reactjs-applications/">https://javascriptplayground.com/context-in-reactjs-applications/</a><div id="articleHeader"><h1>Context in ReactJS Applications</h1></div>
    
    <p>There is a lot of confusion amongst React developers on what context is, and why it exists. It’s also a feature that’s been hidden in the React documentation in the past and, <a href="https://facebook.github.io/react/docs/context.html" target="_blank">although it is now documented on the React site</a> I thought a post on its usage and when to use it would be of use.</p>

<p>The short answer is that you should <strong>very rarely, if ever</strong> use context in your own React components. However, if you’re writing a library of components, it can come in useful, and we’ll discuss why this is later.</p>

<h2 id="what-is-context-in-react-and-how-does-it-work">What is context in React, and how does it work?</h2>

<p>In React the primary mechanism for communication between your components is through properties, or <code>props</code>, for short. Parent components can pass properties down to their children:</p>

<div><div><pre><code>const ParentComponent = () =&gt; {
  const foo = 2;
  return &lt;ChildComponent foo={foo} /&gt;;
};
</code></pre></div></div>

<p>Here, the parent component <code>ParentComponent</code> passes the prop <code>foo</code> through to its child, <code>ChildComponent</code>.</p>

<blockquote>
  <p>Here, a <em>child component</em> is a component that another component renders. A <em>parent component</em> is a component that directly renders another.</p>
</blockquote>

<p>If a child component wants to communicate back to its parent, it can do so through props, most commonly by its parent providing a <em>callback property</em> that the child can call when some event happens:</p>

<div><div><pre><code>const ParentComponent = () =&gt; {
  const letMeKnowAboutSomeThing = () =&gt; console.log('something happened!');

  return &lt;ChildComponent letMeKnowAboutSomeThing={letMeKnowAboutSomeThing} /&gt;;
};

const ChildComponent = props =&gt; {
  const onClick = e =&gt; {
    e.preventDefault();
    props.letMeKnowAboutSomeThing();
  };

  return &lt;a onClick={onClick}&gt;Click me!&lt;/a&gt;;
};
</code></pre></div></div>

<p>The key thing about this communication is that it’s <em>explicit</em>. Looking at the code above, you know how the components are communicating, where the <code>letMeKnowAboutSomeThing</code> function comes from, who calls it, and which two components are in communication. <a href="http://codepen.io/jackfranklin/pen/vgvYOa?editors=0011" target="_blank">You can see this in action on CodePen</a>.</p>

<p>This property of React, its explicitness of data passing between components, is one of its best features. React is very explicit as a rule, and this is in my experience leads to clearer code that’s much easier to maintain and debug when something goes wrong. You simply have to follow the path of props to find the problem.</p>

<p>This diagram shows how props keep communication clear but can get a little excessive as you gain many layers in your application; each component has to explictly pass props down to any children.</p>

<p><div class="readableLargeImageContainer"><img src="/img/posts/context-in-react/props.png" /></div></p>

<p>One issue you might find in big apps is that you might need to pass props from a top level <code>ParentComponent</code> to a deeply nested <code>ChildComponent</code>. The components in between will probably have no use the these props and should probably not even know about them. When this situation arises, you can consider using React’s context feature.</p>

<p>Context acts like a portal in your application in which components can make data available to other components further down the tree without being passed through explictly as props.</p>

<p><div class="readableLargeImageContainer"><img src="/img/posts/context-in-react/context.png" /></div></p>

<p>When a component defines some data onto its <em>context</em>, any of its descendants can access that data. That means any child further down in the component tree can access data from it, without being passed it as a property. Let’s take a look at context in action.</p>

<h2 id="how-to-use-context-in-react-applications">How to use <code>context</code> in React applications</h2>

<p>First, on the <em>parent component</em>, we define two things:</p>

<ol>
  <li>A function, <code>getChildContext</code>, which defines what context is exposed to its descendants.</li>
  <li>A static property, <code>childContextTypes</code>, which defines the types of the objects that <code>getChildContext</code> returns.</li>
</ol>

<p>For a component to provide context to its descendants, it must define both of the above. Here, <code>ParentComponent</code> exposes the property <code>foo</code> on its context:</p>

<div><div><pre><code>class ParentComponent extends React.Component {
  getChildContext() {
    return { foo: 'bar' };
  }

  render() {
    return &lt;ChildComponent /&gt;;
  }
}

ParentComponent.childContextTypes = {
  foo: React.PropTypes.string,
};
</code></pre></div></div>

<p><code>ChildComponent</code> can now gain access to the <code>foo</code> property by defining a static property <code>contextTypes</code>:</p>

<div><div><pre><code>const ChildComponent = (props, context) =&gt; {
  return &lt;p&gt;The value of foo is: {context.foo}&lt;/p&gt;;
};
ChildComponent.contextTypes = {
  foo: React.PropTypes.string,
};
</code></pre></div></div>

<blockquote>
  <p>In a functional, stateless component, <code>context</code> is accessed via the second argument to the function. In a standard class component, it’s available as <code>this.context</code>.</p>
</blockquote>

<p>What’s important here though is that any component that <code>ChildComponent</code> renders, or any component its children render, and so on, are able to access the same context just by defining <code>contextTypes</code>.</p>

<h2 id="why-you-should-avoid-context">Why you should avoid context</h2>

<p>There’s a few reasons why you would want to avoid using context in your own code.</p>

<h4 id="1-hard-to-find-the-source">1. Hard to find the source.</h4>

<p>Imagine that you’re working on a component on a large application that has hundreds of components. There’s a bug in one of them, so you go hunting and you find some component that uses context, and the value it’s outputting is wrong.</p>

<div><div><pre><code>const SomeAppComponent = (props, context) =&gt; (
  &lt;div&gt;
    &lt;p&gt;Hey user, the current value of something is {context.value}&lt;/p&gt;
    &lt;a onClick={context.onSomeClick()}&gt;Click here to change it.&lt;/a&gt;
  &lt;/div&gt;
);

SomeAppComponent.contextTypes = {
  value: React.PropTypes.number.isRequired,
  onSomeClick: React.PropTypes.func.isRequired,
};
</code></pre></div></div>

<p>The bug is related to the click event not updating the right value, so you now go looking for the definition of that function. If it was being passed as a property, you could go immediately to the place where this component is rendered (which is usually just a case of searching for its name), and start debugging. In the case that you’re using context, you have to search for the function name and hope that you find it. This could be found easily, granted, but it also could be a good few components up the chain, and as your apps get larger the chances of you finding the source quickly gets smaller.</p>

<p>It’s similar to the problem when you work in an object oriented language and inherit from classes. The more classes you inherit from (or in React, the further down the component tree you get), it’s harder to find the source for a particular function that’s been inherited.</p>

<h4 id="2-binds-components-to-a-specific-parent">2. Binds components to a specific parent</h4>

<p>A component that expects only properties (or no properties at all) can be used anywhere. It is entirely reusable and a component wanting to render it need only pass in the properties that it expects. If you need to use the component elsewhere in your application you can do easily; just by supplying the right properties.</p>

<p>However, if you have a component that needs specific context, you couple it to having to be rendered by a parent that supplies some context. It’s then harder to pick up and move, because you have to move the original component and then make sure that its new parent (or one of its parents) provides the context required.</p>

<h4 id="3-harder-to-test">3. Harder to test</h4>

<p>Related to the previous point, components that need context are much harder to test. Here’s a test, using <a href="http://airbnb.io/enzyme/" target="_blank">Enzyme</a>, that tests a component that expects a <code>foo</code> prop:</p>

<div><div><pre><code>const wrapper = mount(&lt;SomeComponent foo="bar" /&gt;);
</code></pre></div></div>

<p>And here’s that same test when we need <code>SomeComponent</code> to have a specific piece of context:</p>

<div><div><pre><code>class ParentWithContext extends React.Component {
  getChildContext() {...}

  render() {
    return &lt;SomeComponent /&gt;
  }
}
ParentWithContext.childContextTypes = {...}

const wrapper = mount(&lt;ParentWithContext /&gt;)
</code></pre></div></div>

<p>It’s harder here because we have to build the right parent component - it’s messier and quite verbose just to set up the component in the right context for testing.</p>

<blockquote>
  <p>You can actually use Enzyme’s <a href="http://airbnb.io/enzyme/docs/api/ReactWrapper/setContext.html" target="_blank">setContext</a> to set context for these tests - but I tend to try to avoid any methods like this that breaks the React abstraction. You also wouldn’t be able to do this so easily in other testing frameworks.</p>
</blockquote>

<h4 id="4-unclear-semantics-around-context-value-changes-and-rerenders">4. Unclear semantics around context value changes and rerenders.</h4>

<p>With properties and state, it’s very clear to React when it should rerender a component:</p>

<ol>
  <li>When a component’s properties change.</li>
  <li>When <code>this.setState</code> is called.</li>
</ol>

<p>The <code>getChildContext</code> function is called whenever state or properties change, so in theory you can rely on components that use <code>context</code> values reliably updating. The problem though is <code>shouldComponentUpdate</code>. Any component can define <code>shouldComponentUpdate</code>, making it return <code>false</code> if it knows that it doesn’t need to be re-rendered. If an interim component does this, a child component won’t update, even if a context value changes:</p>

<div><div><pre><code>TopLevelComponent
- defines context.foo

    MidLevelComponent
    - defines `shouldComponentUpdate` to return `false`

        ChildComponent
        - renders `context.foo` into the DOM
</code></pre></div></div>

<p>In the above example, if <code>context.foo</code> changes, <code>ChildComponent</code> will not render, because its parent returned <code>false</code> from <code>shouldComponentUpdate</code>. This makes bugs possible and leaves us with no reliable way to update context and ensure renders, so this is a very good reason to avoid using <code>context</code>.</p>

<h2 id="when-to-use-context">When to use context</h2>

<p>If you’re a library author, context is useful. Libraries like <a href="https://github.com/ReactTraining/react-router/blob/v4/packages/react-router/modules/Router.js#L13" target="_blank">React Router use context</a> to allow the components that they provide application developers to communicate. When you’re writing a library that provides components that need to talk to each other, or pass values around, <code>context</code> is perfect. Another famous library that makes use of context is <a href="https://github.com/reactjs/react-redux/blob/master/src/components/Provider.js#L23" target="_blank">react-redux</a>. I encourage you to look through the source code for both React Router and React Redux, you can learn a lot about React by doing so.</p>

<p>Let’s build our own router library, <code>RubbishRouter</code>. It will define two components: <code>Router</code> and <code>Route</code>. The <code>Router</code> component needs to expose a <code>router</code> object onto the context, so our <code>Route</code> components can pick up on it and use it to function as expected.</p>

<p><code>Router</code> will be used to wrap our entire application, and the user will use multiple <code>Route</code> components to define parts of the app that should only render if the URL matches. To do this, each <code>Route</code> will take a <code>path</code> property, indicating the path that they should match before rendering.</p>

<p>First, <code>Router</code>. It exposes the <code>router</code> object on the context, and other than that it simply renders the children that it’s given:</p>

<div><div><pre><code>const { Component, PropTypes } = React;

class Router extends Component {
  getChildContext() {
    const router = {
      register(url) {
        console.log('registered route!', url);
      },
    };
    return { router: router };
  }
  render() {
    return &lt;div&gt;{this.props.children}&lt;/div&gt;;
  }
}
Router.childContextTypes = {
  router: PropTypes.object.isRequired,
};
</code></pre></div></div>

<p><code>Route</code> expects to find <code>this.context.router</code>, and it registers itself when it’s rendered:</p>

<div><div><pre><code>class Route extends Component {
  componentWillMount() {
    this.context.router.register(this.props.path);
  }
  render() {
    return &lt;p&gt;I am the route for {this.props.path}&lt;/p&gt;;
  }
}
Route.contextTypes = {
  router: PropTypes.object.isRequired,
};
</code></pre></div></div>

<p>Finally, we can use the <code>Router</code> and <code>Route</code> components in our own app:</p>

<div><div><pre><code>const App = () =&gt; (
  &lt;div&gt;
    &lt;Router&gt;
      &lt;div&gt;
        &lt;Route path="/foo" /&gt;
        &lt;Route path="/bar" /&gt;
        &lt;div&gt;
          &lt;Route path="/baz" /&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/Router&gt;
  &lt;/div&gt;
);
</code></pre></div></div>

<p>The beauty of context in this situation is that as library authors we can provide components that can work in any situation, regardless of where they are rendered. As long as all <code>Route</code> components are within a <code>Router</code>, it doesn’t matter at what level, and we don’t tie application developers to a specific structure.</p>

<h2 id="conclusion">Conclusion</h2>

<p>Hopefully this blog post has shown you how and when to use context in React, and why more often than not you’d be better eschewing it in favour of props.</p>

<p>Thank you to the following blog posts and documentation for providing great material whilst putting this blog post together:</p>



<p>Thank you also to <a href="https://twitter.com/ArnaudRinquin" target="_blank">Arnaud Rinquin</a> for taking the time to review this post.</p>

    
    <hr />

    <div>
      <p>
        If you enjoyed this article please feel free to <a href="https://twitter.com/intent/tweet?text=Context in ReactJS Applications&url=https://www.javascriptplayground.com/context-in-reactjs-applications/&via=Jack_Franklin&related=Jack_Franklin" title="Share on Twitter" target="_blank">share it on Twitter</a>.
      </p>

    </div>

    <hr />

    <div>
      <p>
        Don't miss my latest course on <a href="/testing-react-enzyme-jest" target="_blank">Testing React with Enyzme and Jest</a>! The first five videos are free and available to watch now. You'll learn how to write testable React code, test complex components and use Jest and Enzyme effectively to write clean, thorough tests. <a href="/testing-react-enzyme-jest" target="_blank">Get started now</a>.
      </p>
    </div>

      <hr />

      
      <div id="mc_embed_signup">
        <h4>Subscribe to keep up to date with the latest content.</h4>
        <p>Join the JS Playground mailing list to be kept up to date with the latest tutorials, screencasts and more. You won't be spammed and you can unsubscribe at any time.</p>
        
          
        
      </div>

      

      <hr />

      <div>
        <img src="/img/head.png" alt="Headshot of Jack Franklin" />
        <div>
          <p>Jack is JavaScript and React developer in London. He's also a keen <a href="http://elmplayground.com" target="_blank">Elm enthusiast</a>, <a href="https://speakerdeck.com/jackfranklin" target="_blank">conference speaker</a> and <a href="http://twitter.com/jack_franklin" target="_blank">tweets far too often</a>.</p>

          
        </div>
      </div>
    
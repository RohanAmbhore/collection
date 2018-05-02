<a href="https://reactjs.org/docs/react-component.html">https://reactjs.org/docs/react-component.html</a><div id="articleHeader"><h1>React.Component</h1></div><p><a href="/docs/components-and-props.html" target="_blank">Components</a> let you split the UI into independent, reusable pieces, and think about each piece in isolation. <code>React.Component</code> is provided by <a href="/docs/react-api.html" target="_blank"><code>React</code></a>.</p>
<h2 id="overview">Overview</h2>
<p><code>React.Component</code> is an abstract base class, so it rarely makes sense to refer to <code>React.Component</code> directly. Instead, you will typically subclass it, and define at least a <a href="#render" target="_blank"><code>render()</code></a> method.</p>
<p>Normally you would define a React component as a plain <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes" target="_blank">JavaScript class</a>:</p>
<div>
      <pre><code>class Greeting extends React.Component {
  render() {
    return &lt;h1&gt;Hello, {this.props.name}&lt;/h1&gt;;
  }
}
</code></pre>
      </div>
<p>If you don’t use ES6 yet, you may use the <code>create-react-class</code> module instead. Take a look at <a href="/docs/react-without-es6.html" target="_blank">Using React without ES6</a> to learn more.</p>
<p>Note that <strong>we don’t recommend creating your own base component classes</strong>. Code reuse is primarily achieved through composition rather than inheritance in React. Take a look at <a href="/docs/composition-vs-inheritance.html" target="_blank">these common scenarios</a> to get a feel for how to use composition.</p>
<h3 id="the-component-lifecycle">The Component Lifecycle</h3>
<p>Each component has several “lifecycle methods” that you can override to run code at particular times in the process. Methods prefixed with <strong><code>will</code></strong> are called right before something happens, and methods prefixed with <strong><code>did</code></strong> are called right after something happens.</p>
<h4 id="mounting">Mounting</h4>
<p>These methods are called when an instance of a component is being created and inserted into the DOM:</p>

<h4 id="updating">Updating</h4>
<p>An update can be caused by changes to props or state. These methods are called when a component is being re-rendered:</p>

<h4 id="unmounting">Unmounting</h4>
<p>This method is called when a component is being removed from the DOM:</p>
<ul>
<li><a href="#componentwillunmount" target="_blank"><code>componentWillUnmount()</code></a></li>
</ul>
<h4 id="error-handling">Error Handling</h4>
<p>This method is called when there is an error during rendering, in a lifecycle method, or in the constructor of any child component.</p>
<ul>
<li><a href="#componentdidcatch" target="_blank"><code>componentDidCatch()</code></a></li>
</ul>
<h3 id="other-apis">Other APIs</h3>
<p>Each component also provides some other APIs:</p>

<h3 id="class-properties">Class Properties</h3>

<h3 id="instance-properties">Instance Properties</h3>

<hr />
<h2 id="reference">Reference</h2>
<h3 id="render"><code>render()</code></h3>
<div>
      <pre><code>render()
</code></pre>
      </div>
<p>The <code>render()</code> method is required.</p>
<p>When called, it should examine <code>this.props</code> and <code>this.state</code> and return one of the following types:</p>
<ul>
<li><strong>React elements.</strong> Typically created via JSX. An element can either be a representation of a native DOM component (<code>&lt;div /&gt;</code>), or a user-defined composite component (<code>&lt;MyComponent /&gt;</code>).</li>
<li><strong>String and numbers.</strong> These are rendered as text nodes in the DOM.</li>
<li><strong>Portals</strong>. Created with <a href="/docs/portals.html" target="_blank"><code>ReactDOM.createPortal</code></a>.</li>
<li><code>null</code>. Renders nothing.</li>
<li><strong>Booleans</strong>. Render nothing. (Mostly exists to support <code>return test && &lt;Child /&gt;</code> pattern, where <code>test</code> is boolean.)</li>
</ul>
<p>When returning <code>null</code> or <code>false</code>, <code>ReactDOM.findDOMNode(this)</code> will return <code>null</code>.</p>
<p>The <code>render()</code> function should be pure, meaning that it does not modify component state, it returns the same result each time it’s invoked, and it does not directly interact with the browser. If you need to interact with the browser, perform your work in <code>componentDidMount()</code> or the other lifecycle methods instead. Keeping <code>render()</code> pure makes components easier to think about.</p>
<blockquote>

<p><code>render()</code> will not be invoked if <a href="#shouldcomponentupdate" target="_blank"><code>shouldComponentUpdate()</code></a> returns false.</p>
</blockquote>
<h4 id="fragments">Fragments</h4>
<p>You can also return multiple items from <code>render()</code> using an array:</p>
<div>
      <pre><code>render() {
  return [
    &lt;li key="A"&gt;First item&lt;/li&gt;,
    &lt;li key="B"&gt;Second item&lt;/li&gt;,
    &lt;li key="C"&gt;Third item&lt;/li&gt;,
  ];
}
</code></pre>
      </div>
<blockquote>
<p>Note:</p>
<p>Don’t forget to <a href="/docs/lists-and-keys.html#keys" target="_blank">add keys</a> to elements in a fragment to avoid the key warning.</p>
</blockquote>
<p>Since <a href="/blog/2017/11/28/react-v16.2.0-fragment-support.html" target="_blank">React 16.2.0</a>, the same can also be accomplished using <a href="/docs/fragments.html" target="_blank">fragments</a>, which don’t require keys for static items:</p>
<div>
      <pre><code>render() {
  return (
    &lt;React.Fragment&gt;
      &lt;li&gt;First item&lt;/li&gt;
      &lt;li&gt;Second item&lt;/li&gt;
      &lt;li&gt;Third item&lt;/li&gt;
    &lt;/React.Fragment&gt;
  );
}
</code></pre>
      </div>
<hr />
<h3 id="constructor"><code>constructor()</code></h3>
<div>
      <pre><code>constructor(props)
</code></pre>
      </div>
<p>The constructor for a React component is called before it is mounted. When implementing the constructor for a <code>React.Component</code> subclass, you should call <code>super(props)</code> before any other statement. Otherwise, <code>this.props</code> will be undefined in the constructor, which can lead to bugs.</p>
<p>Avoid introducing any side-effects or subscriptions in the constructor. For those use cases, use <code>componentDidMount()</code> instead.</p>
<p>The constructor is the right place to initialize state. To do so, just assign an object to <code>this.state</code>; don’t try to call <code>setState()</code> from the constructor. The constructor is also often used to bind event handlers to the class instance.</p>
<p>If you don’t initialize state and you don’t bind methods, you don’t need to implement a constructor for your React component.</p>
<p>In rare cases, it’s okay to initialize state based on props. This effectively “forks” the props and sets the state with the initial props. Here’s an example of a valid <code>React.Component</code> subclass constructor:</p>
<div>
      <pre><code>constructor(props) {
  super(props);
  this.state = {
    color: props.initialColor
  };
}
</code></pre>
      </div>
<p>Beware of this pattern, as state won’t be up-to-date with any props update. Instead of syncing props to state, you often want to <a href="/docs/lifting-state-up.html" target="_blank">lift the state up</a> instead.</p>
<p>If you “fork” props by using them for state, you might also want to implement <a href="#static-getderivedstatefromprops" target="_blank"><code>getDerivedStateFromProps()</code></a> to keep the state up-to-date with them. But lifting state up is often easier and less bug-prone.</p>
<hr />
<h3 id="static-getderivedstatefromprops"><code>static getDerivedStateFromProps()</code></h3>
<div>
      <pre><code>static getDerivedStateFromProps(nextProps, prevState)
</code></pre>
      </div>
<p><code>getDerivedStateFromProps</code> is invoked after a component is instantiated as well as when it receives new props. It should return an object to update state, or null to indicate that the new props do not require any state updates.</p>
<p>Note that if a parent component causes your component to re-render, this method will be called even if props have not changed. You may want to compare new and previous values if you only want to handle changes.</p>
<p>Calling <code>this.setState()</code> generally doesn’t trigger <code>getDerivedStateFromProps()</code>.</p>
<hr />
<h3 id="unsafe_componentwillmount"><code>UNSAFE_componentWillMount()</code></h3>
<div>
      <pre><code>UNSAFE_componentWillMount()
</code></pre>
      </div>
<p><code>UNSAFE_componentWillMount()</code> is invoked just before mounting occurs. It is called before <code>render()</code>, therefore calling <code>setState()</code> synchronously in this method will not trigger an extra rendering. Generally, we recommend using the <code>constructor()</code> instead for initializing state.</p>
<p>Avoid introducing any side-effects or subscriptions in this method. For those use cases, use <code>componentDidMount()</code> instead.</p>
<p>This is the only lifecycle hook called on server rendering.</p>
<blockquote>

<p>This lifecycle was previously named <code>componentWillMount</code>. That name will continue to work until version 17. Use the <a href="https://github.com/reactjs/react-codemod#rename-unsafe-lifecycles" target="_blank"><code>rename-unsafe-lifecycles</code> codemod</a> to automatically update your components.</p>
</blockquote>
<hr />
<h3 id="componentdidmount"><code>componentDidMount()</code></h3>
<div>
      <pre><code>componentDidMount()
</code></pre>
      </div>
<p><code>componentDidMount()</code> is invoked immediately after a component is mounted. Initialization that requires DOM nodes should go here. If you need to load data from a remote endpoint, this is a good place to instantiate the network request.</p>
<p>This method is a good place to set up any subscriptions. If you do that, don’t forget to unsubscribe in <code>componentWillUnmount()</code>.</p>
<p>Calling <code>setState()</code> in this method will trigger an extra rendering, but it will happen before the browser updates the screen. This guarantees that even though the <code>render()</code> will be called twice in this case, the user won’t see the intermediate state. Use this pattern with caution because it often causes performance issues. It can, however, be necessary for cases like modals and tooltips when you need to measure a DOM node before rendering something that depends on its size or position.</p>
<hr />
<h3 id="unsafe_componentwillreceiveprops"><code>UNSAFE_componentWillReceiveProps()</code></h3>
<div>
      <pre><code>UNSAFE_componentWillReceiveProps(nextProps)
</code></pre>
      </div>
<blockquote>

<p>It is recommended that you use the static <a href="#static-getderivedstatefromprops" target="_blank"><code>getDerivedStateFromProps</code></a> lifecycle instead of <code>UNSAFE_componentWillReceiveProps</code>. <a href="/blog/2018/03/29/react-v-16-3.html#component-lifecycle-changes" target="_blank">Learn more about this recommendation here.</a></p>
</blockquote>
<p><code>UNSAFE_componentWillReceiveProps()</code> is invoked before a mounted component receives new props. If you need to update the state in response to prop changes (for example, to reset it), you may compare <code>this.props</code> and <code>nextProps</code> and perform state transitions using <code>this.setState()</code> in this method.</p>
<p>Note that if a parent component causes your component to re-render, this method will be called even if props have not changed. Make sure to compare the current and next values if you only want to handle changes.</p>
<p>React doesn’t call <code>UNSAFE_componentWillReceiveProps()</code> with initial props during <a href="#mounting" target="_blank">mounting</a>. It only calls this method if some of component’s props may update. Calling <code>this.setState()</code> generally doesn’t trigger <code>UNSAFE_componentWillReceiveProps()</code>.</p>
<blockquote>

<p>This lifecycle was previously named <code>componentWillReceiveProps</code>. That name will continue to work until version 17. Use the <a href="https://github.com/reactjs/react-codemod#rename-unsafe-lifecycles" target="_blank"><code>rename-unsafe-lifecycles</code> codemod</a> to automatically update your components.</p>
</blockquote>
<hr />
<h3 id="shouldcomponentupdate"><code>shouldComponentUpdate()</code></h3>
<div>
      <pre><code>shouldComponentUpdate(nextProps, nextState)
</code></pre>
      </div>
<p>Use <code>shouldComponentUpdate()</code> to let React know if a component’s output is not affected by the current change in state or props. The default behavior is to re-render on every state change, and in the vast majority of cases you should rely on the default behavior.</p>
<p><code>shouldComponentUpdate()</code> is invoked before rendering when new props or state are being received. Defaults to <code>true</code>. This method is not called for the initial render or when <code>forceUpdate()</code> is used.</p>
<p>Returning <code>false</code> does not prevent child components from re-rendering when <em>their</em> state changes.</p>
<p>Currently, if <code>shouldComponentUpdate()</code> returns <code>false</code>, then <a href="#componentwillupdate" target="_blank"><code>UNSAFE_componentWillUpdate()</code></a>, <a href="#render" target="_blank"><code>render()</code></a>, and <a href="#componentdidupdate" target="_blank"><code>componentDidUpdate()</code></a> will not be invoked. Note that in the future React may treat <code>shouldComponentUpdate()</code> as a hint rather than a strict directive, and returning <code>false</code> may still result in a re-rendering of the component.</p>
<p>If you determine a specific component is slow after profiling, you may change it to inherit from <a href="/docs/react-api.html#reactpurecomponent" target="_blank"><code>React.PureComponent</code></a> which implements <code>shouldComponentUpdate()</code> with a shallow prop and state comparison. If you are confident you want to write it by hand, you may compare <code>this.props</code> with <code>nextProps</code> and <code>this.state</code> with <code>nextState</code> and return <code>false</code> to tell React the update can be skipped.</p>
<p>We do not recommend doing deep equality checks or using <code>JSON.stringify()</code> in <code>shouldComponentUpdate()</code>. It is very inefficient and will harm performance.</p>
<hr />
<h3 id="unsafe_componentwillupdate"><code>UNSAFE_componentWillUpdate()</code></h3>
<div>
      <pre><code>UNSAFE_componentWillUpdate(nextProps, nextState)
</code></pre>
      </div>
<p><code>UNSAFE_componentWillUpdate()</code> is invoked just before rendering when new props or state are being received. Use this as an opportunity to perform preparation before an update occurs. This method is not called for the initial render.</p>
<p>Note that you cannot call <code>this.setState()</code> here; nor should you do anything else (e.g. dispatch a Redux action) that would trigger an update to a React component before <code>UNSAFE_componentWillUpdate()</code> returns.</p>
<p>If you need to update <code>state</code> in response to <code>props</code> changes, use <a href="#static-getderivedstatefromprops" target="_blank"><code>getDerivedStateFromProps()</code></a> instead.</p>
<blockquote>

<p>This lifecycle was previously named <code>componentWillUpdate</code>. That name will continue to work until version 17. Use the <a href="https://github.com/reactjs/react-codemod#rename-unsafe-lifecycles" target="_blank"><code>rename-unsafe-lifecycles</code> codemod</a> to automatically update your components.</p>
</blockquote>
<blockquote>

<p><code>UNSAFE_componentWillUpdate()</code> will not be invoked if <a href="#shouldcomponentupdate" target="_blank"><code>shouldComponentUpdate()</code></a> returns false.</p>
</blockquote>
<hr />
<h3 id="getsnapshotbeforeupdate"><code>getSnapshotBeforeUpdate()</code></h3>
<p><code>getSnapshotBeforeUpdate()</code> is invoked right before the most recently rendered output is committed to e.g. the DOM. It enables your component to capture current values (e.g. scroll position) before they are potentially changed. Any value returned by this lifecycle will be passed as a parameter to <code>componentDidUpdate()</code>.</p>
<p>For example:</p>
<div>
        <pre><code>class ScrollingList extends React.Component {
  constructor(props) {
    super(props);
    this.listRef = React.createRef();
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    // Are we adding new items to the list?
    // Capture the scroll position so we can adjust scroll later.
    if (prevProps.list.length &lt; this.props.list.length) {
      const list = this.listRef.current;
      return list.scrollHeight - list.scrollTop;
    }
    return null;
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    // If we have a snapshot value, we've just added new items.
    // Adjust scroll so these new items don't push the old ones out of view.
    // (snapshot here is the value returned from getSnapshotBeforeUpdate)
    if (snapshot !== null) {
      const list = this.listRef.current;
      list.scrollTop = list.scrollHeight - snapshot;
    }
  }

  render() {
    return (
      &lt;div ref={this.listRef}&gt;{/* ...contents... */}&lt;/div&gt;
    );
  }
}
</code></pre>
        </div><p>In the above examples, it is important to read the <code>scrollHeight</code> property in <code>getSnapshotBeforeUpdate</code> rather than <code>componentWillUpdate</code> in order to support async rendering. With async rendering, there may be delays between “render” phase lifecycles (like <code>componentWillUpdate</code> and <code>render</code>) and “commit” phase lifecycles (like <code>getSnapshotBeforeUpdate</code> and <code>componentDidUpdate</code>). If a user does something like resize the browser during this time, a <code>scrollHeight</code> value read from <code>componentWillUpdate</code> will be stale.</p>
<hr />
<h3 id="componentdidupdate"><code>componentDidUpdate()</code></h3>
<div>
      <pre><code>componentDidUpdate(prevProps, prevState, snapshot)
</code></pre>
      </div>
<p><code>componentDidUpdate()</code> is invoked immediately after updating occurs. This method is not called for the initial render.</p>
<p>Use this as an opportunity to operate on the DOM when the component has been updated. This is also a good place to do network requests as long as you compare the current props to previous props (e.g. a network request may not be necessary if the props have not changed).</p>
<p>If your component implements the <code>getSnapshotBeforeUpdate()</code> lifecycle, the value it returns will be passed as a third “snapshot” parameter to <code>componentDidUpdate()</code>. (Otherwise this parameter will be undefined.)</p>
<blockquote>

<p><code>componentDidUpdate()</code> will not be invoked if <a href="#shouldcomponentupdate" target="_blank"><code>shouldComponentUpdate()</code></a> returns false.</p>
</blockquote>
<hr />
<h3 id="componentwillunmount"><code>componentWillUnmount()</code></h3>
<div>
      <pre><code>componentWillUnmount()
</code></pre>
      </div>
<p><code>componentWillUnmount()</code> is invoked immediately before a component is unmounted and destroyed. Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that were created in <code>componentDidMount()</code>.</p>
<hr />
<h3 id="componentdidcatch"><code>componentDidCatch()</code></h3>
<div>
      <pre><code>componentDidCatch(error, info)
</code></pre>
      </div>
<p>Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed. Error boundaries catch errors during rendering, in lifecycle methods, and in constructors of the whole tree below them.</p>
<p>A class component becomes an error boundary if it defines this lifecycle method. Calling <code>setState()</code> in it lets you capture an unhandled JavaScript error in the below tree and display a fallback UI. Only use error boundaries for recovering from unexpected exceptions; don’t try to use them for control flow.</p>
<p>For more details, see <a href="/blog/2017/07/26/error-handling-in-react-16.html" target="_blank"><em>Error Handling in React 16</em></a>.</p>
<blockquote>

<p>Error boundaries only catch errors in the components <strong>below</strong> them in the tree. An error boundary can’t catch an error within itself.</p>
</blockquote>
<hr />
<h3 id="setstate"><code>setState()</code></h3>
<div>
      <pre><code>setState(updater[, callback])
</code></pre>
      </div>
<p><code>setState()</code> enqueues changes to the component state and tells React that this component and its children need to be re-rendered with the updated state. This is the primary method you use to update the user interface in response to event handlers and server responses.</p>
<p>Think of <code>setState()</code> as a <em>request</em> rather than an immediate command to update the component. For better perceived performance, React may delay it, and then update several components in a single pass. React does not guarantee that the state changes are applied immediately.</p>
<p><code>setState()</code> does not always immediately update the component. It may batch or defer the update until later. This makes reading <code>this.state</code> right after calling <code>setState()</code> a potential pitfall. Instead, use <code>componentDidUpdate</code> or a <code>setState</code> callback (<code>setState(updater, callback)</code>), either of which are guaranteed to fire after the update has been applied. If you need to set the state based on the previous state, read about the <code>updater</code> argument below.</p>
<p><code>setState()</code> will always lead to a re-render unless <code>shouldComponentUpdate()</code> returns <code>false</code>. If mutable objects are being used and conditional rendering logic cannot be implemented in <code>shouldComponentUpdate()</code>, calling <code>setState()</code> only when the new state differs from the previous state will avoid unnecessary re-renders.</p>
<p>The first argument is an <code>updater</code> function with the signature:</p>
<div>
      <pre><code>(prevState, props) =&gt; stateChange
</code></pre>
      </div>
<p><code>prevState</code> is a reference to the previous state. It should not be directly mutated. Instead, changes should be represented by building a new object based on the input from <code>prevState</code> and <code>props</code>. For instance, suppose we wanted to increment a value in state by <code>props.step</code>:</p>
<div>
      <pre><code>this.setState((prevState, props) =&gt; {
  return {counter: prevState.counter + props.step};
});
</code></pre>
      </div>
<p>Both <code>prevState</code> and <code>props</code> received by the updater function are guaranteed to be up-to-date. The output of the updater is shallowly merged with <code>prevState</code>.</p>
<p>The second parameter to <code>setState()</code> is an optional callback function that will be executed once <code>setState</code> is completed and the component is re-rendered. Generally we recommend using <code>componentDidUpdate()</code> for such logic instead.</p>
<p>You may optionally pass an object as the first argument to <code>setState()</code> instead of a function:</p>
<div>
      <pre><code>setState(stateChange[, callback])
</code></pre>
      </div>
<p>This performs a shallow merge of <code>stateChange</code> into the new state, e.g., to adjust a shopping cart item quantity:</p>
<div>
      <pre><code>this.setState({quantity: 2})
</code></pre>
      </div>
<p>This form of <code>setState()</code> is also asynchronous, and multiple calls during the same cycle may be batched together. For example, if you attempt to increment an item quantity more than once in the same cycle, that will result in the equivalent of:</p>
<div>
      <pre><code>Object.assign(
  previousState,
  {quantity: state.quantity + 1},
  {quantity: state.quantity + 1},
  ...
)
</code></pre>
      </div>
<p>Subsequent calls will override values from previous calls in the same cycle, so the quantity will only be incremented once. If the next state depends on the previous state, we recommend using the updater function form, instead:</p>
<div>
      <pre><code>this.setState((prevState) =&gt; {
  return {quantity: prevState.quantity + 1};
});
</code></pre>
      </div>
<p>For more detail, see:</p>

<hr />
<h3 id="forceupdate"><code>forceUpdate()</code></h3>
<div>
      <pre><code>component.forceUpdate(callback)
</code></pre>
      </div>
<p>By default, when your component’s state or props change, your component will re-render. If your <code>render()</code> method depends on some other data, you can tell React that the component needs re-rendering by calling <code>forceUpdate()</code>.</p>
<p>Calling <code>forceUpdate()</code> will cause <code>render()</code> to be called on the component, skipping <code>shouldComponentUpdate()</code>. This will trigger the normal lifecycle methods for child components, including the <code>shouldComponentUpdate()</code> method of each child. React will still only update the DOM if the markup changes.</p>
<p>Normally you should try to avoid all uses of <code>forceUpdate()</code> and only read from <code>this.props</code> and <code>this.state</code> in <code>render()</code>.</p>
<hr />
<h2 id="class-properties-1">Class Properties</h2>
<h3 id="defaultprops"><code>defaultProps</code></h3>
<p><code>defaultProps</code> can be defined as a property on the component class itself, to set the default props for the class. This is used for undefined props, but not for null props. For example:</p>
<div>
      <pre><code>class CustomButton extends React.Component {
  // ...
}

CustomButton.defaultProps = {
  color: 'blue'
};
</code></pre>
      </div>
<p>If <code>props.color</code> is not provided, it will be set by default to <code>'blue'</code>:</p>
<div>
      <pre><code>  render() {
    return &lt;CustomButton /&gt; ; // props.color will be set to blue
  }
</code></pre>
      </div>
<p>If <code>props.color</code> is set to null, it will remain null:</p>
<div>
      <pre><code>  render() {
    return &lt;CustomButton color={null} /&gt; ; // props.color will remain null
  }
</code></pre>
      </div>
<hr />
<h3 id="displayname"><code>displayName</code></h3>
<p>The <code>displayName</code> string is used in debugging messages. Usually, you don’t need to set it explicitly because it’s inferred from the name of the function or class that defines the component. You might want to set it explicitly if you want to display a different name for debugging purposes or when you create a higher-order component, see <a href="/docs/higher-order-components.html#convention-wrap-the-display-name-for-easy-debugging" target="_blank">Wrap the Display Name for Easy Debugging</a> for details.</p>
<hr />
<h2 id="instance-properties-1">Instance Properties</h2>
<h3 id="props"><code>props</code></h3>
<p><code>this.props</code> contains the props that were defined by the caller of this component. See <a href="/docs/components-and-props.html" target="_blank">Components and Props</a> for an introduction to props.</p>
<p>In particular, <code>this.props.children</code> is a special prop, typically defined by the child tags in the JSX expression rather than in the tag itself.</p>
<h3 id="state"><code>state</code></h3>
<p>The state contains data specific to this component that may change over time. The state is user-defined, and it should be a plain JavaScript object.</p>
<p>If some value isn’t used for rendering or data flow (for example, a timer ID), you don’t have to put it in the state. Such values can be defined as fields on the component instance.</p>
<p>See <a href="/docs/state-and-lifecycle.html" target="_blank">State and Lifecycle</a> for more information about the state.</p>
<p>Never mutate <code>this.state</code> directly, as calling <code>setState()</code> afterwards may replace the mutation you made. Treat <code>this.state</code> as if it were immutable.</p>
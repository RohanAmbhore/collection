<a href="https://reactjs.org/docs/optimizing-performance.html">https://reactjs.org/docs/optimizing-performance.html</a><div id="articleHeader"><h1>Optimizing Performance</h1></div><p>Internally, React uses several clever techniques to minimize the number of costly DOM operations required to update the UI. For many applications, using React will lead to a fast user interface without doing much work to specifically optimize for performance. Nevertheless, there are several ways you can speed up your React application.</p>
<h2 id="use-the-production-build">Use the Production Build</h2>
<p>If you’re benchmarking or experiencing performance problems in your React apps, make sure you’re testing with the minified production build.</p>
<p>By default, React includes many helpful warnings. These warnings are very useful in development. However, they make React larger and slower so you should make sure to use the production version when you deploy the app.</p>
<p>If you aren’t sure whether your build process is set up correctly, you can check it by installing <a href="https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi" target="_blank">React Developer Tools for Chrome</a>. If you visit a site with React in production mode, the icon will have a dark background:</p>

  <a href="/static/devtools-prod-d0f767f80866431ccdec18f200ca58f1-1e9b4.png" target="_blank" class="readableLinkWithLargeImage">
  
  
    
      <div class="readableLargeImageContainer"><img src="/static/devtools-prod-d0f767f80866431ccdec18f200ca58f1-1e9b4.png" alt="React DevTools on a website with production version of React" /></div>
    
  
  
  </a>
    
<p>If you visit a site with React in development mode, the icon will have a red background:</p>

  <a href="/static/devtools-dev-e434ce2f7e64f63e597edf03f4465694-1e9b4.png" target="_blank" class="readableLinkWithLargeImage">
  
  
    
      <div class="readableLargeImageContainer"><img src="/static/devtools-dev-e434ce2f7e64f63e597edf03f4465694-1e9b4.png" alt="React DevTools on a website with development version of React" /></div>
    
  
  
  </a>
    
<p>It is expected that you use the development mode when working on your app, and the production mode when deploying your app to the users.</p>
<p>You can find instructions for building your app for production below.</p>
<h3 id="create-react-app">Create React App</h3>
<p>If your project is built with <a href="https://github.com/facebookincubator/create-react-app" target="_blank">Create React App</a>, run:</p>
<div>
      <pre><code>npm run build</code></pre>
      </div>
<p>This will create a production build of your app in the <code>build/</code> folder of your project.</p>
<p>Remember that this is only necessary before deploying to production. For normal development, use <code>npm start</code>.</p>
<h3 id="single-file-builds">Single-File Builds</h3>
<p>We offer production-ready versions of React and React DOM as single files:</p>
<div>
      <pre><code>&lt;script src="https://unpkg.com/react@16/umd/react.production.min.js"&gt;&lt;/script&gt;
&lt;script src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"&gt;&lt;/script&gt;
</code></pre>
      </div>
<p>Remember that only React files ending with <code>.production.min.js</code> are suitable for production.</p>
<h3 id="brunch">Brunch</h3>
<p>For the most efficient Brunch production build, install the <a href="https://github.com/brunch/uglify-js-brunch" target="_blank"><code>uglify-js-brunch</code></a> plugin:</p>
<div>
      <pre><code># If you use npm
npm install --save-dev uglify-js-brunch

# If you use Yarn
yarn add --dev uglify-js-brunch</code></pre>
      </div>
<p>Then, to create a production build, add the <code>-p</code> flag to the <code>build</code> command:</p>
<div>
      <pre><code>brunch build -p</code></pre>
      </div>
<p>Remember that you only need to do this for production builds. You shouldn’t pass the <code>-p</code> flag or apply this plugin in development, because it will hide useful React warnings and make the builds much slower.</p>
<h3 id="browserify">Browserify</h3>
<p>For the most efficient Browserify production build, install a few plugins:</p>
<div>
      <pre><code># If you use npm
npm install --save-dev envify uglify-js uglifyify 

# If you use Yarn
yarn add --dev envify uglify-js uglifyify </code></pre>
      </div>
<p>To create a production build, make sure that you add these transforms <strong>(the order matters)</strong>:</p>
<ul>
<li>The <a href="https://github.com/hughsk/envify" target="_blank"><code>envify</code></a> transform ensures the right build environment is set. Make it global (<code>-g</code>).</li>
<li>The <a href="https://github.com/hughsk/uglifyify" target="_blank"><code>uglifyify</code></a> transform removes development imports. Make it global too (<code>-g</code>).</li>
<li>Finally, the resulting bundle is piped to <a href="https://github.com/mishoo/UglifyJS2" target="_blank"><code>uglify-js</code></a> for mangling (<a href="https://github.com/hughsk/uglifyify#motivationusage" target="_blank">read why</a>).</li>
</ul>
<p>For example:</p>
<div>
      <pre><code>browserify ./index.js \
  -g [ envify --NODE_ENV production ] \
  -g uglifyify \
  | uglifyjs --compress --mangle &gt; ./bundle.js</code></pre>
      </div>
<blockquote>
<p><strong>Note:</strong></p>
<p>The package name is <code>uglify-js</code>, but the binary it provides is called <code>uglifyjs</code>.<br />
This is not a typo.</p>
</blockquote>
<p>Remember that you only need to do this for production builds. You shouldn’t apply these plugins in development because they will hide useful React warnings, and make the builds much slower.</p>
<h3 id="rollup">Rollup</h3>
<p>For the most efficient Rollup production build, install a few plugins:</p>
<div>
      <pre><code># If you use npm
npm install --save-dev rollup-plugin-commonjs rollup-plugin-replace rollup-plugin-uglify 

# If you use Yarn
yarn add --dev rollup-plugin-commonjs rollup-plugin-replace rollup-plugin-uglify </code></pre>
      </div>
<p>To create a production build, make sure that you add these plugins <strong>(the order matters)</strong>:</p>
<ul>
<li>The <a href="https://github.com/rollup/rollup-plugin-replace" target="_blank"><code>replace</code></a> plugin ensures the right build environment is set.</li>
<li>The <a href="https://github.com/rollup/rollup-plugin-commonjs" target="_blank"><code>commonjs</code></a> plugin provides support for CommonJS in Rollup.</li>
<li>The <a href="https://github.com/TrySound/rollup-plugin-uglify" target="_blank"><code>uglify</code></a> plugin compresses and mangles the final bundle.</li>
</ul>
<div>
      <pre><code>plugins: [
  // ...
  require('rollup-plugin-replace')({
    'process.env.NODE_ENV': JSON.stringify('production')
  }),
  require('rollup-plugin-commonjs')(),
  require('rollup-plugin-uglify')(),
  // ...
]
</code></pre>
      </div>
<p>For a complete setup example <a href="https://gist.github.com/Rich-Harris/cb14f4bc0670c47d00d191565be36bf0" target="_blank">see this gist</a>.</p>
<p>Remember that you only need to do this for production builds. You shouldn’t apply the <code>uglify</code> plugin or the <code>replace</code> plugin with <code>'production'</code> value in development because they will hide useful React warnings, and make the builds much slower.</p>
<h3 id="webpack">webpack</h3>
<blockquote>
<p><strong>Note:</strong></p>
<p>If you’re using Create React App, please follow <a href="#create-react-app" target="_blank">the instructions above</a>.<br />
This section is only relevant if you configure webpack directly.</p>
</blockquote>
<p>For the most efficient webpack production build, make sure to include these plugins in your production configuration:</p>
<div>
      <pre><code>new webpack.DefinePlugin({
  'process.env.NODE_ENV': JSON.stringify('production')
}),
new webpack.optimize.UglifyJsPlugin()
</code></pre>
      </div>
<p>You can learn more about this in <a href="https://webpack.js.org/guides/production-build/" target="_blank">webpack documentation</a>.</p>
<p>Remember that you only need to do this for production builds. You shouldn’t apply <code>UglifyJsPlugin</code> or <code>DefinePlugin</code> with <code>'production'</code> value in development because they will hide useful React warnings, and make the builds much slower.</p>
<h2 id="profiling-components-with-the-chrome-performance-tab">Profiling Components with the Chrome Performance Tab</h2>
<p>In the <strong>development</strong> mode, you can visualize how components mount, update, and unmount, using the performance tools in supported browsers. For example:</p>

  <a href="/static/react-perf-chrome-timeline-64d522b74fb585f1abada9801f85fa9d-dcc89.png" target="_blank" class="readableLinkWithLargeImage">
  
  
    
      <div class="readableLargeImageContainer"><img src="/static/react-perf-chrome-timeline-64d522b74fb585f1abada9801f85fa9d-dcc89.png" alt="React components in Chrome timeline" /></div>
    
  
  
  </a>
    
<p>To do this in Chrome:</p>
<ol>
<li>
<p>Temporarily <strong>disable all Chrome extensions, especially React DevTools</strong>. They can significantly skew the results!</p>
</li>
<li>
<p>Make sure you’re running the application in the development mode.</p>
</li>
<li>
<p>Open the Chrome DevTools <strong><a href="https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/timeline-tool" target="_blank">Performance</a></strong> tab and press <strong>Record</strong>.</p>
</li>
<li>
<p>Perform the actions you want to profile. Don’t record more than 20 seconds or Chrome might hang.</p>
</li>
<li>
<p>Stop recording.</p>
</li>
<li>
<p>React events will be grouped under the <strong>User Timing</strong> label.</p>
</li>
</ol>
<p>For a more detailed walkthrough, check out <a href="https://building.calibreapp.com/debugging-react-performance-with-react-16-and-chrome-devtools-c90698a522ad" target="_blank">this article by Ben Schwarz</a>.</p>
<p>Note that <strong>the numbers are relative so components will render faster in production</strong>. Still, this should help you realize when unrelated UI gets updated by mistake, and how deep and how often your UI updates occur.</p>
<p>Currently Chrome, Edge, and IE are the only browsers supporting this feature, but we use the standard <a href="https://developer.mozilla.org/en-US/docs/Web/API/User_Timing_API" target="_blank">User Timing API</a> so we expect more browsers to add support for it.</p>
<h2 id="virtualize-long-lists">Virtualize Long Lists</h2>
<p>If your application renders long lists of data (hundreds or thousands of rows), we recommended using a technique known as “windowing”. This technique only renders a small subset of your rows at any given time, and can dramatically reduce the time it takes to re-render the components as well as the number of DOM nodes created.</p>
<p><a href="https://bvaughn.github.io/react-virtualized/" target="_blank">React Virtualized</a> is one popular windowing library. It provides several reusable components for displaying lists, grids, and tabular data. You can also create your own windowing component, like <a href="https://medium.com/@paularmstrong/twitter-lite-and-high-performance-react-progressive-web-apps-at-scale-d28a00e780a3" target="_blank">Twitter did</a>, if you want something more tailored to your application’s specific use case.</p>
<h2 id="avoid-reconciliation">Avoid Reconciliation</h2>
<p>React builds and maintains an internal representation of the rendered UI. It includes the React elements you return from your components. This representation lets React avoid creating DOM nodes and accessing existing ones beyond necessity, as that can be slower than operations on JavaScript objects. Sometimes it is referred to as a “virtual DOM”, but it works the same way on React Native.</p>
<p>When a component’s props or state change, React decides whether an actual DOM update is necessary by comparing the newly returned element with the previously rendered one. When they are not equal, React will update the DOM.</p>
<p>You can now visualize these re-renders of the virtual DOM with React DevTools:</p>

<p>In the developer console select the <strong>Highlight Updates</strong> option in the <strong>React</strong> tab:</p>

  <a href="/static/devtools-highlight-updates-97eda4825de476af4515435a0c36ca78-a62e3.png" target="_blank" class="readableLinkWithLargeImage">
  
  
    
      <div class="readableLargeImageContainer"><img src="/static/devtools-highlight-updates-97eda4825de476af4515435a0c36ca78-acf85.png" alt="How to enable highlight updates" /></div>
    
  
  
  </a>
    
<p>Interact with your page and you should see colored borders momentarily appear around any components that have re-rendered. This lets you spot re-renders that were not necessary. You can learn more about this React DevTools feature from this <a href="https://blog.logrocket.com/make-react-fast-again-part-3-highlighting-component-updates-6119e45e6833" target="_blank">blog post</a> from <a href="https://blog.logrocket.com/@edelstein" target="_blank">Ben Edelstein</a>.</p>
<p>Consider this example:</p>
<div class="readableLargeImageContainer"><img src="/highlight-updates-example-7a42123e91b1b460b1a65605d6ff0d2b.gif" alt="React DevTools Highlight Updates example" /></div>
<p>Note that when we’re entering a second todo, the first todo also flashes on the screen on every keystroke. This means it is being re-rendered by React together with the input. This is sometimes called a “wasted” render. We know it is unnecessary because the first todo content has not changed, but React doesn’t know this.</p>
<p>Even though React only updates the changed DOM nodes, re-rendering still takes some time. In many cases it’s not a problem, but if the slowdown is noticeable, you can speed all of this up by overriding the lifecycle function <code>shouldComponentUpdate</code>, which is triggered before the re-rendering process starts. The default implementation of this function returns <code>true</code>, leaving React to perform the update:</p>
<div>
      <pre><code>shouldComponentUpdate(nextProps, nextState) {
  return true;
}
</code></pre>
      </div>
<p>If you know that in some situations your component doesn’t need to update, you can return <code>false</code> from <code>shouldComponentUpdate</code> instead, to skip the whole rendering process, including calling <code>render()</code> on this component and below.</p>
<p>In most cases, instead of writing <code>shouldComponentUpdate()</code> by hand, you can inherit from <a href="/docs/react-api.html#reactpurecomponent" target="_blank"><code>React.PureComponent</code></a>. It is equivalent to implementing <code>shouldComponentUpdate()</code> with a shallow comparison of current and previous props and state.</p>
<h2 id="shouldcomponentupdate-in-action">shouldComponentUpdate In Action</h2>
<p>Here’s a subtree of components. For each one, <code>SCU</code> indicates what <code>shouldComponentUpdate</code> returned, and <code>vDOMEq</code> indicates whether the rendered React elements were equivalent. Finally, the circle’s color indicates whether the component had to be reconciled or not.</p>
<figure>
  <a href="/static/should-component-update-5ee1bdf4779af06072a17b7a0654f6db-9a3ff.png" target="_blank" class="readableLinkWithLargeImage">
  
  
    
      <div class="readableLargeImageContainer"><img src="/static/should-component-update-5ee1bdf4779af06072a17b7a0654f6db-9a3ff.png" alt="should component update" /></div>
    
  
  
  </a>
    </figure>
<p>Since <code>shouldComponentUpdate</code> returned <code>false</code> for the subtree rooted at C2, React did not attempt to render C2, and thus didn’t even have to invoke <code>shouldComponentUpdate</code> on C4 and C5.</p>
<p>For C1 and C3, <code>shouldComponentUpdate</code> returned <code>true</code>, so React had to go down to the leaves and check them. For C6 <code>shouldComponentUpdate</code> returned <code>true</code>, and since the rendered elements weren’t equivalent React had to update the DOM.</p>
<p>The last interesting case is C8. React had to render this component, but since the React elements it returned were equal to the previously rendered ones, it didn’t have to update the DOM.</p>
<p>Note that React only had to do DOM mutations for C6, which was inevitable. For C8, it bailed out by comparing the rendered React elements, and for C2’s subtree and C7, it didn’t even have to compare the elements as we bailed out on <code>shouldComponentUpdate</code>, and <code>render</code> was not called.</p>
<h2 id="examples">Examples</h2>
<p>If the only way your component ever changes is when the <code>props.color</code> or the <code>state.count</code> variable changes, you could have <code>shouldComponentUpdate</code> check that:</p>
<div>
      <pre><code>class CounterButton extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: 1};
  }

  shouldComponentUpdate(nextProps, nextState) {
    if (this.props.color !== nextProps.color) {
      return true;
    }
    if (this.state.count !== nextState.count) {
      return true;
    }
    return false;
  }

  render() {
    return (
      &lt;button
        color={this.props.color}
        onClick={() =&gt; this.setState(state =&gt; ({count: state.count + 1}))}&gt;
        Count: {this.state.count}
      &lt;/button&gt;
    );
  }
}
</code></pre>
      </div>
<p>In this code, <code>shouldComponentUpdate</code> is just checking if there is any change in <code>props.color</code> or <code>state.count</code>. If those values don’t change, the component doesn’t update. If your component got more complex, you could use a similar pattern of doing a “shallow comparison” between all the fields of <code>props</code> and <code>state</code> to determine if the component should update. This pattern is common enough that React provides a helper to use this logic - just inherit from <code>React.PureComponent</code>. So this code is a simpler way to achieve the same thing:</p>
<div>
      <pre><code>class CounterButton extends React.PureComponent {
  constructor(props) {
    super(props);
    this.state = {count: 1};
  }

  render() {
    return (
      &lt;button
        color={this.props.color}
        onClick={() =&gt; this.setState(state =&gt; ({count: state.count + 1}))}&gt;
        Count: {this.state.count}
      &lt;/button&gt;
    );
  }
}
</code></pre>
      </div>
<p>Most of the time, you can use <code>React.PureComponent</code> instead of writing your own <code>shouldComponentUpdate</code>. It only does a shallow comparison, so you can’t use it if the props or state may have been mutated in a way that a shallow comparison would miss.</p>
<p>This can be a problem with more complex data structures. For example, let’s say you want a <code>ListOfWords</code> component to render a comma-separated list of words, with a parent <code>WordAdder</code> component that lets you click a button to add a word to the list. This code does <em>not</em> work correctly:</p>
<div>
      <pre><code>class ListOfWords extends React.PureComponent {
  render() {
    return &lt;div&gt;{this.props.words.join(',')}&lt;/div&gt;;
  }
}

class WordAdder extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      words: ['marklar']
    };
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    // This section is bad style and causes a bug
    const words = this.state.words;
    words.push('marklar');
    this.setState({words: words});
  }

  render() {
    return (
      &lt;div&gt;
        &lt;button onClick={this.handleClick} /&gt;
        &lt;ListOfWords words={this.state.words} /&gt;
      &lt;/div&gt;
    );
  }
}
</code></pre>
      </div>
<p>The problem is that <code>PureComponent</code> will do a simple comparison between the old and new values of <code>this.props.words</code>. Since this code mutates the <code>words</code> array in the <code>handleClick</code> method of <code>WordAdder</code>, the old and new values of <code>this.props.words</code> will compare as equal, even though the actual words in the array have changed. The <code>ListOfWords</code> will thus not update even though it has new words that should be rendered.</p>
<h2 id="the-power-of-not-mutating-data">The Power Of Not Mutating Data</h2>
<p>The simplest way to avoid this problem is to avoid mutating values that you are using as props or state. For example, the <code>handleClick</code> method above could be rewritten using <code>concat</code> as:</p>
<div>
      <pre><code>handleClick() {
  this.setState(prevState =&gt; ({
    words: prevState.words.concat(['marklar'])
  }));
}
</code></pre>
      </div>
<p>ES6 supports a <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator" target="_blank">spread syntax</a> for arrays which can make this easier. If you’re using Create React App, this syntax is available by default.</p>
<div>
      <pre><code>handleClick() {
  this.setState(prevState =&gt; ({
    words: [...prevState.words, 'marklar'],
  }));
};
</code></pre>
      </div>
<p>You can also rewrite code that mutates objects to avoid mutation, in a similar way. For example, let’s say we have an object named <code>colormap</code> and we want to write a function that changes <code>colormap.right</code> to be <code>'blue'</code>. We could write:</p>
<div>
      <pre><code>function updateColorMap(colormap) {
  colormap.right = 'blue';
}
</code></pre>
      </div>
<p>To write this without mutating the original object, we can use <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign" target="_blank">Object.assign</a> method:</p>
<div>
      <pre><code>function updateColorMap(colormap) {
  return Object.assign({}, colormap, {right: 'blue'});
}
</code></pre>
      </div>
<p><code>updateColorMap</code> now returns a new object, rather than mutating the old one. <code>Object.assign</code> is in ES6 and requires a polyfill.</p>
<p>There is a JavaScript proposal to add <a href="https://github.com/sebmarkbage/ecmascript-rest-spread" target="_blank">object spread properties</a> to make it easier to update objects without mutation as well:</p>
<div>
      <pre><code>function updateColorMap(colormap) {
  return {...colormap, right: 'blue'};
}
</code></pre>
      </div>
<p>If you’re using Create React App, both <code>Object.assign</code> and the object spread syntax are available by default.</p>
<h2 id="using-immutable-data-structures">Using Immutable Data Structures</h2>
<p><a href="https://github.com/facebook/immutable-js" target="_blank">Immutable.js</a> is another way to solve this problem. It provides immutable, persistent collections that work via structural sharing:</p>
<ul>
<li><em>Immutable</em>: once created, a collection cannot be altered at another point in time.</li>
<li><em>Persistent</em>: new collections can be created from a previous collection and a mutation such as set. The original collection is still valid after the new collection is created.</li>
<li><em>Structural Sharing</em>: new collections are created using as much of the same structure as the original collection as possible, reducing copying to a minimum to improve performance.</li>
</ul>
<p>Immutability makes tracking changes cheap. A change will always result in a new object so we only need to check if the reference to the object has changed. For example, in this regular JavaScript code:</p>
<div>
      <pre><code>const x = { foo: 'bar' };
const y = x;
y.foo = 'baz';
x === y; // true
</code></pre>
      </div>
<p>Although <code>y</code> was edited, since it’s a reference to the same object as <code>x</code>, this comparison returns <code>true</code>. You can write similar code with immutable.js:</p>
<div>
      <pre><code>const SomeRecord = Immutable.Record({ foo: null });
const x = new SomeRecord({ foo: 'bar' });
const y = x.set('foo', 'baz');
const z = x.set('foo', 'bar');
x === y; // false
x === z; // true
</code></pre>
      </div>
<p>In this case, since a new reference is returned when mutating <code>x</code>, we can use a reference equality check <code>(x === y)</code> to verify that the new value stored in <code>y</code> is different than the original value stored in <code>x</code>.</p>
<p>Two other libraries that can help use immutable data are <a href="https://github.com/rtfeldman/seamless-immutable" target="_blank">seamless-immutable</a> and <a href="https://github.com/kolodny/immutability-helper" target="_blank">immutability-helper</a>.</p>
<p>Immutable data structures provide you with a cheap way to track changes on objects, which is all we need to implement <code>shouldComponentUpdate</code>. This can often provide you with a nice performance boost.</p>
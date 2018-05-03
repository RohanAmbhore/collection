<a href="https://medium.com/the-web-tub/managing-your-react-state-with-redux-affab72de4b1">https://medium.com/the-web-tub/managing-your-react-state-with-redux-affab72de4b1</a><div id="articleHeader"><h1>Managing your React state with Redux</h1></div><figure id="6ef2"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/66/0*95tBOgxEPQAVq9YO.png?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1760/0*95tBOgxEPQAVq9YO.png" /></div></figure><p id="0ea6">In this post we will take a look at using <a href="https://github.com/reactjs/redux" target="_blank">Redux</a> for managing the state in <a href="https://facebook.github.io/react/" target="_blank">React</a> apps. Redux is a very simple library that enables predictable atomic state changes. While the API is tiny and easy to learn, it gives you a lot of power and solves many of the problems when handling the application state and sharing data between components.</p><p id="d02b">The fact that the Redux state changes predictably opens up a lot of debugging possibilities. For example, using <em>time travel</em> makes it possible to travel back and forth between different states instead of having to reload the whole app in order to get back to the same place.</p><p id="95da">To learn how to integrate the Redux DevTools in your app to enable time travel, please take a look at this article:</p><ul><li id="13ad"><a href="https://onsen.io/blog/react-redux-devtools-with-time-travel/" target="_blank">Time Travel in React Redux apps using Redux DevTools</a></li></ul><p id="2c0c">The code for this article is available in <a href="https://github.com/argelius/react-redux-timetravel" target="_blank">this GitHub repo</a>. It’s simple drawing application where the user can toggle cells in a grid by clicking on them.</p><p id="bca7">You can play with it here:</p><p id="a996"><a href="https://argelius.github.io/react-redux-timetravel/%22%3E%3C/iframe" target="_blank">https://argelius.github.io/react-redux-timetravel/</a></p><p id="ef16">The bar on the right is the <a href="https://github.com/gaearon/redux-devtools" target="_blank">Redux DevTools</a> which enables simple debugging inside the app itself. It is also available as an <a href="https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd" target="_blank">extension for Google Chrome</a>. To learn how to integrate the DevTools, please <a href="https://onsen.io/blog/react-redux-devtools-with-time-travel/" target="_blank">click here</a>.</p><p id="1aa1">I have also created a larger example that uses React and Redux with <a href="https://onsen.io/" target="_blank">Onsen UI</a>. It’s a simple weather forecast application. The code for that application can be found <a href="https://github.com/argelius/react-onsenui-redux-weather" target="_blank">here</a> and there is also a <a href="http://argelius.github.io/react-onsenui-redux-weather/demo.html" target="_blank">demo</a> available. We will take a look at how this app is built in a coming blog post.</p><h3 id="5551">What is Redux?</h3><p id="8857">Patrick already wrote a great <a href="https://onsen.io/blog/building-a-calculator-app-with-redux-and-onsenui/" target="_blank">article on Redux</a> so I will keep this short. <a href="https://github.com/reactjs/redux" target="_blank">Redux</a> is a state container for JavaScript apps, often called a Redux <em>store</em>. It stores the whole state of the app in an immutable object tree.</p><p id="e935">To create a store the <code>createStore(reducer, [initialState], [enhancer])</code> function is used to create a new store. It takes three arguments:</p><ul><li id="e97c"><code>reducer</code> - A reducing function. We will describe it below.</li><li id="c761"><code>initialState</code> - The initial state of the store.</li><li id="f01c"><code>enhancer</code> - Can be used to enhance the Redux store and add third-party libraries and middleware for logging, persistant storage, etc.</li></ul><p id="9893">In the app described below we use the <code>redux-logger</code> library to add console logs when the state changes. This is done with the <code>applyMiddleware</code> function:</p><figure id="cbc8"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars3.githubusercontent.com%2Fu%2F3192899%3Fv%3D4%26s%3D400&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><p id="cbd3">The Redux store API is tiny and has only four methods:</p><ul><li id="73ca"><code>store.getState()</code> - Returns the current state object tree.</li><li id="72ae"><code>store.dispatch(action)</code> - Dispatch an action to change the state.</li><li id="1add"><code>store.subscribe(listener)</code> - Listen to changes in the state tree.</li><li id="0263"><code>store.replaceReducer(nextReducer)</code> - Replaces the current reducer with another. This method is used in advanced use cases such as <a href="https://webpack.github.io/docs/code-splitting.html" target="_blank">code splitting</a>.</li></ul><p id="d98c">The state can only be changed by emitting an <em>action</em>. The state tree is never mutated directly instead you use pure functions called <em>reducers</em>. A reducer takes the current state tree and an action as arguments and returns the resulting state tree.</p><p id="f34a">The following is an example of a simple reducer:</p><figure id="4687"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars3.githubusercontent.com%2Fu%2F3192899%3Fv%3D4%26s%3D400&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><p id="989f">I am using the <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Spread_operator" target="_blank">spread operator</a> in the code. This basically makes it possible to copy an array by doing:</p><pre id="0e31"><code>const copy = [...original];</code></pre><p id="bbb9">This is important because we want the reducer to be a <em>pure</em> function that doesn’t mutate the state directly. So instead of pushing a new element to the array we create a brand new array containing all the previous state in addition to the new element.</p><p id="85ce">As seen in the code above, Redux is a very simple library but because it’s deterministic (the current state is only dependent on the previous actions) it makes the behaviour of the app very predictable and less prone to bugs. It also enables time travel which is an efficient way of finding and solving bugs should they occur.</p><p id="39e9">In the example above there is only one reducer with a single action acting on the state tree but adding new actions and combining several reducers is a relatively simple task. Redux scales very well for larger applications given that the code is structured in a good way.</p><h3 id="e049">Redux with React</h3><p id="2169">Redux is in itself not written specifically for React. It can be used with other frameworks such as Angular, Ember or Vue.js. However, Redux was written with React in mind and they work very well together. For a guide on how to use Redux with Angular2, please take a look at <a href="http://blog.scottlogic.com/2016/01/25/angular2-time-travel-with-redux.html" target="_blank">this article</a>.</p><p id="74a7">The easiest way to use Redux with React is the official <a href="https://github.com/reactjs/react-redux" target="_blank">React Redux binding library</a>. With this library it’s easy to bind the Redux state and actions to props.</p><p id="a6c6">I have created a simple drawing application to illustrate how it can be used. The code is available in <a href="https://github.com/argelius/react-redux-timetravel" target="_blank">this repo on GitHub</a>. I have used a project structure where I split reducers and action creators into different directories. This is a common way to structure the code and it’s what used in the official Redux examples. However, there are other options available such as <a href="https://github.com/erikras/ducks-modular-redux" target="_blank">Ducks</a> where the reducers and action creators are bundled together.</p><p id="7218">In this project Webpack is used to create the <code>bundle.js</code> file. The Webpack config is available <a href="https://github.com/argelius/react-redux-timetravel/blob/master/webpack.config.js" target="_blank">here</a>. Webpack is not the only bundler out there, the code below could just as well be bundled using <a href="http://browserify.org/" target="_blank">Browserify</a> or <a href="https://github.com/rollup/rollup" target="_blank">Rollup</a>.</p><p id="545e">Running the example is as easy as doing:</p><pre id="3180"><code>git clone git@github.com:argelius/react-redux-timetravel.git <br />cd react-redux-timetravel <br />npm install <br />npm start # This will start a server at <a href="http://0.0.0.0:9000/" target="_blank">http://0.0.0.0:9000/</a></code></pre><p id="9866">The Redux part of the code is separated into two parts, <em>action creators</em> and <em>reducers</em>. The reducers have already been explained. An action creator is a simple function that returns the object that should be dispatched in order to execute an action. As an example an action creator for the <code>ADD_QUOTE</code> action in the example above can be written like this:</p><figure id="eed8"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars3.githubusercontent.com%2Fu%2F3192899%3Fv%3D4%26s%3D400&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><p id="8b1c">The syntax <code>{text, person}</code> is shorthand for <code>{text: text, person: person}</code> introduced in ES2016.</p><p id="fbf0">To dispatch the action we can now do:</p><pre id="9406"><code>store.dispatch(addQuote('I shook up the world!', 'Muhammad Ali'));</code></pre><p id="9c60">Let’s take a look at the code of <code>index.js</code>, the entry point of the app. It contains a lot of boilerplate code to enable hot reloading of components and to initialize the Redux DevTools. We will discuss the DevTools in the next blog post so I will not go into the details.</p><p id="e886">The important part is the <code>Provider</code> component which makes the Redux store available to all its descendants. Without this component you would have to pass the store as a prop to all the components that need it.</p><p id="c30a">I have put some comments to clarify what the code does.</p><figure id="ca0c"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars3.githubusercontent.com%2Fu%2F3192899%3Fv%3D4%26s%3D400&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><h3 id="aa02">Action creators</h3><p id="75f1">An action creator is a function that returns an object representing an action that can be dispatched to the Redux store. In this app we have two actions:</p><ul><li id="f05f"><code>SET_GRID_SIZE</code> - Change the size of the grid.</li><li id="c32b"><code>TOGGLE_CELL</code> - Toggle if a cell is filled or not.</li></ul><figure id="ae2e"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars3.githubusercontent.com%2Fu%2F3192899%3Fv%3D4%26s%3D400&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><p id="3970">These objects become arguments to the reducer when dispatched.</p><h3 id="07b0">Reducers</h3><p id="14e6">This app only has one reducer, called <code>grid</code>. The state has the following form:</p><pre id="136e">{<br />    width: 10,<br />    height: 10,<br />    cells: [1, 0, 1, 1, ...]<br />}</pre><p id="0ac3">The <code>width</code> and <code>height</code> parameters are self-explanatory. The <code>cells</code> array is a list of 1s and 0s that represent if a cell is filled or not.</p><p id="7232">The implementation is pretty straightforward. However, when changing the size of the grid we need to be careful so the previous picture is copied correctly onto the new grid since the dimensions changes.</p><p id="83d1">As mentioned before, the reducer should be a pure function which means that we need to copy the cell array before returning the next state.</p><figure id="d251"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars3.githubusercontent.com%2Fu%2F3192899%3Fv%3D4%26s%3D400&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><h3 id="0c9b">Components and containers</h3><p id="3545">In apps using React Redux the components are often separated into two categories, <em>components</em> and <em>containers</em>. This is to distinguish components that use the state tree and dispatch actions from <em>dumb</em> components that are only used for presentation.</p><p id="ce94">This app has three <em>dumb</em> components:</p><ul><li id="1216"><code>App</code> - The root of the app.</li><li id="3a4d"><code>Row</code> - A row in the grid.</li><li id="7ca8"><code>Cell</code> - A grid cell.</li></ul><p id="1e03">Since these components are only used for presentation the implementation is pretty simple. This is one of the strengths of Redux, by separating the state from the graphical presentation we can make tiny reusable components.</p><p id="5a6e">The app also has two containers (actually three but we will discuss the <code>DevTools</code> container in the next blog post).</p><p id="7eba">The two containers are:</p><ul><li id="643b"><code>Grid</code> - Renders a grid of <code>Row</code> and <code>Cell</code> components based on the state and dispatches actions when the cells are clicked.</li><li id="c9ee"><code>SetSize</code> - Renders two input elements that can be used to changed the size of the grid.</li></ul><h4 id="bb22">App component</h4><p id="62c1">The <code>App</code> component just renders two child components: <code>Grid</code> which is the clickable grid and <code>SetSize</code> which is used to set the size of the grid.</p><figure id="7eee"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars3.githubusercontent.com%2Fu%2F3192899%3Fv%3D4%26s%3D400&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><h4 id="f2ea">Row component</h4><p id="2e6f">The <code>Row</code> component is very simple and basically just contains the flexbox layout to make the cells align horizontally and stop them from wrapping.</p><figure id="4d8a"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars3.githubusercontent.com%2Fu%2F3192899%3Fv%3D4%26s%3D400&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><h4 id="4e67">Cell component</h4><p id="e8bd">The <code>Cell</code> component is a clickable cell and it has a black or white background based on the value of the <code>filled</code> prop.</p><figure id="ed85"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars3.githubusercontent.com%2Fu%2F3192899%3Fv%3D4%26s%3D400&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><h3 id="7ed7">Connecting components to Redux</h3><p id="8ebb">We will now take a look at the containers but first we need to understand the <code>connect()</code> method of the Redux React library.</p><p id="abc8">The <code>connect()</code> method takes two arguments: <code>mapStateToProps</code> and <code>mapDispatchToProps</code> and returns a function that can be used to connect the Redux store with a component.</p><p id="e150">Let’s take a look at how this can work with an example:</p><figure id="84b3"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars3.githubusercontent.com%2Fu%2F3192899%3Fv%3D4%26s%3D400&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><h4 id="7c94">Grid container</h4><p id="1eed">Given this we can now take a look at the <code>Grid</code> container and understand how it works. To render the grid it loops through all the cells and renders them either black or white depending on the state:</p><figure id="c3e9"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars3.githubusercontent.com%2Fu%2F3192899%3Fv%3D4%26s%3D400&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><h4 id="bc13">SetSize container</h4><figure id="5ae0"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars3.githubusercontent.com%2Fu%2F3192899%3Fv%3D4%26s%3D400&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><h3 id="721d">Conclusion</h3><p id="c657">Redux is a great library for managing the state of React apps. Storing the whole state in a single tree is very useful since it avoids having multiple sources of truth.</p><p id="091e">In the coming days we will release a couple of blog posts about the Redux DevTools and a tutorial on how to create a more complex app using React Redux and Onsen UI. You can check out the app <a href="http://argelius.github.io/react-onsenui-redux-weather/demo.html" target="_blank">here</a>.</p><p id="468a">We hope the article has been interesting and if you have any questions don’t hesitate to ask in the comments below. If you are a hybrid app developer or thinking about getting into mobile app development, please check out our <a href="https://github.com/OnsenUI/OnsenUI" target="_blank">Onsen UI</a> library and give us a star if you like it. :)</p>
<a href="https://www.valentinog.com/blog/react-redux-tutorial-beginners/">https://www.valentinog.com/blog/react-redux-tutorial-beginners/</a><div id="articleHeader"><h1>React Redux Tutorial for Beginners: learning Redux in 2018</h1></div>

	
	
		<p><em>The simplest <strong>React Redux tutorial</strong> I wish I had when I started learning (updated to webpack4!)</em></p>
<p><div class="readableLargeImageContainer"><img src="https://www.valentinog.com/blog/wp-content/uploads/2017/12/redux-react-tutorial-beginner-2018.png"   alt="The Redux logo - React Redux tutorial" /></div></p>
<p>When I first started learning <strong>Redux</strong> I wish I could find the simplest tutorial ever.</p>
<p>Despite the great resources out there I couldn’t wrap my head around some of the Redux concepts.</p>
<p>I knew what’s the <strong>state</strong>. But <strong>actions</strong>, <strong>action creators, and</strong> <strong>reducers? </strong>Theywere obscure for me.</p>
<p>Last but not least I didn’t know how to glue <strong>React and Redux together</strong>.</p>
<p>During those days I started writing my own React Redux tutorial and since then I learned a lot.</p>
<p>I taught myself the Redux fundamentals by writing this guide. I hope it’ll be useful for all those learning React and Redux.</p>
<p>Enjoy the reading!</p>

<h2>React Redux tutorial: who this guide is for</h2>
<p>The following React Redux guide is exactly what you’re looking for if:</p>
<ul>
<li>you have a good grasp of Javascript, ES6, and React</li>
<li>you’re looking forward to learn Redux in the most simple way</li>
</ul>
<h2>React Redux tutorial: what you will learn</h2>
<p>In the following guide you will learn:</p>
<ol>
<li>what is Redux</li>
<li>how to use Redux with React</li>
</ol>
<h2>React Redux tutorial: a minimal React development environment</h2>
<p>To follow along with the guide you should have a good grasp of <strong>Javascript</strong>, <strong>ES6</strong>, and <strong>React</strong>.</p>
<p>Also, create a <strong>minimal React development environment</strong> before starting off.</p>
<p>Feel free to use <strong>webpack</strong> or <strong>Parcel.</strong></p>
<p>To get started with <strong>webpack</strong>clone my Github repo:</p>
<pre>git clone git@github.com:valentinogagliardi/webpack-4-quickstart.git</pre><div><ol><li>git clone git@github.com:valentinogagliardi/webpack-4-quickstart.git</li></ol><pre>git clone git@github.com:valentinogagliardi/webpack-4-quickstart.git</pre></div>
<p>Remove the file <code>./src/App.js</code>./src/App.jsfrom the repo before moving forward.</p>
<h2>React Redux tutorial: what is the state?</h2>
<p>To <strong>understand what is <a href="https://redux.js.org/" target="_blank">Redux</a></strong> you must first understand what is the <strong>state</strong>.</p>
<p>If you have ever worked with React the term state should be no surprise to you.</p>
<p>I guess you already wrote <strong>stateful React components</strong> like the following:</p>
<pre>import React, { Component } from "react";

class ExampleComponent extends Component {
  constructor() {
    super();

    this.state = {
      articles: [
        { title: "React Redux Tutorial for Beginners", id: 1 },
        { title: "Redux e React: cos'è Redux e come usarlo con React", id: 2 }
      ]
    };
  }

  render() {
    const { articles } = this.state;
    return &lt;ul&gt;{articles.map(el =&gt; &lt;li key={el.id}&gt;{el.title}&lt;/li&gt;)}&lt;/ul&gt;;
  }
}</pre><div><ol><li>import React, { Component } from "react";</li><li>class ExampleComponent extends Component {</li><li>  constructor() {</li><li>    super();</li><li>    this.state = {</li><li>      articles: [</li><li>        { title: "React Redux Tutorial for Beginners", id: 1 },</li><li>        { title: "Redux e React: cos'è Redux e come usarlo con React", id: 2 }</li><li>  render() {</li><li>    const { articles } = this.state;</li><li>    return &lt;ul&gt;{articles.map(el =&gt; &lt;li key={el.id}&gt;{el.title}&lt;/li&gt;)}&lt;/ul&gt;;</li></ol><pre>import React, { Component } from "react";

class ExampleComponent extends Component {
  constructor() {
    super();

    this.state = {
      articles: [
        { title: "React Redux Tutorial for Beginners", id: 1 },
        { title: "Redux e React: cos'è Redux e come usarlo con React", id: 2 }
      ]
    };
  }

  render() {
    const { articles } = this.state;
    return &lt;ul&gt;{articles.map(el =&gt; &lt;li key={el.id}&gt;{el.title}&lt;/li&gt;)}&lt;/ul&gt;;
  }
}</pre></div>
<p>A <strong>stateful React component</strong> is basically a <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes" target="_blank">Javascript ES6 class</a>.</p>
<p>Every stateful React component <strong>carries its own state</strong>. In a React component the state holds up <strong>data</strong>.</p>
<p>The component might render such data to the user.</p>
<p>And there’s <a href="https://reactjs.org/docs/react-component.html#setstate" target="_blank">setState</a> for updating the local state of a component.</p>
<p>Everybody learned React this way:</p>
<ul>
<li>render some data from the <strong>local state</strong></li>
<li>update the state with React setState</li>
</ul>
<h2>React Redux tutorial: what problem does Redux solve?</h2>
<p>Now, it is fine to keep the state within a React component as long as the application remains <strong>small</strong>.</p>
<p>But things could become tricky in more complex scenarios.</p>
<p>You will end up with a bloated component filled with methods for managing and updating the state. The <strong>frontend shouldn’t know about the business logic</strong>.</p>
<p>Fine.</p>
<p>So what are the alternatives for managing the state of a React component? <strong>Redux</strong> is one of them.</p>
<p><strong>Redux solves a problem that might not be clear in the beginning</strong>: it helps giving <strong>each React component</strong> the <strong>exact piece of state</strong> it needs.</p>
<p>Redux holds up the <strong>state</strong> within a <strong>single location</strong>.</p>
<p>Also with Redux the <strong>logic for fetching and managing the state</strong> lives <strong>outside React</strong>.</p>
<p>The benefits of this approach might be not so evident. Things will look clear as soon as you’ll get your feet wet with Redux.</p>
<p>In the next section we’ll see why you should learn Redux and when to use Redux within your applications.</p>
<h2>React Redux tutorial: should I learn Redux?</h2>
<p>Are you trying to learn Redux but you’re going nowhere?</p>
<p>Redux literally scares most beginners. But that shouldn’t be your case.</p>
<p><strong>Redux is not that hard</strong>. The key is: don’t rush learning Redux just because everybody is using it.</p>
<p>You should <strong>start learning Redux</strong> if you’re <strong>motivated and passionate</strong> about it.</p>
<p>Take your time.</p>
<p>I started to learn Redux because:</p>
<ul>
<li>I was 100% interested in learning how Redux works</li>
<li>I was eager to improve my React skills</li>
<li>the combination React/Redux is ubiquitous</li>
<li>Redux is <strong>framework agnostic</strong>. Learn it once, use it everywhere (Vue JS, Angular)</li>
</ul>
<h2>React Redux tutorial: should I use Redux?</h2>
<p>It is feasible to build complex React application without even touching Redux. That comes at a cost.</p>
<p>Redux has a cost as well: it adds another layer of abstraction. But I prefer thinking about <strong>Redux as an investment</strong>, not as a cost.</p>
<p>Another common question for Redux beginners is: how do you know <strong>when you’re ready to use Redux</strong>?</p>
<p>If you think about it there is no rule of thumb for determining when you do need <strong>Redux for managing the state</strong>.</p>
<p>What I found is that you should <strong>consider using Redux</strong> when:</p>
<ul>
<li>multiple React components needs to access the same state but do not have any parent/child relationship</li>
<li>you start to feel awkward passing down the state to multiple components with props</li>
</ul>
<p>If that makes still no sense for you do not worry, I felt the same.</p>
<p>Dan Abramov says “Flux libraries are like glasses: you’ll know when you need them.”</p>
<p>And in fact it worked like that for me.</p>
<p>Dan Abramov has a nice write-up that will help you <a href="https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367" target="_blank">understand if your application needs Redux</a></p>
<p>There’s also an interesting thread on dev.to with Dan explaining <a href="https://dev.to/dan_abramov/react-beginner-question-thread--1i5e/comments/1n21" target="_blank">when is it time to stop managing state at the component level and switching to Redux</a></p>
<figure id="attachment_867"><div class="readableLargeImageContainer"><img src="https://www.valentinog.com/blog/wp-content/uploads/2017/12/dan_abramov.jpg"   alt="Whatever Dan Abramov says to do" /></div><figcaption>Courtesy of dev.to</figcaption></figure>
<p>Make sure to take a look at <a href="http://blog.isquaredsoftware.com/2017/12/blogged-answers-learn-redux/" target="_blank">Resources for learning Redux</a> by Mark Erikson.</p>
<p>Oh by the way, Mark’s blog is a treasure trove of <a href="http://blog.isquaredsoftware.com/" target="_blank">Redux best practices</a>.</p>
<p>Dave Ceddia shares its insight as well in <a href="https://daveceddia.com/what-does-redux-do/" target="_blank">What Does Redux Do? (and when should you use it?.</a></p>
<p>Before going further take your time to understand what problem does Redux solve and whether you’re motivated or not to learn it.</p>
<p>Be aware that Redux is not useful for smaller apps. It really shines in bigger ones. Anyway, learning Redux even if you’re not involved in something big wouldn’t harm anyone.</p>
<p>In the next section we’ll start building a proof of concept to introduce:</p>
<ul>
<li>the <strong>Redux fundamental principles</strong></li>
<li>Redux alongside with React</li>
</ul>
<h2>React Redux tutorial: getting to know the Redux store</h2>
<p>Actions. Reducers. I kind of knew about them. But one thing wasn’t clear to me: <strong>how were all the moving parts glued together</strong>?</p>
<p>Were there some <strong>minions</strong> or what?</p>
<p><div class="readableLargeImageContainer"><img src="https://www.valentinog.com/blog/wp-content/uploads/2017/12/react-redux-tutorial-redux-store.jpg"   alt="React Redux tutorial. There are no minions in Redux" /></div></p>
<p>In Redux there are no minions (unfortunately).</p>
<p>The <strong>store orchestrates all the moving parts in Redux</strong>. Repeat with me: <strong>the store</strong>. The store in Redux is like the human brain: it’s kind of magic.</p>
<p>The <strong>Redux store is fundamental</strong>: the <strong>state of the whole application</strong> lives <strong>inside the store</strong>.</p>
<p>If you think about it Redux works the same as the human brain does. Everybody has memories (the state). And those memories live within your brain (the store).</p>
<p>So to start playing with Redux we should <strong>create a store for wrapping up the state</strong>.</p>
<p>Move into your React development environment and install Redux:</p>
<pre>cd webpack-4-quickstart/</pre><div><ol><li>cd webpack-4-quickstart/</li></ol><pre>cd webpack-4-quickstart/</pre></div>
<pre>npm i redux --save-dev</pre><div><ol><li>npm i redux --save-dev</li></ol><pre>npm i redux --save-dev</pre></div>
<p>Create a directory for the store:</p>
<pre>mkdir -p src/js/store</pre><div><ol><li>mkdir -p src/js/store</li></ol><pre>mkdir -p src/js/store</pre></div>
<p>Create a new file named <code>index.js</code>index.jsin <code>src/js/store</code>src/js/storeand finally initialize the store:</p>
<pre>// src/js/store/index.js

import { createStore } from "redux";
import rootReducer from "../reducers/index";

const store = createStore(rootReducer);

export default store;</pre><div><ol><li>// src/js/store/index.js</li><li>import { createStore } from "redux";</li><li>import rootReducer from "../reducers/index";</li><li>const store = createStore(rootReducer);</li><li>export default store;</li></ol><pre>// src/js/store/index.js

import { createStore } from "redux";
import rootReducer from "../reducers/index";

const store = createStore(rootReducer);

export default store;</pre></div>
<p>createStore is the function for creating the Redux store.</p>
<p>createStore takes a reducer as the first argument, rootReducer in our case.</p>
<p>You may also pass an initial state to createStore. But most of the times you don’t have to. Passing an initial state is useful for server side rendering. Anyway, <strong>the state comes from reducers</strong>.</p>
<p><em><strong>NOTE</strong>: see <a href="https://stackoverflow.com/questions/36619093/why-do-i-get-reducer-returned-undefined-during-initialization-despite-pr" target="_blank">Reducer returned undefined during initialization</a></em></p>
<p>What matters now is understanding what does a reducer do.</p>
<p>In Redux <strong>reducers produce the state</strong>. The state is not something you create by hand.</p>
<p>Armed with that knowledge let’s move on to our first Redux reducer.</p>
<h2>React Redux tutorial: getting to know Redux reducers</h2>
<p>While an initial state is useful for <a href="https://redux.js.org/docs/recipes/ServerRendering.html" target="_blank">SSR</a>, in Redux <strong>the state must return entirely from reducers</strong>.</p>
<p>Cool but what’s a reducer?</p>
<p><div class="readableLargeImageContainer"><img src="https://www.valentinog.com/blog/wp-content/uploads/2017/12/redux-logo.png"   alt="Redux Logo" /></div></p>
<p><strong>A reducer is just a Javascript function</strong>. A reducer <strong>takes two parameters</strong>: <strong>the current state</strong> and an <strong>action</strong> (more about actions soon).</p>
<p>The third principle of Redux says that the state is immutable and cannot change in place.</p>
<p>This is why the reducer must be pure. A pure function is one that returns the exact same output for the given input.</p>
<p>In plain React the local state changes in place with setState. In Redux you cannot do that.</p>
<p>Creating a reducer is not that hard. It’s a plain Javascript function with two parameters.</p>
<p>In our example we’ll be creating a <strong>simple reducer taking the initial state</strong> as the first parameter. As a <strong>second parameter</strong> we’ll provide <strong>action</strong>. As of now the reducer will do nothing than returning the initial state.</p>
<p>Create a directory for the root reducer:</p>
<pre>mkdir -p src/js/reducers</pre><div><ol><li>mkdir -p src/js/reducers</li></ol><pre>mkdir -p src/js/reducers</pre></div>
<p>Then create a new file named <code>index.js</code>index.jsin the <code>src/js/reducers</code>src/js/reducers:</p>
<pre>// src/js/reducers/index.js

const initialState = {
  articles: []
};

const rootReducer = (state = initialState, action) =&gt; state;

export default rootReducer;</pre><div><ol><li>// src/js/reducers/index.js</li><li>const initialState = {</li><li>  articles: []</li><li>const rootReducer = (state = initialState, action) =&gt; state;</li><li>export default rootReducer;</li></ol><pre>// src/js/reducers/index.js

const initialState = {
  articles: []
};

const rootReducer = (state = initialState, action) =&gt; state;

export default rootReducer;</pre></div>
<p>I promised to keep this guide as simple as possibile. That’s why our first reducer is a silly one: it returns the initial state without doing anything else.</p>
<p>Notice how the initial state is passed as a <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters" target="_blank">default parameter</a>.</p>
<p>In the next section we’ll add an action to the mix. That’s where things will become interesting.</p>
<h2>React Redux tutorial: getting to know Redux actions</h2>
<p>Redux reducers are without doubt the most important concept in Redux. <strong>Reducers produce the state of the application</strong>.</p>
<p>But <strong>how does a reducer know when to produce the next state</strong>?</p>
<p>The second principle of Redux says the <strong>only way to change the state is by sending a signal to the store</strong>.This signal is an <strong>action</strong>. “<strong>D</strong><strong>ispatching an action</strong>” is the process of sending out a signal.</p>
<p>Now, how do you change an immutable state? You won’t. The resulting state is a copy of the current state plus the new data.</p>
<p>That’s a lot to know.</p>
<p>The reassuring thing is that <strong>Redux actions are nothing more than Javascript objects</strong>. This is what an action looks like:</p>
<pre>{
  type: 'ADD_ARTICLE',
  payload: { name: 'React Redux Tutorial', id: 1 }
}</pre><div><ol><li>  type: 'ADD_ARTICLE',</li><li>  payload: { name: 'React Redux Tutorial', id: 1 }</li></ol><pre>{
  type: 'ADD_ARTICLE',
  payload: { name: 'React Redux Tutorial', id: 1 }
}</pre></div>
<p>Every action needs a type property for describing how the state should change.</p>
<p>You can specify a payload as well. In the above example the payload is a new article. A reducer will add the article to the current state later.</p>
<p>It is a best pratice to <strong>wrap every action within a function</strong>. Such function is an <strong>action creator</strong>.</p>
<p>Let’s put everything together by creating a simple Redux action.</p>
<p>Create a directory for the actions:</p>
<pre>mkdir -p src/js/actions</pre><div><ol><li>mkdir -p src/js/actions</li></ol><pre>mkdir -p src/js/actions</pre></div>
<p>Then create a new file named <code>index.js</code>index.jsin <code>src/js/actions</code>src/js/actions:</p>
<pre>// src/js/actions/index.js

export const addArticle = article =&gt; ({ type: "ADD_ARTICLE", payload: article });</pre><div><ol><li>// src/js/actions/index.js</li><li>export const addArticle = article =&gt; ({ type: "ADD_ARTICLE", payload: article });</li></ol><pre>// src/js/actions/index.js

export const addArticle = article =&gt; ({ type: "ADD_ARTICLE", payload: article });</pre></div>
<p>So, the <strong>type property</strong> is nothing more than a string.</p>
<p>The reducer will use that string to determine how to calculate the next state.</p>
<p>Since strings are prone to typos and duplicates it’s <strong>better to have action types declared as constants</strong>.</p>
<p>This approach helps <strong>avoiding errors that will be difficult to debug</strong>.</p>
<p>Create a new directory:</p>
<pre>mkdir -p src/js/constants</pre><div><ol><li>mkdir -p src/js/constants</li></ol><pre>mkdir -p src/js/constants</pre></div>
<p>Then create a new file named <code>action-types.js</code>action-types.jsinto the <code>src/js/constants</code>src/js/constants:</p>
<pre>// src/js/constants/action-types.js

export const ADD_ARTICLE = "ADD_ARTICLE";</pre><div><ol><li>// src/js/constants/action-types.js</li><li>export const ADD_ARTICLE = "ADD_ARTICLE";</li></ol><pre>// src/js/constants/action-types.js

export const ADD_ARTICLE = "ADD_ARTICLE";</pre></div>
<p>Now open up again <code>src/js/actions/index.js</code>src/js/actions/index.jsand update the action to use action types:</p>
<pre>// src/js/actions/index.js

import { ADD_ARTICLE } from "../constants/action-types";

export const addArticle = article =&gt; ({ type: ADD_ARTICLE, payload: article });</pre><div><ol><li>// src/js/actions/index.js</li><li>import { ADD_ARTICLE } from "../constants/action-types";</li><li>export const addArticle = article =&gt; ({ type: ADD_ARTICLE, payload: article });</li></ol><pre>// src/js/actions/index.js

import { ADD_ARTICLE } from "../constants/action-types";

export const addArticle = article =&gt; ({ type: ADD_ARTICLE, payload: article });</pre></div>
<p>We’re one step closer to have a working Redux application. Let’s refactor our reducer!</p>
<h2>React Redux tutorial: refactoring the reducer</h2>
<p>Before moving forward let’s recap the main Redux concepts:</p>
<ul>
<li>the <strong>Redux store</strong> is like a brain: it’s in charge for <strong>orchestrating all the moving parts</strong> in Redux</li>
<li>the <strong>state of the application lives as a single, immutable object</strong> within the store</li>
<li>as soon as <strong>the store receives an action it triggers a reducer</strong></li>
<li>the <strong>reducer returns the next state</strong></li>
</ul>
<p>What’s a <strong>Redux reducer</strong> made of?</p>
<p>A reducer is a Javascript function taking <strong>two parameters</strong>: the <strong>state</strong> and the <strong>action</strong>.</p>
<p>A reducer function has a <strong>switch statement</strong> (although unwieldy, a naive reducer could also use if/else).</p>
<p>The <strong>reducer calculates the next state depending on the action type</strong>. Moreover, <strong>it should return at least the initial state when no action type matches</strong>.</p>
<p>When the action type matches a case clause the <strong>reducer calculates the next state</strong> and <strong>returns a new object</strong>. Here’s an excerpt of the code:</p>
<pre>// ...
  switch (action.type) {
    case ADD_ARTICLE:
      return { ...state, articles: [...state.articles, action.payload] };
    default:
      return state;
  }
// ...</pre><div><ol><li>// ...</li><li>  switch (action.type) {</li><li>    case ADD_ARTICLE:</li><li>      return { ...state, articles: [...state.articles, action.payload] };</li><li>    default:</li><li>      return state;</li><li>// ...</li></ol><pre>// ...
  switch (action.type) {
    case ADD_ARTICLE:
      return { ...state, articles: [...state.articles, action.payload] };
    default:
      return state;
  }
// ...</pre></div>
<p>The reducer we created in the previous section does nothing than returning the initial state. Let’s fix that.</p>
<p>Open up <code>src/js/reducers/index.js</code>src/js/reducers/index.jsand update the reducer as follow:</p>
<pre>import { ADD_ARTICLE } from "../constants/action-types";

const initialState = {
  articles: []
};

const rootReducer = (state = initialState, action) =&gt; {
  switch (action.type) {
    case ADD_ARTICLE:
      state.articles.push(action.payload);
      return state;
    default:
      return state;
  }
};

export default rootReducer;</pre><div><ol><li>import { ADD_ARTICLE } from "../constants/action-types";</li><li>const initialState = {</li><li>  articles: []</li><li>const rootReducer = (state = initialState, action) =&gt; {</li><li>  switch (action.type) {</li><li>    case ADD_ARTICLE:</li><li>      state.articles.push(action.payload);</li><li>      return state;</li><li>    default:</li><li>      return state;</li><li>export default rootReducer;</li></ol><pre>import { ADD_ARTICLE } from "../constants/action-types";

const initialState = {
  articles: []
};

const rootReducer = (state = initialState, action) =&gt; {
  switch (action.type) {
    case ADD_ARTICLE:
      state.articles.push(action.payload);
      return state;
    default:
      return state;
  }
};

export default rootReducer;</pre></div>
<p>What do you see here?</p>
<p>Although it’s valid code the <strong>above reducer breaks</strong> the main Redux principle: <strong>immutability</strong>.</p>
<p><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push" target="_blank">Array.prototype.push</a> is an impure function: it alters the original array.</p>
<p>Making our reducer compliant is easy. Using <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat" target="_blank">Array.prototype.concat</a> in place of Array.prototype.push is enough to keep the initial array immutable:</p>
<pre>import { ADD_ARTICLE } from "../constants/action-types";

const initialState = {
  articles: []
};

const rootReducer = (state = initialState, action) =&gt; {
  switch (action.type) {
    case ADD_ARTICLE:
      return { ...state, articles: state.articles.concat(action.payload) };
    default:
      return state;
  }
};

export default rootReducer;</pre><div><ol><li>import { ADD_ARTICLE } from "../constants/action-types";</li><li>const initialState = {</li><li>  articles: []</li><li>const rootReducer = (state = initialState, action) =&gt; {</li><li>  switch (action.type) {</li><li>    case ADD_ARTICLE:</li><li>      return { ...state, articles: state.articles.concat(action.payload) };</li><li>    default:</li><li>      return state;</li><li>export default rootReducer;</li></ol><pre>import { ADD_ARTICLE } from "../constants/action-types";

const initialState = {
  articles: []
};

const rootReducer = (state = initialState, action) =&gt; {
  switch (action.type) {
    case ADD_ARTICLE:
      return { ...state, articles: state.articles.concat(action.payload) };
    default:
      return state;
  }
};

export default rootReducer;</pre></div>
<p>We’re not done yet! With the <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator" target="_blank">spread operator</a> we can make our reducer even better:</p>
<pre>import { ADD_ARTICLE } from "../constants/action-types";

const initialState = {
  articles: []
};

const rootReducer = (state = initialState, action) =&gt; {
  switch (action.type) {
    case ADD_ARTICLE:
      return { ...state, articles: [...state.articles, action.payload] };
    default:
      return state;
  }
};

export default rootReducer;</pre><div><ol><li>import { ADD_ARTICLE } from "../constants/action-types";</li><li>const initialState = {</li><li>  articles: []</li><li>const rootReducer = (state = initialState, action) =&gt; {</li><li>  switch (action.type) {</li><li>    case ADD_ARTICLE:</li><li>      return { ...state, articles: [...state.articles, action.payload] };</li><li>    default:</li><li>      return state;</li><li>export default rootReducer;</li></ol><pre>import { ADD_ARTICLE } from "../constants/action-types";

const initialState = {
  articles: []
};

const rootReducer = (state = initialState, action) =&gt; {
  switch (action.type) {
    case ADD_ARTICLE:
      return { ...state, articles: [...state.articles, action.payload] };
    default:
      return state;
  }
};

export default rootReducer;</pre></div>
<p>In the example above the initial state is left utterly untouched.</p>
<p>The initial articles array doesn’t change in place.</p>
<p>The initial state object doesn’t change as well. The resulting state is a copy of the initial state.</p>
<p>There are two key points for <strong>avoiding mutations in Redux</strong>:</p>

<p>The <strong>object spread operator</strong> is still in stage 3. Install <a href="https://babeljs.io/docs/plugins/transform-object-rest-spread/" target="_blank">Object rest spread transform</a> to <strong>avoid a SyntaxError Unexpected token</strong> when using the object spread operator in Babel:</p>
<pre>npm i --save-dev babel-plugin-transform-object-rest-spread</pre><div><ol><li>npm i --save-dev babel-plugin-transform-object-rest-spread</li></ol><pre>npm i --save-dev babel-plugin-transform-object-rest-spread</pre></div>
<p>Open up <code>.babelrc</code>.babelrcand update the configuration:</p>
<pre>{
    "presets": ["env", "react"],
    "plugins": ["transform-object-rest-spread"]
}</pre><div><ol><li>    "presets": ["env", "react"],</li><li>    "plugins": ["transform-object-rest-spread"]</li></ol><pre>{
    "presets": ["env", "react"],
    "plugins": ["transform-object-rest-spread"]
}</pre></div>
<p><strong>Redux protip</strong>: the reducer will grow as your app will become bigger. You can split a big reducer into separate functions and combine them with <a href="https://redux.js.org/docs/api/combineReducers.html" target="_blank">combineReducers</a></p>
<p>In the next section we’ll play with Redux from the console. Hold tight!</p>
<h2>React Redux tutorial: Redux store methods</h2>
<p>This will be super quick, I promise.</p>
<p>I want you to play with the brower’s console for gaining a quick understanding of how Redux works.</p>
<p>Redux itself is a small library (2KB). The <a href="https://redux.js.org/docs/api/Store.html" target="_blank">Redux store exposes a simple API</a> for managing the state. The most important methods are:</p>
<ul>
<li><a href="https://redux.js.org/docs/api/Store.html#getState" target="_blank">getState</a> for accessing the current state of the application</li>
<li><a href="https://redux.js.org/docs/api/Store.html#dispatch" target="_blank">dispatch</a> for dispatching an action</li>
<li><a href="https://redux.js.org/docs/api/Store.html#subscribe" target="_blank">subscribe</a> for listening on state changes</li>
</ul>
<p>We will play in the brower’s console with the above methods.</p>
<p>To do so we have to export as global variables the store and the action we created earlier.</p>
<p>Create <code>src/js/index.js</code>src/js/index.jsand update the file with the following code:</p>
<pre>import store from "../js/store/index";
import { addArticle } from "../js/actions/index";

window.store = store;
window.addArticle = addArticle;</pre><div><ol><li>import store from "../js/store/index";</li><li>import { addArticle } from "../js/actions/index";</li><li>window.store = store;</li><li>window.addArticle = addArticle;</li></ol><pre>import store from "../js/store/index";
import { addArticle } from "../js/actions/index";

window.store = store;
window.addArticle = addArticle;</pre></div>
<p>Open up <code>src/index.js</code>src/index.jsas well, clean up its content and update it as follows:</p>
<pre>import index from "./js/index"</pre><div><ol><li>import index from "./js/index"</li></ol><pre>import index from "./js/index"</pre></div>
<p>Now run webpack dev server (or Parcel) with:</p>
<pre>npm start</pre><div><ol><li>npm start</li></ol><pre>npm start</pre></div>
<p>head over http://localhost:8080/ and open up the console with F12.</p>
<p>Since we’ve exported the store as a global variable we can access its methods. Give it a try!</p>
<p>Start off by <strong>accessing the current state</strong>:</p>
<pre>store.getState()</pre><div><ol><li>store.getState()</li></ol><pre>store.getState()</pre></div>
<p>output:</p>
<pre>{articles: Array(0)}</pre><div><ol><li>{articles: Array(0)}</li></ol><pre>{articles: Array(0)}</pre></div>
<p>Zero articles. In fact we haven’t update the initial state yet.</p>
<p>To make things interesting we can listen for state updates with <a href="https://redux.js.org/docs/api/Store.html#subscribe" target="_blank">subscribe</a>.</p>
<p>The <strong>subscribe method accepts a callback that will fire whenever an action is dispatched</strong>. Dispatching an action means notifying the store that we want to change the state.</p>
<p>Register the callback with:</p>
<pre>store.subscribe(() =&gt; console.log('Look ma, Redux!!'))</pre><div><ol><li>store.subscribe(() =&gt; console.log('Look ma, Redux!!'))</li></ol><pre>store.subscribe(() =&gt; console.log('Look ma, Redux!!'))</pre></div>
<p>To <strong>change the state in Redux we need to dispatch an action</strong>. To dispatch an action you have to call the <a href="https://redux.js.org/docs/api/Store.html#dispatch" target="_blank">dispatch</a> method.</p>
<p>We have one action at our disposal: addArticle for adding a new item to the state.</p>
<p>Let’s dispatch the action with:</p>
<pre>store.dispatch( addArticle({ name: 'React Redux Tutorial for Beginners', id: 1 }) )</pre><div><ol><li>store.dispatch( addArticle({ name: 'React Redux Tutorial for Beginners', id: 1 }) )</li></ol><pre>store.dispatch( addArticle({ name: 'React Redux Tutorial for Beginners', id: 1 }) )</pre></div>
<p>Right after running the above code you should see:</p>
<pre>Look ma, Redux!!</pre><div><ol><li>Look ma, Redux!!</li></ol><pre>Look ma, Redux!!</pre></div>
<p>To verify that the state changed run again:</p>
<pre>store.getState()</pre><div><ol><li>store.getState()</li></ol><pre>store.getState()</pre></div>
<p>The output should be:</p>
<pre>{articles: Array(1)}</pre><div><ol><li>{articles: Array(1)}</li></ol><pre>{articles: Array(1)}</pre></div>
<p>And that’s it. This is Redux in its simplest form.</p>
<p>Was that difficult?</p>
<p>Take your time to explore these three Redux methods as an exercise. Play with them from the console:</p>
<ul>
<li><a href="https://redux.js.org/docs/api/Store.html#getState" target="_blank">getState</a> for <strong>accessing the current state</strong> of the application</li>
<li><a href="https://redux.js.org/docs/api/Store.html#dispatch" target="_blank">dispatch</a> for <strong>dispatching an action</strong></li>
<li><a href="https://redux.js.org/docs/api/Store.html#subscribe" target="_blank">subscribe</a> for <strong>listening on state changes</strong></li>
</ul>
<p>That’s everything you need to know for getting started with Redux.</p>
<p>Once you feel confident head over the next section. We’ll go straight to connecting React with Redux!</p>
<h2>React Redux tutorial: connecting React with Redux</h2>
<p>After learning Redux I realized it wasn’t so complex.</p>
<p>I knew how to access the current state with <a href="https://redux.js.org/docs/api/Store.html#getState" target="_blank">getState</a>.</p>
<p>I knew how to dispatch an action with <a href="https://redux.js.org/docs/api/Store.html#dispatch" target="_blank">dispatch</a></p>
<p>I knew how to listen for state changes with <a href="https://redux.js.org/docs/api/Store.html#subscribe" target="_blank">subscribe</a></p>
<p>Yet I didn’t know how to couple <strong>React and Redux</strong> together.</p>
<p>I was asking myself: should I call getState within a React component? How do I dispatch an action from a React component? And so on.</p>
<p>Redux on its own is framework agnostic. You can use it with vanilla Javascript. Or with Angular. Or with React. There are bindings for joining together Redux with your favorite framework/library.</p>
<p>For React there is <a href="https://redux.js.org/docs/basics/UsageWithReact.html" target="_blank">react-redux</a>.</p>
<p>Before moving forward install <a href="https://redux.js.org/docs/basics/UsageWithReact.html" target="_blank">react-redux</a> by running:</p>
<pre>npm i react-redux --save-dev</pre><div><ol><li>npm i react-redux --save-dev</li></ol><pre>npm i react-redux --save-dev</pre></div>
<p>To demonstrate how React and Redux work together we’ll build a super simple application. The application is made of the following components:</p>
<ul>
<li>an App component</li>
<li>a List component for displaying articles</li>
<li>a Form component for adding new articles</li>
</ul>
<p>(The application is a toy and it does nothing serious other than displaying a list and a form for adding new items. Nonetheless it’s still a good starting point for learning Redux)</p>
<h2>React Redux tutorial: react-redux</h2>
<p><a href="https://redux.js.org/docs/basics/UsageWithReact.html" target="_blank">react-redux</a> is a Redux binding for React. It’s a small library for connecting Redux and React in an efficient way.</p>
<p>The most important method you’ll work with is <a href="https://github.com/reactjs/react-redux/blob/master/docs/api.md#connectmapstatetoprops-mapdispatchtoprops-mergeprops-options" target="_blank">connect</a></p>
<p>What does react-redux’s <strong>connect</strong> do? Unsurprisingly it connects a React component with the Redux store.</p>
<p>You will use connect with two or three arguments depending on the use case. The fundamental things to know are:</p>
<ul>
<li>the mapStateToProps function</li>
<li>the mapDispatchToProps function</li>
</ul>
<p><strong>What does mapStateToProps do</strong> in react-redux? mapStateToProps does exactly what its name suggests: it <strong>connects a part of the Redux state</strong> to the <a href="https://reactjs.org/docs/components-and-props.html" target="_blank">props of a React component</a>. By doing so a connected React component will have access to the exact part of the store it needs.</p>
<p><strong>What does mapDispatchToProps</strong> do in react-redux? mapDispatchToProps does something similar, but for actions. <strong>mapDispatchToProps connects Redux actions to React props</strong>. This way a connected React component will be able to dispatch actions.</p>
<p>Is everything clear? If not, stop and take your time to re-read the guide. I know it’s a lot to learn and it requires time. Don’t worry if you don’t get Redux right know. It will click sooner or later.</p>
<p>In the next section we’ll finally get our hands dirty!</p>
<h2>React Redux tutorial: App component and Redux store</h2>
<p>We saw that mapStateToProps connects a portion of the Redux state to the props of a React component. You may wonder: is this enough for connecting Redux with React? No, it’s not.</p>
<p>To start off <strong>connecting Redux with React we’re going to use <a href="https://github.com/reactjs/react-redux/blob/master/docs/api.md#provider-store" target="_blank">Provider</a></strong>.</p>
<p><a href="https://github.com/reactjs/react-redux/blob/master/docs/api.md#provider-store" target="_blank">Provider</a> is an high order component coming from react-redux.</p>
<p>Using layman’s terms, Provider wraps up your React application and makes it aware of the entire Redux’s store.</p>
<p>Why so? We saw that in Redux the store manages everything. React must talk to the store for accessing the state and dispatching actions.</p>
<p>Enough theory.</p>
<p>Open up <code>src/js/index.js</code>src/js/index.js, wipe out everything and update the file with the following code:</p>
<pre>import React from "react";
import { render } from "react-dom";
import { Provider } from "react-redux";
import store from "./store/index";
import App from "./components/App";

render(
  &lt;Provider store={store}&gt;
    &lt;App /&gt;
  &lt;/Provider&gt;,
  document.getElementById("app")
);</pre><div><ol><li>import React from "react";</li><li>import { render } from "react-dom";</li><li>import { Provider } from "react-redux";</li><li>import store from "./store/index";</li><li>import App from "./components/App";</li><li>render(</li><li>  &lt;Provider store={store}&gt;</li><li>    &lt;App /&gt;</li><li>  &lt;/Provider&gt;,</li><li>  document.getElementById("app")</li></ol><pre>import React from "react";
import { render } from "react-dom";
import { Provider } from "react-redux";
import store from "./store/index";
import App from "./components/App";

render(
  &lt;Provider store={store}&gt;
    &lt;App /&gt;
  &lt;/Provider&gt;,
  document.getElementById("app")
);</pre></div>
<p>You see? Provider wraps up your entire React application. Moreover it gets the store as a prop.</p>
<p>Now let’s create the <strong>App</strong> component since we’re requiring it. It’s nothing special: App should import a List component and render itself.</p>
<p>Create a directory for holding the components:</p>
<pre>mkdir -p src/js/components</pre><div><ol><li>mkdir -p src/js/components</li></ol><pre>mkdir -p src/js/components</pre></div>
<p>and a new file named <code>App.js</code>App.jsinside <code>src/js/components</code>src/js/components:</p>
<pre>// src/js/components/App.js
import React from "react";
import List from "./List";

const App = () =&gt; (
  &lt;div className="row mt-5"&gt;
    &lt;div className="col-md-4 offset-md-1"&gt;
    &lt;h2&gt;Articles&lt;/h2&gt;
      &lt;List /&gt;
    &lt;/div&gt;
  &lt;/div&gt;
);

export default App;</pre><div><ol><li>// src/js/components/App.js</li><li>import React from "react";</li><li>import List from "./List";</li><li>const App = () =&gt; (</li><li>  &lt;div className="row mt-5"&gt;</li><li>    &lt;div className="col-md-4 offset-md-1"&gt;</li><li>    &lt;h2&gt;Articles&lt;/h2&gt;</li><li>      &lt;List /&gt;</li><li>    &lt;/div&gt;</li><li>  &lt;/div&gt;</li><li>export default App;</li></ol><pre>// src/js/components/App.js
import React from "react";
import List from "./List";

const App = () =&gt; (
  &lt;div className="row mt-5"&gt;
    &lt;div className="col-md-4 offset-md-1"&gt;
    &lt;h2&gt;Articles&lt;/h2&gt;
      &lt;List /&gt;
    &lt;/div&gt;
  &lt;/div&gt;
);

export default App;</pre></div>
<p>Take moment and look at the component without the markup:</p>
<pre>import React from "react";
import List from "./List";

const App = () =&gt; (
      &lt;List /&gt;
);

export default App;</pre><div><ol><li>import React from "react";</li><li>import List from "./List";</li><li>const App = () =&gt; (</li><li>      &lt;List /&gt;</li><li>export default App;</li></ol><pre>import React from "react";
import List from "./List";

const App = () =&gt; (
      &lt;List /&gt;
);

export default App;</pre></div>
<p>then move on to creating <strong>List</strong>.</p>
<h2>React Redux tutorial: List component and Redux state</h2>
<p>We have done nothing special so far.</p>
<p>But our new component, List, will interact with the Redux store.</p>
<p>A brief recap: the key for connecting a React component with Redux is <a href="https://github.com/reactjs/react-redux/blob/master/docs/api.md#connectmapstatetoprops-mapdispatchtoprops-mergeprops-options" target="_blank">connect</a>.</p>
<p>Connect takes at least one argument.</p>
<p>Since we want List to get a list of articles it’s a matter of connecting <code>state.articles</code>state.articleswith the component. How? With <strong>mapStateToProps</strong>.</p>
<p>Create a new file named <code>List.js</code>List.jsinside <code>src/js/components</code>src/js/components. It should look like the following:</p>
<pre>// src/js/components/List.js

import React from "react";
import { connect } from "react-redux";

const mapStateToProps = state =&gt; {
  return { articles: state.articles };
};

const ConnectedList = ({ articles }) =&gt; (
  &lt;ul className="list-group list-group-flush"&gt;
    {articles.map(el =&gt; (
      &lt;li className="list-group-item" key={el.id}&gt;
        {el.title}
      &lt;/li&gt;
    ))}
  &lt;/ul&gt;
);

const List = connect(mapStateToProps)(ConnectedList);

export default List;</pre><div><ol><li>// src/js/components/List.js</li><li>import React from "react";</li><li>import { connect } from "react-redux";</li><li>const mapStateToProps = state =&gt; {</li><li>  return { articles: state.articles };</li><li>const ConnectedList = ({ articles }) =&gt; (</li><li>  &lt;ul className="list-group list-group-flush"&gt;</li><li>    {articles.map(el =&gt; (</li><li>      &lt;li className="list-group-item" key={el.id}&gt;</li><li>        {el.title}</li><li>      &lt;/li&gt;</li><li>  &lt;/ul&gt;</li><li>const List = connect(mapStateToProps)(ConnectedList);</li><li>export default List;</li></ol><pre>// src/js/components/List.js

import React from "react";
import { connect } from "react-redux";

const mapStateToProps = state =&gt; {
  return { articles: state.articles };
};

const ConnectedList = ({ articles }) =&gt; (
  &lt;ul className="list-group list-group-flush"&gt;
    {articles.map(el =&gt; (
      &lt;li className="list-group-item" key={el.id}&gt;
        {el.title}
      &lt;/li&gt;
    ))}
  &lt;/ul&gt;
);

const List = connect(mapStateToProps)(ConnectedList);

export default List;</pre></div>
<p>The List component receives the prop <code>articles</code>articleswhich is a copy of the <code>articles</code>articlesarray. Such array lives inside the Redux state we created earlier. It comes from the reducer:</p>
<pre>const initialState = {
  articles: []
};

const rootReducer = (state = initialState, action) =&gt; {
  switch (action.type) {
    case ADD_ARTICLE:
      return { ...state, articles: [...state.articles, action.payload] };
    default:
      return state;
  }
};</pre><div><ol><li>const initialState = {</li><li>  articles: []</li><li>const rootReducer = (state = initialState, action) =&gt; {</li><li>  switch (action.type) {</li><li>    case ADD_ARTICLE:</li><li>      return { ...state, articles: [...state.articles, action.payload] };</li><li>    default:</li><li>      return state;</li></ol><pre>const initialState = {
  articles: []
};

const rootReducer = (state = initialState, action) =&gt; {
  switch (action.type) {
    case ADD_ARTICLE:
      return { ...state, articles: [...state.articles, action.payload] };
    default:
      return state;
  }
};</pre></div>
<p>Then it’s a matter of using the prop inside JSX for generating a list of articles:</p>
<pre>{articles.map(el =&gt; (
  &lt;li className="list-group-item" key={el.id}&gt;
    {el.title}
  &lt;/li&gt;
))}</pre><div><ol><li>{articles.map(el =&gt; (</li><li>  &lt;li className="list-group-item" key={el.id}&gt;</li><li>    {el.title}</li><li>  &lt;/li&gt;</li></ol><pre>{articles.map(el =&gt; (
  &lt;li className="list-group-item" key={el.id}&gt;
    {el.title}
  &lt;/li&gt;
))}</pre></div>
<p><strong>React protip</strong>: take the habit of validating props with <a href="https://reactjs.org/docs/typechecking-with-proptypes.html" target="_blank">PropTypes</a></p>
<p>Finally the component gets exported as List. List is the result of connecting the stateless component ConnectedList with the Redux store.</p>
<p><em>A stateless component does not have its own local state. Data gets passed to it as props</em></p>
<p>Still confused? I was too. Understanding how <strong>connect</strong> works will take some time. Fear not, the road to learn Redux is paved with “ah-ha” moments.</p>
<p>I suggest taking a break for exploring both <strong>connect</strong> and <strong>mapStateToProps.</strong></p>
<p>Once you’re confident about them head over the next section!</p>
<h2>React Redux tutorial: Form component and Redux actions</h2>
<p>The Form component we’re going to create is a bit more complex than List. It’s a form for adding new items to our application.</p>
<p>Plus it is a <strong>stateful component</strong>.</p>
<p><em>A stateful component in React is a component carrying its own local state</em></p>
<p>A stateful component? “Valentino, we’re talking about Redux for managing the state! Why on earth would you give Form its own local state??”</p>
<p><strong>Even when using Redux it is totally fine to have stateful components</strong>.</p>
<p>Not every piece of the application’s state should go inside Redux.</p>
<p>In this example I don’t want any other component to be aware of the Form local state.</p>
<p>And that’s perfectly fine.</p>
<p>What does the component do?</p>
<p>The component contains some logic for updating the local state upon a form submission.</p>
<p>Plus it receives a Redux action as prop. This way it can update the global state by dispatching the addArticle action.</p>
<p>Create a new file named <code>Form.js</code>Form.jsinside <code>src/js/components</code>src/js/components. It should look like the following:</p>
<pre>// src/js/components/Form.js
import React, { Component } from "react";
import { connect } from "react-redux";
import uuidv1 from "uuid";
import { addArticle } from "../actions/index";

const mapDispatchToProps = dispatch =&gt; {
  return {
    addArticle: article =&gt; dispatch(addArticle(article))
  };
};

class ConnectedForm extends Component {
  constructor() {
    super();

    this.state = {
      title: ""
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({ [event.target.id]: event.target.value });
  }

  handleSubmit(event) {
    event.preventDefault();
    const { title } = this.state;
    const id = uuidv1();
    this.props.addArticle({ title, id });
    this.setState({ title: "" });
  }

  render() {
    const { title } = this.state;
    return (
      &lt;form onSubmit={this.handleSubmit}&gt;
        &lt;div className="form-group"&gt;
          &lt;label htmlFor="title"&gt;Title&lt;/label&gt;
          &lt;input
            type="text"
            className="form-control"
            id="title"
            value={title}
            onChange={this.handleChange}
          /&gt;
        &lt;/div&gt;
        &lt;button type="submit" className="btn btn-success btn-lg"&gt;
          SAVE
        &lt;/button&gt;
      &lt;/form&gt;
    );
  }
}

const Form = connect(null, mapDispatchToProps)(ConnectedForm);

export default Form;</pre><div><ol><li>// src/js/components/Form.js</li><li>import React, { Component } from "react";</li><li>import { connect } from "react-redux";</li><li>import uuidv1 from "uuid";</li><li>import { addArticle } from "../actions/index";</li><li>const mapDispatchToProps = dispatch =&gt; {</li><li>  return {</li><li>    addArticle: article =&gt; dispatch(addArticle(article))</li><li>class ConnectedForm extends Component {</li><li>  constructor() {</li><li>    super();</li><li>    this.state = {</li><li>      title: ""</li><li>    this.handleChange = this.handleChange.bind(this);</li><li>    this.handleSubmit = this.handleSubmit.bind(this);</li><li>  handleChange(event) {</li><li>    this.setState({ [event.target.id]: event.target.value });</li><li>  handleSubmit(event) {</li><li>    event.preventDefault();</li><li>    const { title } = this.state;</li><li>    const id = uuidv1();</li><li>    this.props.addArticle({ title, id });</li><li>    this.setState({ title: "" });</li><li>  render() {</li><li>    const { title } = this.state;</li><li>    return (</li><li>      &lt;form onSubmit={this.handleSubmit}&gt;</li><li>        &lt;div className="form-group"&gt;</li><li>          &lt;label htmlFor="title"&gt;Title&lt;/label&gt;</li><li>          &lt;input</li><li>            type="text"</li><li>            className="form-control"</li><li>            id="title"</li><li>            value={title}</li><li>            onChange={this.handleChange}</li><li>          /&gt;</li><li>        &lt;/div&gt;</li><li>        &lt;button type="submit" className="btn btn-success btn-lg"&gt;</li><li>        &lt;/button&gt;</li><li>      &lt;/form&gt;</li><li>const Form = connect(null, mapDispatchToProps)(ConnectedForm);</li><li>export default Form;</li></ol><pre>// src/js/components/Form.js
import React, { Component } from "react";
import { connect } from "react-redux";
import uuidv1 from "uuid";
import { addArticle } from "../actions/index";

const mapDispatchToProps = dispatch =&gt; {
  return {
    addArticle: article =&gt; dispatch(addArticle(article))
  };
};

class ConnectedForm extends Component {
  constructor() {
    super();

    this.state = {
      title: ""
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({ [event.target.id]: event.target.value });
  }

  handleSubmit(event) {
    event.preventDefault();
    const { title } = this.state;
    const id = uuidv1();
    this.props.addArticle({ title, id });
    this.setState({ title: "" });
  }

  render() {
    const { title } = this.state;
    return (
      &lt;form onSubmit={this.handleSubmit}&gt;
        &lt;div className="form-group"&gt;
          &lt;label htmlFor="title"&gt;Title&lt;/label&gt;
          &lt;input
            type="text"
            className="form-control"
            id="title"
            value={title}
            onChange={this.handleChange}
          /&gt;
        &lt;/div&gt;
        &lt;button type="submit" className="btn btn-success btn-lg"&gt;
          SAVE
        &lt;/button&gt;
      &lt;/form&gt;
    );
  }
}

const Form = connect(null, mapDispatchToProps)(ConnectedForm);

export default Form;</pre></div>
<p>What can I say about the component? Besides <strong>mapDispatchToProps</strong> and <strong>connect</strong> it’s standard React stuff.</p>
<p><strong>mapDispatchToProps connects Redux actions to React props</strong>. This way a connected component is able to dispatch actions.</p>
<p>You can see how the action gets dispatched in the handleSubmit method:</p>
<pre>// ...
  handleSubmit(event) {
    event.preventDefault();
    const { title } = this.state;
    const id = uuidv1();
    this.props.addArticle({ title, id }); // Relevant Redux part!!
// ...
  }
// ...</pre><div><ol><li>// ...</li><li>  handleSubmit(event) {</li><li>    event.preventDefault();</li><li>    const { title } = this.state;</li><li>    const id = uuidv1();</li><li>    this.props.addArticle({ title, id }); // Relevant Redux part!!</li><li>// ...</li><li>// ...</li></ol><pre>// ...
  handleSubmit(event) {
    event.preventDefault();
    const { title } = this.state;
    const id = uuidv1();
    this.props.addArticle({ title, id }); // Relevant Redux part!!
// ...
  }
// ...</pre></div>
<p>Finally the component gets exported as Form. Form is the result of connecting ConnectedForm with the Redux store.</p>
<p>Side note: the first argument for connect must be <code>null</code>nullwhen mapStateToProps is absent like in the Form example. Otherwise you’ll get <code>TypeError: dispatch is not a function</code>TypeError: dispatch is not a function.</p>
<p>Our components are all set!</p>
<p>Update App to include the Form component:</p>
<pre>import React from "react";
import List from "./List";
import Form from "./Form";

const App = () =&gt; (
  &lt;div className="row mt-5"&gt;
    &lt;div className="col-md-4 offset-md-1"&gt;
      &lt;h2&gt;Articles&lt;/h2&gt;
      &lt;List /&gt;
    &lt;/div&gt;
    &lt;div className="col-md-4 offset-md-1"&gt;
      &lt;h2&gt;Add a new article&lt;/h2&gt;
      &lt;Form /&gt;
    &lt;/div&gt;
  &lt;/div&gt;
);

export default App;</pre><div><ol><li>import React from "react";</li><li>import List from "./List";</li><li>import Form from "./Form";</li><li>const App = () =&gt; (</li><li>  &lt;div className="row mt-5"&gt;</li><li>    &lt;div className="col-md-4 offset-md-1"&gt;</li><li>      &lt;h2&gt;Articles&lt;/h2&gt;</li><li>      &lt;List /&gt;</li><li>    &lt;/div&gt;</li><li>    &lt;div className="col-md-4 offset-md-1"&gt;</li><li>      &lt;h2&gt;Add a new article&lt;/h2&gt;</li><li>      &lt;Form /&gt;</li><li>    &lt;/div&gt;</li><li>  &lt;/div&gt;</li><li>export default App;</li></ol><pre>import React from "react";
import List from "./List";
import Form from "./Form";

const App = () =&gt; (
  &lt;div className="row mt-5"&gt;
    &lt;div className="col-md-4 offset-md-1"&gt;
      &lt;h2&gt;Articles&lt;/h2&gt;
      &lt;List /&gt;
    &lt;/div&gt;
    &lt;div className="col-md-4 offset-md-1"&gt;
      &lt;h2&gt;Add a new article&lt;/h2&gt;
      &lt;Form /&gt;
    &lt;/div&gt;
  &lt;/div&gt;
);

export default App;</pre></div>
<p>Install uuid with:</p>
<pre>npm i uuid --save-dev</pre><div><ol><li>npm i uuid --save-dev</li></ol><pre>npm i uuid --save-dev</pre></div>
<p>Now run webpack (or Parcel) with:</p>
<pre>npm start</pre><div><ol><li>npm start</li></ol><pre>npm start</pre></div>
<p>and head over to http://localhost:8080</p>
<p>You should see the following working POC:</p>
<p><div class="readableLargeImageContainer"><img src="https://www.valentinog.com/blog/wp-content/uploads/2017/12/react-redux-demo.png"   alt="React Redux tutorial demo. Nothing fancy but still useful for showing React and Redux at work" /></div></p>
<p>Nothing fancy but still useful for showing React and Redux at work!</p>
<p>The <strong>List component on the left is connected to the Redux store</strong>. It will re-render whenever you add a new item.</p>
<p><div class="readableLargeImageContainer"><img src="https://www.valentinog.com/blog/wp-content/uploads/2017/12/react-redux-tutorial-demo-gif.gif"   alt="React Redux demo " /></div></p>
<p>Whoaaa!</p>
<p>You can find the code for that silly app (with prop-types and a splitted reducer) on my <a href="https://github.com/valentinogagliardi/minimal-react-redux-webpack" target="_blank">Github repo</a>.</p>
<h2>React Redux tutorial: wrapping up</h2>
<p>I hope you’ll learn something from this guide. I tried my best to keep things as simple as possibile. I would love to hear your feedback in the comments below!</p>
<p>Redux has a lot of boilerplate and moving parts. Don’t get discouraged. Pick Redux, play with it and take your time to absorb all the concepts.</p>
<p>I went from zero to <strong>understanding Redux by small steps</strong>. You can do it too!</p>
<p>Also, take your time to investigate <strong>why</strong> and <strong>if</strong> you should <strong>use Redux in your application</strong>.</p>
<p>Either way think of Redux as an investment: learning it is <strong>100% worthwile</strong>.</p>
<p><em>Redux is not a universal solution for state management. <a href="https://github.com/mobxjs/mobx" target="_blank">Mobx</a> emerged as an interesting alternative. I’ve been watching <a href="https://dev-blog.apollodata.com/the-future-of-state-management-dd410864cae2" target="_blank">Apollo Client</a> too. Who will win? Only time will tell</em>.</p>
<h2>React Redux tutorial: resources for learning functional programming</h2>
<p>Redux scares most beginners because it revolves around functional programming and pure functions.</p>
<p>Suggesting some resources is the best I can do since functional programming is beyond the scope of this guide. These are the best places for learning more about functional programming and pure functions:</p>
<p><a href="https://drboolean.gitbooks.io/mostly-adequate-guide/content/ch1.html" target="_blank">Professor Frisby’s Mostly Adequate Guide to Functional Programming</a> by Brian Lonsdorf</p>
<p><a href="https://github.com/getify/Functional-Light-JS" target="_blank">Functional-Light Javascript</a> by Kyle Simpson</p>
<h2>React Redux tutorial: async actions in Redux</h2>
<p>I wasn’t sure whether talking about <strong>async actions</strong> would have been appropriate or not.</p>
<p>Most Redux beginners struggle to learn plain Redux. Handling async actions in Redux is not a straighforward task so better not overcomplicate things.</p>
<p>When you’ll feel confident about the core Redux concepts go check <a href="https://medium.com/@stowball/a-dummys-guide-to-redux-and-thunk-in-react-d8904a7005d3" target="_blank">A Dummy’s Guide to Redux and Thunk in React</a> by Matt Stow. It’s a nice introduction to handling API calls in Redux with <strong>redux-thunk</strong>.</p>
<p>Thanks for reading and happy coding!</p>

                         <div><div><section><div><h3><a href="http://www.valentinog.com" target="_blank">Valentino Gagliardi</a></h3><div>Web Developer & IT Consultant, with over 10 year of experience, I'm here to help you developing your next idea.</div></div> </section></div> </div>	
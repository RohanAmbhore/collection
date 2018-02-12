<a href="https://daveceddia.com/create-react-app-express-backend/">https://daveceddia.com/create-react-app-express-backend/</a><div id="articleHeader"><h1>Create React App with an Express Backend</h1></div>
      <footer>
        
        
        
        <time> April 19, 2017</time>
        
        
        
        
      </footer>
      <a href="https://twitter.com/intent/follow?screen_name=dceddia" id="twitter-follow" target="_blank">
	 Follow @dceddia</a>


      <div>
        
        <p>If you haven’t heard of it yet, <a href="https://github.com/facebookincubator/create-react-app" target="_blank">Create React App</a> is an awesome way to get started with React. It creates a project structure for you, all set up and ready to go. You get to skip the configuration of Webpack and Babel, and get right down to writing your app.</p>

<p>But what if your app isn’t <em>purely</em> frontend? What if you need to connect to a backend server? Create React App has you covered.</p>

<p>In this post we’ll set up a React app alongside an Express backend app, and wire up the UI to fetch some data from the backend.</p>

<p>And, if your backend is <em>not</em> written with Express, don’t worry! This same process will work for you too (skip to the <a href="#configure-the-proxy" target="_blank">Configure the Proxy</a> section).</p>

<p>If you prefer video, here’s a quick walkthrough of the steps below:</p>

<div>
  <div class="readableLargeObjectContainer"><iframe src="https://www.youtube.com/embed/8bNlffXEcC0" width="560" height="315" frameborder="0" /></div>


<h2 id="create-the-express-app">Create the Express App</h2>

<p>We’ll need an Express app first off. If you have one already, you can skip this step.</p>

<p>For the purpose of this post, we’ll generate one with the <a href="https://expressjs.com/en/starter/generator.html" target="_blank">express-generator</a> utility. Install the generator:</p>

<pre><code>$ npm install -g express-generator
# or:  yarn global add express-generator
</code></pre>

<p><div class="readableLargeImageContainer"><img src="https://daveceddia.com/images/install-express-generator.png" alt="Output from installing express-generator" /></div></p>

<p>Then run it to create the Express app:</p>

<pre><code>$ express react-backend
</code></pre>

<p><div class="readableLargeImageContainer"><img src="https://daveceddia.com/images/generate-express-app.png" alt="Output from generating react-backend" /></div></p>

<p>It’ll create a <code>react-backend</code> folder. Then make sure to install the dependencies:</p>

<pre><code>$ cd react-backend
$ npm install   # or yarn
</code></pre>

<p>We can ignore most of the generated files but we’ll edit the <code>react-backend/routes/users.js</code> file as a simple way to return some data. Here’s the change we’ll make:</p>

<pre><code>var express = require('express');
var router = express.Router();

/* GET users listing. */
router.get('/', function(req, res, next) {
	// Comment out this line:
  //res.send('respond with a resource');

  // And insert something like this instead:
  res.json([{
  	id: 1,
  	username: "samsepi0l"
  }, {
  	id: 2,
  	username: "D0loresH4ze"
  }]);
});

module.exports = router;
</code></pre>

<p>That’s all we’ll do to Express. Start up the app by running this:</p>

<pre><code>$ PORT=3001 node bin/www
</code></pre>

<p>Leave it running, and open up a new terminal. Note the <code>PORT</code> variable: this Express app will default to port 3000, and Create React App will also default to port 3000. To avoid the conflict, start Express on 3001.</p>

<h2 id="create-the-react-app">Create the React App</h2>

<p>You can put the React app anywhere you like. It doesn’t need to be a subfolder of the Express app, but that’s what we’ll do here to keep things organized.</p>

<p>First things first, make sure you have <code>create-react-app</code> installed if you don’t already:</p>

<pre><code>npm install -g create-react-app
</code></pre>

<p>Then, from inside the <code>react-backend</code> folder, create the React app:</p>

<pre><code>create-react-app client
</code></pre>

<h2 id="configure-the-proxy">Configure the Proxy</h2>

<p>This is the key change that will let the React app talk to the Express backend (or any backend).</p>

<p>Inside the React app’s folder (<code>client</code>), open up <code>package.json</code> (make sure it’s not Express’ package.json – it should have things like “react” and “react-scripts” in it). Under the “scripts” section, add the “proxy” line like this:</p>

<pre><code>  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  },
  "proxy": "<a href="http://localhost:3001" target="_blank">http://localhost:3001</a>"
</code></pre>

<p>The port (3001) in the “proxy” line <em>must match</em> the port that your Express server is running on.</p>

<p>Note that this can point to <em>any</em> server. It can be another local backend in Java or Python, or it could be a real server on the internet. Doesn’t matter.</p>

<p>The way this works is, any time your React app makes a request to something that’s not a static asset (not an image or CSS or <code>index.html</code>, basically), it will forward the request to the server specified in <code>"proxy"</code>.</p>

<p><div class="readableLargeImageContainer"><img src="https://daveceddia.com/images/how-proxy-works.png" alt="How the Proxy Works" /></div></p>

<p>Once this is done, start the React development server by running <code>npm start</code> (or <code>yarn start</code>).</p>

<h2 id="fetch-the-data-from-react">Fetch the Data from React</h2>

<p>At this point 2 servers are running: Express (on port 3001) and Create React App’s Webpack dev server (on port 3000).</p>

<p>Let’s make a call to the <code>/users</code> endpoint and make sure the whole pipeline is working.</p>

<p>Open up <code>client/src/App.js</code> and tweak it to look like this:</p>

<pre><code>import React, { Component } from 'react';
import './App.css';

class App extends Component {
  state = {users: []}

  componentDidMount() {
    fetch('/users')
      .then(res =&gt; res.json())
      .then(users =&gt; this.setState({ users }));
  }

  render() {
    return (
      &lt;div className="App"&gt;
        &lt;h1&gt;Users&lt;/h1&gt;
        {this.state.users.map(user =&gt;
          &lt;div key={user.id}&gt;{user.username}&lt;/div&gt;
        )}
      &lt;/div&gt;
    );
  }
}

export default App;
</code></pre>

<p>The changes here are:</p>

<ul>
  <li>
    <p>Setting an initial state at the top: an empty users array will prevent the <code>this.state.users.map</code> from blowing up before the users are loaded.</p>
  </li>
  <li>
    <p>Changed <code>render</code> to render the list of users.</p>
  </li>
  <li>
    <p>Added <code>componentDidMount</code> to get the data using <code>fetch</code>, and save them in state.</p>
  </li>
</ul>

<p>Create React App comes with the <code>fetch</code> polyfill <a href="https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#supported-language-features-and-polyfills" target="_blank">built in</a> so you’re all set even if your browser doesn’t natively support it yet. [thanks to Mohamed Elbou for pointing this out in the comments]</p>

<p>There’s also further reading if you’re wondering <a href="/ajax-requests-in-react/" target="_blank">how to do AJAX in React</a> or why the fetch is in <a href="/where-fetch-data-componentwillmount-vs-componentdidmount/" target="_blank">componentDidMount instead of componentWillMount</a>.</p>

<h2 id="wrap-up">Wrap Up</h2>

<p>Now you’re a pro at hooking up a CRA-generated app to any backend you can throw at it! Got more questions? Want to see something else? Leave a comment below.</p>

<h2 id="want-to-deploy-to-production">Want to Deploy to Production?</h2>

<p>Check out Part 2, <a href="/create-react-app-express-production" target="_blank">Create React App with Express in Production</a> where we build an Express+React app and deploy it to Heroku.</p>

<h2 id="translations">Translations</h2>

<p>Read this in <a href="https://reactx.de/artikel/erstellen-einer-reactjs-app-mit-express-backend/" target="_blank">Deutsche (German)</a>.</p>

        
          <div>
  <p>For a step-by-step approach to learning React,<br /> check out my <a href="https://daveceddia.com/pure-react/?utm_campaign=after-post" target="_blank">book</a> — grab 2 free sample chapters.</p>
  <div>
    <div>
      As far as I am concerned, even the intro which is free is worth the price.
    </div>
    <div>
      <div>— Isaac</div>
    
  


        
        
	  <div><div>
  
<div>
  <div>
    <h3>Download a Timeline for Learning React</h3>
    <div>
      
        
      
      <p><div class="readableLargeImageContainer float"><img src="https://convertkit.s3.amazonaws.com/assets/pictures/13404/537365/content_Screen_Shot_2017-05-01_at_11.31.01_AM.png" /></div></p><p>Sign up and get my React Learning Timeline PDF and weekly articles about React and JavaScript.</p>
    
  

  








	

        
          
          




        
      
    
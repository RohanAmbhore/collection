<a href="https://github.com/supnate/rekit">https://github.com/supnate/rekit</a><div id="articleHeader"><h1>IDE and toolkit for building scalable web applications with React, Redux and React-router</h1></div>

    
  

  <div>
  <div>
    <div>
          
            IDE and toolkit for building scalable web applications with React, Redux and React-router
          
          <a href="http://rekit.js.org" target="_blank">http://rekit.js.org</a>
    </div>

  </div>

    
</div>



  

    <div>
      JavaScript
      HTML
      CSS
    </div>


    

  


  


  







  
    <h3>
      
      README.md
    </h3>

      
<blockquote>
<p><g-emoji>🔥</g-emoji>  <a href="https://medium.com/@nate_wang/rekit-now-creates-apps-by-create-react-app-3f0d82fd64f3" target="_blank">Rekit Now Creates Apps By Create-react-app</a></p>
</blockquote>
<blockquote>
<p><g-emoji>🎉</g-emoji>  <a href="https://medium.com/@nate_wang/introducing-rekit-studio-a-real-ide-for-react-and-redux-development-baf0c99cb542" target="_blank">Introducing Rekit Studio: a real IDE for React and Redux development</a></p>
</blockquote>
<blockquote>
<p><g-emoji>🎉</g-emoji>  <a href="https://medium.com/@nate_wang/using-rekit-studio-in-an-existing-react-project-39713d9667b" target="_blank">Using Rekit Studio in an Existing React Project</a></p>
</blockquote>
<p>Rekit is a toolkit for building scalable web applications with React, Redux and React-router. It's an all-in-one solution for creating modern React apps.</p>
<p>It helps you focus on business logic rather than dealing with massive libraries, patterns, configurations etc.</p>
<p>Rekit creates apps bootstrapped by <a href="https://github.com/facebook/create-react-app" target="_blank">create-react-app</a> and uses an opinionated way to organize folder and code. It's designed to be scalable, testable and maintainable by using <a href="https://medium.com/@nate_wang/feature-oriented-architecture-for-web-applications-2b48e358afb0" target="_blank">feature oriented architecture</a>, <a href="https://medium.com/@nate_wang/a-new-approach-for-managing-redux-actions-91c26ce8b5da#.9em77fuwk" target="_blank">one action per file pattern</a>. This ensures application logic is well grouped and decoupled.</p>
<p>Besides creating apps, Rekit provides powerful tools for managing the project:</p>
<ol>
<li><a href="https://medium.com/@nate_wang/introducing-rekit-studio-a-real-ide-for-react-and-redux-development-baf0c99cb542" target="_blank">Rekit Studio</a>: the real IDE for React, Redux development.</li>
<li><a href="http://rekit.js.org/docs/cli.html" target="_blank">Command line tools</a>: besides Rekit Studio, you can use command line tools to create/rename/move/delete project elements like components, actions etc. It has better support for Rekit plugin system.</li>
</ol>
<p>Below is a quick demo video of how Rekit works:</p>
<p><a href="https://youtu.be/i53XffYtWMc" title="Rekit Demo" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/supnate/rekit/raw/master/images/rekit-studio-youtube.png"  alt="Rekit Demo" /></div></a></p>
<p>The demo contains two parts, which are examples in Redux's official website:</p>
<ol>
<li>Create a simple counter in 1 minute!</li>
<li>Show the latest reactjs topics on Reddit using async actions.</li>
</ol>
<h2>Live Demo</h2>
<p>You can also see the live demo at: <a href="http://demo.rekit.org" target="_blank">http://demo.rekit.org</a></p>
<h2>Installation</h2>
<pre><code>npm install -g rekit
</code></pre>
<p>This will install a global command <code>rekit</code> to the system. Rekit is developed and tested on npm 3+ and node 6+, so this is the prerequisite for using Rekit.</p>
<h2>Usage</h2>
<p>Create a new application</p>
<pre><code>rekit create &lt;app-name&gt; [--sass]
</code></pre>
<p>This will create a new app named <code>app-name</code> in the current directory. The <code>--sass</code> flag allows to use <a href="https://sass-lang.com/" target="_blank">sass</a> instead of default <a href="http://lesscss.org/" target="_blank">less</a> as the CSS transpiler. After creating the app, you need to install dependencies and start the dev server:</p>
<pre><code>cd app-name
npm install
npm start
</code></pre>
<p>It then starts two express servers by default:</p>
<ol>
<li>Webpack dev server: <a href="http://localhost:6075" target="_blank">http://localhost:6075</a>. Just what create-react-app starts.</li>
<li>Rekit Studio: <a href="http://localhost:6076" target="_blank">http://localhost:6076</a>. The IDE for Rekit projects.</li>
</ol>
<p>To change the ports dev-servers running on, edit the <code>rekit</code> section in <code>package.json</code>:</p>
<pre><code>{
  ...
  "rekit": {
    "devPort": 6075,
    "studioPort": 6076,
    ...
  }
  ...
}
</code></pre>
<h2>Packages</h2>
<p>This repo contains multiple packages managed by <a href="https://yarnpkg.com/lang/en/docs/workspaces/" target="_blank">yarn workspaces</a>.</p>
<table>
<thead>
<tr>
<th>Packages</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>rekit-core</td>
<td> Provide core APIs such as create components, rename actions, etc...</td>
</tr>
<tr>
<td>rekit</td>
<td> CLI wrapper of rekit-core, create apps by cloning repo from <a href="https://github.com/supnate/rekit-boilerplate-cra" target="_blank">rekit-boilerplate-cra</a></td>
</tr>
<tr>
<td>rekit-studio</td>
<td> Dedicated IDE for Rekit development, uses rekit-core to manage project too.</td>
</tr>
<tr>
<td>rekit-plugin-redux-saga</td>
<td> Use redux-saga instead of redux-thunk for async actions.</td>
</tr>
<tr>
<td>rekit-plugin-selector</td>
<td> Support selectors by Rekit cli.</td>
</tr>
<tr>
<td>rekit-plugin-apollo</td>
<td> Support graphql by <a href="https://www.apollographql.com/" target="_blank">Apollo</a>.</td>
</tr></tbody></table>
<h2>Key Features</h2>
<ul>
<li>It's production-ready but not a starter kit.</li>
<li>Zero additional configuration needed after creating an app.</li>
<li>Dedicated IDE for Rekit development.</li>
<li>Command line tools to manage actions, reducers, components and pages.</li>

<li>Use <a href="http://webpack.js.org" target="_blank">Webpack 3</a> for bundling.</li>
<li>Use <a href="https://babeljs.io/" target="_blank">Babel</a> for ES2015(ES6)+ support.</li>
<li>Use <a href="http://gaearon.github.io/react-hot-loader/" target="_blank">React hot loader</a> for hot module replacement.</li>
<li>Use <a href="http://redux.js.org/" target="_blank">Redux</a> for application state management.</li>

<li>Use <a href="https://webpack.js.org/plugins/dll-plugin/#src/components/Sidebar/Sidebar.jsx" target="_blank">Webpack dll plugin</a> to improve dev-time build performance.</li>
<li>Use <a href="http://lesscss.org/" target="_blank">Less</a> or <a href="https://sass-lang.com/" target="_blank">Sass</a> as CSS transpilers.</li>

<li>Support <a href="https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd" target="_blank">Redux dev tools</a>.</li>
</ul>
<h2>Documentation</h2>
<p><a href="http://rekit.js.org" target="_blank">http://rekit.js.org</a></p>
<h2>License</h2>


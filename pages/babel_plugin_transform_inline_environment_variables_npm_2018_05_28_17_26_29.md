<a href="https://www.npmjs.com/package/babel-plugin-transform-inline-environment-variables">https://www.npmjs.com/package/babel-plugin-transform-inline-environment-variables</a><div id="articleHeader"><h1>babel-plugin-transform-inline-environment-variables</h1></div>
<p>Inline environment variables</p>
<h2>Example</h2>

<div><pre><div>// assuming process.env.NODE_ENV is actually "development"</div><div>process.env.NODE_ENV;</div></pre>

<div><pre><div>"development";</div></pre>
<h2>Installation</h2>
<div><pre><div>npm install babel-plugin-transform-inline-environment-variables --save-dev</div></pre>
<h2>Usage</h2>
<h3>Via <code>.babelrc</code> (Recommended)</h3>
<p><strong>.babelrc</strong></p>
<div><pre><div>// without options</div><div>  "plugins": ["transform-inline-environment-variables"]</div><div>// with options</div><div>  "plugins": [</div><div>    ["transform-inline-environment-variables", {</div><div>      "include": [</div><div>        "NODE_ENV"</div></pre>
<h3>Via CLI</h3>
<div><pre><div>babel --plugins transform-inline-environment-variables script.js</div></pre>
<h3>Via Node API</h3>
<div><pre><div>require("@babel/core").transform("code", {</div><div>  plugins: ["transform-inline-environment-variables"]</div></pre>
<h2>Options</h2>
<ul>
<li><code>include</code> - array of environment variables to include</li>
<li><code>exclude</code> - array of environment variables to exclude</li>
</ul>

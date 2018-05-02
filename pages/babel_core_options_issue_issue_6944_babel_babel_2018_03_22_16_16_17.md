<a href="https://github.com/babel/babel/issues/6944">https://github.com/babel/babel/issues/6944</a><div id="articleHeader"><h1>              @babel/core - `options` issue            #6944    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/stephen-last" target="_blank">stephen-last</a>  opened this Issue
        <relative-time>on Dec 1, 2017</relative-time>
        · 14 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      

  
    
      
          <p>Choose one: is this a bug report or feature request? <strong>Bug?</strong></p>
<h3>Babel Configuration (.babelrc)</h3>
<div><pre>{
  "presets": [
    "@babel/preset-react",
    "@babel/preset-env"
  ],
  "plugins": [
    ["@babel/plugin-proposal-object-rest-spread"],
    ["@babel/plugin-proposal-class-properties", { "spec": true }]
  ]
}</pre></div>
<p>Dev deps:</p>
<div><pre>"devDependencies": {
    "@babel/cli": "^7.0.0-beta.32",
    "@babel/core": "^7.0.0-beta.32",
    "@babel/plugin-proposal-class-properties": "^7.0.0-beta.32",
    "@babel/plugin-proposal-object-rest-spread": "^7.0.0-beta.32",
    "@babel/polyfill": "^7.0.0-beta.32",
    "@babel/preset-env": "^7.0.0-beta.32",
    "@babel/preset-react": "^7.0.0-beta.32",
    "babel-loader": "^8.0.0-beta.0",
    "webpack": "^3.9.0"
  }</pre></div>
<h3>Expected Behavior</h3>
<p>Using <code>webpack.config.babel.js</code> should run.</p>
<h3>Current Behavior</h3>
<p>Error:</p>
<blockquote>
<p>TypeError: Cannot read property 'useBuiltIns' of undefined<br />
at _default (C:\node\clcommerce\node_modules@babel\plugin-proposal-object-rest-spread\lib\index.js:13:32)<br />
at Function.memoisePluginContainer (C:\node\clcommerce\node_modules\babel-core\lib\transformation\file\options\option-manager.js:113:13)</p>
</blockquote>
<p>Removing plugins just changes the error, but always points to an issue with options in <code>@babel/core</code>. For example, removing the plugins changes the error to:</p>
<blockquote>
<p>C:\node\clcommerce\node_modules\babel-core\lib\transformation\file\options\option-manager.js:328 throw e;<br />
TypeError: Cannot read property 'throwIfNamespace' of undefined (While processing preset: "C:\node\clcommerce\node_modules\<a href="https://github.com/babel" target="_blank">@babel</a>\preset-react\lib\index.js")</p>
</blockquote>
<p>Going back to <code>webpack.config.js</code> and using <code>require()</code>'s works.</p>
<h3>Context</h3>
<p>Happening since I installed the new <code>@babel...</code> beta modules.</p>
<h3>Your Environment</h3>
<table>
<thead>
<tr>
<th>software</th>
<th>version(s)</th>
</tr>
</thead>
<tbody>
<tr>
<td>Babel</td>
<td>7.0.0-beta.32</td>
</tr>
<tr>
<td>node</td>
<td>8.9.1</td>
</tr>
<tr>
<td>npm</td>
<td>5.5.1</td>
</tr>
<tr>
<td>Operating System</td>
<td>Win 7 Pro</td>
</tr></tbody></table>
      
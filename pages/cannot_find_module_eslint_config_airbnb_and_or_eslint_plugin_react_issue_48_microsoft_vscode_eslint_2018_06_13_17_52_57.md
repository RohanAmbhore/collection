<a href="https://github.com/Microsoft/vscode-eslint/issues/48">https://github.com/Microsoft/vscode-eslint/issues/48</a><div id="articleHeader"><h1>              Cannot find module 'eslint-config-airbnb' and/or 'eslint-plugin-react'            #48    </h1></div>


  <div>
    
    <div>
        <a href="/Beatusvir" target="_blank">Beatusvir</a>  opened this Issue
        <relative-time>on Mar 10, 2016</relative-time>
        · 33 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-139696159">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I've been trying to solve this for a couple of days and well... I wouldn't be asking if I fixed it <g-emoji>😄</g-emoji>.</p>
<blockquote>
<p>Cannot read config package: eslint-config-airbnb Error: Cannot find module 'eslint-config-airbnb' Referenced from: long_path.eslintrc</p>
<p>Cannot read config package: eslint-plugin-react Error: Cannot find module 'eslint-plugin-react' Referenced from: long_path.eslintrc</p>
</blockquote>
<p>I deleted every package from global (except for webpack and webpack-dev-server).</p>
<p>I ran <code>npm i eslint eslint-plugin-react eslint-config-airbnb babel-eslint -D</code> and all of them appear in <code>node_modules</code> and <code>package.json</code>.</p>
<p>If I run <code>node_modules\.bin\eslint file_name.jsx</code> the command works just fine, using both the plugin and the config.</p>
<p>packages.json</p>
<pre><code>"devDependencies": {
    "babel-core": "^6.6.5",
    "babel-eslint": "^5.0.0",
    "babel-loader": "^6.2.4",
    "babel-preset-es2015": "^6.6.0",
    "babel-preset-react": "^6.5.0",
    "chai": "^3.5.0",
    "chai-immutable": "^1.5.3",
    "eslint": "^2.3.0",
    "eslint-config-airbnb": "^6.1.0",
    "eslint-plugin-react": "^4.2.1",
    "file-loader": "^0.8.5",
    "jsdom": "^8.1.0",
    "mocha": "^2.4.5",
    "path": "^0.12.7",
    "react-hot-loader": "^1.3.0",
    "url-loader": "^0.5.7",
    "webpack": "^1.12.14",
    "webpack-dev-server": "^1.14.1"
  },
</code></pre>
<p>.eslintrc</p>
<pre><code>"parser": "babel-eslint",
  "plugins": ["react"],
  "ecmaFeatures": {
    "jsx": true
  },
  "env": {
    "browser": true,
    "node": true
  },
  "extends": "airbnb",
</code></pre>
<p>Any tips on debugging this?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-197497008">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Quitting VSCode and opening it again fixed this issue for me.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-197529494">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>No luck yet, ended up removing both <code>"plugins": ["react"]</code> and <code>"extends": "airbnb"</code></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-210355462">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>It seems vscode-eslint only  find node_modules from project root. So if your dir like <code>project/admin/</code>, it will not find <code>project/admin/node_modules/eslint-plugin-react</code>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-210459721">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hmm.. I didn't test that. I'll try that asap! Thanks <a href="https://github.com/ustccjw" target="_blank">@ustccjw</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-211380712">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>This configuration makes the language server running eslint crash. Need to find out why:</p>
<pre><code>channel closed: Error: channel closed
    at ChildProcess.target.send (internal/child_process.js:509:16)
    at IPCMessageWriter.write (C:\Users\dirkb\.vscode\extensions\dbaeumer.vscode-eslint-0.10.14\node_modules\vscode-languageclient\node_modules\vscode-jsonrpc\lib\messageWriter.js:34:22)
    at Object.connection.sendNotification (C:\Users\dirkb\.vscode\extensions\dbaeumer.vscode-eslint-0.10.14\node_modules\vscode-languageclient\node_modules\vscode-jsonrpc\lib\main.js:211:27)
    at Object.result.didChangeConfiguration (C:\Users\dirkb\.vscode\extensions\dbaeumer.vscode-eslint-0.10.14\node_modules\vscode-languageclient\lib\main.js:56:71)
    at LanguageClient.onDidChangeConfiguration (C:\Users\dirkb\.vscode\extensions\dbaeumer.vscode-eslint-0.10.14\node_modules\vscode-languageclient\lib\main.js:501:28)
    at LanguageClient.&lt;anonymous&gt; (C:\Users\dirkb\.vscode\extensions\dbaeumer.vscode-eslint-0.10.14\node_modules\vscode-languageclient\lib\main.js:487:81)
    at e.invoke (c:\Program Files (x86)\Microsoft VS Code\resources\app\out\vs\workbench\node\pluginHostProcess.js:7:14035)
    at e.fire (c:\Program Files (x86)\Microsoft VS Code\resources\app\out\vs\workbench\node\pluginHostProcess.js:7:15488)
    at e._acceptConfigurationChanged (c:\Program Files (x86)\Microsoft VS Code\resources\app\out\vs\workbench\node\pluginHostProcess.js:15:18102)
    at t.e.handle (c:\Program Files (x86)\Microsoft VS Code\resources\app\out\vs\workbench\node\pluginHostProcess.js:15:12835)
</code></pre>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-211393801">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Actual it looks like the process is not crashing. Looks like babel eslint calls process.exit() :-(</p>
<p>I also noticed that I receive quite some npm install errors when installing the provided config using npm version 2.14.12.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-211407310">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Here is what I see on npm install</p>
<pre><code>npm WARN package.json name@ No description
npm WARN package.json name@ No repository field.
npm WARN package.json name@ No README data
npm WARN package.json name@ No license field.
npm WARN peerDependencies The peer dependency eslint@&lt;2.3.0 included from babel-eslint will no
npm WARN peerDependencies longer be automatically installed to fulfill the peerDependency
npm WARN peerDependencies in npm 3+. Your application will need to depend on it explicitly.
npm WARN peerDependencies The peer dependency react@&gt;=0.11.0 || ^0.14.0-rc included from react-hot-api will no
npm WARN peerDependencies longer be automatically installed to fulfill the peerDependency
npm WARN peerDependencies in npm 3+. Your application will need to depend on it explicitly.
npm WARN deprecated jade@0.26.3: Jade has been renamed to pug, please install the latest version of pug instead of jade
npm WARN deprecated graceful-fs@2.0.3: graceful-fs version 3 and before will fail on newer node releases. Please update to graceful-fs@^4.0.0 as soon as possible.
npm WARN optional dep failed, continuing fsevents@1.0.11
npm ERR! Windows_NT 10.0.14322
npm ERR! argv "C:\\Program Files\\nodejs\\node.exe" "C:\\Program Files\\nodejs\\node_modules\\npm\\bin\\npm-cli.js" "install"
npm ERR! node v4.2.6
npm ERR! npm  v2.14.12
npm ERR! code EPEERINVALID

npm ERR! peerinvalid The package eslint@2.8.0 does not satisfy its siblings' peerDependencies requirements!
npm ERR! peerinvalid Peer eslint-config-airbnb@6.2.0 wants eslint@^2.4.0
npm ERR! peerinvalid Peer babel-eslint@5.0.4 wants eslint@&lt;2.3.0

npm ERR! Please include the following file with any support request:
npm ERR!     P:\mseng\VSCode\Playgrounds\linters\npm-debug.log
</code></pre>
<p><a href="https://github.com/Beatusvir" target="_blank">@Beatusvir</a> do you see the same or does this install for you without problems.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-214569011">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ustccjw" target="_blank">@ustccjw</a> I'm experiencing a similar issue.  I have multiple node projects inside of a root directory, each with their own npm_modules folder.  Have you seen any solutions to the this use case?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-215012884">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Same problem.</p>
<p>package.json</p>
<div><pre>{
  "devDependencies": {
    "babel-core": "^6.7.7",
    "babel-eslint": "^6.0.4",
    "babel-loader": "^6.2.4",
    "babel-preset-react": "^6.5.0",
    "eslint": "^2.8.0",
    "eslint-loader": "^1.3.0",
    "eslint-plugin-react": "^5.0.1",
    "html-webpack-plugin": "^2.16.0",
    "webpack": "^1.13.0",
    "webpack-dev-server": "^1.14.1"
  }
}</pre></div>
<p>.eslintrc</p>
<div><pre>{"parser": "babel-eslint",
  "plugins": ["react"],
  "ecmaFeatures": {
    "jsx": true
  },
  "env": {
    "browser": true,
    "node": true
  },
    "extends": ["eslint:recommended", "plugin:react/recommended"]
}</pre></div>
<p>file structure</p>
<pre><code>project
│   README.md
│   index.html    
├───app
│   │   index.html
│   │   index.js
│   │   ...
└───node_modules
    │   ...
</code></pre>
<p>So I only have one node_modules folder and it's in the root dir.<br />
eslint via command line works fine on /app/index.js<br />
I just get the error in VSCode<br />
I also get it if I don't include <code>babel-eslint</code></p>
<p>The only error I get doing <code>npm install</code>  is about fsevent, which is only for OS X, I think.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-217081933">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Can everything related to eslint be installed globally?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-217141933">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/yudhir" target="_blank">@yudhir</a> Yeah I believe, the problem is when you need to customize your settings per project basis, which you will sooner than later, hence something like eslint plugins, configs and extensions are usually installed locally and eslint globally.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-217186526">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>These are my dev dependencies if it helps</p>
<pre><code> "devDependencies": {
    "babel-eslint": "^6.0.4",
    "babel-preset-es2015": "^6.6.0",
    "babel-preset-react": "^6.5.0",
    "babelify": "^7.3.0",
    "browserify": "^13.0.0",
    "eslint": "^2.9.0",
    "eslint-config-airbnb": "^8.0.0",
    "eslint-plugin-import": "^1.6.1",
    "eslint-plugin-jsx-a11y": "^1.0.4",
    "eslint-plugin-react": "^5.0.1",
    "gulp": "^3.9.1",
    "gulp-uglify": "^1.5.3",
    "vinyl-source-stream": "^1.1.0",
    "watchify": "^3.7.0"
  },
</code></pre>
<p>eslintrc</p>
<pre><code>{
  "plugins": [
    "react"
  ],
  "env": {
    "browser": true,
    "node": true
  },
  "extends": "airbnb",
  "rules": {
    "no-console": "off",
    "react/jsx-closing-bracket-location": [
      1,
      "after-props"
    ],
    "padded-blocks": "off",
    "indent": "off"
  }
}
</code></pre>
<p>I have only recently begin developing on the web and loved that it is getting organized . I configured vs code with Eslint , Typings ,Task runner etc <a href="https://code.visualstudio.com/docs/runtimes/nodejs#_extensions" target="_blank">Docs</a><br />
I have eslint  installed it globally ,locally and the vsCode Extension as well. I came to the interweb seeing the same error but got eventually solved.</p>
<p>Random idea on multiple Project : have something change the single  eslintrc , to your configuration when running that part of project. (gulp , webpack maybe)</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-221863990">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/malchak" target="_blank">@malchak</a> the multiple project problem is discussed here: <a href="https://github.com/Microsoft/vscode-eslint/issues/32" target="_blank">#32</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-221866897">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Running the configuration in a terminal provided in comment <a href="https://github.com/Microsoft/vscode-eslint/issues/48#issue-139696159" target="_blank">#48 (comment)</a> results in:</p>
<pre><code>Error: Cannot find module 'estraverse-fb'
    at Function.Module._resolveFilename (module.js:339:15)
    at Function.Module._load (module.js:290:25)
    at Module.require (module.js:367:17)
    at monkeypatch (P:\mseng\VSCode\Playgrounds\linters\node_modules\babel-eslint\index.js:59:32)
    at Object.exports.parse (P:\mseng\VSCode\Playgrounds\linters\node_modules\babel-eslint\index.js:385:5)
    at parse (P:\mseng\VSCode\Playgrounds\linters\node_modules\eslint\lib\eslint.js:609:27)
    at EventEmitter.module.exports.api.verify (P:\mseng\VSCode\Playgrounds\linters\node_modules\eslint\lib\eslint.js:749:19)
    at processText (P:\mseng\VSCode\Playgrounds\linters\node_modules\eslint\lib\cli-engine.js:257:31)
    at processFile (P:\mseng\VSCode\Playgrounds\linters\node_modules\eslint\lib\cli-engine.js:292:18)
    at executeOnFile (P:\mseng\VSCode\Playgrounds\linters\node_modules\eslint\lib\cli-engine.js:676:23)
</code></pre>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-221869702">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>The process.exit happens in babel-eslint\index.js#388.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-221883290">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Looks like that if you use eslint &gt; 2.x you need babel-eslint &gt; 6. See <a href="https://github.com/babel/babel-eslint" target="_blank">https://github.com/babel/babel-eslint</a> which is not the case in the dependencies listed in comment <a href="https://github.com/Microsoft/vscode-eslint/issues/48#issue-139696159" target="_blank">#48 (comment)</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-221884230">

    
<div>
  

    
    
      Member
    



  <h3>

    <strong>
      

  <a href="/dbaeumer" target="_blank">dbaeumer</a>
  

    </strong>

    commented

    <a href="#issuecomment-221884230" target="_blank"><relative-time>on May 26, 2016</relative-time></a>


    
      <include-fragment>
            
  •


  

      <summary>
        <div>
          
              edited
          
          
        </div>
      </summary>

    
  

      </include-fragment>
    
  </h3>



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Setting up the right dependencies makes this work. However ESLint should detect this and handle this more gracefully. Ending in this wired error is not user friendly</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-221884772">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Thanks <a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a> I'm gonna try it right now</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  





</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-226438711">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>close + open window solves it for me.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-241620958">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Have this issue also - VC v1.4, plugin v0.10.18.</p>
<p>Running local eslint from terminal works correctly:</p>
<p><code>./node_modules/eslint/bin/eslint.js src/js/game/game.js</code></p>
<p>I do not have eslint installed globally.</p>
<p>Visual Studio Code reports this error: "Cannot find module 'eslint-config-airbnb' Referenced from: /Users/Nanda/Work/games/glitchspace/.eslintrc.json"</p>
<p>I've tried restarting Visual Studio code and completely wiping then re-installing node_modules. No luck. Dependencies:</p>
<pre><code>"devDependencies": {
    "eslint": "^3.3.1",
    "eslint-config-airbnb": "^10.0.1",
    "eslint-plugin-import": "^1.14.0",
    "eslint-plugin-jsx-a11y": "^2.1.0",
    "eslint-plugin-react": "^6.1.2",
    "gulp": "3.9.1",
    "gulp-buffer": "0.0.2",
    "gulp-concat-css": "2.3.0",
    "gulp-livereload": "3.8.1",
    "gulp-rename": "1.2.2",
    "gulp-sourcemaps": "1.6.0",
    "gulp-uglify": "1.5.4",
    "gulp-util": "3.0.7",
    "gulp-zip": "3.2.0",
    "handlebars": "4.0.5",
    "rollup-stream": "1.11.0",
    "vinyl-buffer": "1.0.0",
    "vinyl-source-stream": "1.1.0"
  }
</code></pre>
<p>.eslintrc.json:</p>
<pre><code>{
    "extends": "airbnb"
}
</code></pre>
<p>Any ideas?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-266180356">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm having a similar.  Here's my .eslintrc which is in the root folder of my project:</p>
<pre><code>{
  "extends": [
    "../shared_configuration/shared_linters/eslintrc"
  ]
}
</code></pre>
<p>The <code>shared_linters</code> folder contains its own <code>node_modules</code> with all of the eslint plugin modules.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-266181241">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Setting the <code>eslint.nodePath</code> setting to the absolute path of the eslint module within  <code>shared_linters</code> and that fixed it for me.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-293063253">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Keeping as feature request due to <a href="https://github.com/Microsoft/vscode-eslint/issues/48#issuecomment-221884230" target="_blank">#48 (comment)</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-296528001">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Sounds a bit like <a href="https://github.com/walmartlabs/eslint-config-defaults/issues/38" target="_blank">walmartlabs/eslint-config-defaults#38</a>. I think I have the same problem. I have eslint installed globsally and locally in my project. eslint seems to work only with the local instalation, e.g.</p>
<p>.\node_modules.bin\eslint --c jsconfig.eslintrc.yml src</p>
<p>calling it globally you will get:</p>
<blockquote>
<p>eslint --c jsconfig.eslintrc.yml src<br />
Cannot find module 'eslint-config-walmart/rules/eslint/node/on'<br />
Referenced from: C:\Users\micha\Sources\apps\3delectron\jsconfig.eslintrc.yml<br />
Error: Cannot find module 'eslint-config-walmart/rules/eslint/node/on'<br />
Referenced from: C:\Users\micha\Sources\apps\3delectron\jsconfig.eslintrc.yml<br />
at ModuleResolver.resolve (C:\Users\micha\AppData\Roaming\npm\node_modules\esl</p>
</blockquote>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-300747926">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/merdmann" target="_blank">@merdmann</a> ESlint npm module requires itself and all plugins either being installed locally or globally. Mixing doesn't work.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-312357439">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>You do not need to install everything globally. Check this:</p>
<p><code>npm i -g eslint-config-airbnb-standard</code><br />
<code>eslint -v</code></p>
<p>Here is the <a href="https://medium.com/@doasync/eslint-with-airbnb-standard-js-sublime-text-965a1db58793" target="_blank">guide</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-320239907">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/doasync" target="_blank">@doasync</a> this looks to me like both eslint and eslint-config-airbnb-standard are installed globally. Am I missing something ?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-320512336">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a> No, just install <code>eslint-config-airbnb-standard</code>, no need for <code>eslint</code> itself, it's bundled inside with all the plugins. And when you run <code>eslint -v</code> after installing the module, you are using that featured version from it. It's convenient in some situations.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-320619356">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>No, this will not work for the eslint extension since it doesn't shell out to eslint on the terminal. For performance reasons it loads the eslint npm module directly which it will not find since it is buried into <code>eslint-config-airbnb-standard</code></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-320619624">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>So for this setup you need to install both  <code>eslint-config-airbnb-standard</code> and <code>eslint</code> either globally or locally</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-334107366">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I was facing the same issue,<br />
probably because of eslint installation, eslint was installed globally on my system and all dependencies were installed as dev-dependency. so what I did, simply removed the eslint from global<br />
<code>npm uninstall -g eslint</code><br />
and install eslint locally<br />
<code>npm i eslint --save-dev</code></p>
<p>then run this(mac or Linux)<br />
<code>./node_modules/.bin/eslint --init</code></p>
<p>for windows<br />
<code>.\node_modules\.bin\eslint --init</code></p>
<p>hope this will fix your problem</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-334688103">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/anks333" target="_blank">@anks333</a> ESLint in general (the command line version as well) requires that ESLint and all extension are either installed globally or locally. You can't mix the installation scope.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-336195103">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a> Yes, you are right. That's why I created only one package for Airbnb preset <a href="https://www.npmjs.com/package/eslint-config-airbnb-bundle" target="_blank">eslint-config-airbnb-bundle</a>, which can be installed globally or locally. You will get <code>eslint</code> command at once and it will support Airbnb config by default.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>










        </div>


        <div>
              
<div>
  

    
      



      <div>
        
          <div>
  


  
  <div>

    

    

        <p>
    
    
        Attach files by dragging & dropping,
        selecting them, or pasting
        from the clipboard.
    
    
    
    
    
    
    
    
    
  </p>


    
  </div>

  

  


  
</div>

          
      </div>

</div>


        </div>
      </div>

    </div>
    
  
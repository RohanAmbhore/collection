<a href="https://github.com/Microsoft/vscode-eslint/issues/71">https://github.com/Microsoft/vscode-eslint/issues/71</a><div id="articleHeader"><h1>              Failed to load plugin react: Cannot find module 'eslint-plugin-react' every time I open a .js file            #71    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/dbaeumer" target="_blank">dbaeumer</a>  opened this Issue
        <relative-time>on Apr 24, 2016</relative-time>
        · 63 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-150589192">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><em>From <a href="https://github.com/ddieppa" target="_blank">@ddieppa</a> on April 22, 2016 19:12</em></p>
<ul>
<li>VSCode Version:<br />
Version 1.0.0<br />
Commit fa6d0f03813dfb9df4589c30121e9fcffa8a8ec8<br />
Date 2016-04-13T14:08:36.599Z<br />
Shell 0.35.6<br />
Renderer 45.0.2454.85<br />
Node 4.1.1</li>
<li>OS Version: windows 8.1 Pro</li>
</ul>
<p>Failed to load plugin react: Cannot find module 'eslint-plugin-react' every time I open a .js file, not even related with any react development</p>
<p>Steps to Reproduce:</p>
<ol>
<li>right click on any .js file and open with VS Code</li>
<li>wait a few seconds and the error appears</li>
</ol>
<p><a href="https://cloud.githubusercontent.com/assets/10607192/14752291/78dc4182-089c-11e6-82cc-7d713d11e9e4.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/10607192/14752291/78dc4182-089c-11e6-82cc-7d713d11e9e4.png" alt="image" /></div></a></p>
<p><em>Copied from original issue: <a href="https://github.com/Microsoft/vscode/issues/5667" target="_blank">Microsoft/vscode#5667</a></em></p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  


          

          

  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-213815968">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/ddieppa" target="_blank">@ddieppa</a> do you have the eslint extension installed? Looks like the extension can't load the react plugin?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-213815972">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><em>From <a href="https://github.com/ddieppa" target="_blank">@ddieppa</a> on April 22, 2016 19:32</em></p>
<p>that's my point, I just installed VS Code 1.0 from scratch, and installed eslint plugin for VS Code, but I don't have to install the eslint-plugin-react, I am just trying to open a .js file, not working on any react project or anything related to react</p>
<p>this is what I have globally installed in my pc:<br />
<a href="https://cloud.githubusercontent.com/assets/10607192/14752769/34467d32-089f-11e6-8a6d-4610a3faafb3.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/10607192/14752769/34467d32-089f-11e6-8a6d-4610a3faafb3.png" alt="image" /></div></a></p>
<p>and this are my installed extension in VS Code:<br />
<a href="https://cloud.githubusercontent.com/assets/10607192/14752800/5e868d1c-089f-11e6-8ba8-cc85d7ef8472.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/10607192/14752800/5e868d1c-089f-11e6-8ba8-cc85d7ef8472.png" alt="image" /></div></a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-218244381">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>can vscode check for eslint inside node_modules of current project instead of looking for global eslint?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-218286281">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a> Just ran into similar issue.<br />
My case is slightly different from yours because I am working in React - however, I was getting the same error-toast for "eslint-plugin-react" on every JS file (<em>including config files like webpack.config.js</em>)</p>
<p>I was using the eslint file from Dan Abramov's popular react hot reloader boilerplate.<br />
My issue ended up being that my .eslintrc file had non-es6 flags (JSX), which was causing the error.</p>
<p>See here for notes on migrating to Eslint2.x API: <a href="http://eslint.org/docs/user-guide/migrating-to-2.0.0" target="_blank">http://eslint.org/docs/user-guide/migrating-to-2.0.0</a></p>
<p><strong>[FAILING]</strong> My old .eslintrc file that was making the error:<br />
<code>{ "ecmaFeatures": { "jsx": true, "modules": true }, "env": { "browser": true, "node": true }, "parser": "babel-eslint", "rules": { "quotes": [2, "single"], "strict": [2, "never"], "react/jsx-uses-react": 2, "react/jsx-uses-vars": 2, "react/react-in-jsx-scope": 2 }, "plugins": [ "react" ] }</code></p>
<p><strong>[WORKING]</strong> My new .eslintrc file with working linting / no recurring "eslint-plugin-react" error:<br />
<code>{ "parserOptions": { "ecmaVersion": 6, "sourceType": "module", "ecmaFeatures": { "jsx": true }, "plugins": [ "react" ], "extends": ["eslint:recommended", "plugin:react/recommended"] } }</code></p>
<p>UPDATE: In case you're wondering where the "extends" key comes from, check the eslint-plugin-react NPM page <a href="here" target="_blank">https://www.npmjs.com/package/eslint-plugin-react</a> That's also the page that made me realize my ESLINT config was deprecated.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-221857934">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>@sibeliusseraphini eslint does prefer eslint installed in the workspace folder over a global installed eslint</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-221861281">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/ddieppa" target="_blank">@ddieppa</a> to my understanding your workspace has a .eslint config file requiring the react plugin but that is not installed, neither globally nor locally.</p>
<p>I tested the react plugin with the latest eslint extension and it works for me using a proper 2.0 config file. See screen shot.</p>
<p><a href="https://cloud.githubusercontent.com/assets/1931590/15575045/1ec802a6-2351-11e6-8d9f-ba33c214f94c.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/1931590/15575045/1ec802a6-2351-11e6-8d9f-ba33c214f94c.png" alt="capture" /></div></a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-221862756">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/alechp" target="_blank">@alechp</a> thanks for the information. The ESLint extension uses the eslint API under the cover. So the extension relies on the eslint API to complain about incorrect eslint config files. There is little I can do on my end without reimplementation.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-221863208">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Any objection to close this issue. react plugin is working in general. What is on the plan (as soon as VS Code provides API for it) is to allow to disable the plugin in these cases by clicking a corresponding action in the message.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-222148524">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a> I think I mentioned before, I just open a .js file, not even a project or a folder only a js file, and I got this error, I don't work with react, and I don't have any .eslintrc.json file.<br />
I also have Atom installed in my PC, is there any possibility that Atom installed some sort of global .eslintrc.json file and is conflicting with VS Code or something like that?<br />
<a href="https://cloud.githubusercontent.com/assets/10607192/15609549/9ec513f2-23ee-11e6-8fdb-8f67f34decc0.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/10607192/15609549/9ec513f2-23ee-11e6-8fdb-8f67f34decc0.png" alt="vscode_eslint" /></div></a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-222624654">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/ddieppa" target="_blank">@ddieppa</a> what is happening is that the ESLint plugin is installed and therefore tries to lint the js file. What we are working on this to not lint if no ESLint configuration can be found (dups <a href="https://github.com/Microsoft/vscode-eslint/issues/39" target="_blank">#39</a>) and to offer you a button Disable ESLint if a configuration is found and you still want to disable it.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-227636059">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>This has started happening for me today. The message constantly pops up. I dismiss it then start typing and it pops up again.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-227689505">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/craigsh" target="_blank">@craigsh</a> which version of the plugin are you using?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-227693514">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/craigsh" target="_blank">@craigsh</a> I tried to reproduce this but I can't. How do you dismiss the dialog ?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-227854407">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a> I installed it in VS Code using ext install eslint - it reports the version as 0.10.17</p>
<p>I have just tried it again and get the same result. Opening a .js file results in the popup:</p>
<p>Error: Failed to load plugin react: Cannot find module 'eslint-plugin-react'.</p>
<p>I click the Close button to dismiss the error. As soon as I make a change to my code the error pops up again (as it's obviously trying to lint my code).</p>
<p>I have eslint installed using npm install --save-dev and it reports version 2.13.1</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-227855090">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a> Also, I tried installing eslint-plugin-react to see whether that would fix things but it's had no effect. (Note, I'm not on a react project)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-227944268">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I started from this page <a href="https://code.visualstudio.com/docs/languages/javascript" target="_blank">https://code.visualstudio.com/docs/languages/javascript</a>, it told me to install eslint globally, then I had the same issue that the vscode cannot find eslint-plugin-react.</p>
<p>so I uninstalled the global eslint and install it in the project directory, everything just OK now</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-227953356">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/binbinfrog" target="_blank">@binbinfrog</a> Thanks, I've managed to get it to work now by fiddling with various installs and config files.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-227977961">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/craigsh" target="_blank">@craigsh</a> good to hear you got it to work. An additional note: If eslint is installed globally, it can't load locally installed plugins. This is a limitation in eslint, which the vscode-eslint extension should handle better (not show the message again).</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-228074515">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>so is there any defined workaround? because I uninstalled eslint from global, not the VSCode plugin and now I am getting this error:<br />
<a href="https://cloud.githubusercontent.com/assets/10607192/16307476/62968a68-392f-11e6-9081-dcb18ed82e24.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/10607192/16307476/62968a68-392f-11e6-9081-dcb18ed82e24.png" alt="2016-06-23 10_24_57-eslint-error" /></div></a><br />
I think this is the expected error.<br />
so what I did was install eslint locally (as a dev dependency)<br />
<code>npm install eslint --save-dev</code><br />
then I started getting same error as before:<br />
<a href="https://cloud.githubusercontent.com/assets/10607192/16307633/02025d98-3930-11e6-8ecb-808187795ee8.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/10607192/16307633/02025d98-3930-11e6-8ecb-808187795ee8.png" alt="2016-06-23 10_47_12-windows powershell admin" /></div></a><br />
<a href="https://github.com/craigsh" target="_blank">@craigsh</a> <a href="https://github.com/binbinfrog" target="_blank">@binbinfrog</a> what are the steps to avoid this?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-228151890">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/ddieppa" target="_blank">@ddieppa</a> My current installation is working. In the end I installed the following globally:</p>
<p>eslint<br />
eslint-plugin-react<br />
babel-eslint</p>
<p>I also have a .eslintrc in my project and had to remove the global .eslintrc file.</p>
<p>Basically trial and error to get it working. YMMV :)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-228710894">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/ddieppa" target="_blank">@ddieppa</a> eslint and all its plugins it loads must either all be installed globally or all locally. Mixing it doesn't work in eslint itself (e.g. has nothing to do with the eslint extension).</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-235899772">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <blockquote>
<p>eslint<br />
eslint-plugin-react<br />
babel-eslint<br />
<strong>eslint-config-defaults</strong></p>
</blockquote>
<p><code>npm install -g eslint eslint-plugin-react babel-eslint eslint-config-defaults</code></p>
<p><a href="https://github.com/craigsh" target="_blank">@craigsh</a> thanks for the tip, my configuration needed one more package.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-238166214">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I am still having this issue; here some more details:</p>
<p><a href="https://cloud.githubusercontent.com/assets/6423261/17472984/e0f8e790-5d45-11e6-8939-0ee75100d5ec.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/6423261/17472984/e0f8e790-5d45-11e6-8939-0ee75100d5ec.png"  alt="screen shot 2016-08-08 at 08 53 01" /></div></a></p>
<p><a href="https://cloud.githubusercontent.com/assets/6423261/17472991/e6a580b8-5d45-11e6-8fd0-c4f39e92ce36.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/6423261/17472991/e6a580b8-5d45-11e6-8fd0-c4f39e92ce36.png"  alt="screen shot 2016-08-08 at 08 54 39" /></div></a></p>
<p><a href="https://cloud.githubusercontent.com/assets/6423261/17472993/ebc6520c-5d45-11e6-99aa-8d7d684ffd03.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/6423261/17472993/ebc6520c-5d45-11e6-99aa-8d7d684ffd03.png"  alt="screen shot 2016-08-08 at 08 55 00" /></div></a></p>
<p>// cc <a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-239352566">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I get this same issue on this repo that has no eslint or reference to eslint:</p>
<p><a href="https://github.com/justsayno/webpack-html-sass-starter" target="_blank">https://github.com/justsayno/webpack-html-sass-starter</a></p>
<p>Quite frustrating as I use it heavily for JSX work I do but when not doing JSX and not using eslint it annoys me all the time about eslint plugins.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-239658084">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Im having this same issue..</p>
<p>fresh install of VScode 1.4.0<br />
installed extension<br />
created a folder and opened it<br />
added a main.js file, put a function in it..<br />
npm init<br />
installed eslint locally (npm i eslint)</p>
<p>before I even create an .eslintrc file.. any *.js file opened I get the constant error message "Failed to load plugin react: Cannot find module 'eslint-plugin-react'"</p>
<p>something somewhere is looking for that damn module, I just dont know what or where.</p>
<p>EDIT:<br />
I found the cause of my problem.</p>
<ul>
<li>The vscode workspace I was using was located in my 'documents' folder.</li>
<li>I also have visual studio installed and use it actively for other web development</li>
<li>visual studio had created an .eslintrc file in my user folder (above my document folder)</li>
<li>when eslint ran it was combining?|using the eslint file generated by visual studio which had references to the default eslint config and babeljs.</li>
</ul>
<p>I moved my vscode workspace folder to the root of the C drive and made sure it contained an eslintrc file and victory! the Visual studio created eslintrc file was ignored and all worked as expected. trump this one up to me not knowing enough about my development environment.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-240966322">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I managed to uninstall everything both locally and globally and reinstall everything both locally and globally again and finally it seems to work now; thanks.</p>
<p>it looks like it works if I have got "eslint-plugin-react" in "dependencies" in my package.json file</p>
<p><a href="https://cloud.githubusercontent.com/assets/6423261/17814976/1d6f74fe-662a-11e6-9040-696ab3277ddb.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/6423261/17814976/1d6f74fe-662a-11e6-9040-696ab3277ddb.png" alt="screen shot 2016-08-19 at 16 29 10" /></div></a></p>
<p>// cc <a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-241073774">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I was having the same issue, with the same cause as <a href="https://github.com/lukekentwell" target="_blank">@lukekentwell</a> (i.e., unbeknownst to me there was a <code>.eslintrc</code> file in my <code>%userprofile%</code> folder).<br />
<a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a>, I would suggest that you add this info to a FAQ or troubleshooting document. This problem seems like it would be very common for anyone that uses both Visual Studio and Visual Studio Code. I suspect many people may not bother to search the issues list on this GitHub project and will just assume your extension is defective, when in fact it is not.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-241842027">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><em>For posterity, since I spent a while figuring this out.</em></p>
<p>Globally installing plugins & configs referenced in the local <code>.eslintrc</code> eliminated the error, but was not a fix since global configs/plugins versions are project relative and would quickly go out of sync.</p>
<p><strong>Solution:</strong> <strong>File &gt; Open</strong> the directory containing the <code>node_modules</code> where <code>eslint</code> and the corresponding <code>eslint-plugin-*</code>/<code>eslint-config-*</code> were installed.</p>
<p>This behavior is incorrect for 2 reasons:</p>
<ol>
<li>This is neither how <code>eslint</code> nor <code>SublimeLinter-eslint</code> work, as both properly traverse up the directory tree for the nearest local <code>eslint</code> and corresponding <code>eslint-plugin-*</code> & <code>eslint-config-*</code>.</li>
<li>For most editors, file-level functionality (vs "project"-level like builds) is not dependent on the directory currently open in the current editor. For example, in my case, installs are at <code>project_root/web/node_modules</code>, yet all of the following fail:
<ol>
<li>Opening the file directly (i.e., <code>code project_root/web/foo/bar.js</code>)</li>
<li>Or, at the project root (i.e., File &gt; Open &gt; "project_root", which contains <code>project_root/web/node_modules</code>)</li>
<li>Open any non-project file directly</li>
</ol>
</li>
</ol>
<p>The current <code>vscode-eslint</code> functionality is disconcerting as I suspect it does not load the correct (most local in node_modules) configs/plugins, but instead always loads from <code>directory_root_open_in_vscode/node_modules</code>.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-242076534">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/CrabDude" target="_blank">@CrabDude</a> I changed the module resolution lookup (see <a href="https://github.com/Microsoft/vscode-languageserver-node/issues/77" target="_blank">Microsoft/vscode-languageserver-node#77</a>) which now correctly loads the module looking up the parent chain as well.</p>
<p>However the problem that a 'eslint' installation must be complete in terms of the configuration you use remains since it is the same behavior with eslint on the command line. So if for example eslint is installed globally and used by the eslint extension then all plugins used must be installed globally as well.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-242249275">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <blockquote>
<p>However the problem that a 'eslint' installation must be complete in terms of the configuration you use remains since it is the same behavior with eslint on the command line.</p>
</blockquote>
<p><a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a> IIUYouC, yup. Agreed; It's my understanding that <code>eslint</code> install & <code>eslint-plugin/config-*</code> locations are coupled, and <a href="https://github.com/Microsoft/vscode-languageserver-node/issues/77" target="_blank">the fix you referenced</a> will fix this by loading the nearest local install (which I believe is correct).</p>
<p>Resolution I believe should go something like:</p>
<p><code>$ code ./path/to/file/foo.js</code><br />
=&gt;</p>
<div><pre># pseudo-code bash/js
cd /absolute/path/to/file/

# load local config
eslint_config = eslint config nearest to /absolute/path/to/file/

# Only use local install if local config exists (local installs for a global config doesn't make sense)
eslint = eslint_config && `npm bin`/eslint

# Fall back to global config
eslint_config = eslint_config || global eslint config
if (!eslint_config) exit or use vscode-eslint built-in config(?)

# Fall back to global install
eslint = eslint || `npm bin -g`/eslint

# eslint should load eslint-config/plugin-* relative to itself</pre></div>
<p>While, instead <code>vscode-eslint</code> currently does:</p>
<pre><code>eslint = opened_folder ? opened_folder/node_modules/eslint : `npm bin -g`/eslint
if (!eslint) throw 'Failed to load eslint library'
</code></pre>
<p>EDIT: Minor edits above.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-243825807">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/JeffJacobson" target="_blank">@JeffJacobson</a> Thanks for the info. I was also facing this issue in vscode 1.4 and was very frustrated. Replaced the .eslintrc file in %userprofile% folder and the issue got resolved. I think vscode is using the .eslintrc file in %userprofile% folder instead of working directory. Please fix this.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-243875495">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/bdinesh" target="_blank">@bdinesh</a>, note that the <code>%userprofile%/.eslintrc</code> file will probably be recreated each time you start Visual Studio 2015. (At least that's what happens to me.) I'm not sure if its VS itself or one of the many extensions I have that's generating this file.</p>
<p>It's not a problem with this VS Code extension. The same thing happens if you run eslint from the command line with the VS generated <code>.eslintrc</code> in place.</p>
<pre><code>eslint **/*.js
</code></pre>
<pre><code>Oops! Something went wrong! :(                                                                                                                                                                   

ESLint couldn't find the plugin "eslint-plugin-react". This can happen for a couple different reasons:                                                                                           

1. If ESLint is installed globally, then make sure eslint-plugin-react is also installed globally. A globally-installed ESLint cannot find a locally-installed plugin.                           

2. If ESLint is installed locally, then it's likely that the plugin isn't installed correctly. Try reinstalling by running the following:                                                        

    npm i eslint-plugin-react@latest --save-dev                                                                                                                                                  

If you still can't figure out the problem, please stop by https://gitter.im/eslint/eslint to chat with the team.
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-247857496">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I think many are experiencing this problem due to having <strong>.eslintrc.json</strong> file located even outside of the project directory.</p>
<p>I just realized that I had <strong>.eslintrc.json</strong> file inside my home directory and it applied its rules on all the folders and files including Desktop where I keep my projects. Make sure to look for any <strong>.eslintrc.json</strong> outside your project directory and remove it.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-247943258">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>The eslint extension itself uses ESLint default .eslintrc* lookup behavior which basically looks up the parent chain for that file. I didn't find a way to disable this expect pointing to an explicit configuration file which is possible today using the eslint.options setting.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-248023849">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I have a project where on the root level I have my server code and the package.json containing the server dependencies. In a subdirectory I have the client code and the package.json containing the client dependencies. Both client and server have their own .eslintrc.json, and eslint as dev-dependency. Client also has dependency to eslint-plugin-react. If I open the root directory in vscode, I get the aforementioned error. If I move the client directory outside of the project, or if I open the client directory, I don't get the error.</p>
<p>I think <a href="https://github.com/CrabDude" target="_blank">@CrabDude</a> explained the problem correctly, i.e. vscode-eslint loads plugins from wrong path. It should search for the plugins from the nearest node_modules to the .eslintrc.json, up all the way up to the global node_modules.</p>
<p>ps. Atom seems to handle ESLint plugin loading correctly.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-248725050">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Having now worked on <a href="https://github.com/eslint/eslint/pull/7177" target="_blank">eslint/eslint#7177</a>, I now know <code>eslint</code>'s built-in plugin resolution works as follow:</p>

<p>So from an <code>eslint</code> perspective, it's odd that this bug exists because if filePath is being passed to eslint (via CLI or <code>CLIEngine</code>), the resolution should work automatically. <a href="https://github.com/Microsoft/vscode-languageserver-node/commit/fe5a303907e9307bef57170d9425aa51be3393e1" target="_blank">After</a> <a href="https://github.com/Microsoft/vscode-languageserver-node/commit/b65111a56c30270ae09ec270df139d71fa3de1c4" target="_blank">inspecting</a> <a href="https://github.com/Microsoft/vscode-languageserver-node/issues/89" target="_blank">the</a> <a href="https://github.com/Microsoft/vscode-languageserver-node/commit/9137afd050231abcdf46b729512b7457b47657f2" target="_blank">fixes</a>, it's apparent this issue exists b/c <code>vscode-eslint</code> implements its own package/module/<code>node_modules</code>/<code>eslint-plugin-*</code> resolution logic, which at first blush is concerning. However, I don't know the motivation for doing so; I suspect it's due to some VSCode plugin limitations or requirements (i.e., <code>vscode-eslint</code> does not have access to the whole filesystem, and instead must rely upon project / file contents).</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-249002028">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/CrabDude" target="_blank">@CrabDude</a> vscode-eslint doesn't implement its own resolution logic for eslint plugins. The only logic eslint has (through the language server) is to find the initial eslint npm module. This is basically done using node code (e.g. require.resolve('eslint')). Then I load this eslint npm module and from then on delegate all plugin loading to the eslint CLIEngine loaded from that package.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>



    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-249092262">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a> That exactly is the problem. If the initial module is in the root of the project, eslint plugins that are located in subdirectories are not being loaded. For <a href="https://github.com/AtomLinter/linter-eslint" target="_blank">Atom </a> this is not an issue; therefore this is a bug in vscode-eslint.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-249181330">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/Kitanotori" target="_blank">@Kitanotori</a> interesting. Actually I delegate all the loading to the CLIEngine I get from ESLint. Assuming you have such a setup does eslint work from a terminal as expected (e.g. you call it from the sub directory).</p>
<p>When I experimented with ESLint I noticed that eslint and plugins need to be installed at the same level to make it work in a terminal. But may be something changed I need to catch up with.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-249200908">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Weird.. It seems that the problem has gone away.</p>
<p>EDIT: Never mind, tested with a different project. I realized that the problem occurs if I don't have eslint installed at all in the root. If there is eslint at the root, the plugins from subdirectories seem to be loaded, but if there is no eslint at the root, eslint from subdirectories are not being loaded.</p>
<p>So, the problem is that vscode-eslint fails to load eslint if it is not in the root or global directory. It should be able to load eslint also from subdirectory. The plugin loading does not seem to be an issue if there is no eslint installed globally.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    


    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-249498894">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>The problem with eslint not loaded from a sub directory is know.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-249809008">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Thanks to <a href="https://github.com/JeffJacobson" target="_blank">@JeffJacobson</a> the problem actually was because we installed Eslint ext in VS code</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-250706277">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I'm also getting "Failed to load plugin react: Cannot find module 'eslint-plugin-react'" with my Angular 2 project. I have the ESLint extension installed. Have never touched or done anything with React. Every time I enter a .js file I get the popup. Driving me crazy. Haha. Any help?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-250821148">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>@charlkie14  The main cause I've noticed for this is having a global .eslinrc in your user directory. Once I deleted that it went away. Now that I think about it this seems like fair enough behavior. IF you have a global eslint that references some modules you should have then installed globally. Remove that .eslinrc from the user folder and it goes away.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-251356021">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Alternatively you can disable ESLint via <code>"eslint.enable": false</code> in the workspace settings.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-251894845">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Thanks @justsayno and <a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a> for the advice and help. Much appreciated.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-251926363">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I too faced this issues few days back, and let me sum up the solutions, which I get from the above comments:</p>
<ul>
<li>Delete the global <code>.eslintrc</code> file present in your user directory, or</li>
<li>install plugins globally, or</li>
<li>last option disable ESLint via  <code>"eslint.enable": false</code>in <code>settings.json</code>file and start using jshint extension</li>
</ul>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-252018253">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/nivesh2" target="_blank">@nivesh2</a>, you can also edit (rather than delete) the <code>%userprofile%/.eslintrc</code> file. This is what I ended up doing to prevent Visual Studio 2015 from regenerating the file.</p>
<div><pre>{
    /* See all the pre-defined configs here: https://www.npmjs.com/package/eslint-config-defaults */

}</pre></div>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-252057591">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/JeffJacobson" target="_blank">@JeffJacobson</a> thanks, do you have any idea where the global <code>.eslintrc</code> file resides on Windows 10 system?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-252059195">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/nivesh2" target="_blank">@nivesh2</a> C:\Users{userName}.eslintrc for me</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-252059819">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>@justsayno nope, already looked on that path, nothing like .eslintrc there.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-252062564">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Perhaps your error is for one of the other stated reasons above then? The absence of that file for me stopped the error completely.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-252079334">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/nivesh2" target="_blank">@nivesh2</a> I don't have Windows 10, but in Windows 7 the path to the user profile folder is stored in the <code>%userprofile%</code> environment variable.</p>
<p>At the command prompt, try the following to change to that directory</p>
<div><pre>cd %userprofile%</pre></div>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-252080966">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Okay, done that but could find the file, anyways, will look more into it. But for now, installing plugins globally helped me solve the issue. Thanks!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-253038054">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Yeah this still happens regardless of the .eslint in the user directory. Just to clarify. It did go away for a while but I think ti was just because the project wasn't causing it. New project and its happening again.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-253517113">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>For me (windows 10), the issue turned out to be an <code>.eslintrc</code> file in my home directory (%userprofile%). As others have mentioned, it was likely due to Visual Studio 2015 putting the file there.  That file had references to the react presets.  This was an issue because my project's workspace was in a child directory under my user's home directory, so eslint's default config traversal picked it up. (<a href="http://eslint.org/docs/user-guide/configuring#using-configuration-files" target="_blank">http://eslint.org/docs/user-guide/configuring#using-configuration-files</a>).</p>
<p>I'm using an <code>.eslintrc.json</code> file in my project root to configure eslint locally, so added <code>"root": true</code>, which tells eslint to ignore any inherited parent config files. By doing that, eslint stopped trying to load react presets and no more errors from the extension manager in VSCode.<br />
<a href="http://eslint.org/docs/user-guide/configuring#configuration-cascading-and-hierarchy" target="_blank">http://eslint.org/docs/user-guide/configuring#configuration-cascading-and-hierarchy</a></p>
<p>Plugin is working great now, thank you for your work on it <a href="https://github.com/dbaeumer" target="_blank">@dbaeumer</a> !</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    


    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-253789826">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Let me see if I can add tracing which .eslintrc file is taken into consideration. This at least will help people to understand what is going on.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-254114923">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I met this problem<br />
But not find global .eslintrc file<br />
<a href="https://github.com/traktraktrugui" target="_blank">@traktraktrugui</a> use your solution solve the issue<br />
<a href="https://cloud.githubusercontent.com/assets/22698933/19426104/6892dbd6-946c-11e6-9395-1d6ea8eb3e47.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/22698933/19426104/6892dbd6-946c-11e6-9395-1d6ea8eb3e47.png" alt="qq" /></div></a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-258650069">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Guys, don't forget adding  "plugins": [ "react" ] to your .eslintrc.json</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-259657802">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Unfortunately ESLint doesn't offer any API to tell me which .eslintrc file is used (unstandable since it is a merge of many files). If this happens I now print the following to the output window instead of showing a flashing window message</p>
<pre><code>[Warn  - 11:37:57 AM] Failed to load plugin eslint-react: Cannot find module 'eslint-plugin-eslint-react'
Happend while validating p:\mseng\VSCode\Playgrounds\linters\lib\test.js
This can happen for a couple of reasons:
1. The plugin name is spelled incorrectly in an ESLint configuration file (e.g. .eslintrc).
2. If ESLint is installed globally, then make sure 'eslint-plugin-eslint-react' is installed globally as well.
3. If ESLint is installed locally, then 'eslint-plugin-eslint-react' isn't installed correctly.
</code></pre>
<p>Fixed in the upcoming 1.1.0 release</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-259661516">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Polished the message a little</p>
<pre><code>Failed to load plugin eslint-react: Cannot find module 'eslint-plugin-eslint-react'
Happend while validating p:\mseng\VSCode\Playgrounds\linters\lib\test.js
This can happen for a couple of reasons:
1. The plugin name is spelled incorrectly in an ESLint configuration file (e.g. .eslintrc).
2. If ESLint is installed globally, then make sure 'eslint-plugin-eslint-react' is installed globally as well.
3. If ESLint is installed locally, then 'eslint-plugin-eslint-react' isn't installed correctly.

Consider running eslint --debug p:\mseng\VSCode\Playgrounds\linters\lib\test.js from a terminal to obtain a trace about the configuration files used.
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    


    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-272981957">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I made the mistake of installing the config, but not the plugin. Ran around for a while, but now it's working.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-286136916">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>It seems that running the command line just as written may not always give the information you're trying to get. I'm guessing due to wrong working directory etc.</p>
<p>Had a case with the same react-plugin that was present in a config file in the user's home directory but when looking at the --debug output it did not list that .eslintrc file at all. For some reason it was picked up when running from within VSCode. As I tried to help troubleshooting this remote, it all looked good when looking at the output from the command line invocation, but after reading a few comments here we figured out the additional config file in the home directory, which did not show up in the debug output.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
      <div>
  <h3 id="event-1352820839">

    
      
    

    

        <img src="https://avatars0.githubusercontent.com/in/2406?s=60&v=4" width="16" height="16" alt="@vscodebot" />
  <a href="/apps/vscodebot" target="_blank">vscodebot</a>
  bot


        locked and limited conversation to collaborators


    <a href="#event-1352820839" target="_blank"><relative-time>on Nov 22, 2017</relative-time></a>

  </h3>
</div>



</div>








        </div>


        <div>
              
<div>
  

    
      



      <div>
        
          
<div>
  <div>
    <nav>
      Write
      Preview
    </nav>
  </div>
  <div>
    
    <p>This conversation has been locked and limited to collaborators.</p>
  </div>
</div>

      </div>

</div>


        </div>
      </div>

    </div>
    
  
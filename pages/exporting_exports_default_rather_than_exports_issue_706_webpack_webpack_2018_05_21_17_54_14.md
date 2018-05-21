<a href="https://github.com/webpack/webpack/issues/706">https://github.com/webpack/webpack/issues/706</a><div id="articleHeader"><h1>              exporting 'exports.default' rather than 'exports'            #706    </h1></div>


  <div>
    
    <div>
        <a href="/mhelvens" target="_blank">mhelvens</a>  opened this Issue
        <relative-time>on Jan 21, 2015</relative-time>
        · 17 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-54959322">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm writing a library with ES6 module notation. The main module exports only a default object:</p>
<pre><code>// defining MainObject
//...
export default MainObject;
</code></pre>
<p>Inside other ES6 modules, Webpack seems to handle this well, extracting the <code>exports.default</code> when needed. But when exporting my library to, e.g., UMD, the entire <code>exports</code> object is exported.</p>
<p>I'd like the option to export <code>exports.default</code> instead. Right now, my build-process fixes this with a simple search/replace operation on the Webpack output:</p>
<pre><code>.pipe(replace(
    'return __webpack_require__(0)',
    'return __webpack_require__(0).default'))
</code></pre>
<p>It works, but it's not ideal.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-70761824">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Webpack just uses standard <code>require</code> calls, but if you're using <code>6to5</code>, it wraps all <code>import</code> calls in logic to use <code>.default</code> and fall back to <code>exports</code>.</p>
<p>If you don't want a standard ES6 export for your entry point, perhaps you can have it do <code>module.export =</code> instead of using ES6 <code>export</code>? It's really all up to the transpiler, rather than webpack.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-71461351">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I don't think there <em>is</em> a standard export for ES6-to-ES5. Within ES6, there is special syntax to deal with an <code>exports</code> object, a default value or both. With AMD/CommonJS, you can only export a single value, so a choice has to be made.</p>
<p>The choice that Traceur makes (6to5 too, probably) is to send the whole <code>exports</code> object. This is sensible for ES6-to-ES6, since it contains all exported data, with <code>exports.default</code> being the default value. It can then be properly dissected on the import-side.</p>
<p>But when an ES5 entry-point is made from an ES6 module that <em>only</em> exports a default value, it makes sense for that value to be exported directly. Using old syntax inside an ES6 module doesn't seem like a nice solution when it should be done transparently. And while this may be solvable as a feature of the transpiler, general post-processing of the entry-point export value seems like a useful Webpack feature in any case.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-154220146">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I ran into this issue as well. I'm exposing a exported library with the <code>output.library</code> option. When I export the library like this, it works as expected:</p>
<div><pre>module.exports = Library;</pre></div>
<p>When I export the library like this, I get an exports object with a <code>default</code> key:</p>
<div><pre>export default Library;</pre></div>
<p>I believe this should become something like this:</p>
<div><pre>exports["default"] = Library;
module.exports = exports["default"];</pre></div>
<p>Instead I get the same code as <a href="https://github.com/mhelvens" target="_blank">@mhelvens</a> got:</p>
<div><pre>return __webpack_require__(0)</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-162987017">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Same issue: module is doing export default functionr() {}, using UMD feature of webpack does not work.</p>
<p>Did any of you guys solved this "the right way"?</p>
<p>I have trouble understanding what went bad here, export default function() {} when using webpack "libraryTarget" to umd I really think we should get the exported function, not default: function() {}</p>
<p>But maybe I miss some information</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-167908576">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Same issue!<br />
I had to fix it by using <code>module.exports = lib</code> instead of <code>export default lib</code> in the entry file for my code as suggested above.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-168767102">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>+1 Same issue, using Babel 6.3.15... though maybe this is an issue with Babel/my babel config.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-180429684">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>The problem lies in how webpack exports a library.</p>
<p>Babel adds <code>exports.__esModule = true</code> to each ES6 module. On importing a module Babel calls <code>_interopRequireDefault</code> to check for that property, if it sees it it imports <code>module.default</code>, otherwise just the module.</p>
<p>Webpack's library compiler simply strips out <code>__esModule</code> breaking babel's ability to correctly import the given source as a ES6 module.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-180432166">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>If you're exporting a <code>commonjs</code> library, a quick fix is to set <code>libraryTarget: 'commonjs2'</code> as this does not strip away the required <code>__esModule</code> attribute.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
      

  <div>
  <h3 id="ref-commit-b5600dc">
    
      
    
    
  <a href="/jeffbaumes" target="_blank">jeffbaumes</a> 


      added a commit
        to Kitware/candela
      that referenced
      this issue

    <a href="#ref-commit-b5600dc" target="_blank">
      <relative-time>on Apr 6, 2016</relative-time>
    </a>
  </h3>

  
</div>

  <div>
        <h3 id="ref-pullrequest-146071639">
      
        
      
        
  <a href="/jeffbaumes" target="_blank">jeffbaumes</a>
  

      referenced this issue
        in <strong>Kitware/candela</strong>
      <a href="#ref-pullrequest-146071639" target="_blank">
        <relative-time>on Apr 6, 2016</relative-time>
      </a>
    </h3>

  
    
        
      Merged
    



    
      <h4>
        <a href="/Kitware/candela/pull/90" target="_blank">
          Fix export for ES5
          #90
        </a>
      </h4>
    

    


  

</div>

  <div>
        <h3 id="ref-issue-155477267">
      
        
      
        
  <a href="/DeFuex" target="_blank">DeFuex</a>
  

      referenced this issue
        in <strong>conorhastings/react-syntax-highlighter</strong>
      <a href="#ref-issue-155477267" target="_blank">
        <relative-time>on May 18, 2016</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/conorhastings/react-syntax-highlighter/issues/10" target="_blank">
          Cannot read property 'exports' of undefined
          #10
        </a>
      </h4>
    

    


  

</div>

  <div>
        <h3 id="ref-pullrequest-163030657">
      
        
      
        
  <a href="/toddmazierski" target="_blank">toddmazierski</a>
  

      referenced this issue
        in <strong>pburtchaell/redux-promise-middleware</strong>
      <a href="#ref-pullrequest-163030657" target="_blank">
        <relative-time>on Jun 30, 2016</relative-time>
      </a>
    </h3>

  
    
        
      Merged
    



    
      <h4>
        <a href="/pburtchaell/redux-promise-middleware/pull/91" target="_blank">
          Add UMD build tasks
          #91
        </a>
      </h4>
    

    


  

</div>

  <div>
  <h3 id="ref-commit-f948c49">
    
      
    
    
  <a href="/pburtchaell" target="_blank">pburtchaell</a> 


      added a commit
        to pburtchaell/redux-promise-middleware
      that referenced
      this issue

    <a href="#ref-commit-f948c49" target="_blank">
      <relative-time>on Jul 6, 2016</relative-time>
    </a>
  </h3>

  
</div>




  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-237022586">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Changing to 'commonjs2' as suggested above works for me.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
      <div>
        <h3 id="ref-pullrequest-172631507">
      
        
      
        
  <a href="/alvath96" target="_blank">alvath96</a>
  

      referenced this issue
        in <strong>cermati/satpam</strong>
      <a href="#ref-pullrequest-172631507" target="_blank">
        <relative-time>on Aug 23, 2016</relative-time>
      </a>
    </h3>

  
    
        
      Merged
    



    
      <h4>
        <a href="/cermati/satpam/pull/30" target="_blank">
          Frontend
          #30
        </a>
      </h4>
    

    


  

</div>




  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-244275453">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Webpack <code>v2.1.0beta-14.0</code><br />
Can someone explain this to me. I am writing a library with <code>target: "node"</code> , <code>libraryTarget: "commonjs2"</code>  and <code>library: "jwt"</code>.</p>
<p>From within my <code>src/index.js</code> file, I have multiple exports:</p>
<div><pre>export { a, b, c};

export default (d) =&gt; "e";

export const f = "g";</pre></div>
<p>I consume this library in my project like:</p>
<div><pre>import jwt, { a, b, c, f } from "jwt";
</pre></div>
<p>However, <code>jwt</code> is set to the entire <code>module.exports</code> object rather than <code>module.exports["default"]</code>. Is this expected behavior or am I doing something wrong?</p>
<p>Note: I am not using Babel for any transpiling. This code is meant for <code>node &gt;= 6.4.0</code>, so it can't be a Babel issue.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-246489917">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/f0rr0" target="_blank">@f0rr0</a> Since you're not using babel you'll have to look at how Node V6 detects ES6 modules vs older <code>module.exports</code> modules. Understanding that Babel used <code>.__esModule</code> was what eventually led me to a solution.</p>
<p>This DRAFT spec <a href="https://github.com/nodejs/node-eps/blob/master/002-es6-modules.md#51-determining-if-source-is-an-es-module" target="_blank">https://github.com/nodejs/node-eps/blob/master/002-es6-modules.md#51-determining-if-source-is-an-es-module</a> suggests a parse goal field in <code>package.json</code>, but it's not immediately clear from that document whether or not it has been implemented.</p>
<p>Hope that points you into the right direction.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-247752210">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/skaapgif" target="_blank">@skaapgif</a> Thanks for the heads up! This was clarified at <a href="https://github.com/webpack/webpack/issues/2945" target="_blank">#2945</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-301066363">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/f0rr0" target="_blank">@f0rr0</a> <a href="https://github.com/skaapgif" target="_blank">@skaapgif</a> - did you try add-module-exports plugin from babel?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-322749863">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I've also faced this issue. I've written a library with Typescript + Babel + Wepack, and the <code>libraryTarget: 'umd'</code> exports an object with a <code>default</code> key, instead of my lib code.</p>
<p>Unfortunately the workarounds above did't work because:</p>
<ul>
<li>Typescript with target es2015+ allows only <code>export default x</code></li>
<li><code>add-module-exports</code> is useless when babel <code>modules: false</code> is set</li>
</ul>
<p>So, I had to come up with a different solution: adding a custom UMD wrapper with <a href="https://github.com/levp/wrapper-webpack-plugin" target="_blank">wrapper-webpack-plugin</a>. Just remove the <code>library*</code> options under <code>output</code> and add the plugin:</p>
<div><pre>const WrapperPlugin = require('wrapper-webpack-plugin');
module.exports = {
  //...
  plugins: [
    //...
    new WrapperPlugin({
      test: /\.js$/,
      header: ('(function umdWrapper(root, factory) {' +
        '  if(typeof exports === "object" && typeof module === "object")' +
        '    module.exports = factory().default;' +
        '  else if(typeof define === "function" && define.amd)' +
        '    define("NAME", [], function() { return factory().default; });' +
        '  else if(typeof exports === "object")' +
        '    exports["NAME"] = factory().default;' +
        '  else' +
        '    root["NAME"] = factory().default;' +
        '})(this, function() {' +
        'return ').replace(/NAME/g, 'MyAwesomeLib'), // this is the name of your lib
      footer: '\n})',
    }),
  ],
};</pre></div>
<p>(PS: The header code is almost entirely copied from the default Webpack UMD wrapper)</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-361923568">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Just for reference for anyone coming from a google search, Webpack 3 has an option called <a href="https://webpack.js.org/configuration/output/#output-libraryexport" target="_blank">libraryExport</a> that can be set to "default" which should hopefully fix this issue.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



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
    
  
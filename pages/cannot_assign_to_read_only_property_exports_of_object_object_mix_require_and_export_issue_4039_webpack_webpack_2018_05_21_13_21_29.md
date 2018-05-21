<a href="https://github.com/webpack/webpack/issues/4039">https://github.com/webpack/webpack/issues/4039</a><div id="articleHeader"><h1>              Cannot assign to read only property 'exports' of object '#&lt;Object&gt;' (mix require and export)            #4039    </h1></div>


  <div>
    
    <div>
        <a href="/DimitryDushkin" target="_blank">DimitryDushkin</a>  opened this Issue
        <relative-time>on Jan 19, 2017</relative-time>
        · 62 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-201799135">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          


<p><strong>Do you want to request a <em>feature</em> or report a <em>bug</em>?</strong><br />
bug</p>


<p><strong>What is the current behavior?</strong><br />
Module with code</p>
<div><pre>// 'a.js'
module.exports = { a: 'b' };

// b.js
const a = require('./a.js').a;

export default {
   aa: a
}</pre></div>
<p>Gives error:</p>
<pre><code>Cannot assign to read only property 'exports' of object '#&lt;Object&gt;'
</code></pre>
<p>Appeared after upgrade webpack 2.2.0.rc.6 -&gt; 2.2.0.</p>
<p>If 'harmony-module' is ES2015 module, then looks like it's now impossible to mix <code>require</code> and <code>export default</code> in single module. If it so, that's okay, but should be mentioned in docs.</p>
<p><strong>Please mention other relevant information such as the browser version, Node.js version, webpack version and Operating System.</strong><br />
MacOS 10.12.2<br />
node.js 6.9.2<br />
webpack 2.2</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  


          

          

  


  
<div>
      <div>
  <h3 id="event-928819603">

    
      
    

    

        
  <a href="/DimitryDushkin" target="_blank">DimitryDushkin</a>
  


      
changed the title from
Cannot assign to read only property 'exports' of object '#&lt;Object&gt;'
to
Cannot assign to read only property 'exports' of object '#&lt;Object&gt;' (mix require and export)


    <a href="#event-928819603" target="_blank"><relative-time>on Jan 19, 2017</relative-time></a>

  </h3>
</div>





  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-273804003">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>The code above is ok. You can mix <code>require</code> and <code>export</code>. You can't mix <code>import</code> and <code>module.exports</code>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-273805925">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/sokra" target="_blank">@sokra</a> probably in real code I had something more, that caused the issue. Now I've refactored this part to <code>import export</code> and it works fine.</p>
<p>I'll try check it in more clear example. For now I believe the issue can be closed.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-273890888">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>This issue was newly affecting me after instructing Babel to not transpile module syntax. As sokra described, it only occurred when trying to use CommonJS style <code>module.exports</code> inside of ES modules. <code>require</code> always works. This can be fixed by simply replacing all <code>module.exports = ...</code> to <code>export default ...</code> where applicable, as this is seemingly equivalent for old Babel-style ES module transpilation. (Note though, that importing this module using <code>require</code> will probably give you an option with a <code>default</code> key rather than the default export itself, so it's probably best you make the switch across the entire codebase at once.)</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-273917976">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I find myself also being bitten by this issue since upgrading to <code>2.2.0</code>. In my case, my hypothesis is a require chain that looks like:</p>
<pre><code>CommonJSModule --requires--&gt; ESModule --requires--&gt; AnotherCommonJSModule
</code></pre>
<p>I'm sorry that I can't provide any more details at this time.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-273957585">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm not at all familiar with the internals but a quick, manual binary search suggests the regression is here: <a href="https://github.com/webpack/webpack/compare/v2.2.0-rc.4...v2.2.0-rc.5" target="_blank"><tt>v2.2.0-rc.4...v2.2.0-rc.5</tt></a></p>
<p>Attn: <a href="https://github.com/sokra" target="_blank">@sokra</a>, <a href="https://github.com/TheLarkInn" target="_blank">@TheLarkInn</a> I think this issue should be re-opened.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-273979302">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Taking a quick glance, this is definitely the culprit:</p>
<p><a href="https://github.com/webpack/webpack/commit/a7a41848c73f14ff294b48285f42063e1f0de4b1" target="_blank"><tt>a7a4184</tt></a></p>
<pre><code>detect harmony modules before parsing
exports is now undefined in ESM
module.exports is now read-only in ESM and returns undefined
define is now undefined in ESM
</code></pre>
<p>As it says, <code>module.exports</code> is read-only in ES modules. If you're getting <code>module.exports</code> as read-only in a CommonJS module, THAT would be a bug, but that file is very much not a CommonJS file if it contains any <code>export</code>/<code>import</code> statements. I can confirm that this was the problem in my case and it was fixed by making my ES modules properly use ES exports. As a note <code>require</code> still works just fine inside of any module.</p>
<p>From my PoV it seems like Webpack's new behavior ultimately makes a lot more sense than the old behavior. It is fairly inane to allow mixing of <code>import</code> statements and CommonJS <code>module.exports</code>, and probably was never intended to work that way.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-273983463">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Maybe add this info to migration guide?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-274071458">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I can only speak for myself, but for the situation affecting me the module within which <code>module.exports</code> is read-only does not have any <code>import</code> or <code>export</code> statements. It appears that the heuristic that is identifying the file in question as a 'harmony' model is misfiring in some situations.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-274081658">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ggoodman" target="_blank">@ggoodman</a> are you using babel-runtime?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-274082953">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/sokra" target="_blank">@sokra</a> here are the relevant config files:</p>
<p><strong>.babelrc</strong>:</p>
<div><pre>{
  "presets": [
    ["env", {
      "modules": false,
      "targets": {
        "browsers": ["last 2 versions", "safari &gt;= 7"]
      }
    }]
  ],
  "plugins": ["transform-runtime", "syntax-dynamic-import"]
}</pre></div>
<p><strong>webpack.config.js</strong> (<em>simplified</em>):</p>
<div><pre>'use strict';

const ExtractTextPlugin = require('extract-text-webpack-plugin');
const Path = require('path');
const Webpack = require('webpack');


const config = {
    cache: true,
    devtool: process.env.NODE_ENV !== 'production' ? 'source-map' : false,
    context: Path.join(__dirname),
    output: {
        path: Path.join(__dirname, 'build'),
        filename: '[name].js',
        chunkFilename: '[name].js',
        publicPath: '/static/',
    },
    recordsPath: Path.join(__dirname, 'recordsCache'),
    module: {
        rules: [{
                test: /\js$/,
                exclude: /node_modules/,
                use: [
                    {
                        loader: 'ng-annotate-loader',
                    },
                    {
                        loader: 'babel-loader',
                        options: {
                            cacheDirectory: true,
                        },
                    },
                    {
                        loader: 'string-replace-loader',
                        options: {
                            multiple: [
                                { search: /API_URL/g, replace: process.env['PLUNKER_API_URL'] },
                                { search: /EMBED_URL/g, replace: process.env['PLUNKER_EMBED_URL'] },
                                { search: /RUN_URL/g, replace: process.env['PLUNKER_RUN_URL'] },
                                { search: /SHOT_URL/g, replace: process.env['PLUNKER_SHOT_URL'] },
                                { search: /WWW_URL/g, replace: process.env['PLUNKER_WWW_URL'] },
                            ],
                        },
                    },
                ]
            },
        ],
    },
    plugins: [
        new ExtractTextPlugin({
            filename: '[name].css',
            disable: false,
            allChunks: true,
        }),
    ],
    resolve: {
        modules: [
            Path.join(__dirname, 'node_modules'),
            Path.join(__dirname, 'src'),
        ],
    },
};

module.exports = config;</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-274089238">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Chiming in as I'm getting this error in the browser as well, but neither the requiring module, nor the required module have any <code>import</code> or <code>export</code> statements in them. I am using <code>transform-runtime</code> if that's relevant.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-274094298">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><code>transform-runtime</code> adds <code>import</code> to your files...</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-274187353">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/sokra" target="_blank">@sokra</a> I was not aware that this plugin would add <code>import</code> to my files.</p>
<p>If removing that plugin is a solution, what alternative can we consider so that we don't have <code>babel-runtime</code> stuff like <code>_classCallCheck</code> included for every source file using ES6 features like <code>class</code>es?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-274240819">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>The way I see it, there are a few good solutions:</p>
<ul>
<li>Make <code>transform-runtime</code> support outputting <code>require</code> statements instead of <code>import</code> statements, as an option. This seems unlikely, because it looks like Babel is already relying on the fact that <code>import</code> is declarative.</li>
<li>Use <code>transform-es2015-modules-commonjs</code>. This would replace all <code>import</code> statements with <code>require</code> statements. If you are not using any <code>import</code>/<code>export</code> syntax in your app, this solution is probably ideal, because it incurs no extra cost. However, if you are using ES modules, then this will likely impact Webpack 2's ability to perform tree shaking. (I'm sure everyone is aware of this.)</li>
<li>Use ES modules across the board. I think this is the most correct thing to do. Is there a reason why existing CommonJS exports can't simply be migrated? <code>require</code> does not have to be globally replaced, only <code>module.exports</code> and <code>exports</code> statements.</li>
</ul>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-274459853">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>How i can reproduce module.exports behavior?<br />
I had entry point with name LoginPage, i need to build library with the same name, after that i init it on the page using new LoginPage();<br />
Now i should use new LoginPage.LoginPage() or new LoginPage.default();<br />
How i can resolve this issue?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-275278301">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>adding <code>import</code> (by <code>transform-runtime</code>) also means that the file is switched into strict mode, which could break you code. In my opinion <code>transform-runtime</code> should be changed.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-275905257">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I had the following <strong><code>.babelrc</code></strong></p>
<pre><code>{
    "presets": [
        [
            "es2015",
            {
                "modules": false
            }
        ],
        "stage-0",
        "react"
    ],
    "plugins": [
        "add-module-exports",
        "transform-class-properties",
        "transform-object-rest-spread",
        "transform-object-assign"
    ]
}
</code></pre>
<p>And was able to fix this by removing the <strong><code>add-module-exports</code></strong> plugin. TBH, I can't even recall why I had it in there to begin with... but upon removal it started working as expected. Nobody else has mentioned <strong><code>add-module-exports</code></strong> yet so I thought I'd chime in too to point out that it's not just <strong><code>transform-runtime</code></strong> causing this.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  


  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-281136701">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I am having the same problem with vis project. I made the most simple example if somebody have any idea what could be the problem. Error is in vis code. <a href="https://github.com/almende/vis" target="_blank">https://github.com/almende/vis</a></p>
<p>It does not seam like related to any plugin or mixing of import and module.exports.</p>
<p>error:</p>
<pre><code>Uncaught TypeError: Cannot assign to read only property 'exports' of object '#&lt;Object&gt;'
    at Object.eval (ItemSet.js:2296)
    at eval (ItemSet.js:2298)
    at Object.../node_modules/vis/lib/timeline/component/ItemSet.js
</code></pre>
<p>example:<br />
<a href="https://github.com/primozs/vis-example-webpack2" target="_blank">https://github.com/primozs/vis-example-webpack2</a></p>
<p>I had no issues in versions:</p>
<pre><code>    "webpack": "2.1.0-beta.27",
    "webpack-dev-server": "v2.1.0-beta.12",
</code></pre>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  



</div>

</div>

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-281236672">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>@johnwchadwick I just upgraded one of my project to Webpack 2.2.x and it fixed my issue. Thank you.</p>
<p>Replaced <code>module.exports</code> with <code>export default</code>, and the <code>require(...)</code> with <code>require(...).default</code></p>
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
    
  <div id="issuecomment-281850699">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><code>npm install webpack@2.1.0-beta.27 --save</code> can release the pain temporarily.</p>
<p>This is the reason: <a href="https://github.com/webpack/webpack/pull/3958" target="_blank">#3958</a><br />
But I like this suggestion:<br />
<a href="https://github.com/webpack/webpack/issues/3917#issuecomment-272746700" target="_blank">#3917 (comment)</a></p>
<p>the better error info should be<br />
"module.exports is readonly when using ES2015 modules. Do not mix import with module.exports."</p>
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
    
  <div id="issuecomment-282107000">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Unfortunately the exports-loader injects module.exports statements so using it with a legacy codebase and injecting that to a es6 project has become impossible.</p>
<p><a href="https://cloud.githubusercontent.com/assets/1576993/23277073/e35faece-fa0c-11e6-824c-fecc4d4187cc.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/1576993/23277073/e35faece-fa0c-11e6-824c-fecc4d4187cc.png" alt="image" /></div></a><br />
<a href="https://cloud.githubusercontent.com/assets/1576993/23278346/70e7f8a6-fa11-11e6-8012-4fc3b338e0cc.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/1576993/23278346/70e7f8a6-fa11-11e6-8012-4fc3b338e0cc.png" alt="image" /></div></a></p>
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
    
  <div id="issuecomment-283489171">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Is there any progress on this? I am unable to import a legacy library. Unfortunately i am unable to use import / export in legacy library.</p>
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
        <h3 id="ref-issue-254862721">
      
        
      
        
  <a href="/Tabrizian" target="_blank">Tabrizian</a>
  

      referenced this issue
        in <strong>bambil/vue-mqttsocket</strong>
      <a href="#ref-issue-254862721" target="_blank">
        <relative-time>on Sep 3, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/bambil/vue-mqttsocket/issues/1" target="_blank">
          Transpiling library
          #1
        </a>
      </h4>
    

    


  

</div>

  

  

  

  

  

  

  <div>
  <h3 id="ref-commit-491bdb5">
    
      
    
    
  <a href="/ahdinosaur" target="_blank">ahdinosaur</a> 


      added a commit
        to root-systems/cobuy
      that referenced
      this issue

    <a href="#ref-commit-491bdb5" target="_blank">
      <relative-time>on Oct 26, 2017</relative-time>
    </a>
  </h3>

  
</div>

  

  

  

  

  <div>
        <h3 id="ref-pullrequest-274374911">
      
        
      
        
  <a href="/ssfdust" target="_blank">ssfdust</a>
  

      referenced this issue
        in <strong>LazyHua/vue-element-treeTable</strong>
      <a href="#ref-pullrequest-274374911" target="_blank">
        <relative-time>on Nov 16, 2017</relative-time>
      </a>
    </h3>

  
    
        
      Open
    



    
      <h4>
        <a href="/LazyHua/vue-element-treeTable/pull/1" target="_blank">
          避免在其他文件import时出现TypeError的错误
          #1
        </a>
      </h4>
    

    


  

</div>

  

  

  

  

  

  <div>
        <h3 id="ref-issue-260199129">
      
        
      
        
  <a href="/MaySnow" target="_blank">MaySnow</a>
  

      referenced this issue
        in <strong>vuejs/vue</strong>
      <a href="#ref-issue-260199129" target="_blank">
        <relative-time>on Jan 16</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/vuejs/vue/issues/6685" target="_blank">
          插件挂载有点问题
          #6685
        </a>
      </h4>
    

    


  

</div>

  <div>
        <h3 id="ref-pullrequest-291306178">
      
        
      
        
  <a href="/fenglish" target="_blank">fenglish</a>
  

      referenced this issue
        in <strong>Financial-Times/n-newsletter-signup</strong>
      <a href="#ref-pullrequest-291306178" target="_blank">
        <relative-time>on Jan 25</relative-time>
      </a>
    </h3>

  
    
        
      Open
    



    
      <h4>
        <a href="/Financial-Times/n-newsletter-signup/pull/33" target="_blank">
          fix demo
          #33
        </a>
      </h4>
    

    


  

</div>

  

  <div>
        <h3 id="ref-issue-292291737">
      
        
      
        
  <a href="/icarito" target="_blank">icarito</a>
  

      referenced this issue
        in <strong>metapensiero/metapensiero.pj</strong>
      <a href="#ref-issue-292291737" target="_blank">
        <relative-time>on Jan 30</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/metapensiero/metapensiero.pj/issues/39" target="_blank">
          Support alternative import / export syntax
          #39
        </a>
      </h4>
    

    


  

</div>

  

  

  

  

  

  

  

  

  


</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-382639282">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Removing <code>"modules: false"</code> in .babelrc might work</p>
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
    
  <div id="issuecomment-383291377">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/exarus" target="_blank">exarus</a>
  

    </strong>

    commented

    <a href="#issuecomment-383291377" target="_blank"><relative-time>on Apr 21</relative-time></a>


      
  •


  
    <summary>
      
          edited
      
      
    </summary>

    
  

  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Faced this issue when <code>import</code>ed <code>.js</code> with ES6 <code>class</code> and <code>module.exports =</code> into my <code>vue-cli</code> project.<br />
Webpack config:</p>
<div><pre>{
  test: /\.js$/,
  loader: 'babel-loader',
  include: [
    resolve('src'),
    resolve('test'),
    resolve('node_modules/webpack-dev-server/client'),
    resolve('node_modules/my-class-module'),
  ]
},</pre></div>
<p>babel config:</p>
<div><pre>{
  "presets": [
    ["env", {
      "modules": false,
      "useBuiltIns": true,
    }],
    "stage-2"
  ],
  "plugins": ["transform-vue-jsx", "transform-runtime"],
}</pre></div>
<p>Included class:</p>
<div><pre>class MyClass {}
module.exports = MyClass;</pre></div>
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
    
  <div id="issuecomment-383298688">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/kenberkeley" target="_blank">@kenberkeley</a> it did solve for me, can you help explaining why would it work ?</p>
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
    
  <div id="issuecomment-383299157">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/bitcot" target="_blank">@bitcot</a> I guessed, I tried, it worked, no explanation...</p>
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
    
  
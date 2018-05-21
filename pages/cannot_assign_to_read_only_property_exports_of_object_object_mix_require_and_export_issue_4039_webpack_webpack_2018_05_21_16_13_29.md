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


  <div id="progressive-timeline-item-container">
  


  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-283489998">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/hzoo" target="_blank">@hzoo</a> Hey is there a way to let transform-runtime use require instead of import's</p>
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
    
  <div id="issuecomment-283501082">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I actually just got this to work by changing my <code>.babelrc</code> file.</p>
<pre><code>{
  "presets": [
    "es2015",
    "es2016",
    "stage-2"
  ],
  "plugins": [
    "transform-async-to-generator",
    "transform-class-properties",
    "transform-object-rest-spread",
    "transform-export-extensions",
    "transform-runtime",
    "lodash"
  ]
}
</code></pre>
<p>The big change that worked for me was removing <code>modules: false</code> from <code>es2015</code></p>
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
    
  <div id="issuecomment-283743109">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/TheLarkInn" target="_blank">@TheLarkInn</a> Definitely something we can explore for <code>7.0</code>. There are several issues around transform-runtime that have been longstanding that we're hoping to fix.</p>
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
    
  <div id="issuecomment-283802593">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/loganfsmyth" target="_blank">@loganfsmyth</a> Awesome just wanted to followup. Should we track this or you all? Doing some issue purging this week lol.</p>
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
    
  <div id="issuecomment-284038679">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Just bumped into this myself. There should probably be an eslint rule that disallows using <code>import</code> in a file with <code>module.exports</code>. Anyone know whether this exists? If not, I'll make it :)</p>
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
    
  <div id="issuecomment-284070756">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I've written the rule and it works. I think it'd be best to add to <code>eslint-plugin-import</code> so I've added an issue there: <a href="https://github.com/benmosher/eslint-plugin-import/issues/760" target="_blank">benmosher/eslint-plugin-import#760</a></p>
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
        <h3 id="ref-issue-214954383">
      
        
      
        
  <a href="/mafeifan" target="_blank">mafeifan</a>
  

      referenced this issue
        in <strong>christianalfoni/flux-angular</strong>
      <a href="#ref-issue-214954383" target="_blank">
        <relative-time>on Mar 17, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/christianalfoni/flux-angular/issues/69" target="_blank">
          webpack2 report error
          #69
        </a>
      </h4>
    

    


  

</div>

  

  

  

  

  

  


</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-294071107">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>你把module.export改为export.default试试</p>
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
    
  <div id="issuecomment-300742466">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/smitt04" target="_blank">@smitt04</a> :</p>
<blockquote>
<p>The big change that worked for me was removing modules: false from es2015 <g-emoji>👍</g-emoji> 2</p>
</blockquote>
<p>This will break tree shaking.<br />
Better approach would be to replace module.exports with exports default. Will that work for you?</p>
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
    
  <div id="issuecomment-300790092">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/abhinavsingi" target="_blank">@abhinavsingi</a> unfortunately I can't use exports default. I use that in all my own new code. But the problem was when I imported a node module that was using module.exports</p>
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
    
  <div id="issuecomment-300812034">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Right now, i don't think it is correct to use import / export on node js modules, until node supports them natively.  Client side code is ok to transpile since we can't write a lot of es6+ in browsers and usually you have a build / minify stage on deployment.  But having to transpile your code to run on node i think is an extra step that doesn't need to be done. Now i have to compile / transpile my code be fore testing.</p>
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
    
  <div id="issuecomment-302216844">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>what is the recommended solution for this issue when a dependent npm module is performing an import when they shouldn't? Is there any way to have webpack automatically alter the <code>import blah from 'blah'</code> to <code>var blah = require('blah').default</code> ?</p>
<p><a href="https://github.com/kentcdodds" target="_blank">@kentcdodds</a> PR not really an option as the module devs are trying to decide on which style to adopt, 1.5 months ago, can't force someone else to accept a PR to resolve a bundling issue.</p>
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
    
  <div id="issuecomment-302242986">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/patsissons" target="_blank">@patsissons</a>, I can appreciate that. Forking is always an option. You could also write a custom loader for that module I guess... Though there's probably an easier way...</p>
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
    
  <div id="issuecomment-302247180">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I submitted a PR none the less, <a href="https://github.com/almende/vis/pull/3063" target="_blank">almende/vis#3063</a></p>
<p>This issue just means I have to bundle the entire library, which means my bundle is a bit larger than it needs to be. Not critical, just annoying :)</p>
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
    
  <div id="issuecomment-303043964">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Why would webpack2 banned such a rule???? It can certainly cause a lot of problem! Every module has to be rewrite</p>
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
    
  <div id="issuecomment-307089690">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I had this problem when I had one file with mix of <code>export default</code> and <code>require('...')</code>. I'm ok with changing it, but is it possible to raise an exception on webpack build step?</p>
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
    
  <div id="issuecomment-307438939">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Guys, would be cool to add link to current issue into error on mixed <code>import</code> and <code>module.exports</code></p>
<p>Is it possible and reasonable?</p>
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
    
  <div id="issuecomment-307542564">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>Guys, would be cool to add link to current issue into error on mixed import and module.exports<br />
Is it possible and reasonable?</p>
</blockquote>
<p>I would accept a PR for that <a href="https://github.com/a-x-" target="_blank">@a-x-</a> feel free and tag me when you create it.</p>
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
    
  <div id="issuecomment-309746398">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>It's clear that this issue happens when <code>import</code> and <code>module.exports</code> are mixed.<br />
As well it's clear that the possible solution, such as removing <code>modules:false</code> from the <code>['es2015', {modules: false}]</code> equasion is not good, as it affects tree shaking.</p>
<p>Have two questions though:</p>
<ol>
<li>I thought that if I will <code>require</code> my module on the front-end side (explicitly) this would solve the issue. As <code>module.exports</code> module would be <code>required</code>. But I see the same error. Why?</li>
<li>Why I don't see such error for `React, for example. In my code, as the same file I have:</li>
</ol>
<pre><code>import React, {Component} from 'react';
import Workflow from 'common/modules/workflow';
</code></pre>
<p>whily <code>react</code> leads to:<br />
<a href="https://user-images.githubusercontent.com/839290/27334298-248e070c-55c9-11e7-962c-08991a19f7c3.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://user-images.githubusercontent.com/839290/27334298-248e070c-55c9-11e7-962c-08991a19f7c3.png" alt="image" /></div></a></p>
<p>And <code>workflow</code> leads to:<br />
<a href="https://user-images.githubusercontent.com/839290/27334310-31c36f84-55c9-11e7-9de9-6962d38cec7a.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://user-images.githubusercontent.com/839290/27334310-31c36f84-55c9-11e7-9de9-6962d38cec7a.png" alt="image" /></div></a></p>
<p>In the console I see the error about the workflow inclusion:<br />
<a href="https://user-images.githubusercontent.com/839290/27334336-4eb6e9ea-55c9-11e7-9281-b2a5d4a15c4e.png" target="_blank" class="readableLinkWithMediumImage"><img src="https://user-images.githubusercontent.com/839290/27334336-4eb6e9ea-55c9-11e7-9281-b2a5d4a15c4e.png" alt="image" /></a></p>
<p>how the <code>react</code> case is different?<br />
3. What is the expected way to have an isomorphic modules and use it both on <code>nodejs</code> and <code>front-end</code> parts. (I don't want to transpile my nodejs code)</p>
<p><a href="https://github.com/sokra" target="_blank">@sokra</a></p>
<p>Regards,</p>
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
        <h3 id="ref-issue-224059257">
      
        
      
        
  <a href="/tomasz" target="_blank">tomasz</a>
  

      referenced this issue
        in <strong>autoNumeric/autoNumeric</strong>
      <a href="#ref-issue-224059257" target="_blank">
        <relative-time>on Jun 21, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/autoNumeric/autoNumeric/issues/438" target="_blank">
          Upgrade Webpack to 3.*
          #438
        </a>
      </h4>
    

    


  

</div>


</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-309816843">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>You have to transpile your node code since node doesn't support import/export.</p>
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
    
  <div id="issuecomment-309820695">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ljharb" target="_blank">@ljharb</a><br />
thanks for the answer.<br />
why I don't have the same issue while importing the <code>react</code> ?</p>
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
    
  <div id="issuecomment-309823653">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I assume because Workflow is using export syntax, and React, as a published library, is using module.exports. Not really sure tho.</p>
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
    
  <div id="issuecomment-309829813">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>If so this particular feature looks not very thought through. I think there should be a way for the developer to have an isomorphic modules for nodejs and webpack. This is very natural need.</p>
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
    
  <div id="issuecomment-309834601">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>The only way to do that is to always transpile everything using babel and webpack.</p>
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
    
  <div id="issuecomment-309835938">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ljharb" target="_blank">@ljharb</a><br />
but that's the thing :) I don't want to transpile everything. nodejs has enough ES2015 features to not be transpiled. even <code>async/await</code>. so it feels right to run the original code.</p>
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
    
  <div id="issuecomment-309838733">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Then the codes not truly isomorphic, because you're not using the same output on both platforms. You can't have it both ways :-)</p>
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
  <h3 id="ref-commit-067529b">
    
      
    
    
  <a href="/cpunion" target="_blank">cpunion</a> 


      added a commit
        to cpunion/react-native-elements
      that referenced
      this issue

    <a href="#ref-commit-067529b" target="_blank">
      <relative-time>on Jun 26, 2017</relative-time>
    </a>
  </h3>

  
</div>

  <div>
        <h3 id="ref-pullrequest-238448928">
      
        
      
        
  <a href="/cpunion" target="_blank">cpunion</a>
  

      referenced this issue
        in <strong>react-native-training/react-native-elements</strong>
      <a href="#ref-pullrequest-238448928" target="_blank">
        <relative-time>on Jun 26, 2017</relative-time>
      </a>
    </h3>

  
    
        
      Merged
    



    
      <h4>
        <a href="/react-native-training/react-native-elements/pull/448" target="_blank">
          Fix mix of import and module.exports
          #448
        </a>
      </h4>
    

    


  

</div>


</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-311161061">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hi <a href="https://github.com/sokra" target="_blank">@sokra</a> ,</p>
<p>I know you're busy.</p>
<p>But the question from <a href="https://github.com/webpack/webpack/issues/4039#issuecomment-309746398" target="_blank">#4039 (comment)</a> , why I can <code>import from 'react'</code> but can not import my custom module, while they both do <code>module.exports</code> - doesn't allow me to sleep :)</p>
<p>Please, consider pointing me to the right direction.</p>
<p>Thanks in advance.</p>
<p>Regards,</p>
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
    
  <div id="issuecomment-311296117">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/PavelPolyakov" target="_blank">@PavelPolyakov</a> looks like you use <code>module.exports = Workflow</code>, but somewhere above your're exporting dependencies using <code>export</code>, instead of <code>require</code>.  Can you make sure that you don't have <code>import</code> or <code>export</code> statements in your <code>Workflow.js</code>?</p>
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
    
  <div id="issuecomment-311313766">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>hi <a href="https://github.com/KELiON" target="_blank">@KELiON</a>, thanks for trying to help.<br />
No, there are no <code>imports</code> above.</p>
<p>The modules configuration, as it is stated above is important as well:</p>
<pre><code>presets: [['es2015', {modules: false}], 'react'],
</code></pre>
<p>Whenever I comment it out it works, whether I use <code>imports</code> or <code>require</code>.</p>
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
    
  <div id="issuecomment-311321193">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/KELiON" target="_blank">@KELiON</a> , <a href="https://github.com/ljharb" target="_blank">@ljharb</a><br />
I believe I found the issue why it works for the <code>node_modules</code>, but not for the regular modules.<br />
And the issue was - that <code>node_modules</code> are excluded from the <code>babel-loader</code>.</p>
<p>Probably, when <code>babel-loader</code> meets <code>module.exports</code> something goes wrong.</p>
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
    
  <div id="issuecomment-311384273">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/PavelPolyakov" target="_blank">@PavelPolyakov</a> you should post a reproduction of your issue instead of snippets. It will make it a lot easier for others to follow and diagnose the issue.</p>
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
    
  <div id="issuecomment-311399086">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/vinnymac" target="_blank">@vinnymac</a><br />
I definitely need to, but it started as basic question. And for me is already solved.</p>
<p>I think this <a href="https://github.com/webpack/webpack/issues/4039#issuecomment-311321193" target="_blank">#4039 (comment)</a> explains my question and may help other developers.</p>
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
    
  <div id="issuecomment-319064778">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><code>webpack@3.4.1</code></p>
<h2>This will work:</h2>
<p><strong>a.js</strong></p>
<div><pre>module.exports = {};</pre></div>
<p><strong>b.js</strong></p>
<div><pre>import a from './a'
console.log(a)</pre></div>
<h2>But this will not work:</h2>
<p><strong>a.js</strong></p>
<div><pre>// the occurrence of keyword `typeof` will lead to error:
// `Uncaught TypeError: Cannot assign to read only property 'exports' of object '#&lt;Object&gt;'`
var x = typeof 1;
module.exports = {};</pre></div>
<p><strong>b.js</strong></p>
<div><pre>import a from './a'
console.log(a)</pre></div>
<h2>This will work:</h2>
<p><strong>a.js</strong></p>
<div><pre>// noop</pre></div>
<p><strong>b.js</strong></p>
<div><pre>import a from './a'
console.log('imported a:', a);</pre></div>
<p><strong>output</strong></p>
<blockquote>
<div><pre>imported a: object {}</pre></div>
</blockquote>
<h2>But this will cause a warning:</h2>
<p><strong>a.js</strong></p>
<div><pre>var x = typeof 1;</pre></div>
<p><strong>b.js</strong></p>
<div><pre>import a from './a'
console.log('imported a:', a);</pre></div>
<p><strong>output</strong></p>
<blockquote>
<div><pre>imported a: undefined
[HMR] bundle has 1 warnings
./b.js
"export 'default' (imported as 'a') was not found in './a'</pre></div>
</blockquote>

<p><strong>I think the keyword <code>typeof</code> will cause the ES/CommonJS module type distinguishing error.</strong></p>
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
        <h3 id="ref-pullrequest-247963973">
      
        
      
        
  <a href="/KELiON" target="_blank">KELiON</a>
  

      referenced this issue
        in <strong>rafa-acioly/cerebro-convertcolor</strong>
      <a href="#ref-pullrequest-247963973" target="_blank">
        <relative-time>on Aug 4, 2017</relative-time>
      </a>
    </h3>

  
    
        
      Merged
    



    
      <h4>
        <a href="/rafa-acioly/cerebro-convertcolor/pull/6" target="_blank">
          Use cerebro scripts
          #6
        </a>
      </h4>
    

    


  

</div>


</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-321766110">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>In case this helps anyone …</p>
<p>We've just encountered this issue, and eventually tracked it down to a superfluous inclusion of <code>react</code> in <code>npm-shrinkwrap.json</code> as a dependency of a dependency, as well as being included directly.</p>
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
        <h3 id="ref-pullrequest-251186563">
      
        
      
        
  <a href="/exytab" target="_blank">exytab</a>
  

      referenced this issue
        in <strong>handsontable/handsontable</strong>
      <a href="#ref-pullrequest-251186563" target="_blank">
        <relative-time>on Aug 18, 2017</relative-time>
      </a>
    </h3>

  
    
        
      Closed
    



    
      <h4>
        <a href="/handsontable/handsontable/pull/4469" target="_blank">
          Changed 'module.exports' on 'export default'
          #4469
        </a>
      </h4>
    

    

  
    2 of 5 tasks complete
    
      
    
  

  

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
    
  
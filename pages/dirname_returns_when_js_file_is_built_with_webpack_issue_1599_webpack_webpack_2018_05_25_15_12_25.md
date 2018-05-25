<a href="https://github.com/webpack/webpack/issues/1599">https://github.com/webpack/webpack/issues/1599</a><div id="articleHeader"><h1>              __dirname returns '/' when js file is built with webpack            #1599    </h1></div>


  <div>
    
    <div>
        <a href="/AJShippify" target="_blank">AJShippify</a>  opened this Issue
        <relative-time>on Nov 8, 2015</relative-time>
        · 46 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-115678540">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I have a working express file, which I 'webpack' it but when the bundled file is run the __dirname global changes to '/'. I need the absolute path for certain functions as res.sendFile. Any help?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-154742625">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>See <code>node</code> option in the documentation.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-154754094">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Ok, I set the</p>
<div><pre>node: {
 __dirname: true
    }</pre></div>
<p>But now the __dirname is empty, ''</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-154830172">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Could you provide a sample code for retrieving the proper directory name?. I'm currently using a module called app-root-path but I'd like to know if there is a webpack-native way of doing it</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-157332291">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Typically, <code>__dirname</code> is set to <code>options.output.publicPath</code>. Switching to node, shouldl resolve this.<br />
However, you also need to set <code>target: "node"</code>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-179729952">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I got the same result after trying the above config.<br />
Here is my config:</p>
<p><strong>webpack.config.js</strong></p>
<pre><code>var webpack = require('webpack');
var path = require('path');
var fs = require('fs');

var nodeModules = {};
fs.readdirSync('node_modules')
  .filter(function(x) {
    return ['.bin'].indexOf(x) === -1;
  })
  .forEach(function(mod) {
    nodeModules[mod] = 'commonjs ' + mod;
  });

var exts = ['express'];
module.exports = {
  entry: ['./server/index.js'],
  context: __dirname,
  node: {
    __filename: true,
    __dirname: true
  },
  target: 'node',
  output: {
    path: path.join(__dirname, 'build'),
    filename: '[name].bundle.js',
    chunkFilename: "[id].bundle.js"
  },
  externals: nodeModules,
  plugins: [
    new webpack.IgnorePlugin(/\.(css|less)$/),
    new webpack.BannerPlugin('require("source-map-support").install();',
                             { raw: true, entryOnly: false }),
  ],
  devtool: 'sourcemap',
}
</code></pre>
<p>src: <strong>./server/index.js</strong></p>
<pre><code>...
app.use('/static', express.static(path.join(__dirname, '..', 'public')));
...
</code></pre>
<p>It works for directly run the source. Am I missing something?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-186620333">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Same <g-emoji>👍</g-emoji><br />
How to disable __dirname injection, leaving it as original?</p>
<p>---UPDATE---</p>
<p>For now, I use this hack:</p>
<div><pre>plugins: [
  new webpack.DefinePlugin({
    $dirname: '__dirname',
  }),
]</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-186664656">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/fritx" target="_blank">@fritx</a> I cannot find any related to your usage in the document. May I know how does it works?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-186759114">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/goodseller" target="_blank">@goodseller</a> Just replace <code>__dirname</code> with <code>$dirname</code>, and it works.<br />
The <code>$dirname</code> would be equivalent to <code>__dirname</code>, regardless of the webpack injection.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-186841345">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Sorry, I found the hack unnecessary.</p>
<div><pre>// the webpack config just works
target: 'node',
node: {
  __dirname: false,
  __filename: false,
}</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-191861069">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>wow, that works for me too, the setting seems counterintuitive. wish we had explanations for what true, false mean in each case.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-191862028">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>if I have a node module requiring in a module for me, through a config file, how can I have webpack include the files that are being required in for me so that they are in the build directory?  basically I have a hapijs app, and am trying out webpack for the node build. Glue module reads in a config, and the __dirname is now the build directory, and the modules are still in src since they are not being required in explicitly. thoughts?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-193625057">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/kellyrmilligan" target="_blank">@kellyrmilligan</a> <g-emoji>😵</g-emoji> I think you need to make those modules (in trouble) <code>commonjs</code>?</p>
<div><pre>plugins: [
  new webpack.ExternalsPlugin('commonjs', ['a', 'b'])
]</pre></div>
<p>or just make them all <code>commonjs</code>:</p>
<div><pre>// https://github.com/fritx/os-web/blob/dev/task%2Fwebpack.server.js
externals: [
  (ctx, req,  cb) =&gt; {
    // if (/^\.?\//.test(req)) return cb()
    if (/^\.\.?\//.test(req)) return cb() // fixed √
    cb(null, `commonjs ${req}`)
  },
],</pre></div>
<p>I have a project (experimental) <g-emoji>😆</g-emoji> which webpacks both client & server side.<br />
Check this out: <a href="https://github.com/fritx/os-web" target="_blank">https://github.com/fritx/os-web</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-246825591">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>if I have a node module requiring in a module for me, through a config file, how can I have webpack include the files that are being required in for me so that they are in the build directory? basically I have a hapijs app, and am trying out webpack for the node build. Glue module reads in a config, and the __dirname is now the build directory, and the modules are still in src since they are not being required in explicitly. thoughts?</p>
</blockquote>
<p><a href="https://github.com/kellyrmilligan" target="_blank">@kellyrmilligan</a> Have you found a solution?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-246850044">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I ended up abandoning the approach. Kept on running into brick walls</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-247041126">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'd like to add that using <code>node</code> option</p>
<div><pre>node: {
  __dirname: false
}</pre></div>
<p>will also work if you are targeting electron.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
      <div>
        <h3 id="ref-issue-178301734">
      
        
      
        
  <a href="/catamphetamine" target="_blank">catamphetamine</a>
  

      referenced this issue
        in <strong>catamphetamine/universal-webpack</strong>
      <a href="#ref-issue-178301734" target="_blank">
        <relative-time>on Sep 21, 2016</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/catamphetamine/universal-webpack/issues/30" target="_blank">
          __dirname is / in server modules
          #30
        </a>
      </h4>
    

    


  

</div>




  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-251241493">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Whatever this flag is doing, setting <code>__dirname: true</code>fixed it for me.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-260077616">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Playing with this a bit, assuming I have the following:</p>
<pre><code>./src
  public
    app.js
  server
    app.js
</code></pre>
<p>and inside <code>server/app.js</code> I include the following:</p>
<pre><code>app.use(express.static(path.join(__dirname, '../public')))
</code></pre>
<p>The following happens based upon what <code>options.node.__dirname</code> is set to:</p>
<ul>
<li><em>unset</em> - leading slash, <code>/</code>; express will attempt to serve files from the root, <code>/public</code> (d'oh!)</li>
<li><em>true</em> - sets it to the original path of the src filename, in this case <code>src/server</code></li>
<li><em>false</em> - no injection is performed, global.__dirname is used and it will be <code>options.output.path</code>, effectively.</li>
</ul>
<p>The unset case seems the most counter-intuitive to me and I have a hard time understanding what the use case of injecting <code>/</code> as <code>__dirname</code> would be.... strange that this is the default.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-266588898">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>FWIW to get the actual behavior in node you need to write your own plugin. This is adapted from the NodeStuffPlugin (which handles the configuration discussed here). Just insert the following into your plugins array:</p>
<div><pre>    {
      apply(compiler) {
        function setModuleConstant(expressionName, fn) {
          compiler.parser.plugin('expression ' + expressionName, function() {
            this.state.current.addVariable(expressionName, JSON.stringify(fn(this.state.module)));
            return true;
          });
        }

        setModuleConstant('__filename', function(module) {
          return module.resource;
        });

        setModuleConstant('__dirname', function(module) {
          return module.context;
        });
     }</pre></div>
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
    
  <div id="issuecomment-280752281">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>For everyone's reference, I just posted a similar issue here: <a href="https://github.com/webpack/webpack/issues/4303" target="_blank">#4303</a></p>
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
    
  <div id="issuecomment-310483535">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Why though ?</p>
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
    
  <div id="issuecomment-316052448">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/mmmeff" target="_blank">@mmmeff</a> weird. for me it was <code>__dirname: false</code> that fixed it.</p>
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
    
  <div id="issuecomment-319396399">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>would someone rewrite <a href="https://github.com/amasad" target="_blank">@amasad</a> 's comment. got this warning</p>
<pre><code>Use 
compiler.plugin("compilation", function(compilation, data) {
  data.normalModuleFactory.plugin("parser", function(parser, options) { parser.plugin(/* ... */); });
}); 
instead.```
</code></pre>
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
    
  <div id="issuecomment-328540024">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>for those having this issue, it is also good to note that <code>module.filename</code> would be undefined if you bundled your files. In my case it was undefined and I fixed it by simply replacing it with <code>__filename</code> which yields the same outcome.</p>
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
    
  <div id="issuecomment-328927602">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>@mmclau14 Here's an update that avoids the deprecation warning:</p>
<div><pre>class WebpackDirnamePlugin {
  apply(compiler) {
    function setModuleConstant(expression, fn) {
      compiler.plugin('parser', function(parser) {
        parser.plugin(`expression ${ expression }`, function() {
          this.state.current.addVariable(expression, JSON.stringify(fn(this.state.module)))
          return true
        })
      })
    }

    setModuleConstant('__filename', function(module) {
      return module.resource
    })

    setModuleConstant('__dirname', function(module) {
      return module.context
    })
  }
}</pre></div>
<p>It's ESNext syntax so you'll want to <a href="http://babeljs.io/repl/" target="_blank">run it through Babel</a> or use <code>webpack.config.babel.js</code>.</p>
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
    
  <div id="issuecomment-366553860">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://webpack.js.org/configuration/node/" target="_blank">https://webpack.js.org/configuration/node/</a><br />
AJShippify commented on Nov 7, 2015 that made the parameter true and it wont fix, I fixed doing the opposite, turning parameter false:</p>
<pre><code>node: {
  __dirname: false
}
</code></pre>
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
    
  <div id="issuecomment-368146921">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <h2>Locally</h2>
<p>When I set <code>__dirname</code> and <code>__filename</code> to false, I get a wrong absolute path:</p>
<p><code>/Users/vadorequest/dev/student-loan-simulator-serverless/aws/loan-advisor/.webpack/service/src</code></p>
<p>When I set them to true, I get a right relative path:</p>
<p><code>src</code></p>
<p>I use <code>console.log(__dirname)</code> to display the <code>__dirname</code>.</p>
<p>How to I get a right absolute path? Here is my webpack.config.js</p>
<div><pre>const slsw = require("serverless-webpack");
const nodeExternals = require("webpack-node-externals");

module.exports = {
  entry: slsw.lib.entries,
  target: "node",
  node: {
    __dirname: false,
    __filename: false,
  },
  // Generate sourcemaps for proper error messages
  devtool: 'source-map',
  // Since 'aws-sdk' is not compatible with webpack,
  // we exclude all node dependencies
  externals: [nodeExternals()],
  // Run babel on all .js files and skip those in node_modules
  module: {
    rules: [
      {
        test: /\.js$/,
        loader: "babel-loader",
        include: __dirname,
        exclude: /node_modules/
      }
    ]
  },
};</pre></div>
<h2>On AWS</h2>
<p>Whether I set <code>__dirname</code> and <code>__filename</code> to false or true, I get the following absolute path:</p>
<p><code>/var/task/src</code> -&gt; I have no idea if that's right or wrong path, but file loading is failing with <code>{"errorMessage":"Error: ENOENT: no such file or directory, open '/var/task/src/simulator.hbs'"}</code></p>
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
    
  <div id="issuecomment-373231500">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I used webpack 4.<br />
I try there workanoud that <code>node: {__dirname: true}</code>.<br />
However this workaround is not effect system.</p>
<p>I reinstall webpack 3.<br />
And <code>node: {__dirname: true}</code>.<br />
I confirmed that it is effective.</p>
<p>I think that webpack 4 disable to it workaround.</p>
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
    
  <div id="issuecomment-376306837">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/nfantone" target="_blank">nfantone</a>
  

    </strong>

    commented

    <a href="#issuecomment-376306837" target="_blank"><relative-time>on Mar 27</relative-time></a>


      
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

          <p>I encountered this issue today on an Electron + React project (working on macOS).</p>
<p>Doing <code>console.log(__dirname);</code> on a React component, I get:</p>
<ul>
<li>
<p>Using <code>{ target: 'electron-renderer', node: {__dirname: true} }</code> returns relative paths from build root (e.g.: <code>src/components</code>).</p>
</li>
<li>
<p>Using <code>{ target: 'electron-renderer', node: {__dirname: false} }</code> returns absolute paths pointing to <code>node_modules/electron/dist</code> (e.g.: <code>/Users/xxx/path/to/project/node_modules/electron/dist/Electron.app/Contents/Resources/myfile.js</code>)</p>
</li>
</ul>
<p>None of those worked for me. And none of those would be the expected <code>__dirname</code> value for a node module. I'm looking for the <strong>absolute path to the file I'm calling <code>console.log</code> from</strong>.</p>
<p>Is there a solution/workaround for this?</p>
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
    
  <div id="issuecomment-376308011">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>If you are on React, you would need to set <code>target</code> to <code>electron-renderer</code>. Still, I don't recommend using Node variables inside the <code>Electron Renderer</code>. You may want to call a IPC function from <code>Renderer</code> to <code>Main</code></p>
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
    
  <div id="issuecomment-376309510">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/michaeljota" target="_blank">@michaeljota</a> <code>electron-renderer</code> is what I'm using, yes. Edited my comment above. Makes absolutely no difference to <code>__dirname</code>, though.</p>
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
    
  <div id="issuecomment-376310561">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>You may want to call a IPC function from <code>Renderer</code> to <code>Main</code></p>
</blockquote>
<p>You want to access the root of your project, but <code>Renderer</code> thread does not have that info. Only <code>Main</code>.</p>
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
    
  <div id="issuecomment-376313399">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Ok, fair enough. But this being an Electron app is beyond the point. Let's move that detail out for a second.</p>
<p>What I'm after is to be able to pass the <strong>absolute path</strong> of a file under a certain directory on my project as a <code>file://</code> URI to a React component. What I'm seeing here is that all solutions proposed in this thread either don't work anymore of produce dubious results which I'm not sure they are useful and/or correct.</p>
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
    
  <div id="issuecomment-376314913">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>OK. I get the point, I don't know how to help. You maybe be able to call the IPC method on Electron, and use Electron to return the path you need. But, I don't think that you can do such task on Web only. Maybe you can ask on Stackover flow for something like this. Or you may want to try <code>target</code> to <code>browser</code> and see how that result at the end.</p>
<p>If you need to use modules from electron, using <code>require</code> you can use <code>window.require</code> instead of a simple <code>require</code>.</p>
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
    
  <div id="issuecomment-376330517">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/nfantone" target="_blank">@nfantone</a> I also did some tests and concluded that it wasn't really reliable. __dirname and __filename are non-properly working features when using webpack.</p>
<p>I kind of fixed my own issue, which was related to get the absolute path when hosting on AWS, but really it feels more like a monkey patch than a reliable solution.</p>
<p>Now, I have</p>
<pre><code>node: {
    __dirname: false,
    __filename: false,
  }
</code></pre>
<p>But I doubt very much it'll work on every environments the same way...</p>
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
    
  <div id="issuecomment-376520722">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/Vadorequest" target="_blank">@Vadorequest</a> Yes, my experience was similar. Unfortunately setting those two  to <code>false</code> makes <code>__dirname</code> point to<code>/path/to/project/node_modules/electron/dist/Electron.app/Contents/Resources/electron.asar/renderer</code>, which is rather useless.</p>
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
    
  <div id="issuecomment-376523234">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/nfantone" target="_blank">@nfantone</a> Excuse me if I'm wrong, that I guess I am, but if you were developing a React app that runs into the browser, how do you think it would work? What you want to do.</p>
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
    
  <div id="issuecomment-376526911">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/nfantone" target="_blank">nfantone</a>
  

    </strong>

    commented

    <a href="#issuecomment-376526911" target="_blank"><relative-time>on Mar 27</relative-time></a>


      
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

          <p><a href="https://github.com/michaeljota" target="_blank">@michaeljota</a> It doesn't run in the browser. It's an Electron app. But regardless of webpack's target, <code>__dirname</code> should conceptually point to the <em>directory name of the current module</em> (as decribed in <a href="https://nodejs.org/docs/latest/api/modules.html#modules_dirname" target="_blank">its docs</a>). That may change at runtime and it's certainly dependent on where/who runs the application. Perhaps it's my understanding of how the feature is supposed to work what's wrong here, but if webpack offers a way to emulate its behaviour, making it return <em>relative paths</em> (plain wrong, IMHO) or <em>absolute paths to a dependency in <code>node_modules</code></em> seems odd, to say the very least.</p>
<blockquote>
<p>What you want to do.</p>
</blockquote>
<p>Following <a href="https://github.com/webpack/webpack/issues/1599#issuecomment-376313399" target="_blank">my comment above</a>, I'm looking into preloading a JS script in a <code>&lt;webview&gt;</code> tag. The <code>preload</code> attribute requires a <code>file:</code> (or <code>asar:</code>) URI describing an <em>absolute path</em> to the script being preloaded.</p>
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
    
  <div id="issuecomment-376530355">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>If you can't make it work in the browser, then you won't be able to make it work that way.</p>
<p>The browser part from Electron, is just a regular Chrome browser. Electron makes available some global variables for you to use in the window object, but nothing else. So, you may want to take this approach instead. I think Electron injects a version of <code>__dirname</code> but I don't know, and have no idea where it resolves to.</p>
<p>The point is, this is not a Webpack issue I think. You need a runtime data, but all those variables are being assigned with constant values in the build process.</p>
<p>Think about this, you have several files in several folders, but this is when you are developing. At runtime, you just have one file. (probably).</p>
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
    
  <div id="issuecomment-376536414">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/michaeljota" target="_blank">@michaeljota</a> Not always true, I had this issue with a node.js application, and __dirname was useful to load a script using an absolute path. I was using webpack/babel for ES6+, and it's definitely related to webpack in my case.</p>
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
    
  <div id="issuecomment-376542294">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/michaeljota" target="_blank">@michaeljota</a> That is exactly why I expect <code>__dirname</code> to resolve to different paths depending on environment. Hence,</p>
<blockquote>
<p>That may change at runtime and it's certainly dependent on where/who runs the application.</p>
</blockquote>
<p>So the root path may be different, but my directories from there are the same between builds/development. My script is always under <code>/path/to/electron.app/lib/my-script.js</code>. Of course, <code>/path/to/electron.app</code> varies and is what I'm trying to reference using <code>__dirname</code>.</p>
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
    
  <div id="issuecomment-376551677">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I just build all the posibles options for this, with the minimum code to work:</p>
<div><pre>// app.js
console.log(__dirname);</pre></div>
<p>And this config</p>
<div><pre>// webpack.config.js
function generateConfig({ target, __dirname }) {
  return {
    entry: './app.js',
    output: {
      filename: `${target}-${__dirname}.js`,
    },
    target,
    node: {
      __dirname,
    },
  };
}

module.exports = [
  { target: 'node', __dirname: true },
  { target: 'node', __dirname: false },
  { target: 'web', __dirname: true },
  { target: 'web', __dirname: false },
  { target: 'webworker', __dirname: true },
  { target: 'webworker', __dirname: false },
  { target: 'electron-main', __dirname: true },
  { target: 'electron-main', __dirname: false },
  { target: 'electron-renderer', __dirname: true },
  { target: 'electron-renderer', __dirname: false },
].map(options =&gt; generateConfig(options));</pre></div>
<ul>
<li>When <code>__dirname</code> is set to true, in ALL configurations the variable was replaced with an empty string.</li>
<li>When <code>__dirname</code> was set to false, in ALL configurations the variable was NOT replaced.</li>
</ul>
<p>Conclusion:</p>
<p>This is more like a doc issue, because this is not explained properly, but I don't think Webpack is doing something wrong. This settings only let you to config Webpack if it should or should not replace the variable with the current relative path.</p>
<ul>
<li>
<p>If you are targeting any browser like environment, and you need the value of <code>__dirname</code> in run time you need to have a <code>__dirname</code> variable in the global scope.</p>
</li>
<li>
<p>If you are targeting any node like environment, then <code>__dirname</code> will resolve to the value that <code>node</code> provides.</p>
</li>
</ul>
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
    
  <div id="issuecomment-376553570">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/nfantone" target="_blank">@nfantone</a> In your case, I think that <code>Electron</code> is injecting its own version of <code>__dirname</code> as a constant value. I don't think this will ever resolve to the directory of your current file in the <code>renderer</code>.</p>
<p>However, you can use several approach to do what you want. You are able to <code>require</code> any module installed for Electron, from the <code>renderer</code> in runtime. I think you can <code>require</code> the native <code>path</code> module here, you could try that. Although, I have the need to say this is not a safe approach. You should never require low level APIs from Electron, and you should actually disable that feature. Use under your own risk.</p>
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
    
  <div id="issuecomment-376554310">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/Vadorequest" target="_blank">@Vadorequest</a> In your case, you just need <code>node</code> to resolve, and setting <code>__dirname</code> to false help you because this lets <code>node</code> to resolve instead of Webpack trying to resolve it. Again, don't think this is Webpack fault.</p>
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
    
  <div id="issuecomment-390163039">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/nfantone" target="_blank">@nfantone</a><br />
Hey, I am facing the exact same issue you were.<br />
Did you find a <em>safe</em> workaround for that?</p>
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
    
  <div id="issuecomment-390311032">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/AkshitKrNagpal" target="_blank">@AkshitKrNagpal</a> please read some others comments, and see if you find some <em>safe</em> workaround for that.</p>
<p>TL;DR: There is not a <em>workaround</em>, as this is the intended behavior.</p>
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
    
  <div id="issuecomment-390349694">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/jmca" target="_blank">jmca</a>
  

    </strong>

    commented

    <a href="#issuecomment-390349694" target="_blank"><relative-time>6 days ago</relative-time></a>


      
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

          <p>Regarding behavior with electron, my current dev env uses an express HMR webpack middleware to serve JS files specifically for Renderers. These files directly access node commonJS stuff.</p>
<p>This combination of Webpack config works for me:</p>
<pre><code>node: {
    __dirname: true,
},
  ...
target: 'electron-renderer',

</code></pre>
<p>From Webpack docs:</p>
<blockquote>
<p>node.__dirname<br />
true: The dirname of the input file relative to the context option.</p>
</blockquote>
<p>For "context":</p>
<blockquote>
<p>By default the current directory is used, but it's recommended to pass a value in your configuration</p>
</blockquote>
<p>For my project the "current directory" is fine because it is my project root.</p>
<p>Why <code>true</code>?<br />
<code>false</code> would always lead to the <code>index.html</code> dir that loads the JS bundle, so that doesn't help.<br />
<code>mock</code> would yield <code>/</code> which is definitely incorrect.</p>
<p>Now take for example a file in <code>PROJECT_ROOT/dirA/dirB/aFile</code><br />
Using <code>__dirname</code> in <code>aFile</code> will yield <code>dirA/dirB/aFile</code>.</p>
<p><code>path.resolve()</code> docs say:</p>
<blockquote>
<p>If after processing all given path segments an absolute path has not yet been generated, the current working directory is used.</p>
</blockquote>
<p>Since<code>__dirname</code> yields a relative path, "the current working directory" in this case is my project root.</p>
<p><code>path.resolve(__dirname)</code> correctly yields <code>/full/path/to/project/dirA/dirB/aFile</code>.</p>
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
    
  
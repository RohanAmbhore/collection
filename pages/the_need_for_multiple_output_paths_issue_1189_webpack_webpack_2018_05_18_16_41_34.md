<a href="https://github.com/webpack/webpack/issues/1189">https://github.com/webpack/webpack/issues/1189</a><div id="articleHeader"><h1>              The need for multiple output paths?            #1189    </h1></div>


  <div>
    
    <div>
        <a href="/activatedgeek" target="_blank">activatedgeek</a>  opened this Issue
        <relative-time>on Jun 24, 2015</relative-time>
        · 68 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-90590264">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I have the following use case,<br />
I am using <code>React</code> and along with that I have certain CSS files as dependencies. I have the following distribution folder tree:</p>
<pre><code>-- dist/
    --js/
    --css/
    --media/
</code></pre>
<p>Since, now I would like to include CSS into the build system, but now since I have my output path in the <code>webpack.config.js</code> to <code>./dist/js</code>, so even my CSS files are being generated there.</p>
<p>I think it is important to have multiple output paths. If not, could anybody suggest me any other workflow?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-114992043">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <div><pre>output: {
  path: path.resolve(__dirname, "./dist"),
  filename: "js/bundle.js"
},
... "css/bundle.css"</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-115109184">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hi, this is not clear exactly how to work. Also note that I have multiple entry points so here is what my <code>webpack.config.js</code> looks like:</p>
<div><pre>var webpack = require('webpack');

var CommonsChunkPlugin = webpack.optimize.CommonsChunkPlugin;
var ExtractTextPlugin = require("extract-text-webpack-plugin");

var entryPointsPathPrefix = './src/javascripts/pages';
var WebpackConfig = {
  entry : {
    a: entryPointsPathPrefix + '/a.jsx',
    b: entryPointsPathPrefix + '/b.jsx',
    c: entryPointsPathPrefix + '/c.jsx',
    d: entryPointsPathPrefix + '/d.jsx'
  },

  // send to distribution
  output: {
    path: './dist/js',
    filename: '[name].js'
  },

  module: {
    loaders: [
      // Babel transformer (the one and only)
      { test: /\.js(x)?$/, exclude: /node_modules/, loader: "babel-loader"},
      { test: /\.css$/, loader: ExtractTextPlugin.extract("style-loader", "css-loader")}
    ]
  },

  resolve: {
    // resolve file extensions
    extensions: ['.jsx', '.js', '']
  },

  plugins: [
    // separate common code
    new CommonsChunkPlugin('bundle.js'),
    new ExtractTextPlugin("[name].css")
  ]
};

module.exports = WebpackConfig;</pre></div>
<p>How do I specify file based outputs here?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-140934316">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>+1, I'd like to use this too and I don't understand the example you provided</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-156576084">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>The example from <a href="https://github.com/sokra" target="_blank">@sokra</a> wasnt exactly clear to me as well but it led me to a solution <g-emoji>👍</g-emoji></p>
<p>It works like this <a href="https://github.com/matthewmueller" target="_blank">@matthewmueller</a> <a href="https://github.com/activatedgeek" target="_blank">@activatedgeek</a></p>
<p>We assume <code>webpack.config.js</code> is in the root directory of your project.</p>
<div><pre>entry: {
  'build/application/bundle': './src/application', // will be  ./build/application/bundle.js,
  'build/library/bundle': './src/library`'// will be  ./build/library/bundle.js
},
output: {
  path: './',
  filename: '[name].js'
}</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  


  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-159123335">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/sashless" target="_blank">@sashless</a>  It sloves my problem,thanks.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-160036761">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/activatedgeek" target="_blank">@activatedgeek</a> you sloved the problem?  i think, i meet the same problem, but above answers don't slove my problem.</p>
<p>above answers, specify output files for "entry", but i want sepcify output files for "output"</p>
<p>for example:</p>
<div><pre>entry : {
  // this file require some files(like: big.png, big.css ...)
  // don't concat in one file, when output
  'index': './src/index.js'   
},
output: {
  path: './dist/'
}

//result of output path
dist/
  |-- js/index.js
  |-- css/big.css
  |-- img/big.png
</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-160063409">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>@epooren replace your paths with relative paths instead of file names</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-160068269">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/activatedgeek" target="_blank">@activatedgeek</a> thanks. Before i don't know that file-loader has name option.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-161638237">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>This solution work for the entry chunks but I still have the problem when I use webpack.ensure method.</p>
<ul>
<li>./webpack.conf.js</li>
</ul>
<div><pre>    var entry = {
        './build/admin/admin.js': './src/admin/main.es6')
    };

    var output = {
        path: './',
        filename: '[name].js'
    };</pre></div>
<ul>
<li>./src/admin/main.es6</li>
</ul>
<div><pre>        require.ensure(['./test'], (require) =&gt; {
            const test = require('./test')['default'];
            test.print();
        }, 'test')</pre></div>
<ul>
<li>./src/view/test.html</li>
</ul>
<div><pre>    &lt;script src="/assets/admin.js"&gt;&lt;/script&gt;</pre></div>
<p>Admin chunk is perfectly build into the correct location but the <code>test</code> chunk will be created into <code>./</code> and I would like to have it into <code>./build/core/</code></p>
<p>In this case I can modify my webpack.conf.js :</p>
<div><pre>    var output = {
        path: './',
        filename: '[name].js',
        chunkFilename: './build/core/[name].js'
    };</pre></div>
<p>By doing that, the webpack.ensure will not be able to find the <code>test</code> chunk because the location is now</p>
<pre><code>    /build/core/test.js
</code></pre>
<p>and not</p>
<pre><code>    /assets/test.js
</code></pre>
<p>like I would like</p>
<h3>My question is :</h3>
<p>How can I change the location of my non-entry chunks without affect the filename ?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-191156236">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>But the webpack-dev-server will not work .</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-191395062">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>+1 for multiple output files.</p>
<p>Also want to ask <a href="https://github.com/sokra" target="_blank">@sokra</a> what did he mean by his obscure answer. It is quite tactless of him to toss some info and disappear from conversation.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-210297427">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hello,<br />
When I'm runing only <code>webpack</code> and the directories <code>bar/dist/bundle</code> and <code>foo/dist/bundle</code> are created, but when I'm runing <code>webpack-dev-server</code> the log in terminal is ok, but nothing folder <code>dist</code> isn't created.</p>
<p>Does anyone know to solve it?</p>
<p>My <code>webpack-confing.js</code> bellow.</p>
<div><pre>var path = require("path");
var webpack = require("webpack");

module.exports = {
  entry: {
    "bar/dist/bundle": "./problems/bar/src/js",
    "foo/dist/bundle": "./problems/foo/src/js"
  },
  output: {
    path: path.resolve(__dirname, 'problems'),
    filename: "[name].js"
  },
  module: {
    loaders: [
      {
        loader: 'babel-loader',
        exclude: /node_modules/,
        test: /\.js$/,
        query: {
          presets: ['es2015', 'stage-0'],
        },
      }
    ]
  },
  stats: {
    colors: true
  },
  devtool: 'source-map'
};</pre></div>
<p>My script in <code>package.json</code> bellow</p>
<div><pre>"scripts": {
  "start": "webpack --progress --colors --watch",
  "server": "node_modules/webpack-dev-server/bin/webpack-dev-server.js"
},</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-210299683">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/igorapa" target="_blank">@igorapa</a> Please note that webpack-dev-server runs <em>in-memory</em>. It shouldn't generate any file output.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-210468858">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/bebraw" target="_blank">@bebraw</a> Then I need run both? Because I'd like to create this directories and have the autoreload.</p>
<p>With this command: <code>"start": "webpack --progress --colors --watch",</code> I have only the watch.</p>
<p>Do you have some alternative?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-210471986">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/igorapa" target="_blank">@igorapa</a> Why do you need the file output?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-210476381">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/bebraw" target="_blank">@bebraw</a> I have this project <a href="https://github.com/igorapa/toy-problems" target="_blank">https://github.com/igorapa/toy-problems</a></p>
<p>I configured so that each problem has its own folder <strong>dist</strong>.<br />
This <strong>dist</strong> directory is created when I run for example <strong>webpack</strong>.<br />
With only <strong>webpack</strong> I can have the <strong>watch</strong>, but can not get the browser autoreload so installed <strong>webpack-dev-server</strong>  to have autorelaod, but as you said, it does not generate these folder.</p>
<p>I just wanted a way to get the watch to run whenever any saved file and also have autoreload in the browser, I do not know the best way to implement this.</p>
<p>If you can clone my project to do a test or to send a PR, I'll be more than happy <g-emoji>😄</g-emoji></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-210477952">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/igorapa" target="_blank">@igorapa</a> I am still missing something obvious. Couldn't you use <a href="https://www.npmjs.com/package/browser-sync-webpack-plugin" target="_blank">browser-sync-webpack-plugin</a> with webpack-dev-server? I wouldn't know what to PR.</p>
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
    
  <div id="issuecomment-210711408">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/bebraw" target="_blank">@bebraw</a> Nice, this has solved my issue, but I left the <code>webpack-dev-server</code> out , I'm using only the <code>bowser-sync-webpack-plugin</code>  as you said.</p>
<p>If you want  do see, jump to my repository: <a href="https://github.com/igorapa/toy-problems" target="_blank">https://github.com/igorapa/toy-problems</a></p>
<p>Ps: PR === "Pull Request". <g-emoji>😄</g-emoji></p>
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
    
  <div id="issuecomment-215069915">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/sashless" target="_blank">@sashless</a> Do your way work with other file types? Say i want to process the SCSS in a folder instead of requiring them in the js file, something like this:</p>
<div><pre>entry: {
  'build/application/bundle': './src/application', // will be  ./build/application/bundle.js,
  'build/library/bundle': './src/library`'// will be  ./build/library/bundle.js,
  'build/assets/app.core': './src/assets/theme/app.core.scss`'// Should be  ./build/assets/app.core.css,
},
output: {
  path: './',
  filename: '[name].[ext]'
}</pre></div>
<p>However idk if the output filename need to change the extension for a replacement query, is it <code>[ext]</code> the one to replace for the extension of the different files?, does webpack even support dynamic extensions?</p>
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
    
  <div id="issuecomment-216053379">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>@luchillo You can add the extension to the entry keys. This worked for me:</p>
<pre><code>entry: {
  'js/app.js': './web/static/js/app.js',
  'js/vendor.js': ['react', 'react-dom'],
  'css/app.css': './web/static/css/app.scss',
},
 output: {
  path: "./priv/static",
  filename: "[name]",
},
</code></pre>
<p>Don't forget to update your plugins as well, e.g.</p>
<pre><code>plugins: [
  new webpack.optimize.CommonsChunkPlugin({name: 'js/vendor.js', children: true}),
  new ExtractTextPlugin('css/app.css', { allChunks: true }),
],
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
    
  <div id="issuecomment-216053718">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Awesome, what does that <code>allChunks</code> option in the <code>ExtractTextPlugin</code>?</p>
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
    
  <div id="issuecomment-216054181">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>@luchillo From the docs:<br />
<code>allChunks extract from all additional chunks too (by default it extracts only from the initial chunk(s))</code><br />
Can't tell you more than that <g-emoji>😕</g-emoji></p>
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
    
  <div id="issuecomment-216054263">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I guess that impacts bundle size, what about performance, that should take longer, isn't?</p>
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
    
  <div id="issuecomment-216329366">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/manubo" target="_blank">@manubo</a> Man putting the file ext in the entry key is brilliant, however i had the intent of using it with scss, but i haven't been unable to set up the input and loaders correctly, it alwas output some kind of js, i think it's outputting the embedded css instead of normal css.</p>
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
    
  <div id="issuecomment-220403391">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>@luchillo I think I found a better solution. No need to specify an entry point for stylesheets when using the ExtractTextPlugin:</p>
<pre><code>entry: {
  'js/app': './web/static/js/app.js',
  'js/vendor': ['react', 'react-dom'],
},
 output: {
  path: path.resolve(__dirname, 'priv/static'),
  filename: "[name]-[hash].js",
},
</code></pre>
<pre><code>plugins: [
    new ExtractTextPlugin('css/styles-[contenthash].css', { allChunks: true }),
],
</code></pre>
<p>You will need to require your root stylesheet, from which you <code>@import</code> all dependent stylesheets. E.g in <code>web/static/js/index.js</code></p>
<pre><code>import '../css/style.scss';
</code></pre>
<p>Better, e.g. because it allows you to add a hash to the generated the output files.</p>
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
    
  <div id="issuecomment-220460675">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>That's exactly what i don't want, since each time you save the file that made the import it will call the css loader even if you don't want it, i really want to be able to define it as an entry to separate my compilation of ts and scss apart.</p>
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
    
  <div id="issuecomment-227133370">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>The docs say that webpack will accept an array of configurations. I use this feature for building my app.js and specs.js files with completely different settings.</p>
<p>My <code>webpack.config.js</code> looks something like this:</p>
<pre><code>module.exports = [
  {
    entry: './app/app.js',
    output: {
      filename: './app.build/app.build.js'
    }
    // custom app settings
  },
  {
    entry: './specs/specs.js',
    output: {
      filename: './specs.build/specs.build.js'
    }
    // custom specs settings
  }
];
</code></pre>
<p>The two builds are separate from each other, and can have completely different settings.</p>
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
    
  <div id="issuecomment-227148932">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm using <code>webpack-merge</code> with env vars to change the config, you're saying i could use first config in that array for the js files and the second one for the css files and both would be used at the same time when calling the <code>webpack-dev-server</code>?</p>
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
    
  <div id="issuecomment-227153755">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>@luchillo - When you start webpack, all the configs will be processed in parallel. You could have a completely separate one for CSS if you like. It should work just fine with dev-server.</p>
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
    
  <div id="issuecomment-227191781">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>The thing is i have the structure like this:</p>
<div><pre>// webpack.common.js
module.exports = {
...
}

// webpack.dev.js
var commonConfig = require('./webpack.common.js'); // the settings that are common to prod and dev
module.exports = webpackMerge(commonConfig, {
...
}</pre></div>
<p>So i guess i would have to do something like:</p>
<div><pre>// webpack.common.js
module.exports = [{
  // Js one in index 0
}, {
  // Css one in index 1
}]

// webpack.dev.js
var commonConfig = require('./webpack.common.js'); // the settings that are common to prod and dev
module.exports = [
  webpackMerge(commonConfig[0], {
    // Merge only the js part of commonConfig with dev env specific configs
  }),
  commonConfig[1]
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
    
  <div id="issuecomment-227253977">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I agree this is a great option for building the files side by side when i need scss output aside of the js output.</p>
<p>But with this it becomes hard to make the <code>HMR</code> work and index.html tag with the <code>css</code> output will have to be hard-coded in the template of the <code>HtmlWebpackPlugin</code> since the config for this plugin is in the firs config.</p>
<p>Do you know how to separate the scss into another config, import output into the html template of the first config, and keep HMR working even with the second config?</p>
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
    
  <div id="issuecomment-232268276">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/sashless" target="_blank">@sashless</a><br />
Your solution is nice, however bundle resources are still in root of output directory.<br />
So for example I have fonts which after doing webpack stuff are still in the root of output and I want them in some specific location in there like: dir/resources</p>
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
    
  <div id="issuecomment-232354371">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/tscislo" target="_blank">@tscislo</a> I think that's the purpose of the <code>copy-webpack-plugin</code>.</p>
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
    
  <div id="issuecomment-232438432">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I fix that however now I have a problem that when I define my output like this:</p>
<pre><code>entry: {
  'application/bundle': './src/application',
},
output: {
  path: 'build',
  filename: '[name].build.js'
}
</code></pre>

<pre><code>new HtmlWebpackPlugin(
    {
        chunks: ['build/application/bundle'],
        template: './src/app/background/background.html',
        filename: ./'build/application/index.html',
        inject: 'body',
        hash: true
    })
</code></pre>
<p>Then in index.html I got he following reference to my build.js</p>
&lt;script src="../build/application/bundle.build.js?fdeb2df34a550cb35144"&gt;&lt;/script&gt;
<p>How to get rid of this '../build/application/' part of the path since my index.html is in the same folder as my bundle?</p>
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
    
  <div id="issuecomment-232455326">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>So to clarify, <code>index.html</code> is in same folder as <code>bundle.build.js</code>? Well, then your entry should be just <code>bundle</code> instead of <code>application/bundle</code>.</p>
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
    
  <div id="issuecomment-232458585">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I want it to be in application subdirectory for a purpose</p>
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
    
  <div id="issuecomment-232475445">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>So you have a <code>build</code> folder, within you have an <code>application</code> folder, in it you have both files.</p>
<p>So the bundle path in the HtmlWebpackPlugin should be just <code>bundle</code>, right?</p>
<p>Well, the plugin output path is the same as the webpack config, so first your filename should be <code>application/index.html</code>.</p>
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
        <h3 id="ref-issue-169063749">
      
        
      
        
  <a href="/rasvaan" target="_blank">rasvaan</a>
  

      referenced this issue
        in <strong>rasvaan/digibird_client</strong>
      <a href="#ref-issue-169063749" target="_blank">
        <relative-time>on Aug 3, 2016</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/rasvaan/digibird_client/issues/62" target="_blank">
          Webpack entry per page
          #62
        </a>
      </h4>
    

    

  
    0 of 2 tasks complete
    
      
    
  

  

</div>


</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-248627857">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/fredericgrati" target="_blank">@fredericgrati</a> how did you solve this promblem?</p>
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
    
  <div id="issuecomment-248637933">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I don't remember to have solved this problem with ensure method...<br />
I don't use/need it  :)</p>
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
    
  <div id="issuecomment-250060766">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Different entries indicates different pages, different page should build <strong>ALL</strong> resources to different output directory. In my scenario, if there is a substitution named <code>entryName</code> everything will be nice ^!^</p>
<div><pre>entry: {
  'pageA': './src/pageA/main.js',
  'pageB': './src/pageB/main.js',
},
output: {
  // output: /build/pageA/, /build/pageB/
  path: 'build/[entryName]/'
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
    
  <div id="issuecomment-250071866">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Is that from Webpack 2? i've never knew that we could use the entry name as parameter of the outputh path.</p>
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
    
  <div id="issuecomment-250081492">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Of course not, it was just my idea.  @luchillo</p>
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
    
  <div id="issuecomment-250166043">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Oh then let me ask, how would we define the output file name? would it be the same as the folder like <code>build/pageA/pageA.js</code> or something alike? unless we define directly the entry's output path that would just make the imports 1 folder longer.</p>
<p>I think maybe would be more beneficial to have a general output (default) and the entry if needed could define it's own output path:</p>
<div><pre>entry: {
  'pageA': './src/pageA/main.js',
  'pageB': {
      input: './src/pageB/main.js',
      output: 'build/pageAfolder/' // In this case pageB output overrides the output default
  }
},
output: {
  // Default output 'build/'
  path: 'build/'
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
    
  <div id="issuecomment-250167160">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <div><pre>entry: {
  'pageA': './src/pageA/main.js',
  'pageB': {
      input: './src/pageB/main.js',
      output: 'build/pageAfolder/' // In this case pageB output overrides the output default
  }
},</pre></div>
<p>I like this way. In my project i generate <code>entry</code> object dynamically, and want to set <code>output</code> folder for each <code>input</code> dynamically too. And all additional (not primary) chunks (should be relative to <code>output</code> path of main chunk.</p>
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
    
  <div id="issuecomment-258735305">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>+1 for being able to specify output for each entry (like @luchillo suggested).</p>
<p>It makes maintaining sub-domains (usually mapped as sub-folders in shared-hosting scenarios) easy, especially when each sub-domain could potentially have different styling and set of pages. Relative path resolution of the assets within the entry's output folder could address these kind of scenarios.</p>
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
    
  <div id="issuecomment-259129473">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I have the need for different <code>output</code> configurations for different entries. I want to give different names as <code>output.library</code>. I have an entry for the application code and two entries for locale specific translations. I'd like to publish the two locale specific entries with the <em>same</em> <code>output.library</code> name, but the entry for the application. Currently I need to hack around this, by using the name - which should be <code>output.library</code> - directly in my translations like <a href="https://github.com/donaldpipowitch/webpack-i18n-example/blob/master/i18n/de_DE.js#L1" target="_blank">module.exports['my-module-name'] = {}</a>.</p>
<p>Use case with description can be found here: <a href="https://github.com/donaldpipowitch/webpack-i18n-example" target="_blank">https://github.com/donaldpipowitch/webpack-i18n-example</a></p>
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
    
  <div id="issuecomment-259919350">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I just saw that you can use <code>ouput.library = ["MyLibrary", "[name]"];</code> where <code>[name]</code> is the name of my entry chunk. This will not work for me as my names are used <a href="https://github.com/donaldpipowitch/webpack-i18n-example/blob/master/webpack.config.js#L15" target="_blank">like file paths</a>. (Just like in <a href="https://github.com/webpack/webpack/issues/1189#issuecomment-156576084" target="_blank">this example</a>.)</p>
<p>Say my entries are:</p>
<pre><code>entry: {
  foo: "./some-file",
  bar: "./some-other-file"
},
</code></pre>
<p>I'd need something like this:</p>
<pre><code>ouput.library = {
  foo: 'my-library',
  bar: 'my-module-name'
};
</code></pre>

<pre><code>ouput.library = (name) =&gt; {
  switch(name) {
    case 'foo':
      return 'my-library';
    case 'bar':
      return 'my-module-name';
  }
};
</code></pre>
<p>I could imagine using something like this as well for the whole <code>output</code>:</p>
<pre><code>config.ouput = (name) =&gt; {
  switch(name) {
    case 'foo':
      return { /* output for 'foo' */ };
    case 'bar':
      return { /* output for 'bar' */ };
  }
};
</code></pre>
<p>@luchillo's example would also work.</p>
<p><a href="https://github.com/bebraw" target="_blank">@bebraw</a> Could this issue be re-opened?</p>
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
    
  <div id="issuecomment-260228081">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>After my last comment above, came across this <code>multi-compiler</code> option (ref. example <a href="https://github.com/webpack/webpack/tree/master/examples/multi-compiler" target="_blank">here</a>) that worked great for me (in being able to configure multiple outputs, multiple configurations, multiple sub-folders etc, each with its own specific configuration as well as inheriting from common configuration.).</p>
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
    
  <div id="issuecomment-260270231">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I tried it with <code>multi-compiler</code>, too. But sadly it didn't work for me. It looks like I can't share entry chunks between <code>multi-compiler</code> configs, but I need this to pass all scripts I need into <code>HtmlWebpackPlugin</code> (<a href="HtmlWebpackPlugin" target="_blank">example</a>).</p>
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
    
  <div id="issuecomment-262270911">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>i dont know guys... but something lead me here when i was trying to figure out a way of using two output configs...</p>
<p>in my case its not only changing the output dir or name.. as i am also setting Library..libraryTarget.... so on... what i am doing is im housing my CLI in the same repo as the source.. (as the CLI does require() the main module)... so i get it working by <code>module.exports = [main, cli]</code> exporting as an array... and it works :D not sure if it is official... or if will get dropped in the future thou...</p>
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
    
  <div id="issuecomment-262440754">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>That is the official <code>multi-compiler</code> config mentioned in the last two comments ;)</p>
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
    
  <div id="issuecomment-265082450">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Actually, there two questions here:</p>
<ul>
<li>how to make  <strong>entry</strong> file multiple output path like this: folder/entry.js</li>
<li>how to make <strong>chunkFile</strong> multiple output path like this: folder/chunk.js</li>
</ul>
<p>I just found a solution for this:</p>
<ul>
<li>generate entry file dynamically, result like this:</li>
</ul>
<div><pre>entry: {
  "index/index": "your actual entry file path",
  "home/index": "your actual entry file path"
}</pre></div>
<ul>
<li>store all your chunk files in some folder, output config would look like this:</li>
</ul>
<div><pre>output: {
    path: path.join(__dirname, publicPath),
    filename: '[name].js',
    chunkFilename: "chunk-[id]/[chunkhash:8].chunk.js",
    // make sure that publicPath end up with /
    publicPath: (publicPath+"/").replace(/\/\/$/, '/')
}</pre></div>
<p>It's easy to understand in entry case.<br />
Within chunkFile case, you really don't have to care about where chunkFile reside, webpack does the rest.<br />
Full code is here: <a href="https://github.com/jzzj/boilerplate/blob/master/webpack.config.js" target="_blank">webpack.config.js</a></p>
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
    
  <div id="issuecomment-292744571">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>What about having <code>[chunkhash]</code> for some entries and not for others? I think webpack cannot cover that use case.</p>
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
    
  <div id="issuecomment-302800911">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Here is a proof of concept project for Angular 4 that demonstrates some of the findings above:<br />
<a href="https://github.com/UIUXEngineering/web-worker-in-ng" target="_blank">web-worker-in-ng</a></p>
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
    
  <div id="issuecomment-312884152">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>My use case is an output for npm, and for a dir for a chrome extension.</p>
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
    
  <div id="issuecomment-313156281">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>What is the most simple way to get two outputs from the same entry? Do I have to use chunks?</p>
<p>I suppose I could just to a <code>cp</code> in my npm scrip.</p>
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
    
  <div id="issuecomment-317788684">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/tscislo" target="_blank">@tscislo</a>  how did you solve this promblem?</p>
<pre><code>new HtmlWebpackPlugin(
    {
        chunks: ['build/application/bundle'],
        template: './src/app/background/background.html',
        filename: ./'build/application/index.html',
        inject: 'body',
        hash: true
    })
</code></pre>
<p>Then in index.html I got he following reference to my build.js</p>
&lt;script src="../build/application/bundle.build.js?fdeb2df34a550cb35144"&gt;&lt;/script&gt;
<p>How to get rid of this '../build/application/' part of the path since my index.html is in the same folder as my bundle?</p>
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
    
  <div id="issuecomment-347488113">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>+1 to the ability of providing an output for each entry</p>
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
    
  <div id="issuecomment-348272459">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/jdomingorebollo" target="_blank">@jdomingorebollo</a> I wrote a plugin to do this after much searching around without finding a solution.</p>

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
    
  <div id="issuecomment-349374122">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>No plugins needed for multiple output paths :)</p>
<div><pre>const path = require('path');
const PATHS = {
    root: path.join(__dirname, ''),
    app: path.join(__dirname, 'app') 
};

entry: {
       // ./build/index.js
        'build/index': [
            '${PATHS.app}/app.js',
            '${PATHS.app}/app_2.js'
        ],

        // ./library.js
        './library': [
            '${PATHS.library}/library.js',
        ]
    },   
    output: {
        path: PATHS.root,
        filename: '[name].js'
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
    
  <div id="issuecomment-379525124">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/graknol" target="_blank">graknol</a>
  

    </strong>

    commented

    <a href="#issuecomment-379525124" target="_blank"><relative-time>on Apr 8</relative-time></a>


      
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

          <p>I finally figured out how to keep the entry names clean, while still controlling where they ended up. Utilizing some of the tricks here:</p>
<div><pre>entry: {
  public: './src/public/js/index.js',
  admin: './src/admin/js/index.js'
},
output: {
  filename: '[name]/[hash].bundle.js',
  path: path.resolve(__dirname, 'dist')
}</pre></div>
<p>Which resulted in:</p>
<p><a href="https://user-images.githubusercontent.com/1364029/38464104-4437e5da-3b08-11e8-99d0-0366d1daefbd.png" target="_blank" class="readableLinkWithMediumImage"><img src="https://user-images.githubusercontent.com/1364029/38464104-4437e5da-3b08-11e8-99d0-0366d1daefbd.png" alt="bilde" /></a></p>
<p>With this setup, my HtmlWebpackPlugin, CommonsChunkPlugin & friends could reference the chunks with clean descriptive names.</p>
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
    
  <div id="issuecomment-382256608">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/tatthien" target="_blank">tatthien</a>
  

    </strong>

    commented

    <a href="#issuecomment-382256608" target="_blank"><relative-time>on Apr 18</relative-time></a>


      
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

          <p><a href="https://github.com/sashless" target="_blank">@sashless</a> 's solution solves my problem.</p>
<p>Here is my setup:</p>
<div><pre>let entry = {
 'admin/global.js': 'path-to-admin-global.js',
 'front/global.js': 'path-to-front-global.js'
}</pre></div>
<div><pre>  entry: entry,
  output: {
    path: path.resolve(__dirname, 'dist/js'),
    publicPath: path.resolve(__dirname, 'dist'),
    filename: '[name].js'
  },</pre></div>
<p>After build, webpack will generate 2 directories <code>admin</code> and <code>front</code> inside <code>dist/js</code></p>
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
    
  <div id="issuecomment-388520750">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>So I've watched and I've watched.</p>
<p>Is there still no practical solution to outputting files into different directories? Not everyone (and frankly it slows the hell out of development time if you're not using the webpack-dev-server or its lot). I develop python-backed apps, so I don't really care about those things (and they're plugins anyway! So let the plugin makers deal with it, if you must)</p>
<p>The given solution of</p>
<div><pre>entry: {
  'build/application/bundle': './src/application', // will be  ./build/application/bundle.js,
  'build/library/bundle': './src/library`'// will be  ./build/library/bundle.js,
  'build/assets/app.core': './src/assets/theme/app.core.scss`'// Should be  ./build/assets/app.core.css,
},
output: {
  path: './',
  filename: '[name].[ext]'
}</pre></div>
<p>fails in webpack 4, I've tried every variant I could. Mostly due to the fact that it doesn't seem to be able to resolve relative directories anymore, even with context being set.</p>
<p>for instance:</p>
<pre><code>entry: {
    "example/index/static/js": path.resolve("src/index"),
    "example/admin/static/js": path.resolve("src/admin"),
    "example/teams/static/js": path.resolve("src/teams"),
    "example/reports/static/js": path.resolve("src/reports"),
  },
  output: {
    path: path.resolve(__dirname),
    filename: "[name].js",
  },
</code></pre>
<p>nor does this work:</p>
<pre><code>entry: {
    "example/index/static/js": "./src/index",
    "example/admin/static/js": "./"src/admin",
    "example/teams/static/js": "./src/teams",
    "example/reports/static/js": "./src/reports"
  },
  output: {
    path: "./",
    filename: "[name].js",
  },
</code></pre>
<p>Even having the path entries as path.resolve(__dirname, "src/index") made no difference, in case thats relevant somehow.</p>
<p>Both fail. It follows the exact same idea as the solution above.</p>
<p>Is this not intended to be addressed? I can't even find a good community plugin and to be honest this seems like an oversight.</p>
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
    
  
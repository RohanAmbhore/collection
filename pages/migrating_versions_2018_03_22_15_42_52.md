<a href="https://webpack.js.org/guides/migrating/#module-loaders-is-now-module-rules">https://webpack.js.org/guides/migrating/#module-loaders-is-now-module-rules</a><div id="articleHeader"><h1>Migrating Versions</h1></div><div><a href="https://github.com/webpack/webpack.js.org/edit/master/src/content/guides/migrating.md" target="_blank">Edit Document</a></div><p>The following sections describe the major changes from webpack 1 to 2.</p>
<blockquote><div> Note that there were far fewer changes between 2 and 3, so that migration shouldn't be too bad. If you are running into issues, please see <a href="https://github.com/webpack/webpack/releases" target="_blank">the changelog</a> for details. </div></blockquote><blockquote><div> This content may be moved to the blog post in the near future as version 2 has been out for a while. On top of that, version 3 was recently released and version 4 is on the horizon. As noted above, folks should instead to refer to <a href="https://github.com/webpack/webpack/releases" target="_blank">the changelog</a> for migrations. </div></blockquote><h2><code>resolve.root</code>, <code>resolve.fallback</code>, <code>resolve.modulesDirectories</code></h2>
<p>These options were replaced by a single option <code>resolve.modules</code>. See <a href="/configuration/resolve" target="_blank">resolving</a> for more usage.</p>
<pre><code>  resolve: {
-   root: path.join(__dirname, "src")
+   modules: [
+     path.join(__dirname, "src"),
+     "node_modules"
+   ]
  }
</code></pre>
<h2><code>resolve.extensions</code></h2>
<p>This option no longer requires passing an empty string. This behavior was moved to <code>resolve.enforceExtension</code>. See <a href="/configuration/resolve" target="_blank">resolving</a> for more usage.</p>
<h2><code>resolve.*</code></h2>
<p>Several APIs were changed here. Not listed in detail as it's not commonly used. See <a href="/configuration/resolve" target="_blank">resolving</a> for details.</p>
<h2><code>module.loaders</code> is now <code>module.rules</code></h2>
<p>The old loader configuration was superseded by a more powerful rules system, which allows configuration of loaders and more.
For compatibility reasons, the old <code>module.loaders</code> syntax is still valid and the old names are parsed.
The new naming conventions are easier to understand and are a good reason to upgrade the configuration to using <code>module.rules</code>.</p>
<pre><code>  module: {
-   loaders: [
+   rules: [
      {
        test: /\.css$/,
-       loaders: [
-         "style-loader",
-         "css-loader?modules=true"
+       use: [
+         {
+           loader: "style-loader"
+         },
+         {
+           loader: "css-loader",
+           options: {
+             modules: true
+           }
+         }
        ]
      },
      {
        test: /\.jsx$/,
        loader: "babel-loader", // Do not use "use" here
        options: {
          // ...
        }
      }
    ]
  }
</code></pre>
<h2>Chaining loaders</h2>
<p>Like in webpack 1, loaders can be chained to pass results from loader to loader. Using the <a href="/configuration/module#rule-use" target="_blank">rule.use</a>
 configuration option, <code>use</code> can be set to an array of loaders.
In webpack 1, loaders were commonly chained with <code>!</code>. This style is only supported using the legacy option <code>module.loaders</code>.</p>
<pre><code>  module: {
-   loaders: [{
+   rules: [{
      test: /\.less$/,
-     loader: "style-loader!css-loader!less-loader"
+     use: [
+       "style-loader",
+       "css-loader",
+       "less-loader"
+     ]
    }]
  }
</code></pre>
<h2>Automatic <code>-loader</code> module name extension removed</h2>
<p>It is not possible anymore to omit the <code>-loader</code> extension when referencing loaders:</p>
<pre><code>  module: {
    rules: [
      {
        use: [
-         "style",
+         "style-loader",
-         "css",
+         "css-loader",
-         "less",
+         "less-loader",
        ]
      }
    ]
  }
</code></pre>
<p>You can still opt-in to the old behavior with the <code>resolveLoader.moduleExtensions</code> configuration option, but this is not recommended.</p>
<pre><code>+ resolveLoader: {
+   moduleExtensions: ["-loader"]
+ }
</code></pre>
<p>See <a href="https://github.com/webpack/webpack/issues/2986" target="_blank">#2986</a> for the reason behind this change.</p>
<h2><code>json-loader</code> is not required anymore</h2>
<p>When no loader has been configured for a JSON file, webpack will automatically try to load the JSON
file with the <a href="https://github.com/webpack/json-loader" target="_blank"><code>json-loader</code></a>.</p>
<pre><code>  module: {
    rules: [
-     {
-       test: /\.json/,
-       loader: "json-loader"
-     }
    ]
  }
</code></pre>
<p><a href="https://github.com/webpack/webpack/issues/3363" target="_blank">We decided to do this</a> in order to iron out environment differences
  between webpack, node.js and browserify.</p>
<h2>Loaders in configuration resolve relative to context</h2>
<p>In <strong>webpack 1</strong>, configured loaders resolve relative to the matched file. However, in <strong>webpack 2</strong>, configured loaders resolve relative to the <code>context</code> option.</p>
<p>This solves some problems with duplicate modules caused by loaders when using <code>npm link</code> or referencing modules outside of the <code>context</code>.</p>
<p>You may remove some hacks to work around this:</p>
<pre><code>  module: {
    rules: [
      {
        // ...
-       loader: require.resolve("my-loader")
+       loader: "my-loader"
      }
    ]
  },
  resolveLoader: {
-   root: path.resolve(__dirname, "node_modules")
  }
</code></pre>
<h2><code>module.preLoaders</code> and <code>module.postLoaders</code> were removed:</h2>
<pre><code>  module: {
-   preLoaders: [
+   rules: [
      {
        test: /\.js$/,
+       enforce: "pre",
        loader: "eslint-loader"
      }
    ]
  }
</code></pre>
<h2><code>UglifyJsPlugin</code> sourceMap</h2>
<p>The <code>sourceMap</code> option of the <code>UglifyJsPlugin</code> now defaults to <code>false</code> instead of <code>true</code>. This means that if you are using source maps for minimized code or want correct line numbers for uglifyjs warnings, you need to set <code>sourceMap: true</code> for <code>UglifyJsPlugin</code>.</p>
<pre><code>  devtool: "source-map",
  plugins: [
    new UglifyJsPlugin({
+     sourceMap: true
    })
  ]
</code></pre>
<h2><code>UglifyJsPlugin</code> warnings</h2>
<p>The <code>compress.warnings</code> option of the <code>UglifyJsPlugin</code> now defaults to <code>false</code> instead of <code>true</code>.
This means that if you want to see uglifyjs warnings, you need to set <code>compress.warnings</code> to <code>true</code>.</p>
<pre><code>  devtool: "source-map",
  plugins: [
    new UglifyJsPlugin({
+     compress: {
+       warnings: true
+     }
    })
  ]
</code></pre>
<h2><code>UglifyJsPlugin</code> minimize loaders</h2>
<p><code>UglifyJsPlugin</code> no longer switches loaders into minimize mode. The <code>minimize: true</code> setting needs to be passed via loader options in the long-term. See loader documentation for relevant options.</p>
<p>The minimize mode for loaders will be removed in webpack 3 or later.</p>
<p>To keep compatibility with old loaders, loaders can be switched to minimize mode via plugin:</p>
<pre><code>  plugins: [
+   new webpack.LoaderOptionsPlugin({
+     minimize: true
+   })
  ]
</code></pre>
<h2><code>DedupePlugin</code> has been removed</h2>
<p><code>webpack.optimize.DedupePlugin</code> isn't needed anymore. Remove it from your configuration.</p>
<h2><code>BannerPlugin</code> - breaking change</h2>
<p><code>BannerPlugin</code> no longer accepts two parameters, but a single options object.</p>
<pre><code>  plugins: [
-    new webpack.BannerPlugin('Banner', {raw: true, entryOnly: true});
+    new webpack.BannerPlugin({banner: 'Banner', raw: true, entryOnly: true});
  ]
</code></pre>
<h2><code>OccurrenceOrderPlugin</code> is now on by default</h2>
<p>The <code>OccurrenceOrderPlugin</code> is now enabled by default and has been renamed (<code>OccurenceOrderPlugin</code> in webpack 1).
Thus make sure to remove the plugin from your configuration:</p>
<pre><code>  plugins: [
    // webpack 1
-   new webpack.optimize.OccurenceOrderPlugin()
    // webpack 2
-   new webpack.optimize.OccurrenceOrderPlugin()
  ]
</code></pre>
<h2><code>ExtractTextWebpackPlugin</code> - breaking change</h2>
<p><a href="https://github.com/webpack/extract-text-webpack-plugin" target="_blank">ExtractTextPlugin</a> requires version 2 to work with webpack 2.</p>
<p><code>npm install --save-dev extract-text-webpack-plugin</code></p>
<p>The configuration changes for this plugin are mainly syntactical.</p>
<h3><code>ExtractTextPlugin.extract</code></h3>
<pre><code>module: {
  rules: [
    {
      test: /.css$/,
-      loader: ExtractTextPlugin.extract("style-loader", "css-loader", { publicPath: "/dist" })
+      use: ExtractTextPlugin.extract({
+        fallback: "style-loader",
+        use: "css-loader",
+        publicPath: "/dist"
+      })
    }
  ]
}
</code></pre>
<h3><code>new ExtractTextPlugin({options})</code></h3>
<pre><code>plugins: [
-  new ExtractTextPlugin("bundle.css", { allChunks: true, disable: false })
+  new ExtractTextPlugin({
+    filename: "bundle.css",
+    disable: false,
+    allChunks: true
+  })
]
</code></pre>
<h2>Full dynamic requires now fail by default</h2>
<p>A dependency with only an expression (i. e. <code>require(expr)</code>) will now create an empty context instead of the context of the complete directory.</p>
<p>Code like this should be refactored as it won't work with ES2015 modules. If this is not possible you can use the <code>ContextReplacementPlugin</code> to hint the compiler towards the correct resolving.</p>
<blockquote><div> Link to an article about dynamic dependencies. </div></blockquote><h3>Using custom arguments in CLI and configuration</h3>
<p>If you abused the CLI to pass custom arguments to the configuration like so:</p>
<p><code>webpack --custom-stuff</code></p>
<pre><code>// webpack.config.js
var customStuff = process.argv.indexOf("--custom-stuff") &gt;= 0;
/* ... */
module.exports = config;
</code></pre>
<p>You may notice that this is no longer allowed. The CLI is more strict now.</p>
<p>Instead there is an interface for passing arguments to the configuration. This should be used instead. Future tools may rely on this.</p>
<p><code>webpack --env.customStuff</code></p>
<pre><code>module.exports = function(env) {
  var customStuff = env.customStuff;
  /* ... */
  return config;
};
</code></pre>
<p>See <a href="/api/cli" target="_blank">CLI</a>.</p>
<h2><code>require.ensure</code> and AMD <code>require</code> are asynchronous</h2>
<p>These functions are now always asynchronous instead of calling their callback synchronously if the chunk is already loaded.</p>
<p><strong><code>require.ensure</code> now depends upon native <code>Promise</code>s. If using <code>require.ensure</code> in an environment that lacks them then you will need a polyfill. </strong></p>
<h2>Loader configuration is through <code>options</code></h2>
<p>You can <em>no longer</em> configure a loader with a custom property in the <code>webpack.config.js</code>. It must be done through the <code>options</code>. The following configuration with the <code>ts</code> property is no longer valid with webpack 2:</p>
<pre><code>module.exports = {
  ...
  module: {
    rules: [{
      test: /\.tsx?$/,
      loader: 'ts-loader'
    }]
  },
  // does not work with webpack 2
  ts: { transpileOnly: false }
}
</code></pre>
<h3>What are <code>options</code>?</h3>
<p>Good question. Well, strictly speaking it's 2 possible things; both ways to configure a webpack loader. Classically <code>options</code> was called <code>query</code> and was a string which could be appended to the name of the loader. Much like a query string but actually with <a href="https://github.com/webpack/loader-utils#parsequery" target="_blank">greater powers</a>:</p>
<pre><code>module.exports = {
  ...
  module: {
    rules: [{
      test: /\.tsx?$/,
      loader: 'ts-loader?' + JSON.stringify({ transpileOnly: false })
    }]
  }
}
</code></pre>
<p>But it can also be a separately specified object that's supplied alongside a loader:</p>
<pre><code>module.exports = {
  ...
  module: {
    rules: [{
      test: /\.tsx?$/,
      loader: 'ts-loader',
      options:  { transpileOnly: false }
    }]
  }
}
</code></pre>
<h2><code>LoaderOptionsPlugin</code> context</h2>
<p>Some loaders need context information and read them from the configuration. This needs to be passed via loader options in the long-term. See loader documentation for relevant options.</p>
<p>To keep compatibility with old loaders, this information can be passed via plugin:</p>
<pre><code>  plugins: [
+   new webpack.LoaderOptionsPlugin({
+     options: {
+       context: __dirname
+     }
+   })
  ]
</code></pre>
<h2><code>debug</code></h2>
<p>The <code>debug</code> option switched loaders to debug mode in webpack 1. This needs to be passed via loader options in long-term. See loader documentation for relevant options.</p>
<p>The debug mode for loaders will be removed in webpack 3 or later.</p>
<p>To keep compatibility with old loaders, loaders can be switched to debug mode via a plugin:</p>
<pre><code>- debug: true,
  plugins: [
+   new webpack.LoaderOptionsPlugin({
+     debug: true
+   })
  ]
</code></pre>
<h2>Code Splitting with ES2015</h2>
<p>In webpack 1, you could use <a href="/api/module-methods#require-ensure" target="_blank"><code>require.ensure()</code></a> as a method to lazily-load chunks for your application:</p>
<pre><code>require.ensure([], function(require) {
  var foo = require("./module");
});
</code></pre>
<p>The ES2015 Loader spec defines <a href="/api/module-methods#import-" target="_blank"><code>import()</code></a> as method to load ES2015 Modules dynamically on runtime. webpack treats <code>import()</code> as a split-point and puts the requested module in a separate chunk. <code>import()</code> takes the module name as argument and returns a Promise.</p>
<pre><code>function onClick() {
  import("./module").then(module =&gt; {
    return module.default;
  }).catch(err =&gt; {
    console.log("Chunk loading failed");
  });
}
</code></pre>
<p>Good news: Failure to load a chunk can now be handled because they are <code>Promise</code> based.</p>
<h2>Dynamic expressions</h2>
<p>It's possible to pass a partial expression to <code>import()</code>. This is handled similar to expressions in CommonJS (webpack creates a <a href="https://webpack.github.io/docs/context.html" target="_blank">context</a> with all possible files).</p>
<p><code>import()</code> creates a separate chunk for each possible module.</p>
<pre><code>function route(path, query) {
  return import(`./routes/${path}/route`)
    .then(route =&gt; new route.Route(query));
}
// This creates a separate chunk for each possible route
</code></pre>
<h2>Mixing ES2015 with AMD and CommonJS</h2>
<p>As for AMD and CommonJS you can freely mix all three module types (even within the same file). webpack behaves similar to babel and node-eps in this case:</p>
<pre><code>// CommonJS consuming ES2015 Module
var book = require("./book");

book.currentPage;
book.readPage();
book.default === "This is a book";
</code></pre>
<pre><code>// ES2015 Module consuming CommonJS
import fs from "fs"; // module.exports map to default
import { readFileSync } from "fs"; // named exports are read from returned object+

typeof fs.readFileSync === "function";
typeof readFileSync === "function";
</code></pre>
<p>It is important to note that you will want to tell Babel to not parse these module symbols so webpack can use them. You can do this by setting the following in your <code>.babelrc</code> or <code>babel-loader</code> options.</p>
<p><strong>.babelrc</strong></p>
<pre><code>{
  "presets": [
    ["es2015", { "modules": false }]
  ]
}
</code></pre>
<h2>Hints</h2>
<p>No need to change something, but opportunities</p>
<h3>Template strings</h3>
<p>webpack now supports template strings in expressions. This means you can start using them in webpack constructs:</p>
<pre><code>- require("./templates/" + name);
+ require(`./templates/${name}`);
</code></pre>
<h3>Configuration Promise</h3>
<p>webpack now supports returning a <code>Promise</code> from the configuration file. This allows async processing in your configuration file.</p>
<p><strong>webpack.config.js</strong></p>
<pre><code>module.exports = function() {
  return fetchLangs().then(lang =&gt; ({
    entry: "...",
    // ...
    plugins: [
      new DefinePlugin({ LANGUAGE: lang })
    ]
  }));
};
</code></pre>
<h3>Advanced loader matching</h3>
<p>webpack now supports more things to match on for loaders.</p>
<pre><code>module: {
  rules: [
    {
      resource: /filename/, // matches "/path/filename.js"
      resourceQuery: /^\?querystring$/, // matches "?querystring"
      issuer: /filename/, // matches "/path/something.js" if requested from "/path/filename.js"
    }
  ]
}
</code></pre>
<h3>More CLI options</h3>
<p>There are some new CLI options for you to use:</p>
<p><code>--define process.env.NODE_ENV="production"</code> See <a href="/plugins/define-plugin/" target="_blank"><code>DefinePlugin</code></a>.</p>
<p><code>--display-depth</code> displays the distance to the entry point for each module.</p>
<p><code>--display-used-exports</code> display info about which exports are used in a module.</p>
<p><code>--display-max-modules</code> sets the number for modules displayed in the output (defaults to 15).</p>
<p><code>-p</code> also defines <code>process.env.NODE_ENV</code> to <code>"production"</code> now.</p>
<h2>Loader changes</h2>
<p>Changes only relevant for loader authors.</p>
<h3>Cacheable</h3>
<p>Loaders are now cacheable by default. Loaders must opt-out if they are not cacheable.</p>
<pre><code>  // Cacheable loader
  module.exports = function(source) {
-   this.cacheable();
    return source;
  }
</code></pre>
<pre><code>  // Not cacheable loader
  module.exports = function(source) {
+   this.cacheable(false);
    return source;
  }
</code></pre>
<h3>Complex options</h3>
<p><strong>webpack 1</strong> only supports <code>JSON.stringify</code>-able options for loaders.</p>
<p><strong>webpack 2</strong> now supports any JS object as loader options.</p>
<p>Before webpack <a href="https://github.com/webpack/webpack/releases/tag/v2.2.1" target="_blank">2.2.1</a> (i.e. from 2.0.0 through 2.2.0), using complex options required using <code>ident</code> for the <code>options</code> object to allow its reference from other loaders. <strong>This was removed in 2.2.1</strong> and thus current migrations do not require any use of the <code>ident</code> key.</p>
<pre><code>{
  test: /\.ext/
  use: {
    loader: '...',
    options: {
-     ident: 'id',
      fn: () =&gt; require('./foo.js')
    }
  }
}
</code></pre>

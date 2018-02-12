<a href="https://alligator.io/vuejs/basic-ssr/">https://alligator.io/vuejs/basic-ssr/</a><div id="articleHeader"><h1>Basic Server Side Rendering with Vue.js and Express</h1></div><a href="/author/joshua-bemenderfer" target="_blank">Joshua Bemenderfer</a> <time>March 14, 2017</time></header><p>Server side rendering (SSR) is one of those things that’s long been touted as one of the greatest strengths of <em>React</em>, <em>Angular 2+</em>, and <em>Vue 2</em>. It allows you to render your apps on the server, then hydrate them with client side reactivity after the page loads, greatly increasing the responsiveness and improving the load time of your pages.</p><p>Unfortunately, it’s not the most obvious thing to set up, and the documentation for rendering Vue.js apps on the server is spread across several places. Hopefully this guide should help clear things up for you. :)</p><h2 id="installation">Installation</h2><p>We’ll start with <a href="https://github.com/vuejs/vue-cli" target="_blank">vue-cli’s</a> <a href="https://github.com/vuejs-templates/webpack-simple" target="_blank">webpack-simple</a> template to give us a common base to work with.</p><div><div><pre><code># Create the project
$ vue init webpack-simple vue-ssr-example
$ cd vue-ssr-example

# Install dependencies
$ yarn # (or npm install)
</code></pre></div></div><p>We’ll also need three other packages, <em>express</em> for the server, <em>vue-server-renderer</em> to render the bundle, which is produced by <em>vue-ssr-webpack-plugin</em>.</p><div><div><pre><code># Install with yarn ...
$ yarn add express vue-server-renderer
$ yarn add vue-ssr-webpack-plugin -D # Add this as a development dependency as we don't need it in production.

# ... or with NPM
$ npm install express vue-server-renderer
$ npm install vue-ssr-webpack-plugin -D
</code></pre></div></div><h2 id="preparing-the-app">Preparing the App</h2><p>The <em>webpack-simple</em> template doesn’t come with SSR capability right out of the box. There are a few things we’ll have to configure first.</p><p>The first thing to do is create a separate entry file for the server. Right now the client entry is in <em>main.js</em>. Let’s copy that and create <em>main.server.js</em> from it. The modifications are fairly simple. We just need to remove the <em>el</em> reference and return the app in the default export.</p><p>src/main.server.js</p><div><div><pre><code>import Vue from 'vue';
import App from './App.vue';

// Receives the context of the render call, returning a Promise resolution to the root Vue instance.
export default context =&gt; {
  return Promise.resolve(
    new Vue({
      render: h =&gt; h(App)
    })
  );
}
</code></pre></div></div><p>We also need to modify <em>index.html</em> a bit to prepare it for SSR.</p><p>Replace <em>&lt;div id=”app”&gt;&lt;/div&gt;</em> with <em>&lt;!–vue-ssr-outlet–&gt;</em>, like so:</p><div><div><pre><code>&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
  &lt;head&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;title&gt;vue-ssr-example&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;!--vue-ssr-outlet--&gt;
    &lt;script src="/dist/build.js"&gt;&lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre></div></div><h2 id="webpack-configuration">Webpack Configuration</h2><p>Now, we need a separate webpack configuration file to render the server bundle. Copy <em>webpack.config.js</em> into a new file, <em>webpack.server.config.js</em>.</p><p>There are a few changes we’ll need to make:</p><p>webpack.server.config.js</p><div><div><pre><code>const path = require('path')
const webpack = require('webpack')
// Load the Vue SSR plugin. Don't forget this. :P
const VueSSRPlugin = require('vue-ssr-webpack-plugin')

module.exports = {
  // The target should be set to "node" to avoid packaging built-ins.
  target: 'node',
  // The entry should be our server entry file, not the default one.
  entry: './src/main.server.js',
  output: {
    path: path.resolve(__dirname, './dist'),
    publicPath: '/dist/',
    filename: 'build.js',
    // Outputs node-compatible modules instead of browser-compatible.
    libraryTarget: 'commonjs2'
  },
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: {
          loaders: {
          }
          // other vue-loader options go here
        }
      },
      {
        test: /\.js$/,
        loader: 'babel-loader',
        exclude: /node_modules/
      },
      {
        test: /\.(png|jpg|gif|svg)$/,
        loader: 'file-loader',
        options: {
          name: '[name].[ext]?[hash]'
        }
      }
    ]
  },
  resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  },
  // We can remove the devServer block.
  performance: {
    hints: false
  },
  // Avoids bundling external dependencies, so node can load them directly from node_modules/
  externals: Object.keys(require('./package.json').dependencies),
  devtool: 'source-map',
  // No need to put these behind a production env variable.
  plugins: [
    // Add the SSR plugin here.
    new VueSSRPlugin(),
    new webpack.DefinePlugin({
      'process.env': {
        NODE_ENV: '"production"'
      }
    }),
    new webpack.optimize.UglifyJsPlugin({
      sourceMap: true,
      compress: {
        warnings: false
      }
    }),
    new webpack.LoaderOptionsPlugin({
      minimize: true
    })
  ]
}
</code></pre></div></div><h2 id="build-config">Build Config</h2><p>To simplify development, let’s update the build scripts in <em>package.json</em> to build both the client and server webpack bundles.</p><p>Replace the single <em>build</em> script with these three. Usage stays the same, but you can now build the client or server bundles individually with <em>build:client</em> and <em>build:server</em>, respectively.</p><p>package.json (partial)</p><div><div><pre><code>{
  ...
  "scripts": {
    ...
    "build": "npm run build:server && npm run build:client",
    "build:client": "cross-env NODE_ENV=production webpack --progress --hide-modules",
    "build:server": "cross-env NODE_ENV=production webpack --config webpack.server.config.js --progress --hide-modules"
  },
  ...
}
</code></pre></div></div><h2 id="server-script">Server Script</h2><p>Now, we need the server script to, well, render the application.</p><p>server.js (partial)</p><div><div><pre><code>#!/usr/bin/env node

const fs = require('fs');
const express = require('express');
const { createBundleRenderer } = require('vue-server-renderer');

const bundleRenderer = createBundleRenderer(
  // Load the SSR bundle with require.
  require('./dist/vue-ssr-bundle.json'),
  {
    // Yes, I know, readFileSync is bad practice. It's just shorter to read here.
    template: fs.readFileSync('./index.html', 'utf-8')
  }
);

// Create the express app.
const app = express();

// Serve static assets from ./dist on the /dist route.
app.use('/dist', express.static('dist'));

// Render all other routes with the bundleRenderer.
app.get('*', (req, res) =&gt; {
  bundleRenderer
    // Renders directly to the response stream.
    // The argument is passed as "context" to main.server.js in the SSR bundle.
    .renderToStream({url: req.path})
    .pipe(res);
});

// Bind the app to this port.
app.listen(8080);
</code></pre></div></div><h2 id="running-the-app">Running the App</h2><p>If all goes well, you should be able build the bundle and run the server with:</p><div><div><pre><code># Build client and server bundles.
$ npm run build
# Run the HTTP server.
$ node ./server.js
</code></pre></div></div><p>If you visit <em>http://localhost:8080</em>, everything should look… the same. However, if you disable JavaScript, everything will still look the same, because the app is being rendered on the server first.</p><hr /><h2 id="caveats">Caveats</h2><ul><li>Any modules that are loaded from <em>node_modules</em> instead of the bundle cannot be able to be changed across requests, (ie, have a global state.) Otherwise you will get inconsistent results when rendering your application.</li><li>Make sure you write your tables properly (include the <em>thead</em> and/or <em>tbody</em> wrapper elements.) The client-side version can detect these issues, but the server-side version cannot, which can result in hydration inconsistencies.</li></ul><h2 id="bonus-round">Bonus Round</h2><ul><li>Try making the app display something different depending on whether it was rendered on the client or the server. <strong>Hint: You can pass props to <em>App</em> from the root render function.</strong></li><li>Sync Vuex state from the server to the client. It might involve some global variables!</li></ul><hr /><h2 id="reference">Reference</h2>
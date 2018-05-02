<a href="http://gaearon.github.io/react-hot-loader/getstarted/">http://gaearon.github.io/react-hot-loader/getstarted/</a><div id="articleHeader"><h1>Getting Started</h1></div>
  <p>React Hot Loader is a plugin that allows React components to be live reloaded without the loss of state. It works with Webpack and other bundlers that support both Hot Module Replacement (HMR) and Babel plugins.</p>

<p>If you just want a quick start with a fresh, barebones boilerplate, where everything works out of the box (using Webpack), check out <code>react-hot-boilerplate</code>, the official boilerplate:</p>

<p><a href="https://github.com/gaearon/react-hot-boilerplate" target="_blank">https://github.com/gaearon/react-hot-boilerplate</a></p>

<p>or the new, minimal one:</p>

<p><a href="https://github.com/wkwiatek/react-hot-loader-minimal-boilerplate" target="_blank">https://github.com/wkwiatek/react-hot-loader-minimal-boilerplate</a></p>

<h2 id="integrating-into-your-app">Integrating into your app</h2>

<p>What follows is a 3-step guide for integrating React Hot Loader into your current project.</p>

<h3 id="step-1-of-3-enabling-hot-module-replacement-hmr">Step 1 (of 3): Enabling Hot Module Replacement (HMR)</h3>

<p>HMR allows us to replace modules in-place without restarting the server. Here’s how you can enable it for different bundlers:</p>

<h4 id="webpack">Webpack</h4>

<p><strong>Option 1: Webpack Dev Server CLI (client-side rendering only)</strong></p>

<p>The easiest and fastest option to use React Hot Loader with Webpack is to use <code>webpack-dev-server</code> with <code>--hot</code> CLI option.</p>

<div><div><pre><code>  "scripts": {
    "start": "webpack-dev-server --hot"
  },
</code></pre></div>

<p>That’s it! You can go to the <a href="#step-2-of-3-using-hmr-to-replace-the-root-component" target="_blank">Step 2</a>.</p>

<p><strong>Option 2: Webpack Dev Server with custom server (client-side rendering only)</strong></p>

<p>If you’re only rendering on the client side but you have to use some custom node server, this is still an easy option.  You can simply copy <a href="https://github.com/gaearon/react-hot-boilerplate/blob/master/server.js" target="_blank"><code>server.js</code></a> from the official boilerplate into your project. The important part of the configuration is that when you create a <code>new WebpackDevServer</code>, you need to specify <code>hot: true</code> as an option.</p>

<p>Here is <code>server.js</code> from the official boilerplate:</p>

<div><div><pre><code>var webpack = require('webpack');
var WebpackDevServer = require('webpack-dev-server');
var config = require('./webpack.config');

new WebpackDevServer(webpack(config), {
  publicPath: config.output.publicPath,
  hot: true,
  historyApiFallback: true
}).listen(3000, 'localhost', function (err, result) {
  if (err) {
    return console.log(err);
  }

  console.log('Listening at http://localhost:3000/');
});
</code></pre></div>

<p>To launch it via <code>npm start</code>, add the following script to your <a href="https://github.com/gaearon/react-hot-boilerplate/blob/master/package.json" target="_blank"><code>package.json</code></a>:</p>

<div><div><pre><code>  "scripts": {
    "start": "node server.js"
  },
</code></pre></div>

<p>In your <a href="https://github.com/gaearon/react-hot-boilerplate/blob/master/webpack.config.js" target="_blank"><code>webpack.config.js</code></a>, you’ll need to add the dev server and hot reload server to the <code>entry</code> section. Put them in the <code>entry</code> array, before your appʼs entry point:</p>

<div><div><pre><code>  entry: [
    'webpack-dev-server/client?http://0.0.0.0:3000', // WebpackDevServer host and port
    'webpack/hot/only-dev-server', // "only" prevents reload on syntax errors
    './scripts/index' // Your appʼs entry point
  ]
</code></pre></div>

<p>Finally, the Hot Replacement plugin from Webpack has to be included in the <code>plugins</code> section of the config. Add <code>var webpack = require('webpack')</code> at the top of your Webpack config, then add <code>new webpack.HotModuleReplacementPlugin()</code> to the <code>plugins</code> section:</p>

<div><div><pre><code>  plugins: [
    new webpack.HotModuleReplacementPlugin()
  ]
</code></pre></div>

<blockquote>
  <p>Note: If you are using the Webpack Dev Server command line interface instead of its Node API, <em>do not</em> add this plugin to your config if you use the <code>--hot</code> flag. It is mutually exclusive from the <code>--hot</code> option.</p>
</blockquote>

<p>Check out the boilerplate’s <a href="https://github.com/gaearon/react-hot-boilerplate/blob/master/webpack.config.js" target="_blank"><code>webpack.config.js</code></a> to see it all together.</p>

<p><strong>Option 3: Express with webpack-dev-middleware (client & server)</strong></p>

<p>If you are using server-side rendering, the WebpackDevServer above is not enough. Instead, we have to use an Express server with the <code>webpack-dev-middleware</code>.  This is a bit more work, but also gives us more control. We need to add this middleware and it’s entry point.</p>

<p>XXX TODO</p>

<h4 id="meteor">Meteor</h4>

<ul>
  <li>
    <p>If you’re using <a href="https://atmospherejs.com/webpack/webpack" target="_blank">webpack:webpack</a>, you can follow the Webpack instructions, or ask for help in <a href="https://forums.meteor.com/t/use-webpack-with-meteor-simply-by-adding-packages-meteor-webpack-1-0-is-out/18819" target="_blank">this</a> forum post.</p>
  </li>
  <li>
    <p>Otherwise, for HMR in “native” Meteor, type: <code>meteor remove ecmascript && meteor add gadicc:ecmascript-hot</code> or see the <a href="https://github.com/gadicc/meteor-hmr#readme" target="_blank">README</a> for more details.  There are also some Meteor-specific RHLv3 install instructions <a href="https://github.com/gadicc/meteor-hmr/blob/master/docs/React_Hotloading.md" target="_blank">here</a>.</p>
  </li>
</ul>

<h3 id="step-2-of-3-using-hmr-to-replace-the-root-component">Step 2 (of 3): Using HMR to replace the root component</h3>

<p>To update components when changes occur, you need to add some code to your main client entry point file.</p>

<p>If your entry point looks like this, where <code>&lt;RootContainer&gt;</code> is your app’s top-level component:</p>

<div><div><pre><code>import React from 'react';
import { render } from 'react-dom';
import RootContainer from './containers/rootContainer.js';

render(&lt;RootContainer /&gt;, document.getElementById('react-root'));
</code></pre></div>
<p>Add the following code to accept changes to your RootContainer, <em>or any of its descendants</em>:</p>

<div><div><pre><code> if (module.hot) {
   module.hot.accept('./containers/rootContainer.js', () =&gt; {
     const NextRootContainer = require('./containers/rootContainer.js').default;
     render(&lt;NextRootContainer /&gt;, document.getElementById('react-root'));
   })
 }
</code></pre></div>

<blockquote>
  <p><em>How it works:</em> When the HMR runtime receives an updated module, it first checks to see if the module knows how to update itself. It then goes up the import/require chain, looking for a parent module that can accept the update.  The added code allows our root component to accept an update from any child component.</p>
</blockquote>

<p>Note that, with no further steps, this is enough to hot reload changes to React components, but their internal component state will not be preserved, since a new copy of the component is mounted, and its state is re-initialized.  State that is kept externally in a state store, such as Redux, will obviously not be lost.</p>

<h4 id="step-3-of-3-adding-react-hot-loader-to-preserve-component-state">Step 3 (of 3): Adding React Hot Loader to preserve component state</h4>

<p>To preserve <em>internal component state</em>, you now need to add <code>react-hot-loader</code> to your project.</p>

<ol>
  <li>
    <p>Install the package:</p>

    <div><div><pre><code>$ npm install --save-dev react-hot-loader@next
</code></pre></div>    
  </li>
  <li>
    <p>Add the package to your config:</p>

    <p>a.  If you use Babel, modify your <code>.babelrc</code> to ensure it includes at least:</p>

    <div><div><pre><code>  {
    "plugins": [ "react-hot-loader/babel" ]
  }
</code></pre></div>    
    <p>b. Alternatively, in Webpack, add <code>react-hot-loader/webpack</code> to the <code>loaders</code> section of your <code>webpack.config.js</code>:</p>

    <div><div><pre><code>    module: {
        loaders: [{
            test: /\.js$/,
            loaders: ['react-hot-loader/webpack', 'babel'],
            include: path.join(__dirname, 'src')
        }]
    }
</code></pre></div>    

    <blockquote>
      <p>Note: <code>react-hot-loader/webpack</code> only works on <em>exported</em> components,
whereas <code>react-hot-loader/babel</code> picks up all <em>top-level variables</em> in
your files. As a workaround, with Webpack, you can export all the
components whose state you want to maintain, even if they’re not
imported anywhere else.</p>
    </blockquote>
  </li>
  <li>
    <p>Update your main client entry point:</p>

    <p>a.  Add following line to the top of your main client entry point:</p>

    <div><div><pre><code>import 'react-hot-loader/patch';
</code></pre></div>    

    <blockquote>
      <p>Alternatively, in Webpack, add <code>react-hot-loader/patch</code> to the <code>entry</code> section of your <code>webpack.config.js</code>:</p>
    </blockquote>

    <div><div><pre><code>  entry: [
    'react-hot-loader/patch', // RHL patch
    './scripts/index' // Your appʼs entry point
  ]
</code></pre></div>    

    <p>b.  Wrap your app’s top-level component inside of an <strong><code>&lt;AppContainer&gt;</code>.</strong></p>

    <blockquote>
      <p><code>AppContainer</code> is a component, provided by <code>react-hot-loader</code>, that handles hot reloading, as well as error handling.  It also <a href="https://github.com/gaearon/react-hot-loader/blob/next/src/AppContainer.js#L5-L9" target="_blank">internally</a> handles disabling hot reloading/error handling when running in a production environment, so you no longer have to.</p>
    </blockquote>

    <p>You need to wrap both instances, e.g. your original mount, and your mount code inside of the <code>module.hot.accept()</code> function.  Note that <code>&lt;AppContainer&gt;</code> must only wrap a single React component.</p>

    <p>Your main entry point should now look something like this:</p>

    <div><div><pre><code>import 'react-hot-loader/patch';
import React from 'react';
import ReactDOM from 'react-dom';

import { AppContainer } from 'react-hot-loader';
import RootContainer from './containers/rootContainer';

const render = Component =&gt; {
  ReactDOM.render(
    &lt;AppContainer&gt;
      &lt;Component /&gt;
    &lt;/AppContainer&gt;,
    document.getElementById('root')
  );
}

render(RootContainer);

if (module.hot) {
  module.hot.accept('./containers/rootContainer.js', () =&gt; {
    const NextRootContainer = require('./containers/rootContainer').default;
    render(NextRootContainer);
  });
}
</code></pre></div>    

    <p>c. Webpack 2 has built-in support for ES2015 modules, and you won’t need to re-require your app root in module.hot.accept. The example above becomes:</p>

    <blockquote>
      <p>Note: To make this work, you’ll need to opt out of Babel transpiling ES2015 modules by changing the Babel ES2015 preset to be</p>
      <div><div><pre><code>{
  "presets": [["es2015", { "modules": false }]]
}
</code></pre></div>      
      <p>or when using <code>latest</code> preset then:</p>
      <div><div><pre><code>{
  "presets": [
    ["latest", {
      "es2015": {
        "modules": false
      }
    }]
  ]
}
</code></pre></div>      
    </blockquote>

    <div><div><pre><code>import 'react-hot-loader/patch';
import React from 'react';
import ReactDom from 'react-dom';
import { AppContainer } from 'react-hot-loader';

import RootContainer from './containers/rootContainer';

const render = Component =&gt; {
  ReactDOM.render(
    &lt;AppContainer&gt;
      &lt;Component /&gt;
    &lt;/AppContainer&gt;,
    document.getElementById('root')
  );
}

render(RootContainer);

if (module.hot) {
  module.hot.accept('./containers/rootContainer', () =&gt; { render(RootContainer) });
}
</code></pre></div>    
  </li>
</ol>

<p>That’s it! Happy hot reloading!</p>

<h3 id="troubleshooting">Troubleshooting</h3>

<p>If hot reloading doesnʼt work, itʼs usually due to a deviation from the configuration described above. Make sure to compare your setup to <a href="https://github.com/gaearon/react-hot-boilerplate" target="_blank"><code>react-hot-boilerplate</code></a> or <a href="https://github.com/wkwiatek/react-hot-loader-minimal-boilerplate" target="_blank"><code>react-hot-loader-minimal-boilerplate</code></a> and verify that the boilerplate works for you. Look very closely for small typos.</p>

<p>If youʼre stuck, <a href="https://github.com/gaearon/react-hot-loader/issues/new" target="_blank">file an issue</a> or ask for help in <a href="https://gitter.im/gaearon/react-hot-loader" target="_blank">the Gitter room</a>, and weʼll try to figure it out.</p>

<p>In order to improve our documentation, we need your feedback! Feel free to <a href="https://github.com/gaearon/react-hot-loader/issues/new" target="_blank">open an issue</a> for that too!</p>


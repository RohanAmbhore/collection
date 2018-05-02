<a href="https://javascriptplayground.com/css-modules-webpack-react/">https://javascriptplayground.com/css-modules-webpack-react/</a><div id="articleHeader"><h1>Setting up CSS Modules with React and Webpack</h1></div>
    
    <p>
      Published on <time>Jul 18, 2016</time>
      
      
    </p>
    
    
  </header>
  
    
    <p>One of the biggest problems that developers face with CSS is that CSS is global. Each CSS class gets exposed globally and it’s very easy to inadvertently break a piece of your site when editing or adding CSS for a new feature. In an era where many developers are building websites as components with a framework such as React, CSS is an even bigger problem.</p>

<p>CSS Modules allow us to write <em>scoped</em> CSS, just like a variable in JavaScript or any other programming language. We can write CSS for a component and be certain that it won’t leak into other components. You can also have confidence that adding a new component to your application won’t interfere with any other components on the system.</p>

<p>CSS Modules are a fantastic idea and play particularly nicely with React, but at the time of writing there isn’t a good resource for getting started and setting up React, CSS Modules and Webpack to build everything correctly. In this article I’ll show you how I took a React application and added CSS modules, which Webpack plugins I used for this, and an example of CSS modules in action. If you’d like to get this running yourself you’ll find all the <a href="https://github.com/jackfranklin/react-css-modules-webpack" target="_blank">code available on GitHub</a>. We’ll also look at how we can generate a production <code>bundle.css</code> file which has all our CSS together and fully minified.</p>

<h2 id="the-goal">The goal</h2>

<p>What we’re aiming for is to be able to write CSS on a per component basis. That is, for each component we have a corresponding <code>component.css</code> file that will define the CSS for that component.</p>

<p>For a component <code>App.js</code>, we also have <code>app.css</code>:</p>

<div><div><pre><code>.app p {
  color: blue;
}
</code></pre></div></div>

<p>And then in the component we can import this CSS file, as if it was a JavaScript module:</p>

<div><div><pre><code>import styles from './app.css';
</code></pre></div></div>

<p>Finally, we can reference the class name in our CSS file:</p>

<div><div><pre><code>&lt;div className={styles.app}&gt;
  &lt;p&gt;This text will be blue&lt;/p&gt;
&lt;/div&gt;
</code></pre></div></div>

<p>None of this works out of the box, but we’ll use Webpack with a couple of additional loaders to get this working. The beauty is that the actual class name in the generated CSS file won’t be <code>.app</code> as above, but <code>.app-[some-hash]</code>. By adding a hash to each class name it’s guaranteed that each CSS class declaration is unique (the hash is based on the contents - so if two classes clash it’s because they have the same styles).</p>

<h2 id="webpack-loaders">Webpack Loaders</h2>

<p>To set this up we’re going to dive into the wonderful world of Webpack loaders. These can be confusing at first, but in essence a Webpack loader is a plugin for Webpack that can apply extra transformations or manipulate files before they are bundled.</p>

<p>There’s two we need to use:</p>

<ul>
  <li><a href="https://github.com/webpack/style-loader" target="_blank"><code>style-loader</code></a> is a Webpack loader that can load some CSS and inject it into the document via a <code>&lt;link&gt;</code> tag.</li>
  <li><a href="https://github.com/webpack/css-loader" target="_blank"><code>css-loader</code></a> is the loader that can parse a CSS file and apply various transforms to it. Crucially it has a CSS Modules mode that can take our CSS and hash the classes as mentioned above.</li>
</ul>

<p>In the project that I’m adding CSS Modules to we already have one loader defined for our JavaScript:</p>

<div><div><pre><code>module: {
  loaders: [{
    test: /\.js$/,
    loaders: ['react-hot', 'babel'],
    include: path.join(__dirname, 'src')
  }
}
</code></pre></div></div>

<p>This configures every JavaScript file to be run through the <code>react-hot</code> loader, which configures hot module loading, and <code>babel</code>, which will transpire ES2015 features and the JSX syntax.</p>

<p>What we need to do is add another configuration for <code>.css</code> files where we first configure <code>style-loader</code>, and then <code>css-loader</code>:</p>

<div><div><pre><code>{
  test: /\.css$/,
  loader: 'style-loader'
}, {
  test: /\.css$/,
  loader: 'css-loader',
  query: {
    modules: true,
    localIdentName: '[name]__[local]___[hash:base64:5]'
  }
}
</code></pre></div></div>

<p>First we configure the <code>style-loader</code>, which needs no extra configuration, so we’re set. Then we have to configure <code>css-loader</code>. The important bit to this is the <code>query</code> object, which defines two properties:</p>

<ul>
  <li><code>modules: true</code> turns on the CSS modules mode</li>
  <li><code>localIdentName: '[name]__[local]___[hash:base64:5]'</code> defines the structure of the generated CSS class should be. You don’t need to worry too much about this, other than knowing that this maps to the generated output. For example, our CSS from above with the class of <code>app</code> will end up as <code>app__app___2x3cr</code> in the browser.</li>
</ul>

<h2 id="running-webpack">Running Webpack</h2>

<p>With the above changes to our Webpack configuration we’re done! You can now run Webpack (if you’re running the <a href="https://github.com/jackfranklin/react-css-modules-webpack" target="_blank">example repository</a>, run <code>npm start</code> to fire up the Webpack dev server) and have your CSS modules converted and working for you in the browser.</p>

<p>If you’re using the dev server you’ll also note that the CSS is automatically updated when you change without a hard refresh in the browser which is useful during development.</p>

<h2 id="tidying-up-the-webpack-configuration">Tidying up the Webpack configuration</h2>

<p>One thing that irks me about the Webpack configuration in its current state is the fact that we have to configure loaders for <code>.css</code> twice - once for the style loader, and once for the css loader. I’d much rather group these both up into one. However, once you configure multiple loaders you can’t pass in the <code>query</code> object as we did above, and must use Webpack’s string configuration. In our case if we did that, our configuration would look like so:</p>

<div><div><pre><code>{
    test: /\.css$/,
    loader: 'style-loader!css-loader?modules=true&localIdentName=[name]__[local]___[hash:base64:5]'
}
</code></pre></div></div>

<p>I think this is pretty messy and much harder to follow.</p>

<p>Thankfully I found <a href="https://github.com/jsdf/webpack-combine-loaders" target="_blank">webpack-combine-loaders</a> which enables us to use the <code>query</code> object syntax to configure a loader, but without having to repeat the <code>test: /\.css$/</code> line. Using this module our configuration becomes:</p>

<div><div><pre><code>{
  test: /\.css$/,
  loader: combineLoaders([
    {
      loader: 'style-loader'
    }, {
      loader: 'css-loader',
      query: {
        modules: true,
        localIdentName: '[name]__[local]___[hash:base64:5]'
      }
    }
  ])
}]
</code></pre></div></div>

<p>I think this is cleaner because it’s clearer that we’re using both <code>style-loader</code> and <code>css-loader</code> on the same file type.</p>

<h2 id="deploying-to-production">Deploying to Production</h2>

<p>The final step is to update the production Webpack build to parse all our CSS and generate an outputted CSS file that contains all our CSS. We don’t want to have our CSS injected through Webpack in production, and we don’t want the CSS module transformations to run in the browser; instead we want to simply deploy a generated stylesheet that contains all our styles.</p>

<p>To do this we can use the <a href="https://github.com/webpack/extract-text-webpack-plugin" target="_blank"><code>extract-text-plugin</code></a> for Webpack that will take all files that match a regular expression (in our case we’ll look for CSS files as we did previously) and bundle them all into one file. We can also run them through the CSS Modules transform just like we did in our development config.</p>

<p>To get started we first need to install the plugin:</p>

<div><div><pre><code>npm install extract-text-webpack-plugin —save-dev
</code></pre></div></div>

<p>Then we need to configure the plugin. First we’ll add an entry to the <code>plugins</code> key in the Webpack configuration:</p>

<div><div><pre><code>// at top of file
var ExtractTextPlugin = require('extract-text-webpack-plugin');

// in the webpack config
plugins: [
  new ExtractTextPlugin('styles.css'),
  ...
]
</code></pre></div></div>

<p>This configures the plugin to output to <code>styles.css</code>.</p>

<p>Then we will configure the module loader again to find all our CSS files and bundle them together. The configuration here looks similar, we call <code>ExtractTextPlugin.extract</code>. This takes multiple arguments, where each argument is an individual loader to pass. We first pass <code>style-loader</code>, and then use <code>combineLoaders</code> again to generate a string version of the configuration for <code>css-loader</code>:</p>

<div><div><pre><code>module: {
  ...,
  loaders: [{
    // JS loader config
  }, {
    test: /\.css$/,
    loader: ExtractTextPlugin.extract(
      'style-loader',
      combineLoaders([{
        loader: 'css-loader',
        query: {
          modules: true,
          localIdentName: '[name]__[local]___[hash:base64:5]'
        }
      }])
    )
  }],
  ...
}
</code></pre></div></div>

<p>Now when we run Webpack with this configuration we’ll have a JavaScript and a CSS file that we can use in production with CSS Modules fully transformed.</p>

<h2 id="conclusion">Conclusion</h2>

<p>There’s a few final pieces we could do to tidy up, but I’m going to leave those as exercises for the reader. The main issue now is that we’re duplicating configuration for the CSS Loader across our development Webpack setup and our production Webpack setup. You might consider extracting a file that contains that configuration, rather than duplicating it.</p>

<p>CSS Modules are a great way to organise your CSS in a component based system. Here I’ve used them with React but you’ll notice that none of the code in this tutorial is React specific - this approach can be used with other frameworks with no extra effort.</p>

<p>If you’d like to use this tutorial as a starting point, don’t forget that you can <a href="https://github.com/jackfranklin/react-css-modules-webpack" target="_blank">find the repository on GitHub</a>, and please get in touch if you have any questions. You can find more information on the <a href="https://github.com/css-modules/css-modules" target="_blank">CSS Modules repository</a> and Glenn Maddern’s <a href="http://glenmaddern.com/articles/css-modules" target="_blank">“CSS Modules: Welcome to the Future”</a> blog post.</p>

    
    <hr />

    <div>
      <p>
        If you enjoyed this article please feel free to <a href="https://twitter.com/intent/tweet?text=Setting up CSS Modules with React and Webpack&url=https://www.javascriptplayground.com/css-modules-webpack-react/&via=Jack_Franklin&related=Jack_Franklin" title="Share on Twitter" target="_blank">share it on Twitter</a>.
      </p>

    </div>

    <hr />

    <div>
      <p>
        Don't miss my latest course on <a href="/testing-react-enzyme-jest" target="_blank">Testing React with Enyzme and Jest</a>! The first five videos are free and available to watch now. You'll learn how to write testable React code, test complex components and use Jest and Enzyme effectively to write clean, thorough tests. <a href="/testing-react-enzyme-jest" target="_blank">Get started now</a>.
      </p>
    </div>

      <hr />

      
      <div id="mc_embed_signup">
        <h4>Subscribe to keep up to date with the latest content.</h4>
        <p>Join the JS Playground mailing list to be kept up to date with the latest tutorials, screencasts and more. You won't be spammed and you can unsubscribe at any time.</p>
        
          
        
      </div>

      

      <hr />

      <div>
        <img src="/img/head.png" alt="Headshot of Jack Franklin" />
        <div>
          <p>Jack is JavaScript and React developer in London. He's also a keen <a href="http://elmplayground.com" target="_blank">Elm enthusiast</a>, <a href="https://speakerdeck.com/jackfranklin" target="_blank">conference speaker</a> and <a href="http://twitter.com/jack_franklin" target="_blank">tweets far too often</a>.</p>

          
        </div>
      </div>
    
<a href="https://blog.pusher.com/css-modules-react/">https://blog.pusher.com/css-modules-react/</a><div id="articleHeader"><h1>Getting started with CSS modules in React</h1></div>
					<p>When building React applications (or any application actually), we need it to look great. For web applications, the standard beautification language is called CSS. Since the age of the dinosaurs, properly structuring CSS styles and arranging them has always been a problem.</p>
<p>In small apps this is not really a problem, but with applications of larger structure things are bound to get real hazy. With CSS Modules we can modularize things in React and add some structure to the flow.</p>
<p>In this article we will explore how we can use CSS Modules in React to make maintaining our CSS files way easier and more modular.</p>
<p>Let’s have a real look at the problems we are trying to solve.</p>
<h2>CSS at scale</h2>
<p>CSS has always been easy and flexible, but then this really cool technology doesn’t really lend itself to scalability. With large projects that have extended sections and features, it becomes a real menace to deal with.</p>
<p>At scale these problems become real (scale here referring to a codebase with many developers working on it), but then there are a couple of problems that we have to take into account and make sure we understand before we attempt to solve them.</p>
<p>Some of the problems are:<br />
1. Global ~~warming~~ namespaces.<br />
2. Dead code elimination.<br />
3. Dependencies.<br />
4. Conditionals.</p>
<h3>Global namespaces</h3>
<p>CSS is a language of globals. In most languages, global variables are considered bad and taking into account we have CSS styles mostly specific to our components, it’s obvious that globals are bad (there are cases when using global CSS is okay though).</p>
<p>Global CSS can easily rewrite styling in other classes. A change in the style in one class can ultimately and silently change the UI on multiple components. Generally, no one wants that to happen when they develop apps.</p>
<h3>Dead code elimination</h3>
<p>Most times while building apps, we have styling that is redundant or no longer in use. Although they can be small at first, overtime it builds up and we have rogue and unused CSS everywhere and it can cause unnecessarily large file sizes.</p>
<p>With CSS modules, we get to only import styles we use. therefore reducing redundancy and the increase our ability to spot CSS that is not being used.</p>
<h3>Dependencies</h3>
<p>Working with dependencies in CSS is hazy. Most of the time we are used to just including the entire script directly into the page whether they are being used or not.</p>
<h3>Conditionals</h3>
<p>Sometimes you need your CSS class to style in a certain way in one section and in a different way in another section. In this case, it is usually better to have the CSS class variable modifiable in the component.</p>
<p>Modular CSS solves each of these problems in a clean structured manner by having our components import only the classes they actually use therefore getting rid of redundancy. This in itself also solves the problems of global namespaces.</p>
<h2>Working with CSS modules</h2>
<p>When working with modular CSS in React, we can work in a few ways:<br />
– Using CSS as JavaScript Objects.<br />
– Using CSS Modules.</p>
<p>We will focus on CSS modules but shine a little light on the former.</p>
<h3>CSS as JavaScript objects</h3>
<p>Writing CSS as JavaScript objects is easier in the context of React as it ensures you do not have to stray from JavaScript to write CSS. In JavaScript, CSS classes look similar and CSS classes are named in <a href="https://en.wikipedia.org/wiki/Camel_case" target="_blank">camel cased</a> versions of the property name.</p>
<p>CSS written as JavaScript objects can be leveraged directly in React components by using the  <code>style</code> attribute on components.</p>
<p>Here is an example:</p>
<pre><code>    // lets have some CSS in js: style.css.js
    const button = {
        backgroundColor: '#202020',
        padding: '12px',
        borderRadius: '2px',
        width: '100%'
    }
    export default { button }

    //importing and using in a JSX
    import styles from './style.css.js'

    const button = () =&gt; {
        return &lt;button style={styles.button}&gt;Vanity Button&lt;/button&gt;
    }
</code></pre>
<p>The code above is a clear example of using CSS as a JavaScript object and it allows us to have styling that is unique to that element.</p>
<p>Another thing you can do when defining the CSS as a JavaScript object is use variables as the values for the style property. In this way it can change depending on some conditions:</p>
<pre><code>    // lets have some CSS in JS: style.css.js
    var variables = {
        backgroundColor: '#202020'
    }
    var button = {
        backgroundColor: variables.backgroundColor,
        padding: '12px',
        borderRadius: '2px',
        width: '100%'
    }
    export default { button };

    // importing and using in a JSX
    import styles from './style.css.js'

    const button = () =&gt; {
        return &lt;button style={styles.button}&gt;Vanity Button&lt;/div&gt;
    }
</code></pre>
<p>One of the major wins with CSS as JavaScript objects is it requires no setup to get it working. Since it’s plain JavaScript you are good to go. Although CSS in JavaScript is extensible it does have it’s limitations in various areas.</p>
<h3>CSS modules</h3>
<p>CSS modules are not very different from the method above. However, with CSS modules, we can write our usual CSS code and import that into our component.</p>
<p>Here is an example:</p>
<pre><code>    // lets have some CSS in JS: style.css
    .button {
      background-color: #202020;
      padding: 12px;
      border-radius: 2px;
      width: 100px;
    }


    // Importing and using in a jsx
    import styles from './style.css'
    import React from 'react';

    export default class Button extends React.Component {
        render(){
            return (
                &lt;button className={styles.button}&gt;Vanity Button&lt;/button&gt;
            )
        }
    }
</code></pre>
<p>In the code above, you can see that the CSS is actual CSS and not a JavaScript object. However, this in itself will not work and we will need to configure our loader to make it work.</p>
<h3>Setting up for CSS modules</h3>
<p>Most of the configuration for our application to work with CSS modules will be done in the webpack configuration file. So assuming you have set up a React application using <code>create-react-app</code>, you will need to take control of your apps configuration using the <code>eject</code>  command:</p>
<pre><code>    $ yarn eject
</code></pre>
<blockquote><p>
  <img src="https://s.w.org/images/core/emoji/2.4/svg/1f4a1.svg" alt="💡" />  With normal apps not created using <code>create-react-app</code> you can configure Webpack in a similar way as shown in this article.
</p></blockquote>
<p>After ejecting, we can update our <code>webpack.config.dev.js</code> file to reflect our setup for CSS modules. In the webpack configuration file, replace the content below:</p>
<pre><code>    {
        loader: require.resolve('css-loader'),
        options: {
            importLoaders: 1,
        },
    },
</code></pre>
<p>with the following configuration:</p>
<pre><code>    {
      loader: require.resolve('css-loader'),
      options: {
        importLoaders: 1,
        modules: true,
        localIdentName: "[name]__[local]___[hash:base64:5]"  
      },
    }
</code></pre>
<p>With the change we can now use CSS modules in our project. We have also set up hashing to properly generate names for the classes being used in the modules.</p>
<blockquote><p>
  <img src="https://s.w.org/images/core/emoji/2.4/svg/1f4a1.svg" alt="💡" />  You can use a shorthand to specify the same loader like so: <code>loader: 'css?modules&importLoaders=1&localIdentName=[path]___[name]__[local]___[hash:base64:5]``'</code>
</p></blockquote>
<p>If you are not using <code>create-react-app</code>, adding the required options and setting up the <code>extractTextPlugin</code> will be the way to set up CSS Modules:</p>
<pre><code>    import ExtractTextPlugin from 'extract-text-webpack-plugin'

    module.exports = {
    ....
      plugins: [
        ....
        new ExtractTextPlugin('style.css')
      ]
    }
</code></pre>
<p>Now we can reconfigure our loader to find our CSS files and bundle them together:</p>
<pre><code>    loader: ExtractTextPlugin.extract(
        'style-loader',
        combineLoaders([
          {
            loader: 'css-loader',
            query: {
              modules: true,
              localIdentName: '[name]__[local]___[hash:base64:5]'
            }
          }
        ])
    )
</code></pre>
<h2>Taking things a step further</h2>
<p>Let’s take things a step further using the <code>react-css-module</code>. You can install this via the npm registry:</p>
<pre><code>    $ yarn add react-css-modules
</code></pre>
<p>With <code>react-css-modules</code> we can have our code like this now:</p>
<pre><code>    // lets have some CSS: style.css
    .button{
      background-color: #202020;
      padding: 12px;
      border-radius: 2px;
      width: 100px;
    }

    //importing and using in a jsx
    import styles from './style.css'
    import React from 'react';
    import CssModules from 'react-css-modules';

    class Button extends React.Component{

      render(){
        return (
          &lt;button styleName='button'&gt;Vanity Button&lt;/button&gt;
        );
      }
    }
    export default CssModules(Button, styles);
</code></pre>
<blockquote><p>
  <img src="https://s.w.org/images/core/emoji/2.4/svg/1f4a1.svg" alt="💡" />  Using the <code>react-css-modules</code>, we don’t have to specify the style as an object, but rather we can specify it as a class name and have the style object added to the entire component using the <code>CssModule</code> function.
</p></blockquote>
<h3>Explaining an example usage of CSS modules</h3>
<p>To demonstrate how CSS Modules can be used we will be creating a To-do application (yes I know, again). The demo implements CSS Modules, with every component implementing its own style. You can <a href="https://github.com/neoighodaro/react-todo-sample" target="_blank">download the demo</a> on GitHub.</p>
<p>In the <code>config/webpack.config.dev,js</code> file and the <code>config/webpack.config.prod.js</code> file, we update the CSS loaders configurations to use the CSS modules:</p>
<pre><code>    use: [
      ...
      {
        loader: require.resolve('css-loader'),
        options: {
          importLoaders: 1,
          modules: true,
          localIdentName: "[name]__[local]___[hash:base64:5]"  
        },
      }
      ...
    ],
</code></pre>
<p>Next, we installed the <code>react-css-modules</code> package by running the command below in our terminal:</p>
<pre><code>    $ npm install react-css-modules
</code></pre>
<p>Now we can create a CSS file called <code>todoItem.css</code> and paste in the following:</p>
<pre><code>    .TodoItem{
      width: 100%;
      min-height: 30px;
      padding:12px;
      border-bottom: 1px solid #ededed;
    }

    .removeOp{
      content: "/f00d";
      color: red
    }
</code></pre>
<p>And then paste this in our JavaScript file:</p>
<pre><code>    import React from 'react'
    import propTypes from 'prop-types'
    import CssModules from 'react-css-modules'
    import s from './todoitem.css'

    class TodoItem extends React.Component{ 
        render(){
            return (
                &lt;div styleName="TodoItem"&gt;
                    {this.props.title}
                    &lt;span styleName="removeOp" onClick={()=&gt;this.props.remove(this.props.id)}&gt;click to remove&lt;/span&gt;
                &lt;/div&gt; 
            )   
        }
    }

    TodoItem.propTypes = {
       title: propTypes.string.isRequired,
       id: propTypes.number.isRequired,
       remove: propTypes.func.isRquired
    }
    export default CssModules(TodoItem, s)
</code></pre>
<p>Above you see we can easily use the <code>CssModules</code> package in exporting our components while hooking them to the style implementation. We can use the <code>styleName</code> property to specify the specific styles we want in the stylesheet.</p>
<h2>Conclusion</h2>
<p>We have considered how you can use <code>CssModules</code> to change the way you work with styles in your React application. You can combine this method with a CSS preprocessor like Sass or Less.</p>
<p>We also learned about the methods of including CSS into our React components. While both methods share certain advantages, the implementation differs: one is actual CSS living in CSS files wired with JS modules using imports and hashed class names at build time, the other is actual JS from the start and is composed and attached to elements in the form of inline styles at execution time.</p>
<p>If you have any questions and feedback, please leave them as a comment below.</p>
									
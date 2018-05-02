<a href="https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-a-css-preprocessor-sass-less-etc">https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-a-css-preprocessor-sass-less-etc</a><div id="articleHeader"><h1>create-react-app/README.md at master · facebook/create-react-app</h1></div><p>This project was bootstrapped with <a href="https://github.com/facebookincubator/create-react-app" target="_blank">Create React App</a>.</p>
<p>Below you will find some information on how to perform common tasks.<br />
You can find the most recent version of this guide <a href="https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md" target="_blank">here</a>.</p>
<h2>Table of Contents</h2>

<h2>Updating to New Releases</h2>
<p>Create React App is divided into two packages:</p>
<ul>
<li><code>create-react-app</code> is a global command-line utility that you use to create new projects.</li>
<li><code>react-scripts</code> is a development dependency in the generated projects (including this one).</li>
</ul>
<p>You almost never need to update <code>create-react-app</code> itself: it delegates all the setup to <code>react-scripts</code>.</p>
<p>When you run <code>create-react-app</code>, it always creates the project with the latest version of <code>react-scripts</code> so you’ll get all the new features and improvements in newly created apps automatically.</p>
<p>To update an existing project to a new version of <code>react-scripts</code>, <a href="https://github.com/facebookincubator/create-react-app/blob/master/CHANGELOG.md" target="_blank">open the changelog</a>, find the version you’re currently on (check <code>package.json</code> in this folder if you’re not sure), and apply the migration instructions for the newer versions.</p>
<p>In most cases bumping the <code>react-scripts</code> version in <code>package.json</code> and running <code>npm install</code> in this folder should be enough, but it’s good to consult the <a href="https://github.com/facebookincubator/create-react-app/blob/master/CHANGELOG.md" target="_blank">changelog</a> for potential breaking changes.</p>
<p>We commit to keeping the breaking changes minimal so you can upgrade <code>react-scripts</code> painlessly.</p>
<h2>Sending Feedback</h2>
<p>We are always open to <a href="https://github.com/facebookincubator/create-react-app/issues" target="_blank">your feedback</a>.</p>
<h2>Folder Structure</h2>
<p>After creation, your project should look like this:</p>
<pre><code>my-app/
  README.md
  node_modules/
  package.json
  public/
    index.html
    favicon.ico
  src/
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
</code></pre>
<p>For the project to build, <strong>these files must exist with exact filenames</strong>:</p>
<ul>
<li><code>public/index.html</code> is the page template;</li>
<li><code>src/index.js</code> is the JavaScript entry point.</li>
</ul>
<p>You can delete or rename the other files.</p>
<p>You may create subdirectories inside <code>src</code>. For faster rebuilds, only files inside <code>src</code> are processed by Webpack.<br />
You need to <strong>put any JS and CSS files inside <code>src</code></strong>, otherwise Webpack won’t see them.</p>
<p>Only files inside <code>public</code> can be used from <code>public/index.html</code>.<br />
Read instructions below for using assets from JavaScript and HTML.</p>
<p>You can, however, create more top-level directories.<br />
They will not be included in the production build so you can use them for things like documentation.</p>
<h2>Available Scripts</h2>
<p>In the project directory, you can run:</p>
<h3><code>npm start</code></h3>
<p>Runs the app in the development mode.<br />
Open <a href="http://localhost:3000" target="_blank">http://localhost:3000</a> to view it in the browser.</p>
<p>The page will reload if you make edits.<br />
You will also see any lint errors in the console.</p>
<h3><code>npm test</code></h3>
<p>Launches the test runner in the interactive watch mode.<br />
See the section about <a href="#running-tests" target="_blank">running tests</a> for more information.</p>
<h3><code>npm run build</code></h3>
<p>Builds the app for production to the <code>build</code> folder.<br />
It correctly bundles React in production mode and optimizes the build for the best performance.</p>
<p>The build is minified and the filenames include the hashes.<br />
Your app is ready to be deployed!</p>
<p>See the section about <a href="#deployment" target="_blank">deployment</a> for more information.</p>
<h3><code>npm run eject</code></h3>
<p><strong>Note: this is a one-way operation. Once you <code>eject</code>, you can’t go back!</strong></p>
<p>If you aren’t satisfied with the build tool and configuration choices, you can <code>eject</code> at any time. This command will remove the single build dependency from your project.</p>
<p>Instead, it will copy all the configuration files and the transitive dependencies (Webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except <code>eject</code> will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.</p>
<p>You don’t have to ever use <code>eject</code>. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.</p>
<h2>Supported Browsers</h2>
<p>By default, the generated project uses the latest version of React.</p>
<p>You can refer <a href="https://reactjs.org/docs/react-dom.html#browser-support" target="_blank">to the React documentation</a> for more information about supported browsers.</p>
<h2>Supported Language Features and Polyfills</h2>
<p>This project supports a superset of the latest JavaScript standard.<br />
In addition to <a href="https://github.com/lukehoban/es6features" target="_blank">ES6</a> syntax features, it also supports:</p>

<p>Learn more about <a href="https://babeljs.io/docs/plugins/#presets-stage-x-experimental-presets-" target="_blank">different proposal stages</a>.</p>
<p>While we recommend using experimental proposals with some caution, Facebook heavily uses these features in the product code, so we intend to provide <a href="https://medium.com/@cpojer/effective-javascript-codemods-5a6686bb46fb" target="_blank">codemods</a> if any of these proposals change in the future.</p>
<p>Note that <strong>the project only includes a few ES6 <a href="https://en.wikipedia.org/wiki/Polyfill" target="_blank">polyfills</a></strong>:</p>

<p>If you use any other ES6+ features that need <strong>runtime support</strong> (such as <code>Array.from()</code> or <code>Symbol</code>), make sure you are including the appropriate polyfills manually, or that the browsers you are targeting already support them.</p>
<p>Also note that using some newer syntax features like <code>for...of</code> or <code>[...nonArrayValue]</code> causes Babel to emit code that depends on ES6 runtime features and might not work without a polyfill. When in doubt, use <a href="https://babeljs.io/repl/" target="_blank">Babel REPL</a> to see what any specific syntax compiles down to.</p>
<h2>Syntax Highlighting in the Editor</h2>
<p>To configure the syntax highlighting in your favorite text editor, head to the <a href="https://babeljs.io/docs/editors" target="_blank">relevant Babel documentation page</a> and follow the instructions. Some of the most popular editors are covered.</p>
<h2>Displaying Lint Output in the Editor</h2>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@0.2.0</code> and higher.<br />
It also only works with npm 3 or higher.</p>
</blockquote>
<p>Some editors, including Sublime Text, Atom, and Visual Studio Code, provide plugins for ESLint.</p>
<p>They are not required for linting. You should see the linter output right in your terminal as well as the browser console. However, if you prefer the lint results to appear right in your editor, there are some extra steps you can do.</p>
<p>You would need to install an ESLint plugin for your editor first. Then, add a file called <code>.eslintrc</code> to the project root:</p>
<div><pre>{
  "extends": "react-app"
}</pre></div>
<p>Now your editor should report the linting warnings.</p>
<p>Note that even if you edit your <code>.eslintrc</code> file further, these changes will <strong>only affect the editor integration</strong>. They won’t affect the terminal and in-browser lint output. This is because Create React App intentionally provides a minimal set of rules that find common mistakes.</p>
<p>If you want to enforce a coding style for your project, consider using <a href="https://github.com/jlongster/prettier" target="_blank">Prettier</a> instead of ESLint style rules.</p>
<h2>Debugging in the Editor</h2>
<p><strong>This feature is currently only supported by <a href="https://code.visualstudio.com" target="_blank">Visual Studio Code</a> and <a href="https://www.jetbrains.com/webstorm/" target="_blank">WebStorm</a>.</strong></p>
<p>Visual Studio Code and WebStorm support debugging out of the box with Create React App. This enables you as a developer to write and debug your React code without leaving the editor, and most importantly it enables you to have a continuous development workflow, where context switching is minimal, as you don’t have to switch between tools.</p>
<h3>Visual Studio Code</h3>
<p>You would need to have the latest version of <a href="https://code.visualstudio.com" target="_blank">VS Code</a> and VS Code <a href="https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome" target="_blank">Chrome Debugger Extension</a> installed.</p>
<p>Then add the block below to your <code>launch.json</code> file and put it inside the <code>.vscode</code> folder in your app’s root directory.</p>
<div><pre>{
  "version": "0.2.0",
  "configurations": [{
    "name": "Chrome",
    "type": "chrome",
    "request": "launch",
    "url": "http://localhost:3000",
    "webRoot": "${workspaceRoot}/src",
    "sourceMapPathOverrides": {
      "webpack:///src/*": "${webRoot}/*"
    }
  }]
}</pre></div>
<blockquote>
<p>Note: the URL may be different if you've made adjustments via the <a href="#advanced-configuration" target="_blank">HOST or PORT environment variables</a>.</p>
</blockquote>
<p>Start your app by running <code>npm start</code>, and start debugging in VS Code by pressing <code>F5</code> or by clicking the green debug icon. You can now write code, set breakpoints, make changes to the code, and debug your newly modified code—all from your editor.</p>
<p>Having problems with VS Code Debugging? Please see their <a href="https://github.com/Microsoft/vscode-chrome-debug/blob/master/README.md#troubleshooting" target="_blank">troubleshooting guide</a>.</p>
<h3>WebStorm</h3>
<p>You would need to have <a href="https://www.jetbrains.com/webstorm/" target="_blank">WebStorm</a> and <a href="https://chrome.google.com/webstore/detail/jetbrains-ide-support/hmhgeddbohgjknpmjagkdomcpobmllji" target="_blank">JetBrains IDE Support</a> Chrome extension installed.</p>
<p>In the WebStorm menu <code>Run</code> select <code>Edit Configurations...</code>. Then click <code>+</code> and select <code>JavaScript Debug</code>. Paste <code>http://localhost:3000</code> into the URL field and save the configuration.</p>
<blockquote>
<p>Note: the URL may be different if you've made adjustments via the <a href="#advanced-configuration" target="_blank">HOST or PORT environment variables</a>.</p>
</blockquote>
<p>Start your app by running <code>npm start</code>, then press <code>^D</code> on macOS or <code>F9</code> on Windows and Linux or click the green debug icon to start debugging in WebStorm.</p>
<p>The same way you can debug your application in IntelliJ IDEA Ultimate, PhpStorm, PyCharm Pro, and RubyMine.</p>
<h2>Formatting Code Automatically</h2>
<p>Prettier is an opinionated code formatter with support for JavaScript, CSS and JSON. With Prettier you can format the code you write automatically to ensure a code style within your project. See the <a href="https://github.com/prettier/prettier" target="_blank">Prettier's GitHub page</a> for more information, and look at this <a href="https://prettier.github.io/prettier/" target="_blank">page to see it in action</a>.</p>
<p>To format our code whenever we make a commit in git, we need to install the following dependencies:</p>
<div><pre>npm install --save husky lint-staged prettier</pre></div>
<p>Alternatively you may use <code>yarn</code>:</p>
<div><pre>yarn add husky lint-staged prettier</pre></div>
<ul>
<li><code>husky</code> makes it easy to use githooks as if they are npm scripts.</li>
<li><code>lint-staged</code> allows us to run scripts on staged files in git. See this <a href="https://medium.com/@okonetchnikov/make-linting-great-again-f3890e1ad6b8" target="_blank">blog post about lint-staged to learn more about it</a>.</li>
<li><code>prettier</code> is the JavaScript formatter we will run before commits.</li>
</ul>
<p>Now we can make sure every file is formatted correctly by adding a few lines to the <code>package.json</code> in the project root.</p>
<p>Add the following line to <code>scripts</code> section:</p>
<div><pre>  "scripts": {
+   "precommit": "lint-staged",
    "start": "react-scripts start",
    "build": "react-scripts build",</pre></div>
<p>Next we add a 'lint-staged' field to the <code>package.json</code>, for example:</p>
<div><pre>  "dependencies": {
    // ...
  },
+ "lint-staged": {
+   "src/**/*.{js,jsx,json,css}": [
+     "prettier --single-quote --write",
+     "git add"
+   ]
+ },
  "scripts": {</pre></div>
<p>Now, whenever you make a commit, Prettier will format the changed files automatically. You can also run <code>./node_modules/.bin/prettier --single-quote --write "src/**/*.{js,jsx,json,css}"</code> to format your entire project for the first time.</p>
<p>Next you might want to integrate Prettier in your favorite editor. Read the section on <a href="https://prettier.io/docs/en/editors.html" target="_blank">Editor Integration</a> on the Prettier GitHub page.</p>
<h2>Changing the Page <code>&lt;title&gt;</code></h2>
<p>You can find the source HTML file in the <code>public</code> folder of the generated project. You may edit the <code>&lt;title&gt;</code> tag in it to change the title from “React App” to anything else.</p>
<p>Note that normally you wouldn’t edit files in the <code>public</code> folder very often. For example, <a href="#adding-a-stylesheet" target="_blank">adding a stylesheet</a> is done without touching the HTML.</p>
<p>If you need to dynamically update the page title based on the content, you can use the browser <a href="https://developer.mozilla.org/en-US/docs/Web/API/Document/title" target="_blank"><code>document.title</code></a> API. For more complex scenarios when you want to change the title from React components, you can use <a href="https://github.com/nfl/react-helmet" target="_blank">React Helmet</a>, a third party library.</p>
<p>If you use a custom server for your app in production and want to modify the title before it gets sent to the browser, you can follow advice in <a href="#generating-dynamic-meta-tags-on-the-server" target="_blank">this section</a>. Alternatively, you can pre-build each page as a static HTML file which then loads the JavaScript bundle, which is covered <a href="#pre-rendering-into-static-html-files" target="_blank">here</a>.</p>
<h2>Installing a Dependency</h2>
<p>The generated project includes React and ReactDOM as dependencies. It also includes a set of scripts used by Create React App as a development dependency. You may install other dependencies (for example, React Router) with <code>npm</code>:</p>
<div><pre>npm install --save react-router</pre></div>
<p>Alternatively you may use <code>yarn</code>:</p>
<div><pre>yarn add react-router</pre></div>
<p>This works for any library, not just <code>react-router</code>.</p>
<h2>Importing a Component</h2>
<p>This project setup supports ES6 modules thanks to Babel.<br />
While you can still use <code>require()</code> and <code>module.exports</code>, we encourage you to use <a href="http://exploringjs.com/es6/ch_modules.html" target="_blank"><code>import</code> and <code>export</code></a> instead.</p>
<p>For example:</p>
<h3><code>Button.js</code></h3>
<div><pre>import React, { Component } from 'react';

class Button extends Component {
  render() {
    // ...
  }
}

export default Button; // Don’t forget to use export default!</pre></div>
<h3><code>DangerButton.js</code></h3>
<div><pre>import React, { Component } from 'react';
import Button from './Button'; // Import a component from another file

class DangerButton extends Component {
  render() {
    return &lt;Button color="red" /&gt;;
  }
}

export default DangerButton;</pre></div>
<p>Be aware of the <a href="http://stackoverflow.com/questions/36795819/react-native-es-6-when-should-i-use-curly-braces-for-import/36796281#36796281" target="_blank">difference between default and named exports</a>. It is a common source of mistakes.</p>
<p>We suggest that you stick to using default imports and exports when a module only exports a single thing (for example, a component). That’s what you get when you use <code>export default Button</code> and <code>import Button from './Button'</code>.</p>
<p>Named exports are useful for utility modules that export several functions. A module may have at most one default export and as many named exports as you like.</p>
<p>Learn more about ES6 modules:</p>

<h2>Code Splitting</h2>
<p>Instead of downloading the entire app before users can use it, code splitting allows you to split your code into small chunks which you can then load on demand.</p>
<p>This project setup supports code splitting via <a href="http://2ality.com/2017/01/import-operator.html#loading-code-on-demand" target="_blank">dynamic <code>import()</code></a>. Its <a href="https://github.com/tc39/proposal-dynamic-import" target="_blank">proposal</a> is in stage 3. The <code>import()</code> function-like form takes the module name as an argument and returns a <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise" target="_blank"><code>Promise</code></a> which always resolves to the namespace object of the module.</p>
<p>Here is an example:</p>
<h3><code>moduleA.js</code></h3>
<div><pre>const moduleA = 'Hello';

export { moduleA };</pre></div>
<h3><code>App.js</code></h3>
<div><pre>import React, { Component } from 'react';

class App extends Component {
  handleClick = () =&gt; {
    import('./moduleA')
      .then(({ moduleA }) =&gt; {
        // Use moduleA
      })
      .catch(err =&gt; {
        // Handle failure
      });
  };

  render() {
    return (
      &lt;div&gt;
        &lt;button onClick={this.handleClick}&gt;Load&lt;/button&gt;
      &lt;/div&gt;
    );
  }
}

export default App;</pre></div>
<p>This will make <code>moduleA.js</code> and all its unique dependencies as a separate chunk that only loads after the user clicks the 'Load' button.</p>
<p>You can also use it with <code>async</code> / <code>await</code> syntax if you prefer it.</p>
<h3>With React Router</h3>
<p>If you are using React Router check out <a href="http://serverless-stack.com/chapters/code-splitting-in-create-react-app.html" target="_blank">this tutorial</a> on how to use code splitting with it. You can find the companion GitHub repository <a href="https://github.com/AnomalyInnovations/serverless-stack-demo-client/tree/code-splitting-in-create-react-app" target="_blank">here</a>.</p>
<p>Also check out the <a href="https://reactjs.org/docs/code-splitting.html" target="_blank">Code Splitting</a> section in React documentation.</p>
<h2>Adding a Stylesheet</h2>
<p>This project setup uses <a href="https://webpack.js.org/" target="_blank">Webpack</a> for handling all assets. Webpack offers a custom way of “extending” the concept of <code>import</code> beyond JavaScript. To express that a JavaScript file depends on a CSS file, you need to <strong>import the CSS from the JavaScript file</strong>:</p>
<h3><code>Button.css</code></h3>
<div><pre>.Button {
  padding: 20px;
}</pre></div>
<h3><code>Button.js</code></h3>
<div><pre>import React, { Component } from 'react';
import './Button.css'; // Tell Webpack that Button.js uses these styles

class Button extends Component {
  render() {
    // You can use them as regular CSS styles
    return &lt;div className="Button" /&gt;;
  }
}</pre></div>
<p><strong>This is not required for React</strong> but many people find this feature convenient. You can read about the benefits of this approach <a href="https://medium.com/seek-ui-engineering/block-element-modifying-your-javascript-components-d7f99fcab52b" target="_blank">here</a>. However you should be aware that this makes your code less portable to other build tools and environments than Webpack.</p>
<p>In development, expressing dependencies this way allows your styles to be reloaded on the fly as you edit them. In production, all CSS files will be concatenated into a single minified <code>.css</code> file in the build output.</p>
<p>If you are concerned about using Webpack-specific semantics, you can put all your CSS right into <code>src/index.css</code>. It would still be imported from <code>src/index.js</code>, but you could always remove that import if you later migrate to a different build tool.</p>
<h2>Post-Processing CSS</h2>
<p>This project setup minifies your CSS and adds vendor prefixes to it automatically through <a href="https://github.com/postcss/autoprefixer" target="_blank">Autoprefixer</a> so you don’t need to worry about it.</p>
<p>For example, this:</p>
<div><pre>.App {
  display: flex;
  flex-direction: row;
  align-items: center;
}</pre></div>
<p>becomes this:</p>
<div><pre>.App {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
  -webkit-box-align: center;
      -ms-flex-align: center;
          align-items: center;
}</pre></div>
<p>If you need to disable autoprefixing for some reason, <a href="https://github.com/postcss/autoprefixer#disabling" target="_blank">follow this section</a>.</p>
<h2>Adding a CSS Preprocessor (Sass, Less etc.)</h2>
<p>Generally, we recommend that you don’t reuse the same CSS classes across different components. For example, instead of using a <code>.Button</code> CSS class in <code>&lt;AcceptButton&gt;</code> and <code>&lt;RejectButton&gt;</code> components, we recommend creating a <code>&lt;Button&gt;</code> component with its own <code>.Button</code> styles, that both <code>&lt;AcceptButton&gt;</code> and <code>&lt;RejectButton&gt;</code> can render (but <a href="https://facebook.github.io/react/docs/composition-vs-inheritance.html" target="_blank">not inherit</a>).</p>
<p>Following this rule often makes CSS preprocessors less useful, as features like mixins and nesting are replaced by component composition. You can, however, integrate a CSS preprocessor if you find it valuable. In this walkthrough, we will be using Sass, but you can also use Less, or another alternative.</p>
<p>First, let’s install the command-line interface for Sass:</p>
<div><pre>npm install --save node-sass-chokidar</pre></div>
<p>Alternatively you may use <code>yarn</code>:</p>
<div><pre>yarn add node-sass-chokidar</pre></div>
<p>Then in <code>package.json</code>, add the following lines to <code>scripts</code>:</p>
<div><pre>   "scripts": {
+    "build-css": "node-sass-chokidar src/ -o src/",
+    "watch-css": "npm run build-css && node-sass-chokidar src/ -o src/ --watch --recursive",
     "start": "react-scripts start",
     "build": "react-scripts build",
     "test": "react-scripts test --env=jsdom",</pre></div>
<blockquote>
<p>Note: To use a different preprocessor, replace <code>build-css</code> and <code>watch-css</code> commands according to your preprocessor’s documentation.</p>
</blockquote>
<p>Now you can rename <code>src/App.css</code> to <code>src/App.scss</code> and run <code>npm run watch-css</code>. The watcher will find every Sass file in <code>src</code> subdirectories, and create a corresponding CSS file next to it, in our case overwriting <code>src/App.css</code>. Since <code>src/App.js</code> still imports <code>src/App.css</code>, the styles become a part of your application. You can now edit <code>src/App.scss</code>, and <code>src/App.css</code> will be regenerated.</p>
<p>To share variables between Sass files, you can use Sass imports. For example, <code>src/App.scss</code> and other component style files could include <code>@import "./shared.scss";</code> with variable definitions.</p>
<p>To enable importing files without using relative paths, you can add the  <code>--include-path</code> option to the command in <code>package.json</code>.</p>
<pre><code>"build-css": "node-sass-chokidar --include-path ./src --include-path ./node_modules src/ -o src/",
"watch-css": "npm run build-css && node-sass-chokidar --include-path ./src --include-path ./node_modules src/ -o src/ --watch --recursive",
</code></pre>
<p>This will allow you to do imports like</p>
<div><pre>@import 'styles/_colors.scss'; // assuming a styles directory under src/
@import 'nprogress/nprogress'; // importing a css file from the nprogress node module</pre></div>
<p>At this point you might want to remove all CSS files from the source control, and add <code>src/**/*.css</code> to your <code>.gitignore</code> file. It is generally a good practice to keep the build products outside of the source control.</p>
<p>As a final step, you may find it convenient to run <code>watch-css</code> automatically with <code>npm start</code>, and run <code>build-css</code> as a part of <code>npm run build</code>. You can use the <code>&&</code> operator to execute two scripts sequentially. However, there is no cross-platform way to run two scripts in parallel, so we will install a package for this:</p>
<div><pre>npm install --save npm-run-all</pre></div>
<p>Alternatively you may use <code>yarn</code>:</p>
<div><pre>yarn add npm-run-all</pre></div>
<p>Then we can change <code>start</code> and <code>build</code> scripts to include the CSS preprocessor commands:</p>
<div><pre>   "scripts": {
     "build-css": "node-sass-chokidar src/ -o src/",
     "watch-css": "npm run build-css && node-sass-chokidar src/ -o src/ --watch --recursive",
-    "start": "react-scripts start",
-    "build": "react-scripts build",
+    "start-js": "react-scripts start",
+    "start": "npm-run-all -p watch-css start-js",
+    "build-js": "react-scripts build",
+    "build": "npm-run-all build-css build-js",
     "test": "react-scripts test --env=jsdom",
     "eject": "react-scripts eject"
   }</pre></div>
<p>Now running <code>npm start</code> and <code>npm run build</code> also builds Sass files.</p>
<p><strong>Why <code>node-sass-chokidar</code>?</strong></p>
<p><code>node-sass</code> has been reported as having the following issues:</p>
<ul>
<li>
<p><code>node-sass --watch</code> has been reported to have <em>performance issues</em> in certain conditions when used in a virtual machine or with docker.</p>
</li>
<li>
<p>Infinite styles compiling <a href="https://github.com/facebookincubator/create-react-app/issues/1939" target="_blank">#1939</a></p>
</li>
<li>
<p><code>node-sass</code> has been reported as having issues with detecting new files in a directory <a href="https://github.com/sass/node-sass/issues/1891" target="_blank">#1891</a></p>
</li>
</ul>
<p><code>node-sass-chokidar</code> is used here as it addresses these issues.</p>
<h2>Adding Images, Fonts, and Files</h2>
<p>With Webpack, using static assets like images and fonts works similarly to CSS.</p>
<p>You can <strong><code>import</code> a file right in a JavaScript module</strong>. This tells Webpack to include that file in the bundle. Unlike CSS imports, importing a file gives you a string value. This value is the final path you can reference in your code, e.g. as the <code>src</code> attribute of an image or the <code>href</code> of a link to a PDF.</p>
<p>To reduce the number of requests to the server, importing images that are less than 10,000 bytes returns a <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URIs" target="_blank">data URI</a> instead of a path. This applies to the following file extensions: bmp, gif, jpg, jpeg, and png. SVG files are excluded due to <a href="https://github.com/facebookincubator/create-react-app/issues/1153" target="_blank">#1153</a>.</p>
<p>Here is an example:</p>
<div><pre>import React from 'react';
import logo from './logo.png'; // Tell Webpack this JS file uses this image

console.log(logo); // /logo.84287d09.png

function Header() {
  // Import result is the URL of your image
  return &lt;img src={logo} alt="Logo" /&gt;;
}

export default Header;</pre></div>
<p>This ensures that when the project is built, Webpack will correctly move the images into the build folder, and provide us with correct paths.</p>
<p>This works in CSS too:</p>
<div><pre>.Logo {
  background-image: url(./logo.png);
}</pre></div>
<p>Webpack finds all relative module references in CSS (they start with <code>./</code>) and replaces them with the final paths from the compiled bundle. If you make a typo or accidentally delete an important file, you will see a compilation error, just like when you import a non-existent JavaScript module. The final filenames in the compiled bundle are generated by Webpack from content hashes. If the file content changes in the future, Webpack will give it a different name in production so you don’t need to worry about long-term caching of assets.</p>
<p>Please be advised that this is also a custom feature of Webpack.</p>
<p><strong>It is not required for React</strong> but many people enjoy it (and React Native uses a similar mechanism for images).<br />
An alternative way of handling static assets is described in the next section.</p>
<h2>Using the <code>public</code> Folder</h2>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@0.5.0</code> and higher.</p>
</blockquote>
<h3>Changing the HTML</h3>
<p>The <code>public</code> folder contains the HTML file so you can tweak it, for example, to <a href="#changing-the-page-title" target="_blank">set the page title</a>.
The <code>&lt;script&gt;</code> tag with the compiled code will be added to it automatically during the build process.</p>
<h3>Adding Assets Outside of the Module System</h3>
<p>You can also add other assets to the <code>public</code> folder.</p>
<p>Note that we normally encourage you to <code>import</code> assets in JavaScript files instead.
For example, see the sections on <a href="#adding-a-stylesheet" target="_blank">adding a stylesheet</a> and <a href="#adding-images-fonts-and-files" target="_blank">adding images and fonts</a>.
This mechanism provides a number of benefits:</p>
<ul>
<li>Scripts and stylesheets get minified and bundled together to avoid extra network requests.</li>
<li>Missing files cause compilation errors instead of 404 errors for your users.</li>
<li>Result filenames include content hashes so you don’t need to worry about browsers caching their old versions.</li>
</ul>
<p>However there is an <strong>escape hatch</strong> that you can use to add an asset outside of the module system.</p>
<p>If you put a file into the <code>public</code> folder, it will <strong>not</strong> be processed by Webpack. Instead it will be copied into the build folder untouched.   To reference assets in the <code>public</code> folder, you need to use a special variable called <code>PUBLIC_URL</code>.</p>
<p>Inside <code>index.html</code>, you can use it like this:</p>
<div><pre>&lt;link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico"&gt;</pre></div>
<p>Only files inside the <code>public</code> folder will be accessible by <code>%PUBLIC_URL%</code> prefix. If you need to use a file from <code>src</code> or <code>node_modules</code>, you’ll have to copy it there to explicitly specify your intention to make this file a part of the build.</p>
<p>When you run <code>npm run build</code>, Create React App will substitute <code>%PUBLIC_URL%</code> with a correct absolute path so your project works even if you use client-side routing or host it at a non-root URL.</p>
<p>In JavaScript code, you can use <code>process.env.PUBLIC_URL</code> for similar purposes:</p>
<div><pre>render() {
  // Note: this is an escape hatch and should be used sparingly!
  // Normally we recommend using `import` for getting asset URLs
  // as described in “Adding Images and Fonts” above this section.
  return &lt;img src={process.env.PUBLIC_URL + '/img/logo.png'} /&gt;;
}</pre></div>
<p>Keep in mind the downsides of this approach:</p>
<ul>
<li>None of the files in <code>public</code> folder get post-processed or minified.</li>
<li>Missing files will not be called at compilation time, and will cause 404 errors for your users.</li>
<li>Result filenames won’t include content hashes so you’ll need to add query arguments or rename them every time they change.</li>
</ul>
<h3>When to Use the <code>public</code> Folder</h3>
<p>Normally we recommend importing <a href="#adding-a-stylesheet" target="_blank">stylesheets</a>, <a href="#adding-images-fonts-and-files" target="_blank">images, and fonts</a> from JavaScript.
The <code>public</code> folder is useful as a workaround for a number of less common cases:</p>
<ul>
<li>You need a file with a specific name in the build output, such as <a href="https://developer.mozilla.org/en-US/docs/Web/Manifest" target="_blank"><code>manifest.webmanifest</code></a>.</li>
<li>You have thousands of images and need to dynamically reference their paths.</li>
<li>You want to include a small script like <a href="http://github.hubspot.com/pace/docs/welcome/" target="_blank"><code>pace.js</code></a> outside of the bundled code.</li>
<li>Some library may be incompatible with Webpack and you have no other option but to include it as a <code>&lt;script&gt;</code> tag.</li>
</ul>
<p>Note that if you add a <code>&lt;script&gt;</code> that declares global variables, you also need to read the next section on using them.</p>
<h2>Using Global Variables</h2>
<p>When you include a script in the HTML file that defines global variables and try to use one of these variables in the code, the linter will complain because it cannot see the definition of the variable.</p>
<p>You can avoid this by reading the global variable explicitly from the <code>window</code> object, for example:</p>
<div><pre>const $ = window.$;</pre></div>
<p>This makes it obvious you are using a global variable intentionally rather than because of a typo.</p>
<p>Alternatively, you can force the linter to ignore any line by adding <code>// eslint-disable-line</code> after it.</p>
<h2>Adding Bootstrap</h2>
<p>You don’t have to use <a href="https://react-bootstrap.github.io" target="_blank">React Bootstrap</a> together with React but it is a popular library for integrating Bootstrap with React apps. If you need it, you can integrate it with Create React App by following these steps:</p>
<p>Install React Bootstrap and Bootstrap from npm. React Bootstrap does not include Bootstrap CSS so this needs to be installed as well:</p>
<div><pre>npm install --save react-bootstrap bootstrap@3</pre></div>
<p>Alternatively you may use <code>yarn</code>:</p>
<div><pre>yarn add react-bootstrap bootstrap@3</pre></div>
<p>Import Bootstrap CSS and optionally Bootstrap theme CSS in the beginning of your <code>src/index.js</code> file:</p>
<div><pre>import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap/dist/css/bootstrap-theme.css';
// Put any other imports below so that CSS from your
// components takes precedence over default styles.</pre></div>
<p>Import required React Bootstrap components within <code>src/App.js</code> file or your custom component files:</p>
<div><pre>import { Navbar, Jumbotron, Button } from 'react-bootstrap';</pre></div>
<p>Now you are ready to use the imported React Bootstrap components within your component hierarchy defined in the render method. Here is an example <a href="https://gist.githubusercontent.com/gaearon/85d8c067f6af1e56277c82d19fd4da7b/raw/6158dd991b67284e9fc8d70b9d973efe87659d72/App.js" target="_blank"><code>App.js</code></a> redone using React Bootstrap.</p>
<h3>Using a Custom Theme</h3>
<p>Sometimes you might need to tweak the visual styles of Bootstrap (or equivalent package).<br />
We suggest the following approach:</p>
<ul>
<li>Create a new package that depends on the package you wish to customize, e.g. Bootstrap.</li>
<li>Add the necessary build steps to tweak the theme, and publish your package on npm.</li>
<li>Install your own theme npm package as a dependency of your app.</li>
</ul>
<p>Here is an example of adding a <a href="https://medium.com/@tacomanator/customizing-create-react-app-aa9ffb88165" target="_blank">customized Bootstrap</a> that follows these steps.</p>
<h2>Adding Flow</h2>
<p>Flow is a static type checker that helps you write code with fewer bugs. Check out this <a href="https://medium.com/@preethikasireddy/why-use-static-types-in-javascript-part-1-8382da1e0adb" target="_blank">introduction to using static types in JavaScript</a> if you are new to this concept.</p>
<p>Recent versions of <a href="http://flowtype.org/" target="_blank">Flow</a> work with Create React App projects out of the box.</p>
<p>To add Flow to a Create React App project, follow these steps:</p>
<ol>
<li>Run <code>npm install --save flow-bin</code> (or <code>yarn add flow-bin</code>).</li>
<li>Add <code>"flow": "flow"</code> to the <code>scripts</code> section of your <code>package.json</code>.</li>
<li>Run <code>npm run flow init</code> (or <code>yarn flow init</code>) to create a <a href="https://flowtype.org/docs/advanced-configuration.html" target="_blank"><code>.flowconfig</code> file</a> in the root directory.</li>
<li>Add <code>// @flow</code> to any files you want to type check (for example, to <code>src/App.js</code>).</li>
</ol>
<p>Now you can run <code>npm run flow</code> (or <code>yarn flow</code>) to check the files for type errors.
You can optionally use an IDE like <a href="https://nuclide.io/docs/languages/flow/" target="_blank">Nuclide</a> for a better integrated experience.
In the future we plan to integrate it into Create React App even more closely.</p>
<p>To learn more about Flow, check out <a href="https://flowtype.org/" target="_blank">its documentation</a>.</p>
<h2>Adding a Router</h2>
<p>Create React App doesn't prescribe a specific routing solution, but <a href="https://reacttraining.com/react-router/" target="_blank">React Router</a> is the most popular one.</p>
<p>To add it, run:</p>
<div><pre>npm install --save react-router-dom</pre></div>
<p>Alternatively you may use <code>yarn</code>:</p>
<div><pre>yarn add react-router-dom</pre></div>
<p>To try it, delete all the code in <code>src/App.js</code> and replace it with any of the examples on its website. The <a href="https://reacttraining.com/react-router/web/example/basic" target="_blank">Basic Example</a> is a good place to get started.</p>
<p>Note that <a href="#serving-apps-with-client-side-routing" target="_blank">you may need to configure your production server to support client-side routing</a> before deploying your app.</p>
<h2>Adding Custom Environment Variables</h2>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@0.2.3</code> and higher.</p>
</blockquote>
<p>Your project can consume variables declared in your environment as if they were declared locally in your JS files. By
default you will have <code>NODE_ENV</code> defined for you, and any other environment variables starting with
<code>REACT_APP_</code>.</p>
<p><strong>The environment variables are embedded during the build time</strong>. Since Create React App produces a static HTML/CSS/JS bundle, it can’t possibly read them at runtime. To read them at runtime, you would need to load HTML into memory on the server and replace placeholders in runtime, just like <a href="#injecting-data-from-the-server-into-the-page" target="_blank">described here</a>. Alternatively you can rebuild the app on the server anytime you change them.</p>
<blockquote>
<p>Note: You must create custom environment variables beginning with <code>REACT_APP_</code>. Any other variables except <code>NODE_ENV</code> will be ignored to avoid accidentally <a href="https://github.com/facebookincubator/create-react-app/issues/865#issuecomment-252199527" target="_blank">exposing a private key on the machine that could have the same name</a>. Changing any environment variables will require you to restart the development server if it is running.</p>
</blockquote>
<p>These environment variables will be defined for you on <code>process.env</code>. For example, having an environment
variable named <code>REACT_APP_SECRET_CODE</code> will be exposed in your JS as <code>process.env.REACT_APP_SECRET_CODE</code>.</p>
<p>There is also a special built-in environment variable called <code>NODE_ENV</code>. You can read it from <code>process.env.NODE_ENV</code>. When you run <code>npm start</code>, it is always equal to <code>'development'</code>, when you run <code>npm test</code> it is always equal to <code>'test'</code>, and when you run <code>npm run build</code> to make a production bundle, it is always equal to <code>'production'</code>. <strong>You cannot override <code>NODE_ENV</code> manually.</strong> This prevents developers from accidentally deploying a slow development build to production.</p>
<p>These environment variables can be useful for displaying information conditionally based on where the project is
deployed or consuming sensitive data that lives outside of version control.</p>
<p>First, you need to have environment variables defined. For example, let’s say you wanted to consume a secret defined
in the environment inside a <code>&lt;form&gt;</code>:</p>
<div><pre>render() {
  return (
    &lt;div&gt;
      &lt;small&gt;You are running this application in &lt;b&gt;{process.env.NODE_ENV}&lt;/b&gt; mode.&lt;/small&gt;
      &lt;form&gt;
        &lt;input type="hidden" defaultValue={process.env.REACT_APP_SECRET_CODE} /&gt;
      &lt;/form&gt;
    &lt;/div&gt;
  );
}</pre></div>
<p>During the build, <code>process.env.REACT_APP_SECRET_CODE</code> will be replaced with the current value of the <code>REACT_APP_SECRET_CODE</code> environment variable. Remember that the <code>NODE_ENV</code> variable will be set for you automatically.</p>
<p>When you load the app in the browser and inspect the <code>&lt;input&gt;</code>, you will see its value set to <code>abcdef</code>, and the bold text will show the environment provided when using <code>npm start</code>:</p>
<div><pre>&lt;div&gt;
  &lt;small&gt;You are running this application in &lt;b&gt;development&lt;/b&gt; mode.&lt;/small&gt;
  &lt;form&gt;
    &lt;input type="hidden" value="abcdef" /&gt;
  &lt;/form&gt;
&lt;/div&gt;</pre></div>
<p>The above form is looking for a variable called <code>REACT_APP_SECRET_CODE</code> from the environment. In order to consume this
value, we need to have it defined in the environment. This can be done using two ways: either in your shell or in
a <code>.env</code> file. Both of these ways are described in the next few sections.</p>
<p>Having access to the <code>NODE_ENV</code> is also useful for performing actions conditionally:</p>
<div><pre>if (process.env.NODE_ENV !== 'production') {
  analytics.disable();
}</pre></div>
<p>When you compile the app with <code>npm run build</code>, the minification step will strip out this condition, and the resulting bundle will be smaller.</p>
<h3>Referencing Environment Variables in the HTML</h3>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@0.9.0</code> and higher.</p>
</blockquote>
<p>You can also access the environment variables starting with <code>REACT_APP_</code> in the <code>public/index.html</code>. For example:</p>
<div><pre>&lt;title&gt;%REACT_APP_WEBSITE_NAME%&lt;/title&gt;</pre></div>
<p>Note that the caveats from the above section apply:</p>
<ul>
<li>Apart from a few built-in variables (<code>NODE_ENV</code> and <code>PUBLIC_URL</code>), variable names must start with <code>REACT_APP_</code> to work.</li>
<li>The environment variables are injected at build time. If you need to inject them at runtime, <a href="#generating-dynamic-meta-tags-on-the-server" target="_blank">follow this approach instead</a>.</li>
</ul>
<h3>Adding Temporary Environment Variables In Your Shell</h3>
<p>Defining environment variables can vary between OSes. It’s also important to know that this manner is temporary for the
life of the shell session.</p>
<h4>Windows (cmd.exe)</h4>
<div><pre>set "REACT_APP_SECRET_CODE=abcdef" && npm start</pre></div>
<p>(Note: Quotes around the variable assignment are required to avoid a trailing whitespace.)</p>
<h4>Windows (Powershell)</h4>
<div><pre>($env:REACT_APP_SECRET_CODE = "abcdef") -and (npm start)</pre></div>
<h4>Linux, macOS (Bash)</h4>
<div><pre>REACT_APP_SECRET_CODE=abcdef npm start</pre></div>
<h3>Adding Development Environment Variables In <code>.env</code></h3>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@0.5.0</code> and higher.</p>
</blockquote>
<p>To define permanent environment variables, create a file called <code>.env</code> in the root of your project:</p>
<pre><code>REACT_APP_SECRET_CODE=abcdef
</code></pre>
<blockquote>
<p>Note: You must create custom environment variables beginning with <code>REACT_APP_</code>. Any other variables except <code>NODE_ENV</code> will be ignored to avoid <a href="https://github.com/facebookincubator/create-react-app/issues/865#issuecomment-252199527" target="_blank">accidentally exposing a private key on the machine that could have the same name</a>. Changing any environment variables will require you to restart the development server if it is running.</p>
</blockquote>
<p><code>.env</code> files <strong>should be</strong> checked into source control (with the exclusion of <code>.env*.local</code>).</p>
<h4>What other <code>.env</code> files can be used?</h4>
<blockquote>
<p>Note: this feature is <strong>available with <code>react-scripts@1.0.0</code> and higher</strong>.</p>
</blockquote>
<ul>
<li><code>.env</code>: Default.</li>
<li><code>.env.local</code>: Local overrides. <strong>This file is loaded for all environments except test.</strong></li>
<li><code>.env.development</code>, <code>.env.test</code>, <code>.env.production</code>: Environment-specific settings.</li>
<li><code>.env.development.local</code>, <code>.env.test.local</code>, <code>.env.production.local</code>: Local overrides of environment-specific settings.</li>
</ul>
<p>Files on the left have more priority than files on the right:</p>
<ul>
<li><code>npm start</code>: <code>.env.development.local</code>, <code>.env.development</code>, <code>.env.local</code>, <code>.env</code></li>
<li><code>npm run build</code>: <code>.env.production.local</code>, <code>.env.production</code>, <code>.env.local</code>, <code>.env</code></li>
<li><code>npm test</code>: <code>.env.test.local</code>, <code>.env.test</code>, <code>.env</code> (note <code>.env.local</code> is missing)</li>
</ul>
<p>These variables will act as the defaults if the machine does not explicitly set them.<br />
Please refer to the <a href="https://github.com/motdotla/dotenv" target="_blank">dotenv documentation</a> for more details.</p>
<blockquote>
<p>Note: If you are defining environment variables for development, your CI and/or hosting platform will most likely need
these defined as well. Consult their documentation how to do this. For example, see the documentation for <a href="https://docs.travis-ci.com/user/environment-variables/" target="_blank">Travis CI</a> or <a href="https://devcenter.heroku.com/articles/config-vars" target="_blank">Heroku</a>.</p>
</blockquote>
<h4>Expanding Environment Variables In <code>.env</code></h4>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@1.1.0</code> and higher.</p>
</blockquote>
<p>Expand variables already on your machine for use in your <code>.env</code> file (using <a href="https://github.com/motdotla/dotenv-expand" target="_blank">dotenv-expand</a>).</p>
<p>For example, to get the environment variable <code>npm_package_version</code>:</p>
<pre><code>REACT_APP_VERSION=$npm_package_version
# also works:
# REACT_APP_VERSION=${npm_package_version}
</code></pre>
<p>Or expand variables local to the current <code>.env</code> file:</p>
<pre><code>DOMAIN=www.example.com
REACT_APP_FOO=$DOMAIN/foo
REACT_APP_BAR=$DOMAIN/bar
</code></pre>
<h2>Can I Use Decorators?</h2>
<p>Many popular libraries use <a href="https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841" target="_blank">decorators</a> in their documentation.<br />
Create React App doesn’t support decorator syntax at the moment because:</p>
<ul>
<li>It is an experimental proposal and is subject to change.</li>
<li>The current specification version is not officially supported by Babel.</li>
<li>If the specification changes, we won’t be able to write a codemod because we don’t use them internally at Facebook.</li>
</ul>
<p>However in many cases you can rewrite decorator-based code without decorators just as fine.<br />
Please refer to these two threads for reference:</p>

<p>Create React App will add decorator support when the specification advances to a stable stage.</p>
<h2>Fetching Data with AJAX Requests</h2>
<p>React doesn't prescribe a specific approach to data fetching, but people commonly use either a library like <a href="https://github.com/axios/axios" target="_blank">axios</a> or the <a href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API" target="_blank"><code>fetch()</code> API</a> provided by the browser. Conveniently, Create React App includes a polyfill for <code>fetch()</code> so you can use it without worrying about the browser support.</p>
<p>The global <code>fetch</code> function allows to easily makes AJAX requests. It takes in a URL as an input and returns a <code>Promise</code> that resolves to a <code>Response</code> object. You can find more information about <code>fetch</code> <a href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch" target="_blank">here</a>.</p>
<p>This project also includes a <a href="https://github.com/then/promise" target="_blank">Promise polyfill</a> which provides a full implementation of Promises/A+. A Promise represents the eventual result of an asynchronous operation, you can find more information about Promises <a href="https://www.promisejs.org/" target="_blank">here</a> and <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise" target="_blank">here</a>. Both axios and <code>fetch()</code> use Promises under the hood. You can also use the <a href="https://davidwalsh.name/async-await" target="_blank"><code>async / await</code></a> syntax to reduce the callback nesting.</p>
<p>You can learn more about making AJAX requests from React components in <a href="https://reactjs.org/docs/faq-ajax.html" target="_blank">the FAQ entry on the React website</a>.</p>
<h2>Integrating with an API Backend</h2>
<p>These tutorials will help you to integrate your app with an API backend running on another port,
using <code>fetch()</code> to access it.</p>

<p>Check out <a href="https://www.fullstackreact.com/articles/using-create-react-app-with-a-server/" target="_blank">this tutorial</a>.
You can find the companion GitHub repository <a href="https://github.com/fullstackreact/food-lookup-demo" target="_blank">here</a>.</p>
<h3>Ruby on Rails</h3>
<p>Check out <a href="https://www.fullstackreact.com/articles/how-to-get-create-react-app-to-work-with-your-rails-api/" target="_blank">this tutorial</a>.
You can find the companion GitHub repository <a href="https://github.com/fullstackreact/food-lookup-demo-rails" target="_blank">here</a>.</p>
<h2>Proxying API Requests in Development</h2>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@0.2.3</code> and higher.</p>
</blockquote>
<p>People often serve the front-end React app from the same host and port as their backend implementation.<br />
For example, a production setup might look like this after the app is deployed:</p>
<pre><code>/             - static server returns index.html with React app
/todos        - static server returns index.html with React app
/api/todos    - server handles any /api/* requests using the backend implementation
</code></pre>
<p>Such setup is <strong>not</strong> required. However, if you <strong>do</strong> have a setup like this, it is convenient to write requests like <code>fetch('/api/todos')</code> without worrying about redirecting them to another host or port during development.</p>
<p>To tell the development server to proxy any unknown requests to your API server in development, add a <code>proxy</code> field to your <code>package.json</code>, for example:</p>
<div><pre>  "proxy": "http://localhost:4000",</pre></div>
<p>This way, when you <code>fetch('/api/todos')</code> in development, the development server will recognize that it’s not a static asset, and will proxy your request to <code>http://localhost:4000/api/todos</code> as a fallback. The development server will <strong>only</strong> attempt to send requests without <code>text/html</code> in its <code>Accept</code> header to the proxy.</p>
<p>Conveniently, this avoids <a href="http://stackoverflow.com/questions/21854516/understanding-ajax-cors-and-security-considerations" target="_blank">CORS issues</a> and error messages like this in development:</p>
<pre><code>Fetch API cannot load http://localhost:4000/api/todos. No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://localhost:3000' is therefore not allowed access. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.
</code></pre>
<p>Keep in mind that <code>proxy</code> only has effect in development (with <code>npm start</code>), and it is up to you to ensure that URLs like <code>/api/todos</code> point to the right thing in production. You don’t have to use the <code>/api</code> prefix. Any unrecognized request without a <code>text/html</code> accept header will be redirected to the specified <code>proxy</code>.</p>
<p>The <code>proxy</code> option supports HTTP, HTTPS and WebSocket connections.<br />
If the <code>proxy</code> option is <strong>not</strong> flexible enough for you, alternatively you can:</p>
<ul>
<li><a href="#configuring-the-proxy-manually" target="_blank">Configure the proxy yourself</a></li>
<li>Enable CORS on your server (<a href="http://enable-cors.org/server_expressjs.html" target="_blank">here’s how to do it for Express</a>).</li>
<li>Use <a href="#adding-custom-environment-variables" target="_blank">environment variables</a> to inject the right server host and port into your app.</li>
</ul>
<h3>"Invalid Host Header" Errors After Configuring Proxy</h3>
<p>When you enable the <code>proxy</code> option, you opt into a more strict set of host checks. This is necessary because leaving the backend open to remote hosts makes your computer vulnerable to DNS rebinding attacks. The issue is explained in <a href="https://medium.com/webpack/webpack-dev-server-middleware-security-issues-1489d950874a" target="_blank">this article</a> and <a href="https://github.com/webpack/webpack-dev-server/issues/887" target="_blank">this issue</a>.</p>
<p>This shouldn’t affect you when developing on <code>localhost</code>, but if you develop remotely like <a href="https://github.com/facebookincubator/create-react-app/issues/2271" target="_blank">described here</a>, you will see this error in the browser after enabling the <code>proxy</code> option:</p>
<blockquote>
<p>Invalid Host header</p>
</blockquote>
<p>To work around it, you can specify your public development host in a file called <code>.env.development</code> in the root of your project:</p>
<pre><code>HOST=mypublicdevhost.com
</code></pre>
<p>If you restart the development server now and load the app from the specified host, it should work.</p>
<p>If you are still having issues or if you’re using a more exotic environment like a cloud editor, you can bypass the host check completely by adding a line to <code>.env.development.local</code>. <strong>Note that this is dangerous and exposes your machine to remote code execution from malicious websites:</strong></p>
<pre><code># NOTE: THIS IS DANGEROUS!
# It exposes your machine to attacks from the websites you visit.
DANGEROUSLY_DISABLE_HOST_CHECK=true
</code></pre>
<p>We don’t recommend this approach.</p>
<h3>Configuring the Proxy Manually</h3>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@1.0.0</code> and higher.</p>
</blockquote>
<p>If the <code>proxy</code> option is <strong>not</strong> flexible enough for you, you can specify an object in the following form (in <code>package.json</code>).<br />
You may also specify any configuration value <a href="https://github.com/chimurai/http-proxy-middleware#options" target="_blank"><code>http-proxy-middleware</code></a> or <a href="https://github.com/nodejitsu/node-http-proxy#options" target="_blank"><code>http-proxy</code></a> supports.</p>
<div><pre>{
  // ...
  "proxy": {
    "/api": {
      "target": "&lt;url&gt;",
      "ws": true
      // ...
    }
  }
  // ...
}</pre></div>
<p>All requests matching this path will be proxies, no exceptions. This includes requests for <code>text/html</code>, which the standard <code>proxy</code> option does not proxy.</p>
<p>If you need to specify multiple proxies, you may do so by specifying additional entries.
Matches are regular expressions, so that you can use a regexp to match multiple paths.</p>
<div><pre>{
  // ...
  "proxy": {
    // Matches any request starting with /api
    "/api": {
      "target": "&lt;url_1&gt;",
      "ws": true
      // ...
    },
    // Matches any request starting with /foo
    "/foo": {
      "target": "&lt;url_2&gt;",
      "ssl": true,
      "pathRewrite": {
        "^/foo": "/foo/beta"
      }
      // ...
    },
    // Matches /bar/abc.html but not /bar/sub/def.html
    "/bar/[^/]*[.]html": {
      "target": "&lt;url_3&gt;",
      // ...
    },
    // Matches /baz/abc.html and /baz/sub/def.html
    "/baz/.*/.*[.]html": {
      "target": "&lt;url_4&gt;"
      // ...
    }
  }
  // ...
}</pre></div>
<h3>Configuring a WebSocket Proxy</h3>
<p>When setting up a WebSocket proxy, there are a some extra considerations to be aware of.</p>
<p>If you’re using a WebSocket engine like <a href="https://socket.io/" target="_blank">Socket.io</a>, you must have a Socket.io server running that you can use as the proxy target. Socket.io will not work with a standard WebSocket server. Specifically, don't expect Socket.io to work with <a href="http://websocket.org/echo.html" target="_blank">the websocket.org echo test</a>.</p>
<p>There’s some good documentation available for <a href="https://socket.io/docs/" target="_blank">setting up a Socket.io server</a>.</p>
<p>Standard WebSockets <strong>will</strong> work with a standard WebSocket server as well as the websocket.org echo test. You can use libraries like <a href="https://github.com/websockets/ws" target="_blank">ws</a> for the server, with <a href="https://developer.mozilla.org/en-US/docs/Web/API/WebSocket" target="_blank">native WebSockets in the browser</a>.</p>
<p>Either way, you can proxy WebSocket requests manually in <code>package.json</code>:</p>
<div><pre>{
  // ...
  "proxy": {
    "/socket": {
      // Your compatible WebSocket server
      "target": "ws://&lt;socket_url&gt;",
      // Tell http-proxy-middleware that this is a WebSocket proxy.
      // Also allows you to proxy WebSocket requests without an additional HTTP request
      // https://github.com/chimurai/http-proxy-middleware#external-websocket-upgrade
      "ws": true
      // ...
    }
  }
  // ...
}</pre></div>
<h2>Using HTTPS in Development</h2>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@0.4.0</code> and higher.</p>
</blockquote>
<p>You may require the dev server to serve pages over HTTPS. One particular case where this could be useful is when using <a href="#proxying-api-requests-in-development" target="_blank">the "proxy" feature</a> to proxy requests to an API server when that API server is itself serving HTTPS.</p>
<p>To do this, set the <code>HTTPS</code> environment variable to <code>true</code>, then start the dev server as usual with <code>npm start</code>:</p>
<h4>Windows (cmd.exe)</h4>
<div><pre>set HTTPS=true&&npm start</pre></div>
<h4>Windows (Powershell)</h4>
<div><pre>($env:HTTPS = $true) -and (npm start)</pre></div>
<p>(Note: the lack of whitespace is intentional.)</p>
<h4>Linux, macOS (Bash)</h4>
<div><pre>HTTPS=true npm start</pre></div>
<p>Note that the server will use a self-signed certificate, so your web browser will almost definitely display a warning upon accessing the page.</p>
<h2>Generating Dynamic <code>&lt;meta&gt;</code> Tags on the Server</h2>
<p>Since Create React App doesn’t support server rendering, you might be wondering how to make <code>&lt;meta&gt;</code> tags dynamic and reflect the current URL. To solve this, we recommend to add placeholders into the HTML, like this:</p>
<div><pre>&lt;!doctype html&gt;
&lt;html lang="en"&gt;
  &lt;head&gt;
    &lt;meta property="og:title" content="__OG_TITLE__"&gt;
    &lt;meta property="og:description" content="__OG_DESCRIPTION__"&gt;</pre></div>
<p>Then, on the server, regardless of the backend you use, you can read <code>index.html</code> into memory and replace <code>__OG_TITLE__</code>, <code>__OG_DESCRIPTION__</code>, and any other placeholders with values depending on the current URL. Just make sure to sanitize and escape the interpolated values so that they are safe to embed into HTML!</p>
<p>If you use a Node server, you can even share the route matching logic between the client and the server. However duplicating it also works fine in simple cases.</p>
<h2>Pre-Rendering into Static HTML Files</h2>
<p>If you’re hosting your <code>build</code> with a static hosting provider you can use <a href="https://www.npmjs.com/package/react-snapshot" target="_blank">react-snapshot</a> or <a href="https://github.com/stereobooster/react-snap" target="_blank">react-snap</a> to generate HTML pages for each route, or relative link, in your application. These pages will then seamlessly become active, or “hydrated”, when the JavaScript bundle has loaded.</p>
<p>There are also opportunities to use this outside of static hosting, to take the pressure off the server when generating and caching routes.</p>
<p>The primary benefit of pre-rendering is that you get the core content of each page <em>with</em> the HTML payload—regardless of whether or not your JavaScript bundle successfully downloads. It also increases the likelihood that each route of your application will be picked up by search engines.</p>
<p>You can read more about <a href="https://medium.com/superhighfives/an-almost-static-stack-6df0a2791319" target="_blank">zero-configuration pre-rendering (also called snapshotting) here</a>.</p>
<h2>Injecting Data from the Server into the Page</h2>
<p>Similarly to the previous section, you can leave some placeholders in the HTML that inject global variables, for example:</p>
<div><pre>&lt;!doctype html&gt;
&lt;html lang="en"&gt;
  &lt;head&gt;
    &lt;script&gt;
      window.SERVER_DATA = __SERVER_DATA__;
    &lt;/script&gt;</pre></div>
<p>Then, on the server, you can replace <code>__SERVER_DATA__</code> with a JSON of real data right before sending the response. The client code can then read <code>window.SERVER_DATA</code> to use it. <strong>Make sure to <a href="https://medium.com/node-security/the-most-common-xss-vulnerability-in-react-js-applications-2bdffbcc1fa0" target="_blank">sanitize the JSON before sending it to the client</a> as it makes your app vulnerable to XSS attacks.</strong></p>
<h2>Running Tests</h2>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@0.3.0</code> and higher.<br />
<a href="https://github.com/facebookincubator/create-react-app/blob/master/CHANGELOG.md#migrating-from-023-to-030" target="_blank">Read the migration guide to learn how to enable it in older projects!</a></p>
</blockquote>
<p>Create React App uses <a href="https://facebook.github.io/jest/" target="_blank">Jest</a> as its test runner. To prepare for this integration, we did a <a href="https://facebook.github.io/jest/blog/2016/09/01/jest-15.html" target="_blank">major revamp</a> of Jest so if you heard bad things about it years ago, give it another try.</p>
<p>Jest is a Node-based runner. This means that the tests always run in a Node environment and not in a real browser. This lets us enable fast iteration speed and prevent flakiness.</p>
<p>While Jest provides browser globals such as <code>window</code> thanks to <a href="https://github.com/tmpvar/jsdom" target="_blank">jsdom</a>, they are only approximations of the real browser behavior. Jest is intended to be used for unit tests of your logic and your components rather than the DOM quirks.</p>
<p>We recommend that you use a separate tool for browser end-to-end tests if you need them. They are beyond the scope of Create React App.</p>
<h3>Filename Conventions</h3>
<p>Jest will look for test files with any of the following popular naming conventions:</p>
<ul>
<li>Files with <code>.js</code> suffix in <code>__tests__</code> folders.</li>
<li>Files with <code>.test.js</code> suffix.</li>
<li>Files with <code>.spec.js</code> suffix.</li>
</ul>
<p>The <code>.test.js</code> / <code>.spec.js</code> files (or the <code>__tests__</code> folders) can be located at any depth under the <code>src</code> top level folder.</p>
<p>We recommend to put the test files (or <code>__tests__</code> folders) next to the code they are testing so that relative imports appear shorter. For example, if <code>App.test.js</code> and <code>App.js</code> are in the same folder, the test just needs to <code>import App from './App'</code> instead of a long relative path. Colocation also helps find tests more quickly in larger projects.</p>
<h3>Command Line Interface</h3>
<p>When you run <code>npm test</code>, Jest will launch in the watch mode. Every time you save a file, it will re-run the tests, just like <code>npm start</code> recompiles the code.</p>
<p>The watcher includes an interactive command-line interface with the ability to run all tests, or focus on a search pattern. It is designed this way so that you can keep it open and enjoy fast re-runs. You can learn the commands from the “Watch Usage” note that the watcher prints after every run:</p>
<p><a href="https://camo.githubusercontent.com/e17b470bdfc383db6ea4b32c4257d04af6e1e749/687474703a2f2f66616365626f6f6b2e6769746875622e696f2f6a6573742f696d672f626c6f672f31352d77617463682e676966" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/e17b470bdfc383db6ea4b32c4257d04af6e1e749/687474703a2f2f66616365626f6f6b2e6769746875622e696f2f6a6573742f696d672f626c6f672f31352d77617463682e676966" alt="Jest watch mode" /></div></a></p>
<h3>Version Control Integration</h3>
<p>By default, when you run <code>npm test</code>, Jest will only run the tests related to files changed since the last commit. This is an optimization designed to make your tests run fast regardless of how many tests you have. However it assumes that you don’t often commit the code that doesn’t pass the tests.</p>
<p>Jest will always explicitly mention that it only ran tests related to the files changed since the last commit. You can also press <code>a</code> in the watch mode to force Jest to run all tests.</p>
<p>Jest will always run all tests on a <a href="#continuous-integration" target="_blank">continuous integration</a> server or if the project is not inside a Git or Mercurial repository.</p>
<h3>Writing Tests</h3>
<p>To create tests, add <code>it()</code> (or <code>test()</code>) blocks with the name of the test and its code. You may optionally wrap them in <code>describe()</code> blocks for logical grouping but this is neither required nor recommended.</p>
<p>Jest provides a built-in <code>expect()</code> global function for making assertions. A basic test could look like this:</p>
<div><pre>import sum from './sum';

it('sums numbers', () =&gt; {
  expect(sum(1, 2)).toEqual(3);
  expect(sum(2, 2)).toEqual(4);
});</pre></div>
<p>All <code>expect()</code> matchers supported by Jest are <a href="https://facebook.github.io/jest/docs/en/expect.html#content" target="_blank">extensively documented here</a>.<br />
You can also use <a href="https://facebook.github.io/jest/docs/en/expect.html#tohavebeencalled" target="_blank"><code>jest.fn()</code> and <code>expect(fn).toBeCalled()</code></a> to create “spies” or mock functions.</p>
<h3>Testing Components</h3>
<p>There is a broad spectrum of component testing techniques. They range from a “smoke test” verifying that a component renders without throwing, to shallow rendering and testing some of the output, to full rendering and testing component lifecycle and state changes.</p>
<p>Different projects choose different testing tradeoffs based on how often components change, and how much logic they contain. If you haven’t decided on a testing strategy yet, we recommend that you start with creating simple smoke tests for your components:</p>
<div><pre>import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

it('renders without crashing', () =&gt; {
  const div = document.createElement('div');
  ReactDOM.render(&lt;App /&gt;, div);
});</pre></div>
<p>This test mounts a component and makes sure that it didn’t throw during rendering. Tests like this provide a lot of value with very little effort so they are great as a starting point, and this is the test you will find in <code>src/App.test.js</code>.</p>
<p>When you encounter bugs caused by changing components, you will gain a deeper insight into which parts of them are worth testing in your application. This might be a good time to introduce more specific tests asserting specific expected output or behavior.</p>
<p>If you’d like to test components in isolation from the child components they render, we recommend using <a href="http://airbnb.io/enzyme/docs/api/shallow.html" target="_blank"><code>shallow()</code> rendering API</a> from <a href="http://airbnb.io/enzyme/" target="_blank">Enzyme</a>. To install it, run:</p>
<div><pre>npm install --save enzyme enzyme-adapter-react-16 react-test-renderer</pre></div>
<p>Alternatively you may use <code>yarn</code>:</p>
<div><pre>yarn add enzyme enzyme-adapter-react-16 react-test-renderer</pre></div>
<p>As of Enzyme 3, you will need to install Enzyme along with an Adapter corresponding to the version of React you are using. (The examples above use the adapter for React 16.)</p>
<p>The adapter will also need to be configured in your <a href="#initializing-test-environment" target="_blank">global setup file</a>:</p>
<h4><code>src/setupTests.js</code></h4>
<div><pre>import { configure } from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

configure({ adapter: new Adapter() });</pre></div>
<blockquote>
<p>Note: Keep in mind that if you decide to "eject" before creating <code>src/setupTests.js</code>, the resulting <code>package.json</code> file won't contain any reference to it. <a href="#initializing-test-environment" target="_blank">Read here</a> to learn how to add this after ejecting.</p>
</blockquote>
<p>Now you can write a smoke test with it:</p>
<div><pre>import React from 'react';
import { shallow } from 'enzyme';
import App from './App';

it('renders without crashing', () =&gt; {
  shallow(&lt;App /&gt;);
});</pre></div>
<p>Unlike the previous smoke test using <code>ReactDOM.render()</code>, this test only renders <code>&lt;App&gt;</code> and doesn’t go deeper. For example, even if <code>&lt;App&gt;</code> itself renders a <code>&lt;Button&gt;</code> that throws, this test will pass. Shallow rendering is great for isolated unit tests, but you may still want to create some full rendering tests to ensure the components integrate correctly. Enzyme supports <a href="http://airbnb.io/enzyme/docs/api/mount.html" target="_blank">full rendering with <code>mount()</code></a>, and you can also use it for testing state changes and component lifecycle.</p>
<p>You can read the <a href="http://airbnb.io/enzyme/" target="_blank">Enzyme documentation</a> for more testing techniques. Enzyme documentation uses Chai and Sinon for assertions but you don’t have to use them because Jest provides built-in <code>expect()</code> and <code>jest.fn()</code> for spies.</p>
<p>Here is an example from Enzyme documentation that asserts specific output, rewritten to use Jest matchers:</p>
<div><pre>import React from 'react';
import { shallow } from 'enzyme';
import App from './App';

it('renders welcome message', () =&gt; {
  const wrapper = shallow(&lt;App /&gt;);
  const welcome = &lt;h2&gt;Welcome to React&lt;/h2&gt;;
  // expect(wrapper.contains(welcome)).to.equal(true);
  expect(wrapper.contains(welcome)).toEqual(true);
});</pre></div>
<p>All Jest matchers are <a href="http://facebook.github.io/jest/docs/en/expect.html" target="_blank">extensively documented here</a>.<br />
Nevertheless you can use a third-party assertion library like <a href="http://chaijs.com/" target="_blank">Chai</a> if you want to, as described below.</p>
<p>Additionally, you might find <a href="https://github.com/blainekasten/enzyme-matchers" target="_blank">jest-enzyme</a> helpful to simplify your tests with readable matchers. The above <code>contains</code> code can be written more simply with jest-enzyme.</p>
<div><pre>expect(wrapper).toContainReact(welcome)</pre></div>
<p>To enable this, install <code>jest-enzyme</code>:</p>
<div><pre>npm install --save jest-enzyme</pre></div>
<p>Alternatively you may use <code>yarn</code>:</p>
<div><pre>yarn add jest-enzyme</pre></div>
<p>Import it in <a href="#initializing-test-environment" target="_blank"><code>src/setupTests.js</code></a> to make its matchers available in every test:</p>
<div><pre>import 'jest-enzyme';</pre></div>
<h3>Using Third Party Assertion Libraries</h3>
<p>We recommend that you use <code>expect()</code> for assertions and <code>jest.fn()</code> for spies. If you are having issues with them please <a href="https://github.com/facebook/jest/issues/new" target="_blank">file those against Jest</a>, and we’ll fix them. We intend to keep making them better for React, supporting, for example, <a href="https://github.com/facebook/jest/pull/1566" target="_blank">pretty-printing React elements as JSX</a>.</p>
<p>However, if you are used to other libraries, such as <a href="http://chaijs.com/" target="_blank">Chai</a> and <a href="http://sinonjs.org/" target="_blank">Sinon</a>, or if you have existing code using them that you’d like to port over, you can import them normally like this:</p>
<div><pre>import sinon from 'sinon';
import { expect } from 'chai';</pre></div>
<p>and then use them in your tests like you normally do.</p>
<h3>Initializing Test Environment</h3>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@0.4.0</code> and higher.</p>
</blockquote>
<p>If your app uses a browser API that you need to mock in your tests or if you just need a global setup before running your tests, add a <code>src/setupTests.js</code> to your project. It will be automatically executed before running your tests.</p>
<p>For example:</p>
<h4><code>src/setupTests.js</code></h4>
<div><pre>const localStorageMock = {
  getItem: jest.fn(),
  setItem: jest.fn(),
  clear: jest.fn()
};
global.localStorage = localStorageMock</pre></div>
<blockquote>
<p>Note: Keep in mind that if you decide to "eject" before creating <code>src/setupTests.js</code>, the resulting <code>package.json</code> file won't contain any reference to it, so you should manually create the property <code>setupTestFrameworkScriptFile</code> in the configuration for Jest, something like the following:</p>
</blockquote>
<blockquote>
<div><pre>"jest": {
  // ...
  "setupTestFrameworkScriptFile": "&lt;rootDir&gt;/src/setupTests.js"
 }</pre></div>
</blockquote>
<h3>Focusing and Excluding Tests</h3>
<p>You can replace <code>it()</code> with <code>xit()</code> to temporarily exclude a test from being executed.<br />
Similarly, <code>fit()</code> lets you focus on a specific test without running any other tests.</p>
<h3>Coverage Reporting</h3>
<p>Jest has an integrated coverage reporter that works well with ES6 and requires no configuration.<br />
Run <code>npm test -- --coverage</code> (note extra <code>--</code> in the middle) to include a coverage report like this:</p>
<p><a href="https://camo.githubusercontent.com/bd0bbda8e44ea747e4c199d0e212d40563ad2fcb/687474703a2f2f692e696d6775722e636f6d2f356246686e54532e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/bd0bbda8e44ea747e4c199d0e212d40563ad2fcb/687474703a2f2f692e696d6775722e636f6d2f356246686e54532e706e67" alt="coverage report" /></div></a></p>
<p>Note that tests run much slower with coverage so it is recommended to run it separately from your normal workflow.</p>
<h4>Configuration</h4>
<p>The default Jest coverage configuration can be overriden by adding any of the following supported keys to a Jest config in your package.json.</p>
<p>Supported overrides:</p>

<p>Example package.json:</p>
<div><pre>{
  "name": "your-package",
  "jest": {
    "collectCoverageFrom" : [
      "src/**/*.{js,jsx}",
      "!&lt;rootDir&gt;/node_modules/",
      "!&lt;rootDir&gt;/path/to/dir/"
    ],
    "coverageThreshold": {
      "global": {
        "branches": 90,
        "functions": 90,
        "lines": 90,
        "statements": 90
      }
    },
    "coverageReporters": ["text"],
    "snapshotSerializers": ["my-serializer-module"]
  }
}</pre></div>
<h3>Continuous Integration</h3>
<p>By default <code>npm test</code> runs the watcher with interactive CLI. However, you can force it to run tests once and finish the process by setting an environment variable called <code>CI</code>.</p>
<p>When creating a build of your application with <code>npm run build</code> linter warnings are not checked by default. Like <code>npm test</code>, you can force the build to perform a linter warning check by setting the environment variable <code>CI</code>. If any warnings are encountered then the build fails.</p>
<p>Popular CI servers already set the environment variable <code>CI</code> by default but you can do this yourself too:</p>
<h3>On CI servers</h3>
<h4>Travis CI</h4>
<ol>
<li>Following the <a href="https://docs.travis-ci.com/user/getting-started/" target="_blank">Travis Getting started</a> guide for syncing your GitHub repository with Travis.  You may need to initialize some settings manually in your <a href="https://travis-ci.org/profile" target="_blank">profile</a> page.</li>
<li>Add a <code>.travis.yml</code> file to your git repository.</li>
</ol>
<pre><code>language: node_js
node_js:
  - 6
cache:
  directories:
    - node_modules
script:
  - npm run build
  - npm test
</code></pre>
<ol>
<li>Trigger your first build with a git push.</li>
<li><a href="https://docs.travis-ci.com/user/customizing-the-build/" target="_blank">Customize your Travis CI Build</a> if needed.</li>
</ol>
<h4>CircleCI</h4>
<p>Follow <a href="https://medium.com/@knowbody/circleci-and-zeits-now-sh-c9b7eebcd3c1" target="_blank">this article</a> to set up CircleCI with a Create React App project.</p>
<h3>On your own environment</h3>
<h5>Windows (cmd.exe)</h5>
<div><pre>set CI=true&&npm test</pre></div>
<div><pre>set CI=true&&npm run build</pre></div>
<p>(Note: the lack of whitespace is intentional.)</p>
<h5>Windows (Powershell)</h5>
<div><pre>($env:CI = $true) -and (npm test)</pre></div>
<div><pre>($env:CI = $true) -and (npm run build)</pre></div>
<h5>Linux, macOS (Bash)</h5>
<div><pre>CI=true npm test</pre></div>
<div><pre>CI=true npm run build</pre></div>
<p>The test command will force Jest to run tests once instead of launching the watcher.</p>
<blockquote>
<p>If you find yourself doing this often in development, please <a href="https://github.com/facebookincubator/create-react-app/issues/new" target="_blank">file an issue</a> to tell us about your use case because we want to make watcher the best experience and are open to changing how it works to accommodate more workflows.</p>
</blockquote>
<p>The build command will check for linter warnings and fail if any are found.</p>
<h3>Disabling jsdom</h3>
<p>By default, the <code>package.json</code> of the generated project looks like this:</p>
<div><pre>  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom"</pre></div>
<p>If you know that none of your tests depend on <a href="https://github.com/tmpvar/jsdom" target="_blank">jsdom</a>, you can safely remove <code>--env=jsdom</code>, and your tests will run faster:</p>
<div><pre>  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
-   "test": "react-scripts test --env=jsdom"
+   "test": "react-scripts test"</pre></div>
<p>To help you make up your mind, here is a list of APIs that <strong>need jsdom</strong>:</p>

<p>In contrast, <strong>jsdom is not needed</strong> for the following APIs:</p>

<p>Finally, jsdom is also not needed for <a href="http://facebook.github.io/jest/blog/2016/07/27/jest-14.html" target="_blank">snapshot testing</a>.</p>
<h3>Snapshot Testing</h3>
<p>Snapshot testing is a feature of Jest that automatically generates text snapshots of your components and saves them on the disk so if the UI output changes, you get notified without manually writing any assertions on the component output. <a href="http://facebook.github.io/jest/blog/2016/07/27/jest-14.html" target="_blank">Read more about snapshot testing.</a></p>
<h3>Editor Integration</h3>
<p>If you use <a href="https://code.visualstudio.com" target="_blank">Visual Studio Code</a>, there is a <a href="https://github.com/orta/vscode-jest" target="_blank">Jest extension</a> which works with Create React App out of the box. This provides a lot of IDE-like features while using a text editor: showing the status of a test run with potential fail messages inline, starting and stopping the watcher automatically, and offering one-click snapshot updates.</p>
<p><a href="https://cloud.githubusercontent.com/assets/49038/20795349/a032308a-b7c8-11e6-9b34-7eeac781003f.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/49038/20795349/a032308a-b7c8-11e6-9b34-7eeac781003f.png" alt="VS Code Jest Preview" /></div></a></p>
<h2>Debugging Tests</h2>
<p>There are various ways to setup a debugger for your Jest tests. We cover debugging in Chrome and <a href="https://code.visualstudio.com/" target="_blank">Visual Studio Code</a>.</p>
<blockquote>
<p>Note: debugging tests requires Node 8 or higher.</p>
</blockquote>
<h3>Debugging Tests in Chrome</h3>
<p>Add the following to the <code>scripts</code> section in your project's <code>package.json</code></p>
<div><pre>"scripts": {
    "test:debug": "react-scripts --inspect-brk test --runInBand --env=jsdom"
  }</pre></div>
<p>Place <code>debugger;</code> statements in any test and run:</p>
<div><pre>$ npm run test:debug</pre></div>
<p>This will start running your Jest tests, but pause before executing to allow a debugger to attach to the process.</p>
<p>Open the following in Chrome</p>
<pre><code>about:inspect
</code></pre>
<p>After opening that link, the Chrome Developer Tools will be displayed. Select <code>inspect</code> on your process and a breakpoint will be set at the first line of the react script (this is done simply to give you time to open the developer tools and to prevent Jest from executing before you have time to do so). Click the button that looks like a "play" button in the upper right hand side of the screen to continue execution. When Jest executes the test that contains the debugger statement, execution will pause and you can examine the current scope and call stack.</p>
<blockquote>
<p>Note: the --runInBand cli option makes sure Jest runs test in the same process rather than spawning processes for individual tests. Normally Jest parallelizes test runs across processes but it is hard to debug many processes at the same time.</p>
</blockquote>
<h3>Debugging Tests in Visual Studio Code</h3>
<p>Debugging Jest tests is supported out of the box for <a href="https://code.visualstudio.com" target="_blank">Visual Studio Code</a>.</p>
<p>Use the following <a href="https://code.visualstudio.com/docs/editor/debugging#_launch-configurations" target="_blank"><code>launch.json</code></a> configuration file:</p>
<pre><code>{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug CRA Tests",
      "type": "node",
      "request": "launch",
      "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/react-scripts",      
      "args": [
        "test",
        "--runInBand",
        "--no-cache",
        "--env=jsdom"
      ],
      "cwd": "${workspaceRoot}",
      "protocol": "inspector",
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen"
    }
  ]
}
</code></pre>
<h2>Developing Components in Isolation</h2>
<p>Usually, in an app, you have a lot of UI components, and each of them has many different states.
For an example, a simple button component could have following states:</p>
<ul>
<li>In a regular state, with a text label.</li>
<li>In the disabled mode.</li>
<li>In a loading state.</li>
</ul>
<p>Usually, it’s hard to see these states without running a sample app or some examples.</p>
<p>Create React App doesn’t include any tools for this by default, but you can easily add <a href="https://storybook.js.org" target="_blank">Storybook for React</a> (<a href="https://github.com/storybooks/storybook" target="_blank">source</a>) or <a href="https://react-styleguidist.js.org/" target="_blank">React Styleguidist</a> (<a href="https://github.com/styleguidist/react-styleguidist" target="_blank">source</a>) to your project. <strong>These are third-party tools that let you develop components and see all their states in isolation from your app</strong>.</p>
<p><a href="https://camo.githubusercontent.com/afa6a5df98c90ddb6b23b0fe6fba6b75c96f42b7/687474703a2f2f692e696d6775722e636f6d2f374349415770422e676966" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/afa6a5df98c90ddb6b23b0fe6fba6b75c96f42b7/687474703a2f2f692e696d6775722e636f6d2f374349415770422e676966" alt="Storybook for React Demo" /></div></a></p>
<p>You can also deploy your Storybook or style guide as a static app. This way, everyone in your team can view and review different states of UI components without starting a backend server or creating an account in your app.</p>
<h3>Getting Started with Storybook</h3>
<p>Storybook is a development environment for React UI components. It allows you to browse a component library, view the different states of each component, and interactively develop and test components.</p>
<p>First, install the following npm package globally:</p>
<div><pre>npm install -g @storybook/cli</pre></div>
<p>Then, run the following command inside your app’s directory:</p>
<div><pre>getstorybook</pre></div>
<p>After that, follow the instructions on the screen.</p>
<p>Learn more about React Storybook:</p>

<h3>Getting Started with Styleguidist</h3>
<p>Styleguidist combines a style guide, where all your components are presented on a single page with their props documentation and usage examples, with an environment for developing components in isolation, similar to Storybook. In Styleguidist you write examples in Markdown, where each code snippet is rendered as a live editable playground.</p>
<p>First, install Styleguidist:</p>
<div><pre>npm install --save react-styleguidist</pre></div>
<p>Alternatively you may use <code>yarn</code>:</p>
<div><pre>yarn add react-styleguidist</pre></div>
<p>Then, add these scripts to your <code>package.json</code>:</p>
<div><pre>   "scripts": {
+    "styleguide": "styleguidist server",
+    "styleguide:build": "styleguidist build",
     "start": "react-scripts start",</pre></div>
<p>Then, run the following command inside your app’s directory:</p>
<div><pre>npm run styleguide</pre></div>
<p>After that, follow the instructions on the screen.</p>
<p>Learn more about React Styleguidist:</p>

<h2>Publishing Components to npm</h2>
<p>Create React App doesn't provide any built-in functionality to publish a component to npm. If you're ready to extract a component from your project so other people can use it, we recommend moving it to a separate directory outside of your project and then using a tool like <a href="https://github.com/insin/nwb#react-components-and-libraries" target="_blank">nwb</a> to prepare it for publishing.</p>
<h2>Making a Progressive Web App</h2>
<p>By default, the production build is a fully functional, offline-first
<a href="https://developers.google.com/web/progressive-web-apps/" target="_blank">Progressive Web App</a>.</p>
<p>Progressive Web Apps are faster and more reliable than traditional web pages, and provide an engaging mobile experience:</p>
<ul>
<li>All static site assets are cached so that your page loads fast on subsequent visits, regardless of network connectivity (such as 2G or 3G). Updates are downloaded in the background.</li>
<li>Your app will work regardless of network state, even if offline. This means your users will be able to use your app at 10,000 feet and on the subway.</li>
<li>On mobile devices, your app can be added directly to the user's home screen, app icon and all. You can also re-engage users using web <strong>push notifications</strong>. This eliminates the need for the app store.</li>
</ul>
<p>The <a href="https://github.com/goldhand/sw-precache-webpack-plugin" target="_blank"><code>sw-precache-webpack-plugin</code></a>
is integrated into production configuration,
and it will take care of generating a service worker file that will automatically
precache all of your local assets and keep them up to date as you deploy updates.
The service worker will use a <a href="https://developers.google.com/web/fundamentals/instant-and-offline/offline-cookbook/#cache-falling-back-to-network" target="_blank">cache-first strategy</a>
for handling all requests for local assets, including the initial HTML, ensuring
that your web app is reliably fast, even on a slow or unreliable network.</p>
<h3>Opting Out of Caching</h3>
<p>If you would prefer not to enable service workers prior to your initial
production deployment, then remove the call to <code>registerServiceWorker()</code>
from <a href="/facebook/create-react-app/blob/master/packages/react-scripts/template/src/index.js" target="_blank"><code>src/index.js</code></a>.</p>
<p>If you had previously enabled service workers in your production deployment and
have decided that you would like to disable them for all your existing users,
you can swap out the call to <code>registerServiceWorker()</code> in
<a href="/facebook/create-react-app/blob/master/packages/react-scripts/template/src/index.js" target="_blank"><code>src/index.js</code></a> first by modifying the service worker import:</p>
<div><pre>import { unregister } from './registerServiceWorker';</pre></div>
<p>and then call <code>unregister()</code> instead.
After the user visits a page that has <code>unregister()</code>,
the service worker will be uninstalled. Note that depending on how <code>/service-worker.js</code> is served,
it may take up to 24 hours for the cache to be invalidated.</p>
<h3>Offline-First Considerations</h3>
<ol>
<li>
<p>Service workers <a href="https://developers.google.com/web/fundamentals/getting-started/primers/service-workers#you_need_https" target="_blank">require HTTPS</a>,
although to facilitate local testing, that policy
<a href="http://stackoverflow.com/questions/34160509/options-for-testing-service-workers-via-http/34161385#34161385" target="_blank">does not apply to <code>localhost</code></a>.
If your production web server does not support HTTPS, then the service worker
registration will fail, but the rest of your web app will remain functional.</p>
</li>
<li>
<p>Service workers are <a href="https://jakearchibald.github.io/isserviceworkerready/" target="_blank">not currently supported</a>
in all web browsers. Service worker registration <a href="/facebook/create-react-app/blob/master/packages/react-scripts/template/src/registerServiceWorker.js" target="_blank">won't be attempted</a>
on browsers that lack support.</p>
</li>
<li>
<p>The service worker is only enabled in the <a href="#deployment" target="_blank">production environment</a>,
e.g. the output of <code>npm run build</code>. It's recommended that you do not enable an
offline-first service worker in a development environment, as it can lead to
frustration when previously cached assets are used and do not include the latest
changes you've made locally.</p>
</li>
<li>
<p>If you <em>need</em> to test your offline-first service worker locally, build
the application (using <code>npm run build</code>) and run a simple http server from your
build directory. After running the build script, <code>create-react-app</code> will give
instructions for one way to test your production build locally and the <a href="#deployment" target="_blank">deployment instructions</a> have
instructions for using other methods. <em>Be sure to always use an
incognito window to avoid complications with your browser cache.</em></p>
</li>
<li>
<p>If possible, configure your production environment to serve the generated
<code>service-worker.js</code> <a href="http://stackoverflow.com/questions/38843970/service-worker-javascript-update-frequency-every-24-hours" target="_blank">with HTTP caching disabled</a>.
If that's not possible—<a href="#github-pages" target="_blank">GitHub Pages</a>, for instance, does not
allow you to change the default 10 minute HTTP cache lifetime—then be aware
that if you visit your production site, and then revisit again before
<code>service-worker.js</code> has expired from your HTTP cache, you'll continue to get
the previously cached assets from the service worker. If you have an immediate
need to view your updated production deployment, performing a shift-refresh
will temporarily disable the service worker and retrieve all assets from the
network.</p>
</li>
<li>
<p>Users aren't always familiar with offline-first web apps. It can be useful to
<a href="https://developers.google.com/web/fundamentals/instant-and-offline/offline-ux#inform_the_user_when_the_app_is_ready_for_offline_consumption" target="_blank">let the user know</a>
when the service worker has finished populating your caches (showing a "This web
app works offline!" message) and also let them know when the service worker has
fetched the latest updates that will be available the next time they load the
page (showing a "New content is available; please refresh." message). Showing
this messages is currently left as an exercise to the developer, but as a
starting point, you can make use of the logic included in <a href="/facebook/create-react-app/blob/master/packages/react-scripts/template/src/registerServiceWorker.js" target="_blank"><code>src/registerServiceWorker.js</code></a>, which
demonstrates which service worker lifecycle events to listen for to detect each
scenario, and which as a default, just logs appropriate messages to the
JavaScript console.</p>
</li>
<li>
<p>By default, the generated service worker file will not intercept or cache any
cross-origin traffic, like HTTP <a href="#integrating-with-an-api-backend" target="_blank">API requests</a>,
images, or embeds loaded from a different domain. If you would like to use a
runtime caching strategy for those requests, you can <a href="#npm-run-eject" target="_blank"><code>eject</code></a>
and then configure the
<a href="https://github.com/GoogleChrome/sw-precache#runtimecaching-arrayobject" target="_blank"><code>runtimeCaching</code></a>
option in the <code>SWPrecacheWebpackPlugin</code> section of
<a href="/facebook/create-react-app/blob/master/packages/react-scripts/config/webpack.config.prod.js" target="_blank"><code>webpack.config.prod.js</code></a>.</p>
</li>
</ol>
<h3>Progressive Web App Metadata</h3>
<p>The default configuration includes a web app manifest located at
<a href="/facebook/create-react-app/blob/master/packages/react-scripts/template/public/manifest.json" target="_blank"><code>public/manifest.json</code></a>, that you can customize with
details specific to your web application.</p>
<p>When a user adds a web app to their homescreen using Chrome or Firefox on
Android, the metadata in <a href="/facebook/create-react-app/blob/master/packages/react-scripts/template/public/manifest.json" target="_blank"><code>manifest.json</code></a> determines what
icons, names, and branding colors to use when the web app is displayed.
<a href="https://developers.google.com/web/fundamentals/engage-and-retain/web-app-manifest/" target="_blank">The Web App Manifest guide</a>
provides more context about what each field means, and how your customizations
will affect your users' experience.</p>
<h2>Analyzing the Bundle Size</h2>
<p><a href="https://www.npmjs.com/package/source-map-explorer" target="_blank">Source map explorer</a> analyzes
JavaScript bundles using the source maps. This helps you understand where code
bloat is coming from.</p>
<p>To add Source map explorer to a Create React App project, follow these steps:</p>
<div><pre>npm install --save source-map-explorer</pre></div>
<p>Alternatively you may use <code>yarn</code>:</p>
<div><pre>yarn add source-map-explorer</pre></div>
<p>Then in <code>package.json</code>, add the following line to <code>scripts</code>:</p>
<div><pre>   "scripts": {
+    "analyze": "source-map-explorer build/static/js/main.*",
     "start": "react-scripts start",
     "build": "react-scripts build",
     "test": "react-scripts test --env=jsdom",</pre></div>
<p>Then to analyze the bundle run the production build then run the analyze
script.</p>
<pre><code>npm run build
npm run analyze
</code></pre>
<h2>Deployment</h2>
<p><code>npm run build</code> creates a <code>build</code> directory with a production build of your app. Set up your favorite HTTP server so that a visitor to your site is served <code>index.html</code>, and requests to static paths like <code>/static/js/main.&lt;hash&gt;.js</code> are served with the contents of the <code>/static/js/main.&lt;hash&gt;.js</code> file.</p>
<h3>Static Server</h3>
<p>For environments using <a href="https://nodejs.org/" target="_blank">Node</a>, the easiest way to handle this would be to install <a href="https://github.com/zeit/serve" target="_blank">serve</a> and let it handle the rest:</p>
<div><pre>npm install -g serve
serve -s build</pre></div>
<p>The last command shown above will serve your static site on the port <strong>5000</strong>. Like many of <a href="https://github.com/zeit/serve" target="_blank">serve</a>’s internal settings, the port can be adjusted using the <code>-p</code> or <code>--port</code> flags.</p>
<p>Run this command to get a full list of the options available:</p>
<div><pre>serve -h</pre></div>
<h3>Other Solutions</h3>
<p>You don’t necessarily need a static server in order to run a Create React App project in production. It works just as fine integrated into an existing dynamic one.</p>
<p>Here’s a programmatic example using <a href="https://nodejs.org/" target="_blank">Node</a> and <a href="http://expressjs.com/" target="_blank">Express</a>:</p>
<div><pre>const express = require('express');
const path = require('path');
const app = express();

app.use(express.static(path.join(__dirname, 'build')));

app.get('/', function (req, res) {
  res.sendFile(path.join(__dirname, 'build', 'index.html'));
});

app.listen(9000);</pre></div>
<p>The choice of your server software isn’t important either. Since Create React App is completely platform-agnostic, there’s no need to explicitly use Node.</p>
<p>The <code>build</code> folder with static assets is the only output produced by Create React App.</p>
<p>However this is not quite enough if you use client-side routing. Read the next section if you want to support URLs like <code>/todos/42</code> in your single-page app.</p>
<h3>Serving Apps with Client-Side Routing</h3>
<p>If you use routers that use the HTML5 <a href="https://developer.mozilla.org/en-US/docs/Web/API/History_API#Adding_and_modifying_history_entries" target="_blank"><code>pushState</code> history API</a> under the hood (for example, <a href="https://github.com/ReactTraining/react-router" target="_blank">React Router</a> with <code>browserHistory</code>), many static file servers will fail. For example, if you used React Router with a route for <code>/todos/42</code>, the development server will respond to <code>localhost:3000/todos/42</code> properly, but an Express serving a production build as above will not.</p>
<p>This is because when there is a fresh page load for a <code>/todos/42</code>, the server looks for the file <code>build/todos/42</code> and does not find it. The server needs to be configured to respond to a request to <code>/todos/42</code> by serving <code>index.html</code>. For example, we can amend our Express example above to serve <code>index.html</code> for any unknown paths:</p>
<div><pre> app.use(express.static(path.join(__dirname, 'build')));

-app.get('/', function (req, res) {
+app.get('/*', function (req, res) {
   res.sendFile(path.join(__dirname, 'build', 'index.html'));
 });</pre></div>
<p>If you’re using <a href="https://httpd.apache.org/" target="_blank">Apache HTTP Server</a>, you need to create a <code>.htaccess</code> file in the <code>public</code> folder that looks like this:</p>
<pre><code>    Options -MultiViews
    RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.html [QSA,L]
</code></pre>
<p>It will get copied to the <code>build</code> folder when you run <code>npm run build</code>.</p>
<p>If you’re using <a href="http://tomcat.apache.org/" target="_blank">Apache Tomcat</a>, you need to follow <a href="https://stackoverflow.com/a/41249464/4878474" target="_blank">this Stack Overflow answer</a>.</p>
<p>Now requests to <code>/todos/42</code> will be handled correctly both in development and in production.</p>
<p>On a production build, and in a browser that supports <a href="https://developers.google.com/web/fundamentals/getting-started/primers/service-workers" target="_blank">service workers</a>,
the service worker will automatically handle all navigation requests, like for
<code>/todos/42</code>, by serving the cached copy of your <code>index.html</code>. This
service worker navigation routing can be configured or disabled by
<a href="#npm-run-eject" target="_blank"><code>eject</code>ing</a> and then modifying the
<a href="https://github.com/GoogleChrome/sw-precache#navigatefallback-string" target="_blank"><code>navigateFallback</code></a>
and <a href="https://github.com/GoogleChrome/sw-precache#navigatefallbackwhitelist-arrayregexp" target="_blank"><code>navigateFallbackWhitelist</code></a>
options of the <code>SWPreachePlugin</code> <a href="/facebook/create-react-app/blob/master/packages/react-scripts/config/webpack.config.prod.js" target="_blank">configuration</a>.</p>
<p>When users install your app to the homescreen of their device the default configuration will make a shortcut to <code>/index.html</code>. This may not work for client-side routers which expect the app to be served from <code>/</code>. Edit the web app manifest at <a href="/facebook/create-react-app/blob/master/packages/react-scripts/template/public/manifest.json" target="_blank"><code>public/manifest.json</code></a> and change <code>start_url</code> to match the required URL scheme, for example:</p>
<div><pre>  "start_url": ".",</pre></div>
<h3>Building for Relative Paths</h3>
<p>By default, Create React App produces a build assuming your app is hosted at the server root.<br />
To override this, specify the <code>homepage</code> in your <code>package.json</code>, for example:</p>
<div><pre>  "homepage": "http://mywebsite.com/relativepath",</pre></div>
<p>This will let Create React App correctly infer the root path to use in the generated HTML file.</p>
<p><strong>Note</strong>: If you are using <code>react-router@^4</code>, you can root <code>&lt;Link&gt;</code>s using the <code>basename</code> prop on any <code>&lt;Router&gt;</code>.<br />
More information <a href="https://reacttraining.com/react-router/web/api/BrowserRouter/basename-string" target="_blank">here</a>.<br /><br />For example:</p>
<div><pre>&lt;BrowserRouter basename="/calendar"/&gt;
&lt;Link to="/today"/&gt; // renders &lt;a href="/calendar/today"&gt;</pre></div>
<h4>Serving the Same Build from Different Paths</h4>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@0.9.0</code> and higher.</p>
</blockquote>
<p>If you are not using the HTML5 <code>pushState</code> history API or not using client-side routing at all, it is unnecessary to specify the URL from which your app will be served. Instead, you can put this in your <code>package.json</code>:</p>
<div><pre>  "homepage": ".",</pre></div>
<p>This will make sure that all the asset paths are relative to <code>index.html</code>. You will then be able to move your app from <code>http://mywebsite.com</code> to <code>http://mywebsite.com/relativepath</code> or even <code>http://mywebsite.com/relative/path</code> without having to rebuild it.</p>
<h3><a href="https://azure.microsoft.com/" target="_blank">Azure</a></h3>
<p>See <a href="https://medium.com/@to_pe/deploying-create-react-app-on-microsoft-azure-c0f6686a4321" target="_blank">this</a> blog post on how to deploy your React app to Microsoft Azure.</p>
<p>See <a href="https://medium.com/@strid/host-create-react-app-on-azure-986bc40d5bf2#.pycfnafbg" target="_blank">this</a> blog post or <a href="https://github.com/ulrikaugustsson/azure-appservice-static" target="_blank">this</a> repo for a way to use automatic deployment to Azure App Service.</p>
<h3><a href="https://firebase.google.com/" target="_blank">Firebase</a></h3>
<p>Install the Firebase CLI if you haven’t already by running <code>npm install -g firebase-tools</code>. Sign up for a <a href="https://console.firebase.google.com/" target="_blank">Firebase account</a> and create a new project. Run <code>firebase login</code> and login with your previous created Firebase account.</p>
<p>Then run the <code>firebase init</code> command from your project’s root. You need to choose the <strong>Hosting: Configure and deploy Firebase Hosting sites</strong> and choose the Firebase project you created in the previous step. You will need to agree with <code>database.rules.json</code> being created, choose <code>build</code> as the public directory, and also agree to <strong>Configure as a single-page app</strong> by replying with <code>y</code>.</p>
<div><pre>    === Project Setup

    First, let's associate this project directory with a Firebase project.
    You can create multiple project aliases by running firebase use --add,
    but for now we'll just set up a default project.

    ? What Firebase project do you want to associate as default? Example app (example-app-fd690)

    === Database Setup

    Firebase Realtime Database Rules allow you to define how your data should be
    structured and when your data can be read from and written to.

    ? What file should be used for Database Rules? database.rules.json
    ✔  Database Rules for example-app-fd690 have been downloaded to database.rules.json.
    Future modifications to database.rules.json will update Database Rules when you run
    firebase deploy.

    === Hosting Setup

    Your public directory is the folder (relative to your project directory) that
    will contain Hosting assets to uploaded with firebase deploy. If you
    have a build process for your assets, use your build's output directory.

    ? What do you want to use as your public directory? build
    ? Configure as a single-page app (rewrite all urls to /index.html)? Yes
    ✔  Wrote build/index.html

    i  Writing configuration info to firebase.json...
    i  Writing project information to .firebaserc...

    ✔  Firebase initialization complete!</pre></div>
<p>IMPORTANT: you need to set proper HTTP caching headers for <code>service-worker.js</code> file in <code>firebase.json</code> file or you will not be able to see changes after first deployment (<a href="https://github.com/facebookincubator/create-react-app/issues/2440" target="_blank">issue #2440</a>). It should be added inside <code>"hosting"</code> key like next:</p>
<pre><code>{
  "hosting": {
    ...
    "headers": [
      {"source": "/service-worker.js", "headers": [{"key": "Cache-Control", "value": "no-cache"}]}
    ]
    ...
</code></pre>
<p>Now, after you create a production build with <code>npm run build</code>, you can deploy it by running <code>firebase deploy</code>.</p>
<div><pre>    === Deploying to 'example-app-fd690'...

    i  deploying database, hosting
    ✔  database: rules ready to deploy.
    i  hosting: preparing build directory for upload...
    Uploading: [==============================          ] 75%✔  hosting: build folder uploaded successfully
    ✔  hosting: 8 files uploaded successfully
    i  starting release process (may take several minutes)...

    ✔  Deploy complete!

    Project Console: https://console.firebase.google.com/project/example-app-fd690/overview
    Hosting URL: https://example-app-fd690.firebaseapp.com</pre></div>
<p>For more information see <a href="https://firebase.google.com/docs/web/setup" target="_blank">Add Firebase to your JavaScript Project</a>.</p>
<h3><a href="https://pages.github.com/" target="_blank">GitHub Pages</a></h3>
<blockquote>
<p>Note: this feature is available with <code>react-scripts@0.2.0</code> and higher.</p>
</blockquote>
<h4>Step 1: Add <code>homepage</code> to <code>package.json</code></h4>
<p><strong>The step below is important!</strong><br />
<strong>If you skip it, your app will not deploy correctly.</strong></p>
<p>Open your <code>package.json</code> and add a <code>homepage</code> field for your project:</p>
<div><pre>  "homepage": "https://myusername.github.io/my-app",</pre></div>
<p>or for a GitHub user page:</p>
<div><pre>  "homepage": "https://myusername.github.io",</pre></div>
<p>Create React App uses the <code>homepage</code> field to determine the root URL in the built HTML file.</p>
<h4>Step 2: Install <code>gh-pages</code> and add <code>deploy</code> to <code>scripts</code> in <code>package.json</code></h4>
<p>Now, whenever you run <code>npm run build</code>, you will see a cheat sheet with instructions on how to deploy to GitHub Pages.</p>
<p>To publish it at <a href="https://myusername.github.io/my-app" target="_blank">https://myusername.github.io/my-app</a>, run:</p>
<div><pre>npm install --save gh-pages</pre></div>
<p>Alternatively you may use <code>yarn</code>:</p>
<div><pre>yarn add gh-pages</pre></div>
<p>Add the following scripts in your <code>package.json</code>:</p>
<div><pre>  "scripts": {
+   "predeploy": "npm run build",
+   "deploy": "gh-pages -d build",
    "start": "react-scripts start",
    "build": "react-scripts build",</pre></div>
<p>The <code>predeploy</code> script will run automatically before <code>deploy</code> is run.</p>
<p>If you are deploying to a GitHub user page instead of a project page you'll need to make two
additional modifications:</p>
<ol>
<li>First, change your repository's source branch to be any branch other than <strong>master</strong>.</li>
<li>Additionally, tweak your <code>package.json</code> scripts to push deployments to <strong>master</strong>:</li>
</ol>
<div><pre>  "scripts": {
    "predeploy": "npm run build",
-   "deploy": "gh-pages -d build",
+   "deploy": "gh-pages -b master -d build",</pre></div>
<h4>Step 3: Deploy the site by running <code>npm run deploy</code></h4>
<p>Then run:</p>
<div><pre>npm run deploy</pre></div>
<h4>Step 4: Ensure your project’s settings use <code>gh-pages</code></h4>
<p>Finally, make sure <strong>GitHub Pages</strong> option in your GitHub project settings is set to use the <code>gh-pages</code> branch:</p>
<p><a href="https://camo.githubusercontent.com/22aef6d3f95d8cfe08317f11b161eb9e8c1a6a65/687474703a2f2f692e696d6775722e636f6d2f48556a4572396c2e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/22aef6d3f95d8cfe08317f11b161eb9e8c1a6a65/687474703a2f2f692e696d6775722e636f6d2f48556a4572396c2e706e67"  alt="gh-pages branch setting" /></div></a></p>
<h4>Step 5: Optionally, configure the domain</h4>
<p>You can configure a custom domain with GitHub Pages by adding a <code>CNAME</code> file to the <code>public/</code> folder.</p>
<h4>Notes on client-side routing</h4>
<p>GitHub Pages doesn’t support routers that use the HTML5 <code>pushState</code> history API under the hood (for example, React Router using <code>browserHistory</code>). This is because when there is a fresh page load for a url like <code>http://user.github.io/todomvc/todos/42</code>, where <code>/todos/42</code> is a frontend route, the GitHub Pages server returns 404 because it knows nothing of <code>/todos/42</code>. If you want to add a router to a project hosted on GitHub Pages, here are a couple of solutions:</p>
<ul>
<li>You could switch from using HTML5 history API to routing with hashes. If you use React Router, you can switch to <code>hashHistory</code> for this effect, but the URL will be longer and more verbose (for example, <code>http://user.github.io/todomvc/#/todos/42?_k=yknaj</code>). <a href="https://reacttraining.com/react-router/web/api/Router" target="_blank">Read more</a> about different history implementations in React Router.</li>
<li>Alternatively, you can use a trick to teach GitHub Pages to handle 404 by redirecting to your <code>index.html</code> page with a special redirect parameter. You would need to add a <code>404.html</code> file with the redirection code to the <code>build</code> folder before deploying your project, and you’ll need to add code handling the redirect parameter to <code>index.html</code>. You can find a detailed explanation of this technique <a href="https://github.com/rafrex/spa-github-pages" target="_blank">in this guide</a><img src="chrome-extension://pgmpdhecmoecoihpehfeghpcphaeenkp/images/star-white.svg" />1,412.</li>
</ul>
<h4>Troubleshooting</h4>
<h5>"/dev/tty: No such a device or address"</h5>
<p>If, when deploying, you get <code>/dev/tty: No such a device or address</code> or a similar error, try the follwing:</p>
<ol>

<li><code>git remote set-url origin https://&lt;user&gt;:&lt;token&gt;@github.com/&lt;user&gt;/&lt;repo&gt;</code> .</li>
<li>Try <code>npm run deploy again</code></li>
</ol>
<h3><a href="https://www.heroku.com/" target="_blank">Heroku</a></h3>
<p>Use the <a href="https://github.com/mars/create-react-app-buildpack" target="_blank">Heroku Buildpack for Create React App</a>.<br />
You can find instructions in <a href="https://blog.heroku.com/deploying-react-with-zero-configuration" target="_blank">Deploying React with Zero Configuration</a>.</p>
<h4>Resolving Heroku Deployment Errors</h4>
<p>Sometimes <code>npm run build</code> works locally but fails during deploy via Heroku. Following are the most common cases.</p>
<h5>"Module not found: Error: Cannot resolve 'file' or 'directory'"</h5>
<p>If you get something like this:</p>
<pre><code>remote: Failed to create a production build. Reason:
remote: Module not found: Error: Cannot resolve 'file' or 'directory'
MyDirectory in /tmp/build_1234/src
</code></pre>
<p>It means you need to ensure that the lettercase of the file or directory you <code>import</code> matches the one you see on your filesystem or on GitHub.</p>
<p>This is important because Linux (the operating system used by Heroku) is case sensitive. So <code>MyDirectory</code> and <code>mydirectory</code> are two distinct directories and thus, even though the project builds locally, the difference in case breaks the <code>import</code> statements on Heroku remotes.</p>
<h5>"Could not find a required file."</h5>
<p>If you exclude or ignore necessary files from the package you will see a error similar this one:</p>
<pre><code>remote: Could not find a required file.
remote:   Name: `index.html`
remote:   Searched in: /tmp/build_a2875fc163b209225122d68916f1d4df/public
remote:
remote: npm ERR! Linux 3.13.0-105-generic
remote: npm ERR! argv "/tmp/build_a2875fc163b209225122d68916f1d4df/.heroku/node/bin/node" "/tmp/build_a2875fc163b209225122d68916f1d4df/.heroku/node/bin/npm" "run" "build"
</code></pre>
<p>In this case, ensure that the file is there with the proper lettercase and that’s not ignored on your local <code>.gitignore</code> or <code>~/.gitignore_global</code>.</p>
<h3><a href="https://www.netlify.com/" target="_blank">Netlify</a></h3>
<p><strong>To do a manual deploy to Netlify’s CDN:</strong></p>
<div><pre>npm install netlify-cli -g
netlify deploy</pre></div>
<p>Choose <code>build</code> as the path to deploy.</p>
<p><strong>To setup continuous delivery:</strong></p>
<p>With this setup Netlify will build and deploy when you push to git or open a pull request:</p>
<ol>
<li><a href="https://app.netlify.com/signup" target="_blank">Start a new netlify project</a></li>
<li>Pick your Git hosting service and select your repository</li>
<li>Set <code>yarn build</code> as the build command and <code>build</code> as the publish directory</li>
<li>Click <code>Deploy site</code></li>
</ol>
<p><strong>Support for client-side routing:</strong></p>
<p>To support <code>pushState</code>, make sure to create a <code>public/_redirects</code> file with the following rewrite rules:</p>
<pre><code>/*  /index.html  200
</code></pre>
<p>When you build the project, Create React App will place the <code>public</code> folder contents into the build output.</p>
<h3><a href="https://zeit.co/now" target="_blank">Now</a></h3>
<p>Now offers a zero-configuration single-command deployment. You can use <code>now</code> to deploy your app for free.</p>
<ol>
<li>
<p>Install the <code>now</code> command-line tool either via the recommended <a href="https://zeit.co/download" target="_blank">desktop tool</a> or via node with <code>npm install -g now</code>.</p>
</li>
<li>
<p>Build your app by running <code>npm run build</code>.</p>
</li>
<li>
<p>Move into the build directory by running <code>cd build</code>.</p>
</li>
<li>
<p>Run <code>now --name your-project-name</code> from within the build directory. You will see a <strong>now.sh</strong> URL in your output like this:</p>
<pre><code>&gt; Ready! https://your-project-name-tpspyhtdtk.now.sh (copied to clipboard)
</code></pre>
<p>Paste that URL into your browser when the build is complete, and you will see your deployed app.</p>
</li>
</ol>
<p>Details are available in <a href="https://zeit.co/blog/unlimited-static" target="_blank">this article.</a></p>
<h3><a href="https://aws.amazon.com/s3" target="_blank">S3</a> and <a href="https://aws.amazon.com/cloudfront/" target="_blank">CloudFront</a></h3>
<p>See this <a href="https://medium.com/@omgwtfmarc/deploying-create-react-app-to-s3-or-cloudfront-48dae4ce0af" target="_blank">blog post</a> on how to deploy your React app to Amazon Web Services S3 and CloudFront.</p>
<h3><a href="https://surge.sh/" target="_blank">Surge</a></h3>
<p>Install the Surge CLI if you haven’t already by running <code>npm install -g surge</code>. Run the <code>surge</code> command and log in you or create a new account.</p>
<p>When asked about the project path, make sure to specify the <code>build</code> folder, for example:</p>
<div><pre>       project path: /path/to/project/build</pre></div>
<p>Note that in order to support routers that use HTML5 <code>pushState</code> API, you may want to rename the <code>index.html</code> in your build folder to <code>200.html</code> before deploying to Surge. This <a href="https://surge.sh/help/adding-a-200-page-for-client-side-routing" target="_blank">ensures that every URL falls back to that file</a>.</p>
<h2>Advanced Configuration</h2>
<p>You can adjust various development and production settings by setting environment variables in your shell or with <a href="#adding-development-environment-variables-in-env" target="_blank">.env</a>.</p>
<table>
<thead>
<tr>
<th>Variable</th>
<th>Development</th>
<th>Production</th>
<th>Usage</th>
</tr>
</thead>
<tbody>
<tr>
<td>BROWSER</td>
<td><g-emoji>✅</g-emoji></td>
<td><g-emoji>❌</g-emoji></td>
<td>By default, Create React App will open the default system browser, favoring Chrome on macOS. Specify a <a href="https://github.com/sindresorhus/opn#app" target="_blank">browser</a> to override this behavior, or set it to <code>none</code> to disable it completely. If you need to customize the way the browser is launched, you can specify a node script instead. Any arguments passed to <code>npm start</code> will also be passed to this script, and the url where your app is served will be the last argument. Your script's file name must have the <code>.js</code> extension.</td>
</tr>
<tr>
<td>HOST</td>
<td><g-emoji>✅</g-emoji></td>
<td><g-emoji>❌</g-emoji></td>
<td>By default, the development web server binds to <code>localhost</code>. You may use this variable to specify a different host.</td>
</tr>
<tr>
<td>PORT</td>
<td><g-emoji>✅</g-emoji></td>
<td><g-emoji>❌</g-emoji></td>
<td>By default, the development web server will attempt to listen on port 3000 or prompt you to attempt the next available port. You may use this variable to specify a different port.</td>
</tr>
<tr>
<td>HTTPS</td>
<td><g-emoji>✅</g-emoji></td>
<td><g-emoji>❌</g-emoji></td>
<td>When set to <code>true</code>, Create React App will run the development server in <code>https</code> mode.</td>
</tr>
<tr>
<td>PUBLIC_URL</td>
<td><g-emoji>❌</g-emoji></td>
<td><g-emoji>✅</g-emoji></td>
<td>Create React App assumes your application is hosted at the serving web server's root or a subpath as specified in <a href="#building-for-relative-paths" target="_blank"><code>package.json</code> (<code>homepage</code>)</a>. Normally, Create React App ignores the hostname. You may use this variable to force assets to be referenced verbatim to the url you provide (hostname included). This may be particularly useful when using a CDN to host your application.</td>
</tr>
<tr>
<td>CI</td>
<td><g-emoji>🔶</g-emoji></td>
<td><g-emoji>✅</g-emoji></td>
<td>When set to <code>true</code>, Create React App treats warnings as failures in the build. It also makes the test runner non-watching. Most CIs set this flag by default.</td>
</tr>
<tr>
<td>REACT_EDITOR</td>
<td><g-emoji>✅</g-emoji></td>
<td><g-emoji>❌</g-emoji></td>
<td>When an app crashes in development, you will see an error overlay with clickable stack trace. When you click on it, Create React App will try to determine the editor you are using based on currently running processes, and open the relevant source file. You can <a href="https://github.com/facebookincubator/create-react-app/issues/2636" target="_blank">send a pull request to detect your editor of choice</a>. Setting this environment variable overrides the automatic detection. If you do it, make sure your systems <a href="https://en.wikipedia.org/wiki/PATH_(variable)" target="_blank">PATH</a> environment variable points to your editor’s bin folder. You can also set it to <code>none</code> to disable it completely.</td>
</tr>
<tr>
<td>CHOKIDAR_USEPOLLING</td>
<td><g-emoji>✅</g-emoji></td>
<td><g-emoji>❌</g-emoji></td>
<td>When set to <code>true</code>, the watcher runs in polling mode, as necessary inside a VM. Use this option if <code>npm start</code> isn't detecting changes.</td>
</tr>
<tr>
<td>GENERATE_SOURCEMAP</td>
<td><g-emoji>❌</g-emoji></td>
<td><g-emoji>✅</g-emoji></td>
<td>When set to <code>false</code>, source maps are not generated for a production build. This solves OOM issues on some smaller machines.</td>
</tr>
<tr>
<td>NODE_PATH</td>
<td><g-emoji>✅</g-emoji></td>
<td><g-emoji>✅</g-emoji></td>
<td>Same as <a href="https://nodejs.org/api/modules.html#modules_loading_from_the_global_folders" target="_blank"><code>NODE_PATH</code> in Node.js</a>, but only relative folders are allowed. Can be handy for emulating a monorepo setup by setting <code>NODE_PATH=src</code>.</td>
</tr></tbody></table>
<h2>Troubleshooting</h2>
<h3><code>npm start</code> doesn’t detect changes</h3>
<p>When you save a file while <code>npm start</code> is running, the browser should refresh with the updated code.<br />
If this doesn’t happen, try one of the following workarounds:</p>
<ul>
<li>If your project is in a Dropbox folder, try moving it out.</li>
<li>If the watcher doesn’t see a file called <code>index.js</code> and you’re referencing it by the folder name, you <a href="https://github.com/facebookincubator/create-react-app/issues/1164" target="_blank">need to restart the watcher</a><img src="chrome-extension://pgmpdhecmoecoihpehfeghpcphaeenkp/images/star-orange.svg" />46,703 due to a Webpack bug.</li>
<li>Some editors like Vim and IntelliJ have a “safe write” feature that currently breaks the watcher. You will need to disable it. Follow the instructions in <a href="https://webpack.js.org/guides/development/#adjusting-your-text-editor" target="_blank">“Adjusting Your Text Editor”</a>.</li>
<li>If your project path contains parentheses, try moving the project to a path without them. This is caused by a <a href="https://github.com/webpack/watchpack/issues/42" target="_blank">Webpack watcher bug</a><img src="chrome-extension://pgmpdhecmoecoihpehfeghpcphaeenkp/images/star-blue.svg" />116.</li>
<li>On Linux and macOS, you might need to <a href="https://github.com/webpack/docs/wiki/troubleshooting#not-enough-watchers" target="_blank">tweak system settings</a> to allow more watchers.</li>
<li>If the project runs inside a virtual machine such as (a Vagrant provisioned) VirtualBox, create an <code>.env</code> file in your project directory if it doesn’t exist, and add <code>CHOKIDAR_USEPOLLING=true</code> to it. This ensures that the next time you run <code>npm start</code>, the watcher uses the polling mode, as necessary inside a VM.</li>
</ul>
<p>If none of these solutions help please leave a comment <a href="https://github.com/facebookincubator/create-react-app/issues/659" target="_blank">in this thread</a>.</p>
<h3><code>npm test</code> hangs on macOS Sierra</h3>
<p>If you run <code>npm test</code> and the console gets stuck after printing <code>react-scripts test --env=jsdom</code> to the console there might be a problem with your <a href="https://facebook.github.io/watchman/" target="_blank">Watchman</a> installation as described in <a href="https://github.com/facebookincubator/create-react-app/issues/713" target="_blank">facebookincubator/create-react-app#713</a>.</p>
<p>We recommend deleting <code>node_modules</code> in your project and running <code>npm install</code> (or <code>yarn</code> if you use it) first. If it doesn't help, you can try one of the numerous workarounds mentioned in these issues:</p>

<p>It is reported that installing Watchman 4.7.0 or newer fixes the issue. If you use <a href="http://brew.sh/" target="_blank">Homebrew</a>, you can run these commands to update it:</p>
<pre><code>watchman shutdown-server
brew update
brew reinstall watchman
</code></pre>
<p>You can find <a href="https://facebook.github.io/watchman/docs/install.html#build-install" target="_blank">other installation methods</a> on the Watchman documentation page.</p>
<p>If this still doesn’t help, try running <code>launchctl unload -F ~/Library/LaunchAgents/com.github.facebook.watchman.plist</code>.</p>
<p>There are also reports that <em>uninstalling</em> Watchman fixes the issue. So if nothing else helps, remove it from your system and try again.</p>
<h3><code>npm run build</code> exits too early</h3>
<p>It is reported that <code>npm run build</code> can fail on machines with limited memory and no swap space, which is common in cloud environments. Even with small projects this command can increase RAM usage in your system by hundreds of megabytes, so if you have less than 1 GB of available memory your build is likely to fail with the following message:</p>
<blockquote>
<p>The build failed because the process exited too early. This probably means the system ran out of memory or someone called <code>kill -9</code> on the process.</p>
</blockquote>
<p>If you are completely sure that you didn't terminate the process, consider <a href="https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-ubuntu-14-04" target="_blank">adding some swap space</a> to the machine you’re building on, or build the project locally.</p>
<h3><code>npm run build</code> fails on Heroku</h3>
<p>This may be a problem with case sensitive filenames.
Please refer to <a href="#resolving-heroku-deployment-errors" target="_blank">this section</a>.</p>
<h3>Moment.js locales are missing</h3>
<p>If you use a <a href="https://momentjs.com/" target="_blank">Moment.js</a>, you might notice that only the English locale is available by default. This is because the locale files are large, and you probably only need a subset of <a href="https://momentjs.com/#multiple-locale-support" target="_blank">all the locales provided by Moment.js</a>.</p>
<p>To add a specific Moment.js locale to your bundle, you need to import it explicitly.<br />
For example:</p>
<div><pre>import moment from 'moment';
import 'moment/locale/fr';</pre></div>
<p>If import multiple locales this way, you can later switch between them by calling <code>moment.locale()</code> with the locale name:</p>
<div><pre>import moment from 'moment';
import 'moment/locale/fr';
import 'moment/locale/es';

// ...

moment.locale('fr');</pre></div>
<p>This will only work for locales that have been explicitly imported before.</p>
<h3><code>npm run build</code> fails to minify</h3>
<p>Some third-party packages don't compile their code to ES5 before publishing to npm. This often causes problems in the ecosystem because neither browsers (except for most modern versions) nor some tools currently support all ES6 features. We recommend to publish code on npm as ES5 at least for a few more years.</p>
To resolve this:
<ol>
<li>Open an issue on the dependency's issue tracker and ask that the package be published pre-compiled.</li>
</ol>
<ul>
<li>Note: Create React App can consume both CommonJS and ES modules. For Node.js compatibility, it is recommended that the main entry point is CommonJS. However, they can optionally provide an ES module entry point with the <code>module</code> field in <code>package.json</code>. Note that <strong>even if a library provides an ES Modules version, it should still precompile other ES6 features to ES5 if it intends to support older browsers</strong>.</li>
</ul>
<ol>
<li>
<p>Fork the package and publish a corrected version yourself.</p>
</li>
<li>
<p>If the dependency is small enough, copy it to your <code>src/</code> folder and treat it as application code.</p>
</li>
</ol>
<p>In the future, we might start automatically compiling incompatible third-party modules, but it is not currently supported. This approach would also slow down the production builds.</p>
<h2>Alternatives to Ejecting</h2>
<p><a href="#npm-run-eject" target="_blank">Ejecting</a> lets you customize anything, but from that point on you have to maintain the configuration and scripts yourself. This can be daunting if you have many similar projects. In such cases instead of ejecting we recommend to <em>fork</em> <code>react-scripts</code> and any other packages you need. <a href="https://auth0.com/blog/how-to-configure-create-react-app/" target="_blank">This article</a> dives into how to do it in depth. You can find more discussion in <a href="https://github.com/facebookincubator/create-react-app/issues/682" target="_blank">this issue</a>.</p>
<h2>Something Missing?</h2>
<p>If you have ideas for more “How To” recipes that should be on this page, <a href="https://github.com/facebookincubator/create-react-app/issues" target="_blank">let us know</a> or <a href="https://github.com/facebookincubator/create-react-app/edit/master/packages/react-scripts/template/README.md" target="_blank">contribute some!</a></p>

<a href="http://www.bebetterdeveloper.com/coding/getting-started-react-mocha.html">http://www.bebetterdeveloper.com/coding/getting-started-react-mocha.html</a><div id="articleHeader"><h1>Getting started w/ React & Mocha</h1></div>
     <p>Posted by <em> Lena Barinova</em> on Jul 16, 2015</p>

   
    
    
    
  
  
    
      
      <a href="http://www.bebetterdeveloper.com/categories.html#Coding" target="_blank"> Coding</a>
      
    
  </header>
  
  
  
    <p><em>11/23/2015: I updated this blog post as well as the code to support the newest version of React, ReactDOM, ReactTestUtils, Mocha, JSDOM, Babel. The changed are really minor, but may be frustraiting for some. For those, who are interested in how should this code be written using older version of these libs (React 0.13.3, Mocha 2.0.1, JSDOM 3.1.2, Mocha-JSDOM 1.0.0, Babel 5.1.13) please clone this <a href="https://github.com/LenaBarinova/react-mocha-example/tree/9b71d468a1b7af5b6366be71a3e0dee9b45e3f37" target="_blank">commit from GitHub</a>.</em></p>

<p>It took me half day to setup [almost] empty environment for React app development with testing done using Mocha.
I decided to share my findings here so it would remain.
<div class="readableLargeImageContainer float"><img src="/img/post_img/vfd-react-mocha.png" alt="React and Mocha logo" /></div></p>

<h2 id="my-target">My target</h2>
<p>I wanted to create an environment for further React development. The things that I needed to have:</p>

<ul>
  <li>source structure, that would be suitable for medium-sized project</li>
  <li>build scripts, that would do all needed transformations, run tests, show the output of my app</li>
  <li>Mocha as a test framework of choice</li>
</ul>

<p>For build scripts I prefer to use gulp.</p>

<h2 id="tldr">tl;dr</h2>
<p>You can find working code <a href="https://github.com/LenaBarinova/react-mocha-example" target="_blank">here</a>. Just download it and run</p>

<pre><code>$npm install
</code></pre>

<p>followed by</p>

<pre><code>$npm test
</code></pre>

<p>If you are using Visual Studio Code - you can build it using <code>⇧⌘B</code> (on Mac).</p>

<h2 id="how-i-did-it">How I did it</h2>
<p>I started with these three stages:</p>

<ol>
  <li>Prepare the environment</li>
  <li>Create first React component</li>
  <li>Add Mocha tests</li>
</ol>

<h2 id="step-1-prepare-the-environment">Step 1. Prepare the environment</h2>
<p>First install <a href="https://nodejs.org/" target="_blank">Node.js</a> (if you don’t have it yet).
In your project directory (<em>react-mocha-example</em> in my case) through Terminal do:</p>

<pre><code>$npm init
</code></pre>

<p>and follow the instruction. Then run this command to install libraries to setup the working environment:</p>

<pre><code>$npm install react react-dom babel babel-preset-es2015 babel-preset-react gulp gulp-load-plugins browserify babelify babel-core vinyl-source-stream gulp-open --save-dev
</code></pre>

<p>Now your <em>package.json</em> should look like this:
</p><div id="gist24354655">
    <div>
      <div>
        <div>
  <div id="file-vfd_package_v1-json">
    

  <div>
      <table>
      <tbody>
      <tr>
        <td id="file-vfd_package_v1-json-L2"></td>
        <td id="file-vfd_package_v1-json-LC2">  "name": "react-mocha-example",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L3"></td>
        <td id="file-vfd_package_v1-json-LC3">  "version": "1.0.0",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L4"></td>
        <td id="file-vfd_package_v1-json-LC4">  "description": "Getting started with React and Mocha",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L5"></td>
        <td id="file-vfd_package_v1-json-LC5">  "main": "index.html",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L6"></td>
        <td id="file-vfd_package_v1-json-LC6">  "devDependencies": {</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L7"></td>
        <td id="file-vfd_package_v1-json-LC7">    "babel": "^6.1.18",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L8"></td>
        <td id="file-vfd_package_v1-json-LC8">    "babel-core": "^6.2.1",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L9"></td>
        <td id="file-vfd_package_v1-json-LC9">    "babel-preset-es2015": "^6.1.18",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L10"></td>
        <td id="file-vfd_package_v1-json-LC10">    "babel-preset-react": "^6.1.18",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L11"></td>
        <td id="file-vfd_package_v1-json-LC11">    "babelify": "^7.2.0",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L12"></td>
        <td id="file-vfd_package_v1-json-LC12">    "browserify": "^12.0.1",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L13"></td>
        <td id="file-vfd_package_v1-json-LC13">    "gulp": "^3.9.0",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L14"></td>
        <td id="file-vfd_package_v1-json-LC14">    "gulp-load-plugins": "^1.1.0",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L15"></td>
        <td id="file-vfd_package_v1-json-LC15">    "gulp-open": "^1.0.0",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L16"></td>
        <td id="file-vfd_package_v1-json-LC16">    "react": "^0.14.3",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L17"></td>
        <td id="file-vfd_package_v1-json-LC17">    "react-dom": "^0.14.3",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L18"></td>
        <td id="file-vfd_package_v1-json-LC18">    "vinyl-source-stream": "^1.1.0"</td>
      </tr>
      
      <tr>
        <td id="file-vfd_package_v1-json-L20"></td>
        <td id="file-vfd_package_v1-json-LC20">  "repository": {</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L21"></td>
        <td id="file-vfd_package_v1-json-LC21">    "type": "git",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L22"></td>
        <td id="file-vfd_package_v1-json-LC22">    "url": "https://github.com/JelenaBarinova/react-mocha-example.git"</td>
      </tr>
      
      <tr>
        <td id="file-vfd_package_v1-json-L24"></td>
        <td id="file-vfd_package_v1-json-LC24">  "homepage": "http://jelenabarinova.github.io/react-mocha-example",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L25"></td>
        <td id="file-vfd_package_v1-json-LC25">  "author": "Lena Barinova",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v1-json-L26"></td>
        <td id="file-vfd_package_v1-json-LC26">  "license": "MIT"</td>
      </tr>
      
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>
<p>Add <em>.babelrc</em> file to your project root with these settings:
</p><div id="gist28321074">
    <div>
      <div>
        <div>
  <div id="file-vfd_babelrc">
    

  <div>
      <table>
      <tbody>
      <tr>
        <td id="file-vfd_babelrc-L2"></td>
        <td id="file-vfd_babelrc-LC2">  "presets": ["react", "es2015"]</td>
      </tr>
      
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>
<p>Create <em>gulpfile.js</em> to configure build steps:
</p><div id="gist24354901">
    <div>
      <div>
        <div>
  <div id="file-vfd_gulpfile_v1-js">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-vfd_gulpfile_v1-js-L1"></td>
        <td id="file-vfd_gulpfile_v1-js-LC1">var gulp = require('gulp');</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L2"></td>
        <td id="file-vfd_gulpfile_v1-js-LC2">var plug = require('gulp-load-plugins')({ lazy: true });</td>
      </tr>
      
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L4"></td>
        <td id="file-vfd_gulpfile_v1-js-LC4">var browserify = require('browserify');</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L5"></td>
        <td id="file-vfd_gulpfile_v1-js-LC5">var babelify = require('babelify');</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L6"></td>
        <td id="file-vfd_gulpfile_v1-js-LC6">var babel = require('babel-core/register');</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L7"></td>
        <td id="file-vfd_gulpfile_v1-js-LC7">var source = require('vinyl-source-stream');</td>
      </tr>
      
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L9"></td>
        <td id="file-vfd_gulpfile_v1-js-LC9">gulp.task('babelify', function () {</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L10"></td>
        <td id="file-vfd_gulpfile_v1-js-LC10">  return browserify({</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L11"></td>
        <td id="file-vfd_gulpfile_v1-js-LC11">    extensions: ['.jsx', '.js'],</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L12"></td>
        <td id="file-vfd_gulpfile_v1-js-LC12">    entries: './app.jsx',</td>
      </tr>
      
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L14"></td>
        <td id="file-vfd_gulpfile_v1-js-LC14">    .transform(babelify.configure({ ignore: /(node_modules)/ }))</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L15"></td>
        <td id="file-vfd_gulpfile_v1-js-LC15">    .bundle()</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L16"></td>
        <td id="file-vfd_gulpfile_v1-js-LC16">    .on("error", function (err) { console.log("Error : " + err.message); })</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L17"></td>
        <td id="file-vfd_gulpfile_v1-js-LC17">    .pipe(source('app.js'))</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L18"></td>
        <td id="file-vfd_gulpfile_v1-js-LC18">    .pipe(gulp.dest('./output/'));</td>
      </tr>
      
      
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L21"></td>
        <td id="file-vfd_gulpfile_v1-js-LC21">gulp.task('build',['babelify'], function(){</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L22"></td>
        <td id="file-vfd_gulpfile_v1-js-LC22">  return gulp.src('./index.html')</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v1-js-L23"></td>
        <td id="file-vfd_gulpfile_v1-js-LC23">        .pipe(plug.open(), {app: 'google-chrome'});</td>
      </tr>
      
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>

I’m using <a href="https://www.npmjs.com/package/gulp-load-plugins" target="_blank">gulp-load-plugins</a> for easy and fast use of different gulp plugins. It enables me to access all the plugins I have listed in package.json file without ‘require’ each of them separately.<p>So now everything is ready to start really writing a code. Create <em>index.html</em> file:
</p><div id="gist24354799">
    <div>
      <div>
        <div>
  <div id="file-vfd_index-html">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-vfd_index-html-L1"></td>
        <td id="file-vfd_index-html-LC1">&lt;html&gt;</td>
      </tr>
      <tr>
        <td id="file-vfd_index-html-L2"></td>
        <td id="file-vfd_index-html-LC2">  &lt;head&gt;&lt;/head&gt;</td>
      </tr>
      <tr>
        <td id="file-vfd_index-html-L3"></td>
        <td id="file-vfd_index-html-LC3">  &lt;body&gt;</td>
      </tr>
      <tr>
        <td id="file-vfd_index-html-L4"></td>
        <td id="file-vfd_index-html-LC4">    &lt;h1&gt;Getting started with React and Mocha.&lt;/h1&gt;</td>
      </tr>
      <tr>
        <td id="file-vfd_index-html-L5"></td>
        <td id="file-vfd_index-html-LC5">    &lt;div id="container"&gt; &lt;/div&gt;</td>
      </tr>
      
      <tr>
        <td id="file-vfd_index-html-L7"></td>
        <td id="file-vfd_index-html-LC7">    &lt;script src="https://fb.me/react-0.14.3.min.js"&gt;&lt;/script&gt;</td>
      </tr>
      <tr>
        <td id="file-vfd_index-html-L8"></td>
        <td id="file-vfd_index-html-LC8">    &lt;script src="https://fb.me/react-dom-0.14.3.min.js"&gt;&lt;/script&gt;</td>
      </tr>
      <tr>
        <td id="file-vfd_index-html-L9"></td>
        <td id="file-vfd_index-html-LC9">    &lt;script src="output/app.js"&gt;&lt;/script&gt;</td>
      </tr>
      <tr>
        <td id="file-vfd_index-html-L10"></td>
        <td id="file-vfd_index-html-LC10">  &lt;/body&gt;</td>
      </tr>
      <tr>
        <td id="file-vfd_index-html-L11"></td>
        <td id="file-vfd_index-html-LC11">&lt;/html&gt;</td>
      </tr>
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>
<p>Run build command: either using <code>⇧⌘B</code> (from Visual Studio Code on Mac) or command line:</p>

<pre><code>$gulp build
</code></pre>

<p>And you should get Chrome opened with very first version of our app.</p>

<p><div class="readableLargeImageContainer"><img src="/img/post_img/vfd-1.png" alt="First step result" /></div></p>

<h2 id="step-2-create-first-react-component">Step 2. Create first React component</h2>
<p>Create a <em>components</em> directory and <em>component.jsx</em> file in it:
</p><div id="gist24356487">
    <div>
      <div>
        <div>
  <div id="file-vfd_component-jsx">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-vfd_component-jsx-L1"></td>
        <td id="file-vfd_component-jsx-LC1">var React = require('react');</td>
      </tr>
      
      <tr>
        <td id="file-vfd_component-jsx-L3"></td>
        <td id="file-vfd_component-jsx-LC3">var VeryFirstDiv = React.createClass ({</td>
      </tr>
      <tr>
        <td id="file-vfd_component-jsx-L4"></td>
        <td id="file-vfd_component-jsx-LC4">  render() {</td>
      </tr>
      <tr>
        <td id="file-vfd_component-jsx-L5"></td>
        <td id="file-vfd_component-jsx-LC5">    return (</td>
      </tr>
      <tr>
        <td id="file-vfd_component-jsx-L6"></td>
        <td id="file-vfd_component-jsx-LC6">      &lt;div className="veryFirstDiv"&gt;</td>
      </tr>
      <tr>
        <td id="file-vfd_component-jsx-L7"></td>
        <td id="file-vfd_component-jsx-LC7">        &lt;span&gt;Lovely! Here it is - my very first React component!&lt;/span&gt;</td>
      </tr>
      <tr>
        <td id="file-vfd_component-jsx-L8"></td>
        <td id="file-vfd_component-jsx-LC8">      &lt;/div&gt;</td>
      </tr>
      
      
      
      
      <tr>
        <td id="file-vfd_component-jsx-L13"></td>
        <td id="file-vfd_component-jsx-LC13">module.exports = VeryFirstDiv;</td>
      </tr>
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>
<p>Add this componenet to DOM (I did it in <em>app.jsx</em> file in my project root directroy <em>react-mocha-example</em>)
</p><div id="gist24356553">
    <div>
      <div>
        <div>
  <div id="file-vfd_app-js">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-vfd_app-js-L1"></td>
        <td id="file-vfd_app-js-LC1">var ReactDOM   = require('react-dom');</td>
      </tr>
      <tr>
        <td id="file-vfd_app-js-L2"></td>
        <td id="file-vfd_app-js-LC2">var VeryFirstDiv   = require('./components/component');</td>
      </tr>
      
      <tr>
        <td id="file-vfd_app-js-L4"></td>
        <td id="file-vfd_app-js-LC4">ReactDOM.render(</td>
      </tr>
      <tr>
        <td id="file-vfd_app-js-L5"></td>
        <td id="file-vfd_app-js-LC5">  &lt;VeryFirstDiv /&gt;,</td>
      </tr>
      <tr>
        <td id="file-vfd_app-js-L6"></td>
        <td id="file-vfd_app-js-LC6">  document.getElementById('container')</td>
      </tr>
      
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>
<p>Run build task and we can see our React component in a browser.</p>

<p><div class="readableLargeImageContainer"><img src="/img/post_img/vfd-2.png" alt="Second step result" /></div></p>

<h2 id="step-3-adding-first-mocha-test">Step 3. Adding first Mocha test</h2>
<p>This was the trickiest step for me. I found a couple of good articles on the topic. These are my favourite:</p>



<p>Ok, let’s begin.
First, we need to install <a href="http://mochajs.org/" target="_blank">Mocha</a>. To do it, run npm install command with –save-dev, this way your <em>package.json</em> file will be kept updated with all the dependances you use:</p>

<pre><code>$npm install mocha --save-dev
</code></pre>

<p>Create test directory and a first <em>empty-test.js</em>, which just asserts true all the time.
</p><div id="gist24360556">
    <div>
      <div>
        <div>
  <div id="file-vfd_empty_test-js">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-vfd_empty_test-js-L1"></td>
        <td id="file-vfd_empty_test-js-LC1">var assert = require('assert');</td>
      </tr>
      
      <tr>
        <td id="file-vfd_empty_test-js-L3"></td>
        <td id="file-vfd_empty_test-js-LC3">describe('Empty test', function() {</td>
      </tr>
      
      <tr>
        <td id="file-vfd_empty_test-js-L5"></td>
        <td id="file-vfd_empty_test-js-LC5">  it('empty test should run successfully', function() {</td>
      </tr>
      
      <tr>
        <td id="file-vfd_empty_test-js-L7"></td>
        <td id="file-vfd_empty_test-js-LC7">    assert.equal('A', 'A');</td>
      </tr>
      
      
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>
<p>You can try whether it works just running Mocha from command line from you project root folder:</p>

<pre><code>$mocha
</code></pre>

<p>You should get this output:</p>

<p><div class="readableLargeImageContainer"><img src="/img/post_img/vfd-3.png" alt="Third step result" /></div></p>

<p>Now let’s add test running step in our gulp configuration.
For this I used <a href="https://www.npmjs.com/package/gulp-mocha" target="_blank">gulp-mocha</a> - a gulp plugin wrapper around Mocha.</p>

<p>Now add a new ‘test’ step in <em>gulpfile.js</em> to run mocha:
</p><div id="gist24360920">
    <div>
      <div>
        <div>
  <div id="file-vfd_gulpfile_v3-js">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-vfd_gulpfile_v3-js-L1"></td>
        <td id="file-vfd_gulpfile_v3-js-LC1">var gulp = require('gulp');</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L2"></td>
        <td id="file-vfd_gulpfile_v3-js-LC2">var plug = require('gulp-load-plugins')({ lazy: true });</td>
      </tr>
      
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L4"></td>
        <td id="file-vfd_gulpfile_v3-js-LC4">var browserify = require('browserify');</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L5"></td>
        <td id="file-vfd_gulpfile_v3-js-LC5">var babelify = require('babelify');</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L6"></td>
        <td id="file-vfd_gulpfile_v3-js-LC6">var babel = require('babel-core/register');</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L7"></td>
        <td id="file-vfd_gulpfile_v3-js-LC7">var source = require('vinyl-source-stream');</td>
      </tr>
      
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L9"></td>
        <td id="file-vfd_gulpfile_v3-js-LC9">gulp.task('babelify', function () {</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L10"></td>
        <td id="file-vfd_gulpfile_v3-js-LC10">  return browserify({</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L11"></td>
        <td id="file-vfd_gulpfile_v3-js-LC11">    extensions: ['.jsx', '.js'],</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L12"></td>
        <td id="file-vfd_gulpfile_v3-js-LC12">    entries: './app.jsx',</td>
      </tr>
      
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L14"></td>
        <td id="file-vfd_gulpfile_v3-js-LC14">    .transform(babelify.configure({ ignore: /(node_modules)/ }))</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L15"></td>
        <td id="file-vfd_gulpfile_v3-js-LC15">    .bundle()</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L16"></td>
        <td id="file-vfd_gulpfile_v3-js-LC16">    .on("error", function (err) { console.log("Error : " + err.message); })</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L17"></td>
        <td id="file-vfd_gulpfile_v3-js-LC17">    .pipe(source('app.js'))</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L18"></td>
        <td id="file-vfd_gulpfile_v3-js-LC18">    .pipe(gulp.dest('./output/'));</td>
      </tr>
      
      
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L21"></td>
        <td id="file-vfd_gulpfile_v3-js-LC21">gulp.task('test', function () {</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L22"></td>
        <td id="file-vfd_gulpfile_v3-js-LC22">  return gulp.src('./test/**/*.js', { read: false })</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L23"></td>
        <td id="file-vfd_gulpfile_v3-js-LC23">    .pipe(plug.mocha({</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L24"></td>
        <td id="file-vfd_gulpfile_v3-js-LC24">      compilers: {</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L25"></td>
        <td id="file-vfd_gulpfile_v3-js-LC25">        js: babel</td>
      </tr>
      
      
      
      
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L30"></td>
        <td id="file-vfd_gulpfile_v3-js-LC30">gulp.task('build',['babelify', 'test'], function(){</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L31"></td>
        <td id="file-vfd_gulpfile_v3-js-LC31">  return gulp.src('./index.html')</td>
      </tr>
      <tr>
        <td id="file-vfd_gulpfile_v3-js-L32"></td>
        <td id="file-vfd_gulpfile_v3-js-LC32">        .pipe(plug.open(), {app: 'google-chrome'});</td>
      </tr>
      
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>
<p>Before moving on to testing our React component, we need to take care of a couple of things.</p>

<p><strong>First</strong> - DOM mocking. You can find very good explanation about how to mock DOM in this <a href="http://www.asbjornenge.com/wwc/testing_react_components.html" target="_blank">blog post</a>.
To follow this example we need to install <a href="https://github.com/tmpvar/jsdom" target="_blank">jsdom</a> and <a href="https://github.com/rstacruz/mocha-jsdom" target="_blank">mocha-jsdom</a>.
I’ve created <em>dom-mock.js</em> file (it’s a bit different from what is given in the article, I adopted it to be compatible with the newest JSDOM version).
</p><div id="gist24361090">
    <div>
      <div>
        <div>
  <div id="file-vfd_dom_mock-js">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-vfd_dom_mock-js-L1"></td>
        <td id="file-vfd_dom_mock-js-LC1">module.exports = function(markup) {</td>
      </tr>
      <tr>
        <td id="file-vfd_dom_mock-js-L2"></td>
        <td id="file-vfd_dom_mock-js-LC2">  if (typeof document !== 'undefined') return;</td>
      </tr>
      
      <tr>
        <td id="file-vfd_dom_mock-js-L4"></td>
        <td id="file-vfd_dom_mock-js-LC4">  var jsdom = require('jsdom').jsdom;</td>
      </tr>
      
      <tr>
        <td id="file-vfd_dom_mock-js-L6"></td>
        <td id="file-vfd_dom_mock-js-LC6">  global.document = jsdom(markup || '');</td>
      </tr>
      <tr>
        <td id="file-vfd_dom_mock-js-L7"></td>
        <td id="file-vfd_dom_mock-js-LC7">  global.window = document.defaultView;</td>
      </tr>
      <tr>
        <td id="file-vfd_dom_mock-js-L8"></td>
        <td id="file-vfd_dom_mock-js-LC8">  global.navigator = {</td>
      </tr>
      <tr>
        <td id="file-vfd_dom_mock-js-L9"></td>
        <td id="file-vfd_dom_mock-js-LC9">    userAgent: 'node.js'</td>
      </tr>
      
      
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>
<p><strong>Second</strong> - install <a href="https://www.npmjs.com/package/react-addons-test-utils" target="_blank">React TestUtils add-on</a>:</p>

<pre><code>$npm install react-addons-test-utils --save-dev
</code></pre>

<p>And finally - the test! I’ve created <em>component-test.js</em> file in test directory:
</p><div id="gist24361495">
    <div>
      <div>
        <div>
  <div id="file-vfd_component_test-js">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-vfd_component_test-js-L1"></td>
        <td id="file-vfd_component_test-js-LC1">// Mocking window and document object:</td>
      </tr>
      <tr>
        <td id="file-vfd_component_test-js-L2"></td>
        <td id="file-vfd_component_test-js-LC2">require('./dom-mock')('&lt;html&gt;&lt;body&gt;&lt;/body&gt;&lt;/html&gt;');</td>
      </tr>
      
      <tr>
        <td id="file-vfd_component_test-js-L4"></td>
        <td id="file-vfd_component_test-js-LC4">var jsdom = require('mocha-jsdom');</td>
      </tr>
      <tr>
        <td id="file-vfd_component_test-js-L5"></td>
        <td id="file-vfd_component_test-js-LC5">var assert = require('assert');</td>
      </tr>
      <tr>
        <td id="file-vfd_component_test-js-L6"></td>
        <td id="file-vfd_component_test-js-LC6">var React = require('react');</td>
      </tr>
      <tr>
        <td id="file-vfd_component_test-js-L7"></td>
        <td id="file-vfd_component_test-js-LC7">var TestUtils = require('react-addons-test-utils');</td>
      </tr>
      
      <tr>
        <td id="file-vfd_component_test-js-L9"></td>
        <td id="file-vfd_component_test-js-LC9">describe('Testing my div', function() {</td>
      </tr>
      <tr>
        <td id="file-vfd_component_test-js-L10"></td>
        <td id="file-vfd_component_test-js-LC10">  jsdom({ skipWindowCheck: true });</td>
      </tr>
      
      <tr>
        <td id="file-vfd_component_test-js-L12"></td>
        <td id="file-vfd_component_test-js-LC12">  it('should contain text: Lovely! Here it is - my very first React component!', function() {</td>
      </tr>
      <tr>
        <td id="file-vfd_component_test-js-L13"></td>
        <td id="file-vfd_component_test-js-LC13">    var VeryFirstDiv = require('../components/component.jsx');</td>
      </tr>
      <tr>
        <td id="file-vfd_component_test-js-L14"></td>
        <td id="file-vfd_component_test-js-LC14">    var myDiv = TestUtils.renderIntoDocument(</td>
      </tr>
      <tr>
        <td id="file-vfd_component_test-js-L15"></td>
        <td id="file-vfd_component_test-js-LC15">      &lt;VeryFirstDiv /&gt;</td>
      </tr>
      
      <tr>
        <td id="file-vfd_component_test-js-L17"></td>
        <td id="file-vfd_component_test-js-LC17">    var divText = TestUtils.findRenderedDOMComponentWithTag(myDiv, 'span');</td>
      </tr>
      
      <tr>
        <td id="file-vfd_component_test-js-L19"></td>
        <td id="file-vfd_component_test-js-LC19">    assert.equal(divText.textContent, 'Lovely! Here it is - my very first React component!');</td>
      </tr>
      
      
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>
<p>Run build. Hurray! The test is passing:</p>

<p><div class="readableLargeImageContainer"><img src="/img/post_img/vfd-4.png" alt="Fourth step result" /></div></p>

<p>You can also configure your <em>package.json</em> - to run tests from command line using npm. For this add test section in your <em>package.json</em> like this:
</p><div id="gist24361683">
    <div>
      <div>
        <div>
  <div id="file-vfd_package_v2-json">
    

  <div>
      <table>
      <tbody>
      <tr>
        <td id="file-vfd_package_v2-json-L2"></td>
        <td id="file-vfd_package_v2-json-LC2">  "name": "react-mocha-example",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L3"></td>
        <td id="file-vfd_package_v2-json-LC3">  "version": "1.0.0",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L4"></td>
        <td id="file-vfd_package_v2-json-LC4">  "description": "Getting started with React and Mocha",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L5"></td>
        <td id="file-vfd_package_v2-json-LC5">  "main": "index.html",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L6"></td>
        <td id="file-vfd_package_v2-json-LC6">  "devDependencies": {</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L7"></td>
        <td id="file-vfd_package_v2-json-LC7">    "babel": "^6.1.18",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L8"></td>
        <td id="file-vfd_package_v2-json-LC8">    "babel-core": "^6.2.1",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L9"></td>
        <td id="file-vfd_package_v2-json-LC9">    "babel-preset-es2015": "^6.1.18",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L10"></td>
        <td id="file-vfd_package_v2-json-LC10">    "babel-preset-react": "^6.1.18",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L11"></td>
        <td id="file-vfd_package_v2-json-LC11">    "babelify": "^7.2.0",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L12"></td>
        <td id="file-vfd_package_v2-json-LC12">    "browserify": "^12.0.1",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L13"></td>
        <td id="file-vfd_package_v2-json-LC13">    "gulp": "^3.9.0",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L14"></td>
        <td id="file-vfd_package_v2-json-LC14">    "gulp-load-plugins": "^1.1.0",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L15"></td>
        <td id="file-vfd_package_v2-json-LC15">    "gulp-mocha": "^2.2.0",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L16"></td>
        <td id="file-vfd_package_v2-json-LC16">    "gulp-open": "^1.0.0",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L17"></td>
        <td id="file-vfd_package_v2-json-LC17">    "jsdom": "^7.0.2",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L18"></td>
        <td id="file-vfd_package_v2-json-LC18">    "mocha": "^2.3.4",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L19"></td>
        <td id="file-vfd_package_v2-json-LC19">    "mocha-jsdom": "^1.0.0",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L20"></td>
        <td id="file-vfd_package_v2-json-LC20">    "react": "^0.14.3",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L21"></td>
        <td id="file-vfd_package_v2-json-LC21">    "react-addons-test-utils": "^0.14.3",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L22"></td>
        <td id="file-vfd_package_v2-json-LC22">    "react-dom": "^0.14.3",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L23"></td>
        <td id="file-vfd_package_v2-json-LC23">    "vinyl-source-stream": "^1.1.0"</td>
      </tr>
      
      <tr>
        <td id="file-vfd_package_v2-json-L25"></td>
        <td id="file-vfd_package_v2-json-LC25">  "scripts": {</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L26"></td>
        <td id="file-vfd_package_v2-json-LC26">    "test": "mocha test/**/*-test.js --compilers js:babel-core/register --recursive"</td>
      </tr>
      
      <tr>
        <td id="file-vfd_package_v2-json-L28"></td>
        <td id="file-vfd_package_v2-json-LC28">  "repository": {</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L29"></td>
        <td id="file-vfd_package_v2-json-LC29">    "type": "git",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L30"></td>
        <td id="file-vfd_package_v2-json-LC30">    "url": "https://github.com/JelenaBarinova/react-mocha-example.git"</td>
      </tr>
      
      <tr>
        <td id="file-vfd_package_v2-json-L32"></td>
        <td id="file-vfd_package_v2-json-LC32">  "homepage": "http://jelenabarinova.github.io/react-mocha-example",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L33"></td>
        <td id="file-vfd_package_v2-json-LC33">  "author": "Lena Barinova",</td>
      </tr>
      <tr>
        <td id="file-vfd_package_v2-json-L34"></td>
        <td id="file-vfd_package_v2-json-LC34">  "license": "MIT"</td>
      </tr>
      
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>
<p>Now you can run:</p>

<pre><code>$npm test
</code></pre>

<p>That’s it! You can download the latest code for this example from <a href="https://github.com/LenaBarinova/react-mocha-example" target="_blank">GitHub</a>.</p>

<p>Happy Testing!</p>

  
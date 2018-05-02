<a href="http://attackofzach.com/setting-up-a-project-using-karma-with-mocha-and-chai/">http://attackofzach.com/setting-up-a-project-using-karma-with-mocha-and-chai/</a><div id="articleHeader"><h1>Setting up a project using karma with mocha and chai</h1></div>
										<div>
					<a href="http://attackofzach.com/setting-up-a-project-using-karma-with-mocha-and-chai/#comments" target="_blank">1 Reply</a>				</div>
					</header>

				
			<p>Recently, I was on a quest to evaluate the <a href="http://visionmedia.github.io/mocha/" target="_blank">mocha</a> javascript testing framework<br />
and its direct support for async testing in the browser. I had a hard time finding a complete description of everything that needed to be done in order to get things working with karma for testing in the browser as opposed to testing a node module.</p>
<p>Consequently, I decided it would be useful to create a guide for those who have similar interests to save everyone time. If you want to skip the steps and just download the code, feel free to clone my <a href="https://github.com/zpratt/karma-mocha-chai" target="_blank">github repository</a>. As a quick aside, I decided to try mocha thanks to some frustrations with jasmine. Async testing with jasmine can be done, but it does not have first-class support in my opinion. I intend to give <a href="http://docs.busterjs.org/en/latest/" target="_blank">buster</a> a spin in the near future as well.</p>
<p>This tutorial assumes that you are on a unix-based system (I used OSX to write the article) and already have a working nodejs and npm installation, therefore installing and configuring a node.js/npm environment is outside the scope of this article. With that said, let’s dig in!</p>
<ol>
<li>Create a directory to hold the project and navigate to that directory:
<ul>
<li><code>mkdir &lt;new_dir&gt;</code></li>
<li><code>cd &lt;new_dir&gt;</code></li>
</ul>
</li>
<li>We’ll be installing a bunch of npm modules, so let’s run <code>npm init</code> to build our package.json file for us</li>
<li>Let’s install <a href="http://karma-runner.github.io/" target="_blank">karma</a> with npm. I recommend installing it locally, since it’s likely that you’ll be either executing karma from an IDE (such as webstorm) or as a grunt task. Additionally, one project may be configured for one version of karma while a different project can use a different version if needed.
<ul>
<li><code>npm install karma --save-dev</code></li>
<li>At the time I wrote this article, the latest stable version of karma was 0.10.8.</li>
</ul>
</li>
<li>Now we’re ready to install mocha:
<ul>
<li><code>npm install mocha --save-dev</code></li>
</ul>
</li>
<li>We’ll also need the karma-mocha adapter so we can use mocha as a test framework with karma:
<ul>
<li><code>npm install karma-mocha --save-dev</code></li>
</ul>
</li>
<li>An assertion library will need to included as well. I prefer the <a href="http://chaijs.com/" target="_blank">chai assertion library</a>, since it offers both bdd style assertions using expect and should as well as junit-style assertions.
<ul>
<li><code>npm install karma-chai --save-dev</code>.</li>
<li>Installing chai this way will make it available as a framework within karma, which makes setup much simpler.</li>
</ul>
</li>
<li>I also find <a href="http://sinonjs.org/" target="_blank">sinon</a> to be extremely useful for stubbing and spying, so let’s install it to round out our set of packages required to get our test environment provisioned:
<ul>
<li><code>npm install karma-sinon --save-dev</code></li>
</ul>
</li>
</ol>
<p>At this point, our package.json should have a devDependencies directive that looks something like this:</p>
<p><strong>devDependencies</strong>: </p><div id="gist14058571">
    <div>
      <div>
        <div>
  <div id="file-example-karma-devdependencies">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-example-karma-devdependencies-L1"></td>
        <td id="file-example-karma-devdependencies-LC1">  "devDependencies": {</td>
      </tr>
      <tr>
        <td id="file-example-karma-devdependencies-L2"></td>
        <td id="file-example-karma-devdependencies-LC2">    "chai": "^1.9.1",</td>
      </tr>
      <tr>
        <td id="file-example-karma-devdependencies-L3"></td>
        <td id="file-example-karma-devdependencies-LC3">    "grunt": "^0.4.5",</td>
      </tr>
      <tr>
        <td id="file-example-karma-devdependencies-L4"></td>
        <td id="file-example-karma-devdependencies-LC4">    "grunt-contrib-jshint": "^0.10.0",</td>
      </tr>
      <tr>
        <td id="file-example-karma-devdependencies-L5"></td>
        <td id="file-example-karma-devdependencies-LC5">    "grunt-karma": "^0.8.3",</td>
      </tr>
      <tr>
        <td id="file-example-karma-devdependencies-L6"></td>
        <td id="file-example-karma-devdependencies-LC6">    "karma": "^0.12.17",</td>
      </tr>
      <tr>
        <td id="file-example-karma-devdependencies-L7"></td>
        <td id="file-example-karma-devdependencies-LC7">    "karma-chai": "^0.1.0",</td>
      </tr>
      <tr>
        <td id="file-example-karma-devdependencies-L8"></td>
        <td id="file-example-karma-devdependencies-LC8">    "karma-mocha": "^0.1.4",</td>
      </tr>
      <tr>
        <td id="file-example-karma-devdependencies-L9"></td>
        <td id="file-example-karma-devdependencies-LC9">    "karma-phantomjs-launcher": "^0.1.4",</td>
      </tr>
      <tr>
        <td id="file-example-karma-devdependencies-L10"></td>
        <td id="file-example-karma-devdependencies-LC10">    "load-grunt-tasks": "^0.6.0",</td>
      </tr>
      <tr>
        <td id="file-example-karma-devdependencies-L11"></td>
        <td id="file-example-karma-devdependencies-LC11">    "mocha": "^1.20.1"</td>
      </tr>
      
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>
<p>We can now create our karma configuration and write some tests. Let’s first make sure that our karma installation is working correctly:</p>
<ul>
<li><code>./node_modules/karma/bin/karma --version</code></li>
</ul>
<p>That should print out the version number to the console if everything is working correctly. If you want to, you can initialize a karma configuration file using:</p>
<ul>
<li><code>./node_modules/karma/bin/karma init</code></li>
</ul>
<p>I’ll provide the boilerplate so you can avoid that step. Include the following configuration in a file named</p>
<p><strong>karma.conf.js</strong>: </p><div id="gist14058394">
    <div>
      <div>
        <div>
  <div id="file-example-karma-config-js">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-example-karma-config-js-L1"></td>
        <td id="file-example-karma-config-js-LC1">module.exports = function (config) {</td>
      </tr>
      <tr>
        <td id="file-example-karma-config-js-L2"></td>
        <td id="file-example-karma-config-js-LC2">    'use strict';</td>
      </tr>
      <tr>
        <td id="file-example-karma-config-js-L3"></td>
        <td id="file-example-karma-config-js-LC3">    config.set({</td>
      </tr>
      
      <tr>
        <td id="file-example-karma-config-js-L5"></td>
        <td id="file-example-karma-config-js-LC5">        basePath: '',</td>
      </tr>
      
      <tr>
        <td id="file-example-karma-config-js-L7"></td>
        <td id="file-example-karma-config-js-LC7">        frameworks: ['mocha', 'chai'],</td>
      </tr>
      
      <tr>
        <td id="file-example-karma-config-js-L9"></td>
        <td id="file-example-karma-config-js-LC9">        files: [</td>
      </tr>
      <tr>
        <td id="file-example-karma-config-js-L10"></td>
        <td id="file-example-karma-config-js-LC10">            'src/*.js',</td>
      </tr>
      <tr>
        <td id="file-example-karma-config-js-L11"></td>
        <td id="file-example-karma-config-js-LC11">            'test/*.spec.js'</td>
      </tr>
      
      
      <tr>
        <td id="file-example-karma-config-js-L14"></td>
        <td id="file-example-karma-config-js-LC14">        reporters: ['progress'],</td>
      </tr>
      
      <tr>
        <td id="file-example-karma-config-js-L16"></td>
        <td id="file-example-karma-config-js-LC16">        port: 9876,</td>
      </tr>
      <tr>
        <td id="file-example-karma-config-js-L17"></td>
        <td id="file-example-karma-config-js-LC17">        colors: true,</td>
      </tr>
      <tr>
        <td id="file-example-karma-config-js-L18"></td>
        <td id="file-example-karma-config-js-LC18">        autoWatch: false,</td>
      </tr>
      <tr>
        <td id="file-example-karma-config-js-L19"></td>
        <td id="file-example-karma-config-js-LC19">        singleRun: false,</td>
      </tr>
      
      <tr>
        <td id="file-example-karma-config-js-L21"></td>
        <td id="file-example-karma-config-js-LC21">        // level of logging</td>
      </tr>
      <tr>
        <td id="file-example-karma-config-js-L22"></td>
        <td id="file-example-karma-config-js-LC22">        // possible values: config.LOG_DISABLE || config.LOG_ERROR || config.LOG_WARN || config.LOG_INFO || config.LOG_DEBUG</td>
      </tr>
      <tr>
        <td id="file-example-karma-config-js-L23"></td>
        <td id="file-example-karma-config-js-LC23">        logLevel: config.LOG_INFO,</td>
      </tr>
      
      <tr>
        <td id="file-example-karma-config-js-L25"></td>
        <td id="file-example-karma-config-js-LC25">        browsers: ['PhantomJS']</td>
      </tr>
      
      
      
</tbody></table>


  </div>

  </div>
  
</div>

      </div>
      
    </div>
</div>
<p>Once that file is ready, we can create a failing test to ensure our configuration is working as expected. Create a new file in src/test called <strong>test.spec.js</strong>. Create the directory:</p>
<ul>
<li><code>mkdir -p src/test</code></li>
</ul>
<p>And a test file with the following contents:</p>
<pre>describe("A test suite", function() {
   beforeEach(function() { });
   afterEach(function() { });
   it('should fail', function() { expect(true).to.be.false; });
});
</pre>
<p>With our test spec in place, we can run karma and make sure that we can successfully execute failing tests. <code>./node_modules/karma/bin/karma start karma.conf.js</code></p>
<p>After running our tests, we should see some output along the lines of</p>
<pre>A test suite should fail FAILED</pre>
<p>If so, then you’ve successfully configured karma with mocha, chai and sinon. Cheers!</p>
<h3>Update: 07/14/14</h3>
<p>I recently updated this to use the new 0.12.x version of karma and also added an example <code>Gruntfile.js</code></p>
					
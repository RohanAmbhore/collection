<a href="https://eduardoboucas.com/blog/2017/02/09/contributing-firefox-devtools.html">https://eduardoboucas.com/blog/2017/02/09/contributing-firefox-devtools.html</a><div id="articleHeader"><h1>                Contributing to Mozilla Firefox DevTools              Contributing to              Mozilla Firefox              DevTools                  </h1></div>
        <div>
          
            Wednesday, May 30th, 2018
          
        </div>
      

      
        
          <div>
            <div>
              

              

              Listen to this post

              <audio>
                <source src="/assets/audio/2017-02-09-contributing-firefox-devtools.mp3" type="audio/mpeg" />
              </audio>
              </div>
          </div>
        

        

        
          
        
        
        <p>In 2007, Firebug 1.0 was released as a Mozilla Firefox add-on. This was the first set of browser development tools to feature a DOM inspector, a console and a JavaScript debugger in one place, which revolutionised front-end development tooling and shaped the way other browsers approached it too. A decade later, <a href="https://hacks.mozilla.org/2016/12/firebug-lives-on-in-firefox-devtools/" target="_blank">Firefox DevTools takes its place</a> and I thought it'd be a great time to contribute to it. This article describes my experience in doing it, hoping to convince you to do the same.</p>
<h2>Languages of the web</h2>
<p>Under the hood, Firefox DevTools is essentially a web application built with HTML, CSS and JavaScript. It consists of a front-end piece, which contains all the UI controls to do things like inspect a DOM node or dissect a network request, and a back-end holding the logic that does the actual polling and manipulation of the page being inspected. Interfaces are built as a set of modular <a href="http://mozilla.github.io/devtools-docs/react.html" target="_blank">React components</a> and <a href="http://mozilla.github.io/devtools-docs/redux.html" target="_blank">Redux</a> is used to manage the application state.</p>
<p>DevTools is built using the languages of the web, so any web developer can just dive in and start contributing.</p>
<h2>Pick a task</h2>
<p>There is <a href="http://firefox-dev.tools/" target="_blank">a long list</a> of bug reports and feature requests to choose from. The ones labelled with <em>Good First Bug</em> are probably a good starting point for someone that is new to the codebase.</p>
<p>One of the things I like the most about Mozilla is the community of people, both staff and volunteers, who work tirelessly to make the web a better place. I'm particularly fond of <a href="https://developer.mozilla.org/en-US/" target="_blank">MDN</a>, a community-driven repository of documentation for developers, which I proudly <a href="/blog/2016/08/17/mdn.html" target="_blank">contributed to myself</a>.</p>
<p>In fact, I think Mozilla should leverage this huge knowledge base as much as possible, by syndicating its content to various channels and integrating it with tools used daily by developers — Firefox itself, and DevTools in particular, is a perfect vehicle for that. An example of this is the error messages in the console that, since version 49 of the browser, are accompanied by a link to a relevant MDN page, offering developers extended information about the nature of the error, along with likely causes and possible solutions.</p>
<figure>
  <div class="readableLargeImageContainer"><img src="/posts/2017-02-09-contributing-firefox-devtools/console-error.png" alt="Firefox Web Console showing an error" /></div>
  <figcaption>Firefox Web Console showing an error</figcaption>
</figure>
<p>To help with the effort of integrating MDN with DevTools, I started looking into <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1320233" target="_blank">Bug 1320233</a>. The idea was to add a <em>Learn More</em> button, similar to the one in the console, next to each HTTP header in the Network panel, with a link to the relevant documentation page in MDN.</p>
<h2>Build Firefox</h2>
<p>The first step to make that happen is to download the Firefox source code and build it on your machine. I recommend checking the <a href="https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Build_Instructions" target="_blank">Firefox Build Instructions</a> page on MDN for information specific to your operating system, but it'll start with downloading and running a <a href="https://hg.mozilla.org/mozilla-central/raw-file/default/python/mozboot/bin/bootstrap.py" target="_blank">bootstrap script</a> that will download some dependencies and configure a few things in your system. After that, it's time to download the actual source code and start building.</p>
<pre><code><div># Download the source code</div><div>hg clone http://hg.mozilla.org/mozilla-central/</div><div># Enter the newly-created directory</div><div>cd mozilla-central</div><div># Build</div><div>./mach build</div><div>./mach run</div></code></pre>
<p>You'll notice that we used <code>hg clone</code> instead of <code>git clone</code>. This is because Mozilla uses <a href="https://www.mercurial-scm.org/" target="_blank">Mercurial</a> as a source control management tool, not Git (<em>hg</em> is the chemical symbol for mercury, by the way). It's a bit of a pain, but more on this later.</p>
<p>The build process should take a while, so grab yourself a cup of coffee. When it's finished building, your local version of Firefox Nightly is ready to run.</p>
<h2>Develop for DevTools</h2>
<p>DevTools is typically used to inspect and debug websites, of course, but because the tools themselves are a web application, we can use DevTools to debug itself! To do this, go to <code>Tools</code> &gt; <code>Web Developer</code> &gt; <code>Toggle Tools</code> in Firefox and click on the gear icon to access the settings panel. Make sure you enable <code>Enable browser chrome and add-on debugging toolboxes</code> and <code>Enable remote debugging</code>.</p>
<p>You can then click on the hamburger menu on the top-right corner and go to <code>Developer</code> &gt; <code>Browser Toolbox</code>. You can now inspect the various DevTools panels like you would do with any website. How cool is that?</p>
<figure>
  <div class="readableLargeImageContainer"><img src="/posts/2017-02-09-contributing-firefox-devtools/devtools1.png" alt="Using DevTools to inspect DevTools" /></div>
  <figcaption>Using DevTools to inspect DevTools</figcaption>
</figure>
<p>The code for DevTools lives in the <code>devtools</code> directory on the root of the repository, under which there are a <code>client</code> and <code>server</code>sub-directories for the front-end and the back-end, respectively. Every time you change something in the code, you need to rebuild the application. To avoid the painstakingly long command we ran initially, you can simply use:</p>
<pre><code><div>./mach build faster && ./mach run</div></code></pre>
<h2>Write tests</h2>
<p>When adding a new feature or fixing a bug, it's important to include automated tests along with the code. DevTools includes a suite of unit and integration tests based on <a href="https://developer.mozilla.org/en/XPConnect/xpcshell" target="_blank">xpcshell</a> and <a href="https://developer.mozilla.org/en-US/docs/Mozilla/Projects/Mochitest" target="_blank">Mochitest</a>, a testing suite built on top of <a href="http://mochi.github.io/mochikit/" target="_blank">MochiKit</a>.</p>
<p>Getting the tests right can be quite challenging, as the testing frameworks used in the project are quite bespoke to Mozilla. I recommend having a look around the existing tests and follow conventions as much as possible. There are some shared test utilities (called <em>heads</em>) that you can just import and use in your tests, which might save you some time.</p>
<p>Tests will run as part of a continuous integration system, which we'll cover later, but it's important to make sure they are passing on your local environment before submitting any code.</p>
<pre><code><div># Run all DevTools tests (takes ages)</div><div>./mach test devtools/*</div><div># Run a specific xpcshell test</div><div>./mach xpcshell-test devtools/your-xpcshell-test.js</div><div># Run a specific Mochitest</div><div>./mach mochitest devtools/your-mochitest.js</div></code></pre>
<p>There's <a href="https://wiki.mozilla.org/DevTools/Hacking#DevTools_Automated_Tests" target="_blank">a page</a> on the DevTools Wiki with plenty of information about the testing suite and some best practices for writing new tests.</p>
<h2>Push to try</h2>
<p>The <a href="https://wiki.mozilla.org/ReleaseEngineering/TryServer" target="_blank">Try server</a> is a continuous integration platform used by Mozilla that allows you to have your code evaluated by the same testing infrastructure used in the live release cycle, which includes running tests on various devices and operating systems, without actually pushing the code to the main repository. Your patch is expected to pass the tests on the Try server before being accepted.</p>
<p>To use the Try server, you need commit access to the Mozilla repositories. There are three types of commit access (levels 1 to 3), and you need at least level 1 to use Try. To request access, you should <a href="https://bugzilla.mozilla.org/enter_bug.cgi?product=mozilla.org&component=Repository%20Account%20Requests" target="_blank">file a bug</a> in Bugzilla, stating the level of access you require and your email address, and you must attach a file with your public SSH key (see <a href="https://help.github.com/articles/generating-ssh-keys/" target="_blank">this article</a> if you need help with generating one).</p>
<p>At this point, a Mozillian with sufficient commit access level will need to vouch for you. The mentor or reporter of the bug you're working on should be able to help you with this, otherwise ask for assistance in the <code>#devtools</code> IRC channel. With that taken care of, someone from IT will process the request and email you your credentials.</p>
<p>You'll need to add the Try server to a hosts config file, typically located at <code>~/.ssh/config</code>:</p>
<pre><code><div>Host hg.mozilla.org</div><div>User your-email@address.com</div></code></pre>
<p>To push to Try, you need to choose the platforms and test suites to run, which are defined as a set of parameters to be passed to the CLI tool. The <a href="https://mozilla-releng.net/trychooser/" target="_blank">TryChooser Syntax Builder</a> provides a UI that computes the command you need to use based on the parameters you select. When you run the generated command, you'll receive a link (like <a href="https://treeherder.mozilla.org/#/jobs?repo=try&revision=247af98478ae0f65a87cf1ddf1e0669f51436507" target="_blank">this one</a>) where you can follow the progress of the tests as they come in.</p>
<h2>Submit a patch</h2>
<p>Once you're happy with your changes, it's time to submit the code for review. DevTools is being gradually moved to a <a href="https://github.com/devtools-html" target="_blank">GitHub repository</a>, so if the part of the project you're contributing to is already there, you can simply submit a pull request with your changes, like you would in any other open-source project. If not, you have to generate a patch with Mercurial and attach it to Bugzilla.</p>
<p>To do that, you need to stage and commit all the files you want to submit, similarly to Git. The commit message should follow <a href="https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Committing_Rules_and_Responsibilities" target="_blank">a specific format</a>, including the ID of the bug you're working on and the person responsible for reviewing the code. Finally, you generate a patch file from the commit.</p>
<pre><code><div># Stage the files</div><div>hg add your-file1.js your-file2.js</div><div># Commit with JohnDoe as the reviewer</div><div>hg commit -m "Bug 123456 - Add foo to the bar section. r=JohnDoe"</div><div># Generate a patch file</div><div>hg export . &gt; bug123456.patch</div></code></pre>
<p>You can then attach this patch to the bug and request a review by adding the flag <code>?</code> to the <code>review</code> field. Reviewers will either give their thumbs up or attach additional feedback to the bug, so you might need to repeat the process of staging, committing, pushing to Try and attaching a patch multiple times.</p>
<h2>Celebrate</h2>
<p>Once everyone is happy with your patch, they will check it in and flag it as ready to be included in a future release cycle. As for <a href="https://hg.mozilla.org/mozilla-central/rev/031087a1f3c6" target="_blank">my patch</a>, it will help you learn everything about HTTP headers as soon as Firefox 54 lands. Happy days! ∎</p>
<p><em>Thanks to <a href="https://soledadpenades.com/" target="_blank">Soledad Penadés</a> for reviewing the post.</em></p>


        
      
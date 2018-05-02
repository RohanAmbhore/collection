<a href="https://github.com/meteor/meteor/issues/9224">https://github.com/meteor/meteor/issues/9224</a><div id="articleHeader"><h1>              [1.5.2.2] Production build fails with UglifyJs error while minifying [OS X]            #9224    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/dmitry-salnikov" target="_blank">dmitry-salnikov</a>  opened this Issue
        <relative-time>on Oct 14, 2017</relative-time>
        · 5 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      

  
    
      

          <p>Both <code>meteor build</code> and <code>meteor --production</code> fail, with the next error:</p>
<pre><code>   While processing files with webpack:webpack (for target os.osx.x86_64):
   server/main.js: server.js from UglifyJs
   Unexpected token: name (newObj) [./~/hoek/lib/index.js:33,0]
</code></pre>
<p>Development build is running OK.<br />
The steps I've tried with no success:</p>
<ul>
<li>revert code base to old version with Meteor 1.5.1, which was packaged OK and still running on production for two months - and failed to build it now, with the same error;</li>
<li><code>rm -rf .meteor/local/bundler-cache</code></li>
<li><code>meteor reset && meteor rebuild</code></li>
<li>full meteor reinstall via script;</li>
<li><code>meteor npm cache clean && npm cache clean</code> (using same versions as meteor's built-in, 4.8.4 + 4.6.1);</li>
<li>checked out comments on <a href="https://github.com/meteor/meteor/issues/9138" target="_blank">#9138</a>, <a href="https://github.com/meteor/meteor/issues/9181" target="_blank">#9181</a>, <a href="https://github.com/meteor/meteor/issues/9122" target="_blank">#9122</a>, replaced minifier package with <code>abernix:standard-minifier-js</code>, didn't help.</li>
</ul>
<p>I've googled a bunch of UglifyJS issues, but I can't directly modify configs because of using deprecated build system <a href="https://github.com/thereactivestack-legacy/meteor-webpack" target="_blank">thereactivestack-legacy</a> with webpack. I've tried to get rid of it (assuming that meteor 1.5 can fully replace it), but I'm not so strong in web dev and was lost in thousands of errors occured.</p>
<p>Project <code>packages</code> and <code>versions</code> files here: <a href="https://gist.github.com/dmitry-salnikov/e91464b82f882c6fe5ac6c83c6a33109" target="_blank">https://gist.github.com/dmitry-salnikov/e91464b82f882c6fe5ac6c83c6a33109</a>. Not sure what else info could be helpful.</p>
<p>Thanks in advance for any thoughts.</p>
      
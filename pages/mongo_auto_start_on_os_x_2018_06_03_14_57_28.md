<a href="https://gist.github.com/subfuzion/9630872">https://gist.github.com/subfuzion/9630872</a><div id="articleHeader"><h1>mongo auto start on OS X</h1></div>
    <div>
  <div>
    mongo auto start on OS X
  </div>
</div>


        
  
      
    
  
    <article><h3>Install with Homebrew</h3>
<pre><code>brew install mongodb
</code></pre>
<p>Set up launchctl to auto start <code>mongod</code></p>
<pre><code>$ ln -sfv /usr/local/opt/mongodb/*.plist ~/Library/LaunchAgents
</code></pre>
<p><code>/usr/local/opt/mongodb/</code> is a symlink to <code>/usr/local/Cellar/mongodb/x.y.z</code> (e.g., <code>2.4.9</code>)</p>
<p>You can use launchctl to start and stop <code>mongod</code></p>
<pre><code>$ launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist
$ launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist
</code></pre>
<p>You can also more conveniently use <code>brew</code> to start, stop, and verify service status</p>
<pre><code>$ brew services list | grep mongodb
$ brew services start mongodb
$ brew services stop mongodb
</code></pre>
<h4>Notes</h4>
<p>The default plist provided by homebrew stores the mongod configuration at <code>/usr/local/etc/mongod.conf</code>. This configuration specifies the <code>dbpath</code> to be <code>/usr/local/var/mongodb</code> instead of the default <code>/data/db</code>.</p>
<p>For more about <code>launchctl</code> see:</p>
<p><a href="https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/launchctl.1.html#//apple_ref/doc/man/1/launchctl" target="_blank">https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/launchctl.1.html#//apple_ref/doc/man/1/launchctl</a></p>
<p><a href="http://launchd.info/" target="_blank">http://launchd.info/</a></p>
</article>
  
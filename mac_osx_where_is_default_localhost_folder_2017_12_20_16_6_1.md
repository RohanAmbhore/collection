<a href="https://www.mkyong.com/mac/mac-osx-where-is-default-localhost-folder/">https://www.mkyong.com/mac/mac-osx-where-is-default-localhost-folder/</a><div id="articleHeader"><h1>Mac OSX – where is default localhost folder?</h1></div>

                            <div>
                                <p>By <a href="https://www.mkyong.com/author/mkyong/" title="mkyong" target="_blank">mkyong</a> | <time>September 5, 2017</time> | Viewed : 4,835 times +390 pv/w</p>                            </div>
                            

                            
                                <div>
<div class="readableLargeImageContainer"><img src="http://www.mkyong.com/wp-content/uploads/2017/09/mac-default-localhost-folder.png" /></div>
</div>
<p>On Mac OSX, the default localhost folder is located at <code>/Library/WebServer/Documents</code></p>
<p><em>P.S Tested with MacOS Sierra, 10.12.6</em></p>
<h2>Find httpd.conf</h2>
<p>By default, Apache is enabled and installed in <code>/etc/apache2/</code>, inside <code>httpd.conf</code> file, find  <code>DocumentRoot</code> to tell where is the default localhost folder.</p>
<div>sudo vim /etc/apache2/httpd.conf</div>
<pre><code># DocumentRoot: The directory out of which you will serve your
# documents. By default, all requests are taken from this directory, but
# symbolic links and aliases may be used to point to other locations.
#
DocumentRoot "/Library/WebServer/Documents"
&lt;Directory "/Library/WebServer/Documents"&gt;
    #...
&lt;/Directory&gt;</code></pre>


<h2>References</h2>
<ol>
<li><a href="https://httpd.apache.org/docs/2.4/urlmapping.html" target="_blank">Apache – Mapping URLs to Filesystem Locations</a></li>
</ol>
                            
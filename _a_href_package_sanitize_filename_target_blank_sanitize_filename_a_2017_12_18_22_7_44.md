<a href="https://www.npmjs.com/package/sanitize-filename">https://www.npmjs.com/package/sanitize-filename</a><div id="articleHeader"><h1>    <a href="/package/sanitize-filename" target="_blank">sanitize-filename</a>        </h1></div>

  
    
    
    
      
  

  
      
<p>Sanitize a string to be safe for use as a filename by removing directory
paths and invalid characters.</p>
<h2>Install</h2>
<p><a href="https://www.npmjs.com/package/sanitize-filename" target="_blank">npm: <em>sanitize-filename</em></a></p>
<div><pre><div>npm install sanitize-filename</div></pre></div>
<h2>Example</h2>
<div><pre><div>var sanitize = require("sanitize-filename");</div><div>// Some string that may be unsafe or invalid as a filename </div><div>var UNSAFE_USER_INPUT = "~/.\u0000ssh/authorized_keys";</div><div>// Sanitize the string to be safe for use as a filename. </div><div>var filename = sanitize(UNSAFE_USER_INPUT);</div><div>// -&gt; "~.sshauthorized_keys" </div></pre></div>
<h2>Details</h2>
<p><em>sanitize-filename</em> removes the following:</p>
<ul>
<li><a href="https://en.wikipedia.org/wiki/C0_and_C1_control_codes" target="_blank">Control characters</a> (<code>0x00</code>–<code>0x1f</code> and <code>0x80</code>–<code>0x9f</code>)</li>
<li><a href="https://kb.acronis.com/content/39790" target="_blank">Reserved characters</a> (<code>/</code>, <code>?</code>, <code>&lt;</code>, <code>&gt;</code>, <code>\</code>, <code>:</code>, <code>*</code>, <code>|</code>, and
<code>"</code>)</li>
<li>Unix reserved filenames (<code>.</code> and <code>..</code>)</li>
<li>Trailing periods and spaces (<a href="https://msdn.microsoft.com/en-us/library/aa365247(v=vs.85).aspx#Naming_Conventions" target="_blank">for Windows</a>)</li>
<li>Windows reserved filenames (<code>CON</code>, <code>PRN</code>, <code>AUX</code>, <code>NUL</code>, <code>COM1</code>,
<code>COM2</code>, <code>COM3</code>, <code>COM4</code>, <code>COM5</code>, <code>COM6</code>, <code>COM7</code>, <code>COM8</code>, <code>COM9</code>,
<code>LPT1</code>, <code>LPT2</code>, <code>LPT3</code>, <code>LPT4</code>, <code>LPT5</code>, <code>LPT6</code>, <code>LPT7</code>, <code>LPT8</code>, and
<code>LPT9</code>)</li>
</ul>
<p>The resulting string is truncated to <a href="http://unix.stackexchange.com/questions/32795/what-is-the-maximum-allowed-filename-and-folder-size-with-ecryptfs" target="_blank">255 bytes in length</a>. The
string will not contain any directory paths and will be safe to use as a
filename.</p>
<h3>Empty String <code>""</code> Result</h3>
<p>An empty string <code>""</code> can be returned. For example:</p>
<div><pre><div>var sanitize = require("sanitize-filename");</div><div>sanitize("..")</div><div>// -&gt; "" </div></pre></div>
<h3>Non-unique Filenames</h3>
<p>Two different inputs can return the same value. For example:</p>
<div><pre><div>var sanitize = require("sanitize-filename");</div><div>sanitize("file?")</div><div>// -&gt; "file" </div><div>sanitize ("*file*")</div><div>// -&gt; "file" </div></pre></div>
<h3>File Systems</h3>
<p>Sanitized filenames will be safe for use on modern Windows, OS X, and
Unix file systems (<code>NTFS</code>, <code>ext</code>, etc.).</p>
<p><a href="https://en.wikipedia.org/wiki/8.3_filename" target="_blank"><code>FAT</code> 8.3 filenames</a> are not supported.</p>
<h4>Test Your File System</h4>
<p>The test program will use various strings (including the <a href="https://github.com/minimaxir/big-list-of-naughty-strings" target="_blank">Big List of
Naughty Strings</a>) to create files in the working directory. Run
<code>npm test</code> to run tests against your file system.</p>

<h3><code>sanitize(inputString, [options])</code></h3>
<p>Sanitize <code>inputString</code> by removing or replacing invalid characters.</p>
<p>Options:</p>
<ul>
<li><code>options.replacement</code>: A string to replace invalid characters with.
<em>Optional. Default: <code>""</code>.</em></li>
</ul>

  
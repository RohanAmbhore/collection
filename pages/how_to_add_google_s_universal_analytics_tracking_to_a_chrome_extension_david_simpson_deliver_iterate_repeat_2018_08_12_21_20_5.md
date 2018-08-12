<a href="https://davidsimpson.me/2014/05/27/add-googles-universal-analytics-tracking-chrome-extension/">https://davidsimpson.me/2014/05/27/add-googles-universal-analytics-tracking-chrome-extension/</a><div id="articleHeader"><h1>How to add Google's Universal Analytics tracking to a Chrome extension</h1></div>
    

    
      
 

  
    <p>Google's Universal Analytics is out of beta, so now is a good time to update any Google Chrome extensions with the new code. Except that Google haven't updated their <a href="https://developer.chrome.com/extensions/tut_analytics" target="_blank">tutorial</a> just yet.</p>
<p>Here's the steps for adding Universal Analytics to your Google Chrome extension:</p>
<h2>Update your manifest.json</h2>
<p><b>manifest.json</b></p>
<pre><code>
{<br />
   ...<br />
  "content_security_policy": "script-src 'self' <a href="https://www.google-analytics.com" target="_blank">https://www.google-analytics.com</a>; object-src 'self'"<br /><br /></code><p><code>}<br />
</code></p></pre>
<h2>Update your Options page</h2>
<p>I'm just assuming here that you want to track events in your options page. In your options page e.g. at <b>/options.html</b>, add a reference to the tracking javascript in a separate file:</p>
<pre><code>
&lt;!DOCTYPE html&gt;<br />
&lt;html&gt;<br />
&lt;head&gt;<br />
  ...<br />
  &lt;script src="js/options.js"&gt;&lt;/script&gt;<br />
  ...<br />
&lt;/head&gt;<br />
&lt;body&gt;<br />
  ...<br />
&lt;/body&gt;<br />
&lt;/html&gt;<br />
</code></pre><h2>Update your tracking code</h2>
<p>Add the tracking JavaScript e.g. at <b>js/options.js</b> with the Universal Analytics code. Note the "https" at the start of the script address.</p>
<pre><code>
// Standard Google Universal Analytics code<br />
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){<br />
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),<br />
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)<br />
})(window,document,'script','<a href="https://www.google-analytics.com/analytics.js','ga" target="_blank">https://www.google-analytics.com/analytics.js','ga</a>'); // Note: https protocol here<br /><br /></code><p><code>ga('create', 'UA-XXXXX-YY', 'auto');<br />
ga('set', 'checkProtocolTask', function(){}); // Removes failing protocol check. @see: <a href="http://stackoverflow.com/a/22152353/1958200" target="_blank">http://stackoverflow.com/a/22152353/1958200</a><br />
ga('require', 'displayfeatures');<br />
ga('send', 'pageview', '/options.html');<br />
</code></p></pre>
<p>There are 3 points I'd particularly like to highlight:</p>
<ol>
<li>Specify "<b>https</b>" at the start of the script address to match with the listing in the manifest.json file</li>
<li>Override <b>checkProtocolTask</b> with an empty function</li>
<li>Send a virtual pageview by specifying the path – <b>'/options.html'</b> – otherwise Google Analytics will reject a URL in the format <pre><code>chrome-extension://gdocgfhmbfbbbmhnhmmejncjdcbjkhfc/options.html</code></pre></li>
</ol>
<p>If that all went well, you should soon see page tracking in Google Analytics, like so:</p>
<p><a href="/wp-content/uploads/2014/05/ga-options.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/assets/ga-options.png" alt="ga-options" /></div></a></p>

  
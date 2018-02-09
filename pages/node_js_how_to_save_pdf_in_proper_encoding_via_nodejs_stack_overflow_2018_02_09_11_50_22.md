<a href="https://stackoverflow.com/questions/31040014/how-to-save-pdf-in-proper-encoding-via-nodejs">https://stackoverflow.com/questions/31040014/how-to-save-pdf-in-proper-encoding-via-nodejs</a><div id="articleHeader"><h1>How to save pdf in proper encoding via nodejs</h1></div>

<p>So I'm trying to download a pdf file from a website with my script but the problem is that the file gets broken in the process and I'm pretty sure it's because of wrong encoding being used.</p>

<p>I'm using request lib for downloading the file and I've set the <code>Content-type</code> to <code>application-pdf</code></p>

<p>My code is pretty simple:4</p>

<pre><code>var fs = require('fs');
var request = require("request");


request({uri: 'xxxxxxxxxxxxxx.pdf', headers: { 'Content-type' : 'applcation/pdf' }} , function (error, response, body) {
  if (!error && response.statusCode == 200) {
    fs.writeFileSync("10111.pdf", body);
  }
})</code></pre>

<p>Where do I need to specify the encoding used for this to work?</p>

<p>I tried opening the pdf that I get by normal saving and SublimeText3 encodinghelper says it's in Windows-something while the one I downloaded is in utf8.</p>

<p>I've gone through the nodejs buffer and fs files and they do not supprt encodings like windows-asd, only the general ones like 'utf8' and 'binary'.</p>

<p>Should I maybe use a different method for obtaining the file?</p>
    
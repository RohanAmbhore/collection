<a href="https://ourcodeworld.com/articles/read/203/mastering-the-use-of-the-clipboard-with-electron-framework">https://ourcodeworld.com/articles/read/203/mastering-the-use-of-the-clipboard-with-electron-framework</a><div id="articleHeader"><h1>Mastering the use of the Clipboard with Electron Framework</h1></div>
                    
                                                    <div class="readableLargeImageContainer"><img src="/public-media/articles/articleocw-578635c52e080.png" alt="Mastering the use of the Clipboard with Electron Framework" /></div>
                            <hr />
                                                <p>Modern GUIs often provide a clipboard manager which supports multiple cut and paste transactions. In this model the clipboard is treated as a stack or scrap book, with new cuts and copies being placed on top of the list of recent transactions.</p>
<p>If your electron App prevents any keyboard event by default and you want to filter the events according to the user actions by yourself (or simply be fancy and add copy/paste buttons in your UI), you may want to know how to handle manually the clipboard.</p>
<h2>Accesing the Clibpoard</h2>
<p>To access the clipboard, we are going to use following line :</p>
<pre><code>const {clipboard} = require('electron');</code><div><div><a target="_blank"> Copy snippet</a></div></div></pre>
<p>The clipboard variable (in the scope), will allow you to copy, paste and use other methods that the clipboard of the OS have to offer.</p>
<h2>Retrieve clipboard content</h2>
<p>There are 3 ways to retrieve the content :</p>
<h3>As Plain text</h3>
<p>You can retrieve the content of the clipboard as plain text using the <code>readText</code> method of the clipboard.</p>
<pre><code>const {clipboard} = require('electron');
var content = clipboard.readText();
alert(content);</code><div><div><a target="_blank"> Copy snippet</a></div></div></pre>
<h3>As HTML</h3>
<p>You can retrieve the content of the clipboard but with the markup content using the <code>readHtml</code> method.</p>
<pre><code>const {clipboard} = require('electron');
var content = clipboard.readHtml();
alert(content);</code><div><div><a target="_blank"> Copy snippet</a></div></div></pre>
<h3>As RTF</h3>
<p>You can retrieve the content of the clipboard as RTF (rich text format) using the <code>readRtf</code> method:</p>
<pre><code>const {clipboard} = require('electron');
var content = clipboard.readRtf();
alert(content);</code><div><div><a target="_blank"> Copy snippet</a></div></div></pre>
<h2>Set clipboard content</h2>
<p>There are 3 methods to set the content of the clipboard in your app.</p>
<h3>As Plain Text</h3>
<p>You can fill the content of the clipboard with plain text using the <code>writeText</code> method.</p>
<pre><code>const {clipboard} = require('electron');
var content = "Text that will be now on the clipboard as text";
clipboard.writeText(content);</code><div><div><a target="_blank"> Copy snippet</a></div></div></pre>
<h3>As HTML</h3>
<p>You can fill the content of the clipboard with markup using the <code>writeText</code> method.</p>
<pre><code>const {clipboard} = require('electron');
var content = "&lt;b&gt;Try to paste this content into some editor&lt;/b&gt; and see how this &lt;em&gt;Works&lt;/em&gt;";
clipboard.writeHtml(content);</code><div><div><a target="_blank"> Copy snippet</a></div></div></pre>
<h3>As RTF</h3>
<p>You can fill the content of the clipboard as RTF (rich text format) using the write<code>Rtf</code> method:</p>
<pre><code>const {clipboard} = require('electron');
var content = "{\rtf1\ansi{\fonttbl\f0\fswiss Helvetica;}\f0\pard This is some {\b bold} text.\par }";
clipboard.writeRtf(content);</code><div><div><a target="_blank"> Copy snippet</a></div></div></pre>
<p><a href="https://github.com/electron/electron/blob/master/docs/api/clipboard.md" target="_blank">Read the official documentation of the clipboard here</a> in the repository.</p>
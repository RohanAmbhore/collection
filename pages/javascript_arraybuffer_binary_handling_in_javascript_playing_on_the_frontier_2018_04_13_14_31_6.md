<a href="https://loune.net/2011/05/javascript-arraybuffer-binary-handling-in-javascript/">https://loune.net/2011/05/javascript-arraybuffer-binary-handling-in-javascript/</a><div id="articleHeader"><h1>Javascript ArrayBuffer – Binary handling in javascript</h1></div>
										<div>
					<a href="https://loune.net/2011/05/javascript-arraybuffer-binary-handling-in-javascript/#respond" target="_blank">Leave a reply</a>				</div>
					</header>

				<div>
			<p>As javascript and HTML5 venture into applications never <a href="http://bellard.org/jslinux/" target="_blank">contemplated</a>, there was one basic feature sorely missing from its API line up. The feature I’m talking about is of course native support for binary. Currently, if you want to manipulate binary in javascript, you have to make do with an array of numbers to store each byte in the “byte array”. This was horribly ineffecient given that each byte of number type probably occupied 4 or 8 bytes, so you would be using 4 or 8 times the space. Another alternative is to use base64, but that meant your binary blob was 33% larger and was only good for serialisation and storage.</p>
<p>This changed however, with the advent of WebGL, the straw that broke the camels back. WebGL required efficient processing of byte arrays which herald the creation of the <a href="http://www.khronos.org/registry/webgl/specs/1.0/#ARRAYBUFFER" target="_blank">ArrayBuffer</a>. Although designed for WebGL, the ArrayBuffer can be used anywhere in your javascript. WebGL is currently available for Firefox 4 and Chrome. The ArrayBuffer allows you to allocate a opaque chunk of memory. To manipulate the buffer, we have to “cast” or map the array to a <a href="http://www.khronos.org/registry/typedarray/specs/1.0/" target="_blank">Typed Array</a>. There are various typed arrays such as Int16Array, Float32Array, but the one that interests us is probably Uint8Array, allowing us to view our ArrayBuffer as a byte array.</p>
<pre>var buf = new ArrayBuffer(1024);
var bytes = new Uint8Array(buf);
for (var i = 0; i &lt; bytes.length; i++) {
  bytes[i] = 0xFF;
}
</pre><div><ol><li>var buf = new ArrayBuffer(1024);</li><li>var bytes = new Uint8Array(buf);</li><li>for (var i = 0; i &lt; bytes.length; i++) {</li><li>  bytes[i] = 0xFF;</li></ol><pre>var buf = new ArrayBuffer(1024);
var bytes = new Uint8Array(buf);
for (var i = 0; i &lt; bytes.length; i++) {
  bytes[i] = 0xFF;
}</pre></div><p>The Typed Array may seem like a foreign concept in a dynamic-typed language such as javascript, but it’s neccesarry to provide good performance for binary handling. If you try to assign a Uint8Array element a number greater than 255, it will be truncated, and if you put a string, it’ll become 0, proving that this is more than just your average JS array.</p>
<p>Already there is talk of using these in HTML File API and Web Sockets API. WebSockets currently only support plain text UTF-8 frames, which means you can’t talk binary over the wire. Given that a lot of exisiting protocols are binary, this was a severely limitation. A web based proxy <a href="https://github.com/kanaka/websockify" target="_blank">websockify</a> that proxies native protocols into websocket frames needs the base64 each frame. Array Buffer support would allow us to do away the base64 overhead.</p>
					
		
		<footer>
			This entry was posted in <a href="https://loune.net/category/uncategorized/" target="_blank">Uncategorized</a> on <a href="https://loune.net/2011/05/javascript-arraybuffer-binary-handling-in-javascript/" title="8:52 pm" target="_blank"><time>May 18, 2011</time></a>.								</footer>
	
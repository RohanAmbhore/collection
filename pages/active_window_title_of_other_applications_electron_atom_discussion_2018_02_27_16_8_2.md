<a href="https://discuss.atom.io/t/active-window-title-of-other-applications/25409/8">https://discuss.atom.io/t/active-window-title-of-other-applications/25409/8</a><div id="articleHeader"><h1>Active window title of other applications</h1></div><div><article id="post_5"><div><div><div><div><p>This may interest you. but mac only</p>
<aside>
  <header>
      <img src="https://assets-cdn.github.com/favicon.ico" width="32" height="32" />
      <a href="https://github.com/octalmage/active-window" target="_blank">GitHub297</a>
  </header>
  <article>
    <img src="https://avatars0.githubusercontent.com/u/142006?s=400&v=4" width="400" height="400" />

<h3><a href="https://github.com/octalmage/active-window" target="_blank">octalmage/active-window</a></h3>

<p>active-window - Get active window title in Node.js.</p>


  </article>
  
  
</aside>
</div></div></div></div></article></div><div><div>1 year later</div></div><div><article id="post_8"><div><div><div><div><p>I know it’s a bit late but you do not need to use C++ for something like this, C# or even VB will do just as nicely:</p>
<pre><code>'Public Declare Function GetActiveWindow Lib "user32" () As System.IntPtr
Public Declare Function GetForegroundWindow Lib "user32" () As System.IntPtr
Public Declare Auto Function GetWindowText Lib "user32" _
        (ByVal hWnd As System.IntPtr, _
        ByVal lpString As System.Text.StringBuilder, _
        ByVal cch As Integer) As Integer
Dim makel As String

Function GetCaption() As String
    ' Create a buffer of 256 characters
    Dim Caption As New System.Text.StringBuilder(256)
    Dim hWnd As IntPtr = GetForegroundWindow()
    GetWindowText(hWnd, Caption, Caption.Capacity)
    Return Caption.ToString()
End Function
</code></pre>
<p>Wrap that in a module of a console application and simply use <code>Console.WriteLine(GetCaption())</code>. When calling the console application from nodejs you can get the stdout of the application and manipulate it how you please <img src="https://discourse-cdn-sjc1.com/business/images/emoji/twitter/slight_smile.png?v=5" alt=":slight_smile:" title=":slight_smile:" /></p>
<p>Now if there is a way to use the user32.dll directly in node.js this would be an even better solution!</p>
<p>Note:</p>
<p>Some beautiful person wrapped these Win32 APIs in a <a href="http://www.vbforums.com/showthread.php?644071-Window-class-for-external-windows" target="_blank">VB Class1</a>.</p></div></div></div></div></article></div><div><article id="post_9"><div><div><div><div><p>Looking further into this for my own purposes, I believe you can do this entirely within NodeJS by now…</p>
<pre><code>npm instal ffi
</code></pre>
<p><strong>UNTESTED:</strong></p>
<pre><code>var FFI = require('ffi');
function TEXT(text){
   return new Buffer(text, 'ucs2').toString('binary');
}

var user32 = new FFI.Library('user32', {
   'GetForegroundWindow': [
      'int32', []
   ],
   'GetWindowText': [
      'int32', ['int32','string','int32']
   ]
});

function getCaption(){
    //Create a buffer of 256 characters
    var caption = ""
    var hWnd = user32. GetForegroundWindow()
    getWindowText(hWnd,var caption,256)
    return TEXT(caption)
}</code></pre></div></div></div></div></article></div><div><div>20 days later</div></div><div><article id="post_10"><div><div><div><div><p><code>active-window</code> is quite broken.</p>
<p>But there’s <a href="https://github.com/sindresorhus/active-win" target="_blank"><strong><code>active-win</code></strong>172</a> now <img src="https://discourse-cdn-sjc1.com/business/images/emoji/twitter/tada.png?v=5" alt=":tada:" title=":tada:" />. With Mac, Linux and Windows support, better behaviour, made to work with Electron, etc.</p>
<hr />
<h2>About <code>active-window</code>
</h2>
<p>I needed this, but the package <code>active-window</code> (linked above) from NPM and GitHub is quite broken and unmantained (there are several unmerged PRs, including some mine).</p>
<p>Some of the problems in the official repo / npm package:</p>
<ul>
<li>It is broken for Mac</li>
<li>After fixing it for Mac, it needs to ask for “assistive technologies permissions”</li>
<li>It is broken for Linux</li>
<li>It always creates a subprocess that keeps running and there’s no way to close if after finishing</li>
<li>That subprocess is a shell process in each platform (PowerShell in Windows), so it’s easy for “Antiviruses” to detect it as “suspicious”</li>
<li>It doesn’t work with Asar packages, so you have to compile the electron app with raw directories for it to work</li>
</ul>
<hr />
<h2>About <code>active-win</code>
</h2>
<p>But there is <a href="https://github.com/sindresorhus/active-win" target="_blank"><strong>active-win</strong>172</a> by <strong>sindresorhus</strong> (if you are building something with Electron you probably already use one of his popular packages).</p>
<ul>
<li>It supports Mac</li>
<li>I recently fixed Linux support</li>
<li>I just added Windows support (32 and 64 bits).</li>
<li>It works out of the box if you use it with tools like the awesome <strong>electron-builder</strong> (it doesn’t break asar packaging, <code>electron-builder</code> can compile it automatically for each platform, etc)</li>
<li>It doesn’t leave processes dangling</li>
<li>It uses the internal OS APIs as much as possible (no “suspicious” shell scripts)</li>
</ul></div></div></div></div></article></div><div><div>4 months later</div></div><div><article id="post_13"><div><div><div><div><p><a href="/u/sancarn" target="_blank">@sancarn</a> Yeah, using node-ffi works, though I had to make some changes:</p>
<pre><code>import ffi from "ffi";
import ref from "ref";

declare var Buffer;

var user32 = new ffi.Library("user32", {
   "GetForegroundWindow": ["int32", []],
   "GetWindowTextA": ["int32", ["int32", "string", "int32"]],
});

export function GetForegroundWindowText() {
	var buffer = new Buffer(256);
	buffer.type = ref.types.CString;
    var handle = user32.GetForegroundWindow();
    let length = user32.GetWindowTextA(handle, buffer, 256);
    return buffer.toString().substr(0, length);
}
</code></pre>
<p>I like this approach the best because it’s the most direct access from JavaScript to the native APIs. If you were going for multiple platforms, a package like active-win above might be best, but for just a few small accesses, using node-ffi to hook into native functions seems the cleanest to me. (and more future proof, since there’s no library you need to understand in order to update it if it has an issue)</p></div></div></div></div></article></div>
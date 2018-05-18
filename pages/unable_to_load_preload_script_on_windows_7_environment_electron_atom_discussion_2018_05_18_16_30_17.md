<a href="https://discuss.atom.io/t/unable-to-load-preload-script-on-windows-7-environment/28607">https://discuss.atom.io/t/unable-to-load-preload-script-on-windows-7-environment/28607</a><div id="articleHeader"><h1>Unable to load preload script on windows 7 environment</h1></div><p>I am trying to launch simple browserwindow using below code in main.js. preload.js script is in the same directory as main.js</p>
<blockquote>
<pre><code>mainWindow = new BrowserWindow({
  'width': width,
  'height': height,
  'max-width': width,
  'max-height': height,
  'fullscreen': false,
  'frame': false,
  'kiosk': false,
  'transparent': true,
  'show': true,
  'resizable': false,
  'node-integration': false,
  'preload':__dirname + '\\preload.js'
});
</code></pre>
</blockquote>
<p>preload script loads fine on OS X machine but shows below error on windows 7 machine.</p>
<blockquote>
<p>C:\Temp\electron\electron-quick-start\node_modules\electron-prebuilt\dist\resources\electron.asar\rendrer\init.js:129 Unable to load preload script C:\Temp\electron\electron-quick-start\preload.js</p>
</blockquote>
<p>I have confirmed that <em>perload.js</em> script exists in <em>C:\Temp\electron\electron-quick-start</em> directory.</p>
<p>Wondering whats going on here?</p>
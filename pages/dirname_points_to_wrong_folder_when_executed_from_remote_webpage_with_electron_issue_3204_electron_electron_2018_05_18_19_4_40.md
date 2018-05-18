<a href="https://github.com/electron/electron/issues/3204">https://github.com/electron/electron/issues/3204</a><div id="articleHeader"><h1>              __dirname points to wrong folder when executed from remote webpage with 'electron .'            #3204    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/romaincointepas" target="_blank">romaincointepas</a>  opened this Issue
        <relative-time>on Oct 25, 2015</relative-time>
        · 3 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      


  
    
      

          <ol>
<li><code>main.js</code> is loading a remote page <code>http://www.example.com/page.html</code> into a <code>BrowserWindow</code> with <code>note-integration: true</code>.</li>
<li><code>page.html</code> loads <code>/static/myscript.js</code> (also a remote script).</li>
<li>Inside <code>myscript.js</code>, I console.log <code>__dirname</code></li>
<li>When running my app by doing <code>electron .</code> (I use <code>electron-prebuilt</code>), __dirname points to <code>node_modules/electron-prebuilt/dist/Electron.app/Contents/Resources/atom.asar/renderer/lib</code>, which does not contain any of my app files (they are in <code>app/</code>).</li>
</ol>
<p>The remote <code>page.html</code> embeds a <code>&lt;webview&gt;</code> with a preload script that is NOT remote (same folder as <code>main.js</code>, let's call it <code>preload-script.js</code>) so I need a way to get the absolute path for <code>preload-script.js</code> to provide to <code>preload</code> (or get the absolute path of the <code>app/</code> folder and append <code>/preload-script.js</code>).</p>
<p>Thanks!</p>
      
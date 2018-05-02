<a href="https://github.com/electron-userland/electron-builder/issues/2269">https://github.com/electron-userland/electron-builder/issues/2269</a><div id="articleHeader"><h1>              Linux AppImage icon does not show up            #2269    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/mobitar" target="_blank">mobitar</a>  opened this Issue
        <relative-time>on Nov 6, 2017</relative-time>
        · 6 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      


  
    
      

          <p>Hello, I've been using electron-builder for about a year now. It's made my life tremendously easier.</p>
<p>Users have reported this issue for a long time, and I thought it was some user error. But no matter what I've tried, I can't get the app icon to show up in any Linux distro. I've tested on Ubuntu and Fedora.</p>
<p>Here is what it shows (bottom):</p>
<p>Root package.json:</p>
<pre><code>  "build": {
    "linux": {
      "category": "Office",
      "icon": "build/icon/",
      "target": [
        "AppImage",
        "deb"
      ]
    }
  }
</code></pre>
<p>My <code>build</code> folder in root:</p>
<pre><code>build/
├── icon
│   └── Icon-512x512.png
├── icon.icns
└── icon.ico
</code></pre>
<p>My app/package.json does not have any icon related metadata. Should it?</p>
<p>Any other info I can share that might be helpful?</p>
<p>Here is the app repo: <a href="https://github.com/standardnotes/desktop/tree/backups" target="_blank">https://github.com/standardnotes/desktop/tree/backups</a></p>
<p>Using electron-builder 19.45.0.</p>
      
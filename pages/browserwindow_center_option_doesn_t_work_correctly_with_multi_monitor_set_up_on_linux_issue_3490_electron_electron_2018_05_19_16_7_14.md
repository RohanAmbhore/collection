<a href="https://github.com/electron/electron/issues/3490">https://github.com/electron/electron/issues/3490</a><div id="articleHeader"><h1>               BrowserWindow - center option doesn't work correctly with multi monitor set-up on Linux            #3490    </h1></div>


  <div>
    
    <div>
        <a href="/petrvecera" target="_blank">petrvecera</a>  opened this Issue
        <relative-time>on Nov 19, 2015</relative-time>
        · 9 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      


  
    
      

          <p>When you have multi monitor set-up and you start <code>BrowserWindow</code> with option center:</p>
<div><pre>new BrowserWindow({width: 800, height: 600, center: true});</pre></div>
<p>The new window is opened in the center of all the monitors, instead of the center of primary one. Basically it counts width of all monitors and put the window in the center of it.</p>
<p>OS: Linux only.<br />
Windows, OS X are fine ( window is opened in the center of main monitor)</p>
<p>Tested with:  Electron 0.35.0, Ubuntu 14.04, Linux Mint 17.2</p>
<p><em>This is pretty annoying when you are showing just a little window.</em><br />
Thanks</p>
      
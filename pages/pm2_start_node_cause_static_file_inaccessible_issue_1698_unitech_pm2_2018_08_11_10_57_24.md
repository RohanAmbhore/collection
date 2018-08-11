<a href="https://github.com/Unitech/pm2/issues/1698">https://github.com/Unitech/pm2/issues/1698</a><div id="articleHeader"><h1>              pm2 start node cause static file inaccessible            #1698    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/morfies" target="_blank">morfies</a>  opened this Issue
        <relative-time>on Oct 17, 2015</relative-time>
        · 3 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          <div>
            




            
<div id="issue-111948477">
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>If I start my express project with pm2, my static files in 'public' directory will become inaccessible.<br />
After some time, I figured out that I had multiple projects with the same 'app.js' file as startup js.</p>
<p>So if I use pm2 to start all these app.js,  all the app name should be 'app', though with different ids,<br />
I suspect pm2 can't distinguish these projects with same names,   because after I changed the app.js to different names, everything went ok</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>

          </div>

          

  


  
<div>
    
  <div>

  




  
<div id="issuecomment-165712628">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>If you do <code>pm2 delete app.js</code> to remove the process from pm2 list, and then <code>pm2 start app.js</code> will solve it too without file renaming. I guess there is some cache persistent between <code>stop</code> and <code>restart/start</code> actions and it messed up somehow.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  


  
<div>
    
  <div>

  




  
<div id="issuecomment-237214097">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I hit this as well, but at least for me, the issue was specifying an incorrect relative path for Express' static files.</p>
<p>In my server, I was serving static files with:</p>
<div><pre>app.use(express.static('public'));</pre></div>
<p>At first, this looks correct. However, this actually directs Express to serve static files out of the <code>public</code> folder that is <em>relative to the working directory</em>.</p>
<p>I was running <code>pm2 start /srv/www/project/server.js</code> from a startup script through Docker, so the working directory was <code>/</code>. The static files were being served out of <code>/public</code> instead of the expected <code>/srv/www/project/public</code>.</p>
<p>Deleting and restarting worked for me, too, but that was because I <code>cd</code>'d to <code>/srv/www/project</code> before running <code>pm2 start server.js</code>. With a working directory of <code>/srv/www/project</code>, everything worked.</p>
<p>In the end, the fix is simple. Use <code>__dirname</code> to ensure the static files are served relative to the script, not the current working directory:</p>
<div><pre>app.use(express.static(__dirname + '/public'));</pre></div>
<p>Express' documentation <a href="https://expressjs.com/en/starter/static-files.html" target="_blank">explains this as well</a>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-357636572">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/schmich" target="_blank">@schmich</a> Thank you for posting your update, even after the issue was closed, I had the exact same problem and your solution works great!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>










        
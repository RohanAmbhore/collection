<a href="https://github.com/electron/electron/issues/5224">https://github.com/electron/electron/issues/5224</a><div id="articleHeader"><h1>              process.env is not preserved to the renderer process            #5224    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/gliheng" target="_blank">gliheng</a>  opened this Issue
        <relative-time>on Apr 20, 2016</relative-time>
        · 5 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-149669392">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <ul>
<li>Electron version: 37.6</li>
<li>Operating system: linux</li>
</ul>
<p>I set some environment variable to process.env in the browser process, then start the renderer process, but I can not get the environment variable I have set on the renderer process.</p>
<p>I tested this on windows and mac, they worked!</p>
<p>Since my app rely on this environment passing to the renderer process, it would be great if the behaviors are the same across different platforms.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-212279369">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Seems a bit strange to use environment variables for communication between processes <g-emoji>👍</g-emoji></p>
<p>But as a temporary workaround you might be able to use <code>remote.getGlobal('process').env</code>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-212391515">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/zcbenz" target="_blank">zcbenz</a>
  

    </strong>

    commented

    <a href="#issuecomment-212391515" target="_blank"><relative-time>on Apr 20, 2016</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>This is unfortunately an expected behavior and we are not able to fix it, you can find more about it in <a href="https://github.com/electron/electron/issues/3306" target="_blank">#3306</a>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-292770427">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          
<p>I am trying to use<code>process.env.TZ = 'America/Managua';</code> in my app<br />
if I give that in main process it is working fine, if I give that in render process no effect.<br />
is there any way to achieve this.<br />
I just need to change the time zone for every request.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-332585403">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>In the rendering process, try using the following:</p>
<p><code>const electron = window.require('electron'); const remote = electron.remote; //... console.log(remote.process.env["TZ"]);</code></p>
<p>Change "TZ" to get other environment variable values.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-332805519">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/dcsw" target="_blank">@dcsw</a> : Thanks for the update.<br />
Already <a href="https://github.com/MarshallOfSound" target="_blank">@MarshallOfSound</a> has clarified this  <a href="https://github.com/electron/electron/issues/9150" target="_blank">#9150</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  
















        


        <div>
              
<div>
  

    
      



      <div>
        
          <div>
  


  
  <div>

    

    

        <p>
    
    
        Attach files by dragging & dropping,
        selecting them, or pasting
        from the clipboard.
    
    
    
    
    
    
    
    
    
  </p>


    
  </div>

  

  


  


          
      




        
      

    
    
  
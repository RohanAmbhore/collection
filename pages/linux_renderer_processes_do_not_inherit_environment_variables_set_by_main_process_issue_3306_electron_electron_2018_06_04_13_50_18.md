<a href="https://github.com/electron/electron/issues/3306">https://github.com/electron/electron/issues/3306</a><div id="articleHeader"><h1>              Linux renderer processes do not inherit environment variables set by main process            #3306    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/joaomoreno" target="_blank">joaomoreno</a>  opened this Issue
        <relative-time>on Nov 3, 2015</relative-time>
        · 1 comment
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-114662716">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>One used to be able to do this from the main process:</p>
<div><pre>process.env['HELLO'] = 'WORLD';</pre></div>
<p>And the <code>HELLO</code> environment variable would exist in every renderer spawned after the fact.</p>
<p>I was able to narrow down when the issue started to appear: <code>0.28.3</code> seems to have changed that behaviour for the Linux releases. Before that, environment inheriting worked.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-153218234">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/zcbenz" target="_blank">zcbenz</a>
  

    </strong>

    commented

    <a href="#issuecomment-153218234" target="_blank"><relative-time>on Nov 3, 2015</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>This is unfortunately expected behavior on Linux, because Chromium uses a zygote process to fork renderer processes instead of forking them directly in parent process.</p>
<p>I tried to fix this by disabling zygote process (<a href="https://github.com/electron/electron/pull/1323" target="_blank">#1323</a>), but it then produced more problems like <a href="https://github.com/electron/electron/issues/1605" target="_blank">#1605</a>, so I have to bring it back (<a href="https://github.com/electron/electron/pull/2014" target="_blank">#2014</a>).</p>
<p>To work around it you can probably read the env from <code>remote.process.env</code>.</p>
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

  

  


  


          
      




        
      

    
    
  
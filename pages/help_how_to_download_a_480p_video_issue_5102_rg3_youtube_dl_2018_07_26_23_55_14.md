<a href="https://github.com/rg3/youtube-dl/issues/5102">https://github.com/rg3/youtube-dl/issues/5102</a><div id="articleHeader"><h1>              Help: How to download a 480p video?            #5102    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/keybounce" target="_blank">keybounce</a>  opened this Issue
        <relative-time>on Mar 2, 2015</relative-time>
        · 1 comment
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div id="issue-59421692">
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I find that very often, I will download a 720p video by default. If I try to ask for a 480p or less, I get 360p.</p>
<p>I understand that youtube only makes 360 and 720p available as a simple mp4, and the rest are broken up into DASH pieces. How can I get a 480p re-assembly of those dash pieces?</p>
<p>Sample request:<br />
youtube-dl  -f "[height &lt;=? 480]" <a href="https://www.youtube.com/watch?v=PxqJvFcvZE4" target="_blank">https://www.youtube.com/watch?v=PxqJvFcvZE4</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div id="issuecomment-76669269">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/phihag" target="_blank">phihag</a>
  

    </strong>

    commented

    <a href="#issuecomment-76669269" target="_blank"><relative-time>on Mar 2, 2015</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>At the moment, DASH videos are not yet offered automatically. You can merge them by hand though:</p>
<pre><code>youtube-dl -f "bestvideo[height&lt;=480][ext=mp4]+bestaudio/[height &lt;=? 480]" PxqJvFcvZE4
</code></pre>
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

  

  


  


          
      




        
      

    
    
  
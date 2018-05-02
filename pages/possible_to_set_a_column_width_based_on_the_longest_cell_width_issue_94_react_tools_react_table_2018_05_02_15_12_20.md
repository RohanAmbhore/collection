<a href="https://github.com/react-tools/react-table/issues/94">https://github.com/react-tools/react-table/issues/94</a><div id="articleHeader"><h1>              Possible to set a column width based on the longest cell width?            #94    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/sshaginyan" target="_blank">sshaginyan</a>  opened this Issue
        <relative-time>on Feb 20, 2017</relative-time>
        · 8 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-208757401">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>How can I make the columns automatically adjust the the longest text a corresponding cell?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-280988125">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <div>You would probably need to do that dynamically by measuring the text
beforehand and adjusting the column width accordingly. Since the text and
table style cannot be consistently measured for every single scenario, this
is likely something that would turn into a plugin instead of a core feature</div>
<a href="#" target="_blank">…</a>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-281167538">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I did something like this. Not great, but it works.</p>
<p>` getColumnWidth (accessor, headerText) {<br />
let {data} = this.state;<br />
let max = 0;</p>
<pre><code>    const maxWidth = 400;
    const magicSpacing = 18;

    for (var i = 0; i &lt; data.length; i++) {
        if (data[i] !== undefined && data[i][accessor] !== null) {
            if (stringify(data[i][accessor] || 'null').length &gt; max) {
                max = stringify(data[i][accessor] || 'null').length;
            }
        }
    }

    return Math.min(maxWidth, Math.max(max, headerText.length) * magicSpacing);
}`
</code></pre>
<p>The last bit ensures the width doesn't go over a universal maximum, and is never smaller than the header text (because that's annoying AF).</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-281169011">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <div>That's exactly what I would have done.</div>
<a href="#" target="_blank">…</a>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  


  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-356547376">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hi <a href="https://github.com/spacedarcy" target="_blank">@spacedarcy</a>, I might ask the stupid question here, but how/where do you use this function ? In ReactTable props or did you build a wrapper around it ?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-356761014">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>A wrapper.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-379358013">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/spacedarcy" target="_blank">@spacedarcy</a> Could you please give a little example? I think i'm kind of miss :S</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-385023344">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Please, <a href="https://github.com/spacedarcy" target="_blank">@spacedarcy</a>, where did you place your code? I'm confused</p>
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

  

  


  


          
      




        
      

    
    
  
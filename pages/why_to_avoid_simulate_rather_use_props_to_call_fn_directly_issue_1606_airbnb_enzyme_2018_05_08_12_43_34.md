<a href="https://github.com/airbnb/enzyme/issues/1606">https://github.com/airbnb/enzyme/issues/1606</a><div id="articleHeader"><h1>              Why to avoid .simulate? Rather use `props` to call fn directly?             #1606    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/antoaravinth" target="_blank">antoaravinth</a>  opened this Issue
        <relative-time>on Apr 6</relative-time>
        · 4 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-311841732">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Well, this is not exactly an issue but a question.</p>
<p>I face the same issue as others had face like:<br />
<a href="https://github.com/airbnb/enzyme/issues/1473" target="_blank">#1473</a><br />
<a href="https://github.com/airbnb/enzyme/issues/1081" target="_blank">#1081</a></p>
<p>Interestingly, most of the comments suggest that:</p>
<blockquote>
<p>avoid .simulate entirely; it's best to invoke your prop function directly.</p>
</blockquote>
<p>Yes, the suggested method works, but I just wanted to understand why that is the case? Is that something enzyme can't do well or enzyme actually uses <code>React.simulate</code> under the hood, which has these problems? Also can't we use <code>dispatchEvent</code> on that element? What your thoughts on this?</p>
<p>Thanks for your time on this.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-380605312">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>My understanding is Jest/enzyme is using JS DOM, which is not real DOM, it has problem mocking browser event.</p>
<p>There is a brief Gotchas section at the end of the <code>simulate</code> API doc,</p>
<blockquote>
<p>Common Gotchas<br />
Currently, event simulation for the shallow renderer does not propagate as one would normally expect in a real environment. As a result, one must call .simulate() on the actual node that has the event handler set.<br />
Even though the name would imply this simulates an actual event, .simulate() will in fact target the component's prop based on the event you give it. For example, .simulate('click') will actually get the onClick prop and call it.</p>
</blockquote>
<p><a href="url" target="_blank">http://airbnb.io/enzyme/docs/api/ShallowWrapper/simulate.html</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-380605974">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>Yes. The problem is that "simulate" doesn't actually simulate anything - it just invokes a prop. So, it's better for your test to explicitly invoke a prop.</p>
</blockquote>
<p>Copied from <a href="url" target="_blank">https://github.com/airbnb/enzyme/issues/1054</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-380680841">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>This seems answered.</p>
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

  

  


  


          
      




        
      

    
    
  
<a href="https://github.com/reduxjs/reselect/issues/304">https://github.com/reduxjs/reselect/issues/304</a><div id="articleHeader"><h1>              mapStateToProps with or without createStructuredSelector            #304    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/dkrutsko" target="_blank">dkrutsko</a>  opened this Issue
        <relative-time>on Dec 1, 2017</relative-time>
        · 5 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-278482461">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hello, I'm sorry if this was answered in the past but I couldn't find anything definitive.</p>
<p>While I understand that we should be using <code>createSelector</code> & <code>createStructuredSelector</code> in our selectors. What about the <code>mapStateToProps</code> function? Should we be using reselect to create that function as well, I've seen people do both. What are the best practices?</p>
<div><pre>const mapStateToProps = createStructuredSelector
({
	A: SomeSelector.a(), // === createSelector (...)
	B: SomeSelector.b(), // === createSelector (...)
	C: SomeSelector.c()  // === createSelector (...)
});</pre></div>
<p>versus</p>
<div><pre>const mapStateToProps = state =&gt;
({
	A: SomeSelectors.a (state), // === createSelector (...)
	B: SomeSelectors.b (state), // === createSelector (...)
	C: SomeSelectors.c (state)  // === createSelector (...)
});</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-348559214">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Those two would be equivalent.  Both result in functions that receive <code>state</code> as a parameter, and use more selector functions to extract data and return an object with the data as fields.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-348578471">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Would there be any performance benefits or would you recommend just not using reselect when mapping state to props?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-348589113">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>We <em>highly</em> recommend using Reselect in general, since memoized selectors cut down on the number of new object/array references being returned from <code>mapState</code> functions.</p>
<p>For much more info on the topic, see:</p>

      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-348594310">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Thank you for your response! I'd like to recommend maybe adding this information to the readme file because at the moment I only see it using reselect in the selectors. Instead you may want to add some examples of using reselect for your containers as well. Please close this if there are no further comments!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-348595128">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I think the answer is that you use Reselect to create the memoized selector functions, but those functions could be used anywhere in the application.  They'd be most commonly used inside your <code>mapState</code> functions, but you could (and probably should) use them anywhere you're interacting with the Redux state tree.  That includes thunks (where you can call <code>getState()</code>), sagas (where you can call <code>yield select(selector)</code>, and even in reducers.</p>
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

  

  


  


          
      




        
      

    
    
  
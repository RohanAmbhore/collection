<a href="https://github.com/apollographql/apollo-client/issues/1680">https://github.com/apollographql/apollo-client/issues/1680</a><div id="articleHeader"><h1>              In case of pagination, how can I refresh all pages?            #1680    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/giroplus" target="_blank">giroplus</a>  opened this Issue
        <relative-time>on May 8, 2017</relative-time>
        · 9 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div id="issue-227032549">
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I am using the latest version of react-apollo with meteor</p>
<p><strong>Intended outcome:</strong><br />
I have a paginated list. I would like to add a reload button to this list. On reloadig, the current data should be erased, and new data should be fetched from the server on all pages of that list.</p>
<p><strong>Actual outcome:</strong><br />
I have tried to trigger <code>.refetch()</code> with this button. But it refetches only the current page. If other pages were visited before the reloading button is triggered, the data of those pages is stored in the store and is not refetched.</p>
<p>Triggering <code>.resetStore()</code> resets the whole store and all queries on the page. Which is obviously an overkill...</p>
<p><strong>My question is:</strong></p>
<p>Am I using <code>.refetch()</code> wrong? What would be the right approach?</p>
<p>Or am I using <code>.resetStore()</code> wrong? Is it possible to reset the store of one specific query?</p>
<p>Thank you!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  


  
<div>
    
  <div>

  




  
<div id="issuecomment-301557340">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>You could use fetchMore and instead of appending data like in the example you could have it replace the property you're changing:<br />
<a href="http://dev.apollodata.com/react/pagination.html#numbered-pages" target="_blank">http://dev.apollodata.com/react/pagination.html#numbered-pages</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div id="issuecomment-301875519">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Please correct me if I am wrong. Since I am not using <code>fetchMore()</code> right now. The results of my queries are not connected to each other, therefore <code>refetch()</code>, refetches only the last query.</p>
<p>Instead, if I start using <code>fetchMore()</code>, the results of the queries will be connected to each other (like get the data of the first, later get the data of the second page and so on...).  In the case of <code>refetch()</code>, the whole result of those queries will be refetched at once? Or only of the data that was fetched last, but the other data will at least be obsolete and discarded and fetched again if needed instead of taking it from the store?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div id="issuecomment-302911707">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/Poincare" target="_blank">Poincare</a>
  

    </strong>

    commented

    <a href="https://github.com/apollographql/apollo-client/issues/1680#issuecomment-302911707" target="_blank"><relative-time>on May 21, 2017</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>The point of <code>fetchMore</code> is that it allows receive some data from your server and then tack it onto existing data in your store. This is generally the "right" way to do pagination.</p>
<p>In this case, you can use <code>fetchMore</code> to fetch each page (i.e. regular pagination) and then fire a single query that just refetches all of the items across each of the pages which can be fired by your reload button.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div id="issuecomment-304385777">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Is <code>fetchMore</code> intended to be used for page-based pagination in the UI? It seems more designed for things like infinite scrolling... looking at the examples, it's not clear how one might implement a more traditional paginated view. I'm talking about this sort of thing:</p>
<p>Note that it's not guaranteed that a user will click "Next" - they might go from Page 1 to Page 5 and then to Page 3.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div id="issuecomment-315523533">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>This issue has been automatically marked as stale becuase it has not had recent activity. It will be closed if no further activity occurs. Thank you for your contributions to Apollo Client!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div id="issuecomment-318834792">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>This issue has been automatically closed because it has not had recent activity after being marked as stale. If you belive this issue is still a problem or should be reopened, please reopen it! Thank you for your contributions to Apollo Client!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div id="issuecomment-320329364">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>fetchMore really a solution for cursor-based pagination rather than offset-based. The example on the Apollo-Client documentation improperly exemplifies this behavior for the offset-based pagination. While fetchMore can be used, it definitely is not the correct solution here. The whole point of offset-based pagination is to minimize the amount of cached data and provide a bit more fine grained control for users, such as paginating through table records whereas fetchMore is a great continuous feed solution when data is streaming in.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div id="issuecomment-335019844">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>so what should I use for offset based pagination?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div id="issuecomment-365886355">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I would like to know too how to do pagination where you can skip pages.</p>
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

  

  


  


          
      




        
      

    
    
  
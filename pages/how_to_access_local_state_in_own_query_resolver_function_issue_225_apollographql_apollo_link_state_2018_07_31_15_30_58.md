<a href="https://github.com/apollographql/apollo-link-state/issues/225">https://github.com/apollographql/apollo-link-state/issues/225</a><div id="articleHeader"><h1>              How to access local state in own Query resolver function?            #225    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/nilshartmann" target="_blank">nilshartmann</a>  opened this Issue
        <relative-time>on Mar 19</relative-time>
        · 4 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div id="issue-306394875">
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          
<p>I have client State that consists of a list of items. Now I'm trying to implement an own Query resolver, that should return exactly one of the items in the list, that is identified by an argument passed (like <code>getItemByXyz(xyz: ...)</code>).</p>
<p>While my resolver is called with the correct argument from the query, I have no idea how to get the current state (my array of items) in the resolver implementation, so that I could find and return the queried item.</p>
<pre><code>const client = new ApolloClient({
  uri: "http://localhost:3000/graphql",
  clientState: {
    defaults: {
      draftMessages: [],
     . . .
    },
    resolvers: {
      Query: {
        getDraftMessageById: (_, { draftMessageId }, { cache }) =&gt; {
         // how to get the current list of draftMessages here?
      },
      Mutation: {
        addDraftMessage: (. . .) =&gt; { }
     }
});
</code></pre>
<p>I think this would be very similiar to adding a <code>getTodoWithId(todoId: ...)</code> Query in your todo example app (<a href="https://github.com/apollographql/apollo-link-state/blob/master/examples/todo/src/resolvers/todos.js" target="_blank">https://github.com/apollographql/apollo-link-state/blob/master/examples/todo/src/resolvers/todos.js</a>)</p>
<p>Can you point me to docs/example how I could implement such a resolver?</p>
<p>Thanks a lot!</p>
<hr />
<p>Maybe related: In the docs on Resolvers (<a href="https://www.apollographql.com/docs/link/links/state.html#default" target="_blank">https://www.apollographql.com/docs/link/links/state.html#default</a>) it says <code>For this query, you will need to specify a resolver for Query.user in your resolver map</code> but unfortunately there is no example how one would implement this specific user resolver...</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div id="issuecomment-375234251">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>You can use the <code>cache.readFragment</code> method to query a specific item in the cache (given that this item is already in the cache, wheter by setting the defaults value or because it was added via mutation) :</p>
<div><pre>const client = new ApolloClient({
  uri: "http://localhost:3000/graphql",
  clientState: {
    defaults: {
      draftMessages: [{
        id: '1',
        content: 'message 1',
        __typename: 'DraftMessage',
      }, {
        id: '2',
        content: 'message 2',
        __typename: 'DraftMessage',
      }],
    },
    resolvers: {
      Query: {
        getDraftMessageById: (_, { draftMessageId }, { cache }) =&gt; {
          const fragment = gql`
            fragment draftMessage on DraftMessage {
              content
            }
          `
          /*
          If you haven't edited the dataObjectFromId config property of your cache instance, the cache id
          is the following as stated in the docs :
          https://www.apollographql.com/docs/link/links/state.html#write-fragment
          */
          const id = `DraftMessage:${draftMessageId}`;
          return cache.readFragment({ fragment, id })
      },
      Mutation: {
        addDraftMessage: (. . .) =&gt; { }
     }
});</pre></div>
<p>I think this issue is best suited for StackOverflow, maybe you should move your question here to make it more visible for other people struggling with this !</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div id="issuecomment-375464014">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          
<p>thanks for your reply, that works! <g-emoji>👍</g-emoji></p>
<p>To get the actual list of draft messages from the local cache (for example to filter by other criterias than the <code>id</code>), I wrote in my resolver:</p>
<div><pre>resolvers: {
  Query: {
    getDraftMessageById: (_, { draftMessageId }, { cache }) =&gt; {
      const allDraftMessagesFromCache = cache.readQuery({
        query: gql`
        query getDraftMessages @client {
          draftMessages {
            id
            text
          }
        }`
   });

   return allDraftMessagesFromCache.find(. . .);
  }
}</pre></div>
<p>Is that correct?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div id="issuecomment-375976281">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Sure, it might work !</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div id="issuecomment-376654541">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/fbartho" target="_blank">fbartho</a>
  

    </strong>

    commented

    <a href="#issuecomment-376654541" target="_blank"><relative-time>on Mar 28</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Closing issue as resolved!</p>
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

  

  


  


          
      




        
      

    
    
  
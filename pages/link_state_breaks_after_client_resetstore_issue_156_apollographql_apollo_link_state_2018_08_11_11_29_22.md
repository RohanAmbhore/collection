<a href="https://github.com/apollographql/apollo-link-state/issues/156">https://github.com/apollographql/apollo-link-state/issues/156</a><div id="articleHeader"><h1>              Link State breaks after client.resetStore()            #156    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/stolinski" target="_blank">stolinski</a>  opened this Issue
        <relative-time>on Jan 2</relative-time>
        · 7 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div id="issue-285321420">
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <h1>Intended outcome</h1>
<p>Calling client.resetStore() after a user logs in or out to reset the entire store. Expected things to work as they do without link state.</p>
<h1>Actual outcome</h1>
<p>All active link state queries throw errors <code>Uncaught (in promise) TypeError: Cannot read property 'todos' of undefined at resolver</code> (where "todos" is the name of the property) and all future mutations on those stop working without a refresh.</p>
<h1>How to reproduce the issue</h1>
<p><a href="https://github.com/stolinski/apollo-link-state-todos-resetStorebug" target="_blank">https://github.com/stolinski/apollo-link-state-todos-resetStorebug</a></p>
<p>Add some todos and click the reset store button. Both todos and visibilityFilter will error out.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div id="issuecomment-354667859">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Full error message here:</p>
<pre><code>index.js:26 Uncaught (in promise) TypeError: Cannot read property 'todos' of undefined
    at resolver (index.js:26)
    at async.js:152
    at step (async.js:53)
    at Object.next (async.js:34)
    at async.js:28
    at new Promise (&lt;anonymous&gt;)
    at __awaiter (async.js:24)
    at executeField (async.js:139)
    at async.js:93
    at step (async.js:53)
    at Object.next (async.js:34)
    at async.js:28
    at new Promise (&lt;anonymous&gt;)
    at __awaiter (async.js:24)
    at execute (async.js:84)
    at Array.map (&lt;anonymous&gt;)
    at async.js:127
    at step (async.js:53)
    at Object.next (async.js:34)
    at async.js:28
    at new Promise (&lt;anonymous&gt;)
    at __awaiter (async.js:24)
    at executeSelectionSet (async.js:76)
    at graphql (async.js:73)
    at Object.next (index.js:46)
    at SubscriptionObserver.next (zen-observable.js:154)
    at zen-observable.js:479
    at new Subscription (zen-observable.js:103)
    at Observable.subscribe (zen-observable.js:229)
    at index.js:38
    at new Subscription (zen-observable.js:103)
    at Observable.subscribe (zen-observable.js:229)
    at dedupLink.js:44
    at new Subscription (zen-observable.js:103)
    at Observable.subscribe (zen-observable.js:229)
    at QueryManager.js:684
    at new Promise (&lt;anonymous&gt;)
    at QueryManager.fetchRequest (QueryManager.js:682)
    at QueryManager.fetchQuery (QueryManager.js:209)
    at ObservableQuery.refetch (ObservableQuery.js:144)
    at QueryManager.js:541
    at Map.forEach (&lt;anonymous&gt;)
    at QueryManager.getObservableQueryPromises (QueryManager.js:534)
    at QueryManager.resetStore (QueryManager.js:527)
    at ApolloClient.resetStore (ApolloClient.js:147)
    at onClick (App.js:9)
    at HTMLUnknownElement.boundFunc (ReactErrorUtils.js:63)
    at Object.ReactErrorUtils.invokeGuardedCallback (ReactErrorUtils.js:69)
    at executeDispatch (EventPluginUtils.js:83)
    at Object.executeDispatchesInOrder (EventPluginUtils.js:106)
</code></pre>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div id="issuecomment-354674263">
    
  <div>

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/ShockiTV" target="_blank">ShockiTV</a>
  

    </strong>

    commented

    <a href="#issuecomment-354674263" target="_blank"><relative-time>on Jan 2</relative-time></a>


    
      <include-fragment>
            
  •


  
    <summary>
      <div>
        
            edited
        
        
      </div>
    </summary>
    
  

      </include-fragment>
    
  </h3>



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Good point. And as <code>defaults</code> are on <code>withClientState</code> level and not cache, we would need to extract this enhancement outside of <code>withClientState</code>.</p>
<p>Our current solution is using cache as argument and not wrap it nor return the instance, so each link would have to mutate the cache object which is just bad architecture.</p>
<p>I would suggest some function like <code>enhanceCache</code> which would return wrapped cache instance and patch it's init and reset functions by calling their default value and also <code>cache.writeData(someObject);</code></p>
<p>Or it will accept array of <code>someObject</code> so we can apply few defaults - also for other links which need some default queries/fragments to be inserted.</p>
<p>Or if we define it's arguments as object in shape like</p>
<pre><code>{
  data: [{someObject},{someObject}],
  write: customWrite
}
</code></pre>
<p>We would enhance it in a way which would allow us to override also these things. For example current official persist link is mutating cache itself and not just wrapping it. This way it could just enhance it in our helper function.</p>
<p>Not sure if we want to prepare some apollo-client or utils function which can be reused, or we prepare just 1 simple enhancer for our usecase. In both cases I would return new instance so it can be chained if needed.</p>
<p>That would let us use default Link cache pointer and not need to provide it as argument.</p>
<pre><code>const cache = new InMemoryCache(...);
// this will also add the .writeData method or we can define another enhancer to do so
const cacheWithDefaults = enahnceLinkStateCache({cache, defaults});

const stateLink = withClientState({
  resolvers: {
    Mutation: {
      updateNetworkStatus: (_, { isConnected }, { cache }) =&gt; {
        const data = {
          networkStatus: { isConnected },
        };
        cache.writeData({ data });
      },
    },
  }
});

const client = new ApolloClient({
  cacheWithDefaults,
  link: ApolloLink.from([
    stateLink,
    new HttpLink()
  ]),
});
</code></pre>
<p>I did not check how adding <code>reset()</code> method to <code>withClientState</code> would behave as it would probably still fail refetch of queries with client part. Not sure how we could possibly schedule it to execute between <code>resetStore()</code> and all observed query refetching. And I consider it the bad architecture :-D</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div id="issuecomment-355125525">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hey <a href="https://github.com/stolinski" target="_blank">@stolinski</a>, thanks for reporting this! This is happening because we need to populate the cache with the defaults again after calling <code>client.resetStore</code>.</p>
<p>Thanks <a href="https://github.com/ShockiTV" target="_blank">@ShockiTV</a> for looking into a possible solution. This use case is tricky since the state link has no way to hook into events orchestrated by the client. <a href="https://github.com/jbaxleyiii" target="_blank">@jbaxleyiii</a> and I have been discussing an events API for Apollo Client that will make these types of problems non-existent in the future.</p>
<p>For now, we've added a hook to the client that will allow you to register callbacks that will be executed after <code>client.resetStore</code>. I'm going to expose the function that writes the defaults on the state link itself so all you'll have to do is call <code>client.onResetStore(stateLink.writeDefaults)</code> after you initialize the client.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  


  
<div>
    
  <div>

  




  
<div id="issuecomment-355787115">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I've updated all version and am using <code>client.onResetStore(stateLink.writeDefaults);</code> but resetStore is still breaking local-state.</p>
<p>You can see this in action with.<br />
<a href="https://github.com/stolinski/apollo-link-state-todos-resetStorebug" target="_blank">https://github.com/stolinski/apollo-link-state-todos-resetStorebug</a></p>
<p>Errors shown are:</p>
<pre><code>VM36321:17 DOMException: Failed to execute 'postMessage' on 'Window': TypeError: Cannot read property 'visibilityFilter' of undefined could not be cloned.
    at ApolloClient.hookLogger [as devToolsHookCb] (&lt;anonymous&gt;:14:14)
    at QueryManager.onBroadcast (http://localhost:3000/static/js/bundle.js:4028:27)
    at QueryManager../node_modules/apollo-client/core/QueryManager.js.QueryManager.broadcastQueries (http://localhost:3000/static/js/bundle.js:5108:14)
    at http://localhost:3000/static/js/bundle.js:4684:31
</code></pre>
<pre><code>ApolloError.js:34 Uncaught (in promise) Error: Network error: Cannot read property 'todos' of undefined
    at new ApolloError (ApolloError.js:34)
    at QueryManager.js:218
</code></pre>
<pre><code>index.js:2177 Unhandled (in react-apollo:Apollo(Link)) Error: Network error: Cannot read property 'visibilityFilter' of undefined
    at new ApolloError (http://localhost:3000/static/js/bundle.js:5670:28)
    at ObservableQuery../node_modules/apollo-client/core/ObservableQuery.js.ObservableQuery.currentResult (http://localhost:3000/static/js/bundle.js:4184:24)
    at GraphQL.dataForChild (http://localhost:3000/static/js/bundle.js:21968:62)
    at GraphQL.render (http://localhost:3000/static/js/bundle.js:22018:33)
    at finishClassComponent (http://localhost:3000/static/js/bundle.js:30538:31)
    at updateClassComponent (http://localhost:3000/static/js/bundle.js:30515:12)
    at beginWork (http://localhost:3000/static/js/bundle.js:30890:16)
    at performUnitOfWork (http://localhost:3000/static/js/bundle.js:32889:16)
    at workLoop (http://localhost:3000/static/js/bundle.js:32953:26)
    at HTMLUnknownElement.callCallback (http://localhost:3000/static/js/bundle.js:23207:14)
    at Object.invokeGuardedCallbackDev (http://localhost:3000/static/js/bundle.js:23246:16)
    at invokeGuardedCallback (http://localhost:3000/static/js/bundle.js:23103:27)
    at renderRoot (http://localhost:3000/static/js/bundle.js:33031:7)
    at performWorkOnRoot (http://localhost:3000/static/js/bundle.js:33679:24)
    at performWork (http://localhost:3000/static/js/bundle.js:33632:7)
    at requestWork (http://localhost:3000/static/js/bundle.js:33543:7)
    at scheduleWorkImpl (http://localhost:3000/static/js/bundle.js:33397:11)
    at scheduleWork (http://localhost:3000/static/js/bundle.js:33354:12)
    at Object.enqueueForceUpdate (http://localhost:3000/static/js/bundle.js:28915:7)
    at GraphQL../node_modules/react/cjs/react.development.js.Component.forceUpdate (http://localhost:3000/static/js/bundle.js:44632:16)
    at GraphQL.forceRenderChildren (http://localhost:3000/static/js/bundle.js:21936:26)
    at next (http://localhost:3000/static/js/bundle.js:21911:27)
    at Object.handleError [as error] (http://localhost:3000/static/js/bundle.js:21915:32)
    at SubscriptionObserver.error (http://localhost:3000/static/js/bundle.js:52186:19)
    at http://localhost:3000/static/js/bundle.js:4423:82
    at Array.forEach (&lt;anonymous&gt;)
    at Object.error (http://localhost:3000/static/js/bundle.js:4423:33)
    at http://localhost:3000/static/js/bundle.js:4742:38
    at http://localhost:3000/static/js/bundle.js:5115:17
    at Array.forEach (&lt;anonymous&gt;)
    at http://localhost:3000/static/js/bundle.js:5114:18
    at Map.forEach (&lt;anonymous&gt;)
    at QueryManager../node_modules/apollo-client/core/QueryManager.js.QueryManager.broadcastQueries (http://localhost:3000/static/js/bundle.js:5109:22)
    at http://localhost:3000/static/js/bundle.js:4684:31
</code></pre>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div id="issuecomment-355787466">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Apparently adding a query of any kind to your state resolvers fixes this. As mergebandit mentioned on Slack. None of the examples or docs show anything about a query being needed. I can't imagine needed a <code>Query: () =&gt; ({}),</code> is the intended functionality though.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div id="issuecomment-390942452">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>How about with <strong>apollo-boost</strong> ?<br />
I'm using <code>apollo-boost^0.1.4</code> what callback should I put in <code>client.onResetStore( ? )</code> since there's no <code>stateLink</code> when configuring with <code>apollo-boost</code></p>
<pre><code>import React, { Component } from 'react'
import Route from './src/components/Route'
import { Platform, AsyncStorage } from 'react-native'
import ApolloClient from 'apollo-boost'
import { ApolloProvider  } from 'react-apollo'
import gql from 'graphql-tag'
import defaults from './src/utils/defaults'

const client = new ApolloClient({
  uri: 'xxxxxl',
  clientState: {
    defaults
  },
  request: async (operation) =&gt; {
    const token = await AsyncStorage.getItem('AUTH_TOKEN');
    operation.setContext({
      headers: {
        authorization: token
      }
    })
  }
})

// client.onResetStore( ? )

const App = _ =&gt; {
  return (
    &lt;ApolloProvider client={client}&gt;
      &lt;Route/&gt;
    &lt;/ApolloProvider&gt;
  )
}
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

  

  


  


          
      




        
      

    
    
  
<a href="https://github.com/apollographql/apollo-link-state/issues/172">https://github.com/apollographql/apollo-link-state/issues/172</a><div id="articleHeader"><h1>              Network error: Cannot read property 'selections' of null            #172    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/ron-liu" target="_blank">ron-liu</a>  opened this Issue
        <relative-time>on Jan 21</relative-time>
        · 2 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/ron-liu" target="_blank">ron-liu</a>
  

    </strong>

    commented

    <a href="#issue-290223003" id="issue-290223003-permalink" target="_blank"><relative-time>on Jan 21</relative-time></a>


    
      <include-fragment>
            
  •


  
    <summary>
      <div>
        
            edited
        
        
      </div>
    </summary>
    
  

      </include-fragment>
    
  </h3>



    

      


  
    
      

          <p>Please check <a href="https://github.com/ron-liu/apollo-link-state-error" target="_blank">this repo</a> for more details.</p>
<div><pre>// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import registerServiceWorker from './registerServiceWorker';
import { InMemoryCache } from 'apollo-cache-inmemory'
import { withClientState } from 'apollo-link-state'
import {ApolloClient} from "apollo-client";
import { ApolloProvider } from 'react-apollo'

const cache = new InMemoryCache()

const stateLink = withClientState({
  cache,
  resolvers: {
    Mutation: {
      openModal: (_, args, { cache }) =&gt; {
        const {name} = args
        cache.writeData({
          modal: {
            name,
            open: true,
            __typename: 'Modal',
          },
        })
        return null
      }
    }
  },
  defaults: {
    modal: {
      __typename: 'Modal',
      open: false,
      name: ''
    }
  }
});

const client = new ApolloClient({
  link: stateLink, 
  cache
})

ReactDOM.render((&lt;ApolloProvider client={client}&gt;&lt;App /&gt;&lt;/ApolloProvider&gt;), document.getElementById('root'));
registerServiceWorker();
</pre></div>
<div><pre>// App.js
import React from 'react';
import gql from 'graphql-tag'
import {graphql} from 'react-apollo'
import {compose} from 'recompose'

const App = ({mutate, data: {modal}}) =&gt; (
  &lt;div&gt;
    &lt;button onClick={() =&gt; mutate({ variables: { name: 'test' }})} &gt;Open&lt;/button&gt;
    &lt;p&gt;modal: open({modal.open || 'false'}), name({modal.name || 'none'})&lt;/p&gt;
  &lt;/div&gt;
)

export default compose(
  graphql(gql`
      query modal {
          modal @client {
              name,
              open
          }
      }
  `),
  graphql(gql`
      mutation openModal  ($name: String!) {
          openModal  (name: $name) @client
      }
  `)

)(App);</pre></div>
<p>When it hits <code>cache.writeData(...)</code>, it will complain:</p>
<pre><code>Uncaught (in promise) Error: Network error: Cannot read property 'selections' of null
    at new ApolloError (ApolloError.js:34)
    at Object.error (QueryManager.js:113)
    at SubscriptionObserver.error (zen-observable.js:174)
    at &lt;anonymous&gt;
</code></pre>
      
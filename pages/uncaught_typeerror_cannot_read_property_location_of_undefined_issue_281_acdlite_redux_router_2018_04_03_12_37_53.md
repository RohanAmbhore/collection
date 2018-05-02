<a href="https://github.com/acdlite/redux-router/issues/281">https://github.com/acdlite/redux-router/issues/281</a><div id="articleHeader"><h1>              Uncaught TypeError: Cannot read property 'location' of undefined            #281    </h1></div>


  <div>
    
    <div>
        <a href="/stefensuhat" target="_blank">stefensuhat</a>  opened this Issue
        <relative-time>on Dec 1, 2016</relative-time>
        · 23 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-192877512">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <h2>Version Latest Version</h2>
<p>History: ^2.1.2<br />
React Router: ^3.0.0</p>
<h2>Steps to reproduce</h2>
<pre><code>    const createStoreWithMiddleware = compose(applyMiddleware(reduxThunk, logger),
    reduxReactRouter({ routes, createHistory }));

const store = createStoreWithMiddleware(createStore)(rootReducer);

ReactDOM.render(
    &lt;Provider store={store}&gt;
        &lt;ReduxRouter&gt;
            &lt;Route path="/"&gt;
                &lt;Route path="login" component={Login} /&gt;
                &lt;Route path="/" component={App}&gt;
                    &lt;IndexRoute component={Welcome} onEnter={RequireAuth} /&gt;
                    &lt;Route path='logout' component={Logout} onEnter={RequireAuth} /&gt;
                &lt;/Route&gt;
            &lt;/Route&gt;
        &lt;/ReduxRouter&gt;
    &lt;/Provider&gt;
    , document.querySelector('.main')
);
</code></pre>
<h2>Actual Behavior</h2>
<p>When I ran my code it return me <code>Uncaught TypeError: Cannot read property 'location' of undefined</code></p>
<p>any solution?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  


          

          

  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-264210471">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Your version of history (3.x) is unsupported. Downgrading to 2.x should work. See <a href="https://github.com/acdlite/redux-router/issues/259" target="_blank">#259</a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-264212539">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/mjrussell" target="_blank">@mjrussell</a> I've downgrade my history <code>"history": "^2.0.0",</code> but still show same error.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-264764763">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Hm I dont know then, I would have to see a runnable example. Most likely a configuration error though. Are you doing server side rendering? Hash history doesn't work in SSR.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-265255341">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I've run into this issue with history@3 as well. I tried reverting to history@2 but that then produces the error <code>history.getCurrentLocation is not a function</code>. Tried to work out what was happening myself, but too many libraries I'm not very familiar with. I created a <a href="https://github.com/hobenkr88/redux-router-basic-example" target="_blank">repo</a> based on the "basic example" to try and get anyone else up and running who might be more capable of looking into this.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-265277986">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Thanks for creating the example. I'll try to look this week/weekend.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-266075396">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>@ssuhat <a href="https://github.com/hobenkr88" target="_blank">@hobenkr88</a> Try downgrading <code>react-router</code> from <code>3.x</code> to <code>2.x</code> with <code>history</code> version <code>2.x</code>.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-266168638">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/supasate" target="_blank">@supasate</a> sorry can't try that. I can't do any major changes anymore.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-266169726">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Technically React Router 3 is API backwards compatible with React Router 2. Redux-Router relies on some internals of React Router and this may be the source of the issue. But downgrading React Router from 3.x to 2.x shouldnt affect your code</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-267637649">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I can confirm that using <code>react-router</code> v2.8.1 fixes this problem.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-286663329">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>v3.0.0 is working no issues</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-286982353">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>+1<br />
<a href="https://cloud.githubusercontent.com/assets/7343395/23986688/043863ce-0a58-11e7-8912-3534e3ce7ef4.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/7343395/23986688/043863ce-0a58-11e7-8912-3534e3ce7ef4.png" alt="image" /></div></a><br />
I have same issue from react-router v4.0</p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-293928588">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>npm install react-router@3.0.5</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-294057133">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Thanks for the help! I wonder if there's an open issue for this problem</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-294453395">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I have upgraded my react router to 4.1.1, and history 4.6.1  and I am facing same issue</p>
<p>Uncaught TypeError: Cannot read property 'location' of undefined<br />
at new Router (Router.js:31)</p>
<p>Without changing version, is it possible to fix in the code?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-296599276">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I'm having the same issue as <a href="https://github.com/KalpanaPagariya" target="_blank">@KalpanaPagariya</a>. This is my <code>store.jsx</code> file:</p>
<pre><code>import { createStore, applyMiddleware, compose } from 'redux';
import { routerMiddleware } from 'react-router-redux';
import thunk from 'redux-thunk';
import createHistory from 'history/createBrowserHistory';
import rootReducer from './reducers/index';

// Create a history of your choosing (we're using a browser history in this case)
const history = createHistory({ basename: '/lighthouse' });

// Build the middleware for intercepting and dispatching navigation actions
const middleware = routerMiddleware(history);

const store = createStore(rootReducer, compose(applyMiddleware(middleware), applyMiddleware(thunk), window.devToolsExtension
  ? window.devToolsExtension()
  : f =&gt; f));

export default store;
</code></pre>
<p>And my routes:</p>
<pre><code>ReactDOM.render(
  &lt;Provider store={store}&gt;
    &lt;Router
      onUpdate={() =&gt; {
        window.scrollTo(0, 0);
        logPageView();
      }} history={history}
    &gt;
      &lt;Route path="/" component={App}&gt;
        &lt;IndexRoute component={Home} /&gt;
        &lt;Route path="/favourites" component={Cards} type="favourites" /&gt;
        &lt;Route path="/inbox" component={Cards} type="inbox" /&gt;
        &lt;Route path="/insights" component={Insight} /&gt;
        &lt;Route path="*" component={NotFound} /&gt;
      &lt;/Route&gt;
    &lt;/Router&gt;
  &lt;/Provider&gt;, document.getElementById('react-root'));
</code></pre>
<p><a href="https://cloud.githubusercontent.com/assets/1721288/25331732/60e19cee-28e4-11e7-8978-6d8fc254af34.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/1721288/25331732/60e19cee-28e4-11e7-8978-6d8fc254af34.png" alt="screen shot 2017-04-24 at 11 51 20" /></div></a></p>
<p><a href="https://cloud.githubusercontent.com/assets/1721288/25332500/fc8da5aa-28e6-11e7-860a-18497316de85.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/1721288/25332500/fc8da5aa-28e6-11e7-860a-18497316de85.png" alt="screen shot 2017-04-24 at 12 09 58" /></div></a></p>
<p>Can anyone provide the correct working versions for <code>react-router, react-router-redux and history</code>?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-296606441">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>If I apply the middleware like this <code>const store = createStore(rootReducer, compose(applyMiddleware(middleware, thunk)</code>, then I get this error:</p>
<p><code>Router.js?a4aa:87 Uncaught TypeError: Cannot read property 'getCurrentLocation' of undefined</code></p>
<p><a href="https://cloud.githubusercontent.com/assets/1721288/25332693/b5c58dbc-28e7-11e7-8cf0-308af004c829.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/1721288/25332693/b5c58dbc-28e7-11e7-8cf0-308af004c829.png" alt="screen shot 2017-04-24 at 12 15 16" /></div></a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-297676161">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/mjrussell" target="_blank">@mjrussell</a> <a href="https://github.com/Scarysize" target="_blank">@Scarysize</a> any idea of how can I fix the issue? thanks</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-297962084">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I've fixed the <code>location of undefined</code> issue by adding <code>export</code> to the history const. But then I had to downgrade the <code>history</code> library to <code>3.3.0</code> and then now I get this error: <code>Uncaught Error: Cannot find module "history/createBrowserHistory"</code>. So I think I will revert everything back to the old versions :/</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  




</div>

  
<div>
      <div>
        <h3 id="ref-issue-215337281">
      
        
      
        <img src="https://avatars0.githubusercontent.com/u/20559021?s=60&v=4" width="16" height="16" alt="@wlfsmile" />
  <a href="/wlfsmile" target="_blank">wlfsmile</a>
  

      referenced this issue
        in <strong>Jikewang-Studio/2015-weekly</strong>
      <a href="#ref-issue-215337281" target="_blank">
        <relative-time>on Jun 4, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Open
    



    
      <h4>
        <a href="/Jikewang-Studio/2015-weekly/issues/1" target="_blank">
          周报—吴林霏—前端
          #1
        </a>
      </h4>
    

    


  

</div>

  <div>
        <h3 id="ref-issue-233880114">
      
        
      
        <img src="https://avatars2.githubusercontent.com/u/1087001?s=60&v=4" width="16" height="16" alt="@mzlock" />
  <a href="/mzlock" target="_blank">mzlock</a>
  

      referenced this issue
        in <strong>vigetlabs/microcosm</strong>
      <a href="#ref-issue-233880114" target="_blank">
        <relative-time>on Jun 6, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/vigetlabs/microcosm/issues/344" target="_blank">
          Quick Start - limit React Router version
          #344
        </a>
      </h4>
    

    

  
    1 of 6 tasks complete
    
      
    
  

  

</div>


</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-312553335">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>csillag thanks a lot <g-emoji>👍</g-emoji><br />
actually downgrade to 2.8.1 and it worked</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-334978101">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Downgrading to react-router@2.8.1 and history@2.0.0 works but the following warning occurs<br />
Warning: [react-router] <code>Router</code> no longer defaults the history prop to hash history. Please use the <code>hashHistory</code> singleton instead. <a href="http://tiny.cc/router-defaulthistory" target="_blank">http://tiny.cc/router-defaulthistory</a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-340635384">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Downgrading won't work with React 16 as <code>prop-types</code> is no longer included in React</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>










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

  

  


  
</div>

          
      </div>

</div>


        </div>
      </div>

    </div>
    
  
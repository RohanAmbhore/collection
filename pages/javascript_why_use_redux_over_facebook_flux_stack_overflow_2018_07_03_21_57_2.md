<a href="https://stackoverflow.com/questions/32461229/why-use-redux-over-facebook-flux">https://stackoverflow.com/questions/32461229/why-use-redux-over-facebook-flux</a><div id="articleHeader"><h1>Why use Redux over Facebook Flux?</h1></div>

            

<div id="question">

    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        983
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="Click to mark as favorite question (click again to undo)" target="_blank">favorite</a>
        <div><b>523</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I've read <a href="https://stackoverflow.com/questions/32021763/what-could-be-the-downsides-of-using-redux-instead-of-flux" target="_blank">this answer</a>, <a href="http://redux.js.org/docs/recipes/ReducingBoilerplate.html" target="_blank">reducing boilerplate</a>, looked at few GitHub examples and even tried redux a little bit (todo apps). </p>

<p>As I understand, <a href="http://redux.js.org/docs/introduction/Motivation.html" target="_blank">official redux doc motivations</a> provide pros comparing to traditional MVC architectures. BUT it doesn't provide an answer to the question: </p>

<p><strong>Why you should use Redux over Facebook Flux?</strong> </p>

<p><em>Is that only a question of programming styles: functional vs non-functional? Or the question is in abilities/dev-tools that follow from redux approach? Maybe scaling? Or testing?</em></p>

<p><em>Am I right if I say that redux is a flux for people who come from functional languages?</em> </p>

<p><strong>To answer this question you may compare complexity of implementation redux's motivation points on flux vs redux.</strong></p>

<p>Here are motivation points from <a href="http://redux.js.org/docs/introduction/Motivation.html" target="_blank">official redux doc motivations</a>:</p>

<ol>
<li>Handling optimistic updates (<em>as I understand, it hardly depends on 5th point. Is it hard to implement it in fb flux?</em>)</li>
<li>Rendering on the server (<em>fb flux also can do this. Any benefits comparing to redux?</em>)</li>
<li>Fetching data before performing route transitions (<em>Why it can't be achieved in fb flux? What's the benefits?</em>)</li>
<li>Hot reload (<em>It's possible with <a href="http://gaearon.github.io/react-hot-loader/" target="_blank">React Hot Reload</a>. Why do we need redux?</em>)</li>
<li>Undo/Redo functionality</li>
<li>Any other points? Like persisting state...</li>
</ol>
    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-32920459">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1775
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>Redux author here!  </p>

<p>Redux is not <em>that</em> different from Flux. Overall it has same architecture, but Redux is able to cut some complexity corners by using functional composition where Flux uses callback registration.</p>

<p>There is not a fundamental difference in Redux, but I find it makes certain abstractions easier, or at least possible to implement, that would be hard or impossible to implement in Flux.</p>

<h2>Reducer Composition</h2>

<p>Take, for example, pagination. My <a href="https://github.com/gaearon/flux-react-router-example" target="_blank">Flux + React Router example</a> handles pagination, but the code for that is awful. One of the reasons it's awful is that <strong>Flux makes it unnatural to reuse functionality across stores.</strong> If two stores need to handle pagination in response to different actions, they either need to inherit from a common base store (bad! you're locking yourself into a particular design when you use inheritance), or call a function from the handler, which will need to somehow operate on the Flux store's private state. The whole thing is messy (although definitely in the realm of possible).</p>

<p>On the other hand, with Redux pagination is natural thanks to reducer composition. It's reducers all the way down, so you can write a <a href="https://github.com/reactjs/redux/blob/ecb1bb453a60408543f5760bba0aa4c767650ba2/examples/real-world/reducers/paginate.js" target="_blank">reducer factory that generates pagination reducers</a> and then <a href="https://github.com/reactjs/redux/blob/ecb1bb453a60408543f5760bba0aa4c767650ba2/examples/real-world/reducers/index.js#L29-L46" target="_blank">use it in your reducer tree</a>. The key to why it's so easy is because <strong>in Flux, stores are flat, but in Redux, reducers can be nested via functional composition, just like React components can be nested.</strong></p>

<p>This pattern also enables wonderful features like no-user-code <a href="https://github.com/omnidan/redux-undo" target="_blank">undo/redo</a>. <strong>Can you imagine plugging Undo/Redo into a Flux app being two lines of code? Hardly. With Redux, it is</strong>—again, thanks to reducer composition pattern. I need to highlight there's nothing new about it—this is the pattern pioneered and described in detail in <a href="https://github.com/evancz/elm-architecture-tutorial/" target="_blank">Elm Architecture</a> which was itself influenced by Flux.</p>

<h2>Server Rendering</h2>

<p>People have been rendering on the server fine with Flux, but seeing that we have 20 Flux libraries each attempting to make server rendering “easier”, perhaps Flux has some rough edges on the server. The truth is Facebook doesn't do much server rendering, so they haven't been very concerned about it, and rely on the ecosystem to make it easier.</p>

<p>In traditional Flux, stores are singletons. This means it's hard to separate the data for different requests on the server. Not impossible, but hard. This is why most Flux libraries (as well as the new <a href="https://facebook.github.io/flux/docs/flux-utils.html" target="_blank">Flux Utils</a>) now suggest you use classes instead of singletons, so you can instantiate stores per request.</p>

<p>There are still the following problems that you need to solve in Flux (either yourself or with the help of your favorite Flux library such as <a href="https://github.com/acdlite/flummox" target="_blank">Flummox</a> or <a href="https://github.com/goatslacker/alt" target="_blank">Alt</a>):</p>

<ul>
<li>If stores are classes, how do I create and destroy them with dispatcher per request? When do I register stores?</li>
<li>How do I hydrate the data from the stores and later rehydrate it on the client? Do I need to implement special methods for this?</li>
</ul>

<p>Admittedly Flux frameworks (not vanilla Flux) have solutions to these problems, but I find them overcomplicated. For example, <a href="http://acdlite.github.io/flummox/docs/api/store" target="_blank">Flummox asks you to implement <code>serialize()</code> and <code>deserialize()</code> in your stores</a>. Alt solves this nicer by providing <a href="http://alt.js.org/docs/takeSnapshot/" target="_blank"><code>takeSnapshot()</code></a> that automatically serializes your state in a JSON tree.</p>

<p>Redux just goes further: <strong>since there is just a single store (managed by many reducers), you don't need any special API to manage the (re)hydration.</strong> You don't need to “flush” or “hydrate” stores—there's just a single store, and you can read its current state, or create a new store with a new state. Each request gets a separate store instance. <a href="http://redux.js.org/docs/recipes/ServerRendering.html" target="_blank">Read more about server rendering with Redux.</a></p>

<p>Again, this is a case of something possible both in Flux and Redux, but Flux libraries solve this problem by introducing a ton of API and conventions, and Redux doesn't even have to solve it because it doesn't have that problem in the first place thanks to conceptual simplicity.</p>

<h2>Developer Experience</h2>

<p>I didn't actually intend Redux to become a popular Flux library—I wrote it as I was working on my <a href="http://youtube.com/watch?v=xsSnOQynTHs" target="_blank">ReactEurope talk on hot reloading with time travel</a>. I had one main objective: <strong>make it possible to change reducer code on the fly or even “change the past” by crossing out actions, and see the state being recalculated.</strong></p>

<p><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/a0d66cf145fe35cbe5fb341494b04f277d5d85dd/687474703a2f2f692e696d6775722e636f6d2f4a34476557304d2e676966" /></div></p>

<p>I haven't seen a single Flux library that is able to do this. React Hot Loader also doesn't let you do this—in fact it breaks if you edit Flux stores because it doesn't know what to do with them.</p>

<p>When Redux needs to reload the reducer code, it calls <a href="http://redux.js.org/docs/api/Store.html#replaceReducer" target="_blank"><code>replaceReducer()</code></a>, and the app runs with the new code. In Flux, data and functions are entangled in Flux stores, so you can't “just replace the functions”. Moreover, you'd have to somehow re-register the new versions with the Dispatcher—something Redux doesn't even have.</p>

<h2>Ecosystem</h2>

<p>Redux has a <a href="https://github.com/xgrommx/awesome-redux" target="_blank">rich and fast-growing ecosystem</a>. This is because it provides a few extension points such as <a href="http://redux.js.org/docs/advanced/Middleware.html" target="_blank">middleware</a>. It was designed with use cases such as <a href="https://github.com/fcomb/redux-logger" target="_blank">logging</a>, support for <a href="https://github.com/acdlite/redux-promise" target="_blank">Promises</a>, <a href="https://github.com/acdlite/redux-rx" target="_blank">Observables</a>, <a href="https://github.com/reactjs/react-router-redux" target="_blank">routing</a>, <a href="https://github.com/leoasis/redux-immutable-state-invariant" target="_blank">immutability dev checks</a>, <a href="https://github.com/elgerlambert/redux-localstorage/" target="_blank">persistence</a>, etc, in mind. Not all of these will turn out to be useful, but it's nice to have access to a set of tools that can be easily combined to work together.</p>

<h2>Simplicity</h2>

<p>Redux preserves all the benefits of Flux (recording and replaying of actions, unidirectional data flow, dependent mutations) and adds new benefits (easy undo-redo, hot reloading) without introducing Dispatcher and store registration.</p>

<p>Keeping it simple is important because it keeps you sane while you implement higher-level abstractions.</p>

<p>Unlike most Flux libraries, Redux API surface is tiny. If you remove the developer warnings, comments, and sanity checks, it's <a href="https://gist.github.com/gaearon/ffd88b0e4f00b22c3159" target="_blank">99 lines</a>. There is no tricky async code to debug.</p>

<p>You can actually read it and understand all of Redux.</p>

<hr />

<p>See also <a href="https://stackoverflow.com/a/32916602/458193" target="_blank">my answer on downsides of using Redux compared to Flux</a>.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-32742821">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        50
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>You might be best starting with reading this post by Dan Abramov where he discusses various implementations of Flux and their trade-offs at the time he was writing redux:
<a href="https://medium.com/@dan_abramov/the-evolution-of-flux-frameworks-6c16ad26bb31" target="_blank">The Evolution of Flux Frameworks</a></p>

<p>Secondly that motivations page you link to does not really discuss the motivations of Redux so much as the motivations behind Flux (and React). The <a href="https://redux.js.org/docs/introduction/ThreePrinciples.html" target="_blank">Three Principles</a> is more Redux specific though still does not deal with the implementation differences from the standard Flux architecture.</p>

<p>Basically, Flux has multiple stores that compute state change in response to UI/API interactions with components and broadcast these changes as events that components can subscribe to. In Redux, there is only one store that every component subscribes to. IMO it feels at least like Redux further simplifies and unifies the flow of data by unifying (or reducing, as Redux would say) the flow of data back to the components - whereas Flux concentrates on unifying the other side of the data flow - view to model.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-34613221">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        22
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I'm an early adopter and implemented a mid-large single page application using the Facebook Flux library.</p>

<p>As I'm a little late to the conversation I'll just point out that despite my best hopes Facebook seem to consider their Flux implementation to be a proof of concept and it has never received the attention it deserves.</p>

<p>I'd encourage you to play with it, as it exposes more of the inner working of the Flux architecture which is quite educational, but at the same time it does not provide many of the benefits that libraries like Redux provide (which aren't that important for small projects, but become very valuable for bigger ones).</p>

<p>We have decided that moving forward we will be moving to Redux and I suggest you do the same ;)</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 5 '16 at 13:45
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-42952362">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        72
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong><a href="https://www.quora.com/Should-I-choose-Redux-or-Flux-for-ReactJS/answer/Daniel-Turan-2?srid=d6mq" target="_blank">In Quora, somebody says</a>:</strong> </p>

<blockquote>
  <p>First of all, it is totally possible to write apps with React without
  Flux.</p>
</blockquote>

<p>Also this <strong>visual diagram</strong> which I've created show a quick view of both, probably a quick answer for the people which don't want to read the whole explanation:
<a href="https://i.stack.imgur.com/HbS0b.jpg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/HbS0b.jpg" alt="Flux vs Redux" /></div></a></p>

<p>But if you still interested knowing more, read on.</p>

<blockquote>
  <p>I believe you should start with pure React, then learn Redux and Flux.
  After you will have some REAL experience with React, you will see
  whether Redux is helpful for you or not.</p>
  
  <p>Maybe you will feel that Redux is exactly for your app and maybe you
  will find out, that Redux is trying to solve a problem you are not
  really experiencing.</p>
  
  <p>If you start directly with Redux, you may end up with over-engineered
  code, code harder to maintain and with even more bugs and than without
  Redux.</p>
</blockquote>

<p>From <a href="https://github.com/reactjs/redux/blob/master/docs/introduction/Motivation.md" target="_blank">Redux docs</a>:</p>

<blockquote>
  <p><strong>Motivation</strong> <br /> As the requirements for JavaScript single-page applications have become increasingly complicated, our
  code must manage more state than ever before. This state can include
  server responses and cached data, as well as locally created data that
  has not yet been persisted to the server. UI state is also increasing
  in complexity, as we need to manage active routes, selected tabs,
  spinners, pagination controls, and so on.</p>
  
  <p>Managing this ever-changing state is hard. If a model can update
  another model, then a view can update a model, which updates another
  model, and this, in turn, might cause another view to update. At some
  point, you no longer understand what happens in your app as you have
  lost control over the when, why, and how of its state. When a system
  is opaque and non-deterministic, it's hard to reproduce bugs or add
  new features.</p>
  
  <p>As if this wasn't bad enough, consider the new requirements becoming
  common in front-end product development. As developers, we are
  expected to handle optimistic updates, server-side rendering, fetching
  data before performing route transitions, and so on. We find ourselves
  trying to manage a complexity that we have never had to deal with
  before, and we inevitably ask the question: Is it time to give up? The
  answer is No.</p>
  
  <p>This complexity is difficult to handle as we're mixing two concepts
  that are very hard for the human mind to reason about: mutation and
  asynchronicity. I call them Mentos and Coke. Both can be great when
  separated, but together they create a mess. Libraries like React
  attempt to solve this problem in the view layer by removing both
  asynchrony and direct DOM manipulation. However, managing the state of
  your data is left up to you. This is where Redux comes in.</p>
  
  <p>Following in the footsteps of Flux, CQRS, and Event Sourcing, Redux
  attempts to make state mutations predictable by imposing certain
  restrictions on how and when updates can happen. These restrictions
  are reflected in the three principles of Redux.</p>
</blockquote>

<p>Also from <a href="https://github.com/reactjs/redux/blob/master/docs/introduction/CoreConcepts.md" target="_blank">Redux docs</a>:</p>

<blockquote>
  <p><strong>Core Concepts</strong><br /> Redux itself is very simple.</p>
  
  <p>Imagine your app's state is described as a plain object. For example,
  the state of a todo app might look like this:</p>

<pre><code>{
  todos: [{
    text: 'Eat food',
    completed: true
  }, {
    text: 'Exercise',
    completed: false
  }],
  visibilityFilter: 'SHOW_COMPLETED'
}</code></pre>
  
  <p>This object is like a "model" except that there are no setters. This
  is so that different parts of the code can’t change the state
  arbitrarily, causing hard-to-reproduce bugs.</p>
  
  <p>To change something in the state, you need to dispatch an action. An
  action is a plain JavaScript object (notice how we don't introduce any
  magic?) that describes what happened. Here are a few example actions:</p>

<pre><code>{ type: 'ADD_TODO', text: 'Go to swimming pool' }
{ type: 'TOGGLE_TODO', index: 1 }
{ type: 'SET_VISIBILITY_FILTER', filter: 'SHOW_ALL' }</code></pre>
  
  <p>Enforcing that every change is described as an action lets us have a
  clear understanding of what’s going on in the app. If something
  changed, we know why it changed. Actions are like breadcrumbs of what
  has happened. Finally, to tie state and actions together, we write a
  function called a reducer. Again, nothing magic about it — it's just a
  function that takes state and action as arguments, and returns the
  next state of the app. It would be hard to write such a function for a
  big app, so we write smaller functions managing parts of the state:</p>

<pre><code>function visibilityFilter(state = 'SHOW_ALL', action) {
  if (action.type === 'SET_VISIBILITY_FILTER') {
    return action.filter;
  } else {
    return state;
  }
}

function todos(state = [], action) {
  switch (action.type) {
  case 'ADD_TODO':
    return state.concat([{ text: action.text, completed: false }]);
  case 'TOGGLE_TODO':
    return state.map((todo, index) =&gt;
      action.index === index ?
        { text: todo.text, completed: !todo.completed } :
        todo
   )
  default:
    return state;
  }
}</code></pre>
  
  <p>And we write another reducer that manages the complete state of our
  app by calling those two reducers for the corresponding state keys:</p>

<pre><code>function todoApp(state = {}, action) {
  return {
    todos: todos(state.todos, action),
    visibilityFilter: visibilityFilter(state.visibilityFilter, action)
  };
}</code></pre>
  
  <p>This is basically the whole idea of Redux. Note that we haven't used
  any Redux APIs. It comes with a few utilities to facilitate this
  pattern, but the main idea is that you describe how your state is
  updated over time in response to action objects, and 90% of the code
  you write is just plain JavaScript, with no use of Redux itself, its
  APIs, or any magic.</p>
</blockquote>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-43474951">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        13
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Here is the simple explanation of Redux over Flux.
Redux does not have a dispatcher.It relies on pure functions called reducers. It does not need a dispatcher. Each actions are handled by one or more reducers to update the single store. Since data is immutable, reducers returns a new updated state that updates the store<a href="https://i.stack.imgur.com/uaoem.jpg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/uaoem.jpg" alt="enter image description here" /></div></a></p>

<p>For more information <a href="http://www.prathapkudupublog.com/2017/04/flux-vs-redux.html" target="_blank">http://www.prathapkudupublog.com/2017/04/flux-vs-redux.html</a></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-48442877">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I worked quite a long time with Flux and now quite a long time using Redux. As Dan pointed out both architectures are not so different. The thing is that Redux makes the things simpler and cleaner. It teaches you a couple of things on top of Flux. Like for example Flux is a perfect example of one-direction data flow. Separation of concerns where we have data, its manipulations and view layer separated. In Redux we have the same things but we also learn about immutability and pure functions.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 25 at 12:26
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-51007725">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong><a href="https://github.com/facebook/flux" target="_blank">Flux</a> is a pattern and <a href="https://github.com/reduxjs/redux" target="_blank">Redux</a> is a library.</strong></p>

<p>Flux is a fancy name for the observer pattern modified a little bit to fit React, but Facebook released a few tools to aid in implementing the Flux pattern, so the following is the difference between using these tools (which is commonly referred to as using Flux) and using Redux.</p>

<p>Both Flux and Redux have actions. Actions can be compared to events (or what trigger events). In Flux, an action is a simple JavaScript object, and that’s the default case in Redux too, but when using Redux middleware, actions can also be functions and promises.</p>

<p>With Flux it is a convention to have multiple stores per application; each store is a singleton object. In Redux, the convention is to have a single store per application, usually separated into data domains internally (you can create more than one Redux store if needed for more complex scenarios).</p>

<p>Flux has a single dispatcher and all actions have to pass through that dispatcher. It’s a singleton object. A Flux application cannot have multiple dispatchers. This is needed because a Flux application can have multiple stores and the dependencies between those stores need a single manager, which is the dispatcher.</p>

<p>Redux has no dispatcher entity. Instead, the store has the dispatching process baked in. A Redux store exposes a few simple API functions, one of them is to dispatch actions.</p>

<p>In Flux, the logic of what to do on the data based on the received action is written in the store itself. The store also has the flexibility of what parts of the data to expose publicly. The smartest player in a Flux app is the store.</p>

<p>In Redux, the logic of what to do on the data based on the received actions is in the reducer function that gets called for every action that gets dispatched (through the store API). A store can’t be defined without a reducer function. A Redux reducer is a simple function that receives the previous state and one action, and it returns the new state based on that action. In a Redux app, you can split your reducer into simpler functions as you would do with any other function. The smartest player in Redux is the reducer.</p>

<p>In Redux, also, there isn’t a lot of flexibility about what to expose as the store’s state. Redux will just expose whatever returned from the store’s reducer. This is one constraint.</p>

<p>The other bigger constraint is that the store’s state cannot be mutable (or really, shouldn’t be). There is no such constraint in Flux, you can mutate the state as you wish. The state’s immutability, in Redux, is achieved easily by making the reducers pure functions (with no side effects). Redux reducers always copy the state they receive and returns a modified version of the state’s copy, not the original object itself. While this is a big constraint, it makes life much easier long term.</p>
    </div>
    
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/reactjs" title="show questions tagged 'reactjs'" target="_blank">reactjs</a> <a href="/questions/tagged/reactjs-flux" title="show questions tagged 'reactjs-flux'" target="_blank">reactjs-flux</a> <a href="/questions/tagged/flux" title="show questions tagged 'flux'" target="_blank">flux</a> <a href="/questions/tagged/redux" title="show questions tagged 'redux'" target="_blank">redux</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
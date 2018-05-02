<a href="https://stackoverflow.com/questions/41357897/understanding-compose-functions-in-redux">https://stackoverflow.com/questions/41357897/understanding-compose-functions-in-redux</a><div id="articleHeader"><h1>Understanding compose functions in redux</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        13
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>6</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I was trying to create a store in redux for which I am currently using following syntax:-</p>

<pre><code>const middlewares = [
  thunk,
  logger
]

const wlStore = createStore(
  rootReducer,
  initialState
  compose(applyMiddleware(...middlewares))
)
</code></pre>

<p>The above works fine for me and I can access the store, but I lately I bumped into another syntax:-</p>

<pre><code>const wlStore=applyMiddleware(thunk,logger)(createStore)(rootReducer)
</code></pre>

<p>Both of them seem to be doing the same job.</p>

<p>Is there any reason because of which I should prefer one over another? Pros/Cons?</p>
    </div>
    
    <div>
    

    <div>
        <div>
    <div>
        asked Dec 28 '16 at 8:07
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-41359312">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        38
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p><strong>Improved readability and convenience are the main advantages of using compose.</strong></p>

<p><em>Compose</em> is used when you want to pass multiple store enhancers to the store. Store enhancers are higher order functions that add some extra functionality to the store. The only store enhancer which is supplied with Redux by default is <em>applyMiddleware</em> however many other are available.</p>

<p><strong>Store Enhancers are Higher Order Functions</strong></p>

<p>What are higher order functions? Paraphrased from the <a href="http://learnyouahaskell.com/higher-order-functions" target="_blank">Haskell docs</a>:</p>

<blockquote>
  <p>Higher order functions can take functions as parameters and return functions as return
  values. A function that does either of those is called a higher order
  function</p>
</blockquote>

<p>From the Redux docs:</p>

<blockquote>
  <p>All compose does is let you write deeply nested function transformations without the rightward drift of the code. Don’t give it too much credit!</p>
</blockquote>

<p>So when we chain our higher order functions (store enhancers) instead of having to write</p>

<pre><code>func1(func2(func3(func4))))
</code></pre>

<p>we could just write </p>

<pre><code>compose(func1, func2, func3, func4)
</code></pre>

<p>These two lines of code do the same thing. It is only the syntax which differs.</p>

<p><strong>Redux Example</strong></p>

<p>From the <a href="https://paulkogel.gitbooks.io/redux-docs/content/docs/api/compose.html" target="_blank">Redux docs</a> if we don't use <em>compose</em> we would have</p>

<pre><code>finalCreateStore = applyMiddleware(middleware)(
      require('redux-devtools').devTools()(
       require('redux-devtools').persistState(window.location.href.match(/[?&]debug_session=([^&]+)\b/))()
     )
     )(createStore);
</code></pre>

<p>Whereas if we use <em>compose</em></p>

<pre><code>finalCreateStore = compose(
    applyMiddleware(...middleware),
    require('redux-devtools').devTools(),
    require('redux-devtools').persistState(
      window.location.href.match(/[?&]debug_session=([^&]+)\b/)
    )
  )(createStore);
</code></pre>

<p>To read more about Redux's compose function <a href="https://paulkogel.gitbooks.io/redux-docs/content/docs/api/compose.html" target="_blank">click here</a></p>
    </div>
    
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    




<div id="post-editor">

    <div> 
        <div>
            <div id="mdhelp">
    <ul id="mdhelp-tabs">
        <li>Links</li>
        <li>Images</li>
        <li>Styling/Headers</li>
        <li>Lists</li>
        <li>Blockquotes</li>
        
        
        <li><a href="/editing-help" target="_blank">advanced help »</a></li>
    </ul>
    
    

    
    
    

    

    

    

    
</div>
            
        </div>
    </div>

    
    

    

    


    
    
    



</div>

                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/redux" title="show questions tagged 'redux'" target="_blank">redux</a> <a href="/questions/tagged/react-redux" title="show questions tagged 'react-redux'" target="_blank">react-redux</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
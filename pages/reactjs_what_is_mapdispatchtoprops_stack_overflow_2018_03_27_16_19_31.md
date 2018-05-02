<a href="https://stackoverflow.com/questions/39419237/what-is-mapdispatchtoprops">https://stackoverflow.com/questions/39419237/what-is-mapdispatchtoprops</a><div id="articleHeader"><h1>What is mapDispatchToProps?</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        178
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="Click to mark as favorite question (click again to undo)" target="_blank">favorite</a>
        <div><b>79</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I was reading the documentation for the Redux library and it has this example,</p>

<blockquote>
  <p>In addition to reading the state, container components can dispatch actions. In a similar fashion, you can define a function called <code>mapDispatchToProps()</code> that receives the dispatch() method and returns callback props that you want to inject into the presentational component.</p>
</blockquote>

<p>This actually makes no sense. Why do you need <code>mapDispatchToProps</code> when you already have <code>mapStateToProps</code>? </p>

<p>They also provide this handy code sample:</p>

<pre><code>const mapDispatchToProps = (dispatch) =&gt; {
  return {
    onTodoClick: (id) =&gt; {
      dispatch(toggleTodo(id))
    }
  }
}
</code></pre>

<p>Can someone please explain in laymen's terms what this function is and why it is useful?</p>
    </div>
    
    
</div>

                
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-40068198">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        323
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>I feel like none of the answers have crystallized why <code>mapDispatchToProps</code> is useful.</p>

<p>This can really only be answered in the context of the <code>container-component</code> pattern, which I found best understood by first reading:</p>

<p><a href="https://medium.com/@learnreact/container-components-c0e67432e005#.1a9j3w1jl" target="_blank">https://medium.com/@learnreact/container-components-c0e67432e005#.1a9j3w1jl</a></p>



<p><a href="http://redux.js.org/docs/basics/UsageWithReact.html" target="_blank">http://redux.js.org/docs/basics/UsageWithReact.html</a></p>

<p>In a nutshell, your <code>components</code> are supposed to be concerned only with displaying stuff.   The <strong>only place they are supposed to get information from is their props</strong>.</p>

<p>Separated out from this is the concern about:</p>

<ul>
<li>how you get the stuff to display, </li>
<li>and how you handle events.  </li>
</ul>

<p>That is what <code>containers</code> are for.</p>

<p>Therefore, a "well designed" <code>component</code> in the pattern look like this:</p>

<pre><code>class FancyAlerter extends Component {
    sendAlert = () =&gt; {
        this.props.sendTheAlert()
    }

    render() {
        &lt;div&gt;
          &lt;h1&gt;Today's Fancy Alert is {this.props.fancyInfo}&lt;/h1&gt;
          &lt;Button onClick={sendAlert}/&gt;
        &lt;/div&gt;
     }}
</code></pre>

<p>See how this component gets the info it displays from props (which came from the redux store via <code>mapStateToProps</code>) and it also gets its action function from its props: <code>sendTheAlert()</code>.</p>

<p>That's where <code>mapDispatchToProps</code> comes in: in the corresponding <code>container</code></p>

<p><code>FancyButtonContainer.js</code></p>

<pre><code>function mapDispatchToProps(dispatch) {
    return({
        sendTheAlert: () =&gt; {dispatch(ALERT_ACTION)}
    })
}

function mapStateToProps(state} {
    return({fancyInfo: "Fancy this:" + state.currentFunnyString})
}

export const FancyButtonContainer = connect(
    mapStateToProps, mapDispatchToProps)(
    FancyAlerter
)
</code></pre>

<p>I wonder if you can see, now that it's the <code>container</code> [1] that knows about redux and dispatch and store and state and ... stuff.</p>

<p>The <code>component</code> in the pattern, <code>FancyAlerter</code>, which does the rendering doesn't need to know about any of that stuff: it gets its method to call at <code>onClick</code> of the button, via its props.</p>

<p>And ... <code>mapDispatchToProps</code> was the useful means that redux provides to let the container easily pass that function into the wrapped component on its props.</p>

<p>All this looks very like the todo example in docs, and another answer here, but I have tried to cast it in the light of the pattern to emphasize <strong>why</strong>.</p>

<p>(Note: you can't use <code>mapStateToProps</code> for the same purpose as <code>mapDispatchToProps</code> for the basic reason that you don't have access to <code>dispatch</code> inside <code>mapStateToProp</code>.  So you couldn't use <code>mapStateToProps</code> to give the wrapped component a method that uses <code>dispatch</code>.   </p>

<p>I don't know why they chose to break it into two mapping functions - it might have been tidier to have <code>mapToProps(state, dispatch, props)</code>   IE one function to do both!</p>

<hr />

<p><em>[1]  Note that I deliberately explicitly named the container <code>FancyButtonContainer</code>,  to highlight that it is a "thing" - the identity (and hence existence!) of the container as "a thing" is sometimes lost in the shorthand</em> </p>

<p><code>export default connect(...)</code> </p>

<p><em>syntax that is shown in most examples</em></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-39419474">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        30
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>It's basically a shorthand. So instead of having to write:</p>

<pre><code>this.props.dispatch(toggleTodo(id));
</code></pre>

<p>You would use mapDispatchToProps as shown in your example code, and then elsewhere write:</p>

<pre><code>this.props.onTodoClick(id);
</code></pre>

<p>or more likely in this case, you'd have that as the event handler:</p>

<pre><code>&lt;MyComponent onClick={this.props.onTodoClick} /&gt;
</code></pre>

<hr />

<p>There's a helpful video by Dan Abramov on this here: <a href="https://egghead.io/lessons/javascript-redux-generating-containers-with-connect-from-react-redux-visibletodolist" target="_blank">https://egghead.io/lessons/javascript-redux-generating-containers-with-connect-from-react-redux-visibletodolist</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Sep 9 '16 at 20:47
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-39419536">
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
<p><code>mstp</code> receives the <code>state</code> and <code>props</code> and allows you to extract props from the state to pass to the component.</p>

<p><code>mdtp</code> receives <code>dispatch</code> and <code>props</code> and is meant for you to bind action creators to dispatch so when you execute the resulting function the action gets disptached.</p>

<p>I find this only saves you from having to do <code>dispatch(actionCreator())</code> within your component thus making it a bit easier to read.</p>

<p><a href="https://github.com/reactjs/react-redux/blob/master/docs/api.md#arguments" target="_blank">https://github.com/reactjs/react-redux/blob/master/docs/api.md#arguments</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Sep 9 '16 at 20:52
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-39423836">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        4
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>mapStateToProps, mapDispatchToProps and connect from react-redux library provides a convenient way to access your state and dispatch function of your store. So basically connect is a higher order component, you can also thing as a wrapper if this make sense for you. So every time your state is changed mapStateToProps will be called with your new state and subsequently as you props update component will run render function to render your component in browser. mapDispatchToProps also stores key-values on the props of your component, usually they take a form of a function. In such way you can trigger state change from your component onClick, onChange events.</p>

<p>From docs:</p>

<pre><code>const TodoListComponent = ({ todos, onTodoClick }) =&gt; (
  &lt;ul&gt;
    {todos.map(todo =&gt;
      &lt;Todo
        key={todo.id}
        {...todo}
        onClick={() =&gt; onTodoClick(todo.id)}
      /&gt;
    )}
  &lt;/ul&gt;
)

const mapStateToProps = (state) =&gt; {
  return {
    todos: getVisibleTodos(state.todos, state.visibilityFilter)
  }
}

const mapDispatchToProps = (dispatch) =&gt; {
  return {
    onTodoClick: (id) =&gt; {
      dispatch(toggleTodo(id))
    }
  }
}

function toggleTodo(index) {
  return { type: TOGGLE_TODO, index }
}

const TodoList = connect(
  mapStateToProps,
  mapDispatchToProps
)(TodoList) 
</code></pre>

<p>Also make sure that you are familiar with <a href="https://facebook.github.io/react/docs/reusable-components.html#stateless-functions" target="_blank">React stateless functions</a> and <a href="https://medium.com/@dan_abramov/mixins-are-dead-long-live-higher-order-components-94a0d2f9e750#.8hdi3n2wx" target="_blank">Higher-Order Components</a></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-42572170">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        25
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><code>mapStateToProps()</code> is a utility which helps your component get updated state(which is updated by some other components),<br />
<code>mapDispatchToProps()</code> is a utility which will help your component to fire an action event (dispatching action which may cause change of application state)</p>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/reactjs" title="show questions tagged 'reactjs'" target="_blank">reactjs</a> <a href="/questions/tagged/redux" title="show questions tagged 'redux'" target="_blank">redux</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
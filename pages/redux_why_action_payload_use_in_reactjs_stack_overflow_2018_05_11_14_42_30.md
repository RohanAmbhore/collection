<a href="https://stackoverflow.com/questions/49725708/why-action-payload-use-in-reactjs">https://stackoverflow.com/questions/49725708/why-action-payload-use-in-reactjs</a><div id="articleHeader"><h1>why action.payload use in reactjs</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        1
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>1</b></div>


</div>

            </div>

            
<div>
    <div>

<p><code>action.payload</code> is called when,where and why?? Please anyone help me to understand what is the actual use of action.payload.I already searched so many siteS, but I doesn't get it.. </p>
    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-49726630">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>When you are handling a request the say onclick of an element we need to update the state</p>

<p>In that case we will use like this</p>

<pre><code>&lt;div onClick={this.props.handleClick()} &gt;
</code></pre>

<p>this handleClick will be described in the actions, where we will create an action creator
each action creator contains an action and payload which contains the data we need to pass to the reducers.</p>

<p>A sample action creator will look like the following</p>

<p>const data = 'sample data here'</p>

<p>return {
  type: 'SELECT_ACCOUNT',
  payload: data
}</p>

<p>On the reducers inside the switch case we will handle the action type and update the app mapStateToProps
Example shown below</p>

<p>case SELECT_ACCOUNT:
  return {
    ...state,
    selected : action.payload
 };</p>

<p>Hope this will help you to get a basic idea </p>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/reactjs" title="show questions tagged 'reactjs'" target="_blank">reactjs</a> <a href="/questions/tagged/redux" title="show questions tagged 'redux'" target="_blank">redux</a> <a href="/questions/tagged/react-redux-form" title="show questions tagged 'react-redux-form'" target="_blank">react-redux-form</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
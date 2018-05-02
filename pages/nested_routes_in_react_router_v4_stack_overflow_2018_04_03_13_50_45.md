<a href="https://stackoverflow.com/questions/42095600/nested-routes-in-react-router-v4">https://stackoverflow.com/questions/42095600/nested-routes-in-react-router-v4</a><div id="articleHeader"><h1>Nested Routes in React Router v4</h1></div>

            

<div id="question">

    
        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        49
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>13</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I'm trying to set up some nested routes to add a common layout. Check the code out:</p>

<pre><code>  &lt;Router&gt;
    &lt;Route component={Layout}&gt;
      &lt;div&gt;
        &lt;Route path='/abc' component={ABC} /&gt;
        &lt;Route path='/xyz' component={XYZ} /&gt;
      &lt;/div&gt;
    &lt;/Route&gt;
  &lt;/Router&gt;
</code></pre>

<p>While this works perfectly fine, I still get the warning:</p>

<blockquote>
  <p>Warning: You should not use &lt;Route component&gt; and &lt;Route children&gt; in the same
  route;  will be ignored</p>
</blockquote>
    </div>
    
    
</div>

                
    <div>
	    

        <div id="comments-link-42095600">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </div>        </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-42723446">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        60
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>CESCO's answer renders first the component <code>AppShell</code> <strong>then</strong> one of the components inside  <code>Switch</code>. But these components are NOT going to render inside <code>AppShell</code>, they will NOT be children of <code>AppShell</code>.</p>

<p>In v4 to wrap components you don't put anymore your <code>Route</code>s inside another <code>Route</code>, you put your <code>Route</code>s directly inside a component.<br />
I.E : for the wrapper instead of <code>&lt;Route component={Layout}&gt;</code> you directly use <code>&lt;Layout&gt;</code>.</p>

<p>Full code :</p>

<pre><code>  &lt;Router&gt;
    &lt;Layout&gt;
      &lt;Route path='/abc' component={ABC} /&gt;
      &lt;Route path='/xyz' component={XYZ} /&gt;
    &lt;/Layout&gt;
  &lt;/Router&gt;
</code></pre>

<p>The change is probably explained by the idea to make React Router v4 to be pure 
React so you only use React elements like with any other React element.</p>

<p>EDIT : I removed the <code>Switch</code> component as it's not useful here. See when it's useful <a href="https://github.com/ReactTraining/react-router/blob/master/packages/react-router/docs/api/Switch.md" target="_blank">here</a>.</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-42723446">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>4</b> more comments</a>
        </div>         
    </div>    </div>
</div>

  

<div id="answer-42278734">
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
<p>You need to use the switch component to nesting to work nice. Also, see this <a href="https://stackoverflow.com/questions/42254929/how-to-nest-routes-in-react-router-v4" target="_blank">question</a></p>

<pre><code>// main app
&lt;div&gt;
    // not setting a path prop, makes this always render
    &lt;Route component={AppShell}/&gt;
    &lt;Switch&gt;
        &lt;Route exact path="/" component={Login}/&gt;
        &lt;Route path="/dashboard" component={AsyncDashboard(userAgent)}/&gt;
        &lt;Route component={NoMatch}/&gt;
    &lt;/Switch&gt;
&lt;/div&gt;
</code></pre>

<p>And version-4 components do not take children, instead, you should use the render prop.</p>

<pre><code>&lt;Router&gt;
    &lt;Route render={(props)=&gt;{
      return &lt;div&gt;Whatever&lt;/div&gt;}&gt;
    &lt;/Route&gt;
  &lt;/Router&gt;
</code></pre>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-42278734">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-42542992">
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


<pre><code>&lt;Router&gt;
    &lt;Layout&gt;
        &lt;Route path='/abc' component={ABC} /&gt;
        &lt;Route path='/xyz' component={XYZ} /&gt;
    &lt;/Layout&gt;
&lt;/Router&gt;
</code></pre>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-42542992">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-45798729">
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
<p>If you do not want <code>Layout</code> to run at loaded. Use this method:</p>

<pre><code>&lt;div className="container"&gt;
    &lt;Route path="/main" component={ChatList}/&gt;
    &lt;Switch&gt;
        &lt;Route exact path="/" component={Start} /&gt;
        &lt;Route path="/main/single" component={SingleChat} /&gt;
        &lt;Route path="/main/group" component={GroupChat} /&gt;
        &lt;Route path="/login" component={Login} /&gt;
    &lt;/Switch&gt;
&lt;/div&gt;
</code></pre>

<p>Whenever history changes, <strong>componentWillReceiveProps</strong> in the ChatList will run.</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-45798729">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-48040884">
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
<p>You can also try this :</p>

<pre><code>&lt;Route exact path="/Home"
                 render={props=&gt;(
                                 &lt;div&gt;
                                      &lt;Layout/&gt;
                                      &lt;Archive/&gt;
                                &lt;/div&gt;
                       )} 
    /&gt;
</code></pre>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-48040884">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            <div>
                                
                                            <div>
        
                <div>
                    <div>
                        <h3>Sign up or <a href="/users/login?ssrc=question_page&returnurl=https%3a%2f%2fstackoverflow.com%2fquestions%2f42095600%2fnested-routes-in-react-router-v4%23new-answer" id="login-link" target="_blank">log in</a></h3>
                        
                        <div>
                             Sign up using Google
                        </div>
                        <div>
                             Sign up using Facebook
                        </div>
                        <div>
                             Sign up using Email and Password
                        </div>
                    </div>
                    
                    
                    
                    
                    <div>
                                <h3>Post as a guest</h3>
    <div>
        <table>
        <tbody><tr>
                    <td>
                <div>
                    <label>Name</label>
                    
                </div>
                <div>
                    <label>Email</label>
                    
                </div>
            </td>
        </tr>
        </tbody></table>
    </div>

                    </div>
                </div>
            </div>
            
            

                            </div>

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>

<p>
By posting your answer, you agree to the <a href="https://stackexchange.com/legal/privacy-policy" name="privacy" target="_blank">privacy policy</a> and <a href="https://stackexchange.com/legal/terms-of-service" name="tos" target="_blank">terms of service</a>.</p>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/react-router" title="show questions tagged 'react-router'" target="_blank">react-router</a> <a href="/questions/tagged/react-router-v4" title="show questions tagged 'react-router-v4'" target="_blank">react-router-v4</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
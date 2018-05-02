<a href="https://stackoverflow.com/questions/42672842/how-to-get-history-on-react-router-v4">https://stackoverflow.com/questions/42672842/how-to-get-history-on-react-router-v4</a><div id="articleHeader"><h1>How to get history on react-router v4?</h1></div>

            

<div id="question">

    
        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        37
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>20</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I having some little issue migrating from React-Router v3 to v4.
in v3 I was able to do this anywhere:</p>

<pre><code>import { browserHistory } from 'react-router';
browserHistory.push('/some/path');
</code></pre>

<p>How do I achieve this in v4.</p>

<p>I know that I could use, the hoc <code>withRouter</code>, react context, or event router props when you are in a Component. but it is not the case for me.</p>

<p>I am looking for the equivalence of <a href="https://github.com/ReactTraining/react-router/blob/ab4552d2ea0ec5c0cf3c534bca654a1af3ea0dec/docs/guides/NavigatingOutsideOfComponents.md" target="_blank">NavigatingOutsideOfComponents</a> in v4</p>
    </div>
    
    
</div>

                
    <div>
	    

        <div id="comments-link-42672842">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </div>        </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-42679052">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        74
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>You just need to have a module that exports a <code>history</code> object. Then you would import that object throughout your project.</p>

<pre><code>// history.js
import { createBrowserHistory } from 'history'

export default createBrowserHistory({
  /* pass a configuration object here if needed */
})</code></pre>

<p>Then, instead of using one of the built-in routers, you would use the <code>&lt;Router&gt;</code> component.</p>

<pre><code>// index.js
import { Router } from 'react-router-dom'
import history from './history'
import App from './App'

ReactDOM.render((
  &lt;Router history={history}&gt;
    &lt;App /&gt;
  &lt;/Router&gt;
), holder)</code></pre>

<pre><code>// some-other-file.js
import history from './history'
history.push('/go-here')</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 8 '17 at 18:25
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-42679052">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>5</b> more comments</a>
        </div>         
    </div>    </div>
</div>

  

<div id="answer-44754061">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        23
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>This works!
<a href="https://reacttraining.com/react-router/web/api/withRouter" target="_blank">https://reacttraining.com/react-router/web/api/withRouter</a></p>

<pre><code>import { withRouter } from 'react-router-dom';

class MyComponent extends React.Component {
  render () {
    this.props.history;
  }
}

withRouter(MyComponent);
</code></pre>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-44754061">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-46143522">
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
<p>If you are using redux and redux-thunk the best solution will be using <a href="https://github.com/ReactTraining/react-router/tree/master/packages/react-router-redux" target="_blank">react-router-redux</a></p>

<pre><code>// then, in redux actions for example
import { push } from 'react-router-redux'

dispatch(push('/some/path'))
</code></pre>

<blockquote>
  <p>It's important to see the docs to do some configurations.</p>
</blockquote>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-46143522">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-48369370">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Similiary to accepted answer what you could do is use <code>react</code> and <code>react-router</code> itself to provide you <code>history</code> object which you can scope in a file and then export.</p>

<p><strong>history.js</strong></p>

<pre><code>import React from 'react';
import { withRouter } from 'react-router';

// variable which will point to react-router history
let globalHistory = null;

// component which we will mount on top of the app
class Spy extends React.Component {
  componentWillMount() {
    const { history } = this.props;
    globalHistory = history; 
  }

  componentWillReceiveProps(nextProps) {
    globalHistory = nextProps.history;
  }

  render(){
    return null;
  }
}

export const GlobalHistory = withRouter(Spy);

// export react-router history
export default function getHistory() {    
  return globalHistory;
}</code></pre>

<p>You later then import Component and mount to initialize history variable:</p>

<pre><code>import { BrowserRouter } from 'react-router-dom';
import { GlobalHistory } from './history';

function render() {
  ReactDOM.render(
    &lt;BrowserRouter&gt;
        &lt;div&gt;
            &lt;GlobalHistory /&gt;
            //.....
        &lt;/div&gt;
    &lt;/BrowserRouter&gt;
    document.getElementById('app'),
  );
}</code></pre>

<p>And then you can just import in your app when it has been mounted:</p>

<pre><code>import getHistory from './history'; 

export const goToPage = () =&gt; (dispatch) =&gt; {
  dispatch({ type: GO_TO_SUCCESS_PAGE });
  getHistory().push('/success'); // at this point component probably has been mounted and we can safely get `history`
};</code></pre>

<p>I even made and <a href="https://www.npmjs.com/package/react-router-global-history" target="_blank">npm package</a> that does just that.</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-48369370">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-44197539">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>In the specific case of <code>react-router</code>, using <a href="https://facebook.github.io/react/docs/context.html" target="_blank"><code>context</code></a> is a valid case scenario, e.g.</p>

<pre><code>class MyComponent extends React.Component {
  props: PropsType;

  static contextTypes = {
    router: PropTypes.object
  };

  render () {
    this.context.router;
  }
}
</code></pre>

<p>You can access an instance of the history via the router context, e.g. <code>this.context.router.history</code>.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 26 '17 at 8:57
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-44197539">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            <div>
                                
                                            <div>
        
                <div>
                    <div>
                        <h3>Sign up or <a href="/users/login?ssrc=question_page&returnurl=https%3a%2f%2fstackoverflow.com%2fquestions%2f42672842%2fhow-to-get-history-on-react-router-v4%23new-answer" id="login-link" target="_blank">log in</a></h3>
                        
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/reactjs" title="show questions tagged 'reactjs'" target="_blank">reactjs</a> <a href="/questions/tagged/react-router" title="show questions tagged 'react-router'" target="_blank">react-router</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
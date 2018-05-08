<a href="https://stackoverflow.com/questions/31024639/unit-testing-react-component-that-makes-ajax-calls-using-jest">https://stackoverflow.com/questions/31024639/unit-testing-react-component-that-makes-ajax-calls-using-jest</a><div id="articleHeader"><h1>Unit testing react component that makes ajax calls using JEST</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        8
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>3</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I've a react component that makes AJAX call in <code>componentDidMount</code> method. While I try to render it using <code>React.addons.TestUtils</code>, the component gets rendered without making AJAX call. How would I test react component using jest so that it makes AJAX call? Should I need to use phantomJS (or browser like env) as well to provide DOM abilities to react component?</p>

<p><strong>React Component:</strong></p>

<pre><code>return React.createClass({

  componentDidMount : function() {
    $.ajax({
    ... makes http request
    })
  }

  render : function() {
    &lt;div&gt;
      //view logic based on ajax response...
    &lt;/div&gt;
  }
});</code></pre>

<p><strong>TestCase:</strong></p>

<pre><code>jest.dontMock(../MyComponent);

var React = require('react/addons');

var TestUtils = React.addons.TestUtils;

var MyComponent = require(../MyComponent);

describe('Sample Test', function(){     

    it('To Render the component', function() {

       var component = &lt;MyComponent /&gt;;

       var DOM = TestUtils.renderIntoDocument(component);

       .... // Some other code... 
       });
})</code></pre>


    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-31028901">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        11
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I really like <a href="http://sinonjs.org/" target="_blank">Sinon.js</a> and its ability to create a fake server that can respond to ajax requests for testing purposes.  You can use it alongside Jest just fine.  Here's an example of what it can do for you:</p>

<pre><code>describe('MyComponent', function() {     

    it('successfully makes ajax call and renders correctly', function() {
        //create fake server
        var server = sinon.fakeServer.create();
        //make sure that server accepts POST requests to /testurl
        server.respondWith('POST', '/testurl', 'foo'); //we are supplying 'foo' for the fake response
        //render component into DOM
        var component = &lt;MyComponent /&gt;;
        var DOM = TestUtils.renderIntoDocument(component);
        //allow the server to respond to queued ajax requests
        server.respond();
        //expectations go here
        //restore native XHR constructor
        server.restore();
    });

});</code></pre>

<p>I'm not sure how open you are to including another framework in your test suite so feel free to ignore this answer if it does not suit your purposes.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jun 24 '15 at 14:09
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-31084501">
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
<p>Since your $.ajax is mocked by jest, you are not getting the expected behavor, because you are not getting real $.ajax function in runtime. </p>

<p>You need to mock your $.ajax function such that it changes the state of the react component. You can refer this <a href="https://facebook.github.io/jest/docs/tutorial.html" target="_blank">jest</a> post for details. Use </p>

<div>
<div>
<pre><code>$.ajax.mock.calls</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jun 27 '15 at 2:20
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-40159636">
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
<p>If you only need to mock http requests, you can also use <a href="https://github.com/node-nock/nock" target="_blank">nock</a>. Sinon is great, but comes with a lot of additional functionality that you may not need.</p>

<pre><code>describe('MyComponent', function() {     
  it('successfully makes ajax call and renders correctly', function() {
    // mocks a single post request to example.com/testurl
    var server = nock('http://example.com')
      .post('/testurl')
      .reply(200, 'foo');

    var component = &lt;MyComponent /&gt;;
    var DOM = TestUtils.renderIntoDocument(component);
  });
});</code></pre>

<p>Note that you should probably call <code>nock.cleanAll()</code> after each test so that any failures or lingering mocks don't mess up the next test.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 20 '16 at 16:20
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-40345706">
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
<p>This is a late answer, but two of the answers involve mocking servers, which can be overkill in some cases, and the answer that actually talks about <code>$.ajax.calls</code> leads to a broken link, so I'll give a brief explanation of the simpler way to do it.</p>

<p>jest will mock the $.ajax call, which means <code>$.ajax.calls[0][0]</code> will contain the intercepted $.ajax call. You can then access the success or error callbacks of the call and call them directly, eg <code>$.ajax.calls[0][0].success(/* Returned data here. */)</code>.</p>

<p>Then you can proceed normally with testing the results of your ajax call.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 31 '16 at 15:47
    </div>
    
    
</div>
    </div>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/ajax" title="show questions tagged 'ajax'" target="_blank">ajax</a> <a href="/questions/tagged/unit-testing" title="show questions tagged 'unit-testing'" target="_blank">unit-testing</a> <a href="/questions/tagged/reactjs" title="show questions tagged 'reactjs'" target="_blank">reactjs</a> <a href="/questions/tagged/jestjs" title="show questions tagged 'jestjs'" target="_blank">jestjs</a> <a href="/questions/tagged/reactjs-testutils" title="show questions tagged 'reactjs-testutils'" target="_blank">reactjs-testutils</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
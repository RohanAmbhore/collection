<a href="https://stackoverflow.com/questions/45191742/expressjs-how-to-catch-all-route-parameters-even-if-unknown">https://stackoverflow.com/questions/45191742/expressjs-how-to-catch-all-route-parameters-even-if-unknown</a><div id="articleHeader"><h1>expressjs: How to catch all route parameters even if unknown?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        1
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>1</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>Lets say I have this route.</p>

<pre><code>this.app.use('/app/fileasset/ui.html/:view*?', function(req,res) {});
</code></pre>

<p>If I have this url: /app/fileasset/ui.html <strong>/test/view</strong></p>

<p>Then I can catch them in req.params ==&gt; req.params[0] (root url, 'test') and req.params.view ('view')</p>

<p>The question is: how can I catch an unknown numbers of parameters ?</p>

<p>For example: /app/fileasset/ui.html <strong>/test/view/subview/wtv</strong></p>

<p>How to get 'subview' and 'wtv' in req.params ? and having the same route to catch longer url with unknown number of params ?</p>

<p>thanks in advance</p>
    </div>
    
    <table>
    <tbody><tr>
    <td>
        
    </td>
    <td>
        <div>
    <div>
        asked Jul 19 '17 at 13:14
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-45191742">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-45192027">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>ExpressJS routing does allow to use wildcards, if you do something like this:</p>

<pre><code>this.app.use('/app/fileasset/ui.html/*', function(req,res) {});
</code></pre>

<p>Then going to a url like <code>/app/fileasset/ui.html/test/view/subview/wtv</code> should populate req.params with <code>"['test/view/subview/wtv']"</code> which you can easily split on the forward slash.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 19 '17 at 13:25
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-45192027">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-45191911">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Do you tryed foreach over req.params?</p>

<pre><code>req.params.forEach(function (item) {
  someFn(item);
})
</code></pre>

<p>or just for</p>

<pre><code>for (var i = 0, len = req.params.length; i &lt; len; i++) {
  someFn(req.params[i]);
}
</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 19 '17 at 13:21
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-45191911">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/express" title="show questions tagged 'express'" target="_blank">express</a> <a href="/questions/tagged/routes" title="show questions tagged 'routes'" target="_blank">routes</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="https://stackoverflow.com/questions/6027937/javascript-float-subtract">https://stackoverflow.com/questions/6027937/javascript-float-subtract</a><div id="articleHeader"><h1>Javascript float subtract</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        8
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>2</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I was wondering how can I subtract two negative Floating-Point numbers in javascript. I tried:</p>

<pre><code>alert(-0.2-0.1);</code></pre>

<p>and the result is <code>-0.30000000000000004</code>. Am I doing something wrong? What do I have to do to get <code>-0.3</code> ?</p>
    </div>
    
    
</div>

                
    <div>
	    <div id="comments-6027937">
                <ul>



    <li id="comment-6969592">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Your not subtracting 2 negatives.
                    – <a href="/users/393908/ash-burlaczenko" title="12,922 reputation" target="_blank">Ash Burlaczenko</a>
                <a href="#comment6969592_6027937" target="_blank">May 17 '11 at 8:18</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-14515818">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                duplicate of <i>so</i>, <i>so</i>, many questions...
                    – <a href="/users/6782/alnitak" title="251,372 reputation" target="_blank">Alnitak</a>
                <a href="#comment14515818_6027937" target="_blank">Jun 18 '12 at 16:14</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-14521227">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
                </ul>
				    
	    </div>

                 
    </div>        </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-6027963">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        13
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>No, nothing wrong with your code, most decimal fractions cannot be represented exactly
in binary, use</p>

<pre><code>number.toFixed(x)</code></pre>

<p>Where <code>x</code> is the number of decimals you want and <code>number</code> is the result of the subtraction.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 17 '11 at 8:05
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-6027963">
                <ul>



    <li id="comment-6970015">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                I don't like toFixed() because it will pad unwanted trailing 0s, see <a href="http://www.w3schools.com/jsref/jsref_tofixed.asp" target="_blank">toFixed()</a>.
                    – <a href="/users/755127/daalbert" title="1,359 reputation" target="_blank">daalbert</a>
                <a href="#comment6970015_6027963" target="_blank">May 17 '11 at 8:49</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-39424291">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Your answer is preposterous, how could this be a limitation with binary?
                    – <a href="/users/964000/ronsper" title="281 reputation" target="_blank">RonSper</a>
                <a href="#comment39424291_6027963" target="_blank">Aug 13 '14 at 20:55</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-61431288">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                @RonSper feel free to suggest an edit :)
                    – <a href="/users/57095/alberto-zaccagni" title="21,389 reputation" target="_blank">Alberto Zaccagni</a>
                <a href="#comment61431288_6027963" target="_blank">Apr 29 '16 at 10:35</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-83069989">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-6027972">
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
<p><code>toFixed()</code> is what you must be looking for.</p>



<pre><code>number.toFixed(x); </code></pre>

<p>where x is the number of digits after the decimal point. It is optional with default value of 0.</p>

<p>More here : <a href="http://www.bennadel.com/blog/1013-Javascript-Number-toFixed-Method.htm" target="_blank">Javascript Number.toFixed() Method</a></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-6027998">
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
<p>The reason of your problem is explained here:
<a href="https://stackoverflow.com/questions/3966484/floating-point-numbers-and-javascript-modulus-operator" target="_blank">Why does modulus operator return fractional number in javascript?</a></p>

<p>A possible solution could be:</p>

<pre><code>&lt;script type="text/javascript"&gt;
var result = (-20-10)/100;
alert("My result is "+result);
&lt;/script&gt;</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-6028117">
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
<p>You are doing nothing wrong, what you are seeing is the side effect of computers storing numbers in base 2. In base 10, 1/3 can't be precisely represented: .33333333 (with a bar over the 3). The same is true for 1/10 and 1/5 in base 2 or binary. The answer you see is merely the result of a rounding error. If you are working with money, it is often advised to just store values as cents to avoid some floating point errors.</p>

<p>As far as fixing the result you can do something like:</p>

<pre><code>var SIGDIG= 100000000;
alert( Math.floor((-0.2-0.1)*SIGDIG)/SIGDIG );</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 17 '11 at 8:23
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-16783120">
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
<p>Another possible solution might be this:</p>

<pre><code>Number((-0.2-0.1).toFixed(x))</code></pre>

<p>Where x should be the tolerance in decimals you'd like.</p>

<p>Running this with an <code>x</code> of 16, gives me an output of <code>-0.3</code>.</p>

<pre><code>-0.3 === Number((-0.2-0.1).toFixed(16)) // true, and also with every 0 &lt; x &lt; 16</code></pre>

<p>Let me know.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 28 '13 at 2:47
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/floating-point" title="show questions tagged 'floating-point'" target="_blank">floating-point</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
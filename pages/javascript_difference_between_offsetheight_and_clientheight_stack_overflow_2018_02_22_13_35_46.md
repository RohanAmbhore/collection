<a href="https://stackoverflow.com/questions/4106538/difference-between-offsetheight-and-clientheight">https://stackoverflow.com/questions/4106538/difference-between-offsetheight-and-clientheight</a><div id="articleHeader"><h1>difference between offsetHeight and clientHeight</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        93
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>37</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>In the javascript dom  - what is the difference between offsetHeight and clientHeight of an element?</p>
    </div>
    <div>
        <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> 
    </div>
    <table>
    <tbody><tr>
    <td>
        
    </td>
    <td>
        <div>
    <div>
        asked Nov 5 '10 at 14:00
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
	    

        <div id="comments-link-4106538">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-4106585">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        136
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p><a href="http://help.dottoro.com/ljcadejj.php" target="_blank">clientHeight</a>:</p>

<blockquote>
  <p>Returns the height of the visible area for an object, in pixels. The value contains the height with the padding, but it does not include the scrollBar, border, and the margin.</p>
</blockquote>

<p><a href="http://help.dottoro.com/ljuxqbfx.php" target="_blank">offsetHeight</a>:</p>

<blockquote>
  <p>Returns the height of the visible area for an object, in pixels. The value contains the height with the padding, scrollBar, and the border, but does not include the margin.</p>
</blockquote>

<p>So, <code>offsetHeight</code> includes scrollbar and border, <code>clientHeight</code> doesn't.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Nov 5 '10 at 14:05
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
	    <div id="comments-4106585">
                <ul>



    <li id="comment-29461070">
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
                Another thing I noticed is that clientHeight is much much faster than offsetHeight. Do you have any idea why?
                    – <a href="/users/36047/disc0dancer" title="3,148 reputation" target="_blank">disc0dancer</a>
                <a href="#comment29461070_4106585" target="_blank">Nov 6 '13 at 14:59</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-29461174">
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
                @disc0dancer - Probably because the browser already has the <code>clientSize</code> readily available (after all, it it the viewport), but needs to calculate <code>offsetHeight</code> after reflowing the whole document?
                    – <a href="/users/1583/oded" title="383,874 reputation" target="_blank">Oded</a>
                <a href="#comment29461174_4106585" target="_blank">Nov 6 '13 at 15:02</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-29461946">
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
                Well the webkit inspector says that the reflows are also on the whole document, even when asking for clientHeigh.
                    – <a href="/users/36047/disc0dancer" title="3,148 reputation" target="_blank">disc0dancer</a>
                <a href="#comment29461946_4106585" target="_blank">Nov 6 '13 at 15:21</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-29462268">
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
                @disc0dancer - So much for my guess. But this is an implementation thing - not sure all browsers are like that.
                    – <a href="/users/1583/oded" title="383,874 reputation" target="_blank">Oded</a>
                <a href="#comment29462268_4106585" target="_blank">Nov 6 '13 at 15:29</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-4106585">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-31439965">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        41
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>The answer from Oded is the theory. But the theory and the reality are not always the same, at least not for the &lt;BODY&gt; or the &lt;HTML&gt; elements which may be important for scrolling operations in javascript.</p>

<p>Microsoft has a nice image in the MSDN:</p>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/zWca7.png" alt="ClientHeight, OffsetHeight, ScrollHeight" /></div></p>

<p>If you have a HTML page which shows a vertical scrollbar one would expect that either the &lt;BODY&gt; or the &lt;HTML&gt; element has a ScrollHeight geater than OffsetHeight as this image shows. This is true for all older versions of Internet Explorer.</p>

<p>But it is not true for Internet Explorer 11 and not for Firefox 36.
At least in these browsers OffsetHeight is nearly the same as ScrollHeight which is wrong.</p>

<p>And while OffsetHeight may be wrong, ClientHeight is always correct.</p>

<p>Try the following code on different browsers and you will see:</p>

<pre><code>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;body&gt;
&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;
&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;
&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;&lt;br&gt;
&lt;script&gt;
    document.write("Body off: " + document.body.offsetHeight 
             + "&lt;br&gt;Body cli: " + document.body.clientHeight
             + "&lt;br&gt;Html off: " + document.body.parentElement.offsetHeight               
             + "&lt;br&gt;Html cli: " + document.body.parentElement.clientHeight);
&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

<p>While older Internet Explorer shows correctly:</p>

<pre><code>Body off: 1197
Body cli: 1197
Html off: 878
Html cli: 874  </code></pre>

<p>The output from Firefox and Internet Explorer 11 is:</p>

<pre><code>Body off: 1260
Body cli: 1260
Html off: 1276   // this is completely wrong
Html cli: 889</code></pre>

<p>which shows clearly that offsetHeight is wrong here. OffsetHeight and ClientHeight should differ only a few pixels or be the same.</p>

<hr />

<p>Please note that ClientHeight and OffsetHeight may also differ extremely for elements that are not visible like for example a &lt;FORM&gt; where OffsetHeight may be the real size of the FORM while ClientHeight may be zero.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-31439965">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="https://stackoverflow.com/questions/36525006/do-clearboth-and-overflowhidden-work-the-same-way-to-make-a-container-wrap">https://stackoverflow.com/questions/36525006/do-clearboth-and-overflowhidden-work-the-same-way-to-make-a-container-wrap</a><div id="articleHeader"><h1>Do "clear:both" and "overflow:hidden" work the same way to make a container wrap floated children?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        1
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>2</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I have a div with floated children.</p>

<p>I know I can stretch the height in the following 2 ways:</p>

<div>
<div>
<pre><code>.container {
  border: 2px solid #ccc;
  margin-bottom: 250px;
}

.container-2::after {
  content: '';
  display: block;
  height: 0;
  font-size: 0;
  clear: both;
}

.container-3 {
  overflow: hidden;
}

.item {
  float: left;
  width: 200px;
  height: 50px;
  background: red;
  margin: 10px;
}</code></pre>
<pre><code>&lt;div class="container container-1"&gt;
  &lt;div class="item"&gt;&lt;/div&gt;
  &lt;div class="item"&gt;&lt;/div&gt;
  &lt;div class="item"&gt;&lt;/div&gt;
&lt;/div&gt;

&lt;div class="container container-2"&gt;
  &lt;div class="item"&gt;&lt;/div&gt;
  &lt;div class="item"&gt;&lt;/div&gt;
  &lt;div class="item"&gt;&lt;/div&gt;
&lt;/div&gt;

&lt;div class="container container-3"&gt;
  &lt;div class="item"&gt;&lt;/div&gt;
  &lt;div class="item"&gt;&lt;/div&gt;
  &lt;div class="item"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>
<div><div><div><a target="_blank">Full page</a></div></div></div></div>
</div>
<p>But I think they have the different principles: the <code>clear:both</code> <em>::after</em> element stays away from the float brothers, and force the parent div to stretch the height; the <code>overflow:hidden</code> style makes the div have the <em>BFC</em>, and according to <a href="http://www.w3.org/TR/CSS2/visudet.html#root-height" target="_blank">standard</a>, BFC will stretch its height to include its float children.</p>

<p>The advantages and disadvantages are not important,but the how they works.</p>

<p>Am I right, they are different but have the same result?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-36525006">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-36525225">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<blockquote>
  <p>Do <code>clear:both</code> and <code>overflow:hidden</code> work the same way to make a container wrap floated children?</p>
</blockquote>

<p>No. They perform different functions.</p>

<p><strong><em><code>clear:both</code></em></strong></p>

<p>The <code>clear</code> property controls whether an element can be next to or below floated elements that come before it. It controls whether an element can <em>clear</em> the floated elements.</p>

<p><code>clear:both</code>, when applied to a non-floating, block-level element:</p>

<blockquote>
  <p>Requires that the top border edge of the box be below the bottom outer edge of any right-floating and left-floating boxes that resulted from elements earlier in the source document.</p>
  
  <p><sub><em>source: <a href="https://www.w3.org/TR/CSS2/visuren.html#propdef-clear" target="_blank">https://www.w3.org/TR/CSS2/visuren.html#propdef-clear</a></em></sub></p>
</blockquote>

<p>So the <code>clear</code> property more likely applies to a sibling of floated elements. It has nothing to do with <em>stretching the height of div which has float children</em> (as stated in your question).</p>

<p><strong><em><code>overflow:hidden</code></em></strong> (or <strong><em><code>overflow:auto</code></em></strong>)</p>

<p>The <code>overflow</code> property, when used with a value other than <code>visible</code>, creates a new <a href="https://drafts.csswg.org/css-display-3/#block-formatting-context" target="_blank"><em>block formatting context</em></a>. This causes the element containing floats to expand in order to contain its floated children.</p>

<p>In summary, one property clears an element past floated elements. The other stretches the container to wrap floated elements. The output may appear the same for both. But each property is fundamentally different.</p>

<p>Further reading:</p>


    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-36525225">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/html" title="show questions tagged 'html'" target="_blank">html</a> <a href="/questions/tagged/css" title="show questions tagged 'css'" target="_blank">css</a> <a href="/questions/tagged/css-float" title="show questions tagged 'css-float'" target="_blank">css-float</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
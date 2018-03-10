<a href="https://stackoverflow.com/questions/21064101/understanding-offsetwidth-clientwidth-scrollwidth-and-height-respectively">https://stackoverflow.com/questions/21064101/understanding-offsetwidth-clientwidth-scrollwidth-and-height-respectively</a><div id="articleHeader"><h1>Understanding offsetWidth, clientWidth, scrollWidth and -Height, respectively</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear (click again to undo)" target="_blank">up vote</a>
        256
        <a title="This question does not show any research effort; it is unclear or not useful (click again to undo)" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>192</b></div>


</div>

            </div>

            
<div>
    <div>

<p>There are several questions on StackOverflow regarding offsetWidth/clientWidth/scrollWidth (and -Height, respectively), but none give comprehensive explanation of what those values are.</p>

<p>Also, there are several sources on the web giving confusing or incorrect information.</p>

<p>Can you give a complete explanation including some visual hints?
Also, how can those values be used to calculate scroll bar widths?</p>
    </div>
    
    <div>
    

    <div>
        <div>
    <div>
        asked Jan 11 '14 at 15:26
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-21064102">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful (click again to undo)" target="_blank">up vote</a>
        606
        <a title="This answer is not useful (click again to undo)" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>The CSS box model is rather complicated, particularly when it comes to scrolling content. While the browser uses the values from your CSS to draw boxes, determining all the dimensions using JS is not straight-forward if you only have the CSS.</p>

<p>That's why each element has six DOM properties for your convenience: <code>offsetWidth</code>, <code>offsetHeight</code>, <code>clientWidth</code>, <code>clientHeight</code>, <code>scrollWidth</code> and <code>scrollHeight</code>. These are read-only attributes representing the current visual layout, and all of them are <em>integers</em> (thus possibly subject to rounding errors).</p>

<p>Let's go through them in detail:</p>

<ul>
<li><code>offsetWidth</code>, <code>offsetHeight</code>: The size of the visual box incuding all borders. Can be calculated by adding <code>width</code>/<code>height</code> and paddings and borders, if the element has <code>display: block</code></li>
<li><code>clientWidth</code>, <code>clientHeight</code>: The visual portion of the box content, not including borders or scroll bars , but includes padding . Can not be calculated directly from CSS, depends on the system's scroll bar size.</li>
<li><code>scrollWidth</code>, <code>scrollHeight</code>: The size of all of the box's content, including the parts that are currently hidden outside the scrolling area. Can not be calculated directly from CSS, depends on the content.</li>
</ul>

<p><a href="http://jsfiddle.net/y8Y32/25/" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/5AAyW.png" alt="CSS2 Box Model" /></div></a></p>

<h3>Try it out: <a href="http://jsfiddle.net/y8Y32/25/" target="_blank">jsFiddle</a></h3>

<hr />

<p>Since <code>offsetWidth</code> takes the scroll bar width into account, we can use it to calculate the scroll bar width via the formula</p>

<pre><code>scrollbarWidth = offsetWidth - clientWidth - getComputedStyle().borderLeftWidth - getComputedStyle().borderRightWidth
</code></pre>

<p>Unfortunately, we may get rounding errors, since <code>offsetWidth</code> and <code>clientWidth</code> are always integers, while the actual sizes may be fractional with zoom levels other than 1.</p>

<p>Note that this</p>

<pre><code>scrollbarWidth = getComputedStyle().width + getComputedStyle().paddingLeft + getComputedStyle().paddingRight - clientWidth
</code></pre>

<p>does <strong>not</strong> work reliably in Chrome, since Chrome returns <code>width</code> with scrollbar already substracted. (Also, Chrome renders paddingBottom to the bottom of the scroll content, while other browsers don't)</p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-21064102">
                <ul>



    <li id="comment-38602697">
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
                For those seeking finer granularity than integers, use <code>element.getBoundingClientRect()</code> (see the note at <a href="https://developer.mozilla.org/en-US/docs/Web/API/Element.clientWidth" target="_blank">developer.mozilla.org/en-US/docs/Web/API/Element.clientWidth</a>)
                    – <a href="/users/476426/anson-kao" title="3,059 reputation" target="_blank">Anson Kao</a>
                Jul 21 '14 at 5:03
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-39350460">
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
                Wow! What an example, so descriptive and so nicely explained :) Thanks !!
                    – <a href="/users/2103202/anmol-saraf" title="7,884 reputation" target="_blank">Anmol Saraf</a>
                Aug 12 '14 at 4:09
                                                                            </div>
        </div>
    </li>
    <li id="comment-41206822">
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
                Well really. That is the best answer to <i>any</i> question I've seen on SO!
                    – <a href="/users/2816199/tomekwi" title="1,011 reputation" target="_blank">tomekwi</a>
                Oct 8 '14 at 20:39
                                                                            </div>
        </div>
    </li>
    <li id="comment-59668083">
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
                Note that depending on your layout, scrollWidth and scrollHeight can be really useful to get the size of your pseudo elements ::before and ::after.
                    – <a href="/users/2086460/david" title="164 reputation" target="_blank">David</a>
                Mar 15 '16 at 10:13
                                                                            </div>
        </div>
    </li>
    <li id="comment-66186936">
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
                So, none of these include margin, right?
                    – <a href="/users/3995261/yakovl" title="2,251 reputation" target="_blank">YakovL</a>
                Sep 11 '16 at 0:48
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-33672058">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful (click again to undo)" target="_blank">up vote</a>
        25
        <a title="This answer is not useful (click again to undo)" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>If you want to use scrollWidth to get the <strong>"REAL"</strong> <strong>CONTENT WIDTH/HEIGHT</strong> (as content can be BIGGER than the css-defined width/height-Box) the <strong>scrollWidth/Height is very UNRELIABLE</strong> as some browser seem to "MOVE" the paddingRIGHT & paddingBOTTOM if the content is to big. They then place the paddings at the RIGHT/BOTTOM of the "too broad/high content" (see picture below). </p>

<p><strong>==&gt;</strong> Therefore to get the REAL CONTENT WIDTH in some browsers you have to substract BOTH paddings from the scrollwidth and in some browsers you only have to substract the LEFT Padding.</p>

<p>I found a solution for this and wanted to add this as a comment, but was not allowed. So I took the picture and made it a bit clearer in the regard of the "moved paddings" and the "unreliable scrollWidth". <strong>In the BLUE AREA you find my solution on how to get the "REAL" CONTENT WIDTH!</strong></p>

<p>Hope this helps to make things even clearer!</p>

<p><a href="https://i.stack.imgur.com/JY33m.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/JY33m.png" alt="enter image description here" /></div></a></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-39762954">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful (click again to undo)" target="_blank">up vote</a>
        8
        <a title="This answer is not useful (click again to undo)" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>There is a good article on MDN that explains the theory behind those concepts:
<a href="https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements" target="_blank">https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements</a></p>

<p>It also explains the important conceptual differences between boundingClientRect's width/height vs offsetWidth/offsetHeight.</p>

<p>Then, to prove the theory right or wrong, you need some tests.
That's what I did here: <a href="https://github.com/lingtalfi/dimensions-cheatsheet" target="_blank">https://github.com/lingtalfi/dimensions-cheatsheet</a></p>

<p>It's testing for chrome53, ff49, safari9, edge13 and ie11.</p>

<p>The results of the tests prove that the theory is generally right.
For the tests, I created 3 divs containing 10 lorem ipsum paragraphs each.
Some css was applied to them:</p>

<pre><code>.div1{
    width: 500px;
    height: 300px;
    padding: 10px;
    border: 5px solid black;
    overflow: auto;
}
.div2{
    width: 500px;
    height: 300px;
    padding: 10px;
    border: 5px solid black;
    box-sizing: border-box;
    overflow: auto;
}

.div3{
    width: 500px;
    height: 300px;
    padding: 10px;
    border: 5px solid black;
    overflow: auto;
    transform: scale(0.5);
}
</code></pre>

<p>And here are the results:</p>

<ul>
<li>

<ul>
<li>offsetWidth: 530 (chrome53, ff49, safari9, edge13, ie11)</li>
<li>offsetHeight: 330 (chrome53, ff49, safari9, edge13, ie11)</li>
<li>bcr.width: 530 (chrome53, ff49, safari9, edge13, ie11)</li>
<li><p>bcr.height: 330 (chrome53, ff49, safari9, edge13, ie11)</p></li>
<li><p>clientWidth: 505 (chrome53, ff49, safari9)</p></li>
<li>clientWidth: 508 (edge13)</li>
<li>clientWidth: 503 (ie11)</li>
<li><p>clientHeight: 320 (chrome53, ff49, safari9, edge13, ie11)</p></li>
<li><p>scrollWidth: 505 (chrome53, safari9, ff49)</p></li>
<li>scrollWidth: 508 (edge13)</li>
<li>scrollWidth: 503 (ie11)</li>
<li>scrollHeight: 916 (chrome53, safari9)</li>
<li>scrollHeight: 954 (ff49)</li>
<li>scrollHeight: 922 (edge13, ie11)</li>
</ul></li>
<li>

<ul>
<li>offsetWidth: 500 (chrome53, ff49, safari9, edge13, ie11)</li>
<li>offsetHeight: 300 (chrome53, ff49, safari9, edge13, ie11)</li>
<li>bcr.width: 500 (chrome53, ff49, safari9, edge13, ie11)</li>
<li>bcr.height: 300 (chrome53, ff49, safari9)</li>
<li>bcr.height: 299.9999694824219 (edge13, ie11)</li>
<li>clientWidth: 475 (chrome53, ff49, safari9)</li>
<li>clientWidth: 478 (edge13)</li>
<li>clientWidth: 473 (ie11)</li>
<li><p>clientHeight: 290 (chrome53, ff49, safari9, edge13, ie11)</p></li>
<li><p>scrollWidth: 475 (chrome53, safari9, ff49)</p></li>
<li>scrollWidth: 478 (edge13)</li>
<li>scrollWidth: 473 (ie11)</li>
<li>scrollHeight: 916 (chrome53, safari9)</li>
<li>scrollHeight: 954 (ff49)</li>
<li>scrollHeight: 922 (edge13, ie11)</li>
</ul></li>
<li>

<ul>
<li>offsetWidth: 530 (chrome53, ff49, safari9, edge13, ie11)</li>
<li>offsetHeight: 330 (chrome53, ff49, safari9, edge13, ie11)</li>
<li>bcr.width: 265 (chrome53, ff49, safari9, edge13, ie11)</li>
<li>bcr.height: 165 (chrome53, ff49, safari9, edge13, ie11)</li>
<li>clientWidth: 505 (chrome53, ff49, safari9)</li>
<li>clientWidth: 508 (edge13)</li>
<li>clientWidth: 503 (ie11)</li>
<li><p>clientHeight: 320 (chrome53, ff49, safari9, edge13, ie11)</p></li>
<li><p>scrollWidth: 505 (chrome53, safari9, ff49)</p></li>
<li>scrollWidth: 508 (edge13)</li>
<li>scrollWidth: 503 (ie11)</li>
<li>scrollHeight: 916 (chrome53, safari9)</li>
<li>scrollHeight: 954 (ff49)</li>
<li>scrollHeight: 922 (edge13, ie11)</li>
</ul></li>
</ul>

<p>So, apart from the boundingClientRect's height value (299.9999694824219 instead of expected 300) in edge13 and ie11, the results confirm that the theory behind this works.</p>

<p>From there, here is my definition of those concepts:</p>

<ul>
<li>offsetWidth/offsetHeight: dimensions of the layout border box</li>
<li>boundingClientRect: dimensions of the rendering border box</li>
<li>clientWidth/clientHeight: dimensions of the visible part of the layout padding box (excluding scroll bars)</li>
<li>scrollWidth/scrollHeight: dimensions of the layout padding box if it wasn't constrained by scroll bars</li>
</ul>

<p>Note: the default vertical scroll bar's width is 12px in edge13, 15px in chrome53, ff49 and safari9, and 17px in ie11 (done by measurements in photoshop from screenshots, and proven right by the results of the tests).</p>

<p>However, in some cases, maybe your app is not using the default vertical scroll bar's width.</p>

<p>So, given the definitions of those concepts, the vertical scroll bar's width should be equal to (in pseudo code):</p>

<ul>
<li><p>layout dimension: offsetWidth - clientWidth - (borderLeftWidth + borderRightWidth)</p></li>
<li><p>rendering dimension: boundingClientRect.width - clientWidth - (borderLeftWidth + borderRightWidth)</p></li>
</ul>

<p>Note, if you don't understand layout vs rendering please read the mdn article.</p>

<p>Also, if you have another browser (or if you want to see the results of the tests for yourself), you can see my test page here: <a href="http://codepen.io/lingtalfi/pen/BLdBdL" target="_blank">http://codepen.io/lingtalfi/pen/BLdBdL</a></p>
    </div>
    <div>
    
    
            


    <div>
       

    <div>
    <div>
        answered Sep 29 '16 at 6:31
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-45897388">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful (click again to undo)" target="_blank">up vote</a>
        12
        <a title="This answer is not useful (click again to undo)" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I created a more comprehensive and cleaner version that some people might find useful for remembering which name corresponds to which value. I used Chrome Dev Tool's color code and labels are organized symmetrically to pick up analogies faster:</p>

<p><a href="https://i.stack.imgur.com/Cl1IA.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/Cl1IA.png" alt="enter image description here" /></div></a></p>

<ul>
<li><p>Note 1: <code>clientLeft</code> also includes the width of the vertical scroll
bar if the direction of the text is set to right-to-left (since the
bar is displayed to the left in that case)</p></li>
<li><p>Note 2: the outermost line represents the closest <strong><em>positioned</em></strong> parent
(an element whose <code>position</code> property is set to a value different than
<code>static</code> or <code>initial</code>). Thus, if the direct container isn’t a <strong><em>positioned</em></strong>
element, then the line doesn’t represent the first container in
the hierarchy but another element higher in the hierarchy. If no
<strong><em>positioned</em></strong> parent is found, the browser will take the <code>html</code> or <code>body</code>
element as reference</p></li>
</ul>

<hr />

<p>Hope somebody finds it useful, just my 2 cents ;)</p>
    </div>
    
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/html" title="show questions tagged 'html'" target="_blank">html</a> <a href="/questions/tagged/css" title="show questions tagged 'css'" target="_blank">css</a> <a href="/questions/tagged/dom" title="show questions tagged 'dom'" target="_blank">dom</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
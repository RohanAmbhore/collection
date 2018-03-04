<a href="https://stackoverflow.com/questions/20383622/width-equal-to-content">https://stackoverflow.com/questions/20383622/width-equal-to-content</a><div id="articleHeader"><h1>Width equal to content</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        42
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>8</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I'm experiencing some trouble with the width property of CSS. I have some paragraphs inside a div. I'd like to make the width of the paragraphs equal to their content, so that their green background looks like a label for the text. What I get instead is that the paragraphs inherit the width of the div father node which is wider. </p>

<div>
<div>
<pre><code>#container {
  width: 30%;
  background-color: grey;
}

#container p {
  background-color: green;
}</code></pre>
<pre><code>&lt;div id="container"&gt;
  &lt;p&gt;Sample Text 1&lt;/p&gt;
  &lt;p&gt;Sample Text 2&lt;/p&gt;
  &lt;p&gt;Sample Text 3&lt;/p&gt;
&lt;/div&gt;</code></pre>
<div><div><div><a target="_blank">Full page</a></div></div></div></div>
</div>
</div>
    
    
</div>

                
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-20383701">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        75
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>By default <code>p</code> tags are <code>block</code> elements, which means they take 100% of the parent <code>width</code>. </p>

<p>You can change their display property with:</p>

<pre><code>#container p {
   display:inline-block;
}</code></pre>

<p>But it puts the elements side by side.</p>

<p>To keep each element on its own line you can use:</p>

<pre><code>#container p {
   clear:both;
   float:left;
}</code></pre>

<p><sub>(If you use float and need to clear after floated elements, see this link for different techniques: <a href="http://css-tricks.com/all-about-floats/" target="_blank">http://css-tricks.com/all-about-floats/</a>)</sub></p>

<p>Demo: <strong><a href="http://jsfiddle.net/CvJ3W/5/" target="_blank">http://jsfiddle.net/CvJ3W/5/</a></strong></p>

<p><strong>Edit</strong> </p>

<p>If you go for the solution with <code>display:inline-block</code> but want to keep each item in one line, you can just add a <code>&lt;br&gt;</code> tag after each one:</p>

<pre><code>&lt;div id="container"&gt;
  &lt;p&gt;Sample Text 1&lt;/p&gt;&lt;br/&gt;
  &lt;p&gt;Sample Text 2&lt;/p&gt;&lt;br/&gt;
  &lt;p&gt;Sample Text 3&lt;/p&gt;&lt;br/&gt;
&lt;/div&gt;</code></pre>

<p>New demo: <strong><a href="http://jsfiddle.net/CvJ3W/7/" target="_blank">http://jsfiddle.net/CvJ3W/7/</a></strong></p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-20383701">
                <ul>



    <li id="comment-84128449">
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
                Seeing the new edit, I respectfully disagree with throwing <code>&lt;br&gt;</code> for styling.
                    – <a href="/users/1653236/viswebsoft" title="165 reputation" target="_blank">VisWebsoft</a>
                <a href="#comment84128449_20383701" target="_blank">Feb 1 at 15:26</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-84138739">
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
                @VisWebsoft I agree with you you always have the option to use ´float´ to keep each element in new lines. But give always all the possible solutions is nice, just choice the one of your preference.
                    – <a href="/users/2887133/danip" title="30,407 reputation" target="_blank">DaniP</a>
                <a href="#comment84138739_20383701" target="_blank">Feb 1 at 20:20</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-20383672">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Adding <code>display: inline-block;</code> to the <code>p</code> styling should take of it:</p>

<p><a href="http://jsfiddle.net/pyq3C/" target="_blank">http://jsfiddle.net/pyq3C/</a></p>

<pre><code>#container p{
    background-color: green;
    display: inline-block;
}</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 4 '13 at 19:03
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-20383672">
                <ul>



    <li id="comment-30435023">
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
                It partially works now. The width of the paragraphs equal the content as I wanted. The problem is that now I get all the paragraphs in just a line instead of three.
                    – <a href="/users/3067088/user3067088" title="421 reputation" target="_blank">user3067088</a>
                <a href="#comment30435023_20383672" target="_blank">Dec 4 '13 at 19:08</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-30435113">
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
                You can force to the next line by adding: <code>float: left; clear: left;</code>
                    – <a href="/users/2332112/stuart-kershaw" title="7,263 reputation" target="_blank">Stuart Kershaw</a>
                <a href="#comment30435113_20383672" target="_blank">Dec 4 '13 at 19:10</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-30435831">
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
                Adding <code>float: left</code> to an element displayed as <code>inline-block</code> will set it to <code>block</code> according to CSS 2.1 REC (<a href="http://www.w3.org/TR/CSS2/visuren.html#choose-position" target="_blank">relationships between display, position, and float</a>) so you can as well remove <code>inline-block</code> and it won't change anything
                    – <a href="/users/137626/felipeals" title="16,881 reputation" target="_blank">FelipeAls</a>
                <a href="#comment30435831_20383672" target="_blank">Dec 4 '13 at 19:32</a>
                        
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-20383749">
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
<p>Try using a <code><code>&lt;span&gt;</code></code> element instead. Or if you prefer, try <code>display:inline</code></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 4 '13 at 19:06
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-20383749">
                <ul>



    <li id="comment-30435259">
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
                It partially works now. The width of the paragraphs equal the content as I wanted. The problem is that now I get all the paragraphs in just a line instead of three.
                    – <a href="/users/3067088/user3067088" title="421 reputation" target="_blank">user3067088</a>
                <a href="#comment30435259_20383749" target="_blank">Dec 4 '13 at 19:15</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-20383789">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Set <code>display:inline-block</code> and then adjust your margins.</p>

<p>fiddle here: <a href="http://jsfiddle.net/Q2MrC/" target="_blank">http://jsfiddle.net/Q2MrC/</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 4 '13 at 19:08
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-37353025">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>The solution with <code>inline-block</code> forces you to insert <code>&lt;br&gt;</code> after each element.<br />
The solution with <code>float</code> forces you to wrap all elements with "clearfix" div.</p>

<p>Another elegant solution is to use <code>display: table</code> for elements.</p>

<p>With this solution you don't need to insert line breaks manually (like with <code>inline-block</code>), you don't need a wrapper around your elements (like with floats) and you can center your element if you need.</p>

<p><a href="http://jsfiddle.net/8md3jy4r/3/" target="_blank">http://jsfiddle.net/8md3jy4r/3/</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 20 '16 at 17:57
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-38129639">
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
<p>You can use either of below :-</p>

<p>1) display : inline-block :</p>

<p><a href="http://jsbin.com/feneni/edit?html,css,js,output" target="_blank">http://jsbin.com/feneni/edit?html,css,js,output</a></p>

<p>Uncomment the line</p>

<pre><code> float:left;
 clear:both </code></pre>

<p>and you will find that parent container has collapsed.</p>

<p>2) Using display : table</p>

<p><a href="http://jsbin.com/dujowep/edit?html,css,js,output" target="_blank">http://jsbin.com/dujowep/edit?html,css,js,output</a></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-45493323">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        15
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I set width as max-content and it worked for me.</p>

<p><code>width: max-content;</code></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 3 '17 at 19:47
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-45493323">
                <ul>



    <li id="comment-77998870">
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
                Didn't know about that value, works great thx!
                    – <a href="/users/4916074/philippe-leefsma" title="3,221 reputation" target="_blank">Philippe Leefsma</a>
                <a href="#comment77998870_45493323" target="_blank">Aug 5 '17 at 6:35</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-83244218">
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
                Not supported by IE or Edge though
                    – <a href="/users/774828/pkr298" title="803 reputation" target="_blank">pkr298</a>
                <a href="#comment83244218_45493323" target="_blank">Jan 7 at 1:10</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-84128500">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
    <li id="comment-84302341">
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
                Also, the component will have the width set, and if the browser window is less than that, it will not adjust.
                    – <a href="/users/1026132/nacho-coloma" title="4,024 reputation" target="_blank">Nacho Coloma</a>
                <a href="#comment84302341_45493323" target="_blank">Feb 6 at 21:22</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-45649809">
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
<p>Despite using <code>display: inline-block</code>. My div would fill the screen width when the children elements had their widths set to <code>%</code> of parent. If anyone else is looking for a solution to this and doesn't mind using screen proportion instead of parent proportion, replace the <code>%</code> with <code>vw</code> for width (Viewport Width), or <code>vh</code> for height (Viewport Height).</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 12 '17 at 11:40
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-45838665">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            



    
    <div>
	    <div id="comments-45838665">
                <ul>



    <li id="comment-78636983">
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
                While this link may answer the question, it is better to include the essential parts of the answer here and provide the link for reference.  Link-only answers can become invalid if the linked page changes. - <a href="/review/low-quality-posts/17120891" target="_blank">From Review</a>
                    – <a href="/users/2411243/zabuza" title="6,175 reputation" target="_blank">Zabuza</a>
                <a href="#comment78636983_45838665" target="_blank">Aug 23 '17 at 12:34</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-84123014">
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

  

<div id="answer-48652253">
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
<p>You can use flex to achieve this:</p>

<pre><code>.container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}</code></pre>

<p><code>flex-start</code> will automatically adjust the width of children to their contents.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Feb 6 at 21:28
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/css" title="show questions tagged 'css'" target="_blank">css</a> <a href="/questions/tagged/width" title="show questions tagged 'width'" target="_blank">width</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
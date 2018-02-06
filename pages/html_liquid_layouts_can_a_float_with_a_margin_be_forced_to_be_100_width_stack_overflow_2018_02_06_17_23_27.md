<a href="https://stackoverflow.com/questions/5642364/liquid-layouts-can-a-float-with-a-margin-be-forced-to-be-100-width">https://stackoverflow.com/questions/5642364/liquid-layouts-can-a-float-with-a-margin-be-forced-to-be-100-width</a><div id="articleHeader"><h1>Liquid layouts: Can a float with a margin be forced to be 100% width?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        6
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>6</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I'm coding my first liquid layout and I have to say it's a lot more time-intensive than a fixed width layout. However, I see the advantages and so I'd like to make it work!</p>

<p>Here's my situation:</p>

<ul>
<li>I have a header with some text in that makes the header of variable height depending on the browser text size.</li>
<li>I have a fixed-width nav on the left. The nav is floated left and has a negative margin the same number of pixels as the width which effectively makes it slot into a zero-width space. Neat!</li>
<li>I have my main content section which is floated right. It has a left margin the width of the nav so the content avoids hiding underneath the links of the nav.</li>
<li>The nav comes second in the source so the users of assistive tech get to the content first.</li>
</ul>

<p>This works great but only if the content of the main content section has lines of text that wrap around the full width of the page. If the content in only short lines or a list the content section's width is the same as the content within it. As the content section is floated right it means the content looks wrong in these situations. Obviously the page width is variable and so for larger monitors this problem is more common.</p>

<p>I'm looking for a way of showing the content section filling the page at all times so that the content will sit on the left and fill out to the right even when the lines are short. I've tried absolute positioning but that messes up the footer which stays in the right place by clearing the floated nav and content section.</p>

<p>Any suggestions would be really useful!</p>

<p><strong>Edit:</strong> </p>

<p>As requested I've provided some demo pages.</p>

<p>Here is a page which has wide content and looks OK: <a href="http://www.qkschool.org.uk/static/redesign/widepage.html" target="_blank">http://www.qkschool.org.uk/static/redesign/widepage.html</a></p>

<p>And here is a page with thin content which is all right-aligned because of the float: <a href="http://www.qkschool.org.uk/static/redesign/thinpage.html" target="_blank">http://www.qkschool.org.uk/static/redesign/thinpage.html</a></p>

<p>Many thanks!</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-5642364">
                <ul>



    <li id="comment-6433275">
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
                @Mad, @thirtydot: From what I've seen it is discouraged that code be segmented from the question. <a href="http://jsfiddle.net/" target="_blank">jsFiddle</a> is great to show how it works, but the code itself should be part of the Q or A.
                    – <a href="/users/191837/kevin-peno" title="7,498 reputation" target="_blank">Kevin Peno</a>
                <a href="#comment6433275_5642364" target="_blank">Apr 12 '11 at 23:00</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-5642364">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-5642456">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>This has always been a favorite source of mine for liquid layouts:</p>

<p><a href="http://matthewjamestaylor.com/blog/perfect-3-column.htm" target="_blank">http://matthewjamestaylor.com/blog/perfect-3-column.htm</a></p>

<p>(Make sure to click around for all the different variations)</p>

<p>I'm not saying you should abandon learning yourself, but I think it's worth a look at some of the tricks used in those layouts. All of them work great in IE6 and IE7 as well, and use good content-first source order. They can be easily turned into fixed-width if needed. I honestly have never found another layout that I like as much as the ones posted on this website.</p>

<p>One variation I use with these layouts is wrapping every column with an extra inner div, and setting the margin or padding on this div and nothing else, this will make the width and positioning calculations a lot simpler (you'll see if you check it out). I also wrap the entire thing in a div for easier max-width and centering.</p>

<p>Good luck and let me know if you need any advice with this technique, I've been using it for years and it has served me well.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 12 '11 at 22:39
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
	    <div id="comments-5642456">
                <ul>



    <li id="comment-6471476">
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
                Thanks, that's really neat but my nav needs to be fixed width and I guess it's that that's causing problems... :/ Looking at the article, I think all the columns shown there are flexible.
                    – <a href="/users/582791/mark-stickley" title="546 reputation" target="_blank">Mark Stickley</a>
                <a href="#comment6471476_5642456" target="_blank">Apr 14 '11 at 22:04</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-6471579">
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
                Then <a href="http://matthewjamestaylor.com/blog/ultimate-2-column-left-menu-pixels.htm" target="_blank">this is the one you are looking for</a> I think :) There are so many variations on the layout in the article, you have to click around a bit.
                    – <a href="/users/398242/wesley-murch" title="76,218 reputation" target="_blank">Wesley Murch</a>
                <a href="#comment6471579_5642456" target="_blank">Apr 14 '11 at 22:12</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-6471672">
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
                I think that might be it! I clicked around, but must have missed it somehow :) Thanks!
                    – <a href="/users/582791/mark-stickley" title="546 reputation" target="_blank">Mark Stickley</a>
                <a href="#comment6471672_5642456" target="_blank">Apr 14 '11 at 22:19</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-5642456">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-5642583">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If you think in terms of physics, even liquids have boundaries. When it expands too much it becomes gas. When it contracts too much it becomes solid. In web design, boundaries are important as well. I suggest researching into Elastic design (translates loosely to design that is flexible within specific parameters).</p>

<p>Here are some links to get you started:</p>


    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 12 '11 at 22:56
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
	    <div id="comments-5642583">
                <ul>



    <li id="comment-6471558">
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
                Thanks, that's really interesting reading. I've already got this design signed off but I'll make sure to try and incorporate some elastic design principles into my next project.
                    – <a href="/users/582791/mark-stickley" title="546 reputation" target="_blank">Mark Stickley</a>
                <a href="#comment6471558_5642583" target="_blank">Apr 14 '11 at 22:11</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-6471574">
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

        <div id="comments-link-5642583">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-5642648">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>It´s hard to tell without seeing the design, but 100% heights and widths can be faked styling the parent element (for example using a background on the body or a wrapper div).</p>

<p>If your last point is not crucial (I guess it is because you mentioned it...) you can also switch the order of your floats and remove the float from the content.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 12 '11 at 23:05
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
	    

        <div id="comments-link-5642648">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-5661921">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>You could try using the <a href="http://www.designinfluences.com/fluid960gs/" target="_blank">Fluid 960 grid system</a> - get it working, and then remove/rename classes to make it a bit more semantic.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 14 '11 at 10:34
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
	    

        <div id="comments-link-5661921">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-5670592">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Here is summary of my own layout technique which is in use on many sites, it can take any number of columns, but this sample just copes with your left one : </p>

<h2>JSFiddle <a href="http://jsfiddle.net/clairesuzy/UQ3uX/" target="_blank"><strong>example</strong></a></h2>

<p>the sample shows the footer will always remain below longest column</p>

<p>the sidebar can be any width just change the margin of the content to suit, you can even float two sidebars to the left - then just increase the margin on the <code>#content</code> to clear them.</p>

<p>Alternatively (or as well) the sidebar (or 2) can be floated right, then you just margin the <code>#content</code> div on right instead of the left to "clear" them</p>

<p>This is source ordered, content before sidebars.. it can incorporate any number of headers subheadings and footers (or under content) without affecting the main "columns" area, and you can float your sidebars (if more than one), in any order too.. thus changing their order, width, number even after the fact, via CSS alone</p>

<p>I think my layout technique may have even been incorporated into some Drupal themes and is in use, it's certainly been used on some larger sites too, but I lost track.. it's never let me down anyway :)</p>

<p>here's the template code..</p>

<p><strong>CSS:</strong></p>

<pre><code>html, body {padding: 0; margin: 0;}

#footer,#header {background: #444; color: #fff; clear: both;}

#container { /* always the same don't add anything here */
overflow: hidden;
width: 100%;
}

#contentwrap {/* always the same do not add anything else here */
float: left;
width: 100%;
margin-right: -100%;
}

#content {
margin-left: 270px; /* same as width plus padding of the sidebar(s) and in the same direction(s) */
padding: 20px;
border-left: 1px solid #444;
}

#sidebar {
float: left;
width: 230px;
padding: 20px;
background: #dad;
border-right: 1px solid #444;
}</code></pre>

<p><strong>HTML:</strong></p>

<pre><code>&lt;div id="header"&gt;header&lt;/div&gt;
&lt;div id="container"&gt;
&lt;div id="contentwrap"&gt;
&lt;div id="content"&gt;
&lt;h1&gt;Content  remaining width&lt;/h1&gt;
&lt;p&gt;add more content here&lt;/p&gt;
&lt;h2&gt;Header Level 2&lt;/h2&gt;     
&lt;/div&gt;&lt;!-- content  --&gt;
&lt;/div&gt;&lt;!-- contentwrap  --&gt;

&lt;div id="sidebar"&gt;
&lt;p&gt;short sidebar&lt;/p&gt;
&lt;p&gt;add more content here until this gets longer than main and the footer will still stay below&lt;/p&gt;
&lt;/div&gt;
&lt;/div&gt;
&lt;div id="footer"&gt;footer&lt;/div&gt;</code></pre>

<p>This really is very flexible as sidebars can be fixed width or fluid too, and it will work with ems , %, px.. you name it</p>

<p>yes I'm attached to this code ;)</p>

<p><strong>Edited to add</strong>
If older IE's (6 did) do give trouble with floats/hovers inside the content area, the <code>#content</code> div may need haslayout set, if so just add <code>zoom: 1;</code> to it in fact in my layouts I still do out of habit!</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-5670592">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <div><div><h2>Your Answer</h2><div><div>
    <p>Thanks for contributing an answer to Stack Overflow!</p><ul><li>Please be sure to <em>answer the question</em>. Provide details and share your research!</li></ul><p>But <em>avoid</em> …</p><ul><li>Asking for help, clarification, or responding to other answers.</li><li>Making statements based on opinion; back them up with references or personal experience.</li></ul><p>To learn more, see our <a href="/help/how-to-answer" target="_blank">tips on writing great answers</a>.</p>
</div></div></div></div>


            
    






                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/html" title="show questions tagged 'html'" target="_blank">html</a> <a href="/questions/tagged/css" title="show questions tagged 'css'" target="_blank">css</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
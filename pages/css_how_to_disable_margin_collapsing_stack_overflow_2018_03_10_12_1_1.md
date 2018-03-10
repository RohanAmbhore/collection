<a href="https://stackoverflow.com/questions/19718634/how-to-disable-margin-collapsing">https://stackoverflow.com/questions/19718634/how-to-disable-margin-collapsing</a><div id="articleHeader"><h1>How to disable margin-collapsing?</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        130
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="Click to mark as favorite question (click again to undo)" target="_blank">favorite</a>
        <div><b>52</b></div>


</div>

            </div>

            
<div>
    <div>

<div>
    <p>This question already has an answer here:</p>
    <ul>
        <li>
            <a href="/questions/1828804/how-do-i-uncollapse-a-margin" target="_blank">How do I uncollapse a margin?</a>
                
                    5 answers
                
        </li>
    </ul>
    </div>
<p>Is there a way to disable margin-collapsing altogether?  The only solutions I've found (by the name of "uncollapsing") entail using a 1px border or 1px padding.  I find this unacceptable: the extraneous pixel complicates calculations for no good reason.  Is there a more reasonable way to disable this margin-collapsing?</p>
    </div>
    
    
</div>

                        <div>
                <div>
        <h2>                    <b>marked</b> as duplicate by <a href="/users/3448527/dippas" target="_blank">dippas</a><a href="/badges/tag-badges/css?badgeClass=Gold" target="_blank"> css</a>

 Nov 29 '17 at 23:39
</h2>
        <p>This question has been asked before and already has an answer. If those answers do not fully address your question, please <a href="/questions/ask" target="_blank">ask a new question</a>.</p>
    </div>
            </div>
    
    <div>
	    <div id="comments-19718634">
                <ul>



    <li id="comment-79959153">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
    <li id="comment-82207662">
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
                Simply give elements a value for <code>margin-bottom</code> but leave <code>margin-top</code> as 0.
                    – <a href="/users/2452680/dan-bray" title="1,724 reputation" target="_blank">Dan Bray</a>
                <a href="#comment82207662_19718634" target="_blank">Dec 4 '17 at 0:30</a>
                        
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>        </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-19719427">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        177
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>There are two main types of margin collapse:</p>

<ul>
<li>Collapsing margins between adjacent elements</li>
<li>Collapsing margins between parent and child elements</li>
</ul>

<p>Using a padding or border will prevent collapse only in the latter case. Also, any value of <code>overflow</code> different from its default (<code>visible</code>) applied to the parent will prevent collapse. Thus, both <code>overflow: auto</code> and <code>overflow: hidden</code> will have the same effect. Perhaps the only difference when using <code>hidden</code> is the unintended consequence of hiding content if the parent has a fixed height.</p>

<p>Other properties that, once applied to the parent, can help fix this behaviour are:</p>

<ul>
<li><code>float: left / right</code></li>
<li><code>position: absolute</code></li>
<li><code>display: inline-block</code></li>
</ul>

<p>You can test all of them here: <a href="http://jsfiddle.net/XB9wX/1/" target="_blank">http://jsfiddle.net/XB9wX/1/</a>.</p>

<p>I should add that, as usual, Internet Explorer is the exception. More specifically, in IE 7 margins do not collapse when some kind of layout is specified for the parent element, such as <code>width</code>. </p>

<p>Sources: Sitepoint's article <em><a href="http://reference.sitepoint.com/css/collapsingmargins" target="_blank">Collapsing Margins</a></em></p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-19719427">
                <ul>



    <li id="comment-42717033">
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
                note that padding can also affect this if it's not zero value
                    – <a href="/users/1090395/mladen-janjetovic" title="4,887 reputation" target="_blank">Mladen Janjetovic</a>
                <a href="#comment42717033_19719427" target="_blank">Nov 24 '14 at 14:18</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-47624243">
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
                Note that <code>overflow: auto</code> can cause scrollbars to appear in the parent element, rather than letting overflow content overflow as per <code>overflow: visible</code>.
                    – <a href="/users/926705/leo" title="2,039 reputation" target="_blank">Leo</a>
                <a href="#comment47624243_19719427" target="_blank">Apr 20 '15 at 11:00</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-51651244">
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
                'overflow: auto' doesn't seem to work in Chrome v44.
                    – <a href="/users/623388/tkane2000" title="300 reputation" target="_blank">tkane2000</a>
                <a href="#comment51651244_19719427" target="_blank">Aug 6 '15 at 21:22</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-63052735">
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
                @tkane2000 Works for me with Chrome 51.
                    – <a href="/users/1650137/zero3" title="314 reputation" target="_blank">Zero3</a>
                <a href="#comment63052735_19719427" target="_blank">Jun 13 '16 at 15:13</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-73978212">
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
                Any value of <code>flex</code> different from its default will also disable margin collapse
                    – <a href="/users/4332861/oly" title="101 reputation" target="_blank">Oly</a>
                <a href="#comment73978212_19719427" target="_blank">Apr 17 '17 at 23:28</a>
                        
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-19718884">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        19
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><code>overflow:hidden</code> prevents collapsing margins but it's not free of side effects - namely it... hides overflow.</p>

<p>Apart form this and what you've mentioned you just have to learn live with it and learn for this day when they are actually useful (comes every 3 to 5 years).</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Nov 1 '13 at 0:20
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-19718884">
                <ul>



    <li id="comment-41733422">
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
                Have turned my answer into a community wiki. I think I did cover the side-effect you mentioned in the last two lines of the second paragraph: <i>Perhaps the only difference when using hidden is the unintended consequence of hiding content if the parent has a fixed height</i>. But if you feel that needs further clarification, please feel free to contribute. Thanks.
                    – <a href="/users/2939000/hqcasanova" title="1,088 reputation" target="_blank">hqcasanova</a>
                <a href="#comment41733422_19718884" target="_blank">Oct 24 '14 at 20:41</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-49829808">
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
                <code>overflow: auto</code> is good to use to prevent hidden overflow and still prevent collapsing margins.
                    – <a href="/users/2211053/gavin" title="2,413 reputation" target="_blank">Gavin</a>
                <a href="#comment49829808_19718884" target="_blank">Jun 17 '15 at 15:01</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-25137269">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        42
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>You can also use the good old micro clearfix for this.</p>

<pre><code>#container:before, #container:after{
    content: ' ';
    display: table;
}</code></pre>

<p>See updated fiddle: <a href="http://jsfiddle.net/XB9wX/97/" target="_blank">http://jsfiddle.net/XB9wX/97/</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 5 '14 at 11:04
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-25137269">
                <ul>



    <li id="comment-41733482">
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
                Have turned my answer into a community wiki. Please feel free to extend it with your answer. Thanks.
                    – <a href="/users/2939000/hqcasanova" title="1,088 reputation" target="_blank">hqcasanova</a>
                <a href="#comment41733482_25137269" target="_blank">Oct 24 '14 at 20:43</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-48560146">
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
                I don't get it, when I view that example the margins are collapsing (only 10px vertical space between the divs instead of 20px)
                    – <a href="/users/200224/andy" title="2,990 reputation" target="_blank">Andy</a>
                <a href="#comment48560146_25137269" target="_blank">May 14 '15 at 2:25</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-49915302">
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
                This helps only in removing the collapse between siblings that all have this clearfix applied. I've forked the example to demonstrate this: <a href="http://jsfiddle.net/dpyuyg07/" target="_blank">jsfiddle.net/dpyuyg07</a> --- and even that is not the whole story. It only removes the collapse of margins stemming from children of the elements where you've applied that fix. If you would add a margin on the container itself the margins would still collapse, which can be seen in this fork: <a href="http://jsfiddle.net/oew7qsjx/" target="_blank">jsfiddle.net/oew7qsjx</a>
                    – <a href="/users/3651406/nicbright" title="2,065 reputation" target="_blank">NicBright</a>
                <a href="#comment49915302_25137269" target="_blank">Jun 19 '15 at 14:07</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-49915594">
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
                I can put this even more precisely: the clearfix method only prevents margin collapse between parents and children. It does not affect the collapse between adjacent siblings.
                    – <a href="/users/3651406/nicbright" title="2,065 reputation" target="_blank">NicBright</a>
                <a href="#comment49915594_25137269" target="_blank">Jun 19 '15 at 14:14</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-55841817">
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
                I think I now understand Bootstrap's tendency to fill the DOM with <code>:before</code> and <code>:after</code> elements. I have now added this rule to my stylesheet: <code>div:before, div:after{content: ' '; display: table;}</code>. Fantastic. Suddenly stuff starts to behave as expected.
                    – <a href="/users/286685/stijn-de-witt" title="15,074 reputation" target="_blank">Stijn de Witt</a>
                <a href="#comment55841817_25137269" target="_blank">Dec 2 '15 at 13:15</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-27283750">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Every webkit based browser should support the properties -webkit-margin-collapse. There are also subproperties to only set it for the top or bottom margin. You can give it the values collapse (default), discard (sets margin to 0 if there is a neighboring margin), and separate (prevents margin collapse).</p>

<p>I've tested that this works on 2014 versions of Chrome and Safari. Unfortunately, I don't think this would be supported in IE because it's not based on webkit.</p>

<p>Read <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266--webkit-margin-bottom-collapse" target="_blank">Apple's Safari CSS Reference</a> for a full explanation.</p>

<p>If you check <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Webkit_Extensions" target="_blank">Mozilla's CSS webkit extensions page</a>, they list these properties as proprietary and recommend not to use them. This is because they're likely not going to go into standard CSS anytime soon and only webkit based browsers will support them.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 3 '14 at 23:39
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-27283750">
                <ul>



    <li id="comment-49930947">
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
                This is nice because it helps us iron out an inconsistency in how Safari and Chrome deal with margins.
                    – <a href="/users/239078/bjudson" title="2,908 reputation" target="_blank">bjudson</a>
                <a href="#comment49930947_27283750" target="_blank">Jun 19 '15 at 22:44</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-33132624">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        28
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>One neat trick to disable margin collapsing that has no visual impact, as far as I know, is setting the padding of the parent to <code>0.1px</code>:</p>

<pre><code>.parentClass {
    padding: 0.1px;
}</code></pre>

<p>The padding is no longer 0 so collapsing won't occur anymore and the padding is less than 0.5px so visually it will round down to 0. </p>

<p>If some other padding is desired, then apply padding only to the "direction" in which margin collapsing is not desired, for example <code>padding-top: 0.1px;</code>.</p>

<p><strong>Working example:</strong>
</p><div>
<div>
<pre><code>.noCollapse {
  padding: 0.1px;
}

.parent {
  background-color: red;
  width: 150px;
}

.children {
  margin-top: 50px;

  background-color: lime;      
  width: 100px;
  height: 100px;
}</code></pre>
<pre><code>&lt;h3&gt;Border collapsing&lt;/h3&gt;
&lt;div class="parent"&gt;
  &lt;div class="children"&gt;
  &lt;/div&gt;
&lt;/div&gt;

&lt;h3&gt;No border collapsing&lt;/h3&gt;
&lt;div class="parent noCollapse"&gt;
  &lt;div class="children"&gt;
  &lt;/div&gt;
&lt;/div&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    
</div>
    
    <div>
	    <div id="comments-33132624">
                <ul>



    <li id="comment-58673419">
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
                This is my favorite solution. You could even include this as a default style. Why not? <code>*{padding-top:0.1px}</code>. Are we sure it works in all browsers though?
                    – <a href="/users/1763217/nick-manning" title="1,913 reputation" target="_blank">Nick Manning</a>
                <a href="#comment58673419_33132624" target="_blank">Feb 18 '16 at 19:07</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-58865537">
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
                Worked pretty nice so far for me, but I don't claim to have tested it thoroughly in most browsers.
                    – <a href="/users/460750/nicolae-surdu" title="4,340 reputation" target="_blank">Nicolae Surdu</a>
                <a href="#comment58865537_33132624" target="_blank">Feb 23 '16 at 22:35</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-58880271">
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
                Very nice solution, it seems to work as expected on most browsers. Thanks for sharing it!
                    – <a href="/users/2350638/wiredolphin" title="510 reputation" target="_blank">wiredolphin</a>
                <a href="#comment58880271_33132624" target="_blank">Feb 24 '16 at 9:09</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-79791177">
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
                This is a dodgy solution as it <i>does</i> add extra pixels in various circumstances, due to high-DPI displays and subpixel calculations. (Firefox has done subpixel layout for ages, I believe other browsers have comparatively recently followed suit.)
                    – <a href="/users/497043/chris-morgan" title="52,093 reputation" target="_blank">Chris Morgan</a>
                <a href="#comment79791177_33132624" target="_blank">Sep 26 '17 at 2:04</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-37481793">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I know that this is a very old post but just wanted to say that using flexbox on a parent element would disable margin collapsing for its child elements.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 27 '16 at 11:01
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-37481793">
                <ul>



    <li id="comment-80583727">
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
                Not only for its child elements – it also prevents margin collapsing between parent and first and last child.
                    – <a href="/users/279627/sven-marnach" title="296,859 reputation" target="_blank">Sven Marnach</a>
                <a href="#comment80583727_37481793" target="_blank">Oct 18 '17 at 19:56</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-37562505">
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
<p>I had similar problem with margin collapse because of parent having <code>position</code> set to relative. Here are list of commands you can use to disable margin collapsing.  </p>

<h1>HERE IS PLAYGROUND TO TEST</h1>

<p>Just try to assign any <code>parent-fix*</code> class to <code>div.container</code> element, or any class <code>children-fix*</code> to <code>div.margin</code>. Pick the one that fits your needs best.</p>



<ul>
<li>margin <strong>collapsing</strong> is <strong>disabled</strong>, <code>div.absolute</code> with red background will be positioned at the very top of the page.</li>
<li><strong>margin is collapsing</strong> <code>div.absolute</code> will be positioned at the same Y coordinate as <code>div.margin</code></li>
</ul>

<div>
<div>
<pre><code>html, body { margin: 0; padding: 0; }

.container {
  width: 100%;
  position: relative;
}

.absolute {
  position: absolute;
  top: 0;
  left: 50px;
  right: 50px;
  height: 100px;
  border: 5px solid #F00;
  background-color: rgba(255, 0, 0, 0.5);
}

.margin {
  width: 100%;
  height: 20px;
  background-color: #444;
  margin-top: 50px;
  color: #FFF;
}

/* Here are some examples on how to disable margin 
   collapsing from within parent (.container) */
.parent-fix1 { padding-top: 1px; }
.parent-fix2 { border: 1px solid rgba(0,0,0, 0);}
.parent-fix3 { overflow: auto;}
.parent-fix4 { float: left;}
.parent-fix5 { display: inline-block; }
.parent-fix6 { position: absolute; }
.parent-fix7 { display: flex; }
.parent-fix8 { -webkit-margin-collapse: separate; }
.parent-fix9:before {  content: ' '; display: table; }

/* Here are some examples on how to disable margin 
   collapsing from within children (.margin) */
.children-fix1 { float: left; }
.children-fix2 { display: inline-block; }</code></pre>
<pre><code>&lt;div class="container parent-fix1"&gt;
  &lt;div class="margin children-fix"&gt;margin&lt;/div&gt;
  &lt;div class="absolute"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
<p>Here is <strong><a href="https://jsfiddle.net/buksy/a6wseknw/" target="_blank">jsFiddle</a></strong> with example you can edit</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-45707542">
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
<p>For your information you could use
grid but with side effects :)</p>

<pre><code>.parent {
  display: grid
}</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 16 '17 at 7:30
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-47351270">
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
<p>Actually, there is one that works flawlessly:</p>

<p>display: flex;
flex-direction: column;</p>

<blockquote>
  <p><em>as long as you can live with supporting only IE10 and up</em></p>
</blockquote>

<div>
<div>
<pre><code>.container {
  display: flex;
  flex-direction: column;
    background: #ddd;
    width: 15em;
}

.square {
    margin: 15px;
    height: 3em;
    background: yellow;
}</code></pre>
<pre><code>&lt;div class="container"&gt;
    &lt;div class="square"&gt;&lt;/div&gt;
    &lt;div class="square"&gt;&lt;/div&gt;
    &lt;div class="square"&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;div class="container"&gt;
    &lt;div class="square"&gt;&lt;/div&gt;
    &lt;div class="square"&gt;&lt;/div&gt;
    &lt;div class="square"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Nov 17 '17 at 13:01
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>
                


                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/css" title="show questions tagged 'css'" target="_blank">css</a> <a href="/questions/tagged/css3" title="show questions tagged 'css3'" target="_blank">css3</a> <a href="/questions/tagged/margin" title="show questions tagged 'margin'" target="_blank">margin</a> <a href="/questions/tagged/collapse" title="show questions tagged 'collapse'" target="_blank">collapse</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
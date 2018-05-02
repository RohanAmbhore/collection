<a href="https://stackoverflow.com/questions/8498357/when-should-i-use-html5-sessionstorage">https://stackoverflow.com/questions/8498357/when-should-i-use-html5-sessionstorage</a><div id="articleHeader"><h1>When should I use html5 sessionStorage?</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        17
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="Click to mark as favorite question (click again to undo)" target="_blank">favorite</a>
        <div><b>4</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I've learned difference between <code>sessionStorage</code> (persist during session) and <code>localStorage</code> (persist forever if not deleted).</p>

<p>I can see that <code>localStorage</code> can be used as better version of cookie. (more size, not traveling to server for each HTTP request like cookie does).</p>

<p>But for <code>sessionStorage</code>, I'm thinking <strong>when should I use it effectively?</strong></p>

<p>I thought about user inputs into text fields in pageA and then moves onto pageB within the same tab or browser window, pageB can look up sessionStorage.</p>

<p>I can't really expand my guess more than the scenario above. Could anyone tell me how can sessionStorage be used?</p>
    </div>
    
    
</div>

                
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-8498542">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        19
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>With ajax-driven dynamic interfaces, a lot of times there is nothing storing the current state of how the interface looks (like which tab is selected, for example). <code>sessionStorage</code> could be used to store the state of the interface, so when coming back to a page, you can restore the screen the way the user was looking at it.</p>

<p>Another use would be if several pages deep you are working on a single object, you could store the id like a global variable: <code>currentInvoiceId</code>.</p>

<p>User settings that are needed on every page, like a special layout or template, could be loaded once up front and put into <code>sessionStorage</code> for easy access.</p>

<p>Some things you only want the user to see once per login, like a news popup. You could store that they've seen it already in <code>sessionStorage</code>. This would also work for actions that you only want the user to do once per login.</p>

<p>It's a good alternative to passing data between pages using viewstate, hidden <code>&lt;input&gt;</code> fields, or URL parameters.</p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-8498542">
                <ul>



    <li id="comment-10518659">
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
                Interesting, i can finally remove those ugly hidden input or div from HTML pages :)
                    – <a href="/users/355044/masato-san" title="6,226 reputation" target="_blank">masato-san</a>
                <a href="#comment10518659_8498542" target="_blank">Dec 14 '11 at 2:56</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-61074456">
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
                Is there any good use for sessionStorage in single page apps where the state can be easily stored in memory (javascript object)?
                    – <a href="/users/1815446/pau-frac%c3%a9s" title="764 reputation" target="_blank">Pau Fracés</a>
                <a href="#comment61074456_8498542" target="_blank">Apr 20 '16 at 14:19</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-61141121">
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
                @PauFracés Maybe just preserving state in case the browser crashes. Sucks to fill out a form, have your browser crash, and losing everything.
                    – <a href="/users/918414/thinkingstiff" title="55,040 reputation" target="_blank">ThinkingStiff</a>
                <a href="#comment61141121_8498542" target="_blank">Apr 22 '16 at 0:00</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-61164640">
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
                @ThinkingStiff is sessionStorage preserved after browser crash?
                    – <a href="/users/1815446/pau-frac%c3%a9s" title="764 reputation" target="_blank">Pau Fracés</a>
                <a href="#comment61164640_8498542" target="_blank">Apr 22 '16 at 13:26</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-61172960">
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/html" title="show questions tagged 'html'" target="_blank">html</a> <a href="/questions/tagged/html5" title="show questions tagged 'html5'" target="_blank">html5</a> <a href="/questions/tagged/local-storage" title="show questions tagged 'local-storage'" target="_blank">local-storage</a> <a href="/questions/tagged/web-storage" title="show questions tagged 'web-storage'" target="_blank">web-storage</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
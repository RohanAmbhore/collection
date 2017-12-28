<a href="https://stackoverflow.com/questions/2474009/browser-size-width-and-height/2474211">https://stackoverflow.com/questions/2474009/browser-size-width-and-height/2474211</a><div id="articleHeader"><h1>Browser size (width and height)</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        41
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>8</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I'm trying to detect the browser's current size (width and height). I know it's super easy in jQuery with <code>$(document).width and $(document).height</code>, but I don't want to add the size of the jQuery lib to the project, so I'd rather just use built in JavaScript. What would be the short and efficient way to do the same thing with JavaScript?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-2474009">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-2474211">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        69
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<pre><code>// first get the size from the window
// if that didn't work, get it from the body
var size = {
  width: window.innerWidth || document.body.clientWidth,
  height: window.innerHeight || document.body.clientHeight
}</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-2474211">
		        <table>
                    <tbody>



    <tr id="comment-2495056">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                body size is not the same as window size, which it the desired one actually.
                    – <a href="/users/104380/vsync" title="36,300 reputation" target="_blank">vsync</a>
                <a href="#comment2495056_2474211" target="_blank">Mar 23 '10 at 14:29</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-2495129">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                4
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This can be optimized using short circuit operators. ex: <code>width: window.innerWidth || document.body.clientWidth</code>
                    – <a href="/users/102451/peter-di-cecco" title="1,273 reputation" target="_blank">Peter Di Cecco</a>
                <a href="#comment2495129_2474211" target="_blank">Mar 23 '10 at 14:36</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-2495246">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @vsync, that is true, but window size is not defined by all browsers. @Peter, good point. I'll update that.
                    – <a href="/users/65611/joel" title="16,218 reputation" target="_blank">Joel</a>
                <a href="#comment2495246_2474211" target="_blank">Mar 23 '10 at 14:45</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-2474211">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-2474031">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Try this;</p>

<pre><code> &lt;script type="text/javascript"&gt; 
winwidth=document.all?document.body.clientWidth:window.innerWidth; 
winHeight=document.all?document.body.clientHeight:window.innerHeight; 
alert(winwidth+","+winHeight);
&lt;/script&gt; </code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Mar 18 '10 at 23:24
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
	    <div id="comments-2474031">
		        <table>
                    <tbody>



    <tr id="comment-2464944">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                You shouldn't use a browser check like <code>document.all</code> instead check that clientWidth is not undefined.
                    – <a href="/users/65611/joel" title="16,218 reputation" target="_blank">Joel</a>
                <a href="#comment2464944_2474031" target="_blank">Mar 18 '10 at 23:27</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-2465009">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @Joel, Why not, can you please contribute your answer. Thanks
                    – <a href="/users/296992/dono" title="208 reputation" target="_blank">dono</a>
                <a href="#comment2465009_2474031" target="_blank">Mar 18 '10 at 23:47</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-2465064">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                4
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Just because a browser does or does not implement <code>document.all</code> does not mean it does or does not implement <code>document.body.clientHeight</code>. You should check the property you want, not an unrelated property.
                    – <a href="/users/65611/joel" title="16,218 reputation" target="_blank">Joel</a>
                <a href="#comment2465064_2474031" target="_blank">Mar 19 '10 at 0:04</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-2495065">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                that gives the body height, not the browser height.
                    – <a href="/users/104380/vsync" title="36,300 reputation" target="_blank">vsync</a>
                <a href="#comment2495065_2474031" target="_blank">Mar 23 '10 at 14:29</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-2474031">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-2474677">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<pre><code>function getWindowSize(){
 var d= document, root= d.documentElement, body= d.body;
 var wid= window.innerWidth || root.clientWidth || body.clientWidth, 
 hi= window.innerHeight || root.clientHeight || body.clientHeight ;
 return [wid,hi]
}</code></pre>

<p>IE browsers are the only ones who don't use innerHeight and Width.</p>

<p>But there is no 'standard'- just browser implementations.</p>

<p>Test the html (document.documentElement) clientHeight before checking the body-
if it is not 0, it is the height of the 'viewport' and the body.clientHeight is the height of the body- which can be larger or smaller than the window.</p>

<p>Backwards mode returns 0 for the root element and the window (viewport) height from the body.</p>

<p>Same with width.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-2474677">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-11460486">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>My case use for <code>window.innerWidth</code> involved building a custom modal pop up window. Simply put, the user clicks the button, the pop up opens centered in the browser and there is a transparent black bkgd behind the pop up. My issue was finding the width and height of the browser to create the transparent bkgd. </p>

<p>The <code>window.innerWidth</code> works great to find the width but remember <code>window.innerWidth and window.innerHeight</code> do not compensate for the scroll bars, so if your content goes beyond the visible content area. I had to subtract 17px from the value.</p>

<pre><code>transBkgd.style.width = (window.innerWidth - 17) + "px";</code></pre>

<p>Since the content of the site always went beyond the visible height I couldnt use <code>window.innerHeight</code>. If the user scrolled down the transparent bkgd would end at that point and that just looked nasty. In order to maintain the transparent bkgd all the way to the bottom of the content I used <code>document.body.clientHeight</code>.</p>

<pre><code>transBkgd.style.height = document.body.clientHeight + "px";</code></pre>

<p>I Tested the pop up in IE, FF, Chrome, and it looks good across the board. I know this doesnt follow the original question too much but I figure it might help if anyone else runs into the same issue when creating a custom modal pop up. </p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-11460486">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-15996322">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Here is a code sample</p>

<pre><code>function getSize(){

var w=window.innerWidth || document.documentElement.clientWidth || document.body.clientWidth;

var h=window.innerHeight || document.documentElement.clientHeight ||document.body.clientHeight;


}</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 14 '13 at 6:16
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
	    

        <div id="comments-link-15996322">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/jquery" title="show questions tagged 'jquery'" target="_blank">jquery</a> <a href="/questions/tagged/browser" title="show questions tagged 'browser'" target="_blank">browser</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
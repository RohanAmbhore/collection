<a href="https://stackoverflow.com/questions/36238366/how-to-make-browser-window-draggable">https://stackoverflow.com/questions/36238366/how-to-make-browser-window-draggable</a><div id="articleHeader"><h1>How to make Browser Window draggable?</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        3
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="Click to mark as favorite question (click again to undo)" target="_blank">favorite</a>
        


</div>

            </div>

            
<div>
    <div>

<p>I have a Browser Window (using Electron.atom.io) and I'm trying to make it so that you can click over most of the screen (except inputs, etc) and drag it over your desktop - basically, I don't want to restrict drag just to the title bar.</p>

<p>Does anyone know how I might be able to do this?</p>
    </div>
    <div>
        <a href="/questions/tagged/electron" title="show questions tagged 'electron'" target="_blank">electron</a> 
    </div>
    <table>
    <tbody><tr>
    <td>
        
    </td>
    <td>
        <div>
    <div>
        asked Mar 26 '16 at 17:18
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</div>

                
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-36243066">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>Electron supports a webkit property intended for frameless windows, that I believe should work for you. The documentation is <a href="https://github.com/atom/electron/blob/master/docs/api/frameless-window.md#draggable-region" target="_blank">here</a>. Basically just make a class and add it to any elements you want draggable:</p>

<pre><code>.draggable {
    -webkit-app-region: drag;
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
        answered Mar 27 '16 at 1:59
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</div>
    
    <div>
	    <div id="comments-36243066">
                <ul>



    <li id="comment-60121180">
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
                This works perfectly! Also, as an added note for others, I'm disabling the selection of text in some areas, so it works a little more like a native app. (e.g. Dashlane for an example)
                    – <a href="/users/1715187/lindsay" title="371 reputation" target="_blank">Lindsay</a>
                <a href="#comment60121180_36243066" target="_blank">Mar 27 '16 at 9:13</a>
                        
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/electron" title="show questions tagged 'electron'" target="_blank">electron</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
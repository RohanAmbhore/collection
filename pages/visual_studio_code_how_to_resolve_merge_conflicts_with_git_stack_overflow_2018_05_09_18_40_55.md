<a href="https://stackoverflow.com/questions/38216541/visual-studio-code-how-to-resolve-merge-conflicts-with-git/38216625">https://stackoverflow.com/questions/38216541/visual-studio-code-how-to-resolve-merge-conflicts-with-git/38216625</a><div id="articleHeader"><h1>Visual Studio Code how to resolve merge conflicts with git?</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        11
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>3</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I tried to merge my branch with another branch and there was a merge conflict. In Visual Studio Code (version 1.2.1) I resolved all of the issues, however when I try to commit it keeps giving me this message:</p>

<blockquote>
  <p>You should first resolve the un-merged changes before committing your changes.</p>
</blockquote>

<p>I've tried googling it but I can't find out why it won't let me commit my changes, all of the conflicts have disappeared.</p>
    </div>
    
    <div>
    

    <div>
        <div>
    <div>
        asked Jul 6 '16 at 4:56
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-38216625">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        9
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>After trial and error I discovered that you need to stage the file that had the merge conflict, then you can commit the merge.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jul 6 '16 at 5:05
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-38216647">
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
<p>The error message you are getting is a result of Git still thinking that you have not resolved the merge conflicts.  In fact, you already have, but you need to tell Git that you have done this by <em>adding</em> the resolved files to the index.</p>

<p>This has the side effect that you could actually just add the files <em>without</em> resolving the conflicts, and Git would still think that you have.  So you should be diligent in making sure that you have really resolved the conflicts.  You could even run the build and test the code before you commit.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jul 6 '16 at 5:07
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-44682439">
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
<p>With VSCode you can find the merge conflicts easily. 
<a href="https://i.stack.imgur.com/9Yz5D.jpg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/9Yz5D.jpg" alt="enter image description here" /></div></a></p>

<p>It indicates the current change what you have and incoming change from the server. This makes easy to resolve the conflicts - just press the buttons above "&lt;&lt;&lt;&lt; HEAD".</p>

<p>If you have multiple changes and want to apply all of them at once - open command palette (View -&gt; Command Palette) and start typing merge - multiple options will appear including <code>Merge Conflict: Accept Incoming</code>, etc. </p>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/git" title="show questions tagged 'git'" target="_blank">git</a> <a href="/questions/tagged/visual-studio" title="show questions tagged 'visual-studio'" target="_blank">visual-studio</a> <a href="/questions/tagged/merge" title="show questions tagged 'merge'" target="_blank">merge</a> <a href="/questions/tagged/visual-studio-code" title="show questions tagged 'visual-studio-code'" target="_blank">visual-studio-code</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
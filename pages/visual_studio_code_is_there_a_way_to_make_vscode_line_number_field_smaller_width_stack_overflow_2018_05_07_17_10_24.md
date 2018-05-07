<a href="https://stackoverflow.com/questions/44912058/is-there-a-way-to-make-vscode-line-number-field-smaller-width">https://stackoverflow.com/questions/44912058/is-there-a-way-to-make-vscode-line-number-field-smaller-width</a><div id="articleHeader"><h1>Is there a way to make vscode line number field smaller width?</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        4
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>3</b></div>


</div>

            </div>

            
<div>
    <div>

<p>The vertical column that contains the code line number is VSC is too wide. Is there a way to narrow it down? </p>

<p><a href="https://i.stack.imgur.com/oMfez.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer float"><img src="https://i.stack.imgur.com/oMfez.png" alt="vsc view of line numbers" /></div></a></p>
    </div>
    <div>
        <a href="/questions/tagged/visual-studio-code" title="show questions tagged 'visual-studio-code'" target="_blank">visual-studio-code</a> 
    </div>
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-44920117">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        12
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>You can't change the size of this column.</p>

<p>Actually there are three columns:</p>

<p><a href="https://i.stack.imgur.com/VxCyG.jpg" target="_blank" class="readableLinkWithMediumImage"><img src="https://i.stack.imgur.com/VxCyG.jpg" alt="enter image description here" /></a></p>

<ul>
<li>left of the linenumber is the column called <code>glyphMargin</code>, the place to set debugging breakpoints (red dot). (When you edit settings, the column displays a pen when you point on the line as seen in the screenshots below)</li>
<li>the line number itself</li>
<li>right of it you can fold/unfold your code.</li>
</ul>

<p>If all three are active, it looks like this (settings) or a like above (code)</p>

<p><a href="https://i.stack.imgur.com/iJZWA.jpg" target="_blank" class="readableLinkWithMediumImage"><img src="https://i.stack.imgur.com/iJZWA.jpg" alt="enter image description here" /></a></p>

<p>To save space you can </p>

<ul>


<li><p>if you don't use the debugger, disable the <code>glyphMargin</code>:</p>

<pre><code>"editor.glyphMargin": false
</code></pre>

</li>
</ul>

<p>This is probably not what you want, but if you don't use code folding or the debugger or don't need linenumbers, you can at least save a little bit of space.
To change these settings press <kbd>ctrl</kbd><kbd>,</kbd> or click on the menu file/preferences/settings.</p>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/visual-studio-code" title="show questions tagged 'visual-studio-code'" target="_blank">visual-studio-code</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
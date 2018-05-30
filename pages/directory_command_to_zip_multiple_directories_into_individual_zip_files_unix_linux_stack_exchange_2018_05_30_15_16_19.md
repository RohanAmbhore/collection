<a href="https://unix.stackexchange.com/questions/68489/command-to-zip-multiple-directories-into-individual-zip-files">https://unix.stackexchange.com/questions/68489/command-to-zip-multiple-directories-into-individual-zip-files</a><div id="articleHeader"><h1><a href="/questions/68489/command-to-zip-multiple-directories-into-individual-zip-files" target="_blank">command to zip multiple directories into individual zip files</a></h1></div>
            

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        33
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>22</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I have a single directory that contains dozens of directories inside of it.</p>

<p>I'm new to command line and I'm struggling to come up with a command that will zip each sub-directory into a unique sub-directory.zip file.</p>

<p>So in the end my primary directory will be filled with all of my original sub-directories, plus the corresponding <code>.zip</code> files that contain the zipped up content of each sub-directory.</p>

<p>Is something like this possible? If so, please show me how it's done.</p>
    </div>
    
    
</div>

                
    <div>
	    

        <div id="comments-link-68489">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </div>        </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-68490">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        56
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>You can use this loop in <code>bash</code>:</p>

<pre><code>for i in */; do zip -r "${i%/}.zip" "$i"; done
</code></pre>

<p><code>i</code> is the name of the loop variable. <code>*/</code> means every subdirectory of the current directory, and will include a trailing slash in those names. Make sure you <code>cd</code> to the right place before executing this. <code>"$i"</code> simply names that directory, including trailing slash. The quotation marks ensure that whitespace in the directory name won't cause trouble. <code>${i%/}</code> is like <code>$i</code> but with the trailing slash removed, so you can use that to construct the name of the zip file.</p>

<p>If you want to see how this works, include an <code>echo</code> before the <code>zip</code> and you will see the commands printed instead of executed.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 19 '13 at 21:30
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-68490">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>1</b> more comment</a>
        </div>         
    </div>    </div>
</div>
                    <div>
        <h2>                    <b>protected</b> by <a href="/users/-1/community" target="_blank">Community</a>♦ Nov 2 '13 at 14:37
</h2>
        <p>
Thank you for your interest in this question. 
Because it has attracted low-quality or spam answers that had to be removed, posting an answer now requires 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).
<br /><br />Would you like to answer one of these <a href="/unanswered?fromProtectedNotice=true" target="_blank">unanswered questions</a> instead?</p>
    </div>





                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/command-line" title="show questions tagged 'command-line'" target="_blank">command-line</a> <a href="/questions/tagged/directory" title="show questions tagged 'directory'" target="_blank">directory</a> <a href="/questions/tagged/zip" title="show questions tagged 'zip'" target="_blank">zip</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
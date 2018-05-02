<a href="https://unix.stackexchange.com/questions/76870/cat-files-in-current-folder-and-all-subfolders">https://unix.stackexchange.com/questions/76870/cat-files-in-current-folder-and-all-subfolders</a><div id="articleHeader"><h1>                    <b>marked</b> as duplicate by <a href="/users/33055/anthon" target="_blank">Anthon</a>, <a href="/users/7453/slm" target="_blank">slm</a>♦, <a href="/users/10412/manatwork" target="_blank">manatwork</a>, <a href="/users/6761/jasonwryan" target="_blank">jasonwryan</a>, <a href="/users/28489/runium" target="_blank">Runium</a> May 24 '13 at 9:44</h1></div>
        <p>This question has been asked before and already has an answer. If those answers do not fully address your question, please <a href="/questions/ask" target="_blank">ask a new question</a>.</p>
    
            
    
    <div>
	    

        <div id="comments-link-76870">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
            




        <div id="answers">

                
                




  

<div id="answer-76871">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        22
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            
            


<div>
    <div>


<pre><code>   find . -type f -exec cat {} +</code></pre>
    </div>
    

    
    <div>
	    

        <div id="comments-link-76871">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
        


  

<div id="answer-76881">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        13
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            
            


<div>
    <div>
<p>cat accepts multiple arguments, so you can:</p>

<pre><code>  cat * */*</code></pre>

<p>to cat everything in the current directory and in all subdirectories.  You can also</p>

<pre><code>  cat * */* */*/*</code></pre>

<p>and so on, if you want.</p>

<p>Note, of course, that your shell is translating those '*'s into a list of files then passing that whole list to cat.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 23 '13 at 23:53
    </div>
    
    

    
    

    
    <div>
	    

        <div id="comments-link-76881">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
        

                


                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/shell" title="show questions tagged 'shell'" target="_blank">shell</a> <a href="/questions/tagged/directory" title="show questions tagged 'directory'" target="_blank">directory</a> <a href="/questions/tagged/cat" title="show questions tagged 'cat'" target="_blank">cat</a> <a href="/questions/tagged/tree" title="show questions tagged 'tree'" target="_blank">tree</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            
        
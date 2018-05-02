<a href="https://unix.stackexchange.com/questions/179346/why-does-find-exec-cmd-need-to-end-in">https://unix.stackexchange.com/questions/179346/why-does-find-exec-cmd-need-to-end-in</a><div id="articleHeader"><h1><a href="/questions/179346/why-does-find-exec-cmd-need-to-end-in" target="_blank">Why does 'find -exec cmd {} +' need to end in '{} +'?</a></h1></div>
            

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        6
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="Click to mark as favorite question (click again to undo)" target="_blank">favorite</a>
        <div><b>3</b></div>


</div>

            </div>

            
<div>
    <div>

<p>Preface: I understand the difference between <code>-exec {} \;</code> & <code>-exec {} +</code>. I also don't have a problem <em>as such</em>, I am just curious about the semantics of <code>find</code>.</p>

<hr />

<p>When ending the <code>-exec</code> argument with <code>+</code> instead of <code>;</code>, we <em>need</em> to end this with <code>{} +</code>, for example:</p>

<pre><code># FreeBSD find
$ find . -type f -exec cp {} /tmp +
find: -exec: no terminating ";" or "+"

# GNU find is even more cryptic:
$ find: missing argument to `-exec'
</code></pre>

<p>Using <code>;</code> in these examples instead of <code>+</code> works fine (but obviously does something else).</p>

<p>From <a href="http://pubs.opengroup.org/onlinepubs/9699919799/utilities/find.html" target="_blank">POSIX</a>:</p>

<blockquote>
  <p><code>-exec  <i>utility_name</i>  [<i>argument</i> ...] ;</code><br />
  <code>-exec  <i>utility_name</i>  [<i>argument</i> ...]  {} +</code>  </p>
  
  <p>...   Only a &lt;plus-sign&gt; that immediately follows an argument containing only the two characters "<code>{}</code>" shall punctuate the end of the primary expression. 
  Other uses of the &lt;plus-sign&gt; shall not be treated as special.</p>
</blockquote>

<p>In other words, when using the <code>+</code>, the command <em>needs</em> to end with <code>{} +</code>.</p>

<p>Why is this? And why only with the <code>+</code> and not the <code>;</code>? At first I thought maybe to avoid conflicts with filenames that contain a <code>+</code>, but filenames with a <code>;</code> seem to work fine? I find it hard to believe this limitation is arbitrary ...</p>
    </div>
    
    
</div>

                
    <div>
	    

        <div id="comments-link-179346">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </div>        </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-179383">
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
<p>The <a href="http://pubs.opengroup.org/onlinepubs/009695399/utilities/find.html#tag_04_55_18" target="_blank">rationale</a> given in the POSIX specification is:</p>

<blockquote>
  <p>The <code>"-exec ... {} +"</code> syntax adopted was a result of IEEE PASC Interpretation 1003.2 #210. It should be noted that this is an incompatible change to the ISO/IEC 9899:1999 standard. For example, the following command prints all files with a <code>'-'</code> after their name if they are regular files, and a <code>'+'</code> otherwise:</p>

<pre><code>find / -type f -exec echo {} - ';' -o -exec echo {} + ';'
</code></pre>
  
  <p>The change invalidates usage like this. Even though the previous standard stated that this usage would work, in practice many did not support it and the standard developers felt it better to now state that this was not allowable.</p>
</blockquote>

<p><a href="https://collaboration.opengroup.org/external/pasc.org/interpretations/unofficial/db/p1003.2/pasc-1003.2-210.html" target="_blank">PASC Interpretation 1003.2 #210</a> goes into more detail about the history of <code>-exec … {} +</code>. It existed on several Unix systems before it was adopted by POSIX; the defect report traces it back to <a href="https://en.wikipedia.org/wiki/UNIX_System_V#SVR4" target="_blank">SVR4</a> (where it was largely undocumented). The defect report justifies the incompatible change as having little impact in practice:</p>

<blockquote>
  <p>Note that the "+" is only treated as special if it immediately
  follows "{}".  This minimises the chances of causing problems with
  existing uses of "+" as an argument with "-exec".</p>
</blockquote>

<p>Although adding support for <code>-exec … {} +</code> would break some conforming applications such as the example above, there are fewer of these than if <code>-exec … {} … +</code> was allowed.</p>

<p>Another reason, perhaps, to restrict <code>{}</code> to be the last argument is ease of implementation. If <code>{}</code> was allowed anywhere in the argument list to <code>-exec</code>, the <code>find</code> program would have to build the command line by copying the static arguments, then the variable part, then another static part. This would make it harder to construct the argument list and to account for the size limit. The difficulty is minimal, but implementers like to cut corners. Supporting multiple substitutable instances of <code>{}</code> (if <code>-exec {} foo +</code> is to work, it can be logically expected that <code>-exec {} foo {} +</code> would as well) would be significantly harder.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 16 '15 at 1:43
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-179383">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/find" title="show questions tagged 'find'" target="_blank">find</a> <a href="/questions/tagged/history" title="show questions tagged 'history'" target="_blank">history</a> <a href="/questions/tagged/posix" title="show questions tagged 'posix'" target="_blank">posix</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
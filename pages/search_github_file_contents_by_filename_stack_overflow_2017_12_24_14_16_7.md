<a href="https://stackoverflow.com/questions/41858706/search-github-file-contents-by-filename">https://stackoverflow.com/questions/41858706/search-github-file-contents-by-filename</a><div id="articleHeader"><h1>Search github file contents by filename</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        0
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>1</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I am trying to identify use cases of a specific python package on github. </p>

<p>Is there a way you could search all <code>requirements.txt</code> files on repositories written in python for a string ?</p>
    </div>
    
    <table>
    <tbody><tr>
    <td>
        
    </td>
    <td>
        <div>
    <div>
        asked Jan 25 at 18:14
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-41858706">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-41860005">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<h3>From the Web UI</h3>

<p>In <a href="https://github.com/search" target="_blank">https://github.com/search</a>, type :</p>

<pre><code>django filename:requirements.txt language:python in:requirements.txt
</code></pre>

<p><a href="https://github.com/search?utf8=%E2%9C%93&q=django%20filename%3Arequirements.txt%20language%3Apython%20in%3Arequirements.txt&ref=simplesearch" target="_blank">like this</a> :
<a href="https://i.stack.imgur.com/XqvNn.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/XqvNn.png" alt="enter image description here" /></div></a></p>

<h3>From Github API</h3>

<pre><code>https://api.github.com/search/code?q=django+in:requirements.txt+filename:requirements.txt+language:python+org:openmicroscopy
</code></pre>

<p>For the Github API case, you have to give a user, an organization or a repository</p>

<p>Check <a href="https://developer.github.com/v3/search/#search-code" target="_blank">Search Code doc</a></p>

<p>Note that filename filter & string data are no exact match </p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jan 25 at 19:27
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
	    

        <div id="comments-link-41860005">

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
Not the answer you're looking for?                            Browse other questions tagged   or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
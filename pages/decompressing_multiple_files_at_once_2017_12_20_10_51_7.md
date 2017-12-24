<a href="https://askubuntu.com/questions/431478/decompressing-multiple-files-at-once/431488">https://askubuntu.com/questions/431478/decompressing-multiple-files-at-once/431488</a><div id="articleHeader"><h1><a href="/questions/431478/decompressing-multiple-files-at-once" target="_blank">Decompressing multiple files at once</a></h1></div>
            

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        24
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>9</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I have more than 200 <code>.zip</code> files in one folder. I don't want to decompress those one by one. I want to extract those using single command or script. How to do that.</p>
    </div>
    <div>
        <a href="/questions/tagged/bash" title="show questions tagged 'bash'" target="_blank">bash</a> 
    </div>
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-431478">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-431488">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        34
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>If you really want to uncompress them in parallel, you could do</p>

<pre><code>for i in *zip; do unzip "$i" & done</code></pre>

<p>That however, will launch N processes for N .zip files and could be very heavy on your system. For a more controlled approach, launching only 10 parallel processes at a time, try this:</p>

<pre><code>find . -name '*.zip' -print0 | xargs -0 -I {} -P 10 unzip {}</code></pre>

<p>To control the number of parallel processes launched, change <code>-P</code> to whatever you want. If you don't want recurse into subdirectories, do this instead:</p>

<pre><code>find . -maxdepth 1 -name '*.zip' -print0 | xargs -0 -I {} -P 10 unzip {}</code></pre>

<p>Alternatively, you can install <a href="https://www.gnu.org/software/parallel/" target="_blank">GNU parallel</a> as suggested by @OleTange in the comments and run</p>

<pre><code>parallel unzip ::: *zip</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-431488">
		        <table>
                    <tbody>



    <tr id="comment-562965">
        <td>
            
        </td>
        <td>
            <div>
                Running in parallel is a nice idea, but won't disk I/O be the major bottleneck?
                    – <a href="/users/2088/paddy-landau" title="2,858 reputation" target="_blank">Paddy Landau</a>
                <a href="#comment562965_431488" target="_blank">Mar 12 '14 at 13:05</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-562966">
        <td>
            
        </td>
        <td>
            <div>
                @PaddyLandau not sure, I'd have to check. It will depend on the speed of the decompression algorithm vs the speed of the disk I imagine.
                    – <a href="/users/85695/terdon" title="55,652 reputation" target="_blank">terdon♦</a>
                <a href="#comment562966_431488" target="_blank">Mar 12 '14 at 13:08</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-562967">
        <td>
            
        </td>
        <td>
            <div>
                Use <code>-exec</code> or <code>-execdir</code> instead of piping to <code>xargs</code>. Not only is it simpler to understand, but also it's also less error-prone and uses fewer system resources. <code>find . -name '*.zip' -exec unzip {} ';'</code> (You must quote the semi-colon.)
                    – <a href="/users/2088/paddy-landau" title="2,858 reputation" target="_blank">Paddy Landau</a>
                <a href="#comment562967_431488" target="_blank">Mar 12 '14 at 13:10</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-562969">
        <td>
            
        </td>
        <td>
            <div>
                @PaddyLandau the only reason I'm piping to xargs is to run things in <i>parallel</i> as the OP asked. <code>-exec \;</code> (you can escape the semicolon, no need for quotes), will run each command sequentially. <code>-exec +</code> is better but it won't work here since that's not how <code>unzip</code> works.
                    – <a href="/users/85695/terdon" title="55,652 reputation" target="_blank">terdon♦</a>
                <a href="#comment562969_431488" target="_blank">Mar 12 '14 at 13:13</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-563342">
        <td>
            
        </td>
        <td>
            <div>
                I think that we have understood the OP differently. You read him as wanting it in parallel, whereas I understood him as meaning a single command instead of multiple commands. Well, he has both methods now :)
                    – <a href="/users/2088/paddy-landau" title="2,858 reputation" target="_blank">Paddy Landau</a>
                <a href="#comment563342_431488" target="_blank">Mar 12 '14 at 21:44</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-431488">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-431676">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        16
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>The <a href="http://www.gnu.org/software/parallel/" target="_blank">GNU parallel</a> command is well suited to this type of thing.  After:</p>

<pre><code>$ sudo apt-get install parallel</code></pre>



<pre><code>ls *.zip | parallel unzip</code></pre>

<p>This will use as many cores as you have, keeping each core busy with an unzip, until they are all done.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-431676">
		        <table>
                    <tbody>



    <tr id="comment-560540">
        <td>
            
        </td>
        <td>
            <div>
                It's a better idea to use <code>echo *.zip</code> instead to prevent a possible ls alias from sneaking in extra info. However, this has the same issue as @Guru's answer, it breaks on file names containing whitespace.
                    – <a href="/users/7509/nyuszika7h" title="167 reputation" target="_blank">nyuszika7h</a>
                <a href="#comment560540_431676" target="_blank">Mar 9 '14 at 13:38</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-560564">
        <td>
            
        </td>
        <td>
            <div>
                @nyuszika7h In contrast to <code>xargs</code> GNU Parallel does <i>not</i> break on file names containing space/tab/quote. Only if the file names contain newlines you will have to take extra care. For example by using: <code>parallel unzip ::: *.zip</code>
                    – <a href="/users/22307/ole-tange" title="903 reputation" target="_blank">Ole Tange</a>
                <a href="#comment560564_431676" target="_blank">Mar 9 '14 at 14:12</a>
                        
                                                                            </div>
        </td>
    </tr>
    
    <tr id="comment-560644">
        <td>
            
        </td>
        <td>
            <div>
                @nyuszika7h - These are good reasons to avoid <i>both</i> aliasing standard commands, <i>and</i> putting spaces in filenames.
                    – <a href="/users/249010/wayne-conrad" title="269 reputation" target="_blank">Wayne Conrad</a>
                <a href="#comment560644_431676" target="_blank">Mar 9 '14 at 15:50</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-561229">
        <td>
            
        </td>
        <td>
            <div>
                @NateEldredge While that chance was bigger back in the time when systems had only one magnetic disk, these days with RAIDs with multiple spindles and flash disk that chance is smaller. The best thing to do is of course to measure and see how <i>your</i> system behaves. I recently used a 40 spindle RAID where the optimal parallelism for I/O hungry processes was 10: It did not give a 10x speed up - only a 6x, but fewer than 10 processes gave less than 6x.
                    – <a href="/users/22307/ole-tange" title="903 reputation" target="_blank">Ole Tange</a>
                <a href="#comment561229_431676" target="_blank">Mar 10 '14 at 8:58</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-431676">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>12</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-431481">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        12
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>You can use the following command :</p>

<p>First change directory in terminal to directory that contains .zip files :</p>

<pre><code>cd /path</code></pre>

<p>Then execute this command to unzip all .zip files :</p>

<pre><code>for z in *.zip; do unzip "$z"; done</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-431481">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-431480">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        10
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If you have many <code>.zip</code> files in your folder and you want to decompress all of them then open terminal and go to your folder using:</p>

<pre><code>cd &lt;path_to_folder&gt;</code></pre>

<p>Now use this command to decompress all your <code>.zip</code> file:</p>

<pre><code>ls *.zip | xargs -n1 unzip</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-431480">
		        <table>
                    <tbody>



    <tr id="comment-560210">
        <td>
            
        </td>
        <td>
            <div>
                This will fail if any of the file names contain whitespace.
                    – <a href="/users/85695/terdon" title="55,652 reputation" target="_blank">terdon♦</a>
                <a href="#comment560210_431480" target="_blank">Mar 8 '14 at 20:22</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-560212">
        <td>
            
        </td>
        <td>
            <div>
                yes, you are correct.
                    – <a href="/users/146791/g-p" title="10,719 reputation" target="_blank">g_p</a>
                <a href="#comment560212_431480" target="_blank">Mar 8 '14 at 20:23</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-560538">
        <td>
            
        </td>
        <td>
            <div>
                It's a better idea to use <code>echo *.zip</code> instead to prevent a possible <code>ls</code> alias from sneaking in extra info, however that still does not fix the whitespace issue.
                    – <a href="/users/7509/nyuszika7h" title="167 reputation" target="_blank">nyuszika7h</a>
                <a href="#comment560538_431480" target="_blank">Mar 9 '14 at 13:37</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-560660">
        <td>
            
        </td>
        <td>
            <div>
                @OleTange In case you didn't notice, I said that it still fails on file names with whitespace in them.
                    – <a href="/users/7509/nyuszika7h" title="167 reputation" target="_blank">nyuszika7h</a>
                <a href="#comment560660_431480" target="_blank">Mar 9 '14 at 15:59</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-562964">
        <td>
            
        </td>
        <td>
            <div>
                Never depend on the output from <code>ls</code> for scripts, as its output is not well-defined between versions. Instead look at the answer from @terdon as it solves all the problems of this solution.
                    – <a href="/users/2088/paddy-landau" title="2,858 reputation" target="_blank">Paddy Landau</a>
                <a href="#comment562964_431480" target="_blank">Mar 12 '14 at 13:04</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-431480">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-432020">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>You can use find with <code>-exec</code> like so,</p>

<pre><code>find . -name "*.zip" -exec unzip {} \;</code></pre>

<p>This <strong>will</strong> work if the file has a space in the name.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-432020">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-431692">
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
<p>A non terminal method.</p>

<p>Just select the zip files, right click on one and choose <code>extract here</code>. You can select all or just a number of zip files at a time.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Mar 9 '14 at 12:07
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
	    

        <div id="comments-link-431692">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-432024">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p><code>unzip \*.zip</code> or <code>unzip '*.zip'</code></p>

<p>The obvious <code>unzip *.zip</code> doesn't work, because the shell expands it to <code>unzip foo.zip bar.zip ...</code> and <code>unzip</code> interprets the first filename as the zip file, and the following filenames as files to extract from that zip file.</p>

<p>However, <code>unzip</code> is a bit unusual among Unix commands in that it does its own glob expansions.  If the <code>*</code> is not expanded by the shell, unzip will do it, and intepret all the resulting filenames as zip files to be processed.  So in this special case, one can get away without a <code>for</code> loop or <code>xargs</code> or the like.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-432024">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


        






                            <div>
                                
                                            <div>
        
                <div>
                    <div>
                        <h3>Sign up or <a href="/users/login?ssrc=question_page&returnurl=https%3a%2f%2faskubuntu.com%2fquestions%2f431478%2fdecompressing-multiple-files-at-once%23new-answer" id="login-link" target="_blank">log in</a></h3>
                        
                        <div>
                             Sign up using Google
                        </div>
                        <div>
                             Sign up using Facebook
                        </div>
                        <div>
                             Sign up using Email and Password
                        </div>
                    </div>
                    
                    
                    
                    
                    <div>
                                <h3>Post as a guest</h3>
    <div>
        <table>
        <tbody><tr>
                    <td>
                <div>
                    <label>Name</label>
                    
                </div>
                <div>
                    <label>Email</label>
                    
                </div>
            </td>
        </tr>
        </tbody></table>
    </div>

                    </div>
                </div>
            </div>
            
            

                            </div>

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>

<p>
By posting your answer, you agree to the <a href="https://stackexchange.com/legal/privacy-policy" name="privacy" target="_blank">privacy policy</a> and <a href="https://stackexchange.com/legal/terms-of-service" name="tos" target="_blank">terms of service</a>.</p>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/bash" title="show questions tagged 'bash'" target="_blank">bash</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
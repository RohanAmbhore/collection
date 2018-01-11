<a href="https://stackoverflow.com/questions/20931909/too-many-open-files-while-ensure-index-mongo">https://stackoverflow.com/questions/20931909/too-many-open-files-while-ensure-index-mongo</a><div id="articleHeader"><h1>Too many open files while ensure index mongo</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        3
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>2</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I would like to create text index on mongo collection. I write </p>

<pre><code>db.test1.ensureIndex({'text':'text'})</code></pre>

<p>and then i saw in mongod process</p>

<pre><code>Sun Jan  5 10:08:47.289 [conn1] build index library.test1 { _fts: "text", _ftsx: 1 }
Sun Jan  5 10:09:00.220 [conn1]         Index: (1/3) External Sort Progress: 200/980    20%
Sun Jan  5 10:09:13.603 [conn1]         Index: (1/3) External Sort Progress: 400/980    40%
Sun Jan  5 10:09:26.745 [conn1]         Index: (1/3) External Sort Progress: 600/980    61%
Sun Jan  5 10:09:37.809 [conn1]         Index: (1/3) External Sort Progress: 800/980    81%
Sun Jan  5 10:09:49.344 [conn1]      external sort used : 5547 files  in 62 secs
Sun Jan  5 10:09:49.346 [conn1] Assertion: 16392:FileIterator can't open file: data/_tmp/esort.1388912927.0//file.233errno:24 Too many open files</code></pre>

<p>I work on MaxOSX 10.9.1.
Please help.</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-20931909">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-23524857">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>I've had the same problem (executing a different operation, but still, a "Too many open files" error), and as lese says, it seems to be down to the 'maxfiles' limit on the machine running mongod.</p>

<p>On a mac, it is better to check limits with:</p>

<pre><code>sudo launchctl limit</code></pre>

<p>This gives you: </p>

<pre><code>&lt;limit name&gt; &lt;soft limit&gt; &lt;hard limit&gt;
    cpu         unlimited      unlimited      
    filesize    unlimited      unlimited      
    data        unlimited      unlimited      
    stack       8388608        67104768       
    core        0              unlimited      
    rss         unlimited      unlimited      
    memlock     unlimited      unlimited      
    maxproc     709            1064           
    maxfiles    1024           2048  </code></pre>

<p>What I did to get around the problem was to temporarily set the limit higher (mine was originally something like soft: 256, hard: 1000 or something weird like that):</p>

<pre><code>sudo launchctl limit maxfiles 1024 2048</code></pre>

<p>Then re-run the query/indexing operation and see if it breaks. If not, and to keep the higher limits (they will reset when you log out of the shell session you've set them on), create an '/etc/launchd.conf' file with the following line:</p>

<pre><code>limit maxfiles 1024 2048</code></pre>

<p>(or add that line to your existing launchd.conf file, if you already have one).</p>

<p>This will set the maxfile via launchctl on every shell at login.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-23524857">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-44304254">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I added a temporary <code>ulimit -n 4096</code> before the restore command.
also you can use 
<code>mongorestore --numParallelCollections=1 ...</code> and that seems to help.
But still the connection pool seems to get exhausted.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jun 1 '17 at 9:52
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
	    <div id="comments-44304254">
		        <table>
                    <tbody>



    <tr id="comment-75616219">
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
                <code>sudo launchctl limit maxfiles 512 1024</code> would cause my system to crash, at least with zsh <code>update_terminalapp_cwd:4: pipe failed: too many open files in system                                                                                                       zsh: pipe failed: too many open files in system sudo launchctl limit maxfiles 512 update_terminalapp_cwd:4: pipe failed: too many open files in system                                                                                                       zsh: pipe failed: too many open files in system</code>
                    – <a href="/users/1146785/dcsan" title="2,439 reputation" target="_blank">dcsan</a>
                <a href="#comment75616219_44304254" target="_blank">Jun 1 '17 at 10:52</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-44304254">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-20932525">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        4
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>it may be related to <a href="http://docs.mongodb.org/manual/reference/ulimit/" target="_blank">this</a> </p>

<p>try to check your system configuration issuing the following command in terminal </p>

<blockquote>
  <p>ulimit -a</p>
</blockquote>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jan 5 '14 at 10:33
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
	    

        <div id="comments-link-20932525">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/mongodb" title="show questions tagged 'mongodb'" target="_blank">mongodb</a> <a href="/questions/tagged/macos" title="show questions tagged 'macos'" target="_blank">macos</a> <a href="/questions/tagged/full-text-search" title="show questions tagged 'full-text-search'" target="_blank">full-text-search</a> <a href="/questions/tagged/database" title="show questions tagged 'database'" target="_blank">database</a> <a href="/questions/tagged/nosql" title="show questions tagged 'nosql'" target="_blank">nosql</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
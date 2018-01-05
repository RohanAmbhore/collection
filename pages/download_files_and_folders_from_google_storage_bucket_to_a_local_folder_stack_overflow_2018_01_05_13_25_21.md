<a href="https://stackoverflow.com/questions/11640637/download-files-and-folders-from-google-storage-bucket-to-a-local-folder">https://stackoverflow.com/questions/11640637/download-files-and-folders-from-google-storage-bucket-to-a-local-folder</a><div id="articleHeader"><h1>Download files and folders from Google Storage bucket to a local folder</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        21
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>9</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>What's the best way to download all files from Google Cloud Storage?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-11640637">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-11640830">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        26
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>Take a look of the <a href="https://developers.google.com/storage/docs/gsutil/commands/cp" target="_blank">gsutil tool</a>. You can use the cp command with the <code>-R</code> (recursive) and <code>-m</code> (multithreading) option. </p>

<pre><code>gsutil -m cp -R gs://&lt;bucket_name&gt; .
</code></pre>

<p>And if you want to try it with a public bucket try</p>

<pre><code>gsutil -m cp -R gs://uspto-pair .
</code></pre>

<p>The speedup granted by multithreading can be quite significant:</p>

<pre><code>$ time gsutil cp -R gs://uspto-pair/docs/2010-08-28 .
...

real    0m12.534s
</code></pre>



<pre><code>$ time gsutil -m cp -R gs://uspto-pair/docs/2010-08-28 .
...

real    0m3.345s
</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-11640830">
		        <table>
                    <tbody>



    <tr id="comment-16807573">
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
                I'd suggest <i>not</i> blindly downloading the uspto-pair bucket - there are a bunch of documents in there...
                    – <a href="/users/1612/cebjyre" title="5,092 reputation" target="_blank">Cebjyre</a>
                <a href="#comment16807573_11640830" target="_blank">Sep 19 '12 at 9:01</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-63428102">
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
                A very important thing here, is to install gsutil <b>on your local machine</b>. You can for example do that by installing the Google Cloud SDK. This step I forgot and kept using gsutil on my project's local VM like an idiot.
                    – <a href="/users/5272567/matthias" title="1,351 reputation" target="_blank">Matthias</a>
                <a href="#comment63428102_11640830" target="_blank">Jun 23 '16 at 12:55</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-11640830">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-37859542">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>In my case, what worked was navigating to the bucket in the browser gui and left clicking the file and "Save file".<br />
This is obviously terrible for multiple files, but you can compress them of course to one file (using the google cloud console).</p>

<p>see <a href="https://stackoverflow.com/questions/18794522/how-to-download-from-google-cloud-storage" target="_blank">this</a> thread.</p>

<p>Also, if you don't have a bucket, you can <a href="https://console.cloud.google.com/storage" target="_blank">create one</a>, and then upload to it using gcloud console, e.g. <code>gsutil cp file.tgz gs://&lt;bucket&gt;</code> </p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-37859542">
		        <table>
                    <tbody>



    <tr id="comment-63427998">
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
                I just realized why Sebastian's answer didn't work for me.. for some reason I was totally blind to the fact I needed to have the gsutil <b>installed on my local machine</b>. Kept using it in the gcloud console in-browser downloading to my project VM there.
                    – <a href="/users/5272567/matthias" title="1,351 reputation" target="_blank">Matthias</a>
                <a href="#comment63427998_37859542" target="_blank">Jun 23 '16 at 12:53</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-37859542">

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
        
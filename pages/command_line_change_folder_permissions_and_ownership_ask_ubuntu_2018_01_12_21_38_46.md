<a href="https://askubuntu.com/questions/6723/change-folder-permissions-and-ownership">https://askubuntu.com/questions/6723/change-folder-permissions-and-ownership</a><div id="articleHeader"><h1><a href="/questions/6723/change-folder-permissions-and-ownership" target="_blank">Change folder permissions and ownership</a></h1></div>
            

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        344
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>176</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I would like the user to have full rights on this folder (as well as all sub-directories and files in it):</p>

<pre><code>~/.blabla
</code></pre>

<p>currently owned by root.</p>

<p>I have found numerous posts (in this forum and elsewhere) on how to do this for files but I can't find a way to do it for whole folders.</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-6723">
		        <table>
                    <tbody>



    <tr id="comment-6816">
        <td>
            
        </td>
        <td>
            <div>
                Could anyone add a graphical method I wonder?
                    – <a href="/users/866/8128" title="24,020 reputation" target="_blank">8128</a>
                <a href="#comment6816_6723" target="_blank">Oct 13 '10 at 19:23</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-6821">
        <td>
            
        </td>
        <td>
            <div>
                @fluteflute is there a graphical method?
                    – <a href="/users/41/marco-ceppi" title="34,471 reputation" target="_blank">Marco Ceppi♦</a>
                <a href="#comment6821_6723" target="_blank">Oct 13 '10 at 19:33</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-6822">
        <td>
            
        </td>
        <td>
            <div>
                <code>gksu nautilus</code> perhaps. I'm not quite sure and would like to know.... ;)
                    – <a href="/users/866/8128" title="24,020 reputation" target="_blank">8128</a>
                <a href="#comment6822_6723" target="_blank">Oct 13 '10 at 19:39</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-6723">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-6727">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        541
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>Use <code>chown</code> to change ownership and <code>chmod</code> to change rights.</p>

<p>As Paweł Karpiński said, use the -R option to apply the rights for all files inside of a directory too.</p>

<p>Note that both these commands just work for directories too. The -R option makes them also change the permissions for all files and directories inside of the directory.</p>

<p>For example</p>

<pre><code>sudo chown -R username:group directory
</code></pre>

<p>will change ownership (both user and group) of all files and directories inside of <code>directory</code> and <code>directory</code> itself.</p>

<pre><code>sudo chown username:group directory
</code></pre>

<p>will only change the permission of the folder <code>directory</code> but will leave the files and folders inside the directory alone.</p>

<p>As enzotib mentioned, you need to use <code>sudo</code> to change the ownership from root to yourself.</p>

<p><em>Edit:</em></p>

<p>Note that if you use <code>chown &lt;user&gt;: &lt;file&gt;</code> (Note the left-out group), it will use the default group for that user. </p>

<p>If you want to change only the group, you can use:</p>

<pre><code>chown :&lt;group&gt; &lt;file&gt;
</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-6727">
		        <table>
                    <tbody>



    <tr id="comment-6634">
        <td>
            
        </td>
        <td>
            <div>
                It should be said that "sudo" is required for chown.
                    – <a href="/users/2647/enzotib" title="54,613 reputation" target="_blank">enzotib</a>
                <a href="#comment6634_6727" target="_blank">Oct 13 '10 at 9:45</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-6636">
        <td>
            
        </td>
        <td>
            <div>
                fatanstic. You should consider maybe replacing 'user:user' by username.
                    – <a href="/users/2413/user2413" title="3,049 reputation" target="_blank">user2413</a>
                <a href="#comment6636_6727" target="_blank">Oct 13 '10 at 9:48</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-528821">
        <td>
            
        </td>
        <td>
            <div>
                Although I have changed the owner and group to Me and my group, I cannot edit the file acpi-support. Why? Thx.
                    – <a href="/users/170070/kin" title="1,761 reputation" target="_blank">Kin</a>
                <a href="#comment528821_6727" target="_blank">Jan 26 '14 at 5:48</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-1363279">
        <td>
            
        </td>
        <td>
            <div>
                The predefined variables helped me: <code>sudo chown -R $USER:$USER /path/to/dir</code>. Thanks!
                    – <a href="/users/619172/samuel-elh" title="103 reputation" target="_blank">Samuel Elh</a>
                <a href="#comment1363279_6727" target="_blank">Jan 27 '17 at 13:13</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-1460013">
        <td>
            
        </td>
        <td>
            <div>
                BEWARE of recursively taking ownership of ANY directory. Think before you leap. Don't be <code>chown</code> copypastin' from the internet, kids. Just because you want to install a node package and it won't let you, don't <code>sudo chown -R</code> just because the fist hit from googling the error message says to. Reckless <code>sudo chown -R</code>-ing can kill your OS.
                    – <a href="/users/182590/benjamin-r" title="313 reputation" target="_blank">Benjamin R</a>
                <a href="#comment1460013_6727" target="_blank">Jun 10 '17 at 3:06</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-6727">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>5</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-6735">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        66
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Make the current user own everything inside the folder (and the folder itself):</p>

<pre><code>sudo chown -R $USER ~/.blabla
</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-6735">
		        <table>
                    <tbody>



    <tr id="comment-106214">
        <td>
            
        </td>
        <td>
            <div>
                very helpful for newbies (like me) when don't know what to type in 'usergroup' for <code>sudo chown &lt;your username&gt;:&lt;your usergroup&gt; -R &lt;path to&gt;/.blabla</code>
                    – <a href="/users/13036/quantme" title="133 reputation" target="_blank">quantme</a>
                <a href="#comment106214_6735" target="_blank">Jan 5 '12 at 1:49</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-6735">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-6968">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        52
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If you prefer, this can be done with a GUI as well. You will need to open Nautilus as root to do so. Press <kbd>Alt</kbd> + <kbd>F2</kbd> to access the "Run Applications" dialog and enter <code>gksu nautilus</code></p>

<p>Next, browse to and right click on the folder you would like to modify. Then, select "Properties" from the context menu. You can now select the user or group that you would like to be the "Owner" of the folder as well as the permissions you would like to grant them. Finally, press "Apply Permissions to Enclosed Files" to apply the changes recursively.</p>

<p>Though it seems this does not always work for some operations in a deep folder tree. If it does not work use the appropriate terminal command.</p>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/770Gq.png" alt="alt text" /></div></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-6968">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-6748">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        24
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If it's owned by root you can do this</p>

<pre><code>sudo chown &lt;your username&gt;:&lt;your usergroup&gt; -R &lt;path to&gt;/.blabla
</code></pre>

<p>Since ./blabla owned by root you need to gain root privileges to change that. That's what sudo will do. The -R option for the chown command says: this directory and everything in it recursively.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Oct 13 '10 at 11:14
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
	    

        <div id="comments-link-6748">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-6725">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>you should try <code>chmod -R</code></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-6725">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                    <div>
        <h2>                    <b>protected</b> by <a href="/users/-1/community" target="_blank">Community</a>♦ Feb 21 '14 at 7:21
</h2>
        <p>
Thank you for your interest in this question. 
Because it has attracted low-quality or spam answers that had to be removed, posting an answer now requires 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).
<br /><br />Would you like to answer one of these <a href="/unanswered?fromProtectedNotice=true" target="_blank">unanswered questions</a> instead?</p>
    </div>





                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/command-line" title="show questions tagged 'command-line'" target="_blank">command-line</a> <a href="/questions/tagged/permissions" title="show questions tagged 'permissions'" target="_blank">permissions</a> <a href="/questions/tagged/folder" title="show questions tagged 'folder'" target="_blank">folder</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
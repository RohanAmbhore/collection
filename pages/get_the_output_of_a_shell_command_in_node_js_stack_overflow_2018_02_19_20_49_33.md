<a href="https://stackoverflow.com/questions/12941083/get-the-output-of-a-shell-command-in-node-js">https://stackoverflow.com/questions/12941083/get-the-output-of-a-shell-command-in-node-js</a><div id="articleHeader"><h1>Get the output of a shell command in node.js</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        56
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>20</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>In a node.js, I'd like to find a way to obtain the output of a Unix terminal command. Is there any way to do this?</p>

<pre><code>function getCommandOutput(commandString){
    //now how can I implement this function?
    //getCommandOutput("ls") should print the terminal output of the shell command "ls"
}</code></pre>
    </div>
    <div>
        <a href="/questions/tagged/node.js" title="show questions tagged 'node.js'" target="_blank">node.js</a> 
    </div>
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-12941083">
                <ul>



    <li id="comment-17540157">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
    <li id="comment-17541549">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-12941083">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-12941186">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        79
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>Thats the way I do it in a project I am working now.</p>

<pre><code>var exec = require('child_process').exec;
function execute(command, callback){
    exec(command, function(error, stdout, stderr){ callback(stdout); });
};</code></pre>

<p>Example: Retrieving git user</p>

<pre><code>module.exports.getGitUser = function(callback){
    execute("git config --global user.name", function(name){
        execute("git config --global user.email", function(email){
            callback({ name: name.replace("\n", ""), email: email.replace("\n", "") });
        });
    });
};</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Oct 17 '12 at 18:47
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
	    <div id="comments-12941186">
                <ul>



    <li id="comment-17540316">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Is it possible to make this function return the command's output? (That's what I was trying to do.)
                    – <a href="/users/975097/anderson-green" title="9,447 reputation" target="_blank">Anderson Green</a>
                <a href="#comment17540316_12941186" target="_blank">Oct 17 '12 at 18:48</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-17540391">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                thats what that code does. take a look at the example at the edit I have just made
                    – <a href="/users/91403/renatoargh" title="8,538 reputation" target="_blank">renatoargh</a>
                <a href="#comment17540391_12941186" target="_blank">Oct 17 '12 at 18:51</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-31302669">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                @AndersonGreen You wouldn't want the function to return normally with the "return" keyboard, because it is running the shell command asynchronously. As a result, it's better to pass in a callback with code that should run when the shell command is complete.
                    – <a href="/users/406249/nick-mccurdy" title="5,800 reputation" target="_blank">Nick McCurdy</a>
                <a href="#comment31302669_12941186" target="_blank">Dec 31 '13 at 22:09</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-54053352">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Ouch, your first sample ignores the possibility of an error when it calls that callback. I wonder what happens to <code>stdout</code> if there is an error. Hopefully deterministic and documented.
                    – <a href="/users/1127972/doug65536" title="4,529 reputation" target="_blank">doug65536</a>
                <a href="#comment54053352_12941186" target="_blank">Oct 14 '15 at 8:18</a>
                        
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-12941186">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-12941138">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        18
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>You're looking for <a href="http://nodejs.org/api/child_process.html" target="_blank">child_process</a></p>

<pre><code>var exec = require('child_process').exec;
var child;

child = exec(command,
   function (error, stdout, stderr) {
      console.log('stdout: ' + stdout);
      console.log('stderr: ' + stderr);
      if (error !== null) {
          console.log('exec error: ' + error);
      }
   });</code></pre>

<hr />

<p>As pointed out by Renato, there are some synchronous exec packages out there now too, see <a href="http://davidwalsh.name/sync-exec" target="_blank">sync-exec</a> that might be more what yo're looking for. Keep in mind though, node.js is designed to be a single threaded high performance network server, so if that's what you're looking to use it for, stay away from sync-exec kinda stuff unless you're only using it during startup or something.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-12941138">
                <ul>



    <li id="comment-17540267">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                In this case, how can I obtain the output of the command? Is is "stdout" that contains the command-line output?
                    – <a href="/users/975097/anderson-green" title="9,447 reputation" target="_blank">Anderson Green</a>
                <a href="#comment17540267_12941138" target="_blank">Oct 17 '12 at 18:46</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-17540282">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Also, is it possible to do something similar without using a callback?
                    – <a href="/users/975097/anderson-green" title="9,447 reputation" target="_blank">Anderson Green</a>
                <a href="#comment17540282_12941138" target="_blank">Oct 17 '12 at 18:47</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-17540363">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Correct, stdout contains the output of the program. And no, it's not possible to do it without callbacks. Everything in node.js is oriented around being non-blocking, meaning every time you do IO you're going to be using callbacks.
                    – <a href="/users/438969/hexist" title="4,260 reputation" target="_blank">hexist</a>
                <a href="#comment17540363_12941138" target="_blank">Oct 17 '12 at 18:50</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-17540508">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Note that if you're looking for using javascript to do scripty kinda things where you really want to wait on output and that sort of thing, you might look at the v8 shell, d8
                    – <a href="/users/438969/hexist" title="4,260 reputation" target="_blank">hexist</a>
                <a href="#comment17540508_12941138" target="_blank">Oct 17 '12 at 18:55</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-17540525">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                @hexist there are some <code>Sync</code> methods natively available, even so IMHO it should be avoided
                    – <a href="/users/91403/renatoargh" title="8,538 reputation" target="_blank">renatoargh</a>
                <a href="#comment17540525_12941138" target="_blank">Oct 17 '12 at 18:55</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-12941138">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>4</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/node.js" title="show questions tagged 'node.js'" target="_blank">node.js</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
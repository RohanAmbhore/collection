<a href="https://apple.stackexchange.com/questions/225231/how-to-use-ssh-keys-and-disable-password-authentication">https://apple.stackexchange.com/questions/225231/how-to-use-ssh-keys-and-disable-password-authentication</a><div id="articleHeader"><h1><a href="/questions/225231/how-to-use-ssh-keys-and-disable-password-authentication" target="_blank">How to use SSH keys and disable password authentication</a></h1></div>
            

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        8
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>4</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I'm trying to access a Mac remotely (I do have physical access to this Mac) through SSH from a Linux client computer. My goal is to access this Mac from outside the network. Port forwarding is set up on the router. From my client computer I'm able to <code>ssh user@ip</code> for the public IP and I am able to get into the Mac, so port forwarding is working.</p>

<p>Now I want to set up SSH keys. I've generated SSH keys on my client computer but I wanted to get the SSH Daemon on the Mac setup first. I edited <code>/etc/ssh_config</code> and set <code>PasswordAuthentication no</code>. I restarted SSH with these commands: <code>sudo launchctl unload /System/Library/LaunchDaemons/ssh.plist</code>, then <code>sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist</code>. When I try to SSH in from the client again, it still asks for my password.</p>

<p>I took a look at <a href="https://apple.stackexchange.com/questions/34090/enabling-remote-login-without-password-authentication" target="_blank">this post</a> and from the answer I added <code>UsePAM no</code> to the config file and restarted the service with <code>launchctl</code> again. I'm still being prompted for a password.</p>

<p>I also tried the solution <a href="https://apple.stackexchange.com/questions/84523/disable-password-authentication-on-ssh-server-on-os-x-server-10-8" target="_blank">here</a>. I'm still being prompted for a password.</p>

<p>How do I set up my <code>ssh_config</code> to so that it doesn't ask for the password and only accepts SSH keys? Am I not restarting the daemon properly? Is there another step I am missing?</p>
    </div>
    
    
</div>

                
    <div>
	    

        <div id="comments-link-225231">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </div>        </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-225422">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>I was editing the wrong configuration file! Instead of <code>/etc/ssh_config</code>, I edited <code>private/etc/sshd_config</code>. I think this probably would have also worked if I edited <code>/etc/sshd_config</code> as per the updated answer from @GhostLyrics, but I didn't test that yet so I can't say for sure. After that, I restarted the service with <code>sudo launchctl stop com.openssh.sshd</code> and then <code>sudo launchctl start com.openssh.sshd</code> and I was able to get my desired behavior. Here is the resource where I found the pertinent information: <a href="https://superuser.com/questions/364304/how-do-i-configure-ssh-on-os-x" target="_blank">https://superuser.com/questions/364304/how-do-i-configure-ssh-on-os-x</a></p>

<p>Here are the config options I changed:</p>

<p><code>
PermitRootLogin no
PasswordAuthentication no
PermitEmptyPasswords no
ChallengeResponseAuthentication no
</code></p>

<p>After that I was successfully able to generate SSH keys on my client computer, moved the public key to <code>~/.ssh/authorized_keys</code> on the Mac and set permissions for that file to 644.</p>

<p>It is important to note that those permissions are for my <strong>public key</strong>. My <strong>private key</strong> permissions are set to 600 on my client computer. This is <em>really</em> important if you have both your public and private key in your <code>~/.ssh</code> folder and there are multiple users on the system. If your <strong>private key</strong> permissions are set to 644 then <em>any</em> user could read your private key and impersonate you. Also, the permissions for the <code>~/.ssh</code> folder should be 700.</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-225422">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-225232">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><code>/etc/ssh/ssh_config</code> is the configuration file for the client which is used if you don't have a more specific one in your home directory. What you want to edit is <code>/etc/ssh/sshd_config</code> which is the one for the server.</p>

<p>You will probably want to set <code>PermitRootLogin without-password</code> (or <code>no</code>) and <code>PasswordAuthentication no</code> there. </p>

<hr />

<p>Update:
Since you are running Yosemite, the file is <code>/etc/sshd_config</code> according to this answer: <a href="https://apple.stackexchange.com/a/167405/11135" target="_blank">https://apple.stackexchange.com/a/167405/11135</a></p>

<p>To further elaborate why it still prompts when setting <code>PasswordAuthentication no</code> in <code>/etc/ssh/ssh_config</code> it is important to understand what you configured. "When making an <em>outgoing</em> connection via SSH, don't offer password authentication." </p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-225232">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>1</b> more comment</a>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/macos" title="show questions tagged 'macos'" target="_blank">macos</a> <a href="/questions/tagged/ssh" title="show questions tagged 'ssh'" target="_blank">ssh</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
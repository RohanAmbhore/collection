<a href="https://unix.stackexchange.com/questions/20357/how-can-i-make-a-script-in-etc-init-d-start-at-boot">https://unix.stackexchange.com/questions/20357/how-can-i-make-a-script-in-etc-init-d-start-at-boot</a><div id="articleHeader"><h1><a href="/questions/20357/how-can-i-make-a-script-in-etc-init-d-start-at-boot" target="_blank">How can I make a script in /etc/init.d start at boot?</a></h1></div>
            

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        70
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>40</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I think  I read something a while back about this, but I can't remember how it's done. Essentially, I have a service in <code>/etc/init.d</code> which I'd  like to start automatically at boot time. I remember it has something to do with symlinking the script into the <code>/etc/rc.d</code> directory, but I can't remember at the present. What is the command for this? </p>

<p>I believe I'm on a Fedora/CentOS derivative.</p>
    </div>
    
    
</div>

                
    <div>
	    

        <div id="comments-link-20357">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </div>        </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-20361">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        90
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>If you are on a Red Hat based system, as you mentioned, you can do the following:</p>

<ol>
<li>Create a script and place in <code>/etc/init.d</code> (e.g <code>/etc/init.d/myscript</code>). The script should have the following format:</li>
</ol>

<pre><code>#!/bin/bash
# chkconfig: 2345 20 80
# description: Description comes here....

# Source function library.
. /etc/init.d/functions

start() {
    # code to start app comes here 
    # example: daemon program_name &
}

stop() {
    # code to stop app comes here 
    # example: killproc program_name
}

case "$1" in 
    start)
       start
       ;;
    stop)
       stop
       ;;
    restart)
       stop
       start
       ;;
    status)
       # code to check status of app comes here 
       # example: status program_name
       ;;
    *)
       echo "Usage: $0 {start|stop|status|restart}"
esac

exit 0 </code></pre>

<p>The format is pretty standard and you can view existing scripts in <code>/etc/init.d</code>. You can then use the script like so <code>/etc/init.d/myscript start</code> or <code>chkconfig myscript start</code>. The <code>ckconfig</code> man page explains the header of the script:</p>

<pre><code> &gt; This says that the script should be started in levels 2,  3,  4, and
 &gt; 5, that its start priority should be 20, and that its stop priority
 &gt; should be 80.
</code></pre>

<p>The example start, stop and status code uses helper functions defined in <code>/etc/init.d/functions</code></p>

<ol>
<li><p>Enable the script  </p>

<pre><code>$ chkconfig --add myscript 
$ chkconfig --level 2345 myscript on 
</code></pre></li>
<li><p>Check the script is indeed enabled - you should see "on" for the levels you selected. </p>

<pre><code>$ chkconfig --list | grep myscript
</code></pre></li>
</ol>

<p>Hope this is what you were looking for. </p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-20361">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>4</b> more comments</a>
        </div>         
    </div>    </div>
</div>

  

<div id="answer-20360">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        9
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>You test, what runlevel your machine normally starts into.</p>

<pre><code>runlevel
</code></pre>

<p>Often this is 5 or 2 - there are various conventions, but nothing really established, afaik. Ubuntu uses 2, while former distribution I used always used </p>

<ul>
<li>1 Single user (super user) </li>
<li>2 multi user</li>
<li>3 multi user + network </li>
<li>4 not used / user definable</li>
<li>5 multi user, network + X11 </li>
</ul>

<p>Then you make a symlink from your init-script, maybe <code>/etc/init.d/foobar</code> to <code>/etc/rc2.d/SXYfoobar</code> </p>

<p>S means 'Start this script in this runlevel (here: 2). 
XY is a two-digit decimal number, which is relevant for the sequence, the scripts are started. </p>

<p>If you depend on script S45barfoo to be run before you, and S55foofoo is depending on your script, you would choose xy between 45 and 55. For equal numbers the boot order is undefined. </p>

<p>Ubuntu meanwhile switched (is switching) to another startup procedure, called <code>upstart</code>. </p>

<p>And note: Not always the links link to <code>/etc/rcX.d</code> - sometimes it is <code>/etc/init/rcX.d</code> or something similar, but it should be easy to find, somewhere below /etc. </p>

<p>If you want to start something at the end of the starting scripts, <code>/etc/rc.local</code> would be file to look for, but if it depends on X11 already running, you might look for an autostart-option of your desktop environment, or <code>/etc/X11/Xsession.d/</code> with a similar pattern as described above.</p>

<p>If you depend on the network being up, there is a separate directory (if-up.d), and for mounted devices like external USB-drives <code>/etc/udev/rules.d/</code>. </p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-20360">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-95967">
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
<p>As Naftuli Tzvi Kay asked about Debian above: Beginning with Debian 6, your script should contain a LSB (Linux Standards Base) header which indicates its dependencies and capabilities (<a href="https://wiki.debian.org/LSBInitScripts" target="_blank">see debian wiki page</a>).</p>

<p>If a LSB header is present, you can use <code>insserv</code> to include your script in the boot process (<a href="https://wiki.debian.org/LSBInitScripts/DependencyBasedBoot" target="_blank">see another debian wiki page</a>).</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-95967">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


        






                            <div>
                                
                                            <div>
        
                <div>
                    <div>
                        <h3>Sign up or <a href="/users/login?ssrc=question_page&returnurl=https%3a%2f%2funix.stackexchange.com%2fquestions%2f20357%2fhow-can-i-make-a-script-in-etc-init-d-start-at-boot%23new-answer" id="login-link" target="_blank">log in</a></h3>
                        
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
                                            

By clicking "Post Your Answer", you acknowledge that you have read our updated <a href="https://stackoverflow.com/legal/terms-of-service/public" name="tos" target="_blank">terms of service</a>, <a href="https://stackoverflow.com/legal/privacy-policy" name="privacy" target="_blank">privacy policy</a> and <a href="https://stackoverflow.com/legal/cookie-policy" name="cookie" target="_blank">cookie policy</a>, and that your continued use of the website is subject to these policies.


                                        </p>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/fedora" title="show questions tagged 'fedora'" target="_blank">fedora</a> <a href="/questions/tagged/boot" title="show questions tagged 'boot'" target="_blank">boot</a> <a href="/questions/tagged/init-script" title="show questions tagged 'init-script'" target="_blank">init-script</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
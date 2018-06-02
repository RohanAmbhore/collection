<a href="https://superuser.com/questions/229773/run-command-on-startup-login-mac-os-x">https://superuser.com/questions/229773/run-command-on-startup-login-mac-os-x</a><div id="articleHeader"><h1><a href="/questions/229773/run-command-on-startup-login-mac-os-x" target="_blank">Run command on startup / login (Mac OS X)</a></h1></div>
            

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        47
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>31</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I was wondering which file I should place this bash command in so it will be run on startup.</p>

<pre><code># Start the MongoDB server
/Applications/MongoDB/bin/mongod --dbpath /usr/local/mongo/data --fork --logpath /usr/local/mongo/log
</code></pre>

<p>I have been scouring the net and think it is between <code>~/.bashrc</code>, <code>~/profile</code>, <code>/etc/bashrc</code>, <code>/etc/profile</code> or <code>~/.bash_profile</code>. Although I have tried these and they seem to run on <em>terminal startup</em> <strong>not</strong> <em>Mac startup</em>. Am I missing a file?</p>
    </div>
    
    
</div>

                
    <div>
	    

        <div id="comments-link-229773">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </div>        </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-229777">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        29
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>Officially none of these. The Apple suggested way is to use <a href="https://developer.apple.com/library/content/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html" target="_blank">launchd</a>. Guis to set this up include <a href="https://www.peterborgapps.com/lingon/" target="_blank">lingon</a> and <a href="http://www.soma-zone.com/LaunchControl/" target="_blank">Launch Control</a></p>

<p>As for the files you mention the ones in the home directory ~/.bashrc, ~/profile, ~/.bash_profile  are only started when you login via a terminal. The ones in /etc are run by the shell starting for all users before the ones in home directory but only when a user login is made.. <a href="http://www.faqs.org/docs/bashman/bashref_63.html" target="_blank">bash manual</a></p>

<p>The Unix startup script involved /etc/rc* but for OSX just use the launchd stuff</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-229777">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-229792">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        52
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>To run a command on start up on OS X, you need to use <code>launchd</code>.</p>

<p>If you don't want to use <a href="http://lingon.sourceforge.net/" target="_blank">Lingon</a>, you need to create a <code>launchd</code> Property List. This is an XML file, so you can do it with your favourite text editor or alternatively you can use the Property List Editor that's installed with the Mac OS X Dev Tools. Create the following:</p>

<pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd"&gt;
&lt;plist version="1.0"&gt;
&lt;dict&gt;
    &lt;key&gt;Label&lt;/key&gt;
    &lt;string&gt;some.meaningful.name&lt;/string&gt; &lt;!-- org.mongodb.mongodb perhaps? --&gt;

    &lt;key&gt;OnDemand&lt;/key&gt;
    &lt;false/&gt;

    &lt;key&gt;UserName&lt;/key&gt;
    &lt;string&gt;anAppropriateUser&lt;/string&gt;

    &lt;key&gt;GroupName&lt;/key&gt;
    &lt;string&gt;anAppropriateGroup&lt;/string&gt;

    &lt;key&gt;ProgramArguments&lt;/key&gt;
    &lt;array&gt;
            &lt;string&gt;/Applications/MongoDB/bin/mongod&lt;/string&gt;
            &lt;string&gt;--dbpath&lt;/string&gt;
            &lt;string&gt;/usr/local/mongo/data&lt;/string&gt;
            &lt;string&gt;--fork&lt;/string&gt;
            &lt;string&gt;--logpath&lt;/string&gt;
            &lt;string&gt;/usr/local/mongo/log&lt;/string&gt;
    &lt;/array&gt;
&lt;/dict&gt;
&lt;/plist&gt;
</code></pre>

<p>Save this in <code>/Library/LaunchAgents/some.meaningful.name.plist</code> (you will need an administrator account and/or <code>sudo</code>), then open a terminal and do:</p>

<pre><code>sudo launchctl load /Library/LaunchAgents/some.meaningful.name.plist
</code></pre>

<p>This will cause launchd to load the item which will cause it to start MongoDB on boot. As a bonus, <code>launchd</code> will monitor it and, if it exits for any reason, it will be re-started. To get rid of the item simply replace load in the above command with unload.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 6 '11 at 12:50
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-229792">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-465506">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        42
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><a href="https://stackoverflow.com/a/6445525/403616" target="_blank">Another simple solution from Stack Overflow</a>:
You can:</p>

<ul>
<li>Start Automator.app;  </li>
<li>Select "Application";  </li>
<li>Click "Show library" in the toolbar (if hidden);</li>
<li>Add "Run shell script" (from the Actions/Utilities);</li>
<li>Copy-and-paste your script into the window;</li>
<li>Test it;</li>
<li>Save it somewhere: a file called <code>your_name.app</code> will be created);</li>
<li>Depending your MacOSX version:

<ul>
<li><em>Old</em> versions: Go to System Preferences → Accounts → Login items, or</li>
<li><em>New</em> version: Go to System Preferences → Users and Groups → Login items (top right);</li>
</ul></li>
<li>Add this newly-created app;</li>
</ul>

<p>Log off, log back in, and you should be done. ;)</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-465506">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>1</b> more comment</a>
        </div>         
    </div>    </div>
</div>

  

<div id="answer-995564">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        23
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>To launch commands when logging in, you can do this:</p>

<ul>
<li><p>Create a text file containing your commands (bash script):</p>

<pre><code>#!/bin/bash

# Start the MongoDB server
/Applications/MongoDB/bin/mongod --dbpath /usr/local/mongo/data --fork --logpath /usr/local/mongo/log
</code></pre></li>
<li><p>Save this file in <code>~/Library/Startup.cmd</code></p></li>
<li>You can test it by double-clicking the file in the Finder</li>
<li>Make it executable: <code>chmod +x ~/Library/Startup.cmd</code></li>
<li>Add this file in System Preferences &gt; Accounts &gt; Login items</li>
</ul>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-995564">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-229776">
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
<p>You will have to look at how <code>launchd</code> and <code>launchctl</code> work on MacOS. You could start by reading the man pages for both the commands. You could then look inside <code>/Library/LaunchAgents/</code> and <code>/Library/LaunchDaemons/</code> for examples of how to set up applications to load at different times through the <code>launchctl</code> interface. </p>

<p><a href="https://stackoverflow.com/questions/3652351/creating-a-timed-launchd-plist" target="_blank">Here's an example</a> I found on Stack Overflow that might help you further.</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-229776">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-1056986">
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
<p>If you want an approach that will work on Linux & Mac OS X, a cron task should should be sufficient (edit your cron tasks by executing <code>crontab -e</code>):</p>

<pre><code>@reboot /path/to/script
</code></pre>

<p>(credits: <a href="https://unix.stackexchange.com/questions/49207/how-do-i-set-a-script-that-it-will-run-on-start-up-in-freebsd" target="_blank">https://unix.stackexchange.com/questions/49207/how-do-i-set-a-script-that-it-will-run-on-start-up-in-freebsd</a>) </p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-1056986">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-1325013">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I was interested in a very simple unix answer to this problem and found it at another <a href="https://coderwall.com/p/u003pa/bash-startup-scripts-on-linux-and-mac-os-x" target="_blank">site</a>.  Here is a summary of the solution.  </p>

<p>The standard for login shells is to always look for the bash configuration files with "profile" in the name, in this order: /etc/profile, ~/.bash_profile, then ~/.bash_login and lastly ~/.profile. When login shells exit, they read ~/.bash_logout.  </p>

<p>In my case I just created the ~/.bash_profile and then I opened the preferences for the Mac Terminal app and changed the "Shell opens with" option from default to /bin/bash.  That's it.  Clean and simple.  </p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-1325013">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-1187553">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>open terminal, type  </p>

<pre><code>nano ~/.bash_profile
</code></pre>

<p>then add this text to the file:</p>

<pre><code>/Applications/MongoDB/bin/mongod --dbpath /usr/local/mongo/data --fork logpath /usr/local/mongo/log
</code></pre>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-1187553">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


        






                            <div>
                                
                                            <div>
        
                <div>
                    <div>
                        <h3>Sign up or <a href="/users/login?ssrc=question_page&returnurl=https%3a%2f%2fsuperuser.com%2fquestions%2f229773%2frun-command-on-startup-login-mac-os-x%23new-answer" id="login-link" target="_blank">log in</a></h3>
                        
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/macos" title="show questions tagged 'macos'" target="_blank">macos</a> <a href="/questions/tagged/boot" title="show questions tagged 'boot'" target="_blank">boot</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
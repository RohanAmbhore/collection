<a href="https://stackoverflow.com/questions/11030552/what-does-rc-mean-in-dot-files">https://stackoverflow.com/questions/11030552/what-does-rc-mean-in-dot-files</a><div id="articleHeader"><h1>What does "rc" mean in dot files</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        149
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>39</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>In my home folder in Linux I have several config files that have "rc" as a file name extension:</p>

<pre><code>$ ls -a ~/|pcregrep 'rc$'
.bashrc
.octaverc
.perltidyrc
.screenrc
.vimrc
</code></pre>

<p>What does the "rc" in these names mean?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-11030552">
		        <table>
                    <tbody>



    <tr id="comment-14422963">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                14
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
            
        </td>
    </tr>
    <tr id="comment-14423160">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
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
            
        </td>
    </tr>
    <tr id="comment-29770239">
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
                @JoachimPileborg spoiler!
                    – <a href="/users/611007/n611x007" title="3,940 reputation" target="_blank">n611x007</a>
                <a href="#comment29770239_11030552" target="_blank">Nov 15 '13 at 7:08</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-64532555">
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
                I am more curious about how do programs 'know' which rc files to read from? For example, .vimrc is loaded before Vim starts. .pylintrc is loaded before pylint starts. I assume .bashrc is for the Terminal, but then again .bash_profile does the same. So were these file names pre-defined for each program and some, like the terminal, even recognize multiple configuration files?
                    – <a href="/users/1718916/sean" title="162 reputation" target="_blank">Sean</a>
                <a href="#comment64532555_11030552" target="_blank">Jul 25 '16 at 15:24</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-70704890">
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
                @Sean "So were these file names pre-defined for each program and some, like the terminal, even recognize multiple configuration files?" Yes.
                    – <a href="/users/1440565/code-apprentice" title="37,730 reputation" target="_blank">Code-Apprentice</a>
                <a href="#comment70704890_11030552" target="_blank">Jan 20 '17 at 5:04</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-11030552">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-11030607">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        141
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>Looks like one of the following:</p>

<pre><code>- run commands
- resource control
- run control
- runtime configuration
</code></pre>

<p>Also I've found a <a href="http://www.faqs.org/docs/artu/ch10s03.html#ftn.id2941902" target="_blank">citation</a>:</p>

<pre><code>The ‘rc’ suffix goes back to Unix's grandparent, CTSS.
It had a command-script feature called "runcom". Early
Unixes used ‘rc’ for the name of the operating system's
boot script, as a tribute to CTSS runcom.
</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-11030607">
		        <table>
                    <tbody>



    <tr id="comment-14423091">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
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
                yep there are a lot of different answers. just think of them as resource files and we are good :) I fav Runtime Configuration or resource control.
                    – <a href="/users/578822/prometheus" title="6,300 reputation" target="_blank">Prometheus</a>
                <a href="#comment14423091_11030607" target="_blank">Jun 14 '12 at 9:56</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-29124185">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                14
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
                The "rc" naming convention of "rc files" was inspired by the "runcom" facility mentioned above and does not stand for "resource configuration" or "runtime configuration" as is often wrongly guessed. <a href="http://en.wikipedia.org/wiki/Rc_file" target="_blank">en.wikipedia.org/wiki/Rc_file</a>
                    – <a href="/users/1040889/dan-k-k" title="2,916 reputation" target="_blank">Dan K.K.</a>
                <a href="#comment29124185_11030607" target="_blank">Oct 27 '13 at 14:14</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-29770257">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
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
                "found a citation" - where?
                    – <a href="/users/611007/n611x007" title="3,940 reputation" target="_blank">n611x007</a>
                <a href="#comment29770257_11030607" target="_blank">Nov 15 '13 at 7:09</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-29781804">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                7
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
            
        </td>
    </tr>
    <tr id="comment-72585214">
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
                Why not <b>reconfiguration</b>? Which would be very accurate, as for customization of the default configuration.
                    – <a href="/users/4104817/chinggis6" title="356 reputation" target="_blank">Chinggis6</a>
                <a href="#comment72585214_11030607" target="_blank">Mar 11 '17 at 9:10</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-11030607">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-41756433">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>To understand rc files, it helps to know that Ubuntu boots into several different <em>runlevels.</em> They are 0-6, 0 being "halt", 1 being "single-user", 2 being "multi-user"(the default runlevel), etc. This system has now been outdated by the <em>Upstart</em> and <em>initd</em> programs in most Linux Distros. It is still maintained for backwards compatibility. </p>

<p>Within the <code>/etc</code> directory are several folders labeled "rc0.d, rc1.d" etc, through rc6.d. These are the directories the kernel refers to to know which <em>init</em> scripts it should run for that runlevel. They are symbolic links to the system service scripts residing in the <code>/etc/init.d</code> directory.</p>

<p>In the context you are using it, it would appear that you are listing any files with rc in the name. The code in these files will set the way the services/tasks startup and run when initialized.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jan 20 '17 at 5:02
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
	    

        <div id="comments-link-41756433">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-11030652">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        20
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Runtime Configuration normally if it's in the config. think of them as resource files. If you see RC in file name this could be version i.e. Release Candidate.</p>

<p>Edit: No I take it back official.... "run commands"</p>

<blockquote>
  <p>[Unix: from runcom files on the CTSS system 1962-63, via the startup
  script /etc/rc] Script file containing startup instructions for an
  application program (or an entire operating system), usually a text
  file containing commands of the sort that might have been invoked
  manually once the system was running but are to be executed
  automatically each time the system starts up.</p>
  
  <p>Thus, it would seem that the "rc" part stands for "runcom", which I
  believe can be expanded to "run commands". In fact, this is exactly
  what the file contains, commands that bash should run.</p>
</blockquote>

<p>Quote: <a href="https://unix.stackexchange.com/questions/3467/what-does-rc-in-bashrc-stand-for" target="_blank">https://unix.stackexchange.com/questions/3467/what-does-rc-in-bashrc-stand-for</a></p>

<p>I learn something new. :)</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-11030652">
		        <table>
                    <tbody>



    <tr id="comment-29783128">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
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
                +1 for <code>Release Candidate</code>, even if its not the 'rc in bashrc'
                    – <a href="/users/611007/n611x007" title="3,940 reputation" target="_blank">n611x007</a>
                <a href="#comment29783128_11030652" target="_blank">Nov 15 '13 at 14:27</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-11030652">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/linux" title="show questions tagged 'linux'" target="_blank">linux</a> <a href="/questions/tagged/rc" title="show questions tagged 'rc'" target="_blank">rc</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
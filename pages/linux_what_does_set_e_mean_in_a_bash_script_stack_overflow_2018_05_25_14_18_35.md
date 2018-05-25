<a href="https://stackoverflow.com/questions/19622198/what-does-set-e-mean-in-a-bash-script">https://stackoverflow.com/questions/19622198/what-does-set-e-mean-in-a-bash-script</a><div id="articleHeader"><h1>What does set -e mean in a bash script?</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        379
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>87</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I'm studying the content of this <strong>preinst</strong> file that the script executes before that package is unpacked from its Debian archive (.deb) file.</p>

<p>The script has the following code:</p>

<pre><code>#!/bin/bash
set -e
# Automatically added by dh_installinit
if [ "$1" = install ]; then
   if [ -d /usr/share/MyApplicationName ]; then
     echo "MyApplicationName is just installed"
     return 1
   fi
   rm -Rf $HOME/.config/nautilus-actions/nautilus-actions.conf
   rm -Rf $HOME/.local/share/file-manager/actions/*
fi
# End automatically added section</code></pre>

<p>My first query is about the line:</p>

<pre><code>set -e</code></pre>

<p>I think that the rest of the script is pretty simple: It checks whether the Debian/Ubuntu package manager is executing an install operation. If it is, it checks whether my application has just been installed on the system. If it has, the script prints the message <strong>"MyApplicationName is just installed"</strong> and ends (<code>return 1</code> mean that ends with an “error”, doesn’t it?).</p>

<p>If the user is asking the Debian/Ubuntu package system to install my package, the script also deletes two directories.</p>

<p>Is this right or am I missing something?</p>
    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-19622569">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        431
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>From <code>help set</code> :</p>

<pre><code>  -e  Exit immediately if a command exits with a non-zero status.</code></pre>

<p>But it's not very reliable and considered as a bad practice, better use :</p>

<pre><code>trap 'do_something' ERR</code></pre>

<p>to run <code>do_something</code> function when errors will occurs.</p>

<p>See <a href="http://mywiki.wooledge.org/BashFAQ/105" target="_blank">http://mywiki.wooledge.org/BashFAQ/105</a></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-19622300">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        56
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><code>set -e</code> stops the execution of a script if a command or pipeline has an error - which is the opposite of the default shell behaviour, which is to ignore errors in scripts. Type <code>help set</code> in a terminal to see the documentation for this built-in command.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 27 '13 at 19:14
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-34381499">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        31
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>As per <a href="https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin.html" target="_blank">bash - The Set Builtin</a> manual, if <code>-e</code>/<code>errexit</code> is set, shell exits immediately if a <a href="https://www.gnu.org/software/bash/manual/html_node/Pipelines.html#Pipelines" target="_blank">pipeline</a> consist of a single <a href="https://www.gnu.org/software/bash/manual/html_node/Simple-Commands.html#Simple-Commands" target="_blank">simple command</a>, <a href="https://www.gnu.org/software/bash/manual/html_node/Lists.html#Lists" target="_blank">a list</a> or <a href="https://www.gnu.org/software/bash/manual/html_node/Compound-Commands.html#Compound-Commands" target="_blank">a compound command</a> returns a non-zero status.</p>

<p>By default, the exit status of a pipeline is the exit status of the last command in the pipeline, unless the <code>pipefail</code> option is enabled (it's disabled by default).</p>

<p>If so, the pipeline’s return status of the last (rightmost) command to exit with a non-zero status, or zero if all commands exit successfully.</p>

<p>If you'd like to execute something on exit, try defining <code>trap</code>, for example:</p>

<pre><code>trap onexit EXIT</code></pre>

<p>where <code>onexit</code> is your function to do something on exit, like below which is printing the simple <a href="https://unix.stackexchange.com/q/19323/21471" target="_blank">stack trace</a>:</p>

<pre><code>onexit(){ while caller $((n++)); do :; done; }</code></pre>

<p>There is similar option <a href="https://stackoverflow.com/q/25378845/55075" target="_blank"><code>-E</code>/<code>errtrace</code></a> which would trap on ERR instead, e.g.:</p>

<pre><code>trap onerr ERR</code></pre>

<h3>Examples</h3>

<p>Zero status example:</p>

<pre><code>$ true; echo $?
0</code></pre>

<p>Non-zero status example:</p>

<pre><code>$ false; echo $?
1</code></pre>

<p>Negating status examples:</p>

<pre><code>$ ! false; echo $?
0
$ false || true; echo $?
0</code></pre>

<p>Test with <code>pipefail</code> being disabled:</p>

<pre><code>$ bash -c 'set +o pipefail -e; true | true | true; echo success'; echo $?
success
0
$ bash -c 'set +o pipefail -e; false | false | true; echo success'; echo $?
success
0
$ bash -c 'set +o pipefail -e; true | true | false; echo success'; echo $?
1</code></pre>

<p>Test with <code>pipefail</code> being enabled:</p>

<pre><code>$ bash -c 'set -o pipefail -e; true | false | true; echo success'; echo $?
1</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-38798777">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        19
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I found this question while Googling, trying to figure out what the exit status was for a script that was aborted due to a <code>set -e</code>. The answer didn't appear obvious to me; hence this answer. Basically, <em><code>set -e</code> aborts the execution of a command (e.g. a shell script) and returns the exit status code of the command that failed (i.e. the inner script, not the outer script)</em>.</p>

<p>For example, suppose I have the a shell script <code>outer-test.sh</code>:</p>

<pre><code>#!/bin/sh
set -e
./inner-test.sh
exit 62;</code></pre>

<p>The code for <code>inner-test.sh</code> is:</p>

<pre><code>#!/bin/sh
exit 26;</code></pre>

<p>When I run <code>outer-script.sh</code> from the command line my outer script terminates with the exit code of the inner script:</p>

<pre><code>$ ./outer-test.sh
$ echo $?
26</code></pre>
    </div>
    
</div>
    
        </div>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/linux" title="show questions tagged 'linux'" target="_blank">linux</a> <a href="/questions/tagged/bash" title="show questions tagged 'bash'" target="_blank">bash</a> <a href="/questions/tagged/shell" title="show questions tagged 'shell'" target="_blank">shell</a> <a href="/questions/tagged/sh" title="show questions tagged 'sh'" target="_blank">sh</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
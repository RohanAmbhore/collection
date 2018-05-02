<a href="https://stackoverflow.com/questions/4157189/git-pull-while-ignoring-local-changes/29206075#29206075">https://stackoverflow.com/questions/4157189/git-pull-while-ignoring-local-changes/29206075#29206075</a><div id="articleHeader"><h1>Git Pull While Ignoring Local Changes?</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        295
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>101</b></div>


</div>

            </div>

            
<div>
    <div>

<p>Is there a way to do a <code>git pull</code> that ignores any local file changes without blowing the directory away and having to perform a <code>git clone</code>?</p>
    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-4157261">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        524
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>If you mean you want the pull to overwrite local changes, doing the merge as if the working tree were clean, well, clean the working tree:</p>

<pre><code>git reset --hard
git pull
</code></pre>

<p>If there are untracked local files you could use <code>git clean</code> to remove them. Use <code>git clean -f</code> to remove untracked files, <code>-df</code> to remove untracked files and directories, and <code>-xdf</code> to remove untracked or ignored files or directories.</p>

<p>If on the other hand you want to keep the local modifications somehow, you'd use stash to hide them away before pulling, then reapply them afterwards:</p>

<pre><code>git stash
git pull
git stash pop
</code></pre>

<p>I don't think it makes any sense to literally <em>ignore</em> the changes, though - half of pull is merge, and it needs to merge the committed versions of content with the versions it fetched.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Nov 11 '10 at 17:25
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-4157233">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Look at <a href="http://git-scm.com/docs/git-stash" target="_blank">git stash</a> to put all of your local changes into a "stash file" and revert to the last commit. At that point, you can apply your stashed changes, or discard them.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Nov 11 '10 at 17:23
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-13242209">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>If you are on Linux:</p>

<pre><code>git fetch
for file in `git diff origin/master..HEAD --name-only`; do rm -f "$file"; done
git pull
</code></pre>

<p>The for loop will delete all tracked files which are changed in the local repo, so <code>git pull</code> will work without any problems.<br />
The nicest thing about this is that only the tracked files will be overwritten by the files in the repo, all other files will be left untouched.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-27096046">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        15
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>The command bellow <strong>wont work always</strong>. If you do just:</p>

<pre><code>$ git checkout thebranch
Already on 'thebranch'
Your branch and 'origin/thebranch' have diverged,
and have 23 and 7 different commits each, respectively.

$ git reset --hard
HEAD is now at b05f611 Here the commit message bla, bla

$ git pull
Auto-merging thefile1.c
CONFLICT (content): Merge conflict in thefile1.c
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
</code></pre>

<p>and so on...</p>

<p>To <strong>really</strong> start over, downloading thebranch and overwriting all your local changes, just do:</p>

<hr />

<pre><code>$ git checkout thebranch
$ git reset --hard origin/thebranch
</code></pre>

<hr />

<p>This will work just fine.</p>

<pre><code>$ git checkout thebranch
Already on 'thebranch'
Your branch and 'origin/thebranch' have diverged,
and have 23 and 7 different commits each, respectively.

$ git reset --hard origin/thebranch
HEAD is now at 7639058 Here commit message again...

$ git status
# On branch thebranch
nothing to commit (working directory clean)

$ git checkout thebranch
Already on 'thebranch'
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Nov 24 '14 at 0:10
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-29206075">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        134
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>For me the following worked:</p>

<p>(1) First fetch all changes:</p>

<pre><code>$ git fetch --all
</code></pre>

<p>(2) Then reset the master:</p>

<pre><code>$ git reset --hard origin/master
</code></pre>

<p>(3) Pull/update:</p>

<pre><code>$ git pull
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 23 '15 at 8:42
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-37060240">
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
<p>This will fetch the current branch and attempt to do a fast forward to master:</p>

<pre><code>git fetch && git merge --ff-only origin/master
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 5 '16 at 21:04
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-46180281">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        4
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<pre><code>git fetch --all && git reset --hard origin/master
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Sep 12 '17 at 15:26
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-49230768">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>You just want a command which gives exactly the same result as <code>rm -rf local_repo && git clone remote_url</code>, right? I also want this function. I wonder why git does not provide such a command (such as <code>git reclone</code> or <code>git sync</code>), neither does svn provide such a command (such as <code>svn recheckout</code> or <code>svn sync</code>).</p>

<p>Try the following command:</p>

<pre><code>git reset --hard origin/master
git clean -fxd
git pull
</code></pre>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/git" title="show questions tagged 'git'" target="_blank">git</a> <a href="/questions/tagged/git-pull" title="show questions tagged 'git-pull'" target="_blank">git-pull</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
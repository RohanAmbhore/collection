<a href="https://stackoverflow.com/questions/9069061/what-is-the-difference-between-git-merge-and-git-merge-no-ff">https://stackoverflow.com/questions/9069061/what-is-the-difference-between-git-merge-and-git-merge-no-ff</a><div id="articleHeader"><h1>What is the difference between `git merge` and `git merge --no-ff`?</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        584
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>225</b></div>


</div>

            </div>

            
<div>
    <div>

<p>Using <code>gitk log</code>, I could not spot a difference between the two. How can I observe the difference (with a git command or some tool)?</p>
    </div>
    
    
</div>

                        <div>
                <div>
        <h2>                    <b>protected</b> by <a href="/users/584192/samuel-liew" target="_blank">Samuel Liew</a>♦ Mar 10 '17 at 3:40
</h2>
        <p>
This question is protected to prevent "thanks!", "me too!", or spam answers by new users. 
To answer it, you must have earned at least 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).</p>
    </div>
            </div>
    
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-9069127">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        679
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>The <code>--no-ff</code> flag prevents <code>git merge</code> from executing a "fast-forward" if it detects that your current <code>HEAD</code> is an ancestor of the commit you're trying to merge. A fast-forward is when, instead of constructing a merge commit, git just moves your branch pointer to point at the incoming commit. This commonly occurs when doing a <code>git pull</code> without any local changes.</p>

<p>However, occasionally you want to prevent this behavior from happening, typically because you want to maintain a specific branch topology (e.g. you're merging in a topic branch and you want to ensure it looks that way when reading history). In order to do that, you can pass the <code>--no-ff</code> flag and <code>git merge</code> will <em>always</em> construct a merge instead of fast-forwarding.</p>

<p>Similarly, if you want to execute a <code>git pull</code> or use <code>git merge</code> in order to explicitly fast-forward, and you want to bail out if it can't fast-forward, then you can use the <code>--ff-only</code> flag. This way you can regularly do something like <code>git pull --ff-only</code> without thinking, and then if it errors out you can go back and decide if you want to merge or rebase.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 30 '12 at 18:51
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-14865661">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        687
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<h2>Graphic answer to this question</h2>

<p><a href="http://nvie.com/posts/a-successful-git-branching-model/" target="_blank">Here is a site</a> with a clear explanation and graphical illustration of using <kbd>git merge --no-ff</kbd>:</p>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/GGkZc.png" alt="difference between git merge --no-ff and git merge" /></div></p>

<p>Until I saw this, I was completely lost with git. Using <kbd>--no-ff</kbd> allows someone reviewing history to clearly <a href="https://github.com/blog/39-say-hello-to-the-network-graph-visualizer" target="_blank">see the branch you checked out</a> to work on. (that link points to github's "network" visualization tool) And here is <a href="http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging" target="_blank">another great reference</a> with illustrations. This reference complements the first one nicely with more of a focus on those less acquainted with git. </p>

<hr />

<h2>Basic info for newbs like me</h2>

<p>If you are like me, and not a Git-guru, <a href="https://stackoverflow.com/questions/2047465/how-can-i-delete-a-file-from-git-repo/16753592#16753592" target="_blank">my answer here</a> describes handling the deletion of files from git's tracking without deleting them from the local filesystem, which seems poorly documented but often occurrence. Another newb situation is <a href="https://stackoverflow.com/questions/292357" target="_blank">getting current code</a>, which still manages to elude me.</p>

<hr />

<h2>Example Workflow</h2>

<p>I updated a package to my website and had to go back to my notes to see my workflow; I thought it useful to add an example to this answer. </p>

<p>My workflow of git commands:</p>

<pre><code>git checkout -b contact-form
(do your work on "contact-form")
git status
git commit -am  "updated form in contact module"
git checkout master
git merge --no-ff contact-form
git branch -d contact-form
git push origin master
</code></pre>

<p><strong>Below:</strong> actual usage, including explanations.<br />
<em>Note: the output below is snipped; git is quite verbose.</em></p>

<pre><code>$ git status
# On branch master
# Changed but not updated:
#   (use "git add/rm &lt;file&gt;..." to update what will be committed)
#   (use "git checkout -- &lt;file&gt;..." to discard changes in working directory)
#
#       modified:   ecc/Desktop.php
#       modified:   ecc/Mobile.php
#       deleted:    ecc/ecc-config.php
#       modified:   ecc/readme.txt
#       modified:   ecc/test.php
#       deleted:    passthru-adapter.igs
#       deleted:    shop/mickey/index.php
#
# Untracked files:
#   (use "git add &lt;file&gt;..." to include in what will be committed)
#
#       ecc/upgrade.php
#       ecc/webgility-config.php
#       ecc/webgility-config.php.bak
#       ecc/webgility-magento.php
</code></pre>

<p>Notice 3 things from above:<br />
1) In the output you can see the changes from the ECC package's upgrade, including the addition of new files.<br />
2) Also notice there are two files (not in the <code>/ecc</code> folder) I deleted independent of this change. Instead of confusing those file deletions with <code>ecc</code>, I'll make a different <code>cleanup</code> branch later to reflect those files' deletion.<br />
3) I didn't follow my workflow! I forgot about git while I was trying to get ecc working again. </p>

<p>Below: rather than do the all-inclusive <code>git commit -am "updated ecc package"</code> I normally would, I only wanted to add the files in the <code>/ecc</code> folder. Those deleted files weren't specifically part of my <code>git add</code>, but because they already were tracked in git, I need to remove them from this branch's commit:</p>

<pre><code>$ git checkout -b ecc
$ git add ecc/*
$ git reset HEAD passthru-adapter.igs
$ git reset HEAD shop/mickey/index.php
Unstaged changes after reset:
M       passthru-adapter.igs
M       shop/mickey/index.php

$ git commit -m "Webgility ecc desktop connector files; integrates with Quickbooks"

$ git checkout master
D       passthru-adapter.igs
D       shop/mickey/index.php
Switched to branch 'master'
$ git merge --no-ff ecc
$ git branch -d ecc
Deleted branch ecc (was 98269a2).
$ git push origin master
Counting objects: 22, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (14/14), done.
Writing objects: 100% (14/14), 59.00 KiB, done.
Total 14 (delta 10), reused 0 (delta 0)
To git@github.com:me/mywebsite.git
   8a0d9ec..333eff5  master -&gt; master
</code></pre>

<br /><br /><hr /><h2>Script for automating the above</h2>

<p>Having used this process 10+ times in a day, I have taken to writing batch scripts to execute the commands, so I made an almost-proper <code>git_update.sh &lt;branch&gt; &lt;"commit message"&gt;</code> script for doing the above steps. <a href="https://gist.github.com/cacycleworks/776b39d00c525a090ab2" target="_blank">Here is the Gist source</a> for that script. </p>

<p>Instead of <code>git commit -am</code> I am selecting files from the "modified" list produced via <code>git status</code> and then pasting those in this script. This came about because I made dozens of edits but wanted varied branch names to help group the changes.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-21717431">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        140
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>The <code>--no-ff</code> option ensures that a fast forward merge will not happen, and that <strong>a new commit object will always be created</strong>. This can be desirable if you want git to maintain a history of feature branches. 
            <div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/FMD5h.png" alt="git merge --no-ff vs git merge" /></div>
In the above image, the left side is an example of the git history after using <code>git merge --no-ff</code> and the right side is an example of using <code>git merge</code> where an ff merge was possible.</p>

<p><strong>EDIT</strong>: A previous version of this image indicated only a single parent for the merge commit. <strong>Merge commits have multiple parent commits</strong> which git uses to maintain a history of the "feature branch" and of the original branch. The multiple parent links are highlighted in green.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-22821691">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        29
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>This is an old question, and this is somewhat subtly mentioned in the other posts, but the explanation that made this click for me is that <strong>non fast forward merges will require a separate commit</strong>.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Apr 2 '14 at 19:56
    </div>
    
    
</div>
    </div>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/git" title="show questions tagged 'git'" target="_blank">git</a> <a href="/questions/tagged/merge" title="show questions tagged 'merge'" target="_blank">merge</a> <a href="/questions/tagged/fast-forward" title="show questions tagged 'fast-forward'" target="_blank">fast-forward</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
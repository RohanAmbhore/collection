<a href="https://stackoverflow.com/questions/6934752/combining-multiple-commits-before-pushing-in-git">https://stackoverflow.com/questions/6934752/combining-multiple-commits-before-pushing-in-git</a><div id="articleHeader"><h1>Combining multiple commits before pushing in Git</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        296
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>131</b></div>


</div>

            </div>

            
<div>
    <div>

<div>
    <p>This question already has an answer here:</p>
    <ul>
        <li>
            <a href="/questions/5189560/squash-my-last-x-commits-together-using-git" target="_blank">Squash my last X commits together using Git</a>
                
                    23 answers
                
        </li>
    </ul>
    </div>
<p>I have a bunch of commits on my local repository which are thematically similar. I'd like to combine them into a single commit before pushing up to a remote. How do I do it? I think <code>rebase</code> does this, but I can't make sense of the docs.</p>
    </div>
    
    
</div>

                        <div>
                <div>
        <h2>                    <b>marked</b> as duplicate by <a href="/users/216074/poke" target="_blank">poke</a><a href="/badges/tag-badges/git?badgeClass=Gold" target="_blank"> git</a>

 Dec 9 '17 at 1:36
</h2>
        <p>This question has been asked before and already has an answer. If those answers do not fully address your question, please <a href="/questions/ask" target="_blank">ask a new question</a>.</p>
    </div>
            </div>
    
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-6934882">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        461
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>What you want to do is referred to as "squashing" in git.  There are lots of options when you're doing this (too many?) but if you just want to merge all of your unpushed commits into a single commit, do this:</p>

<pre><code>git rebase -i origin/master
</code></pre>

<p>This will bring up your text editor (<code>-i</code> is for "interactive") with a file that looks like this:</p>

<pre><code>pick 16b5fcc Code in, tests not passing
pick c964dea Getting closer
pick 06cf8ee Something changed
pick 396b4a3 Tests pass
pick 9be7fdb Better comments
pick 7dba9cb All done
</code></pre>

<p>Change all the <code>pick</code> to <code>squash</code> (or <code>s</code>) except the first one:</p>

<pre><code>pick 16b5fcc Code in, tests not passing
squash c964dea Getting closer
squash 06cf8ee Something changed
squash 396b4a3 Tests pass
squash 9be7fdb Better comments
squash 7dba9cb All done
</code></pre>

<p>Save your file and exit your editor.  Then another text editor will open to let you combine the commit messages from all of the commits into one big commit message.</p>

<p>Voila! Googling "git squashing" will give you explanations of all the other options available.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-6934765">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>You probably want to use <a href="http://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#Changing-Multiple-Commit-Messages" target="_blank">Interactive Rebasing</a>, which is described in detail in that link.</p>

<p>You can find other good resources if you search for "git rebase interactive".</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-6934774">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        24
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>You can do this with <code>git rebase -i</code>, passing in the revision that you want to use as the 'root':</p>

<pre><code>git rebase -i origin/master
</code></pre>

<p>will open an editor window showing all of the commits you have made after the last commit in <code>origin/master</code>. You can reject commits, squash commits into a single commit, or edit previous commits.</p>

<p>There are a few resources that can probably explain this in a better way, and show some other examples:</p>

<p><a href="http://book.git-scm.com/4_interactive_rebasing.html" target="_blank">http://book.git-scm.com/4_interactive_rebasing.html</a></p>



<p><a href="http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html" target="_blank">http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html</a></p>

<p>are the first two good pages I could find.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 4 '11 at 0:08
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-21278908">
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
<p>If you have <strong>lots</strong> of commits and you only want to squash the last X commits, find the commit ID of the commit from which you want to start squashing and do</p>

<pre><code>git rebase -i &lt;that_commit_id&gt;
</code></pre>

<p>Then proceed as described in leopd's answer, changing all the <code>pick</code>s to <code>squash</code>es except the first one.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 22 '14 at 9:28
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-29310055">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        10
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I came up with</p>

<pre><code>#!/bin/sh

message=`git log --format=%B origin..HEAD | sort | uniq | grep -v '^$'`
git reset --soft origin
git commit -m "$message"
</code></pre>

<p>Combines, sorts, unifies and remove empty lines from the commit message. I use this for local changes to a github wiki (using gollum)</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 27 '15 at 20:55
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-33635467">
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
<p>You can squash (join) commits with an <strong>Interactive Rebase</strong>. There is a pretty nice YouTube video which shows how to do this on the command line or with <a href="http://www.syntevo.com/smartgit/" target="_blank">SmartGit</a>:</p>

<ul>
<li><a href="https://www.youtube.com/watch?v=qi_QAFrmHJM" target="_blank">https://www.youtube.com/watch?v=qi_QAFrmHJM</a></li>
</ul>

<p>If you are already a SmartGit user then you can select all your outgoing commits (by holding down the Ctrl key) and open the context menu (right click) to squash your commits. </p>

<p>It's very comfortable:</p>

<p><a href="https://i.stack.imgur.com/2Q5rl.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/2Q5rl.png" alt="enter image description here" /></div></a></p>

<p>There is also a very nice tutorial from <a href="https://www.atlassian.com/" target="_blank">Atlassian</a> which shows how it works:</p>

<ul>
<li><a href="https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase-i" target="_blank">https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase-i</a></li>
</ul>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Nov 10 '15 at 17:01
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-33719090">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>And my way of <code>squashing</code> multiple <code>push</code> is (perhaps you pushed to your own branch many commits and now you wish to do a pull request and you don't want to clutter them with many commits which you have already pushed).  The way I do that (no other simpler option as far as I can tell is).</p>

<ol>
<li>Create new branch for the sake of <code>squash</code> (branch from the original branch you wish to pull request to).</li>
<li>Push the newly created branch.</li>
<li>Merge branch with commits (already pushed) to new branch.</li>
<li>Rebase new branch and squash.</li>
<li>Push new branch.</li>
<li>Create new pull request for new branch which now has single commit.</li>
</ol>

<p>Example:</p>

<pre><code>git checkout from_branch_you_wish_to_pull_request_to
git checkout -b new_branch_will_have_single_squashed_commit
git push -u new_branch_will_have_single_squashed_commit
git merge older_branch_with_all_those_multiple_commits
git rebase -i (here you squash)
git push origin new_branch_will_have_single_squashed_commit
</code></pre>

<p>You can now pull request into <code>from_branch_you_wish_to_pull_request_to</code></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-39885116">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        22
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>There are quite a few working answers here, but I found this the easiest. This command will open up an editor, where you can just replace <code>pick</code> with <code>squash</code> in order to remove/merge them into one</p>

<pre><code>git rebase -i HEAD~4
</code></pre>

<p>where, <code>4</code> is the number of commits you want to squash into one. This is explained <a href="http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html" target="_blank">here</a> as well.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 5 '16 at 23:16
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>
                


                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/git" title="show questions tagged 'git'" target="_blank">git</a> <a href="/questions/tagged/git-squash" title="show questions tagged 'git-squash'" target="_blank">git-squash</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
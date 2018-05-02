<a href="https://stackoverflow.com/questions/6839398/find-when-a-file-was-deleted-in-git">https://stackoverflow.com/questions/6839398/find-when-a-file-was-deleted-in-git</a><div id="articleHeader"><h1>Find when a file was deleted in Git</h1></div>
<h3>Short answer:</h3>

<pre><code>git log --full-history -- your_file
</code></pre>

<p>will show you <em>all</em> commits in your repo's history, including merge commits, that touched <code>your_file</code>. The last (top) one is the one that deleted the file.</p>

<h3>Some explanation:</h3>

<p>The <code>--full-history</code> flag here is important. Without it, Git performs "history simplification" when you ask it for the log of a file. The docs are light on details about exactly how this works and I lack the grit and courage required to try and figure it out from the source code, but <a href="https://git-scm.com/docs/git-log" target="_blank">the git-log docs</a> have this much to say:</p>

<blockquote>
  <h3>Default mode</h3>
  
  <p>Simplifies the history to the simplest history explaining the final state of the tree. Simplest because it prunes some side branches if the end result is the same (i.e. merging branches with the same content)</p>
</blockquote>

<p>This is obviously concerning when the file whose history we want is <em>deleted</em>, since the simplest history explaining the final state of a deleted file is <em>no history</em>. Is there a risk that <code>git log</code> without <code>--full-history</code> will simply claim that the file was never created? Unfortunately, yes. Here's a demonstration:</p>

<pre><code>mark@lunchbox:~/example$ <b><i>git init</i></b>
Initialised empty Git repository in /home/mark/example/.git/
mark@lunchbox:~/example$ <b><i>touch foo && git add foo && git commit -m "Added foo"</i></b>
[master (root-commit) ddff7a7] Added foo
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 foo
mark@lunchbox:~/example$ <b><i>git checkout -b newbranch</i></b>
Switched to a new branch 'newbranch'
mark@lunchbox:~/example$ <b><i>touch bar && git add bar && git commit -m "Added bar"</i></b>
[newbranch 7f9299a] Added bar
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 bar
mark@lunchbox:~/example$ <b><i>git checkout master</i></b>
Switched to branch 'master'
mark@lunchbox:~/example$ <b><i>git rm foo && git commit -m "Deleted foo"</i></b>
rm 'foo'
[master 7740344] Deleted foo
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 foo
mark@lunchbox:~/example$ <b><i>git checkout newbranch</i></b>
Switched to branch 'newbranch'
mark@lunchbox:~/example$ <b><i>git rm bar && git commit -m "Deleted bar"</i></b>
rm 'bar'
[newbranch 873ed35] Deleted bar
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 bar
mark@lunchbox:~/example$ <b><i>git checkout master</i></b>
Switched to branch 'master'
mark@lunchbox:~/example$ <b><i>git merge newbranch</i></b>
Already up-to-date!
Merge made by the 'recursive' strategy.
mark@lunchbox:~/example$ <b><i>git log -- foo</i></b>
commit 77403443a13a93073289f95a782307b1ebc21162
Author: Mark Amery 
Date:   Tue Jan 12 22:50:50 2016 +0000

    Deleted foo

commit ddff7a78068aefb7a4d19c82e718099cf57be694
Author: Mark Amery 
Date:   Tue Jan 12 22:50:19 2016 +0000

    Added foo
mark@lunchbox:~/example$ <b><i>git log -- bar</i></b>
mark@lunchbox:~/example$ <b><i>git log --full-history -- foo</i></b>
commit 2463e56a21e8ee529a59b63f2c6fcc9914a2b37c
Merge: 7740344 873ed35
Author: Mark Amery 
Date:   Tue Jan 12 22:51:36 2016 +0000

    Merge branch 'newbranch'

commit 77403443a13a93073289f95a782307b1ebc21162
Author: Mark Amery 
Date:   Tue Jan 12 22:50:50 2016 +0000

    Deleted foo

commit ddff7a78068aefb7a4d19c82e718099cf57be694
Author: Mark Amery 
Date:   Tue Jan 12 22:50:19 2016 +0000

    Added foo
mark@lunchbox:~/example$ <b><i>git log --full-history -- bar</i></b>
commit 873ed352c5e0f296b26d1582b3b0b2d99e40d37c
Author: Mark Amery 
Date:   Tue Jan 12 22:51:29 2016 +0000

    Deleted bar

commit 7f9299a80cc9114bf9f415e1e9a849f5d02f94ec
Author: Mark Amery 
Date:   Tue Jan 12 22:50:38 2016 +0000

    Added bar
</code></pre>

<p>Notice how <code>git log -- bar</code> in the terminal dump above resulted in literally no output; Git is "simplifying" history down into a fiction where <code>bar</code> never existed. <code>git log --full-history -- bar</code>, on the other hand, gives us the commit that created <code>bar</code> and the commit that deleted it.</p>

<p>To be clear: this issue isn't merely theoretical. I only looked into the docs and discovered the <code>--full-history</code> flag because <code>git log -- some_file</code> was failing for me in a real repository where I was trying to track a deleted file down. History simplification might sometimes be helpful when you're trying to understand how a <em>currently-existing</em> file came to be in its current state, but when trying to track down a file <em>deletion</em> it's more likely to screw you over by hiding the commit you care about. Always use the <code>--full-history</code> flag for this use case.</p>
    
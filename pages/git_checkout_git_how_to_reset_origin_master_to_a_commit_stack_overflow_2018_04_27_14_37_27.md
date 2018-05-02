<a href="https://stackoverflow.com/questions/17667023/git-how-to-reset-origin-master-to-a-commit/17667057">https://stackoverflow.com/questions/17667023/git-how-to-reset-origin-master-to-a-commit/17667057</a><div id="articleHeader"><h1>Git, How to reset origin/master to a commit?</h1></div>

<p>I reset my local master to a commit by this command:</p>

<pre><code>git reset --hard e3f1e37
</code></pre>

<p>when I enter <code>$ git status</code> command, terminal says:</p>

<pre><code># On branch master
# Your branch is behind 'origin/master' by 7 commits, and can be fast-forwarded.

#   (use "git pull" to update your local branch)
#
nothing to commit, working directory clean
</code></pre>

<p>Since I want to reset origin/header as well, I checkout to origin/master:</p>

<pre><code>$ git checkout origin/master
Note: checking out 'origin/master'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b new_branch_name

HEAD is now at 2aef1de... master problem fixed for master. its okay now.
</code></pre>

<p>and reset the header by this command:</p>

<pre><code>$ git reset --hard e3f1e37
HEAD is now at e3f1e37 development version code incremented for new build.
</code></pre>

<p>Then I tried to add commit to origin/header that I was not successful.</p>

<pre><code>$ git commit -m "Reverting to the state of the project at e3f1e37"
# HEAD detached from origin/master
nothing to commit, working directory clean
</code></pre>

<p>Finally, I checkout to my local master.</p>

<pre><code>$ git checkout master
Switched to branch 'master'
Your branch is behind 'origin/master' by 7 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
</code></pre>

<p>Since, I reset the head of origin/master I expect local and origin should be in same direction but as you see, git is saying that my local/master is behind origin/master by 7 commits.</p>

<p>How can I fix this issue? The things that I'm looking for is Head of local/master and origin/master point to same commit. Following image shows what I did. Thanks.</p>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/fuQB3.png" alt="enter image description here" /></div></p>
    
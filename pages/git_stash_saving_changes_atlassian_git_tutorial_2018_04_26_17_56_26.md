<a href="https://www.atlassian.com/git/tutorials/saving-changes/git-stash">https://www.atlassian.com/git/tutorials/saving-changes/git-stash</a><div id="articleHeader"><h1>Git stash</h1></div>


<p><code>git stash</code> temporarily shelves (or <em>stashes</em>) changes you've made to your working copy so you can work on something else, and then come back and re-apply them later on. Stashing is handy if you need to quickly switch context and work on something else, but you're mid-way through a code change and aren't quite ready to commit.</p>

<h2 id="stashing-your-work">Stashing your work</h2>
<p>The <code>git stash</code> command takes your uncommitted changes (both staged and unstaged), saves them away for later use, and then reverts them from your working copy. For example:</p>
<pre><code>$ git status
On branch master
Changes to be committed:
new file: style.css
Changes not staged for commit:
modified: index.html
$ git stash
Saved working directory and index state WIP on master: 5002d47 our new homepage
HEAD is now at 5002d47 our new homepage
$ git status
On branch master
nothing to commit, working tree clean</code></pre>
<p>At this point you're free to make changes, create new commits, switch branches, and perform any other Git operations; then come back and re-apply your stash when you're ready.</p>
<p>Note that the stash is local to your Git repository; stashes are not transferred to the server when you push.</p>
<h2 id="re-applying-your-stashed-changes">Re-applying your stashed changes</h2>
<p>You can reapply previously stashed changes with <code>git stash pop</code>:</p>
<pre><code>$ git status
On branch master
nothing to commit, working tree clean
$ git stash pop
On branch master
Changes to be committed:
new file: style.css
Changes not staged for commit:
modified: index.html
Dropped refs/stash@{0} (32b3aa1d185dfe6d57b3c3cc3b32cbf3e380cc6a)</code></pre>
<p><em>Popping</em> your stash removes the changes from your stash and reapplies them to your working copy.</p>
<p>Alternatively, you can reapply the changes to your working copy <em>and</em> keep them in your stash with <code>git stash apply</code>:</p>
<pre><code>$ git stash apply
On branch master
Changes to be committed:
new file: style.css
Changes not staged for commit:
modified: index.html</code></pre>
<p>This is useful if you want to apply the same stashed changes to multiple branches. </p>
<p>Now that you know the basics of stashing, there is one caveat with <code>git stash</code> you need to be aware of: by default Git <em>won't</em> stash changes made to untracked or ignored files.</p>
<h2 id="stashing-untracked-or-ignored">Stashing untracked or ignored files</h2>
<p>By default, running <code>git stash</code> will stash:</p>
<ul>
<li>changes that have been added to your index (staged changes)</li>
<li>changes made to files that are currently tracked by Git (unstaged changes)</li>
</ul>
<p>But it will <strong>not</strong> stash:</p>
<ul>
<li>new files in your working copy that have not yet been staged</li>
<li>files that have been <a href="https://www.atlassian.com/git/tutorials/gitignore" target="_blank">ignored</a></li>
</ul>
<p>So if we add a third file to our example above, but don't stage it (i.e. we don't run <code>git add</code>), <code>git stash</code> won't stash it.</p>
<pre><code>$ script.js
$ git status
On branch master
Changes to be committed:
new file: style.css
Changes not staged for commit:
modified: index.html
Untracked files:
script.js
$ git stash
Saved working directory and index state WIP on master: 5002d47 our new homepage
HEAD is now at 5002d47 our new homepage
$ git status
On branch master
Untracked files:
script.js</code></pre>
<p>Adding the <code>-u</code> option (or <code>--include-untracked</code>) tells <code>git stash</code> to also stash your untracked files:</p>
<pre><code>$ git status
On branch master
Changes to be committed:
new file: style.css
Changes not staged for commit:
modified: index.html
Untracked files:
script.js
$ git stash -u
Saved working directory and index state WIP on master: 5002d47 our new homepage
HEAD is now at 5002d47 our new homepage
$ git status
On branch master
nothing to commit, working tree clean</code></pre>
<p>You can include changes to <a href="https://www.atlassian.com/git/tutorials/gitignore" target="_blank">ignored</a> files as well by passing the <code>-a</code> option (or <code>--all</code>) when running <code>git stash</code>.</p>
<div class="readableLargeImageContainer"><img src="https://wac-cdn.atlassian.com/dam/jcr:d6fec41a-dc66-4af6-8b0f-c23d271eaf8e/01.svg?cdnVersion=kv" alt="Git Stash options" /></div>
<h2 id="managing-multiple-stashes">Managing multiple stashes</h2>
<p>You aren't limited to a single stash. You can run <code>git stash</code> several times to create multiple stashes, and then use <code>git stash list</code> to view them. By default, stashes are identified simply as a "WIP" – work in progress – on top of the branch and commit that you created the stash from. After a while it can be difficult to remember what each stash contains:</p>
<pre><code>$ git stash list
stash@{0}: WIP on master: 5002d47 our new homepage
stash@{1}: WIP on master: 5002d47 our new homepage
stash@{2}: WIP on master: 5002d47 our new homepage</code></pre>
<p>To provide a bit more context, it's good practice to annotate your stashes with a description, using <code>git stash save "message"</code>:</p>
<pre><code>$ git stash save "add style to our site"
Saved working directory and index state On master: add style to our site
HEAD is now at 5002d47 our new homepage
$ git stash list
stash@{0}: On master: add style to our site
stash@{1}: WIP on master: 5002d47 our new homepage
stash@{2}: WIP on master: 5002d47 our new homepage</code></pre>
<p>By default, <code>git stash pop</code> will re-apply the most recently created stash: <code>stash@{0}</code></p>
<p>You can choose which stash to re-apply by passing its identifier as the last argument, for example:</p>
<pre><code>$ git stash pop stash@{2}</code></pre>
<h2 id="viewing-stash-diffs">Viewing stash diffs</h2>
<p>You can view a summary of a stash with <code>git stash show</code>:</p>
<pre><code>$ git stash show
index.html | 1 +
style.css | 3 +++
2 files changed, 4 insertions(+)</code></pre>
<p>Or pass the <code>-p</code> option (or <code>--patch</code>) to view the full diff of a stash:</p>
<pre><code>$ git stash show -p
diff --git a/style.css b/style.css
new file mode 100644
index 0000000..d92368b
--- /dev/null
+++ b/style.css
@@ -0,0 +1,3 @@
+* {
+ text-decoration: blink;
+}
diff --git a/index.html b/index.html
index 9daeafb..ebdcbd2 100644
--- a/index.html
+++ b/index.html
@@ -1 +1,2 @@
+&lt;link rel="stylesheet" href="style.css"/&gt;</code></pre>
<h2 id="partial-stashes">Partial stashes</h2>
<p>You can also choose to stash just a single file, a collection of files, or individual changes from within files. If you pass the <code>-p</code> option (or <code>--patch</code>) to <code>git stash</code>, it will iterate through each changed "hunk" in your working copy and ask whether you wish to stash it:</p>
<pre><code>$ git stash -p
diff --git a/style.css b/style.css
new file mode 100644
index 0000000..d92368b
--- /dev/null
+++ b/style.css
@@ -0,0 +1,3 @@
+* {
+ text-decoration: blink;
+}
Stash this hunk [y,n,q,a,d,/,e,?]? y
diff --git a/index.html b/index.html
index 9daeafb..ebdcbd2 100644
--- a/index.html
+++ b/index.html
@@ -1 +1,2 @@
+&lt;link rel="stylesheet" href="style.css"/&gt;
Stash this hunk [y,n,q,a,d,/,e,?]? n</code></pre>
<div class="readableLargeImageContainer"><img src="https://wac-cdn.atlassian.com/dam/jcr:4f32476c-e84f-41b3-a7d9-1b5a70acb22b/02.svg?cdnVersion=kv" alt="Git Stash -p" /></div>
<p>You can hit <strong>?</strong> for a full list of hunk commands. Commonly useful ones are:</p>
<table>
<thead>
<tr>
<th><strong>Command</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<thead>
<tr>
<td><em>/</em></td>
<td>search for a hunk by regex</td>
</tr>
<tr>
<td><em>?</em></td>
<td>help</td>
</tr>
<tr>
<td><em>n</em></td>
<td>don't stash this hunk</td>
</tr>
<tr>
<td><em>q</em></td>
<td>quit (any hunks that have already been selected will be stashed)</td>
</tr>
<tr>
<td><em>s</em></td>
<td>split this hunk into smaller hunks</td>
</tr>
<tr>
<td><em>y</em></td>
<td>stash this hunk</td>
</tr>
</thead>
</table>
<p>There is no explicit "abort" command, but hitting <code>CTRL-C</code>(SIGINT) will abort the stash process.</p>
<h2 id="creating-a-branch-from-your-stash">Creating a branch from your stash</h2>
<p>If the changes on your branch diverge from the changes in your stash, you may run into conflicts when popping or applying your stash. Instead, you can use <code>git stash branch</code> to create a new branch to apply your stashed changes to:</p>
<pre><code>$ git stash branch add-stylesheet stash@{1}
Switched to a new branch 'add-stylesheet'
On branch add-stylesheet
Changes to be committed:
new file: style.css
Changes not staged for commit:
modified: index.html
Dropped refs/stash@{1} (32b3aa1d185dfe6d57b3c3cc3b32cbf3e380cc6a)</code></pre>
<p>This checks out a new branch based on the commit that you created your stash from, and then pops your stashed changes onto it.</p>
<h2 id="cleaning-up-your-stash">Cleaning up your stash</h2>
<p>If you decide you no longer need a particular stash, you can delete it with <code>git stash drop</code>:</p>
<pre><code>$ git stash drop stash@{1}
Dropped stash@{1} (17e2697fd8251df6163117cb3d58c1f62a5e7cdb)</code></pre>
<p>Or you can delete all of your stashes with:</p>
<pre><code>$ git stash clear</code></pre>
<h2 id="how-git-stash-works">How git stash works</h2>
<p>If you just wanted to know how use <code>git stash</code>, you can stop reading here. But if you're curious about how Git (and <code>git stash</code>) works under the hood, read on!</p>
<p>Stashes are actually encoded in your repository as commit objects. The special ref at <code>.git/refs/stash</code> points to your most recently created stash, and previously created stashes are referenced by the <code>stash</code> ref's reflog. This is why you refer to stashes by <code>stash@{n}:</code> you're actually referring to the nth reflog entry for the <code>stash</code> ref. Since a stash is just a commit, you can inspect it with <code>git log</code>:</p>
<pre><code>$ git log --oneline --graph stash@{0}
*-. 953ddde WIP on master: 5002d47 our new homepage
|\ \
| | * 24b35a1 untracked files on master: 5002d47 our new homepage
| * 7023dd4 index on master: 5002d47 our new homepage
|/
* 5002d47 our new homepage</code></pre>
<p>Depending on what you stashed, a single <code>git stash</code> operation creates either two or three new commits. The commits in the diagram above are:</p>
<ul>
<li><code>stash@{0}</code>, a new commit to store the tracked files that were in your working copy when you ran <code>git stash</code></li>
<li><code>stash@{0}</code>'s first parent, the pre-existing commit that was at HEAD when you ran <code>git stash</code></li>
<li><code>stash@{0}</code>'s second parent, a new commit representing the index when you ran <code>git stash</code></li>
<li><code>stash@{0}</code>'s third parent, a new commit representing untracked files that were in your working copy when you ran <code>git stash</code>. This third parent only created if:
<ul>
<li>your working copy actually contained untracked files; and</li>
<li>you specified the <code>--include-untracked</code> or <code>--all</code> option when invoked <code>git stash</code>.</li>
</ul></li>
</ul>
<p>How <code>git stash</code> encodes your worktree and index as commits:</p>
<ul>
<li>
<p>Before stashing, your worktree may contain changes to tracked files, untracked files, and ignored files. Some of these changes may also be staged in the index.</p>
<div><div class="readableLargeImageContainer"><img src="/dam/jcr:3a2ede93-1f2d-45ae-9e0b-167cc0362f37/03.svg" alt="Before stashing" /></div></div>
</li>
<li>
<p>Invoking <code>git stash</code> encodes any changes to tracked files as two new commits in your DAG: one for unstaged changes, and one for changes staged in the index. The special <code>refs/stash</code> ref is updated to point to them.</p>
<div><div class="readableLargeImageContainer"><img src="/dam/jcr:35edaf68-e8b1-484e-b5f0-292c532f048a/04.svg" alt="Git stash" /></div></div>
</li>
<li>
<p>Using the <code>--include-untracked</code> option also encodes any changes to untracked files as an additional commit.</p>
<div><div class="readableLargeImageContainer"><img src="/dam/jcr:f7dd5493-a98d-449e-ae37-146d6270ccf7/05.svg" alt="Git stash --include-untracked" /></div></div>
</li>
<li>
<p>Using the <code>--all</code> option includes changes to any ignored files alongside changes to untracked files in the same commit.</p>
<div><div class="readableLargeImageContainer"><img src="/dam/jcr:446fad60-0ff5-4383-8177-a5fc2813364d/06.svg" alt="Git Stash --all" title="Git Stash --all" /></div></div>
</li>
</ul>
<p>When you run <code>git stash pop</code>, the changes from the commits above are used to update your working copy and index, and the stash reflog is shuffled to remove the popped commit. Note that the popped commits aren't immediately deleted, but do become candidates for future garbage collection.</p>

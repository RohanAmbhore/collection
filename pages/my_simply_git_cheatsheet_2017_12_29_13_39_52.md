<a href="https://gist.github.com/WooodHead/683327f7706b837fc6dd7d0707516e11">https://gist.github.com/WooodHead/683327f7706b837fc6dd7d0707516e11</a><div id="articleHeader"><h1>Using Git</h1></div>
<h2>Global Settings</h2>
<p>Related Setup: <a href="https://gist.github.com/hofmannsven/6814278" target="_blank">https://gist.github.com/hofmannsven/6814278</a></p>
<p>Related Pro Tips: <a href="https://ochronus.com/git-tips-from-the-trenches/" target="_blank">https://ochronus.com/git-tips-from-the-trenches/</a></p>
<p>Interactive Beginners Tutorial: <a href="http://try.github.io/" target="_blank">http://try.github.io/</a></p>
<h2>Reminder</h2>
<p>Press <code>minus + shift + s</code> and <code>return</code> to chop/fold long lines!</p>
<p>Show folder content: <code>ls -la</code></p>
<h2>Notes</h2>
<p>Do not put (external) dependencies in version control!</p>
<h2>Setup</h2>
<p>See where Git is located:
<code>which git</code></p>
<p>Get the version of Git:
<code>git --version</code></p>
<p>Create an alias (shortcut) for <code>git status</code>:
<code>git config --global alias.st status</code></p>

<p>Help:
<code>git help</code></p>
<h2>General</h2>
<p>Initialize Git:
<code>git init</code></p>
<p>Get everything ready to commit:
<code>git add .</code></p>
<p>Get custom file ready to commit:
<code>git add index.html</code></p>
<p>Commit changes:
<code>git commit -m "Message"</code></p>
<p>Add and commit in one step:
<code>git commit -am "Message"</code></p>
<p>Remove files from Git:
<code>git rm index.html</code></p>
<p>Update all changes:
<code>git add -u</code></p>
<p>Remove file but do not track anymore:
<code>git rm --cached index.html</code></p>
<p>Move or rename files:
<code>git mv index.html dir/index_new.html</code></p>
<p>Undo modifications (restore files from latest commited version):
<code>git checkout -- index.html</code></p>
<p>Restore file from a custom commit (in current branch):
<code>git checkout 6eb715d -- index.html</code></p>
<h2>Reset</h2>
<p>Go back to commit:
<code>git revert 073791e7dd71b90daa853b2c5acc2c925f02dbc6</code></p>
<p>Soft reset (move HEAD only; neither staging nor working dir is changed):
<code>git reset --soft 073791e7dd71b90daa853b2c5acc2c925f02dbc6</code></p>
<p>Undo latest commit: <code>git reset --soft HEAD~</code></p>
<p>Mixed reset (move HEAD and change staging to match repo; does not affect working dir):
<code>git reset --mixed 073791e7dd71b90daa853b2c5acc2c925f02dbc6</code></p>
<p>Hard reset (move HEAD and change staging dir and working dir to match repo):
<code>git reset --hard 073791e7dd71b90daa853b2c5acc2c925f02dbc6</code></p>
<h2>Update & Delete</h2>
<p>Test-Delete untracked files:
<code>git clean -n</code></p>
<p>Delete untracked files (not staging):
<code>git clean -f</code></p>
<p>Unstage (undo adds):
<code>git reset HEAD index.html</code></p>
<p>Commit to most recent commit:
<code>git commit --amend -m "Message"</code></p>
<p>Update most recent commit message:
<code>git commit --amend -m "New Message"</code></p>
<h2>Branch</h2>
<p>Show branches:
<code>git branch</code></p>
<p>Create branch:
<code>git branch branchname</code></p>
<p>Change to branch:
<code>git checkout branchname</code></p>
<p>Create and change to new branch:
<code>git checkout -b branchname</code></p>
<p>Rename branch:
<code>git branch -m branchname new_branchname</code> or:
<code>git branch --move branchname new_branchname</code></p>
<p>Show all completely merged branches with current branch:
<code>git branch --merged</code></p>
<p>Delete merged branch (only possible if not HEAD):
<code>git branch -d branchname</code> or:
<code>git branch --delete branchname</code></p>
<p>Delete not merged branch:
<code>git branch -D branch_to_delete</code></p>
<h2>Merge</h2>
<p>True merge (fast forward):
<code>git merge branchname</code></p>
<p>Merge to master (only if fast forward):
<code>git merge --ff-only branchname</code></p>
<p>Merge to master (force a new commit):
<code>git merge --no-ff branchname</code></p>
<p>Stop merge (in case of conflicts):
<code>git merge --abort</code></p>
<p>Stop merge (in case of conflicts):
<code>git reset --merge</code> // prior to v1.7.4</p>
<p>Merge only one specific commit:
<code>git cherry-pick 073791e7</code></p>
<h2>Stash</h2>
<p>Put in stash:
<code>git stash save "Message"</code></p>
<p>Show stash:
<code>git stash list</code></p>
<p>Show stash stats:
<code>git stash show stash@{0}</code></p>
<p>Show stash changes:
<code>git stash show -p stash@{0}</code></p>
<p>Use custom stash item and drop it:
<code>git stash pop stash@{0}</code></p>
<p>Use custom stash item and do not drop it:
<code>git stash apply stash@{0}</code></p>
<p>Delete custom stash item:
<code>git stash drop stash@{0}</code></p>
<p>Delete complete stash:
<code>git stash clear</code></p>
<h2>Gitignore & Gitkeep</h2>
<p>About: <a href="https://help.github.com/articles/ignoring-files" target="_blank">https://help.github.com/articles/ignoring-files</a></p>
<p>Useful templates: <a href="https://github.com/github/gitignore" target="_blank">https://github.com/github/gitignore</a></p>
<p>Add or edit gitignore:
<code>nano .gitignore</code></p>
<p>Track empty dir:
<code>touch dir/.gitkeep</code></p>

<p>Show commits:
<code>git log</code></p>
<p>Show oneline-summary of commits:
<code>git log --oneline</code></p>
<p>Show oneline-summary of commits with full SHA-1:
<code>git log --format=oneline</code></p>
<p>Show oneline-summary of the last three commits:
<code>git log --oneline -3</code></p>
<p>Show only custom commits:
<code>git log --author="Sven"</code>
<code>git log --grep="Message"</code>
<code>git log --until=2013-01-01</code>
<code>git log --since=2013-01-01</code></p>
<p>Show only custom data of commit:
<code>git log --format=short</code>
<code>git log --format=full</code>
<code>git log --format=fuller</code>
<code>git log --format=email</code>
<code>git log --format=raw</code></p>
<p>Show changes:
<code>git log -p</code></p>
<p>Show every commit since special commit for custom file only:
<code>git log 6eb715d.. index.html</code></p>
<p>Show changes of every commit since special commit for custom file only:
<code>git log -p 6eb715d.. index.html</code></p>
<p>Show stats and summary of commits:
<code>git log --stat --summary</code></p>
<p>Show history of commits as graph:
<code>git log --graph</code></p>
<p>Show history of commits as graph-summary:
<code>git log --oneline --graph --all --decorate</code></p>
<h2>Compare</h2>
<p>Compare modified files:
<code>git diff</code></p>
<p>Compare modified files and highlight changes only:
<code>git diff --color-words index.html</code></p>
<p>Compare modified files within the staging area:
<code>git diff --staged</code></p>
<p>Compare branches:
<code>git diff master..branchname</code></p>
<p>Compare branches like above:
<code>git diff --color-words master..branchname^</code></p>
<p>Compare commits:
<code>git diff 6eb715d</code>
<code>git diff 6eb715d..HEAD</code>
<code>git diff 6eb715d..537a09f</code></p>
<p>Compare commits of file:
<code>git diff 6eb715d index.html</code>
<code>git diff 6eb715d..537a09f index.html</code></p>
<p>Compare without caring about spaces:
<code>git diff -b 6eb715d..HEAD</code> or:
<code>git diff --ignore-space-change 6eb715d..HEAD</code></p>
<p>Compare without caring about all spaces:
<code>git diff -w 6eb715d..HEAD</code> or:
<code>git diff --ignore-all-space 6eb715d..HEAD</code></p>
<p>Useful comparings:
<code>git diff --stat --summary 6eb715d..HEAD</code></p>
<p>Blame:
<code>git blame -L10,+1 index.html</code></p>
<h2>Releases & Version Tags</h2>
<p>Show all released versions:
<code>git tag</code></p>
<p>Show all released versions with comments:
<code>git tag -l -n1</code></p>
<p>Create release version:
<code>git tag v1.0.0</code></p>
<p>Create release version with comment:
<code>git tag -a v1.0.0 -m 'Message'</code></p>
<p>Checkout a specific release version:
<code>git checkout v1.0.0</code></p>
<h2>Collaborate</h2>
<p>Show remote:
<code>git remote</code></p>
<p>Show remote details:
<code>git remote -v</code></p>
<p>Add remote origin from GitHub project:
<code>git remote add origin https://github.com/user/project.git</code></p>
<p>Add remote origin from existing empty project on server:
<code>git remote add origin ssh://root@123.123.123.123/path/to/repository/.git</code></p>
<p>Remove origin:
<code>git remote rm origin</code></p>
<p>Show remote branches:
<code>git branch -r</code></p>
<p>Show all branches:
<code>git branch -a</code></p>
<p>Compare:
<code>git diff origin/master..master</code></p>
<p>Push (set default with <code>-u</code>):
<code>git push -u origin master</code></p>
<p>Push to default:
<code>git push origin master</code></p>
<p>Fetch:
<code>git fetch origin</code></p>
<p>Fetch a custom branch:
<code>git fetch origin branchname:local_branchname</code></p>
<p>Pull:
<code>git pull</code></p>
<p>Pull specific branch:
<code>git pull origin branchname</code></p>
<p>Merge fetched commits:
<code>git merge origin/master</code></p>
<p>Clone to localhost:
<code>git clone https://github.com/user/project.git</code> or:
<code>git clone ssh://user@domain.com/~/dir/.git</code></p>
<p>Clone to localhost folder:
<code>git clone https://github.com/user/project.git ~/dir/folder</code></p>
<p>Clone specific branch to localhost:
<code>git clone -b branchname https://github.com/user/project.git</code></p>
<p>Delete remote branch (push nothing):
<code>git push origin :branchname</code> or:
<code>git push origin --delete branchname</code></p>
<h2>Archive</h2>
<p>Create a zip-archive: <code>git archive --format zip --output filename.zip master</code></p>
<p>Export/write custom log to a file: <code>git log --author=sven --all &gt; log.txt</code></p>
<h2>Troubleshooting</h2>
<p>Ignore files that have already been committed to a Git repository: <a href="http://stackoverflow.com/a/1139797/1815847" target="_blank">http://stackoverflow.com/a/1139797/1815847</a></p>
<h2>Security</h2>
<p>Hide Git on the web via <code>.htaccess</code>: <code>RedirectMatch 404 /\.git</code>
(more info here: <a href="http://stackoverflow.com/a/17916515/1815847" target="_blank">http://stackoverflow.com/a/17916515/1815847</a>)</p>
<h2>Large File Storage</h2>
<p>Website: <a href="https://git-lfs.github.com/" target="_blank">https://git-lfs.github.com/</a></p>
<p>Install: <code>brew install git-lfs</code></p>
<p>Track <code>*.psd</code> files: <code>git lfs track "*.psd"</code> (init, add, commit and push as written above)</p>

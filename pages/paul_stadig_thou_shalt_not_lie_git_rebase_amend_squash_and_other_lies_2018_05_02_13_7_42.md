<a href="http://paul.stadig.name/2010/12/thou-shalt-not-lie-git-rebase-ammend.html">http://paul.stadig.name/2010/12/thou-shalt-not-lie-git-rebase-ammend.html</a><div id="articleHeader"><h1>Thou Shalt Not Lie: git rebase, amend, squash, and other lies</h1></div>


<p>As I've used git more, and used more advanced features, my opinions about the merit and uses of certain features have changed.  At work we're constantly re-evaluating our git workflow in light of the problems we encounter with the way we're doing things. I may yet re-evaluate these opinions, but rest assured they come not from some theoretical nit-pick, but from real experience.</p>

<h3>Rewriting History is a Lie</h3>
<p>Using git to rewrite history is a sin.  It's called lying.  Don't do it.  With git there are several forms in which lying comes, but usually you know you're lying if you break the functionality of <code>`git branch --contains some-branch`</code>, <code>`git blame`</code>, <code>`git bisect`</code>, or if you have to use <code>`git push -f origin some-branch`</code>.</p>

<h3>Squash merging is a lie</h3>
<p>A squash merge (<code>`git merge --squash some-branch`</code>) takes all the commits from a topic branch, combines them into a single commit, and applies that commit.  The history now looks as if you had a flash of brilliance, made a ton of changes, and did everything right the first time.  It makes you look good, but it's a lie.</p>

<p>Since, you have not actually merged any of the work you did on the topic branch, but instead have merged another <em>totally new</em> commit, <code>`git branch --contains some-branch`</code> cannot tell you that you have merged your branch anywhere.  When a QA person or your boss says, "Hey, is some-feature {merged into QA, deployed}" you have to resort to <code>`git log`</code> spelunking.</p>

<p>Also, anytime you are creating a <em>new commit</em> with the same changes as another commit, you are destroying <code>`git blame`</code>'s ability to tell you who to flog publicly.  And as we all know, public floggings are the lifeblood of software development teams.</p>

<p>Finally, when you squash merge, the totally awesome <a href="http://progit.org/2010/03/08/rerere.html" target="_blank">rerere</a> feature will not help you re-resolve conflicts.  Instead you will have to re-resolve conflicts when you cherry pick the squash commit, or when you squash merge your topic branch to the UA branch or to master.  Why?  Because <code>rerere</code> depends on being able to detect that you are resolving conflicts between the same SHAs as before, but every time you squash merge it creates a <em>totally new</em> commit. It creates a totally new commit even if you squash merge, <code>`git reset --hard HEAD^`</code>, and then immediately squash merge again.</p>

<h3>Rebasing is a lie</h3>
<p>Rebasing using <code>`git rebase foo`</code> allows you to rebase your topic branch on foo, instead of whatever it was based on before.  This makes it look like you were working from foo the whole time.  However, each commit to your topic branch was birthed in a context and by a sequence of events that was unique to that time and that topic branch.  You are yanking those commits out of their context and putting them into a <em>totally new</em> context.</p>

<p>Rebasing is effectively a retroactive merge.  It is pretending that you "merged" foo into your topic branch 3 days ago, but you didn't.  You merged it in today, and you are lying to everyone.</p>

<p>In fact, the commits from your topic branch don't exist anymore, because every single rebased commit gets remade into a <em>totally new</em> commit with a <em>totally different</em> SHA. Pick any one of those rebased commits: Does the commit message make sense anymore?  Does the code compile?  Do the tests pass?</p>

<p>The answer to these last two questions will tell you whether you can use the totally awesome <code>bisect</code> feature of git.  This feature does a binary search through your history to help you discover exactly where some bug or problem was introduced into your code.  If you cannot compile and run tests on every commit, then you cannot use <code>`git bisect`</code>, which is a shame.</p>

<p>Being able to compile and run tests for each commit is also useful for resolving conflicts.  Say I'm trying to decide whether your change will work with my code, or my change with your code, or maybe some totally different code that "resolves" the conflict, how can I know "resolved" means resolved?  The most basic thing I can do (though it's not foolproof) is compile the code and run the tests, but if your code doesn't even compile or run the tests by itself, then I can't intelligently resolve the conflict.  Your lie has hurt me and the rest of the team.</p>

<p>Finally, if for some reason you wanted to cherry-pick a commit, but it doesn't compile or run the tests, then cherry-picking it into another branch would break that branch.  Thanks for that!  Your lie has now become destruction of property, which is a misdemeanor.</p>

<h3>Amending a commit is a lie</h3>
<p>Amending a commit (<code>`git commit --amend`</code>) to add changes, or to change the commit message is a lie.  It breaks <code>`git branch --contains some-branch`</code>.  It forces you to do a <code>`git push -f origin some-branch`</code>.  It's a sin.  See above arguments, enough said.</p>

<h3>Selective, retroactive commits are lies</h3>
<p>In this last form of lying git is not an accomplice, because you are lying <em>to</em> git.  What happens here is that you have been working for a while (20 minutes, 30 minutes, an hour, whatever), and you decide to commit your work, but instead of committing all of your work as you have come to it naturally, you decide to break your work up into several small, "logical" commits.  This makes you look good, but it's a lie.</p>

<p>You've changed both "foo.clj" and "bar.clj" and you think there is no dependency between them, so you commit "foo.clj" separately from "bar.clj".  The problem is that you don't <em>really</em> know this unless you compile the code and run the tests.  Since you don't know for sure that these selective commits can compile and run the tests, you've broken <code>`git bisect`</code>, undermined trust in conflict resolution, and break my stuff if I cherry-pick your commit.</p>

<p>You may think that your commits are "logical", but I would say if you are not committing your work the way that you come to it naturally, then it is not logical.  Sure you started solving problem A and then discovered problem B, if they are related and you have to solve problem B in order to solve A, then commit the changes together.  They are related so its logical to commit them at the same time.</p>

<p>If you want to solve them separately, then make a WIP commit or a stash, create another branch and solve B, then come back to your original branch and rebase it on B (gasp, see below for explanations of this inconsistency!).</p>

<h3>Conclusion</h3>
<p>There are several awesome features of git: <code>blame</code>, <code>branch --contains</code>, <code>rerere</code>, and <code>bisect</code>.  These features are borked if you lie.  If you're going to lie, you may as well use SVN, since these awesome features don't exist there anyway.  But don't do that!  Let's just all agree not to lie.</p>

<h3>Epilogue</h3>
<p>Some people may get the impression that I do not think you should ever use <code>`git rebase`</code>, <code>`git commit --amend`</code>, or <code>`git merge --squash`</code>, but that would not be true.  These are powerful tools that may be necessary sometimes, but should be used sparingly and judiciously.  Perhaps its OK to lie sometimes.  If someone comes up to you and says, "How does this make me look?"  You choose your words carefully.</p>

<p>One case for history rewriting is integration branches. At work we have integration branches for qa, ua, etc.  We have a workflow where we move a single feature through the pipeline kanban style, so we have to be able to merge a feature to an integration branch, rebase it out, etc.  In this case no one has an expectation that they should be able to see a clean history for these branches, and no one expects to base their work on one of them.</p>

<p>Other than integration branches, a good rule of thumb is that you should not rewrite history for things that are already push out into the world.  This would limit these rewriting tools to uses locally to "fix" things up before pushing them.  I still cannot whole-heartedly advise use of rewriting in this case, but if you need to, and the rewriting your doing is limited enough that you're sure the new commits will still compile and pass tests, then fine.  Just do it carefully, and don't make it habitual. The End.</p>


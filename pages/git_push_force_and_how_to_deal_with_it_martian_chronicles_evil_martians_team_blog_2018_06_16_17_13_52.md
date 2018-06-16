<a href="https://evilmartians.com/chronicles/git-push---force-and-how-to-deal-with-it">https://evilmartians.com/chronicles/git-push---force-and-how-to-deal-with-it</a><div id="articleHeader"><h1><b>git push --force</b> and how to deal with it</h1></div><div>September 12, 2017</div></article>
<div>
  <p>Have you ever found yourself in a situation where a wrong git command wreaked havoc on your project’s repo? People make mistakes, and sometimes those mistakes can cost hours of your team’s time. In this tutorial, we will show you how to recover from an unfortunate <code>git push --force</code> quickly.</p>
</div>

<p>Let’s not get overly confident. Sooner or later, this is going to happen. While working with several remotes in the same git repository, you <em>will</em> eventually <code>git push --force</code> into <code>master</code> (or another important branch that should never be messed with).</p>

<p>That may happen, for instance, when deploying with <a href="https://deis.com/" target="_blank">Deis</a> or <a href="http://heroku.com" target="_blank">Heroku</a> that use separate git remotes to build and deploy an application. After a long day of work, it is incredibly easy to execute <code>git push --force</code> instead of usual <code>git push --force deis master</code>.</p>

<p>Oops! In the blink of an eye, your teammates have lost all their latest work. Time to face their rage.</p>

<p>However, as one excellent guide tells us, <a href="https://en.wikipedia.org/wiki/Phrases_from_The_Hitchhiker%27s_Guide_to_the_Galaxy#Don.27t_Panic" target="_blank">DON’T PANIC</a>! The good thing is, you use git, and that means <em>everything</em> can be fixed.</p>

<blockquote>
  <p>Best case scenario: someone else who is working on the same code pulled a recent version of the <code>master</code> just before you broke it. Then all you have to do is to go into your team’s chat and ask that person to <em>force push</em> their recent changes.</p>
</blockquote>

<p>If you are lucky, their local repository will have the full history of commits, your mistake will be overwritten with fresh code, and nothing will be lost. But what if you are not that lucky? Then, read on!</p>

<h2 id="case-1-you-were-the-last-person-to-push-to-master-before-the-mistake">Case 1: You were the last person to push to <code>master</code> before the mistake</h2>

<p>Good news! You have everything you need to undo your mistake before your very eyes. Just <em>do not</em> close or clear your terminal. First, go into your team’s chat and confess your sins. Ask people not to mess with the repo for the next minute or so while you are fixing things.</p>

<p>In the output of <code>git push --force</code> command in your shell look for a line that resembles this one:</p>

<div>
<pre><code> + deadbeef...f00f00ba master -&gt; master (forced update)
</code></pre>
</div>

<p>The first group of symbols (which looks like a commit’s SHA prefix) is the key to the rescue. <code>deadbeef</code> <em>is</em> your last good commit to the <code>master</code> just before you inflicted damage.</p>

<p>So all you need is to… <em>force push</em> (fighting fire with fire!) this commit back to the <code>master</code> branch, on top a bad one.</p>

<div>
<pre><code>$ git push --force origin deadbeef:master
</code></pre>
</div>

<p>Congratulations! You have saved the day. Now it’s time to learn from your mistakes.</p>

<h2 id="case-2-master-was-changed-by-someone-else-before-you-messed-up">Case 2: <code>master</code> was changed by someone else before you messed up</h2>

<p>So, just before you did <code>git push --force</code> someone had closed a bunch of pull requests, and the <code>master</code> now looks nothing like your local copy. You can no longer do <code>git push --force sha1:master</code> as <em>you do not have recent commits locally</em> (and you can’t get them with <code>git fetch</code> because they do not belong to any branch anymore). Still, keep calm and ask your teammates to stay off the remote for a while.</p>

<blockquote>
  <p>We will benefit from the fact that GitHub does not remove unreachable commits immediately. Of course, you can not fetch them either, but there is a workaround.</p>
</blockquote>

<p>Note that it will only work if you are “watching” the repository, so that everything happening in it appears in a feed displayed on your GitHub’s front page. Open that feed and look for something like this:</p>

<div>
<pre><code>an hour ago
Username pushed to master at org/repo
 - deadbeef Implement foo
 - deadf00d Fix bar
</code></pre>
</div>

<p>Now you can:</p>

<ul>
  <li>Compose a URL <code>https://github.com/org/repo/tree/deadbeef</code>, where <code>deadbeef</code> is a hash of the last good commit to the damaged branch;</li>
  <li>Open the branches/tags switcher in the GitHub’s web UI;</li>
</ul>

<figure>
  <p><div class="readableLargeImageContainer"><img src="https://cdn.evilmartians.com/front/posts/git-push---force-and-how-to-deal-with-it/github-branch-switcher-810ee93.png"   alt="GitHub branch/tag switcher" /></div></p>

  <figcaption>
    <p>GitHub branch/tag switcher</p>
  </figcaption>
</figure>

<ul>
  <li>Create a name for a new temporary branch (e.g., <code>master-before-force-push</code>);</li>
  <li>Click “Create branch”.</li>
</ul>

<p>Now you can fetch all missing commits:</p>

<div>
<pre><code>$ git fetch
From github.com:org/repo
 * [new branch]      master-before-force-push -&gt; origin/master-before-force-push
</code></pre>
</div>

<p>Your problem is now reduced to the one described in a previous example:</p>

<div>
<pre><code>$ git push --force origin origin/master-before-force-push:master
</code></pre>
</div>

<p>If you still need your work to be in the <code>master</code>, just rebase on top of it:</p>

<div>
<pre><code>$ git rebase origin/master
</code></pre>
</div>

<h2 id="how-to-avoid-such-disaster-in-the-future">How to avoid such disaster in the future</h2>

<ol>
  <li>
    <p>GitHub and GitLab have a feature called “protected branches.”  Mark <code>master</code>, <code>develop</code>, <code>stable</code>, or any other crucial branches as protected and no one will be allowed to force push into them. It is always possible to temporarily “unprotect” a branch if you really need to overwrite history.</p>

    <p>Read the <a href="https://help.github.com/articles/defining-the-mergeability-of-pull-requests/" target="_blank">GitHub docs</a> for details.</p>
  </li>
  <li>
    <p>Instead of <code>--force</code> option, use <code>--force-with-lease</code>. It will halt the push operation if someone has pushed to the same branch while you were working on it (and haven’t pulled any changes).</p>

    <p>See this <a href="https://developer.atlassian.com/blog/2015/04/force-with-lease/" target="_blank">article from Atlassian</a>.</p>
  </li>
  <li>
    <p>Create aliases for commands that use <code>git push --force</code> to prevent destructive actions by accident:</p>

    <div>
<pre><code># ~/.gitconfig
[alias]
  deploy = "!git push --force deis \"$(git rev-parse --abbrev-ref HEAD):master\""
</code></pre>
    </div>

    <p>Read the <a href="https://git-scm.com/book/tr/v2/Git-Basics-Git-Aliases" target="_blank">ProGit chapter about aliases</a>.</p>
  </li>
  <li>
    <p>Never do your experiments in the main branch of a repository! <code>git checkout -b experiments</code> is your best friend.</p>
  </li>
</ol>

<hr />

<p><strong>Pro Tip</strong>: <code>git push</code> has many options. <code>--force</code> and <code>--all</code> work together especially well. You can use this combo when returning to the project after several months of inactivity. Give it a try if you’re feeling extra adventurous!</p>


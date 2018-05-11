<a href="https://stackoverflow.com/questions/804115/when-do-you-use-git-rebase-instead-of-git-merge">https://stackoverflow.com/questions/804115/when-do-you-use-git-rebase-instead-of-git-merge</a><div id="articleHeader"><h1>When do you use git rebase instead of git merge?</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        1201
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>480</b></div>


</div>

            </div>

            
<div>
    <div>

<p>When is it recommended to use <code>git rebase</code> vs. <code>git merge</code>?</p>

<p>Do I still need to merge after a successful rebase?</p>
    </div>
    
    
</div>

                        <div>
                <div>
        <h2>                    <b>protected</b> by <a href="/users/584518/lundin" target="_blank">Lundin</a> Aug 28 '17 at 7:36
</h2>
        <p>
This question is protected to prevent "thanks!", "me too!", or spam answers by new users. 
To answer it, you must have earned at least 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).</p>
    </div>
            </div>
    
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-804156">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        953
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<h2>Short Version</h2>

<ul>
<li>Merge takes all the changes in one branch and merges them into another branch in one commit.</li>
<li>Rebase says I want the point at which I branched to move to a new starting point</li>
</ul>

<p>So when do you use either one?</p>

<h3>Merge</h3>

<ul>
<li>Let's say you have created a branch for the purpose of developing a single feature.  When you want to bring those changes back to master, you probably want <strong>merge</strong> (you don't care about maintaining all of the interim commits).  </li>
</ul>

<h3>Rebase</h3>

<ul>
<li>A second scenario would be if you started doing some development and then another developer made an unrelated change.  You probably want to pull and then <strong>rebase</strong> to base your changes from the current version from the repo.</li>
</ul>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-804178">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        251
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>To complement <a href="https://stackoverflow.com/questions/457927/git-workflow-and-rebase-vs-merge-questions" target="_blank">my own answer</a> mentioned <a href="https://stackoverflow.com/questions/804115/git-rebase-vs-git-merge/804119#804119" target="_blank">by TSamper</a>, </p>

<ul>
<li><p>a rebase is quite often a good idea to do before a merge, because the idea is that you integrate in your branch <code>Y</code> the work of the branch <code>B</code> upon which you will merge.<br />
But again, before merging, you resolve any conflict in <em>your</em> branch (i.e.: "rebase", as in "replay my work in my branch starting from a recent point from the branch <code>B</code>)<br />
If done correctly, the subsequent merge from your branch to branch <code>B</code> can be fast-forward.</p></li>
<li><p>a merge impact directly the destination branch <code>B</code>, which means the merges better be trivial, otherwise that branch <code>B</code> can be long to get back to a stable state (time for you solve all the conflicts)</p></li>
</ul>

<hr />

<blockquote>
  <p>the point of merging after a rebase? </p>
</blockquote>

<p>In the case that I describe, I rebase <code>B</code> onto my branch, just to have the opportunity to replay my work from a more recent point from <code>B</code>, but while staying into my branch.<br />
In this case, a merge is still needed to bring my "replayed" work onto <code>B</code>.</p>

<p>The other scenario (<a href="http://www.gitready.com/intermediate/2009/01/31/intro-to-rebase.html" target="_blank">described in Git Ready</a> for instance), is to bring your work directly in <code>B</code> through a rebase (which does conserve all your nice commits, or even give you the opportunity to re-order them through an interactive rebase).<br />
In that case (where you rebase while being in the B branch), you are right: no further merge is needed:</p>

<p><strong>A git tree at default when we have not merged nor rebased</strong></p>

<p><img src="https://i.stack.imgur.com/7vsGZ.png" alt="rebase1" /> </p>

<p><strong>we get by rebasing:</strong></p>

<p><img src="https://i.stack.imgur.com/yCxOO.png" alt="rebase3" /></p>

<p>That second scenario is all about: how do I get new-feature back into master.</p>

<p>My point, by describing the first rebase scenario, is to remind everyone that a rebase can also be used as a preliminary step to that (that being "get new-feature back into master").<br />
You can use rebase to first bring master "in" the new-feature branch: the rebase will replay new-feature commits from the <code>HEAD master</code>, but still in the new-feature branch, effectively moving your branch starting point from an old master commit to <code>HEAD-master</code>.<br />
That allows you to resolve any conflicts in <em>your</em> branch (meaning, in isolation, while allowing master to continue to evolve in parallel if your conflict resolution stage takes too long).<br />
Then you can switch to master and merge <code>new-feature</code> (or rebase <code>new-feature</code> onto <code>master</code> if you want to preserve commits done in your <code>new-feature</code> branch).</p>



<ul>
<li>"rebase vs. merge" can be viewed as two ways to import a work on, say, <code>master</code>.  </li>
<li>But "rebase then merge" can be a valid workflow to first resolve conflict in isolation, then bring back your work.</li>
</ul>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-9147389">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        276
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>It's simple, with rebase you say to use another branch as the new <strong>base</strong> for your work.</p>

<p>If you have for example a branch <code>master</code> and you create a branch to implement a new feature, say you name it <code>cool-feature</code>, of course the master branch is the base for your new feature.</p>

<p>Now at a certain point you want to add the new feature you implemented in the <code>master</code> branch. You could just switch to <code>master</code> and merge the <code>cool-feature</code> branch:</p>

<pre><code>$git checkout master
$git merge cool-feature
</code></pre>

<p>but this way a new dummy commit is added, if you want to avoid spaghetti-history you can <strong>rebase</strong>:</p>

<pre><code>$git checkout cool-feature
$git rebase master
</code></pre>

<p>and then merge it in <code>master</code>:</p>

<pre><code>$git checkout master
$git merge cool-feature
</code></pre>

<p>This time, since the topic branch has the same commits of master plus the commits with the new feature, the merge will be just a fast-forward.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-9147473">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        65
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Merge means: Create a single new commit that merges my changes into the destination.</p>

<p>Rebase means: Create a whole new series of commits, using my current set of commits as hints. In other words, calculate what my changes would have looked like if I had started making them from the point I'm rebasing on to. After the rebase, therefore, you might need to re-test your changes and during the rebase, you would possibly have a few conflicts. </p>

<p>Given this, why would you rebase? Just to keep the development history clear. Let's say you're working on feature X and when you're done, you merge your changes in. The destination will now have a single commit that would say something along the lines of "Added feature X". Now, instead of merging, if you rebased and then merged, the destination development history would contain all the individual commits in a single logical progression. This makes reviewing changes later on much easier. Imagine how hard you'd find it to review the development history if 50 developers were merging various features all the time.  </p>

<p>That said, if you have already pushed the branch you're working on upstream, you should not rebase, but merge instead. For branches that have not been pushed upstream, rebase, test and merge. </p>

<p>Another time you might want to rebase is when you want to get rid of commits from your branch before pushing upstream. For example: Commits that introduce some debugging code early on and other commits further on that clean that code up. The only way to do this is by performing an interactive rebase: <code>git rebase -i &lt;branch/commit/tag&gt;</code></p>

<p>UPDATE: You also want to use rebase when you're using Git to interface to a version control system that doesn't support non-linear history (subversion for example). When using the git-svn bridge, it is very important that the changes you merge back into subversion are a sequential list of changes on top of the most recent changes in trunk. There are only two ways to do that: (1) Manually re-create the changes and (2) Using the rebase command, which is a lot faster.</p>

<p>UPDATE2 : One additional way to think of a rebase is that it enables a sort of mapping from your development style to the style accepted in the repository you're committing to. Let's say you like to commit in small, tiny chunks. You have one commit to fix a typo, one commit to get rid of unused code and so on. By the time you've finished what you need to do, you have a long series of commits. Now let's say the repository you're committing to encourages large commits, so for the work you're doing, one would expect one or maybe two commits. How do you take your string of commits and compress them to what is expected? You would use an interactive rebase and squash your tiny commits into fewer larger chunks. The same is true if the reverse was needed - if your style was a few large commits, but the repo demanded long strings of small commits. You would use a rebase to do that as well. If you had merged instead, you have now grafted your commit style onto the main repository. If there are a lot of developers, you can imagine how hard it would be to follow a history with several different commit styles after some time.</p>

<p>UPDATE3: <code>Does one still need to merge after a successful rebase?</code> Yes, you do. The reason is that a rebase essentially involves a "shifting" of commits. As I've said above, these commits are calculated, but if you had 14 commits from the point of branching, then assuming nothing goes wrong with your rebase, you will be 14 commits ahead (of the point you're rebasing onto) after the rebase is done. You had a branch before a rebase. You will have a branch of the same length after. You still need to merge before you publish your changes. In other words, rebase as many times as you want (again, only if you have not pushed your changes upstream). Merge only after you rebase.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-10926614">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        54
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>before merge/rebase:</p>

<pre><code>A &lt;- B &lt;- C    [master]
^
 \
  D &lt;- E       [branch]
</code></pre>

<p>after <code>git merge master</code>:</p>

<pre><code>A &lt;- B &lt;- C
^         ^
 \         \
  D &lt;- E &lt;- F
</code></pre>

<p>after <code>git rebase master</code>:</p>

<pre><code>A &lt;- B &lt;- C &lt;- D' &lt;- E'
</code></pre>

<p>(A, B, C, D, E and F are commits)</p>

<p>this example and much more well illustrated info about git can be found here: <a href="http://excess.org/article/2008/07/ogre-git-tutorial/" target="_blank">http://excess.org/article/2008/07/ogre-git-tutorial/</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jun 7 '12 at 6:19
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-13980932">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        14
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>The pro git book as a really good explanation on the <a href="http://git-scm.com/book/en/Git-Branching-Rebasing" target="_blank">rebasing page</a>.</p>

<p>Basically a merge will take 2 commits and combine them.</p>

<p>A rebase will go to the common ancestor on the 2 and incrementally apply the changes on top of each other. This makes for a 'cleaner' and more linear history. </p>

<p>But when you rebase you abandon previous commits and create new ones. So you should never rebase a repo that is public. The other people working on the repo will hate you.</p>

<p>For that reason alone I almost exclusively merge. 99% of the time my branches don’t differ that much, so if there are conflicts it's only in one or two places.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-18974177">
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
<p>Git rebase is used to make the branching paths in history cleaner and repository structure linear. </p>

<p>It is also used to keep the branches created by you private, as after rebasing and pushing the changes to server, if you delete your branch, there will be no evidence of branch you have worked upon. So your branch is now your local concern.</p>

<p>After doing rebase we also get rid of an extra commit which we used to see if we do normal merge. </p>

<p>And yes one still needs to do merge after a successful rebase as rebase command just puts your work on top of the branch you mentioned during rebase say master and makes the first commit of your branch as a direct descendant of the master branch. This means we can now do a fast forward merge to bring changes from this branch to master branch.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Sep 24 '13 at 6:11
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-21539012">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        142
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>A lot of answers here say that merging turns all your commits into one, and therefore suggest to use rebase to preserve your commits. <strong>This is incorrect. And a bad idea if you have pushed your commits already</strong>.</p>

<p>Merge does <em>not</em> obliterate your commits. Merge preserves history! (just look at gitk) Rebase rewrites history, which is a Bad Thing after you've <em>pushed</em> it.</p>

<p><strong>Use merge -- not rebase</strong> whenever you've already pushed.</p>

<p><a href="http://thread.gmane.org/gmane.comp.video.dri.devel/34739/focus=34744" target="_blank">Here is Linus' (author of git) take on it</a>. It's a really good read. Or you can read my own version of the same idea below.</p>

<p>Rebasing a branch on master:</p>

<ul>
<li>provides an incorrect idea of how commits were created</li>
<li>pollutes master with a bunch of intermediate commits that may not have been well tested</li>
<li>could actually introduce build breaks on these intermediate commits because of changes that were made to master between when the original topic branch was created and when it was rebased.</li>
<li>makes finding good places in master to checkout difficult.</li>
<li>Causes the timestamps on commits to not align with their chronological order in the tree. So you would see that commit A precedes commit B in master, but commit B was authored first. (What?!)</li>
<li>Produces more conflicts because individual commits in the topic branch can each involve merge conflicts which must be individually resolved (Further lying in history about what happened in each commit).</li>
<li>is a rewrite of history. If the branch being rebased has been pushed anywhere (shared with anyone other than yourself) then you've screwed up everyone else who has that branch since you've rewritten history. </li>
</ul>

<p>In contrast, merging a topic branch into master:</p>

<ul>
<li>preserves history of where topic branches were created, including any merges from master to the topic branch to help keep it current. You really get an accurate idea of what code the developer was working with when they were building.</li>
<li>master is a branch made up mostly of merges, and each of those merge commits are typically 'good points' in history that are safe to check out because that's where the topic branch was ready to be integrated.</li>
<li>all the individual commits of the topic branch are preserved, including the fact that they were in a topic branch, so isolating those changes is natural and you can drill in where required.</li>
<li>merge conflicts only have to be resolved once (at the point of the merge) so intermediate commit changes made in the topic branch don't have to be resolved independently.</li>
<li>can be done multiple times smoothly. If you integrate your topic branch to master periodically, folks can keep building on the topic branch and it can keep being merged independently.</li>
</ul>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-27780931">
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
<p>This sentence gets it:</p>

<blockquote>
  <p>In general the way to get the best of both worlds is to rebase local
  changes you’ve made but haven’t shared yet before you push them in
  order to clean up your story, but never rebase anything you’ve pushed
  somewhere.</p>
</blockquote>

<p>Source: <a href="http://www.git-scm.com/book/en/v2/Git-Branching-Rebasing#Rebase-vs.-Merge" target="_blank">http://www.git-scm.com/book/en/v2/Git-Branching-Rebasing#Rebase-vs.-Merge</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 5 '15 at 13:50
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-35570171">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Some practical examples, somewhat connected to large scale development where gerrit is used for review and delivery integration.</p>

<p>I merge when i uplift my feature branch to a fresh remote master. This gives minimal uplift work and it's easy to follow the history of the feature development in for example gitk.</p>

<pre><code>git fetch
git checkout origin/my_feature
git merge origin/master
git commit
git push origin HEAD:refs/for/my_feature
</code></pre>

<p>I merge when I prepare a delivery commit.</p>

<pre><code>git fetch
git checkout origin/master
git merge --squash origin/my_feature
git commit
git push origin HEAD:refs/for/master
</code></pre>

<p>I rebase when my delivery commit fails integration for whatever reason and I need to update it towards a fresh remote master.</p>

<pre><code>git fetch
git fetch &lt;gerrit link&gt;
git checkout FETCH_HEAD
git rebase origin/master
git push origin HEAD:refs/for/master
</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-36587353">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        105
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<h1>TL;DR</h1>

<p>If you have any doubt, use merge.</p>

<h2>Short Answer</h2>

<p>The only differences between a rebase and a merge are:</p>

<ul>
<li>The resulting tree structure of the history (generally only noticeable when looking at a commit graph) is different (one will have branches, the other won't).</li>
<li>Merge will generally create an extra commit (e.g. node in the tree).</li>
<li>Merge and rebase will handle conflicts differently.  Rebase will present conflicts one commit at a time where merge will present them all at once.</li>
</ul>

<p>So the short answer is to <em>pick rebase or merge based on what you want your history to look like</em>.</p>

<h2>Long Answer</h2>

<p>There are a few factors you should consider when choosing which operation to use.</p>

<h3>Is the branch you are getting changes from shared with other developers outside your team (e.g. open source, public)?</h3>

<p>If so, don't rebase.  Rebase destroys the branch and those developers will have broken/inconsistent repositories unless they use <code>git pull --rebase</code>.  This is a good way to upset other developers quickly.</p>

<h3>How skilled is your development team?</h3>

<p>Rebase is a destructive operation.  That means, if you do not apply it correctly, <strong>you could lose committed work and/or break the consistency of other developer's repositories.</strong></p>

<p>I've worked on teams where the developers all came from a time when companies could afford dedicated staff to deal with branching and merging.  Those developers don't know much about Git and don't want to know much.  In these teams I wouldn't risk recommending rebasing for any reason.</p>

<h3>Does the branch itself represent useful information</h3>

<p>Some teams use the branch-per-feature model where each branch represents a feature (or bugfix, or sub-feature, etc.)  In this model the branch helps identify sets of related commits.  For example, one can quickly revert a feature by reverting the merge of that branch (to be fair, this is a rare operation).  Or diff a feature by comparing two branches (more common).  Rebase would destroy the branch and this would not be straightforward.</p>

<p>I've also worked on teams that used the branch-per-developer model (we've all been there).  In this case the branch itself doesn't convey any additional information (the commit already has the author).  There would be no harm in rebasing.</p>

<h3>Might you want to revert the merge for any reason?</h3>

<p>Reverting (as in undoing) a rebase is considerably difficult and/or impossible (if the rebase had conflicts) compared to reverting a merge.  If you think there is a chance you will want to revert then use merge.</p>

<h3>Do you work on a team?  If so, are you willing to take an all or nothing approach on this branch?</h3>

<p>Rebase operations need to be pulled with a corresponding <code>git pull --rebase</code>.  If you are working by yourself you may be able to remember which you should use at the appropriate time.  If you are working on a team this will be very difficult to coordinate.  This is why most rebase workflows recommend using rebase for all merges (and <code>git pull --rebase</code> for all pulls).</p>

<h2>Common Myths</h2>

<h3>Merge destroys history (squashes commits)</h3>

<p>Assuming you have the following merge:</p>

<pre><code>    B -- C
   /      \
  A--------D
</code></pre>

<p>Some people will state that the merge "destroys" the commit history because if you were to look at the log of only the master branch (A -- D) you would miss the important commit messages contained in B and C.</p>

<p>If this were true we wouldn't have <a href="https://stackoverflow.com/questions/15875253/git-log-to-return-only-the-commits-made-to-the-master-branch" target="_blank">questions like this</a>.  Basically, you will see B and C unless you explicitly ask not to see them (using --first-parent).  This is very easy to try for yourself.</p>

<h3>Rebase allows for safer/simpler merges</h3>

<p>The two approaches merge differently, but it is not clear that one is always better than the other and it may depend on the developer workflow.  For example, if a developer tends to commit regularly (e.g. maybe they commit twice a day as they transition from work to home) then there could be a lot of commits for a given branch.  Many of those commits might not look anything like the final product (I tend to refactor my approach once or twice per feature).  If someone else was working on a related area of code and they tried to rebase my changes it could be a fairly tedious operation.</p>

<h3>Rebase is cooler / sexier / more professional</h3>

<p>If you like to alias <code>rm</code> to <code>rm -rf</code> to "save time" then maybe rebase is for you.</p>

<h1>My Two Cents</h1>

<p>I always think that someday I will come across a scenario where git rebase is the awesome tool that solves the problem.  Much like I think I will come across a scenario where git reflog is an awesome tool that solves my problem.  I have worked with git for over five years now.  It hasn't happened.</p>

<p>Messy histories have never really been a problem for me.  I don't ever just read my commit history like an exciting novel.  A majority of the time I need a history I am going to use git blame or git bisect anyways.  In that case having the merge commit is actually useful to me because if the merge introduced the issue that is meaningful information to me.</p>

<h1>Update (4/2017)</h1>

<p>I feel obligated to mention that I have personally softened on using rebase although my general advice still stands.  I have recently been interacting a lot with the <a href="https://github.com/angular/material2" target="_blank">Angular 2 Material</a> project.  They have used rebase to keep a very clean commit history.  This has allowed me to very easily see what commit fixed a given defect and whether or not that commit was included in a release.  It serves as a great example of using rebase correctly.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-42165259">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        14
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>


<p>This answer is widely oriented around <a href="http://nvie.com/posts/a-successful-git-branching-model/" target="_blank">Git Flow</a>. The tables have been generated with the nice <a href="https://ozh.github.io/ascii-tables/" target="_blank">ASCII Table Generator</a>, and the history trees with this wonderful command (<a href="https://githowto.com/aliases" target="_blank">aliased</a> as <code>git lg</code>):</p>

<pre><code>git log --graph --abbrev-commit --decorate --date=format:'%Y-%m-%d %H:%M:%S' --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%ad%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)'</code></pre>

<p>Tables are in reverse chronological order to be more consistent with the history trees. See also the difference between <code>git merge</code> and <code>git merge --no-ff</code> first (you usually want to use <code>git merge --no-ff</code> as it makes your history look closer to the reality):</p>

<h3><code>git merge</code></h3>

<p>Commands:</p>

<pre><code>Time          Branch "develop"             Branch "features/foo"
------- ------------------------------ -------------------------------
15:04   git merge features/foo
15:03                                  git commit -m "Third commit"
15:02                                  git commit -m "Second commit"
15:01   git checkout -b features/foo
15:00   git commit -m "First commit"</code></pre>

<p>Result:</p>

<pre><code>* 142a74a - YYYY-MM-DD 15:03:00 (XX minutes ago) (HEAD -&gt; develop, features/foo)
|           Third commit - Christophe
* 00d848c - YYYY-MM-DD 15:02:00 (XX minutes ago)
|           Second commit - Christophe
* 298e9c5 - YYYY-MM-DD 15:00:00 (XX minutes ago)
            First commit - Christophe</code></pre>

<h3><code>git merge --no-ff</code></h3>

<p>Commands:</p>

<pre><code>Time           Branch "develop"              Branch "features/foo"
------- -------------------------------- -------------------------------
15:04   git merge --no-ff features/foo
15:03                                    git commit -m "Third commit"
15:02                                    git commit -m "Second commit"
15:01   git checkout -b features/foo
15:00   git commit -m "First commit"</code></pre>

<p>Result:</p>

<pre><code>*   1140d8c - YYYY-MM-DD 15:04:00 (XX minutes ago) (HEAD -&gt; develop)
|\            Merge branch 'features/foo' - Christophe
| * 69f4a7a - YYYY-MM-DD 15:03:00 (XX minutes ago) (features/foo)
| |           Third commit - Christophe
| * 2973183 - YYYY-MM-DD 15:02:00 (XX minutes ago)
|/            Second commit - Christophe
* c173472 - YYYY-MM-DD 15:00:00 (XX minutes ago)
            First commit - Christophe</code></pre>

<hr />

<h1><code>git merge</code> vs <code>git rebase</code></h1>

<p>First point: <strong>always merge features into develop, never rebase develop from features</strong>. This is a consequence of the <a href="https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing" target="_blank">Golden Rule of Rebasing</a>:</p>

<blockquote>
  <p>The golden rule of <code>git rebase</code> is to never use it on <em>public</em> branches.</p>
</blockquote>

<p><a href="https://git-scm.com/book/en/v2/Git-Branching-Rebasing" target="_blank">In other words</a>:</p>

<blockquote>
  <p>Never rebase anything you've pushed somewhere.</p>
</blockquote>

<p>I would personally add: <em>unless it's a feature branch AND you and your team are aware of the consequences</em>.</p>

<p>So the question of <code>git merge</code> vs <code>git rebase</code> applies almost only to the feature branches (in the following examples, <code>--no-ff</code> has always been used when merging). Note that since I'm not sure there's one better solution (<a href="https://www.atlassian.com/git/articles/git-team-workflows-merge-or-rebase" target="_blank">a debate exists</a>), I'll only provide how both commands behave. In my case, I prefer using <code>git rebase</code> as it produces a nicer history tree :)</p>

<h2>Between feature branches</h2>

<h3><code>git merge</code></h3>

<p>Commands:</p>

<pre><code>Time           Branch "develop"              Branch "features/foo"           Branch "features/bar"
------- -------------------------------- ------------------------------- --------------------------------
15:10   git merge --no-ff features/bar
15:09   git merge --no-ff features/foo
15:08                                                                    git commit -m "Sixth commit"
15:07                                                                    git merge --no-ff features/foo
15:06                                                                    git commit -m "Fifth commit"
15:05                                                                    git commit -m "Fourth commit"
15:04                                    git commit -m "Third commit"
15:03                                    git commit -m "Second commit"
15:02   git checkout -b features/bar
15:01   git checkout -b features/foo
15:00   git commit -m "First commit"</code></pre>

<p>Result:</p>

<pre><code>*   c0a3b89 - YYYY-MM-DD 15:10:00 (XX minutes ago) (HEAD -&gt; develop)
|\            Merge branch 'features/bar' - Christophe
| * 37e933e - YYYY-MM-DD 15:08:00 (XX minutes ago) (features/bar)
| |           Sixth commit - Christophe
| *   eb5e657 - YYYY-MM-DD 15:07:00 (XX minutes ago)
| |\            Merge branch 'features/foo' into features/bar - Christophe
| * | 2e4086f - YYYY-MM-DD 15:06:00 (XX minutes ago)
| | |           Fifth commit - Christophe
| * | 31e3a60 - YYYY-MM-DD 15:05:00 (XX minutes ago)
| | |           Fourth commit - Christophe
* | |   98b439f - YYYY-MM-DD 15:09:00 (XX minutes ago)
|\ \ \            Merge branch 'features/foo' - Christophe
| |/ /
|/| /
| |/
| * 6579c9c - YYYY-MM-DD 15:04:00 (XX minutes ago) (features/foo)
| |           Third commit - Christophe
| * 3f41d96 - YYYY-MM-DD 15:03:00 (XX minutes ago)
|/            Second commit - Christophe
* 14edc68 - YYYY-MM-DD 15:00:00 (XX minutes ago)
            First commit - Christophe</code></pre>

<h3><code>git rebase</code></h3>

<p>Commands:</p>

<pre><code>Time           Branch "develop"              Branch "features/foo"           Branch "features/bar"
------- -------------------------------- ------------------------------- -------------------------------
15:10   git merge --no-ff features/bar
15:09   git merge --no-ff features/foo
15:08                                                                    git commit -m "Sixth commit"
15:07                                                                    git rebase features/foo
15:06                                                                    git commit -m "Fifth commit"
15:05                                                                    git commit -m "Fourth commit"
15:04                                    git commit -m "Third commit"
15:03                                    git commit -m "Second commit"
15:02   git checkout -b features/bar
15:01   git checkout -b features/foo
15:00   git commit -m "First commit"</code></pre>

<p>Result:</p>

<pre><code>*   7a99663 - YYYY-MM-DD 15:10:00 (XX minutes ago) (HEAD -&gt; develop)
|\            Merge branch 'features/bar' - Christophe
| * 708347a - YYYY-MM-DD 15:08:00 (XX minutes ago) (features/bar)
| |           Sixth commit - Christophe
| * 949ae73 - YYYY-MM-DD 15:06:00 (XX minutes ago)
| |           Fifth commit - Christophe
| * 108b4c7 - YYYY-MM-DD 15:05:00 (XX minutes ago)
| |           Fourth commit - Christophe
* |   189de99 - YYYY-MM-DD 15:09:00 (XX minutes ago)
|\ \            Merge branch 'features/foo' - Christophe
| |/
| * 26835a0 - YYYY-MM-DD 15:04:00 (XX minutes ago) (features/foo)
| |           Third commit - Christophe
| * a61dd08 - YYYY-MM-DD 15:03:00 (XX minutes ago)
|/            Second commit - Christophe
* ae6f5fc - YYYY-MM-DD 15:00:00 (XX minutes ago)
            First commit - Christophe</code></pre>

<h2>From <code>develop</code> to a feature branch</h2>

<h3><code>git merge</code></h3>

<p>Commands:</p>

<pre><code>Time           Branch “develop"              Branch "features/foo"           Branch "features/bar"
------- -------------------------------- ------------------------------- -------------------------------
15:10   git merge --no-ff features/bar
15:09                                                                    git commit -m “Sixth commit"
15:08                                                                    git merge --no-ff development
15:07   git merge --no-ff features/foo
15:06                                                                    git commit -m “Fifth commit"
15:05                                                                    git commit -m “Fourth commit"
15:04                                    git commit -m “Third commit"
15:03                                    git commit -m “Second commit"
15:02   git checkout -b features/bar
15:01   git checkout -b features/foo
15:00   git commit -m “First commit"</code></pre>

<p>Result:</p>

<pre><code>*   9e6311a - YYYY-MM-DD 15:10:00 (XX minutes ago) (HEAD -&gt; develop)
|\            Merge branch 'features/bar' - Christophe
| * 3ce9128 - YYYY-MM-DD 15:09:00 (XX minutes ago) (features/bar)
| |           Sixth commit - Christophe
| *   d0cd244 - YYYY-MM-DD 15:08:00 (XX minutes ago)
| |\            Merge branch 'develop' into features/bar - Christophe
| |/
|/|
* |   5bd5f70 - YYYY-MM-DD 15:07:00 (XX minutes ago)
|\ \            Merge branch 'features/foo' - Christophe
| * | 4ef3853 - YYYY-MM-DD 15:04:00 (XX minutes ago) (features/foo)
| | |           Third commit - Christophe
| * | 3227253 - YYYY-MM-DD 15:03:00 (XX minutes ago)
|/ /            Second commit - Christophe
| * b5543a2 - YYYY-MM-DD 15:06:00 (XX minutes ago)
| |           Fifth commit - Christophe
| * 5e84b79 - YYYY-MM-DD 15:05:00 (XX minutes ago)
|/            Fourth commit - Christophe
* 2da6d8d - YYYY-MM-DD 15:00:00 (XX minutes ago)
            First commit - Christophe</code></pre>

<h3><code>git rebase</code></h3>

<p>Commands:</p>

<pre><code>Time           Branch “develop"              Branch "features/foo"           Branch "features/bar"
------- -------------------------------- ------------------------------- -------------------------------
15:10   git merge --no-ff features/bar
15:09                                                                    git commit -m “Sixth commit"
15:08                                                                    git rebase development
15:07   git merge --no-ff features/foo
15:06                                                                    git commit -m “Fifth commit"
15:05                                                                    git commit -m “Fourth commit"
15:04                                    git commit -m “Third commit"
15:03                                    git commit -m “Second commit"
15:02   git checkout -b features/bar
15:01   git checkout -b features/foo
15:00   git commit -m “First commit"</code></pre>

<p>Result:</p>

<pre><code>*   b0f6752 - YYYY-MM-DD 15:10:00 (XX minutes ago) (HEAD -&gt; develop)
|\            Merge branch 'features/bar' - Christophe
| * 621ad5b - YYYY-MM-DD 15:09:00 (XX minutes ago) (features/bar)
| |           Sixth commit - Christophe
| * 9cb1a16 - YYYY-MM-DD 15:06:00 (XX minutes ago)
| |           Fifth commit - Christophe
| * b8ddd19 - YYYY-MM-DD 15:05:00 (XX minutes ago)
|/            Fourth commit - Christophe
*   856433e - YYYY-MM-DD 15:07:00 (XX minutes ago)
|\            Merge branch 'features/foo' - Christophe
| * 694ac81 - YYYY-MM-DD 15:04:00 (XX minutes ago) (features/foo)
| |           Third commit - Christophe
| * 5fd94d3 - YYYY-MM-DD 15:03:00 (XX minutes ago)
|/            Second commit - Christophe
* d01d589 - YYYY-MM-DD 15:00:00 (XX minutes ago)
            First commit - Christophe</code></pre>

<hr />

<h1>Side notes</h1>

<h3><code>git cherry-pick</code></h3>

<p>When you just need one specific commit, <code>git cherry-pick</code> is a nice solution (the <code>-x</code> option appends a line that says "<em>(cherry picked from commit...)</em>" to the original commit message body, so it's usually a good idea to use it - <code>git log &lt;commit_sha1&gt;</code> to see it):</p>

<p>Commands:</p>

<pre><code>Time           Branch “develop"              Branch "features/foo"                Branch "features/bar"           
------- -------------------------------- ------------------------------- -----------------------------------------
15:10   git merge --no-ff features/bar                                                                            
15:09   git merge --no-ff features/foo                                                                            
15:08                                                                    git commit -m “Sixth commit"             
15:07                                                                    git cherry-pick -x &lt;second_commit_sha1&gt;  
15:06                                                                    git commit -m “Fifth commit"             
15:05                                                                    git commit -m “Fourth commit"            
15:04                                    git commit -m “Third commit"                                             
15:03                                    git commit -m “Second commit"                                            
15:02   git checkout -b features/bar                                                                              
15:01   git checkout -b features/foo                                                                              
15:00   git commit -m “First commit"                                                                              </code></pre>

<p>Result:</p>

<pre><code>*   50839cd - YYYY-MM-DD 15:10:00 (XX minutes ago) (HEAD -&gt; develop)
|\            Merge branch 'features/bar' - Christophe
| * 0cda99f - YYYY-MM-DD 15:08:00 (XX minutes ago) (features/bar)
| |           Sixth commit - Christophe
| * f7d6c47 - YYYY-MM-DD 15:03:00 (XX minutes ago)
| |           Second commit - Christophe
| * dd7d05a - YYYY-MM-DD 15:06:00 (XX minutes ago)
| |           Fifth commit - Christophe
| * d0d759b - YYYY-MM-DD 15:05:00 (XX minutes ago)
| |           Fourth commit - Christophe
* |   1a397c5 - YYYY-MM-DD 15:09:00 (XX minutes ago)
|\ \            Merge branch 'features/foo' - Christophe
| |/
|/|
| * 0600a72 - YYYY-MM-DD 15:04:00 (XX minutes ago) (features/foo)
| |           Third commit - Christophe
| * f4c127a - YYYY-MM-DD 15:03:00 (XX minutes ago)
|/            Second commit - Christophe
* 0cf894c - YYYY-MM-DD 15:00:00 (XX minutes ago)
            First commit - Christophe</code></pre>

<h3><code>git pull --rebase</code></h3>

<p>Not sure I can explain it better than <a href="https://www.derekgourlay.com/blog/git-when-to-merge-vs-when-to-rebase/" target="_blank">Derek Gourlay</a>... Basically, use <code>git pull --rebase</code> instead of <code>git pull</code> :) What's missing in the article though, is that <a href="https://coderwall.com/p/tnoiug/rebase-by-default-when-doing-git-pull" target="_blank">you can enable it by default</a>:</p>

<pre><code>git config --global pull.rebase true</code></pre>

<h3><code>git rerere</code></h3>

<p>Again, nicely explained <a href="https://git-scm.com/blog/2010/03/08/rerere.html" target="_blank">here</a>. But put simple, if you enable it, you won't have to resolve the same conflict multiple times anymore.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-46708899">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        20
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>While merging is definitely the easiest and most common way to integrate changes, it's not the only one: <strong><em>Rebase</em></strong> is an alternative means of integration.</p>

<p><strong>Understanding Merge a Little Better</strong></p>

<p>When Git performs a merge, it looks for three commits:</p>

<ul>
<li>(1) Common ancestor commit If you follow the history of two branches in a project, they always have at least one commit in common: at this point in time, both branches had the same content and then evolved differently.</li>
<li>(2) + (3) Endpoints of each branch The goal of an integration is to combine the current states of two branches. Therefore, their respective latest revisions are of special interest.
Combining these three commits will result in the integration we're aiming for.</li>
</ul>

<p><strong>Fast-Forward or Merge Commit</strong></p>

<p>In very simple cases, one of the two branches doesn't have any new commits since the branching happened - its latest commit is still the common ancestor.</p>

<p><a href="https://i.stack.imgur.com/57Wt0.gif" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/57Wt0.gif" alt="enter image description here" /></div></a></p>

<p>In this case, performing the integration is dead simple: Git can just add all the commits of the other branch on top of the common ancestor commit. In Git, this simplest form of integration is called a "fast-forward" merge. Both branches then share the exact same history.</p>

<p><a href="https://i.stack.imgur.com/f1VTv.gif" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/f1VTv.gif" alt="enter image description here" /></div></a></p>

<p>In a lot of cases, however, both branches moved forward individually.
<a href="https://i.stack.imgur.com/GlAgx.gif" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/GlAgx.gif" alt="enter image description here" /></div></a></p>

<p>To make an integration, Git will have to create a new commit that contains the differences between them - the merge commit.</p>

<p><a href="https://i.stack.imgur.com/e3xJE.gif" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/e3xJE.gif" alt="enter image description here" /></div></a></p>

<p><strong>Human Commits & Merge Commits</strong></p>

<p>Normally, a commit is carefully created by a human being. It's a meaningful unit that wraps only related changes and annotates them with a comment.</p>

<p>A merge commit is a bit different: instead of being created by a developer, it gets created automatically by Git. And instead of wrapping a set of related changes, its purpose is to connect two branches, just like a knot. If you want to understand a merge operation later, you need to take a look at the history of both branches and the corresponding commit graph.</p>

<p><strong>Integrating with Rebase</strong></p>

<p><em>Some people prefer to go without such automatic merge commits. Instead, they want the project's history to look as if it had evolved in a single, straight line.</em> No indication remains that it had been split into multiple branches at some point.</p>

<p><a href="https://i.stack.imgur.com/b1nud.gif" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/b1nud.gif" alt="enter image description here" /></div></a></p>

<p>Let's walk through a rebase operation step by step. The scenario is the same as in the previous examples: we want to integrate the changes from branch-B into branch-A, but now by using rebase.</p>

<p><a href="https://i.stack.imgur.com/Az5LO.gif" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/Az5LO.gif" alt="enter image description here" /></div></a></p>

<p>We will do this in three steps</p>

<ol>
<li><code>git rebase branch-A // syncs the history with branch-A</code></li>
<li><code>git checkout branch-A // change the current branch to branch-A</code></li>
<li><code>git merge branch-B // merge/take the changes from branch-B to branch-A</code> </li>
</ol>

<p>First, Git will "undo" all commits on branch-A that happened after the lines began to branch out (after the common ancestor commit). However, of course, it won't discard them: instead you can think of those commits as being "saved away temporarily".</p>

<p><a href="https://i.stack.imgur.com/To3Iq.gif" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/To3Iq.gif" alt="enter image description here" /></div></a></p>

<p>Next, it applies the commits from branch-B that we want to integrate. At this point, both branches look exactly the same.</p>

<p><a href="https://i.stack.imgur.com/Vrfmo.gif" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/Vrfmo.gif" alt="enter image description here" /></div></a></p>

<p>In the final step, the new commits on branch-A are now reapplied - but on a new position, on top of the integrated commits from branch-B (they are re-based).
<strong>The result looks like development had happened in a straight line. Instead of a merge commit that contains all the combined changes, the original commit structure was preserved.</strong></p>

<p><a href="https://i.stack.imgur.com/4IKL0.gif" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/4IKL0.gif" alt="enter image description here" /></div></a></p>

<p>Finally you get a clean branch <strong>branch-A</strong> with no unwanted and auto generated commits.</p>

<p><strong>Note:</strong> Taken from the awesome <a href="https://www.git-tower.com/learn/git/ebook/en/desktop-gui/advanced-topics/rebase" target="_blank">post</a> by <a href="https://www.git-tower.com/windows/" target="_blank"><code>git-tower</code></a>. The <em>disadvantages</em> of <code>rebase</code> is also a good read in the same post.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-48349481">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>When do I use <code>git rebase</code>? Almost never, because it rewrites history. <code>git merge</code> is almost always the preferable choice, because it respects what actually happened in your project. </p>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/git" title="show questions tagged 'git'" target="_blank">git</a> <a href="/questions/tagged/version-control" title="show questions tagged 'version-control'" target="_blank">version-control</a> <a href="/questions/tagged/git-merge" title="show questions tagged 'git-merge'" target="_blank">git-merge</a> <a href="/questions/tagged/git-rebase" title="show questions tagged 'git-rebase'" target="_blank">git-rebase</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
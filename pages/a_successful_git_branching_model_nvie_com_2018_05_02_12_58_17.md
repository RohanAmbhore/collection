<a href="http://nvie.com/posts/a-successful-git-branching-model/">http://nvie.com/posts/a-successful-git-branching-model/</a><div id="articleHeader"><h1>A successful Git branching model</h1></div>

      

  <div>
    
    By <a href="/about/" target="_blank">Vincent Driessen</a>
    on Tuesday, January 05, 2010
  </div>

  
    

    <p>In this post I present the development model that I’ve introduced for some of
my projects (both at work and private) about a year ago, and which has turned
out to be very successful. I’ve been meaning to write about it for a while now,
but I’ve never really found the time to do so thoroughly, until now. I won’t
talk about any of the projects’ details, merely about the branching strategy
and release management.</p>
<p><div class="readableLargeImageContainer"><img src="/img/git-model@2x.png"  /></div></p>
<h2 id="why-git">Why git? <a href="#why-git" target="_blank">¶</a></h2>
<p>For a thorough discussion on the pros and cons of Git compared to centralized
source code control systems, <a href="http://whygitisbetterthanx.com/" target="_blank">see</a> the
<a href="http://git.or.cz/gitwiki/GitSvnComparsion" target="_blank">web</a>. There are plenty of flame
wars going on there. As a developer, I prefer Git above all other tools around
today. Git really changed the way developers think of merging and branching.
From the classic CVS/Subversion world I came from, merging/branching has always
been considered a bit scary (“beware of merge conflicts, they bite you!”) and
something you only do every once in a while.</p>
<p>But with Git, these actions are extremely cheap and simple, and they are
considered one of the core parts of your <em>daily</em> workflow, really. For example,
in CVS/Subversion <a href="http://svnbook.red-bean.com" target="_blank">books</a>, branching and merging
is first discussed in the later chapters (for advanced users), while in
<a href="http://book.git-scm.com" target="_blank">every</a>
<a href="http://pragprog.com/titles/tsgit/pragmatic-version-control-using-git" target="_blank">Git</a>
<a href="http://github.com/progit/progit" target="_blank">book</a>, it’s already covered in chapter
3 (basics).</p>
<p>As a consequence of its simplicity and repetitive nature, branching and merging
are no longer something to be afraid of. Version control tools are supposed to
assist in branching/merging more than anything else.</p>
<p>Enough about the tools, let’s head onto the development model. The model that
I’m going to present here is essentially no more than a set of procedures that
every team member has to follow in order to come to a managed software
development process.</p>
<h2 id="decentralized-but-centralized">Decentralized but centralized <a href="#decentralized-but-centralized" target="_blank">¶</a></h2>
<p>The repository setup that we use and that works well with this branching model,
is that with a central “truth” repo. Note that this repo is only <em>considered</em>
to be the central one (since Git is a DVCS, there is no such thing as a central
repo at a technical level). We will refer to this repo as <code>origin</code>, since this
name is familiar to all Git users.</p>
<p><div class="readableLargeImageContainer"><img src="/img/centr-decentr@2x.png"  /></div></p>
<p>Each developer pulls and pushes to origin. But besides the centralized
push-pull relationships, each developer may also pull changes from other peers
to form sub teams. For example, this might be useful to work together with two
or more developers on a big new feature, before pushing the work in progress to
<code>origin</code> prematurely. In the figure above, there are subteams of Alice and Bob,
Alice and David, and Clair and David.</p>
<p>Technically, this means nothing more than that Alice has defined a Git remote,
named <code>bob</code>, pointing to Bob’s repository, and vice versa.</p>
<h2 id="the-main-branches">The main branches <a href="#the-main-branches" target="_blank">¶</a></h2>
<p><div class="readableLargeImageContainer"><img src="/img/main-branches@2x.png"  /></div></p>
<p>At the core, the development model is greatly inspired by existing models out
there. The central repo holds two main branches with an infinite lifetime:</p>
<ul>
<li><code>master</code></li>
<li><code>develop</code></li>
</ul>
<p>The <code>master</code> branch at <code>origin</code> should be familiar to every Git user. Parallel
to the <code>master</code> branch, another branch exists called <code>develop</code>.</p>
<p>We consider <code>origin/master</code> to be the main branch where the source code of
<code>HEAD</code> always reflects a <em>production-ready</em> state.</p>
<p>We consider <code>origin/develop</code> to be the main branch where the source code of
<code>HEAD</code> always reflects a state with the latest delivered development changes
for the next release. Some would call this the “integration branch”.  This is
where any automatic nightly builds are built from.</p>
<p>When the source code in the <code>develop</code> branch reaches a stable point and is
ready to be released, all of the changes should be merged back into <code>master</code>
somehow and then tagged with a release number. How this is done in detail will
be discussed further on.</p>
<p>Therefore, each time when changes are merged back into <code>master</code>, this is a new
production release <em>by definition</em>. We tend to be very strict at this, so that
theoretically, we could use a Git hook script to automatically build and
roll-out our software to our production servers everytime there was a commit on
<code>master</code>.</p>
<h2 id="supporting-branches">Supporting branches <a href="#supporting-branches" target="_blank">¶</a></h2>
<p>Next to the main branches <code>master</code> and <code>develop</code>, our development model uses
a variety of supporting branches to aid parallel development between team
members, ease tracking of features, prepare for production releases and to
assist in quickly fixing live production problems. Unlike the main branches,
these branches always have a limited life time, since they will be removed
eventually.</p>
<p>The different types of branches we may use are:</p>
<ul>
<li>Feature branches</li>
<li>Release branches</li>
<li>Hotfix branches</li>
</ul>
<p>Each of these branches have a specific purpose and are bound to strict rules as
to which branches may be their originating branch and which branches must be
their merge targets. We will walk through them in a minute.</p>
<p>By no means are these branches “special” from a technical perspective.  The
branch types are categorized by how we <em>use</em> them. They are of course plain old
Git branches.</p>
<h3 id="feature-branches">Feature branches <a href="#feature-branches" target="_blank">¶</a></h3>
<p><img src="/img/fb@2x.png" width="133" /></p>
<dl>
<dt>May branch off from:</dt>
<dd><code>develop</code>  </dd>
<dt>Must merge back into:</dt>
<dd><code>develop</code>  </dd>
<dt>Branch naming convention:</dt>
<dd>anything except <code>master</code>, <code>develop</code>, <code>release-*</code>, or <code>hotfix-*</code></dd>
</dl>
<p>Feature branches (or sometimes called topic branches) are used to develop new
features for the upcoming or a distant future release. When starting
development of a feature, the target release in which this feature will be
incorporated may well be unknown at that point. The essence of a feature branch
is that it exists as long as the feature is in development, but will eventually
be merged back into <code>develop</code> (to definitely add the new feature to the
upcoming release) or discarded (in case of a disappointing experiment).</p>
<p>Feature branches typically exist in developer repos only, not in <code>origin</code>.</p>
<h4 id="creating-a-feature-branch">Creating a feature branch <a href="#creating-a-feature-branch" target="_blank">¶</a></h4>
<p>When starting work on a new feature, branch off from the <code>develop</code> branch.</p>
<div><pre>$ git checkout -b myfeature develop
Switched to a new branch "myfeature"
</pre></div>


<h4 id="incorporating-a-finished-feature-on-develop">Incorporating a finished feature on develop <a href="#incorporating-a-finished-feature-on-develop" target="_blank">¶</a></h4>
<p>Finished features may be merged into the <code>develop</code> branch to definitely add
them to the upcoming release:</p>
<div><pre>$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff myfeature
Updating ea1b82a..05e9557
(Summary of changes)
$ git branch -d myfeature
Deleted branch myfeature (was 05e9557).
$ git push origin develop
</pre></div>


<p>The <code>--no-ff</code> flag causes the merge to always create a new commit object, even
if the merge could be performed with a fast-forward. This avoids losing
information about the historical existence of a feature branch and groups
together all commits that together added the feature. Compare:</p>
<p><div class="readableLargeImageContainer"><img src="/img/merge-without-ff@2x.png"  /></div></p>
<p>In the latter case, it is impossible to see from the Git history which of the
commit objects together have implemented a feature—you would have to manually
read all the log messages. Reverting a whole feature (i.e. a group of commits),
is a true headache in the latter situation, whereas it is easily done if the
<code>--no-ff</code> flag was used.</p>
<p>Yes, it will create a few more (empty) commit objects, but the gain is much
bigger than the cost.</p>
<h3 id="release-branches">Release branches <a href="#release-branches" target="_blank">¶</a></h3>
<dl>
<dt>May branch off from:</dt>
<dd><code>develop</code></dd>
<dt>Must merge back into:</dt>
<dd><code>develop</code> and <code>master</code></dd>
<dt>Branch naming convention:</dt>
<dd><code>release-*</code></dd>
</dl>
<p>Release branches support preparation of a new production release. They allow
for last-minute dotting of i’s and crossing t’s. Furthermore, they allow for
minor bug fixes and preparing meta-data for a release (version number, build
dates, etc.). By doing all of this work on a release branch, the <code>develop</code>
branch is cleared to receive features for the next big release.</p>
<p>The key moment to branch off a new release branch from <code>develop</code> is when
develop (almost) reflects the desired state of the new release. At least all
features that are targeted for the release-to-be-built must be merged in to
<code>develop</code> at this point in time. All features targeted at future releases may
not—they must wait until after the release branch is branched off.</p>
<p>It is exactly at the start of a release branch that the upcoming release gets
assigned a version number—not any earlier. Up until that moment, the <code>develop</code>
branch reflected changes for the “next release”, but it is unclear whether that
“next release” will eventually become 0.3 or 1.0, until the release branch is
started. That decision is made on the start of the release branch and is
carried out by the project’s rules on version number bumping.</p>
<h4 id="creating-a-release-branch">Creating a release branch <a href="#creating-a-release-branch" target="_blank">¶</a></h4>
<p>Release branches are created from the <code>develop</code> branch. For example, say
version 1.1.5 is the current production release and we have a big release
coming up. The state of <code>develop</code> is ready for the “next release” and we have
decided that this will become version 1.2 (rather than 1.1.6 or 2.0). So we
branch off and give the release branch a name reflecting the new version
number:</p>
<div><pre>$ git checkout -b release-1.2 develop
Switched to a new branch "release-1.2"
$ ./bump-version.sh 1.2
Files modified successfully, version bumped to 1.2.
$ git commit -a -m "Bumped version number to 1.2"
[release-1.2 74d9424] Bumped version number to 1.2
1 files changed, 1 insertions(+), 1 deletions(-)
</pre></div>


<p>After creating a new branch and switching to it, we bump the version number.
Here, <code>bump-version.sh</code> is a fictional shell script that changes some files in
the working copy to reflect the new version. (This can of course be a manual
change—the point being that <em>some</em> files change.) Then, the bumped version
number is committed.</p>
<p>This new branch may exist there for a while, until the release may be rolled
out definitely. During that time, bug fixes may be applied in this branch
(rather than on the <code>develop</code> branch). Adding large new features here is
strictly prohibited. They must be merged into <code>develop</code>, and therefore, wait
for the next big release.</p>
<h4 id="finishing-a-release-branch">Finishing a release branch <a href="#finishing-a-release-branch" target="_blank">¶</a></h4>
<p>When the state of the release branch is ready to become a real release, some
actions need to be carried out. First, the release branch is merged into
<code>master</code> (since every commit on <code>master</code> is a new release <em>by definition</em>,
remember). Next, that commit on <code>master</code> must be tagged for easy future
reference to this historical version. Finally, the changes made on the release
branch need to be merged back into <code>develop</code>, so that future releases also
contain these bug fixes.</p>
<p>The first two steps in Git:</p>
<div><pre>$ git checkout master
Switched to branch 'master'
$ git merge --no-ff release-1.2
Merge made by recursive.
(Summary of changes)
$ git tag -a 1.2
</pre></div>


<p>The release is now done, and tagged for future reference.  </p>
<blockquote>
<p><strong>Edit:</strong> You might as well want to use the <code>-s</code> or <code>-u &lt;key&gt;</code> flags to sign
your tag cryptographically.</p>
</blockquote>
<p>To keep the changes made in the release branch, we need to merge those back
into <code>develop</code>, though. In Git:</p>
<div><pre>$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff release-1.2
Merge made by recursive.
(Summary of changes)
</pre></div>


<p>This step may well lead to a merge conflict (probably even, since we have
changed the version number). If so, fix it and commit.</p>
<p>Now we are really done and the release branch may be removed, since we don’t
need it anymore:</p>
<div><pre>$ git branch -d release-1.2
Deleted branch release-1.2 (was ff452fe).
</pre></div>


<h3 id="hotfix-branches">Hotfix branches <a href="#hotfix-branches" target="_blank">¶</a></h3>
<p><div class="readableLargeImageContainer"><img src="/img/hotfix-branches@2x.png"  /></div></p>
<dl>
<dt>May branch off from:</dt>
<dd><code>master</code></dd>
<dt>Must merge back into:</dt>
<dd><code>develop</code> and <code>master</code></dd>
<dt>Branch naming convention:</dt>
<dd><code>hotfix-*</code></dd>
</dl>
<p>Hotfix branches are very much like release branches in that they are also meant
to prepare for a new production release, albeit unplanned. They arise from the
necessity to act immediately upon an undesired state of a live production
version. When a critical bug in a production version must be resolved
immediately, a hotfix branch may be branched off from the corresponding tag on
the master branch that marks the production version.</p>
<p>The essence is that work of team members (on the <code>develop</code> branch) can
continue, while another person is preparing a quick production fix.</p>
<h4 id="creating-the-hotfix-branch">Creating the hotfix branch <a href="#creating-the-hotfix-branch" target="_blank">¶</a></h4>
<p>Hotfix branches are created from the <code>master</code> branch. For example, say version
1.2 is the current production release running live and causing troubles due to
a severe bug. But changes on <code>develop</code> are yet unstable. We may then branch off
a hotfix branch and start fixing the problem:</p>
<div><pre>$ git checkout -b hotfix-1.2.1 master
Switched to a new branch "hotfix-1.2.1"
$ ./bump-version.sh 1.2.1
Files modified successfully, version bumped to 1.2.1.
$ git commit -a -m "Bumped version number to 1.2.1"
[hotfix-1.2.1 41e61bb] Bumped version number to 1.2.1
1 files changed, 1 insertions(+), 1 deletions(-)
</pre></div>


<p>Don’t forget to bump the version number after branching off!</p>
<p>Then, fix the bug and commit the fix in one or more separate commits.</p>
<div><pre>$ git commit -m "Fixed severe production problem"
[hotfix-1.2.1 abbe5d6] Fixed severe production problem
5 files changed, 32 insertions(+), 17 deletions(-)
</pre></div>


<p><strong>Finishing a hotfix branch</strong></p>
<p>When finished, the bugfix needs to be merged back into <code>master</code>, but also needs
to be merged back into <code>develop</code>, in order to safeguard that the bugfix is
included in the next release as well. This is completely similar to how release
branches are finished.</p>
<p>First, update <code>master</code> and tag the release.</p>
<div><pre>$ git checkout master
Switched to branch 'master'
$ git merge --no-ff hotfix-1.2.1
Merge made by recursive.
(Summary of changes)
$ git tag -a 1.2.1
</pre></div>


<p><strong>Edit:</strong> You might as well want to use the <code>-s</code> or <code>-u &lt;key&gt;</code> flags to sign
your tag cryptographically.</p>
<p>Next, include the bugfix in <code>develop</code>, too:</p>
<div><pre>$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff hotfix-1.2.1
Merge made by recursive.
(Summary of changes)
</pre></div>


<p>The one exception to the rule here is that, <strong>when a release branch currently
exists, the hotfix changes need to be merged into that release branch, instead
of <code>develop</code></strong>. Back-merging the bugfix into the release branch will eventually
result in the bugfix being merged into <code>develop</code> too, when the release branch
is finished. (If work in <code>develop</code> immediately requires this bugfix and cannot
wait for the release branch to be finished, you may safely merge the bugfix
into <code>develop</code> now already as well.)</p>
<p>Finally, remove the temporary branch:</p>
<div><pre>$ git branch -d hotfix-1.2.1
Deleted branch hotfix-1.2.1 (was abbe5d6).
</pre></div>


<h2 id="summary">Summary <a href="#summary" target="_blank">¶</a></h2>
<p>While there is nothing really shocking new to this branching model, the “big
picture” figure that this post began with has turned out to be tremendously
useful in our projects. It forms an elegant mental model that is easy to
comprehend and allows team members to develop a shared understanding of the
branching and releasing processes.</p>
<p>A high-quality PDF version of the figure is provided here. Go ahead and hang it
on the wall for quick reference at any time.</p>
<p><strong>Update:</strong> And for anyone who requested it: here’s the
<a href="http://github.com/downloads/nvie/gitflow/Git-branching-model-src.key.zip" target="_blank">gitflow-model.src.key</a> of the main diagram image (Apple Keynote).</p>
<p>
<a href="/files/Git-branching-model.pdf" target="_blank">Git-branching-model.pdf</a></p>
  
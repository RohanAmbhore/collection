<a href="https://www.derekgourlay.com/blog/git-when-to-merge-vs-when-to-rebase/">https://www.derekgourlay.com/blog/git-when-to-merge-vs-when-to-rebase/</a><div id="articleHeader"><h1>Git - When to Merge vs. When to Rebase</h1></div>
      <footer>
        
        
          <img src="https://www.derekgourlay.com/images/bio-photo-dg.jpg" alt="Derek Gourlay bio photo" />
        
        By Derek Gourlay
        <time> February 15, 2016</time>
        
        
        
        
      </footer>
      <div>
        <p>Does this (messy) branch history look familiar to you?</p>

<figure>
	<div class="readableLargeImageContainer"><img src="/images/merge_commits.png" alt="image" /></div>
	<figcaption>Holly merge-commits batman.</figcaption>
</figure>

<p>Keeping a clean history in git comes down to knowing when to use merge vs. rebase.  Great quote describing when to use each:</p>

<blockquote>
  <p>Rebases are how changes should pass from the top of hierarchy downwards and merges are how they flow back upwards.</p>
</blockquote>

<h3 id="rule-of-thumb">Rule of thumb:</h3>
<ul>
  <li>When pulling changes from origin/develop onto your local develop  use rebase.</li>
  <li>When finishing a feature branch merge the changes back to develop.</li>
</ul>

<h3 id="use--span-stylecolor-f14e32git-pull---rebasespan-when-pulling-changes-from--span-stylecolor-209098originspan">Use  git pull --rebase when pulling changes from  origin</h3>

<h3 id="difference-between-span-stylecolor-f14e32git-pullspan--span-stylecolor-f14e32git-pull---rebasespan">Difference between git pull & git pull --rebase:</h3>
<p><strong>Situation #1:</strong> You haven’t made any changes to your local develop branch and you want to pull changes from origin/develop.</p>

<p>In this case, git pull and git pull --rebase will produce the same results.  No problems.</p>

<p><strong>Situation #2:</strong> You’ve got one or two small changes of your own on your local develop branch that have not yet been pushed.  You want to pull any changes you are missing from  origin/develop to your local  develop before you can push.</p>

<figure><pre><code>                     origin/develop
                       |
         +−−−− (E)−−−−(F)
        /                 
(A) −− (B)−−−−−−− (C) −− (D)  
                          |          
                        develop</code></pre></figure>

<p>A regular git pull will often result in the following:</p>

<figure><pre><code>                 origin/develop
                       |        
         +−−−− (E)−−−−(F)−−−−−−−−−−−−−−−−
        /                                \
(A) −− (B) −−−−−−−−(C) −− (D)−−−−(G − merge commit)  
                                          |          
                                        develop </code></pre></figure>

<p>Unfortunately you no longer have a linear commit history.  And after pushing your git history looks like:</p>

<figure><pre><code>         +−−−− (E)−−−−(F)−−−−−−−−−−−−−−−−
        /                                \
(A) −− (B) −−−−−−−−(C) −− (D)−−−−(G − merge commit)  
                                          |          
                                        develop 
                                          |
                                   origin/develop</code></pre></figure>

<p><strong>Instead</strong> use git pull –rebase:</p>

<figure><pre><code>(A) −− (B)−−−−−−− (E) −− (F) −−−−−−− (C') −− (D') 
                          |                   |
                    origin/develop         develop</code></pre></figure>

<p>During the rebase your local commits C & D are played in order on top of the changes you pulled from origin/develop. These commits are replaced with C’ & D’ as you solve local conflicts one commit at a time when they are replayed.
Now pushing to origin/develop results in a fast-forward and a nice clean git history:</p>

<figure><pre><code>(A) −− (B)−−−−−−− (E) −− (F) −−−−−−− (C') −− (D') 
                                              |
                                           develop  
                                              |
                                        origin/develop</code></pre></figure>

<p>Use git merge  when finishing off a feature branch.</p>

<p>Example of merging a feature branch back into develop before pushing:</p>

<figure><pre><code>                 origin/develop                       develop
                       |                                 |        
         +−−−− (C)−−−−(D)−−−−−−−−−−−(H − Merging completed Feature for TMS−123)−−−−−
        /                           /      
(A) −− (B) −−−−−−−−(E) −− (F)−−−−(G)  
                                  |          
                         feature/TMS−123/myCoolFeature</code></pre></figure>

<p>After pushing to origin:</p>

<figure><pre><code>                                                   origin/develop 
                                                          |
                                                       develop
                                                         |        
         +−−−− (C)−−−−(D)−−−−−−−−−−−(H − Merging completed Feature for TMS−123)−−−−−
        /                           /      
(A) −− (B) −−−−−−−−(E) −− (F)−−−−(G)  
                                  |          
                         feature/TMS−123/myCoolFeature</code></pre></figure>

<h3 id="hold-on-span-stylecolor-f14e32git-pull---rebasespan-isnt-all-gravy">Hold on, git pull --rebase isn’t all gravy!</h3>

<p>While it is possible to set your system to default to git pull --rebase over using the regular git pull you will occasionally find you run into problems such as the following scenario:</p>

<p>You slave away working on a local feature branch and finish it off by merging it back into develop (using the --no-ff flag of course) resulting in the same history as the previous example:</p>

<figure><pre><code>                                                   origin/develop 
                                                         |
                                                       develop
                                                         |        
         +−−−− (C)−−−−(D)−−−−−−−−−−−(H − Merging completed Feature for TMS−123)−−−−−
        /                           /      
(A) −− (B) −−−−−−−−(E) −− (F)−−−−(G)  
                                  |          
                         feature/TMS−123/myCoolFeature</code></pre></figure>

<p>However after running git fetch you notice that origin/develop is 2 commits of head of develop:</p>

<figure><pre><code>                                                       develop                        origin/develop
                                                         |                                  |
         +−−−− (C)−−−−(D)−−−−−−−−−−−(H − Merging completed Feature for TMS−123)−−−−−(I)−−−−(J)
        /                           /      
(A) −− (B) −−−−−−−−(E)−−−−(F)−−−−(G)  
                                  |          
                         feature/TMS−123/myCoolFeature</code></pre></figure>

<p>You run git pull –rebase as told and all of a sudden something strange has happened:</p>

<figure><pre><code>(A) −− (B) −−−−−−(C)−−−(D)−−−−(I)−−−−(J)−−−−(E')−−−−−(F')−−−−−(G')−−−−  
        \                             |                        |         
         \                      origin/develop             develop
          \
            −−−−−−−−(E)−−−−(F)−−−−(G) 
                                   |          
                          feature/TMS−123/myCoolFeature</code></pre></figure>

<p>Your merge commit has disappeared!</p>

<p>What we really wanted was:</p>

<figure><pre><code>                                    origin/develop                 develop  
                                         |                           |          
         +−−−− (C)−−−−(D)−−−−−−−(I)−−−−−(J)−−−−−−−−(H' − Merging completed Feature for TMS−123)
        /                                                        /      
(A) −− (B) −−−−−−−−(E)−−−−(F)−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−(G)  
                                                                |          
                                                 feature/TMS−123/myCoolFeature</code></pre></figure>

<p>The problem is…</p>

<h3 id="rebasing-deletes-merge-commits">Rebasing Deletes Merge Commits!</h3>
<hr />

<h3 id="welcome-the-span-stylecolor-f14e32--preserve-mergesspan-flag-to-center-stage">Welcome the –preserve-merges flag to center stage:</h3>

<p>From the git-rebase manpage:</p>

<figure><pre><code>−p, −−preserve−merges
           Instead of ignoring merges, try to recreate them.
           This uses the −−interactive machinery internally, 
           but combining it with the −−interactive option explicitly 
           is generally not a good idea unless you know what you are 
           doing (see BUGS below).</code></pre></figure>

<p>So, instead of using git pull –rebase, use:</p>

<h3 id="span-stylecolor-f14e32git-fetchspan-span-stylecolor-209098originspan-and-span-stylecolor-f14e32git-rebase--pspan-span-stylecolor-209098origindevelopspan">git fetch origin and git rebase -p origin/develop</h3>

<hr />

<p>Downsides to git rebase -p:</p>

<p><strong>Git pull is dead!</strong></p>

<p>Unfortunately the -p flag cannot be used in conjunction with git pull ( git pull –rebase -p doesn’t work!) and as a result you have to explicitly fetch & rebase changes from origin.</p>

<p><strong>ORIG_HEAD is no longer preserved</strong></p>

<figure>
	<div class="readableLargeImageContainer"><img src="/images/finn_upset.png" alt="image" /></div>
</figure>

<p>ORIG_HEAD can be quite handy for multiple scenarios (If you want to review all changes you’ve just merged: git log -p –reverse ORIG_HEAD).  Unfortunately, git rebase -p sets ORIG_HEAD for each commit being rebased.</p>

<p>(Check out <a href="https://plus.google.com/111049168280159033135/posts/Xmycxn7VwHV" target="_blank">this google+ conversation</a> for more tips RE: how to use ORIG_HEAD)</p>

<p><strong>Branch tracking is not used</strong></p>

<p>Unlike git pull –rebase, which will fetch changes from the branch your current branch is tracking, git rebase -p doesn’t have a sensible default to work from. You have to give it a branch to rebase from (which is why we specify origin/develop in the above example).</p>
<hr />

<h2 id="conclusion">Conclusion</h2>

<p>To avoid messy merge commits and help keep a relatively clean git commit history use the following workflow when fetching upstream changes:</p>

<h3 id="span-stylecolor-f14e32git-fetchspan-span-stylecolor-209098originspan">git fetch origin</h3>

<h3 id="span-stylecolor-f14e32git-rebase-pspan-span-stylecolor-209098origindevelopspan">git rebase −p origin/develop</h3>

<p>For further reading about the inner workings of Git, I found the Git Internals section of the <a href="http://www.amazon.com/Pro-Git-Scott-Chacon/dp/1484200772" target="_blank">Pro Git</a> book very helpful!</p>


        
      
    
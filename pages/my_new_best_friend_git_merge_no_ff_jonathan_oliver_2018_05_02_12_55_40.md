<a href="http://blog.jonathanoliver.com/my-new-best-friend-git-merge-no-ff/">http://blog.jonathanoliver.com/my-new-best-friend-git-merge-no-ff/</a><div id="articleHeader"><h1>My New Best Friend: git merge  --no-ff</h1></div>
        

        <section>
        
          <time>
            Aug 31, 2011
          </time>
        
         
        </section>
    </header>

    
      <p>I've been using Git now for several years. Over a year ago I bumped into a great article about <a href="http://nvie.com/posts/a-successful-git-branching-model/" target="_blank">A Successful Git Branching Model</a>. It's a great article in its own right and deserves your attention if you're using Git. If you're not using Git, you'd better be using some form of distributed version control. If you're not…well…I digress.</p>  <p>One of the things about Git that I never worried about too much was leveraging branches for various work items. Instead, I'd often just do my work on my own local copy and use master. Then, when I'd go to push, I'd first pull in changes, rebase, and push. (There's another great article on <a href="http://paul.stadig.name/2010/12/thou-shalt-not-lie-git-rebase-ammend.html" target="_blank">why rebase is bad</a>.) The thing about rebase and merge is that they creates a single "branch" that is long and all of the work that you performed for a particular work item or bug or whatever gets lost in the single master branch. Enter "git merge –no-ff".</p>  <p>The "no-ff" stands for "no fast forward". The whole idea is that each time you do something, you to keep its identity and know that it came as a result of a particular bug. If you merge and you do so by fast forwarding, that context has been lost. But by appending "--no-ff" onto the merge command, you'll retain the context and the merge is maintained. Of course the end result in terms of the source code is the same, but we <em>know how we got there</em>. Kind of like event sourcing, huh?</p>  <p>If there's anything you guys know about me, it's that context is king. Without it, we're lost because we can't tell the forest from the trees. That's why from now on, I'm going to be doing lots of merging but without fast forwarding.</p>

    
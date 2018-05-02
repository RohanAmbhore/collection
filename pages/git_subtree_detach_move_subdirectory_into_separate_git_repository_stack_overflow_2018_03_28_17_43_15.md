<a href="https://stackoverflow.com/questions/359424/detach-move-subdirectory-into-separate-git-repository">https://stackoverflow.com/questions/359424/detach-move-subdirectory-into-separate-git-repository</a><div id="articleHeader"><h1>Detach (move) subdirectory into separate Git repository</h1></div>

            

<div id="question">

    
        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        1564
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>1062</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I have a <a href="http://en.wikipedia.org/wiki/Git_%28software%29" target="_blank">Git</a> repository which contains a number of subdirectories. Now I have found that one of the subdirectories is unrelated to the other and should be detached to a separate repository.</p>

<p>How can I do this while keeping the history of the files within the subdirectory?</p>

<p>I guess I could make a clone and remove the unwanted parts of each clone, but I suppose this would give me the complete tree when checking out an older revision etc. This might be acceptable, but I would prefer to be able to pretend that the two repositories doesn't have a shared history.</p>

<p>Just to make it clear, I have the following structure:</p>

<pre><code>XYZ/
    .git/
    XY1/
    ABC/
    XY2/
</code></pre>

<p>But I would like this instead:</p>

<pre><code>XYZ/
    .git/
    XY1/
    XY2/
ABC/
    .git/
    ABC/
</code></pre>
    </div>
    
    
</div>

                        <div>
                <div>
        <h2>                    <b>protected</b> by <a href="/users/1586880/lifetimes" target="_blank">lifetimes</a> Jun 30 '13 at 0:11
</h2>
        <p>
This question is protected to prevent "thanks!", "me too!", or spam answers by new users. 
To answer it, you must have earned at least 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).</p>
    </div>
            </div>
    
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-359759">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1148
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p><strong>Update</strong>: This process is so common, that the git team made it much simpler with a new tool, <code>git subtree</code>. See here: <a href="https://stackoverflow.com/questions/359424/detach-subdirectory-into-separate-git-repository/17864475#17864475" target="_blank">Detach (move) subdirectory into separate Git repository</a></p>

<hr />

<p>You want to clone your repository and then use <code>git filter-branch</code> to mark everything but the subdirectory you want in your new repo to be garbage-collected.</p>

<ol>
<li><p>To clone your local repository:</p>

<pre><code>git clone /XYZ /ABC
</code></pre>

<p>(Note: the repository will be cloned using hard-links, but that is not a problem since the hard-linked files will not be modified in themselves - new ones will be created.)</p></li>
<li><p>Now, let us preserve the interesting branches which we want to rewrite as well, and then remove the origin to avoid pushing there and to make sure that old commits will not be referenced by the origin:</p>

<pre><code>cd /ABC
for i in branch1 br2 br3; do git branch -t $i origin/$i; done
git remote rm origin
</code></pre>

<p>or for all remote branches:</p>

<pre><code>cd /ABC
for i in $(git branch -r | sed "s/.*origin\///"); do git branch -t $i origin/$i; done
git remote rm origin
</code></pre></li>
<li><p>Now you might want to also remove tags which have no relation with the subproject; you can also do that later, but you might need to prune your repo again. I did not do so and got a <code>WARNING: Ref 'refs/tags/v0.1' is unchanged</code> for all tags (since they were all unrelated to the subproject); additionally, after removing such tags more space will be reclaimed. Apparently <code>git filter-branch</code> should be able to rewrite other tags, but I could not verify this. If you want to remove all tags, use <code>git tag -l | xargs git tag -d</code>.</p></li>
<li><p>Then use filter-branch and reset to exclude the other files, so they can be pruned. Let's also add <code>--tag-name-filter cat --prune-empty</code> to remove empty commits and to rewrite tags (note that this will have to strip their signature):</p>

<pre><code>git filter-branch --tag-name-filter cat --prune-empty --subdirectory-filter ABC -- --all
</code></pre>

<p>or alternatively, to only rewrite the HEAD branch and ignore tags and other branches:</p>

<pre><code>git filter-branch --tag-name-filter cat --prune-empty --subdirectory-filter ABC HEAD
</code></pre></li>
<li><p>Then delete the backup reflogs so the space can be truly reclaimed (although now the operation is destructive)</p>

<pre><code>git reset --hard
git for-each-ref --format="%(refname)" refs/original/ | xargs -n 1 git update-ref -d
git reflog expire --expire=now --all
git gc --aggressive --prune=now
</code></pre>

<p>and now you have a local git repository of the ABC sub-directory with all its history preserved. </p></li>
</ol>

<p>Note: For most uses, <code>git filter-branch</code> should indeed have the added parameter <code>-- --all</code>. Yes that's really dash dash space dash dash <code>all</code>.  This needs to be the last parameters for the command. As Matli discovered, this keeps the project branches and tags included in the new repo.</p>

<p>Edit: various suggestions from comments below were incorporated to make sure, for instance, that the repository is actually shrunk (which was not always the case before).</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-955793">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        132
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><a href="https://stackoverflow.com/a/359759/42473" target="_blank">Paul's answer</a> creates a new repository containing /ABC, but does not remove /ABC from within /XYZ.  The following command will remove /ABC from within /XYZ:</p>

<pre><code>git filter-branch --tree-filter "rm -rf ABC" --prune-empty HEAD
</code></pre>

<p>Of course, test it in a 'clone --no-hardlinks' repository first, and follow it with the reset, gc and prune commands Paul lists.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-984775">
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
<p>You might need something like "git reflog expire --expire=now --all" before the garbage collection to actually clean the files out. git filter-branch just removes references in the history, but doesn't remove the reflog entries that hold the data. Of course, test this first.</p>

<p>My disk usage dropped dramatically in doing this, though my initial conditions were somewhat different. Perhaps --subdirectory-filter negates this need, but I doubt it.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-1181785">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>To add to <a href="https://stackoverflow.com/a/359759/42473" target="_blank">Paul's answer</a>, I found that to ultimately recover space, I have to push HEAD to a clean repository and that trims down the size of the .git/objects/pack directory.</p>



<pre>$ mkdir ...ABC.git
$ cd ...ABC.git
$ git init --bare
</pre>

<p>After the gc prune, also do:</p>

<pre>$ git push ...ABC.git HEAD
</pre>

<p>Then you can do</p>

<pre>$ git clone ...ABC.git
</pre>

<p>and the size of ABC/.git is reduced</p>

<p>Actually, some of the time consuming steps (e.g. git gc) aren't needed with the push to clean repository, i.e.:</p>

<pre>$ git clone --no-hardlinks /XYZ /ABC
$ git filter-branch --subdirectory-filter ABC HEAD
$ git reset --hard
$ git push ...ABC.git HEAD
</pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-1591174">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        94
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I’ve found that in order to properly delete the old history from the new repository, you have to do a little more work after the <code>filter-branch</code> step.</p>

<ol>
<li><p>Do the clone and the filter:</p>

<pre><code>git clone --no-hardlinks foo bar; cd bar
git filter-branch --subdirectory-filter subdir/you/want
</code></pre></li>
<li><p>Remove every reference to the old history. “origin” was keeping track of your clone, and “original” is where filter-branch saves the old stuff:</p>

<pre><code>git remote rm origin
git update-ref -d refs/original/refs/heads/master
git reflog expire --expire=now --all
</code></pre></li>
<li><p>Even now, your history might be stuck in a packfile that fsck won’t touch. Tear it to shreds, creating a new packfile and deleting the unused objects:</p>

<pre><code>git repack -ad
</code></pre></li>
</ol>

<p>There is <a href="http://git.kernel.org/?p=git/git.git;a=commitdiff;h=d0268de6d755c72ff375ec95a0cc0dbd99dc31e2" target="_blank">an explanation of this</a> in the <a href="http://git-scm.com/docs/git-filter-branch#_checklist_for_shrinking_a_repository" target="_blank">manual for filter-branch</a>.</p>
    </div>
    
</div>
    
        </div>
</div>

  



  

<div id="answer-4039311">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Use this filter command to remove a subdirectory, while preserving your tags and branches:</p>

<pre><code>git filter-branch --index-filter \
"git rm -r -f --cached --ignore-unmatch DIR" --prune-empty \
--tag-name-filter cat -- --all</code></pre>
    </div>
    <div>
    
    <div>
<div>
    <div>
        <a href="/posts/4039311/revisions" title="show all edits to this post" target="_blank">edited May 26 '14 at 14:51</a>
    </div>
    
    
</div>    </div>
            


    <div>
       

    <div>
    <div>
        answered Oct 28 '10 at 2:36
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-6295550">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        38
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><em>Edit: Bash script added.</em></p>

<p>The answers given here worked just partially for me; Lots of big files remained in the cache. What finally worked (after hours in #git on freenode):</p>

<pre><code>git clone --no-hardlinks file:///SOURCE /tmp/blubb
cd blubb
git filter-branch --subdirectory-filter ./PATH_TO_EXTRACT  --prune-empty --tag-name-filter cat -- --all
git clone file:///tmp/blubb/ /tmp/blooh
cd /tmp/blooh
git reflog expire --expire=now --all
git repack -ad
git gc --prune=now
</code></pre>

<p>With the previous solutions, the repository size was around 100 MB. This one brought it down to 1.7 MB. Maybe it helps somebody :)</p>

<hr />

<p>The following bash script automates the task:</p>

<pre><code>!/bin/bash

if (( $# &lt; 3 ))
then
    echo "Usage:   $0 &lt;/path/to/repo/&gt; &lt;directory/to/extract/&gt; &lt;newName&gt;"
    echo
    echo "Example: $0 /Projects/42.git first/answer/ firstAnswer"
    exit 1
fi


clone=/tmp/${3}Clone
newN=/tmp/${3}

git clone --no-hardlinks file://$1 ${clone}
cd ${clone}

git filter-branch --subdirectory-filter $2  --prune-empty --tag-name-filter cat -- --all

git clone file://${clone} ${newN}
cd ${newN}

git reflog expire --expire=now --all
git repack -ad
git gc --prune=now
</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-9182278">
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
<p>For what it's worth, here is how using GitHub on a Windows machine. Let's say you have a cloned repo in residing in <code>C:\dir1</code>. The directory structure looks like this: <code>C:\dir1\dir2\dir3</code>. The <code>dir3</code> directory is the one I want to be a new separate repo.  </p>

<p><strong>Github:</strong></p>

<ol>
<li>Create your new repository: <code>MyTeam/mynewrepo</code></li>
</ol>

<p><strong>Bash Prompt:</strong></p>

<ol>
<li><code>$ cd c:/Dir1</code></li>
<li><p><code>$ git filter-branch --prune-empty --subdirectory-filter dir2/dir3 HEAD</code><br />
Returned: <code>Ref 'refs/heads/master' was rewritten</code> (fyi: dir2/dir3 is case sensitive.)</p></li>
<li><p><code>$ git remote add some_name git@github.com:MyTeam/mynewrepo.git</code><br />
<code>git remote add origin etc</code>. did not work, returned "<code>remote origin already exists</code>"</p></li>
<li><p><code>$ git push --progress some_name master</code>   </p></li>
</ol>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-10185428">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        10
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>The original question wants XYZ/ABC/(*files) to become ABC/ABC/(*files). After implementing the accepted answer for my own code, I noticed that it actually changes XYZ/ABC/(*files) into ABC/(*files). The filter-branch man page even says, </p>

<blockquote>
  <p>The result will contain that directory (and only that) <em>as its project root</em>." </p>
</blockquote>

<p>In other words, it promotes the top-level folder "up" one level. That's an important distinction because, for example, in my history I had renamed a top-level folder. By promoting folders "up" one level, git loses continuity at the commit where I did the rename.</p>

<p><img src="https://i.stack.imgur.com/qR1zI.png" alt="I lost contiuity after filter-branch" /></p>

<p>My answer to the question then is to make 2 copies of the repository and manually delete the folder(s) you want to keep in each. The man page backs me up with this:</p>

<blockquote>
  <p>[...] avoid using [this command]  if a simple single commit would suffice to fix your problem</p>
</blockquote>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Apr 17 '12 at 5:12
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-15710792">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Put this into your gitconfig:</p>

<pre><code>reduce-to-subfolder = !sh -c 'git filter-branch --tag-name-filter cat --prune-empty --subdirectory-filter cookbooks/unicorn HEAD && git reset --hard && git for-each-ref refs/original/ | cut -f 2 | xargs -n 1 git update-ref -d && git reflog expire --expire=now --all && git gc --aggressive --prune=now && git remote rm origin'
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 29 '13 at 20:18
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-16854710">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>As I <a href="https://stackoverflow.com/questions/359424/detach-subdirectory-into-separate-git-repository#comment24306261_10185428" target="_blank">mentioned above</a>, I had to use the reverse solution (deleting all commits not touching my <code>dir/subdir/targetdir</code>) which seemed to work pretty well removing about 95% of the commits (as desired).  There are, however, two small issues remaining.</p>

<p><strong>FIRST</strong>, <code>filter-branch</code> did a bang up job of removing commits which introduce or modify code but apparently, <strong>merge commits</strong> are beneath its station in the Gitiverse.  </p>

<ul>
<li><strong><a href="https://www.evernote.com/shard/s4/sh/a3d2bdfb-119e-4c06-bbe7-31caa1e7f33c/40bf20f0378670f9f3307e03119fbdfc" target="_blank">Screenshot: Merge Madness!</a></strong></li>
</ul>

<p>This is a cosmetic issue which I can probably live with <em>(he says...backing away slowly with eyes averted)</em>.</p>

<p><strong>SECOND</strong> the few commits that remain are pretty much <strong>ALL</strong> duplicated!  I seem to have acquired a second, redundant timeline that spans just about the entire history of the project.  The interesting thing (which you can see from the picture below), is that my three local branches are not all on the same timeline (which is, certainly why it exists and isn't just garbage collected).</p>

<ul>
<li><strong><a href="https://www.evernote.com/shard/s4/sh/f474a082-1aa6-4fc5-a2ea-3a8978cf7eb0/b5ef88551c266df9af3d8b86d5a7dd56" target="_blank">Screnshot: Double-double, Git filter-branch style</a></strong></li>
</ul>

<p>The only thing I can imagine is that one of the deleted commits was, perhaps, the single merge commit that <code>filter-branch</code> <em>actually did delete</em>, and that created the parallel timeline as each now-unmerged strand took its own copy of the commits. (<em>shrug</em> Where's my TARDiS?)  I'm pretty sure I can fix this issue, though I'd <em>really</em> love to understand how it happened.</p>

<p>In the case of crazy mergefest-O-RAMA, I'll likely be leaving that one alone since it has so firmly entrenched itself in my commit history—menacing at me whenever I come near—, it doesn't seem to be actually causing any non-cosmetic problems and because it is quite pretty in Tower.app.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-17864475">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1088
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<h1>The Easy Way™</h1>

<p>It turns out that this is such a common and useful practice that the overlords of git made it really easy, but you have to have a newer version of git (&gt;= 1.7.11 May 2012). See the <strong>appendix</strong> for how to install the latest git. Also, there's a <strong>real-world example</strong> in the <strong>walkthrough</strong> below.</p>

<ol>
<li><p>Prepare the old repo</p>

<pre><code>pushd &lt;big-repo&gt;
git subtree split -P &lt;name-of-folder&gt; -b &lt;name-of-new-branch&gt;
popd
</code></pre>

<p><strong>Note:</strong> <code>&lt;name-of-folder&gt;</code> must NOT contain leading or trailing characters.  For instance, the folder named <code>subproject</code> MUST be passed as <code>subproject</code>, NOT <code>./subproject/</code></p>

<p><strong>Note for windows users:</strong> when your folder depth is &gt; 1, <code>&lt;name-of-folder&gt;</code> must have *nix style folder separator (/). For instance, the folder named <code>path1\path2\subproject</code> MUST be passed as <code>path1/path2/subproject</code></p></li>
<li><p>Create the new repo</p>

<pre><code>mkdir &lt;new-repo&gt;
pushd &lt;new-repo&gt;

git init
git pull &lt;/path/to/big-repo&gt; &lt;name-of-new-branch&gt;
</code></pre></li>
<li><p>Link the new repo to Github or wherever</p>

<pre><code>git remote add origin &lt;git@github.com:my-user/new-repo.git&gt;
git push origin -u master
</code></pre></li>
<li><p>Cleanup, <em>if desired</em></p>

<pre><code>popd # get out of &lt;new-repo&gt;
pushd &lt;big-repo&gt;

git rm -rf &lt;name-of-folder&gt;
</code></pre>

<p><strong>Note</strong>: This leaves all the historical references in the repository.See the <strong>Appendix</strong> below if you're actually concerned about having committed a password or you need to decreasing the file size of your <code>.git</code> folder.</p></li>
</ol>



<h1>Walkthrough</h1>

<p>These are the <strong>same steps as above</strong>, but following my exact steps for my repository instead of using <code>&lt;meta-named-things&gt;</code>.</p>

<p>Here's a project I have for implementing JavaScript browser modules in node:</p>

<pre><code>tree ~/Code/node-browser-compat

node-browser-compat
├── ArrayBuffer
├── Audio
├── Blob
├── FormData
├── atob
├── btoa
├── location
└── navigator
</code></pre>

<p>I want to split out a single folder, <code>btoa</code>, into a separate git repository</p>

<pre><code>pushd ~/Code/node-browser-compat/
git subtree split -P btoa -b btoa-only
popd
</code></pre>

<p>I now have a new branch, <code>btoa-only</code>, that only has commits for <code>btoa</code> and I want to create a new repository.</p>

<pre><code>mkdir ~/Code/btoa/
pushd ~/Code/btoa/
git init
git pull ~/Code/node-browser-compat btoa-only
</code></pre>

<p>Next I create a new repo on Github or bitbucket, or whatever and add it is the <code>origin</code> (btw, "origin" is just a convention, not part of the command - you could call it "remote-server" or whatever you like)</p>

<pre><code>git remote add origin git@github.com:node-browser-compat/btoa.git
git push origin -u master
</code></pre>

<p>Happy day!</p>

<p><strong>Note:</strong> If you created a repo with a <code>README.md</code>, <code>.gitignore</code> and <code>LICENSE</code>, you will need to pull first:</p>

<pre><code>git pull origin -u master
git push origin -u master
</code></pre>

<p>Lastly, I'll want to remove the folder from the bigger repo</p>

<pre><code>git rm -rf btoa
</code></pre>



<h1>Appendix</h1>

<h2>Latest git on OS X</h2>

<p>To get the latest version of git:</p>

<pre><code>brew install git
</code></pre>

<p>To get brew for OS X:</p>

<p><a href="http://brew.sh" target="_blank">http://brew.sh</a></p>

<h2>Latest git on Ubuntu</h2>

<pre><code>sudo apt-get update
sudo apt-get install git
git --version
</code></pre>

<p>If that doesn't work (you have a very old version of ubuntu), try</p>

<pre><code>sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
</code></pre>

<p>If that still doesn't work, try</p>

<pre><code>sudo chmod +x /usr/share/doc/git/contrib/subtree/git-subtree.sh
sudo ln -s \
/usr/share/doc/git/contrib/subtree/git-subtree.sh \
/usr/lib/git-core/git-subtree
</code></pre>

<p>Thanks to rui.araujo from the comments.</p>

<h2>clearing your history</h2>

<p>By default removing files from git doesn't actually remove them from git, it just commits that they aren't there anymore. If you want to actually remove the historical references (i.e. you have a committed a password), you need to do this:</p>

<pre><code>git filter-branch --prune-empty --tree-filter 'rm -rf &lt;name-of-folder&gt;' HEAD
</code></pre>

<p>After that you can check that your file or folder no longer shows up in the git history at all</p>

<pre><code>git log -- &lt;name-of-folder&gt; # should show nothing
</code></pre>

<p>However, you <strong>can't "push" deletes to github</strong> and the like. If you try you'll get an error and you'll have to <code>git pull</code> before you can <code>git push</code> - and then you're back to having everything in your history.</p>

<p>So if you want to delete history from the "origin" - meaning to delete it from github, bitbucket, etc - you'll need to delete the repo and re-push a pruned copy of the repo. But wait - <strong>there's more</strong>! - If you're really concerned about getting rid of a password or something like that you'll need to prune the backup (see below).</p>

<h2>making <code>.git</code> smaller</h2>

<p>The aforementioned delete history command still leaves behind a bunch of backup files - because git is all too kind in helping you to not ruin your repo by accident. It will eventually deleted orphaned files over the days and months, but it leaves them there for a while in case you realize that you accidentally deleted something you didn't want to.</p>

<p>So if you really want to <em>empty the trash</em> to <strong>reduce the clone size</strong> of a repo immediately you have to do all of this really weird stuff:</p>

<pre><code>rm -rf .git/refs/original/ && \
git reflog expire --all && \
git gc --aggressive --prune=now

git reflog expire --all --expire-unreachable=0
git repack -A -d
git prune
</code></pre>

<p>That said, I'd recommend not performing these steps unless you know that you need to - just in case you did prune the wrong subdirectory, y'know? The backup files shouldn't get cloned when you push the repo, they'll just be in your local copy.</p>

<h1>Credit</h1>


    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-22307345">
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
<p>I had exactly this problem but all the standard solutions based on git filter-branch were extremely slow. If you have a small repository then this may not be a problem, it was for me. I wrote another git filtering program based on libgit2 which as a first step creates branches for each filtering of the primary repository and then pushes these to clean repositories as the next step. On my repository (500Mb 100000 commits) the standard git filter-branch methods took days. My program takes minutes to do the same filtering.</p>

<p>It has the fabulous name of git_filter and lives here: </p>

<p><a href="https://github.com/slobobaby/git_filter" target="_blank">https://github.com/slobobaby/git_filter</a> </p>

<p>on GitHub.</p>

<p>I hope it is useful to someone.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 10 '14 at 17:39
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-25406990">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        21
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>This is no longer so complex you can just use the <a href="http://git-scm.com/docs/git-filter-branch" target="_blank">git filter-branch</a> command on a clone of you repo to cull the subdirectories you don't want and then push to the new remote.</p>

<pre><code>git filter-branch --prune-empty --subdirectory-filter &lt;YOUR_SUBDIR_TO_KEEP&gt; master
git push &lt;MY_NEW_REMOTE_URL&gt; -f .
</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-26888022">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Proper way now is the following:</p>

<p><code>git filter-branch --prune-empty --subdirectory-filter FOLDER_NAME [first_branch] [another_branch]</code></p>

<p>GitHub now even have <a href="https://help.github.com/articles/splitting-a-subfolder-out-into-a-new-repository/" target="_blank">small article</a> about such cases.</p>

<p>But be sure to clone your original repo to separate directory first (as it would delete all the files and other directories and you probable need to work with them).</p>

<p>So your algorithm should be:</p>

<ol>
<li>clone your remote repo to another directory</li>
<li>using <code>git filter-branch</code> left only files under some subdirectory, push to new remote</li>
<li>create commit to remove this subdirectory from your original remote repo</li>
</ol>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-28451972">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<h1>The Easier Way</h1>

<ol>
<li>install <a href="https://github.com/simpliwp/git-splits" target="_blank"><code>git splits</code></a>. I created it as a git extension, based on <a href="https://stackoverflow.com/a/6006679/3306354" target="_blank">jkeating's solution</a>. </li>
<li><p>Split the directories into a local branch
<code>
   #change into your repo's directory
   cd /path/to/repo
   #checkout the branch
   git checkout XYZ<br />
   #split multiple directories into new branch XYZ
   git splits -b XYZ XY1 XY2
</code></p></li>
<li><p>Create an empty repo somewhere. We'll assume we've created an empty repo called <code>xyz</code> on GitHub that has path : <code>git@github.com:simpliwp/xyz.git</code></p></li>
<li><p>Push to the new repo.
<code>
   #add a new remote origin for the empty repo so we can push to the empty repo on GitHub
   git remote add origin_xyz git@github.com:simpliwp/xyz.git
   #push the branch to the empty repo's master branch
   git push origin_xyz XYZ:master
</code></p></li>
<li><p>Clone the newly created remote repo into a new local directory<br />
<code>
   #change current directory out of the old repo
   cd /path/to/where/you/want/the/new/local/repo
   #clone the remote repo you just pushed to 
   git clone  git@github.com:simpliwp/xyz.git
</code></p></li>
</ol>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-31859803">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        13
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Here is a small modification to <a href="https://stackoverflow.com/users/151312/coolaj86" target="_blank">CoolAJ86</a>'s <a href="https://stackoverflow.com/a/17864475/535203" target="_blank">"The Easy Way™" answer</a> in order to split <strong>multiple sub folders</strong> (let's say <code>sub1</code>and <code>sub2</code>) into a new git repository.</p>

<h1>The Easy Way™ (multiple sub folders)</h1>

<ol>
<li><p>Prepare the old repo</p>

<pre><code>pushd &lt;big-repo&gt;
git filter-branch --tree-filter "mkdir &lt;name-of-folder&gt;; mv &lt;sub1&gt; &lt;sub2&gt; &lt;name-of-folder&gt;/" HEAD
git subtree split -P &lt;name-of-folder&gt; -b &lt;name-of-new-branch&gt;
popd
</code></pre>

<p><strong>Note:</strong> <code>&lt;name-of-folder&gt;</code> must NOT contain leading or trailing characters.  For instance, the folder named <code>subproject</code> MUST be passed as <code>subproject</code>, NOT <code>./subproject/</code></p>

<p><strong>Note for windows users:</strong> when your folder depth is &gt; 1, <code>&lt;name-of-folder&gt;</code> must have *nix style folder separator (/). For instance, the folder named <code>path1\path2\subproject</code> MUST be passed as <code>path1/path2/subproject</code>. Moreover don't use <code>mv</code>command but <code>move</code>.</p>

<p><strong>Final note:</strong> the unique and big difference with the base answer is the second line of the script "<code>git filter-branch...</code>"</p></li>
<li><p>Create the new repo</p>

<pre><code>mkdir &lt;new-repo&gt;
pushd &lt;new-repo&gt;

git init
git pull &lt;/path/to/big-repo&gt; &lt;name-of-new-branch&gt;
</code></pre></li>
<li><p>Link the new repo to Github or wherever</p>

<pre><code>git remote add origin &lt;git@github.com:my-user/new-repo.git&gt;
git push origin -u master
</code></pre></li>
<li><p>Cleanup, <em>if desired</em></p>

<pre><code>popd # get out of &lt;new-repo&gt;
pushd &lt;big-repo&gt;

git rm -rf &lt;name-of-folder&gt;
</code></pre>

<p><strong>Note</strong>: This leaves all the historical references in the repository.See the <strong>Appendix</strong> in the original answer if you're actually concerned about having committed a password or you need to decreasing the file size of your <code>.git</code> folder.</p></li>
</ol>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-34624761">
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
<p>Check out git_split project at <a href="https://github.com/vangorra/git_split" target="_blank">https://github.com/vangorra/git_split</a></p>

<p>Turn git directories into their very own repositories in their own location. No subtree funny business. This script will take an existing directory in your git repository and turn that directory into an independent repository of its own. Along the way, it will copy over the entire change history for the directory you provided. </p>

<pre><code>./git_split.sh &lt;src_repo&gt; &lt;src_branch&gt; &lt;relative_dir_path&gt; &lt;dest_repo&gt;
        src_repo  - The source repo to pull from.
        src_branch - The branch of the source repo to pull from. (usually master)
        relative_dir_path   - Relative path of the directory in the source repo to split.
        dest_repo - The repo to push to.
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 6 '16 at 2:42
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-35321301">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I'm sure git subtree is all fine and wonderful, but my subdirectories of git managed code that I wanted to move was all in eclipse.
So if you're using egit, it's painfully easy.
Take the project you want to move and team-&gt;disconnect it, and then team-&gt;share it to the new location. It will default to trying to use the old repo location, but you can uncheck the use-existing selection and pick the new place to move it.
All hail egit.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Feb 10 '16 at 16:57
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-39580074">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>It appears that most (all?) of the answers here rely on some form of <code>git filter-branch --subdirectory-filter</code> and its ilk.  This may work "most times" however for some cases, for instance the case of when you renamed the folder, ex:</p>

<pre><code> ABC/
    /move_this_dir # did some work here, then renamed it to

ABC/
    /move_this_dir_renamed
</code></pre>

<p>If you do a normal git filter style to extract "move_me_renamed" you will lose file change history that occurred from back when it was initially move_this_dir (<a href="https://stackoverflow.com/questions/2797191/how-to-split-a-git-repository-while-preserving-subdirectories" target="_blank">ref</a>).</p>

<p>It thus appears that the only way to really keep <em>all</em> change history (if yours is a case like this), is, in essence, to copy the repository (create a new repo, set that to be the origin), then nuke everything else and rename the subdirectory to the parent like this:</p>

<ol>
<li>Clone the multi-module project locally</li>
<li>Branches - check what's there: <code>git branch -a</code></li>
<li>Do a checkout to each branch to be included in the split to get a local copy on your workstation: <code>git checkout --track origin/branchABC</code></li>
<li>Make a copy in a new directory: <code>cp -r oldmultimod simple</code></li>
<li>Go into the new project copy: <code>cd simple</code></li>
<li>Get rid of the other modules that aren't needed in this project: </li>
<li><code>git rm otherModule1 other2 other3</code></li>
<li>Now only the subdir of the target module remains </li>
<li>Get rid of the module subdir so that the module root becomes the new project root</li>
<li><code>git mv moduleSubdir1/* .</code></li>
<li>Delete the relic subdir: <code>rmdir moduleSubdir1</code></li>
<li>Check changes at any  point: <code>git status</code></li>
<li>Create the new git repo and copy its URL to point this project into it:</li>
<li><code>git remote set-url origin http://mygithost:8080/git/our-splitted-module-repo</code></li>
<li>Verify this is good: <code>git remote -v</code></li>
<li>Push the changes up to the remote repo: <code>git push</code></li>
<li>Go to the remote repo and check it's all there</li>
<li>Repeat it for any other branch needed: <code>git checkout branch2</code></li>
</ol>

<p>This follows <a href="https://help.github.com/articles/splitting-a-subfolder-out-into-a-new-repository/" target="_blank">the github doc "Splitting a subfolder out into a new repository"</a> steps 6-11 to push the module to a new repo.</p>

<p>This will not save you any space in your .git folder, but it will preserve all your change history for those files even across renames.  And this may not be worth it if there isn't "a lot" of history lost, etc.  But at least you are guaranteed not to lose older commits!</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-45983384">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>


<p>I recommend <a href="https://help.github.com/articles/splitting-a-subfolder-out-into-a-new-repository/" target="_blank">GitHub's guide to splitting subfolders into a new repository</a>. The steps are similar to <a href="https://stackoverflow.com/a/359759/3357935" target="_blank">Paul's answer</a>, but I found their instructions easier to understand.</p>

<p>I have modified the instructions so that they apply for a local repository, rather than one hosted on GitHub.</p>

<hr />

<blockquote>
  <h3><a href="https://help.github.com/articles/splitting-a-subfolder-out-into-a-new-repository/" target="_blank">Splitting a subfolder out into a new repository</a></h3>
  
  <ol>
  <li><p>Open Git Bash.</p></li>
  <li><p>Change the current working directory to the location where you want to create your new repository.</p></li>
  <li><p>Clone the repository that contains the subfolder.</p></li>
  </ol>
  
  <pre><code>git clone OLD-REPOSITORY-FOLDER NEW-REPOSITORY-FOLDER</code></pre>
  
  <ol>
  <li>Change the current working directory to your cloned repository.</li>
  </ol>
  
  <pre><code>cd REPOSITORY-NAME</code></pre>
  
  <ol>
  <li>To filter out the subfolder from the rest of the files in the repository, run <code>git filter-branch</code>, supplying this information:
  
  <ul>
  <li><code>FOLDER-NAME</code>: The folder within your project that you'd like to create a separate repository from.
  
  <ul>
  <li>Tip: Windows users should use <code>/</code> to delimit folders.</li>
  </ul></li>
  <li><code>BRANCH-NAME</code>: The default branch for your current project, for example, <code>master</code> or <code>gh-pages</code>.</li>
  </ul></li>
  </ol>
  
  <pre><code>git filter-branch --prune-empty --subdirectory-filter FOLDER-NAME  BRANCH-NAME 
# Filter the specified branch in your directory and remove empty commits
Rewrite 48dc599c80e20527ed902928085e7861e6b3cbe6 (89/89)
Ref 'refs/heads/BRANCH-NAME' was rewritten</code></pre>
</blockquote>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 31 '17 at 14:02
    </div>
    
    
</div>
    </div>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/git" title="show questions tagged 'git'" target="_blank">git</a> <a href="/questions/tagged/git-subtree" title="show questions tagged 'git-subtree'" target="_blank">git-subtree</a> <a href="/questions/tagged/git-filter-branch" title="show questions tagged 'git-filter-branch'" target="_blank">git-filter-branch</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
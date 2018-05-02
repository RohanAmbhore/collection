<a href="https://stackoverflow.com/questions/18126297/when-to-use-the-no-ff-merge-option-in-git">https://stackoverflow.com/questions/18126297/when-to-use-the-no-ff-merge-option-in-git</a><div id="articleHeader"><h1>When to use the '--no-ff' merge option in Git</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        56
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>18</b></div>


</div>

            </div>

            
<div>
    <div>

<p><a href="http://nvie.com/posts/a-successful-git-branching-model/" target="_blank">A Successful Git Branching Model</a> recommends to use <code>--no-ff</code> when merging branches:</p>

<blockquote>
  <p>The <code>--no-ff</code> flag causes the merge to always create a new commit
  object, even if the merge could be performed with a fast-forward. This
  avoids losing information about the historical existence of a feature
  branch and groups together all commits that together added the
  feature. […]</p>
  
  <p>Yes, it will create a few more (empty) commit objects, but the gain is
  much bigger that that cost. Unfortunately, I have not found a way to
  make <code>--no-ff</code> the default behavior of git merge yet, but it really
  should be.</p>
</blockquote>

<p><a href="https://sandofsky.com/blog/git-workflow.html" target="_blank">Understanding the Git Workflow</a>, however, recommends <em>not</em> to use <code>--no-ff</code>:</p>

<blockquote>
  <p>So you add a new rule: “When you merge in your feature branch, use
  <code>–-no-ff</code> to force a new commit.” This gets the job done, and you move
  on. […]</p>
  
  <p>The <code>--no-ff</code> band-aid, broken <a href="https://www.kernel.org/pub/software/scm/git/docs/git-bisect.html" target="_blank"><code>bisect</code></a>, and <a href="https://www.kernel.org/pub/software/scm/git/docs/git-blame.html" target="_blank"><code>blame</code></a> mysteries are all
  symptoms that you’re using a screwdriver as a hammer. […]</p>
</blockquote>

<p>Both approaches seem reasonable for difference scenarios, but what is considered "good practice?"</p>

<p>When do you use <code>--no-ff</code>, when do you not, why?</p>
    </div>
    
    
</div>

                        <div>
                <div>
        <h2>                    <b>protected</b> by <a href="/users/584192/samuel-liew" target="_blank">Samuel Liew</a>♦ Mar 10 '17 at 3:40
</h2>
        <p>
This question is protected to prevent "thanks!", "me too!", or spam answers by new users. 
To answer it, you must have earned at least 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).</p>
    </div>
            </div>
    
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-18128086">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        40
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>It's really dependent on what you're trying to do. My rule of thumb is that if the merge "means something" I use the --no-ff option. When the merge doesn't really mean anything and you might have used a rebase there's no reason to use --no-ff</p>

<p>The thing with git is that it's a very powerful tool, and you can use it in many ways - most of which are not wrong. Asking what's the "right way" to do it is like asking what's the right way to paint a picture.</p>

<p>At least for me it's an evolving set of ways I like to do it, with frequent discussions in the team of how we want to collaborate on the code - from this we try to derive a kind of "how it's done here" standard, but it's just our way of doing it.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-18127234">
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
<p>That really depends on your workflow, and how you are using branches.</p>

<p>Let´s say you have a "master" and two feature branches, "foo" and "bar", in development.</p>

<p>In this case, the branches only exist to allow different developer work without conflict, when the features are done, they need to be merged into master, and it is not important to know if those features were implemented in different branches.</p>

<p>But you could have a different workflow, were the branches, "foo" and "bar", refers to independent modules in your system.</p>

<p>In this case, some commits may change files outside the module scope. When you merge those two branches to the master, the log of the files, outside the specific module, may become confusing and hard to know where those changes come from.</p>

<p>You need to decide if the historic of branch´s merge is important to your workflow.</p>

<p>And following the comments, I prefer the <code>rebase</code>, and <code>pull --rebase</code> workflow.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 8 '13 at 13:25
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-18128585">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        41
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>For the case of a finished branch with a single commit, don't use <code>--no-ff</code>, just fast-forward it, because the history will be much simpler and less cluttered. It's hard to argue that <code>--no-ff</code> gets you any advantages in this case, because it's uninteresting to see a parallel branch of development with just a single commit, vs a single commit in a sequential line:</p>

<pre><code># No fast-forward
$ git merge --no-ff awesome-feature
*   3aa649c Merge branch 'awesome-feature'
|\
| * 35ec88f Add awesome feature
|/
* 89408de Modify feature-001.txt and fix-001.txt
* c1abcde Add feature-003

# versus fast-forward
$ git merge awesome-feature
* 35ec88f Add awesome feature
* 89408de Modify feature-001.txt and fix-001.txt
* c1abcde Add feature-003
</code></pre>

<p>For the case of a finished branch with more than a single commit, it's up to you, whether or not you want to keep the fact that the branched development happened in parallel vs sequential. I would probably use <code>--no-ff</code> for more than one commit, just so that I can visually see this branched work, and so that I can manipulate it easily with a single <code>git revert -m 1 &lt;sha-of-merge-commit&gt;</code> if I had to.</p>

<pre><code># No fast-forward
$ git merge --no-ff epic-feature
*   d676897 Merge branch 'epic-feature'
|\
| * ba40d93 Add octocat.txt
| * b09d343 Add bye.txt
| * 75e18c8 Add hello.txt
|/
* 89408de Modify feature-001.txt and fix-001.txt
* c1abcde Add feature-003

# versus fast-forward
$ git merge epic-feature
* ba40d93 Add octocat.txt
* b09d343 Add bye.txt
* 75e18c8 Add hello.txt
* 89408de Modify feature-001.txt and fix-001.txt
* c1abcde Add feature-003
</code></pre>

<p>See how in this case of fast-forward merge, without additional information in the commit messages themselves, it's hard to tell that the last 3 commits actually belong together as one feature?</p>
    </div>
    <div>
    
    <div>
<div>
    <div>
        <a href="/posts/18128585/revisions" title="show all edits to this post" target="_blank">edited Aug 8 '13 at 14:32</a>
    </div>
    
    
</div>    </div>
            


    <div>
       

    <div>
    <div>
        answered Aug 8 '13 at 14:24
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/git" title="show questions tagged 'git'" target="_blank">git</a> <a href="/questions/tagged/git-merge" title="show questions tagged 'git-merge'" target="_blank">git-merge</a> <a href="/questions/tagged/fast-forward" title="show questions tagged 'fast-forward'" target="_blank">fast-forward</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
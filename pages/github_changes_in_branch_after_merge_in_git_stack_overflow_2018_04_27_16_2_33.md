<a href="https://stackoverflow.com/questions/42786656/changes-in-branch-after-merge-in-git">https://stackoverflow.com/questions/42786656/changes-in-branch-after-merge-in-git</a><div id="articleHeader"><h1>Changes in branch after merge in git</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        0
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>1</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I have two branches, <code>foo</code> and <code>bar</code> under <code>master</code> in a project that I'm managing with git. Let's suppose I work under <code>foo</code> and after being done with it, I merge the changes with <code>master</code>. Then I go to <code>bar</code> and repeat the process. But then someone tells me there's something I have to change on <code>foo</code>, so my first idea was to repeat again, but then I lose all the work done under <code>bar</code> branch. How do I achieve my purpose of coming back to a branch and then when I merge with <code>master</code> I don't override the changes made under <code>bar</code></p>

<p>I tried creating a new branch for those new changes but if this is the approach, I find the branches a bit useless. But I think git is smart enough to do what I want.</p>
    </div>
    
    <div>
    

    <div>
        <div>
    <div>
        asked Mar 14 '17 at 12:57
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-42788972">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>Answering with a series of diagrams:</p>



<p>create <code>foo</code> and <code>bar</code> off <code>master</code> after commit C:</p>

<pre><code>                       foo
                      /
master A ---- B ---- C
                      \
                       bar
</code></pre>

<hr />

<p>work on <code>foo</code> and merge into <code>master</code>: (<code>git checkout master && git merge foo</code>)</p>

<pre><code>foo                    D ---- E ---- F
                      /               \ (merge-commit)
master A ---- B ---- C --------------- G 
                      \
                       bar
</code></pre>

<hr />

<p>meanwhile, <code>bar</code> progressed independently..</p>

<pre><code>foo                    D ---- E ---- F
                      /               \
master A ---- B ---- C --------------- G 
                      \
bar                    D' ---- E' ----- F'
</code></pre>

<hr />

<p>you now wish to update <code>bar</code> with changes to <code>master</code> (<code>git pull origin master</code>)</p>

<pre><code>foo                    D ---- E ----------- F
                      /                      \
master A ---- B ---- C ---------------------- G 
                      \                        \
bar                    D' ---- E' ----- F' ---- G' (another merge-commit)
</code></pre>

<hr />

<p>another change commited on <code>foo</code></p>

<pre><code>foo                    D ---- E ----------- F ---- H
                      /                      \
master A ---- B ---- C ---------------------- G 
                      \                        \
bar                    D' ---- E' ----- F' ---- G'
</code></pre>

<hr />

<p>then, to sync <code>bar</code> with new <code>foo</code> (<code>git checkout bar && git pull origin foo</code>)</p>

<pre><code>foo                    D ---- E ----------- F ---- H
                      /                      \      \
master A ---- B ---- C ---------------------- G      \
                      \                        \      \
bar                    D' ---- E' ----- F' ---- G'---- H' (another merge-commit) 
</code></pre>

<hr />

<p>then merge <code>bar</code> into <code>master</code> (with <code>master</code> as active branch, <code>git merge bar</code>)</p>

<pre><code>foo                    D ---- E ----------- F ---- H
                      /                      \      \
master A ---- B ---- C ---------------------- G -----}-------- I (latest merge-commit)
                      \                        \      \      /
bar                    D' ---- E' ----- F' ---- G'---- H' ---
</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-42787184">
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
<blockquote>
  <p>Then I go to bar and repeat the process</p>
</blockquote>

<p>Why don't you merge master or foo in bar? That's unclear to me.</p>

<blockquote>
  <p>But then someone tells me there's something I have to change on foo, so my first idea was to repeat again, but then I lose all the work done under bar branch.</p>
</blockquote>

<p>What do you mean with repeat? Commit you last changes and checkout the other branch.</p>

<p>Also if you made changes that you won't commit you can use git stash for storing the changes temporary.</p>

<p>Please specify your question for more detailed help.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 14 '17 at 13:21
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-42789479">
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
<p>If your <code>foo</code> and <code>bar</code> branch is not yet deleted, you can rebase</p>

<pre><code>git checkout master
git pull
git checkout foo
git rebase master
git checkout bar
git rebase master
</code></pre>

<p>But ideally, if your <code>foo</code> and <code>bar</code> branch is a feature/issue, you should only merge them to master when it's done. If it's too big, break it down to smaller branches (nester or flat). </p>

<blockquote>
  <p>I don't override the changes made under bar</p>
</blockquote>

<p>this depends on your changes and why care, you merge <code>bar</code> branch to <code>master</code> anyway. It's none of <code>bar</code> business if the work he have done is modify because that feature/fix is done (that's why you merge it). Actually, when you finished a feature/fix branch and merge it master, ideally you delete it cause it's done.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 14 '17 at 15:00
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/git" title="show questions tagged 'git'" target="_blank">git</a> <a href="/questions/tagged/github" title="show questions tagged 'github'" target="_blank">github</a> <a href="/questions/tagged/merge" title="show questions tagged 'merge'" target="_blank">merge</a> <a href="/questions/tagged/branch" title="show questions tagged 'branch'" target="_blank">branch</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
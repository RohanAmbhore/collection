<a href="https://stackoverflow.com/questions/12481639/remove-files-from-git-commit">https://stackoverflow.com/questions/12481639/remove-files-from-git-commit</a><div id="articleHeader"><h1>Remove files from Git commit</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        971
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>331</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I am using Git and I have committed few files using </p>

<pre><code>git commit -a
</code></pre>

<p>Later, I found that a file had mistakenly been added to the commit.</p>

<p>How can I remove a file from the last commit?</p>
    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-15321456">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1898
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>I think other answers here are wrong, because this is a question of moving the mistakenly committed files back to the staging area from the previous commit, without cancelling the changes done to them. This can be done like Paritosh Singh suggested:</p>

<pre><code>git reset --soft HEAD^ 
</code></pre>



<pre><code>git reset --soft HEAD~1
</code></pre>

<p>Then reset the unwanted files in order to leave them out from the commit:</p>

<pre><code>git reset HEAD path/to/unwanted_file
</code></pre>

<p>Now commit again, you can even re-use the same commit message:</p>

<pre><code>git commit -c ORIG_HEAD  
</code></pre>
    </div>
    <div>
    
    
            


    <div>
       

    <div>
    <div>
        answered Mar 10 '13 at 10:56
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-12481977">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        200
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>ATTENTION</strong>! If you only want to remove a file from your previous commit, and <em>keep it on disk</em>, read <a href="https://stackoverflow.com/a/15321456/11343" target="_blank">juzzlin's answer</a> just above.</p>

<p>If this is your last commit and you want to <strong>completely delete the file from your local and the remote repository</strong>, you can: </p>

<ol>
<li>remove the file <code>git rm &lt;file&gt;</code></li>
<li>commit with amend flag: <code>git commit --amend</code></li>
</ol>

<p>The amend flag tells git to commit again, but "merge" (not in the sense of merging two branches) this commit with the last commit.</p>

<p>As stated in the comments, using <code>git rm</code> here is like using the <code>rm</code> command itself!</p>
    </div>
    <div>
    
    
            


    <div>
       

    <div>
    <div>
        answered Sep 18 '12 at 17:22
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-12482845">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        34
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>If you have not pushed the changes on the server you can use</p>

<pre><code>git reset --soft HEAD~1
</code></pre>

<p>It will reset all the changes and revert to one  commit back</p>

<p>If you have pushed your changes then follow steps as answered by @CharlesB</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-14563682">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        34
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Removing the file using rm will delete it!</p>

<p>You're always adding to a commit in git rather than removing, so in this instance return the file to the state it was in prior to the first commit (this may be a delete 'rm' action if the file is new) and then re-commit and the file will go.</p>

<p>To return the file to some previous state:</p>

<pre><code>    git checkout &lt;commit_id&gt; &lt;path_to_file&gt;
</code></pre>

<p>or to return it to the state at the remote HEAD:</p>

<pre><code>    git checkout origin/master &lt;path_to_file&gt;
</code></pre>

<p>then amend the commit and you should find the file has disappeared from the list (and not deleted from your disk!)</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 28 '13 at 14:00
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-17155890">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>If you want to preserve your commit (maybe you already spent some time writing a detailed commit message and don't want to lose it), and you only want to remove the file from the commit, but not from the repository entirely:</p>

<pre><code>git checkout origin/&lt;remote-branch&gt; &lt;filename&gt;
git commit --amend
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jun 17 '13 at 20:07
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-18410048">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        30
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<pre><code>git checkout HEAD~ path/to/file
git commit --amend
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 23 '13 at 19:01
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-25300710">
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
<p>Something that worked for me, but still think there should be a better solution:</p>

<pre><code>$ git revert &lt;commit_id&gt;
$ git reset HEAD~1 --hard
</code></pre>

<p>Just leave the change you want to discard in the other commit, check others out</p>

<pre><code>$ git commit --amend // or stash and rebase to &lt;commit_id&gt; to amend changes
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 14 '14 at 5:34
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-27340569">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        28
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>The following will unstage just the file you intended, which is what the OP asked.</p>

<pre><code>git reset HEAD^ /path/to/file
</code></pre>

<p>You'll see something like the following...</p>

<blockquote>
  <p>Changes to be committed:   (use "git reset HEAD ..." to unstage)</p>
  
  <p>modified:   /path/to/file</p>
  
  <p>Changes not staged for commit:   (use "git add ..." to update
  what will be committed)   (use "git checkout -- ..." to discard
  changes in working directory)</p>
  
  <p>modified:   /path/to/file</p>
</blockquote>

<ul>
<li>"Changes to be committed" is the previous version of the file before the commit.  This will look like a deletion if the file never existed.  If you commit this change, there will be a revision that reverts the change to the file in your branch.</li>
<li>"Changes not staged for commit" is the change you committed, and the current state of the file</li>
</ul>

<p>At this point, you can do whatever you like to the file, such as resetting to a different version.  </p>

<p>When you're ready to commit:</p>

<pre><code>git commit --amend -a
</code></pre>

<p>or (if you've got some other changes going on that you don't want to commit, yet)</p>

<pre><code>git commit add /path/to/file
git commit --amend
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 7 '14 at 7:13
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-28173964">
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
<p>Existing answers are all talking about removing the unwanted files from the <strong><em>last</em></strong> commit.</p>

<p>If you want to remove unwanted files from an <strong><em>old</em></strong> commit (even pushed) and don't want to create a new commit, which is unnecessary, because of the action:</p>



<p>Find the commit that you want the file to conform to.</p>

<pre><code>git checkout &lt;commit_id&gt; &lt;path_to_file&gt;
</code></pre>

<p>you can do this multiple times if you want to remove many files.</p>



<pre><code>git commit -am "remove unwanted files"
</code></pre>



<p>Find the commit_id of the commit <strong>on which the files were added mistakenly</strong>, let's say "35c23c2" here</p>

<pre><code>git rebase 35c23c2~1 -i  // notice: "~1" is necessary
</code></pre>

<p>This command opens the editor according to your settings. The default one is vim.</p>

<p>Move the  last commit, which should be "remove unwanted files", to the next line of the incorrect commit("35c23c2" in our case), and set the command as <code>fixup</code>:</p>

<pre><code>pick 35c23c2 the first commit
fixup 0d78b28 remove unwanted files
</code></pre>

<p>You should be good after saving the file.</p>

<p>To finish : </p>

<pre><code>git push -f
</code></pre>

<p>If you unfortunately get conflicts, you have to solve them manually.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-30311679">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Using git GUI can simplify removing a file from the prior commit.</p>

<p>Assuming that this isn't a shared branch and you don't mind <a href="https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History" target="_blank">rewriting history</a>, then run:</p>

<pre><code>git gui citool --amend
</code></pre>

<p>You can un-check the file that was mistakenly committed and then click "Commit".</p>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/2t0XK.png" alt="enter image description here" /></div></p>

<p>The file is removed from the commit, but will be <em>kept on disk</em>.  So if you un-checked the file after mistakenly adding it, it will show in your untracked files list (and if you un-checked the file after mistakenly modifying it it will show in your changes not staged for commit list).</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-32501145">
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
<p>Do a sequence of the following commands:    </p>

<pre><code>//to remove the last commit, but preserve changes  
git reset --soft HEAD~1

//to remove unneded file from the staging area  
git reset HEAD `&lt;your file&gt;` 

//finally make a new commit  
git commit -m 'Your message'
</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-35570291">
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
<pre><code>git rm --cached &lt;file_to_remove_from_commit_&lt;commit_id&gt;_which_added_file&gt;
git commit -m "removed unwanted file from git"
</code></pre>

<p>will leave you the local file still. If you don't want the file locally either, you can skip the --cached option.</p>

<p>If all work is on your local branch, you need to keep the file in a later commit, and like having a clean history, I think a simpler way to do this could be:</p>

<pre><code>git rm --cached &lt;file_to_remove_from_commit_&lt;commit_id&gt;_which_added_file&gt;
git commit --squash &lt;commit_id&gt;
git add &lt;file_to_remove_from_commit_&lt;commit_id&gt;_which_added_file&gt;
git commit -m "brand new file!"
git rebase --interactive &lt;commit_id&gt;^
</code></pre>

<p>and you can then finish the rebase with ease without having to remember more complex commands or commit message or type as much.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-37333888">
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
<p>Actually, I think a quicker and easier way is to use git rebase interactive mode.</p>

<pre><code>git rebase -i head~1  
</code></pre>

<p>(or head~4, how ever far you want to go)</p>

<p>and then, instead of 'pick', use 'edit'.
I did not realize how powerful 'edit' is.</p>

<p><a href="https://www.youtube.com/watch?v=2dQosJaLN18" target="_blank">https://www.youtube.com/watch?v=2dQosJaLN18</a></p>

<p>Hope you will find it helpful.  </p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-37441508">
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
<p>Just wanted to complement the top answer as I had to run an extra command:</p>

<pre><code>git reset --soft HEAD^
git checkout origin/master &lt;filepath&gt;
</code></pre>

<p>Cheers!</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 25 '16 at 15:24
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-41799137">
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
<p>Had the same issue where I have changes in a local branch where I wanted to revert just one file. What worked for me was -</p>

<p><em>(<strong>feature/target_branch</strong> below is where I have all my changes including those I wanted to undo for a specific file)</em></p>

<p><em>(<strong>origin/feature/target_branch</strong> is the remote branch where I want to push my changes to)</em></p>

<p><em>(<strong>feature/staging</strong> is my temporary staging branch where I will be pushing from all my wanted changes excluding the change to that one file)</em></p>

<ol>
<li><p>Create a local branch from my <strong>origin/feature/target_branch</strong> - called it <strong>feature/staging</strong></p></li>
<li><p>Merged my working local branch <strong>feature/target_branch</strong>  to the <strong>feature/staging</strong> branch</p></li>
<li><p>Checked out <strong>feature/staging</strong> then <strong>git reset --soft ORIG_HEAD</strong> <em>(Now all changes from the feature/staging' will be staged but uncommitted.)</em></p></li>
<li><p>Unstaged the file which I have previously checked in with unnecessary changes</p></li>
<li><p>Changed the upstream branch for <strong>feature/staging</strong> to  <em>origin/feature/target_branch</em></p></li>
<li><p>Committed the rest of the staged changes and pushed upstream to my remote <em>origin/feature/target_branch</em></p></li>
</ol>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-42450337">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        47
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>As the accepted answer indicates, you can do this by resetting the entire commit. But this is a rather heavy handed approach.<br />
A cleaner way to do this would be to keep the commit, and simply remove the changed files from it.</p>

<pre><code>git reset HEAD^ -- path/to/file
git commit --amend --no-edit
</code></pre>

<p>The <code>git reset</code> will take the file as it was in the previous commit, and stage it in the index. The file in the working directory is untouched.<br />
The <code>git commit</code> will then commit and squash the index into the current commit.</p>

<p>This essentially takes the version of the file that was in the previous commit and adds it to the current commit. This results in no net change, and so the file is effectively removed from the commit.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-42795124">
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
<p>If you haven't yet pushed the commit, GitHub Desktop solves this problem easily:</p>

<ol>
<li>Choose Repository -&gt; Undo Most Recent Commit</li>
<li>Unselect the file that you mistakenly added. Your previous commit message will be in the dialog box already.</li>
<li>Press the Commit button!</li>
</ol>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 14 '17 at 19:41
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-45731879">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I will explain to you with example.<br />
Let A, B, C be 3 successive commits. Commit B contains a file that should not have been committed.</p>

<pre><code>git log  # take A commit_id
git rebase -i "A_commit_ID" # do an interactive rebase
change commit to 'e' in rebase vim # means commit will be edited
git rm unwanted_file
git rebase --continue
git push --force &lt;branchName&gt;   
</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-46478842">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>If you dont need that file anymore, you could do </p>

<pre><code>git rm file
git commit --amend
git push origin branch
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Sep 28 '17 at 21:49
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/git" title="show questions tagged 'git'" target="_blank">git</a> <a href="/questions/tagged/git-commit" title="show questions tagged 'git-commit'" target="_blank">git-commit</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
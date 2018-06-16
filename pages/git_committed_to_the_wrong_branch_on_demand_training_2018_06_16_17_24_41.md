<a href="https://services.github.com/on-demand/git-trouble/git-commit-wrong-branch">https://services.github.com/on-demand/git-trouble/git-commit-wrong-branch</a><div id="articleHeader"><h1>              Git Committed to the Wrong Branch!          </h1></div>
    
    
    
    <br /><br />

  
  




  
    
      


      
        
        
        
        

        
          <div>
            
              
<p>We have all been there, cruising along, making changes, making commits, and just as you are about to call it a night, you realize you just committed all of your changes to <code>master</code> and not that new branch you forgot to <code>checkout</code> to.</p>

<p>Fear not! You can salvage those changes and put them where they belong!</p>

<p>Keep in mind, all exercises expect you to have run the script to create files using the scripts found on the <a href="%7B%7Bsite.baseurl%7D%7D/git-set-up" target="_blank">Set Up Your Environment</a> page.</p>

            
          </div>

          
            
              <summary>I didn't push</summary>
              <hr />
              
              <p>The good news is, you didn’t push, so none of the collaborators on your project know you just committed a bunch of changes directly to <code>Master</code> on ‘accident’ (I mean, lets be serious, those changes are awesome and are definitely gonna get merged). Here is how we can fix that ‘mistake’.</p>

<ol>
  <li>Ensure you are on the branch you accidentally made those commits to. If you followed the ‘Setting Up Your Scenario Environment’ directions, you should have made a few commits to a branch named <code>test</code>.</li>
  <li>Enter: <code>git log --oneline</code> and identify the SHA-1 hash associated with the commit just before the first incorrect commit. In this case, let’s pretend file 5 was the first one that should have been on the other branch.</li>
  <li>Enter: <code>git reset --mixed SHA-1</code>, where <code>SHA-1</code> is the SHA-1 associated with the <strong>adding file 4</strong> commit.</li>
  <li>Enter: <code>git status</code>. You should see files 5 and 6 in your working directory.</li>
  <li>Enter: <code>git checkout -b correct</code>. This will create a new branch named <code>correct</code> and check you out to that branch.</li>
  <li>Enter: <code>git status</code>. Files 5 and 6 should still be in your working directory.</li>
  <li>Add both File 5 and File 6 by entering: <code>git add file* </code>.</li>
  <li>Enter: <code>git status</code>. File 5 and 6 should now be in the staging area waiting to be committed.</li>
  <li>Enter <code>git commit -m "Adding file 5 and 6"</code>.</li>
</ol>

<p>Congratulations, you just removed the commits you made to the incorrect branch and added them to the correct branch!</p>

<p>P.S. Next time, try to remember to run a quick <code>git checkout BRANCH</code> before you get working on that sweet new feature <img src="https://assets-cdn.github.com/images/icons/emoji/unicode/1f609.png" width="20" height="20" alt=":wink:" title=":wink:" />.</p>

              
            
          

          
            
              <summary>I pushed</summary>
              <hr />
              
              <h2 id="first-things-first-fix-master">First Things First: Fix Master</h2>

<p>Since this usually happens on <code>master</code>, the first thing you probably need to do is get those untested, unapproved commits out of master.</p>

<ol>
  <li>While on <code>master</code> enter: <code>git log --oneline</code>. Identify the SHA-1 hash for the commits that should be removed. In this case, let’s use the <strong>adding file 3</strong> commit.</li>
  <li>Enter: <code>git revert SHA-1</code>, where SHA-1 is the hash for the <strong>adding file 3</strong> commit. You can revert multiple commits in the same operation by adding a list of SHA-1’s with a space between each one.</li>
  <li>You can modify the revert commit message(s) if you would like or just close the editor.</li>
  <li>Use <code>git push</code> to send the changes to the remote.</li>
</ol>

<h2 id="rebuilding-the-branch">Rebuilding the Branch</h2>

<p>Now that <code>master</code> is safe, let’s create a new branch and grab those commits.</p>

<ol>
  <li>Create a new branch with: <code>git checkout -b BRANCH-NAME</code>(or check out to one you had already created).</li>
  <li>Enter <code>git reflog</code> to identify the SHA-1 hash for the commits you need to rescue.</li>
  <li>Enter: <code>git cherry-pick SHA-1</code>, where SHA-1 is the hash for the commit you want to place on the branch. You can cherry pick multiple commits by adding multiple SHA-1s separated by a space.</li>
  <li>Push your new branch to the remote with: <code>git push -u origin BRANCH-NAME</code>
</li>
</ol>

              
            
          

          

          

          

          
            
              <summary>Tell me why</summary>
              <hr />
              
              




































              
            
          

          

          
            <a href="/on-demand/git-trouble/git-scenarios" target="_blank">Continue</a>
          
          

          

        
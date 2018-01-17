<a href="https://github.com/nodegit/nodegit/issues/341">https://github.com/nodegit/nodegit/issues/341</a><div id="articleHeader"><h1>              Needed pull example or help with code            #341    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/Yezior" target="_blank">Yezior</a>  opened this Issue
        <relative-time>on Jan 12, 2015</relative-time>
        · 8 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        
          

  
  

    





      
  

    



    
      

  
    
      
          
<p>Firstly, thanks for good work.</p>
<h5>Is there a chance to provide by you PULL example (git fetch followed by git merge FETCH_HEAD) or can you help me how should I change below code to achieve "git merge FETCH_HEAD"?</h5>
<p>I used your fetch example and it worked, my repo is in this stage:</p>
<p>"Your branch is behind 'origin/master' by 1 commit, and can be fast-forwarded.<br />
nothing to commit, working directory clean"</p>
<p>I won't have any changes in repository in future and don't have now, so I'm looking for method that won't create commit and won't force me to push 'merge commit'.<br />
I was trying to modify your merge-cleanly example, but it creates commit, so it's not perfect for me (BTW don't know if this correct, because source tree shows history strange, maybe something with date of commit 1973-11-29)</p>
<div><pre>    var repo;
    var localReference, ourCommit;
    var remoteReference, theirCommit;
    var ourSignature = nodegit.Signature.create("user test", "user@test.com", 123456789, 60);

    Repository.open("master")
        .then(function(repository) {
            repo = repository;
            return repo.getReference('refs/remotes/origin/master');
        }).then(function(reference) {
            console.log(reference.target());
            remoteReference = reference;
            return repo.getReference('refs/heads/master');
        }).then(function(reference) {
            console.log(reference.target());
            localReference = reference;
            return repo.getCommit(localReference.target());
        }).then(function(commit) {
            ourCommit = commit;
            return repo.getCommit(remoteReference.target());
        }).then(function(commit) {
            theirCommit = commit;
            return Merge.commits(repo, ourCommit, theirCommit);
        }).then(function(index) {
            if (!index.hasConflicts()) {
                index.write();
                return index.writeTreeTo(repo);
            }
        }).then(function(oid) {
            return repo.createCommit('refs/heads/master', ourSignature, ourSignature, 'we merged their commit', oid, [ourCommit, theirCommit]);
        })
        .done(function(commitId) {
            console.log('New Commit: ', commitId);
            console.log("It worked!");
        },
        function() {
            console.log("It failed :( !");
        });</pre></div>
<p>Thanks</p>
      
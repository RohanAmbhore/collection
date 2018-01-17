<a href="http://radek.io/2015/10/27/nodegit/">http://radek.io/2015/10/27/nodegit/</a><div id="articleHeader"><h1>Manipulating git repositories with Node.js</h1></div>




    
    
        <time>27 Oct 2015</time>
        
    
        
            <p>What do linting, building and testing have in common? They all work best when
automated. With services like <a href="https://developer.github.com/webhooks/" target="_blank">GitHub’s
webhooks</a>, it’s easy to subscribe to
certain events on your repository and be notified by a HTTP request. These
might be commits being pushed or pull request landing at your repo when you
  can trigger a build or run your tests.</p>

<p>Apart from a webhook, you’ll need a server that will listen at the other end to
make it work. <a href="https://nodejs.org/en/" target="_blank">Node.js</a> with
<a href="http://expressjs.com/" target="_blank">Express</a> are pretty good at handling requests and you
can have them up an running in minutes. What’s left is processing the
repository itself.</p>

<p>This post is about how to do that with Node.</p>

<h2 id="meet-nodegit">Meet nodegit</h2>

<p>A <a href="https://www.npmjs.com/search?q=git" target="_blank">quick search</a> through npm reveals no
shortage of packages that provide access to the functionality of git in
Javascript either by wrapping around the <code>git</code> binary or implementing the
functionality directly.</p>

<p>The one that caught my eye is <a href="http://www.nodegit.org/" target="_blank">nodegit</a> — native
bindings to the <a href="https://libgit2.github.com/" target="_blank">libgit2</a> library made by GitHub.
The package gets lots of development activity and seems to be well supported.</p>

<p>You can install it as any other Node.js package using npm:</p>

<figure><pre><code>$ npm install nodegit</code></pre></figure>

<p>The maintainers provide pre-built binaries of libgit2 for the most common
architectures. However, if yours isn’t amongst them, the installer might need
to build the library from source and you’ll be required to install a C
toolchain to proceed.</p>

<p>Done installing? Let’s take a look at a few examples. There’s quite literally a
million things you can do with nodegit, and while this post can’t
possibly cover everything, we’ll go though a few to give you an idea of how
the library works.</p>

<p>All the snippets below were made with nodegit 0.5.0. When in doubt, please
refer to the <a href="http://www.nodegit.org/api/" target="_blank">official API docs</a>.</p>

<h2 id="clone-a-repo">Clone a repo</h2>

<p>The first step is pretty obvious: you can hardly do anything with the
repository without cloning it first. To do that, we’ll use the <a href="http://www.nodegit.org/api/clone/#clone" target="_blank">Clone
class</a>:</p>

<figure><pre><code>var nodegit = require('nodegit'),
    path = require('path');

var url = "https://github.com/pazdera/scriptster.git",
    local = "./scriptster",
    cloneOpts = {};

nodegit.Clone(url, local, cloneOpts).then(function (repo) {
    console.log("Cloned " + path.basename(url) + " to " + repo.workdir());
}).catch(function (err) {
    console.log(err);
});</code></pre></figure>

<p>Cloning will return an already initialised handle to the repository (an
instance of the <a href="http://www.nodegit.org/api/repository/" target="_blank">Repository</a> class)
that you can use to access its contents.</p>

<p>The library uses promises to manage the asynchronous calls. If you’re unsure
what the weird chain of <code>.then()</code> and <code>.catch()</code> functions mean, checkout this
<a href="https://www.promisejs.org/" target="_blank">quick introduction</a>.</p>

<h3 id="authentication">Authentication</h3>

<p>In case your repository isn’t openly available, you may need to authenticate
via http or ssh. Nodegit can do that via
<a href="http://www.nodegit.org/api/clone_options/" target="_blank">CloneOptions</a> that you can pass to
<code>Clone</code> as an argument. Like this:</p>

<figure><pre><code>var cloneOpts = {
  fetchOpts: {
    callbacks: {
      credentials: function(url, userName) {
        return nodegit.Cred.sshKeyNew(
          userName,
          '/Users/radek/.ssh/id_rsa.pub',
          '/Users/radek/.ssh/id_rsa',
          "&lt;your-passphrase-here&gt;");
      }
    }
  }
};</code></pre></figure>

<p>The <code>credentials</code> function is called when the remote requests authentication.
The implementation will vary for http, ssh and other types of authentication.
Check out the <a href="http://www.nodegit.org/api/cred/" target="_blank">Cred</a> class in the docs for
more ways to authenticate.</p>

<h2 id="open-it-up">Open it up</h2>

<p>If you already have a local copy of the repo, you can open it with nodegit
using the <a href="http://www.nodegit.org/api/repository/#open" target="_blank">Reposiotory#open</a>
function:</p>

<figure><pre><code>var nodegit = require('nodegit');

nodegit.Repository.open('./scriptster').then(function(repo) {
  console.log("Using " + repo.path());
}).catch(function (err) {
  console.log(err);
});</code></pre></figure>

<p>Just as <code>Clone</code>, it returns an instance of <code>Repository</code> that you can use to
manipulate it.</p>

<h2 id="read-the-commit-history">Read the commit history</h2>

<p>One thing that you may need is going through the last few commits on a branch
and extracting metadata from each one. This can be done through the
<a href="http://www.nodegit.org/api/commit/#history" target="_blank">Commit#history</a> event emitter that
iterates through the revisions, generates events for each commit along the way
and returns an array of all the <a href="http://www.nodegit.org/api/commit/" target="_blank">Commit
objects</a> at the end.</p>

<p>The following promise chain will retrieve the name of the current branch, walk
through its history and print the hash and commit messages for the last 10
commits on it:</p>

<figure><pre><code>var nodegit = require('nodegit');
var Promise = require('promise');

nodegit.Repository.open('./scriptster').then(function(repo) {
  /* Get the current branch. */
  return repo.getCurrentBranch().then(function(ref) {
    console.log("On " + ref.shorthand() + " (" + ref.target() + ")");

    /* Get the commit that the branch points at. */
    return repo.getBranchCommit(ref.shorthand());
  }).then(function (commit) {
    /* Set up the event emitter and a promise to resolve when it finishes up. */
    var hist = commit.history(),
        p = new Promise(function(resolve, reject) {
            hist.on("end", resolve);
            hist.on("error", reject);
        });
    hist.start();
    return p;
  }).then(function (commits) {
    /* Iterate through the last 10 commits of the history. */
    for (var i = 0; i &lt; 10; i++) {
      var sha = commits[i].sha().substr(0,7),
          msg = commits[i].message().split('\n')[0];
      console.log(sha + " " + msg);
    }
  });
}).catch(function (err) {
  console.log(err);
}).done(function () {
  console.log('Finished');
});</code></pre></figure>

<p>Here’s the output in the terminal:</p>

<figure>
    <a href="/assets/images/posts/nodegit/commits.png" target="_blank" class="readableLinkWithLargeImage">
        <div class="readableLargeImageContainer"><img src="/assets/images/posts/nodegit/commits.png" alt="nodegit: Listing commits" /></div>
    </a>
    <figcaption>
        <strong>nodegit</strong>: Listing the last 10 commits on a branch.
    </figcaption>
</figure>

<h2 id="checkout-a-different-branch">Checkout a different branch</h2>

<p>Besides manipulating metadata, <code>nodegit</code> has no problems working with trees.
You can check out different branches, modify your files and even create new
commits. For the sake of keeping the examples simple, this is how you checkout
a branch:</p>

<figure><pre><code>var nodegit = require('nodegit');

nodegit.Repository.open('./scriptster').then(function(repo) {
  return repo.getCurrentBranch().then(function(ref) {
    console.log("On " + ref.shorthand() + " " + ref.target());

    console.log("Checking out master");
    var checkoutOpts = {
      checkoutStrategy: nodegit.Checkout.STRATEGY.FORCE
    };
    return repo.checkoutBranch("master", checkoutOpts);
  }).then(function () {
    return repo.getCurrentBranch().then(function(ref) {
      console.log("On " + ref.shorthand() + " " + ref.target());
    });
  });
}).catch(function (err) {
  console.log(err);
}).done(function () {
  console.log('Finished');
});</code></pre></figure>

<p>All the work here is done by the
<a href="http://www.nodegit.org/api/repository/#checkoutBranch" target="_blank">Repository#checkoutBranch</a>
function, the rest is just printing the name of the current branch before and
after the checkout.</p>

<p>Note that you need to specify a preferred <a href="http://www.nodegit.org/api/checkout/#STRATEGY" target="_blank">checkout
strategy</a>. I picked <code>FORCE</code>
which will ditch any local modifications of the working tree in favour of the
version from the repository.</p>

<p>The output of the above should look something like this:</p>

<figure>
    <a href="/assets/images/posts/nodegit/checkout.png" target="_blank" class="readableLinkWithLargeImage">
        <div class="readableLargeImageContainer"><img src="/assets/images/posts/nodegit/checkout.png" alt="nodegit: Checkout a different branch" /></div>
    </a>
    <figcaption>
        <strong>nodegit</strong>: Checking out a different branch.
    </figcaption>
</figure>

<h2 id="search-through-the-tree">Search through the tree</h2>

<p>When you clone a repository with <code>nodegit</code>, it will look exactly the same as if
you did it with the <code>git</code> command and you can read and modify the working tree
as you wish.</p>

<p>Here’s an example that will print all the files from the
<a href="https://github.com/pazdera/scriptster" target="_blank">scriptster</a> repo that I cloned earlier:</p>

<figure><pre><code>var rr = require("recursive-readdir");

rr("./scriptster", ["scriptster/.git/**"], function (err, files) {
  for (var i = 0; i &lt; files.length; i++) {
    console.log(files[i]);
  }
});</code></pre></figure>

<p>For simplicity, it uses the
<a href="https://www.npmjs.com/package/recursive-readdir" target="_blank">recursive-readdir</a> module
from npm and ignores all the files within the <code>.git/</code> directory. Here’s the
output:</p>

<figure>
    <a href="/assets/images/posts/nodegit/files.png" target="_blank" class="readableLinkWithLargeImage">
        <div class="readableLargeImageContainer"><img src="/assets/images/posts/nodegit/files.png" alt="Reading the working tree" /></div>
    </a>
    <figcaption>
        Iterating through the contents of the working tree.
    </figcaption>
</figure>

<h2 id="summary">Summary</h2>

<p>This was <a href="https://github.com/nodegit/nodegit" target="_blank">nodegit</a>, a useful library if you
need to manipulate git repositories with Node.js. Under the hood, its calling
GitHub’s <a href="https://libgit2.github.com/" target="_blank">libgit2</a> to do the heavy lifting. It
works particularly well if you need to automate various parts of your workflow
— like building, testing and deployment using git on your server.</p>

<p>It’s open-source, distributed under the MIT licence (libgit2 is
licensed under GPLv2). Do get in touch with the
<a href="https://github.com/nodegit/nodegit#maintained-by" target="_blank">maintainers</a> if you’d like
to contribute!</p>

<p>If you liked the article, please give it a thumbs up on <a href="https://news.ycombinator.com/item?id=10457855" target="_blank">Hacker News</a> or
<a href="https://www.reddit.com/r/programming/comments/3qf1ne/manipulating_git_repositories_with_nodejs/" target="_blank">Reddit</a>. Thanks!</p>

        
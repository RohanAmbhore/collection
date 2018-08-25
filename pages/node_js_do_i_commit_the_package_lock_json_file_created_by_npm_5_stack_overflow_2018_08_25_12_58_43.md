<a href="https://stackoverflow.com/questions/44206782/do-i-commit-the-package-lock-json-file-created-by-npm-5">https://stackoverflow.com/questions/44206782/do-i-commit-the-package-lock-json-file-created-by-npm-5</a><div id="articleHeader"><h1>Do I commit the package-lock.json file created by npm 5?</h1></div>

            

<div id="question">

    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        588
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>93</b></div>



</div>

            </div>

            
<div>
    <div>

<p><a href="http://blog.npmjs.org/post/161081169345/v500" target="_blank">npm 5 was released today</a> and one of the new features include deterministic installs with the creation of a <code>package-lock.json</code> file.</p>

<p>Is this file supposed to be kept in source control?</p>

<p>I'm assuming it's similar to <a href="https://stackoverflow.com/questions/39990017/should-i-commit-the-yarn-lock-file-and-what-is-it-for" target="_blank"><code>yarn.lock</code></a> and <a href="https://stackoverflow.com/questions/12896780/should-composer-lock-be-committed-to-version-control" target="_blank"><code>composer.lock</code></a>, both of which are supposed to be kept in source control. </p>
    </div>
    
    <div>
    

    <div>
<div>
    <div>
        asked May 26 '17 at 17:03
    </div>
    
    
</div>

    </div>
    </div>
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-44210813">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        713
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted


</div>

            </div>
            


<div>
    <div>
<p>Yes, <code>package-lock.json</code> is intended to be checked into source control. If you're using npm 5, you may see this on the command line: <code>created a lockfile as package-lock.json. You should commit this file.</code> According to <a href="https://github.com/npm/npm/blob/v5.0.0/doc/files/package-lock.json.md" target="_blank"><code>npm help package-lock.json</code></a>:</p>

<blockquote>
  <p><code>package-lock.json</code> is automatically generated for any operations where npm
  modifies either the <code>node_modules</code> tree, or <code>package.json</code>. It describes the
  exact tree that was generated, such that subsequent installs are able to
  generate identical trees, regardless of intermediate dependency updates.</p>
  
  <p><strong>This file is intended to be committed into source repositories</strong>, and serves
  various purposes:</p>
  
  <ul>
  <li><p>Describe a single representation of a dependency tree such that teammates, deployments, and continuous integration are guaranteed to install exactly the same dependencies.</p></li>
  <li><p>Provide a facility for users to "time-travel" to previous states of <code>node_modules</code> without having to commit the directory itself.</p></li>
  <li><p>To facilitate greater visibility of tree changes through readable source control diffs.</p></li>
  <li><p>And optimize the installation process by allowing npm to skip repeated metadata resolutions for previously-installed packages.</p></li>
  </ul>
  
  <p>One key detail about <code>package-lock.json</code> is that it cannot be published, and it
  will be ignored if found in any place other than the toplevel package. It shares
  a format with npm-shrinkwrap.json(5), which is essentially the same file, but
  allows publication. This is not recommended unless deploying a CLI tool or
  otherwise using the publication process for producing production packages.</p>
  
  <p>If both <code>package-lock.json</code> and <code>npm-shrinkwrap.json</code> are present in the root of
  a package, <code>package-lock.json</code> will be completely ignored.</p>
</blockquote>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-51308761">
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
<p>I don't commit this file in my projects. What's the point ?</p>

<ol>
<li>It's generated</li>
<li>It's the cause of a SHA1 code integrity err in gitlab with gitlab-ci.yml builds</li>
</ol>

<p>Though it's true that i never use ^ in my package.json for libs because I had bad experiences with it :)</p>

<p>Regards.</p>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered Jul 12 at 14:53
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-50868690">
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
<p><strong>Yes, the best practice is to check in</strong></p>

<p>I agree that it will cause a lot of noise or conflict when seeing the diff. But the benefits are:</p>

<ol>
<li><strong>guarantee exact same version of every package</strong>. This is most the important when building in different environments in a different time. You may use <code>^1.2.3</code> in your <code>package.json</code>, but how can u ensure each time <code>npm install</code> will pick up same version in your dev machine and in the build server? Special those indirect dependency packages. Well, <code>package-lock.json</code> will ensure that.</li>
<li>it improves the installation process</li>
<li>it helps with new audit feature <code>npm audit fix</code> (I think the audit feature is from npm version 6)</li>
</ol>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-50961985">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -1
        <a title="This answer is not useful" target="_blank">down vote</a>





</div>

            </div>
            


<div>
    <div>
<blockquote>
  <p>Note: First of all, I was not able to make the below suggested
  solution work but I feel that with more knowledge about subject we can
  make it work. Let me know if that helped you or my understanding
  about <code>npm-merge-driver</code> is wrong.</p>
</blockquote>

<p>As said by many here <code>it will cause a lot of noise or conflict</code>, in that case run:</p>

<pre><code>npx npm-merge-driver install -g</code></pre>



<pre><code>npx npm-merge-driver install
$ git merge my-conflicting-branch
npm WARN conflict A git conflict was detected in package-lock.json. Attempting to auto-resolve.

added 1 package in 0.077s
Auto-merging package-lock.json
Merge made by the 'recursive' strategy.
 package-lock.json | 6 +++---
 1 file changed, 3 insertions(+), 3 deletions(-)
$ git status
&lt;clean&gt;</code></pre>

<p>Check more on docs here: <a href="https://www.npmjs.com/package/npm-merge-driver" target="_blank">https://www.npmjs.com/package/npm-merge-driver</a></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-50982431">
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
<p>To the people complaining about the noise when doing git diff:</p>

<pre><code>git diff -- . ':(exclude)*package-lock.json'</code></pre>

<p>what I did was use an alias</p>

<pre><code>alias gd="git diff --ignore-all-space --ignore-space-at-eol --ignore-space-change --ignore-blank-lines -- . ':(exclude)*package-lock.json'"</code></pre>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered Jun 22 at 7:04
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-46600592">
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
<p>You can check the official docs: <a href="https://docs.npmjs.com/files/package-lock.json" target="_blank">https://docs.npmjs.com/files/package-lock.json</a></p>

<p>Yes, you can commit this file. <code>package-lock.json</code> is automatically generated for any operations where <code>npm</code> modifies either the <code>node_modules</code> tree, or <code>package.json</code>. It describes the exact tree that was generated, such that subsequent installs are able to generate identical trees, regardless of intermediate dependency updates.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-44598161">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        61
        <a title="This answer is not useful" target="_blank">down vote</a>





</div>

            </div>
            


<div>
    <div>
<p>Yes, it's intended to be checked in. I want to suggest that it gets its own unique commit. We find that it adds a lot of noise to our diffs.</p>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered Jun 16 '17 at 21:18
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/node.js" title="show questions tagged 'node.js'" target="_blank">node.js</a> <a href="/questions/tagged/git" title="show questions tagged 'git'" target="_blank">git</a> <a href="/questions/tagged/npm" title="show questions tagged 'npm'" target="_blank">npm</a> <a href="/questions/tagged/version-control" title="show questions tagged 'version-control'" target="_blank">version-control</a> <a href="/questions/tagged/lockfile" title="show questions tagged 'lockfile'" target="_blank">lockfile</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
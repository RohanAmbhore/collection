<a href="https://stackoverflow.com/questions/10312521/how-to-fetch-all-git-branches">https://stackoverflow.com/questions/10312521/how-to-fetch-all-git-branches</a><div id="articleHeader"><h1>How to fetch all git branches?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        757
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>266</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I cloned a git repository, which contains about 5 branches. However, when I do <code>git branch</code> I only see one of them:</p>

<pre><code>$ git branch
* master
</code></pre>

<p>I know that I can do <code>git branch -a</code> to see <strong>all</strong> the branches, but how would I pull all the branches locally so when I do <code>git branch</code>, it shows:</p>

<pre><code>$ git branch
* master
* staging
* etc...
</code></pre>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-10312521">
		        <table>
                    <tbody>



    <tr id="comment-16959132">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            
        </td>
    </tr>
    <tr id="comment-48849613">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This question shows how to get all branches after using the <code>--single-branch</code> setting when cloning: <a href="http://stackoverflow.com/questions/17714159/how-do-i-undo-a-single-branch-clone" title="how do i undo a single branch clone" target="_blank">stackoverflow.com/questions/17714159/…</a> (<code>git fetch --all</code> will never work if you've specified only one branch!)
                    – <a href="/users/266375/matthew-wilcoxson" title="2,177 reputation" target="_blank">Matthew Wilcoxson</a>
                <a href="#comment48849613_10312521" target="_blank">May 21 '15 at 17:10</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-56021175">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                You will not see that output ever because the asterisk represents the branch that is currently checkout out. Since you can only have one branch checked out at once, you can have only one asterisk on the left of your branch listing.
                    – <a href="/users/833208/robino" title="1,553 reputation" target="_blank">Robino</a>
                <a href="#comment56021175_10312521" target="_blank">Dec 7 '15 at 15:09</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-62396820">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                The top-ranked answer below misses the OP's intent. I recommend that you look at <a href="http://stackoverflow.com/a/72156/342839" target="_blank">stackoverflow.com/a/72156/342839</a> instead. <code>git checkout -b &lt;branch&gt;</code> seems like the most likely answer.
                    – <a href="/users/342839/reece" title="3,036 reputation" target="_blank">Reece</a>
                <a href="#comment62396820_10312521" target="_blank">May 25 '16 at 20:53</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-73127401">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I saw a lot of answers but none of them mentioned what I think is probably the easiest way to do what you want:  <code>git clone --bare &lt;repo url&gt; .git </code> (notice you need to add "--bare" and ".git" at the end to clone the repo as a "bare" repo), then <code>git config --bool core.bare false</code> (sets the "bare" flag to false), then <code>git reset --hard</code> (moves the HEAD to current HEAD on the repo). Now if you <code>git branch</code> you should see all branches from the repo you cloned.
                    – <a href="/users/3354501/gabriel-ferraz" title="157 reputation" target="_blank">Gabriel Ferraz</a>
                <a href="#comment73127401_10312521" target="_blank">Mar 25 '17 at 17:37</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-10312521">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>5</b> more comments</a>
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-10312587">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1018
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p><sup>I've written my answer some time ago and last downvote motivated me to update it with my later experience :-)</sup></p>

<p><sup>Edit: previous version of this answer created branches with 'origin' prefix, all pointing to master branch, instead of actual branches, and having problems with variable expansions. This has been fixed as per comments.</sup></p>

<p>You can fetch one branch from all remotes like this:</p>

<pre><code>git fetch --all
</code></pre>

<p><code>fetch</code> updates local copies of remote branches so this is always safe for your local branches <strong>BUT</strong>:</p>

<ol>
<li><p><code>fetch</code> will not <strong>update</strong> local branches (which <strong>track</strong> remote branches); If you want to update your local branches you still need to pull every branch. </p></li>
<li><p><code>fetch</code> will not <strong>create</strong> local branches (which <strong>track</strong> remote branches), you have to do this manually. If you want to list all remote branches:
<code>git branch -a</code></p></li>
</ol>

<p>To <strong>update</strong> local branches which track remote branches:</p>

<pre><code>git pull --all
</code></pre>

<p>However, this can be still insufficient. It will work only for your local branches which track remote branches. To track all remote branches execute this oneliner <strong>BEFORE</strong> <code>git pull --all</code>:</p>

<pre><code>git branch -r | grep -v '\-&gt;' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done
</code></pre>

<h3>TL;DR version</h3>

<pre><code>git branch -r | grep -v '\-&gt;' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done
git fetch --all
git pull --all
</code></pre>

<p>(it seems that pull fetches all branches from all remotes, but I always fetch first just to be sure)</p>

<p>Run the first command only if there are remote branches on the server that aren't tracked by your local branches.</p>

<p>P.S. AFAIK <code>git fetch --all</code> and <code>git remote update</code> are equivalent.</p>

<hr /><p>Kamil Szot's <a href="https://stackoverflow.com/questions/10312521/how-to-fetch-all-git-branches#comment27984640_10312587" target="_blank">comment</a>, which 74 (at least) people found useful.</p>

<blockquote>
  <p>I had to use:</p>

<pre><code>for remote in `git branch -r`; do git branch --track ${remote#origin/} $remote; done
</code></pre>
  
  <p>because your code created local branches named <code>origin/branchname</code> and
  I was getting "refname 'origin/branchname' is ambiguous whenever I
  referred to it.</p>
</blockquote>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-10312587">
		        <table>
                    <tbody>



    <tr id="comment-13281266">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                27
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Sorry.  I can't imagine that this is what the OP actually wants.  The 'pull' command is 'fetch+merge' and the merge part will overlay all the branches on top of one another - leaving one giant mess.
                    – <a href="/users/1286639/gozoner" title="41,349 reputation" target="_blank">GoZoner</a>
                <a href="#comment13281266_10312587" target="_blank">Apr 25 '12 at 14:06</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-17621952">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                6
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                that fetch wouldn't create a new remote branch you still need to check it out with <code>git checkout -b localname remotename/remotebranch</code>
                    – <a href="/users/697012/learath2" title="7,454 reputation" target="_blank">Learath2</a>
                <a href="#comment17621952_10312587" target="_blank">Oct 20 '12 at 17:06</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-27984640">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                85
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I had to use      <code>for remote in `git branch -r`; do git branch --track ${remote#origin/} $remote; done</code>   because your code created local branches named origin/branchname and I was getting "refname 'origin/branchname' is ambiguous whenever I referred to it.
                    – <a href="/users/166921/kamil-szot" title="9,759 reputation" target="_blank">Kamil Szot</a>
                <a href="#comment27984640_10312587" target="_blank">Sep 22 '13 at 23:46</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-28201931">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                16
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I don't know if I'm using a different version of GIT, but I had to amend the script to <code>git pull --all; for remote in `git branch -r | grep -v \&gt;`; do git branch --track ${remote#origin/} $remote; done</code>. The change strips out HEAD.
                    – <a href="/users/110010/kim3er" title="4,102 reputation" target="_blank">kim3er</a>
                <a href="#comment28201931_10312587" target="_blank">Sep 29 '13 at 13:16</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-30998873">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                13
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                For the Windows folks: <code>for /F %remote in ('git branch -r') do ( git branch --track %remote) && git fetch --all && git pull --all</code>
                    – <a href="/users/205813/max" title="616 reputation" target="_blank">Max</a>
                <a href="#comment30998873_10312587" target="_blank">Dec 20 '13 at 6:03</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-10312587">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>19</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-39985786">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        13
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>You can fetch all the branches by:</p>

<pre><code>git fetch --all
</code></pre>



<pre><code>git fetch origin --depth=10000 $(git ls-remote -h -t origin)
</code></pre>

<p><sup>The <code>--depth=10000</code> parameter may help if you've shallowed repository.</sup></p>

<hr />

<p>To pull all the branches, use:</p>

<pre><code>git pull --all
</code></pre>

<hr />

<p>If above won't work, then precede the above command with:</p>

<pre><code>git config remote.origin.fetch '+refs/heads/*:refs/remotes/origin/*'
</code></pre>

<p>as the <code>remote.origin.fetch</code> could support only a specific branch while fetching, especially when you cloned your repo with <code>--single-branch</code>. Check this by: <code>git config remote.origin.fetch</code>.</p>

<p>After that you should be able to checkout any branch.</p>

<p>See also:</p>



<hr />

<p>To push all the branches to the remote, use:</p>

<pre><code>git push --all
</code></pre>

<p>eventually <code>--mirror</code> to mirror all refs.</p>

<hr />

<p>If your goal is to duplicate a repository, see: <a href="https://help.github.com/articles/duplicating-a-repository/" target="_blank">Duplicating a repository</a> article at GitHub.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-39985786">
		        <table>
                    <tbody>



    <tr id="comment-72446823">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Awesome...I tried everything else before your solution in this page. Thanks a lot!
                    – <a href="/users/2152791/sujoy" title="359 reputation" target="_blank">Sujoy</a>
                <a href="#comment72446823_39985786" target="_blank">Mar 7 '17 at 23:45</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-81773141">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I used shallow cloning (<code>depth=1</code>) and the config also specified one specific branch for <code>fetch</code> - the <code>depth=1000</code> parameter was the fix that helped me to checkout a specific remote branch
                    – <a href="/users/1875965/sandra" title="141 reputation" target="_blank">Sandra</a>
                <a href="#comment81773141_39985786" target="_blank">Nov 21 '17 at 9:47</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-39985786">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-10313379">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        289
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>To list remote branches:<br />
<code>git branch -r</code> </p>

<p>You can check them out as local branches with:<br />
<code>git checkout -b LocalName origin/remotebranchname</code></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-10313379">
		        <table>
                    <tbody>



    <tr id="comment-17600694">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                31
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This is exactly what I was looking for when I found the question above. I suspect many people looking for how to pull a remote branch definitely don't want to merge the branch into their current working copy, but they do want a local branch identical to the remote one.
                    – <a href="/users/319287/frug" title="308 reputation" target="_blank">Frug</a>
                <a href="#comment17600694_10313379" target="_blank">Oct 19 '12 at 16:03</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-42132936">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                9
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Even if the branch is not visible locally, I can do <code>git checkout remotebranchname</code>and it works. what's the difference with your solution?
                    – <a href="/users/2112538/fran%c3%a7ois-romain" title="3,403 reputation" target="_blank">François Romain</a>
                <a href="#comment42132936_10313379" target="_blank">Nov 6 '14 at 10:43</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-42434660">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                8
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Its default behaviour now. Wasn't the case on older git versions. Using <code>git checkout remotebranchname</code> used to just create a new <b>unrelated</b> branch that is named <i>remotebranchname</i>.
                    – <a href="/users/697012/learath2" title="7,454 reputation" target="_blank">Learath2</a>
                <a href="#comment42434660_10313379" target="_blank">Nov 15 '14 at 13:10</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-51138049">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                6
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                The accepted answer does something fundamentaly different and to be frank I don't even understand why its the accepted answer
                    – <a href="/users/697012/learath2" title="7,454 reputation" target="_blank">Learath2</a>
                <a href="#comment51138049_10313379" target="_blank">Jul 23 '15 at 16:28</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-64955628">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                4
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                The OP asked for all branches.  This answer only does one.
                    – <a href="/users/868121/ted-bigham" title="2,898 reputation" target="_blank">Ted Bigham</a>
                <a href="#comment64955628_10313379" target="_blank">Aug 5 '16 at 15:19</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-10313379">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>4</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-46295801">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Make sure all the remote branches are fetchable in <code>.git/config</code> file. </p>

<p>In this example, only the <code>origin/production</code> branch is fetchable, even if you try to do <code>git fetch --all</code> nothing will happen but fetching the <code>production</code> branch:</p>

<pre><code>[origin]
fetch = +refs/heads/production:refs/remotes/origin/production
</code></pre>

<p>This line should be replaced by:</p>

<pre><code>[origin]
fetch = +refs/heads/*:refs/remotes/origin/*
</code></pre>

<p>Then run <code>git fetch</code> etc...</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Sep 19 '17 at 8:43
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-46295801">
		        <table>
                    <tbody>



    <tr id="comment-79667665">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                To inspect:  <code>git config --get remote.origin.fetch</code> and then to (destructively) set it: <code>git config remote.origin.fetch '+refs/heads/*:refs/remotes/origin/*'</code>
                    – <a href="/users/468252/qneill" title="837 reputation" target="_blank">qneill</a>
                <a href="#comment79667665_46295801" target="_blank">Sep 21 '17 at 22:00</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-80847693">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                or modify config text file in .git directory, worked for me
                    – <a href="/users/1642418/fdim" title="1,412 reputation" target="_blank">FDIM</a>
                <a href="#comment80847693_46295801" target="_blank">Oct 26 '17 at 9:13</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-46295801">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-45123711">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>For Windows users using PowerShell:</p>

<pre><code>git branch -r | ForEach-Object {
    # Skip default branch, this script assumes
    # you already checked-out that branch when cloned the repo
    if (-not ($_ -match " -&gt; ")) {
        $localBranch = ($_ -replace "^.*/", "")
        $remoteBranch = $_.Trim()
        git branch --track "$localBranch" "$remoteBranch"
    }
}
git fetch --all
git pull --all
</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 15 '17 at 23:43
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-45123711">
		        <table>
                    <tbody>



    <tr id="comment-83010446">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                The command will ignore the branch which name with "/"
                    – <a href="/users/3634867/john-j" title="175 reputation" target="_blank">John_J</a>
                <a href="#comment83010446_45123711" target="_blank">2 days ago</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-45123711">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-21591209">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        10
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If you are here seeking a solution to get all branches and then migrate everything to another Git server, I put together the below process. If you just want to get all the branches updated locally, stop at the first empty line.</p>

<pre><code>git clone &lt;ORIGINAL_ORIGIN&gt;
git branch -r | awk -F'origin/' '!/HEAD|master/{print $2 " " $1"origin/"$2}' | xargs -L 1 git branch -f --track 
git fetch --all
git pull --all

git remote set-url origin &lt;NEW_ORIGIN&gt;
git pull
&lt;resolve_any_merge_conflicts&gt;
git push --all
git push --tags
&lt;check_NEW_ORIGIN_to_ensure_it_matches_ORIGINAL_ORIGIN&gt;
</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-21591209">
		        <table>
                    <tbody>



    <tr id="comment-35289548">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Very helpful; exactly what I needed. The only thing I had to change was in the second line, added single quotes around 'HEAD' and 'master'; probably because I'm using zsh. Thanks!
                    – <a href="/users/687840/sockmonk" title="3,379 reputation" target="_blank">sockmonk</a>
                <a href="#comment35289548_21591209" target="_blank">Apr 15 '14 at 16:10</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-55530055">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This is basically doing the following: (1) Obtaining the actual names of  remote branches [not head, not master]; (2) Completely telling Git to track them [not all solutions do this]; (3) Fetching and pulling everything from these branches [including tags]; (4) Setting a new origin and walking through pushing absolutely everything up. Again, most of the other solutions fail to move all pieces. This does it all.
                    – <a href="/users/325452/ingyhere" title="4,273 reputation" target="_blank">ingyhere</a>
                <a href="#comment55530055_21591209" target="_blank">Nov 23 '15 at 23:37</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-71112525">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I removed the antipattern of running grep then awk and condensed the grep commands into the awk command. Thanks <a href="http://stackoverflow.com/users/874188/tripleee" target="_blank">tripleee</a>!
                    – <a href="/users/325452/ingyhere" title="4,273 reputation" target="_blank">ingyhere</a>
                <a href="#comment71112525_21591209" target="_blank">Jan 31 '17 at 20:29</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-21591209">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-39658100">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I believe you have clone the repository by </p>

<pre><code>git clone https://github.com/pathOfrepository
</code></pre>

<p>now go to that folder using cd</p>

<pre><code>cd pathOfrepository
</code></pre>

<p>if you type <code>git status</code> </p>

<p>you can see all </p>

<pre><code>   On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
</code></pre>

<p>to see all hidden branch type </p>

<pre><code> git branch -a
</code></pre>

<p>it will list all the remote branch</p>

<p>now if you want to checkout on any particular branch just type </p>

<pre><code>git checkout -b localBranchName origin/RemteBranchName
</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Sep 23 '16 at 10:06
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-39658100">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-39248777">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<pre><code>git fetch --all
</code></pre>

<p>This will fetch all branches for you and then you can checkout to your desired branch through</p>

<pre><code>get checkout YOUR_BRANCH
</code></pre>

<p>Hope this helps.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-39248777">
		        <table>
                    <tbody>



    <tr id="comment-65835214">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Please edit with more information. Code-only and "try this" answers are discouraged, because they contain no searchable content, and don't explain why someone should "try this".
                    – <a href="/users/4579155/abarisone" title="2,716 reputation" target="_blank">abarisone</a>
                <a href="#comment65835214_39248777" target="_blank">Aug 31 '16 at 12:33</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-39248777">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-36744181">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<pre><code>git remote add origin https://yourBitbucketLink

git fetch origin

git checkout -b yourNewLocalBranchName origin/requiredRemoteBranch (use tab :D)
</code></pre>

<p>Now locally your <code>yourNewLocalBranchName</code> is your <code>requiredRemoteBranch</code>.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-36744181">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-38195213">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>We can put all branch or tag names in a temporary file, then do git pull for each name/tag:</p>

<pre><code>git branch -r | grep origin | grep -v HEAD| awk -F/ '{print $NF}' &gt; /tmp/all.txt
git tag -l &gt;&gt; /tmp/all.txt
for tag_or_branch in `cat /tmp/all.txt`; do git checkout $tag_or_branch; git pull origin $tag_or_branch; done
</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 5 '16 at 4:32
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-38195213">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-21189710">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        147
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Since the original answer <em>completely</em> misses the point and an edit was rejected, here a concise answer:</p>

<p>You will need to create local branches tracking remote branches.</p>

<p>Assuming that you've got only one remote called <code>origin</code>, this snippet will create local branches for all remote tracking ones:</p>

<pre><code>for b in `git branch -r | grep -v -- '-&gt;'`; do git branch --track ${b##origin/} $b; done
</code></pre>

<p>After that, <code>git fetch --all</code> will update all local copies of remote branches.</p>

<p>Also, <code>git pull --all</code> will update your local tracking branches, but depending on your local commits and how the 'merge' configure option is set it might create a merge commit, fast-forward or fail.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-21189710">
		        <table>
                    <tbody>



    <tr id="comment-51816500">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                4
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This robustifies the solution against branch names containing shell metacharacters (as per pinkeen's comment on the other answer), and avoids spurious error output: git branch -r | grep -v -- ' -&gt; ' | while read remote; do git branch --track "${remote#origin/}" "$remote" 2&gt;&1 | grep -v ' already exists'; done
                    – <a href="/users/393146/daira-hopwood" title="1,361 reputation" target="_blank">Daira Hopwood</a>
                <a href="#comment51816500_21189710" target="_blank">Aug 11 '15 at 23:28</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-64577751">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Are you sure that <code>git pull --all</code> will update all local tracking branches?  As far as I can tell it only updates the current branch from all remotes.
                    – <a href="/users/200224/andy" title="2,873 reputation" target="_blank">Andy</a>
                <a href="#comment64577751_21189710" target="_blank">Jul 26 '16 at 16:07</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-71513488">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Did this.  Local branches matching remote branches were not created.  What is the git command that simply says "pull all remote branches creating local ones if they do not exist?"
                    – <a href="/users/2326613/josephk" title="513 reputation" target="_blank">JosephK</a>
                <a href="#comment71513488_21189710" target="_blank">Feb 11 '17 at 10:47</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-21189710">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-24613312">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        19
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I usually use nothing else but commands like this:</p>

<pre><code>git fetch origin
git checkout --track origin/remote-branch
</code></pre>

<p>A little shorter version:</p>

<pre><code>git fetch origin
git checkout -t origin/remote-branch
</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-24613312">
		        <table>
                    <tbody>



    <tr id="comment-46702201">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                git fetch origin before checking out did the trick for me.
                    – <a href="/users/2615428/suraj" title="873 reputation" target="_blank">Suraj</a>
                <a href="#comment46702201_24613312" target="_blank">Mar 25 '15 at 6:30</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-24613312">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-24213098">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I wrote a little script to manage cloning a new repo and making local branches for all the remote branches.</p>

<p>You can find the latest version <a href="https://gist.github.com/tstone2077/8380f7862b00b6234963" target="_blank">here</a>:</p>

<pre><code>#!/bin/bash

# Clones as usual but creates local tracking branches for all remote branches.
# To use, copy this file into the same directory your git binaries are (git, git-flow, git-subtree, etc)

clone_output=$((git clone "$@" ) 2&gt;&1)
retval=$?
echo $clone_output
if [[ $retval != 0 ]] ; then
    exit 1
fi
pushd $(echo $clone_output | head -1 | sed 's/Cloning into .\(.*\).\.\.\./\1/') &gt; /dev/null 2&gt;&1
this_branch=$(git branch | sed 's/^..//')
for i in $(git branch -r | grep -v HEAD); do
  branch=$(echo $i | perl -pe 's/^.*?\///')
  # this doesn't have to be done for each branch, but that's how I did it.
  remote=$(echo $i | sed 's/\/.*//')
  if [[ "$this_branch" != "$branch" ]]; then
      git branch -t $branch $remote/$branch
  fi
done
popd &gt; /dev/null 2&gt;&1
</code></pre>

<p>To use it, just copy it into your git bin directory (for me, that’s <code>C:\Program Files (x86)\Git\bin\git-cloneall</code>), then, on the command line:</p>

<pre><code>git cloneall [standard-clone-options] &lt;url&gt;
</code></pre>

<p>It clones as usual, but creates local tracking branches for all remote branches.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-24213098">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-34122152">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        20
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>When you clone a repository all the information of the branches is actually downloaded but the branches are hidden. With the command</p>

<pre><code>$ git branch -a
</code></pre>

<p>you can show all the branches of the repository, and with the command</p>

<pre><code>$ git checkout -b branchname origin/branchname
</code></pre>

<p>you can then "download" them manually one at a time. </p>

<hr />

<p>However, there is a much cleaner and quicker way, though it's a bit complicated. You need three steps to accomplish this:</p>

<ol>
<li><p>First step</p>

<p>create a new empty folder on your machine and clone a mirror copy of the .git folder from the repository:</p>

<pre><code>$ cd ~/Desktop && mkdir my_repo_folder && cd my_repo_folder
$ git clone --mirror https://github.com/planetoftheweb/responsivebootstrap.git .git
</code></pre>

<p>the local repository inside the folder my_repo_folder is still empty, there is just a hidden .git folder now that you can see with a "ls -alt" command from the terminal.</p></li>
<li><p>Second step</p>

<p>switch this repository from an empty (bare) repository to a regular repository by switching the boolean value "bare" of the git configurations to false:</p>

<pre><code>$ git config --bool core.bare false
</code></pre></li>
<li><p>Third Step</p>

<p>Grab everything that inside the current folder and create all the branches on the local machine, therefore making this a normal repo. </p>

<pre><code>$ git reset --hard
</code></pre></li>
</ol>

<p>So now you can just type the command <code>git branch</code> and you can see that all the branches are downloaded. </p>

<p>This is the quick way in which you can clone a git repository with all the branches at once, but it's not something you wanna do for every single project in this way. </p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-34122152">
		        <table>
                    <tbody>



    <tr id="comment-75385831">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Upvoted for mention of hidden branches. helped me understand the local branch tracking immensely.
                    – <a href="/users/1492284/mburke05" title="386 reputation" target="_blank">mburke05</a>
                <a href="#comment75385831_34122152" target="_blank">May 25 '17 at 17:03</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-34122152">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-32239249">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Just those 3 commands will get all the branches</p>

<pre><code>git clone --mirror repo.git  .git     (gets just .git  - bare repository)

git config --bool core.bare false         

git reset --hard                  
</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-32239249">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-31188660">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Based on the answer by Learath2, here's what I did after doing <code>git clone [...]</code> and <code>cd</code>-ing into the created directory:</p>

<p><code>git branch -r | grep -v master | awk {print\$1} | sed 's/^origin\/\(.*\)$/\1 &/' | xargs -n2 git checkout -b</code></p>

<p>Worked for me but I can't know it'll work for you. Be careful.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 2 '15 at 15:23
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-31188660">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-21672555">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>After you clone the master repository, you just can execute</p>

<pre><code>git fetch && git checkout &lt;branchname&gt;
</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-21672555">
		        <table>
                    <tbody>



    <tr id="comment-53218984">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                simple. and worked to get a branch from remote origin
                    – <a href="/users/1434322/sirvon" title="1,269 reputation" target="_blank">sirvon</a>
                <a href="#comment53218984_21672555" target="_blank">Sep 21 '15 at 4:26</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-66423031">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Thanks a lot, this should be the correct answer.
                    – <a href="/users/3146509/reza" title="1,071 reputation" target="_blank">Reza</a>
                <a href="#comment66423031_21672555" target="_blank">Sep 18 '16 at 9:17</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-70039700">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This does not answer the original question: "How would I pull all the branches locally?" It is pulling them one-by-one, which isn't scalable. Consider the case of 100 branches.
                    – <a href="/users/325452/ingyhere" title="4,273 reputation" target="_blank">ingyhere</a>
                <a href="#comment70039700_21672555" target="_blank">Jan 1 '17 at 17:41</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-21672555">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-23547118">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        29
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>what about <code>git fetch && git checkout RemoteBranchName</code> ? works very well for me...</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered May 8 '14 at 16:14
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-23547118">
		        <table>
                    <tbody>



    <tr id="comment-37850121">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                5
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This is the new best answer, y'all. I don't know if maybe this wasn't possible before, but recent versions of Git at least will notice that you are trying to checkout a remote branch and will automatically set up the local tracking branch for you (and you don't need to specify <code>origin/branch</code>; it suffices to say only <code>branch</code>).
                    – <a href="/users/213525/neil-traft" title="10,753 reputation" target="_blank">Neil Traft</a>
                <a href="#comment37850121_23547118" target="_blank">Jun 27 '14 at 18:12</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-61117795">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Exactly what i wanted! Something simple!
                    – <a href="/users/1534242/maloo" title="168 reputation" target="_blank">maloo</a>
                <a href="#comment61117795_23547118" target="_blank">Apr 21 '16 at 12:53</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-70039670">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                4
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This does not answer the original question: "How would I pull all the branches locally?" It is pulling them one-by-one, which isn't scalable.
                    – <a href="/users/325452/ingyhere" title="4,273 reputation" target="_blank">ingyhere</a>
                <a href="#comment70039670_23547118" target="_blank">Jan 1 '17 at 17:39</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-74068475">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This was the only answer which allowed me to pull remote branches in every situation I've encountered
                    – <a href="/users/5522881/emmanuel-buckshi" title="189 reputation" target="_blank">Emmanuel Buckshi</a>
                <a href="#comment74068475_23547118" target="_blank">Apr 19 '17 at 22:07</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-23547118">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-20367335">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Looping didn't seem to work for me and I wanted to ignore origin/master.
Here's what worked for me.</p>

<pre><code>git branch -r | grep -v HEAD | awk -F'/' '{print $2 " " $1"/"$2}' | xargs -L 1 git branch -f --track
</code></pre>

<p>After that:</p>

<pre><code>git fetch --all
git pull --all
</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 4 '13 at 5:09
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-20367335">
		        <table>
                    <tbody>



    <tr id="comment-32618529">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                A variation of this is the correct answer, but this one does not work in all edge cases. Also, the branch names can be funky. So I did the following: git branch -r | grep -v HEAD | grep –v master | awk -F'origin/' '{print $2 " " $1"origin/"$2}' | xargs -L 1 git branch -f --track ; git fetch --all ; git pull --all ; AND THAT DID THE TRICK!
                    – <a href="/users/325452/ingyhere" title="4,273 reputation" target="_blank">ingyhere</a>
                <a href="#comment32618529_20367335" target="_blank">Feb 5 '14 at 23:49</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-55154576">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                A stylistic improvement to avoid the <code>grep | awk</code> <a href="http://www.iki.fi/era/unix/award.html#grep" target="_blank">antipattern</a>: <code>git branch -r | awk -F 'origin/' '!/HEAD|master/{</code> ...
                    – <a href="/users/874188/tripleee" title="71,698 reputation" target="_blank">tripleee</a>
                <a href="#comment55154576_20367335" target="_blank">Nov 13 '15 at 11:14</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-20367335">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-19644027">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        21
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>The bash for loop wasn't working for me, but this did exactly what I wanted. All the branches from my origin mirrored as the same name locally.</p>

<pre><code>git fetch origin '+refs/heads/*:refs/heads/*'
</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Oct 28 '13 at 20:02
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-19644027">
		        <table>
                    <tbody>



    <tr id="comment-47453334">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                That produces <code>fatal: Refusing to fetch into current branch refs/heads/master of non-bare repository</code> after a simple clone. Have to detach head first. I did this with <code>git checkout &lt;SHA&gt;</code>
                    – <a href="/users/621762/brannerchinese" title="696 reputation" target="_blank">brannerchinese</a>
                <a href="#comment47453334_19644027" target="_blank">Apr 15 '15 at 17:28</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-50251500">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                4
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                My Solution using this is <code>git checkout --detach # detach the head</code> and then <code>git fetch origin \'+refs/heads/*:refs/heads/* </code>
                    – <a href="/users/3939046/mike-dupont" title="53 reputation" target="_blank">Mike DuPont</a>
                <a href="#comment50251500_19644027" target="_blank">Jun 29 '15 at 15:09</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-58681255">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This one worked for me, except I also use the --tags parameter.  I wish there was a standard, simple front end for git, the number of simple things in git that need 10-plus stack overflow answers is ridiculous!
                    – <a href="/users/192221/kristianp" title="2,799 reputation" target="_blank">kristianp</a>
                <a href="#comment58681255_19644027" target="_blank">Feb 18 '16 at 23:13</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-61364845">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @kristianp Have you checked out Ungit or GitKraken?
                    – <a href="/users/3794873/dragon788" title="715 reputation" target="_blank">dragon788</a>
                <a href="#comment61364845_19644027" target="_blank">Apr 27 '16 at 20:33</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-61419312">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @dragon788 I've been using SourceTree for a git GUI, but I was really talking about a simpler command-line for scripting tasks.
                    – <a href="/users/192221/kristianp" title="2,799 reputation" target="_blank">kristianp</a>
                <a href="#comment61419312_19644027" target="_blank">Apr 29 '16 at 4:28</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-19644027">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>2</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-10317152">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        79
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If you do:</p>

<pre><code>git fetch origin
</code></pre>

<p>then they will be all there locally.  If you then perform:</p>

<pre><code>git branch -a
</code></pre>

<p>you'll see them listed as remotes/origin/branch-name.  Since they are there locally you can do whatever you please with them.  For example:</p>

<pre><code>git diff origin/branch-name 
</code></pre>



<pre><code>git merge origin/branch-name
</code></pre>



<pre><code>git checkout -b some-branch origin/branch-name
</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-10317152">
		        <table>
                    <tbody>



    <tr id="comment-22310351">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                5
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Just found this page on google... this was the actual type of answer I was seeking.  I tried the first command but received an error: [$ git fetch --all origin fatal: fetch --all does not take a repository argument] ---  Using "git fetch --all" seems to do the trick.  Thanks for the lead!
                    – <a href="/users/298758/longda" title="4,208 reputation" target="_blank">longda</a>
                <a href="#comment22310351_10317152" target="_blank">Mar 29 '13 at 18:26</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-22312615">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Fixed (eliminated <code>--all</code>)
                    – <a href="/users/1286639/gozoner" title="41,349 reputation" target="_blank">GoZoner</a>
                <a href="#comment22312615_10317152" target="_blank">Mar 29 '13 at 19:47</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-23164620">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                9
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                <code>git fetch -all</code> fetches all branches of all remotes.  <code>git fetch origin</code> fetches all branches of the remote <code>origin</code>.  The later is what the OP was asking.
                    – <a href="/users/1286639/gozoner" title="41,349 reputation" target="_blank">GoZoner</a>
                <a href="#comment23164620_10317152" target="_blank">Apr 24 '13 at 19:37</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-24387511">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                <code>--all</code> means "all remotes", not "all branches of a given remote". The latter is implied by any fetch from a remote.
                    – <a href="/users/839809/spacediver" title="1,175 reputation" target="_blank">spacediver</a>
                <a href="#comment24387511_10317152" target="_blank">Jun 3 '13 at 14:58</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-64955751">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                OP asked for a solution enabling "branch", not "branch -a".
                    – <a href="/users/868121/ted-bigham" title="2,898 reputation" target="_blank">Ted Bigham</a>
                <a href="#comment64955751_10317152" target="_blank">Aug 5 '16 at 15:22</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-10317152">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>2</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-10312552">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        40
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<pre><code>$ git remote update  
$ git pull --all
</code></pre>

<p>This assumes all branches are tracked</p>

<p>if they aren't you can fire this in bash </p>

<pre><code>for remote in `git branch -r `; do git branch --track $remote; done
</code></pre>

<p>Then run the command.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-10312552">
		        <table>
                    <tbody>



    <tr id="comment-13274033">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                When I try that I still get the same result as above.
                    – <a href="/users/651174/david542" title="26,278 reputation" target="_blank">David542</a>
                <a href="#comment13274033_10312552" target="_blank">Apr 25 '12 at 9:10</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-19632217">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                last one worked for me.. with a few git errors
                    – <a href="/users/304735/jacob-lowe" title="500 reputation" target="_blank">Jacob Lowe</a>
                <a href="#comment19632217_10312552" target="_blank">Jan 5 '13 at 5:52</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-38633016">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Same as @JacobLowe, I got the error, but it worked anyway; 'fatal: A branch named 'origin/master' already exists.'
                    – <a href="/users/242110/annetheagile" title="5,717 reputation" target="_blank">AnneTheAgile</a>
                <a href="#comment38633016_10312552" target="_blank">Jul 21 '14 at 20:15</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-10312552">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/git" title="show questions tagged 'git'" target="_blank">git</a> <a href="/questions/tagged/branch" title="show questions tagged 'branch'" target="_blank">branch</a> <a href="/questions/tagged/git-branch" title="show questions tagged 'git-branch'" target="_blank">git-branch</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
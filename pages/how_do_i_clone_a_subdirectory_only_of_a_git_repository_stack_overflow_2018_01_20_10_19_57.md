<a href="https://stackoverflow.com/questions/600079/how-do-i-clone-a-subdirectory-only-of-a-git-repository/13738951#13738951">https://stackoverflow.com/questions/600079/how-do-i-clone-a-subdirectory-only-of-a-git-repository/13738951#13738951</a><div id="articleHeader"><h1>How do I clone a subdirectory only of a Git repository?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        882
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>375</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I have my Git repository which, at the root, has two sub directories:</p>

<pre><code>/finisht
/static
</code></pre>

<p>When this was in <a href="http://en.wikipedia.org/wiki/Apache_Subversion" target="_blank">SVN</a>, <code>/finisht</code> was checked out in one place, while <code>/static</code> was checked out elsewhere, like so:</p>

<pre><code>svn co svn+ssh://admin@domain.com/home/admin/repos/finisht/static static
</code></pre>

<p>Is there a way to do this with Git?</p>
    </div>
    
    
</div>
</td>
        </tr>
                    <tr>
            <td colspan="2">
                <div>
        <h2>                    <b>protected</b> by <a href="/users/1743880/tunaki" target="_blank">Tunaki</a> May 24 '16 at 22:30
</h2>
        <p>
This question is protected to prevent "thanks!", "me too!", or spam answers by new users. 
To answer it, you must have earned at least 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).</p>
    </div>
            </td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-600079">
		        <table>
                    <tbody>



    <tr id="comment-25379144">
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
            
        </td>
    </tr>
    <tr id="comment-41975136">
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
                For a 2014's user, what the <code>git clone</code> simplest command?? I used <a href="http://stackoverflow.com/a/2466755/287948" target="_blank">this <b>simple answer</b></a>. If there are something more simple, please comment
                    – <a href="/users/287948/peter-krauss" title="4,341 reputation" target="_blank">Peter Krauss</a>
                <a href="#comment41975136_600079" target="_blank">Nov 1 '14 at 12:00</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-46848013">
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
                For those trying to clone the contents of the repository (not creating the root folder), this is a very easy solution: <a href="http://stackoverflow.com/questions/6224626/github-clone-contents-of-a-repo-without-folder-itself" title="github clone contents of a repo without folder itself" target="_blank">stackoverflow.com/questions/6224626/…</a>
                    – <a href="/users/497126/marc" title="662 reputation" target="_blank">Marc</a>
                <a href="#comment46848013_600079" target="_blank">Mar 29 '15 at 12:38</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-54042785">
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
            
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-600079">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-600189">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        390
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p><strong>This answer is outdated and only apply to git versions lower than 1.7.0 (Feb. 2012). See below for newer versions.</strong></p>

<p>No, that's not possible in Git.</p>

<p>Implementing something like this in Git would be a substantial effort and it would mean that the integrity of the clientside repository could no longer be guaranteed. If you are interested, search for discussions on "sparse clone" and "sparse fetch" on the git mailinglist.</p>

<p>In general, the consensus in the Git community is that if you have several directories that are always checked out independently, then these are really two different projects and should live in two different repositories. You can glue them back together using <a href="http://Book.Git-SCM.Com/5_submodules.html" target="_blank">Git Submodules</a>.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-600189">
		        <table>
                    <tbody>



    <tr id="comment-1048547">
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
                Depending on the scenario, you may want to use git subtree instead of git submodule.  See <a href="http://alumnit.ca/~apenwarr/log/?m=200904#30" target="_blank">alumnit.ca/~apenwarr/log/?m=200904#30</a>
                    – <a href="/users/34990/c-pirate" title="451 reputation" target="_blank">C Pirate</a>
                <a href="#comment1048547_600189" target="_blank">Aug 3 '09 at 17:12</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-31969932">
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
                +0 Link is broken. I think you want <a href="http://git-scm.com/docs/git-submodule" target="_blank">this</a>.
                    – <a href="/users/2494012/mr-shtuffs" title="87 reputation" target="_blank">Mr. Shtuffs</a>
                <a href="#comment31969932_600189" target="_blank">Jan 20 '14 at 3:28</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-33750961">
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
                @StijndeWitt: Sparse checkouts happen during <code>git-read-tree</code>, which is long after <code>get-fetch</code>. The question was not about checking out only a subdirectory, it was about <i>cloning</i> only a subdirectory. I don't see how sparse checkouts could possibly do that, since <code>git-read-tree</code> runs after the clone has already completed.
                    – <a href="/users/2988/j%c3%b6rg-w-mittag" title="267,472 reputation" target="_blank">Jörg W Mittag</a>
                <a href="#comment33750961_600189" target="_blank">Mar 6 '14 at 14:53</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-49073600">
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
                To help you show only the directory you want, you have to execute git read-tree -m -u HEAD
                    – <a href="/users/2436398/jackxu" title="333 reputation" target="_blank">JackXu</a>
                <a href="#comment49073600_600189" target="_blank">May 28 '15 at 6:08</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-78563810">
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
                Rather than this "stub", would you like for me to delete this answer so Chronial's can float to the top? You can't delete it yourself, because it's accepted, but a moderator can. You would keep the reputation you've earned from it, since it's so old. (I came across this because someone flagged it as "link-only". :-)
                    – <a href="/users/366904/cody-gray" title="177,161 reputation" target="_blank">Cody Gray♦</a>
                <a href="#comment78563810_600189" target="_blank">Aug 21 '17 at 17:49</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-600189">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-600540">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        56
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If you never plan to interact with the repository from which you cloned, you can do a full <strong>git clone</strong> and rewrite your repository using <strong>git filter-branch --subdirectory-filter</strong>. This way, at least the history will be preserved.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-600540">
		        <table>
                    <tbody>



    <tr id="comment-41765775">
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
                For people that doesn't know the command, it is <code>git filter-branch --subdirectory-filter &lt;subdirectory&gt;</code>
                    – <a href="/users/320594/jaime-hablutzel" title="3,654 reputation" target="_blank">Jaime Hablutzel</a>
                <a href="#comment41765775_600540" target="_blank">Oct 26 '14 at 14:32</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-43677259">
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
                This method has the advantage that the subdirectory you choose becomes the root of the new repository, which happens to be exactly what I want.
                    – <a href="/users/937392/andrew-schulman" title="2,638 reputation" target="_blank">Andrew Schulman</a>
                <a href="#comment43677259_600540" target="_blank">Dec 23 '14 at 21:27</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-51370094">
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
                <code>git log --all</code> still shows all logs..
                    – <a href="/users/278405/cychoi" title="1,236 reputation" target="_blank">cychoi</a>
                <a href="#comment51370094_600540" target="_blank">Jul 30 '15 at 6:15</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-600540">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-2861204">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        61
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Git 1.7.0 has “sparse checkouts”. See 
“core.sparseCheckout” in the <a href="http://git-scm.com/docs/git-config" target="_blank"><em>git config</em> manpage</a>, 
“Sparse checkout” in the <a href="http://www.kernel.org/pub/software/scm/git/docs/git-read-tree.html#_sparse_checkout" target="_blank"><em>git read-tree</em> manpage</a>, and
“Skip-worktree bit” in the <a href="http://www.kernel.org/pub/software/scm/git/docs/git-update-index.html#_skip_worktree_bit" target="_blank"><em>git update-index</em> manpage</a>.</p>

<p>The interface is not as convenient as SVN’s (e.g. there is no way to make a sparse checkout at the time of an initial clone), but the base functionality upon which simpler interfaces could be built is now available.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-2861204">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-13738951">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1224
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>What you are trying to do is called a <strong>sparse checkout</strong>, and that feature was added in git 1.7.0 (Feb. 2012). The steps to do a sparse <em>clone</em> are as follows:</p>

<pre><code>mkdir &lt;repo&gt;
cd &lt;repo&gt;
git init
git remote add -f origin &lt;url&gt;
</code></pre>

<p>This creates an empty repository with your remote, and fetches all objects but doesn't check them out. Then do:</p>

<pre><code>git config core.sparseCheckout true
</code></pre>

<p>Now you need to define which files/folders you want to actually check out. This is done by listing them in <code>.git/info/sparse-checkout</code>, eg:</p>

<pre><code>echo "some/dir/" &gt;&gt; .git/info/sparse-checkout
echo "another/sub/tree" &gt;&gt; .git/info/sparse-checkout</code></pre>

<p>Last but not least, update your empty repo with the state from the remote:</p>

<pre><code>git pull origin master
</code></pre>

<p>You will now have files "checked out" for <code>some/dir</code> and <code>another/sub/tree</code> on your file system (with those paths still), and no other paths present.</p>

<p>You might want to have a look at the <a href="http://jasonkarns.com/blog/subdirectory-checkouts-with-git-sparse-checkout/" target="_blank">extended tutorial</a> and you should probably read the official <a href="http://schacon.github.com/git/git-read-tree.html#_sparse_checkout" target="_blank">documentation for sparse checkout</a>.</p>

<hr />

<p>Note that this will still download the whole repository from the server – only the checkout is reduced in size. At the moment it is not possible to clone only a single directory. But if you don't need the history of the repository, you can at least save on bandwidth by creating a shallow clone. See <a href="https://stackoverflow.com/a/28039894/962603" target="_blank">udondan's answer</a> below for information on how to combine shallow <a href="https://git-scm.com/docs/git-clone" target="_blank">clone</a> and sparse checkout.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-13738951">
		        <table>
                    <tbody>



    <tr id="comment-20933420">
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
                on Apple the '-f' perimeter does not work. just do git remote add origin &lt;url&gt;   without -f
                    – <a href="/users/1201015/anno2001" title="1,144 reputation" target="_blank">Anno2001</a>
                <a href="#comment20933420_13738951" target="_blank">Feb 17 '13 at 10:58</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-24715498">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                105
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
                It is an improvement but still needs to download and store a full copy of the remote repository in origin, which one might like to avoid at all if he is interested only in portions of the codebase (or if there is documentation subfolders as in my case)
                    – <a href="/users/1006828/a1an" title="1,502 reputation" target="_blank">a1an</a>
                <a href="#comment24715498_13738951" target="_blank">Jun 13 '13 at 12:42</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-35091077">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                48
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
                Is there a way to clone desired directory contents (not directory itself) right into my repository?  For example I want clone contents of <code>https://github.com/Umkus/nginx-boilerplate/tree/master/src</code> right into <code>/etc/nginx</code>
                    – <a href="/users/1168586/mac" title="515 reputation" target="_blank">mac</a>
                <a href="#comment35091077_13738951" target="_blank">Apr 10 '14 at 5:40</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-36401533">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                21
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
                @Chronial, @ErikE: you're both right / wrong :P The <code>git remote add</code> command does <i>not</i> imply a fetch, but <code>git remote add -f</code>, as used here, does! That's what the <code>-f</code> means.
                    – <a href="/users/470844/ntc2" title="5,306 reputation" target="_blank">ntc2</a>
                <a href="#comment36401533_13738951" target="_blank">May 16 '14 at 0:02</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-41660795">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                14
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
                Using this and <code>--depth=1</code> I cloned Chromium Devtools in 338 MB instead of 4.9 GB of full Blink source + history. Excellent.
                    – <a href="/users/247372/rudie" title="24,032 reputation" target="_blank">Rudie</a>
                <a href="#comment41660795_13738951" target="_blank">Oct 22 '14 at 19:26</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-13738951">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>20</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-21316855">
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
<p>I just <a href="https://github.com/mfbx9da4/git-sub-dir" target="_blank">wrote a script</a> for <a href="http://en.wikipedia.org/wiki/GitHub" target="_blank">GitHub</a>.</p>

<p>Usage: </p>

<pre><code>python get_git_sub_dir.py path/to/sub/dir &lt;RECURSIVE&gt;
</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-21316855">
		        <table>
                    <tbody>



    <tr id="comment-36716112">
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
                FYI, that's for <i>GitHub</i> only.
                    – <a href="/users/1479945/sz" title="948 reputation" target="_blank">Sz.</a>
                <a href="#comment36716112_21316855" target="_blank">May 25 '14 at 14:49</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-54122365">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                7
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
                And apparently this is for <b>downloading</b> a directory, not <b>cloning</b> a piece of a repo with all its metadata... right?
                    – <a href="/users/423105/larsh" title="19,754 reputation" target="_blank">LarsH</a>
                <a href="#comment54122365_21316855" target="_blank">Oct 15 '15 at 19:18</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-21316855">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-25771130">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        52
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p><a href="https://www.kernel.org/pub/software/scm/git/docs/git-archive.html" target="_blank">This</a> looks far simpler:</p>

<pre><code>git archive --remote=&lt;repo_url&gt; &lt;branch&gt; &lt;path&gt; | tar xvf -
</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-25771130">
		        <table>
                    <tbody>



    <tr id="comment-40799515">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                12
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
                When I do this on github I get fatal: Operation not supported by protocol. Unexpected end of command stream
                    – <a href="/users/914859/michael-fox" title="1,868 reputation" target="_blank">Michael Fox</a>
                <a href="#comment40799515_25771130" target="_blank">Sep 25 '14 at 17:37</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-41672144">
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
                This works with bitbucket =)
                    – <a href="/users/565946/paul-rigor" title="479 reputation" target="_blank">Paul Rigor</a>
                <a href="#comment41672144_25771130" target="_blank">Oct 23 '14 at 5:05</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-43146383">
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
                The protocol error could be because of HTTPS or : in the repo url. It could also be because of missing ssh key.
                    – <a href="/users/355507/neutralizer" title="3,784 reputation" target="_blank">Neutralizer</a>
                <a href="#comment43146383_25771130" target="_blank">Dec 7 '14 at 17:34</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-50462431">
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
                If you're using github you can use <code>svn export</code> instead
                    – <a href="/users/442852/0sh" title="1,695 reputation" target="_blank">0sh</a>
                <a href="#comment50462431_25771130" target="_blank">Jul 5 '15 at 15:25</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-50794627">
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
                Won't work wiht Github --&gt; Invalid command: 'git-upload-archive 'xxx/yyy.git''   You appear to be using ssh to clone a git:// URL.   Make sure your core.gitProxy config option and the   GIT_PROXY_COMMAND environment variable are NOT set. fatal: The remote end hung up unexpectedly
                    – <a href="/users/790198/nianliang" title="1,998 reputation" target="_blank">Nianliang</a>
                <a href="#comment50794627_25771130" target="_blank">Jul 14 '15 at 15:19</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-25771130">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>2</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-28039894">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        243
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>You can combine the <em>sparse checkout</em> and the <em>shallow clone</em> features. The <em>shallow clone</em> cuts off the history and the <em>sparse checkout</em> only pulls the files matching your patterns.</p>

<pre><code>git init &lt;repo&gt;
cd &lt;repo&gt;
git remote add origin &lt;url&gt;
git config core.sparsecheckout true
echo "finisht/*" &gt;&gt; .git/info/sparse-checkout
git pull --depth=1 origin master
</code></pre>

<p>You'll need minimum git 1.9 for this to work. Tested it myself only with 2.2.0 and 2.2.2.</p>

<p>This way you'll be still able to <strong>push</strong>, which is not possible with <code>git archive</code>.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-28039894">
		        <table>
                    <tbody>



    <tr id="comment-47412093">
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
                This is the correct answer. All the other answers pull way too much data.
                    – <a href="/users/650492/johan" title="56,247 reputation" target="_blank">Johan</a>
                <a href="#comment47412093_28039894" target="_blank">Apr 14 '15 at 18:37</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-52313164">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                11
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
                This is useful, and may be the best available answer, but it still <i>clones</i> the content that you don't care about (if it is on the branch that you pull), even though it doesn't show up in the checkout.
                    – <a href="/users/86967/nobar" title="19,385 reputation" target="_blank">nobar</a>
                <a href="#comment52313164_28039894" target="_blank">Aug 25 '15 at 21:54</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-53175020">
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
                What is your git version? According to git help is the depth option available?
                    – <a href="/users/2753241/udondan" title="26,032 reputation" target="_blank">udondan</a>
                <a href="#comment53175020_28039894" target="_blank">Sep 19 '15 at 5:14</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-62101105">
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
            
        </td>
    </tr>
    <tr id="comment-65940464">
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
                How to only fetch files inside sub directory?
                    – <a href="/users/2264452/babish-shrestha" title="1,481 reputation" target="_blank">Babish Shrestha</a>
                <a href="#comment65940464_28039894" target="_blank">Sep 3 '16 at 4:49</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-28039894">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>12</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-36166891">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        16
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>It's not possible to clone subdirectory only with Git, but below are few workarounds.</p>

<h3>Filter branch</h3>

<p>You may want to rewrite the repository to look as if <code>trunk/public_html/</code> had been its project root, and discard all other history (using <a href="https://git-scm.com/docs/git-filter-branch" target="_blank"><code>filter-branch</code></a>), try on already checkout branch:</p>

<pre><code>git filter-branch --subdirectory-filter trunk/public_html -- --all
</code></pre>

<p><sup>Notes: The <code>--</code> that separates filter-branch options from revision options, and the <code>--all</code> to rewrite all branches and tags. All information including original commit times or merge information will be <strong>preserved</strong>. This command honors <code>.git/info/grafts</code> file and refs in the <code>refs/replace/</code> namespace, so if you have any grafts or replacement <code>refs</code> defined, running this command will make them permanent.</sup></p>

<blockquote>
  <p>Warning! The rewritten history will have different object names for all the objects and will not converge with the original branch. You will not be able to easily push and distribute the rewritten branch on top of the original branch. Please do not use this command if you do not know the full implications, and avoid using it anyway, if a simple single commit would suffice to fix your problem. </p>
</blockquote>

<hr />

<h3>Sparse checkout</h3>

<p>Here are simple steps with <a href="https://git-scm.com/docs/git-read-tree" target="_blank">sparse checkout</a> approach which will populate the working directory sparsely, so you can tell Git which folder(s) or file(s) in the working directory are worth checking out.</p>

<ol>
<li><p>Clone repository as usual (<code>--no-checkout</code> is optional):</p>

<pre><code>git clone --no-checkout git@foo/bar.git
cd bar
</code></pre>

<p><sup>You may skip this step, if you've your repository already cloned.</sup></p>

<p>Hint: For large repos, consider <a href="https://git-scm.com/docs/git-read-tree" target="_blank">shallow clone</a> (<code>--depth 1</code>) to checkout only latest revision or/and <code>--single-branch</code> only.</p></li>
<li><p>Enable <code>sparseCheckout</code> option:</p>

<pre><code>git config core.sparseCheckout true
</code></pre></li>
<li><p>Specify folder(s) for sparse checkout (<strong>without</strong> space at the end):</p>

<pre><code>echo "trunk/public_html/*"&gt; .git/info/sparse-checkout
</code></pre>

<p>or edit <code>.git/info/sparse-checkout</code>.</p></li>
<li><p>Checkout the branch (e.g. <code>master</code>):</p>

<pre><code>git checkout master
</code></pre></li>
</ol>

<p>Now you should have selected folders in your current directory.</p>

<p>You may consider symbolic links if you've too many levels of directories or filtering branch instead.</p>

<hr />
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-36166891">
		        <table>
                    <tbody>



    <tr id="comment-69603587">
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
                Would <b>Filter branch</b> still allow you to <code>pull</code>?
                    – <a href="/users/822138/sam" title="16,094 reputation" target="_blank">sam</a>
                <a href="#comment69603587_36166891" target="_blank">Dec 17 '16 at 19:21</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-76106493">
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
                @sam: no.  <code>filter-branch</code> would rewrite the parent commits so they'd have different SHA1 IDs, and thus your filtered tree would have no commits in common with the remote tree.  <code>git pull</code> wouldn't know where to try to merge from.
                    – <a href="/users/224132/peter-cordes" title="78,320 reputation" target="_blank">Peter Cordes</a>
                <a href="#comment76106493_36166891" target="_blank">Jun 15 '17 at 4:06</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-36166891">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-39317180">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        55
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>For other users who <strong><em>just want to download</em></strong> a file/folder from github</p>

<p>simply use</p>

<pre><code>svn export &lt;repo&gt;/trunk/&lt;folder&gt;
</code></pre>



<pre><code>svn export https://github.com/lodash/lodash/trunk/docs
</code></pre>

<p>(yes, that's svn here. apparently in 2016 you still need svn to simply download some github files)</p>

<p>Courtesy of <a href="https://stackoverflow.com/questions/7106012/download-a-single-folder-or-directory-from-a-github-repo" target="_blank">Download a single folder or directory from a GitHub repo</a> </p>

<p>Important! Make sure you update the github URL and replace '/tree/master/' with '/trunk/'.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-39317180">
		        <table>
                    <tbody>



    <tr id="comment-71151355">
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
                only version which worked for me with github. The git commands checked out &gt;10k files, the svn export only the 700 i wanted. Thanks!
                    – <a href="/users/1885277/christopher-l%c3%b6rken" title="1,462 reputation" target="_blank">Christopher Lörken</a>
                <a href="#comment71151355_39317180" target="_blank">Feb 1 '17 at 18:19</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-71819095">
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
                Tried doing this with <code>https://github.com/tensorflow/tensorflow/tree/master/tensorf‌​low/examples/trunk/u‌​dacity</code> but got <code>svn: E170000: URL 'https://github.com/tensorflow/tensorflow/tree/master/tensor‌​flow/examples/trunk/‌​udacity' doesn't exist</code> error :(
                    – <a href="/users/3899919/zthomas-nc" title="483 reputation" target="_blank">zthomas.nc</a>
                <a href="#comment71819095_39317180" target="_blank">Feb 19 '17 at 21:55</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-73010823">
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
                @zthomas.nc  You need to remove the 'trunk' preceding udacity, and replace /tree/master/ with /trunk/ instead.
                    – <a href="/users/859249/speedy" title="423 reputation" target="_blank">Speedy</a>
                <a href="#comment73010823_39317180" target="_blank">Mar 22 '17 at 17:01</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-73022378">
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
                This doesn't create an actual repo I can commit to etc does it?
                    – <a href="/users/414062/dominic-tobias" title="19,238 reputation" target="_blank">Dominic Tobias</a>
                <a href="#comment73022378_39317180" target="_blank">Mar 22 '17 at 22:55</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-75643559">
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
                This command was the one that worked for me!  I just wanted to get a copy of a file from a repo so I could modify it locally.  Good old SVN to the rescue!
                    – <a href="/users/2308522/michael-j" title="348 reputation" target="_blank">Michael J</a>
                <a href="#comment75643559_39317180" target="_blank">Jun 2 '17 at 0:32</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-39317180">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>1</b> more comment</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-44005197">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -6
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Why not just the following -- after you initialize the repo, do:
git checkout </p>

<p>This works for files and folders, I do this all the time when i want to clean checkout something. </p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered May 16 '17 at 15:07
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
	    

        <div id="comments-link-44005197">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/git" title="show questions tagged 'git'" target="_blank">git</a> <a href="/questions/tagged/repository" title="show questions tagged 'repository'" target="_blank">repository</a> <a href="/questions/tagged/subfolder" title="show questions tagged 'subfolder'" target="_blank">subfolder</a> <a href="/questions/tagged/git-clone" title="show questions tagged 'git-clone'" target="_blank">git-clone</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
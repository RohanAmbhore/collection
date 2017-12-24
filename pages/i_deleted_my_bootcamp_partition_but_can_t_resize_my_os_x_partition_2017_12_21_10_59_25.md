<a href="https://apple.stackexchange.com/questions/145292/i-deleted-my-bootcamp-partition-but-cant-resize-my-os-x-partition">https://apple.stackexchange.com/questions/145292/i-deleted-my-bootcamp-partition-but-cant-resize-my-os-x-partition</a><div id="articleHeader"><h1><a href="/questions/145292/i-deleted-my-bootcamp-partition-but-cant-resize-my-os-x-partition" target="_blank">I deleted my Bootcamp partition but can't resize my OS X partition</a></h1></div>
            

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        14
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>4</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I didn't realize this would cause issues, but I used Disk Utility to delete my Bootcamp partition and then tried to resize my main partition to fill the disk. This causes an error and I searched for answers only to be <a href="http://forums.macrumors.com/showpost.php?p=10580067&postcount=2" target="_blank">told</a>, </p>

<blockquote>
  <p>You're going to have to reinstall Mac OS X (that's the only solution).</p>
  
  <p>You should have removed the Boot Camp partition in the Boot Camp Assistant.</p>
</blockquote>

<p>What?? I Didn't see any warning in Disk Utility.</p>

<blockquote>
  <p>If you delete this Bootcamp partition you may not be able to boot Windows anymore.</p>
</blockquote>

<p>I saw this but figured it was ok -- I didn't want to boot Windows anymore, I wanted to delete it.  So now what am I supposed to do?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-145292">
		        <table>
                    <tbody>



    <tr id="comment-186040">
        <td>
            
        </td>
        <td>
            <div>
                I had had similar problem and when I opened bootcamp assistant the erase the windows partition, i opened disk utility and "erased the bootcamp partition as microsoft FAT" and this did the trick,opened bootcamp assistant back up and the greyed out box was back in bold I clicked it and voila my hardrive is ONE now
		            – user102419
                <a href="#comment186040_145292" target="_blank">Nov 26 '14 at 17:27</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-300378">
        <td>
            
        </td>
        <td>
            <div>
                I would like to add that this method above (erasing bootcamp partition as FAT and then opening bootcamp assistant) worked absolutely perfectly, with minimal effort and in about 3 minutes.
                    – <a href="/users/79532/xdavidliu" title="110 reputation" target="_blank">xdavidliu</a>
                <a href="#comment300378_145292" target="_blank">Jun 25 '16 at 18:26</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-300489">
        <td>
            
        </td>
        <td>
            <div>
                Sure, that's the "Quick fix" at the start of the answer :)
                    – <a href="/users/66209/arya" title="410 reputation" target="_blank">arya</a>
                <a href="#comment300489_145292" target="_blank">Jun 26 '16 at 16:56</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-145292">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-145293">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        22
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<h1>Quick fix:  Fake Bootcamp.</h1>

<p><a href="http://forums.macrumors.com/showpost.php?p=14164926&postcount=5" target="_blank">"I partitioned the free space (that OS X couldn't use) as MS-DOS, Bootcamp Assistant thought it was Windows, and was able to remove this MS-DOS partition and restore Mac OS to a single partition."</a></p>

<p>This is the easiest solution, so try that first.  </p>

<h1>No luck?  Long fix:</h1>

<p>In my case, I couldn't get Disk Utility to create the partition.</p>

<p>I tried using <code>gpt</code> to recreate the partition, but it wouldn't write to the GPT while any of the partitions were mounted.  But since it's my boot partition we're talking about, the disk was in use, because one of the partitions (my boot partition!) is mounted.  So we need to boot from not-this-disk, and unmount all the partitions on the disk, and then use <code>gpt</code>.</p>

<h2>Internet Recovery</h2>

<p><img src="https://i.stack.imgur.com/bgRI4.jpg" width="100" height="100" /></p>

<p>Boot to Internet Recovery  (hold Cmd+Opt+R during startup), so that the disk will not be in use.  If your machine is too old for Internet Recovery, you should be able to boot from another disk (not another partition) and get the same result.  Note: in this case that the disk numbers (<code>/dev/disk0</code>) may be different for you.</p>

<p>Start Internet Recovery, and go to Utilities -&gt; Terminal.</p>

<p><div class="readableLargeImageContainer"><img src="https://cdn.osxdaily.com/wp-content/uploads/2011/08/launch-terminal-from-recovery-hd.jpg" alt="Internet Recovery terminal" /></div></p>

<p><code>-bash-3.2# gpt show /dev/disk0</code></p>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/m2Zpq.png" alt="gpt show my former bootcamp partition" /></div></p>

<p>This is the space I want to reclaim.</p>

<p>As a sanity check, take the size (second column), multiply it by 512, and divide by a billion.  The result should match the size of your former Bootcamp partition in GB.</p>

<p>Example: <code>58593759</code> * 512 / 1,000,000,000 = 30 GB</p>

<p>Take the start position (first column), that's where we'll tell gpt to make the new partition, with </p>

<pre><code>gpt add -b &lt;start position&gt; -t windows /dev/disk0
</code></pre>

<p>In my case, you can see that the start position is <code>431640960</code>.  You can and should select/Copy/Paste in your own Terminal to get this number copied correctly. </p>

<p>Example: <code>-bash-3.2# gpt add -b 431640960 -t windows /dev/disk0</code></p>

<pre><code>/dev/disk0s4 added
</code></pre>

<h2>Finally!</h2>

<p>If you got an error <code>No such file or directory</code>, read the next section, and then come back here and try again.</p>

<p>Assuming you got the disk added ok, <code>reboot</code> and use Disk Utility to erase the new partition as MS-DOS.  Run Bootcamp assistant and choose Remove Windows 7.</p>

<blockquote>
  <p>Bootcamp has been removed and your disk has been restored to a single volume.</p>
</blockquote>

<p>And all it took was my whole day.</p>

<h2>unable to open device '/dev/disk0': No such file or directory</h2>

<p>When you use the <code>gpt add</code> command, you might get the error</p>

<blockquote>
  <p>unable to open device '/dev/disk0': No such file or directory</p>
</blockquote>

<p>This message is very confusing.  We just read that device earlier with <code>gpt show</code>.
This message really means "device is in use".</p>

<p>OS X Recovery may have mounted it, and you have to unmount it.  Use the <code>mount</code> command to find your mounted partition and <code>umount</code> it.</p>

<pre><code>-bash-3.2# mount
</code></pre>

<p>will produce a huge list of partitions:</p>

<pre><code>/dev/disk2s3 on /
devfs on /dev
/dev/disk3 on /Volumes
/dev/disk4 on /private/var/tmp
/dev/disk5 on /private/var/run
/dev/disk6 on /System/Installation
/dev/disk7 on /private/var/db
/dev/disk8 on /private/var/folders
/dev/disk9 on /private/var/root/Library
/dev/disk10 on /Library/ColorSync/Profiles/Displays
/dev/disk11 on /Library/Preferences
/dev/disk12 on /Library/Preferences/SystemConfiguration
/dev/disk13 on /Library/Keychains
/dev/disk1 /Volumes/Macintosh HD  &lt;--- unmount this /Volumes/&lt;YourDisk&gt;
</code></pre>

<p><code>-bash-3.2# umount /dev/disk1</code></p>

<p>It will periodically be remounted automatically, so try to hurry or you'll have to unmount it again.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-145293">
		        <table>
                    <tbody>



    <tr id="comment-171212">
        <td>
            
        </td>
        <td>
            <div>
                Alternative [if rather facetious] solution. Don't put Bootcamp on your main drive in the first place. I put mine on a separate drive & never had to go through your apparent hell [for which you have my total sympathy & well done for figuring it all out] in ... maybe 8 years of tweaks, upgrades, etc.
                    – <a href="/users/85275/tetsujin" title="45,224 reputation" target="_blank">Tetsujin</a>
                <a href="#comment171212_145293" target="_blank">Sep 14 '14 at 19:10</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-171236">
        <td>
            
        </td>
        <td>
            <div>
                @Tetsujin: Even safer solution while we're in the neighborhood: Don't use Bootcamp at all.  I'll be using VirtualBox from this point forward!
                    – <a href="/users/66209/arya" title="410 reputation" target="_blank">arya</a>
                <a href="#comment171236_145293" target="_blank">Sep 14 '14 at 22:54</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-186039">
        <td>
            
        </td>
        <td>
            <div>
                Great post - if you want to add in how someone would back up their system as a step one here, that would be great. I edited it out of the question since it seems part of the solution and not the initial problem.
                    – <a href="/users/5472/bmike" title="136,712 reputation" target="_blank">bmike♦</a>
                <a href="#comment186039_145293" target="_blank">Nov 26 '14 at 17:34</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-233700">
        <td>
            
        </td>
        <td>
            <div>
                A few extra tips: While you are in "Recovery Mode" - also do a Repair Disk on the main OSX partition. I had a couple small issues that prevented bootcamp from completing the recovery (last step in the process). Some people reported that they had to turn off File Vault to finish this process. I ended up turning mine off too but I'm not sure if it was needed.
		            – user104930
                <a href="#comment233700_145293" target="_blank">Dec 16 '14 at 3:15</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-306013">
        <td>
            
        </td>
        <td>
            <div>
                Just saved me from a full reformat. Only minor difference was when doing <code>gpt add</code> got "Resource Busy" but simple enough to figure out to use same <code>umount</code> solution and then it added fine. In disk utility, don't use the "-" link but instead the "erase" by clicking on the newly created partition and renamed to BOOTCAMP, then the restore magically worked!
                    – <a href="/users/87668/ldg" title="101 reputation" target="_blank">ldg</a>
                <a href="#comment306013_145293" target="_blank">Aug 2 '16 at 1:44</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-145293">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>2</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                    <div>
        <h2>                    <b>protected</b> by <a href="/users/-1/community" target="_blank">Community</a>♦ Jan 8 '15 at 2:58
</h2>
        <p>
Thank you for your interest in this question. 
Because it has attracted low-quality or spam answers that had to be removed, posting an answer now requires 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).
<br /><br />Would you like to answer one of these <a href="/unanswered?fromProtectedNotice=true" target="_blank">unanswered questions</a> instead?
</p>
    </div>





                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/bootcamp" title="show questions tagged 'bootcamp'" target="_blank">bootcamp</a> <a href="/questions/tagged/partition" title="show questions tagged 'partition'" target="_blank">partition</a> <a href="/questions/tagged/display" title="show questions tagged 'display'" target="_blank">display</a> <a href="/questions/tagged/delete" title="show questions tagged 'delete'" target="_blank">delete</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
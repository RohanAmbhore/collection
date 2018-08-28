<a href="https://askubuntu.com/questions/943463/e-problem-executing-scripts-apt-updatepost-invoke-success-error-during-apt-ge">https://askubuntu.com/questions/943463/e-problem-executing-scripts-apt-updatepost-invoke-success-error-during-apt-ge</a><div id="articleHeader"><h1>E: Problem executing scripts APT Update::Post-Invoke-Success error during apt-get update</h1></div>

            

<div id="question">

    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        58
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>13</b></div>



</div>

            </div>

            
<div>
    <div>

<p>I cannot install any package.
It seems the command <code>apt-get update</code> must be run
but it throws some errors:</p>

<pre><code>$ sudo apt-get update
Get:1 http://security.ubuntu.com/ubuntu xenial-security InRelease [102 kB]     
Hit:2 http://ve.archive.ubuntu.com/ubuntu xenial InRelease                     
Hit:3 http://ve.archive.ubuntu.com/ubuntu xenial-updates InRelease             
Hit:4 http://ve.archive.ubuntu.com/ubuntu xenial-backports InRelease           
Fetched 102 kB in 23s (4337 B/s)                                               
*** Error in `appstreamcli': double free or corruption (fasttop): 0x000000000210f4b0 ***
======= Backtrace: =========
/lib/x86_64-linux-gnu/libc.so.6(+0x777e5)[0x7fac8d8317e5]
[...]
Aborted (core dumped)
Reading package lists... Done
E: Problem executing scripts APT::Update::Post-Invoke-Success 
 'if /usr/bin/test -w /var/cache/app-info -a -e /usr/bin/appstreamcli; 
 then appstreamcli refresh &gt; /dev/null; fi'
E: Sub-process returned an error code
</code></pre>

<p><a href="https://drive.google.com/open?id=0B4gb2dfdpIGeamJWam5Jb0o0OHM" target="_blank">Full terminal output.txt </a></p>
    </div>
    
    
</div>

                
    <div>
	    

        <div id="comments-link-943463">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </div>        </div>
</div>



        <div id="answers">

                
                




  



  

<div id="answer-944156">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        39
        <a title="This answer is not useful" target="_blank">down vote</a>





</div>

            </div>
            


<div>
    <div>
<pre><code>sudo apt install --reinstall libappstream3
</code></pre>

<p>can fix it.</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-944156">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-949722">
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
<p>In my case, purging, or re-installing didn't help.</p>

<p>The removal of the apt.conf.d entry did however solve the issue for me.</p>

<pre><code>Friday 25 August  22:17:45 AEST 2017
LSB Version:    core-9.20160110ubuntu0.2-amd64:core-9.20160110ubuntu0.2-noarch:printing-9.20160110ubuntu0.2-amd64:printing-9.20160110ubuntu0.2-noarch:security-9.20160110ubuntu0.2-amd64:security-9.20160110ubuntu0.2-noarch
    Distributor ID: Ubuntu
    Description:    Ubuntu 16.04.3 LTS
    Release:    16.04
    Codename:   xenial
</code></pre>

<p>I ran the following commands to get rid of the error:</p>

<pre><code>sudo apt-get purge libappstream2
sudo rm /etc/apt/apt.conf.d/50appstream
</code></pre>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-949722">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-1053844">
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
<p>I came from <a href="https://askubuntu.com/questions/1051536/appstreamcli-appstream-system-cache-was-updated-but-problems-were-found-metad?noredirect=1&lq=1" target="_blank">this page</a> and was redirected here, over there I cannot answer but this is actually an answer for that page. Since I had the same issue (at least same as one of the related issues, but hey I did not relate them so sorry if it is not right solution for you ) and found it quite difficult to find the right information, but in the end succeeded, I thought why not share it here. It took me 2 days evening hours to put the pieces together but this is what I did, hope it helps some of you.</p>

<p>I followed this procedure to clean the mess, made a backup first, just in case. </p>

<pre><code>sudo apt install appstream/xenial-backports
sudo rm /etc/apt/apt.conf.d/50appstream
sudo rm /var/cache/app-info/xmls/fwupd.xml
sudo apt install --reinstall libappstream4
sudo appstreamcli refresh --force
sudo reboot
</code></pre>

<p>Not sure if the reboot is necessary but after reboot I did:</p>

<pre><code>sudo appstreamcli refresh --force
</code></pre>

<p>and had no more errors. </p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-1053844">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-1062375">
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
<p>I had this issue after upgrading from 16.04 LTS to 18.04.1 LTS.  My initial error message was:</p>

<pre><code>AppStream system cache was updated, but problems were found: Metadata files have errors: /var/cache/app-info/xmls/fwupd.xml
</code></pre>

<p>Here is what I did to fix it:</p>

<pre><code>$ sudo rm /var/cache/app-info/xmls/fwupd.xml
$ sudo appstreamcli refresh --force
</code></pre>

<p>That resulted in this terminal message:</p>

<pre><code>AppStream cache update completed successfully.
</code></pre>

<p>Then, <code>sudo apt-get update</code> and <code>sudo apt-get upgrade</code> worked perfectly.</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-1062375">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-1059935">
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
<p>For having this:</p>

<pre>$ sudo apt-get update
[sudo] password for XXX:           
...

AppStream system cache was updated, but problems were found: Metadata files have errors: /var/cache/app-info/xmls/fwupd.xml
Reading package lists... Done
E: Problem executing scripts APT::Update::Post-Invoke-Success 'if /usr/bin/test -w /var/cache/app-info -a -e /usr/bin/appstreamcli; then appstreamcli refresh-cache &gt; /dev/null; fi'
E: Sub-process returned an error code

$ sudo appstreamcli --version
AppStream CLI tool version: 0.10.6

$ sudo appstreamcli refresh-cache --force --verbose
** (appstreamcli:15334): DEBUG: Added /usr/share/app-info/xmls to metadata search path.
** (appstreamcli:15334): DEBUG: Added /var/lib/app-info/yaml to metadata search path.
** (appstreamcli:15334): DEBUG: Added /var/cache/app-info/xmls to metadata search path.
** (appstreamcli:15334): DEBUG: Refreshing AppStream cache
** (appstreamcli:15334): DEBUG: Searching for data in: /usr/share/app-info/xmls
** (appstreamcli:15334): DEBUG: Searching for data in: /var/cache/app-info/xmls
** (appstreamcli:15334): DEBUG: Searching for data in: /var/lib/app-info/yaml
** (appstreamcli:15334): DEBUG: Reading: /usr/share/app-info/xmls/org.freedesktop.fwupd.xml
** (appstreamcli:15334): DEBUG: Reading: /var/cache/app-info/xmls/fwupd.xml
** (appstreamcli:15334): DEBUG: WARNING: Could not parse XML data: Entity: line 265: parser error : EntityRef: expecting ';'
        &lt;checksum filename="Firmware_SF30&SN30_Pro_V1.26.dat" target="content" t
                                                            ^
...
</pre>

<p>The fix is:</p>

<pre>$ sudo -i

# cd /var/cache/app-info/xmls/

# ls -l
total 236
drwxr-xr-x 2 root root   4096 jul 27 09:56 ./
drwxr-xr-x 5 root root   4096 aug 31  2017 ../
-rw-r--r-- 1 root root 233177 jun 29 16:02 fwupd.xml

# sed &lt; fwupd.xml  -rne 's/Firmware_SF30\&SN30_Pro_V1.26.dat/Firmware_SF30\&SN30_Pro_V1.26.dat/gp'
        &lt;checksum filename="Firmware_SF30&SN30_Pro_V1.26.dat" target="content" type="sha1"&gt;3ef2bdee8aca2a45b9f53b4d4cce9722523f57f8&lt;/checksum&gt;

# sed fwupd.xml -i_BACKUP -re 's/Firmware_SF30\&SN30_Pro_V1.26.dat/Firmware_SF30\&SN30_Pro_V1.26.dat/gp'

# ls -l
total 464
drwxr-xr-x 2 root root   4096 jul 27 09:57 ./
drwxr-xr-x 5 root root   4096 aug 31  2017 ../
-rw-r--r-- 1 root root 233328 jul 27 09:57 fwupd.xml
-rw-r--r-- 1 root root 233177 jun 29 16:02 fwupd.xml_BACKUP

# rm fwupd.xml_BACKUP

# apt-get update
Hit:1 http://se.archive.ubuntu.com/ubuntu xenial InRelease
...
Fetched 491 kB in 0s (715 kB/s)                    
Reading package lists... Done

# exit
logout

$
</pre>

<p>Note:<br />
<a href="https://github.com/hughsie/lvfs-website/issues/33" target="_blank">https://github.com/hughsie/lvfs-website/issues/33</a></p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-1059935">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>
                    <div>
        <h2>                    <b>protected</b> by <a href="/users/-1/community" target="_blank">Community</a>♦ Feb 19 at 11:34
</h2>
        <p>
Thank you for your interest in this question. 
Because it has attracted low-quality or spam answers that had to be removed, posting an answer now requires 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).
<br /><br />Would you like to answer one of these <a href="/unanswered?fromProtectedNotice=true" target="_blank">unanswered questions</a> instead?</p>
    </div>





                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/apt" title="show questions tagged 'apt'" target="_blank">apt</a> <a href="/questions/tagged/appstream" title="show questions tagged 'appstream'" target="_blank">appstream</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
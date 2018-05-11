<a href="https://blog.csdn.net/yangcs2009/article/details/47166361">https://blog.csdn.net/yangcs2009/article/details/47166361</a><div id="articleHeader"><h1>1.首先使用git log查看一下提交历史</h1></div>
<div><ol><li>[demo@ubuntu1204:zh_cn(bugfix/ycs-MOS-1503-notify-template-table-center)]$ git log  </li><li>commit 5e187c7dbe84af67ad19823a54f3cc3e3f6d6940  </li><li>Author: yangcs2009 &lt;yangchangsheng@meituan.com&gt;  </li><li>Date:   Thu Jul 30 20:48:15 2015 +0800  </li><li>    add center style indent  </li><li>commit 6d577eb344080d7e3593733ac8dcb622de22b492  </li><li>Author: yangcs2009 &lt;yangchangsheng@meituan.com&gt;  </li><li>Rebasing (4/4)  </li><li>Date:   Thu Jul 30 20:30:20 2015 +0800  </li><li>    add center style  </li><li>commit f9b9508a3ab634f8c8a2d28ab844a3a87d8e30ab  </li><li>Author: yangcs2009 &lt;yangchangsheng@meituan.com&gt;  </li><li>Date:   Thu Jul 30 20:16:35 2015 +0800  </li><li>    add center style  </li><li>commit 111ab9cc26101f7c6972de3dccfef2836a95efe0  </li><li>Author: yangcs2009 &lt;yangchangsheng@meituan.com&gt;  </li><li>Date:   Thu Jul 30 18:57:46 2015 +0800  </li><li>    update templates  </li></ol></div><pre>[demo@ubuntu1204:zh_cn(bugfix/ycs-MOS-1503-notify-template-table-center)]$ git log
commit 5e187c7dbe84af67ad19823a54f3cc3e3f6d6940
Author: yangcs2009 &lt;yangchangsheng@meituan.com&gt;
Date:   Thu Jul 30 20:48:15 2015 +0800

    add center style indent

commit 6d577eb344080d7e3593733ac8dcb622de22b492
Author: yangcs2009 &lt;yangchangsheng@meituan.com&gt;
Rebasing (4/4)
Date:   Thu Jul 30 20:30:20 2015 +0800

    add center style

commit f9b9508a3ab634f8c8a2d28ab844a3a87d8e30ab
Author: yangcs2009 &lt;yangchangsheng@meituan.com&gt;
Date:   Thu Jul 30 20:16:35 2015 +0800

    add center style

commit 111ab9cc26101f7c6972de3dccfef2836a95efe0
Author: yangcs2009 &lt;yangchangsheng@meituan.com&gt;
Date:   Thu Jul 30 18:57:46 2015 +0800

    update templates</pre>这样在git中看到的是4次提交，有点冗余，需要做的是将4次commit合并为一次
<h1>2. git 压缩  git rebase -i HEAD~4</h1>
<p>该命令执行后，会弹出一个编辑窗口，4次提交的commit倒序排列，最上面的是最早的提交，最下面的是最近一次提交。</p>
<div><ol><li>pick 5e187c7dbe8    add center style indent  </li><li>pick 6d577eb3440    add center style  </li><li>pick f9b9508a3ab    add center style  </li><li>pick 111ab9cc261    update templates  </li><li># Rebase 150a643..2fad1ae onto 150a643  </li><li># Commands:  </li><li>#  p, pick = use commit  </li><li>#  r, reword = use commit, but edit the commit message  </li><li>#  e, edit = use commit, but stop for amending  </li><li>#  s, squash = use commit, but meld into previous commit  </li><li>#  f, fixup = like "squash", but discard this commit's log message  </li><li>#  x, exec = run command (the rest of the line) using shell  </li><li># These lines can be re-ordered; they are executed from top to bottom.  </li><li># If you remove a line here THAT COMMIT WILL BE LOST.  </li><li># However, if you remove everything, the rebase will be aborted.  </li><li># Note that empty commits are commented out  </li></ol></div><pre>pick 5e187c7dbe8	add center style indent
pick 6d577eb3440	add center style
pick f9b9508a3ab	add center style
pick 111ab9cc261	update templates
# Rebase 150a643..2fad1ae onto 150a643
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
</pre><div><ol><li>pick 5e187c7dbe8    add center style indent  </li><li>squash 6d577eb3440  add center style  </li><li>squash f9b9508a3ab  add center style  </li><li>squash 111ab9cc261  update templates  </li><li># Rebase 150a643..2fad1ae onto 150a643  </li><li># Commands:  </li><li>#  p, pick = use commit  </li><li>#  r, reword = use commit, but edit the commit message  </li><li>#  e, edit = use commit, but stop for amending  </li><li>#  s, squash = use commit, but meld into previous commit  </li><li>#  f, fixup = like "squash", but discard this commit's log message  </li><li>#  x, exec = run command (the rest of the line) using shell  </li><li># These lines can be re-ordered; they are executed from top to bottom.  </li><li># If you remove a line here THAT COMMIT WILL BE LOST.  </li><li># However, if you remove everything, the rebase will be aborted.  </li><li># Note that empty commits are commented out  </li></ol></div><pre>pick 5e187c7dbe8	add center style indent
squash 6d577eb3440	add center style
squash f9b9508a3ab	add center style
squash 111ab9cc261	update templates
# Rebase 150a643..2fad1ae onto 150a643
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out</pre>修改第2-4行的第一个单词pick为squash，当然看一下里面的注释就理解含义了。
<p>然后保存退出，git会压缩提交历史，如果有冲突，需要修改，修改的时候要注意，保留最新的历史，不然我们的修改就丢弃了。修改以后要记得敲下面的命令：</p>
<div><ol><li>git add .  </li><li>git rebase --continue  </li></ol></div><pre>git add .
git rebase --continue</pre>
<p>如果你想放弃这次压缩的话，执行以下命令：</p>
<div><ol><li>git rebase --abort  </li></ol></div><pre>git rebase --abort</pre>
<p>如果没有冲突，或者冲突已经解决，则会出现如下的编辑窗口：</p>
<div><ol><li># This is a combination of 4 commits.  </li><li># The first commit’s message is:  </li><li>add center style indent  </li><li># The 2nd commit’s message is:  </li><li>add center style  </li><li># The 3rd commit’s message is:  </li><li>add center style  </li><li># The 4th commit’s message is:  </li><li>update templates  </li><li># Please enter the commit message for your changes. Lines starting  </li><li># with ‘#’ will be ignored, and an empty message aborts the commit.  </li></ol></div><pre># This is a combination of 4 commits.
# The first commit’s message is:
add center style indent

# The 2nd commit’s message is:
add center style

# The 3rd commit’s message is:
add center style

# The 4th commit’s message is:
update templates

# Please enter the commit message for your changes. Lines starting
# with ‘#’ will be ignored, and an empty message aborts the commit.</pre>
<h1>3.同步到远程git仓库</h1>
不过此时远程的信息仍未改变，下面操作会把修改同步到远程git仓库
<div><ol><li>[demo@ubuntu1204:zh_cn(bugfix/ycs-MOS-1503-notify-template-table-center)]$ git push -f  </li><li>Enter passphrase for key '/home/demo/.ssh/id_rsa':  </li><li>Counting objects: 1, done.  </li><li>Writing objects: 100% (1/1), 223 bytes | 0 bytes/s, done.  </li><li>Total 1 (delta 0), reused 0 (delta 0)  </li><li>remote:  </li><li>remote: View pull request for bugfix/ycs-MOS-1503-notify-template-table-center =&gt; release/1.1.3:  </li><li>remote:   http://git.sankuai.com/projects/SA/repos/cloud/pull-requests/1042  </li><li>remote:  </li><li>To ssh://git@git.sankuai.com/sa/cloud.git  </li><li> + 5e187c7...8d26431 bugfix/ycs-MOS-1503-notify-template-table-center -&gt; bugfix/ycs-MOS-1503-notify-template-table-center (forced update)  </li></ol></div><pre>[demo@ubuntu1204:zh_cn(bugfix/ycs-MOS-1503-notify-template-table-center)]$ git push -f
Enter passphrase for key '/home/demo/.ssh/id_rsa':
Counting objects: 1, done.
Writing objects: 100% (1/1), 223 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
remote:
remote: View pull request for bugfix/ycs-MOS-1503-notify-template-table-center =&gt; release/1.1.3:
remote:   http://git.sankuai.com/projects/SA/repos/cloud/pull-requests/1042
remote:
To ssh://git@git.sankuai.com/sa/cloud.git
 + 5e187c7...8d26431 bugfix/ycs-MOS-1503-notify-template-table-center -&gt; bugfix/ycs-MOS-1503-notify-template-table-center (forced update)</pre><h1>4.查看远程git仓库效果</h1>
<p><div class="readableLargeImageContainer"><img src="https://img-blog.csdn.net/20150731104937750" /></div><div class="readableLargeImageContainer"><img src="https://img-blog.csdn.net/20150731104830228" /></div></p>
            
                
				
        	</article>
	
		
	
	
		
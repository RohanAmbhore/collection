<a href="http://www.ssite.cn/2017/05/23/centos-6-5%E5%AE%89%E8%A3%85aria2/">http://www.ssite.cn/2017/05/23/centos-6-5%E5%AE%89%E8%A3%85aria2/</a><div id="articleHeader"><h1>CentOS 6.5安装aria2</h1></div>

	<div>
		<p>由于yum install aria2无法找到安装包，试了好几个源，都找不到，于是自己找了一些地址：</p>
<p>1、下载安装包：</p>
<p># wget http://ftp.tu-chemnitz.de/pub/linux/dag/redhat/el6/en/x86_64/rpmforge/RPMS/aria2-1.16.4-1.el6.rf.x86_64.rpm</p>
<p># wget http://ftp.tu-chemnitz.de/pub/linux/dag/redhat/el6/en/x86_64/rpmforge/RPMS/nettle-2.2-1.el6.rf.x86_64.rpm</p>
<p># wget http://ftp.tu-chemnitz.de/pub/linux/dag/redhat/el6/en/x86_64/rpmforge/RPMS/nettle-devel-2.2-1.el6.rf.x86_64.rpm</p>

<p>安装aria2时会提示</p>
<blockquote><p>error: Failed dependencies:<br />
libnettle.so.4()(64bit) is needed by aria2-1.16.4-1.el6.rf.x86_64</p></blockquote>
<p>所以，需要先安装nettle-2.2.1，依次执行以下安装命令即可：</p>
<p># rpm -ivh nettle-2.2-1.el6.rf.x86_64.rpm</p>
<p># rpm -ivh nettle-devel-2.2-1.el6.rf.x86_64.rpm</p>
<p># rpm -ivh aria2-1.16.4-1.el6.rf.x86_64.rpm</p>
<p>3、测试（下载百度首页）</p>
<p># aria2c http://www.baidu.com</p>
<blockquote><p>05/23 00:00:13 [NOTICE] Download complete: /home/root/index.html</p>
<p>Download Results:<br />
gid |stat|avg speed |path/URI<br />
======+====+===========+=======================================================<br />
678b8e|OK | 0.9MiB/s|/home/root/index.html</p>
<p>Status Legend:<br />
(OK):download completed.</p></blockquote>
	</div>

	
	<footer>
		发布于 <a href="http://www.ssite.cn/2017/05/23/centos-6-5%e5%ae%89%e8%a3%85aria2/" target="_blank"><time>2017年5月23日</time></a>作者 <a href="http://www.ssite.cn/author/cuijf/" target="_blank">cc</a>分类 <a href="http://www.ssite.cn/category/useful/" target="_blank">实用</a>标签 <a href="http://www.ssite.cn/tag/aria2/" target="_blank">aria2</a>、<a href="http://www.ssite.cn/tag/centos/" target="_blank">centos</a>			</footer>

</article>

<div id="comments">

	
	
		<div id="respond">
		<h3 id="reply-title">发表评论 <small><a href="/2017/05/23/centos-6-5%E5%AE%89%E8%A3%85aria2/#respond" id="cancel-comment-reply-link" target="_blank">取消回复</a></small></h3>			
				<p>电子邮件地址不会被公开。</p><p><label>评论</label> </p><p><label>姓名</label> </p>
<p><label>电子邮件</label> </p>
<p><label>站点</label> </p>
<p><label>Save my name, email, and website in this browser for the next time I comment.</label></p>
</div>
	


	
		</main>
	
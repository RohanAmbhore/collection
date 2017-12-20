<a href="http://www.cnblogs.com/fengtengfei/p/4359691.html">http://www.cnblogs.com/fengtengfei/p/4359691.html</a><div id="articleHeader"><h1>			<a href="http://www.cnblogs.com/fengtengfei/p/4359691.html" id="cb_post_title_url" target="_blank">Mac下Apache+MySQL+PHP安装</a>		</h1></div>
		
		
			<p>max下是自带有Apache和php的服务器的，不需要另外安装，本文就对相关配置进行介绍。</p>
<h2 id="第一apache">第一：Apache</h2>
<p>在终端中输入，下面指令即可启动Apache服务器：</p>
<pre><code> //启动
 sudo apachectl-k start  
  //重新启动
 sudo apachectl -k restart
 </code></pre>

<p>在浏览器中输入：<a href="http://127.0.0.1，显示为It" target="_blank">http://127.0.0.1，显示为It</a> Works！，既证明服务器已经启动。</p>
<p>但是由于默认站点位于系统路径下，所以我们修改到自定义的路径。所以还需要进行相关配置</p>
<p>修改站点位置：</p>
<p>终端中输入</p>
<pre><code> cd /etc/apache2/
 sudo vim httpd.conf // 会提示输入密码，输入后回车即可
 英文下输入： /DocumentRoot，查找,
 注：1：注意区分大小写；2：要修改两个地方，故要进行两次查找。</code></pre>
<p>第一次查找后，修改：<div class="readableLargeImageContainer"><img src="http://images.cnitblog.com/blog2015/589133/201503/231410589898815.png" /></div></p>
<p>第二次查找后，修改<div class="readableLargeImageContainer"><img src="http://images.cnitblog.com/blog2015/589133/201503/231410512861995.png" /></div></p>
<p>修改好后:wq保存退出，重启服务器，并在自定义的路径下放置html文件，即可访问。</p>
<h2 id="第二配置php服务器">第二：配置PHP服务器：</h2>
<p>1：终端中输入指令：</p>
<pre><code> cd /etc/apache2
 sudo vim httpd.conf
 按 /php，进行搜索，把带有LoadModule php5…..这一行的#(注释符号）去掉即可。</code></pre>
<p><div class="readableLargeImageContainer"><img src="http://images.cnitblog.com/blog2015/589133/201503/231410352395226.png" /></div></p>
<p>2：终端中输入：</p>
<pre><code> cd /etc/
 sudo cp php.ini.default php.ini
 </code></pre>
<p>重启服务器，在自定义的站点路径下放置php文件，即可访问php内容。</p>
<p>第三：MySQ安装：<br />
MySql下载：<a href="http://dev.mysql.com/downloads/mysql/" target="_blank">http://dev.mysql.com/downloads/mysql/</a></p>
<p>MySqlWorkbench下载：<a href="http://dev.mysql.com/downloads/workbench/" target="_blank">http://dev.mysql.com/downloads/workbench/</a><br />
下载后直接安装即可，一路默认就好</p>
<p>MySql配置：<br />
打开终端，输入：</p>
<pre><code> vim ~/.bash_profile</code></pre>
<p>输入 i进行编辑 ，然后粘贴以下内容</p>
<pre><code># mysql
alias mysql='/usr/local/mysql/bin/mysql'
alias mysqladmin='/usr/local/mysql/bin/mysqladmin'
# ls
alias ls='ls -G'</code></pre>
<p>按ESC键 ，输入 :wq<br />
这样在终端中 直接输入 mysql 就可以进入mysql 。输入 exit 为退出</p>
<p>修改MySql的管理员密码，在终端中输入：</p>
<pre><code> mysqladmin -u root password "root"


启动Mysql服务
     sudo /Library/StartupItems/MySQLCOM/MySQLCOM start
停止Mysql服务
     sudo /Library/StartupItems/MySQLCOM/MySQLCOM stop
重启Mysql服务
     sudo /Library/StartupItems/MySQLCOM/MySQLCOM restart</code></pre>
<p>至此，Apache+MySQL+PHP安装配置完毕。</p>
<p>附：对vim编辑器进行介绍<br />
vim有两种模式：<br />
1：命令模式</p>
<pre><code> shift+v -&gt; 选中一行
 y -&gt; 复制一行
 yy -&gt; 复制当前行 (yank current line)
 p -&gt; 在当前行的下一行复制粘贴的内容
 x -&gt; 删除一个字符
 :wq -&gt; 保存退出
 :q! -&gt; 不保存退出
 i -&gt; 进入编辑
 / -&gt; 按/再输入字符可进行查找
 </code></pre>
<p>2：编辑模式，可直接编辑文档，按esc键可以退出编辑模式</p>

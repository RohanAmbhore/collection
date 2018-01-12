<a href="https://sraji.wordpress.com/2011/08/10/how-to-reset-mysql-root-password/">https://sraji.wordpress.com/2011/08/10/how-to-reset-mysql-root-password/</a><div id="articleHeader"><h1>How to reset MySQL root password ?</h1></div>
					<p>August 10, 2011 by <a href="https://sraji.wordpress.com/author/sraji/" title="Posts by raji" target="_blank">raji</a>  </p>
				

				
					<p>Greetings!</p>
<p>To access MySQL db from terminal it is necessary to give its root password</p>
<p>Since i forgot its root password, i ended up with the following error</p>
<h4>Error:</h4>
<p><strong>ERROR 1045 (28000): Access denied for user ‘root’@’localhost’ </strong></p>
<p><strong>(using password: NO) </strong></p>
<p>Then i followed the below steps to reset it</p>
<h4>Steps:</h4>
<p><strong>1.</strong> [root@venus ~]# service mysqld stop</p>
<p>Stopping mysqld: [ OK ]</p>
<p><strong>2.</strong> [root@venus ~]# mysqld_safe –skip-grant-tables & [1] 3735</p>
<p><strong>3</strong>. [root@venus ~]# 110809 10:43:22 mysqld_safe Logging to ‘/var/log/mysqld.log’. 110809 10:43:22 mysqld_safe</p>
<p>Starting mysqld daemon with databases from /var/lib/mysql</p>
<p><strong>4.</strong> [root@venus ~]# mysql -u root</p>
<p>Welcome to the MySQL monitor. Commands end with ; or \g.</p>
<p>Your MySQL connection id is 1</p>
<p>Server version: 5.1.56 Source distribution</p>
<p>Copyright (c) 2000, 2010, Oracle and/or its affiliates. All rights reserved.</p>
<p>This software comes with ABSOLUTELY NO WARRANTY.</p>
<p>This is free software, and you are welcome to modify and redistribute it under the GPL v2 license</p>
<p>Type ‘help;’ or ‘\h’ for help. Type ‘\c’ to clear the current input statement.</p>
<p><strong>5.</strong> mysql&gt; UPDATE user SET password=PASSWORD(“slash123″)WHERE user=”root”;</p>
<p>ERROR 1046 (3D000): No database selected</p>
<p>( Note: Here “slash123” is my mysql root password )</p>
<p><strong>6</strong>. mysql&gt; show databases;</p>
<p>+——————–+<br />
| Database |<br />
+——————–+<br />
| information_schema |<br />
| django |<br />
| drupal |<br />
| mysql |<br />
| student |<br />
| test |<br />
+——————–+<br />
6 rows in set (0.34 sec)</p>
<p><strong>7.</strong> mysql&gt; use mysql;</p>
<p>Reading table information for completion of table and column names</p>
<p>You can turn off this feature to get a quicker startup with –</p>
<p>A Database changed</p>
<p><strong>8.</strong> mysql&gt; UPDATE user SET password=PASSWORD(“slash123″)WHERE user=”root”;</p>
<p>Query OK, 3 rows affected (1.07 sec) Rows matched: 3 Changed: 3 Warnings: 0</p>
<p><strong>9.</strong> mysql&gt; flush privileges;</p>
<p>Query OK, 0 rows affected (0.00 sec)</p>
<p><strong>10</strong>. mysql&gt; quit Bye</p>
<p><strong>11.</strong> [rajee@venus ~]$ mysql -u root -p</p>
<p>Enter password:</p>
<p>Welcome to the MySQL monitor. Commands end with ; or \g.</p>
<p>Your MySQL connection id is 3</p>
<p>Server version: 5.1.56 Source distribution</p>
<p>Copyright (c) 2000, 2010, Oracle and/or its affiliates. All rights reserved.</p>
<p>This software comes with ABSOLUTELY NO WARRANTY. This is free software,</p>
<p>and you are welcome to modify and redistribute it under the GPL v2 license</p>
<p>Type ‘help;’ or ‘\h’ for help. Type ‘\c’ to clear the current input statement.</p>
<p>That’s it <img src="https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg" alt="🙂" /></p>
<p>Now i am able to access MySQL prompt from the terminal</p>
		<div>
			<div>
				Advertisements
				
						
				
		
			</div>
		</div>									
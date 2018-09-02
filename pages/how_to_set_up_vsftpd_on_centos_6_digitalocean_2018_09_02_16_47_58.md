<a href="https://www.digitalocean.com/community/tutorials/how-to-set-up-vsftpd-on-centos-6--2">https://www.digitalocean.com/community/tutorials/how-to-set-up-vsftpd-on-centos-6--2</a><div id="articleHeader"><h1>       How To Set Up vsftpd on CentOS 6    </h1></div>

    PostedJune 19, 2012

    676.4k views

    
      <a href="/community/tags/security?type=tutorials" target="_blank">Security</a>
      <a href="/community/tags/centos?type=tutorials" target="_blank">CentOS</a>
    
  

  


    <div>
      <h3>About vsftpd</h3>

<p><strong>Warning: FTP is inherently insecure.  If you must use FTP, consider <a href="https://www.digitalocean.com/community/articles/how-to-configure-vsftpd-to-use-ssl-tls-on-a-centos-vps" target="_blank">securing your FTP connection with SSL/TLS</a>.  Otherwise, it is best to <a href="https://www.digitalocean.com/community/articles/how-to-use-sftp-to-securely-transfer-files-with-a-remote-server" target="_blank">use SFTP, a secure alternative to FTP</a>.</strong></p>

<p>The first two letters of vsftpd stand for "very secure" and the program was built to have strongest protection against possible FTP vulnerabilities.</p> 

<h2>Step One—Install vsftpd</h2>

<p>You can quickly install vsftpd on your virtual private server in the command line:</p>

<pre>sudo yum install vsftpd</pre>

<p>We also need to install the FTP client, so that we can connect to an FTP server:</p>

<pre>sudo yum install ftp</pre>

<p>Once the files finish downloading, vsftpd will be on your VPS. Generally speaking, the virtual private server is already configured with a reasonable amount of security. However, it does provide access to anonymous users.</p>

<h2>Step Two—Configure VSFTP</h2>

<p>Once VSFTP is installed, you can adjust the configuration.</p>

<p>Open up the configuration file:</p>

<pre>sudo vi /etc/vsftpd/vsftpd.conf</pre>

<p>One primary change you need to make is to change the Anonymous_enable to No:</p>

<pre>anonymous_enable=NO</pre>

<p>Prior to this change, vsftpd allowed anonymous, unidentified users to access the VPS's files. This is useful if you are seeking to distribute information widely, but may be considered a serious security issue in most other cases. 
After that, uncomment the local_enable option, changing it to yes.
</p>

<pre>local_enable=YES</pre>

<p>Finish up by uncommenting command to chroot_local_user. When this line is set to Yes, all the local users will be jailed within their chroot and will be denied access to any other part of the server.</p> 

<pre>chroot_local_user=YES</pre>

<p>Finish up by restarting vsftpd:</p>

<pre>sudo service vsftpd restart</pre>

<p>In order to ensure that vsftpd runs at boot, run chkconfig:</p>

<pre>chkconfig vsftpd on</pre>

<h2>Step Three—Access the FTP server</h2>

<p>Once you have installed the FTP server and configured it to your liking, you can now access it.</p>

<p>You can reach an FTP server in the browser by typing the domain name into the address bar and logging in with the appropriate ID. Keep in mind, you will only be able to access the user's home directory.</p> 

<pre>ftp://example.com</pre>

<p>Alternatively, you can reach the FTP server through the command line by typing:</p>

<pre> ftp example.com</pre>

<p>Then you can use the word, "exit," to get out of the FTP shell.</p>


    </div>

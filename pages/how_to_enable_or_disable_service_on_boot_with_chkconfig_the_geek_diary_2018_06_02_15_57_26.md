<a href="https://www.thegeekdiary.com/how-to-enable-or-disable-service-on-boot-with-chkconfig/">https://www.thegeekdiary.com/how-to-enable-or-disable-service-on-boot-with-chkconfig/</a><div id="articleHeader"><h1>How to enable or disable service on boot with chkconfig</h1></div>
<p>By <a href="https://www.thegeekdiary.com/author/sandeep_patil/" target="_blank">admin</a> </p></header><p>CentOS/RHEL provides us with a simple command-line tool (chkconfig) for managing services that are started during the various runlevels of your system. chkconfig requires some additional comment lines in the actual init script to tell it in which run levels the service should be started, and when, relatively, the service should be started during the initialization of the run level. (init scripts are processed in a specific order to ensure that services dependent on others are started after the services they depend on.) These lines, taken from the httpd init script, are as follows:</p>
<div>
<pre># chkconfig: 345 85 15
# description: Apache is a World Wide Web server.  It is used to serve
# HTML files and CGI.</pre>
</div>
<p>Here,<br />
<strong>345</strong> – runlevels that the service will be enabled for by default.<br />
<strong>85</strong> – start priority. The lower the number the higher the priority and the sooner a service will be started within a given runlevel.<br />
<strong>15</strong> – stop priority. The lower the number the higher the priority and the sooner a service will be stopped within a given runlevel.</p>
<h2>Listing Services by Using chkconfig</h2>
<p>To get a list of which services are started at which run level, use the command “<strong>chkconfig –list</strong>“. </p>
<div>
<pre># chkconfig --list
acpid          	0:off	1:off	2:on	3:on	4:on	5:on	6:off
auditd         	0:off	1:off	2:on	3:on	4:on	5:on	6:off
blk-availability	0:off	1:on	2:on	3:on	4:on	5:on	6:off
cgconfig       	0:off	1:off	2:off	3:off	4:off	5:off	6:off
...</pre>
</div>
<p>Optionally, you can add a name as an additional argument, and chkconfig will list only the information for that service. Following is the output of chkconfig –list iptables on my system:</p>
<div>
<pre># chkconfig --list iptables
iptables       	0:off	1:off	2:off	3:on	4:on	5:on	6:off</pre>
</div>
<p>In this case, chkconfig reports that the iptables service is to be started for run levels 3, 4, and 5.</p>
<h2>Enabling or Disabling a Service at boot</h2>
<p>In this example, we will use iptables service. If you want, list the currents rulevels where the services will be starting:</p>
<div>
<pre># chkconfig --list iptables
httpd           0:off   1:off   2:off    3:off    4:off    5:off    6:off</pre>
</div>
<p>“chkconfig on” without specifying any runlevel will enable the service on runlevel 2,3,4 and 5. For example:</p>
<div>
<pre># chkconfig iptables on</pre>
</div>
<div>
<pre># chkconfig --list iptables
iptables       	0:off	1:off	2:on	3:on	4:on	5:on	6:off</pre>
</div>
<p>Similarly, to disable the service at all run levels, use the “chkconfig off” command. For example:</p>
<div>
<pre># chkconfig iptables off</pre>
</div>
<div>
<pre># chkconfig --list iptables
iptables       	0:off	1:off	2:off	3:off	4:off	5:off	6:off</pre>
</div>
<h3>chkconfig Fine Control</h3>
<p>The <strong>–level</strong> option can be given to chkconfig to specify which runlevels to make the change (either on or off). Other runlevels will not be altered. This would configure the system to start iptables in runlevels 3 and 5:</p>
<div>
<pre># chkconfig --level 35 iptables on</pre>
</div>
<div>
<pre># chkconfig --list iptables
iptables       	0:off	1:off	2:off	3:on	4:off	5:on	6:off</pre>
</div>
<h2>Adding a Service by Using chkconfig</h2>
<p>To add a new service to all run levels according to the recommendations given to chkconfig, use the following command:</p>
<div>
<pre># chkconfig --add [servicename]</pre>
</div>
<p>chkconfig sets all the links for the service in the correct directories in one swoop.</p>
<div><strong>Note</strong>: When an application or service is installed an initialization script is generated and automatically added to the /etc/init.d. So if you have difficulty in identifying the name of your service, visit /etc/init.d, locate the appropriate script and obtain the service name from its contents.</div>
<h2>Resetting Service Information</h2>
<p>Playing with services is educational, as long as you have a backup of your /etc/rc.d directory tree and a way to get back into the system to restore it. However, this type of drastic action is usually not necessary. Instead, you can restore the service’s startup priority and other information to the recommended settings by issuing the following command.</p>
<div>
<pre># chkconfig [servicename] reset</pre>
</div>
<p>This command returns everything to a (hopefully) sane default.</p>
<h2>Removing a service using chkconfig</h2>
<p>If you no longer require the use of a service, you can disable it at boot by using the “chkconfig off” switch:</p>
<div>
<pre># chkconfig [servicename] off</pre>
</div>
<p>You should then proceed to stop the service from running with the following command:</p>
<div>
<pre># service [servicename] stop</pre>
</div>
<p>The preceding command will take immediate effect. However, in order to finalize this procedure you may want to remove it from the chkconfig management tool by typing:</p>
<div>
<pre># chkconfig --del [servicename]</pre>
</div>
<a href="https://tecadmin.net/install-python-2-7-on-centos-rhel/">https://tecadmin.net/install-python-2-7-on-centos-rhel/</a><div id="articleHeader"><h1>How to Install Python 2.7.15 on CentOS/RHEL 7/6 and Fedora 27/26/25</h1></div>
Updated on May 9, 2018 by <a href="https://tecadmin.net/author/myadmin/" title="Posts by Rahul K." target="_blank">Rahul K.</a>
</header><p>Today, I was trying to install an application on my CentOS 7.4 system which required Python &gt;= 2.7.10, but there are Python 2.7.5 installed, which we can’t remove as other applications depend on it. This tutorial will help you to install Python 2.7.15 without removing older versions.</p><h2>1. Install GCC</h2><p>Firstly make sure that you have GCC package installed on your system. Use the following command to install GCC if you don’t have it installed.</p><pre><hprompt>yum install gcc openssl-devel bzip2-devel
</hprompt></pre><h2>3. Download Python 2.7</h2><p>Download <a href="https://www.python.org/" target="_blank">Python</a> using following command from python official site. You can also download the latest version in place of specified below.</p><pre><hprompt>cd /usr/src
<hprompt>wget https://www.python.org/ftp/python/2.7.15/Python-2.7.15.tgz
</hprompt></hprompt></pre><p>Extract downloaded archive using tar command.</p><pre><hprompt>tar xzf Python-2.7.14.tgz
</hprompt></pre><h2>3. Install Python 2.7</h2><p>Now run the following commands to compile Python 2.7 and install on your system using <code>altinstall</code>.</p><pre><hprompt>cd Python-2.7.15
<hprompt>./configure --enable-optimizations
<hprompt>make altinstall
</hprompt></hprompt></hprompt></pre><p><red>make altinstall</red> is used to prevent replacing the default python binary file /usr/bin/python.</p><h2>4. Check Python Version</h2><p>Check the latest version installed of python using below command. During this installation, the latest Python binary was installed on path /usr/local/bin/python2.7. The existing binary was located under /usr/bin.</p><pre><hprompt><orange>/usr/local/bin/python2.7 -V</orange>

Python 2.7.15
</hprompt></pre><p><strong><red>Warning:</red> Do not overwrite or link the original Python binary, This may damage your system. </strong></p><h2>Step 5 – Install PIP</h2><p>PIP is a useful utility to install and manage Python modules. Let’s install the PIP for the installed Python version.</p><pre><hprompt>curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
<hprompt>python2.7 get-pip.py
</hprompt></hprompt></pre><br /><br />
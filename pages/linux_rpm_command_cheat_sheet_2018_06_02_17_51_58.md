<a href="https://www.cyberciti.biz/howto/question/linux/linux-rpm-cheat-sheet.php">https://www.cyberciti.biz/howto/question/linux/linux-rpm-cheat-sheet.php</a><div id="articleHeader"><h1>rpm command cheat sheet for Linux</h1></div>
<p>rpm is a powerful Package Manager for Red Hat, Suse and Fedora Linux. It can be used to build, install, query, verify, update, and remove/erase individual software packages. A Package consists of an archive of files, and package information, including name, version, and description:</p>
<table>
<tbody><tr>
<td><b>Syntax</b></td>
<td><b>Description</b></td>
<td><b>Example(s)</b></td>
</tr>
<tr>
<td>rpm -ivh {rpm-file}</td>
<td>Install the package</td>
<td>rpm -ivh mozilla-mail-1.7.5-17.i586.rpm<br />rpm -ivh --test mozilla-mail-1.7.5-17.i586.rpm</td>
</tr>
<tr>
<td>rpm -Uvh {rpm-file}</td>
<td>Upgrade package</td>
<td>rpm -Uvh mozilla-mail-1.7.6-12.i586.rpm<br />rpm -Uvh --test mozilla-mail-1.7.6-12.i586.rpm</td>
</tr>
<tr>
<td>rpm -ev {package}</td>
<td>Erase/remove/ an installed package</td>
<td>rpm -ev mozilla-mail</td>
</tr>
<tr><td>rpm -ev --nodeps {package}</td>
<td>Erase/remove/ an installed package without checking for dependencies</td>
<td>rpm -ev --nodeps mozilla-mail</td>
</tr>
<tr>
<td>rpm -qa</td>
<td>Display list all installed packages</td>
<td>rpm -qa<br />rpm -qa | less</td>
</tr>
<tr>
<td>rpm -qi {package}</td>
<td>Display installed information along with package version and short description</td>
<td>rpm -qi mozilla-mail</td>
</tr>
<tr>
<td>rpm -qf {/path/to/file}</td>
<td>Find out what package a file belongs to i.e. find what package owns the file</td>
<td>rpm -qf /etc/passwd<br />rpm -qf /bin/bash</td>
</tr>
<tr>
<td>rpm -qc {pacakge-name}</td>
<td>Display list of configuration file(s) for a package</td>
<td>rpm -qc httpd</td>
</tr>
<tr>
<td>rpm -qcf {/path/to/file}</td>
<td>Display list of configuration files for a command</td>
<td>rpm -qcf /usr/X11R6/bin/xeyes</td>
</tr>
<tr>
<td>rpm -qa --last</td>
<td>Display list of all recently installed RPMs</td>
<td>rpm -qa --last<br />rpm -qa --last | less</td>
</tr>
<tr>
<td>rpm -qpR {.rpm-file}<br />rpm -qR {package}</td>
<td>Find out what dependencies a rpm file has</td>
<td>rpm -qpR mediawiki-1.4rc1-4.i586.rpm<br /> rpm -qR bash</td>
</tr>
</tbody></table>
<p>{package} - Replace with actual package name

</p>
For more info see:


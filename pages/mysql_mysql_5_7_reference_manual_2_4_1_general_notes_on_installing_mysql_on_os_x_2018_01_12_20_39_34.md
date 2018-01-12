<a href="https://dev.mysql.com/doc/refman/5.7/en/osx-installation-notes.html">https://dev.mysql.com/doc/refman/5.7/en/osx-installation-notes.html</a><div id="articleHeader"><h1>2.4.1 General Notes on Installing MySQL on OS X</h1></div>
<p>
      You should keep the following issues and notes in mind:
</p>
<div>
<ul><li><p>
          As of MySQL server 5.7.8, the DMG bundles a launchd daemon
          instead of the deprecated startup item. Startup items do not
          function as of OS X 10.10 (Yosemite), so using launchd is
          preferred. The available MySQL preference pane under OS X
          System Preferences was also updated to
          use launchd.
        </p></li><li><p>
          You may need (or want) to create a specific
          <code>mysql</code> user to own the MySQL directory and
          data. You can do this through the <strong>Directory
          Utility</strong>, and the <code>mysql</code> user
          should already exist. For use in single user mode, an entry
          for <code>_mysql</code> (note the underscore prefix)
          should already exist within the system
          <code>/etc/passwd</code> file.
        </p></li><li><p>
          Because the MySQL package installer installs the MySQL
          contents into a version and platform specific directory, you
          can use this to upgrade and migrate your database between
          versions. You will need to either copy the
          <code>data</code> directory from the old version to
          the new version, or alternatively specify an alternative
          <code>datadir</code> value to set location of the data
          directory. By default, the MySQL directories are installed
          under <code>/usr/local/</code>.
        </p></li><li><p>
          You might want to add aliases to your shell's resource file to
          make it easier to access commonly used programs such as
          <a href="mysql.html" title="4.5.1 mysql — The MySQL Command-Line Tool" target="_blank"><strong>mysql</strong></a> and <a href="mysqladmin.html" title="4.5.2 mysqladmin — Client for Administering a MySQL Server" target="_blank"><strong>mysqladmin</strong></a>
          from the command line. The syntax for <strong>bash</strong>
          is:
        </p><div><pre><code>alias mysql=/usr/local/mysql/bin/mysql
alias mysqladmin=/usr/local/mysql/bin/mysqladmin</code></pre></div><p>
          For <strong>tcsh</strong>, use:
        </p><div><pre><code>alias mysql /usr/local/mysql/bin/mysql
alias mysqladmin /usr/local/mysql/bin/mysqladmin</code></pre></div><p>
          Even better, add <code>/usr/local/mysql/bin</code> to
          your <code>PATH</code> environment variable. You can do
          this by modifying the appropriate startup file for your shell.
          For more information, see <a href="invoking-programs.html" title="4.2.1 Invoking MySQL Programs" target="_blank">Section 4.2.1, “Invoking MySQL Programs”</a>.
        </p></li><li><p>
          After you have copied over the MySQL database files from the
          previous installation and have successfully started the new
          server, you should consider removing the old installation
          files to save disk space. Additionally, you should also remove
          older versions of the Package Receipt directories located in
          <code>/Library/Receipts/mysql-<em><code>VERSION</code></em>.pkg</code>.
        </p></li><li><p>
          Prior to OS X 10.7, MySQL server was bundled with OS X Server.
</p></li></ul>





                
        
         

                     
<div id="docs-comments">
    <div> User Comments</div>

    <div id="comment-listing">
    
            <div id="c13792">
            <div>
                                  
                Posted by
                
                                    Jay Lawrence
                                
                on
                February 22, 2016
            </div>
                            
                <div>
                    To make future upgrades easier here is what I do:<br /><br />1 - place my 'my.cnf' file in /etc/mysql<br /><br />mkdir /etc/mysql<br />  cp /usr/local/mysql/etc/my.cnf /etc/mysql<br /><br />Note that the cnf search path is: /etc/my.cnf /etc/mysql/my.cnf /usr/local/mysql/etc/my.cnf ~/.my.cnf<br /><br />2 - data in /usr/local/var/mysql/data<br /><br />Stop MySQL<br /><br />Edit the my.cnf file and within the [mysqld] section place:<br />datadir = /usr/local/var/mysql/data<br /><br />mkdir /usr/local/var<br />  mkdir /usr/local/var/mysql<br />  mv /usr/local/mysql/data /usr/local/var/mysql<br /><br />3 - Update Launch Daemon values<br /><br />sudo vi /Library/LaunchDaemons/com.oracle.oss.mysql.mysqld.plist<br /><br />Look for:<br /><br />&lt;string&gt;/usr/local/mysql/bin/mysqld&lt;/string&gt;<br />            &lt;string&gt;--user=_mysql&lt;/string&gt;<br />            &lt;string&gt;--basedir=/usr/local/mysql&lt;/string&gt;<br />            &lt;string&gt;--datadir=/usr/local/mysql/data&lt;/string&gt;<br />            &lt;string&gt;--plugin-dir=/usr/local/mysql/lib/plugin&lt;/string&gt;<br />            &lt;string&gt;--log-error=/usr/local/mysql/data/mysqld.local.err&lt;/string&gt;<br />            &lt;string&gt;--pid-file=/usr/local/mysql/data/mysqld.local.pid&lt;/string&gt;<br /><br />And change to (put var/ in front of mysql/data in lines below)<br /><br />&lt;string&gt;/usr/local/mysql/bin/mysqld&lt;/string&gt;<br />            &lt;string&gt;--user=_mysql&lt;/string&gt;<br />            &lt;string&gt;--basedir=/usr/local/mysql&lt;/string&gt;<br />            &lt;string&gt;--datadir=/usr/local/var/mysql/data&lt;/string&gt;<br />            &lt;string&gt;--plugin-dir=/usr/local/mysql/lib/plugin&lt;/string&gt;<br />            &lt;string&gt;--log-error=/usr/local/var/mysql/data/mysqld.local.err&lt;/string&gt;<br />            &lt;string&gt;--pid-file=/usr/local/var/mysql/data/mysqld.local.pid&lt;/string&gt;<br /><br />Then when you go to upgrade your my.cnf is retained as are your data directories.</div>
                    
            <div id="c15302">
            <div>
                                  
                Posted by
                
                                    Sytze Kalisvaart
                                
                on
                January 5, 2018
            </div>
                            
                <div>
                    After mysql_upgrade, you may need to update /Library/LaunchDaemons/com.oracle.oss.mysql.mysqld.plist again following above suggestions. If you run into problems getting this to work, make sure there are no old my.cfg files around (disable them). If nothing works (could not update local.pid) go back to a clean install and the original upgrade approach proposed in the documentation.</div>
                    
        

        <div>
        <a href="https://dev.mysql.com/auth/register/?dest=https%3A%2F%2Fdev.mysql.com%2Fdoc%2Frefman%2F5.7%2Fen%2Fosx-installation-notes.html%3Facf%3D1%23add-comment" target="_blank">Sign Up</a>
        <a href="https://dev.mysql.com/auth/login/?dest=https%3A%2F%2Fdev.mysql.com%2Fdoc%2Frefman%2F5.7%2Fen%2Fosx-installation-notes.html%3Facf%3D1%23add-comment" target="_blank">Login</a>
        You must be logged in to post a comment.
    </div>
    
              
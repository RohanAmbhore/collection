<a href="https://stackoverflow.com/questions/17666249/how-to-import-an-sql-file-using-the-command-line-in-mysql">https://stackoverflow.com/questions/17666249/how-to-import-an-sql-file-using-the-command-line-in-mysql</a><div id="articleHeader"><h1>How to import an SQL file using the command line in MySQL?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        1099
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>401</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I have a <code>.sql</code> file with an export from phpMyAdmin. I want to import it into a different server using the command line.</p>

<p>I have a <a href="http://en.wikipedia.org/wiki/Windows_Server_2008" target="_blank">Windows Server 2008</a> R2 installation. I placed the <code>.sql</code> file on the C drive, and I tried this command</p>

<pre><code>database_name &lt; file.sql</code></pre>

<p>It is not working I get syntax errors.</p>

<ul>
<li>How can I import this file without a problem?</li>
<li>Do I need to create a database first?</li>
</ul>
    </div>
    
    
</div>
</td>
        </tr>
                    <tr>
            <td colspan="2">
                <div>
        <h2>                    <b>protected</b> by <a href="/users/-1/community" target="_blank">Community</a>♦ Mar 13 '15 at 13:24
</h2>
        <p>
This question is protected to prevent "thanks!", "me too!", or spam answers by new users. 
To answer it, you must have earned at least 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).</p>
    </div>
            </td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-17666249">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-17666279">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2158
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>


<pre><code>mysql -u username -p database_name &lt; file.sql</code></pre>

<p>Check <a href="http://dev.mysql.com/doc/refman/5.0/en/mysql-command-options.html" target="_blank">MySQL Options</a>.</p>

<p>Note: It is better to use the full path of the SQL file <code>file.sql</code>.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-17666279">
		        <table>
                    <tbody>



    <tr id="comment-25733067">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                When I run the file from a program like Toad I get no error but when I run it from the command line i get the error I mentioned
                    – <a href="/users/1915046/jaylen" title="9,857 reputation" target="_blank">Jaylen</a>
                <a href="#comment25733067_17666279" target="_blank">Jul 16 '13 at 1:37</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-51704833">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                33
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Note that yes, you have to create the (empty) database from mysql if it doesn't exist already, before you can import it.
                    – <a href="/users/812102/skippy-le-grand-gourou" title="2,239 reputation" target="_blank">Skippy le Grand Gourou</a>
                <a href="#comment51704833_17666279" target="_blank">Aug 8 '15 at 14:29</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-69671315">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                4
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Yups, remember to create an empty Database (if the db doesn't previously exist), from the MySQL console like so: <code>CREATE DATABASE db-name;</code>
                    – <a href="/users/1290849/qasim" title="663 reputation" target="_blank">Qasim</a>
                <a href="#comment69671315_17666279" target="_blank">Dec 20 '16 at 6:06</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-72153555">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Be sure to check that the backup file does not have "use 'original_db'" in it. Although i specified restore to new DB "mysql new_db &lt; dump.sql" , the sql dump file had that in, and it overwrote my live DB.  Not sure if there is an option to force it to use the DB specified and disregard the "use 'original_db'" in the sql file
                    – <a href="/users/1220728/shaakir" title="194 reputation" target="_blank">Shaakir</a>
                <a href="#comment72153555_17666279" target="_blank">Feb 28 '17 at 11:55</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-79374917">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @Joe, yes, if you have a space between '-p' and 'password', it thinks that 'password' is the database name.  Alternatively, you can type '-p' without your password and then you'll be prompted for a password when you hit enter.
                    – <a href="/users/878703/notjay" title="2,372 reputation" target="_blank">NotJay</a>
                <a href="#comment79374917_17666279" target="_blank">Sep 13 '17 at 19:54</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-17666279">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>13</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-48114605">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p><strong>Import into database:-</strong></p>

<blockquote>
  <p>mysql -u username -p database_name  &lt;  /file path/file_name.sql</p>
</blockquote>

<p><strong>Export from database :-</strong></p>

<blockquote>
  <p>mysqldump -u username -p database_name   &gt;  /file path/file_name.sql</p>
</blockquote>

<p>after these commands prompt will ask for your mysql password</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-48114605">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-47874516">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<pre><code>mysql -u root -p password -D database_name &lt;&lt; import.sql</code></pre>

<p>Use mysql help for details <code>mysql --help</code></p>

<p>I think these will be useful options in our context</p>

<pre><code>[~]$ mysql --help
mysql  Ver 14.14 Distrib 5.7.20, for osx10.12 (x86_64) using  EditLine wrapper
Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.                                                                                                                                         
Usage: mysql [OPTIONS] [database]
  -?, --help          Display this help and exit.
  -I, --help          Synonym for -?
  --bind-address=name IP address to bind to.
  -D, --database=name Database to use.
  --delimiter=name    Delimiter to be used.
  --default-character-set=name Set the default character set.
  -f, --force         Continue even if we get an SQL error.
  -p, --password[=name] Password to use when connecting to server.
  -h, --host=name     Connect to host.
  -P, --port=#        Port number to use for connection or 0 for default to, in order of preference, my.cnf, $MYSQL_TCP_PORT, /etc/services, built-in default (3306).
  --protocol=name     The protocol to use for connection (tcp, socket, pipe,
  -s, --silent        Be more silent. Print results with a tab as separator, each row on new line.
  -v, --verbose       Write more. (-v -v -v gives the table output format).
  -V, --version       Output version information and exit.
  -w, --wait          Wait and retry if connection is down.</code></pre>

<p>what is fun, if we are importing a large database and not having a progress bar. Use Pipe Viewer and see the data transfer through the pipe</p>

<p>For Mac, <code>brew install pv</code>
.For Debian/Ubuntu, <code>apt-get install pv</code>.
Others, refer <a href="http://www.ivarch.com/programs/pv.shtml" target="_blank">http://www.ivarch.com/programs/pv.shtml</a></p>

<pre><code>pv import.sql | mysql -u root -p password -D database_name

1.45GiB 1:50:07 [339.0KiB/s]   [=============&gt;      ] 14% ETA 11:09:36
1.46GiB 1:50:14 [ 246KiB/s]     [=============&gt;      ] 14% ETA 11:09:15
1.47GiB 1:53:00 [ 385KiB/s]     [=============&gt;      ] 14% ETA 11:05:36</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 18 '17 at 18:40
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-47874516">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-45998128">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        22
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If you already have the database use the following to import the <code>dump</code> or the <code>sql</code> file</p>

<pre><code>mysql -u username -p database_name &lt; file.sql</code></pre>

<p>if you don't you need to create the relevant database(empty) in MySQL, for that first log on to  the <code>MySQL</code> console by running the following command in terminal or in cmd</p>

<pre><code>mysql -u userName -p;</code></pre>

<p>and when prompted provide the password.</p>

<p>Next create a database and use it</p>

<pre><code>mysql&gt;create database yourDatabaseName;
mysql&gt;use yourDatabaseName;</code></pre>

<p>Then import the <code>sql</code> or the <code>dump</code> file to the database from</p>

<pre><code>mysql&gt; source pathToYourSQLFile;</code></pre>

<p>Note: if your terminal is not in the location where the <code>dump</code> or <code>sql</code> file exists, use the relative path in above.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-45998128">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-45576629">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Similarly to <a href="https://stackoverflow.com/a/17666285/1888983" target="_blank">https://stackoverflow.com/a/17666285/1888983</a><br />
Key differences for me:</p>

<ol>
<li>The database has to exist first</li>
<li>No space between <code>-p</code> and the password</li>
</ol>

<hr />

<pre><code>shell&gt; mysql -u root -ppassword #note: no space between -p and password
mysql&gt; CREATE DATABASE databasename;
mysql&gt; using databasename;
mysql&gt; source /path/to/backup.sql</code></pre>

<p>Running fedora 26 with MariaDB.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Aug 8 '17 at 19:30
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-45576629">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>1</b> more comment</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-39115498">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        28
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Solution that worked for me is below:</p>

<pre><code>Use your_database_name;
SOURCE path_to_db_sql_file_on_your_local;</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-39115498">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>2</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-42754014">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I'm using Windows 10 with Powershell 5 and I found almost all "unix-like" solutions not working for me.</p>

<pre><code>&gt; mysql -u[username] [database-name] &lt; my-database.sql
At line:1 char:31
+ mysql -u[username] [database-name] &lt; my-database.sql
+                               ~
The '&lt;' operator is reserved for future use.
    + CategoryInfo          : ParserError: (:) [], ParentContainsErrorRecordException
    + FullyQualifiedErrorId : RedirectionNotSupported</code></pre>

<p>I ends up using this command.</p>

<pre><code>&gt; type my-database.sql | mysql -u[username] -h[localhost] -p [database-name]</code></pre>

<p>and it works perfectly, hopefully it helps.</p>

<p>Thanks to @<a href="https://stackoverflow.com/users/828366/francesco-casula" target="_blank">Francesco Casula</a>'s <a href="https://stackoverflow.com/a/39125080/881743" target="_blank">answer</a> btw.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-42754014">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-39125080">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        13
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I think it's worth mentioning that you can also load a <strong>gzipped (compressed)</strong> file with <code>zcat</code> like shown below:</p>

<pre><code>zcat database_file.sql.gz | mysql -u username -p -h localhost database_name</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-39125080">
		        <table>
                    <tbody>



    <tr id="comment-66409854">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Not sure I follow. The source file is compressed in the archive you're zcatting. In my example inside <code>database_file.sql.gz</code>.
                    – <a href="/users/828366/francesco-casula" title="11,358 reputation" target="_blank">Francesco Casula</a>
                <a href="#comment66409854_39125080" target="_blank">Sep 17 '16 at 16:05</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-39125080">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-42450834">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Providing credentials on the command line is not a good idea. The above answers are great, but neglect to mention</p>

<pre><code>mysql --defaults-extra-file=etc/myhost.cnf database_name &lt; file.sql</code></pre>

<p>Where etc/myhost.cnf is a file that contains host, user, password, and you avoid exposing the password on the command line. Here is a sample,</p>

<pre><code>[client]
host=hostname.domainname
user=dbusername
password=dbpassword</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Feb 25 '17 at 1:18
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-42450834">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-41470089">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        17
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>To dump a database into a SQL file use the following command</p>

<pre><code>mysqldump -u username -p database_name &gt; database_name.sql</code></pre>

<p>To import a SQL file into a database (make sure you are in the same directory as the SQL file or supply the full path to the file)</p>

<pre><code>mysql u -username -p database_name &lt; database_name.sql</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jan 4 '17 at 17:42
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-41470089">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-41381838">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        4
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>For information I just had default root + withoutpassword, it didn't works with all above answers. </p>

<ul>
<li><p>I created a new user with all privileges and a password. It works. </p></li>
<li><p>-ppassword WITHOUT SPACE. </p></li>
</ul>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 29 '16 at 14:40
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-41381838">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-22855514">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        186
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Regarding the time taken for importing huge files: most importantly, it takes more time because the default setting of MySQL is <code>autocommit = true</code>. You must set that off before importing your file and then check how import works like a gem.</p>

<p>You just need to do the following thing:</p>

<pre><code>mysql&gt; use db_name;

mysql&gt; SET autocommit=0 ; source the_sql_file.sql ; COMMIT ;</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-22855514">
		        <table>
                    <tbody>



    <tr id="comment-44531024">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                4
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Is there a way to do that in a single command line on the mysql command used for import?
                    – <a href="/users/105539/volomike" title="12,317 reputation" target="_blank">Volomike</a>
                <a href="#comment44531024_22855514" target="_blank">Jan 21 '15 at 20:12</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-62310561">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                8
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I agree that this is <b>the best answer</b>. The <code>autocommit=0</code> portion made a world of difference in terms of the speed.
                    – <a href="/users/722036/the-sexiest-man-in-jamaica" title="1,404 reputation" target="_blank">The Sexiest Man in Jamaica</a>
                <a href="#comment62310561_22855514" target="_blank">May 23 '16 at 21:36</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-69314145">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                will the <code>autocommit=0</code> will work on larger files? like 8gb sql file.
                    – <a href="/users/2761390/newbie" title="695 reputation" target="_blank">newbie</a>
                <a href="#comment69314145_22855514" target="_blank">Dec 9 '16 at 5:06</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-22855514">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>1</b> more comment</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-39017909">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        43
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Among all the answers, for the problem above, this is the best one:</p>

<pre><code> mysql&gt; use db_name;
 mysql&gt; source file_name.sql;</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Aug 18 '16 at 12:12
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-39017909">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-38887596">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I kept running into the problem where the database wasn't created.</p>

<p>I fixed it like this</p>

<pre><code>mysql -u root -e "CREATE DATABASE db_name"
mysql db_name --force &lt; import_script.sql</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Aug 11 '16 at 5:02
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-38887596">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-25051722">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<h3>Import a database</h3>

<ol>
<li><p>Go to drive:</p>

<pre><code>command: d:</code></pre></li>
<li><p>MySQL login</p>

<pre><code>command: c:\xampp\mysql\bin\mysql -u root -p</code></pre></li>
<li><p>It will ask for pwd. Enter it:</p>

<pre><code>pwd</code></pre></li>
<li><p>Select the database</p>

<pre><code>use DbName;</code></pre></li>
<li><p>Provide the file name</p>

<pre><code>\.DbName.sql</code></pre></li>
</ol>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-25051722">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-25474834">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Add the <a href="http://dev.mysql.com/doc/refman/5.0/en/mysql-command-options.html#option_mysql_force" target="_blank"><code>--force</code> option</a>:</p>

<pre><code>mysql -u username -p database_name --force &lt; file.sql</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-25474834">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-30274932">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        10
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>For importing multiple SQL files at one time, use this:</p>

<pre><code>#Unix-based solution
for i in *.sql;do mysql -u root -pPassword DataBase &lt; $i;done</code></pre>

<p>For simple importing:</p>

<pre><code>#Unix Based solution
mysql -u root -pPassword DataBase &lt; data.sql</code></pre>

<p>For <a href="http://en.wikipedia.org/wiki/WAMP" target="_blank">WAMP</a>:</p>

<pre><code>#mysqlVersion replace with your own version
C:\wamp\bin\mysql\mysqlVersion\bin\mysql.exe -u root -pPassword DataBase &lt; data.sql</code></pre>

<p>for Xampp</p>

<pre><code>C:\xampp\mysql\bin\mysql -u root -pPassword DataBase &lt; data.sql</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-30274932">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-30431609">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        16
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>To import a single database, use the following commands.</p>

<pre><code>mysql -u username -p password dbname &lt; dump.sql</code></pre>

<p>For multiple database dumps, use the following commands.</p>

<pre><code>mysql -u username -p password &lt; dump.sql</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-30431609">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-32364858">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        10
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>You do not need to specify the name of the database on the command line if the .sql file contains <code>CREATE DATABASE IF NOT EXISTS db_name</code> and <code>USE db_name</code> statements.</p>

<p>Just make sure you are connecting with a user that has the permissions to create the database, if the database mentioned in the .sql file does not exist.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-32364858">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-34377402">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If your folder has multiple SQL files, and you've installed <a href="https://stackoverflow.com/questions/17807485" target="_blank">Git Bash</a> you can use this command to import multiple files:</p>

<pre><code>cd /my-project/data

cat *.sql | /c/xampp/mysql/bin/mysql -u root -p 1234 myProjectDbName</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-34377402">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-36718618">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Export particular databases:</p>

<pre><code> djimi:&gt; mysqldump --user=root --host=localhost --port=3306 --password=test -B CCR KIT &gt; ccr_kit_local.sql</code></pre>

<p>This will export CCR and KIT databases...</p>

<p>Import all exported databases to a particular MySQL instance (you have to be where your dump file is):</p>

<pre><code>  djimi:&gt; mysql --user=root --host=localhost --port=3306 --password=test &lt; ccr_kit_local.sql</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-36718618">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-28991002">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>The following command works for me from the command line (cmd) on 
Windows 7 on <a href="http://en.wikipedia.org/wiki/WAMP" target="_blank">WAMP</a>.</p>

<pre><code>d:/wamp/bin/mysql/mysql5.6.17/bin/mysql.exe -u root -p db_name &lt; database.sql</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-28991002">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-27981805">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>The following steps help to upload <code>file.sql</code> to the MySQL database.</p>

<p>Step 1: Upload <code>file.sql.zip</code> to any directory and unzip there <br />
<strong>Note</strong>: <code>sudo apt-get install unzip</code>
: <code>sudo apt-get unzip file.sql.zip</code><br />
Step 2: Now navigate to that directory. Example: <code>cd /var/www/html</code></p>

<p>Step 3: <code>mysql -u username -p database-name &lt; file.sql</code><br /> 
         Enter the password and wait till uploading is completed.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-27981805">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-27744820">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        41
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<ol>
<li>Open the MySQL command line</li>
<li>Type the path of your mysql bin directory and press <kbd>Enter</kbd></li>
<li>Paste your SQL file inside the <code>bin</code> folder of mysql server.</li>
<li>Create a database in MySQL.</li>
<li>Use that particular database where you want to import the SQL file.</li>
<li>Type <code>source databasefilename.sql</code> and <kbd>Enter</kbd></li>
<li>Your SQL file upload successfully.</li>
</ol>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-27744820">
		        <table>
                    <tbody>



    <tr id="comment-76745885">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                ype the path of your mysql bin directory and press
                    – <a href="/users/4183221/ramesh-pareek" title="677 reputation" target="_blank">Ramesh Pareek</a>
                <a href="#comment76745885_27744820" target="_blank">Jul 3 '17 at 11:03</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-27744820">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-27283712">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If you are using <a href="https://en.wikipedia.org/wiki/MAMP" target="_blank">MAMP</a> on Mac OS X, this may be helpful:</p>

<pre><code>/applications/MAMP/library/bin/mysql -u MYSQL_USER -p DATABASE_NAME &lt; path/to/database_sql/FILE.sql</code></pre>

<p>MYSQL_USER is root by default.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-27283712">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-26831942">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I thought it could be useful for those who are using <a href="http://en.wikipedia.org/wiki/Mac_OS_X" target="_blank">Mac OS X</a>:</p>

<pre><code>/Applications/xampp/xamppfiles/bin/mysql -u root -p database &lt; database.sql</code></pre>

<p>Replace <code>xampp</code> with <code>mamp</code> or other web servers.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-26831942">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-25724087">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        23
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Go to the directory where you have the MySQL executable. <code>-u</code> for username and <code>-p</code> to prompt for the password:</p>

<pre><code>C:\xampp\mysql\bin&gt;mysql -u username -ppassword databasename &lt; C:\file.sql</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-25724087">
		        <table>
                    <tbody>



    <tr id="comment-40218980">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I think it would be more helpful for the OP and further questions, when you add some explaination to your intension.
                    – <a href="/users/326807/reporter" title="2,943 reputation" target="_blank">reporter</a>
                <a href="#comment40218980_25724087" target="_blank">Sep 8 '14 at 13:59</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-25724087">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>1</b> more comment</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-25484464">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        4
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>For backup purposes, make a BAT file and run this BAT file using <a href="https://en.wikipedia.org/wiki/Windows_Task_Scheduler" target="_blank">Task Scheduler</a>. It will take a backup of the database; just copy the following line and paste in <a href="http://en.wikipedia.org/wiki/Notepad_%28software%29" target="_blank">Notepad</a> and then save the .bat file, and run it on your system.</p>

<pre><code>@echo off
for /f "tokens=1" %%i in ('date /t') do set DATE_DOW=%%i
for /f "tokens=2" %%i in ('date /t') do set DATE_DAY=%%i
for /f %%i in ('echo %date_day:/=-%') do set DATE_DAY=%%i
for /f %%i in ('time /t') do set DATE_TIME=%%i
for /f %%i in ('echo %date_time::=-%') do set DATE_TIME=%%i

"C:\Program Files\MySQL\mysql server 5.5\bin\mysqldump" -u username -ppassword mysql&gt;C:/%DATE_DAY%_%DATE_TIME%_database.sql</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-25484464">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-23625564">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Sometimes the port defined as well as the server <a href="http://en.wikipedia.org/wiki/IP_address" target="_blank">IP address</a> of that database also matters...</p>

<pre><code>mysql -u user -p user -h &lt;Server IP&gt; -P&lt;port&gt; (DBNAME) &lt; DB.sql </code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-23625564">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-22324351">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        38
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>We can use this command to import SQL from command line:</p>

<pre><code>mysql -u username -p password db_name &lt; file.sql</code></pre>

<p>For example, if the username is <code>root</code> and password is <code>password</code>. And you have a database name as <code>bank</code> and the SQL file is <code>bank.sql</code>. Then, simply do like this:</p>

<pre><code>mysql -u root -p password bank &lt; bank.sql</code></pre>

<p>Remember where your SQL file is. If your SQL file is in the <code>Desktop</code> folder/directory then go the desktop directory and enter the command like this:</p>

<pre><code>~ ? cd Desktop
~/Desktop ? mysql -u root -p password bank &lt; bank.sql</code></pre>

<p>And if your are in the <code>Project</code> directory and your SQL file is in the <code>Desktop</code> directory. If you want to access it from the <code>Project</code> directory then you can do like this:</p>

<pre><code>~/Project ? mysql -u root -p password bank &lt; ~/Desktop/bank.sql</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-22324351">
		        <table>
                    <tbody>



    <tr id="comment-39584529">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                11
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                There shouldn't be a space between <code>-p</code> and <code>password</code>
                    – <a href="/users/2219831/ejaz" title="6,818 reputation" target="_blank">Ejaz</a>
                <a href="#comment39584529_22324351" target="_blank">Aug 19 '14 at 12:00</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-50371293">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                why you simply can't answer in one line?  <code>mysql -u username -ppassword db_name &lt; file.sql</code>
                    – <a href="/users/671046/naveed" title="8,752 reputation" target="_blank">Naveed</a>
                <a href="#comment50371293_22324351" target="_blank">Jul 2 '15 at 11:11</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-22324351">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>2</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            


            
    






                            

                                                            
                        
                            
                            



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/mysql" title="show questions tagged 'mysql'" target="_blank">mysql</a> <a href="/questions/tagged/sql" title="show questions tagged 'sql'" target="_blank">sql</a> <a href="/questions/tagged/command-line" title="show questions tagged 'command-line'" target="_blank">command-line</a> <a href="/questions/tagged/import" title="show questions tagged 'import'" target="_blank">import</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
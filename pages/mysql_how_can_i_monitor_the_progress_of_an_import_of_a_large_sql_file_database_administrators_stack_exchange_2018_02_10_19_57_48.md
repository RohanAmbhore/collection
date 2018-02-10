<a href="https://dba.stackexchange.com/questions/17367/how-can-i-monitor-the-progress-of-an-import-of-a-large-sql-file">https://dba.stackexchange.com/questions/17367/how-can-i-monitor-the-progress-of-an-import-of-a-large-sql-file</a><div id="articleHeader"><h1><a href="/questions/17367/how-can-i-monitor-the-progress-of-an-import-of-a-large-sql-file" target="_blank">How can I monitor the progress of an import of a large .sql file?</a></h1></div>
            

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        143
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>52</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I am importing a 7 GB <code>foobar.sql</code> to restore a table in a local database.  </p>

<pre><code>$ mysql -h localhost -u root 'my_data' &lt; foobar.sql

$ mysql --version
/usr/local/mysql/bin/mysql  Ver 14.12 Distrib 5.0.96, for apple-darwin9.8.0 (i386) using readline 5.1</code></pre>

<p>How can I monitor its progress?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-17367">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-28646">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        183
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>If you're  just importing from a dump file from the CLI on *nix, e.g.</p>

<pre><code>mysql -uxxx -pxxx dbname &lt; /sqlfile.sql</code></pre>

<p>then first install <a href="https://www.ivarch.com/programs/pv.shtml" target="_blank">pipe viewer</a> on your OS then try something like this:</p>

<pre><code>pv sqlfile.sql | mysql -uxxx -pxxxx dbname</code></pre>

<p>which will show a progress bar as the program runs.  </p>

<p>It's very useful and you can also use it to get an estimate for mysqldump progress.</p>

<p>pv dumps the <code>sqlfile.sql</code> and passes them to mysql (because of the pipe operator). While it is dumping, it shows the progress. The cool thing is that mysql takes the data only as fast as it can progress it, so pv can show the progress of the import. I do not have any proof. But it seems so. I guess there is some buffer used, but at some point I think <code>mysql</code> does not read any more data when it is still busy processing.</p>

<p><a href="https://i.stack.imgur.com/ibmzD.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/ibmzD.png" alt="Pipe Viewer screenshot" /></div></a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-28646">
                <ul>



    <li id="comment-202836">
        
        <div>
            <div>
                I would guess that mysql might have a buffer, in which some data can be piped in, without being fully "processed" (i.e. if it errors out, pv may have slightly over-reported what actually gets in). But in general, this is how pipes work. It's the same reason you can do <code>sudo hd /dev/sda1 | less</code> and not have your entire system partition in memory.
                    – <a href="/users/15396/snapfractalpop" title="101 reputation" target="_blank">snapfractalpop</a>
                <a href="#comment202836_28646" target="_blank">Aug 21 '15 at 15:34</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-234272">
        
        <div>
            <div>
                @snapfractalpop <code>pv</code> won't be overly accurate in many cases because some chunks of SQL will take more time to process than others. A line that constitutes a simple insert will run a lot faster than one that creates on index on a table that already has many rows, for instance. <i>But</i> a a rough idea of progress the output should be helpful unless the read buffer used by <code>mysql</code> is particularly large (for a 7Gb input the buffer would need to be very large to render <code>pv</code>'s output not useful at all.
                    – <a href="/users/61/david-spillett" title="19,822 reputation" target="_blank">David Spillett</a>
                <a href="#comment234272_28646" target="_blank">Jan 20 '16 at 14:38</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-234286">
        
        <div>
            <div>
                @DavidSpillett indeed. Your comment mirrors my sentiment. Basically, pv is crude, but effective. What I like most about it is how general it is. Such is the beauty of unix pipes (thank you McIlroy).
                    – <a href="/users/15396/snapfractalpop" title="101 reputation" target="_blank">snapfractalpop</a>
                <a href="#comment234286_28646" target="_blank">Jan 20 '16 at 15:19</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-263109">
        
        <div>
            <div>
                @rob This is awesome dude, could you also provide an example with <code>mysqldump</code>?
                    – <a href="/users/71355/josue-alexander-ibarra" title="101 reputation" target="_blank">Josue Alexander Ibarra</a>
                <a href="#comment263109_28646" target="_blank">May 26 '16 at 18:03</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-315739">
        
        <div>
            <div>
                Very nice solution ! If the password is manual, pv does not wait for it to display its progression though
                    – <a href="/users/29610/pierre-de-lespinay" title="101 reputation" target="_blank">Pierre de LESPINAY</a>
                <a href="#comment315739_28646" target="_blank">Feb 10 '17 at 14:40</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-28646">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-53172">
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
<p>If you've already started the import, you can execute this command in another window to see the current size of your databases. This can be helpful if you know the total size of the .sql file you're importing.</p>

<pre><code>SELECT table_schema "Data Base Name", sum( data_length + index_length ) / 1024 / 1024 "Data Base Size in MB" 
FROM information_schema.TABLES GROUP BY table_schema;  </code></pre>

<p>Credit to: <a href="http://forums.mysql.com/read.php?108,201578,201578" target="_blank">http://forums.mysql.com/read.php?108,201578,201578</a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-53172">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-17369">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        15
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>When you execute a mysqldump of a single database, all tables are dumped in alphabetical order.</p>

<p>Naturally, the reload of the mysqldump into a database would also be in alphabetical order.</p>

<p>You could just do a SHOW PROCESSLIST; and find out the DB Connection running the mysqldump. When the dump is reloaded, the DB Connection will vanish.</p>

<p>If you want to know what tables are in the dumpfile, run this against foobar.sql</p>

<pre><code>cat foobar.sql | grep "^CREATE TABLE" | awk '{print $3}'</code></pre>

<h2><strong>UPDATE 2012-05-02 13:53 EDT</strong></h2>

<p>Sorry for not noticing that there is only one table.</p>

<p>If the table is MyISAM, the only way to monitor is from the OS point of view. The reason? The table is write-locked throughout the reload. What do you look for? The size of the <code>.MYD</code> and <code>.MYI</code> files. Of course, you need to compare that with what the table size was before on the other DB server you imported from.</p>

<p>If the table is InnoDB and you have <a href="http://dev.mysql.com/doc/refman/5.5/en/innodb-parameters.html#sysvar_innodb_file_per_table" target="_blank"><strong>innodb_file_per_table</strong></a> enabled, the only way to monitor is from the OS point of view. The reason? The table is write-locked throughout the reload. What do you look for? The size of the <code>.ibd</code> file. Of course, you need to compare that with what the table size was before on the other DB server you imported from.</p>

<p>If the table is InnoDB and you have <strong>innodb_file_per_table</strong> disabled, not even the OS point of view can help.</p>

<h2><strong>UPDATE 2012-05-02 13:56 EDT</strong></h2>

<p>I addressed something like this last year : <a href="https://dba.stackexchange.com/questions/1282/how-do-i-get-progress-for-type-db-sql-mysql/1307#1307" target="_blank">How do I get % progress for "type db.sql | mysql"</a></p>

<h2><strong>UPDATE 2012-05-02 14:09 EDT</strong></h2>

<p>Since a standard mysqldump write-locks the table like this:</p>

<pre><code>LOCK TABLES `a` WRITE;
/*!40000 ALTER TABLE `a` DISABLE KEYS */;
INSERT INTO `a` VALUES (123),(451),(199),(0),(23);
/*!40000 ALTER TABLE `a` ENABLE KEYS */;
UNLOCK TABLES;</code></pre>

<p>then, there is no way to get a progress from with mysql until the table lock is released.</p>

<p>If you can get <code>LOCK TABLES</code> and <code>UNLOCK TABLES</code> commented out of the dumpfile...</p>

<ul>
<li>if the table is MyISAM, SELECT COUNT(*) would work</li>
<li>if the table is InnoDB, SELECT COUNT(*) would probably slow down/halt the load until count is done</li>
</ul>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-17369">
                <ul>



    <li id="comment-26988">
        
        <div>
            <div>
                That worked.  Thanks.  One last question is, by experience, do you know if the importing time is roughly <b>linear</b> with respect to the <code>.MYD</code> and <code>.MYI</code> file sizes?
                    – <a href="/users/7169/qazwsx" title="943 reputation" target="_blank">qazwsx</a>
                <a href="#comment26988_17369" target="_blank">May 2 '12 at 21:06</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-26990">
        
        <div>
            <div>
                Table reload is linear. Index rebuilds are linear. Years ago, it was not as I ventured this as a question to MySQL ( <a href="http://lists.mysql.com/mysql/202489" target="_blank">lists.mysql.com/mysql/202489</a> ) and I mentioned it in the DBA StackExchange ( <a href="http://dba.stackexchange.com/a/2697/877" target="_blank">dba.stackexchange.com/a/2697/877</a> )
                    – <a href="/users/877/rolandomysqldba" title="128,617 reputation" target="_blank">RolandoMySQLDBA</a>
                <a href="#comment26990_17369" target="_blank">May 2 '12 at 21:12</a>
                        
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-17369">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-86536">
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
<p>As a solution for someone who can't get pv to work or for whom pv tells lies. You can monitor the size of ibdata1 file in /var/lib/mysql which contains the data. This will end up the same size (or thereabouts)  of the filesize in your source server.</p>

<p>If there are many tables you can also watch them appear one by one in /var/lib/mysql/&lt; database name&gt;.</p>

<p>I happened to use this fact recently when a long term database had built up a log file of around 20G over a period of three or four years. I noticed the transfer was taking ages and used this technique to monitor progress.</p>

<p>I think that it is highly unlikely that the day will dawn when a database does not involve a file somewhere or other. Meanwhile, you can monitor the file to see how a transfer is progressing. The method I suggested has been something you could do in one form or another since the first sql database was written. I never intended to suggest that it was any kind of "official" technique that a manual jockey could fall back on. It assumes a general level of proficiency with computers in general and unix in particular.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-86536">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-157671">
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
<p>Every 2 seconds you will see the processes running.</p>

<pre><code>watch 'echo "show processlist;" | mysql -uuser -ppassword';</code></pre>

<p>If you want it less frequent then add <code>-n x</code> where <em>x</em> is the number of seconds. 5 seconds would be:</p>

<pre><code>watch -n 5 'echo "show processlist;" | mysql -uuser -ppassword';</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-157671">
                <ul>



    <li id="comment-302298">
        
        <div>
            <div>
                Can you post a example output? Also, does it just show the process or does it really indicate the progress of the import, which was really I was asking for?
                    – <a href="/users/7169/qazwsx" title="943 reputation" target="_blank">qazwsx</a>
                <a href="#comment302298_157671" target="_blank">Dec 9 '16 at 17:29</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-352912">
        
        <div>
            <div>
                This is such a helpful code. Thankyou
                    – <a href="/users/95750/narayan" title="113 reputation" target="_blank">NarayaN</a>
                <a href="#comment352912_157671" target="_blank">Aug 5 '17 at 20:52</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-157671">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-123847">
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
<p>If you just want to check if it is stalled you can query </p>

<pre><code>show processlist; </code></pre>

<p>and see what is being executed.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 16 '15 at 17:12
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
	    

        <div id="comments-link-123847">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-195295">
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
<p>For someone who is looking for the pipe viewer example using <code>mysqldump</code> you would just doing something like this:</p>

<pre><code>mysqldump -hxxx -uxxx -p dbname | pv -W &gt; dump.sql</code></pre>

<p>The <code>-W</code> flag just tells pv to wait for the first byte to come before showing the progress (after the prompt)</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-195295">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-158786">
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
<p>If your DB is otherwise quiet (i.e. there are not other users active) and you want to just see read/write activity why not just do something like:</p>

<pre><code>mysqladmin -h&lt;host&gt;-uroot -p&lt;yourpass&gt; extended -r -i 10 |grep 'row'</code></pre>

<p>You will see number of reads/writes/inserts/waits/updates.</p>

<p>If you are inserting for example you will see something like:</p>

<pre><code>Innodb_rows_inserted                          | 28958 </code></pre>

<p>Where 28958 is the number of rows inserted for your interval (10 seconds in my case).</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-158786">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-128189">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I'm so surprised no one just posted 'mysql -v' as an option. If it gets stuck, the output will stop. </p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-128189">
                <ul>



    <li id="comment-237988">
        
        <div>
            <div>
                "Monitoring progress" commonly means trying to estimate how far the process has progressed or when would it complete, which <code>mysql -v</code> won't offer. Also, spewing 7 GB of data to the terminal will <i>significantly</i> slow down the restore.
                    – <a href="/users/23721/mustaccio" title="7,176 reputation" target="_blank">mustaccio</a>
                <a href="#comment237988_128189" target="_blank">Feb 3 '16 at 19:25</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-238010">
        
        <div>
            <div>
                i see, thanks for the explanation. thats true, the output of 7 GB would not be good to output into the terminal. i guess me using -v was just for a small local test case where my db would just get stuck.
                    – <a href="/users/86294/dtc" title="103 reputation" target="_blank">dtc</a>
                <a href="#comment238010_128189" target="_blank">Feb 3 '16 at 20:46</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-244295">
        
        <div>
            <div>
                This suggestion helped me pinpoint a problem, however impractical it might be for using with large files. (Mine was small).
                    – <a href="/users/88260/jason-tyler" title="101 reputation" target="_blank">Jason Tyler</a>
                <a href="#comment244295_128189" target="_blank">Feb 26 '16 at 15:46</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-128189">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


        






                            <div>
                                
                                            <div>
        
                <div>
                    <div>
                        <h3>Sign up or <a href="/users/login?ssrc=question_page&returnurl=https%3a%2f%2fdba.stackexchange.com%2fquestions%2f17367%2fhow-can-i-monitor-the-progress-of-an-import-of-a-large-sql-file%23new-answer" id="login-link" target="_blank">log in</a></h3>
                        
                        <div>
                             Sign up using Google
                        </div>
                        <div>
                             Sign up using Facebook
                        </div>
                        <div>
                             Sign up using Email and Password
                        </div>
                    </div>
                    
                    
                    
                    
                    <div>
                                <h3>Post as a guest</h3>
    <div>
        <table>
        <tbody><tr>
                    <td>
                <div>
                    <label>Name</label>
                    
                </div>
                <div>
                    <label>Email</label>
                    
                </div>
            </td>
        </tr>
        </tbody></table>
    </div>

                    </div>
                </div>
            </div>
            
            

                            </div>

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>

<p>
By posting your answer, you agree to the <a href="https://stackexchange.com/legal/privacy-policy" name="privacy" target="_blank">privacy policy</a> and <a href="https://stackexchange.com/legal/terms-of-service" name="tos" target="_blank">terms of service</a>.</p>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/mysql" title="show questions tagged 'mysql'" target="_blank">mysql</a> <a href="/questions/tagged/mysqldump" title="show questions tagged 'mysqldump'" target="_blank">mysqldump</a> <a href="/questions/tagged/import" title="show questions tagged 'import'" target="_blank">import</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
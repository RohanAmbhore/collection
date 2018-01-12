<a href="https://dba.stackexchange.com/questions/11806/why-is-drop-database-taking-so-long-mysql">https://dba.stackexchange.com/questions/11806/why-is-drop-database-taking-so-long-mysql</a><div id="articleHeader"><h1><a href="/questions/11806/why-is-drop-database-taking-so-long-mysql" target="_blank">Why is DROP DATABASE taking so long? (MySQL)</a></h1></div>
            

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        34
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>12</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>New CentOS installation.</p>

<p>I was running an import of a large DB (2GB sql file) and had a problem. The SSH client seemed to lose the connection and the import seemed to freeze. I used another window to login to mysql and the import appeared to be dead, stuck on a particular 3M row table.</p>

<p>So I tried </p>

<pre><code>DROP DATABASE huge_db;</code></pre>

<p>15-20 minutes later, nothing. In another window, I did:</p>

<pre><code>/etc/init.d/mysqld restart</code></pre>

<p>The DROP DB window messaged: SERVER SHUTDOWN.
Then I actually restarted the physical server.</p>

<p>Logged back into mysql, checked and the db was still there, ran</p>

<pre><code>DROP DATABASE huge_db;</code></pre>

<p>again, and again I'm waiting already about 5 minutes.</p>

<p>Once again, it's fresh installation. The <code>huge_db</code> is the only db (other than system dbs). I swear I've dropped db's this large before and quickly, but maybe I'm wrong.</p>

<p>EDIT:</p>

<p>I've successfully dropped the database. It took something like 30 minutes. Also note that I think I was mistaken when I thought the mysqldump import was dead. The terminal connection was lost, but I think the process was still running. I most-likely killed the import mid-table (the 3M row table) and probably 3/4 of the way through the whole db. It was misleading that "top" showed mysql using only 3% of memory, when it seemed like it should be using more.</p>

<p>Dropping the DB ended up taking 30 min, so, again, I might not have had to restart the server and possibly could have just waited for the DROP to finish, but I don't know how mysql would react to getting a DROP query for the same db that it's importing via mysqldump.</p>

<p>Still, the question remains, why does it take 30min+ to DROP a 2GB database when all it should have to do is delete all the db files and remove all references to the DB from information_schema? What's the big deal?</p>
    </div>
    
    
</div>
</td>
        </tr>
                    <tr>
            <td colspan="2">
                <div>
        <h2>                    <b>migrated</b> from <a href="//serverfault.com/posts/354226/revisions" title="why-is-drop-database-taking-so-long-mysql" target="_blank">serverfault.com</a> Jan 27 '12 at 17:40
</h2>
        <p>This question came from our site for system and network administrators.</p>
    </div>
            </td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-11806">
		        <table>
                    <tbody>



    <tr id="comment-17699">
        <td>
            
        </td>
        <td>
            <div>
                Out of curiosity, what does <code>SHOW FULL PROCESSLIST</code> report while the database drop is busy spinning its wheels? That's usually the first place I look when some query is taking substantially longer than expected.
                    – <a href="/users/1514/db2" title="7,293 reputation" target="_blank">db2</a>
                <a href="#comment17699_11806" target="_blank">Jan 27 '12 at 18:38</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-17738">
        <td>
            
        </td>
        <td>
            <div>
                Unfortunately I didn't get a chance to run your query, but I did use shell command "top" and MySQL was using very little resources, I think it was under 3% of memory.
                    – <a href="/users/6235/buttle-butkus" title="450 reputation" target="_blank">Buttle Butkus</a>
                <a href="#comment17738_11806" target="_blank">Jan 28 '12 at 1:12</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-17740">
        <td>
            
        </td>
        <td>
            <div>
                This is curious, if you find a solution post it as answer please.  The only thing the immediately comes to mind is the server is thrashing in paging so I/O grinds to halt.  If this were the case though you wouldn't even be able to maintain an ssh connection.  And for the record a 2 GB table is meh, let alone a 2 GB DB ;)
                    – <a href="/users/3423/atxdba" title="3,696 reputation" target="_blank">atxdba</a>
                <a href="#comment17740_11806" target="_blank">Jan 28 '12 at 2:13</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-20271">
        <td>
            
        </td>
        <td>
            <div>
                @db2: thank you 1000x for your comment! I had the same problem as the OP, and with your remark, I was able to kill an offending thread that I thought didn't exist.
                    – <a href="/users/515/ren%c3%a9-nyffenegger" title="2,563 reputation" target="_blank">René Nyffenegger</a>
                <a href="#comment20271_11806" target="_blank">Feb 18 '12 at 20:58</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-354969">
        <td>
            
        </td>
        <td>
            <div>
                I just dropped a +600M rows table (&gt;100GB compressed InnnoDB) on a moderately-spec'd home computer, it did take about 10 minutes which was more than expected. In your case, what may have made it even worse is that the aborted backup may have been rolling back the transaction which can be very slow.
                    – <a href="/users/57465/thomas-guyot-sionnest" title="101 reputation" target="_blank">Thomas Guyot-Sionnest</a>
                <a href="#comment354969_11806" target="_blank">Aug 17 '17 at 6:44</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-11806">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-37646">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        51
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>Rather than killing the process (as in the accepted answer) it would be safer if you did it within MySQL:</p>

<pre><code>$ mysqladmin processlist -u root -p
Enter password: 
+-----+------+-----------+-------------------+---------+------+-------+------------------+
| Id  | User | Host      | db                | Command | Time | State | Info             |
+-----+------+-----------+-------------------+---------+------+-------+------------------+
| 174 | root | localhost | example           | Sleep   | 297  |       |                  |
| 407 | root | localhost |                   | Query   | 0    |       | show processlist |
+-----+------+-----------+-------------------+---------+------+-------+------------------+</code></pre>

<p>The query with id 174 is the one blocking deletion of the 'example' database, so before you kill any processes first let MySQL try to terminate the query:</p>

<pre><code>$ mysqladmin kill 174</code></pre>

<p>Run the processlist command above again to confirm that it was killed.</p>

<p>If this doesn't work, then you could perhaps look at killing the errant process, but before that you might try restarting the MySQL server.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-37646">
		        <table>
                    <tbody>



    <tr id="comment-67973">
        <td>
            
        </td>
        <td>
            <div>
                is mysqladmin a standard api? I have never used it. I usually use mysql command line or phpmyadmin.
                    – <a href="/users/6235/buttle-butkus" title="450 reputation" target="_blank">Buttle Butkus</a>
                <a href="#comment67973_37646" target="_blank">Mar 28 '13 at 2:37</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-68401">
        <td>
            
        </td>
        <td>
            <div>
                Yes, it's part of the MySQL server install. You can also run commands like 'SHOW FULL PROCESSLIST' and 'KILL 174' in the MySQL shell, for example if you only have the MySQL client installed.  The main point is to avoid killing the process using 'kill' in the shell unless absolutely necessary.
                    – <a href="/users/21809/stefan-magnuson" title="626 reputation" target="_blank">Stefan Magnuson</a>
                <a href="#comment68401_37646" target="_blank">Apr 1 '13 at 4:35</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-68611">
        <td>
            
        </td>
        <td>
            <div>
                Thanks. Any reason why you use mysqladmin instead of mysql? It seems like you have to type "mysqladmin" in front of every command. That would get tedious fast.
                    – <a href="/users/6235/buttle-butkus" title="450 reputation" target="_blank">Buttle Butkus</a>
                <a href="#comment68611_37646" target="_blank">Apr 2 '13 at 23:17</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-71341">
        <td>
            
        </td>
        <td>
            <div>
                Generally speaking you can use either. You shouldn't need to be running commands like this that often though; once you start killing queries regularly something is definitely wrong and you'd be better off fixing that problem (killing the query process is just treating the symptom).
                    – <a href="/users/21809/stefan-magnuson" title="626 reputation" target="_blank">Stefan Magnuson</a>
                <a href="#comment71341_37646" target="_blank">Apr 23 '13 at 0:54</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-37646">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-12175">
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
<p>As per the edit in my question, I believe this is the answer:</p>

<p>Though I thought that the import process had died, it was probably still running.</p>

<p>The DROP DATABASE command probably waited for the database to finish importing before it ran.</p>

<p>So, rather than DROP DATABASE taking a long time, it was probably just the import.</p>

<p>If anyone else reads this and is trying to cancel a database import and drop the database, I recommend you first find the PID (process id) for the import and run this from a different terminal:</p>

<pre><code>$ kill [PID]</code></pre>

<p>...where [PID] would be the actual PID for the process.</p>

<p>You should see the import halt immediately if the other terminal is still connected.</p>

<p>You could also run <code>SHOW PROCESSLIST</code> in the phpMyAdmin SQL tab. The resulting table shows running processes, and clicking the 'x' next to the row you want to kill should do the trick.</p>

<p>Then run </p>

<pre><code>DROP DATABASE `database_name`;</code></pre>

<p>And everything should be clean.</p>

<p>EDIT:</p>

<p>Another answer suggested that killing the process within mysql is better than doing it from outside. I have not tested that answer, but it sounds very plausible. So I have marked it as "best answer" instead of this one.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-12175">
		        <table>
                    <tbody>



    <tr id="comment-204236">
        <td>
            
        </td>
        <td>
            <div>
                I killed the mysql process from windows taks manager and then it all started working again. Thanks.
                    – <a href="/users/66504/moishe-lipsker" title="101 reputation" target="_blank">Moishe Lipsker</a>
                <a href="#comment204236_12175" target="_blank">Aug 28 '15 at 1:31</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-12175">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-11807">
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
<p>Try to truncate the largest tables in youra database before you drop it. I saw very similar behavior when working with MySQL archives of firewall traffic and this helped immensely. </p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-11807">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-12216">
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
<p>The first thing that comes to mind is the status <code>Checking Permissions...</code></p>

<p>When you issue <code>DROP DATABASE mydb;</code> everything inside /var/lib/mysql/mydb is checked to see if OS permissions exists for the right to drop every file.</p>

<p><a href="https://serverfault.com/a/238436/69271" target="_blank">Some have felt that reducing  the number of mysql users may help</a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-12216">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-20771">
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
<p>I faced the same problem . But this time I checked show processlist; it said checking for permissions for longer time. Then I found that mysqld_safe was running as root whereas folder level permissions was only for mysql user. Hence I killed the query, ofcourse it took long time saying its in killed state but I waited for it to react then it killed the query and changed the folder level permissions to root also by adding it to group and chmod to 770. Then I executed the same drop database blah; it did work for me in 2 secs for 20GB database. </p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 12 '12 at 9:04
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
	    <div id="comments-20771">
		        <table>
                    <tbody>



    <tr id="comment-141925">
        <td>
            
        </td>
        <td>
            <div>
                I just read this. I think is very brilliant. I knew from my answer that it was file permissions, but I never dreamed of doing chmod. I may try this in the future when it is called for and I'll let you know. +1 !!!
                    – <a href="/users/877/rolandomysqldba" title="127,532 reputation" target="_blank">RolandoMySQLDBA</a>
                <a href="#comment141925_20771" target="_blank">Oct 2 '14 at 12:59</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-251226">
        <td>
            
        </td>
        <td>
            <div>
                Very interesting. @RolandoMySQLDBA have you tried this yet? If this works so well, I wonder why MySQL does not set permissions like this automatically.
                    – <a href="/users/6235/buttle-butkus" title="450 reputation" target="_blank">Buttle Butkus</a>
                <a href="#comment251226_20771" target="_blank">Mar 30 '16 at 0:38</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-20771">

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
                        <h3>Sign up or <a href="/users/login?ssrc=question_page&returnurl=https%3a%2f%2fdba.stackexchange.com%2fquestions%2f11806%2fwhy-is-drop-database-taking-so-long-mysql%23new-answer" id="login-link" target="_blank">log in</a></h3>
                        
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/mysql" title="show questions tagged 'mysql'" target="_blank">mysql</a> <a href="/questions/tagged/mysqldump" title="show questions tagged 'mysqldump'" target="_blank">mysqldump</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
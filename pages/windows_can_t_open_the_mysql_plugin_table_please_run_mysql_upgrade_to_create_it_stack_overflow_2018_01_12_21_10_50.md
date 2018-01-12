<a href="https://stackoverflow.com/questions/41531225/cant-open-the-mysql-plugin-table-please-run-mysql-upgrade-to-create-it">https://stackoverflow.com/questions/41531225/cant-open-the-mysql-plugin-table-please-run-mysql-upgrade-to-create-it</a><div id="articleHeader"><h1>Can't open the mysql.plugin table. Please run mysql_upgrade to create it</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        3
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>2</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I have downloaded mysql ZIP from here <a href="https://dev.mysql.com/downloads/file/?id=467269" target="_blank">https://dev.mysql.com/downloads/file/?id=467269</a></p>

<p>Then extracted it, renamed <code>my-default.ini</code> to <code>my.ini</code>, set </p>

<pre><code>basedir = D:\Apps\MySQL\mysql-5.7.17-winx64
datadir = D:\Apps\MySQL\data5717</code></pre>

<p>then started </p>

<pre><code>mysqld --console</code></pre>

<p>under admin privileges. All was described here: <a href="http://dev.mysql.com/doc/refman/5.7/en/windows-install-archive.html" target="_blank">http://dev.mysql.com/doc/refman/5.7/en/windows-install-archive.html</a></p>

<p>Unfortunately it prints the following in console:</p>

<blockquote>
  <p>[ERROR] Can't open the mysql.plugin table. Please run mysql_upgrade to
  create it.</p>
</blockquote>

<p>and doesn't work.</p>
    </div>
    
    <table>
    <tbody><tr>
    <td>
        
    </td>
    <td>
        <div>
    <div>
        asked Jan 8 '17 at 9:25
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-41531225">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-41532987">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        10
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>


<p>You probably misunderstood/skipped point 4 in your list, <em>Initialize MySQL</em>. It means to either copy an existing data directory there or to create a new one, see <a href="https://dev.mysql.com/doc/refman/5.7/en/data-directory-initialization-mysqld.html" target="_blank">Initializing the Data Directory Manually Using mysqld</a> .</p>

<p>To initialize a fresh data directory, you basically (after setting your config file) just have to run either</p>

<pre><code>bin\mysqld --initialize</code></pre>



<pre><code>bin\mysqld --initialize-insecure</code></pre>

<p>The latter will set an empty root password.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jan 8 '17 at 13:02
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
	    <div id="comments-41532987">
		        <table>
                    <tbody>



    <tr id="comment-80852835">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
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
                mysqld --initialize-insecure fixed my problem with Wamp64
                    – <a href="/users/94335/zzapper" title="1,814 reputation" target="_blank">zzapper</a>
                <a href="#comment80852835_41532987" target="_blank">Oct 26 '17 at 11:19</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-41532987">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-45725394">
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
<p>If you set datadir to some other location than basedir, like we do, then you have to COPY, not move, the basedir databases there too.
Apparently mysqld looks for some of it's own stuff in the wrong place. 
After the copy you have to change the owner and group of everything you copied to mysql.</p>

<p>sudo cp -R /usr/local/mysql/data/* /your/own/data/place
sudo chown -R mysql:mysql /your/own/data/place</p>

<p>BTW you can't just change the basedir to match the new datadir after the copy.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-45725394">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/mysql" title="show questions tagged 'mysql'" target="_blank">mysql</a> <a href="/questions/tagged/windows" title="show questions tagged 'windows'" target="_blank">windows</a> <a href="/questions/tagged/installation" title="show questions tagged 'installation'" target="_blank">installation</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
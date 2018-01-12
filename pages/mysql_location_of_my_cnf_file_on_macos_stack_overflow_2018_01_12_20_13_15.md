<a href="https://stackoverflow.com/questions/10757169/location-of-my-cnf-file-on-macos/10757312">https://stackoverflow.com/questions/10757169/location-of-my-cnf-file-on-macos/10757312</a><div id="articleHeader"><h1>Location of my.cnf file on macOS</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        102
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>41</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I'm trying to follow along <a href="http://www.cyberciti.biz/tips/how-do-i-enable-remote-access-to-mysql-database-server.html" target="_blank">this tutorial</a> to enable remote access to MySQL. The problem is, where should <code>my.cnf</code> file be located? I'm using Mac OS X Lion.</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-10757169">
		        <table>
                    <tbody>



    <tr id="comment-13981099">
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
                I think this belongs to serverfault.com. But still, welcome to SO!
                    – <a href="/users/615776/artefact2" title="5,175 reputation" target="_blank">Artefact2</a>
                <a href="#comment13981099_10757169" target="_blank">May 25 '12 at 15:28</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-10757169">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-10757261">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        179
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p><a href="http://forums.mysql.com/read.php?11,366143,376017#msg-376017" target="_blank">This thread on the MySQL forum</a> says:</p>

<blockquote>
  <p><em>By default, the OS X installation does not use a my.cnf, and MySQL just uses the default values. To set up your own my.cnf, you could just create a file straight in /etc.</em> </p>
</blockquote>

<p>OS X provides example configuration files at <code>/usr/local/mysql/support-files/</code>.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-10757261">
		        <table>
                    <tbody>



    <tr id="comment-13981275">
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
                Thanks!! So just in /usr/etc? Or should I make some kind of mysql directory there? :) <i>edit</i> Found the answer to that on the link, thanks!
                    – <a href="/users/1162474/nicolas" title="673 reputation" target="_blank">nicolas</a>
                <a href="#comment13981275_10757261" target="_blank">May 25 '12 at 15:35</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-36487210">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                14
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
                At least the current MySQL package for Mac OS X (mysql-5.6.17-osx10.7-x86_64 at the time of this writing) <i>does</i> in fact create and use a my.cnf. It is located at /usr/local/mysql-5.6.17-osx10.7-x86_64/my.cnf
                    – <a href="/users/430742/jpsy" title="8,525 reputation" target="_blank">Jpsy</a>
                <a href="#comment36487210_10757261" target="_blank">May 19 '14 at 11:07</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-58805600">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                32
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
                you may want to ensure that mysql is actually loading in whichever <code>my.cnf</code> file you're editing via <code>mysql --verbose --help | grep my.cnf</code>
                    – <a href="/users/1700270/ryan-tuck" title="1,446 reputation" target="_blank">Ryan Tuck</a>
                <a href="#comment58805600_10757261" target="_blank">Feb 22 '16 at 16:25</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-73061957">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
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
                On Mac OS Sierra, it wasn't set up already. I had to copy /usr/local/mysql/support-files/my-default.cnf to my.cnf in the same dir. Note that the mysql is symlinked to the package, in my case mysql-5.7.17-macos10.12-x86_64.
                    – <a href="/users/6941075/christia" title="110 reputation" target="_blank">Christia</a>
                <a href="#comment73061957_10757261" target="_blank">Mar 23 '17 at 19:20</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-79285202">
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
                Just did a clean install of MySQL 5.7.19 on Mac OS 10.12 using the .dmg from dev.mysql.com. There's no my.cnf in any of the places that mysql --help says it looks in. And there's no my-default.cnf in /usr/local/mysql/support-files/ or anywhere else I've found. Turns out that <a href="https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html" target="_blank">"as of MySQL 5.7.18, my-default.cnf is no longer included in or installed by distribution packages"</a>.
                    – <a href="/users/703200/chris-bartley" title="371 reputation" target="_blank">Chris Bartley</a>
                <a href="#comment79285202_10757261" target="_blank">Sep 11 '17 at 17:49</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-10757261">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>3</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-37729535">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        25
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>In general, on Unix and Unix-like systems, MySQL/MariaDB programs read config/startup files in the following locations (in the specified order):</p>

<ul>
<li><code>/etc/my.cnf</code> -   Global</li>
<li><code>/etc/mysql/my.cnf</code> - Global</li>
<li><p><code>SYSCONFDIR/my.cnf</code> - Global</p>

<blockquote>
  <p><code>SYSCONFDIR</code> represents the directory specified with the <code>SYSCONFDIR</code> option to <code>CMake</code> when MySQL was built. By default, this is the etc directory located under the compiled-in installation directory.</p>
</blockquote></li>
<li><p><code>$MYSQL_HOME/my.cnf</code> -    Server-specific (server only)</p>

<blockquote>
  <p><code>MYSQL_HOME</code> is an environment variable containing the path to the directory in which the server-specific <code>my.cnf</code> file resides. If <code>MYSQL_HOME</code> is not set and you start the server using the <code>mysqld_safe</code> program, <code>mysqld_safe</code> sets it to <code>BASEDIR</code>, the MySQL base installation directory.</p>
</blockquote></li>
<li><p>file specified with <code>--defaults-extra-file=path</code> if any</p></li>
<li><code>~/.my.cnf</code> - User-specific</li>
<li><code>~/.mylogin.cnf</code> - User-specific (clients only)</li>
</ul>

<p><sup>Source: <a href="https://dev.mysql.com/doc/refman/5.7/en/option-files.html" target="_blank">Using Option Files</a>.</sup></p>

<blockquote>
  <p>Note: On Unix platforms, MySQL ignores configuration files that are world-writable. This is intentional as a security measure.</p>
</blockquote>

<hr />

<p>Additionally on Mac there is a simple way to check it.</p>

<ol>
<li><p>Run: <code>sudo fs_usage | grep my.cnf</code></p>

<p><sup>This will report any filesystem activity in real-time related to that file.</sup></p></li>
<li><p>In another Terminal, restart your MySQL/MariaDB, e.g.</p>

<pre><code>brew services restart mysql</code></pre>



<pre><code>brew services restart mariadb</code></pre></li>
<li><p>On terminal with <code>fs_usage</code>, the proper location should be shown, e.g.</p>

<pre><code>15:52:22  access            /usr/local/Cellar/mariadb/10.1.14/my.cnf                                         0.000002   sh          </code></pre>

<p>So if the file doesn't exist, create one.</p></li>
</ol>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-37729535">
		        <table>
                    <tbody>



    <tr id="comment-83195419">
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
                Thanks! the  <code>sudo fs_usage | grep my.cnf</code> method is quite efficient. I find this file on folder: <b>/usr/local/etc/my.cnf</b>
                    – <a href="/users/3831478/gary" title="658 reputation" target="_blank">gary</a>
                <a href="#comment83195419_37729535" target="_blank">Jan 5 at 8:52</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-37729535">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-45070637">
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
<p>For me in sierra version</p>

<p>copy the default configuration at:</p>

<blockquote>
  <p>/usr/local/Cellar/mysql/5.6.27/support-files/my-default.cnf</p>
</blockquote>



<blockquote>
  <p>/usr/local/Cellar/mysql/5.6.27/my.cnf</p>
</blockquote>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 13 '17 at 2:50
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
	    

        <div id="comments-link-45070637">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-44453530">
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
<p>Copy /usr/local/opt/mysql/support-files/my-default.cnf as /etc/my.cnf or /etc/mysql/my.cnf and then restart mysql.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-44453530">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-43630651">
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
<p>I checked in macOS Sierra, the homebrew installed <code>MySql 5.7.12</code></p>

<p>The support files are located at </p>

<pre><code>/usr/local/opt/mysql/support-files</code></pre>

<p>Just copy <code>my-default.cnf</code> as <code>/etc/my.cnf</code> or <code>/etc/mysql/my.cnf</code> and the configuration will be picked up on restart.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 26 '17 at 9:47
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
	    <div id="comments-43630651">
		        <table>
                    <tbody>



    <tr id="comment-74429234">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
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
                I just installed 5.7.18 on 12.12.4 via homebrew and they are not there.
                    – <a href="/users/1831325/norman-h" title="586 reputation" target="_blank">norman_h</a>
                <a href="#comment74429234_43630651" target="_blank">Apr 29 '17 at 3:48</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-43630651">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-24250739">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        59
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>In case of Mac OS X Maverick when MySQL is installed via Homebrew it's located at <code>/usr/local/opt/mysql/my.cnf</code></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-24250739">
		        <table>
                    <tbody>



    <tr id="comment-38894993">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
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
                which is /usr/local/Cellar/yourMySqlVersion/my.cnf
                    – <a href="/users/890537/m02ph3u5" title="1,773 reputation" target="_blank">m02ph3u5</a>
                <a href="#comment38894993_24250739" target="_blank">Jul 29 '14 at 10:24</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-44899271">
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
                /usr/local/opt/mariadb/VERSIONNUMBER/ in my case MariaDB is installed
                    – <a href="/users/589132/steven-lizarazo" title="2,498 reputation" target="_blank">Steven Lizarazo</a>
                <a href="#comment44899271_24250739" target="_blank">Feb 2 '15 at 6:11</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-51603243">
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
            
        </td>
    </tr>
    <tr id="comment-55648942">
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
                Mine is in /usr/local/etc/my.cnf
                    – <a href="/users/825364/steve-tauber" title="4,485 reputation" target="_blank">Steve Tauber</a>
                <a href="#comment55648942_24250739" target="_blank">Nov 26 '15 at 18:22</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-24250739">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-40114962">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>For MAMP 3.5 Mac El Capitan, create a separate empty config file and write your additional settings for mysql</p>

<pre><code>sudo vim /Applications/MAMP/Library/my.cnf</code></pre>

<p>And Add like this </p>

<pre><code>[mysqld]
max_allowed_packet = 256M</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Oct 18 '16 at 17:55
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
	    

        <div id="comments-link-40114962">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-38563093">
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
<p>you can check the file /usr/local/bin/mysql.server and see from where my.conf is being read. usually it is from /etc/my.cnf or ~/my.cnf</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 25 '16 at 8:38
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
	    

        <div id="comments-link-38563093">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-37456359">
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
<p>For Mac , what worked for me is creating a .my.cnf file in my ~ path. Hope this helps.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered May 26 '16 at 9:08
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
	    

        <div id="comments-link-37456359">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-10757312">
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
<p>I don't know which version of MySQL you're using, but here are possible locations of the my.cnf file for version 5.5 (taken from <a href="http://dev.mysql.com/doc/refman/5.5/en/option-files.html" target="_blank">here</a>) on Mac OS X:</p>

<ol>
<li><code>/etc/my.cnf</code></li>
<li><code>/etc/mysql/my.cnf</code></li>
<li><code>SYSCONFDIR/my.cnf</code></li>
<li><code>$MYSQL_HOME/my.cnf</code></li>
<li><code>defaults-extra-file</code> (the file specified with <code>--defaults-extra-file=path</code>, if any)</li>
<li><code>~/.my.cnf</code></li>
</ol>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-10757312">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-34547799">
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
<p>For MySQL 5.7 on Mac OS X El Capitan: <code>/usr/local/mysql/etc/my.cnf</code></p>

<p>Copy default conf from <code>/usr/local/mysql/support-files/my-default.cnf</code></p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 31 '15 at 14:30
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
	    <div id="comments-34547799">
		        <table>
                    <tbody>



    <tr id="comment-62282251">
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
                Just to be clear, you have to create "etc/" folder yourself and you need root privileges for that "sudo su -"
                    – <a href="/users/1838098/trojan" title="787 reputation" target="_blank">trojan</a>
                <a href="#comment62282251_34547799" target="_blank">May 23 '16 at 8:35</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-65940069">
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
                Thank you @trojan
		            – user3717115
                <a href="#comment65940069_34547799" target="_blank">Sep 3 '16 at 4:01</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-67500389">
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
                Not found in that location for me . I am using MAMP
                    – <a href="/users/2273007/mirza-vu" title="590 reputation" target="_blank">mirza vu</a>
                <a href="#comment67500389_34547799" target="_blank">Oct 18 '16 at 17:29</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-67531579">
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
            
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-34547799">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-32278167">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>So none of these things worked for me.  I am using the current dmg install of mysql community server.  ps shows that all of the most critical parameters normally in my.cnf are passed on the command line, and I couldn't figure out where that was coming from.  After doing a full text search of my box I found it in:</p>

<p>/Library/LaunchDaemons/com.oracle.oss.mysql.mysqld.plist  </p>

<p>So you can either change them there, or take them out so it will actually respect the ones you have in your my.cnf wherever you decided to put it.</p>

<p>Enjoy!</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-32278167">
		        <table>
                    <tbody>



    <tr id="comment-82150624">
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
                great! you saved my day.
                    – <a href="/users/6717058/jenny" title="95 reputation" target="_blank">jenny</a>
                <a href="#comment82150624_32278167" target="_blank">Dec 1 '17 at 15:23</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-32278167">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-30011425">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        9
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>In mysql 5.6.22, which I installed it from Homebrew, the path of my.cnf is </p>

<pre><code>/usr/local/opt/mysql/my.cnf </code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-30011425">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-23755479">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        11
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>The <a href="http://dev.mysql.com/downloads/mysql/" target="_blank">current MySQL package for Mac OS X Mavericks</a> (mysql-5.6.17-osx10.7-x86_64 at the time of this writing) automatically creates a my.cnf during installation. </p>

<p>It is located at <code>/usr/local/mysql-5.6.17-osx10.7-x86_64/my.cnf</code><br />
Adapt your path according to your version.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-23755479">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-10757247">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>You can open a terminal and type <code>locate my.cnf</code></p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered May 25 '12 at 15:31
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
	    <div id="comments-10757247">
		        <table>
                    <tbody>



    <tr id="comment-13981237">
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
                Sorry to not be specific enough, I apparently need to copy 'my-large.cnf' to some folder and rename it 'my.cnf'. But I don't know to where..
                    – <a href="/users/1162474/nicolas" title="673 reputation" target="_blank">nicolas</a>
                <a href="#comment13981237_10757247" target="_blank">May 25 '12 at 15:33</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-41521233">
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
                also, you do need to have a populated locate db. on mac osx: sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist
                    – <a href="/users/1882064/arcseldon" title="15,138 reputation" target="_blank">arcseldon</a>
                <a href="#comment41521233_10757247" target="_blank">Oct 18 '14 at 10:16</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-10757247">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/mysql" title="show questions tagged 'mysql'" target="_blank">mysql</a> <a href="/questions/tagged/database" title="show questions tagged 'database'" target="_blank">database</a> <a href="/questions/tagged/macos" title="show questions tagged 'macos'" target="_blank">macos</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
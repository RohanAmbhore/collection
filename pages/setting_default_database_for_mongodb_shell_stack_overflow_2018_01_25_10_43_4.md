<a href="https://stackoverflow.com/questions/11336346/setting-default-database-for-mongodb-shell">https://stackoverflow.com/questions/11336346/setting-default-database-for-mongodb-shell</a><div id="articleHeader"><h1>Setting default database for MongoDB shell</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        29
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>6</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>When I go into the mongo shell in my terminal, it always starts with the database test, which is the wrong database. Can you set mongo to start in a specific database?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-11336346">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-11336375">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        36
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<h3>Command Line</h3>

<p>You can select the database to use on the <a href="http://www.mongodb.org/display/DOCS/Overview+-+The+MongoDB+Interactive+Shell#Overview-TheMongoDBInteractiveShell-RunningtheShell" target="_blank">mongo command line</a>, eg for 'mydb':</p>

<pre><code>mongo mydb</code></pre>

<p>If a database name is not provided, 'test' will be used.</p>

<h3>In .mongorc.js</h3>

<p>If you want to set a default database without specifying on the command line each time, you can add a line to the <a href="http://docs.mongodb.org/manual/reference/program/mongo/#mongo-mongorc-file" target="_blank"><code>.mongorc.js</code></a> file in your home directory:</p>

<pre><code>db = db.getSiblingDB("mydb")</code></pre>

<p>The <code>.mongorc.js</code> file is executed after the <code>mongo</code> shell is started, so if you set a default here it will override a database specified on the command line.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-11336375">
		        <table>
                    <tbody>



    <tr id="comment-14926626">
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
                I meant like setting a default database to use, so I wouldn't have to start up in test each time. I've set an alias in my .bash_profil now though.
                    – <a href="/users/1005396/holger-edward-wardlow-sindb%c3%a6k" title="303 reputation" target="_blank">Holger Edward Wardlow Sindbæk</a>
                <a href="#comment14926626_11336375" target="_blank">Jul 4 '12 at 23:55</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-31392453">
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
                I didn't realize the impact of .mongorc.js. Be careful when using .mongorc.js because when you connect to other database, like your production ones, it will still run the same commands.
                    – <a href="/users/1236394/kirk" title="450 reputation" target="_blank">Kirk</a>
                <a href="#comment31392453_11336375" target="_blank">Jan 3 '14 at 19:42</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-31393202">
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
                @kirk: FYI, you can run <code>mongo --norc</code> if you don't want <code>.mongorc.js</code> to be run when the shell starts.
                    – <a href="/users/1388319/stennie" title="40,266 reputation" target="_blank">Stennie</a>
                <a href="#comment31393202_11336375" target="_blank">Jan 3 '14 at 20:07</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-41272587">
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
                -1, if you don't have permissions to access database <code>test</code> then you are kicked out on authentication before <code>.mongorc.js</code> kicks in.
                    – <a href="/users/520567/akostadinov" title="10,007 reputation" target="_blank">akostadinov</a>
                <a href="#comment41272587_11336375" target="_blank">Oct 10 '14 at 14:42</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-11336375">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-26302518">
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
<p>At the moment (looking 2.6.4) there is no way to universally set the default DB for the client. It seems hardcoded to <code>test</code>. In my anger I downvoted the Stennie's answer [1] because it doesn't work if your user does not have permissions to access the test database. But if your case is not such, then it may work good enough.</p>

<p>[1] and I can't reverse my vote now unless answer is edited</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Oct 10 '14 at 15:07
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
	    

        <div id="comments-link-26302518">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-26744074">
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
<p>It's entirely possible to set a default, albiet in a slightly strange way. Here's what I do for using automatic authentication to an admin in .mongorc.js:</p>

<pre><code>//Persist the database selected
var selectedDB = db
//Authenticate
db = db.getSiblingDB("admin")
db.auth('admin','adminpass')
//Switch back to selected DB
db = selectedDB
//Universally allow read queries on secondaries from shell. 
rs.slaveOk()</code></pre>

<p>To directly answer the question, I'd think the way to accomplish this is simply by executing a check to see if the current database loaded up is "test" and alter only if that's the case, so.</p>

<p><code>
if(db.name == 'test')
db.getSiblingDB('yourdefaultdb')
</code></p>

<p>This allows both selecting a database at the command line and setting a default. Naturally it'll prevent you from overriding and using the "test" db from the command line, but I think that's a bit of a strange use case given the question. Cheers. </p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Nov 4 '14 at 20:08
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
	    

        <div id="comments-link-26744074">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/shell" title="show questions tagged 'shell'" target="_blank">shell</a> <a href="/questions/tagged/mongodb" title="show questions tagged 'mongodb'" target="_blank">mongodb</a> <a href="/questions/tagged/terminal" title="show questions tagged 'terminal'" target="_blank">terminal</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
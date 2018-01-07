<a href="https://stackoverflow.com/questions/9038547/mongodb-update-every-document-on-one-field">https://stackoverflow.com/questions/9038547/mongodb-update-every-document-on-one-field</a><div id="articleHeader"><h1>MongoDB: update every document on one field</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        118
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>28</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I have a collected named <code>foo</code> hypothetically.</p>

<p>Each instance of <code>foo</code> has a field called lastLookedAt which is a UNIX timestamp since epoch. I'd like to be able to go through the MongoDB client and set that timestamp for all existing documents (about 20,000 of them) to the current timestamp.</p>

<p>What's the best way of handling this?</p>
    </div>
    <div>
        <a href="/questions/tagged/mongodb" title="show questions tagged 'mongodb'" target="_blank">mongodb</a> 
    </div>
    <table>
    <tbody><tr>
    <td>
        
    </td>
    <td>
        <div>
    <div>
        asked Jan 27 '12 at 18:55
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
	    

        <div id="comments-link-9038547">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-9038593">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        256
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>In the Mongo shell, or with any Mongodb client:</p>

<p><strong>• For Mongodb &gt;= 3.2:</strong></p>

<p><code>db.foo.updateMany({}, {$set: {lastLookedAt: Date.now() / 1000}})</code></p>

<p>See <a href="http://docs.mongodb.org/manual/tutorial/modify-documents/#update-multiple-documents" target="_blank">http://docs.mongodb.org/manual/tutorial/modify-documents/#update-multiple-documents</a></p>

<ul>
<li><code>{}</code> is the condition (the empty condition matches any document)</li>
<li><code>{$set: {lastLookedAt: Date.now() / 1000}}</code> is what you want to do</li>
</ul>

<p><strong>• For Mongodb &gt;= 2.2:</strong></p>

<p><code>db.foo.update({}, {$set: {lastLookedAt: Date.now() / 1000}}, { multi: true })</code></p>

<p>See <a href="http://docs.mongodb.org/manual/tutorial/modify-documents/#update-multiple-documents" target="_blank">http://docs.mongodb.org/manual/tutorial/modify-documents/#update-multiple-documents</a></p>

<ul>
<li><code>{}</code> is the condition (the empty condition matches any document)</li>
<li><code>{$set: {lastLookedAt: Date.now() / 1000}}</code> is what you want to do</li>
<li><code>{multi: true}</code> is the "update multiple documents" option</li>
</ul>

<p><strong>• For Mongodb &lt; 2.2:</strong> </p>

<p><code>db.foo.update({}, {$set: {lastLookedAt: Date.now() / 1000}}, false, true)</code></p>

<p>See <a href="https://web.archive.org/web/20120613233453/http://www.mongodb.org/display/DOCS/Updating" target="_blank">https://web.archive.org/web/20120613233453/http://www.mongodb.org/display/DOCS/Updating</a></p>

<ul>
<li><code>{}</code> is the condition (the empty condition matches any document)</li>
<li><code>{$set: {lastLookedAt: Date.now() / 1000}}</code> is what you want to do</li>
<li><code>false</code> is for the "upsert" parameter (insert if not present, or else update - not what you want)</li>
<li><code>true</code> is for the "multi" parameter (update multiple records)</li>
</ul>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-9038593">
		        <table>
                    <tbody>



    <tr id="comment-11337983">
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
                should it not be Date.now().getTime() for unix timestamp?
                    – <a href="/users/175836/randombits" title="8,734 reputation" target="_blank">randombits</a>
                <a href="#comment11337983_9038593" target="_blank">Jan 27 '12 at 19:05</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-11338064">
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
    <tr id="comment-11338186">
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
                It's still giving me a date that's no where near right for all of these instances of foo. After running that I do a db.foo.findOne() and lastLookedAt is: 1327691719186, which translates to jruby-1.6.5 :011 &gt; Time.at(1327691719186)  =&gt; Sun Nov 16 02:19:46 -0500 44042
                    – <a href="/users/175836/randombits" title="8,734 reputation" target="_blank">randombits</a>
                <a href="#comment11338186_9038593" target="_blank">Jan 27 '12 at 19:16</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-11338258">
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
                My bad, POSIX time uses seconds, whereas Javascript time uses milliseconds. Date.now() / 1000 should work, though. You may have to round it.
                    – <a href="/users/834833/philippe-plantier" title="4,568 reputation" target="_blank">Philippe Plantier</a>
                <a href="#comment11338258_9038593" target="_blank">Jan 27 '12 at 19:20</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-60795849">
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
                psh it's that empty {} that did it for me, thanks Phil
                    – <a href="/users/3147774/jona" title="335 reputation" target="_blank">Jona</a>
                <a href="#comment60795849_9038593" target="_blank">Apr 13 '16 at 13:10</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-9038593">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>2</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-36200280">
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
<p>This code will be helpful for you</p>

<pre><code>        Model.update({
            'type': "newuser"
        }, {
            $set: {
                email: "abc@gmail.com",
                phoneNumber:"0123456789"
            }
        }, {
            multi: true
        },
        function(err, result) {
            console.log(result);
            console.log(err);
        })  </code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Mar 24 '16 at 12:31
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
	    

        <div id="comments-link-36200280">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-9038688">
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
<p>I have been using MongoDB .NET driver for a little over a month now. If I were to do it using .NET driver, I would use Update method on the collection object. First, I will construct a query that will get me all the documents I am interested in and do an Update on the fields I want to change. Update in Mongo only affects the first document and to update all documents resulting from the query one needs to use 'Multi' update flag. Sample code follows...</p>

<pre><code>var collection = db.GetCollection("Foo");
var query = Query.GTE("No", 1); // need to construct in such a way that it will give all 20K //docs.
var update = Update.Set("timestamp", datetime.UtcNow);
collection.Update(query, update, UpdateFlags.Multi);</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jan 27 '12 at 19:08
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
	    

        <div id="comments-link-9038688">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/mongodb" title="show questions tagged 'mongodb'" target="_blank">mongodb</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
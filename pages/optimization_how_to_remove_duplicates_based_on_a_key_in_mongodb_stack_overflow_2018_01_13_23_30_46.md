<a href="https://stackoverflow.com/questions/13190370/how-to-remove-duplicates-based-on-a-key-in-mongodb">https://stackoverflow.com/questions/13190370/how-to-remove-duplicates-based-on-a-key-in-mongodb</a><div id="articleHeader"><h1>How to remove duplicates based on a key in Mongodb?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        31
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>19</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I have a collection in MongoDB where there are around (~3 million records). My sample record would look like,</p>

<pre><code> { "_id" = ObjectId("50731xxxxxxxxxxxxxxxxxxxx"),
   "source_references" : [
                           "_id" : ObjectId("5045xxxxxxxxxxxxxx"),
                           "name" : "xxx",
                           "key" : 123
                          ]
 }</code></pre>

<p>I am having a lot of duplicate records in the collection having same <code>source_references.key</code>. (By Duplicate I mean, <code>source_references.key</code> not the <code>_id</code>).</p>

<p>I want to remove duplicate records based on <code>source_references.key</code>, I'm thinking of writing some PHP code to traverse each record and remove the record if exists.</p>

<p>Is there a way to remove the duplicates in Mongo Internal command line?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-13190370">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-13190994">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        64
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>If you are certain that the <code>source_references.key</code> identifies duplicate records, you can ensure a unique index with the <a href="http://docs.mongodb.org/manual/tutorial/create-a-unique-index/#drop-duplicates" target="_blank"><code>dropDups:true</code></a> index creation option in MongoDB 2.6 or older:</p>

<pre><code>db.things.ensureIndex({'source_references.key' : 1}, {unique : true, dropDups : true})</code></pre>

<p>This will keep the first unique document for each <code>source_references.key</code> value, and drop any subsequent documents that would otherwise cause a duplicate key violation.</p>

<p><strong>Important Notes</strong>:</p>

<ul>
<li>The <code>dropDups</code> option was <a href="http://docs.mongodb.org/manual/release-notes/3.0-compatibility/#remove-dropdups-option" target="_blank">removed in MongoDB 3.0</a>, so a different approach will be required. For example, you could use aggregation as suggested on: <a href="https://stackoverflow.com/questions/29072209/mongo-db-duplicate-documents-even-after-adding-unique-key" target="_blank">MongoDB duplicate documents even after adding unique key</a>. </li>
<li>Any documents missing the <code>source_references.key</code> field will be considered as having a <em>null</em> value, so subsequent documents missing the key field will be deleted.  You can add the <a href="http://docs.mongodb.org/manual/tutorial/create-a-sparse-index/" target="_blank"><code>sparse:true</code></a> index creation option so the index only applies to documents with a <code>source_references.key</code> field.</li>
</ul>

<p><strong>Obvious caution</strong>: Take a backup of your database, and try this in a staging environment first if you are concerned about unintended data loss.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-13190994">
		        <table>
                    <tbody>



    <tr id="comment-18345348">
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
                Hands on explanations like this should be mandatory in all docs
                    – <a href="/users/538837/erik" title="2,027 reputation" target="_blank">Erik</a>
                <a href="#comment18345348_13190994" target="_blank">Nov 16 '12 at 19:46</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-33121396">
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
                Can we delete only the newest duplicates ?  I prefeer to keep the old ones , How can I do this ?
                    – <a href="/users/3062150/sekai" title="1,964 reputation" target="_blank">Sekai</a>
                <a href="#comment33121396_13190994" target="_blank">Feb 19 '14 at 9:08</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-33132071">
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
                @Sekai: If you want to delete the newest duplicates (or have more control) you'll have to write a bit of custom script/code to find duplicates and work out which document(s) you want to delete.
                    – <a href="/users/1388319/stennie" title="40,046 reputation" target="_blank">Stennie</a>
                <a href="#comment33132071_13190994" target="_blank">Feb 19 '14 at 13:24</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-40105094">
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
                @NicCottrell: the <code>dropDups</code> option only applies when the unique index is created. Future inserts with duplicate keys will generate a duplicate key error.
                    – <a href="/users/1388319/stennie" title="40,046 reputation" target="_blank">Stennie</a>
                <a href="#comment40105094_13190994" target="_blank">Sep 4 '14 at 11:26</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-67771682">
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
                @wordsforthewise Obvious reasons to deprecate <code>dropDups</code>: it was not clear which duplicate would be removed and more importantly deleting documents is an unexpected side effect of creating an index. Worst case scenario: if you create a unique index with <code>dropDups:true</code> on a field that doesn't exist (eg. due to a typo) the indexed value will be <code>null</code> and you'll be left with exactly one document in the collection.
                    – <a href="/users/1388319/stennie" title="40,046 reputation" target="_blank">Stennie</a>
                <a href="#comment67771682_13190994" target="_blank">Oct 26 '16 at 6:20</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-13190994">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>5</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-13191077">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>While @Stennie's is a valid answer, it is not the only way. Infact the MongoDB manual asks you to be very cautious while doing that. There are two other options</p>

<ol>
<li>Let the MongoDB do that for you <a href="https://stackoverflow.com/questions/5530580/removing-duplicate-records-using-mapreduce" target="_blank">using Map Reduce</a>

<ul>
<li><a href="http://glassonionblog.wordpress.com/2012/03/19/mongodb-how-to-check-for-duplicates-in-a-collection/" target="_blank">Another way</a></li>
</ul></li>
<li>You do <a href="https://stackoverflow.com/questions/8405331/how-to-remove-duplicate-record-in-mongodb-by-mapreduce" target="_blank">programatically</a> which is less efficient.</li>
</ol>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-13191077">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-33364816">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        21
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Remove duplicates by <a href="https://docs.mongodb.org/manual/aggregation/" target="_blank">aggregation framework</a>.</p>

<p>a. If you want to delete in one go.</p>

<pre><code>var duplicates = [];

db.collectionName.aggregate([
  // discard selection criteria, You can remove "$match" section if you want
  { $match: { 
    source_references.key: { "$ne": '' }  
  }},
  { $group: { 
    _id: { source_references.key: "$source_references.key"}, // can be grouped on multiple properties 
    dups: { "$addToSet": "$_id" }, 
    count: { "$sum": 1 } 
  }}, 
  { $match: { 
    count: { "$gt": 1 }    // Duplicates considered as count greater than one
  }}
])               // You can display result until this and check duplicates 
.forEach(function(doc) {
    doc.dups.shift();      // First element skipped for deleting
    doc.dups.forEach( function(dupId){ 
        duplicates.push(dupId);   // Getting all duplicate ids
        }
    )    
})

// If you want to Check all "_id" which you are deleting else print statement not needed
printjson(duplicates);     

// Remove all duplicates in one go    
db.collectionName.remove({_id:{$in:duplicates}})</code></pre>

<p>b. You can delete documents one by one.</p>

<pre><code>db.collectionName.aggregate([
  // discard selection criteria, You can remove "$match" section if you want
  { $match: { 
    source_references.key: { "$ne": '' }  
  }},
  { $group: { 
    _id: { source_references.key: "$source_references.key"}, // can be grouped on multiple properties 
    dups: { "$addToSet": "$_id" }, 
    count: { "$sum": 1 } 
  }}, 
  { $match: { 
    count: { "$gt": 1 }    // Duplicates considered as count greater than one
  }}
])               // You can display result until this and check duplicates 
.forEach(function(doc) {
    doc.dups.shift();      // First element skipped for deleting
    db.collectionName.remove({_id : {$in: doc.dups }});  // Delete remaining duplicates
})</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-33364816">
		        <table>
                    <tbody>



    <tr id="comment-66210606">
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
                can you explain this line  <code>// If your result getting response in "result" then use else don't use ".result" in query </code> I am getting a syntax error  <code>SyntaxError: Unexpected token .</code>
                    – <a href="/users/1934182/vaulstein" title="3,200 reputation" target="_blank">Vaulstein</a>
                <a href="#comment66210606_33364816" target="_blank">Sep 12 '16 at 6:20</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-66211183">
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
                In Mongodb old version or Robomongo, I was getting output in result object. I hope you are using new version and you won't need it. Updated answer.
                    – <a href="/users/1045444/somnath-muluk" title="27,463 reputation" target="_blank">Somnath Muluk</a>
                <a href="#comment66211183_33364816" target="_blank">Sep 12 '16 at 6:44</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-67771519">
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
                Yeah, that's a lot simpler than <code>db.things.ensureIndex({'source_references.key' : 1}, {unique : true, dropDups : true})</code>, I totally understand why they deprecated ensureIndex.....................         (◟ ;益;◞)
                    – <a href="/users/4549682/wordsforthewise" title="1,944 reputation" target="_blank">wordsforthewise</a>
                <a href="#comment67771519_33364816" target="_blank">Oct 26 '16 at 6:14</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-72967573">
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
                NOTE: <i>$addToSet does not guarantee a particular ordering of elements in the modified set</i> as per <a href="https://docs.mongodb.com/manual/reference/operator/update/addToSet/" target="_blank">docs.mongodb.com/manual/reference/operator/update/addToSet</a>  ...use <code>$push</code> if you'd like to preserve order  ...ALSO NOTE: <code>$addToSet</code> will not add duplicates to the array whereas <code>$push</code> will
                    – <a href="/users/4645935/benjamin-hoffman" title="603 reputation" target="_blank">Benjamin Hoffman</a>
                <a href="#comment72967573_33364816" target="_blank">Mar 21 '17 at 18:26</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-33364816">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-36099237">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        29
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>This is the easiest query I used on my MongoDB 3.2</p>

<pre><code>db.myCollection.find({}, {myCustomKey:1}).sort({_id:1}).forEach(function(doc){
    db.myCollection.remove({_id:{$gt:doc._id}, myCustomKey:doc.myCustomKey});
})</code></pre>

<p>Index your <code>customKey</code> before running this to increase speed</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Mar 19 '16 at 7:44
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
	    <div id="comments-36099237">
		        <table>
                    <tbody>



    <tr id="comment-60096101">
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
                easiest and really simple!!!
                    – <a href="/users/1115059/jaydeep" title="1,321 reputation" target="_blank">Jaydeep</a>
                <a href="#comment60096101_36099237" target="_blank">Mar 26 '16 at 7:10</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-60522635">
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
                If i have more duplicates means it will remove the all duplicates
                    – <a href="/users/5214355/sara" title="25 reputation" target="_blank">sara</a>
                <a href="#comment60522635_36099237" target="_blank">Apr 6 '16 at 15:05</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-61051721">
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
                Yes @sara. It will delete all duplicates until you specify limit in remove query
                    – <a href="/users/3666966/kanak-singhal" title="974 reputation" target="_blank">Kanak Singhal</a>
                <a href="#comment61051721_36099237" target="_blank">Apr 20 '16 at 5:10</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-65124486">
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
                Thanks, this worked for me.
                    – <a href="/users/4378740/chakeda" title="564 reputation" target="_blank">chakeda</a>
                <a href="#comment65124486_36099237" target="_blank">Aug 10 '16 at 19:12</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-74691237">
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
                How would this work if I need to search on multiple keys instead of just one?
                    – <a href="/users/172637/3zzy" title="22,911 reputation" target="_blank">3zzy</a>
                <a href="#comment74691237_36099237" target="_blank">May 7 '17 at 0:40</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-36099237">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>3</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-40387609">
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
<p>pip install mongo_remove_duplicate_indexes</p>

<ol>
<li>create a script in any language</li>
<li>iterate over your collection</li>
<li>create new collection and create new index in this collection with unique set to true ,remember this index has to be same as index u wish to remove duplicates from in ur original collection with same name
for ex-u have a collection gaming,and in this collection u have field genre which contains duplicates,which u wish to remove,so just create new collection
db.createCollection("cname")
create new index
db.cname.createIndex({'genre':1},unique:1)
now when u will insert document with similar genre only first will be accepted,other will be rejected with duplicae key error</li>
<li>now just insert the json format values u received into new collection and handle exception using exception handling
for ex pymongo.errors.DuplicateKeyError </li>
</ol>

<p>check out the package source code for the mongo_remove_duplicate_indexes for better understanding</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Nov 2 '16 at 18:50
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
	    

        <div id="comments-link-40387609">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-41104751">
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
<p>If you have enough memory, you can in scala do something like that: </p>

<pre><code>cole.find().groupBy(_.customField).filter(_._2.size&gt;1).map(_._2.tail).flatten.map(_.id)
.foreach(x=&gt;cole.remove({id $eq x})</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-41104751">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-45840274">
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
<p>Here is a slightly more 'manual' way of doing it:</p>

<p>Essentially, first, get a list of all the unique keys you are interested. </p>

<p>Then perform a search using each of those keys and delete if that search returns bigger than one. </p>

<pre><code>    db.collection.distinct("key").forEach((num)=&gt;{
      var i = 0;
      db.collection.find({key: num}).forEach((doc)=&gt;{
        if (i)   db.collection.remove({key: num}, { justOne: true })
        i++
      })
    });</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Aug 23 '17 at 12:51
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
	    

        <div id="comments-link-45840274">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/mongodb" title="show questions tagged 'mongodb'" target="_blank">mongodb</a> <a href="/questions/tagged/optimization" title="show questions tagged 'optimization'" target="_blank">optimization</a> <a href="/questions/tagged/duplicates" title="show questions tagged 'duplicates'" target="_blank">duplicates</a> <a href="/questions/tagged/key" title="show questions tagged 'key'" target="_blank">key</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
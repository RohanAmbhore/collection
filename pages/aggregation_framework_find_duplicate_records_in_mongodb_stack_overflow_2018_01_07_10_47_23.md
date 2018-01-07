<a href="https://stackoverflow.com/questions/26984799/find-duplicate-records-in-mongodb">https://stackoverflow.com/questions/26984799/find-duplicate-records-in-mongodb</a><div id="articleHeader"><h1>Find duplicate records in MongoDB</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        51
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>20</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<div>
    <p>This question already has an answer here:</p>
    <ul>
        <li>
            <a href="/questions/29072209/mongodb-duplicate-documents-even-after-adding-unique-key" target="_blank">MongoDB Duplicate Documents even after adding unique key</a>
                
                    2 answers
                
        </li>
    </ul>
    </div>
<p>How would I find duplicate fields in a mongo collection.</p>

<p>I'd like to check if any of the "name" fields are duplicates.</p>

<pre><code>{
    "name" : "ksqn291",
    "__v" : 0,
    "_id" : ObjectId("540f346c3e7fc1054ffa7086"),
    "channel" : "Sales"
}</code></pre>

<p>Many thanks!</p>
    </div>
    
    
</div>
</td>
        </tr>
                    <tr>
            <td colspan="2">
                <div>
        <h2>                    <b>marked</b> as duplicate by <a href="/users/2313887/neil-lunn" target="_blank">Neil Lunn</a><a href="/badges/tag-badges/aggregation-framework?badgeClass=Gold" target="_blank"> aggregation-framework</a>

 Jul 31 '17 at 6:57
</h2>
        <p>This question has been asked before and already has an answer. If those answers do not fully address your question, please <a href="/questions/ask" target="_blank">ask a new question</a>.</p>
    </div>
            </td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-26984799">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-26985011">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        88
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Use aggregation on <code>name</code> and get <code>name</code> with <code>count &gt; 1</code>:</p>

<pre><code>db.collection.aggregate(
    {"$group" : { "_id": "$name", "count": { "$sum": 1 } } },
    {"$match": {"_id" :{ "$ne" : null } , "count" : {"$gt": 1} } }, 
    {"$project": {"name" : "$_id", "_id" : 0} }
)</code></pre>

<p>To sort the results by most to least duplicates:</p>

<pre><code>db.collection.aggregate(
    {"$group" : { "_id": "$name", "count": { "$sum": 1 } } },
    {"$match": {"_id" :{ "$ne" : null } , "count" : {"$gt": 1} } }, 
    {"$sort": {"count" : -1} },
    {"$project": {"name" : "$_id", "_id" : 0} }     
)</code></pre>

<p>To use with another column name than "name", change "<strong>$name</strong>" to "<strong>$column_name</strong>"</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-26985011">
		        <table>
                    <tbody>



    <tr id="comment-42503604">
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
                <code>"$match": {"_id" :{ "$ne" : null } </code>- is unnecessary here, since the second part of the statement would suffice filtering the result. So only checking for the group having <code>count &gt; 1</code> will do.
                    – <a href="/users/1617024/batscream" title="12,882 reputation" target="_blank">BatScream</a>
                <a href="#comment42503604_26985011" target="_blank">Nov 18 '14 at 1:21</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-42503729">
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
                Tks @BatScream. { "$ne" : null } is there just in case 'name' is null or doesn't exist. Aggregation will count null as well.
                    – <a href="/users/3015960/anhlc" title="5,071 reputation" target="_blank">anhlc</a>
                <a href="#comment42503729_26985011" target="_blank">Nov 18 '14 at 1:30</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-42503750">
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
                Welcome. But then why check the <code>_id</code> field. It is always guaranteed to be not null after the <code>group</code> operation.
                    – <a href="/users/1617024/batscream" title="12,882 reputation" target="_blank">BatScream</a>
                <a href="#comment42503750_26985011" target="_blank">Nov 18 '14 at 1:32</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-42511266">
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
                The <code>_id</code> of a document from a <code>$group</code> stage can be null.
                    – <a href="/users/3749550/wdberkeley" title="8,461 reputation" target="_blank">wdberkeley</a>
                <a href="#comment42511266_26985011" target="_blank">Nov 18 '14 at 8:35</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-75467049">
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
                How would you sort the results by most to least duplicates?
                    – <a href="/users/984975/zehelvion" title="3,060 reputation" target="_blank">zehelvion</a>
                <a href="#comment75467049_26985011" target="_blank">May 28 '17 at 14:42</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-26985011">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>3</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-41122859">
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
<p>The answer anhic gave can be very inefficient if you have a large database and the attribute name is present only in some of the documents.</p>

<p>To improve efficiency you can add a $match to the aggregation.</p>

<pre><code>db.collection.aggregate(
    {"$match": {"name" :{ "$ne" : null } } }, 
    {"$group" : {"_id": "$name", "count": { "$sum": 1 } } },
    {"$match": {"count" : {"$gt": 1} } }, 
    {"$project": {"name" : "$_id", "_id" : 0} }
)</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 13 '16 at 13:53
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
	    

        <div id="comments-link-41122859">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-37405764">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<pre><code>db.collectionName.aggregate([
{ $group:{
    _id:{Name:"$name"},
    uniqueId:{$addToSet:"$_id"},
    count:{"$sum":1}
  } 
},
{ $match:{
  duplicate:{"$gt":1}
 }
}
]);</code></pre>

<p>First Group Query the group according to the fields. </p>

<p>Then we check the unique Id and count it, If count is greater then 1 then the field is duplicate in the entire collection so that thing is to be handle by $match query. </p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-37405764">
		        <table>
                    <tbody>



    <tr id="comment-64005372">
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
                couldn't get this one to work for me
                    – <a href="/users/2044993/cpres" title="376 reputation" target="_blank">cpres</a>
                <a href="#comment64005372_37405764" target="_blank">Jul 10 '16 at 16:42</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-69292595">
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
                haven't been able to make this one work for me too. Down voting!
                    – <a href="/users/650396/mathieu-g" title="148 reputation" target="_blank">Mathieu G</a>
                <a href="#comment69292595_37405764" target="_blank">Dec 8 '16 at 15:06</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-37405764">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-26984964">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        14
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>You can find the <code>list</code> of <code>duplicate</code> names using the following <code>aggregate</code> pipeline:</p>

<ul>
<li><code>Group</code> all the records having similar <code>name</code>.</li>
<li><code>Match</code> those <code>groups</code> having records greater than <code>1</code>.</li>
<li>Then <code>group</code> again to <code>project</code> all the duplicate names as an <code>array</code>.</li>
</ul>

<p>The Code:</p>

<pre><code>db.collection.aggregate([
{$group:{"_id":"$name","name":{$first:"$name"},"count":{$sum:1}}},
{$match:{"count":{$gt:1}}},
{$project:{"name":1,"_id":0}},
{$group:{"_id":null,"duplicateNames":{$push:"$name"}}},
{$project:{"_id":0,"duplicateNames":1}}
])</code></pre>



<pre><code>{ "duplicateNames" : [ "ksqn291", "ksqn29123213Test" ] }</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Nov 18 '14 at 1:13
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
	    

        <div id="comments-link-26984964">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                


                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/mongodb" title="show questions tagged 'mongodb'" target="_blank">mongodb</a> <a href="/questions/tagged/aggregation-framework" title="show questions tagged 'aggregation-framework'" target="_blank">aggregation-framework</a> <a href="/questions/tagged/database" title="show questions tagged 'database'" target="_blank">database</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
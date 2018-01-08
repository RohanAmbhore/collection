<a href="https://stackoverflow.com/questions/5373198/mongodb-relationships-embed-or-reference">https://stackoverflow.com/questions/5373198/mongodb-relationships-embed-or-reference</a><div id="articleHeader"><h1>MongoDB relationships: embed or reference?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        373
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>227</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I'm new to MongoDB--coming from a relational database background. I want to design a question structure with some comments, but I don't know which relationship to use for comments: <code>embed</code> or <code>reference</code>?</p>

<p>A question with some comments, like <a href="https://stackoverflow.com/" target="_blank">stackoverflow</a>, would have a structure like this:</p>

<pre><code>Question
    title = 'aaa'
    content = bbb'
    comments = ???</code></pre>

<p>At first, I want to use embeded comments (I think <code>embed</code> is recommended in MongoDB), like this:</p>

<pre><code>Question
    title = 'aaa'
    content = 'bbb'
    comments = [ { content = 'xxx', createdAt = 'yyy'}, 
                 { content = 'xxx', createdAt = 'yyy'}, 
                 { content = 'xxx', createdAt = 'yyy'} ]</code></pre>

<p>It clear, but I'm worried about this case: <strong>If I want to edit a specified comment, how do I get its content and its question?</strong> There is no <code>_id</code> to let me find one, nor <code>question_ref</code> to let me find its question. (I'm so newbie, that I don't know if there's any way to do this without <code>_id</code> and <code>question_ref</code>.)</p>

<p>Do I have to use <code>ref</code> not <code>embed</code>? Then I have to create a new collection for comments?</p>
    </div>
    
    
</div>
</td>
        </tr>
                    <tr>
            <td colspan="2">
                <div>
        <h2>                    <b>protected</b> by <a href="/users/1259510/johnnyhk" target="_blank">JohnnyHK</a> Feb 4 '15 at 2:18
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
	    <div id="comments-5373198">
		        <table>
                    <tbody>



    <tr id="comment-31625907">
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
                All Mongo objects are created with an _ID, whether you create the field or not. So technically each comment will still have an ID.
                    – <a href="/users/1005669/robbie-guilfoyle" title="2,025 reputation" target="_blank">Robbie Guilfoyle</a>
                <a href="#comment31625907_5373198" target="_blank">Jan 10 '14 at 5:31</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-36352085">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                15
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
    <tr id="comment-36379606">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                5
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
                I stand corrected, thanks @pennstatephil :)
                    – <a href="/users/1005669/robbie-guilfoyle" title="2,025 reputation" target="_blank">Robbie Guilfoyle</a>
                <a href="#comment36379606_5373198" target="_blank">May 15 '14 at 13:23</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-69346924">
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
                What he maybe means is that all <b>mongoose</b> objects are created with an _id for those who use this framework – see <a href="http://mongoosejs.com/docs/subdocs.html" target="_blank">mongoose subdocs</a>
                    – <a href="/users/3062017/luca-steeb" title="906 reputation" target="_blank">Luca Steeb</a>
                <a href="#comment69346924_5373198" target="_blank">Dec 9 '16 at 22:31</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-5373198">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-5373969">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        614
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>This is more an art than a science. The <a href="http://docs.mongodb.org/manual/data-modeling/" target="_blank">Mongo Documentation on Schemas</a> is a good reference, but here are some things to consider:</p>

<ul>
<li><p>Put as much in as possible</p>

<p>The joy of a Document database is that it eliminates lots of Joins.  Your first instinct should be to place as much in a single document as you can.  Because MongoDB documents have structure, and because you can efficiently query within that structure (this means that you can take the part of the document that you need, so document size shouldn't worry you much) there is no immediate need to normalize data like you would in SQL.  In particular any data that is not useful apart from its parent document should be part of the same document.</p></li>
<li><p>Separate data that can be referred to from multiple places into its own collection.</p>

<p>This is not so much a "storage space" issue as it is a "data consistency" issue.  If many records will refer to the same data it is more efficient and less error prone to update a single record and keep references to it in other places.</p></li>
<li><p>Document size considerations</p>

<p>MongoDB imposes a 4MB (16MB with 1.8) size limit on a single document.  In a world of GB of data this sounds small, but it is also 30 thousand tweets or 250 typical Stack Overflow answers or 20 flicker photos.  On the other hand, this is far more information than one might want to present at one time on a typical web page.  First consider what will make your queries easier.  In many cases concern about document sizes will be premature optimization.</p></li>
<li><p>Complex data structures:</p>

<p>MongoDB can store arbitrary deep nested data structures, but cannot search them efficiently.  If your data forms a tree, forest or graph, you effectively need to store each node and its edges in a separate document.  (Note that there are data stores specifically designed for this type of data that one should consider as well)</p>

<p>It has also <a href="http://seanhess.github.com/2012/02/01/mongodb_relational.html" target="_blank">been pointed out</a> than it is impossible to return a subset of elements in a document.  If you need to pick-and-choose a few bits of each document, it will be easier to separate them out.</p></li>
<li><p>Data Consistency</p>

<p>MongoDB makes a trade off between efficiency and consistency.  The rule is changes to a single document are <strong>always</strong> atomic, while updates to multiple documents should never be assumed to be atomic.  There is also no way to "lock" a record on the server (you can build this into the client's logic using for example a "lock" field).  When you design your schema consider how you will keep your data consistent.  Generally, the more that you keep in a document the better.</p></li>
</ul>

<p>For what you are describing, I would embed the comments, and give each comment an id field with an ObjectID.  The ObjectID has a time stamp embedded in it so you can use that instead of created at if you like.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-5373969">
		        <table>
                    <tbody>



    <tr id="comment-20564448">
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
                I'd like to add to the OP question: My comments model contains the user name and link to his avatar. What would be the best approach, considering a user can modify his name/avatar?
                    – <a href="/users/1102018/user1102018" title="2,197 reputation" target="_blank">user1102018</a>
                <a href="#comment20564448_5373969" target="_blank">Feb 5 '13 at 9:36</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-27996630">
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
                Regarding 'Complex data structures', it seems it is possible to return a subset of elements in a document using the aggregation framework (try $unwind).
                    – <a href="/users/114626/errr" title="1,104 reputation" target="_blank">errr</a>
                <a href="#comment27996630_5373969" target="_blank">Sep 23 '13 at 10:33</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-28139567">
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
                Errr, This technique was either not possibel or not widely known in MongoDB at the beginning of 2012. Given the popularity of this question, I would encourage you to write your own updated answer. I'm afraid I've stepped away from active development on MongoDB and I am not in a good position to address you comment within my original post.
                    – <a href="/users/163177/john-f-miller" title="14,955 reputation" target="_blank">John F. Miller</a>
                <a href="#comment28139567_5373969" target="_blank">Sep 27 '13 at 1:51</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-42440685">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                39
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
                16MB = 30 million tweets? ths menas about 0,5 byte per tweet?!
                    – <a href="/users/1029825/paolo" title="1,195 reputation" target="_blank">Paolo</a>
                <a href="#comment42440685_5373969" target="_blank">Nov 15 '14 at 19:13</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-79208377">
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
                Yes, it appears I was off by a factor of 1000 and some people find this important.  I will edit the post. WRT 560bytes per tweet, when I rote this in 2011 twitter was still tied to text messages and Ruby 1.4 strings; in other words still ASCII chars only.
                    – <a href="/users/163177/john-f-miller" title="14,955 reputation" target="_blank">John F. Miller</a>
                <a href="#comment79208377_5373969" target="_blank">Sep 8 '17 at 18:52</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-5373969">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>2</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-43960000">
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
<p>That's depend on the usage of the document. When you use the document, if you always using the comments, The best way to using embedding. But you should consider the maximum document size (16MB).</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered May 14 '17 at 3:08
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
	    

        <div id="comments-link-43960000">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-37595554">
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
<p>I came across this small presentation while researching this question on my own. I was surprised at how well it was laid out, both the info and the presentation of it.</p>

<p><a href="http://openmymind.net/Multiple-Collections-Versus-Embedded-Documents" target="_blank">http://openmymind.net/Multiple-Collections-Versus-Embedded-Documents</a></p>

<p>It summarized:</p>

<blockquote>
  <p>As a general rule, if you have a lot of [child documents] or if they are large, a separate collection might be best.</p>
  
  <p>Smaller and/or fewer documents tend to be a natural fit for embedding.</p>
</blockquote>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jun 2 '16 at 15:04
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
	    <div id="comments-37595554">
		        <table>
                    <tbody>



    <tr id="comment-80769607">
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
                How much is <code>a lot</code>? 3? 10? 100? What's <code>large</code>? 1kb? 1MB? 3 fields? 20 fields? What is <code>smaller</code> / <code>fewer</code>?
                    – <a href="/users/1981247/traxo" title="653 reputation" target="_blank">Traxo</a>
                <a href="#comment80769607_37595554" target="_blank">Oct 24 '17 at 13:07</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-80787432">
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
                That's a good question, and one I don't have a specific answer for. The same presentation included a slide that said "A document, including all its embedded documents and arrays, cannot exceed 16MB", so that could be your cutoff, or just go with what seems reasonable/comfortable for your specific situation. In my current project, the majority of embedded documents are for 1:1 relationships, or 1:many where the embedded documents are really simple.
                    – <a href="/users/83743/chris-bloom" title="2,269 reputation" target="_blank">Chris Bloom</a>
                <a href="#comment80787432_37595554" target="_blank">Oct 24 '17 at 21:01</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-80787565">
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
                See also the current top comment by @john-f-miller, which while also not providing specific numbers for a threshold does contain some additional pointers that should help guide your decision.
                    – <a href="/users/83743/chris-bloom" title="2,269 reputation" target="_blank">Chris Bloom</a>
                <a href="#comment80787565_37595554" target="_blank">Oct 24 '17 at 21:05</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-37595554">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-33284416">
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
<blockquote>
  <p>If I want to edit a specified comment, how do I get its content and
  its question?</p>
</blockquote>

<p>If you had kept track of the number of comments and the index of the comment you wanted to alter, you could use <a href="http://docs.mongodb.org/manual/core/document/#dot-notation" target="_blank">the dot operator</a> (<a href="https://stackoverflow.com/questions/32646613/alter-field-by-number-in-nested-array" target="_blank">SO example</a>).</p>

<p>You could do f.ex.</p>

<pre><code>db.questions.update(
    {
        "title": "aaa"       
    }, 
    { 
        "comments.0.contents": "new text"
    }
)</code></pre>

<p>(as another way to edit the comments inside the question)</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-33284416">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-27913989">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        19
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>In general, embed is good if you have one-to-one or one-to-many relationships between entities, and reference is good if you have many-to-many relationships.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jan 13 '15 at 2:19
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
	    <div id="comments-27913989">
		        <table>
                    <tbody>



    <tr id="comment-55587940">
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
                can you please add a reference link? Thanks.
                    – <a href="/users/379906/db80" title="949 reputation" target="_blank">db80</a>
                <a href="#comment55587940_27913989" target="_blank">Nov 25 '15 at 9:45</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-27913989">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-25908082">
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
<p>Yes, we can use the reference in the document.To populate the another document just like sql i joins.In mongo db they dont have joins to mapping one to many relationship document.Instead that we can use <strong>populate</strong> to fulfill our scenario..</p>

<pre><code>var mongoose = require('mongoose')
  , Schema = mongoose.Schema

var personSchema = Schema({
  _id     : Number,
  name    : String,
  age     : Number,
  stories : [{ type: Schema.Types.ObjectId, ref: 'Story' }]
});

var storySchema = Schema({
  _creator : { type: Number, ref: 'Person' },
  title    : String,
  fans     : [{ type: Number, ref: 'Person' }]
});</code></pre>

<p>Population is the process of automatically replacing the specified paths in the document with document(s) from other collection(s). We may populate a single document, multiple documents, plain object, multiple plain objects, or all objects returned from a query. Let's look at some examples.</p>

<p>Better you can get more information please visit :<a href="http://mongoosejs.com/docs/populate.html" target="_blank">http://mongoosejs.com/docs/populate.html</a>  </p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-25908082">
		        <table>
                    <tbody>



    <tr id="comment-55845664">
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
                Mongoose will issue a seperate request for each populated field. This is different to SQL JOINS as they are performed on the server. This includes extra traffic between the app server and the mongodb server. Again, you might consider this when you're optimizing. Nevertheless, your anwser is still correct.
                    – <a href="/users/1489386/max" title="493 reputation" target="_blank">Max</a>
                <a href="#comment55845664_25908082" target="_blank">Dec 2 '15 at 14:46</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-25908082">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-24992030">
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
<p>Well, I'm a bit late but still would like to share my way of schema creation.</p>

<p>I have schemas for everything that can be described by a word, like you would do it in the classical OOP.</p>



<ul>
<li>Comment</li>
<li>Account</li>

<li>Blogpost</li>

</ul>

<p>Every schema can be saved as a Document or Subdocument, so I declare this for each schema.</p>

<p>Document:</p>

<ul>
<li>Can be used as a reference. (E.g. the user made a comment -&gt; comment has a "made by" reference to user)</li>
<li>Is a "Root" in you application. (E.g. the blogpost -&gt; there is a page about the blogpost)</li>
</ul>

<p>Subdocument:</p>

<ul>
<li>Can only be used once / is never a reference. (E.g. Comment is saved in the blogpost)</li>
<li>Is never a "Root" in you application. (The comment just shows up in the blogpost page but the page is still about the blogpost)</li>
</ul>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 28 '14 at 9:18
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
	    

        <div id="comments-link-24992030">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-19014410">
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
<p>I know this is quite old but if you are looking for the answer to the OP's question on how to return only specified comment, you can use the <a href="http://docs.mongodb.org/manual/reference/operator/positional/#query" target="_blank">$ (query)</a> operator like this:</p>

<pre><code>db.question.update({'comments.content': 'xxx'}, {'comments.$': true})</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Sep 25 '13 at 20:16
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
	    <div id="comments-19014410">
		        <table>
                    <tbody>



    <tr id="comment-51190799">
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
                this won't work if two comments have identical contents. one might argue that we could also add author to the search query, which still wouldn't work if the author made two identical comments with same content
                    – <a href="/users/2652018/steel-brain" title="2,320 reputation" target="_blank">Steel Brain</a>
                <a href="#comment51190799_19014410" target="_blank">Jul 24 '15 at 22:46</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-19014410">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-5381238">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        36
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<blockquote>
  <p>If I want to edit a specified comment, how to get its content and its question?</p>
</blockquote>

<p>You can query by sub-document: <code>db.question.find({'comments.content' : 'xxx'})</code>.</p>

<p>This will return the whole Question document. To edit the specified comment, you then have to find the comment on the client, make the edit and save that back to the DB.</p>

<p>In general, if your document contains an array of objects, you'll find that those sub-objects will need to be modified client side.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Mar 21 '11 at 17:19
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
	    <div id="comments-5381238">
		        <table>
                    <tbody>



    <tr id="comment-51190791">
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
                this won't work if two comments have identical contents. one might argue that we could also add author to the search query, which still wouldn't work if the author made two identical comments with same content
                    – <a href="/users/2652018/steel-brain" title="2,320 reputation" target="_blank">Steel Brain</a>
                <a href="#comment51190791_5381238" target="_blank">Jul 24 '15 at 22:45</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-54369035">
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
                @SteelBrain: if he had kept the comment index, dot notation might help. see <a href="http://stackoverflow.com/a/33284416/1587329" target="_blank">stackoverflow.com/a/33284416/1587329</a>
                    – <a href="/users/1587329/serv-inc" title="6,457 reputation" target="_blank">serv-inc</a>
                <a href="#comment54369035_5381238" target="_blank">Oct 22 '15 at 15:11</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-73036345">
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
                I don't understand how this answer has 34 upvotes, the second multiple people comment the same thing the whole system would break. This is an absolutely terrible design and should never be used. The way @user does it is the way to go
                    – <a href="/users/2073973/user2073973" title="305 reputation" target="_blank">user2073973</a>
                <a href="#comment73036345_5381238" target="_blank">Mar 23 '17 at 9:30</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-5381238">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/mongodb" title="show questions tagged 'mongodb'" target="_blank">mongodb</a> <a href="/questions/tagged/reference" title="show questions tagged 'reference'" target="_blank">reference</a> <a href="/questions/tagged/embed" title="show questions tagged 'embed'" target="_blank">embed</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="https://stackoverflow.com/questions/22924300/removing-data-from-elasticsearch">https://stackoverflow.com/questions/22924300/removing-data-from-elasticsearch</a><div id="articleHeader"><h1>Removing Data From ElasticSearch</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        173
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>55</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I'm new to <a href="http://www.elasticsearch.org/" target="_blank">ElasticSearch</a>. I'm trying to figure out how to remove data from ElasticSearch. I have deleted my indexes. However, that doesn't seem to actually remove the data itself. The other stuff I've seen points to the <a href="http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/docs-delete-by-query.html" target="_blank">Delete by Query</a> feature. However, I'm not even sure what to query on. I know my indexes. Essentially, I'd like to figure out how to do a </p>

<pre><code>DELETE FROM [Index]
</code></pre>

<p>From PostMan in Chrome. However, I'm not having any luck. It seems like no matter what I do, the data hangs around. Thus far, I've successfully deleted the indexes by using the DELETE HTTP Verb in PostMan and using a url like:</p>

<pre><code>   http://localhost:9200/[indexName]
</code></pre>

<p>However, that doesn't seem to actually remove the data (aka docs) themselves.</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-22924300">
		        <table>
                    <tbody>



    <tr id="comment-65919029">
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
                I check this with postman and got reposne as "{   "acknowledged": true }" If you see this acknowledged response don't worry. The index is removed from elastic.
                    – <a href="/users/991513/bijayk" title="336 reputation" target="_blank">bijayk</a>
                <a href="#comment65919029_22924300" target="_blank">Sep 2 '16 at 12:42</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-22924300">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-22932471">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        211
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>You can delete using <code>cURL</code> or visually using one of the many tools that open source enthusiasts have created for Elasticsearch. </p>

<p><strong>Using cURL</strong></p>

<pre><code>curl -XDELETE localhost:9200/index/type/documentID
</code></pre>



<pre><code>curl -XDELETE localhost:9200/shop/product/1
</code></pre>

<p>You will then receive a reply as to whether this was successful or not. You can delete an entire index or types with an index also, you can delete a type by leaving out the document ID like so - </p>

<pre><code>curl -XDELETE localhost:9200/shop/product
</code></pre>

<p>If you wish to delete an index -</p>

<pre><code>curl -XDELETE localhost:9200/shop
</code></pre>

<p>If you wish to delete more than one index that follows a certain naming convention (note the <code>*</code>, a wildcard), -</p>

<pre><code>curl -XDELETE localhost:9200/.mar* 
</code></pre>

<p><strong>Visually</strong></p>

<p>There are various tools as mentioned above, I wont list them here but I will link you to one which enables you to get started straight away, located <a href="http://lmenezes.com/elasticsearch-kopf/" target="_blank">here</a>. This tool is called KOPF, to connect to your host please click on the logo on top left hand corner and enter the URL of your cluster.</p>

<p>Once connected you will be able to administer your entire cluster, delete, optimise and tune your cluster.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 8 '14 at 9:08
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
	    <div id="comments-22932471">
		        <table>
                    <tbody>



    <tr id="comment-50561975">
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
                is there any way I can delete 3 doc's of which id I know.
                    – <a href="/users/2463734/leonardo-da-codinchi" title="7,198 reputation" target="_blank">Leonardo Da Codinchi</a>
                <a href="#comment50561975_22932471" target="_blank">Jul 8 '15 at 6:18</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-50571695">
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
                @JayeshJain to my current knowledge, no. You could put 3 modified curl -XDELETE commands into a bash script and execute or run 3 one after the other.
                    – <a href="/users/1218285/nate" title="3,794 reputation" target="_blank">Nate</a>
                <a href="#comment50571695_22932471" target="_blank">Jul 8 '15 at 10:39</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-50571717">
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
                @JayeshJain so curl -XDELETE localhost:9200/index/type/docid1 // curl -XDELETE localhost:9200/index/type/docid2 // curl -XDELETE localhost:9200/index/type/docid3
                    – <a href="/users/1218285/nate" title="3,794 reputation" target="_blank">Nate</a>
                <a href="#comment50571717_22932471" target="_blank">Jul 8 '15 at 10:40</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-50572740">
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
                i did it the same way.but I was just thinking if there is a smarter way of deleting multiple docs. I could use term if I knew the field. But In this scenario,i just need to delete docs by their id. Thx anyways
                    – <a href="/users/2463734/leonardo-da-codinchi" title="7,198 reputation" target="_blank">Leonardo Da Codinchi</a>
                <a href="#comment50572740_22932471" target="_blank">Jul 8 '15 at 11:08</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-68956690">
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
                How can I delete an index with an invalid character, e.g., logstash-eu-%{customer}-2016.11.22. I want to delete ALL indices logstash-eu-%{customer}-* or logstash-eu-%*
                    – <a href="/users/1401560/chris-f" title="1,390 reputation" target="_blank">Chris F</a>
                <a href="#comment68956690_22932471" target="_blank">Nov 29 '16 at 16:13</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-22932471">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-22930285">
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
<p>You have to send a <code>DELETE</code> request to </p>

<pre><code>http://[your_host]:9200/[your_index_name_here]
</code></pre>

<p>You can also delete a single document: </p>

<pre><code>http://[your_host]:9200/[your_index_name_here]/[your_type_here]/[your_doc_id]
</code></pre>

<p>I suggest you to use <a href="http://elastichammer.exploringelasticsearch.com/" target="_blank">elastichammer</a>.</p>

<p>After deleting you can look up if the index still exists with the following URL: <code>http://[your_host]:9200/_stats/</code></p>

<p>Good luck!</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-22930285">
		        <table>
                    <tbody>



    <tr id="comment-78953905">
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
                what is the way to delete indices older than 10 days ? I can not use curator because my server is not support.
                    – <a href="/users/1920536/biolinh" title="967 reputation" target="_blank">biolinh</a>
                <a href="#comment78953905_22930285" target="_blank">Sep 1 '17 at 9:19</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-22930285">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-30953261">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        234
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If you ever need to delete all the indexes, this may come in handy:</p>

<pre><code>curl -X DELETE 'http://localhost:9200/_all'
</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
    <td>
    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jun 20 '15 at 11:06
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
	    <div id="comments-30953261">
		        <table>
                    <tbody>



    <tr id="comment-53335358">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                10
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
                this is very useful for development and needing to reset back to scratch (empty) database. Thanks!!
                    – <a href="/users/372215/artistan" title="740 reputation" target="_blank">Artistan</a>
                <a href="#comment53335358_30953261" target="_blank">Sep 23 '15 at 18:55</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-57814187">
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
                in your bash_profile create an alias for this command and it will come in handy for development.
                    – <a href="/users/805981/user805981" title="1,753 reputation" target="_blank">user805981</a>
                <a href="#comment57814187_30953261" target="_blank">Jan 27 '16 at 18:15</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-61367567">
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
                'Wildcard expressions or all indices are not allowed'
                    – <a href="/users/1016530/piero" title="497 reputation" target="_blank">Piero</a>
                <a href="#comment61367567_30953261" target="_blank">Apr 27 '16 at 22:03</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-72425268">
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
    <tr id="comment-72425319">
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

        <div id="comments-link-30953261">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>3</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-31747997">
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
<p>For mass-delete by query you may use special API: <a href="https://www.elastic.co/guide/en/elasticsearch/reference/1.6/docs-delete-by-query.html" target="_blank">https://www.elastic.co/guide/en/elasticsearch/reference/1.6/docs-delete-by-query.html</a></p>

<p>Although it is deprecated it still works and much more convenient for mass delete.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 31 '15 at 13:57
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
	    <div id="comments-31747997">
		        <table>
                    <tbody>



    <tr id="comment-51699016">
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
                Be careful using delete by query. Its deprecated for a major reason. OutOfMemoryError!
                    – <a href="/users/3658423/user3658423" title="796 reputation" target="_blank">user3658423</a>
                <a href="#comment51699016_31747997" target="_blank">Aug 8 '15 at 8:01</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-51745669">
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
                Sure. But you may spy if it happened for you or you have anough memory.
                    – <a href="/users/307525/hubbitus" title="1,546 reputation" target="_blank">Hubbitus</a>
                <a href="#comment51745669_31747997" target="_blank">Aug 10 '15 at 9:52</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-31747997">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-37549582">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        24
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>The <a href="https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-delete-index.html" target="_blank">documentation</a> (or <a href="https://www.elastic.co/guide/en/elasticsearch/guide/current/_deleting_an_index.html" target="_blank">The Definitive Guide</a>) says, that you can also use the next query to delete <em>all</em> indices:</p>

<p><code>curl -XDELETE 'http://localhost:9200/*'</code></p>

<p>And there's an important note:</p>

<blockquote>
  <p>For some, the ability to delete all your data with a single command is a very scary prospect. If you want to eliminate the possibility of an accidental mass-deletion, you can set the following to <code>true</code> in your <code>elasticsearch.yml</code>:</p>
  
  <p><code>action.destructive_requires_name: true</code></p>
</blockquote>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered May 31 '16 at 15:16
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
	    

        <div id="comments-link-37549582">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-39798144">
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
<p>Deleting the index will delete the mapping and type along. you can delete all rows by the following query</p>

<pre><code>curl -XDELETE 'localhost:9200/twitter/tweet/_query?pretty' -d'
{
   "query": { 
      "match_all": 
   }
}'
</code></pre>

<p>However for above query you need to install delete-by-query plugin as of Elasticsearch's 2.0.0-beta1  delete-by-query was removed from main api</p>

<pre><code>Install delete-by-query plugin

sudo bin/plugin install delete-by-query
</code></pre>

<p>For more </p>

<p><a href="http://blog.appliedinformaticsinc.com/how-to-delete-elasticsearch-data-records-by-dsl-query/" target="_blank">http://blog.appliedinformaticsinc.com/how-to-delete-elasticsearch-data-records-by-dsl-query/</a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-39798144">
		        <table>
                    <tbody>



    <tr id="comment-72318560">
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
                Both before and after installing the plugin and restarting ES, I get "No handler found for uri and method".
                    – <a href="/users/507761/matthew-read" title="459 reputation" target="_blank">Matthew Read</a>
                <a href="#comment72318560_39798144" target="_blank">Mar 4 '17 at 7:51</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-39798144">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-40487524">
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
<p>There are lots of good answers here, but there is also something i'd like to add:</p>

<ul>
<li>If you are running on <strong>AWS ElasticSearch service</strong>, <strong>you can´t drop/delete indexes</strong>. <strong><em>Instead of delete indexes, you must reindex them</em></strong>.</li>
</ul>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Nov 8 '16 at 12:55
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
	    <div id="comments-40487524">
		        <table>
                    <tbody>



    <tr id="comment-73344727">
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
                Just deleted an index on AWS ElasticSearch, my domain is running ES 5.1.
                    – <a href="/users/411355/gazarsgo" title="46 reputation" target="_blank">gazarsgo</a>
                <a href="#comment73344727_40487524" target="_blank">Mar 31 '17 at 6:04</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-40487524">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-43230386">
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
<p>You can delete an index in python as follows</p>

<pre><code>from elasticsearch import Elasticsearch

es = Elasticsearch([{'host':'localhost', 'port':'9200'}])

es.index(index='grades',doc_type='ist_samester',id=1,body={
    "Name":"Programming Fundamentals",
    "Grade":"A"
})

es.indices.delete(index='grades')
</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-43230386">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-44693558">
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
<pre><code>#list all index:       curl -XGET http://localhost:9200/_cat/indices?v 
</code></pre>

<p><a href="https://i.stack.imgur.com/7CK5P.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/7CK5P.png" alt="enter image description here" /></div></a> </p>

<pre><code>#delete index:         curl -XDELETE 'localhost:9200/index_name'
#delete all indices:   curl -XDELETE 'localhost:9200/_all'
#delete document   :   curl -XDELETE 'localhost:9200/index_name/type_name/document_id'
</code></pre>

<blockquote>
  <p>Install <a href="https://www.elastic.co/products/kibana" target="_blank">kibana</a>. Kibana has a smarter dev tool which helps to build query easily.</p>
</blockquote>

<p><a href="https://i.stack.imgur.com/kpXdU.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/kpXdU.png" alt="enter image description here" /></div></a></p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jun 22 '17 at 8:00
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
	    <div id="comments-44693558">
		        <table>
                    <tbody>



    <tr id="comment-78953893">
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
                what is the way to delete indices older than 10 days ? I can not use curator because my server is not support.
                    – <a href="/users/1920536/biolinh" title="967 reputation" target="_blank">biolinh</a>
                <a href="#comment78953893_44693558" target="_blank">Sep 1 '17 at 9:18</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-44693558">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-45099742">
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
<p>I wanted to delete logstash index and searched a lot regarding different tools like curl. But found the solution at the end. 
Login into Kibana. Go to Dev Tools tab and type <code>DELETE /logstash-*</code> in query field and hit green arrow button. if you get "acknowledged": true in response that means the data has been cleared.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-45099742">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-45922199">
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
<p>simplest way !</p>

<pre><code>Endpoint :
http://localhost:9201/twitter/_delete_by_query

Payload :
{
  "query": { 
    "match": {
      "message": "some message"
    }
  }
}
</code></pre>

<p>where <code>twitter</code> is the index in elastic search</p>

<p>ref ; <a href="https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-delete-by-query.html" target="_blank">https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-delete-by-query.html</a></p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Aug 28 '17 at 15:11
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
	    

        <div id="comments-link-45922199">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-46277674">
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
<pre><code>You can delete either whole index,doc-type or a perticular id data.
these are the three ways:
1. curl -XDELETE localhost:9200/index_name

2. curl -XDELETE localhost:9200/index_name/doc-type

3. curl -XDELETE localhost:9200/index_name/doc-type/documentId

and if you wish to delete all the index then go for wildcard.
</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Sep 18 '17 at 11:00
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
	    

        <div id="comments-link-46277674">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-46579947">
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
<p>Using Curl :-</p>

<p>1) Delete a document from index</p>

<pre><code>curl -XDELETE 'localhost:9200/indexName/type/documentId?pretty&pretty'           
</code></pre>

<p>Example: <code>curl -XDELETE 'localhost:9200/mentorz/users/10557?pretty&pretty'</code></p>

<p>2) Delete a whole index:-</p>

<pre><code>curl -XDELETE 'localhost:9200/indexName?pretty&pretty'                             
</code></pre>

<p>Example: <code>curl -XDELETE 'localhost:9200/mentorz?pretty&pretty'</code> </p>

<p>for more details you can find here -<a href="https://www.elastic.co/guide/en/elasticsearch/reference/current/_deleting_documents.html" target="_blank">https://www.elastic.co/guide/en/elasticsearch/reference/current/_deleting_documents.html</a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-46579947">

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
Not the answer you're looking for?                            Browse other questions tagged   or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
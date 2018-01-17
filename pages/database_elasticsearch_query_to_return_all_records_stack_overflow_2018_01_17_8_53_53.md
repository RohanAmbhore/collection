<a href="https://stackoverflow.com/questions/8829468/elasticsearch-query-to-return-all-records">https://stackoverflow.com/questions/8829468/elasticsearch-query-to-return-all-records</a><div id="articleHeader"><h1>Elasticsearch query to return all records</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        311
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>85</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I have a small database in Elasticsearch and for testing purposes would like to pull all records back.  I am attempting to use a URL of the form...</p>

<pre><code>http://localhost:9200/foo/_search?pretty=true&q={'matchAll':{''}}
</code></pre>

<p>Can someone give me the URL you would use to accomplish this, please?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-8829468">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-8831494">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        477
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>I think lucene syntax is supported so:</p>

<p><code>http://localhost:9200/foo/_search?pretty=true&q=*:*</code></p>

<p>size defaults to 10, so you may also need <code>&size=BIGNUMBER</code> to get more than 10 items. (where BIGNUMBER equals a number you believe is bigger than your dataset)</p>

<p>BUT, elasticsearch documentation <a href="https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-search-type.html" target="_blank">suggests</a> for large result sets, using the scan search type.</p>



<pre><code>curl -XGET 'localhost:9200/foo/_search?search_type=scan&scroll=10m&size=50' -d '
{
    "query" : {
        "match_all" : {}
    }
}'
</code></pre>

<p>and then keep requesting as per the documentation link above suggests.</p>

<p>EDIT: <code>scan</code> Deprecated in 2.1.0.</p>

<p><code>scan</code> does not provide any benefits over a regular <code>scroll</code> request sorted by <code>_doc</code>. <a href="https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-search-type.html#scan" target="_blank">link to elastic docs</a> (spotted by @christophe-roussy)</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-8831494">
		        <table>
                    <tbody>



    <tr id="comment-11027931">
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
            
        </td>
    </tr>
    <tr id="comment-26259332">
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
    <tr id="comment-27628335">
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
                Thanks @Steve for your answer. I didn't think it was significant enough for a new question. It wasn't explicitly stated anywhere, so I figured I'd ask here just to verify.
                    – <a href="/users/1038832/churro" title="1,772 reputation" target="_blank">Churro</a>
                <a href="#comment27628335_8831494" target="_blank">Sep 11 '13 at 15:32</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-29873412">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                7
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
                You should really use the scan+scroll-requests. If you do use size=BIGNUMBER, note that Lucene allocates memory for scores for that number, so don't make it exceedingly large. :)
                    – <a href="/users/230253/alex-brasetvik" title="8,142 reputation" target="_blank">Alex Brasetvik</a>
                <a href="#comment29873412_8831494" target="_blank">Nov 18 '13 at 19:33</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-61556606">
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
            
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-8831494">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>8</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-22513070">
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
<p>The query below would return the NO_OF_RESULTS you would like to be returned..</p>

<pre><code>curl -XGET 'localhost:9200/foo/_search?size=NO_OF_RESULTS' -d '
{
"query" : {
    "match_all" : {}
  }
}'
</code></pre>

<p>Now, the question here is that you want <strong>all</strong> the records to be returned. So naturally, before writing a query, you wont know the value of <strong>NO_OF_RESULTS</strong>. </p>

<p>How do we know how many records exist in your document? Simply type the query below</p>

<pre><code>curl -XGET 'localhost:9200/foo/_search' -d '
</code></pre>

<p>This would give you a result that looks like the one below </p>

<pre><code> {
hits" : {
  "total" :       2357,
  "hits" : [
    {
      ..................
</code></pre>

<p>The result <strong>total</strong> tells you how many records are available in your document. So, that's a nice way to know the value of <strong>NO_OF RESULTS</strong></p>

<pre><code>curl -XGET 'localhost:9200/_search' -d ' 
</code></pre>

<p>Search all types in all indices</p>

<pre><code>curl -XGET 'localhost:9200/foo/_search' -d '
</code></pre>

<p>Search all types in the foo index</p>

<pre><code>curl -XGET 'localhost:9200/foo1,foo2/_search' -d '
</code></pre>

<p>Search all types in the foo1 and foo2 indices</p>

<pre><code>curl -XGET 'localhost:9200/f*/_search
</code></pre>

<p>Search all types in any indices beginning with f</p>

<pre><code>curl -XGET 'localhost:9200/_all/type1,type2/_search' -d '
</code></pre>

<p>Search types user and tweet in all indices</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-22513070">
		        <table>
                    <tbody>



    <tr id="comment-34953607">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                8
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
                By default ES will return 10 results unless a size param is included in the base query.
                    – <a href="/users/1426788/lfender6445" title="12,315 reputation" target="_blank">lfender6445</a>
                <a href="#comment34953607_22513070" target="_blank">Apr 7 '14 at 3:11</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-50701729">
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
                The previous response was three years old. Updated it to a current one.
                    – <a href="/users/3438582/vjpan8564" title="340 reputation" target="_blank">vjpan8564</a>
                <a href="#comment50701729_22513070" target="_blank">Jul 11 '15 at 18:19</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-22513070">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-22903026">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        89
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<pre><code>http://127.0.0.1:9200/foo/_search/?size=1000&pretty=1
                                   ^
</code></pre>

<p><strong>Note the size param</strong>, which increases the hits displayed from the default (10) to 1000 per shard.</p>

<p><a href="http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/search-request-from-size.html" target="_blank">http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/search-request-from-size.html</a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-22903026">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-25364398">
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
<p>use <code>server:9200/_stats</code> also to get statistics about all your aliases.. like size and number of elements per alias, that's very useful and provides helpful information</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Aug 18 '14 at 13:21
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
	    <div id="comments-25364398">
		        <table>
                    <tbody>



    <tr id="comment-61207059">
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
                But, from what I remember, ES only allow getting 16000 data per request. So if the data is above 16000, this solution is not enough.
                    – <a href="/users/1564659/aminah-nuraini" title="4,306 reputation" target="_blank">Aminah Nuraini</a>
                <a href="#comment61207059_25364398" target="_blank">Apr 23 '16 at 22:48</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-25364398">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-32832160">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        20
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>elasticsearch(ES) supports both a GET or a POST request for getting the data from the ES cluster index. </p>

<p>When we do a GET:</p>

<pre><code>http://localhost:9200/[your index name]/_search?size=[no of records you want]&q=*:*
</code></pre>

<p>When we do a POST:</p>

<pre><code>http://localhost:9200/[your_index_name]/_search
{
  "size": [your value] //default 10
  "from": [your start index] //default 0
  "query":
   {
    "match_all": {}
   }
}   
</code></pre>

<p>I would suggest to use a UI plugin with elasticsearch <a href="http://mobz.github.io/elasticsearch-head/" target="_blank">http://mobz.github.io/elasticsearch-head/</a>
This will help you get a better feeling of the indices you create and also test your indices.  </p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Sep 28 '15 at 21:31
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
	    

        <div id="comments-link-32832160">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-33830831">
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
<p>Elasticsearch will get <strong>significant</strong> slower if you just add some big number as size, one method to use to get all documents is using scan and scroll ids.</p>

<p>So your call would be:</p>

<pre><code>GET /foo/_search?search_type=scan&scroll=1m
{
    "query": { "match_all": {}},
    "size":  1000
}
</code></pre>

<p>This will return a _scroll_id, which you can now use to get the first batch of documents.</p>

<p><a href="https://www.elastic.co/guide/en/elasticsearch/guide/current/scan-scroll.html" target="_blank">https://www.elastic.co/guide/en/elasticsearch/guide/current/scan-scroll.html</a></p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Nov 20 '15 at 15:53
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
	    

        <div id="comments-link-33830831">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-34264723">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Simple! You can use <code>size</code> and <code>from</code> parameter!</p>

<pre><code>http://localhost:9200/[your index name]/_search?size=1000&from=0
</code></pre>

<p>then you change the <code>from</code> gradually until you get all of the data.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-34264723">
		        <table>
                    <tbody>



    <tr id="comment-77398347">
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
                never use this method if the data contains many documents... Each time you go to "the next page" Elastic will be slower and slower! Use SearchAfter instead
                    – <a href="/users/447371/joshlo" title="153 reputation" target="_blank">Joshlo</a>
                <a href="#comment77398347_34264723" target="_blank">Jul 20 '17 at 13:25</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-34264723">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-35332946">
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
<p>A few of them gave the right answer of using scan and scroll, apparently, I could not a complete answer which would magically work. When someone wants to pull of records then one has to run following curl command.</p>

<pre><code>curl -XGET 'http://ip1:9200/myindex/_search?scroll=1m' -d '
{
    "query": {
            "match_all" : {}
    }
}
'
</code></pre>

<p>But we are not done here. The output of the above curl command would be something like this </p>

<pre><code>{"_scroll_id":"c2Nhbjs1OzUyNjE6NU4tU3BrWi1UWkNIWVNBZW43bXV3Zzs1Mzc3OkhUQ0g3VGllU2FhemJVNlM5d2t0alE7NTI2Mjo1Ti1TcGtaLVRaQ0hZU0FlbjdtdXdnOzUzNzg6SFRDSDdUaWVTYWF6YlU2Uzl3a3RqUTs1MjYzOjVOLVNwa1otVFpDSFlTQWVuN211d2c7MTt0b3RhbF9oaXRzOjIyNjAxMzU3Ow==","took":109,"timed_out":false,"_shards":{"total":5,"successful":5,"failed":0},"hits":{"total":22601357,"max_score":0.0,"hits":[]}}
</code></pre>

<p>its important to have _scroll_id handy as the very next you shd run the following command </p>

<pre><code>    curl -XGET  'localhost:9200/_search/scroll'  -d'
    {
        "scroll" : "1m", 
        "scroll_id" : "c2Nhbjs2OzM0NDg1ODpzRlBLc0FXNlNyNm5JWUc1" 
    }
    '
</code></pre>

<p>However, I dont think its easy to run this manually. Your best bet is to write a java code to do the same. </p>

<pre><code>    private TransportClient client = null;
    private Settings settings = ImmutableSettings.settingsBuilder()
                  .put(CLUSTER_NAME,"cluster-test").build();
    private SearchResponse scrollResp  = null;

    this.client = new TransportClient(settings);
    this.client.addTransportAddress(new InetSocketTransportAddress("ip", port));

    QueryBuilder queryBuilder = QueryBuilders.matchAllQuery();
    scrollResp = client.prepareSearch(index).setSearchType(SearchType.SCAN)
                 .setScroll(new TimeValue(60000))                            
                 .setQuery(queryBuilder)
                 .setSize(100).execute().actionGet();

    scrollResp = client.prepareSearchScroll(scrollResp.getScrollId())
                .setScroll(new TimeValue(timeVal))
                .execute()
                .actionGet();
</code></pre>

<p>Now LOOP on the last command use SearchResponse to extract the data.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Feb 11 '16 at 7:13
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
	    

        <div id="comments-link-35332946">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-37752835">
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
<p>This is the best solution I found using python client</p>

<pre><code>  # Initialize the scroll
  page = es.search(
  index = 'yourIndex',
  doc_type = 'yourType',
  scroll = '2m',
  search_type = 'scan',
  size = 1000,
  body = {
    # Your query's body
    })
  sid = page['_scroll_id']
  scroll_size = page['hits']['total']

  # Start scrolling
  while (scroll_size &gt; 0):
    print "Scrolling..."
    page = es.scroll(scroll_id = sid, scroll = '2m')
    # Update the scroll ID
    sid = page['_scroll_id']
    # Get the number of results that we returned in the last scroll
    scroll_size = len(page['hits']['hits'])
    print "scroll size: " + str(scroll_size)
    # Do something with the obtained page</code></pre>

<p><a href="https://gist.github.com/drorata/146ce50807d16fd4a6aa" target="_blank">https://gist.github.com/drorata/146ce50807d16fd4a6aa</a></p>

<p>Using java client </p>

<pre><code>import static org.elasticsearch.index.query.QueryBuilders.*;

QueryBuilder qb = termQuery("multi", "test");

SearchResponse scrollResp = client.prepareSearch(test)
        .addSort(FieldSortBuilder.DOC_FIELD_NAME, SortOrder.ASC)
        .setScroll(new TimeValue(60000))
        .setQuery(qb)
        .setSize(100).execute().actionGet(); //100 hits per shard will be returned for each scroll
//Scroll until no hits are returned
do {
    for (SearchHit hit : scrollResp.getHits().getHits()) {
        //Handle the hit...
    }

    scrollResp = client.prepareSearchScroll(scrollResp.getScrollId()).setScroll(new TimeValue(60000)).execute().actionGet();
} while(scrollResp.getHits().getHits().length != 0); // Zero hits mark the end of the scroll and the while loop.</code></pre>

<p><a href="https://www.elastic.co/guide/en/elasticsearch/client/java-api/current/java-search-scrolling.html" target="_blank">https://www.elastic.co/guide/en/elasticsearch/client/java-api/current/java-search-scrolling.html</a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-37752835">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-38874465">
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
<p>The best way to adjust the size is using size=<strong>number</strong> in front of the URL </p>

<pre><code>Curl -XGET "http://localhost:9200/logstash-*/_search?size=50&pretty"
</code></pre>

<p>Note: maximum value which can be defined in this size is 10000. For any value above ten thousand it expects you to use scroll function which would minimise any chances of impacts to performance.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-38874465">
		        <table>
                    <tbody>



    <tr id="comment-71245128">
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
                Since which version does max size occur?
                    – <a href="/users/2553276/woodydrn" title="549 reputation" target="_blank">WoodyDRN</a>
                <a href="#comment71245128_38874465" target="_blank">Feb 4 '17 at 1:10</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-38874465">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-41442261">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>You can  use size=0 this will return you all the documents 
example</p>

<pre><code>curl -XGET 'localhost:9200/index/type/_search' -d '
{
   size:0,
   "query" : {
   "match_all" : {}
    }
}'
</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jan 3 '17 at 11:16
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
	    <div id="comments-41442261">
		        <table>
                    <tbody>



    <tr id="comment-73317254">
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
                This will return an accumulated information, but not the hits themselves
                    – <a href="/users/732456/user732456" title="1,273 reputation" target="_blank">user732456</a>
                <a href="#comment73317254_41442261" target="_blank">Mar 30 '17 at 13:17</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-77118808">
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
                sorry, i have to downvote for misleading
                    – <a href="/users/1823396/esgi-dendyanri" title="108 reputation" target="_blank">Esgi Dendyanri</a>
                <a href="#comment77118808_41442261" target="_blank">Jul 13 '17 at 6:40</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-41442261">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-43539749">
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
<p><a href="http://localhost:9200/foo/_search/" target="_blank">http://localhost:9200/foo/_search/</a>?<strong>size</strong>=1000&pretty=1</p>

<p>you will need to specify size query parameter as the default is 10</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 21 '17 at 10:03
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
	    <div id="comments-43539749">
		        <table>
                    <tbody>



    <tr id="comment-75786714">
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
    <tr id="comment-75789974">
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
                you are welcome @hamzeh.hanandeh.....glad this helped someone else
                    – <a href="/users/3139595/edwin-ikechukwu" title="1,155 reputation" target="_blank">Edwin Ikechukwu</a>
                <a href="#comment75789974_43539749" target="_blank">Jun 6 '17 at 16:20</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-43539749">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-44598418">
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
<p>You can use the <a href="https://www.elastic.co/guide/en/elasticsearch/reference/current/search-count.html" target="_blank"><code>_count</code></a> API to get the value for the <code>size</code> parameter:</p>

<pre><code>http://localhost:9200/foo/_count?q=&lt;your query&gt;
</code></pre>

<p>Returns <code>{count:X, ...}</code>. Extract value 'X' and then do the actual query:</p>

<pre><code>http://localhost:9200/foo/_search?q=&lt;your query&gt;&size=X
</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jun 16 '17 at 21:43
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
	    

        <div id="comments-link-44598418">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/database" title="show questions tagged 'database'" target="_blank">database</a>  <a href="/questions/tagged/bigdata" title="show questions tagged 'bigdata'" target="_blank">bigdata</a> <a href="/questions/tagged/query-string" title="show questions tagged 'query-string'" target="_blank">query-string</a> <a href="/questions/tagged/elasticsearch-dsl" title="show questions tagged 'elasticsearch-dsl'" target="_blank">elasticsearch-dsl</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
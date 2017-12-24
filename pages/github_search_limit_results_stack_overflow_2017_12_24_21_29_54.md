<a href="https://stackoverflow.com/questions/37602893/github-search-limit-results">https://stackoverflow.com/questions/37602893/github-search-limit-results</a><div id="articleHeader"><h1>github search limit results</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        4
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>2</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I need to do a very large search on Github for a statistic in my thesis. </p>

<p>For example, I need to explore a large number of Android projects on GitHub, but the site limits the search result to 1000 (ex. <a href="https://github.com/search?l=java&q=onCreate&ref=searchresults&type=Code&utf8=%E2%9C%93" target="_blank">https://github.com/search?l=java&q=onCreate&ref=searchresults&type=Code&utf8=%E2%9C%93</a>). Also using the Java GitHub API I tried the library org.eclipse.egit.github.core.client.GitHubClient using the method <code>GitHubClient.searchRepositories()</code> but even there the number of results is limited. </p>

<p>Does anyone know how to get all results?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-37602893">
		        <table>
                    <tbody>



    <tr id="comment-62690620">
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
                Have you looked at the <a href="https://www.githubarchive.org/" target="_blank">GitHub Archive</a>? It could be a way to get your data without having to bother the live GitHub search API, which as you found out gives a limited number of results, and is also rate-limited.
                    – <a href="/users/182402/wander-nauta" title="9,448 reputation" target="_blank">Wander Nauta</a>
                <a href="#comment62690620_37602893" target="_blank">Jun 2 '16 at 22:12</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-62690783">
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
                Are you able to page through the results? You could get the first chunk of 1000, get the next chunk, and repeat until you have it all.
                    – <a href="/users/940217/kyle-falconer" title="4,203 reputation" target="_blank">Kyle Falconer</a>
                <a href="#comment62690783_37602893" target="_blank">Jun 2 '16 at 22:19</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-62690836">
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
                This is not a Java question, or even a programming question.
                    – <a href="/users/1553851/shmosel" title="28,835 reputation" target="_blank">shmosel</a>
                <a href="#comment62690836_37602893" target="_blank">Jun 2 '16 at 22:23</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-62692964">
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
    <tr id="comment-70482783">
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
                Is your code publicly available?
                    – <a href="/users/3158028/soubriquet" title="573 reputation" target="_blank">Soubriquet</a>
                <a href="#comment70482783_37602893" target="_blank">Jan 13 at 18:48</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-37602893">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-37639739">
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
<p>The Search API will return up to 1000 results per query (including pagination), as documented here:</p>

<p><a href="https://developer.github.com/v3/search/#about-the-search-api" target="_blank">https://developer.github.com/v3/search/#about-the-search-api</a></p>

<p>However, there's a neat trick you could use to fetch more than 1000 results when executing a repository search. You could split up your search into segments, by the date when the repositories were created. For example, you could first search for repositories that were created in the first week of October 2013, then second week, then September, and so on.</p>

<p>Because you would be restricting search to a narrow period, you will probably get less than 1000 results, and would therefore be able to get all of them. In case you notice that more than 1000 results are returned for a period, you would have to narrow the period even more, so that you can collect all results.</p>

<p><a href="https://help.github.com/articles/searching-repositories/#search-based-on-when-a-repository-was-created-or-last-updated" target="_blank">https://help.github.com/articles/searching-repositories/#search-based-on-when-a-repository-was-created-or-last-updated</a></p>

<p>You should be able to automate this via the API.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jun 5 '16 at 8:03
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
	    <div id="comments-37639739">
		        <table>
                    <tbody>



    <tr id="comment-70482791">
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
    <tr id="comment-70532850">
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
                Seems like you can't query the repository search api by date created. The following will search, but sort, order, and created are ignored: <code>curl -H 'Accept: application/vnd.github.v3.text-match+json' 'https://api.github.com/search/repositories?q=language:Java&‌​created&gt;=2013-04-11T‌​00:00:00Z&sort=creat‌​ed&order=asc' | grep created_at</code>
                    – <a href="/users/3158028/soubriquet" title="573 reputation" target="_blank">Soubriquet</a>
                <a href="#comment70532850_37639739" target="_blank">Jan 15 at 23:09</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-70545022">
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
                @Soubriquet You're not constructing that URL correctly. The "created" parameter should be a part of the query, not a parameter on its own.
                    – <a href="/users/1673062/ivan-zuzak" title="10,389 reputation" target="_blank">Ivan Zuzak</a>
                <a href="#comment70545022_37639739" target="_blank">Jan 16 at 10:06</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-70545056">
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
                Also, you can't sort by created -- the fields you can sort by are listed here: <a href="https://developer.github.com/v3/search/#parameters" target="_blank">developer.github.com/v3/search/#parameters</a>
                    – <a href="/users/1673062/ivan-zuzak" title="10,389 reputation" target="_blank">Ivan Zuzak</a>
                <a href="#comment70545056_37639739" target="_blank">Jan 16 at 10:07</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-70552977">
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
                Awesome! Thanks! In case anyone else needs this: <code>https://api.github.com/search/repositories?q=language:Java+c‌​reated:&gt;=2013-04-11T‌​00:00:00Z&order=asc</code>
                    – <a href="/users/3158028/soubriquet" title="573 reputation" target="_blank">Soubriquet</a>
                <a href="#comment70552977_37639739" target="_blank">Jan 16 at 13:52</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-37639739">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>1</b> more comment</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-47828323">
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
<p>If you are searching for all files in Github with filename:your-file-name, you could also slice it with <a href="https://help.github.com/articles/searching-code/#search-by-the-source-code-file-size" target="_blank">a query attribute : size</a>. </p>

<p>For example, you are looking for all files named test.rb in Github, Github API may return more than 11M results, but you could only get 1000 of them because <a href="https://developer.github.com/v3/search/#about-the-search-api" target="_blank">the GitHub Search API provides up to 1,000 results for each search</a>. An url like : <a href="https://api.github.com/search/code?q=filename:test.rb+size:1000..1500" target="_blank">https://api.github.com/search/code?q=filename:test.rb+size:1000..1500</a> would be able to slice your search by changing size range.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-47828323">
		        <table>
                    <tbody>



    <tr id="comment-82619589">
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
                While this link may answer the question, it is better to include the essential parts of the answer here and provide the link for reference.  Link-only answers can become invalid if the linked page changes. - <a href="/review/low-quality-posts/18263687" target="_blank">From Review</a>
                    – <a href="/users/1219012/artem-mostyaev" title="2,151 reputation" target="_blank">Artem Mostyaev</a>
                <a href="#comment82619589_47828323" target="_blank">Dec 15 at 8:43</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-82633113">
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

        <div id="comments-link-47828323">

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
Not the answer you're looking for?                            Browse other questions tagged  <a href="/questions/tagged/github-api" title="show questions tagged 'github-api'" target="_blank">github-api</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
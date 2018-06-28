<a href="https://stackoverflow.com/questions/44919773/how-do-i-query-the-github-v4-api-for-directory-contents-at-a-certain-tag">https://stackoverflow.com/questions/44919773/how-do-i-query-the-github-v4-api-for-directory-contents-at-a-certain-tag</a><div id="articleHeader"><h1>How do I query the GitHub v4 API for directory contents at a certain tag?</h1></div>

            

<div id="question">

    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        2
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>1</b></div>


</div>

            </div>

            
<div>
    <div>

<p>How do I query the <a href="https://developer.github.com/v4/reference/" target="_blank">GitHub API v4</a> for the contents of a certain directory of a repository at a certain tag?</p>

<p>This is the best I've come up with so far:</p>

<pre><code>query {
  repository(owner:"example", name:"example") {
    refs(refPrefix: "tags") {
    }
  } 
}
</code></pre>
    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-44934363">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>From <a href="https://stackoverflow.com/questions/44137710/github-graphql-equivalent-of-the-contents-api" target="_blank">this post</a>, you can get the <code>GitObject</code> with <code>object</code> to filter on <code>branch:/path/folder</code> and print the <code>Tree</code>. The following will get the tree from <code>gson</code> folder from tag <code>gson-2.4</code> and print <code>name</code>, <code>type</code> and <code>mode</code> : </p>

<pre><code>query {
  repository(owner:"google", name:"gson") {
      object(expression: "gson-2.4:gson") {
      ... on Tree{
        entries{
          name
          type
          mode
        }
      }
    }
  } 
}
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jul 5 '17 at 19:18
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/graphql" title="show questions tagged 'graphql'" target="_blank">graphql</a> <a href="/questions/tagged/github-api" title="show questions tagged 'github-api'" target="_blank">github-api</a> <a href="/questions/tagged/github-graphql" title="show questions tagged 'github-graphql'" target="_blank">github-graphql</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
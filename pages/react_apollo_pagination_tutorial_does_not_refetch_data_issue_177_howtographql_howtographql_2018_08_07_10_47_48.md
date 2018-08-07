<a href="https://github.com/howtographql/howtographql/issues/177">https://github.com/howtographql/howtographql/issues/177</a><div id="articleHeader"><h1>              React Apollo Pagination tutorial does not refetch data?            #177    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/scotmatson" target="_blank">scotmatson</a>  opened this Issue
        <relative-time>on Aug 5, 2017</relative-time>
        · 2 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          <div>
            




            
<div id="issue-248093517">
  <div>

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/scotmatson" target="_blank">scotmatson</a>
  

    </strong>

    commented

    <a href="#issue-248093517" target="_blank"><relative-time>on Aug 5, 2017</relative-time></a>


    
      <include-fragment>
            
  •


  
    <summary>
      <div>
        
            edited
        
        
      </div>
    </summary>
    
  

      </include-fragment>
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I was trying out the Apollo-Client as in lieu of Relay as it provides better support for offset-based pagination. Following the tutorial at <a href="https://www.howtographql.com/react-apollo/9-pagination/" target="_blank">https://www.howtographql.com/react-apollo/9-pagination/</a>, when the _nextPage() event is triggered the page paginates forward but data is not being fetched.</p>
<p>It isn't exactly mentioned in this tutorial what is handling the refetch and I'm wondering if I overlooked something or if this could be better implemented to address a more general use case.</p>
<p>The Apollo documentation uses <code>fetchMore</code>, but this isn't really a correct solution for offset-based pagination as much as it is more for cursor based pagination. <a href="http://dev.apollodata.com/react/pagination.html#numbered-pages" target="_blank">http://dev.apollodata.com/react/pagination.html#numbered-pages</a>. However changing this <code>feed: [...previousResult.feed, ...fetchMoreResult.feed]</code> to simply <code>feed: [...fetchMoreResult.feed]</code> does achieve a more offset-like result, so perhaps I'm being overly picky in respects to that.</p>
<p>I noticed there is <code>refetchQueries</code> that looks like a possible solution <a href="http://dev.apollodata.com/react/cache-updates.html#refetchQueries" target="_blank">http://dev.apollodata.com/react/cache-updates.html#refetchQueries</a> but am inexperienced with this client and am wondering if I'm missing something or if this tutorial should be revisited/updated.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>

          </div>

          

  


  


  
<div>
    
  <div>

  




  
<div id="issuecomment-337109316">
    
  <div>

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/ghost" target="_blank">ghost</a>

    </strong>

    commented

    <a href="#issuecomment-337109316" target="_blank"><relative-time>on Oct 17, 2017</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I had the same issue as well although I was working on the new version of Apollo Client 2. So hopefully I will not be confusing anyone here. I managed to find a piece of documentation in Apollo Client about an option named <a href="http://dev.apollodata.com/react/api-queries.html#graphql-config-options-fetchPolicy" target="_blank">FetchPolicy</a> . It appears that FetchPolicy is defaulted to cache-first and so debugging the Pagination code showed that the pages were being moved by the data was loaded from the store in Apollo Client instead of firing a call to the GraphCool server.</p>
<p>I managed to get around that by setting that option to  'cache-and-network' when exporting the LinkList Component<br />
`export default graphql(ALL_LINKS_QUERY, {<br />
name: 'allLinksQuery',<br />
options: (ownProps) =&gt; {<br />
const page = parseInt(ownProps.match.params.page, 10);<br />
const isNewPage = ownProps.location.pathname.includes('new');<br />
const skip = isNewPage ? (page - 1) * LINKS_PER_PAGE : 0;<br />
const first = isNewPage ? LINKS_PER_PAGE : 100;<br />
const orderBy = isNewPage ? 'createdAt_DESC' : null;</p>
<pre><code> return {
   variables: { first, skip, orderBy },
   fetchPolicy: 'cache-and-network'     // Apollo Client 2 sets this to cache-first which will grab stale data from the store
 };
</code></pre>
<p>}<br />
})(LinkList);`</p>
<p>I have a version of the tutorial using Apollo Client 2 and the latest subscriptions-transport-ws if you are interested <a href="https://github.com/oredi/howtographql-react-apollo" target="_blank">React Apollo Client v 2.0</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-365546006">
    
  <div>

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/nikolasburk" target="_blank">nikolasburk</a>
  

    </strong>

    commented

    <a href="#issuecomment-365546006" target="_blank"><relative-time>on Feb 14</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Apologies for the late response <a href="https://github.com/scotmatson" target="_blank">@scotmatson</a>! I believe this issues has been fixed with the latest update of the React & Apollo tutorial to Apollo Client 2.0. If you still have questions, please open an issue in the <a href="https://github.com/howtographql/react-apollo" target="_blank"><code>react-apollo</code></a> repo <g-emoji>🙂</g-emoji></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  











        
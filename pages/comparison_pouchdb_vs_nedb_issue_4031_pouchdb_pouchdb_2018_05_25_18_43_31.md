<a href="https://github.com/pouchdb/pouchdb/issues/4031">https://github.com/pouchdb/pouchdb/issues/4031</a><div id="articleHeader"><h1>              Comparison: PouchDB vs. NeDB            #4031    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/Kentoseth" target="_blank">Kentoseth</a>  opened this Issue
        <relative-time>on Jul 7, 2015</relative-time>
        · 5 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          <div>
            




            
<div>
  <div id="issue-93368340">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hello,</p>
<p>Can anyone tell me what is the difference between PouchDB and NeDB?</p>
<p>NeDB can be found here:</p>
<p><a href="https://github.com/louischatriot/nedb/" target="_blank">https://github.com/louischatriot/nedb/</a></p>
<p>Thanks,</p>
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

  




  
<div>
    
  <div id="issuecomment-119181825">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I dont have experience with NeDB so only making a comparison by reading the README, but from a brief look it looks like the main differences are PouchDB does synchronisation between the server and the browser, and that PouchDB was designed with the browser in mind. NeDB looks like it has a slightly more featureful querying probably more along the lines of <a href="http://nolanlawson.github.io/pouchdb-find/" target="_blank">http://nolanlawson.github.io/pouchdb-find/</a></p>
<p>Cheers</p>
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

  




  
<div>
    
  <div id="issuecomment-241243773">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Here is a performance bench comparing NoSQL databases written in pure javascript (finaldb, lowdb, memory, nedb, nosql, pouchdb, tingodb).</p>
<p>Bench source code is available here:<br />
<a href="https://github.com/ezpaarse-project/dbbench" target="_blank">https://github.com/ezpaarse-project/dbbench</a></p>
<p>Here are the results of the bench with nice graphs:<br />
<a href="https://docs.google.com/spreadsheets/d/1oU6YG_7JK6_qBuTNdkXRw6GGiX3vQpzg3f47t84rJAA/edit#gid=1556857962" target="_blank">https://docs.google.com/spreadsheets/d/1oU6YG_7JK6_qBuTNdkXRw6GGiX3vQpzg3f47t84rJAA/edit#gid=1556857962</a></p>
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

  




  
<div>
    
  <div id="issuecomment-241291117">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Interesting stuff! What is "NoSQL" in this case?</p>
<p>BTW PouchDB will definitely have overhead compared to the other databases, because it stores everything in a "revision" model where the history of every document is preserved. (Think of it as git vs just overwriting files.) Hence it tends to have overhead, even for gets/puts.</p>
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

  




  
<div>
    
  <div id="issuecomment-274751509">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>Interesting stuff! What is "NoSQL" in this case?</p>
</blockquote>
<p>Looks like it's <a href="https://github.com/petersirka/nosql" target="_blank">https://github.com/petersirka/nosql</a></p>
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

  




  
<div>
    
  <div id="issuecomment-298198134">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>It's probably worth noting, at the risk of sounding quite rude, that PouchDB is significantly better maintained than NeDB as there's an actual group of people working on it. NeDB is largely a one-man project and as of my comment, the last commit (just under a year ago) was just adding a cute cat pic to the read me asking for donations. That's not to say that he doesn't deserve to be paid for creating a high-quality product, but it's certainly not the same scale of organization as PouchDB, and I think support/community is certainly an important factor to consider when choosing a dependency. At this point it seems that NeDB is mostly kept alive because electron happens to mention it on their site.</p>
<p>(ps I know this issue is pretty old but it does show up on google when searching for pouchdb vs nedb :P)</p>
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










        
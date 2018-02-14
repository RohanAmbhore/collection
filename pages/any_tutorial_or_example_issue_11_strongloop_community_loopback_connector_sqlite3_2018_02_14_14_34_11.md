<a href="https://github.com/strongloop-community/loopback-connector-sqlite3/issues/11">https://github.com/strongloop-community/loopback-connector-sqlite3/issues/11</a><div id="articleHeader"><h1>              Any tutorial or example?            #11    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/kidwm" target="_blank">kidwm</a>  opened this Issue
        <relative-time>on Oct 14, 2015</relative-time>
        · 12 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            





            
  <div id="issue-111388118">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>I've tried to migrate from <a href="https://github.com/Synerzip/loopback-connector-sqlite" target="_blank">https://github.com/Synerzip/loopback-connector-sqlite</a><br />
but don't know how to start with this and find no info on <a href="https://docs.strongloop.com/" target="_blank">https://docs.strongloop.com/</a></p>
<p>and this is my datasources.json:</p>
<div><pre>{
  "db": {
    "name": "db",
    "connector": "memory",
    "file": "db.json"
  },
  "sqlite3": {
    "name": "sqlite3",
    "connector": "sqlite3",
    "file": "test.sqlite3",
    "debug": true
  }
}</pre></div>
      </td>
    </tr>
  </tbody>
</table>


        



    

  

          

          

  
  


  


  


  


  
<div>
    
<div>
  





  
  <div id="issuecomment-148465805">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>In general, we don't document <a href="https://docs.strongloop.com/display/LB/Community+connectors" target="_blank">community connectors</a> such as the SQLite.  Instead, you should refer to the doc in GitHub.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-148592274">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/crandmck" target="_blank">@crandmck</a> So this repo is a community connector, too?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  


  
<div>
    
<div>
  





  
  <div id="issuecomment-148806025">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/kraman" target="_blank">kraman</a>
  

    </strong>

    commented

    <a href="#issuecomment-148806025" target="_blank"><relative-time>on Oct 17, 2015</relative-time></a>


  </h3>
</div>


    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/superkhau" target="_blank">@superkhau</a> I created this connector but havent had time to put it through its paces as yet.</p>
<p><a href="https://github.com/kidwm" target="_blank">@kidwm</a> is something not working? your DS definition seems fine...</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-148843664">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/kraman" target="_blank">@kraman</a> I don't mind helping out with maintaining it if we make it official. Let's get <a href="https://github.com/raymondfeng" target="_blank">@raymondfeng</a>'s input on this. At least we should make it a SL labs project as suggested by <a href="https://github.com/crandmck" target="_blank">@crandmck</a>.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-148883280">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/kraman" target="_blank">@kraman</a> I changed my DS from mongodb to this connector, but it give this error message:</p>
<pre><code>SQLITE_ERROR: no such table: item
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  


  


  
<div>
    
<div>
  





  
  <div id="issuecomment-149413858">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/superkhau" target="_blank">@superkhau</a> No, I didn't. it says <code>Implementing auto-migration is optional for connector.</code><br />
<a href="https://github.com/crandmck" target="_blank">@crandmck</a> So I have to create the schema by myself?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-149607072">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/kraman" target="_blank">kraman</a>
  

    </strong>

    commented

    <a href="#issuecomment-149607072" target="_blank"><relative-time>on Oct 20, 2015</relative-time></a>


  </h3>
</div>


    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/kidwm" target="_blank">@kidwm</a> <code>Implementing auto-migration is optional for connector</code> because DBs like mongo and memory can store arbitrary documents. However, SQL like databases require that the tables be defined and so you need to auto-migrate/auto-update or create tables manually before you can use them.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-149752503">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/kraman" target="_blank">@kraman</a> Thank you for explanation.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  















        


        <div>
              
<div>
  

    
      



      <div>
        
          <div>
  


  
  <div>

    

    

        <p>
    
    
        Attach files by dragging & dropping,
        selecting them, or pasting
        from the clipboard.
    
    
    
    
    
    
    
    
    
  </p>


    
  </div>

  

  


  


          
      




        
      

    
    
  
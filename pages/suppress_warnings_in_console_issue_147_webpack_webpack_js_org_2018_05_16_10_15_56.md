<a href="https://github.com/webpack/webpack.js.org/issues/147">https://github.com/webpack/webpack.js.org/issues/147</a><div id="articleHeader"><h1>              Suppress warnings in console            #147    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/pksjce" target="_blank">pksjce</a>  opened this Issue
        <relative-time>on Sep 7, 2016</relative-time>
        · 7 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-175488246">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/pksjce" target="_blank">pksjce</a>
  

    </strong>

    commented

    <a href="#issue-175488246" target="_blank"><relative-time>on Sep 7, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><em>From <a href="https://github.com/natew" target="_blank">@natew</a> on March 15, 2015 0:18</em></p>
<p>We do dynamic route requires in a library that's used by people, and a lot of them are confused by this messaging:</p>
<pre><code>WARNING in ./app/routes.js
Critical dependencies:
25:16-23 require function is used in a way, in which dependencies cannot be statically extracted
</code></pre>
<p>Beyond some sort of console.log override, is there a way to suppress this warning even if only in the server-side output?</p>
<p><em>Copied from original issue: <a href="https://github.com/webpack/webpack/issues/887" target="_blank">webpack/webpack#887</a></em></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-245262967">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/pksjce" target="_blank">pksjce</a>
  

    </strong>

    commented

    <a href="#issuecomment-245262967" target="_blank"><relative-time>on Sep 7, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><em>From <a href="https://github.com/dnutels" target="_blank">@dnutels</a> on May 26, 2016 6:46</em></p>
<p>Is there no response? At all?</p>
<p>Having the ability to control the tool's logging level/output seems instrumental, yet there is currently no way to show only errors, while skipping (or folding) warnings...</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-245262972">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/pksjce" target="_blank">pksjce</a>
  

    </strong>

    commented

    <a href="#issuecomment-245262972" target="_blank"><relative-time>on Sep 7, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><em>From <a href="https://github.com/jorilallo" target="_blank">@jorilallo</a> on June 5, 2016 1:6</em></p>
<p>I would like to see a way to suppress warnings as well. As per <a href="https://github.com/webpack/webpack.js.org/pull/1617" target="_blank">#1617</a> many popular libraries (e.g. Quill, localforage) come build with Browserify, I don't really see the point of repackaging them and installing random loaders in the process. I would much rather use the original if it works and not see the warning contantly.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-253736058">

    
<div>
  

    
    
      Member
    



  <h3>

    <strong>
      

  <a href="/SpaceK33z" target="_blank">SpaceK33z</a>
  

    </strong>

    commented

    <a href="#issuecomment-253736058" target="_blank"><relative-time>on Oct 14, 2016</relative-time></a>


      
  •


  
    <summary>
      
          edited by skipjack 
      
      
    </summary>

    
  

  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>This has actually been possible for a while, but it just hadn't been documented.</p>
<p>You can find the <a href="https://webpack.js.org/configuration/stats/" target="_blank">documentation here</a>.</p>
<p>tl;dr:</p>
<div><pre>stats: {
  warnings: false
}</pre></div>
<p>in the "root" of your webpack config, OR if you are using webpack-dev-server, in the <code>devServer</code> object.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-286887846">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Is there a way to do this from the CLI?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-339053988">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/SpaceK33z" target="_blank">@SpaceK33z</a> is there a way to only suppress warnings on a certain line?</p>
<p>I have server code that runs from webpack bundle in prod and straight from babel-node in dev, and I want to suppress the dynamic require warning only for this file.</p>
<div><pre>  if (typeof __WEBPACK__ !== 'undefined') {
    // flow-issue(toy-factory-tracker)
    const requireMigration = require.context('../migrations/', false, /\.js$/)
    migrations = requireMigration.keys().map(requireMigration)
  } else {
    migrations = (await promisify(glob)(path.resolve(__dirname, '..', 'migrations', '*.js'))).map(require)
  }</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-350766852">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/SpaceK33z" target="_blank">@SpaceK33z</a> please update documentation reference link, currently the link to the answer 404's</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



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

  

  


  


          
      




        
      

    
    
  
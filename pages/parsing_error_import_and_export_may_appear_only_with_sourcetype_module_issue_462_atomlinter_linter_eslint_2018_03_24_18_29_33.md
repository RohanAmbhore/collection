<a href="https://github.com/AtomLinter/linter-eslint/issues/462">https://github.com/AtomLinter/linter-eslint/issues/462</a><div id="articleHeader"><h1>              Parsing error: 'import' and 'export' may appear only with 'sourceType: module'            #462    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/TitanNano" target="_blank">TitanNano</a>  opened this Issue
        <relative-time>on Mar 1, 2016</relative-time>
        · 3 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-137601549">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I get this error since the most recent update. is it possible there this is missing somewhere in the package?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  


          

          


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-190768439">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Are you using <code>import</code> or <code>export</code>?  If so, what is your config file?  And, how are you using ESLint (installed in your project, globally, or using the version packaged with <code>linter-eslint</code>), and what version of ESLint are you using?</p>
<p>My first guess is that you need to add</p>
<div><pre>{
    "parserOptions": {
        "sourceType": "module",
    }
}</pre></div>
<p>to your config file.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-190770417">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>yes thank you, that solved the issue! <g-emoji>👍</g-emoji></p>
<p>My eslint config is:</p>
<div><pre>{
    "ecmaFeatures": {
        "modules": true,
        "spread" : true,
        "restParams" : true
    },
    "env" : {
        "browser" : true,
        "node" : true,
        "es6" : true
    },
    "rules" : {
        "no-unused-vars" : 2,
        "no-undef" : 2
    },
    "parserOptions": {
        "sourceType": "module"
    }
}</pre></div>
<p>and I'm using the packaged version.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-190797380">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>We recently upgraded the packaged version from ESLint <code>1.x</code> to <code>2.x</code>, which had some breaking changes in the way configurations should be written.  Check out ESLint's <a href="http://eslint.org/docs/user-guide/migrating-to-2.0.0#language-options" target="_blank">migration docs</a> for more details.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    <div>
        <h3 id="ref-issue-294954047">
      
        
      
        <img src="https://avatars0.githubusercontent.com/u/30992774?s=60&v=4" width="16" height="16" alt="@cosmo-naut" />
  <a href="/cosmo-naut" target="_blank">cosmo-naut</a>
  

      referenced this issue
        in <strong>image-js/stroke-width-transform</strong>
      <a href="#ref-issue-294954047" target="_blank">
        <relative-time>on Feb 8</relative-time>
      </a>
    </h3>

  
    
          
      Open
    



    
      <h4>
        <a href="/image-js/stroke-width-transform/issues/2" target="_blank">
          Does it work in browser or just on node?
          #2
        </a>
      </h4>
    

    


  

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

  

  


  


          
      




        
      

    
    
  
<a href="https://github.com/gruntjs/grunt-contrib-watch/issues/294">https://github.com/gruntjs/grunt-contrib-watch/issues/294</a><div id="articleHeader"><h1>              Warning: Task "compass" not found. Use --force to continue.            #294    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/ldexterldesign" target="_blank">ldexterldesign</a>  opened this Issue
        <relative-time>on Feb 25, 2014</relative-time>
        · 13 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-28185570">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          
<p>Is anyone able to help me fix this error? It's quite annoying as my terminal pops everytime I save out my code?</p>
<p><a href="https://camo.githubusercontent.com/b1d77962e18b1e6fd2a66aa0cdd20b7ebef0d838/68747470733a2f2f662e636c6f75642e6769746875622e636f6d2f6173736574732f313731353830392f323234393332382f62393262333536632d396438332d313165332d386437612d3766343635633137663864662e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/b1d77962e18b1e6fd2a66aa0cdd20b7ebef0d838/68747470733a2f2f662e636c6f75642e6769746875622e636f6d2f6173736574732f313731353830392f323234393332382f62393262333536632d396438332d313165332d386437612d3766343635633137663864662e706e67" alt="screen shot 2014-02-24 at 18 43 09" /></div></a></p>
<p><a href="https://camo.githubusercontent.com/42460cf96d33f719e7fccf6488fc48e7dd7f2285/68747470733a2f2f662e636c6f75642e6769746875622e636f6d2f6173736574732f313731353830392f323234393333332f62636332383833382d396438332d313165332d383863362d3437396164333362303834332e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/42460cf96d33f719e7fccf6488fc48e7dd7f2285/68747470733a2f2f662e636c6f75642e6769746875622e636f6d2f6173736574732f313731353830392f323234393333332f62636332383833382d396438332d313165332d383863362d3437396164333362303834332e706e67" alt="screen shot 2014-02-24 at 18 43 18" /></div></a></p>
<p>Yours hopefully,</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-35921042">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Is grunt-contrib-compass installed and loaded?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-35921542">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          
<p>Thanks for reply</p>
<p>Yea, although I suspect I may need to do this: <a href="https://github.com/gruntjs/grunt-contrib-compass#watch" target="_blank">https://github.com/gruntjs/grunt-contrib-compass#watch</a> - I'll look into it and report back if I'm still stuck</p>
<p>Cheers,</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-35922696">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>The <code>watch</code> option there uses <code>compass watch</code> which uses compass's built-in watch. I don't recommend it unless you're only compiling scss files (but then one would just use <code>compass watch</code> directly). It greatly complicates things to save fractions of time and I have no idea why it was implemented in that task.</p>
<p>The warning <code>Task "compass" not found.</code> comes from the task not being installed and loaded. Install with <code>npm i grunt-contrib-compass --save-dev</code> and <code>grunt.loadNpmTasks('grunt-contrib-compass');</code>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-35923313">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/shama" target="_blank">@shama</a></p>
<p>Thanks, I'm only compiling .scss files, yea</p>
<p>I've run those commands and still get the error?</p>
<p>Do you think I should look into <a href="https://github.com/sindresorhus/grunt-concurrent" target="_blank">https://github.com/sindresorhus/grunt-concurrent</a> ?</p>
<p>Cheers,</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-35923482">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/jmeas" target="_blank">@jmeas</a></p>
<p>Ahh, I think I finally understand the purpose of <a href="http://yeoman.io/" target="_blank">http://yeoman.io/</a> :P</p>
<p>Cheers,</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-35923542">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>The yeoman generator contains lots of fun things, most of which you don't need.</p>
<p>Here is a simple example that uses grunt-contrib-watch to compile with compass:</p>
<div><pre>module.exports = function(grunt) {
  grunt.initConfig({
    compass: {
      dist: {
        options: {
          sassDir: 'sass',
          cssDir: 'css',
          environment: 'production',
        },
      },
    },
    watch: {
      css: {
        files: ['sass/*.scss'],
        tasks: ['compass'],
      },
    },
  });
  grunt.loadNpmTasks('grunt-contrib-watch');
  grunt.loadNpmTasks('grunt-contrib-compass');
  grunt.registerTask('default', ['compass']);
};</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-171855336">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I had the same error, which I solved by installing the compass ruby gem: <code>sudo gem install compass</code></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-253205857">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I also had the same problem on Windows.  After installing compass, make sure your path includes the path to ruby.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-280255041">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I am also getting the same Warning: not found: compass Use --force to continue.<br />
<a href="https://cloud.githubusercontent.com/assets/13750636/23011725/9162ad84-f448-11e6-85eb-757d7bf6b43d.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/13750636/23011725/9162ad84-f448-11e6-85eb-757d7bf6b43d.png" alt="image" /></div></a><br />
i tried installing the compass seperately as well, no luck.  Also, what do you mean by "make sure your path includes the path to ruby."?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-283202267">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Your PATH environment variable needs to include the directory where Ruby was installed.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-313024535">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I install yo and yo angular. Here is a angular project, I run "grunt server" &gt; get the same error.</p>
<p><a href="https://user-images.githubusercontent.com/7057383/27853753-990c2f68-6196-11e7-90d7-55dfce423200.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://user-images.githubusercontent.com/7057383/27853753-990c2f68-6196-11e7-90d7-55dfce423200.png" alt="image" /></div></a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  
















        


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

  

  


  


          
      




        
      

    
    
  
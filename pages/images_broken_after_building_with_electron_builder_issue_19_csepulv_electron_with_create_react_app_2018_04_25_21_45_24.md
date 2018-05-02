<a href="https://github.com/csepulv/electron-with-create-react-app/issues/19">https://github.com/csepulv/electron-with-create-react-app/issues/19</a><div id="articleHeader"><h1>              images broken after building with electron-builder            #19    </h1></div>


  <div>
    
    <div>
        <a href="/lduros" target="_blank">lduros</a>  opened this Issue
        <relative-time>on Feb 22</relative-time>
        · 3 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/lduros" target="_blank">lduros</a>
  

    </strong>

    commented

    <a href="#issue-299398381" target="_blank"><relative-time>on Feb 22</relative-time></a>


      
  •


  
    <summary>
      
          edited
      
      
    </summary>

    
  

  </h3>
</div>


    

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Hello,<br />
This may not be directly an issue with this package, but whenever I use electron-builder and build a standalone electron app (dmg file, ...) everything works great for the React piece inside Electron except for the images. I can see them both in my public directory as well as in the build/ directory. However after debugging the standalone electron app, it's attempting to load the image from</p>
<pre><code>file:///my-img-folder/my-img.png
</code></pre>
<p>while it should probably be something like this as a prod electron, I'm assuming:</p>
<pre><code>file:///Applications/m-yapp.app/Contents/Resources/app.asar/build/my-img-folder/my-img.png
</code></pre>
<p>Has anyone seen this behavior as well? I'm thinking a variable in .env might be the solution here, but I'm not sure what it should be.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    
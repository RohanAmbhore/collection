<a href="https://github.com/electron/electron/issues/1769">https://github.com/electron/electron/issues/1769</a><div id="articleHeader"><h1>              Failed to load resource: net::ERR_FILE_NOT_FOUND file:///D:/css/app.css            #1769    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/RinatMullayanov" target="_blank">RinatMullayanov</a>  opened this Issue
        <relative-time>on May 25, 2015</relative-time>
        · 14 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          <div>
            




            
<div>
  <div id="issue-80415892">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I have such a structure in the application:<br />
<a href="https://cloud.githubusercontent.com/assets/7579698/7792911/fb0c2a54-02d1-11e5-9656-ceee18a79006.PNG" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/7579698/7792911/fb0c2a54-02d1-11e5-9656-ceee18a79006.PNG" alt="file struct" /></div></a></p>
<p>I write in head my index.html:</p>
<pre><code>&lt;link rel="stylesheet" href="css/app.css"/&gt;
</code></pre>
<p>run electron and get error:</p>
<p>
Failed to load resource: net::ERR_FILE_NOT_FOUND file:///D:/css/app.css<br />
Please everyone, tell me, how should I set the path to the file?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

          </div>

          

  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-105276513">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/shama" target="_blank">shama</a>
  

    </strong>

    commented

    <a href="#issuecomment-105276513" target="_blank"><relative-time>on May 26, 2015</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Try this as an alternative way to get around this path issue:</p>
<div><pre>&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;script&gt;
    var link = document.createElement('link')
    link.setAttribute('rel', 'stylesheet')
    link.setAttribute('href', require('path').join(__dirname, 'css', 'app.css'))
    document.head.appendChild(link)
    &lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt;</pre></div>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-105276916">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/shama" target="_blank">@shama</a> Thanks for snippet.<br />
I get an error because the use &lt;base href="/"&gt;, without this error does not occur.<br />
Sample work <a href="https://github.com/RinatMullayanov/angular-boilerplate" target="_blank">https://github.com/RinatMullayanov/angular-boilerplate</a> branch <strong>electron</strong>.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-186587867">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Have the same issue too. Electron tries to load resources from C:/ , relative paths not working.<br />
Setting full path is not an option, files will not be loading if we will place application on another path.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-209412970">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I have the same issue getting some font</p>
<p>I have added this to my CSS<br />
<code>@import url(https://fonts.googleapis.com/css?family=Open+Sans:400,700);</code><br />
I have even tried adding this to my html:<br />
<code>&lt;link rel="stylesheet" type="text/css" href="//fonts.googleapis.com/css?family=Open+Sans" /&gt;</code></p>
<p>I have also tried:</p>
<p><code>&lt;link rel="stylesheet" type="text/css" href="http//fonts.googleapis.com/css?family=Open+Sans" /&gt;</code></p>
<p><code>&lt;link rel="stylesheet" type="text/css" href="https//fonts.googleapis.com/css?family=Open+Sans" /&gt;</code></p>
<p>but I get this error:<br />
<code>Failed to load resource: net::ERR_CONNECTION_REFUSED</code></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-257424968">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>If this occur when having <code>&lt;base href="/"&gt;</code> in the index.html, just replace it by <code>&lt;base href="./"&gt;</code>.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-260261158">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/Myrga" target="_blank">@Myrga</a> you're a life save. I've been looking for an answer for 5 days now, no doc on this, until I came across this old post. Thanks a lot</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-272069773">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>ps: if you came here and are using create-react-app, try putting <code>"homepage": "./",</code> in your package.json. (Although apparently this is not currently supported so you might have other issues with fonts and such, which might require moving those assets to your /public folder)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-280696920">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>thank you so much</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-280716990">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/BesatZardosht" target="_blank">@BesatZardosht</a> You've got a typo in your URL:</p>
<pre><code>&lt;link rel="stylesheet" type="text/css" href="https//fonts.googleapis.com/css?family=Open+Sans" /&gt;
</code></pre>
<p>should be:</p>
<pre><code>&lt;link rel="stylesheet" type="text/css" href="https://fonts.googleapis.com/css?family=Open+Sans" /&gt;
</code></pre>
<p>(note the <code>:</code>)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
      <div>
        <h3 id="ref-issue-184448136">
      
        
      
        
  <a href="/vanchisel" target="_blank">vanchisel</a>
  

      referenced this issue
        in <strong>JonnyBGod/angular2-webpack-advance-starter</strong>
      <a href="#ref-issue-184448136" target="_blank">
        <relative-time>on Mar 16, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Open
    



    
      <h4>
        <a href="/JonnyBGod/angular2-webpack-advance-starter/issues/8" target="_blank">
          Issue getting Dev environment up
          #8
        </a>
      </h4>
    

    


  

</div>


</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-309228698">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>In case you are here with the same problem using <code>Webpack 2.x</code>, <code>React</code> and/or <code>Redux</code>, there is a chance that this would solve your problem:</p>
<blockquote>
<p>Search your project directory for "publicPath" and change its value from <code>/</code> to <code>./</code><br />
with all the different available boilerplates this setting may be found in different locations, In my case using <code>redux-cli</code> which uses <code>redux-starter-kit</code>, it was in the <code>project.config.js</code>:</p>
</blockquote>
<div><pre>publicPath: './',</pre></div>
<p>Also if you are building for <code>Electron</code> you may need to add/modify the Webpack <code>target</code> property.<br />
Stay Happy!! <g-emoji>😄</g-emoji></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-318436942">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Had same problem, Myrga's solution worked. I think  must consider / as global root directory for the PC when using file protocol. While "./" works as a relative reference to the current folder. Just a guess, when using http:// protocol on port 4200 (Where I serve my Angular4 app) everything works with "/". For file protocol have to use "./"</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-320263563">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Decided to remake my application in React. Once I added file-loader to my project, I started getting this issue again. changing the publicPath property in webpack.config.js to a relative path (for me ./app/ rather than /app/) fixed the problem.</p>
<p>P.S. seems that the dev server hates this. If you make this change and want to run a webpack dev server this change will confuse it. You'll need to switch back and forth as you go from working directly in electron and working on dev server (The reason i do this is to do css work, I find the dev server faster and more stable)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-323900576">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>You can save the html file as "save as web page" then try to open in chrome.<br />
This worked for me.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>










        
<a href="https://github.com/webpack-contrib/eslint-loader/issues/129">https://github.com/webpack-contrib/eslint-loader/issues/129</a><div id="articleHeader"><h1>              eslint-loader doesn't check if additional .eslintrc exists            #129    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/hinok" target="_blank">hinok</a>  opened this Issue
        <relative-time>on Dec 4, 2016</relative-time>
        · 9 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-193309525">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/hinok" target="_blank">hinok</a>
  

    </strong>

    commented

    <a href="#issue-193309525" target="_blank"><relative-time>on Dec 4, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><code>eslint</code> gives ability to overrides rules for specific folders, for example:</p>
<pre><code>- app/
- app/index.js
- app/.eslintrc // (a) Overrides rules from (b)
- index.js
- .eslintrc // (b)
</code></pre>
<p>In my project when I use <code>eslint</code> by <code>eslint-cli</code> I don't get any errors but when I develop and use <code>webpack</code> + <code>eslint-loader</code>, then I get errors.</p>
<pre><code>ERROR in ./src/components/Icons/IconSearch.js

/a/b/c/e/f/g/h/src/components/Icons/IconSearch.js
  8:1  error  Line 8 exceeds the maximum line length of 100  max-len

✖ 1 problem (1 error, 0 warnings)

 @ ./src/views/home/index.js 13:0-61
 @ ./src/app/routes.js
 @ ./src/app/index.js
 @ ./src/index.js
 @ multi app
</code></pre>
<p>I don't want append</p>
<pre><code>/* eslint-disable max-len */
</code></pre>
<p>in each file that contains SVG because I have a lot of icons...<br />
Is there any way to instrument this loader to check if additional <code>.eslintrc</code> files exists?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-264898519">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/wrakky" target="_blank">wrakky</a>
  

    </strong>

    commented

    <a href="#issuecomment-264898519" target="_blank"><relative-time>on Dec 6, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>eslint-loader doesn't load the eslintrc files - it uses an instance of eslint.CLIEngine which the eslint-cli also uses and that should resolve the correct rules for each file itself. I've just tried nested .eslintrc files and it seemed to be working correctly for me.</p>
<p>Do you have the eslint-loader cache option enabled? If so then you may be experiencing the problem described in <a href="https://github.com/webpack-contrib/eslint-loader/issues/124" target="_blank">#124</a> where if you change the eslint rules the previously cached results are still being output. Try setting cache to false and if that fixes the issue you can delete <code>node_modules/.cache/eslint-loader</code> to reset the cache properly.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-264917847">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/hinok" target="_blank">hinok</a>
  

    </strong>

    commented

    <a href="#issuecomment-264917847" target="_blank"><relative-time>on Dec 6, 2016</relative-time></a>


      
  •


  
    <summary>
      
          edited
      
      
    </summary>

    
  

  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>Do you have the eslint-loader cache option enabled?</p>
</blockquote>
<p>Yes. If I disable cache, it doesn't change anything.<br />
I'm using webpack <code>2.1.0-beta.27</code> with this configuration:</p>
<div><pre>{
    module: {
      loaders: [
        {
          enforce: 'pre',
          test: /\.js$/,
          loader: 'eslint-loader',
          exclude: /node_modules/,
        },
      ],
    },
    plugins: [
      new webpack.LoaderOptionsPlugin({
        test: /\.js$/,
        options: {
          eslint: {
            configFile: utils.root('.eslintrc'), // this is my helper for resolving paths
            cache: false,
          }
        },
      }),
    ],
  }</pre></div>
<p>I'm using also <code>eslint-config-airbnb</code> but this probably is not related. I will try reproduce this issue and create an example repository that could show this bug.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-265007184">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/hinok" target="_blank">hinok</a>
  

    </strong>

    commented

    <a href="#issuecomment-265007184" target="_blank"><relative-time>on Dec 6, 2016</relative-time></a>


      
  •


  
    <summary>
      
          edited
      
      
    </summary>

    
  

  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><strong>Update: If I remove <code>configFile</code> property, it works - so weird</strong></p>
<hr />
<p><a href="https://github.com/wrakky" target="_blank">@wrakky</a> <a href="https://github.com/hinok/webpack2-eslint-loader" target="_blank">https://github.com/hinok/webpack2-eslint-loader</a></p>
<div><pre>npm install

# Run eslint by eslint-cli
npm run lint

# Run webpack2 + eslint-loader
npm start</pre></div>
<p>Repository contains <code>demo.gif</code> added in README.md that shows recorded behaviour.<br />
Look at additional <code>.eslintrc</code> inside <code>subfolder</code>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-265019260">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/wrakky" target="_blank">wrakky</a>
  

    </strong>

    commented

    <a href="#issuecomment-265019260" target="_blank"><relative-time>on Dec 6, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>If you use the <code>-c</code> option in the <code>npm run lint</code> command (<code>eslint . --ext .js -c .eslintrc</code>) which is the equivalent to the eslint-loader <code>configFile</code> option you get the same output from both eslint cli and weback.</p>
<p>The file passed to the<code>configFile</code> option is not extendable which is why you are having the problem. You probably want to either remove the option if possible or maybe the <code>baseConfig</code> option will work for you instead.</p>
<p>Either way this isn't an eslint-loader issue. Hope that helps!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-265087023">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/hinok" target="_blank">hinok</a>
  

    </strong>

    commented

    <a href="#issuecomment-265087023" target="_blank"><relative-time>on Dec 6, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Yep, that's it. Sorry for the confussion! When I found yesterday that removing configFile solved the problem, I was pretty sure that let's say it's the eslint's fault not eslint-loader - if we could name it as a fault.</p>
<p>I close this issue and maybe it's worth to update README? I could add PR if you want.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-265089255">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>PR welcome!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-265282470">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/hinok" target="_blank">hinok</a>
  

    </strong>

    commented

    <a href="#issuecomment-265282470" target="_blank"><relative-time>on Dec 7, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Added PR <a href="https://github.com/webpack-contrib/eslint-loader/pull/130" target="_blank">MoOx#130</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-379259401">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I am having a similar problem, can you post your actual config files which resolved your issue?</p>
<p>configs:</p>
<ul>
<li>webpack</li>
<li>package.json</li>
</ul>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-379268231">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          
<p><a href="https://github.com/webpack-contrib/eslint-loader/pull/183/files" target="_blank">https://github.com/webpack-contrib/eslint-loader/pull/183/files</a></p>
<p>Use eslintPath with the <code>CLIEngine class wrapper</code> .</p>
<p>Seems like defining CLIEngine is overkill. Why is this not wrapped within the code/eslint-loader library itself?</p>
<pre><code>class CLIEngine {
  executeOnText() {
    return require(eslintPath);
  }
}
</code></pre>
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

  

  


  


          
      




        
      

    
    
  
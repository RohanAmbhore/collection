<a href="https://github.com/webpack-contrib/css-loader/issues/447">https://github.com/webpack-contrib/css-loader/issues/447</a><div id="articleHeader"><h1>              Can't resolve 'fs' when bundle with webpack            #447    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/Alex-Sokolov" target="_blank">Alex-Sokolov</a>  opened this Issue
        <relative-time>on Mar 10, 2017</relative-time>
        · 54 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-213255868">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><strong>Do you want to request a <em>feature</em> or report a <em>bug</em>?</strong><br />
Bug</p>
<p><strong>What is the current behavior?</strong><br />
Webpack finish bundle without errors with css-loader <code>0.26.4</code>.<br />
After update to <code>0.27.0</code> webpacking finished with error:</p>
<pre><code>ERROR in ./~/convert-source-map/index.js
Module not found: Error: Can't resolve 'fs' in 'C:\Projects\project_name\node_modules\convert-source-map'
 @ ./~/convert-source-map/index.js 2:9-22
 @ ./~/css-loader/lib/css-base.js
</code></pre>
<p><strong>If the current behavior is a bug, please provide the steps to reproduce.</strong></p>
<ol>
<li>Update css-loader from <code>0.26.4</code> to <code>0.27.0</code> version</li>
<li>Run webpack to build</li>
</ol>
<p><strong>What is the expected behavior?</strong><br />
Works without error</p>
<p><strong>Please mention other relevant information such as your webpack version, Node.js version and Operating System.</strong><br />
Windows 8.1<br />
Node.js 7.7.2<br />
Webpack 2.2.1</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  


          

          

  


  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-285595531">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Same for me, had to rollback that update</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-285598881">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Adding</p>
<div><pre>node: {
  fs: 'empty'
}</pre></div>
<p>to webpack config file and the error is gone. Not sure how it works, It seems like webpack did some thing with <code>fs</code> module in <code>web</code> target.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-285600014">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>add the following to your Webpack config:</p>
<div><pre>node: {
   fs: "empty"
}</pre></div>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-285600188">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/bebraw" target="_blank">bebraw</a>
  

    </strong>

    commented

    <a href="#issuecomment-285600188" target="_blank"><relative-time>on Mar 10, 2017</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>The issue has been acknowledged and we are in process of figuring out a good fix. No need for "me too"s. Please add a thumbs up on the original issue if you want to do that. <g-emoji>👍</g-emoji></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-285602896">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Did you can to unpublish this version? It will keep calm to all of us</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-285603267">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/PredokMiF" target="_blank">@PredokMiF</a>  You don't unpublish anything, ever.</p>
<p>The workaround is sufficient and the bug is actually in webpack, related to <code>fs</code> in the web target.</p>
<p><strong>WORKAROUND</strong> thanks to <a href="https://github.com/hdnha11" target="_blank">@hdnha11</a> / <a href="https://github.com/mehdivk" target="_blank">@mehdivk</a></p>
<pre><code>node: {
  fs: 'empty'
}
</code></pre>
<p>If using this workaround isn't viable, version lock to the previous minor version.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-286086224">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/bebraw" target="_blank">@bebraw</a> With your fix of this issue, I have a <code>Uncaught ReferenceError: Buffer is not defined</code> in the <code>lib/convert-source-map.js</code> file, in the browser.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-286090441">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/bebraw" target="_blank">bebraw</a>
  

    </strong>

    commented

    <a href="#issuecomment-286090441" target="_blank"><relative-time>on Mar 13, 2017</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/fklingler" target="_blank">@fklingler</a> I have a proposed fix for that at <a href="https://github.com/webpack-contrib/css-loader/pull/453" target="_blank">#453</a> . Still waiting for some approvals before I can push it. Feel free to give that a go and let me know how it goes.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-306139610">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I came across the same error. I am starting off with JS (with vuejs) and I would like to understand what this does?</p>
<p>I got this error when using the "fetch" library from npm. At first I got the same error but with other packages (<code>net</code> and <code>dns</code>). My first thought was that those are missing dependencies. After running <code>npm install net</code> and <code>npm install dns</code>, those errors were replaced with <code>dgram</code> and <code>fs</code>. The latter one prompted me to hit Google and landed on this issue.</p>
<p>I now added two sections in my webpack config for both <code>fs</code> and <code>dgram</code>, and now the errors are gone.</p>
<p>But I don't know what this entails. Will my compiled code still work? Even if these sections are configured as being <code>empty</code>? What does it actually do?</p>
<p>Also, is this the right place to ask this? Or should it be rather targeted at vuejs?</p>
<p><strong>nb:</strong> I would like to give a bit more insight about my running environment but as I'm still getting my feet wet, I don't know which commands are the best to represent a snapshot of my dev-environment. If you need some additional output, let me know which commands to run.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-306158909">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/bebraw" target="_blank">bebraw</a>
  

    </strong>

    commented

    <a href="#issuecomment-306158909" target="_blank"><relative-time>on Jun 5, 2017</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/exhuma" target="_blank">@exhuma</a> See <a href="https://webpack.js.org/configuration/node/" target="_blank">the related page on documentation</a>. That describes the default behavior. You can also find possible overrides there. I hope this helps.</p>
<blockquote>
<p>Also, is this the right place to ask this? Or should it be rather targeted at vuejs?</p>
</blockquote>
<p>Stack Overflow might be better for this type of questions.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
      <div>
        <h3 id="ref-issue-191961198">
      
        
      
        <img src="https://avatars3.githubusercontent.com/u/2854616?s=60&v=4" width="16" height="16" alt="@sebelga" />
  <a href="/sebelga" target="_blank">sebelga</a>
  

      referenced this issue
        in <strong>react-boilerplate/react-boilerplate</strong>
      <a href="#ref-issue-191961198" target="_blank">
        <relative-time>on Jun 13, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/react-boilerplate/react-boilerplate/issues/1278" target="_blank">
          Module not found: Error: Can't resolve 'fs'
          #1278
        </a>
      </h4>
    

    

  
    1 of 2 tasks complete
    
      
    
  

  

</div>




  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-308918678">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>just wanted to add that I fixed this by the answer in <a href="https://github.com/josephsavona/valuable/issues/9" target="_blank">josephsavona/valuable#9</a> about setting <code>target: 'node'</code></p>
<p>This explains more: <a href="http://jlongster.com/Backend-Apps-with-Webpack--Part-I" target="_blank">http://jlongster.com/Backend-Apps-with-Webpack--Part-I</a></p>
<blockquote>
<p>The target: 'node' option tells webpack not to touch any built-in modules like fs or path.</p>
</blockquote>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-316254695">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Hi - when I did<br />
<code>target: 'node'</code>,</p>
<p>the error went away. Then I got<br />
<code>global not defined</code>,</p>
<p>so I fixed it with<br />
<code>'global': {},</code> in <code>webpack.definePlugin({...})</code></p>
<p>Then I got a GetEnv error saying SERVER_HOST not defined... but it is... so there's a slew of errors that I'm swimming in - I hope someone can take a look at my boilerplate and give me hand? Thank you!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
      <div>
        <h3 id="ref-issue-244335812">
      
        
      
        <img src="https://avatars2.githubusercontent.com/u/1344142?s=60&v=4" width="16" height="16" alt="@saniko" />
  <a href="/saniko" target="_blank">saniko</a>
  

      referenced this issue
        in <strong>ctrlplusb/react-universally</strong>
      <a href="#ref-issue-244335812" target="_blank">
        <relative-time>on Jul 20, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/ctrlplusb/react-universally/issues/474" target="_blank">
          Error: Can't resolve 'fs'
          #474
        </a>
      </h4>
    

    


  

</div>




  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-318793467">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I fixed the problem by changing webpack.config.js:</p>
<p>...<br />
var config = Encore.getWebpackConfig();<br />
config.node = { fs: 'empty' };<br />
module.exports = config;</p>
<p>and:<br />
yarn add --dev file system</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-325993939">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Someone please fix this issue. Non of the mentioned answer could fix it for me</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-327427372">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/samayo" target="_blank">@samayo</a> I'm not sure what I got could help you.</p>
<p>I fix this error by installing <code>node-sass</code> into <code>devDenpendency</code>, if I install <code>node-sass</code> into <code>denpendency</code>, I will get this error, I'm not sure you use <code>node-sass</code> or not, you can check some packages in <code>denpendency</code> and <code>devDenpendency</code></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
      <div>
  <h3 id="ref-commit-0782881">
    
      
    
    
  <a href="/thorncp" target="_blank">thorncp</a> 


      added a commit
        to davidimoore/rails_4_react_sandbox
      that referenced
      this issue

    <a href="#ref-commit-0782881" target="_blank">
      <relative-time>on Sep 7, 2017</relative-time>
    </a>
  </h3>

  
</div>

  <div>
        <h3 id="ref-pullrequest-255701999">
      
        
      
        <img src="https://avatars2.githubusercontent.com/u/72176?s=60&v=4" width="16" height="16" alt="@thorncp" />
  <a href="/thorncp" target="_blank">thorncp</a>
  

      referenced this issue
        in <strong>davidimoore/rails_4_react_sandbox</strong>
      <a href="#ref-pullrequest-255701999" target="_blank">
        <relative-time>on Sep 7, 2017</relative-time>
      </a>
    </h3>

  
    
        
      Merged
    



    
      <h4>
        <a href="/davidimoore/rails_4_react_sandbox/pull/4" target="_blank">
          Handle Can't resolve 'fs' error
          #4
        </a>
      </h4>
    

    


  

</div>

  

  <div>
        <h3 id="ref-pullrequest-260413568">
      
        
      
        <img src="https://avatars1.githubusercontent.com/u/1566880?s=60&v=4" width="16" height="16" alt="@adlius" />
  <a href="/adlius" target="_blank">adlius</a>
  

      referenced this issue
        in <strong>CenterForOpenScience/osf.io</strong>
      <a href="#ref-pullrequest-260413568" target="_blank">
        <relative-time>on Sep 26, 2017</relative-time>
      </a>
    </h3>

  
    
        
      Merged
    



    
      <h4>
        <a href="/CenterForOpenScience/osf.io/pull/7733" target="_blank">
          [OSF-8011] Markdown image resize
          #7733
        </a>
      </h4>
    

    


  

</div>




  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-333643814">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>How should I go about solving this issue when importing an npm module that uses Webpack (i.e., when importing an npm module that imports a package that yields this problem)?</p>
<p>To add some clarity: say I've create two npm modules, both using Webpack. Let's call them module A and module B.</p>
<p>Module A imports <code>require</code>, which yields this error. Thus, in <code>webpack.config.js</code> of module A, I add:</p>
<pre><code>  node: {
    console: false,
    fs: 'empty',
    net: 'empty',
    tls: 'empty'
  }
</code></pre>
<p>Module B then imports module A. However, even though I've added the above code in module A, the error still comes up when I try to build module B.</p>
<p>Does anyone know how to solve this problem <strong>without adding the above code to module B as well</strong> (i.e., modifying only module A)?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  


</div>

</div>

  



  

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-352286764">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Why is this issue closed? I just spent the last two days racking my brains, until I finally stumbled upon this bug report with a lucky combination of search keywords. The workaround seems like a really bad one. Will we see a fix?</p>
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
    
  <div id="issuecomment-352324111">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I get an error like this:</p>
<p><code>TypeError: fs.readFileSync is not a function</code></p>
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
    
  <div id="issuecomment-352366627">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/vgjenks" target="_blank">@vgjenks</a> <a href="https://github.com/tjvg91" target="_blank">@tjvg91</a> please read <strong>above</strong>. Need minimum reproducible test repo. Thanks!</p>
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
    
  <div id="issuecomment-353994469">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Super annoying! None of the fixes work for me. And there's nothing to reproduce. just <code>require("fs")</code> causes the problem.</p>
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
    
  <div id="issuecomment-354216982">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <pre><code>  node: {
    fs: 'empty'
  }
</code></pre>
<p>The work-around allows us to run the webpack, but if our application needs to use FS for any reason, like write to file, the work-around is now a problem as FS no longer exists.</p>
<blockquote>
<p>fs.writeFile is not a function</p>
</blockquote>
<p>Does anyone have a different solution?</p>
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
    
  <div id="issuecomment-355326149">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/Percapio" target="_blank">@Percapio</a>  add this</p>
<pre><code>target: 'node'
</code></pre>
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
    
  <div id="issuecomment-355380878">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/mrkaspa" target="_blank">@mrkaspa</a> not only did your suggestion resolve my fs issue, I had other modules as well and it resolved all of them ('net' was one)</p>
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
    
  <div id="issuecomment-356175589">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>None of these suggestions have worked for my env. How is this not fixed?</p>
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
    
  <div id="issuecomment-356220511">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Installing that package and saving solves problem, for example:<br />
<code>npm install fs --save</code></p>
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
        <h3 id="ref-issue-288093861">
      
        
      
        <img src="https://avatars2.githubusercontent.com/u/1881059?s=60&v=4" width="16" height="16" alt="@leotm" />
  <a href="/leotm" target="_blank">leotm</a>
  

      referenced this issue
        in <strong>uphold/uk-modulus-checking</strong>
      <a href="#ref-issue-288093861" target="_blank">
        <relative-time>on Jan 12</relative-time>
      </a>
    </h3>

  
    
          
      Open
    



    
      <h4>
        <a href="/uphold/uk-modulus-checking/issues/12" target="_blank">
          Can't resolve 'fs'
          #12
        </a>
      </h4>
    

    


  

</div>


</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-357234398">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><code>npm install fs --save</code> doesn't seem to have any affect in my case.<br />
<a href="https://webpack.js.org/configuration/target/" target="_blank">https://webpack.js.org/configuration/target/</a> hints I should be using <code>target: 'web'</code>.<br />
This gives me <em>Can't resolve 'fs'</em>.<br />
<code>node: { fs: "empty", }</code> gives me <em>_fs2.default.readFileSync is not a function</em>.<br />
Changing to <code>target: 'node'</code> gives me <em>require is not defined</em> (people also mentioning this in comments <a href="https://stackoverflow.com/a/39249719/1998086" target="_blank">here</a>.</p>
<p>Oops, I've been trying to run a node module in the browser to do some validation.<br />
Of course, the browser doesn't have file system access.<br />
In the end I just ran <code>build</code> on the node module and <em>import</em> or <em>require</em> the <code>/dist</code> <em>.js</em> file</p>
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
    
  <div id="issuecomment-360007311">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <h4>I got it to work when I added the following element inside <code>module.exports</code> in my <em>webpack.config</em> file</h4>
<div><pre>node: {
        fs: 'empty'
},</pre></div>
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
  <h3 id="ref-commit-10ae018">
    
      
    
    
  <a href="/johnnyoshika" target="_blank">johnnyoshika</a> 


      added a commit
        to johnnyoshika/jellypic-dashboard-from-redux-starter-kit
      that referenced
      this issue

    <a href="#ref-commit-10ae018" target="_blank">
      <relative-time>on Jan 27</relative-time>
    </a>
  </h3>

  
</div>

  <div>
  <h3 id="ref-commit-40379cf">
    
      
    
    
  <a href="/johnnyoshika" target="_blank">johnnyoshika</a> 


      added a commit
        to johnnyoshika/jellypic-dashboard-from-redux-starter-kit
      that referenced
      this issue

    <a href="#ref-commit-40379cf" target="_blank">
      <relative-time>on Jan 27</relative-time>
    </a>
  </h3>

  
</div>

  <div>
  <h3 id="ref-commit-127ebae">
    
      
    
    
  <a href="/johnnyoshika" target="_blank">johnnyoshika</a> 


      added a commit
        to johnnyoshika/jellypic-dashboard-from-redux-starter-kit
      that referenced
      this issue

    <a href="#ref-commit-127ebae" target="_blank">
      <relative-time>on Jan 27</relative-time>
    </a>
  </h3>

  
</div>

  

  

  <div>
        <h3 id="ref-issue-287791456">
      
        
      
        <img src="https://avatars3.githubusercontent.com/u/11574195?s=60&v=4" width="16" height="16" alt="@Spatlani" />
  <a href="/Spatlani" target="_blank">Spatlani</a>
  

      referenced this issue
        in <strong>EducationLink/vue-tel-input</strong>
      <a href="#ref-issue-287791456" target="_blank">
        <relative-time>on Feb 12</relative-time>
      </a>
    </h3>

  
    
          
      Open
    



    
      <h4>
        <a href="/EducationLink/vue-tel-input/issues/5" target="_blank">
          Cant resolve fs & net.
          #5
        </a>
      </h4>
    

    


  

</div>

  


</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-366445981">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>There is a better solution available <a href="https://stackoverflow.com/a/42425214/2557900" target="_blank">hee</a></p>
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
    
  <div id="issuecomment-366446549">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Maybe it will help some of you.<br />
I was having this issue because an emscripten built dependency was used by my project.<br />
Emscripten js output contains require(‘fs’).</p>
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
    
  <div id="issuecomment-368196290">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>If any of you is using NextJS to fix this problem, you can add:</p>
<pre><code>module.exports = {
  webpack: (config, { buildId, dev, isServer, defaultLoaders }) =&gt; {
    config.node = {
      fs: 'empty'
    }
    return config
  },
}
</code></pre>
<p>To your next.config.js file</p>
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
    
  <div id="issuecomment-368345121">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/J-Gallo" target="_blank">@J-Gallo</a> Thank you so much!</p>
<p><code>next.config.js</code></p>
<div><pre>module.exports = {
  webpack: (config, { buildId, dev, isServer, defaultLoaders }) =&gt; {
    config.node = {
      fs: 'empty',
      module: "empty",
    };
    return config;
  },
};</pre></div>
<p>I just had to add the <code>module: "empty",</code> as well.</p>
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
    
  <div id="issuecomment-374567043">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>For those of you using Nuxt.js for Vue.s server-side rendering, webpack can be extended as follows:</p>
<blockquote>
<p><strong>nuxt.config.js</strong></p>
</blockquote>
<div><pre>module.exports = {
  ...
  build: {
    extend (config, { isDev, isClient }) {
      if (isDev && isClient) {
        ...
        config.node = {
          fs: 'empty'
        }
      }
    }
  }
}</pre></div>
<p>However, if you need <code>fs</code> for any reason, you may run into the same issues as mentioned above and require further workarounds</p>
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
    
  <div id="issuecomment-377071626">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I solved this by just requiring the fs module in my electron window:<br />
<code>const fs = window.require('fs');</code><br />
Looks like something in ipcRenderer tries to use it without defining it? Once it was defined all my errors went away.</p>
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
        <h3 id="ref-issue-308644715">
      
        
      
        <img src="https://avatars3.githubusercontent.com/u/12032248?s=60&v=4" width="16" height="16" alt="@adi518" />
  <a href="/adi518" target="_blank">adi518</a>
  

      referenced this issue
        in <strong>vue-styleguidist/vue-docgen-api</strong>
      <a href="#ref-issue-308644715" target="_blank">
        <relative-time>19 hours ago</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/vue-styleguidist/vue-docgen-api/issues/26" target="_blank">
          "Dependencies not found"
          #26
        </a>
      </h4>
    

    


  

</div>


</div>








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

  

  


  
</div>

          
      </div>

</div>


        </div>
      </div>

    </div>
    
  
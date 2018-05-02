<a href="https://github.com/webpack-contrib/css-loader/issues/38">https://github.com/webpack-contrib/css-loader/issues/38</a><div id="articleHeader"><h1>              css-loader parse fail on @font-face            #38    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/mattybow" target="_blank">mattybow</a>  opened this Issue
        <relative-time>on Jan 31, 2015</relative-time>
        · 40 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-56094366">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I get this error when webpack tries to run:</p>
<pre><code>ERROR in ./bower_components/bootstrap/dist/fonts/glyphicons-halflings-regular.eot
Module parse failed: 
./bower_components/bootstrap/dist/fonts/glyphicons-halflings-regular.eot Line 1: Unexpected token ILLEGAL
You may need an appropriate loader to handle this file type.
(Source code omitted for this binary file)
 @ ./~/css-loader?importLoaders=1!./bower_components/bootstrap/dist/css/bootstrap.css 2:4480-4532 2:4551-4603
</code></pre>
<p>Here's my configuration</p>
<pre><code> module: {
    loaders: [
      // Pass *.jsx files through jsx-loader transform
      { test: /\.js$/, loaders: ['react-hot','jsx?harmony'] },

      { test: /\.css$/, loader: "style-loader!css-loader?importLoaders=1" }
    ]
  }
</code></pre>
<p>Is it something in my config that's wrong or missing something?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  


          

          

  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-72287584">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I needed to add url-loader to my config</p>
<pre><code>{ test: /\.(png|woff|woff2|eot|ttf|svg)$/, loader: 'url-loader?limit=100000' }
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-152411328">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Thanks for the answer <a href="https://github.com/mattybow" target="_blank">@mattybow</a>, it seems better to add a suffix regex to fit more general cases, the following configuration works for me:<br />
{ test: /.(png|woff(2)?|eot|ttf|svg)(?[a-z0-9=.]+)?$/, loader: 'url-loader?limit=100000' }</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
      <div>
        <h3 id="ref-pullrequest-116059277">
      
        
      
        <img src="https://avatars3.githubusercontent.com/u/41547?s=60&v=4" width="16" height="16" alt="@n1k0" />
  <a href="/n1k0" target="_blank">n1k0</a>
  

      referenced this issue
        in <strong>react-cosmos/react-cosmos</strong>
      <a href="#ref-pullrequest-116059277" target="_blank">
        <relative-time>on Nov 10, 2015</relative-time>
      </a>
    </h3>

  
    
        
      Merged
    



    
      <h4>
        <a href="/react-cosmos/react-cosmos/pull/172" target="_blank">
          Added support for url-loader.
          #172
        </a>
      </h4>
    

    


  

</div>




  


  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-184916012">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I am struggling to add new fonts to my styles. My webpack.config test for fonts is:</p>
<pre><code>...
{
  test: /\.ttf$/,
  loaders: ['url?limit=100000']
},
...
</code></pre>
<p>I am unsure of the syntax that I should use to load the font file, and I think that this is the problem. Could anyone share with me a code snippet to illustrate how they have successfully loaded a font? Right now I have the following in my <code>main.scss</code>:</p>
<pre><code>@font-face {
  font-family: testFont;
  src: url("../assets/fonts/Proxima_Nova_Regular.ttf");
  font-weight: bold;
}
</code></pre>
<p>But this isn't working for me. Any help would be greatly appreciated!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-189375589">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/wpcarro" target="_blank">@wpcarro</a> which <code>css-loader</code> version are you using ?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-189378200">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/cusspvz" target="_blank">@cusspvz</a>:</p>
<p>From the package.json</p>
<pre><code>"css-loader": "^0.23.1",
</code></pre>
<p>We ended up getting the fonts to load using <code>file-loader</code> in lieu of <code>url-loader</code>. To be completely honest, I'm unsure of the nuances between the two loaders. I also ended up switching the order in which the loaders were applied, which I think ultimately did the trick.</p>
<p>When I was experiencing trouble, Webpack was processing the font files before processing the Sass files. I rearranged this so that the order went:</p>
<pre><code>json --&gt; photos --&gt; Sass --&gt; audio --&gt; fonts --&gt; JS
</code></pre>
<p>Either way, the process was a little bit similar to shooting in the dark, but it's working now.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-189382377">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <blockquote>
<p>To be completely honest, I'm unsure of the nuances between the two loaders.</p>
</blockquote>
<p><code>file-loader</code> grabs the file and handle its writing on build (you could specify saved path/name.extension, and other nice features it has).<br />
<code>url-loader</code> tries to load up file data inline by using <code>blob</code> style url loading, but it would do it only if a file size is under the <code>limit</code>specified, otherwise it will fallback and use <code>file-loader</code> instead.</p>
<p>URL loader is indicated to be used on <code>images</code> and other small resources you could have.</p>
<blockquote>
<p>I also ended up switching the order in which the loaders were applied, which I think ultimately did the trick.</p>
</blockquote>
<p>Loaders order definition is important because they pipe the content over them.<br />
Here are some examples so you can understand how it works under the hood:</p>
<pre><code>**JS CONTENT ** &lt; Loader D &lt; Loader C &lt; Loader B &lt; Loader A &lt; **File**
</code></pre>
<p>file-loader example</p>
<pre><code>"public/path/to/image.thumbnail.png" (module exported string) &lt; file-loader?name=[name].thumbnail.[ext] (saves file on folder and exports path) &lt; gm-loader (handle resizing, exports thumbnailed file) &lt; Original File (buffer with its content)
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-189384740">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/cusspvz" target="_blank">@cusspvz</a> thanks for the detailed explanation and overview!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-202520381">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>It'd better be</p>
<pre><code>,
      {
        test: /\.(png|woff|woff2|eot|ttf|svg)(\?v=[0-9]\.[0-9]\.[0-9])?$/,
        loader: 'url'
      }
</code></pre>
<p>to cover caching specific versions</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-220842106">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Hi, I also have some questions  when I <code>import "amazeui/less/amazeui.less"</code>.</p>
<pre><code>ERROR in ./~/css-loader!./~/less-loader!./~/amazeui/less/amazeui.less
Module not found: Error: Cannot resolve 'file' or 'directory' ../fonts/fontawesome-webfont.eot in /Users/missl/webpack-lazyload-angular/node_modules/amazeui/less
 @ ./~/css-loader!./~/less-loader!./~/amazeui/less/amazeui.less 6:99961-100012

ERROR in ./~/css-loader!./~/less-loader!./~/amazeui/less/amazeui.less
Module not found: Error: Cannot resolve 'file' or 'directory' ../fonts/fontawesome-webfont.eot in /Users/missl/webpack-lazyload-angular/node_modules/amazeui/less
 @ ./~/css-loader!./~/less-loader!./~/amazeui/less/amazeui.less 6:100035-100078

ERROR in ./~/css-loader!./~/less-loader!./~/amazeui/less/amazeui.less
Module not found: Error: Cannot resolve 'file' or 'directory' ../fonts/fontawesome-webfont.woff2 in /Users/missl/webpack-lazyload-angular/node_modules/amazeui/less
 @ ./~/css-loader!./~/less-loader!./~/amazeui/less/amazeui.less 6:100136-100189

ERROR in ./~/css-loader!./~/less-loader!./~/amazeui/less/amazeui.less
Module not found: Error: Cannot resolve 'file' or 'directory' ../fonts/fontawesome-webfont.woff in /Users/missl/webpack-lazyload-angular/node_modules/amazeui/less
 @ ./~/css-loader!./~/less-loader!./~/amazeui/less/amazeui.less 6:100220-100272

ERROR in ./~/css-loader!./~/less-loader!./~/amazeui/less/amazeui.less
Module not found: Error: Cannot resolve 'file' or 'directory' ../fonts/fontawesome-webfont.ttf in /Users/missl/webpack-lazyload-angular/node_modules/amazeui/less
 @ ./~/css-loader!./~/less-loader!./~/amazeui/less/amazeui.less 6:100302-100353

ERROR in ./~/css-loader!./~/less-loader!./~/amazeui/less/amazeui.less
Module not found: Error: Cannot resolve 'file' or 'directory' ../fonts/fontawesome-webfont.svg in /Users/missl/webpack-lazyload-angular/node_modules/amazeui/less
 @ ./~/css-loader!./~/less-loader!./~/amazeui/less/amazeui.less 6:100387-100438
</code></pre>
<p>In addition, Please click <a href="https://github.com/amazeui/amazeui/" target="_blank">here</a> about <code>amazeui</code></p>
<p>But when I <code>import "amazeui/dist/css/amazeui.min.css"</code> questions don't exist.</p>
<p>I think in less file use <code>font</code>  so it have these questions.</p>
<p>Can you help me?</p>
<p>Thanks</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-220879259">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I reviewed <code>amazeui</code> work tree , there is not fonts folder.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-260818734">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>thanks <a href="https://github.com/TonyWang031" target="_blank">@TonyWang031</a></p>
<p>before :</p>
<blockquote>
<p>You may need an appropriate loader to handle this file type.<br />
SyntaxError: Unexpected character '�' (1:0)</p>
</blockquote>
<p>it worked! after apply:</p>
<blockquote>
<p>{ test: /.(png|woff(2)?|eot|ttf|svg)(?[a-z0-9=.]+)?$/, loader: 'url-loader?limit=100000' }</p>
</blockquote>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-261277259">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>You can find the full solution here<br />
<a href="https://github.com/theodybrothers/webpack-bootstrap" target="_blank">webpack-bootstrap</a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-266200836">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>None of this works for me</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-270055074">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>what if you are not wanting to bundle fonts at all? I originally had my pcss being parsed by postcss-cli and output to the same dir as webpacks build.</p>
<pre><code>@font-face {
  font-family: "sofachrome";
  src: url(../fonts/sofachrome.regular.ttf) format("truetype");
}
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-270251286">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Lovely solution !! Thank you for your answer.<br />
I wasted so much time but you solve it. I'm so happy now.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
      <div>
        <h3 id="ref-issue-197561765">
      
        
      
        <img src="https://avatars3.githubusercontent.com/u/3920576?s=60&v=4" width="16" height="16" alt="@lordptolmy" />
  <a href="/lordptolmy" target="_blank">lordptolmy</a>
  

      referenced this issue
        in <strong>shakacode/bootstrap-loader</strong>
      <a href="#ref-issue-197561765" target="_blank">
        <relative-time>on Jan 5, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/shakacode/bootstrap-loader/issues/230" target="_blank">
          Unexpected character '�' (1:0)
          #230
        </a>
      </h4>
    

    


  

</div>




  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-271762065">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>None of the solutions worked for me until I changed the paths to absolute<br />
Ex.:</p>
<pre><code>@font-face {
  font-family: 'Quicksand-Bold';
  src: url('~/src/sass/fonts/quicksand/quicksand-bold/Quicksand-Bold.eot');
}
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-272045587">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/mbeauchamp7" target="_blank">@mbeauchamp7</a> Have you tried this?</p>
<div><pre>@font-face {
  font-family: 'Quicksand-Bold';
  src: url('~./fonts/quicksand/quicksand-bold/Quicksand-Bold.eot');
}</pre></div>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-272047286">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/cusspvz" target="_blank">@cusspvz</a> This worked as well thanks!</p>
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
    
  <div id="issuecomment-272047520">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/mbeauchamp7" target="_blank">@mbeauchamp7</a> It worked because the <code>~</code> acts as a module indicator for <code>css-loader</code>, meaning that it should load the file over webpack instead of css.</p>
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
    
  <div id="issuecomment-272050512">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/cusspvz" target="_blank">@cusspvz</a> Ah thanks for the clarification!</p>
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
        <h3 id="ref-issue-198640369">
      
        
      
        <img src="https://avatars3.githubusercontent.com/u/664177?s=60&v=4" width="16" height="16" alt="@posva" />
  <a href="/posva" target="_blank">posva</a>
  

      referenced this issue
        in <strong>vuejs-templates/webpack</strong>
      <a href="#ref-issue-198640369" target="_blank">
        <relative-time>on Jan 17, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/vuejs-templates/webpack/issues/431" target="_blank">
          import bootstrap fonts errors
          #431
        </a>
      </h4>
    

    


  

</div>


</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-273027871">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/mattybow" target="_blank">@mattybow</a> Hey I am using scss syntax and added an appropriate loader for it also. Here is my config<br />
<code>var webpack = require('webpack');</code><br />
<code>module.exports = {</code><br />
<code>context: __dirname + '/src',</code><br />
<code>entry: {</code><br />
<code>app: './app.js',</code><br />
<code>vendor: ['angular', 'angular-ui-router', 'angular-bootstrap-calendar', 'bootstrap-css-only']</code><br />
<code>},</code><br />
<code>output: {</code><br />
<code>path: __dirname + '/js',</code><br />
<code>filename: 'app.bundle.js'</code><br />
<code>},</code><br />
<code>module:{</code><br />
<code>loaders: [</code><br />
<code>{</code><br />
<code>test: /\.scss$/,</code><br />
<code>loader: "style!css!sass",</code><br />
<code>},</code><br />
<code>{ test: /\.(png|woff|woff2|eot|ttf|svg)$/, loader: 'url-loader?limit=100000' }</code><br />
<code>],</code><br />
<code>},</code><br />
<code>plugins: [</code><br />
<code>new webpack.optimize.CommonsChunkPlugin("vendor", "vendor.bundle.js")</code><br />
<code>]</code><br />
<code>};</code><br />
But I am getting the error</p>
<blockquote>
<p>node_modules/bootstrap-css-only/css/bootstrap.min.css Unexpected token (5:83)<br />
You may need an appropriate loader to handle this file type.<br />
SyntaxError: Unexpected token (5:83)</p>
</blockquote>
<p>while building. Am I in short of any loaders here?</p>
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
    
  <div id="issuecomment-273031323">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/hrishikeshqb" target="_blank">@hrishikeshqb</a> your error says that it does not know how to handle a <code>.css</code> file.  You'll need to tell it how to handle a file with that extension in another loader entry with a test regex that matches ending in .css</p>
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
    
  <div id="issuecomment-273032145">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/mattybow" target="_blank">@mattybow</a> Thanks man! it worked. Earlier I added css as <code>&lt;link rel="stylesheet" type="text/css" href='node_modules/bootstrap-only-css/dist/bootstrap.css'&gt;</code>  in my index.html. But from now I guess webpack will take care of it.</p>
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
    
  <div id="issuecomment-297680061">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Just remeber to install file-loader and url-loader before changing your webpack config.<br />
<strong>Using</strong> :<br />
<code>npm install --save file-loader url-loader</code></p>
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
    
  <div id="issuecomment-308182276">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>For people from the future, I went with a different solution.<br />
I used <code>raw-loader</code>:</p>
<pre><code>module: {
  rules: [
    {
      test: /\.scss$/,
      use: ExtractTextPlugin.extract([
        'raw-loader',
        'sass-loader',
      ])
    },
  ]
}
</code></pre>
<p>Then imported fonts where I wanted them with <code>copy-webpack-plugin</code>:</p>
<pre><code>plugins: [
  new CopyWebpackPlugin([
    {
      // Copy Some Specific Fonts
      from: './node_modules/.../.../fonts',
      to: 'fonts'
    }
  ])
]
</code></pre>
<p>This gives me some extra control too so we avoid importing fonts unintentionally from other plugins, etc.</p>
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
    
  <div id="issuecomment-309260496">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Thanks! <a href="https://github.com/mattybow" target="_blank">@mattybow</a> , for sharing the solution :)</p>
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
    
  <div id="issuecomment-313673931">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>This code worked for me with webpack2:</p>
<div><pre>      {
        test: /\.(ttf|otf|eot|svg|woff(2)?)(\?[a-z0-9]+)?$/,
        loader: 'file-loader?name=fonts/[name].[ext]'
      }</pre></div>
<p>I'm using <a href="https://icomoon.io/app/" target="_blank">https://icomoon.io/app/</a> , my css looks like:</p>
<div><pre>@font-face {
  font-family: 'icomoon';
  src:
    url('fonts/icomoon.ttf?3jbvu') format('truetype'),
    url('fonts/icomoon.woff?3jbvu') format('woff'),
    url('fonts/icomoon.svg?3jbvu#icomoon') format('svg');
  font-weight: normal;
  font-style: normal;
}</pre></div>
<p>Hope it helps.</p>
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
        <h3 id="ref-issue-248205057">
      
        
      
        <img src="https://avatars3.githubusercontent.com/u/1731922?s=60&v=4" width="16" height="16" alt="@psimyn" />
  <a href="/psimyn" target="_blank">psimyn</a>
  

      referenced this issue
        in <strong>storybooks/storybook</strong>
      <a href="#ref-issue-248205057" target="_blank">
        <relative-time>on Aug 6, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/storybooks/storybook/issues/1603" target="_blank">
          Can't import css
          #1603
        </a>
      </h4>
    

    


  

</div>


</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-325165976">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Slight improvement to <a href="https://github.com/TonyWang031" target="_blank">@TonyWang031</a> suggestion as it gives invalid regex<br />
<code>{test: /\.(jpe?g|png|woff|woff2|eot|ttf|svg)(\?[a-z0-9=.]+)?$/, loader: 'url-loader?limit=100000'}</code></p>
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
    
  <div id="issuecomment-326382025">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>@codetaha Good catch!  Beyond adding support for more filetypes, it looks like you're escaping a <code>.</code> and a <code>?</code>.  Are there other changes I'm missing?</p>
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
    
  <div id="issuecomment-327033901">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>The solution proposed by <a href="https://github.com/zyxneo" target="_blank">@zyxneo</a> is the best. Other solutions attempts to inline the SVG font into the CSS file which is insane.</p>
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
    
  <div id="issuecomment-343918994">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/oscaroceguera" target="_blank">@oscaroceguera</a> where did you put this? what location in what file? this is the exact issue I am having.</p>
<p>before :You may need an appropriate loader to handle this file type.SyntaxError: Unexpected character '�' (1:0)it worked!</p>
<h2>after apply:{ test: /.(png|woff(2)?|eot|ttf|svg)(?[a-z0-9=.]+)?$/, loader: 'url-loader?limit=100000' }</h2>
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
    
  <div id="issuecomment-343925073">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/anzcarroll" target="_blank">@anzcarroll</a>  When you get that error try stopping webpack and run it again</p>
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
    
  <div id="issuecomment-344828856">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I add the rule by zyxneo into webpack.config.js and redo<br />
<code>npm run dev</code><br />
It's fixed! Thank!</p>
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
    
  <div id="issuecomment-350081127">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Кто пояснит, в какой именно  файл это вписать? Какой именно конфиг??</p>
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
    
  <div id="issuecomment-354110333">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>In <code>webpack.config.js</code> in the section with <code>rules</code>. This is what works for me (slightly different from the proposed solution):</p>
<pre><code>module: {
  rules: [
    {
      test: /\.(woff|woff2|eot|ttf|svg)$/,
      exclude: /node_modules/,
      use: {
        loader: 'url-loader?limit=1024&name=/fonts/[name].[ext]'
      }
    }
  ]
}
</code></pre>
<p>You also need to install <code>url-loader</code> and <code>file-loader</code> for <code>webpack</code> with this command (if using <code>npm</code>):</p>
<pre><code>npm install --save-dev url-loader file-loader
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
    
  
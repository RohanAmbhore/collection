<a href="https://github.com/yinsang/blog/issues/5">https://github.com/yinsang/blog/issues/5</a><div id="articleHeader"><h1>              webpack            #5    </h1></div>


  <div>
    
    <div>
        <a href="/yinsang" target="_blank">yinsang</a>  opened this Issue
        <relative-time>on Feb 4</relative-time>
        · 13 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-294181960">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/yinsang" target="_blank">yinsang</a>
  

    </strong>

    commented

    <a href="#issue-294181960" target="_blank"><relative-time>on Feb 4</relative-time></a>


      
  •


  

  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>1, html-webpack-plugin 打包出来的文件过大无法显示,而且不报错.原因是 new HtmlWebpackPlugin ()于实例化的时候多了个空格。hoho！</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  


          

          

  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-362899278">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/yinsang" target="_blank">yinsang</a>
  

    </strong>

    commented

    <a href="#issuecomment-362899278" target="_blank"><relative-time>on Feb 4</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>2，html-webpack-plugin有一次打包后，打包后的文件不能被浏览器识别：<br />
报错：<br />
文件将不再编辑器显示，因为他是二进制文件、非常大或使用不支持的文本编码。<br />
结果是我查了很久没找到原因，后来无意发现我的ejs写错了！！！<br />
&lt;%= htmlWebpackPlugin.options.date =&gt; 最后的=该是%。</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-368508995">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/yinsang" target="_blank">yinsang</a>
  

    </strong>

    commented

    <a href="#issuecomment-368508995" target="_blank"><relative-time>on Feb 26</relative-time></a>


      
  •


  

  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>webpack 热刷新时请求的hot-update.json。dev环境下。<br />
<code>Failed to load http://localhost:8410/dist/82dca94f1807993529b8.hot-update.json: No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://172.18.101.75:8080' is therefore not allowed access.</code><br />
在静态服务static server 与请求host不一致时导致跨域。最简单的解决思路是安装chrome 下的<a href="https://chrome.google.com/webstore/detail/allow-control-allow-origi/nlfbmbojpeacfghkpbjhddihlkkiljbi/reviews" target="_blank">跨域插件</a>。</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-369116868">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><code>Module build failed: Error: Cannot find module '@babel/core'</code><br />
解决方案：<code>npm install -D @babel/core</code><br />
babel-core与babel/core不同！</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-369129912">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><code>Plugin/Preset files are not allowed to export objects, only functions.</code><br />
解决方案：<a href="https://github.com/babel/babel/issues/6808" target="_blank">babel/babel#6808</a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-369163801">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/yinsang" target="_blank">yinsang</a>
  

    </strong>

    commented

    <a href="#issuecomment-369163801" target="_blank"><relative-time>on Feb 28</relative-time></a>


      
  •


  

  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><code>Error: webpack.optimize.CommonsChunkPlugin has been removed, please use config.optimization.splitChunks instead.</code><br />
解决方案：<br />
<code>new webpack .optimize .CommonsChunkPlugin({ name: 'vendor', filename: 'js/vendor.bundle.js', minChunks: 2, }),</code><br />
to<br />
<code>optimization: { splitChunks: { cacheGroups: { commons: { name: 'vendor', chunks: 'initial', minChunks: 2 } } }, runtimeChunk: false },</code><br />
optimization is like a  <code>entry</code> 's brother direction. :)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-369166123">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/yinsang" target="_blank">yinsang</a>
  

    </strong>

    commented

    <a href="#issuecomment-369166123" target="_blank"><relative-time>on Feb 28</relative-time></a>


      
  •


  

  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>error:<code>Module build failed: Error: Plugin/Preset files are not allowed to export objects, only functions.</code><br />
solution：<code>"presets": ["@babel/preset-env","@babel/react"]</code><br />
you may need to install <code>npm install -D babel-preset-react</code></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-369169715">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/yinsang" target="_blank">yinsang</a>
  

    </strong>

    commented

    <a href="#issuecomment-369169715" target="_blank"><relative-time>on Feb 28</relative-time></a>


      
  •


  

  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><code>DeprecationWarning: Tapable.plugin is deprecated. Use new API on</code>.hooks<code>instead</code><br />
update extract-text-webpack-plugin！at least "extract-text-webpack-plugin": "^4.0.0-beta.0",</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-369174444">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/yinsang" target="_blank">yinsang</a>
  

    </strong>

    commented

    <a href="#issuecomment-369174444" target="_blank"><relative-time>on Feb 28</relative-time></a>


      
  •


  

  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><code>Module build failed: TypeError: Cannot read property 'babel' of undefined</code><br />
you may need to update your babel-loader to adapt webpack4!<br />
at least "babel-loader": "^8.0.0-beta.2",</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-369175309">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><code>TypeError: Cannot read property 'lessLoader' of undefined</code></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-369189967">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/yinsang" target="_blank">yinsang</a>
  

    </strong>

    commented

    <a href="#issuecomment-369189967" target="_blank"><relative-time>on Feb 28</relative-time></a>


      
  •


  

  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><code>TypeError: missingDeps.some is not a function 1|resource | at compiler.plugin (/Users/weiyinpeng/Documents/work-area/fe-lottery-terminal/node_modules/react-dev-utils/WatchMissingNodeModulesPlugin.js:27:23)</code><br />
solution:<br />
delete react-dev-utils.<br />
require('react-dev-utils/WatchMissingNodeModulesPlugin') 好像不被支持了</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-369190641">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/yinsang" target="_blank">yinsang</a>
  

    </strong>

    commented

    <a href="#issuecomment-369190641" target="_blank"><relative-time>on Feb 28</relative-time></a>


      
  •


  

  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><code>The 'mode' option has not been set. Set 'mode' option to 'development' or 'production' to enable defaults for this environment.</code><br />
solution:<br />
<code>mode: 'production',</code><br />
or<br />
<code>mode: 'development',</code></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-375838571">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>url-loader 是一个过滤器。不能说是file-loader的加强版！没有file-loader还行会导致<br />
<code>ERROR in ./src/index.png Module build failed: Error: Cannot find module 'file-loader'</code><br />
you need <code>yarn add file-loader url-loader -S</code></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-375843230">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>如果使用vue-loader ，就不必用完整版的vue了 也就是说webpack 里不需要配置vue$<br />
<code>alias: { vue$: "vue/dist/vue.esm.js" }</code><br />
to<br />
<code>alias: { // vue$: "vue/dist/vue.esm.js" }</code><br />
但是入口文件 index.js 需要<br />
<code>new Vue({ el: "#app", render: h =&gt; h(App) });</code></p>
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

  

  


  


          
      




        
      

    
    
  
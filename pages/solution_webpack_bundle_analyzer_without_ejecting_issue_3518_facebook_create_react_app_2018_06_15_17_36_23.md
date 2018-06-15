<a href="https://github.com/facebook/create-react-app/issues/3518">https://github.com/facebook/create-react-app/issues/3518</a><div id="articleHeader"><h1>              Solution: webpack-bundle-analyzer without ejecting.            #3518    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/trevorwhealy" target="_blank">trevorwhealy</a>  opened this Issue
        <relative-time>on Nov 29, 2017</relative-time>
        · 7 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      


  
    
      

          <p>Ejecting is a real shame for any instance of create-react-app, so I found a way to use webpack-bundle-analyzer without ejecting. Hopefully this will save someone out there from having to eject to make this addition.</p>
<ol>
<li>Create a file in root, I call mine "build.js"</li>
<li>Add this javascript.</li>
</ol>
<div><pre>process.env.NODE_ENV = "production"
var BundleAnalyzerPlugin = require("webpack-bundle-analyzer")
  .BundleAnalyzerPlugin

const webpackConfigProd = require("react-scripts/config/webpack.config.prod")

webpackConfigProd.plugins.push(
  new BundleAnalyzerPlugin({
    analyzerMode: "static",
    reportFilename: "report.html",
  })
)

require("react-scripts/scripts/build")</pre></div>
<ol>
<li><code>node build.js</code></li>
</ol>
<p><a href="https://camo.githubusercontent.com/973f843892247df345ac75ed7bf9df473890b229/68747470733a2f2f692e696d6775722e636f6d2f416d6a596976322e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/973f843892247df345ac75ed7bf9df473890b229/68747470733a2f2f692e696d6775722e636f6d2f416d6a596976322e706e67" /></div></a></p>
      
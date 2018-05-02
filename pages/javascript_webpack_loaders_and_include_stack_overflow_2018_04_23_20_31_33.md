<a href="https://stackoverflow.com/questions/34623229/webpack-loaders-and-include">https://stackoverflow.com/questions/34623229/webpack-loaders-and-include</a><div id="articleHeader"><h1>webpack loaders and include</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        21
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>2</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I'm new to webpack and I'm trying to understand loaders as well as its properties such as test, loader, include etc.</p>

<p>Here is a sample snippet of webpack.config.js that I found in google.</p>

<pre><code>module: {
    loaders: [
      {
        test: /\.js$/,
        loader: 'babel-loader',
        include: [
          path.resolve(__dirname, 'index.js'),
          path.resolve(__dirname, 'config.js'),
          path.resolve(__dirname, 'lib'),
          path.resolve(__dirname, 'app'),
          path.resolve(__dirname, 'src')
        ],
        exclude: [
          path.resolve(__dirname, 'test', 'test.build.js')
        ],
        cacheDirectory: true,
        query: {
          presets: ['es2015']
        }
      },
    ]
}</code></pre>

<ol>
<li><p>Am I right that test: /.js$/ will be used only for files with extension .js?</p></li>
<li><p>The loader: 'babel-loader', is the loader we install using npm</p></li>
<li><p>The include: I have many questions on this. Am I right that anything we put inside the array will be transpiled? That means, index.js, config.js, and all *.js files in lib, app and src will be transpiled.</p></li>
<li><p>More questions on the include: When files get transpiled, do the *.js files get concatenated into one big file?</p></li>
<li><p>I think exclude is self explanatory. It will not get transpiled.</p></li>
<li><p>What does query: { presets: ['es2015'] } do?</p></li>
</ol>
    </div>
    
    <div>
    

    <div>
        <div>
    <div>
        asked Jan 5 '16 at 23:39
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-34861723">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        13
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>In webpack config there are multiple things for configuration, important ones are</p>

<ol>
<li>entry - can be an array or an object defining the entry point for the asset you want to bundle, can be a js as test here says do it only for /.js$. Your application if has multiple entry points use an array.</li>
<li>include - defines the set of path or files where the imported files will be transformed by the loader.</li>
<li>exclude is self explanatory (do not transform file from these places).</li>
<li><p>output - the final bundle you want to create. if you specify for example</p>

<p>output: {
  filename: "[name].bundle.js",
  vendor: "react"
}</p>

<p>Then your application js files will be bundled as main.bundle.js and react in a vendor.js files. It is an error if you do not use both in html page.</p></li>
</ol>

<p>Hope it helped</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 18 '16 at 18:36
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-34623333">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>1) Correct.</p>

<p>2) Correct.</p>

<p>3) Correct.</p>

<p>4) I am unsure. My webpack.config.js file includes an output key, and does bundle it all into one file:</p>

<pre><code>output: {
    path: path.resolve(__dirname, 'build'),
    filename: 'bundle.js'
}</code></pre>

<p>5) Correct.</p>

<p>6) This tells babel-loader what sort of transpile you want it to perform, as well as other compile options. So, for example, if you want it to transpile jsx as well + cache results for improve performance, you would change it to:</p>

<pre><code>query: {
    presets: ['react', 'es2015'],
    cacheDirectory: true
}</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 5 '16 at 23:49
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-46979439">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>This documentation helped me understand better. Looks like it is for webpack 1 but still applies. </p>

<p><a href="https://webpack.github.io/docs/configuration.html#module-loaders" target="_blank">https://webpack.github.io/docs/configuration.html#module-loaders</a></p>

<blockquote>
  <p><strong>Loaders</strong></p>
  
  <p>An array of automatically applied loaders.</p>
  
  <p>Each item can have these properties:</p>
  
  <ul>
  <li><strong>test:</strong> A condition that must be met</li>
  <li><strong>exclude:</strong> A condition that must not be met </li>
  <li><strong>include:</strong> An array of paths or files where the imported files will be transformed by the loader </li>
  <li><strong>loader:</strong>  A string of “!” separated loaders </li>
  <li><strong>loaders:</strong> An array of    loaders as string</li>
  </ul>
</blockquote>

<p>This example helped me understand what is going on. Looks like you use either include or exclude but not both. The test is a condition applied to all files. So if you include a folder, each file must pass the test condition. I have not verified this, but based on the example provided by the documentation, it look like that is how it works. </p>

<pre><code>    module: {

      rules: [
        {
          // "test" is commonly used to match the file extension
          test: /\.jsx$/,

          // "include" is commonly used to match the directories
          include: [
            path.resolve(__dirname, "app/src"),
            path.resolve(__dirname, "app/test")
          ],
          // "exclude" should be used to exclude exceptions
          // try to prefer "include" when possible

          // the "loader"
          loader: "babel-loader" // or "babel" because webpack adds the '-loader' automatically
        }
      ]

    }</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 27 '17 at 16:16
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    




<div id="post-editor">

    <div> 
        <div>
            <div id="mdhelp">
    <ul id="mdhelp-tabs">
        <li>Links</li>
        <li>Images</li>
        <li>Styling/Headers</li>
        <li>Lists</li>
        <li>Blockquotes</li>
        
        
        <li><a href="/editing-help" target="_blank">advanced help »</a></li>
    </ul>
    
    

    
    
    

    

    

    

    
</div>
            
        </div>
    </div>

    
    

    

    


    
    
    



</div>

                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/ecmascript-6" title="show questions tagged 'ecmascript-6'" target="_blank">ecmascript-6</a> <a href="/questions/tagged/webpack" title="show questions tagged 'webpack'" target="_blank">webpack</a> <a href="/questions/tagged/webpack-style-loader" title="show questions tagged 'webpack-style-loader'" target="_blank">webpack-style-loader</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
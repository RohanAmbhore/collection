<a href="https://github.com/chentsulin/electron-react-boilerplate/issues/129">https://github.com/chentsulin/electron-react-boilerplate/issues/129</a><div id="articleHeader"><h1>              Images not showing in packaged app            #129    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/NikZar" target="_blank">NikZar</a>  opened this Issue
        <relative-time>on Jan 29, 2016</relative-time>
        · 4 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      

  
    
      

          <p>Hi all, I am having problems with images (referenced in app.css) in my packaged electron application.</p>
<p><code>background-image: url(images/splashscreen.gif);</code></p>
<p>While developing, the images are loaded correctly.<br />
I am using the url-loader for png and gif images in my <em>webpack.config.base.js</em>:</p>
<pre><code>module: {
    loaders: [
    {
      test: /\.jsx?$/,
      loaders: ['babel-loader'],
      exclude: /node_modules/
    },
    {
      test: /\.png$/,
      loader: "url-loader?limit=100000"
    },
    {
      test: /\.gif$/,
      loader: "url-loader?limit=100000"
    },
    {
      test: /\.jpg$/,
      loader: "file-loader"
    }
    ]
  },
</code></pre>
<p>The images seem also to be correctly generated in the dist folder.<br />
However in the packaged app (after running "npm run package-all") the images are not showing correctly (I don't know how to debug a packaged app).<br />
Here it is my dummy project: <a href="https://github.com/NikZar/Reactiwall" target="_blank">repo</a><br />
This is the first time I am using react and webpack, am I missing something?<br />
Could we add something to correctly cover image handling in the boilerplate?</p>
<p>Thank you in advance!</p>
      
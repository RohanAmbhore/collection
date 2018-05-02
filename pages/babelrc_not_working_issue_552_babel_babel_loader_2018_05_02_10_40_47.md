<a href="https://github.com/babel/babel-loader/issues/552">https://github.com/babel/babel-loader/issues/552</a><div id="articleHeader"><h1>              .babelrc not working            #552    </h1></div>


  <div>
    
    <div>
        <a href="/jaschaio" target="_blank">jaschaio</a>  opened this Issue
        <relative-time>on Dec 10, 2017</relative-time>
        · 26 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I have folled a very simple tutorial to set up webpack, babel and react, but get an error with the presets when I use a <code>.babelrc</code> file.</p>
<p>webpack.config.js:</p>
<pre><code>var path = require('path');

module.exports = {
    entry: './src/index.js', // Bundle all assets from this location together
    output: {
        filename: 'bundle.js', // Output to this file
        path: path.resolve( __dirname, 'dist' ) // In this location
    },
    module: {
        rules: [
            { 
                test: /\.(js|jsx|mjs)$/, 
                loader: 'babel-loader',
                exclude: /node_modules/,

            },
            {
                test: /\.css$/,
                use: [ 'style-loader', 'css-loader' ]
            }
        ]
    },
    devServer: {
        contentBase: path.resolve(__dirname, "dist")
    }
};
</code></pre>
<p>.babelrc:</p>
<pre><code>{
  "presets": ["env", "react"]
}
</code></pre>
<p>Gets me the following error:</p>
<pre><code>ERROR in ./src/index.js
Module build failed: SyntaxError: Unexpected token (17:12)

  15 |     render() {
  16 |         return (
&gt; 17 |             &lt;div style={ { textAlign: 'center' } }&gt;
     |             ^
</code></pre>
<p>If I change my webpack.config.js file to this instead it works:</p>
<pre><code>var path = require('path');

module.exports = {
    entry: './src/index.js', // Bundle all assets from this location together
    output: {
        filename: 'bundle.js', // Output to this file
        path: path.resolve( __dirname, 'dist' ) // In this location
    },
    module: {
        rules: [
            { 
                test: /\.(js|jsx|mjs)$/, 
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['env', 'react']
                    }
                }
            },
            {
                test: /\.css$/,
                use: [ 'style-loader', 'css-loader' ]
            }
        ]
    },
    devServer: {
        contentBase: path.resolve(__dirname, "dist")
    }
};
</code></pre>
<p>From my understanding having the options object or a .babelrc file should do the same thing. But only one of them works.</p>
<p>I don't have a <code>"babel": {}</code> block within my package.json so I really don't see why it seems that the .babelrc file is not recognized.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    
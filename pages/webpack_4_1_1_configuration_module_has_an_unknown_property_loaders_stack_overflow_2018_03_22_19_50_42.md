<a href="https://stackoverflow.com/questions/49203841/webpack-4-1-1-configuration-module-has-an-unknown-property-loaders">https://stackoverflow.com/questions/49203841/webpack-4-1-1-configuration-module-has-an-unknown-property-loaders</a><div id="articleHeader"><h1>webpack 4.1.1 -> configuration.module has an unknown property 'loaders'.</h1></div>

<p>I just updated webpack to <code>4.1.1</code> and when I try to run it I get the following error:</p>

<blockquote>
  <p>Invalid configuration object. Webpack has been initialised using a
  configuration object that does not match the API schema.
   - configuration.module has an unknown property 'loaders'. These properties are valid:    object { exprContextCritical?,
  exprContextRecursive?, exprContextRegExp?, exprContextRequest?,
  noParse?, rules?, defaultRules?, unknownContextCritical?,
  unknownContextRecursive?, unknownContextRegExp?,
  unknownContextRequest?, unsafeCache?, wrappedContextCritical?,
  wrappedContextRecursive?, wrappedContextRegExp?,
  strictExportPresence?, strictThisContextOnImports? }    -&gt; Options
  affecting the normal modules (<code>NormalModuleFactory</code>).</p>
</blockquote>

<p><code>loaders</code> look like this and worked with <code>webpack 3.11.0</code>:</p>

<pre><code>module: {
    loaders: [
        { test: /\.tsx?$/, loader: ['ts-loader'] },
        { test: /\.css$/, loader: "style-loader!css-loader" },
        {
            test: /\.scss$/, use: [{
                loader: "style-loader" // creates style nodes from JS strings
            }, {
                loader: "css-loader" // translates CSS into CommonJS
            }, {
                loader: "sass-loader" // compiles Sass to CSS
            }]
        },
        { test: /\.(otf|ttf|eot|svg|woff(2)?)(\?[a-z0-9=&.]+)?$/, loader: 'file-loader?name=./Scripts/dist/[name].[ext]' }
    ]
}
</code></pre>
    
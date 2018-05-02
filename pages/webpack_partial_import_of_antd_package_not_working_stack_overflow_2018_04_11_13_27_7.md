<a href="https://stackoverflow.com/questions/44563394/partial-import-of-antd-package-not-working">https://stackoverflow.com/questions/44563394/partial-import-of-antd-package-not-working</a><div id="articleHeader"><h1>Partial import of antd package not working</h1></div>

<p>I am importing antd package using the <code>babel-plugin-import</code> plugin. However, I am getting the warning that the whole bundle is imported.</p>

<blockquote>
  <p>You are using a whole package of antd, please use
  <a href="https://www.npmjs.com/package/babel-plugin-import" target="_blank">https://www.npmjs.com/package/babel-plugin-import</a> to reduce app bundle
  size.</p>
</blockquote>

<p>My webpack config for jsx is as follows:</p>

<pre><code>{
    test: /\.jsx$/,
    loader: 'babel-loader',
    exclude: [nodeModulesDir],
    options: {
        cacheDirectory: true,
        plugins: [
            'transform-decorators-legacy',
            'add-module-exports',
            ["import", { "libraryName": "antd", "style": true }],
            ["react-transform", {
                transforms: [
                    {
                        transform: 'react-transform-hmr',
                        imports: ['react'],
                        locals: ['module']
                    }
                ]
            }]
        ],
        presets: ['es2015', 'stage-0', 'react']
    }
},
</code></pre>

<p>For some reason, the entire antd bundle is being imported. </p>
    
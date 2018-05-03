<a href="https://juejin.im/post/5ae9ae5e518825672f19b094?utm_source=gold_browser_extension">https://juejin.im/post/5ae9ae5e518825672f19b094?utm_source=gold_browser_extension</a><div id="articleHeader"><h1>Webpack中publicPath详解</h1></div><br /><br /><figure><div class="readableLargeImageContainer"><img src="https://user-gold-cdn.xitu.io/2018/5/2/16320dd1bf6c1c8e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" /></div></figure><blockquote>
<p>最近自己在搭建一个基于webpack的react项目，遇到关于<code>output.publicPath</code>和webpack-dev-server中<code>publicPath</code>的问题，而官方文档对它们的描述也不是很清楚，所以自己研究了下并写下本文记录。</p>
</blockquote>
<h2>output</h2>
<p>output选项指定webpack输出的位置，其中比较重要的也是经常用到的有<code>path</code>和<code>publicPath</code></p>
<h3>output.path</h3>
<ul>
<li>默认值：<code>process.cwd()</code></li>
</ul>
<p><code>output.path</code>只是指示输出的目录，对应一个<strong>绝对路径</strong>，例如在项目中通常会做如下配置：</p>
<pre><code>output: {
	path: path.resolve(__dirname, '../dist'),
}
</code></pre><h3>output.publicPath</h3>
<ul>
<li>默认值：空字符串</li>
</ul>
<p><a href="https://link.juejin.im?target=https%3A%2F%2Fdoc.webpack-china.org%2Fguides%2Fpublic-path%2F" target="_blank">官方文档中对publicPath的解释</a>是</p>
<blockquote>
<p>webpack 提供一个非常有用的配置，该配置能帮助你为项目中的所有资源指定一个基础路径，它被称为公共路径(publicPath)。</p>
</blockquote>
<p>而关于如何应用该路径并没有说清楚...</p>
<p>其实这里说的所有资源的基础路径是指项目中引用css，js，img等资源时候的一个基础路径，这个基础路径要配合具体资源中指定的路径使用，所以其实打包后资源的访问路径可以用如下公式表示：</p>
<pre><code>静态资源最终访问路径 = output.publicPath + 资源loader或插件等配置路径
</code></pre>
<pre><code>output.publicPath = '/dist/'

// image
options: {
 	name: 'img/[name].[ext]?[hash]'
}

// 最终图片的访问路径为
output.publicPath + 'img/[name].[ext]?[hash]' = '/dist/img/[name].[ext]?[hash]'

// js output.filename
output: {
	filename: '[name].js'
}
// 最终js的访问路径为
output.publicPath + '[name].js' = '/dist/[name].js'

// extract-text-webpack-plugin css
new ExtractTextPlugin({
	filename: 'style.[chunkhash].css'
})
// 最终css的访问路径为
output.publicPath + 'style.[chunkhash].css' = '/dist/style.[chunkhash].css'
</code></pre><p>这个最终静态资源访问路径在使用html-webpack-plugin打包后得到的html中可以看到。所以<code>publicPath</code>设置成相对路径后，相对路径是相对于build之后的index.html的，例如，如果设置<code>publicPath: './dist/'</code>，则打包后js的引用路径为<code>./dist/main.js</code>，但是这里有一个问题，相对路径在访问本地时可以，但是如果将静态资源托管到CDN上则访问路径显然不能使用相对路径，但是如果将<code>publicPath</code>设置成<code>/</code>，则打包后访问路径为<code>localhost:8080/dist/main.js</code>，本地无法访问</p>
<p>所以这里需要在上线时候手动更改<code>publicPath</code>，感觉不是很方便，但是不知道该如何解决...</p>
<blockquote>
<p>一般情况下<strong>publicPath应该以'/'结尾，而其他loader或插件的配置不要以'/'开头</strong></p>
</blockquote>
<h2>webpack-dev-server中的publicPath</h2>
<p><a href="https://link.juejin.im?target=https%3A%2F%2Fdoc.webpack-china.org%2Fconfiguration%2Fdev-server%2F%23devserver-publicpath-" target="_blank">点击查看官方文档中关于devServer.publicPath的介绍</a></p>
<p>在开发阶段，我们借用devServer启动一个开发服务器进行开发，这里也会配置一个<code>publicPath</code>，这里的<code>publicPath</code>路径下的打包文件可以在浏览器中访问。而静态资源仍然使用<code>output.publicPath</code>。</p>
<p>webpack-dev-server打包的内容是放在内存中的，这些打包后的资源对外的的根目录就是<code>publicPath</code>，换句话说，这里我们设置的是打包后资源存放的位置</p>

<pre><code>// 假设devServer的publicPath为
const publicPath = '/dist/'
// 则启动devServer后index.html的位置为
const htmlPath = `${pablicPath}index.html`
// 包的位置
cosnt mainJsPath = `${pablicPath}main.js`
</code></pre><p>以上可以直接通过<code>http://lcoalhost:8080/dist/main.js</code>访问到。</p>
<p>通过访问 <code>http://localhost:8080/webpack-dev-server</code> 可以得到devServer启动后的资源访问路径，如图所示，点击静态资源可以看到静态资源的访问路径为 <code>http://localhost:8080${publicPath}index.html</code></p><figure><div class="readableLargeImageContainer"><img src="data:image/svg+xml;utf8,<?xml version="1.0"?><svg xmlns="http://www.w3.org/2000/svg" version="1.1"  ></svg>" alt="图1-1" /></div></figure><h2>html-webpack-plugin</h2>
<p>这个插件用于将css和js添加到html模版中，其中<code>template</code>和<code>filename</code>会受到路径的影响，从源码中可以看出</p>
<h3>template</h3>
<p>作用：用于定义模版文件的路径</p>

<pre><code>this.options.template = this.getFullTemplatePath(this.options.template, compiler.context);
</code></pre><p>因此<code>template</code>只有定义在webpack的<code>context</code>下才会被识别，<strong>webpack context的默认值为<code>process.cwd()</code>，既运行 node 命令时所在的文件夹的绝对路径</strong></p>
<h3>filename</h3>
<p>作用：输出的HTML文件名，默认为index.html，可以直接配置带有子目录</p>

<pre><code>this.options.filename = path.relative(compiler.options.output.path, filename);
</code></pre><p><strong>所以filename的路径是相对于<code>output.path</code>的，而在webpack-dev-server中，则是相对于webpack-dev-server配置的<code>publicPath</code>。</strong></p>
<p>如果webpack-dev-server的<code>publicPath</code>和<code>output.publicPath</code>不一致，在使用html-webpack-plugin可能会导致引用静态资源失败，因为在devServer中仍然以<code>output.publicPath</code>引用静态资源，和webpack-dev-server的提供的资源访问路径不一致，从而无法正常访问。</p>
<blockquote>
<p>有一种情况除外，就是<code>output.publicPath</code>是相对路径，这时候可以访问本地资源</p>
</blockquote>
<p><strong>所以一般情况下都要保证devServer中的<code>publicPath</code>与<code>output.publicPath</code>保持一致。</strong></p>

<p>关于webpack中的<code>path</code>就总结这么多，在研究关于webpack路径的过程中看查到的一些关于路径的零碎的知识如下：</p>
<h3>斜杠<code>/</code>的含义</h3>
<p>配置中<code>/</code>代表url根路径，例如<code>http://localhost:8080/dist/js/test.js</code>中的<code>http://localhost:8080/</code></p>
<h3>devServer.publicPath & devServer.contentBase</h3>
<ul>
<li>devServer.contentBase 告诉服务器从哪里提供内容。只有在你想要提供静态文件时才需要。</li>
<li>devServer.publicPath 将用于确定应该从哪里提供 bundle，并且此选项优先。</li>
</ul>
<h3>node中的路径</h3>
<ul>
<li><code>__dirname</code>: 总是返回被执行的 js 所在文件夹的绝对路径</li>
<li><code>__filename</code>: 总是返回被执行的 js 的绝对路径</li>
<li><code>process.cwd()</code>: 总是返回运行 node 命令时所在的文件夹的绝对路径</li>
</ul>



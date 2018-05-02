<a href="https://juejin.im/post/5a99f80cf265da238c3a1e16?utm_source=gold_browser_extension">https://juejin.im/post/5a99f80cf265da238c3a1e16?utm_source=gold_browser_extension</a><div id="articleHeader"><h1>当面试官问你如何进行性能优化时，你该这么回答(一)</h1></div>
<p>在开发好页面后，如何让页面更快更好的运行，是区分一个程序猿技术水平和视野的一个重要指标。所以面试时，面试官总会问你一个问题，如何进行性能优化呢？</p>
<p>如果你这时是头脑一片空白，或是像之前的我一样，靠死记硬背或是之前的经历，答一下压缩代码，打包代码，雪碧图，cdn，事件代理，这说明你对性能优化还是缺乏一个整体，系统的掌握，对性能优化还只是处于听说过一个方法就加上去的阶段。这样也就无从去更好的优化性能。</p>
<p>最近一个星期经过疯狂的面试和查询资料，我总算积累了一些经验和思考，在这个招聘的黄金时间，分享给大家，希望大家可以有一点收获。如果有收获，欢迎关注和star一下<a href="https://link.juejin.im?target=hpoenixf.com" target="_blank">博客</a>，<a href="https://link.juejin.im?target=https%3A%2F%2Fgithub.com%2Fhpoenixf%2Fhpoenixf.github.io" target="_blank">github</a></p>
<h4>性能优化是什么</h4>
<p>从前端的角度来说，性能优化可以分为两个方向。从用户角度来看，一个是页面加载的很快，另一个是页面使用起来很流畅。因此，对性能优化的探索，我们可以分为页面加载时间跟页面运行效率两个方向来进行研究</p>
<h4>从浏览器打开到页面渲染完成，花费了多少时间</h4>
<p>是的，这个问题有点熟悉，面试官比较常问的是从浏览器打开到页面渲染完成，发生了什么事情。这个问题网上很多回答，我也不就重复的细说了。主要的过程是：</p>
<p>浏览器解析-&gt;查询缓存-&gt;dns查询-&gt;建立链接-&gt;服务器处理请求-&gt;服务器发送响应-&gt;客户端收到页面-&gt;解析HTML-&gt;构建渲染树-&gt;开始显示内容(白屏时间)-&gt;首屏内容加载完成(首屏时间)-&gt;用户可交互(DOMContentLoaded)-&gt;加载完成(load)</p>
<p>很显然，如果我们要进行加载时间的优化，我们需要从这里的每一个步骤都去思考，去总结，而避免东凑一点，西凑一点。</p>
<h5>页面加载时间监控</h5>
<p>有一句话说得好，If You Can't Measure It, You Can't Manage It。在对这些环节进行优化之前，我们需要知道如何监控这些环节花费了多少时间。</p>
<p>首先推荐一个<a href="https://link.juejin.im?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FAPI%2FPerformanceTiming" target="_blank">PerformanceTiming</a>,可以获取到很多页面加载相关的数据。
比较常用的有</p>
<pre><code>DNS解析时间： domainLookupEnd - domainLookupStart
TCP建立连接时间： connectEnd - connectStart
白屏时间： responseStart - navigationStart
dom渲染完成时间： domContentLoadedEventEnd - navigationStart
页面onload时间： loadEventEnd - navigationStart

</code></pre><p>如果不使用该API，可以以服务器渲染返回的时间，或是SPA路由跳转离开的时间为起点，domContentLoaded，load等事件为结束点进行记录。或是直接上google analytics。方法很多，就不细说了。</p>
<h5>服务器部分优化要点</h5>
<p>后端部分可以对缓存，dns查询时间，链接时间，处理请求时间，响应时间等进行优化。</p>
<p>缓存就不细说了。</p>
<p>dns查询时间可以使用httpdns或是dns预加载，域名收敛等手段优化。</p>
<p>建立连接的重点是长连接和链接复用，keep-alive，long-polling，http-straming，websocket或是自己写过别的协议，更好的是直接上http2。为了优化链接的环节，前端这里还需要对资源使用cdn，雪碧图，代码合并等手段。</p>
<p>服务器处理请求这里可以优化的点也不少，值得注意的就是移动端访问PC端页面需要跳转到移动端页面时，要再服务器端使用302跳转，不要在前端进行跳转。还有就是启用hsts，要求浏览器在之后的访问使用https，减少无谓的http跳转https，同时还可以防止ssl剥离攻击，提升安全性。</p>
<p>服务器发送响应环节，可以使用Transfer-Encoding=chunked，多次返回响应，具体操作查询bigpipe。还有就是减小cookie的体积等等。</p>
<h5>前端部分优化要点</h5>
<p>前端部分可以对白屏时间，首屏事件，可交换时间，加载完成时间进行优化。</p>
<p>-未完，待续-</p>
<p>博客文章链接<a href="https://link.juejin.im?target=http%3A%2F%2Fhpoenixf.com%2Fweb%25E6%2580%25A7%25E8%2583%25BD%25E4%25BC%2598%25E5%258C%2596%25EF%25BC%2588%25E4%25B8%2580%25EF%25BC%2589.html" target="_blank">web性能优化（一）</a>，<a href="https://link.juejin.im?target=https%3A%2F%2Fgithub.com%2Fhpoenixf%2Fhpoenixf.github.io" target="_blank">github</a>，欢迎star和follow，谢谢！</p>

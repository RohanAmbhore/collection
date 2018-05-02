<a href="https://developers.google.com/web/fundamentals/web-components/shadowdom">https://developers.google.com/web/fundamentals/web-components/shadowdom</a><div id="articleHeader"><h1>    Shadow DOM v1：独立的网络组件  </h1></div>
  
  
  
  
  
    



<section>
  <div>
    <figure>
      <img src="https://developers.google.com/web/images/contributors/ericbidelman.jpg" alt="Eric Bidelman" />
    </figure>
  </div>
  <section>
    <div>
      <strong>By</strong>
      
        <a href="https://developers.google.com/web/resources/contributors/ericbidelman" target="_blank">
          Eric
          Bidelman
        </a>
      
    </div>
    <div>
        Engineer @ Google working on web tooling: Headless Chrome, Puppeteer, Lighthouse
    </div>
  </section>
</section>

<h3 id="tldr">TL;DR</h3>
<p>Shadow DOM 解决了构建网络应用的脆弱性问题。脆弱性是由 HTML、CSS 和 JS 的全局性引起的。
多年以来，我们发明了<a href="http://getbem.com/introduction/" target="_blank">多</a><a href="https://github.com/css-modules/css-modules" target="_blank">个</a><a href="https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/" target="_blank">工具</a>来规避这些问题。例如，使用新的 HTML id/类时，无法了解是否与页面所使用的现有名称冲突。<a href="http://www.2ality.com/2012/08/ids-are-global.html" target="_blank">微小错误</a>渐渐增多，CSS 特异性成为一个大问题（<code>!important</code> 所有的事情！），样式选择器变得失控以及<a href="https://developers.google.com/web/updates/2016/06/css-containment" target="_blank">性能可能受损</a>，不一而足。</p>
<p><strong>Shadow DOM 修复了 CSS 和 DOM</strong>。它在网络平台中引入<strong>作用域样式</strong>。
无需工具或命名约定，您即可使用原生 JavaScript <strong>捆绑 CSS 和标记</strong>、隐藏实现详情以及<strong>编写独立的组件</strong>。</p>

<p>注：<strong>已经很熟悉 Shadow DOM？</strong>本文章介绍新版 <a href="http://w3c.github.io/webcomponents/spec/shadow/" target="_blank">Shadow DOM v1 规范</a>。如果您有 Shadow DOM 的使用经验，则应该了解 <a href="https://www.chromestatus.com/features/4507242028072960" target="_blank">Chrome 35 中随附的 v0 版本</a>以及 webcomponents.js polyfill。这些概念是相同的，只不过 v1 规范的 API 存在一些重要差异。此外，所有主要浏览器已确定将实现该版本，其中 Safari Tech Preview 和 Chrome Canary 已实现。请继续阅读，了解新的内容。或者参阅<a href="#historysupport" target="_blank">历史记录和浏览器支持</a>，了解详细信息。</p>
<p>Shadow DOM 是四大网络组件标准之一：<a href="https://www.html5rocks.com/en/tutorials/webcomponents/template/" target="_blank">HTML 模板</a>、<a href="https://dom.spec.whatwg.org/#shadow-trees" target="_blank">Shadow DOM</a>、<a href="https://developers.google.com/web/fundamentals/getting-started/primers/customelements" target="_blank">自定义元素</a>以及 <a href="https://www.html5rocks.com/en/tutorials/webcomponents/imports/" target="_blank">HTML 导入</a>。</p>
<p>您无需编写使用 shadow DOM 的网络组件。但是如果您有编写，可充分利用其各种优势（CSS 作用域、DOM 封装和组合），并构建可重复使用的<a href="https://developers.google.com/web/fundamentals/getting-started/primers/customelements" target="_blank">自定义元素</a>，这些元素具有弹性、高度可配置且高度可重用。如果自定义元素是创建新 HTML（通过 JS API）的方式，shadow DOM 则是创建其 HTML 和 CSS 的方式。这两种 API 组合使用，通过独立的 HTML、CSS 和 JavaScript 来创建组件。</p>
<p>Shadow DOM 这款工具旨在构建基于组件的应用。因此，可为网络开发中的常见问题提供解决方案：</p>
<ul>
<li><strong>隔离 DOM</strong>：组件的 DOM 是独立的（例如，<code>document.querySelector()</code> 不会返回组件 shadow DOM 中的节点）。</li>
<li><strong>作用域 CSS</strong>：shadow DOM 内部定义的 CSS 在其作用域内。样式规则不会泄漏，页面样式也不会渗入。</li>
<li><strong>组合</strong>：为组件设计一个声明性、基于标记的 API。</li>
<li><strong>简化 CSS</strong> - 作用域 DOM 意味着您可以使用简单的 CSS 选择器，更通用的 id/类名称，而无需担心命名冲突。</li>
<li><strong>效率</strong> - 将应用看成是多个 DOM 块，而不是一个大的（全局性）页面。</li>
</ul>
<p>注：尽管您可以在网络组件之外利用 shadow DOM API 及其优势，这里我只列出一些基于自定义元素的示例。我将在所有示例中使用自定义元素 v1 API。</p>
<h4 id="demo"><code>fancy-tabs</code> 演示</h4>
<p>在整篇文章中，我将引用演示组件 (<code>&lt;fancy-tabs&gt;</code>) 以及其中的代码段。
如果您的浏览器支持 API，您可以看到下面的实时演示。
否则，请查看 </p>
<p><a href="https://gist.github.com/ebidel/2d2bb0cdec3f2a16cf519dbaa791ce1b" target="_blank">Github 上的完整源代码</a>。</p>
<figure>
  
  <figcaption>
    <a href="https://gist.github.com/ebidel/2d2bb0cdec3f2a16cf519dbaa791ce1b" target="_blank">
      在 Github 上查看源代码
    </a>
  </figcaption>
</figure>

<h2 id="what">什么是 shadow DOM？</h2>
<h4 id="sdbackground">DOM 相关背景</h4>
<p>HTML 因其易于使用的特点驱动着网络的发展。通过声明几个标记，即可在几秒内编写一个带有图文信息和结构的页面。
但是，HTML 自身的功能并不强大。
对于我们人类而言，理解基于文本语言很容易，但是机器需要更多帮助才能理解。
因此，文档对象模型 (DOM) 应运而生。</p>
<p>浏览器加载网页时会做一些很有趣的事情。其中之一就是它会将编写的 HTML 转变成活动文档。为理解页面的结构，浏览器通常会将 HTML（静态文本字符串）解析为数据模型（对象/节点）。浏览器通过创建一个节点树来保留 HTML 的层次结构：DOM。
DOM 很酷的一点在于它能够生动地展示您的页面。
与我们编写的静态 HTML 不同，浏览器生成的节点包含有属性、方法，而且最棒的是可通过程序进行操作！这就是为什么我们直接使用 JavaScript 即可创建 DOM 元素的原因：</p>
<pre><code>const header = document.createElement('header');<br />const h1 = document.createElement('h1');<br />h1.textContent = 'Hello world!';<br />header.appendChild(h1);<br />document.body.appendChild(header);<br /></code></pre>
<p>生成以下 HTML 标记：</p>
<pre><code>&lt;body&gt;<br />  &lt;header&gt;<br />    &lt;h1&gt;Hello DOM&lt;/h1&gt;<br />  &lt;/header&gt;<br />&lt;/body&gt;<br /></code></pre>
<p>一切都还不错。那么，<a href="https://glazkov.com/2011/01/14/what-the-heck-is-shadow-dom/" target="_blank">究竟什么是 <em>shadow DOM</em></a>？</p>
<h4 id="sddom">影子中的 DOM</h4>
<p>Shadow DOM 与普通 DOM 相同，但有两点区别：1) 创建/使用的方式；2) 与页面其他部分有关的行为方式。
通常，您创建 DOM 节点并将其附加至其他元素作为子项。
借助于 shadow DOM，您可以创建作用域 DOM 树，该 DOM 树附加至该元素上，但与其自身真正的子项分离开来。这一作用域子树称为<strong>影子树</strong>。被附着的元素称为<strong>影子宿主</strong>。
您在影子中添加的任何项均将成为宿主元素的本地项，包括 <code>&lt;style&gt;</code>。
这就是 shadow DOM 实现 CSS 样式作用域的方式。</p>
<h2 id="create">创建 shadow DOM</h2>
<p><strong>影子根</strong>是附加至“宿主”元素的文档片段。元素通过附加影子根来获取其 shadow DOM。
要为元素创建 shadow DOM，请调用 <code>element.attachShadow()</code>：</p>
<pre><code>const header = document.createElement('header');<br />const shadowRoot = header.attachShadow({mode: 'open'});<br />shadowRoot.innerHTML = '&lt;h1&gt;Hello Shadow DOM&lt;/h1&gt;'; // Could also use appendChild().<br /><br />// header.shadowRoot === shadowRoot<br />// shadowRoot.host === header<br /></code></pre>
<p>我现在使用 <code>.innerHTML</code> 来填充影子根，不过您也可使用其他 DOM API 来实现。
这就是网络。我们可自主选择。</p>
<p>规范<a href="http://w3c.github.io/webcomponents/spec/shadow/#h-methods" target="_blank">定义了元素列表</a>，这些元素无法托管影子树，
元素之所以在所选之列，其原因如下：</p>
<ul>
<li>
<p>浏览器已为该元素托管其自身的内部 shadow DOM（<code>&lt;textarea&gt;</code>、<code>&lt;input&gt;</code>）。</p>
</li>
<li>
<p>让元素托管 shadow DOM 毫无意义 (<code>&lt;img&gt;</code>)。</p>
</li>
</ul>
<p>例如，以下方法行不通：</p>
<pre><code>document.createElement('input').attachShadow({mode: 'open'});<br />// Error. `&lt;input&gt;` cannot host shadow dom.<br /></code></pre>
<h3 id="elements">为自定义元素创建 shadow DOM</h3>
<p>创建<a href="https://developers.google.com/web/fundamentals/getting-started/primers/customelements" target="_blank">自定义元素</a>时，Shadow DOM 尤其有用。使用 shadow DOM 来分隔元素的 HTML、CSS 和 JS，从而生成一个“网络组件”。</p>
<p><strong>例如</strong> - 自定义元素<strong>将 shadow DOM 附加至其自身</strong>，对其 DOM/CSS 进行封装：</p>
<pre><code>// Use custom elements API v1 to register a new HTML tag and define its JS behavior<br />// using an ES6 class. Every instance of &lt;fancy-tab&gt; will have this same prototype.<br />customElements.define('fancy-tabs', class extends HTMLElement {<br />  constructor() {<br />    super(); // always call super() first in the ctor.<br /><br />// Attach a shadow root to &lt;fancy-tabs&gt;.<br />    const shadowRoot = this.attachShadow({mode: 'open'});<br />    shadowRoot.innerHTML = `<br />      &lt;style&gt;#tabs { ... }&lt;/style&gt; &lt;!-- styles are scoped to fancy-tabs! --&gt;<br />      &lt;div id="tabs"&gt;...&lt;/div&gt;<br />      &lt;div id="panels"&gt;...&lt;/div&gt;<br />    `;<br />  }<br />  ...<br />});<br /></code></pre>
<p>这里有几个有趣的事情。首先，<code>&lt;fancy-tabs&gt;</code> 实例创建后，自定义元素<strong>创建其自身的 shadow DOM</strong>。这在 <code>constructor()</code> 中完成。其次，因为我们要创建一个影子根，因此 <code>&lt;style&gt;</code> 中的 CSS 规则将作用域仅限于 <code>&lt;fancy-tabs&gt;</code>。</p>
<p>注：尝试运行该示例时，您可能会注意到没有任何渲染。
用户的标记似乎消失了！这是因为<strong>元素的 shadow DOM 代替其子项被渲染</strong>。
如果想要显示子项，您需要告诉浏览器在哪里进行渲染，具体做法是在您的 shadow DOM 中添加 <a href="#slots" target="_blank"><code>&lt;slot&gt;</code> 元素</a>。</p>
<p><a href="#composition_slot" target="_blank">之后</a>将会提供相关更多内容。</p>
<h2 id="composition_slot">组合和 slot</h2>
<p>组合是 shadow DOM 最难理解的功能之一，但可以说是最重要的功能。</p>
<p>在网络开发世界中，组合是指我们如何使用 HTML 来通过声明构建应用。
不同的构建块（<code>&lt;div&gt;</code>、<code>&lt;header&gt;</code>、<code>&lt;form&gt;</code>、<code>&lt;input&gt;</code>）共同构成应用。
某些标记甚至还相互合作。
组合是 <code>&lt;select&gt;</code>、<code>&lt;details&gt;</code>、<code>&lt;form&gt;</code> 和 <code>&lt;video&gt;</code> 等原生元素如此灵活的原因所在。
这些标记中的每个标记接受特定的 HTML 作为子项，并且加以特殊处理。
例如，<code>&lt;select&gt;</code> 知道如何将 <code>&lt;option&gt;</code> 和 <code>&lt;optgroup&gt;</code> 渲染为下拉和多选小部件。<code>&lt;details&gt;</code> 元素将 <code>&lt;summary&gt;</code> 渲染为可展开的箭头。
甚至 <code>&lt;video&gt;</code> 知道如何处理特定的子项：<code>&lt;source&gt;</code> 元素未进行渲染，但却会影响视频的行为。多么神奇！</p>
<h3 id="lightdom">术语：light DOM 与 shadow DOM</h3>
<p>Shadow DOM 组合引入了大量与网络开发相关的新的基础知识。
为避免陷入迷茫，我们先标准化一些术语，这样我们就能讲同样的行话。</p>
<p><strong>Light DOM</strong></p>
<p>组件用户编写的标记。该 DOM 不在组件 shadow DOM 之内。
它是元素实际的子项。</p>
<pre><code>&lt;button is="better-button"&gt;<br />  &lt;!-- the image and span are better-button's light DOM --&gt;<br />  &lt;img src="gear.svg" slot="icon"&gt;<br />  &lt;span&gt;Settings&lt;/span&gt;<br />&lt;/button&gt;<br /></code></pre>
<p><strong>Shadow DOM</strong></p>
<p>该 DOM 是由组件的作者编写。Shadow DOM 对于组件而言是本地的，它定义内部结构、作用域 CSS 并封装实现详情。它还可定义如何渲染由组件使用者编写的标记。</p>
<pre><code>#shadow-root<br />  &lt;style&gt;...&lt;/style&gt;<br />  &lt;slot name="icon"&gt;&lt;/slot&gt;<br />  &lt;span id="wrapper"&gt;<br />    &lt;slot&gt;Button&lt;/slot&gt;<br />  &lt;/span&gt;<br /></code></pre>
<p><strong>扁平的 DOM 树</strong></p>
<p>浏览器将用户的 light DOM 分布到您的 shadow DOM 的结果，对最终产品进行渲染。
扁平树是指您在 DevTools 中最终看到的树以及在页面上渲染的对象。</p>
<pre><code>&lt;button is="better-button"&gt;<br />  #shadow-root<br />    &lt;style&gt;...&lt;/style&gt;<br />    &lt;slot name="icon"&gt;<br />      &lt;img src="gear.svg" slot="icon"&gt;<br />    &lt;/slot&gt;<br />    &lt;slot&gt;<br />      &lt;span&gt;Settings&lt;/span&gt;<br />    &lt;/slot&gt;<br />&lt;/button&gt;<br /></code></pre>
<h3 id="slots">&lt;slot&gt; 元素</h3>
<p>Shadow DOM 使用 <code>&lt;slot&gt;</code> 元素将不同的 DOM 树组合在一起。<strong>Slot 是组件内部的占位符，用户_可以_使用自己的标记来填充</strong>。</p>
<p>通过定义一个或多个 slot，您可将外部标记引入到组件的 shadow DOM 中进行渲染。
这相当于您在说“在此处渲染用户的标记”。</p>
<p>注：Slot 是为网络组件创建“声明性 API”的一种方法。它们混入到用户的 DOM 中，帮助对整个组件进行渲染，从而<strong>将不同的 DOM 树组合在一起</strong>。</p>
<p>如果 <code>&lt;slot&gt;</code> 引入了元素，则这些元素可“跨越” shadow DOM 的边界。
这些元素称为<strong>分布式节点</strong>。从概念上来看，分布式节点似乎有点奇怪。
Slot 实际上并不移动 DOM；它们在 shadow DOM 内部的其他位置进行渲染。</p>
<p>组件可在其 shadow DOM 中定义零个或多个 slot。Slot 可以为空，或者提供回退内容。
如果用户不提供 <a href="#lightdom" target="_blank">light DOM</a> 内容，slot 将对其备用内容进行渲染。</p>
<pre><code>&lt;!-- Default slot. If there's more than one default slot, the first is used. --&gt;<br />&lt;slot&gt;&lt;/slot&gt;<br /><br />&lt;slot&gt;Fancy button&lt;/slot&gt; &lt;!-- default slot with fallback content --&gt;<br /><br />&lt;slot&gt; &lt;!-- default slot entire DOM tree as fallback --&gt;<br />  &lt;h2&gt;Title&lt;/h2&gt;<br />  &lt;summary&gt;Description text&lt;/summary&gt;<br />&lt;/slot&gt;<br /></code></pre>
<p>您还可以创建<strong>已命名 slot</strong>。已命名 slot 是 shadow DOM 中用户可通过名称引用的特定槽。</p>
<p><strong>例如</strong> - <code>&lt;fancy-tabs&gt;</code> shadow DOM 中的已命名 slot：</p>
<pre><code>#shadow-root<br />  &lt;div id="tabs"&gt;<br />    &lt;slot id="tabsSlot" name="title"&gt;&lt;/slot&gt;<br />  &lt;/div&gt;<br />  &lt;div id="panels"&gt;<br />    &lt;slot id="panelsSlot"&gt;&lt;/slot&gt;<br />  &lt;/div&gt;<br /></code></pre>
<p>组件用户对 <code>&lt;fancy-tabs&gt;</code> 的声明类似于：</p>
<pre><code>&lt;fancy-tabs&gt;<br />  &lt;button slot="title"&gt;Title&lt;/button&gt;<br />  &lt;button slot="title" selected&gt;Title 2&lt;/button&gt;<br />  &lt;button slot="title"&gt;Title 3&lt;/button&gt;<br />  &lt;section&gt;content panel 1&lt;/section&gt;<br />  &lt;section&gt;content panel 2&lt;/section&gt;<br />  &lt;section&gt;content panel 3&lt;/section&gt;<br />&lt;/fancy-tabs&gt;<br /><br />&lt;!-- Using &lt;h2&gt;'s and changing the ordering would also work! --&gt;<br />&lt;fancy-tabs&gt;<br />  &lt;h2 slot="title"&gt;Title&lt;/h2&gt;<br />  &lt;section&gt;content panel 1&lt;/section&gt;<br />  &lt;h2 slot="title" selected&gt;Title 2&lt;/h2&gt;<br />  &lt;section&gt;content panel 2&lt;/section&gt;<br />  &lt;h2 slot="title"&gt;Title 3&lt;/h2&gt;<br />  &lt;section&gt;content panel 3&lt;/section&gt;<br />&lt;/fancy-tabs&gt;<br /></code></pre>
<p>而且如果您很好奇，您会发现扁平树看起来类似于：</p>
<pre><code>&lt;fancy-tabs&gt;<br />  #shadow-root<br />    &lt;div id="tabs"&gt;<br />      &lt;slot id="tabsSlot" name="title"&gt;<br />        &lt;button slot="title"&gt;Title&lt;/button&gt;<br />        &lt;button slot="title" selected&gt;Title 2&lt;/button&gt;<br />        &lt;button slot="title"&gt;Title 3&lt;/button&gt;<br />      &lt;/slot&gt;<br />    &lt;/div&gt;<br />    &lt;div id="panels"&gt;<br />      &lt;slot id="panelsSlot"&gt;<br />        &lt;section&gt;content panel 1&lt;/section&gt;<br />        &lt;section&gt;content panel 2&lt;/section&gt;<br />        &lt;section&gt;content panel 3&lt;/section&gt;<br />      &lt;/slot&gt;<br />    &lt;/div&gt;<br />&lt;/fancy-tabs&gt;<br /></code></pre>
<p>注意，我们的组件可处理不同的配置，但是扁平的 DOM 树保持不变。
我们还可以从 <code>&lt;button&gt;</code> 切换到 <code>&lt;h2&gt;</code>。
编写此组件的目的在于处理不同类型的子项 - 如同 <code>&lt;select&gt;</code> 一样。</p>

<p>有多种方式可设定网络组件的样式。使用 shadow DOM 的组件可通过主页来设定样式，定义其自己的样式或提供钩子（以 <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables" target="_blank">CSS 自定义属性</a>的形式）让用户替换默认值。</p>
<h3 id="host">组件定义的样式</h3>
<p>请记住，shadow DOM 最有用的功能是<strong>作用域 CSS</strong>：</p>
<ul>
<li>外部页面中的 CSS 选择器不应用于组件内部。</li>
<li>内部定义的样式也不会渗出。它们的作用域仅限于宿主元素。</li>
</ul>
<p><strong>shadow DOM 内部使用的 CSS 选择器在本地应用于组件。</strong>。实践中，这意味着我们可再次使用一般的 id/类名称，而无需担心在页面其他位置有冲突。</p>
<p>最佳做法是在 Shadow DOM 内使用更简单的 CSS 选择器。
它们在性能上也不错。</p>
<p><strong>例如</strong> - 在影子根中定义的样式是本地的</p>
<pre><code>#shadow-root<br />  &lt;style&gt;<br />    #panels {<br />      box-shadow: 0 2px 2px rgba(0, 0, 0, .3);<br />      background: white;<br />      ...<br />    }<br />    #tabs {<br />      display: inline-flex;<br />      ...<br />    }<br />  &lt;/style&gt;<br />  &lt;div id="tabs"&gt;<br />    ...<br />  &lt;/div&gt;<br />  &lt;div id="panels"&gt;<br />    ...<br />  &lt;/div&gt;<br /></code></pre>
<p>样式表的作用域也仅限于影子树：</p>
<pre><code>#shadow-root<br />  &lt;!-- Available in Chrome 54+ --&gt;<br />  &lt;!-- WebKit bug: https://bugs.webkit.org/show_bug.cgi?id=160683 --&gt;<br />  &lt;link rel="stylesheet" href="styles.css"&gt;<br />  &lt;div id="tabs"&gt;<br />    ...<br />  &lt;/div&gt;<br />  &lt;div id="panels"&gt;<br />    ...<br />  &lt;/div&gt;<br /></code></pre>
<p>您可能想知道在您添加 <code>multiple</code> 属性时，<code>&lt;select&gt;</code> 元素是如何渲染多选小部件（而不是下拉工具）的：</p>
<p><code>&lt;select&gt;</code> 可基于您声明的属性为_自身_设定不同的样式。
网络组件也可通过 <code>:host</code> 选择器对自身进行样式设定。</p>
<p><strong>例如</strong> - 组件为自身设定样式</p>
<pre><code>&lt;style&gt;<br />:host {<br />  display: block; /* by default, custom elements are display: inline */<br />  contain: content; /* CSS containment FTW. */<br />}<br />&lt;/style&gt;<br /></code></pre>
<p>使用 <code>:host</code> 的一个问题是，父页面中的规则较之在元素中定义的 <code>:host</code> 规则具有更高的特异性。
也就是说，外部样式优先。这可让用户从外部替换您的顶级样式。
此外，<code>:host</code> 仅在影子根范围内起作用，因此无法在 shadow DOM 之外使用。</p>
<p>如果 <code>:host(&lt;selector&gt;)</code> 的函数形式与 <code>&lt;selector&gt;</code> 匹配，您可以指定宿主。
对于您的组件而言，这是一个很好的方法，它可让您基于宿主将对用户互动或状态的反应行为进行封装，或对内部节点进行样式设定。</p>
<pre><code>&lt;style&gt;<br />:host {<br />  opacity: 0.4;<br />  will-change: opacity;<br />  transition: opacity 300ms ease-in-out;<br />}<br />:host(:hover) {<br />  opacity: 1;<br />}<br />:host([disabled]) { /* style when host has disabled attribute. */<br />  background: grey;<br />  pointer-events: none;<br />  opacity: 0.4;<br />}<br />:host(.blue) {<br />  color: blue; /* color host when it has class="blue" */<br />}<br />:host(.pink) &gt; #tabs {<br />  color: pink; /* color internal #tabs node when host has class="pink". */<br />}<br />&lt;/style&gt;<br /></code></pre>
<h3 id="contextstyling">基于情境设定样式</h3>
<p>如果 <code>:host-context(&lt;selector&gt;)</code> 或其任意父级与 <code>&lt;selector&gt;</code> 匹配，它将与组件匹配。
一个常见用途是根据组件的环境进行主题化。
例如，很多人都通过将类应用到 <code>&lt;html&gt;</code> 或 <code>&lt;body&gt;</code> 进行主题化：</p>
<pre><code>&lt;body class="darktheme"&gt;<br />  &lt;fancy-tabs&gt;<br />    ...<br />  &lt;/fancy-tabs&gt;<br />&lt;/body&gt;<br /></code></pre>
<p>如果 <code>:host-context(.darktheme)</code> 为 <code>.darktheme</code> 的子级，它将对 <code>&lt;fancy-tabs&gt;</code> 进行样式化：</p>
<pre><code>:host-context(.darktheme) {<br />  color: white;<br />  background: black;<br />}<br /></code></pre>
<p><code>:host-context()</code> 对于主题化很有用，但更好的方法是<a href="#stylehooks" target="_blank">使用 CSS 自定义属性创建样式钩子</a>。</p>
<h3 id="stylinglightdom">为分布式节点设定样式</h3>
<p><code>::slotted(&lt;compound-selector&gt;)</code> 与分布到 <code>&lt;slot&gt;</code> 中的节点匹配。</p>
<p>比如说我们已创建了一个 name badge 组件：</p>
<pre><code>&lt;name-badge&gt;<br />  &lt;h2&gt;Eric Bidelman&lt;/h2&gt;<br />  &lt;span class="title"&gt;<br />    Digital Jedi, &lt;span class="company"&gt;Google&lt;/span&gt;<br />  &lt;/span&gt;<br />&lt;/name-badge&gt;<br /></code></pre>
<p>组件的 shadow DOM 可为用户的 <code>&lt;h2&gt;</code> 和 <code>.title</code> 设定样式：</p>
<pre><code>&lt;style&gt;<br />::slotted(h2) {<br />  margin: 0;<br />  font-weight: 300;<br />  color: red;<br />}<br />::slotted(.title) {<br />   color: orange;<br />}<br />/* DOESN'T WORK (can only select top-level nodes).<br />::slotted(.company),<br />::slotted(.title .company) {<br />  text-transform: uppercase;<br />}<br />*/<br />&lt;/style&gt;<br />&lt;slot&gt;&lt;/slot&gt;<br /></code></pre>
<p>如果您还记得前面的内容，就知道 <code>&lt;slot&gt;</code> 不会移动用户的 light DOM。节点分布于 <code>&lt;slot&gt;</code> 中后，<code>&lt;slot&gt;</code> 会对其 DOM 进行渲染，但节点实际上留在原处。<strong>分布之前已应用的样式在分布后仍继续应用</strong>。
但是，light DOM 分布后，它_可以_采用其他样式（通过 shadow DOM 定义的样式）。</p>
<p>另一个来自 <code>&lt;fancy-tabs&gt;</code> 的更深入的例子：</p>
<pre><code>const shadowRoot = this.attachShadow({mode: 'open'});<br />shadowRoot.innerHTML = `<br />  &lt;style&gt;<br />    #panels {<br />      box-shadow: 0 2px 2px rgba(0, 0, 0, .3);<br />      background: white;<br />      border-radius: 3px;<br />      padding: 16px;<br />      height: 250px;<br />      overflow: auto;<br />    }<br />    #tabs {<br />      display: inline-flex;<br />      -webkit-user-select: none;<br />      user-select: none;<br />    }<br />    #tabsSlot::slotted(*) {<br />      font: 400 16px/22px 'Roboto';<br />      padding: 16px 8px;<br />      ...<br />    }<br />    #tabsSlot::slotted([aria-selected="true"]) {<br />      font-weight: 600;<br />      background: white;<br />      box-shadow: none;<br />    }<br />    #panelsSlot::slotted([aria-hidden="true"]) {<br />      display: none;<br />    }<br />  &lt;/style&gt;<br />  &lt;div id="tabs"&gt;<br />    &lt;slot id="tabsSlot" name="title"&gt;&lt;/slot&gt;<br />  &lt;/div&gt;<br />  &lt;div id="panels"&gt;<br />    &lt;slot id="panelsSlot"&gt;&lt;/slot&gt;<br />  &lt;/div&gt;<br />`;<br /></code></pre>
<p>在该示例中，有两个 slot：用于标签标题的命名 slot，以及用于标签内容的命名 slot。
用户选择一个标签后，我们会对其选择进行加粗并在面板上显示。
这是通过选择具有 <code>selected</code> 属性的分布式节点来实现的。
自定义元素的 JS（此处未显示）会在合适的时间添加此属性。</p>
<h3 id="stylefromoutside">从外部为组件设定样式</h3>
<p>有几种方法可从外部为组件设定样式：最简单的方法是使用标记名称作为选择器：</p>
<pre><code>fancy-tabs {<br />  width: 500px;<br />  color: red; /* Note: inheritable CSS properties pierce the shadow DOM boundary. */<br />}<br />fancy-tabs:hover {<br />  box-shadow: 0 3px 3px #ccc;<br />}<br /></code></pre>
<p><strong>外部样式总是优先于在 shadow DOM 中定义的样式</strong>。例如，如果用户编写选择器 <code>fancy-tabs { width: 500px; }</code>，它将优先于组件的规则：<code>:host { width: 650px;}</code>。</p>
<p>为组件自身设定样式只能到此为止。但是如果您想要为组件内容设定样式，会发生什么情况呢？
对于这种情况，我们需要 CSS 自定义属性。</p>
<h4 id="stylehooks">使用 CSS 自定义属性创建样式钩子</h4>
<p>如果组件的作者通过 <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables" target="_blank">CSS 自定义属性</a>提供样式钩子，则用户可调整内部样式。
从概念上看，这与 <code>&lt;slot&gt;</code> 类似。
您创建“样式占位符”以便用户进行替换：</p>
<p><strong>例如</strong> - <code>&lt;fancy-tabs&gt;</code> 可让用户替换背景颜色：</p>
<pre><code>&lt;!-- main page --&gt;<br />&lt;style&gt;<br />  fancy-tabs {<br />    margin-bottom: 32px;<br />    --fancy-tabs-bg: black;<br />  }<br />&lt;/style&gt;<br />&lt;fancy-tabs background&gt;...&lt;/fancy-tabs&gt;<br /></code></pre>
<p>在其 shadow DOM 内部：</p>
<pre><code>:host([background]) {<br />  background: var(--fancy-tabs-bg, #9E9E9E);<br />  border-radius: 10px;<br />  padding: 10px;<br />}<br /></code></pre>
<p>在本例中，该组件将使用 <code>black</code> 作为背景值，因为用户指定了该值。
否则，背景颜色将采用默认值 <code>#9E9E9E</code>。</p>
<p>注：作为组件的作者，您负责让开发者了解他们所能使用的 CSS 自定义属性。
将其看成是组件公共接口的一部分。
确保将样式钩子记录下来！</p>

<h3 id="closed">创建闭合影子根（应避免）</h3>
<p>shadow DOM 的另一情况称为“闭合”模式。创建闭合影子树后，在 JavaScript 外部无法访问组件的内部 DOM。这与 <code>&lt;video&gt;</code> 等原生元素工作方式类似。JavaScript 无法访问 <code>&lt;video&gt;</code> 的 shadow DOM，因为浏览器使用闭合模式的影子根来实现。</p>
<p><strong>例如</strong> - 创建一个闭合的影子树：</p>
<pre><code>const div = document.createElement('div');<br />const shadowRoot = div.attachShadow({mode: 'closed'}); // close shadow tree<br />// div.shadowRoot === null<br />// shadowRoot.host === div<br /></code></pre>
<p>其他 API 也会受到闭合模式的影响：</p>
<ul>
<li><code>Element.assignedSlot</code> / <code>TextNode.assignedSlot</code> 返回 <code>null</code></li>
<li><code>Event.composedPath()</code>，用于与 shadow DOM 内部元素关联的事件，返回 []</li>
</ul>
<p>注：闭合的影子树不是非常有用。有些开发者将闭合模式视为一项人工安全功能。
但是让我们澄清一点，它并<strong>不是</strong>一项安全功能。
闭合模式只是简单地阻止外部 JS 深入到元素的内部 DOM。</p>
<p>任何时候都不要使用 <code>{mode: 'closed'}</code> 来创建网络组件，以下是我总结的几点原因：</p>
<ol>
<li>
<p>人为的安全功能。没有什么能够阻止攻击者入侵 <code>Element.prototype.attachShadow</code>。</p>
</li>
<li>
<p>闭合模式<strong>阻止自定义元素代码访问其自己的 shadow DOM</strong>。
这根本没用。相反，如果您想要使用如 <code>querySelector()</code> 等元素，您必须存放影子根以备日后参考。
这就与闭合模式的最初目的完全背道而驰！</p>
<pre><code>customElements.define('x-element', class extends HTMLElement {<br />  constructor() {<br />    super(); // always call super() first in the ctor.<br />    this._shadowRoot = this.attachShadow({mode: 'closed'});<br />    this._shadowRoot.innerHTML = '&lt;div class="wrapper"&gt;&lt;/div&gt;';<br />  }<br />  connectedCallback() {<br />    // When creating closed shadow trees, you'll need to stash the shadow root<br />    // for later if you want to use it again. Kinda pointless.<br />    const wrapper = this._shadowRoot.querySelector('.wrapper');<br />  }<br />  ...<br />});<br /></code></pre>
</li>
<li>
<p><strong>闭合模式使组件对最终用户的灵活性大为降低</strong>。在构建网络组件时，您有时可能会忘记添加某项功能、某个配置选项以及用户所需的用例。一个很常见的例子是忘记为内部节点添加足够的样式钩子。在闭合模式下，用户无法替换默认值并调整样式。
如果能访问组件的内容，这将超级有用。最终，如果用户得不到他们想要的，他们就会舍弃您的组件，寻找其他组件或创建自己的组件:(</p>
</li>
</ol>
<h3 id="workwithslots">在 JS 中使用 slot</h3>
<p>shadow DOM API 提供了使用 slot 和分布式节点的实用程序。
这些实用程序在编写自定义元素时迟早派得上用场。</p>
<h4 id="slotchange">slotchange 事件</h4>
<p>当 slot 的分布式节点发生变化时，<code>slotchange</code> 事件会触发。例如，当用户从 light DOM 中添加/移除子项时。</p>
<pre><code>const slot = this.shadowRoot.querySelector('#slot');<br />slot.addEventListener('slotchange', e =&gt; {<br />  console.log('light dom children changed!');<br />});<br /></code></pre>
<p>注：当组件的实例首次初始化时，<code>slotchange</code> 不触发。</p>
<p>如要监控 light DOM 其他类型的变化，您可以在元素的构造函数中设置 <a href="https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver" target="_blank"><code>MutationObserver</code></a>。</p>
<h4 id="slotnodes">哪些元素在 slot 中进行渲染？</h4>
<p>有时候，了解哪些元素与 slot 相关联非常有用。调用 <code>slot.assignedNodes()</code> 可查看 slot 正在渲染哪些元素。
<code>{flatten: true}</code> 选项将返回 slot 的备用内容（前提是没有分布任何节点）。</p>
<p>举个例子，比如您的 shadow DOM 看起来像这样：</p>
<pre><code>&lt;slot&gt;&lt;b&gt;fallback content&lt;/b&gt;&lt;/slot&gt;<br /></code></pre>
<div><table>
  <thead><tr><th>用法</th><th>调用</th><th>结果</th></tr></thead>
  <tbody><tr>
    <td>&lt;button is="better-button"&gt;My button&lt;/button&gt;</td>
    <td><code>slot.assignedNodes();</code></td>
    <td><code>[text]</code></td>
  </tr>
  <tr>
    <td>&lt;button is="better-button"&gt;&lt;/button&gt;</td>
    <td><code>slot.assignedNodes();</code></td>
    <td><code>[]</code></td>
  </tr>
  <tr>
    <td>&lt;button is="better-button"&gt;&lt;/button&gt;</td>
    <td><code>slot.assignedNodes({flatten: true});</code></td>
    <td><code>[&lt;b&gt;fallback content&lt;/b&gt;]</code></td>
  </tr>
</tbody></table></div>

<h4 id="assignedslot">元素分配给哪个 Slot？</h4>
<p>这个反向问题也是可以回答的。<code>element.assignedSlot</code> 将告诉您元素分配给哪个组件 slot。</p>
<h3 id="events">Shadow DOM 事件模型</h3>
<p>当事件从 shadow DOM 中触发时，其目标将会调整为维持 shadow DOM 提供的封装。
也就是说，事件的目标重新进行了设定，因此这些事件看起来像是来自组件，而不是来自 shadow DOM 中的内部元素。</p>
<p>有些事件甚至不会从 shadow DOM 中传播出去。</p>
<p><strong>确实</strong>会跨过影子边界的事件有：</p>
<ul>
<li>聚焦事件：<code>blur</code>、<code>focus</code>、<code>focusin</code>、<code>focusout</code></li>
<li>鼠标事件：<code>click</code>、<code>dblclick</code>、<code>mousedown</code>、<code>mouseenter</code>、<code>mousemove</code>，等等</li>
<li>滚轮事件：<code>wheel</code></li>
<li>输入事件：<code>beforeinput</code>、<code>input</code></li>
<li>键盘事件：<code>keydown</code>、<code>keyup</code></li>
<li>组合事件：<code>compositionstart</code>、<code>compositionupdate</code>、<code>compositionend</code></li>
<li>拖放事件：<code>dragstart</code>、<code>drag</code>、<code>dragend</code>、<code>drop</code>，等等</li>
</ul>
<p><strong>提示</strong></p>
<p>如果影子树处于打开状态，调用 <code>event.composedPath()</code> 将返回事件经过的一组节点。</p>
<h4 id="customevents">使用自定义事件</h4>
<p>通过影子树中内部节点触发的自定义 DOM 事件不会超出影子边界，除非事件是使用 <code>composed: true</code> 标记创建的：</p>
<pre><code>// Inside &lt;fancy-tab&gt; custom element class definition:<br />selectTab() {<br />  const tabs = this.shadowRoot.querySelector('#tabs');<br />  tabs.dispatchEvent(new Event('tab-select', {bubbles: true, composed: true}));<br />}<br /></code></pre>
<p>如果是 <code>composed: false</code>（默认值），用户无法侦听到影子根之外的事件。</p>
<pre><code>&lt;fancy-tabs&gt;&lt;/fancy-tabs&gt;<br />&lt;script&gt;<br />  const tabs = document.querySelector('fancy-tabs');<br />  tabs.addEventListener('tab-select', e =&gt; {<br />    // won't fire if `tab-select` wasn't created with `composed: true`.<br />  });<br />&lt;/script&gt;<br /></code></pre>

<p>如果您从 <a href="#events" target="_blank">shadow DOM 的事件模型</a>重新调用，将对在 shadow DOM 内部触发的事件进行调整，使其看起来来自宿主元素。例如，我们假设您点击某个影子根内部的 <code>&lt;input&gt;</code>：</p>
<pre><code>&lt;x-focus&gt;<br />  #shadow-root<br />    &lt;input type="text" placeholder="Input inside shadow dom"&gt;<br /></code></pre>
<p><code>focus</code> 事件看起来来自 <code>&lt;x-focus&gt;</code>，而不是 <code>&lt;input&gt;</code>。
与此类似，<code>document.activeElement</code> 将是 <code>&lt;x-focus&gt;</code>。如果影子根使用 <code>mode:'open'</code> 创建（请参阅<a href="#closed" target="_blank">闭合模式</a>），您还可以访问获得焦点的外部节点：</p>
<pre><code>document.activeElement.shadowRoot.activeElement // only works with open mode.<br /></code></pre>
<p>如果存在多个级别的 shadow DOM（即自定义元素位于另一个自定义元素中），您需要以递归方式深入影子根以查找 <code>activeElement</code>：</p>
<pre><code>function deepActiveElement() {<br />  let a = document.activeElement;<br />  while (a && a.shadowRoot && a.shadowRoot.activeElement) {<br />    a = a.shadowRoot.activeElement;<br />  }<br />  return a;<br />}<br /></code></pre>
<p>焦点的另一个选项是 <code>delegatesFocus: true</code> 选项，它可以将元素的焦点行为拓展到影子树内：</p>
<ul>
<li>如果您点击 shadow DOM 内的某个节点，且该节点不是一个可聚焦区域，那么第一个可聚焦区域将成为焦点。</li>
<li>当 shadow DOM 内的节点获得焦点时，除了聚焦的元素外，<code>:focus</code> 还会应用到宿主。</li>
</ul>
<p><strong>示例</strong> - <code>delegatesFocus: true</code> 如何更改焦点行为</p>
<pre><code>&lt;style&gt;<br />  :focus {<br />    outline: 2px solid red;<br />  }<br />&lt;/style&gt;<br /><br />&lt;x-focus&gt;&lt;/x-focus&gt;<br /><br />&lt;script&gt;<br />customElements.define('x-focus', class extends HTMLElement {<br />  constructor() {<br />    super(); // always call super() first in the ctor.<br /><br />const root = this.attachShadow({mode: 'open', delegatesFocus: true});<br />    root.innerHTML = `<br />      &lt;style&gt;<br />        :host {<br />          display: flex;<br />          border: 1px dotted black;<br />          padding: 16px;<br />        }<br />        :focus {<br />          outline: 2px solid blue;<br />        }<br />      &lt;/style&gt;<br />      &lt;div&gt;Clickable Shadow DOM text&lt;/div&gt;<br />      &lt;input type="text" placeholder="Input inside shadow dom"&gt;`;<br /><br />// Know the focused element inside shadow DOM:<br />    this.addEventListener('focus', function(e) {<br />      console.log('Active element (inside shadow dom):',<br />                  this.shadowRoot.activeElement);<br />    });<br />  }<br />});<br />&lt;/script&gt;<br /></code></pre>
<p><strong>结果</strong></p>
<p><div class="readableLargeImageContainer"><img src="https://developers.google.com/web/fundamentals/web-components/imgs/delegateFocusTrue.png" /></div></p>
<p>上面是 <code>&lt;x-focus&gt;</code> 获得焦点（用户点击、点按和 <code>focus()</code> 等）、点击“Clickable Shadow DOM text”或内部 <code>&lt;input&gt;</code> 获得焦点（包括 <code>autofocus</code>）时的结果。</p>
<p>如果是设置 <code>delegatesFocus: false</code>，下面将是您看到的结果：</p>
<figure>
  <div class="readableLargeImageContainer"><img src="https://developers.google.com/web/fundamentals/web-components/imgs/delegateFocusFalse.png" /></div>
  <figcaption>
    <code>delegatesFocus: false</code> 和内部  <code>&lt;input&gt;</code> 获得焦点。
  </figcaption>
</figure>

<figure>
  <div class="readableLargeImageContainer"><img src="https://developers.google.com/web/fundamentals/web-components/imgs/delegateFocusFalseFocus.png" /></div>
  <figcaption>
    <code>delegatesFocus: false</code> 和  <code>&lt;x-focus&gt;</code> 获得焦点（例如， <code>tabindex="0"</code>）。
  </figcaption>
</figure>

<figure>
  <div class="readableLargeImageContainer"><img src="https://developers.google.com/web/fundamentals/web-components/imgs/delegateFocusNothing.png" /></div>
  <figcaption>
    <code>delegatesFocus: false</code> 并且点击“Clickable Shadow DOM text”（或点击元素 shadow DOM 内的其他空白区域）。
  </figcaption>
</figure>

<h2 id="tricks">提示与技巧</h2>
<p>这些年，我学到了一些关于编写网络组件的技巧。我觉得这些技巧对于编写组件和调试 shadow DOM 会比较有用。</p>
<h3 id="containment">使用 CSS 组件</h3>
<p>通常，网络组件的布局/样式/绘制相当独立。在 <code>:host</code> 中使用 <a href="https://developers.google.com/web/updates/2016/06/css-containment" target="_blank">CSS containment</a> 可获得更好性能：</p>
<pre><code>&lt;style&gt;<br />:host {<br />  display: block;<br />  contain: content; /* Boom. CSS containment FTW. */<br />}<br />&lt;/style&gt;<br /></code></pre>
<h3 id="reset">重置可继承样式</h3>
<p>可继承样式（<code>background</code>、<code>color</code>、<code>font</code> 以及 <code>line-height</code> 等）可在 shadow DOM 中继续继承。
也就是说，默认情况下它们会突破 shadow DOM 边界。
如果您想从头开始，可在它们超出影子边界时，使用 <code>all: initial;</code> 将可继承样式重置为初始值。</p>
<pre><code>&lt;style&gt;<br />  div {<br />    padding: 10px;<br />    background: red;<br />    font-size: 25px;<br />    text-transform: uppercase;<br />    color: white;<br />  }<br />&lt;/style&gt;<br /><br />&lt;div&gt;<br />  &lt;p&gt;I'm outside the element (big/white)&lt;/p&gt;<br />  &lt;my-element&gt;Light DOM content is also affected.&lt;/my-element&gt;<br />  &lt;p&gt;I'm outside the element (big/white)&lt;/p&gt;<br />&lt;/div&gt;<br /><br />&lt;script&gt;<br />const el = document.querySelector('my-element');<br />el.attachShadow({mode: 'open'}).innerHTML = `<br />  &lt;style&gt;<br />    :host {<br />      all: initial; /* 1st rule so subsequent properties are reset. */<br />      display: block;<br />      background: white;<br />    }<br />  &lt;/style&gt;<br />  &lt;p&gt;my-element: all CSS properties are reset to their<br />     initial value using &lt;code&gt;all: initial&lt;/code&gt;.&lt;/p&gt;<br />  &lt;slot&gt;&lt;/slot&gt;<br />`;<br />&lt;/script&gt;<br /></code></pre>

<h3 id="findall">查找页面所使用的所有自定义元素</h3>
<p>有时，查找页面所使用的自定义元素非常有用。为此，您需要递归地遍历页面所使用的所有元素的 shadow DOM。</p>
<pre><code>const allCustomElements = [];<br /><br />function isCustomElement(el) {<br />  const isAttr = el.getAttribute('is');<br />  // Check for &lt;super-button&gt; and &lt;button is="super-button"&gt;.<br />  return el.localName.includes('-') || isAttr && isAttr.includes('-');<br />}<br /><br />function findAllCustomElements(nodes) {<br />  for (let i = 0, el; el = nodes[i]; ++i) {<br />    if (isCustomElement(el)) {<br />      allCustomElements.push(el);<br />    }<br />    // If the element has shadow DOM, dig deeper.<br />    if (el.shadowRoot) {<br />      findAllCustomElements(el.shadowRoot.querySelectorAll('*'));<br />    }<br />  }<br />}<br /><br />findAllCustomElements(document.querySelectorAll('*'));<br /></code></pre>
<h3 id="fromtemplate">使用 &lt;template&gt; 创建元素</h3>
<p>我们不是使用 <code>.innerHTML</code> 来填充影子根，而是使用一个声明性 <code>&lt;template&gt;</code>。
模板是用于声明网络组件结构的理想占位符。</p>
<p>具体请参见<a href="https://developers.google.com/web/fundamentals/getting-started/primers/customelements" target="_blank">“自定义元素：构建可重复使用的网络组件”</a>中的示例。</p>
<h2 id="historysupport">历史记录和浏览器支持</h2>
<p>如果最近几年您一直在关注网络组件，您会发现有一段时间 Chrome 35+/Opera 随附的是旧版本 shadow DOM。Blink 将继续在一段时间内同时支持新旧两种版本。
v0 规范提供了创建影子根的不同方法（<code>element.createShadowRoot</code>，而不是 v1 的 <code>element.attachShadow</code>）。
调用旧方法仍可通过 v0 语法来创建影子根，因此现有的 v0 代码不会出错。</p>
<p>如果您想了解旧版 v0 规范，可查看 html5rocks 文章：<a href="https://www.html5rocks.com/en/tutorials/webcomponents/shadowdom/" target="_blank">1</a>、<a href="https://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-201/" target="_blank">2</a>、<a href="https://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-301/" target="_blank">3</a>。<a href="http://hayato.io/2016/shadowdomv1/" target="_blank">shadow DOM v0 与 v1 的差异</a>中也提供了大量的二者比较信息。</p>
<h3 id="support">浏览器支持</h3>
<p>Chrome 53（<a href="https://www.chromestatus.com/features/4667415417847808" target="_blank">状态</a>）、Opera 40 和 Safari 10 随附的是 shadow DOM v1。
Edge 在考虑中，但<a href="https://developer.microsoft.com/en-us/microsoft-edge/platform/status/shadowdom/" target="_blank">优先级很高</a>。Mozilla 需要处理一个<a href="https://bugzilla.mozilla.org/show_bug.cgi?id=811542" target="_blank">未解决的错误</a>。</p>
<p>如希望获得 shadow DOM 检测功能，请查看是否存在 <code>attachShadow</code>：</p>
<pre><code>const supportsShadowDOMV1 = !!HTMLElement.prototype.attachShadow;<br /></code></pre>
<h4 id="polyfill">Polyfill</h4>
<p>在浏览器提供广泛支持前，<a href="https://github.com/webcomponents/shadydom" target="_blank">shadydom</a> 和 <a href="https://github.com/webcomponents/shadycss" target="_blank">shadycss</a> polyfill 可以为您提供 v1 功能。Shady DOM 可以模拟 Shadow DOM 的 DOM 作用域，而 shadycss polyfill 则可以模拟原生 API 提供的 CSS 自定义属性和样式作用域。</p>
<p>安装 polyfill：</p>
<pre><code>bower install --save webcomponents/shadydom<br />bower install --save webcomponents/shadycss<br /></code></pre>
<p>使用 polyfill：</p>
<pre><code>function loadScript(src) {<br /> return new Promise(function(resolve, reject) {<br />   const script = document.createElement('script');<br />   script.async = true;<br />   script.src = src;<br />   script.onload = resolve;<br />   script.onerror = reject;<br />   document.head.appendChild(script);<br /> });<br />}<br /><br />// Lazy load the polyfill if necessary.<br />if (!supportsShadowDOMV1) {<br />  loadScript('/bower_components/shadydom/shadydom.min.js')<br />    .then(e =&gt; loadScript('/bower_components/shadycss/shadycss.min.js'))<br />    .then(e =&gt; {<br />      // Polyfills loaded.<br />    });<br />} else {<br />  // Native shadow dom v1 support. Go to go!<br />}<br /></code></pre>
<p>请参阅 <a href="https://github.com/webcomponents/shadycss" target="_blank">https://github.com/webcomponents/shadycss#usage</a>，了解有关如何对您的样式进行填充/作用域设置的说明。</p>

<p>有史以来第一次，我们拥有了实施适当 CSS 作用域、DOM 作用域的 API 原语，并且有真正意义上的组合。
与自定义元素等其他网络组件 API 组合后，shadow DOM 提供了一种编写真正封装组件的方法，无需花多大的功夫或使用如 <code>&lt;iframe&gt;</code> 等陈旧的东西。</p>
<p>不要误会我的意思。Shadow DOM 无疑是一个复杂的巨兽！值得我们去学习。
请花一些时间来研究。认真学习并积极提问！</p>


<h2 id="_3">常见问题解答</h2>
<p><strong>我今天可以使用 Shadow DOM v1 吗？</strong></p>
<p>如果有 polyfill，那么是的，您可以使用。请参见<a href="#support" target="_blank">浏览器支持</a>。</p>
<p><strong>shadow DOM 提供哪些安全功能？</strong></p>
<p>Shadow DOM 不是一项安全功能。它是一款轻量级工具，用于限定作用域 CSS 并在组件中隐藏 DOM 树。
如果您需要一个真正的安全边界，请使用 <code>&lt;iframe&gt;</code>。</p>
<p><strong>网络组件是否必须使用 shadow DOM？</strong></p>
<p>不是！您无需创建使用 shadow DOM 的网络组件。但是，编写<a href="#elements" target="_blank">使用 Shadow DOM 的自定义元素</a>意味着您可以利用其功能，例如 CSS 作用域、DOM 封装以及组合。</p>
<p><strong>开放的影子根与闭合的影子根有何不同？</strong></p>
<p>请参阅<a href="#closed" target="_blank">闭合的影子根</a>。</p>

  
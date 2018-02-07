<a href="https://jakearchibald.com/2014/dont-use-flexbox-for-page-layout/">https://jakearchibald.com/2014/dont-use-flexbox-for-page-layout/</a><div id="articleHeader"><h1>Don't use flexbox for overall page layout</h1></div>
  <time>
    Posted 05 February 2014
    
    only 5 months after the previous post
    
  </time>
  
  <p>When I was building this blog I tried to use <a href="http://dev.w3.org/csswg/css-flexbox/" target="_blank">flexbox</a> for the overall page layout because I wanted to look cool and modern in front of my peers. However, like all of my other attempts to look cool and modern, it didn't really work.</p>
<p>Why? Well, take my hand and follow me into the next section…</p>
<p><strong>Update:</strong> Don't let this post scare you off flexbox, it's one of the best layout systems we have on the web today. However, there's a growing problem on the web when it comes to content shifting around during loading. For large amounts of content, flexbox can cause this, whereas grid is less likely to, but more commonly content-shift is caused by JS modifying the DOM. "Tools not rules" - test your layout with a 2g connection & large amounts of content, and ensure things are stable during loading.</p>
<h2 id="flexbox-vs-grid">Flexbox vs Grid</h2>
<p>Here's a basic three column design:</p>
<figure>
  <div class="readableLargeImageContainer"><img src="/static/posts/flexbox-vs-grid/site.179883e3a774.png" alt="Three column layout" /></div>
  <figcaption>The Holy Grail, apparently</figcaption>
</figure>

<p><a href="http://jsbin.com/iYEmaTUF/1" target="_blank">Here it is mocked up using flexbox</a> (works in all modern browsers), and <a href="http://jsbin.com/iYEmaTUF/2" target="_blank">here it is using grid layout</a> (works in IE10+). Both look the same, the difference is in how they load:</p>
<figure>
<div><div class="readableLargeObjectContainer"><iframe src="//www.youtube.com/embed/vPryjyFP5FM?rel=0&html5=1" frameborder="0" /></div>
<figcaption>Flexbox vs Grid</figcaption>
</figure>

<p>Browsers can progressively render content as it's streamed from the server, this is great because it means users can start consuming content before it's all arrived. However, when combined with flexbox it causes misalignment and horizontal shifting.</p>
<p>It's difficult to spot too, you're unlikely to notice it while developing locally, or via a super-fast connection. In those cases the page loads too quickly to notice. <a href="http://jsbin.com/iYEmaTUF/3" target="_blank">Here's a demo that displays the columns on a delay</a>, similar to how they will appear on a slower connection.</p>
<h2 id="flexbox-content-dictates-layout">Flexbox: content dictates layout</h2>
<p>Here's a simplified version of the layout:</p>
<div><pre>.container {
  display: flex;
  flex-flow: row;
}

nav {
  flex: 1;
  min-width: 118px;
  max-width: 160px;
}

.main {
  order: 1;
  flex: 1;
  min-width: 510px;
}

aside {
  flex: 1;
  order: 2;
  min-width: 150px;
  max-width: 210px;
}
</pre></div>


<p>The container declares itself as a flexbox, and child elements declare how they'd like to interact with one another within the flexbox.</p>
<p>As the page loads, the container starts to receive the first child, the main content. At this point it's the only child and it has <code>flex: 1</code>, so it gets all of the space. When the nav starts to arrive, the main content has to resize to make room for it, which causes that ugly re-layout.</p>
<h2 id="grid-container-dictates-layout-to-some-extent">Grid: container dictates layout (to some extent)</h2>
<p>Here's a simplified version of the same layout:</p>
<div><pre>.container {
  display: grid;
  grid-template-columns:
    (nav)   minmax(118px, 160px),
    (main)  minmax(612px, 1fr),
    (aside) minmax(182px, 242px);
}

nav {
  grid-area: nav;
}

.main {
  grid-area: main;
}

aside {
  grid-area: aside;
}
</pre></div>


<p><strong>Note:</strong> The code above is based on <a href="http://dev.w3.org/csswg/css-grid/" target="_blank">the latest spec</a> and isn't implemented in any browser, yet. You should bother your favourite browser vendor about this.</p>
<p>Here the layout is defined in the container, so the nav is rendered into the middle column as soon as it starts to arrive.</p>
<h2 id="but-grid-can-load-poorly-too">But grid can load poorly too...</h2>
<p>To load nicely, you need to restrict yourself to configurations that can be predetermined by the grid container.</p>
<p>Here are some examples that break that:</p>
<div><pre>.container {
  display: grid;
  grid-template-columns:
    /* Size defined by content, so will change with content */
    (foo)   max-content,
    /* Same again */ 
    (bar)   min-content,
    /* Computes to minmax(min-content, max-content), so same again */
    (hello) auto;
}

aside {
  /* This column isn't defined by the container, so one
     is created dynamically. This will cause content to
     shift as 'aside' appears in the container */
  grid-column: 4;
}
</pre></div>


<h2 id="but-dont-write-off-flexbox">But don't write-off flexbox!</h2>
<p>Flexbox is great, it just isn't the best thing for overall page layouts.</p>
<p>Flexbox's strength is in its content-driven model. It doesn't need to know the content up-front. You can <a href="http://dev.w3.org/csswg/css-flexbox/#valuedef-flex-basis" target="_blank">distribute items based on their content</a>, <a href="http://dev.w3.org/csswg/css-flexbox/#flex-wrap-property" target="_blank">allow boxes to wrap</a> which is really handy for responsive design, you can even <a href="http://dev.w3.org/csswg/css-flexbox/#flex-shrink-property" target="_blank">control the distribution of negative space</a> separately to positive space.</p>
<p><a href="http://codepen.io/chriscoyier/pen/FAbpm" target="_blank">This nav bar by Chris Coyier</a> is a great example of something that makes more sense as a flexbox than grid.</p>
<p>Flexbox and grid play well together, and are a huge step forward from the float & table hacks they replace. The sooner we can use them both in production, the better.</p>
<h2 id="further-reading">Further reading</h2>


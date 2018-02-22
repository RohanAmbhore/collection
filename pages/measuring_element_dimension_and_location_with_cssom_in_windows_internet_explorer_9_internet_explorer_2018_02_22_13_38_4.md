<a href="https://msdn.microsoft.com/en-us/library/hh781509(v=vs.85).aspx">https://msdn.microsoft.com/en-us/library/hh781509(v=vs.85).aspx</a><div id="articleHeader"><h1>Measuring Element Dimension and Location with CSSOM in Windows Internet Explorer 9</h1></div>
  
  

<p>This topic is designed to help web developers understand how to access the dimension and location of elements on the page through the CSS Object Model (CSSOM) in Windows Internet Explorer 9.</p>
<h2>Understanding Properties That Measure Element Dimension and Location</h2>
<p>The following diagrams represent different CSSOM properties for the same page. The sample page contains a <a href="https://msdn.microsoft.com/en-us/library/ms535240(v=vs.85).aspx" target="_blank"><strong>div</strong></a> red element that is relatively positioned on the page. The blue element is the red element's parent. Its primary purpose is to define the different Cascading Style Sheets (CSS) boxes that compose an element's layout, as well as to show how the <a href="https://msdn.microsoft.com/en-us/library/ms534303(v=vs.85).aspx" target="_blank"><strong>offsetTop</strong></a> property is calculated. The viewport is the black outline, and is represented by the <a href="https://msdn.microsoft.com/en-us/library/ms535255(v=vs.85).aspx" target="_blank"><strong>html</strong></a> element. In the diagrams, the <strong>html</strong> element is not shown with any margin or border. Adding a margin or border would not change any of the measurements, however.</p>
<p>Because the <a href="https://msdn.microsoft.com/en-us/library/ms530824(v=vs.85).aspx" target="_blank"><strong>overflow</strong></a> attribute of the <a href="https://msdn.microsoft.com/en-us/library/ms535240(v=vs.85).aspx" target="_blank"><strong>div</strong></a> has been set to "scroll" and it contains more content than can be displayed within its limited client area, scroll bars are displayed. Be aware that the values illustrated are all the <em>vertical</em>-oriented properties. The horizontal-oriented properties are similar; simply substitute "left" for "top", "width" for "height", and so on.</p>
<p>For more information about any of these properties, see Reference.</p>
<p>The following diagram illustrates vertical sizing and positioning values for the red element.</p>
<p><div class="readableLargeImageContainer"><img src="https://i-msdn.sec.s-msft.com/dynimg/IC561968.png" alt="Vertical sizing and positioning values for a child element" title="Vertical sizing and positioning values for a child element" id="ie9_positioning1" /></div></p>
<div><strong>Note</strong>  When elements are scrolled such that they are partly visible at the top of the viewport, the <a href="https://msdn.microsoft.com/en-us/library/ms536433(v=vs.85).aspx" target="_blank"><strong>getBoundingClientRect</strong></a>().<a href="https://msdn.microsoft.com/en-us/library/ms534688(v=vs.85).aspx" target="_blank"><strong>top</strong></a> property returns negative values.</div>
<p>The following diagram illustrates vertical sizing and mouse coordinate positions that are affected by CSS transforms. Be aware that the <a href="https://msdn.microsoft.com/en-us/library/ms534306(v=vs.85).aspx" target="_blank"><strong>offsetY</strong></a> coordinates are reported in the red element's original coordinate space (that is, as if the element were not transformed). This is in contrast to <a href="https://msdn.microsoft.com/en-us/library/gg130968(v=vs.85).aspx" target="_blank"><strong>layerY</strong></a>, which is reported in the transformed coordinate space (that is, according to the dimensions of the bounding box).</p>
<p><div class="readableLargeImageContainer"><img src="https://i-msdn.sec.s-msft.com/dynimg/IC561969.png" alt="Vertical sizing and mouse coordinate positions affected by CSS transforms" title="Vertical sizing and mouse coordinate positions affected by CSS transforms" id="ie9_positioning2" /></div></p>
<p>The following diagram illustrates all vertical mouse coordinates and viewport offsets on an untransformed element. Be aware that, in Internet Explorer 9, when the page has been scrolled, the <a href="https://msdn.microsoft.com/en-us/library/gg130968(v=vs.85).aspx" target="_blank"><strong>layerY</strong></a> value includes the <a href="https://msdn.microsoft.com/en-us/library/ff974684(v=vs.85).aspx" target="_blank"><strong>window.pageYOffset</strong></a> amount in the value. This is incorrect behavior, and will be fixed in a future release.</p>
<p>Also, in this diagram, the viewport has been scrolled down such that there is additional content available "above" the viewport. This is designed to show that each property—<a href="https://msdn.microsoft.com/en-us/library/ff974656(v=vs.85).aspx" target="_blank"><strong>pageY</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms533568(v=vs.85).aspx" target="_blank"><strong>clientY</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/gg130968(v=vs.85).aspx" target="_blank"><strong>layerY</strong></a>, and <a href="https://msdn.microsoft.com/en-us/library/ms534306(v=vs.85).aspx" target="_blank"><strong>offsetY</strong></a>—corresponds to a different relative coordinate point when the document has been scrolled.</p>
<p><div class="readableLargeImageContainer"><img src="https://i-msdn.sec.s-msft.com/dynimg/IC561970.png" alt="All vertical mouse coordinates and viewport offsets on an untransformed element" title="All vertical mouse coordinates and viewport offsets on an untransformed element" id="ie9_positioning3" /></div></p>
<h2>Finding an Element's Location Relative to the Page Origin</h2>
<p>An element has convenient CSSOM properties to find its location relative to the element's <a href="https://msdn.microsoft.com/en-us/library/ms534302(v=vs.85).aspx" target="_blank"><strong>offsetParent</strong></a> or the viewport. There is currently no CSSOM property to directly locate an element based on the page (document) origin (for instance, similar to the <a href="https://msdn.microsoft.com/en-us/library/ff974655(v=vs.85).aspx" target="_blank"><strong>pageX</strong></a>/<a href="https://msdn.microsoft.com/en-us/library/ff974656(v=vs.85).aspx" target="_blank"><strong>pageY</strong></a> properties for mouse events).</p>
<p>A common solution to find the element's location relative to the page involves summing the value of <a href="https://msdn.microsoft.com/en-us/library/ms534303(v=vs.85).aspx" target="_blank"><strong>offsetTop</strong></a> with the element's <a href="https://msdn.microsoft.com/en-us/library/ms534302(v=vs.85).aspx" target="_blank"><strong>offsetParent</strong></a>.<strong>offsetTop</strong> and so on until <strong>offsetParent</strong> returns null. (Naturally, <a href="https://msdn.microsoft.com/en-us/library/ms534200(v=vs.85).aspx" target="_blank"><strong>offsetLeft</strong></a> is used for horizontal positioning.) Avoid this practice for the following reasons:</p>
<ol>
<li>The <a href="https://msdn.microsoft.com/en-us/library/ms534303(v=vs.85).aspx" target="_blank"><strong>offsetTop</strong></a> value does not include the width of the <a href="https://msdn.microsoft.com/en-us/library/ms534302(v=vs.85).aspx" target="_blank"><strong>offsetParent's</strong></a> border. This can lead to slight misalignments when any element in the <strong>offsetParent</strong> chain has a border style applied.</li>
<li>These repeated summations can contribute to slow performance when <a href="https://msdn.microsoft.com/en-us/library/ms534302(v=vs.85).aspx" target="_blank"><strong>offsetParent</strong></a> chains are long.</li>
</ol>
<p>With Internet Explorer 9, it is better to use the newly added <a href="https://msdn.microsoft.com/en-us/library/ff974684(v=vs.85).aspx" target="_blank"><strong>window.pageYOffset</strong></a> property (<a href="https://msdn.microsoft.com/en-us/library/ff974683(v=vs.85).aspx" target="_blank"><strong>window.pageXOffset</strong></a> for horizontal scenarios). The recommended practice to find an element's vertical location from the page's origin is to add the element's <a href="https://msdn.microsoft.com/en-us/library/ms536433(v=vs.85).aspx" target="_blank"><strong>getBoundingClientRect</strong></a>().<a href="https://msdn.microsoft.com/en-us/library/ms534688(v=vs.85).aspx" target="_blank"><strong>top</strong></a> property to the <strong>window.pageYOffset</strong> value. (<strong>getBoundingClientRect</strong>().<a href="https://msdn.microsoft.com/en-us/library/ms534099(v=vs.85).aspx" target="_blank"><strong>left</strong></a> + <strong>window.pageXOffset</strong> for the horizontal location.) This yields the correct result avoiding both pitfalls previously shown.</p>
<h2>Reference</h2>
<p>Coordinates relative to the <strong>page</strong> origin (document origin, regardless of viewport scrolling):</p>
<ul>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ff974655(v=vs.85).aspx" target="_blank"><strong>pageX</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ff974656(v=vs.85).aspx" target="_blank"><strong>pageY</strong></a> (location of the mouse)</li>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ff974683(v=vs.85).aspx" target="_blank"><strong>pageXOffset</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ff974684(v=vs.85).aspx" target="_blank"><strong>pageYOffset</strong></a> (location of the viewport)</li>
</ul>
<p>Coordinates relative to the <strong>viewport</strong> origin (visible area of the page):</p>
<ul>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ms536433(v=vs.85).aspx" target="_blank"><strong>getBoundingClientRect</strong></a>().<a href="https://msdn.microsoft.com/en-us/library/ms534688(v=vs.85).aspx" target="_blank"><strong>top</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms533535(v=vs.85).aspx" target="_blank"><strong>bottom</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms534099(v=vs.85).aspx" target="_blank"><strong>left</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms534374(v=vs.85).aspx" target="_blank"><strong>right</strong></a> (location of the element's border box/bounding box when CSS transforms are applied)</li>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ms536435(v=vs.85).aspx" target="_blank"><strong>getClientRects</strong></a>()[0].top, bottom, left, right (same as above)</li>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ms533567(v=vs.85).aspx" target="_blank"><strong>clientX</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms533568(v=vs.85).aspx" target="_blank"><strong>clientY</strong></a> (location of the mouse)</li>
</ul>
<p>Coordinates relative to an element's <strong>margin box</strong> origin (unaffected by CSS transforms):</p>
<ul>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ff975168(v=vs.85).aspx" target="_blank"><strong>getComputedStyle</strong></a>().<a href="https://msdn.microsoft.com/en-us/library/ms530808(v=vs.85).aspx" target="_blank"><strong>marginTop</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms530804(v=vs.85).aspx" target="_blank"><strong>marginLeft</strong></a> (location of the element's border box)</li>
</ul>
<p>Coordinates relative to an element's <strong>border box</strong> origin (unaffected by CSS transforms):</p>

<p>Coordinates relative to an element's <strong>border box/bounding box</strong> (when CSS transforms are applied):</p>
<ul>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ms536433(v=vs.85).aspx" target="_blank"><strong>getBoundingClientRect</strong></a>().<a href="https://msdn.microsoft.com/en-us/library/ff974674(v=vs.85).aspx" target="_blank"><strong>height</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ff974675(v=vs.85).aspx" target="_blank"><strong>width</strong></a> (dimension of element's border box/bounding box)</li>
<li>
<a href="https://msdn.microsoft.com/en-us/library/gg130967(v=vs.85).aspx" target="_blank"><strong>layerX</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/gg130968(v=vs.85).aspx" target="_blank"><strong>layerY</strong></a> (location of the mouse)</li>
</ul>
<p>Coordinates relative to an element's <strong>padding box</strong> (unaffected by CSS transforms):</p>
<ul>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ms533563(v=vs.85).aspx" target="_blank"><strong>clientHeight</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms533566(v=vs.85).aspx" target="_blank"><strong>clientWidth</strong></a> (dimension of the element's padding box, less scrollbar track when visible)</li>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ff975168(v=vs.85).aspx" target="_blank"><strong>getComputedStyle</strong></a>().<a href="https://msdn.microsoft.com/en-us/library/ms530839(v=vs.85).aspx" target="_blank"><strong>paddingTop</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms530835(v=vs.85).aspx" target="_blank"><strong>paddingLeft</strong></a> (location of the element's content box)</li>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ms534305(v=vs.85).aspx" target="_blank"><strong>offsetX</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms534306(v=vs.85).aspx" target="_blank"><strong>offsetY</strong></a> (location of the mouse)</li>
</ul>
<p>Coordinates relative to an element's <strong>content origin</strong> (when content overflows producing scrollbars):</p>
<ul>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ms534618(v=vs.85).aspx" target="_blank"><strong>scrollTop</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms534617(v=vs.85).aspx" target="_blank"><strong>scrollLeft</strong></a> (location of the padding box)</li>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ms534615(v=vs.85).aspx" target="_blank"><strong>scrollHeight</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms534619(v=vs.85).aspx" target="_blank"><strong>scrollWidth</strong></a> (dimension of the overflow content)</li>
</ul>
<p>Coordinates relative to an element's <strong>content box</strong> (unaffected by CSS transforms):</p>
<ul>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ff975168(v=vs.85).aspx" target="_blank"><strong>getComputedStyle</strong></a>().<a href="https://msdn.microsoft.com/en-us/library/ms530765(v=vs.85).aspx" target="_blank"><strong>height</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms531183(v=vs.85).aspx" target="_blank"><strong>width</strong></a> (dimension of the content box)</li>
</ul>
<p>Coordinates relative to an element's <a href="https://msdn.microsoft.com/en-us/library/ms534302(v=vs.85).aspx" target="_blank"><strong>offsetParent</strong></a> (padding box of the <a href="https://msdn.microsoft.com/en-us/library/ms534302(v=vs.85).aspx" target="_blank"><strong>offsetParent</strong></a>):</p>
<ul>
<li>
<a href="https://msdn.microsoft.com/en-us/library/ms534303(v=vs.85).aspx" target="_blank"><strong>offsetTop</strong></a>, <a href="https://msdn.microsoft.com/en-us/library/ms534200(v=vs.85).aspx" target="_blank"><strong>offsetLeft</strong></a> (location of the border box)</li>
</ul>
<h2>Related topics</h2>
<dl>
<dt><strong>Conceptual</strong></dt>
<dt>
<a href="https://msdn.microsoft.com/en-us/library/bg124103(v=vs.85).aspx" target="_blank">CSS Overviews and Tutorials</a>
</dt>
<dt><strong>Other Resources</strong></dt>
<dt><a href="http://go.microsoft.com/fwlink/p/?LinkId=219155" target="_blank">Spotlight on Internet Explorer</a></dt>
</dl>
<br /><br />
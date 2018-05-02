<a href="https://stackoverflow.com/questions/42613359/how-does-flex-wrap-work-with-align-self-align-items-and-align-content">https://stackoverflow.com/questions/42613359/how-does-flex-wrap-work-with-align-self-align-items-and-align-content</a><div id="articleHeader"><h1>How does flex-wrap work with align-self, align-items and align-content?</h1></div>
<h2>Short Answer</h2>

<p>Although the <code>flex-wrap</code> property seems pretty basic – it controls whether flex items can wrap – it actually has a wide-ranging impact on the entire flexbox layout.</p>

<p>The <code>flex-wrap</code> property determines the type of flex container you will use.</p>

<ul>
<li><code>flex-wrap: nowrap</code> creates a <strong><em>single-line flex container</em></strong></li>
<li><code>flex-wrap: wrap</code> and <code>wrap-reverse</code> create a <strong><em>multi-line flex container</em></strong></li>
</ul>

<p>The <code>align-items</code> and <code>align-self</code> properties work in both single- and multi-line containers. However, they can only have an effect when there's free space in the cross axis of the flex line.</p>

<p>The <code>align-content</code> property works only in multi-line containers. It is ignored in single-line containers.</p>

<hr />

<h2>Explanation</h2>

<p>The <a href="https://www.w3.org/TR/css-flexbox-1/" target="_blank">flexbox specification</a> provides four keyword properties for aligning flex items:</p>

<ul>
<li><code>align-items</code></li>
<li><code>align-self</code></li>
<li><code>align-content</code></li>
<li><code>justify-content</code></li>
</ul>

<p>To understand the functions of these properties it's important to first understand the structure of a flex container.</p>

<hr />

<h2>Part 1: Understanding the Main Axis and Cross Axis of a Flex Container</h2>

<p><strong><em>The X and Y Axes</em></strong></p>

<p>A flex container works in two directions: x-axis (horizontal) and y-axis (vertical).</p>

<p><a href="https://i.stack.imgur.com/wmy0R.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/wmy0R.png" alt="x-axis and the y-axis" /></div></a></p>

<p>                                                                                                                <sup>Source: <a href="https://es.wikipedia.org/wiki/Tridimensional" target="_blank">Wikipedia</a></sup></p>

<p>The child elements of a flex container – known as "flex items" – can be aligned in either direction.</p>

<p>This is flex alignment at its most fundamental level.</p>

<p><strong><em>The Main and Cross Axes</em></strong></p>

<p>Overlaying the x and y axes are, in flex layout, the <em>main</em> and <em>cross</em> axes.</p>

<p>By default, the main axis is horizontal (x-axis), and the cross axis is vertical (y-axis). That's the initial setting, as defined by the <a href="https://www.w3.org/TR/css-flexbox-1/#box-model" target="_blank">flexbox specification</a>.</p>

<p><a href="https://i.stack.imgur.com/9Oxw7.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/9Oxw7.png" alt="flex main axis and cross axis" /></div></a></p>

<p>                                                                                                                <sup>Source: <a href="https://www.w3.org/TR/css-flexbox-1/#box-model" target="_blank">W3C</a></sup></p>

<p>However, unlike the x and y axes, which are fixed, the main and cross axes can switch directions.</p>

<p><strong><em>The <code>flex-direction</code> Property</em></strong></p>

<p>In the image above, the main axis is horizontal and the cross axis is vertical. As mentioned earlier, that's an initial setting of a flex container.</p>

<p>However, these directions can be easily switched with the <code>flex-direction</code> property. This property controls the direction of the main axis; it determines whether flex items align vertically or horizontally.</p>

<p><em>From the spec:</em></p>

<blockquote>
  <p><a href="https://www.w3.org/TR/css-flexbox-1/#flex-direction-property" target="_blank"><strong>5.1. Flex Flow Direction: the <code>flex-direction</code>
  property</strong></a></p>
  
  <p>The <code>flex-direction</code> property specifies how flex items are placed in
  the flex container, by setting the direction of the flex container’s
  main axis. This determines the direction in which flex items are laid
  out.</p>
</blockquote>

<p>There are four values for the <code>flex-direction</code> property:</p>

<pre><code>/* main axis is horizontal, cross axis is vertical */
flex-direction: row; /* default */
flex-direction: row-reverse;

/* main axis is vertical, cross axis is horizontal */    
flex-direction: column;
flex-direction: column-reverse;</code></pre>

<p>The cross axis is always perpendicular to the main axis.</p>

<hr />

<h2>Part 2: Flex Lines</h2>

<p>Within the container, flex items exist in a line, known as a "flex line".</p>

<p>A flex line is a row or column, depending on <code>flex-direction</code>.</p>

<p>A container can have one or more lines, depending on <code>flex-wrap</code>. </p>

<p><strong><em>Single-Line Flex Container</em></strong></p>

<p><code>flex-wrap: nowrap</code> establishes a single-line flex container, in which flex items are forced to stay in a single line (even if they overflow the container).</p>

<p><a href="https://i.stack.imgur.com/i4f2k.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/i4f2k.png" alt="a single-line flex container (one column)" /></div></a></p>

<p><em>The image above has one flex line.</em></p>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>
<p><strong><em>Multi-Line Flex Container</em></strong></p>

<p><code>flex-wrap: wrap</code> or <code>wrap-reverse</code> establishes a multi-line flex container, in which flex items can create new lines.</p>

<p><a href="https://i.stack.imgur.com/UVKhz.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/UVKhz.png" alt="multi-line flex container (3 columns)" /></div></a></p>

<p><em>The image above has three flex lines.</em></p>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>
<p><a href="https://i.stack.imgur.com/kp4MO.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/kp4MO.png" alt="multi-line flex container (3 rows)" /></div></a></p>

<p><em>The image above has three flex lines.</em></p>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>

<hr />

<h2>Part 3: Keyword Alignment Properties</h2>

<p><strong><em>Properties are Assigned to the Main and Cross (not X and Y) Axes</em></strong></p>

<p>While the <code>flex-direction</code> property controls the direction in which flex items are laid out, there are four properties that control alignment and positioning. These are:</p>

<ul>
<li><code>align-items</code></li>
<li><code>align-self</code></li>
<li><code>align-content</code></li>
<li><code>justify-content</code></li>
</ul>

<p>Each one of these properties is permanently assigned to an axis.</p>

<p>The <code>justify-content</code> property works only in the main axis.</p>

<p>The three <code>align-*</code> properties work only in the cross axis.</p>

<p>It's a common mistake to assume that these properties are fixed to the x and y axes. For example, <code>justify-content</code> is always horizontal, and <code>align-items</code> is always vertical.</p>

<p>However, when <code>flex-direction</code> is switched to <code>column</code>, the main axis becomes the y-axis, and <code>justify-content</code> works vertically.</p>

<p>The focus of this post is cross-axis alignment. For an explanation of main-axis alignment and the <code>justify-content</code> property, see this post:</p>

<ul>
<li><a href="https://stackoverflow.com/q/32551291/3597276" target="_blank">In CSS Flexbox, why are there no "justify-items" and "justify-self" properties?</a></li>
</ul>

<p><strong><em>Definitions</em></strong></p>

<p>The flexbox specification provides three keyword properties for cross-axis alignment:</p>

<ul>
<li><code>align-items</code></li>
<li><code>align-self</code></li>
<li><code>align-content</code></li>
</ul>

<h2><code>align-items</code> / <code>align-self</code></h2>

<p>The <code>align-items</code> property aligns flex items along the cross axis of the flex line. It applies to flex containers.</p>

<p>The <code>align-self</code> property is used to override <code>align-items</code> on individual flex items. It applies to flex items.</p>

<p>Here's the definition from the spec:</p>

<blockquote>
  <p><a href="https://www.w3.org/TR/css-flexbox-1/#align-items-property" target="_blank"><strong>8.3. Cross-axis Alignment: the <code>align-items</code> and <code>align-self</code>
  properties</strong></a></p>
  
  <p>Flex items can be aligned in the cross axis of the current line of the
  flex container, similar to <code>justify-content</code> but in the perpendicular
  direction. <code>align-items</code> sets the default alignment for all of the
  flex container’s items. <code>align-self</code> allows this default alignment to
  be overridden for individual flex items.</p>
</blockquote>

<p>There are six possible values for <code>align-items</code> / <code>align-self</code>:</p>

<ul>
<li><code>flex-start</code></li>
<li><code>flex-end</code></li>
<li><code>center</code></li>
<li><code>baseline</code></li>
<li><code>stretch</code></li>
<li><code>auto</code> (<code>align-self</code> only)</li>
</ul>

<p>(For a description of each value, click on the spec definition heading above.)</p>

<p>The initial value of <code>align-items</code> is <code>stretch</code>, meaning flex items will expand the full available length of the container's cross axis.</p>

<p>The initial value of <code>align-self</code> is <code>auto</code>, meaning it inherits the value of <code>align-items</code>. </p>

<p>Below is an illustration of the effect of each value in a row-direction container.</p>

<p><a href="https://i.stack.imgur.com/8A6EZ.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/8A6EZ.png" alt="align-items align-self values" /></div></a></p>

<p>                                                                                                                <sup>source: <a href="https://www.w3.org/TR/css-flexbox-1/#align-items-property" target="_blank">W3C</a></sup></p>

<h2><code>align-content</code></h2>

<p>This property is slightly more complex than <code>align-items</code> and <code>align-self</code>. </p>

<p>Here's the definition from the spec:</p>

<blockquote>
  <p><a href="https://www.w3.org/TR/css-flexbox-1/#align-content-property" target="_blank"><strong>8.4. Packing Flex Lines: the <code>align-content</code>
  property</strong></a></p>
  
  <p>The <code>align-content</code> property aligns a flex container’s lines within
  the flex container when there is extra space in the cross-axis,
  similar to how <code>justify-content</code> aligns individual items within the
  main-axis. Note, this property has no effect on a single-line flex
  container.</p>
</blockquote>

<p>In contrast to <code>align-items</code> and <code>align-self</code>, which move flex items <em>within their line</em>, <code>align-content</code> moves flex lines <em>within the container</em>.</p>

<p>There are the six possible values for <code>align-content</code>:</p>

<ul>
<li><code>flex-start</code></li>
<li><code>flex-end</code></li>
<li><code>center</code></li>
<li><code>space-between</code></li>
<li><code>space-around</code> </li>
<li><code>stretch</code></li>
</ul>

<p>(For a description of each value, click on the spec definition heading above.)</p>

<p>Below is an illustration of the effect of each value in a row-direction container.</p>

<p><a href="https://i.stack.imgur.com/2HjlC.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/2HjlC.png" alt="enter image description here" /></div></a></p>

<p>                                                                                                                <sup>source: <a href="https://www.w3.org/TR/css-flexbox-1/#align-content-property" target="_blank">W3C</a></sup></p>

<p><strong><em>Why does <code>align-content</code> work only in multi-line flex containers?</em></strong></p>

<p>In a single-line flex container, the cross size of the line is equal to the cross size of the container. This means there is no free space between the line and the container. As a result, <code>align-content</code> can have no effect.</p>

<p>Here's the <a href="https://www.w3.org/TR/css-flexbox-1/#align-content-property" target="_blank">relevant section from the spec</a>:</p>

<blockquote>
  <blockquote>
    <p>Only multi-line flex containers ever have free space in the cross-axis for lines to be aligned in, because in a single-line flex container the sole line automatically stretches to fill the space.</p>
  </blockquote>
</blockquote>

<hr />

<h2>Part 4: Examples Explained</h2>

<p><a href="https://i.stack.imgur.com/E9uHd.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/E9uHd.png" alt="enter image description here" /></div></a></p>

<p>In Example #1, <code>align-self</code> works with <code>flex-wrap: nowrap</code> because the flex items exist in a single-line container. Therefore, there is one flex line and it matches the height of the container.</p>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>
<p><a href="https://i.stack.imgur.com/3UtjN.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/3UtjN.png" alt="enter image description here" /></div></a></p>

<p>In Example #2, <code>align-self</code> fails because it exists in a multi-line container (<code>flex-wrap: wrap</code>) <em>and</em> <code>align-content</code> is set to <code>flex-start</code>. This means that flex lines are packed tightly to the start of the cross axis, leaving no free space for <code>align-self</code> to work.</p>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>
<p><a href="https://i.stack.imgur.com/Ijjxk.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/Ijjxk.png" alt="enter image description here" /></div></a></p>

<p>The explanation for Example #3 is the same as for Example #1.</p>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>
<p><a href="https://i.stack.imgur.com/jEs73.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/jEs73.png" alt="enter image description here" /></div></a></p>

<p>The explanation for Example #4 is the same as for Example #2.</p>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>
<p><a href="https://i.stack.imgur.com/1ydI0.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/1ydI0.png" alt="enter image description here" /></div></a></p>

<p>Example #5 is a single-line container. As such, the cross size of the flex line equals the cross size of the container, leaving no extra space between the two. Therefore, <code>align-content</code>, which aligns flex lines <em>when there is extra space in the cross axis</em>, is having no effect.</p>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>
<p><a href="https://i.stack.imgur.com/Kpy8P.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/Kpy8P.png" alt="enter image description here" /></div></a></p>

<p>The initial setting for <code>align-content</code> is <code>stretch</code>. This means that if no other value is specified, the container will distribute available space evenly among flex lines. (A similar effect is created on the main axis when all flex items get <code>flex: 1</code>.)</p>

<p>This distribution of space among lines can cause wide gaps between rows / columns. Less lines result in wider gaps. More lines result in smaller gaps, as each line gets a smaller share of the space. </p>

<p>To resolve this problem switch from <code>align-content: stretch</code> to <code>align-content: flex-start</code>. This packs the lines together (see examples #2 and #4 above). Of course, this also eliminates any free space in the line, and <code>align-items</code> and <code>align-self</code> can no longer work.</p>

<p>Here's a related post: <a href="https://stackoverflow.com/q/40890613/3597276" target="_blank">Remove space (gaps) between multiple lines of flex items when they wrap</a></p>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>
<p><a href="https://i.stack.imgur.com/tfKpo.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/tfKpo.png" alt="enter image description here" /></div></a></p>

<p>As explained in previous examples, with <code>align-content: stretch</code>, there can be extra space in the flex lines, which allows <code>align-items</code> and <code>align-self</code> to work. Any other value for <code>align-content</code> would pack the lines, eliminating  extra space, and making <code>align-items</code> and <code>align-self</code> useless.</p>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>
    
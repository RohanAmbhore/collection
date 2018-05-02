<a href="https://stackoverflow.com/questions/32551291/in-css-flexbox-why-are-there-no-justify-items-and-justify-self-properties">https://stackoverflow.com/questions/32551291/in-css-flexbox-why-are-there-no-justify-items-and-justify-self-properties</a><div id="articleHeader"><h1>In CSS Flexbox, why are there no "justify-items" and "justify-self" properties?</h1></div>

            

<div id="question">

    
        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        371
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>264</b></div>


</div>

            </div>

            
<div>
    <div>

<p>Consider the main axis and cross axis of a flex container:</p>

<p><a href="https://i.stack.imgur.com/9Oxw7.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/9Oxw7.png" alt="enter image description here" /></div></a>
                                                                                                                       <sup>Source: <a href="http://www.w3.org/TR/css-flexbox-1/#box-model" target="_blank">W3C</a></sup></p>

<p>To align flex items along the main axis there is one property:</p>

<ul>
<li><a href="http://www.w3.org/TR/css-flexbox-1/#justify-content-property" target="_blank"><code>justify-content</code></a></li>
</ul>

<p>To align flex items along the cross axis there are three properties:</p>



<p>In the image above, the main axis is horizontal and the cross axis is vertical. These are the default directions of a flex container.</p>

<p>However, these directions can be easily interchanged with the <a href="http://www.w3.org/TR/css-flexbox-1/#propdef-flex-direction" target="_blank"><code>flex-direction</code></a> property.</p>

<pre><code>/* main axis is horizontal, cross axis is vertical */
flex-direction: row;
flex-direction: row-reverse;

/* main axis is vertical, cross axis is horizontal */    
flex-direction: column;
flex-direction: column-reverse;</code></pre>

<p>(The cross axis is always perpendicular to the main axis.)</p>

<p>My point in describing how the axes' work is that there doesn't seem to be anything special about either direction. Main axis, cross axis, they're both equal in terms of importance and <code>flex-direction</code> makes it easy to switch back and forth. </p>

<p><em>So why does the cross axis get two additional alignment properties?</em></p>

<p><em>Why are <code>align-content</code> and <code>align-items</code> consolidated into one property for the main axis?</em></p>

<p><em>Why does the main axis not get a <code>justify-self</code> property?</em></p>

<hr />

<p>Scenarios where these properties would be useful:</p>

<ul>
<li><p>placing a flex item in the corner of the flex container<br />
<code>#box3 { align-self: flex-end; justify-self: flex-end; }</code></p></li>
<li><p>making a group of flex items align-right (<code>justify-content: flex-end</code>) but have the first item align left (<code>justify-self: flex-start</code>)</p>

<p><em>Consider a header section with a group of nav items and a logo. With <code>justify-self</code> the logo could be aligned left while the nav items stay far right, and the whole thing adjusts smoothly ("flexes") to different screen sizes.</em></p></li>
<li><p>in a row of three flex items, affix the middle item to the center of the container  (<code>justify-content: center</code>) and align the adjacent items to the container edges (<code>justify-self: flex-start</code> and <code>justify-self: flex-end</code>). </p>

<p><em>Note that values <code>space-around</code> and <code>space-between</code> on
<code>justify-content</code> property  will not keep the middle item centered in relation to the container if the adjacent items have different widths.</em></p></li>
</ul>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>
<p><a href="http://jsfiddle.net/7an37m20/12/" target="_blank">jsFiddle version</a></p>

<hr />

<p>As of this writing, there is no mention of <code>justify-self</code> or <code>justify-items</code> in the <a href="http://www.w3.org/TR/css-flexbox-1/" target="_blank">flexbox spec</a>.</p>

<p>However, in the <a href="http://www.w3.org/TR/css-align-3/" target="_blank">CSS Box Alignment Module</a>, which is the W3C's unfinished proposal to establish a common set of alignment properties for use across all box models, there is this:</p>

<p><a href="https://i.stack.imgur.com/uu2tP.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/uu2tP.png" alt="enter image description here" /></div></a>
                                                                                                                       
<sup>Source: <a href="http://www.w3.org/TR/css3-align/#overview" target="_blank">W3C</a></sup></p>

<p>You'll notice that <code>justify-self</code> and <code>justify-items</code> are being considered... <em>but not for flexbox</em>.</p>

<hr />

<p>I'll end by reiterating the main question:</p>

<blockquote>
  <p>Why are there no "justify-items" and "justify-self" properties?</p>
</blockquote>
    </div>
    
    
</div>

                
    <div>
	    

        <div id="comments-link-32551291">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </div>        </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-33856609">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        699
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<h2>Methods for Aligning Flex Items along the Main Axis</h2>

<p>As stated in the question:</p>

<blockquote>
  <p>To align flex items along the main axis there is one property: <a href="http://www.w3.org/TR/css-flexbox-1/#justify-content-property" target="_blank"><code>justify-content</code></a></p>
  
  <p>To align flex items along the cross axis there are three properties: <a href="http://www.w3.org/TR/css-flexbox-1/#align-content-property" target="_blank"><code>align-content</code></a>, <a href="http://www.w3.org/TR/css-flexbox-1/#align-items-property" target="_blank"><code>align-items</code> and <code>align-self</code></a>.</p>
</blockquote>

<p>The question then asks:</p>

<blockquote>
  <p>Why are there no <code>justify-items</code> and <code>justify-self</code> properties?</p>
</blockquote>

<p>One answer may be: <em>Because they're not necessary.</em></p>

<p>The <a href="http://www.w3.org/TR/css-flexbox-1/" target="_blank">flexbox specification</a> provides <em>two</em> methods for aligning flex items along the main axis:</p>

<ol>
<li>The <code>justify-content</code> keyword property, and</li>
<li><a href="http://www.w3.org/TR/css-flexbox-1/#auto-margins" target="_blank"><code>auto</code> margins</a></li>
</ol>

<hr />

<h2><em>justify-content</em></h2><p>The <a href="http://www.w3.org/TR/css-flexbox-1/#justify-content-property" target="_blank"><code>justify-content</code></a> property aligns flex items along the main axis of the flex container. </p>

<p>It is applied to the flex container but only affects flex items. </p>

<p>There are five alignment options:</p>

<ul>
<li><p><strong><code>flex-start</code></strong> ~ Flex items are packed toward the start of the line.</p>

<p><a href="https://i.stack.imgur.com/YOzeU.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/YOzeU.png" alt="enter image description here" /></div></a></p></li>
<li><p><strong><code>flex-end</code></strong> ~ Flex items are packed toward the end of the line.</p>

<p><a href="https://i.stack.imgur.com/13Z1u.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/13Z1u.png" alt="enter image description here" /></div></a></p></li>
<li><p><strong><code>center</code></strong> ~ Flex items are packed toward the center of the line.</p>

<p><a href="https://i.stack.imgur.com/oKi7M.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/oKi7M.png" alt="enter image description here" /></div></a></p></li>
<li><p><strong><code>space-between</code></strong> ~ Flex items are evenly spaced, with the first item aligned to one edge of the container and the last item aligned to the opposite edge. The edges used by the first and last items depends on <a href="http://www.w3.org/TR/css-flexbox-1/#flex-direction-property" target="_blank"><code>flex-direction</code></a> and <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/direction" target="_blank">writing mode</a> (<code>ltr</code> or <code>rtl</code>).</p>

<p><a href="https://i.stack.imgur.com/0mQqd.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/0mQqd.png" alt="enter image description here" /></div></a></p></li>
<li><p><strong><code>space-around</code></strong> ~ Same as <code>space-between</code> except with half-size spaces on both ends.</p>

<p><a href="https://i.stack.imgur.com/u4BH6.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/u4BH6.png" alt="enter image description here" /></div></a></p></li>
</ul>

<hr />

<h2>Auto Margins</h2>

<p>With <a href="http://www.w3.org/TR/css-flexbox-1/#auto-margins" target="_blank"><code>auto</code> margins</a>, flex items can be centered, spaced away or packed into sub-groups.</p>

<p>Unlike <code>justify-content</code>, which is applied to the flex container, <code>auto</code> margins go on flex items.</p>

<p>They work by consuming all free space in the specified direction.</p>

<hr />

<h3>Align group of flex items to the right, but first item to the left</h3>

<p>Scenario from the question:</p>

<blockquote>
  <ul>
  <li><p>making a group of flex items align-right (<code>justify-content: flex-end</code>)
  but have the first item align left (<code>justify-self: flex-start</code>)</p>
  
  <p><em>Consider a header section with a group of nav items and a logo. With
  <code>justify-self</code> the logo could be aligned left while the nav items stay
  far right, and the whole thing adjusts smoothly ("flexes") to
  different screen sizes.</em></p></li>
  </ul>
</blockquote>

<p><a href="https://i.stack.imgur.com/D3Vnv.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/D3Vnv.png" alt="enter image description here" /></div></a></p>

<p><a href="https://i.stack.imgur.com/Um8DM.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/Um8DM.png" alt="enter image description here" /></div></a></p>

<hr />

<p><strong><em>Other useful scenarios:</em></strong></p>

<p><a href="https://i.stack.imgur.com/qLzgU.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/qLzgU.png" alt="enter image description here" /></div></a></p>

<p><a href="https://i.stack.imgur.com/HtaOc.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/HtaOc.png" alt="enter image description here" /></div></a></p>

<p><a href="https://i.stack.imgur.com/M2WkZ.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/M2WkZ.png" alt="enter image description here" /></div></a></p>

<hr />

<h3>Place a flex item in the corner</h3>

<p>Scenario from the question:</p>

<blockquote>
  <ul>
  <li>placing a flex item in a corner <code>.box { align-self: flex-end; justify-self: flex-end; }</code></li>
  </ul>
</blockquote>

<p><a href="https://i.stack.imgur.com/BtbfK.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/BtbfK.png" alt="enter image description here" /></div></a></p>

<hr />

<h3>Center a flex item vertically and horizontally</h3>

<p><a href="https://i.stack.imgur.com/lV9a0.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/lV9a0.png" alt="enter image description here" /></div></a></p>

<p><code>margin: auto</code> is an alternative to <code>justify-content: center</code> and <code>align-items: center</code>.</p>

<p>Instead of this code on the flex container:</p>

<pre><code>.container {
    justify-content: center;
    align-items: center;
}</code></pre>

<p>You can use this on the flex item:</p>

<pre><code>.box56 {
    margin: auto;
}</code></pre>

<p>This alternative is useful when <a href="https://stackoverflow.com/q/33454533/3597276" target="_blank"><strong>centering a flex item that overflows the container</strong></a>.</p>

<hr />

<h3>Center a flex item, and center a second flex item between the first and the edge</h3>

<p>A flex container aligns flex items by distributing free space.</p>

<p>Hence, in order to create <em>equal balance</em>, so that a middle item can be centered in the container with a single item alongside, a counterbalance must be introduced.</p>

<p>In the examples below, invisible third flex items (boxes 61 & 68) are introduced to balance out the "real" items (box 63 & 66).</p>

<p><a href="https://i.stack.imgur.com/3IeTy.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/3IeTy.png" alt="enter image description here" /></div></a></p>

<p><a href="https://i.stack.imgur.com/BmtRt.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/BmtRt.png" alt="enter image description here" /></div></a></p>

<p>Of course, this method is nothing great in terms of semantics.</p>

<p>Alternatively, you can use a pseudo-element instead of an actual DOM element. Or you can use absolute positioning. All three methods are covered here: <strong><a href="https://stackoverflow.com/q/36191516/3597276" target="_blank">Center and bottom-align flex items</a></strong></p>

<p><em>NOTE: The examples above will only work – in terms of true centering – when the outermost items are equal height/width. When flex items are different lengths, see next example.</em></p>

<hr />

<h3>Center a flex item when adjacent items vary in size</h3>

<p>Scenario from the question:</p>

<blockquote>
  <ul>
  <li><p>in a row of three flex items, affix the middle item to the center of the container  (<code>justify-content: center</code>) and align the adjacent
  items to the container edges (<code>justify-self: flex-start</code> and
  <code>justify-self: flex-end</code>). </p>
  
  <p><em>Note that values <code>space-around</code> and <code>space-between</code> on <code>justify-content</code> property  will not keep the middle item centered in relation to the container if the adjacent items have different widths (<a href="http://jsfiddle.net/7an37m20/12/" target="_blank">see demo</a>).</em></p></li>
  </ul>
</blockquote>

<p>As noted, unless all flex items are of equal width or height (depending on <code>flex-direction</code>), the middle item cannot be truly centered. This problem makes a strong case for a <code>justify-self</code> property (designed to handle the task, of course).</p>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>
<p><em>Here are two methods for solving this problem:</em></p>

<p><strong><em>Solution #1: Absolute Positioning</em></strong></p>

<p>The flexbox spec allows for <a href="http://www.w3.org/TR/css-flexbox-1/#abspos-items" target="_blank">absolute positioning of flex items</a>. This allows for the middle item to be perfectly centered regardless of the size of its siblings.</p>

<p>Just keep in mind that, like all absolutely positioned elements, the items are removed from the <a href="https://www.w3.org/TR/CSS22/visuren.html#normal-flow" target="_blank">document flow</a>. This means they don't take up space in the container and can overlap their siblings. </p>

<p>In the examples below, the middle item is centered with absolute positioning and the outer items remain in-flow. But the same layout can be achieved in reverse fashion: Center the middle item with <code>justify-content: center</code> and absolutely position the outer items.</p>

<p><a href="https://i.stack.imgur.com/U1eLb.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/U1eLb.png" alt="enter image description here" /></div></a></p>

<p><strong><em>Solution #2: Nested Flex Containers (no absolute positioning)</em></strong></p>

<div>
<div>
<pre><code>.container {
  display: flex;
}
.box {
  flex: 1;
  display: flex;
  justify-content: center;
}
.box71 &gt; span { margin-right: auto; }
.box73 &gt; span { margin-left: auto;  }

/* non-essential */
.box {
  align-items: center;
  border: 1px solid #ccc;
  background-color: lightgreen;
  height: 40px;
}</code></pre>
<pre><code>&lt;div class="container"&gt;
  &lt;div class="box box71"&gt;&lt;span&gt;71 short&lt;/span&gt;&lt;/div&gt;
  &lt;div class="box box72"&gt;&lt;span&gt;72 centered&lt;/span&gt;&lt;/div&gt;
  &lt;div class="box box73"&gt;&lt;span&gt;73 loooooooooooooooong&lt;/span&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
<p>Here's how it works:</p>

<ul>
<li>The top-level div (<code>.container</code>) is a flex container.</li>
<li>Each child div (<code>.box</code>) is now a flex item.</li>
<li>Each <code>.box</code> item is given <code>flex: 1</code> in order to distribute container space equally.</li>
<li>Now the items are consuming all space in the row and are equal width.</li>
<li>Make each item a (nested) flex container and add <code>justify-content: center</code>.</li>
<li>Now each <code>span</code> element is a centered flex item.</li>
<li>Use flex <code>auto</code> margins to shift the outer <code>span</code>s left and right.</li>
</ul>

<p>You could also forgo <code>justify-content</code> and use <code>auto</code> margins exclusively.</p>

<p>But <code>justify-content</code> can work here because <code>auto</code> margins always have priority. From the spec:</p>

<blockquote>
  <p><a href="https://www.w3.org/TR/css-flexbox-1/#auto-margins" target="_blank"><strong>8.1. Aligning with <code>auto</code>
  margins</strong></a></p>
  
  <p>Prior to alignment via <code>justify-content</code> and <code>align-self</code>, any
  positive free space is distributed to auto margins in that dimension.</p>
</blockquote>

<hr />

<h3><em>justify-content: space-same (concept)</em></h3><p>Going back to <a href="https://stackoverflow.com/a/33856609/3597276" target="_blank"><code>justify-content</code></a> for a minute, here's an idea for one more option.</p>

<ul>
<li><strong><code>space-same</code></strong> ~ A hybrid of <code>space-between</code> and <code>space-around</code>. Flex items are evenly spaced (like <code>space-between</code>), except instead of half-size spaces on both ends (like <code>space-around</code>), there are full-size spaces on both ends.</li>
</ul>

<p>This layout can be achieved with <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/%3A%3Abefore" target="_blank"><code>::before</code></a> and <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/%3A%3Aafter" target="_blank"><code>::after</code></a> pseudo-elements on the flex container.</p>

<p><a href="https://i.stack.imgur.com/Jjw9w.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/Jjw9w.png" alt="enter image description here" /></div></a></p>

<p><em><sup>(credit: <a href="https://stackoverflow.com/a/34455480/3597276" target="_blank">@oriol</a> for the code, and <a href="https://stackoverflow.com/users/3183756/crl" target="_blank">@crl</a> for the label)</sup></em></p>

<p><strong>UPDATE:</strong> Browsers have begun implementing <strong><code>space-evenly</code></strong>, which accomplishes the above. See this post for details: <a href="https://stackoverflow.com/q/45134400/3597276" target="_blank">Equal space between flex items</a></p>

<hr />

<p><a href="http://jsfiddle.net/mz1ft6jx/8/" target="_blank"><strong>PLAYGROUND</strong></a> (includes code for all examples above)</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-33856609">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>13</b> more comments</a>
        </div>         
    </div>    </div>
</div>

  

<div id="answer-32583512">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        76
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I know not an answer but I like to contribute to this matter for what it's worth. It would be great if they could release <code>justify-self</code> for flexbox to make it truly flexible. </p>

<p>In my believe when there are multiple items on the axis, the most logical way for <code>justify-self</code> to behave is to align itself to it's nearest neighbors (or edge) as demonstrated below. </p>

<p>I truly hope, W3C watches this and will at least consider it. =)</p>

<p><a href="https://i.stack.imgur.com/wpSsJ.jpg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/wpSsJ.jpg" alt="enter image description here" /></div></a></p>

<p>This way you can have an item that is truly centered regardless of the size of the left and right box. When one of the boxes reaches the point of the center box it will simply push it until there is no more space to distribute.</p>

<p><a href="https://i.stack.imgur.com/NgobL.gif" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/NgobL.gif" alt="enter image description here" /></div></a></p>

<p>The ease of making awesome layouts are endless, take a look at this "complex" example.</p>

<p><a href="https://i.stack.imgur.com/U2ELF.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/U2ELF.png" alt="enter image description here" /></div></a></p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-32583512">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-32569434">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>This was asked on the www-style list, and Tab Atkins (spec editor) <a href="https://lists.w3.org/Archives/Public/www-style/2015Apr/0114.html" target="_blank">provided an answer explaining why</a>. I'll elaborate on that a bit here.</p>

<p>To start out, let's initially assume our flex container is single-line (<code>flex-wrap: nowrap</code>). In this case, there's clearly an alignment difference between the main axis and the cross axis -- there are multiple items stacked in the main axis, but only one item stacked in the cross axis. So it makes sense to have a customizeable-per-item "align-self" in the cross axis (since each item is aligned separately, on its own), whereas it doesn't make sense in the main axis (since there, the items are aligned collectively).</p>

<p>For multi-line flexbox, the same logic applies to each "flex line". In a given line, items are aligned individually in the cross axis (since there's only one item per line, in the cross axis), vs. collectively in the main axis.</p>

<hr />

<p>Here's another way of phrasing it: so, <em>all</em> of the <code>*-self</code> and <code>*-content</code> properties are about how to distribute extra space around things.  But the key difference is that the <code>*-self</code> versions are for cases where there's <em>only a single thing in that axis</em>, and the <code>*-content</code> versions are for when there are potentially <em>many things in that axis</em>. The one-thing vs. many-things scenarios are different types of problems, and so they have different types of options available -- for example, the <code>space-around</code> / <code>space-between</code> values make sense for <code>*-content</code>, but not for <code>*-self</code>.</p>

<p>SO: In a flexbox's main axis, there are many things to distribute space around. So a <code>*-content</code> property makes sense there, but not a <code>*-self</code> property.</p>

<p>In contrast, in the cross axis, we have both a <code>*-self</code> and a <code>*-content</code> property.  One determines how we'll distribute space around the <em>many</em> flex lines (<code>align-content</code>), and one determines how to distribute space around <em>individual</em> flex items in the cross axis, within a given flex line.</p>

<p>(I'm ignoring <code>*-items</code> properties here, since they simply establish defaults for <code>*-self</code>.)</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-32569434">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-41189508">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>There is <code>justify-self</code>, but in Chrome Canary, not in Chrome stable version. There is even <code>justify-items</code>:</p>

<p><a href="https://i.stack.imgur.com/RH8Bw.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/RH8Bw.png" alt="enter image description here" /></div></a></p>

<p>But as far as I can tell those properties do not work either. So probably Google saved it beforehand for future CSS releases. Can only hope they will add the properties soon.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 16 '16 at 17:25
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-41189508">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            <div>
                                
                                            <div>
        
                <div>
                    <div>
                        <h3>Sign up or <a href="/users/login?ssrc=question_page&returnurl=https%3a%2f%2fstackoverflow.com%2fquestions%2f32551291%2fin-css-flexbox-why-are-there-no-justify-items-and-justify-self-properties%23new-answer" id="login-link" target="_blank">log in</a></h3>
                        
                        <div>
                             Sign up using Google
                        </div>
                        <div>
                             Sign up using Facebook
                        </div>
                        <div>
                             Sign up using Email and Password
                        </div>
                    </div>
                    
                    
                    
                    
                    <div>
                                <h3>Post as a guest</h3>
    <div>
        <table>
        <tbody><tr>
                    <td>
                <div>
                    <label>Name</label>
                    
                </div>
                <div>
                    <label>Email</label>
                    
                </div>
            </td>
        </tr>
        </tbody></table>
    </div>

                    </div>
                </div>
            </div>
            
            

                            </div>

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>

<p>
By posting your answer, you agree to the <a href="https://stackexchange.com/legal/privacy-policy" name="privacy" target="_blank">privacy policy</a> and <a href="https://stackexchange.com/legal/terms-of-service" name="tos" target="_blank">terms of service</a>.</p>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/css" title="show questions tagged 'css'" target="_blank">css</a> <a href="/questions/tagged/css3" title="show questions tagged 'css3'" target="_blank">css3</a> <a href="/questions/tagged/flexbox" title="show questions tagged 'flexbox'" target="_blank">flexbox</a> <a href="/questions/tagged/language-lawyer" title="show questions tagged 'language-lawyer'" target="_blank">language-lawyer</a> <a href="/questions/tagged/w3c" title="show questions tagged 'w3c'" target="_blank">w3c</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="http://brolik.com/blog/when-to-use-flexbox/">http://brolik.com/blog/when-to-use-flexbox/</a><div id="articleHeader"><h1>When to use Flexbox</h1></div>
				

				
				By <a href="http://brolik.com/blog/author/alexcaldwell/" title="Posts by Alex Caldwell" target="_blank">Alex Caldwell</a>
				Tuesday December 22nd, 2015
				
										
		            
		            
				
								

				<hr />
			</section>

			<section>
				<p>The flexbox box layout is a great technological advancement on the web. In this article, I’ll share some tips on when to (and when not to) use flexbox with some Sass and jQuery for backwards compatibility.</p>			</section>

			<section>
				<p>Flexbox is a layout model that allows elements to align and distribute space within a container. Using flexible widths and heights, elements can be aligned to fill a space or distribute space between elements, which makes it a great tool to use for responsive design systems.</p>
<p>Flexbox has been around since 2009, and it’s beginning to be widely supported by all modern browsers. If you look at <a href="http://caniuse.com/#search=flexbox" target="_blank"><strong>Flexbox on Can I Use?</strong></a> you’ll see that it has great support across the board.</p>
<p><a href="http://caniuse.com/#search=flexbox" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="http://brolik.com/blog/wp-content/uploads/2015/12/Screen-Shot-2015-11-25-at-Nov-25-10.12.45-AM.png" alt="Can I use Flexbox?" /></div></a></p>
<p>There are some problems in IE8 and IE9, but that’s to be expected. At Brolik, we implement a fallback system using a <a href="http://brolik.com/flexbox/flexboxIE.scss" target="_blank">Sass style sheet</a> and a <a href="http://brolik.com/flexbox/flexboxIE.js" target="_blank">javascript file</a> to account for these older browsers.</p>
<p>We also use the Compass @include function to get specific browser prefixes, which you can find in this <a href="http://brolik.com/flexbox/flex.scss" target="_blank">Sass style sheet</a>. The line at the top “$flexbox-support-threshold: -3;” is to support the last three versions of flexbox, which is great for backward compatibility.</p>
<p>Obviously, feel free to use these three files on your own websites. Note, that we use Compass to compile our Sass.</p>
<h2>When not to use flexbox</h2>
<p>Before I talk about how useful flexbox is, I want to touch on when flexbox overcomplicates things.</p>
<p><strong>Don’t</strong> use flexbox for page layout. A basic grid system using percentages, max-widths, and media queries is a much safer approach for creating responsive page layouts. Optimally you’d use a grid system in conjunction with flexbox to achieve the most responsive website. Furthermore, because the flexbox layout is dependent upon content, issues can arise as the page loads. <a href="https://jakearchibald.com/2014/dont-use-flexbox-for-page-layout/" target="_blank">Jake Archibald has a good blog</a> explaining why it’s a bad idea to use flexbox for overall page layout.</p>
<p><strong>Don’t</strong> add display:flex; to every single container div. Ask yourself if flexbox really solves an alignment, scale, or ordering issue that can’t be solved in a simpler way with basic CSS.</p>
<p><strong>Don’t</strong> use flexbox if you have a lot of traffic from IE8 and IE9. While there are fallbacks (linked above), the experience won’t look the same.</p>
<h2>When to use flexbox</h2>
<p>Personally, I like to use flexbox for a few main things: scaling, vertically and horizontally aligning, and re-ordering elements within a container. These are best used on page components within a parent element. There are plenty of other uses for flexbox, like changing the direction of a column or row. But honestly, I prefer to use media-queries and percentage-based widths for creating columns and rows. Below, we’ll examine scaling, aligning, ordering, and wrapping with some flexbox CSS tips and CodePen examples.</p>
<h2>Scaling</h2>
<p>Flexbox is inherently good at dynamically scaling elements. I was very excited the first time I put display:flex; on a parent element and saw the child elements form a nice orderly queue with matching heights.</p>

<p>Matching heights vertically used to be somewhat difficult and would require jQuery after the page loaded. Now flexbox handles the vertical height and floats by default. It’s one of my favorite features of flexbox because I love orderly grids. The align-items property in flexbox defaults to “stretch,” which leads me into my favorite feature of flexbox.</p>
<h2>Vertical alignment</h2>
<p>You can vertically align all child elements with the align-items property on the parent container by setting it to flex-start, flex-end, center, baseline, or stretch (the default). Alternatively, you can align individual child elements with the property align-self. Below you’ll see these properties illustrated. I left stretch out because it is what naturally happens in the first example.</p>
<p>See the Pen <a href="http://codepen.io/ACaldy/pen/eJYYXR/" target="_blank">Flexbox Vertical Align</a> by Alex Caldwell (<a href="http://codepen.io/ACaldy" target="_blank">@ACaldy</a>) on <a href="http://codepen.io" target="_blank">CodePen</a>.</p>
<h2>Horizontal alignment</h2>
<p>Furthermore, you can horizontally align items by setting the justify-content property to either flex-start, flex-end, center, space-between, or space-around. I like to use it for creating responsive menus that start at desktop sizes.</p>

<p>The space-between property is particularly useful when you want to craft a responsive menu that fills the entire width of a desktop browser, like we did with the <a href="http://christinaseixacademy.org" target="_blank"><strong>Christina Seix Academy website.</strong></a></p>
<h2>Ordering</h2>
<p>Generally, I think that website hierarchy should naturally fall in the logical left to right and top to bottom order. With that being said, there are some instances when that doesn’t work within a design system, and therefore ordering is a really useful tool for responsive design.</p>
<p>For example, I like to use the <a href="http://webdesign.tutsplus.com/articles/understanding-the-split-layout-in-web-design--webdesign-9551" target="_blank">zig-zag layout</a> on content blocks that contain an image and some copy. It’s good for encouraging a user to scroll down the page and quickly skim the information. Eventually you run out of horizontal space as the width of the browser shrinks and you want to stack the image on top of the text. This is when the flexbox properties order and flex-wrap become useful.</p>
<p>See the Pen <a href="http://codepen.io/ACaldy/pen/eJpJYp/" target="_blank">Flexbox Ordering</a> by Alex Caldwell (<a href="http://codepen.io/ACaldy" target="_blank">@ACaldy</a>) on <a href="http://codepen.io" target="_blank">CodePen</a>.</p>
<p>Using a media query at a 600px browser width (resize your browser to see it in action), the flex-parent container gets the flex-wrap property which makes the child elements go to two lines. By default the child elements will always try to fit on one line with the default value of nowrap. At the same time, we move .flex-image to the first position with the property order:-1. The negative number overrides the inherent source order (1, 2, 3, etc.) and puts .flex-image at the beginning of the parent container. Overall, it’s a relatively simple way to control elements within a container for responsive design.</p>
<h2>In conclusion</h2>
<p>At Brolik we use flexbox on every project, but we’ve learned to use it sparingly.</p>
<blockquote><p><a href="https://twitter.com/intent/tweet?text=Not%20every%20container%20or%20element%20needs%20to%20have%20display%3Aflex%3B&url=http%3A%2F%2Fbrolik.com%2Fblog%2Fwhen-to-use-flexbox%2F&via=brolik" target="_blank">Not every container or element needs to have display:flex;</a></p></blockquote>
<p>You must know your project, audience, and the desired outcome and implement flexbox accordingly. Understand that you will still need to use some fallbacks for some of the older browsers, but it’s a very exciting piece of technology and a good indication of the evolution of modern web design.</p>
<p><a href="http://flexboxfroggy.com/" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="http://brolik.com/blog/wp-content/uploads/2015/12/Screen-Shot-2015-12-04-at-Dec-4-3.04.36-PM.png" alt="Flexbox Froggy Game" /></div></a></p>
<p>If you want some practice with flexbox check out the <a href="http://flexboxfroggy.com/" target="_blank">flexbox froggy game</a> to learn the basics of using flexbox.</p>
			</section>

			
		
<a href="https://www.smashingmagazine.com/2018/08/flexbox-alignment/?utm_source=mybridge&utm_medium=blog&utm_campaign=read_more">https://www.smashingmagazine.com/2018/08/flexbox-alignment/?utm_source=mybridge&utm_medium=blog&utm_campaign=read_more</a><div id="articleHeader"><h1>Everything You Need To Know About Alignment In Flexbox</h1></div>

					


					
						<div>
							<div>
    <div>
        <a href="/the-smashing-newsletter/" target="_blank" class="readableLinkWithLargeImage">
        <picture>
                <div class="readableLargeImageContainer float"><img src="https://d33wubrfki0l68.cloudfront.net/1dbc465f56f3a812f09666f522fa226efd947cfa/a4d9f/images/smashing-cat/newsletter-fish-cat.svg" alt="A postcat. Sign up for our Smashing Newsletter." /></div>
           </picture>
        </a>

          <div>
            <h2>Smashing Newsletter</h2>
            <p>Upgrade your inbox and get our editors’ picks twice a month.</p>
        </div>
    

    <div>
        
            <label>
                Your email
                
            </label>
            
        
    </div>

    <small>With <a href="/the-smashing-newsletter/" target="_blank">useful tips for web devs</a>. Sent 2× a month. <br />You can unsubscribe any time — <em>obviously</em>.</small>


						
					

					




					<p>
						
							In this article, we take a look at the alignment properties in Flexbox while discovering some basic rules to help remember how alignment on both the main and cross axis works.
						
	        </p>

					



        	

<p><a href="https://www.smashingmagazine.com/2018/08/flexbox-display-flex-container/" target="_blank">In the first article of this series</a>, I explained what happens when you declare <code>display: flex</code> on an element. This time we will take a look at the alignment properties, and how these work with Flexbox. If you have ever been confused about when to align and when to justify, I hope this article will make things clearer!</p>

<h3 id="history-of-flexbox-alignment">History Of Flexbox Alignment</h3>

<p>For the entire history of CSS Layout, being able to properly align things on both axes seemed like it might truly be the hardest problem in web design. So the ability to properly align items and groups of items was for many of us the most exciting thing about Flexbox when it first started to show up in browsers. Alignment became as simple as two lines of CSS:</p>




<p>The alignment properties that you might think of as the flexbox alignment properties are now fully defined in the <a href="https://www.w3.org/TR/css-align-3/" target="_blank">Box Alignment Specification</a>. This specification details how alignment works across the various layout contexts. This means that we can use the same alignment properties in CSS Grid as we use in Flexbox — and in future in other layout contexts, too. Therefore, any new alignment capability for flexbox will be detailed in the Box Alignment specification and not in a future level of Flexbox.</p>



<aside>
    <div>
      <div>
    <p>Nope, we can't do any magic tricks, but we have articles, <a href="https://smashed.by/perfpanelbooks" target="_blank">books</a> and <a href="https://smashed.by/perfpaneltv" target="_blank">webinars</a> featuring techniques we all can use to improve our work. <a href="https://smashed.by/perfpanelmembership" target="_blank">Smashing Members</a> get a seasoned selection of magic front-end tricks — e.g. <strong>live designing sessions</strong> and perf audits, too. <em>Just sayin'</em>! ;-)</p>

      <a href="https://smashed.by/perfpanelmembership" target="_blank">
        Explore Smashing Wizardry →
      </a>
      </div>
      <div>
        <a href="https://smashed.by/perfpanelmembership" target="_blank" class="readableLinkWithLargeImage">
        <div>
          <div class="readableLargeImageContainer float"><img src="https://www.smashingmagazine.com/images/smashing-cat/cat-wizard.svg"   alt="Smashing Cat, just preparing to do some magic stuff." /></div>
        
      </a>
      
    
  </aside>




<h3 id="the-properties">The Properties</h3>

<p>Many people tell me that they struggle to remember whether to use properties which start with <code>align-</code> or those which start with <code>justify-</code> in flexbox. The thing to remember is that:</p>

<ul>
<li><code>justify-</code> performs main axis alignment. Alignment in the same direction as your <code>flex-direction</code></li>
<li><code>align-</code> performs cross-axis alignment. Alignment across the direction defined by <code>flex-direction</code>.</li>
</ul>

<p>Thinking in terms of main axis and cross axis, rather than horizontal and vertical really helps here. It doesn’t matter which way the axis is physically.</p>

<h4 id="main-axis-alignment-with-justify-content">Main Axis Alignment With <code>justify-content</code></h4>

<p>We will start with the main axis alignment. On the main axis, we align using the <code>justify-content</code> property. This property deals with all of our flex items as a group, and controls how space is distributed between them.</p>

<p>The initial value of <code>justify-content</code> is <code>flex-start</code>. This is why, when you declare <code>display: flex</code> all your flex items line up against the start of the flex line. If you have a <code>flex-direction</code> of <code>row</code> and are in a left to right language such as English, then the items will start on the left.</p>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67648629-b445-429f-9fd4-0fb47b7875ef/justify-content-flex-start.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67648629-b445-429f-9fd4-0fb47b7875ef/justify-content-flex-start.png" alt="The items are all lined up in a row starting on the left" /></div>
	</a>

	
		<figcaption>
			The items line up to the start (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67648629-b445-429f-9fd4-0fb47b7875ef/justify-content-flex-start.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>Note that the <code>justify-content</code> property can only do something <strong>if there is spare space to distribute</strong>. Therefore if you have a set of flex items which take up all of the space on the main axis, using <code>justify-content</code> will not change anything.</p>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/064418da-c45c-4fbf-9b4e-65c481c05c00/justify-content-no-space.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/064418da-c45c-4fbf-9b4e-65c481c05c00/justify-content-no-space.png" alt="The container is filled with the items" /></div>
	</a>

	
		<figcaption>
			There is no space to distribute (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/064418da-c45c-4fbf-9b4e-65c481c05c00/justify-content-no-space.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>If we give <code>justify-content</code> a value of <code>flex-end</code> then all of the items will move to the end of the line. The spare space is now placed at the beginning.</p>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/262c2132-a9bf-4c6c-90cd-4ec445c9f3e1/justify-content-flex-end.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/262c2132-a9bf-4c6c-90cd-4ec445c9f3e1/justify-content-flex-end.png" alt="The items are displayed in a row starting at the end of the container — on the right" /></div>
	</a>

	
		<figcaption>
			The items line up at the end (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/262c2132-a9bf-4c6c-90cd-4ec445c9f3e1/justify-content-flex-end.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>We can do other things with that space. We could ask for it to be distributed <em>between</em> our flex items, by using <code>justify-content: space-between</code>. In this case, the first and last item will be flush with the ends of the container and all of the space shared equally between the items.</p>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0df6bac-5250-47d2-82ed-da66306e7c95/justify-content-space-between.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0df6bac-5250-47d2-82ed-da66306e7c95/justify-content-space-between.png" alt="Items lined up left and right with equal space between them" /></div>
	</a>

	
		<figcaption>
			The spare space is shared out between the items (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0df6bac-5250-47d2-82ed-da66306e7c95/justify-content-space-between.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>We can ask that the space to be distributed around our flex items, using <code>justify-content: space-around</code>. In this case, the available space is shared out and placed on each side of the item.</p>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acab1663-6d66-4d98-9d1c-2f2b98911bbe/justify-content-space-around.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acab1663-6d66-4d98-9d1c-2f2b98911bbe/justify-content-space-around.png" alt="Items spaced out with even amounts of space on each side" /></div>
	</a>

	
		<figcaption>
			The items have space either side of them (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acab1663-6d66-4d98-9d1c-2f2b98911bbe/justify-content-space-around.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>A newer value of <code>justify-content</code> can be found in the Box Alignment specification; it doesn’t appear in the Flexbox spec. This value is <code>space-evenly</code>. In this case, the items will be evenly distributed in the container, and the extra space will be shared out between and either side of the items.</p>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8960c00-dd71-4147-bd7a-7a32bc98f08a/justify-content-space-evenly.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8960c00-dd71-4147-bd7a-7a32bc98f08a/justify-content-space-evenly.png" alt="Items with equal amounts of space between and on each end" /></div>
	</a>

	
		<figcaption>
			The items are spaced evenly (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8960c00-dd71-4147-bd7a-7a32bc98f08a/justify-content-space-evenly.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>You can play with all of the values in the demo:</p>




<p>These values work in the same way if your <code>flex-direction</code> is <code>column</code>. You may not have extra space to distribute in a column however unless you add a height or block-size to the flex container as in this next demo.</p>




<h4 id="cross-axis-alignment-with-align-content">Cross Axis Alignment with <code>align-content</code></h4>

<p>If you have added <code>flex-wrap: wrap</code> to your flex container, and have multiple flex lines then you can use <code>align-content</code> to align your flex lines on the cross axis. However, this will require that you have additional space on the cross axis. In the below demo, my cross axis is running in the block direction as a column, and I have set the height of the flex container to <code>60vh</code>. As this is more than is needed to display my flex items I have spare space vertically in the container.</p>

<p>I can then use <code>align-content</code> with any of the values:</p>




<p>If my <code>flex-direction</code> were <code>column</code> then <code>align-content</code> would work as in the following example.</p>




<p>As with <code>justify-content</code>, we are working with the lines as a group and distributing the spare space.</p>






<h3 id="the-place-content-shorthand">The <code>place-content</code> Shorthand</h3>

<p>In the Box Alignment, we find the shorthand <code>place-content</code>; using this property means you can set <code>justify-content</code> and <code>align-content</code> at once. The first value is for <code>align-content</code>, the second for <code>justify-content</code>. If you only set one value then both values are set to that value, therefore:</p>

<pre><code>.container {
    place-content: space-between stretch;
}</code><div><div><a target="_blank">Copy</a></div></pre>

<p>Is the same as:</p>

<pre><code>.container {
    align-content: space-between; 
    justify-content: stretch;
}</code><div><div><a target="_blank">Copy</a></div></pre>

<p>If we used:</p>

<pre><code>.container {
    place-content: space-between;
}</code><div><div><a target="_blank">Copy</a></div></pre>

<p>This would be the same as:</p>

<pre><code>.container {
    align-content: space-between; 
    justify-content: space-between;
}</code><div><div><a target="_blank">Copy</a></div></pre>

<h4 id="cross-axis-alignment-with-align-items">Cross Axis Alignment With <code>align-items</code></h4>

<p>We now know that we can align our set of flex items or our flex lines as a group. However, there is another way we might wish to align our items and that is to align items in relationship to each other on the cross axis. Your flex container has a height. That height might be defined by the height of the tallest item as in this image.</p>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dabd13bf-bf9c-411f-86c0-d43cdfb935fe/container-height-of-item.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dabd13bf-bf9c-411f-86c0-d43cdfb935fe/container-height-of-item.png" alt="The container height is tall enough to contain the items, the third item has more content" /></div>
	</a>

	
		<figcaption>
			The container height is defined by the third item (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dabd13bf-bf9c-411f-86c0-d43cdfb935fe/container-height-of-item.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>It might instead be defined by adding a height to the flex container:</p>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c477a442-ea29-48cf-bed9-94b75593a1b2/container-added-height.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c477a442-ea29-48cf-bed9-94b75593a1b2/container-added-height.png" alt="The container height is taller than needed to display the items" /></div>
	</a>

	
		<figcaption>
			The height is defined by a size on the flex container (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c477a442-ea29-48cf-bed9-94b75593a1b2/container-added-height.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>The reason that flex items appear to stretch to the size of the tallest item is that the initial value of <code>align-items</code> is <code>stretch</code>. The items stretch on the cross axis to become the size of the flex container in that direction.</p>

<p>Note that where <code>align-items</code> is concerned, if you have a multi-line flex container, each line acts like a new flex container. The tallest item in that line would define the size of all items in that line.</p>

<p>In addition to the initial value of stretch, you can give <code>align-items</code> a value of <code>flex-start</code>, in which case they align to the start of the container and no longer stretch to the height.</p>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7da24e8b-8d18-4ada-9f0e-e417e0293607/align-items-flex-start.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7da24e8b-8d18-4ada-9f0e-e417e0293607/align-items-flex-start.png" alt="The items are aligned to the start" /></div>
	</a>

	
		<figcaption>
			The items aligned to the start of the cross axis (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7da24e8b-8d18-4ada-9f0e-e417e0293607/align-items-flex-start.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>The value <code>flex-end</code> moves them to the end of the container on the cross axis.</p>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52d4c377-8c60-4336-be64-f01cb9a20833/align-items-flex-end.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52d4c377-8c60-4336-be64-f01cb9a20833/align-items-flex-end.png" alt="Items aligned to the end of the cross axis" /></div>
	</a>

	
		<figcaption>
			The items aligned to the end of the cross axis (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52d4c377-8c60-4336-be64-f01cb9a20833/align-items-flex-end.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>If you use a value of <code>center</code> the items all centre against each other:</p>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ccb2aba-b692-4ba5-8827-1043674fc1d4/align-items-center.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ccb2aba-b692-4ba5-8827-1043674fc1d4/align-items-center.png" alt="The items are centered" /></div>
	</a>

	
		<figcaption>
			Centering the items on the cross axis (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ccb2aba-b692-4ba5-8827-1043674fc1d4/align-items-center.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>We can also do baseline alignment. This ensures that the baselines of text line up, as opposed to aligning the boxes around the content.</p>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6607e8bc-9f6b-43a6-9b13-24bff76068f1/align-items-baseline.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6607e8bc-9f6b-43a6-9b13-24bff76068f1/align-items-baseline.png" alt="The items are aligned so their baselines match" /></div>
	</a>

	
		<figcaption>
			Aligning the baselines (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6607e8bc-9f6b-43a6-9b13-24bff76068f1/align-items-baseline.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>You can try these values out in the demo:</p>




<h4 id="individual-alignment-with-align-self">Individual Alignment With <code>align-self</code></h4>

<p>The <code>align-items</code> property means that you can set the alignment of all of the items at once. What this really does is set all of the <code>align-self</code> values on the individual flex items as a group. You can also use the <code>align-self</code> property on any individual flex item to align it inside the flex line and against the other flex items.</p>

<p>In the following example, I have used <code>align-items</code> on the container to set the alignment for the group to <code>center</code>, but also used <code>align-self</code> on the first and last items to change their alignment value.</p>




<h3 id="why-is-there-no-justify-self">Why Is There No <code>justify-self</code>?</h3>

<p>A common question is why it is not possible to align one item or a group of the items on the main axis. Why is there no <code>-self</code> property for main axis alignment in Flexbox? If you think about <code>justify-content</code> and <code>align-content</code> as being about space distribution, the reason for their being no self-alignment becomes more obvious. We are dealing with the flex items as a group, and distributing available space in some way — either at the start or end of the group or between the items.</p>

<p>If might be also helpful to think about how <code>justify-content</code> and <code>align-content</code> work in CSS Grid Layout. In Grid, these properties are used to distribute spare space in the grid container <em>between grid tracks</em>. Once again, we take the tracks as a group, and these properties give us a way to distribute any extra space between them. As we are acting on a group in both Grid and Flexbox, we can’t target an item on its own and do something different with it. However, there is a way to achieve the kind of layout that you are asking for when you ask for a <code>self</code> property on the main axis, and that is to use auto margins.</p>






<h4 id="using-auto-margins-on-the-main-axis">Using Auto Margins On The Main Axis</h4>

<p>If you have ever centered a block in CSS (such as the wrapper for your main page content by setting a margin left and right of <code>auto</code>), then you already have some experience of how auto margins behave. A margin set to auto will try to become as big as it can in the direction it has been set in. In the case of using margins to center a block, we set the left and right both to auto; they each try and take up as much space as possible and so push our block into the center.</p>

<p>Auto margins work very nicely in Flexbox to align single items or groups of items on the main axis. In the next example, I am achieving a common design pattern. I have a navigation bar using Flexbox, the items are displayed as a row and are using the initial value of <code>justify-content: start</code>. I would like the final item to be displayed separated from the others at the end of the flex line — assuming there is enough space on the line to do so.</p>

<p>I target that item and give it a margin-left of auto. This then means that the margin tries to get as much space as possible to the left of the item, which means the item gets pushed all the way over to the right.</p>




<p>If you use auto margins on the main axis then <code>justify-content</code> will cease to have any effect, as the auto margins will have taken up all of the space that would otherwise be assigned using <code>justify-content</code>.</p>

<h3 id="fallback-alignment">Fallback Alignment</h3>

<p>Each alignment method details a fallback alignment, this is what will happen if the alignment you have requested can’t be achieved. For example, if you only have one item in a flex container and ask for <code>justify-content: space-between</code>, what should happen? The answer is that the fallback alignment of <code>flex-start</code> is used and your single item will align to the start of the flex container. In the case of <code>justify-content: space-around</code>, a fallback alignment of <code>center</code> is used.</p>

<p>In the current specification you can’t change what the fallback alignment is, so if you would prefer that the fallback for <code>space-between</code> was <code>center</code> rather than <code>flex-start</code>, there isn’t a way to do that. There is <a href="https://www.w3.org/TR/css-align-3/#distribution-values" target="_blank">a note in the spec</a> which says that future levels may enable this.</p>

<h3 id="safe-and-unsafe-alignment">Safe And Unsafe Alignment</h3>

<p>A more recent addition to the Box Alignment specification is the concept of safe and unsafe alignment using the <em>safe</em> and <em>unsafe</em> keywords.</p>

<p>With the following code, the final item is too wide for the container and with unsafe alignment and the flex container on the left-hand side of the page, the item becomes cut off as the overflow is outside the page boundary.</p>

<pre><code>.container {  
    display: flex;
    flex-direction: column;
    width: 100px;
    align-items: unsafe center;
}

.item:last-child {
    width: 200px;
}</code><div><div><a target="_blank">Copy</a></div></pre>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54359e1a-e4e4-445a-8fcc-e4ef59591bad/unsafe-alignment.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54359e1a-e4e4-445a-8fcc-e4ef59591bad/unsafe-alignment.png" alt="The overflowing item is centered and partly cut off" /></div>
	</a>

	
		<figcaption>
			Unsafe alignment will give you the alignment you asked for but may cause data loss (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54359e1a-e4e4-445a-8fcc-e4ef59591bad/unsafe-alignment.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>A safe alignment would prevent the data loss occurring, by relocating the overflow to the other side.</p>

<pre><code>.container {  
    display: flex;
    flex-direction: column;
    width: 100px;
    align-items: safe center;
}

.item:last-child {
    width: 200px;
}</code><div><div><a target="_blank">Copy</a></div></pre>











<figure>
	<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e31128f-cc18-430d-aa06-9a5307021d0c/safe-alignment.png" target="_blank" class="readableLinkWithLargeImage">
		<div class="readableLargeImageContainer"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e31128f-cc18-430d-aa06-9a5307021d0c/safe-alignment.png" alt="The overflowing item overflows to the right" /></div>
	</a>

	
		<figcaption>
			Safe alignment tries to prevent data loss (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e31128f-cc18-430d-aa06-9a5307021d0c/safe-alignment.png" target="_blank">Large preview</a>)
		</figcaption>
	
</figure>


<p>These keywords have limited browser support right now, however, they demonstrate the additional control being brought to Flexbox via the Box Alignment specification.</p>




<h3 id="in-summary">In Summary</h3>

<p>The alignment properties started as a list in Flexbox, but are now in their own specification and apply to other layout contexts. A few key facts will help you to remember how to use them in Flexbox:</p>

<ul>
<li><code>justify-</code> the main axis and <code>align-</code> the cross axis;</li>
<li>To use <code>align-content</code> and <code>justify-content</code> you need spare space to play with;</li>
<li>The <code>align-content</code> and <code>justify-content</code> properties deal with the items as a group, sharing out space. Therefore, you can’t target an individual item and so there is no <code>-self</code> alignment for these properties;</li>
<li>If you do want to align one item, or split a group on the main axis, use auto margins to do so;</li>
<li>The <code>align-items</code> property sets all of the <code>align-self</code> values as a group. Use <code>align-self</code> on the flex child to set the value for an individual item.</li>
</ul>

<div>
  <img src="https://www.smashingmagazine.com/images/logo/logo--red.png" alt="Smashing Editorial" />
  (il)
</div>


				
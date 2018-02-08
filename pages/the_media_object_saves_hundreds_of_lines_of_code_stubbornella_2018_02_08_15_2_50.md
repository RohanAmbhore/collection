<a href="http://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code/">http://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code/</a><div id="articleHeader"><h1>The media object saves hundreds of lines of code</h1></div>
			

	
	

		
		<p>What is the internet made of? At least the UI layer is mainly composed of media blocks. I talked about the Facebook <a href="http://www.stubbornella.org/content/2010/06/21/css-granularity-architecture/" target="_blank">stream story before, and all the tiny objects of which it is composed</a>. For the most part, the stream story is made up of the media object repeated over and over.</p>
<p>The <em>media object</em> is an image to the left, with descriptive content to the right, like this Facebook story:</p>
<div id="attachment_468"><img src="http://www.stubbornella.org/content/wp-content/uploads/2010/06/media11.png" width="346" height="54" alt="image to the left, descriptive content to the right" title="media1" /><p>The media object</p></div>
<p>The content area on the right can contain any other objects. In this case, it contains text, but we could put lists, grids, or even other media objects inside. As we’ve seen before, there are actually many different versions of the media block on the Facebook website (and on most websites). These five are just a few examples of the way this object might be used:</p>
<div id="attachment_468"><div class="readableLargeImageContainer"><img src="http://www.stubbornella.org/content/wp-content/uploads/2010/06/5mediaBlocks.png"   title="5mediaBlocks" /></div><p>Variations on the media object</p></div>
<p>Sometimes the image is a tiny icon, a large video, or an avatar, but it is the same basic object. When I’m building a new object, the first thing I do is to figure out which parts are reusable components, and define what I <strong>know</strong> and <strong>do not know</strong> about them.</p>
<h3>what do we know?</h3>
<ul>
<li> Can be nested
  </li>
<li>Optional right button
  </li>
<li>Must clearfix
</li>
</ul>
<h3>What have we decided *not* to know? (Think flexibility!)</h3>
<p>It is equally important to define what is flexible, or unknown, about a new object.</p>
<ul>
<li>Image width, margins, and decoration vary
  </li>
<li>Right content is unknown
  </li>
<li>Width unknown
</li>
</ul>
<p>Once it is built, we can use it to create many of the same basic object. In the following image, I’ve highlighted all the media objects on the facebook homepage. You can see that even implementing this one object can save a ton of code because we stop repeating ourselves.</p>
<div>
          <div id="attachment_504"><div class="readableLargeImageContainer float"><img src="http://www.stubbornella.org/content/wp-content/uploads/2010/06/Facebook-ImageBlock-216x1024.png"   alt="media block use" title="Facebook-ImageBlock" /></div><p>The media object highlighted in red on the facebook homepage</p></div><div>
<h2>Implementation Details</h2>
<p>           How does it work? The hard part is making sure that the image can be any width, so that the element is reusable. It means our content area needs to be flexible so that it can fill in all the remaining space available. We’ll have to create a new formatting context to make a flexible column.</p>
<p>The HTML:</p>
<pre>&lt;div class="media attribution"&gt;<br />
  &lt;a href="http://twitter.com/stubbornella" class="img"&gt;
    &lt;img src="http://stubbornella.com/profile_image.jpg" alt="me" /&gt;
  &lt;/a&gt;<br />
  &lt;div class="bd"&gt;
    @Stubbornella 14 minutes ago
  &lt;/div&gt;<br />
&lt;/div&gt;
</pre>
<p>The CSS:</p>
<pre>/* ====== media ====== */
.media {margin:10px;}
.media, .bd {overflow:hidden; _overflow:visible; zoom:1;}
.media .img {float:left; margin-right: 10px;}
.media .img img{display:block;}
.media .imgExt{float:right; margin-left: 10px;}
</pre>
<ol>
<li>We clearfix both the wrapper element, media, and the inner content wrapper, bd (body) using the <a href="http://www.stubbornella.org/content/2009/07/23/overflow-a-secret-benefit/" target="_blank">secret benefits of overflow</a>. There are other ways we could have implemented the clearfix plus new formatting context. More on that in a later post.</li>
<li>Then we float our image wrapper (generally a link) left and our optional right region to the right. </li>
<li>Finally, we set some margins and paddings to keep everything lining up nicely. You might choose to set margins via a class which extends the .img object if you have several different kinds of images with different spacing and decoration.</li>
</ol>
<p>Voila, we’re done. It is a very simple object, but it is very powerful. We can eliminate a lot of lines of code abstracting this repeating pattern. The code for the media block and many other “web Lego” are available on the <a href="http://wiki.github.com/stubbornella/oocss/" target="_blank">Object Oriented CSS open source project</a>.
        </p></div>
</div>
	
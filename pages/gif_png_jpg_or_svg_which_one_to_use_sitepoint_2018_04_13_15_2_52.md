<a href="https://www.sitepoint.com/gif-png-jpg-which-one-to-use/">https://www.sitepoint.com/gif-png-jpg-which-one-to-use/</a><div id="articleHeader"><h1>GIF, PNG, JPG or SVG. Which One To Use? — SitePoint</h1></div>
      <p>If this article feels a little familiar, we published the first edition of it way back in 2009. While SVG has added a whole new dimension to web design, questions such as “What is the difference between JPEG and PNG?” are still as relevant as ever. We thought it was time to take a fresh look at the state of play in web-image formats.</p>
<p>Today’s short guide will give you the quick rundown of the various file types and where they work best. Enjoy.</p>
<h2>JPG vs PNG vs GIF vs SVG – What is the Difference?</h2>
<table><tbody><tr><td> </td>
<td>Category</td>
<td>Palette</td>
<td>Use for</td>
</tr><tr><td>JPG</td>
<td>Lossy</td>
<td>Millions of colors</td>
<td>Still Images<br />
			Photography</td>
</tr><tr><td>GIF</td>
<td>Lossless</td>
<td>Maximum 256 colors</td>
<td>Simple animations<br />
			Graphics with flat colors<br />
			Graphics without gradients</td>
</tr><tr><td>PNG-8</td>
<td>Lossless</td>
<td>Maximum 256 colors</td>
<td>Similar to GIF<br />
			Better transparency but no animation<br />
			Great for icons</td>
</tr><tr><td>PNG-24</td>
<td>Lossless</td>
<td>Unlimited colors</td>
<td>Similar to PNG-8<br />
			Handles still images and transparency</td>
</tr><tr><td>SVG</td>
<td>Vector/lossless</td>
<td>Unlimited colors</td>
<td>Graphics/logos for web<br />
			Retina/high-dpi screens</td>
</tr></tbody></table><h2>GIF: The Graphic Interchange Format</h2>
<div id="attachment_148665"><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2009/08/1486518514palette.jpg"   alt="256 color palette." /></div><p>256 color palette.</p></div>
<p>Unless you just stepped out of a <a href="https://en.wikipedia.org/wiki/DeLorean_time_machine" target="_blank">faintly smoking DeLorean straight from 1985</a>, you’re very likely already familiar with the web’s goofiest image format – the <a href="https://en.wikipedia.org/wiki/GIF" target="_blank">GIF</a> (Graphics Interchange Format).</p>
<p>The GIF format is a type of bitmap, but unlike JPEG or PNG, GIF files are limited to a maximum palette of 256 colors. Essentially each GIF image contains a preset ‘box of crayons’ and there is no way to truly mix those colors to make <strong><em>new</em></strong> colors.</p>
<p>While 256 might <strong><em>sound</em></strong> like a lot of crayons to work with, complex photographs typically have many thousands of tones. This color range is lost during the GIF conversion process and this is the key reason not to use GIF for color photos.</p>
<p>While GIF is generally a poor choice for images with wide color variation, that 256 color limit can help keep file sizes small which is ideal for even the slowest of internet speeds. For many years, GIF provided the web’s only transparency option – though PNG and SVG now offer this too.</p>
<h3>Category: Lossless</h3>
<h3>Choose GIF for:</h3>
<ul><li>Simple animations</li>
<li>Small icons</li>
<li>Graphics with low pixel-to-pixel variation (i.e. lots of flat color like logos and flags)</li>
</ul>
<p>Depending on your preference, you may refer to this format as either ‘JPEG’ or ‘JPG’ – both are accepted variations of the same acronym – <a href="https://en.wikipedia.org/wiki/JPEG" target="_blank">Joint Photographic Experts Group</a>.</p>
<p>Unlike GIF, JPEG is a 16-bit format, which means that it can blend red, blue and green light to display millions of color. This makes JPG very ‘photo-friendly’. This is partly why it is a standard format when it comes to most digital cameras on the market.</p>
<p>The JPEG format also allows you the flexibility to choose the how much you compress your image – from 0% (heavy compression) to 100% (no compression). Generally, a 60%-75% compression setting will shrink your file considerably while keeping your image looking decent on most screens.</p>
<p>While JPEG is well suited to compressing and rendering photography, it is a lossy compression type which means it’s less useful for ongoing editing of an image. Exporting a JPEG results in a loss of quality, and these losses get worse with each successive export – like a photocopy of a photocopy. This is why professional photographers generally shoot in lossless <a href="https://en.wikipedia.org/wiki/Raw_image_format" target="_blank">RAW</a> format.</p>
<p>Also note that, unlike the GIF and PNG, JPEG can not preserve transparency.</p>
<h3>Category: Lossy</h3>
<h3>Use JPEG for:</h3>
<ul><li>Still Images</li>
<li>Photography</li>
<li>Images with complex colors and dynamic</li>
</ul>
<p>A newer file format than GIF and JPEG, the PNG (Portable Network Graphics) is like a marriage between both the GIF and JPEG format thanks to its two variants.</p>
<h4>PNG-8</h4>
<p>PNG-8 is similar to GIF in many ways and uses the same 256 color palette (maximum). It has better transparency options and usually exports slightly smaller file sizes. However, PNG-8 has no animation function.</p>
<h4>PNG-24</h4>
<p>PNG-24 allows you to render images with millions of colors – much like JPEG – but also offers the ability to preserve transparency. Because PNG-24 is a lossless format file type, you are likely to get larger files, but if image quality is more important than file size, PNG-24 is your best option. Even so, services like <a href="https://tinypng.com/" target="_blank">TinyPNG.com</a> can often make a big difference to your file size. Compared to their cousin JPEG, PNG-24 files are not as universally compatible with every app and platform which makes the format marginally less ideal for web sharing. However, it is capable of being edited without diminished qualities.</p>
<h3>Category: Lossless</h3>
<h3>Use PNG for:</h3>
<ul><li>Web graphics that require transparency</li>
<li>Color heavy and complex photographs and graphics</li>
<li>Images that require re-editing and re-exporting</li>
</ul>
<p>Unlike the three formats mentioned above, SVG (Scalable Vector Graphics) is not a pure bitmap format. Instead it is a vector format – a close cousin to Adobe Illustrator’s AI format and EPS – that is steadily becoming an attractive option for web and UI designers.</p>
<p>Sometimes it’s helpful to think of SVG as ‘HTML for illustrations’ and you need to think about it quite differently to other image formats we’ve listed.</p>
<p>SVG is best-suited to displaying logos, icons, maps, flags, charts, and other graphics created in vector graphics applications like Illustrator, Sketch, and Inkscape. Written in an XML-based markup, your SVG can be edited in any text editor and modified by JavaScript or CSS. As vectors can be scaled to any size while retaining crisp image quality, they are ideal for responsive design.</p>
<p>Though SVG is a vector format at its core, it is possible (even common) to embed bitmap graphics <strong><em>inside</em></strong> your SVG file – just as you might embed JPEGs in your HTML.</p>
<p>You can do this by either linking to an image source via its URL (as you might link to JPG in a webpage) or by encapsulating the pixel image as a <a href="https://en.wikipedia.org/wiki/Data_URI_scheme" target="_blank">Data URI</a>. This gives SVG unchallenged flexibility and power.</p>
<p>Though SVG can help keep your images looking beautiful on the web, it isn’t necessarily a format that the everyday person can utilize to save and upload images via their website or social media platforms.</p>
<p>Online services like WordPress, Flickr, Medium, Tumblr, and Facebook will either forcibly convert your SVG to a format they like, or – more likely – outright block your SVG upload. There are a handful of SVG hosting options including <a href="http://svgur.com/" target="_blank">svgur.com</a>, <a href="https://imgh.us" target="_blank">imgh.us</a> and even <a href="https://www.sitepoint.com/why-hosting-your-svgs-is-hard-and-how-to-beat-it/" target="_blank">Github, as Alex demonstrated here</a>.</p>
<p>As happy as I am to see smaller hosting services tackle SVG, Github is currently the only SVG-friendly service I’d be 99% confident will be around in 5 years. If you are using SVG to design for the web, you will find that you can almost always reduce file size when compared to something like the JPEG or PNG. But note that the more complex your SVG the larger the file will become.</p>
<h3 id="category-vectorlossless">Category: Vector/Lossless</h3>
<h3 id="use-3">Use SVG for:</h3>
<ul><li>Logos and icon with strong, geometric, vector-friendly design</li>
<li>Graphics that may need to be displayed in multiple sizes and screens</li>
<li>Graphics that respond to their device</li>
<li>Graphics that need to be edied, updated and redeployed.</li>
</ul><h2 id="compare-and-contrast">Compare and Contrast</h2>
<p>Now that we have covered the differences between popular file formats it is time to see them side by side. Below you will see how GIF, JPEG, PNG and SVG formats handle images with both simple and complex colors along with photographic images.</p>
<h3>Flat Color Graphics</h3>
<p>The first type of image we’re going to look at are flat color graphics. This covers most logos and branding, icons, simple maps, charts, and diagrams. The original image is a 23.4 KB PNG image with a 1280 x 1280 dimension.</p>
<p>Below you will be able to see the difference in compression size as well as image quality. Note the images were saved using Photoshop’s “Save for Web and Devices” option at the highest quality settings.</p>
<h4>GIF: 17.6 KB</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/1486514787VxhCRE1.gif"   alt="GIF" /></div></p>
<h4>JPEG 100% (no compression): 53.3 KB</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/14865148461vNNhMD.jpg"   alt="JPG" /></div></p>
<h4>JPEG 75%: 33 KB</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/14865155381vNNhMD-75-2.jpg"   alt="JPEG: 75% quality" /></div></p>
<h4>PNG-8: 11.8 KB</h4>
<p><div class="readableLargeImageContainer"><img src="https://i.imgur.com/jDK67ry.png" alt="enter image description here" /></div></p>
<h4>PNG-24: 19.6 KB</h4>
<p><div class="readableLargeImageContainer"><img src="https://i.imgur.com/1svnpnX.png" alt="enter image description here" /></div></p>
<h4>SVG: 6 KB (as a pure vector graphic)</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/1486513498pc-1776996.svg" alt="SVG" /></div> In the case of this particular image, there isn’t much loss in quality when you compare the six formats – though you’ll notice slight artifacts near edges inside the compressed JPEG. This isn’t always true with flat color graphics, but in most cases, you should be fine with going with the least byte-heavy image. For this image, assuming we have the original vector file, SVG is the obvious choice at 6kb. If we don’t have the vector, the PNG-8 option is a decent fallback with our original image dropping from 23.4 KB to 11.8 KB.</p>
<h3>Complex Color Images</h3>
<p>The original image is a 328 KB JPEG image with a 1280 x 960 dimension. Below you will be able to see the difference in compression size as well as image quality. Note the images were saved using Photoshop’s “Save for Web and Devices” option at the highest quality settings.</p>
<p>As we don’t have access to a vector version of this file, any SVG version of this image would just be a JPEG embedded inside an SVG. This makes it a little redundant, so I won’t offer an SVG example here.</p>
<h4>GIF: 426kb</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/1486516221gif-color.gif"   alt="GIF - 426kb" /></div></p>
<h4>JPEG 100% (no compression): 776 KB</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/1486516304fUEIj69.jpg"   alt="JPG 100" /></div></p>
<h4>JPEG 75%: 215 KB</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/1486516361fUEIj69-75.jpg"   alt="JPG-75: 215kg" /></div></p>
<h4>PNG-8: 327 KB</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/1486516486Udg2jTH.png"   alt="PNG8 - 335kb" /></div></p>
<h4>PNG-24: 1.7 MB</h4>
<p><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/1486516806mandala-1063242_1280.png" width="1280" height="960" alt="PNG-24: 1.7MB" /></p>
<p>Images that have complex colors tend to look better when using a JPEG, PNG-24 or SVG format. Colors are for the most part preserved and don’t have ugly banding and noise that you are likely to get with GIF and PNG-8 formats.</p>
<h3>Color Photography</h3>
<p>The original image is a 215 KB JPEG image with a 1280 x 701 dimension. Below you will be able to see the difference in compression size as well as image quality. Note the images were saved using Photoshop’s “Save for Web and Devices” option at the highest quality settings.</p>
<p>Again, there’s little to be gained with an SVG offering here.</p>
<h4>GIF: 453 KB</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/1486516880XXG21LJ.gif"   alt="GIF: 463kb" /></div></p>
<h4>JPEG 100% (No compression): 410 KB</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/1486516928OuDc0y3.jpg"   alt="JPEG 100% : 419kb" /></div></p>
<h4>JPEG 75% : 410 KB</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/1486517067OuDc0y3-75.jpg"   alt="JPG 75%: 105kb" /></div></p>
<h4>PNG-8: 395 KB</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/1486517241NFYYtqp.png"   alt="PNG-8 " /></div></p>
<h4>PNG-24: 1.03 MB</h4>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/02/1486517309OuDc0y3-24.png"   alt="PNG-24 1.2MB " /></div></p>
<p>As with complex images, your photographs are best to be saved under a JPEG, PNG-24 or SVG format. In the photo above, the color remains preserved in all formats aside from banding and noise that stand out in the shadows of the hair, skin, and background as well as at the top of photo as seen in the GIF and PNG-8 outputs.</p>
<p><em>Have a question about Photoshop? Why not ask it on our <a href="http://www.sitepoint.com/forums/forumdisplay.php?8-Graphics?utm_source=sitepoint&utm_medium=link&utm_campaign=forumlink" target="_blank">forums</a>?</em></p>
      <div>
        
        <div>Gabrielle is a creative type who specializes in graphic design, animation and photography.</div>
      </div>
            <div>
        
        <div>Jennifer Farley is a designer, illustrator and design instructor based in Ireland. She writes about design and illustration on her blog at Laughing Lion Design.</div>
      </div>
      
      
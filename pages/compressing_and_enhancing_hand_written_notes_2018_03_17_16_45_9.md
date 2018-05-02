<a href="https://mzucker.github.io/2016/09/20/noteshrink.html">https://mzucker.github.io/2016/09/20/noteshrink.html</a><div id="articleHeader"><h1>Compressing and enhancing hand-written notes</h1></div>
    <p><time>Sep 20, 2016</time></p>
  </header>

  
    <p>I wrote a program to clean up scans of handwritten notes while simultaneously reducing file size.</p>

<p>Example input and output:</p>

<p><div class="readableLargeImageContainer"><img src="/images/noteshrink/notesA1_comparison.png" alt="input/output comparison" /></div></p>

<p><em>Left:</em> input scan @ 300 DPI, 7.2MB PNG / 790KB JPG. <em>Right:</em>
output @ same resolution, 121KB PNG.<sup id="fnref:1"><a href="#fn:1" target="_blank">1</a></sup></p>

<p><em>Disclaimer:</em> the process described here is more or less what the
<a href="https://blogs.office.com/2015/04/02/office-lens-comes-to-iphone-and-android/" target="_blank">Office Lens</a> app does already, and there’s probably any number of
other tools that do similar things. I’m not claiming to have come up
with a radical new invention – just my own implementation of a useful
tool.</p>

<p>If you’re in a hurry, just check out the <a href="https://github.com/mzucker/noteshrink" target="_blank">github</a> repo, or jump down
to the <a href="#results" target="_blank">results</a> section, where you can play with
interactive 3D diagrams of color clusters.</p>

<h1 id="motivation">Motivation</h1>

<p>Some of my classes don’t have an assigned textbook. For these, I like
to appoint weekly “student scribes” to share their lecture notes with
the rest of the class, so that there’s some kind written resource for
students to double-check their understanding of the material. The
notes get posted to a course website as PDFs.</p>

<p>At school we have a “smart” copier capable of scanning to PDF, but the
documents it produces are… less than attractive.  Here’s some example
output from a handwritten homework page:</p>

<p><div class="readableLargeImageContainer"><img src="/images/noteshrink/copier_bad.png" alt="omg copier" /></div></p>

<p>Seemingly at random, the copier chooses whether to <a href="http://www.leptonica.com/binarization.html" target="_blank">binarize</a> each
mark (like the <em>x</em>’s), or turn them into abysmally blocky JPGs (like
the square root symbols). Needless to say, we can do better.</p>

<h1 id="overview">Overview</h1>

<p>We start out with a scan of a lovely page of student notes like this one:</p>

<p><a href="/images/noteshrink/notesA1.jpg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/images/noteshrink/notesA1.jpg" alt="a page of notes" /></div></a></p>

<p>The original PNG image scanned at 300 DPI is about 7.2MB; the same
image converted to a JPG at quality level 85 is about 790KB.<sup id="fnref:2"><a href="#fn:2" target="_blank">2</a></sup> Since
PDFs of scans are typically just a <a href="https://en.wikipedia.org/wiki/Digital_container_format" target="_blank">container format</a> around PNG
or JPG, we certainly don’t expect to <em>reduce</em> the required storage
size when converting to PDF. 800KB per page is pretty hefty – for the
sake of loading times, I’d love to see things closer to
100KB/page.<sup id="fnref:3"><a href="#fn:3" target="_blank">3</a></sup></p>

<p>Although this student is a very neat note-taker, the scan shown above
looks a bit messy (through no fault of her own). There’s lots of
bleed-through from the opposite side of the page, which is both
distracting for the viewer and hard for a JPG or PNG encoder to
compress, compared to a constant-color background.</p>

<p>This is what the output of my <code>noteshrink.py</code> program looks like:</p>

<p><a href="/images/noteshrink/notesA1_output.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/images/noteshrink/notesA1_output.png" alt="a page of notes" /></div></a></p>

<p>It’s a comparatively tiny PNG file, weighing in at just 121KB. My
favorite part? Not only did the image get <em>smaller</em>, it also got
<em>clearer</em>!</p>

<h1 id="process-and-color-image-fundamentals">Process and color image fundamentals</h1>

<p>Here are the steps required to produce the compact, clean image above:</p>

<ol>
  <li>
    <p>Identify the background color of the original scanned image.</p>
  </li>
  <li>
    <p>Isolate the foreground by thresholding on difference from background color.</p>
  </li>
  <li>
    <p>Convert to an indexed color PNG by choosing a small number of
“representative colors” from the foreground.</p>
  </li>
</ol>

<p>Before we delve into each one of these steps, it might be useful to
recap <em>how</em> color images are stored digitally. Because humans have
three different types of color-sensitive cells in their eyes, we can
reconstruct any color by combining various intensities of red, green,
and blue light.<sup id="fnref:4"><a href="#fn:4" target="_blank">4</a></sup> The resulting system equates colors with 3D
points in the <a href="https://en.wikipedia.org/wiki/RGB_color_space" target="_blank">RGB colorspace</a>, illustrated here:<sup id="fnref:5"><a href="#fn:5" target="_blank">5</a></sup></p>

<p><a href="https://commons.wikimedia.org/wiki/File:RGB_color_cube.svg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/images/noteshrink/RGB_color_cube.svg" alt="RGB color cube" /></div></a></p>

<p>Although a true vector space would allow an infinite number of
continuously varying pixel intensities, we need to discretize colors
in order to store them digitally – typically assigning 8 bits each to
the red, green, and blue channels.  Nevertheless, considering colors
in an image analogously to points in a continuous 3D space provides
powerful tools for analysis, as we shall see when we step through the
process outlined above.</p>

<h1 id="identifying-the-background-color">Identifying the background color</h1>

<p>Since the majority of the page is free from ink or lines, we might
expect the paper color to be the one that appears most frequently in
the scanned image – and if the scanner always represented every bit
of unmarked white paper as the same RGB triplet, we would have no
problems picking it out. Regrettably, this is not the case; random
variations in color appear due to dust specks and smudges on the
glass, color variations of the page itself, sensor noise, etc.  So in
reality, the “page color” can spread across thousands of distinct
RGB values.</p>

<p>The original scanned image is 2,081 x 2,531, with a total area of
5,267,011 pixels. Although we <em>could</em> consider each individual pixel,
it’s much faster to work on a representative sample of the input
image. The <code>noteshrink.py</code> program samples 5% of the input image by
default (more than sufficient for scans at 300 DPI), but for now,
let’s look at an even smaller subset of 10,000 pixels chosen at random
from the original scan:</p>

<p><div class="readableLargeImageContainer"><img src="/images/noteshrink/notesA1_samples_raw.png" alt="random pixels" /></div></p>

<p>Although it bears scant resemblance to the actual scanned page –
there’s no text to be found – the distribution of colors in the two
images is pretty much identical. Both are mostly grayish-white, with a
handful of red, blue, and dark gray pixels. Here are the same 10,000
pixels, sorted by brightness (e.g. the sum of their R, G, and B
intensities):</p>

<p><div class="readableLargeImageContainer"><img src="/images/noteshrink/notesA1_samples_sorted.png" alt="random pixels, sorted" /></div></p>

<p>Viewed from afar, the bottom 80-90% of the image all seems to be the
same color; however, closer inspection reveals quite a bit of variation.
In fact, the most frequent color in the image above, with RGB value
(240, 240, 242), accounts for just 226 of the 10,000 samples – less
than 3% of the total number of pixels.</p>

<p>Because the <a href="https://en.wikipedia.org/wiki/Mode_(statistics)" target="_blank">mode</a> here accounts for such a small percentage of the
sample, we should question how reliably it describes the distribution
of colors in the image. We’ll have a better chance of identifying a
prevalent page color if we first reduce the <a href="https://en.wikipedia.org/wiki/Color_depth" target="_blank">bit depth</a> of the image
before finding the mode. Here’s what things look like when we move
from 8 bits per channel to 4 by zeroing out the four
<a href="https://en.wikipedia.org/wiki/Least_significant_bit" target="_blank">least significant bits</a>:</p>

<p><div class="readableLargeImageContainer"><img src="/images/noteshrink/notesA1_samples_sorted_4bit.png" alt="random pixels, sorted, 4 bits per channel" /></div></p>

<p>Now the most frequently occurring color has RGB value (224, 224, 224),
and accounts for 3,623 (36%) of the sampled pixels. Essentially, by
reducing the bit depth, we are grouping similar pixels into larger
“bins”, which makes it easier to find a strong peak in the data.<sup id="fnref:6"><a href="#fn:6" target="_blank">6</a></sup></p>

<p>There’s a tradeoff here between reliability and precision: small bins
enable finer distinctions of color, but bigger bins are much more
robust. In the end, I went with 6 bits per channel to identify the
background color, which seemed like a good sweet spot between the two
extremes.</p>

<h1 id="isolating-the-foreground">Isolating the foreground</h1>

<p>Once we have identified the background color, we can <a href="https://en.wikipedia.org/wiki/Thresholding_(image_processing)" target="_blank">threshold</a> the
image according to how similar each pixel in the image is to it.  One
natural way to calculate the similarity of two colors is to compute
the <a href="https://en.wikipedia.org/wiki/Euclidean_distance" target="_blank">Euclidean distance</a> of their coordinates in RGB space; however,
this simple method fails to properly segment the colors shown below:</p>

<p><img src="/images/noteshrink/colors.svg" alt="difficult" /></p>

<p>Here’s a table specifying the colors and their Euclidean distances from the background color:</p>

<table>
  <thead>
    <tr>
      <th>Color</th>
      <th>Where found</th>
      <th>R</th>
      <th>G</th>
      <th>B</th>
      <th>Dist. from BG</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>white</strong></td>
      <td>background</td>
      <td>238</td>
      <td>238</td>
      <td>242</td>
      <td><strong>—</strong></td>
    </tr>
    <tr>
      <td><strong>gray</strong></td>
      <td>bleed-through from back</td>
      <td>160</td>
      <td>168</td>
      <td>166</td>
      <td><strong>129.4</strong></td>
    </tr>
    <tr>
      <td><strong>black</strong></td>
      <td>ink on front of page</td>
      <td>71</td>
      <td>73</td>
      <td>71</td>
      <td><strong>290.4</strong></td>
    </tr>
    <tr>
      <td><strong>red</strong></td>
      <td>ink on front of page</td>
      <td>219</td>
      <td>83</td>
      <td>86</td>
      <td><strong>220.7</strong></td>
    </tr>
    <tr>
      <td><strong>pink</strong></td>
      <td>vertical line at left margin</td>
      <td>243</td>
      <td>179</td>
      <td>182</td>
      <td><strong>84.3</strong></td>
    </tr>
  </tbody>
</table>

<p>As you can see, the dark gray bleed-through that we would like to
classify as background is actually <em>further</em> away from the white page
color than the pink line color which we hope to classify as
foreground. Any threshold on Euclidean distance that marks pink as
foreground would necessarily also have to include the bleed-through.</p>

<p>We can get around this issue by moving from RGB space to
<a href="https://en.wikipedia.org/wiki/HSL_and_HSV" target="_blank">Hue-Saturation-Value</a> (HSV) space, which deforms the RGB cube
into the cylindrical shape illustrated in this cutaway view:<sup id="fnref:7"><a href="#fn:7" target="_blank">7</a></sup></p>

<p><a href="https://commons.wikimedia.org/wiki/File:HSV_color_solid_cylinder.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/images/noteshrink/hsv.png" alt="diagram of HSV space" /></div></a></p>

<p>The HSV cylinder features a rainbow of colors distributed circularly
about its outside top edge; <em>hue</em> refers to the angle along this
circle. The central axis of the cylinder ranges from black at the
bottom to white at the top, with gray shades in between – this entire
axis has zero <em>saturation</em>, or intensity of color, and the vivid hues
on the outside circumference all have a saturation of 1.0. Finally,
<em>value</em> refers to the overall brightness of the color, ranging from
black at the bottom to bright shades at the top.</p>

<p>So now let’s reconsider our colors above, this time in terms of value
and saturation:</p>

<table>
  <thead>
    <tr>
      <th>Color</th>
      <th>Value</th>
      <th>Saturation</th>
      <th>Value diff. from BG</th>
      <th>Sat. diff from BG</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>white</strong></td>
      <td>0.949</td>
      <td>0.017</td>
      <td><strong>—</strong></td>
      <td><strong>—</strong></td>
    </tr>
    <tr>
      <td><strong>gray</strong></td>
      <td>0.659</td>
      <td>0.048</td>
      <td><strong>0.290</strong></td>
      <td><strong>0.031</strong></td>
    </tr>
    <tr>
      <td><strong>black</strong></td>
      <td>0.286</td>
      <td>0.027</td>
      <td><strong>0.663</strong></td>
      <td><strong>0.011</strong></td>
    </tr>
    <tr>
      <td><strong>red</strong></td>
      <td>0.859</td>
      <td>0.621</td>
      <td><strong>0.090</strong></td>
      <td><strong>0.604</strong></td>
    </tr>
    <tr>
      <td><strong>pink</strong></td>
      <td>0.953</td>
      <td>0.263</td>
      <td><strong>0.004</strong></td>
      <td><strong>0.247</strong></td>
    </tr>
  </tbody>
</table>

<p>As you might expect, white, black, and gray vary significantly in
value, but share similarly low saturation levels – well below 
either red or pink. With the additional information provided by HSV,
we can successfully mark a pixel as belonging to the foreground if
either one of these criteria holds:</p>

<ul>
  <li>the value differs by more than 0.3 from the background color, <em>or</em></li>
  <li>the saturation differs by more than 0.2 from the background color</li>
</ul>

<p>The former criterion pulls in the black pen marks, whereas the latter
pulls in the red ink as well as the pink line. Both criteria
successfully exclude the gray bleed-through from the foreground.
Different images may require different saturation/value thresholds;
see the <a href="#results" target="_blank">results</a> section for details.</p>

<h1 id="colors">Choosing a set of representative colors</h1>

<p>Once we isolate the foreground, we are left with a new set of colors
corresponding to the marks on the page. Let’s visualize the set – but
this time, instead of considering colors as a collection of pixels, we
will consider them as 3D points in the RGB colorspace. The resulting
scatterplot ends up looking quite “clumpy”, with several bands of
related colors:</p>

<p>Interactive 3D plot powered by <a href="http://threejs.org/" target="_blank">three.js</a>. Click and drag to rotate; <a href="#" id="notesA1pointsonly_animate" target="_blank"><code>a</code></a> toggles spinning animation, <a href="#" id="notesA1pointsonly_rotate" target="_blank"><code>r</code></a> resets rotation. </p>

<p>Our goal now is to convert the original 24 bit-per-pixel image into an
<a href="https://en.wikipedia.org/wiki/Indexed_color" target="_blank">indexed color</a> image by choosing a small number (8, in this example)
of colors to represent the whole image. This has two effects: first,
it reduces the file size because specifying a color now requires only
3 bits (since <nobr>8=23</nobr><math><mn>8</mn><mo>=</mo><msup><mn>2</mn><mn>3</mn></msup></math>). Furthermore, it makes the resulting image
more visually cohesive because similarly colored ink marks are likely
to be assigned the same color in the final output image.</p>

<p>To accomplish this goal we will use a data-driven method that
exploits the “clumpy” nature of the diagram above. Choosing colors
that correspond to the centers of clusters will
lead to a set of colors that accurately represents the underlying
data.  In technical terms, we’ll be solving a <a href="https://en.wikipedia.org/wiki/Color_quantization" target="_blank">color quantization</a>
problem (which is itself just a special case of
<a href="https://en.wikipedia.org/wiki/Vector_quantization" target="_blank">vector quantization</a>), through the use of <a href="https://en.wikipedia.org/wiki/Cluster_analysis" target="_blank">cluster analysis</a>.</p>

<p>The particular methodological tool for the job that I picked is
<a href="https://en.wikipedia.org/wiki/K-means_clustering" target="_blank"><em>k</em>-means clustering</a>. Its overall goal is to find a set of
means or centers which minimizes the average distance from each point
to the nearest center. Here’s what you get when you use it to pick out
seven different clusters on the dataset above:<sup id="fnref:8"><a href="#fn:8" target="_blank">8</a></sup></p>

<p>Interactive 3D plot powered by <a href="http://threejs.org/" target="_blank">three.js</a>. Click and drag to rotate; <a href="#" id="notesA1_animate" target="_blank"><code>a</code></a> toggles spinning animation, <a href="#" id="notesA1_rotate" target="_blank"><code>r</code></a> resets rotation. Use <a href="#" id="notesA1_points" target="_blank"><code>p</code></a>, <a href="#" id="notesA1_circles" target="_blank"><code>c</code></a>, and <a href="#" id="notesA1_lines" target="_blank"><code>l</code></a>to toggle visibility of points, circles, and lines.</p>

<p>In this diagram, the points with black outlines represent foreground
color samples, and the colored lines connect them to their closest
center in the RGB colorspace. When the image is converted to indexed
color, each foreground sample will get replaced with the color of the
closest center.  Finally, the circular outlines indicate the distance
from each center its furthest associated sample.</p>

<h1 id="whistles-and-bells">Whistles and bells</h1>

<p>Aside from being able to set the value and saturation thresholds, the
<code>noteshrink.py</code> program has several other notable features. By
default, it increases the vividness and contrast of the final palette
by rescaling the minimum and maximum intensity values to 0 and 255,
respectively. Without this adjustment, the 8-color palette for the
scan above would look like this:</p>

<p><img src="/images/noteshrink/notesA1_palette.png" alt="original palette" /></p>

<p>The adjusted palette is more vibrant:</p>

<p><img src="/images/noteshrink/notesA1_modified_palette.png" alt="adjusted palette" /></p>

<p>There is also an option to force the background color to white after
isolating the foreground colors.  To further reduce the PNG image
sizes after conversion to indexed color, <code>noteshrink.py</code> can
automatically run <a href="http://optipng.sourceforge.net/pngtech/optipng.html" target="_blank">PNG optimization</a> tools such as <a href="http://optipng.sourceforge.net/" target="_blank">optipng</a>,
<a href="http://pmt.sourceforge.net/pngcrush/" target="_blank">pngcrush</a>, or <a href="https://pngquant.org/" target="_blank">pngquant</a>.</p>

<p>The program’s final output combines several output images together
into PDFs like <a href="/images/noteshrink/notesA.pdf" target="_blank">this one</a> using ImageMagick’s <a href="http://www.imagemagick.org/script/convert.php" target="_blank">convert</a> tool.  As a
further bonus, <code>noteshrink.py</code> automatically sorts input filenames
numerically (as opposed to alphabetically, as the shell <a href="https://en.wikipedia.org/wiki/Glob_(programming)" target="_blank">globbing</a>
operator does).  This is helpful when your dumb scanning program<sup id="fnref:9"><a href="#fn:9" target="_blank">9</a></sup>
produces output filenames like <code>scan 9.png</code> and <code>scan 10.png</code>, and you
don’t want their order to be swapped in the PDF.</p>

<h1 id="results">Results</h1>

<p>Here are some more examples of the program output. The first one
(<a href="/images/noteshrink/tree.pdf" target="_blank">PDF</a>) looks great with the default
threshold settings:</p>

<p><div class="readableLargeImageContainer"><img src="/images/noteshrink/tree_comparison.png" alt="tree comparison" /></div></p>

<p>Here is the visualization of the color clusters:</p>

<p>Interactive 3D plot powered by <a href="http://threejs.org/" target="_blank">three.js</a>. Click and drag to rotate; <a href="#" id="tree_animate" target="_blank"><code>a</code></a> toggles spinning animation, <a href="#" id="tree_rotate" target="_blank"><code>r</code></a> resets rotation. Use <a href="#" id="tree_points" target="_blank"><code>p</code></a>, <a href="#" id="tree_circles" target="_blank"><code>c</code></a>, and <a href="#" id="tree_lines" target="_blank"><code>l</code></a>to toggle visibility of points, circles, and lines.</p>

<p>The next one (<a href="/images/noteshrink/notesB.pdf" target="_blank">PDF</a>) required lowering
the saturation threshold to 0.045 because the blue-gray lines are so
drab:</p>

<p><div class="readableLargeImageContainer"><img src="/images/noteshrink/notesB1_comparison.png" alt="notesB comparison" /></div></p>

<p>Color clusters:</p>

<p>Interactive 3D plot powered by <a href="http://threejs.org/" target="_blank">three.js</a>. Click and drag to rotate; <a href="#" id="notesB1_animate" target="_blank"><code>a</code></a> toggles spinning animation, <a href="#" id="notesB1_rotate" target="_blank"><code>r</code></a> resets rotation. Use <a href="#" id="notesB1_points" target="_blank"><code>p</code></a>, <a href="#" id="notesB1_circles" target="_blank"><code>c</code></a>, and <a href="#" id="notesB1_lines" target="_blank"><code>l</code></a>to toggle visibility of points, circles, and lines.</p>

<p>Finally, an example scanned in from engineer’s graph paper
(<a href="/images/noteshrink/graph-paper-ink-only.pdf" target="_blank">PDF</a>). For this one, I
set the value threshold to 0.05 because the contrast between the
background and the lines was so low:</p>

<p><div class="readableLargeImageContainer"><img src="/images/noteshrink/engr_comparison.png" alt="graph paper comparison" /></div></p>

<p>Color clusters:</p>

<p>Interactive 3D plot powered by <a href="http://threejs.org/" target="_blank">three.js</a>. Click and drag to rotate; <a href="#" id="engr_animate" target="_blank"><code>a</code></a> toggles spinning animation, <a href="#" id="engr_rotate" target="_blank"><code>r</code></a> resets rotation. Use <a href="#" id="engr_points" target="_blank"><code>p</code></a>, <a href="#" id="engr_circles" target="_blank"><code>c</code></a>, and <a href="#" id="engr_lines" target="_blank"><code>l</code></a>to toggle visibility of points, circles, and lines.</p>

<p>All together, the four PDFs take up about 788KB, averaging about about
 130KB per page of output.</p>

<h1 id="conclusions-and-future-work">Conclusions and future work</h1>

<p>I’m glad I was able to produce a practical tool that I can use to
prepare scribe note PDFs for my course websites. Beyond that, I really
enjoyed preparing this writeup, especially because it prodded me to
try to improve on the essentially 2D visualizations displayed on the
Wikipedia <a href="https://en.wikipedia.org/wiki/Color_quantization" target="_blank">color quantization</a> page, and also to finally learn
<a href="http://threejs.org/" target="_blank">three.js</a> (very fun, would use again).</p>

<p>If I ever revisit this project, I’d like to play around with
alternative quantization schemes. One that occurred to me this week
was to use <a href="https://en.wikipedia.org/wiki/Spectral_clustering" target="_blank">spectral clustering</a> on the <a href="https://en.wikipedia.org/wiki/Nearest_neighbor_graph" target="_blank">nearest neighbor graph</a> of 
a set of color samples – I thought this was an exciting new idea when I
dreamed it up, but it turns out there’s a <a href="http://www.sciencedirect.com/science/article/pii/S003132031200074X" target="_blank">2012 paper</a> that proposes this
exact approach. Oh well.</p>

<p>You could also try using <a href="https://en.wikipedia.org/wiki/Expectation%E2%80%93maximization_algorithm" target="_blank">expectation maximization</a> to form a
<a href="https://en.wikipedia.org/wiki/Mixture_model#Gaussian_mixture_model" target="_blank">Gaussian mixture model</a> describing the color distribution – not sure
if that’s been done much in the past. Other fun ideas include trying
out a “perceptually uniform” colorspace like <a href="https://en.wikipedia.org/wiki/Lab_color_space" target="_blank">L*a*b*</a> to cluster in, and
also to attempt to automatically determine the
<a href="https://en.wikipedia.org/wiki/Determining_the_number_of_clusters_in_a_data_set" target="_blank">“best” number of clusters</a> for a given image.</p>

<p>On the other hand, I’ve got a backlog of blog entries to shove out the
door, so I’m going to put a pin in this project for now, and invite you to go
checkout the <code>noteshrink.py</code> <a href="https://github.com/mzucker/noteshrink" target="_blank">github</a> repository. Until next time!</p>











<h1>Comments</h1>
<div>
<p>Comments are closed, see <a href="/2017/05/08/no-more-disqus.html" target="_blank">here</a> for details.</p>
</div>
<div>
<div>
Giancarlo Ventura Granados · 2016-Sep-26
</div>
<div>
<p>Great post and great application</p>
</div>
</div>
<div>
<div>
Leonel Salazar · 2016-Sep-28
</div>
<div>
<p>Hi there, I can't run the program, it gives me this output and I can't solve the problem by myself, I'm running Debian Jessie... I'm testing using one of the images from this webpage.<br />Traceback:<br />$ noteshrink /home/lordford/Downloads/notesA1.jpg <br />opened /home/lordford/Downloads/notesA1.jpg<br />  getting palette...<br />Traceback (most recent call last):<br />  File "/usr/local/bin/noteshrink", line 9, in &lt;module&gt;<br />    load_entry_point('noteshrink==0.1.0', 'console_scripts', 'noteshrink')()<br />  File "build/bdist.linux-x86_64/egg/<a href="http://noteshrink.py" target="_blank">noteshrink.py</a>", line 582, in main<br />  File "build/bdist.linux-x86_64/egg/<a href="http://noteshrink.py" target="_blank">noteshrink.py</a>", line 558, in notescan_main<br />  File "build/bdist.linux-x86_64/egg/<a href="http://noteshrink.py" target="_blank">noteshrink.py</a>", line 381, in get_palette<br />  File "build/bdist.linux-x86_64/egg/<a href="http://noteshrink.py" target="_blank">noteshrink.py</a>", line 106, in get_bg_color<br />TypeError: unique() got an unexpected keyword argument 'return_counts'</p>
</div>
<div>
<div>
<div>
Matt Zucker · 2016-Sep-29
</div>
<div>
<p>Yep, I was unaware return_counts was a recently added option in numpy.unique. You will need numpy 1.10 or greater to run the script. I have updated the requirements.txt in the repo, but I haven't yet incremented my version number and re-uploaded to PyPI, working on it...</p>
</div>
</div>
</div>
</div>
<div>
<div>
Cidraque · 2016-Oct-23
</div>
<div>
<p>Only linux? :(</p>
</div>
<div>
<div>
<div>
Matt Zucker · 2016-Oct-23
</div>
<div>
<p>It should work on any system where you can install Python and the requirements, including windows.</p>
</div>
</div>
</div>
</div>
<div>
<div>
Mekk · 2016-Oct-23
</div>
<div>
<p>Congratulations for interesting software and for very clear writing, showing non-trivial algorithm in very understandable way.  Thank you.</p>
</div>
<div>
<div>
<div>
Matt Zucker · 2016-Oct-23
</div>
<div>
<p>Thanks!</p>
</div>
</div>
</div>
</div>
<div>
<div>
Sergio · 2016-Oct-24
</div>
<div>
<p>Hi! Thanks for providing this tool. I was trying to make it work with Python 2.7 but, after installing the required packages successfully I get the following error:<br />    "running PDF command "convert page0000.png output.pdf"..."<br />    "warning: PDF command failed"<br />And only PNG is generated. <br />Do you know what should be failing?<br />Thanks in advance!</p>
</div>
<div>
<div>
<div>
Matt Zucker · 2016-Oct-24
</div>
<div>
<p>Yes, it looks like the ImageMagick software is not installed. Please see <a href="http://www.imagemagick.org/script/binary-releases.php" target="_blank">http://www.imagemagick.org/scr...</a> or use your usual package manager (apt-get/macports/homebrew/etc.) to install it.</p>
</div>
</div>
</div>
</div>
<div>
<div>
Kelvin Titimbo · 2016-Nov-12
</div>
<div>
<p>Hi, thank you for this tool. I would like to know whether is possible to<br /> convert pdf files.</p><p>I have been trying to convert my pdf's as png, but the quality is not the best, so the final output does not have the best resolution.</p>
</div>
</div>
<div>
<div>
Matthias Laumer · 2016-Nov-15
</div>
<div>
<p>Dear Matt, a user from a german forum asked me / the community if someone would create a GUI for your noteshrinker... (additionally to the django based which is alread existing). Therefor I would get in touch with you via email, if it is possible and wanted by you... (of course it will be open source and hosted on github...) hopefully you can see my mail-adress due to this comment... Regards Matthias</p>
</div>
<div>
<div>
<div>
Matt Zucker · 2016-Nov-16
</div>
<div>
<p>Hi Matthias - the software is open sourced with a very permissive license. There's nothing stopping anyone from picking it up and doing pretty much whatever they'd like with it. I don't have time to support development of a GUI but I encourage you and your fellow forum members to go for it!</p>
</div>
<div>
<div>
<div>
Matthias Laumer · 2016-Nov-16
</div>
<div>
<p>Hey Matt, thanks for your fast reply! Of course we will take care of development of the GUI ;-) no support from your side should be needed... your programm is in a good shape and structure. I just wanted to be sure and have asked for your permission (beside the MIT license) :-D Maybe in a few weeks / months(?) depending on my time which I can spend I'll get in touch with you again, just to let you know the github repo of the finished GUI! Thanks so far and best regards from Germany, <br />Matthias</p>
</div>
<div>
<div>
<div>
Matthias Laumer · 2016-Dec-15
</div>
<div>
<p>Hi Matt, here you can find the first alpha if you want to have a look at it -&gt; <a href="https://github.com/Acer54/noteshrinker-qt" target="_blank">https://github.com/Acer54/note...</a> ... for Win User, there is a zip file with all dependencies ... for Linux and Mac only source code is available. Take a look at the release notes as well... I have made a few changes, e.g. replacing PIL and Imagemagick with qt4 libs. Regards, Matthias</p>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div>
<div>
Xemmas Enesimo Cuarto · 2016-Dec-04
</div>
<div>
<p>Hey, have you tried using graphics magick instead of image magick?</p>
</div>
<div>
<div>
<div>
Matt Zucker · 2016-Dec-05
</div>
<div>
<p>No, I imagine it would probably work as long as the command line arguments to 'convert' haven't been changed too much...</p>
</div>
</div>
</div>
</div>

<div>
  <ol>
    <li id="fn:1">
      <p>Handwritten note samples are presented with the generous permission of my students Ursula Monaghan and John Larkin. <a href="#fnref:1" target="_blank">↩</a></p>
    </li>
    <li id="fn:2">
      <p>The image shown here is actually downsampled to 150 DPI to allow the page to load faster. <a href="#fnref:2" target="_blank">↩</a></p>
    </li>
    <li id="fn:3">
      <p>One thing our copier <em>does</em> do well is keep PDF sizes down – it gets about 50-75 KB/page for these types of documents. <a href="#fnref:3" target="_blank">↩</a></p>
    </li>
    <li id="fn:4">
      <p>This makes red, green, and blue the <em>additive primary colors</em>. Your elementary school art teacher may have told you that the primary colors are red, yellow and blue. This is a <a href="https://en.wikipedia.org/wiki/Lie-to-children" target="_blank">lie</a>; however, there are three <em>subtractive primary colors</em>: cyan, yellow, and magenta. The additive primaries relate to combining <em>light</em> (which is what monitors emit), whereas the subtractive colors relate to combining <em>pigment</em> found in inks and dyes. <a href="#fnref:4" target="_blank">↩</a></p>
    </li>
    <li id="fn:5">
      <p>Image courtesy Wikimedia Commons user Maklaan. License: CC BY-SA 3.0 <a href="#fnref:5" target="_blank">↩</a></p>
    </li>
    <li id="fn:6">
      <p>Check out the “tips” example in Wikipedia’s <a href="https://en.wikipedia.org/wiki/Histogram#Examples" target="_blank">histogram article</a> for another illustration of why increasing the bin size helps. <a href="#fnref:6" target="_blank">↩</a></p>
    </li>
    <li id="fn:7">
      <p>Image courtesy Wikimedia Commons user SharkD. License: CC BY-SA 3.0 <a href="#fnref:7" target="_blank">↩</a></p>
    </li>
    <li id="fn:8">
      <p>Why <em>k</em>=7 and not 8? We want 8 colors in the final image, and we already have identified a background color… <a href="#fnref:8" target="_blank">↩</a></p>
    </li>
    <li id="fn:9">
      <p>Yes, I’m glaring at you, Mac OS <a href="https://support.apple.com/en-us/HT204790" target="_blank">Image Capture</a>… <a href="#fnref:9" target="_blank">↩</a></p>
    </li>
  </ol>
</div>

  
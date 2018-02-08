<a href="https://www.smashingmagazine.com/2017/12/understanding-css-layout-block-formatting-context/">https://www.smashingmagazine.com/2017/12/understanding-css-layout-block-formatting-context/</a><div id="articleHeader"><h1>Understanding CSS Layout And The Block Formatting Context — Smashing Magazine</h1></div>
		
			
			
			
				


<div>
  <img src="https://d33wubrfki0l68.cloudfront.net/a2b586e0ae8a08879457882013f0015fa9c31f7c/9e355/images/drop-caps/t.svg" />
  <img src="https://d33wubrfki0l68.cloudfront.net/b5449482a65c611116580c9dfbf75c686b132629/e2b2f/images/drop-caps/character-7.svg" />
</div>

        		

<p>There are a few concepts in CSS layout that can really enhance your CSS game once you understand them. This article is about the Block Formatting Context (BFC). You may never have heard of this term, but if you have ever made a layout with CSS, you probably know what it is. Understanding what a BFC is, why it works, and how to create one is useful and can help you to understand how layout works in CSS.</p>

<p>In this article, I’ll explain what a BFC is through examples which are likely to be familiar to you. I’ll then show you a new value of display, that really only makes sense once you understand what a BFC is and why you might need one.</p><h3 id="what-is-a-bfc">What Is A BFC? </h3>

<p>How a Block Formatting Context (BFC) behaves is easiest to understand with a simple float example. In the below example I have a box that contains an image that has been floated left and some text. If we have a good amount of text it wraps around the floated image and the border then runs around the whole lot.</p><pre><code>&lt;div class="outer"&gt;
      &lt;div class="float"&gt;I am a floated element.&lt;/div&gt;
      I am text inside the outer box.
    &lt;/div&gt;
</code><div><div><a target="_blank">Copy</a></div></div></pre>

<pre><code>.outer {
      border: 5px dotted rgb(214,129,137);
      border-radius: 5px;
      width: 450px;
      padding: 10px;
      margin-bottom: 40px;
    }

    .float {
      padding: 10px;
      border: 5px solid rgba(214,129,137,.4);
      border-radius: 5px;
      background-color: rgba(233,78,119,.4);
      color: #fff;
      float: left;  
      width: 200px;
      margin: 0 20px 0 0;
    }
</code><div><div><a target="_blank">Copy</a></div></div></pre>

<figure><a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a526965-c119-4479-b8ba-80f48b1d491a/floats1-large-opt.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf72a345-d837-4524-a9a7-47a75b281589/floats1-800w-opt.png" "  alt="Screenshot of a box with a border, inside is an item floated with text wrapping around" /></div></a><figcaption>Text wraps around a floated element. (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a526965-c119-4479-b8ba-80f48b1d491a/floats1-large-opt.png" target="_blank">Large preview</a>)</figcaption></figure>

<p>If I remove some of the text, then there is not enough to wrap around the image, and because the float is taken out of document flow, the border rises up and runs underneath the image to the height of the text.</p>

<figure><a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91b96e1e-59e9-484d-8bb5-3405af8c8a74/floats2-large-opt.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f40fbaa1-771c-4655-82bb-d16ec1e4f447/floats2-800w-opt.png" "  alt="Screenshot of a box with a border, the text not long enough to cause the border to clear the float" /></div></a><figcaption>Without enough text the border does not respect the height needed for the floated element. (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91b96e1e-59e9-484d-8bb5-3405af8c8a74/floats2-large-opt.png" target="_blank">Large preview</a>)</figcaption></figure>

<p>This happens because when we float an element, the box that the text is in remains the same width, what is shortened to make space for the floated element are the line boxes of the text. This is why backgrounds and borders will appear to run behind our float.</p>



  <aside>
    <div>
      <div>
    <p><em>“You must unlearn what you have learned!”</em> Meet the <strong>brand new episode</strong> of <a href="https://www.smashingmagazine.com/events/san-francisco-2018/" target="_blank">SmashingConf San Francisco</a> with smart front-end tricks and UX techniques. Featuring Yiying Lu, Aarron Draplin, Smashing Yoda, and many others. Tickets now on sale. April 17-18.</p>
      <a href="/events/san-francisco-2018/#speakers" target="_blank">
        Check the speakers →
      </a>
      </div>
      <div>
        <a href="/membership/" target="_blank" class="readableLinkWithLargeImage">
        <div>
          <div class="readableLargeImageContainer float"><img src="https://d33wubrfki0l68.cloudfront.net/4afa3480a88ab5052f5fc65875503c35f7c375f3/049a9/images/smashing-cat/cat-smashingconf-sf.png"   alt="SmashingConf San Francisco, with Yiying Lu, Josh Clark and many others." /></div>
        </div>
      </a>
      </div>
    </div>
  </aside>





<div>


<p>There are two ways in which we ordinarily fix this layout problem. One would be to use a <a href="https://css-tricks.com/snippets/css/clear-fix/" target="_blank">clearfix hack</a>, which has the effect of inserting an element below the text and image and setting it to clear both. The other method is to use the overflow property, with a value other than the default of visible.</p>

<pre><code>.outer {
      overflow: auto;
    }
</code><div><div><a target="_blank">Copy</a></div></div></pre>

<figure><a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4394a5a-a432-4a15-ba46-724240583f89/floats3-large-opt.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6f19f98-20ca-43ac-adc0-facb474ed81f/floats3-800w-opt.png" "  alt="Screenshot of a box with a border where the border clears the floated item" /></div></a><figcaption>Using <code>overflow: auto</code> causes the box to contain the float. (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4394a5a-a432-4a15-ba46-724240583f89/floats3-large-opt.png" target="_blank">Large preview</a>)</figcaption></figure>




<p>The reason overflow works in this way is that using any value other than the initial value of <code>visible</code> creates a Block Formatting Context, and one of the features of a BFC is that <strong>it contains floats</strong>.</p>

<h3 id="a-bfc-is-a-mini-layout-in-your-layout">A BFC Is A Mini Layout In Your Layout </h3>

<p>You can think of a BFC as like a mini layout inside your page. Once an element creates a BFC, everything is contained inside it. As we have seen, this includes floated elements which no longer poke out of the bottom of the box. The BFC also causes some other useful behavior.</p>

<p><strong>The BFC prevents margins collapsing</strong></p>


  



<p>Understanding margin collapsing is another underrated CSS skill. In this next example, I have a div with a background color of grey.</p>

<p>This div has two paragraphs inside it. The outer div element has a margin-bottom of 40 pixels; the paragraphs also have a top and bottom margin of 20 pixels.</p>

<pre><code>.outer {
       background-color: #ccc;
      margin: 0 0 40px 0;
    }

    p {
      padding: 0;
      margin: 20px 0 20px 0;
      background-color: rgb(233,78,119);
      color: #fff;
    }
</code><div><div><a target="_blank">Copy</a></div></div></pre>

<p>As there is nothing between the margin of the <code>p</code> element and the margin on the outer div, the two will collapse and so the paragraphs end up flush with the top and bottom of the box. We don’t see any grey above and below the paragraphs.</p>

<figure><a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8185b27-9f9e-4e47-9501-d1f3bb4fde15/margins1-large-opt.png" target="_blank" class="readableLinkWithMediumImage"><img src="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d596e968-5d2e-4b84-8d8b-90b1a793a13d/margins1-800w-opt.png" width="“800"" height="81" alt="A box with a grey background, the two paragraphs inside flush with the top and bottom" /></a><figcaption>The margins collapse so we see no grey top and bottom of the box. (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8185b27-9f9e-4e47-9501-d1f3bb4fde15/margins1-large-opt.png" target="_blank">Large preview</a>)</figcaption></figure>

<p>If we make the box a BFC however, it now contains the paragraphs and their margins, so they don’t collapse and we can see the grey background of the container behind the margin.</p>

<pre><code>.outer {
       background-color: #ccc;
      margin: 0 0 40px 0;
      overflow: auto;
    }
</code><div><div><a target="_blank">Copy</a></div></div></pre>

<figure><a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/517fc92c-810b-47a0-8ab8-bcf4c03956ea/margins2-large-opt.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/054a7da3-fb51-40b4-a0d6-366839a34327/margins2-800w-opt.png" "  alt="A box with a grey background the paragraphs have a margin top and bottom" /></div></a><figcaption>With the container, BFC margins do not collapse. (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/517fc92c-810b-47a0-8ab8-bcf4c03956ea/margins2-large-opt.png" target="_blank">Large preview</a>)</figcaption></figure>




<p>Once again the BFC is doing this job of containing the things inside it, stopping them from escaping and poking out of the box.</p>

<p><strong>A BFC stops content wrapping floats.</strong>
You will also be familiar with this behavior of a BFC, as it is how any column type layout using floats works. If an item creates a BFC, then that item will not wrap any floats. In the following example I have markup like this:</p>

<pre><code>&lt;div class="outer"&gt;
      &lt;div class="float"&gt;I am a floated element.&lt;/div&gt;
      &lt;div class="text"&gt;I am text&lt;/div&gt;
    &lt;/div&gt;
</code><div><div><a target="_blank">Copy</a></div></div></pre>

<p>The item with a class of float is floated left and so the text in the div which comes after it wraps around the float.</p>

<figure><a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66b38f4d-41b9-446d-ab19-35ae7a12b4de/wrap1-large-opt.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0446b45e-6cde-435b-b3be-8878452257f9/wrap1-800w-opt.png" "  alt="Screenshot of a box with a border, inside is an item floated with text wrapping around" /></div></a><figcaption>Text wraps around the floated element. (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66b38f4d-41b9-446d-ab19-35ae7a12b4de/wrap1-large-opt.png" target="_blank">Large preview</a>)</figcaption></figure>

<p>I can prevent that wrapping behavior by making the div that wraps the text a BFC.</p>

<pre><code>.text {
      overflow: auto;
    }
</code><div><div><a target="_blank">Copy</a></div></div></pre>

<figure><a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/739da4c9-b0bc-453a-9ea9-66c4261aa9f9/wrap2-large-opt.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/015d66df-523d-4440-ad39-58dcf925f9b6/wrap2-800w-opt.png" "  alt="Screenshot of a box with a border, the text is not wrapping around the floated item" /></div></a><figcaption>The div containing the text is now a BFC so the text does not wrap. (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/739da4c9-b0bc-453a-9ea9-66c4261aa9f9/wrap2-large-opt.png" target="_blank">Large preview</a>)</figcaption></figure>

<p>This is essentially the way we can create a floated layout with several columns. Floating an item also creates a BFC for that item, and so our columns don’t attempt to wrap around each other if one on the right is taller than one on the left.</p>







  <aside>
    <div>
      <div>
        <p>
          Is your pattern library up to date today? <em>Alla Kholmatova</em> has just finished a fully fledged book on <strong>Design Systems</strong> and how to get them right. With common traps, gotchas and the lessons she learned. Hardcover, eBook. <em>Just sayin'.</em>
        </p>
        
      </div>
      <div>
        <a href="/printed-books/design-systems/" target="_blank" class="readableLinkWithLargeImage">
        <div>
          <div class="readableLargeImageContainer float"><img src="https://d33wubrfki0l68.cloudfront.net/91ed41706514200a7ef212ebfeead7471354e622/01dcc/images/books/design-systems--large-opt.png" /></div>
        </div>
      </a>
      </div>
    </div>
  </aside>




<h3 id="what-else-creates-a-bfc">What Else Creates A BFC? </h3>

<p>In addition to using <code>overflow</code> to create a BFC, some other CSS properties create a BFC. As we have seen, floating an element creates a BFC. So your floated item will contain anything inside it.</p>

<p>Using <code>position: absolute</code> or <code>position: fixed</code> on an element.</p>

<p>Using <code>display: inline-block</code>, <code>display: table-cell</code> or <code>display: table-caption</code>. The <code>table-cell</code> and <code>table-captions</code> are the default for these HTML elements, so if you have a data table for example, each cell will create a BFC.</p>

<p>Using <code>column-span: all</code>, which is used to span the columns of a multi-column layout. Flex and Grid items also create something like a BFC, except they are described as a <strong>Flex Formatting Context</strong> and <strong>Grid Formatting Context</strong> respectively. This reflects the type of layout each is participating in. A Block Formatting Context indicates that the item is participating in Block Layout, a Flex Formatting Context means the item is participating in Flex layout. In practice, the result is the same, floats are contained and margins do not collapse.</p>

<h3 id="the-new-way-to-create-a-bfc">The New Way To Create A BFC </h3>

<p>There are two issues with using overflow, or some other method to create a BFC. The first is that these methods have side effects based on what they were really designed to do. The overflow method creates a BFC and contains floats, however in certain scenarios you might find that you get an unwanted scrollbar, or that shadows are clipped. This is due to the fact that the overflow property is designed to allow you to tell the browser what to do in an overflow situation - cause a scrollbar or clip the content. The browser is doing exactly what you told it to do!</p>

<p>Even in situations where you don’t get any unwanted side effects, using overflow is potentially confusing to another developer. Why is overflow set to auto or scroll? What was the original developer’s intention there? Did they want scrollbars on this component?</p>

<p>What would be useful would be a method of creating a BFC that is otherwise inert, causing no other behavior but to create that mini layout, and the ability for things to happen inside it safely. That method would not cause any unexpected issues and also allow clarity in terms of what the developer intended. The CSS Working Group thought that might be pretty handy too, and so we have a new value of the <code>display</code> property - <code>flow-root</code>.</p>

<p>You would use <code>display: flow-root</code> in any of the situations in this article where creating a new BFC would be advantageous - to contain floats, to prevent margins collapsing, or to prevent an item wrapping a float.</p>

<p>You can see all of these in the CodePen below if you have a browser that supports <code>display: flow-root</code> such as up to date Firefox or Chrome.</p>




<p><strong>Browser support for display: flow-root</strong></p>

<figure><a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c127c381-0ebe-4d6d-a77c-45a7d0967b37/caniuse-large-opt.png
" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02590ea1-08e2-439e-8e06-7d5ff4174615/caniuse-800w-opt.png" "  /></div></a><figcaption><a href="https://caniuse.com/#feat=flow-root" target="_blank">Can I Use display: flow-root</a>. (<a href="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c127c381-0ebe-4d6d-a77c-45a7d0967b37/caniuse-large-opt.png" target="_blank">Large preview</a>)</figcaption></figure>

<p>Browser support for this value is limited, but increasing and if you think it would be handy, do go and vote for it in Edge. However, even if you aren’t able to use the handy flow-root feature in your code right now, you now understand what a BFC is, and what you are doing when you use overflow or some other method to contain floats. Understanding the fact that a BFC will stop an item wrapping a float, for example, is pretty useful if you want to create a fallback for a flex or grid layout in non-supporting browsers.</p>

<p>You also understand something that is pretty fundamental in terms of how web pages are laid out by the browser. While they seem inconsequential on their own, it is these little bits of knowledge that can speed up the time it takes to create and debug CSS layouts.</p>




<div>
  <img src="https://d33wubrfki0l68.cloudfront.net/5322ca5f2bf4fad4e893ba1d32a13a16971b5212/62e76/images/logo/logo--red.svg" alt="Smashing Editorial" />
  (yk, il)
</div>


</div>




  <div id="sponsors-article-end"><ul><li><a href="https://mozilladevelopers.github.io/playground/?xv=developers&utm_source=Smashing&utm_medium=display&utm_campaign=N258203.287930SMASHINGMAGAZINE.C_207379696&utm_term=207379696&utm_content=A144_A927_C003789" target="_blank" class="readableLinkWithMediumImage"><img src="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2e836d6-0247-4dfd-9c60-821fde4d0af1/mozilla.png" width="250" /></a><br /><a href="https://mozilladevelopers.github.io/playground/?xv=developers&utm_source=Smashing&utm_medium=display&utm_campaign=N258203.287930SMASHINGMAGAZINE.C_207379696&utm_term=207379696&utm_content=A144_A927_C003789" target="_blank">Learn CSS Grid Layout</a></li><li><a href="https://www.psd2html.com/?utm_source=smashingmagazine&utm_medium=banner&utm_campaign=smashingmagazine_banner_black_webdev" target="_blank" class="readableLinkWithMediumImage"><img src="https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27f20b52-daf9-42e4-8934-aaf35266c8cc/your-web-dev-department.png" width="250" /></a><br /><a href="https://www.psd2html.com/?utm_source=smashingmagazine&utm_medium=banner&utm_campaign=smashingmagazine_banner_black_webdev" target="_blank">We develop your responsive layouts</a></li></ul></div>




			
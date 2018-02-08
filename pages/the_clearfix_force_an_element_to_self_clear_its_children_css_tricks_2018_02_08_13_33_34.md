<a href="https://css-tricks.com/snippets/css/clear-fix/">https://css-tricks.com/snippets/css/clear-fix/</a><div id="articleHeader"><h1>The Clearfix: Force an Element To Self-Clear its Children</h1></div>

    <div>

      <p>This will do you fine these days (IE 8 and up):</p>
<pre><code>.group:after {
  content: "";
  display: table;
  clear: both;
}</code></pre>
<p>Apply it to any parent element in which you need to clear the floats. For example:</p>
<pre><code>&lt;div class="group"&gt;
  &lt;div class="is-floated"&gt;&lt;/div&gt;
  &lt;div class="is-floated"&gt;&lt;/div&gt;
  &lt;div class="is-floated"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>
<p>You would use this instead of clearing the float with something like <code>&lt;br style="clear: both;" /&gt;</code> at the bottom of the parent (easy to forget, not handleable right in CSS, non-semantic) or using something like <code>overflow: hidden;</code> on the parent (you don't always want to hide overflow). </p>
<hr />
<p>Now for a bit of history!</p>
<p>This was the original popular version, designed to support browsers as far back as it possibly could:</p>
<pre><code>.clearfix:after {
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " ";
  clear: both;
  height: 0;
}
.clearfix { display: inline-block; }
/* start commented backslash hack \*/
* html .clearfix { height: 1%; }
.clearfix { display: block; }
/* close commented backslash hack */</code></pre>
<p>There then was a bit of a cleaner version <a href="http://perishablepress.com/press/2008/02/05/lessons-learned-concerning-the-clearfix-css-hack/" target="_blank">documented here</a> by Jeff Starr, based on the fact that nobody uses IE for Mac, which is what the backslash hack was all about.</p>
<pre><code>.clearfix:after {
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " ";
  clear: both;
  height: 0;
}
* html .clearfix             { zoom: 1; } /* IE6 */
*:first-child+html .clearfix { zoom: 1; } /* IE7 */</code></pre>
<p>Then it became popular to use "group" as a class name, which is nicer and more semantic (via Dan Cederholm). Also, the <code>content</code> property doesn't even need the space, it can be empty string (via Nicolas Gallagher). Then, without any text, <code>font-size</code> is un-needed (Chris Coyier).</p>
<pre><code>.group:after {
  visibility: hidden;
  display: block;
  content: "";
  clear: both;
  height: 0;
}
* html .group             { zoom: 1; } /* IE6 */
*:first-child+html .group { zoom: 1; } /* IE7 */</code></pre>
<p>Of course, if you drop IE 6 or 7 support, remove the associated lines.</p>
<div>Update May 18, 2011: Nicolas Gallagher again with the <a href="http://nicolasgallagher.com/micro-clearfix-hack/" target="_blank">"micro" clearfix</a>. Also see this <a href="http://nicolasgallagher.com/better-float-containment-in-ie/" target="_blank">additional stuff</a>.</div>
<pre><code>.group:before,
.group:after {
  content: "";
  display: table;
} 
.group:after {
  clear: both;
}
.group {
  zoom: 1; /* For IE 6/7 (trigger hasLayout) */
}</code></pre>
<p>See the top of this page for the most modern version of the clearfix. </p>
<p>In the future, we <a href="https://css-tricks.com/display-flow-root/" target="_blank">might be able to do</a>:</p>
<pre><code>.group {
  display: flow-root;
}</code></pre>

    

  </article>

  

<div>
      <div>
      <section id="comments">



  <h2>
    Comments
  </h2>

  

  <ol id="commentlist">
    
    

    

    

    

    

    <li id="li-comment-71957">

      <div id="comment-71957">

        

        <div>

          <div>
            <div>Maggie Wolfe Riley</div> <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-71957" target="_blank">Permalink to comment#</a> <time>March 5, 2010</time></div>
            
          
          
          <div>

            <p>Chris – you, like Mary Poppins, are practically perfect in every way, except for it’s and its. So in order to help you attain a higher level of perfection, I am going to give you a free lesson!!!! (are you excited yet?)</p>
<p>Possessive pronouns: his, hers, theirs, ours, mine, yours, whose, and its<br />
Notice no apostrophes on any of those – just think “his, hers, its” to help you remember that.</p>
<p>Contraction: It is shortens to it’s, he is =&gt; he’s, she is =&gt; she’s, I am =&gt; I’m, you are =&gt; you’re, they are =&gt; they’re, we are =&gt; we’re, who is =&gt; who’s</p>
<p>For pronouns, the only apostrophes are for contractions as shown above. Regular nouns do use apostrophes to show possession but not pronouns.</p>
<p>So your title for this post should be “Force Element To Self-Clear its Children” (not it’s). I see this mistake a lot in your posts, but this one stands out even more since it’s in the title.</p>
<p>Whew! That out of the way (and seeing those errors really does get in the way of content), you are awesome and I have learned SO much from you – I hope my little grammar lesson actually helps!</p>
<p>And, on topic, thank you for THIS helpful snippet!</p>

            

          </div>
        
      
    
  
</li>

    

    

    

    <li id="li-comment-87554">

      <div id="comment-87554">

        

        <div>

          <div>
             <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-87554" target="_blank">Permalink to comment#</a> <time>January 9, 2011</time></div>
            
          
          
          <div>

            <p>Wow. This is hands down one of the best designed websites I’ve seen. Everything is beautiful, loads quick, and has just the right amount of interactivity and minimalism. </p>
<p>About this post, I’m new to CSS, and this problem had me puzzled for a while, till I learned that a thing like a clearfix hack existed from a TutorialZine template. I can’t believe that so many people, for so many years, have pointed out this problem, and it still hasn’t been fixed. Semantic tags like nav and section mean little when more basic problems such as this are not addressed. I find the whole designing by CSS technique very tedious, I can’t blame developers for using tables in the past.</p>

            <div>
              <a href="https://css-tricks.com/snippets/css/clear-fix/?replytocom=87554#respond" target="_blank">Reply ↓</a>            </div>

          
        
      
    
  </li>

    

    

    

    

    <li id="li-comment-99325">

      <div id="comment-99325">

        

        <div>

          <div>
            <div>Daniel Pegues</div> <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-99325" target="_blank">Permalink to comment#</a> <time>July 8, 2011</time></div>
            
          
          
          <div>

            <p>I’ve been using this for years now, and it hasn’t failed me once. But it amazes me how people still have difficulties grasping this concept when they are UI developers. I had to teach this to a programmer of 15+ years recently, and still they are cloudy with the understanding of it.</p>
<p>One of the best examples I show them is with background colors for parent, and separate child containers. That usually clears things up almost immediately with the difference between using clear fix and not having it applied.</p>

            <div>
              <a href="https://css-tricks.com/snippets/css/clear-fix/?replytocom=99325#respond" target="_blank">Reply ↓</a>            </div>

          
        
      
    
  </li>

    <li id="li-comment-103885">

      
    
  <ul>

    <li id="li-comment-1586649">

      <div id="comment-1586649">

        

        <div>

          <div>
            <div>Kristian</div> <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-1586649" target="_blank">Permalink to comment#</a> <time>November 12, 2014</time></div>
            
          
          
          <div>

            <p>when you use floating of elements the parent element no longer tries to wrap said element. When using a ton of floated elements all as part of a layout you sometimes have to “clear” the floating children so that the parent can continue to fully wrap them as desired maintaining the proper flow from a layout/design perspective.</p>
<p>the .clearfix or .group classes when used with the above solutions provide a modular way to add this to a parent element with CSS and a class and not have to resort to adding non-semantic divs or breaks to your HTML.</p>

            

          </div>
        
      
    
  </li>

    
</ul>
</li>

    

    

    

    <li id="li-comment-133548">

      <div id="comment-133548">

        

        <div>

          <div>
            <div>Mark, me again</div> <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-133548" target="_blank">Permalink to comment#</a> <time>December 14, 2011</time></div>
            
          
          
          <div>

            <p>Overflow is the missing ‘chink’ [thanks, Patrick, you old Dog] …<br />
CSS3 parenting [CSScube] semantic ever since IE4-6, Opera.fun is simply</p>
<p>overflow: auto</p>
<p>In context, it’s [sp. for ms. Lady things]</p>
<p>.cleargroup, parentname.cleargroup {<br />
display: block;<br />
font-size: 0;<br />
overflow: auto;<br />
} </p>
<p>And then, since we’re taking this to the nth degree</p>
<pre><code>.cleargroup:after { 
display: block; 
content: " "; 
clear: both; 
font-size: 0; 
position: relative; 
} 
.cleargroup:after, *.cleargroup&lt;parentname.clearfix { 
position: relative; 
visibility: visible; 
zoom: 1;
} </code></pre>
<p>Font-size is the display element spacer, not height. Attribute font-size is the logical display anchor, and it’s value will be ignored (selector not required in new browsers? oh dear, anchor!). Echoing display:block in the attribute is critical to manage fluid float overflow inside cleargroup, with an absolute position. Relative positioning handles any CSS widgets you may throw into the cleargroup zone. For those still hobbled with old IE and Firefox foibles, the &lt;operator cache helps; operator is ignored by others. Similarly, visibillity (loosen your collar, scriptites) is managed by display:block being attached to parent and child, securing attribute operator overflow in display as required.</p>
<p>This runs especially well where build includes side-by-side vertical columns that wrap around a floated element or block. Parentname allows inclusion of an opening blockquote salvo, or whatever. A closing salvo, however, would slightly screw your float wrap, inline or otherwise. Because there’s no overflow left over. It’s one of those characteristic CSS logical die-out things, Ugh.</p>
<p>Now, the design and development question is inside of parent or outside of predecessor. On page, in new browsers it seems a non-challant either-or div. Which leaves the style cue open for scripting and devicing. For the pure at heart, there’s also cleargroup container popup tutorials. In that scenario, overflow balances clip margins, etc. </p>
<p>ergo: hope those awesome “echo” and “zone” terms in the vicinity of any CSS attribute don’t upset designers out there. The hermeneutic envelope that secures CSS discourse is not quite secure, is it? Net5 and CSS4 are on the move. … overflow:auto</p>

            <div>
              <a href="https://css-tricks.com/snippets/css/clear-fix/?replytocom=133548#respond" target="_blank">Reply ↓</a>            </div>

          
        
      
    
  <ul>

    <li id="li-comment-195069">

      <div id="comment-195069">

        

        <div>

          <div>
            <div>nnif semaj</div> <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-195069" target="_blank">Permalink to comment#</a> <time>October 5, 2012</time></div>
            
          
          
          <div>

            <p>What in holy hell are you talking about. I hate pseudo-intellectuals.</p>
<p>(Sorry, I just had to say that. It sounded funny and fit in perfectly at this juncture)</p>
<p>pseudo-intellectual: a person who attempts to pass themselves off as above the average intelligence by assuming their chosen vocabulary will confuse most people. The desired effect being: “Wow, he sounds smart!”</p>
<p>[my definition]</p>
<p>OK. I should stop now.</p>
<p>BTW – your site rocks Chris. Many blessings.</p>

            

          </div>
        
      
    
  </li>
</ul>
</li>

    

    

    

    

    <li id="li-comment-167653">

      
    
  <ul>

    <li id="li-comment-171372">

      <div id="comment-171372">

        

        <div>

          <div>
             <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-171372" target="_blank">Permalink to comment#</a> <time>May 18, 2012</time></div>
            
          
          
          <div>

            <p>Adding markup to fix styles issues is not a good idea (even if it is possible indeed) simply because markup is supposed to have semantical reasons, without any style / design implication.</p>
<p>You can add a &lt;div&gt; (or a &lt;hr&gt; or whatever) to fix floats issues, and it has been done for a long time, but it adds avoidable elements to the DOM tree, and it uses the markup on a wrong purpose. </p>
<p>Moreover, it is easier to have a class to apply to the element which needs a clear fix than adding a non semantical element before the close tag of the element which needs a clear fix.</p>

            

          </div>
        
      
    
  </li>

    

    
</ul>
</li>

    <li id="li-comment-178155">

      <div id="comment-178155">

        

        <div>

          <div>
            <div>Ronny</div> <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-178155" target="_blank">Permalink to comment#</a> <time>June 21, 2012</time></div>
            
          
          
          <div>

            <p>Hi,<br />
I love the micro clearfix hack, and find it very appropriate when writing modular CSS. Just add a .cf class to the element you’d like to clear and your done! Also, using this as a mixin when using LESS or SCSS is a breeze.</p>
<p>Still – a discussion with a colleague made me think. How is using pseudo :before/ :after affect memory usage when the browser renders the page?</p>
<p>Using content: “”; in your CSS does not insert anything into the DOM-tree, but they are being rendered into the render-tree, right?</p>
<p>Let’s say you have 1000 elements, all with the clearfix applied. The browser actually has to handle the :before and :after as well as the main element (visually). The issue arise when discussing optimization for mobile browsers. Usually they perform slower than desktop browsers.</p>
<p>If the traditional overflow:hidden can be used to clear elements (and your design let’s you use this), isn’t this better performance-wise?</p>

            <div>
              <a href="https://css-tricks.com/snippets/css/clear-fix/?replytocom=178155#respond" target="_blank">Reply ↓</a>            </div>

          
        
      
    
  <ul>

    

    <li id="li-comment-1586647">

      <div id="comment-1586647">

        

        <div>

          <div>
            <div>Kristian</div> <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-1586647" target="_blank">Permalink to comment#</a> <time>November 12, 2014</time></div>
            
          
          
          <div>

            <p>It seems unlikely that you would need a clearfix applied to so many elements on one page? if you do, perhaps before worrying about if that would bog down a browser, then perhaps you should also work on writing simpler layout HTML and CSS that wouldn’t require so many clearing events to be required to make everything go where it needs, as such a complicated or redundant pile of layout code will also be bogging down the browser.</p>
<p>overflow:hidden and overflow:auto have the occasional problem where they either a) hide stuff that you don’t want hidden, or b) show scroll bars sometimes if things get a little off. Neither of these is optimal in my book, so these clearfix hacks are the preferred method. There is a reason people like Chris and Nic Gallagher promote these solutions — from a layout/design perspective they are reliable and have less adverse affects than the alternative.</p>

            

          </div>
        
      
    
  </li>
</ul>
</li>

    

    <li id="li-comment-184082">

      <div id="comment-184082">

        

        <div>

          <div>
            <div>Derek</div> <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-184082" target="_blank">Permalink to comment#</a> <time>July 31, 2012</time></div>
            
          
          
          <div>

            <p>Using the universal selector (*) has pretty severe adverse performance implications. Adding single top-level wildcard to your CSS like you’ve shown will usually at least quadruple your CSS parse time in my experience. Better to use IE conditional comments for the IE specific stuff so that you don’t slow down everyone else’s browser (not to mention that it’s not a hack, but a supported feature designed to do exactly what you want to do that you can rely on).</p>

            <div>
              <a href="https://css-tricks.com/snippets/css/clear-fix/?replytocom=184082#respond" target="_blank">Reply ↓</a>            </div>

          
        
      
    
  </li>

    <li id="li-comment-184087">

      <div id="comment-184087">

        

        <div>

          <div>
            <div>Chris Coyier</div> <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-184087" target="_blank">Permalink to comment#</a> <time>July 31, 2012</time></div>
            
          
          
          <div>

            <blockquote><p>Using the universal selector (*) has pretty severe adverse performance implications.</p></blockquote>
<p>Do you have some real data on that? I’ve literally never seen data to that effect. I know that, technically, yes, that selector is going to take long to parse than an ID selector, but is it literally a delay that you can feel? My hypothesis is that it’s not a big deal you either have a page with WAY more elements than an average site has or you use TONS of universal selectors.</p>

            <div>
              <a href="https://css-tricks.com/snippets/css/clear-fix/?replytocom=184087#respond" target="_blank">Reply ↓</a>            </div>

          
        
      
    
  
</li>

    

    

    

    <li id="li-comment-197544">

      <div id="comment-197544">

        

        <div>

          <div>
            <div>Jerry</div> <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-197544" target="_blank">Permalink to comment#</a> <time>October 15, 2012</time></div>
            
          
          
          <div>

            <p>Compatibility Issue : ?</p>
<p>I don’t know if you’ve tried looking at this site using<br />
Opera 12.02<br />
Build 1578<br />
Windows 7 ( 32 bit ),</p>
<p>but the CSS snippets, don’t look good at all.</p>
<p>The snippets require the user to scroll horizontally to view the whole snippet, which makes it hard to read.</p>
<p>I tried this on Chrome and it works as expected but Opera puts it all on 1 line and adds a left-right scroll bar.</p>
<p>Very unpleasant for us Opera users. I just wanted to let you know in case it matters to you.</p>

            

          </div>
        
      
    
  </li>

    

    

    

    

    

    

    

    

    <li id="li-comment-481607">

      
    
  <ul>

    

    

    <li id="li-comment-1089949">

      <div id="comment-1089949">

        

        <div>

          <div>
             <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-1089949" target="_blank">Permalink to comment#</a> <time>January 16, 2014</time></div>
            
          
          
          <div>

            <p>I believe the second-to-last one is the most recent “update” to the clearfix (and you can use the last one if you don’t support IE6/7). I know that doesn’t seem right as the date on it says August 2012 but I am going through CodeSchool.com and that is what they are using. Also, he mentions how he updates to using .group instead of .clearfix which would nullify any which use clearfix as the class name. You can see that it is also more simple than the others which, I’m assuming would mean that it is more relevant as things tend to get simpler over time.</p>
<p>Could be wrong but that is just my two-cents.</p>

            

          </div>
        
      
    
  </li>
</ul>
</li>

    

    

    <li id="li-comment-746606">

      <div id="comment-746606">

        

        <div>

          <div>
            <div>A humble Brazilian.</div> <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-746606" target="_blank">Permalink to comment#</a> <time>December 1, 2013</time></div>
            
          
          
          <div>

            <p>What’s up everybody?!</p>
<p>I’ve been looking in the entire internet to solve this bug with firefox. My site presents perfectly in chrome, I.E., but firefox was blank (yea, nothing inside the “container” appears in screen).</p>
<p>The Solution: #contaier {overflow: auto; clear: both;}<br />
obs. “container” is the ID name of the main div in my site.</p>
<p>Problems I had:<br />
Adding a div with the property “clear: both” inside the container worked until I realized that my “border-radius” disappeared.<br />
“Overflow: visible” (only) showed the elements, BUT the background color also disappeared.<br />
“clear: both” (only) also doesn’t show the background.</p>
<p>For me, this worked very well.<br />
I really hopped to explain more about this issue, but my English is not so good for that.</p>

            <div>
              <a href="https://css-tricks.com/snippets/css/clear-fix/?replytocom=746606#respond" target="_blank">Reply ↓</a>            </div>

          
        
      
    
  </li>

    

    

    

    <li id="li-comment-1583593">

      <div id="comment-1583593">

        

        <div>

          <div>
            <div>chris.</div> <div><a href="https://css-tricks.com/snippets/css/clear-fix/#comment-1583593" target="_blank">Permalink to comment#</a> <time>July 9, 2014</time></div>
            
          
          
          <div>

            <p>All kudos to the author, but the point of css is cut out redundant styling. So their version while it works great would be better like this.</p>
<pre><code>    `/* our Global CSS file */
    article:after, aside:after, div:after, footer:after, 
    form:after, header:after, nav:after, section:after, ul:after {
        clear:both; content:".";
        display:block;
        height:0;
        visibility:hidden;
    }

    /* our ie CSS file */
    article, aside, div, footer,
    form, header, nav, section, ul {
        zoom:1; 
    }`
</code></pre>
<p>No need to repeat the same line over and again for each element to clear right? now that is some nice automatic clearing right there. Excellent.</p>

            <div>
              <a href="https://css-tricks.com/snippets/css/clear-fix/?replytocom=1583593#respond" target="_blank">Reply ↓</a>            </div>

          
        
      
    
  </li>

    

    

    

    

    

    

    

    

    

    

    

    

    
  </ol>



  <div id="respond">

    
      
		<div id="respond">
							<h3 id="reply-title">Leave a Comment					<small><a href="/snippets/css/clear-fix/#respond" id="cancel-comment-reply-link" target="_blank">Cancel reply</a></small>
				</h3>
						
				
				
				
				
			
		</div>

		
		

		
      <div>

        <div>
          <h4>Posting Code!</h4>

          <p>You may write comments in <strong>Markdown</strong>. This makes code easy to post, as you can write inline code like `&lt;div&gt;this&lt;/div&gt;` or multiline blocks of code in triple backtick fences (```) with double new lines before and after.</p>
        </div>

        <div>
          <h4>Code of Conduct</h4>

          <p>Absolutely anyone is welcome to submit a comment here. But not all comments will be posted. Think of it like writing a letter to the editor. All submitted comments will be read, but not all published. Published comments will be on-topic, helpful, and further the discussion or debate.</p>
        </div>

        <div>
          <h4>Want to tell us something privately?</h4>

          <p>Feel free to use our <a href="/contact/" target="_blank">contact form</a>. That's a great place to let us know about typos or anything off-topic.</p>
        </div>

      </div>

    
  </div>

</section>    </div>
  </div>
</div>




  </div>

  <footer>

    

    <div>

      <img src="https://cdn.css-tricks.com/wp-content/themes/CSS-Tricks-16/images/get-the-newsletter.png" alt="Get the Newsletter!" />

      

        <p>
          <label>Email Address</label>
          
          
          
        </p>
        
        

      
    </div>

    <div>
      Lots of great stuff that isn't published anywhere else!
    </div>

  </footer>

  <footer>

    
    <div>
      <a href="https://mediatemple.net/landing/csstricks/?utm_source=CSS-Tricks&utm_medium=display&utm_campaign=heaeder-box" target="_blank" class="readableLinkWithMediumImage"><img src="https://cdn.css-tricks.com/wp-content/themes/CSS-Tricks-16/images/mediatemple-logo-white-superwide.svg" alt="Media Temple" /></a>
    </div>
    <div>
      <a href="https://mediatemple.net/landing/csstricks/?utm_source=CSS-Tricks&utm_medium=display&utm_campaign=heaeder-box" target="_blank">CSS-Tricks web host since day one. Save 20% with code <strong>CSSTRICKS</strong>.</a>
    </div>

  </footer>

  <footer>

    

    <div>
      <div>
        <p>CSS-Tricks* is created, written by, and maintained by <a href="http://chriscoyier.net" target="_blank">Chris Coyier</a> and <a href="/about/" target="_blank">a team</a> of swell people. It is built on <a href="http://wordpress.org/" target="_blank">WordPress</a>, hosted by <a href="https://mediatemple.net/landing/csstricks/?utm_source=CSS-Tricks&utm_medium=display&utm_campaign=footer-link" target="_blank">Media Temple</a>, and the assets are served by <a href="http://tracking.maxcdn.com/c/13088/3982/378" target="_blank">MaxCDN</a>. It is made possible through <a href="/advertising/" target="_blank">sponsorships</a> from products and services we like.</p>

        <p><small>*May or may not contain any actual "CSS" or "Tricks".</small></p>

        
      </div>

      <nav>
        <a href="/contact/" target="_blank">Contact</a>
        <a href="/about/" target="_blank">About</a>
        <a href="/archives/" target="_blank">Archives</a>
        <a href="/advertising/" target="_blank">Advertise</a>
        <a href="/jobs/" target="_blank">Jobs</a>
        <a href="/license/" target="_blank">License</a>
        <a href="/subscription-options/" target="_blank">Subscribe</a>
        <a href="/random" target="_blank">Random</a>
        <a href="/guest-posting/" target="_blank">Guest Posting</a>
      </nav>

    </div>

    

  </footer>

  <svg><symbol id="icon-anchor"><title>icon-anchor</title></symbol><symbol id="icon-close"><title>icon-close</title></symbol><symbol id="icon-email"><title>icon-email</title></symbol><symbol id="icon-link"><title>icon-link</title></symbol><symbol id="icon-logo-star"><title>icon-logo-star</title></symbol><symbol id="icon-menu"><title>icon-menu</title></symbol><symbol id="icon-nav-guide"><title>icon-nav-guide</title></symbol><symbol id="icon-search"><title>icon-search</title></symbol><symbol id="icon-star"><title>icon-star</title></symbol><symbol id="icon-tag"><title>icon-tag</title></symbol></svg>
  	

















		
		

		


  
    
  
















<div><h3>Like On Github</h3><div><div>*Title (label for the link)</div></div><div><div>*Comment (commit message)</div></div><div id="action-btns"><div id="logh_btn_save">Saving...</div><div id="logh_btn_cancel">Cancel</div></div></div><img src="https://pixel.wp.com/g.gif?v=ext&j=1%3A5.7.1&blog=45537868&post=3289&tz=-7&srv=css-tricks.com&host=css-tricks.com&ref=https%3A%2F%2Fwww.google.com%2F&rand=0.15368456126696217" width="6" height="5" alt=":)" id="wpstats" />
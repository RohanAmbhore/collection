<a href="https://css-tricks.com/debouncing-throttling-explained-examples/">https://css-tricks.com/debouncing-throttling-explained-examples/</a><div id="articleHeader"><h1>                Debouncing and Throttling Explained Through Examples              </h1></div>

    <p>

      
                By
        <a href="https://css-tricks.com/author/dcorbacho/" target="_blank">
                    
            David Corbacho          
        </a>
                On
        <time>
          April 6, 2016        </time>
      

              
          <a href="https://css-tricks.com/tag/animation/" target="_blank">animation</a>, <a href="https://css-tricks.com/tag/debounce/" target="_blank">debounce</a>, <a href="https://css-tricks.com/tag/events/" target="_blank">events</a>, <a href="https://css-tricks.com/tag/javascript/" target="_blank">JavaScript</a>, <a href="https://css-tricks.com/tag/throttle/" target="_blank">throttle</a>        
      
    </p>

    

      
      <p><em>The following is a guest post by <a href="https://twitter.com/dcorbacho" target="_blank">David Corbacho</a>, a front end engineer in London. We've <a href="https://css-tricks.com/the-difference-between-throttling-and-debouncing/" target="_blank">broached this topic before</a>, but this time, David is going to drive the concepts home through interactive demos that make things very clear.</em></p>
<p><strong>Debounce</strong> and <strong>throttle</strong> are two similar (but different!) techniques to control how many times we allow a function to be executed over time.</p>
<p>Having a debounced or throttled version of our function is especially useful when we are attaching the function to a DOM event. Why? Because we are giving ourselves a layer of control between the event and the execution of the function. Remember, we don't control how often those DOM events are going to be emitted. It can vary.</p>
<p>For example, let's talk about scroll events. See this example:</p>

<p>When scrolling using a trackpad, scroll wheel, or just by dragging a scrollbar can trigger easily 30 events per second. But scrolling slowly (swapping) in a smartphone could trigger as much as 100 events per second during my tests. Is your scroll handler prepared for this rate of execution?</p>
<p>In 2011, an issue popped up on the Twitter website: when you were scrolling down your Twitter feed, it became slow and unresponsive. John Resig published <a href="http://ejohn.org/blog/learning-from-twitter" target="_blank">a blog post about the problem</a> where it was explained how bad of an idea it is to directly attach expensive functions to the <code>scroll</code> event.</p>
<p>The suggested solution by John (at that time, five years ago) was a loop running every 250ms, outside of the <code>onScroll event</code>. That way the handler is not coupled to the event. With this simple technique, we can avoid ruining the user experience. </p>
<p>These days there are slightly more sophisticated ways of handling events. Let me introduce you to Debounce, Throttle, and requestAnimationFrame. We'll also look at the matching use cases.</p>
<h3 id="article-header-id-0"><a href="#article-header-id-0" target="_blank">#</a>Debounce</h3>
<p>The Debounce technique allow us to "group" multiple sequential calls in a single one. </p>
<figure id="post-240288"><div class="readableLargeImageContainer"><img src="//cdn.css-tricks.com/wp-content/uploads/2016/04/debounce.png" /></div></figure>
<p>Imagine you are in an elevator. The doors begin to close, and suddenly another person tries to get on. The elevator doesn't begin its function to change floors, the doors open again. Now it happens again with another person. The elevator is delaying its function (moving floors), but optimizing its resources.</p>
<p>Try it for yourself. Click or move the mouse on top of the button:</p>

<p>You can see how sequential fast events are represented by a single debounced event. But if the events are triggered with big gaps, the debouncing doesn't happen. </p>
<h4 id="article-header-id-1"><a href="#article-header-id-1" target="_blank">#</a>Leading edge (or "immediate")</h4>
<p>You may find it irritating that the debouncing event <em>waits</em> before triggering the function execution, until the events stop happening so rapidly. Why not trigger the function execution immediately, so it behaves exactly as the original non-debounced handler? But not fire again until there is a pause in the rapid calls.</p>
<p>You can do this! Here's an example with the <code>leading</code> flag on:</p>
<figure id="post-240291"><div class="readableLargeImageContainer"><img src="//cdn.css-tricks.com/wp-content/uploads/2016/04/debounce-leading.png" /></div><figcaption>Example of a "leading" debounce.</figcaption></figure>
<p>In underscore.js, the option is called <code>immediate</code> instead of <code>leading</code></p>
<p>Try it for yourself:</p>

<h4 id="article-header-id-2"><a href="#article-header-id-2" target="_blank">#</a>Debounce Implementations</h4>
<p>The first time I saw debounce implemented in JavaScript was in 2009 in <a href="http://unscriptable.com/2009/03/20/debouncing-javascript-methods/" target="_blank">this John Hann post</a> (who also coined the term).</p>
<p>Soon after that, Ben Alman created <a href="http://benalman.com/projects/jquery-throttle-debounce-plugin/" target="_blank">a jQuery plugin</a> (no longer maintained), and a year after, Jeremy Ashkenas <a href="https://github.com/jashkenas/underscore/commit/9e3e067f5025dbe5e93ed784f93b233882ca0ffe" target="_blank">added it to underscore.js</a>. It was later added to Lodash, a drop-in alternative to underscore.</p>
<p>The 3 implementations are a bit different internally, but their interface is almost identical.</p>
<p>There was a time that underscore adopted the debounce/throttle implementation from Lodash, after <a href="http://drupalmotion.com/article/debounce-and-throttle-visual-explanation" target="_blank">I discovered a bug</a> in the <code>_.debounce</code> function in 2013. Since then, both implementations have grown apart. </p>
<p>Lodash <a href="https://lodash.com/docs#debounce" target="_blank">has added</a> more features to its <code>_.debounce</code> and <code>_.throttle</code> functions. The original <code>immediate</code> flag was replaced with <code>leading</code> and <code>trailing</code> options. You can choose one, or both. By default, only the <code>trailing</code> edge is enabled.</p>
<p>The new <code>maxWait</code> option (only in Lodash at the moment) is not covered in this article but it can be very useful. Actually, the throttle function is defined using <code>_.debounce</code> with <code>maxWait</code>, as you see in the lodash <a href="https://github.com/lodash/lodash/blob/4.8.0-npm/throttle.js" target="_blank">source code</a>.</p>
<h4 id="article-header-id-3"><a href="#article-header-id-3" target="_blank">#</a>Debounce Examples</h4>
<h5>Resize Example</h5>
<p>When resizing a (desktop) browser window, they can emit many <code>resize</code> events while dragging the resize handle.</p>
<p>See for yourself in this demo:</p>

<p>As you can see, we are using the default <code>trailing</code> option for the resize event, because we are only interested on the final value, after user stops resizing the browser.</p>
<h5>keypress on autocomplete form with Ajax request</h5>
<p>Why to send Ajax requests to the server every 50ms, when the user is still typing? <code>_.debounce</code> can help us, avoiding extra work, and only send the request when the user stops typing.</p>
<p>Here, it wouldn't make sense to have the <code>leading</code> flag on. We want to wait to the last letter typed.</p>

<p>A similar use case would be to wait until user stops typing before validate its input. "Your password is too short" type of messages.</p>
<h3 id="article-header-id-4"><a href="#article-header-id-4" target="_blank">#</a>How to use debounce and throttle and common pitfalls</h3>
<p>It can be tempting to build your own debounce/throttle function, or copy it from some random blog post. <strong>My recommendation is to use underscore or Lodash directly.</strong> If you only need the <code>_.debounce</code> and <code>_.throttle</code> functions, you can use Lodash custom builder to output a custom 2KB minified library. Build it with this simple command:</p>
<pre><code>npm i -g lodash-cli
lodash include = debounce, throttle</code></pre>
<p>That said, most use the modular form `lodash/throttle` and `lodash/debounce` or `lodash.throttle` and `lodash.debounce` packages with webpack/browserify/rollup.</p>
<p>A common pitfall is to call the <code>_.debounce</code> function more than once:</p>
<pre><code>// WRONG
$(window).on('scroll', function() {
   _.debounce(doSomething, 300); 
});

// RIGHT
$(window).on('scroll', _.debounce(doSomething, 200));</code></pre>
<p>Creating a variable for the debounced function will allow us to call the private method <code>debounced_version.cancel()</code>, available in lodash and underscore.js, in case you need it.</p>
<pre><code>var debounced_version = _.debounce(doSomething, 200);
$(window).on('scroll', debounced_version);

// If you need it
debounced_version.cancel();</code></pre>
<h3 id="article-header-id-5"><a href="#article-header-id-5" target="_blank">#</a>Throttle</h3>
<p>By using <code>_.throttle</code>, we don't allow to our function to execute more than once every X milliseconds. </p>
<p>The main difference between this and debouncing is that throttle guarantees the execution of the function regularly, at least every X milliseconds.</p>
<p>The same way than debounce, throttle technique is covered by Ben's plugin, underscore.js and lodash.</p>
<h4 id="article-header-id-6"><a href="#article-header-id-6" target="_blank">#</a>Throttling Examples</h4>
<h5>Infinite scrolling</h5>
<p>A quite common example. The user is scrolling down your infinite-scrolling page. You need to check how far from the bottom the user is. If the user is near the bottom, we should request via Ajax more content and append it to the page.</p>
<p>Here our beloved <code>_.debounce</code> wouldn't be helpful. It only would trigger only when the user stops scrolling.. and we need to start fetching the content <em>before</em> the user reaches the bottom.<br />
With <code>_.throttle</code> we can warranty that we are checking constantly how far we are from the bottom.</p>

<h3 id="article-header-id-7"><a href="#article-header-id-7" target="_blank">#</a>requestAnimationFrame (rAF)</h3>
<p><code>requestAnimationFrame</code> is another way of rate-limiting the execution of a function.</p>
<p>It can be thought as a <code>_.throttle(dosomething, 16)</code>. But with a much higher fidelity, since it's a browser native API that aims for better accuracy.</p>
<p>We can use the rAF API, as an alternative to the throttle function, considering this pros/cons:</p>
<h4 id="article-header-id-8"><a href="#article-header-id-8" target="_blank">#</a>Pros</h4>
<ul>
<li>Aims for 60fps (frames of 16 ms) but internally will decide the best timing on how to schedule the rendering.</li>
<li>Fairly simple and standard API, not changing in the future. Less maintenance.</li>
</ul>
<h4 id="article-header-id-9"><a href="#article-header-id-9" target="_blank">#</a>Cons</h4>
<ul>
<li>The start/cancelation of rAFs it's our responsibility, unlike <code>.debounce</code> or <code>.throttle</code>, where it's managed internally.</li>
<li>If the browser tab is not active, it would not execute. Although for scroll, mouse or keyboard events this doesn't matter.</li>
<li>Although all modern browsers offer rAF, still is not supported in IE9, Opera Mini and old Android. <a href="http://www.paulirish.com/2011/requestanimationframe-for-smart-animating/" target="_blank">A polyfill</a> would <a href="http://caniuse.com/#feat=requestanimationframe" target="_blank">be needed</a> still today.</li>
<li>rAF is not supported in node.js, so you can't use it on the server to throttle filesystem events.</li>
</ul>
<p>As a rule of thumb, I would use <code>requestAnimationFrame</code> if your JavaScript function is "painting" or animating directly properties, use it at everything that involves re-calculating element positions.</p>
<p>To make Ajax requests, or deciding if adding/removing a class (that could trigger a CSS animation), I would consider <code>_.debounce</code> or <code>_.throttle</code>, where you can set up lower executing rates (200ms for example, instead of 16ms)</p>
<p>If you think that rAF could be implemented inside underscore or lodash, they both have rejected the idea, since it's a specialized use case, and it's easy enough to be called directly.</p>
<h4 id="article-header-id-10"><a href="#article-header-id-10" target="_blank">#</a>Examples of rAF</h4>
<p>I will cover only this example to use requestAnimation frame on scroll, inspired by <a href="http://www.html5rocks.com/en/tutorials/speed/animations/" target="_blank">Paul Lewis article</a>, where he explains step-by-step the logic of this example.</p>
<p>I put it side by side to compare it to <code>_.throttle</code> at 16ms. Giving similar performance, but probably rAF will give you better results on more complex scenarios.</p>

<p>A more advanced example where I've seen this technique is in the library headroom.js, where the <a href="https://github.com/WickyNilliams/headroom.js/blob/3282c23bc69b14f21bfbaf66704fa37b58e3241d/src/Debouncer.js" target="_blank">logic is decoupled</a> and wrapped inside an object.</p>
<h3 id="article-header-id-11"><a href="#article-header-id-11" target="_blank">#</a>Conclusion</h3>
<p>Use debounce, throttle and <code>requestAnimationFrame</code> to optimize your event handlers. Each technique is slightly different, but all three of them are useful and complement each other.</p>
<p>In summary:</p>
<ul>
<li><strong>debounce:</strong> Grouping a sudden burst of events (like keystrokes) into a single one.</li>
<li><strong>throttle:</strong> Guaranteeing a constant flow of executions every X milliseconds. Like checking every 200ms your scroll position to trigger a CSS animation.</li>
<li><strong>requestAnimationFrame:</strong> a throttle alternative. When your function recalculates and renders elements on screen and you want to guarantee smooth changes or animations. Note: no IE9 support.</li>
</ul>

<div id="jp-relatedposts">
	<h3 id="article-header-id-12"><a href="#article-header-id-12" target="_blank">#</a><em>Related</em></h3>
<div><div><h4><a href="https://css-tricks.com/the-difference-between-throttling-and-debouncing/" title="The Difference Between Throttling and Debouncing

I got these confused the other day and someone corrected me. So I tossed it on the ol' list of blog post ideas and here we are. Both of them are ways to limit the amount of JavaScript you are executing based on DOM events for performance reasons. But they…" target="_blank">The Difference Between Throttling and Debouncing</a></h4><p>I got these confused the other day and someone corrected me. So I tossed it on the ol' list of blog post ideas and here we are. Both of them are ways to limit the amount of JavaScript you are executing based on DOM events for performance reasons. But they…</p></div><div><h4><a href="https://css-tricks.com/capturing-all-events/" title="JavaScript Event Madness! Capturing *all* events without interference

The following is a guest post by Matthias Christen and Florian Müller from Ghostlab. Ghostlab is cross-browser cross-device testing software for Mac and PC. One of the things I'm very impressed Ghostlab can do is sync the events from one browser to all the others. Scroll one page, the others…" target="_blank">JavaScript Event Madness! Capturing *all* events without interference</a></h4><p>The following is a guest post by Matthias Christen and Florian Müller from Ghostlab. Ghostlab is cross-browser cross-device testing software for Mac and PC. One of the things I'm very impressed Ghostlab can do is sync the events from one browser to all the others. Scroll one page, the others…</p></div><div><h4><a href="https://css-tricks.com/the-javascript-behind-touch-friendly-sliders/" title="The JavaScript Behind Touch-Friendly Sliders

Kevin Foley explains how to build a swipeable gallery on touch devices." target="_blank">The JavaScript Behind Touch-Friendly Sliders</a></h4><p>Kevin Foley explains how to build a swipeable gallery on touch devices.</p></div></div></div>
    
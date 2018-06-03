<a href="http://bradfrost.com/blog/link/replacing-jquery-with-vue-js-no-build-step-necessary/">http://bradfrost.com/blog/link/replacing-jquery-with-vue-js-no-build-step-necessary/</a><div id="articleHeader"><h1>				<a href="https://www.smashingmagazine.com/2018/02/jquery-vue-javascript/" target="_blank">		            						            			Replacing jQuery With Vue.js: No Build Step Necessary				</a>			</h1></div>

			

				<p>I absolutely love this article by <a href="https://www.smashingmagazine.com/2018/02/jquery-vue-javascript/" target="_blank">Sarah Drasner</a> about replacing jQuery with <a href="https://vuejs.org/" target="_blank">Vue.js</a>. We need more articles like this. “Here’s how to replace the once-new hotness with the new hotness.”</p>
<p>I’ve been neck-deep in React-land for a while, and I’m trying to think of how this article would look like for <a href="https://reactjs.org/" target="_blank">React</a>. I’d imagine doing a <a href="https://www.smashingmagazine.com/2018/02/jquery-vue-javascript/#hiding-and-showing" target="_blank">toggle</a> would look something like:</p>
<ol>
<li>Burn all of your markup down to the ground and replace what you had with <code>&lt;div id="app" /&gt;</code></li>
<li>Rewrite your markup as <a href="https://reactjs.org/docs/introducing-jsx.html" target="_blank">JSX</a>. Be sure to replace <code>class</code> with <code>className</code> or the whole thing will blow up.</li>
<li>Inline an <code>onClick</code> attribute attached to your JSX that maps to a function to handle the click.</li>
<li>Write an <a href="https://reactjs.org/docs/handling-events.html" target="_blank">event handler</a> to handle the click. Be sure to call <code>constructor(props) { super(props); }</code> before you do anything. Add <code>this.handleClick = this.handleClick.bind(this);</code> to the constructor in order to get things to work.</li>
</ol>
<p>It may just be me, but this feels comparatively way more complicated and inelegant.</p>

<p><a href="https://twitter.com/SaraSoueidan/status/1001189524477743105" target="_blank">Sara’s talking about</a> React’s ubiquity rather than its conventions. Because migrating from something like jQuery to React is not a lateral move. It requires a major overhaul of how the entire thing is built.</p>
<p>If you tear out something like jQuery, you’re going to have to figure out a way to get those accordions to expand and collapse again. If you tear out React, you get a blank page. React is a big commitment. I guess that’s why I’m still struggling to comprehend why so many organizations are so eager to take the sturdy, foundational layer of the frontend stack and rewrite it all in a proprietary format. That’s all necessary to get reactive components? Projects like Vue are showing that’s not necessary.</p>
<p>I’m really just thinking out loud here as I continue to slog my way through React, continue to get my head around what other frameworks provide, and continue to try my damnedest to keep up with this ever-shifting web design landscape.</p>

		    
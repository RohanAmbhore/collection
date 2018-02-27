<a href="https://eric.blog/2016/08/23/set-default-node-version-with-nvm/">https://eric.blog/2016/08/23/set-default-node-version-with-nvm/</a><div id="articleHeader"><h1>Set default node version with NVM – Eric Binnion</h1></div>
		

		

	<div>
		
		<div>
			<p>I was recently figuring out how to use <code>nvm</code>, and one thing that stood out to me is that I needed to set the default version of node that I wanted to use when opening a new tab.</p>
<p>Because I was new to using <code>nvm</code> it took me a while to find the commands. So, if you happen to find this article while configuring <code>nvm</code>, hopefully you find this useful.</p>
<pre><code># Install the version that you would like 
nvm install 6.1.0

# Set 6.1.0 (or another version) as default
nvm alias default 6.1.0
</code></pre>
<p>Then you can open a new tab and if you run <code>node -v</code>, you should see <code>v6.1.0</code> (or whichever version you set as the default.</p>
<p>Easy peasy, right? Hopefully this helps you if you’re having some issues!</p>

<div id="jp-relatedposts">
	<h3><em>Related</em></h3>
</div>		</div>

			<footer>
		Tagged <a href="https://eric.blog/tag/node/" target="_blank">node</a>, <a href="https://eric.blog/tag/nvm/" target="_blank">nvm</a>	</footer>
			<div>
		

		<div>
			<h2>Published by Eric Binnion</h2>
		</div>

		<p>
			Father to a Hero, Code Wrangler at Automattic, WordPress core contributor, and alum of Midwestern State University.			<a href="https://eric.blog/author/ebinnion/" target="_blank">
				View all posts by Eric Binnion			</a>
		</p>
	</div>
	</div> 

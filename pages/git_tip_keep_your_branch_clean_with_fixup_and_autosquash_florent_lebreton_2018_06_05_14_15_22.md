<a href="https://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html">https://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html</a><div id="articleHeader"><h1>GIT tip : Keep your branch clean with fixup and autosquash</h1></div>
		
		
		<p>Who is not tired of committing a "Remove pdb" or a "Fix a typo" few minutes or hours after committing a clean feature ? A few time ago, I discovered two useful options in GIT that work together : <tt>git commit --fixup</tt> and <tt>git rebase --autosquash</tt>. With these, you can easily merge little fixes with the original feature and keep your branch clean.</p>
<p>Preferably, you won't use it in a stable or master branch, because rebase rewrites history and can create a big mess, mainly if project counts several developers. It rather can be convenient to clean a development branch before merging it in master.</p>
<div id="fixup-autosquash">
<h2>--fixup & --autosquash</h2>
<ul>
<li><tt>git commit --fixup &lt;commit&gt;</tt> automatically marks your commit as a fix of a previous commit</li>
<li><tt>git rebase -i --autosquash</tt> automatically organize merging of these fixup commits and associated normal commits</li>
</ul>
</div>
<div id="example">
<h2>Example</h2>
<p>Take a git repos with a branch <cite>dev</cite>. You intend to commit features A and B:</p>
<div><pre>$ (dev) git add featureA
$ (dev) git commit -m "Feature A is done"
[dev fb2f677] Feature A is done
$ (dev) git add featureB
$ (dev) git commit -m "Feature B is done"
[dev 733e2ff] Feature B is done
</pre></div>
<p>Your work is in progress and you find minor mistakes in Feature A : it's time to use <tt>--fixup</tt> option !</p>
<div><pre>$ (dev) git add featureA                # you've removed a pdb : shameful commit
$ (dev) git commit --fixup fb2f677
[dev c5069d5] fixup! Feature A is done
</pre></div>
<p>Here, you see that GIT automatically retrieved featureA commit message prefixed by fixup!.</p>
<p>All work is done, let's see the log:</p>
<div><pre>$ (dev) git log --oneline
c5069d5 fixup! Feature A is done
733e2ff Feature B is done
fb2f677 Feature A is done
ac5db87 Previous commit
</pre></div>
<p>Now, you want to clean your branch before merging it : it's time to use <tt>--autosquash</tt> option !</p>
<div><pre>$ (dev) git rebase -i --autosquash ac5db87
pick fb2f677 Feature A is done
fixup c5069d5 fixup! Feature A is done
fixup c9e138f fixup! Feature A is done
pick 733e2ff Feature B is done
</pre></div>
<p>This command has opened your editor with lines above. Just save & quit and ... :</p>
<div><pre>$ (dev) git log --oneline
ff4de2a Feature B is done
5478cee Feature A is done
ac5db87 Previous commit
</pre></div>
<p>Your shameful commit has been merged properly with the original feature. It's just a shorcut for something you could do otherwise but I find it very convenient :).</p>
<p>That's all folks !</p>
<p>EDIT : <tt>git rebase i &lt;after-this-commit&gt;</tt> must be launched with as argument <cite>the last commit you want to retain as-is</cite>, not the first one you want to change.</p>
<p>Thanks <a href="http://twitter.com/regilero" target="_blank">regilero</a> & <a href="http://twitter.com/SebCorbin" target="_blank">SebCorbin</a> for reviewing!</p>

	

	
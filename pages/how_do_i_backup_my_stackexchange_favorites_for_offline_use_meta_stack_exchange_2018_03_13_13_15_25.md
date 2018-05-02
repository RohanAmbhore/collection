<a href="https://meta.stackexchange.com/questions/158546/how-do-i-backup-my-stackexchange-favorites-for-offline-use">https://meta.stackexchange.com/questions/158546/how-do-i-backup-my-stackexchange-favorites-for-offline-use</a><div id="articleHeader"><h1>How do I backup my Stackexchange favorites for offline use?</h1></div>

<p>The more I use Stack Exchange, the more it is getting a knowledge-base for me.</p>

<p>All questions, that I need for later reference I mark as favorite. Now I need to store these pages locally on my laptop.</p>

<p>It is really time-consuming:</p>

<ul>
<li>I could use <kbd>Ctrl</kbd>+<kbd>S</kbd> on each favorite question page</li>
</ul>

<p><strong><em>on Linux:</em></strong><br />
there could be a solution with</p>

<pre><code>wget -N -r -l 1 "https://stackoverflow.com/users/1069083/rubo77?tab=favorites"
</code></pre>

<p>this will download all favorite questions but it creates no correct index.html</p>

<p>Another approach would be to use the <a href="http://stackexchange.com/users/1047481/rubo77?tab=accounts" target="_blank">Stack Exchange -accounts-tab</a> to automatically follow into all your Stack Exchange-accounts.<br />
But that would have to be somehow limited to only favorites links on your <a href="https://stackoverflow.com/users/1069083/rubo77?tab=favorites" target="_blank">favorites-tab</a> in each stack.</p>

<p><strong><em>cross-platform:</em></strong><br />
You would need a <em>firefox-plugin</em> that downloads links recursively but only within the favorite-area of the <a href="https://stackoverflow.com/users/1069083/rubo77?tab=favorites" target="_blank">favorites page</a> in your stack</p>
    
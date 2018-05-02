<a href="https://github.com/davidgilbertson/know-it-all">https://github.com/davidgilbertson/know-it-all</a><div id="articleHeader"><h1>Know it all</h1></div>
<p><a href="https://know-it-all.io/" target="_blank">know-it-all.io</a></p>
<p>The goal of know-it-all is to help you discover things
that you don't know about web development.</p>
<p>And maybe one day about other things too.</p>
<h2>Running it locally</h2>
<ol>
<li>fork it/clone it <code>git clone https://github.com/davidgilbertson/know-it-all.git</code></li>
<li><code>npm i</code></li>
<li>Before running in dev mode for the very first time, you must do a build (<code>npm run build</code>)</li>
<li><code>npm run dev</code> to start up the webpack dev server, then head to <code>localhost:8080</code></li>
<li><code>npm run build</code> to build the production bundles</li>
<li><code>npm start</code> to start in production mode, also at <code>localhost:8080</code>. Note that this
is hosted as a static site, so the production build just starts a very simple little NodeJS server.</li>
</ol>
<h2>Planned stuff</h2>
<ul>
<li>View a list of all "Don't know" and/or "Know of it" items.</li>
<li>Counts of scores (e.g. Don't know: 43, unrated: 8,723, etc)</li>
<li>Links to docs for each item. Maybe.</li>
<li>Search the list</li>
</ul>
<h2>Contributing</h2>
<p>I'd be delighted to get help from the greater community, I imagine
in typing out all that data I made some mistakes. Typos etc you
can go right ahead and do a PR. For any architectural change open
an issue and let's chat about it first.</p>
<p>PRs that degrade performance will not be accepted.</p>
</article>
  
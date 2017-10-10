<div class="kg-card-markdown"><p>These past few days, I dove into Visual Studio Code and TypeScript in an attempt to get a better workflow going with GraphQL / React apps. It&apos;s been a few months since evaluating the tools I use for developing every day apps, and I&apos;ve found some amazing stuff. If you implement all these things and switch to VS Code, you&apos;re going to be shocked at how many bugs you catch even before saving a file!</p>
<p><strong>ESLint + GraphQL!</strong></p>
<p>This is the biggest developer life hack I&apos;ve ever come across. Using GraphQL is the gift that never stops giving. Thanks to <a href="https://github.com/apollographql/apollo-codegen">apollo-codegen</a> you can generate types on the client side from your GraphQL schema! It looks like this:</p>
<pre><code>// This file was automatically generated and should not be edited. export type announcementsQuery = { // Daily announcements announcements: Array&lt;{ title: string; } | null&gt; | null;
};
/* tslint:enable */ </code></pre>
<p>It will only generate types for queries you&apos;re actually using, instead of adding types for things not in use on the frontend.</p>
<p>As if that wasn&apos;t cool enough, we can take this a step further. Using the graphql schema dump, we can generate eslint errors when writing queries with <a href="https://github.com/apollographql/eslint-plugin-graphql">eslint-plugin-graphql</a>. This will happen as you are typing out fields inside of a query!</p>
<p><img src="https://zach.codes/content/images/2017/10/query-1.jpg" alt="query-1"></p>
<p><strong>Types</strong></p>
<p>As I alluded to in the last example, static typing is awesome. Instead of rambling about all of TypeScript&apos;s features, I&apos;m going to show you the 3 step process it takes to implement and how it&apos;s so useful.</p>
<ol>
<li>Rename <code>.js</code> files to <code>.tsx</code></li>
<li>Add some <code>interfaces</code></li>
<li>Use the interfaces!</li>
</ol>
<p>Here&apos;s an example:</p>
<pre><code>interface MessageProps { name: string;
} export default ({ name }: MessageProps) =&gt; ( &lt;p className={styles.container}&gt; Say hello to &lt;Link to=&quot;/about/zach&quot;&gt;{name}&lt;/Link&gt; &lt;/p&gt;
);
</code></pre>
<p>Now any time I import this component, I will get an error if I don&apos;t supply a <code>name</code> prop, if I don&apos;t pass it as a string, or if I try to pass other props. This is huge if you ever refactor your code and have props that are no longer used, or when a new dev comes in. VS Code also lets you right click and peek at the type defintion from anywhere. My other favorite features include enabling <code>noUnusedLocals</code> and <code>noUnusedParameters</code> in my TypeScript config. This will show warnings for unsed code.</p>
<p><strong>Precommit checks</strong></p>
<p>Running <a href="https://github.com/prettier/prettier">prettier</a>, <a href="https://eslint.org/">eslint</a>, and <a href="https://facebook.github.io/jest/">jest</a> can be very useful. Sometimes a team member will make a small commit to my app but not have my tooling. This way when they commit, things will still get formatted and checked for linting errors. Here&apos;s how I do it.</p>
<p>Add this to your <code>package.json</code></p>
<pre><code>&quot;lint-staged&quot;: { &quot;*.test.tsx&quot;: [ &quot;jest&quot; ], &quot;*.{js,tsx,ts}&quot;: [ &quot;prettier --single-quote --trailing-comma es5 --write&quot;, &quot;eslint&quot;, &quot;git add&quot; ] },
</code></pre>
<p>Now run: <code>npm install lint-staged husky --save-dev</code></p>
<p>That&apos;s it, now these things will be ran when the corresponding file types are staged for a commit. If something fails, it will not let you commit.</p>
<p><strong>Debugging Setup</strong></p>
<p>VS Code has this really cool <a href="https://code.visualstudio.com/docs/editor/debugging">launch config</a> that lets you start your apps with the press of a button. No more <code>npm start</code>ing your server, and create react app, AND opening the browser. We can put all of this into one file and start it with a single button press. On top of this, we can set breakpoints right in our editor, and have any console errors jump directly to the line in our code with the error below it! Here&apos;s an example config that I&apos;m using:</p>
<pre><code>{ &quot;version&quot;: &quot;0.2.0&quot;, &quot;configurations&quot;: [ { &quot;name&quot;: &quot;Server&quot;, &quot;type&quot;: &quot;node&quot;, &quot;request&quot;: &quot;launch&quot;, &quot;program&quot;: &quot;${workspaceRoot}/node_modules/.bin/webpack-dev-server&quot;, &quot;args&quot;: [&quot;--hot&quot;, &quot;--inline&quot;, &quot;--config&quot;, &quot;config/dev.config.js&quot;], &quot;outFiles&quot;: [&quot;${workspaceRoot}/build/*&quot;], &quot;stopOnEntry&quot;: false, &quot;cwd&quot;: &quot;${workspaceRoot}&quot;, &quot;env&quot;: { &quot;NODE_ENV&quot;: &quot;development&quot; }, &quot;console&quot;: &quot;internalConsole&quot;, &quot;sourceMaps&quot;: true }, { &quot;name&quot;: &quot;Browser&quot;, &quot;type&quot;: &quot;chrome&quot;, &quot;request&quot;: &quot;launch&quot;, &quot;url&quot;: &quot;http://localhost:8080/&quot;, &quot;webRoot&quot;: &quot;${workspaceRoot}/&quot; } ], &quot;compounds&quot;: [ { &quot;name&quot;: &quot;Server/Browser&quot;, &quot;configurations&quot;: [&quot;Server&quot;, &quot;Browser&quot;] } ]
}
</code></pre>
<p>If you are using webpack like me, make sure <code>devtool: &apos;eval-source-map&apos;</code> is in your config. If you use anything below that in the <a href="https://webpack.js.org/configuration/devtool/">sourcemap chart</a>, breakpoints will not work and stack traces will go to the wrong location in your code.</p>
<p>After adding this launch config (read more about the feature <a href="https://code.visualstudio.com/docs/editor/debugging">here</a>) simply open up the debugger tab and hit start!</p>
<p><strong>Conclusion</strong></p>
<p>Think about a new developer joining your team. You now have so many awesome things in place, they can get up and running immediately. Download VS Code, hit start in the debugger, app is running. Want to change some data that is displayed? Have them edit a GraphQL query and immediately be told if that variable is in the schema or not. Have them use a component you made for list items, they can hover over the component and see what props it takes. Try using something else, immediate error. Now they&apos;re ready to commit.... did it break something? On precommit, linting and tests will run! I hope this helps somebody out there. If you have any other neat things to level up my development environment, leave a comment or tweet me <a href="https://twitter.com/zachcodes">@zachcodes</a>!</p>
</div>




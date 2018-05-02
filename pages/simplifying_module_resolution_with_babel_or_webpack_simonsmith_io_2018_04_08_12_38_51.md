<a href="https://simonsmith.io/simplifying-module-resolution-with-babel-or-webpack/">https://simonsmith.io/simplifying-module-resolution-with-babel-or-webpack/</a><div id="articleHeader"><h1>Simplifying module resolution with Babel or webpack</h1></div>
    <time>
      May 20, 2017
    </time>
  

  <div>
    

<p>I like to keep my projects organised and this usually means varying levels of
directory structure to satisfy my OCD. One side effect of this which I often
bump into is trying to work out how many <code>../</code> to add in an <code>import</code> or
<code>require</code> module path:</p>
<div><pre><code>import Component from '../../../components/Component'; // not found - argh!</code></pre></div>
<p>It’s ugly, but also makes moving files around prone to error. It can be equally
frustrating within various test directories to know how far away from the
source code you are.</p>

<p>Thankfully this can be solved by tooling and I’ll cover two solutions that can
be used.</p>

<h2 id="webpack-and-resolve-alias">webpack and <code>resolve.alias</code></h2>

<p>The first option for webpack users is to configure <a href="https://webpack.js.org/configuration/resolve/#resolve-alias" target="_blank">the <code>alias</code> option</a>. This works as you might expect:</p>
<div><pre><code>/* webpack.config.js */

resolve: {
  alias: {
    components: path.resolve('./assets/scripts/components'),
  },
}</code></pre></div><div><pre><code>import Component from 'components/Component'; // works!</code></pre></div>
<h3 id="a-problem">A problem</h3>

<p>Whilst it seems to work well it can fall apart when loading modules inside
tests. It’s highly unlikely that test files will be loaded via webpack so when a
module path like <code>components/Component</code> is encountered it will complain it can’t
be found.</p>

<p>If you’re using Jest this can be fixed <a href="https://facebook.github.io/jest/docs/en/configuration.html#modulenamemapper-object-string-string" target="_blank">via
configuration</a>
with <code>moduleNameMapper</code>:</p>
<div><pre><code>moduleNameMapper: {
  '^components/(.*)': '&lt;rootDir&gt;/assets/scripts/components/$1.js',
},</code></pre></div>
<p>This works as expected but now the configuration exists in two places which is
less than ideal. And what about other test runners?</p>

<h2 id="using-a-babel-plugin">Using a Babel plugin</h2>

<p>It’s likely that Babel exists in your build process these days. If so we can
instead use <a href="https://github.com/tleunen/babel-plugin-module-resolver" target="_blank">babel-plugin-module-resolver</a> to handle the aliases. This has the benefit of keeping configuration in one
place and allows all JS files passed through Babel to pick up the configuration.
This is good news for our test files.</p>

<p>Let’s say I have the following structure in a React application:</p>
<div><pre><code>src
├── client.js
├── components
│  ├── Avatar
│  ├── Bio
│  └── Search
├── store
│  ├── index.js
│  ├── reducers</code></pre></div>
<p>It would be nice to be able to require modules directly not just from <code>src</code> but
also from within <code>store</code> as well. The configuration would look like this:</p>
<div><pre><code>// .babelrc
{
  "plugins": [
    ["module-resolver", {
      "root": ["./src/**", "./src/store/**"]
    }]
  ]
}</code></pre></div>
<p>Now from either the source files or the tests we can use the shorter module
paths:</p>
<div><pre><code>import UserReducer from 'store/reducers/User';
import Component from 'components/Component';</code></pre></div>
<blockquote>
<p>This relies on your test runner of choice using Babel on the test files. I can
  highly recommend Jest as it will automatically use a <code>.babelrc</code> if one is
  found.</p>
</blockquote>

<h2 id="done">Done!</h2>

<p>Be sure to consult <a href="https://github.com/tleunen/babel-plugin-module-resolver#eslint-plugin" target="_blank">the
README</a>
for tips on handling ESLint and flow.</p>

  

  

  

  

      
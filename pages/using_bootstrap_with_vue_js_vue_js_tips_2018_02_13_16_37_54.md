<a href="http://vuetips.com/bootstrap">http://vuetips.com/bootstrap</a><div id="articleHeader"><h1>Use Bootstrap CSS with Vue.js</h1></div>

<p>This is easy. In a “classic” setup (no module bundler) just include the <code>&lt;link&gt;</code> tag, as usual.</p>

<p>If you are using the Webpack template, you may use LESS or SASS, depending on your preference :</p>

<h3 id="less-version">LESS version</h3>

<div><pre><code>npm install --save-dev bootstrap less less-loader
</code></pre>
</div>

<p>And include the LESS file in <code>src/main.js</code></p>

<div><pre><code>require('../node_modules/bootstrap/less/bootstrap.less')
</code></pre>
</div>

<h3 id="sass-version">SASS version</h3>

<div><pre><code>npm install --save-dev bootstrap-sass node-sass sass-loader
</code></pre>
</div>

<p>And include the SASS file in <code>src/main.js</code></p>

<div><pre><code>require('../node_modules/bootstrap-sass/assets/stylesheets/_bootstrap.scss')
</code></pre>
</div>

<h2 id="use-bootstrap-js-with-vuejs">Use Bootstrap JS with Vue.js</h2>

<p>Now this is fairly more complex and calls for other questions.</p>

<h3 id="do-i-really-need-bootstrap-"><em>Do I really need Bootstrap ?</em></h3>

<p>In most cases the answer is no. Bootstrap’s JS is based on jQuery, and <a href="/jquery-vs-vue-js" target="_blank">jQuery is probably not needed either</a>. <strong>I won’t describe here how to install Bootstrap JS because it just doesn’t feel right</strong>. There are alternatives and using a global JS components library is not really the way you should be thinking when working with a component-based framework such as Vue.js</p>

<h3 id="what-do-i-need-bootstrap-for-"><em>What do I need Bootstrap for ?</em></h3>

<p>One thing that comes often is <em>I like the way it looks and I already know its API</em>. If this is the main reason you want to stick with Bootstrap, it’s a good time to get out of your comfort zone. Bootstrap JS is not meant for you anymore, you have in your hands a powerful framework surrounded by a rich ecosystem, just use it.</p>

<p>Most people don’t use each and every Bootstrap JS components available. So you could start by listing the components you need, and find an alternative. Here are a few ideas of place where you may find what you need :</p>

<h4 id="elementui">ElementUI</h4>

<p>Very nice-looking, complete library. It is mostly a UI framework, but components can be used separately. Check out <a href="http://element.eleme.io" target="_blank">its website</a>, includes a showcase of every component.</p>

<p>Very professionnal looking, and a nice guide. Native language is chinese.</p>

<h4 id="bulma">Bulma</h4>

<p><a href="http://bulma.io" target="_blank">Bulma</a> is another UI library. This one is more an alternative to Bootstrap but <a href="https://github.com/fundon" target="_blank">@fundon</a> has been working on Vue.js components that come ready-to-go.</p>

<p>Check out <a href="https://github.com/vue-bulma" target="_blank"><code>vue-bulma</code></a> project page on Github. It also contains this sweet Admin template for Vue.js named <a href="https://github.com/vue-bulma/vue-admin" target="_blank"><code>vue-admin</code></a>.</p>

<h4 id="find-the-vue-xxx-version-of-your-favorite-library">Find the <code>vue-xxx</code> version of your favorite library</h4>

<p>The good thing about component-based framework is, well there are components available out there that don’t require you to write any code (beside including the component obviously).</p>

<p>Most big projects have their <code>vue-xxx</code> version available out there. Amongst the ones I use regularly, there are <a href="https://github.com/brockpetrie/vue-moment" target="_blank"><code>vue-moment</code></a> and <a href="https://github.com/jrainlau/vue-cleave" target="_blank"><code>vue-cleave</code></a> that come in very handy and simple to use.</p>

<h4 id="vuejs-components-resources">Vue.js components resources</h4>

<p>I like to check out <a href="https://www.getrevue.co/profile/vuenewsletter" target="_blank">Vue.js newsletter</a>, <a href="https://twitter.com/search?q=%23VueJS" target="_blank">Twitter</a> and the <a href="https://github.com/vuejs/awesome-vue" target="_blank"><code>awesome-vue</code></a> repository for the freshest updates.</p>

<p>If you know websites dedicated to Vue.js components, please post it in the comments.</p>

<h4 id="nothing-found--just-code-it">Nothing found ? Just code it</h4>

<p>You may not have found the component you are looking for. In the case of Bootstrap component, most of them are fairly easy to do yourself.</p>

<p>I found myself coding an autocomplete component and it was surprinsingly easy. Its code is not relevant and now outdated but start considering the component you need and think how you would do it if you had to code it yourself.</p>

<p>If it seems easy enough, just do it ! It may end up more complicated than planned but well, you’ll learn on the way.</p>

<h2 id="links">Links</h2>

<ul>
  <li><a href="https://github.com/bootstrap-vue/bootstrap-vue" target="_blank"><code>bootstrap-vue</code></a> provides Bootstrap 4 components (2/2/2017: Boostrap v4 is still in Alpha release)</li>
  <li><a href="http://bulma.io/" target="_blank">Bulma</a> is a CSS framework</li>
  <li><a href="https://github.com/yuche/vue-strap" target="_blank"><code>vue-strap</code></a> are Bootstrap Vue.js components (2/2/2017: still on its way to Vue.js 2.x)</li>
</ul>

<h2 id="feedback">Feedback</h2>

<p>If you are still going to include Bootstrap JS in your app, please tell me why in the comments.</p>

<p>This content may become outdated or irrelevant so please let me know so that I can update it.</p>


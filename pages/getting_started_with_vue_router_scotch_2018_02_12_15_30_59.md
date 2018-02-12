<a href="https://scotch.io/tutorials/getting-started-with-vue-router">https://scotch.io/tutorials/getting-started-with-vue-router</a><div id="articleHeader"><h1>Getting Started With Vue Router</h1></div>






<p>Vue is already a great Javascript library that allows you to create some really cool, dynamic, front-end applications. Vue is also great for single page applications (SPA). SPAs work a little differently that your standard backend web application built in something like PHP. Instead of making requests to different routes on the backend and getting a fully rendered page as a response, a SPA does all the page rendering on the front-end and only sends requests to the server when new data is needed or needs to be refreshed or saved.</p>
<p>This can improve the responsiveness of your web application because you can render the pages once and display them dynamically based on the current context of the application. In order to make this work, you need a way to distinguish the different views or pages from eachother. In SPAs this is done with a router. Luckily Vue has a fully supported first-party router library called vue-router.</p>
<p>In this tutorial we'll setup a simple SPA that will show some information about popular cryptocurrencies. We'll call it "Crypto Info". It will have a few pages and link those pages using vue-router. You should already be familiar with Vue as well as creating and using Vue components. Having experience with <code>.vue</code> files is helpful but not required.</p>
<h2 id="setup">
    <a href="#toc-setup" target="_blank">
      #
      Setup
    </a> 
  </h2>
<p>To get started, let's use the handy Vue command line installer. Open a terminal and run the following.</p>
<pre><code># install vue-cli
$ npm install --global vue-cli
# create a new project using the "webpack" template
$ vue init webpack router-app</code></pre>
<p>When prompted, answer the questions displayed on the screen like so. Make sure to answer "yes" for installing vue-router.</p>
<pre><code> This will install Vue 2.x version of the template.

 For Vue 1.x use: vue init webpack#1.0 router-app

? Project name router-app &lt;Enter&gt;
? Project description A Vue.js project  &lt;Enter&gt;
? Author  &lt;Enter&gt;
? Vue build standalone  &lt;Enter&gt;
? Install vue-router? Yes
? Use ESLint to lint your code? No
? Setup unit tests with Karma + Mocha? No
? Setup e2e tests with Nightwatch? No</code></pre>
<p>Once the app is setup, install all the dependencies and start up a dev server.</p>
<pre><code># install dependencies and go!
$ cd router-app
$ npm install
$ npm run dev</code></pre>
<p>You should now be able to point a browser at <a href="http://localhost:8080" target="_blank">http://localhost:8080</a> and see something like this.</p>
<p><div class="readableLargeImageContainer"><img src="https://cdn.scotch.io/3660/eoz5DLvZS5mMBSe3JPjj_welcome-page.png" /></div></p>
<h2 id="digging-in">
    <a href="#toc-digging-in" target="_blank">
      #
      Digging In
    </a> 
  </h2>
<p>The great thing about the Vue command line tool is that it will wire up vue-router for us. To get a better understanding of how it works, we can take a look the boilerplate that was created. Open <code>/src/router/index.js</code></p>
<pre><code>import Vue from 'vue'
import Router from 'vue-router'
import Hello from '@/components/Hello'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'Hello',
      component: Hello
    }
  ]
})</code></pre>
<p>The first two lines are importing vue and vue-router. The third line is importing a component called Hello. We will discuss why in a bit. The <code>@</code> is just a nice alias for the <code>/src</code> directory that was setup in webpack by the Vue command line tool.</p><div>Related Course: <a href="https://bit.ly/2gCILn1" target="_blank">Build an Online Shop with Vue</a></div>
<p>Next we tell Vue to use the vue-router plugin. Finally the router is configured with a single route. The router uses Vue components as pages. In the above example we want to render the Hello component whenever a user navigates to the <code>/</code> route.</p>
<p>Next open <code>/src/main.js</code></p>
<pre><code>// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'
import router from './router'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  template: '&lt;App/&gt;',
  components: { App }
})</code></pre>
<p>The first line is importing Vue again. The second line is bringing in a component called <code>App</code>. This will serve as the root component for the application. The third line is importing the router setup we looked at earlier. The next line tells Vue whether or not to show tips and warnings in the developer console of your browser. In this case it is set to false.</p>
<p>Finally a new Vue instance is created and mounted to the <code>#app</code> div in our html and then it instantiated the <code>App</code> component. We also inject the router configuration from earlier.</p>
<p>Now open <code>/src/App.vue</code></p>
<pre><code>&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;img src="./assets/logo.png"&gt;
    &lt;router-view&gt;&lt;/router-view&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  name: 'app'
}
&lt;/script&gt;

&lt;style&gt;
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
&lt;/style&gt;</code></pre>
<p>This, like I mentioned before, is the root component. It will serve as the point from which our page components will be rendered. Note that all the components we will use are in <code>.vue</code> files which allows us to save the template, javascript and styling into a single file.</p>
<p>Within the <code>&lt;template&gt;</code> tag we just have some simple markup. The important piece though is the <code>&lt;router-view&gt;</code> tag. The router uses this tag as a container for rendering the different components tied to the different routes. Just think of it as a placeholder.</p>
<p>The <code>&lt;script&gt;</code> tag just contains a simple Vue component object that does nothing. The <code>&lt;style&gt;</code> tag just contains some nice styling boilerplate provided by the Vue command line tool.</p>
<p>Now open <code>/src/components/Hello.vue</code></p>
<pre><code>&lt;template&gt;
  &lt;div class="hello"&gt;
    &lt;h1&gt;{{ msg }}&lt;/h1&gt;
    &lt;h2&gt;Essential Links&lt;/h2&gt;
    &lt;ul&gt;
      &lt;li&gt;&lt;a href="https://vuejs.org" target="_blank"&gt;Core Docs&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="https://forum.vuejs.org" target="_blank"&gt;Forum&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="https://gitter.im/vuejs/vue" target="_blank"&gt;Gitter Chat&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="https://twitter.com/vuejs" target="_blank"&gt;Twitter&lt;/a&gt;&lt;/li&gt;
      &lt;br&gt;
      &lt;li&gt;&lt;a href="http://vuejs-templates.github.io/webpack/" target="_blank"&gt;Docs for This Template&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
    &lt;h2&gt;Ecosystem&lt;/h2&gt;
    &lt;ul&gt;
      &lt;li&gt;&lt;a href="http://router.vuejs.org/" target="_blank"&gt;vue-router&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="http://vuex.vuejs.org/" target="_blank"&gt;vuex&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="http://vue-loader.vuejs.org/" target="_blank"&gt;vue-loader&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="https://github.com/vuejs/awesome-vue" target="_blank"&gt;awesome-vue&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
&lt;/script&gt;

&lt;!-- Add "scoped" attribute to limit CSS to this component only --&gt;
&lt;style scoped&gt;
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
&lt;/style&gt;</code></pre>
<p>This is very similar to the <code>App</code> component. Again, within the <code>&lt;template&gt;</code> tag there is the HTML markup for the component. In this case it's all the links and text shown when we pointed our browser to <a href="http://localhost:8080" target="_blank">http://localhost:8080</a>. This is because in our router config, we specified that <code>/</code> or the root path of our application should point to <code>Hello.vue</code>.</p>
<p>Now let's get rid of the default content and create a simpler home page. Edit <code>Hello.vue</code> to look like the following:</p>
<pre><code>&lt;template&gt;
  &lt;div class="hello"&gt;
    &lt;h1&gt;{{ msg }}&lt;/h1&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
  export default {
    name: 'Hello',
    data () {
      return {
        msg: 'Welcome to Crypto Info'
      }
    }
  }
&lt;/script&gt;</code></pre>
<p>If you reload, you should now see a page like this.</p>
<p><div class="readableLargeImageContainer"><img src="https://cdn.scotch.io/3660/iHR6SLT0QFjWgywSEUeD_welcome-page.png" /></div></p>
<h2 id="creating-and-linking-to-routes">
    <a href="#toc-creating-and-linking-to-routes" target="_blank">
      #
      Creating and Linking to Routes
    </a> 
  </h2>
<p>Now let's create a new page and add some links for navigating between the two. Open <code>/src/router/index.js</code> and edit it to look like the following.</p>
<pre><code>import Vue from 'vue'
import Router from 'vue-router'
import Hello from '@/components/Hello'
import About from '@/components/About'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'Hello',
      component: Hello
    },
    {
      path: '/about',
      name: 'About',
      component: About
    }
  ]
})</code></pre>
<p>We've added a new route <code>/about</code> that points to a new component called <code>About</code>. We've also imported the new component at the top. We will create this shortly.</p>
<p>Now open <code>/src/App.vue</code> and edit the <code>&lt;template&gt;</code> section to look like this.</p>
<pre><code>&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;img src="./assets/logo.png"&gt;
    &lt;router-link :to="{ name: 'Hello' }"&gt;Home&lt;/router-link&gt;
    &lt;router-link to="/about"&gt;About&lt;/router-link&gt;
    &lt;router-view&gt;&lt;/router-view&gt;
  &lt;/div&gt;
&lt;/template&gt;</code></pre>
<p>As you can see, we added two <code>&lt;router-link&gt;</code> tags using two different methods. The router uses <code>&lt;router-link&gt;</code> to create html links to routes you created. The first method uses a named route. If you recall, in <code>/src/router/index.js</code> we added the <code>name</code> parameter to our routes. In this case the name of the route is <code>Hello</code> just like the component it points to. The second method is the standard method and just specifies the path we want to link to.</p>
<p>If you refresh the browser, you should see the original welcome page but with two links added.</p>
<p><img /></p>
<p>If you click the <code>About</code> link, you will get a blank page. This is because we haven't created the component yet. Let's fix this be creating <code>/src/components/About.vue</code>.</p>
<pre><code>&lt;template&gt;
  &lt;div class="about"&gt;
    &lt;h1&gt;What is a Crypto-Currency?&lt;/h1&gt;
    &lt;p&gt;
      It's a digital currency in which encryption techniques are used to regulate the generation of units of currency 
      and verify the transfer of funds, operating independently of a central bank.
    &lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  name: 'About'
}
&lt;/script&gt;</code></pre>
<p>Now if you refresh the browser and click <code>About</code> you should see the new page.</p>
<p><img /></p>
<h2 id="dynamic-routes">
    <a href="#toc-dynamic-routes" target="_blank">
      #
      Dynamic Routes
    </a> 
  </h2>
<p>So we can create a new page and a route to point to it but what about passing parameters? We'll need a page that displays some useful info about various crypto currencies based on a string id passed in the URL. Let's make that happen. Open <code>/src/router/index.js</code> again and add a third route.</p>
<pre><code>...
import Coins from '@/components/Coins'

...

export default new Router({
  routes: [
    ...
   {
      path: '/coins/:id',
      name: 'Coins',
      component: Coins
    }
  ]
})</code></pre>
<p>In order to display up-to-date information on the various currencies, we'll use the popular <a href="https://github.com/mzabriskie/axios" target="_blank">axios</a> http client to fetch data from the free <a href="https://coinmarketcap.com/api/" target="_blank">Coin Market Capitalization</a> API. We'll accept a string parameter in the URL called <code>:id</code>. This will be passed to the API to retrieve the relevant data.</p>
<p>First we need to install axios.</p>
<pre><code>npm install --save axios</code></pre>
<p>Next create a file called <code>/src/components/Coins.vue</code></p>
<pre><code>&lt;template&gt;
  &lt;div&gt;
    &lt;p&gt;Name: {{ coin.name }}&lt;/p&gt;
    &lt;p&gt;Symbol: {{ coin.symbol }}&lt;/p&gt;
    &lt;p&gt;Price (USD): {{ coin.price_usd }}&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
  import axios from 'axios'

  export default {
    name: 'Coins',

    data() {
      return {
        coin: {}
      }
    },

    created() {
      this.fetchData()
    },

    watch: {
      '$route': 'fetchData'
    },

    methods: {
      fetchData() {
        axios.get('https://api.coinmarketcap.com/v1/ticker/'+this.$route.params.id+'/')
        .then((resp) =&gt; {
          this.coin = resp.data[0]
          console.log(resp)
        })
        .catch((err) =&gt; {
          console.log(err)
        })
      }
    }
  }
&lt;/script&gt;</code></pre>
<p>You'll notice that in the data object of our component, we declare an empty object called <code>coin</code>. This will store our coin information after it is fetched. In the <code>&lt;template&gt;</code> section we have some markup to display the name, symbol and US dollar price of the coin. The <code>created</code> method is a special hook used by Vue that is called before the component is rendered. In this case we are calling the <code>fetchData</code> method which is making a <code>GET</code> request with axios to the Coin Market Capitalization API and passing the <code>:id</code> parameter at the end. </p>
<p>We get the parameter from the <code>$route</code> object <code>params</code> property. This object is auto injected by VueRouter. The paramater we want is the <code>:id</code> parameter which we defined in our router file. On success, as defined in the the <code>then</code> promise method, we save the data returned into our <code>coin</code> object. This is then rendered on in the template.</p>
<p>One other thing we need is to add a <code>watch</code> hook for the <code>$route</code> object. VueRouter components are only rendered once for speed. If you need to rerender, you need to do that manually so in this case we want to rerender when the <code>:id</code> parameter in <code>$route</code> changes and then fetch new data.</p>
<p>Now lets create a few more links in <code>/src/App.vue</code> to see how this new page might be used. </p>
<pre><code>&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;img src="./assets/logo.png"&gt;
    &lt;router-link :to="{ name: 'Hello' }"&gt;Home&lt;/router-link&gt;
    &lt;router-link to="/about"&gt;About&lt;/router-link&gt;
    &lt;router-link to="/coins/ethereum"&gt;Ethereum&lt;/router-link&gt;
    &lt;router-link to="/coins/bitcoin"&gt;Bitcoin&lt;/router-link&gt;
    &lt;router-view&gt;&lt;/router-view&gt;
  &lt;/div&gt;
&lt;/template&gt;</code></pre>
<p>If you refresh the browser and click on <code>Ethereum</code> you should see something like this.</p>
<p><img /></p>
<p>Now click on <code>Bitcoin</code> and you should see relevant information for that coin as well. If you want to try out other coins, have a look at <a href="https://api.coinmarketcap.com/v1/ticker/" target="_blank">https://api.coinmarketcap.com/v1/ticker/</a> and paste a few ids from the list into the URL of our app.</p>
<h2 id="conclusion">
    <a href="#toc-conclusion" target="_blank">
      #
      Conclusion
    </a> 
  </h2>
<p>That's how easy it is to get started with Vue Router. There are a bunch of other great features as well and you can read about them in the official documentation. I hope this tutorial is enough to get you started making some cool SPAs in Vue!</p>

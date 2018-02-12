<a href="https://vuejsdevelopers.com/2017/04/22/vue-js-libraries-plugins/">https://vuejsdevelopers.com/2017/04/22/vue-js-libraries-plugins/</a><div id="articleHeader"><h1>Use Any Javascript Library With Vue.js</h1></div>  <p>Lodash, Moment, Axios, Async…these are useful Javascript libraries that you’ll want to utilise in many of your Vue.js apps.</p> <p>But as your project grows you’ll be separating code into single file components and module files. You also may want to run your app in different environments to allow server rendering.</p> <p>Unless you find an easy and robust way to include those Javascript libraries across your components and module files they’re going to be a nuisance!</p> <h2>How <em>not</em> to include a library in a Vue.js project</h2> <h3>Global variable</h3> <p>The naive way to add a library to your project is to make it a global variable by attaching it to the <code>window</code> object:</p> <p><em>entry.js</em></p> <div><pre><code>window._ = require('lodash');
</code></pre></div> <p><em>MyComponent.vue</em></p> <div><pre><code>export default {
  created() {
    console.log(_.isEmpty() ? 'Lodash everywhere!' : 'Uh oh..');
  }
}
</code></pre></div> <p>The case against window variables is a long one, but, specifically to this discussion, they don’t work with server rendering. When the app runs on the server the <code>window</code> object will be undefined and so attempting to access a property will end with an error.</p> <h3>Importing in every file</h3> <p>Another second-rate method is to import the library into every file:</p> <p><em>MyComponent.vue</em></p> <div><pre><code>import _ from 'lodash';

export default {
  created() {
    console.log(_.isEmpty() ? 'Lodash is available here!' : 'Uh oh..');
  }
}
</code></pre></div> <p>This works, but it’s not very DRY and it’s basically just a pain: you have to remember to import it into every file, and remove it again if you stop using it in that file. And if you don’t setup your build tool correctly you may end up with multiple copies of the same library in your build.</p> <h2>A better way</h2>  <p>The cleanest and most robust way to use a Javascript library in a Vue project is to proxy it to a property of the Vue prototype object. Let’s do that to add the Moment date and time library to our project:</p> <p><em>entry.js</em></p> <div><pre><code>import moment from 'moment';
Object.definePrototype(Vue.prototype, '$moment', { value: moment });
</code></pre></div> <p>Since all components inherit their methods from the Vue prototype object this will make Moment automatically available across any and all components with no global variables or anything to manually import. It can simply be accessed in any instance/component from <code>this.$moment</code>:</p> <p><em>MyNewComponent.vue</em></p> <div><pre><code>export default {
  created() {
    console.log('The time is ' . this.$moment().format("HH:mm"));
  }
}
</code></pre></div> <p>Let’s take the time now to understand how this works.</p> <h3>Object.defineProperty</h3> <p>We would normally set an object property like this:</p> <div><pre><code>Vue.prototype.$moment = moment;
</code></pre></div> <p>You could do that here, but by using <code>Object.defineProperty</code> instead we are able to define our property with a <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty" target="_blank">descriptor</a>. A descriptor allows us to set some low-level details such as whether or not our property is writeable and whether it shows up during enumeration in a <code>for</code> loop and more.</p> <p>We don’t normally bother with this in our day-to-day Javascript because 99% of the time we don’t need that level of detail with a property assignment. But here it gives us a distinct advantage: properties created with a descriptor are <em>read-only</em> by default.</p> <p>This means that some coffee-deprived developer (probably you) won’t be able to do something silly like this in a component and break everything:</p> <div><pre><code>this.$http = 'Assign some random thing to the instance method';
this.$http.get('/'); // TypeError: this.$http.get is not a function
</code></pre></div> <p>Instead, our read-only instance method protects our library, and if you attempt to overwrite it you will get “TypeError: Cannot assign to read only property”.</p>  <p>You’ll notice that we proxy our library to a property name prefixed with the dollar sign “$”. You’ve probably also seen other properties and methods like <code>$refs</code>, <code>$on</code>, <code>$mount</code> etc which have this prefix too.</p> <p>While not required, the prefix is added to properties to remind coffee-deprived developers (you, again) that this is a public API property or method that you’re welcome to use, unlike other properties of the instance that are probably just for Vue’s internal use.</p> <p>Being a prototype-based language, there are no (real) classes in Javascript so it doesn’t have “private” and “public” variables or “static” methods. This convention is a mild substitute which I think is worthwhile to follow.</p> <h3><em>this</em></h3> <p>You’ll also notice that to use the library you use <code>this.libraryName</code> which is probably not a surprise since it is now an instance method.</p> <p>One consequence of this, though, is that unlike a global variable you must ensure you’re in the correct scope when using your library. Inside callback methods you can’t access the <code>this</code> that your library inhabits.</p> <p>Fat arrow callbacks are a good solution to making sure you stay in the right scope:</p> <div><pre><code>this.$http.get('/').then(res =&gt; {
  if (res.status !== 200) {
    this.$http.get('/') // etc
    // Only works in a fat arrow callback.
  }
});
</code></pre></div> <h2>Why not make it a plugin?</h2> <p>If you’re planning to use a library across many Vue projects, or you want to share it with the world, you can build this into your own plugin!</p> <p>A plugin abstracts complexity and allows you to simply do the following in a project to add your chosen library:</p> <div><pre><code>import MyLibraryPlugin from 'my-library-plugin';
Vue.use(MyLibraryPlugin);
</code></pre></div> <p>With these two lines we can use the library in any component just like we can with Vue Router, Vuex and other plugins that utilise <code>Vue.use</code>.</p> <h3>Writing a plugin</h3> <p>Firstly, create a file for your plugin. In this example I’ll make a plugin that adds Axios to your all your Vue instances and components, so I’ll call the file <em>axios.js</em>.</p> <p>The main thing to understand is that a plugin must expose an <code>install</code> method which takes the Vue constructor as the first argument:</p> <p><em>axios.js</em></p> <div><pre><code>export default {
  install: function(Vue) {
    // Do stuff
  }
}
</code></pre></div> <p>Now we can use our previos method to add the library to the prototype object:</p> <p><em>axios.js</em></p> <div><pre><code>import axios from 'axios';

export default {
  install: function(Vue,) {
    Object.defineProperty(Vue.prototype, '$http', { value: axios });
  }
}
</code></pre></div> <p>The <code>use</code> instance method is all we now need to add our library to a project. For example, we can now add the Axios library as easily as this:</p> <p><em>entry.js</em></p> <div><pre><code>import AxiosPlugin from './axios.js';
Vue.use(AxiosPlugin);

new Vue({
  created() {
    console.log(this.$http ? 'Axios works!' : 'Uh oh..');
  }
})
</code></pre></div> <h3>Bonus: plugin optional arguments</h3> <p>Your plugin install method can take optional arguments. Some devs might not like calling their Axios instance method <code>$http</code> since Vue Resource is commonly given that name, so let’s use an optional argument to allow them to change it to whatever they like:</p> <p><em>axios.js</em></p> <div><pre><code>import axios from 'axios';

export default {
  install: function(Vue, name = '$http') {
    Object.defineProperty(Vue.prototype, name, { value: axios });
  }
}
</code></pre></div> <p><em>entry.js</em></p> <div><pre><code>import AxiosPlugin from './axios.js';
Vue.use(AxiosPlugin, '$axios');

new Vue({
  created() {
    console.log(this.$axios ? 'Axios works!' : 'Uh oh..');
  }
})
</code></pre></div> 
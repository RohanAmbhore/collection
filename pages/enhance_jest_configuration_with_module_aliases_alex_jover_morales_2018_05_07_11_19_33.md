<a href="https://alexjoverm.github.io/2017/10/07/Enhance-Jest-configuration-with-Module-Aliases/">https://alexjoverm.github.io/2017/10/07/Enhance-Jest-configuration-with-Module-Aliases/</a><div id="articleHeader"><h1>Enhance Jest configuration with Module Aliases</h1></div><p>Posted on Oct 7 2017 · <a href="/tags/VueJS/" target="_blank">VueJS</a> · <a href="/tags/JavaScript/" target="_blank">JavaScript</a> · <a href="/tags/Testing/" target="_blank">Testing</a></p></header><p>Learn how to use Module Aliases Jest configuration to avoid using relative paths.</p>

<p>The module managers we have in the JavaScript community, mainly ES Modules and CommonJS, don’t support project-based paths. They only support relative paths for our own modules, and paths for the <code>node_modules</code> folder. When a project grows a bit, it’s common to see paths such:</p>
<pre><code>import SomeComponent from '../../../../components/SomeComponent'
</code></pre>
<p>Luckily, we have different ways to cope with this, in a way that we can define aliases for folders relative to the project root, so we could the above line like:</p>
<pre><code>import SomeComponent from '@/components/SomeComponent'
</code></pre>
<p>The <code>@</code> here is an arbitrary character to define the root project, you can define your own. Let’s see what solutions we have to apply module aliasing. Let’s start <a href="https://github.com/alexjoverm/vue-testing-series/tree/test-slots" target="_blank">from where we left it on the last article</a>.</p>
<h2 id="Webpack-aliases">Webpack aliases</h2><p><a href="https://webpack.js.org/configuration/resolve/#resolve-alias" target="_blank">Webpack aliases</a> are very simple to set up. You just need to add a <code>resolve.alias</code> property in your webpack configuration. If you take a look at the <code>build/webpack.base.conf.js</code>, it already has it defined:</p>
<pre><code>{
  ...
  resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
    }
  }
}
</code></pre>
<p>Taking this as an entry point, we can add a simple alias that points to the <code>src</code> folder and use that as the root:</p>
<pre><code>{
  ...
  resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': path.join(__dirname, '..', 'src')
    }
  }
}
</code></pre>
<p>Just with this, we can access anything taking the root project as the <code>@</code> symbol. Let’s go to <code>src/App.vue</code> and change the reference to those two components:</p>
<pre><code>  import MessageList from '@/components/MessageList'
  import Message from '@/components/Message'
  ...
</code></pre>
<p>And if we run <code>npm start</code> and open the browser at <code>localhost:8080</code>, that should work out of the box.</p>
<p>However, if we try to run the tests by running <code>npm t</code>, we’ll see Jest doesn’t find the modules. We still didn’t configured Jest to do so. So let’s go to <code>package.json</code> where the Jest config is, and add <code>"@/([^\\.]*)$": "&lt;rootDir&gt;/src/$1"</code> to <code>moduleNameMapper</code>:</p>
<pre><code>"jest": {
    "moduleNameMapper": {
      "@(.*)$": "&lt;rootDir&gt;/src/$1",
      "^vue$": "vue/dist/vue.common.js"
    },
...
</code></pre>
<p>Let’s explain it:</p>
<ul>
<li><code>@(.*)$</code>: Whatever starts with <code>@</code>, and continues with literally whatever (<code>(.*)$</code>) till the end of the string, grouping it by using the parenthesis</li>
<li><code>&lt;rootDir&gt;/src/$1</code>: <code>&lt;rootDir&gt;</code> is a special word of Jest, meaning the root directory. Then we map it to the <code>src</code>, and with <code>$1</code> we append the whatever clause from the <code>(.*)</code> statement.</li>
</ul>
<p>For example, <code>@/components/MessageList</code> will be mapped to <code>../src/components/MessageList</code> when you’re importing it from the <code>src</code> or <code>test</code> folders.</p>
<p>That’s really it. Now you can even update your <code>App.test.js</code> file to use the alias as well, since it’s usable from within the tests:</p>
<pre><code>import { shallow } from "vue-test-utils"
import App from "@/App"
...
</code></pre>
<p>And it will work for both <code>.vue</code> and <code>.js</code> files.</p>
<h2 id="Multiple-aliases">Multiple aliases</h2><p>Very often, multiple aliases are used for convenience, so instead of using just a <code>@</code> to define your root folder, you use many. For example, let’s say you have a <code>actions</code> and <code>models</code> folder. If you create an alias for each one, and then you move the folders around, you just need to change the aliases instead of updating all the references to it in the codebase. That’s the power of module aliases, they make your codebase more maintainable and cleaner.</p>
<p>Let’s add a <code>components</code> alias in <code>build/webpack.base.conf.js</code>:</p>
<pre><code>{
  ...
  resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': path.join(__dirname, '..', 'src')
      'components': path.join(__dirname, '..', 'src', 'components')
    }
  }
}
</code></pre>
<p>Then, we just need to add it as well to the Jest configuration in <code>package.json</code>:</p>
<pre><code>"jest": {
    "moduleNameMapper": {
      "@(.*)$": "&lt;rootDir&gt;/src/$1",
      "components(.*)$": "&lt;rootDir&gt;/src/components/$1",
      "^vue$": "vue/dist/vue.common.js"
    },
...
</code></pre>
<p>As simple as that. Now, we can try in <code>App.vue</code> to use both forms:</p>
<pre><code>import MessageList from 'components/MessageList'
import Message from '@/components/Message'
</code></pre>
<p>Stop and re-run the tests, and that should work, as well as if you run <code>npm start</code> and try it.</p>
<h2 id="Other-solutions">Other solutions</h2><p>I’ve seen <a href="https://github.com/trayio/babel-plugin-webpack-alias" target="_blank">babel-plugin-webpack-alias</a>, specially used for other testing frameworks such as <a href="https://mochajs.org/" target="_blank">mocha</a> which doesn’t have a module mapper.</p>
<p>I haven’t tried it myself, since Jest already gives you that, but if you have or wanna try, please share how it went!</p>
<h2 id="Conclusion">Conclusion</h2><p>Adding module aliases is very simple and can keep your codebase much cleaner and easier to maintain. Jest makes it as well very easy to define them, you just need to keep in in sync with the Webpack aliases, and you can say bye-bye to the dot-hell references.</p>
<p>Find the <a href="https://github.com/alexjoverm/vue-testing-series/tree/Enhance-Jest-configuration-with-Module-Aliases" target="_blank">full example on Github</a></p>

    <p>If you like it, please go and share it!
    You can follow me <a href="https://egghead.io/instructors/alex-jover-morales" target="_blank">recording videos on Egghead</a>
    or on twitter as <a href="https://twitter.com/alexjoverm" target="_blank">@alexjoverm</a>. Any questions? Shoot!</p>
  
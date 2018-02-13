<a href="https://stackoverflow.com/questions/42749973/es6-import-using-at-sign-in-path-in-a-vue-js-project-using-webpack">https://stackoverflow.com/questions/42749973/es6-import-using-at-sign-in-path-in-a-vue-js-project-using-webpack</a><div id="articleHeader"><h1>ES6 import using at ('@') sign in path in a vue.js project using Webpack</h1></div>

<p>I'm starting out a new vue.js project so I used the vue-cli tool to scaffold out a new webpack project (i.e. <code>vue init webpack</code>).</p>

<p>As I was walking through the generated files I noticed the following imports in the <code>src/router/index.js</code> file:</p>

<pre><code>import Vue from 'vue'
import Router from 'vue-router'
import Hello from '@/components/Hello' // &lt;- this one is what my qusestion is about

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

<p>I've not seen the at sign (<code>@</code>) in a path before. I suspect it allows for relative paths (maybe?) but I wanted to be sure I understand what it truly does. </p>

<p>I tried searching around online but wasn't able to find an explanation (prob because searching for "at sign" or using the literal character <code>@</code> doesn't help as search criteria).</p>

<p>What does the <code>@</code> do in this path (link to documentation would be fantastic) and is this an es6 thing? A webpack thing? A vue-loader thing?</p>

<h1>UPDATE</h1>

<p>Thanks Felix Kling for pointing me to another duplicate stackoverflow question/answer about this same question.</p>

<p>While the comment on the other stackoverflow post isn't the exact answer to this question (it wasn't a babel plugin in my case) it did point me in the correct direction to find what it was. </p>

<p>In in the scaffolding that vue-cli cranks out for you, part of the base webpack config sets up an alias for .vue files:</p>

<p><a href="https://i.stack.imgur.com/Nz1TS.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/Nz1TS.png" alt="Alias location within project" /></div></a></p>

<p>This makes sense both in the fact that it gives you a relative path from the src file <em>and</em> it removes the requirement of the <code>.vue</code> at the end of the import path (which you normally need). </p>

<p>Thanks for the help!</p>
    
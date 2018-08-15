<a href="https://adrianmejia.com/blog/2018/08/04/vue-js-tutorial-for-beginners-create-a-todo-app/#.W3NVkKA68SE.hackernews">https://adrianmejia.com/blog/2018/08/04/vue-js-tutorial-for-beginners-create-a-todo-app/#.W3NVkKA68SE.hackernews</a><div id="articleHeader"><h1>Vue.js Tutorial for beginners</h1></div>
        <p>In this tutorial, you are going to learn the basics of Vue.js. While we learn, we are going to build a Todo app that will help us to put in practice what we learn.</p>

<p>A good way to learn a new framework, It’s by doing a Todo app. It’s an excellent way to compare framework features. It’s quick to implement and easy to understand. However, don’t be fooled by the simplicity, we are going to take it to the next level. We are going to explore advanced topics as well such as Vue Routing, Components, directives and many more!</p>
<p>Let’s first setup the dev environment, so we can focus on Vue! 🖖</p>
<h1 id="Setup">Setup</h1><p>We are going to start with essential HTML elements and CSS files and no JavaScript. You will learn how to add all the JavaScript functionality using Vue.js.</p>
<p>To get started quickly, clone the following repo and check out the <code>start-here</code> branch:</p>
<figure><table><tbody><tr><td></td><td><pre><div>git clone https://github.com/amejiarosario/vue-todo-app.git</div><div>cd vue-todo-app</div><div>git checkout start-here</div><div>npm install</div><div>npm start</div></pre></td></tr></tbody></table></figure>
<p>After running <code>npm start</code>, your browser should open on port <code>http://127.0.0.1:8080</code> and show the todo app.</p>
<p><div class="readableLargeImageContainer"><img src="/images/todo-app.jpg" alt="todo-app" /></div></p>
<p>Try to interact with it. You cannot create a new Todos, nor can you delete them or edit them. We are going to implement that!</p>
<p>Open your favorite code editor (I recommend <a href="https://code.visualstudio.com/" target="_blank">Code</a>) on <code>vue-todo-app</code> directory.</p>
<h2 id="Package-json">Package.json</h2><p>Take a look at the <code>package.json</code> dependencies:</p>
<figure><figcaption>app.js</figcaption><table><tbody><tr><td></td><td><pre><div>"dependencies": {</div><div>  "todomvc-app-css": "2.1.2",</div><div>  "vue": "2.5.17",</div><div>  "vue-router": "3.0.1"</div><div>"devDependencies": {</div><div>  "live-server": "1.2.0"</div></pre></td></tr></tbody></table></figure>
<p>We installed <code>Vue</code> and <code>VueRouter</code> dependencies. Also, we have the nice CSS library for Todo apps and <code>live-server</code> to serve and reload the page when we make changes. That’s all we would need for this tutorial.</p>
<h2 id="index-html">index.html</h2><p>Open the <code>index.html</code> file.  There we have the basic HTML structure for the Todo app that we are going to build upon:</p>
<ul>
<li>Line 9: Loads the CSS from NPM module <code>node_modules/todomvc-app-css/index.css</code>.</li>
<li>Line 23: We have the <code>ul</code> and some hard-coded todo lists. We are going to change this in a bit.</li>
<li>Line 73: we have multiple script files that load Vue, VueRouter and an empty <code>app.js</code>.</li>
</ul>
<p>Now, you know the basic structure where we are going to work on. Let’s get started with Vue! 🖖</p>
<h1 id="Getting-started-with-Vue">Getting started with Vue</h1><p>As you might know…</p>
<blockquote>
<p>Vue.js is a <em>reactive</em> JavaScript framework to build UI components.</p>
</blockquote>
<p>It’s reactive because the data and the DOM are linked. That means, that when data changes, it automatically updates the DOM. Let’s try that!</p>
<h2 id="Vue-Data-amp-v-text">Vue Data & v-text</h2><p>Go to <code>app.js</code> and type the following:</p>
<figure><figcaption>app.js</figcaption><table><tbody><tr><td></td><td><pre><div>const todoApp = new Vue({</div><div>  el: '.todoapp',</div><div>  data: {</div><div>    title: 'Hello Vue!'</div></pre></td></tr></tbody></table></figure>
<p>The <code>el</code> is the element where Vue is going to be mounted. If you notice in the <code>index.html</code> that’s the section part. The <code>data</code> object is reactive. It keeps track of changes and re-render the DOM if needed. Go to the index page and change <code>&lt;h1&gt;todos&lt;/h1&gt;</code> for <code>&lt;h1&gt;{{ title }}&lt;/h1&gt;</code>. The rest remains the same:</p>
<figure><figcaption>index.html</figcaption><table><tbody><tr><td></td><td><pre><div>&lt;section class="todoapp"&gt;</div><div>  &lt;header class="header"&gt;</div><div>    &lt;h1&gt;{{ title }}&lt;/h1&gt;</div><div>    &lt;input class="new-todo" placeholder="What needs to be done?" autofocus&gt;</div><div>  &lt;/header&gt;</div><div>  &lt;!--  ...  --&gt;</div></pre></td></tr></tbody></table></figure>
<p>If you have <code>npm start</code> running you will see that the title changed!</p>
<p>You can also go to the console and change it <code>todoApp.title = "Bucket List"</code> and see that it updates the DOM.</p>
<p><div class="readableLargeImageContainer"><img src="/images/vue-reactive.gif" alt="vue" /></div></p>
<p>Note: besides the curly braces you can also use <code>v-text</code>:</p>
<figure><figcaption>index.html</figcaption><table><tbody><tr><td></td><td><pre><div>&lt;h1 v-text="title"&gt;&lt;/h1&gt;</div></pre></td></tr></tbody></table></figure>
<p>Let’s do something useful and put an initial todo list:</p>
<figure><figcaption>app.js</figcaption><table><tbody><tr><td></td><td><pre><div>const todoApp = new Vue({</div><div>  el: '.todoapp',</div><div>  data: {</div><div>    title: 'Todos',</div><div>    todos: [</div><div>      { text: 'Learn JavaScript ES6+ goodies', isDone: true },</div><div>      { text: 'Learn Vue', isDone: false },</div><div>      { text: 'Build something awesome', isDone: false },</div></pre></td></tr></tbody></table></figure>
<p>Now that we have the list we need to replace the <code>&lt;li&gt;</code> elements with each of the elements in the <code>data.todos</code> array.</p>
<p>Let’s do the CRUD (Create-Read-Update-Delete) of a Todo application.</p>
<p><a href="https://github.com/amejiarosario/vue-todo-app/commit/2d1f2e5" target="_blank">review diff</a></p>
<h2 id="READ-List-rendering-with-v-for">READ: List rendering with <code>v-for</code></h2><p>As you can see everything starting with <code>v-</code> is defined by the Vue library.</p>
<p>We can iterate through elements using <code>v-for</code> as follows:</p>
<figure><figcaption>index.html</figcaption><table><tbody><tr><td></td><td><pre><div>&lt;li v-for="todo in todos"&gt;</div><div>  &lt;div class="view"&gt;</div><div>    &lt;input class="toggle" type="checkbox"&gt;</div><div>    &lt;label&gt;{{todo.text}}&lt;/label&gt;</div><div>    &lt;button class="destroy"&gt;&lt;/button&gt;</div><div>  &lt;/div&gt;</div><div>  &lt;input class="edit" value="Rule the web"&gt;</div><div>&lt;/li&gt;</div></pre></td></tr></tbody></table></figure>
<p>You can remove the other <code>&lt;li&gt;</code> tag that was just a placeholder.</p>
<p><a href="https://github.com/amejiarosario/vue-todo-app/commit/3dc4871" target="_blank">review diff</a></p>
<h2 id="CREATE-Todo-and-event-directives">CREATE Todo and event directives</h2><p>We are going to implement the create functionality. We have a textbox, and when we press enter, we would like to add whatever we typed to the list.</p>
<p>In Vue, we can listen to an event using <code>v-on:EVENT_NAME</code>. E.g.:</p>
<ul>
<li>v-on:click</li>
<li>v-on:dbclick</li>
<li>v-on:keyup</li>
<li>v-on:keyup.enter</li>
</ul>
<p><strong>Protip</strong>: since <code>v-on:</code> is used a lot, there’s a shortcut <code>@</code>. E.g. Instead of <code>v-on:keyup.enter</code> it can be <code>@keyup.enter</code>.</p>
<p>Let’s use the <code>keyup.enter</code> to create a todo:</p>
<figure><figcaption>index.html</figcaption><table><tbody><tr><td></td><td><pre><div>&lt;input class="new-todo" placeholder="What needs to be done?"</div><div>  v-on:keyup.enter="createTodo"</div><div>  autofocus&gt;</div></pre></td></tr></tbody></table></figure>
<p>On <code>enter</code> we are calling <code>createTodo</code> method, but it’s not defined yet. Let’s define it on <code>app.js</code> as follows:</p>
<figure><figcaption>app.js</figcaption><table><tbody><tr><td></td><td><pre><div>methods: {</div><div>  createTodo(event) {</div><div>    const textbox = event.target;</div><div>    this.todos.push({ text: textbox.value, isDone: false });</div><div>    textbox.value = '';</div></pre></td></tr></tbody></table></figure>
<p><a href="https://github.com/amejiarosario/vue-todo-app/commit/fcd305c" target="_blank">review diff</a></p>
<h2 id="Applying-classes-dynamically-amp-Vue-v-bind">Applying classes dynamically & Vue <code>v-bind</code></h2><p>If you click the checkbox (or checkcirlcle) we would like the class <code>completed</code> to be applied to the element. We can accomplish this by using the <code>v-bind</code> directive.</p>
<p><code>v-bind</code> can be applied to any HTML attribute such as <code>class</code>, <code>title</code> and so forth. Since <code>v-bind</code> is used a lot we can have a shortcut <code>:</code>, so instead of <code>v-bind:class</code> it becomes <code>:class</code>.</p>
<figure><figcaption>index.html</figcaption><table><tbody><tr><td></td><td><pre><div>&lt;li v-for="todo in todos" :class="{ completed: todo.isDone }"&gt;</div></pre></td></tr></tbody></table></figure>
<p>Now if a Todo list is completed, it will become cross out. However, if we click on the checkbox, it doesn’t update the <code>isDone</code> property.  Let’s fix that next.</p>
<p><a href="https://github.com/amejiarosario/vue-todo-app/commit/2145c36" target="_blank">review diff</a></p>
<h2 id="Keep-DOM-and-data-in-sync-with-Vue-v-model">Keep DOM and data in sync with Vue v-model</h2><p>The todos have a property called <code>isDone</code> if it’s true we want the checkbox to be marked. That’s data -&gt; DOM. We also want if we change the DOM (click the checkbox) we want to update the data (DOM -&gt; data). This bi-directional communication is easy to do using <code>v-model</code>, it will keep it in sync for you!</p>
<figure><table><tbody><tr><td></td><td><pre><div>&lt;input class="toggle" type="checkbox" v-model="todo.isDone"&gt;</div></pre></td></tr></tbody></table></figure>
<p>If you test the app now, you can see when you click the checkbox; also the text gets cross out. Yay!</p>
<p>You can also go to the console and verify that if you change the data directly, it will immediately update the HTML. Type the following in the browser console where you todo app is running:</p>
<figure><table><tbody><tr><td></td><td><pre><div>todoApp.todos[2].isDone = true</div></pre></td></tr></tbody></table></figure>
<p>You should see the update. Cool!</p>
<h2 id="UPDATE-todo-list-with-a-double-click">UPDATE todo list with a double-click</h2><p>We want to double click on any list and that it automatically becomes a checkbox. We have some CSS magic to do that, the only thing we need to do is to apply the <code>editing</code> class.</p>
<figure><figcaption>index.html</figcaption><table><tbody><tr><td></td><td><pre><div>&lt;!-- List items should get the class `editing` when editing and `completed` when marked as completed --&gt;</div><div>&lt;li v-for="todo in todos" :class="{ completed: todo.isDone }"&gt;</div><div>  &lt;div class="view"&gt;</div><div>    &lt;input class="toggle" type="checkbox" v-model="todo.isDone"&gt;</div><div>    &lt;label&gt;{{todo.text}}&lt;/label&gt;</div><div>    &lt;button class="destroy"&gt;&lt;/button&gt;</div><div>  &lt;/div&gt;</div><div>  &lt;input class="edit" value="Rule the web"&gt;</div><div>&lt;/li&gt;</div></pre></td></tr></tbody></table></figure>
<p>Similar to what we did with the <code>completed</code> class, we need to add a condition when we start editing.</p>
<p>Starting with the label, we want to start editing when we double-click on it. Vue provides <code>v-on:dblclick</code> or shorthand <code>@dblclick</code>:</p>
<figure><table><tbody><tr><td></td><td><pre><div>&lt;label @dblclick="startEditing(todo)"&gt;{{todo.text}}&lt;/label&gt;</div></pre></td></tr></tbody></table></figure>
<p>In the <code>app.js</code> we can define start editing as follows:</p>
<figure><figcaption>app.js</figcaption><table><tbody><tr><td></td><td><pre><div>const todoApp = new Vue({</div><div>  el: '.todoapp',</div><div>  data: {</div><div>    title: 'Todos',</div><div>    todos: [</div><div>      { text: 'Learn JavaScript ES6+ goodies', isDone: true },</div><div>      { text: 'Learn Vue', isDone: false },</div><div>      { text: 'Build something awesome', isDone: false },</div><div>    editing: null,</div><div>  methods: {</div><div>    createTodo(event) {</div><div>      const textbox = event.target;</div><div>      this.todos.push({ text: textbox.value, isDone: false });</div><div>      textbox.value = '';</div><div>    startEditing(todo) {</div><div>      this.editing = todo;</div></pre></td></tr></tbody></table></figure>
<p>We created a new variable <code>editing</code> in data. We just set whatever todo we are currently editing. We want only to edit one at a time, so this works perfectly. When you double-click the label, the <code>startEditing</code> function is called and set the <code>editing</code> variable to the current todo element.</p>
<p>Next, we need to apply the <code>editing</code> class:</p>
<figure><table><tbody><tr><td></td><td><pre><div>&lt;li v-for="todo in todos" :class="{ completed: todo.isDone, editing: todo === editing }"&gt;</div></pre></td></tr></tbody></table></figure>
<p>When <code>data.editing</code> matches the <code>todo</code> , then we apply the CSS class. Try it out!</p>
<p>If you try it out, you will notice you can enter on edit mode, but there’s no way to exit from it (yet). Let’s fix that.</p>
<figure><table><tbody><tr><td></td><td><pre><div>&lt;input class="edit"</div><div>  @keyup.esc="cancelEditing"</div><div>  @keyup.enter="finishEditing"</div><div>  @blur="finishEditing"</div><div>  :value="todo.text"&gt;</div></pre></td></tr></tbody></table></figure>
<p>First, we want the input textbox to have the <code>value</code> of the <code>todo.text</code> when we enter to the editing mode. We can accomplish this using <code>:value="todo.text"</code>. Remember that colon <code>:</code> is a shorthand for <code>v-bind</code>.</p>
<p>Before, we implemented the <code>startEditing</code> function. Now, we need to complete the edit functionality with these two more methods:</p>
<ul>
<li><code>finishEditing</code>: applies changes to the <code>todo.text</code>. This is triggered by pressing <kbd>enter</kbd> or clicking elsewhere (blur).</li>
<li><code>cancelEditing</code>: discard the changes and leave <code>todos</code> list untouched. This happens when you press the <kbd>esc</kbd> key.</li>
</ul>
<p>Let’s go to the <code>app.js</code> and define these two functions.</p>
<figure><figcaption>app.js</figcaption><table><tbody><tr><td></td><td><pre><div>finishEditing(event) {</div><div>  if (!this.editing) { return; }</div><div>  const textbox = event.target;</div><div>  this.editing.text = textbox.value;</div><div>  this.editing = null;</div><div>cancelEditing() {</div><div>  this.editing = null;</div></pre></td></tr></tbody></table></figure>
<p>Cancel is pretty straightforward. It just set editing to null.</p>
<p><code>finishEditing</code> will take the input current’s value (event.target.value) and copy over the todo element that is currently being edited. That’s it!</p>
<p><a href="https://github.com/amejiarosario/vue-todo-app/commit/4af7d31" target="_blank">review diff</a></p>
<h2 id="DELETE-todo-list-on-click-event">DELETE todo list on @click event</h2><p>Finally, the last step to complete the CRUD operations is deleting. We are going to listen for click events on the destroy icon:</p>
<figure><table><tbody><tr><td></td><td><pre><div>&lt;button class="destroy" @click="destroyTodo(todo)"&gt;&lt;/button&gt;</div></pre></td></tr></tbody></table></figure>
<p>also, <code>destroyTodo</code> implementation is as follows:</p>
<figure><figcaption>app.js</figcaption><table><tbody><tr><td></td><td><pre><div>destroyTodo(todo) {</div><div>  const index = this.todos.indexOf(todo);</div><div>  this.todos.splice(index, 1);</div></pre></td></tr></tbody></table></figure>
<p><a href="https://github.com/amejiarosario/vue-todo-app/commit/a73e058" target="_blank">review diff</a></p>
<h2 id="Trimming-inputs">Trimming inputs</h2><p>It’s always a good idea to <code>trim</code> user inputs, so any accidental whitespace doesn’t get in the way with <code>textbox.value.trim()</code>.</p>
<p><a href="https://github.com/amejiarosario/vue-todo-app/commit/45b4eed44abd9a4cfec3b3977b61fe7031ff6c4e" target="_blank">review diff</a></p>
<h2 id="Items-left-count-with-computed-properties">Items left count with  <code>computed</code> properties</h2><p>Right now the <code>item left</code> count is always 0. We want the number of remaining tasks.  We could do something like this:</p>
<figure><table><tbody><tr><td></td><td><pre><div>&lt;strong&gt;{{ todos.filter(t =&gt; !t.isDone).length }}&lt;/strong&gt; item(s) left&lt;/span&gt;</div></pre></td></tr></tbody></table></figure>
<p>That’s a little ugly to stick out all that logic into the template. That’s why Vue has the <code>computed</code>  section!</p>
<figure><figcaption>app.js</figcaption><table><tbody><tr><td></td><td><pre><div>computed: {</div><div>  activeTodos() {</div><div>    return this.todos.filter(t =&gt; !t.isDone);</div></pre></td></tr></tbody></table></figure>
<p>Now the template is cleaner:</p>
<figure><table><tbody><tr><td></td><td><pre><div>&lt;strong&gt;{{ activeTodos.length }}&lt;/strong&gt; item(s) left&lt;/span&gt;</div></pre></td></tr></tbody></table></figure>
<p>You might ask, why use a computed property when we can create a method instead?</p>
<blockquote>
<p>Computed vs. Methods. Computed properties are <strong>cached</strong> and updated when their dependencies changes. The computed property would return immediately without having to evaluate the function if no changes happened. On the other hand, Methods will <strong>always</strong> run the function.</p>
</blockquote>
<p>Try completing other tasks and verify that the count gets updated.</p>
<p><div class="readableLargeImageContainer"><img src="/images/items-left.gif" alt="items-left" /></div></p>
<p><a href="https://github.com/amejiarosario/vue-todo-app/commit/24ae5a0f74c226325d88a2aaecad9e40b35760fb" target="_blank">review diff</a></p>
<h2 id="Clearing-completed-tasks-amp-conditional-rendering-with-v-show">Clearing completed tasks & conditional rendering with <code>v-show</code></h2><p>We want to show <code>clear completed</code> button only if there are any completed task. We can accomplish this with the <code>v-show</code> directive:</p>
<figure><table><tbody><tr><td></td><td><pre><div>&lt;button class="clear-completed" @click="clearCompleted" v-show="completedTodos.length"&gt;Clear completed&lt;/button&gt;</div></pre></td></tr></tbody></table></figure>
<p>The v-show will hide the element if the expression evaluates to false or 0.</p>
<p>One way to clearing out completed tasks is by assigning the <code>activeTodos</code> property to the <code>todos</code>:</p>
<figure><figcaption>app.js</figcaption><table><tbody><tr><td></td><td><pre><div>clearCompleted() {</div><div>  this.todos = this.activeTodos;</div></pre></td></tr></tbody></table></figure>
<p>Also, we have to add the computed property <code>completedTodos</code> that we use in the v-show</p>
<figure><table><tbody><tr><td></td><td><pre><div>completedTodos() {</div><div>  return this.todos.filter(t =&gt; t.isDone);</div></pre></td></tr></tbody></table></figure>
<p><a href="https://github.com/amejiarosario/vue-todo-app/commit/dd7dd90" target="_blank">review diff</a></p>
<h1 id="Vue-Conditional-Rendering-v-show-vs-v-if">Vue Conditional Rendering: <code>v-show</code> vs <code>v-if</code></h1><p><code>v-show</code> and <code>v-if</code> looks very similar, but they work differently. <code>v-if</code> removes the element from the DOM and disable events, while <code>v-show</code> hides it with the CSS <code>display: none;</code>. So, <code>v-if</code> is more expensive than <code>v-show</code>.</p>
<blockquote>
<p>If you foresee the element being toggling visibility very often then you should use <code>v-show</code>. If not, then use <code>v-if</code>.</p>
</blockquote>
<p>We can hide the footer and central section if there’s no todo list.</p>
<figure><table><tbody><tr><td></td><td><pre><div>&lt;section class="main" v-if="todos.length"&gt;... &lt;/section&gt;</div><div>&lt;footer class="footer" v-if="todos.length"&gt;...&lt;/footer&gt;</div></pre></td></tr></tbody></table></figure>
<p><a href="https://github.com/amejiarosario/vue-todo-app/commit/790b241" target="_blank">review diff</a></p>
<h1 id="Local-Storage">Local Storage</h1><p>On every refresh, our list gets reset. This is useful for dev but not for users. Let’s persist our Todos in the local storage.</p>
<blockquote>
<p>Local storage vs. Session storage. <strong>Session</strong> data goes away when you close the window or expire after a specific time. <strong>Local storage</strong> doesn’t have an expiration time.</p>
</blockquote>
<p>The way <code>localStorage</code> works is straightforward. It is global variable and has only 4 methods:</p>
<ul>
<li><code>localStorage.setItem(key, value)</code>: key/value storage. <code>key</code> and <code>value</code> are coerced into a string.</li>
<li><code>localStorage.getItem(key)</code>: get the item by key.</li>
<li><code>localStorage.removeItem(key)</code>: remove item matching the key.</li>
<li><code>localStorage.clear()</code>: clear all items for the current hostname.</li>
</ul>
<p>We are going to use <code>getItem</code> and <code>setItem</code>. First we need to define a storage key:</p>
<figure><figcaption>app.js</figcaption><table><tbody><tr><td></td><td><pre><div>const LOCAL_STORAGE_KEY = 'todo-app-vue';</div></pre></td></tr></tbody></table></figure>
<p>Then we replace <code>data.todos</code> to get items (if any) from the local storage:</p>
<figure><figcaption>app.js</figcaption><table><tbody><tr><td></td><td><pre><div>data: {</div><div>  title: 'Todos',</div><div>  todos: JSON.parse(localStorage.getItem(LOCAL_STORAGE_KEY)) || [</div><div>    { text: 'Learn JavaScript ES6+ goodies', isDone: true },</div><div>    { text: 'Learn Vue', isDone: false },</div><div>    { text: 'Build something awesome', isDone: false },</div><div>  editing: null,</div></pre></td></tr></tbody></table></figure>
<p>We have to use <code>JSON.parse</code> because everything gets stored as a string and we need to convert it to an object.</p>
<p><code>getItem</code> will retrieve the saved todos from the <code>localstorage</code>. However, we are saying it yet. Let’s see how we can do that.</p>
<h1 id="Vue-Watchers">Vue Watchers</h1><p>For saving, we are going to use the Vue watchers.</p>
<blockquote>
<p>Vue watchers vs. Computed properties. Computed properties are usually used to “compute” and cache the value of 2 or more properties. Watchers are more low level than computed properties. Watchers allow you to “watch” for changes on a single property. This is useful for performing expensive operations like saving to DB, API calls and so on.</p>
</blockquote>
<figure><table><tbody><tr><td></td><td><pre><div>watch: {</div><div>  todos: {</div><div>    deep: true,</div><div>    handler(newValue) {</div><div>      localStorage.setItem(LOCAL_STORAGE_KEY, JSON.stringify(newValue));</div></pre></td></tr></tbody></table></figure>
<p>This expression watches for changes in our <code>todos</code> data. Deep means that it recursively watches for changes in the values inside arrays and objects. If there’s a change, we save them to the local storage.</p>
<p><a href="https://github.com/amejiarosario/vue-todo-app/commit/579da19" target="_blank">review diff</a></p>
<p>Once you change some todos, you will see they are stored in the local storage. You can access them using the browser’s dev tools:</p>
<p><div class="readableLargeImageContainer"><img src="/images/local-storage-devtools.jpg" alt="local storage" /></div></p>
<p>The last part to implement is the routing! However, for that, we need to explain some more concepts and will do that in the next post.</p>
<hr />
<p>In the next tutorial, we are going to switch gears a little bit and go deeper into Vue Components, Routing, and Local Storage. Stay tuned!</p>
<h1 id="Summary-Vue-cheatsheet">Summary: Vue cheatsheet</h1><p>We learned a lot! Here is a summary:</p>
<div>
  <table>
    <caption>Binders</caption>
    <thead>
      <tr><th>Name</th>
      <th>Description</th>
      <th>Examples</th>
    </tr></thead>

    <tbody>
      <tr>
        <td> v-bind </td>
        <td>Bind to HTML attribute</td>
        <td>
          <code>&lt;span v-bind:title="tooltip"&gt;&lt;/span&gt;</code>
        </td>
      </tr>

      <tr>
        <td> :</td>
        <td>Shortcut for v-bind</td>
        <td>
          <code>&lt;span :title="tooltip"&gt;&lt;/span&gt;</code>
          <code>&lt;li v-bind:class="{completed: todo.isDone }"&gt;&lt;/li&gt;</code>
        </td>
      </tr>

      <tr>
        <td> v-text </td>
        <td>Inject text into the element</td>
        <td>
          <code>&lt;h1 v-text="title"&gt;&lt;/h1&gt;</code>
        </td>
      </tr>

      <tr>
        <td> v-html </td>
        <td>Inject raw HTML into the element</td>
        <td>
          <code>&lt;blog-post v-html="content"&gt;&lt;/blog-post&gt;</code>
        </td>
      </tr>

    </tbody>
  </table>
</div>

<div>
  <table>
    <caption>Iterators</caption>
    <thead>
      <tr><th>Name</th>
      <th>Description</th>
      <th>Examples</th>
    </tr></thead>

    <tbody>
      <tr>
        <td> v-for </td>
        <td>Iterate over elements</td>
        <td>
          <code>&lt;li v-for="todo in todos"&gt;&lt;/li&gt;</code>
        </td>
      </tr>

    </tbody>
  </table>
</div>

<div>
  <table>
    <caption>Events</caption>
    <thead>
      <tr><th>Name</th>
      <th>Description</th>
      <th>Examples</th>
    </tr></thead>

    <tbody>
      <tr>
        <td> v-on:click </td>
        <td>Invoke callback on click</td>
        <td>
          <code>&lt;button class="destroy" v-on:click="destroyTodo(todo)"&gt;&lt;/button&gt;</code>
        </td>
      </tr>

      <tr>
        <td> @ </td>
        <td><code>@</code> is shorcut for <code>v-on:</code></td>
        <td>
          <code>&lt;input class="edit"
              @keyup.esc="cancelEditing"
              @keyup.enter="finishEditing"
              @blur="finishEditing"&gt;</code>
        </td>
      </tr>

      <tr>
        <td> v-on:dblclick </td>
        <td>Invoke callback on double-click</td>
        <td>
          <code>&lt;label @dblclick="startEditing(todo)"&gt;&lt;/label&gt;</code>
        </td>
      </tr>

      <tr>
        <td> @keyup.enter </td>
        <td>Invoke callback on keyup <kbd>enter</kbd></td>
        <td>
          <code>&lt;input @keyup.enter="createTodo"&gt;</code>
        </td>
      </tr>

      <tr>
        <td> @keyup.esc </td>
        <td>Invoke callback on keyup <kbd>esc</kbd></td>
        <td>
          <code>&lt;input @keyup.esc="cancelEditing"&gt;</code>
        </td>
      </tr>

    </tbody>
  </table>
</div>

<div>
  <table>
    <caption>Conditional Rendering</caption>
    <thead>
      <tr><th>Name</th>
      <th>Description</th>
      <th>Examples</th>
    </tr></thead>

    <tbody>
      <tr>
        <td> v-show </td>
        <td>Show or hide the element if the expression evaluates to truthy</td>
        <td>
          <code>&lt;button v-show="completedTodos.length"&gt;Clear completed&lt;/button&gt;</code>
        </td>
      </tr>

      <tr>
        <td> v-if </td>
        <td>Remove or add the element if the expression evaluates to truthy</td>
        <td>
          <code>&lt;footer v-if="todos.length"&gt;...&lt;/footer&gt;</code>
        </td>
      </tr>

    </tbody>
  </table>
</div>

<div>
  <table>
    <caption>Automatic Data&lt;-&gt;DOM Sync</caption>
    <thead>
      <tr><th>Name</th>
      <th>Description</th>
      <th>Examples</th>
    </tr></thead>

    <tbody>
      <tr>
        <td> v-model </td>
        <td>Keep data and DOM in sync automatially</td>
        <td>
          <code>&lt;input class="toggle" type="checkbox" v-model="todo.isDone"&gt;</code>
        </td>
      </tr>

    </tbody>
  </table>
</div>

<div>
  <table>
    <caption>Vue instance</caption>
    <thead>
      <tr><th>Examples</th>
    </tr></thead>

    <tbody>
      <tr>
        <td>

<figure><table><tbody><tr><td></td><td><pre><div>const todoApp = new Vue({</div><div>  // element matcher</div><div>  el: '.todoapp',</div><div>  // data available on the templates</div><div>  data: {</div><div>    title: 'Todos',</div><div>    editing: null,</div><div>  // invoke this functions on event handlers, etc.</div><div>  methods: {</div><div>    createTodo(event) {</div><div>      const textbox = event.target;</div><div>      this.todos.push({ text: textbox.value.trim(), isDone: false });</div><div>      textbox.value = '';</div><div>  // cached methods (only get invokes when data changes)</div><div>  computed: {</div><div>    activeTodos() {</div><div>      return this.todos.filter(t =&gt; !t.isDone);</div><div>  // watch for changes on the data</div><div>  watch: {</div><div>    todos: {</div><div>      deep: true,</div><div>      handler(newValue, oldValue) {</div><div>        localStorage.setItem(LOCAL_STORAGE_KEY, JSON.stringify(newValue));</div></pre></td></tr></tbody></table></figure>

        </td>
      </tr>

    </tbody>
  </table>
</div>

      
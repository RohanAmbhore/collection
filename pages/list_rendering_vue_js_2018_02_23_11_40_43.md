<a href="https://vuejs.org/v2/guide/list.html#Caveats">https://vuejs.org/v2/guide/list.html#Caveats</a><div id="articleHeader"><h1>List Rendering</h1></div>
  
  
    <h2 id="Mapping-an-Array-to-Elements-with-v-for"><a href="#Mapping-an-Array-to-Elements-with-v-for" title="Mapping an Array to Elements with v-for" target="_blank">Mapping an Array to Elements with <code>v-for</code></a></h2><p>We can use the <code>v-for</code> directive to render a list of items based on an array. The <code>v-for</code> directive requires a special syntax in the form of <code>item in items</code>, where <code>items</code> is the source data array and <code>item</code> is an <strong>alias</strong> for the array element being iterated on:</p>
<figure><table><tbody><tr><td><pre>&lt;ul id="example-1"&gt;<br />  &lt;li v-for="item in items"&gt;<br />    {{ item.message }}<br />  &lt;/li&gt;<br />&lt;/ul&gt;<br /></pre></td></tr></tbody></table></figure>
<figure><table><tbody><tr><td><pre>var example1 = new Vue({<br />  el: '#example-1',<br />  data: {<br />    items: [<br />      { message: 'Foo' },<br />      { message: 'Bar' }<br />    ]<br />  }<br />})<br /></pre></td></tr></tbody></table></figure>
<p>Result:</p>




<p>Inside <code>v-for</code> blocks we have full access to parent scope properties. <code>v-for</code> also supports an optional second argument for the index of the current item.</p>
<figure><table><tbody><tr><td><pre>&lt;ul id="example-2"&gt;<br />  &lt;li v-for="(item, index) in items"&gt;<br />    {{ parentMessage }} - {{ index }} - {{ item.message }}<br />  &lt;/li&gt;<br />&lt;/ul&gt;<br /></pre></td></tr></tbody></table></figure>
<figure><table><tbody><tr><td><pre>var example2 = new Vue({<br />  el: '#example-2',<br />  data: {<br />    parentMessage: 'Parent',<br />    items: [<br />      { message: 'Foo' },<br />      { message: 'Bar' }<br />    ]<br />  }<br />})<br /></pre></td></tr></tbody></table></figure>
<p>Result:</p>

<ul id="example-2"><li>
    Parent - 0 - Foo
  </li><li>
    Parent - 1 - Bar
  </li></ul>


<p>You can also use <code>of</code> as the delimiter instead of <code>in</code>, so that it is closer to JavaScript’s syntax for iterators:</p>
<figure><table><tbody><tr><td><pre>&lt;div v-for="item of items"&gt;&lt;/div&gt;<br /></pre></td></tr></tbody></table></figure>
<h2 id="v-for-with-an-Object"><a href="#v-for-with-an-Object" title="v-for with an Object" target="_blank"><code>v-for</code> with an Object</a></h2><p>You can also use <code>v-for</code> to iterate through the properties of an object.</p>
<figure><table><tbody><tr><td><pre>&lt;ul id="v-for-object" class="demo"&gt;<br />  &lt;li v-for="value in object"&gt;<br />    {{ value }}<br />  &lt;/li&gt;<br />&lt;/ul&gt;<br /></pre></td></tr></tbody></table></figure>
<figure><table><tbody><tr><td><pre>new Vue({<br />  el: '#v-for-object',<br />  data: {<br />    object: {<br />      firstName: 'John',<br />      lastName: 'Doe',<br />      age: 30<br />    }<br />  }<br />})<br /></pre></td></tr></tbody></table></figure>
<p>Result:</p>




<p>You can also provide a second argument for the key:</p>
<figure><table><tbody><tr><td><pre>&lt;div v-for="(value, key) in object"&gt;<br />  {{ key }}: {{ value }}<br />&lt;/div&gt;<br /></pre></td></tr></tbody></table></figure>

<div id="v-for-object-value-key"><div>
    firstName: John
  </div><div>
    lastName: Doe
  </div><div>
    age: 30
  </div>


<p>And another for the index:</p>
<figure><table><tbody><tr><td><pre>&lt;div v-for="(value, key, index) in object"&gt;<br />  {{ index }}. {{ key }}: {{ value }}<br />&lt;/div&gt;<br /></pre></td></tr></tbody></table></figure>

<div id="v-for-object-value-key-index"><div>
    0. firstName: John
  </div><div>
    1. lastName: Doe
  </div><div>
    2. age: 30
  </div>


<p>When iterating over an object, the order is based on the key enumeration order of <code>Object.keys()</code>, which is <strong>not</strong> guaranteed to be consistent across JavaScript engine implementations.</p>

<h2 id="key"><a href="#key" title="key" target="_blank"><code>key</code></a></h2><p>When Vue is updating a list of elements rendered with <code>v-for</code>, by default it uses an “in-place patch” strategy. If the order of the data items has changed, instead of moving the DOM elements to match the order of the items, Vue will patch each element in-place and make sure it reflects what should be rendered at that particular index. This is similar to the behavior of <code>track-by="$index"</code> in Vue 1.x.</p>
<p>This default mode is efficient, but only suitable <strong>when your list render output does not rely on child component state or temporary DOM state (e.g. form input values)</strong>.</p>
<p>To give Vue a hint so that it can track each node’s identity, and thus reuse and reorder existing elements, you need to provide a unique <code>key</code> attribute for each item. An ideal value for <code>key</code> would be the unique id of each item. This special attribute is a rough equivalent to <code>track-by</code> in 1.x, but it works like an attribute, so you need to use <code>v-bind</code> to bind it to dynamic values (using shorthand here):</p>
<figure><table><tbody><tr><td><pre>&lt;div v-for="item in items" :key="item.id"&gt;<br />  &lt;!-- content --&gt;<br />&lt;/div&gt;<br /></pre></td></tr></tbody></table></figure>
<p>It is recommended to provide a <code>key</code> with <code>v-for</code> whenever possible, unless the iterated DOM content is simple, or you are intentionally relying on the default behavior for performance gains.</p>
<p>Since it’s a generic mechanism for Vue to identify nodes, the <code>key</code> also has other uses that are not specifically tied to <code>v-for</code>, as we will see later in the guide.</p>
<h2 id="Array-Change-Detection"><a href="#Array-Change-Detection" title="Array Change Detection" target="_blank">Array Change Detection</a></h2><h3 id="Mutation-Methods"><a href="#Mutation-Methods" title="Mutation Methods" target="_blank">Mutation Methods</a></h3><p>Vue wraps an observed array’s mutation methods so they will also trigger view updates. The wrapped methods are:</p>
<ul>
<li><code>push()</code></li>
<li><code>pop()</code></li>
<li><code>shift()</code></li>
<li><code>unshift()</code></li>
<li><code>splice()</code></li>
<li><code>sort()</code></li>
<li><code>reverse()</code></li>
</ul>
<p>You can open the console and play with the previous examples’ <code>items</code> array by calling their mutation methods. For example: <code>example1.items.push({ message: 'Baz' })</code>.</p>
<h3 id="Replacing-an-Array"><a href="#Replacing-an-Array" title="Replacing an Array" target="_blank">Replacing an Array</a></h3><p>Mutation methods, as the name suggests, mutate the original array they are called on. In comparison, there are also non-mutating methods, e.g. <code>filter()</code>, <code>concat()</code> and <code>slice()</code>, which do not mutate the original array but <strong>always return a new array</strong>. When working with non-mutating methods, you can replace the old array with the new one:</p>
<figure><table><tbody><tr><td><pre>example1.items = example1.items.filter(function (item) {<br />  return item.message.match(/Foo/)<br />})<br /></pre></td></tr></tbody></table></figure>
<p>You might think this will cause Vue to throw away the existing DOM and re-render the entire list - luckily, that is not the case. Vue implements some smart heuristics to maximize DOM element reuse, so replacing an array with another array containing overlapping objects is a very efficient operation.</p>
<h3 id="Caveats"><a href="#Caveats" title="Caveats" target="_blank">Caveats</a></h3><p>Due to limitations in JavaScript, Vue <strong>cannot</strong> detect the following changes to an array:</p>
<ol>
<li>When you directly set an item with the index, e.g. <code>vm.items[indexOfItem] = newValue</code></li>
<li>When you modify the length of the array, e.g. <code>vm.items.length = newLength</code></li>
</ol>
<p>To overcome caveat 1, both of the following will accomplish the same as <code>vm.items[indexOfItem] = newValue</code>, but will also trigger state updates in the reactivity system:</p>
<figure><table><tbody><tr><td><pre>// Vue.set<br />Vue.set(example1.items, indexOfItem, newValue)<br /></pre></td></tr></tbody></table></figure>
<figure><table><tbody><tr><td><pre>// Array.prototype.splice<br />example1.items.splice(indexOfItem, 1, newValue)<br /></pre></td></tr></tbody></table></figure>
<p>To deal with caveat 2, you can use <code>splice</code>:</p>
<figure><table><tbody><tr><td><pre>example1.items.splice(newLength)<br /></pre></td></tr></tbody></table></figure>
<h2 id="Object-Change-Detection-Caveats"><a href="#Object-Change-Detection-Caveats" title="Object Change Detection Caveats" target="_blank">Object Change Detection Caveats</a></h2><p>Again due to limitations of modern JavaScript, <strong>Vue cannot detect property addition or deletion</strong>. For example:</p>
<figure><table><tbody><tr><td><pre>var vm = new Vue({<br />  data: {<br />    a: 1<br />  }<br />})<br />// `vm.a` is now reactive<br /><br />vm.b = 2<br />// `vm.b` is NOT reactive<br /></pre></td></tr></tbody></table></figure>
<p>Vue does not allow dynamically adding new root-level reactive properties to an already created instance. However, it’s possible to add reactive properties to a nested object using the <code>Vue.set(object, key, value)</code> method. For example, given:</p>
<figure><table><tbody><tr><td><pre>var vm = new Vue({<br />  data: {<br />    userProfile: {<br />      name: 'Anika'<br />    }<br />  }<br />})<br /></pre></td></tr></tbody></table></figure>
<p>You could add a new <code>age</code> property to the nested <code>userProfile</code> object with:</p>
<figure><table><tbody><tr><td><pre>Vue.set(vm.userProfile, 'age', 27)<br /></pre></td></tr></tbody></table></figure>
<p>You can also use the <code>vm.$set</code> instance method, which is an alias for the global <code>Vue.set</code>:</p>
<figure><table><tbody><tr><td><pre>vm.$set(vm.userProfile, 'age', 27)<br /></pre></td></tr></tbody></table></figure>
<p>Sometimes you may want to assign a number of new properties to an existing object, for example using <code>Object.assign()</code> or <code>_.extend()</code>. In such cases, you should create a fresh object with properties from both objects. So instead of:</p>
<figure><table><tbody><tr><td><pre>Object.assign(vm.userProfile, {<br />  age: 27,<br />  favoriteColor: 'Vue Green'<br />})<br /></pre></td></tr></tbody></table></figure>
<p>You would add new, reactive properties with:</p>
<figure><table><tbody><tr><td><pre>vm.userProfile = Object.assign({}, vm.userProfile, {<br />  age: 27,<br />  favoriteColor: 'Vue Green'<br />})<br /></pre></td></tr></tbody></table></figure>
<h2 id="Displaying-Filtered-Sorted-Results"><a href="#Displaying-Filtered-Sorted-Results" title="Displaying Filtered/Sorted Results" target="_blank">Displaying Filtered/Sorted Results</a></h2><p>Sometimes we want to display a filtered or sorted version of an array without actually mutating or resetting the original data. In this case, you can create a computed property that returns the filtered or sorted array.</p>
<p>For example:</p>
<figure><table><tbody><tr><td><pre>&lt;li v-for="n in evenNumbers"&gt;{{ n }}&lt;/li&gt;<br /></pre></td></tr></tbody></table></figure>
<figure><table><tbody><tr><td><pre>data: {<br />  numbers: [ 1, 2, 3, 4, 5 ]<br />},<br />computed: {<br />  evenNumbers: function () {<br />    return this.numbers.filter(function (number) {<br />      return number % 2 === 0<br />    })<br />  }<br />}<br /></pre></td></tr></tbody></table></figure>
<p>In situations where computed properties are not feasible (e.g. inside nested <code>v-for</code> loops), you can use a method:</p>
<figure><table><tbody><tr><td><pre>&lt;li v-for="n in even(numbers)"&gt;{{ n }}&lt;/li&gt;<br /></pre></td></tr></tbody></table></figure>
<figure><table><tbody><tr><td><pre>data: {<br />  numbers: [ 1, 2, 3, 4, 5 ]<br />},<br />methods: {<br />  even: function (numbers) {<br />    return numbers.filter(function (number) {<br />      return number % 2 === 0<br />    })<br />  }<br />}<br /></pre></td></tr></tbody></table></figure>
<h2 id="v-for-with-a-Range"><a href="#v-for-with-a-Range" title="v-for with a Range" target="_blank"><code>v-for</code> with a Range</a></h2><p><code>v-for</code> can also take an integer. In this case it will repeat the template that many times.</p>
<figure><table><tbody><tr><td><pre>&lt;div&gt;<br />  &lt;span v-for="n in 10"&gt;{{ n }} &lt;/span&gt;<br />&lt;/div&gt;<br /></pre></td></tr></tbody></table></figure>
<p>Result:</p>

<div id="range">1 2 3 4 5 6 7 8 9 10 </div>


<h2 id="v-for-on-a-lt-template-gt"><a href="#v-for-on-a-lt-template-gt" title="v-for on a <template>" target="_blank"><code>v-for</code> on a <code>&lt;template&gt;</code></a></h2><p>Similar to template <code>v-if</code>, you can also use a <code>&lt;template&gt;</code> tag with <code>v-for</code> to render a block of multiple elements. For example:</p>
<figure><table><tbody><tr><td><pre>&lt;ul&gt;<br />  &lt;template v-for="item in items"&gt;<br />    &lt;li&gt;{{ item.msg }}&lt;/li&gt;<br />    &lt;li class="divider"&gt;&lt;/li&gt;<br />  &lt;/template&gt;<br />&lt;/ul&gt;<br /></pre></td></tr></tbody></table></figure>
<h2 id="v-for-with-v-if"><a href="#v-for-with-v-if" title="v-for with v-if" target="_blank"><code>v-for</code> with <code>v-if</code></a></h2><p>When they exist on the same node, <code>v-for</code> has a higher priority than <code>v-if</code>. That means the <code>v-if</code> will be run on each iteration of the loop separately. This can be useful when you want to render nodes for only <em>some</em> items, like below:</p>
<figure><table><tbody><tr><td><pre>&lt;li v-for="todo in todos" v-if="!todo.isComplete"&gt;<br />  {{ todo }}<br />&lt;/li&gt;<br /></pre></td></tr></tbody></table></figure>
<p>The above only renders the todos that are not complete.</p>
<p>If instead, your intent is to conditionally skip execution of the loop, you can place the <code>v-if</code> on a wrapper element (or <a href="conditional.html#Conditional-Groups-with-v-if-on-lt-template-gt" target="_blank"><code>&lt;template&gt;</code></a>). For example:</p>
<figure><table><tbody><tr><td><pre>&lt;ul v-if="todos.length"&gt;<br />  &lt;li v-for="todo in todos"&gt;<br />    {{ todo }}<br />  &lt;/li&gt;<br />&lt;/ul&gt;<br />&lt;p v-else&gt;No todos left!&lt;/p&gt;<br /></pre></td></tr></tbody></table></figure>
<h2 id="v-for-with-a-Component"><a href="#v-for-with-a-Component" title="v-for with a Component" target="_blank"><code>v-for</code> with a Component</a></h2><blockquote>
<p>This section assumes knowledge of <a href="components.html" target="_blank">Components</a>. Feel free to skip it and come back later.</p>
</blockquote>
<p>You can directly use <code>v-for</code> on a custom component, like any normal element:</p>
<figure><table><tbody><tr><td><pre>&lt;my-component v-for="item in items" :key="item.id"&gt;&lt;/my-component&gt;<br /></pre></td></tr></tbody></table></figure>
<blockquote>
<p>In 2.2.0+, when using <code>v-for</code> with a component, a <a href="list.html#key" target="_blank"><code>key</code></a> is now required.</p>
</blockquote>
<p>However, this won’t automatically pass any data to the component, because components have isolated scopes of their own. In order to pass the iterated data into the component, we should also use props:</p>
<figure><table><tbody><tr><td><pre>&lt;my-component<br />  v-for="(item, index) in items"<br />  v-bind:item="item"<br />  v-bind:index="index"<br />  v-bind:key="item.id"<br />&gt;&lt;/my-component&gt;<br /></pre></td></tr></tbody></table></figure>
<p>The reason for not automatically injecting <code>item</code> into the component is because that makes the component tightly coupled to how <code>v-for</code> works. Being explicit about where its data comes from makes the component reusable in other situations.</p>
<p>Here’s a complete example of a simple todo list:</p>
<figure><table><tbody><tr><td><pre>&lt;div id="todo-list-example"&gt;<br />  &lt;input<br />    v-model="newTodoText"<br />    v-on:keyup.enter="addNewTodo"<br />    placeholder="Add a todo"<br />  &gt;<br />  &lt;ul&gt;<br />    &lt;li<br />      is="todo-item"<br />      v-for="(todo, index) in todos"<br />      v-bind:key="todo.id"<br />      v-bind:title="todo.title"<br />      v-on:remove="todos.splice(index, 1)"<br />    &gt;&lt;/li&gt;<br />  &lt;/ul&gt;<br />&lt;/div&gt;<br /></pre></td></tr></tbody></table></figure>
<p>Note the <code>is="todo-item"</code> attribute. This is necessary in DOM templates, because only an <code>&lt;li&gt;</code> element is valid inside a <code>&lt;ul&gt;</code>. It does the same thing as <code>&lt;todo-item&gt;</code>, but works around a potential browser parsing error. See <a href="components.html#DOM-Template-Parsing-Caveats" target="_blank">DOM Template Parsing Caveats</a> to learn more.</p>

<figure><table><tbody><tr><td><pre>Vue.component('todo-item', {<br />  template: '\<br />    &lt;li&gt;\<br />      {{ title }}\<br />      &lt;button v-on:click="$emit(\'remove\')"&gt;X&lt;/button&gt;\<br />    &lt;/li&gt;\<br />  ',<br />  props: ['title']<br />})<br /><br />new Vue({<br />  el: '#todo-list-example',<br />  data: {<br />    newTodoText: '',<br />    todos: [<br />      {<br />        id: 1,<br />        title: 'Do the dishes',<br />      },<br />      {<br />        id: 2,<br />        title: 'Take out the trash',<br />      },<br />      {<br />        id: 3,<br />        title: 'Mow the lawn'<br />      }<br />    ],<br />    nextTodoId: 4<br />  },<br />  methods: {<br />    addNewTodo: function () {<br />      this.todos.push({<br />        id: this.nextTodoId++,<br />        title: this.newTodoText<br />      })<br />      this.newTodoText = ''<br />    }<br />  }<br />})<br /></pre></td></tr></tbody></table></figure>

<div id="todo-list-example"> <ul><li>      Do the dishes      </li><li>      Take out the trash      </li><li>      Mow the lawn      </li></ul></div>



  
  
    
  
  <div>
      



    Caught a mistake or want to contribute to the documentation?
    <a href="https://github.com/vuejs/vuejs.org/blob/master/src/v2/guide/list.md" target="_blank">
      Edit this page on GitHub!
    </a>
  </div>

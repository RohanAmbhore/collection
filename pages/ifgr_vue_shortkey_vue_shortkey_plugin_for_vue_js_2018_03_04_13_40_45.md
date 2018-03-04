<a href="https://github.com/iFgR/vue-shortkey">https://github.com/iFgR/vue-shortkey</a><div id="articleHeader"><h1>iFgR/vue-shortkey: Vue-ShortKey</h1></div>
    <h3>
      
      README.md
    </h3>

      <p><a href="https://github.com/iFgR/vue-shortkey/blob/master/logo/shortkey.png?raw=true" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://github.com/iFgR/vue-shortkey/raw/master/logo/shortkey.png?raw=true" alt="vue-shortkey logo" /></div></a></p>
<p>Vue-ShortKey - plugin for VueJS 2.x accepts shortcuts globaly and in a single listener.</p>
<h2>Install</h2>
<pre><code>npm install vue-shortkey --save
</code></pre>
<h2>Usage</h2>
<div><pre>Vue.use(require('vue-shortkey'))</pre></div>
<p>Add the shortkey directive to the elements that accept the shortcut.
The shortkey must have explicitly which keys will be used.</p>
<h4>Running functions</h4>
<p><sub>The code below ensures that the key combination ctrl + alt + o will perform the 'theAction' method.</sub></p>
<div><pre>&lt;button v-shortkey="['ctrl', 'alt', 'o']" @shortkey="theAction()"&gt;Open&lt;/button&gt;</pre></div>
<p>The function in the modifier <strong>@shortkey</strong> will be called repeatedly while the key is pressed. To call the function only once, use the <strong>once</strong> modifier</p>
<div><pre>&lt;button v-shortkey.once="['ctrl', 'alt', 'o']" @shortkey="theAction()"&gt;Open&lt;/button&gt;</pre></div>
<h4>Multi keys</h4>
<div><pre>&lt;button v-shortkey="{up: ['arrowup'], down: ['arrowdown']}" @shortkey="theAction"&gt;Joystick&lt;/button&gt;</pre></div>
<p>... and your method will be called with the key in the  parameter</p>
<div><pre>methods: {
  theAction (event) {
    switch (event.srcKey) {
      case 'up':
        ...
        break
      case 'down':
        ...
        break</pre></div>
<h4>Setting the focus</h4>
<p>You can point the focus with the shortcut easily.
<sub>The code below reserves the ALT + I key to set the focus to the input element.</sub></p>
<div><pre>&lt;input type="text" v-shortkey.focus="['alt', 'i']" v-model="name" /&gt;</pre></div>
<h4>Push button</h4>
<p>Sometimes you may need a shortcut works as a push button. It calls the function one time until you release the shortcut. When you release the shortcut, it call the same function again like a toggle. In these cases, insert the "push" modifier.</p>
<p>The example below shows how to do this</p>
<div><pre>&lt;tooltip v-shortkey.push="['f3']" @shortkey="toggleToolTip"&gt;&lt;/tooltip&gt;</pre></div>
<h4>Using on a component</h4>
<p>Use the modifier <code>native</code> to catch the event.</p>
<div><pre> &lt;my-component v-shortkey="['ctrl', 'alt', 'o']" @shortkey.native="theAction()"&gt;&lt;/my-component&gt;</pre></div>
<h4>Key list</h4>
<table>
<thead>
<tr>
<th>Key</th>
<th>Shortkey Name</th>
</tr>
</thead>
<tbody>
<tr>
<td>Shift</td>
<td>shift</td>
</tr>
<tr>
<td>Control</td>
<td>ctrl</td>
</tr>
<tr>
<td>Alt</td>
<td>alt</td>
</tr>
<tr>
<td>Alt Graph</td>
<td>altgraph</td>
</tr>
<tr>
<td>Super (Windows or Mac Cmd)</td>
<td>meta</td>
</tr>
<tr>
<td>Arrow Up</td>
<td>arrowup</td>
</tr>
<tr>
<td>Arrow Down</td>
<td>arrowdown</td>
</tr>
<tr>
<td>Arrow Left</td>
<td>arrowleft</td>
</tr>
<tr>
<td>Arrow Right</td>
<td>arrowright</td>
</tr>
<tr>
<td>Enter</td>
<td>enter</td>
</tr>
<tr>
<td>Escape</td>
<td>esc</td>
</tr>
<tr>
<td>Tab</td>
<td>tab</td>
</tr>
<tr>
<td>Space</td>
<td>space</td>
</tr>
<tr>
<td>Page Up</td>
<td>pageup</td>
</tr>
<tr>
<td>Page Down</td>
<td>pagedown</td>
</tr>
<tr>
<td>Home</td>
<td>home</td>
</tr>
<tr>
<td>End</td>
<td>end</td>
</tr>
<tr>
<td>A - Z</td>
<td>a-z</td>
</tr>
<tr>
<td>0-9</td>
<td>0-9</td>
</tr>
<tr>
<td>F1-F12</td>
<td>f1-f12</td>
</tr></tbody></table>
<p>You can make any combination of keys as well as reserve a single key.</p>
<div><pre>&lt;input type="text" v-shortkey="['q']" @shortkey="foo()"/&gt;
&lt;button v-shortkey="['ctrl', 'p']" @shortkey="bar()"&gt;&lt;/button&gt;
&lt;button v-shortkey="['f1']" @shortkey="help()"&gt;&lt;/button&gt;
&lt;textarea v-shortkey="['ctrl', 'v']" @shortkey="dontPaste()"&gt;&lt;/textarea&gt;</pre></div>
<h4>Avoided fields</h4>
<p>You can avoid shortcuts within fields if you really need it. This can be done in two ways:</p>
<ul>
<li>Preventing a given element from executing the shortcut by adding the <strong>v-shortkey.avoid</strong> tag in the body of the element</li>
</ul>
<div><pre>&lt;textarea v-shortkey.avoid&gt;&lt;/textaea&gt;</pre></div>
<ul>
<li>Generalizing type of element that will not perform shortcut. To do this, insert a list of elements in the global method.</li>
</ul>
<div><pre>Vue.use('vue-shortkey', { prevent: ['input', 'textarea'] })</pre></div>
<ul>
<li>Or even by class</li>
</ul>
<div><pre>Vue.use('vue-shortkey', { prevent: ['.my-class-name', 'textarea.class-of-textarea'] })</pre></div>
<h4>Other uses</h4>
<p>With the dynamism offered by Vue, you can easily create shortcuts dynamically</p>
<div><pre>&lt;li v-for="(ctx, item) in items"&gt;
  &lt;a
    href="https://vuejs.org"
    target="_blank"
    v-shortkey="['f' + (item + 1)]"
    @shortkey="testa(item)"
    @click="testa()"&gt;
      F {{ item }}
  &lt;/a&gt;
&lt;/li&gt;</pre></div>
<h3>Unit Test</h3>
<pre><code>npm test
</code></pre>

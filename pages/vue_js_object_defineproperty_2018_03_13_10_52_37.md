<a href="https://www.jianshu.com/p/07ba2b0c8fca">https://www.jianshu.com/p/07ba2b0c8fca</a><div id="articleHeader"><h1>关于Object.defineProperty</h1></div>
<p>这个函数接受三个参数，一个参数是obj，表示要定义属性的对象,一个参数是prop，是要定义或者更改的属性名字，另外是descriptor,描述符，来定义属性的具体描述。<br />
<code>Object.defineProperty(obj, prop, descriptor)</code></p>
<p>下面的是实例代码，obj是一个没有属性的空对象，然后"key"是属性名，{}大括号里面定义了要给属性赋值的情况，value代表属性的值，<strong>proto</strong>代表继承属性的性质，这里面还有其他的选项。比如configurable,enumerable,writable等默认是false的。</p>
<pre><code>// using __proto__
var obj = {};
Object.defineProperty(obj, 'key', {
  __proto__: null, // no inherited properties
  value: 'static'  // not enumerable
                   // not configurable
                   // not writable
                   // as defaults
});
</code></pre>
<p>我们通过控制台的结果来感受一下writable为false的作用。我们发现，就算对"key"属性重新赋值了，它的属性仍然保持不变。</p>
<div>
<div>

<div><div class="readableLargeImageContainer"><img src="//upload-images.jianshu.io/upload_images/2099962-326822b37e1a4d95.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/365"   /></div>

<div>控制台结果</div>

<p>descriptors（描述符）分成两种，一种是data descriptors,另外一种是 accessor descriptors.两种的descriptors有两个必选项,configurable和enumerable</p>
<blockquote>
<p><strong>configurable</strong><br />
true if and only if the type of this property descriptor may be changed and if the property may be deleted from the corresponding object.<strong>Defaults to false<br />
.</strong></p>
</blockquote>
<p>代表这个属性的descriptor也就是描述是可以更改的，这个熟悉也能从对象上面删除,<strong>默认false</strong>,也就是不能更改跟属性有关的任意值，如果我重新对这个属性进行定义的话，会提示出错,同时也不能删除。</p>
<div>
<div>

<div><div class="readableLargeImageContainer"><img src="//upload-images.jianshu.io/upload_images/2099962-8ec117310684858d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/540"   /></div>

<div>configurable</div>

<blockquote>
<p><strong>enumerable</strong><br />
true if and only if this property shows up during enumeration of the properties on the corresponding object.<strong>Defaults to false<br />
.</strong></p>
</blockquote>
<p>代表这个属性能够通过for in或者<a href="https://link.jianshu.com?t=https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys" target="_blank">Object.keys<br />
</a> 来遍历。<strong>默认为false</strong></p>
<div>
<div>

<div><div class="readableLargeImageContainer"><img src="//upload-images.jianshu.io/upload_images/2099962-acbab5903935ea04.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/438"   /></div>

<div>关于enumerable的属性</div>

<p>A data descriptor有两个可选项.</p>
<blockquote>
<p><strong>value</strong><br />
The value associated with the property. Can be any valid JavaScript value (number, object, function, etc).<strong>Defaults to <a href="https://link.jianshu.com?t=https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined" target="_blank">undefined<br />
</a>.</strong></p>
</blockquote>
<p>这个选项为属性赋值，可以是任意的JavaScript值，<strong>默认为undefined</strong></p>
<blockquote>
<p><strong>writable</strong><br />
true if and only if the value associated with the property may be changed with an <a href="https://link.jianshu.com?t=https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators" target="_blank">assignment operator</a>.<strong>Defaults to false<br />
.</strong></p>
</blockquote>
<p>writable表示能不能够重写属性值，<strong>默认为false</strong></p>
<p>accessor descriptor也有两个关键的属性。</p>
<blockquote>
<p>get<br />
A function which serves as a getter for the property, or <a href="https://link.jianshu.com?t=https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined" target="_blank">undefined<br />
</a> if there is no getter. The function return will be used as the value of property.<strong>Defaults to <a href="https://link.jianshu.com?t=https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined" target="_blank">undefined<br />
</a>.</strong><br />
set</p>
</blockquote>
<p>定义了一个函数，作为属性的getter,如果没有getter就为undefined 默认为undefined</p>
<blockquote>
<p>set<br />
A function which serves as a setter for the property, or <a href="https://link.jianshu.com?t=https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined" target="_blank">undefined<br />
</a> if there is no setter. The function will receive as only argument the new value being assigned to the property.<strong>Defaults to <a href="https://link.jianshu.com?t=https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined" target="_blank">undefined<br />
</a>.</strong></p>
</blockquote>

<p>这里面有一点是，可能会从原型链上面继承相应的属性，如果想避免这种情况，可以写<code>get</code>。所以可以用<code>__proto__: null</code></p>
<p>下面是一个可爱的例子</p>
<pre><code>var o = {}; // Creates a new object 创造对象

// Example of an object property added with defineProperty with a data property descriptor
Object.defineProperty(o, 'a', {
  value: 37,
  writable: true,
  enumerable: true,
  configurable: true
});
// 'a' property exists in the o object and its value is 37 

// Example of an object property added with defineProperty with an accessor property descriptor
var bValue = 38;
Object.defineProperty(o, 'b', {
  get: function() { return bValue; },
  set: function(newValue) { bValue = newValue; },
  enumerable: true,
  configurable: true
});
o.b; // 38
// 'b' property exists in the o object and its value is 38
// The value of o.b is now always identical to bValue, unless o.b is redefined

// You cannot try to mix both:
Object.defineProperty(o, 'conflict', {
  value: 0x9f91102,
  get: function() { return 0xdeadbeef; }
});
// throws a TypeError: value appears only in data descriptors, get appears only in accessor descriptors

</code></pre>
<div>
<div>

<div><div class="readableLargeImageContainer"><img src="//upload-images.jianshu.io/upload_images/2099962-29975379bdef9655.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/543"   /></div>


<p>第一段代表定义了一个data descriptor,第二段代表定义了accessor descriptor，通get定义了取值操作，第三段代码告诉我们这两种不能混用。</p>

<h2>视图和数据变化绑定</h2>
<p>而vue.js主要利用了accessor descriptors的set和get来更新视图，<a href="https://link.jianshu.com?t=http://www.cnblogs.com/oceanxing/p/3938443.html" target="_blank">这里</a>看到的这个例子挺好，是一个简单的绑定。<br />
对于一个html页面</p>
<pre><code>&lt;div&gt;
    &lt;p&gt;你好，&lt;span id='nickName'&gt;&lt;/span&gt;&lt;/p&gt;
    &lt;div id="introduce"&gt;&lt;/div&gt;
&lt;/div&gt;　　　　
</code></pre>
<p>设置一个数据的属性的getter和setter</p>
<pre><code>//视图控制器
var userInfo = {};
Object.defineProperty(userInfo, "nickName", {
    get: function(){
        return document.getElementById('nickName').innerHTML;
    },
    set: function(nick){
        document.getElementById('nickName').innerHTML = nick;
    }
});
Object.defineProperty(userInfo, "introduce", {
    get: function(){
        return document.getElementById('introduce').innerHTML;
    },
    set: function(introduce){
        document.getElementById('introduce').innerHTML = introduce;
    }
})
</code></pre>
<p>然后就能愉快地绑定数据交互了。</p>
<pre><code>userInfo.nickName = "xxx";
userInfo.introduce = "我是xxx，我来自云南，..."
</code></pre>
<h2>vue.js的数据变动</h2>
<p>但是，这个例子只是数据和dom节点的绑定，而vue.js更为复杂一点，它在网页dom和accessor之间会有两层，一层是Wacher，一层是Directive，比如以下代码。</p>
<pre><code>var a = { b: 1 }
var vm = new Vue({ 
  data: data
})
</code></pre>
<p>把一个普通对象（a={b:1}）传给 Vue 实例作为它的 data 选项，Vue.js 将遍历它的属性，用<a href="https://link.jianshu.com?t=https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty" target="_blank">Object.defineProperty</a> 将它们转为 getter/setter,如图绿色的部分所示。<br />
每次用户更改data里的数据的时候，比如<code>a.b =1</code>，setter就会重新通知Watcher进行变动，Watcher再通知Directive对dom节点进行更改。</p><div>
<div>

<div><div class="readableLargeImageContainer"><img src="//upload-images.jianshu.io/upload_images/2099962-1d6deea4b7c6f18d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700"   /></div>




          
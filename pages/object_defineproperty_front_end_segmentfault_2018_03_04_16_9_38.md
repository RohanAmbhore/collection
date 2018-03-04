<a href="https://segmentfault.com/a/1190000004346467">https://segmentfault.com/a/1190000004346467</a><div id="articleHeader"><h1>解析神奇的 Object.defineProperty</h1></div>
                    
<p>这个方法了不起啊。。vue.js是通过它实现双向绑定的。。而且Object.observe也被草案发起人撤回了。。所以defineProperty更有必要了解一下了。</p>
<p>几行代码看他怎么用</p>
<pre><code>var a= {}
Object.defineProperty(a,"b",{
  value:123
})
console.log(a.b);//123</code></pre>
<p>很简单，它接受三个参数，而且都是必填的。。</p>

<ul>
<li><p>第一个参数：目标对象</p></li>
<li><p>第二个参数：需要定义的属性或方法的名字。</p></li>
<li><p>第三个参数：目标属性所拥有的特性。（descriptor）</p></li>
</ul>
<p>前两个参数不多说了，一看代码就懂，主要看第三个参数descriptor，看看有哪些取值</p>
<h2 id="articleHeader1">descriptor</h2>
<p>他又以下取值，我们简单认识一下，后面例子，挨个介绍。</p>
<ul>
<li><p>value：属性的值(不用多说了)</p></li>
<li><p>writable：如果为false，属性的值就不能被重写,只能为只读了</p></li>
<li><p>configurable：总开关，一旦为false，就不能再设置他的（value，writable，configurable）</p></li>
<li><p>enumerable：是否能在for...in循环中遍历出来或在Object.keys中列举出来。</p></li>
<li><p>get：一会细说</p></li>
<li><p>set：一会细说</p></li>
</ul>
<h3 id="articleHeader2">descriptor 默认值</h3>
<p>我们再看看第一个例子</p>
<pre><code>var a= {}
Object.defineProperty(a,"b",{
  value:123
})
console.log(a.b);//123</code></pre>
<p>我们只设置了 value，别的并没有设置，但是<strong>第一次的时候</strong> 可以简单的理解为（暂时这样理解）它会默认帮我们把writable，configurable，enumerable。都设上值，而且值还都是false。。也就是说，上面代码和下面是等价的的（<strong>仅限于第一次设置的时候</strong>）。</p>
<pre><code>var a= {}
Object.defineProperty(a,"b",{
  value:123,
  writable:false,
  enumerable:false,
  configurable:false
})
console.log(a.b);//123</code></pre>
<p><strong>以上非常重要哦。。并且以上理解对set 和 get 不起作用哦</strong></p>
<h3 id="articleHeader3">configurable</h3>
<p>总开关，第一次设置 false 之后，，第二次什么设置也不行了，比如说</p>
<pre><code>var a= {}
Object.defineProperty(a,"b",{
  configurable:false
})
Object.defineProperty(a,"b",{
  configurable:true
})
//error: Uncaught TypeError: Cannot redefine property: b</code></pre>
<p>就会报错了。。</p>
<p>注意上面讲的默认值。。。如果第一次不设置它会怎样。。会帮你设置为false。。所以。。第二次。再设置他会怎样？。。对喽，，会报错</p>
<h3 id="articleHeader4">writable</h3>
<p>如果设置为fasle，就变成只读了。。</p>
<pre><code>var a = {}; 

Object.defineProperty(o, "b", { 
    value : 123,
    writable : false });

console.log(a.b); // 打印 37
a.b = 25; // 没有错误抛出（在严格模式下会抛出，即使之前已经有相同的值）
console.log(o.a); // 打印 37， 赋值不起作用。</code></pre>
<h3 id="articleHeader5">enumerable</h3>
<p>属性特性 enumerable 定义了对象的属性是否可以在 for...in 循环和 Object.keys() 中被枚举。</p>
<pre><code>var a= {}
Object.defineProperty(a,"b",{
  value:3445,
  enumerable:true
})
console.log(Object.keys(a));// 打印["b"]</code></pre>
<p>改为false</p>
<pre><code>var a= {}
Object.defineProperty(a,"b",{
  value:3445,
  enumerable:false //注意咯这里改了
})
console.log(Object.keys(a));// 打印[]</code></pre>
<p>for...in 类似，不赘述了</p>
<h2 id="articleHeader6">set 和 get</h2>
<p>在 descriptor 中不能<strong>同时</strong>设置访问器（get 和 set）和 wriable 或 value，否则会错，就是说想用 get 和 set，就不能用 writable 或 value 中的任何一个。</p>
<p>set 和 get，他俩干啥用的的。</p>
<pre><code>var a= {}
Object.definePrope`请输入代码`rty(a,"b",{
  set:function(newValue){
    console.log("你要赋值给我,我的新值是"＋newValue)
    },
  get:function(){
    console.log("你取我的值")
    return 2 //注意这里，我硬编码返回2
   }
})
a.b =1 //打印 你要赋值给我,我的新值是1
console.log(a.b)    //打印 你取我的值
                    //打印 2    注意这里，和我的硬编码相同的</code></pre>
<p>简单来说，这个 “b” 赋值或者取值的时候会分别触发 set 和 get 对应的函数。</p>
<p><strong><em>这就是实现 observe的关键啊。</em></strong></p>
<p><a href="http://segmentfault.com/a/1190000004384515" target="_blank">下一篇，我会分析vue的observe的实现源码，聊聊自己如何一步一步实现$watch。</a></p>

                
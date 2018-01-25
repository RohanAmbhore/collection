<a href="https://scotch.io/bar-talk/copying-objects-in-javascript">https://scotch.io/bar-talk/copying-objects-in-javascript</a><div id="articleHeader"><h1>Copying Objects in JavaScript</h1></div>
<div>
<div>
<a href="https://jsbin.com/fefedoc/edit?js,console" target="_blank">


Demo
</a>
</div> 





<p>Objects are the fundamental blocks of JavaScript. An object is a collection of properties, and a property is an association between a key (or name) and a value. Almost all objects in JavaScript are instances of <code>Object</code> which sits on the top of the prototype chain.</p>
<h2 id="introduction">
    <a href="#toc-introduction" target="_blank">
      #
      Introduction
    </a> 
  </h2>
<p>As you know, the assignment operator doesn't create a copy of an object, it only assigns a reference to it, let's look at the following code:</p><div>Related Course: <a href="https://bit.ly/2rVqDcs" target="_blank">Getting Started with JavaScript for Web Development</a></div>
<pre><code>let obj = {
  a: 1,
  b: 2,
};
let copy = obj;

obj.a = 5;
console.log(copy.a);
// Result 
// a = 5;</code></pre>
<p><strong> ---&gt; <a href="https://jsbin.com/yudogil/1/edit?js,console" target="_blank">Edit on JS Bin</a></strong></p>
<p>The <code>obj</code> variable is a container for the new object initialized. The <code>copy</code> variable is pointing to the same object and is a reference to that object. So basically this <code>{ a: 1, b: 2, }</code> object is saying: There are now two ways to gain access to me. You have to pass through the <code>obj</code> variable or the <code>copy</code> variable either ways you still get to me and anything you do to me via these ways (gateways) will affect me.</p>
<p>Immutability is widely spoken about these days and you have to listen to this call! This method removes any form of immutability and could lead to bugs should the original object be used by another part of your code.</p>
<h2 id="the-naive-way-of-copying-objects">
    <a href="#toc-the-naive-way-of-copying-objects" target="_blank">
      #
      The Naive Way of Copying Objects
    </a> 
  </h2>
<p>The naive way of copying objects is looping through the original object and copying each property one after the other. Let's take a look at this code:</p>
<pre><code>function copy(mainObj) {
  let objCopy = {}; // objCopy will store a copy of the mainObj
  let key;

  for (key in mainObj) {
    objCopy[key] = mainObj[key]; // copies each property to the objCopy object
  }
  return objCopy;
}

const mainObj = {
  a: 2,
  b: 5,
  c: {
    x: 7,
    y: 4,
  },
}

console.log(copy(mainObj));
</code></pre>
<p><strong> ---&gt; <a href="https://jsbin.com/vukifig/edit?js,console" target="_blank">Edit on JS Bin</a></strong></p>
<h3>Inherent Issues</h3>
<ol>
<li><code>objCopy</code> object has a new <code>Object.prototype</code> method different from the <code>mainObj</code> object prototype method, which is not what we want. We want an exact copy of the original object.</li>
<li>Property descriptors are not copied. A "writable" descriptor with value set to be false will be true in the <code>objCopy</code> object.</li>
<li>The code above only copies enumerable properties of <code>mainObj</code>.</li>
<li>If one of the properties in the original object is an object itself, then it will be shared between the copy and the original making their respective properties point to the same object.</li>
</ol>
<h2 id="shallow-copying-objects">
    <a href="#toc-shallow-copying-objects" target="_blank">
      #
      Shallow Copying Objects
    </a> 
  </h2>
<p>An object is said to be shallow copied when the source top-level properties are copied without any reference and there exist a source property whose value is an object and is copied as a reference. If the source value is a reference to an object, it only copies that reference value to the target object. </p>
<p>A shallow copy will duplicate the top-level properties, but the nested object is shared between the original(source) and the copy(target). </p>
<h3>Using Object.assign() method</h3>
<p>The Object.assign() method is used to copy the values of all enumerable own properties from one or more source objects to a target object.</p>
<pre><code>let obj = {
  a: 1,
  b: 2,
};
let objCopy = Object.assign({}, obj);
console.log(objCopy);
// Result - { a: 1, b: 2 }</code></pre>
<p><strong> ---&gt; <a href="https://jsbin.com/rirawav/edit?js,console" target="_blank">Edit on JS Bin </a></strong></p>
<p>Well, this does the job so far. We have made a copy of <code>obj</code>. Let's see if immutability exist:</p>
<pre><code>let obj = {
  a: 1,
  b: 2,
};
let objCopy = Object.assign({}, obj);

console.log(objCopy); // result - { a: 1, b: 2 }
objCopy.b = 89;
console.log(objCopy); // result - { a: 1, b: 89 }
console.log(obj); // result - { a: 1, b: 2 }</code></pre>
<p><strong> ---&gt; <a href="https://jsbin.com/sugoru/edit?js,console" target="_blank">Edit on JS Bin</a></strong></p>
<p>In the code above, we changed the value of the property <code>'b'</code> in <code>objCopy</code> object to <code>89</code> and when we log the modified <code>objCopy</code> object in the console, the changes only apply to <code>objCopy</code>. The last line of code checks that the <code>obj</code> object is still intact and hasn't change. This implies that we have successfully created a copy of the source object without any references to it.</p>
<h3>Pitfall of Object.assign()</h3>
<p>Not so fast! While we successfully created a copy and everything seem to be working fine, remember we discussed shallow copying? Let's take a look at this example:</p>
<pre><code>let obj = {
  a: 1,
  b: {
    c: 2,
  },
}
let newObj = Object.assign({}, obj);
console.log(newObj); // { a: 1, b: { c: 2} }

obj.a = 10;
console.log(obj); // { a: 10, b: { c: 2} }
console.log(newObj); // { a: 1, b: { c: 2} }

newObj.a = 20;
console.log(obj); // { a: 10, b: { c: 2} }
console.log(newObj); // { a: 20, b: { c: 2} }

newObj.b.c = 30;
console.log(obj); // { a: 10, b: { c: 30} }
console.log(newObj); // { a: 20, b: { c: 30} }

// Note: newObj.b.c = 30; Read why..
</code></pre>
<p><strong> ---&gt; <a href="https://jsbin.com/fefedoc/edit?js,console" target="_blank">Edit on JS Bin</a></strong></p>
<h3>Why is obj.b.c = 30?</h3>
<p>Well, that is a pitfall of <code>Object.assign()</code>. <code>Object.assign</code> only makes shallow copies. Both <code>newObj.b</code> and <code>obj.b</code> share the same reference to the object because of individual copies were not made, instead a reference to the object was copied. Any change made to any of the object's property applies to all references using the object. How can we fix this? Continue reading... we have a fix in the next section.</p>
<p>Note: Properties on the prototype chain and non-enumerable properties cannot be copied. See here:</p>
<pre><code>let someObj = {
  a: 2,
}

let obj = Object.create(someObj, { 
  b: {
    value: 2,  
  },
  c: {
    value: 3,
    enumerable: true,  
  },
});

let objCopy = Object.assign({}, obj);
console.log(objCopy); // { c: 3 }
</code></pre>
<p><strong> ---&gt; <a href="https://jsbin.com/gogubeh/edit?js,console" target="_blank">Edit on JS Bin </a></strong></p>
<ul>
<li><code>someObj</code> is on obj's prototype chain so it wouldn't be copied.</li>
<li><code>property b</code> is a non-enumerable property.</li>
<li><code>property c</code> has an enumerable property descriptor allowing it to be enumerable. That's why it was copied.</li>
</ul>
<h2 id="deep-copying-objects">
    <a href="#toc-deep-copying-objects" target="_blank">
      #
      Deep Copying Objects
    </a> 
  </h2>
<p>A deep copy will duplicate every object it encounters. The copy and the original object will not share anything, so it will be a copy of the original. Here's the fix to the problem we encountered using <code>Object.assign()</code>. Let's explore.</p>
<h3>Using JSON.parse(JSON.stringify(object));</h3>
<p>This fixes the issue we had earlier. Now <code>newObj.b</code> has a copy and not a reference! This is a way to deep copy objects. Here's an example:</p>
<pre><code>let obj = { 
  a: 1,
  b: { 
    c: 2,
  },
}

let newObj = JSON.parse(JSON.stringify(obj));

obj.b.c = 20;
console.log(obj); // { a: 1, b: { c: 20 } }
console.log(newObj); // { a: 1, b: { c: 2 } } (New Object Intact!)</code></pre>
<p>Immutable: ✓</p>
<p><strong> ---&gt; <a href="https://jsbin.com/gogubeh/edit?js,console" target="_blank">Edit on JS Bin</a></strong></p>
<h3>Pitfall</h3>
<p>Unfortunately, this method can't be used to copy user-defined object methods. See below.</p>
<h2 id="copying-object-methods">
    <a href="#toc-copying-object-methods" target="_blank">
      #
      Copying Object methods
    </a> 
  </h2>
<p>A method is a property of an object that is a function. In the examples so far, we haven't copied an object with a method. Let's try that now and use the methods we've learnt to make copies. </p>
<pre><code>let obj = {
  name: 'scotch.io',
  exec: function exec() {
    return true;
  },
}

let method1 = Object.assign({}, obj);
let method2 = JSON.parse(JSON.stringify(obj));

console.log(method1); //Object.assign({}, obj)
/* result
{
  exec: function exec() {
    return true;
  },
  name: "scotch.io"
}
*/

console.log(method2); // JSON.parse(JSON.stringify(obj))
/* result
{
  name: "scotch.io"
}
*/
</code></pre>
<p><strong> ---&gt; <a href="https://jsbin.com/qoxuwe/edit?js,console" target="_blank">Edit on JS Bin</a></strong></p>
<p>The result shows that <code>Object.assign()</code> can be used to copy methods while <code>JSON.parse(JSON.stringify(obj))</code> can't be used.</p>
<h2 id="copying-circular-objects">
    <a href="#toc-copying-circular-objects" target="_blank">
      #
      Copying Circular Objects
    </a> 
  </h2>
<p>Circular objects are objects that have properties referencing themselves. Let's use the methods of copying objects we've learnt so far to make copies of a circular object and see if it works.</p>
<h3>Using JSON.parse(JSON.stringify(object))</h3>
<p>Let's try <code>JSON.parse(JSON.stringify(object))</code>:</p>
<pre><code>// circular object
let obj = { 
  a: 'a',
  b: { 
    c: 'c',
    d: 'd',
  },
}

obj.c = obj.b;
obj.e = obj.a;
obj.b.c = obj.c;
obj.b.d = obj.b;
obj.b.e = obj.b.c;

let newObj = JSON.parse(JSON.stringify(obj));

console.log(newObj); </code></pre>
<p><strong> ---&gt; <a href="https://jsbin.com/bikibet/edit?js,console" target="_blank">Edit on JS Bin</a></strong></p>
<p>Here's the result:
<img /></p>
<p><code>JSON.parse(JSON.stringify(obj))</code> clearly doesn't work for circular objects.</p>
<h3>Using Object.assign()</h3>
<p>Let's try <code>Object.assign()</code>:</p>
<pre><code>// circular object
let obj = { 
  a: 'a',
  b: { 
    c: 'c',
    d: 'd',
  },
}

obj.c = obj.b;
obj.e = obj.a;
obj.b.c = obj.c;
obj.b.d = obj.b;
obj.b.e = obj.b.c;

let newObj2 = Object.assign({}, obj);

console.log(newObj2); </code></pre>
<p><strong> ---&gt; <a href="https://jsbin.com/becoyem/edit?js,console" target="_blank">Edit on JS Bin</a></strong></p>
<p>Here's the result:</p>
<p><img /></p>
<p><code>Object.assign()</code> works fine for shallow copying circular objects but wouldn't work for deep copying. Feel free to explore the <code>circular object tree</code> on your browser console. I'm sure you'll find a lot of interesting work going on there.</p>
<h2 id="using-spread-elements">
    <a href="#toc-using-spread-elements" target="_blank">
      #
      Using Spread Elements ( ... )
    </a> 
  </h2>
<p>ES6 already has rest elements for array destructuring assignment and spread elements for array literals implemented. Take a look at spread element implementation on an array here:</p>
<pre><code>const array = [
  "a",
  "c",
  "d", {
    four: 4
  },
];
const newArray = [...array];
console.log(newArray);
// Result 
// ["a", "c", "d", { four: 4 }]
</code></pre>
<p><strong> ---&gt; <a href="https://jsbin.com/denadeg/edit?js,console" target="_blank">Edit on JS Bin</a></strong></p>
<p>The spread property for object literals is currently a <a href="https://github.com/tc39/proposal-object-rest-spread" target="_blank">Stage 3 proposal for ECMAScript</a>. Spread properties in object initializers copies own enumerable properties from a source object onto the target object. The example below shows how easy it would be to copy an object once the proposal has been accepted.</p>
<pre><code>let obj = {
  one: 1,
  two: 2,
}

let newObj = { ...z };

// { one: 1, two: 2 }</code></pre>
<p>Note: This will just be effective for shallow copy</p>
<h2 id="conclusion">
    <a href="#toc-conclusion" target="_blank">
      #
      Conclusion
    </a> 
  </h2>
<p>Copying objects in JavaScript can be quite daunting especially if you're new to JavaScript and don't know your way around the language. Hopefully this article helped you understand and avoid future pitfalls you may encounter copying objects. If you have any library or piece of code that achieves a better result, feel welcome to share with the community. Happy coding!</p>

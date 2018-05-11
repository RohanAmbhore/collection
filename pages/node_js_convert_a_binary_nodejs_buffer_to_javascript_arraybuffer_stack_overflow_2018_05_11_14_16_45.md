<a href="https://stackoverflow.com/questions/8609289/convert-a-binary-nodejs-buffer-to-javascript-arraybuffer/17064149">https://stackoverflow.com/questions/8609289/convert-a-binary-nodejs-buffer-to-javascript-arraybuffer/17064149</a><div id="articleHeader"><h1>Convert a binary NodeJS Buffer to JavaScript ArrayBuffer</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        78
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>36</b></div>


</div>

            </div>

            
<div>
    <div>

<p>How can I convert a NodeJS binary buffer into a JavaScript ArrayBuffer?</p>
    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-9015666">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>NodeJS, at one point (I think it was v0.6.x) had ArrayBuffer support. I created a small library for base64 encoding and decoding <a href="https://github.com/arunjitsingh/base64" target="_blank">here</a>, but since updating to v0.7, the tests (on NodeJS) fail. I'm thinking of creating something that normalizes this, but till then, I suppose Node's native <code>Buffer</code> should be used.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 26 '12 at 8:50
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-12101012">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        75
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><a href="https://nodejs.org/docs/latest/api/buffer.html#buffer_buffers_and_typedarray" target="_blank">Instances of <code>Buffer</code> are also instances of <code>Uint8Array</code></a> in node.js 4.x and higher.  Thus, the most efficient solution is to access the <code>buf.buffer</code> property directly, as per <a href="https://stackoverflow.com/a/31394257/1375574" target="_blank">https://stackoverflow.com/a/31394257/1375574</a>.  The Buffer constructor also takes an ArrayBufferView argument if you need to go the other direction.</p>

<p>Note that this will not create a copy, which means that writes to any ArrayBufferView will write through to the original Buffer instance.</p><hr />
In older versions, node.js has both ArrayBuffer as part of v8, but the Buffer class provides a more flexible API.  In order to read or write to an ArrayBuffer, you only need to create a view and copy across.<p>From Buffer to ArrayBuffer:</p>

<pre><code>function toArrayBuffer(buf) {
    var ab = new ArrayBuffer(buf.length);
    var view = new Uint8Array(ab);
    for (var i = 0; i &lt; buf.length; ++i) {
        view[i] = buf[i];
    }
    return ab;
}</code></pre>

<p>From ArrayBuffer to Buffer:</p>

<pre><code>function toBuffer(ab) {
    var buf = new Buffer(ab.byteLength);
    var view = new Uint8Array(ab);
    for (var i = 0; i &lt; buf.length; ++i) {
        buf[i] = view[i];
    }
    return buf;
}</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-17064149">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        38
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>"From ArrayBuffer to Buffer" could be done this way: </p>

<pre><code>var buffer = Buffer.from( new Uint8Array(ab) );</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-19544002">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        22
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>A quicker way to write it</p>

<pre><code>var arrayBuffer = new Uint8Array(nodeBuffer).buffer;</code></pre>

<p>However, this appears to run roughly 4 times slower than the suggested toArrayBuffer function on a buffer with 1024 elements.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 23 '13 at 14:06
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-22165328">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        12
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Use the following excellent npm package: <a href="https://www.npmjs.com/package/to-arraybuffer" target="_blank"><code>to-arraybuffer</code></a>.</p>

<p>Or, you can implement it yourself. If your buffer is called <code>buf</code>, do this:</p>

<pre><code>buf.buffer.slice(buf.byteOffset, buf.byteOffset + buf.byteLength)</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-31242762">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I tried the above for a Float64Array and it just did not work.</p>

<p>I ended up realising that really the data needed to be read 'INTO' the view in correct chunks. This means reading 8 bytes at a time from the source Buffer.</p>

<p>Anyway this is what I ended up with...</p>

<pre><code>var buff = new Buffer("40100000000000004014000000000000", "hex");
var ab = new ArrayBuffer(buff.length);
var view = new Float64Array(ab);

var viewIndex = 0;
for (var bufferIndex=0;bufferIndex&lt;buff.length;bufferIndex=bufferIndex+8)            {

    view[viewIndex] = buff.readDoubleLE(bufferIndex);
    viewIndex++;
}</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jul 6 '15 at 9:54
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-31394257">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        26
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<ul>
<li><strong>No dependencies, fastest, node 4.x and later</strong></li>
</ul>

<p>Buffers are Uint8Arrays, so you just need to access its ArrayBuffer. This is <em>O(1)</em>:</p>

<pre><code> // node buffer
var b = new Buffer(512);
 // ArrayBuffer
var ab = b.buffer.slice(b.byteOffset, b.byteOffset + b.byteLength);
 // TypedArray
var ui32 = new Uint32Array(b.buffer, b.byteOffset, b.byteLength / Uint32Array.BYTES_PER_ELEMENT);</code></pre>

<p>The <code>slice</code> and offset stuff is <strong>required</strong> because small Buffers (&lt;4096 bytes, I think) are views on a shared ArrayBuffer. Without it you might end up with an ArrayBuffer containing data from another TypedArray.</p>

<ul>
<li><strong>No dependencies, moderate speed, any version of node</strong></li>
</ul>

<p>Use <a href="https://stackoverflow.com/a/12101012/1218408" target="_blank">Martin Thomson's answer</a>, which runs in <em>O(n)</em> time. (See also my replies to comments on his answer about non-optimizations. Using a DataView is slow. Even if you need to flip bytes, there are faster ways to do so.)</p>

<ul>
<li><strong>Dependency, fast, any version of node</strong></li>
</ul>

<p>You can use <a href="https://www.npmjs.com/package/memcpy" target="_blank">https://www.npmjs.com/package/memcpy</a> to go in either direction (Buffer to ArrayBuffer and back). It's faster than the other answers posted here and is a well-written library. Node 0.12 through iojs 3.x require ngossen's fork (see <a href="https://github.com/dcodeIO/node-memcpy/pull/6" target="_blank">this</a>).</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-33606515">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I have already update my node to Version 5.0.0
And I work work with this:</p>

<pre><code>function toArrayBuffer(buffer){
    var array = [];
    var json = buffer.toJSON();
    var list = json.data

    for(var key in list){
        array.push(fixcode(list[key].toString(16)))
    }

    function fixcode(key){
        if(key.length==1){
            return '0'+key.toUpperCase()
        }else{
            return key.toUpperCase()
        }
    }

    return array
}</code></pre>

<p>I use it to check my vhd disk image.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-42335394">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>This Proxy will expose the buffer as any of the TypedArrays, without any copy. : </p>

<p><a href="https://www.npmjs.com/package/node-buffer-as-typedarray" target="_blank">https://www.npmjs.com/package/node-buffer-as-typedarray</a></p>

<p>It only works on LE, but can be easily ported to BE.
Also, never got to actually test how efficient this is.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Feb 20 '17 at 2:07
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-45965552">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>You can think of an <code>ArrayBuffer</code> as a typed <code>Buffer</code>. </p>

<p>An <code>ArrayBuffer</code> therefore always needs a type (the so-called "Array Buffer View"). Typically, the <strong>Array Buffer View</strong> has a type of <code>Uint8Array</code> or <code>Uint16Array</code>.</p>

<p>There is a good article from Renato Mangini on <a href="https://developers.google.com/web/updates/2012/06/How-to-convert-ArrayBuffer-to-and-from-String" target="_blank">converting between an ArrayBuffer and a String</a>.</p>

<p>I have summarized the essential parts in a code example (for Node.js). It also shows how to convert between the typed <code>ArrayBuffer</code> and the untyped <code>Buffer</code>.</p>

<pre><code>function stringToArrayBuffer(string) {
  const arrayBuffer = new ArrayBuffer(string.length);
  const arrayBufferView = new Uint8Array(arrayBuffer);
  for (let i = 0; i &lt; string.length; i++) {
    arrayBufferView[i] = string.charCodeAt(i);
  }
  return arrayBuffer;
}

function arrayBufferToString(buffer) {
  return String.fromCharCode.apply(null, new Uint8Array(buffer));
}

const helloWorld = stringToArrayBuffer('Hello, World!'); // "ArrayBuffer" (Uint8Array)
const encodedString = new Buffer(helloWorld).toString('base64'); // "string"
const decodedBuffer = Buffer.from(encodedString, 'base64'); // "Buffer"
const decodedArrayBuffer = new Uint8Array(decodedBuffer).buffer; // "ArrayBuffer" (Uint8Array)

console.log(arrayBufferToString(decodedArrayBuffer)); // prints "Hello, World!"</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 30 '17 at 16:31
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-48418283">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        4
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<h1>1. A <code>Buffer</code> is just a <em>view</em> for looking into an <code>ArrayBuffer</code>.</h1>

<p>A <code>Buffer</code>, in fact, is a <code>FastBuffer</code>, which <code>extends</code> (inherits from) <code>Uint8Array</code>, which is a octet-unit <em>view</em> (“partial accessor”) of the actual memory, an <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer" target="_blank"><code>ArrayBuffer</code></a>.</p>

  <em>📜</em><a href="https://github.com/nodejs/node/blob/a083786c7733b5828102661a04a86884c934950a/lib/buffer.js#L65-L73" target="_blank"><strong><code>/lib/buffer.js#L65-L73</code></strong></a> <sup>Node.js 9.4.0</sup>

<pre><code>class FastBuffer extends Uint8Array {
  constructor(arg1, arg2, arg3) {
    super(arg1, arg2, arg3);
  }
}
FastBuffer.prototype.constructor = Buffer;
internalBuffer.FastBuffer = FastBuffer;

Buffer.prototype = FastBuffer.prototype;</code></pre>

<hr />

<h1>2. The size of an <code>ArrayBuffer</code> and the size of its <em>view</em> may vary.</h1>

<h2>Reason #1: <code>Buffer.from(arrayBuffer[, byteOffset[, length]])</code>.</h2>

<p>With <code>Buffer.from(arrayBuffer[, byteOffset[, length]])</code>, you can create a <code>Buffer</code> with specifying its underlying <code>ArrayBuffer</code> and the view's position and size.</p>

<pre><code>const test_buffer = Buffer.from(new ArrayBuffer(50), 40, 10);
console.info(test_buffer.buffer.byteLength); // 50; the size of the memory.
console.info(test_buffer.length); // 10; the size of the view.</code></pre>

<h2>Reason #2: <code>FastBuffer</code>'s memory allocation.</h2>

<p>It allocates the memory in two different ways depending on the size.</p>

<ul>
<li><strong>If the size is less than the half of the size of a <em>memory pool</em> and is not 0 (“small”)</strong>: it makes use of a <em>memory pool</em> to prepare the required memory.</li>
<li><strong>Else</strong>: it creates a dedicated <code>ArrayBuffer</code> that exactly fits the required memory.</li>
</ul>

  <em>📜</em><a href="https://github.com/nodejs/node/blob/a083786c7733b5828102661a04a86884c934950a/lib/buffer.js#L306-L320" target="_blank"><strong><code>/lib/buffer.js#L306-L320</code></strong></a> <sup>Node.js 9.4.0</sup>

<pre><code>function allocate(size) {
  if (size &lt;= 0) {
    return new FastBuffer();
  }
  if (size &lt; (Buffer.poolSize &gt;&gt;&gt; 1)) {
    if (size &gt; (poolSize - poolOffset))
      createPool();
    var b = new FastBuffer(allocPool, poolOffset, size);
    poolOffset += size;
    alignPool();
    return b;
  } else {
    return createUnsafeBuffer(size);
  }
}</code></pre>

  <em>📜</em><a href="https://github.com/nodejs/node/blob/a083786c7733b5828102661a04a86884c934950a/lib/buffer.js#L98-L100" target="_blank"><strong><code>/lib/buffer.js#L98-L100</code></strong></a> <sup>Node.js 9.4.0</sup>

<pre><code>function createUnsafeBuffer(size) {
  return new FastBuffer(createUnsafeArrayBuffer(size));
}</code></pre>

<hr />

<h3>What do you mean by a “<em>memory pool</em>”?</h3>

<p>A <a href="https://en.wikipedia.org/wiki/Memory_pool" target="_blank"><em>memory pool</em></a> is a fixed-size <strong>pre-allocated</strong> memory block for keeping small-size memory chunks for <code>Buffer</code>s. Using it keeps the small-size memory chunks tightly together, so prevents <a href="https://en.wikipedia.org/wiki/Fragmentation_(computing)" target="_blank"><em>fragmentation</em></a> caused by separate management (allocation and deallocation) of small-size memory chunks.</p>

<p>In this case, the memory pools are <code>ArrayBuffer</code>s whose size is 8 KiB by default, which is specified in <a href="https://nodejs.org/api/buffer.html#buffer_class_property_buffer_poolsize" target="_blank"><code>Buffer.poolSize</code></a>. When it is to provide a small-size memory chunk for a <code>Buffer</code>, it checks if the last memory pool has enough available memory to handle this; if so, it creates a <code>Buffer</code> that <em>“views”</em> the given partial chunk of the memory pool, otherwise, it creates a new memory pool and so on.</p>

<hr />

<p>You can access the underlying <code>ArrayBuffer</code> of a <code>Buffer</code>. The <code>Buffer</code>'s <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray/buffer" target="_blank"><code>buffer</code> property</a> (that is, inherited from <code>Uint8Array</code>) holds it. <strong>A <em>“small”</em> <code>Buffer</code>'s <code>buffer</code> property is an <code>ArrayBuffer</code> that represents the entire memory pool.</strong> So in this case, the <code>ArrayBuffer</code> and the <code>Buffer</code> varies in size.</p>

<pre><code>const zero_sized_buffer = Buffer.allocUnsafe(0);
const small_buffer = Buffer.from([0xC0, 0xFF, 0xEE]);
const big_buffer = Buffer.allocUnsafe(Buffer.poolSize &gt;&gt;&gt; 1);

// A `Buffer`'s `length` property holds the size, in octets, of the view.
// An `ArrayBuffer`'s `byteLength` property holds the size, in octets, of its data.

console.info(zero_sized_buffer.length); /// 0; the view's size.
console.info(zero_sized_buffer.buffer.byteLength); /// 0; the memory..'s size.
console.info(Buffer.poolSize); /// 8192; a memory pool's size.

console.info(small_buffer.length); /// 3; the view's size.
console.info(small_buffer.buffer.byteLength); /// 8192; the memory pool's size.
console.info(Buffer.poolSize); /// 8192; a memory pool's size.

console.info(big_buffer.length); /// 4096; the view's size.
console.info(big_buffer.buffer.byteLength); /// 4096; the memory's size.
console.info(Buffer.poolSize); /// 8192; a memory pool's size.</code></pre>

<hr />

<h1>3. So we need to extract the memory it <em>“views”</em>.</h1>

<p>An <code>ArrayBuffer</code> is fixed in size, so we need to extract it out by making a copy of the part. To do this, we use <code>Buffer</code>'s <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray/byteOffset" target="_blank"><code>byteOffset</code> property</a> and <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray/length" target="_blank"><code>length</code> property</a>, which are inherited from <code>Uint8Array</code>, and <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer/slice" target="_blank">the <code>ArrayBuffer.prototype.slice</code> method</a>, which makes a copy of a part of an <code>ArrayBuffer</code>. The <code>slice()</code>-ing method herein was inspired by <a href="https://stackoverflow.com/a/31394257/4510033" target="_blank">@ZachB</a>.</p>

<pre><code>const test_buffer = Buffer.from(new ArrayBuffer(10));
const zero_sized_buffer = Buffer.allocUnsafe(0);
const small_buffer = Buffer.from([0xC0, 0xFF, 0xEE]);
const big_buffer = Buffer.allocUnsafe(Buffer.poolSize &gt;&gt;&gt; 1);

function extract_arraybuffer(buf)
{
    // You may use the `byteLength` property instead of the `length` one.
    return buf.buffer.slice(buf.byteOffset, buf.byteOffset + buf.length);
}

// A copy -
const test_arraybuffer = extract_arraybuffer(test_buffer); // of the memory.
const zero_sized_arraybuffer = extract_arraybuffer(zero_sized_buffer); // of the... void.
const small_arraybuffer = extract_arraybuffer(small_buffer); // of the part of the memory.
const big_arraybuffer = extract_arraybuffer(big_buffer); // of the memory.

console.info(test_arraybuffer.byteLength); // 10
console.info(zero_sized_arraybuffer.byteLength); // 0
console.info(small_arraybuffer.byteLength); // 3
console.info(big_arraybuffer.byteLength); // 4096</code></pre>

<hr />

<h1>4. Performance improvement</h1>

<p><strong>If you're to use the results as read-only, or it is okay to modify the input <code>Buffer</code>s' contents</strong>, you can avoid unnecessary memory copying.</p>

<pre><code>const test_buffer = Buffer.from(new ArrayBuffer(10));
const zero_sized_buffer = Buffer.allocUnsafe(0);
const small_buffer = Buffer.from([0xC0, 0xFF, 0xEE]);
const big_buffer = Buffer.allocUnsafe(Buffer.poolSize &gt;&gt;&gt; 1);

function obtain_arraybuffer(buf)
{
    if(buf.length === buf.buffer.byteLength)
    {
        return buf.buffer;
    } // else:
    // You may use the `byteLength` property instead of the `length` one.
    return buf.buffer.subarray(buf.byteOffset, buf.byteOffset + buf.length);
}

// Its underlying `ArrayBuffer`.
const test_arraybuffer = obtain_arraybuffer(test_buffer);
// Just a zero-sized `ArrayBuffer`.
const zero_sized_arraybuffer = obtain_arraybuffer(zero_sized_buffer);
// A copy of the part of the memory.
const small_arraybuffer = obtain_arraybuffer(small_buffer);
// Its underlying `ArrayBuffer`.
const big_arraybuffer = obtain_arraybuffer(big_buffer);

console.info(test_arraybuffer.byteLength); // 10
console.info(zero_sized_arraybuffer.byteLength); // 0
console.info(small_arraybuffer.byteLength); // 3
console.info(big_arraybuffer.byteLength); // 4096</code></pre>
    </div>
    
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    




<div id="post-editor">

    <div> 
        <div>
            <div id="mdhelp">
    <ul id="mdhelp-tabs">
        <li>Links</li>
        <li>Images</li>
        <li>Styling/Headers</li>
        <li>Lists</li>
        <li>Blockquotes</li>
        
        
        <li><a href="/editing-help" target="_blank">advanced help »</a></li>
    </ul>
    
    

    
    
    

    

    

    

    
</div>
            
        </div>
    </div>

    
    

    

    


    
    
    



</div>

                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/node.js" title="show questions tagged 'node.js'" target="_blank">node.js</a> <a href="/questions/tagged/binary" title="show questions tagged 'binary'" target="_blank">binary</a> <a href="/questions/tagged/buffer" title="show questions tagged 'buffer'" target="_blank">buffer</a> <a href="/questions/tagged/arraybuffer" title="show questions tagged 'arraybuffer'" target="_blank">arraybuffer</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
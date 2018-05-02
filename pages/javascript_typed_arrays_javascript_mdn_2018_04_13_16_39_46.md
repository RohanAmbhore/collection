<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Typed_arrays">https://developer.mozilla.org/en-US/docs/Web/JavaScript/Typed_arrays</a><div id="articleHeader"><h1>JavaScript typed arrays</h1></div>
  
  
  

      
      

    
      
        

          
          

            
            

              

              
              

              

              
              

              
              
                
                  
                    

<p>JavaScript typed arrays are array-like objects and provide a mechanism for accessing raw binary data. As you may already know, <a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array" title="The JavaScript Array object is a global object that is used in the construction of arrays; which are high-level, list-like objects." target="_blank"><code>Array</code></a> objects grow and shrink dynamically and can have any JavaScript value. JavaScript engines perform optimizations so that these arrays are fast. However, as web applications become more and more powerful, adding features such as audio and video manipulation, access to raw data using WebSockets, and so forth, it has become clear that there are times when it would be helpful for JavaScript code to be able to quickly and easily manipulate raw binary data in typed arrays.</p>

<p>However, typed arrays are not to be confused with normal arrays, as calling <a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray" title="The Array.isArray() function determines whether the passed value is an Array." target="_blank"><code>Array.isArray()</code></a> on a typed array returns <code>false</code>. Moreover, not all methods available for normal arrays are supported by typed arrays (e.g. push and pop).</p>

<h2 id="Buffers_and_views_typed_array_architecture">Buffers and views: typed array architecture</h2>

<p>To achieve maximum flexibility and efficiency, JavaScript typed arrays split the implementation into <strong>buffers</strong> and <strong>views</strong>. A buffer (implemented by the <a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer" title="The ArrayBuffer object is used to represent a generic, fixed-length raw binary data buffer. You cannot directly manipulate the contents of an ArrayBuffer; instead, you create one of the typed array objects or a DataView object which represents the buffer in a specific format, and use that to read and write the contents of the buffer." target="_blank"><code>ArrayBuffer</code></a> object) is an object representing a chunk of data; it has no format to speak of and offers no mechanism for accessing its contents. In order to access the memory contained in a buffer, you need to use a view. A view provides a context — that is, a data type, starting offset, and the number of elements — that turns the data into a typed array.</p>

<p><div class="readableLargeImageContainer"><img src="https://mdn.mozillademos.org/files/8629/typed_arrays.png" alt="Typed arrays in an ArrayBuffer" /></div></p>

<h3 id="ArrayBuffer">ArrayBuffer</h3>

<p>The <a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer" title="The ArrayBuffer object is used to represent a generic, fixed-length raw binary data buffer. You cannot directly manipulate the contents of an ArrayBuffer; instead, you create one of the typed array objects or a DataView object which represents the buffer in a specific format, and use that to read and write the contents of the buffer." target="_blank"><code>ArrayBuffer</code></a> is a data type that is used to represent a generic, fixed-length binary data buffer. You can't directly manipulate the contents of an <code>ArrayBuffer</code>; instead, you create a typed array view or a <a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView" title="The DataView view provides a low-level interface for reading and writing multiple number types in an ArrayBuffer irrespective of the platform's endianness." target="_blank"><code>DataView</code></a> which represents the buffer in a specific format, and use that to read and write the contents of the buffer.</p>

<h3 id="Typed_array_views">Typed array views</h3>

<p>Typed array views have self-descriptive names and provide views for all the usual numeric types like <code>Int8</code>, <code>Uint32</code>, <code>Float64</code> and so forth. There is one special typed array view, the <code>Uint8ClampedArray</code>. It clamps the values between 0 and 255. This is useful for <a href="/en-US/docs/Web/API/ImageData" target="_blank">Canvas data processing</a>, for example.</p>

<table>
 <tbody>
  <tr>
   <td>Type</td>
   <td>Value Range</td>
   <td>Size in bytes</td>
   <td>Description</td>
   <td>Web IDL type</td>
   <td>Equivalent C type</td>
  </tr>
  <tr>
   <td><a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int8Array" title="The Int8Array typed array represents an array of twos-complement 8-bit signed integers. The contents are initialized to 0. Once established, you can reference elements in the array using the object's methods, or using standard array index syntax (that is, using bracket notation)." target="_blank"><code>Int8Array</code></a></td>
   <td>-128 to 127</td>
   <td>1</td>
   <td>8-bit two's complement signed integer</td>
   <td><code>byte</code></td>
   <td><code>int8_t</code></td>
  </tr>
  <tr>
   <td><a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array" title="The Uint8Array typed array represents an array of 8-bit unsigned integers. The contents are initialized to 0. Once established, you can reference elements in the array using the object's methods, or using standard array index syntax (that is, using bracket notation)." target="_blank"><code>Uint8Array</code></a></td>
   <td>0 to 255</td>
   <td>1</td>
   <td>8-bit unsigned integer</td>
   <td><code>octet</code></td>
   <td><code>uint8_t</code></td>
  </tr>
  <tr>
   <td><a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8ClampedArray" title="The Uint8ClampedArray typed array represents an array of 8-bit unsigned integers clamped to 0-255; if you specified a value that is out of the range of [0,255], 0 or 255 will be set instead; if you specify a non-integer, the nearest integer will be set. The contents are initialized to 0. Once established, you can reference elements in the array using the object's methods, or using standard array index syntax (that is, using bracket notation)." target="_blank"><code>Uint8ClampedArray</code></a></td>
   <td>0 to 255</td>
   <td>1</td>
   <td>8-bit unsigned integer (clamped)</td>
   <td><code>octet</code></td>
   <td><code>uint8_t</code></td>
  </tr>
  <tr>
   <td><a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int16Array" title="The Int16Array typed array represents an array of twos-complement 16-bit signed integers in the platform byte order. If control over byte order is needed, use DataView instead. The contents are initialized to 0. Once established, you can reference elements in the array using the object's methods, or using standard array index syntax (that is, using bracket notation)." target="_blank"><code>Int16Array</code></a></td>
   <td>-32768 to 32767</td>
   <td>2</td>
   <td>16-bit two's complement signed integer</td>
   <td><code>short</code></td>
   <td><code>int16_t</code></td>
  </tr>
  <tr>
   <td><a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint16Array" title="The Uint16Array typed array represents an array of 16-bit unsigned integers in the platform byte order. If control over byte order is needed, use DataView instead. The contents are initialized to 0. Once established, you can reference elements in the array using the object's methods, or using standard array index syntax (that is, using bracket notation)." target="_blank"><code>Uint16Array</code></a></td>
   <td>0 to 65535</td>
   <td>2</td>
   <td>16-bit unsigned integer</td>
   <td><code>unsigned short</code></td>
   <td><code>uint16_t</code></td>
  </tr>
  <tr>
   <td><a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int32Array" title="The Int32Array typed array represents an array of twos-complement 32-bit signed integers in the platform byte order. If control over byte order is needed, use DataView instead. The contents are initialized to 0. Once established, you can reference elements in the array using the object's methods, or using standard array index syntax (that is, using bracket notation)." target="_blank"><code>Int32Array</code></a></td>
   <td>-2147483648 to 2147483647</td>
   <td>4</td>
   <td>32-bit two's complement signed integer</td>
   <td><code>long</code></td>
   <td><code>int32_t</code></td>
  </tr>
  <tr>
   <td><a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint32Array" title="The Uint32Array typed array represents an array of 32-bit unsigned integers in the platform byte order. If control over byte order is needed, use DataView instead. The contents are initialized to 0. Once established, you can reference elements in the array using the object's methods, or using standard array index syntax (that is, using bracket notation)." target="_blank"><code>Uint32Array</code></a></td>
   <td>0 to 4294967295</td>
   <td>4</td>
   <td>32-bit unsigned integer</td>
   <td><code>unsigned long</code></td>
   <td><code>uint32_t</code></td>
  </tr>
  <tr>
   <td><a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float32Array" title="The Float32Array typed array represents an array of 32-bit floating point numbers (corresponding to the C float data type) in the platform byte order. If control over byte order is needed, use DataView instead. The contents are initialized to 0. Once established, you can reference elements in the array using the object's methods, or using standard array index syntax (that is, using bracket notation)." target="_blank"><code>Float32Array</code></a></td>
   <td>1.2x10<sup>-38</sup> to 3.4x10<sup>38</sup></td>
   <td>4</td>
   <td>32-bit IEEE floating point number ( 7 significant digits e.g. 1.1234567)</td>
   <td><code>unrestricted float</code></td>
   <td><code>float</code></td>
  </tr>
  <tr>
   <td><a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float64Array" title="The Float64Array typed array represents an array of 64-bit floating point numbers (corresponding to the C double data type) in the platform byte order. If control over byte order is needed, use DataView instead. The contents are initialized to 0. Once established, you can reference elements in the array using the object's methods, or using standard array index syntax (that is, using bracket notation)." target="_blank"><code>Float64Array</code></a></td>
   <td>5.0x10<sup>-324</sup> to 1.8x10<sup>308</sup></td>
   <td>8</td>
   <td>64-bit IEEE floating point number (16 significant digits e.g. 1.123...15)</td>
   <td><code>unrestricted double</code></td>
   <td><code>double</code></td>
  </tr>
 </tbody>
</table>

<h3 id="DataView">DataView</h3>

<p>The <a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView" title="The DataView view provides a low-level interface for reading and writing multiple number types in an ArrayBuffer irrespective of the platform's endianness." target="_blank"><code>DataView</code></a> is a low-level interface that provides a getter/setter API to read and write arbitrary data to the buffer. This is useful when dealing with different types of data, for example. Typed array views are in the native byte-order (see <a href="/en-US/docs/Glossary/Endianness" title="Endianness: "Endian" and "endianness" (or "byte-order") describe how computers organize the bytes that make up numbers." target="_blank">Endianness</a>) of your platform. With a <code>DataView</code> you are able to control the byte-order. It is big-endian by default and can be set to little-endian in the getter/setter methods.</p>

<h2 id="Web_APIs_using_typed_arrays">Web APIs using typed arrays</h2>

<dl>
 <dt><a href="/en-US/docs/Web/API/FileReader#readAsArrayBuffer()" title="/en-US/docs/Web/API/FileReader#readAsArrayBuffer()" target="_blank"><code>FileReader.prototype.readAsArrayBuffer()</code></a></dt>
 <dd>The <code>FileReader.prototype.readAsArrayBuffer()</code> method starts reading the contents of the specified <a href="/en-US/docs/Web/API/Blob" title="/en-US/docs/DOM/Blob" target="_blank"><code>Blob</code></a> or <a href="/en-US/docs/Web/API/File" title="/en-US/docs/DOM/File" target="_blank"><code>File</code></a>.</dd>
 <dt><a href="/en-US/docs/Web/API/XMLHttpRequest#send()" title="/en-US/docs/Web/API/XMLHttpRequest#send()" target="_blank"><code>XMLHttpRequest.prototype.send()</code></a></dt>
 <dd><code>XMLHttpRequest</code> instances' <code>send()</code> method now supports typed arrays and <a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer" title="The ArrayBuffer object is used to represent a generic, fixed-length raw binary data buffer. You cannot directly manipulate the contents of an ArrayBuffer; instead, you create one of the typed array objects or a DataView object which represents the buffer in a specific format, and use that to read and write the contents of the buffer." target="_blank"><code>ArrayBuffer</code></a> objects as argument.</dd>
 <dt><code><a href="https://developer.mozilla.org/en-US/docs/Web/API/ImageData" target="_blank">ImageData.data</a></code></dt>
 <dd>Is a <a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8ClampedArray" title="The Uint8ClampedArray typed array represents an array of 8-bit unsigned integers clamped to 0-255; if you specified a value that is out of the range of [0,255], 0 or 255 will be set instead; if you specify a non-integer, the nearest integer will be set. The contents are initialized to 0. Once established, you can reference elements in the array using the object's methods, or using standard array index syntax (that is, using bracket notation)." target="_blank"><code>Uint8ClampedArray</code></a> representing a one-dimensional array containing the data in the RGBA order, with integer values between <code>0</code> and <code>255</code> inclusive.</dd>
</dl>

<h2 id="Examples">Examples</h2>

<h3 id="Using_views_with_buffers">Using views with buffers</h3>

<p>First of all, we will need to create a buffer, here with a fixed length of 16-bytes:</p>

<pre><code>var buffer = new ArrayBuffer(16);</code></pre>

<p>At this point, we have a chunk of memory whose bytes are all pre-initialized to 0. There's not a lot we can do with it, though. We can confirm that it is indeed 16 bytes long, and that's about it:</p>

<pre><code>if (buffer.byteLength === 16) {
  console.log("Yes, it's 16 bytes.");
} else {
  console.log("Oh no, it's the wrong size!");
}</code></pre>

<p>Before we can really work with this buffer, we need to create a view. Let's create a view that treats the data in the buffer as an array of 32-bit signed integers:</p>

<pre><code>var int32View = new Int32Array(buffer);</code></pre>

<p>Now we can access the fields in the array just like a normal array:</p>

<pre><code>for (var i = 0; i &lt; int32View.length; i++) {
  int32View[i] = i * 2;
}</code></pre>

<p>This fills out the 4 entries in the array (4 entries at 4 bytes each makes 16 total bytes) with the values 0, 2, 4, and 6.</p>

<h3 id="Multiple_views_on_the_same_data">Multiple views on the same data</h3>

<p>Things start to get really interesting when you consider that you can create multiple views onto the same data. For example, given the code above, we can continue like this:</p>

<pre><code>var int16View = new Int16Array(buffer);

for (var i = 0; i &lt; int16View.length; i++) {
  console.log('Entry ' + i + ': ' + int16View[i]);
}</code></pre>

<p>Here we create a 16-bit integer view that shares the same buffer as the existing 32-bit view and we output all the values in the buffer as 16-bit integers. Now we get the output 0, 0, 2, 0, 4, 0, 6, 0.</p>

<p>You can go a step farther, though. Consider this:</p>

<pre><code>int16View[0] = 32;
console.log('Entry 0 in the 32-bit array is now ' + int32View[0]);</code></pre>

<p>The output from this is "Entry 0 in the 32-bit array is now 32". In other words, the two arrays are indeed simply viewed on the same data buffer, treating it as different formats. You can do this with any <a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray#TypedArray_objects" title="JavaScript typed arrays/ArrayBufferView#Typed array subclasses" target="_blank">view types</a>.</p>

<h3 id="Working_with_complex_data_structures">Working with complex data structures</h3>

<p>By combining a single buffer with multiple views of different types, starting at different offsets into the buffer, you can interact with data objects containing multiple data types. This lets you, for example, interact with complex data structures from <a href="/en-US/docs/Web/WebGL" title="WebGL" target="_blank">WebGL</a>, data files, or C structures you need to use while using <a href="/en-US/docs/Mozilla/js-ctypes" title="js-ctypes" target="_blank">js-ctypes</a>.</p>

<p>Consider this C structure:</p>

<pre><code>struct someStruct {
  unsigned long id;
  char username[16];
  float amountDue;
};</code></pre>

<p>You can access a buffer containing data in this format like this:</p>

<pre><code>var buffer = new ArrayBuffer(24);

// ... read the data into the buffer ...

var idView = new Uint32Array(buffer, 0, 1);
var usernameView = new Uint8Array(buffer, 4, 16);
var amountDueView = new Float32Array(buffer, 20, 1);</code></pre>

<p>Then you can access, for example, the amount due with <code>amountDueView[0]</code>.</p>

<div><strong>Note:</strong> The <a href="http://en.wikipedia.org/wiki/Data_structure_alignment" title="http://en.wikipedia.org/wiki/Data_structure_alignment" target="_blank">data structure alignment</a> in a C structure is platform-dependent. Take precautions and considerations for these padding differences.</div>

<h3 id="Conversion_to_normal_arrays">Conversion to normal arrays</h3>

<p>After processing a typed array, it is sometimes useful to convert it back to a normal array in order to benefit from the <a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array" title="The JavaScript Array object is a global object that is used in the construction of arrays; which are high-level, list-like objects." target="_blank"><code>Array</code></a> prototype. This can be done using <a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from" title="The Array.from() method creates a new Array instance from an array-like or iterable object." target="_blank"><code>Array.from</code></a>, or using the following code where <code>Array.from</code> is unsupported.</p>

<pre><code>var typedArray = new Uint8Array([1, 2, 3, 4]),
    normalArray = Array.prototype.slice.call(typedArray);
normalArray.length === 4;
normalArray.constructor === Array;</code></pre>

<h2 id="Specifications">Specifications</h2>



<h2 id="Browser_compatibility">Browser compatibility</h2>



<div><table><thead><tr><td></td><th colspan="6"><abbr>Desktop</abbr></th><th colspan="7"><abbr>Mobile</abbr></th><th colspan="1"><abbr>Server</abbr></th></tr><tr><td></td><th><abbr>Chrome</abbr></th><th><abbr>Edge</abbr></th><th><abbr>Firefox</abbr></th><th><abbr>Internet Explorer</abbr></th><th><abbr>Opera</abbr></th><th><abbr>Safari</abbr></th><th><abbr>Android webview</abbr></th><th><abbr>Chrome for Android</abbr></th><th><abbr>Edge Mobile</abbr></th><th><abbr>Firefox for Android</abbr></th><th><abbr>Opera for Android</abbr></th><th><abbr>iOS Safari</abbr></th><th><abbr>Samsung Internet</abbr></th><th><abbr>Node.js</abbr></th></tr></thead><tbody><tr><th><a href="/docs/Web/JavaScript/Reference/Global_Objects/Int8Array" target="_blank">Basic support</a></th><td><abbr>
                Full support
              </abbr>
              7</td><td><abbr>
                Full support
              </abbr>
              Yes</td><td><abbr>
                Full support
              </abbr>
              4</td><td><abbr>
                Full support
              </abbr>
              10</td><td><abbr>
                Full support
              </abbr>
              11.6</td><td><abbr>
                Full support
              </abbr>
              5.1</td><td><abbr>
                Full support
              </abbr>
              4</td><td><abbr>
                Full support
              </abbr>
              Yes</td><td><abbr>
                Full support
              </abbr>
              Yes</td><td><abbr>
                Full support
              </abbr>
              4</td><td><abbr>
                Full support
              </abbr>
              11.6</td><td><abbr>
                Full support
              </abbr>
              4.2</td><td><abbr>
                ?
              </abbr></td><td><abbr>
                Full support
              </abbr>
              Yes</td></tr><tr><th><code>Int8Array()</code> without <code>new</code> throws</th><td><abbr>
                Full support
              </abbr>
              Yes</td><td><abbr>
                Full support
              </abbr>
              Yes</td><td><abbr>
                Full support
              </abbr>
              44</td><td><abbr>
                No support
              </abbr>
              No</td><td><abbr>
                Full support
              </abbr>
              Yes</td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                Full support
              </abbr>
              44</td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                Full support
              </abbr>
              Yes</td></tr><tr><th>Iterable in constructor</th><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                Full support
              </abbr>
              52</td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                Full support
              </abbr>
              52</td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td></tr><tr><th>Constructor without arguments</th><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                Full support
              </abbr>
              55</td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                Full support
              </abbr>
              55</td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td><td><abbr>
                ?
              </abbr></td></tr></tbody></table><section id="sect1"><h3 id="Legend">Legend</h3><dl><dt>
                <abbr>
                 Full support
                  
                </abbr></dt><dd>Full support</dd><dt>
                <abbr>
                 No support
                  
                </abbr></dt><dd>No support</dd><dt>
                <abbr>
                 Compatibility unknown
                  
                </abbr></dt><dd>Compatibility unknown</dd></dl></section></div>

<h2 id="See_also">See also</h2>


                  
                
              
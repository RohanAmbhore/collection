<a href="http://blog.teamtreehouse.com/reading-files-using-the-html5-filereader-api">http://blog.teamtreehouse.com/reading-files-using-the-html5-filereader-api</a><div id="articleHeader"><h1><small><a href="http://blog.teamtreehouse.com/category/learn" target="_blank">Learn</a></small>Reading Files Using The HTML5 FileReader API</h1></div><br /><br /></section>

  

    

      

        
        <p>HTML5 saw the introduction of a number of new APIs that can be used to handle files in the browser. These APIs make it much easier to accomplish tasks like reading and writing files or uploading a file created using JavaScript.</p>
<p>In this blog post you are going to learn how to use the <a href="https://developer.mozilla.org/en-US/docs/Web/API/FileReader" target="_blank">FileReader</a> API to read the contents of a file from your local hard drive. You will be creating two demo applications. The first application will handle reading and then displaying the contents of a text file. The second will read an image file and then generate a data URL that will be used to display the image on the page.</p>
<p>Let’s get going!</p>
<p><strong>Free trial on Treehouse:</strong> Do you want to learn more about HTML5? <a href="https://teamtreehouse.com/subscribe/plans?cid=2112&utm_source=popular-22282-html5-file-reader-api&trial=yes" target="_blank">Click here to try a free trial on Treehouse</a>.</p>
<h2 id="the-filereader-interface">The FileReader Interface</h2>
<p>The <code>FileReader</code> interface provides a number of methods that can be used to read either <code>File</code> or <code>Blob</code> objects. These methods are all <em>asynchronous</em> which means that your program will not stall whilst a file is being read. This is particularly useful when dealing with large files.</p>
<p>The following code shows how to create a new instance of <code>FileReader</code>.</p>
<pre>var reader = new FileReader();</pre>
<p>In the following sections we are going to take a look at the methods provided by <code>FileReader</code>.</p>
<h3 id="readastext">readAsText()</h3>
<p>The <code>readAsText()</code> method can be used to read text files. This method has two parameters. The first parameter is for the <code>File</code> or <code>Blob</code> object that is to be read. The second parameter is used to specify the encoding of the file. This second parameter is optional. If you don’t specify an encoding <code>UTF-8</code> is assumed by default.</p>
<p>As this is an asynchronous method we need to setup an event listener for when the file has finished loading. When the <code>onload</code> event is called we can examine the <code>result</code> property of our <code>FileReader</code> instance to get the file’s contents. You will need to use this same approach for all of the read methods provided by <code>FileReader</code>.</p>
<pre>var reader = new FileReader();

reader.onload = function(e) {
  var text = reader.result;
}

reader.readAsText(file, encoding);</pre>
<h3 id="readasdataurl">readAsDataURL()</h3>
<p>The <code>readAsDataURL()</code> method takes in a <code>File</code> or <code>Blob</code> and produces a <a href="http://css-tricks.com/data-uris/" target="_blank">data URL</a>. This is basically a base64 encoded string of the file data. You can use this data URL for things like setting the <code>src</code> property for an image. We will look at how to do this later in the images demo.</p>
<pre>var reader = new FileReader();

reader.onload = function(e) {
  var dataURL = reader.result;
}

reader.readAsDataURL(file);</pre>
<h3 id="readasbinarystring">readAsBinaryString()</h3>
<p>The <code>readAsBinaryString()</code> method can be used to read any type of file. The method returns the raw binary data from the file. If you use <code>readAsBinaryString()</code> along with the <code>XMLHttpRequest.sendAsBinary()</code> method you can upload any file to a server using JavaScript.</p>
<pre>var reader = new FileReader();

reader.onload = function(e) {
  var rawData = reader.result;
}

reader.readAsBinaryString(file);</pre>
<h3 id="readasarraybuffer">readAsArrayBuffer()</h3>
<p>The <code>readAsArrayBuffer()</code> method will read a <code>Blob</code> or <code>File</code> object and produce an <a href="https://developer.mozilla.org/en-US/docs/Web/API/ArrayBuffer" target="_blank"><code>ArrayBuffer</code></a>. An <code>ArrayBuffer</code> is a fixed-length binary data buffer. They can come in handy when manipulating files (like converting a JPEG image to PNG).</p>
<pre>var reader = new FileReader();

reader.onload = function(e) {
  var arrayBuffer = reader.result;
}

reader.readAsArrayBuffer(file);</pre>
<h3 id="abort">abort()</h3>
<p>The <code>abort()</code> method will stop a read operation. This can come in handy when reading large files.</p>
<pre>reader.abort();</pre>
<p>Now that you have an understanding of how the <code>FileReader</code> API works lets take a look at a couple of examples.</p>
<h2 id="example-reading-text-files-with-the-file-api">Example: Reading Text Files With The FileReader API</h2>
<div id="attachment_22283"><a href="http://blog.teamtreehouse.com/wp-content/uploads/2013/09/text-file-example.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="http://blog.teamtreehouse.com/wp-content/uploads/2013/09/text-file-example.png" alt="Reading Text Files With The FileReader API" /></div></a><p>Reading Text Files With The FileReader API</p></div>
<p><a href="http://codepen.io/matt-west/full/KjEHg" target="_blank">See the Demo</a> <a href="http://cl.ly/3h2R222J1j47" target="_blank">Download The Code</a> <a href="http://codepen.io/matt-west/pen/KjEHg" target="_blank">View on CodePen</a></p>
<p>In this section you are going to learn how to build a small JavaScript application that reads a text file and displays it’s contents within a <code>&lt;pre&gt;</code> element.</p>
<p>To get started we first need to setup the HTML for our demo. We are going to use a file <code>&lt;input&gt;</code> to handle selecting our file but you could also use <a href="http://blog.teamtreehouse.com/implementing-native-drag-and-drop" target="_blank">drag and drop</a>. We also need to add a <code>&lt;pre&gt;</code> element that will be used for displaying the file’s contents.</p>
<pre>&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="utf-8"&gt;
  &lt;title&gt;File API&lt;/title&gt;

  &lt;link rel="stylesheet" href="style.css"&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;div id="page-wrapper"&gt;

    &lt;h1&gt;Text File Reader&lt;/h1&gt;
    &lt;div&gt;
      Select a text file: 
      &lt;input type="file" id="fileInput"&gt;
    &lt;/div&gt;
    &lt;pre id="fileDisplayArea"&gt;&lt;/pre&gt;

  &lt;/div&gt;

  &lt;script src="text.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>
<p>You can find a copy of the stylesheet used in this demo in the code resources.</p>
<p>Now it’s time to start writing the JavaScript code for your application. Create a new file called <code>text.js</code> to house this code.</p>
<p>First we need to get references to the important elements within our HTML. Here we get references to the file <code>&lt;input&gt;</code> and the <code>&lt;pre&gt;</code> element and store them in variables called <code>fileInput</code> and <code>fileDisplayArea</code>. We also setup an event listener on the <code>fileInput</code> that listens for the <code>change</code> event. This will be fired whenever the user selects a file.</p>
<pre>window.onload = function() {
    var fileInput = document.getElementById('fileInput');
    var fileDisplayArea = document.getElementById('fileDisplayArea');

    fileInput.addEventListener('change', function(e) {
      // Put the rest of the demo code here.
    });
}</pre>
<p>Now we need to write the code that will handle reading the text file. We first fetch the first file from our input by examining the <code>fileInput</code>s <code>files</code> property and store this in a variable called <code>file</code>. We then create another variable called <code>textType</code> that holds a regular expression that we will use later to test that the selected file is indeed a text file.</p>
<pre>var file = fileInput.files[0];
var textType = /text.*/;</pre>
<p>In this next block of code we first check to make sure that the selected file is a text file by testing it’s <code>type</code> property. If the file is not a text file we show a <code>File not supported!</code> message on the page.</p>
<p>Once we have determined that the file type is correct we create a new instance of <code>FileReader</code>. Next we setup an event listener for the <code>onload</code> event. Within this event listener we add some code that will update the <code>innerText</code> property of <code>fileDisplayArea</code> using the <code>result</code> property from our <code>FileReader</code>.</p>
<p>Finally we call the <code>readAsText()</code> method, passing in the <code>file</code> variable that we created earlier.</p>
<pre>if (file.type.match(textType)) {
  var reader = new FileReader();

  reader.onload = function(e) {
    fileDisplayArea.innerText = reader.result;
  }

  reader.readAsText(file);  
} else {
  fileDisplayArea.innerText = "File not supported!";
}</pre>
<p>If you load up the <a href="http://codepen.io/matt-west/full/KjEHg" target="_blank">live demo</a> you should be able to select a file from your local hard drive and see it’s contents displayed on the page.</p>
<h2 id="example-reading-image-files-with-the-file-api">Example: Reading Image Files With The FileReader API</h2>
<div id="attachment_22284"><a href="http://blog.teamtreehouse.com/wp-content/uploads/2013/09/image-file-example.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="http://blog.teamtreehouse.com/wp-content/uploads/2013/09/image-file-example.png" alt="Reading Image Files With The FileReader API" /></div></a><p>Reading Image Files With The FileReader API</p></div>
<p><a href="http://codepen.io/matt-west/full/CfilG" target="_blank">See the Demo</a> <a href="http://cl.ly/3h2R222J1j47" target="_blank">Download The Code</a> <a href="http://codepen.io/matt-west/pen/CfilG" target="_blank">View on CodePen</a></p>
<p>For our next demo we are going to create an application that reads an image file and then displays that image on the page. To do this we are going to be using the <code>readAsDataURL()</code> method.</p>
<p>The HTML markup for this demo is very similar to the HTML we used before. The main difference is that we are now using a <code>&lt;div&gt;</code> element as our <code>fileDisplayArea</code> rather than a <code>&lt;pre&gt;</code>. Note that the name of the JavaScript file has also changed to <code>images.js</code>.</p>
<pre>&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="utf-8"&gt;
  &lt;title&gt;File API&lt;/title&gt;

  &lt;link rel="stylesheet" href="style.css"&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;div id="page-wrapper"&gt;

    &lt;h1&gt;Image File Reader&lt;/h1&gt;
    &lt;div&gt;
      Select an image file: 
      &lt;input type="file" id="fileInput"&gt;
    &lt;/div&gt;
    &lt;div id="fileDisplayArea"&gt;&lt;/div&gt;

  &lt;/div&gt;

  &lt;script src="images.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>
<p>The initial JavaScript code for this demo is exactly the same as before. We get references to the key elements in our HTML and then setup an event listener for the file <code>&lt;input&gt;</code>.</p>
<pre>window.onload = function() {
    var fileInput = document.getElementById('fileInput');
    var fileDisplayArea = document.getElementById('fileDisplayArea');

    fileInput.addEventListener('change', function(e) {
      // Put the rest of the demo code here.
    });
}</pre>
<p>Next we start by fetching the first file from <code>fileInput</code>. We then create the regular expression for checking the file type. This time we want an image file so the regular expression is: <code>/image.*/</code>.</p>
<p>As before, we do a check to make sure that the selected file is indeed an image.</p>
<p>We’re now at the point where things start to get a little different. We start by creating a new instance of <code>FileReader</code> and then setting up an event listener for the <code>onload</code> event.</p>
<p>When this event listener is called we first need to clear out <code>fileDisplayArea</code> just in case there is already an image in there. We can do this by setting <code>fileDisplayArea.innerHTML</code> to an empty string.</p>
<p>Next we create a new <code>Image</code> instance and set it’s <code>src</code> property to the data URL that is generated by <code>readAsDataURL()</code>. Remember, the data URL can be accessed from the <code>FileReader</code>‘s <code>result</code> property. We then add <code>img</code> to the <code>fileDisplayArea</code> using <code>appendChild()</code>.</p>
<p>Finally we issue a call to <code>readAsDataURL()</code> and pass in the selected image file.</p>
<pre>var file = fileInput.files[0];
var imageType = /image.*/;

if (file.type.match(imageType)) {
  var reader = new FileReader();

  reader.onload = function(e) {
    fileDisplayArea.innerHTML = "";

    // Create a new image.
    var img = new Image();
    // Set the img src property using the data URL.
    img.src = reader.result;

    // Add the image to the page.
    fileDisplayArea.appendChild(img);
  }

  reader.readAsDataURL(file); 
} else {
  fileDisplayArea.innerHTML = "File not supported!";
}</pre>
<p>Load up the <a target="_blank">live demo</a> and select a file from your hard drive. You should see that the file is display on the page. If you were to use the browser’s developer tools to examine the <code>&lt;img&gt;</code> element you would see that the <code>src</code> attribute has been set using the data URL for the image you selected.</p>
<h2 id="browser-support-for-the-filereader-api">Browser Support for the FileReader API</h2>
<p>Browser support for the <code>FileReader</code> API is pretty good. The API will work in the latest versions of all the major desktop browsers. It’s worth noting that Internet Explorer only started supporting <code>FileReader</code> in IE10.</p>
<table>
<thead>
<tr>
<th>IE</th>
<th>Firefox</th>
<th>Chrome</th>
<th>Safari</th>
<th>Opera</th>
</tr>
</thead>
<tbody>
<tr>
<td>10+</td>
<td>3.6+</td>
<td>6.0+</td>
<td>6.0+</td>
<td>11.1+</td>
</tr>
</tbody>
</table>
<p>Source: <a href="http://caniuse.com/filereader" target="_blank">http://caniuse.com/filereader</a></p>
<h2 id="final-thoughts">Final Thoughts</h2>
<p>Historically there has been a big divide between the capabilities of a native app and that of an application built with pure web technologies. Whilst I don’t deny that this gap still exists, APIs like <code>FileReader</code> are really helping to close up the divide.</p>
<p>In this post you have learned how to use the <code>FileReader</code> API to read a file from the user’s hard drive and display it’s contents on the page. If you feel like a challenge why not try to create an application that allows the user to drop a file onto the page rather than using an <code>&lt;input&gt;</code> element. My previous post on <a href="http://blog.teamtreehouse.com/implementing-native-drag-and-drop" target="_blank">implementing native drag and drop</a> should help to get you started.</p>
<h2 id="useful-links">Useful Links</h2>


        
      
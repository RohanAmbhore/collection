<a href="https://coligo.io/building-ajax-file-uploader-with-node/">https://coligo.io/building-ajax-file-uploader-with-node/</a><div id="articleHeader"><h1>Building a File Uploader with NodeJs</h1></div>
<p>Whether you're building a blog, image gallery, dashboard, file host, etc.. chances are you'll be needing a way to upload files via your web application. In this tutorial we'll be looking at how to build a file uploader that uses AJAX. It will consist of a simple HTML + JavaScript front end to allow the user to select multiple files at once and a NodeJS backend to handle the file upload sent via the HTML form.</p>
<p>The AJAX requests allow us to upload multiple files and display their progress without having to reload the page or navigate away from it.</p>
<p>We will be using a NodeJS module called <a href="https://github.com/felixge/node-formidable" target="_blank">formidable</a> which is a fast, easy to use, and well-tested form data parser. It is also capable of handling multiple file uploads in the same request which is perfect for our purposes.</p>
<p>If you haven't had a chance to check out the <a href="https://coligo-uploader.herokuapp.com/" target="_blank">demo</a> yet, here's what the front end of our file uploader is going to look like:</p>
<p><div class="readableLargeImageContainer"><img src="file-uploader-demo.png" alt="file uploader demo" /></div></p>
<h1 id="setting-up-the-project">Setting Up the Project</h1>
<p>Let's get started by setting up the NodeJS project and installing the necessary modules we'll be using in our application.</p>
<p>The folder structure for our project will look like this:</p>
<p><div class="readableLargeImageContainer"><img src="folder-structure.png" alt="file uploader project structure" /></div></p>
<ul>
<li><em>node_modules/</em> contains our NodeJS module dependencies</li>
<li><em>public/</em> contains the javascript and css for our front end</li>
<li><em>uploads/</em> will be where we upload the files</li>
<li><em>views/</em> contains the HTML templates we will serve up to visitors</li>
<li><em>app.js</em> will have the routes and main logic for our back end</li>
<li><em>package.json</em> has general information about our project and it's dependencies</li>
</ul>
<p>Go ahead and create the root directory for our project, in this case I named it <em>file-uploader</em>. We can now <code>cd</code> into that directory and run <code>npm init</code> and follow the prompts to create the <em>package.json</em> file.</p>
<p>Now that we have the <em>package.json</em> created, let's install our dependencies:</p>
<ul>
<li><em>express</em>: to handle the routes and serve up the HTML, CSS, and JS files</li>
<li><em>formidable</em>: to parse the incoming form data containing the file uploads</li>
</ul>
<p>The command to install the dependencies via NPM:</p>
<pre><code>npm install express formidable --save
</code></pre><p>You should now see the <em>node_modules</em> directory with express and formidable in your project folder.</p>
<p>Note: if you're using NPM version 3 or later, you might not see a separate directory for each dependency. NPM version 3 got rid of nested dependencies, meaning express and formidable will be installed in the root of the node_modules folder along with all the modules they depend on.</p>
<h1 id="the-front-end">The Front End</h1>
<p>The HTML and CSS for our front end are relatively simple. It uses <a href="http://getbootstrap.com" target="_blank">Twitter Bootstrap</a> for some basic aesthetics and responsiveness.</p>
<p>Create a file in the <em>views/</em> directory and call it <strong>index.html</strong>. This contains the basic page structure and most importantly our <strong>HTML file input</strong>.</p>
<pre><code>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
  &lt;meta charset="utf-8"&gt;
  &lt;meta http-equiv="X-UA-Compatible" content="IE=edge"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1"&gt;

  &lt;title&gt;File Uploader - coligo.io&lt;/title&gt;
  &lt;link href='https://fonts.googleapis.com/css?family=Raleway' rel='stylesheet' type='text/css'&gt;
  &lt;link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css"&gt;
  &lt;link href="css/styles.css" rel="stylesheet"&gt;
&lt;/head&gt;
&lt;body&gt;

  &lt;div class="container"&gt;
    &lt;div class="row"&gt;
      &lt;div class="col-xs-12"&gt;
        &lt;div class="panel panel-default"&gt;
          &lt;div class="panel-body"&gt;
            &lt;span class="glyphicon glyphicon-cloud-upload"&gt;&lt;/span&gt;
            &lt;h2&gt;File Uploader&lt;/h2&gt;
            &lt;h4&gt;coligo.io&lt;/h4&gt;
            &lt;div class="progress"&gt;
              &lt;div class="progress-bar" role="progressbar"&gt;&lt;/div&gt;
            &lt;/div&gt;
            &lt;button class="btn btn-lg upload-btn" type="button"&gt;Upload File&lt;/button&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;

  &lt;input id="upload-input" type="file" name="uploads[]" multiple="multiple"&gt;&lt;/br&gt;

  &lt;script src="https://code.jquery.com/jquery-2.2.0.min.js"&gt;&lt;/script&gt;
  &lt;script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js"&gt;&lt;/script&gt;
  &lt;script src="javascripts/upload.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>
<p>We won't go into details about each line of HTML in here since it's mostly just basic HTML and Bootstrap classes. Instead, let's focus specifically on the HTML file input:</p>
<pre><code>&lt;input id="upload-input" type="file" name="uploads[]" multiple="multiple"&gt;
</code></pre>
<p><code>type="file"</code> will give us a file-select field and a browse button to select the file we wish to upload, which doesn't look too fancy but does the job:</p>
<p><img src="file-input-box.png" alt="HTML file input box" /></p>
<p>The <code>multiple</code> attribute allows the user to select multiple files from the file picker dialog at once. You can change it to allow only one file at a time by removing that attribute.</p>
<p>As you can see from the demo, that plain looking file input does not show up, instead we are using the orange upload button to make it look more appealing. We will hide this file input element by adding this property to the CSS:</p>
<pre><code>#upload-input {
  display: none;
}
</code></pre>
<p>And we will later add the logic to the JavaScript such that each time the user clicks on the orange upload button, it triggers the hidden file input box to bring up the file picker dialog.</p>
<p>Create the CSS file under <em>public/css/</em> and call it <strong>styles.css</strong>:</p>
<pre><code>.btn:focus, .upload-btn:focus{
  outline: 0 !important;
}

html,
body {
  height: 100%;
  background-color: #4791D2;
}

body {
  text-align: center;
  font-family: 'Raleway', sans-serif;
}

.row {
  margin-top: 80px;
}

.upload-btn {
  color: #ffffff;
  background-color: #F89406;
  border: none;
}

.upload-btn:hover,
.upload-btn:focus,
.upload-btn:active,
.upload-btn.active {
  color: #ffffff;
  background-color: #FA8900;
  border: none;
}

h4 {
  padding-bottom: 30px;
  color: #B8BDC1;
}

.glyphicon {
  font-size: 5em;
  color: #9CA3A9;
}

h2 {
  margin-top: 15px;
  color: #68757E;
}

.panel {
  padding-top: 20px;
  padding-bottom: 20px;
}

#upload-input {
  display: none;
}

@media (min-width: 768px) {
  .main-container {
    width: 100%;
  }
}

@media (min-width: 992px) {
  .container {
    width: 450px;
  }
}
</code></pre>
<p>You should now have a basic, styled HTML page with an upload button and a progress bar. Let's jump into the JavaScript an add some logic to our front end such as handling the clicks on the upload button and making AJAX requests to the server.</p>
<p>Create a file call <strong>upload.js</strong> under the <em>public/javascripts/</em> directory to house this logic.</p>
<p>First things first, let's get the upload button working so that each time the user clicks on the big orange upload button, it automatically triggers that hidden file input. jQuery makes this quite straight forward by assigning a <em>click</em> listener to the upload button and triggering a click event on the file input.</p>
<pre><code>$('.upload-btn').on('click', function (){
    $('#upload-input').click();
});
</code></pre>
<p>We also want to reset the progress bar to 0% each time a user attempts to select a new set of files for upload:</p>
<pre><code>$('.upload-btn').on('click', function (){
    $('#upload-input').click();
    $('.progress-bar').text('0%');
    $('.progress-bar').width('0%');
});
</code></pre>
<p>Now for the actual file uploading logic! We want to listen to the file input for a change event. This will tell us that the user clicked the upload button and selected a file or hit cancel. As soon as a change event is triggered, we want to verify that one or more files were actually selected to ensure that the user didn't hit cancel.</p>
<pre><code>$('#upload-input').on('change', function(){

  var files = $(this).get(0).files;

  if (files.length &gt; 0){
    // One or more files selected, process the file upload
  }

});
</code></pre>
<p><code>files</code> is an array containing all the files selected by the user</p>
<p>We now need to create and populate a FormData object which is basically a set of key/value pairs representing form fields and their values. Once constructed, we can send this FormData object with our AJAX request to the server.</p>
<pre><code>$('#upload-input').on('change', function(){

  var files = $(this).get(0).files;

  if (files.length &gt; 0){
    // One or more files selected, process the file upload

    // create a FormData object which will be sent as the data payload in the
    // AJAX request
    var formData = new FormData();

    // loop through all the selected files
    for (var i = 0; i &lt; files.length; i++) {
      var file = files[i];

      // add the files to formData object for the data payload
      formData.append('uploads[]', file, file.name);
    }

  }

});
</code></pre>
<p>After we've verified that the user has selected one or more files and added them to the FormData object, we can create the AJAX request that will POST the data to our <em>/upload</em> endpoint:</p>
<pre><code>$.ajax({
  url: '/upload',
  type: 'POST',
  data: formData,
  processData: false,
  contentType: false,
  success: function(data){
      console.log('upload successful!');
  }
});
</code></pre>
<ul>
<li>The data we are sending is the formData object we constructed</li>
<li>Setting <code>contentType</code> to false tells jQuery not to add a <code>Content-Type</code> header for us</li>
<li>Setting <code>processData</code> to false stops jQuery from attempting to convert the <code>formData</code> object to a string</li>
</ul>
<p>We've successfully created the font end logic that will handle selecting multiple files and POSTing the data to the server via an AJAX request. The last thing we need to do for the front end is add the logic to update the progress bar which is done via the <code>xhr</code> option in the jQuery AJAX call:</p>
<pre><code>xhr: function() {
  // create an XMLHttpRequest
  var xhr = new XMLHttpRequest();

  // listen to the 'progress' event
  xhr.upload.addEventListener('progress', function(evt) {

    if (evt.lengthComputable) {
      // calculate the percentage of upload completed
      var percentComplete = evt.loaded / evt.total;
      percentComplete = parseInt(percentComplete * 100);

      // update the Bootstrap progress bar with the new percentage
      $('.progress-bar').text(percentComplete + '%');
      $('.progress-bar').width(percentComplete + '%');

      // once the upload reaches 100%, set the progress bar text to done
      if (percentComplete === 100) {
        $('.progress-bar').html('Done');
      }

    }

  }, false);

  return xhr;
}
</code></pre>
<p>Our complete <strong>upload.js</strong> file now looks like so:</p>
<pre><code>$('.upload-btn').on('click', function (){
    $('#upload-input').click();
    $('.progress-bar').text('0%');
    $('.progress-bar').width('0%');
});

$('#upload-input').on('change', function(){

  var files = $(this).get(0).files;

  if (files.length &gt; 0){
    // create a FormData object which will be sent as the data payload in the
    // AJAX request
    var formData = new FormData();

    // loop through all the selected files and add them to the formData object
    for (var i = 0; i &lt; files.length; i++) {
      var file = files[i];

      // add the files to formData object for the data payload
      formData.append('uploads[]', file, file.name);
    }

    $.ajax({
      url: '/upload',
      type: 'POST',
      data: formData,
      processData: false,
      contentType: false,
      success: function(data){
          console.log('upload successful!\n' + data);
      },
      xhr: function() {
        // create an XMLHttpRequest
        var xhr = new XMLHttpRequest();

        // listen to the 'progress' event
        xhr.upload.addEventListener('progress', function(evt) {

          if (evt.lengthComputable) {
            // calculate the percentage of upload completed
            var percentComplete = evt.loaded / evt.total;
            percentComplete = parseInt(percentComplete * 100);

            // update the Bootstrap progress bar with the new percentage
            $('.progress-bar').text(percentComplete + '%');
            $('.progress-bar').width(percentComplete + '%');

            // once the upload reaches 100%, set the progress bar text to done
            if (percentComplete === 100) {
              $('.progress-bar').html('Done');
            }

          }

        }, false);

        return xhr;
      }
    });

  }
});
</code></pre>
<h1 id="the-back-end-processing-the-upload">The Back End: Processing the Upload</h1>
<p>We've successfully setup a front end through which the user can select multiple files to upload and monitor their progress through a simple progress bar. In this section we will be focusing on the NodeJS backend to process incoming requests to our upload route.</p>
<p>We will add all the backend logic and upload handling to the <strong>app.js</strong> file in the root of our project folder.</p>
<p>Let's start off by requiring all the modules needed for the file uploader:</p>
<pre><code>var express = require('express');
var app = express();
var path = require('path');
var formidable = require('formidable');
var fs = require('fs');
</code></pre>
<ul>
<li><code>express</code> handles our routing and serves up the index.html page and static files to our visitors</li>
<li><code>formidable</code> will parse the incoming form data (the uploaded files)</li>
<li>The <code>fs</code> module will be used to rename uploaded files</li>
</ul>
<p>We'll use the <code>express.static</code> middleware to serve up the static files in our <em>public/</em> directory and we'll create a route which will serve up the homepage (index.html) when someone visits the website:</p>
<pre><code>app.use(express.static(path.join(__dirname, 'public')));

app.get('/', function(req, res){
  res.sendFile(path.join(__dirname, 'views/index.html'));
});
</code></pre>
<p>Create the <em>upload/</em> route to handle the incoming uploads via the POST method:</p>
<pre><code>app.post('/upload', function(req, res){

  // create an incoming form object
  var form = new formidable.IncomingForm();

  // specify that we want to allow the user to upload multiple files in a single request
  form.multiples = true;

  // store all uploads in the /uploads directory
  form.uploadDir = path.join(__dirname, '/uploads');

  // every time a file has been uploaded successfully,
  // rename it to it's orignal name
  form.on('file', function(field, file) {
    fs.rename(file.path, path.join(form.uploadDir, file.name));
  });

  // log any errors that occur
  form.on('error', function(err) {
    console.log('An error has occured: \n' + err);
  });

  // once all the files have been uploaded, send a response to the client
  form.on('end', function() {
    res.end('success');
  });

  // parse the incoming request containing the form data
  form.parse(req);

});
</code></pre>
<p>Now that we have everything set up and the route to handle the uploads in place, all we need to do it start our NodeJS server and start processing uploads!</p>
<pre><code>var server = app.listen(3000, function(){
  console.log('Server listening on port 3000');
});
</code></pre>
<p>Our full <strong>app.js</strong> file now looks like so:</p>
<pre><code>var express = require('express');
var app = express();
var path = require('path');
var formidable = require('formidable');
var fs = require('fs');

app.use(express.static(path.join(__dirname, 'public')));

app.get('/', function(req, res){
  res.sendFile(path.join(__dirname, 'views/index.html'));
});

app.post('/upload', function(req, res){

  // create an incoming form object
  var form = new formidable.IncomingForm();

  // specify that we want to allow the user to upload multiple files in a single request
  form.multiples = true;

  // store all uploads in the /uploads directory
  form.uploadDir = path.join(__dirname, '/uploads');

  // every time a file has been uploaded successfully,
  // rename it to it's orignal name
  form.on('file', function(field, file) {
    fs.rename(file.path, path.join(form.uploadDir, file.name));
  });

  // log any errors that occur
  form.on('error', function(err) {
    console.log('An error has occured: \n' + err);
  });

  // once all the files have been uploaded, send a response to the client
  form.on('end', function() {
    res.end('success');
  });

  // parse the incoming request containing the form data
  form.parse(req);

});

var server = app.listen(3000, function(){
  console.log('Server listening on port 3000');
});
</code></pre>
<p>You can now start the server by typing <code>node app.js</code> in your console and navigate to <code>http://localhost:3000</code> in your browser to test out the file uploader for yourself!</p>
<h1 id="conclusion">Conclusion</h1>
<p>We covered how to create an AJAX file uploader using NodeJs as our backend and a simple HTML + JavaScript front end. Remember that you can always swap out the NodeJs for any other backend like PHP, Python, Ruby, etc... and still keep the same front end logic.</p>
<p>Also, be sure to checkout the full working <a href="https://github.com/coligo-io/file-uploader" target="_blank">code for this tutorial</a> on GitHub if you'd like to integrate it into your own website or application using the concepts we learned.</p>

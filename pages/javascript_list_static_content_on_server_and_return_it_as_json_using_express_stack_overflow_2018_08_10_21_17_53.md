<a href="https://stackoverflow.com/questions/30752115/list-static-content-on-server-and-return-it-as-json-using-express">https://stackoverflow.com/questions/30752115/list-static-content-on-server-and-return-it-as-json-using-express</a><div id="articleHeader"><h1>List static content on server and return it as JSON using Express</h1></div>

            

<div id="question">

    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        1
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>2</b></div>



</div>

            </div>

            
<div>
    <div>

<p>I have a very simple app serving static files:</p>

<pre><code>var express = require('express');
var app = express();
app.use(express.static(__dirname + '/files'));
app.listen(process.env.PORT || 8080);</code></pre>

<p>I'd like to make this app slightly smarter by responding to GET for <strong>folders</strong>. I mean, to <strong>list the full list of files of the folder, in a JSON</strong>.</p>

<p>For instance, for a GET at <code>localhost:8080/</code>, I would like the app to return:</p>

<pre><code>[{
  "type" : "file",
  "name" : "file1.ext"
},
{
  "type" : "file",
  "name" : "file2.ext"
},
{
  "type" : "dir",
  "name" : "a-folder"
}]</code></pre>

<p>instead of:</p>

<pre><code>Cannot GET /</code></pre>

<p>Is there a way to extend Express's static behaviour to achieve this?
If not, what approach would you recommend?</p>

<p><strong>EDIT</strong>: I tried to use the <code>serve-index</code> middleware (formerly <code>directory</code>), which works well but unfortunately returns directly html, when I need raw JSON.</p>
    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-30752244">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted


</div>

            </div>
            


<div>
    <div>
<p>As said in <a href="http://expressjs.com/starter/static-files.html" target="_blank">http://expressjs.com/starter/static-files.html</a></p>

<p>You need to use express.static:</p>

<pre><code>var express = require('express');
var app = express();
app.use("/files",express.static('files'));
app.listen(process.env.PORT || 8080);</code></pre>

<p>Then you will be able to access the files as: </p>

<pre><code>http://yourdomain.com/files/file.jpg</code></pre>

<p><strong>EDIT</strong> I just realized, you need the list of files in the dir.</p>



<p>There you have the answers, then, I´ll mark as duplicate</p>

<p>As commented <a href="https://stackoverflow.com/a/25580289/3617531" target="_blank">here</a>, maybe installing node utility glob (<code>npm install glob</code>), and code some express function for GET in <code>/files</code> dir this way:</p>

<pre><code>var express = require('express');
var app = express();
var glob = require("glob")


//EDIT: As you commented, you should add this also here, to allow 
//  accessing the files inside the dir. It should not be a problem as 
//  GET only manages the requests to "/files" url, without a file name    
//  after it.

app.use("/files", express.static("/files"));

app.get('/files', function (req, res) {

//EDIT: USE WALK INSTEAD OF WALK TO GO UNDER CHILD DIRS
glob("*.ext", options, function (er, files) {
  // files is an array of filenames.
  // If the `nonull` option is set, and nothing
  // was found, then files is ["**/*.js"]
  // er is an error object or null.
  res.send(files);
});


});

var server = app.listen(8080, function () {

  var host = server.address().address;
  var port = server.address().port;

  console.log('Example app listening at http://%s:%s', host, port);

});</code></pre>

<p><strong>WALK MODE: (FOR SUBDIRS, AS REQUIRED)</strong></p>

<pre><code>var express = require('express');
var app = express();
var walk    = require('walk');
var ALLfiles   = [];

app.use("/files", express.static("/files"));

app.get('/files', function (req, res) {

//EDIT: If you need to go under subdirs: change glob to walk as said in https://stackoverflow.com/questions/2727167/getting-all-filenames-in-a-directory-with-node-js/25580289#25580289
  var walker  = walk.walk('./files', { followLinks: false });
   walker.on('file', function(root, stat, next) {
       // Add this file to the list of files
       ALLfiles.push(root + '/' + stat.name);
       next();
   });

   walker.on('end', function() {
    res.send(ALLfiles);
   });

});

var server = app.listen(8080, function () {

  var host = server.address().address;
  var port = server.address().port;

  console.log('Example app listening at http://%s:%s', host, port);

});</code></pre>
    </div>
    
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/node.js" title="show questions tagged 'node.js'" target="_blank">node.js</a> <a href="/questions/tagged/express" title="show questions tagged 'express'" target="_blank">express</a> <a href="/questions/tagged/fs" title="show questions tagged 'fs'" target="_blank">fs</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="https://stackoverflow.com/questions/17510979/how-to-add-multiple-files-to-a-zip-with-zip-js">https://stackoverflow.com/questions/17510979/how-to-add-multiple-files-to-a-zip-with-zip-js</a><div id="articleHeader"><h1>How to add multiple files to a zip with zip.js?</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        6
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>5</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I am using the javascript <a href="http://gildas-lormeau.github.io/zip.js/" target="_blank">zip.js</a> library. I've seach all around I a cannot find an example where more than one file is added to the zip.</p>

<p>Here is my code, but it generates a "corrupted" zip.</p>

<pre><code>var len = results.rows.length, i;
var k=1;
zip.createWriter(new zip.BlobWriter(), function(writer) {
    for (i = 0; i &lt; len; i++){
        // get the image url from a sqlite request
        url = results.rows.item(i).url;


        var img = new Image();
        img.onload = function() {
            var a = document.createElement('a');
            a.href = this.src;
            var filename= a.pathname.split('/').pop(); // filename.php
            timest = new Date().getTime();
            // use a TextReader to read the String to add

                writer.add(timest+".jpg", new zip.Data64URIReader(getBase64Image(img)), function() {
                // onsuccess callback
                    k++;
                    if(k==len){
                        setTimeout(function(){
                        writer.close(function(blob) {

                            // blob contains the zip file as a Blob object
                            $('#test').attr("href", window.URL.createObjectURL(blob));
                            $('#test').attr("download", "woeii.zip");

                        });
                        },1000);
                    }
                }, function(currentIndex, totalIndex) {
                // onprogress callback
                });



        };
        img.src = url;
    }
});</code></pre>

<p>Any idea to make it work? :)</p>
    </div>
    
    <div>
    

    <div>
        <div>
    <div>
        asked Jul 7 '13 at 9:47
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-17511338">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>If you are looking for a good example of code that handles multiple files, <a href="http://gildas-lormeau.github.io/zip.js/demos/demo1.html" target="_blank">see here</a>. You can then <a href="http://gildas-lormeau.github.io/zip.js/demos/demo1.js" target="_blank">view the source code</a>.</p>

<p>This is the key source of the demo (modified just slightly):</p>

<pre><code>var obj = this;
var model = (function() {
    var zipFileEntry, zipWriter, writer, creationMethod, URL = obj.webkitURL || obj.mozURL || obj.URL;

    return {
        setCreationMethod : function(method) {
            creationMethod = method;
        },
        addFiles : function addFiles(files, oninit, onadd, onprogress, onend) {
            var addIndex = 0;

            function nextFile() {
                var file = files[addIndex];
                onadd(file);
                // Modified here to use the Data64URIReader instead of BlobReader
                zipWriter.add(file.name, new zip.Data64URIReader(file.data), function() {
                    addIndex++;
                    if (addIndex &lt; files.length)
                        nextFile();
                    else
                        onend();
                }, onprogress);
            }

            function createZipWriter() {
                zip.createWriter(writer, function(writer) {
                    zipWriter = writer;
                    oninit();
                    nextFile();
                }, onerror);
            }

            if (zipWriter)
                nextFile();
            else if (creationMethod == "Blob") {
                writer = new zip.BlobWriter();
                createZipWriter();
            } else {
                createTempFile(function(fileEntry) {
                    zipFileEntry = fileEntry;
                    writer = new zip.FileWriter(zipFileEntry);
                    createZipWriter();
                });
            }
        },
        getBlobURL : function(callback) {
            zipWriter.close(function(blob) {
                var blobURL = creationMethod == "Blob" ? URL.createObjectURL(blob) : zipFileEntry.toURL();
                callback(blobURL);
                zipWriter = null;
            });
        },
        getBlob : function(callback) {
            zipWriter.close(callback);
        }
    };
})();</code></pre>

<p>Usage:
Assumes a <code>&lt;a id="downloadLink"&gt;Download&lt;/a&gt;</code> element exists to provide the download once ready.</p>

<pre><code>// Prepare your images
var files = [];
for (i = 0; i &lt; len; i++) {

    // Get the image URL from a SQLite request
    var url = results.rows.item(i).url;

    (function(url){
        var img = new Image();
        img.onload = function() {
            // Add to file array [{name, data}]
            var a = document.createElement('a');
            a.href = this.src;
            var filename= a.pathname.split('/').pop();

            console.log("Loaded file " + filename);
            files.push({name: filename, data: getBase64Image(img) });
        }
        img.src = url;
    })(url);
}

// Wait for the image to load
var check = setInterval(function(){
    if(files.length==images.length) {
        clearInterval(check);

        // Set the mode
        model.setCreationMethod("Blob");

        // Add the files to the zip
        model.addFiles(files, 
            function() {
                // Initialise Method
                console.log("Initialise");
            }, function(file) {
                // OnAdd
                console.log("Added file");
            }, function(current, total) {
                // OnProgress
                console.log("%s %s", current, total);
            }, function() {
                // OnEnd
                // The zip is ready prepare download link
                // &lt;a id="downloadLink" href="blob:url"&gt;Download Zip&lt;/a&gt;
                model.getBlobURL(function(url) {
                    document.getElementById("downloadLink").href = url;
                    document.getElementById("downloadLink").style.display = "block";
                    document.getElementById("downloadLink").download = "filename.zip";
                });
            });

    }
}, 500);</code></pre>

<p>You can use the example source code to add in progress indicators.
Hope this helps, the nice thing about this method is the zip model is easily reusable if you make it it's own JS file.</p>

<hr />

<p>Another thought: I presume you are using the <code>getBase64Image</code> function <a href="https://stackoverflow.com/questions/934012/get-image-data-in-javascript" target="_blank">from here</a>, if so and you still experience corruption issues, perhaps try modifying the return to simply <code>return dataURL;</code> and comment out the <code>.replace(...</code>, as the <code>Data64URIReader</code> may expect the prefix.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-29737025">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Here's a stripped-down version of <a href="http://gildas-lormeau.github.io/zip.js/demos/demo1.html" target="_blank">that demo</a> that only uses RAM storage. It assumes that zip.js, z-worker.js, and deflate.js from the zip.js install are in the same directory as the two files below, along with <a href="https://github.com/eligrey/FileSaver.js/" target="_blank">FileSaver.js</a>.</p>

<p><em>Note:</em> This is not production-ready code! It is a bare-bones demo that I made so I could figure out what was going on. If you generate and save the zip programmatically, you may need to implement a nextFile() iterator like the one above to prevent a race condition from populating the zip with empty files. (See <a href="https://stackoverflow.com/a/29738675/738675" target="_blank">https://stackoverflow.com/a/29738675/738675</a> for an example of this.)</p>

<p><strong>demo.html:</strong></p>

<pre><code>&lt;li&gt;
    add files into the zip
    &lt;input type="file" multiple id="file-input" onchange="addFiles(this.files)"&gt;
&lt;/li&gt;
&lt;li&gt;
    download the zip file
    &lt;a href="#" onclick="saveZip()"&gt;Download&lt;/a&gt;
&lt;/li&gt;

&lt;script type="text/javascript" src="zip.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="demo.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="FileSaver.js"&gt;&lt;/script&gt;</code></pre>

<p><strong>demo.js:</strong></p>

<pre><code>var zipWriter;

function addFiles(files) {
    writer = new zip.BlobWriter();
    zip.createWriter(writer, function(writer) {
        zipWriter = writer;
        for (var f = 0; f &lt; files.length; f++) {
            zipWriter.add(files[f].name,
            new zip.BlobReader(files[f]), function() {});
        }
    });
}

function saveZip() {
    zipWriter.close(function(blob) {
        saveAs(blob, "Example.zip"); // uses FileSaver.js
        document.getElementById("file-input").value = null; // reset input file list
        zipWriter = null;
    });
}</code></pre>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/zip" title="show questions tagged 'zip'" target="_blank">zip</a> <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
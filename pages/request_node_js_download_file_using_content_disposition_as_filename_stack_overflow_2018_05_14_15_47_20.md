<a href="https://stackoverflow.com/questions/20132064/node-js-download-file-using-content-disposition-as-filename">https://stackoverflow.com/questions/20132064/node-js-download-file-using-content-disposition-as-filename</a><div id="articleHeader"><h1>Node.js Download File Using Content Disposition as Filename</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        16
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>5</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I'm using the Request module to download files, but I'm not quite sure how to pipe the response to an output stream when the filename must come from the 'Content-Disposition' header. So basically, I need to read the response until the header is found, and then pipe the rest to that filename.</p>

<p>The examples show something like:</p>

<p><code>request('http://google.com/doodle.png').pipe(fs.createWriteStream('doodle.png'));</code></p>

<p>Where I want to do (pseudocode):</p>

<pre><code>var req = request('http://example.com/download_latest_version?token=XXX');
var filename = req.response.headers['Content-Disposition'];

req.pipe(fs.createWriteStream(filename));</code></pre>

<p>I could get the filename using the Request callback:</p>

<pre><code>request(url, function(err, res, body) {
 // get res headers here
});</code></pre>

<p>But wouldn't that negate the benefits of using pipe and not loading the downloaded file into memory?</p>
    </div>
    
    <div>
    

    <div>
        <div>
    <div>
        asked Nov 21 '13 at 21:18
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-20133385">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        24
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>I'm reqesting a image from yahoo and it isn't using the <code>content-disposition</code> header but I am extracting the <code>date</code> and <code>content-type</code> headers to construct a filename. This seems close enough to what you're trying to do...</p>

<pre><code>var request = require('request'),
fs = require('fs');

var url2 = 'http://l4.yimg.com/nn/fp/rsz/112113/images/smush/aaroncarter_635x250_1385060042.jpg';

var r = request(url2);

r.on('response',  function (res) {
  res.pipe(fs.createWriteStream('./' + res.headers.date + '.' + res.headers['content-type'].split('/')[1]));

});</code></pre>

<p>Ignore my image choice please :)</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Nov 21 '13 at 22:36
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-28141320">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        9
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Question has been around a while, but I today faced the same problem and solved it differently:</p>

<pre><code>var Request = require( 'request' ),
    Fs = require( 'fs' );

// RegExp to extract the filename from Content-Disposition
var regexp = /filename=\"(.*)\"/gi;

// initiate the download
var req = Request.get( 'url.to/somewhere' )
                 .on( 'response', function( res ){

                    // extract filename
                    var filename = regexp.exec( res.headers['content-disposition'] )[1];

                    // create file write stream
                    var fws = Fs.createWriteStream( '/some/path/' + filename );

                    // setup piping
                    res.pipe( fws );

                    res.on( 'end', function(){
                      // go on with processing
                    });
                 });</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-38513408">
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
<p>Here's my solution:</p>

<pre><code>var fs = require('fs');
var request = require('request');
var through2 = require('through2');

var req = request(url);
req.on('error', function (e) {
    // Handle connection errors
    console.log(e);
});
var bufferedResponse = req.pipe(through2(function (chunk, enc, callback) {
    this.push(chunk);
    callback()
}));
req.on('response', function (res) {
    if (res.statusCode === 200) {
        try {
            var contentDisposition = res.headers['content-disposition'];
            var match = contentDisposition && contentDisposition.match(/(filename=|filename\*='')(.*)$/);
            var filename = match && match[2] || 'default-filename.out';
            var dest = fs.createWriteStream(filename);
            dest.on('error', function (e) {
                // Handle write errors
                console.log(e);
            });
            dest.on('finish', function () {
                // The file has been downloaded
                console.log('Downloaded ' + filename);
            });
            bufferedResponse.pipe(dest);
        } catch (e) {
            // Handle request errors
            console.log(e);
        }
    }
    else {
        // Handle HTTP server errors
        console.log(res.statusCode);
    }
});</code></pre>

<p>The other solutions posted here use <code>res.pipe</code>, which can fail if the content is transferred using <code>gzip</code> encoding, because the response stream contains the raw (compressed) HTTP data. To avoid this problem you have to use <code>request.pipe</code> instead. (See the second example at <a href="https://github.com/request/request#examples" target="_blank">https://github.com/request/request#examples</a>.)</p>

<p>When using <code>request.pipe</code> I was getting an error: "You cannot pipe after data has been emitted from the response.", because I was doing some async stuff before actually piping (creating a directory to hold the downloaded file). I also had some problems where the file was being written with no content, which might have been due to <code>request</code> reading the HTTP response and buffering it.</p>

<p>So I ended up creating an intermediate buffering stream with <code>through2</code>, so that I could pipe the request to it before the response handler fires, then later piping from the buffering stream into the file stream once the filename is known.</p>

<p>Finally, I'm parsing the content disposition header whether the filename is encoded in plain form or in UTF-8 form using the <code>filename*=''file.txt</code> syntax.</p>

<p>I hope this helps someone else who experiences the same issues that I had.</p>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/node.js" title="show questions tagged 'node.js'" target="_blank">node.js</a> <a href="/questions/tagged/request" title="show questions tagged 'request'" target="_blank">request</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
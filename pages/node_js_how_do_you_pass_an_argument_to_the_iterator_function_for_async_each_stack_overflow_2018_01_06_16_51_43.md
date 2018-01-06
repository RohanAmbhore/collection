<a href="https://stackoverflow.com/questions/16990160/how-do-you-pass-an-argument-to-the-iterator-function-for-async-each">https://stackoverflow.com/questions/16990160/how-do-you-pass-an-argument-to-the-iterator-function-for-async-each</a><div id="articleHeader"><h1>How do you pass an argument to the iterator function for async.each?</h1></div>

<p>I can't for the life of me find the answer to this.  How do you pass a parameter to the iterator function for async.each using caolan's async.js node module?  I want to reuse the iterator but it needs to save things with a different prefix based on the context.  What I've got is:</p>

<pre><code>async.each(myArray, urlToS3, function(err){
    if(err) {
       console.log('async each failed for myArray');
    } else {
        nextFunction(err, function(){
            console.log('successfully saved myArray');
            res.send(200);
        });
    }
});

function urlToS3(url2fetch, cb){
    //get the file and save it to s3
}</code></pre>

<p>What I'd like to be able to do is: </p>

<pre><code>    async.each(myArray, urlToS3("image"), function(err){
    if(err) {
       console.log('async each failed for myArray');
    } else {
        nextFunction(err, function(){
            console.log('successfully saved myArray');
            res.send(200);
        });
    }
});

function urlToS3(url2fetch, fileType, cb){
    if (fileType === "image") {
    //get the file and save it to s3 with _image prefix
    }
}</code></pre>

<p>I found something one similar question for coffeescript but the answer didn't work.  I'm open to refactoring in case i'm trying to do something that is just not idiomatic, but this seems like such a logical thing to do. </p>
    
<a href="https://github.com/request/request-promise/issues/171">https://github.com/request/request-promise/issues/171</a><div id="articleHeader"><h1>              How to save downloaded binary data without using pipe            #171    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/Aranir" target="_blank">Aranir</a>  opened this Issue
        <relative-time>on Jan 20, 2017</relative-time>
        · 5 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            





            
  <div id="issue-201940132">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>On my node server and try to download a png image from a url and write it to a file:</p>
<pre><code>  request
.get("https://url/for/png/file")
.on('error', function(err) {
  console.log(err)
})
.on('response', function(response){
  console.log(response.statusCode) // 200
  console.log(response.headers['content-type']); // 'image/png'
})
.on('complete', (resp: http.IncomingMessage, body: string | Buffer) =&gt; {
  fs.writeFile(".../test.png", body, 'binary');

});
</code></pre>
<p>The main issue is that the written file is corrupted (can't be opened).</p>
<p>If I use pipe instead of on('complete'...) at the end the written file is correct.</p>
<pre><code>.pipe(fs.createWriteStream(".../test.png"))
</code></pre>
<p>What exactly is the difference and what am I missing to be able to write the file?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  

          

          

  
  


  
<div>
    
<div>
  





  
  <div id="issuecomment-273873128">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Hi <a href="https://github.com/aranir" target="_blank">@Aranir</a> , please do not use <code>request-promise</code> for streaming the response. See the first bullet point <a href="https://github.com/request/request-promise#api-in-detail" target="_blank">here</a> for more explanation.</p>
<p>Instead, please use the <code>request</code> library directly for that purpose. Btw, you may use <code>request-promise</code> and <code>request</code> side by side. This way you can benefit from <code>request-promise</code>'s capabilities for all your other requests where you don't download a lot of data. In the future <code>request-promise</code> will properly support streaming the response as well. You may subscribe to <a href="https://github.com/request/request-promise/issues/90" target="_blank">this issue</a> to get notified.</p>
<p>To get an answer for your question please read the <a href="https://github.com/request/request#streaming" target="_blank"><code>request</code> docs</a> and ask the <code>request</code> community.</p>
<p>I am closing this issue because there is nothing I can do for you. But feel free to ask follow-up questions.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  


  
<div>
    
<div>
  





  
  <div id="issuecomment-301526309">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/aranir" target="_blank">@Aranir</a> it's too late maybe, but here is my solution:</p>
<div><pre>const options = {
  url: 'https://url/for/png/file',
  encoding: null
};

request.get(options)
  .then(function (res) {
    const buffer = Buffer.from(res, 'utf8');
    fs.writeFileSync('/some/path', buffer);
  });</pre></div>
      </td>
    </tr>
  </tbody>
</table>


        



    

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-354030234">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          
<p><code>Buffer.from(res, 'utf8')</code> is not necessary since passing <code>encoding: null</code> as option would already make <code>res</code> a <code>Buffer</code>.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-358389703">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>If you are using <code>resolveWithFullResponse</code>, then setting <code>encoding</code> to <code>null</code> will make <code>res.body</code> a buffer. Useful in my case because I care about reading the content type header.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-358857483">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>I just wanted to say thank you to <a href="https://github.com/l11r" target="_blank">@L11R</a> <a href="https://github.com/raine" target="_blank">@raine</a> <a href="https://github.com/boutell" target="_blank">@boutell</a> for putting this all up here. Helped me come up with a clean looking solution where I have to "pipe" an image from a URL to a POST upload endpoint. Here's pseudo (not tested since I had to port it over from my actual code, but you get the gist):</p>
<pre><code>const getImageOptions = {
  url: 'https://news.nationalgeographic.com/content/dam/news/photos/000/755/75552.ngsversion.1422285553360.adapt.1900.1.jpg',
  encoding: null,
  resolveWithFullResponse: true
};

const uploadImageOptions = {
  url: '&lt;your upload url here&gt;'
};

request.get(getImageOptions)
  .then(res =&gt; {
    // Get the content-type of whatever it is that we just grabbed off the interwebs
    // and use that in the subsequent upload request.
    postImageOptions.headers = { 'content-type': res.headers['content-type'] };
    // `res.body` will be a `Buffer`, so we'll pass that right though to the post
    postImageOptions.body = res.body;

    return request.post(uploadImageOptions);
  })
  .then(res =&gt; {
    // Have to JSON.parse this because you can't pass 'json: true' as an option if you
    // are sending a Buffer (or non-JSON-stringifiable data). Upvote this and maybe
    // something can be done:
    // https://github.com/request/request/issues/2692
    res = res && JSON.parse(res);
  });
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  















        


        <div>
              
<div>
  

    
      



      <div>
        
          <div>
  


  
  <div>

    

    

        <p>
    
    
        Attach files by dragging & dropping,
        selecting them, or pasting
        from the clipboard.
    
    
    
    
    
    
    
    
    
  </p>


    
  </div>

  

  


  


          
      




        
      

    
    
  
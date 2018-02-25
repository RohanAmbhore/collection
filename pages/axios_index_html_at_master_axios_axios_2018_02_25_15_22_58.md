<a href="https://github.com/axios/axios/blob/master/examples/upload/index.html">https://github.com/axios/axios/blob/master/examples/upload/index.html</a><div id="articleHeader"><h1>axios/index.html at master · axios/axios</h1></div>
    <div>
  

  <div>
      49 lines (43 sloc)
      
    1.53 KB
  </div>
</div>

    

  
      <table>
      <tbody><tr>
        <td id="L1"></td>
        <td id="LC1">&lt;!doctype html&gt;</td>
      </tr>
      <tr>
        <td id="L2"></td>
        <td id="LC2">&lt;html&gt;</td>
      </tr>
      <tr>
        <td id="L3"></td>
        <td id="LC3">  &lt;head&gt;</td>
      </tr>
      <tr>
        <td id="L4"></td>
        <td id="LC4">    &lt;title&gt;axios - file upload example&lt;/title&gt;</td>
      </tr>
      <tr>
        <td id="L5"></td>
        <td id="LC5">    &lt;link rel="stylesheet" type="text/css" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css"/&gt;</td>
      </tr>
      <tr>
        <td id="L6"></td>
        <td id="LC6">  &lt;/head&gt;</td>
      </tr>
      <tr>
        <td id="L7"></td>
        <td id="LC7">  &lt;body class="container"&gt;</td>
      </tr>
      <tr>
        <td id="L8"></td>
        <td id="LC8">    &lt;h1&gt;file upload&lt;/h1&gt;</td>
      </tr>
      
      <tr>
        <td id="L10"></td>
        <td id="LC10">    &lt;form role="form" class="form" onsubmit="return false;"&gt;</td>
      </tr>
      <tr>
        <td id="L11"></td>
        <td id="LC11">      &lt;div class="form-group"&gt;</td>
      </tr>
      <tr>
        <td id="L12"></td>
        <td id="LC12">        &lt;label for="file"&gt;File&lt;/label&gt;</td>
      </tr>
      <tr>
        <td id="L13"></td>
        <td id="LC13">        &lt;input id="file" type="file" class="form-control"/&gt;</td>
      </tr>
      <tr>
        <td id="L14"></td>
        <td id="LC14">      &lt;/div&gt;</td>
      </tr>
      <tr>
        <td id="L15"></td>
        <td id="LC15">      &lt;button id="upload" type="button" class="btn btn-primary"&gt;Upload&lt;/button&gt;</td>
      </tr>
      <tr>
        <td id="L16"></td>
        <td id="LC16">    &lt;/form&gt;</td>
      </tr>
      
      <tr>
        <td id="L18"></td>
        <td id="LC18">    &lt;div id="output" class="container"&gt;&lt;/div&gt;</td>
      </tr>
      
      <tr>
        <td id="L20"></td>
        <td id="LC20">    &lt;script src="/axios.min.js"&gt;&lt;/script&gt;</td>
      </tr>
      <tr>
        <td id="L21"></td>
        <td id="LC21">    &lt;script&gt;</td>
      </tr>
      <tr>
        <td id="L22"></td>
        <td id="LC22">      (function () {</td>
      </tr>
      <tr>
        <td id="L23"></td>
        <td id="LC23">        var output = document.getElementById('output');</td>
      </tr>
      <tr>
        <td id="L24"></td>
        <td id="LC24">        document.getElementById('upload').onclick = function () {</td>
      </tr>
      <tr>
        <td id="L25"></td>
        <td id="LC25">          var data = new FormData();</td>
      </tr>
      <tr>
        <td id="L26"></td>
        <td id="LC26">          data.append('foo', 'bar');</td>
      </tr>
      <tr>
        <td id="L27"></td>
        <td id="LC27">          data.append('file', document.getElementById('file').files[0]);</td>
      </tr>
      
      <tr>
        <td id="L29"></td>
        <td id="LC29">          var config = {</td>
      </tr>
      <tr>
        <td id="L30"></td>
        <td id="LC30">            onUploadProgress: function(progressEvent) {</td>
      </tr>
      <tr>
        <td id="L31"></td>
        <td id="LC31">              var percentCompleted = Math.round( (progressEvent.loaded * 100) / progressEvent.total );</td>
      </tr>
      
      
      
      <tr>
        <td id="L35"></td>
        <td id="LC35">          axios.put('/upload/server', data, config)</td>
      </tr>
      <tr>
        <td id="L36"></td>
        <td id="LC36">            .then(function (res) {</td>
      </tr>
      <tr>
        <td id="L37"></td>
        <td id="LC37">              output.className = 'container';</td>
      </tr>
      <tr>
        <td id="L38"></td>
        <td id="LC38">              output.innerHTML = res.data;</td>
      </tr>
      
      <tr>
        <td id="L40"></td>
        <td id="LC40">            .catch(function (err) {</td>
      </tr>
      <tr>
        <td id="L41"></td>
        <td id="LC41">              output.className = 'container text-danger';</td>
      </tr>
      <tr>
        <td id="L42"></td>
        <td id="LC42">              output.innerHTML = err.message;</td>
      </tr>
      
      
      <tr>
        <td id="L45"></td>
        <td id="LC45">      })();</td>
      </tr>
      <tr>
        <td id="L46"></td>
        <td id="LC46">    &lt;/script&gt;</td>
      </tr>
      <tr>
        <td id="L47"></td>
        <td id="LC47">  &lt;/body&gt;</td>
      </tr>
      <tr>
        <td id="L48"></td>
        <td id="LC48">&lt;/html&gt;</td>
      </tr>
</tbody></table>

  

  
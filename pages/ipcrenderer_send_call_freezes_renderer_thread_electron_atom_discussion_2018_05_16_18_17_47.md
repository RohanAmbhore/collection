<a href="https://discuss.atom.io/t/ipcrenderer-send-call-freezes-renderer-thread/29419">https://discuss.atom.io/t/ipcrenderer-send-call-freezes-renderer-thread/29419</a><div id="articleHeader"><h1>ipcRenderer.send(...) call freezes renderer thread</h1></div><p>I am using React to render the view on the frontend, and have a dropzone element.<br />
I am able to receive the files that are uploaded, and I’ve written a function that updates a local db (lowDB - just a json file) and runs some scripts to process the files.</p>
<p>However, while it is processing (on the main thread) the renderer thread freezes and gives a beach ball of death. I am sending events back to the renderer thread that contain the progress of this long-running process, but those only appear AFTER the process is complete, all in a row, like they’ve been clogged up in a pipe somewhere.</p>
<p>Roughly:</p>
<p>View file:</p>
<pre><code>
var DropzoneDemo = React.createClass({
  onDrop: function (files) {
    console.log('sending files: ' + JSON.stringify(files));
    ipcRenderer.send('photo-upload', files.map((file) =&gt; file.path));
  },
  
  render: function () {
    return (
      &lt;div&gt;
      	&lt;Dropzone onDrop={this.onDrop}&gt;
      	  &lt;div&gt;Drop some files here, or click to select files to upload.&lt;/div&gt;
      	&lt;/Dropzone&gt;
        {this.props.hashed} of {this.props.totalfiles}
      &lt;/div&gt;
    );
  }
});
</code></pre>
<p>main.js</p>
<pre><code>ipcMain.on('photo-upload', function(event, arg) {
  db.resetDB();
  //Long term process being run as a shell script
  resizeAll(dir, function(error, stdout, stderr){
    if(error){
      console.log(error);
      console.log(stderr);
    }
  });
  // ... more code here to run another process that deals with the first process
  console.log("returning from photo-upload event.")
})
</code></pre>
<p>The log <code>returning from photo-upload event</code> occurs immediately after calling the function, which means that nothing is blocking the thread… yet everything freezes.</p>
<p>Help!</p>
<a href="https://stackoverflow.com/questions/28509569/gulp-livereload-error-in-chrome">https://stackoverflow.com/questions/28509569/gulp-livereload-error-in-chrome</a><div id="articleHeader"><h1>Gulp livereload error in Chrome</h1></div>

<p>I am trying to get LiveReload to work with Gulp and Chrome. I have installed the Chrome extension (v2.0.9), I have enabled "Allow Access to File URLs", which everyone says to do. I am running a simple PHP server with <code>php -S 127.0.0.1:35729 -t dist</code>. I have installed gulp-livereload and started the watch task with this code:</p>

<pre><code>var gulp = require('gulp'),
    reload = require('gulp-livereload');

gulp.task('watch', function(){

    reload.listen(35729, function (err) {
        if (err) return console.log(err);
    });

    gulp.watch('dist/**').on('change', function(file) {
        reload.changed();
        console.log('PHP file changed' + ' (' + file.path + ')');
    });    
});

gulp.task('default', function(){
    gulp.start('watch');
});
</code></pre>

<p>I go to 127.0.0.1:35729 in Chrome. I enable LiveReload by clicking the extension button. I go and edit a file. Gulp says:</p>

<pre><code> [13:28:48] undefined reloaded. 
 PHP file changed (M:\path\to\file)
</code></pre>

<p>The web page does not update. The console in Chrome has this lovely error when the page loads:</p>

<pre><code>GET http://127.0.0.1:35729/livereload.js?ext=Chrome&extver=2.0.9 injected.js:116 
LiveReloadInjected.doEnable injected.js:116
(anonymous function) injected.js:150
. many
. other
. lines
$Array.forEach.publicClass.(anonymous function) extensions::utils:94
dispatchOnMessage extensions::messaging:304 
</code></pre>

<p>I tried something crazy and put the livereload.js file in the root of my server and then I get this error instead:</p>

<blockquote>
  <p>WebSocket connection to 'ws://127.0.0.1:35729/livereload' failed: 
  Connection closed before receiving a handshake response</p>
</blockquote>

<p>Also, I would like to run LiveReload on a different port, but when I change the php server and Gulp watch to port 9999 I get this error:</p>

<blockquote>
  <p>WebSocket connection to 'ws://127.0.0.1:35729/livereload' failed: Error in connection establishment: net::ERR_CONNECTION_REFUSED</p>
</blockquote>
    
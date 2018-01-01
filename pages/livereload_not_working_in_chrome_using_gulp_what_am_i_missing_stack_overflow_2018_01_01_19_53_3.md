<a href="https://stackoverflow.com/questions/32399469/livereload-not-working-in-chrome-using-gulp-what-am-i-missing">https://stackoverflow.com/questions/32399469/livereload-not-working-in-chrome-using-gulp-what-am-i-missing</a><div id="articleHeader"><h1>Livereload not working in Chrome using Gulp, what am I missing</h1></div>

<p>I'm trying to use Livereload using Gulp, Sublime Text 3 and Chrome but for some reason it doesn't work. Here is what I did.</p>

<ol>
<li>Installed the Livereload extension in Chrome.</li>
<li>Installed gulp-livereload.</li>
<li>Setup gulpfile.js.</li>
<li>Ran gulp.</li>
</ol>

<p>What am I missing here? Do I need to install the Livereload plugin for Sublime Text 3?</p>

<p>FYI - The Options button in the Livereload extension in Chrome is grayed-out.</p>

<p>My Gulpfile:</p>

<pre><code>var gulp = require('gulp');        
var scssPlugin = require('gulp-sass');
var livereload = require('gulp-livereload');

gulp.task('myStyles', function () {
    gulp.src('sass/*.scss')
        .pipe(scssPlugin())
        .pipe(gulp.dest('css'))
       .pipe(livereload());
});

gulp.task('watchMyStyles', function() {
    livereload.listen();
    gulp.watch('sass/*.scss', ['myStyles']);
});

gulp.task('default', ['watchMyStyles']);  </code></pre>

<p>Package File:</p>

<pre><code>{
  "devDependencies": {
    "gulp": "^3.9.0",
    "gulp-livereload": "^3.8.0",
    "gulp-sass": "^2.0.4"
  }
}</code></pre>
    
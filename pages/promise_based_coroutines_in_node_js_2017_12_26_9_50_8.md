<a href="http://tobyho.com/2015/12/27/promise-based-coroutines-nodejs/">http://tobyho.com/2015/12/27/promise-based-coroutines-nodejs/</a><div id="articleHeader"><h1>Promise-Based Coroutines in Node.js</h1></div>
	<div>
		Dec 27 ’15
		·
		
			programming
		
			Node.js
		
			JavaScript
		
	
	</div>
</header>

	<p>Ever since the dawn of Node.js, Node developers have complained about <a href="http://callbackhell.com/" target="_blank">Callback Hell</a>. Various solutions have been proposed with various degrees of success.
<a href="http://tobyho.com/2013/06/16/what-are-generators/" target="_blank">Generators</a> is an exciting prospect because it finally allows us to write async code in a straight-line fashion. Although generators is not yet available on all browsers, you can make it work using the <a href="https://babeljs.io/" target="_blank">Babel compiler</a>. It is getting more adoption in Node because the modules <a href="https://github.com/tj/co" target="_blank">co</a> and <a href="https://github.com/koajs/koa" target="_blank">koa</a> have been around for over 2 years, and first <a href="https://iojs.org/en/" target="_blank">IO.js</a> and now Node has had out-of-the-box support for it since version 4.0. This post will cover two modules that give support to generators as a coroutine mechanism to tame the async beast: <a href="https://github.com/tj/co" target="_blank">co</a> and <a href="https://github.com/petkaantonov/bluebird" target="_blank">Bluebird</a>. Both co and Bluebird make use of promises. Bluebird is in fact specifically a promise library. The way you write coroutines with co vs Bluebird are quite similar.</p>

<h2>Prerequisites</h2>

<p>While you may be able to vaguely follow along otherwise, I do expect you to know about <em>generators</em> and <em>promises</em>. Here are some resources if you need to drill down to those topics:</p>




<h2>The Big Idea</h2>

<p>Both co and Bluebird let you do the following: <code>yield</code> a promise to get the underlying value that's wrapped by the promise. Since we can use promises to wrap async operations, yielding allows async operations to be written in a straight-line manner - something that has been sought after since the dawn of Node.js.</p>



<p><a href="https://github.com/tj/co" target="_blank">co</a> is a module that returns just two functions
:</p>

<ul>
<li><code>co(genFn)</code> - co takes a generator function and returns a promise. It will execute the supplied generator function to completion and then resolve the promise.</li>
<li><code>co.wrap(genFn)</code> - co.wrap works like co except it returns a function that returns a promise.</li>
</ul>


<p>The following program will read a Markdown file from the filesystem, convert the contents to HTML, then read a handlebars template file again from the filesystem, then inject the contents into the template, and finally write the resulting HTML into a file.</p>

<div><pre><code>'use strict'

const co = require('co');
const marked = require('marked');
const fs = require('fs-promise');
const handlebars = require('handlebars');

co(function *() {
  let md = yield fs.readFile('README.md');
  let html = marked(md.toString());
  let template = yield fs.readFile('layout.hbs');
  let output = handlebars.compile(template.toString())({
    title: 'README',
    contents: html
  });
  yield fs.writeFile('index.html', output);
}).catch(function(err) {
  console.error(err.stack);
});
</code></pre>
</div>


<p><a href="https://github.com/airportyh/coroutines-in-node/blob/master/co.js" target="_blank">Full Source</a></p>

<p>There are a few things to note about this example:</p>

<ol>
<li>Instead of the core fs module, I am using the <code>fs-promise</code> module which promisifies all the fs APIs.</li>
<li>Whenever we need an async operation, we wrap it up inside of a promise, and we <code>yield</code> it to get back the underlying value. In this example, I use <code>yield</code> twice to read a file, and once to write a file. In the case of writing a file, I didn't care about the resulting value.</li>
<li>Error handling: since <code>co()</code> returns a promise, I can use <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch" target="_blank">catch()</a> to handle any errors occurs within the coroutine - anything from file-not-found to variable-not-defined. If I hadn't set up an error handler this way, any error that occured would have been silenced, which doesn't not make for a good debugging experience.</li>
</ol>


<h2>Bluebird</h2>

<p>Bluebird is primarily a promise library - maybe the most popular one at this time. But it also features a <a href="http://bluebirdjs.com/docs/api/promise.coroutine.html" target="_blank">coroutine function</a> which works very similarly to co. Rewriting the previous example using Bluebird is a small change</p>

<div><pre><code>'use strict'

const bluebird = require('bluebird');
const marked = require('marked');
const fs = require('fs-promise');
const handlebars = require('handlebars');

bluebird.coroutine(function *() {
  let md = yield fs.readFile('README.md');
  let html = marked(md.toString());
  let template = yield fs.readFile('layout.hbs');
  let output = handlebars.compile(template.toString())({
    title: 'README',
    contents: html
  });
  yield fs.writeFile('index.html', output);
})().catch(function(err) {
  console.error(err.stack);
});
</code></pre>
</div>


<p><a href="https://github.com/airportyh/coroutines-in-node/blob/master/bluebird.js" target="_blank">Full Source</a></p>

<p>The only changes are</p>

<ol>
<li>It use the <code>bluebird.coroutine()</code> function instead of <code>co()</code>.</li>
<li><code>bluebird.coroutine()</code> returns a function that returns a promise, as opposed to <code>co()</code> which returns a promise directly - this is like the behavior of <code>co.wrap()</code> - this necessitated adding a <code>()</code> to invoke the resulting function that was returned.</li>
</ol>


<h2>Same Example Code in Promsed-Land</h2>

<p>For comparison, this is what the example code might have looked like written using promises, but without the help of coroutines</p>

<div><pre><code>'use strict'

const marked = require('marked');
const fs = require('fs-promise');
const handlebars = require('handlebars');

fs.readFile('README.md').then(function(md) {;
  let html = marked(md.toString());
  return [fs.readFile('layout.hbs'), html];
})
.spread(function(template, html) {
  let output = handlebars.compile(template.toString())({
    title: 'README',
    contents: html
  });
  return fs.writeFile('index.html', output);
})
.catch(function(err) {
  console.error(err.stack);
});
</code></pre>
</div>


<p><a href="https://github.com/airportyh/coroutines-in-node/blob/master/promise-based.js" target="_blank">Full Source</a></p>

<p>Note: <a href="http://bluebirdjs.com/docs/api/spread.html" target="_blank">spread()</a> is a convinience provided by Bluebird, which is used by <a href="https://www.npmjs.com/package/fs-promise" target="_blank">fs-promise</a> underneath.</p>

<h2>Promisifying Async Operations</h2>

<p>Using this coroutine paradigm means that you have to wrap any and all async APIs with promisified versions. You have two options:</p>

<ol>
<li>Use a promise library's helper utilities to wrap Node-style async functions as functions that return a promise.


</li>
<li>Use libraries whose sole purpose is to promisify an exist Node-style library. Some examples are:


</li>
</ol>


<h2>Extracting Sub-Coroutines</h2>

<p>Now that you are writing a lot of code inside of generator functions, you may want to at some point break them up into sub-routines in order to reuse and better organize your code. Normally you'd extract a new function, but since you can't use <code>yield</code> statements inside of functions, you will need need to extract generator functions.</p>

<h3>Subroutines With co</h3>

<p>Extracting subroutines will work slightly differently between co and Bluebird. I will start with co.</p>

<p>If I wanted to extract a routine called <code>md2html</code> to convert a Markdown file to HTML. I could write</p>

<div><pre><code>function * md2html(filename) {
  let md = yield fs.readFile(filename + '.md');
  let html = marked(md.toString());
  let template = yield fs.readFile('layout.hbs');
  let output = handlebars.compile(template.toString())({
    title: filename,
    contents: html
  });
  yield fs.writeFile(filename + '.html', output);
  console.log(`Wrote ${filename}.html`);
}
</code></pre>
</div>


<p>The body of this generator function is mostly copy-n-pasted from my original, only now with the file name substituted via a variable. To call this generator function via another function, you would simply <code>yield</code> it:</p>

<div><pre><code>yield md2html('README');
</code></pre>
</div>


<p><a href="https://github.com/airportyh/coroutines-in-node/blob/master/sub-routine.js" target="_blank">Full Source</a></p>

<h3>Subroutines With A Return Value</h3>

<p>If you want to extract a subroutine that returns a value, you can use the <code>return</code> statement within the extracted generator function - same as normal functions. For example, let's say we want to return the generated markup instead of writing it to a file:</p>

<div><pre><code>function * md2html(filename) {
  let md = yield fs.readFile(filename + '.md');
  let html = marked(md.toString());
  let template = yield fs.readFile('layout.hbs');
  let output = handlebars.compile(template.toString())({
    title: filename,
    contents: html
  });
  return output;
}
</code></pre>
</div>


<p>Now we can yield to get its value:</p>

<div><pre><code>let html = yield md2html('README');
</code></pre>
</div>


<p><a href="https://github.com/airportyh/coroutines-in-node/blob/master/sub-routine-with-return.js" target="_blank">Full Source</a></p>

<h3>Subroutines With Bluebird</h3>

<p>Bluebird's coroutine mechanism doesn't permit yielding generator instances directly. To extract a generator function in Bluebird, you could use the <code>bluebird.coroutine</code> function to wrap the extracted generator function</p>

<div><pre><code>const md2html = bluebird.coroutine(function * md2html(filename) {
  let md = yield fs.readFile(filename + '.md');
  let html = marked(md.toString());
  let template = yield fs.readFile('layout.hbs');
  let output = handlebars.compile(template.toString())({
    title: filename,
    contents: html
  });
  return output;
});
</code></pre>
</div>


<p>And then invoking the coroutine the same way</p>

<div><pre><code>let html = yield md2html('README');
</code></pre>
</div>


<p><a href="https://github.com/airportyh/coroutines-in-node/blob/master/sub-routine-with-return-bluebird.js" target="_blank">Full Source</a></p>

<h2>Parallelizing Tasks</h2>

<p>Someone once mentioned to me that using generators in Node is not in the Node style because it removes the parallelization of IO operations that Node <a href="http://blog.mixu.net/2011/02/01/understanding-the-node-js-event-loop/" target="_blank">gives you for free</a>. Well, yes and no, because this can be easily rectified.</p>

<p>Let's say you have 100 files you have to convert from Markdown to HTML. You might do this:</p>

<div><pre><code>let files = yield fs.readdir('markdown');
for (let i = 0; i &lt; files.length; i++) {
  yield md2html('markdown/' + path.basename(files[i], '.md'));
}
</code></pre>
</div>


<p><a href="https://github.com/airportyh/coroutines-in-node/blob/master/serial.js" target="_blank">Full Source</a></p>

<p>And this would convert the files serially. But to convert them in parallel is pretty easy too! Just convert each task into a promise and then use <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all" target="_blank">Promise.all</a> or equivalent to execute them in parallel. <code>Promise.all()</code> takes an array of promises and resolves as an array of the resolved values of the promises when every one of the promises has resolved. <em>Hint: you can convert a generator function into a promise using co or Bluebird.</em></p>

<div><pre><code>let files = yield fs.readdir('markdown');
let tasks = files.map(function(file) {
  return co(md2html('markdown/' + path.basename(file, '.md')));
});
yield Promise.all(tasks);
</code></pre>
</div>


<p><a href="https://github.com/airportyh/coroutines-in-node/blob/master/parallel.js" target="_blank">Full Source</a></p>

<p>If you want to limit the concurrency - the number of tasks that are being performed at a time, you can use the <a href="https://www.npmjs.com/package/throat" target="_blank">throat module</a>.</p>

<h2>Error Handling</h2>

<p>Error handling within a coroutine is easy - you can use try/catch. <em>What a concept!</em></p>

<div><pre><code>function * md2html(filename) {
  try {
    let md = yield fs.readFile(filename + '.md');
    let html = marked(md.toString());
    let template = yield fs.readFile('layout.hbs');
    let output = handlebars.compile(template.toString())({
      title: filename,
      contents: html
    });
    yield fs.writeFile(filename + '.html', output);
    console.log(`Wrote ${filename}.html`);
  } catch (e) {
    console.error(`Failed to convert ${filename}.md because ${e.message}`);
  }
}
</code></pre>
</div>


<p><a href="https://github.com/airportyh/coroutines-in-node/blob/master/error-handling.js" target="_blank">Full Source</a></p>

<h2>Gotchas</h2>

<p>The most common gotcha for someone learning to use this paradigm is forgetting to yield a promise. Unfortunately, you often won't get a very illuminating error message in this case due to JavaScript's lack of type safety. For example, if I had forgotten to yield the promise that holds the contents of the file:</p>

<div><pre><code>let md = fs.readFile(filename + '.md');
let html = marked(md.toString());
</code></pre>
</div>


<p><a href="https://github.com/airportyh/coroutines-in-node/blob/master/forgot-yield.js#L15" target="_blank">Full Source</a></p>

<p><code>md</code> would hold the promise object rather than the actual buffer containing the content of the file. Then on the next line, <code>md.toString()</code> will actually work and return the string "[object Promise]" because <code>toString()</code> is a method that all JavaScript objects have.</p>

<p>If you forget to yield a generator function that doesn't return a value, or whose value you simple don't care about</p>

<div><pre><code>md2html('README'); // nothing happens!
</code></pre>
</div>


<p><a href="https://github.com/airportyh/coroutines-in-node/blob/master/forgot-yield-2.js#L9" target="_blank">Full Source</a></p>

<p>That generator function never executes! Because calling a generator function only instantiates a generator instance, but it doesn't execute that generator instance.</p>

<p>If you are hitting a JSON-based API, and you forget to yield, for example</p>

<div><pre><code>let result = request({
  url: 'https://api.github.com/repos/petkaantonov/bluebird', 
  json: true,
  headers: { 'User-Agent': 'Script' }
});
let owner = result.owner.login;
</code></pre>
</div>


<p><a href="https://github.com/airportyh/coroutines-in-node/blob/master/forgot-yield-3.js" target="_blank">Full Source</a></p>

<p>Will result in a <code>TypeError: Cannot read property 'login' of undefined</code> because a promise object doesn't have the properties/object struct you are expecting.</p>

<p>Alas, we are still coding JavaScript!</p>

<h2>Are Coroutines Right For You?</h2>

<p>I have been using this approach for Node.js programming to do standalone command-line scripts, app servers, and end-to-end browser tests using selenium, and not having to write the standard Node-style callback pattern and handle error handling code every time I do an IO operation has really help me reduce mental and typing overhead.</p>

<p>I think this approach is particularly appealing if you primarily do server-side programming. You can also use this approach in the browser in a way that works cross-browser if you use the <a href="https://babeljs.io/" target="_blank">Babel compiler</a> with the <a href="https://babeljs.io/docs/usage/polyfill/" target="_blank">regenerator runtime</a> - although I have not done this extensively.</p>

<p>One reason some people might shy away from adopting this technique now is the upcoming <a href="http://pouchdb.com/2015/03/05/taming-the-async-beast-with-es7.html" target="_blank">async/await</a> feature - which is essentially a small layer of syntactic suger on top of generators. async/await is an ES7 feature, but you can already use it currently if you use the Babel compiler. I have not taken this route myself because I take comfort in staying close to the metal and prefer not using code transpilers. Also, in general I feel more comfortable when there is a bit of distance between me and the bleeding edge.</p>

<p>At the end of the day, try it and see.</p>

<h2>Next Up</h2>

<p>In the near future I will have more to say about server programming and testing in this paradigm.</p>


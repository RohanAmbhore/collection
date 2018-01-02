<a href="https://www.sitepoint.com/introduction-jquery-deferred-objects/">https://www.sitepoint.com/introduction-jquery-deferred-objects/</a><div id="articleHeader"><h1>            An Introduction to jQuery’s Deferred Objects          </h1></div>
    
      
        
                        
    
      

        
      
      <p>For a long time, JavaScript developers have used callback functions to perform several tasks. A very common example is to add a callback via the <code>addEventListener()</code> function to execute various operations when an event, such as <code>click</code> or <code>keypress</code>, is fired. Callback functions are simple and get the job done for simple cases. Unfortunately, when your web pages increase in complexity and you need to perform many asynchronous operations, either in parallel or in sequence, they become unmanageable.</p>
<p>ECMAScript 2015 (a.k.a. ECMAScript 6) introduced a native means to deal with such situations: promises. If you don’t know what promises are, you can read the article <a href="http://www.sitepoint.com/overview-javascript-promises/" target="_blank">An Overview of JavaScript Promises</a>. jQuery provided and still provides its own flavor of promises, called <a href="https://api.jquery.com/category/deferred-object/" target="_blank">Deferred objects</a>. They were introduced to jQuery years before promises were introduced to ECMAScript. In this article, I’ll discuss what <code>Deferred</code> objects are, and what problems they try to solve.</p>
<h2 id="abriefhistory">A Brief History</h2>

<p>The <code>Deferred</code> object was introduced in jQuery 1.5 as a chainable utility used to register multiple callbacks into callback queues, invoke callback queues, and relay the success or failure state of any synchronous or asynchronous function. Since then, it has been the subject of discussion, some criticism, and a lot of changes along the way. A couple of examples of criticism are <a href="https://blog.domenic.me/youre-missing-the-point-of-promises/" target="_blank">You’re Missing the Point of Promises</a> and <a href="https://thewayofcode.wordpress.com/tag/jquery-deferred-broken/" target="_blank">JavaScript Promises and why jQuery implementation is broken</a>.</p>
<p>Together with the <a href="http://api.jquery.com/Types/#Promise" target="_blank">Promise object</a>, <code>Deferred</code> represents the jQuery implementation of promises. In jQuery version 1.x and 2.x the <code>Deferred</code> object adheres to <a href="http://wiki.commonjs.org/wiki/Promises/A" target="_blank">the CommonJS Promises/A proposal</a>. This proposal was used as a base for the <a href="https://promisesaplus.com/" target="_blank">Promises/A+ proposal</a> which native promises are built upon. As mentioned in the introduction, the reason why jQuery doesn’t adhere to the Promises/A+ proposal is because it implemented promises way before this proposal was even conceived.</p>
<p>Because jQuery was a precursor and due to backward-compatibility issues, there are differences in how you can use promises in pure JavaScript and in jQuery 1.x and 2.x. Moreover, because jQuery follows a different proposal, the library is incompatible with other libraries that implemented promises such as <a href="https://github.com/kriskowal/q" target="_blank">the Q library</a>.</p>
<p>In the upcoming <strong>jQuery 3</strong> the interoperability with native promises (as implemented in ECMAScript 2015) <a href="https://github.com/jquery/jquery/issues/1722" target="_blank">has been improved</a>. The signature of the main method (<code>then()</code>) is still a bit different for reasons of backwards compatibility, but the behavior is more in line with the standard.</p>
<h2 id="callbacksinjquery">Callbacks in jQuery</h2>
<p>To understand why you might need to use the <code>Deferred</code> object, let’s discuss an example. When using jQuery, it’s very common to use its Ajax methods to perform asynchronous requests. For the sake of the example, let’s say that you’re developing a web page that is sending Ajax requests to the GitHub API. Your goal is to retrieve the list of a user’s repositories, find the most recently updated repository, locate the first file with the string “README.md” in its name and finally retrieve that file’s contents. Based on this description, each Ajax request may only start when the previous step has been completed. In other words, the requests must run in <em>sequence</em>.</p>
<p>Turning this description into pseudocode (please note that I’m not using the real GitHub API), we get:</p>
<pre><code>var username = 'testuser';
var fileToSearch = 'README.md';

$.getJSON('https://api.github.com/user/' + username + '/repositories', function(repositories) {
  var lastUpdatedRepository = repositories[0].name;

  $.getJSON('https://api.github.com/user/' + username + '/repository/' + lastUpdatedRepository + '/files', function(files) {
    var README = null;

    for (var i = 0; i &lt; files.length; i++) {
      if (files[i].name.indexOf(fileToSearch) &gt;= 0) {
        README = files[i].path;

        break;
      }
    }

    $.getJSON('https://api.github.com/user/' + username + '/repository/' + lastUpdatedRepository + '/file/' + README + '/content', function(content) {
      console.log('The content of the file is: ' + content);
    });
  });
});
</code></pre>
<p>As you can see in this example, using callbacks we have to nest the calls to perform the Ajax requests in the sequence we want. This makes the code less readable. The situation where you have a lot of nested callbacks, or independent callbacks that have to be synchronized, is often referred to as the “callback hell”.</p>
<p>To make it slightly better, you can extract named functions from the anonymous inline functions I created. However, this change doesn’t help much and we still find ourselves in callback hell. Enter the <code>Deferred</code> and the <code>Promise</code> objects.</p>
<h2 id="thedeferredandthepromiseobjects">The Deferred and the Promise Objects</h2>
<p>The <code>Deferred</code> object can be employed when performing asynchronous operations, such as Ajax requests and animations. In jQuery, the <code>Promise</code> object is created from a <code>Deferred</code> object or a <code>jQuery</code> object. It possesses a subset of the methods of the <code>Deferred</code> object: <code>always()</code>, <code>done()</code>, <code>fail()</code>, <code>state()</code>, and <code>then()</code>. I’ll cover these methods and others in the next section.</p>
<p>If you’re coming from the native JavaScript world, you might be confused by the existence of these two objects. Why have two objects (<code>Deferred</code> and <code>Promise</code>) when JavaScript has one (<code>Promise</code>)? To explain the difference and their use cases, I’ll adopt the same analogy I’ve used in my book <a href="https://www.manning.com/books/jquery-in-action-third-edition" target="_blank">jQuery in Action, third edition</a>.</p>
<p><code>Deferred</code> objects are typically used if you write the function that deals with asynchronous operations and which should return a value (which can also be an error or no value at all). In this case, your function is the <strong>producer</strong> of the value and you want to prevent users from changing the state of the <code>Deferred</code>. The promise object is used when you’re the <strong>consumer</strong> of the function.</p>
<p>To clarify the concept, let’s say that you want to implement a promise-based <code>timeout()</code> function (I’ll show you the code for this example in a <a href="#creatingapromisebasedsettimeoutfunction" target="_blank">following section of this article</a>). You are the one in charge of writing the function that has to wait for a given amount of time (no value is returned in this case). This makes you the <strong>producer</strong>. The <strong>consumer</strong> of your function doesn’t care about resolving or rejecting it. The consumer only needs to be able to add functions to execute upon the fulfillment, the failure, or the progress of the <code>Deferred</code>. Moreover, you want to ensure that the consumer isn’t able to resolve or reject the <code>Deferred</code> at their discretion. To achieve this goal, you need to return the <code>Promise</code> object of the <code>Deferred</code> you’ve created in your <code>timeout()</code> function, not the <code>Deferred</code> itself. By doing so, you ensure that nobody can call the <code>resolve()</code> or <code>reject()</code> method except for your <code>timeout()</code> function.</p>
<p>You can read more about the difference between jQuery’s Deferred and Promise objects in this <a href="http://stackoverflow.com/q/17308172/1136887" target="_blank">StackOverflow question</a>.</p>
<p>Now that you know what these objects are, let’s take a look at the methods available.</p>
<h2 id="thedeferredmethods">The Deferred Methods</h2>
<p>The <code>Deferred</code> object is quite flexible and provides methods for all your needs. It can be created by calling the <code>jQuery.Deferred()</code> method as follows:</p>
<pre><code>var deferred = jQuery.Deferred();
</code></pre>
<p>or, using the <code>$</code> shortcut:</p>
<pre><code>var deferred = $.Deferred();
</code></pre>
<p>Once created, the <code>Deferred</code> object exposes several methods. Ignoring those deprecated or removed, they are:</p>
<ul><li><code>always(callbacks[, callbacks, ..., callbacks])</code>: Add handlers to be called when the <code>Deferred</code> object is either resolved or rejected.</li>
<li><code>done(callbacks[, callbacks, ..., callbacks])</code>: Add handlers to be called when the <code>Deferred</code> object is resolved.</li>
<li><code>fail(callbacks[, callbacks, ..., callbacks])</code>: Add handlers to be called when the <code>Deferred</code> object is rejected.</li>
<li><code>notify([argument, ..., argument])</code>: Call the <code>progressCallbacks</code> on a <code>Deferred</code> object with the given arguments.</li>
<li><code>notifyWith(context[, argument, ..., argument])</code>: Call the <code>progressCallbacks</code> on a <code>Deferred</code> object with the given context and arguments.</li>
<li><code>progress(callbacks[, callbacks, ..., callbacks])</code>: Add handlers to be called when the <code>Deferred</code> object generates progress notifications.</li>
<li><code>promise([target])</code>: Return a <code>Deferred</code>‘s <code>Promise</code> object.</li>
<li><code>reject([argument, ..., argument])</code>: Reject a <code>Deferred</code> object and call any <code>failCallbacks</code> with the given arguments.</li>
<li><code>rejectWith(context[, argument, ..., argument])</code>: Reject a <code>Deferred</code> object and call any <code>failCallbacks</code> with the given context and arguments.</li>
<li><code>resolve([argument, ..., argument])</code>: Resolve a <code>Deferred</code> object and call any <code>doneCallbacks</code> with the given arguments.</li>
<li><code>resolveWith(context[, argument, ..., argument])</code>: Resolve a <code>Deferred</code> object and call any <code>doneCallbacks</code> with the given context and arguments.</li>
<li><code>state()</code>: Determine the current state of a <code>Deferred</code> object.</li>
<li><code>then(resolvedCallback[, rejectedCallback[, progressCallback]])</code>: Add handlers to be called when the <code>Deferred</code> object is resolved, rejected, or still in progress.</li>
</ul><p>The description of these methods gives me the chance to highlight one difference between the terminology used by jQuery’s documentation and ECMAScript’s specifications. In the ECMAScript specifications, a promise is said to be resolved when it’s either fulfilled or rejected. In jQuery’s documentation however, the word resolved is used to refer to what the ECMAScript specification calls the fulfilled state.</p>
<p>Due to the quantity of the methods provided, it isn’t possible to cover all of them in this article. However, in the next sections I’ll show you a couple of examples of the use of <code>Deferred</code> and <code>Promise</code>. In the first example we’ll rewrite the snippet examined in the section “Callbacks in jQuery” but instead of using callbacks we’ll employ these objects. In the second example, I’ll clarify the producer-consumer analogy discussed.</p>
<h2 id="ajaxrequestsinsequencewithdeferred">Ajax Requests in Sequence with Deferred</h2>
<p>In this section I’ll show how to use the <code>Deferred</code> object and some of its methods to improve the readability of the code developed in the “Callbacks in jQuery” section. Before delving into it, we have to understand which of the available methods we need.</p>
<p>According to our requirements and the list of methods provided, it’s clear than we can use either the <code>done()</code> or the <code>then()</code> method to manage the successful cases. Since many of you might already be accustomed to the JavaScript’s <code>Promise</code> object, in this example I’ll employ the <code>then()</code> method. One important difference between these two methods is that <code>then()</code> has the ability to forward the value received as a parameter to other <code>then()</code>, <code>done()</code>, <code>fail()</code>, or <code>progress()</code> calls defined after it.</p>
<p>The final result is shown below:</p>
<pre><code>var username = 'testuser';
var fileToSearch = 'README.md';

$.getJSON('https://api.github.com/user/' + username + '/repositories')
  .then(function(repositories) {
    return repositories[0].name;
  })
  .then(function(lastUpdatedRepository) {
    return $.getJSON('https://api.github.com/user/' + username + '/repository/' + lastUpdatedRepository + '/files');
  })
  .then(function(files) {
    var README = null;

    for (var i = 0; i &lt; files.length; i++) {
      if (files[i].name.indexOf(fileToSearch) &gt;= 0) {
        README = files[i].path;

        break;
      }
    }

    return README;
  })
  .then(function(README) {
    return $.getJSON('https://api.github.com/user/' + username + '/repository/' + lastUpdatedRepository + '/file/' + README + '/content');
  })
  .then(function(content) {
    console.log(content);
  });
</code></pre>
<p>As you can see, the code is much more readable as we’re able to break the whole process in small steps that are all at the same level (in regards of indentation).</p>
<h2 id="creatingapromisebasedsettimeoutfunction">Creating a Promise-Based setTimeout Function</h2>
<p>As you might know, <a href="http://www.sitepoint.com/jquery-settimeout-function-examples/" target="_blank">setTimeout()</a> is a function that executes a callback function after a given amount of time. Both these elements (the callback function and the time) should be provided as arguments. Let’s say that you want to log a message to the console after one second. By using the <code>setTimeout()</code> function, you can achieve this goal with the code shown below:</p>
<pre><code>setTimeout(
  function() {
    console.log('I waited for 1 second!');
  },
  1000
);
</code></pre>
<p>As you can see, the first argument is the function to execute, while the second is the amount of milliseconds to wait. This function has worked well for years but what if you need to introduce a delay in your <code>Deferred</code> chain?</p>
<p>In the following code I’ll show you how to use the <code>Promise</code> object that jQuery provides to develop a promise-based <code>setTimeout()</code> function. To do so, I’ll employ the <code>Deferred</code> object’s <code>promise()</code> method.</p>
<p>The final result is shown below:</p>
<pre><code>function timeout(milliseconds) {
  // Create a new Deferred object
  var deferred = $.Deferred();

  // Resolve the Deferred after the amount of time specified by milliseconds
  setTimeout(deferred.resolve, milliseconds);

  // Return the Deferred's Promise object
  return deferred.promise();
}

timeout(1000).then(function() {
  console.log('I waited for 1 second!');
});
</code></pre>
<p>In this listing I defined a function called <code>timeout()</code> which wraps the JavaScript’s native <code>setTimeout()</code> function. Inside the <code>timeout()</code> I created a new <code>Deferred</code> object to manage an asynchronous task that consists of resolving the <code>Deferred</code> object after the specified amount of milliseconds. In this case, the <code>timeout()</code> function is the producer of the value, so it creates the <code>Deferred</code> object and returns a <code>Promise</code> object. By doing so, I ensure that the caller of the function (the consumer) can’t resolve or reject the <code>Deferred</code> object at will. In fact, the caller can only add functions to execute, using methods such as <code>done()</code> and <code>fail()</code>.</p>
<h2 id="differencesbetweenjquery1x2xandjquery3">Differences between jQuery 1.x/2.x and jQuery 3</h2>
<p>In the first example using <code>Deferred</code> we developed a snippet that looks for a file containing the string “README.md” in its name, but we didn’t account for the situation in which such file isn’t found. This situation can be seen as a failure. When this case happens we might want to break the chain of calls and jump right to its end. To do so it would be natural to throw an exception and catch it with the <code>fail()</code> method, as you would do with the JavaScript’s <code>catch()</code> method.</p>
<p>In Promises/A and Promises/A+ compliant libraries (for example, jQuery 3.x), a thrown exception is translated into a rejection and the failure callback, such as one added with <code>fail()</code> is called. This receives the exception as an argument.</p>
<p>In jQuery 1.x and 2.x an uncaught exception will halt the program’s execution. These versions allow the thrown exception to bubble up, usually reaching <code>window.onerror</code>. If no function is defined to handle this exception, the exception’s message is shown and the program’s execution is aborted.</p>
<p>To better understand the different behavior, take a look at this example taken from my book:</p>
<pre><code>var deferred = $.Deferred();
deferred
  .then(function() {
    throw new Error('An error message');
  })
  .then(
    function() {
      console.log('First success function');
    },
    function() {
      console.log('First failure function');
    }
  )
  .then(
    function() {
      console.log('Second success function');
    },
    function() {
      console.log('Second failure function');
    }
  );

deferred.resolve();
</code></pre>
<p>In jQuery 3.x, this code would write the message “First failure function” and “Second success function” to the console. The reason is that, as I mentioned before, the specification states that a thrown exception should be translated into a rejection and the failure callback has to be called with the exception. In addition, once the exception has been managed (in our example by the failure callback passed to the second <code>then()</code>), the following success functions should be executed (in this case the success callback passed to the third <code>then()</code>).</p>
<p>In jQuery 1.x and 2.x, none but the first function (the one throwing the error) is executed and you’ll only see the message “Uncaught Error: An error message” displayed on the console.</p>
<h3 id="jquery1x2x">jQuery 1.x/2.x</h3>
<h3 id="jquery3">jQuery 3</h3>
<p>To further improve its compatibility with ECMAScript 2015, jQuery 3 also adds a new method to the <code>Deferred</code> and the <code>Promise</code> objects called <code>catch()</code>. It’s a method to define a handler executed when the <code>Deferred</code> object is <code>rejected</code> or its <code>Promise</code> object is in a rejected state. Its signature is as follows:</p>
<pre><code>deferred.catch(rejectedCallback)
</code></pre>
<p>This method is nothing but a shortcut for <code>then(null, rejectedCallback)</code>.</p>
<h2 id="conclusions">Conclusions</h2>
<p>In this article I’ve introduced you to jQuery’s implementation of promises. Promises allow you to avoid nasty tricks to synchronize parallel asynchronous functions and the need to nest callbacks inside callbacks inside callbacks…</p>
<p>In addition to showing a few examples, I’ve also covered how jQuery 3 improves the interoperability with native promises. Despite the differences highlighted between old jQuery versions and ECMAScript 2015, <code>Deferred</code> remains an incredibly powerful tool to have in your toolbox. As a professional developer and with the increasing difficulty of your projects, you’ll find yourself using it a lot.</p>
      <div>
        
        <div>I'm a (full-stack) web and app developer with more than 5 years' experience programming for the web using HTML, CSS, Sass, JavaScript, and PHP. I'm an expert of JavaScript and HTML5 APIs but my interests include web security, accessibility, performance, and SEO. I'm also a regular writer for several networks, speaker, and author of the books <a href="http://www.manning.com/derosa/" target="_blank"><cite>jQuery in Action, third edition</cite></a> and <a href="http://www.packtpub.com/learn-how-to-use-jquery-selectors-effectively/book" target="_blank"><cite>Instant jQuery Selectors</cite></a>.</div>
      </div>
      
      
<a href="https://www.sitepoint.com/proper-error-handling-javascript/">https://www.sitepoint.com/proper-error-handling-javascript/</a><div id="articleHeader"><h1>A Guide to Proper Error Handling in JavaScript — SitePoint</h1></div>
      <p>Ah, the perils of error handling in JavaScript. If you believe <a href="https://en.wikipedia.org/wiki/Murphy%27s_law" target="_blank">Murphy’s law</a>, anything that can go wrong, will go wrong. In this article, I would like to explore error handling in JavaScript. I will cover pitfalls, good practices, and finish with asynchronous code and Ajax.</p>
<blockquote>
<p>This popular article was updated on 08.06.2017 to address reader feedback. Specifically, file names were added to snippets, unit tests were cleaned up, wrapper pattern was added to <code>uglyHandler</code>,  sections on CORS and 3rd party error handlers were added.</p>
</blockquote>

<p>I feel JavaScript’s event-driven paradigm adds richness to the language. I like to imagine the browser as this event-driven machine, and errors are no different. When an error occurs, an event gets thrown at some point. In theory, one could argue errors are simple events in JavaScript.</p>
<p>If this sounds foreign to you, buckle up as you are in for quite a ride. For this article, I will focus only on client-side JavaScript.</p>
<p>This topic builds on concepts explained in <a href="http://www.sitepoint.com/exceptional-exception-handling-in-javascript/" target="_blank">Exceptional Exception Handling in JavaScript</a>. I recommend reading up on the basics if you are not familiar. This article also assumes an intermediate level of JavaScript knowledge. If you’re looking to level up, why not sign up for SitePoint Premium and watch our course <a href="https://www.sitepoint.com/premium/courses/javascript-next-steps-2921" target="_blank">JavaScript: Next Steps</a>. The first lesson is free.</p>
<p>In either case, my goal is to explore beyond the bare necessities for handling exceptions. Reading this article will make you think twice the next time you see a nice <code>try...catch</code> block.</p>
<h2 id="thedemo">The Demo</h2>
<p>The demo we’ll be using for this article is available on <a href="https://github.com/sitepoint-editors/ProperErrorHandlingJavaScript" target="_blank">GitHub</a>, and presents a page like this:</p>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/05/1496102337proper_error_handling_javascript_1.png" alt="Error Handling in JavaScript Demo" /></div></p>
<p>All buttons detonate a “bomb” when clicked. This bomb simulates an exception that gets thrown as a <code>TypeError</code>. Below is the definition of such a module:</p>
<pre><code>// scripts/error.js

function error() {
  var foo = {};
  return foo.bar();
}
</code></pre>
<p>To begin, this function declares an empty object named <code>foo</code>. Note that <code>bar()</code> does not get a definition anywhere. Let’s verify that this will detonate a bomb with a good unit test:</p>
<pre><code>// tests/scripts/errorTest.js

it('throws a TypeError', function () {
  should.throws(error, TypeError);
});
</code></pre>
<p>This unit test is in <a href="http://mochajs.org/" target="_blank">Mocha</a> with test assertions in <a href="http://shouldjs.github.io/" target="_blank">Should.js</a>. Mocha is a test runner while Should.js is the assertion library. Feel free to explore the testing APIs if you are not already familiar. A test begins with <code>it('description')</code> and ends with a pass / fail in <code>should</code>. The unit tests run on Node and do not need a browser. I recommend paying attention to the tests as they prove out key concepts in plain JavaScript.</p>
<blockquote>
<p>Once you have cloned the repo and installed the dependencies, you can run the tests using <code>npm t</code>. Alternatively, you can run this individual test like so: <code>./node_modules/mocha/bin/mocha tests/scripts/errorTest.js</code>. </p>
</blockquote>
<p>As shown, <code>error()</code> defines an empty object then it tries to access a method. Because <code>bar()</code> does not exist within the object, it throws an exception. Believe me, with a dynamic language like JavaScript this happens to everyone!</p>
<h2 id="thebad">The Bad</h2>
<p>On to some bad error handling. I have abstracted the handler on the button from the implementation. Here is what the handler looks like:</p>
<pre><code>// scripts/badHandler.js

function badHandler(fn) {
  try {
    return fn();
  } catch (e) { }
  return null;
}
</code></pre>
<p>This handler receives a <code>fn</code> callback as a parameter. This callback then gets called inside the handler function. The unit tests show how it is useful:</p>
<pre><code>// tests/scripts/badHandlerTest.js

it('returns a value without errors', function() {
  var fn = function() {
    return 1;
  };

  var result = badHandler(fn);

  result.should.equal(1);
});

it('returns a null with errors', function() {
  var fn = function() {
    throw new Error('random error');
  };

  var result = badHandler(fn);

  should(result).equal(null);
});
</code></pre>
<p>As you can see, this bad error handler returns <code>null</code> if something goes wrong. The callback <code>fn()</code> can point to a legit method or a bomb.</p>
<p>The click event handler below tells the rest of the story:</p>
<pre><code>// scripts/badHandlerDom.js

(function (handler, bomb) {
  var badButton = document.getElementById('bad');

  if (badButton) {
    badButton.addEventListener('click', function () {
      handler(bomb);
      console.log('Imagine, getting promoted for hiding mistakes');
    });
  }
}(badHandler, error));
</code></pre>
<p>What stinks is I only get a <code>null</code>. This leaves me blind when I try to figure out what went wrong. This fail-silent strategy can range from bad UX all the way down to data corruption. What is frustrating with this is I can spend hours debugging the symptom but miss the try-catch block. This wicked handler swallows mistakes in the code and pretends all is well. This may be okay with organizations that don’t sweat code quality. But, hiding mistakes will find you debugging for hours in the future. In a multi-layered solution with deep call stacks, it is impossible to figure out where it went wrong. As far as error handling, this is pretty bad.</p>
<p>A fail-silent strategy will leave you pining for better error handling. JavaScript offers a more elegant way of dealing with exceptions.</p>
<h2 id="theugly">The Ugly</h2>
<p>Time to investigate an ugly handler. I will skip the part that gets tight-coupled to the DOM. There is no difference here from the bad handler you saw. </p>
<pre><code>// scripts/uglyHandler.js

function uglyHandler(fn) {
  try {
    return fn();
  } catch (e) {
    throw new Error('a new error');
  }
}
</code></pre>
<p>What matters is the way it handles exceptions as shown below with this unit test:</p>
<pre><code>// tests/scripts/uglyHandlerTest.js

it('returns a new error with errors', function () {
  var fn = function () {
    throw new TypeError('type error');
  };

  should.throws(function () {
    uglyHandler(fn);
  }, Error);
});
</code></pre>
<p>A definite improvement over the bad handler. Here the exception gets bubbled through the call stack. What I like is now errors will <a href="https://en.wikipedia.org/wiki/Call_stack#Unwinding" target="_blank">unwind the stack</a> which is super helpful in debugging. With an exception, the interpreter travels up the stack looking for another handler. This opens many opportunities to deal with errors at the top of the call stack. Unfortunately, since it is an ugly handler I lose the original error. So I am forced to traverse back down the stack to figure out the original exception. With this at least I know something went wrong, which is why you throw an exception.</p>
<p>As an alternative, is is possible to end the ugly handler with a custom error. When you add more details to an error it is no longer ugly but helpful. The key is to append specific information about the error.</p>
<p>For example:</p>
<pre><code>// scripts/specifiedError.js

// Create a custom error
var SpecifiedError = function SpecifiedError(message) {
  this.name = 'SpecifiedError';
  this.message = message || '';
  this.stack = (new Error()).stack;
};

SpecifiedError.prototype = new Error();
SpecifiedError.prototype.constructor = SpecifiedError;
</code></pre>
<pre><code>// scripts/uglyHandlerImproved.js

function uglyHandlerImproved(fn) {
  try {
    return fn();
  } catch (e) {
    throw new SpecifiedError(e.message);
  }
}
</code></pre>
<pre><code>// tests/scripts/uglyHandlerImprovedTest.js

it('returns a specified error with errors', function () {
  var fn = function () {
    throw new TypeError('type error');
  };

  should.throws(function () {
    uglyHandlerImproved(fn);
  }, SpecifiedError);
});
</code></pre>
<p>The specified error adds more details and keeps the original error message. With this improvement it is no longer an ugly handler but clean and useful.</p>
<p>With these handlers, I still get an unhandled exception. Let’s see if the browser has something up its sleeve to deal with this.</p>
<h2 id="unwindthatstack">Unwind that Stack</h2>
<p>So, one way to unwind exceptions is to place a <code>try...catch</code> at the top of the call stack.</p>
<p>Say for example:</p>
<pre><code>function main(bomb) {
  try {
    bomb();
  } catch (e) {
    // Handle all the error things
  }
}
</code></pre>
<p>But, remember I said the browser is event-driven? Yes, an exception in JavaScript is no more than an event. The interpreter halts execution in the executing context and unwinds. Turns out, there is an <a href="https://developer.mozilla.org/en/docs/Web/API/GlobalEventHandlers/onerror" target="_blank">onerror global event handler</a> we can use.</p>
<p>And it goes something like this:</p>
<pre><code>// scripts/errorHandlerDom.js

window.addEventListener('error', function (e) {
  var error = e.error;
  console.log(error);
});
</code></pre>
<p>This event handler catches errors within any executing context. Error events get fired from various targets for any kind of error. What is so radical is this event handler centralizes error handling in the code. Like with any other event, you can daisy chain handlers to handle specific errors. This allows error handlers to have a single purpose if you follow <a href="https://en.wikipedia.org/wiki/SOLID_" title="object-oriented_design" target="_blank">SOLID</a> principles. These handlers can get registered at any time. The interpreter will cycle through as many handlers as it needs to. The code base gets freed from <code>try...catch</code> blocks that get peppered all over which makes it easy to debug. The key is to treat error handling like event handling in JavaScript.</p>
<p>Now that there is a way to unwind the stack with global handlers, what can we do with this?</p>
<p>After all, may the call stack be with you.</p>
<h2 id="capturethestack">Capture the Stack</h2>
<p>The call stack is super helpful in troubleshooting issues. The good news is that the browser provides this information out of the box. The <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error/Stack" target="_blank">stack property</a> is not part of the standard, but it is consistently available on the latest browsers.</p>
<p>So, for example, you can now log errors on the server:</p>
<pre><code>// scripts/errorAjaxHandlerDom.js

window.addEventListener('error', function (e) {
  var stack = e.error.stack;
  var message = e.error.toString();

  if (stack) {
    message += '\n' + stack;
  }

  var xhr = new XMLHttpRequest();
  xhr.open('POST', '/log', true);
  // Fire an Ajax request with error details
  xhr.send(message);
});
</code></pre>
<p>It may not be obvious from this example, but this will fire alongside the previous example. Every error handler can have a single purpose which keeps the code <a href="https://en.wikipedia.org/wiki/Don%27t_repeat_yourself" target="_blank">DRY</a>.</p>
<p>In the browser, event handlers get <em>appended</em> to the DOM. This means if you are building a third party library, your events will coexist with client code. The <code>window.addEventListener()</code> takes care of this for you, it does not blot out existing events.</p>
<p>Here is a screenshot of what this log looks like on the server:</p>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/05/1496102455proper_error_handling_javascript_2.png" alt="Ajax Log Request to Node Server" /></div></p>
<p>This log lives inside a command prompt, yes, it is unapologetically running on Windows.</p>
<p>This message comes from Firefox Developer Edition 54. With a proper error handler, note that it is crystal clear what the issue is. No need to hide mistakes, by glancing at this, I can see what threw the exception and where. This level of transparency is good for debugging front-end code. You can analyze logs, giving insight on what conditions trigger which errors.</p>
<p>The call stack is helpful for debugging, never underestimate the power of the call stack.</p>
<p>One gotcha is if you have a script from a different domain and <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS" target="_blank">enable CORS</a> you won’t see any of the error details. This occurs when you put scripts on a CDN, for example, to exploit the limitation of six requests per domain. The <code>e.message</code> will only say “Script error” which is bad. In JavaScript, error information is only available for a single domain.</p>
<p>One solution is to re-throw errors while keeping the error message:</p>
<pre><code>try {
  return fn();
} catch (e) {
  throw new Error(e.message);
}
</code></pre>
<p>Once you rethrow the error back up, your global error handlers will do the rest of the work. Only make sure your error handlers are on the same domain. You can even wrap it around a custom error with specific error information. This keeps the original message, stack, and custom error object.</p>
<h2 id="asynchandling">Async Handling</h2>
<p>Ah, the perils of asynchrony. JavaScript rips asynchronous code out of the executing context. This means exception handlers such as the one below have a problem:</p>
<pre><code>// scripts/asyncHandler.js

function asyncHandler(fn) {
  try {
    // This rips the potential bomb from the current context
    setTimeout(function () {
      fn();
    }, 1);
  } catch (e) { }
}
</code></pre>
<p>The unit test tells the rest of the story:</p>
<pre><code>// tests/scripts/asyncHandlerTest.js

it('does not catch exceptions with errors', function () {
  // The bomb
  var fn = function () {
    throw new TypeError('type error');
  };

  // Check that the exception is not caught
  should.doesNotThrow(function () {
    asyncHandler(fn);
  });
});
</code></pre>
<p>The exception does not get caught and I can verify this with this unit test. Note that an unhandled exception occurs, although I have the code wrapped around a nice <code>try...catch</code>. Yes, <code>try...catch</code> statements only work within a single executing context. By the time an exception gets thrown, the interpreter has moved away from the <code>try...catch</code>. This same behavior occurs with Ajax calls too.</p>
<p>So, one alternative is to catch exceptions inside the asynchronous callback:</p>
<pre><code>setTimeout(function () {
  try {
    fn();
  } catch (e) {
    // Handle this async error
  }
}, 1);
</code></pre>
<p>This approach will work, but it leaves much room for improvement. First of all, <code>try...catch</code> blocks get tangled up all over the place. In fact, 1970s bad programming called and they want their code back. Plus, the V8 engine discourages the use of <a href="https://github.com/nodejs/node-v0.x-archive/wiki/Best-practices-and-gotchas-with-v8" target="_blank">try…catch blocks inside functions</a>. V8 is the JavaScript engine used in the Chrome browser and Node. One idea is to move blocks to the top of the call stack but this does not work for asynchronous code.</p>
<p>So, where does this lead us? There is a reason I said global error handlers operate within any executing context. If you add an error handler to the window object, that’s it, done! It is nice that the decision to stay DRY and SOLID is paying off. A global error handler will keep your async code nice and clean.</p>
<p>Below is what this exception handler reports on the server. Note that if you’re following along, the output you see will be different depending on which browser you use.</p>
<p><div class="readableLargeImageContainer"><img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2017/05/1496102759proper_error_handling_javascript_3.png" alt="Async Error Report on the Server" /></div></p>
<p>This handler even tells me that the error is coming from asynchronous code. It says it is coming from a <code>setTimeout()</code> function. Too cool!</p>
<h2 id="conclusion">Conclusion</h2>
<p>In the world of error handling, there are at least two approaches. One is the fail-silent approach where you ignore errors in the code. The other is the fail-fast and unwind approach where errors stop the world and rewind. I think it is clear which of the two I am in favor of and why. My take: don’t hide problems. No one will shame you for accidents that may occur in the program. It is acceptable to stop, rewind and give users another try.</p>
<p>In a world that is far from perfect, it is important to allow for a second chance. Errors are inevitable, it’s what you do about them that counts.</p>
<p><em>This article was peer reviewed by <a href="http://www.sitepoint.com/author/tseverien/" target="_blank">Tim Severien</a> and <a href="http://www.sitepoint.com/author/morkro/" target="_blank">Moritz Kröger</a>. Thanks to all of SitePoint’s peer reviewers for making SitePoint content the best it can be!</em></p>
      <div>
        <div>
          
          <div>
            <div>Meet the author</div>
            
          </div>
        </div>
        <div>Husband, father, and software engineer living in Houston Texas. Passionate about JavaScript and cyber-ing all the things.</div>
      </div>
      
      
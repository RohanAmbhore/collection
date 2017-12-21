<a href="http://blog.bloomca.me/2017/12/19/how-to-use-generators.html?utm_source=mybridge&utm_medium=web&utm_campaign=read_more">http://blog.bloomca.me/2017/12/19/how-to-use-generators.html?utm_source=mybridge&utm_medium=web&utm_campaign=read_more</a><div id="articleHeader"><h1>How to Use Generators in JavaScript</h1></div>


  <p>Generators are a very powerful concept, but it is not used that often (see the twitter poll!). Why is it so? They are more sophisticated than async/await, not so easy to debug (mostly back to the old days), and people in general like async/await more, even despite the fact that we can achieve similar experience in a really easy way.</p>




<p>However, generators allow us to iterate over <code>yield</code> keywords using our own code! This is a super powerful concept, and we can actually manipulate the execution! To start with not so obvious cancelling, let’s start with synchronous operations.</p>

<blockquote>
  <p>I’ve created a repository with functions from this article – <a href="https://github.com/Bloomca/obscure-generator-fns" target="_blank">https://github.com/Bloomca/obscure-generator-fns</a></p>
</blockquote>

<h2 id="batching-or-scheduling">Batching (or Scheduling)</h2>

<p>Generators return iterators, and it means we can actually iterate over it synchronously. Why would we want to? Well, the reason might be batching. Imagine that we download 10,000 items, and display them as rows in our table (don’t ask me why, and let’s assume we have no framework).
While there is nothing bad in showing them immediately, sometimes it might not be the best solution – maybe your MacBook Pro can handle it, but the average person’s laptop cannot (not to mention mobiles). So, it means we need to somehow delay the execution.</p>

<blockquote>
  <p>Please note that this example is about performance optimization, and you should not do it until you actually hit this issue – premature optimization <a href="https://en.wikipedia.org/wiki/Program_optimization#When_to_optimize" target="_blank">is evil</a>!</p>
</blockquote>

<div><div><pre><code>// our original synchronous function
function renderItems(items) {
  for (item of items) {
    renderItem(item);
  }
}

// function which will be run by our runner
// in fact, we can execute it in the same
// synchronous manner!
function* renderItems(items) {
  // I use for..of iterator to avoid
  // new functions creation
  for (item of items) {
    yield renderItem(item);
  }
}
</code></pre></div></div>

<p>There is no difference, huh? Well, the difference here is that now we can run this function differently, without changing the source code – so it means we can actually tweak it very easily. In fact, as I’ve mentioned before, there is no need to actually wait, we can execute it synchronously.
So, let’s tweak our code. What about adding 4ms (one tick in JS VM) sleep after each yield? Well, given that it is 10,000 items, it will take 4 seconds – which is not bad, but let’s say I want to render it in 2 seconds. The obvious answer is to chunk them by two, and all of the sudden the same solution using promises will start to become more complicated – we’ll have to pass another parameter: number of elements in the chunk. With our runner, we still need to pass this number, but the beauty is that we don’t have to affect our <code>renderItems</code> function at all!</p>

<div><div><pre><code>function runWithBatch(chunk, fn, ...args) {
  const gen = fn(...args);
  let num = 0;
  return new Promise((resolve, promiseReject) =&gt; {
    callNextStep();

    function callNextStep(res) {
      let result;
      try {
        result = gen.next(res);
      } catch (e) {
        return reject(e);
      }
      next(result);
    }

    function next({ done, value }) {
      if (done) {
        return resolve(value);
      }

      // every chunk we sleep for a tick
      if (num++ % chunk === 0) {
        return sleep(4).then(proceed);
      } else {
        return proceed();
      }
      
      function proceed() {
        return callNextStep(value);
      }
    }
  });
}

// first arg – how many items are processed in one batch
const items = [...];
batchRunner(2, function*() {
  for (item of items) {
    yield renderItem(item);
  }
});
</code></pre></div></div>

<p>As you can see, we can easily change the number of items in the chunk, throw this runner away and switch back to usual synchronous execution – and all of this won’t affect our <code>renderItems</code> function.</p>

<h2 id="cancellation">Cancellation</h2>

<p>Let’s go to more traditional stuff – cancelling. I’ve touched on it extensively in my article about <a href="http://blog.bloomca.me/2017/12/04/how-to-cancel-your-promise.html" target="_blank">promises cancellation in general</a>, so I’ll reuse code from it:</p>

<div><div><pre><code>function runWithCancel(fn, ...args) {
  const gen = fn(...args);
  let cancelled, cancel;
  const promise = new Promise((resolve, promiseReject) =&gt; {
    // define cancel function to return it from our fn
    cancel = () =&gt; {
      cancelled = true;
      reject({ reason: 'cancelled' });
    };

    onFulfilled();

    function onFulfilled(res) {
      if (!cancelled) {
        let result;
        try {
          result = gen.next(res);
        } catch (e) {
          return reject(e);
        }
        next(result);
        return null;
      }
    }

    function onRejected(err) {
      var result;
      try {
        result = gen.throw(err);
      } catch (e) {
        return reject(e);
      }
      next(result);
    }

    function next({ done, value }) {
      if (done) {
        return resolve(value);
      }
      // we assume we always receive promises, so no type checks
      return value.then(onFulfilled, onRejected);
    }
  });
  
  return { promise, cancel };
}
</code></pre></div></div>

<p>The best part here is that we cancel all requests which were not able to execute yet (as well as we can pass something like <a href="https://developer.mozilla.org/en-US/docs/Web/API/AbortController" target="_blank">AbortController</a> to our runner, so it can even cancel the current request!), and we did not change even one line in our business logic!</p>

<h2 id="pauseresume">Pause/Resume</h2>

<p>Another special requirement might be pause/resume functionality. Why would you want it? Imagine we render our 10,000 rows, and it is pretty slow, and we want to give the power to pause/resume rendering to the user, so they can stop all background work and read already downloaded content. Let’s do that:</p>

<div><div><pre><code>// our function is still the same!
function* renderItems() {
  for (item of items) {
    yield renderItem(item);
  }
}

function runWithPause(genFn, ...args) {
  let pausePromiseResolve = null;
  let pausePromise;

  const gen = genFn(...args);

  const promise = new Promise((resolve, reject) =&gt; {
    onFulfilledWithPromise();

    function onFulfilledWithPromise(res) {
      if (pausePromise) {
        pausePromise.then(() =&gt; onFulfilled(res));
      } else {
        onFulfilled(res);
      }
    }

    function onFulfilled(res) {
      let result;
      try {
        result = gen.next(res);
      } catch (e) {
        return reject(e);
      }
      next(result);
      return null;
    }

    function onRejected(err) {
      var result;
      try {
        result = gen.throw(err);
      } catch (e) {
        return reject(e);
      }
      next(result);
    }

    function next({ done, value }) {
      if (done) {
        return resolve(value);
      }
      // we assume we always receive promises, so no type checks
      return value.then(onFulfilledWithPromise, onRejected);
    }
  });

  return {
    pause: () =&gt; {
      pausePromise = new Promise(resolve =&gt; {
        pausePromiseResolve = resolve;
      });
    },
    resume: () =&gt; {
      pausePromiseResolve();
      pausePromise = null;
    },
    promise
  };
}
</code></pre></div></div>

<p>Calling this runner will give us an object with pause/resume buttons, and all of that for free, using our previous function! So, if you have a lot of “heavy” request chains, which can take several seconds, and you want to give your user power to pause and resume them, feel free to implement this runner in your codebase.</p>

<h2 id="error-handling">Error Handling</h2>

<p>We had this mysterious <code>onRejected</code> call, which is our main target for this section. If we use normal async/await or promise chaining, we fall through our try/catch, and it is really hard to recover to our point of failure without adding a lot of logic. The usual scenario is if we need to somehow handle the error (retry the call, for example), we just do it inside the internal promise, which will handle itself and call the same endpoint again.
However, as usual, it is not a generic solution – and the sad part is, that even generators can’t help us here. We hit the limitation of generators here – while we can control the execution flow, we cannot move around our generator function’s body; so we cannot return one step back and re-execute our command again. One possible solution is to use <a href="https://en.wikipedia.org/wiki/Command_pattern" target="_blank">command pattern</a>, which (unfortunately) dictates us the structure of everything we yield – it should be all the info we need to execute this command, this way we will be able to execute it again. So, our function will be changed to:</p>

<div><div><pre><code>function* renderItems() {
  for (item of items) {
    // we had to pass everything:
    // fn, context, arguments
    yield [renderItem, null, item];
  }
}
</code></pre></div></div>

<p>As you can see, it makes it very unclear what is going on – so, maybe it would be better to write some sort of <code>wrapWithRetry</code> function, which will check what is the type of error in the <code>catch</code> handler, and try again.
However, we still can do something without affecting our function. For example, we can decide on a strategy about ignoring errors – in async/await we’d have to wrap each call in try/catch, or add empty <code>.catch(() =&gt; {})</code> part. With generators we can just write a runner which will ignore all errors.</p>

<div><div><pre><code>function runWithIgnore(fn, ...args) {
  const gen = fn(...args);
  return new Promise((resolve, promiseReject) =&gt; {
    onFulfilled();

    function onFulfilled(res) {
      proceed({ data: res });
    }

    // these are errors from yielded promises
    // and we want to ignore them
    // so we act like usual, except we pass an error
    function onRejected(error) {
      proceed({ error });
    }

    function proceed(data) {
      let result;
      try {
        result = gen.next(data);
      } catch (e) {
        // these errors are sync errors (like TypeError, etc)
        return reject(e);
      }
      // in order to differentiate errors and normal results
      // we execute it with
      next(result);
    }

    function next({ done, value }) {
      if (done) {
        return resolve(value);
      }
      // we assume we always receive promises, so no type checks
      return value.then(onFulfilled, onRejected);
    }
  });
}
</code></pre></div></div>

<h2 id="note-about-asyncawait">Note About async/await</h2>

<p>Async/await is a preferred syntax nowadays (and even <a href="https://github.com/tj/co#co-v4" target="_blank">co</a> talks about it), and it is the future. However, generators are inside the ECMAScript standard, and it means that in order to use them, you don’t need anything, except writing several utility functions. I’ve tried to show you not-so-trivial examples, and it is up to you to decide whether it is worth it or not. Remember, not so many people are familiar with generators, and in case you have only one place to use them in the whole codebase, it might be easier to work around using promises – but on the other side, some problems can be solved especially beautifully and concisely with generators.</p>

<p>Be wise in your choice – with great power comes great responsibility (Spiderman, 2004)!</p>


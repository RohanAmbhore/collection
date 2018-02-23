<a href="https://skyronic.com/blog/vuejs-internals-computed-properties">https://skyronic.com/blog/vuejs-internals-computed-properties</a><div id="articleHeader"><h1><a href="/blog/vuejs-internals-computed-properties" target="_blank">Vue.js Internals: How computed properties work</a></h1></div>
        
                
             December 2, 2016, 5:04 pm
        
                    

    

            <p>In this post, we will more learn about how <a href="https://vuejs.org/v2/guide/computed.html" target="_blank">Vue.js Computed Properties</a> work by writing a very (very very very) simple implementation which achieves similar functionality.</p>
<ol>
<li>This is just to illustrate how it works. It doesn't support objects, arrays, watching/unwatching and a dozen performance optimizations that exist in vue.js core.</li>
<li>I wrote this after reading the Vue.js source code, based on my very limited understanding. <strong>A lot of it might be wrong.</strong> Please <a href="mailto:skyronic@gmail.com" target="_blank">email me</a> if you find any corrections or if I'm flat out wrong.</li>
</ol>

<h3>JS Properties</h3>
<p>JavaScript has a <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty" target="_blank">feature</a> <code>Object.defineProperty</code>. It can do quite a bit but let's focus on one thing:</p>
<pre><code>var person = {};

Object.defineProperty (person, 'age', {
  get: function () {
    console.log ("Getting the age");
    return 25;
  }
});

console.log ("The age is ", person.age);

// Prints:
//
// Getting the age
// The age is 25
</code></pre>
<p>Even though <code>person.age</code> looks like we're accessing a part of the object, we're internally running a function.</p>
<h3>A basic Vue.js Observable</h3>
<p>Vue.js has a basic construct which lets you turn a regular object into an "observed" value called an "observable". Here's an over-simplified version of how to add a <strong>reactive property</strong></p>
<pre><code>function defineReactive (obj, key, val) {
  Object.defineProperty (obj, key, {
    get: function () {
      return val;
    },
    set: function (newValue) {
      val = newValue;
    }
  })
};

// create an object
var person = {};

// add a reactive property called 'age' and 'country'
defineReactive (person, 'age', 25);
defineReactive (person, 'country', 'Brazil');

// now you can use `person.age` any way you please
if (person.age &lt; 18) {
  return 'minor';
}
else {
  return 'adult';
}

// Set a value as well.
person.country = 'Russia';
</code></pre>
<p>Interestingly, the actual value <code>25</code> and <code>'Brazil'</code> is still inside a "closure variable" <code>val</code> and is modified when you set the value. <code>person.country</code> doesn't contain the actual value, instead the getter function's closure contains the value.</p>
<h3>Defining a computed property</h3>
<p>Let's create a function for defining a computed property <code>defineComputed</code>. This is how a user might use it.</p>
<pre><code>defineComputed (
  person, // the object to create computed property on
  'status', // the name of the computed property
  function () { // the function which actually computes the property
    console.log ("status getter called")
    if (person.age &lt; 18) {
      return 'minor';
    }
    else {
      return 'adult';
    }
  },
  function (newValue) {
    // called when the computed value is updated
    console.log ("status has changed to", newValue)
  }
});

// We can use the computed property like a regular property
console.log ("The person's status is: ", person.status);
</code></pre>
<p>Let us write a simple implementation of <code>defineComputed</code>. This will support calling the compute function, we won't support <code>updateCallback</code> right now</p>
<pre><code>function defineComputed (obj, key, computeFunc, updateCallback) {
  Object.defineProperty (obj, key, {
    get: function () {
      // call the compute function and return the value
      return computeFunc ();
    },
    set: function () {
      // don't do anything. can't set computed funcs
    }
  })
}</code></pre>
<p>There are some issues with this:</p>
<ol>
<li>It'll run the compute function each time the propety is accessed.</li>
<li>It doesn't know when to update.</li>
</ol>
<pre><code>// We want something like this to happen

person.age = 17;
// console: status has changed to: minor

person.age = 22;
// console: status has changed to: adult
</code></pre>
<h3>Adding a dependency tracker.</h3>
<p>Let's add a global object called <code>Dep</code></p>
<pre><code>var Dep = {
  target: null
};</code></pre>
<p>This is the 'dependency tracker'. Let's modify the <code>defineComputed</code> function with one key trick.</p>
<pre><code>function defineComputed (obj, key, computeFunc, updateCallback) {
  var onDependencyUpdated = function () {
    // TODO
  }
  Object.defineProperty (obj, key, {
    get: function () {
      // Set the dependency target as this function
      Dep.target = onDependencyUpdated;
      var value = computeFunc ();
      Dep.target = null;
    },
    set: function () {
      // don't do anything. can't set computed funcs
    }
  })
}</code></pre>
<p>Let's now go back to how we define a reactive property.</p>
<pre><code>function defineReactive (obj, key, val) {
  // all computed properties that depend on this
  var deps = [];

  Object.defineProperty (obj, key, {
    get: function () {
      // Check if there's a computed property which 'invoked'
      // this getter. Also check that it's already not a dependency
      if (Dep.target && ) {
        // add the dependency
        deps.push (target);
      }

      return val;
    },
    set: function (newValue) {
      val = newValue;

      // notify all dependent computed properties
      deps.forEach ((changeFunction) =&gt; {
        // Request recalculation and update
        changeFunction ();
      });
    }
  })
};</code></pre>
<p>We can update the <code>onDependencyUpdated</code> function in the computed property definition to now trigger the update callback.</p>
<pre><code>var onDependencyUpdated = function () {
  // compute the value again
  var value = computeFunc ();
  updateCallback (value);
}</code></pre>
<h3>Putting it all together.</h3>
<p>Let's re-visit the definition of our computed property <code>person.status</code></p>
<pre><code>person.age = 22;

defineComputed (
  person,
  'status',
  function () {
    // compute function
    if (person.age &gt; 18) {
      return 'adult';
    }
  },
  function (newValue) {
    console.log ("status has changed to", newValue)
  }
});

console.log ("Status is ", person.status);</code></pre>
<h4>Step 1:</h4>
<p><code>get()</code> is called on the <code>person.status</code> property. This sets <code>Dep.target</code> to it's callback.</p>
<p><div class="readableLargeImageContainer"><img src="/user/pages/01.blog/vuejs-internals-computed-properties/compprop1.png" /></div></p>
<h4>Step 2:</h4>
<p><code>get()</code> on <code>person.status</code> calls the compute function. This in turn calls <code>get()</code> on <code>person.age</code> property because the callback function needs this value.</p>
<p><div class="readableLargeImageContainer"><img src="/user/pages/01.blog/vuejs-internals-computed-properties/compprop2.png" /></div></p>
<h4>Step 3:</h4>
<p><code>person.age</code>'s <code>get()</code> checks with <code>Dep</code> to see if a target is available. And stores it as a dependency</p>
<p><div class="readableLargeImageContainer"><img src="/user/pages/01.blog/vuejs-internals-computed-properties/compprop3.png" /></div></p>
<h4>Step 4:</h4>
<p>The compute function gets the new value and returns it. But now <code>person.age</code> knows to notify <code>person.status</code> whenever it's value updates.</p>
<p><div class="readableLargeImageContainer"><img src="/user/pages/01.blog/vuejs-internals-computed-properties/compprop4.png" /></div></p>
<h2>Live example</h2>
<p><a href="http://jsbin.com/vevupup/embed?js,console" target="_blank">JS Bin on jsbin.com</a></p><p>
                            <a href="/blog/dealing-with-a-major-finger-injury-thenar-flap" target="_blank"> Next Post</a>
            
                            <a href="/blog/collection-pipelines-with-vue-js" target="_blank">Previous Post </a>
                    </p>
    
    
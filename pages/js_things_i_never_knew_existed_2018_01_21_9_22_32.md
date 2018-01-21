<a href="https://air.ghost.io/js-things-i-never-knew-existed/">https://air.ghost.io/js-things-i-never-knew-existed/</a><div id="articleHeader"><h1>JS things I never knew existed</h1></div>

            

            
                <p>I was reading through the MDN docs the other day and found these JS features and APIs I never knew existed. So here is a short list of those things, useful or not - learning JS seemingly never ends.</p>
<h2 id="labelstatements"><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/label" target="_blank">Label Statements</a></h2>
<p>You can name <code>for</code> loops and blocks in JS... who knew (not me)! You can then refer to that name and use <code>break</code> or <code>continue</code> in <code>for</code> loops and <code>break</code> in blocks.</p>
<pre><code>loop1: // labeling "loop1" 
for (let i = 0; i &lt; 3; i++) { // "loop1"
   loop2: // labeling "loop2"
   for (let j = 0; j &lt; 3; j++) { // "loop2"
      if (i === 1) {
         continue loop1; // continues upper "loop1"
         // break loop1; // breaks out of upper "loop1"
      }
      console.log(`i = ${i}, j = ${j}`);
   }
}

/* 
 * # Output
 * i = 0, j = 0
 * i = 0, j = 1
 * i = 0, j = 2
 * i = 2, j = 0
 * i = 2, j = 1
 * i = 2, j = 2
 */
</code><div><div><a target="_blank">Copy</a></div></div></pre>
<p>Here is an example of block naming, you can only use <code>break</code> in blocks.</p>
<pre><code>foo: {
  console.log('one');
  break foo;
  console.log('this log will not be executed');
}
console.log('two');

/*
 * # Output
 * one
 * two
 */
</code><div><div><a target="_blank">Copy</a></div></div></pre>
<h2 id="voidoperator"><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/void" target="_blank">"void" Operator</a></h2>
<p>I thought I knew all the operators until I saw this one which has been in <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/1.1" target="_blank">JS since 1996</a>. It's supported by all browers and its pretty easy to understand, quote from MDN:</p>
<blockquote>
<p>The void operator evaluates the given expression and then returns undefined.</p>
</blockquote>
<p>This allow you to write an alternative IIFE like this:</p>
<pre><code>void function iife() {
	console.log('hello');
}();

// is the same as...

(function iife() {
    console.log('hello');
})()
</code><div><div><a target="_blank">Copy</a></div></div></pre>
<p>One cavaet with <code>void</code> is the evaluation of the expression is... void (undefined)!</p>
<pre><code>const word = void function iife() {
	return 'hello';
}();

// word is "undefined"

const word = (function iife() {
	return 'hello';
})();

// word is "hello"
</code><div><div><a target="_blank">Copy</a></div></div></pre>
<p>You can also use <code>void</code> with <code>async</code>, you could then use it as an asynchronous entry point to your code:</p>
<pre><code>void async function() { 
    try {
        const response = await fetch('air.ghost.io'); 
        const text = await response.text();
        console.log(text);
    } catch(e) {
        console.error(e);
    }
}()

// or just stick to this :)

(async () =&gt; {
    try {
        const response = await fetch('air.ghost.io'); 
        const text = await response.text();
        console.log(text);
    } catch(e) {
        console.error(e);
    }
})();
</code><div><div><a target="_blank">Copy</a></div></div></pre>
<h2 id="commaoperator"><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comma_Operator" target="_blank">Comma Operator</a></h2>
<p>After reading about the comma operator, I realised I was not fully aware of how it works. Here is a good quote from MDN:</p>
<blockquote>
<p>The comma operator evaluates each of its operands (from left to right) and returns the value of the last operand.</p>
</blockquote>
<pre><code>function myFunc() {
  let x = 0;
  return (x += 1, x); // same as return ++x;
}

y = false, true; // returns true in console
console.log(y); // false (left-most)

z = (false, true); // returns true in console
console.log(z); // true (right-most)
</code><div><div><a target="_blank">Copy</a></div></div></pre>
<h3 id="withconditionaloperator">With <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator" target="_blank">Conditional Operator</a></h3>
<p>The last value in the comma operator becomes the return value for the conditional. So you can put any number of expressions before it, in the example below I put a console log before the returned boolean value.</p>
<pre><code>const type = 'man';

const isMale = type === 'man' ? (
    console.log('Hi Man!'),
    true
) : (
    console.log('Hi Lady!'),
    false
);

console.log(`isMale is "${isMale}"`);
</code><div><div><a target="_blank">Copy</a></div></div></pre>
<h2 id="internationalizationapi"><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl" target="_blank">Internationalization API</a></h2>
<p>Internationalization is difficult to get right at the best of times, luckily there is a <a href="https://caniuse.com/#feat=internationalization" target="_blank">well supported</a> API for it now in most browsers. One of my favourite features from it is the date formatter, see example below.</p>
<pre><code>const date = new Date();

const options = {
  year: 'numeric', 
  month: 'long', 
  day: 'numeric'
};

const formatter1 = new Intl.DateTimeFormat('es-es', options);
console.log(formatter1.format(date)); // 22 de diciembre de 2017

const formatter2 = new Intl.DateTimeFormat('en-us', options);
console.log(formatter2.format(date)); // December 22, 2017
</code><div><div><a target="_blank">Copy</a></div></div></pre>
<h2 id="pipelineoperator"><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Pipeline_operator" target="_blank">Pipeline Operator</a></h2>
<p>At time of writing this is only supported in Firefox 58+ behind a flag, however Babel does already have a proposal plugin for it <a href="https://github.com/babel/babel/tree/master/packages/babel-plugin-proposal-pipeline-operator" target="_blank">here</a>. It looks very bash inspired and I like it!</p>
<pre><code>const square = (n) =&gt; n * n;
const increment = (n) =&gt; n + 1;

// without pipeline operator
square(increment(square(2))); // 25

// with pipeline operator
2 |&gt; square |&gt; increment |&gt; square; // 25
</code><div><div><a target="_blank">Copy</a></div></div></pre>
<h1 id="notablementions">Notable Mentions</h1>
<h2 id="atomics"><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Atomics" target="_blank">Atomics</a></h2>
<p>Atomic operations give predictable read and write values when data is shared between the multiple threads, waiting for other operations to finish before the next one is executed. Useful for keeping data in sync between things like the main thread and another WebWorker.</p>
<p>I really like Atomics in other languages like Java. I feel these will be used more in JS when more of us use WebWorkers to move operations away from the main thread.</p>
<h2 id="arrayprototypereduceright"><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/ReduceRight" target="_blank">Array.prototype.reduceRight</a></h2>
<p>Ok, I've never seen this used because its basically <code>Array.prototype.reduce()</code> + <code>Array.prototype.reverse()</code> and its quite rare you need to do that. If you do... then <code>reduceRight</code> is perfect!</p>
<pre><code>const flattened = [[0, 1], [2, 3], [4, 5]].reduceRight(function(a, b) {
    return a.concat(b);
}, []);

// flattened array is [4, 5, 2, 3, 0, 1]
</code><div><div><a target="_blank">Copy</a></div></div></pre>
<h2 id="settimeoutparameters"><a href="https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval" target="_blank">setTimeout() Parameters</a></h2>
<p>I could of probably saved myself a <code>.bind(...)</code> or two by knowing this - and it's been around forever.</p>
<pre><code>setTimeout(alert, 1000, 'Hello world!');

/*
 * # Output (alert)
 * Hello World!
 */

function log(text, textTwo) {
    console.log(text, textTwo);
}

setTimeout(log, 1000, 'Hello World!', 'And Mars!');

/*
 * # Output
 * Hello World! And Mars!
 */
</code><div><div><a target="_blank">Copy</a></div></div></pre>
<h2 id="htmlelementdataset"><a href="https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dataset" target="_blank">HTMLElement.dataset</a></h2>
<p>I had used custom data attributes <code>data-*</code> on HTML elements before now but I blissfully was unaware there was an API to query them easily. Apart from a few naming restrictions (see link above) it's essentially dash-case naming for attributes and camelCase when querying them in JS. So attribute <code>data-birth-planet</code> would become <code>birthPlanet</code> in JS.</p>
<pre><code>&lt;div id='person' data-name='john' data-birth-planet='earth'&gt;&lt;/div&gt;
</code><div><div><a target="_blank">Copy</a></div></div></pre>
<p>Query:</p>
<pre><code>let personEl = document.querySelector('#person');

console.log(person.dataset) // DOMStringMap {name: "john", birthPlanet: "earth"}
console.log(personEl.dataset.name) // john
console.log(personEl.dataset.birthPlanet) // earth

// you can programmatically add more too
personEl.dataset.foo = 'bar';
console.log(personEl.dataset.foo); // bar
</code><div><div><a target="_blank">Copy</a></div></div></pre>

<p>Hope you discovered something new in the list for JS like I did. Shout out to Mozilla for the new MDN site, looks much nicer in my opinion - I spent way longer than I thought reading through it.</p>
<p><em>Edit: Fixed some naming and added <code>try</code>, <code>catch</code> to <code>async</code> functions. Thanks Reddit!</em></p>
<p>Happy New 2018!</p>

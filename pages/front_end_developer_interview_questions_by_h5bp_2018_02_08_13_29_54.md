<a href="https://h5bp.github.io/Front-end-Developer-Interview-Questions/">https://h5bp.github.io/Front-end-Developer-Interview-Questions/</a><div id="articleHeader"><h1>Front-end Job Interview Questions</h1></div>

<p>This file contains a number of front-end interview questions that can be used when vetting potential candidates. It is by no means recommended to use every single question here on the same candidate (that would take hours). Choosing a few items from this list should help you vet the intended skills you require.</p>

<p><strong>Note:</strong> Keep in mind that many of these questions are open-ended and could lead to interesting discussions that tell you more about the person's capabilities than a straight answer would.</p>

<h2>
Table of Contents</h2>



<h2>
Getting Involved</h2>



<h4>
General Questions:</h4>

<ul>
<li>What did you learn yesterday/this week?</li>
<li>What excites or interests you about coding?</li>
<li>What is a recent technical challenge you experienced and how did you solve it?</li>
<li>What UI, Security, Performance, SEO, Maintainability or Technology considerations do you make while building a web application or site?</li>
<li>Talk about your preferred development environment.</li>
<li>Which version control systems are you familiar with?</li>
<li>Can you describe your workflow when you create a web page?</li>
<li>If you have 5 different stylesheets, how would you best integrate them into the site?</li>
<li>Can you describe the difference between progressive enhancement and graceful degradation?</li>
<li>How would you optimize a website's assets/resources?</li>
<li>How many resources will a browser download from a given domain at a time?

<ul>
<li>What are the exceptions?</li>
</ul>
</li>
<li>Name 3 ways to decrease page load (perceived or actual load time).</li>
<li>If you jumped on a project and they used tabs and you used spaces, what would you do?</li>
<li>Describe how you would create a simple slideshow page.</li>
<li>If you could master one technology this year, what would it be?</li>
<li>Explain the importance of standards and standards bodies.</li>
<li>What is Flash of Unstyled Content? How do you avoid FOUC?</li>
<li>Explain what ARIA and screenreaders are, and how to make a website accessible.</li>
<li>Explain some of the pros and cons for CSS animations versus JavaScript animations.</li>
</ul>

<h4>
HTML Questions:</h4>

<ul>
<li>What does a <code>doctype</code> do?</li>
<li>What's the difference between standards mode and quirks mode?</li>
<li>What's the difference between HTML and XHTML?</li>
<li>Are there any problems with serving pages as <code>application/xhtml+xml</code>?</li>
<li>How do you serve a page with content in multiple languages?</li>
<li>What kind of things must you be wary of when design or developing for multilingual sites?</li>
<li>What are <code>data-</code> attributes good for?</li>
<li>Consider HTML5 as an open web platform. What are the building blocks of HTML5?</li>
<li>Describe the difference between a <code>cookie</code>, <code>sessionStorage</code> and <code>localStorage</code>.</li>
<li>Describe the difference between <code>&lt;script&gt;</code>, <code>&lt;script async&gt;</code> and <code>&lt;script defer&gt;</code>.</li>
<li>Why is it generally a good idea to position CSS <code>&lt;link&gt;</code>s between <code>&lt;head&gt;&lt;/head&gt;</code> and JS <code>&lt;script&gt;</code>s just before <code>&lt;/body&gt;</code>? Do you know any exceptions?</li>
<li>What is progressive rendering?</li>
<li>Have you used different HTML templating languages before?</li>
</ul>

<h4>
CSS Questions:</h4>

<ul>
<li>What is the difference between classes and ID's in CSS?</li>
<li>What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?</li>
<li>Describe Floats and how they work.</li>
<li>Describe z-index and how stacking context is formed.</li>
<li>Describe BFC(Block Formatting Context) and how it works.</li>
<li>What are the various clearing techniques and which is appropriate for what context?</li>
<li>Explain CSS sprites, and how you would implement them on a page or site.</li>
<li>What are your favourite image replacement techniques and which do you use when?</li>
<li>How would you approach fixing browser-specific styling issues?</li>
<li>How do you serve your pages for feature-constrained browsers?

<ul>
<li>What techniques/processes do you use?</li>
</ul>
</li>
<li>What are the different ways to visually hide content (and make it available only for screen readers)?</li>
<li>Have you ever used a grid system, and if so, what do you prefer?</li>
<li>Have you used or implemented media queries or mobile specific layouts/CSS?</li>
<li>Are you familiar with styling SVG?</li>
<li>How do you optimize your webpages for print?</li>
<li>What are some of the "gotchas" for writing efficient CSS?</li>
<li>What are the advantages/disadvantages of using CSS preprocessors?

<ul>
<li>Describe what you like and dislike about the CSS preprocessors you have used.</li>
</ul>
</li>
<li>How would you implement a web design comp that uses non-standard fonts?</li>
<li>Explain how a browser determines what elements match a CSS selector.</li>
<li>Describe pseudo-elements and discuss what they are used for. </li>
<li>Explain your understanding of the box model and how you would tell the browser in CSS to render your layout in different box models.</li>
<li>What does <code>* { box-sizing: border-box; }</code> do? What are its advantages?</li>
<li>List as many values for the display property that you can remember.</li>
<li>What's the difference between inline and inline-block?</li>
<li>What's the difference between a relative, fixed, absolute and statically positioned element?</li>
<li>The 'C' in CSS stands for Cascading.  How is priority determined in assigning styles (a few examples)?  How can you use this system to your advantage?</li>
<li>What existing CSS frameworks have you used locally, or in production? How would you change/improve them?</li>
<li>Have you played around with the new CSS Flexbox or Grid specs?</li>
<li>How is responsive design different from adaptive design?</li>
<li>Have you ever worked with retina graphics? If so, when and what techniques did you use?</li>
<li>Is there any reason you'd want to use <code>translate()</code> instead of <em>absolute positioning</em>, or vice-versa? And why?</li>
</ul>

<h4>
JS Questions:</h4>

<ul>
<li>Explain event delegation</li>
<li>Explain how <code>this</code> works in JavaScript</li>
<li>Explain how prototypal inheritance works</li>
<li>What do you think of AMD vs CommonJS?</li>
<li>Explain why the following doesn't work as an IIFE: <code>function foo(){ }();</code>.

<ul>
<li>What needs to be changed to properly make it an IIFE?</li>
</ul>
</li>
<li>What's the difference between a variable that is: <code>null</code>, <code>undefined</code> or <code>undeclared</code>?

<ul>
<li>How would you go about checking for any of these states?</li>
</ul>
</li>
<li>What is a closure, and how/why would you use one?</li>
<li>What's a typical use case for anonymous functions?</li>
<li>How do you organize your code? (module pattern, classical inheritance?)</li>
<li>What's the difference between host objects and native objects?</li>
<li>Difference between: <code>function Person(){}</code>, <code>var person = Person()</code>, and <code>var person = new Person()</code>?</li>
<li>What's the difference between <code>.call</code> and <code>.apply</code>?</li>
<li>Explain <code>Function.prototype.bind</code>.</li>
<li>When would you use <code>document.write()</code>?</li>
<li>What's the difference between feature detection, feature inference, and using the UA string?</li>
<li>Explain AJAX in as much detail as possible.</li>
<li>Explain how JSONP works (and how it's not really AJAX).</li>
<li>Have you ever used JavaScript templating?

<ul>
<li>If so, what libraries have you used?</li>
</ul>
</li>
<li>Explain "hoisting".</li>
<li>Describe event bubbling.</li>
<li>What's the difference between an "attribute" and a "property"?</li>
<li>Why is extending built-in JavaScript objects not a good idea?</li>
<li>Difference between document load event and document ready event?</li>
<li>What is the difference between <code>==</code> and <code>===</code>?</li>
<li>Explain the same-origin policy with regards to JavaScript.</li>
<li>Make this work:</li>
</ul>

<div><pre>duplicate([1,2,3,4,5]); // [1,2,3,4,5,1,2,3,4,5]</pre></div>

<ul>
<li>Why is it called a Ternary expression, what does the word "Ternary" indicate?</li>
<li>What is <code>"use strict";</code>? what are the advantages and disadvantages to using it?</li>
<li>Create a for loop that iterates up to <code>100</code> while outputting <strong>"fizz"</strong> at multiples of <code>3</code>, <code>"buzz"</code> at multiples of <code>5</code> and <strong>"fizzbuzz"</strong> at multiples of <code>3</code> and <code>5</code>
</li>
<li>Why is it, in general, a good idea to leave the global scope of a website as-is and never touch it?</li>
<li>Why would you use something like the <code>load</code> event? Does this event have disadvantages? Do you know any alternatives, and why would you use those?</li>
<li>Explain what a single page app is and how to make one SEO-friendly.</li>
<li>What is the extent of your experience with Promises and/or their polyfills?</li>
<li>What are the pros and cons of using Promises instead of callbacks?</li>
<li>What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?</li>
</ul>

<h4>
Testing Questions:</h4>

<ul>
<li>What are some advantages/disadvantages to testing your code?</li>
<li>What tools would you use to test your code's functionality?</li>
<li>What is the difference between a unit test and a functional/integration test?</li>
<li>What is the purpose of a code style linting tool?</li>
</ul>

<h4>
Performance Questions:</h4>

<ul>
<li>What tools would you use to find a performance bug in your code?</li>
<li>What are some ways you may improve your website's scrolling performance?</li>
<li>Explain the difference between layout, painting and compositing.</li>
</ul>

<h4>
Network Questions:</h4>

<ul>
<li>Traditionally, why has it been better to serve site assets from multiple domains?</li>
<li>Do your best to describe the process from the time you type in a website's URL to it finishing loading on your screen.</li>
<li>What are the differences between Long-Polling, Websockets and Server-Sent Events?</li>
<li>Explain the following request and response headers:

<ul>
<li>Diff. between Expires, Date, Age and If-Modified-...</li>
<li>Do Not Track</li>
<li>Cache-Control</li>
<li>Transfer-Encoding</li>

<li>X-Frame-Options</li>
</ul>
</li>
<li>What are HTTP actions? List all HTTP actions that you know, and explain them.</li>
</ul>

<h4>
Coding Questions:</h4>

<p><em>Question: What is the value of <code>foo</code>?</em></p>

<div><pre>var foo = 10 + '20';</pre></div>

<p><em>Question: How would you make this work?</em></p>

<div><pre>add(2, 5); // 7
add(2)(5); // 7</pre></div>

<p><em>Question: What value is returned from the following statement?</em></p>

<div><pre>"i'm a lasagna hog".split("").reverse().join("");</pre></div>

<p><em>Question: What is the value of <code>window.foo</code>?</em></p>

<div><pre>( window.foo || ( window.foo = "bar" ) );</pre></div>

<p><em>Question: What is the outcome of the two alerts below?</em></p>

<div><pre>var foo = "Hello";
(function() {
  var bar = " World";
  alert(foo + bar);
})();
alert(foo + bar);</pre></div>

<p><em>Question: What is the value of <code>foo.length</code>?</em></p>

<div><pre>var foo = [];
foo.push(1);
foo.push(2);</pre></div>

<p><em>Question: What is the value of <code>foo.x</code>?</em></p>

<div><pre>var foo = {n: 1};
var bar = foo;
foo.x = foo = {n: 2};</pre></div>

<h4>
Fun Questions:</h4>

<ul>
<li>What's a cool project that you've recently worked on?</li>
<li>What are some things you like about the developer tools you use?</li>
<li>Do you have any pet projects? What kind?</li>
<li>What's your favorite feature of Internet Explorer?</li>
<li>How do you like your coffee?</li>
</ul>

<h4>
Contributors:</h4>

<p>This document started in 2009 as a collaboration of <a href="https://twitter.com/paul_irish" target="_blank">@paul_irish</a> <a href="https://twitter.com/bentruyman" target="_blank">@bentruyman</a> <a href="https://twitter.com/cowboy" target="_blank">@cowboy</a> <a href="https://twitter.com/ajpiano" target="_blank">@ajpiano</a>  <a href="https://twitter.com/slexaxton" target="_blank">@SlexAxton</a> <a href="https://twitter.com/boazsender" target="_blank">@boazsender</a> <a href="https://twitter.com/miketaylr" target="_blank">@miketaylr</a> <a href="https://twitter.com/vladikoff" target="_blank">@vladikoff</a> <a href="https://twitter.com/gf3" target="_blank">@gf3</a> <a href="https://twitter.com/jon_neal" target="_blank">@jon_neal</a> <a href="https://twitter.com/sambreed" target="_blank">@sambreed</a> and <a href="https://twitter.com/iansym" target="_blank">@iansym</a>.</p>

<p>It has since received contributions from over <a href="https://github.com/h5bp/Front-end-Developer-Interview-Questions/graphs/contributors" target="_blank">100 developers</a>.</p>
      
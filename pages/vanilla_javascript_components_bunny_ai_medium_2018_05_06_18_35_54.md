<a href="https://medium.com/bunnyllc/vanilla-js-components-8d20c58b69f4">https://medium.com/bunnyllc/vanilla-js-components-8d20c58b69f4</a><div id="articleHeader"><h1>Vanilla JavaScript Components</h1></div><h2 id="7624">Learn how to build Vanilla JS components that work today without polyfills</h2><div><figure id="6091"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/105/1*KYLUsvBiRYQM9zTHj3sKXA.jpeg?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/2000/1*KYLUsvBiRYQM9zTHj3sKXA.jpeg" /></div><figcaption>From Wikipedia: History of Lego. Author: Arto Alanenpää. License: Creative Commons Attribution-Share Alike 4.0.</figcaption></figure><div><p id="8590">Components are stand-alone, independent parts of the application which are responsible for handling only one job and don’t know about each other. We already have native components like forms, tables, images, but how we can add custom ones which just works?</p><h3 id="8815">Current state with web components</h3><p id="5f97">Currently there is a <a href="https://www.w3.org/standards/techs/components#w3c_all" target="_blank">Web Components</a> specification in development, which probably, someday will make a web component development standardized, however, it is still far away from being finished and adopted, doesn’t work without a polyfill or framework like Polymer. Apart from the polyfill, there is another problem — current implementation uses ES6 class syntactic sugar which already adds too much complexity altogether with prototypes and doesn’t allow to define properties. The specification also doesn’t tell us how to register custom attributes.</p><p id="cce9">There are also many UI libraries and frameworks available already and the new one comes every day. From the most popular there are React.js and Vue.js. The problem with them is about the marketing hype, huge bundle size, too much extra complexity, “Reacts way” and many other points to mention.</p><blockquote id="9251">The most powerful JavaScript framework is JavaScript itself</blockquote><p id="1b86">Do we really need special tools, new language/syntax, new needless abstraction layers using more user device resources and time to handle that job? JavaScript was designed in 10 days to be used by a simple people, even designers, who could just make things done. No matter what you listen or read today — JavaScript still is the most powerful, easiest and flexible way to do the job it was created for and you don’t need a framework to build a modern production app. Yes, web trends evolved for last years, but JavaScript evolved together with them.</p><blockquote id="9617">The biggest problem with JavaScript community I see is people instead of learning JavaScript and software engineering are learning another tool.</blockquote><h3 id="47aa">How then create JavaScript components?</h3><p id="2b04">One of the most powerful features of JavaScript language you won’t find in another one is an <em>Object literal notation</em>, simplicity and flexibility of creating and modifying objects. Use it. Here is how you create a component:</p><pre id="2ecf">const Button = {</pre><pre id="3946">  tagName: 'btn',</pre><pre id="c573">  init(btn) {<br />    btn.addEventListener('click', () =&gt; {<br />      btn.textContent++;<br />    });<br />  },</pre><pre id="d788">  getAll(container = document.body) {<br />    return container.getElementsByTagName(this.tagName);<br />  }</pre><pre id="2303">};</pre><p id="34fb">As you can see it is just a simple JavaScript object. Moreover, I have found the <em>3rd Person pattern</em> or an <em>Object-Speaking pattern</em> without <code>new</code> and prototypes with the usage of the idea behind the <em>factory pattern</em> the simplest way of creating objects in JavaScript. Almost every method will receive a DOM element (component) as a 1st argument. You have only one global Button object which operates on all buttons in the DOM and this is your component. You never create any new instances and can access any button from any part of your code without the <em>Singleton pattern.</em></p><h3 id="b943">How were JavaScript components implemented for many years before the modern frameworks war?</h3><p id="8483">For more than 10 years Vanilla JS components were implemented as jQuery plugins or stand-alone widgets. Basically, they were same simple JavaScript objects and functions. You imported one file and in most cases just called init() method. When component was inserted into DOM later, like a simple dropdown, you had to manually call init() on a new DOM element again yourself.</p><p id="88fe">However, there were DOM events available we could use to listen for changes in the DOM like a new tag inserted, removed or attribute changed. So we could use them to call init() or deinit() automatically. The problem there was with a performance and because of that today we have a modern <a href="https://developer.mozilla.org/en/docs/Web/API/MutationObserver" target="_blank"><strong>Mutation Observer API</strong></a> which works on every modern platform and even in IE11.</p><p id="c5e5">You can initialize just one MutationObserver and listen for changes in the whole document.body, then register custom callbacks when, for example, new tag is inserted into DOM. Since Mutation Observer API and this algorithm requires a bit of logic to implement every time I have created a <a href="https://github.com/Mevrael/bunny/blob/master/src/DOMObserver.js" target="_blank"><strong>DOMObserver</strong></a> which can be used to handle that job with ease. Just call <code>DOMObserver.onInsert('tagname', callback)</code>.</p><h3 id="7d51">How to register custom attributes?</h3><p id="b64b">All DOM elements are also just an objects and it is possible to add new properties to any DOM element, i.e. document.body.myProperty = 1;</p><p id="3402">JavaScript has something called <strong>Object Descriptors</strong> or simply — getters and setters. Getters are called when you try to read a property of any object and Setters are called when you assign a new value to a property. Since all global objects are properties of the window you can execute some code anytime you just use a variable, i.e. this line of code <code>a;</code> may do something.</p><p id="eec3">Let say we want to implement a simple counter. Whenever <code>btn.counter = 1</code> is executed a counter should have a new value and a <code>btn.counter</code> should return a current value. We also want to “register” a <code>counter</code> attribute so <code>&lt;btn counter="6"&gt;&lt;/btn&gt;</code> could define a default value.</p><p id="2d4a">To define getters and setters in JavaScript you have to use <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty" target="_blank">Object.defineProperty()</a>:</p><pre id="4d7b"><strong>const </strong>attrVal = component.getAttribute(name);<br />component['_' + name] = attrVal ? attrVal : defaultValue;<br />onChange(component['_' + name]);</pre><pre id="0637">Object.defineProperty(component, name, {<br />  get() {<br />    <strong>return </strong>component['_' + name]<br />  },<br />  set(val) {<br />    component['_' + name] = val;<br />    onChange(val);<br />  }<br />});</pre><p id="6706">Now everything will work except changes in attribute, i.e. <code>btn.setAttribute('counter', 10)</code>won’t work. For that we will need to register a MutationObserver and listen for attribute changes. To make this job easier I have created a <a href="https://github.com/Mevrael/bunny/blob/master/src/DOMObserver.js#L87" target="_blank">DOMObserver.registerAttribute()</a> method.</p><h3 id="60cf">What about a template/view/UI?</h3><p id="e69b">In a good software architecture business logic, of course, should be separated from the presentation logic. Each Component should not know about any data and should not have any side effects. Components are just plain objects — sets of pure functions connecting data with a DOM. In the example above Button is a Controller. For simple components, UI/View/DOM methods can be implemented in the same object. For larger objects, I would recommend separating UI from Controller also and make a ButtonUI object and inject it into Button.UI. In most cases, document.createElement() is the best approach for handling view layer.</p><p id="df33">However, sometimes we need to parse a template and import custom variables in it. Here is another technic used for many years: server returns some HTML templates hidden from the user, then JS parses those templates. From the Button point of view, I just call UI methods and don’t care about the implementation. Under the hood, it is always easy to replace the UI logic and template engine.</p><p id="051c">Today we have a <code>&lt;template&gt;</code> tag and there is no more need of hiding template contents. Browsers also remove all the content so no components would be initialized inside a template. For older platforms, polyfill can be used or just a <code>&lt;div hidden&gt;</code>. I am not going to write about different template engines, there are many of them and you may use any but I would recommend using the right tool for the right job. Sometimes you can just use old document.createElement(), sometimes you may write a simple parseTemplate() function and do a simple string.replace(). The common point here is I strongly would not recommend using a custom JSX or other syntax, or writing HTML or CSS in JavaScript (browser). Many years ago we have been writing all of them together but later we decided to separate them because of maintainability, single responsibility, and simplicity, especially in huge systems. When I am going to change a template of a UI component in a large production app I am searching for the specific template file which is used by a back-end. This also allowed us to share the same template in both front-end and back-end for many years.</p><p id="6341">The fastest, the most native and simplest way of defining HTML templates without any “server-side rendering” buzzwords is to render all the required HTML needed for the certain page request. Usually, all the templates are put at the bottom before the closing &lt;/body&gt;, where today you may find also JS and SVG sprite.</p><p id="bfa3">It is also absolutely normal today to just generate HTML on the server like 10 years ago and append it in JS. GitHub, YouTube, and many other apps are still doing this because it is simple and fast.</p><p id="eccb">To sum up this section I want to say that there is no “right way”, there is no only one technic or only one library or framework. Use the right tool for the right job, be flexible.</p><h3 id="9b2e">What about a state?</h3><p id="2ada">“State” is another modern buzzword replaced data but I always will keep calling it data and no matter how you call your architecture pattern, it still is an MVC or inherits a 3-tier architecture, even React components uses MVC, M just became a “state”, V — render() and C — Component itself.</p><blockquote id="6708">The most powerful JavaScript function is Object.assign()</blockquote><p id="1e1c">Let say we have same btn, counter and another customAttribute. Our data or a state is a data = {counter: 0, customAttribute: 0} which is stored in a DOM element directly. And to update our component all that we need to do is Object.assign(component, data).</p><p id="e80d">Object.assign() will merge all objects together. All properties in the component object will be overridden by properties of data object but this approach, of course, will only work if we have defined component descriptors (getters and setters).</p><p id="3613">Talking about the data received from the server I am using same simple JavaScript API-speaking objects. Here is, for example, how I can change the state of a Like button to active when a server returns a successful result and in error case, nothing would happen, or base Api object could display a small alert in the corner of the screen:</p><pre id="81ce">CommentModel.like(commentId).then(() =&gt; {<br />  Comment.UI.setLikeActive(commentId);<br />});</pre><h3 id="b25a">Combining all together</h3><p id="0ae9">In the example above by using the current JavaScript features:</p><ul><li id="8c8e">Object literal notation</li><li id="d677">Object descriptors</li><li id="30d5">Mutation Observer API (only if you want to automatically init components inserted into DOM after DOMContentLoaded)</li></ul><p id="a59f">and without using any 3rd party libraries or frameworks we created a custom modern component which can be re-used in absolutely every web application around the world.</p><p id="63a4">We, of course, may create a core abstract Component object to make our life even easier and I have created an <a href="https://github.com/mevrael/bunny#experimental-components-based-on-domobserver-mutation-observer" target="_blank">experimental Component</a> as a part of <a href="https://bunnyjs.com" target="_blank"><strong>BunnyJS </strong></a><strong>— modern JS and ES6 library, set of stand-alone Vanilla JS components which just works everywhere.</strong> DataTables in 6kb, Form Validation in 6kb and mentioned Component+DOMObserver <a href="https://unpkg.com/bunnyjs/dist/component.min.js" target="_blank">component.min.js</a> only 2.8kb. Not talking about the helpers/utils like BunnyDate, BunnyURL, BunnyFile, BunnyImage, DOM utils like onClickOutside(), accessible addEventKeyNavigation() and many others.</p><blockquote id="111f">After so many years we still don’t have a Vanilla JS components while we have over 9000 datepickers, dropdowns, datatables and other widgets coupled only to a jQuery or React or Angular or Vue or another framework’s of the day implementation.</blockquote><p id="0806">BunnyJS is not a hype and it still may suck in some ways, however, if you would like to make JavaScript great again, any feedback or contributions would be very appreciated.</p><h4 id="651b">If you liked this article please press the ❤ button, share the article and star the project on GitHub.</h4><p id="95ea">I hope this article will bring us more Vanilla JS components in the future.</p><blockquote id="2ae3">“Perfection is achieved, not when there is nothing more to add, but when there is nothing left to take away.”</blockquote><blockquote id="b62d">— Antoine de Saint-Exupery</blockquote><h3 id="e169">Useful links:</h3><p id="81bb"><a href="https://twitter.com/Mevrael" target="_blank"><em>Mev-Rael</em></a><em> is a founder, CEO and CTO of </em><a href="https://bunny.earth" target="_blank"><em>Bunny AI</em></a><em> and an experienced software architect working with the Web and the Internet technologies for more than 10 years, Leader and a tech entrepreneur, author of </em><a href="https://bunnyjs.com" target="_blank"><em>BunnyJS </em></a><em>and </em><a href="https://github.com/Mevrael/assets-builder" target="_blank"><em>Assets Builder</em></a><em>; Web Standards, Laravel, Bootstrap, CSSNext community member/contributor; who peer reviews articles on </em><a href="https://www.sitepoint.com/javascript/" target="_blank"><em>SitePoint</em></a><em> and shares his life experience by answering community questions on </em><a href="https://hashnode.com/@mevrael" target="_blank"><em>Hashnode</em></a><em> — amazing platform for developers by developers. In free time he also teaches web development and practices Chen style Taijiquan.</em></p></div>
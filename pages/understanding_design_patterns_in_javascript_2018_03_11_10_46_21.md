<a href="https://code.tutsplus.com/tutorials/understanding-design-patterns-in-javascript--net-25930">https://code.tutsplus.com/tutorials/understanding-design-patterns-in-javascript--net-25930</a><div id="articleHeader"><h1>Understanding Design Patterns in JavaScript</h1></div><div><div><div>by <a href="https://tutsplus.com/authors/tilo-mitra" target="_blank">Tilo Mitra</a><time>16 Feb 2013</time></div><div>Difficulty:IntermediateLength:LongLanguages:</div><p>Today, we're going to put on our computer science hats as we learn about some common design patterns. Design patterns offer developers ways to solve technical problems in a reusable and elegant way. Interested in becoming a better JavaScript developer? Then read on.</p>
<div>
<strong>Republished Tutorial</strong>
<p>Every few weeks, we revisit some of our reader's favorite posts from throughout the history of the site. This tutorial was first published in July, 2012.</p>
</div>
<hr />
<h2>Introduction</h2>
<p>Solid design patterns are the basic building block for maintainable software applications. If you've ever participated in a technical interview, you've liked been asked about them. In this tutorial, we'll take a look at a few patterns that you can start using today.</p>
<hr />
<h2>What is a Design Pattern?</h2>
<blockquote><p>A design pattern is a reusable software solution</p></blockquote>
<p>Simply put, a design pattern is a reusable software solution to a specific type of problem that occurs frequently when developing software. Over the many years of practicing software development, experts have figured out ways of solving similar problems. These solutions have been encapsulated into design patterns. So:</p>
<ul>
<li>patterns are proven solutions to software development problems </li>
<li>patterns are scalable as they usually are structured and have rules that you should follow </li>
<li>patterns are reusable for similar problems </li>
</ul>
<p>We'll get into some examples of design patterns further in to the tutorial.</p>
<hr />
<h2>Types of Design Patterns</h2>
<p>In software development, design patterns are generally grouped into a few categories. We'll cover the three most important ones in this tutorial. They are explained in brief below:</p>
<ol>
<li>
<strong>Creational</strong> patterns focus on ways to create objects or classes. This may sound simple (and it is in some cases), but large applications need to control the object creation process.
</li>
<li>
<strong>Structural</strong> design patterns focus on ways to manage relationships between objects so that your application is architected in a scalable way. A key aspect of structural patterns is to ensure that a change in one part of your application does not affect all other parts.
</li>
<li>
<strong>Behavioral</strong> patterns focus on communication between objects. </li>
</ol>
<p>You may still have questions after reading these brief descriptions. This is natural, and things will clear up once we look at some design patterns in depth below. So read on!</p>
<hr />
<h2>A Note About Classes in JavaScript</h2>
<p>When reading about design patterns, you'll often see references to classes and objects. This can be confusing, as JavaScript does not really have the construct of "class"; a more correct term is "data type".</p>
<h3>Data Types in JavaScript</h3>
<p>JavaScript is an object-oriented language where objects inherit from other objects in a concept known as prototypical inheritance. A data type can be created by defining what is called a constructor function, like this:</p>
<div><div id="highlighter_623899"><table><tbody><tr><td></td><td><div><div><code>function</code> <code>Person(config) {</code></div><div><code>this</code><code>.name = config.name;</code></div><div><code>this</code><code>.age = config.age;</code></div><div><code>}</code></div><div><code>Person.prototype.getAge = </code><code>function</code><code>() {</code></div><div><code>return</code> <code>this</code><code>.age;</code></div><div><code>};</code></div><div><code>var</code> <code>tilo = </code><code>new</code> <code>Person({name:</code><code>"Tilo"</code><code>, age:23 });</code></div><div><code>console.log(tilo.getAge());</code></div></div></td></tr></tbody></table></div></div>
<p>Note the use of the <code>prototype</code> when defining methods on the <code>Person</code> data type. Since multiple <code>Person</code> objects will reference the same prototype, this allows the <code>getAge()</code> method to be shared by all instances of the <code>Person</code> data type, rather than redefining it for every instance. Additionally, any data type that inherits from <code>Person</code> will have access to the <code>getAge()</code> method. </p>
<h3>Dealing with Privacy</h3>
<p>Another common issue in JavaScript is that there is no true sense of private variables. However, we can use closures to somewhat simulate privacy. Consider the following snippet:</p>
<div><div id="highlighter_651387"><table><tbody><tr><td></td><td><div><div><code>var</code> <code>retinaMacbook = (</code><code>function</code><code>() {</code></div><div><code>//Private variables</code></div><div><code>var</code> <code>RAM, addRAM;</code></div><div><code>RAM = 4;</code></div><div><code>//Private method</code></div><div><code>addRAM = </code><code>function</code> <code>(additionalRAM) {</code></div><div><code>RAM += additionalRAM;</code></div><div><code>};</code></div><div><code>return</code> <code>{</code></div><div><code>//Public variables and methods</code></div><div><code>USB: undefined,</code></div><div><code>insertUSB: </code><code>function</code> <code>(device) {</code></div><div><code>this</code><code>.USB = device;</code></div><div><code>},</code></div><div><code>removeUSB: </code><code>function</code> <code>() {</code></div><div><code>var</code> <code>device = </code><code>this</code><code>.USB;</code></div><div><code>this</code><code>.USB = undefined;</code></div><div><code>return</code> <code>device;</code></div><div><code>}</code></div><div><code>};</code></div><div><code>})();</code></div></div></td></tr></tbody></table></div></div>
<p>In the example above, we created a <code>retinaMacbook</code> object, with public and private variables and methods. This is how we would use it:</p>
<div><div id="highlighter_524900"><table><tbody><tr><td></td><td><div><div><code>retinaMacbook.insertUSB(</code><code>"myUSB"</code><code>);</code></div><div><code>console.log(retinaMacbook.USB); </code><code>//logs out "myUSB"</code></div><div><code>console.log(retinaMacbook.RAM) </code><code>//logs out undefined</code></div></div></td></tr></tbody></table></div></div>
<p>There's a lot more that we can do with functions and closures in JavaScript, but we won't get into all of it in this tutorial. With this little lesson on JavaScript data types and privacy behind us, we can carry along to learn about design patterns.</p>
<hr />
<h2>Creational Design Patterns</h2>
<p>There are many different kinds of creational design patterns but we are going to cover two of them in this tutorial: Builder and Prototype. I find that these are used often enough to warrant the attention. </p>
<h3>Builder Pattern</h3>
<p>The Builder Pattern is often used in web development, and you've probably used it before without realizing it. Simply put, this pattern can be defined as the following:</p>
<blockquote>
<p>Applying the builder pattern allows us to construct objects by only specifying the type and the content of the object. We don't have to explicitly create the object. </p>
</blockquote>
<p>For example, you've probably done this countless times in jQuery:</p>
<div><div id="highlighter_583307"><table><tbody><tr><td></td><td><div><div><code>var</code> <code>myDiv = $(</code><code>'&lt;div id="myDiv"&gt;This is a div.&lt;/div&gt;'</code><code>);</code></div><div><code>//myDiv now represents a jQuery object referencing a DOM node.</code></div><div><code>var</code> <code>someText = $(</code><code>'&lt;p/&gt;'</code><code>);</code></div><div><code>//someText is a jQuery object referencing an HTMLParagraphElement</code></div><div><code>var</code> <code>input = $(</code><code>'&lt;input /&gt;'</code><code>);</code></div></div></td></tr></tbody></table></div></div>
<p>Take a look at the three examples above. In the first one, we passed in a <code>&lt;div/&gt;</code> element with some content. In the second, we passed in an empty <code>&lt;p&gt;</code> tag. In the last one, we passed in an <code>&lt;input /&gt;</code> element. The result of all three were the same: we were returned a jQuery object referencing a DOM node.</p>
<p>The <code>$</code> variable adopts the Builder Pattern in jQuery. In each example, we were returned a jQuery DOM object and had access to all the methods provided by the jQuery library, but at no point did we explicitly call <code>document.createElement</code>. The JS library handled all of that under the hood. </p>
<p>Imagine how much work it would be if we had to explicitly create the DOM element and insert content into it! By leveraging the builder pattern, we're able to focus on the type and the content of the object, rather than explicit creation of it. </p>
<h3>Prototype Pattern</h3>
<p>Earlier, we went through how to define data types in JavaScript through functions and adding methods to the object's <code>prototype</code>. The Prototype pattern allows objects to inherit from other objects, via their prototypes. </p>
<blockquote>
<p>The prototype pattern is a pattern where objects are created based on a template of an existing object through cloning. </p>
</blockquote>
<p>This is an easy and natural way of implementing inheritance in JavaScript. For example:</p>
<div><div id="highlighter_330307"><table><tbody><tr><td></td><td><div><div><code>var</code> <code>Person = {</code></div><div><code>numFeet: 2,</code></div><div><code>numHeads: 1,</code></div><div><code>numHands:2</code></div><div><code>};</code></div><div><code>//Object.create takes its first argument and applies it to the prototype of your new object.</code></div><div><code>var</code> <code>tilo = Object.create(Person);</code></div><div><code>console.log(tilo.numHeads); </code><code>//outputs 1</code></div><div><code>tilo.numHeads = 2;</code></div><div><code>console.log(tilo.numHeads) </code><code>//outputs 2</code></div></div></td></tr></tbody></table></div></div>
<p>The properties (and methods) in the <code>Person</code> object get applied to the prototype of the <code>tilo</code> object. We can redefine the properties on the <code>tilo</code> object if we want them to be different.</p>
<p>In the example above, we used <code>Object.create()</code>. However, Internet Explorer 8 does not support the newer method. In these cases, we can simulate it's behavior:</p>
<div><div id="highlighter_49331"><table><tbody><tr><td></td><td><div><div><code>var</code> <code>vehiclePrototype = {</code></div><div><code>init: </code><code>function</code> <code>(carModel) {</code></div><div><code>this</code><code>.model = carModel;</code></div><div><code>},</code></div><div><code>getModel: </code><code>function</code> <code>() {</code></div><div><code>console.log( </code><code>"The model of this vehicle is "</code> <code>+ </code><code>this</code><code>.model);</code></div><div><code>}</code></div><div><code>};</code></div><div><code>function</code> <code>vehicle (model) {</code></div><div><code>function</code> <code>F() {};</code></div><div><code>F.prototype = vehiclePrototype;</code></div><div><code>var</code> <code>f = </code><code>new</code> <code>F();</code></div><div><code>f.init(model);</code></div><div><code>return</code> <code>f;</code></div><div><code>}</code></div><div><code>var</code> <code>car = vehicle(</code><code>"Ford Escort"</code><code>);</code></div><div><code>car.getModel();</code></div></div></td></tr></tbody></table></div></div>
<p>The only disadvantage to this method is that you cannot specify read-only properties, which <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Object/create" target="_blank">can be specified</a> when using <code>Object.create()</code>. Nonetheless, the prototype pattern shows how objects can inherit from other objects. </p>
<hr />
<h2>Structural Design Patterns</h2>
<p>Structural design patterns are really helpful when figuring out how a system should work. They allow our applications to scale easily and remain maintainable. We're going to look at the following patterns in this group: Composite and Facade.</p>
<h3>Composite Pattern</h3>
<p>The composite pattern is another pattern that you probably have used before without any realization. </p>
<blockquote>
<p>The composite pattern says that a group of objects can be treated in the same manner as an individual object of the group.</p>
</blockquote>
<p>So what does this mean? Well, consider this example in jQuery (most JS libraries will have an equivalent to this):</p>
<div><div id="highlighter_926249"><table><tbody><tr><td></td><td><div><div><code>$(</code><code>'.myList'</code><code>).addClass(</code><code>'selected'</code><code>);</code></div><div><code>$(</code><code>'#myItem'</code><code>).addClass(</code><code>'selected'</code><code>);</code></div><div><code>//dont do this on large tables, it's just an example.</code></div><div><code>$(</code><code>"#dataTable tbody tr"</code><code>).on(</code><code>"click"</code><code>, </code><code>function</code><code>(event){</code></div><div><code>alert($(</code><code>this</code><code>).text());</code></div><div><code>});</code></div><div><code>$('</code><code>#myButton').on("click", function(event) {</code></div><div><code>alert(</code><code>"Clicked."</code><code>);</code></div><div><code>});</code></div></div></td></tr></tbody></table></div></div>
<p>Most JavaScript libraries provide a consistent API regardless of whether we are dealing with a single DOM element or an array of DOM elements. In the first example, we are able to add the <code>selected</code> class to all the items picked up by the <code>.myList</code> selector, but we can use the same method when dealing with a singular DOM element, <code>#myItem</code>. Similarly, we can attach event handlers using the <code>on()</code> method on multiple nodes, or on a single node through the same API. </p>
<p>By leveraging the Composite pattern, jQuery (and many other libraries) provide us with a simplified API.</p>
<p>The Composite Pattern can sometimes cause problems as well. In a loosely-typed language such as JavaScript, it can often be helpful to know whether we are dealing with a single element or multiple elements. Since the composite pattern uses the same API for both, we can often mistake one for the other and end up with unexpected bugs. Some libaries, such as YUI3, offer two separate methods of getting elements (<code>Y.one()</code> vs <code>Y.all()</code>). </p>
<h3>Facade Pattern</h3>
<p>Here's another common pattern that we take for granted. In fact, this one is one of my favorites because it's simple, and I've seen it being used all over the place to help with browser inconsistencies. Here's what the Facade pattern is about:</p>
<blockquote>
<p>The Facade Pattern provides the user with a simple interface, while hiding it's underlying complexity. </p>
</blockquote>
<p>The Facade pattern almost always improves usability of a piece of software. Using jQuery as an example again, one of the more popular methods of the library is the <code>ready()</code> method:</p>
<div><div id="highlighter_928793"><table><tbody><tr><td></td><td><div><div><code>$(document).ready(</code><code>function</code><code>() {</code></div><div><code>//all your code goes here...</code></div><div><code>});</code></div></div></td></tr></tbody></table></div></div>
<p>The <code>ready()</code> method actually implements a facade. If you take a look at the source, here's what you find:</p>
<div><div id="highlighter_329008"><table><tbody><tr><td></td><td><div><div><code>ready: (</code><code>function</code><code>() {</code></div><div><code>...</code></div><div><code>//Mozilla, Opera, and Webkit</code></div><div><code>if</code> <code>(document.addEventListener) {</code></div><div><code>document.addEventListener(</code><code>"DOMContentLoaded"</code><code>, idempotent_fn, </code><code>false</code><code>);</code></div><div><code>...</code></div><div><code>}</code></div><div><code>//IE event model</code></div><div><code>else</code> <code>if</code> <code>(document.attachEvent) {</code></div><div><code>// ensure firing before onload; maybe late but safe also for iframes</code></div><div><code>document.attachEvent(</code><code>"onreadystatechange"</code><code>, idempotent_fn);</code></div><div><code>// A fallback to window.onload, that will always work</code></div><div><code>window.attachEvent(</code><code>"onload"</code><code>, idempotent_fn);</code></div><div><code>...     </code></div><div><code>}</code></div><div><code>})</code></div></div></td></tr></tbody></table></div></div>
<p>Under the hood, the <code>ready()</code> method is not all that simple. jQuery normalizes the browser inconsistencies to ensure that <code>ready()</code> is fired at the appropriate time. However, as a developer, you are presented with a simple interface. </p>
<p>Most examples of the Facade pattern follow this principle. When implementing one, we usually rely on conditional statements under the hood, but present it as a simple interface to the user. Other methods implementing this pattern include <code>animate()</code> and <code>css()</code>. Can you think of why these would be using a facade pattern?</p>
<hr />
<h2>Behavioral Design Patterns</h2>
<p>Any object-oriented software systems will have communication between objects. Not organizing that communication can lead to bugs that are difficult to find and fix. Behavioral design patterns prescribe different methods of organizing the communication between objects. In this section, we're going to look at the Observer and Mediator patterns. </p>
<h3>Observer Pattern</h3>
<p>The Observer pattern is the first of the two behavioral patterns that we are going to go through. Here's what it says:</p>
<blockquote>
<p>In the Observer Pattern, a subject can have a list of observers that are interested in it's lifecycle. Anytime the subject does something interesting, it sends a notification to its observers. If an observer is no longer interested in listening to the subject, the subject can remove it from its list. </p>
</blockquote>
<p>Sounds pretty simple, right? We need three methods to describe this pattern:</p>
<ul>
<li>
<code>publish(data)</code>: Called by the subject when it has a notification to make. Some data may be passed by this method. </li>
<li>
<code>subscribe(observer)</code>: Called by the subject to add an observer to its list of observers. </li>
<li>
<code>unsubscribe(observer)</code>: Called by the subject to remove an observer from its list of observers. </li>
</ul>
<p>Well, it turns out that most modern JavaScript libraries support these three methods as part of their custom events infrastructure. Usually, there's an <code>on()</code> or <code>attach()</code> method, a <code>trigger()</code> or <code>fire()</code> method, and an <code>off()</code> or <code>detach()</code> method. Consider the following snippet:</p>
<div><div id="highlighter_452634"><table><tbody><tr><td></td><td><div><div><code>//We just create an association between the jQuery events methods</code></div></div></td></tr></tbody></table></div></div>
<div><div id="highlighter_877824"><table><tbody><tr><td></td><td><div><div><code>//and those prescribed by the Observer Pattern but you don't have to.</code></div><div><code>var</code> <code>o = $( {} );</code></div><div><code>$.subscribe = o.on.bind(o);</code></div><div><code>$.unsubscribe = o.off.bind(o);</code></div><div><code>$.publish = o.trigger.bind(o);</code></div><div><code>// Usage</code></div><div><code>document.on( 'tweetsReceived</code><code>', function(tweets) {</code></div><div><code>//perform some actions, then fire an event</code></div><div><code>$.publish('</code><code>tweetsShow</code><code>', tweets);</code></div><div><code>});</code></div><div><code>//We can subscribe to this event and then fire our own event.</code></div><div><code>$.subscribe( '</code><code>tweetsShow</code><code>', function() {</code></div><div><code>//display the tweets somehow</code></div><div><code>..</code></div><div><code>//publish an action after they are shown.</code></div><div><code>$.publish('</code><code>tweetsDisplayed);</code></div><div><code>});</code></div><div><code>$.subscribe('tweetsDisplayed, </code><code>function</code><code>() {</code></div><div><code>...</code></div><div><code>});</code></div></div></td></tr></tbody></table></div></div>
<p>The Observer pattern is one of the simpler patterns to implement, but it is very powerful. JavaScript is well suited to adopt this pattern as it's naturally event-based. The next time you develop web applications, think about developing modules that are loosely-coupled with each other and adopt the Observer pattern as a means of communication. The observer pattern can become problematic if there are too many subjects and observers involved. This can happen in large-scale systems, and the next pattern we look at tries to solve this problem.</p>
<h3>Mediator Pattern</h3>
<p>The last pattern we are going to look at is the Mediator Pattern. It's similar to the Observer pattern but with some notable differences.</p>
<blockquote>
<p>The Mediator Pattern promotes the use of a single shared subject that handles communication with multiple objects. All objects communicate with each other through the mediator.</p>
</blockquote>
<p>A good real-world analogy would be an Air Traffic Tower, which handles communication between the airport and the flights. In the world of software development, the Mediator pattern is often used as a system gets overly complicated. By placing mediators, communication can be handled through a single object, rather than having multiple objects communicating with each other. In this sense, a mediator pattern can be used to replace a system that implements the observer pattern.</p>
<p>There's a simplified implementation of the Mediator pattern by Addy Osmani in <a href="https://gist.github.com/1794823" target="_blank">this gist</a>. Let's talk about how you may use it. Imagine that you have a web app that allows users to click on an album, and play music from it. You could set up a mediator like this:</p>
<div><div id="highlighter_3763"><table><tbody><tr><td></td><td><div><div><code>$(</code><code>'#album'</code><code>).on(</code><code>'click'</code><code>, </code><code>function</code><code>(e) {</code></div><div><code>e.preventDefault();</code></div><div><code>var</code> <code>albumId = $(</code><code>this</code><code>).id();</code></div><div><code>mediator.publish(</code><code>"playAlbum"</code><code>, albumId);</code></div><div><code>});</code></div><div><code>var</code> <code>playAlbum = </code><code>function</code><code>(id) {</code></div><div><code>…</code></div><div><code>mediator.publish(</code><code>"albumStartedPlaying"</code><code>, {songList: [..], currentSong: </code><code>"Without You"</code><code>});</code></div><div><code>};</code></div><div><code>var</code> <code>logAlbumPlayed = </code><code>function</code><code>(id) {</code></div><div><code>//Log the album in the backend</code></div><div><code>};</code></div><div><code>var</code> <code>updateUserInterface = </code><code>function</code><code>(album) {</code></div><div><code>//Update UI to reflect what's being played</code></div><div><code>};</code></div><div><code>//Mediator subscriptions</code></div><div><code>mediator.subscribe(</code><code>"playAlbum"</code><code>, playAlbum);</code></div><div><code>mediator.subscribe(</code><code>"playAlbum"</code><code>, logAlbumPlayed);</code></div><div><code>mediator.subscribe(</code><code>"albumStartedPlaying"</code><code>, updateUserInterface);</code></div></div></td></tr></tbody></table></div></div>
<p>The benefit of this pattern over the Observer pattern is that a single object is responsible for communication, whereas in the observer pattern, multiple objects could be listening and subscribing to each other. </p>
<p>In the Observer pattern, there is no single object that encapsulates a constraint. Instead, the Observer and the Subject must cooperate to maintain the constraint. Communication patterns are determined by the way observers and subjects are interconnected: a single subject usually has many observers, and sometimes the observer of one subject is a subject of another observer.</p>
<hr />
<h2>Conclusion</h2>
<blockquote><p>Someone has already applied it successfully in the past.</p></blockquote>
<p>The great thing about design patterns is that someone has already applied it successfully in the past. There are lots of open-source code that implement various patterns in JavaScript. As developers, we need to be aware of what patterns are out there and when to apply them. I hope this tutorial helped you take one more step towards answering these questions. </p>
<hr />
<h2>Additional Reading</h2>
<p>Much of the content from this article can be found in the excellent <a href="http://addyosmani.com/resources/essentialjsdesignpatterns/book/" target="_blank">Learning JavaScript Design Patterns</a> book, by Addy Osmani. It's an online book that was released for free under a Creative Commons license. The book extensively covers the theory and implementation of lots of different patterns, both in vanilla JavaScript and various JS libraries. I encourage you to look into it as a reference when you start your next project. </p>

<a href="https://gist.github.com/staltz/868e7e9bc2a7b8c1f754">https://gist.github.com/staltz/868e7e9bc2a7b8c1f754</a><div id="articleHeader"><h1>The introduction to Reactive Programming you've been missing</h1></div>
<p>(by <a href="https://twitter.com/andrestaltz" target="_blank">@andrestaltz</a>)</p>
<hr />
<h3>This tutorial as a series of videos</h3>
<p><strong>If you prefer to watch video tutorials with live-coding, then check out this series I recorded with the same contents as in this article: <a href="https://egghead.io/series/introduction-to-reactive-programming" target="_blank">Egghead.io - Introduction to Reactive Programming</a>.</strong></p>
<hr />
<p>So you're curious in learning this new thing called Reactive Programming, particularly its variant comprising of Rx, Bacon.js, RAC, and others.</p>
<p>Learning it is hard, even harder by the lack of good material. When I started, I tried looking for tutorials. I found only a handful of practical guides, but they just scratched the surface and never tackled the challenge of building the whole architecture around it. Library documentations often don't help when you're trying to understand some function. I mean, honestly, look at this:</p>
<blockquote>
<p><strong>Rx.Observable.prototype.flatMapLatest(selector, [thisArg])</strong></p>
</blockquote>
<blockquote>
<p>Projects each element of an observable sequence into a new sequence of observable sequences by incorporating the element's index and then transforms an observable sequence of observable sequences into an observable sequence producing values only from the most recent observable sequence.</p>
</blockquote>
<p>Holy cow.</p>
<p>I've read two books, one just painted the big picture, while the other dived into how to use the Reactive library. I ended up learning Reactive Programming the hard way: figuring it out while building with it. At my work in <a href="https://www.futurice.com" target="_blank">Futurice</a> I got to use it in a real project, and had the <a href="http://blog.futurice.com/top-7-tips-for-rxjava-on-android" target="_blank">support of some colleagues</a> when I ran into troubles.</p>
<p>The hardest part of the learning journey is <strong>thinking in Reactive</strong>. It's a lot about letting go of old imperative and stateful habits of typical programming, and forcing your brain to work in a different paradigm. I haven't found any guide on the internet in this aspect, and I think the world deserves a practical tutorial on how to think in Reactive, so that you can get started. Library documentation can light your way after that. I hope this helps you.</p>
<h2>"What is Reactive Programming?"</h2>
<p>There are plenty of bad explanations and definitions out there on the internet. <a href="https://en.wikipedia.org/wiki/Reactive_programming" target="_blank">Wikipedia</a> is too generic and theoretical as usual. <a href="http://stackoverflow.com/questions/1028250/what-is-functional-reactive-programming" target="_blank">Stackoverflow</a>'s canonical answer is obviously not suitable for newcomers. <a href="http://www.reactivemanifesto.org/" target="_blank">Reactive Manifesto</a> sounds like the kind of thing you show to your project manager or the businessmen at your company. Microsoft's <a href="https://rx.codeplex.com/" target="_blank">Rx terminology</a> "Rx = Observables + LINQ + Schedulers" is so heavy and Microsoftish that most of us are left confused. Terms like "reactive" and "propagation of change" don't convey anything specifically different to what your typical MV* and favorite language already does. Of course my framework views react to the models. Of course change is propagated. If it wouldn't, nothing would be rendered.</p>
<p>So let's cut the bullshit.</p>
<h4>Reactive programming is programming with asynchronous data streams.</h4>
<p>In a way, this isn't anything new. Event buses or your typical click events are really an asynchronous event stream, on which you can observe and do some side effects. Reactive is that idea on steroids. You are able to create data streams of anything, not just from click and hover events. Streams are cheap and ubiquitous, anything can be a stream: variables, user inputs, properties, caches, data structures, etc. For example, imagine your Twitter feed would be a data stream in the same fashion that click events are. You can listen to that stream and react accordingly.</p>
<p><strong>On top of that, you are given an amazing toolbox of functions to combine, create and filter any of those streams.</strong> That's where the "functional" magic kicks in. A stream can be used as an input to another one. Even multiple streams can be used as inputs to another stream. You can <em>merge</em> two streams. You can <em>filter</em> a stream to get another one that has only those events you are interested in. You can <em>map</em> data values from one stream to another new one.</p>
<p>If streams are so central to Reactive, let's take a careful look at them, starting with our familiar "clicks on a button" event stream.</p>
<p><a href="https://camo.githubusercontent.com/36c0a9ffd8ed22236bd6237d44a1d3eecbaec336/687474703a2f2f692e696d6775722e636f6d2f634c344d4f73532e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/36c0a9ffd8ed22236bd6237d44a1d3eecbaec336/687474703a2f2f692e696d6775722e636f6d2f634c344d4f73532e706e67" alt="Click event stream" /></div></a></p>
<p>A stream is a sequence of <strong>ongoing events ordered in time</strong>. It can emit three different things: a value (of some type), an error, or a "completed" signal. Consider that the "completed" takes place, for instance, when the current window or view containing that button is closed.</p>
<p>We capture these emitted events only <strong>asynchronously</strong>, by defining a function that will execute when a value is emitted, another function when an error is emitted, and another function when 'completed' is emitted. Sometimes these last two can be omitted and you can just focus on defining the function for values. The "listening" to the stream is called <strong>subscribing</strong>. The functions we are defining are observers. The stream is the subject (or "observable") being observed. This is precisely the <a href="https://en.wikipedia.org/wiki/Observer_pattern" target="_blank">Observer Design Pattern</a>.</p>
<p>An alternative way of drawing that diagram is with ASCII, which we will use in some parts of this tutorial:</p>
<pre><code>--a---b-c---d---X---|-&gt;

a, b, c, d are emitted values
X is an error
| is the 'completed' signal
---&gt; is the timeline
</code></pre>
<p>Since this feels so familiar already, and I don't want you to get bored, let's do something new: we are going to create new click event streams transformed out of the original click event stream.</p>
<p>First, let's make a counter stream that indicates how many times a button was clicked. In common Reactive libraries, each stream has many functions attached to it, such as <code>map</code>, <code>filter</code>, <code>scan</code>, etc. When you call one of these functions, such as <code>clickStream.map(f)</code>, it returns a <strong>new stream</strong> based on the click stream. It does not modify the original click stream in any way. This is a property called <strong>immutability</strong>, and it goes together with Reactive streams just like pancakes are good with syrup. That allows us to chain functions like <code>clickStream.map(f).scan(g)</code>:</p>
<pre><code>  clickStream: ---c----c--c----c------c--&gt;
               vvvvv map(c becomes 1) vvvv
               ---1----1--1----1------1--&gt;
               vvvvvvvvv scan(+) vvvvvvvvv
counterStream: ---1----2--3----4------5--&gt;
</code></pre>
<p>The <code>map(f)</code> function replaces (into the new stream) each emitted value according to a function <code>f</code> you provide. In our case, we mapped to the number 1 on each click. The <code>scan(g)</code> function aggregates all previous values on the stream, producing value <code>x = g(accumulated, current)</code>, where <code>g</code> was simply the add function in this example. Then, <code>counterStream</code> emits the total number of clicks whenever a click happens.</p>
<p>To show the real power of Reactive, let's just say that you want to have a stream of "double click" events. To make it even more interesting, let's say we want the new stream to consider triple clicks as double clicks, or in general, multiple clicks (two or more). Take a deep breath and imagine how you would do that in a traditional imperative and stateful fashion. I bet it sounds fairly nasty and involves some variables to keep state and some fiddling with time intervals.</p>
<p>Well, in Reactive it's pretty simple. In fact, the logic is just <a href="http://jsfiddle.net/staltz/4gGgs/27/" target="_blank">4 lines of code</a>.
But let's ignore code for now. Thinking in diagrams is the best way to understand and build streams, whether you're a beginner or an expert.</p>
<p><a href="https://camo.githubusercontent.com/995c301de2f566db10748042a5a67cc5d9ac45d9/687474703a2f2f692e696d6775722e636f6d2f484d47574e4f352e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/995c301de2f566db10748042a5a67cc5d9ac45d9/687474703a2f2f692e696d6775722e636f6d2f484d47574e4f352e706e67" alt="Multiple clicks stream" /></div></a></p>
<p>Grey boxes are functions transforming one stream into another. First we accumulate clicks in lists, whenever 250 milliseconds of "event silence" has happened (that's what <code>buffer(stream.throttle(250ms))</code> does, in a nutshell. Don't worry about understanding the details at this point, we are just demoing Reactive for now). The result is a stream of lists, from which we apply <code>map()</code> to map each list to an integer matching the length of that list. Finally, we ignore <code>1</code> integers using the <code>filter(x &gt;= 2)</code> function. That's it: 3 operations to produce our intended stream. We can then subscribe ("listen") to it to react accordingly how we wish.</p>
<p>I hope you enjoy the beauty of this approach. This example is just the tip of the iceberg: you can apply the same operations on different kinds of streams, for instance, on a stream of API responses; on the other hand, there are many other functions available.</p>
<h2>"Why should I consider adopting RP?"</h2>
<p>Reactive Programming raises the level of abstraction of your code so you can focus on the interdependence of events that define the business logic, rather than having to constantly fiddle with a large amount of implementation details. Code in RP will likely be more concise.</p>
<p>The benefit is more evident in modern webapps and mobile apps that are highly interactive with a multitude of UI events related to data events. 10 years ago, interaction with web pages was basically about submitting a long form to the backend and performing simple rendering to the frontend. Apps have evolved to be more real-time: modifying a single form field can automatically trigger a save to the backend, "likes" to some content can be reflected in real time to other connected users, and so forth.</p>
<p>Apps nowadays have an abundancy of real-time events of every kind that enable a highly interactive experience to the user. We need tools for properly dealing with that, and Reactive Programming is an answer.</p>
<h2>Thinking in RP, with examples</h2>
<p>Let's dive into the real stuff. A real-world example with a step-by-step guide on how to think in RP. No synthetic examples, no half-explained concepts. By the end of this tutorial we will have produced real functioning code, while knowing why we did each thing.</p>
<p>I picked <strong>JavaScript</strong> and <strong><a href="https://github.com/Reactive-Extensions/RxJS" target="_blank">RxJS</a></strong> as the tools for this, for a reason: JavaScript is the most familiar language out there at the moment, and the <a href="http://www.reactivex.io" target="_blank">Rx* library family</a> is widely available for many languages and platforms (<a href="https://rx.codeplex.com/" target="_blank">.NET</a>, <a href="https://github.com/Netflix/RxJava" target="_blank">Java</a>, <a href="https://github.com/Netflix/RxJava/tree/master/language-adaptors/rxjava-scala" target="_blank">Scala</a>, <a href="https://github.com/Netflix/RxJava/tree/master/language-adaptors/rxjava-clojure" target="_blank">Clojure</a>,  <a href="https://github.com/Reactive-Extensions/RxJS" target="_blank">JavaScript</a>, <a href="https://github.com/Reactive-Extensions/Rx.rb" target="_blank">Ruby</a>, <a href="https://github.com/Reactive-Extensions/RxPy" target="_blank">Python</a>, <a href="https://github.com/Reactive-Extensions/RxCpp" target="_blank">C++</a>, <a href="https://github.com/ReactiveCocoa/ReactiveCocoa" target="_blank">Objective-C/Cocoa</a>, <a href="https://github.com/Netflix/RxJava/tree/master/language-adaptors/rxjava-groovy" target="_blank">Groovy</a>, etc). So whatever your tools are, you can concretely benefit by following this tutorial.</p>
<h2>Implementing a "Who to follow" suggestions box</h2>
<p>In Twitter there is this UI element that suggests other accounts you could follow:</p>
<p><a href="https://camo.githubusercontent.com/81e5d63c69768e1b04447d2e246f47540dd83fbd/687474703a2f2f692e696d6775722e636f6d2f65416c4e62306a2e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/81e5d63c69768e1b04447d2e246f47540dd83fbd/687474703a2f2f692e696d6775722e636f6d2f65416c4e62306a2e706e67" alt="Twitter Who to follow suggestions box" /></div></a></p>
<p>We are going to focus on imitating its core features, which are:</p>
<ul>
<li>On startup, load accounts data from the API and display 3 suggestions</li>
<li>On clicking "Refresh", load 3 other account suggestions into the 3 rows</li>
<li>On click 'x' button on an account row, clear only that current account and display another</li>
<li>Each row displays the account's avatar and links to their page</li>
</ul>
<p>We can leave out the other features and buttons because they are minor. And, instead of Twitter, which recently closed its API to the unauthorized public, let's build that UI for following people on Github. There's a <a href="https://developer.github.com/v3/users/#get-all-users" target="_blank">Github API for getting users</a>.</p>
<p>The complete code for this is ready at <a href="http://jsfiddle.net/staltz/8jFJH/48/" target="_blank">http://jsfiddle.net/staltz/8jFJH/48/</a> in case you want to take a peak already.</p>
<h2>Request and response</h2>
<p><strong>How do you approach this problem with Rx?</strong> Well, to start with, (almost) <em>everything can be a stream</em>. That's the Rx mantra. Let's start with the easiest feature: "on startup, load 3 accounts data from the API". There is nothing special here, this is simply about (1) doing a request, (2) getting a response, (3) rendering the response. So let's go ahead and represent our requests as a stream. At first this will feel like overkill, but we need to start from the basics, right?</p>
<p>On startup we need to do only one request, so if we model it as a data stream, it will be a stream with only one emitted value. Later, we know we will have many requests happening, but for now, it is just one.</p>
<pre><code>--a------|-&gt;

Where a is the string 'https://api.github.com/users'
</code></pre>
<p>This is a stream of URLs that we want to request. Whenever a request event happens, it tells us two things: when and what. "When" the request should be executed is when the event is emitted. And "what" should be requested is the value emitted: a string containing the URL.</p>
<p>To create such stream with a single value is very simple in Rx*. The official terminology for a stream is "Observable", for the fact that it can be observed, but I find it to be a silly name, so I call it <em>stream</em>.</p>
<div><pre>var requestStream = Rx.Observable.just('https://api.github.com/users');</pre></div>
<p>But now, that is just a stream of strings, doing no other operation, so we need to somehow make something happen when that value is emitted. That's done by <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypesubscribeobserver--onnext-onerror-oncompleted" target="_blank">subscribing</a> to the stream.</p>
<div><pre>requestStream.subscribe(function(requestUrl) {
  // execute the request
  jQuery.getJSON(requestUrl, function(responseData) {
    // ...
  });
}</pre></div>
<p>Notice we are using a jQuery Ajax callback (which we assume you <a href="http://devdocs.io/jquery/jquery.getjson" target="_blank">should know already</a>) to handle the asynchronicity of the request operation. But wait a moment, Rx is for dealing with <strong>asynchronous</strong> data streams. Couldn't the response for that request be a stream containing the data arriving at some time in the future? Well, at a conceptual level, it sure looks like it, so let's try that.</p>
<div><pre>requestStream.subscribe(function(requestUrl) {
  // execute the request
  var responseStream = Rx.Observable.create(function (observer) {
    jQuery.getJSON(requestUrl)
    .done(function(response) { observer.onNext(response); })
    .fail(function(jqXHR, status, error) { observer.onError(error); })
    .always(function() { observer.onCompleted(); });
  });
  
  responseStream.subscribe(function(response) {
    // do something with the response
  });
}</pre></div>
<p>What <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservablecreatesubscribe" target="_blank"><code>Rx.Observable.create()</code></a> does is create your own custom stream by explicitly informing each observer (or in other words, a "subscriber") about data events (<code>onNext()</code>) or errors (<code>onError()</code>). What we did was just wrap that jQuery Ajax Promise. <strong>Excuse me, does this mean that a Promise is an Observable?</strong></p>
<p>Observable is Promise++. In Rx you can easily convert a Promise to an Observable by doing <code>var stream = Rx.Observable.fromPromise(promise)</code>, so let's use that. The only difference is that Observables are not <a href="http://promises-aplus.github.io/promises-spec/" target="_blank">Promises/A+</a> compliant, but conceptually there is no clash. A Promise is simply an Observable with one single emitted value. Rx streams go beyond promises by allowing many returned values.</p>
<p>This is pretty nice, and shows how Observables are at least as powerful as Promises. So if you believe the Promises hype, keep an eye on what Rx Observables are capable of.</p>
<p>Now back to our example, if you were quick to notice, we have one <code>subscribe()</code> call inside another, which is somewhat akin to callback hell. Also, the creation of <code>responseStream</code> is dependent on <code>requestStream</code>. As you heard before, in Rx there are simple mechanisms for transforming and creating new streams out of others, so we should be doing that.</p>
<p>The one basic function that you should know by now is <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypemapselector-thisarg" target="_blank"><code>map(f)</code></a>, which takes each value of stream A, applies <code>f()</code> on it, and produces a value on stream B. If we do that to our request and response streams, we can map request URLs to response Promises (disguised as streams).</p>
<div><pre>var responseMetastream = requestStream
  .map(function(requestUrl) {
    return Rx.Observable.fromPromise(jQuery.getJSON(requestUrl));
  });</pre></div>
<p>Then we will have created a beast called "<em>metastream</em>": a stream of streams. Don't panic yet. A metastream is a stream where each emitted value is yet another stream. You can think of it as <a href="https://en.wikipedia.org/wiki/Pointer_(computer_programming)" target="_blank">pointers</a>: each emitted value is a <em>pointer</em> to another stream. In our example, each request URL is mapped to a pointer to the promise stream containing the corresponding response.</p>
<p><a href="https://camo.githubusercontent.com/2a8a9cc75acd13443f588fd7f386bd7a6dcb271a/687474703a2f2f692e696d6775722e636f6d2f48486e6d6c61632e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/2a8a9cc75acd13443f588fd7f386bd7a6dcb271a/687474703a2f2f692e696d6775722e636f6d2f48486e6d6c61632e706e67" alt="Response metastream" /></div></a></p>
<p>A metastream for responses looks confusing, and doesn't seem to help us at all. We just want a simple stream of responses, where each emitted value is a JSON object, not a 'Promise' of a JSON object. Say hi to <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypeflatmapselector-resultselector" target="_blank">Mr. Flatmap</a>: a version of <code>map()</code> that "flattens" a metastream, by emitting on the "trunk" stream everything that will be emitted on "branch" streams. Flatmap is not a "fix" and metastreams are not a bug, these are really the tools for dealing with asynchronous responses in Rx.</p>
<div><pre>var responseStream = requestStream
  .flatMap(function(requestUrl) {
    return Rx.Observable.fromPromise(jQuery.getJSON(requestUrl));
  });</pre></div>
<p><a href="https://camo.githubusercontent.com/0b0ac4a249e1c15d7520c220957acfece1af3e95/687474703a2f2f692e696d6775722e636f6d2f4869337a4e7a4a2e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/0b0ac4a249e1c15d7520c220957acfece1af3e95/687474703a2f2f692e696d6775722e636f6d2f4869337a4e7a4a2e706e67" alt="Response stream" /></div></a></p>
<p>Nice. And because the response stream is defined according to request stream, <strong>if</strong> we have later on more events happening on request stream, we will have the corresponding response events happening on response stream, as expected:</p>
<pre><code>requestStream:  --a-----b--c------------|-&gt;
responseStream: -----A--------B-----C---|-&gt;

(lowercase is a request, uppercase is its response)
</code></pre>
<p>Now that we finally have a response stream, we can render the data we receive:</p>
<div><pre>responseStream.subscribe(function(response) {
  // render `response` to the DOM however you wish
});</pre></div>
<p>Joining all the code until now, we have:</p>
<div><pre>var requestStream = Rx.Observable.just('https://api.github.com/users');

var responseStream = requestStream
  .flatMap(function(requestUrl) {
    return Rx.Observable.fromPromise(jQuery.getJSON(requestUrl));
  });

responseStream.subscribe(function(response) {
  // render `response` to the DOM however you wish
});</pre></div>
<h2>The refresh button</h2>
<p>I did not yet mention that the JSON in the response is a list with 100 users. The API only allows us to specify the page offset, and not the page size, so we're using just 3 data objects and wasting 97 others. We can ignore that problem for now, since later on we will see how to cache the responses.</p>
<p>Everytime the refresh button is clicked, the request stream should emit a new URL, so that we can get a new response. We need two things: a stream of click events on the refresh button (mantra: anything can be a stream), and we need to change the request stream to depend on the refresh click stream. Gladly, RxJS comes with tools to make Observables from event listeners.</p>
<div><pre>var refreshButton = document.querySelector('.refresh');
var refreshClickStream = Rx.Observable.fromEvent(refreshButton, 'click');</pre></div>
<p>Since the refresh click event doesn't itself carry any API URL, we need to map each click to an actual URL. Now we change the request stream to be the refresh click stream mapped to the API endpoint with a random offset parameter each time.</p>
<div><pre>var requestStream = refreshClickStream
  .map(function() {
    var randomOffset = Math.floor(Math.random()*500);
    return 'https://api.github.com/users?since=' + randomOffset;
  });</pre></div>
<p>Because I'm dumb and I don't have automated tests, I just broke one of our previously built features. A request doesn't happen anymore on startup, it happens only when the refresh is clicked. Urgh. I need both behaviors: a request when <em>either</em> a refresh is clicked <em>or</em> the webpage was just opened.</p>
<p>We know how to make a separate stream for each one of those cases:</p>
<div><pre>var requestOnRefreshStream = refreshClickStream
  .map(function() {
    var randomOffset = Math.floor(Math.random()*500);
    return 'https://api.github.com/users?since=' + randomOffset;
  });
  
var startupRequestStream = Rx.Observable.just('https://api.github.com/users');</pre></div>
<p>But how can we "merge" these two into one? Well, there's <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypemergemaxconcurrent--other" target="_blank"><code>merge()</code></a>. Explained in the diagram dialect, this is what it does:</p>
<pre><code>stream A: ---a--------e-----o-----&gt;
stream B: -----B---C-----D--------&gt;
          vvvvvvvvv merge vvvvvvvvv
          ---a-B---C--e--D--o-----&gt;
</code></pre>
<p>It should be easy now:</p>
<div><pre>var requestOnRefreshStream = refreshClickStream
  .map(function() {
    var randomOffset = Math.floor(Math.random()*500);
    return 'https://api.github.com/users?since=' + randomOffset;
  });
  
var startupRequestStream = Rx.Observable.just('https://api.github.com/users');

var requestStream = Rx.Observable.merge(
  requestOnRefreshStream, startupRequestStream
);</pre></div>
<p>There is an alternative and cleaner way of writing that, without the intermediate streams.</p>
<div><pre>var requestStream = refreshClickStream
  .map(function() {
    var randomOffset = Math.floor(Math.random()*500);
    return 'https://api.github.com/users?since=' + randomOffset;
  })
  .merge(Rx.Observable.just('https://api.github.com/users'));</pre></div>
<p>Even shorter, even more readable:</p>
<div><pre>var requestStream = refreshClickStream
  .map(function() {
    var randomOffset = Math.floor(Math.random()*500);
    return 'https://api.github.com/users?since=' + randomOffset;
  })
  .startWith('https://api.github.com/users');</pre></div>
<p>The <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypestartwithscheduler-args" target="_blank"><code>startWith()</code></a> function does exactly what you think it does. No matter how your input stream looks like, the output stream resulting of <code>startWith(x)</code> will have <code>x</code> at the beginning. But I'm not <a href="https://en.wikipedia.org/wiki/Don't_repeat_yourself" target="_blank">DRY</a> enough, I'm repeating the API endpoint string. One way to fix this is by moving the <code>startWith()</code> close to the <code>refreshClickStream</code>, to essentially "emulate" a refresh click on startup.</p>
<div><pre>var requestStream = refreshClickStream.startWith('startup click')
  .map(function() {
    var randomOffset = Math.floor(Math.random()*500);
    return 'https://api.github.com/users?since=' + randomOffset;
  });</pre></div>
<p>Nice. If you go back to the point where I "broke the automated tests", you should see that the only difference with this last approach is that I added the <code>startWith()</code>.</p>
<h2>Modelling the 3 suggestions with streams</h2>
<p>Until now, we have only touched a <em>suggestion</em> UI element on the rendering step that happens in the responseStream's <code>subscribe()</code>. Now with the refresh button, we have a problem: as soon as you click 'refresh', the current 3 suggestions are not cleared. New suggestions come in only after a response has arrived, but to make the UI look nice, we need to clean out the current suggestions when clicks happen on the refresh.</p>
<div><pre>refreshClickStream.subscribe(function() {
  // clear the 3 suggestion DOM elements 
});</pre></div>
<p>No, not so fast, pal. This is bad, because we now have <strong>two</strong> subscribers that affect the suggestion DOM elements (the other one being <code>responseStream.subscribe()</code>), and that doesn't really sound like <a href="https://en.wikipedia.org/wiki/Separation_of_concerns" target="_blank">Separation of concerns</a>. Remember the Reactive mantra?</p>
<p><a href="https://camo.githubusercontent.com/e581baffb3db3e4f749350326af32de8d5ba4363/687474703a2f2f692e696d6775722e636f6d2f4149696d5138432e6a7067" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/e581baffb3db3e4f749350326af32de8d5ba4363/687474703a2f2f692e696d6775722e636f6d2f4149696d5138432e6a7067" alt="Mantra" /></div></a></p>
<p>So let's model a suggestion as a stream, where each emitted value is the JSON object containing the suggestion data. We will do this separately for each of the 3 suggestions. This is how the stream for suggestion #1 could look like:</p>
<div><pre>var suggestion1Stream = responseStream
  .map(function(listUsers) {
    // get one random user from the list
    return listUsers[Math.floor(Math.random()*listUsers.length)];
  });</pre></div>
<p>The others, <code>suggestion2Stream</code> and <code>suggestion3Stream</code> can be simply copy pasted from <code>suggestion1Stream</code>. This is not DRY, but it will keep our example simple for this tutorial, plus I think it's a good exercise to think how to avoid repetition in this case.</p>
<p>Instead of having the rendering happen in responseStream's subscribe(), we do that here:</p>
<div><pre>suggestion1Stream.subscribe(function(suggestion) {
  // render the 1st suggestion to the DOM
});</pre></div>
<p>Back to the "on refresh, clear the suggestions", we can simply map refresh clicks to <code>null</code> suggestion data, and include that in the <code>suggestion1Stream</code>, as such:</p>
<div><pre>var suggestion1Stream = responseStream
  .map(function(listUsers) {
    // get one random user from the list
    return listUsers[Math.floor(Math.random()*listUsers.length)];
  })
  .merge(
    refreshClickStream.map(function(){ return null; })
  );</pre></div>
<p>And when rendering, we interpret <code>null</code> as "no data", hence hiding its UI element.</p>
<div><pre>suggestion1Stream.subscribe(function(suggestion) {
  if (suggestion === null) {
    // hide the first suggestion DOM element
  }
  else {
    // show the first suggestion DOM element
    // and render the data
  }
});</pre></div>
<p>The big picture is now:</p>
<pre><code>refreshClickStream: ----------o--------o----&gt;
     requestStream: -r--------r--------r----&gt;
    responseStream: ----R---------R------R--&gt;   
 suggestion1Stream: ----s-----N---s----N-s--&gt;
 suggestion2Stream: ----q-----N---q----N-q--&gt;
 suggestion3Stream: ----t-----N---t----N-t--&gt;
</code></pre>
<p>Where <code>N</code> stands for <code>null</code>.</p>
<p>As a bonus, we can also render "empty" suggestions on startup. That is done by adding <code>startWith(null)</code> to the suggestion streams:</p>
<div><pre>var suggestion1Stream = responseStream
  .map(function(listUsers) {
    // get one random user from the list
    return listUsers[Math.floor(Math.random()*listUsers.length)];
  })
  .merge(
    refreshClickStream.map(function(){ return null; })
  )
  .startWith(null);</pre></div>
<p>Which results in:</p>
<pre><code>refreshClickStream: ----------o---------o----&gt;
     requestStream: -r--------r---------r----&gt;
    responseStream: ----R----------R------R--&gt;   
 suggestion1Stream: -N--s-----N----s----N-s--&gt;
 suggestion2Stream: -N--q-----N----q----N-q--&gt;
 suggestion3Stream: -N--t-----N----t----N-t--&gt;
</code></pre>
<h2>Closing a suggestion and using cached responses</h2>
<p>There is one feature remaining to implement. Each suggestion should have its own 'x' button for closing it, and loading another in its place. At first thought, you could say it's enough to make a new request when any close button is clicked:</p>
<div><pre>var close1Button = document.querySelector('.close1');
var close1ClickStream = Rx.Observable.fromEvent(close1Button, 'click');
// and the same for close2Button and close3Button

var requestStream = refreshClickStream.startWith('startup click')
  .merge(close1ClickStream) // we added this
  .map(function() {
    var randomOffset = Math.floor(Math.random()*500);
    return 'https://api.github.com/users?since=' + randomOffset;
  });</pre></div>
<p>That does not work. It will close and reload <em>all</em> suggestions, rather than just only the one we clicked on. There are a couple of different ways of solving this, and to keep it interesting, we will solve it by reusing previous responses. The API's response page size is 100 users while we were using just 3 of those, so there is plenty of fresh data available. No need to request more.</p>
<p>Again, let's think in streams. When a 'close1' click event happens, we want to use the <em>most recently emitted</em> response on <code>responseStream</code> to get one random user from the list in the response. As such:</p>
<pre><code>    requestStream: --r---------------&gt;
   responseStream: ------R-----------&gt;
close1ClickStream: ------------c-----&gt;
suggestion1Stream: ------s-----s-----&gt;
</code></pre>
<p>In Rx* there is a combinator function called <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypecombinelatestargs-resultselector" target="_blank"><code>combineLatest</code></a> that seems to do what we need. It takes two streams A and B as inputs, and whenever either stream emits a value, <code>combineLatest</code> joins the two most recently emitted values <code>a</code> and <code>b</code> from both streams and outputs a value <code>c = f(x,y)</code>, where <code>f</code> is a function you define. It is better explained with a diagram:</p>
<pre><code>stream A: --a-----------e--------i--------&gt;
stream B: -----b----c--------d-------q----&gt;
          vvvvvvvv combineLatest(f) vvvvvvv
          ----AB---AC--EC---ED--ID--IQ----&gt;

where f is the uppercase function
</code></pre>
<p>We can apply combineLatest() on <code>close1ClickStream</code> and <code>responseStream</code>, so that whenever the close 1 button is clicked, we get the latest response emitted and produce a new value on <code>suggestion1Stream</code>. On the other hand, combineLatest() is symmetric: whenever a new response is emitted on <code>responseStream</code>, it will combine with the latest 'close 1' click to produce a new suggestion. That is interesting, because it allows us to simplify our previous code for <code>suggestion1Stream</code>, like this:</p>
<div><pre>var suggestion1Stream = close1ClickStream
  .combineLatest(responseStream,             
    function(click, listUsers) {
      return listUsers[Math.floor(Math.random()*listUsers.length)];
    }
  )
  .merge(
    refreshClickStream.map(function(){ return null; })
  )
  .startWith(null);</pre></div>
<p>One piece is still missing in the puzzle. The combineLatest() uses the most recent of the two sources, but if one of those sources hasn't emitted anything yet, combineLatest() cannot produce a data event on the output stream. If you look at the ASCII diagram above, you will see that the output has nothing when the first stream emitted value <code>a</code>. Only when the second stream emitted value <code>b</code> could it produce an output value.</p>
<p>There are different ways of solving this, and we will stay with the simplest one, which is simulating a click to the 'close 1' button on startup:</p>
<div><pre>var suggestion1Stream = close1ClickStream.startWith('startup click') // we added this
  .combineLatest(responseStream,             
    function(click, listUsers) {l
      return listUsers[Math.floor(Math.random()*listUsers.length)];
    }
  )
  .merge(
    refreshClickStream.map(function(){ return null; })
  )
  .startWith(null);</pre></div>
<h2>Wrapping up</h2>
<p>And we're done. The complete code for all this was:</p>
<div><pre>var refreshButton = document.querySelector('.refresh');
var refreshClickStream = Rx.Observable.fromEvent(refreshButton, 'click');

var closeButton1 = document.querySelector('.close1');
var close1ClickStream = Rx.Observable.fromEvent(closeButton1, 'click');
// and the same logic for close2 and close3

var requestStream = refreshClickStream.startWith('startup click')
  .map(function() {
    var randomOffset = Math.floor(Math.random()*500);
    return 'https://api.github.com/users?since=' + randomOffset;
  });

var responseStream = requestStream
  .flatMap(function (requestUrl) {
    return Rx.Observable.fromPromise($.ajax({url: requestUrl}));
  });

var suggestion1Stream = close1ClickStream.startWith('startup click')
  .combineLatest(responseStream,             
    function(click, listUsers) {
      return listUsers[Math.floor(Math.random()*listUsers.length)];
    }
  )
  .merge(
    refreshClickStream.map(function(){ return null; })
  )
  .startWith(null);
// and the same logic for suggestion2Stream and suggestion3Stream

suggestion1Stream.subscribe(function(suggestion) {
  if (suggestion === null) {
    // hide the first suggestion DOM element
  }
  else {
    // show the first suggestion DOM element
    // and render the data
  }
});</pre></div>
<p><strong>You can see this working example at <a href="http://jsfiddle.net/staltz/8jFJH/48/" target="_blank">http://jsfiddle.net/staltz/8jFJH/48/</a></strong></p>
<p>That piece of code is small but dense: it features management of multiple events with proper separation of concerns, and even caching of responses. The functional style made the code look more declarative than imperative: we are not giving a sequence of instructions to execute, we are just <strong>telling what something is</strong> by defining relationships between streams. For instance, with Rx we told the computer that <em><code>suggestion1Stream</code> <strong>is</strong> the 'close 1' stream combined with one user from the latest response, besides being <code>null</code> when a refresh happens or program startup happened</em>.</p>
<p>Notice also the impressive absence of control flow elements such as <code>if</code>, <code>for</code>, <code>while</code>, and the typical callback-based control flow that you expect from a JavaScript application. You can even get rid of the <code>if</code> and <code>else</code> in the <code>subscribe()</code> above by using <code>filter()</code> if you want (I'll leave the implementation details to you as an exercise). In Rx, we have stream functions such as <code>map</code>, <code>filter</code>, <code>scan</code>, <code>merge</code>, <code>combineLatest</code>, <code>startWith</code>, and many more to control the flow of an event-driven program. This toolset of functions gives you more power in less code.</p>
<h2>What comes next</h2>
<p>If you think Rx* will be your preferred library for Reactive Programming, take a while to get acquainted with the <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md" target="_blank">big list of functions</a> for transforming, combining, and creating Observables. If you want to understand those functions in diagrams of streams, take a look at <a href="https://github.com/Netflix/RxJava/wiki/Creating-Observables" target="_blank">RxJava's very useful documentation with marble diagrams</a>. Whenever you get stuck trying to do something, draw those diagrams, think on them, look at the long list of functions, and think more. This workflow has been effective in my experience.</p>
<p>Once you start getting the hang of programming with Rx*, it is absolutely required to understand the concept of <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/gettingstarted/creating.md#cold-vs-hot-observables" target="_blank">Cold vs Hot Observables</a>. If you ignore this, it will come back and bite you brutally. You have been warned. Sharpen your skills further by learning real functional programming, and getting acquainted with issues such as side effects that affect Rx*.</p>
<p>But Reactive Programming is not just Rx*. There is <a href="http://baconjs.github.io/" target="_blank">Bacon.js</a> which is intuitive to work with, without the quirks you sometimes encounter in Rx*. The <a href="http://elm-lang.org/" target="_blank">Elm Language</a> lives in its own category: it's a Functional Reactive Programming <strong>language</strong> that compiles to JavaScript + HTML + CSS, and features a <a href="http://debug.elm-lang.org/" target="_blank">time travelling debugger</a>. Pretty awesome.</p>
<p>Rx works great for event-heavy frontends and apps. But it is not just a client-side thing, it works great also in the backend and close to databases. In fact, <a href="http://techblog.netflix.com/2013/02/rxjava-netflix-api.html" target="_blank">RxJava is a key component for enabling server-side concurrency in Netflix's API</a>. Rx is not a framework restricted to one specific type of application or language. It really is a paradigm that you can use when programming any event-driven software.</p>
<p>If this tutorial helped you, <a href="https://twitter.com/intent/tweet?original_referer=https%3A%2F%2Fgist.github.com%2Fstaltz%2F868e7e9bc2a7b8c1f754%2F&text=The%20introduction%20to%20Reactive%20Programming%20you%27ve%20been%20missing&tw_p=tweetbutton&url=https%3A%2F%2Fgist.github.com%2Fstaltz%2F868e7e9bc2a7b8c1f754&via=andrestaltz" target="_blank">tweet it forward</a>.</p>
<hr />
<h3>Legal</h3>
<p>© Andre Cesar de Souza Medeiros (alias "Andre Staltz"), 2014. Unauthorized use and/or duplication of this material without express and written permission from this site’s author and/or owner is strictly prohibited. Excerpts and links may be used, provided that full and clear credit is given to Andre Medeiros and <a href="http://andre.staltz.com" target="_blank">http://andre.staltz.com</a> with appropriate and specific direction to the original content.</p>
<p>"Introduction to Reactive Programming you've been missing" by <a href="http://andre.staltz.com" target="_blank">Andre Staltz</a> is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" target="_blank">Creative Commons Attribution-NonCommercial 4.0 International License</a>.<br />Based on a work at <a href="https://gist.github.com/staltz/868e7e9bc2a7b8c1f754" target="_blank">https://gist.github.com/staltz/868e7e9bc2a7b8c1f754</a>.</p>

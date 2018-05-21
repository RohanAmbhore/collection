<a href="https://addyosmani.com/writing-modular-js/">https://addyosmani.com/writing-modular-js/</a><div id="articleHeader"><h1>Writing Modular JavaScript With AMD, CommonJS & ES Harmony</h1></div>




  <a href="http://twitter.com/share" target="_blank">Tweet</a>






<div>
    <h2>Modularity <small>The Importance Of Decoupling Your Application </small></h2>
  </div>

<p>When we say an application is <strong>modular</strong>, we generally mean it's composed of a set of highly decoupled, distinct pieces of functionality stored in modules. As you probably know, <a href="http://arguments.callee.info/2009/05/18/javascript-design-patterns--mediator/" target="_blank">loose coupling</a> facilitates easier maintainability of apps by removing <i>dependencies</i> where possible. When this is implemented efficiently, its quite easy to see how changes to one part of a system may affect another.</p>

<p>Unlike some more traditional programming languages however, the current iteration of JavaScript (<a href="http://www.ecma-international.org/publications/standards/Ecma-262.htm" target="_blank">ECMA-262</a>) doesn't provide developers with the means to import such modules of code in a clean, organized manner. It's one of the concerns with specifications that haven't required great thought until more recent years where the need for more organized JavaScript applications became apparent.</p>

<p>Instead, developers at present are left to fall back on variations of the <a href="http://www.adequatelygood.com/2010/3/JavaScript-Module-Pattern-In-Depth" target="_blank">module</a> or <a href="http://blog.rebeccamurphey.com/2009/10/15/using-objects-to-organize-your-code" target="_blank">object literal</a> patterns. With many of these, module scripts are strung together in the DOM with namespaces being described by a single global object where it's still possible to incur naming collisions in your architecture. There's also no clean way to handle dependency management without some manual effort or third party tools.</p>


<p>Whilst native solutions to these problems will be arriving in <a href="http://wiki.ecmascript.org/doku.php?id=harmony:modules" target="_blank">ES Harmony</a>, the good news is that writing modular JavaScript has never been easier and you can start doing it today.</p>
<p>In this article, we're going to look at three formats for writing modular JavaScript: <strong>AMD</strong>, <strong>CommonJS</strong> and proposals for the next version of JavaScript, <strong>Harmony</strong>.</p>





<div>
    <h2>Prelude <small>A Note On Script Loaders </small></h2>
  </div>

<p>It's difficult to discuss AMD and CommonJS modules without talking about the elephant in the room - <a href="http://msdn.microsoft.com/en-us/scriptjunkie/hh227261" target="_blank">script loaders</a>. At present, script loading is a means to a goal, that goal being modular JavaScript that can be used in applications today - for this, use of a compatible script loader is unfortunately necessary. In order to get the most out of this article, I recommend gaining a <strong>basic understanding</strong> of how popular script loading tools work so the explanations of module formats make sense in context.</p>

<p>
There are a number of great loaders for handling module loading in the AMD and CJS formats, but my personal preferences are <a href="http://requirejs.org" target="_blank">RequireJS</a> and <a href="https://github.com/unscriptable/curl" target="_blank">curl.js</a>. Complete tutorials on these tools are outside the scope of this article, but I can recommend reading John Hann's post about <a href="http://unscriptable.com/index.php/2011/03/30/curl-js-yet-another-amd-loader/" target="_blank">curl.js</a> and James Burke's <a href="http://requirejs.org/docs/api.html" target="_blank">RequireJS</a> API documentation for more.</p> 

<p>From a production perspective, the use of optimization tools (like the RequireJS optimizer) to concatenate scripts is recommended for deployment when working with such modules. Interestingly, with the <a href="https://github.com/jrburke/almond" target="_blank">Almond</a> AMD shim, RequireJS doesn't need to be rolled in the deployed site and what you might consider a script loader can be easily shifted outside of development.</p>
<p>That said, James Burke would probably say that being able to dynamically load scripts after page load still has its use cases and RequireJS can assist with this too. With these notes in mind, let's get started.</p>




<div>
    <h2>AMD <small>A Format For Writing Modular JavaScript In The Browser </small></h2>
  </div>

<p>The overall goal for the AMD (Asynchronous Module Definition) format is to provide a solution for modular JavaScript that developers can use today. It was born out of Dojo's real world experience using XHR+eval and proponents of this format wanted to avoid any future solutions suffering from the weaknesses of those in the past.</p>

<p>The AMD module format itself is a proposal for defining modules where both the module and dependencies can be <a href="http://dictionary.reference.com/browse/asynchronous" target="_blank">asynchronously</a> loaded. It has a number of distinct advantages including being both asynchronous and highly flexible by nature which removes the tight coupling one might commonly find between code and module identity. Many developers enjoy using it and one could consider it a reliable stepping stone towards the <a href="http://wiki.ecmascript.org/doku.php?id=harmony:modules" target="_blank">module system</a> proposed for ES Harmony.</p>

<p>AMD began as a draft specification for a module format on the CommonJS list but as it wasn't able to reach full concensus, further development of the format moved to the <a href="https://github.com/amdjs" target="_blank">amdjs</a> group.</p>
<p>Today it's embraced by projects including Dojo (1.7), MooTools (2.0), Firebug (1.8) and even jQuery (1.7). Although the term <i>CommonJS AMD format</i> has been seen in the wild on occasion, it's best to refer to it as just AMD or Async Module support as not all participants on the CJS list wished to pursue it.</p>


<div><strong>Note:</strong> There was a time when the proposal was referred to as Modules Transport/C, however as the spec wasn't geared for transporting existing CJS modules, but rather, for defining modules it made more sense to opt for the AMD naming convention.</div><h3>Getting Started With Modules</h3>
<p>The two key concepts you need to be aware of here are the idea of a <code>define</code> method for facilitating module definition and a <code>require</code> method for handling dependency loading. <em>define</em> is used to define named or unnamed modules based on the proposal using the following signature:</p>

<pre><ol><li>define(</li><li>    module_id /*optional*/, </li><li>    [dependencies] /*optional*/, </li><li>    definition function /*function for instantiating the module or object*/</li></ol></pre>

<p>As you can tell by the inline comments, the <code>module_id</code> is an optional argument which is typically only required when non-AMD concatenation tools are being used (there may be some other edge cases where it's useful too). When this argument is left out, we call the module anonymous.</p>

<p>When working with anonymous modules, the idea of a module's identity is DRY, making it trivial to avoid duplication of filenames and code. Because the code is more portable, it can be easily moved to other locations (or around the file-system) without needing to alter the code itself or change its ID. The <code>module_id</code> is equivalent to folder paths in simple packages and when not used in packages. Developers can also run the same code on multiple environments just by using an AMD optimizer that works with a CommonJS environment such as <a href="https://github.com/jrburke/r.js/" target="_blank">r.js</a>. </p>

<p>Back to the define signature, the dependencies argument represents an array of dependencies which are required by the module you are defining and the third argument ('definition function') is a function that's executed to instantiate your module. A barebone module could be defined as follows: </p>

<h4>Understanding AMD: define()</h4>
<pre><ol><li>// A module_id (myModule) is used here for demonstration purposes only</li><li>define('myModule', </li><li>    ['foo', 'bar'], </li><li>    // module definition function</li><li>    // dependencies (foo and bar) are mapped to function parameters</li><li>    function ( foo, bar ) {</li><li>        // return a value that defines the module export</li><li>        // (i.e the functionality we want to expose for consumption)</li><li>        // create your module here</li><li>        var myModule = {</li><li>            doStuff:function(){</li><li>                console.log('Yay! Stuff');</li><li>        return myModule;</li><li>// An alternative example could be..</li><li>define('myModule', </li><li>    ['math', 'graph'], </li><li>    function ( math, graph ) {</li><li>        // Note that this is a slightly different pattern</li><li>        // With AMD, it's possible to define modules in a few</li><li>        // different ways due as it's relatively flexible with</li><li>        // certain aspects of the syntax</li><li>        return {</li><li>            plot: function(x, y){</li><li>                return graph.drawPie(math.randomGrid(x,y));</li></ol></pre>


<p><em>require</em> on the other hand is typically used to load code in a top-level JavaScript file or within a module should you wish to dynamically fetch dependencies. An example of its usage is:</p>

<h4>Understanding AMD: require()</h4>
<pre><ol><li>// Consider 'foo' and 'bar' are two external modules</li><li>// In this example, the 'exports' from the two modules loaded are passed as</li><li>// function arguments to the callback (foo and bar)</li><li>// so that they can similarly be accessed</li><li>require(['foo', 'bar'], function ( foo, bar ) {</li><li>        // rest of your code here</li><li>        foo.doSomething();</li></ol></pre>

<h4>Dynamically-loaded Dependencies</h4>
<pre><ol><li>define(function ( require ) {</li><li>    var isReady = false, foobar;</li><li>    // note the inline require within our module definition</li><li>    require(['foo', 'bar'], function (foo, bar) {</li><li>        isReady = true;</li><li>        foobar = foo() + bar();</li><li>    // we can still return a module</li><li>    return {</li><li>        isReady: isReady,</li><li>        foobar: foobar</li></ol></pre>

<h4>Understanding AMD: plugins</h4>
<p>The following is an example of defining an AMD-compatible plugin:</p>
<pre><ol><li>// With AMD, it's possible to load in assets of almost any kind</li><li>// including text-files and HTML. This enables us to have template</li><li>// dependencies which can be used to skin components either on</li><li>// page-load or dynamically.</li><li>define(['./templates', 'text!./template.md','css!./template.css'],</li><li>    function( templates, template ){</li><li>        console.log(templates);</li><li>        // do some fun template stuff here.</li></ol></pre>
<div><strong>Note:</strong> Although css! is included for loading CSS dependencies in the above example, it's important to remember that this approach has some caveats such as it not being fully possible to establish when the CSS is fully loaded. Depending on how you approach your build, it may also result in CSS being included as a dependency in the optimized file, so use CSS as a loaded dependency in such cases with caution.</div><h4>Loading AMD Modules Using require.js</h4>
<pre><ol><li>require(['app/myModule'], </li><li>    function( myModule ){</li><li>        // start the main module which in-turn</li><li>        // loads other modules</li><li>        var module = new myModule();</li><li>        module.doStuff();</li></ol></pre>

<h4>Loading AMD Modules Using curl.js</h4>
<pre><ol><li>curl(['app/myModule.js'], </li><li>    function( myModule ){</li><li>        // start the main module which in-turn</li><li>        // loads other modules</li><li>        var module = new myModule();</li><li>        module.doStuff();</li></ol></pre>

<h4>Modules With Deferred Dependencies</h4>
<pre><ol><li>// This could be compatible with jQuery's Deferred implementation,</li><li>// futures.js (slightly different syntax) or any one of a number</li><li>// of other implementations</li><li>define(['lib/Deferred'], function( Deferred ){</li><li>    var defer = new Deferred(); </li><li>    require(['lib/templates/?index.html','lib/data/?stats'],</li><li>        function( template, data ){</li><li>            defer.resolve({ template: template, data:data });</li><li>    return defer.promise();</li></ol></pre>


<h4>Why Is AMD A Better Choice For Writing Modular JavaScript?</h4>

<ul>
    <li>Provides a clear proposal for how to approach defining flexible modules. </li>

    <li>Significantly cleaner than the present global namespace and <code>&lt;script&gt;</code> tag solutions many of us rely on. There's a clean way to declare stand-alone modules and dependencies they may have.</li>

    <li>Module definitions are encapsulated, helping us to avoid pollution of the global namespace.</li>

    <li>Works better than some alternative solutions (eg. CommonJS, which we'll be looking at shortly). Doesn't have issues with cross-domain, local or debugging and doesn't have a reliance on server-side tools to be used. Most AMD loaders support loading modules in the browser without a build process.</li>

    <li>Provides a 'transport' approach for including multiple modules in a single file. Other approaches like CommonJS have yet to agree on a transport format.</li>

    <li>It's possible to lazy load scripts if this is needed.</li>
</ul>


  






<h3>AMD Modules With Dojo</h3>

<p>Defining AMD-compatible modules using Dojo is fairly straight-forward. As per above, define any module dependencies in an array as the first argument and provide a callback (factory) which will execute the module once the dependencies have been loaded. e.g:</p>

<pre><ol><li>define(["dijit/Tooltip"], function( Tooltip ){</li><li>    //Our dijit tooltip is now available for local use</li><li>    new Tooltip(...);</li></ol></pre>

<p>Note the anonymous nature of the module which can now be both consumed by a Dojo asynchronous loader, RequireJS or the standard <a href="http://docs.dojocampus.org/dojo/require" target="_blank">dojo.require()</a> module loader that you may be used to using.</p>

<p>For those wondering about module referencing, there are some interesting gotchas that are useful to know here. Although the AMD-advocated way of referencing modules declares them in the dependency list with a set of matching arguments, this isn't supported by the Dojo 1.6 build system - it really only works for AMD-compliant loaders. e.g:</p>

<pre><ol><li>define(["dojo/cookie", "dijit/Tooltip"], function( cookie, Tooltip ){</li><li>    var cookieValue = cookie("cookieName"); </li><li>    new Tree(...); </li></ol></pre>

<p>This has many advances over nested namespacing as modules no longer need to directly reference complete namespaces every time - all we require is the 'dojo/cookie' path in dependencies, which once aliased to an argument, can be referenced by that variable. This removes the need to repeatedly type out 'dojo.' in your applications.</p>

<div><strong>Note:</strong> Although Dojo 1.6 doesn't officially support user-based AMD modules (nor asynchronous loading), it's possible to get this working with Dojo using a number of different script loaders. At present, all Dojo core and Dijit modules have been transformed to the AMD syntax and improved overall AMD support will likely land between 1.7 and 2.0.</div>

<p>The final gotcha to be aware of is that if you wish to continue using the Dojo build system or wish to migrate older modules to this newer AMD-style, the following more verbose version enables easier migration. Notice that dojo and dijit and referenced as dependencies too:</p>

<pre><ol><li>define(["dojo", "dijit", "dojo/cookie", "dijit/Tooltip"], function(dojo, dijit){</li><li>    var cookieValue = dojo.cookie("cookieName");</li><li>    new dijit.Tooltip(...);</li></ol></pre>




<h3>AMD Module Design Patterns (Dojo)</h3>
<p>If you've followed any of my previous posts on the benefits of design patterns, you'll know that they can be highly effective in improving how we approach structuring solutions to common development problems. <a href="http://twitter.com/unscriptable" target="_blank">John Hann</a> recently gave an excellent presentation about AMD module design patterns covering the Singleton, Decorator, Mediator and others. I highly recommend checking out his <a href="http://unscriptable.com/code/AMD-module-patterns/" target="_blank">slides</a> if you get a chance.</p>
<p>Some samples of these patterns can be found below:</p>

<p><strong>Decorator pattern:</strong></p>

<pre><ol><li>// mylib/UpdatableObservable: a decorator for dojo/store/Observable</li><li>define(['dojo', 'dojo/store/Observable'], function ( dojo, Observable ) {</li><li>    return function UpdatableObservable ( store ) {</li><li>        var observable = dojo.isFunction(store.notify) ? store :</li><li>                new Observable(store);</li><li>        observable.updated = function( object ) {</li><li>            dojo.when(object, function ( itemOrArray) {</li><li>                dojo.forEach( [].concat(itemOrArray), this.notify, this );</li><li>        return observable; // makes `new` optional</li><li>// decorator consumer</li><li>// a consumer for mylib/UpdatableObservable</li><li>define(['mylib/UpdatableObservable'], function ( makeUpdatable ) {</li><li>    var observable, updatable, someItem;</li><li>    // ... here be code to get or create `observable`</li><li>    // ... make the observable store updatable</li><li>    updatable = makeUpdatable(observable); // `new` is optional!</li><li>    // ... later, when a cometd message arrives with new data item</li><li>    updatable.updated(updatedItem);</li></ol></pre>

<p><strong>Adapter pattern</strong></p>

<pre><ol><li>// 'mylib/Array' adapts `each` function to mimic jQuery's:</li><li>define(['dojo/_base/lang', 'dojo/_base/array'], function (lang, array) {</li><li>    return lang.delegate(array, {</li><li>        each: function (arr, lambda) {</li><li>            array.forEach(arr, function (item, i) {</li><li>                lambda.call(item, i, item); // like jQuery's each</li><li>// adapter consumer</li><li>// 'myapp/my-module':</li><li>define(['mylib/Array'], function ( array ) {</li><li>    array.each(['uno', 'dos', 'tres'], function (i, esp) {</li><li>        // here, `this` == item</li></ol></pre>



<h3>AMD Modules With jQuery</h3>

<h4>The Basics</h4>
<p>Unlike Dojo, jQuery really only comes with one file, however given the plugin-based nature of the library, we can demonstrate how straight-forward it is to define an AMD module that uses it below.</p>
<pre><ol><li>define(['js/jquery.js','js/jquery.color.js','js/underscore.js'],</li><li>    function($, colorPlugin, _){</li><li>        // Here we've passed in jQuery, the color plugin and Underscore</li><li>        // None of these will be accessible in the global scope, but we</li><li>        // can easily reference them below.</li><li>        // Pseudo-randomize an array of colors, selecting the first</li><li>        // item in the shuffled array</li><li>        var shuffleColor = _.first(_.shuffle(['#666','#333','#111']));</li><li>        // Animate the background-color of any elements with the class</li><li>        // 'item' on the page using the shuffled color</li><li>        $('.item').animate({'backgroundColor': shuffleColor });</li><li>        return {};</li><li>        // What we return can be used by other modules</li></ol></pre>

<p>There is however something missing from this example and it's the concept of registration.</p>

<h4>Registering jQuery As An Async-compatible Module</h4>
<p>One of the key features that landed in jQuery 1.7 was support for registering jQuery as an asynchronous module. There are a number of compatible script loaders (including RequireJS and curl) which are capable of loading modules using an asynchronous module format and this means fewer hacks are required to get things working.</p>

<p>As a result of jQuery's popularity, AMD loaders need to take into account multiple versions of the library being loaded into the same page as you ideally don't want several different versions loading at the same time. Loaders have the option of either specifically taking this issue into account or instructing their users that there are known issues with third party scripts and their libraries.</p>

<p>What the 1.7 addition brings to the table is that it helps avoid issues with other third party code on a page accidentally loading up a version of jQuery on the page that the owner wasn't expecting. You don't want other instances clobbering your own and so this can be of benefit.</p>

<p>The way this works is that the script loader being employed indicates that it supports multiple jQuery versions by specifying that a property, <code>define.amd.jQuery</code> is equal to true. For those interested in more specific implementation details, we register jQuery as a named module as there is a risk that it can be concatenated with other files which may use AMD's <code>define()</code> method, but not use a proper concatenation script that understands anonymous AMD module definitions.</p>

<p>The named AMD provides a safety blanket of being both robust and safe for most use-cases.</p>
<pre>// Account for the existence of more than one global 
// instances of jQuery in the document, cater for testing 
// .noConflict()

var jQuery = this.jQuery || "jQuery", 
$ = this.$ || "$",
originaljQuery = jQuery,
original$ = $,
amdDefined;

define(['jquery'] , function ($) {
    $('.items').css('background','green');
    return function () {};
});

// The very easy to implement flag stating support which 
// would be used by the AMD loader
define.amd = {
    jQuery: true
};

</pre>

<h4>Smarter jQuery Plugins</h4>
<p>I've recently discussed some ideas and examples of how jQuery plugins could be written using Universal Module Definition (<a href="https://github.com/umdjs" target="_blank">UMD</a>) patterns <a href="http://coding.smashingmagazine.com/2011/10/11/essential-jquery-plugin-patterns/" target="_blank">here</a>. UMDs define modules that can work on both the client and server, as well as with all popular script loaders available at the moment. Whilst this is still a new area with a lot of concepts still being finalized, feel free to look at the code samples in the section title <i>AMD && CommonJS</i> below and let me know if you feel there's anything we could do better. </p>


<h4>What Script Loaders & Frameworks Support AMD?</h4>In-browser:


<h5>Server-side:</h5>


<h3>AMD Conclusions</h3>

<p>The above are very trivial examples of just how useful AMD modules can truly be, but they hopefully provide a foundation for understanding how they work.</p>
<p>You may be interested to know that many visible large applications and companies currently use AMD modules as a part of their architecture. These include <a href="http://www.ibm.com" target="_blank">IBM</a> and the <a href="http://www.bbc.co.uk/iplayer/" target="_blank">BBC iPlayer</a>, which highlight just how seriously this format is being considered by developers at an enterprise-level.</p>

<p>For more reasons why many developers are opting to use AMD modules in their applications, you may be interested in <a href="http://tagneto.blogspot.com/2011/04/on-inventing-js-module-formats-and.html" target="_blank">this</a> post by James Burke.</p>









<div>
    <h2>CommonJS <small>A Module Format Optimized For The Server </small></h2>
  </div>

<p><a href="http://www.commonjs.org/" target="_blank">CommonJS</a> are a volunteer working group which aim to design, prototype and standardize JavaScript APIs. To date they've attempted to ratify standards for both <a href="http://www.commonjs.org/specs/modules/1.0/" target="_blank">modules</a> and <a href="http://wiki.commonjs.org/wiki/Packages/1.0" target="_blank">packages</a>. The CommonJS module proposal specifies a simple API for declaring modules server-side and unlike AMD attempts to cover a broader set of concerns such as io, filesystem, promises and more.


</p><h3>Getting Started</h3>
<p>From a structure perspective, a CJS module is a reusable piece of JavaScript which exports specific objects made available to any dependent code - there are typically no function wrappers around such modules (so you won't see <code>define</code> used here for example).</p>

<p>At a high-level they basically contain two primary parts: a free variable named <code>exports</code> which contains the objects a module wishes to make available to other modules and a <code>require</code> function that modules can use to import the exports of other modules.
</p>

<h4>Understanding CJS: require() and exports</h4>
<pre><ol><li>// package/lib is a dependency we require</li><li>var lib = require('package/lib');</li><li>// some behaviour for our module</li><li>function foo(){</li><li>    lib.log('hello world!');</li><li>// export (expose) foo to other modules</li><li>exports.foo = foo;</li></ol></pre>

<h4>Basic consumption of exports</h4>
<pre><ol><li>// define more behaviour we would like to expose</li><li>function foobar(){</li><li>        this.foo = function(){</li><li>                console.log('Hello foo');</li><li>        this.bar = function(){</li><li>                console.log('Hello bar');</li><li>// expose foobar to other modules</li><li>exports.foobar = foobar;</li><li>// an application consuming 'foobar'</li><li>// access the module relative to the path</li><li>// where both usage and module files exist</li><li>// in the same directory</li><li>var foobar = require('./foobar').foobar,</li><li>    test   = new foobar();</li><li>test.bar(); // 'Hello bar'</li></ol></pre>

<h4>AMD-equivalent Of The First CJS Example</h4>

<pre><ol><li>define(['package/lib'], function(lib){</li><li>    // some behaviour for our module</li><li>    function foo(){</li><li>        lib.log('hello world!');</li><li>    // export (expose) foo for other modules</li><li>    return {</li><li>        foobar: foo</li></ol></pre>

<h4>Consuming Multiple Dependencies</h4>

<h5>app.js</h5>
<pre><ol><li>var modA = require('./foo');</li><li>var modB = require('./bar');</li><li>exports.app = function(){</li><li>    console.log('Im an application!');</li><li>exports.foo = function(){</li><li>    return modA.helloWorld();</li></ol></pre>

<h5>bar.js</h5>
<pre><ol><li>exports.name = 'bar';</li></ol></pre>


<h5>foo.js</h5>
<pre><ol><li>require('./bar');</li><li>exports.helloWorld = function(){</li><li>    return 'Hello World!!''</li></ol></pre>

<h4>What Loaders & Frameworks Support CJS?</h4>

<h5>In-browser:</h5>


<h5>Server-side:</h5>





<h4>Is CJS Suitable For The Browser?</h4>

<p>There are developers that feel CommonJS is better suited to server-side development which is one reason there's currently a level of <strong>disagreement</strong> over which format should and will be used as the de facto standard in the pre-Harmony age moving forward. Some of the arguments against CJS include a note that many CommonJS APIs address server-oriented features which one would simply not be able to implement at a browser-level in JavaScript - for example, <em>io</em>, <em>system</em> and <em>js</em> could be considered unimplementable by the nature of their functionality.</p>

<p>That said, it's useful to know how to structure CJS modules regardless so that we can better appreciate how they fit in when defining modules which may be used everywhere. Modules which have applications on both the client and server include validation, conversion and templating engines. The way some developers are approaching choosing which format to use is opting for CJS when a module can be used in a server-side environment and using AMD if this is not the case. </p>

<p>As AMD modules are capable of using plugins and can define more granular things like constructors and functions this makes sense. CJS modules are only able to define objects which can be tedious to work with if you're trying to obtain constructors out of them.</p>

<p>Although it's beyond the scope of this article, you may have also noticed that there were different types of 'require' methods mentioned when discussing AMD and CJS. </p>

<p>The concern with a similar naming convention is of course confusion and the community are currently split on the merits of a global require function. John Hann's suggestion here is that rather than calling it 'require', which would probably fail to achieve the goal of informing users about the different between a global and inner require, it may make more sense to rename the global loader method something else (e.g. the name of the library). It's for this reason that a loader like curl.js uses <code>curl()</code> as opposed to <code>require</code>. </p>

<div>
    <h2>AMD && CommonJS <small>Competing, But Equally Valid Standards</small></h2>
  </div>


<p>Whilst this article has placed more emphasis on using AMD over CJS, the reality is that both formats are valid and have a use. </p>

<p>AMD adopts a browser-first approach to development, opting for asynchronous behaviour and simplified backwards compatability but it doesn't have any concept of File I/O. It supports objects, functions, constructors, strings, JSON and many other types of modules, running natively in the browser. It's incredibly flexible.</p>

<p>CommonJS on the other hand takes a server-first approach, assuming synchronous behaviour, no global <i>baggage</i> as John Hann would refer to it as and it attempts to cater for the future (on the server). What we mean by this is that because CJS supports unwrapped modules, it can feel a little more close to the ES.next/Harmony specifications, freeing you of the <code>define()</code> wrapper that AMD enforces. CJS modules however only support objects as modules.</p>

<p>Although the idea of yet another module format may be daunting, you may be interested in some samples of work on hybrid AMD/CJS and Univeral AMD/CJS modules.</p>

<h4>Basic AMD Hybrid Format (John Hann)</h4>

<pre><ol><li>define( function (require, exports, module){</li><li>    var shuffler = require('lib/shuffle');</li><li>    exports.randomize = function( input ){</li><li>        return shuffler.shuffle(input);</li></ol></pre>


<h4>AMD/CommonJS Universal Module Definition (Variation 2, <a href="https://github.com/umdjs/umd" target="_blank">UMDjs</a>)</h4>
<pre><ol><li> * exports object based version, if you need to make a</li><li> * circular dependency or need compatibility with</li><li> * commonjs-like environments that are not Node.</li><li>(function (define) {</li><li>    //The 'id' is optional, but recommended if this is</li><li>    //a popular web library that is used mostly in</li><li>    //non-AMD/Node environments. However, if want</li><li>    //to make an anonymous module, remove the 'id'</li><li>    //below, and remove the id use in the define shim.</li><li>    define('id', function (require, exports) {</li><li>        //If have dependencies, get them here</li><li>        var a = require('a');</li><li>        //Attach properties to exports.</li><li>        exports.name = value;</li><li>}(typeof define === 'function' && define.amd ? define : function (id, factory) {</li><li>    if (typeof exports !== 'undefined') {</li><li>        //commonjs</li><li>        factory(require, exports);</li><li>    } else {</li><li>        //Create a global function. Only works if</li><li>        //the code does not have dependencies, or</li><li>        //dependencies fit the call pattern below.</li><li>        factory(function(value) {</li><li>            return window[value];</li><li>        }, (window[id] = {}));</li></ol></pre>

<h4>Extensible UMD Plugins With (Variation by myself and Thomas Davis).</h4>

<h5>core.js</h5>
<pre><ol><li>// Module/Plugin core</li><li>// Note: the wrapper code you see around the module is what enables</li><li>// us to support multiple module formats and specifications by </li><li>// mapping the arguments defined to what a specific format expects</li><li>// to be present. Our actual module functionality is defined lower </li><li>// down, where a named module and exports are demonstrated. </li><li>;(function ( name, definition ){</li><li>  var theModule = definition(),</li><li>      // this is considered "safe":</li><li>      hasDefine = typeof define === 'function' && define.amd,</li><li>      // hasDefine = typeof define === 'function',</li><li>      hasExports = typeof module !== 'undefined' && module.exports;</li><li>  if ( hasDefine ){ // AMD Module</li><li>    define(theModule);</li><li>  } else if ( hasExports ) { // Node.js Module</li><li>    module.exports = theModule;</li><li>  } else { // Assign to common namespaces or simply the global object (window)</li><li>    (this.jQuery || this.ender || this.$ || this)[name] = theModule;</li><li>})( 'core', function () {</li><li>    var module = this;</li><li>    module.plugins = [];</li><li>    module.highlightColor = "yellow";</li><li>    module.errorColor = "red";</li><li>  // define the core module here and return the public API</li><li>  // this is the highlight method used by the core highlightAll()</li><li>  // method and all of the plugins highlighting elements different</li><li>  // colors</li><li>  module.highlight = function(el,strColor){</li><li>    // this module uses jQuery, however plain old JavaScript</li><li>    // or say, Dojo could be just as easily used.</li><li>    if(this.jQuery){</li><li>      jQuery(el).css('background', strColor);</li><li>  return {</li><li>      highlightAll:function(){</li><li>        module.highlight('div', module.highlightColor);</li></ol></pre>

<h5>myExtension.js</h5>
<pre><ol><li>;(function ( name, definition ) {</li><li>    var theModule = definition(),</li><li>        hasDefine = typeof define === 'function',</li><li>        hasExports = typeof module !== 'undefined' && module.exports;</li><li>    if ( hasDefine ) { // AMD Module</li><li>        define(theModule);</li><li>    } else if ( hasExports ) { // Node.js Module</li><li>        module.exports = theModule;</li><li>    } else { // Assign to common namespaces or simply the global object (window)</li><li>        // account for for flat-file/global module extensions</li><li>        var obj = null;</li><li>        var namespaces = name.split(".");</li><li>        var scope = (this.jQuery || this.ender || this.$ || this);</li><li>        for (var i = 0; i &lt; namespaces.length; i++) {</li><li>            var packageName = namespaces[i];</li><li>            if (obj && i == namespaces.length - 1) {</li><li>                obj[packageName] = theModule;</li><li>            } else if (typeof scope[packageName] === "undefined") {</li><li>                scope[packageName] = {};</li><li>            obj = scope[packageName];</li><li>})('core.plugin', function () {</li><li>    // define your module here and return the public API</li><li>    // this code could be easily adapted with the core to</li><li>    // allow for methods that overwrite/extend core functionality</li><li>    // to expand the highlight method to do more if you wished.</li><li>    return {</li><li>        setGreen: function ( el ) {</li><li>            highlight(el, 'green');</li><li>        setRed: function ( el ) {</li><li>            highlight(el, errorColor);</li></ol></pre>

<h5>app.js</h5>
<pre><ol><li>$(function(){</li><li>    // the plugin 'core' is exposed under a core namespace in </li><li>    // this example which we first cache</li><li>    var core = $.core;</li><li>    // use then use some of the built-in core functionality to </li><li>    // highlight all divs in the page yellow</li><li>    core.highlightAll();</li><li>    // access the plugins (extensions) loaded into the 'plugin'</li><li>    // namespace of our core module:</li><li>    // Set the first div in the page to have a green background.</li><li>    core.plugin.setGreen("div:first");</li><li>    // Here we're making use of the core's 'highlight' method</li><li>    // under the hood from a plugin loaded in after it</li><li>    // Set the last div to the 'errorColor' property defined in </li><li>    // our core module/plugin. If you review the code further down</li><li>    // you'll see how easy it is to consume properties and methods</li><li>    // between the core and other plugins</li><li>    core.plugin.setRed('div:last');</li></ol></pre>



<div>
    <h2>ES Harmony <small>Modules Of The Future </small></h2>
  </div>

<p><a href="http://www.ecma-international.org/memento/TC39.htm" target="_blank">TC39</a>, the standards body charged with defining the syntax and semantics of ECMAScript and its future iterations is composed of a number of very intelligent developers. Some of these developers (such as <a href="http://twitter.com/slightlylate" target="_blank">Alex Russell</a>) have been keeping a close eye on the evolution of JavaScript usage for large-scale development over the past few years and are acutely aware of the need for better language features for writing more modular JS.</p>

<p>For this reason, there are currently proposals for a number of exciting additions to the language including flexible <a href="http://wiki.ecmascript.org/doku.php?id=harmony:modules" target="_blank">modules</a> that can work on both the client and server, a <a href="http://wiki.ecmascript.org/doku.php?id=harmony:module_loaders" target="_blank">module loader</a> and <a href="http://wiki.ecmascript.org/doku.php?id=harmony:proposals" target="_blank">more</a>. In this section, I'll be showing you some code samples of the syntax for modules in ES.next so you can get a taste of what's to come.</p>

<div><strong>Note: </strong> Although Harmony is still in the proposal phases, you can already try out (partial) features of ES.next that address native support for writing modular JavaScript thanks to Google's <a href="http://code.google.com/p/traceur-compiler/" target="_blank">Traceur</a> compiler. To get up and running with Traceur in under a minute, read this <a href="http://code.google.com/p/traceur-compiler/wiki/GettingStarted" target="_blank">getting started</a> guide. There's also a JSConf <a href="http://traceur-compiler.googlecode.com/svn/branches/v0.10/presentation/index.html" target="_blank">presentation</a> about it that's worth looking at if you're interested in learning more about the project.</div><h3>Modules With Imports And Exports</h3>
<p>If you've read through the sections on AMD and CJS modules you may be familiar with the concept of module dependencies (imports) and module exports (or, the public API/variables we allow other modules to consume). In ES.next, these concepts have been proposed in a slightly more succinct manner with dependencies being specified using an <code>import</code> keyword. <code>export</code> isn't greatly different to what we might expect and I think many developers will look at the code below and instantly 'get' it.</p>

<ul><li><strong>import</strong> declarations bind a module's exports as local variables and may be renamed to avoid name collisions/conflicts.</li>
<li><strong>export</strong> declarations declare that a local-binding of a module is externally visible such that other modules may read the exports but can't modify them. Interestingly, modules may export child modules however can't export modules that have been defined elsewhere. You may also rename exports so their external name differs from their local names.</li></ul> <pre><ol><li>module staff{</li><li>    // specify (public) exports that can be consumed by</li><li>    // other modules</li><li>    export var baker = {</li><li>        bake: function( item ){</li><li>            console.log('Woo! I just baked ' + item);</li><li>module skills{</li><li>    export var specialty = "baking";</li><li>    export var experience = "5 years";</li><li>module cakeFactory{</li><li>    // specify dependencies</li><li>    import baker from staff;</li><li>    // import everything with wildcards</li><li>    import * from skills;</li><li>    export var oven = {</li><li>        makeCupcake: function( toppings ){</li><li>            baker.bake('cupcake', toppings);</li><li>        makeMuffin: function( mSize ){</li><li>            baker.bake('muffin', size);</li></ol></pre>

<h3>Modules Loaded From Remote Sources</h3>
<p>The module proposals also cater for modules which are remotely based (e.g. a third-party API wrapper) making it simplistic to load modules in from external locations. Here's an example of us pulling in the module we defined above and utilizing it:</p>
<pre><ol><li>module cakeFactory from 'http://addyosmani.com/factory/cakes.js';</li><li>cakeFactory.oven.makeCupcake('sprinkles');</li><li>cakeFactory.oven.makeMuffin('large');</li></ol></pre>

<h3>Module Loader API</h3>
<p>The module loader proposed describes a dynamic API for loading modules in highly controlled contexts. Signatures supported on the loader include <code>load( url, moduleInstance, error) </code> for loading modules, <code>createModule( object, globalModuleReferences)</code> and <a href="http://wiki.ecmascript.org/doku.php?id=harmony:module_loaders" target="_blank">others</a>. Here's another example of us dynamically loading in the module we initially defined. Note that unlike the last example where we pulled in a module from a remote source, the module loader API is better suited to dynamic contexts.</p>
<pre><ol><li>Loader.load('http://addyosmani.com/factory/cakes.js',</li><li>    function(cakeFactory){</li><li>        cakeFactory.oven.makeCupcake('chocolate');</li></ol></pre>

<h3>CommonJS-like Modules For The Server</h3>
<p>For developers who are server-oriented, the module system proposed for ES.next isn't just constrained to looking at modules in the browser. Below for examples, you can see a CJS-like module proposed for use on the server:</p>
<pre><ol><li>// io/File.js</li><li>export function open(path) { ... };</li><li>export function close(hnd) { ... };</li></ol></pre>

<pre><ol><li>// compiler/LexicalHandler.js</li><li>module file from 'io/File';</li><li>import { open, close } from file;</li><li>export function scan(in) {</li><li>        var h = open(in) ...</li><li>    finally { close(h) }</li></ol></pre>

<pre><ol><li>module lexer from 'compiler/LexicalHandler';</li><li>module stdlib from '@std';</li><li>//... scan(cmdline[0]) ...</li></ol></pre>

<h3>Classes With Constructors, Getters & Setters</h3>
<p>The notion of a class has always been a contentious issue with purists and we've so far got along with either falling back on JavaScript's <a href="http://javascript.crockford.com/prototypal.html" target="_blank">prototypal</a> nature or through using frameworks or abstractions that offer the ability to use <i>class</i> definitions in a form that desugars to the same prototypal behavior.</p>
<p>In Harmony, classes come as part of the language along with constructors and (finally) some sense of true privacy. In the following examples, I've included some inline comments to help you understand how classes are structured, but you may also notice the lack of the word 'function' in here. This isn't a typo error: TC39 have been making a conscious effort to decrease our abuse of the <code>function</code> keyword for everything and the hope is that this will help simplify how we write code.</p>
<pre><ol><li>class Cake{</li><li>    // We can define the body of a class' constructor</li><li>    // function by using the keyword 'constructor' followed</li><li>    // by an argument list of public and private declarations.</li><li>    constructor( name, toppings, price, cakeSize ){</li><li>        public name = name;</li><li>        public cakeSize = cakeSize;</li><li>        public toppings = toppings;</li><li>        private price = price;</li><li>    // As a part of ES.next's efforts to decrease the unnecessary</li><li>    // use of 'function' for everything, you'll notice that it's</li><li>    // dropped for cases such as the following. Here an identifier</li><li>    // followed by an argument list and a body defines a new method</li><li>    addTopping( topping ){</li><li>        public(this).toppings.push(topping);</li><li>    // Getters can be defined by declaring get before</li><li>    // an identifier/method name and a curly body.</li><li>    get allToppings(){</li><li>        return public(this).toppings;</li><li>    get qualifiesForDiscount(){</li><li>        return private(this).price &gt; 5;</li><li>    // Similar to getters, setters can be defined by using</li><li>    // the 'set' keyword before an identifier</li><li>    set cakeSize( cSize ){</li><li>        if( cSize &lt; 0 ){</li><li>            throw new Error('Cake must be a valid size - </li><li>            either small, medium or large');</li><li>        public(this).cakeSize = cSize;</li></ol></pre>

<h3>ES Harmony Conclusions</h3>
<p>As you can see, ES.next is coming with some exciting new additions. Although Traceur can be used to an extent to try our such features in the present, remember that it may not be the best idea to plan out your system to use Harmony (just yet). There are risks here such as specifications changing and a potential failure at the cross-browser level (IE9 for example will take a while to die) so your best bets until we have both spec finalization and coverage are AMD (for in-browser modules) and CJS (for those on the server).</p>

  





<div>
    <h2>Conclusions And Further Reading <small>A Review</small></h2>
  </div>
<p>In this article we've reviewed several of the options available for writing modular JavaScript using modern module formats. These formats have a number of advantages over using the (classical) module pattern alone including: avoiding a need for developers to create global variables for each module they create, better support for static and dynamic dependency management, improved compatibility with script loaders, better (optional) compatibility for modules on the server and more.</p>

<p>In short, I recommend trying out what's been suggested today as these formats offer a lot of power and flexibility that can help when building applications based on many reusable blocks of functionality.</p>

<p>And that's it for now. If you have further questions about any of the topics covered today, feel free to hit me up on <a href="http://twitter.com/addyosmani" target="_blank">twitter</a> and I'll do my best to help!</p>



<p><small>Copyright Addy Osmani, 2012. All Rights Reserved.</small></p>




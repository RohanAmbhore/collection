<a href="https://tutorialzine.com/2011/06/15-powerful-jquery-tips-and-tricks-for-developers">https://tutorialzine.com/2011/06/15-powerful-jquery-tips-and-tricks-for-developers</a><div id="articleHeader"><h1>                          15 Powerful jQuery Tips and Tricks for Developers                        </h1></div>



                        

                        
                        

                        
                        <div>
                            <p>In this article we will take a look at 15 jQuery techniques which will be useful for your effective use of the library. We will start with a few tips about performance and continue with short introductions to some of the library's more obscure features.</p>
<h2>1) Use the Latest Version of jQuery</h2>
<p>With all the innovation taking place in the jQuery project, one of the easiest ways to improve the performance of your web site is to simply use the latest version of jQuery. Every release of the library introduces optimizations and bug fixes, and most of the time upgrading involves only changing a script tag.</p>
<p>You can even include jQuery directly from Google's servers, which provide <a href="http://code.google.com/apis/libraries/devguide.html" target="_blank">free CDN hosting</a> for a number of JavaScript libraries.</p>
<pre>&lt;!-- Include a specific version of jQuery --&gt;
&lt;script src="http://ajax.googleapis.com/ajax/libs/jquery/1.6.1/jquery.min.js"&gt;&lt;/script&gt;

&lt;!-- Include the latest version in the 1.6 branch --&gt;
&lt;script src="http://ajax.googleapis.com/ajax/libs/jquery/1.6/jquery.min.js"&gt;&lt;/script&gt;</pre>
<p>The latter example will include the latest 1.6.x version automatically as it becomes available, but as pointed out on <a href="http://css-tricks.com/7924-google-cdn-naming/" target="_blank">css-tricks</a>, it is cached only for an hour, so you better not use it in production environments.</p>

  
<h2>2) Keep Selectors Simple</h2>
<p>Up until recently, retrieving DOM elements with jQuery was a finely choreographed combination of parsing selector strings, JavaScript loops and inbuilt APIs like <code>getElementById()</code>, <code>getElementsByTagName()</code> and <code>getElementsByClassName()</code>. But now, all major browsers support <code>querySelectorAll()</code>, which understands CSS query selectors and brings a <a href="http://ejohn.org/blog/queryselectorall-in-firefox-31/" target="_blank">significant performance gain</a>.</p>
<p>However, you should still try to optimize the way you retrieve elements. Not to mention that a lot of users still use older browsers that force jQuery into traversing the DOM tree, which is slow.</p>
<pre>$('li[data-selected="true"] a')   // Fancy, but slow
$('li.selected a')  // Better
$('#elem')  // Best</pre>
<p>Selecting by id is the fastest. If you need to select by class name, prefix it with a tag - <code>$('li.selected')</code>. These optimizations mainly affect older browsers and mobile devices.</p>
<p>Accessing the DOM will always be the slowest part of every JavaScript application, so minimizing it is beneficial. One of the ways to do this, is to cache the results that jQuery gives you. The variable you choose will hold a jQuery object, which you can access later in your script.</p>
<pre>var buttons = $('#navigation a.button');

// Some prefer prefixing their jQuery variables with $:
var $buttons = $('#navigation a.button');</pre>
<p>Another thing worth noting, is that jQuery gives you a large number of <a href="http://api.jquery.com/category/selectors/jquery-selector-extensions/" target="_blank">additional selectors</a> for convenience, such as <code>:visible</code>, <code>:hidden</code>, <code>:animated</code> and more, which are not valid CSS3 selectors. The result is that if you use them the library cannot utilize <code>querySelectorAll()</code>. To remedy the situation, you can first select the elements you want to work with, and later filter them, like this:</p>
<pre>$('a.button:animated');   // Does not use querySelectorAll()
$('a.button').filter(':animated');  // Uses it</pre>
<p>The results of the above are the same, with the exception that the second example is faster.</p>
<h2>3) jQuery Objects as Arrays</h2>
<p>The result of running a selector is a jQuery object. However, the library makes it appear as if you are working with an array by defining index elements and a length.</p>
<pre>// Selecting all the navigation buttons:
var buttons = $('#navigation a.button');

// We can loop though the collection:
for(var i=0;i&lt;buttons.length;i++){
    console.log(buttons[i]);    // A DOM element, not a jQuery object
}

// We can even slice it:
var firstFour = buttons.slice(0,4);</pre>
<p>If performance is what you are after, using a simple <code>for</code> (or a <code>while</code>) loop instead of <code>$.each()</code>, can make your code <a href="http://jsfiddle.net/martinaglv/NcRsV/" target="_blank">several times faster</a>.</p>
<p>Checking the length is also the only way to determine whether your collection contains any elements.</p>
<pre>if(buttons){  // This is always true
    // Do something
}

if(buttons.length){ // True only if buttons contains elements
    // Do something
}</pre>
<h2>4) The Selector Property</h2>
<p>jQuery provides a property which contains the selector that was used to start the chain.</p>
<pre>$('#container li:first-child').selector    // #container li:first-child
$('#container li').filter(':first-child').selector    // #container li.filter(:first-child)</pre>
<p>Although the examples above target the same element, the selectors are quite different. The second one is actually invalid - you can't use it as the basis of a new jQuery object. It only shows that the filter method was used to narrow down the collection.</p>
<h2>5) Create an Empty jQuery Object</h2>
<p>Creating a new jQuery object can bring significant overhead. Sometimes, you might need to create an empty object, and fill it in with the <a href="http://api.jquery.com/add/" target="_blank">add()</a> method later.</p>
<pre>var container = $([]);
container.add(another_element);</pre>
<p>This is also the basis for the <a href="http://jsperf.com/jquery-each-vs-quickeach" target="_blank">quickEach() method</a> that you can use as a faster alternative to the default <code>each()</code>.</p>
<h2>6) Select a Random Element</h2>
<p>As I mentioned above, jQuery adds its own selection filters. As with everything else in the library, you can also create your own. To do this simply add a new function to the <code>$.expr[':']</code> object. One awesome use case was presented by Waldek Mastykarz on <a href="http://blog.mastykarz.nl/jquery-random-filter/" target="_blank">his blog</a>: creating a selector for retrieving a random element. You can see a slightly modified version of his code below:</p>
<pre>(function($){
    var random = 0;

    $.expr[':'].random = function(a, i, m, r) {
        if (i == 0) {
            random = Math.floor(Math.random() * r.length);
        }
        return i == random;
    };

})(jQuery);

// This is how you use it:
$('li:random').addClass('glow');</pre>
<h2>7) Use CSS Hooks</h2>
<p>The <a href="http://api.jquery.com/jQuery.cssHooks/" target="_blank">CSS hooks API</a> was introduced to give developers the ability to get and set particular CSS values. Using it, you can hide browser specific implementations and expose a unified interface for accessing particular properties.</p>
<pre>$.cssHooks['borderRadius'] = {
        get: function(elem, computed, extra){
            // Depending on the browser, read the value of
            // -moz-border-radius, -webkit-border-radius or border-radius
        },
        set: function(elem, value){
            // Set the appropriate CSS3 property
        }
};

// Use it without worrying which property the browser actually understands:
$('#rect').css('borderRadius',5);</pre>
<p>What is even better, is that people have already built a rich <a href="https://github.com/brandonaaron/jquery-cssHooks" target="_blank">library of supported CSS hooks</a> that you can use for free in your next project.</p>
<h2>8) Use Custom Easing Functions</h2>
<p>You have probably heard of the jQuery <a href="http://gsgd.co.uk/sandbox/jquery/easing/" target="_blank">easing plugin</a> by now - it allows you to add effects to your animations. The only shortcoming is that this is another JavaScript file your visitors have to load. Luckily enough, you can simply copy the effect you need from the <a href="http://gsgd.co.uk/sandbox/jquery/easing/jquery.easing.1.3.js" target="_blank">plugin file</a>, and add it to the <code>jQuery.easing</code> object:</p>
<pre>$.easing.easeInOutQuad = function (x, t, b, c, d) {
    if ((t/=d/2) &lt; 1) return c/2*t*t + b;
    return -c/2 * ((--t)*(t-2) - 1) + b;
};

// To use it:
$('#elem').animate({width:200},'slow','easeInOutQuad');</pre>
<h2>9) The $.proxy()</h2>
<p>One of the drawbacks to using callback functions in jQuery has always been that when they are executed by a method of the library, the context is set to a different element. For example, if you have this markup:</p>
<pre>&lt;div id="panel" style="display:none"&gt;
    &lt;button&gt;Close&lt;/button&gt;
&lt;/div&gt;</pre>
<p>And you try to execute this code:</p>
<pre>$('#panel').fadeIn(function(){
    // this points to #panel
    $('#panel button').click(function(){
        // this points to the button
        $(this).fadeOut();
    });
});</pre>
<p>You will run into a problem - the button will disappear, not the panel. With <code>$.proxy</code>, you can write it like this:</p>
<pre>$('#panel').fadeIn(function(){
    // Using $.proxy to bind this:

    $('#panel button').click($.proxy(function(){
        // this points to #panel
        $(this).fadeOut();
    },this));
});</pre>
<p>Which will do what you expect. The <code>$.proxy</code> function takes two arguments - your original function, and a context. It returns a new function in which the value of this is always fixed to the context. You can read more about <a href="http://api.jquery.com/jQuery.proxy/" target="_blank">$.proxy in the docs</a>.</p>
<h2>10) Determine the Weight of Your Page</h2>
<p>A simple fact: the more content your page has, the more time it takes your browser to render it. You can get a quick count of the number of DOM elements on your page by running this in your console:</p>
<pre>console.log( $('*').length );</pre>
<p>The smaller the number, the faster the website is rendered. You can optimize it by removing redundant markup and unnecessary wrapping elements.</p>
<h2>11) Turn your Code into a jQuery Plugin</h2>
<p>If you invest some time in writing a piece of jQuery code, consider turning it into a plugin. This promotes code reuse, limits dependencies and helps you organize your project's code base. Most of the <a href="https://tutorialzine.com/category/tutorials/" target="_blank">tutorials on Tutorialzine</a> are organized as plugins, so that it is easy for people to simply drop them in their sites and use them.</p>
<p>Creating a jQuery plugin couldn't be easier:</p>
<pre>(function($){
    $.fn.yourPluginName = function(){
        // Your code goes here
        return this;
    };
})(jQuery);</pre>
<p>Read a detailed tutorial on <a href="https://tutorialzine.com/2011/02/converting-jquery-code-plugin/" target="_blank">turning jQuery code into a plugin</a>.</p>
<h2>12) Set Global AJAX Defaults</h2>
<p>When triggering AJAX requests in your application, you often need to display some kind of indication that a request is in progress. This can be done by displaying a loading animation, or using a dark overlay. Managing this indicator in every single <code>$.get</code> or <code>$.post</code> call can quickly become tedious.</p>
<p>The best solution is to set global AJAX defaults using one of jQuery's methods.</p>
<pre>// ajaxSetup is useful for setting general defaults:
$.ajaxSetup({
    url         : '/ajax/',
    dataType    : 'json'
});

$.ajaxStart(function(){
    showIndicator();
    disableButtons();
});

$.ajaxComplete(function(){
    hideIndicator();
    enableButtons();
});

/*
    // Additional methods you can use:
    $.ajaxStop();
    $.ajaxError();
    $.ajaxSuccess();
    $.ajaxSend();
*/</pre>
<p>Read the docs about <a href="http://api.jquery.com/category/ajax/" target="_blank">jQuery's AJAX functionality</a>.</p>
<h2>13) Use delay() for Animations</h2>
<p>Chaining animation effects is a powerful tool in every jQuery developer's toolbox. One of the more overlooked features is that you can introduce delays between animations.</p>
<pre>// This is wrong:
$('#elem').animate({width:200},function(){
    setTimeout(function(){
        $('#elem').animate({marginTop:100});
    },2000);
});

// Do it like this:
$('#elem').animate({width:200}).delay(2000).animate({marginTop:100});</pre>
<p>To appreciate how much time jQuery's <code>animation()</code> save us, just imagine if you had to manage everything yourself: you would need to set timeouts, parse property values, keep track of the animation progress, cancel when appropriate and update numerous variables on every step.</p>
<p>Read the docs about <a href="http://api.jquery.com/category/effects/" target="_blank">jQuery animations</a>.</p>
<h2>14) Make Use of  HTML5 Data Attributes</h2>
<p>HTML5 data attributes are a simple means to embed data in a webpage. It is useful for exchanging data between the server and the front end, something that used to require outputting &lt;script&gt; blocks or hidden markup.</p>
<p>With the recent updates to the jQuery <code>data()</code> method, HTML5 data attributes are pulled automatically and are available as entries, as you can see from the example below:</p>
<pre>&lt;div id="d1" data-role="page" data-last-value="43" data-hidden="true"
    data-options='{"name":"John"}'&gt;
&lt;/div&gt;</pre>
<p>To access the data attributes of this div, you would use code like the one below:</p>
<pre>$("#d1").data("role");            // "page"
$("#d1").data("lastValue");     // 43
$("#d1").data("hidden");        // true;
$("#d1").data("options").name;  // "John";</pre>
<p>Read more about <a href="http://api.jquery.com/data/" target="_blank">data() in the jQuery docs</a>.</p>
<h2>15) Local Storage and jQuery</h2>
<p>Local storage is a dead simple API for storing information on the client side. Simply add your data as a property of the global <code>localStorage</code> object:</p>
<pre>localStorage.someData = "This is going to be saved across page refreshes and browser restarts";</pre>
<p>The bad news is that it is not supported in older browsers. This is where you can use one of the <a href="http://plugins.jquery.com/plugin-tags/localstorage" target="_blank">many jQuery plugins</a> that provide different fallbacks if <code>localStorage</code> is not available, which makes client-side storage work almost everywhere.</p>
<p>Here is an example using the <a href="http://www.jstorage.info/" target="_blank">$.jStorage jQuery plugin</a>:</p>
<pre>// Check if "key" exists in the storage
var value = $.jStorage.get("key");
if(!value){
    // if not - load the data from the server
    value = load_data_from_server();
    // and save it
    $.jStorage.set("key",value);
}

// Use value</pre>
<h2>To Wrap it Up</h2>
<p>The techniques presented here will give you a head start in effectively using the jQuery library. If you want something to be added to this list, or if you have any suggestions, use the comment section below.</p>
                            <div>

    

    
    

    <div>

        <h6><strong>Bootstrap Studio</strong></h6>

        <p>The revolutionary web design tool for creating responsive websites and apps.</p>

        <a href="#" target="_blank">Learn more</a>

        
    </div>

    

                        

                        
                    
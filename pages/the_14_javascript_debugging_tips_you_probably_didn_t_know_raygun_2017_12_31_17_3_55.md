<a href="https://raygun.com/javascript-debugging-tips?utm_source=mybridge&utm_medium=blog&utm_campaign=read_more">https://raygun.com/javascript-debugging-tips?utm_source=mybridge&utm_medium=blog&utm_campaign=read_more</a><div id="articleHeader"><h1>The 14 JavaScript debugging tips you probably didn't know</h1></div>
          
          <p>Debug your JavaScript with greater speed and efficiency</p>
          

        

      
    
  
</section>



  


  

    
      

        

        

          <div> <div id="atstbx"><div><table><tr><td><div>SHARES</div></td><td><a target="_blank">Share to LinkedIn<svg><title id="at-svg-linkedin-1">LinkedIn</title></svg>LinkedIn</a><a target="_blank">Share to Facebook<svg><title id="at-svg-facebook-2">Facebook</title></svg>Facebook</a><a target="_blank">Share to Twitter<svg><title id="at-svg-twitter-3">Twitter</title></svg>Twitter</a><a target="_blank">Share to Reddit<svg><title id="at-svg-reddit-4">Reddit</title></svg>Reddit</a><a target="_blank">Share to Hacker News<svg><title id="at-svg-hackernews-5">Hacker News</title></svg>Hacker News</a><a target="_blank">Share to More<svg><title id="at-svg-addthis-6">Addthis</title></svg>More</a></td></tr></table></div></div></div>

<p>Knowing your tools can make a significant difference when it comes to getting things done. Despite JavaScript's reputation as being difficult to debug, if you keep a couple of tricks up your sleeve errors and bugs will take less time to resolve.</p>

<p><strong>We've put together a list of 14 debugging tips that you may not know</strong>, but might want to keep in mind for next time you find yourself needing to debug your JavaScript code! </p>

<p><a href="https://app.raygun.com/signup" target="_blank"><u><strong>If you need to find your JavaScript bugs faster, try Raygun Crash Reporting, which will alert you to bugs and give the stack trace.</strong></u></a></p>

<p>Most of these tips are for Chrome Inspector and Firefox, although many will also work with other inspectors. </p>

<h2>1. ‘debugger;’</h2>

<p>After console.log, 'debugger;' is my favorite quick and dirty debugging tool. Once it's in your code, Chrome will automatically stop there when executing. You can even wrap it in conditionals, so it only runs when you need it.</p>

<pre>if (thisThing) {
    debugger;
}</pre>

<h2>2. Display objects as a table</h2>

<p>Sometimes, you have a complex set of objects that you want to view. You can either console.log them and scroll through the list, or break out the console.table helper. Makes it easier to see what you’re dealing with!</p>

<pre>var animals = [
    { animal: 'Horse', name: 'Henry', age: 43 },
    { animal: 'Dog', name: 'Fred', age: 13 },
    { animal: 'Cat', name: 'Frodo', age: 18 }
];
 
console.table(animals);</pre>

<p>Will output: </p>

<p><a href="/upload/Debugging 2b.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/upload/Debugging 2b.png" alt="Screenshot showing the resulting table for JavaScript debugging tip 2 " /></div></a></p>

<h2>3. Try all the sizes</h2>

<p>While having every single mobile device on your desk would be awesome, it’s not feasible in the real world. How about resizing your viewport instead? Chrome provides you with everything you need. Jump into your inspector and click the <strong>‘toggle device mode’ </strong>button. Watch your media queries come to life!</p>

<p><a href="/upload/Debugging 1 .png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/upload/Debugging 1 .png" /></div></a></p>

<h2>4. How to find your DOM elements quickly</h2>

<p>Mark a DOM element in the elements panel and use it in your console. Chrome Inspector keeps the last five elements in its history so that the final marked element displays with $0, the second to last marked element $1 and so on.</p>

<p>If you mark following items in order ‘item-4′, ‘item-3’, ‘item-2’, ‘item-1’, ‘item-0’ then you can access the DOM nodes like this in the console:</p>

<p><a href="/upload/Debugging 2.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/upload/Debugging 2.png" /></div></a></p>

<h2>5. Benchmark loops using console.time() and console.timeEnd()</h2>

<p>It can be super useful to know exactly how long something has taken to execute, especially when debugging slow loops. You can even set up multiple timers by assigning a label to the method. Let’s see how it works:</p>

<pre>console.time('Timer1');
 
var items = [];
 
for(var i = 0; i &lt; 100000; i++){
   items.push({index: i});
}
 
console.timeEnd('Timer1');</pre>

<p>This has produced the following result:</p>

<p><a href="/upload/Debugging 3.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/upload/Debugging 3.png" /></div></a></p>

<h2>6. Get the stack trace for a function</h2>

<p>You probably know JavaScript frameworks, produce a lot of code – quickly.</p>

<p>It creates views and triggers events, so eventually you'll want to know what caused the function call.</p>

<p>Since JavaScript is not a very structured language, it can sometimes be hard to get an overview of <strong>what</strong> happened and <strong>when</strong>. This is when console.trace (or just trace in the console) comes handy to be able to debug JavaScript.</p>

<p>Imagine you want to see the entire stack trace for the function call funcZ in the car instance on line 33:</p>

<pre>var car;
var func1 = function() {
	func2();
}

var func2 = function() {
	func4();
}
var func3 = function() {
}

var func4 = function() {
	car = new Car();
	car.funcX();
}
var Car = function() {
	this.brand = ‘volvo’;
	this.color = ‘red’;
	this.funcX = function() {
		this.funcY();
	}

	this.funcY = function() {
		this.funcZ();
	}

	this.funcZ = function() {
		console.trace(‘trace car’)
	}
}
func1();
var car; 
var func1 = function() {
	func2();
} 
var func2 = function() {
	func4();
}
var func3 = function() {
} 
var func4 = function() {
	car = new Car();
	car.funcX();
}
var Car = function() {
	this.brand = ‘volvo’;
	this.color = ‘red’;
	this.funcX = function() {
		this.funcY();
	}
	this.funcY = function() {
		this.funcZ();
	}
 	this.funcZ = function() {
		console.trace(‘trace car’)
	}
} 
func1();</pre>

<p>Line 33 will output:</p>

<p><a href="/upload/Debugging 4.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/upload/Debugging 4.png" /></div></a></p>

<p>Now we can see that <strong>func1</strong> called <strong>func2, </strong>which called <strong>func4</strong>. <strong>Func4 </strong>thencreated an instance of <strong>Car</strong> and then called the function<strong> car.funcX</strong>, and so on.</p>

<p>Even though you think you know your script well this can still be quite handy. Let’s say you want to improve your code. Get the trace and your great list of all related functions. Every single one is clickable, and you can now go back and forth between them. It’s like a menu just for you.</p>

<h2>7. Unminify code as an easy way to debug JavaScript</h2>

<p>Sometimes you may have an issue in production, and your source maps didn’t quite make it to the server.<strong> Fear not</strong>. Chrome can unminify your Javascript files to a more human-readable format. The code won’t be as helpful as your real code – but at the very least you can see what’s happening. Click the {} Pretty Print button below the source viewer in the inspector.</p>

<p><a href="/upload/Debugging 5.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/upload/Debugging 5.png" /></div></a></p>

<h2>8. Quick-find a function to debug</h2>

<p>Let’s say you want to set a breakpoint in a function.</p>

<p>The two most common ways to do that is:</p>

<p><strong>1. Find the line in your inspector and add a breakpoint<br />
2. Add a debugger in your script</strong></p>

<p>In both of these solutions, you have to click around in your files to find the particular line you want to debug</p>

<p>What’s probably less common is to use the console. Use debug(funcName) in the console and the script will stop when it reaches the function you passed in.</p>

<p>It’s quick, but the downside is it doesn’t work on private or anonymous functions. But if that’s not the case, it’s probably the fastest way to find a function to debug. (Note: there’s a function called console.debug which is not the same thing.)</p>

<pre>var func1 = function() {
	func2();
};
 
var Car = function() {
	this.funcX = function() {
		this.funcY();
	}
 
	this.funcY = function() {
		this.funcZ();
	}
}
 
var car = new Car();</pre>

<p>Type debug(car.funcY) in the console and the script will stop in debug mode when it gets a function call to car.funcY:</p>

<p><a href="/upload/Debugging 6.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/upload/Debugging 6.png" /></div></a></p>

<h2>9.  Black box scripts that are NOT relevant</h2>

<p>Today we often have a few libraries and frameworks on our web apps. Most of them are well tested and relatively bug-free. But, the debugger still steps into all the files that have no relevance for this debugging task. The solution is to black box the script you don’t need to debug. This could also include your own scripts. <a href="https://raygun.com/blog/javascript-debugging-with-black-box/" target="_blank">Read more about debugging black box in this article. </a></p>

<h2>10. Find the important things in complex debugging</h2>

<p>In more complex debugging we sometimes want to output many lines. One thing you can do to keep a better structure of your outputs is to use more console functions, for example, Console.log, console.debug, console.warn, console.info, console.error and so on. You can then filter them in your inspector. But sometimes this is not really what you want when you need to debug JavaScript. It’s now that YOU can get creative and style your messages. Use CSS and make your own structured console messages when you want to debug JavaScript:</p>

<pre>console.todo = function(msg) {
	console.log(‘ % c % s % s % s‘, ‘color: yellow; background - color: black;’, ‘–‘, msg, ‘–‘);
}
 
console.important = function(msg) {
	console.log(‘ % c % s % s % s’, ‘color: brown; font - weight: bold; text - decoration: underline;’, ‘–‘, msg, ‘–‘);
}
 
console.todo(“This is something that’ s need to be fixed”);
console.important(‘This is an important message’);</pre>

<p>Will output: </p>

<p><a href="/upload/Debugging 7.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/upload/Debugging 7.png" /></div></a></p>

<p><strong>For example:</strong></p>

<p>In the console.log() you can set %s for a string, %i for integers and %c for custom style. You can probably find better ways to use this. If you use a single page framework, you maybe want to have one style for view message and another for models, collections, controllers and so on. Maybe also name the shorter like wlog, clog and mlog use your imagination!</p>

<h2>11. Watch specific function calls and its arguments</h2>

<p>In the Chrome console, you can keep an eye on specific functions. Every time the function is called, it will be logged with the values that it was passed in.</p>

<pre>var func1 = function(x, y, z) {
//....
};</pre>

<p>Will output: </p>

<p><a href="/upload/Debugging 8.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/upload/Debugging 8.png" /></div></a></p>

<p>This is a great way to see which arguments are passed into a function. But I must say it would be good if the console could tell how many arguments to expect. In the above example, func1 expect 3 arguments, but only 2 is passed in. If that’s not handled in the code it could lead to a possible bug.</p>

<h2>12. Quickly access elements in the console</h2>

<p>A faster way to do a querySelector in the console is with the dollar sign. $(‘css-selector’) will return the first match of CSS selector. $$(‘css-selector’) will return all of them. If you are using an element more than once, it’s worth saving it as a variable.</p>

<p><a href="/upload/Debugging 10.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/upload/Debugging 10.png" /></div></a></p>

<h2>13. Postman is great (but Firefox is faster)</h2>

<p>Many developers are using Postman to play around with ajax requests. Postman is excellent, but it can be a bit annoying to open up a new browser window, write new request objects and then test them.</p>

<p>Sometimes it’s easier to use your browser.</p>

<p>When you do, you no longer need to worry about authentication cookies if you are sending to a password-secure page. This is how you would edit and resend requests in Firefox.</p>

<p>Open up the inspector and go to the network tab. Right-click on the desired request and choose Edit and Resend. Now you can change anything you want. Change the header and edit your parameters and hit resend.</p>

<p>Below I present a request twice with different properties:</p>

<p><div class="readableLargeImageContainer"><img src="/upload/Debugging 11.png" alt="When debugging JavaScript, Chrome lets you pause when a DOM element changes" /></div></p>

<h2>14. Break on node change</h2>

<p>The DOM can be a funny thing. Sometimes things change and you don’t know why. However, when you need to debug JavaScript, Chrome lets you pause when a DOM element changes. You can even monitor its attributes. In Chrome Inspector, right click on the element and pick a break on setting to use:</p>

<p><a href="/upload/Debugging 14.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/upload/Debugging 14.png" /></div></a></p>

<h2>Further reading</h2>

<p><strong><a href="https://raygun.com/blog/javascript-debugging-with-black-box/" target="_blank">JavaScript debugging with Blackbox</a></strong></p>

<p><strong><a href="https://raygun.com/blog/jslint-safer-coding/" target="_blank">How to use JSLint for faster, safer debugging with less errors </a></strong></p>

<h2><strong>Want to get 100% visibility on your JavaScript errors?</strong></h2>

<p><strong>Raygun surfaces the diagnostic information you need to detect and diagnose JavaScript errors quickly. With support for all JavaScript frameworks and implemented with a few lines of code, you can start bashing bugs on your coffee break. </strong></p>

<p><a href="https://raygun.com/customer-stories/healthcare-com" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/upload/Luis Alonzo Image.png" alt="Quote image with HealthCare.com - how they got visibility with Raygun" /></div></a></p>


        
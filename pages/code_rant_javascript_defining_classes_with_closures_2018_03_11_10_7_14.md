<a href="http://mikehadlow.blogspot.ca/2010/12/javascript-defining-classes-with.html?m=1">http://mikehadlow.blogspot.ca/2010/12/javascript-defining-classes-with.html?m=1</a><div id="articleHeader"><h1>Javascript: Defining Classes with Closures</h1></div>

<div id="post-body-3722895307501129469">
<p>Over the weekend I watched Douglas Crockford’s five part series on Javascript, <a href="http://www.yuiblog.com/blog/2010/02/03/video-crockonjs-1/" target="_blank">Crockford on Javascript</a>. Probably one of the best video introductions to a programming language I have ever seen.</p>  <p>The section I enjoyed the most was part 3, <a href="http://developer.yahoo.com/yui/theater/video.php?v=crockonjs-3" target="_blank">Function the Ultimate</a>, especially the section where he discusses object creation. I’ve always disliked prototype based inheritance. It’s clumsy, awkward and lacks encapsulation. Crockford shows a much nicer object creation strategy based on closures, which looks something like this:</p>  <div id="codeSnippetWrapper">   <pre id="codeSnippet">var animalsApp = (function(){<br /><br />var new_animal = function(name) {<br />        var animal = {};<br /><br />animal.sayHello = function() {<br />            return "Hello, my name is " + name;<br />        }<br />        return animal;<br />    }<br /><br />var new_dog = function(name) {<br />        var dog = new_animal(name);<br /><br />dog.bark = function() {<br />            return "woof";<br />        }<br />        return dog;<br />    }<br /><br />var new_cat = function(name) {<br />        var cat = new_animal(name);<br /><br />cat.meow = function() {<br />            return "eeooowww";<br />        }<br />        return cat;<br />    }<br /><br />return {<br />        main: function(){<br />            var dog = new_dog("rover");<br /><br />console.log(dog.sayHello());<br />            console.log(dog.bark());<br /><br />var cat = new_cat("tom");<br /><br />console.log(cat.sayHello());<br />            console.log(cat.meow());<br />        }<br />    };<br />}());<br /><br />animalsApp.main();</pre>

  </div>



<p>Using this technique we can create properly encapsulated objects. In the example above, our animalsApp only exposes a single function, main, new_animal, new_dog and new_cat are all private. The class definitions are very clear, any variables or functions defined in the constructor body are private and we only expose members that we explicitly attach to the object (dog.bark = function(){}).</p>

<p>You can run this example using <a href="http://nodejs.org/" target="_blank">node</a>:</p>

<div id="codeSnippetWrapper">
  <pre id="codeSnippet">$ node closureclass.js<br />Hello, my name is rover<br />woof<br />Hello, my name is tom<br />eeooowww</pre>

  </div>  




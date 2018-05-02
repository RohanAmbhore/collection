<a href="https://webapplog.com/es6/">https://webapplog.com/es6/</a><div id="articleHeader"><h1>Top 10 ES6 Features Every Busy JavaScript Developer Must Know</h1></div>
			
										<a href="https://webapplog.com/es6/" title="Top 10 ES6 Features Every Busy JavaScript Developer Must Know" target="_blank" class="readableLinkWithLargeImage">
				<div class="readableLargeImageContainer"><img src="https://m03s6dh33i0jtc3uzfml36au-wpengine.netdna-ssl.com/wp-content/uploads/Death_to_stock_photography_wild_7-700x467.jpg"   alt="10 ES6 Features Every Busy JavaScript Software Engineer Must Know" /></div>				</a>
										<div>
					<a href="https://webapplog.com/es6/#comments" target="_blank">45 Replies</a>				</div>
			
		</header>

				
			
<div id="banerBlueContent">
	<div>Courses on Node.js, React<br /> and JavaScript</div>
	<div>Become an expert with my comprehensive <br /> Node.js, React.js and JavaScript courses.</div>
	<a href="https://node.university/" target="_blank">Learn Full Stack Javascript →</a>
	
	
</div>
<p>I recently went to <a href="http://webapplog.com/html5" target="_blank">HTML5 Dev conference</a> in San Francisco. Half of the talks I went to were about ES6 or, as it’s now called officially, ECMAScript2015. I prefer the more succinct ES6 though.</p>
<p>This essay will give you a quick introduction to ES6. If you don’t know what is ES6, it’s a new JavaScript implementation. If you’re a busy JavaScript software engineer (and who is not?), then proceed reading to learn the best 10 features of the new generation of the most popular programming language—JavaScript.</p>
<p>Here’s the list of the top 10 best ES6 features for a busy software engineer (in no particular order):</p>
<ol>
<li>Default Parameters in ES6</li>
<li>Template Literals in ES6</li>
<li>Multi-line Strings in ES6</li>
<li>Destructuring Assignment in ES6</li>
<li>Enhanced Object Literals in ES6</li>
<li>Arrow Functions in ES6</li>
<li>Promises in ES6</li>
<li>Block-Scoped Constructs Let and Const</li>
<li>Classes in ES6</li>
<li>Modules in ES6</li>
</ol>
<p>Disclaimer: the list if highly biased and subjective. It is in no way was intended to diminish usefulness of other ES6 features, which didn’t make it to the list simply because I had to limit the number to 10.</p>
<p>First, a bit of history because those who don’t know the history can’t make it. This is a brief JavaScript timeline:</p>
<ol>
<li>1995: JavaScript is born as LiveScript</li>
<li>1997: ECMAScript standard is established</li>
<li>1999: ES3 comes out and IE5 is all the rage</li>
<li>2000–2005: XMLHttpRequest, a.k.a. AJAX, gains popularity in app such as Outlook Web Access (2000) and Oddpost (2002), Gmail (2004) and Google Maps (2005).</li>
<li>2009: ES5 comes out (this is what most of us use now) with <code>forEach</code>, <code>Object.keys</code>, <code>Object.create</code> (specially for <a href="http://www.crockford.com" target="_blank">Douglas Crockford</a>), and standard JSON</li>
<li>2015: ES6/ECMAScript2015 comes out; it has mostly syntactic sugar, because people weren’t able to agree on anything more ground breaking (ES7?)</li>
</ol>
<p>Enough with history, let’s get to the business of coding.</p>
<h2>1. Default Parameters in ES6</h2>
<p>Remember we had to do these statements to define default parameters:</p>
<pre><code>var link = function (height, color, url) {
    var height = height || 50
    var color = color || 'red'
    var url = url || 'http://azat.co'
    ...
}
</code></pre>
<p>They were okay until the value was 0 and because 0 is falsy in JavaScript it would default to the hard-coded value instead of becoming the value itself. Of course, who needs 0 as a value (#sarcasmfont), so we just ignored this flaw and used the logic OR anyway… No more! In ES6, we can put the default values right in the signature of the functions:</p>
<pre><code>var link = function(height = 50, color = 'red', url = 'http://azat.co') {
  ...
}
</code></pre>
<p>By the way, this syntax is similar to Ruby!</p>
<h2>2. Template Literals in ES6</h2>
<p>Template literals or interpolation in other languages is a way to output variables in the string. So in ES5 we had to break the string like this:</p>
<pre><code>var name = 'Your name is ' + first + ' ' + last + '.'
var url = 'http://localhost:3000/api/messages/' + id
</code></pre>
<p>Luckily, in ES6 we can use a new syntax <code>${NAME}</code> inside of the back-ticked string:</p>
<pre><code>var name = `Your name is ${first} ${last}.`
var url = `http://localhost:3000/api/messages/${id}`
</code></pre>
<h2>3. Multi-line Strings in ES6</h2>
<p>Another yummy syntactic sugar is multi-line string. In ES5, we had to use one of these approaches:</p>
<pre><code>var roadPoem = 'Then took the other, as just as fair,\n\t'
    + 'And having perhaps the better claim\n\t'
    + 'Because it was grassy and wanted wear,\n\t'
    + 'Though as for that the passing there\n\t'
    + 'Had worn them really about the same,\n\t'

var fourAgreements = 'You have the right to be you.\n\
    You can only be you when you do your best.'
</code></pre>
<p>While in ES6, simply utilize the backticks:</p>
<pre><code>var roadPoem = `Then took the other, as just as fair,
    And having perhaps the better claim
    Because it was grassy and wanted wear,
    Though as for that the passing there
    Had worn them really about the same,`

var fourAgreements = `You have the right to be you.
    You can only be you when you do your best.`
</code></pre>
<h2>4. Destructuring Assignment in ES6</h2>
<p>Destructuring can be a harder concept to grasp, because there’s some magic going on… let’s say you have simple assignments where keys <code>house</code> and <code>mouse</code> are variables <code>house</code> and <code>mouse</code>:</p>
<pre><code>var data = $('body').data(), // data has properties house and mouse
  house = data.house,
  mouse = data.mouse
</code></pre>
<p>Other examples of destructuring assignments (from Node.js):</p>
<pre><code>var jsonMiddleware = require('body-parser').json

var body = req.body, // body has username and password
  username = body.username,
  password = body.password  
</code></pre>
<p>In ES6, we can replace the ES5 code above with these statements:</p>
<pre><code>var {house, mouse} = $('body').data() // we'll get house and mouse variables

var {json: jsonMiddleware} = require('body-parser')

var {username, password} = req.body
</code></pre>
<p>This also works with arrays. Crazy!</p>
<pre><code>var [col1, col2]  = $('.column'),
  [line1, line2, line3, , line5] = file.split('\n')
</code></pre>
<p>It might take some time to get use to the destructuring assignment syntax, but it’s a sweet sugarcoating.</p>
<h2>5. Enhanced Object Literals in ES6</h2>
<p>What you can do with object literals now is mind blowing! We went from a glorified version of JSON in ES5 to something closely resembling classes in ES6.</p>
<p>Here’s a typical ES5 object literal with some methods and attributes/properties:</p>
<pre><code>var serviceBase = {port: 3000, url: 'azat.co'},
    getAccounts = function(){return [1,2,3]}

var accountServiceES5 = {
  port: serviceBase.port,
  url: serviceBase.url,
  getAccounts: getAccounts,
  toString: function() {
    return JSON.stringify(this.valueOf())
  },
  getUrl: function() {return "http://" + this.url + ':' + this.port},
  valueOf_1_2_3: getAccounts()
}
</code></pre>
<p>If we want to be fancy, we can inherit from <code>serviceBase</code> by making it the prototype with the <code>Object.create</code> method:</p>
<pre><code>var accountServiceES5ObjectCreate = Object.create(serviceBase)
var accountServiceES5ObjectCreate = {
  getAccounts: getAccounts,
  toString: function() {
    return JSON.stringify(this.valueOf())
  },
  getUrl: function() {return "http://" + this.url + ':' + this.port},
  valueOf_1_2_3: getAccounts()
}
</code></pre>
<p>I know, <code>accountServiceES5ObjectCreate</code> and <code>accountServiceES5</code> are NOT totally identical, because one object (<code>accountServiceES5</code>) will have the properties in the <code>__proto__</code> object as shown below:</p>
<div id="attachment_1759"><a href="http://m03s6dh33i0jtc3uzfml36au-wpengine.netdna-ssl.com/wp-content/uploads/s-pYuaRxwA0HKoW-BmPPBmWARd9qzHY-dqIRyWg1mhU.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="http://m03s6dh33i0jtc3uzfml36au-wpengine.netdna-ssl.com/wp-content/uploads/s-pYuaRxwA0HKoW-BmPPBmWARd9qzHY-dqIRyWg1mhU.png"   alt="Enhanced Object Literals in ES6" /></div></a><p>Enhanced Object Literals in ES6</p></div>
<p>But for the sake of the example, we’ll consider them similar. So in ES6 object literal, there are shorthands for assignment <code>getAccounts: getAccounts,</code> becomes just <code>getAccounts,</code>. Also, we set the prototype right there in the <code>__proto__`` property which makes sense (not</code>‘<strong>proto</strong>’` though:</p>
<pre><code>var serviceBase = {port: 3000, url: 'azat.co'},
    getAccounts = function(){return [1,2,3]}
var accountService = {
    __proto__: serviceBase,
    getAccounts,
</code></pre>
<p>Also, we can invoke <code>super</code> and have dynamic keys (<code>valueOf_1_2_3</code>):</p>
<pre><code>    toString() {
     return JSON.stringify((super.valueOf()))
    },
    getUrl() {return "http://" + this.url + ':' + this.port},
    [ 'valueOf_' + getAccounts().join('_') ]: getAccounts()
};
console.log(accountService)
</code></pre>
<div id="attachment_1760"><a href="http://m03s6dh33i0jtc3uzfml36au-wpengine.netdna-ssl.com/wp-content/uploads/woRH94fOhCC0aYxgI40qu-dUzHPoxNjhwsLG5U4ob0c.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="http://m03s6dh33i0jtc3uzfml36au-wpengine.netdna-ssl.com/wp-content/uploads/woRH94fOhCC0aYxgI40qu-dUzHPoxNjhwsLG5U4ob0c.png"   alt="Enhanced Object Literals in ES6 II" /></div></a><p>Enhanced Object Literals in ES6 II</p></div>
<p>This is a great enhancement to good old object literals!</p>
<h2>6. Arrow Functions in ES6</h2>
<p>This is probably one feature I waited the most. I love CoffeeScript for its fat arrows. Now we have them in ES6. The fat arrows are amazing because they would make your <code>this</code> behave properly, i.e., <code>this</code> will have the same value as in the context of the function—it won’t mutate. The mutation typically happens each time you create a closure.</p>
<p>Using arrows functions in ES6 allows us to stop using <code>that = this</code> or <code>self = this</code> or <code>_this = this</code> or <code>.bind(this)</code>. For example, this code in ES5 is ugly:</p>
<pre><code>var _this = this
$('.btn').click(function(event){
  _this.sendData()
})
</code></pre>
<p>This is the ES6 code without <code>_this = this</code>:</p>
<pre><code>$('.btn').click((event) =&gt;{
  this.sendData()
})
</code></pre>
<p>Sadly, the ES6 committee decided that having skinny arrows is too much of a good thing for us and they left us with a verbose old <code>function</code> instead. (<a href="https://www.udemy.com/coffeescript/?couponCode=a" target="_blank">Skinny arrow in CoffeeScript</a> works like regular <code>function</code> in ES5 and ES6).</p>
<p>Here’s another example in which we use <code>call</code> to pass the context to the <code>logUpperCase()</code> function in ES5:</p>
<pre><code>var logUpperCase = function() {
  var _this = this

  this.string = this.string.toUpperCase()
  return function () {
    return console.log(_this.string)
  }
}

logUpperCase.call({ string: 'es6 rocks' })()
</code></pre>
<p>While in ES6, we don’t need to mess around with <code>_this</code>:</p>
<pre><code>var logUpperCase = function() {
  this.string = this.string.toUpperCase()
  return () =&gt; console.log(this.string)
}

logUpperCase.call({ string: 'es6 rocks' })()
</code></pre>
<p>Note that you can mix and match old <code>function</code> with <code>=&gt;</code> in ES6 as you see fit. And when an arrow function is used with one line statement, it becomes an expression, i.e,. it will implicitly return the result of that single statement. If you have more than one line, then you’ll need to use <code>return</code> explicitly.</p>
<p>This ES5 code is creating an array from the <code>messages</code> array:</p>
<pre><code>var ids = ['5632953c4e345e145fdf2df8','563295464e345e145fdf2df9']
var messages = ids.map(function (value) {
  return "ID is " + value // explicit return
})
</code></pre>
<p>Will become this in ES6:</p>
<pre><code>var ids = ['5632953c4e345e145fdf2df8','563295464e345e145fdf2df9']
var messages = ids.map(value =&gt; `ID is ${value}`) // implicit return
</code></pre>
<p>Notice that I used the string templates? Another feature from CoffeeScript… I love them!</p>
<p>The parenthesis <code>()</code> are optional for single params in an arrow function signature. You need them when you use more than one param.</p>
<p>In ES5 the code has <code>function</code> with explicit return:</p>
<pre><code>var ids = ['5632953c4e345e145fdf2df8', '563295464e345e145fdf2df9'];
var messages = ids.map(function (value, index, list) {
  return 'ID of ' + index + ' element is ' + value + ' ' // explicit return
})
</code></pre>
<p>And more eloquent version of the code in ES6 with parenthesis around params and implicit return:</p>
<pre><code>var ids = ['5632953c4e345e145fdf2df8','563295464e345e145fdf2df9']
var messages = ids.map((value, index, list) =&gt; `ID of ${index} element is ${value} `) // implicit return
</code></pre>
<h2>7. Promises in ES6</h2>
<p>Promises have been a controversial topic. There were a lot of promise implementations with slightly different syntax. q, bluebird, deferred.js, vow, avow, jquery deferred to name just a few. Others said we don’t need promises and can just use async, generators, callbacks, etc. Gladly, there’s a standard <code>Promise</code> implementation in ES6 now!</p>
<p>Let’s consider a rather trivial example of a delayed asynchronous execution with <code>setTimeout()</code>:</p>
<pre><code>setTimeout(function(){
  console.log('Yay!')
}, 1000)
</code></pre>
<p>We can re-write the code in ES6 with Promise:</p>
<pre><code>var wait1000 =  new Promise(function(resolve, reject) {
  setTimeout(resolve, 1000)
}).then(function() {
  console.log('Yay!')
})
</code></pre>
<p>Or with ES6 arrow functions:</p>
<pre><code>var wait1000 =  new Promise((resolve, reject)=&gt; {
  setTimeout(resolve, 1000)
}).then(()=&gt; {
  console.log('Yay!')
})
</code></pre>
<p>So far, we’ve increased the number of lines of code from three to five without any obvious benefit. That’s right. The benefit will come if we have more nested logic inside of the <code>setTimeout()</code> callback:</p>
<pre><code>setTimeout(function(){
  console.log('Yay!')
  setTimeout(function(){
    console.log('Wheeyee!')
  }, 1000)
}, 1000)
</code></pre>
<p>Can be re-written with ES6 promises:</p>
<pre><code>var wait1000 =  ()=&gt; new Promise((resolve, reject)=&gt; {setTimeout(resolve, 1000)})

wait1000()
  .then(function() {
    console.log('Yay!')
    return wait1000()
  })
  .then(function() {
    console.log('Wheeyee!')
  })
</code></pre>
<p>Still not convinced that Promises are better than regular callbacks? Me neither. I think once you got the idea of callbacks and wrap your head around them, then there’s no need for additional complexity of promises.</p>
<p>Nevertheless, ES6 has Promises for those of you who adore them. Promises have a fail-and-catch-all callback as well which is a nice feature. Take a look at this post for more info on promises: <a href="http://jamesknelson.com/grokking-es6-promises-the-four-functions-you-need-to-avoid-callback-hell" target="_blank"><em>Introduction to ES6 Promises</em></a>.</p>
<h2>8. Block-Scoped Constructs Let and Const</h2>
<p>You might have already seen the weird sounding <code>let</code> in ES6 code. I remember the first time I was in London, I was confused by all those TO LET signs. The ES6 let has nothing to do with renting. This is not a sugarcoating feature. It’s more intricate. <code>let</code> is a new <code>var</code> which allows to scope the variable to the blocks. We define blocks by the curly braces. In ES5, the blocks did NOTHING to the vars:</p>
<pre><code>function calculateTotalAmount (vip) {
  var amount = 0
  if (vip) {
    var amount = 1
  }
  { // more crazy blocks!
    var amount = 100
    {
      var amount = 1000
      }
  }  
  return amount
}

console.log(calculateTotalAmount(true))
</code></pre>
<p>The result will be 1000. Wow! That’s a really bad bug. In ES6, we use <code>let</code> to restrict the scope to the blocks. Vars are function scoped.</p>
<pre><code>function calculateTotalAmount (vip) {
  var amount = 0 // probably should also be let, but you can mix var and let
  if (vip) {
    let amount = 1 // first amount is still 0
  } 
  { // more crazy blocks!
    let amount = 100 // first amount is still 0
    {
      let amount = 1000 // first amount is still 0
      }
  }  
  return amount
}

console.log(calculateTotalAmount(true))
</code></pre>
<p>The value is 0, because the <code>if</code> block also has <code>let</code>. If it had nothing (<code>amount=1</code>), then the expression would have been 1.</p>
<p>When it comes to <code>const</code>, things are easier; it’s just an immutable, and it’s also block-scoped like <code>let</code>. Just to demonstrate, here are a bunch of constants and they all are okay because they belong to different blocks:</p>
<pre><code>function calculateTotalAmount (vip) {
  const amount = 0  
  if (vip) {
    const amount = 1 
  } 
  { // more crazy blocks!
    const amount = 100 
    {
      const amount = 1000
      }
  }  
  return amount
}

console.log(calculateTotalAmount(true))
</code></pre>
<p>In my humble opinion, <code>let</code> and <code>const</code> overcomplicate the language. Without them we had only one behavior, now there are multiple scenarios to consider. ;-(</p>
<h2>9. Classes in ES6</h2>
<p>If you love object-oriented programming (OOP), then you’ll love this feature. It makes writing classes and inheriting from them as easy as liking a comment on Facebook.</p>
<p>Classes creation and usage in ES5 was a pain in the rear, because there wasn’t a keyword <code>class</code> (it was reserved but did nothing). In addition to that, lots of inheritance patterns like <a href="http://javascript.info/tutorial/pseudo-classical-pattern" target="_blank">pseudo classical</a>, <a href="http://www.crockford.com/javascript/inheritance.html" target="_blank">classical</a>, <a href="http://javascript.info/tutorial/factory-constructor-pattern" target="_blank">functional</a> just added to the confusion, pouring gasoline on the fire of religious JavaScript wars.</p>
<p>I won’t show you how to write a class (yes, yes, there are classes, objects inherit from objects) in ES5, because there are many flavors. Let’s take a look at the ES6 example right away. I can tell you that the ES6 class will use prototypes, not the function factory approach. We have a class <code>baseModel</code> in which we can define a <code>constructor</code> and a <code>getName()</code> method:</p>
<pre><code>class baseModel {
  constructor(options = {}, data = []) { // class constructor
    this.name = 'Base'
    this.url = 'http://azat.co/api'
    this.data = data
    this.options = options
  }

    getName() { // class method
      console.log(`Class name: ${this.name}`)
    }
}
</code></pre>
<p>Notice that I’m using default parameter values for options and data. Also, method names don’t need to have the word <code>function</code> or the colon (<code>:</code>) anymore. The other big difference is that you can’t assign properties <code>this.NAME</code> the same way as methods, i.e., you can’t say <code>name</code> at the same indentation level as a method. To set the value of a property, simply assign a value in the constructor.</p>
<p>The <code>AccountModel</code> inherits from <code>baseModel</code> with <code>class NAME extends PARENT_NAME</code>:</p>
<pre><code>class AccountModel extends baseModel {
  constructor(options, data) {
</code></pre>
<p>To call the parent constructor, effortlessly invoke <code>super()</code> with params:</p>
<pre><code>    super({private: true}, ['32113123123', '524214691']) //call the parent method with super
     this.name = 'Account Model'
     this.url +='/accounts/'
   }
</code></pre>
<p>If you want to be really fancy, you can set up a getter like this and <code>accountsData</code> will be a property:</p>
<pre><code> get accountsData() { //calculated attribute getter
    // ... make XHR
    return this.data
  }
}
</code></pre>
<p>So how do you actually use this abracadabra? It’s as easy as tricking a three-year old into thinking Santa Claus is real:</p>
<pre><code>let accounts = new AccountModel(5)
accounts.getName()
console.log('Data is %s', accounts.accountsData)
</code></pre>
<p>In case you’re wondering, the output is:</p>
<pre><code>Class name: Account Model
Data is %s 32113123123,524214691
</code></pre>
<h2>10. Modules in ES6</h2>
<p>As you might now, there were no native modules support in JavaScript before ES6. People came up with AMD, RequireJS, CommonJS and other workarounds. Now there are modules with <code>import</code> and <code>export</code> operands.</p>
<p>In ES5 you would use <code>&lt;script&gt;</code> tags with IIFE, or some library like AMD, while in ES6 you can expose your class with <code>export</code>. I am a Node.js guy, so I’ll use CommonJS which is also a Node.js syntax. It’s straightforward to use CommonJS on the browser with the <a href="http://browserify.org" target="_blank">Browserify</a> bunder. Let’s say we have <code>port</code> variable and <code>getAccounts</code> method in ES5 <code>module.js</code>:</p>
<pre><code>module.exports = {
  port: 3000,
  getAccounts: function() {
    ...
  }
}
</code></pre>
<p>In ES5 <code>main.js</code>, we would <code>require('module')</code> that dependency:</p>
<pre><code>var service = require('module.js')
console.log(service.port) // 3000
</code></pre>
<p>In ES6, we would use <code>export</code> and <code>import</code>. For example, this is our library in the ES6 <code>module.js</code> file:</p>
<pre><code>export var port = 3000
export function getAccounts(url) {
  ...
}
</code></pre>
<p>In the importer ES6 file <code>main.js</code>, we use <code>import {name} from 'my-module'</code> syntax. For example,</p>
<pre><code>import {port, getAccounts} from 'module'
console.log(port) // 3000
</code></pre>
<p>Or we can import everything as a variable <code>service</code> in <code>main.js</code>:</p>
<pre><code>import * as service from 'module'
console.log(service.port) // 3000
</code></pre>
<p>Personally, I find the ES6 modules confusing. Yes, they are more eloquent, but Node.js modules won’t change anytime soon. It’s better to have only one style for browser and server JavaScript, so I’ll stick with CommonJS/Node.js style for now.</p>
<p>The support for ES6 modules in the browsers are not coming anytime soon (as of this writing), so you’ll need something like <a href="http://jspm.io" target="_blank">jspm</a> to use ES6 modules.</p>
<p>For more information and examples on ES6 modules, take a look at <a href="http://exploringjs.com/es6/ch_modules.html" target="_blank">this text</a>. No matter what, write modular JavaScript!</p>
<h2>How to Use ES6 Today (Babel)</h2>
<p>ES6 is finalized, but not fully supported by all browsers (e.g., <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_6_support_in_Mozilla" target="_blank">ES6 Firefox support</a>). To use ES6 today, get a compiler like <a href="https://babeljs.io" target="_blank">Babel</a>. You can run it as a standalone tool or use with your build system. There are Babel <a href="http://babeljs.io/docs/setup" target="_blank">plugins</a> for Grunt, Gulp and Webpack.</p>
<div id="attachment_1758"><a href="http://m03s6dh33i0jtc3uzfml36au-wpengine.netdna-ssl.com/wp-content/uploads/i2AGKyI1Jx5QZnOPrrF2SuyPY9zCCdUPitaBI-KMeyc.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="http://m03s6dh33i0jtc3uzfml36au-wpengine.netdna-ssl.com/wp-content/uploads/i2AGKyI1Jx5QZnOPrrF2SuyPY9zCCdUPitaBI-KMeyc-1024x757.png"   alt="How to Use ES6 Today (Babel)" /></div></a><p>How to Use ES6 Today (Babel)</p></div>
<p>Here’s a Gulp example. Install the plugin:</p>
<pre><code>$ npm install --save-dev gulp-babel
</code></pre>
<p>In <code>gulpfile.js</code>, define a task <code>build</code> that takes <code>src/app.js</code> and compiles it into the <code>build</code> folder:</p>
<pre><code>var gulp = require('gulp'),
  babel = require('gulp-babel')

gulp.task('build', function () {
  return gulp.src('src/app.js')
    .pipe(babel())
    .pipe(gulp.dest('build'))
})
</code></pre>
<h2>Node.js and ES6</h2>
<p>For Node.js, you can compile your Node.js files with a build tool or use a standalone Babel module <code>babel-core</code>. To install it,</p>
<pre><code>$ npm install --save-dev babel-core
</code></pre>
<p>Then in Node.js, you call this function:</p>
<pre><code>require("babel-core").transform(es5Code, options)
</code></pre>
<h2>Summary of ES6 Things</h2>
<p>There are many other noteworthy ES6 features which you probably won’t use (at least not right away). In no particular order:</p>
<ol>
<li>New Math, Number, String, Array and Object methods</li>
<li>Binary and octal number types</li>
<li>Default rest spread</li>
<li><code>For of</code> comprehensions (hello again mighty CoffeeScript!)</li>
<li>Symbols</li>
<li>Tail calls</li>
<li>Generators</li>
<li>New data structures like Map and Set</li>
</ol>
<p>For overachievers who can’t stop learning about ES6, like some people who can’t stop after the first potato chip (just one more!), here’s the list for further reading:</p>




<div id="banerBlackContent">
	<div>Courses on Node.js, <br /> React and JavaScript</div>
	<div>Become an expert with my comprehensive <br /> Node.js, React.js and JavaScript courses.</div>
	<a href="https://node.university/" target="_blank">Learn Full Stack Javascript →</a>
	
</div>
<p>--<br />
Azat Mardan<br /> 
<img src="https://1.gravatar.com/avatar/bf96d0a97418613fcbd6ec2ec9a50f0d?size=100" width="100" alt="Azat Mardan avatar" title="Azat Mardan" /><br />
<a href="https://www.linkedin.com/in/azatm" target="_blank">https://www.linkedin.com/in/azatm</a><br />
To contact Azat, the main author of this blog, submit <a href="http://webapplog.com/azat" target="_blank">the contact form</a>. 
<br /><br />Also, make sure to get 3 amazing resources to <a href="http://eepurl.com/Tj3F9" target="_blank">FREE when you sign up for the newsletter.</a><br /> Simple. <br />Easy. <br />No commitment.</p>					
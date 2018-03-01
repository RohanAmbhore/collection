<a href="https://scotch.io/tutorials/better-javascript-with-es6-pt-ii-a-deep-dive-into-classes">https://scotch.io/tutorials/better-javascript-with-es6-pt-ii-a-deep-dive-into-classes</a><div id="articleHeader"><h1>Better JavaScript with ES6, Pt. II: A Deep Dive into Classes</h1></div>





<h2 id="out-with-the-old-in-with-the-new">
    <a href="#toc-out-with-the-old-in-with-the-new" target="_blank">
      #
      Out with the Old, In with the new
    </a> 
  </h2>
<p>Let's be clear about one thing from the start:</p>
<blockquote>
<p>Under the hood, ES6 classes are not something that is radically new: They mainly provide more convenient syntax to create old-school constructor functions. ~ Axel Rauschmayer</p>
</blockquote>
<p>Functionally, <code>class</code> is little more than syntactic sugar over the prototype-based behavior delegation capabilities we've had all along. This article will take a close look at the basic use of ES2015's <code>class</code> keyword, from the perspective of its relation to prototypes. We'll cover:</p>
<ul>
<li>Defining and instantiating classes;</li>
<li>Creating subclasses with <code>extends</code>;</li>
<li><code>super</code> calls from subclasses; and </li>
<li>Examples of important symbol methods. </li>
</ul>
<p>Along the way, we'll pay special attention to how <code>class</code> maps to prototype-based code under the hood. </p>
<p>Let's take it from the top.</p>
<hr />
<p><em>Note: This is part 2 of the Better JavaScript series. Be sure to check out part 1:</em></p>
<ul>
<li><a href="https://scotch.io/tutorials/better-node-with-es6-pt-i" target="_blank">Better JavaScript with ES6, Part 1: Popular Features</a></li>
</ul>
<h2 id="a-step-back-what-classes-arent">
    <a href="#toc-a-step-back-what-classes-arent" target="_blank">
      #
      A Step Back: What Classes Aren't
    </a> 
  </h2>
<p>JavaScript's "classes" aren't anything like classes in Java, Python, or . . . Really, any other object-oriented language you're likely to have used. Which, by the way, I'll refer to as <em>class</em>-oriented languages, as that's more accurate.</p>
<p>In traditional class-oriented languages, you create <em>classes</em>, which are templates for <em>objects</em>. When you want a new object, you <em>instantiate</em> the class, which tells the language engine to <em>copy</em> the methods and properties of the class into a new entity, called an <em>instance</em>. The <em>instance</em> is your object, and, after instantiation, has absolutely no active relation with the parent class. </p>
<p>JavaScript does <em>not</em> have such copy mechanics. "Instantiating" a <code>class</code> in JavaScript <em>does</em> create a new object, but <em>not</em> one that is independent of its parent class.</p>
<p>Rather, it creates an object that is linked to a <em>prototype</em>. Changes to that prototype propagate to the new object, <em>even after</em> instantiation. </p><div>Related Course: <a href="https://bit.ly/2rVqDcs" target="_blank">Getting Started with JavaScript for Web Development</a></div>
<p>Prototypes are an immensely powerful design pattern in their own right. There are a number of techniques for using them to emulate something like traditional class mechanics, and it's these techniques that <code>class</code> provides compact syntax for.</p>
<p>To summarize:</p>
<ol>
<li>JavaScript <em>does not</em> have classes, the way that Java and other languages have classes; and</li>
<li>JavaScript's <code>class</code> is (mostly) just syntactical sugar for prototypes, which are <em>very</em> different from traditional classes. </li>
</ol>
<p>With that out of the way, let's get our feet wet with <code>class</code>.</p>
<h2 id="base-classes-declarations-expressions">
    <a href="#toc-base-classes-declarations-expressions" target="_blank">
      #
      Base Classes: Declarations & Expressions
    </a> 
  </h2>
<p>You create classes with the <code>class</code> keyword, followed by an identifier, and finally, a code block, called the <em>class body</em>. These are called <strong>class declarations</strong>. Class declarations that don't use the <code>extends</code> keyword are called <em>base classes</em>:</p>
<pre><code>"use strict";

// Food is a base class
class Food {

    constructor (name, protein, carbs, fat) {
        this.name = name;
        this.protein = protein;
        this.carbs = carbs;
        this.fat = fat;
    }

    toString () {
        return `${this.name} | ${this.protein}g P :: ${this.carbs}g C :: ${this.fat}g F`
    }

    print () {
      console.log( this.toString() );
    }
}

const chicken_breast = new Food('Chicken Breast', 26, 0, 3.5);

chicken_breast.print(); // 'Chicken Breast | 26g P :: 0g C :: 3.5g F'
console.log(chicken_breast.protein); // 26 (LINE A)</code></pre>
<p>A few things to note.</p>
<ul>
<li>Classes can <em>only</em> contain method definitions, <strong>not</strong> data properties;</li>
<li>When defining methods, you use <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions" target="_blank">shorthand method definitions</a>;</li>
<li>Unlike when creating objects, you do <em>not</em> separate method definitions in class bodies with commas; and</li>
<li>You <em>can</em> refer to properties on instances of the class directly (Line A).</li>
</ul>
<p>A distinctive feature of classes is the function called <strong>constructor</strong>. This is where you initialize your object's properties. </p>
<p>You don't <em>have</em> to define a constructor function. If you choose not to, the engine will insert an empty one for you:</p>
<pre><code>"use strict";

class NoConstructor { 
    /* JavaScript inserts something like this:
     constructor () { }
    */
}

const nemo = new NoConstructor(); // Works, but pretty boring</code></pre>
<p>Assigning a class to a variable is called a <strong>class expression</strong>, and is an alternative to the above syntax:</p>
<pre><code>"use strict";

// This is an anonymous class expression -- you can't refer to the it by name within the class body.
const Food = class {
    // Class definition is the same as before. . . 
}

// This is a named class expression -- you /can/ refer to this class by name within the class body . . . 
const Food = class FoodClass {
    // Class definition is the same as before . . . 

    //  Adding new method, to demonstrate we can refer to FoodClass by name
    //   within the class . . . 
    printMacronutrients () {
      console.log(`${FoodClass.name} | ${FoodClass.protein} g P :: ${FoodClass.carbs} g C :: ${FoodClass.fat} g F`)
    }
}

const chicken_breast = new Food('Chicken Breast', 26, 0, 3.5);
chicken_breast.printMacronutrients(); // 'Chicken Breast | 26g P :: 0g C :: 3.5g F'

// . . . But /not/ outside of it
try {
    console.log(FoodClass.protein); // ReferenceError 
} catch (err) { 
    // pass
}</code></pre>
<p>This behavior is analogous to that of <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function" target="_blank">anonymous and named function expressions</a>.</p>
<h2 id="creating-subclasses-with-extends-calling-with-super">
    <a href="#toc-creating-subclasses-with-extends-calling-with-super" target="_blank">
      #
      Creating Subclasses with extends & Calling with super
    </a> 
  </h2>
<p>Classes created with <code>extends</code> are called <strong>subclasses</strong>, or <strong>derived classes</strong>. Using them is straightforward. Building on our Food example:</p>
<pre><code>"use strict";

// FatFreeFood is a derived class
class FatFreeFood extends Food {

    constructor (name, protein, carbs) {
        super(name, protein, carbs, 0);
    }

    print () {
        super.print(); 
        console.log(`Would you look at that -- ${this.name} has no fat!`);
    }

}

const fat_free_yogurt = new FatFreeFood('Greek Yogurt', 16, 12);
fat_free_yogurt.print(); // 'Greek Yogurt | 26g P :: 16g C :: 0g F  /  Would you look at that -- Greek Yogurt has no fat!'</code></pre>
<p>Everything we discussed above regarding base classe holds true for derived classes, but with a few additional points.</p>
<ul>
<li>Subclasses are declared with the <code>class</code> keyword, followed by an identifier, and then the <code>extends</code> keyword, followed by an <em>arbitrary expression</em>. This will generally just be an identifier, <a href="https://gist.github.com/sebmarkbage/fac0830dbb13ccbff596" target="_blank">but could, in theory, be a function</a>.</li>
<li>If your derived class needs to refer to the class it extends, it can do so with the <code>super</code> keyword.</li>
<li>A derived class can't contain an empty constructor. Even if all the constructor does is call <code>super()</code>, you'll still have to do so explicitly. It can, however, contain <em>no</em> constructor.</li>
<li>You <em>must</em> call <code>super</code> in the constructor of a derived class before you use <code>this</code>.</li>
</ul>
<p>In JavaScript, there are precisely two use cases for the <code>super</code> keyword. </p>
<ol>
<li><strong>Within subclass constructor calls</strong>. If initializing your derived class requires you to use the parent class's constructor, you can call <code>super(parentConstructorParams[ )</code> within the subclass constructor, passing along any necessary parameters. </li>
<li><strong>To refer to methods in the superclass</strong>. Within normal method definitions, derived classes can refer to methods on the parent class with dot notation: <code>super.methodName</code>. </li>
</ol>
<p>Our <code>FatFreeFood</code> demonstrates both use cases:</p>
<ol>
<li>In the constructor, we simply call <code>super</code>, passing along <code>0</code> as our quantity of fat.</li>
<li>In our <code>print</code> method, we first call <code>super.print</code>, and add additional logic after.</li>
</ol>
<p>Believe it or not, that wraps up the basic syntactical overview of <code>class</code>; this is all you need to start experimenting.</p>
<h2 id="prototypes-a-deep-dive">
    <a href="#toc-prototypes-a-deep-dive" target="_blank">
      #
      Prototypes: A Deep Dive
    </a> 
  </h2>
<p>It's time we turn our attention to how <code>class</code> maps to JavaScript's underlying prototype mechanisms. We'll look at:</p>
<ul>
<li>Creating objects with constructor calls;</li>
<li>The nature of prototype linkages;</li>
<li>Property & method delegation; and</li>
<li>Emulating classes with prototypes</li>
</ul>
<h3>Creating Objects with Constructor Calls</h3>
<p>Constructors are nothing new. Calling <em>any</em> function with the <code>new</code> keyword causes it to return an object -- this is called making a <em>constructor call</em>, and such functions are generally called <em>constructors</em>:</p>
<pre><code>"use strict";

function Food (name, protein, carbs, fat) {
    this.name    = name;
    this.protein = protein;
    this.carbs    = carbs;
    this.fat          = fat;
}

// Calling Food with 'new' is a "constructor call", and results in its returning an object 
const chicken_breast = new Food('Chicken Breast', 26, 0, 3.5);
console.log(chicken_breast.protein) // 26

// Failing to call Food with 'new' results in its returning 'undefined'
const fish = Food('Halibut', 26, 0, 2);
console.log(fish); // 'undefined'</code></pre>
<p>When you call a function with <code>new</code>, four things happen under the hood:</p>
<ol>
<li>A new object gets created (let's call it <strong>O</strong>);</li>
<li><strong>O</strong> gets linked to another object, called its <em>prototype</em>;</li>
<li>The function's <code>this</code> value is set to refer to <strong>O</strong>;</li>
<li>The function implicitly returns <strong>O</strong>.</li>
</ol>
<p>It's between steps three and four that the engine executes your function's specific logic.</p>
<p>Knowing this, we can rewrite our <code>Food</code> function to work <em>without</em> the <code>new</code> keyword:</p>
<pre><code>"use strict";

// Eliminating the need for 'new' -- just for demonstration
function Food (name, protein, carbs, fat) {
       // Step One: Create a new Object
    const obj = { }; 

    // Step Two: Link prototypes -- we'll cover this in greater detail shortly
    Object.setPrototypeOf(obj, Food.prototype);

    // Step Three: Set 'this' to point to our new Object
    //    Since we can't reset `this` inside of a running execution context, 
    //      we simulate Step Three by using 'obj' instead of 'this'
    obj.name    = name;
    obj.protein = protein;
    obj.carbs    = carbs;
    obj.fat         = fat;

    // Step Four: Return the newly created object
    return obj;
}

const fish = Food('Halibut', 26, 0, 2);
console.log(fish.protein); // 26</code></pre>
<p>Three of these four steps are straightforward. Creating an object, assigning properties, and writing a <code>return</code> statement are unlikely to give most developers any conceptual trouble: It's the prototype weirdness that trips people up.</p>
<h3>Grokking the Prototype Chain</h3>
<p>Under normal circumstances, all objects in JavaScript -- including Functions -- are linked to another object, called its <em>prototype</em>. </p>
<p>If you request a property on an object that the object doesn't have, JavaScript checks the object's prototype for that property. In other words, if you ask for a property on an object that the object doesn't have, it says: "I don't know. Ask my prototype."</p>
<p>This process -- referring lookups for nonexistent properties to another object -- is called <em>delegation</em>.</p>
<pre><code>"use strict";

// joe has no toString property . . . 
const joe    = { name : 'Joe' },
       sara  = { name : 'Sara' };

Object.hasOwnProperty(joe, toString); // false
Object.hasOwnProperty(sara, toString); // false

// . . . But we can call it anyway!
joe.toString(); // '[object Object]', instead of ReferenceError!
sara.toString(); // '[object Object]', instead of ReferenceError!</code></pre>
<p>The output from our <code>toString</code> calls is utterly useless, but note that this snippet doesn't raise a single <code>ReferenceError</code>! That's because, while neither <code>joe</code> or <code>sara</code> has a <code>toString</code> property, <em>their prototype does</em>.</p>
<p>When we look for <code>sara.toString()</code>, <code>sara</code> says, "I don't have a <code>toString</code> property. Ask my prototype." JavaScript, obligingly, does as told, and asks <code>Object.prototype</code> if <em>it</em> has a <code>toString</code> property. Since it does, it hands <code>Object.prototype</code>'s <code>toString</code> back to our program, which executes it. </p>
<p>It doesn't matter that <code>sara</code> didn't have the property herself -- <em>we just delegated the lookup to the prototype</em>.</p>
<p>In other words, we can access non-existent properties on an object <em>as long as that object's prototype <strong>does</strong> have those properties</em>. We can take advantage of this by assigning properties and methods to an object's prototype, so that we can use them as if they existed on the object itself. </p>
<p>Even better, if several objects share the same prototype -- as is the case with <code>joe</code> and <code>sara</code> above -- they can <em>all</em> access that prototype's properties, immediately after we assign them, <em>without</em> our having to copy those properties or methods to each individual object. </p>
<p>This is what people generally refer to as <em>prototypical/prototypal inheritance</em> -- if my object doesn't have it, but my object's prototype does, my object <em>inherits</em> the property. </p>
<p>In reality, there's no "inheritance" going on, here. In class-oriented languages, inheritance implies behavior is <em>copied</em> from a parent to a child. In JavaScript, no such copying takes place -- which is, in fact, one of the major benefits of prototypes over classes.</p>
<p>Here's a quick recap before we see precisely where these prototypes come from:</p>
<ul>
<li><code>joe</code> and <code>sara</code> do <em>not</em> "inherit" a <code>toString</code> property;</li>
<li><code>joe</code> and <code>sara</code>, as a matter of fact, do <em>not</em> "inherit" from <code>Object.prototype</code> <em>at all</em>;</li>
<li><code>joe</code> and <code>sara</code> <em>are</em> <strong>linked</strong> to <code>Object.prototype</code>;</li>
<li>Both <code>joe</code> and <code>sara</code> are linked to the <em>same</em> <code>Object.prototype</code>.</li>
<li>To find the prototype of an object -- let's call it <strong>O</strong> -- you use: <code>Object.getPrototypeOf(O)</code>.</li>
</ul>
<p>And, just to hammer it home: Objects do not "inherit from" their prototypes. They <em>delegate</em> to them.</p>
<p>Period.</p>
<p>Let's dig deeper.</p>
<h2 id="setting-an-objects-prototype">
    <a href="#toc-setting-an-objects-prototype" target="_blank">
      #
      Setting an Object's Prototype
    </a> 
  </h2>
<p>We learned above that (almost) every object (<strong>O</strong>) has a <em>prototype</em> (<strong>P</strong>), and that, when you look for a property on <strong>O</strong> that <strong>O</strong> doesn't have, the JavaScript engine will look for that property on <strong>P</strong> instead.</p>
<p>From here, the questions are:</p>
<ol>
<li>How do <em>functions</em> play into all of this?</li>
<li>Where do these prototypes come from, anyway?</li>
</ol>
<h3>A Function Named Object</h3>
<p>Before the JavaScript engine executes a program, it builds an environment to run it in, in which it creates a function, called <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object" target="_blank">Object</a>, and an associated object, called <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype" target="_blank">Object.prototype</a>. </p>
<p>In other words, <code>Object</code> and <code>Object.prototype</code> <em>always</em> exist, in <em>any</em> executing JavaScript program.</p>
<p>The <em>function</em>, <code>Object</code>, is like any other function. In particular, it's a <em>constructor</em> -- calling it returns a new object:</p>
<pre><code>"use strict";

typeof new Object(); // "object"
typeof Object();         // A peculiarity of the Object function is that it does /not/ need to be called with new.</code></pre>
<p>The <em>object</em>, <code>Object.prototype</code>, is . . . Well, an object. And, like many objects, it has properties.</p>
<p><div class="readableLargeImageContainer"><img alt="Properties on Object.prototype" /></div></p>
<p>Here's what you need to know about <code>Object</code> and <code>Object.prototype</code>:</p>
<ol>
<li>The <em>function</em>, <code>Object</code>, has a property, called <code>.prototype</code>, which points to an object (<code>Object.prototype</code>);</li>
<li>The <em>object</em>, <code>Object.prototype</code>, has a property, called <code>.constructor</code>, which points to a function (<code>Object</code>).</li>
</ol>
<p>As it turns out, this general scheme is true for <em>all</em> functions in JavaScript. When you create a function -- <code>someFunction</code> -- it will have a property, <code>.prototype</code>, that points to an object, called <code>someFunction.prototype</code>.</p>
<p>Conversely, that object -- <code>someFunction.prototype</code> -- will have a property, called <code>.constructor</code>, which points <em>back</em> to the function <code>someFunction</code>.</p>
<pre><code>"use strict";

function foo () {  console.log('Foo!');  }

console.log(foo.prototype); // Points to an object called 'foo'
console.log(foo.prototype.constructor); // Points to the function, 'foo'

foo.prototype.constructor(); // Prints 'Foo!' -- just proving that 'foo.prototype.constructor' does, in fact, point to our original function </code></pre>
<p>The major points to keep in mind are these:</p>
<ol>
<li>All functions have a property, called <code>.prototype</code>, which points to an object associated with that function.</li>
<li>All function prototypes have a property, called <code>.constructor</code>, which points back to the function.</li>
<li>A function prototype's <code>.constructor</code> does not necessarily point to the function that created the function prototype . . . Confusingly enough. We'll touch on this in greater detail soon.</li>
</ol>
<p>These are the rules for setting a <em>function's</em> prototype. With that out of the way, we can cover three rules for setting an object's prototype:</p>
<ol>
<li>The "default" rule;</li>
<li>Setting the prototype implicitly, with <code>new</code>;</li>
<li>Setting the prototype explicitly, with <code>Object.create</code>.</li>
</ol>
<h3>The Default Rule</h3>
<p>Consider this snippet:</p>
<pre><code>"use strict";

const foo = { status : 'foobar' };</code></pre>
<p>Refreshingly simple. All we've done is create an object, called <code>foo</code>, and give it a property, called <code>status</code>.</p>
<p>Behind the scenes, however, JavaScript does a little extra work. When we create an object literal, JavaScript sets the object's prototype reference to <code>Object.prototype</code>, and sets its <code>.constructor</code> reference to <code>Object</code>:</p>
<pre><code>"use strict";

const foo = { status : 'foobar' };

Object.getPrototypeOf(foo) === Object.prototype; // true
foo.constructor === Object; // true</code></pre>
<h3>Setting the Prototype Implicitly with <code>new</code></h3>
<p>Let's take another look at our modified <code>Food</code> example.</p>
<pre><code>"use strict";

function Food (name, protein, carbs, fat) {
    this.name    = name;
    this.protein = protein;
    this.carbs    = carbs;
    this.fat          = fat;
}</code></pre>
<p>By now, we know that the <em>function</em> <code>Food</code> will be associated with an <em>object</em>, called <code>Food.prototype</code>. </p>
<p>When we create an object using the <code>new</code> keyword, JavaScript:</p>
<ol>
<li>Sets the object's prototype reference to the <code>.prototype</code> property of the function you called with <code>new</code>; and</li>
<li>Sets the object's <code>.constructor</code> reference to the function you called <code>new</code> with.</li>
</ol>
<pre><code>const tootsie_roll = new Food('Tootsie Roll', 0, 26, 0);

Object.getPrototypeOf(tootsie_roll) === Food.prototype; // true
tootsie_roll.constructor === Food; // true</code></pre>
<p>This is what lets us do slick stuff like this:</p>
<pre><code>"use strict";

Food.prototype.cook = function cook () {
    console.log(`${this.name} is cooking!`);
};

const dinner = new Food('Lamb Chops', 52, 8, 32);
dinner.cook(); // 'Lamb Chops are cooking!'</code></pre>
<h3>Setting the Prototype Explicitly with <code>Object.create</code></h3>
<p>Finally, we can set an object's prototype reference <em>manually</em>, using a utility called <code>Object.create</code>.</p>
<pre><code>"use strict";

const foo = {
    speak () {
    console.log('Foo!');
    }
};

const bar = Object.create(foo);

bar.speak(); // 'Foo!'
Object.getPrototypeOf(bar) === foo; // true</code></pre>
<p>Remember the four things that JavaScript does under the hood when you call a function with <code>new</code>? <code>Object.create</code> does all but the third step:</p>
<ol>
<li>Create a new object;</li>
<li>Set its prototype reference; and</li>
<li>Return the new object.</li>
</ol>
<p><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create" target="_blank">You can see this yourself if you take a look at the polyfill</a>.</p>
<h3>Emulating <code>class</code> Behavior</h3>
<p>Using prototypes directly, emulating class-oriented behavior required a bit of manual acrobatics.</p>
<pre><code>"use strict";

function Food (name, protein, carbs, fat) {
    this.name    = name;
    this.protein = protein;
    this.carbs    = carbs;
    this.fat          = fat;
}

Food.prototype.toString = function () {
    return `${this.name} | ${this.protein}g P :: ${this.carbs}g C :: ${this.fat}g F`;
};

function FatFreeFood (name, protein, carbs) {
    Food.call(this, name, protein, carbs, 0);
}

// Setting up "subclass" relationships
// =====================
// LINE A :: Using Object.create to manually set FatFreeFood's "parent".
FatFreeFood.prototype = Object.create(Food.prototype);

// LINE B :: Manually (re)setting constructor reference (!)
Object.defineProperty(FatFreeFood.constructor, "constructor", {
    enumerable : false,
    writeable      : true,
    value             : FatFreeFood
});</code></pre>
<p>At Line A, we have to set <code>FatFreeFood.prototype</code> equal to a new object, whose prototype reference is to <code>Food.prototype</code>. If we fail to do this, our "child classes" won't have access to "superclass" methods. </p>
<p>Unfortunately, this results in the rather bizarre behavior that <code>FatFreeFood.constructor</code> is <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function" target="_blank">Function</a> . . . Not <code>FatFreeFood</code>. So, to keep everything sane, we have to manually set <code>FatFreeFood.constructor</code> by hand at Line B.</p>
<p>Sparing developers from the noise and unwieldliness of emulating class behavior with prototypes is one of the motives for the <code>class</code> keyword. It <em>does</em> provide a solution to the most common gotchas of prototype syntax.</p>
<p>Now that we've seen so much of JavaScript's prototype mechanics, it should be easier to appreciate just <em>how</em> much easier it can make things! </p>
<h2 id="a-closer-look-at-methods">
    <a href="#toc-a-closer-look-at-methods" target="_blank">
      #
      A Closer Look at Methods
    </a> 
  </h2>
<p>Now that we've seen the essentials of JavaScript's prototype system, we'll wrap up by taking a closer look at three kinds of methods classes support, and a special case of the last sort:</p>
<ul>
<li>Constructors;</li>
<li>Static methods; </li>
<li>Prototype methods; and</li>
<li>"Symbol methods", a special case of <em>prototype methods</em></li>
</ul>
<p>I didn't come up with these groups -- credit goes to Dr Rauschmayer for identifying them in <a href="http://exploringjs.com/es6/ch_classes.html" target="_blank">Exploring ES6</a>.</p>
<h3>Class Constructors</h3>
<p>A class's <code>constructor</code> function is where you'll focus your initialization logic. The <code>constructor</code> is special in a few ways:</p>
<ol>
<li>It's the only method of a class from which you can make a superconstructor call;</li>
<li>It handles all the dirty work of setting up the prototype chain properly; and </li>
<li>It acts as the definition of the class.</li>
</ol>
<p>Point 2 is one of the principle benefits to using <code>class</code> in JavaScript. To quote heading 15.2.3.1 of Exploring ES6:</p>
<blockquote>
<p><strong>The prototype of a subclass is the superclass.</strong></p>
</blockquote>
<p>As we've seen, setting this up manually is tedious and error-prone. That the language takes care of it all behind the scenes if we use <code>class</code> is a major boon. </p>
<p>Point 3 is interesting. In JavaScript, a class is just a function -- it's equivalent to the <code>constructor</code> method in the class.</p>
<pre><code>"use strict";

class Food {
    // Class definition is the same as before . . . 
}

typeof Food; // 'function'</code></pre>
<p>Unlike normal-functions-as-constructors, you can't call a class's constructor without the <code>new</code> keyword:</p>
<p><code>const burrito = Food('Heaven', 100, 100, 25); // TypeError</code></p>
<p>. . . Which raises another question: What happens when we call a function-as-constructor <em>without</em> new?</p>
<p>The short answer: It returns <code>undefined</code>, as does any function without an explicit return. You just have to trust your users will constructor-call your function. This is why the community has adopted the convention of only capitalizing constructor names: It's a reminder to call with <code>new</code>. </p>
<pre><code>"use strict";

function Food (name, protein, carbs, fat) {
    this.name    = name;
    this.protein = protein;
    this.carbs    = carbs;
    this.fat          = fat;
}

const fish = Food('Halibut', 26, 0, 2); // D'oh . . .
console.log(fish); // 'undefined'</code></pre>
<p>The long answer: It returns <code>undefined</code>, <em>unless</em> you manually detect that it wasn't called with <code>new</code>, and then do something about it yourself. </p>
<p>ES2015 introdues a property that makes this check trivial: <code>[new.target]</code>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new.target" target="_blank">https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new.target</a>).</p>
<p><code>new.target</code> is a property defined on all functions called with <code>new</code>, including class constructors. When you call a function with the <code>new</code> keyword, the value of <code>new.target</code> within the function body is the function itself. If the function wasn't called with <code>new</code>, its value is <code>undefined</code>.</p>
<pre><code>"use strict";

// Enforcing constructor call
function Food (name, protein, carbs, fat) {
    // Manually call 'new' if user forgets
    if (!new.target)
        return new Food(name, protein, carbs, fat); 

    this.name    = name;
    this.protein = protein;
    this.carbs    = carbs;
    this.fat          = fat;
}

const fish = Food('Halibut', 26, 0, 2); // Oops -- but, no problem!
fish; // 'Food {name: "Halibut", protein: 20, carbs: 5, fat: 0}'</code></pre>
<p>This wasn't any worse in ES5:</p>
<pre><code>"use strict";

function Food (name, protein, carbs, fat) {

    if (!(this instanceof Food))
        return new Food(name, protein, carbs, fat); 

    this.name    = name;
    this.protein = protein;
    this.carbs    = carbs;
    this.fat          = fat;
}</code></pre>
<p>The <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new.target" target="_blank">MDN documentation</a> has more details on <code>new.target</code>, and the <a href="https://tc39.github.io/ecma262/#sec-built-in-function-objects" target="_blank">spec is the definitive reference</a> for the truly curious. The descriptions of [[Construct]] are particularly illuminating.</p>
<h3>Static Methods</h3>
<p><em>Static methods</em> are methods on the constructor function itself, which are <em>not</em> available on instances of the class. You define them by using the <code>static</code> keyword.</p>
<pre><code>"use strict";

class Food {
     // Class definition is the same as before . . . 

     // Adding a static method
     static describe () {
       console.log('"Food" is a data type for storing macronutrient information.');
      }
}

Food.describe(); // '"Food" is a data type for storing macronutrient information.'</code></pre>
<p>Static methods are analogous to attaching properties directly to old-school functions-as-constructors:</p>
<pre><code>"use strict";

function Food (name, protein, carbs, fat) {
    Food.count += 1;

    this.name    = name;
    this.protein = protein;
    this.carbs    = carbs;
    this.fat          = fat;
}

Food.count = 0;
Food.describe = function count () {
       console.log(`You've created ${Food.count} food(s).`);
};

const dummy = new Food();
Food.describe(); // "You've created 1 food."</code></pre>
<h3>Prototype Methods</h3>
<p>Any method that isn't a constructor or a static method is <em>prototype method</em>. The name comes from the fact that we used to achieve this functionality by attaching functions to the <code>.prototype</code> of functions-as-constructors:</p>
<pre><code>"use strict";

// Using ES6:
class Food {

    constructor (name, protein, carbs, fat) {
        this.name = name;
        this.protein = protein;
        this.carbs = carbs;
        this.fat = fat;
    }

    toString () {  
    return `${this.name} | ${this.protein}g P :: ${this.carbs}g C :: ${this.fat}g F`; 
    }

    print () {  
    console.log( this.toString() );  
    }
}

// In ES5:
function Food  (name, protein, carbs, fat) {
    this.name = name;
    this.protein = protein;
    this.carbs = carbs;
    this.fat = fat;
}

// The name "prototype methods" presumably comes from the fact that we 
//    used to attach such methods to the '.prototype' old-school functions-as-constructors.
Food.prototype.toString = function toString () {
    return `${this.name} | ${this.protein}g P :: ${this.carbs}g C :: ${this.fat}g F`; 
};

Food.prototype.print = function print () {
    console.log( this.toString() ); 
};</code></pre>
<p>To be clear, it's perfectly fine to use generators in method definitions, as well:</p>
<pre><code>"use strict";

class Range {

  constructor(from, to) {
    this.from = from;
    this.to   = to;
  }

  * generate () {
    let counter = this.from,
        to      = this.to;

    while (counter &lt; to) {
      if (counter == to)
        return counter++;
      else
        yield counter++;
    }
  }
}

const range = new Range(0, 3);
const gen = range.generate();
for (let val of range.generate()) {
  console.log(`Generator value is: ${ val }. `);
  //  Prints:
  //    Generator value is: 0.
  //    Generator value is: 1.
  //    Generator value is: 2.
}</code></pre>
<h3>Symbol Methods</h3>
<p>Finally, there are the <em>symbol methods</em>. These are functions whose names are <code>Symbol</code> values, and which the JavaScript engine recognizes and uses when you use certain built-in constructs with your custom objects.</p>
<p>The <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol" target="_blank">MDN docs</a> provide a succinct overview of what Symbols are in general:</p>
<blockquote>
<p>A symbol is a unique and immutable data type and may be used as an identifier for object properties.</p>
</blockquote>
<p>Creating a new symbol provides you with a value that is guaranteed to be unique within your program. This is what makes it useful for naming object properties: You're guaranteed never to accidentally shadow anything. Symbol-valued keys also aren't innumerable, so they're largely invisible to the outside world (<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect/ownKeys" target="_blank">but not completely</a>).</p>
<pre><code>"use strict";

const secureObject = {
    // This key is guaranteed to be unique.
    [new Symbol("name")] : 'Dr. Secure A. F.'
};

console.log( Object.getKeys(superSecureObject) ); // [] -- The symbol property is pretty hard to get at . . .  
console.log( Reflect.ownKeys(secureObject) ); // [Symbol("name")] -- . . . But, not /truly/ hidden.</code></pre>
<p>More interestingly for us, they give us a way to tell the JavaScript engine to use certain functions for special purposes.</p>
<p>The so-called <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol" target="_blank">Well-known Symbols</a> are special object keys that identify functions the JavaScript engine invokes when you use certain built-in constructs with custom objects.</p>
<p>This is a bit exotic for JavaScript, so let's see an example:</p>
<pre><code>"use strict";

// Extending Array lets us use 'length' in an intuitive way,
//   and also gives us access to built-in array methods, like 
//   map, filter, reduce, push, pop, etc.
class FoodSet extends Array {

    // ...foods collects arbitrary number of arguments into an array
    //   https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator
    constructor(...foods) {
        super();
        this.foods = [];
        foods.forEach((food) =&gt; this.foods.push(food))
    }

     // Custom iterator behavior. This isn't very *useful* iterator behavior, mind you, but it's a fine example.
     // The asterisk *must* precede the name of the key.
     * [Symbol.iterator] () {
        let position = 0;
        while (position &lt; this.foods.length) {
          if (position === this.foods.length) {
              return "Done!"
          } else {
              yield `${this.foods[ position++ ]} is the food item at position ${position}`;
          }
         }
     }

      // Return an object of type Array, rather than type FoodSet, when users
      //   use built-in array methods. This makes our FoodSet interoperable
      //   with code expecting an array.
      static get [Symbol.species] () {
          return Array;
      }
}

const foodset = new FoodSet(new Food('Fish', 26, 0, 16), new Food('Hamburger', 26, 48, 24));

// When you use for . . . of with a FoodSet, JavaScript will iterate using the function you 
//    assoiated with the key [Symbol.iterator].
for (let food of foodset) {
  // Prints all of our foods
  console.log( food );
}

// JavaScript creates and returns a new object when you `filter` on an array, 
//    which it creates using the default constructor of the object you execute `filter` on.
//
//    Since most code would expect filter to return an Array, we can tell JavaScript
//       to use the Array constructor when implicitly creating a new instance by 
//       overriding [Symbol.species].
const healthy_foods = foodset.filter((food) =&gt; food.name !== 'Hamburger');

console.log( healthy_foods instanceof FoodSet ); // 
console.log( healthy_foods instanceof Array );</code></pre>
<p>When you use a <code>for...of</code> loop on an object, JavaScript will try to execute the object's <em>iterator</em> function, which is the function associated with the key, <code>Symbol.iterator</code>. If you provide your own definition, JavaScript will use that. If you don't, it'll use the default implementation, if there is one; or do nothing, if there isn't.</p>
<p><code>Symbol.species</code> is a bit more exotic. In a custom class, the default <code>Symbol.species</code> function is the constructor for your class. When you subclass built-in collections, like <code>Array</code> or <code>Set</code>, however, you'll often want to be able to use your subclass wherever you could use an instance of the parent class.</p>
<p>Returning instances of the parent class from methods on the class <em>instead</em> of instances of the derived class gets us closer to ensuring full interoperability of a subclass with more general code. This is <code>Symbol.species</code> allows.</p>
<p>Don't sweat it if this bit doesn't make much sense. Using symbols this way -- or at all -- is still a niche case, and the point of these examples is to demonstrate:</p>
<ol>
<li>That you <em>can</em> use certain built-in JavaScript constructs with custom classes; and</li>
<li><em>How</em> you achieve that, in two common cases.</li>
</ol>
<h2 id="conclusion">
    <a href="#toc-conclusion" target="_blank">
      #
      Conclusion
    </a> 
  </h2>
<p>ES2015's <code>class</code> keyword does <em>not</em> bring us "true classes", a là Java or SmallTalk. Rather, it simply provides a more convenient syntax for creating objects related via prototype linkage. Under the hood, there's nothing new here. </p>
<p>I covered enough of JavaScript's prototype mechanism for our discussion, but there's quite a bit more to say. Read Kyle Simpson's <a href="https://github.com/getify/You-Dont-Know-JS/tree/master/this%20%26%20object%20prototypes" target="_blank">this & Object Prototypes</a> for fuller coverage on that front. <a href="https://github.com/getify/You-Dont-Know-JS/blob/master/this%20&%20object%20prototypes/apA.md" target="_blank">Appendix A</a> is particularly relevant.</p>
<p>For the nitty-gritty on ES2015 classes, Dr Rauschmayer's <a href="http://exploringjs.com/es6/ch_classes.html" target="_blank">Exploring ES6: Classes</a> should be your go-to resource. It was the inspiration for much of what I've written here.</p>
<p>Finally, if you've got questions, drop a line in the comments, or <a href="https://twitter.com/PelekeS" target="_blank">hit me on Twitter</a>. I'll do my best to get back to everyone directly.</p>
<p>What do you think about <code>class</code>? Love it, hate it, no strong feelings? It seems like everyone's got an opinion -- let us know yours below!</p>
<hr />
<p><em>Note: This is part 2 of the Better JavaScript series. You can see parts 1, 2, and 3 here:</em></p>


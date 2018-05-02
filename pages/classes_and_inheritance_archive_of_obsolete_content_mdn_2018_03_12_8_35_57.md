<a href="https://developer.mozilla.org/en-US/docs/Archive/Add-ons/Add-on_SDK/Guides/Contributor_s_Guide/Classes_and_Inheritance">https://developer.mozilla.org/en-US/docs/Archive/Add-ons/Add-on_SDK/Guides/Contributor_s_Guide/Classes_and_Inheritance</a><div id="articleHeader"><h1>Archive of obsolete content</h1></div>
                
                  
                    <div><p>Add-ons using the techniques described in this document are considered a legacy technology in Firefox. Don't use these techniques to develop new add-ons. Use <a href="/en-US/Add-ons/WebExtensions" target="_blank">WebExtensions</a> instead. If you maintain an add-on which uses the techniques described here, consider migrating it to use WebExtensions.</p><p><strong>Starting from <a href="https://wiki.mozilla.org/RapidRelease/Calendar" target="_blank">Firefox 53</a>, no new legacy add-ons will be accepted on addons.mozilla.org (AMO) for desktop Firefox and Firefox for Android.</strong></p><p><strong>Starting from <a href="https://wiki.mozilla.org/RapidRelease/Calendar" target="_blank">Firefox 57</a>, only extensions developed using WebExtensions APIs will be supported on Desktop Firefox and Firefox for Android. </strong></p><p>Even before Firefox 57, changes coming up in the Firefox platform will break many legacy extensions. These changes include multiprocess Firefox (e10s), sandboxing, and multiple content processes. Legacy extensions that are affected by these changes should migrate to use WebExtensions APIs if they can. See the <a href="https://blog.mozilla.org/addons/2017/02/16/the-road-to-firefox-57-compatibility-milestones/" target="_blank">"Compatibility Milestones" document</a> for more information.</p><p>A wiki page containing <a href="https://wiki.mozilla.org/Add-ons/developer/communication" target="_blank">resources, migration paths, office hours, and more</a>, is available to help developers transition to the new technologies.</p></div>

<p>A class is a blueprint from which individual objects are created. These individual objects are the instances of the class. Each class defines one or more members, which are initialized to a given value when the class is instantiated. Data members are properties that allow each instance to have their own state, whereas member functions are properties that allow instances to have behavior. Inheritance allows classes to inherit state and behavior from an existing classes, known as the base class. Unlike languages like C++ and Java, JavaScript does not have native support for classical inheritance. Instead, it uses something called prototypal inheritance. As it turns out, it is possible to emulate classical inheritance using prototypal inheritance, but not without writing a significant amount of boilerplate code.</p>

<p>Classes in JavaScript are defined using constructor functions. Each constructor function has an associated object, known as its prototype, which is shared between all instances of that class. We will show how to define classes using constructors, and how to use prototypes to efficiently define member functions on each instance. Classical inheritance can be implemented in JavaScript using constructors and prototypes. We will show how to make inheritance work correctly with respect to constructors, prototypes, and the instanceof operator, and how to override methods in subclasses. The SDK uses a special constructor internally, known as <code>Class</code>, to create constructors that behave properly with respect to inheritance. The last section shows how to work with the <code>Class</code> constructor. It is possible to read this section on its own. However, to fully appreciate how <code>Class</code> works, and the problem it is supposed to solve, it is recommended that you read the entire article.</p>

<h2 id="Constructors">Constructors</h2>

<p>Before the ECMASCript 6 standard, a JavaScript class was defined by creating a constructor function for that class. To illustrate this, let's define a simple constructor for a class <code>Shape</code>:</p>

<pre><code>function Shape(x, y) {
    this.x = x;
    this.y = y;
}
</code></pre>

<p>We can now use this constructor to create instances of <code>Shape</code>:</p>

<pre><code>let shape = new Shape(2, 3);
shape instanceof Shape; // =&gt; true
shape.x; // =&gt; 2
shape.y; // =&gt; 3
</code></pre>

<p>The keyword new tells JavaScript that we are performing a constructor call. Constructor calls differ from ordinary function calls in that JavaScript automatically creates a new object and binds it to the keyword this for the duration of the call. Moreover, if the constructor does not return a value, the result of the call defaults to the value of this. Constructors are just ordinary functions, however, so it is perfectly legal to perform ordinary function calls on them. In fact, some people (including the Add-on SDK team) prefer to use constructors this way. However, since the value of this is undefined for ordinary function calls, we need to add some boilerplate code to convert them to constructor calls:</p>

<pre><code>function Shape(x, y) {
    if (!this)
        return new Shape(x, y);
    this.x = x;
    this.y = y;
}
</code></pre>

<h2 id="Prototypes">Prototypes</h2>

<p>Every object has an implicit property, known as its prototype. When JavaScript looks for a property, it first looks for it in the object itself. If it cannot find the property there, it looks for it in the object's prototype. If the property is found on the prototype, the lookup succeeds, and JavaScript pretends that it found the property on the original object. Every function has an explicit property, known as <code>prototype</code>. When a function is used in a constructor call, JavaScript makes the value of this property the prototype of the newly created object:</p>

<pre><code>let shape = Shape(2, 3);
Object.getPrototypeOf(shape) == Shape.prototype; // =&gt; true
</code></pre>

<p>All instances of a class have the same prototype. This makes the prototype the perfect place to define properties that are shared between instances of the class. To illustrate this, let's add a member function to the class <code>Shape</code>:</p>

<pre><code>Shape.prototype.draw = function () {
    throw Error("not yet implemented");
}
let shape = Shape(2, 3);
Shape.draw(); // =&gt; Error: not yet implemented
</code></pre>

<h2 id="Inheritance_and_Constructors">Inheritance and Constructors</h2>

<p>Suppose we want to create a new class, <code>Circle</code>, and inherit it from <code>Shape</code>. Since every <code>Circle</code> is also a <code>Shape</code>, the constructor for <code>Shape</code> must be called every time we call the constructor for <code>Circle</code>. Since JavaScript does not have native support for inheritance, it doesn't do this automatically. Instead, we need to call the constructor for <code>Shape</code> explicitly. The resulting constructor looks as follows:</p>

<pre><code>function Circle(x, y, radius) {
   if (!this)
       return new Circle(x, y, radius);
   Shape.call(this, x, y);
   this.radius = radius;
}
</code></pre>

<p>Note that the constructor for <code>Shape</code> is called as an ordinary function, and reuses the object created for the constructor call to <code>Circle</code>. Had we used a constructor call instead, the constructor for <code>Shape</code> would have been applied to a different object than the constructor for <code>Circle</code>. We can now use the above constructor to create instances of the class <code>Circle</code>:</p>

<pre><code>let circle = Circle(2, 3, 5);
circle instanceof Circle; // =&gt; true
circle.x; // =&gt; 2
circle.y; // =&gt; 3
circle.radius; // =&gt; 5
</code></pre>

<h2 id="Inheritance_and_Prototypes">Inheritance and Prototypes</h2>

<p>There is a problem with the definition of <code>Circle</code> in the previous section that we have glossed over thus far. Consider the following:</p>

<pre><code>let circle = Circle(2, 3, 5);
circle.draw(); // =&gt; TypeError: circle.draw is not a function
</code></pre>

<p>This is not quite right. The method <code>draw</code> is defined on instances of <code>Shape</code>, so we definitely want it to be defined on instances of <code>Circle</code>. The problem is that <code>draw</code> is defined on the prototype of <code>Shape</code>, but not on the prototype of <code>Circle</code>. We could of course copy every property from the prototype of <code>Shape</code> over to the prototype of <code>Circle</code>, but this is needlessly inefficient. Instead, we use a clever trick, based on the observation that prototypes are ordinary objects. Since prototypes are objects, they have a prototype as well. We can thus override the prototype of <code>Circle</code> with an object which prototype is the prototype of <code>Shape</code>.</p>

<pre><code>Circle.prototype = Object.create(Shape.prototype);
</code></pre>

<p>Now when JavaScript looks for the method draw on an instance of Circle, it first looks for it on the object itself. When it cannot find the property there, it looks for it on the prototype of <code>Circle</code>. When it cannot find the property there either, it looks for it on <code>Shape</code>, at which point the lookup succeeds. The resulting behavior is what we were aiming for.</p>

<h2 id="Inheritance_and_Instanceof">Inheritance and Instanceof</h2>

<p>The single line of code we added in the previous section solved the problem with prototypes, but introduced a new problem with the <strong>instanceof</strong> operator. Consider the following:</p>

<pre><code>let circle = Circle(2, 3, 5);
circle instanceof Shape; // =&gt; false
</code></pre>

<p>Since instances of <code>Circle</code> inherit from <code>Shape</code>, we definitely want the result of this expression to be true. To understand why it is not, we need to understand how <strong>instanceof</strong> works. Every prototype has a <code>constructor</code> property, which is a reference to the constructor for objects with this prototype. In other words:</p>

<pre><code>Circle.prototype.constructor == Circle // =&gt; true
</code></pre>

<p>The <strong>instanceof</strong> operator compares the <code>constructor</code> property of the prototype of the left hand side with that of the right hand side, and returns true if they are equal. Otherwise, it repeats the comparison for the prototype of the right hand side, and so on, until either it returns <strong>true</strong>, or the prototype becomes <strong>null</strong>, in which case it returns <strong>false</strong>. The problem is that when we overrode the prototype of <code>Circle</code> with an object whose prototype is the prototype of <code>Shape</code>, we didn't correctly set its <code>constructor</code> property. This property is set automatically for the <code>prototype</code> property of a constructor, but not for objects created with <code>Object.create</code>. The <code>constructor</code> property is supposed to be non-configurable, non-enumberable, and non-writable, so the correct way to define it is as follows:</p>

<pre><code>Circle.prototype = Object.create(Shape.prototype, {
    constructor: {
        value: Circle
    }
});
</code></pre>

<h2 id="Overriding_Methods">Overriding Methods</h2>

<p>As a final example, we show how to override the stub implementation of the method <code>draw</code> in <code>Shape</code> with a more specialized one in <code>Circle</code>. Recall that JavaScript returns the first property it finds when walking the prototype chain of an object from the bottom up. Consequently, overriding a method is as simple as providing a new definition on the prototype of the subclass:</p>

<pre><code>Circle.prototype.draw = function (ctx) {
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.radius,
            0, 2 * Math.PI, false);
    ctx.fill();
};
</code></pre>

<p>With this definition in place, we get:</p>

<pre><code>let shape = Shape(2, 3);
shape.draw(); // Error: not yet implemented 
let circle = Circle(2, 3, 5);
circle.draw(); // TypeError: ctx is not defined
</code></pre>

<p>which is the behavior we were aiming for.</p>

<h2 id="Classes_in_the_Add-on_SDK">Classes in the Add-on SDK</h2>

<p>We have shown how to emulate classical inheritance in JavaScript using constructors and prototypes. However, as we have seen, this takes a significant amount of boilerplate code. The Add-on SDK team consists of highly trained professionals, but they are also lazy: that is why the SDK contains a helper function that handles this boilerplate code for us. It is defined in the module “core/heritage”:</p>

<pre><code>const { Class } = require('sdk/core/heritage');
</code></pre>

<p>The function <code>Class</code> is a meta-constructor: it creates constructors that behave properly with respect to inheritance. It takes a single argument, which is an object which properties will be defined on the prototype of the resulting constructor. The semantics of <code>Class</code> are based on what we've learned earlier. For instance, to define a constructor for a class <code>Shape</code> in terms of <code>Class</code>, we can write:</p>

<pre><code>let Shape = Class({
    initialize: function (x, y) {
        this.x = x;
        this.y = y;
    },
    draw: function () {
        throw new Error("not yet implemented");
    }
});
</code></pre>

<p>The property <code>initialize</code> is special. When it is present, the call to the constructor is forwarded to it, as are any arguments passed to it (including the this object). In effect, initialize specifies the body of the constructor. Note that the constructors created with <code>Class</code> automatically check whether they are called as constructors, so an explicit check is no longer necessary.</p>

<p>Another special property is <code>extends</code>. It specifies the base class from which this class inherits, if any. <code>Class</code> uses this information to automatically set up the prototype chain of the constructor. If the extends property is omitted, <code>Class</code> itself is used as the base class:</p>

<pre><code>var shape = new Shape(2, 3);
shape instanceof Shape; // =&gt; true
shape instanceof Class; // =&gt; true
</code></pre>

<p>To illustrate the use of the <code>extends</code> property, let's redefine the constructor for the class <code>Circle</code> in terms of <code>Class</code>:</p>

<pre><code>var Circle = Class({
    extends: Shape,
    initialize: function(x, y, radius) {
        Shape.prototype.initialize.call(this, x, y);
        this.radius = radius;
    },
    draw: function (<code>context</code>) {
        context.beginPath();
        context.arc(this.x, this.y, this.radius,
                    0, 2 * Math.PI, false);
        context.fill();
    }
});
</code></pre>

<p>Unlike the definition of <code>Circle</code> in the previous section, we no longer have to override its prototype, or set its <code>constructor</code> property. This is all handled automatically. On the other hand, the call to the constructor for <code>Shape</code> still has to be made explicitly. This is done by forwarding to the initialize method of the prototype of the base class. Note that this is always safe, even if there is no <code>initialize</code> method defined on the base class: in that case the call is forwarded to a stub implementation defined on <code>Class</code> itself.</p>

<p>The last special property we will look into is <code>implements</code>. It specifies a list of objects, which properties are to be copied to the prototype of the constructor. Note that only properties defined on the object itself are copied: properties defined on one of its prototypes are not. This allows objects to inherit from more than one class. It is not true multiple inheritance, however: no constructors are called for objects inherited via <code>implements</code>, and <strong>instanceof</strong> only works correctly for classes inherited via <code>extends</code>.</p>
                  
                
              
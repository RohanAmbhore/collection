<a href="https://stackoverflow.com/questions/17392857/benefits-of-using-object-create-for-inheritance">https://stackoverflow.com/questions/17392857/benefits-of-using-object-create-for-inheritance</a><div id="articleHeader"><h1>Benefits of using `Object.create` for inheritance</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        46
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>43</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I've been trying to wrap my head around the new <code>Object.create</code> method which was introduced in ECMAScript 5.</p>

<p>Usually when I want to use inheritance I do something like this:</p>

<pre><code>var Animal = function(name) { this.name = name; }
Animal.prototype.print = function() { console.log(this.name); }

var Dog = function() 
{ 
  return Animal.call(this, 'Dog'); 
}

Dog.prototype = new Animal();
Dog.prototype.bark = function() { console.log('bark'); }</code></pre>

<p>I just assign a newly created Animal object to Dog's prototype and everything works like a charm:</p>

<pre><code>var dog1 = new Dog();
dog1.print(); // prints 'Dog'
dog1.bark(); // prints 'bark'
dog1.name; //prints 'Dog'</code></pre>

<p>but people(without explaining) are saying that <code>Dog.prototype = new Animal();</code> is not the way inheritance works and that I should use Object.create approach:</p>

<pre><code>Dog.prototype = Object.create(Animal.prototype);</code></pre>

<p>which also works. </p>

<p>What's the benefit of using <code>Object.create</code> or am I missing something?</p>

<p><strong>UPDATE: Some say that <code>Dog.prototype = Animal.prototype;</code> can also work. So now I'm totally confused</strong></p>
    </div>
    <div>
        <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> 
    </div>
    
</div>

                
    <div>
	    <div id="comments-17392857">
                <ul>



    <li id="comment-25251484">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                If I have to guess, you'll notice the difference when expanding the Animal prototype after <code>Dog.prototype = new Animal();</code>. This expansion will not be inherited by <code>Dog</code>. Can't test that theory here though.
                    – <a href="/users/2209007/sumurai8" title="11,337 reputation" target="_blank">Sumurai8</a>
                <a href="#comment25251484_17392857" target="_blank">Jun 30 '13 at 17:19</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-25251514">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                @SimonBoudrias Unfortunately I didn't find anything useful in those questions
                    – <a href="/users/1796666/kir-ivlev" title="7,310 reputation" target="_blank">Kir Ivlev</a>
                <a href="#comment25251514_17392857" target="_blank">Jun 30 '13 at 17:21</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-25251614">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Short answer: running the <code>Animal</code> constructor may have undesired side effects.
                    – <a href="/users/27862/user123444555621" title="85,817 reputation" target="_blank">user123444555621</a>
                <a href="#comment25251614_17392857" target="_blank">Jun 30 '13 at 17:27</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-25251796">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                With <code>Dog.prototype = new Animal();</code> the prototype of dog gets all the properties of the Animal instance, also the <code>name</code> property. But with <code>Object.create(Animal.prototype);</code> the prototype gets only the properties of the prototype of <code>Animal</code>.
                    – <a href="/users/1258878/basilikum" title="7,610 reputation" target="_blank">basilikum</a>
                <a href="#comment25251796_17392857" target="_blank">Jun 30 '13 at 17:38</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-25252436">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Just for the record: here's yet another way to implement class inheritance, taken from Backbone.js: <code>var Surrogate = function(){ this.constructor = child; }; Surrogate.prototype = parent.prototype; child.prototype = new Surrogate;</code>
                    – <a href="/users/27862/user123444555621" title="85,817 reputation" target="_blank">user123444555621</a>
                <a href="#comment25252436_17392857" target="_blank">Jun 30 '13 at 18:17</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>        </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-17393153">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        104
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>In the following I assume you are only interested in why <code>Object.create</code> is preferable for setting up inheritance.</p>

<p>To understand the benefits, lets first clarify what a "class" is made of in JavaScript. You have two parts:</p>

<ol>
<li><p>The <strong>constructor</strong> function. This function contains all the logic to create an instance of the "class", i.e. instance specific code.</p></li>
<li><p>The <strong>prototype</strong> object. This is the object the instance inherits from. It contains all methods (and other properties) that should be shared among all instances.</p></li>
</ol>

<p><strong>Inheritance</strong> establishes an <em>is-a</em> relation, for example, a <code>Dog</code> <em>is</em> an <code>Animal</code>. How is this expressed in terms of constructor function and prototype object?  </p>

<p>Obviously a dog must have the same methods as an animal, that is the <code>Dog</code> <em>prototype</em> object must somehow incorporate the methods from the <code>Animal</code> <em>prototype</em> object. There are multiple ways to do this. You will often see this:</p>

<pre><code>Dog.prototype = new Animal();</code></pre>

<p>This works because an <code>Animal</code> <em>instance</em> inherits from the <code>Animal</code> <em>prototype</em> object. <strong>But</strong> it also implies that every dog inherits from <em>one</em> specific <code>Animal</code> <em>instance</em>. That seems to be a bit strange. Shouldn't instance specific code only be run in the <em>constructor</em> function? Suddenly <em>instance</em> specific code and <em>prototype</em> methods seem to be mixed.</p>

<p>We don't actually want to run <code>Animal</code> <em>instance</em> specific code at that moment, we only want all the methods from the <code>Animal</code> <em>prototype</em> object. That is what <code>Object.create</code> lets us  do:</p>

<pre><code>Dog.prototype = Object.create(Animal.prototype);</code></pre>

<p>Here we are <em>not</em> creating a new <code>Animal</code> instance, we only get the prototype methods. The <em>instance</em> specific code is executed exactly where it should be, inside the constructor:</p>

<pre><code>function Dog() { 
   Animal.call(this, 'Dog'); 
}</code></pre>

<p>The biggest advantage is that <code>Object.create</code> will <em>always</em> work. Using <code>new Animal()</code> only works if the constructor does not expect any arguments. Imagine if the constructor looked like this:</p>

<pre><code>function Animal(name) { 
    this.name = name.toLowerCase();
}</code></pre>

<p>You always have to pass a string to <code>Animal</code>, otherwise you will get an error. What will you pass when you do <code>Dog.prototype = new Animal(??);</code>? It doesn't actually matter which string you pass, as long as pass <em>something</em>, which hopefully shows you that this is bad design.</p>

<hr />

<blockquote>
  <p>Some say that <code>Dog.prototype = Animal.prototype;</code> can also work. So now I'm totally confused</p>
</blockquote>

<p>Everything that "adds" the properties from <code>Animal.prototype</code> to <code>Dog.prototype</code> will "work". But the solutions are of different quality. In this case here you will have the problem that any method you add to <code>Dog.prototype</code> will also be added to <code>Animal.prototype</code>.</p>

<p>Example:</p>

<pre><code>Dog.prototype.bark = function() {
    alert('bark');
};</code></pre>

<p>Since <code>Dog.prototype === Animal.prototype</code>, all <code>Animal</code> instances have a method <code>bark</code> now, which is certainly not what you want. </p>

<p><code>Object.create</code> (and even <code>new Animal</code>) add one level of indirection to the inheritance by creating a new object which inherits from <code>Animal.prototype</code> and that new object becomes <code>Dog.prototype</code>.</p>

<hr />

<p><strong>Inheritance in ES6</strong></p>

<p>ES6 introduces a new syntax to create constructor functions and prototype methods, which looks like this:</p>

<pre><code>class Dog extends Animal {

  bark() {
    alert('bark');
  }

}</code></pre>

<p>This is more convenient than what I explained above, but as it turns out, <code>extends</code> also uses an internal equivalent to <code>Object.create</code> to setup inheritance. See steps 2 and 3 in the <a href="https://people.mozilla.org/~jorendorff/es6-draft.html#sec-runtime-semantics-classdefinitionevaluation" target="_blank">ES6 draft</a>.<br />
Which means that using <code>Object.create(SuperClass.prototype)</code> is the "more correct" approach in ES5.</p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-17393153">
                <ul>



    <li id="comment-25252168">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                +1 for "only works if the constructor does not expect any arguments"
                    – <a href="/users/27862/user123444555621" title="85,817 reputation" target="_blank">user123444555621</a>
                <a href="#comment25252168_17393153" target="_blank">Jun 30 '13 at 18:00</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-44692397">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Good explanation - nice job. But.  If Animal really needs something set in the constructor, one could argue whether allowing Object.create to creat a half-baked Animal is a plus or a minus.  Personally I feel it is a minus.  I am still unpersuaded that Object.create() is so wonderful.
                    – <a href="/users/949300/user949300" title="11,950 reputation" target="_blank">user949300</a>
                <a href="#comment44692397_17393153" target="_blank">Jan 26 '15 at 23:17</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-59331728">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                I usually just pass and options variable to my constructor that then gets extended. Then if I wanted to <code>new Animal()</code> but with options it would look like  <code>new Animal({ species: 'dog', sound: 'bark' })</code>  With this however, if you're not using jQuery, you'd need to create you own extend function.
                    – <a href="/users/293153/banning" title="1,962 reputation" target="_blank">Banning</a>
                <a href="#comment59331728_17393153" target="_blank">Mar 6 '16 at 20:56</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-85151051">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Is it a good practice for us new JavaScript developers to continue to dive deep into creating and sharing object prototypes with Object.Create in ES6?  Especially if we want to be true to the behavior delegation of objects? Felix what is your opinion?
                    – <a href="/users/957186/blackhawk" title="2,500 reputation" target="_blank">blackhawk</a>
                <a href="#comment85151051_17393153" target="_blank">Mar 2 at 15:55</a>
                        
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-17393115">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        9
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>First, running the <code>Animal</code> constructor may have undesired side effects. Consider this:</p>

<pre><code>var Animal = function(name) {
    this.name = name;
    Animal.instances.push(this);
};
Animal.instances = [];</code></pre>

<p>This version would keep track of all instances that have been created. You don't want your <code>Dog.prototype</code> to be recorded there.</p>

<p>Second, <code>Dog.prototype = Animal.prototype</code> is a bad idea, since that would mean that <code>bark</code> would become a method of <code>Animal</code>.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jun 30 '13 at 17:42
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-17393115">
                <ul>



    <li id="comment-44695403">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                If that Animal constructor has undesired side-effects, that is a problem with the design or the code, not the technique of inheritance.
                    – <a href="/users/949300/user949300" title="11,950 reputation" target="_blank">user949300</a>
                <a href="#comment44695403_17393115" target="_blank">Jan 27 '15 at 2:09</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-17393390">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I'm trying to illustrate the difference a little bit:</p>

<p>Here is what basically happens when you write <code>new Animal()</code>:</p>

<pre><code>    //creating a new object
    var res = {};

    //setting the internal [[prototype]] property to the prototype of Animal
    if (typeof Animal.prototype === "object" && Animal.prototype !== null) {
        res.__proto__ = Animal.prototype;
    }

    //calling Animal with the new created object as this
    var ret = Animal.apply(res, arguments);

    //returning the result of the Animal call if it is an object
    if (typeof ret === "object" && ret !== null) {
        return ret;
    }

    //otherise return the new created object
    return res;</code></pre>

<p>And here is what basically happens with <code>Object.create</code>:</p>

<pre><code>    //creating a new object
    var res = {};

    //setting the internal [[prototype]] property to the prototype of Animal
    if (typeof Animal.prototype !== "object") {
        throw "....";
    }
    res.__proto__ = Animal.prototype;

    //return the new created object
    return res;</code></pre>

<p>So it does the same but it doesn't call the <code>Animal</code> function and it also always returns the new created object.
In your case you end up with two different objects. With the first method you get:</p>

<pre><code>Dog.prototype = {
    name: undefined,
    __proto__: Animal.prototype
};</code></pre>

<p>and with the second method you get:</p>

<pre><code>Dog.prototype = {
    __proto__: Animal.prototype
};</code></pre>

<p>You don't really need to have the <code>name</code> property in your prototype, because you already assigning it to your <code>Dog</code> instance with <code>Animal.call(this, 'Dog');</code>.</p>

<p>Your primary goal is to let your <code>Dog</code> instance access all the properties of the <code>Animal</code> prototype, which is achieved by both methods. The first method however does some extra stuff that is not really needed in your case or can even cause unwanted results as Pumbaa80 mentioned.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jun 30 '13 at 18:13
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-21461586">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        4
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Let's understand it with code only;</p>

<p><strong>A.prototype = B.prototype;</strong></p>

<pre><code>function B() {console.log("I am B");this.b1= 30;}
    B.prototype.b2 = 40;

    function A() {console.log("I am A");this.a1= 10;}
    A.prototype.a2 = 20;

    A.prototype = B.prototype;

    A.prototype.constructor = A; 

    var a = new A;
    var b = new B;

    console.log(a);//A {a1: 10, b2: 40}
    console.log(b);//B {b1: 30, b2: 40}

    console.log(A.prototype.constructor);//A
    console.log(B.prototype.constructor);//A
    console.log(A.prototype);//A {b2: 40}
    console.log(B.prototype);//A {b2: 40}
    console.log(a.constructor === A); //true
    console.log(b.constructor === A); //true

console.log(a.a2);//undefined</code></pre>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/CrjAX.jpg" alt="enter image description here" /></div></p>

<p><strong>A.prototype = Object.create(B.prototype);</strong></p>

<pre><code>function B() {console.log("I am B");this.b1= 30;}
B.prototype.b2 = 40;

function A() {console.log("I am A");this.a1= 10;}
A.prototype.a2 = 20;

A.prototype = Object.create(B.prototype);

A.prototype.constructor = A; 

var a = new A;
var b = new B;

console.log(a);//A {a1: 10, constructor: function, b2: 40}
console.log(b);//B {b1: 30, b2: 40} 

console.log(A.prototype.constructor);//A
console.log(B.prototype.constructor);//B
console.log(A.prototype);//A {constructor: function, b2: 40}
console.log(B.prototype);//B {b2: 40}
console.log(a.constructor === A); //true
console.log(b.constructor === B); //true
console.log(a.a2);//undefined</code></pre>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/eKqV4.png" alt="enter image description here" /></div></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 30 '14 at 16:10
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    




<div id="post-editor">

    <div> 
        <div>
            <div id="mdhelp">
    <ul id="mdhelp-tabs">
        <li>Links</li>
        <li>Images</li>
        <li>Styling/Headers</li>
        <li>Lists</li>
        <li>Blockquotes</li>
        
        
        <li><a href="/editing-help" target="_blank">advanced help »</a></li>
    </ul>
    
    

    
    
    

    

    

    

    
</div>
            
        </div>
    </div>

    
    

    

    


    
    
    



</div>

                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
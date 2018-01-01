<a href="https://stackoverflow.com/questions/572897/how-does-javascript-prototype-work">https://stackoverflow.com/questions/572897/how-does-javascript-prototype-work</a><div id="articleHeader"><h1>How does JavaScript .prototype work?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        1751
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>1098</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I'm not that into dynamic programming languages, but I've written my fair share of JavaScript code. I never really got my head around this prototype-based programming, does any one know how this works? </p>

<pre><code>var obj = new Object(); // not a functional object
obj.prototype.test = function() { alert('Hello?'); }; // this is wrong!

function MyObject() {} // a first class functional object
MyObject.prototype.test = function() { alert('OK'); } // OK</code></pre>

<p>I remember a lot discussion I had with people a while back (I'm not exactly sure what I'm doing) but as I understand it, there's no concept of a class. It's just an object, and instances of those objects are clones of the original, right?</p>

<p>But what is the exact purpose of this <code>.prototype</code> property in JavaScript? How does it relate to instantiating objects?</p>

<hr />



<p>These <a href="http://ejohn.org/apps/learn/#64" target="_blank">slides</a> really helped a lot to understand this topic.</p>
    </div>
    
    
</div>
</td>
        </tr>
                    <tr>
            <td colspan="2">
                <div>
        <h2>                    <b>protected</b> by <a href="/users/1026459/travis-j" target="_blank">Travis J</a> Jul 12 '13 at 22:29
</h2>
        <p>
This question is protected to prevent "thanks!", "me too!", or spam answers by new users. 
To answer it, you must have earned at least 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).</p>
    </div>
            </td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-572897">
		        <table>
                    <tbody>



    <tr id="comment-25311276">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                69
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                John Resig has a few slides on function prototypes that were helpful to me when looking into the subject (you can also make changes to the code and see what happens...) <a href="http://ejohn.org/apps/learn/#64" target="_blank">http://ejohn.org/apps/learn/#64</a>
                    – <a href="/users/45859/john-foster" title="7,387 reputation" target="_blank">John Foster</a>
                <a href="#comment25311276_572897" target="_blank">Feb 21 '09 at 12:56</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-25311277">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Great reference material, for purposes of keeping this question informative perhaps place some of the comments from John's site on your answer in case his site is changes in a way that your link is no longer available. Either way +1, helped me.
                    – <a href="/users/364114/chris" title="6,166 reputation" target="_blank">Chris</a>
                <a href="#comment25311277_572897" target="_blank">May 27 '11 at 23:14</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-14671662">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                89
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                +1 for your link to <a href="http://ejohn.org/apps/learn/#64" target="_blank">John Resig's JavaScript Ninja slide #64</a>. Starting from there was really helpful, and I feel like I understand prototypes correctly.
                    – <a href="/users/102704/a-paid-nerd" title="17,379 reputation" target="_blank">a paid nerd</a>
                <a href="#comment14671662_572897" target="_blank">Jun 24 '12 at 21:02</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-21003249">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Do we really need a functional object for applying prototype? if yes than why ?
                    – <a href="/users/1768910/anshul" title="5,163 reputation" target="_blank">Anshul</a>
                <a href="#comment21003249_572897" target="_blank">Feb 19 '13 at 15:40</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-22683902">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                5
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-572897">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>6</b> more comments</a>
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-572996">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        875
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>Every JavaScript object has an internal property called <em>[[Prototype]]</em>. If you look up a property via <code>obj.propName</code> or <code>obj['propName']</code> and the object does not have such a property - which can be checked via <code>obj.hasOwnProperty('propName')</code> - the runtime looks up the property in the object referenced by [[Prototype]] instead. If the prototype-object also doesn't have such a property, its prototype is checked in turn, thus walking the original object's <em>prototype-chain</em> until a match is found or its end is reached.</p>

<p>Some JavaScript implementations allow direct access to the [[Prototype]] property, eg via a non-standard property named <code>__proto__</code>. In general, it's only possible to set an object's prototype during object creation: If you create a new object via <code>new Func()</code>, the object's [[Prototype]] property will be set to the object referenced by <code>Func.prototype</code>.</p>

<p>This allows to simulate classes in JavaScript, although JavaScript's inheritance system is - as we have seen - prototypical, and not class-based:</p>

<p>Just think of constructor functions as classes and the properties of the prototype (ie of the object referenced by the constructor function's <code>prototype</code> property) as shared members, ie members which are the same for each instance. In class-based systems, methods are implemented the same way for each instance, so methods are normally added to the prototype, whereas an object's fields are instance-specific and therefore added to the object itself during construction.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-572996">
		        <table>
                    <tbody>



    <tr id="comment-384759">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                So, I'm I doing something wrong by defining new properties on the prototype property in my short snippet?
                    – <a href="/users/58961/john-leidegren" title="33,506 reputation" target="_blank">John Leidegren</a>
                <a href="#comment384759_572996" target="_blank">Feb 21 '09 at 14:11</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-386327">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I think this is what it means to have function objects as first-class citizens.
                    – <a href="/users/58961/john-leidegren" title="33,506 reputation" target="_blank">John Leidegren</a>
                <a href="#comment386327_572996" target="_blank">Feb 22 '09 at 7:16</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-386340">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                7
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I hate non standard things, especially in programming languages, why is there even a <b>proto</b> when it's clearly not needed?
                    – <a href="/users/58961/john-leidegren" title="33,506 reputation" target="_blank">John Leidegren</a>
                <a href="#comment386340_572996" target="_blank">Feb 22 '09 at 7:23</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-4450924">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                37
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            
        </td>
    </tr>
    <tr id="comment-25164290">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                12
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                note that the use of <i>[[Prototype]]</i> is deliberate - ECMA-262 encloses names of internal properties with double square brackets
                    – <a href="/users/48015/christoph" title="116,145 reputation" target="_blank">Christoph</a>
                <a href="#comment25164290_572996" target="_blank">Jun 27 '13 at 13:25</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-572996">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>7</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-47790356">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful (click again to undo)" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>There's two distinct but related entities here that need explaining:</p>

<ul>
<li>The <code>.prototype</code> property of functions.</li>
<li>The <code>[[Prototype]]</code><sup><sup>[1]</sup></sup> property of all objects<sup><sup>[2]</sup></sup>. </li>
</ul>

<p>These are two different things. </p>

<h2>The <code>[[Prototype]]</code> property:</h2>

<p>This is a property that exists on all<sup><sup>[2]</sup></sup> objects.</p>

<p>What's stored here is another object, which, as an object itself, has a <code>[[Prototype]]</code> of its own that points to another object. That other object has a <code>[[Prototype]]</code> of its own. This story continues until you reach the prototypical object that provides methods that are accessible on all objects (like <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString" target="_blank"><code>.toString</code></a>).</p>

<p>The <code>[[Prototype]]</code> property is part of what forms the <code>[[Prototype]]</code> chain which is how prototypical inheritance is implemented. This chain of <code>[[Prototype]]</code> objects is what is examined when look-ups are performed on an object. </p>

<h2>The <code>.prototype</code> property:</h2>

<p><em>This is a property that is only found on functions.</em> Using a very simple function:</p>

<pre><code>function Bar(){};</code></pre>

<p>The <code>.prototype</code> property <em>holds an object</em> that will be assigned to <code>b.[[Prototype]]</code> when you do <code>var b = new Bar</code>. You can easily examine this:</p>

<pre><code>// Both assign Bar.prototype to b1/b2[[Prototype]]
var b = new Bar;
// Object.getPrototypeOf grabs the objects [[Prototype]]
console.log(Object.getPrototypeOf(b) === Bar.prototype) // true</code></pre>

<p>One of the most important <code>.prototype</code>s is that <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype" target="_blank">of the <code>Object</code> function</a>. This prototype holds the prototypical object that all <code>[[Prototype]]</code> chains contain. On it, all the available methods for new objects are defined:</p>

<pre><code>// Get properties that are defined on this object
console.log(Object.getOwnPropertyDescriptors(Object.prototype))</code></pre>

<p>Now, since <code>.prototype</code> is an object, it has a <code>[[Prototype]]</code> property. When you don't make any assignments to <code>Function.prototype</code>, the <code>.prototype</code>'s <code>[[Prototype]]</code> points to the prototypical object (<code>Object.prototype</code>). This is automatically performed anytime you create a new function. </p>

<p>This way, any time you do <code>new Bar;</code> the prototype chain is set up for you, you get everything defined on <code>Bar.prototype</code> and everything defined on <code>Object.prototype</code>:</p>

<pre><code>var b = new Bar;
// Get all Bar.prototype properties
console.log(b.__proto__ === Bar.prototype)
// Get all Object.prototype properties
console.log(b.__proto__.__proto__ === Object.prototype)</code></pre>

<p>When you <em>do</em> make assignments to <code>Function.prototype</code> all you are doing is extending the prototype chain to include another object. It's like an insertion in a singly linked list. </p>

<p>This basically alters the <code>[[Prototype]]</code> chain allowing properties that are defined on the object assigned to <code>Function.prototype</code> to be seen by any object created by the function.</p>

<hr />

<p><sup>[1: That won't confuse anyone; made available via <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/proto" target="_blank">the <code>__proto__</code> property</a> in many implementations.</sup><br />
<sup>[2]: All except <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null" target="_blank"><code>null</code></a>.</sup></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-47790356">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-23877420">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful (click again to undo)" target="_blank">up vote</a>
        47
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p><strong>0)</strong> Two different things can be called "prototype":</p>

<ul>
<li><p>the prototype property, as in <code>obj.prototype</code></p></li>
<li><p>the prototype internal property, denoted as <code>[[Prototype]]</code> <a href="http://www.ecma-international.org/ecma-262/5.1/#sec-8.6.2" target="_blank">in ES5</a>.</p>

<p>It can be retrieved via the ES5 <code>Object.getPrototypeOf()</code>.</p>

<p>Firefox makes it accessible through the <code>__proto__</code> property as an extension. <a href="http://www.ecma-international.org/ecma-262/6.0/#sec-additional-ecmascript-features-for-web-browsers" target="_blank">ES6 now mentions</a> some optional requirements for <code>__proto__</code>.</p></li>
</ul>

<hr />

<p><strong>1)</strong> Those concepts exist to answer the question:</p>

<blockquote>
  <p>When I do <code>obj.property</code>, where does JS look for <code>.property</code>?</p>
</blockquote>

<p>Intuitively, classical inheritance should affect property lookup.</p>

<hr />

<p><strong>2)</strong></p>

<ul>
<li><code>__proto__</code> is used for the dot <code>.</code> property lookup as in <code>obj.property</code>. </li>
<li><code>.prototype</code> is <em>not</em> used for lookup directly, only indirectly as it determines <code>__proto__</code> at object creation with <code>new</code>.</li>
</ul>

<p>Lookup order is:</p>

<ul>
<li><code>obj</code> properties added with <code>obj.p = ...</code> or <code>Object.defineProperty(obj, ...)</code></li>
<li>properties of <code>obj.__proto__</code></li>
<li>properties of <code>obj.__proto__.__proto__</code>, and so on</li>
<li>if some <code>__proto__</code> is <code>null</code>, return <code>undefined</code>.</li>
</ul>

<p>This is the so-called <em>prototype chain</em>.</p>

<p>You can avoid <code>.</code> lookup with <code>obj.hasOwnProperty('key')</code> and <code>Object.getOwnPropertyNames(f)</code></p>

<hr />

<p><strong>3)</strong> There are two main ways to set <code>obj.__proto__</code>:</p>

<ul>
<li><p><code>new</code>:</p>

<pre><code>var F = function() {}
var f = new F()</code></pre>

<p>then <code>new</code> has set:</p>

<pre><code>f.__proto__ === F.prototype</code></pre>

<p><em>This</em> is where <code>.prototype</code> gets used.</p></li>
<li><p><code>Object.create</code>:</p>

<pre><code> f = Object.create(proto)</code></pre>

<p>sets:</p>

<pre><code>f.__proto__ === proto</code></pre></li>
</ul>

<hr />

<p><strong>4)</strong> The code:</p>

<pre><code>var F = function() {}
var f = new F()</code></pre>

<p>Corresponds to the following diagram:</p>

<pre><code>(Function)       (  F  )                                      (f)
 |  ^             | | ^                                        |
 |  |             | | |                                        |
 |  |             | | +-------------------------+              |
 |  |constructor  | |                           |              |
 |  |             | +--------------+            |              |
 |  |             |                |            |              |
 |  |             |                |            |              |
 |[[Prototype]]   |[[Prototype]]   |prototype   |constructor   |[[Prototype]]
 |  |             |                |            |              |
 |  |             |                |            |              |
 |  |             |                | +----------+              |
 |  |             |                | |                         |
 |  |             |                | | +-----------------------+
 |  |             |                | | |
 v  |             v                v | v
(Function.prototype)              (F.prototype)
 |                                 |
 |                                 |
 |[[Prototype]]                    |[[Prototype]]
 |                                 |
 |                                 |
 | +-------------------------------+
 | |
 v v
(Object.prototype)
 | | ^
 | | |
 | | +---------------------------+
 | |                             |
 | +--------------+              |
 |                |              |
 |                |              |
 |[[Prototype]]   |constructor   |prototype
 |                |              |
 |                |              |
 |                | -------------+
 |                | |
 v                v |
(null)           (Object)</code></pre>

<p>This diagram shows many language predefined object nodes: <code>null</code>, <code>Object</code>, <code>Object.prototype</code>, <code>Function</code> and <code>Function.prototype</code>. Our 2 lines of code only created <code>f</code>, <code>F</code> and <code>F.prototype</code>.</p>

<hr />

<p><strong>5)</strong> <code>.constructor</code> normally comes from <code>F.prototype</code> through the <code>.</code> lookup:</p>

<pre><code>f.constructor === F
!f.hasOwnProperty('constructor')
Object.getPrototypeOf(f) === F.prototype
F.prototype.hasOwnProperty('constructor')
F.prototype.constructor === f.constructor</code></pre>

<p>When we write <code>f.constructor</code>, JavaScript does the <code>.</code> lookup as:</p>

<ul>
<li><code>f</code> does not have <code>.constructor</code></li>
<li><code>f.__proto__ === F.prototype</code> has <code>.constructor === F</code>, so take it</li>
</ul>

<p>The result <code>f.constructor == F</code> is intuitively correct, since <code>F</code> is used to construct <code>f</code>, e.g. set fields, much like in classic OOP languages. </p>

<hr />

<p><strong>6)</strong> Classical inheritance syntax can be achieved by manipulating prototypes chains.</p>

<p>ES6 adds the <code>class</code> and <code>extends</code> keywords, which are simply syntax sugar for previously possible prototype manipulation madness.</p>

<pre><code>class C {
    constructor(i) {
        this.i = i
    }
    inc() {
        return this.i + 1
    }
}

class D extends C {
    constructor(i) {
        super(i)
    }
    inc2() {
        return this.i + 2
    }
}</code></pre>



<pre><code>// Inheritance syntax works as expected.
(new C(1)).inc() === 2
(new D(1)).inc() === 2
(new D(1)).inc2() === 3</code></pre>



<pre><code>// "Classes" are just function objects.
C.constructor === Function
C.__proto__ === Function.prototype
D.constructor === Function
// D is a function "indirectly" through the chain.
D.__proto__ === C
D.__proto__.__proto__ === Function.prototype</code></pre>



<pre><code>// "extends" sets up the prototype chain so that base class
// lookups will work as expected
var d = new D(1)
d.__proto__ === D.prototype
D.prototype.__proto__ === C.prototype
// This is what `d.inc` actually does.
d.__proto__.__proto__.inc === C.prototype.inc</code></pre>



<pre><code>// Class variables
// No ES6 syntax sugar apparently:
// http://stackoverflow.com/questions/22528967/es6-class-variable-alternatives
C.c = 1
C.c === 1
// Because `D.__proto__ === C`.
D.c === 1
// Nothing makes this work.
d.c === undefined</code></pre>

<p>Simplified diagram without all predefined objects:</p>

<pre><code>      __proto__
(C)&lt;---------------(D)         (d)
| |                |           |
| |                |           |
| |prototype       |prototype  |__proto__
| |                |           |
| |                |           |
| |                | +---------+
| |                | |
| |                | |
| |                v v
|__proto__        (D.prototype)
| |                |
| |                |
| |                |__proto__
| |                |
| |                |
| | +--------------+
| | |
| | |
| v v
| (C.prototype)---&gt;(inc)
|
v
Function.prototype</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-23877420">
		        <table>
                    <tbody>



    <tr id="comment-42776134">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I don't know where you got this but this is the most clear answer!
                    – <a href="/users/881375/tomasb" title="1,350 reputation" target="_blank">tomasb</a>
                <a href="#comment42776134_23877420" target="_blank">Nov 26 '14 at 0:10</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-42784553">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @tomasb thanks! "I don't know where you got this": after I've seen a few of those dynamic languages, I noticed what matters the most about their class system is how the <code>.</code> lookup works ( and how many copies of the data are made). So I set out to understand that point. The rest is Google + blog posts + a Js interpreter at hand. :)
                    – <a href="/users/895245/ciro-santilli-%e5%8d%8e%e6%b6%8c%e4%bd%8e%e7%ab%af%e4%ba%ba%e5%8f%a3-%e5%85%ad%e5%9b%9b%e4%ba%8b%e4%bb%b6-%e6%b3%95%e8%bd%ae%e5%8a%9f" title="96,286 reputation" target="_blank">Ciro Santilli 华涌低端人口 六四事件 法轮功</a>
                <a href="#comment42784553_23877420" target="_blank">Nov 26 '14 at 8:19</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-45782432">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This answer shows true and deep understanding of that concept.  Good job!
                    – <a href="/users/2776181/nir-smadar" title="117 reputation" target="_blank">Nir Smadar</a>
                <a href="#comment45782432_23877420" target="_blank">Feb 26 '15 at 18:43</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-52686146">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I still don't get the point why g.constructor === Object because you said that "4) When you do f = new F, new also sets f.constructor = F".  Could you explain to me more?  Anyway this is the best answer I'm looking for. Thank you so much!
                    – <a href="/users/1562388/nguyenngoc101" title="381 reputation" target="_blank">nguyenngoc101</a>
                <a href="#comment52686146_23877420" target="_blank">Sep 5 '15 at 3:16</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-52726805">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @Now it's all clear, I voted for your answer. Thank you for helping me.
                    – <a href="/users/1562388/nguyenngoc101" title="381 reputation" target="_blank">nguyenngoc101</a>
                <a href="#comment52726805_23877420" target="_blank">Sep 7 '15 at 4:05</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-23877420">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>9</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-17177624">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        30
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Every object has an internal property, [[Prototype]], linking it to another object:</p>

<pre><code>object [[Prototype]] -&gt; anotherObject</code></pre>

<p>Some environments expose that property as <code>__proto__</code>:</p>

<pre><code>anObject.__proto__ === anotherObject</code></pre>

<p>You create the [[Prototype]] link when creating an object:</p>

<pre><code>var object = Object.create(anotherObject)
// imagine:
// object.__proto__ = anotherObject

// or (ES6 only):
var object = { __proto__: anotherObject };</code></pre>

<p>In traditional javascript, the linked object is the <code>prototype</code> property of a function:</p>

<pre><code>object [[Prototype]] -&gt; aFunction.prototype</code></pre>

<p>and you create the [[Prototype]] link with <code>new</code>:</p>

<pre><code>var object = new aFunction;
// imagine:
// object.__proto__ = aFunction.prototype;</code></pre>

<p>So these statements are equivalent:</p>

<pre><code>var object = Object.create(Object.prototype);
var object = new Object;
// object.__proto__ === Object.prototype</code></pre>

<p>Note that the link target (<code>Object.prototype</code>) appears only in the <code>Object.create</code> call.</p>

<p>Remember:</p>

<ul>
<li>Every object has a link, [[Prototype]], sometimes exposed as <code>__proto__</code>.</li>
<li>Every function has a <code>prototype</code> property.</li>
<li>Objects created with <code>new</code> are linked to the <code>prototype</code> property of their constructor.</li>
<li>If a function is never used as a constructor, its <code>prototype</code> property will go unused.</li>
<li>If you don't need a constructor, skip <code>new</code> and use <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create" target="_blank">Object.create</a> instead.</li>
</ul>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-17177624">
		        <table>
                    <tbody>



    <tr id="comment-31922275">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                +1 for highlighting Object.create()
                    – <a href="/users/1576463/jakob-sternberg" title="1,063 reputation" target="_blank">Jakob Sternberg</a>
                <a href="#comment31922275_17177624" target="_blank">Jan 18 '14 at 1:46</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-51229673">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Revision 5 removed some useful info, including info on Object.create(). See <a href="http://stackoverflow.com/revisions/17177624/4" target="_blank">revision 4</a>.
                    – <a href="/users/2157640/palec" title="6,243 reputation" target="_blank">Palec</a>
                <a href="#comment51229673_17177624" target="_blank">Jul 26 '15 at 20:21</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-51266591">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @Palec what should I add back?
                    – <a href="/users/822138/sam" title="15,764 reputation" target="_blank">sam</a>
                <a href="#comment51266591_17177624" target="_blank">Jul 27 '15 at 18:50</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-51333794">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                IMO at least the link to <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create" target="_blank"><code>Object.create()</code> docs</a>, @sam. Links to <a href="https://developer.mozilla.org/cs/docs/Web/JavaScript/Reference/Global_Objects/Object/Proto" target="_blank"><code>__proto__</code></a> and <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype" target="_blank"><code>Object.prototype</code></a> would be nice enhancements. And I liked your examples of how prototypes work with constructors and <code>Object.create()</code>, but they were probably the long and less relevant part you wanted to get rid of.
                    – <a href="/users/2157640/palec" title="6,243 reputation" target="_blank">Palec</a>
                <a href="#comment51333794_17177624" target="_blank">Jul 29 '15 at 9:55</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-68630703">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                from the all discussion what i get(came from classical inheritance) if i create constructor function and try to create instance of it using new operator i will only get methods and properties that was attach to proto object, therefore its necessary to attach all the method and properties to proto object if we want to inherit, m i right?
                    – <a href="/users/5710014/blackhawk" title="1,105 reputation" target="_blank">blackHawk</a>
                <a href="#comment68630703_17177624" target="_blank">Nov 20 '16 at 5:33</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-17177624">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-44199180">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I always like analogies when it comes to understand this type of stuff. 'Prototypal inheritance' is pretty confusing in comparison to class bass inheritance in my opinion, even though prototypes are much simpler paradigm. In fact there really is no inheritance, so the name in and of itself misleading, it's more like prototypal delegation.</p>

<p>Imagine this ....</p>

<p>You're in high-school, and you're in class and have a test that's due today, but you don't have a pen to complete it. Ohshi-</p>

<p>You have a best friend, Finnius Mcdinglebutt who might possibly have a pen? You ask, and he looks on his desk unsuccessfully, but instead of saying "Man, I don't have a pen", he's a nice friend he checks with his other friend Derp Derpington if he has a pen. Derp does have a pen and passes it back to Finnius, who passes it over to you to complete your test. Derp has entrusted the pen to Finnius, who has delegated the pen to you for use.</p>

<p>This, is essentially how prototypes work in a nutshell.</p>


    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered May 26 '17 at 10:24
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-44199180">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-42880438">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        12
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>It may help to categorise prototype chains into two categories.</p>

<p>Consider the constructor:</p>

<pre><code> function Person() {}</code></pre>

<p>The value of <code>Object.getPrototypeOf(Person)</code> is a function. In fact, it is <code>Function.prototype</code>. Since <code>Person</code> was created as a function, it shares the same prototype function object that all functions have. It is the same as <code>Person.__proto__</code>, but that property should not be used. Anyway, with <code>Object.getPrototypeOf(Person)</code> you effectively walk up the ladder of what is called the prototype chain.</p>

<p>The chain in upward direction looks like this:</p>

<p>    <code>Person</code> → <code>Function.prototype</code> → <code>Object.prototype</code> (end point)</p>

<p>Important is that this prototype chain has little to do with the objects that <code>Person</code> can <em>construct</em>. Those constructed objects have their own prototype chain, and this chain can potentially have no close ancestor in common with the one mentioned above.</p>

<p>Take for example this object:</p>

<pre><code>var p = new Person();</code></pre>

<p><em>p</em> has no direct prototype-chain relationship with <em>Person</em>. Their relationship is a different one. The object <em>p</em> has its own prototype chain. Using <code>Object.getPrototypeOf</code>, you'll find the chain is as follows:</p>

<p>    <code>p</code> → <code>Person.prototype</code> → <code>Object.prototype</code> (end point)</p>

<p>There is no function object in this chain (although that could be).</p>

<p>So <code>Person</code> seems related to two kinds of chains, which live their own lives. To "jump" from one chain to the other, you use:</p>

<ol>
<li><p><code>.prototype</code>: jump from the constructor's chain to the created-object's chain. This property is thus only defined for function objects (as <code>new</code> can only be used on functions).</p></li>
<li><p><code>.constructor</code>: jump from the created-object's chain to the constructor's chain.</p></li>
</ol>

<p>Here is a visual presentation of the two prototype chains involved, represented as columns:</p>

<p><a href="https://i.stack.imgur.com/FPPdI.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/FPPdI.png" alt="enter image description here" /></div></a></p>

<p>To summarise:</p>

<blockquote>
  <p>The <code>prototype</code> property gives no information of the <em>subject's</em> prototype chain, but of objects <em>created by</em> the subject. </p>
</blockquote>

<p>It is no surprise that the name of the property <code>prototype</code> can lead to confusion. It would maybe have been clearer if this property had been named <code>prototypeOfConstructedInstances</code> or something along that line.</p>

<p>You can jump back and forth between the two prototype chains:</p>

<pre><code>Person.prototype.constructor === Person</code></pre>

<p>This symmetry can be broken by explicitly assigning a different object to the <code>prototype</code> property (more about that later).</p>

<h3>Create one Function, Get Two Objects</h3>

<p><code>Person.prototype</code> is an object that was created at the same time the function <code>Person</code> was created. It has <code>Person</code> as constructor, even though that constructor did not actually execute yet. So two objects are created at the same time:</p>

<ol>
<li>The function <code>Person</code> itself</li>
<li>The object that will act as prototype when the function is called as a constructor</li>
</ol>

<p>Both are objects, but they have different roles: the function object <em>constructs</em>, while the other object represents the prototype of any object that function will construct. The prototype object will become the parent of the constructed object in its prototype chain.</p>

<p>Since a function is also an object, it also has its own parent in its own prototype chain, but recall that these two chains are about different things. </p>

<p>Here are some equalities that could help grasp the issue -- all of these print <code>true</code>:</p>

<div>
<div>
<pre><code>function Person() {};

// This is prototype chain info for the constructor (the function object):
console.log(Object.getPrototypeOf(Person) === Function.prototype);
// Step further up in the same hierarchy:
console.log(Object.getPrototypeOf(Function.prototype) === Object.prototype);
console.log(Object.getPrototypeOf(Object.prototype) === null);
console.log(Person.__proto__ === Function.prototype);
// Here we swap lanes, and look at the constructor of the constructor
console.log(Person.constructor === Function);
console.log(Person instanceof Function);

// Person.prototype was created by Person (at the time of its creation)
// Here we swap lanes back and forth:
console.log(Person.prototype.constructor === Person);
// Although it is not an instance of it:
console.log(!(Person.prototype instanceof Person));
// Instances are objects created by the constructor:
var p = new Person();
// Similarly to what was shown for the constructor, here we have
// the same for the object created by the constructor:
console.log(Object.getPrototypeOf(p) === Person.prototype);
console.log(p.__proto__ === Person.prototype);
// Here we swap lanes, and look at the constructor
console.log(p.constructor === Person);
console.log(p instanceof Person);</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
<h3>Adding levels to the prototype chain</h3>

<p>Although a prototype object is created when you create a constructor function, you can ignore that object, and assign another object that should be used as prototype for any subsequent instances created by that constructor.</p>

<p>For instance:</p>

<pre><code>function Thief() { }
var p = new Person();
Thief.prototype = p; // this determines the prototype for any new Thief objects:
var t = new Thief();</code></pre>

<p>Now the prototype chain of <em>t</em> is one step longer than that of <em>p</em>:</p>

<p>    <code>t</code> → <code>p</code> → <code>Person.prototype</code> → <code>Object.prototype</code> (end point)</p>

<p>The other prototype chain is not longer: <code>Thief</code> and <code>Person</code> are siblings sharing the same parent in their prototype chain:</p>

<p>    <code>Person</code>}<br />
    <code>Thief</code>  } → <code>Function.prototype</code> → <code>Object.prototype</code> (end point)</p>

<p>The earlier presented graphic can then be extended to this (the original <code>Thief.prototype</code> is left out):</p>

<p><a href="https://i.stack.imgur.com/m5DXc.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/m5DXc.png" alt="enter image description here" /></div></a></p>

<p>The blue lines represent prototype chains, the other coloured lines represent other relationships:</p>

<ul>
<li>between an object and its constructor</li>
<li>between a constructor and the prototype object that will be used for constructing objects</li>
</ul>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-42880438">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-38174603">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        18
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>The concept of <code>prototypal</code> inheritance is one of the most complicated for many developers. Let's try to understand the root of problem to understand <code>prototypal inheritance</code> better. Let's start with a <code>plain</code> function. </p>

<p>If we use a <code>new</code> operator on the <code>Tree function</code>, we call it as a <code>constructor</code> function. </p>

<p><a href="https://i.stack.imgur.com/cU6Qh.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/cU6Qh.png" alt="enter image description here" /></div></a></p>

<p>Every <code>JavaScript</code> function has a <code>prototype</code>. When you log the <code>Tree.prototype</code>, you get...</p>

<p><a href="https://i.stack.imgur.com/Xop8c.png" target="_blank" class="readableLinkWithMediumImage"><img src="https://i.stack.imgur.com/Xop8c.png" alt="enter image description here" /></a></p>

<p>If you look at the above <code>console.log()</code> output, you could a see a constructor property on <code>Tree.prototype</code> and a <code>__proto__</code> property too. The <code>__proto__</code> represents the <code>prototype</code> that this <code>function</code> is based off, and since this is just a plain <code>JavaScript function</code> with no <code>inheritance</code> set up yet, it refers to the <code>Object prototype</code> which is something just built in to JavaScript...</p>

<p><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype" target="_blank">https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype</a></p>

<p>This has things like <code>.toString, .toValue, .hasOwnProperty</code> etc...</p>

<p><code>__proto__</code> which was brought my mozilla is deprecated and is replaced by <code>Object.getPrototypeOf</code> method to get the <code>object's prototype</code>. </p>

<pre><code>Object.getPrototypeOf(Tree.prototype); // Object {} </code></pre>

<p>Let's add a method to our <code>Tree</code> <code>prototype</code>. </p>

<p>We have modified the <code>Root</code> and added a <code>function</code> branch to it. </p>

<p><a href="https://i.stack.imgur.com/cU6Qh.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/cU6Qh.png" alt="enter image description here" /></div></a></p>

<p>That means when you create an <code>instance</code> of <code>Tree</code>, you can call it's <code>branch</code> method.</p>

<p><a href="https://i.stack.imgur.com/Xop8c.png" target="_blank" class="readableLinkWithMediumImage"><img src="https://i.stack.imgur.com/Xop8c.png" alt="enter image description here" /></a></p>

<p>We can also add <code>primitives</code> or <code>objects</code> to our <code>Prototype</code>. </p>

<p>Let's add a <code>child-tree</code> to our <code>Tree</code>. </p>

<p><a href="https://i.stack.imgur.com/ggFON.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/ggFON.png" alt="enter image description here" /></div></a></p>

<p>Here the <code>Child</code> inherits its <code>prototype</code> from Tree, what we are doing here is using <code>Object.create()</code> method to create a new object based off what you pass, here it is <code>Tree.prototype</code>. In this case what we're doing is setting the prototype of Child to a new object that looks identical to the <code>Tree</code> prototype. Next we are setting the <code>Child's constructor to Child</code>, if we don't it would point to <code>Tree()</code>. </p>

<p><a href="https://i.stack.imgur.com/yiZcY.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/yiZcY.png" alt="enter image description here" /></div></a></p>

<p><code>Child</code> now has its own <code>prototype</code>, its <code>__proto__</code> points to <code>Tree</code> and <code>Tree's prototype</code> points to base <code>Object</code>. </p>

<pre><code>Child  
|
 \
  \
   Tree.prototype
   - branch
   |
   |
    \
     \
      Object.prototype
      -toString
      -valueOf
      -etc., etc.</code></pre>

<p>Now you create an <code>instance</code> of <code>Child</code> and call <code>branch</code> which is originally available in <code>Tree</code>. We haven't actually defined our <code>branch</code> on the <code>Child prototype</code>. BUT, in the <code>Root prototype</code> which Child inherits from. </p>

<p><a href="https://i.stack.imgur.com/k6BNb.png" target="_blank" class="readableLinkWithMediumImage"><img src="https://i.stack.imgur.com/k6BNb.png" alt="enter image description here" /></a></p>

<p><strong>In JS everything is not an object, everything can act like an object.</strong></p>

<p><code>Javascript</code> has primitives like <code>strings, number, booleans, undefined, null.</code> They are not <code>object(i.e reference types)</code>, but certainly can act like an <code>object</code>. Let's look at an example here.</p>

<p>In the first line of this listing, a <code>primitive</code> string value is assigned to name. The second line treats name like an <code>object</code> and calls <code>charAt(0)</code> using dot notation.</p>

<p>This is what happens behind the scenes:
// what the <code>JavaScript</code> engine does</p>

<p><a href="https://i.stack.imgur.com/l6MHc.png" target="_blank" class="readableLinkWithMediumImage"><img src="https://i.stack.imgur.com/l6MHc.png" alt="enter image description here" /></a></p>

<p>The <code>String object</code> exists only for one statement before it’s destroyed (a process called <code>autoboxing</code>). Let's again get back to our <code>prototypal</code> <code>inheritance</code>. </p>

<ul>
<li><code>Javascript</code> supports inheritance via <code>delegation</code> based on
<code>prototypes</code>.</li>
<li>Each <code>Function</code> has a <code>prototype</code> property, which refers to another
object.</li>
<li><code>properties/functions</code> are looked from the <code>object</code> itself or via
<code>prototype</code> chain if it does not exist</li>
</ul>

<p>A <code>prototype</code> in JS is an object which <code>yields</code> you to the parent of another <code>object</code>. <strong>[ie.. delegation]</strong> <code>Delegation</code> means that if you are unable to do something, you’ll tell someone else to do it for you.</p>

<p><a href="https://i.stack.imgur.com/W0NUA.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/W0NUA.png" alt="enter image description here" /></div></a></p>

<p><a href="https://jsfiddle.net/say0tzpL/1/" target="_blank">https://jsfiddle.net/say0tzpL/1/</a></p>

<p>If you look up the above fiddle, dog has access to <code>toString</code> method, but its not available in it, but available via the prototype chain which delegates to <code>Object.prototype</code></p>

<p>If you look at the below one, we are trying to access the <code>call</code> method which is available in every <code>function</code>.</p>

<p><a href="https://i.stack.imgur.com/iF4RN.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/iF4RN.png" alt="enter image description here" /></div></a></p>

<p><a href="https://jsfiddle.net/rknffckc/" target="_blank">https://jsfiddle.net/rknffckc/</a></p>

<p>If you look up the above fiddle, <code>Profile</code> Function has access to <code>call</code> method, but its not available in it, but available via the prototype chain which delegates to <code>Function.prototype</code></p>

<p><strong>Note:</strong> <code>prototype</code> is a property of the function constructor, whereas <code>__proto__</code> is a property of the objects constructed from the function constructor. Every function comes with a <code>prototype</code> property whose value is an empty <code>object</code>. When we create an instance of the function, we get an internal property <code>[[Prototype]]</code> or <code>__proto__</code> whose reference is the prototype of the Function <code>constructor</code>.</p>

<p><a href="https://i.stack.imgur.com/HvzDP.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/HvzDP.png" alt="enter image description here" /></div></a></p>

<p>The above diagram looks bit complicated, but brings out the whole picture on how <code>prototype chaining</code> works. Let's walk through this slowly:</p>

<p>There are two instance <code>b1</code> and <code>b2</code>, whose constructor is <code>Bar</code> and parent is Foo and has two methods from prototype chain <code>identify</code> and <code>speak</code> via <code>Bar</code> and <code>Foo</code></p>

<p><a href="https://i.stack.imgur.com/EllEL.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/EllEL.png" alt="enter image description here" /></div></a></p>

<p><a href="https://jsfiddle.net/kbp7jr7n/" target="_blank">https://jsfiddle.net/kbp7jr7n/</a></p>

<p>If you look up the code above, we have <code>Foo</code> constructor who has the method <code>identify()</code> and <code>Bar</code> constructor which has <code>speak</code> method. We create two <code>Bar</code> instance <code>b1</code> and <code>b2</code> whose parent type is <code>Foo</code>. Now while calling <code>speak</code> method of <code>Bar</code>, we are able to identify the who is calling the speak via <code>prototype</code> chain. </p>

<p><a href="https://i.stack.imgur.com/V7fH7.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/V7fH7.png" alt="enter image description here" /></div></a></p>

<p><code>Bar</code> now has all the methods of <code>Foo</code> which are defined in its <code>prototype</code>. Let's dig further in understanding the <code>Object.prototype</code> and <code>Function.prototype</code> and how they are related. If you look up the constructor of <code>Foo</code>, <code>Bar</code> and <code>Object</code> are <code>Function constructor</code>.</p>

<p><a href="https://i.stack.imgur.com/wzzRu.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/wzzRu.png" alt="enter image description here" /></div></a></p>

<p>The <code>prototype</code> of <code>Bar</code> is <code>Foo</code>, <code>prototype</code> of <code>Foo</code> is <code>Object</code> and if you look closely the <code>prototype</code> of <code>Foo</code> is related to <code>Object.prototype</code>.</p>

<p><a href="https://i.stack.imgur.com/wEOxo.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/wEOxo.png" alt="enter image description here" /></div></a></p>

<p>Before we close this down, let's just wrap with a small piece of code here to <strong>summarize everything above</strong>. We are using <code>instanceof</code> operator here to check whether an <code>object</code> has in its <code>prototype</code> chain the <code>prototype</code> property of a <code>constructor</code> which below summarizes the entire big diagram. </p>

<p><a href="https://i.stack.imgur.com/n84uV.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/n84uV.png" alt="enter image description here" /></div></a></p>

<p>I hope this add's some information, I know this kinda could be big to grasp... in simple words its <strong>it's just objects linked to objects!!!!</strong> </p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 3 '16 at 21:44
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-38174603">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-35948308">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Consider the following <code>keyValueStore</code> object :</p>

<pre><code>var keyValueStore = (function() {
    var count = 0;
    var kvs = function() {
        count++;
        this.data = {};
        this.get = function(key) { return this.data[key]; };
        this.set = function(key, value) { this.data[key] = value; };
        this.delete = function(key) { delete this.data[key]; };
        this.getLength = function() {
            var l = 0;
            for (p in this.data) l++;
            return l;
        }
    };

    return  { // Singleton public properties
        'create' : function() { return new kvs(); },
        'count' : function() { return count; }
    };
})();</code></pre>

<p>I can create a new instance of this object by doing this :</p>

<pre><code>kvs = keyValueStore.create();</code></pre>

<p>Each instance of this object would have the following public properties :</p>

<ul>
<li><code>data</code></li>
<li><code>get</code> </li>
<li><code>set</code></li>
<li><code>delete</code></li>
<li><code>getLength</code></li>
</ul>

<p>Now, suppose we create 100 instances of this <code>keyValueStore</code> object. Even though <code>get</code>, <code>set</code>, <code>delete</code>, <code>getLength</code> will do the exact same thing for each of these 100 instances, every instance has its own copy of this function.</p>

<p>Now, imagine if you could have just a single <code>get</code>, <code>set</code>, <code>delete</code> and <code>getLength</code> copy, and each instance would reference that same function. This would be better for performance and require less memory.</p>

<p>That's where prototypes come in. A prototype is a "blueprint" of properties that is inherited but not copied by instances. So this means that it exists only once in memory for all instances of an object and is shared by all of those instances.</p>

<p>Now, consider the <code>keyValueStore</code> object again. I could rewrite it like this :</p>

<pre><code>var keyValueStore = (function() {
    var count = 0;
    var kvs = function() {
        count++;
        this.data = {};
    };

    kvs.prototype = {
        'get' : function(key) { return this.data[key]; },
        'set' : function(key, value) { this.data[key] = value; },
        'delete' : function(key) { delete this.data[key]; },
        'getLength' : function() {
            var l = 0;
            for (p in this.data) l++;
            return l;
        }
    };

    return  {
        'create' : function() { return new kvs(); },
        'count' : function() { return count; }
    };
})();</code></pre>

<p>This does EXACTLY the same as the previous version of the <code>keyValueStore</code> object, except that all of its methods are now put in a prototype. What this means, is that all of the 100 instances now share these four methods instead of each having their own copy.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Mar 11 '16 at 19:24
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-35948308">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-35485350">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        13
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p><a href="https://www.youtube.com/watch?v=PMfcsYzj-9M" target="_blank">The Definitive Guide to Object-Oriented JavaScript</a> - a very concise and clear ~30min video explanation of the asked question (Prototypal Inheritance topic begins from <a href="https://youtu.be/PMfcsYzj-9M?t=344" target="_blank">5:45</a>, although I'd rather listen to the whole video). The author of this video also made JavaScript object visualizer website <a href="http://www.objectplayground.com/" target="_blank">http://www.objectplayground.com/</a>.<a href="https://i.stack.imgur.com/Vf4qR.jpg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/Vf4qR.jpg" alt="enter image description here" /></div></a>
<a href="https://i.stack.imgur.com/xcRpT.jpg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/xcRpT.jpg" alt="enter image description here" /></div></a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-35485350">
		        <table>
                    <tbody>



    <tr id="comment-65099618">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-35485350">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-33523979">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        22
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>This article is long. But I am sure it will clear most of your queries 
regarding the "prototypical" nature of JavaScript Inheritance. And even more. Please read the complete article.</p>

<p>JavaScript basically has two kinds of data types</p>

<ul>
<li><strong><em>Non objects</em></strong> </li>
<li><strong><em>Objects</em></strong></li>
</ul>

<p><strong><em>Non objects</em></strong></p>

<p>Following are the <strong><em>Non object</em></strong> data types</p>

<ul>
<li><strong>string</strong></li>
<li><strong>number (including NaN and Infinity)</strong></li>
<li><strong>boolean values(true,false)</strong> </li>
<li><strong>undefined</strong></li>
</ul>

<p>These data types return following when you use the <strong>typeof</strong> operator </p>

<p><strong>typeof</strong> <em>"string literal"</em> (or a variable containing string literal)  === <strong>'string'</strong></p>

<p><strong>typeof</strong> <em>5</em> (or any numeric literal or a variable containing numeric literal or <strong><em>NaN or Infynity</em></strong>)  === <strong>'number'</strong></p>

<p><strong>typeof</strong> <em>true</em> (or <em>false</em> or a variable containing <em>true</em> or <em>false</em>)  === <strong>'boolean'</strong></p>

<p><strong>typeof</strong> <em>undefined</em> (or an undefined variable or a variable containing <em>undefined</em>) === <strong>'undefined'</strong></p>

<p>The <strong>string</strong>,<strong>number</strong> and <strong>boolean</strong> data types can be represented both as <strong>Objects</strong> and <strong>Non objects</strong>.When they are represented as objects their typeof is always === 'object'. We shall come back to this once we understand the object data types.</p>

<p><strong><em>Objects</em></strong></p>

<p>The object datatypes can be further divided into two types</p>

<ol>
<li><strong>Function type objects</strong></li>
<li><strong>Non Function type objects</strong></li>
</ol>

<p>The <strong>Function type objects</strong> are the ones that return the string <strong>'function'</strong> with <strong>typeof</strong> operator. 
All the user defined functions and all the JavaScript built in objects that can create new objects by using new operator fall into this category. For eg.</p>

<ul>
<li><strong>Object</strong></li>
<li><strong>String</strong> </li>
<li><strong>Number</strong>  </li>
<li><strong>Boolean</strong></li>
<li><strong>Array</strong> </li>
<li><strong>Typed Arrays</strong></li>
<li><strong>RegExp</strong></li>
<li><strong>Function</strong> </li>
<li>All the other built in objects that can create new objects by using new operator</li>
<li><em>function</em> <strong>UserDefinedFunction</strong>(){ /*user defined code */ }</li>
</ul>

<p>So,
<strong>typeof(Object)</strong> === <strong>typeof(String)</strong> === <strong>typeof(Number)</strong> === <strong>typeof(Boolean)</strong> === <strong>typeof(Array)</strong>  === <strong>typeof(RegExp)</strong> === <strong>typeof(Function)</strong>  === <strong>typeof(UserDefinedFunction)</strong> === <strong>'function'</strong></p>

<p>All the <strong><em>Function type objects</em></strong> are actually instances of the built in JavaScript object <strong>Function</strong> (including the <strong>Function</strong> object i.e it is recursively defined). It is as if the these objects have been defined in the following way</p>

<pre><code>var Object= new Function ([native code for object Object])
var String= new Function ([native code for object String])
var Number= new Function ([native code for object Number])
var Boolean= new Function ([native code for object Boolean])
var Array= new Function ([native code for object Array])
var RegExp= new Function ([native code for object RegExp])
var Function= new Function ([native code  for object Function])
var UserDefinedFunction= new Function ("user defined code")</code></pre>

<p>As mentioned, the <strong><em>Function type objects</em></strong> can further create new objects using the <strong>new operator</strong>. For e.g an object of type <strong>Object</strong>, <strong>String</strong>, <strong>Number</strong>, <strong>Boolean</strong>, <strong>Array</strong>, <strong>RegExp</strong>  Or <strong>UserDefinedFunction</strong> can be created by using</p>

<pre><code>var a=new Object() or var a=Object() or var a={} //Create object of type Object
var a=new String() //Create object of type String
var a=new Number() //Create object of type Number
var a=new Boolean() //Create object of type Boolean
var a=new Array() or var a=Array() or var a=[]  //Create object of type Array
var a=new RegExp() or var a=RegExp() //Create object of type RegExp
var a=new UserDefinedFunction() </code></pre>

<p>The objects thus created are all <strong><em>Non Function type objects</em></strong> and return their <strong>typeof</strong>===<strong>'object'</strong>. In all these cases the object "a" cannot further create 
objects using operator new. So the following is wrong</p>

<pre><code>var b=new a() //error. a is not typeof==='function'</code></pre>

<p>The built in object <strong>Math</strong> is <strong>typeof</strong>===<strong>'object'</strong>. Hence a new object of type Math cannot be created by new operator.</p>

<pre><code>var b=new Math() //error. Math is not typeof==='function'</code></pre>

<p>Also notice that <strong>Object</strong>,<strong>Array</strong> and <strong>RegExp</strong> functions can create a new object without even using <strong>operator new</strong>. However the follwing ones don't.</p>

<pre><code>var a=String() // Create a new Non Object string. returns a typeof==='string' 
var a=Number() // Create a new Non Object Number. returns a typeof==='number'
var a=Boolean() //Create a new Non Object Boolean. returns a typeof==='boolean'</code></pre>

<p>The user defined functions are special case. </p>

<pre><code>var a=UserDefinedFunction() //may or may not create an object of type UserDefinedFunction() based on how it is defined.</code></pre>

<p>Since the <strong><em>Function type objects</em></strong> can create new objects they are also called <strong><em>Constructors</em></strong>.</p>

<p>Every <strong>Constructor/Function</strong> (whether built in or user defined) when defined automatically has a property called <strong>"prototype"</strong> whose value by default is set as an object. This object itself has a property called <strong>"constructor"</strong> which by default references back the <strong>Constructor/Function</strong> .</p>

<p>For example when we define a function</p>

<pre><code>function UserDefinedFunction()
{
}</code></pre>

<p>following automatically happens</p>

<pre><code>UserDefinedFunction.prototype={constructor:UserDefinedFunction}</code></pre>

<p>This <strong>"prototype" property</strong> is only present in the <strong>Function type objects</strong> 
(and never in <strong>Non Function type objects</strong>). </p>

<p>This is because <strong>when a new object is created (using new operator)it inherits all properties and methods from Constructor function's current prototype object i.e. an</strong> <strong><em>internal reference</em></strong> <strong>is created in the newly created object that references the object referenced by Constructor function's current prototype object.</strong></p>

<p>This <strong>"internal reference"</strong> that is created in the object for referencing inherited properties is known as the <strong>object's prototype</strong> (which references the object referenced by Constructor's <strong>"prototype"</strong> property but is different from it). For any object (Function or Non Function) this can be retrieved using <strong>Object.getPrototypeOf()</strong> method. Using this method one can trace the prototype chain of an object. </p>

<p>Also, <strong>every object that is created</strong> (<strong>Function type</strong> or <strong>Non Function type</strong>) has a <strong>"constructor"</strong> property which is inherited from the object referenced by prototype  property of the Constructor function. By default this <strong>"constructor"</strong> property references the <strong>Constructor function</strong> that created it (if the <strong>Constructor Function's</strong> default "prototype" is not changed). </p>

<p>For all <strong><em>Function type objects</em></strong> the constructor function is always
<strong><em>function Function(){}</em></strong></p>

<p>For <strong><em>Non Function type objects</em></strong> (e.g Javascript Built in  Math object) the constructor function is the function that created it.
For <strong>Math</strong> object it is <strong><em>function Object(){}</em></strong>. </p>

<p>All the concept explained above can be a little daunting to understand without any supporting code. Please go through the following code line by line to understand the concept. Try to execute it to have a better understanding.</p>

<pre><code>function UserDefinedFunction()
{ 

} 

/* creating the above function automatically does the following as mentioned earlier

UserDefinedFunction.prototype={constructor:UserDefinedFunction}

*/


var newObj_1=new UserDefinedFunction()

alert(Object.getPrototypeOf(newObj_1)===UserDefinedFunction.prototype)  //Displays true

alert(newObj_1.constructor) //Displays function UserDefinedFunction

//Create a new property in UserDefinedFunction.prototype object

UserDefinedFunction.prototype.TestProperty="test"

alert(newObj_1.TestProperty) //Displays "test"

alert(Object.getPrototypeOf(newObj_1).TestProperty)// Displays "test"

//Create a new Object

var objA = {
        property1 : "Property1",
        constructor:Array

}


//assign a new object to UserDefinedFunction.prototype
UserDefinedFunction.prototype=objA

alert(Object.getPrototypeOf(newObj_1)===UserDefinedFunction.prototype)  //Displays false. The object referenced by UserDefinedFunction.prototype has changed

//The internal reference does not change
alert(newObj_1.constructor) // This shall still Display function UserDefinedFunction

alert(newObj_1.TestProperty) //This shall still Display "test" 

alert(Object.getPrototypeOf(newObj_1).TestProperty) //This shall still Display "test"


//Create another object of type UserDefinedFunction
var newObj_2= new UserDefinedFunction();

alert(Object.getPrototypeOf(newObj_2)===objA) //Displays true.

alert(newObj_2.constructor) //Displays function Array()

alert(newObj_2.property1) //Displays "Property1"

alert(Object.getPrototypeOf(newObj_2).property1) //Displays "Property1"

//Create a new property in objA
objA.property2="property2"

alert(objA.property2) //Displays "Property2"

alert(UserDefinedFunction.prototype.property2) //Displays "Property2"

alert(newObj_2.property2) // Displays Property2

alert(Object.getPrototypeOf(newObj_2).property2) //Displays  "Property2"</code></pre>

<p>The prototype chain of every object ultimately traces back to Object.prototype (which itself does not have any prototype object) .
Following code can be used for tracing the prototype chain of an object</p>

<pre><code>var o=Starting object;

do {
    alert(o + "\n" + Object.getOwnPropertyNames(o))

}while(o=Object.getPrototypeOf(o))</code></pre>

<p>The prototype chain for various objects work out as follows.</p>

<ul>
<li>Every Function object (including built in Function object)-&gt;
Function.prototype -&gt; Object.prototype -&gt; null   </li>
<li>Simple Objects (created By new Object() or {} including built in Math  object)-&gt;   Object.prototype -&gt; null</li>
<li>Object created with new or Object.create -&gt; One or More prototype chains -&gt; Object.prototype -&gt; null</li>
</ul>

<p>For creating an object without any prototype use the following:</p>

<pre><code>var o=Object.create(null)
alert(Object.getPrototypeOf(o)) //Displays null</code></pre>

<p>One might think that setting the prototype property of the Constructor to null shall create an object with a null prototype. However in such cases the newly created object's prototype is set to Object.prototype and its constructor is set to function Object. This is demonstrated by the following code</p>

<pre><code>function UserDefinedFunction(){}
UserDefinedFunction.prototype=null// Can be set to any non object value (number,string,undefined etc.)

var o=new UserDefinedFunction()
alert(Object.getPrototypeOf(o)==Object.prototype)   //Displays true
alert(o.constructor)    //Displays Function Object</code></pre>

<p>Following in the summary of this article</p>

<ul>
<li>There are two types of objects <strong>Function types</strong> and <strong>Non Function types</strong></li>
<li><p>Only <strong>Function type objects</strong> can create a new object using the <strong>operator new</strong>. The objects thus created are <strong>Non Function type</strong> objects. The <strong>Non Function type objects</strong> cannot further create an object using <strong>operator new</strong>.</p></li>
<li><p>All <strong>Function type objects</strong> by default have a <strong>"prototype"</strong> property. This <strong>"prototype"</strong> property references an object that has a <strong>"constructor"</strong> property that by default references the <strong>Function type object</strong> itself.  </p></li>
<li><p>All objects (<strong>Function type</strong> and <strong>Non Function type</strong>) have a "constructor" property that by default references the <strong>Function type object</strong>/<strong>Constructor</strong> that created it.</p></li>
<li><p>Every object that gets created internally references the object referenced by
<strong>"prototype"</strong> property of the Constructor that created it. This object is known as the created <strong><em>object's prototype</em></strong> (which is different from Function type objects "prototype" property which it references) . This way the created object can directly access the methods and properties defined in object referenced by the Constructor's "prototype" property (at the time of object creation).</p></li>
<li><p>An <strong>object's prototype</strong> (and hence its inherited property names) can be retrieved using the <strong>Object.getPrototypeOf()</strong>   method. In fact this method 
can be used for navigating the entire prototype chain of the object.</p></li>
<li><p>The prototype chain of every object ultimately traces back to Object.prototype (Unless the object is created using Object.create(null) in which case the object has no prototype).</p></li>
<li><p><strong>typeof(new Array())==='object'</strong> is by design of language and not a mistake as pointed by <a href="http://javascript.crockford.com/survey.html" target="_blank">Douglas Crockford</a>  </p></li>
<li><p>Setting the prototype property of the Constructor to null(or undefined,number,true,false,string) shall not create an object with a null prototype. In such cases the newly created object's prototype is set to Object.prototype and its constructor is set to function Object. </p></li>
</ul>

<p>Hope this helps.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-33523979">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-33323493">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Another attempt to explain <a href="https://github.com/rus0000/jsinheritance" target="_blank">JavaScript prototype-based inheritance</a> with better pictures</p>

<p><a href="https://github.com/rus0000/jsinheritance" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/6gEKe.png" alt="Simple objects inheritanse" /></div></a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-33323493">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-26830003">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Let me tell you my understanding of prototypes. I am not going to compare the inheritance here with other languages. I wish people would stop comparing languages, and just understand the language as itself. Understanding prototypes and prototypal inheritance is so simple, as I will show you below.</p>

<p>Prototype is like a model, based on which you create a product. The crucial point to understand is that when you create an object using another object as it's prototype, the link between the prototype and the product is ever-lasting. For instance:</p>

<pre><code>var model = {x:2};
var product = Object.create(model);
model.y = 5;
product.y
=&gt;5</code></pre>

<p>Every object contains an internal property called the [[prototype]], which can be accessed by the <code>Object.getPrototypeOf()</code> function. <code>Object.create(model)</code> creates a new object and sets it's [[prototype]] property to the object <strong>model</strong>. Hence when you do <code>Object.getPrototypeOf(product)</code>, you will get the object <strong>model</strong>.</p>

<p>Properties in the <strong>product</strong> are handled in the following way:</p>

<ul>
<li>When a property is accessed to just read it's value, its looked up in the scope chain. The search for the variable starts from the <strong>product</strong> upwards to it's prototype. If such a variable is found in the search, the search is stopped right there, and the value is returned. If such a variable cannot be found in the scope chain, undefined is returned.</li>
<li>When a property is written(altered), then the property is always written on the <strong>product</strong> object. If the <strong>product</strong> does not have such a property already, it is implicitly created and written.</li>
</ul>

<p>Such a linking of objects using the prototype property is called prototypal inheritance. There, it is so simple, agree?</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-26830003">
		        <table>
                    <tbody>



    <tr id="comment-42235367">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Not always written on product on assignment. You're not making it very clear that instance specific members have to be initialized and shared members can go on the prototype. Especially when you have instance specific mutable members: <a href="http://stackoverflow.com/questions/16063394/prototypical-inheritance-writing-up/16063711#16063711" title="prototypical inheritance writing up" target="_blank">stackoverflow.com/questions/16063394/…</a>
                    – <a href="/users/1641941/hmr" title="9,566 reputation" target="_blank">HMR</a>
                <a href="#comment42235367_26830003" target="_blank">Nov 9 '14 at 23:43</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-42238653">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                HMR: In your example in your answer, the ben.food.push("Hamburger"); line alters the prototype object's property due to the following: 1.) First ben.food is looked up, and any lookup action will simply lookup the scope  chain. 2.) The push function of that ben.food object is executed. By writing mode in my answer, I mean when you explicitly set a value to it, as in: ben.food = ['Idly']; This will always create a new property(if not already there) on the product object, and then assign the value to it.
                    – <a href="/users/1376717/aravind" title="2,305 reputation" target="_blank">Aravind</a>
                <a href="#comment42238653_26830003" target="_blank">Nov 10 '14 at 3:57</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-42239230">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                HMR: Thank for your comment, it made me think and test my understanding.
                    – <a href="/users/1376717/aravind" title="2,305 reputation" target="_blank">Aravind</a>
                <a href="#comment42239230_26830003" target="_blank">Nov 10 '14 at 4:37</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-42246606">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                When re assigning ben.food it'll shadow the food member unless food is created using Object.defineProperty, Object.defineProperties or Object.create with second argument (so not always). You can even change prototype with (what looks like) a re assignment when you created a getter setter. When it comes to patterns of inheritance I understand the constructor function is hard to understand and has some major problems but it is good if you understand it. Inheritance in JavaScript doesn't begin and end with setting a prototype, initializes (constructors) are to be (re) used as well.
                    – <a href="/users/1641941/hmr" title="9,566 reputation" target="_blank">HMR</a>
                <a href="#comment42246606_26830003" target="_blank">Nov 10 '14 at 10:11</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-42246695">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Your answer is good in explaining prototype but could be mis interpreted by over simplifying inheritance in JavaScript and instance specific members. A lot of questions have been asked why mutating a prototype member on an instance affects other instances.
                    – <a href="/users/1641941/hmr" title="9,566 reputation" target="_blank">HMR</a>
                <a href="#comment42246695_26830003" target="_blank">Nov 10 '14 at 10:14</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-26830003">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>1</b> more comment</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-4778408">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1712
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>In a language implementing classical inheritance like Java, C# or C++ you start by creating a class--a blueprint for your objects--and then you can create new objects from that class or you can extend the class, defining a new class that augments the original class.</p>

<p>In JavaScript you first create an object (there is no concept of class), then you can augment your own object or create new objects from it. It's not difficult, but a little foreign and hard to metabolize for somebody used to the classical way.</p>

<p>Example:</p>

<div>
<div>
<pre><code>//Define a functional object to hold persons in JavaScript
var Person = function(name) {
  this.name = name;
};

//Add dynamically to the already defined object a new getter
Person.prototype.getName = function() {
  return this.name;
};

//Create a new object of type Person
var john = new Person("John");

//Try the getter
alert(john.getName());

//If now I modify person, also John gets the updates
Person.prototype.sayMyName = function() {
  alert('Hello, my name is ' + this.getName());
};

//Call the new method on john
john.sayMyName();</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
<p>Until now I've been extending the base object, now I create another object and then inheriting from Person.</p>

<pre><code>//Create a new object of type Customer by defining its constructor. It's not 
//related to Person for now.
var Customer = function(name) {
    this.name = name;
};

//Now I link the objects and to do so, we link the prototype of Customer to 
//a new instance of Person. The prototype is the base that will be used to 
//construct all new instances and also, will modify dynamically all already 
//constructed objects because in JavaScript objects retain a pointer to the 
//prototype
Customer.prototype = new Person();     

//Now I can call the methods of Person on the Customer, let's try, first 
//I need to create a Customer.
var myCustomer = new Customer('Dream Inc.');
myCustomer.sayMyName();

//If I add new methods to Person, they will be added to Customer, but if I
//add new methods to Customer they won't be added to Person. Example:
Customer.prototype.setAmountDue = function(amountDue) {
    this.amountDue = amountDue;
};
Customer.prototype.getAmountDue = function() {
    return this.amountDue;
};

//Let's try:       
myCustomer.setAmountDue(2000);
alert(myCustomer.getAmountDue());</code></pre>

<div><div><p><a target="_blank">Show code snippet</a></p></div>

</div>
<p>While as said I can't call setAmountDue(), getAmountDue() on a Person.</p>

<pre><code>//The following statement generates an error.
john.setAmountDue(1000);</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-4778408">
		        <table>
                    <tbody>



    <tr id="comment-5293872">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                331
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I think the answers on stackoverflow are not only interesting to the original poster, but also to a big community of other people lurking or coming from searches. And I've been one of them and I had benefit from old posts. I think I could contribute to the other answers adding some code examples.   About your question: if you leave out the new, it doesn't work. when I call myCustomer.sayMyName() it returns "myCustomer.sayMyName is not a function". The easiest way is experiment with firebug and see what happens.
                    – <a href="/users/445543/stivlo" title="52,524 reputation" target="_blank">stivlo</a>
                <a href="#comment5293872_4778408" target="_blank">Jan 24 '11 at 9:52</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-5305792">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                6
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                As far as I understand  var Person = function (name) {...}; is defining a constructor function capable of building Person Objects. So there is no Object yet, only the anonymous constructor function is assigned to Person. This is a very good explanation:  <a href="http://helephant.com/2008/08/how-javascript-objects-work/" target="_blank">helephant.com/2008/08/how-javascript-objects-work</a>
                    – <a href="/users/445543/stivlo" title="52,524 reputation" target="_blank">stivlo</a>
                <a href="#comment5305792_4778408" target="_blank">Jan 25 '11 at 3:30</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-29686501">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                14
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                WARNING: This answer neglects the fact that the parent class constructor is not called on a per instance basis.  The only reason it works is because he did the exact same thing (setting the name) in both the child and parent constructor.  For a more in depth explanation on common mistakes made when attempting inheritance in JavaScript (and a final solution), please see:  <a href="http://stackoverflow.com/questions/14564155/javascript-prototypal-inheritance-descendants-override-each-other/14576273#14576273" target="_blank">this stack overflow post</a>
                    – <a href="/users/2020258/goofyguy763" title="444 reputation" target="_blank">goofyguy763</a>
                <a href="#comment29686501_4778408" target="_blank">Nov 13 '13 at 6:26</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-33238876">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I notice that this answer also doesn't mention that by using "new Person()" as the prototype, you are actually setting the "name" instance property of "Person" to be a static property of "Customer" (so all Customer instances will have the same property). While it's a good basic example, DON'T DO THAT. :)  Create a new anonymous function to act as a "bridge" by setting it's prototype to "Person.prototype", then create an instance from it and set "Customer.prototype" to that anonymous instance instead.
                    – <a href="/users/1236397/james-wilkins" title="2,500 reputation" target="_blank">James Wilkins</a>
                <a href="#comment33238876_4778408" target="_blank">Feb 21 '14 at 17:53</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-40011280">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                10
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                About the <code>Customer.prototype = new Person();</code> line, MDN shows an example using <code>Customer.prototype = Object.create(Person.prototype)</code>, and states that <i>'A common error here is to use "new Person()"'</i>. <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript" target="_blank">source</a>
                    – <a href="/users/1717979/rafael-eyng" title="2,081 reputation" target="_blank">Rafael Eyng</a>
                <a href="#comment40011280_4778408" target="_blank">Sep 1 '14 at 20:24</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-4778408">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>10</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-21763808">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        152
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p><em>I play a role as a JavaScript teacher and the prototype concept has always been a controversial topic to cover when I teach. It took me a while to come up with a good method to clarify the concept, and now in this text I'm gonna be trying to explain How does JavaScript .prototype work.</em></p>

<hr />

<p>This is a very simple prototype based object model that would be considered as a sample during the explanation, with no comment yet:</p>

<pre><code>function Person(name){
    this.name = name;
}
Person.prototype.getName = function(){
    console.log(this.name);
}
var person = new Person("George");</code></pre>

<hr />

<p>There are some crucial points that we have to consider before going through the prototype concept.</p>

<h1>1- How JavaScript functions actually work:</h1>

<p>To take the first step we have to figure out, how JavaScript functions actually work , as a class like function using <strong><code>this</code></strong> keyword in it or just as a regular function with its arguments, what it does and what it returns.</p>

<p>Let's say we want to create a <code>Person</code> object model. but in this step I'm gonna be trying to <strong>do the same exact thing without using <code>prototype</code> and <code>new</code> keyword</strong>.</p>

<p>So in this step <strong><code>functions</code></strong>, <strong><code>objects</code></strong> and <strong><code>this</code></strong> keyword, are all we have.</p>

<p>The first question would be <strong>how <code>this</code> keyword could be useful without using <code>new</code> keyword</strong>.</p>

<p>So to answer that let's say we have an empty object, and two functions like:</p>

<pre><code>var person = {};
function Person(name){  this.name = name;  }

function getName(){
    console.log(this.name);
}</code></pre>

<p>and now <strong>without using <code>new</code> keyword</strong> how we could use these functions. So JavaScript has 3 different ways to do that:</p>

<h2>a. first way is just to call the function as a regular function:</h2>

<pre><code>Person("George");
getName();//would print the "George" in the console</code></pre>

<p>in this case, this would be the current context object, which is usually is the global  <code>window</code> object in the browser or <code>GLOBAL</code> in <code>Node.js</code>. It means we would have, window.name in browser or GLOBAL.name in Node.js, with "George" as its value.</p>

<h2>b. We can <strong>attach</strong> them to an object, as its properties</h2>

<p>-<strong>The easiest way</strong> to do this is modifying the empty <code>person</code> object, like:</p>

<pre><code>person.Person = Person;
person.getName = getName;</code></pre>

<p>this way we can call them like:</p>

<pre><code>person.Person("George");
person.getName();// --&gt;"George"</code></pre>

<p>and now the <code>person</code> object is like:</p>

<pre><code>Object {Person: function, getName: function, name: "George"}</code></pre>

<hr />

<p>-<strong>The other way to attach a property</strong> to an object is using the <code>prototype</code> of that object that can be find in any JavaScript object with the name of <code>__proto__</code>, and I have tried to explain it a bit on the summary part. So we could get the similar result by doing:</p>

<pre><code>person.__proto__.Person = Person;
person.__proto__.getName = getName;</code></pre>

<p><strong>But</strong> this way what we actually are doing is modifying the <code>Object.prototype</code>, because whenever we create a JavaScript object using literals (<code>{ ... }</code>), it gets created based on <code>Object.prototype</code>, which means it gets attached to the newly created object as an attribute named <strong><code>__proto__</code></strong> , so if we change it, as we have done on our previous code snippet, all the JavaScript objects would get changed, not a good practice. So what could be the better practice now:</p>

<pre><code>person.__proto__ = {
    Person: Person,
    getName: getName
};</code></pre>

<p>and now other objects are in peace, but it still doesn't seem to be a good practice. So we have still one more solutions, but to use this solution we should get back to that line of code where <code>person</code> object got created (<code>var person = {};</code>) then change it like:</p>

<pre><code>var propertiesObject = {
    Person: Person,
    getName: getName
};
var person = Object.create(propertiesObject);</code></pre>

<p>what it does is creating a new JavaScript <code>Object</code> and attach the <code>propertiesObject</code> to the <code>__proto__</code> attribute. So to make sure you can do:</p>

<pre><code>console.log(person.__proto__===propertiesObject); //true</code></pre>

<p>But the tricky point here is you have access to all the properties defined in <code>__proto__</code> on the first level of the <code>person</code> object(read the summary part for more detail).</p>

<hr />

<p>as you see using any of these two way <code>this</code> would exactly point to the <code>person</code> object.</p>

<h2>c. JavaScript has another way to provide the function with <code>this</code>, which is using <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call" target="_blank">call</a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply" target="_blank">apply</a> to invoke the function.</h2>

<blockquote>
  <p>The apply() method calls a function with a given this value and
  arguments provided as an array (or an array-like object).</p>
</blockquote>



<blockquote>
  <p>The call() method calls a function with a given this value and
  arguments provided individually.</p>
</blockquote>

<p>this way which is my favorite, we can easily call our functions like:</p>

<pre><code>Person.call(person, "George");</code></pre>



<pre><code>//apply is more useful when params count is not fixed
Person.apply(person, ["George"]);

getName.call(person);   
getName.apply(person);</code></pre>

<p>these 3 methods are the important initial steps to figure out the .prototype functionality.</p>

<hr />

<h1>2- How does the <code>new</code> keyword works?</h1>

<p>this is the second step to understand the <code>.prototype</code> functionality.this is what I use to simulate the process:</p>

<pre><code>function Person(name){  this.name = name;  }
my_person_prototype = { getName: function(){ console.log(this.name); } };</code></pre>

<p>in this part I'm gonna be trying to take all the steps which JavaScript takes, without using the <code>new</code> keyword and <code>prototype</code>, when you use <code>new</code> keyword. so when we do <code>new Person("George")</code>, <code>Person</code> function serves as a constructor, These are what JavaScript does, one by one:</p>

<h2>a. first of all it makes an empty object, basically an empty hash like:</h2>

<pre><code>var newObject = {};</code></pre>

<h2>b. the next step that JavaScript takes is to <strong>attach</strong> the all prototype objects to the newly created object</h2>

<p>we have <code>my_person_prototype</code> here similar to the prototype object.</p>

<pre><code>for(var key in my_person_prototype){
    newObject[key] = my_person_prototype[key];
}</code></pre>

<p>It is not the way that JavaScript actually attaches the properties that are defined in the prototype. The actual way is related to the prototype chain concept.</p>

<hr />

<h2>a. & b. Instead of these two steps you can have the exact same result by doing:</h2>

<pre><code>var newObject = Object.create(my_person_prototype);
//here you can check out the __proto__ attribute
console.log(newObject.__proto__ === my_person_prototype); //true
//and also check if you have access to your desired properties
console.log(typeof newObject.getName);//"function"</code></pre>

<p>now we can call the <code>getName</code> function in our <code>my_person_prototype</code>:</p>

<pre><code>newObject.getName();</code></pre>

<h2>c. then it gives that object to the constructor,</h2>

<p>we can do this with our sample like:</p>

<pre><code>Person.call(newObject, "George");</code></pre>



<pre><code>Person.apply(newObject, ["George"]);</code></pre>

<p>then the constructor can do whatever it wants, because <strong>this</strong> inside of that constructor is the object that was just created.</p>

<p>now the end result before simulating the other steps:
    Object {name: "George"}</p>

<hr />

<h2>Summary:</h2>

<p>Basically, when you use the <strong>new</strong> keyword on a function, you are calling on that and that function serves as a constructor, so when you say:</p>

<pre><code>new FunctionName()</code></pre>

<p>JavaScript internally makes an object, an empty hash and then it gives that object to the constructor, then the constructor can do whatever it wants, because <strong>this</strong> inside of that constructor is the object that was just created and then it gives you that object of course if you haven't used the return statement in your function or if you've put a <code>return undefined;</code> at the end of your function body.</p>

<p>So when JavaScript goes to look up a property on an object, the first thing it does, is it looks it up on that object. And then there is a secret property <strong><code>[[prototype]]</code></strong> which we usually have it like <strong><code>__proto__</code></strong> and that property is what JavaScript looks at next. And when it looks through the <strong><code>__proto__</code></strong>, as far as it is again another JavaScript object, it has its own <strong><code>__proto__</code></strong> attribute, it goes up and up until it gets to the point where the next <strong><code>__proto__</code></strong> is null. The point is the only object in JavaScript that its <strong><code>__proto__</code></strong> attribute is null is <code>Object.prototype</code> object:</p>

<pre><code>console.log(Object.prototype.__proto__===null);//true</code></pre>

<p>and that's how inheritance works in JavaScript.</p>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/JnpBV.png" alt="The prototype chain" /></div></p>

<p>In other words, when you have a prototype property on a function and you call a new on that, after JavaScript finishes looking at that newly created object for properties, it will go look at the function's <code>.prototype</code> and also it is possible that this object has its own internal prototype. and so on.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-21763808">
		        <table>
                    <tbody>



    <tr id="comment-32922717">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                4
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                a) Please don't explain prototypes by copying properties b) Setting the internal <i>[[prototype]]</i> happens before the constructor function is applied on the instance, please change that order c) jQuery is totally offtopic in this question
                    – <a href="/users/1048572/bergi" title="298,285 reputation" target="_blank">Bergi</a>
                <a href="#comment32922717_21763808" target="_blank">Feb 13 '14 at 19:42</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-32924233">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @Bergi: thanks for pointing out, I'd be appreciated if you let me know if that's ok now.
                    – <a href="/users/2877719/mehran-hatami" title="8,193 reputation" target="_blank">Mehran Hatami</a>
                <a href="#comment32924233_21763808" target="_blank">Feb 13 '14 at 20:27</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-34880684">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                6
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Can you please make it simple? You are right on all points, but students who read this explanation may be really confused for the first time. pick up any simpler example, and let the code explain itself or add a bunch of comments to clarify what you mean.
                    – <a href="/users/132610/p-m" title="1,563 reputation" target="_blank">P.M</a>
                <a href="#comment34880684_21763808" target="_blank">Apr 4 '14 at 12:40</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-34884054">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @P.M: Thanks for your feedback. I've tried to make it as simple as possible but I think you are right it has still some vague points. So I will try to modify it and also be more descriptive. :)
                    – <a href="/users/2877719/mehran-hatami" title="8,193 reputation" target="_blank">Mehran Hatami</a>
                <a href="#comment34884054_21763808" target="_blank">Apr 4 '14 at 13:58</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-40909772">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                +1 for the illustration at the end of your "book" :)
                    – <a href="/users/2251437/sargas" title="1,585 reputation" target="_blank">sargas</a>
                <a href="#comment40909772_21763808" target="_blank">Sep 29 '14 at 16:56</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-21763808">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>4</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-19483767">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        11
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I found it helpful to explain the "prototype chain" as recursive convention when <code>obj_n.prop_X</code> is being referenced:</p>

<p>if <code>obj_n.prop_X</code> doesn't exist, check <code>obj_n+1.prop_X</code> where <code>obj_n+1 = obj_n.[[prototype]]</code></p>

<p>If the <code>prop_X</code> is finally found in the k-th prototype object then</p>

<p><code>obj_1.prop_X = obj_1.[[prototype]].[[prototype]]..(k-times)..[[prototype]].prop_X</code></p>

<p>You can find a graph of the relation of Javascript objects by their properties here:</p>

<p> <div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/2tGyY.jpg" alt="js objects graph" /></div> </p>

<p><a href="http://jsobjects.org" target="_blank">http://jsobjects.org</a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-19483767">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-13267099">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        56
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>After reading this thread, I feel confused with JavaScript Prototype Chain, then I found these charts </p>

<p><a href="http://iwiki.readthedocs.org/en/latest/javascript/js_core.html#inheritance" target="_blank">http://iwiki.readthedocs.org/en/latest/javascript/js_core.html#inheritance</a>
<div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/rcGmc.png" alt="*[[protytype]]* and <code>prototype</code> property of function objects" /></div></p>

<p><em>it's a clear chart to show JavaScript Inheritance by Prototype Chain</em></p>



<p><a href="http://www.javascriptbank.com/javascript/article/JavaScript_Classical_Inheritance/" target="_blank">http://www.javascriptbank.com/javascript/article/JavaScript_Classical_Inheritance/</a></p>

<p><em>this one contains a example with code and several nice diagrams.</em></p>

<blockquote>
  <p>prototype chain ultimately falls back to Object.prototype. </p>
  
  <p>prototype chain can be technically extended as long as you want, each time by setting the prototype of the subclass equal to an object of the parent class.</p>
</blockquote>

<p>Hope it's also helpful for you to understand JavaScript Prototype Chain.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-13267099">
		        <table>
                    <tbody>



    <tr id="comment-18083010">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                It would be great if you could provide a short abstract of the contents of the links so this answer is still usefull when the links are dead.
                    – <a href="/users/682559/nicktar" title="3,363 reputation" target="_blank">Nicktar</a>
                <a href="#comment18083010_13267099" target="_blank">Nov 7 '12 at 10:08</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-18107469">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @Nicktar, Thanks for your suggestion, I have added simple description by these links.
                    – <a href="/users/1254006/rockxrock" title="2,737 reputation" target="_blank">rockXrock</a>
                <a href="#comment18107469_13267099" target="_blank">Nov 8 '12 at 3:10</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-29290462">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                276
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            
        </td>
    </tr>
    <tr id="comment-38144609">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                A diagram speaks a thousand words. This is so useful :)
                    – <a href="/users/1141160/mark-robson" title="620 reputation" target="_blank">Mark Robson</a>
                <a href="#comment38144609_13267099" target="_blank">Jul 7 '14 at 16:35</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-41797565">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Can you explain what <code>[[Prototype]]</code> means?
                    – <a href="/users/1675976/codybugstein" title="5,259 reputation" target="_blank">CodyBugstein</a>
                <a href="#comment41797565_13267099" target="_blank">Oct 27 '14 at 15:44</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-13267099">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>5</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-2209489">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        10
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>When a constructor creates an object, that object implicitly references the constructor’s “prototype” property for the purpose of resolving property references. The constructor’s “prototype” property can be referenced by the program expression constructor.prototype, and properties added to an object’s prototype are shared, through inheritance, by all objects sharing the prototype.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Feb 5 '10 at 18:42
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-2209489">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-572904">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        65
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p><code>prototype</code> allows you to make classes. if you do not use <code>prototype</code> then it becomes a static.</p>

<p>Here is a short example.</p>

<pre><code>var obj = new Object();
obj.test = function() { alert('Hello?'); };</code></pre>

<p>In the above case, you have static funcation call test. This function can be accessed only by obj.test where you can imagine obj to be a class.</p>

<p>where as in the below code</p>

<pre><code>function obj()
{
}

obj.prototype.test = function() { alert('Hello?'); };
var obj2 = new obj();
obj2.test();</code></pre>

<p>The obj has become a class which can now be instantiated. Multiple instances of obj can exist and they all have the <code>test</code> function.</p>

<p>The above is my understanding. I am making it a community wiki, so people can correct me if I am wrong.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-572904">
		        <table>
                    <tbody>



    <tr id="comment-384688">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                12
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                -1: <code>prototype</code> is a property of constructor functions, not instances, ie your code is wrong! Perhaps you meant the non-standard property <code>__proto__</code> of objects, but that's a whole different beast...
                    – <a href="/users/48015/christoph" title="116,145 reputation" target="_blank">Christoph</a>
                <a href="#comment384688_572904" target="_blank">Feb 21 '09 at 13:25</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-384722">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @Christoph - Thanks for pointing it out. I have updated the sample code.
                    – <a href="/users/30594/ramesh" title="9,165 reputation" target="_blank">Ramesh</a>
                <a href="#comment384722_572904" target="_blank">Feb 21 '09 at 13:52</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-384778">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                4
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This a sort of good answer, but there's more to it.
                    – <a href="/users/58961/john-leidegren" title="33,506 reputation" target="_blank">John Leidegren</a>
                <a href="#comment384778_572904" target="_blank">Feb 21 '09 at 14:22</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-384841">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                There's so much more to it... Plus JavaScript is not a class-based language - it deals with inheritance via prototypes, you need to cover the differences in more detail!
                    – <a href="/users/21677/james" title="84,515 reputation" target="_blank">James</a>
                <a href="#comment384841_572904" target="_blank">Feb 21 '09 at 15:00</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-23126493">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                5
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I think this answer is a little misguiding.
                    – <a href="/users/575185/armin-cifuentes" title="405 reputation" target="_blank">Armin Cifuentes</a>
                <a href="#comment23126493_572904" target="_blank">Apr 23 '13 at 20:33</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-572904">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>2</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-572913">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        22
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Javascript doesn't have inheritance in the usual sense, but it has the prototype chain.</p>

<h2>prototype chain</h2>

<p>If a member of an object can't be found in the object it looks for it in the prototype chain. The chain consists of other objects. The prototype of a given instance can be accessed with the <code>__proto__</code> variable. Every object has one, as there is no difference between classes and instances in javascript.</p>

<p>The advantage of adding a function / variable to the prototype is that it has to be in the memory only once, not for every instance.</p>

<p>It's also useful for inheritance, because the prototype chain can consist of many other objects.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Feb 21 '09 at 12:41
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-572913">
		        <table>
                    <tbody>



    <tr id="comment-384642">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                FF and Chrome supports <b>proto</b>, but not IE nor Opera.
                    – <a href="/users/36866/some" title="31,618 reputation" target="_blank">some</a>
                <a href="#comment384642_572913" target="_blank">Feb 21 '09 at 12:44</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-18103893">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Georg, please clarify for a noob - "there is no difference between classes and instances in javascript." - could you elaborate? How does this work?
                    – <a href="/users/231677/hamish-grubijan" title="3,820 reputation" target="_blank">Hamish Grubijan</a>
                <a href="#comment18103893_572913" target="_blank">Nov 7 '12 at 23:03</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-68630725">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                from the all discussion what i get(came from classical inheritance) if i create constructor function and try to create instance of it using new operator i will only get methods and properties that was attach to proto object, therefore its necessary to attach all the method and properties to proto object if we want to inherit, m i right?
                    – <a href="/users/5710014/blackhawk" title="1,105 reputation" target="_blank">blackHawk</a>
                <a href="#comment68630725_572913" target="_blank">Nov 20 '16 at 5:36</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-572913">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-572905">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        16
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<blockquote>
  <p>what is the exact purpose of this ".prototype" property?</p>
</blockquote>

<p>The interface to standard classes become extensible. For example, you are using the <code>Array</code> class and you also need to add a custom serializer for all your array objects. Would you spend time coding up a subclass, or use composition or ... The prototype property solves this by letting the users control the exact set of members/methods available to a class.</p>

<p>Think of prototypes as an extra vtable-pointer. When some members are missing from the original class, the prototype is looked up at runtime.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Feb 21 '09 at 12:37
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-572905">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/prototype-oriented" title="show questions tagged 'prototype-oriented'" target="_blank">prototype-oriented</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
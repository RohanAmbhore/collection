<a href="https://stackoverflow.com/questions/359494/which-equals-operator-vs-should-be-used-in-javascript-comparisons">https://stackoverflow.com/questions/359494/which-equals-operator-vs-should-be-used-in-javascript-comparisons</a><div id="articleHeader"><h1>Which equals operator (== vs ===) should be used in JavaScript comparisons?</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        5370
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>1617</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I'm using <a href="http://en.wikipedia.org/wiki/JSLint" target="_blank">JSLint</a> to go through JavaScript, and it's returning many suggestions to replace <code>==</code> (two equals signs) with <code>===</code> (three equals signs) when doing things like comparing <code>idSele_UNVEHtype.value.length == 0</code> inside of an <code>if</code> statement.</p>

<p>Is there a performance benefit to replacing <code>==</code> with <code>===</code>? </p>

<p>Any performance improvement would be welcomed as many comparison operators exist.</p>

<p>If no type conversion takes place, would there be a performance gain over <code>==</code>?</p>
    </div>
    
    <div>
    

    
    <div>
        <div>
    <div>
        asked Dec 11 '08 at 14:19
    </div>
    
    
</div>
    </div>
    </div>
</div>

                        <div>
                <div>
        <h2>                    <b>protected</b> by <a href="/users/19068/quentin" target="_blank">Quentin</a> Oct 4 '12 at 12:53
</h2>
        <p>
This question is protected to prevent "thanks!", "me too!", or spam answers by new users. 
To answer it, you must have earned at least 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).</p>
    </div>
            </div>
    
    <div>
	    <div id="comments-359494">
                <ul>



    <li id="comment-5014385">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
    <li id="comment-14900957">
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
                Just in case anyone was wondering in 2012: <code>===</code> is <i>way</i> faster than <code>==</code>. <a href="http://jsperf.com/comparison-of-comparisons" target="_blank">jsperf.com/comparison-of-comparisons</a>
                    – <a href="/users/707111/ryan" title="154,680 reputation" target="_blank">Ryan♦</a>
                <a href="#comment14900957_359494" target="_blank">Jul 3 '12 at 23:02</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-15170186">
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
                @minitech it should be as it does not do type conversion
                    – <a href="/users/825780/umur-kontac%c4%b1" title="31,816 reputation" target="_blank">Umur Kontacı</a>
                <a href="#comment15170186_359494" target="_blank">Jul 14 '12 at 19:10</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-19377732">
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
                @minitech, I doubt anyone is going to make their application noticeably faster by using <code>===</code> over <code>==</code>. In fact, the benchmark doesn't show a big difference between both on modern browsers. Personally, I usually use <code>==</code> everywhere unless I really need strict equality.
                    – <a href="/users/561309/this-lau" title="48,159 reputation" target="_blank">this.lau_</a>
                <a href="#comment19377732_359494" target="_blank">Dec 25 '12 at 9:09</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-23081314">
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
                @johndodo: Premature Optimization is only a thing because optimized code can be less ideal from a maintainability and readability standpoint, but if the type conversion features of <code>==</code> are not needed, the use of <code>===</code> instead is good practice, not premature optimization.  There's nothing about <code>===</code> that degrades code maintainability or readability.
                    – <a href="/users/102937/robert-harvey" title="140,744 reputation" target="_blank">Robert Harvey♦</a>
                <a href="#comment23081314_359494" target="_blank">Apr 22 '13 at 17:48</a>
                        
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>        </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-359509">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5366
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>The identity (<code>===</code>) operator behaves identically to the equality (<code>==</code>) operator except no type conversion is done, and the types must be the same to be considered equal.</p>

<p>Reference: <a href="http://www.c-point.com/javascript_tutorial/jsgrpComparison.htm" target="_blank">Javascript Tutorial: Comparison Operators</a></p>

<p>The <code>==</code> operator will compare for equality <em>after doing any necessary type conversions</em>.  The <code>===</code> operator will <strong>not</strong> do the conversion, so if two values are not the same type <code>===</code> will simply return <code>false</code>. Both are equally quick.</p>

<p>To quote Douglas Crockford's excellent <a href="https://rads.stackoverflow.com/amzn/click/0596517742" target="_blank">JavaScript: The Good Parts</a>,</p>

<blockquote>
  <p>JavaScript has two sets of equality operators: <code>===</code> and <code>!==</code>, and their evil twins <code>==</code> and <code>!=</code>.  The good ones work the way you would expect.  If the two operands are of the same type and have the same value, then <code>===</code> produces <code>true</code> and <code>!==</code> produces <code>false</code>.  The evil twins do the right thing when the operands are of the same type, but if they are of different types, they attempt to coerce the values.  the rules by which they do that are complicated and unmemorable.  These are some of the interesting cases:</p>

<pre><code>'' == '0'           // false
0 == ''             // true
0 == '0'            // true

false == 'false'    // false
false == '0'        // true

false == undefined  // false
false == null       // false
null == undefined   // true

' \t\r\n ' == 0     // true</code></pre>
  
  <p>The lack of transitivity is alarming.  My advice is to never use the evil twins.  Instead, always use <code>===</code> and <code>!==</code>.  All of the comparisons just shown produce <code>false</code> with the <code>===</code> operator.</p>
</blockquote>

<hr />

<h3>Update:</h3>

<p>A good point was brought up by <a href="https://stackoverflow.com/users/165495/casebash" target="_blank">@Casebash</a> in the comments and in <a href="https://stackoverflow.com/users/113570/philippe-leybaert" target="_blank">@Phillipe Laybaert's</a> <a href="https://stackoverflow.com/a/957602/1288" target="_blank">answer</a> concerning reference types.  For reference types <code>==</code> and <code>===</code> act consistently with one another (except in a special case).</p>

<pre><code>var a = [1,2,3];
var b = [1,2,3];

var c = { x: 1, y: 2 };
var d = { x: 1, y: 2 };

var e = "text";
var f = "te" + "xt";

a == b            // false
a === b           // false

c == d            // false
c === d           // false

e == f            // true
e === f           // true</code></pre>

<p>The special case is when you compare a literal with an object that evaluates to the same literal, due to its <code>toString</code> or <code>valueOf</code> method. For example, consider the comparison of a string literal with a string object created by the <code>String</code> constructor.</p>

<pre><code>"abc" == new String("abc")    // true
"abc" === new String("abc")   // false</code></pre>

<p>Here the <code>==</code> operator is checking the values of the two objects and returning <code>true</code>, but the <code>===</code> is seeing that they're not the same type and returning <code>false</code>.  Which one is correct?  That really depends on what you're trying to compare.  My advice is to bypass the question entirely and just don't use the <code>String</code> constructor to create string objects.</p>

<p><strong>Reference</strong><br />
<a href="http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3" target="_blank">http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3</a></p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-359509">
                <ul>



    <li id="comment-227431">
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
                === is not quicker if the types are the same.  If types are not the same, === will be quicker because it won't try to do the conversion.
                    – <a href="/users/1288/bill-the-lizard" title="266,799 reputation" target="_blank">Bill the Lizard</a>
                <a href="#comment227431_359509" target="_blank">Dec 31 '08 at 3:02</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-317360">
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
                === will never be slower than ==.  They both do type checking, so === doesn't do anything extra compared to ==, but the type check may allow === to exit sooner when types are not the same.
                    – <a href="/users/1288/bill-the-lizard" title="266,799 reputation" target="_blank">Bill the Lizard</a>
                <a href="#comment317360_359509" target="_blank">Feb 2 '09 at 4:17</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-2553541">
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
                Replacing all ==/!= with ===/!== increases the size of the js file, it will take then more time to load. :)
                    – <a href="/users/260080/marco-demaio" title="18,090 reputation" target="_blank">Marco Demaio</a>
                <a href="#comment2553541_359509" target="_blank">Mar 31 '10 at 9:22</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-10443007">
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
                "...the rules by which they do that are complicated and unmemorable..." Now such statements make you feel so safe when programming...
                    – <a href="/users/122977/johan" title="603 reputation" target="_blank">Johan</a>
                <a href="#comment10443007_359509" target="_blank">Dec 9 '11 at 16:24</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-18108077">
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
                Sometimes JavaScript's type system makes me want to run away screaming.
                    – <a href="/users/20371/yawar" title="6,054 reputation" target="_blank">Yawar</a>
                <a href="#comment18108077_359509" target="_blank">Nov 8 '12 at 4:06</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-359547">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        927
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Using the <code>==</code> operator (<em>Equality</em>)</p>

<pre><code>true == 1; //true, because 'true' is converted to 1 and then compared
"2" == 2;  //true, because "2" is converted to 2 and then compared</code></pre>

<p>Using the <code>===</code> operator (<em>Identity</em>)</p>

<pre><code>true === 1; //false
"2" === 2;  //false</code></pre>

<p>This is because the <strong>equality operator <code>==</code> does type coercion</strong>, meaning that the interpreter implicitly tries to convert the values before comparing.</p>

<p>On the other hand, the <strong>identity operator <code>===</code> does not do type coercion</strong>, and thus does not convert the values when comparing.</p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-359547">
                <ul>



    <li id="comment-766543">
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
                @Software Monkey: not for value types (number, boolean, ...)
                    – <a href="/users/113570/philippe-leybaert" title="119,708 reputation" target="_blank">Philippe Leybaert</a>
                <a href="#comment766543_359547" target="_blank">Jun 5 '09 at 20:00</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-43992813">
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
                Since nobody has mentioned the Javascript Equality Table, here it is: <a href="http://dorey.github.io/JavaScript-Equality-Table/" target="_blank">dorey.github.io/JavaScript-Equality-Table</a>
                    – <a href="/users/710805/blaze" title="1,088 reputation" target="_blank">blaze</a>
                <a href="#comment43992813_359547" target="_blank">Jan 6 '15 at 3:17</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-68703667">
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
                In the first statement, are you sure that 'true' is converted to 1 and not 1 converted to true?
                    – <a href="/users/3380497/shadi-namrouti" title="1,092 reputation" target="_blank">Shadi Namrouti</a>
                <a href="#comment68703667_359547" target="_blank">Nov 22 '16 at 10:05</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-359588">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        30
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>There is unlikely to be any performance difference between the two operations in your usage. There is no type-conversion to be done because both parameters are already the same type. Both operations will have a type comparison followed by a value comparison.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 11 '08 at 14:44
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-359629">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        65
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>The <strong>===</strong> operator is called a strict comparison operator, it <strong>does</strong> differ from the <strong>==</strong> operator.</p>

<p>Lets take 2 vars a and b.</p>

<p>For <strong>"a == b"</strong> to evaluate to true a and b need to be the <strong>same value</strong>.</p>

<p>In the case of <strong>"a === b"</strong> a and b must be the <strong>same value</strong> and also the <strong>same type</strong> for it to evaluate to true.  </p>

<p>Take the following example</p>

<pre><code>var a = 1;
var b = "1";

if (a == b) //evaluates to true as a and b are both 1
{
    alert("a == b");
}

if (a === b) //evaluates to false as a is not the same type as b
{
    alert("a === b");
}</code></pre>

<p><strong>In summary</strong>; using the <strong>==</strong> operator might evaluate to true in situations where you do not want it to so using the <strong>===</strong> operator would be safer.  </p>

<p>In the 90% usage scenario it won't matter which one you use, but it is handy to know the difference when you get some unexpected behaviour one day.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-371472">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        41
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>In a typical script there will be no performance difference. More important may be the fact that thousand "===" is 1 KB heavier than thousand "==" :) <a href="https://stackoverflow.com/questions/tagged/javascript+performance" target="_blank">JavaScript profilers</a> can tell you if there is a performance difference in your case.</p>

<p>But personally I would do what JSLint suggests. This recommendation is there not because of performance issues, but because type coercion means <code>('\t\r\n' == 0)</code> is true.</p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-371472">
                <ul>



    <li id="comment-840044">
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
                Not always true. With gzip compression, the difference would be almost negligible.
                    – <a href="/users/68210/daniel-x-moore" title="9,530 reputation" target="_blank">Daniel X Moore</a>
                <a href="#comment840044_371472" target="_blank">Jun 22 '09 at 23:43</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-66806387">
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
                Agree, but thousand "===" means also 10 thousands of code lines else so 1kb more or less... ;)
                    – <a href="/users/4313697/jonny" title="167 reputation" target="_blank">Jonny</a>
                <a href="#comment66806387_371472" target="_blank">Sep 28 '16 at 18:32</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-392748">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        79
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I tested this in Firefox with <a href="http://en.wikipedia.org/wiki/Firebug_%28software%29" target="_blank">Firebug</a> using code like this:</p>

<pre><code>console.time("testEquality");
var n = 0;
while(true) {
    n++;
    if(n==100000) 
        break;
}
console.timeEnd("testEquality");</code></pre>



<pre><code>console.time("testTypeEquality");
var n = 0;
while(true) {
    n++;
    if(n===100000) 
        break;
}
console.timeEnd("testTypeEquality");</code></pre>

<p>My results (tested five times each and averaged):</p>

<pre><code>==: 115.2
===: 114.4</code></pre>

<p>So I'd say that the miniscule difference (this is over 100000 iterations, remember) is negligible. Performance <strong><em>isn't</em></strong> a reason to do <code>===</code>. Type safety (well, as safe as you're going to get in JavaScript), and code quality is.</p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-392748">
                <ul>



    <li id="comment-8951872">
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
                More than type safety you want logical correctness - sometimes you want things to be truthy when <code>==</code> disagrees.
                    – <a href="/users/151195/rpjohnst" title="877 reputation" target="_blank">rpjohnst</a>
                <a href="#comment8951872_392748" target="_blank">Sep 13 '11 at 21:14</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-25675841">
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
                Now, how do these compare when there is an actual type coersion for <code>==</code> operator? Remember, that's when there's a performance boost.
                    – <a href="/users/876409/hubert-og" title="15,225 reputation" target="_blank">Hubert OG</a>
                <a href="#comment25675841_392748" target="_blank">Jul 13 '13 at 21:13</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-397583">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        17
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>The problem is that you might easily get into trouble since JavaScript have a lot of implicit conversions meaning...</p>

<pre><code>var x = 0;
var isTrue = x == null;
var isFalse = x === null;</code></pre>

<p>Which pretty soon becomes a problem. The best sample of why implicit conversion is "evil" can be taken from this code in <a href="http://en.wikipedia.org/wiki/Microsoft_Foundation_Class_Library" target="_blank">MFC</a> / C++ which actually will compile due to an implicit conversion from CString to HANDLE which is a pointer typedef type...</p>

<pre><code>CString x;
delete x;</code></pre>

<p>Which obviously during runtime does <em>very</em> undefined things...</p>

<p>Google for implicit conversions in C++ and <a href="http://en.wikipedia.org/wiki/Standard_Template_Library" target="_blank">STL</a> to get some of the arguments against it...</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-957602">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        508
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>In the answers here, I didn't read anything about what <strong>equal</strong> means. Some will say that <code>===</code> means <strong>equal and of the same type</strong>, but that's not really true. It actually means that <strong>both operands reference the same object</strong>, or in case of <strong>value types, have the same value</strong>.</p>

<p>So, let's take the following code:</p>

<pre><code>var a = [1,2,3];
var b = [1,2,3];
var c = a;

var ab_eq = (a === b); // false (even though a and b are the same type)
var ac_eq = (a === c); // true</code></pre>

<p>The same here:</p>

<pre><code>var a = { x: 1, y: 2 };
var b = { x: 1, y: 2 };
var c = a;

var ab_eq = (a === b); // false (even though a and b are the same type)
var ac_eq = (a === c); // true</code></pre>

<p>Or even:</p>

<pre><code>var a = { };
var b = { };
var c = a;

var ab_eq = (a === b); // false (even though a and b are the same type)
var ac_eq = (a === c); // true</code></pre>

<p>This behavior is not always obvious. There's more to the story than being equal and being of the same type.</p>

<p>The rule is:</p>

<p><strong><em>For value types (numbers):</em></strong><br />
   <code>a === b</code> returns true if <code>a</code> and <code>b</code> have the same value and are of the same type</p>

<p><strong><em>For reference types:</em></strong><br />
   <code>a === b</code> returns true if <code>a</code> and <code>b</code> reference the exact same object</p>

<p><strong><em>For strings:</em></strong><br />
   <code>a === b</code> returns true if <code>a</code> and <code>b</code> are both strings and contain the exact same characters</p>

<hr />

<h2>Strings: the special case...</h2>

<p>Strings are not value types, but in Javascript they behave like value types, so they will be "equal" when the characters in the string are the same and when they are of the same length (as explained in the third rule)</p>

<p>Now it becomes interesting:</p>

<pre><code>var a = "12" + "3";
var b = "123";

alert(a === b); // returns true, because strings behave like value types</code></pre>

<p>But how about this?:</p>

<pre><code>var a = new String("123");
var b = "123";

alert(a === b); // returns false !! (but they are equal and of the same type)</code></pre>

<p>I thought strings behave like value types? Well, it depends who you ask... In this case a and b are not the same type. <code>a</code> is of type <code>Object</code>, while <code>b</code> is of type <code>string</code>. Just remember that creating a string object using the <code>String</code> constructor creates something of type <code>Object</code> that behaves as a string <em>most of the time</em>.</p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-957602">
                <ul>



    <li id="comment-766508">
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
                activa: I would clarify, that the strings are so equal only when they are literals.  new String("abc") === "abc" is false (according to my research).
                    – <a href="/users/8946/lawrence-dol" title="43,729 reputation" target="_blank">Lawrence Dol</a>
                <a href="#comment766508_957602" target="_blank">Jun 5 '09 at 19:54</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-6217391">
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
                <code>new Number() == "0"</code>. Also in Firefox: <code>(function(){}) == "function () {\n}"</code>
                    – <a href="/users/239916/thomas-eding" title="20,648 reputation" target="_blank">Thomas Eding</a>
                <a href="#comment6217391_957602" target="_blank">Mar 30 '11 at 5:21</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-16218868">
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
                Thank you for explaining why <code>new String("123") !== "123"</code>. They are different types. Simple, yet confusing.
                    – <a href="/users/266535/styfle" title="5,794 reputation" target="_blank">styfle</a>
                <a href="#comment16218868_957602" target="_blank">Aug 26 '12 at 5:51</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-18836708">
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
                <code>String</code> objects behave as strings as does <a href="http://jsfiddle.net/k83ad/1/" target="_blank">any other object</a>. <code>new String</code> should never be used, as that doesn't create real strings. A real string and can be made with string literals or calling <code>String</code> as a function <b>without</b> <code>new</code>, for example: <code>String(0); //"0", Real string, not an object</code>
                    – <a href="/users/995876/esailija" title="112,239 reputation" target="_blank">Esailija</a>
                <a href="#comment18836708_957602" target="_blank">Dec 4 '12 at 23:51</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-45069593">
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
                But in the cases you detailed, the operator "==" behaves exactly the same.
                    – <a href="/users/412992/yaron-levi" title="3,847 reputation" target="_blank">Yaron Levi</a>
                <a href="#comment45069593_957602" target="_blank">Feb 6 '15 at 10:48</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-1813267">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        234
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Let me add this counsel:</p>

<p><strong><em>If in doubt, read the <a href="http://www.ecma-international.org/publications/standards/Ecma-262.htm" target="_blank">specification</a>!</em></strong> </p>

<p>ECMA-262 is the specification for a scripting language of which JavaScript is a dialect. Of course in practice it matters more how the most important browsers behave than an esoteric definition of how something is supposed to be handled. But it is helpful to understand why <strong>new String("a") !== "a"</strong>.</p>

<p>Please let me explain how to read the specification to clarify this question. I see that in this very old topic nobody had an answer for the very strange effect. So, if you can read a specification, this will help you in your profession tremendously. It is an acquired skill. So, let's continue.</p>

<p>Searching the PDF file for === brings me to page 56 of the specification: <strong>11.9.4. The Strict Equals Operator ( === )</strong>, and after wading through the specificationalese I find:</p>

<blockquote>
  <p><strong>11.9.6 The Strict Equality Comparison Algorithm</strong><br />
  The comparison x === y, where x and y are values, produces <strong>true</strong> or <strong>false</strong>. Such a comparison is performed as follows:<br />
    1. If Type(x) is different from Type(y), return <strong>false</strong>.<br />
    2. If Type(x) is Undefined, return <strong>true</strong>.<br />
    3. If Type(x) is Null, return <strong>true</strong>.<br />
    4. If Type(x) is not Number, go to step 11.<br />
    5. If x is <strong>NaN</strong>, return <strong>false</strong>.<br />
    6. If y is <strong>NaN</strong>, return <strong>false</strong>.<br />
    7. If x is the same number value as y, return <strong>true</strong>.<br />
    8. If x is +0 and y is −0, return <strong>true</strong>.<br />
    9. If x is −0 and y is +0, return <strong>true</strong>.<br />
    10. Return <strong>false</strong>.<br />
    11. If Type(x) is String, then return <strong>true</strong> if x and y are exactly the same sequence of characters (same length and same characters in corresponding positions); otherwise, return <strong>false</strong>.<br />
    12. If Type(x) is Boolean, return <strong>true</strong> if x and y are both <strong>true</strong> or both <strong>false</strong>; otherwise, return <strong>false</strong>.<br />
    13. Return <strong>true</strong> if x and y refer to the same object or if they refer to objects joined to each other (see 13.1.2). Otherwise, return <strong>false</strong>.</p>
</blockquote>

<p>Interesting is step 11. Yes, strings are treated as value types. But this does not explain why <strong>new String("a") !== "a"</strong>. Do we have a browser not conforming to ECMA-262?</p>

<p>Not so fast!</p>

<p>Let's check the types of the operands. Try it out for yourself by wrapping them in <strong>typeof()</strong>. I find that <strong>new String("a")</strong> is an object, and step 1 is used: return <strong>false</strong> if the types are different.</p>

<p>If you wonder why <strong>new String("a")</strong> does not return a string, how about some exercise reading a specification? Have fun!</p>

<hr />

<p>Aidiakapi wrote this in a comment below:</p>

<blockquote>
  <p>From the specification </p>
  
  <p><strong>11.2.2 The new Operator</strong>:</p>
  
  <p>If Type(constructor) is not Object, throw a TypeError exception.</p>
  
  <p>With other words, if String wouldn't be of type Object it couldn't be used with the new operator. </p>
</blockquote>

<p><strong>new</strong> always returns an Object, even for <strong>String</strong> constructors, too. And alas! The value semantics for strings (see step 11) is lost.</p>

<p>And this finally means: <strong>new String("a") !== "a"</strong>.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-2818945">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        57
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>It checks if same sides are equal in <strong>type</strong> as well as <strong>value</strong>.</p>

<p><em>Example:</em></p>

<pre><code>'1' === 1 // will return "false" because `string` is not a `number`</code></pre>

<p><em>Common Example:</em></p>

<pre><code>0 == ''  // will be "true", but it's very common to want this check to be "false"</code></pre>
    </div>
    
</div>
    
    <div>
	    <div id="comments-2818945">
                <ul>



    <li id="comment-10921743">
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
                also, <code>'string' !== 'number'</code>
                    – <a href="/users/251614/homer" title="4,250 reputation" target="_blank">Homer</a>
                <a href="#comment10921743_2818945" target="_blank">Jan 6 '12 at 19:34</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-2818947">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        77
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>In JavaScript it means of the same value and type.</p>

<p>For example,</p>

<pre><code>4 == "4" // will return true</code></pre>



<pre><code>4 === "4" // will return false </code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-2818949">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        84
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>In PHP and JavaScript, it is a strict equality operator. Which means, it will compare both type and values.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 12 '10 at 12:58
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-2818949">
                <ul>



    <li id="comment-2999068">
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
                @David: correct. That's why this answer is inaccurate (or even wrong)
                    – <a href="/users/113570/philippe-leybaert" title="119,708 reputation" target="_blank">Philippe Leybaert</a>
                <a href="#comment2999068_2818949" target="_blank">May 31 '10 at 12:25</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-5753350">
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
                @David <code>var a = {}, b = {};</code> <code>a == b</code> returns false.
                    – <a href="/users/492203/nyuszika7h" title="5,590 reputation" target="_blank">nyuszika7h</a>
                <a href="#comment5753350_2818949" target="_blank">Feb 26 '11 at 18:37</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-28835488">
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
                Yes: Two <i>different</i> objects with the same type and value compare false, i.e., this answer is just wrong. Why does it have 50 upvotes?
                    – <a href="/users/699305/alexis" title="30,198 reputation" target="_blank">alexis</a>
                <a href="#comment28835488_2818949" target="_blank">Oct 18 '13 at 10:45</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-2818955">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        43
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>It means <strong>equality without type coercion</strong>
type coercion means JavaScript do not automatically convert any other data types to string data types </p>

<pre><code>0==false   // true,although they are different types

0===false  // false,as they are different types

2=='2'    //true,different types,one is string and another is integer but 
            javaScript convert 2 to string by using == operator 

2==='2'  //false because by using === operator ,javaScript do not convert 
           integer to string 

2===2   //true because both have same value and same types </code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-2818957">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        18
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>From the <a href="https://developer.mozilla.org/en/Core_JavaScript_1.5_Reference/Operators/Comparison_Operators" target="_blank">core javascript reference</a></p>

<blockquote>
  <p><code>===</code> Returns <code>true</code> if the operands are strictly equal (see above)
  with no type conversion.</p>
</blockquote>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-2818982">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        27
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><code>===</code> operator  checks the values as well as the types of the variables for equality.</p>

<p><code>==</code> operator just checks the value of the variables for equality.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-2819117">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        27
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>It's a strict check test.</p>

<p>It's a good thing especially if you're checking between 0 and false and null. </p>

<p>For example, if you have:</p>

<pre><code>$a = 0;</code></pre>

<p>Then:</p>

<pre><code>$a==0; 
$a==NULL;
$a==false;</code></pre>

<p>All returns true and you may not want this. Let's suppose you have a function that can return the 0th index of an array or false on failure. If you check with "==" false, you can get a confusing result.</p>

<p>So with the same thing as above, but a strict test:</p>

<pre><code>$a = 0;

$a===0; // returns true
$a===NULL; // returns false
$a===false; // returns false</code></pre>
    </div>
    
</div>
    
    <div>
	    <div id="comments-2819117">
                <ul>



    <li id="comment-23495213">
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
                In JavaScript, this is completely wrong and wrongly incomplete. <code>0 != null</code>. -1
                    – <a href="/users/707111/ryan" title="154,680 reputation" target="_blank">Ryan♦</a>
                <a href="#comment23495213_2819117" target="_blank">May 6 '13 at 3:07</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-7446163">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        38
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><em><strong>The equal comparison operator == is confusing and should be avoided.</strong></em> </p>

<p>If you <strong>HAVE TO</strong> live with it, then remember the following 3 things: </p>

<ol>
<li><strong>It is not transitive: <em>(a == b)</em> and <em>(b == c)</em> does not lead to <em>(a == c)</em></strong></li>
<li><strong>It's mutually exclusive to its negation: <em>(a == b)</em> and <em>(a != b)</em> always hold opposite Boolean values, with all a and b.</strong></li>
<li><strong>In case of doubt, learn by heart the following truth table:</strong></li>
</ol>

<p>EQUAL OPERATOR TRUTH TABLE IN JAVASCRIPT</p>

<ul>
<li>Each row in the table is a set of 3 mutually "equal" values, meaning that any 2 values among them are equal using the equal == sign*</li>
</ul>

<p>** STRANGE: note that any two values on the first column are not equal in that sense.**</p>

<pre><code>''       == 0 == false   // Any two values among these 3 ones are equal with the == operator
'0'      == 0 == false   // Also a set of 3 equal values, note that only 0 and false are repeated
'\t'     == 0 == false   // -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
'\r'     == 0 == false   // -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
'\n'     == 0 == false   // -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
'\t\r\n' == 0 == false   // -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --

null == undefined  // These two "default" values are not-equal to any of the listed values above
NaN                // NaN is not equal to any thing, even to itself.</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-10893560">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        24
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>JSLint sometimes gives you unrealistic reasons to modify stuff. <code>===</code> has exactly the same performance as <code>==</code> if the types are already the same. </p>

<p>It is faster only when the types are not the same, in which case it does not try to convert types but directly returns a false.</p>

<p>So, <em>IMHO,</em> JSLint maybe used to write new code, but useless over-optimizing should be avoided at all costs. </p>

<p>Meaning, there is no reason to change <code>==</code> to <code>===</code> in a check like <code>if (a == 'test')</code> when you know it for a fact that a can only be a String. </p>

<p>Modifying a lot of code that way wastes developers' and reviewers' time and achieves nothing.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-16253116">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        19
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>As a rule of thumb, I would generally use <code>===</code> instead of <code>==</code> (and <code>!==</code> instead of <code>!=</code>).</p>

<p>Reasons are explained in in the answers above and also Douglas Crockford is pretty clear about it (<a href="http://rads.stackoverflow.com/amzn/click/0596517742" target="_blank">JavaScript: The Good Parts</a>).</p>

<p>However there is <strong>one single exception</strong>:
<code>== null</code> is an efficient way to check for 'is null or undefined':</p>

<pre><code>if( value == null ){
    // value is either null or undefined
}</code></pre>

<p>For example jQuery 1.9.1 uses this pattern 43 times, and  the <a href="http://www.jshint.com/docs/#options" target="_blank">JSHint syntax checker</a> even provides the <code>eqnull</code> relaxing option for this reason.</p>

<p>From the <a href="http://contribute.jquery.org/style-guide/js/" target="_blank">jQuery style guide</a>:</p>

<blockquote>
  <p>Strict equality checks (===) should be used in favor of ==. The only
  exception is when checking for undefined and null by way of null.</p>

<pre><code>// Check for both undefined and null values, for some important reason. 
undefOrNull == null;</code></pre>
</blockquote>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Apr 27 '13 at 14:15
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-17439518">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        45
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>JavaScript <code>===</code> <strong>vs</strong> <code>==</code> .</p>

<pre><code>0==false   // true
0===false  // false, because they are of a different type
1=="1"     // true, auto type coercion
1==="1"    // false, because they are of a different type</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-18694319">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        20
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>The top 2 answers both mentioned == means equality and === means identity. Unfortunately, this statement is incorrect. </p>

<p>If both operands of == are objects, then they are compared to see if they are the same object. If both operands point to the same object, then the equal operator returns true. Otherwise,
the two are not equal. </p>

<pre><code>var a = [1, 2, 3];  
var b = [1, 2, 3];  
console.log(a == b)  // false  
console.log(a === b) // false  </code></pre>

<p>In the code above, both == and === get false because a and b are not the same objects.</p>

<p>That's to say: if both operands of == are objects, == behaves same as ===, which also means identity. The essential difference of this two operators is about type conversion. == has conversion before it checks equality, but === does not.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Sep 9 '13 at 8:31
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-19147489">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        16
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><b>Equality comparison: </b></p>

<p>Operator <code>==</code></p>

<p>Returns true, when both operands are equal. The operands are converted to the same type before being compared.</p>

<pre><code>&gt;&gt;&gt; 1 == 1
true
&gt;&gt;&gt; 1 == 2
false
&gt;&gt;&gt; 1 == '1'
true</code></pre>

<p><b>Equality and type comparison: </b></p>

<p>Operator <code>===</code></p>

<p>Returns true if both operands are equal and of the same type. It's generally 
better and safer if you compare this way, because there's no behind-the-scenes type conversions.</p>

<pre><code>&gt;&gt;&gt; 1 === '1'
false
&gt;&gt;&gt; 1 === 1
true</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 2 '13 at 21:54
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-22505350">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        14
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>*<strong><em>Operators === vs == *</em></strong> </p>

<pre><code>1 == true    =&gt;    true
true == true    =&gt;    true
1 === true    =&gt;    false
true === true    =&gt;    true</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 19 '14 at 12:08
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-22675800">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        14
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Here is a handy comparison table that shows the conversions that happen and the differences between <code>==</code> and <code>===</code>.</p>

<p>As the conclusion states:</p>

<blockquote>
  <p>"Use three equals unless you fully understand the conversions that take
  place for two-equals."</p>
</blockquote>

<p><a href="http://dorey.github.io/JavaScript-Equality-Table/" target="_blank">http://dorey.github.io/JavaScript-Equality-Table/</a></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-23056538">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        16
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>null and undefined are nothingness, that is,</p>

<pre><code>var a;
var b = null;</code></pre>

<p>Here <code>a</code> and <code>b</code> do not have values. Whereas, 0, false and '' are all values. One thing common beween all these are that they are all falsy values, which means they all <strong>satisfy</strong> falsy conditions.</p>

<p>So, the 0, false and '' together form a sub-group. And on other hand, null & undefined form the second sub-group. Check the comparisons in the below image. null and undefined would equal. The other three would equal to each other. But, they all are treated as falsy conditions in JavaScript.</p>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/11I0i.jpg" alt="Enter image description here" /></div></p>

<p>This is same as any object (like {}, arrays, etc.), non-empty string & Boolean true are all truthy conditions. But, they are all not equal.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-23465314">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        468
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>An interesting pictorial representation of the equality comparison between <code>==</code> and <code>===</code>.  </p>

<p><strong>Source: <a href="http://dorey.github.io/JavaScript-Equality-Table/" target="_blank">http://dorey.github.io/JavaScript-Equality-Table/</a></strong></p>

<h1>var1===var2</h1>

<blockquote>
  <p><strong><em>When using three equals signs for JavaScript equality testing,
  everything is as is. Nothing gets converted before being evaluated.</em></strong></p>
</blockquote>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/62vxI.png" alt="Equality evaluation of === in JS" /></div></p>

<h1>var1==var2</h1>

<blockquote>
  <p><strong><em>When using two equals signs for JavaScript equality testing, some
  funky conversions take place.</em></strong></p>
</blockquote>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/35MpY.png" alt="Equality evaluation of == in JS" /></div></p>

<blockquote>
  <p><strong><em>Moral of the story: Use three equals unless you fully understand the
  conversions that take place for two-equals.</em></strong></p>
</blockquote>
    </div>
    
</div>
    
    <div>
	    <div id="comments-23465314">
                <ul>



    <li id="comment-42134109">
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
                @temple: Of course it is. <code>x == y</code> and <code>y == x</code> are the same!
                    – <a href="/users/979621/snag" title="9,069 reputation" target="_blank">SNag</a>
                <a href="#comment42134109_23465314" target="_blank">Nov 6 '14 at 11:15</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-63431497">
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
                @mfeineis you mean === or !== instead of == or != . Don't want to confuse new coders ;)
                    – <a href="/users/2507142/katalin-2003" title="433 reputation" target="_blank">katalin_2003</a>
                <a href="#comment63431497_23465314" target="_blank">Jun 23 '16 at 14:04</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-74184442">
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
                @vsync: Wow, those people who abuse JQuery also say the same thing. I never knew you had so much in common...
		            – user7892745
                <a href="#comment74184442_23465314" target="_blank">Apr 23 '17 at 3:25</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-74209972">
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
                @vsync: If you <i>really don't want types to be equal</i>, you <i>should</i> use <i>three equals</i>!
                    – <a href="/users/979621/snag" title="9,069 reputation" target="_blank">SNag</a>
                <a href="#comment74209972_23465314" target="_blank">Apr 24 '17 at 5:19</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-76036737">
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
                This answer is so damn useful!!!
                    – <a href="/users/881739/skiabox" title="1,666 reputation" target="_blank">skiabox</a>
                <a href="#comment76036737_23465314" target="_blank">Jun 13 '17 at 13:07</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-25208410">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        13
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>JavaScript has both strict and type–converting comparisons. A strict comparison (e.g., <code>===</code>) is only true if the operands are of the same type. The more commonly used abstract comparison (e.g. <code>==</code>) converts the operands to the same Type before making the comparison.</p>

<ul>
<li><p>The equality (<code>==</code>) operator converts the operands if they are not of the same type, then applies strict comparison. If either operand is a number or a boolean, the operands are converted to numbers if possible; else if either operand is a string, the string operand is converted to a number if possible. If both operands are objects, then JavaScript compares internal references which are equal when operands refer to the same object in memory.</p>

<p>Syntax:</p>

<p><code>x == y</code></p>

<p>Examples:</p>

<pre><code>3 == 3     // true
"3" == 3   // true
3 == '3'   // true</code></pre></li>
<li><p>The identity/strict equality(<code>===</code>) operator returns true if the operands are strictly equal (see above) with no type conversion.</p>

<p>Syntax:</p>

<p><code>x === y</code></p>

<p>Examples:</p>

<p><code>3 === 3   // true</code></p></li>
</ul>

<p>For reference: <em><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators" target="_blank">Comparison operators</a></em> (Mozilla Developer Network)</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-26923895">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        30
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>Yes!</strong> It does matter.</p>

<p><code>===</code> operator in javascript <strong>checks value as well as type</strong> where as <code>==</code> operator just checks <strong>the value (does type conversion if required)</strong>.</p>

<p><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/5ttlR.png" alt="enter image description here" /></div></p>

<p>You can easily test it. Paste following code in an HTML file and open it in browser</p>

<pre><code>&lt;script&gt;

function onPageLoad()
{
    var x = "5";
    var y = 5;
    alert(x === 5);
};

&lt;/script&gt;

&lt;/head&gt;

&lt;body onload='onPageLoad();'&gt;</code></pre>

<p>You will get '<strong>false</strong>' in alert. Now modify the <code>onPageLoad()</code> method to <code>alert(x == 5);</code> you will get <strong>true</strong>.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-27195277">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        13
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>If you are making a web application or a secured page you should always use (only when possible)</p>

<pre><code>===</code></pre>

<p>because it will will check if it is the same content and if it is the same type!</p>

<p>so when someone enters:</p>

<pre><code>var check = 1;
if(check == '1') {
    //someone continued with a string instead of number, most of the time useless for your webapp, most of the time entered by a user who does not now what he is doing (this will sometimes let your app crash), or even worse it is a hacker searching for weaknesses in your webapp!
}</code></pre>

<p>but with</p>

<pre><code>var check = 1;
if(check === 1) {
    //some continued with a number (no string) for your script
} else {
    alert('please enter a real number');
}</code></pre>

<p>a hacker will never get deeper in the system to find bugs and hack your app or your users</p>

<p>my point it is that the </p>

<pre><code>===</code></pre>

<p>will add more security to your scripts</p>

<p>of course you can also check if the entered number is valid, is a string, etc.. with other if statements inside the first example, but this is for at least me more easier to understand and use</p>

<p>The reason I posted this is that the word 'more secure' or 'security' has never been said in this conversation (if you look at iCloud.com it uses 2019 times === and 1308 times ==, this also means that you sometimes have the use == instead of === because it will otherwise block your function, but as said in the begin you should use === as much as possible)</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Nov 28 '14 at 20:06
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-29159784">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        25
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Simply </p>

<p><code>==</code> means <strong>comparison</strong> between operands <strong>with</strong> <code>type conversion</code></p>



<p><code>===</code> means <strong>comparison</strong> between operands <strong>without</strong> <code>type conversion</code></p>

<p>Type conversion in javaScript means javaScript automatically convert any other data types to string data types.</p>

<p>For example:</p>

<pre><code>123=='123'   //will return true, because JS convert integer 123 to string '123'
             //as we used '==' operator 

123==='123' //will return false, because JS do not convert integer 123 to string 
            //'123' as we used '===' operator </code></pre>
    </div>
    
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            


            
    






                            

                                                            
                        
                            
                            



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/operators" title="show questions tagged 'operators'" target="_blank">operators</a> <a href="/questions/tagged/equality" title="show questions tagged 'equality'" target="_blank">equality</a> <a href="/questions/tagged/equality-operator" title="show questions tagged 'equality-operator'" target="_blank">equality-operator</a> <a href="/questions/tagged/identity-operator" title="show questions tagged 'identity-operator'" target="_blank">identity-operator</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
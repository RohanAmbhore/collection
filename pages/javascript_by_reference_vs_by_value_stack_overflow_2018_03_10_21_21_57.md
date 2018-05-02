<a href="https://stackoverflow.com/questions/6605640/javascript-by-reference-vs-by-value">https://stackoverflow.com/questions/6605640/javascript-by-reference-vs-by-value</a><div id="articleHeader"><h1>Javascript by reference vs. by value</h1></div>


    

                
                    

                



            



                
                    






    

    <div>

<div>
    <p>This question already has an answer here:</p>
    <ul>
        <li>
            <a href="/questions/518000/is-javascript-a-pass-by-reference-or-pass-by-value-language" target="_blank">Is JavaScript a pass-by-reference or pass-by-value language?</a>
                
                    29 answers
                
        </li>
    </ul>
    </div>
        <p>I'm looking for some good comprehensive reading material on when Javascript passes something by value and when by reference and when modifying a passed item affects the value outside a function and when not.  I'm also interested in when assigning to another variable is by reference vs. by value and whether that follows any different rules than passing as a function parameter.</p>

<p>I've done a lot of searching and find lots of specific examples (many of them here on SO) from which I can start to piece together pieces of the real rules, but I haven't yet found a single, well written document that describes it all.</p>

<p>Also, are there ways in the language to control whether something is passed by reference or by value?</p>

<p>Here are some of the types of questions I want to understand.  These are just examples - I'm actually looking to understand the rules the language goes by, not just the answers to specific examples.  But, here are some examples:</p>

<pre><code>function f(a,b,c) {
   a = 3;
   b.push("foo");
   c.first = false;
}

var x = 4;
var y = ["eeny", "miny", "mo"];
var z = {first: true};
f(x,y,z);</code></pre>

<p>When are the contents of x, y and z changed outside the scope of f for all the different types?</p>

<pre><code>function f() {
    var a = ["1", "2", "3"];
    var b = a[1];
    a[1] = "4";
    // what is the value of b now for all possible data types that the array in "a" might hold?
}

function f() {
    var a = [{yellow: "blue"}, {red: "cyan"}, {green: "magenta"}];
    var b = a[1];
    a[1].red = "tan";
    // what is the value of b now and why?
    b.red = "black";
    // did the value of a[1].red change when I assigned to b.red?
}</code></pre>

<p>If I want to make a fully independent copy of an object (no references whatsoever), what's the best practice way to do that?</p>

    </div>

    <footer>
        




        <div>
		
		
		<div>
            <a href="/users/816620/jfriend00" target="_blank">jfriend00</a><br />
            377k●40●454●514
		</div>
	</div>


            <div>
                                <div>
        <h2>                    <b>marked</b> as duplicate by <a href="/users/811/shog9" target="_blank">Shog9</a>♦ Nov 12 '14 at 1:30
</h2>
        <p>This question has been asked before and already has an answer. If those answers do not fully address your question, please <a href="/questions/ask" target="_blank">ask a new question</a>.</p>
    </div>
            </div>
    </footer>



<div id="comments-6605640">
            <ul>


    <li id="comment-7795688">
        
        <div>
            <div>
                This is a worthwhile read: <a href="http://en.wikipedia.org/wiki/Evaluation_strategy" target="_blank">Wiki: Evaluation Strategy</a>. I prefer Call By Object Sharing to avoid such confusion and leave Call By Reference to actually mean something else, where it applies. To make a "clone" consider <code>jQuery.extend</code> (shallow clone only!) or similar provided by your choice of framework. (I think ECMA ed. 5 introduces <code>Object.clone</code> ...?). A "deep clone" can be achieved with serializing to JSON and back, where such an operation is preserving (it might not always be). I am sure there are also other functions designed for this :)
		            – user166390
                <a href="#comment7795688_6605640" target="_blank">Jul 7 '11 at 4:21</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-36955380">
        
        <div>
            <div>
                I believe jQuery.extend now (1.8.x +) supports deep cloning (using an optional boolean parameter)
                    – <a href="/users/589655/flak-dinenno" title="1,432 reputation" target="_blank">Flak DiNenno</a>
                <a href="#comment36955380_6605640" target="_blank">Jun 1 '14 at 18:53</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-56035193">
        
        <div>
            <div>
                In the years since this question, I've found it is easiest to explain this issue to Javascript newbies (particularly people who know C/C++) by saying just this: "In Javascript, objects are passed by pointer and everything else is passed by value."
                    – <a href="/users/816620/jfriend00" title="377,349 reputation" target="_blank">jfriend00</a>
                <a href="#comment56035193_6605640" target="_blank">Dec 7 '15 at 21:25</a>
                        
                                                                            </div>
        </div>
    </li>
            </ul>
    
</div>
<a href="https://stackoverflow.com/questions/1979884/how-to-use-javascript-regex-over-multiple-lines">https://stackoverflow.com/questions/1979884/how-to-use-javascript-regex-over-multiple-lines</a><div id="articleHeader"><h1>How to use JavaScript regex over multiple lines?</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        185
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>36</b></div>


</div>

            </div>

            
<div>
    <div>

<pre><code>var ss= "&lt;pre&gt;aaaa\nbbb\nccc&lt;/pre&gt;ddd";
var arr= ss.match( /&lt;pre.*?&lt;\/pre&gt;/gm );
alert(arr);     // null</code></pre>

<p>I'd want the PRE block be picked up, even though it spans over newline characters. I thought the 'm' flag does it. Does not.</p>

<p>Found the answer <a href="http://blog.simonwillison.net/post/57956777104/newlines" target="_blank">here</a> before posting. SInce I thought I knew JavaScript (read three books, worked hours) and there wasn't an existing solution at SO, I'll dare to post anyways. <strong>throw stones here</strong></p>

<p>So the solution is:</p>

<pre><code>var ss= "&lt;pre&gt;aaaa\nbbb\nccc&lt;/pre&gt;ddd";
var arr= ss.match( /&lt;pre[\s\S]*?&lt;\/pre&gt;/gm );
alert(arr);     // &lt;pre&gt;...&lt;/pre&gt; :)</code></pre>

<p>Does anyone have a less cryptic way?</p>

<p>Edit: <a href="https://stackoverflow.com/questions/1387116/matching-multiline-patterns" target="_blank">this</a> is a duplicate but since it's harder to find than mine, I don't remove.</p>

<p>It proposes <code>[^]</code> as a "multiline dot". What I still don't understand is why <code>[.\n]</code> does not work. Guess this is one of the sad parts of JavaScript..</p>
    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-1981692">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        158
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p><code>[.\n]</code> does not work because <code>.</code> has no special meaning inside of <code>[]</code>, it just means a literal <code>.</code>. <code>(.|\n)</code> would be a way to specify "any character, including a newline". If you want to match all newlines, you would need to add <code>\r</code> as well to include Windows and classic Mac OS style line endings: <code>(.|[\r\n])</code>.</p>

<p>That turns out to be somewhat cumbersome, as well as slow, (see <a href="https://stackoverflow.com/a/16119722/69755" target="_blank">KrisWebDev's answer for details</a>), so a better approach would be to match all whitespace characters and all non-whitespace characters, with <code>[\s\S]</code>, which will match everything, and is faster and simpler.</p>

<p>In general, you shouldn't try to use a regexp to match the actual HTML tags. See, for instance, <a href="https://stackoverflow.com/questions/701166/can-you-provide-some-examples-of-why-it-is-hard-to-parse-xml-and-html-with-a-rege" target="_blank">these</a> <a href="https://stackoverflow.com/questions/1732348/regex-match-open-tags-except-xhtml-self-contained-tags/1732454#1732454" target="_blank">questions</a> for more information on why.</p>

<p>Instead, try actually searching the DOM for the tag you need (using jQuery makes this easier, but you can always do <code>document.getElementsByTagName("pre")</code> with the standard DOM), and then  search the text content of those results with a regexp if you need to match against the contents.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-1981642">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        11
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><code>[.\n]</code> doesn't work, because dot in <code>[]</code> (by regex definition; not javascript only) means the dot-character. You can use <code>(.|\n)</code> (or <code>(.|[\n\r])</code>) instead.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 30 '09 at 18:18
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-16119722">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        265
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>DON'T use <code>(.|[\r\n])</code> instead of <code>.</code> for multiline matching.</p>

<p>DO use <code>[\s\S]</code> instead of <code>.</code> for multiline matching</p>

<p>Also, avoid greediness where not needed by using <code>*?</code> or <code>+?</code> quantifier instead of <code>*</code> or <code>+</code>. This can have a huge performance impact.</p>

<p>See the benchmark I have made: <a href="http://jsperf.com/javascript-multiline-regexp-workarounds" target="_blank">http://jsperf.com/javascript-multiline-regexp-workarounds</a></p>

<pre><code>Using [^]: fastest
Using [\s\S]: 0.83% slower
Using (.|\r|\n): 96% slower
Using (.|[\r\n]): 96% slower</code></pre>

<p>NB: You can also use <code>[^]</code> but it is deprecated in the below comment.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-44906981">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I have tested it (Chrome) and it working for me( both <code>[^]</code> and <code>[^\0]</code>), by changing the dot (<code>.</code>) by either <code>[^\0]</code> or <code>[^]</code> , because dot doesn't match line break (See here: <a href="http://www.regular-expressions.info/dot.html" target="_blank">http://www.regular-expressions.info/dot.html</a>).</p>

<div>
<div>
<pre><code>var ss= "&lt;pre&gt;aaaa\nbbb\nccc&lt;/pre&gt;ddd";
var arr= ss.match( /&lt;pre[^\0]*?&lt;\/pre&gt;/gm );
alert(arr);     //Working</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jul 4 '17 at 13:10
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-48821634">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>In addition to above-said examples, it is an alternate.</p>

<pre><code>^[\\w\\s]*$</code></pre>

<p>Where <code>\w</code> is for words and <code>\s</code> is for white spaces</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Feb 16 at 7:04
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-49766419">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>You do not specify your environment and version of Javascript (ECMAscript), and I realise this post was from 2009, but just for completeness, with the release of ECMA2018 we can now use the <code>s</code> flag to cause <code>.</code> to match '\n', see <a href="https://stackoverflow.com/a/36006948/141801" target="_blank">https://stackoverflow.com/a/36006948/141801</a></p>

<p>Thus:</p>

<pre><code>let s = 'I am a string\nover several\nlines.';
console.log('String: "' + s + '".');

let r = /string.*several.*lines/s; // Note 's' modifier
console.log('Match? ' + r.test(s); // 'test' returns true</code></pre>

<p>This is a recent addition and will not work in many current environments, for example Node v8.7.0 does not seem to recognise it, but it works in Chromium, and I'm using it in a Typescript test I'm writing and presumably it will become more mainstream as time goes by.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Apr 11 at 4:17
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/regex" title="show questions tagged 'regex'" target="_blank">regex</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
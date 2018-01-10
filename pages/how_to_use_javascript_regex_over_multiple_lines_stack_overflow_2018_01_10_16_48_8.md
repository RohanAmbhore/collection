<a href="https://stackoverflow.com/questions/1979884/how-to-use-javascript-regex-over-multiple-lines">https://stackoverflow.com/questions/1979884/how-to-use-javascript-regex-over-multiple-lines</a><div id="articleHeader"><h1>How to use JavaScript regex over multiple lines?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        172
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>29</b></div>


</div>

            </td>
            
<td>
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
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-1979884">
		        <table>
                    <tbody>



    <tr id="comment-1895265">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                16
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
                A less cryptic regex? Impossible, by nature.
                    – <a href="/users/113794/rubens-farias" title="46,082 reputation" target="_blank">Rubens Farias</a>
                <a href="#comment1895265_1979884" target="_blank">Dec 30 '09 at 12:18</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-1895280">
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
                @rubens: I was about to put exactly the same comment
                    – <a href="/users/90691/marcgg" title="38,476 reputation" target="_blank">marcgg</a>
                <a href="#comment1895280_1979884" target="_blank">Dec 30 '09 at 12:21</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-1895288">
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
            
        </td>
    </tr>
    <tr id="comment-43935587">
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
            
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-1979884">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-1981692">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        149
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p><code>[.\n]</code> does not work because <code>.</code> has no special meaning inside of <code>[]</code>, it just means a literal <code>.</code>. <code>(.|\n)</code> would be a way to specify "any character, including a newline". If you want to match all newlines, you would need to add <code>\r</code> as well to include Windows and classic Mac OS style line endings: <code>(.|[\r\n])</code>.</p>

<p>That turns out to be somewhat cumbersome, as well as slow, (see <a href="https://stackoverflow.com/a/16119722/69755" target="_blank">KrisWebDev's answer for details</a>), so a better approach would be to match all whitespace characters and all non-whitespace characters, with <code>[\s\S]</code>, which will match everything, and is faster and simpler.</p>

<p>In general, you shouldn't try to use a regexp to match the actual HTML tags. See, for instance, <a href="https://stackoverflow.com/questions/701166/can-you-provide-some-examples-of-why-it-is-hard-to-parse-xml-and-html-with-a-rege" target="_blank">these</a> <a href="https://stackoverflow.com/questions/1732348/regex-match-open-tags-except-xhtml-self-contained-tags/1732454#1732454" target="_blank">questions</a> for more information on why.</p>

<p>Instead, try actually searching the DOM for the tag you need (using jQuery makes this easier, but you can always do <code>document.getElementsByTagName("pre")</code> with the standard DOM), and then  search the text content of those results with a regexp if you need to match against the contents.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-1981692">
		        <table>
                    <tbody>



    <tr id="comment-1918562">
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
                What I'm doing is making .wiki -&gt; HTML conversion on the fly, using JavaScript. Therefore, I don't have the DOM available, yet.  Wiki file is mostly its own syntax, but I allow HTML tags to be used if needed.   Your advice is <i>very</i> valid, if I was dealing in DOM with this. Thanks. :)
                    – <a href="/users/14455/akauppi" title="7,063 reputation" target="_blank">akauppi</a>
                <a href="#comment1918562_1981692" target="_blank">Jan 4 '10 at 14:34</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-1918708">
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
                Fair enough. I suppose that is a valid reason to want to use regexes on HTML, though wiki syntaxes mixed with HTML can have all kinds of fun corner cases themselves.
                    – <a href="/users/69755/brian-campbell" title="200,737 reputation" target="_blank">Brian Campbell</a>
                <a href="#comment1918708_1981692" target="_blank">Jan 4 '10 at 14:56</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-61206070">
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
                <code>[\r\n]</code>applied to a sequence \r\n, would first match \r and then \n. If you want to match the entire sequence at once, regardless of whether that sequence is \r\n or just \n, use the pattern <code>.|\r?\n</code>
                    – <a href="/users/3897504/eirik-birkeland" title="405 reputation" target="_blank">Eirik Birkeland</a>
                <a href="#comment61206070_1981692" target="_blank">Apr 23 '16 at 21:47</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-1981692">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-44906981">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        4
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
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
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 4 '17 at 13:10
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
	    

        <div id="comments-link-44906981">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-16119722">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        245
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
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
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-16119722">
		        <table>
                    <tbody>



    <tr id="comment-23024379">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                15
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
                Good points, but I recommend against using <code>[^]</code> anyway.  On one hand, JavaScript is the only flavor I know that supports that idiom, and even there it's used nowhere near as often as <code>[\s\S]</code>.  On the other hand, most other flavors let you escape the <code>]</code> by listing it first.  In other words, in JavaScript <code>[^][^]</code> matches any two characters, but in .NET it matches any <i>one</i> character other than <code>]</code>, <code>[</code>, or <code>^</code>.
                    – <a href="/users/20938/alan-moore" title="56,777 reputation" target="_blank">Alan Moore</a>
                <a href="#comment23024379_16119722" target="_blank">Apr 20 '13 at 12:53</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-26798569">
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
                +1 helped me understand the multiline matching better, AND the performance issue, that go hand in hand. :)
                    – <a href="/users/1679286/winner-joiner" title="2,828 reputation" target="_blank">winner_joiner</a>
                <a href="#comment26798569_16119722" target="_blank">Aug 16 '13 at 10:20</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-30209722">
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
                How do you know that <code>\S</code> will match <code>\r</code> or <code>\n</code> versus some other character?
                    – <a href="/users/14731/gili" title="33,740 reputation" target="_blank">Gili</a>
                <a href="#comment30209722_16119722" target="_blank">Nov 27 '13 at 21:38</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-30308248">
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
                See <a href="http://stackoverflow.com/questions/4544636/what-does-s-s-mean-in-regex-in-php" target="_blank">this question</a> for \s\S details. This is a hack to match all white-space characters + all non-whitespace characters = all characters. See also <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp" target="_blank">MDN</a> for regexp special character documentation.
                    – <a href="/users/2227298/kriswebdev" title="6,554 reputation" target="_blank">KrisWebDev</a>
                <a href="#comment30308248_16119722" target="_blank">Dec 1 '13 at 9:55</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-66545625">
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
                . doesn't work while accepted solution works.
                    – <a href="/users/2166409/daniel-kmak" title="12,449 reputation" target="_blank">Daniel Kmak</a>
                <a href="#comment66545625_16119722" target="_blank">Sep 21 '16 at 14:48</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-16119722">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>3</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-1981642">
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
<p><code>[.\n]</code> doesn't work, because dot in <code>[]</code> (by regex definition; not javascript only) means the dot-character. You can use <code>(.|\n)</code> (or <code>(.|[\n\r])</code>) instead.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 30 '09 at 18:18
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
	    <div id="comments-1981642">
		        <table>
                    <tbody>



    <tr id="comment-1919590">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                22
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
                <code>[\s\S]</code> is the most common JavaScript idiom for matching everything including newlines.  It's easier on the eyes and much more efficient than an alternation-based approach like <code>(.|\n)</code>.  (It literally means "any character that <i>is</i> whitespace or any character that <i>isn't</i> whitespace.)
                    – <a href="/users/20938/alan-moore" title="56,777 reputation" target="_blank">Alan Moore</a>
                <a href="#comment1919590_1981642" target="_blank">Jan 4 '10 at 17:04</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-1919957">
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
                You're right, but the question was about <code>.</code> and <code>\n</code>, and why <code>[.\n]</code> doesn't work. As mentioned in the question, the <code>[^]</code> is also nice approach.
                    – <a href="/users/225680/y-shoham" title="5,748 reputation" target="_blank">Y. Shoham</a>
                <a href="#comment1919957_1981642" target="_blank">Jan 4 '10 at 18:01</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-1981642">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/regex" title="show questions tagged 'regex'" target="_blank">regex</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
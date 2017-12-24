<a href="https://stackoverflow.com/questions/15458876/check-if-a-string-is-html-or-not">https://stackoverflow.com/questions/15458876/check-if-a-string-is-html-or-not</a><div id="articleHeader"><h1>Check if a string is html or not</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        59
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>19</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I have a certain string for which I want to check if it is a html or not. I am using regex for the same but not getting the proper result.</p>

<p>I validated my regex and it works fine <a href="http://tools.netshiftmedia.com/regexlibrary/#" target="_blank">here</a>.</p>

<pre><code>var htmlRegex = new RegExp("&lt;([A-Za-z][A-Za-z0-9]*)\b[^&gt;]*&gt;(.*?)&lt;/\1&gt;");
return htmlRegex.test(testString);</code></pre>

<p>Here's the fiddle but the regex isn't running in there. <a href="http://jsfiddle.net/wFWtc/" target="_blank">http://jsfiddle.net/wFWtc/</a></p>

<p>On my machine, the code runs fine but I get a false instead of true as the result.
What am missing here?</p>
    </div>
    
    <table>
    <tbody><tr>
    <td>
        
    </td>
    <td>
        <div>
    <div>
        asked Mar 17 '13 at 8:23
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-15458876">
		        <table>
                    <tbody>



    <tr id="comment-21873857">
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
                Use an HTML parser to parse HTML. Please read <a href="http://stackoverflow.com/a/1732454/464709" target="_blank">this</a> if you haven't already.
                    – <a href="/users/464709/fr%c3%a9d%c3%a9ric-hamidi" title="190,212 reputation" target="_blank">Frédéric Hamidi</a>
                <a href="#comment21873857_15458876" target="_blank">Mar 17 '13 at 8:25</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-21873871">
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
                the question keep coming, there should be a stack bot that will aoutmatically set a comment on every question with html and regex in it
                    – <a href="/users/673760/bartlomiej-lewandowski" title="5,799 reputation" target="_blank">Bartlomiej Lewandowski</a>
                <a href="#comment21873871_15458876" target="_blank">Mar 17 '13 at 8:26</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-21873913">
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
                It kinda depends on what level of sophistication you want from the check. You could check if the string contains at least one <code>&lt;</code> and at least one <code>&gt;</code> and call it HTML, or you could check that it is strictly valid with correct HTML syntax, or anything from between. For the simplest of cases a HTML parser is not necessary.
                    – <a href="/users/502381/jjj" title="27,769 reputation" target="_blank">JJJ</a>
                <a href="#comment21873913_15458876" target="_blank">Mar 17 '13 at 8:30</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-21873918">
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
                Why do you check a string is HTML?
                    – <a href="/users/1400768/nhahtdh" title="44,086 reputation" target="_blank">nhahtdh</a>
                <a href="#comment21873918_15458876" target="_blank">Mar 17 '13 at 8:31</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-21873978">
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
                @user1240679: Valid markup format? What kind of validity? In the strictest sense, you need DTD to describe it. In a loose sense, you may want to check that the tags are matched up properly. Either of the 2 cases above are not job for regex.
                    – <a href="/users/1400768/nhahtdh" title="44,086 reputation" target="_blank">nhahtdh</a>
                <a href="#comment21873978_15458876" target="_blank">Mar 17 '13 at 8:36</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-15458876">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>3</b> more comments</a>
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-15458987">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        175
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>A better regex to use to check if a string is HTML is:</p>

<pre><code>/^/</code></pre>

<p>For example:</p>

<pre><code>/^/.test('') // true
/^/.test('foo bar baz') //true
/^/.test('&lt;p&gt;fizz buzz&lt;/p&gt;') //true</code></pre>

<p>In fact, it's so good, that it'll return <code>true</code> for <em>every</em> string passed to it, which is because <strong><em>every string is HTML</em></strong>. Seriously, even if it's poorly formatted or invalid, it's still HTML.</p>

<p>If what you're looking for is the presence of HTML elements, rather than simply any text content, you could use something along the lines of:</p>

<pre><code>/&lt;[a-z][\s\S]*&gt;/i.test()</code></pre>

<p>It won't help you parse the HTML in any way, but it will certainly flag the string as containing HTML elements.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Mar 17 '13 at 8:43
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
	    <div id="comments-15458987">
		        <table>
                    <tbody>



    <tr id="comment-21874068">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                72
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
                +1 for the funny lesson
                    – <a href="/users/731947/cs%e1%b5%a0" title="8,037 reputation" target="_blank">CSᵠ</a>
                <a href="#comment21874068_15458987" target="_blank">Mar 17 '13 at 8:46</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-21882870">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                11
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
                I'm honestly surprised I didn't get more downvotes for the snark.
                    – <a href="/users/497418/zzzzbov" title="116,289 reputation" target="_blank">zzzzBov</a>
                <a href="#comment21882870_15458987" target="_blank">Mar 17 '13 at 17:56</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-44995055">
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
                @clenemt, so you consider <code>a &lt; b && a &gt; c</code> to be HTML?
                    – <a href="/users/497418/zzzzbov" title="116,289 reputation" target="_blank">zzzzBov</a>
                <a href="#comment44995055_15458987" target="_blank">Feb 4 '15 at 14:20</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-59686419">
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
                @zzzzBov you know that you consider <code>a&lt;b && a&gt;c</code> to be HTML... I wish HTML detection could be simplified that much. Parsing is never easy.
                    – <a href="/users/3356679/oriadam" title="1,735 reputation" target="_blank">oriadam</a>
                <a href="#comment59686419_15458987" target="_blank">Mar 15 '16 at 17:00</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-59687401">
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
                @oriadam, the context was for detecting elements in that case. If you use <code>a &lt; b && a &gt; c</code> the browser will turn the <code>&gt;</code> and <code>&lt;</code> characters into <code>&gt;</code> and <code>&lt;</code> entities appropriately. If, instead, you use <code>a&lt;b && a&gt;c</code> the browser will interpret the markup as <code>a&lt;b && a&gt;c&lt;/b&gt;</code> because the lack of a space means that <code>&lt;b</code> opens a <code>&lt;b&gt;</code> element. <a href="https://jsfiddle.net/utf9027v/" target="_blank">Here's a quick demo of what I'm talking about</a>.
                    – <a href="/users/497418/zzzzbov" title="116,289 reputation" target="_blank">zzzzBov</a>
                <a href="#comment59687401_15458987" target="_blank">Mar 15 '16 at 17:24</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-15458987">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>6</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-15458922">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If you're creating a regex from a string literal you need to escape any backslashes:</p>

<pre><code>var htmlRegex = new RegExp("&lt;([A-Za-z][A-Za-z0-9]*)\\b[^&gt;]*&gt;(.*?)&lt;/\\1&gt;");
// extra backslash added here ---------------------^ and here -----^</code></pre>

<p>This is not necessary if you use a regex literal, but then you need to escape forward slashes:</p>

<pre><code>var htmlRegex = /&lt;([A-Za-z][A-Za-z0-9]*)\b[^&gt;]*&gt;(.*?)&lt;\/\1&gt;/;
// forward slash escaped here ------------------------^</code></pre>

<p>Also your jsfiddle didn't work because you assigned an <code>onload</code> handler inside another <code>onload</code> handler - the default as set in the Frameworks & Extensions panel on the left is to wrap the JS in an <code>onload</code>. Change that to a nowrap option and fix the string literal escaping and it "works" (within the constraints everybody has pointed out in comments): <a href="http://jsfiddle.net/wFWtc/4/" target="_blank">http://jsfiddle.net/wFWtc/4/</a></p>

<p><s>As far as I know JavaScript regular expressions don't have back-references. So this part of your expression:</s></p><s>

<pre><code>&lt;/\1&gt;</code></pre>

</s><p><s>won't work in JS (but would work in some other languages).</s></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-15458922">
		        <table>
                    <tbody>



    <tr id="comment-21873947">
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
    <tr id="comment-21873968">
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
                @nhahtdh - I stand corrected. Thanks.
                    – <a href="/users/615754/nnnnnn" title="113,463 reputation" target="_blank">nnnnnn</a>
                <a href="#comment21873968_15458922" target="_blank">Mar 17 '13 at 8:36</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-21874019">
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
                Well, this will test that one of the tags looks OK, but nothing about the rest. Not sure what sort of "validity" that OP wants.
                    – <a href="/users/1400768/nhahtdh" title="44,086 reputation" target="_blank">nhahtdh</a>
                <a href="#comment21874019_15458922" target="_blank">Mar 17 '13 at 8:39</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-21874028">
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
                what about <code>&lt;br&gt;</code> <code>&lt;hr&gt;</code> <code>&lt;input...&gt;</code> @user1240679 ?
                    – <a href="/users/731947/cs%e1%b5%a0" title="8,037 reputation" target="_blank">CSᵠ</a>
                <a href="#comment21874028_15458922" target="_blank">Mar 17 '13 at 8:41</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-15458922">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-15458968">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        48
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p><strong>Method #1</strong>. Here is the simple function to test if the string contains HTML data:</p>

<pre><code>function isHTML(str) {
  var a = document.createElement('div');
  a.innerHTML = str;

  for (var c = a.childNodes, i = c.length; i--; ) {
    if (c[i].nodeType == 1) return true; 
  }

  return false;
}</code></pre>

<p>The idea is to allow browser DOM parser to decide if provided string looks like an HTML or not. As you can see it simply checks for <code>ELEMENT_NODE</code> (<code>nodeType</code> of 1).</p>

<p>I made a couple of tests and looks like it works:</p>

<pre><code>isHTML('&lt;a&gt;this is a string&lt;/a&gt;') // true
isHTML('this is a string')        // false
isHTML('this is a &lt;b&gt;string&lt;/b&gt;') // true</code></pre>

<p>This solution will properly detect HTML string, however it has side effect that img/vide/etc. tags will start downloading resource once parsed in innerHTML.</p>

<p><strong>Method #2</strong>. Another method uses <a href="https://developer.mozilla.org/en-US/docs/Web/API/DOMParser" target="_blank">DOMParser</a> and doesn't have loading resources side effects:</p>

<pre><code>function isHTML(str) {
  var doc = new DOMParser().parseFromString(str, "text/html");
  return Array.from(doc.body.childNodes).some(node =&gt; node.nodeType === 1);
}</code></pre>

<p><sub>
Notes:<br />1. <code>Array.from</code> is ES2015 method, can be replaced with <code>[].slice.call(doc.body.childNodes)</code>.<br />2. Arrow function in <code>some</code> call can be replaced with usual anonymous function.</sub></p>

</div>
    <table>
    <tbody><tr>
    <td>
                    </td>
    <td>
<div>
    <div>
        <a href="/posts/15458968/revisions" title="show all edits to this post" target="_blank">edited Dec 15 at 11:00</a>
    </div>
    
    
</div>    </td>
            


    <td>   
       

    <div>
    <div>
        answered Mar 17 '13 at 8:40
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
	    <div id="comments-15458968">
		        <table>
                    <tbody>



    <tr id="comment-26265132">
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
                This is a very readable solution !
                    – <a href="/users/1003222/user49126" title="391 reputation" target="_blank">user49126</a>
                <a href="#comment26265132_15458968" target="_blank">Jul 31 '13 at 11:19</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-34803046">
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
                This's an awesome idea. However, this function could not detect closing tag (i.e. <code>isHTML("&lt;/a&gt;") --&gt; false</code>).
                    – <a href="/users/3247703/tresdin" title="6,381 reputation" target="_blank">Tresdin</a>
                <a href="#comment34803046_15458968" target="_blank">Apr 2 '14 at 18:11</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-37979108">
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
                Great solution!.. The only negative side-affect of is that if your html contains any static resources like an image src attribute.. <code>innerHTML</code> will force the browser to start fetching those resources. :(
                    – <a href="/users/831738/jose-browne" title="2,764 reputation" target="_blank">Jose Browne</a>
                <a href="#comment37979108_15458968" target="_blank">Jul 2 '14 at 9:46</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-71031362">
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
                @JoseBrowne even if it's not appended to the DOM?
                    – <a href="/users/1938970/kuus" title="117 reputation" target="_blank">kuus</a>
                <a href="#comment71031362_15458968" target="_blank">Jan 29 at 20:15</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-71031476">
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
                @kuus Yes, even if not appending. Use DOMParser solution.
                    – <a href="/users/949476/dfsq" title="150,110 reputation" target="_blank">dfsq</a>
                <a href="#comment71031476_15458968" target="_blank">Jan 29 at 20:21</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-15458968">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-15459273">
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
<p>A little bit of validation with:</p>

<pre><code>/&lt;(?=.*? .*?\/ ?&gt;|br|hr|input|!--|wbr)[a-z]+.*?&gt;|&lt;([a-z]+).*?&lt;\/\1&gt;/i.test(htmlStringHere) </code></pre>

<p>This searches for empty tags (some predefined) and <code>/</code> terminated XHTML empty tags and validates as HTML because of the empty tag OR will capture the tag name and attempt to find it's closing tag somewhere in the string to validate as HTML.</p>

<p>Explained demo: <a href="http://regex101.com/r/cX0eP2" target="_blank">http://regex101.com/r/cX0eP2</a></p>

<p><strong>Update:</strong></p>

<p>Complete validation with:  </p>

<pre><code>/&lt;(br|basefont|hr|input|source|frame|param|area|meta|!--|col|link|option|base|img|wbr|!DOCTYPE).*?&gt;|&lt;(a|abbr|acronym|address|applet|article|aside|audio|b|bdi|bdo|big|blockquote|body|button|canvas|caption|center|cite|code|colgroup|command|datalist|dd|del|details|dfn|dialog|dir|div|dl|dt|em|embed|fieldset|figcaption|figure|font|footer|form|frameset|head|header|hgroup|h1|h2|h3|h4|h5|h6|html|i|iframe|ins|kbd|keygen|label|legend|li|map|mark|menu|meter|nav|noframes|noscript|object|ol|optgroup|output|p|pre|progress|q|rp|rt|ruby|s|samp|script|section|select|small|span|strike|strong|style|sub|summary|sup|table|tbody|td|textarea|tfoot|th|thead|time|title|tr|track|tt|u|ul|var|video).*?&lt;\/\2&gt;/i.test(htmlStringHere) </code></pre>

<p>This does <strong><em>proper</em></strong> validation as it contains <strong>ALL</strong> HTML tags, empty ones first followed by the rest which need a closing tag.</p>

<p>Explained demo here: <a href="http://regex101.com/r/pE1mT5" target="_blank">http://regex101.com/r/pE1mT5</a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-15459273">
		        <table>
                    <tbody>



    <tr id="comment-66555672">
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
                Just a note the bottom regex does work but it won't detect unclosed html tags such as "'&lt;strong&gt;hello world". granted this is broken html therefore should be treated as a string but for practical purposes your app may want to detect these too.
                    – <a href="/users/967451/tk123" title="9,449 reputation" target="_blank">TK123</a>
                <a href="#comment66555672_15459273" target="_blank">Sep 21 '16 at 19:39</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-15459273">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-20073705">
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
<p>With jQuery:</p>

<pre><code>function isHTML(str) {
  return /^&lt;.*?&gt;$/.test(str) && !!$(str)[0];
}</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-20073705">
		        <table>
                    <tbody>



    <tr id="comment-31741980">
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
                <code>isHTML("&lt;foo&gt;");</code> // returns true <code>isHTML("div");</code> // returns true if there are <code>div</code>s on the page
                    – <a href="/users/847201/ack-stoverflow" title="1,380 reputation" target="_blank">ACK_stoverflow</a>
                <a href="#comment31741980_20073705" target="_blank">Jan 13 '14 at 19:46</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-62182034">
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
                This will not work if the string is an email.
                    – <a href="/users/277186/yekta" title="1,979 reputation" target="_blank">yekta</a>
                <a href="#comment62182034_20073705" target="_blank">May 19 '16 at 18:58</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-62182191">
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
                @yekta - What are you taking about? This is supposed to check wether the string is html or not. An email is not an html tag as far as I know... isHTML('foo@bar.com') -&gt; false // correct
                    – <a href="/users/2268492/gtournie" title="1,651 reputation" target="_blank">gtournie</a>
                <a href="#comment62182191_20073705" target="_blank">May 19 '16 at 19:02</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-62185258">
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
                A string can be anything, if you know its an HTML tag then why check if its HTML in the first place, I don't quite follow your point.  The <code>@</code> is not a valid syntax for a selector.  Thus when you pass it to a jQuery selector, it will throw an exception (i.e. <code>$("you@example.com")</code> from <code>!!$(str)[0]</code>).  I'm specifically referring to the <code>!!$(str)[0]</code>  portion.  You just edited your answer, but now you're checking for HTML before jQuery does anything.
                    – <a href="/users/277186/yekta" title="1,979 reputation" target="_blank">yekta</a>
                <a href="#comment62185258_20073705" target="_blank">May 19 '16 at 20:42</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-62187455">
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
                I don't think the author wanted to check if it was just a string. That's the point. What he wanted was a function able to check if the string was a valid HTML <b>tag</b>, not just HTML (otherwise this is a bit stupid). I updated my answer after I read @ACK_stoverflow comment, but I'm sure a simple regex should do it.
                    – <a href="/users/2268492/gtournie" title="1,651 reputation" target="_blank">gtournie</a>
                <a href="#comment62187455_20073705" target="_blank">May 19 '16 at 22:07</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-20073705">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-25381038">
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
<p><a href="https://stackoverflow.com/questions/15458876/check-if-a-string-is-html-or-not#15458987" target="_blank">zzzzBov's answer</a> above is good, but it does not account for stray closing tags, like for example:</p>

<pre><code>/&lt;[a-z][\s\S]*&gt;/i.test('foo &lt;/b&gt; bar'); // false</code></pre>

<p>A version that also catches closing tags could be this:</p>

<pre><code>/&lt;[a-z/][\s\S]*&gt;/i.test('foo &lt;/b&gt; bar'); // true</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-25381038">
		        <table>
                    <tbody>



    <tr id="comment-66253304">
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
                Could have been better to suggest an edit, instead of posting this as a comment.
                    – <a href="/users/481422/zlatin-zlatev" title="2,002 reputation" target="_blank">Zlatin Zlatev</a>
                <a href="#comment66253304_25381038" target="_blank">Sep 13 '16 at 9:27</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-74787751">
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
                I think you mean <code>&lt;[a-z/][\s\S]*&gt;</code> - note the slash in the first group.
                    – <a href="/users/7186/ryan-guill" title="8,810 reputation" target="_blank">Ryan Guill</a>
                <a href="#comment74787751_25381038" target="_blank">May 9 at 17:38</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-75066801">
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
                @RyanGuill, thanks - I edited the regex to fix it.
                    – <a href="/users/2298192/aeonoftime" title="395 reputation" target="_blank">AeonOfTime</a>
                <a href="#comment75066801_25381038" target="_blank">May 17 at 8:47</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-25381038">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-35216143">
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
<p><code>/&lt;\/?[^&gt;]*&gt;/.test(str)</code> Only detect whether it contains html tags, may be a xml</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Feb 5 '16 at 4:09
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
	    

        <div id="comments-link-35216143">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-36773193">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Here's a sloppy one-liner that I use from time to time:</p>

<pre><code>var isHTML = RegExp.prototype.test.bind(/(&lt;([^&gt;]+)&gt;)/i);</code></pre>

<p>It will basically return <code>true</code> for strings containing a <code>&lt;</code> followed by <strong><code>ANYTHING</code></strong> followed by <code>&gt;</code>.</p>

<p>By <strong><code>ANYTHING</code></strong>, I mean basically anything except an empty string.</p>

<p>It's not great, but it's a one-liner.</p>

<p><strong>Usage</strong></p>

<pre><code>isHTML('Testing');               // false
isHTML('&lt;p&gt;Testing&lt;/p&gt;');        // true
isHTML('&lt;img src="hello.jpg"&gt;'); // true
isHTML('My &lt; weird &gt; string');   // true (caution!!!)
isHTML('&lt;&gt;');                    // false</code></pre>

<p>As you can see it's far from perfect, but might do the job for you in some cases.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-36773193">
		        <table>
                    <tbody>



    <tr id="comment-77218273">
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
                just what i needed. Nothing fancy, just clean. Thanks!
                    – <a href="/users/2397922/moeiscool" title="594 reputation" target="_blank">moeiscool</a>
                <a href="#comment77218273_36773193" target="_blank">Jul 15 at 23:59</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-36773193">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-44480655">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Using jQuery in this case, the simplest form would be:</p>

<pre><code>if ($(testString).length &gt; 0)</code></pre>

<p>If <code>$(testString).length = 1</code>, this means that there is one HTML tag inside <code>textStging</code>.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-44480655">

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
        
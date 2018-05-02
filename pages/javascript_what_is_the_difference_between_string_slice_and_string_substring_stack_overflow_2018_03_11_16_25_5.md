<a href="https://stackoverflow.com/questions/2243824/what-is-the-difference-between-string-slice-and-string-substring">https://stackoverflow.com/questions/2243824/what-is-the-difference-between-string-slice-and-string-substring</a><div id="articleHeader"><h1>What is the difference between String.slice and String.substring?</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        538
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>148</b></div>


</div>

            </div>

            
<div>
    <div>

<p>Does anyone know what the difference is between these two methods:</p>

<pre><code>String.slice
String.substring</code></pre>
    </div>
    
    
</div>

                
    <div>
	    <div id="comments-2243824">
                <ul>



    <li id="comment-2203099">
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
                It's an example of the poor design of JavaScript that we ended up with three methods that all do the same thing, but with different quirks. IMO <code>slice</code> is the one with the least unexpected behaviour.
                    – <a href="/users/18936/bobince" title="416,507 reputation" target="_blank">bobince</a>
                <a href="#comment2203099_2243824" target="_blank">Feb 11 '10 at 15:53</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-7783141">
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
                IMO substring when used to take a substring from idx till end is more understandable at a glance. Especially to noobs
                    – <a href="/users/295783/mplungjan" title="77,152 reputation" target="_blank">mplungjan</a>
                <a href="#comment7783141_2243824" target="_blank">Jul 6 '11 at 13:12</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-22639587">
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
                The <code>slice</code> & <code>substring</code> methods are all most the same; except the that the <code>slice()</code> accepts a negative index, relative to the end of the string, but not the <code>substring</code>, it throws <code>out-of-bound</code> error
                    – <a href="/users/1933917/amol-m-kulkarni" title="10,207 reputation" target="_blank">Amol M Kulkarni</a>
                <a href="#comment22639587_2243824" target="_blank">Apr 9 '13 at 9:46</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-25803509">
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
                @AmolMKulkarni Not true at all. If you try <code>var a = "asdf".substring(-1);</code>, it's treated as <code>var a = "asdf".substring(0);</code>. There's no exception thrown. And if you use <code>var a = "asdf".substring(2, -1);</code>, it uses <code>0</code> in place of <code>-1</code> (like before), and swaps the arguments so it acts like <code>var a = "asdf".substring(0, 2);</code>. I even tried these on IE 8 and got the results with no exceptions
                    – <a href="/users/1317927/ian" title="36,542 reputation" target="_blank">Ian</a>
                <a href="#comment25803509_2243824" target="_blank">Jul 17 '13 at 17:38</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-46338593">
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
                "I even tried these on IE 8" - I love programming.
                    – <a href="/users/3933502/quemeful" title="4,960 reputation" target="_blank">quemeful</a>
                <a href="#comment46338593_2243824" target="_blank">Mar 14 '15 at 14:55</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>        </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-2243835">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        609
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><code>slice()</code> works like <code>substring()</code> with a few different behaviors.</p>

<pre><code>Syntax: string.slice(start, stop);
Syntax: string.substring(start, stop);</code></pre>

<p><strong>What they have in common:</strong></p>

<ol>
<li>If <code>start</code> equals <code>stop</code>: returns an empty string</li>
<li>If <code>stop</code> is omitted: extracts characters to the end of the string</li>
<li>If either argument is greater than the string's length, the string's length will be used instead.</li>
</ol>

<p><strong>Distinctions of</strong> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring" target="_blank"><code>substring()</code></a><strong>:</strong></p>

<ol>
<li>If <code>start &gt; stop</code>, then <code>substring</code> will swap those 2 arguments.</li>
<li>If either argument is negative or is <code>NaN</code>, it is treated as if it were <code>0</code>.</li>
</ol>

<p><strong>Distinctions of</strong> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice" target="_blank"><code>slice()</code></a><strong>:</strong></p>

<ol>
<li>If <code>start &gt; stop</code>, <code>slice()</code> will NOT swap the 2 arguments.</li>
<li>If <code>start</code> is negative: sets char from the end of string, exactly like <code>substr()</code> in Firefox. This behavior is observed in both Firefox and IE.</li>
<li>If <code>stop</code> is negative: sets stop to: <code>string.length – Math.abs(stop)</code> (original value).</li>
</ol>

<p>Source: <a href="http://rapd.wordpress.com/2007/07/12/javascript-substr-vs-substring/" target="_blank">Rudimentary Art of Programming & Development: Javascript: substr() v.s. substring()</a></p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-2243835">
                <ul>



    <li id="comment-11698739">
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
                In your last note on <code>slice()</code>, it should be <code>string.length - stop</code>
                    – <a href="/users/15788/andy" title="962 reputation" target="_blank">Andy</a>
                <a href="#comment11698739_2243835" target="_blank">Feb 14 '12 at 15:16</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-16388510">
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
                In your last note on <code>slice()</code>, I think it should be <code>(string.length – 1) + stop</code> or, to make it clear that it's negative, <code>(string.length – 1) – Math.abs(stop)</code>
                    – <a href="/users/1529630/oriol" title="134,108 reputation" target="_blank">Oriol</a>
                <a href="#comment16388510_2243835" target="_blank">Sep 1 '12 at 17:46</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-19878632">
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
                @Longpoke: <code>String.slice</code> was added so that there is a string method consistent to <code>Array.slice</code>. <code>substring</code> has been there forever, so they didn’t break it and added another method. Hardly a crappy decision as 1. consistency is nice and 2. it allows CoffeeScript’s slicing syntax to work on arrays and strings. @Oriol: edited it in.
                    – <a href="/users/247482/flying-sheep" title="3,812 reputation" target="_blank">flying sheep</a>
                <a href="#comment19878632_2243835" target="_blank">Jan 13 '13 at 21:34</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-25811750">
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
                It seems there's a performance difference between substring and slice in Firefox 22.  <a href="http://jsperf.com/string-slice-vs-substring" target="_blank">jsperf.com/string-slice-vs-substring</a>
                    – <a href="/users/210874/rick" title="397 reputation" target="_blank">Rick</a>
                <a href="#comment25811750_2243835" target="_blank">Jul 17 '13 at 21:29</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-43214968">
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
                Andy was right. <code>stop</code> will be set to <code>string.length + stop</code> if <code>stop</code> is negative. Remember <code>stop</code> is the index after the last character extracted!
                    – <a href="/users/1537366/user1537366" title="657 reputation" target="_blank">user1537366</a>
                <a href="#comment43214968_2243835" target="_blank">Dec 9 '14 at 15:53</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-24040304">
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
<p>The one answer is fine, but requires a little reading into.  Especially with the new terminology "stop".</p>

<p>My Go -- organized by differences to make it useful in addition to the first answer by Daniel above:</p>

<p>1) negative indexes.  Substring requires positive indexes, and will set a negative index to 0.  Slice's nagative index means the position from the end of the string.</p>

<pre><code>"1234".substring(-2, -1) == "1234".substring(0,0) == ""
"1234".slice(-2, -1) == "1234".slice(2, 3) == "3"</code></pre>

<p>2) Swaping of indexes.  Substring will reorder the indexes to make the first index less than or equal to the second index.</p>

<pre><code>"1234".substring(3,2) == "1234".substring(2,3) == "3"
"1234".slice(3,2) == ""</code></pre>

<h2>--------------------------</h2>

<p>General comment -- I find it weird that the second index is the position after the last character of the slice or substring.  I would expect "1234".slice(2,2) to return "3".  This makes Andy's confusion above justified -- I would expect "1234".slice(2, -1) to return "34".  Yes, this means I'm new to Javascript.  This means also this behavior:</p>

<pre><code>"1234".slice(-2, -2) == "", "1234".slice(-2, -1) == "3", "1234".slice(-2, -0) == "" &lt;-- you have to use length or omit the argument to get the 4.
"1234".slice(3, -2) == "", "1234".slice(3, -1) == "", "1234".slice(3, -0) == "" &lt;-- same issue, but seems weirder.</code></pre>

<p>My 2c.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jun 4 '14 at 14:32
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-27320116">
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
<p>Ben Nadel has written a good article about this, he points out the difference in the parameters to these functions:</p>

<pre><code>String.slice( begin [, end ] )
String.substring( from [, to ] )
String.substr( start [, length ] )</code></pre>

<p>He also points out that if the parameters to slice are negative, they reference the string from the end. Substring and substr doesn´t. </p>

<p>Here is his article about this <a href="http://www.bennadel.com/blog/2159-using-slice-substring-and-substr-in-javascript.htm" target="_blank">http://www.bennadel.com/blog/2159-using-slice-substring-and-substr-in-javascript.htm</a></p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-27320116">
                <ul>



    <li id="comment-75382270">
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
                This is incorrect, substr does handle negative parameters.  <code>'0123456789'.substr(-3, 2) -&gt; '78'</code>
                    – <a href="/users/154079/neil-fraser" title="699 reputation" target="_blank">Neil Fraser</a>
                <a href="#comment75382270_27320116" target="_blank">May 25 '17 at 15:22</a>
                        
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-31910656">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        61
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Note: if you're in a hurry, and/or looking for short answer scroll to the bottom of the answer, and read the last two lines.if Not in a hurry read the whole thing.<br /><br /><br />let me start by stating the facts:</p>

<p>Syntax:<br />
<code>string.slice(start,end)</code><br />
<code>string.substr(start,length)</code><br />
<code>string.substring(start,end)</code><br />
Note #1: <code>slice()==substring()</code></p>

<p>What it does?<br />
The <code>slice()</code> method extracts parts of a string and returns the extracted parts in a new string.<br />
The <code>substr()</code> method extracts parts of a string, beginning at the character at the specified position, and returns the specified number of characters.<br />
The <code>substring()</code> method extracts parts of a string and returns the extracted parts in a new string.<br />
Note #2:<code>slice()==substring()</code></p>

<p>Changes the Original String?<br />
<code>slice()</code> Doesn't<br />
<code>substr()</code> Doesn't<br />
<code>substring()</code> Doesn't<br />
Note #3:<code>slice()==substring()</code></p>

<p>Using Negative Numbers as an Argument:<br />
<code>slice()</code> selects characters starting from the end of the string<br />
<code>substr()</code>selects characters starting from the end of the string<br />
<code>substring()</code> Doesn't Perform<br />
Note #3:<code>slice()==substr()==substr()</code></p>

<p>if the First Argument is Greater than the Second:<br />
<code>slice()</code> Doesn't Perform<br />
<code>substr()</code> since the Second Argument is NOT a position, but length value, it will perform as usual, with no problems<br />
<code>substring()</code> will swap the two arguments, and perform as usual</p>

<p>the First Argument:<br />
<code>slice()</code> Required, indicates: Starting Index<br />
<code>substr()</code> Required, indicates: Starting Index<br />
<code>substring()</code> Required, indicates: Starting Index<br />
Note #4:<code>slice()==substr()==substring()</code></p>

<p>the Second Argument:<br />
<code>slice()</code> Optional, The position (up to, but not including) where to end the extraction<br />
<code>substr()</code> Optional, The number of characters to extract<br />
<code>substring()</code> Optional, The position (up to, but not including) where to end the extraction<br />
Note #5:<code>slice()==substring()</code></p>

<p>What if the Second Argument is Omitted?<br />
<code>slice()</code> selects all characters from the start-position to the end of the string<br />
<code>substr()</code> selects all characters from the start-position to the end of the string<br />
<code>substring()</code> selects all characters from the start-position to the end of the string<br />
Note #6:<code>slice()==substr()==substring()</code></p>

<p>so, you can say that there's a difference between <code>slice()</code> and <code>substr()</code>, while <code>substring()</code> is basically a copy of <code>slice()</code>.</p>

<p>in Summary:<br />
if you know the index(the position) on which you'll stop (but NOT include), Use <code>slice()</code><br />
if you know the length of characters to be extracted use <code>substr()</code>.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 10 '15 at 1:58
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-35226646">
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
<p>The difference between substring and slice - is how they work with negative and overlooking lines abroad arguments:</p>

<p><strong>substring (start, end)</strong></p>

<p>Negative arguments are interpreted as zero. Too large values ​​are truncated to the length of the string:
 
    alert ( "testme" .substring (-2)); // "testme", -2 becomes 0</p>

<p>Furthermore, if start &gt; end, the arguments are interchanged, i.e. plot line returns between the start and end:</p>

<pre><code>alert ( "testme" .substring (4, -1)); // "test"
// -1 Becomes 0 -&gt; got substring (4, 0)
// 4&gt; 0, so that the arguments are swapped -&gt; substring (0, 4) = "test"</code></pre>

<p><strong>slice</strong></p>

<p>Negative values ​​are measured from the end of the line:</p>

<pre><code>alert ( "testme" .slice (-2)); // "me", from the end position 2
alert ( "testme" .slice (1, -1)); // "estm", from the first position to the one at the end.</code></pre>

<p>It is much more convenient than the strange logic substring.</p>

<p>A negative value of the first parameter to substr supported in all browsers except IE8-.</p>

<p>If the choice of one of these three methods, for use in most situations - it will be <strong><em>slice</em></strong>: negative arguments and it maintains and operates most obvious.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Feb 5 '16 at 14:32
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-37415301">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>The only difference between slice and substring method is of arguments</p>

<p>Both take two arguments e.g. start/from and end/to.</p>

<p>You cannot pass a negative value as first argument for <strong>substring</strong> method but for <strong>slice</strong> method to traverse it from end.</p>

<p>Slice method argument details:</p>

<p>REF: 
<a href="http://www.thesstech.com/javascript/string_slice_method" target="_blank">http://www.thesstech.com/javascript/string_slice_method</a></p>

<p><strong>Arguments</strong></p>

<p><strong>start_index</strong>
Index from where slice should begin. If value is provided in negative it means start from last. e.g. -1 for last character.
<strong>end_index</strong>
Index after end of slice. If not provided slice will be taken from start_index to end of string. In case of negative value index will be measured from end of string.</p>

<p>Substring method argument details:</p>

<p>REF: <a href="http://www.thesstech.com/javascript/string_substring_method" target="_blank">http://www.thesstech.com/javascript/string_substring_method</a></p>

<p><strong>Arguments</strong></p>

<p><strong>from</strong>
It should be a non negative integer to specify index from where sub-string should start.
<strong>to</strong>
An optional non negative integer to provide index before which sub-string should be finished.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 24 '16 at 13:37
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-43085096">
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
<p>For slice(start, stop), if stop is negative, stop will be set to: string.length – Math.abs(stop), rather (string.length – 1) – Math.abs(stop).</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 29 '17 at 5:32
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-45432051">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<h1>-------------------------------------- <strong>Differences</strong> --------------------------------------</h1>

<blockquote>
  <h1><strong><em><code>String.prototype.slice</code></em></strong></h1>
  
  <h3><strong>Treatment of negative indices</strong></h3>
  
  <ul>
  <li><b>"</b> If [<em>either argument is</em>] negative, it is treated as <code>strLength +</code> [<em><code>index</code></em>] where <code>strLength</code> is the length of the string (for example, if [<em><code>index</code></em>] is <code>-3</code> it is treated as <code>strLength - 3</code>). <b>"</b></li>
  </ul>
  
  <h3><strong>Starting index greater than ending index</strong></h3>
  
  <ul>
  <li><p><b>"</b> If [<em>the starting index</em>] is greater than <strong>or equal</strong> to the [<em>treatment of the ending index</em>] of the [<em>string slice</em>], <code>slice()</code> returns an empty string. <b>"</b></p>
  
  <p>-- <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice" title="String.prototype.slice -- Mozilla Developer Network" target="_blank">MDN</a>
  </p></li>
  </ul>
</blockquote>

<hr />

<blockquote>
  <h1><strong><em><code>String.prototype.substring</code></em></strong></h1>
  
  <h3><strong>Treatment of negative indices</strong></h3>
  
  <ul>
  <li><b>"</b> If either argument is [<em>negative</em>] [<em>...</em>], it is treated as if it were <code>0</code>. <b>"</b></li>
  </ul>
  
  <h3><strong>Starting index greater than ending index</strong></h3>
  
  <ul>
  <li><p><b>"</b> If [<em>the starting index</em>] is greater than [<em>the ending index</em>], then the<br /> effect of <code>substring()</code> is as if the two arguments were swapped; for example, <code>str.substring(1, 0) == str.substring(0, 1)</code>. <b>"</b></p>
  
  <p>-- <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring" title="String.prototype.substring -- Mozilla Developer Network" target="_blank">MDN</a></p></li>
  </ul>
</blockquote>

<h1>-------------------------------------- <strong>Similarities</strong> --------------------------------------</h1>

<p>Everything else is the same, I think, including:</p>

<ul>
<li>If an <strong>ending index</strong> argument is <code>undefined</code>, it becomes the length of the string.</li>
<li><strong>Arguments</strong> that are not numbers and cannot be coerced to numbers become <code>0</code>.</li>
</ul>

<p><sub>*The above is also true for the <code>substr()</code> method, except <code>substr()</code> does not have an ending index argument (<em>see notes under <code>String.prototype.substr</code></em>).
</sub></p>

<h1>------------------------------------------ <strong>Notes</strong> ------------------------------------------</h1>

<h2><code>String.prototype.substr</code></h2>

<p>[<em>slightly beyond the scope of the question</em>]</p>

<ul>
<li><strong><code>String.prototype.substr</code></strong> is very much like <code>slice()</code>, especially with regards to the treatment of negative numbers for index values; however, the key difference is that <code>substr()</code>'s second argument does not specify an ending index, but the length of characters the caller wants returned. Suffice it to say that <code>substr()</code> behaves as predictably as <code>slice()</code> does beyond that key difference; passing a negative <code>length</code> argument returns an empty string with this method.</li>
</ul>

<hr />
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/substring" title="show questions tagged 'substring'" target="_blank">substring</a> <a href="/questions/tagged/slice" title="show questions tagged 'slice'" target="_blank">slice</a> <a href="/questions/tagged/substr" title="show questions tagged 'substr'" target="_blank">substr</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
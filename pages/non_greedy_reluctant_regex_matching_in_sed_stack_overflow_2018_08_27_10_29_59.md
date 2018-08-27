<a href="https://stackoverflow.com/questions/1103149/non-greedy-reluctant-regex-matching-in-sed">https://stackoverflow.com/questions/1103149/non-greedy-reluctant-regex-matching-in-sed</a><div id="articleHeader"><h1>Non greedy (reluctant) regex matching in sed?</h1></div>

            

<div id="question">

    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        337
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>87</b></div>



</div>

            </div>

            
<div>
    <div>

<p>I'm trying to use sed to clean up lines of URLs to extract just the domain..</p>

<p>So from:</p>

<pre><code>http://www.suepearson.co.uk/product/174/71/3816/</code></pre>

<p>I want:</p>

<p><a href="http://www.suepearson.co.uk/" target="_blank">http://www.suepearson.co.uk/</a></p>

<p>(either with or without the trainling slash, it doesn't matter)</p>

<p>I have tried:</p>

<pre><code> sed 's|\(http:\/\/.*?\/\).*|\1|'</code></pre>

<p>and (escaping the non greedy quantifier)</p>

<pre><code>sed 's|\(http:\/\/.*\?\/\).*|\1|'</code></pre>

<p>but I can not seem to get the non greedy quantifier to work, so it always ends up matching the whole string.</p>
    </div>
    
    <div>
    

    
    <div>
<div>
    <div>
        asked Jul 9 '09 at 10:47
    </div>
    
    
</div>

    </div>
    </div>
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-1103177">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        354
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted


</div>

            </div>
            


<div>
    <div>
<p>Neither basic nor extended Posix/GNU regex recognizes the non-greedy quantifier; you need a later regex.  Fortunately, Perl regex for this context is pretty easy to get:</p>

<pre><code>perl -pe 's|(http://.*?/).*|\1|'</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-51048193">
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
<p>This is how to robustly do non-greedy matching of multi-character strings using sed. Lets say you want to change every <code>foo...bar</code> to <code>&lt;foo...bar&gt;</code> so for example this input:</p>

<pre><code>$ cat file
ABC foo DEF bar GHI foo KLM bar NOP foo QRS bar TUV</code></pre>

<p>should become this output:</p>

<pre><code>ABC &lt;foo DEF bar&gt; GHI &lt;foo KLM bar&gt; NOP &lt;foo QRS bar&gt; TUV</code></pre>

<p>To do that you convert foo and bar to individual characters and then use the negation of those characters between them:</p>

<pre><code>$ sed 's/@/@A/g; s/{/@B/g; s/}/@C/g; s/foo/{/g; s/bar/}/g; s/{[^{}]*}/&lt;&&gt;/g; s/}/bar/g; s/{/foo/g; s/@C/}/g; s/@B/{/g; s/@A/@/g' file
ABC &lt;foo DEF bar&gt; GHI &lt;foo KLM bar&gt; NOP &lt;foo QRS bar&gt; TUV</code></pre>

<p>In the above:</p>

<ol>
<li><code>s/@/@A/g; s/{/@B/g; s/}/@C/g</code> is converting <code>{</code> and <code>}</code> to placeholder strings that cannot exist in the input so those chars then are available to convert <code>foo</code> and <code>bar</code> to.</li>
<li><code>s/foo/{/g; s/bar/}/g</code> is converting <code>foo</code> and <code>bar</code> to <code>{</code> and <code>}</code> respectively</li>
<li><code>s/{[^{}]*}/&lt;&&gt;/g</code> is performing the op we want - converting <code>foo...bar</code> to <code>&lt;foo...bar&gt;</code></li>
<li><code>s/}/bar/g; s/{/foo/g</code> is converting <code>{</code> and <code>}</code> back to <code>foo</code> and <code>bar</code>.</li>
<li><code>s/@C/}/g; s/@B/{/g; s/@A/@/g</code> is converting the placeholder strings back to their original characters.</li>
</ol>

<p>Note that the above does not rely on any particular string not being present in the input as it manufactures such strings in the first step, nor does it care which occurrence of any particular regexp you want to match since you can use <code>{[^{}]*}</code> as many times as necessary in the expression to isolate the actual match you want and/or with seds numeric match operator, e.g. to only replace the 2nd occurrence:</p>

<pre><code>$ sed 's/@/@A/g; s/{/@B/g; s/}/@C/g; s/foo/{/g; s/bar/}/g; s/{[^{}]*}/&lt;&&gt;/2; s/}/bar/g; s/{/foo/g; s/@C/}/g; s/@B/{/g; s/@A/@/g' file
ABC foo DEF bar GHI &lt;foo KLM bar&gt; NOP foo QRS bar TUV</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-19683076">
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
<h2>Non-greedy solution for more than a single character</h2>

<p>This thread is really old but I assume people still needs it.
Lets say you want to kill everything till the very first occurrence of <code>HELLO</code>. You cannot say <code>[^HELLO]</code>...</p>

<p>So a nice solution involves two steps, assuming that you can spare a unique word that you are not expecting in the input, say <code>top_sekrit</code>.</p>

<p>In this case we can:</p>

<pre><code>s/HELLO/top_sekrit/     #will only replace the very first occurrence
s/.*top_sekrit//        #kill everything till end of the first HELLO</code></pre>

<p>Of course, with a simpler input you could use a smaller word, or maybe even a single character.</p>


    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-46719361">
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
<p><a href="http://0x2a.at/blog/2008/07/sed--non-greedy-matching/" target="_blank">sed - non greedy matching by Christoph Sieghart</a></p>

<p>The trick to get non greedy matching in sed is to match all characters excluding the one that terminates the match. I know, a no-brainer, but I wasted precious minutes on it and shell scripts should be, after all, quick and easy. So in case somebody else might need it:</p>

<p>Greedy matching</p>

<pre><code>% echo "&lt;b&gt;foo&lt;/b&gt;bar" | sed 's/&lt;.*&gt;//g'
bar</code></pre>

<p>Non greedy matching</p>

<pre><code>% echo "&lt;b&gt;foo&lt;/b&gt;bar" | sed 's/&lt;[^&gt;]*&gt;//g'
foobar</code></pre>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered Oct 12 '17 at 21:45
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-44445086">
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
<p>Here is something you can do with a two step approach and awk:</p>

<pre><code>A=http://www.suepearson.co.uk/product/174/71/3816/  
echo $A|awk '  
{  
  var=gensub(///,"||",3,$0) ;  
  sub(/\|\|.*/,"",var);  
  print var  
}'  </code></pre>

<blockquote>
  <p>Output:
  <a href="http://www.suepearson.co.uk" target="_blank">http://www.suepearson.co.uk</a></p>
</blockquote>

<p>Hope that helps!</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-39752929">
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
<h2>Simulating lazy (un-greedy) quantifier in <code>sed</code></h2>

<p><em>And all other regex flavors!</em></p>

<ol>
<li><p>Finding first occurrence of an expression:</p>

<ul>
<li><p><strong>POSIX ERE</strong> (using <code>-r</code> option)</p>

<p>Regex:</p>

<pre><code>(EXPRESSION).*|.</code></pre>



<pre><code>sed -r "s/(EXPRESSION).*|./\1/g" # Global `g` modifier should be on</code></pre>

<p>Example (finding first sequence of digits) <strong><a href="https://www.regex101.com/r/AHDm5F/1" target="_blank">Live demo</a></strong>:</p>

<pre><code>$ sed -r "s/([0-9]+).*|./\1/g" &lt;&lt;&lt; "foo 12 bar 34"</code></pre>



<pre><code>12</code></pre>

<p><strong>How does it work</strong>?</p>

<p>This regex benefits from an alternation <code>|</code>. At each position engine will look for the first side of alternation (our target) and if it is not matched second side of alternation which has a dot <code>.</code> matches the next immediate character. </p>



<p>Since global flag is set, engine tries to continue matching character by character up to the end of input string or our target. As soon as the first and only capturing group  of left side of alternation is matched <code>(EXPRESSION)</code> rest of line is consumed immediately as well <code>.*</code>. We now hold our value in the first capturing group.</p></li>
<li><p><strong>POSIX BRE</strong></p>

<p>Regex:</p>

<pre><code>\(\(\(EXPRESSION\).*\)*.\)*</code></pre>



<pre><code>sed "s/\(\(\(EXPRESSION\).*\)*.\)*/\3/"</code></pre>

<p>Example (finding first sequence of digits):</p>

<pre><code>$ sed "s/\(\(\([0-9]\{1,\}\).*\)*.\)*/\3/" &lt;&lt;&lt; "foo 12 bar 34"</code></pre>



<pre><code>12</code></pre>

<p>This one is like ERE version but with no alternation involved. That's all. At each single position engine tries to match a digit.</p>



<p>If it is found, other following digits are consumed and captured and the rest of line is matched immediately otherwise since <code>*</code> means
<em>more or zero</em> it skips over second capturing group <code>\(\([0-9]\{1,\}\).*\)*</code> and arrives at a dot <code>.</code> to match a single character and this process continues.</p></li>
</ul></li>
<li><p>Finding first occurrence of a <strong>delimited</strong> expression:</p>

<p>This approach will match the very first occurrence of a string that is delimited. We can call it a block of string. </p>

<pre><code>sed "s/\(END-DELIMITER-EXPRESSION\).*/\1/; \
     s/\(\(START-DELIMITER-EXPRESSION.*\)*.\)*/\1/g"</code></pre>

<p>Input string:</p>

<pre><code>foobar start block #1 end barfoo start block #2 end</code></pre>

<p>-EDE: <code>end</code></p>

<p>-SDE: <code>start</code></p>

<pre><code>$ sed "s/\(end\).*/\1/; s/\(\(start.*\)*.\)*/\1/g"</code></pre>

<p>Output:</p>

<pre><code>start block #1 end</code></pre>

<p>First regex <code>\(end\).*</code> matches and captures first end delimiter <code>end</code> and substitues all match with recent captured characters which
is the end delimiter. At this stage our output is: <code>foobar start block #1 end</code>.</p>



<p>Then the result is passed to second regex <code>\(\(start.*\)*.\)*</code> that is same as POSIX BRE version above. It matches a single character
if start delimiter <code>start</code> is not matched otherwise it matches and captures the start delimiter and matches the rest of characters.</p>

</li>
</ol>

<hr />

<h2>Directly answering your question</h2>

<p>Using approach #2 (delimited expression) you should select two appropriate expressions:</p>

<ul>
<li><p>EDE: <code>[^:/]\/</code></p></li>
<li><p>SDE: <code>http:</code></p></li>
</ul>

<p>Usage: </p>

<pre><code>$ sed "s/\([^:/]\/\).*/\1/g; s/\(\(http:.*\)*.\)*/\1/" &lt;&lt;&lt; "http://www.suepearson.co.uk/product/174/71/3816/"</code></pre>

<p>Output:</p>

<pre><code>http://www.suepearson.co.uk/</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-38699423">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>





</div>

            </div>
            


<div>
    <div>
<p>There is still hope to solve this using pure (GNU) sed. Despite this is not a generic solution in some cases you can use "loops" to eliminate all the unnecessary parts of the string like this:</p>

<pre><code>sed -r -e ":loop" -e 's|(http://.+)/.*|\1|' -e "t loop"</code></pre>

<ul>
<li>-r: Use extended regex (for + and unescaped parenthesis)</li>
<li>":loop": Define a new label named "loop"</li>
<li>-e: add commands to sed</li>
<li>"t loop": Jump back to label "loop" if there was a successful substitution</li>
</ul>

<p>The only problem here is it will also cut the last separator character ('/'), but if you really need it you can still simply put it back after the "loop" finished, just append this additional command at the end of the previous command line:</p>

<pre><code>-e "s,$,/,"</code></pre>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered Aug 1 '16 at 12:52
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-35142758">
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
<p>Another sed version:</p>

<pre><code>sed 's|/[:alphanum:].*||' file.txt</code></pre>

<p>It matches <code>/</code> followed by an alphanumeric character (so not another forward slash) as well as the rest of characters till the end of the line. Afterwards it replaces it with nothing (ie. deletes it.)</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-1103159">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        200
        <a title="This answer is not useful" target="_blank">down vote</a>





</div>

            </div>
            


<div>
    <div>
<p>Try <code>[^/]*</code> instead of <code>.*?</code>:</p>

<pre><code>sed 's|\(http://[^/]*/\).*|\1|g'</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-13982225">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        95
        <a title="This answer is not useful" target="_blank">down vote</a>





</div>

            </div>
            


<div>
    <div>
<p>With sed, I usually implement non-greedy search by searching for anything except the separator until the separator :</p>

<pre><code>echo "http://www.suon.co.uk/product/1/7/3/" | sed -n 's;\(http://[^/]*\)/.*;\1;p'</code></pre>

<p>Output:</p>

<pre><code>http://www.suon.co.uk</code></pre>

<p>this is:</p>

<ul>
<li>don't output <code>-n</code></li>
<li>search, match pattern, replace and print <code>s/&lt;pattern&gt;/&lt;replace&gt;/p</code></li>
<li>use <code>;</code> search command separator instead of <code>/</code> to make it easier to type so <code>s;&lt;pattern&gt;;&lt;replace&gt;;p</code></li>
<li>remember match between brackets <code>\(</code> ... <code>\)</code>, later accessible with <code>\1</code>,<code>\2</code>...</li>
<li>match <code>http://</code></li>
<li>followed by anything in brackets <code>[]</code>, <code>[ab/]</code> would mean either <code>a</code> or <code>b</code> or <code>/</code> </li>
<li>first <code>^</code> in <code>[]</code> means <code>not</code>, so followed by anything but the thing in the <code>[]</code></li>
<li>so <code>[^/]</code> means anything except <code>/</code> character</li>
<li><code>*</code> is to repeat previous group so <code>[^/]*</code> means characters except <code>/</code>.</li>
<li>so far <code>sed -n 's;\(http://[^/]*\)</code> means search and remember <code>http://</code>followed by any characters except <code>/</code> and remember what you've found</li>
<li>we want to search untill the end of domain so stop on the next <code>/</code> so add another <code>/</code> at the end: <code>sed -n 's;\(http://[^/]*\)/'</code> but we want to match the rest of the line after the domain so add <code>.*</code></li>
<li>now the match remembered in group 1 (<code>\1</code>) is the domain so replace matched line with stuff saved in group <code>\1</code> and print: <code>sed -n 's;\(http://[^/]*\)/.*;\1;p'</code> </li>
</ul>

<p>If you want to include backslash after the domain as well, then add one more backslash in the group to remember:</p>

<pre><code>echo "http://www.suon.co.uk/product/1/7/3/" | sed -n 's;\(http://[^/]*/\).*;\1;p'</code></pre>

<p>output:</p>

<pre><code>http://www.suon.co.uk/</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-21610775">
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
<p>Because you specifically stated you're trying to use sed (instead of perl, cut, etc.), try grouping. This circumvents the non-greedy identifier potentially not being recognized. The first group is the protocol (i.e. 'http://', 'https://', 'tcp://', etc). The second group is the domain: </p>

<pre>echo "http://www.suon.co.uk/product/1/7/3/" | sed "s|^\(.*//\)\([^/]*\).*$|\1\2|"
</pre>

<p>If you're not familiar with grouping, start <a href="https://stackoverflow.com/questions/11650940/sed-how-to-do-regex-groups-using-sed" target="_blank">here</a>.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-18535624">
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
<p><code>sed</code> certainly has its place but this not not one of them !</p>

<p>As Dee has pointed out:  Just use <code>cut</code>. It is far simpler and much more safe in this case. Here's an example where we extract various components from the URL using Bash syntax:</p>

<pre><code>url="http://www.suepearson.co.uk/product/174/71/3816/"

protocol=$(echo "$url" | cut -d':' -f1)
host=$(echo "$url" | cut -d'/' -f3)
urlhost=$(echo "$url" | cut -d'/' -f1-3)
urlpath=$(echo "$url" | cut -d'/' -f4-)</code></pre>

<p>gives you:</p>

<pre><code>protocol = "http"
host = "www.suepearson.co.uk"
urlhost = "http://www.suepearson.co.uk"
urlpath = "product/174/71/3816/"</code></pre>

<p>As you can see this is a lot more flexible approach.</p>

<p>(all credit to Dee)</p>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered Aug 30 '13 at 14:41
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-17279357">
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
<p><code>sed 's|\(http:\/\/www\.[a-z.0-9]*\/\).*|\1|</code> works too</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-4404719">
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
<p>This can be done using cut:</p>

<pre><code>echo "http://www.suepearson.co.uk/product/174/71/3816/" | cut -d'/' -f1-3</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-4404815">
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
<pre><code>echo "/home/one/two/three/myfile.txt" | sed 's|\(.*\)/.*|\1|'</code></pre>

<p>don bother, i got it on another forum :)</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-6523482">
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
<p>I realize this is an old entry, but someone may find it useful.
As the full domain name may not exceed a total length of 253 characters replace .* with .\{1, 255\}</p>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered Jun 29 '11 at 15:49
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-1103282">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>





</div>

            </div>
            


<div>
    <div>
<p>sed -E interprets regular expressions as extended (modern) regular expressions</p>

<p>Update: -E on MacOS X, -r in GNU sed.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-1103226">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        34
        <a title="This answer is not useful" target="_blank">down vote</a>





</div>

            </div>
            


<div>
    <div>
<p>sed does not support "non greedy" operator.</p>

<p>You have to use "[]" operator to exclude "/" from match.</p>

<pre><code>sed 's,\(http://[^/]*\)/.*,\1,'</code></pre>

<p>P.S. there is no need to backslash "/".</p>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered Jul 9 '09 at 11:08
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-1103182">
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
<p>another way, not using regex, is to use fields/delimiter method eg</p>

<pre><code>string="http://www.suepearson.co.uk/product/174/71/3816/"
echo $string | awk -F"/" '{print $1,$2,$3}' OFS="/"</code></pre>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered Jul 9 '09 at 10:59
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-1103179">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>





</div>

            </div>
            


<div>
    <div>
<pre><code>sed 's|(http:\/\/[^\/]+\/).*|\1|'</code></pre>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered Jul 9 '09 at 10:58
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/regex" title="show questions tagged 'regex'" target="_blank">regex</a> <a href="/questions/tagged/sed" title="show questions tagged 'sed'" target="_blank">sed</a> <a href="/questions/tagged/pcre" title="show questions tagged 'pcre'" target="_blank">pcre</a> <a href="/questions/tagged/greedy" title="show questions tagged 'greedy'" target="_blank">greedy</a> <a href="/questions/tagged/regex-greedy" title="show questions tagged 'regex-greedy'" target="_blank">regex-greedy</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="https://stackoverflow.com/questions/27753246/match-vs-exec-in-javascript">https://stackoverflow.com/questions/27753246/match-vs-exec-in-javascript</a><div id="articleHeader"><h1>match Vs exec in JavaScript</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        16
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>10</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<div>
    <p>This question already has an answer here:</p>
    <ul>
        <li>
            <a href="/questions/9214754/what-is-the-difference-between-regexp-s-exec-function-and-string-s-match-fun" target="_blank">What is the difference between RegExp’s exec() function and String’s match() function?</a>
                
                    4 answers
                
        </li>
    </ul>
    </div>
<p>I need some clarification for match Vs exec in JavaScript; <a href="https://stackoverflow.com/questions/9214754/what-is-the-difference-between-regexp-s-exec-function-and-string-s-match-fun" target="_blank">here</a> some one says that </p>

<p><em>"exec with a global regular expression is meant to be used in a loop"</em> but first of all as you see in my example this is not the case; in my example exec with global regular expression is returning all of the matches in an array! Secondly they say that for String.match it returns all of the matches with  no need of looping through! But again that's not happening in my example and it is just returning the input string? Have I misunderstood/done something wrong?</p>

<pre><code>var myString = "[22].[44].[33].";
var myRegexp = /.*\[(\d*)*\].*\[(\d*)*\].*\[(\d*)*\].*/g;

var execResult = myRegexp.exec(myString);
console.log(execResult.length);
console.log(execResult[1]);// returns 22 and execResult has all of my matches from index 1 to the length of array


var matchResult = myString.match(myRegexp);
console.log(matchResult.length);
console.log(matchResult);// returns just myString which is "[22].[44].[33]."! Why is that?</code></pre>
    </div>
    
    
</div>
</td>
        </tr>
                    <tr>
            <td colspan="2">
                <div>
        <h2>                    <b>marked</b> as duplicate by <a href="/users/465053/rbt" target="_blank">RBT</a>, <a href="/users/3155639/alexander-omara" target="_blank">Alexander O'Mara</a><a href="/badges/tag-badges/javascript?badgeClass=Gold" target="_blank"> javascript</a>

 Jul 17 '17 at 5:29
</h2>
        <p>This question has been asked before and already has an answer. If those answers do not fully address your question, please <a href="/questions/ask" target="_blank">ask a new question</a>.</p>
    </div>
            </td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-27753246">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-27753327">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        35
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<ol>
<li><p><code>string.match</code> finds the first match and returns it with the actual match, the index at which the text was found and the actual input, <em>when the global flag is not used.</em></p></li>
<li><p><code>string.match</code> just returns all the matches, <em>when the global flag is used.</em></p>

<pre><code>var myString = "[22].[44].[33].";

console.log(myString.match(/\d+/));
# [ '22', index: 1, input: '[22].[44].[33].' ]
console.log(myString.match(/\d+/g));
# [ '22', '44', '33' ]</code></pre></li>
</ol>

<p><strong>The main difference between <code>string.match</code> and <code>regex.exec</code> is, the <code>regex</code> object will be updated of the current match with <code>regex.exec</code> call.</strong> For example,</p>

<pre><code>var myString = "[22].[44].[33].", myRegexp = /\d+/g, result;

while (result = myRegexp.exec(myString)) {
    console.log(result, myRegexp.lastIndex);
}</code></pre>

<p>will return</p>

<pre><code>[ '22', index: 1, input: '[22].[44].[33].' ] 3
[ '44', index: 6, input: '[22].[44].[33].' ] 8
[ '33', index: 11, input: '[22].[44].[33].' ] 13</code></pre>

<p>As you can see, the <code>lastIndex</code> property is updated whenever a match is found. So, keep two things in mind when you use <code>exec</code>, or <strong>you will run into an infinite loop.</strong></p>

<ol>
<li><p>If you don't use <code>g</code> option, then you will always get the first match, if there is one, otherwise <code>null</code>. So, the following will run into an infinite loop.</p>

<pre><code>var myString = "[22].[44].[33].", myRegexp = /\d+/, result;

while (result = myRegexp.exec(myString)) {
    console.log(result, myRegexp.lastIndex);
}</code></pre></li>
<li><p>Don't forget to use the same regular expression object with subsequent calls. Because, the regex object is updated every time, and if you pass new object, again the program will run into an infinite loop.</p>

<pre><code>var myString = "[22].[44].[33].", result;

while (result = /\d+/g.exec(myString)) {
    console.log(result);
}</code></pre></li>
</ol>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-27753327">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-37187900">
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
<p><code>String.prototype.match()</code> and <code>RegExp.prototype.exec()</code> are similar in both finding multiple occurrences and returning them in an array. Yet exec method returns an array of more detailed information. For instance unlike match it can find multiple occurrences of the capture groups as well. So if you have capture groups, exec is essential. One thing to keep in mind when working with exec you shouldn't invoke if from a literal regexp. Assign your regex to a variable first and use it to call your exec method from. One other thing is, while match would bring multiple occurrences in an array of items at one go, with exec you have to iterate for each occurrence to be captured.</p>

<p>Invoking match is fairly simple. Since it is a string prototype method you just chain it to a string and provide a regexp as an argument to the match method like; "test".match(/es/) A literal representation of a regex can be used with no problem.</p>

<p>Invoking exec is more complicated. As i mentioned previously it's best to have the regex assigned to something previously. Ok lets see an example</p>

<div>
<div>
<pre><code>var text = '["job name 1","nat 1"],["job name 2","nat 2"],["job name 3","nat 3"]',
     reg = /([^"]+)","([^"]+)/g,
      tm = [],
      te = [];

tm = text.match(reg); // tm has result of match
while(te[te.length]=reg.exec(text)); // te has result of exec + an extra null item at the end
te.length--; // te normalized.

document.write("&lt;pre&gt;" + JSON.stringify(tm,null,2) + "&lt;/pre&gt;\n");
document.write("&lt;pre&gt;" + JSON.stringify(te,null,2) + "&lt;/pre&gt;\n");</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
<p>As you see exec's result also includes the capture groups. The way i choose to populate <code>te</code> array is somewhat unorthodox but i hate to use a temp array just in the conditional part of while loop. This looks to me much more neat. The only thing is, the final null to stop the while loop gets inserted to the end of <code>te</code> array. Hence the following <code>te.length--</code> instruction.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-37187900">
		        <table>
                    <tbody>



    <tr id="comment-65854682">
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
                I believe it's misleading to say "So if you have capture groups, exec is essential", since <code>.match()</code> clearly does return an array of all specified captured groups. You imply as much in your first sentence and you obviously know how each works. Maybe you mean something more along the lines of "if you need to recursively apply one or more capture groups, using the global flag and <code>.exec()</code> are essential"?
                    – <a href="/users/5641202/ben-fletcher" title="395 reputation" target="_blank">Ben Fletcher</a>
                <a href="#comment65854682_37187900" target="_blank">Aug 31 '16 at 21:32</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-37187900">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                


            </div>
        
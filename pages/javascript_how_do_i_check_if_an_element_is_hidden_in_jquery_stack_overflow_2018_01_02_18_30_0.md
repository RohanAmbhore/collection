<a href="https://stackoverflow.com/questions/178325/how-do-i-check-if-an-element-is-hidden-in-jquery">https://stackoverflow.com/questions/178325/how-do-i-check-if-an-element-is-hidden-in-jquery</a><div id="articleHeader"><h1>How do I check if an element is hidden in jQuery?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        6244
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>776</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>It is possible to toggle the visibility of an element, using the functions <code>.hide()</code>, <code>.show()</code> or <code>.toggle()</code>.</p>

<p>How would you test if an element is visible or hidden?</p>
    </div>
    
    
</div>
</td>
        </tr>
                    <tr>
            <td colspan="2">
                <div>
        <h2>                    <b>protected</b> by <a href="/users/707111/ryan" target="_blank">Ryan</a>♦ Apr 13 '12 at 3:09
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
	    <div id="comments-178325">
		        <table>
                    <tbody>



    <tr id="comment-44145892">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                26
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
                It's worth mentioning (even after all this time), that <code>$(element).is(":visible")</code> works for jQuery 1.4.4, but not for jQuery 1.3.2, under <a href="http://en.wikipedia.org/wiki/Internet_Explorer_8" target="_blank">Internet&nbsp;Explorer&nbsp;8</a>. This can be tested using <a href="http://stackoverflow.com/questions/178325/testing-if-something-is-hidden-with-jquery/178450#178450" target="_blank">Tsvetomir Tsonev's helpful test snippet</a>. Just remember to change the version of jQuery, to test under each one.
                    – <a href="/users/343614/reuben" title="2,518 reputation" target="_blank">Reuben</a>
                <a href="#comment44145892_178325" target="_blank">Feb 1 '11 at 3:57</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-178325">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>1</b> more comment</a>
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-178450">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7783
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>Since the question refers to a single element, this code might be more suitable:</p>

<pre><code>// Checks for display:[none|block], ignores visible:[true|false]
$(element).is(":visible"); </code></pre>

<p>Same as <a href="https://stackoverflow.com/questions/178325/how-do-you-test-if-something-is-hidden-in-jquery/178386#178386" target="_blank">twernt's suggestion</a>, but applied to a single element; and it <a href="https://stackoverflow.com/a/4685330/49942" target="_blank">matches the algorithm recommended in the jQuery FAQ</a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-178450">
		        <table>
                    <tbody>



    <tr id="comment-4996571">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                127
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
                This solution would seem to encourage the confustion of <code>visible=false</code> and <code>display:none</code>; whereas Mote's solution clearly illistrates the coders intent to check the <code>display:none</code>; (via mention of hide and show which control <code>display:none</code> not <code>visible=true</code>)
                    – <a href="/users/351980/kralco626" title="3,503 reputation" target="_blank">kralco626</a>
                <a href="#comment4996571_178450" target="_blank">Dec 29 '10 at 18:30</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-5073391">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                73
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
                That is correct, but <code>:visible</code> will also check if the parent elements are visible, as chiborg pointed out.
                    – <a href="/users/25449/tsvetomir-tsonev" title="81,234 reputation" target="_blank">Tsvetomir Tsonev</a>
                <a href="#comment5073391_178450" target="_blank">Jan 6 '11 at 12:30</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-5177770">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                33
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
                You have a point - I'll make it clear that the code checks only for the <code>display</code> property. Given that the the original question is for <code>show()</code> and <code>hide()</code>, and they set <code>display</code>, my answer is correct. By the way it does work with IE7, here's a test snippet - <a href="http://jsfiddle.net/MWZss/" target="_blank">jsfiddle.net/MWZss</a> ;
                    – <a href="/users/25449/tsvetomir-tsonev" title="81,234 reputation" target="_blank">Tsvetomir Tsonev</a>
                <a href="#comment5177770_178450" target="_blank">Jan 14 '11 at 16:54</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-10893573">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                38
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
                I actually found that the reverse logic words better: !$('selector').is(':hidden'); for some reason.  Worth a try.
                    – <a href="/users/69993/kzqai" title="13,564 reputation" target="_blank">Kzqai</a>
                <a href="#comment10893573_178450" target="_blank">Jan 5 '12 at 15:36</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-14631942">
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
                Here's a simple benchmark testing is() against regexp:<a href="http://jsperf.com/jquery-is-vs-regexp-for-css-visibility" target="_blank">jsperf.com/jquery-is-vs-regexp-for-css-visibility</a>. Conclusion: if you're out for performance, use regexp over is() (since is() looks for all hidden nodes first before looking at the actual element).
                    – <a href="/users/219324/max-leske" title="3,967 reputation" target="_blank">Max Leske</a>
                <a href="#comment14631942_178450" target="_blank">Jun 22 '12 at 14:12</a>
                        
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-178450">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>18</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-47946881">
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
<p>You can do this:</p>

<pre><code>isHidden = function(element){
    return (element.style.display === "none");
};</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 22 '17 at 20:12
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
	    

        <div id="comments-link-47946881">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-14515952">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        82
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div><div>
<div>
<pre><code>$('#clickme').click(function() {
  $('#book').toggle('slow', function() {
    // Animation complete.
    alert($('#book').is(":visible")); //&lt;--- TRUE if Visible False if Hidden
  });
});</code></pre>
<pre><code>&lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.1/jquery.min.js"&gt;&lt;/script&gt;
&lt;div id="clickme"&gt;
  Click here
&lt;/div&gt;
&lt;img id="book" src="http://www.chromefusion.com/wp-content/uploads/2012/06/chrome-logo.jpg" alt="" /&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
<p><strong>Source:</strong> </p>

<p><a href="http://bloggerplugnplay.blogspot.in/2013/01/how-to-see-if-element-is-hidden-or.html" target="_blank">Blogger Plug n Play - jQuery Tools and Widgets: How to See if Element is hidden or Visible Using jQuery</a></p>

<p><strong>jsFiddle:</strong> </p>

<p><a href="http://jsfiddle.net/ipsjolly/k4WWj/" target="_blank">JSFiddle - ipsjolly - k4WWj</a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-14515952">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>2</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-47605158">
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
<p>You can use below code for check div is visible or not.</p>

<pre><code>if($('#postcode_div').is(':visible')) {
      //put your code if div is visible.
    } else {
     //put your code if div is not visible.
}</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-47605158">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-46422283">
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
<p>You can use a css class when it visible or hidden by toggling the class.</p>

<pre><code>.show{ display :block; }</code></pre>

<p>Set your jQuery <code>toggleClass()</code> or <code>addClass()</code> or <code>removeClass();</code>.</p>

<p>As an example,</p>

<p><code>jQuery('#myID').toggleClass('show')</code></p>

<p>The above code will add <code>show</code> css class when the element don't have <code>show</code> and will remove when it has <code>show</code> class.</p>

<p>And when you are checking if it visible or not, You can follow this jQuery code,</p>

<p><code>jQuery('#myID').hasClass('show');</code> </p>

<p>Above code will return a boolean (true) when <code>#myID</code> element has our class (<code>show</code>) and false when it don't have the (<code>show</code>) class.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Sep 26 '17 at 9:11
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
	    

        <div id="comments-link-46422283">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-43817534">
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
<p>Just simply check if that element is <strong>visible</strong> and it will return a boolean, jQuery hide the elements by adding display none to the element, so if you want to use pure JavaScript, you can still do that, for example:</p>

<pre><code>if (document.getElementById("element").style.display === 'block') { 
  // your element is visible, do whatever you'd like
}</code></pre>

<p>Also, you can use jQuery as seems the rest of your code using that and you have smaller block of code, something like below in jQuery, do the same track for you:</p>

<pre><code>if ($(element).is(":visible")) { 
    // your element is visible, do whatever you'd like
};</code></pre>

<p>Also using css method in jQuery can result the same thing:</p>

<pre><code>if ($(element).css('display')==='block') {
    // your element is visible, do whatever you'd like
}</code></pre>

<p>Also in case of checking for visibility and display, you can do the below:</p>

<pre><code>if ($(this).css("display")==="block"||$(this).css("visibility")==="visible") {
   // your element is visible, do whatever you'd like
}</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-43817534">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-45574894">
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
<p>Simply check for the <code>display</code> attribute (or <code>visibility</code> depending on what kind of invisibility you prefer). Example :</p>

<pre><code>if ($('#invisible').css('display') == 'none') {
    // This means the HTML element with ID 'invisible' has its 'display' attribute set to 'none'
}</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Aug 8 '17 at 17:47
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
	    

        <div id="comments-link-45574894">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-10305968">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        157
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>How <strong><a href="http://web-profile.net/jquery/dev/jquery-element-visible-hidden/" target="_blank">element visibility and jQuery works</a></strong>;</p>

<p>An element could be hidden with <code>display:none</code>, <code>visibility:hidden</code> or <code>opacity:0</code>. The difference between those methods:</p>

<ul>
<li><code>display:none</code> hides the element, and it does not take up any space;</li>
<li><code>visibility:hidden</code> hides the element, but it still takes up space in the layout;</li>
<li><p><code>opacity:0</code> hides the element as "visibility:hidden", and it still takes up space in the layout; the only difference is that opacity lets one to make an element partly transparent;   </p>

<pre><code>if ($('.target').is(':hidden')) {
  $('.target').show();
} else {
  $('.target').hide();
}
if ($('.target').is(':visible')) {
  $('.target').hide();
} else {
  $('.target').show();
}

if ($('.target-visibility').css('visibility') == 'hidden') {
  $('.target-visibility').css({
    visibility: "visible",
    display: ""
  });
} else {
  $('.target-visibility').css({
    visibility: "hidden",
    display: ""
  });
}

if ($('.target-visibility').css('opacity') == "0") {
  $('.target-visibility').css({
    opacity: "1",
    display: ""
  });
} else {
  $('.target-visibility').css({
    opacity: "0",
    display: ""
  });
}</code></pre>

<p><strong>Useful jQuery toggle methods:</strong>  </p>

<pre><code>$('.click').click(function() {
  $('.target').toggle();
});

$('.click').click(function() {
  $('.target').slideToggle();
});

$('.click').click(function() {
  $('.target').fadeToggle();
});</code></pre></li>
</ul>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-10305968">
		        <table>
                    <tbody>



    <tr id="comment-14812892">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                19
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
                Another difference between <code>visibility:hidden</code> and <code>opacity:0</code> is that the element will still respond to events (like clicks) with <code>opacity:0</code>. I learned that trick making a custom button for file uploads.
                    – <a href="/users/1382949/urraka" title="877 reputation" target="_blank">urraka</a>
                <a href="#comment14812892_10305968" target="_blank">Jun 29 '12 at 18:15</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-10305968">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>1</b> more comment</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-32068044">
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
<pre><code>if($('#id_element').is(":visible")){
   alert('shown');
}else{
   alert('hidden');
}</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-32068044">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-25236348">
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
<p>Simply check visibility by checking for a boolean value, like:</p>

<pre><code>if (this.hidden === false) {
    // Your code
}</code></pre>

<p>I used this code for each function. Otherwise you can use <code>is(':visible')</code> for checking the visibility of an element.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-25236348">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-19628550">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        51
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Example: </p>

<div>
<div>
<pre><code>$(document).ready(function() {
  if ($("#checkme:hidden").length) {
    console.log('Hidden');
  }
});</code></pre>
<pre><code>&lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.1/jquery.min.js"&gt;&lt;/script&gt;
&lt;div id="checkme" class="product" style="display:none"&gt;
  &lt;span class="itemlist"&gt;&lt;!-- Shows Results for Fish --&gt;&lt;/span&gt; Category:Fish
  &lt;br&gt;Product: Salmon Atlantic
  &lt;br&gt;Specie: Salmo salar
  &lt;br&gt;Form: Steaks
&lt;/div&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-19628550">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-44996514">
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
<p>Very simple:</p>

<pre><code>if($('#div').is(":visible")) {
    // visible
} else {
    // hide
}</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-44996514">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-5423934">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        422
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>None of these answers address what I understand to be the question, which is what I was searching for, <em>"How do I handle items that have <code>visibility: hidden</code>?"</em>. Neither <code>:visible</code> nor <code>:hidden</code> will handle this, as they are both looking for display per the documentation.  As far as I could determine, there is no selector to handle CSS visibility.  Here is how I resolved it (standard jQuery selectors, there may be a more condensed syntax):</p>

<pre><code>$(".item").each(function() {
    if ($(this).css("visibility") == "hidden") {
        // handle non visible state
    } else {
        // handle visible state
    }
});</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-5423934">
		        <table>
                    <tbody>



    <tr id="comment-23688295">
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
                This answer is good to handle <code>visibility</code> literally, but the question was <code>How you would test if an element has been hidden or shown using jQuery?</code>. Using jQuery means: the <code>display</code> property.
                    – <a href="/users/1313143/mariods" title="7,012 reputation" target="_blank">MarioDS</a>
                <a href="#comment23688295_5423934" target="_blank">May 11 '13 at 22:37</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-28753708">
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
                Elements with <code>visibility: hidden</code> or <code>opacity: 0</code> are considered to be visible, since they still consume space in the layout. See <a href="http://stackoverflow.com/a/8266879/109392" target="_blank">answer by <b>Pedro Rainho</b></a> and <a href="http://api.jquery.com/visible-selector" target="_blank">jQuery documentation</a> on the <code>:visible</code> selector.
                    – <a href="/users/109392/awe" title="16,692 reputation" target="_blank">awe</a>
                <a href="#comment28753708_5423934" target="_blank">Oct 16 '13 at 9:12</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-35537322">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                8
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
                you need to traverse up the DOM to check the node's parents, or else ,this is useless.
                    – <a href="/users/104380/vsync" title="36,340 reputation" target="_blank">vsync</a>
                <a href="#comment35537322_5423934" target="_blank">Apr 22 '14 at 19:20</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-51616275">
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
                this won't work if you hide element with .hide().
                    – <a href="/users/3197818/user3197818" title="155 reputation" target="_blank">user3197818</a>
                <a href="#comment51616275_5423934" target="_blank">Aug 6 '15 at 5:51</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-5423934">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-40991133">
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
<p>I just want to clarify that, in jQuery,</p>

<blockquote>
  <p>Elements can be considered hidden for several reasons:</p>
  
  <ul>
  <li>They have a CSS display value of none.</li>
  <li>They are form elements with type="hidden".</li>
  <li>Their width and height are explicitly set to 0.</li>
  <li>An ancestor element is hidden, so the element is not shown on the page.</li>
  </ul>
  
  <p>Elements with visibility: hidden or opacity: 0 are considered to be visible, since they still consume space in the layout. During animations that hide an element, the element is considered to be visible until the end of the animation.</p>
  
  <p>Source: <a href="https://api.jquery.com/hidden-selector/" target="_blank">:hidden Selector | jQuery API Documentation</a></p>
</blockquote>

<pre><code>if($('.element').is(':hidden')) {
  // Do something
}</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-40991133">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-8266879">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        173
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>The <code>:visible</code> selector according to <a href="https://api.jquery.com/hidden-selector/" target="_blank">the jQuery documentation</a>:</p>

<blockquote>
  <ul>
  <li>They have a CSS <code>display</code> value of <code>none</code>.</li>
  <li>They are form elements with <code>type="hidden"</code>.</li>
  <li>Their width and height are explicitly set to 0.</li>
  <li>An ancestor element is hidden, so the element is not shown on the page.</li>
  </ul>
  
  <p>Elements with <code>visibility: hidden</code> or <code>opacity: 0</code> are considered to be visible, since they still consume space in the layout.</p>
</blockquote>

<p>This is useful in some cases and useless in others, because if you want to check if the element is visible (<code>display != none</code>), ignoring the parents visibility, you will find that doing <code>.css("display") == 'none'</code> is not only faster, but will also return the visibility check correctly.</p>

<p>If you want to check visibility instead of display, you should use: <code>.css("visibility") == "hidden"</code>.</p>

<p>Also take into consideration <a href="https://api.jquery.com/visible-selector/" target="_blank">the additional jQuery notes</a>:</p>

<blockquote>
  <p>Because <code>:visible</code> is a jQuery extension and not part of the CSS specification, queries using <code>:visible</code> cannot take advantage of the performance boost provided by the native DOM <code>querySelectorAll()</code> method. To achieve the best performance when using <code>:visible</code> to select elements, first select the elements using a pure CSS selector, then use <code>.filter(":visible")</code>.</p>
</blockquote>

<p>Also, if you are concerned about performance, you should check <em><a href="http://www.learningjquery.com/2010/05/now-you-see-me-showhide-performance" target="_blank">Now you see me… show/hide performance</a></em> (2010-05-04). And use other methods to show and hide elements.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-8266879">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-43694490">
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
<pre><code>$('someElement').on('click', function(){ $('elementToToggle').is(':visible')</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
    <td>
    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 29 '17 at 10:25
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
	    

        <div id="comments-link-43694490">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-42896214">
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
<p>There are too many methods to check for hidden elements. This is the best choice (I just recommended you):</p>

<blockquote>
  <p>Using jQuery, make an element, "display:none", in CSS for hidden.</p>
</blockquote>

<p>The point is:</p>

<pre><code>$('element:visible')</code></pre>

<p>And an example for use:</p>

<pre><code>$('element:visible').show();</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-42896214">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-41117640">
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
<p>There are quite a few ways to check if an element is visible or hidden in jQuery.</p>

<p><em>Demo HTML for example reference</em></p>

<pre><code>&lt;div id="content"&gt;Content&lt;/div&gt;
&lt;div id="content2" style="display:none"&gt;Content2&lt;/div&gt;</code></pre>

<p><strong>Use Visibility Filter Selector <code>$('element:hidden')</code> or <code>$('element:visible')</code></strong></p>

<ul>
<li><p><code>$('element:hidden')</code>: Selects all elements that are hidden.</p>

<pre><code>Example:
   $('#content2:hidden').show();</code></pre></li>
<li><p><code>$('element:visible')</code>: Selects all elements that are visible.</p>

<pre><code>Example:
   $('#content:visible').css('color', '#EEE');</code></pre></li>
</ul>

<blockquote>
  <p>Read more at <a href="http://api.jquery.com/category/selectors/visibility-filter-selectors/" target="_blank">http://api.jquery.com/category/selectors/visibility-filter-selectors/</a></p>
</blockquote>

<p><strong>Use <code>is()</code> Filtering</strong></p>

<pre><code>    Example:
       $('#content').is(":visible").css('color', '#EEE');

    Or checking condition
    if ($('#content').is(":visible")) {
         // Perform action
    }</code></pre>

<blockquote>
  <p>Read more at <a href="http://api.jquery.com/is/" target="_blank">http://api.jquery.com/is/</a></p>
</blockquote>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-41117640">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-36397659">
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
<p>You can just add a class when it is visible. Add a class, <code>show</code>. Then check for it have a class:</p>

<pre><code>$('#elementId').hasClass('show');</code></pre>

<p>It returns true if you have the <code>show</code> class.</p>

<p>Add CSS like this:</p>

<pre><code>.show{ display: block; }</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-36397659">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-36982533">
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
<p>You can use this:</p>

<pre><code>$(element).is(':visible');</code></pre>

<h2>Example code</h2>

<div>
<div>
<pre><code>$(document).ready(function()
{
    $("#toggle").click(function()
    {
        $("#content").toggle();
    });

    $("#visiblity").click(function()
    {
       if( $('#content').is(':visible') )
       {
          alert("visible"); // Put your code for visibility
       }
       else
       {
          alert("hidden");
       }
    });
});</code></pre>
<pre><code>&lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.2/jquery.min.js"&gt;&lt;/script&gt;

&lt;p id="content"&gt;This is a Content&lt;/p&gt;

&lt;button id="toggle"&gt;Toggle Content Visibility&lt;/button&gt;
&lt;button id="visibility"&gt;Check Visibility&lt;/button&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-36982533">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-43014382">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>To be fair the question pre-dates this answer. I add it not to criticise the OP but to help anyone still asking this question.</p>

<p>The correct way to determine whether something is visible is to consult your view-model. If you don't know what that means then you are about to embark on a journey of discovery that will make your work a great deal less difficult.</p>

<p>Here's an overview of the <a href="https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93viewmodel" target="_blank">model-view-viewmodel</a> architecture (MVVM).</p>

<p><a href="http://knockoutjs.com" target="_blank">KnockoutJS</a> is a binding library that will let you try this stuff out without learning an entire framework.</p>

<p>And here's some JS and a DIV that may or may not be visible.</p>

<pre><code>&lt;html&gt;&lt;body&gt;
&lt;script src="https://cdnjs.cloudflare.com/ajax/libs/knockout/3.4.1/knockout-min.js"&gt;&lt;/script&gt;
&lt;script&gt;
var vm = {
  IsDivVisible: ko.observable(true);
}
vm.toggle = function(data, event) {
  //get current visibility state for the div
  var x = IsDivVisible();
  //set it to the opposite
  IsDivVisible(!x);
}
ko.applyBinding(vm);
&lt;/script&gt;
&lt;div data-bind="visible: IsDivVisible"&gt;Peekaboo!&lt;/div&gt;
&lt;button data-bind="click: toggle"&gt;Toggle the div's visibility&lt;/button&gt;
&lt;/body&gt;&lt;/html&gt;</code></pre>

<p>Notice that the toggle function does not consult the DOM to determine the visibility of the div, it consults the view-model.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Mar 25 '17 at 8:49
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
	    

        <div id="comments-link-43014382">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-37561155">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        17
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I searched for this, and none of the answers are correct for my case, so I've created a function that will return false if one's eyes can't see the element</p>

<pre><code>jQuery.fn.extend({
  isvisible: function() {
    //
    //  This function call this: $("div").isvisible()
    //  Return true if the element is visible
    //  Return false if the element is not visible for our eyes
    //
    if ( $(this).css('display') == 'none' ){
        console.log("this = " + "display:none");
        return false;
    }
    else if( $(this).css('visibility') == 'hidden' ){
        console.log("this = " + "visibility:hidden");   
        return false;
    }
    else if( $(this).css('opacity') == '0' ){
        console.log("this = " + "opacity:0");
        return false;
    }   
    else{
        console.log("this = " + "Is Visible");
        return true;
    }
  }  
});</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-37561155">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>1</b> more comment</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-40904208">
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
<p>You can use the </p>

<pre><code>$( "div:visible" ).click(function() {
  $( this ).css( "background", "yellow" );
});
$( "button" ).click(function() {
  $( "div:hidden" ).show( "fast" );
});</code></pre>

<p>API Documentation: <a href="https://api.jquery.com/visible-selector/" target="_blank">https://api.jquery.com/visible-selector/</a></p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 1 '16 at 6:46
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
	    

        <div id="comments-link-40904208">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-40438235">
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
<p>As <code>hide()</code>, <code>show()</code> and <code>toggle()</code> attaches inline css (display:none or display:block) to element.
Similarly, we can easily use ternary operator to check weather element is hidden or visible by checking display css.</p>

<pre><code>var visible = $('#element').css('display') === 'block'? true:false;</code></pre>

<p>This will easily check whether the element is visible or not.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-40438235">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-29890170">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        47
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Example of using the <strong>visible</strong> check for adblocker is activated:</p>

<div>
<div>
<pre><code>$(document).ready(function(){
  if(!$("#ablockercheck").is(":visible"))
    $("#ablockermsg").text("Please disable adblocker.").show();
});</code></pre>
<pre><code>&lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.1/jquery.min.js"&gt;&lt;/script&gt;
&lt;div class="ad-placement" id="ablockercheck"&gt;&lt;/div&gt;
&lt;div id="ablockermsg" style="display: none"&gt;&lt;/div&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
<p>"ablockercheck" is a ID which adblocker blocks. So checking it if it is visible you are able to detect if adblocker is turned On.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-29890170">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-23492646">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        73
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>When testing an element against <code>:hidden</code> selector in jQuery it should be considered that <strong>an absolute positioned element may be recognized as hidden although their child elements are visible</strong>.</p>

<p>This seems somewhat counter-intuitive in the first place – though having a closer look at the jQuery documentation gives the relevant information:</p>

<blockquote>
  <p>Elements can be considered hidden for several reasons: [...] Their width and height are explicitly set to 0. [...]</p>
</blockquote>

<p>So this actually makes sense in regards to the box-model and the computed style for the element. Even if width and height are not set <em>explicitly</em> to 0 they may be set <em>implicitly</em>.</p>

<p>Have a look at the following example:</p>

<div>
<div>
<pre><code>console.log($('.foo').is(':hidden')); // true
console.log($('.bar').is(':hidden')); // false</code></pre>
<pre><code>.foo {
  position: absolute;
  left: 10px;
  top: 10px;
  background: #ff0000;
}

.bar {
  position: absolute;
  left: 10px;
  top: 10px;
  width: 20px;
  height: 20px;
  background: #0000ff;
}</code></pre>
<pre><code>&lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.1/jquery.min.js"&gt;&lt;/script&gt;
&lt;div class="foo"&gt;
  &lt;div class="bar"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>

<hr />

<p><strong>UPDATE FOR JQUERY 3.x:</strong></p>

<p>With jQuery 3 the described behavior will change! Elements will be considered visible if they have any layout boxes, including those of zero width and/or height.</p>

<p>JSFiddle with jQuery 3.0.0-alpha1:</p>

<p><a href="http://jsfiddle.net/pM2q3/7/" target="_blank">http://jsfiddle.net/pM2q3/7/</a></p>

<p>The same JS will then have this output:</p>

<pre><code>console.log($('.foo').is(':hidden')); // false
console.log($('.bar').is(':hidden')); // false</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-23492646">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-29491573">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        31
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Maybe you can do something like this</p>

<div>
<div>
<pre><code>$(document).ready(function() {
   var visible = $('#tElement').is(':visible');

   if(visible) {
      alert("visible");
                    // Code
   }
   else
   {
      alert("hidden");
   }
});</code></pre>
<pre><code>&lt;script src="https://code.jquery.com/jquery-1.10.2.js"&gt;&lt;/script&gt;

&lt;input type="text" id="tElement" style="display:block;"&gt;Firstname&lt;/input&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-29491573">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-36561933">
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
<p>This is how <a href="https://github.com/jquery/jquery/blob/055cb7534e2dcf7ee8ad145be83cb2d74b5331c7/src/css/hiddenVisibleSelectors.js" target="_blank">jQuery</a> internally solves this problem:</p>

<pre><code>jQuery.expr.pseudos.visible = function( elem ) {
    return !!( elem.offsetWidth || elem.offsetHeight || elem.getClientRects().length );
};</code></pre>

<p>If you don't use jQuery, you can just leverage this code and turn it into your own function:</p>

<pre><code>function isVisible(elem) {
    return !!( elem.offsetWidth || elem.offsetHeight || elem.getClientRects().length );
};</code></pre>

<p>Which <code>isVisible</code> will return <code>true</code> as long as the element is visible.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 12 '16 at 1:11
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
	    

        <div id="comments-link-36561933">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-36179368">
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
<pre><code>if($("h1").is(":hidden")){
    // your code..
}</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-36179368">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-4685330">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        301
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>From <em><a href="http://learn.jquery.com/using-jquery-core/faq/how-do-i-determine-the-state-of-a-toggled-element/" target="_blank">How do I determine the state of a toggled element?</a></em></p>

<hr />

<p>You can determine whether an element is collapsed or not by using the <code>:visible</code> and <code>:hidden</code> selectors.</p>

<pre><code>var isVisible = $('#myDiv').is(':visible');
var isHidden = $('#myDiv').is(':hidden');</code></pre>

<p>If you're simply acting on an element based on its visibility, you can just include <code>:visible</code> or <code>:hidden</code> in the selector expression. For example:</p>

<pre><code> $('#myDiv:visible').animate({left: '+=200px'}, 'slow');</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-4685330">
		        <table>
                    <tbody>



    <tr id="comment-74724294">
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
                wondering why no answer mentions the case when element is moved away from the visible window, like <code>top:-1000px</code>... Guess it's an edge-case
                    – <a href="/users/714733/jazzcat" title="2,628 reputation" target="_blank">jazzcat</a>
                <a href="#comment74724294_4685330" target="_blank">May 8 '17 at 9:34</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-4685330">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            


            
    






                            

                                                            
                        
                            
                            



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/jquery" title="show questions tagged 'jquery'" target="_blank">jquery</a> <a href="/questions/tagged/dom" title="show questions tagged 'dom'" target="_blank">dom</a> <a href="/questions/tagged/visibility" title="show questions tagged 'visibility'" target="_blank">visibility</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
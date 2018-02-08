<a href="https://perishablepress.com/lessons-learned-concerning-the-clearfix-css-hack/">https://perishablepress.com/lessons-learned-concerning-the-clearfix-css-hack/</a><div id="articleHeader"><h1>				<a href="https://perishablepress.com/lessons-learned-concerning-the-clearfix-css-hack/" title="Posted: February 5th, 2008 | 20 Comments" target="_blank">Lessons Learned Concerning the Clearfix CSS Hack</a>							</h1></div>

		
			<p>I use the <acronym>CSS</acronym> <a href="http://www.positioniseverything.net/easyclearing.html" title="How To Clear Floats Without Structural Markup" target="_blank">clearfix hack</a> on nearly all of my sites. The clearfix hack — also known as the “<a href="http://www.456bereastreet.com/archive/200603/new_clearing_method_needed_for_ie7/" title="New clearing method needed for IE7?" target="_blank">Easy Clearing Hack</a>” — is used to clear floated divisions (<code>div</code>s) without using structural markup. It is very effective in resolving layout issues and browser inconsistencies without the need to mix structure with presentation. Over the course of the past few years, I have taken note of several useful bits of information regarding the Easy Clear Method. In this article, I summarize these lessons learned and present a (slightly) enhanced version of the clearfix hack..</p>
<h3>Use a space instead of a dot to prevent breaking layouts</h3>
<p>Here is the defacto implementation of the clearfix hack, as presented in one of the <a href="http://www.positioniseverything.net/easyclearing.html" title="How To Clear Floats Without Structural Markup" target="_blank">original articles</a> covering the method:</p>
<pre><code>.clearfix:after {
     content: "."; 
     display: block; 
     height: 0; 
     clear: both; 
     visibility: hidden;
}

.clearfix {display: inline-block;}

/* Hides from IE-mac \*/
* html .clearfix {height: 1%;}
.clearfix {display: block;}
/* End hide from IE-mac */</code></pre>
<p>Notice the line containing the <code>content: ".";</code> property. I have found that the period (or dot) specified in quotes has a nasty tendency to break certain layouts. By adding a literal dot <em>after</em> the <code>.clearfix</code> division (i.e., via the <code>.clearfix:after</code> selector), the clearfix hack creates a stumbling block for certain browsers. And not just for Internet Explorer — depending on the layout, even Firefox will choke a layout upon tripping on an <code>:after</code>-based pseudo-dot. The solution to this subtle design chaos? Replace the literal dot with a single blank space: <code>"content: " ";</code> — this trick has proven successful so consistently that I now use it as the default property in every clearfix hack that I use.</p>
<pre><code>/* drop the dot, replace with space */
.clearfix:after {
     content: " "; 
     display: block; 
     height: 0; 
     clear: both; 
     visibility: hidden;
     }
     .
     .
     .</code></pre>
<h3>Add a zero font-size property to make it all smooth</h3>
<p>Another bizarre inconsistency involved with clearfixed (probably not a real verb) layouts seems to disappear when the <code>	font-size</code> property is included in the hack and subsequently set to zero:</p>
<pre><code>/* zero font-size added to prevent potential layout issues */
.clearfix:after {
     content: " "; 
     display: block; 
     height: 0; 
     clear: both; 
     visibility: hidden;
     font-size: 0;
     }
     .
     .
     .</code></pre>
<p>This may be overkill when using a blank space instead of an actual dot (as described above), but I honestly don’t care. I’m like some sort of <acronym>CSS</acronym> animal — using every available weapon to fight hellish layout battles. Looking back, I think I may have implemented this solution <em>before</em> discovering the empty-space fix. Yet some browsers may process white space as text, so it may prove beneficial nonetheless. Maybe, maybe not — I’m going to throw it out there for all of you <acronym>CSS</acronym> gurus to trip on.</p>
<h3>Beware of misinformation regarding this method</h3>
<p>No, I am not trying to warn you against the tips offered in this article — you will find they are quite harmless. Instead, I am referring to erroneous information found elsewhere on the Internet and even in printed form. Here is a presentation of the clearfix hack as presented in Joseph W. Lowery’s otherwise excellent book, <em>CSS Hack & Filters</em>:</p>
<pre><code>.clearItem:after {
     content: ".";
     clear: both;
     height: 0;
     visibility: hidden;
     display: block;
}

.clearItem { display: inline; }

/* Start Commented Backslash Hack \*/
* html .clearItem, * html .clearItem * {height: 1%;}
.clearItem { display: block; }
/* Close Commented Backslash Hack */</code></pre>
<p>Yikes! Do you see the problem? Actually, there are two potential issues in Mr. Lowery’s “.clearItem” hack. The first one is the deprecated use of the <code>inline</code> value for the <code>display</code> property in the middle <code>.clearItem</code> declaration:</p>
<p><code>.clearItem { display: inline; }</code></p>
<p>..as discussed in the original article, the property value here should be <code>inline-block</code> to fix floats on <acronym>IE/Mac</acronym>:</p>
<p><code>.clearItem { display: inline-block; }</code></p>
<p>The second flaw in Mr. Lowery’s “.clearItem” hack involves the <code>* html .clearItem *</code> selector in the following line:</p>
<p><code>* html .clearItem, * html .clearItem * {height: 1%;}</code></p>
<p>The first selector in this line is all that is required to achieve a successful hack. The <em>second</em> selector, however, effectively sets the height to <code>1%</code> for all Internet Explorer browsers. This sucks, and I found out the hard way: after a month or so of using this version of the hack, I discovered that around half of my visitors (i.e., those using <acronym>IE</acronym>) were unable to leave comments because all of the form fields were only 1 pixel tall! Fortunately, it did not take <em>too</em> long to hammer down the culprit: the nefarious <acronym>CSS</acronym> wildcard selector ( <code>*</code> ) as seen in the erroneous code above. After deleting that second selector, everything clicked. </p>
<p>So what’s the moral of the story here? Simple. <em>Always double-check your code and think critically before blindly copying & pasting your way to victory.</em> Even professional writers and programmers make mistakes, so be sure to <strong>pay attention and make no assumptions</strong>.</p>
<h3>All together now..</h3>
<p>Putting everything together and combining these lessons learned with the original (correct) version of the Easy Clear Method, we fashion the following, fully functional, flaw-fixing clearfix formula:</p>
<pre><code>/* slightly enhanced, universal clearfix hack */
.clearfix:after {
     visibility: hidden;
     display: block;
     font-size: 0;
     content: " ";
     clear: both;
     height: 0;
     }
.clearfix { display: inline-block; }
/* start commented backslash hack \*/
* html .clearfix { height: 1%; }
.clearfix { display: block; }
/* close commented backslash hack */</code></pre>
<p>..and that’s a wrap! I sure hope you had as much fun as I did while writing this article.. if not, hopefully this round of “lessons learned” presented you with some useful information regarding the omnipresent, ever-useful clearfix hack. And finally, as this post focuses on <acronym>CSS</acronym>, I expect nothing less than the <em>severest</em> of criticism <sup>1</sup> concerning the ideas presented herein. — Fire away, all you crazy <acronym>CSS</acronym> heads! ;)</p>

<ul>
<li><sup>1</sup> A bit of sarcasm for you ;)</li>
</ul>
<h3>Translated version</h3>


		
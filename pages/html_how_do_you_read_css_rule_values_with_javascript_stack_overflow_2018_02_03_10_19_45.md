<a href="https://stackoverflow.com/questions/324486/how-do-you-read-css-rule-values-with-javascript">https://stackoverflow.com/questions/324486/how-do-you-read-css-rule-values-with-javascript</a><div id="articleHeader"><h1>How do you read CSS rule values with JavaScript?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        90
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>33</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I would like to return a string with all of the contents of a CSS rule, like the format you'd see in an inline style. I'd like to be able to do this without knowing what is contained in a particular rule, so I can't just pull them out by style name (like <code>.style.width</code> etc.) </p>

<p>The CSS:</p>

<pre><code>.test {
    width:80px;
    height:50px;
    background-color:#808080;
}</code></pre>

<p>The code so far:</p>

<pre><code>function getStyle(className) {
    var classes = document.styleSheets[0].rules || document.styleSheets[0].cssRules
    for(var x=0;x&lt;classes.length;x++) {
        if(classes[x].selectorText==className) {
            //this is where I can collect the style information, but how?
        }
    }
}
getStyle('.test')</code></pre>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-324486">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-324533">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        67
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>Adapted from <a href="http://www.javascriptkit.com/domref/cssrule.shtml" target="_blank">here</a>, building on scunliffe's answer:</p>

<pre><code>function getStyle(className) {
    var classes = document.styleSheets[0].rules || document.styleSheets[0].cssRules;
    for (var x = 0; x &lt; classes.length; x++) {
        if (classes[x].selectorText == className) {
            (classes[x].cssText) ? alert(classes[x].cssText) : alert(classes[x].style.cssText);
        }
    }
}
getStyle('.test');</code></pre>
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
        answered Nov 27 '08 at 19:36
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
	    <div id="comments-324533">
                <ul>



    <li id="comment-9096539">
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
                Note that className must exactly match the selector used in CSS file. For example getStyle(".article a") won't find anything if a style has been described like this ".article a, article a:hover { color: #ccc; }".
                    – <a href="/users/200325/vilius-paulauskas" title="1,687 reputation" target="_blank">Vilius Paulauskas</a>
                <a href="#comment9096539_324533" target="_blank">Sep 22 '11 at 7:49</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-9743434">
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
                This does not work in chrome, but it works in firefox, what could be the problem??
                    – <a href="/users/750965/johnydep" title="1,985 reputation" target="_blank">Johnydep</a>
                <a href="#comment9743434_324533" target="_blank">Nov 1 '11 at 15:31</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-18697121">
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
                if there are multiple stylesheets, then you will also need to loop through those as well.for(var i=0;i&lt;document.styleSheets.length;i++) {             var s = document.styleSheets[i];}
                    – <a href="/users/209609/surya" title="665 reputation" target="_blank">surya</a>
                <a href="#comment18697121_324533" target="_blank">Nov 29 '12 at 17:39</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-43483403">
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
                @surya See my answer for a adapted full working solution
                    – <a href="/users/3894981/dude" title="2,201 reputation" target="_blank">dude</a>
                <a href="#comment43483403_324533" target="_blank">Dec 17 '14 at 14:09</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-46135325">
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
                @Johnydep <code>var classes</code> should be <code>document.styleSheets[0].rules[0].cssRules</code> in Chrome. This could be (creatively) added to the shim in the answer.
                    – <a href="/users/667253/henrik-christensen" title="194 reputation" target="_blank">Henrik Christensen</a>
                <a href="#comment46135325_324533" target="_blank">Mar 9 '15 at 10:58</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-324533">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-324527">
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
<p>//works in IE, not sure about other browsers...</p>

<pre><code>alert(classes[x].style.cssText);</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Nov 27 '08 at 19:32
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
	    

        <div id="comments-link-324527">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-350573">
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
<p>Some browser differences to be aware of:</p>

<p>Given the CSS:</p>

<pre><code>div#a { ... }
div#b, div#c { ... }</code></pre>

<p>and given InsDel's example, classes will have <strong>2 classes in FF and 3 classes in IE7</strong>.</p>

<p>My example illustrates this:</p>

<pre><code>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
   "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;
&lt;html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en"&gt;
&lt;head&gt;
    &lt;style&gt;
    div#a { }
    div#b, div#c { }
    &lt;/style&gt;
    &lt;script&gt;
    function PrintRules() {
    var rules = document.styleSheets[0].rules || document.styleSheets[0].cssRules
        for(var x=0;x&lt;rules.length;x++) {
            document.getElementById("rules").innerHTML += rules[x].selectorText + "&lt;br /&gt;";
        }
    }
    &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;input onclick="PrintRules()" type="button" value="Print Rules" /&gt;&lt;br /&gt;
    RULES:
    &lt;div id="rules"&gt;&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
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
        answered Dec 8 '08 at 19:31
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
	    

        <div id="comments-link-350573">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-3345851">
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
<p>I made a similar helper  function 
which shows the unneeded styles for this page. appends a <code>&lt;div&gt;</code> to the body listing all styles that where not used.</p>

<p>(to be used with the firebug console)</p>

<pre><code>(function getStyles(){var CSSrules,allRules,CSSSheets, unNeeded, currentRule;
CSSSheets=document.styleSheets;

for(j=0;j&lt;CSSSheets.length;j++){
for(i=0;i&lt;CSSSheets[j].cssRules.length;i++){
    currentRule = CSSSheets[j].cssRules[i].selectorText;

    if(!document.querySelectorAll(currentRule).length){ 
       unNeeded+=CSSSheets[j].cssRules[i].cssText+"&lt;br&gt;"; 
  }       
 }
}

docBody=document.getElementsByTagName("body")[0];
allRulesContainer=document.createElement("div");
docBody.appendChild(allRulesContainer);
allRulesContainer.innerHTML=unNeeded+isHover;
return false
})()</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jul 27 '10 at 16:40
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
	    

        <div id="comments-link-3345851">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-5960538">
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
<pre><code>function getStyle(className) {
    document.styleSheets.item("menu").cssRules.item(className).cssText;
}
getStyle('.test')</code></pre>

<p>Note : "menu" is an element ID which you have applied CSS.
"className" a css class name which we need to get its text.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-5960538">
                <ul>



    <li id="comment-22442444">
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
                Are you sure this is working? (AFAIK the <code>item</code> method takes an integer index, not a className).
                    – <a href="/users/698168/julien-kronegg" title="2,460 reputation" target="_blank">Julien Kronegg</a>
                <a href="#comment22442444_5960538" target="_blank">Apr 3 '13 at 10:57</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-5960538">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-15823002">
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
<p>This version will go through all of the stylesheets on a page. For my needs, the styles were usually in the 2nd to last of the 20+ stylesheets, so I check them backwards.</p>

<pre><code>    var getStyle = function(className){
        var x, sheets,classes;
        for( sheets=document.styleSheets.length-1; sheets&gt;=0; sheets-- ){
            classes = document.styleSheets[sheets].rules || document.styleSheets[sheets].cssRules;
            for(x=0;x&lt;classes.length;x++) {
                if(classes[x].selectorText===className) {
                    return  (classes[x].cssText ? classes[x].cssText : classes[x].style.cssText);
                }
            }
        }
        return false;
    };</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 4 '13 at 22:43
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
	    

        <div id="comments-link-15823002">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-18987296">
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
<p>I added return of object where attributes are parsed out style/values:</p>

<pre><code>var getClassStyle = function(className){
    var x, sheets,classes;
    for( sheets=document.styleSheets.length-1; sheets&gt;=0; sheets-- ){
        classes = document.styleSheets[sheets].rules || document.styleSheets[sheets].cssRules;
        for(x=0;x&lt;classes.length;x++) {
            if(classes[x].selectorText===className){
                classStyleTxt = (classes[x].cssText ? classes[x].cssText : classes[x].style.cssText).match(/\{\s*([^{}]+)\s*\}/)[1];
                var classStyles = {};
                var styleSets = classStyleTxt.match(/([^;:]+:\s*[^;:]+\s*)/g);
                for(y=0;y&lt;styleSets.length;y++){
                    var style = styleSets[y].match(/\s*([^:;]+):\s*([^;:]+)/);
                    if(style.length &gt; 2)
                        classStyles[style[1]]=style[2];
                }
                return classStyles;
            }
        }
    }
    return false;
};</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-18987296">
                <ul>



    <li id="comment-44906785">
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
                <code>style.cssText.match(...).1</code> is null or not an object
                    – <a href="/users/3894981/dude" title="2,201 reputation" target="_blank">dude</a>
                <a href="#comment44906785_18987296" target="_blank">Feb 2 '15 at 10:56</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-77851378">
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
                <code>Uncaught ReferenceError: classStyleTxt is not defined</code>
                    – <a href="/users/332578/jacksonkr" title="16,336 reputation" target="_blank">Jacksonkr</a>
                <a href="#comment77851378_18987296" target="_blank">Aug 1 '17 at 18:31</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-18987296">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-27527462">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        16
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Since the accepted answer from "nsdel" is only avilable with one stylesheet in a document this is the adapted full working solution:</p>

<pre><code>    /**
     * Gets styles by a classname
     * 
     * @notice The className must be 1:1 the same as in the CSS
     * @param string className_
     */
    function getStyle(className_) {

        var styleSheets = window.document.styleSheets;
        var styleSheetsLength = styleSheets.length;
        for(var i = 0; i &lt; styleSheetsLength; i++){
            var classes = styleSheets[i].rules || styleSheets[i].cssRules;
            if (!classes)
                continue;
            var classesLength = classes.length;
            for (var x = 0; x &lt; classesLength; x++) {
                if (classes[x].selectorText == className_) {
                    var ret;
                    if(classes[x].cssText){
                        ret = classes[x].cssText;
                    } else {
                        ret = classes[x].style.cssText;
                    }
                    if(ret.indexOf(classes[x].selectorText) == -1){
                        ret = classes[x].selectorText + "{" + ret + "}";
                    }
                    return ret;
                }
            }
        }

    }</code></pre>

<p>Notice: The selector must be the same as in the CSS.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-27527462">
                <ul>



    <li id="comment-46482633">
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
                <b><code>ReferenceError: global_ is not defined</code></b> !!!!
                    – <a href="/users/2377343/t-todua" title="22,886 reputation" target="_blank">T.Todua</a>
                <a href="#comment46482633_27527462" target="_blank">Mar 18 '15 at 17:11</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-46546540">
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
                <code>global_</code> ist just a alias for the window object. I've edited the code snippet. It should work now
                    – <a href="/users/3894981/dude" title="2,201 reputation" target="_blank">dude</a>
                <a href="#comment46546540_27527462" target="_blank">Mar 20 '15 at 9:52</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-53880284">
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
                your code fails if a stylesheet has no rules or cssRules (which can happen!) add     if (!classes) continue; after     var classes = styleSheets[i].rules || styleSheets[i].cssRules;             var classesLength = classes.length; see my edit
                    – <a href="/users/460084/kofifus" title="2,379 reputation" target="_blank">kofifus</a>
                <a href="#comment53880284_27527462" target="_blank">Oct 9 '15 at 2:44</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-68291578">
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
                works, but should return a object instead of a string
                    – <a href="/users/670229/brauliobo" title="2,072 reputation" target="_blank">brauliobo</a>
                <a href="#comment68291578_27527462" target="_blank">Nov 10 '16 at 10:46</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-77013060">
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
                @kofifus Your approach has been added
                    – <a href="/users/3894981/dude" title="2,201 reputation" target="_blank">dude</a>
                <a href="#comment77013060_27527462" target="_blank">Jul 10 '17 at 18:49</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-27527462">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-29130215">
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
<h1>SOLUTION 1 (CROSS-BROWSER)</h1>

<pre><code>function GetProperty(classOrId,property){ 
    var FirstChar = classOrId.charAt(0);  var Remaining= classOrId.substring(1);
    var elem = (FirstChar =='#') ?  document.getElementById(Remaining) : document.getElementsByClassName(Remaining)[0];
    return window.getComputedStyle(elem,null).getPropertyValue(property);
}

alert(  GetProperty(".my_site_title","position") ) ;</code></pre>

<h1>SOLUTION 2 (CROSS-BROWSER)</h1>

<pre><code>function GetStyle(CLASSname) {
    var styleSheets = document.styleSheets;
    var styleSheetsLength = styleSheets.length;
    for(var i = 0; i &lt; styleSheetsLength; i++){
        if (styleSheets[i].rules ) { var classes = styleSheets[i].rules; }
        else { 
            try {  if(!styleSheets[i].cssRules) {continue;} } 
            //Note that SecurityError exception is specific to Firefox.
            catch(e) { if(e.name == 'SecurityError') { console.log("SecurityError. Cant readd: "+ styleSheets[i].href);  continue; }}
            var classes = styleSheets[i].cssRules ;
        }
        for (var x = 0; x &lt; classes.length; x++) {
            if (classes[x].selectorText == CLASSname) {
                var ret = (classes[x].cssText) ? classes[x].cssText : classes[x].style.cssText ;
                if(ret.indexOf(classes[x].selectorText) == -1){ret = classes[x].selectorText + "{" + ret + "}";}
                return ret;
            }
        }
    }
}

alert(GetStyle('.my_site_title'));</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-29130215">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-30917685">
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
<p>Have adapted julmot's answer in order to get a more complete result. This method will also return styles where the class is part for the selector.</p>

<pre><code>//Get all styles where the provided class is involved
//Input parameters should be css selector such as .myClass or #m
//returned as an array of tuples {selectorText:"", styleDefinition:""}
function getStyleWithCSSSelector(cssSelector) {
    var styleSheets = window.document.styleSheets;
    var styleSheetsLength = styleSheets.length;
    var arStylesWithCSSSelector = [];

    //in order to not find class which has the current name as prefix
    var arValidCharsAfterCssSelector = [" ", ".", ",", "#","&gt;","+",":","["];

    //loop through all the stylessheets in the bor
    for(var i = 0; i &lt; styleSheetsLength; i++){
        var classes = styleSheets[i].rules || styleSheets[i].cssRules;
        var classesLength = classes.length;
        for (var x = 0; x &lt; classesLength; x++) {
            //check for any reference to the class in the selector string
            if(typeof classes[x].selectorText != "undefined"){
                var matchClass = false;

                if(classes[x].selectorText === cssSelector){//exact match
                    matchClass=true;
                }else {//check for it as part of the selector string
                    //TODO: Optimize with regexp
                    for (var j=0;j&lt;arValidCharsAfterCssSelector.length; j++){
                        var cssSelectorWithNextChar = cssSelector+ arValidCharsAfterCssSelector[j];

                        if(classes[x].selectorText.indexOf(cssSelectorWithNextChar)!=-1){
                            matchClass=true;
                            //break out of for-loop
                            break;
                        }
                    }
                }

                if(matchClass === true){
                    //console.log("Found "+ cssSelectorWithNextChar + " in css class definition " + classes[x].selectorText);
                    var styleDefinition;
                    if(classes[x].cssText){
                        styleDefinition = classes[x].cssText;
                    } else {
                        styleDefinition = classes[x].style.cssText;
                    }
                    if(styleDefinition.indexOf(classes[x].selectorText) == -1){
                        styleDefinition = classes[x].selectorText + "{" + styleDefinition + "}";
                    }
                    arStylesWithCSSSelector.push({"selectorText":classes[x].selectorText, "styleDefinition":styleDefinition});
                }
            }
        }
    }
    if(arStylesWithCSSSelector.length==0) {
        return null;
    }else {
        return arStylesWithCSSSelector;    
    }
}</code></pre>

<p>In addition, I've made a function which collects the css style definitions to the sub-tree of a root node your provide (through a jquery selector). </p>

<pre><code>function getAllCSSClassDefinitionsForSubtree(selectorOfRootElement){
    //stack in which elements are pushed and poped from
    var arStackElements = [];
    //dictionary for checking already added css class definitions
    var existingClassDefinitions = {}

    //use jquery for selecting root element
    var rootElement = $(selectorOfRootElement)[0];
    //string with the complete CSS output
    var cssString = "";

    console.log("Fetching all classes used in sub tree of " +selectorOfRootElement);
    arStackElements.push(rootElement);
    var currentElement;

    while(currentElement = arStackElements.pop()){
        currentElement = $(currentElement);
        console.log("Processing element " + currentElement.attr("id"));

        //Look at class attribute of element 
        var classesString = currentElement.attr("class");
        if(typeof classesString != 'undefined'){
            var arClasses = classesString.split(" ");

            //for each class in the current element
            for(var i=0; i&lt; arClasses.length; i++){

                //fetch the CSS Styles for a single class. Need to append the . char to indicate its a class
                var arStylesWithCSSSelector = getStyleWithCSSSelector("."+arClasses[i]);
                console.log("Processing class "+ arClasses[i]);

                if(arStylesWithCSSSelector != null){
                    //console.log("Found "+ arStylesWithCSSSelector.length + " CSS style definitions for class " +arClasses[i]);
                    //append all found styles to the cssString
                    for(var j=0; j&lt; arStylesWithCSSSelector.length; j++){
                        var tupleStyleWithCSSSelector = arStylesWithCSSSelector[j];

                        //check if it has already been added
                        if(typeof existingClassDefinitions[tupleStyleWithCSSSelector.selectorText] === "undefined"){
                            //console.log("Adding " + tupleStyleWithCSSSelector.styleDefinition);
                            cssString+= tupleStyleWithCSSSelector.styleDefinition;
                            existingClassDefinitions[tupleStyleWithCSSSelector.selectorText] = true;
                        }else {
                            //console.log("Already added " + tupleStyleWithCSSSelector.styleDefinition);
                        }
                    }
                }
            }
        }
        //push all child elments to stack
        if(currentElement.children().length&gt;0){
            arStackElements= arStackElements.concat(currentElement.children().toArray());
        }
    }

    console.log("Found " + Object.keys(existingClassDefinitions).length + " CSS class definitions");
    return cssString;
}</code></pre>

<p>Note that if a class is defined several times with the same selector, the above function will only pick up the first. Note that the example uses jQuery (but cab relatively easily be rewritten to not use it)</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-30917685">
                <ul>



    <li id="comment-53832745">
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
                would be great to have a non jquery solution (and a jsfiddle ..)
                    – <a href="/users/460084/kofifus" title="2,379 reputation" target="_blank">kofifus</a>
                <a href="#comment53832745_30917685" target="_blank">Oct 7 '15 at 23:10</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-30917685">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-40298390">
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
<p>I've found none of the suggestions to really work.  Here's a more robust one that normalizes spacing when finding classes. </p>

<pre><code>//Inside closure so that the inner functions don't need regeneration on every call.
const getCssClasses = (function () {
    function normalize(str) {
        if (!str)  return '';
        str = String(str).replace(/\s*([&gt;~+])\s*/g, ' $1 ');  //Normalize symbol spacing.
        return str.replace(/(\s+)/g, ' ').trim();           //Normalize whitespace
    }
    function split(str, on) {               //Split, Trim, and remove empty elements
        return str.split(on).map(x =&gt; x.trim()).filter(x =&gt; x);
    }
    function containsAny(selText, ors) {
        return selText ? ors.some(x =&gt; selText.indexOf(x) &gt;= 0) : false;
    }
    return function (selector) {
        const logicalORs = split(normalize(selector), ',');
        const sheets = Array.from(window.document.styleSheets);
        const ruleArrays = sheets.map((x) =&gt; Array.from(x.rules || x.cssRules || []));
        const allRules = ruleArrays.reduce((all, x) =&gt; all.concat(x), []);
        return allRules.filter((x) =&gt; containsAny(normalize(x.selectorText), logicalORs));
    };
})();</code></pre>

<p>Here's it in action from the Chrome console. </p>

<p><a href="https://i.stack.imgur.com/AElQK.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/AElQK.png" alt="enter image description here" /></div></a></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-40298390">
                <ul>



    <li id="comment-77851460">
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
                This is the mecha of all the answers on this page. I would even go as far as to say this should be on github
                    – <a href="/users/332578/jacksonkr" title="16,336 reputation" target="_blank">Jacksonkr</a>
                <a href="#comment77851460_40298390" target="_blank">Aug 1 '17 at 18:33</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-79851985">
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
                This doesn't work in IE11, because Array.map() with the provided syntax is not supported. I'd suggest changing it to the old function(){ return xxx; } syntax for better compatibility. Otherwise, great answer!
                    – <a href="/users/1548580/demonblack" title="230 reputation" target="_blank">Demonblack</a>
                <a href="#comment79851985_40298390" target="_blank">Sep 27 '17 at 12:44</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-79852980">
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
                I modified this to work with IE11 (e.g. ES5). Here's a JSFiddle with everything you need: <a href="https://jsfiddle.net/xp5r8961/" target="_blank">jsfiddle.net/xp5r8961</a>
                    – <a href="/users/1548580/demonblack" title="230 reputation" target="_blank">Demonblack</a>
                <a href="#comment79852980_40298390" target="_blank">Sep 27 '17 at 13:06</a>
                        
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-40298390">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-40526517">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Based on @dude answer this should return relevant styles in a object, for instance:</p>

<pre><code>.recurly-input {                                                                                                                                                                             
  display: block;                                                                                                                                                                            
  border-radius: 2px;                                                                                                                                                                        
  -webkit-border-radius: 2px;                                                                                                                                                                
  outline: 0;                                                                                                                                                                                
  box-shadow: none;                                                                                                                                                                          
  border: 1px solid #beb7b3;                                                                                                                                                                 
  padding: 0.6em;                                                                                                                                                                            
  background-color: #f7f7f7;                                                                                                                                                                 
  width:100%;                                                                                                                                                                                
}</code></pre>

<p>This will return:</p>

<pre><code>backgroundColor:
"rgb(247, 247, 247)"
border
:
"1px solid rgb(190, 183, 179)"
borderBottom
:
"1px solid rgb(190, 183, 179)"
borderBottomColor
:
"rgb(190, 183, 179)"
borderBottomLeftRadius
:
"2px"
borderBottomRightRadius
:
"2px"
borderBottomStyle
:
"solid"
borderBottomWidth
:
"1px"
borderColor
:
"rgb(190, 183, 179)"
borderLeft
:
"1px solid rgb(190, 183, 179)"
borderLeftColor
:
"rgb(190, 183, 179)"
borderLeftStyle
:
"solid"
borderLeftWidth
:
"1px"
borderRadius
:
"2px"
borderRight
:
"1px solid rgb(190, 183, 179)"
borderRightColor
:
"rgb(190, 183, 179)"
borderRightStyle
:
"solid"
borderRightWidth
:
"1px"
borderStyle
:
"solid"
borderTop
:
"1px solid rgb(190, 183, 179)"
borderTopColor
:
"rgb(190, 183, 179)"
borderTopLeftRadius
:
"2px"
borderTopRightRadius
:
"2px"
borderTopStyle
:
"solid"
borderTopWidth
:
"1px"
borderWidth
:
"1px"
boxShadow
:
"none"
display
:
"block"
outline
:
"0px"
outlineWidth
:
"0px"
padding
:
"0.6em"
paddingBottom
:
"0.6em"
paddingLeft
:
"0.6em"
paddingRight
:
"0.6em"
paddingTop
:
"0.6em"
width
:
"100%"</code></pre>

<p>Code:</p>

<pre><code>function getStyle(className_) {

    var styleSheets = window.document.styleSheets;
    var styleSheetsLength = styleSheets.length;
    for(var i = 0; i &lt; styleSheetsLength; i++){
        var classes = styleSheets[i].rules || styleSheets[i].cssRules;
        if (!classes)
            continue;
        var classesLength = classes.length;
        for (var x = 0; x &lt; classesLength; x++) {
            if (classes[x].selectorText == className_) {
                return _.pickBy(classes[x].style, (v, k) =&gt; isNaN(parseInt(k)) && typeof(v) == 'string' && v && v != 'initial' && k != 'cssText' )
            }
        }
    }

}</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Nov 10 '16 at 11:28
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
	    <div id="comments-40526517">
                <ul>



    <li id="comment-75136767">
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
                anything without lodash in use? _.pickBy doesn't exist otherwise.
                    – <a href="/users/4228193/mpag" title="131 reputation" target="_blank">mpag</a>
                <a href="#comment75136767_40526517" target="_blank">May 18 '17 at 19:03</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-75137926">
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
                k & v are reversed based on what you're asking of them....  should be return <code>_.pickBy(classes[x].style, (k,v) =&gt; isNaN(parseInt(k)) && typeof(v) == 'string' && v && v != 'initial' && k != 'cssText' )</code>
                    – <a href="/users/4228193/mpag" title="131 reputation" target="_blank">mpag</a>
                <a href="#comment75137926_40526517" target="_blank">May 18 '17 at 19:39</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-40526517">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-45486783">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I created a version that searches all stylesheets and returns matches as a key/value object. You can also specify <strong>startsWith</strong> to match child styles.</p>

<pre><code>getStylesBySelector('.pure-form-html', true);</code></pre>

<p>returns:</p>

<pre><code>{
    ".pure-form-html body": "padding: 0; margin: 0; font-size: 14px; font-family: tahoma;",
    ".pure-form-html h1": "margin: 0; font-size: 18px; font-family: tahoma;"
}</code></pre>

<p>from: </p>

<pre><code>.pure-form-html body {
    padding: 0;
    margin: 0;
    font-size: 14px;
    font-family: tahoma;
}

.pure-form-html h1 {
    margin: 0;
    font-size: 18px;
    font-family: tahoma;
}</code></pre>

<p>The code:</p>

<pre><code>/**
 * Get all CSS style blocks matching a CSS selector from stylesheets
 * @param {string} className - class name to match
 * @param {boolean} startingWith - if true matches all items starting with selector, default = false (exact match only)
 * @example getStylesBySelector('pure-form .pure-form-html ')
 * @returns {object} key/value object containing matching styles otherwise null
 */
function getStylesBySelector(className, startingWith) {

    if (!className || className === '') throw new Error('Please provide a css class name');

    var styleSheets = window.document.styleSheets;
    var result = {};

    // go through all stylesheets in the DOM
    for (var i = 0, l = styleSheets.length; i &lt; l; i++) {

        var classes = styleSheets[i].rules || styleSheets[i].cssRules || [];

        // go through all classes in each document
        for (var x = 0, ll = classes.length; x &lt; ll; x++) {

            var selector = classes[x].selectorText || '';
            var content = classes[x].cssText || classes[x].style.cssText || '';

            // if the selector matches
            if ((startingWith && selector.indexOf(className) === 0) || selector === className) {

                // create an object entry with selector as key and value as content
                result[selector] = content.split(/(?:{|})/)[1].trim();
            }
        }
    }

    // only return object if we have values, otherwise null
    return Object.keys(result).length &gt; 0 ? result : null;
}</code></pre>

<p>I'm using this in production as part of the <a href="https://github.com/john-doherty/pure-form" target="_blank">pure-form</a> project. Hope it helps.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-45486783">
                <ul>



    <li id="comment-79276460">
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
                I'm confused, why the downvotes?
                    – <a href="/users/443431/john-doherty" title="766 reputation" target="_blank">John Doherty</a>
                <a href="#comment79276460_45486783" target="_blank">Sep 11 '17 at 13:47</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-45486783">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-45517927">
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
<p>Here is code to iterate through all rules in a page:</p>

<div>
<div>
<pre><code>function iterateCSS(f) {
  for (const styleSheet of window.document.styleSheets) {
    const classes = styleSheet.rules || styleSheet.cssRules;
    if (!classes) continue;

    for (const cssRule of classes) {
      if (cssRule.type !== 1 || !cssRule.style) continue;
      const selector = cssRule.selectorText, style=cssRule.style;
      if (!selector || !style.cssText) continue;
      for (let i=0; i&lt;style.length; i++) {
        const propertyName=style.item(i);
        if (f(selector, propertyName, style.getPropertyValue(propertyName), style.getPropertyPriority(propertyName), cssRule)===false) return;
      }
    }
  }
}

iterateCSS( (selector, propertyName, propertyValue, propertyPriority, cssRule) =&gt; {
  console.log(selector+' { '+propertyName+': '+propertyValue+(propertyPriority==='important' ? ' !important' : '')+' }');
});</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-45517927">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/html" title="show questions tagged 'html'" target="_blank">html</a> <a href="/questions/tagged/css" title="show questions tagged 'css'" target="_blank">css</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
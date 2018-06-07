<a href="https://stackoverflow.com/questions/2952667/find-all-css-rules-that-apply-to-an-element">https://stackoverflow.com/questions/2952667/find-all-css-rules-that-apply-to-an-element</a><div id="articleHeader"><h1>Find all CSS rules that apply to an element</h1></div>

            

<div id="question">

    
        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        63
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>38</b></div>


</div>

            </div>

            
<div>
    <div>

<p>Many tools/APIs provide ways of selecting elements of specific classes or IDs. There's also possible to inspect the raw stylesheets loaded by the browser.</p>

<p>However, for browsers to render an element, they'll compile all CSS rules (possibly from different stylesheet files) and apply it to the element. This is what you see with Firebug or the WebKit Inspector - the full CSS inheritance tree for an element.</p>

<p>How can I reproduce this feature in pure JavaScript without requiring additional browser plugins?</p>

<p>Perhaps an example can provide some clarification for what I'm looking for:</p>

<pre><code>&lt;style type="text/css"&gt;
    p { color :red; }
    #description { font-size: 20px; }
&lt;/style&gt;

&lt;p id="description"&gt;Lorem ipsum&lt;/p&gt;</code></pre>

<p>Here the p#description element have two CSS rules applied: a red color and a font size of 20 px.</p>

<p>I would like to find the source from where these computed CSS rules originate from (color comes the p rule and so on).</p>
    </div>
    
    <div>
    

    <div>
        <div>
    <div>
        asked Jun 1 '10 at 19:30
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-2953122">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        19
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>EDIT: This answer is now deprecated and <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=437569&desc=2" target="_blank">no longer works in Chrome 64+</a>. Leaving for historical context. In fact that bug report links back to this question for alternative solutions to using this.</p>

<hr />

<p>Seems I managed to answer my own question after another hour of research.</p>

<p>It's as simple as this:</p>

<pre><code>window.getMatchedCSSRules(document.getElementById("description"))</code></pre>

<p>(Works in WebKit/Chrome, possibly others too)</p>
    </div>
    <div>
    
    
            


    <div>
       

    <div>
    <div>
        answered Jun 1 '10 at 20:33
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-12023174">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        15
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Have a look at this library, which does what was asked for:  <a href="http://www.brothercake.com/site/resources/scripts/cssutilities/" target="_blank">http://www.brothercake.com/site/resources/scripts/cssutilities/</a></p>

<p>It works in all modern browsers right back to IE6, can give you rule and property collections like Firebug (in fact it's more accurate than Firebug), and can also calculate the relative or absolute specificity of any rule. The only caveat is that, although it understands static media types, it doesn't understand media-queries.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 18 '12 at 23:59
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-22638396">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        59
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Since this question currently doesn't have a lightweight (non-library), cross-browser compatible answer, I'll try to provide one:</p>

<pre><code>function css(el) {
    var sheets = document.styleSheets, ret = [];
    el.matches = el.matches || el.webkitMatchesSelector || el.mozMatchesSelector 
        || el.msMatchesSelector || el.oMatchesSelector;
    for (var i in sheets) {
        var rules = sheets[i].rules || sheets[i].cssRules;
        for (var r in rules) {
            if (el.matches(rules[r].selectorText)) {
                ret.push(rules[r].cssText);
            }
        }
    }
    return ret;
}</code></pre>

<p>JSFiddle: <a href="http://jsfiddle.net/HP326/6/" target="_blank">http://jsfiddle.net/HP326/6/</a></p>

<p>Calling <code>css(document.getElementById('elementId'))</code> will return an array with an element for each CSS rule that matches the passed element.
If you want to find out more specific information about each rule, check out the <a href="https://developer.mozilla.org/en-US/docs/Web/API/CSSRule" target="_blank">CSSRule object</a> documentation.</p>
    </div>
    <div>
    
    
            


    <div>
       

    <div>
    <div>
        answered Mar 25 '14 at 15:01
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-36126329">
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
<p>Here's a version of S.B.'s answer which also returns matching rules within matching media queries. I've removed the <code>*.rules || *.cssRules</code> coalescence and the <code>.matches</code> implementation finder; add a polyfill or add those lines back in if you need them.</p>

<p>This version also returns the <code>CSSStyleRule</code> objects rather than the rule text. I think this is a little more useful, since the specifics of the rules can be more easily probed programmatically this way.</p>

<p>Coffee:</p>

<pre><code>getMatchedCSSRules = (element) -&gt;
  sheets = document.styleSheets
  matching = []

  loopRules = (rules) -&gt;
    for rule in rules
      if rule instanceof CSSMediaRule
        if window.matchMedia(rule.conditionText).matches
          loopRules rule.cssRules
      else if rule instanceof CSSStyleRule
        if element.matches rule.selectorText
          matching.push rule
    return

  loopRules sheet.cssRules for sheet in sheets

  return matching</code></pre>



<pre><code>function getMatchedCSSRules(element) {
  var i, len, matching = [], sheets = document.styleSheets;

  function loopRules(rules) {
    var i, len, rule;

    for (i = 0, len = rules.length; i &lt; len; i++) {
      rule = rules[i];
      if (rule instanceof CSSMediaRule) {
        if (window.matchMedia(rule.conditionText).matches) {
          loopRules(rule.cssRules);
        }
      } else if (rule instanceof CSSStyleRule) {
        if (element.matches(rule.selectorText)) {
          matching.push(rule);
        }
      }
    }
  };

  for (i = 0, len = sheets.length; i &lt; len; i++) {
    loopRules(sheets[i].cssRules);
  }

  return matching;
}</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-37958301">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        13
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<h1>Short version<sup>12 April 2017</sup></h1>

<p>Challenger appears.</p>

<pre><code>var getMatchedCSSRules = (el, css = el.ownerDocument.styleSheets) =&gt; 
    [].concat(...[...css].map(s =&gt; [...s.cssRules||[]]))     /* 1 */
    .filter(r =&gt; el.matches(r.selectorText));                /* 2 */</code></pre>

<p>Line <code>/* 1 */</code> builds a flat array of all rules.<br />
Line <code>/* 2 */</code> discards non-matching rules.</p>

<p>Based on <a href="https://stackoverflow.com/a/22638396/6314667" target="_blank">function <code>css(el)</code></a> by @S.B. on the same page.</p>

<h3>Example 1</h3>

<pre><code>var div = iframedoc.querySelector("#myelement");
var rules = getMatchedCSSRules(div, iframedoc.styleSheets);
console.log(rules[0].parentStyleSheet.ownerNode, rules[0].cssText);</code></pre>

<h3>Example 2</h3>

<div>
<div>
<pre><code>var getMatchedCSSRules = (el, css = el.ownerDocument.styleSheets) =&gt; 
    [].concat(...[...css].map(s =&gt; [...s.cssRules||[]]))
    .filter(r =&gt; el.matches(r.selectorText));

function Go(big,show) {
    var r = getMatchedCSSRules(big);
PrintInfo:
    var f = (dd,rr,ee="\n") =&gt; dd + rr.cssText.slice(0,50) + ee;
    show.value += "--------------- Rules: ----------------\n";
    show.value += f("Rule 1:   ", r[0]);
    show.value += f("Rule 2:   ", r[1]);
    show.value += f("Inline:   ", big.style);
    show.value += f("Computed: ", getComputedStyle(big), "(…)\n");
    show.value += "-------- Style element (HTML): --------\n";
    show.value += r[0].parentStyleSheet.ownerNode.outerHTML;
}

Go(...document.querySelectorAll("#big,#show"));</code></pre>
<pre><code>.red {color: red;}
#big {font-size: 20px;}</code></pre>
<pre><code>&lt;h3 id="big" class="red" style="margin: 0"&gt;Lorem ipsum&lt;/h3&gt;
&lt;textarea id="show" cols="70" rows="10"&gt;&lt;/textarea&gt;</code></pre>
<div><div><div><a target="_blank">Full page</a></div></div></div></div>
</div>
<h3>Shortcomings</h3>

<ul>
<li>No media handling, no <code>@import</code>, <code>@media</code>.</li>
<li>No access to styles loaded from cross-domain stylesheets.</li>
<li>No sorting by selector “specificity” (order of importance).</li>
<li>No styles inherited from parents.</li>
<li>May not work with old or rudimentary browsers.</li>
<li>Not sure how it copes with pseudo-classes and pseudo-selectors but seems to fare okay.</li>
</ul>

<p>Maybe I will address these shortcomings one day.</p>

<h1>Long version<sup>4 May 2017</sup></h1>

<p>Here’s a much more comprehensive implementation taken from <a href="https://gist.github.com/ssafejava/6605832" target="_blank">someone’s GitHub page</a>
(forked from this <a href="https://gist.github.com/ydaniv/3033012" target="_blank">original code</a>, via <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=438278" target="_blank">Bugzilla</a>). Written for Gecko and IE, but is rumoured to work also with Blink.</p>

<p><strong>4 May 2017:</strong> The specificity calculator has had critical bugs which I have now fixed. (I can’t notify the authors because I don’t have a GitHub account.)</p>

<pre><code>// polyfill window.getMatchedCSSRules() in FireFox 6+
if (typeof window.getMatchedCSSRules !== 'function') {
    var ELEMENT_RE = /[\w-]+/g,
            ID_RE = /#[\w-]+/g,
            CLASS_RE = /\.[\w-]+/g,
            ATTR_RE = /\[[^\]]+\]/g,
            // :not() pseudo-class does not add to specificity, but its content does as if it was outside it
            PSEUDO_CLASSES_RE = /\:(?!not)[\w-]+(\(.*\))?/g,
            PSEUDO_ELEMENTS_RE = /\:\:?(after|before|first-letter|first-line|selection)/g;
        // convert an array-like object to array
        function toArray(list) {
            return [].slice.call(list);
        }

        // handles extraction of `cssRules` as an `Array` from a stylesheet or something that behaves the same
        function getSheetRules(stylesheet) {
            var sheet_media = stylesheet.media && stylesheet.media.mediaText;
            // if this sheet is disabled skip it
            if ( stylesheet.disabled ) return [];
            // if this sheet's media is specified and doesn't match the viewport then skip it
            if ( sheet_media && sheet_media.length && ! window.matchMedia(sheet_media).matches ) return [];
            // get the style rules of this sheet
            return toArray(stylesheet.cssRules);
        }

        function _find(string, re) {
            var matches = string.match(re);
            return matches ? matches.length : 0;
        }

        // calculates the specificity of a given `selector`
        function calculateScore(selector) {
            var score = [0,0,0],
                parts = selector.split(' '),
                part, match;
            //TODO: clean the ':not' part since the last ELEMENT_RE will pick it up
            while (part = parts.shift(), typeof part == 'string') {
                // find all pseudo-elements
                match = _find(part, PSEUDO_ELEMENTS_RE);
                score[2] += match;
                // and remove them
                match && (part = part.replace(PSEUDO_ELEMENTS_RE, ''));
                // find all pseudo-classes
                match = _find(part, PSEUDO_CLASSES_RE);
                score[1] += match;
                // and remove them
                match && (part = part.replace(PSEUDO_CLASSES_RE, ''));
                // find all attributes
                match = _find(part, ATTR_RE);
                score[1] += match;
                // and remove them
                match && (part = part.replace(ATTR_RE, ''));
                // find all IDs
                match = _find(part, ID_RE);
                score[0] += match;
                // and remove them
                match && (part = part.replace(ID_RE, ''));
                // find all classes
                match = _find(part, CLASS_RE);
                score[1] += match;
                // and remove them
                match && (part = part.replace(CLASS_RE, ''));
                // find all elements
                score[2] += _find(part, ELEMENT_RE);
            }
            return parseInt(score.join(''), 10);
        }

        // returns the heights possible specificity score an element can get from a give rule's selectorText
        function getSpecificityScore(element, selector_text) {
            var selectors = selector_text.split(','),
                selector, score, result = 0;
            while (selector = selectors.shift()) {
                if (matchesSelector(element, selector)) {
                    score = calculateScore(selector);
                    result = score &gt; result ? score : result;
                }
            }
            return result;
        }

        function sortBySpecificity(element, rules) {
            // comparing function that sorts CSSStyleRules according to specificity of their `selectorText`
            function compareSpecificity (a, b) {
                return getSpecificityScore(element, b.selectorText) - getSpecificityScore(element, a.selectorText);
            }

            return rules.sort(compareSpecificity);
        }

        // Find correct matchesSelector impl
        function matchesSelector(el, selector) {
          var matcher = el.matchesSelector || el.mozMatchesSelector || 
              el.webkitMatchesSelector || el.oMatchesSelector || el.msMatchesSelector;
          return matcher(selector);
        }

        //TODO: not supporting 2nd argument for selecting pseudo elements
        //TODO: not supporting 3rd argument for checking author style sheets only
        window.getMatchedCSSRules = function (element /*, pseudo, author_only*/) {
            var style_sheets, sheet, sheet_media,
                rules, rule,
                result = [];
            // get stylesheets and convert to a regular Array
            style_sheets = toArray(window.document.styleSheets);

            // assuming the browser hands us stylesheets in order of appearance
            // we iterate them from the beginning to follow proper cascade order
            while (sheet = style_sheets.shift()) {
                // get the style rules of this sheet
                rules = getSheetRules(sheet);
                // loop the rules in order of appearance
                while (rule = rules.shift()) {
                    // if this is an @import rule
                    if (rule.styleSheet) {
                        // insert the imported stylesheet's rules at the beginning of this stylesheet's rules
                        rules = getSheetRules(rule.styleSheet).concat(rules);
                        // and skip this rule
                        continue;
                    }
                    // if there's no stylesheet attribute BUT there IS a media attribute it's a media rule
                    else if (rule.media) {
                        // insert the contained rules of this media rule to the beginning of this stylesheet's rules
                        rules = getSheetRules(rule).concat(rules);
                        // and skip it
                        continue
                    }

                    // check if this element matches this rule's selector
                    if (matchesSelector(element, rule.selectorText)) {
                        // push the rule to the results set
                        result.push(rule);
                    }
                }
            }
            // sort according to specificity
            return sortBySpecificity(element, result);
        };
}</code></pre>

<h3>Fixed bugs</h3>

<ul>
<li><code>= match</code> → <code>+= match</code></li>
<li><code>return re ? re.length : 0;</code> → <code>return matches ? matches.length : 0;</code></li>
<li><code>_matchesSelector(element, selector)</code> → <code>matchesSelector(element, selector)</code></li>
</ul>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-39772849">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div><div>
<div>
<pre><code>var GetMatchedCSSRules = (elem, css = document.styleSheets) =&gt; Array.from(css)
  .map(s =&gt; Array.from(s.cssRules).filter(r =&gt; elem.matches(r.selectorText)))
  .reduce((a,b) =&gt; a.concat(b));

function Go(paragraph, print) {
  var rules = GetMatchedCSSRules(paragraph);
PrintInfo:
  print.value += "Rule 1: " + rules[0].cssText + "\n";
  print.value += "Rule 2: " + rules[1].cssText + "\n\n";
  print.value += rules[0].parentStyleSheet.ownerNode.outerHTML;
}

Go(document.getElementById("description"), document.getElementById("print"));</code></pre>
<pre><code>p {color: red;}
#description {font-size: 20px;}</code></pre>
<pre><code>&lt;p id="description"&gt;Lorem ipsum&lt;/p&gt;
&lt;textarea id="print" cols="50" rows="12"&gt;&lt;/textarea&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Sep 29 '16 at 14:18
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-42844146">
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
<p>Ensuring IE9+, I wrote a function which calculates CSS for requested element and its children, and gives possibility to save it to a new className if needed in snippet below.</p>

<pre><code>/**
  * @function getElementStyles
  *
  * Computes all CSS for requested HTMLElement and its child nodes and applies to dummy class
  *
  * @param {HTMLElement} element
  * @param {string} className (optional)
  * @param {string} extras (optional)
  * @return {string} CSS Styles
  */
function getElementStyles(element, className, addOnCSS) {
  if (element.nodeType !== 1) {
    return;
  }
  var styles = '';
  var children = element.getElementsByTagName('*');
  className = className || '.' + element.className.replace(/^| /g, '.');
  addOnCSS = addOnCSS || '';
  styles += className + '{' + (window.getComputedStyle(element, null).cssText + addOnCSS) + '}';
  for (var j = 0; j &lt; children.length; j++) {
    if (children[j].className) {
      var childClassName = '.' + children[j].className.replace(/^| /g, '.');
      styles += ' ' + className + '&gt;' + childClassName +
        '{' + window.getComputedStyle(children[j], null).cssText + '}';
    }
  }
  return styles;
}</code></pre>

<p><strong>Usage</strong></p>

<pre><code>getElementStyles(document.getElementByClassName('.my-class'), '.dummy-class', 'width:100%;opaity:0.5;transform:scale(1.5);');</code></pre>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/css" title="show questions tagged 'css'" target="_blank">css</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
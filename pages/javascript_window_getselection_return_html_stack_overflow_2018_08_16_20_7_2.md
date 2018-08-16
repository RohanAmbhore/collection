<a href="https://stackoverflow.com/questions/5222814/window-getselection-return-html">https://stackoverflow.com/questions/5222814/window-getselection-return-html</a><div id="articleHeader"><h1>window.getSelection return html</h1></div>

            

<div id="question">

    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        3
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>3</b></div>



</div>

            </div>

            
<div>
    <div>

<div>
    <p>This question already has an answer here:</p>
    <ul>
        <li>
            <a href="/questions/4176923/html-of-selected-text" target="_blank">HTML of selected text</a>
                
                    1 answer
                
        </li>
    </ul>
    </div>
<pre><code>function selected() {
   var selObj = window.getSelection();
}</code></pre>

<p>
This function returns selected text from a webpage. How do return the <strong>html</strong> of a selected area. Is this possible to do with an <code>&lt;img&gt;</code> and an <code>&lt;a&gt;</code> tag?</p>

<p>
Here's the list of functions:<br />
<a href="https://developer.mozilla.org/Special:Tags?tag=DOM&language=en" target="_blank">https://developer.mozilla.org/Special:Tags?tag=DOM&language=en</a></p>
    </div>
    
    <div>
    

    <div>
        <div>
    <div>
        asked Mar 7 '11 at 17:18
    </div>
    
    
</div>
    </div>
    </div>
</div>

                        <div>
                <div>
        <h2>                    <b>marked</b> as duplicate by <a href="/users/9913/jedidja" target="_blank">Jedidja</a>, <a href="/users/2287470/joe" target="_blank">Joe</a>, <a href="/users/529548/khr055" target="_blank">khr055</a>, <a href="/users/844923/craigteegarden" target="_blank">CraigTeegarden</a>, <a href="/users/223391/jball" target="_blank">jball</a> Jun 20 '13 at 16:33
</h2>
        <p>This question has been asked before and already has an answer. If those answers do not fully address your question, please <a href="/questions/ask" target="_blank">ask a new question</a>.</p>
    </div>
            </div>
    
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-5222955">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        18
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted


</div>

            </div>
            


<div>
    <div>
<p>The following will do this in all major browsers and is an exact duplicate of <a href="https://stackoverflow.com/a/4177234/96100" target="_blank">this answer</a>:</p>

<pre><code>function getSelectionHtml() {
    var html = "";
    if (typeof window.getSelection != "undefined") {
        var sel = window.getSelection();
        if (sel.rangeCount) {
            var container = document.createElement("div");
            for (var i = 0, len = sel.rangeCount; i &lt; len; ++i) {
                container.appendChild(sel.getRangeAt(i).cloneContents());
            }
            html = container.innerHTML;
        }
    } else if (typeof document.selection != "undefined") {
        if (document.selection.type == "Text") {
            html = document.selection.createRange().htmlText;
        }
    }
    return html;
}</code></pre>
    </div>
    
</div>
    
        </div>
</div>
                


                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/jquery" title="show questions tagged 'jquery'" target="_blank">jquery</a> <a href="/questions/tagged/html" title="show questions tagged 'html'" target="_blank">html</a> <a href="/questions/tagged/dom" title="show questions tagged 'dom'" target="_blank">dom</a> <a href="/questions/tagged/execcommand" title="show questions tagged 'execcommand'" target="_blank">execcommand</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
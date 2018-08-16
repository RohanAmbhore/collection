<a href="https://stackoverflow.com/questions/4176923/html-of-selected-text/4177234#4177234">https://stackoverflow.com/questions/4176923/html-of-selected-text/4177234#4177234</a><div id="articleHeader"><h1>HTML of selected text</h1></div>

            

<div id="question">

    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        14
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>13</b></div>



</div>

            </div>

            
<div>
    <div>

<p>Is there a cross-browser way to get HTML of selected text?</p>
    </div>
    <div>
        <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> 
    </div>
    <div>
    

    <div>
        <div>
    <div>
        asked Nov 14 '10 at 9:32
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-4177234">
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
<p>This function will do it in all major browsers:</p>

<div>
<div>
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
}


// bind events for selection

document.addEventListener('mouseup', function(){
  var selectedHTML = getSelectionHtml();
  if( selectedHTML )
    console.log( selectedHTML )
});

document.addEventListener('keyup', function(e){ 
  var selectedHTML, key = e.keyCode || e.which; 
  if( key == 16 ){ // if "shift" key was released
    selectedHTML = getSelectionHtml();
    if( selectedHTML )
      console.log( selectedHTML )
  }
});</code></pre>
<pre><code>&lt;ul contenteditable&gt;
  &lt;li&gt;&lt;p&gt;Select &lt;b&gt;this&lt;/b&gt; &lt;em&gt;text&lt;/em&gt; right &lt;i&gt;here&lt;/i&gt;&lt;/p&gt;&lt;/li&gt;
  &lt;li&gt;Or &lt;b&gt;this text&lt;/b&gt;&lt;/li&gt;
&lt;/ul&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    <div>
    
    
            


    <div>
       

    <div>
    <div>
        answered Nov 14 '10 at 11:23
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
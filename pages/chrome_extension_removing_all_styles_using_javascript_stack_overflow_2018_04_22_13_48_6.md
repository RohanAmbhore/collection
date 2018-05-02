<a href="https://stackoverflow.com/questions/48434105/chrome-extension-removing-all-styles-using-javascript?noredirect=1&lq=1">https://stackoverflow.com/questions/48434105/chrome-extension-removing-all-styles-using-javascript?noredirect=1&lq=1</a><div id="articleHeader"><h1>Chrome Extension: Removing all styles using Javascript</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        0
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>1</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I'm admittedly a bit new to this; I know HTML/CSS more then I know Javascript. I know enough to code an extension, but I'm having problems that I believe may be specific to Chrome. I don't want to be too specific, but as part of my extension I'd like to remove styles from all webpages.</p>

<p>Here's what I have:</p>

<p><strong>manifest.json</strong></p>

<pre><code>{
"manifest_version": 2,
    "name": "[redacted]",
    "description": "[redacted]",
    "version": "1.0",
    "content_scripts": [
        {
            "matches": ["&lt;all_urls&gt;"],
            "js": ["script.js"],
                "run_at": "document_start"
        }
    ]
}</code></pre>

<p><strong>script.js</strong></p>

<pre><code>function lolxd() {
    var hs = document.getElementsByTagName('style');
    for (var i=0, max = hs.length; i &lt; max; i++) {
        hs[i].parentNode.removeChild(hs[i]);
}

window.onload = lolxd();</code></pre>

<p>I've tried multiple different scripts, none of which have worked. Strangely the extension loads fine, but the Javascript doesn't work and I can still see styles on all webpages. Any help?</p>
    </div>
    
    <div>
    

    <div>
        <div>
    <div>
        asked Jan 25 at 1:06
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-48456266">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>You can recursively iterate through all elements and remove the style attribute, remove all linked (external) stylesheets and embedded stylesheets. </p>

<p><strong>BEFORE</strong></p>

<div>
<div>
<pre><code>&lt;!DOCTYPE html&gt;
&lt;html&gt;

&lt;head&gt;
  &lt;link rel="stylesheet" href="https://www.w3schools.com/html/styles.css"&gt;
  &lt;style&gt;
    p {
      font-size: 150%;
    }
  &lt;/style&gt;
&lt;/head&gt;

&lt;body&gt;

  &lt;h1&gt;This is a heading&lt;/h1&gt;
  &lt;p style="font-weight: bold;"&gt;This is a paragraph.&lt;/p&gt;

&lt;/body&gt;

&lt;/html&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
<p><strong>AFTER</strong></p>

<div>
<div>
<pre><code>function removeStyles(el) {
  // code to remove inline styles 
  el.removeAttribute('style');

  if (el.childNodes.length &gt; 0) {
    for (var child in el.childNodes) {
      /* filter element nodes only */
      if (el.childNodes[child].nodeType == 1)
        removeStyles(el.childNodes[child]);
    }
  }

  // code to remove embedded style sheets 

  var styletag = document.getElementsByTagName('style');
  var i = 0;
  for (; i &lt; styletag.length; i++) {
    styletag[i].remove();
  }

  // code to remove external stylesheets
  var stylesheets = document.getElementsByTagName('link'),
    sheet;

  for (i = 0; i &lt; stylesheets.length; i++) {
    sheet = stylesheets[i];

    if (sheet.getAttribute('rel').toLowerCase() == 'stylesheet')
      sheet.parentNode.removeChild(sheet);
  }
}

removeStyles(document.body);</code></pre>
<pre><code>&lt;!DOCTYPE html&gt;
&lt;html&gt;

&lt;head&gt;
  &lt;link rel="stylesheet" href="https://www.w3schools.com/html/styles.css"&gt;
  &lt;style&gt;
    p {
      font-size: 150%;
    }
  &lt;/style&gt;
&lt;/head&gt;

&lt;body&gt;

  &lt;h1&gt;This is a heading&lt;/h1&gt;
  &lt;p style="font-weight: bold;"&gt;This is a paragraph.&lt;/p&gt;

&lt;/body&gt;

&lt;/html&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 26 at 5:37
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-48435418">
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
<p>like this:</p>

<pre><code>function removeCSS() {
    // remove `link`
    var links = document.getElementsByTagName('link');
    for(var i = 0, len = links.length; i &lt; len; i++) {
        links[i].parentNode.removeChild(links[i]);
    }

    // remove `style`
    var styles = document.getElementsByTagName('style');
    for(var j = 0, len = styles.length; j &lt; len; j++) {
        styles[j].parentNode.removeChild(styles[j]);
    }

    // remove inline style
    var nodes = document.querySelectorAll('[style]');
    for(var h = 0, len = nodes.length; h &lt; len; h++) {
        nodes[h].removeAttribute('style');
    }
}</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 25 at 3:56
    </div>
    
    
</div>
    </div>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a>   or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="https://stackoverflow.com/questions/10730309/find-all-text-nodes-in-html-page">https://stackoverflow.com/questions/10730309/find-all-text-nodes-in-html-page</a><div id="articleHeader"><h1>Find all text nodes in HTML page</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        26
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>17</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<blockquote>
  <p><strong>Possible Duplicate:</strong><br />
  <a href="https://stackoverflow.com/questions/2579666/getelementsbytagname-equivalent-for-textnodes" target="_blank">getElementsByTagName() equivalent for textNodes</a>  </p>
</blockquote>



<p>For <a href="https://stackoverflow.com/questions/10729983/highlight-word-in-html-text-but-not-markup/10730063#10730063" target="_blank">this question</a> I needed to find all text nodes under a particular node. I <em>can</em> do this like so:</p>

<pre><code>function textNodesUnder(root){
  var textNodes = [];
  addTextNodes(root);
  [].forEach.call(root.querySelectorAll('*'),addTextNodes);
  return textNodes;

  function addTextNodes(el){
    textNodes = textNodes.concat(
      [].filter.call(el.childNodes,function(k){
        return k.nodeType==Node.TEXT_NODE;
      })
    );
  }
}</code></pre>

<p>However, this seems inelegant in light of the fact that with XPath one could simply query for <code>.//text()</code> and be done with it.</p>

<p><strong>What's the simplest way to get all text nodes under a particular element in an HTML document, that works on IE9+, Safari5+, Chrome19+, Firefox12+, Opera11+?</strong></p>

<p><em>"Simplest" is defined loosely as "efficient and short, without golfing".</em></p>
    </div>
    
    
</div>
</td>
        </tr>
                    <tr>
            <td colspan="2">
                <div>
        <h2>                    <b>marked</b> as duplicate by <a href="/users/480674/pedrofurla" target="_blank">pedrofurla</a>, <a href="/users/255562/ashish-gupta" target="_blank">Ashish Gupta</a>, <a href="/users/4794/don-kirkby" target="_blank">Don Kirkby</a>, <a href="/users/1491895/barmar" target="_blank">Barmar</a>, <a href="/users/750613/nikhil" target="_blank">Nikhil</a> Oct 15 '12 at 6:01
</h2>
        <p>This question has been asked before and already has an answer. If those answers do not fully address your question, please <a href="/questions/ask" target="_blank">ask a new question</a>.</p>
    </div>
            </td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-10730309">
		        <table>
                    <tbody>



    <tr id="comment-13939506">
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
            
        </td>
    </tr>
    <tr id="comment-13939563">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
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
                Aw, bugger. Thanks, Jack, I did search but failed to find that question.
                    – <a href="/users/405017/phrogz" title="200,759 reputation" target="_blank">Phrogz</a>
                <a href="#comment13939563_10730309" target="_blank">May 24 '12 at 3:13</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-13939670">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
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
                Yeah, I don't know why it didn't show up in the side bar either, but I found it while doing a Google search :)
                    – <a href="/users/1338292/ja%cd%a2ck" title="135,334 reputation" target="_blank">Ja͢ck</a>
                <a href="#comment13939670_10730309" target="_blank">May 24 '12 at 3:26</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-10730309">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-10730777">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        86
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p><em>Based on @kennebec's answer, a slightly tighter implementation of the same logic:</em></p>

<pre><code>function textNodesUnder(node){
  var all = [];
  for (node=node.firstChild;node;node=node.nextSibling){
    if (node.nodeType==3) all.push(node);
    else all = all.concat(textNodesUnder(node));
  }
  return all;
}</code></pre>

<p><em>However, far faster, tighter, and more elegant is using <a href="https://developer.mozilla.org/en/DOM/document.createTreeWalker" target="_blank"><code>createTreeWalker</code></a> so that the browser filters out everything but the text nodes for you:</em></p>

<pre><code>function textNodesUnder(el){
  var n, a=[], walk=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null,false);
  while(n=walk.nextNode()) a.push(n);
  return a;
}</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-10730777">
		        <table>
                    <tbody>



    <tr id="comment-61028882">
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
                @julmot On my computer, looking for all text nodes on this page using Chrome v50, it takes 1900μs using the first technique, but 220μs using the TreeWalker technique. So, 8 or 9 times faster.
                    – <a href="/users/405017/phrogz" title="200,759 reputation" target="_blank">Phrogz</a>
                <a href="#comment61028882_10730777" target="_blank">Apr 19 '16 at 14:59</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-65977439">
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
            
        </td>
    </tr>
    <tr id="comment-77636135">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
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
                If you're using the TreeWalker method and you want to exclude script or style tags as Web_Designer mentioned, you can pass a filter as the third argument to createTreeWalker
                    – <a href="/users/468495/vinay-pai" title="3,275 reputation" target="_blank">Vinay Pai</a>
                <a href="#comment77636135_10730777" target="_blank">Jul 26 '17 at 20:44</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-10730777">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-10730367">
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
<pre><code>function deepText(node){
    var A= [];
    if(node){
        node= node.firstChild;
        while(node!= null){
            if(node.nodeType== 3) A[A.length]=node;
            else A= A.concat(deepText(node));
            node= node.nextSibling;
        }
    }
    return A;
}</code></pre>
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
        answered May 24 '12 at 2:31
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
	    <div id="comments-10730367">
		        <table>
                    <tbody>



    <tr id="comment-13939180">
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
                How about <code>while (node)</code> without the <code>!= null</code>?
                    – <a href="/users/405017/phrogz" title="200,759 reputation" target="_blank">Phrogz</a>
                <a href="#comment13939180_10730367" target="_blank">May 24 '12 at 2:33</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-13939270">
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
                Or even <code>for (node=node.firstChild;node;node=node.nextSibling){ … }</code>
                    – <a href="/users/405017/phrogz" title="200,759 reputation" target="_blank">Phrogz</a>
                <a href="#comment13939270_10730367" target="_blank">May 24 '12 at 2:43</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-13939300">
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
                I was worried that the recursive solution might run into stack limit issues, but <a href="http://stackoverflow.com/questions/7826992/browser-javascript-stack-size-limit" target="_blank">I see now that this is unlikely</a>.
                    – <a href="/users/405017/phrogz" title="200,759 reputation" target="_blank">Phrogz</a>
                <a href="#comment13939300_10730367" target="_blank">May 24 '12 at 2:46</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-13939906">
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
                Once you know the first (parent) node is a child node the only possible values for node.nextSibling are another child node or null.
                    – <a href="/users/80860/kennebec" title="70,244 reputation" target="_blank">kennebec</a>
                <a href="#comment13939906_10730367" target="_blank">May 24 '12 at 3:55</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-10730367">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                


                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/html" title="show questions tagged 'html'" target="_blank">html</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
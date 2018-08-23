<a href="https://stackoverflow.com/questions/8632410/style-webkit-scrollbar-on-certain-state">https://stackoverflow.com/questions/8632410/style-webkit-scrollbar-on-certain-state</a><div id="articleHeader"><h1>Style webkit scrollbar on certain state</h1></div>

            

<div id="question">

    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        2
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>1</b></div>



</div>

            </div>

            
<div>
    <div>

<p>I'd like my <a href="http://www.webkit.org/blog/363/styling-scrollbars/" target="_blank">WebKit scrollbars</a> to have a different color when its container is hovered over. I want the entire scrollbar to light up.</p>

<p>I was thinking something like this would do the trick (but it doesn't):</p>

<pre><code>.scroller:hover::-webkit-scrollbar {
  background: green;
}</code></pre>

<p>I've styled the scrollbars the same way: on <code>.scroller</code>, not globally. (That works: <code>.scroller::-webkit-scrollbar</code>) I want the overflowed divs special, not the document.</p>

<p>Another (related) problem: light up the thumb when hovering over the scrollbar. This doesn't work:</p>

<pre><code>.scroller::-webkit-scrollbar:hover ::-webkit-scrollbar-thumb</code></pre>
    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-8633218">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted


</div>

            </div>
            


<div>
    <div>
<p>Changing the background color works just fine for me.</p>

<p><a href="http://jsfiddle.net/QcqBM/1" target="_blank">http://jsfiddle.net/QcqBM/1</a></p>

<pre><code>div#container:hover::-webkit-scrollbar {
    background: lightyellow;
}</code></pre>

<p>Are you sure there isn't something else wrong with your CSS call?</p>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered Dec 26 '11 at 5:40
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-19171215">
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
<p>This is possible using pure CSS, at least with Chrome version 29.</p>

<p><a href="http://jsfiddle.net/eR9SP/" target="_blank">http://jsfiddle.net/eR9SP/</a></p>

<p>To style the scrollbar when its container (in this case <code>.scroller</code>) is hovered over, use:</p>

<pre><code>.scroller:hover::-webkit-scrollbar { /* styles for scrollbar */ }
.scroller:hover::-webkit-scrollbar-thumb { /* styles for scrollbar thumb */ }
.scroller:hover::-webkit-scrollbar-track { /* styles for scrollbar track */ }</code></pre>

<p>Additionally, you can style the scrollbar thumb itself when it's hovered over or active (being clicked) using the following:</p>

<pre><code>.scroller::-webkit-scrollbar-thumb:horizontal:hover,
.scroller::-webkit-scrollbar-thumb:vertical:hover { /* hover thumb styles */ }
.scroller::-webkit-scrollbar-thumb:horizontal:active,
.scroller::-webkit-scrollbar-thumb:vertical:active { /* active thumb styles */ }</code></pre>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered Oct 4 '13 at 0:20
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/css" title="show questions tagged 'css'" target="_blank">css</a> <a href="/questions/tagged/webkit" title="show questions tagged 'webkit'" target="_blank">webkit</a> <a href="/questions/tagged/scrollbar" title="show questions tagged 'scrollbar'" target="_blank">scrollbar</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
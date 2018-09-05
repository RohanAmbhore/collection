<a href="https://stackoverflow.com/questions/43974824/align-self-flex-end-not-moving-item-to-bottom/43974846">https://stackoverflow.com/questions/43974824/align-self-flex-end-not-moving-item-to-bottom/43974846</a><div id="articleHeader"><h1>align-self: flex-end not moving item to bottom</h1></div>

            

<div id="question">

    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        14
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>2</b></div>



</div>

            </div>

            
<div>
    <div>


<p>As you can see here: <a href="https://jsfiddle.net/0zq5a5xu/1/" target="_blank">JSFiddle</a> </p>

<p>I want author div to be at the bottom of his parent container. I tried with <code>align-self: flex-end;</code> but it's not working. What am I doing wrong?</p>

<div>
<div>
<pre><code>.flexbox {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.item {
  display: flex;
  flex-direction: column;
  width: 100px;
  border: 1px solid #000;
  padding: 10px;
}

.item .author {
  width: 100%;
  align-self: flex-end;
  border: 1px solid #000;
}</code></pre>
<pre><code>&lt;div class="flexbox"&gt;

  &lt;div class="item"&gt;
    &lt;div class="title"&gt;
      Title
    &lt;/div&gt;
    &lt;div class="content"&gt;
      Content
    &lt;/div&gt;
    &lt;div class="author"&gt;
      Author
    &lt;/div&gt;
  &lt;/div&gt;

  &lt;div class="item"&gt;
    &lt;div class="title"&gt;
      Title
    &lt;/div&gt;
    &lt;div class="content"&gt;
      Content&lt;br&gt;Content
    &lt;/div&gt;
    &lt;div class="author"&gt;
      Author
    &lt;/div&gt;
  &lt;/div&gt;

  &lt;div class="item"&gt;
    &lt;div class="title"&gt;
      Title
    &lt;/div&gt;
    &lt;div class="content"&gt;
      Content&lt;br&gt;Content&lt;br&gt;Content
    &lt;/div&gt;
    &lt;div class="author"&gt;
      Author
    &lt;/div&gt;
  &lt;/div&gt;

&lt;/div&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    
    
</div>

                        <div>
                <div>
        <h2>                    <b>marked</b> as duplicate by <a href="/users/3597276/michael-b" target="_blank">Michael_B</a><a href="/badges/tag-badges/css?badgeClass=Gold" target="_blank"> css</a>

 May 15 '17 at 19:07
</h2>
        <p>This question has been asked before and already has an answer. If those answers do not fully address your question, please <a href="/questions/ask" target="_blank">ask a new question</a>.</p>
    </div>
            </div>
    
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-43974846">
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
<p>Try add to .author</p>

<pre><code>margin-top: auto;</code></pre>

<p>You also need to remove flex-end.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-43974977">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>





</div>

            </div>
            


<div>
    <div>
<p>You can make a wrapper div around the divs which have to float from flex start. And the author outside the wrapper and give to <code>.item</code> <code>justify-content: space-between;</code>.</p>

<p><a href="https://jsfiddle.net/0zq5a5xu/2/" target="_blank">https://jsfiddle.net/0zq5a5xu/2/</a></p>

<div>
<div>
<pre><code>.flexbox {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.item {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 100px;
  border: 1px solid #000;
  padding: 10px;
}

.wrapper {
  display: flex;
  flex-direction: column;
}

.author {
  width: 100%;
  border: 1px solid #000;
}</code></pre>
<pre><code>&lt;div class="flexbox"&gt;

  &lt;div class="item"&gt;
    &lt;div class="wrapper"&gt;
      &lt;div class="title"&gt;
        Title
      &lt;/div&gt;
      &lt;div class="content"&gt;
        Content
      &lt;/div&gt;
    &lt;/div&gt;

    &lt;div class="author"&gt;
      Author
    &lt;/div&gt;
  &lt;/div&gt;

  &lt;div class="item"&gt;
    &lt;div class="wrapper"&gt;
      &lt;div class="title"&gt;
        Title
      &lt;/div&gt;
      &lt;div class="content"&gt;
        Content&lt;br&gt;Content
      &lt;/div&gt;
    &lt;/div&gt;
    &lt;div class="author"&gt;
      Author
    &lt;/div&gt;
  &lt;/div&gt;

  &lt;div class="item"&gt;
    &lt;div class="wrapper"&gt;
      &lt;div class="title"&gt;
        Title
      &lt;/div&gt;
      &lt;div class="content"&gt;
        Content&lt;br&gt;Content&lt;br&gt;Content
      &lt;/div&gt;
    &lt;/div&gt;
    &lt;div class="author"&gt;
      Author
    &lt;/div&gt;
  &lt;/div&gt;


&lt;/div&gt;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
<p>Hope this helps.</p>
    </div>
    <div>
    
            


    <div>
<div>
    <div>
        answered May 15 '17 at 8:45
    </div>
    
    
</div>

    </div>
    </div>
</div>
    
        </div>
</div>
                


                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/html" title="show questions tagged 'html'" target="_blank">html</a> <a href="/questions/tagged/css" title="show questions tagged 'css'" target="_blank">css</a> <a href="/questions/tagged/css3" title="show questions tagged 'css3'" target="_blank">css3</a> <a href="/questions/tagged/flexbox" title="show questions tagged 'flexbox'" target="_blank">flexbox</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
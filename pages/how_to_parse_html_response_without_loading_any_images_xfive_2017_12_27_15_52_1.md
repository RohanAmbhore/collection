<a href="https://www.xfive.co/blog/how-to-parse-html-response-without-loading-any-images/">https://www.xfive.co/blog/how-to-parse-html-response-without-loading-any-images/</a><div id="articleHeader"><h1>How to parse HTML response without loading any images</h1></div>
  <div>
    <i>by</i> <a href="/blog/author/michal/" target="_blank">Michal Pierzchala</a> <i>on</i> August 12, 2015
  </div>
  


    
    
  
  
    <p>Or: How I stopped worrying and learned to createHTMLDocument.</p>
    <section>
      <p><i>—–</i></p>
<p><strong>TL;DR</strong></p>
<p><strong>If you want to parse HTML response without loading any unnecessary resources like images or scripts inside, use DOMImplementation’s <a href="https://developer.mozilla.org/en-US/docs/Web/API/DOMImplementation/createHTMLDocument" target="_blank">createHTMLDocument()</a><br />
to create new <a href="https://developer.mozilla.org/en-US/docs/Web/API/Document" target="_blank">document</a> which is not connected to the current one parsed by the browser and behaves as well as normal document.</strong></p>
<p><i>—–</i></p>
<p>There are times when as a frontend developer you can’t always use RESTful APIs providing well formatted JSON server responses with which you can do whatever you like. Sometimes you just have to use HTML responses, no matter how badly it sounds.</p>
<p>While working on our latest project I came across an interesting case. One of the project’s requirements was to have some of the corresponding pages’ content (basically a hero section) preloaded. The solution was maybe not the best, but it was quite simple :</p>
<ol>
<li>Send an AJAX request for the desired page.</li>
<li>Get its whole HTML in the response (partial was not an option here)</li>
<li>Create new document element or jQuery object from it just to find the needed section</li>
<li>Append it to your current document when needed.</li>
</ol>
<p><strong>Simple, works, we can go home now. Well, nope.</strong></p>
<p>Later on, while testing network usage, I realised that actually there are some images loaded, which should not be there. What the-? They’re not even in the DOM. Actually, they were there. Not rendered and attached, but created in the context of current <a href="https://developer.mozilla.org/en-US/docs/Web/API/Document" target="_blank">document</a>.</p>
<p>Calling document.createElement(el).innerHTML(data) or with jQuery $(data) creates a node in current document which triggers the browser to treat it like the rest of the page, which means loading all of the resources like images, scripts, etc. inside.</p>
<h2>So, what’s the solution to that?</h2>
<p>I’ve read whole stories about replacing src attributes with some dummy data and restoring them later, removing &lt;img&gt; elements with RegEx (sic!), storing them somewhere and recreate when needed, even using web workers to provide some better performance. None of this crap.</p>
<h2>Better and easier solution</h2>
<p>Create an entirely new document, which is not connected with current one. Short research reveals that it’s possible and is super easy to use in our case.<br />
Document object provides  <a href="https://developer.mozilla.org/en-US/docs/Web/API/DOMImplementation/createHTMLDocument" target="_blank">document.implementation.createHTMLDocument()</a> method, which is intended to do just that. What’s best — creating new elements inside our entirely new and detached document isn’t recognised by a browser to load anything extra and we can traverse it with our favourite methods and then just attach it to our current document.</p>
<p>Here’s a basic code snippet showing how easy it is to deal with new document, where data is HTML string response. It just works:</p>
<pre><code>function insertPreview (data) {
    var newHTMLDocument = document.implementation.createHTMLDocument('preview');
    var el = newHTMLDocument.createElement('div').innerHTML = data;
    var $pageHTML = $(el);
    var $pageHero = $pageHTML.find('.page-section--hero');
    $('.page--next').append($pageHero);
}</code></pre>

<p>Cool, huh? What's cooler, it's supported by all modern browsers, even in IE9+.</p>

    </section>
    

    <section>
  <h3>Share the article</h3>
      <p>If you find this blog post interesting, we appreciate if you share it. Thank you.</p>
    
</section>


  
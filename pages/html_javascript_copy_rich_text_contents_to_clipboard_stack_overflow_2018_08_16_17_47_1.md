<a href="https://stackoverflow.com/questions/23934656/javascript-copy-rich-text-contents-to-clipboard">https://stackoverflow.com/questions/23934656/javascript-copy-rich-text-contents-to-clipboard</a><div id="articleHeader"><h1>javascript copy rich text contents to clipboard</h1></div>

<p>I need help copying rich text to the clipboard using JavaScript. i have searched around and haven't found anything to suit my specific need.</p>

<p><strong>My JS</strong></p>

<pre><code>function ctrlA1(corp) {
  with(corp) {
  }
  if (document.all) {
    txt = corp.createTextRange()
    txt.execCommand("Copy")
  } else
    setTimeout("window.status=''", 5000)
}</code></pre>

<p><strong>HTML</strong></p>

<pre><code>&lt;div id="sc1"&gt;hello &lt;br&gt; &lt;b&gt; world &lt;/b&gt; &lt;/div&gt;
&lt;button onclick="ctrlA1(document.getElementById('sc1') )"&gt;&lt;/button&gt;</code></pre>

<p>The above code isn't working and getting an object expected error. any help is appreciated.
I have seen a library out there called <code>zeroclipboard</code>, but would prefer to write my own function.</p>

<p><strong>EDIT</strong>
i now have this function to select text on the page. is it possible to write a formula to copy the selected range as is?</p>

<pre><code>function containerSelect(id) {
containerUnselect();
if(document.selection) {
var range = document.body.createTextRange();
range.moveToElementText(id);
range.select();
}
else if(window.getSelection) {
var range = document.createRange();
range.selectNode(id);
window.getSelection().addRange(range);
}
}

&lt;label onclick="containerSelect(this); select_all()"&gt;
&lt;p&gt;hello world&lt;/p&gt;
&lt;img src="imagepath.png"&gt;
&lt;/label&gt;</code></pre>
    
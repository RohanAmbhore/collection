<a href="https://makandracards.com/makandra/9245-use-overflow-hidden-to-avoid-floating-elements-from-wrapping-a-container-s-text">https://makandracards.com/makandra/9245-use-overflow-hidden-to-avoid-floating-elements-from-wrapping-a-container-s-text</a><div id="articleHeader"><h1>Use "overflow: hidden" to avoid floating elements from wrapping a container's text</h1></div>

<div>
<p>Consider this HTML:</p>

<pre><code>&lt;div id="container"&gt;
  &lt;div id="actions"&gt;
    &lt;a href="#"&gt;Click me!&lt;/a&gt;
  &lt;/div&gt;
  &lt;div id="content"&gt;
    Hello Universe! Hello Universe! Hello Universe! Hello Universe! Hello Universe! Hello Universe!
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>

<p>If you want the <code>actions</code> element to float on the left, you'd just say this in your CSS:</p>

<pre><code>#actions { float: left; }
</code></pre>

<p>Unfortunately, any content of the <code>content</code>'s text will wrap underneath it:</p>

<p><div class="readableLargeImageContainer"><img src="https://makandracards.com/makandra/9245-use-overflow-hidden-to-avoid-floating-elements-from-wrapping-a-container-s-text/attachments/4259" alt="paja9.png" /></div></p>

<p>If you don't want that but actually wish for longer text to stay on the same vertical boundaries, use <code>overflow: hidden</code> on the element whose content you don't want to see wrapping:</p>

<pre><code>#actions { float: left; }
#content { overflow: hidden; }
</code></pre>

<p>Now it's pretty:</p>

<p><div class="readableLargeImageContainer"><img src="https://makandracards.com/makandra/9245-use-overflow-hidden-to-avoid-floating-elements-from-wrapping-a-container-s-text/attachments/4261" alt="qx72h5.png" /></div></p>

<p>The reason behind this is that "<code>overflow: hidden</code>" will give you a new <a href="/makandra/31071" target="_blank">block formatting context</a>. You could use <a href="http://www.w3.org/TR/CSS21/visuren.html#block-formatting" target="_blank">other attributes</a> as well, but <code>overflow: hidden</code> works nicely without interfering much.</p>

<p>Follow the attached link for a (more verbose) example.</p>









<div>
<h2>
Author of this card:
</h2>


<dl>
<dt>Last edit:</dt>
<dd>
<div>over 2 years ago</div>
<div>by Henning Koch</div>
</dd>
<dt>Attachments:</dt>
<dd>
<a href="/makandra/9245-use-overflow-hidden-to-avoid-floating-elements-from-wrapping-a-container-s-text/attachments/4259" target="_blank">paja9.png</a>, <a href="/makandra/9245-use-overflow-hidden-to-avoid-floating-elements-from-wrapping-a-container-s-text/attachments/4261" target="_blank">qx72h5.png</a></dd>
<dt>Keywords:</dt>
<dd>
clear</dd>
<dt>About this deck:</dt>
<dd>
We are <a href="http://makandra.com" target="_blank">makandra</a> and do test-driven, agile Ruby on Rails software development.
</dd>
<dd><a href="/makandra/9245-use-overflow-hidden-to-avoid-floating-elements-from-wrapping-a-container-s-text" target="_blank">License for source code</a></dd>

</dl>


<div>
<div><div>
<h2>
Related cards:
</h2>
<div>

<div>
<h2><a href="/makandra/5883-use-css-text-overflow-to-truncate-long-texts" target="_blank">Use CSS "text-overflow" to truncate long texts</a></h2>
<div>
<p>When using Rails to truncate strings, you may end up with strings that are still too long for their container or are not as long as they could be. You can get a prettier result using stylesheets.</p>

<p>The CSS property <code>text-overflow: ellipsis</code> has been around for quite a long time now but since Firefox did not support it for ages, you did not use it. <a href="http://caniuse.com/text-overflow" target="_blank">Since Firefox 7 you can!</a></p>

<p><strong>Note that this only works for single-line texts.</strong> If you want to truncate tests across multiple lines, use a JavaScript solution like…</p>

</div>







<div>

<div>
<h2><a href="/makandra/1060-prevent-floating-sibling-elements-from-wrapping-in-css" target="_blank">Prevent floating sibling elements from wrapping in CSS</a></h2>
<div>
<p>When you style multiple adjacent block elements with <code>float: left</code>, they will be rendered next to each other similar to inline elements. Also like inline elements, they will wrap at the horizontal end of the parent container.</p>

<p>If you want to keep floating elements from wrapping, nest them in a really wide container:</p>

<pre><code>&lt;div class="tabs"&gt;
  &lt;div class="really_wide_container"&gt;
    &lt;div class="tab"&gt;...&lt;/div&gt;
    &lt;div class="tab"&gt;...&lt;/div&gt;
    &lt;div class="tab"&gt;...&lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>

<p>This is the [Sass](http://sass-la…</p>

</div>







<div>

<div>
<h2><a href="/makandra/48582-rspec-how-to-check-that-an-activerecord-relation-contains-exactly-these-elements" target="_blank">RSpec: How to check that an ActiveRecord relation contains exactly these elements</a></h2>
<div>
<p>To check which elements an ActiveRecord relation contains use the <code>contain_exactly</code> matcher.</p>

<pre><code>describe User do
  let!(:admin) { create(:user, role: 'admin') }
  let!(:customer) { create(:user, role: 'customer') }
  
  subject(:users) { User.where(role: 'admin') }
  
  # Recommended (The error output is most helpful)
  it { expect(users).to contain_exactly(admin) }
  
  # Other options
  it { expect(users).to eq([admin]) }
  it { expect(users.pluck(:id).to eq([admin.id]) }
end

</code></pre>

<p>In case you have an <code>ActiveRecord::AssociationRelation</code> …</p>

</div>





<div>

<div>
<h2><a href="/makandra/46962-javascript-bookmarklet-to-click-an-element-and-copy-its-text-contents" target="_blank">JavaScript bookmarklet to click an element and copy its text contents</a></h2>
<div>
<p>Here is some JavaScript code that allows you to click the screen and get the clicked element's text contents (or value, in case of inputs).</p>

<p>The approach is simple: we place an overlay so you don't really click the target element. When you click the overlay, we look up the element underneath it and show its text in a browser dialog. You can then copy it from there.</p>

<p>It will also highlight the clicked element.</p>

<p>Here is the one-liner URL that you can store as a bookmark. Place it in your bookmarks bar and click it to activate.</p>

<p>```<br />
javascript:…</p>

</div>





<div>
<div><img src="/assets/icons/arrow-circle-315-beb5ed6dc67a794211c1a361f540123c.png" alt="Repeats" /></div>
<div>
<h2><a href="/makandra/31289-how-to-create-giant-memory-leaks-in-angularjs" target="_blank">How to create giant memory leaks in AngularJS</a></h2>
<div>
<p>This guide shows how to create an AngularJS application that consumes more and more memory until, eventually, the browser process crashes on your users.</p>

<p>Although this guide has been written for Angular 1 originally, most of the advice is relevant for all client-side JavaScript code.</p>

<h1 id="how-to-observe-memory-consumption">How to observe memory consumption</h1>

<p>To inspect the amount of memory consumed by your Javascripts in Chrome:</p>

<ul>
  <li>Open an incognito window</li>
  <li>Open the page you want to inspect</li>
  <li>Press <code>Shift + ESC</code> to see a list of Chrome processes…</li>
</ul>

</div>





<div>

<div>
<h2><a href="/makandra/46228-cucumber-test-that-an-element-is-not-overshadowed-by-another-element" target="_blank">Cucumber: Test that an element is not overshadowed by another element</a></h2>
<div>
<p>I needed to make sure that an element is visible and not overshadowed by an element that has a higher <code>z-index</code> (like a modal overlay).</p>

<p>Here is the step I wanted:</p>

<pre><code>Then the very important notice should not be overshadowed by another element
</code></pre>

<p>This is the step definition:</p>

<p>```<br />
Then(/^(.*?) should not be overshadowed by another element$/) do |locator|<br />
  selector = selector_for(locator)<br />
  expect(page).to have_css(selector)<br />
  js = «-JS<br />
    var selector = #{selector.to_json};<br />
    var elementFromSelector = document.querySelector(selector)…</p>

</div>
















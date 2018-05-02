<a href="https://learn.jquery.com/plugins/basic-plugin-creation/">https://learn.jquery.com/plugins/basic-plugin-creation/</a><div id="articleHeader"><h1>How to Create a Basic Plugin</h1></div>

	
		<p>Sometimes you want to make a piece of functionality available throughout your code. For example, perhaps you want a single method you can call on a jQuery selection that performs a series of operations on the selection. In this case, you may want to write a plugin.</p>
<h2><a href="#how-jquery-works-101-jquery-object-methods" id="how-jquery-works-101-jquery-object-methods" target="_blank">link</a> How jQuery Works 101: jQuery Object Methods</h2><p>Before we write our own plugins, we must first understand a little about how jQuery works. Take a look at this code:</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>$( "a" ).css( "color", "red" );</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<p>This is some pretty basic jQuery code, but do you know what's happening behind the scenes? Whenever you use the <code>$</code> function to select elements, it returns a jQuery object. This object contains all of the methods you've been using (<code>.css()</code>, <code>.click()</code>, etc.) and all of the elements that fit your selector. The jQuery object gets these methods from the <code>$.fn</code> object. This object contains all of the jQuery object methods, and if we want to write our own methods, it will need to contain those as well.</p>
<h2><a href="#basic-plugin-authoring" id="basic-plugin-authoring" target="_blank">link</a> Basic Plugin Authoring</h2><p>Let's say we want to create a plugin that makes text within a set of retrieved elements green. All we have to do is add a function called <code>greenify</code> to <code>$.fn</code> and it will be available just like any other jQuery object method.</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
						
					
						
					
						
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>$.fn.greenify = function() {</code></div></div><div><div><code>    this.css( "color", "green" );</code></div></div><div><div><code>};</code></div></div><div><div><code>$( "a" ).greenify(); // Makes all the links green.</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<p>Notice that to use <code>.css()</code>, another method, we use <code>this</code>, not <code>$( this )</code>. This is because our <code>greenify</code> function is a part of the same object as <code>.css()</code>.</p>
<h2><a href="#chaining" id="chaining" target="_blank">link</a> Chaining</h2><p>This works, but there are a couple of things we need to do for our plugin to survive in the real world. One of jQuery's features is chaining, when you link five or six actions onto one selector. This is accomplished by having all jQuery object methods return the original jQuery object again (there are a few exceptions: <code>.width()</code> called without parameters returns the width of the selected element, and is not chainable). Making our plugin method chainable takes one line of code:</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
						
					
						
					
						
					
						
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>$.fn.greenify = function() {</code></div></div><div><div><code>    this.css( "color", "green" );</code></div></div><div><div><code>    return this;</code></div></div><div><div><code>}</code></div></div><div><div><code>$( "a" ).greenify().addClass( "greenified" );</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<h2><a href="#protecting-the-alias-and-adding-scope" id="protecting-the-alias-and-adding-scope" target="_blank">link</a> Protecting the $ Alias and Adding Scope</h2><p>The <code>$</code> variable is very popular among JavaScript libraries, and if you're using another library with jQuery, you will have to make jQuery not use the <code>$</code> with <code>jQuery.noConflict()</code>. However, this will break our plugin since it is written with the assumption that <code>$</code> is an alias to the <code>jQuery</code> function. To work well with other plugins, <em>and</em> still use the jQuery <code>$</code> alias, we need to put all of our code inside of an <a href="http://benalman.com/news/2010/11/immediately-invoked-function-expression/" target="_blank">Immediately Invoked Function Expression</a>, and then pass the function <code>jQuery</code>, and name the parameter <code>$</code>:</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>(function ( $ ) {</code></div></div><div><div><code>    $.fn.greenify = function() {</code></div></div><div><div><code>        this.css( "color", "green" );</code></div></div><div><div><code>        return this;</code></div></div><div><div><code>    };</code></div></div><div><div><code>}( jQuery ));</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<p>In addition, the primary purpose of an Immediately Invoked Function is to allow us to have our own private variables. Pretend we want a different color green, and we want to store it in a variable.</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>(function ( $ ) {</code></div></div><div><div><code>    var shade = "#556b2f";</code></div></div><div><div><code>    $.fn.greenify = function() {</code></div></div><div><div><code>        this.css( "color", shade );</code></div></div><div><div><code>        return this;</code></div></div><div><div><code>    };</code></div></div><div><div><code>}( jQuery ));</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<h2><a href="#minimizing-plugin-footprint" id="minimizing-plugin-footprint" target="_blank">link</a> Minimizing Plugin Footprint</h2><p>It's good practice when writing plugins to only take up one slot within <code>$.fn</code>. This reduces both the chance that your plugin will be overridden, and the chance that your plugin will override other plugins. In other words, this is bad:</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>(function( $ ) {</code></div></div><div><div><code>    $.fn.openPopup = function() {</code></div></div><div><div><code>        // Open popup code.</code></div></div><div><div><code>    };</code></div></div><div><div><code>    $.fn.closePopup = function() {</code></div></div><div><div><code>        // Close popup code.</code></div></div><div><div><code>    };</code></div></div><div><div><code>}( jQuery ));</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<p>It would be much better to have one slot, and use parameters to control what action that one slot performs.</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>(function( $ ) {</code></div></div><div><div><code>    $.fn.popup = function( action ) {</code></div></div><div><div><code>        if ( action === "open") {</code></div></div><div><div><code>            // Open popup code.</code></div></div><div><div><code>        }</code></div></div><div><div><code>        if ( action === "close" ) {</code></div></div><div><div><code>            // Close popup code.</code></div></div><div><div><code>        }</code></div></div><div><div><code>    };</code></div></div><div><div><code>}( jQuery ));</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<h2><a href="#using-the-each-method" id="using-the-each-method" target="_blank">link</a> Using the <code>each()</code> Method</h2><p>Your typical jQuery object will contain references to any number of DOM elements, and that's why jQuery objects are often referred to as collections. If you want to do any manipulating with specific elements (e.g. getting a data attribute, calculating specific positions) then you need to use <code>.each()</code> to loop through the elements.</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>$.fn.myNewPlugin = function() {</code></div></div><div><div><code>    return this.each(function() {</code></div></div><div><div><code>        // Do something to each element here.</code></div></div><div><div><code>    });</code></div></div><div><div><code>};</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<p>Notice that we return the results of <code>.each()</code> instead of returning <code>this</code>. Since <code>.each()</code> is already chainable, it returns <code>this</code>, which we then return. This is a better way to maintain chainability than what we've been doing so far.</p>
<h2><a href="#accepting-options" id="accepting-options" target="_blank">link</a> Accepting Options</h2><p>As your plugins get more and more complex, it's a good idea to make your plugin customizable by accepting options. The easiest way to do this, especially if there are lots of options, is with an object literal. Let's change our greenify plugin to accept some options.</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>(function ( $ ) {</code></div></div><div><div><code>    $.fn.greenify = function( options ) {</code></div></div><div><div><code>        // This is the easiest way to have default options.</code></div></div><div><div><code>        var settings = $.extend({</code></div></div><div><div><code>            // These are the defaults.</code></div></div><div><div><code>            color: "#556b2f",</code></div></div><div><div><code>            backgroundColor: "white"</code></div></div><div><div><code>        }, options );</code></div></div><div><div><code>        // Greenify the collection based on the settings variable.</code></div></div><div><div><code>        return this.css({</code></div></div><div><div><code>            color: settings.color,</code></div></div><div><div><code>            backgroundColor: settings.backgroundColor</code></div></div><div><div><code>        });</code></div></div><div><div><code>    };</code></div></div><div><div><code>}( jQuery ));</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<p>Example usage:</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
						
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>$( "div" ).greenify({</code></div></div><div><div><code>    color: "orange"</code></div></div><div><div><code>});</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<p>The default value for <code>color</code> of <code>#556b2f</code> gets overridden by <code>$.extend()</code> to be orange.</p>
<h2><a href="#putting-it-together" id="putting-it-together" target="_blank">link</a> Putting It Together</h2><p>Here's an example of a small plugin using some of the techniques we've discussed:</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>(function( $ ) {</code></div></div><div><div><code>    $.fn.showLinkLocation = function() {</code></div></div><div><div><code>        this.filter( "a" ).each(function() {</code></div></div><div><div><code>            var link = $( this );</code></div></div><div><div><code>            link.append( " (" + link.attr( "href" ) + ")" );</code></div></div><div><div><code>        });</code></div></div><div><div><code>        return this;</code></div></div><div><div><code>    };</code></div></div><div><div><code>}( jQuery ));</code></div></div><div><div><code>// Usage example:</code></div></div><div><div><code>$( "a" ).showLinkLocation();</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<p>This handy plugin goes through all anchors in the collection and appends the <code>href</code> attribute in parentheses.</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
						
					
						
					
						
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>&lt;!-- Before plugin is called: --&gt;</code></div></div><div><div><code>&lt;a href="page.html"&gt;Foo&lt;/a&gt;</code></div></div><div><div><code>&lt;!-- After plugin is called: --&gt;</code></div></div><div><div><code>&lt;a href="page.html"&gt;Foo (page.html)&lt;/a&gt;</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<p>Our plugin can be optimized though:</p>
<div>
	<table>
		<tbody>
			<tr>
				
				<td>
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
						
					
				</td>
				
				<td>
					<pre><div><div><code>(function( $ ) {</code></div></div><div><div><code>    $.fn.showLinkLocation = function() {</code></div></div><div><div><code>        this.filter( "a" ).append(function() {</code></div></div><div><div><code>            return " (" + this.href + ")";</code></div></div><div><div><code>        });</code></div></div><div><div><code>        return this;</code></div></div><div><div><code>    };</code></div></div><div><div><code>}( jQuery ));</code></div></div></pre>
				</td>
			</tr>
		</tbody>
	</table>
</div>
<p>We're using the <code>.append()</code> method's capability to accept a callback, and the return value of that callback will determine what is appended to each element in the collection. Notice also that we're not using the <code>.attr()</code> method to retrieve the <code>href</code> attribute, because the native DOM API gives us easy access with the aptly named <code>href</code> property.</p>					
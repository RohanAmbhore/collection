<a href="http://tutsplus.github.io/syntax-highlighter-demos/prism_okaidia.html">http://tutsplus.github.io/syntax-highlighter-demos/prism_okaidia.html</a><div id="articleHeader"><h1> Prism Demo - Okaidia Theme</h1></div>
        <p>Website: <a href="http://prismjs.com/" target="_blank">http://prismjs.com/</a></p>
        
        <pre><code> 
&lt;header&gt;
&lt;h1&gt;Example HTML&lt;/h1&gt;
&lt;/header&gt;
&lt;main class="style"&gt;
&lt;p&gt;Some text&lt;/p&gt;
&lt;/main&gt;</code></pre>
        <h2>JavaScript</h2>
        <pre><code>var example = true;

function foo(arg) {
	console.log( "do", arg);
	arg = example ? true : false;
	return arg;
}</code></pre>
        
        <pre><code>@import "somestyle.css"

body {
	background: white;
}

.wrapper {
	background: #F88;
	color: #454545;
}

.box::after {
	content: "...";
}</code></pre>
        
        <pre><code>&lt;?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?&gt;
&lt;article&gt;
&lt;h1&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
&lt;?php the_content(); ?&gt;
&lt;/article&gt;
&lt;?php endwhile; endif; ?&gt;</code></pre>
        <h2>Markdown</h2>
        <pre><code># Example Markdown

Some text with *emphasis*

* list
* list
* list

Some text with a [link](http://tutsplus.com)</code></pre>
        <h2>CoffeeScript</h2>
        <pre><code># Objects:
math =
  root:   Math.sqrt
  square: square
  cube:   (x) -&gt; x * square x

# Splats:
race = (winner, runners...) -&gt;
  print winner, runners

# Existence:
alert "I knew it!" if elvis?

# Array comprehensions:
cubes = (math.cube num for num in list)</code></pre>
        <h2>Handlebars</h2>
        <pre><code>&lt;header&gt;
&lt;h1&gt;{{title}}&lt;/h1&gt;
&lt;/header&gt;
&lt;main class="style"&gt;
{{content}}
&lt;/main&gt;</code></pre>
        
        <pre><code>- var title = "Example Jade";
header
	h1 #{title}
main.style
	p Some text</code></pre>
        
        <pre><code>@body_background: white;
@wrapper_background: #F88;
@wrapper_color: #454545;

body {
	background: @body_background;
}

.wrapper {
	background: @wrapper_background;
	color: @wrapper_color;
}

.box::after {
	content: "...";
}</code></pre>
        
        <pre><code>$body_background: white;
$wrapper_background: #F88;
$wrapper_color: #454545;

body {
	background: $body_background;
}

.wrapper {
	background: $wrapper_background;
	color: $wrapper_color;
}

.box::after {
	content: "...";
}</code></pre>
        <h2>Stylus</h2>
        <pre><code>$body_background = white
$wrapper_background = #F88
$wrapper_color = #454545

body
	background: $body_background

.wrapper
	background: $wrapper_background
	color: $wrapper_color

.box::after
	content: "..."</code></pre>
      
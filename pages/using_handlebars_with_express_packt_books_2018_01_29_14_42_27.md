<a href="https://www.packtpub.com/books/content/using-handlebars-express">https://www.packtpub.com/books/content/using-handlebars-express</a><div id="articleHeader"><h1>Templates</h1></div>
<p><strong>Templates</strong> come in many shapes or forms. Traditionally, they are non-executable files with some pre-formatted text, used as the basis of a bazillion documents that can be generated with a computer program. I worked on a project where I had to write a program that would take a Microsoft Word template, containing parameters like <em>$first</em>, <em>$name</em>, <em>$phone</em>, and so on, and generate a specific Word document for every student in a school.</p>
<p><strong>Web templating</strong> does something very similar. It uses a <strong>templating processor</strong> that takes data from a source of information, typically a database and a template, a generic HTML file with some kind of parameters inside. The processor then merges the data and template to generate a bunch of static web pages or dynamically generates HTML on the fly.</p>
<p>If you have been using <a href="https://www.packtpub.com/tech/PHP" target="_blank">PHP</a> to create dynamic webpages, you will have been busy with web templating. Why? Because you have been inserting PHP code inside HTML files in between the <em>&lt;?php</em> and <em>?&gt;</em> strings. Your templating processor was the Apache web server that has many additional roles. By the time your browser gets to see the result of your code, it is pure HTML. This makes this an example of <em>server side templating</em>. You could also use <strong>Ajax</strong> and PHP to transfer data in the <strong>JSON</strong> format and then have the browser process that data using <a href="https://www.packtpub.com/tech/JavaScript" target="_blank">JavaScript</a> to create the HTML you need. Combine this with using templates and you will have <em>client side templating</em>.</p>
<h2>Node.js</h2>
<p>What <em>Le Sacre du Printemps</em> by Stravinsky did to the world of classical music, <a href="https://www.packtpub.com/tech/Nodejs" target="_blank">Node.js</a> may have done to the world of web development. At its introduction, it shocked the world. By now, Node.js is considered by many as the coolest thing. Just like <em>Le Sacre</em> is a totally different kind of music—but by now every child who has seen <em>Fantasia</em> has heard it—Node.js is a different way of doing web development. Rather than writing an application and using a web server to soup up your code to a browser, the application and the web server are <em>one and the same</em>.</p>
<p>This may sound scary, but you should not worry as there is an entire community that developed <em>modules</em> you can obtain using the <em>npm</em> tool. Before showing you an example, I need to point out an extremely important feature of Node.js: the language in which you will write your web server and application is <strong>JavaScript</strong>. So Node.js gives you server side JavaScript.</p>
<h3>Installing Node.js</h3>
<p>How to install Node.js will be different, depending on your OS, but the result is the same everywhere. It gives you two programs: <em>Node</em> and <em>npm</em>.</p>

<p>The <strong>node packaging manager</strong> (<strong>npm</strong>)is the tool that you use to look for and install modules. Each time you write code that needs a module, you will have to add a line like this in:</p>
<pre>var module = require('module');</pre><p>The module will have to be installed first, or the code will fail. This is how it is done:</p>
<pre><strong>npm install module </strong></pre>
<pre><strong>npm -g install module </strong></pre><p>The latter will attempt to install the module globally, the former, in the directory where the command is issued. It will typically install the module in a folder called <em>node_modules</em>.</p>

<p>The <em>node</em> program is the command to use to start your Node.js program, for example:</p>
<pre><strong>node myprogram.js</strong></pre><p><em>node</em> will start and interpret your code. Type <em>Ctrl</em>-<em>C</em> to stop node. Now create a file <em>myprogram.js</em> containing the following text:</p>
<pre>var http = require('http');<br />http.createServer(function (req, res) {<br />res.writeHead(200, {'Content-Type': 'text/plain'});<br />res.end('Hello World\n');<br />}).listen(8080, 'localhost');<br />console.log('Server running at http://localhost:8080');</pre><p>So, if you installed Node.js and the required <em>http</em> module, typing node <em>myprogram.js</em> in a terminal window, your console will start up a web server. And, when you type <em>http://localhost:8080</em> in a browser, you will see the world famous two word program example on your screen. This is the equivalent of getting the It works! thing, after testing your Apache web server installation.</p>
<p>As a matter of fact, if you go to <em>http://localhost:8080/it/does/not/matterwhat</em>, the same will appear. Not very useful maybe, but it is a web server.</p>
<h3>Serving up static content</h3>
<p>This does not work in a way we are used to. URLs typically point to a file (or a folder, in which case the server looks for an <em>index.html</em> file) , <em>foo.html</em>, or <em>bar.php</em>, and when present, it is served up to the client.</p>
<p>So what if we want to do this with Node.js? We will need a module. Several exist to do the job. We will use <em>node-static</em> in our example. But first we need to install it:</p>
<pre><strong>npm install node-static</strong></pre><p>In our app, we will now create not only a web server, but a fileserver as well. It will serve all the files in the local directory <em>public</em>. It is good to have all the so called static content together in a separate folder. These are basically all the files that will be served up to and interpreted by the client. As we will now end up with a mix of client code and server code, it is a good practice to separate them.</p>
<p>When you use the <strong>Express</strong> framework, you have an option to have Express create these things for you. So, here is a second, more complete, Node.js example, including all its static content.</p>
<h3>hello.js, our node.js app</h3>
<pre>var http = require('http');<br />var static = require('node-static');<br />var fileServer = new static.Server('./public');<br />http.createServer(function (req, res) {<br />fileServer.serve(req,res);<br />}).listen(8080, 'localhost');<br />console.log('Server running at http://localhost:8080');</pre><p><strong>hello.html</strong> is stored in <em>./public</em>.</p>
<pre>&lt;!DOCTYPE html&gt;<br />&lt;html&gt;<br />&lt;head&gt;<br />&lt;meta charset="UTF-8" /&gt;<br />&lt;title&gt;Hello world document&lt;/title&gt;<br />&lt;link href="./styles/hello.css" rel="stylesheet"&gt;<br />&lt;/head&gt;<br />&lt;body&gt;<br />&lt;h1&gt;Hello, World&lt;/h1&gt;<br />&lt;/body&gt;<br />&lt;/html&gt;</pre><p><strong>hello.css</strong> is stored in <em>public/styles</em>.</p>
<pre>body {<br />background-color:#FFDEAD;<br />}<br />h1<br />{<br />color:teal;<br />margin-left:30px;<br />}<br />.bigbutton {<br />height:40px;<br />color: white;<br />background-color:teal;<br />margin-left:150px;<br />margin-top:50px;<br />padding:15 15 25 15;<br />font-size:18px;<br />}</pre><p>So, if we now visit <em>http://localhost:8080/hello</em>, we will see our, by now too familiar, <em>Hello World</em> message with some basic styling, proving that our file server also delivered the CSS file.</p>
<p>You can easily take it one step further and add <a href="https://www.packtpub.com/tech/JavaScript" target="_blank">JavaScript</a> and the <a href="https://www.packtpub.com/tech/jQuery" target="_blank">jQuery</a> library and put it in, for example, <em>public/js/hello.js</em> and <em>public/js/jquery.js</em> respectively.</p>
<h3>Too many notes</h3>
<p>With Node.js, you only install the modules that you need, so it does not include the kitchen sink by default! You will benefit from that for as far as performance goes.</p>
<p>Back in California, I have been a proud product manager of a PC UNIX product, and one of our coolest value-add was a tool, called <em>kconfig</em>, that would allow people to customize what would be inside the UNIX kernel, so that it would only contain what was needed. This is what Node.js reminds me of. And it is written in C, as was UNIX. <em>Deja vu</em>.</p>
<p>However, if we wanted our Node.js web server to do everything the Apache Web Server does, we would need a lot of modules. Our application code needs to be added to that as well. That means a lot of modules. Like the critics in the movie <em>Amadeus</em> said: <em>Too many notes</em>.</p>
<h1>Express 4</h1>
<p>A good way to get the job done with fewer notes is by using the <strong>Express</strong> framework. On the expressjs.com website, it is called a <em>minimal and flexible Node.js web application framework, providing a robust set of features for building web applications</em>.</p>
<p>This is a good way to describe what Express can do for you. It is minimal, so there is little overhead for the framework itself. It is flexible, so you can add just what you need. It gives a robust set of features, which means you do not have to create them yourselves, and they have been tested by an ever growing community.</p>
<p>But we need to get back to templating, so all we are going to do here is explain how to get Express, and give one example.</p>
<h2>Installing Express</h2>
<p>As Express is also a node module, we install it as such. In your project directory for your application, type:</p>
<pre><strong>npm install express</strong></pre><p>You will notice that a folder called <em>express</em> has been created inside <em>node_modules</em>, and inside that one, there is another collection of node-modules. These are examples of what is called <strong>middleware</strong>.</p>
<p>In the code example that follows, we assume <em>app.js</em> as the name of our JavaScript file, and app for the variable that you will use in that file for your instance of Express. This is for the sake of brevity. It would be better to use a string that matches your project name.</p>
<p>We will now use Express to rewrite the <em>hello.js</em> example. All static resources in the public directory can remain untouched. The only change is in the node app itself:</p>
<pre>var express = require('express');<br />var path = require('path');<br />var app = express();<br />app.set('port', process.env.PORT || 3000);<br />var options = {<br />dotfiles: 'ignore',<br />extensions: ['htm', 'html'],<br />index: false<br />};<br />app.use(express.static(path.join(__dirname, 'public') ,<br />options ));<br />app.listen(app.get('port'), function () {<br />console.log('Hello express started on http://localhost:' +<br />app.get('port') + '; press Ctrl-C to terminate.' );<br />});</pre><p>This code uses so called middleware (<em>static</em>) that is included with express. There is a lot more available from third parties.</p>
<p>Well, compared to our node.js example, it is about the same number of lines. But it looks a lot cleaner and it does more for us. You no longer need to explicitly include the HTTP module and other such things.</p>
<h1>Templating and Express</h1>
<p>We need to get back to templating now. Imagine all the JavaScript ecosystem we just described. Yes, we could still put our client JavaScript code in between the <em>&lt;script&gt;</em> tags but what about the server JavaScript code? There is no such thing as <em>&lt;?javascript ?&gt;</em> !</p>
<p>Node.js and Express, support several templating languages that allow you to separate layout and content, and which have the template system do the work of fetching the content and injecting it into the HTML.</p>
<p>The default templating processor for Express appears to be <strong>Jade</strong>, which uses its own, albeit more compact than HTML, language. Unfortunately, that would mean that you have to learn yet another syntax to produce something.</p>
<p>We propose to use <strong>handlebars.js</strong>. There are two reasons why we have chosen <em>handlebars.js</em>:</p>
<ul>
<li>It uses <em>&lt;html&gt;</em> as the language</li>
<li>It is available on both the client and server side</li>
</ul>
<h2>Getting the handlebars module for Express</h2>
<p>Several Express modules exist for handlebars. We happen to like the one with the surprising name <em>express-handlebars</em>. So, we install it, as follows:</p>
<pre><strong>npm install express-handlebars</strong></pre><h2>Layouts</h2>
<p>I almost called this section <em>templating without templates</em> as our first example will not use a parameter inside the templates. Most websites will consist of several pages, either static or dynamically generated ones. All these pages usually have common parts; a header and footer part, a navigation part or menu, and so on. This is the layout of our site. What distinguishes one page from another, usually, is some part in the body of the page where the home page has different information than the other pages. With <em>express-handlebars</em>, you can separate layout and content. We will start with a very simple example.</p>
<p>Inside your project folder that contains <em>public</em>, create a folder, <em>views</em>, with a subdirectory layout. Inside the <em>layouts</em> subfolder, create a file called <em>main.handlebars</em>. This is your default layout. Building on top of the previous example, have it say:</p>
<pre>&lt;!doctype html&gt;<br />&lt;html&gt;<br />&lt;head&gt;<br />&lt;title&gt;Handlebars demo&lt;/title&gt; &lt;/head&gt;<br />&lt;link href="./styles/hello.css" rel="stylesheet"&gt;<br />&lt;body&gt;<br />{{{body}}}<br />&lt;/body&gt;<br />&lt;/html&gt;</pre><p>Notice the <em>{{{body}}}</em> part. This token will be replaced by HTML. Handlebars escapes HTML. If we want our HTML to stay intact, we use <em>{{{</em> <em>}}}</em>, instead of <em>{{</em> <em>}}</em>. Body is a reserved word for handlebars.</p>
<p>Create, in the folder <em>views</em>, a file called <em>hello.handlebars</em> with the following content. This will be one (of many) example of the HTML <em>{{{body}}}</em>, which will be replaced by:</p>
<pre>&lt;h1&gt;Hello, World&lt;/h1&gt;</pre><p>Let’s create a few more <em>june.handlebars</em> with:</p>
<pre>&lt;h1&gt;Hello, June Lake&lt;/h1&gt;</pre><p>And <em>bodie.handlebars</em> containing:</p>
<pre>&lt;h1&gt;Hello, Bodie&lt;/h1&gt;</pre><h3>Our first handlebars example</h3>
<p>Now, create a file, <em>handlehello.js</em>, in the project folder. For convenience, we will keep the relevant code of the previous Express example:</p>
<pre>var express = require('express');<br />var path = require('path');<br />var app = express();<br />var exphbs = require(‘express-handlebars’); app.engine('handlebars', <br />exphbs({defaultLayout: 'main'})); app.set('view engine', 'handlebars');<br />app.set('port', process.env.PORT || 3000);<br />var options = { dotfiles: 'ignore', etag: false,<br />extensions: ['htm', 'html'],<br />index: false<br />};<br />app.use(express.static(path.join(__dirname, 'public') , options  ));<br />app.get('/', function(req, res)<br />{<br />res.render('hello');   // this is the important part<br />});<br />app.get('/bodie', function(req, res)<br />{<br />res.render('bodie');<br />});<br />app.get('/june', function(req, res)<br />{<br />res.render('june');<br />});<br />app.listen(app.get('port'),  function () {<br />console.log('Hello express started on http://localhost:' +<br />app.get('port') + '; press Ctrl-C to terminate.' );<br />});</pre><p>Everything that worked before still works, but if you type <em>http://localhost:3000/</em>, you will see a page with the layout from <em>main.handlebars</em> and <em>{{{body}}}</em> replaced by, you guessed it, the same <em>Hello World</em> with basic markup that looks the same as our <em>hello.html</em> example.</p>
<p>Let’s look at the new code. First, of course, we need to add a require statement for our <em>express-handlebars</em> module, giving us an instance of express-handlebars. The next two lines specify what the <em>view</em> engine is for this app and what the extension is that is used for the templates and layouts. We pass one option to express-handlebars, <em>defaultLayout</em>, setting the default layout to be main. This way, we could have different versions of our app with different layouts, for example, one using <a href="https://www.packtpub.com/tech/Bootstrap" target="_blank">Bootstrap</a> and another using <strong>Foundation</strong>.</p>
<p>The <em>res.render</em> calls determine which <em>views</em> need to be rendered, so if you type <em>http:// localhost:3000/june</em>, you will get <em>Hello, June Lake</em>, rather than Hello World. But this is not at all useful, as in this implementation, you still have a separate file for each Hello flavor. Let’s create a true template instead.</p>
<h3>Templates</h3>
<p>In the views folder, create a file, <em>town.handlebars</em>, with the following content:</p>
<pre>{{!-- Our first template with tokens --}}<br />&lt;h1&gt;Hello, {{town}} &lt;/h1&gt;</pre><p>Please note the comment line. This is the syntax for a handlebars comment. You could HTML comments as well, of course, but the advantage of using handlebars comments is that it will not show up in the final output.</p>
<p>Next, add this to your JavaScript file:</p>
<pre>app.get('/lee', function(req, res)<br />{<br />res.render('town', { town: "Lee Vining"});<br />});</pre><p>Now, we have a template that we can use over and over again with different context, in this example, a different town name. All you have to do is pass a different second argument to the <em>res.render</em> call, and <em>{{town}}</em> in the template, will be replaced by the value of <em>town</em> in the object. In general, what is passed as the second argument is referred to as the <em>context</em>.</p>
<h3>Helpers</h3>
<p>The token can also be replaced by the output of a function. After all, this is JavaScript. In the context of handlebars, we call those <strong>helpers</strong>. You can write your own, or use some of the cool built-in ones, such as <em>#if</em> and <em>#each</em>.</p>
<h4>#if/else</h4>
<p>Let us update <em>town.handlebars</em> as follows:</p>
<pre>{{#if town}}<br />&lt;h1&gt;Hello, {{town}} &lt;/h1&gt;<br />{{else}}<br />&lt;h1&gt;Hello, World &lt;/h1&gt;<br />{{/if}}</pre><p>This should be self explanatory. If the variable town has a value, use it, if not, then show the world. Note that what comes after <em>#if</em> can only be something that is either true of false, zero or not. The helper does not support a construct such as <em>#if x &lt; y</em>.</p>
<h4>#each</h4>
<p>A very useful built-in helper is <em>#each</em>, which allows you to walk through an array of things and generate HTML accordingly. This is an example of the code that could be inside your app and the template you could use in your <em>view</em> folder:</p>
<h4>app.js code snippet</h4>
<pre>var californiapeople = {<br />   people: [<br />{“name":"Adams","first":"Ansel","profession":"photographer",<br />   "born"       :"SanFrancisco"},<br />{“name":"Muir","first":"John","profession":"naturalist",<br />   "born":"Scotland"},<br />{“name":"Schwarzenegger","first":"Arnold",<br />   "profession":"governator","born":"Germany"},<br />{“name":"Wellens","first":"Paul","profession":"author",<br />   "born":"Belgium"}<br />]   };<br />app.get('/californiapeople', function(req, res)<br />{<br />res.render('californiapeople', californiapeople);<br />});</pre><h4>template (californiapeople.handlebars)</h4>
<pre>&lt;table class=“cooltable”&gt;<br />{{#each people}}<br />   &lt;tr&gt;&lt;td&gt;{{first}}&lt;/td&gt;&lt;td&gt;{{name}}&lt;/td&gt;<br />   &lt;td&gt;{{profession}}&lt;/td&gt;&lt;/tr&gt;<br />{{/each}}<br />&lt;/table&gt;</pre><p>Now we are well on our way to do some true templating. You can also write your own helpers, which is beyond the scope of an introductory article. However, before we leave you, there is one cool feature of handlebars you need to know about: <strong>partials</strong>.</p>
<h4>Partials</h4>
<p>In web development, where you dynamically generate HTML to be part of a web page, it is often the case that you repetitively need to do the same thing, albeit on a different page.</p>
<p>There is a cool feature in express-handlebars that allows you to do that very same thing: partials. Partials are templates you can refer to inside a template, using a special syntax and drastically shortening your code that way. The partials are stored in a separate folder. By default, that would be views/partials, but you can even use subfolders.</p>
<p>Let's redo the previous example but with a partial. So, our template is going to be extremely petite:</p>
<pre>{{!-- people.handlebars inside views  --}}<br />   {{&gt; peoplepartial }}</pre><p>Notice the <em>&gt;</em> sign; this is what indicates a <em>partial</em>. Now, here is the familiar looking <em>partial</em> template:</p>
<pre>{{!-- peoplepartialhandlebars inside views/partials --}}<br />&lt;h1&gt;Famous California people &lt;/h1&gt;<br />&lt;table&gt;<br />{{#each people}}<br />&lt;tr&gt;&lt;td&gt;{{first}}&lt;/td&gt;&lt;td&gt;{{name}}&lt;/td&gt;<br />&lt;td&gt;{{profession}}&lt;/td&gt;&lt;/tr&gt;<br />{{/each}}<br />&lt;/table&gt;</pre><p>And, following is the JavaScript code that triggers it:</p>
<pre>app.get('/people', function(req, res)<br />{<br />res.render('people', californiapeople);<br />});</pre><p>So, we give it the same context but the view that is rendered is ridiculously simplistic, as there is a partial underneath that will take care of everything. Of course, these were all examples to demonstrate how handlebars and Express can work together really well, nothing more than that.</p>
<h1>Summary</h1>
<p>In this article, we talked about using templates in web development. Then, we zoomed in on using Node.js and Express, and introduced Handlebars.js. Handlebars.js is cool, as it lets you separate logic from layout and you can use it server-side (which is where we focused on), as well as client-side. Moreover, you will still be able to use HTML for your views and layouts, unlike with other templating processors.</p>
<p>For those of you new to Node.js, I compared it to what <em>Le Sacre du Printemps</em> was to music. To all of you, I recommend the recording by the <em>Los Angeles Philharmonic and Esa-Pekka Salonen</em>. I had season tickets for this guy and went to his inaugural concert with Mahler’s third symphony.</p>
<p>PHP had not been written yet, but this particular performance I had heard on the radio while on the road in California, and it was magnificent. Check it out. And, also check out Express and handlebars.</p>
<h2>Resources for Article:</h2>
<hr />
<p><strong>Further resources on this subject:</strong></p>

<hr />
                                                                    
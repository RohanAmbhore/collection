<a href="https://javascriptreport.com/the-ultimate-guide-to-javascript-frameworks/">https://javascriptreport.com/the-ultimate-guide-to-javascript-frameworks/</a><div id="articleHeader"><h1>The Ultimate Guide to JavaScript Frameworks</h1></div>
						<div>
							 <a href="/author/john/" target="_blank">John Hannah</a> <time>January 16, 2018</time>
						</div>
						<a href="#" target="_blank">Scroll Down</a>
					
				
			</header>
			
				
					<p><strong>Updated Jan. 21st, 2018:</strong> Added AppRun and dva.</p>
<p>Keeping up with JavaScript frameworks can be a challenge. There are a lot of them, and seemingly another one every month. How do you know which ones might be right for your project? What are their strengths and weaknesses? How do you get started?</p>
<p>That’s where this guide comes in. It’s a living document that is a reference for all known front end JavaScript frameworks (archived or deprecated projects are not included). In this case, the term “frameworks” is being used in a broad sense. It includes user interface (UI) libraries like React, as well as full frameworks like Angular.</p>
<h3 id="whyisthisuseful">Why Is This Useful?</h3>
<p>Some of you may be wondering why a guide like this is useful. Most readers will end up using one of the frameworks I call the "Big Three" — React, Angular and Vue. That's OK. They're great choices. That said, a guide like this has value. Here's an example...</p>
<p>Perhaps you've heard of the <a href="#dojo" target="_blank">Dojo</a> framework. Probably not, though. Dojo focuses on a couple of things that make it unique — accessibility and internationalization. All Dojo widgets are accessible by default and it provides everything needed to internationalize an application.</p>
<p>Another example...maybe you're making an app that needs excellent performance on mobile networks. There are a number of very good, high performance libraries and frameworks listed below that may just fit the bill.</p>
<p>There are also small frameworks that provide a fantastic opportunity for learning. You can dig into the code and find out for yourself how one goes about building this kind of software. <a href="#picodom" target="_blank">Picodom</a> is a library that you can use to <em>build your own framework</em>. Very cool, right?</p>
<h3 id="howthisguideisorganized">How This Guide Is Organized</h3>
<p>The frameworks are broken up into broad categories — you’ll see that in the listing tables below. To the extent possible, each framework will have a section that explains the rationale for the framework, it's pros and cons and some additional learning resources.</p>
<p>If you are a framework author — or a fan of one — and you don’t see your framework listed, or wish to correct some information, <a href="https://twitter.com/__jhannah" target="_blank">reach out to me</a> on Twitter. I’ll be happy to add or update the listing.</p>
<h3 id="guidetoicons">Guide to icons:</h3>
<p>The icons below are meant to help readers understand general framework characteristics and tendencies. They are only rough guides.</p>
<p>🔥 Performance: A top five performer in <a href="https://rawgit.com/krausest/js-framework-benchmark/master/webdriver-ts-results/table.html" target="_blank">benchmarks</a><br />
<img src="https://javascriptreport.com/content/images/2018/01/functional.svg" width="16" height="16" /> Functional programming paradigm<br />
<img src="https://javascriptreport.com/content/images/2018/01/reactive.svg" width="16" height="16" /> Reactive programming paradigm<br />
<img src="https://javascriptreport.com/content/images/2018/01/oop.svg" width="16" height="16" /> Object-oriented programming paradigm<br />
<img src="https://javascriptreport.com/content/images/2018/01/typescript.svg" width="16" height="16" /> TypeScript as primary devlopment language</p>
<h3><a href="#big3" target="_blank">The Big Three</a></h3>

<h3><a href="#legacy" target="_blank">Historically Significant</a></h3>

<h3><a href="#notable" target="_blank">Notable</a></h3>

<h3><a href="#rest" target="_blank">Rest of the Pack</a></h3>


<h2 id="thebigthree">The Big Three</h2>
<p>The three frameworks that currently dominate in popularity and usage are React, Angular and Vue. They each have large communities and lots of training resources available. If you’re a new developer learning a framework to help you get a job, these three are your best bets. Here's a look at their npm downloads over the last six months:</p>
<p><a href="https://images.contentful.com/f42iyx0drm0u/2PuqVJe5AAqUCEmaMIGACA/54a1940e62057dacfddf5fa14eecf023/react-angular-vue-jan-2018.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://images.contentful.com/f42iyx0drm0u/2PuqVJe5AAqUCEmaMIGACA/54a1940e62057dacfddf5fa14eecf023/react-angular-vue-jan-2018.png?w=900&h=413" /></div></a></p>
<p>We can see that React is far ahead of Angular and Vue. What is less apparent is that Vue has had roughly double the growth rate over the past year compared to Angular. If GitHub stars are an indicator of developer enthusiam or interest, then Vue looks strong there as well, with 79,000 stars compared to Angular's 32,000. React has almost 86,000 stars at this writing.</p>

<h3 id="react">React</h3>
<p><img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9Ii0xMS41IC0xMC4yMzE3NCAyMyAyMC40NjM0OCI+CiAgPHRpdGxlPlJlYWN0IExvZ288L3RpdGxlPgogIDxjaXJjbGUgY3g9IjAiIGN5PSIwIiByPSIyLjA1IiBmaWxsPSIjNjFkYWZiIi8+CiAgPGcgc3Ryb2tlPSIjNjFkYWZiIiBzdHJva2Utd2lkdGg9IjEiIGZpbGw9Im5vbmUiPgogICAgPGVsbGlwc2Ugcng9IjExIiByeT0iNC4yIi8+CiAgICA8ZWxsaXBzZSByeD0iMTEiIHJ5PSI0LjIiIHRyYW5zZm9ybT0icm90YXRlKDYwKSIvPgogICAgPGVsbGlwc2Ugcng9IjExIiByeT0iNC4yIiB0cmFuc2Zvcm09InJvdGF0ZSgxMjApIi8+CiAgPC9nPgo8L3N2Zz4K" height="20" alt="React logo" /><a href="https://reactjs.org/" target="_blank">React</a> was introduced as an open source project in May, 2013. The original author was Jordan Walke, an engineer at Facebook.</p>
<p>React bills itself as, "a JavaScript library for building user interfaces", as opposed to a full framework like Angular. Concerns like routing, state management and data fetching have been left to third parties. This has resulted in a large and very active ecosystem around React.</p>
<div><div class="readableLargeObjectContainer"><iframe src="https://www.youtube.com/embed/XxVg_s8xAms" frameborder="0" id="fitvid47777" /></div></div>
<p>Many large React applications will use the popular <a href="https://redux.js.org/" target="_blank">Redux</a> library for state management and <a href="https://reacttraining.com/react-router/" target="_blank">React Router</a> for routing, but there are other good alternatives available.</p>
<p>React is responsible for popularizing <a href="https://github.com/getify/Functional-Light-JS/tree/master/manuscript" target="_blank">functional programming</a> principles among a new generation of developers. Although not a purely functional library, it allows developers to work in a largely functional style, particularly when combined with Redux.</p>
<p>For more information on how React compares to the other popular frameworks, see my article on <a href="https://javascriptreport.com/why-is-react-more-popular-than-angular/" target="_blank">React and Angular</a>, and this one on <a href="https://javascriptreport.com/how-is-react-different-from-vue/" target="_blank">React and Vue</a>.</p>

<ul>
<li>Hugely popular with a strong job market</li>
<li>Lots of training resources and third-party libraries to help accelerate development</li>
<li>Best choice for cross-platform teams (web, mobile, desktop, other devices)</li>
<li>Versatile</li>
<li>Strong corporate support (Facebook)</li>
</ul>

<ul>
<li>Abundance of choice can be overwhelming at first</li>
<li>Best practices not always clear to newcomers</li>
<li>Learning curve can be steep for building larger applications</li>
</ul>
<h4 id="additionalresources">Additional Resources</h4>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="angular">Angular</h3>
<p><img src="https://images.contentful.com/f42iyx0drm0u/1XKikNcdGAGmKEKC2A2q0S/f541d5e19773e3703af7b04002f51f29/angular.png?w=100" alt="Angular logo" /><a href="https://angular.io/" target="_blank">Angular</a> is the successor to AngularJS. It is a full-featured and opinionated framework that provides defaults for data fetching, state management, development language, and build toolchain.</p>
<p>Perhaps the most notable feature of Angular is its use of <a href="https://www.typescriptlang.org/" target="_blank">TypeScript</a> as the development language. This has made the framework <a href="https://yakovfain.com/2016/01/03/why-java-developers-will-embrace-angular-2-and-typescript/" target="_blank">well-suited</a> to those coming from traditional object-oriented languages like Java and C#, as TypeScript takes inspiration from those languages.</p>
<div><div class="readableLargeObjectContainer"><iframe src="https://www.youtube.com/embed/e3djIqAGqZo" frameborder="0" id="fitvid97312" /></div></div>
<p>It's been said that "enterprises" are the the target users for Angular. In the sense that many large companies have teams familiar with Java and other object-oriented languages, this may be correct.</p>

<ul>
<li>Full-featured framework with well-tested defaults</li>
<li>TypeScript provides familiar language for those with background in object-oriented programming</li>
<li>Strong corporate support (Google)</li>
<li>Clear best practices</li>
</ul>

<ul>
<li>Learning curve can be steep</li>
<li>TypeScript may be a barrier to adoption</li>
<li>Poor start up metrics in benchmarks</li>
</ul>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="vuejs">Vue.js</h3>
<p><img src="https://images.contentful.com/f42iyx0drm0u/3Pxb9zXE00MuEEaoMMQc8C/c5b75f893717dd912d12ad8d978a2239/Vue.png?w=100" alt="Vue logo" />Although often seen as the "new kid on the block", <a href="https://vuejs.org/" target="_blank">Vue</a> has been around since 2013. Evan You is the creator and primary developer, and unlike React and Angular, Vue is not directly supported by a major company. It instead relies on individual and corporate donations.</p>
<p>Of the three most popular frameworks, Vue is widely considered to be the easiest to learn. It is similar to React in many respects, but also has things in common with AngularJS — for example, directives and templates.</p>
<p>Vue's relative simplicity, developer experience, and good performance have contributed to a huge surge in its popularity.</p>
<div><div class="readableLargeObjectContainer"><iframe src="https://www.youtube.com/embed/p1iLqZnZPdo" frameborder="0" id="fitvid231350" /></div></div>
<p>One notable feature of Vue is that it's a "progressive framework" and can be used as a jQuery replacement as well as for large single page applications. From the Vue documentation:</p>
<blockquote>
<p>Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable. The core library is focused on the view layer only, and is easy to pick up and integrate with other libraries or existing projects.</p>
</blockquote>
<p>While Angular is opinionated and React agnostic about concerns like routing and state management, Vue takes a middle approach, with official routing and state management solutions that are optional, but kept in sync with the core library.</p>
<p>To learn more about how Vue compares to React, see <a href="https://javascriptreport.com/how-is-react-different-from-vue/" target="_blank">my article</a> that reviews the differences.</p>

<ul>
<li>Easy to learn</li>
<li>Good documentation</li>
<li>Surging in popularity and usage</li>
<li>Best performance of top three frameworks</li>
</ul>

<ul>
<li>Current job market is less than that for React and Angular</li>
</ul>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h2 id="historicallysignificant">Historically Significant</h2>
<p>There was a time some years ago when these frameworks would have been considered the "Big Three". Although less popular today, they are still widely used and have been influential in the development of later frameworks.</p>

<h3 id="angularjs">AngularJS</h3>
<p><img src="https://images.contentful.com/f42iyx0drm0u/5pgSrDJ63608UmqQUE2ySy/abcbce8ef53dabc058813804df4796c3/AngularJS_logo.png?w=100" alt="AngularJS logo" />In 2013, <a href="https://angularjs.org/" target="_blank">AngularJS</a> was the most popular framework. Some of the factors contributing to its popularity during that period were its MVC architecture, declarative programming style, two-way data binding, and robust feature set.</p>
<p>AngularJS has an opinionated approach and aims to provide developers with a <a href="https://docs.angularjs.org/guide/introduction" target="_blank">complete solution</a>:</p>
<blockquote>
<p>AngularJS is not a single piece in the overall puzzle of building the client-side of a web application. It handles all of the DOM and AJAX glue code you once wrote by hand and puts it in a well-defined structure. This makes AngularJS opinionated about how a CRUD (Create, Read, Update, Delete) application should be built. But while it is opinionated, it also tries to make sure that its opinion is just a starting point you can easily change.</p>
</blockquote>
<p>In late 2013 React was introduced. React used unidirectional data flow and argued that two-way data binding made it difficult to understand applications, particularly as they scaled. In 2014, the Angular team announced Angular 2, which would subsequently be renamed to simply, <a href="#angular" target="_blank">Angular</a>. This new version would introduce unidirectional data flow among other <a href="http://eisenbergeffect.bluespire.com/all-about-angular-2-0/" target="_blank">major changes</a>. This marked the beginning of a long decline in the popularity of AngularJS.</p>
<p>Despite the growth of its successor project, AngularJS is still widely used and is in active development.</p>

<ul>
<li>Abundant training resources</li>
<li>Good documentation</li>
<li>Very well established</li>
<li>Full featured</li>
</ul>

<ul>
<li>Two-way data binding, other technical issues that may not be desirable</li>
<li>Declining popularity (fewer jobs)</li>
</ul>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>
<h3 id="backbone">Backbone</h3>
<p><img src="https://images.contentful.com/f42iyx0drm0u/AFRKH9ankGeKC0q6eS6eo/dde426b8c4a45f7b1ebdb8004695cc00/backbone.png?w=100" alt="Backbone logo" />Authored by Jeremy Ashkenas, who also created CoffeeScript, <a href="http://backbonejs.org/" target="_blank">Backbone</a> was initially released in the fall of 2010. A key part of the Backbone ecosystem is <a href="https://marionettejs.com/" target="_blank">Marionette</a>, a framework that simplifies development.</p>
<p>Backbone is significant because it was one of the first frameworks to bring more structure to front end applications by implementing a <a href="https://blog.codinghorror.com/understanding-model-view-controller/" target="_blank">MVC pattern</a>. From the documentation:</p>
<blockquote>
<p>The single most important thing that Backbone can help you with is keeping your business logic separate from your user interface. When the two are entangled, change is hard; when logic doesn't depend on UI, your interface becomes easier to work with.</p>
</blockquote>
<p>In recent years Backbone has seen a decline in usage, although it continues to be shipped in the latest version of the Drupal content management system. One relevant <a href="https://benmccormick.org/2016/03/07/the-sad-state-of-the-backbone-ecosystem" target="_blank">comment</a> on a possible reason for the decline:</p>
<blockquote>
<p>Backbone’s author, Jeremy Ashkenas made a decision to call Backbone “finished” in terms of API and feature set after the 1.0 release. This has the advantage of leaving Backbone as by far the most stable major JavaScript framework, but hinders efforts to pull in lessons from other frameworks</p>
</blockquote>

<ul>
<li>Provides code structure</li>
<li>Stable project</li>
</ul>

<ul>
<li>Declining popularity (fewer jobs)</li>
<li>Imperative programming style (as opposed to popular declarative style)</li>
</ul>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="ember">Ember</h3>
<p><img src="https://images.contentful.com/f42iyx0drm0u/CmTdkS22aWg82MYqoSOiE/d3780bbce78ca5b50c0cebb3633c7b07/ember.png?w=100" alt="Ember logo" /><a href="https://www.emberjs.com/" target="_blank">Ember</a> was authored by Yehuda Katz, a prolific creator or contributor to numerous open source projects. Ember is based on the MVVM pattern and has a rich feature set. It also has a strong <a href="https://en.wikipedia.org/wiki/Ember.js" target="_blank">philosophical viewpoint</a>:</p>
<blockquote>
<p>Ember sets out to provide a wholesale solution to the client-side application problem. This is in contrast to many JavaScript frameworks that start by providing a solution to the V in MVC (Model–View–Controller), and attempt to grow from there...</p>
<p>Ember is one component of a set of tools that work together to provide a complete development stack. The aim of these tools is to make the developer productive immediately. For example Ember CLI, provides a standard application structure and build pipeline. It also has a pluggable architecture and over 3500 addons to enhance and extend it.</p>
</blockquote>
<p>One of the major criticisms of Ember is its large size, which has a negative impact on performance. Ember is also viewed as having a steep learning curve and difficult to master.</p>

<ul>
<li>Clear best practices</li>
<li>Very well established</li>
<li>Full featured</li>
</ul>

<ul>
<li>Large size</li>
<li>Steep learning curve</li>
<li>Declining popularity (fewer jobs)</li>
</ul>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h2 id="notable">Notable</h2>
<p>The frameworks listed in this section all have good documentation and healthy communities around them. Although they aren’t as widely used as "The Big Three", they fill important niches and are notable for their unique or innovative approaches.</p>

<h3 id="aurelia">Aurelia</h3>
<p><img src="https://images.contentful.com/f42iyx0drm0u/2hIx26Q1sEGua0ewOiiUCC/0a4b53b1d853f97522d83c04b73c8040/aurelia.png?w=100" alt="Aurelia logo" /><a href="http://aurelia.io/" target="_blank">Aurelia</a>, authored by Rob Eisenberg, can be seen as a decendant of both AngularJS and Eisenberg's previous framework, Durandal. Prior to creating Aurelia, Eisenberg was a part of the Angular team, leaving in late 2014 over disagreement with the direction of the Angular 2 project.</p>
<p>Aurelia is a complete framework. Here's the basic pitch from the documentation:</p>
<blockquote>
<p>Aurelia provides core capabilities like dependency injection, templating, routing and pub/sub, so you don't have to piece together a bunch of libraries in order to build an application. On top of this rich core, Aurelia also provides a number of additional plugins for internationalization, validation, modal dialogs, UI virtualization and much more.</p>
<p>You also don't have to cobble together a bunch of different tools. Aurelia provides a CLI for generating and building projects, a browser plugin for debugging and a VS Code plugin as well. Yet, you're not forced to use any of these as Aurelia is structured to enable you to swap out any detail, even down to the templating/binding engine, in order to guarantee maximum flexibility.</p>
</blockquote>
<div><div class="readableLargeObjectContainer"><iframe src="https://player.vimeo.com/video/117778145?title=0&byline=0&portrait=0" frameborder="0" id="fitvid675994" /></div></div>

<ul>
<li>Complete solution</li>
<li>Language agnostic, works with JavaScript, TypeScript and other languages</li>
<li>Stable API</li>
</ul>

<ul>
<li>Smaller community vs top frameworks</li>
<li>Fewer job opportunities</li>
</ul>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p><img src="https://images.contentful.com/f42iyx0drm0u/41teYJRcmQ6OqiKiKmaSC0/189e48f023c910cb992068d7e51da9ea/Elm.png?w=100" alt="Elm logo" /><a href="http://elm-lang.org/" target="_blank">Elm</a> is somewhat unique on this list. Rather than a typical framework, it's actually a separate language that compiles to JavaScript, similar to <a href="#reason" target="_blank">Reason</a>. However, it positions itself as an alternative to React:</p>
<blockquote>
<p>Elm is a functional language that compiles to JavaScript. It competes with projects like React as a tool for creating websites and web apps. Elm has a very strong emphasis on simplicity, ease-of-use, and quality tooling...I can safely guarantee that if you give Elm a shot and actually make a project in it, you will end up writing better JavaScript and React code.</p>
</blockquote>
<p>Elm has also been highly influential, including being one of the sources of inspiration for the popular <a href="https://redux.js.org/docs/introduction/PriorArt.html" target="_blank">Redux</a> state management library.</p>
<p>The basic advantages of Elm:</p>
<blockquote>
<p>Forget what you have heard about functional programming. Fancy words, weird ideas, bad tooling. Barf. Elm is about:</p>
<ul>
<li>No runtime errors in practice. No null. No undefined is not a function.</li>
<li>Friendly error messages that help you add features more quickly.</li>
<li>Well-architected code that stays well-architected as your app grows.</li>
<li>Automatically enforced semantic versioning for all Elm packages.</li>
</ul>
<p>No combination of JS libraries can ever give you this, yet it is all free and easy in Elm. Now these nice things are only possible because Elm builds upon 40+ years of work on typed functional languages.</p>
</blockquote>

<ul>
<li>Elimination of virtually all runtime errors</li>
<li>Strong architecture</li>
<li>Simplified refactoring</li>
</ul>

<ul>
<li>Interoperability with JavaScript required in some cases (added complexity)</li>
<li>Smaller commmunity</li>
<li>Fewer job opportunties</li>
</ul>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="inferno">Inferno</h3>
<p><img src="https://images.contentful.com/f42iyx0drm0u/2sta2RFiqE8y4OcSkkC6Og/8a65bda7c2f422d60b2005b6ef73b20b/inferno.png?w=100" alt="Inferno logo" />If performance is your primary concern, <a href="https://infernojs.org/" target="_blank">Inferno</a> might be the framework for you. Originally authored by Dominic Gannaway — now a member of the React team — Inferno was initially designed to prove that a JavaScript framework could perform well on mobile devices.</p>
<blockquote>
<p>Inferno started as an idea two years ago, to see if a UI library could really improve the experience, battery, memory usage and performance on mobile devices. At the time we really struggled to get good performance on any UI library/framework – it simply wasn't happening...</p>
<p>Inferno proves that it is possible to be fast on mobile...In terms of performance, Inferno is currently the fastest JavaScript UI library there is – both in benchmarks and actual real-world scenarios. It excels on the browser at initial page load, parse times, render times and update times. Inferno's server-side rendering is around 5x faster than React, around 3x faster than Angular 2 and around 1.5x faster than Preact and Vue.</p>
</blockquote>
<p>Inferno has an API that is very similar to React and it's possible to port a React app directly to Inferno using the <code>inferno-compat</code> library.</p>
<p>Inferno also has it's own router, soon to be updated to match the API of React Router 4, and is compatible with the Redux and MobX state management libraries.</p>

<ul>
<li>Excellent performance</li>
<li>Familiar API for React developers</li>
<li>Good documentation</li>
</ul>

<ul>
<li>Small community</li>
<li>Using <code>inferno-compat</code> may impact performance</li>
</ul>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="polymer">Polymer</h3>
<p><img src="https://images.contentful.com/f42iyx0drm0u/1xLcr81wegoCookgq8sKAi/a5c7efcf07bfcf343da6546e06df022e/polymer.png?w=100" alt="Polymer logo" /><a href="https://www.polymer-project.org/" target="_blank">Polymer</a> is a Google-backed libary focused on <a href="https://www.w3.org/standards/techs/components#w3c_all" target="_blank">Web Components</a>, a proposed group of technologies that are currently not well-supported in browsers. Polymer, along with the Polymer App Toolbox, helps developers use these technologies today to build web applications.</p>
<blockquote>
<p>Polymer is a lightweight library that helps you take full advantage of Web Components.</p>
<p>With Web Components, you can create reusable custom elements that interoperate seamlessly with the browser’s built-in elements, or break your app up into right-sized components, making your code cleaner and less expensive to maintain.</p>
<p>Polymer sprinkles a bit of sugar over the standard Web Components APIs, making it easier for you to get great results.</p>
</blockquote>
<p>A primary motivation of the Polymer project is to move the web platform forward. The Polymer team have a #UseThePlatform hashtag that they explain on their About page:</p>
<blockquote>
<p>...there are real costs to doing too much outside and above the platform itself—costs that both developers and users pay. Developer costs come in the form of complexity and lock-in.</p>
<p>Over time, the stacks we’ve built on top of the platform have pushed web development further and further from the simplicity of view-source and shift-refresh, to a place where every project begins with an overwhelming sea of choices.</p>
<p>Thanks to new web platform primitives, many of the needs we’ve addressed by building over and around the platform can now be met by the platform itself...</p>
<p>We believe the patterns, libraries and tools we work on are beneficial, and we're happy to see them widely adopted. But our campaign to #UseThePlatform is ultimately not about driving people to use the stuff the Polymer Project builds. It’s about promoting the use of the web platform to deliver the best apps possible</p>
</blockquote>
<p>If you've followed Google's much-appreciated efforts to promote the web platform over the years, much of this will sound familiar and in line with other efforts from the company.</p>

<ul>
<li>Strong corporate support (Google)</li>
<li>Supports emerging web standards</li>
</ul>

<ul>
<li>Community complaints around communication</li>
<li>Poor browser support limits options/implementation of vision</li>
</ul>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="preact">Preact</h3>
<p><img src="https://images.contentful.com/f42iyx0drm0u/7jomguCDTOAkI6w2gaI66I/dc569b96c927a004d72c343e0ac7a093/preact.png?w=100" alt="Preact logo" />Authored by Jason Miller, <a href="https://preactjs.com/" target="_blank">Preact</a> is a well-established React alternative that emphasizes small library size. Coming in at 3KB gzipped, Preact uses the same API as React and is compatible with much of the ecosystem.</p>
<blockquote>
<p>Preact itself is not intended to be a reimplementation of React. There are differences. Many of these differences are trivial, or can be completely removed by using preact-compat, which is an thin layer over Preact that attempts to achieve 100% compatibility with React.</p>
<p>The reason Preact does not attempt to include every single feature of React is in order to remain small and focused - otherwise it would make more sense to simply submit optimizations to the React project, which is already a very complex and well-architected codebase.</p>
</blockquote>
<p>Preact is used by a number of large organizations including Lyft, Pepsi and <a href="https://eng.uber.com/m-uber/" target="_blank">Uber</a>. Although Preact has better start up performance (page load, for example) than React, in the latest benchmarks React is faster at updating the UI once the page is loaded.</p>

<ul>
<li>Lightweight</li>
<li>Good documentation</li>
<li>React-compatible</li>
</ul>

<ul>
<li>Smaller community than React (but lots of overlap, intermingling)</li>
<li>Using <code>preact-compat</code> may impact performance</li>
</ul>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="reason">Reason</h3>
<p><img src="https://images.contentful.com/f42iyx0drm0u/3cubmjES7e8Ayo2Cmqi8OE/39815a267b449d151f0276c9b815340c/reason.png?w=100" alt="Reason logo" />In a way, <a href="https://reasonml.github.io/" target="_blank">Reason</a> can be thought of as a part of the React ecosystem. However, it is much more than that. Reason is a syntax on top of the OCaml langauge. It can compile to JavaScript, but it can also compile to assembly and be used to build desktop and mobile applications. Here's some further explanation from the documentation:</p>
<blockquote>
<p>Reason is not a new language; it's a new syntax and toolchain powered by the battle-tested language, OCaml. Reason gives OCaml a familiar syntax geared toward JavaScript programmers, and caters to the existing NPM/Yarn workflow folks already know...</p>
<p>Reason compiles to JavaScript thanks to our partner project, BuckleScript, which compiles OCaml/Reason into readable JavaScript with smooth interop. Reason also compiles to fast, barebone assembly, thanks to OCaml itself.</p>
</blockquote>
<p>Reason (sometimes referred to as ReasonML) has a companion project, <a href="https://reasonml.github.io/reason-react/" target="_blank">ReasonReact</a>:</p>
<blockquote>
<p>ReasonReact is a safer, simpler way to build React components, in Reason.</p>
<p>By leveraging the latter's great type system, expressive language features and smooth interoperability with JS, ReasonReact packs ReactJS' features into an API that is:</p>
<ul>
<li>Safe and statically typed</li>
<li>Simple and lean</li>
<li>Familiar and easy to insert into an existing ReactJS codebase</li>
<li>Well thought-out (made by the creator of ReactJS himself!)</li>
</ul>
<p>It is often said that writing ReactJS code feels like "just using JavaScript". The same applies to ReasonReact, but we push it further; writing routing, data management, component composition and components themselves feel like "just using Reason".</p>
</blockquote>

<ul>
<li>Strong corporate support (Facebook)</li>
<li>Good documentation</li>
<li>Versatile</li>
<li>Familiar for React developers</li>
</ul>

<ul>
<li>Very new??</li>
</ul>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="svelte">Svelte</h3>
<p><img src="https://images.contentful.com/f42iyx0drm0u/6gU9pBmwc8ysGgomkCCemw/93d06b4522399f515c7c532e41901079/svelte.png?w=100" alt="Svelte logo" />Authored by Rich Harris, <a href="https://github.com/sveltejs/svelte" target="_blank">Svelte</a> takes a unique approach. It compiles your app at build time so that you ship the lightest weight code possible. From the documentation:</p>
<blockquote>
<p>...Svelte has a crucial difference: rather than interpreting your application code at run time, your app is converted into ideal JavaScript at build time. That means you don't pay the performance cost of the framework's abstractions, or incur a penalty when your app first loads.</p>
<p>And because there's no overhead, you can easily adopt Svelte in an existing app incrementally, or ship widgets as standalone packages that work anywhere.</p>
</blockquote>
<p>An interesting project related to Svelte is <a href="https://sapper.svelte.technology/" target="_blank">Sapper</a>, a framework similar in philosophy to <a href="https://learnnextjs.com/" target="_blank">Next.js</a>, but with a greater emphasis on performance.</p>
<blockquote>
<p>Sapper is a framework for building extremely high-performance web apps...There are two basic concepts:</p>
<ul>
<li>Each page of your app is a Svelte component</li>
<li>You create pages by adding files to the routes directory of your project. These will be server-rendered so that a user's first visit to your app is as fast as possible, then a client-side app takes over</li>
</ul>
<p>Building an app with all the modern best practices — code-splitting, offline support, server-rendered views with client-side hydration — is fiendishly complicated. Sapper does all the boring stuff for you so that you can get on with the creative part.</p>
</blockquote>

<ul>
<li>Fast and lightweight</li>
<li>Good documentation</li>
<li>Innovative</li>
</ul>

<ul>
<li>Small community</li>
<li>Very new (but promising!)</li>
</ul>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h2 id="therestofthepack">The Rest of the Pack</h2>
<p>There are a lot of interesting frameworks here. Some are the product of a single developer, while others have strong communities with a large number of contributors and corporate sponsorship.</p>
<p>If you're an author or contributor to one of these projects and you'd like to provide more or updated information, please <a href="https://twitter.com/__jhannah" target="_blank">reach out to me</a>.</p>

<h3 id="apprun">AppRun</h3>
<p>Authored by Yiyi Sun, <a href="https://github.com/yysun/apprun" target="_blank">AppRun</a> in a small (3KB) library that uses TypeScript as the development language and takes inspiration from Elm:</p>
<blockquote>AppRun is a lightweight library...using the elm style model-view-update architecture and event publication and subscription.</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="bindingscala">Binding.scala</h3>
<p>Binding.scala is a one-way data-binding library written in Scala, although it targets both JavaScript and JVM. From the <a href="https://github.com/ThoughtWorksInc/Binding.scala" target="_blank">documentation</a>:</p>
<blockquote>Binding.scala can be used as a reactive templating language in both web and desktop GUI development. It enables you use native XHTML literal syntax to create reactive DOM nodes, which are able to automatically change whenever the data source changes...Binding.scala has more features and less concepts than other reactive web frameworks like ReactJS.</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="bobril">Bobril</h3>
<p><a href="http://bobril.com/" target="_blank">Bobril</a> takes inspiration from React and <a href="#mithril" target="_blank">Mithril</a>. From the documentation:</p>
<blockquote>
<p>It is fast, low size framework with rendering based on Virtual DOM. The main focus is on speed and simplicity of code generation...Content and behavior of any page can be defined simply by composing JavaScript objects.</p>
<p>The page content rendering is based on comparison of Virtual DOMs. The application has some state in time and bobril application generates the Virtual DOM according to this state. Virtual DOM is an object representation of the resultant DOM. If some state-changing event occurs and the previous Virtual DOM is different than currently generated Virtual DOM, the real DOM will change according to this change.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://www.codeproject.com/Articles/1044425/Bobril-I-Getting-Started" target="_blank">Bobril - I - Getting Started</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p><a href="https://choo.io/" target="_blank">Choo</a> is a functional library for building user interfaces. It's small (4KB) and supports server rendering. The Choo philosophy:</p>
<blockquote>
<p>We believe frameworks should be disposable, and components recyclable. We don't want a web where walled gardens jealously compete with one another. By making the DOM the lowest common denominator, switching from one framework to another becomes frictionless. Choo is modest in its design; we don't believe it will be top of the class forever, so we've made it as easy to toss out as it is to pick up...We want everyone on a team, no matter the size, to fully understand how an application is laid out. And once an application is built, we want it to be small, performant and easy to reason about. All of which makes for easy to debug code, better results and super smiley faces.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="cyclejs">Cycle.js</h3>
<p>Billed as a "functional and reactive JavaScript framework for predictable code" <a href="https://cycle.js.org/" target="_blank">Cycle.js</a> is primarily the work of <a href="https://twitter.com/andrestaltz" target="_blank">André Staltz</a>. It has over 100 contributors and corporate sponsorship. From the documentation:</p>
<blockquote>
<p>Cycle’s core abstraction is your application as a pure function main() where inputs are read effects (sources) from the external world and outputs (sinks) are write effects to affect the external world. These I/O effects in the external world are managed by drivers: plugins that handle DOM effects, HTTP effects, etc.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p><a href="https://dio.js.org/" target="_blank">DIO</a> is a lightweight (7KB), declarative UI library that offers an alternative to React:</p>
<blockquote>
<p>There a lot of small details that give DIO its edge that don't realy touch on new API's but rather on creating a larger surface area of what React already supports and adding to this.</p>
<p>For example React can render strings, numbers, elements and components but what if it was able to render Promises or Thenables? This would help solve a lot of "problems" with data fetching and lazy loading that is possible with React but not declaratively incentivised at the library level.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://dio.js.org/misc/comparison.html" target="_blank">Comparison with React</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p>One of the important principles behind <a href="https://dojo.io/" target="_blank">Dojo</a> is accessibility, which makes me think it's a potential candidate for projects in government and higher education, where there are often stringent compliance requirements. From the website:</p>
<blockquote>
<p>Dojo 2 is grounded in the belief that accessibility is as important online as it is in our physical environments, and architects of both share a similar responsibility to provide access to all...all Dojo 2 widgets have been designed to be accessible by default, and any tools needed to meet WCAG standards have been integrated into @dojo/widget-core and @dojo/widgets.</p>
</blockquote>
<p>Internationalization is another area of focus:</p>
<blockquote>
<p>Internationalization, or i18n, is the process of decoupling an application from a particular language or culture, and is a major requirement of most enterprise applications. As such, internationalization is one of Dojo 2’s core concerns. @dojo/i18n, Dojo 2’s internationalization ecosystem, provides everything that is needed to internationalize and localize an application, from locale-specific messaging to date, number, and unit formatting.</p>
</blockquote>
<p>Like Angular, Dojo uses TypeScript as its development language.</p>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="domvm">Domvm</h3>
<p><a href="http://leeoniya.github.io/domvm/" target="_blank">Domvm</a> is a, "thin, fast, dependency-free vdom view layer". Like Vue, it can be used as a jQuery replacement. Similar to React, it leaves concerns beyond views to other libraries (but provides a good list of options). From the documentation:</p>
<blockquote>
<p>domvm is a flexible, pure-js view layer for building high performance web applications. Like jQuery, it’ll happily fit into any existing codebase without introducing new tooling or requiring major architectural changes...As a view layer, domvm does not include some things you would find in a larger framework. This gives you the freedom to choose libs you already know or prefer for common tasks. domvm provides a small, common surface for integration of routers, streams and immutable libs.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://www.reddit.com/r/javascript/comments/5m70ex/reacts_tictactoe_demo_using_domvm/" target="_blank">React's tic-tac-toe demo using domvm</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p><a href="https://github.com/dvajs/dva" target="_blank">dva</a> is a popular framework from China. The documentation in English is somewhat limited. It takes inspiration from a number of functional libraries/frameworks like Elm, Choo and Redux.</p>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p>Although <a href="https://github.com/atom/etch" target="_blank">Etch</a> can be used for front end web applications, its target usage is in Atom packages and the Electron desktop framework. From the documentation:</p>
<blockquote>
<p>Etch is a library for writing HTML-based user interface components that provides the convenience of a virtual DOM, while at the same time striving to be minimal, interoperable, and explicit. Etch can be used anywhere, but it was specifically designed with Atom packages and Electron applications in mind.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://arcath.net/2017/05/etch-router/" target="_blank">Etch Router</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p><a href="https://gruujs.com/" target="_blank">Gruu</a> is a relatively new framework by Marek Łabuz. From Marek's article introducing Gruu:</p>
<blockquote>
<p>I believe that none of the existing libraries is perfect. Each time a new library/framework is created, some new idea is revealed. No matter if the new library is good or bad. It always brings something unique that is valuable.</p>
<p>Many frontend libraries rely on a render function that is called each time something changes, no matter what the change affects. It leads to unnecessary renders of the parts of the application that has not changed, but still we have to check it because we don’t know for sure...Gruu gets rid of a render function. Instead, it renders only once at the beginning, then it changes only this parts of the view that have actually changed without rendering whole components.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://medium.com/@lmrk/creating-web-applications-in-gruu-ab68737d34e5" target="_blank">Creating Single Page Applications in Gruu</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="glimmer">Glimmer</h3>
<p><a href="https://glimmerjs.com/" target="_blank">Glimmer</a> is part of the Ember ecosystem and even uses the Ember CLI to manage projects. As mentioned when discussing Ember, it is a large framework. Glimmer provides Ember developers with a lighter weight option for building single page apps. If needed, Glimmer components can be dropped directly into Ember without a problem.</p>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="hyperapp">Hyperapp</h3>
<p>Coming in at a very slender 1KB, <a href="https://hyperapp.js.org/" target="_blank">Hyperapp</a> is a library with a minimalist API. It does, however, support server rendering. The Hyperapp approach:</p>
<blockquote>
<p>Hyperapp is a JavaScript library for building web applications.</p>
<p>Minimal: Hyperapp was born out of the attempt to do more with less. We have aggressively minimized the concepts you need to understand while remaining on par with what other frameworks can do.</p>
<p>Functional: Hyperapp's design is inspired by The Elm Architecture. Create scalable browser-based applications using a functional paradigm. The twist is you don't have to learn a new language.</p>
<p>Batteries-included: Out of the box, Hyperapp combines state management with a VDOM engine that supports keyed updates & lifecycle events — all with no dependencies.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="hyperdom">Hyperdom</h3>
<p>Formerly named, Plastiq, <a href="https://github.com/featurist/hyperdom" target="_blank">Hyperdom</a>, is a "fast, feature rich virtual-dom framework for building dynamic browser applications." From the documentation:</p>
<blockquote>
<p>Hyperdom applications are made of regular JavaScript objects that represent application state with render() methods that define how that state is represented in HTML. Hyperdom supports a simple event-update-render cycle, promises for asynchronous operations, JSX, non-JSX, client-side routing, SVG, two-way data binding, and optimises for performance, developer usability and simplicity of application architecture.</p>
</blockquote>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="hyperhtml">hyperHTML</h3>
<p>Framework agnostic, <a href="https://viperhtml.js.org/" target="_blank">hyperHTML</a> was created to, "simplify DOM performance best practices...is 100% ECMAScript compliant and it weighs in at less than 4Kb". From the introductory article:</p>
<blockquote>
<p>It’s nothing more than a function, that works bound with DOM nodes and fragments as context. You bind your target node once, or even more if you don’t care, and you render the same template literals over and over simply passing new data.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p>The <a href="https://github.com/ivijs/ivi" target="_blank">Ivi</a> documentation notes that, although Ivi is small, size is at the bottom of its list of priorities:</p>
<blockquote>
<p>It seems that nowadays many people in javascript community were brainwashed that small library size is a synonym to fast performance and simple implementation. In reality it usually means that library is using different tricks to reduce code size by using inappropriate data structures (slower performance), initializing data structures at runtime (slower bootstrap performance), reusing code for many different data types (slower performance), etc.</p>
<p>Library size in ivi library is at the bottom on the list of priorities:</p>
<ul>
<li>Correctness</li>
<li>Consistency / Predictable Behavior</li>
<li>Performance / Developer Experience</li>
<li>Library Size</li>
</ul>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://github.com/ivijs/todomvc/" target="_blank">Ivi Todo MVC</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="knockout">Knockout</h3>
<p>Using the MVVM pattern, <a href="http://knockoutjs.com/" target="_blank">Knockout</a> is a library that has been around for a while. From the documentation:</p>
<blockquote>
<p>Knockout is a JavaScript MVVM (a modern variant of MVC) library that makes it easier to create rich, desktop-like user interfaces with JavaScript and HTML. It uses observers to make your UI automatically stay in sync with an underlying data model, along with a powerful and extensible set of declarative bindings to enable productive development.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="maquette">Maquette</h3>
<p><a href="https://maquettejs.org/" target="_blank">Maquette</a> is a lightweight (3KB) library inspired by React, Mithril and Mercury:</p>
<blockquote>
<p>Maquette is a virtual DOM implementation that excels in both speed and simplicity. It solves the problem of keeping the user interface in sync with underlying data.</p>
<p>Maquette allows you to specify the UI using plain Javascript. This makes maquette easy to learn, easy to debug and easy to deploy. Maquette is very unopionated by design, making integration with other frameworks and libraries as painless as possible.</p>
</blockquote>
<p>Although it's not the default, you can use TypeScript with Maquette.</p>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="marko">Marko</h3>
<p>A product of eBay Open Source, <a href="https://markojs.com/" target="_blank">Marko</a> is a reactive front end framework that emphasizes UI performance. Similar to Vue, you can use single file components that include component logic, template and CSS.</p>
<p>Here's a quote on Marko vs React from the lead developer, Patrick Steele-Idem:</p>
<blockquote>
<p>While many of the features in Marko were inspired by React, Marko and React offer very different usability and performance characteristics. Marko was designed to avoid almost all boilerplate and is more closely aligned with HTML. In almost all cases, a Marko UI component will require less lines of code than its React JSX equivalent while maintaining readability and allowing the same expressiveness as JSX.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="mithril">Mithril</h3>
<p><a href="https://mithril.js.org/" target="_blank">Mithril</a> is a lighweight framework. Unlike React, it incudes functionality for routing, XHR and state management.  The pitch for Mithril:</p>
<blockquote>
<p>Why use Mithril? In one sentence: because Mithril is pragmatic. This 10 minute guide is a good example: that's how long it takes to learn components, XHR and routing - and that's just about the right amount of knowledge needed to build useful applications.</p>
<p>Mithril is all about getting meaningful work done efficiently. Doing file uploads? The docs show you how. Authentication? Documented too. Exit animations? You got it. No extra libraries, no magic.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p>A small (7KB) library, <a href="http://moonjs.ga/" target="_blank">Moon</a> positions itself as an alternative to React, Vue and Mithril.</p>
<blockquote>
<p>Moon is a minimal, blazing fast library for building user interfaces. It combines the positive aspects of popular libraries into one small package. It's super lightweight, and includes advanced optimizations to ensure fast render times. The API is small and intuitive, while still remaining powerful. Moon is compatible with IE9+.</p>
<p>Yes, there have been a lot of front end libraries released lately, and many people prefer different parts about each of these libraries. For example, React provides the ability to use JSX and uses a virtual DOM, Angular provides easy to use directives, and Ember provides a nice templating engine built in.</p>
<p>Moon aims to combine the best parts of these libraries into a single, lightweight package, while providing improved performance.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://sabe.io/tutorials/getting-started-with-moon-js" target="_blank">Getting Started with Moon.js</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p><a href="https://nerv.aotu.io/" target="_blank">Nerv</a> is a new framework out of China. It bills itself as a, "blazing fast React alternative, compatible with IE8 and React 16." In fact, you can convert a React app to Nerv simply by adding an alias in your webpack config. All of that and a library size of 4.4 KB.</p>
<p>Because it is so new and makes claims of superior performance vs React — some members of the React community asked for clarification on those claims, as well as more information about Nerv. From the author's reply:</p>
<blockquote>
<p>In my humble opinion, The biggest difference between preact, Inferno, and Nerv, is not some technical issue like what’s the right way to implementing a React feature. It is about the what does the library want to achieve. In preact, maybe they just want a lite library, Inferno want to be fast as they can, React compatibility just a bonus, they are both need a compat module to do that. But for Nerv, compatible with React is our main goal, by doing that, we can sacrifice performance and size.</p>
<p>Peter Mikitsh’s criticism is right. Nerv can’t pass React fiber(16) 100% unit test, which is predictable —— the React team takes whole year to achieve the target, how can two guys come from nowhere(says by some guy in Hacker news) be able to do that?</p>
<p>So, What’s the tradeoffs? Obviously, some third-party React component/library couldn’t work properly in Nerv. But which one? To be honest I don’t know. I’m glad to be heard that Next.js next-news worked on first try., but in the meantime, Benchmark tabs don't work in Firefox (fixed) —— All of this, We wouldn’t know if we don’t go public.</p>
<p>Rome wasn't built in a day. Nerv is not perfect, no library is, particularly in early stage, maybe there still tons of bug we don’t know. Therefore we decided to open source, to go public, we need the community’s help, we need your help.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://github.com/NervJS/nerv/issues/10" target="_blank">What's the tradeoff?</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p>NX is the work of Bertalan Miklos, JavaScript engineer at RisingStack. From the <a href="https://github.com/nx-js/framework" target="_blank">NX</a> documentation:</p>
<blockquote>
<p>NX is a modular front-end framework - built with ES6 and Web Components. The building blocks of NX are the core, the middlewares, the components and the utilities. These are all hosted in separate GitHub repos and npm packages.</p>
<p>The NX core is a tiny library, responsible for one thing only. It allows you to create dumb components and to augment them with middlewares. A component executes its middlewares when it is attached to the DOM and it gains all the extra functionalities from them. NX comes with some core middlewares out of the box, which you can find listed below.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="petitdom">petit-dom</h3>
<p>Authored by Yassine Elouafi and one of the fastest in performance benchmarks, <a href="https://github.com/yelouafi/petit-dom" target="_blank">petit-dom</a> takes a minimalist approach:</p>
<blockquote>
<p>Diff algroithm is based on pre-optimizations described at <a href="https://neil.fraser.name/writing/diff/" target="_blank">https://neil.fraser.name/writing/diff/</a> and the algorithm presented in the paper "An O(ND) Difference Algorithm and Its Variations. There is also an excellent article which explains how the algorithm works. The article includes a GUI application to play with the algorithm</p>
</blockquote>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="picodom">Picodom</h3>
<p><a href="https://github.com/picodom/picodom" target="_blank">Picodom</a> is interesting in that it's authored by the same guy behind <a href="#hyperapp" target="_blank">Hyperapp</a>, Jorge Bucaran. Described as a, "1 KB VDOM builder and patch function", Picodom is a tool that can be used to build your own framework:</p>
<blockquote>
<p>Picodom supports keyed updates & lifecycle events — all with no dependencies. Mix it with your favorite state management library or create your own custom view framework.</p>
</blockquote>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p><a href="http://purescript-pux.org/" target="_blank">Pux</a> is a framework that uses <a href="http://www.purescript.org/" target="_blank">PureScript</a>, a strongly-typed, functional programming language that complies to JavaScript. There are currently problems with performance:</p>
<blockquote>
<p>The slow performance arises from translating Pux's (smolder) virtual DOM to React's virtual DOM. The goal is to write a purescript virtual DOM module for smolder, which would avoid that translation step and could be optimized for a monadic datastructure. I suspect this would achieve performance on par with Halogen.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://github.com/alexmingoia/purescript-pux/tree/master/examples/" target="_blank">Pux Examples</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="ractivejs">Ractive.js</h3>
<p>Originally created for use on the Guardian website, <a href="https://ractive.js.org/" target="_blank">Ractive</a> is a reactive, template-driven UI library:</p>
<blockquote>
<p>Unlike other frameworks, Ractive works for you, not the other way around. It doesn't have an opinion about the other tools you want to use with it. It also adapts to the approach you want to take. You're not locked-in to a framework-specific way of thinking. Should you hate one of your tools for some reason, you can easily swap it out for another and move on with life.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="reactlite">react-lite</h3>
<p>Aiming to be a lighter-weight version of React, <a href="https://github.com/Lucifier129/react-lite" target="_blank">react-lite</a>, is an "implementation of React that optimizes for small script size." From the documentation:</p>
<blockquote>
<p>React-lite supports the core APIs of React, such as Virtual DOM, intended as a drop-in replacement for React, when you don't need server-side rendering in browser(no ReactDOM.renderToString & ReactDOM.renderToStaticMarkup).</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://survivejs.com/blog/react-lite-interview/" target="_blank">react-lite - Implementation of React optimized for small size - Interview with Jade</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="redom">RE:DOM</h3>
<p>Authored by Juha Lindstedt, <a href="https://redom.js.org/" target="_blank">RE:DOM</a> is a small (2KB) and fast UI library. In fact, it's one of the best performers in the latest benchmarks. From the website:</p>
<blockquote>
<p>RE:DOM is a tiny (2 KB) DOM library by Juha Lindstedt and contributors, which adds useful helpers to create DOM elements and keeping them in sync with the data.</p>
<p>Because RE:DOM is so close to the metal and doesn't use virtual dom, it's actually faster and uses less memory than almost all virtual dom based libraries, including React (benchmark).</p>
<p>It's also easy to create reusable components with RE:DOM.</p>
<p>Another benefit is, that you can use just pure JavaScript, so no complicated templating languages to learn and hassle with. Plus RE:DOM plays nicely with others. No need to write wrappers for things like Google Maps.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<p><a href="https://redom.js.org/documentation/" target="_blank">Documentation site</a></p>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="reflex">Reflex</h3>
<p>Authored by Irakli Gozalishvili of Mozilla, <a href="https://github.com/mozilla/reflex" target="_blank">Reflex</a> is a library heavily inspired by Elm:</p>
<blockquote>
<p>Reflex is a functional reactive UI library that is heavily inspired by (pretty much is a port of) elm and it's amazingly simple yet powerful architecture where "flux" in react terms is simply a byproduct of a pattern. In order to keep a major attraction of elm — algebraic data types & type safety — the library uses flow, a static type checker for JS. All types are separated from implementation though, so it's your call if you want to take advantage of it or just ignore it.</p>
</blockquote>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p>The <a href="http://riotjs.com/" target="_blank">Riot</a> documentation gets straight to the point:</p>
<blockquote>
<p>The frontend space is indeed crowded, but we honestly feel the solution is still “out there”. We believe Riot offers the right balance for solving the great puzzle. While React seems to do it, they have serious weak points that Riot will solve.</p>
</blockquote>
<p>A major feature of Riot is custom tags (which look a lot like a Vue single file component):</p>
<blockquote>
<p>A custom tag glues relevant HTML and JavaScript together forming a reusable component. Think React + Polymer but with enjoyable syntax and a small learning curve.</p>
</blockquote>
<p>And...</p>
<blockquote>
<p>Riot is Web Components for everyone. Think React + Polymer but without the bloat. It’s intuitive to use and it weighs almost nothing. And it works today. No reinventing the wheel, but rather taking the good parts of what’s there and making the simplest tool possible.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="rxdomh">rxdomh</h3>
<p>Although interesting, <a href="https://github.com/xialvjun/rx-domh" target="_blank">rxdomh</a> has the look of an experimental project. It was inspired by <a href="#binding" target="_blank">Binding.scala</a> and react-flyd.</p>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>


<p><a href="https://ecomfe.github.io/san/" target="_blank">San</a> is another project from Chinese developers. The documenation is in Chinese, but Chrome does a pretty good job with the translation:</p>
<blockquote>
<p>San, is a MVVM component framework. Its small size (12K), good compatibility (IE6), high performance is a reliable and dependable solution for implementing a responsive user interface.</p>
<p>San also supports data-to-view binding instructions, the most commonly used branches in business development, looping instructions, etc. in addition to supporting the syntax features of all native HTML through declarative HTML-like view templates that remain well-used on the basis of, based on the complete frame template string parsing, and build a view of layer node relation tree generated by the UI view of the quick view of a high-performance engine.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://ecomfe.github.io/san/tutorial/start/" target="_blank">San tutorial</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="simulacrajs">Simulacra.js</h3>
<p>It's fair to say that no other framework has a smaller API than <a href="https://simulacra.js.org/" target="_blank">Simulacra</a>:</p>
<blockquote>
<p>Simulacra.js returns a DOM Node that updates when an object changes. Its API is a single function, and it does not introduce any new syntax or a template language. It recursively adds metaprogramming features to vanilla data structures to work.</p>
<p>It is a fairly low cost abstraction, though it may not be quite as fast as hand-optimized code. The approximate size of this library is ~5 KB (minified and gzipped).</p>
</blockquote>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="slimjs">Slim.js</h3>
<p>Authored by Avichay Eyal, <a href="https://github.com/eavichay/slim.js" target="_blank">Slim.js</a> is a lightweight web component authoring library:</p>
<blockquote>
<p>Slim.js is a lightning fast library for development of native web-components and custom-elements based modern applications. No black magic involved. It uses es6+DOM native API and boosts up HTML elements with superpowers.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="http://slimjs.com/#/getting-started" target="_blank">Documentation site</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="stemjs">Stem JS</h3>
<p>Authored by Mihai Ciucu, <a href="https://stemjs.org/" target="_blank">Stem JS</a> is the framework that tries not to be a framework:</p>
<blockquote>
<p>The syntax might look familiar, but Stem is designed to empower individual components and not the framework...</p>
<p>Stem was designed with code maintainability as a primary purpose, regardless if your project has 100 or 100k lines of code.</p>
<p>We also hate it when libraries force programmers to jump through hoops to make any non-standard change to it, so everything is designed to be easily modified.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://stemjs.org/blog/another_javascript_framework/" target="_blank">Another Javascript Framework</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="surplus">Surplus</h3>
<p>In performance benchmarks, <a href="https://github.com/adamhaile/surplus" target="_blank">Surplus</a> was very fast. It also has a different approach, utilizing S.js:</p>
<blockquote>
<p>Surplus is a compiler and runtime to allow S.js applications to create high-performance web views using JSX. Thanks to JSX, the views are clear, declarative definitions of your UI. Thanks to S, they update automatically and efficiently as your data changes.</p>
</blockquote>
<p>Also...</p>
<blockquote>
<p>Surplus is not a React “work-alike,” but it uses the JSX syntax popularized by React to define its views...JSX mitigates some of the risk of adopting (or abandoning) Surplus. Much Surplus JSX code already works as React stateless functional components, and vice versa. Surplus avoids arbitrary differences with React when feasible.</p>
</blockquote>
<h5 id="differenceswithreact">Differences with React:</h5>
<ol>
<li>Surplus makes real DOM elements, not virtual, and they update automatically. This removes most of the React API.</li>
<li>The ref property takes an assignable reference, not a function.</li>
<li>Events are native events, not React's synthetic events.</li>
<li>Surplus is a little more liberal in the property names it accepts, like onClick/onclick, className/class, etc.</li>
</ol>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="thermite">Thermite</h3>
<p><a href="https://github.com/paf31/purescript-thermite" target="_blank">Thermite</a> is another library that uses <a href="http://www.purescript.org/" target="_blank">PureScript</a>, the functional language that compiles to JavaScript. From the documentation:</p>
<blockquote>
<p>It does not provide all of the functionality of React, but instead to provide a clean API to the most commonly-used parts of its API. It is possible to use purescript-react for more specialized use cases.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://github.com/tfausak/purescript-thermite-example" target="_blank">Example App</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="tsers">TSERS</h3>
<p><a href="https://github.com/tsers-js/core" target="_blank">TSERS</a> stands for Transform-Signal-Executor framework for Reactive Streams. From the documentation:</p>
<blockquote>
<p>In the era of the JavaScript fatigue, new JS frameworks pop up like mushrooms after the rain, each of them providing some new and revolutionary concepts. So overwhelming! That's why TSERS was created. It doesn't provide anything new. Instead, it combines some old and well-known techniques/concepts and packs them into single compact form suitable for the modern web application development.</p>
<p>Technically the closest relative to TSERS is Cycle.js, but conceptually the closest one is CALM^2. Roughly it could be said that TSERS tries to combine the excellent state consistency maintaining strategies from CALM^2 and explicit input/output gates from Cycle - the best from both worlds.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://github.com/tsers-js/examples" target="_blank">TSERSful Examples</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="vidom">Vidom</h3>
<p>Authored by Filatov Dmitry, <a href="https://github.com/dfilatov/vidom" target="_blank">Vidom</a> is another React-inspired library:</p>
<blockquote>
<p>Vidom is just a library to build UI. It's highly inspired from React and based on the same ideas. Its main goal is to provide as fast as possible lightweight implementation with API similar to React.</p>
</blockquote>
<h5 id="additionalresources">Additional Resources</h5>

<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>

<h3 id="vuera">Vuera</h3>
<p><a href="https://github.com/akxcv/vuera" target="_blank">Vuera</a> is an unusual library. It allows you to use React componets inside Vue and vice versa. The anticipated use cases are when migrating between React and Vue or when using both frameworks with a single project.</p>
<h5 id="additionalresources">Additional Resources</h5>
<ul>
<li><a href="https://x-team.com/blog/react-vue-component-integration/" target="_blank">Integrating React and Vue Components in One Application</a></li>
</ul>
<p>⬆️ <a href="#top" target="_blank">Return to top</a></p>
<p>Hey! You made it all the way down here! If you’ve enjoyed this post, sign up for my weekly newsletter. I curate the best JavaScript writing from around the web and deliver it to readers every Thursday. The sign up form is right below this article.</p>
<p>Until next time, happy coding…</p>

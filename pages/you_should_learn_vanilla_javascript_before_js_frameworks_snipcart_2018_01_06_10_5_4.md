<a href="https://snipcart.com/blog/learn-vanilla-javascript-before-using-js-frameworks?ref=mybridge.co">https://snipcart.com/blog/learn-vanilla-javascript-before-using-js-frameworks?ref=mybridge.co</a><div id="articleHeader"><h1>Yes, You Should Learn Vanilla JavaScript Before Fancy JS Frameworks</h1></div>

        August 18, 2016

            <div>

                <div class="readableLargeImageContainer"><img src="https://snipcartweb-10f3.kxcdn.com/media/9760/monitor-snipcart-blog.png" /></div>

            

    

    




    
    
        

                
                    <p>It's 2013. Our small dev team is on the verge of shipping one of its most impressive client projects to date. I'm at my stand-up desk, skimming through early morning emails. My partner bursts through the office door:</p>
<p>"Something's wrong with our Angular app, man. I've got a <code>digest is already in progress</code> error popping everywhere, and I can't figure out what's happening," he says, visibly nervous.</p>
<p>But I'm not nervous, nor stressed. I know exactly where to start looking, because I know my JavaScript.</p>
<p>And I know all of this thanks to a small robot. Yup, you read that right: <strong>a robot</strong>.</p>
<hr />
<p>Rewind to 2011.</p>
<p>I was still a dreamy-eyed software engineer student back then, unaffected by <a href="https://snipcart.com/blog/guide-choosing-tech-stack-client-work" target="_blank">the business imperatives of real-world coding</a>. I was passionate about back-end development, and had no desire whatsoever to learn vanilla JavaScript, or anything related.</p>
<p>But my friends and I had to build a soft real-time, task-oriented robot for one of our classes.</p>
<p><div class="readableLargeImageContainer"><img src="https://snipcartweb-10f3.kxcdn.com/media/9904/vanilla-js-before-js-frameworks-robot-story.jpg" alt="vanilla-js-before-js-frameworks-robot-story" /></div></p>
<div> We named the robot Optimus Prime, and eventually sold it to Michael Bay for his Transformers movies. </div>
<p>We quickly stumbled upon this new cool thing called Node.js (quick peek at <a href="https://nodejs.org/docs/v0.4.9/" target="_blank">its docs back then</a>). No fancy dependencies, easy child processes spawning, async and event-driven... and many people online were saying it was the sh*t. We had absolutely no clue of what JavaScript or V8 were, but it still seemed like a good call for our robot project.</p>
<p>Many peers told me to just find a decent library for my use cases, and pull off some copy/pasting art to get the socket communication job done. And I could've done just that.</p>
<p>But I didn't. Although I didn't know it at the time, that was one of the best early career decisions I made.</p>
<p>I started reading avidly instead. About asynchronous programming, the history of JavaScript, its pros and cons, everything. Because I wanted to <strong>master the underlying principles of the language powering my project</strong>. And it took quite a lot of time, coffee, beer, and dummy code to do so.</p>
<p>In between managing my teammates' impatience and creating a not-so-clean, functional robot codebase, <strong>I learned a whole damn lot</strong>.</p>
<hr />
<p>So what's the point here? It's that <strong>I took enough time to understand the core principles of JavaScript before using shortcuts provided by JS frameworks and libraries</strong>. And why is that important? Well, this is what this post is about: <em>not just pretending.</em></p>
<p><div class="readableLargeImageContainer"><img src="https://snipcartweb-10f3.kxcdn.com/media/9901/pretending-vanilla-javascript-knowledge.jpg" alt="pretending-vanilla-javascript-knowledge" /></div></p>
<div> Source: the ever-hilarious <a href="https://twitter.com/iamdevloper" target="_blank">@iamdevloper</a>. </div>
<h2>First, what do I mean by JS "frameworks" here?</h2>
<p>When I use <em>framework</em>, I put all of the Angular, React, Backbone, Ember, Knockout, Vue, Ext, jQuery, Meteor, Express, Koa, Total, Socket.io, and so on, in the same box. Yes, I know some are quite different. Yes, I know some are "not really a framework, but more of a library and BTW have you seen this thread on HN?".</p>
<p>But please, for the sake of this article, let's declare them equivalent in their primary purpose.</p>
<h2>And for those asking "What is vanilla JavaScript?"</h2>
<p>Let me steal an answer from <a href="http://stackoverflow.com/questions/20435653/what-is-vanillajs" target="_blank">koenpeters on Stack Overflow</a>:</p>
<blockquote>
<p>"VanillaJS is a name to refer to using <strong>plain JavaScript without any additional libraries</strong> like jQuery. People use it as a joke to remind other developers that many things can be done nowadays without the need for additional JavaScript libraries."</p>
</blockquote>
<p>Or, in our case, without additional, fancy frameworks.</p>
<h2>Why I think JavaScript frameworks are awesome</h2>
<blockquote>
<p>"JS frameworks help you out by abstracting hard & complex code."</p>
</blockquote>
<blockquote>
<p>"JS frameworks help you ship code faster and increase development velocity."</p>
</blockquote>
<blockquote>
<p>"JS frameworks force you to focus on your app's value rather than its implementation."</p>
</blockquote>
<p>These reasons quickly come up whenever we discuss the popularity of JS frameworks. But to me, they are <em>marketing-ish reasons</em> more than anything else. And I'm not ranting against frameworks here. I've actually used quite a few of them throughout my career (see list in previous section).</p>
<p>And I believe the greatest value there is to find in JS frameworks is <em>collaboration</em>. Their consistent interface and methods allow developers from, say, Canada, the US, and Brazil to understand one another and work together.</p>
<p>If you're building an app with [insert your favorite framework], when the time comes, you'll be able to find an experienced developer to hop in the project codebase with confidence. He or she'll be able to start tackling features without you needing to explain every part of your software architecture.</p>
<p>Another key reason to use frameworks is <em>practice</em>. They make you practice, over and over again. And that's good, really! Practice always leads to mastery, whatever you're trying to accomplish.</p>
<h2>Why I believe JS frameworks are not THAT awesome</h2>
<p>People who work on frameworks implementation are all talented—at least most of them. They do a tremendous job of turning complex things into easy stuff (e.g. providing ruthlessly simple client-side router in IE6). But all of these levels of abstraction can quickly become <em>evil</em>.</p>
<p>In every app development, there comes a day when something doesn't work as expected, and you don't really know why. This is when you have to start digging. And when you start searching through poorly documented, complex, generic, pure JS code, <strong>you'll need a deep understanding of JavaScript</strong> to make it. Otherwise, I can guarantee you're going to lose all the precious time you saved by using your fancy framework. You might just have to buy a new espresso machine to meet your deadlines.</p>
<p><a href="https://twitter.com/home?status=As%20I%20once%20read%20somewhere%3A%20%22You're%20not%20an%20Angular%20nor%20an%20Express%20developer.%20You're%20a%20developer.%22%20http%3A%2F%2Fbit.ly%2F2bBilPl%20via%20%40snipcart%20%23webdev%20%23javascript" target="_blank">As I once read somewhere: "You're not an Angular nor an Express developer. You're a developer."</a></p>
<p>Sure, frameworks are useful for small teams working on a single app. Yes, they'll save you some time (unless you're a <a href="https://snipcart.com/blog/tips-on-code-refactoring-from-a-former-addict" target="_blank">refactoring addict</a>). But what if you have more than one team working on more than one app? Do you really think all team leaders will agree on a single framework for the whole suite of apps? And what if a new "cool kid" framework comes around in 2017?</p>
<p>Problem is: the moment you settle on a framework, you impact <em>every single upcoming engineering decision</em>. Plus, you chain your team to a technology that will probably soon be deprecated. This stuff blows my mind.</p>
<h2>How learning vanilla JavaScript before JS frameworks can—and will—help you</h2>
<p>JavaScript is now <a href="https://w3techs.com/technologies/details/cp-javascript/all/all" target="_blank"><em>the</em> programming language for the web</a>. Understanding its core engineering principles is paramount if you want to build yourself a decent web career. Especially if you're aiming for the front of the pack.</p>
<p>In the past 5 years, more than 10 frontend JS frameworks made the news. Guess how many will do the same in the next 5-10 years? If you're simply <em>pretending</em> to know JavaScript, the engine powering this web revolution, how will you keep up?</p>
<p>Just think about what "jQuery developers" are doing today: trying to catch up on Angular. Tomorrow, they'll be trying to catch up on React. And the sad, depressing loop goes on.</p>
<p><div class="readableLargeImageContainer"><img src="https://snipcartweb-10f3.kxcdn.com/media/9902/javascript-frameworks-popularity.png" alt="javascript-frameworks-popularity" /></div></p>
<p>Knowing vanilla JavaScript will make you actually understand—or even contribute to—JS frameworks, and help you choose the right one <strong><a href="http://www.planningforaliens.com/blog/2016/06/09/when-to-use-a-js-framework/" target="_blank">when you need it</a>.</strong></p>
<p>For me, it brought a lot of positive stuff:</p>
<ul>
<li>It helped me deliver a killer set of client features in a super short timeframe for an Ember app, without knowing jacksh*t about Ember.</li>
<li>It got me a job offer from one of the tech giants because of a very simple library I wrote in my spare time.</li>
<li>It made me identify bugs in libs implementation and suggest simple solutions really quickly.</li>
</ul>
<h3>Takeaways: Learning vanilla JavaScript before JS frameworks</h3>
<p>So here's my TL;DR for you folks:</p>
<ul>
<li>If you don't know the underlying principles of the web, you'll eventually hit a wall thanks to the evolution of the language itself and the constant arrival of new frameworks.</li>
<li>Knowing pure JS will make you a key engineer who can solve complex problems (reason before frantic searching).</li>
<li>It'll make you versatile and productive, both on the front-end and back-end.</li>
<li>It'll give you the toolset to innovate, not just execute.</li>
<li>It’ll guide you on when to use a framework <a href="https://snugug.com/musings/you-probably-shouldnt-use-javascript-framework/" target="_blank">or not</a>.</li>
<li>It'll give you a better general understanding of how browsers and computers work.</li>
</ul>
<p>Using a JS framework can surely bring you somewhere fast. But it won't bring you far if you don't understand the core concepts behind it. Just like learning to play Wonderwall on the guitar won’t teach you how to compose music, but it’ll give you a reason to practice.</p>
<p>And I strongly believe that this "learn the basics/roots first" principle applies to pretty much everything in life. From learning a new programming language to starting a new sport. It requires a lot of practice, but once you master it, the only thing left to do is to get creative with it. And that's where the real fun begins.</p>
<h2>A word on getting started with vanilla JS</h2>
<p>I sure hope I've convinced you to get your hands dirty with plain ol' JavaScript. So if you want to kick ass at web dev and do just that, here's my high-level advice:</p>
<blockquote>
<p>Always be curious, always read the source material, and always try it yourself.</p>
</blockquote>
<p>And some more specific advice:</p>
<ul>
<li>Whenever a new JS lib or framework is trending on Echo JS, Hacker News or GitHub, go on and read the sources.</li>
<li>Every time you write a piece of code, try to think of a plain JS solution that could fit your needs instead of instantly seeking for a lib to integrate.</li>
<li>Go on Stack Overflow and challenge yourself to answer vanilla JS questions on your own.</li>
</ul>
<p>Of course, you should subscribe to useful channels such as <a href="http://www.echojs.com/" target="_blank">Echo JS</a>, <a href="https://news.js.org/" target="_blank">JS news</a>, and <a href="https://ecmascript-daily.github.io/" target="_blank">ECMAScript Daily</a>.</p>
<p>Last but definitely not least, you should also read about the language itself. Classics such as <a href="http://shop.oreilly.com/product/9780596517748.do" target="_blank">JavaScript: The Good Parts</a> and the <a href="https://github.com/getify/You-Dont-Know-JS" target="_blank">You Don't Know JS</a> book series contain tons of value & insights.</p>
<hr />
<p><em>Enjoyed the post? Take a second to <a href="https://twitter.com/home?status=Yes,%20You%20Should%20Learn%20Vanilla%20%23JavaScript%20Before%20Fancy%20JS%20Frameworks%20%3E%20http%3A//buff.ly/2biJUhA%20%23webdevelopment" target="_blank">share it on Twitter</a>! And hit the comments section for questions/suggestions/insults!</em></p>


                
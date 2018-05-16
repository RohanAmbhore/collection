<a href="https://www.nearform.com/blog/architecting-electron-applications-for-60fps/">https://www.nearform.com/blog/architecting-electron-applications-for-60fps/</a><div id="articleHeader"><h1>Architecting Electron Applications for 60fps</h1></div>
            <p><div class="readableLargeImageContainer"><img src="/uploads/versions/electron60fps---x----850-300x---.png" /></div>Electron is a native desktop environment that combines the NodeJS runtime with the Chromium browser. This creates a powerful combination of technologies that allows creating cross-platform applications at a fraction of the cost of other methods.</p>

<p>Despite the many benefits Electron is lauded for, performance often isn’t one of them. In this post we’ll dive deep into optimizations that can (and should) be made to achieve smooth rendering, and a low resource footprint for Electron on all platforms.</p>

<p>We’ll discuss how to optimize the performance of booting & rendering Electron app, and various tools to help you debug performance problems.</p>

<h1 id="booting">Booting</h1>

<p>Before applications can respond to user input, they generally go through an unresponsive period where they are booting up. To provide a snappy user experience, this phase should be reduced to a bare minimum.</p>

<p>Some optimizations are already done when <a href="https://github.com/electron-userland/electron-builder" target="_blank">compiling</a>; for example resolving <code>require()</code> calls ahead of time, so <a href="http://devdocs.io/node/fs#fs_fs_readfilesync_path_options" target="_blank">fs.readFileSync()</a> does not occur while booting. This means that startup performance whilst developing may not always reflect performance in production.</p>

<h2 id="using-domcontentloaded">Using DOMContentLoaded</h2>

<p>Booting itself is defined by a few phases:</p>

<ol>
  <li><strong>loading</strong> - load the resources into the Electron runtime</li>
  <li><strong>interpreting</strong> - convert the static resources into executable code</li>
  <li><strong>executing</strong> - execute the code</li>
</ol>

<p>To achieve high performance while booting, the goal should be to reduce the amount of the work that needs to be done. To quote <a href="https://twitter.com/dominictarr/status/881262182603800576" target="_blank">Dominic Tarr</a>:<em>“Software performance is losing weight not building muscles”</em>.</p>

<p>Probably the most efficient technique to improve boot performance is to wait for the <a href="http://devdocs.io/dom_events/domcontentloaded" target="_blank">‘DOMContentLoaded’</a> event before executing any non-UI critical code. This event fires after the initial set of code is done executing, and before any timers start resolving.</p>

<p><code>'DOMContentLoaded'</code> has the drawback that if a listener is attached after the event has already fired, it will never fire. To circumvent this, it’s recommended to use the <a href="https://github.com/bendrucker/document-ready" target="_blank">document-ready</a> package. This checks the ready state on the page before attaching the listener, and fixes this problem altogether.</p>

<h2 id="prerendering">Prerendering</h2>

<p>Building Electron applications often has the same performance considerations as building websites. More specifically: what works well for websites often also works well for Electron. One of the optimizations that’s particularly interesting to improve boot times is prerendering.</p>

<p>Prerendering is the practice of taking a JavaScript application, and compiling it to static HTML. This means that when booting up the application, the browser process can start painting things on the screen without needing to first interpret, and execute JavaScript. This should significantly improve perceived startup performance, making applications feel way snappier.</p>

<p>As illustrated in this image, it’s only after the JavaScript has loaded that the browser can paint the actual UI - causing the first useful UI to show up around the 900ms mark.</p>

<p><div class="readableLargeImageContainer"><img src="/img/blog/2017/08/electron-sans-pre-render.png" alt="Big chunk of layout after JS execution if you don't prerender" /></div></p>

<p>But if we prerender the HTML and serve it directly, the UI is created about half a second earlier. And on top of that, once the JavaScript has been executed, the second paint is virtually instant because no DOM nodes have to be invalidated. Pretty sweet!</p>

<p><div class="readableLargeImageContainer"><img src="/img/blog/2017/08/electron-with-pre-render.png" alt="Oh neat we're prerendering and UI paints sooner" /></div></p>

<h1 id="rendering">Rendering</h1>

<p>After the application has finished booting, it is ready to respond to outside input. This phase is commonly referred to as the main loop. Optimizations during this phase are usually geared towards reducing resource usage, and scheduling actions efficiently.</p>

<h2 id="compiling-ui-code">Compiling UI code</h2>

<p>To achieve high runtime performance, it’s common to compile browser applications and apply transforms using tools such as <a href="https://github.com/substack/node-browserify" target="_blank">browserify</a>. For example when using <a href="https://github.com/shama/bel" target="_blank">template strings to create DOM nodes</a>,you’ll want to compile it to <a href="https://github.com/shama/yo-yoify/" target="_blank">static <code>document.createElement()</code>calls</a> instead of reparsing HTML on every call. Though this is an example, there are plenty of optimizations that can drastically improve front-end performance.</p>

<p>But because these compilation tools are usually built to make Node code work in the Browser, they don’t necessarily work well for environments such as Electron that can run code directly. Particularly when dealing with Native Addons (e.g.<code>C++</code>) things can get hairy, and debugging them is never fun.</p>

<p>The solution to this problem is fairly straightforward. By separating Browser code from Node code, the browser code can directly be targeted. The most efficient way of doing this, is to use <code>require()</code> for Browser code, and <code>window.require()</code> for Node code:</p>

<div><div><pre><code>// This code will be compiled by Browserify
var foo = require('./bar')

// This code is ignored by Browserify, but picked up at runtime by Electron
var beep = window.require('./boop')
</code></pre></div></div>

<p><em>Note: before arriving at <code>window.require()</code> we’ve experimented with various different approaches. Among others there have been attempts to add C++ support to Browserify, creating separate Node / Browser processes in Electron with shared memory, and variations on the two. In hindsight it was fun to have tried these approaches, but <code>window.require()</code> is about as good as it gets.</em></p>

<h2 id="explicit-scheduling-of-background-tasks">Explicit scheduling of background tasks</h2>

<p>The Browser’s event loop is different from Node’s event loop because it is primarily concerned with providing a smooth visual experience for humans. In practice this means that it must be able to render 60 frames per second, and every frame (or “tick” in Node-speak) has a budget of <code>~16ms</code>.</p>

<p>Every frame in the browser is roughly resolved as follows:</p>

<ol>
  <li>All tasks in the <a href="https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/" target="_blank">microtasks queue</a> resolve.</li>
  <li>All calls to <a href="https://devdocs.io/dom/windoworworkerglobalscope/settimeout" target="_blank">setTimeout()</a>whose timer has expired resolve.</li>
  <li>All queued calls to <a href="https://devdocs.io/dom/window/requestanimationframe" target="_blank">window.requestAnimationFrame()</a>resolve. If <code>requestAnimationFrame()</code> is called during this step, it’s queued for the next frame.</li>
  <li>At this point the browser expects all UI-related tasks to have been resolved, and starts calculating layout, and painting layers on the screen.</li>
  <li>When painting has finished, and there’s likely time left on the frame, the browser starts something called the <a href="https://www.w3.org/TR/requestidlecallback/#start-an-event-loop-s-idle-period" target="_blank">“idle period”</a>. During this phase all queued callbacks from prior <a href="https://devdocs.io/dom/window/requestidlecallback" target="_blank">window.requestIdleCallback()</a> calls are resolved.</li>
</ol>

<p><em>Note: calls to <code>requestIdleCallback()</code> may resolve at a much slower rate (e.g.every 10 seconds) if the window is in the background.</em></p>

<p>From the APIs we mentioned above, <code>window.requestIdleCallback()</code> is probably the most exciting. It allows prioritization of tasks within a single process! This allows us to deprioritize everything that isn’t essential to rendering UI; and allows breaking up CPU intensive tasks into chunks that resolve over multiple frames.</p>

<p>But like with most things, it doesn’t come without drawbacks. Because <em>all</em>callbacks are resolved during the idle period, it requires carefully checking <a href="https://devdocs.io/dom/idledeadline/timeremaining" target="_blank">the time remaining</a> at the start of each call. If there’s not enough time remaining on the tick, the callback should be re-queued onto the next tick. Luckily the <a href="https://github.com/yoshuawuyts/on-idle" target="_blank">on-idle</a> takes care of all that for you:</p>

<div><div><pre><code>var onIdle = require('on-idle')

onIdle(function () {
  console.log("hello from the idle period")
})
</code></pre></div></div>

<h1 id="debugging">Debugging</h1>

<p>So far we’ve talked about what you can do to improve performance of applications. But up front knowledge is only half the work - catching warnings,and acting on them is equally important.</p>

<p><em>Note: At the time of writing, some of these features we’ll be discussing here rely on the beta release Electron 1.7, which uses Chrome 58. The Electron beta can be installed from npm as <code>electron@1.7</code>.</em></p>

<h2 id="toggle-verbose-mode-in-console">Toggle verbose mode in console</h2>

<p>Probably the easiest way of catching performance regressions is by setting the log level to <code>verbose</code> through the new log level dropdown in the console. Once enabled, performance regressions will emit actionable warnings.</p>

<p><div class="readableLargeImageContainer"><img src="/img/blog/2017/08/console-dropdown.png" alt="console log level dropdown" /></div></p>

<h2 id="browser-performance-api">Browser Performance API</h2>

<p>The final tool in the toolbox we’ll be covering today is the <a href="http://devdocs.io/dom/performance_api" target="_blank">DOM Performance API</a>. This API contains all sorts of information about the Browser’s performance, but more importantly, it allows creating measuring the time elapsed between two points, and displays them in the devtool’s timeline.</p>

<p>Now before we continue, it’s worth mentioning Node’s new <a href="https://devdocs.io/node/async_hooks" target="_blank">async_hooks</a> API available in its current form without flags since Node 8.2. Because we’re discussing Electron, we get to choose which API we use to create custom performance entries. Although Node’s API is potent, the Browser’s API is more friendly to use, and has the benefit that it integrates directly with the DevTools.</p>

<p>To create a new <a href="https://devdocs.io/dom/performancemeasure" target="_blank">Performance Measure</a> on the Performance Timeline, <a href="https://devdocs.io/dom/performance/measure" target="_blank">performance.measure(name, firstMark, secondMark)</a> should be called to measure the time spent between two calls to<a href="https://devdocs.io/dom/performance/mark" target="_blank"><code>performance.mark(name)</code></a>. Once a measure has been created, it can be seen on the Performance Timeline under the”User Timing” dropdown.</p>

<p><div class="readableLargeImageContainer"><img src="/img/blog/2017/08/electron-user-timings.png" alt="user timings" /></div></p>

<p>A simpler way of creating these marks is by using the <a href="https://github.com/choojs/nanotiming" target="_blank">nanotiming</a> module:</p>

<div><div><pre><code>var nanotiming = require('nanotiming')

var timing = nanotiming('my-timing.my-loop')
var i = 1000
while (--i) console.log(i)
timing()
</code></pre></div></div>

<p>Sometimes it can be useful to act on <a href="https://devdocs.io/dom/performanceentry" target="_blank">PerformanceEntries</a>. For example: you might want to send them back to a server for later inspection, or log them out during debugging to catch performance problems early.</p>

<p>While there are several APIs that allow retrieving Performance Entries, the <a href="https://devdocs.io/dom/performanceobserver" target="_blank">PerformanceObserver API</a> is by far the most powerful. However, one of the downsides of using it is that it only starts emitting events <em>after</em> the observer has been created. To react to these events, we recommend using the <a href="https://github.com/yoshuawuyts/on-performance" target="_blank">on-performance</a> module. Not only does it retrieve all Performance Entries once it’s attached, it also clears them from the <a href="https://devdocs.io/dom/performance/onresourcetimingbufferfull" target="_blank">Browser’s internal timing buffer</a> so new events can keep flowing in without overflowing the buffer.</p>

<div><div><pre><code>var onPerformance = require('on-performance')

onPerformance(function (entry) {
  console.log('entry: ', entry.entryType, entry)
})
</code></pre></div></div>

<h2 id="wrapping-up">Wrapping up</h2>

<p>In this post we’ve touched on the different aspects of Electron’s performance,how to design code in such a way that it can be optimized, and discussed various APIs that can help with improving performance.</p>

<p>Let us know what you think in the comments below, or drop <a href="https://twitter.com/nearform" target="_blank">Nearform</a> or <a href="https://twitter.com/yoshuawuyts" target="_blank">Yosh</a> a line on Twitter. Cheers!</p>

            

<div>
  <a href="https://cta-service-cms2.hubspot.com/ctas/v2/public/cs/c/?cta_guid=8c74e87b-af7d-4b20-bde9-84ff7620c253&placement_guid=acaccca3-8c8b-490b-b4bb-cf76c73c7c44&portal_id=1964953&redirect_url=APefjpFS2FOXbPLcIGHZCG5gNBitNw1MFTqZa2S0cJ8oGI1eLh7zYfQ2mpY7Q2uCOmnOALp8jGmRQFlepQIO0zQMRxcLnvx5q5vO-KaUYEinTcZ3z6r7hq3HyqaDO07vZljE4Ud4l6u5pdfV95Vo9dYlmAtMTl73_1DAjr_lIuh9goD5MDpFyuuKDv6uLsJJmvwMPBS0AxqRXQ2_usaIRRO_hIJJ852QQg&hsutk=b357cbfa40447e24c727806e0173d59f&canon=https%3A%2F%2Fwww.nearform.com%2Fblog%2Farchitecting-electron-applications-for-60fps%2F&click=c34484d1-4097-44e0-bbd6-be415d2df1e7&utm_referrer=https%3A%2F%2Fwww.google.com%2F&__hstc=67462030.b357cbfa40447e24c727806e0173d59f.1526453040144.1526453040144.1526453040144.1&__hssc=67462030.1.1526453040145&__hsfp=2574385306" id="cta_button_1964953_8c74e87b-af7d-4b20-bde9-84ff7620c253" target="_blank" class="readableLinkWithMediumImage"><img src="https://cdn2.hubspot.net/hubfs/1964953/hub_generated/resized/073336f2-f133-4b22-b7a5-e49775a407c3.png" alt="New Call-to-action" id="hs-cta-img-acaccca3-8c8b-490b-b4bb-cf76c73c7c44" /></a>
</div>



          
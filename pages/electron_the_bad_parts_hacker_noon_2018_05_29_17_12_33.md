<a href="https://hackernoon.com/electron-the-bad-parts-2b710c491547">https://hackernoon.com/electron-the-bad-parts-2b710c491547</a><div id="articleHeader"><h1>🦋Electron: The Bad Parts</h1></div><p id="571e">Most cross platform programming languages and frameworks contain good and bad parts. Electron probably has more than its share of the good — but also hides some dark secrets under its shining facade.</p><figure id="3c66"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*BYeFTcHFVhZAhOq_-Y_m1Q.jpeg?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/1*BYeFTcHFVhZAhOq_-Y_m1Q.jpeg" /></div></figure><p id="9c98">While the first impression of Electron might be that it solves all the problems related to cross platform development the reality is that many things won’t work out of the box and they probably can’t. It took me quite some time to understand this, and it took even more time until I had all the DIY solutions in place to provide users with things like correct installers, updates, a feedback mechanism.</p><figure id="2400"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*_WZ2Su4hO0rlFduDVRxjlw.png?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/1*_WZ2Su4hO0rlFduDVRxjlw.png" /></div><figcaption>This list of features on the Electron webpage is setting high expectations</figcaption></figure><p id="b0f5">I’m a big fan of Electron and thought the following list could be very helpful for people who are new to the topic. But project managers who are evaluating different stacks and want to avoid “surprises” should benefit as well. The list presents things that are not completely clear in the beginning. Things where it’s worth to spend some extra time on evaluation before a decision and long term commitment is made.</p><h3 id="7ac4">Installers</h3><p id="b347">Once the coding is over and the release planning starts, the first tough decision is waiting. One can either use the installer and update mechanism as described in the Electron documentation or use the installer and update mechanism that one of the best builder tools (electron-builder) recommends.</p><figure id="823d"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/0*aK7Jg1QPDqe_RdPL.?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/0*aK7Jg1QPDqe_RdPL." /></div></figure><p id="fd7f">The <a href="https://electron.atom.io/docs/api/auto-updater/" target="_blank">official Electron documentation</a> suggests the Squirrel (Windows and Mac) installer and the built-in autoUpdater. An open source <a href="https://github.com/GitbookIO/nuts" target="_blank">release server (“Nuts”)</a> is available which handles the server side management of updates and releases.</p><p id="b3e9">The other option is <a href="https://www.electron.build/auto-update" target="_blank">electron-builder’s own update mechanism</a> “electron-updater”. It is based on the established NSIS installer (Windows) and plain old mac packages. electron-builder uses this approach as the default setting for all generated installers.</p><blockquote id="2547"><a href="https://github.com/electron-userland/electron-builder/issues/837" target="_blank">“Quite frankly switching to NSIS by default seems like a very drastic move considering the Electron project still recommends Squirrel for Windows.”</a></blockquote><p id="54c2">The Electron and electron-builder project do very much disagree on which solution is better. This leads to a tricky situation where devs have to decide between one official solution (which many consider to be complicated and not flexible enough) and a simple and powerful one that has built-in tool support. Personally, I think electron-builder is a blessing if you actually plan to provide installations of your software to millions of people around the world and you don’t know where to start. It can save you weeks if not months of development and I would consider it to be an essential part of the ecosystem.</p><p id="9cf2">Here is a list of pros <a href="https://www.electron.build/auto-update" target="_blank">from the electron-builder/electron-updater docs</a> that should be considered before one solution is chosen over the other:</p><ul><li id="8400">It doesn’t require a dedicated release server.</li><li id="ed1d">Code signature validation not only on macOS, but also on Windows.</li><li id="e5a7">electron-builder produces and publishes all required metadata files and artifacts.</li><li id="ab3e">Download progress supported on all platforms, including macOS.</li><li id="4f22"><a href="https://www.electron.build/auto-update#staged-rollouts" target="_blank">Staged rollouts</a> supported on all platforms, including macOS.</li><li id="3a39">Actually, built-in autoUpdater is used inside on macOS.</li><li id="a9a3">Different providers supported out of the box (GitHub, Bintray, Amazon S3, generic HTTP(s) server).</li><li id="5792">You need only 2 lines of code to make it work.</li></ul><h3 id="a1c1">Continuous Integration (CI) & Multi Platform Builds</h3><p id="95c0">Electron should not be confused with a pre-installed “Java virtual machine”. You will have to make (build, sign, distribute) your app cross platform. It won’t be cross platform “automatically”.</p><figure id="3d7c"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/0*WMsq_uI0pTnauBUs.jpg?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/0*WMsq_uI0pTnauBUs.jpg" /></div></figure><figure id="5e00"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*MPJvWpcpWWs3vjqy9WF5qA.png?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/1*MPJvWpcpWWs3vjqy9WF5qA.png" /></div><figcaption><a href="https://www.electron.build/multi-platform-build" target="_blank">From the electron-builder documentation</a></figcaption></figure><p id="a855">This can be quite confusing and shocking, but cheap and easy multi platform builds are a myth. It is almost ironical how often one will find “cross platform” Electron applications that are “only for Mac” or “only for Windows”. The reason is not that it’s complicated to write code for multiple platforms (Electron handles it amazingly well and the documentation is clear). The reason is simply that many developers do not have the big budget or access to other hardware to test and build on. Even worse: if you plan to be a “legitimate developer” your app needs to be signed and it might have one or more native dependencies.</p><p id="0da3">The recommended solution in these cases is to get accounts for different CI providers: one for Mac (and Linux) and one for Windows. Why? Because Apple officially prohibits the use of their operating systems</p><ul><li id="20fa">in Virtual Machines on Non-OS X systems</li><li id="872b">on non-Apple Hardware</li></ul><p id="127a">The result is that if your app is closed source it will cost twice as much to build for two OS. And if money and a complex build system is not and issue, you still have the issue that the app will only be tested and built on multiple systems. At this point it cannot be shipped yet. Signing your app remotely with an Extended Validation (EV) code signing certificate for example is pretty much impossible with all existing CI tools available since your certificate is bound to a physical hardware token which cannot / should not be transferred.</p><p id="2aea">The fact that each application comes with its own version of Chromium (the 20 million LOC, ~30MB [packaged] Web runtime) is one of the most criticised aspects. Fun fact: if you would decide today to build your own simplified competitor version from scratch it would probably take you <a href="https://www.openhub.net/p/chrome/estimated_cost" target="_blank">5,099 years to build</a>. Some have tried to <a href="https://medium.com/dailyjs/put-your-electron-app-on-a-diet-with-electrino-c7ffdf1d6297" target="_blank">put Electron on diet</a> and critics say it creates the feeling of installing a full operating system on top of an operating system. Every time.</p><figure id="a399"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*haylJPT34Tczd74NBzHapA.png?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/1*haylJPT34Tczd74NBzHapA.png" /></div><figcaption>not an issue</figcaption></figure><p id="41a3">While many people would expect Chromium to drastically slow down the performance or “consume precious RAM” I haven’t experienced any of this in practice and haven’t heard bad feedback from thousands of test users. I guess it isn’t such a big issue if you are used to have the Chrome browser running in background anyways. But here is the thing:</p><p id="3b08">Not just installations bundle Chromium. <strong>Every update</strong> also comes with Chromium, Node and all the other Electron components unless the update is designed as delta or differential update.</p><h3 id="6963">Delta Updates</h3><p id="9816">Everyone who’s experienced a Windows update knows that updates suck! But they don’t have to. Updates can introduce cool new stuff, don’t have to interrupt the workflow and they can happen in the background instead of blocking your machine for one hour — I’m looking at you Microsoft. The 🔑 is “delta updates”. Instead of uninstalling and re-installing everything, only the relevant parts should be updated incrementally.</p><figure id="efbd"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/0*OMe50c8sv3BL6YsG.jpg?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/0*OMe50c8sv3BL6YsG.jpg" /></div><figcaption>The challenge: how to switch versions without the user noticing it (inspired by <a href="https://www.amazon.com/Developing-Electron-Edge-edge-Book-ebook/dp/B01G7TTKSK" target="_blank">Developing an Electron Edge</a>)</figcaption></figure><p id="1f5f">Imagine the example <a href="https://arcath.net/2016/11/squirrel-release-server/" target="_blank">from this blog</a>: A class of students is trying out a software and the update is 70MB big. 30 people start their computers and get presented with an update. They download the update simultanously resulting in 2.1GB. Now, compare this to a delta update, handled in background, which is only 100KB in size and brings down the initial 2.1GB to 3MB total. It will shorten the time each student is waiting for the update to write itself to disk, to register with the system after the download; and it takes load from servers, saves bandwith, saves $$$, creates happy students and teachers.</p><p id="09dd">Squirrel, in theory, supports delta updates. As of last week, <a href="https://github.com/electron-userland/electron-builder/issues/1523" target="_blank">electron builder with NSIS provides a beta solution for this too.</a> However, I wouldn’ call either one of them to be available out of the box.</p><p id="a353">One of the applications I’m working on — <a href="http://www.autobeatplayer.com/" target="_blank">Autobeat Player </a>— uses its own “delta” update mechanism which updates <strong>the whole app</strong>. The twist: the whole application without external modules and libraries is only ~750KB(!) in size. Whenever I mention this, the reactions are priceless. Most people cannot believe the small size considering the feature richness and complexity of the application. A whole desktop application that has the size of a single image is how I would describe a new generation of (Electron) desktop apps. And the way we’ve implemented updates in Autobeat is straighforward and no rocket science.</p><p id="49c6"><strong>Everything that can be remotely considered static is not part of the application image</strong>: jQuery, Font Awesome, Bootstrap, or all the other frontend libraries and any of the node modules <strong>are not part of the app</strong> itself.</p><p id="86ec">If one strips everything that is not frequently changing such as these libraries and only updates the app logic part — the things you’re actually working on — a 99.9% size decrease is absolutely possible. However, it requires custom update logic. There is no standard solution available. The benefit: in Autobeat’s case we can update the app as a whole as long as external dependencies are not changing which rarely happens. Updates take between 1–2 seconds and go often unnoticed. It is like updating a website — after a refresh it looks different. No need to worry that the deltas are miscalculated or parts are not working together as expected. Once in a while we add more dependencies and have to do a ”full” 31MB update. But we’re making a long term bet here, assuming that these intervals get longer and longer while our regular release cycles can be as short as a couple of hours. And everyday we are learning more about how to leverage things that work for the Web and how to bring them to desktop to release more efficiently.</p><h3 id="b32e">Security</h3><p id="fe29">The separation between app logic and libraries as described above unlocks another very powerful feature: it potentially allows to release a second app, which shares the same, existing core libraries and does not require the installation of another Chromium bundled package or the need to signand distribute a new installer. It creates an environment like a super-powered browser that supports jQuery, Vue, Font Awesome, Polymer and every other framework as well as all relevant node modules out of the box and minimizes the app’s size. Think about it for a second.</p><p id="b3d3">In recent tests, our team has successfully launched other “instant apps” (&lt;1MB) in a distributed, P2P fashion in a fraction of a second. In the same way one would start apps on a Chromecast powered TV, it is also possible to remotely load apps on other machines. When I realized that we had just launched a fully featured desktop software from a web server running on a smartphone it partly felt like creating the next generation of decentralised apps and partly like the next generation of viruses.</p><p id="6bb8">In the same way that browsers are able to load any website, Electron potentially can load as many apps as it wants without the need to re-install the runtime over and over again. And the more the line between Web and desktop gets blurred, the more challenges we face as users to protect our machines and data.</p><p id="a195">Electron can also load websites just like any other browser. There are even tools like the extremely popular <a href="https://github.com/jiahaog/nativefier" target="_blank">nativefier</a> that wrap existing websites. These “native-website-apps” can potentially activate the webcam or microphone, access the filesystem and create, delete, encrypt things as they wish, or send them to servers — and most of the time this is intended. Eventually, the hosting server becomes the command and control server of a gigantic botnet.</p><blockquote id="5101"><a href="https://blog.dcpos.ch/how-to-make-your-electron-app-sexy" target="_blank"><strong>“Once you get your first million users, your auto updater is basically a botnet with a million nodes. </strong>With great power comes great responsibility.</a>”</blockquote><p id="5e89">Electron provides many protection mechanisms: The sandbox model can be activated, node integration can be turned off, preload scripts and webviews create local environments with different permissions... However, it concerns me that these desktop web apps evolve and distribute faster than our old security models. Things like installer signing and trusted authorities are in the process of becoming meaningless in a world where websites can be run as full-fledged apps outside their sandbox.</p><figure id="be22"><div><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/1*tIv06rY_ykD9vauKWI4KbA.png" /></div><figcaption>“every time you download express, you favorite this exact tweet from Hot Pockets” — <a href="https://medium.com/friendship-dot-js/i-peeked-into-my-node-modules-directory-and-you-wont-believe-what-happened-next-b89f63d21558" target="_blank">satire by Jordan Scales</a></figcaption></figure><p id="450f">Recently, I was attending a talk from a well-funded startup that scans and analyzes npm modules for vulnerabilities to warn developers before they integrate them. When I asked if they would also consider npm module security in a desktop context the answer was that they haven’t looked into it and that it has no priority. But every module that we reference and install on a user’s machine comes with its own dependencies and we end up sharing the user’s trust and permissions with modules we lose track of and often don’t even know. In a time where a single cyber attack such as the recent WannaCry ransomware can have a financial impact <a href="http://www.cbsnews.com/news/wannacry-ransomware-attacks-wannacry-virus-losses/" target="_blank">as high as $4 billion</a>, we are facing complete new challenges. <a href="https://medium.com/friendship-dot-js/i-peeked-into-my-node-modules-directory-and-you-wont-believe-what-happened-next-b89f63d21558" target="_blank">This gets especially concerning when you read about popular modules that retweet hot pocket ads in the background every time they are </a>installed.</p><h3 id="1963">Code Protection</h3><p id="732a">In the same way we want to protect users we might also want to protect our own and our company’s work. Electron apps are usually distributed in asar container files. To retrieve the plain source code from an installation and its contained asar file is as simple as:</p><p id="aca4"><code>asar extract app.asar secret_source_code</code></p><p id="f341">Files don’t get obfuscated, encrypted or protected by default which means someone who wants to temper with an app can pretty much receive the working copy of the repository. This makes Electron a very poor fit for commercial solutions.</p><p id="fc1d"><a href="https://github.com/electron/electron/issues/3041" target="_blank">The official Electron statement reads like this</a>:</p><figure id="f4a3"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*leRvgOnxH6NYyLr7ysUdmQ.png?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/1*leRvgOnxH6NYyLr7ysUdmQ.png" /></div></figure><p id="0fb1">The idea is that any sort of built-in protection can be bypassed anyways (which is true) and would just steal resources from more important areas (which is true).</p><p id="b80f">Our products use a couple of obfuscation and encryption techniques and are definitely not as sensitive as say <a href="https://github.com/ethereum/mist/releases" target="_blank">your Ethereum tokens</a>. But many struggle with protection so here is one simple example to achieve source code encryption during packaging:</p><pre id="8913">const crypto = require('crypto')<br />var password = new Buffer(‘my secret password’);<br />function transform(filename) {<br /> return crypto.createCipher(‘aes-256-cbc’, password);<br />}<br />asar.createPackageWithOptions(src, dest, { transform: transform }..)</pre><p id="4abf">Asar’s transform option allows to specify a stream transformer that is applied when the files are packed into the asar container. However at some point you will have to decrypt your files and this is where it gets really tricky. Also, if your static password leaks you’re not winning anything. There are other options like creating a V8 snapshot or to use C++ binaries and one can definitely make it their “battle” as much as they want. The main takeaway here is that Electron provides close to no protection and every minute that you invest in security hopefully creates 5 minutes for a hacker.</p><p id="80ba">If you have an Electron app yourself and you liked the article, would like to get another perspective, or if you think that something is missing, presented in the wrong way or inaccurate, please leave a comment, clap or contact me.</p><p id="c31f">To keep this article “short”, I’m thinking about compiling additional and more detailed material. Additional topics could be crash reporting, separation of main and renderer process logic, analytics, installer distribution, campaign tracking and reengaging users through notifications. If you are generally interested in more information please let me know:</p><figure id="8e65"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Flh5.googleusercontent.com%2FO8lnjS_iAN-deQZZTeXZbC0vmqafdpRSOLIuDLKIuywA0KBBNqFmnpJbK80mhk4iF9E%3Dw1200-h630-p&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><p id="d6ef">Link to form: <a href="https://goo.gl/forms/cnXgxM8fmg60f4lX2" target="_blank">https://goo.gl/forms/cnXgxM8fmg60f4lX2</a></p><h3 id="f114">Links</h3><p id="9821">Good electron overview guide: <a href="https://blog.dcpos.ch/how-to-make-your-electron-app-sexy" target="_blank">https://blog.dcpos.ch/how-to-make-your-electron-app-sexy</a></p><p id="48ae">electron-builder: <a href="https://github.com/electron-userland/electron-builder" target="_blank">https://github.com/electron-userland/electron-builder</a></p><p id="c043">Official updater docs: <a href="https://electron.atom.io/docs/api/auto-updater/" target="_blank">https://electron.atom.io/docs/api/auto-updater/</a></p><p id="de08">electron-updater: <a href="https://www.electron.build/auto-update" target="_blank">https://www.electron.build/auto-update</a></p><p id="b5ba">Squirrel to NSIS migration: <a href="https://github.com/electron-userland/electron-builder/issues/837" target="_blank">https://github.com/electron-userland/electron-builder/issues/837</a></p><p id="2f6d">Multi platform builds: <a href="https://www.electron.build/multi-platform-build" target="_blank">https://www.electron.build/multi-platform-build</a></p><p id="d48d">electron-builder delta update support: <a href="https://github.com/electron-userland/electron-builder/issues/1523" target="_blank">https://github.com/electron-userland/electron-builder/issues/1523</a></p><p id="cce0">Source code protection: <a href="https://github.com/electron/electron/issues/3041" target="_blank">https://github.com/electron/electron/issues/3041</a></p>
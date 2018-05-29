<a href="https://drewdevault.com/2016/11/24/Electron-considered-harmful.html">https://drewdevault.com/2016/11/24/Electron-considered-harmful.html</a><div id="articleHeader"><h1>                        Electron considered harmful        </h1></div>
        
        <p>
            Published 2016-11-24
            on <a href="/" target="_blank">Drew DeVault's blog</a>
            
              —
              <a href="/2016/11/24/Electron-considered-harmful.html" target="_blank">
                Permalink
              </a>
            
        </p>
        
        
          <p>Yeah, I know that “considered harmful” essays are allegedly <a href="http://meyerweb.com/eric/comment/chech.html" target="_blank">considered
harmful</a>. If it surprises you that
I’m writing one, though, you must be a new reader. Welcome! Let’s get started.
If you’re unfamiliar with Electron, it’s some hot new tech that lets you make
desktop applications with HTML+CSS+JavaScript. It’s basically a chromeless web
browser with a Node.js backend and a Chromium-based frontend. What follows is
the rant of a pissed off Unix hacker, you’ve been warned.</p>

<p>As software engineers we have a responsibility to pick the <em>right</em> tools for the
job. In fact, that’s the <em>most important</em> choice we have to make when we start a
project. When you choose Electron you get:</p>

<ul>
  <li>An entire copy of Chromium you’ll be shipping with your app</li>
  <li>An interface that looks and feels nothing like the rest of the user’s OS</li>
  <li>One of the slowest, least memory efficient, and most inelegant GUI application
  platforms out there (remember, we <em>tolerate</em> frontend web development because
  we have no choice, not because it is by any means <em>good</em>)</li>
</ul>

<p>Let’s go over some case studies.</p>

<p><strong><a href="https://github.com/mifi/lossless-cut" target="_blank">lossless-cut</a></strong> is an Electron app that
gives you a graphical UI for <em>two ffmpeg flags</em>. Seriously, the flags in
question are -ss and -t. No really, that’s <em><a href="https://github.com/mifi/lossless-cut/blob/master/src/ffmpeg.js#L46" target="_blank">literally all it
does</a></em>. It
doesn’t even use ffmpeg to decode the video preview in the app, it’s limited to
the codecs chromium supports. It also ships its own ffmpeg, so it has the
industry standard video decoding tool <em>right there</em> and doesn’t use it to render
video. For the price of 200 extra MiB of disk space and an entire Chromium process
in RAM and on your CPU, you get a less capable GUI that saves you from having to
type the -ss and -t flags yourself.</p>

<p><strong><a href="http://1clipboard.io/" target="_blank">1Clipboard</a></strong> is a clipboard manager. In Electron. A
<em>clipboard manager</em>. In order to show you <em>a list of things you’ve copied</em>, it
uses <em>an entire bundled copy of Chromium</em>. Also note that despite the promises
of Electron making cross platform development easy, it doesn’t support Linux.</p>

<p><strong><a href="https://getcollectie.com/" target="_blank">Collectie</a></strong> is a… fancy bookmark manager, I
guess? Another one that fails to get the cross platform value add from Electron,
this only supports OS X (or is it macOS). For only $10 bucks you get to organize
your shit into folders. Or you could just open the Finder for free and get a
native UX to boot.</p>

<p>This is a <a href="https://hyper.is/" target="_blank">terminal</a> written with Electron. On the landing
page they say “# A terminal emulator 100% based on JavaScript, HTML, and CSS”
like they’re proud of it. They’ve taken one of the most lightweight and
essential tools on your computer and bloated it by orders of magnitude. Why the
fuck would you want to render Google in your god damn terminal emulator? Bonus:
also not cross platform.</p>

<p>This is not to mention the dozens of companies that have taken their websites
and crammed them into a shitty electron app and called it their desktop app.
Come on guys!</p>

<p>By the way, if you’re the guy who’s going to leave a comment about how this blog
post introduced you to a bunch of interesting apps you’re going to install now,
I hate you.</p>

<h2 id="electron-enables-lazy-developers-to-write-garbage">Electron enables lazy developers to write garbage</h2>

<p>Let me be clear about this: JavaScript sucks. It’s not the worst, but it’s also
not by any means good. ES6 is a really great step forward and I’m thrilled about
how much easier it’s going to be to write JavaScript, but it’s still JavaScript
underneath the syntactic sugar. We use it because we have no choice (people who
know more than just JavaScript know this). The object model is whack and the
loose typing is whack and the DOM is super whack.</p>

<p>When Node.js happened, a bunch of developers who never bothered to learn more
than JavaScript for their frontend work suddenly could write their crappy code
on the backend, too. Now this is happening to desktop applications. The reason
people choose Electron is because they are <em>too lazy</em> to learn the right tools
for the job. This is the <em>worst</em> quality a developer can have. You’re an
engineer, for the love of God! Fucking act like one! Do they build square
airplanes so they don’t have to learn about aerodynamics, then just throw on an
extra ten engines to make up for it? NO!</p>

<p>For the love of God, learn something else. Learn how to use GTK or Qt. Maybe Xwt
is more up your alley. How about GNOME’s Vala thing? <em>Learn another programming
language</em>. Learn Python or C/C++ or C#. Fun fact: it’ll make your JavaScript
better, and once you have it in your toolbox you can make more educated
decisions on the appropriate tool to use when you face your next problem. Hint:
it’s not Electron.</p>

<h2 id="some-electron-apps-dont-suck">Some Electron apps don’t suck</h2>

<p>For some use-cases Electron is a reasonable choice.</p>

<ul>
  <li><a href="https://code.visualstudio.com/" target="_blank">Visual Studio Code</a>, because it’s a full
  blown IDE with a debugger and plugins and more. It’s already gonna be
  bloated.</li>
  <li><a href="http://www.soundnodeapp.com/" target="_blank">Soundnode</a>, because it’s not like any other
  music service’s app obeys your OS’s UI conventions</li>
</ul>

<p>Uh, that’s it. That’s the entire list.</p>


        
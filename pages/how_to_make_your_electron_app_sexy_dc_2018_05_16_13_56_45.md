<a href="https://blog.dcpos.ch/how-to-make-your-electron-app-sexy">https://blog.dcpos.ch/how-to-make-your-electron-app-sexy</a><div id="articleHeader"><h1><a href="http://blog.dcpos.ch/how-to-make-your-electron-app-sexy" target="_blank">How To Make Your Electron App Sexy</a></h1></div>

  
    
      <p>Electron is excellent.</p><p>There's a long history of ways to package HTML and Javascript into an installed desktop app. The result usually feels like a web app detached from the rest of the OS.</p><p><b>Electron makes it easy to do better.</b></p><div id="posthaven_gallery[1067855]">
          <div>
                    <p>
          <div class="readableLargeImageContainer"><img src="https://phaven-prod.s3.amazonaws.com/files/image_part/asset/1721700/NsPg9NIh2pBqFyQSAPpn4y1U9H8/medium_Screen_Shot_2016-06-11_at_8.53.38_PM.png" /></div>
        </p>

          </div>
          
        </div>
<p>Electron exposes lots of deep OS integrations thru simple Javascript APIs, so you can have a single clean codebase instead of having to code against three different C++ and Objective C libraries for Windows, Linux, and Mac.</p><p>Using <b>npm</b> and <b>electron-prebuilt</b>, you can also keep your build simple and clean. No node-gyp, no native compilation at all. Things that are a pain in most environments, like installers and automatic updates for multiple platforms, are easy here.</p><p><a href="https://feross.org" target="_blank">Feross</a> and I used Electron to make WebTorrent Desktop recently. We were surprised by Electron's quality and attention to detail.</p><div id="posthaven_gallery[1068456]">
          <div>
                    <p>
          <div class="readableLargeImageContainer"><img src="https://phaven-prod.s3.amazonaws.com/files/image_part/asset/1722691/HxMEI2g3ZOhnJwAWNLQx0jl68HM/medium_Screen_Shot_2016-06-13_at_7.42.07_PM.png" /></div>
        </p>

          </div>
          
        </div>
<p><b>Here's a list of things you can do to make your Electron app feel native and pro.</b></p><p>(<b>If you're new to Electron, check out the <a href="https://github.com/electron/electron/blob/master/docs/tutorial/quick-start.md" target="_blank">Quick Start</a>. </b>First things first! This post is for people who already know Electron, but want to make their apps even better.)</p><h1><b>The List</b></h1><ul>
<li>Dock and tray integration</li>
<li>Notifications</li>
<li>Menus</li>
<li>Shortcuts</li>
<li>Drag and drop</li>
<li>Crash reporting</li>
<li>Signed installers for all three platforms</li>
<li>Automatic updaters for Mac and Windows</li>
<li>Fast startup</li>
<li>One-step build</li>
</ul><p><b>WebTorrent Desktop implements 10 / 10.</b></p><p><b>How does your app score?</b></p><h1><b>Dock and tray integration</b></h1><p><b>On Windows and Linux, you can minimize to tray.</b></p><p>(You can do it on Mac too, but you probably don't need to since Mac has the dock.)</p><p>This is great for running in the background or running automatically on system startup.</p><p><b>If you're making a decentralized app, you probably want to do this to keep your network healthy.</b></p><p><b>On a Mac, integrate with the dock.</b></p><div id="posthaven_gallery[1067834]">

          <div>
                    <p>
          <div class="readableLargeImageContainer"><img src="https://phaven-prod.s3.amazonaws.com/files/image_part/asset/1721676/G6j4ddmxtya2Ny9qYP9ekh2f_ZU/medium_Screen_Shot_2016-06-11_at_7.00.52_PM.png" /></div>
        </p>

          </div>
          
        </div>
<p>Show a progress bar when the user might be waiting for something to finish.</p><p>Show a badge when work finishes while your app is in the background.</p><div id="gist36754104">
    <div>
      <div>
        <div>
  <div id="file-electron-dock-js">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-electron-dock-js-L1"></td>
        <td id="file-electron-dock-js-LC1">const win = new electron.BrowserWindow(...)</td>
      </tr>
      
      <tr>
        <td id="file-electron-dock-js-L3"></td>
        <td id="file-electron-dock-js-LC3">// When work makes progress, show the progress bar</td>
      </tr>
      <tr>
        <td id="file-electron-dock-js-L4"></td>
        <td id="file-electron-dock-js-LC4">function onProgress (progess) {</td>
      </tr>
      <tr>
        <td id="file-electron-dock-js-L5"></td>
        <td id="file-electron-dock-js-LC5">  // Use values 0 to 1, or -1 to hide the progress bar</td>
      </tr>
      <tr>
        <td id="file-electron-dock-js-L6"></td>
        <td id="file-electron-dock-js-LC6">  win.setProgressBar(progress || -1) // Progress bar works on all platforms</td>
      </tr>
      
      
      <tr>
        <td id="file-electron-dock-js-L9"></td>
        <td id="file-electron-dock-js-LC9">// When work completes while the app is in the background, show a badge</td>
      </tr>
      <tr>
        <td id="file-electron-dock-js-L10"></td>
        <td id="file-electron-dock-js-LC10">var numDoneInBackground = 0</td>
      </tr>
      <tr>
        <td id="file-electron-dock-js-L11"></td>
        <td id="file-electron-dock-js-LC11">function onDone () {</td>
      </tr>
      <tr>
        <td id="file-electron-dock-js-L12"></td>
        <td id="file-electron-dock-js-LC12">  var dock = electron.app.dock // Badge works only on Mac</td>
      </tr>
      <tr>
        <td id="file-electron-dock-js-L13"></td>
        <td id="file-electron-dock-js-LC13">  if (!dock || win.isFocused()) return</td>
      </tr>
      <tr>
        <td id="file-electron-dock-js-L14"></td>
        <td id="file-electron-dock-js-LC14">  numDoneInBackground++</td>
      </tr>
      <tr>
        <td id="file-electron-dock-js-L15"></td>
        <td id="file-electron-dock-js-LC15">  dock.setBadge('' + numDoneInBackground)</td>
      </tr>
      
      
      <tr>
        <td id="file-electron-dock-js-L18"></td>
        <td id="file-electron-dock-js-LC18">// Subscribe to the window focus event. When that happens, hide the badge</td>
      </tr>
      <tr>
        <td id="file-electron-dock-js-L19"></td>
        <td id="file-electron-dock-js-LC19">function onFocus () {</td>
      </tr>
      <tr>
        <td id="file-electron-dock-js-L20"></td>
        <td id="file-electron-dock-js-LC20">  numDoneInBackground = 0</td>
      </tr>
      <tr>
        <td id="file-electron-dock-js-L21"></td>
        <td id="file-electron-dock-js-LC21">  dock.setBadge('')</td>
      </tr>
      
</tbody></table>


  </div>

  </div>
</div>

      </div>
      
    </div>
</div><b>Caveat: </b>only some Linux distros support the tray correctly. Check that you're on one of them--otherwise, your users will have no way to quit your program if you hide the window and your tray icon doesn't show up. See <a href="https://github.com/feross/webtorrent-desktop/blob/8ac42078d49adfa4b9821632e6a1b4a622ac69e2/main/tray.js#L57" target="_blank">checkElectronTraySupport</a> for a workaround.<h1><b>Notifications</b></h1><p>Desktop notifications work on all three platforms. They're really easy to use.</p><p>Stay concise. Don't go over 256 characters, or your message will be truncated on Mac OS.</p><div id="posthaven_gallery[1067835]">
          <div>
                    <p>
          <div class="readableLargeImageContainer"><img src="https://phaven-prod.s3.amazonaws.com/files/image_part/asset/1721681/2zw7Mnlgs6YvAM6niXYSmjiPYZw/medium_Screen_Shot_2016-06-11_at_7.18.05_PM.png" /></div>
        </p>

          </div>
          
        </div>
<p>Here's an example with custom sounds: a satisfying "ding!" whenever a file finishes downloading.</p><div id="gist36701149">
    <div>
      <div>
        <div>
  <div id="file-electron-notification-js">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-electron-notification-js-L1"></td>
        <td id="file-electron-notification-js-LC1">// Do this from the renderer process</td>
      </tr>
      <tr>
        <td id="file-electron-notification-js-L2"></td>
        <td id="file-electron-notification-js-LC2">var notif = new window.Notification('Download Complete', {</td>
      </tr>
      <tr>
        <td id="file-electron-notification-js-L3"></td>
        <td id="file-electron-notification-js-LC3">  body: torrent.name,</td>
      </tr>
      <tr>
        <td id="file-electron-notification-js-L4"></td>
        <td id="file-electron-notification-js-LC4">  silent: true // We'll play our own sound</td>
      </tr>
      
      
      <tr>
        <td id="file-electron-notification-js-L7"></td>
        <td id="file-electron-notification-js-LC7">// If the user clicks in the Notifications Center, show the app</td>
      </tr>
      <tr>
        <td id="file-electron-notification-js-L8"></td>
        <td id="file-electron-notification-js-LC8">notif.onclick = function () {</td>
      </tr>
      <tr>
        <td id="file-electron-notification-js-L9"></td>
        <td id="file-electron-notification-js-LC9">  ipcRenderer.send('focusWindow', 'main')</td>
      </tr>
      
      
      <tr>
        <td id="file-electron-notification-js-L12"></td>
        <td id="file-electron-notification-js-LC12">// Play a sound using the standard HTML5 Audio API</td>
      </tr>
      <tr>
        <td id="file-electron-notification-js-L13"></td>
        <td id="file-electron-notification-js-LC13">sound.play('DONE')</td>
      </tr>
</tbody></table>


  </div>

  </div>
</div>

      </div>
      
    </div>
</div>
<p>Play sounds using the normal web audio API. You'll want to preload them. <a href="https://github.com/feross/webtorrent-desktop/blob/f0315f7f77d03a5accc368c4bb35067eb15e6d04/renderer/lib/sound.js" target="_blank">Here's a nice way to do that</a>.</p><h1><b>Menus</b></h1><p>Electron gives you nice declarative menus on all three platforms.</p><p>You can use them in lots of places: context menus, dock icon menus, tray menus. Most are optional but the one you'll always want to implement is the window menu.</p><div id="posthaven_gallery[1067856]">
          <div>
                    <p>
          <div class="readableLargeImageContainer"><img src="https://phaven-prod.s3.amazonaws.com/files/image_part/asset/1721701/-_AAFp0N7hFJb6fFZ6Jnr7koGjM/medium_Screen_Shot_2016-06-11_at_7.02.21_PM.png" /></div>
        </p>

          </div>
          
        </div>
<p><b>Follow each platform's conventions for what goes where.</b> For example, if you have Preferences, Mac users will expect to click YourApp &gt; Preferences while Windows users expect Window &gt; Preferences and Linux users expect File &gt; Preferences.</p><p>If you have a button for something, give it a menu item anyway. Two advantages: it makes your keyboard shortcuts discoverable, and it makes actions searchable under Help &gt; Search on a Mac.</p><p><a href="https://github.com/feross/webtorrent-desktop/blob/4a3ca5459da995c15af36952c07701479e69c472/main/menu.js" target="_blank">See it in action here: menu.js</a>.</p><h1><b>Shortcuts</b></h1><p>Electron supports two kinds of shortcuts: menu shortcuts and global shortcuts. </p><p>Menu shortcuts are great. New users can click around and learn what's available. Power users can use your app very efficiently.</p><b>Follow each platform's keyboard shortcut conventions.</b> Electron makes this easy: for example, you can specify "CmdOrCtrl+O" as the accelerator for Open, and it'll be Cmd+O on Mac and Ctrl+O on Windows and Linux.<p>Global shortcuts work even when your app is not focused. For example, if you're running WebTorrent Desktop in the background, playing an audiobook, while using Chrome in the foreground, you can still use the play/pause button on your keyboard (F8 on Mac) to control WebTorrent.</p><h1><b>Drag and drop</b></h1><p>If you want to let users drag files into your app, you'll need to handle three separate cases.</p><p>When someone drags files onto the window of your running app, you'll get the regular HTML5 drag-and-drop events.</p><p>When someone drags files onto the icon while your app is running, you'll get a special Electron on-file event.</p><p>When someone drags files onto the icon while your app is not running, the OS will run your main process with special command-line arguments. You'll have to handle those.</p><div id="gist36756652">
    <div>
      <div>
        <div>
  <div id="file-electron-drag-drop-js">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-electron-drag-drop-js-L1"></td>
        <td id="file-electron-drag-drop-js-LC1">// In the main process, check whether the app is starting</td>
      </tr>
      <tr>
        <td id="file-electron-drag-drop-js-L2"></td>
        <td id="file-electron-drag-drop-js-LC2">// because the user dragged files onto the app icon</td>
      </tr>
      <tr>
        <td id="file-electron-drag-drop-js-L3"></td>
        <td id="file-electron-drag-drop-js-LC3">process.argv.forEach(onOpen)</td>
      </tr>
      
      <tr>
        <td id="file-electron-drag-drop-js-L5"></td>
        <td id="file-electron-drag-drop-js-LC5">// Open handlers should be added on the first tick.</td>
      </tr>
      <tr>
        <td id="file-electron-drag-drop-js-L6"></td>
        <td id="file-electron-drag-drop-js-LC6">// These fire if the app is already running and the user</td>
      </tr>
      <tr>
        <td id="file-electron-drag-drop-js-L7"></td>
        <td id="file-electron-drag-drop-js-LC7">// drags files or URLs onto the dock icon, or if they set</td>
      </tr>
      <tr>
        <td id="file-electron-drag-drop-js-L8"></td>
        <td id="file-electron-drag-drop-js-LC8">// the app as a handler for a file type and then open a file</td>
      </tr>
      <tr>
        <td id="file-electron-drag-drop-js-L9"></td>
        <td id="file-electron-drag-drop-js-LC9">app.on('open-file', onOpen)</td>
      </tr>
      <tr>
        <td id="file-electron-drag-drop-js-L10"></td>
        <td id="file-electron-drag-drop-js-LC10">app.on('open-url', onOpen)</td>
      </tr>
      
      <tr>
        <td id="file-electron-drag-drop-js-L12"></td>
        <td id="file-electron-drag-drop-js-LC12">// Separately, in the renderer process, you can use the HTML5</td>
      </tr>
      <tr>
        <td id="file-electron-drag-drop-js-L13"></td>
        <td id="file-electron-drag-drop-js-LC13">// drag-drop API to create a drop target and handle files </td>
      </tr>
      <tr>
        <td id="file-electron-drag-drop-js-L14"></td>
        <td id="file-electron-drag-drop-js-LC14">// dropped directly onto the window.</td>
      </tr>
</tbody></table>


  </div>

  </div>
</div>

      </div>
      
    </div>
</div>
<h1><b>Crash Reporting</b></h1><p>Electron has built-in Crashpad support so that you can get a report when a process crashes.</p><div id="gist36756701">
    <div>
      <div>
        <div>
  <div id="file-electron-crash-reporter-js">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-electron-crash-reporter-js-L1"></td>
        <td id="file-electron-crash-reporter-js-LC1">// In *both* the main and renderer processes</td>
      </tr>
      <tr>
        <td id="file-electron-crash-reporter-js-L2"></td>
        <td id="file-electron-crash-reporter-js-LC2">// For example, in both main/index.js and renderer/index.js</td>
      </tr>
      <tr>
        <td id="file-electron-crash-reporter-js-L3"></td>
        <td id="file-electron-crash-reporter-js-LC3">var crashReporter = require('../crash-reporter')</td>
      </tr>
      <tr>
        <td id="file-electron-crash-reporter-js-L4"></td>
        <td id="file-electron-crash-reporter-js-LC4">crashReporter.init()</td>
      </tr>
      
      <tr>
        <td id="file-electron-crash-reporter-js-L6"></td>
        <td id="file-electron-crash-reporter-js-LC6">// Separately, create crash-reporter.js, shared by main and renderer:</td>
      </tr>
      <tr>
        <td id="file-electron-crash-reporter-js-L7"></td>
        <td id="file-electron-crash-reporter-js-LC7">module.exports = {</td>
      </tr>
      
      
      
      <tr>
        <td id="file-electron-crash-reporter-js-L11"></td>
        <td id="file-electron-crash-reporter-js-LC11">var config = require('./config')</td>
      </tr>
      <tr>
        <td id="file-electron-crash-reporter-js-L12"></td>
        <td id="file-electron-crash-reporter-js-LC12">var electron = require('electron')</td>
      </tr>
      
      <tr>
        <td id="file-electron-crash-reporter-js-L14"></td>
        <td id="file-electron-crash-reporter-js-LC14">function init () {</td>
      </tr>
      <tr>
        <td id="file-electron-crash-reporter-js-L15"></td>
        <td id="file-electron-crash-reporter-js-LC15">  electron.crashReporter.start({</td>
      </tr>
      <tr>
        <td id="file-electron-crash-reporter-js-L16"></td>
        <td id="file-electron-crash-reporter-js-LC16">    companyName: config.APP_NAME,</td>
      </tr>
      <tr>
        <td id="file-electron-crash-reporter-js-L17"></td>
        <td id="file-electron-crash-reporter-js-LC17">    productName: config.APP_NAME,</td>
      </tr>
      <tr>
        <td id="file-electron-crash-reporter-js-L18"></td>
        <td id="file-electron-crash-reporter-js-LC18">    submitURL: config.CRASH_REPORT_URL</td>
      </tr>
      
      
</tbody></table>


  </div>

  </div>
</div>

      </div>
      
    </div>
</div>
<p>You might also want to be notified of uncaught Javascript exceptions. You can do this:</p><ul>
<li>In the main process with <b>process.on('uncaughtException')</b>
</li>
<li>In the renderer process using <b>window.onerror</b>
</li>
</ul><p>Your server will need an API endpoint to save the crash reports. Check out the WebTorrent website code for an <a href="https://github.com/feross/webtorrent-www/blob/a8fd5b8a353bde867890b56a0e1491d12ed5c67a/server/web.js#L138" target="_blank">example of how to make one</a>.</p><h1>
<b>Signed Installers</b>
</h1><p><b>You must sign your installers.</b> Otherwise, you'll get a scary full-page red warning on Windows that says your app is "untrusted", and modern Macs in their stock configuration will refuse to run your app altogether.</p><p>Here's a build script that does this for <a href="https://github.com/feross/webtorrent-desktop/blob/12500dfb6415a665ea412319eef953d842dd2f04/bin/package.js#L250-L278" target="_blank">Mac</a> and for <a href="https://github.com/feross/webtorrent-desktop/blob/12500dfb6415a665ea412319eef953d842dd2f04/bin/package.js#L365-L369" title="Link: https://github.com/feross/webtorrent-desktop/blob/12500dfb6415a665ea412319eef953d842dd2f04/bin/package.js#L365-L369" target="_blank">Windows</a>.</p><p><b>Getting certs:</b></p><p><b>To get a Mac signing certificate, sign up for an Apple Developer account.</b> It costs $100 a year.</p><p><b>To get a Windows signing certificate, we recommend Digicert.</b> The documentation for Windows app signing is surprisingly bad. If you go with the wrong vendor, they'll ask you to mail them notarized paperwork. That makes it a slow and annoying process to get the cert. Digicert is easier: they just send you a password via Certified Mail, you go to the post office, show your ID to pick it up, and bam, you get your signing certificate.</p><p><b>You do not have to go thru the Mac App Store, unless you want to.</b> If you do, your app will be sandboxed and you may have to change the UX slightly to accommodate the extra restrictions and permission prompts.</p><p><b>You definitely don't need the Windows App Certification Kit.</b> WACK is wack, and also kind of obsolete.</p><div id="posthaven_gallery[1068448]">
          <div>
                    <p>
          <div class="readableLargeImageContainer"><img src="https://phaven-prod.s3.amazonaws.com/files/image_part/asset/1722666/kYZbRNfF3tkRxSwJsPRSmtPSJFE/medium_Screen_Shot_2016-06-13_at_6.45.31_PM.png" /></div>
        </p>

          </div>
          
        </div>
<p><b>Consider starting an organization to own your project's domain and certs.</b> It looks a lot more legit if a user downloads your app and sees "Do you want to run this file? ... Publisher: Webtorrent LLC", than if they see "Publisher: Jim Bob". There are other advantages as well. In California, starting an LLC costs just a few hundred dollars and a few hours of time.</p><p><b>Keep your signing certificates safe.</b> At a very minimum, they must never be sent via email or checked into a Github repo, even a private one. In fact, certs should never ever be online at all. Store them offline, passphrase-protected. Back them up onto a thumb drive, preferably an encrypted thumb drive, and keep it safe.</p><p><b>Once you get your first million users, your auto updater is basically a botnet with a million nodes. </b>With great power comes great responsibility.</p><h1><b>Automatic Updaters</b></h1><p>Your app is getting better every week. Remember Flash back in the day, nagging you to Please Upgrade To The Latest Version? Don't be that guy.</p><p>Ever since Chrome popularized autoupdaters eight years ago, users have come to expect software to just continuously get better and fix bugs automatically.</p><p>Writing your own reliable auto updater is hard. Fortunately, Electron has already integrated with Squirrel, which makes it easy.</p><p>Squirrel only works on Windows and Mac.</p><p>For Linux, I recommend checking for updates as you would on the other two platforms, and simply popping up a notification if a new version is available:</p><div id="posthaven_gallery[1068458]">
          <div>
                    <p>
          <div class="readableLargeImageContainer"><img src="https://phaven-prod.s3.amazonaws.com/files/image_part/asset/1722693/1oKuG6KVhqM4Mnlz1A1s_q8VNPA/medium_webtorrent-linux-update.png" /></div>
        </p>

          </div>
          
        </div>
<p>Here's a bit of code that checks for updates on all three platforms: <a href="https://github.com/feross/webtorrent-desktop/blob/62cb304971cb867e5923044df9b7afa2c5f35e78/main/updater.js" title="Link: https://github.com/feross/webtorrent-desktop/blob/62cb304971cb867e5923044df9b7afa2c5f35e78/main/updater.js" target="_blank">updater.js</a></p><p>Your server will need an API endpoint to tell the app which version is the latest. This can be really lightweight. You can offload the heavier work of hosting binaries to Github Releases.</p><p>Here's <a href="https://github.com/feross/webtorrent-www/blob/master/server/web.js#L159-204" title="Link: https://github.com/feross/webtorrent-www/blob/master/server/web.js#L159-204" target="_blank">our server code for the updater API</a>.</p><h1><b>One-Step Build</b></h1><p>16 years ago, <a href="http://www.joelonsoftware.com/articles/fog0000000043.html" target="_blank">a smart guy named Joel Spolsky invented the Joel Test</a> for whether a software project has its act together.</p><p>#2 on his list: Can You Make A Build In One Step?</p><p>Yes, you can! Electron makes it pretty easy to automate your build. And you can do it without any fancy tools like Grunt or Bower.</p><p>Check out WebTorrent Desktop's <a href="https://github.com/feross/webtorrent-desktop/blob/master/bin/package.js" target="_blank">build script</a>. With one command, <b>npm run package</b>, we can:</p><ul>
<li>Run the linter and tests</li>
<li>Package the app for all three platforms</li>
<li>Create signed installers for Mac and Windows*</li>
<li>Create binary deltas for the auto updater</li>
</ul><p>* (Almost. Right now we still need to do the Windows code signing on a separate Windows machine, but <a href="https://github.com/electron/windows-installer/issues/27" target="_blank">there's a bug</a> that should be fixed in the next few weeks that will allow us to build an entire release in a single command on a Mac.)</p><h1><b>Fast Startup</b></h1><p>You want your app to start quickly and smoothly. If it doesn't, it won't feel native.</p><p>Check out Spotify, for example. After clicking the dock icon, the window takes a long time to appear. Once it does, it first flashes grey, then some DOM elements appear, then the style changes, then more elements appear. Each time, it reflows, so the elements bounce around.</p><p>It feels like a web page loading over slow internet, not like a native app. (Spotify's UI is built with HTML and Javascript, but it doesn't use Electron.)</p><p><b>Make your app load quickly.</b></p><p><b>Step 1. Measure</b></p><p>Right at the start of our main process index.js, we call console.time('init')</p><p>Then, once the window (renderer process) has started and sends us an IPC message saying it's ready, we call console.timeEnd('init')</p><p>That gives us a bottom-line number to get as low as possible: the total startup time.</p><p><b>Step 2. Get your DOM right the first time</b></p><p>If you use functional reactive programming, this i easy. What you see is a function of your state object. The state object should be correct and ready to go the first time you render your DOM---otherwise, the DOM might have to change immediately and your app first renders, and the elements will jank around.</p><p>In our case, WebTorrent Desktop loads a JSON config file <i>before</i> the first render. This only adds a few milliseconds to our couple-hundred-millisecond startup time.</p><div id="gist36702295">
    <div>
      <div>
        <div>
  <div id="file-electron-renderer-init-js">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-electron-renderer-init-js-L1"></td>
        <td id="file-electron-renderer-init-js-LC1">console.time('init')</td>
      </tr>
      
      <tr>
        <td id="file-electron-renderer-init-js-L3"></td>
        <td id="file-electron-renderer-init-js-LC3">// require() calls and early initialization</td>
      </tr>
      <tr>
        <td id="file-electron-renderer-init-js-L4"></td>
        <td id="file-electron-renderer-init-js-LC4">[...]</td>
      </tr>
      
      <tr>
        <td id="file-electron-renderer-init-js-L6"></td>
        <td id="file-electron-renderer-init-js-LC6">var state = State.getInitialState()</td>
      </tr>
      
      <tr>
        <td id="file-electron-renderer-init-js-L8"></td>
        <td id="file-electron-renderer-init-js-LC8">// `state.saved` is read from and written to a file. All other state is ephemeral. </td>
      </tr>
      <tr>
        <td id="file-electron-renderer-init-js-L9"></td>
        <td id="file-electron-renderer-init-js-LC9">// First we load state.saved, once that is done, initialize the app.</td>
      </tr>
      <tr>
        <td id="file-electron-renderer-init-js-L10"></td>
        <td id="file-electron-renderer-init-js-LC10">loadState(init)</td>
      </tr>
      
      <tr>
        <td id="file-electron-renderer-init-js-L12"></td>
        <td id="file-electron-renderer-init-js-LC12">function init () {</td>
      </tr>
      <tr>
        <td id="file-electron-renderer-init-js-L13"></td>
        <td id="file-electron-renderer-init-js-LC13">  // Initialize your app</td>
      </tr>
      <tr>
        <td id="file-electron-renderer-init-js-L14"></td>
        <td id="file-electron-renderer-init-js-LC14">  // Set up event listeners</td>
      </tr>
      <tr>
        <td id="file-electron-renderer-init-js-L15"></td>
        <td id="file-electron-renderer-init-js-LC15">  // - Listen for IPC messages from the main process</td>
      </tr>
      <tr>
        <td id="file-electron-renderer-init-js-L16"></td>
        <td id="file-electron-renderer-init-js-LC16">  // - Listen for drag-drop events</td>
      </tr>
      <tr>
        <td id="file-electron-renderer-init-js-L17"></td>
        <td id="file-electron-renderer-init-js-LC17">  // - etc</td>
      </tr>
      <tr>
        <td id="file-electron-renderer-init-js-L18"></td>
        <td id="file-electron-renderer-init-js-LC18">  // Start your React or virtual-dom render loop</td>
      </tr>
      <tr>
        <td id="file-electron-renderer-init-js-L19"></td>
        <td id="file-electron-renderer-init-js-LC19">  // Create the DOM</td>
      </tr>
      <tr>
        <td id="file-electron-renderer-init-js-L20"></td>
        <td id="file-electron-renderer-init-js-LC20">  [...]</td>
      </tr>
      
      <tr>
        <td id="file-electron-renderer-init-js-L22"></td>
        <td id="file-electron-renderer-init-js-LC22">  // Done! Ideally we want to get here &lt;100ms after the user clicks the app</td>
      </tr>
      <tr>
        <td id="file-electron-renderer-init-js-L23"></td>
        <td id="file-electron-renderer-init-js-LC23">  console.timeEnd('init')</td>
      </tr>
      
</tbody></table>


  </div>

  </div>
</div>

      </div>
      
    </div>
</div>
<p><b>Step 3. Defer loading of big modules</b></p><p>We bisected using console.time() calls to find out which requires() were taking the longest, and cut our startup time almost in half by loading those lazily. They are loaded either the first time we need them or five seconds after app startup, whichever comes first.</p><p><b>Step 4. Colors and CSS</b></p><p>Make sure your window background color, which electron sends down to the OS, matches your CSS background color. Otherwise, you'll see flashes of white when the app is starting and again when you resize the window quickly.</p><p>Now we're already doing a lot better than a lot of apps. The window shows up quickly and with the correct background color, then a fraction of a second later the UI shows up.</p><p>One last improvement: by adding a CSS fade-in, the window shows up and the UI smoothly but quickly fades in, instead of popping up suddenly. Try it both ways---we think this feels better:</p><div id="gist36757161">
    <div>
      <div>
        <div>
  <div id="file-electron-app-css">
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-electron-app-css-L1"></td>
        <td id="file-electron-app-css-LC1">@keyframes fadein {</td>
      </tr>
      <tr>
        <td id="file-electron-app-css-L2"></td>
        <td id="file-electron-app-css-LC2">  from {</td>
      </tr>
      <tr>
        <td id="file-electron-app-css-L3"></td>
        <td id="file-electron-app-css-LC3">    opacity: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-electron-app-css-L6"></td>
        <td id="file-electron-app-css-LC6">    opacity: 1;</td>
      </tr>
      
      
      
      <tr>
        <td id="file-electron-app-css-L10"></td>
        <td id="file-electron-app-css-LC10">.app {</td>
      </tr>
      <tr>
        <td id="file-electron-app-css-L11"></td>
        <td id="file-electron-app-css-LC11">  /* Disable text selection, or your app will feel like a web page */</td>
      </tr>
      <tr>
        <td id="file-electron-app-css-L12"></td>
        <td id="file-electron-app-css-LC12">  -webkit-user-select: none;</td>
      </tr>
      <tr>
        <td id="file-electron-app-css-L13"></td>
        <td id="file-electron-app-css-LC13">  -webkit-app-region: drag;</td>
      </tr>
      
      <tr>
        <td id="file-electron-app-css-L15"></td>
        <td id="file-electron-app-css-LC15">  /* Cover the whole window */</td>
      </tr>
      <tr>
        <td id="file-electron-app-css-L16"></td>
        <td id="file-electron-app-css-LC16">  height: 100%;</td>
      </tr>
      
      <tr>
        <td id="file-electron-app-css-L18"></td>
        <td id="file-electron-app-css-LC18">  /* Make sure this matches the native window background color that you pass to</td>
      </tr>
      <tr>
        <td id="file-electron-app-css-L19"></td>
        <td id="file-electron-app-css-LC19">   * electron.BrowserWindow({...}), otherwise your app startup will look janky. */</td>
      </tr>
      <tr>
        <td id="file-electron-app-css-L20"></td>
        <td id="file-electron-app-css-LC20">  background: rgb(40, 40, 40);</td>
      </tr>
      
      <tr>
        <td id="file-electron-app-css-L22"></td>
        <td id="file-electron-app-css-LC22">  /* Smoother startup */</td>
      </tr>
      <tr>
        <td id="file-electron-app-css-L23"></td>
        <td id="file-electron-app-css-LC23">  animation: fadein 0.5s;</td>
      </tr>
      
</tbody></table>


  </div>

  </div>
</div>

      </div>
      
    </div>
</div>
<h1>Conclusion</h1><p><b>1. Make It Native</b></p><p>When on Mac, your app should look and feel like a Mac app. When on Windows, it should feel like a Windows app.</p><p><b>2. Make It Fast</b></p><p>Measure your startup speed. Keep it well under a second.</p><p><b>3. Keep It Simple</b></p><p>Your users don't care if you're using Flux and Redux and React and Bower and Grunt and Less and Coffeescript. Plain npm, plain Javascript, and plain CSS go a long way. Electron supports require() natively, so you don't need Browserify.</p><p>WebTorrent Desktop uses no preprocessors at all and no build system except npm. Spend your energy on things that give your users pleasure!</p><p>Bruce Lee said it best--</p><blockquote>
<p>The height of cultivation always runs to simplicity. </p>Art is the expression of the self. The more complicated and restricted the method, the less the opportunity for expression of one's original sense of freedom.</blockquote><blockquote><div>To me a lot of this fancy stuff is not functional.</div></blockquote><div><div id="posthaven_gallery[1067854]">
          <div>
                    <p>
          <div class="readableLargeImageContainer"><img src="https://phaven-prod.s3.amazonaws.com/files/image_part/asset/1721699/rNl29HOvBbNhSfq8PwKyTUnBedY/medium_bruce.jpeg" /></div>
        </p>

          </div>
          
        </div>
<p>Happy Hacking!</p>
</div>
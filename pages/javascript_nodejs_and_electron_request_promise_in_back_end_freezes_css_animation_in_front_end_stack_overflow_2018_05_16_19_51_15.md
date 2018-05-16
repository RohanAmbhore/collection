<a href="https://stackoverflow.com/questions/48430578/nodejs-and-electron-request-promise-in-back-end-freezes-css-animation-in-front">https://stackoverflow.com/questions/48430578/nodejs-and-electron-request-promise-in-back-end-freezes-css-animation-in-front</a><div id="articleHeader"><h1>request-promise in back-end freezes CSS animation in front-end</h1></div>

<p><em>Note: Additional information appended to end of original question as <strong>Edit #1</strong>, detailing how <code>request-promise</code> in the back-end is causing the UI freeze. Keep in mind that a pure CSS animation is hanging temporarily, and you can probably just skip to the edit (or read all for completeness)</em></p>

<p><strong>The setup</strong></p>

<p>I'm working on a desktop webapp, using <a href="https://electronjs.org/docs" target="_blank">Electron</a>.</p>

<p>At one point, the user is required to enter and submit some data. When they click "submit", I use JS to show <a href="https://projects.lukehaas.me/css-loaders/" target="_blank">this css loading animation</a> (bottom-right loader), and send data asynchronously to the back-end...</p>

<p><em>- HTML -</em></p>

<pre><code>&lt;button id="submitBtn" type="submit" disabled="true"&gt;Go!&lt;/button&gt;

&lt;div class="submit-loader"&gt;
    &lt;div class="loader _hide"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>

<p><em>- JS -</em></p>

<pre><code>form.addEventListener('submit', function(e) {
    e.preventDefault();

    loader.classList.remove('_hide');

    setTimeout(function() {
        ipcRenderer.send('credentials:submit', credentials);
    }, 0)
});</code></pre>

<p>where <code>._hide</code> is simply</p>

<pre><code>._hide {
    visibility: hidden;
}</code></pre>

<p>and where <code>ipcRenderer.send()</code> is an <a href="https://electronjs.org/docs/api/ipc-renderer#ipcrenderersendchannel-arg1-arg2-" target="_blank">async method</a>, without option to set otherwise.</p>

<p><strong>The problem</strong></p>

<p><em>Normally</em>, the <code>0ms</code> delay is sufficient to allow the DOM to be changed before the blocking event takes place. But not here. Whether using the <code>setTimeout()</code> or not, there is still a delay.</p>

<p>So, add a tiny delay...</p>

<pre><code>loader.classList.remove('_hide');

setTimeout(function() {
    ipcRenderer.send('credentials:submit', credentials);
}, 100);</code></pre>

<p>Great! The loader displays immediately upon submitting! But... after 100ms, the animation stops dead in its tracks, for about 500ms or so, and then gets back to chooching.</p>

<p>This working -&gt; not working -&gt; working pattern happens regardless of the delay length. As soon as the <code>ipcRenderer</code> starts doing stuff, everything is halted.</p>

<p><strong>So... Why!?</strong></p>

<p>This is the first time I've seen this kind of behavior. I'm pretty well-versed in HTML/CSS/JS, but am admittedly new to NodeJS and Electron. Why is my <em>pure CSS</em> animation being halted by the <code>ipcRenderer</code>, and what can I do to remedy this?</p>

<p><strong>Edit #1 - Additional Info</strong></p>

<p>In the back-end (NodeJS), I am using <a href="https://www.npmjs.com/package/request-promise" target="_blank">request-promise</a> to make a call to an external API. This happens when the back-end receives the <code>ipcRenderer</code> message.</p>

<pre><code>var rp = require('request-promise');

ipcMain.on('credentials:submit', function(e, credentials) {    

    var options = {
        headers : {
            ... api-key...
        },
        json: true,
        url : url,
        method : 'GET'
    };

    return rp(options).then(function(data) {
        ... send response to callback...
    }).catch(function(err) {
        ... send error to callback...
    });

}</code></pre>

<p>The buggy freezing behavior <em>only happens on the first API call</em>. Successive API calls (i.e. refreshing the desktop app without restarting the NodeJS backend), do not cause the hang-up. Even if I call a different API method, there are no issues.</p>

<p>For now, I've implemented the following hacky workaround:</p>

<p>First, initialize the first <code>BrowserWindow</code> with <code>show:false</code>...</p>

<pre><code>window = new BrowserWindow({
    show: false
});</code></pre>

<p>When the window is ready, send a ping to the external API, and only display the window after a successful response...</p>

<pre><code>window.on('ready-to-show', function() {
    apiWrapper.ping(function(response) {
        if(response.error) {
            app.quit();
        }else {
            window.show(true);
        }
    });
});</code></pre>

<p>This extra step means that there is about 500ms delay before the window appears, but then all successive API calls (whether <code>.ping()</code> or otherwise) no longer block the UI. We're getting to the verge of <a href="http://callbackhell.com/" target="_blank">callback hell</a>, but this isn't too bad.</p>

<p>So... this is a <code>request-promise</code> issue (which is <em>asynchronous</em>, as far as I can tell from the docs). Not sure why this behavior is only showing-up on the <strong><em>first call</em></strong>, so please feel free to let me know if you know! Otherwise, the little hacky bit will have to do for now.</p>

<p><em>(Note: I'm the only person who will ever use this desktop app, so I'm not too worried about displaying a "ping failed" message. For a commercial release, I would alert the user to a failed API call.)</em></p>
    
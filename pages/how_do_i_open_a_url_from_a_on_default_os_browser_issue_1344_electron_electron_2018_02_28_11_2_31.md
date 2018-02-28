<a href="https://github.com/electron/electron/issues/1344">https://github.com/electron/electron/issues/1344</a><div id="articleHeader"><h1>              How do I open a url from &lt;a&gt; on default OS browser?            #1344    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/luicaps" target="_blank">luicaps</a>  opened this Issue
        <relative-time>on Apr 1, 2015</relative-time>
        · 16 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          <div>
            





            
  <div id="issue-65708541">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>I want to take an  to an external website, but I do not want it to happen inside atom-shell, I want it to be in the default browser. How can I do that?</p>
<p>Thanks!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

          </div>

          


  


  


  


  
<div>
    
<div>
  





  
  <div id="issuecomment-138328385">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>On my setup, I tried both <code>shell.openExternal('http://example.com')</code> and <code>shell.openItem('http://example.com')</code> and both opened the website in the background.</p>
<p>I ended up using <code>child_process.execSync('start http://example.com')</code> on Win32 and <code>child_process.execSync('open http://example.com')</code> on Darwin so the browser actually pops up and gets focus.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  
<div>
    
<div>
  





  
  <div id="issuecomment-149800318">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>On Linux, you can use xdg-open:<br />
<code>child_process.execSync('xdg-open http://example.com')</code></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  
<div>
    
<div>
  





  
  <div id="issuecomment-150031171">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>I have actually decided to use <a href="https://github.com/pwnall/node-open" target="_blank">node-open</a>. You should give it a try if you don't want to mess with escaping and such.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  
<div>
    
<div>
  





  
  <div id="issuecomment-168730855">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Guys, but your solutions are great, but I'm wondering how to intercept attempt to open url like "<a href="http://someurl.com" target="_blank">http://someurl.com</a>" and then open in with <code>shell.openExternal</code>? Service worker allows to catch only requests to the files on the same domain. Is there ability to do this? /cc <a href="https://github.com/maxogden" target="_blank">@maxogden</a> <a href="https://github.com/alicanc" target="_blank">@AlicanC</a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  
<div>
    
<div>
  





  
  <div id="issuecomment-171512775">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Same question here as <a href="https://github.com/havenchyk" target="_blank">@havenchyk</a>, is there a way to tell electron to open links external by default?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  
<div>
    
<div>
  





  
  <div id="issuecomment-171516261">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>If your app only uses one window, and you can guarantee that every external link in your app opens in a new window (via eg. <code>target="_blank"</code>), you can do something like:</p>
<pre><code>webContents.on('new-window', function(event, url){
  event.preventDefault();
  open(url);
});
</code></pre>
<p>Where <code>webContents</code> is your main BrowserWindow's webContents and <code>open</code> is a function that opens the url in your browser (I use <a href="https://www.npmjs.com/package/open" target="_blank">node-open</a> as recommended by AlicanC).</p>
<p>It'd be nice if there was an event fired when <em>any</em> link is clicked, so the app could decide if it should open in the browser, but I haven't found such an event if it exists.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  
<div>
    
<div>
  





  
  <div id="issuecomment-171516636">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>I found this code snippet on S.O.:</p>
<pre><code>    var shell = require('electron').shell;
    //open links externally by default
    $(document).on('click', 'a[href^="http"]', function(event) {
        event.preventDefault();
        shell.openExternal(this.href);
    });
</code></pre>
<p>Dropped it in my main index file, it seems to be working as far as I can tell, even for dynamically generated links. I'm too noob at electron to know if there are any drawbacks to this I should watch out for. Thoughts?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  


  
<div>
    
<div>
  





  
  <div id="issuecomment-208839713">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>I'm using this piece of code:</p>
<div><pre>var handleRedirect = (e, url) =&gt; {
  if(url != webContents.getURL()) {
    e.preventDefault()
    require('electron').shell.openExternal(url)
  }
}

webContents.on('will-navigate', handleRedirect)
webContents.on('new-window', handleRedirect)</pre></div>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  
<div>
    
<div>
  





  
  <div id="issuecomment-218495898">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>First declare a spawn proccess</p>
<p>`app.controller('GuideCtrl', ['$scope', ($scope)=&gt;{<br />
const spawn = require('child_process').spawn;</p>
<pre><code>  $scope.openBrowser=(url)=&gt;{
     let exec = spawn('explore', [url], {});
     exec.stdout.on('data', (data)=&gt; {
        console.log('stdout: ' + data)
     });
  }
</code></pre>

<p>and before call the method</p>
<p><code>&lt;a ng-click="openBrowser('https://google.com')"&gt;Goto google&lt;/a&gt;</code></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  


  
<div>
    
<div>
  





  
  <div id="issuecomment-262619122">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Does <code>shell.openExternal</code> have any security issues? For example if links come off the net then raw net data is being passed to <code>shell.openExternal</code> or any of the other functions above. Does <code>shell.openExternal</code> make sure nothing bad's going to happen? Do I need to filter for schemas?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  
<div>
    
<div>
  





  
  <div id="issuecomment-264662585">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Base on the code from <a href="https://github.com/rubencodes" target="_blank">@rubencodes</a> , i used :</p>
<pre><code>   const shell = require('electron').shell;
   $('.open-in-browser').click((event) =&gt; {
           event.preventDefault();
           shell.openExternal(event.target.href);
   });
</code></pre>
<p>Then you just have to drop the 'open-in-browser' class to each elements you want to open in the browser.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  


  
<div>
    
<div>
  





  
  <div id="issuecomment-339585884">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Here's one that doesn't require JQuery, in case anyone else is hunting for it. It will automatically open any link that starts with 'http' in the external browser.</p>
<p>Put this in your renderer process:</p>
<div><pre>// Open all links in external browser
let shell = require('electron').shell
document.addEventListener('click', function (event) {
  if (event.target.tagName === 'A' && event.target.href.startsWith('http')) {
    event.preventDefault()
    shell.openExternal(event.target.href)
  }
})</pre></div>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  


  
<div>
    
<div>
  





  
  <div id="issuecomment-359309049">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>If you want <strong>ALL</strong> <code>&lt;a&gt;</code> tags to open in the default browser, try this in your main.ts:</p>
<pre><code>const shell = require('electron').shell;

mainWin.webContents.on('will-navigate', (event, url) =&gt; {
  event.preventDefault()
  shell.openExternal(url)
});
</code></pre>
<p>This assumes your have a single page app like me. If not, you'll need to do some extra sanitizing.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  
<div>
    
<div>
  





  
  <div id="issuecomment-359312676">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/greggman" target="_blank">greggman</a>
  

    </strong>

    commented

    <a href="#issuecomment-359312676" target="_blank"><relative-time>on Jan 22</relative-time></a>


      
  •


  

  </h3>
</div>


    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>I just want to reiterate that using this with user content without a whitelist is probably a gaping security hole. I don't know what all various schemes do and what their inputs are but just as a simple example a link like this</p>
<pre><code> &lt;a href="imessage:hello"&gt;click me&lt;/a&gt;
</code></pre>
<p>Will prompt the user in Chrome and Safari on macOS but with the code above Electron will just open the app.</p>
<p>It almost feels like Electron itself should default to being more secure here rather than leave it to every individual programmer to figure out how to make it secure on their own.</p>
<p>At a minimum you probably want something like</p>
<pre><code>function isSafeishURL(url) {
  return url.startsWith('http:') || url.startsWith('https:');
}

mainWin.webContents.on('will-navigate', (event, url) =&gt; {
  event.preventDefault();
  if (isSafeishURL(url)) {
    shell.openExternal(url);
  }
});
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>

</div>

</div>

  


  












        
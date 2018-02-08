<a href="https://github.com/GoogleChrome/puppeteer/issues/1597">https://github.com/GoogleChrome/puppeteer/issues/1597</a><div id="articleHeader"><h1>              Failed to download Chromium r515411            #1597    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/gp5251" target="_blank">gp5251</a>  opened this Issue
        <relative-time>on Dec 14, 2017</relative-time>
        · 13 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            





            
  <div id="issue-281980263">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>I came across an problem like below when i tried to run npm i puppeteer, is there any solution?</p>
<p>puppeteer@0.13.0 install /Users/guipeng/Desktop/ldl/puppeteer/node_modules/puppeteer<br />
node install.js</p>
<p>ERROR: Failed to download Chromium r515411! Set "PUPPETEER_SKIP_CHROMIUM_DOWNLOAD" env variable to skip download.<br />
{ Error: read ETIMEDOUT<br />
at _errnoException (util.js:1041:11)<br />
at TLSWrap.onread (net.js:606:25) code: 'ETIMEDOUT', errno: 'ETIMEDOUT', syscall: 'read' }<br />
npm WARN enoent ENOENT: no such file or directory, open '/Users/guipeng/Desktop/ldl/puppeteer/package.json'</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  

          

          

  
  


  
<div>
    
<div>
  





  
  <div id="issuecomment-351692464">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/gp5251" target="_blank">@gp5251</a> This might just be an intermittent network issue. Does this happen consistently?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-351897094">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/paambaati" target="_blank">@paambaati</a> I also encountered the same situation.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-351945645">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>使用国内Chromium源<br />
<a href="https://npm.taobao.org/mirrors" target="_blank">https://npm.taobao.org/mirrors</a></p>
<div><pre># // &gt; https://npm.taobao.org/mirrors
# // export PUPPETEER_DOWNLOAD_HOST=https://npm.taobao.org/mirrors
# // set PUPPETEER_DOWNLOAD_HOST=https://npm.taobao.org/mirrors

npm config set puppeteer_download_host=https://npm.taobao.org/mirrors
npm i puppeteer</pre></div>
<hr />
<p>或者用淘宝的<a href="https://npm.taobao.org/" target="_blank">cnpm </a>安装，自动使用国内源</p>
<div><pre>npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm i puppeteer</pre></div>
<hr />
<p>还可以手动下载Chromium文件，解压后放在本地<br />
<a href="https://npm.taobao.org/mirrors/chromium-browser-snapshots/" target="_blank">https://npm.taobao.org/mirrors/chromium-browser-snapshots/</a></p>
<ul>
<li>放在模块的默认读取目录下<br />
例如 <code>node_modules\puppeteer\.local-chromium\win64-526987(系统类型-版本号)\chrome-win32(下载的文件名)\</code><br />
版本号来自 puppeteer/package.json-&gt;puppeteer.chromium_revision，具体见<a href="https://github.com/GoogleChrome/puppeteer/blob/master/lib/Downloader.js" target="_blank">lib/Downloader.js</a></li>
<li>放在其他目录，运行时设置路径参数<br />
<a href="https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#puppeteerlaunchoptions" target="_blank">puppeteer.launch({executablePath:'ChromiumExePath'})</a></li>
</ul>
<hr />
<blockquote>
<p><a href="https://github.com/cnpm/cnpmjs.org/issues/1246" target="_blank">cnpm/cnpmjs.org#1246</a><br />
<code>storage.googleapis.com</code> 整站代理：<a href="https://storage.googleapis.com.cnpmjs.org" target="_blank">https://storage.googleapis.com.cnpmjs.org</a><br />
<a href="https://npm.taobao.org/mirrors" target="_blank">https://npm.taobao.org/mirrors</a><br />
<a href="https://github.com/cnpm/binary-mirror-config/blob/master/package.json#L43" target="_blank">cnpm/binary-mirror-config/package.json</a></p>
</blockquote>
      </td>
    </tr>
  </tbody>
</table>


        



    

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-351959112">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/vc1" target="_blank">@vc1</a> problem resolved, 3q.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-351987548">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>We're using a private nexus repository. Could I interchange the googleapis.com url, with our own direct route? Are there any other request related attributes we need to take care off?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  


  
<div>
    
<div>
  





  
  <div id="issuecomment-355238047">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/aslushnikov" target="_blank">aslushnikov</a>
  

    </strong>

    commented

    <a href="#issuecomment-355238047" target="_blank"><relative-time>on Jan 4</relative-time></a>


  </h3>
</div>


    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/p0psicles" target="_blank">@p0psicles</a> there's <a href="https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#environment-variables" target="_blank"><code>PUPPETEER_DOWNLOAD_HOST</code></a> that you can use to download from a mirror.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  


  
<div>
    
<div>
  





  
  <div id="issuecomment-355261319">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Yes I figured it out eventually. I do think it would help if this would be added to the documentation. Now you need to search through a number of issues or go through the code yourself.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-355356165">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/aslushnikov" target="_blank">aslushnikov</a>
  

    </strong>

    commented

    <a href="#issuecomment-355356165" target="_blank"><relative-time>on Jan 5</relative-time></a>


  </h3>
</div>


    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/p0psicles" target="_blank">@p0psicles</a> I'll be happy to review a PR!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-357842295">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>I tried the above method, But it did not work</p>
<pre><code>cnpm i puppeteer
ERROR: Failed to download Chromium r526987! Set "PUPPETEER_SKIP_CHROMIUM_DOWNLOAD" env variable to skip download.
Error: Download failed: server returned code 404. URL: https://cdn.npm.taobao.org/dist/chromium-browser-snapshots/Mac/526987/chrome-mac.zip
    at response (/Users/mac/Desktop/node/learnNode/pupp/node_modules/_puppeteer@1.0.0@puppeteer/lib/Downloader.js:228:21)

cnpm config get registry
http://registry.npm.taobao.org/
</code></pre>
<pre><code>npm i puppeteer
npm WARN registry Using stale data from https://registry.npmjs.org/ because the host is inaccessible -- are you offline?
npm WARN registry Using stale package data from https://registry.npmjs.org/ due to a request error during revalidation.

&gt; puppeteer@1.0.0 install /Users/mac/Desktop/node/learnNode/pupp/node_modules/puppeteer
&gt; node install.js

ERROR: Failed to download Chromium r526987! Set "PUPPETEER_SKIP_CHROMIUM_DOWNLOAD" env variable to skip download.
{ Error: read ETIMEDOUT
    at _errnoException (util.js:1024:11)
    at TLSWrap.onread (net.js:615:25) code: 'ETIMEDOUT', errno: 'ETIMEDOUT', syscall: 'read' }

echo $PUPPETEER_DOWNLOAD_HOST
https://storage.googleapis.com.cnpmjs.org
</code></pre>
<p>How can I resolve it?<br />
I tried to manually install It. But hen I run it I got the following error</p>
<pre><code>const puppeteer = require('puppeteer');

(async () =&gt; {

    const executablePath = '/Applications/Chromium.app/Contents/MacOS/Chromium';
    const headless = true;
    const context = 'default';

    const browser = await puppeteer.launch({ executablePath, headless });
    const page = await browser.newPage({ context });
    await page.goto('https://example.com');
    await page.screenshot({path: 'example.png'});
    browser.close();

})();

(node:1980) UnhandledPromiseRejectionWarning: Unhandled promise rejection (rejection id: 1): Error: Protocol error (Page.getFrameTree): 'Page.getFrameTree' wasn't found undefined
(node:1980) [DEP0018] DeprecationWarning: Unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a non-zero exit code.
</code></pre>
<p>I do not know if this error was caused by a manual installation。<br />
Can anyone help me?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-358067975">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <blockquote>
<p>I tried the above method, But it did not work<br />
How can I resolve it?</p>
</blockquote>
<p>It looks like there's a something that prevents pptr from network access. If there's a proxy, you can set it up with <a href="https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#environment-variables" target="_blank">env variables</a>.</p>
<blockquote>
<p>I do not know if this error was caused by a manual installation。<br />
Can anyone help me?</p>
</blockquote>
<p><a href="https://github.com/kiki882727" target="_blank">@kiki882727</a> you're trying to run an old chromium. If you're using pptr 1.0.0, try running Chrome Canary instead.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  


  
<div>
    
<div>
  





  
  <div id="issuecomment-362927590">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Any progress?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-363629225">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>It doesn't work with any solutions on my mac.<br />
Finally I solve with following steps:</p>
<ol>
<li><code>vi .npmrc</code></li>
<li>type <code>puppeteer_download_host = https://npm.taobao.org/mirrors</code></li>
<li><code>yarn add puppeteer@1.0.0 -D</code><br />
After waiting for about 10mins, done!</li>
</ol>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-364120088">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/aslushnikov" target="_blank">@aslushnikov</a> thanks for your help, I tried anther version of puppeter -- 0.13.0, It worked very well. I will upgrades it in the feature, But not now, thank you again for your help</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  















        


        <div>
              
<div>
  

    
      



      <div>
        
          <div>
  


  
  <div>

    

    

        <p>
    
    
        Attach files by dragging & dropping,
        selecting them, or pasting
        from the clipboard.
    
    
    
    
    
    
    
    
    
  </p>


    
  </div>

  

  


  


          
      




        
      

    
    
  
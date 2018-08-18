<a href="https://github.com/npm/npm/issues/17340">https://github.com/npm/npm/issues/17340</a><div id="articleHeader"><h1>Unexpected token < in JSON at position 35 · Issue #17340 · npm/npm</h1></div>

        

          
            




            

  

    



    

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <h4>I'm opening this issue because:</h4>
<ul>
<li>
  
    
   npm is crashing.</li>
<li>
  
    
   npm is producing an incorrect install.</li>
<li>
  
    
   npm is doing something I don't understand.</li>
<li>
  
    
   Other (<em>see below for feature requests</em>):</li>
</ul>
<h4>What's going wrong?</h4>
<p>Running <code>npm i</code> within a certain project produces the following error.</p>
<pre><code>npm ERR! Unexpected token &lt; in JSON at position 35
</code></pre>
<p>From the <a href="https://gist.github.com/joshfarrant/01306b808399ec6cacd752086622baf1" target="_blank">debug.log</a> it appears that npm is trying to read the load the shrinkwrap and failing. It's worth noting that this issue only occurs in this project on my current machine. I've tested on another Fedora 22 machine, (same npm and node versions) and the install works as expected. I appreciate this points to my local environment being the cause, however it looks like there may be some invalid syntax (<code>&lt;</code>) stuck in a config file somewhere that shouldn't be there and that I am unable to clear. Here is the <a href="https://gist.github.com/joshfarrant/660f8d5559fb0d0d3f481a72f76c2308" target="_blank">package.json</a> for this project.</p>
<h4>How can the CLI team reproduce the problem?</h4>
<p>I'm unsure how to suggest reproduction of the issue, however I'm happy to test any suggestions anyone offers and report back.</p>
<h3>supporting information:</h3>
<ul>
<li><code>npm -v</code> prints: 5.0.3</li>
<li><code>node -v</code> prints: 8.0.0</li>
<li><code>npm config get registry</code> prints: <a href="https://registry.npmjs.org/" target="_blank">https://registry.npmjs.org/</a></li>
<li>Windows, OS X/macOS, or Linux?: Linux (Fedora 22)</li>
<li>Network issues:
<ul>
<li>Geographic location where npm was run: United Kingdom</li>
<li>
  
    
   I use a proxy to connect to the npm registry.</li>
<li>
  
    
   I use a proxy to connect to the web.</li>
<li>
  
    
   I use a proxy when downloading Git repos.</li>
<li>
  
    
   I access the npm registry via a VPN</li>
<li>
  
    
   I don't use a proxy, but have limited or unreliable internet access.</li>
</ul>
</li>
<li>Container:
<ul>
<li>
  
    
   I develop using Vagrant on Windows.</li>
<li>
  
    
   I develop using Vagrant on OS X or Linux.</li>
<li>
  
    
   I develop / deploy using Docker.</li>
<li>
  
    
   I deploy to a PaaS (Triton, Heroku).</li>
</ul>
</li>
</ul>


      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    
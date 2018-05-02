<a href="https://github.com/facebook/create-react-app/issues/2352">https://github.com/facebook/create-react-app/issues/2352</a><div id="articleHeader"><h1>              TypeError: Cannot read property 'request' of undefined            #2352    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/wiadev" target="_blank">wiadev</a>  opened this Issue
        <relative-time>on May 25, 2017</relative-time>
        · 11 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      

  
    
      
          <p>Hi. I 'm having problem running the create-react-app.</p>
<p>Here is the error I've got.<br />
`<br />
TypeError: Cannot read property 'request' of undefined</p>
<ul>
<li>
<p>ExternalModuleFactoryPlugin.js:37 handleExternals<br />
[www-react-client]/[webpack]/lib/ExternalModuleFactoryPlugin.js:37:33</p>
</li>
<li>
<p>ExternalModuleFactoryPlugin.js:46 next<br />
[www-react-client]/[webpack]/lib/ExternalModuleFactoryPlugin.js:46:8</p>
</li>
<li>
<p>ExternalModuleFactoryPlugin.js:59 handleExternals<br />
[www-react-client]/[webpack]/lib/ExternalModuleFactoryPlugin.js:59:7</p>
</li>
<li>
<p>ExternalModuleFactoryPlugin.js:79 ExternalModuleFactoryPlugin.<br />
[www-react-client]/[webpack]/lib/ExternalModuleFactoryPlugin.js:79:5</p>
</li>
<li>
<p>NormalModuleFactory.js:246 applyPluginsAsyncWaterfall<br />
[www-react-client]/[react-scripts]/[webpack]/lib/NormalModuleFactory.js:246:4</p>
</li>
<li>
<p>Tapable.js:204<br />
[www-react-client]/[react-scripts]/[tapable]/lib/Tapable.js:204:11</p>
</li>
<li>
<p>IgnorePlugin.js:56 IgnorePlugin.checkIgnore<br />
[www-react-client]/[react-scripts]/[webpack]/lib/IgnorePlugin.js:56:10</p>
</li>
<li>
<p>Tapable.js:208 NormalModuleFactory.applyPluginsAsyncWaterfall<br />
[www-react-client]/[react-scripts]/[tapable]/lib/Tapable.js:208:13</p>
</li>
<li>
<p>NormalModuleFactory.js:230 NormalModuleFactory.create<br />
[www-react-client]/[react-scripts]/[webpack]/lib/NormalModuleFactory.js:230:8</p>
</li>
<li>
<p>Compilation.js:382 Compilation._addModuleChain<br />
[www-react-client]/[react-scripts]/[webpack]/lib/Compilation.js:382:17</p>
</li>
<li>
<p>Compilation.js:464 Compilation.addEntry<br />
[www-react-client]/[react-scripts]/[webpack]/lib/Compilation.js:464:8</p>
</li>
<li>
<p>SingleEntryPlugin.js:22 SingleEntryPlugin.<br />
[www-react-client]/[webpack]/lib/SingleEntryPlugin.js:22:15</p>
</li>
<li>
<p>Tapable.js:229 Compiler.applyPluginsParallel<br />
[www-react-client]/[react-scripts]/[tapable]/lib/Tapable.js:229:14</p>
</li>
<li>
<p>Compiler.js:488<br />
[www-react-client]/[react-scripts]/[webpack]/lib/Compiler.js:488:8</p>
</li>
<li>
<p>Tapable.js:131 Compiler.applyPluginsAsyncSeries<br />
[www-react-client]/[react-scripts]/[tapable]/lib/Tapable.js:131:46</p>
</li>
<li>
<p>Compiler.js:481 Compiler.compile<br />
[www-react-client]/[react-scripts]/[webpack]/lib/Compiler.js:481:7<br />
`</p>
</li>
</ul>
<p>Thanks</p>
      
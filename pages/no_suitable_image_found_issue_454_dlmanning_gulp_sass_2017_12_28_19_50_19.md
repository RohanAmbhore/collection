<a href="https://github.com/dlmanning/gulp-sass/issues/454">https://github.com/dlmanning/gulp-sass/issues/454</a><div id="articleHeader"><h1>              no suitable image found            #454    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/wzl610" target="_blank">wzl610</a>  opened this Issue
        <relative-time>on Mar 24, 2016</relative-time>
        · 9 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        
          

  
  

    





      
  

    



    
      
        
          
            
                <p>When I add gulp-sass into my project and write gulpfile.js as "Basic Usage" write,but when I start gulp`s task,it shows me as bottom:</p>
<pre><code>module.js:434
  return process.dlopen(module, path._makeLong(filename));
                 ^

Error: dlopen(/Users/AllenWang/Documents/project/h5model/node_modules/node-sass/vendor/darwin-x64-46/binding.node, 1): no suitable image found.  Did find:
    /Users/AllenWang/Documents/project/h5model/node_modules/node-sass/vendor/darwin-x64-46/binding.node: truncated mach-o error: segment __TEXT extends to 1167360 which is past end of file 678448
    at Error (native)
    at Object.Module._extensions..node (module.js:434:18)
    at Module.load (module.js:343:32)
    at Function.Module._load (module.js:300:12)
    at Module.require (module.js:353:17)
    at require (internal/module.js:12:17)
    at Object.&lt;anonymous&gt; (/Users/AllenWang/Documents/project/h5model/node_modules/node-sass/lib/index.js:16:15)
    at Module._compile (module.js:409:26)
    at Object.Module._extensions..js (module.js:416:10)
    at Module.load (module.js:343:32)
</code></pre>
<p>I have reinstall gulp-sass and update my nodejs and npm version,but it also show this error.Can you help me?</p>
            
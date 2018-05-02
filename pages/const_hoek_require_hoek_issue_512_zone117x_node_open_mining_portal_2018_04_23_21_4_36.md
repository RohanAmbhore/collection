<a href="https://github.com/zone117x/node-open-mining-portal/issues/512">https://github.com/zone117x/node-open-mining-portal/issues/512</a><div id="articleHeader"><h1>              const Hoek = require('hoek');            #512    </h1></div>


  <div>
    
    <div>
        <a href="/jcreyesb" target="_blank">jcreyesb</a>  opened this Issue
        <relative-time>on Sep 27, 2017</relative-time>
        · 16 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      

  
    
      

          /home/pool/nomp/node_modules/request/node_modules/hawk/node_modules/boom/lib/index.js:5<br />
const Hoek = require('hoek');<br />
^^^^^<br />
SyntaxError: Use of const in strict mode.<br />
at Module._compile (module.js:439:25)<br />
at Object.Module._extensions..js (module.js:474:10)<br />
at Module.load (module.js:356:32)<br />
at Function.Module._load (module.js:312:12)<br />
at Module.require (module.js:364:17)<br />
at require (module.js:380:17)<br />
at Object. (/home/pool/nomp/node_modules/request/node_modules/hawk/lib/index.js:5:33)<br />
at Module._compile (module.js:456:26)<br />
at Object.Module._extensions..js (module.js:474:10)<br />
at Module.load (module.js:356:32)
<p>i installed hoek,<br />
pool@ubuntu143:~/nomp$ sudo npm install hoek<br />
npm http GET <a href="https://registry.npmjs.org/hoek" target="_blank">https://registry.npmjs.org/hoek</a><br />
npm http 304 <a href="https://registry.npmjs.org/hoek" target="_blank">https://registry.npmjs.org/hoek</a><br />
npm WARN engine hoek@5.0.0: wanted: {"node":"&gt;=8.0.0"} (current: {"node":"v0.10.25","npm":"1.3.10"})<br />
hoek@5.0.0 node_modules/hoek</p>
<p>but when i run node init.js i have the same message</p>
      
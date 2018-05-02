<a href="https://github.com/hapijs/hoek/issues/207">https://github.com/hapijs/hoek/issues/207</a><div id="articleHeader"><h1>              Minify index.js is failing when trying to minify            #207    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/krhubert" target="_blank">krhubert</a>  opened this Issue
        <relative-time>on Sep 20, 2017</relative-time>
        · 2 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          <div>
            




            
<div>
  <div id="issue-258932893">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>When using joi with create-react-app script <code>yarn build</code> cmd returns error:</p>
<pre><code>Failed to compile.

Failed to minify the code from this file: 

 	./node_modules/joi/node_modules/hoek/lib/index.js:33 
</code></pre>
<p>There is no way to prevent minify build and joi became unusable (without hacks) in create-react-app</p>
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
  <h3 id="event-1256113904">

    
      
    

    

        
  <a href="/krhubert" target="_blank">krhubert</a>
  


      
changed the title from
Minify index.js is failing
to
Minify index.js is failing when trying to minify


    <a href="#event-1256113904" target="_blank"><relative-time>on Sep 20, 2017</relative-time></a>

  </h3>
</div>



</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-330660541">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>What version of Node are you running <a href="https://github.com/krhubert" target="_blank">@krhubert</a> also what version of <code>Hoek</code> is this occurring with (provide the version of <code>Joi</code> if you have that handy and I can lookup the version)?</p>
<p>Currently in Hoek line <a href="https://github.com/hapijs/hoek/blob/1db691bc84ae059321146b83e03889adf36c8ef4/lib/index.js#L33" target="_blank">33</a> is the first occurrence of an ES6 piece of code <code>let newObj;</code> which I've run into some minifiers that still don't have support for ES6 and instead have had to either switch to WebPack (or a similar packager) or run the code through Babel prior to minifying it (I haven't done any of this on Joi or Hoek but on other libraries).</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-362791151">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>This is an old issue, but if you ended up in her from a search engine this might help:</p>
<p>try using joi-browser</p>
<p>npm i joi-browser</p>
<p>and in your code:<br />
const Joi = require('joi-browser');</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>










        
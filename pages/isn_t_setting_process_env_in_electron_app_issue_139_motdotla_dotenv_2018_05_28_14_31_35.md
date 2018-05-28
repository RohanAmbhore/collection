<a href="https://github.com/motdotla/dotenv/issues/139">https://github.com/motdotla/dotenv/issues/139</a><div id="articleHeader"><h1>              Isn't setting process.env in Electron app            #139    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/tashoecraft" target="_blank">tashoecraft</a>  opened this Issue
        <relative-time>on Apr 30, 2016</relative-time>
        · 6 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      


  
    
      

          <p>I am running an electron application with webpack and it seems to be pulling in the values from the .env file, but process.env isn't getting set.</p>
<p>I have placed the require('dotenv').config() at the entrance to the application where webpack starts building, which is my where all my vendor files live.</p>
<p>If I set a variable to the result of the require, it stores my variables, but when I go to use them only my Node_ENV variable is available.</p>

<pre><code>GAUTHID=secretID
</code></pre>
<p>vendor.js</p>
<pre><code>module.exports = function() {
require('dotenv').config();
//lots of modules loaded in below
}
</code></pre>
<p>home.js</p>
<pre><code>console.log(process.env)
</code></pre>
<p>logs =&gt; {NODE_ENV: 'Development'}</p>
<p>Wondering why it seems to access the values fine, but isn't saving them. I've tried different locations, using .load(), but all have no effect.</p>
      
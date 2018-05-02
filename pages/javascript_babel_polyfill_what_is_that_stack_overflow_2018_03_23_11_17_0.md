<a href="https://stackoverflow.com/questions/31122193/babel-polyfill-what-is-that">https://stackoverflow.com/questions/31122193/babel-polyfill-what-is-that</a><div id="articleHeader"><h1>Babel polyfill? What is that?</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        108
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>23</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I just started to use Babel to compile my ES6 javascript code into ES5. When I start to use Promises it looks like it's not working. The Babel website states support for promises via polyfills.</p>

<p>Without any luck, I tried to add:</p>

<pre><code>require("babel/polyfill");</code></pre>



<pre><code>import * as p from "babel/polyfill";</code></pre>

<p>With that I'll get the following error on my app bootstrapping:</p>

<blockquote>
  <p>Cannot find module 'babel/polyfill'</p>
</blockquote>

<p>I searched for the module but it seems I'm missing some fundamental thing here. I also tried to add the old and good bluebird NPM but it looks like it's not working.</p>

<p>How to use the polyfills from Babel?</p>
    </div>
    
    
</div>

                
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-31122311">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        44
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>The <a href="https://babeljs.io/docs/usage/polyfill/" target="_blank">Babel docs</a> describe this pretty concisely:</p>

<blockquote>
  <p>Babel includes a polyfill that includes a custom regenerator runtime
  and core.js.</p>
  
  <p>This will emulate a full ES6 environment. This polyfill is
  automatically loaded when using babel-node and babel/register.</p>
</blockquote>

<p>Make sure you require it at the entry-point to your application, before anything else is called. If you're using a tool like webpack, that becomes pretty simple (you can tell webpack to include it in the bundle).</p>

<p>If you're using a tool like <code>gulp-babel</code> or <code>babel-loader</code>, you need to also install the <code>babel</code> package itself to use the polyfill.</p>

<p>Also note that for modules that affect the global scope (polyfills and the like), you can use a terse import to avoid having unused variables in your module:</p>

<pre><code>import 'babel/polyfill';</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-32515193">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>First off, the obvious answer that no one has provided, you need to install Babel into your application:</p>

<pre><code>npm install babel --save</code></pre>

<p>(or <code>babel-core</code> if you instead want to <code>require('babel-core/polyfill')</code>).</p>

<p>Aside from that, I have a grunt task to transpile my es6 and jsx as a build step (i.e. I don't want to use <code>babel/register</code>, which is why I am trying to use <code>babel/polyfill</code> directly in the first place), so I'd like to put more emphasis on this part of @ssube's answer:</p>

<blockquote>
  <p>Make sure you require it at the entry-point to your application,
  before anything else is called</p>
</blockquote>

<p>I ran into some weird issue where I was trying to require <code>babel/polyfill</code> from some shared environment startup file and I got the error the user referenced - I think it might have had something to do with how babel orders imports versus requires but I'm unable to reproduce now. Anyway, moving <code>import 'babel/polyfill'</code> as the first line in both my client and server startup scripts fixed the problem.</p>

<p>Note that if you instead want to use <code>require('babel/polyfill')</code> I would make sure all your other module loader statements are also requires and not use imports - avoid mixing the two. In other words, if you have any import statements in your startup script, make <code>import babel/polyfill</code> the first line in your script rather than <code>require('babel/polyfill')</code>.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-33568284">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        54
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>This changed a bit in babel v6.</p>

<p>From the docs:</p>

<blockquote>
  <p>The polyfill will emulate a full ES6 environment. This polyfill is automatically loaded when using babel-node.</p>
</blockquote>

<p><strong>Installation:</strong><br />
<code>$ npm install babel-polyfill</code></p>

<p><strong>Usage in Node / Browserify / Webpack:</strong><br />
To include the polyfill you need to require it at the top of the entry point to your application.<br />
<code>require("babel-polyfill");</code></p>

<p><strong>Usage in Browser:</strong><br />
Available from the <code>dist/polyfill.js</code> file within a <code>babel-polyfill</code> npm release. This needs to be included before all your compiled Babel code. You can either prepend it to your compiled code or include it in a <code>&lt;script&gt;</code> before it.</p>

<p>NOTE: Do not <code>require</code> this via browserify etc, use <code>babel-polyfill</code>.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-37152576">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        15
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>If your package.json looks something like the following:</p>

<pre><code>  ...
  "devDependencies": {
    "babel": "^6.5.2",
    "babel-eslint": "^6.0.4",
    "babel-polyfill": "^6.8.0",
    "babel-preset-es2015": "^6.6.0",
    "babelify": "^7.3.0",
  ...</code></pre>

<p>And you get the <code>Cannot find module 'babel/polyfill'</code> error message, then you probably just need to change your import statement FROM:</p>

<pre><code>import "babel/polyfill";</code></pre>



<pre><code>import "babel-polyfill";</code></pre>

<p>And make sure it comes before any other <code>import</code> statement (not necessarily at the entry point of your application).</p>

<p>Reference:  <a href="https://babeljs.io/docs/usage/polyfill/" target="_blank">https://babeljs.io/docs/usage/polyfill/</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 11 '16 at 3:22
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-46175642">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<blockquote>
  <p>babel-polyfill allows you to use the full set of ES6 features beyond
  syntax changes. This includes features such as new built-in objects
  like Promises and WeakMap, as well as new static methods like
  Array.from or Object.assign.</p>
  
  <p>Without babel-polyfill, babel only allows you to use features like
  arrow functions, destructuring, default arguments, and other
  syntax-specific features introduced in ES6.</p>
</blockquote>

<p><a href="https://www.quora.com/What-does-babel-polyfill-do" target="_blank">https://www.quora.com/What-does-babel-polyfill-do</a></p>

<p><a href="https://hackernoon.com/polyfills-everything-you-ever-wanted-to-know-or-maybe-a-bit-less-7c8de164e423" target="_blank">https://hackernoon.com/polyfills-everything-you-ever-wanted-to-know-or-maybe-a-bit-less-7c8de164e423</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Sep 12 '17 at 11:50
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    




<div id="post-editor">

    <div> 
        <div>
            <div id="mdhelp">
    <ul id="mdhelp-tabs">
        <li>Links</li>
        <li>Images</li>
        <li>Styling/Headers</li>
        <li>Lists</li>
        <li>Blockquotes</li>
        
        
        <li><a href="/editing-help" target="_blank">advanced help »</a></li>
    </ul>
    
    

    
    
    

    

    

    

    
</div>
            
        </div>
    </div>

    
    

    

    


    
    
    



</div>

                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/node.js" title="show questions tagged 'node.js'" target="_blank">node.js</a> <a href="/questions/tagged/babeljs" title="show questions tagged 'babeljs'" target="_blank">babeljs</a> <a href="/questions/tagged/polyfills" title="show questions tagged 'polyfills'" target="_blank">polyfills</a> <a href="/questions/tagged/babel-polyfill" title="show questions tagged 'babel-polyfill'" target="_blank">babel-polyfill</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
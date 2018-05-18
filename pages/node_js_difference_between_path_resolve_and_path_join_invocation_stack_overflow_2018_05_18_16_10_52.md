<a href="https://stackoverflow.com/questions/35048686/difference-between-path-resolve-and-path-join-invocation">https://stackoverflow.com/questions/35048686/difference-between-path-resolve-and-path-join-invocation</a><div id="articleHeader"><h1>Difference between path.resolve and path.join invocation?</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        89
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="Click to mark as favorite question (click again to undo)" target="_blank">favorite</a>
        <div><b>19</b></div>


</div>

            </div>

            
<div>
    <div>

<p>Is there some difference between the following invocations?</p>

<pre><code>path.join(__dirname, 'app')</code></pre>



<pre><code>path.resolve(__dirname, 'app')</code></pre>

<p>Which one should be preferred?</p>
    </div>
    <div>
        <a href="/questions/tagged/node.js" title="show questions tagged 'node.js'" target="_blank">node.js</a> 
    </div>
    <div>
    

    <div>
        <div>
    <div>
        asked Jan 27 '16 at 21:46
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-39836259">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        124
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>The two functions deal with segments starting with <code>/</code> in very different ways; <code>join</code> will just concatenate it with the previous argument, however <code>resolve</code> will treat this as the root directory, and ignore all previous paths - think of it as the result of executing <code>cd</code> with each argument:</p>

<pre><code>path.join('/a', '/b') // Outputs '/a/b'

path.resolve('/a', '/b') // Outputs '/b'</code></pre>

<p>Another thing to note is that <code>path.resolve</code> will always result in an absolute URL, and will use your working directory as a base to resolve this path. But as <code>__dirname</code> is an absolute path anyway this doesn't matter in your case.</p>

<p>As for which one you should use, the answer is: it depends on how you want segments starting in <code>/</code> to behave - should they be simply joined or should they act as the new root?</p>

<p>If the other arguments are hard coded it really doesn't matter, in which case you should probably consider (a) how this line might change in future and (b) how consistent is it with other places in the code.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 3 '16 at 16:30
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-45542259">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>The default operations of file system path vary based on the operating system we need some thing that abstract it.
The <code>path</code> module provides utilities or API for working with file and directory
paths.
you can include it in your project using </p>

<pre><code>const path = require('path');</code></pre>

<p>The <code>path.join</code> and <code>path.resolve</code> are two different methods of the path module.</p>

<p>Both these methods accept a sequence of paths or path segments.</p>

<p>The <code>path.resolve()</code> method resolves a sequence of paths or path segments into an <em>absolute path</em>.</p>

<p>The <code>path.join()</code> method joins all given path segments together using the platform specific separator as a delimiter, then normalizes the resulting path.</p>

<p>In order to better understand and differentiate behaviours, let me explain it with different scenarios.</p>

<p><strong>1. If we don't supply any arguments to or empty string</strong></p>

<p>in my case, my filename is <code>index.js</code> and the current working directory is <code>E:\MyFolder\Pjtz\node</code></p>

<pre><code>const path = require('path');

console.log("path.join() : ", path.join());
// outputs .
console.log("path.resolve() : ", path.resolve());
// outputs current directory or equalent to __dirname</code></pre>

<p>and on running result is as below </p>

<pre><code>λ node index.js
path.join() :  .
path.resolve() :  E:\MyFolder\Pjtz\node</code></pre>

<p><em>The infernce from above experiemt is tha <code>path.resolve()</code> method will output the <strong>absolute path</strong> where as the <code>path.join()</code> returns . representing the current working directory or <strong>relative path</strong> if nothing is provided</em></p>

<p><strong>2. Adding a /path as any of arguments.</strong></p>

<pre><code>const path=require('path');

console.log("path.join() : " ,path.join('abc','/bcd'));
console.log("path.resolve() : ",path.resolve('abc','/bcd'));</code></pre>

<p>and the result is</p>

<pre><code>λ node index.js
path.join() :  abc\bcd
path.resolve() :  E:\bcd</code></pre>

<p><em>The inference we can found with this experiment is that <code>path.join()</code> only concatenates the input list with platform specific separator while the <code>path.resolve()</code> process the sequence of paths from right to left, with each subsequent path prepended until an absolute path is constructed.</em></p>

<p><code>path.join()</code> concatenates each argument with OS specific separators while <code>path.resolve()</code> will resolve each argument with root and produce output.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-45670522">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>1) path.resolve creates the absolute path.</strong></p>

<p>The method creates absoulte path <strong>from right to left</strong> until an absolute path is constructed. </p>

<p>For example:</p>

<pre><code>path.resolve('/a', 'b', 'c');     //    C:\a\b\c
path.resolve('/a', '/b', 'c');    //    C:\b\c
path.resolve('/a', '/b', '/c');   //    C:\c</code></pre>

<p>If absolute path is not generated, the method using current working directory:</p>

<p>For example:</p>

<pre><code>path.resolve('a', 'b', 'c');     //    C:\{current_working_directory}\a\b\c</code></pre>

<p><strong>2) path.join joins all path and the normalize the result</strong></p>

<p>For example:</p>

<pre><code>path.join('/a', '/b', '/c');   //   \a\b\c
path.join('/a', '/b', 'c');    //   \a\b\c
path.join('/a', 'b', 'c');     //   \a\b\c
path.join('a', 'b', 'c');      //   \a\b\c</code></pre>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/node.js" title="show questions tagged 'node.js'" target="_blank">node.js</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
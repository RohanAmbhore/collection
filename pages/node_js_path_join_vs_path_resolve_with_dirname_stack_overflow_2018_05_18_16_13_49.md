<a href="https://stackoverflow.com/questions/39110801/path-join-vs-path-resolve-with-dirname/39111164">https://stackoverflow.com/questions/39110801/path-join-vs-path-resolve-with-dirname/39111164</a><div id="articleHeader"><h1>path.join vs path.resolve with __dirname</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        46
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>6</b></div>


</div>

            </div>

            
<div>
    <div>

<p>Is there a difference when using <em>both</em> <code>path.join</code> and <code>path.resolve</code> with <code>__dirname</code> for resolving absolute path in Node.js?</p>

<p>Should one of them be preferred when being used like that (absolute path resolutions are 90% of use cases)?</p>



<pre><code>const absolutePath = path.join(__dirname, some, dir);</code></pre>



<pre><code>const absolutePath = path.resolve(__dirname, some, dir);</code></pre>

<p>Both methods normalize path.</p>

<p><em>This is not a duplicate of <a href="https://stackoverflow.com/questions/35048686/difference-between-path-resolve-and-path-join-invocation" target="_blank">this question</a> because the accepted answer is wrong.</em></p>
    </div>
    <div>
        <a href="/questions/tagged/node.js" title="show questions tagged 'node.js'" target="_blank">node.js</a> 
    </div>
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-39111164">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        54
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>Yes there is a difference between the functions but how you are using them in this case will result in the same outcome.</p>

<p><code>path.join</code> returns a normalized path by merging two paths together. It can return an absolute path, but it doesn't necessarily always do so.</p>

<p>For instance:</p>

<pre><code>path.join('app/libs/oauth', '/../ssl')</code></pre>

<p>resolves to <code>app/libs/ssl</code></p>

<p><code>path.resolve</code>, on the other hand, will resolve to an absolute path.</p>

<p>For instance, when you run:</p>

<pre><code>path.resolve('bar', '/foo');</code></pre>

<p>The path returned will be <code>/foo</code> since that is the first absolute path that can be constructed.</p>

<p>However, if you run:</p>

<pre><code>path.resolve('/bar/bae', '/foo', 'test');</code></pre>

<p>The path returned will be <code>/foo/test</code> again because that is the first absolute path that can be formed from right to left.</p>

<p>If you don't provide a path that specifies the root directory then the paths given to the <code>resolve</code> function are appended to the current working directory. So if your working directory was <code>/home/mark/project/</code>:</p>

<pre><code>path.resolve('test', 'directory', '../back');</code></pre>

<p>resolves to</p>

<p><code>/home/mark/project/test/back</code></p>

<p>Using <code>__dirname</code> gives an absolute path to your current working directory. When you use <code>path.resolve</code> or <code>path.join</code> they will return the same result if you give the same path following <code>__dirname</code>. In such cases it's really just a matter of preference.</p>
    </div>
    <div>
    
    
            


    <div>
       

    <div>
    <div>
        answered Aug 23 '16 at 21:44
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-45575007">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        4
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<pre><code>const absolutePath = path.join(__dirname, some, dir);</code></pre>



<pre><code>const absolutePath = path.resolve(__dirname, some, dir);</code></pre>

<p><code>path.join</code> will concatenate __dirname which is the directory name of the current file concatenated with values of <code>some</code> and <code>dir</code> with platform specific separator</p>

<p>where as </p>

<p><code>path.resolve</code> will process <code>__dirname</code> , <code>some</code> and <code>dir</code> i.e. from left to right prepending it by processing it.</p>

<p><strong>if any of the values of <code>some</code> or <code>dir</code> corresponds to a root path then the previous path will be omitted and process rest by considering it as root</strong></p>

<p>Inorder to better understand concept let me explain both little bit detailed as follows :-</p>

<p>The <code>path.join</code> and <code>path.resolve</code> are two different methods or functions of the path module provided by nodejs.</p>

<p>Where both accept a list of path but the difference comes in the result i.e. how they process these path.</p>

<p><code>path.join</code> concatenates all given path segments together using the platform specific separator as a delimiter, then normalizes the resulting path. while the <code>path.resolve()</code> process the sequence of paths from right to left, with each subsequent path prepended until an absolute path is constructed.</p>

<p><strong>When no arguments supplied</strong> </p>

<p>Following example will help you to clearly understand both concepts:-</p>

<p>my filename is <code>index.js</code> and the current working directory is <code>E:\MyFolder\Pjtz\node</code></p>

<pre><code>const path = require('path');

console.log("path.join() : ", path.join());
// outputs .
console.log("path.resolve() : ", path.resolve());
// outputs current directory or equalent to __dirname</code></pre>

<p>Result</p>

<pre><code>λ node index.js
path.join() :  .
path.resolve() :  E:\MyFolder\Pjtz\node</code></pre>

<p><em><code>path.resolve()</code> method will output the absolute path where as the <code>path.join()</code> returns . representing the current working directory if nothing is provided</em></p>

<p><strong>When some root path is passed as arguments</strong></p>

<pre><code>const path=require('path');

console.log("path.join() : " ,path.join('abc','/bcd'));
console.log("path.resolve() : ",path.resolve('abc','/bcd'));</code></pre>

<p>Result i</p>

<pre><code>λ node index.js
path.join() :  abc\bcd
path.resolve() :  E:\bcd</code></pre>

<p><em><code>path.join()</code> only concatenates the input list with platform specific separator while the <code>path.resolve()</code> process the sequence of paths from right to left, with each subsequent path prepended until an absolute path is constructed.</em></p>
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
        
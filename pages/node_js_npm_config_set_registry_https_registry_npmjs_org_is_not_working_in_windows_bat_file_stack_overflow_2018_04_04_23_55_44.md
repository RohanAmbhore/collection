<a href="https://stackoverflow.com/questions/22385092/npm-config-set-registry-https-registry-npmjs-org-is-not-working-in-windows/22390936">https://stackoverflow.com/questions/22385092/npm-config-set-registry-https-registry-npmjs-org-is-not-working-in-windows/22390936</a><div id="articleHeader"><h1>"npm config set registry https://registry.npmjs.org/" is not working in windows bat file</h1></div>

            

<div id="question">

    
        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        71
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>18</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I create a.bat on windows 7, the content of a.bat is:</p>

<pre><code>@echo off
npm config set registry https://registry.npmjs.org/</code></pre>

<p>and then run a.bat, but not working, I find the word "set" is special keyword for npm and bat, is there any methods to resolve this question?</p>
    </div>
    
    
</div>

                
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-22390936">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        103
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>You shouldn't change the npm registry using <code>.bat</code> files. 
Instead try to use modify the <code>.npmrc</code> file which is the configuration for <code>npm</code>.
The correct command for changing registry is</p>

<p><code>npm config set registry &lt;registry url&gt;</code></p>

<p>you can find more information with <code>npm help config</code> command, also check for privileges when and if you are running <code>.bat</code> files this way.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-29397307">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        31
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>You can change using the .bat make sure you run the call command prior, hopefully this helps anyone in future making similar .bat commands</p>

<pre><code>call npm config set registry https://registry.npmjs.org/</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Apr 1 '15 at 17:39
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-36692046">
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
<p>On npm version 3.7.3</p>

<p><code>npm set registry=http://whatever/</code></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Apr 18 '16 at 10:58
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-42792731">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        11
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>On version 4.4.1, you can use:</p>

<pre><code>npm config set @myco:registry http://reg.example.com</code></pre>

<p>Where @myco is your package scope. You can install package in this way:</p>

<pre><code>npm install @myco/my-package</code></pre>

<p>ref: <a href="https://docs.npmjs.com/misc/scope" target="_blank">https://docs.npmjs.com/misc/scope</a></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-43859193">
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
<p>We can also run npm install with <code>registry</code> options for multiple custom registry URLs.</p>

<pre><code>npm install --registry=https://registry.npmjs.org/ 
npm install --registry=https://custom.npm.registry.com/ </code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 9 '17 at 0:27
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-45204773">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Probably I am too late to answer. But if anybody need it, following works fine, as I have used it a lot of times.</p>

<pre><code>npm config set registry=https://registry.npmjs.com/</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jul 20 '17 at 3:46
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-45457379">
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
<p>By executing your .bat you are setting config for only that session not globally. When you open and another cmd prompt and run <code>npm install</code> that config will not set for this session so modify your .bat file as </p>

<pre><code>@echo off
npm config set registry https://registry.npmjs.org/
@cmd.exe /K</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 2 '17 at 9:50
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/node.js" title="show questions tagged 'node.js'" target="_blank">node.js</a> <a href="/questions/tagged/batch-file" title="show questions tagged 'batch-file'" target="_blank">batch-file</a> <a href="/questions/tagged/npm" title="show questions tagged 'npm'" target="_blank">npm</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
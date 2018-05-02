<a href="https://stackoverflow.com/questions/32832264/change-language-to-jsx-in-visual-studio-code">https://stackoverflow.com/questions/32832264/change-language-to-jsx-in-visual-studio-code</a><div id="articleHeader"><h1>Change language to JSX in Visual Studio Code</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        32
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>9</b></div>


</div>

            </div>

            
<div>
    <div>

<p>Visual Studio Code now <a href="https://code.visualstudio.com/Updates#_languages-jsx-colorization" target="_blank">supports JSX on 0.8 version</a>, but looks like the only way to activate it is with a <code>.jsx</code> file extension. It is not on the list to change the language mode manually, the nearest option is <code>JavaScriptReact</code>, but it doesn't parse the JSX tags.</p>

<p>I'm in a project with a lot of <code>.js</code> files with JSX and I can't change it.</p>

<p>Is there any other way to use JSX syntax without the <code>.jsx</code> extension?</p>
    </div>
    
    
</div>

                
    <div>
	    

        <div id="comments-link-32832264">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </div>        </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-37592711">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        75
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>Change your user settings or workspace settings as below:</p>

<pre><code>// Place your settings in this file to overwrite the default settings
{
    "files.associations": {
        "*.js": "javascriptreact"
    }
}
</code></pre>

<p>Note: You might need to restart VSCode.</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-37592711">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-32899368">
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
<p>I could do it, but "not React JS files" are also show with JavaScriptReact mode.</p>

<ol>
<li>open file C:\Program Files (x86)\Microsoft VS Code\resources\app\plugins\vs.language.javascript\syntaxes\javascriptreact.json
(probably, need to open with administrator privileges.)</li>
<li>change "jsx" to "js" in array "fileTypes".</li>
<li>restart app, close opened js files, and reopen.</li>
</ol>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-32899368">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-34683944">
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
<p>There is now a <a href="https://marketplace.visualstudio.com/items/eg2.js-is-jsx" target="_blank">VS Code extension that allows <code>.js</code> files to be treated as <code>.jsx</code> files</a>.</p>

<p>Unfortunately the readme for the extension also warns:</p>

<blockquote>
  <p>when you install this extension you will loose all the existing language support provided for .js files</p>
</blockquote>

<p>Fortunately VS Code is now very close to <a href="http://blogs.msdn.com/b/user_ed/archive/2016/01/11/visual-studio-code-new-features-4-language-improvements-javascript-typescript-jsx-amp-tsx.aspx" target="_blank">adopting Salsa</a>, which means soon the js-is-jsx issue should be completely resolved.</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-34683944">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-39835716">
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
<p>Took me a while to figure this out but – JSX is already part of Emmet – which is part of VS Code. I've told Emmet to also (additionally) make JSX snippets available in regular JS files.</p>

<p>Just put this in your settings file: </p>

<pre><code>"emmet.syntaxProfiles": {
    "javascript": "jsx"
}    
</code></pre>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-39835716">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-34029530">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Just install an extension:</p>

<ul>
<li>Press F1 (in Visual Studio Code)</li>
<li>Type "extension" in the appearing text field</li>
<li>Pick "Extensions: Install Extension"</li>
<li>Type "ext install jsx"</li>
<li>Restart Visual Studio Code</li>
</ul>

<p>Source:</p>

<p><a href="https://code.visualstudio.com/docs/editor/extension-gallery?pub=TwentyChung&ext=jsx" target="_blank">https://code.visualstudio.com/docs/editor/extension-gallery?pub=TwentyChung&ext=jsx</a>
<a href="https://marketplace.visualstudio.com/items/TwentyChung.jsx" target="_blank">https://marketplace.visualstudio.com/items/TwentyChung.jsx</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 1 '15 at 20:30
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-34029530">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-33844615">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -8
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Try using link on Mac or Linux.</p>

<pre><code>ln -s index.ios.js index.ios.jsx
</code></pre>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-33844615">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            <div>
                                
                                            <div>
        
                <div>
                    <div>
                        <h3>Sign up or <a href="/users/login?ssrc=question_page&returnurl=https%3a%2f%2fstackoverflow.com%2fquestions%2f32832264%2fchange-language-to-jsx-in-visual-studio-code%23new-answer" id="login-link" target="_blank">log in</a></h3>
                        
                        <div>
                             Sign up using Google
                        </div>
                        <div>
                             Sign up using Facebook
                        </div>
                        <div>
                             Sign up using Email and Password
                        </div>
                    </div>
                    
                    
                    
                    
                    <div>
                                <h3>Post as a guest</h3>
    <div>
        <table>
        <tbody><tr>
                    <td>
                <div>
                    <label>Name</label>
                    
                </div>
                <div>
                    <label>Email</label>
                    
                </div>
            </td>
        </tr>
        </tbody></table>
    </div>

                    </div>
                </div>
            </div>
            
            

                            </div>

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>

<p>
By posting your answer, you agree to the <a href="https://stackexchange.com/legal/privacy-policy" name="privacy" target="_blank">privacy policy</a> and <a href="https://stackexchange.com/legal/terms-of-service" name="tos" target="_blank">terms of service</a>.</p>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/react-jsx" title="show questions tagged 'react-jsx'" target="_blank">react-jsx</a> <a href="/questions/tagged/visual-studio-code" title="show questions tagged 'visual-studio-code'" target="_blank">visual-studio-code</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
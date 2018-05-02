<a href="https://stackoverflow.com/questions/31529772/how-to-set-app-icon-for-electron-atom-shell-app">https://stackoverflow.com/questions/31529772/how-to-set-app-icon-for-electron-atom-shell-app</a><div id="articleHeader"><h1>How to set app icon for Electron</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        84
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>17</b></div>


</div>

            </div>

            
<div>
    <div>

<p>How do you set the app icon for your Electron app?</p>

<p>I am trying <code>BrowserWindow({icon:'path/to/image.png'});</code> but it does not work.</p>

<p>Do I need to pack the app to see the effect?</p>
    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-31538436">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        105
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>Setting the <code>icon</code> property when creating the <code>BrowserWindow</code> only has an effect on Windows and Linux.</p>

<p>To set the icon on OS X, you can use <a href="https://github.com/maxogden/electron-packager" target="_blank">electron-packager</a> and set the icon using the <code>--icon</code> switch.</p>

<p>It will need to be in .icns format for OS X. There is an <a href="https://iconverticons.com/online/" target="_blank">online icon converter</a> which can create this file from your .png.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-36517446">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        24
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Below is the solution that i have :</p>

<pre><code>mainWindow = new BrowserWindow({width: 800, height: 600,icon: __dirname + '/Bluetooth.ico'});
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Apr 9 '16 at 13:33
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-40690900">
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
<p>You can do it for macOS, too. Ok, not through code, but with some simple steps:</p>

<ol>
<li>Find the .icns file you want to use, open it and copy it via Edit menu</li>
<li>Find the electron.app, usually in node_modules/electron/dist</li>
<li>Open the information window</li>
<li>Select the icon on the top left corner (gray border around it)</li>
<li>Paste the icon via cmd+v</li>
<li>Enjoy your icon during development :-)</li>
</ol>

<p><a href="https://i.stack.imgur.com/HllX2.png" target="_blank" class="readableLinkWithMediumImage"><img src="https://i.stack.imgur.com/HllX2.png" alt="enter image description here" /></a></p>

<p>Actually it is a general thing not specific to electron. You can change the icon of many macOS apps like this.</p>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/icons" title="show questions tagged 'icons'" target="_blank">icons</a> <a href="/questions/tagged/electron" title="show questions tagged 'electron'" target="_blank">electron</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
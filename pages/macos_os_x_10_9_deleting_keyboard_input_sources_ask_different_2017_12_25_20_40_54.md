<a href="https://apple.stackexchange.com/questions/108622/os-x-10-9-deleting-keyboard-input-sources">https://apple.stackexchange.com/questions/108622/os-x-10-9-deleting-keyboard-input-sources</a><div id="articleHeader"><h1><a href="/questions/108622/os-x-10-9-deleting-keyboard-input-sources" target="_blank">OS X 10.9: Deleting Keyboard Input Sources</a></h1></div>
            

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        3
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>2</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>This is really similar to:
<a href="https://apple.stackexchange.com/questions/44921/how-to-remove-or-disable-a-default-keyboard-layout/" target="_blank">How to remove or disable a default keyboard layout?</a>
However, I am new here and have no ability to comment or make remarks towards this to voice further problems.</p>

<p>In OS X 10.9, I need to remove input sources in System Preferences &gt; Language and Region &gt; Keyboard Preferences &gt; Input Source.</p>

<p>To be clear, I want these gone completely; if I were to click the add button then I want there to be nothing but the basic English layout available. </p>

<hr />

<p>**Edit:
The solution can be as dangerous as editing near-/root-level files in the OS as long as there's a possible solutions</p>

<p>If no possible solution can be found can anyone recommend third-party software or a way to lock system preferences?**</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-108622">
		        <table>
                    <tbody>



    <tr id="comment-135993">
        <td>
            
        </td>
        <td>
            <div>
                Why would you want to do that anyway?
                    – <a href="/users/27581/shane-hsu" title="1,540 reputation" target="_blank">Shane Hsu</a>
                <a href="#comment135993_108622" target="_blank">Jan 7 '14 at 6:25</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-108622">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-127979">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If others got here searching for how to disable all input sources except a custom keyboard layout, you can edit the <code>com.apple.HIToolbox</code> plist:</p>

<ol>
<li>Change the current input source to your custom keyboard layout.</li>
<li>Open <code>~/Library/Preferences/com.apple.HIToolbox.plist</code> (in 10.9) or <code>~/Library/Preferences/ByHost/com.apple.HIToolbox.*.plist</code> (in 10.8 and earlier). You can convert the plist to XML with <code>plutil -convert xml1</code>.</li>
<li>Remove the input source or input sources you want to disable from the <code>AppleEnabledInputSources</code> dictionary. If there is an <code>AppleDefaultAsciiInputSource</code> key, remove it.</li>
<li>Restart.</li>
</ol>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 18 '14 at 13:51
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-127979">
		        <table>
                    <tbody>



    <tr id="comment-172897">
        <td>
            
        </td>
        <td>
            <div>
                if you have Xcode installed, you can directly <code>open ~/Library/Preferences/com.apple.HIToolbox.plist</code> (in 10.9) from a terminal konsole. The items I had to remove to get rid of the keyboard layouts are those with <code>InputSourceKind</code> equal to <code>Keyboard Layout</code>
                    – <a href="/users/16220/andre-holzner" title="201 reputation" target="_blank">Andre Holzner</a>
                <a href="#comment172897_127979" target="_blank">Sep 24 '14 at 8:12</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-382836">
        <td>
            
        </td>
        <td>
            <div>
                Again, I'm pretty sure this is not removing the keyboard from the list that you can find in "Keyboard Preferences", "Input Sources", and then the "+" button.
                    – <a href="/users/122223/flimm" title="402 reputation" target="_blank">Flimm</a>
                <a href="#comment382836_127979" target="_blank">Oct 20 at 12:56</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-127979">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-108632">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>I not completely sure that's what you're looking for. But if you want to remove some input sources. You just have to select them then click the "minus" button. </p>

<p>You can delete them all but one. There has to be a least one input source. In your case one of the english input sources. </p>

<p><div class="readableLargeImageContainer float"><img src="https://i.stack.imgur.com/nv4zW.png" alt="enter image description here" /></div></p>

<p>Edit : OP want's to remove all the input source from the list (accessible by clicking the "+" button). And that's not possible. </p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-108632">
		        <table>
                    <tbody>



    <tr id="comment-127317">
        <td>
            
        </td>
        <td>
            <div>
                From @user61808 : No this does not delete the input sources. This just removes them from the list but they can still be re-added via the plus button. They need to be deleted, not hidden.
                    – <a href="/users/21416/matthieu-riegler" title="15,068 reputation" target="_blank">Matthieu Riegler</a>
                <a href="#comment127317_108632" target="_blank">Nov 7 '13 at 1:33</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-127322">
        <td>
            
        </td>
        <td>
            <div>
                In that case can anyone think of any third party options for locking system preferences? Thusly, does anyone know the root of the input sources to where I could simply delete them (I understand this would be os/root level and is dangerous).
                    – <a href="/users/61808/user61808" title="16 reputation" target="_blank">user61808</a>
                <a href="#comment127322_108632" target="_blank">Nov 7 '13 at 2:20</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-127356">
        <td>
            
        </td>
        <td>
            <div>
                System preferences &gt; Security & Privacy &gt; Advanced &gt; Require password to access system wide preferences.
                    – <a href="/users/21416/matthieu-riegler" title="15,068 reputation" target="_blank">Matthieu Riegler</a>
                <a href="#comment127356_108632" target="_blank">Nov 7 '13 at 11:31</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-108632">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


        






                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/macos" title="show questions tagged 'macos'" target="_blank">macos</a> <a href="/questions/tagged/keyboard" title="show questions tagged 'keyboard'" target="_blank">keyboard</a> <a href="/questions/tagged/preferences" title="show questions tagged 'preferences'" target="_blank">preferences</a> <a href="/questions/tagged/input-source" title="show questions tagged 'input-source'" target="_blank">input-source</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="https://stackoverflow.com/questions/5921413/difference-between-e-target-and-e-currenttarget">https://stackoverflow.com/questions/5921413/difference-between-e-target-and-e-currenttarget</a><div id="articleHeader"><h1>Difference between e.target and e.currentTarget</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        193
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>61</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I don't understand the difference, they both seem the same but I guess they are not.</p>

<p>Any examples of when to use one or the other would be appreciated.</p>
    </div>
    
    
</div>

                        <div>
                <div>
        <h2>                    <b>protected</b> by <a href="/users/2435473/pankaj-parkar" target="_blank">Pankaj Parkar</a> Sep 18 '15 at 10:48
</h2>
        <p>
This question is protected to prevent "thanks!", "me too!", or spam answers by new users. 
To answer it, you must have earned at least 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).</p>
    </div>
            </div>
    
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-5921615">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        164
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>Ben is completely correct in his answer - so keep what he says in mind. What I'm about to tell you isn't a full explanation, but it's a very easy way to remember how <code>e.target</code>, <code>e.currentTarget</code> work in relation to mouse events and the display list:</p>

<p><code>e.target</code> = The thing under the mouse (as ben says... the thing that triggers the event).
<code>e.currentTarget</code> = The thing before the dot... (see below)</p>

<p>So if you have 10 buttons inside a clip with an instance name of "btns" and you do:</p>

<pre><code>btns.addEventListener(MouseEvent.MOUSE_OVER, onOver);
// btns = the thing before the dot of an addEventListener call
function onOver(e:MouseEvent):void{
  trace(e.target.name, e.currentTarget.name);
}</code></pre>

<p><code>e.target</code> will be one of the 10 buttons and <code>e.currentTarget</code> will always be the "btns" clip.</p>

<p>It's worth noting that if you changed the MouseEvent to a ROLL_OVER or set the property <code>btns.mouseChildren</code> to false, <code>e.target</code> and <code>e.currentTarget</code> will both always be "btns".</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-5921528">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        306
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><code>e.target</code> is what triggers the event dispatcher to trigger and <code>e.currentTarget</code> is what you assigned your listener to. </p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-5923314">
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
<p>It's worth noting that event.target can be useful, for example, for using a single listener to trigger different actions. Let's say you have the typical "menu" sprite with 10 buttons inside, so instead of doing:</p>

<pre><code>menu.button1.addEventListener(MouseEvent.CLICK, doAction1);
menu.button2.addEventListener(MouseEvent.CLICK, doAction2);
etc...</code></pre>

<p>You can simply do:</p>

<pre><code>menu.addEventListener(MouseEvent.CLICK, doAction);</code></pre>

<p>And trigger a different action within doAction(event) depending on the event.target (using it's name property, etc...)</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 7 '11 at 19:02
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-15996352">
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
<p>e.currentTarget would always return the component onto which the event listener is added.</p>

<p>On the other hand, e.target can be the component itself or any direct child or grand child or grand-grand-child and so on who received the event. In other words, e.target returns the component which is on top in the Display List hierarchy and must be in the child hierarchy or the component itself.</p>

<p>One use can be when you have several Image in Canvas and you want to drag Images inside the component but Canvas. You can add a listener on Canvas and in that listener you can write the following code to make sure that Canvas wouldn't get dragged.</p>

<pre><code>function dragImageOnly(e:MouseEvent):void
{
    if(e.target==e.currentTarget)
    {
        return;
     }
     else
     {
        Image(e.target).startDrag();
     }
}</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Apr 14 '13 at 6:21
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-18632787">
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
<p>make an example:</p>

<pre><code>var body = document.body,
    btn = document.getElementById( 'id' );
body.addEventListener( 'click', function( event ) {
    console.log( event.currentTarget === body );
    console.log( event.target === btn );
}, false );</code></pre>

<p>when you click 'btn', and 'true' and 'true' will be appeared!</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Sep 5 '13 at 9:37
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-19548905">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        14
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><code>e.currentTarget</code> is always the element the event is actually bound do. <code>e.target</code> is the element the event originated from, so <code>e.target</code> could be a child of <code>e.currentTarget</code>, or <code>e.target</code> could be === <code>e.currentTarget</code>, depending on how your markup is structured.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 23 '13 at 17:52
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-29328767">
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
<ul>
<li>e.target is element, which you f.e. click</li>
<li>e.currentTarget is element with added event listener.</li>
</ul>

<p>If you click on child element of button, its better to use currentTarget to detect buttons attributes, in CH its sometimes problem to use e.target.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 29 '15 at 11:53
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-40187434">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>I like visual answers. </p>

<p><a href="https://i.stack.imgur.com/pxWr6.png" target="_blank" class="readableLinkWithMediumImage"><img src="https://i.stack.imgur.com/pxWr6.png" alt="enter image description here" /></a></p>

<p>When you click <code>#btn</code>, two event handlers get called and they output what you see in the picture.</p>

<p>Demo here: <a href="https://jsfiddle.net/ujhe1key/" target="_blank">https://jsfiddle.net/ujhe1key/</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 22 '16 at 1:26
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/actionscript-3" title="show questions tagged 'actionscript-3'" target="_blank">actionscript-3</a> <a href="/questions/tagged/events" title="show questions tagged 'events'" target="_blank">events</a> <a href="/questions/tagged/event-handling" title="show questions tagged 'event-handling'" target="_blank">event-handling</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
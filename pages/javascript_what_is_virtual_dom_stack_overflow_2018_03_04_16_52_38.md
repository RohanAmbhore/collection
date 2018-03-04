<a href="https://stackoverflow.com/questions/21965738/what-is-virtual-dom">https://stackoverflow.com/questions/21965738/what-is-virtual-dom</a><div id="articleHeader"><h1>What is Virtual DOM?</h1></div>

            

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

<p>Recently, I looked at Facebook's <a href="https://facebook.github.io/react/" target="_blank">React</a> framework. It uses a concept called "the Virtual DOM," which I didn't really understand.</p>

<p>What is the Virtual DOM? What are the advantages?</p>
    </div>
    
    
</div>

                
    <div>
	    <div id="comments-21965738">
                <ul>



    <li id="comment-33282935">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                I believe Virtual DOM is talking about nodes that are not in the normal DOM.
                    – <a href="/users/283863/derek-%e6%9c%95%e6%9c%83%e5%8a%9f%e5%a4%ab" title="55,570 reputation" target="_blank">Derek 朕會功夫</a>
                <a href="#comment33282935_21965738" target="_blank">Feb 23 '14 at 8:08</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-47866973">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                I agree with the above sentiments with regard to moderation. Moreover, I believe this is a very valid and useful question. "Virtual DOM" is often referenced, but rarely defined.
                    – <a href="/users/527333/btiernay" title="5,657 reputation" target="_blank">btiernay</a>
                <a href="#comment47866973_21965738" target="_blank">Apr 25 '15 at 21:38</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-52845679">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                I could not understand this with my limited web experience until reading the <a href="https://scotch.io/tutorials/learning-react-getting-started-and-concepts" target="_blank">scotch.io</a> tutorial to get started. They've done a great job.
                    – <a href="/users/1751090/rachael" title="986 reputation" target="_blank">Rachael</a>
                <a href="#comment52845679_21965738" target="_blank">Sep 10 '15 at 3:52</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>        </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-21965987">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        97
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>React creates a tree of custom objects representing a part of the DOM. For example, instead of creating an actual DIV element containing a UL element, it creates a React.div object that contains a React.ul object. It can manipulate these objects very quickly without actually touching the real DOM or going through the DOM API. Then, when it renders a component, it uses this virtual DOM to figure out what it needs to do with the real DOM to get the two trees to match.</p>

<p>You can think of the virtual DOM like a blueprint. It contains all the details needed to construct the DOM, but because it doesn't require all the heavyweight parts that go into a real DOM, it can be created and changed much more easily.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Feb 23 '14 at 8:35
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-21965987">
                <ul>



    <li id="comment-63865723">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Can this be used for the entire DOM, instead of just a part of it?
                    – <a href="/users/4026523/hipkiss" title="134 reputation" target="_blank">hipkiss</a>
                <a href="#comment63865723_21965987" target="_blank">Jul 6 '16 at 10:26</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-71637218">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                It's basically abstraction over abstraction which in the end what react does it look for the the reference in its object model tree, select the real node in the html and tinker with it. The sound is great <code>virtual dom</code>, but it's nothing fancy and overhype.
                    – <a href="/users/1682607/syarul" title="1,336 reputation" target="_blank">syarul</a>
                <a href="#comment71637218_21965987" target="_blank">Feb 15 '17 at 1:07</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-40693994">
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
<p>Let's take an example — though a very naive one: If you have something messed up in a room in your home and you need to clean it, what will be your first step? Will you be cleaning your room which is messed up or the whole house? The answer is definitely that you will be cleaning only the room which requires the cleaning. That's what the virtual DOM does.</p>

<p>Ordinary JS traverses or renders the whole DOM instead of rendering only the part which requires changes.</p>

<p>So whenever you have any changes, as in you want to add another <code>&lt;div&gt;</code> to your DOM then the virtual DOM will be created which actually does not do any changes in the actual DOM. Now with this virtual DOM, you will be checking the difference between this and your current DOM. And only the part which is different (in this case the new <code>&lt;div&gt;</code>) will be added instead of re-rendering the whole DOM.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-43645128">
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
<p>What is the virtual DOM?</p>

<p>The virtual DOM is an in-memory representation of the real DOM elements generated by React components before any changes are made to the page.</p>

<p><a href="https://i.stack.imgur.com/Y7nsK.jpg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/Y7nsK.jpg" alt="enter image description here" /></div></a></p>

<p>It’s a step that happens between the render function being called and the displaying of elements on the screen.</p>

<p>A component’s render method returns some markup, but it’s not the final HTML yet. It’s the in-memory representation of what will become real elements (this is step 1). Then that output will be transformed into real HTML, which is what gets displayed in the browser (This is step 2).</p>

<p>So why go through all this to generate a virtual DOM?
Simple answer — This is what allows react to be fast. It does this by means of virtual DOM diffing. Comparing two virtual trees — old and new — and make only the necessary changes into the real DOM.</p>

<p><a href="https://medium.com/@nerimbarakat/intro-to-react-2-41b84dd74b5d" target="_blank">Source from Intro To React #2</a></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-46981568">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Virtual DOM is an abstraction of the HTML DOM that selectively renders subtrees of nodes based upon state changes. It does the least amount of DOM manipulation possible in order to keep your components up to date.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 27 '17 at 18:44
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-47406893">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>A <code>virtual DOM</code>(VDOM) is not a new concept: <a href="https://github.com/Matt-Esch/virtual-dom" target="_blank">https://github.com/Matt-Esch/virtual-dom</a></strong>. </p>

<p>VDOM is a strategically to update DOM without redrawing all the nodes in a single page application. Finding a node in tress structure is easy but DOM tree for an SPA app can be drastically huge. Finding and updating a node/nodes in case of an event is not time efficient. </p>

<p>VDOM solve this problem by creating a high label abstraction of actual dom. <strong>The VDOM is a high level lightweight in-memory tree representation of actual DOM.</strong> </p>

<p>For example, consider adding a node in DOM; react keep a copy of VDOM in memory</p>

<ol>
<li>Create a VDOM with a new state  </li>
<li>Compare it with older VDOM using diffing.</li>
<li>Update only differ nodes in real DOM.  </li>
<li>Assign new VDOM as older VDOM.</li>
</ol>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Nov 21 '17 at 6:50
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-47887021">
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
<p><strong>How does the Virtual DOM work?</strong></p>

<p>Imagine you had an object that you modeled around a person. It had every relevant property a person could possibly have, and mirrored the persons current state. This is basically what React does with the DOM.</p>

<p>Now think about if you took that object and made some changes. Added a mustache, some sweet biceps and Steve Buscemi eyes. In React-land, when we apply these changes, two things take place. First, React runs a "<strong>diffing</strong>" algorithm, which identifies what has changed. The second step is <strong>reconciliation</strong>, where it updates the DOM with the results of diff.</p>

<p>The way React works, rather than taking the real person and rebuilding them from the ground up, it would only change the face and the arms. This means that if you had text in an input and a render took place, as long as the input's parent node wasn't scheduled for reconciliation, the text would stay undisturbed.</p>

<p>Because React is using a fake DOM and not a real one, it also opens up a fun new possibility. We can render that fake DOM on the server, and boom, server side React views.</p>

<p><a href="https://scotch.io/tutorials/learning-react-getting-started-and-concepts" target="_blank">Reference</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 19 '17 at 12:26
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/reactjs" title="show questions tagged 'reactjs'" target="_blank">reactjs</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
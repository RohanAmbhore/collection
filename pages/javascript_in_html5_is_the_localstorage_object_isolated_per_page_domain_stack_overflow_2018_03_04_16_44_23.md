<a href="https://stackoverflow.com/questions/4201239/in-html5-is-the-localstorage-object-isolated-per-page-domain">https://stackoverflow.com/questions/4201239/in-html5-is-the-localstorage-object-isolated-per-page-domain</a><div id="articleHeader"><h1>In HTML5, is the localStorage object isolated per page/domain?</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        120
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>18</b></div>


</div>

            </div>

            
<div>
    <div>

<p>Is the HTML5 localStorage object isolated per page/domain? I am wondering because of how I would name localStorage keys. Do I need a separate prefix? Or can I name them whatever I want?</p>
    </div>
    
    <div>
    

    <div>
        <div>
    <div>
        asked Nov 17 '10 at 3:33
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
    <div>
	    <div id="comments-4201239">
                <ul>



    <li id="comment-49352991">
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
                Does the domain include the port number?
                    – <a href="/users/365261/tony-ohagan" title="14,136 reputation" target="_blank">Tony O'Hagan</a>
                <a href="#comment49352991_4201239" target="_blank">Jun 4 '15 at 13:01</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>        </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-4201249">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        135
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>It's per domain (the same segregation rules as the <a href="http://en.wikipedia.org/wiki/Same-origin_policy#Origin_determination_rules" target="_blank">same origin policy</a>), to make it per-page you'd have to use a key based on the <code>location</code>, or some other approach. </p>

<p>You don't <em>need</em> a prefix, use one if you need it though.  Also, yes, you can name them whatever you want.</p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-4201249">
                <ul>



    <li id="comment-4554297">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
    <li id="comment-58097100">
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
                It's unique per <code>protocol://host:port</code> combination.
                    – <a href="/users/455988/thasmo" title="1,840 reputation" target="_blank">Thasmo</a>
                <a href="#comment58097100_4201249" target="_blank">Feb 3 '16 at 23:48</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-65958941">
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
                I'm commenting here to confirm that it's helpful to know that the port is relevant in the scoping. Consider: dev server, <code>localhost</code>.
                    – <a href="/users/340947/steven-lu" title="16,828 reputation" target="_blank">Steven Lu</a>
                <a href="#comment65958941_4201249" target="_blank">Sep 4 '16 at 2:38</a>
                        
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-4242999">
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
<p>Yeah, each domain/subdomain has a different <strong>localStorage</strong> and you can call the keys whatever you want (prefix is not required).</p>

<p>To get a key you can use the method key(index) such as </p>

<pre><code>localStorage.key(0);</code></pre>

<p>There was an object called <strong>globalStorage</strong> before where you could have multiple localStorages, but it's been deprecated from the specs</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-5510376">
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
<p>I'd always use a prefix, just to avoid potential collisions with user scripts - which could use localStorage too.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Apr 1 '11 at 7:30
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-5510376">
                <ul>



    <li id="comment-11786599">
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
                IMO It's the user scripts who should avoid collisions, not the pages. In my user script I'm using a prefix named after the script.
                    – <a href="/users/124119/camilo-martin" title="17,118 reputation" target="_blank">Camilo Martin</a>
                <a href="#comment11786599_5510376" target="_blank">Feb 18 '12 at 4:43</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-7762913">
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
<p>It is available anywhere on that domain as Nick suggested, as an alternative there is sessionStorage works slightly differently in that it is distinct to the browser window itself.  That is to say that other tabs or windows on the same domain do not have access to that same copy of the storage object.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 14 '11 at 4:05
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-41856313">
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
<p>The stores are <em>per origin</em>, where origin is the same as for the <a href="http://en.wikipedia.org/wiki/Same_origin_policy" target="_blank">Same Origin Policy</a> (a combination of schema [<code>http</code> vs. <code>https</code>, etc.], port, and host). From <a href="https://www.w3.org/TR/webstorage/" target="_blank">the spec</a>:</p>

<blockquote>
  <p>Each top-level browsing context has a unique set of session storage areas, one for each origin.</p>
</blockquote>

<p>Thus, the storage for <code>http://a.example.com</code> and the storage for <code>http://b.example.com</code> are separate (and they're both separate from <code>http://stackoverflow.com</code>) as those are all different hosts. Similarly, <code>http://example.com:80</code> and <code>http://example.com:8080</code> and <code>https://example.com</code> are all different origins.</p>

<p>There is no mechanism built into web storage that allows one origin to access the storage of another.</p>

<p>Note that it's <em>origin</em>, not URL, so <code>http://example.com/page1</code> and <code>http://example.com/page2</code> both have access to the storage for <code>http://example.com</code>.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 25 '17 at 16:09
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-45150432">
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
<p>As others have pointed out, localStorage is unique per protocol, host & port. If you want a handy way to control your storage with prefixed keys, I suggest <a href="https://github.com/macmcmeans/localDataStorage" target="_blank">localDataStorage</a>.</p>

<p>Not only does it help enforce segmented shared storage within the same domain by prefixing keys, it also transparently stores javascript data types (Array, Boolean, Date, Float, Integer, String and Object), provides lightweight data obfuscation, automatically compresses strings, and facilitates query by key (name) as well as query by (key) value.</p>

<p>[DISCLAIMER] I am the author of the utility [/DISCLAIMER]</p>

<p>Examples:</p>

<pre><code>// instantiate our first storage object
// internally, all keys will use the specified prefix, i.e. passphrase.life
var localData = localDataStorage( 'passphrase.life' );

localData.set( 'key1', 'Belgian' )
localData.set( 'key2', 1200.0047 )
localData.set( 'key3', true )
localData.set( 'key4', { 'RSK' : [1,'3',5,'7',9] } )
localData.set( 'key5', null )

localData.get( 'key1' )   --&gt;   'Belgian'
localData.get( 'key2' )   --&gt;   1200.0047
localData.get( 'key3' )   --&gt;   true
localData.get( 'key4' )   --&gt;   Object {RSK: Array(5)}
localData.get( 'key5' )   --&gt;   null


// instantiate our second storage object
// internally, all keys will use the specified prefix, i.e. prismcipher.com
var localData2 = localDataStorage( 'prismcipher.com' );

localData2.set( 'key1', 123456789 )  // integer

localData2.get( 'key1' )   --&gt;   123456789</code></pre>

<p>As you can see, primitive values are respected, and you can create several instances to control your storage.</p>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/html5" title="show questions tagged 'html5'" target="_blank">html5</a> <a href="/questions/tagged/local-storage" title="show questions tagged 'local-storage'" target="_blank">local-storage</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="https://stackapps.com/questions/6530/unable-to-get-access-token">https://stackapps.com/questions/6530/unable-to-get-access-token</a><div id="articleHeader"><h1><a href="/questions/6530/unable-to-get-access-token" target="_blank">Unable to get access token</a></h1></div>
            

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        9
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="Click to mark as favorite question (click again to undo)" target="_blank">favorite</a>
        <div><b>4</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I am trying to get a non-expiry access token, like so:</p>

<pre><code>https://stackexchange.com/oauth?scope=no_expiry&redirect_uri={{some_uri}}&client_id={{some_value}}
</code></pre>

<p>I am repeatedly getting the error:</p>

<blockquote>
  <p><strong>Application Login Failure</strong><br />
  An error occurred while login into an application. </p>
  
  <p><strong>Error Details</strong><br />
  error description: Cannot return to provided redirect_uri</p>
</blockquote>

<p>I have tried several values for `redirect_uri, such as:</p>

<ul>
<li><code>https://www.yahoo.com/</code><br />
and</li>
<li><code>10.**.**.**/myscript.php</code> </li>
</ul>

<p>None of them seem to be working. </p>
    </div>
    
    
</div>

                
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-6531">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>Refer to <a href="http://api.stackexchange.com/docs/authentication" target="_blank">the Stack Exchange API, <strong>Authentication</strong> docs</a>.  It <em>looks</em> like you are trying to authenticate using either a server you do not control, or a local server that is not on the public internet.</p>

<p>Crucial Points:</p>

<ol>
<li><p><strong>Do not specify a <code>redirect_uri</code> to any server that you do not control!!!</strong><br />
When you use something like <code>redirect_uri=https://www.yahoo.com/</code>, then a third party host has you, or your user's, credentials!  That page/server will see a request like:</p>

<pre><code>https://www.yahoo.com/#access_token=X0duhxxxxxxxxxxxNvfDbQ%29%29&expires=86399
</code></pre>

<p>It can then use that <code>access_token</code> to do unspeakable evil.</p>

<p><strong>This is a major breach of both security and trust!</strong>  <sub>(Frankly, if you or your app are caught doing this, lifetime bans should be issued.  Legal action may even be appropriate in some cases.)</sub></p></li>
<li><p>The value you <strong><a href="https://stackapps.com/apps/oauth/" target="_blank">set for <code>OAuth Domain</code></a> must match the <code>redirect_uri</code>.</strong></p>

<p>So, if you use, <code>redirect_uri=http://10.0.0.86/myscript.php</code>,<br />
then you must set <code>OAuth Domain</code> to <code>10.0.0.86</code>.</p></li>
<li><p><strong>If you do not have your own server</strong>:</p>

<ol>
<li>Use the "implicit OAuth 2.0 flow" (Client side).  Activate <code>Enable Client Side OAuth Flow</code> in your app's control panel.</li>
<li>Leave <code>Disable Desktop Application OAuth Redirect Uri</code> unchecked.</li>
<li>Set <code>OAuth Domain</code> to <code>stackexchange.com</code>.</li>
<li>Use <code>redirect_uri=https://stackexchange.com/oauth/login_success</code>.
</li>
</ol></li>
<li><p>Be sure to use <code>GET</code> requests for implicit (client side) OAuth and <code>POST</code> for explicit (server-side) OAuth.</p></li>
</ol>

<p>
When the authentication is successful, the <code>access_token</code> will be in the <code>location.hash</code> of the redirected page.  For example:</p>

<pre><code>https://stackexchange.com/oauth/login_success#access_token=5bcPtLjiyuySD7WeKSo3Mw))&expires=86399
</code></pre>
    </div>
    
</div>
    
    <div>
	    <div id="comments-6531">
                <ul>



    <li id="comment-14149">
        
        <div>
            <div>
                So i just need security token for one time. Instagram/Facebook use any redirect_uri and provide token on the URL itself. StackApps following the same model, i was expecting that any URL should work. Will try the point 2/3 and will update. Thanks for answering.
                    – <a href="/users/34257/user34257" title="115 reputation" target="_blank">user34257</a>
                <a href="#comment14149_6531" target="_blank">Aug 14 '15 at 4:18</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-14150">
        
        <div>
            <div>
                The token <i>is</i> returned in the URL (hash). And, even for Instagram/Facebook it's a major security breach to use a 3rd-party URL.
                    – <a href="/users/7653/brock-adams" title="9,007 reputation" target="_blank">Brock Adams</a>
                <a href="#comment14150_6531" target="_blank">Aug 14 '15 at 4:25</a>
                        
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/support" title="show questions tagged 'support'" target="_blank">support</a> <a href="/questions/tagged/api" title="show questions tagged 'api'" target="_blank">api</a> <a href="/questions/tagged/api-v2" title="show questions tagged 'api-v2'" target="_blank">api-v2</a> <a href="/questions/tagged/authentication" title="show questions tagged 'authentication'" target="_blank">authentication</a> <a href="/questions/tagged/oauth2" title="show questions tagged 'oauth2'" target="_blank">oauth2</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="https://stackoverflow.com/questions/12948809/trying-to-get-app-access-token">https://stackoverflow.com/questions/12948809/trying-to-get-app-access-token</a><div id="articleHeader"><h1>trying to get app access token</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        42
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>20</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I tried to get an app-access-token for my facebook app with this code:</p>

<pre><code>APP_ACCESS_TOKEN = FB.api(
    "oauth/access_token",
    {client_id: APP_ID, client_secret: APP_SECRET_CODE, redirect_uri: uri},
    function(response){
    console.log(response);
});
</code></pre>

<p>which should be like:</p>

<pre><code>GET https://graph.facebook.com/oauth/access_token?
        client_id=YOUR_APP_ID
       &client_secret=YOUR_APP_SECRET
       &redirect_uri=uri
</code></pre>

<p>but i get an error:</p>

<pre><code>code: 1
message: "Missing authorization code"
type: "OAuthException"
</code></pre>

<p>What is the authorization code and how can i get it?</p>
    </div>
    
    <div>
    

    <div>
        <div>
    <div>
        asked Oct 18 '12 at 6:58
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
    <div>
	    <div id="comments-12948809">
                <ul>



    <li id="comment-32328038">
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
                Did you find a working solution?
                    – <a href="/users/201482/kees-c-bakker" title="16,022 reputation" target="_blank">Kees C. Bakker</a>
                <a href="#comment32328038_12948809" target="_blank">Jan 29 '14 at 10:18</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-33331557">
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
                Sorry I can´t remember. Too long ago. It was during a lab.
                    – <a href="/users/1755381/franz-deschler" title="831 reputation" target="_blank">Franz Deschler</a>
                <a href="#comment33331557_12948809" target="_blank">Feb 24 '14 at 16:35</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>        </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-12951233">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        46
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><a href="https://developers.facebook.com/docs/howtos/login/login-as-app/" target="_blank">https://developers.facebook.com/docs/howtos/login/login-as-app/</a>:</p>

<blockquote>
  <p><em>“Because it requires you to include your App Secret you should not attempt to make this call client-side as that would expose this secret to all your app users. <strong>It is important that your App Secret is never shared with anyone.</strong> For this reason, this call should be performed server-side”</em></p>
</blockquote>

<p>And for the app access token, it’s the same – you should never <em>use</em> it client-side, because every user could spot it there and then start using it to perform actions on behalf of your app (or change many of your app’s settings).</p>

<p>If you have a server-side part to your application, you can simply “build” the app access token there yourself, concatenating app id and secret with a pipe symbol, <code>app_id|app_secret</code>.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 18 '12 at 9:21
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    <div id="comments-12951233">
                <ul>



    <li id="comment-17556393">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
    <li id="comment-20394326">
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
                thanks a lot for the info how the access token is being created!
                    – <a href="/users/1331671/ron" title="7,922 reputation" target="_blank">Ron</a>
                <a href="#comment20394326_12951233" target="_blank">Jan 30 '13 at 14:43</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-23570164">
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
                Can people still see it client side even if you hide your .js files?
                    – <a href="/users/996035/ben-pearce" title="2,271 reputation" target="_blank">Ben Pearce</a>
                <a href="#comment23570164_12951233" target="_blank">May 8 '13 at 7:17</a>
                        
                                                                            </div>
        </div>
    </li>
    <li id="comment-23571090">
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
                Of course they can, there is no "hiding" of client-side scripts.
                    – <a href="/users/1427878/cbroe" title="66,932 reputation" target="_blank">CBroe</a>
                <a href="#comment23571090_12951233" target="_blank">May 8 '13 at 7:51</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-24862836">
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
                @CBroe Thanks for the sharing the <code>app_id|app_secret</code> concatenate method of having a <b>permanent access token</b>. I was looking for hours for an answer to this.
                    – <a href="/users/456406/marco-alves" title="1,107 reputation" target="_blank">marco alves</a>
                <a href="#comment24862836_12951233" target="_blank">Jun 18 '13 at 14:50</a>
                        
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-16412556">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        65
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>Obtaining an App Access Token</strong></p>

<p>To obtain an App Access Token, invoke the following HTTP GET request:</p>

<pre><code>GET https://graph.facebook.com/oauth/access_token?
            client_id=YOUR_APP_ID
           &client_secret=YOUR_APP_SECRET
           &grant_type=client_credentials
</code></pre>

<p>The API will respond with a query-string formatted string of the form:</p>

<pre><code>access_token=YOUR_APP_ID|YOUR_APP_ACCESS_TOKEN
</code></pre>

<p>Reference: <a href="http://developers.facebook.com/docs/opengraph/howtos/publishing-with-app-token/" target="_blank">http://developers.facebook.com/docs/opengraph/howtos/publishing-with-app-token/</a></p>
    </div>
    
</div>
    
    <div>
	    <div id="comments-16412556">
                <ul>



    <li id="comment-41546972">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
    <li id="comment-41718628">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
    <li id="comment-48406374">
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
                Thank you, I was looking for this +!
                    – <a href="/users/3178944/simon" title="9,412 reputation" target="_blank">Simon</a>
                <a href="#comment48406374_16412556" target="_blank">May 10 '15 at 8:33</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-60476055">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
    <li id="comment-73200223">
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
                As of 4/27/17 the api response format has changed and it's returning <code>{"access_token":"YOUR_APP_ID|YOUR_APP_ACCESS_TOKEN","token_type":"bearer"}</code>
                    – <a href="/users/2054629/guig" title="3,574 reputation" target="_blank">Guig</a>
                <a href="#comment73200223_16412556" target="_blank">Mar 27 '17 at 23:11</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				    
	    </div>

                 
    </div>    </div>
</div>

  

<div id="answer-43038878">
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
<p>check if users of the node.js or the JAVASCRIPT.
    getLongLiveToken: function(data){</p>

<pre><code>        FB.api('oauth/access_token', {
            client_id: data.client_id, // FB_APP_ID
            client_secret: data.secret, // FB_APP_SECRET
            grant_type: 'fb_exchange_token',
            fb_exchange_token: data.access_token // USER_TOKEN
        }, function (res) {
            if(!res || res.error) {
                console.log(!res ? 'error occurred' : res.error);
            }else{
                var accessToken = res.access_token;
                if(typeof accessToken != 'undefined'){
                }
            }
        });
    }
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 27 '17 at 5:59
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-44606715">
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
<p>I'm not sure that exposing the APP client secret in the code is a good idea, you can take the APP token from Facebook tool "Access Token Tool" just copy the token to your code for any use   <a href="https://developers.facebook.com/tools-and-support/" target="_blank">https://developers.facebook.com/tools-and-support/</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jun 17 '17 at 16:15
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-46995038">
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
<p>You can also use this POST endpoint without generating the token, just be sure its being called from the server not client-side where the app_secret is exposed to public:</p>

<pre><code>https://graph.facebook.com/?id={url}&scrape=true&access_token={app_id}|{app_secret}
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 28 '17 at 22:17
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/facebook" title="show questions tagged 'facebook'" target="_blank">facebook</a> <a href="/questions/tagged/access-token" title="show questions tagged 'access-token'" target="_blank">access-token</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
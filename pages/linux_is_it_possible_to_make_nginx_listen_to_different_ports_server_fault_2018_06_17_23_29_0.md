<a href="https://serverfault.com/questions/655067/is-it-possible-to-make-nginx-listen-to-different-ports">https://serverfault.com/questions/655067/is-it-possible-to-make-nginx-listen-to-different-ports</a><div id="articleHeader"><h1><a href="/questions/655067/is-it-possible-to-make-nginx-listen-to-different-ports" target="_blank">Is it possible to make Nginx listen to different ports?</a></h1></div>
            

            

<div id="question">

    
        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        47
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>6</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I created one Nginx with one Linux Azure VM, is it possible to make nginx listen to different ports so that when I change the port number, the content would be different. I found there would be a collision if I created two or more ports related to HTTP on VM. Can anyone help me with that?</p>
    </div>
    
    
</div>

                
    <div>
	    

        <div id="comments-link-655067">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </div>        </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-655072">
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
<p>Yes, it is.</p>

<p>What you probably want is multiple "server" stanzas, each with a different port, but possibly (probably?) the same server_name, serving the "different" content appropriately within each one, maybe with a different document root in each server.</p>

<p>Full documentation is here:
<a href="http://nginx.org/en/docs/http/server_names.html" target="_blank">http://nginx.org/en/docs/http/server_names.html</a></p>

<p>Example:</p>

<pre><code>server {
    listen       80;
    server_name  example.org  www.example.org;
    root         /var/www/port80/
}

server {
    listen       81;
    server_name  example.org  www.example.org;
    root         /var/www/port81/
}
</code></pre>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-655072">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-755791">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        113
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>You can also do the following:</p>

<pre><code>server {
    listen 80;
    listen 8000;
    server_name example.org;
    root /var/www/;
}
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Feb 12 '16 at 11:53
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-755791">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


        






                            <div>
                                
                                            <div>
        
                <div>
                    <div>
                        <h3>Sign up or <a href="/users/login?ssrc=question_page&returnurl=https%3a%2f%2fserverfault.com%2fquestions%2f655067%2fis-it-possible-to-make-nginx-listen-to-different-ports%23new-answer" id="login-link" target="_blank">log in</a></h3>
                        
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
                                            

By clicking "Post Your Answer", you acknowledge that you have read our updated <a href="https://stackoverflow.com/legal/terms-of-service/public" name="tos" target="_blank">terms of service</a>, <a href="https://stackoverflow.com/legal/privacy-policy" name="privacy" target="_blank">privacy policy</a> and <a href="https://stackoverflow.com/legal/cookie-policy" name="cookie" target="_blank">cookie policy</a>, and that your continued use of the website is subject to these policies.


                                        </p>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/linux" title="show questions tagged 'linux'" target="_blank">linux</a> <a href="/questions/tagged/nginx" title="show questions tagged 'nginx'" target="_blank">nginx</a> <a href="/questions/tagged/virtual-machines" title="show questions tagged 'virtual-machines'" target="_blank">virtual-machines</a> <a href="/questions/tagged/azure" title="show questions tagged 'azure'" target="_blank">azure</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
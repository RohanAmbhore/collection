<a href="https://unix.stackexchange.com/questions/38755/how-to-download-a-file-through-an-ssh-server">https://unix.stackexchange.com/questions/38755/how-to-download-a-file-through-an-ssh-server</a><div id="articleHeader"><h1><a href="/questions/38755/how-to-download-a-file-through-an-ssh-server" target="_blank">How to download a file through an SSH server?</a></h1></div>
            

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        27
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" target="_blank">favorite</a>
        <div><b>17</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I have a server in USA (Linux box B), and my home PC (Linux box A),
and I need download a file from website C,</p>

<p>The issue is, it is very slow to download a file direct from A,
so I need download the file when I log in B, and <code>sftp</code> get the file from A.</p>

<p>Is there any way that I can download file and use B as proxy directly through only one line command?</p>
    </div>
    
    
</div>

                
    <div>
	    

        <div id="comments-link-38755">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </div>        </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-38761">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        40
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>(Strange situation, doesn't something like the <a href="http://en.wikipedia.org/wiki/Triangle_inequality" target="_blank">triangle inequality</a> hold for internet routing?)</p>

<p>Anyway, try the following, on <strong>A</strong>, <code>ssh</code> into <strong>B</strong> with a <code>-D</code> argument,</p>

<pre><code>ssh -D 1080 address-of-B
</code></pre>

<p>which acts as a SOCKS5 proxy on <code>127.0.0.1:1080</code>, which can be used by anything supporting SOCKS5 proxied connections.  <a href="https://superuser.com/a/262972/102592" target="_blank">Apparently, <code>wget</code> can do this</a>, by using the environment variable</p>

<pre><code>export SOCKS_SERVER=127.0.0.1:1080
wget http://server-C/whatever
</code></pre>

<p>Note that sometimes <code>curl</code> is more handy (i.e. I'm not sure if <code>wget</code> can do hostname lookups via SOCKS5; but this is not one of your concerns I suppose); also Firefox is able to work completely through such a SOCKS5 proxy.</p>

<p><strong>Edit</strong> I've just now noticed that you're looking for a <strong>one-line</strong> solution.  Well, how about </p>

<pre><code>ssh address-of-B 'wget -O - http://server-C/whatever' &gt;&gt; whatever
</code></pre>

<p>i.e. redirection the <code>wget</code>-fetched output to <code>stdout</code>, and redirecting the local output (from <code>ssh</code> running <code>wget</code> remotely) to a file.</p>

<p>This seems to work, the <code>wget</code> output is just a little confusing ("<em>saved to -</em>"), you can get rid of it by adding <code>-q</code> to the <code>wget</code> call.</p>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-38761">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-38776">
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
<p>Another approach could be that you normally log in into <code>B</code>, where you start a <code>screen</code> session. There you do the <code>wget</code> of your files - all into one directory.</p>

<p>And there the program can happily run; you just detach from screen, but let it run in the background.</p>

<p>If the downloads are finished (maybe even earlier), you can fech the data from <code>B</code> to <code>A</code> using <code>rsync</code> (my preference).</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 16 '12 at 9:47
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-38776">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-210580">
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
<p>Inspired by <a href="https://superuser.com/a/504119" target="_blank">another answer to another question</a>, I suggest using <a href="https://github.com/rofl0r/proxychains-ng" target="_blank">proxychains-ng</a> (which is the newer version of <a href="http://proxychains.sourceforge.net/" target="_blank">proxychains</a>).</p>

<ol>
<li>Download, compile, and optionally install <a href="https://github.com/rofl0r/proxychains-ng" target="_blank">proxychains-ng</a>.</li>
<li>Create a <code>proxychains.conf</code> file in the current directory, or at <code>~/.proxychains/proxychains.conf</code>, or at <code>/etc/proxychains.conf</code>.
<ul>
<li>Alternatively, create one file anywhere else, or with another name, and specify if through <code>-f</code> command-line argument, or through <code>PROXYCHAINS_CONF_FILE</code> environment variable.</li>
<li>There is a <a href="https://github.com/rofl0r/proxychains-ng/blob/master/src/proxychains.conf" target="_blank">sample config file</a> available. The most relevant options are at the very end.</li>
</ul></li>
<li><p>In your <code>proxychains.conf</code> file, add:</p>

<pre><code>[ProxyList]
socks5 127.0.0.1 1234
</code></pre></li>
<li><p>Run <code>ssh -D 1234 your_host_b</code>. This will make ssh listen on port 1234 on localhost, and use your remote host as a SOCKS proxy.</p>

<ul>
<li>Alternatively, run <code>ssh -ND 1234 your_host_b</code> instead. <code>-N</code> will prevent ssh from running any command on the remote server (i.e. it won't open a shell).</li>
</ul></li>
<li>Run: <code>proxychains4 yourcommandhere yourparametershere</code>. See some examples:
<ul>
<li><code>proxychains4 wget -O - http://ifconfig.co/</code></li>
<li><code>proxychains4 -q links http://ifconfig.co/</code></li>
</ul></li>
</ol>
    </div>
    
</div>
    
    <div>
	    

        <div id="comments-link-210580">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-38762">
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
<p>You can do a ssh tunnel from box A to box B and add to the routing table in box A, that website C is reachable via tunnel to box B. You have to allow packet forwarding on the box B.</p>

<p><a href="http://bodhizazen.net/Tutorials/VPN-Over-SSH" target="_blank">Here</a> you can see a very good step-by-step tutorial...</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 16 '12 at 7:34
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-38762">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-38763">
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
<p>You would need to create a tunnel on machine B tha would redirect the call to website C. But I'm puzzled as why this would be faster, unless your ISP as some restrictions.</p>

<p>I don't know a oneliner, but this isn't much more complicated.</p>

<p>On machine A, you do (I took 11111 randomly, you can take whatever you want as long as it is &gt; 1024, or you would need to be root)</p>

<pre><code>ssh -f -C -N -L 11111:C:80 username@B
</code></pre>

<p>The username on B is the one you use to connect to B. This should create a tunnel on port 11111 on machine B that redirect to port 80 (web site in HTTP use 443 for HTTPS) on machine C (I hope I did not mess the order ;) )</p>

<p>Then you can download the file directly from machine A via machine B. I'm assuming the file is at <code>http://C/path/to/file</code> so you would then use:</p>

<pre><code>wget http://B:11111/path/to/file
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 16 '12 at 7:35
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-38763">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-38764">
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
<p>You can do this via port forwarding (ssh tunneling).  Here's a resource:
<a href="http://www.jfranken.de/homepages/johannes/vortraege/ssh2_inhalt.en.html#ToC9" target="_blank">http://www.jfranken.de/homepages/johannes/vortraege/ssh2_inhalt.en.html#ToC9</a></p>

<p>Essentially, you should set up port forwarding on B.  When A issues wget to B, B will forward the packets to C and send the results back to A.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered May 16 '12 at 7:37
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-38764">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>

  

<div id="answer-227677">
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
<h1>Option 0:</h1>

<p>In order to use <a href="http://ports.su/net/wget" target="_blank"><code>wget</code></a> with a SOCKS5 proxy from <a href="http://mdoc.su/o/ssh" target="_blank"><code>ssh</code></a>, you have to install the <a href="http://ports.su/security/dante" target="_blank"><code>security/dante</code></a> package in order to use the <code>SOCKS_SERVER</code> option with the <code>socksify</code> utility.</p>

<pre><code>sudo pkg_add dante
</code></pre>

<p>Subsequently, you open an SSH connection in the background:</p>

<pre><code>ssh -N -C -D1080 user@hostB &
</code></pre>

<p>And use wget through a SOCKS5 proxy through socksify:</p>

<pre><code>env SOCKS_SERVER=127.0.0.1:1080 socksify wget http://website-C
</code></pre>

<hr />

<h1>Option 1:</h1>

<p>Just pipe the file to <code>stdout</code> on the server, and read it from <code>stdin</code> on your workstation.</p>

<pre><code>ssh -C user@hostB "wget -O- http://website-C" &gt;&gt; file-from-website-C
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Sep 5 '15 at 8:00
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
    <div>
	    

        <div id="comments-link-227677">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </div>    </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


        






                            <div>
                                
                                            <div>
        
                <div>
                    <div>
                        <h3>Sign up or <a href="/users/login?ssrc=question_page&returnurl=https%3a%2f%2funix.stackexchange.com%2fquestions%2f38755%2fhow-to-download-a-file-through-an-ssh-server%23new-answer" id="login-link" target="_blank">log in</a></h3>
                        
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/ssh" title="show questions tagged 'ssh'" target="_blank">ssh</a> <a href="/questions/tagged/wget" title="show questions tagged 'wget'" target="_blank">wget</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
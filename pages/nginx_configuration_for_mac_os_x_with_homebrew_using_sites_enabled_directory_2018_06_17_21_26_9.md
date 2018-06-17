<a href="https://gist.github.com/jimothyGator/5436538">https://gist.github.com/jimothyGator/5436538</a><div id="articleHeader"><h1>Nginx configuration for Mac OS X with Homebrew, using sites-enabled directory.</h1></div>
    <div>
  <div>
    Nginx configuration for Mac OS X with Homebrew, using sites-enabled directory.
  </div>
</div>


        <div>
  <div id="file-readme-md">
      
    
  <div id="readme">
    <article><pre><code>mkdir -p /usr/local/etc/nginx/sites-{enabled,available}
cd /usr/local/etc/nginx/sites-enabled
ln -s ../sites-available/default.conf
ln -s ../sites-available/default-ssl.conf
</code></pre>
<p>File locations:</p>
<ul>
<li><code>nginx.conf</code> to <code>/usr/local/etc/nginx/</code></li>
<li><code>default.conf</code> and <code>default-ssl.conf</code> to <code>/usr/local/etc/nginx/sites-available</code></li>
<li><code>homebrew.mxcl.nginx.plist</code> to <code>/Library/LaunchDaemons/</code></li>
</ul>
<p>Not documented yet:</p>
<ul>
<li>How to create self-signed SSL certificates</li>
<li>How to start and stop Nginx</li>
</ul>
</article>
  </div>

  </div>
</div>

        <div>
  <div id="file-default-ssl-conf">
      
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-default-ssl-conf-L1"></td>
        <td id="file-default-ssl-conf-LC1">server {</td>
      </tr>
      <tr>
        <td id="file-default-ssl-conf-L2"></td>
        <td id="file-default-ssl-conf-LC2">    listen       443;</td>
      </tr>
      <tr>
        <td id="file-default-ssl-conf-L3"></td>
        <td id="file-default-ssl-conf-LC3">    server_name  localhost;</td>
      </tr>
      
      <tr>
        <td id="file-default-ssl-conf-L5"></td>
        <td id="file-default-ssl-conf-LC5">    ssl                  on;</td>
      </tr>
      <tr>
        <td id="file-default-ssl-conf-L6"></td>
        <td id="file-default-ssl-conf-LC6">    ssl_certificate      server.crt;</td>
      </tr>
      <tr>
        <td id="file-default-ssl-conf-L7"></td>
        <td id="file-default-ssl-conf-LC7">    ssl_certificate_key  server.key;</td>
      </tr>
      
      <tr>
        <td id="file-default-ssl-conf-L9"></td>
        <td id="file-default-ssl-conf-LC9">    ssl_session_timeout  5m;</td>
      </tr>
      
      <tr>
        <td id="file-default-ssl-conf-L11"></td>
        <td id="file-default-ssl-conf-LC11">    ssl_protocols  SSLv2 SSLv3 TLSv1;</td>
      </tr>
      <tr>
        <td id="file-default-ssl-conf-L12"></td>
        <td id="file-default-ssl-conf-LC12">    ssl_ciphers  HIGH:!aNULL:!MD5;</td>
      </tr>
      <tr>
        <td id="file-default-ssl-conf-L13"></td>
        <td id="file-default-ssl-conf-LC13">    ssl_prefer_server_ciphers   on;</td>
      </tr>
      
      <tr>
        <td id="file-default-ssl-conf-L15"></td>
        <td id="file-default-ssl-conf-LC15">    location / {</td>
      </tr>
      <tr>
        <td id="file-default-ssl-conf-L16"></td>
        <td id="file-default-ssl-conf-LC16">        root   html;</td>
      </tr>
      <tr>
        <td id="file-default-ssl-conf-L17"></td>
        <td id="file-default-ssl-conf-LC17">        index  index.html index.htm;</td>
      </tr>
      
      
</tbody></table>


  </div>

  </div>
</div>

        <div>
  <div id="file-default-conf">
      
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-default-conf-L1"></td>
        <td id="file-default-conf-LC1">server {</td>
      </tr>
      <tr>
        <td id="file-default-conf-L2"></td>
        <td id="file-default-conf-LC2">    listen       80;</td>
      </tr>
      <tr>
        <td id="file-default-conf-L3"></td>
        <td id="file-default-conf-LC3">    server_name  localhost;</td>
      </tr>
      
      <tr>
        <td id="file-default-conf-L5"></td>
        <td id="file-default-conf-LC5">    #access_log  logs/host.access.log  main;</td>
      </tr>
      
      <tr>
        <td id="file-default-conf-L7"></td>
        <td id="file-default-conf-LC7">    location / {</td>
      </tr>
      <tr>
        <td id="file-default-conf-L8"></td>
        <td id="file-default-conf-LC8">        root   html;</td>
      </tr>
      <tr>
        <td id="file-default-conf-L9"></td>
        <td id="file-default-conf-LC9">        index  index.html index.htm;</td>
      </tr>
      
      
      <tr>
        <td id="file-default-conf-L12"></td>
        <td id="file-default-conf-LC12">    #error_page  404              /404.html;</td>
      </tr>
      
      <tr>
        <td id="file-default-conf-L14"></td>
        <td id="file-default-conf-LC14">    # redirect server error pages to the static page /50x.html</td>
      </tr>
      
      <tr>
        <td id="file-default-conf-L16"></td>
        <td id="file-default-conf-LC16">    error_page   500 502 503 504  /50x.html;</td>
      </tr>
      <tr>
        <td id="file-default-conf-L17"></td>
        <td id="file-default-conf-LC17">    location = /50x.html {</td>
      </tr>
      <tr>
        <td id="file-default-conf-L18"></td>
        <td id="file-default-conf-LC18">        root   html;</td>
      </tr>
      
      
</tbody></table>


  </div>

  </div>
</div>

        <div>
  <div id="file-homebrew-mxcl-nginx-plist">
      
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-homebrew-mxcl-nginx-plist-L1"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC1">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L2"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC2">&lt;!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd"&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L3"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC3">&lt;plist version="1.0"&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L4"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC4">  &lt;dict&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L5"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC5">    &lt;key&gt;Label&lt;/key&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L6"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC6">    &lt;string&gt;homebrew.mxcl.nginx&lt;/string&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L7"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC7">    &lt;key&gt;RunAtLoad&lt;/key&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L8"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC8">    &lt;true/&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L9"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC9">    &lt;key&gt;KeepAlive&lt;/key&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L10"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC10">    &lt;false/&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L11"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC11">    &lt;key&gt;ProgramArguments&lt;/key&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L12"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC12">    &lt;array&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L13"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC13">        &lt;string&gt;/usr/local/opt/nginx/sbin/nginx&lt;/string&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L14"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC14">        &lt;string&gt;-g&lt;/string&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L15"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC15">        &lt;string&gt;daemon off;&lt;/string&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L16"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC16">    &lt;/array&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L17"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC17">    &lt;key&gt;WorkingDirectory&lt;/key&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L18"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC18">    &lt;string&gt;/usr/local&lt;/string&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L19"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC19">  &lt;/dict&gt;</td>
      </tr>
      <tr>
        <td id="file-homebrew-mxcl-nginx-plist-L20"></td>
        <td id="file-homebrew-mxcl-nginx-plist-LC20">&lt;/plist&gt;</td>
      </tr>
</tbody></table>


  </div>

  </div>
</div>

        <div>
  <div id="file-nginx-conf">
      
    

  <div>
      <table>
      <tbody><tr>
        <td id="file-nginx-conf-L1"></td>
        <td id="file-nginx-conf-LC1">#user  nobody;</td>
      </tr>
      <tr>
        <td id="file-nginx-conf-L2"></td>
        <td id="file-nginx-conf-LC2">worker_processes  1;</td>
      </tr>
      
      <tr>
        <td id="file-nginx-conf-L4"></td>
        <td id="file-nginx-conf-LC4">error_log  /Library/Logs/nginx/error.log;</td>
      </tr>
      
      <tr>
        <td id="file-nginx-conf-L6"></td>
        <td id="file-nginx-conf-LC6">events {</td>
      </tr>
      <tr>
        <td id="file-nginx-conf-L7"></td>
        <td id="file-nginx-conf-LC7">    worker_connections  1024;</td>
      </tr>
      
      
      <tr>
        <td id="file-nginx-conf-L10"></td>
        <td id="file-nginx-conf-LC10">http {</td>
      </tr>
      <tr>
        <td id="file-nginx-conf-L11"></td>
        <td id="file-nginx-conf-LC11">    include       mime.types;</td>
      </tr>
      <tr>
        <td id="file-nginx-conf-L12"></td>
        <td id="file-nginx-conf-LC12">    default_type  application/octet-stream;</td>
      </tr>
      
      <tr>
        <td id="file-nginx-conf-L14"></td>
        <td id="file-nginx-conf-LC14">    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '</td>
      </tr>
      <tr>
        <td id="file-nginx-conf-L15"></td>
        <td id="file-nginx-conf-LC15">                      '$status $body_bytes_sent "$http_referer" '</td>
      </tr>
      <tr>
        <td id="file-nginx-conf-L16"></td>
        <td id="file-nginx-conf-LC16">                      '"$http_user_agent" "$http_x_forwarded_for"';</td>
      </tr>
      
      <tr>
        <td id="file-nginx-conf-L18"></td>
        <td id="file-nginx-conf-LC18">    access_log  /Library/Logs/nginx/access.log  main;</td>
      </tr>
      
      <tr>
        <td id="file-nginx-conf-L20"></td>
        <td id="file-nginx-conf-LC20">    sendfile        on;</td>
      </tr>
      
      <tr>
        <td id="file-nginx-conf-L22"></td>
        <td id="file-nginx-conf-LC22">    keepalive_timeout  65;</td>
      </tr>
      
      <tr>
        <td id="file-nginx-conf-L24"></td>
        <td id="file-nginx-conf-LC24">    index index.html index.php;</td>
      </tr>
      
      <tr>
        <td id="file-nginx-conf-L26"></td>
        <td id="file-nginx-conf-LC26">    upstream www-upstream-pool{</td>
      </tr>
      <tr>
        <td id="file-nginx-conf-L27"></td>
        <td id="file-nginx-conf-LC27">        server unix:/tmp/php-fpm.sock;</td>
      </tr>
      
      
      <tr>
        <td id="file-nginx-conf-L30"></td>
        <td id="file-nginx-conf-LC30">    include /etc/nginx/conf.d/*.conf;</td>
      </tr>
      <tr>
        <td id="file-nginx-conf-L31"></td>
        <td id="file-nginx-conf-LC31">    include /usr/local/etc/nginx/sites-enabled/*.conf; </td>
      </tr>
      
</tbody></table>


  </div>

  </div>
</div>


    
    <div>
      <div>
        
  <div>
      




    
<div>
    
  <div id="gistcomment-1581868">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Good idea putting the logs in /Library/Logs. I had to create the directory /Library/Logs/nginx first—nginx couldn't handle that itself.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


    </div>

  </div>
</div>

  </div>
  <div>
      




    
<div>
    
  <div id="gistcomment-1586617">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/spamguy" target="_blank">@spamguy</a> What good in logs at /Library/Logs? Only unix way, only hardcore!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


    </div>

  </div>
</div>

  </div>
  <div>
      




    
<div>
    
  <div id="gistcomment-1594784">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I can't seem to get nginx to load anything on port :8080<br />
<code>brew install nginx --with-passenger</code></p>
<p>followed brew's instructions but couldn't get localhost to work.<br />
I have it running on my iMac but not on my MBP, is there some difference in configuration?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


    </div>

  </div>
</div>

  </div>
  
  
  <div>
      




    
<div>
    
  <div id="gistcomment-1795707">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>You saved my day!!!</p>
<p>Forgot to <code>include /usr/local/etc/nginx/sites-enabled/*.conf;</code></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


    </div>

  </div>
</div>

  </div>
  <div>
      




    
<div>
    
  <div id="gistcomment-1849282">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>include /etc/nginx/conf.d ??? i must make it, cause i didn't find it</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


    </div>

  </div>
</div>

  </div>
  <div>
      




    
<div>
    
  <div id="gistcomment-1878233">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>You are right!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


    </div>

  </div>
</div>

  </div>
  
  <div>
      




    
<div>
    
  <div id="gistcomment-1957184">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>thanks dude!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


    </div>

  </div>
</div>

  </div>
  <div>
      




    
<div>
    
  <div id="gistcomment-1975614">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Thanks a lot dude!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


    </div>

  </div>
</div>

  </div>
  <div>
      




    
<div>
    
  <div id="gistcomment-1977858">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><code>/usr/local/opt/nginx/sbin/nginx</code> was <code>/usr/local/opt/nginx/bin/nginx</code> for me.  Thanks!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


    </div>

  </div>
</div>

  </div>
  
  <div>
      




    
<div>
    
  <div id="gistcomment-2185712">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>people always fail to inform others to edit <code>/private/etc/hosts</code> and add entries for the servers.</p>
<p>for example:</p>
<pre><code> 127.0.0.1 localhost.sec1
 127.0.0.1 mywebsite.local.com
</code></pre>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


    </div>

  </div>
</div>

  </div>
  
  <div>
      




    
<div>
    
  <div id="gistcomment-2391706">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>where can i find the /private/etc/hosts?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


    </div>

  </div>
</div>

  </div>





        <div>
            <div>
  

  
    <div>
      <div>
  


  
  <div>

    

    

        <p>
    
    
        Attach files by dragging & dropping,
        selecting them, or pasting
        from the clipboard.
    
    
    
    
    
    
    
    
    
  </p>


    
  </div>

  

  


  
</div>


      
    </div>
</div>

        </div>
      </div>
    </div>

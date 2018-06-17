<a href="https://www.digitalocean.com/community/questions/how-to-run-multiple-node-application-with-nginx-same-droplet-same-domain">https://www.digitalocean.com/community/questions/how-to-run-multiple-node-application-with-nginx-same-droplet-same-domain</a><div id="articleHeader"><h1>How to run multiple node application with NGINX: same droplet same domain</h1></div>

    <div>

      
        July 21, 2014
      

      23.1k views

      </div>
        
          
          
        

    

    


    <div>
      
      <p>I followed the tutorial here with node and NGINX.<br />
They work great.<br />
But, they all are running the node application from the root of the domain.</p>

<p>I have a number of small node apps and I want to be able to run them like:</p>

<p><a href="http://mydomain/app1" target="_blank">http://mydomain/app1</a><br />
<a href="http://mydomain/app2" target="_blank">http://mydomain/app2</a></p>

<p>where app1 may be localhost:9000 and app2 is localhost:9001 etc.</p>

<p>when I change my hosts-enabled file from<br />
location / to location /app1/</p>
<pre><code>server {
    listen 0.0.0.0:80;
    server_name 192.241.223.202;
    access_log /var/log/nginx/ddApp.log;

    location /app1/ {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header HOST $http_host;
        proxy_set_header X-NginX-Proxy true;

        proxy_pass http://127.0.0.1:9000;
        proxy_redirect off;
    }
}
</code></pre>
<p>my application is launched (node sends down the html document) but the browser can't follow any of the links (load any resources ..404's).</p>

<p>This direct link can get the resouces:</p>

<p><a href="http://192.241.223.202:9000/app/b7672478.app.js" target="_blank">http://192.241.223.202:9000/app/b7672478.app.js</a></p>

<p>but through the app1 path </p>

<p><a href="http://192.241.223.202/app1/app/b7672478.app.js" target="_blank">http://192.241.223.202/app1/app/b7672478.app.js</a></p>

<p>NGINX just serves up the root html document.</p>

<p>Actually all requests to the app1 path produce the same response.</p>

<p>The NGINX docs just make my head hurt (as well as my pride).</p>

<p>Any help and direction would be great.</p>



    </div>

    <div>
      <div id="question_4835">

  

  <div>
  

    <div>
        <a href="/community/auth/digitalocean" target="_blank">Log In to Comment</a>
    </div>

  
      

    

      

    





    

  


<div>
  <div>
    <div>
      <div>6 Answers</div>
    
    <div>
        <div id="answer_15098">
  <div>
    

    <div>
      

      <div>
        


  <div>
    <div><p>Oh happy days!<br />
We are up with app1! ... other than a couple of bootstrap fronts out of the bower component failing to pick up the app1 base  ....   I'll deal with it later.<br />
Also the &lt;base&gt; tag needs a trailing slash so for this baby it was:</p>
<pre><code>&lt;base href="/app1/"&gt;
</code></pre>
<p>THANK YOU SO MUCH!!!</p>
</div>
    
  



<div>
  <a href="#form_answer_15098" target="_blank">
    Reply
  </a>


  

  
</div>

      

      <div>
        <div id="response_answer_15098">

    

  <div>
    <ul>
      

      <li id="comment_15346">
    <div>
      
      <div>
        

          <div>
            <div><p>Awesome! Glad to hear it's working now! :)</p>
</div>
            
          

        

        


        

      
      
    
    

  </li>



    </ul>
  


  

      
    
  

  

        <div id="answer_15079">
  <div>
    

    <div>
      

      <div>
        


  <div>
    <div><p>Try adding </p>
<pre><code>rewrite ^/app1/(.*)$ /$1 break;
</code></pre>
<p>under</p>
<pre><code>location /app1/ {
</code></pre>
<p>and restarting nginx. Does that work?</p>
</div>
    
  



<div>
  <a href="#form_answer_15079" target="_blank">
    Reply
  </a>


  

  
</div>

      

      
    
  

  

        <div id="answer_15081">
  <div>
    

    <div>
      

      <div>
        


  <div>
    <div><pre><code>server {
    listen 0.0.0.0:80;
    server_name 192.241.223.202;
    access_log /var/log/nginx/ddApp.log;

    location /app1/ {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header HOST $http_host;
        proxy_set_header X-NginX-Proxy true;

        proxy_pass http://127.0.0.1:9000;
        proxy_redirect off;
        rewrite ^/app1/(.*)$ /$1 break;
    }
}
</code></pre>
<p>nginx -s reload</p>

<p><a href="http://192.241.223.202/app1/" target="_blank">http://192.241.223.202/app1/</a>  in a new browser window is still broken.</p>
</div>
    
  



<div>
  <a href="#form_answer_15081" target="_blank">
    Reply
  </a>


  

  
</div>

      

      <div>
        <div id="response_answer_15081">

    

  <div>
    <ul>
      

      <li id="comment_15315">
    <div>
      
      <div>
        

          <div>
            <div><p>Does your application log requests/visits? Can you check what path nginx passed to it?</p>
</div>
            
          

        

        


        

      
      
    
    

  </li>



    </ul>
  


  

      
    
  

  

        <div id="answer_15082">
  <div>
    

    <div>
      

      <div>
        


  <div>
    <div><p>root@test:/etc/nginx/sites-enabled# tail /var/log/nginx/ddApp.log<br />
82.166.118.134 - - [21/Jul/2014:15:31:07 -0400] "GET /socket.io/socket.io.js HTTP/1.1" 404 208 "<a href="http://192.241.223.202/app1/" target="_blank">http://192.241.223.202/app1/</a>" "Mozilla/5.0 (X11; Linux x86<em>64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"<br />
82.166.118.134 - - [21/Jul/2014:15:31:07 -0400] "GET /app/77f2a613.vendor.js HTTP/1.1" 404 208 "<a href="http://192.241.223.202/app1/" target="_blank">http://192.241.223.202/app1/</a>" "Mozilla/5.0 (X11; Linux x86</em>64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"<br />
82.166.118.134 - - [21/Jul/2014:15:31:07 -0400] "GET /app/b7672478.app.js HTTP/1.1" 404 208 "<a href="http://192.241.223.202/app1/" target="_blank">http://192.241.223.202/app1/</a>" "Mozilla/5.0 (X11; Linux x86<em>64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"<br />
82.166.118.134 - - [21/Jul/2014:15:31:14 -0400] "GET /app1/ HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Linux x86</em>64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"<br />
82.166.118.134 - - [21/Jul/2014:15:31:14 -0400] "GET /app/77f2a613.vendor.js HTTP/1.1" 404 208 "<a href="http://192.241.223.202/app1/" target="_blank">http://192.241.223.202/app1/</a>" "Mozilla/5.0 (X11; Linux x86<em>64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"<br />
82.166.118.134 - - [21/Jul/2014:15:31:14 -0400] "GET /socket.io/socket.io.js HTTP/1.1" 404 208 "<a href="http://192.241.223.202/app1/" target="_blank">http://192.241.223.202/app1/</a>" "Mozilla/5.0 (X11; Linux x86</em>64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"<br />
82.166.118.134 - - [21/Jul/2014:15:31:14 -0400] "GET /app/b7672478.app.js HTTP/1.1" 404 208 "<a href="http://192.241.223.202/app1/" target="_blank">http://192.241.223.202/app1/</a>" "Mozilla/5.0 (X11; Linux x86<em>64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"<br />
82.166.118.134 - - [21/Jul/2014:15:31:14 -0400] "GET /app/58c604fc.app.css HTTP/1.1" 404 208 "<a href="http://192.241.223.202/app1/" target="_blank">http://192.241.223.202/app1/</a>" "Mozilla/5.0 (X11; Linux x86</em>64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"<br />
82.166.118.134 - - [21/Jul/2014:15:31:14 -0400] "GET /app/088ba864.vendor.css HTTP/1.1" 404 208 "<a href="http://192.241.223.202/app1/" target="_blank">http://192.241.223.202/app1/</a>" "Mozilla/5.0 (X11; Linux x86<em>64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"<br />
82.166.118.134 - - [21/Jul/2014:15:31:30 -0400] "GET /app1/ HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Linux x86</em>64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"<br />
root@test:/etc/nginx/sites-enabled# </p>
</div>
    
  



<div>
  <a href="#form_answer_15082" target="_blank">
    Reply
  </a>


  

  
</div>

      

      <div>
        <div id="response_answer_15082">

    

  <div>
    <ul>
      

      <li id="comment_15316">
    <div>
      
      <div>
        

          <div>
            <div><p>I meant on the node.js end. If you're using express version 3, you can add this to enable request logging:</p>
<pre><code>app.use(express.logger('dev')); 
</code></pre>

<pre><code>app.use(require('morgan')('dev')); // make sure you install the "morgan" package.
</code></pre>
<p>if you're using express version 4.</p>
</div>
            
          

        

        


        

      
      
    
    

  </li>



    </ul>
  


  

      
    
  

  

        <div id="answer_15090">
  <div>
    

    <div>
      

      <div>
        


  <div>
    <div><p>sorry .... I've added morgan (I'm on Express 4)  I only seem to get a<br />
Get / 304 with <br />
<a href="http://192.241.223.202/app1/" target="_blank">http://192.241.223.202/app1/</a><br />
and then the broken app is displayed in the browser</p>

<p>Here is a session:</p>

<p>root@test:/var/log/upstart# service ddApp stop<br />
ddApp stop/waiting<br />
root@test:/var/log/upstart# service ddApp start<br />
ddApp start/running, process 7080<br />
root@test:/var/log/upstart# tail ddApp.log -f<br />
league list<br />
GET /api/leagueList 304 160ms<br />
GET /api/leagueList 304 161ms<br />
GET / 304 157ms<br />
GET / 304 159ms<br />
GET / 304 164ms<br />
   info  - socket.io started<br />
loading league.controller<br />
Express server listening on 9000, in production mode<br />
db connection open<br />
GET / 304 181ms<br />
GET / 304 164ms  &lt;-- one of these for each refress of the browser at <a href="http://192....../app1" target="_blank">http://192....../app1</a></p>
</div>
    
  



<div>
  <a href="#form_answer_15090" target="_blank">
    Reply
  </a>


  

  
</div>

      

      <div>
        <div id="response_answer_15090">

    

  <div>
    <ul>
      

      <li id="comment_15327">
    <div>
      
      <div>
        

          <div>
            <div><p>Ok, so the rewrite rule is actually working properly.</p>

<p><code>http://192.241.223.202/app1/app/77f2a613.vendor.js</code> works while <code>http://192.241.223.202/app/77f2a613.vendor.js</code> doesn't, so you need to update your layout view and replace</p>
<pre><code>&lt;base href="/"&gt;
</code></pre>

<pre><code>&lt;base href="/app1"&gt;
</code></pre></div>
            
          

        

        


        

      
      
    
    

  </li>



    </ul>
  


  

      
    
  

  

        <div id="answer_31255">
  <div>
    

    <div>
      

      <div>
        


  <div>
    <div><p>I spent hours and hours trying to solve this same problem. Knowing those hours are wasted because I needed a trailing slash is heartbreaking, but so glad I found this post. </p>
</div>
    
  



<div>
  <a href="#form_answer_31255" target="_blank">
    Reply
  </a>


  

  
</div>

      

      
    
  

  

    
    <div>Have another answer? Share your knowledge.</div>
    <div>  
  <div>
    
    
      <div><div><ul><li>Highlight</li><li>Table</li></ul></div>
      
        <div><a href="/community/auth/digitalocean" target="_blank">Log In to Answer</a></div>
  


  







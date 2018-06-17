<a href="https://serverfault.com/questions/591367/hosting-multiple-nodejs-applications-on-a-single-domain">https://serverfault.com/questions/591367/hosting-multiple-nodejs-applications-on-a-single-domain</a><div id="articleHeader"><h1>Hosting multiple Nodejs applications on a single domain</h1></div>

<p>I'm trying to run multiple nodejs applications (using the express framework) all served on the same external port (80) but each under a subdirectory.</p>

<p>E.g. I want...</p>

<p>NodeJsApplication1 to be available at <a href="http://www.mydomain.com/NodeJsApplication1" target="_blank">http://www.mydomain.com/NodeJsApplication1</a></p>

<p>NodeJsApplication2 to be available at <a href="http://www.mydomain.com/NodeJsApplication2" target="_blank">http://www.mydomain.com/NodeJsApplication2</a></p>



<p>I have tried using Nginx as a proxy with a conf similar to the following.</p>

<pre><code>server {
    listen       80;
    server_name  www.mydomain.com;

    location / {
        root   /var/www/html;
        index  index.html index.htm;
    }

    location /NodeJsApplication1/ {
        proxy_pass http://0.0.0.0:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        rewrite /NodeJsApplication1/(.*) /$1 break;
    }

    location /NodeJsApplication2/ {
        proxy_pass http://0.0.0.0:3001;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        rewrite /NodeJsApplication2/(.*) /$1 break;
    }
}
</code></pre>

<p>This works find for accessing the page but it breaks all relative URLs on the returning page. All scripts and css etc are pointing at the root (E.g. www.mydomain.com/styles/main.css).</p>

<p>I know I can use multiple subdomains but don't want to go down that route. I'd prefer to have subfolder proxy so it is all handled in software and I don't need to set up any DNS records for each application.</p>

<p>Is this even possible?</p>

<p>Update</p>

<p>Within the applications themselves all links are using relative paths. For example:</p>

<p>

But when rendered the browser treats them as "www.mydomain.com/styles/main.css" rather than "www.mydomain.com/NodeJsApplication1/styles/main.css".</p>

<p>the first being to modify the NodeJS applications to specify a full URL but this requires the application to know the subdirectory that nginx is configured with and it ruins portability to another environment.</p>
    
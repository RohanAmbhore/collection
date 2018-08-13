<a href="https://www.digitalocean.com/community/tutorials/how-to-redirect-www-to-non-www-with-nginx-on-centos-7">https://www.digitalocean.com/community/tutorials/how-to-redirect-www-to-non-www-with-nginx-on-centos-7</a><div id="articleHeader"><h1>       How To Redirect www to Non-www with Nginx on CentOS 7    </h1></div>

    PostedMay  4, 2015

    116k views

    
      <a href="/community/tags/nginx?type=tutorials" target="_blank">Nginx</a>
      <a href="/community/tags/centos?type=tutorials" target="_blank">CentOS</a>
    
  

  


    
      <h3 id="introduction">Introduction</h3>

<p>When you have your web site or application up and running behind a domain, it is often desirable to also allow your users access to it via the plain domain name <em>and</em> the <strong>www</strong> subdomain. That is, they should be able to visit your domain with or without the "<a href="http://www." target="_blank">www.</a>" prefix, e.g. <code>example.com</code> or <code>www.example.com</code>, in a web browser, and be presented with the same content. While there are a variety of ways to set this up, the best solution, for consistency and SEO considerations, is to choose which domain you prefer, plain or www, and redirect the other one to the preferred domain. This type of redirect is called a <strong>Permanent Redirect</strong>, or "301 redirect", and can be easily set up by properly configuring your DNS resource records and web server software.</p>

<p>This tutorial will show you how to redirect a www URL to non-www, e.g. <code>www.example.com</code> to <code>example.com</code>, with Nginx on CentOS 7. We will also show you how to redirect in the other direction, from a non-www URL to <a href="http://www" target="_blank">www</a>. The Ubuntu 14.04 version of this tutorial is available <a href="https://www.digitalocean.com/community/tutorials/how-to-redirect-www-to-non-www-with-nginx-on-ubuntu-14-04" target="_blank">here</a>.</p>

<p>If you want to perform this type of redirect with Apache as your web server, you should follow this tutorial instead: <a href="https://www.digitalocean.com/community/tutorials/how-to-redirect-www-to-non-www-with-apache-on-centos-7" target="_blank">How to Redirect www to non-www with Apache on CentOS 7</a>.</p>

<h2 id="prerequisites">Prerequisites</h2>

<p>This tutorial assumes that you have superuser privileges, i.e. <code>sudo</code> or root, on the server that is running Nginx. If you don't already have that set up, follow this tutorial: <a href="https://www.digitalocean.com/community/tutorials/initial-server-setup-with-centos-7" target="_blank">Initial Server Setup on CentOS 7</a>.</p>

<p>It is assumed that you have Nginx installed. If you do not already have this set up, there are several tutorials on the subject under the <a href="https://www.digitalocean.com/community/tags/nginx" target="_blank">Nginx tag</a>.</p>

<p>You must be able to add records to the DNS that is managing your domain. If you do not already have a domain, you may purchase one from a domain registrar, and manage it with the registrar's DNS or <a href="https://www.digitalocean.com/community/tutorials/how-to-point-to-digitalocean-nameservers-from-common-domain-registrars" target="_blank">DigitalOcean's DNS</a>. In this tutorial, we will use the <a href="https://www.digitalocean.com/community/tutorials/how-to-set-up-a-host-name-with-digitalocean" target="_blank">DigitalOcean DNS</a> to create the necessary records.</p>

<p>Let's get started by configuring your DNS records.</p>

<h2 id="configure-dns-records">Configure DNS Records</h2>

<p>In order to set up the desired redirect, <code>www.example.com</code> to <code>example.com</code> or vice versa, you must have an <strong>A record</strong> for each name.</p>

<p>Open whatever you use to manage your DNS. For our example, we'll use the <a href="https://cloud.digitalocean.com/domains" target="_blank">DigitalOcean DNS</a>.</p>

<p>If a domain (also known as a zone) record does not already exist, create one now. The <strong>hostname</strong> should be your domain, e.g. <code>example.com</code>, and the IP address should be set to the public IP address of your Nginx server. This will automatically create an A record that points your domain to the IP address that you specified. If you are using another system to manage your domain, you may need to add this manually.</p>

<p>Next, add another A record with "www" as the hostname (or "<a href="http://www.example.com" target="_blank">www.example.com</a>" if the partial subdomain doesn't work), and specify the same IP address.</p>

<p>When you have created both records, it should look something like this:</p>

<p><div class="readableLargeImageContainer"><img src="https://assets.digitalocean.com/articles/redirect/dns_a_records.png" alt="Required A records" /></div></p>

<p><strong>Note:</strong> This will also work with CNAME records, as long as the canonical name's A record refers to the IP address of your Nginx web server.</p>

<p>Now your server should be accessible via the www and non-www domain, but we still need to set up the redirect. We'll do that now.</p>

<h2 id="configure-nginx-redirect">Configure Nginx Redirect</h2>

<p>In order to perform the 301 redirect, you must add a new Nginx server block that points to your original server block.</p>

<p>Open your Nginx server block configuration in an editor. We'll add another configuration file in the Nginx include directory, <code>/etc/nginx/conf.d</code> called <code>redirect.conf</code>:</p>
<pre><code>sudo vi /etc/nginx/conf.d/redirect.conf
</code></pre>
<p>Your original server block should already be defined. Depending on which direction you want to redirect, use one of the following options.</p>

<h3 id="option-1-redirect-www-to-non-www">Option 1: Redirect www to non-www</h3>

<p>If you want redirect users from www to a plain, non-www domain, insert this configuration:</p>
<div>New Server Block — www to non-www</div><pre><code>server {
    server_name www.example.com;
    return 301 $scheme://example.com$request_uri;
}
</code></pre>
<p>Save and exit. This configures Nginx to redirect requests to "<a href="http://www.example.com" target="_blank">www.example.com</a>" to "example.com". Note that there should be another server block that defines your non-www web server.</p>

<p>To put the changes into effect, restart Nginx:</p>
<pre><code>sudo systemctl restart nginx
</code></pre>
<p>Note that if you are using HTTPS, the <code>listen</code> directive should be set to port <code>443</code> instead of <code>80</code>.</p>

<p>Use this curl command to ensure that the non-www domain redirects to the www domain (replace the highlighted part with your actual domain):</p>
<pre><code>curl -I http://www.example.com
</code></pre>
<p>You should get a <code>301 Moved Permanently</code> response, that shows the non-www redirect location, like this:</p>
<pre><code><div>Output:</div>HTTP/1.1 301 Moved Permanently
Server: nginx/1.4.6 (Ubuntu)
Date: Mon, 04 May 2015 18:20:19 GMT
Content-Type: text/html
Content-Length: 193
Connection: keep-alive
Location: http://example.com/
</code></pre>
<p>Of course, you should access your domain in a web browser (www and non-www) to be sure.</p>

<h3 id="option-2-redirect-non-www-to-www">Option 2: Redirect non-www to www</h3>

<p>If you want redirect users from a plain, non-www domain to a www domain, add this server block:</p>
<div>New Server Block — non-www to www</div><pre><code>server {
    server_name example.com;
    return 301 $scheme://www.example.com$request_uri;
}
</code></pre>
<p>Save and exit. This configures Nginx to redirect requests to "example.com" to "<a href="http://www.example.com" target="_blank">www.example.com</a>". Note that there should be another server block that defines your www web server.</p>

<p>To put the changes into effect, restart Nginx:</p>
<pre><code>sudo systemctl restart nginx
</code></pre>
<p>Note that if you are using HTTPS, the <code>listen</code> directive should be set to port <code>443</code> instead of <code>80</code>.</p>

<p>Use this curl command to ensure that the non-www domain redirects to the www domain (replace the highlighted part with your actual domain):</p>
<pre><code>curl -I http://example.com
</code></pre>
<p>You should get a <code>301 Moved Permanently</code> response, that shows the www redirect location, like this:</p>
<pre><code><div>Output:</div>HTTP/1.1 301 Moved Permanently
Server: nginx/1.4.6 (Ubuntu)
Date: Mon, 04 May 2015 18:20:19 GMT
Content-Type: text/html
Content-Length: 193
Connection: keep-alive
Location: http://www.example.com/
</code></pre>
<p>Of course, you should access your domain in a web browser (www and non-www) to be sure.</p>

<h2 id="conclusion">Conclusion</h2>

<p>That's it! Your Nginx permanent redirect is now configured properly, and your users will be able to access your web server via your non-www and www domain.</p>

    
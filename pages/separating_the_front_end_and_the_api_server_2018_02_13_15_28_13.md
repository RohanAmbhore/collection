<a href="http://www.jhipster.tech/separating-front-end-and-api/">http://www.jhipster.tech/separating-front-end-and-api/</a><div id="articleHeader"><h1> Separating the front-end and the API server</h1></div>

<h2 id="introduction">Introduction</h2>

<p>JHipster is a “full-stack” development tool, and its goal is to make you work efficiently with your front-end code (AngularJS/Angular) and your back-end code (Spring Boot).</p>

<p>However, it is a common requirement to separate the front-end and the back-end codes, typically because they are developed by different teams and have a different lifecycle.</p>

<p><strong>Pleae note</strong> that this isn’t the default JHipster way of working: this isn’t complex to do, and works well, but this is an advanced topic. If you are just getting started with JHipster, we recommend that you begin by using our standard way of working.</p>

<h2 id="generating-only-a-front-end-or-a-back-end-application">Generating only a front-end or a back-end application</h2>

<p>You can choose to generate only a JHipster back-end or JHipster front-end application. At generation time, this is only a matter of choosing flags which are described in our <a href="http://www.jhipster.tech/creating-an-app/" target="_blank">application generation documentation</a>:</p>

<ul>
  <li><code>jhipster --skip-client</code> will only generate a back-end application (this is typically what JHipster microservices are)</li>
  <li><code>jhipster --skip-server</code> will only generate a front-end application</li>
</ul>

<h2 id="directory-layout">Directory layout</h2>

<p>JHipster uses the standard Maven directory layout. When working on the back-end, you can just read the <a href="https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html" target="_blank">Maven standard directory layout documentation</a>.</p>

<p>When working on the front-end, there are 2 directories you need to know:</p>

<ul>
  <li><code>src/main/webapp</code> is where the client application will be developed</li>
  <li><code>target/www</code> is where your client application will be packaged</li>
</ul>

<p>If you have separate teams working on the front-end and back-end, you have two solutions:</p>

<ul>
  <li>Both teams can work on the same project. As the directories are separated, there won’t have much conflicts between teams. To make things even cleaner, both teams could work on separate branches.</li>
  <li>The front-end code can be stored in a specific Git project, and then imported into the main back-end project as a Git sub-module. This would require to move the client-side build scripts, but this is a simple refactoring.</li>
</ul>

<h2 id="http-requests-routing-and-caching">HTTP requests routing and caching</h2>

<p>Once the front-end and back-end have been separated, the issue will be how to handle HTTP requests:</p>

<ul>
  <li>All API calls will use a <code>/api</code> prefix. If you are using Angular, there is also a specific <code>SERVER_API_URL</code> constant, defined in the <code>webpack.common.js</code> configuration, that can enrich this prefix. For example, you can use <code>"http://api.jhipster.tech:8081/"</code> as a back-end API server (If you do this, please read our documentation on CORS below).</li>
  <li>Calls to <code>/</code> serve static assets (from the front-end), which should not be cached by the browser.</li>
  <li>Calls to <code>/app</code> (which contains the client-side application) and to <code>/content</code> (which contains the static content, like images and CSS) should be cached in production, as those assets are hashed.</li>
</ul>

<h1 id="using-browsersync">Using BrowserSync</h1>

<p>In <code>dev</code> mode, JHipster uses BrowserSync for hot-reload of the front-end application. BrowserSync has a proxy (<a href="https://www.browsersync.io/docs/options#option-proxy" target="_blank">here is its documentation</a>) that will route requests from <code>/api</code> to a back-end server (by default, <code>http://127.0.0.1:8080</code>).</p>

<p>This only works in <code>dev</code> mode, but this is a very powerful way of accessing different API servers from the front-end.</p>

<h2 id="using-cors">Using CORS</h2>

<p>CORS (<a href="https://wikipedia.org/wiki/Cross-origin_resource_sharing" target="_blank">Cross-origin request sharing</a>) allow to access different back-end servers with the same front-end, without configuring a proxy.</p>

<p>This is an easy-to-use solution, but it can be less secure in production.</p>

<p>JHipster provides out-of-the-box a CORS configuration:</p>

<ul>
  <li>CORS can be configured using the <code>jhipster.cors</code> property, as defined in <a href="http://www.jhipster.tech/common-application-properties/" target="_blank">the JHipster common application properties</a></li>
  <li>It is enabled by default in <code>dev</code> mode for monoliths and gateways. It is disabled by default for microservices as you are supposed to access them through a gateway.</li>
  <li>It is disabled by default in <code>prod</code> mode, for security reasons.</li>
</ul>

<h2 id="using-nginx">Using NGinx</h2>

<p>Another solution to separate the front-end and back-end codes is to use a proxy server. This is very common in production, and some teams also use this technique in development.</p>

<p>This configuration will change depending on your specific use-case, so this cannot be automated by the generator, here is below a working configuration.</p>

<p>Create a <code>src/main/docker/nginx.yml</code> Docker Compose file:</p>

<div><div><pre><code>version: '2'
services:
  nginx:
    image: nginx:1.13-alpine
    volumes:
    - ./../../../target/www:/usr/share/nginx/html
    - ./nginx/site.conf:/etc/nginx/conf.d/default.conf
    ports:
    - "8000:80"
</code></pre></div>

<p>This Docker image will configure an NGinx server, that reads the static assets from <code>target/www</code>: this is where the JHipster front-end application is generated by default. In production, you will probably have a specific folder for this.</p>

<p>It also reads a <code>./nginx/site.conf</code> file: this is a NGinx-specific configuration file. Here is a sample <code>site.conf</code>:</p>

<div><div><pre><code>server {
    listen 80;
    index index.html;
    server_name localhost;
    error_log  /var/log/nginx/error.log;

    location / {
        root /usr/share/nginx/html;
    }
    location /api {
        proxy_pass http://api.jhipster.tech:8081/api;
    }
    location /management {
        proxy_pass http://api.jhipster.tech:8081/management;
    }
    location /v2 {
       proxy_pass http://api.jhipster.tech:8081/v2;
    }
    location /swagger-ui {
        proxy_pass http://api.jhipster.tech:8081/swagger-ui;
    }
    location /swagger-resources {
        proxy_pass http://api.jhipster.tech:8081/swagger-resources;
    }
}
</code></pre></div>

<p>This configuration means that:</p>

<ul>
  <li>NGinx will run on port <code>80</code></li>
  <li>It will read the static assets in folder <code>/usr/share/nginx/html</code>, and</li>
  <li>It will act as a proxy from <code>/api</code> to <code>http://api.jhipster.tech:8081/api</code></li>
</ul>

<p>This configuration will require some tuning depending on your specific needs, but should be a good enough starting point for most applications.</p>

                        
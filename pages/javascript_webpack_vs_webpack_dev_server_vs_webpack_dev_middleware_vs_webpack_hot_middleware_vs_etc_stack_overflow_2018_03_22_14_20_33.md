<a href="https://stackoverflow.com/questions/42294827/webpack-vs-webpack-dev-server-vs-webpack-dev-middleware-vs-webpack-hot-middlewar">https://stackoverflow.com/questions/42294827/webpack-vs-webpack-dev-server-vs-webpack-dev-middleware-vs-webpack-hot-middlewar</a><div id="articleHeader"><h1>Webpack vs webpack-dev-server vs webpack-dev-middleware vs webpack-hot-middleware vs etc</h1></div>

<p>I'm starting working with <code>webpack</code> with a <code>node/express</code> environment developing a <code>ReactJS</code> server side rendered application with <code>react-router</code>. I'm getting very confused about the role of each webpack package for dev and prod (runtime) environments.</p>

<p>Here is the summary of my understanding:</p>

<p><code>webpack</code>: Is a package, a tool to join together different pieces of an web application and bundle then in a single .js file (normally <code>bundle.js</code>). The result file is then served in a prod environment to be loaded by the application and contains all necessary components to run the code. Features include shrinking code, minifying, etc.</p>

<p><code>webpack-dev-server</code>: Is a package that offers a <strong>server</strong> to process the website files. It also builds a single .js file (<code>bundle.js</code>) from client components but serves it in memory. If also has the option (<code>-hot</code>) to monitor all the building files and build a new bundle in memory in case of code changes. The server is served directly in the browser (ex: <code>http:/localhost:8080/webpack-dev-server/whatever</code>). The combination of in memory loading, hot processing and browser serving let the user get the application updated on browser when the code changes, ideal for development environment. </p>

<p><strong><em>If I have doubts about the above text, I'm really not sure about the content below, so please advise me if necessary</em></strong></p>

<p>A common problem when using <code>webpack-dev-server</code> with <code>node/express</code> is that <code>webpack-dev-server</code> is a server, as is <code>node/express</code>. That makes this environment tricky to run both the client and some node/express code (an API etc.). <strong><em>NOTE: This is what I've faced but would be great to understand why does that happens in more details...</em></strong></p>

<p><code>webpack-dev-middleware</code>: This is a middleware with same functions of <code>webpack-dev-server</code> (inmemory bundling, hot reloading), but in format that can be injected to the <code>server/express</code> application. In that way, you have a sort of server (the <code>webpack-dev-server</code>) insider the node server.  <strong><em>Oops: Is this a crazy dream ??? How can this piece solve the dev and prod equation and makes life simpler</em></strong></p>

<p><code>webpack-hot-middleware</code>: This... <strong><em>Stuck here... found this piece when looking for <code>webpack-dev-middleware</code>... No idea how to use it.</em></strong> </p>

<p>ENDNOTE: Sorry is there is any wrong thinking. I really need help in order to undestand these variants in a complex environment. If conveninent, please add more packages/data that will build the whole scenario.</p>
    
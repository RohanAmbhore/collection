<a href="http://getfirefly.org/">http://getfirefly.org/</a><div id="articleHeader"><h1>Philosophy</h1></div>

  <p>Firefly does away with a lot of the stuff that teams of professional engineers use to build large, high-volume, scalable applications. Instead, it's designed to help people without backend experience learn and build simple sites quickly.</p>

  <p>It embraces modern javascript syntax, the NPM ecosystem, single-page front-end applications, serverless backends, schemaless databases, and 3rd-party APIs for hard things like authentication and search—all to keep the codebase small and easier to "reason about". Firebase has no server to monitor, no database instance to host, no REST API to build, no containers, no password salts, no migrations, and no real need to learn HTTP or SQL.</p>

  <p>That said, we never go bleeding edge: all <a href="https://github.com/sampl/firefly/blob/master/package.json" target="_blank">Firefly dependencies</a> are used by large tech companies in production, are hugely popular in the community, and will likely be supported for years to come.</p>


  <h1 id="how-it-works">How it works</h1>

  <p>Firefly isn't a framework or library—it's just a boilerplate that you can copy when starting a new project.</p>

  <p>When you first copy Firefly and start it up, you'll see an empty list of "posts" (imagine blog posts, or wiki pages). Users can read individual posts or search for posts. Once they log in, they can like posts or create and edit their own posts. You can play with a live Firefly demo at <a href="https://demo.getfirefly.org/" target="_blank">demo.getfirefly.org</a> to see how it works.</p>

  <p>To make the project your own, simply find-and-replace all the instaces of "Firefly" and "posts" to match your own project and data.</p>

  <p>Let's take a closer look at the different parts of Firefly:</p>

  <h2 id="how-it-works-views">Views</h2>

  <p>Most of Firefly is built with <a target="_blank">React</a>. React can feel weird at first—it looks funny, and it doesn't use normal HTML and CSS. Stick with it though—using components will feel like a revelation soon. Get started by reading the excellent <a href="https://facebook.github.io/react/docs/hello-world.html" target="_blank">official React guide</a>.</p>

  <h3>Presentation views</h3>

  <p>The main UI of a firebase app is a bunch of simple React components in the /views folder. These are usually stateless, presentational components written in the simple functional React style. Think of them like templates in MVC--their job is basically just to show HTML.</p>

  <h3>Styles</h3>

  <p>Firefly uses styled-components to add style. These are React components written with CSS, and they live in the /styles folder. Think of them as a replacement for SASS or LESS files.</p>

  <h3>Routing</h3>

  <p>The router is the part of the app that shows different React components based on the browser URL. React has no built-in router, so we use the popular <a href="https://reacttraining.com/react-router/web/guides" target="_blank">React Router</a>. All our app's routes live in the Routes.js file.</p>


  

  <p>Instead of a datastore like Redux, in Firefly you directly query the using Firebase</p>

  <h3>The database</h3>
  <p>Firefly uses the NoSQL <a target="_blank">Firebase Firestore database</a> for saving data. Firestore organizes your data into "collections" (kind of like SQL tables) which have "documents" (kind of like rows, or big blobs of JSON). You write to the Firebase database directly from the user's web browser (no server required). Before you go much further, you should read the <a href="https://firebase.google.com/docs/firestore/web/start" target="_blank">Firebase Firestore Database Guide</a>.</p>
  <p>Firestore queries use javascript Promises to make async requests and error handling very simple. If you're not familiar with promises, learn a bit about <a href="https://www.youtube.com/watch?v=f8IgdnYIwOU" target="_blank">how promises work</a>.</p>

  <h3>Data providers</h3>
  <p>So how do you get your data into your views? Firefly comes with a bunch of "provider" react components in the /data folder to do just that--their responsibility is to listen for data from the database and pass it down to the views using the <a href="https://reactjs.org/docs/render-props.html" target="_blank">render prop</a> pattern.</p>
  <p>Many other React apps use something like <a href="https://egghead.io/courses/getting-started-with-redux" target="_blank">Redux</a> to keep their UI up-to-date when data changes, but many developers agree that <a target="_blank">Redux is overkill</a> for a lot of simple apps, so Firefly just uses render methods and Firebase subscriptions.</p>

  <h3>Securing your data</h3>
  <p>Because any browser can write data directly into your database, you need some Firebase security rules to keep hackers from deleting data or viewing private stuff. Firefly comes with a default set of rules for posts that you can use can copy. <a href="https://firebase.google.com/docs/database/security" target="_blank">This video</a> does a great job explaining how these rules work.</p>

  

  <h3>Authentication</h3>
  <p>Firefly uses <a href="https://firebase.google.com/docs/auth/web/start" target="_blank">Firebase Authentication</a> for logging users in.</p>
  


  <h3>Actions</h3>

  <p>OK, so now you know how Firefly shows UI with data from the database. But how do you make the app change when the user clicks something?</p>

  <p>The answer in Firefly is "actions"—plain old javascript functions that live in the "actions" folder. When the user wants to add a post, for example, the "add post" view will call the "add post" action, which takes care of sending the new post to the database. When the database gets the new post, the data providers will automatically send it to the views so everything's always up-to-date.</p>


  <h2 id="how-it-works-other">Other stuff</h2>

  <p>Firefly uses <a target="_blank">Create React App</a> to take care of transpiling, bundling, linting, and running tests. You don't have to write or manage any configuration for this to work, just run <code>npm start</code>.</p>

  <p>The deployment scripts use Firebase hosting to host your app when you're ready to go live. Firebase hosting comes with HTTPS for free, and it's the same price as Google Cloud Platform object storage (cheap), and works well with the other Firebase services like backend functions and your database.</p>


  <h1 id="getting-started">Getting Started</h1>

  <div>
    <h3 id="getting-started-quick-start">Quick start</h3>

    <ol>
      <li>
        Clone the repo and install the packages with
        <code>git clone https://github.com/sampl/firefly && cd firefly && npm install</code>
      </li>
      <li>
        Remove `.example` from the names of your environment files with
        <code>mv .firebaserc.example .firebaserc && mv env.dev.example env.dev && mv .env.stage.example .env.stage && mv .env.live.example .env.live</code>
      </li>
      <li>Create firebase projects in the <a href="https://console.firebase.google.com/" target="_blank">Firebase console</a> and add keys to <code>.firebaserc</code> and the <code>.env</code> files</li>
      <li>Start development with <code>npm start</code> and deploy with <code>npm run live</code></li>
    </ol>
  </div>

  <h2 id="getting-started-prerequisites">Before you begin</h2>

  <p>You'll need <a href="https://en.wikipedia.org/wiki/Git" target="_blank">git</a> to use Firefly. If you don't already know how to use git, <a href="https://www.codecademy.com/learn/learn-git" target="_blank">you can learn on Codecademy</a>.</p>

  <p><a href="https://nodejs.org/en/download" target="_blank">Download and install Node JS</a> if you haven't already.</p>

  <p>Run <code>npm install -g firebase-tools</code> to install the <a href="https://firebase.google.com/docs/cli/" target="_blank">Firebase command line tools</a>. You only need to do this once per computer.</p>

  <h2 id="getting-started-create">Creating your app</h2>

  <h3>Get the code</h3>

  <p>Firefly is a boilerplate, so to start a new Firefly project, we just make a copy of Firefly.</p>

  <ol>
    <li>In your terminal, <code>cd</code> to the folder where you want your project to live</li>
    <li>Clone this repo by running <code>git clone https://github.com/sampl/firefly</code></li>
    <li>Move "into" the folder you just created with <code>cd firefly</code> (you can also safely rename the <code>firefly</code> folder to the name of your project)</li>
    <li>Run <code>npm install</code> to install all the javascript packages Firefly needs</li>
  </ol>

  <h3>Connect to the database</h3>

  <p>Firefly projects only have one codebase, but use three Firebase projects. Each project has its own URL and its own separate copy of the database. This lets you develop and stage your app without affecting the live version.</p>
  <ol>
    <li>Go to the <a href="https://console.firebase.google.com" target="_blank">Firebase console</a> and sign in with your Google account</li>
    <li>Create three new projects, and name them something like <code>MyProject Dev</code>, <code>MyProject Stage</code>, and <code>MyProject LIVE</code></li>
  </ol>

  <p>Now let's connect our databases to our app by adding their "keys" to our app's environment ("env") files. You should generally keep connection keys like this secret, so first we'll rename our environment files to keep them from getting committed into git (the new filenames are listed in <code>.gitignore</code>).</p>

  <ol>
    <li>First, rename <code>.firebaserc.example</code> to <code>.firebaserc</code> and replace the blank space next to "development" with the <code>projectId</code> from the Firebase website.</li>
    <li>Rename <code>.env.dev.example</code> to <code>.env.dev</code>, and do the same thing for the stage and live files. Replace the blank spaces in that file with the codes from the Firebase website too.</li>
    <li>Now back on the Firebase website, click "Add Firebase to your web app" for each new project</li>
    <li>You'll see a block of code with info like "project id" and "API key"—add these values to your firebaserc and your dev, stage and live env files.</li>
  </ol>


  <h3>Set up authentication</h3>

  <p>Before you can add any posts, you'll have to allow sign-in with Google. Firebase makes this very easy.</p>

  <ol>
    <li>Back in the <a href="https://console.firebase.google.com/" target="_blank">Firebase console</a>, click on "Authentication" in the sidebar on the left</li>
    <li>Click "Set up sign-in method"</li>
    <li>Click "Google", toggle the "Enable" switch, and hit "Save"</li>
  </ol>


  <h3>Set up Firebase Functions</h3>

  <p>Before your app can run any backend functions.</p>

  Firebase Cloud Functions only work if your project has a paid plan, so <a href="https://console.firebase.google.com" target="_blank">upgrade your Firebase project</a> to "Blaze". This should still be free to use (unless you get a lot of traffic).
  <p><a href="https://firebase.google.com/docs/admin/setup#add_firebase_to_your_app" target="_blank">Create a Service Account</a> to run maintenance scripts</p>


  <h3>Other services</h3>

  <p>Firefly comes with a search powered by <a href="https://www.algolia.com" target="_blank">Algolia</a>. To enable search, <a href="https://www.algolia.com" target="_blank">create an account</a>, <a href="https://firebase.google.com/docs/functions/config-env" target="_blank">configure your functions credentials</a>. See <a href="https://github.com/sampl/firefly/blob/master/functions/index.js" target="_blank">index.js</a> for full instructions.</p>

  <p>There's also a simple <a href="https://stripe.com/" target="_blank">Stripe</a> integration for creating subscriptions and charging users. If you're not asking users for money, you can get rid of the files with "subscription" in the name. If you are, add your Stripe keys to the <code>.env</code> files and your Firebase functions config.</p>

  <p>Firefly also comes with <a href="https://analytics.google.com/" target="_blank">Google Analytics</a> for tracking page views and <a href="https://docs.sentry.io/clients/javascript/" target="_blank">Sentry</a> for monitoring errors. To use them, just create an account and project on each site, then add your tracking codes to your <code>.env</code> files.</p>


  <h2 id="getting-started-working">As you work</h2>

  <h3>Develop</h3>

  <p>Start your app with <code>npm start</code>. You should see a basic web app in your browser! 😎</p>

  <p>Try logging in, then make sure you can create, like, edit, and delete posts.</p>

  <p>Now go back to your text editor and try editing some files. When you save, the changes should automatically appear in the browser.</p>

  <p>Now is probably a good time to CTRL-F for all the instances of "Firefly" in the codebase and rename them to the name of your project. You should also probably do this for "post", too.</p>


  <h3>Deploy</h3>

  <p>Firefly is insecure by default. <strong>Before going live, <a href="https://firebase.google.com/docs/database/security" target="_blank">secure your app</a> by writing rules in <code>database.rules.json</code></strong></p>

  <p>You can deploy your project to your test stage URL by running <code>npm run stage</code>.</p>

  <p>When it's time to go live, run <code>npm run live</code>!</p>


  <h2 id="getting-started-next-steps">Next Steps</h2>

  <ul>
    <li>Since Firefly is just a Javascript app, adding javascript packages is as simple as running an <code>npm install foo</code> and adding <code>import Foo from 'foo'</code> in your code.</li>

    <li>This <a href="https://github.com/agarrharr/awesome-static-website-services" target="_blank">Awesome Static Website Services</a> has a lot of examples of things that you can integrate with a Firefly-style app.</li>

    <li>The <a href="https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md" target="_blank">Create React App user guide</a> has a ton of great guides for adding things like CSS Preprocessors, unit testing, and more.</li>

    <li>Firebase has a large repo of <a href="https://github.com/firebase/functions-samples" target="_blank">Firebase functions samples</a> for common backend tasks like sending emails and taking payments.</li>
  </ul>

  <p>That's it!</p>

  <p>Remember that <strong>learning this stuff is always hard—for everyone</strong>. Take small bites and keep at it. Eventually you'll build something amazing.</p>

  <p>🎉 🎉 🎉</p>

  <em>Did I miss something? Was something confusing? I'd love to hear from you; <a href="https://github.com/sampl/firefly/issues" target="_blank">submit an issue</a> or <a href="https://github.com/sampl/firefly/pulls" target="_blank">pull request</a>.</em>

  <footer>by <a href="http://sampl.us/" target="_blank">Sam Pierce Lolla</a> at <a href="http://directedworks.com/" target="_blank">Directed Works</a></footer>


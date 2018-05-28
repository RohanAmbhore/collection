<a href="https://alligator.io/angular/environment-variables">https://alligator.io/angular/environment-variables</a><div id="articleHeader"><h1>Environment Variables in Angular</h1></div><p>Need to use different values depending on the environment you’re in? If you’re building an app that talks to the Stripe API for example, you’ll want to use your test publishable key during development and then your live publishable key in production. It’s easy to do in Angular using the <em>environment.ts</em> file.</p><p> This post applies to Angular 2+ apps.</p><p><a href="/angular/angular-cli/" target="_blank">Angular CLI</a> projects already use a <em>production</em> environment variable to enable production mode when in the production environment:</p><p>main.ts</p><pre><code>// ...

if (environment.production) {
  enableProdMode();
}

// ...</code></pre><p>And you’ll also notice that by default in the <code>/src/environment</code> folder you have an environment file for development and one for production. Let’s say we want to be a different animal depending if we’re in development or production mode:</p><p>environment.ts</p><pre><code>export const environment = {
  production: false,
  animal: '🐊'
};</code></pre><p>environment.prod.ts</p><pre><code>export const environment = {
  production: false,
  animal: '🐔'
};</code></pre><p>And in our component all we have to do in order to access the variable is the following:</p><p>app.component.ts</p><pre><code>import { Component } from '@angular/core';
import { environment } from '../environments/environment';

@Component({ ... })
export class AppComponent {
  animal: string = environment.animal;
}</code></pre><p>And it’s as simple as that! Angular takes care of swapping the environment file for the correct one.</p><p>Now in development mode the <em>animal</em> variable resolves to 🐊 and in production, if you run <code>ng build --prod</code> for example, <em>animal</em> resolves 🐔.</p><h2 id="detecting-development-mode-with-isdevmode">Detecting Development Mode With <em>isDevMode()</em></h2><p>Angular also provides us with an utility function called <em>isDevMode</em> that makes it easy to check if the app in running in dev mode:</p><pre><code>import { Component, OnInit, isDevMode } from '@angular/core';

@Component({ ... })
export class AppComponent implements OnInit {
  ngOnInit() {
    if (isDevMode()) {
      console.log('👋 Development!');
    } else {
      console.log('💪 Production!');
    }
  }
}</code></pre><h2 id="adding-a-staging-environment">Adding a Staging Environment</h2><p>It’s easy to add new environments in Angular CLI projects by adding new entries to the <em>environments</em> field in the <code>.angular-cli.json</code> file. Let’s add a staging environment for example:</p><p>.angular-cli.json</p><pre><code>"environments": {
  "dev": "environments/environment.ts",
  "prod": "environments/environment.prod.ts",
  "staging": "environments/environment.staging.ts"
}</code></pre><p>And now we can add a staging environment file and suddenly be a 🐻 if we build the project with <code>ng build --env=staging</code>:</p><p>environment.staging.ts</p><pre><code>export const environment = {
  production: true,
  animal: '🐻'
};</code></pre>
<a href="https://vuejsdevelopers.com/2018/01/29/vue-js-e2e-test-hacker-news?utm_source=mybridge&utm_medium=blog&utm_campaign=read_more">https://vuejsdevelopers.com/2018/01/29/vue-js-e2e-test-hacker-news?utm_source=mybridge&utm_medium=blog&utm_campaign=read_more</a><div id="articleHeader"><h1>End-To-End Testing A VueJS HackerNews Clone</h1></div>  <p>In this blog post I will show how to test a HackerNews clone without pulling out hair.</p> <p>There is an elegant and fast Vue.js 2 HackerNews clone made by the framework’s author himself: <a href="https://github.com/vuejs/vue-hackernews-2.0" target="_blank">vuejs/vue-hackernews-2.0</a> with live demo hosted at <a href="https://vue-hn.now.sh/" target="_blank">https://vue-hn.now.sh/</a>. The clone has all the bells and whistles one can expect from a modern progressive application: includes server-side rendering, inlined CSS, routing, single file components, etc. There is only one thing the code is missing - tests! Hmm.</p> <p><div class="readableLargeImageContainer"><img src="https://d33wubrfki0l68.cloudfront.net/55fbeff5600e367322d9e83d5dafd9d24d0ec89a/84ed3/images/posts/e2e_hn.png" alt="HackerNews with Vue" /></div></p> <p>What would it take to quickly confirm that this project is working? Would you need to jump through hoops if you wanted to add tests? Would you write unit tests or would end-to-end tests be better? Would the tests work in a modern browser or using JavaScript DOM emulation? Would the entire experience be full of pain and misery?</p> <p>I will show you can <em>quickly</em> write lots of end-to-end tests without any pain. These tests are most important ones - because they ensure that the deployed application is actually usable by the end user. My tool of choice is <a href="https://www.cypress.io" target="_blank">Cypress</a> - our open source free test runner.</p> <h3>Setup</h3> <p>I start testing by forking the repository and getting a local copy.</p> <div><pre><code>git clone git@github.com:bahmutov/vue-hackernews-2.0.git
cd vue-hackernews-2.0
npm install
</code></pre></div>  <p>I add <code>cypress</code> NPM dependency. It is a self-contained Electron-based cross-platform module that can be installed on any system that has at least Node v4+.</p> <div><pre><code>$ npm i -D cypress
&gt; cypress@1.4.1 postinstall /git/vue-hackernews-2.0/node_modules/cypress
&gt; node index.js --exec install

Installing Cypress (version: 1.4.1)

 ✔  Downloaded Cypress
 ✔  Unzipped Cypress
 ✔  Finished Installation /git/vue-hackernews-2.0/node_modules/cypress/dist/Cypress.app

You can now open Cypress by running: node_modules/.bin/cypress open

<a href="https://on.cypress.io/installing-cypress" target="_blank">https://on.cypress.io/installing-cypress</a>
+ cypress@1.4.1
added 120 packages in 24.149s
</code></pre></div> <p>I open Cypress once and it scaffolds its settings file <code>cypress.json</code> and a folder with spec files.</p> <div><pre><code>$ $(npm bin)/cypress open
It looks like this is your first time using Cypress: 1.4.1

 ✔  Verified Cypress!

Opening Cypress...
</code></pre></div> <p><img alt="Scaffolded project" /></p> <h3>First test</h3> <p>The generated <code>cypress/integration/example_spec.js</code> file is useful to anyone starting with Cypress - it contains lots of example tests you can execute right away. Because I know the tests I want to show, I will clear the entire file and rename it to just <code>cypress/integration/spec.js</code>. Here is my first test.</p> <div><pre><code>// cypress/integration/spec.js
describe('HackerNews', () =&gt; {
  it('loads', () =&gt; {
    cy.visit('<a href="https://vue-hn.now.sh/" target="_blank">https://vue-hn.now.sh/</a>')
    cy.contains('Built with Vue.js')
  })
})
</code></pre></div> <p>I can keep Cypress open while renaming spec files or writing tests - the test runner is watching files and reruns the tests automatically. The first test passes.</p> <p><img alt="First test" /></p> <p>Despite the test’s simplicity, there is a LOT going under the hood though. The test runner proxies all requests thus <a href="https://on.cypress.io/visit" target="_blank"><code>cy.visit</code></a> <em>knows</em> that the server successfully responded with an HTML page. Only after the page has loaded the test runner checks if it contains text “Build with Vue.js”. Because the world is asynchronous, and any content on the page might be dynamic, Cypress will intelligently wait several seconds for it. If the app is fast, and the text appear quickly - that’s great, the test moves on to the next assertion immediately. But if the server takes a few seconds to cold-start - no big deal, the test runner will not fail. This makes Cypress <em>fast and flake-free</em>.</p> <p>Checking for static text is not much fun. Let’s make sure we are getting actual news items. I open DevTools (Cypress is running tests in either built-in Electron browser, or any installed Chrome-like browser, Firefox <a href="https://github.com/cypress-io/cypress/issues/1096" target="_blank">support is coming</a>). Luckily, the application has nice class names we can use to select list elements.</p> <p><img alt="List elements" /></p> <h3>Items test</h3> <p>The second test will make sure the application displays 30 news items.</p> <div><pre><code>it('loads news items', () =&gt; {
  cy.visit('<a href="https://vue-hn.now.sh/" target="_blank">https://vue-hn.now.sh/</a>')
  cy.get('.news-item').should('have.length', 30)
})
</code></pre></div> <p>The test runner reruns our tests, and … hmm … it fails.</p> <p><img alt="Failing test" /></p> <p>Luckily, a single look at the error message is enough to diagnose the problem. Hovering over the error message or clicking on it even shows the DOM snapshot and all the elements selected during the command. I assumed that the application would show 30 news items, just like the original <a href="https://news.ycombinator.com/" target="_blank">https://news.ycombinator.com/</a>, but this app only shows 20. I will change the assertion to make sure there are more than 10 items. Cypress comes with all <a href="on.cypress.io/assertions" target="_blank">Chai, jQuery-Chai and Sinon-Chai</a> assertions, and you can add your own libraries.</p> <div><pre><code>// need at least 10 items
cy.get('.news-item').should('have.length.gt', 10)
</code></pre></div> <p>Everything is green again.</p> <p><img alt="Minimum number of items" /></p> <h3>Configuration</h3> <p>Before I wrote any more tests, let’s avoid duplicate <code>cy.visit</code> code. We can move the URL to <code>cypress.json</code> file for example.</p> <div><pre><code>{
  "baseUrl": "<a href="https://vue-hn.now.sh" target="_blank">https://vue-hn.now.sh</a>"
}
</code></pre></div> <p>Besids <code>baseUrl</code> there a lot of <a href="https://on.cypress.io/configuration" target="_blank">configuration options</a> you can pass via <code>cypress.json</code> file, CLI options or environment variables. I suggest installing <a href="https://on.cypress.io/configuration#IntelliSense" target="_blank">cypress.json schema file</a> to get IntelliSense support. It suggest options as you start typing new property name or hover over existing settings. For example, this tooltip explains the <code>baseUrl</code> configuration variable.</p> <p><img alt="Configuration IntelliSense" /></p> <p>Next I update my spec file and move opening the page to <code>beforeEach</code> callback.</p> <div><pre><code>/* eslint-env mocha */
/* global cy */
describe('HackerNews', () =&gt; {
  beforeEach(() =&gt; {
    cy.visit('/')
  })
  it('loads', () =&gt; {
    cy.contains('Built with Vue.js')
  })
  it('loads news items', () =&gt; {
    cy.get('.news-item').should('have.length.gt', 10)
  })
})
</code></pre></div> <p>I am also showing two comments to make my linter happy - Cypress uses BDD convention, thus <code>eslint-env mocha</code> tell linter to accept global <code>describe, beforeEach, it</code> functions. Variable global <code>cy</code> is injected automatically and has an <a href="https://www.cypress.io/api" target="_blank">extensive API of commands</a> for the tests to use.</p> <h3>Routing test</h3> <p>Let us make sure the routing works. The application should display more news when clicking on the “more &gt;” anchor. It should also go back to the first page using browser’s “back” button. When we are at the first page, we should not be able to go to the previous page. Let’s test this.</p> <div><pre><code>it('goes to the second page and back', () =&gt; {
  cy.contains('.news-list-nav a', 'more &gt;').click()
  cy.url().should('contain', '/top/2')
  cy.go('back')
  cy.url().should('contain', '/top')
})
it('cannot go to the previous page', () =&gt; {
  cy.contains('.news-list-nav a', '&lt; prev')
    .should('have.class', 'disabled')
})
</code></pre></div> <p>The traditional rule of thumb tells developers to write small tests with a single assertion per test. But at Cypress we have invested a lot of time into <a href="https://www.cypress.io/blog/2017/07/26/good-error-messages/" target="_blank">helpful error messages</a>. Not only the test runner is going to tell exactly the reason why a test fails, on CI it will take a screenshot automatically! Plus video recording is turned on by default - thus you will <em>see</em> the steps leading to the failure. So I feel comfortable testing entire scenarios rather than individual actions.</p> <p>Here is another such scenario. There are comments for each news item. I should be able to click on the comments link, read the comments, then go back to the main list. First, I need to know the selector of the comments link. Rather than “hunting” in the DevTools, I can click on “CSS Selector Playground” target icon and then on the desired item.</p> <p><img alt="CSS Selector Playground" /></p> <p>The playground tool suggests selector string <code>cy.get(':nth-child(1) &gt; .meta &gt; .comments-link &gt; a')</code>, but we can split it up into <code>cy.get('.news-item').first().find('.meta .comments-link')</code>. When we click on the link, we are going to the comments page. There is a (brief) loading spinner and then the comments appear. Finally, we can go back to the “Top” news page by using a navigation link.</p> <div><pre><code>it('goes to comments and back', () =&gt; {
  // see comments for the first story
  cy.get('.news-item')
    .first().find('.meta .comments-link')
    .click()
  // loader disappears, and comments are there
  cy.get('.item-view-comments-header .spinner').should('not.be.visible')
  // note: there might be zero comments
  cy.get('.comment')
    .should('have.length.gte', 0)
    .and('be.visible')
  // go to the top news
  cy.get('nav').contains('Top').click()
  cy.url().should('contain', '/top')
})
</code></pre></div> <p>The result shows the test going through the entire scenario, ensuring that many components of the app are working as expected.</p> <p><img alt="Comments and Top news" /></p> <h3>Continuous Integration</h3> <p>Running Cypress locally is great, but what about our continuous integration server? We want to execute the tests and see every failure somehow. Every CI provider is supported by Cypress - either right out of the box or through the provided <a href="https://github.com/cypress-io/cypress-docker-images" target="_blank">Docker images</a>, but we recommend using our <a href="https://www.cypress.io/dashboard/" target="_blank">dashboard service</a> to store test results, screenshots and videos. It is a quick setup. From the desktop click “Runs” button.</p> <p><img alt="Runs" /></p> <p>Each user by default gets a personal organization - or you can create new organization for your team. I will add a new project under my own account, and its results will be publicly visible.</p> <p><img alt="Project recording" /></p> <p>The modal gives me the command to use on my CI server to execute the tests while recording the results on the dashboard. Copy the record key - we will keep it private. The simplest CI to setup for a public GitHub project is Travis. I added the record key I just copied as an environment variable.</p> <p><img alt="Travis" /></p> <p>The <code>.travis.yml</code> file executes <code>cypress run --record</code> command.</p> <div><pre><code>language: node_js
node_js:
  - '8'
cache:
  directories:
    - ~/.npm
    - node_modules
script:
  - $(npm bin)/cypress run --record
</code></pre></div> <p>Push the code to GitHub and watch the tests <a href="https://travis-ci.org/bahmutov/vue-hackernews-2.0/builds/332310458" target="_blank">run on CI</a>. Now head over to the <a href="https://dashboard.cypress.io/#/projects/b1sfu5/runs" target="_blank">Cypress Dashboard</a> and see test results nicely organized, including video of the entire run!</p> <p><img alt="Project runs" /></p> <p><img alt="Project run video" /></p> <p>The entire setup took less than a minute.</p> <h3>Final thoughts</h3> <p>Our Cypress team has put a lot of thought into designing the most developer-friendly end-to-end test runner. It includes <a href="https://on.cypress.io/api" target="_blank">powerful API</a>, <a href="https://on.cypress.io/screenshots-and-videos" target="_blank">built-in recording</a>, <a href="https://on.cypress.io/continuous-integration" target="_blank">simple CI setup</a> and many <a href="https://www.cypress.io/features" target="_blank">other features</a> that make the testing experience truly painless. We appreciate any feedback (positive and negative) through the usual channels: GitHub issues, Gitter chat and even Tweets.</p> <p>If you would like to try Cypress (and why not, it is free and open source!) follow these links</p>  <p>If you want to try experimental code, we have built a Cypress plugin for unit testing Vue code. It is like a cross between end-to-end tests and <a href="https://storybook.js.org/" target="_blank">Storybook.js</a>. You can find it at <a href="https://github.com/bahmutov/cypress-vue-unit-test" target="_blank">bahmutov/cypress-vue-unit-test</a>.</p> <p>For Cypress updates, follow <a href="https://twitter.com/Cypress_io" target="_blank">@cypress_io</a> on Twitter.</p> 
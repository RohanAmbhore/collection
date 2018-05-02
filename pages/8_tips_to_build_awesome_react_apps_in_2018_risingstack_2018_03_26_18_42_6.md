<a href="https://blog.risingstack.com/8-tips-to-build-better-react-apps-in-2018/">https://blog.risingstack.com/8-tips-to-build-better-react-apps-in-2018/</a><div id="articleHeader"><h1>8 Tips to Build Awesome React.js Apps in 2018</h1></div>
<section>

by <a href="/author/bertalan" target="_blank"><b>Bertalan Miklos</b></a>(<a href="https://twitter.com/@solkimicreb1" target="_blank">@solkimicreb1</a>), Full-Stack Developer at RisingStack
</section>
</header>

<p>New year, better code: mind these React.js best practices to improve the quality of your code. <strong>This post is a short collection of essential React.js tips and tricks for 2018.</strong> I hope that everyone finds something useful among them.</p>
<h2 id="tip1usereact16">Tip #1: Use React 16</h2>
<p>React 16 was released 4 months ago! It is time for everyone to start using it. Chances are that you can migrate with a simple version bump and it provides some neat improvements. My favorites are the <a href="https://reactjs.org/blog/2017/09/26/react-v16.0.html#new-core-architecture" target="_blank">Fiber Architecture</a> and the <a href="https://reactjs.org/blog/2017/09/26/react-v16.0.html#support-for-custom-dom-attributes" target="_blank">support for custom DOM attributes</a>. Pick your top features from the official <a href="https://reactjs.org/blog/2017/09/26/react-v16.0.html" target="_blank">release notes</a> and start using them.</p>
<h2 id="tip2keepitsimple">Tip #2: Keep it simple</h2>
<p>Choose your tools wisely and never overcomplicate. <a href="https://github.com/facebookincubator/create-react-app" target="_blank">Create-react-app</a> bootstraps new projects in seconds, <a href="https://github.com/zeit/serve" target="_blank">serve</a> lets you share it on your network with a single command and <a href="https://zeit.co/now" target="_blank">now</a> deploys it to the internet ... with a single command.</p>
<p>Work with easy-to-use tools that you are comfortable with. Let the project develop over time and never throw in complex technologies when you don't need them.</p>
<h2 id="tip3learnreactjspatterns">Tip #3: Learn React.js patterns</h2>
<p>Libraries come and go, but good patterns are immortal. Learn the common patterns that inspire your favorite React.js projects from the <a href="https://reactpatterns.com/" target="_blank">React Patterns</a> page.</p>
<p>If any of them draws your interest you can deepen your knowledge in the following articles about <a href="https://medium.com/@franleplant/react-higher-order-components-in-depth-cf9032ee6c3e" target="_blank">higher order components</a>, <a href="https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0" target="_blank">container and presentational components</a>, <a href="https://goshakkk.name/controlled-vs-uncontrolled-inputs-react/" target="_blank">controlled and uncontrolled inputs</a> and <a href="https://medium.com/merrickchristensen/function-as-child-components-5f3920a9ace9" target="_blank">function as child components</a>.</p>
<h2 id="tip4trynewthingsfromthereactjsecosystem">Tip #4: Try new things from the React.js ecosystem</h2>
<p>Don't be afraid to try new things if you have the time. React.js has an incredible ecosystem, you can almost always find a ready-to-go solution for your problems. Run through the <a href="https://github.com/enaqx/awesome-react" target="_blank">awesome-react list</a> and find what draws you attention. Be sure to check out the many tooling, styling and state management libraries and take a look at the example projects when you are out of inspiration.</p>
<h2 id="tip5embracetheplatform">Tip #5: Embrace the platform</h2>
<p>Users expect wep apps to be navigable with history buttons, to be shareable by URL and to keep session in web storage. When any of these are missing, people get frustrated. Make that extra effort and integrate properly with the browser.</p>
<p>While you get these right, get familiar with the new <a href="https://developer.mozilla.org/en-US/docs/WebAPI" target="_blank">Web APIs</a>. Things have changed a lot in the last few years. Web pages have increasing control over the underlying device, make good use of it!</p>
<h2 id="tip6gooffline">Tip #6: Go offline</h2>
<p>Be awesome and optimize for shaky connections. The <a href="https://developers.google.com/web/fundamentals/instant-and-offline/offline-cookbook/" target="_blank">Offline Cookbook</a> gives a detailed overview about the different offline caching strategies with Service Workers. This is still pretty new tech, but browser support is <a href="https://caniuse.com/#feat=serviceworkers" target="_blank">catching up</a>.</p>
<p>Don't worry if the cookbook is overwhelming at first. Create-react-app gives your app shell offline support out of the box, which is a nice start. You still have to prepare your data for offline usage though. <a href="https://developers.google.com/web/tools/workbox/" target="_blank">Google Workbox</a> and <a href="https://firebase.google.com/" target="_blank">Firebase</a> can get you started.</p>
<h2 id="tip7optimizeforslowdevices">Tip #7: Optimize for slow devices</h2>
<p>People may use your web app on low-end devices with awful connections. Do not be satisfied with its speed on your MacBook, but never get obsessed with performance either. Stick to this simple rule: measure before you act.</p>
<p>Use <a href="https://developers.google.com/web/tools/lighthouse/" target="_blank">Lighthouse</a> to get a rough idea about what needs improvement, then go on with the new <a href="https://github.com/FormidableLabs/webpack-dashboard" target="_blank">webpack dashboard</a> or <a href="https://github.com/webpack-contrib/webpack-bundle-analyzer" target="_blank">webpack bundler analyzer</a> to see where can you cut down on size.</p>
<p>If you really need everything you import, performance can still be improved with <a href="https://developers.google.com/web/updates/2017/11/dynamic-import" target="_blank">code plitting and dynamic imports</a>, <a href="https://blog.risingstack.com/node-js-http-2-push/" target="_blank">HTTP/2's multiplexing and push capabilities</a> and the new <a href="https://css-tricks.com/prefetching-preloading-prebrowsing/" target="_blank">prefetching link attributes</a> - to name a few.</p>
<p>Ultimately it's not only about the size of the code, but the quality too. Improve your apps performance with the <a href="https://reactjs.org/docs/optimizing-performance.html" target="_blank">official React.js optimization tips</a>. It's a pretty good list.</p>
<h2 id="tip8lookunderthehood">Tip #8: Look under the hood</h2>
<p>Learning the concepts behind React.js is time well spent. Create a dummy project <a href="https://reactjs.org/docs/react-without-jsx.html" target="_blank">without JSX</a> to get closer to the underlying vDOM. By deepening your understanding of the vDOM and <a href="https://reactjs.org/docs/reconciliation.html" target="_blank">reconciliation</a>, you can optimize your apps more efficiently.</p>
<p>Get familiar with the <a href="https://reactjs.org/docs/context.html" target="_blank">context API and all of its issues</a>. It gives a sneak peak into the context sharing of popular libraries - like MobX and Redux. Finally, grasping the broad overview of <a href="https://reactjs.org/blog/2017/09/26/react-v16.0.html#new-core-architecture" target="_blank">React.js Fiber</a> gives a sense of control.</p>
<h2 id="becomeconfidentwithreactjs">Become confident with React.js</h2>
<p>Would you like to know more about how building Modern Front-End Apps with React.js? We have good news for you!</p>
<p>We organize <a href="https://risingstack.com/trainings#modernfrontendwithreact" target="_blank">React.js training sessions</a><br />
throughout Europe in the upcoming months:</p>
<ul>
<li><a href="https://ti.to/risingstack/modern-front-end-with-react-berlin-2018" target="_blank">Berlin</a> (March 12 - March 13)</li>
<li><a href="https://ti.to/risingstack/modern-front-end-with-react-tel-aviv-2018" target="_blank">Tel-Aviv</a> (April 16 - April 17)</li>
<li><a href="https://ti.to/risingstack/modern-front-end-with-react-barcelona-2018" target="_blank">Barcelona</a> (May 17 - May 18)</li>
<li><a href="https://ti.to/risingstack/modern-front-end-with-react-warsaw-2018" target="_blank">Warsaw</a> (June 21 - June 22)</li>
</ul>
<p>Make sure to reserve your tickets online so we know we can count on you. See you there!</p>
<p>These trainings are perfect for you if you want to improve your front-end skills, build application prototypes rapidly, and create complex and maintainable websites. Take a look at the detailed agenda <a href="https://s3-eu-west-1.amazonaws.com/risingstack-resources/RisingStack+Public+Trainings/React+Training+RisingStack.pdf" target="_blank">here</a>.</p>
<p>In case you have any questions regarding this training, or you’d like to invite our team to provide a training exclusively for your company, please reach out to us at <a href="mailto:info@risingstack.com" target="_blank">info@risingstack.com</a>.</p>
<h2 id="whattipswouldyouadd">What tips would you add?</h2>
<p>These are just a handful of React.js tips and tricks, but I hope you found them useful. Keep these advices always in mind to optimize the performance of your React.js code. If you think that I missed something, please share it in the comments.</p>
<p><em>Thanks!</em></p>

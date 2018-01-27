<a href="https://levelup.gitconnected.com/a-recap-of-front-end-development-in-2017-7072ce99e727">https://levelup.gitconnected.com/a-recap-of-front-end-development-in-2017-7072ce99e727</a><div id="articleHeader"><h1>A recap of front-end development in 2017</h1></div><p id="3443">Front-end engineering once again evolved at a feverish pace in 2017. Here is a list of the most notable events of the past year.</p><figure id="7b41"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*aVzJTznRRfP1lM7AXe9yLw.jpeg?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/1*aVzJTznRRfP1lM7AXe9yLw.jpeg" /></div></figure><h3 id="971e">React 16 and the MIT license</h3><p id="44d2">React continues to dominate the front-end landscape, and 2017 provided one of the most anticipated releases yet with <a href="https://edgecoders.com/react-16-features-and-fiber-explanation-e779544bb1b7" target="_blank">version 16</a>. It includes the fiber architecture which enables asynchronous UI rendering. This release also makes it much easier to manage unexpected application failures by providing error boundaries along with <a href="https://edgecoders.com/react-16-features-and-fiber-explanation-e779544bb1b7" target="_blank">many other features</a>.</p><p id="d613">Surprisingly, the most important improvement to React this past year wasn’t the new features, but the change to its open source license. Facebook shed its BSD license that was causing companies to move away from React and adopted the <a href="https://code.facebook.com/posts/300798627056246/relicensing-react-jest-flow-and-immutable-js/" target="_blank">user-friendly MIT license</a>. In addition, Jest, Flow, Immutable.js, and GraphQL gained the MIT license as well.</p><p id="5f04">Core team and top contributors include <a href="https://medium.com/@trueadm" target="_blank">Dominic Gannaway</a>, <a href="https://medium.com/@dan_abramov" target="_blank">Dan Abramov</a>, <a href="https://medium.com/@sophiebits" target="_blank">Sophie Alpert</a>, <a href="https://medium.com/@sebmarkbage" target="_blank">Sebastian Markbåge</a>, <a href="https://medium.com/@zpao" target="_blank">Paul O’Shannessy</a>, <a href="https://medium.com/@acdlite" target="_blank">Andrew Clark</a>, <a href="https://medium.com/@chenglou" target="_blank">Cheng Lou</a>, Clement Hoang, Probably Flarnie, Brian Vaughn, .</p><h3 id="c0fc">Progressive Web Apps</h3><p id="f12e">We’ve long been searching for the solution to bridge the gap between web and other clients. Google has been spearheading the movement to enhance web applications by converting them to progressive web apps (PWA’s), and 2017 has seen a rapid adoption. A PWA utilizes modern browser technologies to provide a web experience that is more like mobile applications. This offers improved performance and offline experience as well as features previously only available to mobile, such as push notifications. The backbone for PWA’s are a combination of a <code>manifest.json</code> file and utilizing <a href="https://developers.google.com/web/fundamentals/primers/service-workers/" target="_blank">service workers</a>.</p><figure id="2c02"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Fi.ytimg.com%2Fvi%2Fm-sCdS0sQO8%2Fhqdefault.jpg&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div><figcaption>Progressive Web Apps: Great Experiences Everywhere (Google I/O ‘17)</figcaption></figure><h3 id="4a02">Yarn’s adoption improves the JS package ecosystem</h3><p id="145e">NPM has grown up quite a bit since its initial release, but it was still missing some crucial features, which Yarn looked to add. Yarn’s key contributions are package caching, a lock file to ensure deterministic builds, parallelizing operations, and flattening dependencies. These features were so successful that NPM implemented them in the version 5.0 release. Yarn has over 1 billion downloads (currently 1.25 million downloads per month) and boasts a staggering <a href="https://github.com/yarnpkg/yarn" target="_blank">28,000+ GitHub stars</a>. Even if you aren’t using Yarn, JavaScript package management as a whole has improved significantly thanks to its release.</p><h3 id="a323">CSS Grid Layout</h3><p id="6fd5">Grids are finally native to CSS, and browsers are adopting it quickly. In the past, grid systems have been created in CSS using tables, <code>float</code>, <code>flex</code>, and <code>inline-block</code>. The native CSS Grid Layout excels at dividing a page into major regions and creating columns and rows for content. Check out <a href="https://gridbyexample.com/" target="_blank">https://gridbyexample.com/</a> by <a href="https://medium.com/@rachelandrew" target="_blank">Rachel Andrew</a> to start learning.</p><h3 id="c5d9">WebAssembly supported in all major browsers</h3><p id="e44d"><a href="http://webassembly.org/" target="_blank">WebAssembly</a> (or <em>wasm</em>) is now shipping in all major browsers. wasm is a low-level <a href="https://en.wikipedia.org/wiki/Bytecode" title="Bytecode" target="_blank">bytecode</a> format for in-browser client-side scripting. Since it is low-level, it boasts incredible performance but also offers a <a href="http://webassembly.org/docs/js/" target="_blank">JavaScript API</a> providing front end developers an easier entry point. <a href="https://medium.com/@firefox" target="_blank">Firefox</a> recently announced the inclusion in all browsers.</p><h3 id="a4f7">Serverless architectures</h3><p id="c57f">The popularity for serverless applications grew at a feverish pace in 2017. They offer a way to increase performance at a reduced cost. Your client is fully decoupled from the server, allowing you to focus on your application and not your infrastructure. A common implementation is to use an AWS API Gateway combined with an AWS Lambda function as a BaaS (backend as a service) to be consumed by your client. You can get started with this excellent introduction by <a href="https://medium.com/@adnanrahic" target="_blank">Adnan Rahić</a>.</p><h3 id="7912">Vue.js continuing to grow in popularity</h3><p id="edce">Even with all of React’s success, <a href="https://vuejs.org/" target="_blank">Vue</a> (created by <a href="https://medium.com/@youyuxi" target="_blank">Evan You</a>) continues to grow in popularity. The framework provides a component-based architecture and is one of the leading alternatives for React. It has seen adoption from larger companies including <a href="https://medium.com/@gitlab" target="_blank">GitLab</a> which <a href="https://about.gitlab.com/2017/11/09/gitlab-vue-one-year-later/" target="_blank">recaps their past year</a> using the framework.</p><figure id="8dbb"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*EauHdmiXdyc-nWQJI3Zw_g.png?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/1*EauHdmiXdyc-nWQJI3Zw_g.png" /></div></figure><h3 id="55d0">CSS-in-JS and preparing for the upcoming CSS Holy War</h3><p id="0e20">After the rapid evolution in JavaScript that we’ve witnessed, the ecosystem is starting to stabilize. It’s inevitable that we’ll also see the same relentless advancements in CSS as well, as it catches up to modern web application needs. In 2017, the primary advancement has been the stark improvements and adoption of CSS-in-JS, where all styles are built through code and not style sheets. It’s not yet clear if this will be the ultimate direction that the front end community lands on, but it’s the current bleeding edge method and appears to solve many of the problems found while building a component-based applications.</p><p id="4d9a">2017 has seen <a href="https://www.styled-components.com/" target="_blank"><strong>styled-components</strong></a> (by <a href="https://medium.com/@mxstbr" target="_blank">Max Stoiber</a>, <a href="https://medium.com/@glenmaddern" target="_blank">Glen Maddern</a>, <a href="https://medium.com/@philpl" target="_blank">Phil Plückthun</a>) take the lead in terms of popularity. <a href="https://github.com/emotion-js/emotion" target="_blank"><strong>Emotion</strong></a> (by <a href="https://medium.com/@tkh44" target="_blank">Kye Hohenberger</a>) is one of the newest libraries available, but it has seen rapid adoption. Another option to consider is <a href="https://glamorous.rocks/" target="_blank"><strong>glamorous</strong></a> (by PayPal, <a href="https://medium.com/@kentcdodds" target="_blank">Kent C. Dodds</a>, and a lot of passionate <a href="https://github.com/paypal/glamorous/blob/master/README.md#contributors" target="_blank">contributors</a>) which wraps the <a href="https://github.com/threepointone/glamor" target="_blank"><strong>glamor</strong></a> library. Check out <a href="https://alligator.io/react/css-in-js-roundup-styling-react-components/" target="_blank">this article</a> out for a summary of many of the available CSS-in-JS options.</p><h3 id="b9be"><strong>Static site generation</strong></h3><p id="703f">2017 saw a time warp with static website making a comeback. Frameworks such as <a href="https://www.gatsbyjs.org/" target="_blank">Gatsby</a> empower you to build static websites using React and other modern tools. Not every website needs to be or should be a complicated modern web application. Static site generation offers you the benefits of server side rendering and unmatched speed since you’re serving prebuilt markup. If you’re looking for a good example, the <a href="https://reactjs.org/" target="_blank">official React docs</a> themselves have been built using Gatsby.</p><p id="2a6e">Static site generation has sparked another trend known as the <a href="https://jamstack.org/" target="_blank">JAMStack</a>: “JavaScript, APIs, Markup”. The JAMStack uses the same static prebuilt HTML files along with reusable APIs and JavaScript to handle any dynamic programming during the request/response cycle. <a href="https://medium.com/@Netlify" target="_blank">Netlify</a> is a great option for getting started with the JAMStack and static hosting for free. <a href="https://medium.com/@bddougie" target="_blank">Brian Douglas</a> wrote an excellent article <a href="https://www.netlify.com/blog/2017/06/06/jamstack-vs-isomorphic-server-side-rendering/" target="_blank">comparing the JAMStack vs. server side rendered apps</a> by building Hacker News clones.</p><h3 id="113c">GraphQL explodes and makes us rethink API construction</h3><p id="0828">GraphQL appears to rapidly be gaining ground on REST, and <a href="https://medium.com/@samerbuna" target="_blank">Samer Buna</a> even claims that <a href="https://medium.freecodecamp.org/rest-apis-are-rest-in-peace-apis-long-live-graphql-d412e559d8e4" target="_blank">REST is already dead</a>. Instead of managing multiple endpoints and fetching unnecessary data, GraphQL allows the client to declaratively define the data that it needs and retrieve it all from a single endpoint.</p><p id="c4c1">It is becoming so prevalent that <a href="https://medium.com/@github" target="_blank">GitHub</a> has written the <a href="https://developer.github.com/v4/" target="_blank">newest version of its API</a> in GraphQL, and many companies are creating products to make it accessible to all developers such as the popular <a href="https://medium.com/@graphcool" target="_blank">Graphcool</a> framework by <a href="https://medium.com/@schickling" target="_blank">Johannes Schickling</a>.</p><h3 id="ec4c">React Router 4</h3><p id="df68">React Router by <a href="https://medium.com/@ryanflorence" target="_blank">Ryan Florence</a> and <a href="https://medium.com/@mjackson" target="_blank">Michael Jackson</a> evolved from just being a router for React to truly becoming React Router — a declarative router enabled by simply using React components. It is the first version endorsed by the React team. The API has stabilized, and the <a href="https://medium.com/@ReactTraining" target="_blank">React Training</a> team has stated that it will not see any large breaking changes for the lifetime of the project.</p><figure id="a973"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Fpbs.twimg.com%2Fprofile_images%2F864681873984835585%2F4eV1BACS_400x400.jpg&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></figure><h3 id="de5c">Angular released v4 quickly followed by v5</h3><p id="7e09">After infamously skipping version 3 to maintain SEMVER, Angular 4 officially shipped on March 23rd. In version 4 the Angular team adopted the community project Angular Universal — which provides a method for server-side rendering Angular apps — as an official part of the Angular project. The Angular Animation package was also extracted from <code>@angular/core</code> for importing only when needed, and Ahead Of Time compilation within the View Engine has been refactored for performance, “reduc[ing] the size of the generated code for your components by around 60% in most cases.”</p><p id="1dce">Version 5 saw the adoption of additional long-awaited improvements. Creating a Progressive Web App with Angular v5 is now much easier than any earlier version thanks to the new <code>@angular/service-worker</code> package. The Angular compiler was also improved, enabling faster builds/rebuilds during development, and the Angular Router now exposes all new lifecycle hooks, including ActivationStart, ActivationEnd, ResolveStart, and ResolveEnd.</p><h3 id="d682">TypeScript and Flow</h3><p id="c802"><a href="https://www.typescriptlang.org/" target="_blank">TypeScript</a> has gained a cult following among many JavaScript developers while <a href="https://flow.org/" target="_blank">Flow</a> offers a more nimble way to introduce types without aggressive refactoring. The lack of types in JavaScript has been a complaint of many. TypeScript was created by Microsoft and is a requirement in the new version of Angular. Flow is the brainchild of Facebook.</p><h3 id="4f0b">gitconnected creates the community for developers</h3><p id="564b">gitconnected launched creating the community for developers and software engineers. It offers the ability to collaborate, share articles, and create discussions with other developers. In addition, you can seamlessly display you projects and portfolios on your personalized profile page. Don’t miss the opportunity to connect with others that share you interests and help each other to learn and grow.</p><h3 id="7aa2">What to expect in 2018</h3><ul><li id="63d1">The CSS battle rages as we figure out the best way to handle styles in component-based applications.</li><li id="8734">More companies adopt mobile solutions that have a unified codebase such as <a href="https://facebook.github.io/react-native/" target="_blank">React Native</a> or <a href="https://flutter.io/" target="_blank">Flutter</a>.</li><li id="fbfa">The web becomes more native with offline capabilities and seamless mobile experiences.</li><li id="e0f6">WebAssembly could make great strides, offering a better web experience.</li><li id="5fc6">GraphQL continues to challenge REST.</li><li id="9c11">React strengthens its position (yes, even more) now that there is no fear over the license.</li><li id="36dc">Flow and TypeScript take a stronger hold, giving JavaScript more structure.</li><li id="0640">The influence of containerization becomes more prevalent for front end architecture.</li><li id="76e1">Virtual reality makes strides forward using libraries like <a href="https://aframe.io/" target="_blank">A-Frame</a>, <a href="https://facebook.github.io/react-vr/" target="_blank">React VR</a>, and <a href="https://developers.google.com/vr/?hl=en" target="_blank">Google VR</a>.</li><li id="48e3">People build some really cool applications using the blockchain and <a href="https://github.com/ethereum/web3.js/" target="_blank">web3.js</a> (authored by <a href="https://medium.com/@marekkotewicz" target="_blank">Marek Kotewicz</a> and <a href="https://medium.com/@frozeman" target="_blank">Fabian Vogelsteller</a>).</li></ul><p id="56a1">If I missed anything big, leave a comment and I’ll be sure to add it!</p>
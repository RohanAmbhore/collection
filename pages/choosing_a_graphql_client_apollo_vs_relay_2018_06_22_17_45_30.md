<a href="https://www.codazen.com/choosing-graphql-client-apollo-vs-relay/">https://www.codazen.com/choosing-graphql-client-apollo-vs-relay/</a><div id="articleHeader"><h1>Choosing a GraphQL Client: Apollo vs. Relay</h1></div>
						<div>
							<div>
								
								September 8, 2016
							</div>
							<div>
								
																	Rachel Lee
															</div>
							<div>
								
								<a href="https://www.codazen.com/choosing-graphql-client-apollo-vs-relay/#comments" target="_blank">8 Comments</a>							</div>
						
						
							
	
		
			<p><a href="//www.codazen.com/wp-content/uploads/2016/09/GraphQL-Blog-Image.jpg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="//www.codazen.com/wp-content/uploads/2016/09/GraphQL-Blog-Image.jpg"   alt="Apollo vs. Relay" /></div></a></p>
<p>If you just want to see the comparison table, keep scrolling down. You won’t hurt anyone’s feelings. <em>Probably.</em></p>
<p>You’re likely here because you’ve heard about GraphQL, the groundbreaking new way to fetch data for your applications. Maybe you’ve figured out how to set up a basic GraphQL server. (If not, <a href="https://medium.com/apollo-stack/the-concepts-of-graphql-bc68bd819be3#.22a4zp5sd" target="_blank">check</a> <a href="https://medium.com/apollo-stack/how-do-i-graphql-2fcabfc94a01#.cekw8rmwb" target="_blank">out</a> <a href="https://medium.com/apollo-stack/graphql-explained-5844742f195e#.x0zixkf7o" target="_blank">these</a> <a href="https://medium.com/apollo-stack/tutorial-building-a-graphql-server-cddaa023c035#.7mopo6abm" target="_blank">great</a> <a href="https://www.compose.com/articles/using-graphql-with-mongodb/" target="_blank">articles</a>.) Now, you’ve got to pick a client that takes advantage of your shiny new GraphQL server. You’ve probably heard of Relay and tried a <a href="https://medium.com/@clayallsopp/relay-101-building-a-hacker-news-client-bb8b2bdc76e6#.zgmzyanu1" target="_blank">tutorial</a>. Maybe you found it confusing or difficult and didn’t realize you have other options. Well, Apollo and Relay are currently* two of the leading open-source GraphQL clients for NodeJS apps.</p>
<h6>If only there was a quick and easy side-by-side comparison so you could make an easily informed decision on which client is right for you. Well, congratulations, you found one!</h6>
<h3><strong>Why choose a GraphQL client?</strong></h3>
<p>Of course, before making such an important decision, we should discuss why we even need a GraphQL-specific client. Why can’t you just stick with whatever you’ve comfortably been using? Redux, for one, happens to work fine with GraphQL. If you’d like to spend more time simply figuring out how GraphQL works within a more familiar context like Redux, I highly recommend <a href="https://medium.com/@thisbejim/getting-started-with-redux-and-graphql-8384b3b25c56#.3ihvkvja4" target="_blank">James Childs-Maidment’s fantastic article on Getting started with Redux and GraphQL.</a></p>
<p>However, Redux isn’t designed to maximize the benefits of GraphQL. If your goal in learning GraphQL is to really take advantage of its amazing benefits, it makes sense to also invest in a client-side technology that aims to get the most out of your GraphQL server. To this end,</p>
<h6>Apollo and Relay both implement query and data caching in some form to further optimize requests to the GraphQL server.</h6>
<p>This means doing lots of pre/post-processing to make “smart” requests, which Redux isn’t built to do for you. Apollo and Relay also do lots of other nice things. Instead of reading an entire compare/contrast essay about said things, here’s a neat table below.</p>
<h3><strong>Comparison</strong></h3>
<p><a href="http://dev.apollodata.com/core/" target="_blank">Apollo</a> and <a href="https://facebook.github.io/relay/" target="_blank">Relay</a> share many features, but they’re <em>clearly not identical</em>. So, here’s a breakdown of how they’re different. In order to keep this brief, I’ve included links to what I believe are good resources for more information.</p>
<div id="tablepress-1-scroll-wrapper">

<div id="tablepress-1_wrapper"><table id="tablepress-1">
<thead>
<tr><th colspan="1" rowspan="1">Feature</th><th colspan="1" rowspan="1">Apollo</th><th colspan="1" rowspan="1">Relay</th></tr>
</thead>
<tbody>



















<tr>
	<td><em>Key Values</em></td><td><ul><li>Incrementally adoptable</li><li>Simple to get started with</li><li>Inspectable and understandable</li><li>Built for interactive apps</li><li>Community driven</li></ul></td><td><ul><li>Declarative: <em>what</em> data, don't worry about <em>how</em> or <em>when</em></li><li>Colocations: write data dependencies right in the view</li><li>Mutations: data consistency, optimistic updates, and error handling</li></ul></td>
</tr><tr>
	<td><em>Object Identification for Caching</em></td><td>__typename + id <br />
<em>(client-side, automatic)</em></td><td><a href="https://www.npmjs.com/package/graphql-relay" target="_blank"><code>graphql-relay</code></a> globalId <br />
<em>(server-side, requires <a href="https://facebook.github.io/relay/docs/graphql-object-identification.html" target="_blank">GraphQL schema configuration</a>)</em></td>
</tr><tr>
	<td><em>Query Language</em></td><td><code><a href="https://www.npmjs.com/package/graphql-tag" target="_blank">graphql-tag</a></code></td><td><a href="https://facebook.github.io/relay/docs/api-reference-relay-ql.html" target="_blank">Relay.QL</a></td>
</tr><tr>
	<td><em>Query Batching</em></td><td><a href="https://medium.com/apollo-stack/query-batching-in-apollo-63acfd859862" target="_blank">built-in</a> <em>(one-line setup + config)</em></td><td><a href="https://www.npmjs.com/package/react-relay-network-layer" target="_blank"><code>react-relay-network-layer</code></a></td>
</tr><tr>
	<td><em>Subscriptions</em></td><td><a href="https://medium.com/apollo-stack/graphql-subscriptions-in-apollo-client-9a2457f015fb" target="_blank">yes</a></td><td><a href="https://www.npmjs.com/search?q=graphql+relay+subscription" target="_blank">yes<em>(ish)</em></a></td>
</tr><tr>
	<td><em>Fragments</em></td><td><a href="http://dev.apollodata.com/core/fragments.html" target="_blank">yes</a></td><td>yes</td>
</tr><tr>
	<td><em>Optimistic UI Updates</em></td><td><a href="https://medium.com/apollo-stack/mutations-and-optimistic-ui-in-apollo-client-517eacee8fb0#.wwud7jpr0" target="_blank">yes</a></td><td><a href="http://blog.pathgather.com/blog/a-beginners-guide-to-relay-mutations" target="_blank">yes</a></td>
</tr><tr>
	<td><em>Pagination</em></td><td>Arbitrary <a href="https://medium.com/apollo-stack/pagination-and-infinite-scrolling-in-apollo-client-59ff064aac61#.t1suezbso" target="_blank">pagination</a> schema <em>(server-side)</em>, <a href="http://dev.apollodata.com/react/pagination.html" target="_blank">fetchMore</a> <em>(client-side)</em></td><td>cursor-based <em>(server-side, requires <a href="https://facebook.github.io/relay/docs/graphql-connections.html" target="_blank">GraphQL connections configuration</a>)</em></td>
</tr><tr>
	<td><em>Custom Network Interfaces</em></td><td><a href="http://dev.apollodata.com/core/network.html" target="_blank">yes</a></td><td><a href="https://facebook.github.io/relay/docs/guides-network-layer.html" target="_blank">yes</a></td>
</tr><tr>
	<td><em>Server-Side rendering</em></td><td><a href="http://dev.apollodata.com/react/server-side-rendering.html" target="_blank">yes</a></td><td><a href="https://www.npmjs.com/package/isomorphic-relay" target="_blank"><code>isomorphic-relay</code></a></td>
</tr><tr>
	<td><em>Performance (Caching and Query Optimization</em></td><td><a href="http://dev.apollodata.com/react/receiving-updates.html" target="_blank">yes</a></td><td><a href="https://facebook.github.io/relay/docs/thinking-in-graphql.html" target="_blank">yes</a></td>
</tr><tr>
	<td><em>Routing</em></td><td><code><a href="https://www.npmjs.com/package/react-router" target="_blank">react-router</a></code></td><td><a href="https://www.npmjs.com/package/react-router-relay" target="_blank"><code>react-router-relay</code></a></td>
</tr><tr>
	<td><em>Testing</em></td><td><a href="https://facebook.github.io/jest/" target="_blank">Jest</a> (assuming you're using React)</td><td><a href="https://facebook.github.io/jest/" target="_blank">Jest</a></td>
</tr><tr>
	<td><em>Developer Tools</em></td><td><a href="http://dev.apollodata.com/core/devtools.html" target="_blank">Redux DevTools</a> (<a href="https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd" target="_blank"><em>chrome extension</em></a>)</td><td>React DevTools <em>(<a href="https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi" target="_blank">chrome extension</a>)</em></td>
</tr><tr>
	<td><em>Compatibility</em></td><td>React, React Native, Angular 2, Redux, Meteor</td><td>React, React Native</td>
</tr><tr>
	<td><em>Learning Curve (Familiarity)</em></td><td><a href="http://dev.apollodata.com/react/initialization.html" target="_blank">similar to <code>react-redux</code></a></td><td>new material</td>
</tr><tr>
	<td><em>Mutation-Writing Complexity</em></td><td><ul><li>Simple GraphQL mutation w/resolve</li><li>Send literal mutation through Apollo client</li><li>Update Apollo client store</li></ul></td><td><ul><li>GraphQL mutation w/mutationWithClientMutationId</li><li>Match variable names between GraphQL and Relay</li><li>Set up fat query & configs for Relay</li></ul></td>
</tr><tr>
	<td><em>Documentation</em></td><td><a href="http://dev.apollodata.com/core/" target="_blank">fantastic</a> (with <a href="http://dev.apollodata.com/core/how-it-works.html" target="_blank">pictures</a>!)</td><td><a href="https://facebook.github.io/relay/docs/getting-started.html" target="_blank">...spotty</a></td>
</tr><tr>
	<td><em>Open Source Stats (as of 9/1/2016)</em></td><td><a href="https://github.com/apollostack/apollo-client" target="_blank">https://github.com/apollostack/apollo-client</a><ul><li>Watchers: 87</li><li>Stars: 815</li><li>Forks: 61</li><li>Open Issues: 81</li><li>Pending PRs: 9</li><li>Commits in last month: 176</li></ul></td><td><a href="https://github.com/facebook/relay" target="_blank">https://github.com/facebook/relay</a><ul><li>Watchers: 339</li><li>Stars: 6,940</li><li>Forks: 576</li><li>Open Issues: 123</li><li>Pending PRs: 10</li><li>Commits in the last month: 10</li></ul></td>
</tr></tbody>
</table></div>

</div>
<h3><strong>Coda</strong></h3>
<p>Ultimately, it comes down to you and the specifics of your project. Apollo offers a friendly developer experience and works great for learning and adopting GraphQL into an existing project, especially if it doesn’t use React. Relay is being built with mobile performance and scalability–at the Facebook level–in mind.</p>
<h6>As GraphQL continues to mature, both technologies have great communities dedicated to creating a better internet, so you can’t really go wrong with either one.</h6>
<p>My team decided to go with Relay. Why? The Relay team at Facebook is hard at work on some major improvements, and <a href="https://facebook.github.io/react/blog/2016/08/05/relay-state-of-the-state.html" target="_blank">the future of Relay</a> looks pretty bright. Also, because Relay and GraphQL are both developed at Facebook, we expect any updates for GraphQL will be supported faster by Relay 2 than Apollo.</p>
<p>Make your choice: <a href="https://medium.com/apollo-stack/apollo-client-graphql-with-react-and-redux-49b35d0f2641#.6o2t5khlj" target="_blank">Get started with Apollo</a> or <a href="https://facebook.github.io/relay/docs/tutorial.html#content" target="_blank">Get started with Relay</a></p>
<p>If you were hoping for more words to read, check out some of the many links throughout this post. They’re dedicated to more specific topics about GraphQL, Apollo, and Relay. Also, keep an eye out for a follow-up article exploring key changes between Relay and Relay 2!</p>
<p>Posted by Rachel Lee, <em>Software Engineer</em></p>

		
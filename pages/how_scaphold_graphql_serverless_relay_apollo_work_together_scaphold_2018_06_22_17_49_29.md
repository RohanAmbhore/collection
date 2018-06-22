<a href="https://scaphold.io/community/blog/scaphold-graphql-serverless-relay-apollo/">https://scaphold.io/community/blog/scaphold-graphql-serverless-relay-apollo/</a><div id="articleHeader"><h1>How Scaphold, GraphQL, Serverless, Relay, & Apollo Work Together</h1></div><div><h3>A detailed breakdown of where GraphQL starts and Scaphold ends from a frontend perspective.</h3></div><p>by Vince Ning</p><div><div><h1>How Scaphold, GraphQL, Serverless, Relay, & Apollo Work Together</h1>
<p>As a GraphQL service provider, we get asked the question of how Scaphold is different from a traditional GraphQL server. In short, it’s not very different. We expose you GraphQL in a vanilla way without inserting any tricks up our sleeves, while layering value-added features on top of it to help you in your app development process.</p>
<h2>Architecture</h2>
<p><div class="readableLargeImageContainer"><img src="https://assets.scaphold.io/community/blog/scaphold-graphql-serverless-relay-apollo/scaphold-graphql-serverless-apollo-relay.png" alt="Architecture Comparison" /></div></p>
<p>From the server side to the client side, there are many tools needed to build an end-to-end application. In the following sections, we’ll go into each part of the application stack and how it fits into the larger development process.</p>
<h2>GraphQL Server</h2>
<img src="https://assets.scaphold.io/community/blog/scaphold-graphql-serverless-relay-apollo/graphql.png" />
<p>Let’s start with GraphQL. What’s in the box?</p>
<h4>GraphQL Schema</h4>
<p>One of the main principles of GraphQL development is GraphQL-first and the importance of setting up your GraphQL schema first. The schema is the single source of truth for how your data is structured in your app. It’s the backbone for your API.</p>
<h4>GraphQL Language</h4>
<p>GraphQL provides a powerful declarative query language that the server understands and uses to fetch data with.
On the server side, you get a clean framework that parses GraphQL queries and routes them to event handlers.</p>
<p>In these resolvers, you’ll need to fetch data to be returned to the client that made the request. The beauty of GraphQL is that it’s data source agnostic. And as a GraphQL developer, your job is to figure out the logic needed to fetch the required data whether it be from your data store(s) or even other REST APIs.</p>
<p>In essence, GraphQL is a thin layer that composes the core of your app’s API. Architectural pieces in your app that
remain to be handled are authentication, permissioning, and the logic behind each resolver to fetch the appropriate
data.</p>
<h2>Serverless</h2>
<img src="https://assets.scaphold.io/community/blog/scaphold-graphql-serverless-relay-apollo/lambda.png" />
<p>Microservices are becoming more and more popular as a way of building apps. You can use serverless providers like
Amazon Lambda, Azure Functions, or Auth0 Webtask in order to set up and manage your microservices. You can gain
massive efficiencies this way since these services only run as often as they’re called.</p>
<p>In your services, you can include your app’s custom logic to be able to fetch the data you need, transform data in your requests, and more.</p>
<p>Managing these microservices is tough though, particularly at scale, since you’ll eventually have to wrangle hundreds if not thousands of microservices functions across multiple teams.</p>
<h2>Scaphold Server (i.e. GraphQL Server++)</h2>
<img src="https://assets.scaphold.io/community/blog/scaphold-graphql-serverless-relay-apollo/scaphold.png" />
<p>After understanding the scope of GraphQL, here’s the surface area of Scaphold. We provide elements of an implemented GraphQL server and layer on top features that any app running in production would need. Scaphold provides everything from hosting and managing your API layer, data layer, auth mechanisms, and logic functions, so you don’t have to manage all of those infrastructural pieces yourself.</p>
<p>Here’s some highlighted features just to name a few:</p>
<ul>
<li>Authentication</li>
<li>Aggregations</li>
<li>Permissioning</li>
<li>Analytics</li>
<li>Relay-spec compliant API</li>
<li>Visual schema designer</li>
<li>Integrations (i.e. Auth0, push notifications, etc.)</li>
<li>Protoyping tools</li>
<li>Persisted queries</li>
<li>File management</li>
<li>Microservice management (via webhooks)</li>
</ul>
<p>With Scaphold, you won’t have to manage any of the above yourself anymore with manually-written code. You have a GUI web interface that you can use to manage your GraphQL API, as well as the nitty-gritty features above that you get for free by using Scaphold.</p>
<p>Here’s what Scaphold looks like as you’re developing your application to configure your API.</p>
<p><div class="readableLargeImageContainer"><img src="https://assets.scaphold.io/community/blog/scaphold-graphql-serverless-relay-apollo/scaphold-dashboard.png" alt="Scaphold Dashboard" /></div></p>
<h2>Frontend caching</h2>
<p>Now, how do you interact with this server from my client in an efficient way? Well, there are frontend network layers that can help you.</p>
<h4>Relay</h4>
<img src="https://assets.scaphold.io/community/blog/scaphold-graphql-serverless-relay-apollo/relay.png" />
<p>Relay is Facebook’s frontend client that works with React. It works strictly with Relay-compliant GraphQL APIs, hence the name. And Facebook recently released Relay Modern as a way to combat many of the problems that Relay Classic had, particularly in allowing for a simpler GraphQL mutation API.</p>
<p>This is what Facebook uses internally, and you can check out how you can use it <a href="https://facebook.github.io/relay/" target="_blank">here</a>.</p>
<h4>Apollo</h4>
<img src="https://assets.scaphold.io/community/blog/scaphold-graphql-serverless-relay-apollo/apollo.png" />
<p>This frontend client was released by Meteor Development Group as part of the Apollo Stack and has a powerful frontend caching library. They have support for most popular frontend frameworks, like React, Angular, Vue, iOS, and Android. It has powerful frontend caching capabilities along with convenience methods to allow to you easily
access the frontend store.</p>
<p>Large companies like Shopify and Coursera already use Apollo Client in their stack, and you can read more about it <a href="https://github.com/apollographql/apollo-client" target="_blank">here</a>.</p>
<h2>Conclusion</h2>
<p>Revisiting the full stack app development architecture using Scaphold, you can now understand how much value Scaphold brings to your software development process. You can save time on infrastructure management, allowing you to focus more on perfecting the frontend for your application to make your users happy.</p>
<p>Scaphold abstracts away the data management, custom logic management, and provides you a painless way to manage the rest of your system. Meanwhile, you can still build your client app the way that you want.</p>
<p><div class="readableLargeImageContainer"><img src="https://assets.scaphold.io/community/blog/scaphold-graphql-serverless-relay-apollo/scaphold-graphql-serverless-apollo-relay.png" alt="Architecture Comparison" /></div></p>
<p>After analyzing the Scaphold stack, now you can see how many more features Scaphold adds to the base GraphQL library, not to mention the scalability issues that it addresses.</p>
<p>Thanks for reading!</p>
<p>If you enjoyed reading this post, please <a href="http://slack.scaphold.io" target="_blank">join us on Slack</a> or <a href="https://docs.scaphold.io" target="_blank">check out our docs</a>!</p>

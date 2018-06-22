<a href="https://www.prisma.io/blog/relay-vs-apollo-comparing-graphql-clients-for-react-apps-b40af58c1534/">https://www.prisma.io/blog/relay-vs-apollo-comparing-graphql-clients-for-react-apps-b40af58c1534/</a><div id="articleHeader"><h1>An un-opinionated comparison of GraphQL clients for React apps</h1></div>
<p><a href="https://facebook.github.io/relay/" target="_blank">Relay</a> and <a href="http://dev.apollodata.com/" target="_blank">Apollo</a> are the most popular and sophisticated GraphQL clients available at the moment. But how do you know which one to choose?</p>
<p>In this article, we’ll cover the following:</p>

<blockquote>
<p><strong>Note</strong>: This article only applies to <strong>Relay Classic</strong>, we’ll update it for Relay Modern soon. Stay tuned!</p>
</blockquote>
<p>In this article, we are going to shed some light on the commonalities and differences between Relay and Apollo and want to help you in making an informed decision on which GraphQL client is the best for your next project!</p>
<blockquote>
<p>This article assumes some familiarity with basic GraphQL concepts such as queries, mutations or fragments. If you’re just getting started with GraphQL, the <a href="https://www.howtographql.com" target="_blank">How to GraphQL</a> fullstack tutorial website is a great entry point!</p>
</blockquote>
<p>At Prisma, we have been using Relay and Apollo extensively over the last years and now want to share our learnings with the community. Also note that while Apollo can also be used with other frameworks, this article primarily targets React developers and specifically compares Relay and Apollo in the context of React applications.</p>
<h3>Why a GraphQL client?</h3>
<p>GraphQL backends commonly expose their API over HTTP where queries and mutations can be sent in the <em>body</em> of a POST request. When building a JavaScript app, this means that you can get quite far by using fetch or request and thus interact with the GraphQL API directly.</p>
<p>However, there are a number of recurring challenges and use cases in working with a GraphQL backend that are agnostic to the app that’s being built and that would have to be reimplemented with every new project. A few examples are:</p>
<ul>
<li>caching data that is returned by the server</li>
<li>UI framework integration (React, Angular, Vue, …)</li>
<li>keeping the local cache consistent after a mutation</li>
<li>managing up websockets for GraphQL subscriptions enabling realtime updates</li>
<li>pagination for collections</li>
</ul>
<p>A GraphQL client should come with that kind of functionality so that you don’t have to reimplement these behaviours yourself. Instead, you can completely focus on your application domain and on implementing the specific requirements of your app.</p>
<h3>Overview</h3>
<p>In the following, we are going to explore how to solve common and recurring client-side tasks when working with a GraphQL API, both from a Relay and an Apollo perspective.</p>
<p>To give you a broad overview of both clients, here is a high-level comparison before we dive into more details.</p>
<p><div><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/2046/0*ADpwj3uhA98QTc9L." /></div></p>
<p>When reading about Relay and Apollo, you’ll notice that one major difference lies in the flexibility of the two approaches. While Relay is very opiniated and doesn’t give you a lot of freedom in how you want to structure your application, Apollo has a variety of options that range from lightweight integrations to much more sophisticated approaches.</p>
<p>In short, Relay lends itself well for large-scale applications that have complex data requirements and many dependencies between different parts of the application where maintaining these dependencies by hand would be very tedious and error-prone. Apollo on the other hand provides a much more lightweight and flexible approach that works in any environment. Many tasks such as keeping the local cache consistent can also be achieved with the Apollo Client but require more manual work and bookkeeping.</p>
<h4>An example to follow along</h4>
<p>In the following, we are going to compare Apollo and Relay by practical examples and show how each of them can be used to deal with a certain use case. We are going to use the data model for the Pokedex application that is being used on <a href="https://www.learnrelay.org/" target="_blank">Learn Relay</a> and <a href="https://www.learnapollo.com/" target="_blank">Learn Apollo</a>.</p>
<p>This is what the data model looks like:</p>
<div><pre>copy<code>type Pokemon {
  id: ID!
  name: String
  trainer: Trainer @relation(name: "OwnedPokemons")
  url: String
}

type Trainer {
  id: ID!
  name: String
  ownedPokemons: [Pokemon!]! @relation(name: "OwnedPokemons")
}
</code></pre></div>
<h3>Server Requirements</h3>
<p>In contrast to Apollo Client that works with any GraphQL schema, Relay actually has a few requirements when it comes to the structure of the GraphQL schema that’s implemented on the server.</p>
<p>With Relay, the GraphQL server is expected to expose the following capabilities:</p>
<ul>
<li>
<p><em>The ability to query one particular resource (node) by its ID.</em> This is done with a root query field in the GraphQL schema called node that takes an ID as an argument: node(id: ID!). In Relay, every object is expected to have a unique ID which is why every type needs to implement the Node interface:</p>
<div><pre>copy<code>interface Node {
    id: ID!
}
</code></pre></div>
<p>The reason for this is that Relay can efficiently fetch a node by its ID after it was mutated and generally brings further performance benefits when working with the data graph.</p>
</li>
<li>
<p><em>The ability to query the data graph using a root field called <code>viewer</code> that contains all other fields as children.</em> The <code>viewer</code> is the root field that all other nodes are somehow connected to. While the availability of this field is not actually a hard requirement for Relay to work, it's conventional and you'll find it in almost all GraphQL APIs that work with Relay. You can read more about the rationale of the <code>viewer</code> field <a href="https://github.com/facebook/relay/issues/112" target="_blank">here</a>.</p>
</li>
<li>
<p><em>Mutation arguments must be wrapped in input type object.</em> Relay requires that every mutation receives its input arguments in the form of one single object. So, for a <code>createPokemon</code> mutation that expects a <code>name</code> and a <code>url</code>, this information needs to be provided as one object wrapping these two values.</p>
</li>
<li>
<p><em>Requirements for mutation payloads.</em> Relay has strong conventions for how mutations work and how updates to the local Relay store are performed. This requires that certain fields need to be included in the payload of a mutation — which fields exactly have to be included depends on the mutation kind.</p>
</li>
<li>
<p><em>Using connections for modelling relationships.</em> In Relay, the concept that is used to model a relationship between two types is called <a href="https://facebook.github.io/relay/docs/graphql-connections.html#content" target="_blank">Connection</a>. It requires that a relation in the data model is expressed using edges that each contain a node. If you wanted to access the first 100 Pokemons in the database, this would look as follows with Relay:</p>
<div><pre>copy<code>{
  viewer {
    allPokemons(first: 100) {
      edges {
        node {
          id
          name
        }
      }
    }
  }
}
</code></pre></div>
<p>In this case, the <code>viewer</code> has a <em>connection</em> to the <code>allPokemons</code> field. Also notice that a connection requires an indication of how many objects should be fetched, here this is done using the first parameter but more options such as last, after or beforeare available as well. This allows for easy slicing of the list and implement pagination easily. This <a href="https://dev-blog.apollodata.com/explaining-graphql-connections-c48b7c3d6976#.fd4h8iuj5" target="_blank">article</a> gives a lot of insights on the rationale behind the connection model and how it enhances pagination.</p>
</li>
</ul>
<h3>React Integration</h3>
<p>While Apollo can be used in <a href="http://dev.apollodata.com/" target="_blank">any client-side environment</a> (such as React, Angular, Vue or plain JS as well as on iOS and Android), Relay is restricted to be used with React or React Native.</p>
<p>However, they actually both follow a similar approach when being used in a React application: With both clients, the general idea is that React components are wrapped using a <a href="http://dev.apollodata.com/" target="_blank">higher-order component</a> which takes care of fetching the data and making it available to the component through its props. Data requirements for a component are specified in a declarative manner and all actual networking logic is completely abstracted away and hidden from the developer. A major benefit of this approach is that the container can manage data fetching and resolution logic without interfering with the state of the inner component.</p>
<h3>Queries</h3>
<p>A major responsibility of any GraphQL client is the ability to fetch data and make it available to the view layer of the app. In Relay, the major way of getting access to data inside of a React component is by means of a higher-order component called <a href="https://facebook.github.io/relay/docs/guides-containers.html#content" target="_blank">Relay.Container</a>.</p>
<p>With Apollo, it is possible to use a similar approach with the <a href="https://facebook.github.io/relay/docs/guides-containers.html#content" target="_blank">graphql</a> higher-order component. Another way to obtain data from the server would be to directly send queries using the <a href="http://dev.apollodata.com/core/apollo-client-api.html#apollo-client" target="_blank">ApolloClient</a> class and process the returned data with a promise. In the following, we are going to dive into what data fetching with Relay and with Apollo looks like.</p>
<p>In the next two sections, we are going to analyze the following query and how it would be incorporated using each Relay and Apollo:</p>
<div><pre>copy<code>query {
  allPokemons(filter: {
    trainer: {
      name: "Ash Ketchum"
    }
  }) {
    id
    name
    url
  }
}
</code></pre></div>
<h4>Data fetching with Relay</h4>
<p><strong>Co-located queries</strong></p>
<p>Relay heavily relies on GraphQL <em>fragments</em> to express data requirements for the React components. In fact, when working with Relay, we’re not actually writing full-blown GraphQL queries but only specify the data that is needed for each component in terms of a fragment. Relay then takes care of composing the fragments and building the actual GraphQL queries that are getting sent to the server. It hides all the details in this process so that the developer never has to deal with the nitty-gritty of network connections and HTTP requests.</p>
<p>As mentioned above, React components that need data from the server must be wrapped with a <code>Relay.Container</code>. This higher-order component does not directly take care of fetching the data but rather provides the wrapped component with the ability to define its data requirements and then guarantees that this data is available before the component is rendered.</p>
<p>Let’s take a look at some example code that creates and exports a <code>Relay.Container</code> which wants to display all Pokemons of the trainer called <code>"Ash Ketchum"</code> in a <code>Pokedex</code> component.</p>
<p>The <code>Pokedex</code> component renders a list of <code>PokemonPreview</code> components where each <code>PokemonPreview</code> presents information for one particular <code>Pokemon</code>.</p>
<div><pre>copy<code>// wrap Pokedex class with a RelayContainer and inject the data requirements via fragments
export default Relay.createContainer(
  // the wrapped component
  Pokedex,
  {
    // specify data requirements in terms of a fragment
    fragments: {
      viewer: () =&gt; Relay.QL`
        fragment on Viewer {
          allPokemons (
            filter: {
              trainer: {
                name: "Ash Ketchum"
              }
            },
            first: 1000
          ) {
            edges {
              node {
                id
                # include fields that appear in the `pokemon` fragment in `PokemonPreview`
                ${PokemonPreview.getFragment('pokemon')}
              }
            }
          }
          id
        }
      `,
    },
  },
)
</code></pre></div>
<p>In the wrapped React component, we have to specify props according to the defined fragments on the Relay container. In this case, we need to specify viewer that includes the <code>allPokemons</code> object.</p>
<div><pre>copy<code>// the Pokedex class is responsible to display multiple pokemons
class Pokedex extends React.Component {
  // require the viewer prop type
  static propTypes = {
    viewer: React.PropTypes.shape({
      allPokemons: React.PropTypes.object,
    }),
  }
​
  render () {
    return (
      &lt;div&gt;
        &lt;div&gt;
          // iterate the edges and nodes in the allPokemons connection
          {this.props.viewer.allPokemons.edges.map((edge) =&gt; edge.node).map((pokemon) =&gt;
            &lt;PokemonPreview key={pokemon.id} pokemon={pokemon} /&gt;)
          }
        &lt;/div&gt;
      &lt;/div&gt;
    )
  }
}
</code></pre></div>
<p>It’s important to note however that this approach still requires the <code>viewer</code> prop to be passed in to the Pokedex component through the component hierarchy - the mere fact that we have declared the <code>viewer</code> as a data requirement in a fragment does not yet guarantee its availability! It only serves to express what parts of the <code>viewer</code> are needed in that particular component. </p>
<p>When working with React and Relay, there are two separate <em>trees</em> being managed by these frameworks: The <em>component tree</em> that is managed by React and that will eventually represent the UI of the application as well as the <em>fragment tree</em> managed by Relay where the individual GraphQL fragments will be composed to queries that are sent over to the server.</p>
<p>Relay is heavily based on conventions. A major advantage of this approach is that following these conventions will enforce a very clean architecture and reduce subtle bugs that appear when changing certain parts of a system that had interdependencies with other parts.</p>
<p>Relay also optimizes for performance and tries to minimize the data transfer by only ever fetching data that is not yet available on the client. Facebook created GraphQL and Relay in the context of trying to improve the user experience of their applications in regions with very low connectivity, sending as little data as possible over the wire was one of the primary goals and still is a major part of the whole framework.</p>
<p><strong>Data normalization with nodes</strong></p>
<p>Relay requires the unique <code>id</code> field on every node in the GraphQL backend. This <code>id</code> is heavily used by Relay to <em>normalize</em> the data and make sure that all components rerender when there is new data for a certain node. No more configuration is needed to make the cache consistent from the client side - however, there is also no possibility to change this behaviour.</p>
<p>For example, for a GraphQL backend that only has unique IDs per type, Relay’s cache mechanisms would break. Graphcool uses <a href="https://github.com/graphcool/cuid-java" target="_blank">cuids</a> to generate unique IDs across all nodes in your project, so this is not an issue.</p>
<p>To read more about GraphQL queries in Relay, refer to the section in <a href="https://github.com/graphcool/cuid-java" target="_blank">Learn Relay</a>.</p>
<h4>Data fetching with Apollo</h4>
<p>With Apollo, it is possible to fetch data in two different ways:</p>
<ol>
<li>Wrapping the React component with the <code>graphql</code> higher-order component and make the data available through the props</li>
<li>Send a query directly using the <code>ApolloClient</code> class and handle the return data in a promise</li>
</ol>
<p><strong>1. Using graphql to wrap a React component</strong></p>
<p>When a React component requires some data, it can be wrapped with a query that expresses these data requirements and then the result of that will be available through the component’s props. Apollo further injects a <code>loading</code> and <code>error</code> property into the wrapped component. This allows the component to render in situations where the data has not yet arrived in the client (where loading will be <code>true</code>) or where the network request failed (so <code>error</code> will contain some info about what went wrong).</p>
<p>Taking the same scenario as above where the <code>Pokedex</code> component displays all Pokemons owned by the trainer called <code>"Ash Ketchum"</code>, the code to wrap the <code>Pokedex</code> component looks as follows:</p>
<div><pre>copy<code>const allPokemonsQuery = gql`
  query {
    allPokemons(filter: {
      trainer: {
        name: "Ash Ketchum"
      }
    }) {
      id
      name
      url
    }
  }
`

export default graphql(allPokemonsQuery)(Pokedex)
</code></pre></div>
<p>The response for the query as well as the <code>loading</code> and <code>error</code> properties are all part of an object called <code>data</code> in the props of the wrapped component. Note that it is possible to rename this object, but it's called <code>data</code> by default.</p>
<p>Consequently, in our scenario the implementation of the <code>Pokedex</code> component could be done like so:</p>
<div><pre>copy<code>// the Pokedex class is responsible to display multiple pokemons
class Pokedex extends React.Component {

// require the data prop type
  static propTypes = {
    data: React.PropTypes.shape({
      loading: React.PropTypes.bool,
      error: React.PropTypes.object,
      allPokemons: React.PropTypes.array,
    }).isRequired,
  }

render () {
    // data.loading informs about loading state - we can easily render a loading animation or a text
    if (this.props.data.loading) {
      return (&lt;div&gt;Loading&lt;/div&gt;)
    }

// in the case of an error with the query, data.error contains more information
    if (this.props.data.error) {
      console.log(this.props.data.error)
      return (&lt;div&gt;An unexpected error occurred&lt;/div&gt;)
    }

return (
      &lt;div className='w-100 bg-light-gray min-vh-100'&gt;
        &lt;div className='flex flex-wrap justify-center center w-75'&gt;
          {this.props.data.allPokemons.map((pokemon) =&gt;
            &lt;PokemonPreview key={pokemon.id} pokemon={pokemon} /&gt;
          )}
        &lt;/div&gt;
      &lt;/div&gt;
    )
  }
}
</code></pre></div>
<p><strong>2. Directly send queries using <code>ApolloClient</code></strong></p>
<p>The second option is to send a query using <code>ApolloClient</code> and processing the result as a promise. In that case, the <a href="http://dev.apollodata.com/core/apollo-client-api.html#ApolloClient.query" target="_blank"><code>query</code></a> method of the <code>ApolloClient</code> class can be used:</p>
<div><pre>copy<code>client.query({
  query: gql`
    {
    allPokemons(filter: {
      trainer: {
        name: "Ash Ketchum"
      }
    }) {
      id
      name
      url
    }
  }
  `
})
.then(result =&gt; console.log(result))
</code></pre></div>
<p>This approach leads to more flexibility if you require certain data for something other than displaying it in the UI.</p>
<p><strong>Controlling the Apollo Store</strong></p>
<p>Apollo uses a <a href="https://dev-blog.apollodata.com/building-a-graphql-store-from-first-principles-413e19ea65b4" target="_blank">normalized store</a> for its local cache. That means that the data that is being returned by the server (potentially) has a nested shape and will be flattened before being put into the store. All objects will be stored on the first level of the cache uniquely identified by their ID.</p>
<p>Let’s consider the following example query:</p>
<div><pre>copy<code>query {
  Trainer(name: "Ash Ketchum"){
    id
    name
    ownedPokemons {
      id
      name
    }
  }
}
</code></pre></div>
<p>And assume it returns the following JSON data:</p>
<div><pre>copy<code>{
  "data": {
    "Trainer": {
      "id": "ciwj0dw5dm6aj01632pto44t0",
      "name": "Nikolas",
      "ownedPokemons": [
        {
          "id": "ciwj0dw6zpeuj0148xvsgc3hr",
          "name": "Mewtwo"
        },
        {
          "id": "ciwj0dw8gm6c80163wh8zku78",
          "name": "Pikachu"
        }
      ]
    }
  }
}
</code></pre></div>
<p>Apollo would now <em>flatten</em> the nested Pokemons and put them on the first level of the store, so the contents of the store would look somewhat similar to this:</p>
<div><pre>copy<code>{
  "ciwj0dw5dm6aj01632pto44t0": {
    "id": "ciwj0dw5dm6aj01632pto44t0",
    "name": "Nikolas",
    "ownedPokemons": [ciwj0dw6zpeuj0148xvsgc3hr, ciwj0dw8gm6c80163wh8zku78]
  },
  "ciwj0dw6zpeuj0148xvsgc3hr": {
    "id": "ciwj0dw6zpeuj0148xvsgc3hr",
    "name": "Mewtwo"
  },
  "ciwj0dw8gm6c80163wh8zku78": {
    "id": "ciwj0dw8gm6c80163wh8zku78",
    "name": "Pikachu"
  }
}
</code></pre></div>
<p>In order for this approach to work, the Apollo store needs to be able to uniquely identify an object. It therefore provides the <code>dataIdFromObject</code> function that can be provided upon initialization of the <code>ApolloClient</code>. In this method, we can specify how an object can be uniquely identified. With Graphcool, this is done using the <code>id</code> property, so the implementation would look as follows:</p>
<div><pre>copy<code>const client = new ApolloClient({
  networkInterface: createNetworkInterface({ uri: 'https://api.graph.cool/simple/v1/__PROJECT_ID__' }),
  dataIdFromObject: o =&gt; o.id
})
</code></pre></div>
<p>With another GraphQL backend, your IDs might only be unique per type. In this case, you can use the following setup:</p>
<div><pre>copy<code>const client = new ApolloClient({
  networkInterface: createNetworkInterface({ uri: 'https://api.graph.cool/simple/v1/__PROJECT_ID__' }),
  dataIdFromObject: o =&gt; o.__typename + ' ' + o.id
})
</code></pre></div>
<p>In both cases, you have to make sure to include the <code>id</code> in all queries and mutations whose results should be normalized. To read more about GraphQL queries in Apollo Client, refer to the <a href="https://www.learnapollo.com/tutorial-react/react-02/" target="_blank">Learn Apollo</a>. There's also an <a href="https://www.learnapollo.com/excursions/excursion-02" target="_blank">excursion on the Apollo Store</a>.</p>
<h3>Mutations</h3>
<p>Sending mutations is a core feature of any GraphQL client allowing you to create, modify or delete data in a GraphQL backend.</p>
<p>While calling mutations in both Relay and Apollo is done with mutation strings where GraphQL variables are injected, the two clients handle cache consistency in combination with mutations in completely different manners. Mutations in Relay are extremely powerful and guarantee that the local store is always in a consistent state with the server. With Apollo on the other hand, achieving cache consistency requires a bit more manual work and potentially allows the developers to make mistakes which can lead to inconsistencies on the client-side.</p>
<p>We now want to explore how we can send the following GraphQL mutation with Relay and Apollo:</p>
<div><pre>copy<code>mutation {
  createPokemon(
    name: "Zapdos"
    types: [FLYING, ELECTRIC]
    url: "http://assets.pokemon.com/assets/cms2/img/pokedex/full/145.png"
  ) {
    id
    name
  }
}
</code></pre></div>
<h4>Mutations with Relay</h4>
<p>Mutations in Relay are very verbose and complex, this complexity however provides a lot of power and saves large amounts of work from the developer. When creating a mutation, we need to provide specific information that Relay uses behind the scenes to make sure all places in our app where the mutated data is used are getting updated properly.</p>
<p>It’s also important to note that the only way in Relay to change the state in the local store is by means of a mutation, there is no way to manually influence how the data in the store should be updated. After a mutation is sent, it is possible for the developer to specify what an opmistic UI update should look like, however, any changes that actually end up in the local store have to be confirmed by the server! If the interaction with the server fails, the optimistic UI updates are rolled back.</p>
<p>Generally, a mutation needs to be defined as a subclass of the <code>Relay.Mutation</code> class. After an instance of that class was created, there are two methods on the Relay object that can be used to actually send that mutation to the server:</p>
<ul>
<li><a href="https://facebook.github.io/relay/docs/api-reference-relay-store.html#commitupdate-static-method" target="_blank"><code>commitUpdate(mutation)</code></a> send the mutation right away</li>
<li><a href="https://facebook.github.io/relay/docs/api-reference-relay-store.html#applyupdate-static-method" target="_blank"><code>applyUpdate(mutation)</code></a> returns a <em>transaction</em> that can be sent later on by simply calling <code>commit()</code> on it</li>
</ul>
<p>When subclassing <code>Relay.Mutation</code>, the following methods must be implemented:</p>
<ul>
<li><code>getMutation()</code>: Specify the name of the mutation (from the GraphQL schema).</li>
<li><code>getFatQuery()</code>: Specify all nodes, edges and connections in our data graph that may change after this mutation.</li>
<li><code>getConfigs()</code>: Tell Relay what exactly happens with this mutation. The configuration <code>RANGE_ADD</code> needs a <code>parentName</code>, a <code>parentID</code> (that's what we need the <code>viewer</code> in the fragments for!), a <code>connectionName</code> and an <code>edgeName</code>. Additionally we need a list of <code>rangeBehaviors</code>, but typically <code>'': 'append'</code> is enough. The Relay <a href="https://facebook.github.io/relay/docs/guides-mutations.html" target="_blank">documentation</a> have listed the arguments that are required for each configuration.</li>
<li><code>getVariables()</code>: Specify the variables needed for this mutation.</li>
<li><code>getOptimisticResponse()</code> (optional): Specify optimistic data for the query response. It's only possible to return data specified in the fat query and <code>viewer</code>.</li>
</ul>
<p>We also need to provide the static property fragments:</p>
<ul>
<li><code>fragments</code>: Specify the data needed by this mutation that is already a part of our data graph, this is similar to specifying data requirements in a <code>Relay.Container</code>. In our case, we need the <code>viewer</code> ID so that we're able to append a pokemon node to the <code>allPokemons</code> connection (see <code>getConfigs</code>).</li>
</ul>
<p>This is what our mutation subclass would look like:</p>
<div><pre>copy<code>import Relay from 'react-relay'
export default class CreatePokemonMutation extends Relay.Mutation {
​
  // Specifies required data for this mutation.
  // Needs to be supplied together with `getVariables` defined below when calling this mutation.
  static fragments = {
    viewer: () =&gt; Relay.QL`
      fragment on Viewer {
        id
      }
    `,
  }
​
  // Specifies name of the mutation from the GraphQL schema.
  getMutation () {
    return Relay.QL`mutation{createPokemon}`
  }
​
  // Specifies what data may have changed due to this mutation.
  getFatQuery () {
    return Relay.QL`
      fragment on CreatePokemonPayload {
        pokemon
        edge
        viewer {
          allPokemons
        }
      }
    `
  }
​
  // Uses RANGE_ADD type to add `pokemon` node to `allPokemons` edge
  getConfigs () {
    return [{
      type: 'RANGE_ADD',
      parentName: 'viewer',
      parentID: this.props.viewer.id,
      connectionName: 'allPokemons',
      edgeName: 'edge',
      rangeBehaviors: {
        '': 'append',
      },
    }]
  }
​
  // Required variables for this mutation.
  // Needs to be supplied together with objects defined in `fragments` above when calling this mutation
  getVariables () {
    return {
      name: this.props.name,
      url: this.props.url,
    }
  }
​
  // Defines an optimistic response to instantly update the UI. This will be overwritten if the mutation fails.
  getOptimisticResponse () {
    return {
      edge: {
        node: {
          name: this.props.name,
          url: this.props.url,
        },
      },
      viewer: {
        id: this.props.viewer.id,
      },
    }
  }
​
}
</code></pre></div>
<p>In this mutation, we describe what Relay needs to know about the <code>createPokemonMutation</code> to first execute the mutation and then update the client side store to keep its data consistent.</p>
<p>We can then actually send the mutation to the server using the <code>commitUpdate()</code> method that was mentioned above:</p>
<div><pre>copy<code>Relay.Store.commitUpdate(
  new CreatePokemonMutation({name: this.state.name, url: this.state.url, viewer: this.props.viewer}),
  {
    onSuccess: (response) =&gt; console.log('created pokemon', response),
    onFailure: (transaction) =&gt; console.log('error', transaction),
  },
)
</code></pre></div>
<p>To find out more, you can read about other <a href="https://www.learnrelay.org/mutations/mutation-types" target="_blank">mutation configurations</a> and <a href="https://www.learnrelay.org/mutations/optimistic-updates" target="_blank">optimistic responses</a> or read the <a href="https://facebook.github.io/relay/docs/guides-mutations.html" target="_blank">official mutation documentation</a>.</p>
<h4>Mutations with Apollo</h4>
<p>Calling mutations with the Apollo Client follows the same approach as sending queries. We again have two options:</p>
<ol>
<li>Wrapping the React component that should send the mutation with the <code>graphql</code> higher-order component</li>
<li>Send a mutation directly using <code>ApolloClient</code> and handle the return data in a promise</li>
</ol>
<p>In contrast to Relay however, Apollo doesn’t take care of cache consistency with every mutation that is sent, so we have to manually specify how Apollo should update the cache after the mutation has been performed.</p>
<p><strong>1. Wrapping the component with <code>graphql</code></strong></p>
<p>First, we define a mutation with variables using the <code>gql</code> syntax and wrap a React component with <code>graphql</code> to later call the mutation:</p>
<div><pre>copy<code>const createPokemonMutation = gql`
  mutation createPokemon($name: String!, $url: String!) {
    createPokemon(name: $name, url: $url) {
      id
      name
      url
    }
  }
`
const AddPokemonComponentWithMutation = graphql(createPokemonMutation)(AddPokemonComponent)
export default AddPokemonComponentWithMutation
</code></pre></div>
<p>When we used the same approach for fetching data, the query was sent behind the scenes and the returned data was made available to our component as a <code>data</code> object in its props. This time, since we're dealing with a mutation where we want keep control as to <em>when</em> that mutation is fired, Apollo actually injects a new function called <code>mutate</code> into the component's props that we can use explicitly to send the mutation to the server:</p>
<div><pre>copy<code>const {name, url} = this.state
this.props.mutate({variables: {name, url}})
  .then((data) =&gt; {
    console.log(data)
  })
</code></pre></div>
<p>However, to ensure cache consistency in that scenario, we have to configure our <code>AddPokemonComponentWithMutation</code> with an <a href="http://dev.apollodata.com/react/cache-updates.html#updateQueries" target="_blank"><code>updateQueries</code></a> object.</p>
<blockquote>
<p>From the <a href="http://dev.apollodata.com/react/cache-updates.html" target="_blank">Apollo docs</a>: Most of the time, your UI will update automatically based on mutation results, as long as the object IDs in the result match up with the IDs you already have in your store. See the <a href="http://dev.apollodata.com/react/cache-updates.html#dataIdFromObject" target="_blank"><code>dataIdFromObject</code></a> documentation above for more information about how to take advantage of this feature. However, if you are removing or adding items to a list with a mutation or can’t assign object identifiers to some of your objects, you’ll have to use <code>updateQueries</code> to make sure that your UI reflects the change correctly.</p>
</blockquote>
<p>In essence, the <code>updateQueries</code> object is a map from the name of a query (that we used previously to fetch some data) to a function that will specify how the new data that's returned from the mutation should be incorporated into the former result of the query. We thus avoid having to refetch the data for the query but instead specify how the cache should be changed after the mutation. The function that we specify follows the same principle as a <a href="http://redux.js.org/docs/basics/Reducers.html" target="_blank">Redux reducer</a> in that it receives the previous result of the query and the mutation data and merges the two into the new query result.</p>
<p>Taking the example from above, we can add the <code>updateQueries</code> configuration like so:</p>
<div><pre>copy<code>const AddPokemonComponentWithMutation = graphql(createPokemonMutation, {
  props({ ownProps, mutate }) {
    return {
      createPokemon({ variables }) {
        return mutate({
          variables: { ...variables },
          updateQueries: {
            allPokemonsQuery: (prev, { mutationResult }) =&gt; {
              const newPokemon = mutationResult.data.createPokemon
              return {
                ...prev,
                allPokemons: [...prev.allPokemons, newPokemon]
              }
            },
          },
        })
      },
    }
  },
})(AddPokemonComponent)
</code></pre></div>
<p>What happens here with <code>updateQueries</code> is that we tell the Apollo Client to update all places where we used the <code>allPokemonsQuery</code> to also include the new pokemon. Once the mutation is sent and the data is returned from the server, the function we specified for the <code>allPokemonsQuery</code> will be called and the cache will be updated as specified. The resulting change is made available through the props of all components that were using data from that query and the UI will be rerendered.</p>
<p>Note that if we have multiple queries that are affected by a mutation, all of them need to be included in <code>updateQueries</code> individually. For example, consider this query:</p>
<div><pre>copy<code>const TrainerQuery = gql`
  query TrainerQuery {
    Trainer(name: "Ash Ketchum") {
      ownedPokemons
    }
  }
`
</code></pre></div>
<p>If we used this query at some point before and its returned data was cached, we would have to include a <code>TrainerQuery</code> as part of the returned object in <code>updateQueries</code> as well to make sure the cache is properly updated.</p>
<p>To find our more, you can read about other <a href="https://www.learnrelay.org/mutations/mutation-types" target="_blank">advanced mutations</a>, <a href="https://www.learnapollo.com/excursions/excursion-02" target="_blank">managing Apollo Store</a> or read the <a href="http://dev.apollodata.com/react/cache-updates.html" target="_blank">official mutation documentation</a>.</p>
<p><strong>2. Using <code>ApolloCient</code> to directly send a mutation</strong></p>
<p>Rather than making the mutation available through the props of a component, we can also use an instance of the <code>ApolloClient</code> to directly send a mutation. The code for that would look similar to sending a query but using the <a href="http://dev.apollodata.com/core/apollo-client-api.html#ApolloClient.mutate" target="_blank">mutate</a> method of the client:</p>
<div><pre>copy<code>mutate({
  mutation: gql`
      mutation createPokemon($name: String!, $url: String!) {
        createPokemon(name: $name, url: $url) {
        id
        name
        url
      }
    }
  `,
  variables: {
    name: "Zapdos",
    url: "[http://assets.pokemon.com/assets/cms2/img/pokedex/full/145.png](http://assets.pokemon.com/assets/cms2/img/pokedex/full/145.png)"
  },
  updateQueries: {
    allPokemonsQuery: (prev, { mutationResult }) =&gt; {
      const newPokemon = mutationResult.data.createPokemon
        return {
          ...prev,
          allPokemons: [...prev.allPokemons, newPokemon]
        }
      },
    }
})
.then(result =&gt; console.log(result))
</code></pre></div>
<p>Note that we can specify how Apollo should be updating the local cache after the mutation in the same way as before using <code>updateQueries</code>.</p>
<h3>Subscriptions</h3>
<p>GraphQL offers the ability for clients to <a href="http://graphql.org/blog/subscriptions-in-graphql-and-relay/" target="_blank">subscribe</a> to changes that are caused by mutations in a GraphQL backend. This allows the client to implement realtime functionality in an application and always keep the UI up to date with the current server-side state.</p>
<p>With Relay, there is not a lot of support for handling subscriptions on the client. You can use this <a href="http://graphql.org/blog/subscriptions-in-graphql-and-relay/" target="_blank">helper</a> package to ease up integration of subscriptions in Relay. Other than that there is not a lot of support that comes with Relay.</p>
<p>Apollo on the other hand offers a relatively sophisticated support for subscriptions through an additional package called <a href="https://github.com/taion/graphql-relay-subscription" target="_blank">subscriptions-transport-ws</a>. If you're keen on learning more about how subscriptions work with the Apollo Client, you can read up on it in our comprehensive <a href="https://www.graph.cool/docs/tutorials/relay-vs-apollo-iechu0shia/!alias-ui0eizishe/" target="_blank">tutorial</a> and checkout the <a href="https://github.com/graphcool-examples/react-graphql/tree/master/subscriptions-with-apollo-worldchat" target="_blank">example project</a>.</p>
<h3>Conclusion</h3>
<p>Relay and Apollo vary greatly in their approaches how they interact with a GraphQL server and make data available to React components.</p>
<p>Apollo optimizes for ease of use and flexibility, thus allowing developers to get started quickly with their applications. However, making sure that the local cache is kept consistent with Apollo requires lots of manual effort and, especially in larger applications, can get pretty complicated.</p>
<p>Relay on the other hand is a very sophisticated system that is designed from the ground up to maximize efficiency in the communication with the server. React components express their data requirements using GraphQL fragments that are co-located to each component. This makes it easier to ensure that each component gets the data it needs even when data requirements for other components in the hierarchy are changing. Relay is doing a lot of work behind the scenes to keep its local store consistent with the state on the server. The power of Relay comes at the price difficult to grasp complexity and a slow learning curve.</p>
<p>Both Apollo and Relay are still actively being worked on and improved. Facebook is planning a major release they’re currently sometimes referred to as <a href="https://www.youtube.com/watch?v=OEfUBN9dAI8" target="_blank">Relay Modern</a> that is supposed to improve the developer experience and lower the entrace barrier for people getting started with Relay. Apollo very recently added their an <a href="https://dev-blog.apollodata.com/apollo-clients-new-imperative-store-api-6cb69318a1e3" target="_blank">imperative store API</a> that allows the developer to have more fine-grained control over how the local cache should be updated after a mutation and provides an alternative to updateQueries.</p>
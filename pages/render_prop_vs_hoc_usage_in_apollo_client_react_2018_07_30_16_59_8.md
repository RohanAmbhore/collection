<a href="https://spectrum.chat/thread/d2e9ad39-f6b2-4614-ae20-3f619100bb3b">https://spectrum.chat/thread/d2e9ad39-f6b2-4614-ae20-3f619100bb3b</a><div id="articleHeader"><h1>Render prop vs HOC usage in apollo-client</h1></div><a href="/react" target="_blank">React</a> / <a href="/react/general" target="_blank">General</a><a href="/thread/d2e9ad39-f6b2-4614-ae20-3f619100bb3b" target="_blank">April 23, 2018 · 6:35pm</a><div><div>Important Note : This is not about which one is best, but rather which one fits which scenario.</div></div><div><div>I've been writing a <a href="http://contibuting.md" target="_blank">contibuting.md</a> file for out front-end team, so far so good. I arrived to the graphql section. This is how we're going to structure our queries and mutations (inspired by <a href="https://github.com/withspectrum/spectrum/blob/alpha/shared/graphql/queries/channel/getChannel.js" target="_blank">spectum code</a>) :</div></div><div><div>The way query and mutation files are structured is:</div></div><ul><li><div> The query as a named export  export const leadsQuery = gql`` </div></li><li><div>The options for the query leadsQueryOptions  (not exported)</div></li><li><div>The default export graphql(leadsQuery, leadsQueryOptions) </div></li><li><div>When importing the default, its name starts with with   import withLeadsQuery from "graphql/queries/leads" </div></li><li><div> This structure enables quick usage of the query, and further customization if needed by importing only the query and changing the options to suit.</div></li><li><div> It also allows using the render prop pattern using Query components.</div></li></ul><div><div>Here is some sample code</div></div><pre><code><div><div>import gql from "graphql-tag";
import { graphql } from "react-apollo";

export const loginMutation = gql`
  mutation Login($email: String!, $password: String!) {
    login(email: $email, password: $password) {
      token
    }
  }
`;
const loginMutationOptions = {
  props: ({ mutate }) =&gt; ({
    login: ({ email, password }) =&gt; mutate({ variables: { email, password } }),
  }),
};
export default graphql(loginMutation, loginMutationOptions);</div></div></code></pre><div><div>Now the next section is </div></div><h3><div>HOC vs render prop:</div></h3><div><div>When to use HOC? render prop? why?!!</div></div><div><div>I did <a href="https://dev-blog.apollodata.com/query-components-with-apollo-ec603188c157" target="_blank">some</a>  research and found the following arguments in favour of the render prop:</div></div><ol><li><div>Testability </div></li><li><div>Separation of concerns</div></li><li><div>Abstraction over data management layer</div></li></ol><div><div>Now let's push these arguments a bit:</div></div><h4><div>Testability and separation of concerns</div></h4><div><div>I don't see any particular improvement in testing. And we can put the query logic in a separate file for separation of files/concerns</div></div><pre><code><div><div>import withLeads from "graphql/queries/leads"
export const LeadsList = () =&gt; &lt;div&gt;...&lt;/div&gt;
export default withLeads(LeadsList)</div></div></code></pre><h4><div>Abstraction over data management layer</div></h4><div><div>I don't think this one is a strong argument, as we very rarely (i.e never) change data management layers.</div></div><div><div>I did <a href="http://engineering.khanacademy.org/posts/creating-query-components-with-apollo.htm" target="_blank">more research</a> and found the following arguments in favour of the Query component:</div></div><ol><li><div>When using HOC, The properties of the component don't properly communicate the intended usage, as you don't know which props you should pass to the component VS data-fetching prop-types</div></li><li><div>This use case "We'd like to pass a parameter to the component in order to filter the query by date"  makes presentation component tightly coupled to the query logic. Using the same logic in another component isn't obvious </div></li></ol><h4><div>Prop types</div></h4><div><div>This is a totally valid argument. And we can circumvent it with a simple comment // data fetching props </div></div><h4><div>Tight coupling</div></h4><div><div>In the example of the article above, mapping props is done in the query side. And it's what makes it tightly coupled to the presentation component. </div></div><h3><div>In favour of the render prop</div></h3><div><div>I have been pushing back the render prop even though i like it. Here are some reasons for using it instead of HOC.</div></div><div><div>1- The query is launched as soon as the component renders. Maybe you want to delay  it until it's needed.</div></div><pre><code><div><div>render(){
    return (
        &lt;div&gt;
            ...
            { timeToLoadMe && (
                &lt;Query query={leadsQuery}&gt;
                    {()=&gt; ...}
                &lt;/Query&gt;
            )}
        &lt;/div&gt;
    )
}</div></div></code></pre><div><div>2- You're planning to move some part to a separate component. You might as well move data and presentation all together.</div></div><div><div>What are your thoughts on this? what are your use cases?</div></div>
<a href="https://stackoverflow.com/questions/43233760/what-are-the-differences-between-apollo-client-and-relay">https://stackoverflow.com/questions/43233760/what-are-the-differences-between-apollo-client-and-relay</a><div id="articleHeader"><h1>What are the differences between Apollo Client and Relay?</h1></div>

            

<div id="question">

    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        2
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>1</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I have just been introduced to GraphQL and am deciding between the two frameworks (<a href="http://dev.apollodata.com/" target="_blank">Apollo</a> and <a href="https://facebook.github.io/relay/" target="_blank">Relay</a>) for implementing my front end React web app.</p>

<p>I'm aware that Relay is built by Facebook, while Apollo is by Meteor. Has anyone tried both and how has your experience been? I'm wondering what are the differences between them and which kind of GraphQL apps would benefit more from using Relay as compared to Apollo.</p>
    </div>
    
    
</div>

                        <div>
                <div>
        <h2>                    <b>closed</b> as primarily opinion-based by <a href="/users/499214/john-dvorak" target="_blank">John Dvorak</a>, <a href="/users/4342498/nathanoliver" target="_blank">NathanOliver</a>, <a href="/users/409792/zwippie" target="_blank">zwippie</a>, <a href="/users/1324/paul-roub" target="_blank">Paul Roub</a>, <a href="/users/2370483/machavity" target="_blank">Machavity</a> Apr 6 '17 at 14:01
</h2>
        <p>Many good questions generate some degree of opinion based on expert experience, but answers to this question   will tend to be almost entirely based on opinions, rather than facts, references, or specific expertise. If this question can be reworded to fit the rules in the <a href="/help/closed-questions" target="_blank">help center</a>, please <a href="/posts/43233760/edit" target="_blank">edit the question</a>.</p>
    </div>
            </div>
    
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-43256057">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        12
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p><strong>TL;DR:</strong> The answer to this question boils down to "it depends". I encourage you to try both GraphQL clients and come up with your own conclusion. <a href="https://www.learnapollo.com" target="_blank">Learn Apollo</a> and <a href="https://www.learnrelay.org" target="_blank">Learn Relay</a> are great resources to get started with this, or you could try example apps for <a href="https://github.com/graphcool-examples/react-relay-instagram-example" target="_blank">Relay</a> and <a href="https://github.com/graphcool-examples/react-apollo-instagram-example" target="_blank">Apollo</a>.</p>

<p>Have a look at this <a href="https://www.graph.cool/docs/tutorials/relay-vs-apollo-iechu0shia/" target="_blank">in-depth comparions of Apollo vs. Relay</a>. Here's a quick overview:</p>

<h2>Frameworks</h2>

<p>Relay only works on React and RN while Apollo is framework agnostic. As you want to build a React app, that's not an issue for you, but it's still worth mentioning.</p>

<h2>GraphQL API</h2>

<p>Relay requires a custom schema further described in the <a href="https://facebook.github.io/relay/docs/graphql-relay-specification.html" target="_blank">Relay specification</a>. Apollo works with any GraphQL schema.</p>

<h2>Flexibility</h2>

<p>Relay imposes a strict, fixed structure that you absolutely need to follow. Apollo on the other hand gives you a lot of different approaches and choices for handling a particular topic.</p>

<h2>Productivity</h2>

<p>Relay offers great developer experience, but comes with a high entry barrier. Apollo requires more manual work to get things done.</p>

<h2>Difficulty</h2>

<p>Relay introduces <a href="https://www.graph.cool/blog/connections-edges-nodes-relay-tioghei9go/" target="_blank">a lot of new concepts</a> and to reiterate, comes with a high entry barrier. Apollo is extremely easy to get started with in constrast to that.</p>

<h2>Subscriptions</h2>

<p>Aside from some community efforts to make subscriptions work with Relay, there's not really a consensus about subscriptions in Relay. On the other hand, Apollo integrates nicely with <a href="https://github.com/apollographql/subscriptions-transport-ws" target="_blank"><code>subscriptions-transport-ws</code></a> that already finds great adoption in the community. Here's a <a href="https://demo.graph.cool/worldchat/" target="_blank">worldchat app using GraphQL subscriptions</a> for example.</p>

<h2>Schema Check</h2>

<p>Relay requires <a href="https://github.com/graphcool/babel-plugin-react-relay" target="_blank">a schema check using Babel on build-time</a>. Apollo offers optional tools for this instead.</p>
    </div>
    
</div>
    
        </div>
</div>
                


                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/reactjs" title="show questions tagged 'reactjs'" target="_blank">reactjs</a> <a href="/questions/tagged/graphql" title="show questions tagged 'graphql'" target="_blank">graphql</a> <a href="/questions/tagged/relay" title="show questions tagged 'relay'" target="_blank">relay</a> <a href="/questions/tagged/apollo" title="show questions tagged 'apollo'" target="_blank">apollo</a> <a href="/questions/tagged/react-apollo" title="show questions tagged 'react-apollo'" target="_blank">react-apollo</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="https://www.grok-interactive.com/blog/building-reusable-react-with-redux-components/">https://www.grok-interactive.com/blog/building-reusable-react-with-redux-components/</a><div id="articleHeader"><h1>Building reusable components with React and Redux</h1></div><div> <time>Jan 10, 2017</time> <a href="/blog/anton-domratchev/" target="_blank">Anton Domratchev</a></div><div class="readableLargeImageContainer"><img src="/assets/2017/01/Verschiedene_LEDs-e70dd5bf0b0c7382530e7c4e329ff2d1fbbbfbb0f42a1e6543fe684a09548d2b.jpg" alt="Building reusable components with React and Redux" /></div><h1>Building reusable components with React and Redux.</h1><p>Recently, I've been spending a majority of my time in React and I began to really enjoy front-end JavaScript development. I avoided JavaScript from the beginning of my career as a programmer, and I think it was mostly because I didn't have a good way of keeping and maintaining a state in components. I've been writing a React Redux single page application for the past several months and have learned a great deal about making front end applications. Most of all, I learned to build reusable components in React. These components can be used throughout the application and even packaged to be used in other projects because of their <code>scoped action</code> prop. While on the project, I made a component which could dispatch an action to a number different reducers. The component would receive a <code>scope</code> prop from its highest order parent, that prop would contain the component's <code>scoped action type</code>.</p><p>What makes React a great platform for building applications is its powerful <a href="https://facebook.github.io/react/docs/composition-vs-inheritance.html" target="_blank">component composition model</a>. The React team at Facebook encourages the use of component composition for building container components. An example of a container component would be a <code>Tweet</code> on a page which is composed of <code>TweetHeader</code>, <code>TweetLikeButton</code>, and <code>TweetBody</code> among other similar components. Some components can have children components as well, <code>MentionedUsernames</code> and <code>Hashtags</code> would compose the <code>TweetBody</code> component. Such component structure allows for high reusability of each child component throughout the application. A generic button component can be specialized to work in any context with use of props. Props are simply properties that are passed from the parent component to the child component. Props are also useful when working Redux for state management. By providing the component with a <code>scoped action type</code> prop we can use the same component action with different reducers.</p><p>Let's look at an example of the component structure in this situation.</p><div><pre><code>|app
|--containers
|----HomeFeedPage
|----UserFeedPage
|----TweetPage
|--components
|----Tweet
|------TweetHeader
|------TweetLikeButton
</code></pre></div><p>From the <code>containers</code> directory we can see that a <code>Tweet</code> component may be used in three different contexts of <code>HomeFeedPage</code>, <code>UserFeedPage</code>, and <code>TweetPage</code>. A <code>Tweet</code> component contains a <code>TweetLikeButton</code> component which would dispatch an action to transform some data in the state.</p><p>First, we will need to create a scope for the shared action types</p><div><pre><code>export const HOME_FEED = {
    INCREMENT_LIKE_COUNT: "HOME_FEED_INCREMENT_LIKE_COUNT",
}

export const USER_FEED = {
    INCREMENT_LIKE_COUNT: "USER_FEED_INCREMENT_LIKE_COUNT",
}

export const TWEET_PAGE = {
    INCREMENT_LIKE_COUNT: "TWEET_PAGE_INCREMENT_LIKE_COUNT",
}
</code></pre></div><p>As you may have already noticed, the scope is just a simple object which namespaces the action type. We can continue to use this scope to designate which action belongs where.</p><p>Let's start looking at the components going from the highest order parent down to the child component with our scoped action. <code>HomeFeedPage</code> container might look like so:</p><div><pre><code>/** imported dependencies and components */
import { HOME_FEED } = 'actions/actionTypes'

export default class HomeFeedPage extends React.Component {
    componentWillMount() {
        /** Do some async action */
    }

    render() {
        const { tweets } = this.props
        return (
            &lt;div&gt; 
                tweets.map(tweet =&gt; &lt;Tweet {...tweet} scope={HOME_FEED}/&gt;) || null
            &lt;/div&gt;
        )
    }
}
</code></pre></div><p>Notice the scope is being injected into props at this compoent. In this component we map over the tweet data and return a component with props.</p><p>Let's take a look at what Tweet would look like:</p><div><pre><code>/** imported dependencies and components */

export default const Tweet = (props) =&gt; {
    return (
        &lt;div&gt;
            &lt;TweetHeader tweetHeader={props.tweetHeader} /&gt;
            &lt;TweetLikeButton tweetId={props.tweetId} scope={props.scope} /&gt;
        &lt;/div&gt;
    )
}
</code></pre></div><p>In this component we pass the scope prop down to the connected component. The parent component should have <code>PropTypes</code> validation to require the scope prop. We dont need to validate the structure at this point, we just want to make sure we have that prop present, since it is being used by child compoents.</p><p>Next, let's take a look at the button code:</p><div><pre><code>/** imported dependencies and components */

class TweetLikeButton extends React.Component {
    handleLikeClick = (e) =&gt; {
        const { dispatch } = this.props
        dispatch(handleTweet(
            this.props.tweetId, 
            this.props.scope.INCREMENT_LIKE_COUNT // This action should be validated in the props
        ))
    }

    render() {
       return &lt;button onClick={handleLikeClick} value="Like this Tweet" /&gt;
    }
}

export default connect()(TweetLikeButton)

/** Validate props for presence of the action type */
</code></pre></div><p>By providing the scope prop to <code>TweetLikeButton</code> we can now dispatch actions to the reducer provided in the scope. At this point we will need to validate that the passed scope prop contains the action that our component is expecting.</p><p>Now, let's look at the <code>handleTweet</code> action:</p><div><pre><code>function incrementLikeCount(tweetId, actionType) {
    return { type: actionType, payload: tweetId }
}

export function handleTweet(tweetId, actionType) {
    return dispatch =&gt; {
        return asyncCallToApi(tweetId)
            .then(json =&gt; dispatch(incrementLikeCount(tweetId, actionType)))
    }
}
</code></pre></div><p>Our <code>handleTweet</code> action takes an <code>id</code> and an <code>actionType</code> arguments. The action type is scoped so now it will be picked up by the corresponding reducer. I am omitting the reducer code as it is irrelevant for this example.</p><blockquote><p>The above implementation is simplified for brevity but a more robust solution would be to implement a switch case on the action type in the action creator function. By white listing the actions we would expect to get from the component, it would allow us to add a default <code>NOOP</code> action in case the component gave the action creator something unexpected.</p></blockquote><p>Now the component can stay unchanged and new <code>scoped action types</code>, and reducers can be added to accomodate the data for that component. By making more reusable components we can expect making more specific components and reduce the overall application size. Making reusable components is easy through component composition. By providing your components with a <code>scoped action type</code> we are able to put it in different contexts and expect it to operate the same. Some components can be generalized enough to be exported as modules and used in other React projects.</p><div id="mc_embed_signup"> <div id="mc_embed_signup_scroll"> <label>Subscribe to our newsletter for more articles like this one</label> </div><p> Categories: <a href="/blog/category/software_development/" target="_blank">Software Development</a> | Tags: <a href="/blog/tag/reactjs/" target="_blank">ReactJS</a>, <a href="/blog/tag/redux/" target="_blank">Redux</a>, <a href="/blog/tag/components/" target="_blank">components</a>, <a href="/blog/tag/action_types/" target="_blank">action types</a></p><p> SHARE:    </p>
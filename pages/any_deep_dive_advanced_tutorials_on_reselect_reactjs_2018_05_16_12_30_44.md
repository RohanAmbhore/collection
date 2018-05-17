<a href="https://www.reddit.com/r/reactjs/comments/5dxasp/any_deepdiveadvanced_tutorials_on_reselect/">https://www.reddit.com/r/reactjs/comments/5dxasp/any_deepdiveadvanced_tutorials_on_reselect/</a><div id="articleHeader"><h1>Any deep-dive/advanced tutorials on reselect?</h1></div><div><p><strong>Forward:</strong> Maybe "advanced" is too strong a request (as I might simply not be understanding it correctly!).</p><p>I use selectors and I "get" them to an extent - I understand their purpose, and "why" we should be using them. Before using reselect, I used lodash' memoize to achieve similar outcomes (I think, again, unless I am misunderstanding something).</p><p>However, I get stuck on a few key concepts:</p><ol><li><p>arguments. Namely why dynamic arguments are discouraged (<a href="https://github.com/reactjs/reselect#q-how-do-i-create-a-selector-that-takes-an-argument" target="_blank">docs</a>). Initially I thought one of the most powerful parts of reselect would be shooting in arguments to get a particular slice of the state.</p></li><li><p>the purpose of factory functions in the context of reselect (which is partially tied to question 1 above). Especially when talking about react-connect, <a href="https://github.com/reactjs/reselect#sharing-selectors-with-props-across-multiple-components" target="_blank">multiple components</a>. I understand I have to pass a function to connect that itself returns a function, but I don't feel like I understand the "why".</p></li></ol><p>So back to the original question, any really deep dive tutorials on reselect - I prefer to really understand things. Something like Dans redux tutorials on egghead - those helped me understand <em>how</em> and <em>why</em> redux worked.</p><p>Thanks!</p></div><div><div><div><div>3 comments</div>67% Upvoted<div><div><div>This thread is archived</div><div>New comments cannot be posted and votes cannot be cast</div><div><div>Sort by</div><div><div><div><div><div id="t1_da88r5m"><div><div><div><div><p>I'll be honest, I don't entirely understand the way the discussions refer to "dynamic arguments" either.</p><p>For what it's worth, selectors created with Reselect <em>do</em> allow you to pass in arguments, but in a slightly limited way.  Reselect's implementation looks <em>very</em> roughly like this:</p><pre><code>function createSelector(inputSelectors, finalSelector) {

    return function selectorFunction(...args) {
        const inputResults = inputSelectors.map(selector =&gt; selector(...args));
        
        return finalSelector(...inputResults);
    }
}
</code></pre><p>Note that whatever arguments you passed to the selector actually get passed to all of the input selectors you used in creating it.  So, those input selectors <em>can</em> absolutely use more than one argument, not just <code>state</code>, but the inputs also need to be somewhat compatible with each other.  If, say, <code>inputSelector1</code> is expecting its second argument to be an object with <code>{itemId}</code>, and <code>inputSelector2</code> is expecting its second argument to be a number, then things would probably break.</p><p>As for factory functions, the issue is that a given selector generated by <code>createSelector</code> by default only memoizes the arguments it was last called with.  If you're only calling it with <code>const someData = selectTheData(getState())</code>, then there's no problem.  However, if you have a component that wants to look up an item based on an ID it was given as a prop, and multiple instances of that component exist at once, then each component would be using the same instance of the selector function, like this: <code>const itemData = selectTheItem(state, ownProps.itemId)</code>.  That means that the memoization for the selector would be useless, because every component would be passing in different arguments.</p><p>Using the factory syntax for a Redux <code>mapState</code> function gives you space to create a unique selector function instance for every component.  That allows the memoization to work properly for that component instance, since the inputs to the selector will be consistent between calls.  A basic example looks like:</p><pre><code>function makeMapState(originalState, originalOwnProps) {
    const uniqueSelectorInstance = makeSelectorForThisItem();
    
    return function actualMapState(state, ownProps) {
        const dataForThisItem = uniqueSelectorInstance(state, ownProps.itemId);
        
        return {item : dataForThisItem};
    }    
}
</code></pre><p>FYI, I have some articles on use of selectors in my <a href="https://github.com/markerikson/react-redux-links" target="_blank">React/Redux links list</a>, under the <a href="https://github.com/markerikson/react-redux-links/blob/master/redux-techniques.md#selectors-and-normalization" target="_blank">Redux Techniques#Selectors</a> category.  I also have some further links in the <a href="http://redux.js.org/docs/FAQ.html" target="_blank">Redux FAQ</a>, under <a href="http://redux.js.org/docs/faq/Performance.html#performance-scaling" target="_blank">Performance#Scaling</a>.</p><p>Hopefully that helps clear things up!</p></div><div><div><div id="t1_da98dr6"><div><div><div><div><a href="/user/mastermog" target="_blank">mastermog</a></div><i id="CommentTopMeta--OP--t1_da98dr6"><desc>Original Poster</desc></i>2 points·<a href="/r/reactjs/comments/5dxasp/any_deepdiveadvanced_tutorials_on_reselect/da98dr6/" id="CommentTopMeta--Created--t1_da98dr6" target="_blank">1 year ago</a><div><div><p>Man, you're a champion. I'm reading and re-reading this until it sinks in. Thanks. And btw, keep up the awesome blog posts.</p></div><div><div><div id="t1_da9n8sd"><div><div><div><div><p>Heh, thanks :)  And yeah, yesterday I put together a first draft of the next post in my "Practical Redux" series, and I'm hoping to publish that by Wednesday.  I'll submit it here when it goes up.</p></div>
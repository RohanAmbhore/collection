<a href="http://blog.isquaredsoftware.com/2016/10/idiomatic-redux-why-use-action-creators/">http://blog.isquaredsoftware.com/2016/10/idiomatic-redux-why-use-action-creators/</a><div id="articleHeader"><h1>Idiomatic Redux: Why use action creators?</h1></div>
    
	
        
	    
    	<p>This is a post in the <a href="/series/idiomatic-redux" target="_blank"><b>Idiomatic Redux</b></a> series.
        </p><hr />
	 
  </header>
  
    <p><em>First in an occasional series of thoughts on good usage patterns for Redux</em></p>

<h3 id="preface">Preface</h3>

<p>I've spent a lot of time discussing Redux usage patterns online, whether it be helping answer questions from learners in the Reactiflux channels, debating possible changes to the Redux library APIs on Github, or discussing various aspects of Redux in comment threads on Reddit and HN.  Over time, I've developed my own opinions about what constitutes good, idiomatic Redux code, and I'd like to start sharing some of those thoughts.  Despite my status as a Redux maintainer, <strong>these are <em>just</em> opinions</strong>, but I think they're pretty good approaches to follow :)</p>

<h3 id="action-creators">Action Creators</h3>

<p>One of the most common complaints about Redux is the amount of "boilerplate" involved.  People complain about having to declare constants, writing indirect code, touching multiple files to implement features, and so on.  I've specifically seen people asking why "action creators" are needed in several places (such as <a href="https://www.reddit.com/r/reactjs/comments/50azs2/10_tips_for_better_redux_architecture_javascript/d74doei?context=2" target="_blank">here</a>, <a href="https://www.reddit.com/r/reactjs/comments/4upe9t/async_redux_workflow_calling_actions_outside_redux/" target="_blank">here</a>, and <a href="https://www.reddit.com/r/reactjs/comments/51rfr1/react_redux_50_could_use_your_help_in_going_from/d7egp4a" target="_blank">here</a>).</p>

<p>So, <strong>why not just put all your logic right into a component?</strong>  Dan Abramov has written some fantastic answers on similar topics, and I've answered this question several times, but I'd like to cover the topic in more detail.</p>

<p>First, let's start with some clarification of terms and concepts:</p>

<ul>
<li>An <em>action</em> is a plain simple object, like <code>{type : "ADD_TODO", text : "Buy milk"}</code>.</li>
<li>An <em>action type</em> is the value for the <code>type</code> field in an action.  Per the Redux FAQ, <a href="http://redux.js.org/docs/faq/Actions.html#actions-string-constants" target="_blank">this field <em>should</em> be a string</a>, although Redux only enforces that a <code>type</code> field exists in the action.</li>
<li>An <em>action creator</em> is a function that returns an action, like:</li>
</ul>

<pre><code>function addTodo(text) {
    return {
        type : "ADD_TODO",
        text
    }
}
</code></pre>

<ul>
<li>A <em>thunk action creator</em> is a function that returns a function.  If you're using the <code>redux-thunk</code> middleware, the inner function will be called and given references to <code>dispatch</code> and <code>getState</code>, like this:</li>
</ul>

<pre><code>function makeAjaxCall(someValue) {
    return (dispatch, getState) =&gt; {
        dispatch({type : "REQUEST_STARTED"});
        
        myAjaxLib.post("/someEndpoint", {data : someValue})
            .then(response =&gt; dispatch({type : "REQUEST_SUCCEEDED", payload : response})
            .catch(error =&gt; dispatch({type : "REQUEST_FAILED", error : error});    
    };
}
</code></pre>

<h3 id="reasons-for-using-action-creators">Reasons for Using Action Creators</h3>

<p>Per Dan's answers on Stack Overflow, it's completely possible to do the work of making AJAX calls and calling <code>dispatch</code> entirely inline in a component.  However, as programmers, it is good practice to encapsulate behavior, separate concerns, and keep code duplication to a minimum.  We'd also like to keep our code as testable as possible.</p>

<p>To me, there are <strong>five primary reasons to use action creators</strong> rather than putting all your logic directly into a component:</p>

<ol>
<li><strong>Basic abstraction</strong>: Rather than writing action type strings in every component that needs to create the same type of action, put the logic for creating that action in one place.</li>
<li><strong>Documentation</strong>: The parameters of the function act as a guide for what data is needed to go into the action.</li>
<li><strong>Brevity and DRY</strong>: There could be some larger logic that goes into preparing the action object, rather than just immediately returning it.</li>
<li><strong>Encapsulation and consistency</strong>: Consistently using action creators means that a component doesn't have to know any of the details of creating and dispatching the action, and whether it's a simple "return the action object" function or a complex thunk function with numerous async calls. It just calls <code>this.props.someBoundActionCreator(arg1, arg2)</code>, and lets the action creator worry about how to handle things.</li>
<li><strong>Testability and flexibility</strong>: if a component only ever calls a function passed in as a prop rather than explicitly referencing <code>dispatch</code>, it becomes easy to write tests for the component that pass in a mock version of the function instead.  It also enables reusing the component in another situation, or even with something other than Redux.</li>
</ol>

<h3 id="dispatching-actions-from-components">Dispatching Actions from Components</h3>

<p>There's a number of semantically equivalent ways to dispatch Redux actions to the store from a component.  For example, all these do the same thing:</p>

<pre><code>// approach 1: define action object in the component
this.props.dispatch({
    type : "EDIT_ITEM_ATTRIBUTES", 
    payload : {
        item : {itemID, itemType},
        newAttributes : newValue,
    }
});

// approach 2: use an action creator function
const actionObject = editItemAttributes(itemID, itemType, newAttributes);
this.props.dispatch(actionObject);

// approach 3: directly pass result of action creator to dispatch
this.props.dispatch(editItemAttributes(itemID, itemType, newAttributes));

// approach 4: pre-bind action creator to automatically call dispatch
const boundEditItemAttributes = bindActionCreators(editItemAttributes, dispatch);
boundEditItemAttributes(itemID, itemType, newAttributes);
</code></pre>

<p>To me, the simplest and most idiomatic approach is to <strong>always use pre-bound action creators</strong> in your components.  This removes the need for components to worry about <code>dispatch</code>, and makes them agnostic to Redux itself.  In addition, I highly encourage the use of the <strong>object literal shorthand for binding actions with <code>connect</code></strong>:</p>

<pre><code>import {connect} from "react-redux";
import {action1, action2} from "myActions";


const MyComponent = (props) =&gt; (
    &lt;div&gt;
        &lt;button onClick={props.action1}&gt;Do first action&lt;/button&gt;
        &lt;button onClick={props.action2}&gt;Do second action&lt;/button&gt;
    &lt;/div&gt;
)

// Passing an object full of actions will automatically run each action 
// through the bindActionCreators utility, and turn them into props

export default connect(null, {action1, action2})(MyComponent);
</code></pre>

<p>For a while, I used a utility function that could generate my <code>mapDispatch</code> functions, and ensure that all my bound action creators were available under a prop named <code>actions</code> (such as <code>this.props.actions.someCallback()</code>).  However, I've changed my mind on that approach, and am phasing that out of my codebase as I go.  I liked the explicitness of the intent, but eventually decided that it was too much of a conceptual coupling to Redux.  My components had to "know" whether they were connected or not by knowing whether to call <code>this.props.actions.someCallback()</code> or <code>this.props.someCallback()</code>.  It also introduced a bit of extra complexity and inconsistency.</p>

<h3 id="final-thoughts">Final thoughts</h3>

<p>I know that many people dislike adding extra layers of indirection and abstraction, to which I sympathize.  I've always been a very pragmatic, direct, "let's write the code that actually does this" kind of developer, and I hate <a href="http://discuss.joelonsoftware.com/?joel.3.219431.12" target="_blank">HammerFactories</a> and enterprise architectures where everything is configured with a 15,000-line XML file.  I've also seen concerns that prolific use of Redux reduces React to nothing more than a "fancy templating language", or a reinvention of MVC under another name.  But, to me, <strong>consistent use of action creators promotes readable code with a reasonable level of abstraction</strong>, is in keeping with software engineering principles of encapsulation and DRY, and provides just enough decoupling between "display logic" and "business logic" to keep a codebase manageable and flexible.</p>

<h3 id="further-information">Further Information</h3>


  
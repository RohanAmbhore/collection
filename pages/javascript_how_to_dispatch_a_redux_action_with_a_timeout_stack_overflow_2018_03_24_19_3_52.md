<a href="https://stackoverflow.com/questions/35411423/how-to-dispatch-a-redux-action-with-a-timeout/35415559#35415559">https://stackoverflow.com/questions/35411423/how-to-dispatch-a-redux-action-with-a-timeout/35415559#35415559</a><div id="articleHeader"><h1>How to dispatch a Redux action with a timeout?</h1></div>
<p>Don’t fall into the <a href="http://amasad.me/2016/01/03/overcoming-intuition-in-programming/" target="_blank">trap of thinking a library should prescribe how to do everything</a>. If you want to do something with a timeout in JavaScript, you need to use <code>setTimeout</code>. There is no reason why Redux actions should be any different.</p>

<p>Redux <em>does</em> offer some alternative ways of dealing with asynchronous stuff, but you should only use those when you realize you are repeating too much code. Unless you have this problem, use what the language offers and go for the simplest solution.</p>

<h2>Writing Async Code Inline</h2>

<p>This is by far the simplest way. And there’s nothing specific to Redux here.</p>

<pre><code>store.dispatch({ type: 'SHOW_NOTIFICATION', text: 'You logged in.' })
setTimeout(() =&gt; {
  store.dispatch({ type: 'HIDE_NOTIFICATION' })
}, 5000)</code></pre>

<p>Similarly, from inside a connected component:</p>

<pre><code>this.props.dispatch({ type: 'SHOW_NOTIFICATION', text: 'You logged in.' })
setTimeout(() =&gt; {
  this.props.dispatch({ type: 'HIDE_NOTIFICATION' })
}, 5000)</code></pre>

<p>The only difference is that in a connected component you usually don’t have access to the store itself, but get either <code>dispatch()</code> or specific action creators injected as props. However this doesn’t make any difference for us.</p>

<p>If you don’t like making typos when dispatching the same actions from different components, you might want to extract action creators instead of dispatching action objects inline:</p>

<pre><code>// actions.js
export function showNotification(text) {
  return { type: 'SHOW_NOTIFICATION', text }
}
export function hideNotification() {
  return { type: 'HIDE_NOTIFICATION' }
}

// component.js
import { showNotification, hideNotification } from '../actions'

this.props.dispatch(showNotification('You just logged in.'))
setTimeout(() =&gt; {
  this.props.dispatch(hideNotification())
}, 5000)</code></pre>

<p>Or, if you have previously bound them with <code>connect()</code>:</p>

<pre><code>this.props.showNotification('You just logged in.')
setTimeout(() =&gt; {
  this.props.hideNotification()
}, 5000)</code></pre>

<p>So far we have not used any middleware or other advanced concept. </p>

<h2>Extracting Async Action Creator</h2>

<p>The approach above works fine in simple cases but you might find that it has a few problems:</p>

<ul>
<li>It forces you to duplicate this logic anywhere you want to show a notification.</li>
<li>The notifications have no IDs so you’ll have a race condition if you show two notifications fast enough. When the first timeout finishes, it will dispatch <code>HIDE_NOTIFICATION</code>, erroneously hiding the second notification sooner than after the timeout.</li>
</ul>

<p>To solve these problems, you would need to extract a function that centralizes the timeout logic and dispatches those two actions. It might look like this:</p>

<pre><code>// actions.js
function showNotification(id, text) {
  return { type: 'SHOW_NOTIFICATION', id, text }
}
function hideNotification(id) {
  return { type: 'HIDE_NOTIFICATION', id }
}

let nextNotificationId = 0
export function showNotificationWithTimeout(dispatch, text) {
  // Assigning IDs to notifications lets reducer ignore HIDE_NOTIFICATION
  // for the notification that is not currently visible.
  // Alternatively, we could store the interval ID and call
  // clearInterval(), but we’d still want to do it in a single place.
  const id = nextNotificationId++
  dispatch(showNotification(id, text))

  setTimeout(() =&gt; {
    dispatch(hideNotification(id))
  }, 5000)
}</code></pre>

<p>Now components can use <code>showNotificationWithTimeout</code> without duplicating this logic or having race conditions with different notifications:</p>

<pre><code>// component.js
showNotificationWithTimeout(this.props.dispatch, 'You just logged in.')

// otherComponent.js
showNotificationWithTimeout(this.props.dispatch, 'You just logged out.')    </code></pre>

<p>Why does <code>showNotificationWithTimeout()</code> accept <code>dispatch</code> as the first argument? Because it needs to dispatch actions to the store. Normally a component has access to <code>dispatch</code> but since we want an external function to take control over dispatching, we need to give it control over dispatching.</p>

<p>If you had a singleton store exported from some module, you could just import it and <code>dispatch</code> directly on it instead:</p>

<pre><code>// store.js
export default createStore(reducer)

// actions.js
import store from './store'

// ...

let nextNotificationId = 0
export function showNotificationWithTimeout(text) {
  const id = nextNotificationId++
  store.dispatch(showNotification(id, text))

  setTimeout(() =&gt; {
    store.dispatch(hideNotification(id))
  }, 5000)
}

// component.js
showNotificationWithTimeout('You just logged in.')

// otherComponent.js
showNotificationWithTimeout('You just logged out.')    </code></pre>

<p>This looks simpler but <strong>we don’t recommend this approach</strong>. The main reason we dislike it is because <strong>it forces store to be a singleton</strong>. This makes it very hard to implement <a href="http://redux.js.org/docs/recipes/ServerRendering.html" target="_blank">server rendering</a>. On the server, you will want each request to have its own store, so that different users get different preloaded data.</p>

<p>A singleton store also makes testing harder. You can no longer mock a store when testing action creators because they reference a specific real store exported from a specific module. You can’t even reset its state from outside.</p>

<p>So while you technically can export a singleton store from a module, we discourage it. Don’t do this unless you are sure that your app will never add server rendering.</p>

<p>Getting back to the previous version:</p>

<pre><code>// actions.js

// ...

let nextNotificationId = 0
export function showNotificationWithTimeout(dispatch, text) {
  const id = nextNotificationId++
  dispatch(showNotification(id, text))

  setTimeout(() =&gt; {
    dispatch(hideNotification(id))
  }, 5000)
}

// component.js
showNotificationWithTimeout(this.props.dispatch, 'You just logged in.')

// otherComponent.js
showNotificationWithTimeout(this.props.dispatch, 'You just logged out.')    </code></pre>

<p>This solves the problems with duplication of logic and saves us from race conditions.</p>

<h2>Thunk Middleware</h2>

<p>For simple apps, the approach should suffice. Don’t worry about middleware if you’re happy with it.</p>

<p>In larger apps, however, you might find certain inconveniences around it.</p>

<p>For example, it seems unfortunate that we have to pass <code>dispatch</code> around. This makes it trickier to <a href="https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0" target="_blank">separate container and presentational components</a> because any component that dispatches Redux actions asynchronously in the manner above has to accept <code>dispatch</code> as a prop so it can pass it further. You can’t just bind action creators with <code>connect()</code> anymore because <code>showNotificationWithTimeout()</code> is not really an action creator. It does not return a Redux action.</p>

<p>In addition, it can be awkward to remember which functions are synchronous action creators like <code>showNotification()</code> and which are asynchronous helpers like <code>showNotificationWithTimeout()</code>. You have to use them differently and be careful not to mistake them with each other.</p>

<p>This was the motivation for <strong>finding a way to “legitimize” this pattern of providing <code>dispatch</code> to a helper function, and help Redux “see” such asynchronous action creators as a special case of normal action creators</strong> rather than totally different functions.</p>

<p>If you’re still with us and you also recognize as a problem in your app, you are welcome to use the <a href="http://github.com/gaearon/redux-thunk" target="_blank">Redux Thunk</a> middleware.</p>

<p>In a gist, Redux Thunk teaches Redux to recognize special kinds of actions that are in fact functions:</p>

<pre><code>import { createStore, applyMiddleware } from 'redux'
import thunk from 'redux-thunk'

const store = createStore(
  reducer,
  applyMiddleware(thunk)
)

// It still recognizes plain object actions
store.dispatch({ type: 'INCREMENT' })

// But with thunk middleware, it also recognizes functions
store.dispatch(function (dispatch) {
  // ... which themselves may dispatch many times
  dispatch({ type: 'INCREMENT' })
  dispatch({ type: 'INCREMENT' })
  dispatch({ type: 'INCREMENT' })

  setTimeout(() =&gt; {
    // ... even asynchronously!
    dispatch({ type: 'DECREMENT' })
  }, 1000)
})</code></pre>

<p>When this middleware is enabled, <strong>if you dispatch a function</strong>, Redux Thunk middleware will give it <code>dispatch</code> as an argument. It will also “swallow” such actions so don’t worry about your reducers receiving weird function arguments. Your reducers will only receive plain object actions—either emitted directly, or emitted by the functions as we just described.</p>

<p>This does not look very useful, does it? Not in this particular situation. However it lets us declare <code>showNotificationWithTimeout()</code> as a regular Redux action creator:</p>

<pre><code>// actions.js
function showNotification(id, text) {
  return { type: 'SHOW_NOTIFICATION', id, text }
}
function hideNotification(id) {
  return { type: 'HIDE_NOTIFICATION', id }
}

let nextNotificationId = 0
export function showNotificationWithTimeout(text) {
  return function (dispatch) {
    const id = nextNotificationId++
    dispatch(showNotification(id, text))

    setTimeout(() =&gt; {
      dispatch(hideNotification(id))
    }, 5000)
  }
}</code></pre>

<p>Note how the function is almost identical to the one we wrote in the previous section. However it doesn’t accept <code>dispatch</code> as the first argument. Instead it <em>returns</em> a function that accepts <code>dispatch</code> as the first argument.</p>

<p>How would we use it in our component? Definitely, we could write this:</p>

<pre><code>// component.js
showNotificationWithTimeout('You just logged in.')(this.props.dispatch)</code></pre>

<p>We are calling the async action creator to get the inner function that wants just <code>dispatch</code>, and then we pass <code>dispatch</code>.</p>

<p>However this is even more awkward than the original version! Why did we even go that way?</p>

<p>Because of what I told you before. <strong>If Redux Thunk middleware is enabled, any time you attempt to dispatch a function instead of an action object, the middleware will call that function with <code>dispatch</code> method itself as the first argument</strong>.</p>

<p>So we can do this instead:</p>

<pre><code>// component.js
this.props.dispatch(showNotificationWithTimeout('You just logged in.'))</code></pre>

<p>Finally, dispatching an asynchronous action (really, a series of actions) looks no different than dispatching a single action synchronously to the component. Which is good because components shouldn’t care whether something happens synchronously or asynchronously. We just abstracted that away.</p>

<p>Notice that since we “taught” Redux to recognize such “special” action creators (we call them <a href="https://en.wikipedia.org/wiki/Thunk" target="_blank">thunk</a> action creators), we can now use them in any place where we would use regular action creators. For example, we can use them with <code>connect()</code>:</p>

<pre><code>// actions.js

function showNotification(id, text) {
  return { type: 'SHOW_NOTIFICATION', id, text }
}
function hideNotification(id) {
  return { type: 'HIDE_NOTIFICATION', id }
}

let nextNotificationId = 0
export function showNotificationWithTimeout(text) {
  return function (dispatch) {
    const id = nextNotificationId++
    dispatch(showNotification(id, text))

    setTimeout(() =&gt; {
      dispatch(hideNotification(id))
    }, 5000)
  }
}

// component.js

import { connect } from 'react-redux'

// ...

this.props.showNotificationWithTimeout('You just logged in.')

// ...

export default connect(
  mapStateToProps,
  { showNotificationWithTimeout }
)(MyComponent)</code></pre>

<h2>Reading State in Thunks</h2>

<p>Usually your reducers contain the business logic for determining the next state. However, reducers only kick in after the actions are dispatched. What if you have a side effect (such as calling an API) in a thunk action creator, and you want to prevent it under some condition?</p>

<p>Without using the thunk middleware, you’d just do this check inside the component:</p>

<pre><code>// component.js
if (this.props.areNotificationsEnabled) {
  showNotificationWithTimeout(this.props.dispatch, 'You just logged in.')
}</code></pre>

<p>However, the point of extracting an action creator was to centralize this repetitive logic across many components. Fortunately, Redux Thunk offers you a way to <em>read</em> the current state of the Redux store. In addition to <code>dispatch</code>, it also passes <code>getState</code> as the second argument to the function you return from your thunk action creator. This lets the thunk read the current state of the store.</p>

<pre><code>let nextNotificationId = 0
export function showNotificationWithTimeout(text) {
  return function (dispatch, getState) {
    // Unlike in a regular action creator, we can exit early in a thunk
    // Redux doesn’t care about its return value (or lack of it)
    if (!getState().areNotificationsEnabled) {
      return
    }

    const id = nextNotificationId++
    dispatch(showNotification(id, text))

    setTimeout(() =&gt; {
      dispatch(hideNotification(id))
    }, 5000)
  }
}</code></pre>

<p>Don’t abuse this pattern. It is good for bailing out of API calls when there is cached data available, but it is not a very good foundation to build your business logic upon. If you use <code>getState()</code> only to conditionally dispatch different actions, consider putting the business logic into the reducers instead.</p>

<h2>Next Steps</h2>

<p>Now that you have a basic intuition about how thunks work, check out Redux <a href="http://redux.js.org/docs/introduction/Examples.html#async" target="_blank">async example</a> which uses them.</p>

<p>You may find many examples in which thunks return Promises. This is not required but can be very convenient. Redux doesn’t care what you return from a thunk, but it gives you its return value from <code>dispatch()</code>. This is why you can return a Promise from a thunk and wait for it to complete by calling <code>dispatch(someThunkReturningPromise()).then(...)</code>.</p>

<p>You may also split complex thunk action creators into several smaller thunk action creators. The <code>dispatch</code> method provided by thunks can accept thunks itself, so you can apply the pattern recursively. Again, this works best with Promises because you can implement asynchronous control flow on top of that.</p>

<p>For some apps, you may find yourself in a situation where your asynchronous control flow requirements are too complex to be expressed with thunks. For example, retrying failed requests, reauthorization flow with tokens, or a step-by-step onboarding can be too verbose and error-prone when written this way. In this case, you might want to look at more advanced asynchronous control flow solutions such as <a href="https://github.com/yelouafi/redux-saga" target="_blank">Redux Saga</a> or <a href="https://github.com/raisemarketplace/redux-loop" target="_blank">Redux Loop</a>. Evaluate them, compare the examples relevant to your needs, and pick the one you like the most.</p>

<p>Finally, don’t use anything (including thunks) if you don’t have the genuine need for them. Remember that, depending on the requirements, your solution might look as simple as</p>

<pre><code>store.dispatch({ type: 'SHOW_NOTIFICATION', text: 'You logged in.' })
setTimeout(() =&gt; {
  store.dispatch({ type: 'HIDE_NOTIFICATION' })
}, 5000)</code></pre>

<p>Don’t sweat it unless you know why you’re doing this.</p>
    
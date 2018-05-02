<a href="https://stackoverflow.com/questions/35530547/async-actions-in-redux">https://stackoverflow.com/questions/35530547/async-actions-in-redux</a><div id="articleHeader"><h1>Async actions in Redux</h1></div>

<p>I have a React App, I need to make an ajax call (in order to learn) to a online service (async) with Redux.</p>

<p>This is my store:</p>

<pre><code>import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import duedates from './reducers/duedates'


export default applyMiddleware(thunk)(createStore)(duedates);</code></pre>

<p>This is the actions:</p>

<pre><code>import rest from '../Utils/rest';

export function getDueDatesOptimistic(dueDates){
    console.log("FINISH FETCH");
    console.log(dueDates);
    return {
        type: 'getDueDate',
        dueDates
    }
}

export function waiting() {
    console.log("IN WAIT");
    return {
        type: 'waiting'
    }
}


function fetchDueDates() {
    console.log("IN FETCH");
    return rest({method: 'GET', path: '/api/dueDates'});
}

export function getDueDates(dispatch) {
    console.log("IN ACTION");
    return fetchDueDates().done(
        dueDates =&gt; dispatch(getDueDatesOptimistic(dueDates.entity._embedded.dueDates))
    )
}</code></pre>

<p>And this is the reducer:</p>

<pre><code>export default (state = {}, action) =&gt; {
  switch(action.type) {
    case 'getDueDate':
        console.log("IN REDUCER")

        return state.dueDates = action.dueDates;
    default:
        return state
  }
}</code></pre>

<p>I dont get what I'm doing wrong. The action is being called perfectly from the component. But then I get this error:</p>

<blockquote>
  <p>Error: Actions must be plain objects. Use custom middleware for async actions.</p>
</blockquote>

<p>I guess I'm using wrong the react-thunk middleware.
What am I doing wrong?</p>

<p><strong>EDIT</strong></p>

<p>Now the action is calling to the reducer, but the reducer, after changing state, is not re-running the render method</p>

<pre><code>    case 'getDueDate':
        console.log("IN REDUCER")

        return state.dueDates = action.dueDates;</code></pre>
    
<a href="https://www.reddit.com/r/reactjs/comments/6djrgz/what_is_the_exact_usage_of_subscribe_from_redux/">https://www.reddit.com/r/reactjs/comments/6djrgz/what_is_the_exact_usage_of_subscribe_from_redux/</a><div id="articleHeader"><h1>what is the exact usage of subscribe from redux?：reactjs</h1></div><p>So,  when you're subscribe with redux youre basically creating an event-listener for changes. Redux at it core is basically just a huge event emitter that observes state and will call user created call backs whenever the user tells it the state has changed. </p>

<p>The way the user tells the store that the state has changed is by using dispatch. Dispatch functions take an action parameter,  as I'm sure you're familiar with, which is normally a pure function that represents how the state will change. Which dispatch happens, the reducer function used to create the store (your root reducer) will be called with the current state tree and the action and it will return the next state I'm the tree and notify the change listeners. </p>

<p>This is where we start to see things unfold. When you subscribe to the store,  the subscribe function actually takes a callback function called listener. This callback will be invoked everytime that dispatch is called,  so now you can see how this flow starts to fit together. </p>

<p>You create the store with your root reducer. The store keeps an index of active change listeners. </p>

<p>You then subscribe to the store, which listens for changes. Whenever you call dispatch the store realizes that their needs to be a change. </p>

<p>The action you dispatched gets passed to the reducer to create the next  state.  When the state has updated, the subscribe function actually then returns a callback that removes this listener from the stores indexed listeners. So in a round about,  not 100% technically correct way,  the subscribe function listens to your action, and then the store will use these active listener callbacks to update to the next state with the reducer, then all changes are done and the subscribe function removes the active listener. </p>

<p>I hope this helps a bit </p>

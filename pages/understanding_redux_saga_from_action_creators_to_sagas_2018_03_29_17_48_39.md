<a href="https://blog.logrocket.com/understanding-redux-saga-from-action-creators-to-sagas-2587298b5e71">https://blog.logrocket.com/understanding-redux-saga-from-action-creators-to-sagas-2587298b5e71</a><div id="articleHeader"><h1>Understanding redux-saga: From action creators to sagas</h1></div><figure id="43ab"><div><div><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/1*tRxcPS10RsKHLVND-rNCWw.jpeg" /></div></figure><p id="aac8">As any redux developer could tell you, the hardest part of building an app are asynchronous calls — how do you handle network requests, timeouts, and other callbacks without complicating the redux actions and reducers?</p><p id="f038">To manage this complexity, I’ll describe a few different approaches for handling asynchronicity in your app, ranging from simple approaches like redux-thunk, to more full-featured libraries like redux-saga.</p><p id="2b26">We are going to use React and Redux, so this post assumes you have at least a passing familiarity with how they work.</p></section><h3 id="4f1d">Action creators</h3><p id="4ad2">Calling an API is a common requirement in many apps. Imagine we need to show a random picture of a dog when we click a button:</p><figure id="0648"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*PlnXr-N-xMlk0sHb1shPOg.gif?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/1*PlnXr-N-xMlk0sHb1shPOg.gif" /></div></div></div></figure><p id="af31">We can use the <a href="https://www.google.com/url?q=https://dog.ceo/dog-api/&sa=D&ust=1507757792415000&usg=AFQjCNEiK8rhUGBOYrTEyBlLh86e_zpFfQ" target="_blank">Dog CEO API</a> and something as simple as a <a href="https://www.google.com/url?q=https://developers.google.com/web/updates/2015/03/introduction-to-fetch&sa=D&ust=1507757792416000&usg=AFQjCNF04-VM6izV6127LPv8siI0TEp8JA" target="_blank">fetch</a> call inside of an action creator:</p><figure id="7e7f"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Fwww.gravatar.com%2Favatar%2F0ca97e4de56c3b7beeae6546e4d74ab5%2F%3Fdefault%3D%26s%3D80&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></div></figure><p id="2e0b"><a href="https://jsfiddle.net/eh3rrera/utwt4dr8/" target="_blank">https://jsfiddle.net/eh3rrera/utwt4dr8/</a></p><p id="2bec">There is nothing wrong with this approach. All things being equal, we should go for the simplest approach.</p><p id="bec1">However, using Redux alone won’t give us much flexibility. At its core, Redux is only a state container that supports synchronous data flows.</p><p id="5d3e">Every time an action, a plain object that describes what happened, is sent to the store, a reducer is called and the state is updated immediately.</p><p id="d5c6">But in an asynchronous flow, you have to wait for the response first, and then, if there’s no error, update the state. And what if your application has a complex logic/workflow?</p><p id="64fa">Redux use middlewares to solve this problem. A middleware is a piece of code that is executed after an action is dispatched but before reaching the reducer.</p><p id="2fdc">Many middlewares can be arranged into a chain of execution to process the action in different ways. However, the middleware has to interpret anything you pass to it, and it must make sure to dispatch a plain object (an action) at the end of the chain.</p><p id="8d84">For asynchronous operations, Redux offers the <a href="https://www.google.com/url?q=https://github.com/gaearon/redux-thunk&sa=D&ust=1507757792417000&usg=AFQjCNFlksgie7cnqh-wqtANFV5xW4V8nw" target="_blank">redux-thunk</a> middleware.</p><h3 id="ea20">Redux-thunk</h3><p id="a53f">Redux-thunk is the standard way of performing asynchronous operations in Redux.</p><p id="4514">For our purposes, a thunk represents a function that is not called immediately, only when needed. Take the example from <a href="https://www.google.com/url?q=https://github.com/gaearon/redux-thunk%23whats-a-thunk&sa=D&ust=1507757792417000&usg=AFQjCNHQ1KDwcPfSyxNqErykWK-7tIb3Kw" target="_blank">redux-thunk’s documentation</a>:</p><figure id="9ebb"><div><img src="https://cdn-images-1.medium.com/max/1600/1*X1uOF_88PJiNdgCMo6I_jA.png" /></div></figure><p id="fb68">The value <em>3</em> is assigned immediately to <em>x</em>.</p><p id="1b8c">However, when we have something like the following statement:</p><figure id="015e"><div><img src="https://cdn-images-1.medium.com/max/1600/1*djrq3Jd0QLOZzvE6t8HtmQ.png" /></div></figure><p id="c683">The sum operation is not executed immediately, only when you call <em>foo()</em>. This makes <em>foo </em>a thunk.</p><p id="5205">Redux-thunk allows an action creator to dispatch a function in addition to a plain object, converting the action creator into a thunk.</p><p id="4720">This is how our previous example looks using redux-thunk:</p><figure id="9d9e"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Fwww.gravatar.com%2Favatar%2F0ca97e4de56c3b7beeae6546e4d74ab5%2F%3Fdefault%3D%26s%3D80&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></div></figure><p id="8ae5"><a href="https://jsfiddle.net/eh3rrera/0s7b54n4/" target="_blank">https://jsfiddle.net/eh3rrera/0s7b54n4/</a></p><p id="58dd">At first look, this might not seem too different than the previous approach.</p><p id="0419">Without redux-thunk:</p><figure id="9545"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*MsQvkptB793NoYer9xLiBg.png?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/1*MsQvkptB793NoYer9xLiBg.png" /></div></div></div></figure><p id="aa1c">With redux-thunk:</p><figure id="36c3"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*WXrNLK-VHRSd3-K8HlIvRA.png?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1600/1*WXrNLK-VHRSd3-K8HlIvRA.png" /></div><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/2000/1*WXrNLK-VHRSd3-K8HlIvRA.png" /></div></div></div></figure><p id="81f5">The advantage of using redux-thunk is that the component doesn’t know that it is executing an asynchronous action.</p><p id="8015">Since the middleware automatically passes the <em>dispatch</em> function to the function that the action creator returns, for the component, there will be no difference between asking to perform a synchronous and an asynchronous action (and they don’t have to care anyway).</p><p id="e2d9">By using a middleware, we have added a <a href="https://www.google.com/url?q=https://en.wikipedia.org/wiki/Fundamental_theorem_of_software_engineering&sa=D&ust=1507757792423000&usg=AFQjCNH1AFRkoFdvuD8Gi1p7xAwZsZM4Zw" target="_blank">layer of indirection</a> that gives us more flexibility.</p><p id="8af3">Since redux-thunk gives to the dispatched function the <em>dispatch </em>and <em>getState </em>methods from the store as parameters, you can also dispatch other actions and read the state to implement more complex business logic and workflows.</p><p id="7535">Another benefit is that if there’s something that is too complex to be expressed with thunks, without changing the component, we can use another middleware library to have more control.</p><p id="0c6c">Let’s see how to replace redux-thunk with a library that can give us more control, <a href="https://www.google.com/url?q=https://redux-saga.js.org/&sa=D&ust=1507757792423000&usg=AFQjCNGoORPY8cxpcgtypkuWNiEJyg7TeQ" target="_blank">redux-saga</a>.</p><h3 id="dab7">Redux-saga</h3><p id="80c6">Redux-saga is <a href="https://www.google.com/url?q=https://github.com/redux-saga/redux-saga&sa=D&ust=1507757792424000&usg=AFQjCNEYddF5eevgabzuSB6t9EBRAWQsaw" target="_blank">a library</a> that aims to make side effects easier and better by working with sagas.</p><p id="6704">Sagas are a design pattern that comes from the distributed transactions world, where a saga manages processes that need to be executed in a transactional way, keeping the state of the execution and compensating failed processes.</p><p id="4df6">To learn more about sagas, start by watching <a href="https://www.google.com/url?q=https://twitter.com/caitie?lang%3Den&sa=D&ust=1507757792425000&usg=AFQjCNFeGaOiyq-snfyHAoG7_SMST_szgQ" target="_blank">Caitie McCaffrey’s</a> <a href="https://www.google.com/url?q=https://www.youtube.com/watch?v%3DxDuwrtwYHu8&sa=D&ust=1507757792425000&usg=AFQjCNFQOP4vTrCb1dtxZT0n_gA_tFDHoQ" target="_blank">Applying the Saga Pattern</a>. If you’re feeling ambitious, <a href="https://www.google.com/url?q=http://citeseerx.ist.psu.edu/viewdoc/download?doi%3D10.1.1.93.7258%26rep%3Drep1%26type%3Dpdf&sa=D&ust=1507757792426000&usg=AFQjCNG-jtTMj7F7oddUpO9Jr6so-JuFnQ" target="_blank">the paper</a> that first defined sagas in relation to distributed systems.</p><p id="477d">In the context of Redux, a saga is implemented as a middleware (we can’t use a reducer because this must be a pure function) to coordinate and trigger asynchronous actions (side-effects).</p><p id="cf1e">Redux-saga does this with the help of <a href="https://www.google.com/url?q=https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*&sa=D&ust=1507757792427000&usg=AFQjCNEgLx9YmBNg9rzNXzCKVhdbELhgtA" target="_blank">ES6 generators</a>:</p><figure id="0ee3"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*zt6M4K2tuSR7Ta6I-MX1Sg.png?q=20" /><div class="readableLargeImageContainer"><img /></div></div></div></figure><p id="87ee">Generators are functions that can be paused and resumed, instead of executing all the statements of the function in one pass.</p><p id="37ba">When you invoke a generator function, it will return an iterator object. With each call of the iterator’s <em>next()</em> method, the generator’s body will be executed until the next <em>yield</em> statement and then pause:</p><figure id="f06c"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*YCqSqdwN1RoYc66EMBtzKQ.png?q=20" /><div class="readableLargeImageContainer"><img /></div></div></div></figure><p id="6e33">This can make asynchronous code easy to write and understand. For example, instead of doing this:</p><figure id="465e"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*cSsNYk0MYw9lDSaSW8S7HA.png?q=20" /><div class="readableLargeImageContainer"><img /></div></div></div></figure><p id="8bdc">With generators, we could do this:</p><figure id="fa50"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*vWsBLfL87JZaEYMx3pZZXA.png?q=20" /><img /></div></div></figure><p id="e43d">Back to redux-saga, we generally have a saga whose job is to watch for dispatched actions:</p><figure id="89cf"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*2T0gXE0qN8klIYaSIm9xZQ.png?q=20" /><img /></div></div></figure><p id="4219">To coordinate the logic we want to implement inside the saga, we can use a helper function like <a href="https://www.google.com/url?q=https://redux-saga.js.org/docs/api/%23takeeverypattern-saga-args&sa=D&ust=1507757792431000&usg=AFQjCNGVN_8Gok4Xtqz27qvg7i638H73Pw" target="_blank">takeEvery</a> to spawn a new saga to perform an operation:</p><figure id="7b06"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*jk0J1E5I0B4NxxYaoWkPtA.png?q=20" /><div class="readableLargeImageContainer"><img /></div></div></div></figure><p id="42ee">If there are multiple requests, <em>takeEvery </em>will start multiple instances of the worker saga. In other words, it handles concurrency for you.</p><p id="891f">Notice that the watcher saga is another layer of indirection that gives more flexibility to implement complex logic (but may be unnecessary for simple apps).</p><p id="ac36">Now, we could implement the <em>fetchDogAsync()</em> function with something like this (assuming we had access to the <em>dispatch </em>method):</p><figure id="b870"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*ZMz70Ny3LD4aXpqEOodbpw.png?q=20" /><div class="readableLargeImageContainer"><img /></div></div></div></figure><p id="8bea">But redux-saga allows us to yield an object that declares our intention to perform an operation rather than yielding the result of executing the operation itself. In other words, the above example is implemented in redux-saga in this way:</p><figure id="fd37"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*fDjxvb2y-29glXfUIpekzA.png?q=20" /><div class="readableLargeImageContainer"><img /></div></div></div></figure><p id="918e">Instead of invoking the asynchronous request directly, the method <em>call</em> will return only a plain object describing the operation so redux-saga can take care of the invocation and returns the result to the generator.</p><p id="f6dd">The same thing happens with the <em>put</em> method. Instead of dispatching an action inside the generator, <em>put</em> returns an object with instructions for the middleware to dispatch the action.</p><p id="f179">Those returned objects are called <em>Effects</em>. Here’s an example of the effect returned by the <em>call </em>method:</p><figure id="797b"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*TiZp6XcQBQf_BpH5GJ6ZCQ.png?q=20" /><div class="readableLargeImageContainer"><img /></div></div></div></figure><p id="ad8f">By working with Effects, redux-saga makes sagas <a href="https://www.google.com/url?q=https://en.wikipedia.org/wiki/Declarative_programming&sa=D&ust=1507757792437000&usg=AFQjCNGwD95iE_VajquduwLdJJrpG-8pmw" target="_blank">declarative </a>rather than <a href="https://www.google.com/url?q=https://en.wikipedia.org/wiki/Imperative_programming&sa=D&ust=1507757792437000&usg=AFQjCNE5yGqcv_YCTZ0KlgJuC8fl9vNkSQ" target="_blank">imperative</a>.</p><p id="72e1">Declarative programming is a programming style that attempts to minimize or eliminate side effects by describing <em>what </em>the program must accomplish instead of describing <em>how </em>to accomplish it.</p><p id="c58b">The benefit this brings, and which most people talked about, is that a function that returns a simple object is easier to test than a function that directly makes an asynchronous call. To run the test, you don’t need to use the real API, fake it, or mock it.</p><p id="a7cc">For testing, you just iterate over the generator function, asserting for equality on the values yielded:</p><figure id="f7b5"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/60/1*fcus3p8S2BSNc32x9851Ig.png?q=20" /><div class="readableLargeImageContainer"><img /></div></div></div></figure><p id="c6b9">However, another added benefit is the ability to easily compose many effects into a complex workflow.</p><p id="8086">In addition to <a href="https://www.google.com/url?q=https://redux-saga.js.org/docs/api/%23takeeverypattern-saga-args&sa=D&ust=1507757792439000&usg=AFQjCNGy0BxNH77K16u84KJ4wTZmeIro-g" target="_blank">takeEvery</a>, <a href="https://www.google.com/url?q=https://redux-saga.js.org/docs/api/%23callfn-args&sa=D&ust=1507757792439000&usg=AFQjCNEOsn_lPUcQO0JZhEcMWwBjaaZifw" target="_blank">call</a>, and <a href="https://www.google.com/url?q=https://redux-saga.js.org/docs/api/%23putaction&sa=D&ust=1507757792440000&usg=AFQjCNGDgc8EL0DvBquIddYqw87K7rsGMA" target="_blank">put</a>, redux-saga offers a lot of <a href="https://www.google.com/url?q=https://redux-saga.js.org/docs/api/%23effect-creators&sa=D&ust=1507757792440000&usg=AFQjCNH7YRr6afgEwo8pUTBPTdtDTDGhEQ" target="_blank">effect creators</a> for <a href="https://www.google.com/url?q=https://redux-saga.js.org/docs/recipes/%23throttling&sa=D&ust=1507757792440000&usg=AFQjCNFZ0iAd_uzMv0YtijRP5YmqTRZdSw" target="_blank">throttling</a>, <a href="https://www.google.com/url?q=https://redux-saga.js.org/docs/advanced/FutureActions.html%23a-simple-logger&sa=D&ust=1507757792441000&usg=AFQjCNEkrqnboPHh98SNKkuskkgpnnqQcg" target="_blank">getting the current state</a>, <a href="https://www.google.com/url?q=https://redux-saga.js.org/docs/advanced/RunningTasksInParallel.html&sa=D&ust=1507757792441000&usg=AFQjCNHWJN4PCvINxRHIUKYqPQpzhuRKMQ" target="_blank">running tasks in parallel</a>, and <a href="https://www.google.com/url?q=https://redux-saga.js.org/docs/advanced/TaskCancellation.html&sa=D&ust=1507757792441000&usg=AFQjCNHzPzL-PKv5uNWCKHevmza7mKtn-g" target="_blank">cancel tasks</a>, just to mention a few.</p><p id="4c07">Back to our trivia example, this is the complete implementation in redux-saga:</p><figure id="08e2"><div><div><img src="https://i.embed.ly/1/display/resize?url=https%3A%2F%2Fwww.gravatar.com%2Favatar%2F0ca97e4de56c3b7beeae6546e4d74ab5%2F%3Fdefault%3D%26s%3D80&key=a19fcc184b9711e1b4764040d3dc5c07&width=40" /></div></div></figure><p id="9dac"><a href="https://jsfiddle.net/eh3rrera/qu42h5ee/" target="_blank">https://jsfiddle.net/eh3rrera/qu42h5ee/</a></p><p id="c8be">When you click the button, this is what happens:</p><ol><li id="2689">The action FETCHED_DOG is dispatched</li><li id="c032">The watcher saga (<em>watchFetchDog</em>) takes the dispatched action and calls the worker saga (<em>fetchDogAsync</em>)</li><li id="0b70">The action to show the loading indicator is dispatched</li><li id="d9b1">The API call is executed</li><li id="922a">An action to update the state is dispatched (success or fail)</li></ol><p id="9997">If you believe some layers of indirection and a little bit of additional work is worth it, redux-saga can give you more control to handle side-effects in a functional way.</p><h3 id="5167">Conclusion</h3><p id="1094">This post has shown how to implement an asynchronous operation in Redux with action creators, thunks, and sagas, going from the simplest approach to the most complex.</p><p id="118e">Redux doesn’t prescribe a solution for handling side-effects. When deciding which approach to take, you have to consider the complexity of your application. My recommendation is starting with the simplest solution.</p><p id="cef7">There are other alternatives to redux-saga that are worth trying. Two of the most popular options are <a href="https://www.google.com/url?q=https://github.com/redux-observable/redux-observable&sa=D&ust=1507757792443000&usg=AFQjCNGqSb17q-9KpopVfNL86y37prAzaw" target="_blank">redux-observable</a> (based on <a href="https://www.google.com/url?q=https://github.com/ReactiveX/rxjs&sa=D&ust=1507757792443000&usg=AFQjCNEXx9h3ECg6vkCOQSYgYPrhf3yGJg" target="_blank">RxJS</a>) and <a href="https://www.google.com/url?q=https://github.com/jeffbski/redux-logic&sa=D&ust=1507757792443000&usg=AFQjCNG9lbIwvmnqqIhvh-gotydQZd6y4A" target="_blank">redux-logic</a> (also based on RxJS observables but with the freedom to write your logic in <a href="https://www.google.com/url?q=https://github.com/jeffbski/redux-logic%23tldr&sa=D&ust=1507757792444000&usg=AFQjCNHSDD8tO1eSiH0CSivDIIqUQ5d23Q" target="_blank">other styles</a>).</p>
<a href="https://news.ycombinator.com/item?id=14859206">https://news.ycombinator.com/item?id=14859206</a><div id="articleHeader"><h1>Show HN: Kea – The power of Redux with the simplicity of MobX</h1></div><table id="hnmain">
        <tbody>
<tr><td>
  <table>
            <tbody><tr id="14859705"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Looks pretty neat. My initial reactions:<p>- I don't like the `@kea(...` because it's another bit of JS syntax I hadn't heard of before. Though I do like decorators in Python, I just feel like I have learned enough of JS syntax to be productive and they seem to keep adding unnecessary stuff.</p><p>- There is still duplication between the action names and the reducers. When using Redux I now always use these two functions:</p><pre><code>    function makeReducer(reducerObject) {
      return (state, action) =&gt; {
        if (Object.keys(reducerObject).includes(action.type)) {
          return reducerObject[action.type](state, action.value)
        }
        return state
      }
    }
    
    function makeActions(reducerObject) {
      const actions = {}
      Object.keys(reducerObject).forEach(name =&gt; {
        actions[name] = value =&gt; {
          return {type: name, value}
        }
      })
      return actions
    }
</code></pre>
So I can just declare a single object of reducers and can infer the action names and creators from that e.g.<pre><code>   const reducerObject = {
      increment(state, value) {
         return state + 1
      },
      decrement(state, value) {
         return state - 1
      }
   }
 
   const reducer = makeReducer(reducerObject)
   const actions = makeActions(reducerObject)</code></pre>
              </div></td></tr>
      </tbody></table></td></tr>
        <tr id="14859794"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  &gt;- I don't like the `@kea(...` because it's another bit of JS syntax I hadn't heard of before, though I do like decorators in Python.<p>You can just not use the @ syntax for decorators and instead just do it manually like so:</p><pre><code>    class Counter extends Component {
        ...
    }

    Counter = kea(...)(Counter);

    export default Counter;</code></pre>
              </div></td></tr>
      </tbody></table></td></tr>
    <tr id="14859883"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I'm a big fan of decorators, but it seems like much of the React/Redux world is overly class-decorator happy. It's really common to define properties in a decorator which would be much easier to read, IMO, as static or instance properties. I'd rather read something more like this:<pre><code>    @kea // kicks off the meta-programming to read the statics below
    export default class Counter extends Component {
      static actions = {
        increment: (amount) =&gt; ({ amount }),
        decrement: (amount) =&gt; ({ amount }),
      };

      static reducers = {
        counter: [0, PropTypes.number, {
          [this.actions.increment]: (state, payload) =&gt; state + payload.amount,
          [this.actions.decrement]: (state, payload) =&gt; state - payload.amount
        }],
      };

      static selectors = ({ selectors }) =&gt; ({
        doubleCounter: [
          () =&gt; [selectors.counter],
          (counter) =&gt; counter * 2,
          PropTypes.number,
        ],
      });

      render () {
        const { counter, doubleCounter } = this.props
        const { increment, decrement } = this.constructor.actions

        return (
          &lt;div className='kea-counter'&gt;
            Count: {counter}&lt;br /&gt;
            Doublecount: {doubleCounter}&lt;br /&gt;
            &lt;button onClick={() =&gt; increment(1)}&gt;Increment&lt;/button&gt;
            &lt;button onClick={() =&gt; decrement(1)}&gt;Decrement&lt;/button&gt;
          &lt;/div&gt;
        )
      }
    }</code></pre>
              </div></td></tr>
      </tbody></table></td></tr>
        <tr id="14859938"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Hey, thanks for the feedback! This is definitely something to think about, as nothing in the syntax of kea is set in stone.<p>That said, the magic with having a big options hash in the `@kea({})` call itself is that then you can easily disconnect the logic from your components as your application grows. Here's more information about this: <a href="https://kea.js.org/guide/connected" target="_blank">https://kea.js.org/guide/connected</a></p><p>Also, I'm not sure you can do `this.actions` inside a static variable, but I understand the point that you were trying to make.
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14860082"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  &gt; That said, the magic with having a big options hash in the `@kea({})` call itself is that then you can easily disconnect the logic from your components as your application grows. Here's more information about this: <a href="https://kea.js.org/guide/connected" target="_blank">https://kea.js.org/guide/connected</a><p>Interesting. I still think these are better modeled (and read) as part of the class declaration. You can do the same thing with mixins:</p><p>Transforming that example:</p><pre><code>    import FeaturesLogic from '../features-logic.js';

    @kea
    class CounterExampleScene extends FeaturesLogic(Component) {
      // no change here
    }
</code></pre>
Where FeaturesLogic is a JS class mixin: <a href="http://justinfagnani.com/2015/12/21/real-mixins-with-javascript-classes/" target="_blank">http://justinfagnani.com/2015/12/21/real-mixins-with-javascr...</a><pre><code>    export const FeaturesLogic = (base) =&gt; class extends base {
      static actions = ...;
    }
</code></pre>
&gt; Also, I'm not sure you can do `this.actions` inside a static variable, but I understand the point that you were trying to make.<p>Not in the current Babel transform, but I thought it may be in the latest unified class fields proposal. I'm digging for it...
              </p></div></td></tr>
      </tbody></table></td></tr>
      <tr id="14860155"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  It's worth noting that both the React and Redux teams generally discourage the use of decorators.  Quoting the Create-React-App README:<p>&gt; Create React App doesn’t support decorator syntax at the moment because:</p><p>&gt; - It is an experimental proposal and is subject to change.</p><p>&gt; - The current specification version is not officially supported by Babel.</p><p>&gt; - If the specification changes, we won’t be able to write a codemod because we don’t use them internally at Facebook.</p><p>&gt; Create React App will add decorator support when the specification advances to a stable stage.</p><p>In addition, use of the React-Redux `connect` method as a decorator can lead to unexpected behavior, such as `defaultProps` applying to the generated wrapper component instead of the underlying "plain" component.  I'm not sure how the `kea` decorator handles that sort of thing.
              </p></div></td></tr>
      </tbody></table></td></tr>
      <tr id="14859904"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Hey,
1) As munchor pointed out, you don't need to use the decorators. See the "what is this @kea()" button in the first guide for more details: <a href="https://kea.js.org/guide/counter" target="_blank">https://kea.js.org/guide/counter</a><p>2) Indeed there is duplication between action names and the reducers. This however makes it so that you can have many reducers listening to the same actions. E.g. setting `isLoading` to `false` when `actions.resultsFetched` occurs.
              </p></div></td></tr>
      </tbody></table></td></tr>
    <tr id="14861973"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  In my experience action creators and actions in the reducer don't necessarily map 1 to 1, and often don't. I think of action creators as the API to the reducer. This makes a lot more sense when using redux-thunk and similar, of course.
              </div></td></tr>
      </tbody></table></td></tr>
    <tr id="14860360"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Thanks for sharing those functions. Definitely cuts down on a lot of the boilerplate I see with Redux.
              </div></td></tr>
      </tbody></table></td></tr>
        <tr id="14860431"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Also worth noting that the Redux docs _specifically_ have a section called "Reducing Boilerplate" [0] that shows how to write functions like this, and my Redux addons catalog [1] lists dozens of such libraries already.<p>As I've said many times: it's entirely up to you how much abstraction you want to apply on top of Redux.</p><p>[0] <a href="http://redux.js.org/docs/recipes/ReducingBoilerplate.html" target="_blank">http://redux.js.org/docs/recipes/ReducingBoilerplate.html</a></p><p>[1] <a href="https://github.com/markerikson/redux-ecosystem-links" target="_blank">https://github.com/markerikson/redux-ecosystem-links</a>
              </p></div></td></tr>
      </tbody></table></td></tr>
                  <tr id="14859653"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I know it's just an example... But the Slider code is ridiculously overwrought.<p>Building this type of image carousel is trivial with just plain HTML+CSS+JS. This example uses "actions", "reducers", "selectors", weird functions from something called "redux-saga/effects", a "promise-based timeout" library AND generator functions to produce the magic ... of switching between images.</p><p>If someone I work with came up with this code, I would assume that the person is extremely bored with her job and wants to spruce up her résumé with buzzwords.
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14859736"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I can't really speak for the Kea library directly, but the patterns used in React/Redux land are most valuable in large, evolving projects spanning many developers. Such benefits are therefore subtle and difficult to illustrate with concise examples.<p>It's easy to dismiss these things as "buzzword" soup when the examples are trivial for illustrative purposes, but having <i>real</i> experience employing these patterns at scale is extremely valuable in the real world.
              </p></div></td></tr>
      </tbody></table></td></tr>
    <tr id="14859966"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Hey, indeed it's an example, as you point out. This was the best example I could come up with that demonstrated most of the functionality available, yet remained rather small in size.<p>The point was to show what this library is capable of, so that people with the imagination of your imaginary co-worker could extrapolate its usefulness to real world applications.</p><p>I have built 3 large applications using kea, and at that scale all these features come in handy.
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14860987"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Just to clarify, I'm not picking on you; I realize it's hard to come up with meaningful examples.<p>The problem with Slider is that it doesn't readily extrapolate into anything bigger. To put it another way, it's not the embryo of any real world web app.</p><p>I feel this indicates a larger problem with present-day web dev: due to the complexity of client and server stacks, it's really hard to come up with a self-contained example app that makes any sense as a starting point.</p><p>Looking back some 20 years, one could look at the example apps from the Win32, Classic MacOS and OpenStep SDKs, and come out with a solid feel for what it's like to build an app on each platform.</p><p>Today, I could compare the provided examples from twelve different JavaScript frameworks, and I wouldn't feel any closer to understanding their strengths.
              </p></div></td></tr>
      </tbody></table></td></tr>
      <tr id="14860848"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  It's an example. Do you also comment on new programming languages and say "jeez, all that code to say "hello world"!<p>Why the scare quotes around "promise-based timeout" library? I can guess just by looking at the code that it's a Promise wrapper around setTimeout. It makes the example easier to read, since the API is based around promises and not callbacks. It's probably less than 5 lines of code.
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14861028"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  See my other reply below: I feel Slider is not a useful example because it doesn't extrapolate into any kind of real world web app -- which is a problem when this library is about helping you build real world web apps.<p>The scare quotes are because it's hardly a library when it provides less than 5 lines of code, as you noted.
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14861227"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  &gt; The scare quotes are because it's hardly a library when it provides less than 5 lines of code, as you noted.<p>It makes the example easier to read for me, because I can figure out what it does by the context:</p><p>1. It's called "delay"</p><p>2. It's a function that takes 1 parameter, a number</p><p>3. There is a browser API called setTimeout, which takes a function and a number</p><p>4. Converting functions that take a callback to a function that returns a promise is a common pattern.</p><p>I know what delay does without even needing to see it. Maybe if you don't know the 4 things I've listed above, this makes the example harder to read, but then you probably do not need this library.</p><p>&gt; I feel Slider is not a useful example because it doesn't extrapolate into any kind of real world web app -- which is a problem when this library is about helping you build real world web apps.</p><p>It's an example on the homepage, not documentation. How many lines of code do you want to see? I feel like if you assume that the author wrote this to scratch their own itch, then you can use your imagination and assume that they work on apps with complicated state that needs to be persisted over a network, that gets fed to functional components.</p><p>Edit: I read your other comment, and I agree it's really hard to come up with good, non-trivial examples.
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14859751"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  As you indicate, it's just an example. These libraries aren't for building image sliders, they're for building complex applications that you can't easily provide examples for.
              </div></td></tr>
      </tbody></table></td></tr>
                <tr id="14859715"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Shameless plug for another take on the same promise: <a href="https://github.com/jnorth/megalith" target="_blank">https://github.com/jnorth/megalith</a><p>I think most people who are attracted to Redux's core principals but want a more opinionated structure will end up gravitating towards mobx-state-tree though.
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14860108"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  If my favorite part of redux is structuring flows with redux-saga, does mobx-state-tree have a solution for me?<p>For example, this is nice:</p><pre><code>  // On login, spin off the auth process. If an error or a logout happens, clean up.
  // Be sure to cancel any pending auth request! 
  // Then get ready for a new login.

  function* loginFlow() {
    while (true) {
      const {user, password} = yield take('LOGIN_REQUEST')
      const task = yield fork(authorize, user, password)
      const action = yield take(['LOGOUT', 'LOGIN_ERROR'])
      if (action.type === 'LOGOUT')
        yield cancel(task)
      yield call(Api.clearItem, 'token')
    }
  }

</code></pre>
(Genuine question...idk!)
              </div></td></tr>
      </tbody></table></td></tr>
        <tr id="14860297"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  This example doesn't cover all the cases you're showing above, but in megalith or MST you would typically have a clearer separation between the functions that change state and the async communication parts.<p><a href="https://github.com/jnorth/megalith/blob/master/docs/examples/async-actions.md" target="_blank">https://github.com/jnorth/megalith/blob/master/docs/examples...</a></p><p><a href="https://github.com/mobxjs/mobx-state-tree#creating-async-processes" target="_blank">https://github.com/mobxjs/mobx-state-tree#creating-async-pro...</a>
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14860514"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  Yeah, I also like to use redux with a clear separation between actions that change state and those that don't. (For example, reducers only take actions prefixed by DATA_ or UI_, all other actions...the bulk of them really...don't have anything to do with changing state and are handled by other processes. But because of this I don't bother with action creators, so what do I know!)<p>A conceptual appeal of mobx to me is that this distinction seems baked in. The original mobx didn't click with me like redux did ¯\_(ツ)_/¯, but if MST gives transactional updates and support for redux dev tools (right?) could be worth trying.
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14861106"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  Right, maybe I called out the wrong part of your example. redux-saga gives a really elegant way to describe the flow, but I feel at the expense of wrapping the async code with special helpers (call, put, fork, etc). You have to learn a few extra concepts for it to be comfortable. Async code in MST and megalith interact a bit more directly with the stores.<p>One thing I tried to do with megalith is mapping ideas from Redux to built-in language features as much as possible. An action object can trivially be represented as a function call for example—action name and payload is mapped to function name and arguments.</p><p>I think Mobx gets into trouble there by building off of observables—you have to litter your async code with different types of action markers to keep state consistent. MST tries to corral all those variations down into a smaller set, where the Redux ecosystem is layering ideas on top of an small initial core. Megalith and MST are starting from two completely opposite sides, but end up looking very similar somewhere in the middle :)
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14860196"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  MST doesn't have the same restrictions as redux in terms of async so you don't need to do it in the same way.<p>Edit: In MST it would look more like plain js:</p><pre><code>    class AuthStore() {
        ....
        
        {
            login() {
                do_async_thing()
                    .then(this.postLoginStuff)
                    .catch(this.handleFailedLogin)
            },
            
            logout() {
                // do logout stuff
            }
        }
    }</code></pre>
              </div></td></tr>
      </tbody></table></td></tr>
      <tr id="14860051"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Looks nice. Seems to do a good job of making the code easy to read.<p>I'm assuming you started this before mobx state tree? It looks very similar. After much experimentation, MST is where I've decided to spend my time. Like your library, the code ends up readable.
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14860193"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Yeah, if I was starting today I might end up with MST as well. The only real benefit of megalith right now would be its size (5k vs 45k). You do get more features for that size though, like integration with the Redux toolset.
              </div></td></tr>
      </tbody></table></td></tr>
        <tr id="14860677"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  I guess you miss out on all the nice mobx stuff too (computed properties etc).<p>Having said that, I have to commend you. Your state library is the cleanest I've seen in terms of the user land code. There's nothing in the examples that feels like framework noise.
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14861190"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  Thanks!<p>Yeah, right now, state that shouldn't be saved (like computed properties) can be added as regular object properties (i.e. not a part of the initialState), and updated by listening for action events.</p><p>I've been thinking of ways to make that a little easier, possibly by having "reactions" that execute in response to actions. But I haven't had the need in my own projects yet, and like to err on the side of a smaller API footprint :)
              </p></div></td></tr>
      </tbody></table></td></tr>
                      <tr id="14860717"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I’ve made a lightweight React library influenced by functional setState, and supports async/await/Promises, extracting values from DOM / forms easily, pure function actions, animation with requestAnimationFrame, and reloading when props change.<p>I’ve put a lot of effort into providing some good examples (more coming!), and also on keeping it lightweight: core is 1.18KB gzipped.</p><p><a href="https://github.com/RoyalIcing/react-organism" target="_blank">https://github.com/RoyalIcing/react-organism</a></p><p>Feedback welcome, here or as issues!
              </p></div></td></tr>
      </tbody></table></td></tr>
        <tr id="14861456"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Looks nice, but I think I can get most of it using recompose, which I've been using extensively lately.
              </div></td></tr>
      </tbody></table></td></tr>
        <tr id="14861873"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Yes, you would be able to do a lot with the flexible recompose. I’ve tried to make something more friendly and lightweight that makes common use cases easier. I can find recompose a little overwhelming in the multiple layers.
              </div></td></tr>
      </tbody></table></td></tr>
                  <tr id="14859627"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Funny, I always thought of Redux as offering greater simplicity and MobX being more powerful.
              </div></td></tr>
      </tbody></table></td></tr>
        <tr id="14859983"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  With great simplicity comes great power ;)<p>MobX is simple to get going, but I fear there are dragons beneath. Here's a small writeup I did about it on Reddit: <a href="https://www.reddit.com/r/reactjs/comments/6pni2i/kea_high_level_abstraction_between_react_and_redux/dkr97n4/?st=j5lgq1hz&sh=4ba21f1e" target="_blank">https://www.reddit.com/r/reactjs/comments/6pni2i/kea_high_le...</a>
              </p></div></td></tr>
      </tbody></table></td></tr>
                <tr id="14863504"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Is this type-safe? Can it infer the payload type somehow? With MobX you can write type-safe code, and it's pretty important in bigger code bases. Redux can be made type-safe but is a bit clunky to use that way.
              </div></td></tr>
      </tbody></table></td></tr>
        <tr id="14867547"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Hi, propTypes are supported as an (optional) first class citizen. Thus whatever is the output of a reducer or a selector, provided it is passed to a react component, is type checked.<p>That said, I haven't used flow or TS myself and can't confirm nor deny compatibility
              </p></div></td></tr>
      </tbody></table></td></tr>
                <tr id="14859592"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  The concept expressed in the title matches a desire. Looking forward to checking out and hearing other's experiences.
              </div></td></tr>
      </tbody></table></td></tr>
              <tr id="14860110"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Why not just use state, which seems like the correct solution to the examples?
              </div></td></tr>
      </tbody></table></td></tr>
        <tr id="14867559"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Because the examples are just that, examples. Kea is designed for large complicated apps, and is in production use for at least 4 apps that I'm aware of (from marketplaces to fleet tracking)
              </div></td></tr>
      </tbody></table></td></tr>
                <tr id="14859517"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I have to dig into this but at first glance I like the approach
              </div></td></tr>
      </tbody></table></td></tr>
            </tbody></table>
      </td></tr>
<tr><td><img src="s.gif" width="0" height="10" /><br /><a href="newsguidelines.html" target="_blank">Guidelines</a>
        | <a href="newsfaq.html" target="_blank">FAQ</a>
        | <a href="mailto:hn@ycombinator.com" target="_blank">Support</a>
        | <a href="https://github.com/HackerNews/API" target="_blank">API</a>
        | <a href="security.html" target="_blank">Security</a>
        | <a href="lists" target="_blank">Lists</a>
        | <a href="bookmarklet.html" target="_blank">Bookmarklet</a>
        | <a href="http://www.ycombinator.com/legal/" target="_blank">Legal</a>
        | <a href="http://www.ycombinator.com/apply/" target="_blank">Apply to YC</a>
        | <a href="mailto:hn@ycombinator.com" target="_blank">Contact</a><br /><br />Search:
          
            </td></tr>
      </tbody></table>
  
<div><h3>Like On Github</h3><div><div>*Title (label for the link)</div></div><div><div>*Comment (commit message)</div></div><div id="action-btns"><div id="logh_btn_save">Saving...</div><div id="logh_btn_cancel">Cancel</div></div></div>
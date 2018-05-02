<a href="https://www.sohamkamani.com/blog/2017/03/31/react-redux-connect-explained/">https://www.sohamkamani.com/blog/2017/03/31/react-redux-connect-explained/</a><div id="articleHeader"><h1>React-redux "connect" explained 🔗</h1></div>
    <p>Mar 31, 2017 • 
  
  
    5 minute read
  

</p>
  </header>

  <article>
    <p>Redux is a terribly simple library for state management, and has made working with React more manageable for everyone. However, there are a lot of cases where people blindly follow boilerplate code to integrate redux with their React application without understanding all the moving parts involved.</p>

<p>There is an entire library, called <a href="https://github.com/reactjs/react-redux" target="_blank">react-redux</a> whose sole purpose is to seamlessly integrate redux’s state management into a React application. I feel that it’s important to know what’s going on when you do something that essentially forms the backbone of your application.</p>



<h2 id="react-and-redux-on-their-own">React and redux on their own</h2>

<p>At this point it’s hard for some to believe, but redux and React are actually two separate libraries which can and have been used completely independent of each other. Lets take a look at redux’s state management flow :</p>

<p><div class="readableLargeImageContainer"><img src="/assets/images/posts/react-redux-explanation/redux-flow.svg" alt="redux flow diagram" /></div></p>

<p>If you have worked with redux before, you know that its functionality revolves around a “store”, which is where the state of the application lives. There is no way anyone can directly modify the store. The only way to do so is through reducers, and the only way to trigger reducers is to dispatch actions. So ultimately :</p>

<blockquote>
  <p>To change data, we need to <strong>dispatch</strong> an action</p>
</blockquote>

<p>On the other hand, when we want to retrieve data, we do not get it directly from the store. Instead, we get a snapshot of the data in the store at any point in time using <code>store.getState()</code> , which gives us the “state” of the application as on the time at which we called the <code>getState</code> method.</p>

<blockquote>
  <p>To obtain data we need to get the current <strong>state</strong> of the store</p>
</blockquote>

<p>Now, let’s come to the (simplified) component structure of a <a href="http://todomvc.com/examples/react/#/" target="_blank">standard react todo-mvc application</a> :</p>

<p><div class="readableLargeImageContainer"><img src="/assets/images/posts/react-redux-explanation/react-flow.svg" alt="react flow diagram" /></div></p>

<h2 id="putting-them-together">Putting them together</h2>

<p>If we want to link our React application with the redux store, we first have to let our app know that this store exists. This is where we come to the first major part of the react-redux library, which is the <code>Provider</code>.</p>

<p><code>Provider</code> is a React component given to us by the “react-redux” library. It serves just one purpose : to “provide” the store to its child components.</p>

<div><div><pre><code>//This is the store we create with redux's createStore method
const store = createStore(todoApp,{})

// Provider is given the store as a prop
render(
  &lt;Provider store={store}&gt;
    &lt;App/&gt;
  &lt;/Provider&gt;, document.getElementById('app-node'))
</code></pre></div>

<p>Since the provider only makes the store accessible to it’s children, and we would ideally want our entire app to access the store, the most sensible thing to do would be to put our <code>App</code> component within <code>Provider</code>.</p>

<p>If we were to follow the previous diagram, the <code>Provider</code> node would be represented as a parent node on top of the <code>App</code> node. However, because of the utility that <code>Provider</code> gives us, I feel it’s more appropriate to represent it as something which “wraps” the entire application tree, like this :</p>

<p><div class="readableLargeImageContainer"><img src="/assets/images/posts/react-redux-explanation/react-flow-provider.svg" alt="react flow diagram with provider" /></div></p>

<h3 id="connect">Connect</h3>

<p>Now that we have “provided” the redux store to our application, we can now <em>connect</em> our components to it.
We established previously that there is no way to directly interact with the store. We can either retrieve data by obtaining its current state, or change its state by dispatching an action (we only have access to the top and bottom component of the redux flow diagram shown previously).</p>

<p>This is precisely what <code>connect</code> does. Consider this piece of code, which uses <code>connect</code> to map the stores state and dispatch to the props of a component :</p>

<div><div><pre><code>import {connect} from 'react-redux'

const TodoItem = ({todo, destroyTodo}) =&gt; {
  return (
    &lt;div&gt;
      {todo.text}
      &lt;span onClick={destroyTodo}&gt; x &lt;/span&gt;
    &lt;/div&gt;
  )
}

const mapStateToProps = state =&gt; {
  return {
    todo : state.todos[0]
  }
}

const mapDispatchToProps = dispatch =&gt; {
  return {
    destroyTodo : () =&gt; dispatch({
      type : 'DESTROY_TODO'
    })
  }
}

export default connect(
  mapStateToProps,
  mapDispatchToProps
)(TodoItem)
</code></pre></div>

<p><code>mapStateToProps</code> and <code>mapDispatchToProps</code> are both pure functions that are provided the stores “state” and “dispatch” respectively. Furthermore, both functions have to return an object, whose keys will then be passed on as the props of the component they are connected to.</p>

<p>In this case, <code>mapStateToProps</code> returns an object with only one key : “todo”, and <code>mapDispatchToProps</code> returns an object with the <code>destroyTodo</code> key.</p>

<p>The connected component (which is exported) provides <code>todo</code> and <code>destroyTodo</code> as props to <code>TodoItem</code>.</p>

<p><div class="readableLargeImageContainer"><img src="/assets/images/posts/react-redux-explanation/final-connect-flow.svg" alt="final connect flow" /></div></p>

<p>It’s important to note that only components <em>within</em> the <code>Provider</code> can be connected (In the above diagram, the connect is done <em>through</em> the Provider).</p>

<p>Redux is a powerful tool and even more so when combined with React. It really helps to know why each part of the <code>react-redux</code> library is used, and hopefully after reading this post, the function of <code>Provider</code> and <code>connect</code> is clear.</p>

<p>If you want to know how to use redux in an efficient and easy to use manner for calling APIs, you should read my other post on <a href="/blog/2016/06/05/redux-apis/" target="_blank">a simplified approach to calling APIs with redux</a></p>

  </article>

  <div>
    Share this on →
    
    
    
</div>




<div id="mc_embed_signup">

    <div id="mc_embed_signup_scroll">
	<h3>Like what I write? Join my mailing list, and I'll let you know whenever I write another post</h3>
<div>
	<label>Email Address </label>
	
</div>
	    
    
    
    





<a href="/blog/" target="_blank">View more blogs</a>


  
  


  


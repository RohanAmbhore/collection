<a href="https://react-apollo.github.io/2018/03/28/Apollo%7Capollo-link-state%20local%20state%20management/">https://react-apollo.github.io/2018/03/28/Apollo%7Capollo-link-state%20local%20state%20management/</a><div id="articleHeader"><h1>Apollo|apollo-link-state local state management</h1></div>
        

        <div>
          
            
              
                
              
              
                发表于
              
              <time>
                2018-03-28
              </time>
            

            
              |
            

            
              
                
              
              
                更新于:
              
              <time>
                2018-04-07
              </time>
            
          

          
            
            
              |
            
              
                
              
              
                分类于
              
              
                
                  <a href="/categories/技术备忘/" target="_blank">
                    技术备忘
                  </a>
                

                
                
              
            
          

          
            
          

          
          
             
               |
               
                 
               
               
                 阅读次数:
               
                 51
             
          

          

          
            <div>
              
                
                
                  
                
                
                  字数统计:
                
                
                  1,497
                
              

              
                |
              

              
                
                  
                
                
                  阅读时长 ≈
                
                
                  7
                
              
            </div>
          

          

        
      </header>
    

    
    
    
    

      
      

      
        <blockquote>
<p>Apollo-client中的本地数据管理方法. 和远程数据的流动方向一样, 但是在到达 server之前会被 apollo-link-state 截获,并做处理.数据仍然保持单向流动. </p>
</blockquote>
<p>调用<code>withClientState</code>方法,并使用 resolver做对应的处理. </p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br />6<br />7<br />8<br />9<br />10<br />11<br />12<br />13<br />14<br />15<br />16<br />17<br />18<br />19<br />20<br />21<br />22<br /></pre></td><td><pre>import { withClientState } from 'apollo-link-state';<br /><br />// This is the same cache you pass into new ApolloClient<br />const cache = new InMemoryCache(...);<br /><br />const stateLink = withClientState({<br />  cache,<br />  resolvers: {<br />    Mutation: {<br />      updateNetworkStatus: (_, { isConnected }, { cache }) =&gt; {<br />        const data = {<br />          networkStatus: {<br />            __typename: 'NetworkStatus',<br />            isConnected<br />          },<br />        };<br />        cache.writeData({ data });<br />        return null;<br />      },<br />    },<br />  }<br />});<br /></pre></td></tr></tbody></table></figure>
<p>在 Apollo-client 上挂载 state,state link 应该在在链的末端,由此其他的 link 可以做逻辑上的处理, 但是<code>必须要在 HttpLink之前</code>,只有这样本地的操作才可以在到达网络之前被截获.  如果使用了持久化查询(persisted queries), 也必须要在<code>apollo-link-persisted-queries</code>之前.  </p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br /></pre></td><td><pre>const client = new ApolloClient({<br />  cache,<br />  link: ApolloLink.from([stateLink, new HttpLink()]),<br />});<br /></pre></td></tr></tbody></table></figure>
<p>请求远程数据和本地数据,通过<code>@client</code>指令来区分. </p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br /></pre></td><td><pre>const UPDATE_NETWORK_STATUS = gql`<br />  mutation updateNetworkStatus($isConnected: Boolean) {<br />    updateNetworkStatus(isConnected: $isConnected) @client<br />  }<br />`;<br /></pre></td></tr></tbody></table></figure>
<p>在组件注入 query 或者 mutate 就可以了</p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br /></pre></td><td><pre>const WrappedComponent = graphql(UPDATE_NETWORK_STATUS, {<br />  props: ({ mutate }) =&gt; ({<br />    updateNetworkStatus: isConnected =&gt; mutate({ variables: { isConnected } }),<br />  }),<br />})(NetworkStatus);<br /></pre></td></tr></tbody></table></figure>
<p>如果要从其他组件访问 nework status 怎么办? 因为在访问之前,并不知道是否有<code>UPDATA_NETWORK_STATUS</code>存在,为了防止出现 undefined,需要提供一个默认的 state 作为初始值.</p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br />6<br />7<br />8<br />9<br />10<br />11<br />12<br />13<br />14<br /></pre></td><td><pre>const stateLink = withClientState({<br />  cache,<br />  resolvers: {<br />    Mutation: {<br />      /* same as above */<br />    },<br />  },<br />  defaults: {<br />    networkStatus: {<br />      __typename: 'NetworkStatus',<br />      isConnected: true,<br />    },<br />  },<br />});<br /></pre></td></tr></tbody></table></figure>
<p>组件查询 network也使用<code>@client</code>指令</p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br />6<br />7<br />8<br />9<br />10<br />11<br /></pre></td><td><pre>const GET_ARTICLES = gql`<br />  query {<br />    networkStatus @client {<br />      isConnected<br />    }<br />    articles {<br />      id<br />      title<br />    }<br />  }<br />`;<br /></pre></td></tr></tbody></table></figure>
<hr />
<h2 id="Defaults">Defaults</h2><figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br />6<br />7<br />8<br />9<br />10<br />11<br />12<br />13<br />14<br />15<br />16<br />17<br />18<br /></pre></td><td><pre>const defaults = {<br />  todos: [],<br />  visibilityFilter: 'SHOW_ALL',<br />  networkStatus: {<br />    __typename: 'NetworkStatus',<br />    isConnected: false,<br />  }<br />};<br /><br />const resolvers = { /* ... */ };<br /><br />const cache = new InMemoryCache();<br /><br />const stateLink = withClientState({<br />  resolvers,<br />  cache,<br />  defaults<br />});<br /></pre></td></tr></tbody></table></figure>
<h2 id="Resolvers">Resolvers</h2><p>resolvers 是实现 local state 的地方.  resolver的 map是对应每个 GraphQL 对象类型的resolver 函数.  </p>
<p><code>apollo-link-state</code>有四个重要的部分</p>
<ol>
<li>cache在上下文中,可以用来读取数据</li>
<li>resolver 应该返回一个有<code>_typename</code>属性的对象, 也可以用<code>dataIdFromObject</code>代替.  目的是 Apollo 用于数据的normalize</li>
<li>如果需要执行异步操作,可以使用 promise.</li>
<li>Query只针对 cache. 如果在所有的 mutate 之前执行 query,需要提供默认值</li>
</ol>
<h2 id="Default-resolvers">Default resolvers</h2><p>不一定要为每个字段都建立特定的 resolvers,如果从 parent 对象返回的值和children 请求的字段一致,就不需要 resolvers.这就是<code>default resovlers</code></p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br />6<br />7<br />8<br />9<br />10<br />11<br /></pre></td><td><pre>const getUser = gql`<br />  query {<br />    user(id: 1) @client {<br />      name {<br />        last<br />        first<br />      }<br />    }<br />  }<br />`;<br /></pre></td></tr></tbody></table></figure>
<h2 id="Resolvers-signature">Resolvers signature</h2><p>Apollo-client 中的resolver 函数和用<code>graph-tools</code>构建的 server 中的 resolvers 是完全一样的.  </p>
<figure><table><tbody><tr><td><pre>1<br /></pre></td><td><pre>fieldName:(obj,args,context,info)=&gt;result;<br /></pre></td></tr></tbody></table></figure>
<ol>
<li><code>obj</code>: 包含 parent 字段 或者<code>ROOT_QUERY</code>对象</li>
<li><code>args</code>: 传递进入的参数, 例如<code>updataNetworkStatus(isConnected:true)</code>,<code>args</code>对象就是<code>{isConnected:true}</code></li>
<li><code>context</code>: 在所有的link 中共享的数据. 重要的的一点是Apollo cache添加在其中,所以可以用<code>cache.writeData({})</code>.如果想设定额外的值,可以在组件内设定,或者使用<code>apollo-link-context</code>. </li>
<li><code>info</code>:  有关 state 执行状态的信息. 个人不会用到</li>
</ol>
<h2 id="Async-resolvers">Async resolvers</h2><p>如果想访问 REST 数据,可以参考<code>apollo-link-rest</code>.  </p>
<p>对于 RN或者 其他的 browser API,需要在组件的生命周期方法中添加触发函数.</p>
<h2 id="这一部分暂时不写">这一部分暂时不写</h2><h2 id="Organizing-resolvers">Organizing resolvers</h2><p>使用鸭子类型 ,每个feature都有自己的一套方法,然后合并起来</p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br />6<br />7<br />8<br />9<br />10<br />11<br /></pre></td><td><pre>import merge from 'lodash.merge';<br />import { withClientState } from 'apollo-link-state';<br /><br />import currentUser from './resolvers/user';<br />import cameraRoll from './resolvers/camera';<br />import networkStatus from './resolvers/camera';<br /><br />const stateLink = withClientState({<br />  cache,<br />  resolvers: merge(currentUser, cameraRoll, networkStatus),<br />});<br /></pre></td></tr></tbody></table></figure>
<p>可以设定默认值</p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br />6<br />7<br />8<br />9<br />10<br />11<br />12<br />13<br /></pre></td><td><pre>const currentUser = {<br />  defaults: {<br />    currentUser: null,<br />  },<br />  resolvers: { ... }<br />};<br /><br />const cameraRoll = { defaults: { ... }, resolvers: { ... }};<br /><br />const stateLink = withClientState({<br />  ...merge(currentUser, cameraRoll, networkStatus),<br />  cache,<br />});<br /></pre></td></tr></tbody></table></figure>
<h2 id="updating-the-cache">updating the cache</h2><p>可以通过<code>context</code>访问或者更新 cache. Apollo cache API 有几个方法 </p>
<h3 id="writeData">writeData</h3><p>直接在 Cahce 中写入数据,不用通过 query. </p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br />6<br />7<br />8<br /></pre></td><td><pre>const filter = {<br />  Mutation: {<br />    updateVisibilityFilter: (_, { visibilityFilter }, { cache }) =&gt; {<br />      const data = { visibilityFilter, __typename: 'Filter' };<br />      cache.writeData({ data });<br />    },<br />  },<br />};<br /></pre></td></tr></tbody></table></figure>
<p><code>如果传递id属性,也可以在已经存在的对象中写入片段数据.</code></p>
<p>这里的<code>id</code>应该对应对象的 cache key. 如果使用<code>InMemroyCache</code>,并且没有覆盖<code>dataObjectFromId</code>,cache key就是<code>_typename:id</code></p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br />6<br />7<br />8<br /></pre></td><td><pre>const user = {<br />  Mutation: {<br />    updateUserEmail: (_, { id, email }, { cache }) =&gt; {<br />      const data = { email };<br />      cache.writeData({ id: `User:${id}`, data });<br />    },<br />  },<br />};<br /></pre></td></tr></tbody></table></figure>
<h2 id="writeQuery-和-readQuery">writeQuery 和 readQuery</h2><p>在某些情况下,写入到 cache 的数据依赖于已经存在的数据,例如 ,在 list 中添加一条 item或者对属性做修改.  做法是使用<code>cache.readQuery</code>传递 query,在写入数据之前从 cache 中读取数据. 看看 list的例子</p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br />6<br />7<br />8<br />9<br />10<br />11<br />12<br />13<br />14<br />15<br />16<br />17<br />18<br />19<br />20<br />21<br />22<br />23<br />24<br />25<br />26<br />27<br />28<br />29<br />30<br />31<br />32<br /></pre></td><td><pre>let nextTodoId = 0;<br /><br />const todos = {<br />  defaults: {<br />    todos: [],<br />  },<br />  resolvers: {<br />    Mutation: {<br />      addTodo: (_, { text }, { cache }) =&gt; {<br />        const query = gql`<br />          query GetTodos {<br />            todos @client {<br />              id<br />              text<br />              completed<br />            }<br />          }<br />        `;<br /><br />const previous = cache.readQuery({ query });<br />        const newTodo = { id: nextTodoId++, text, completed: false, __typename: 'TodoItem' },<br />        const data = {<br />          todos: previous.todos.concat([newTodo]),<br />        };<br /><br />// you can also do cache.writeData({ data }) here if you prefer<br />        cache.writeQuery({ query, data });<br />        return newTodo;<br />      },<br />    },<br />  },<br />};<br /></pre></td></tr></tbody></table></figure>
<p>为了在 list 中添加 todo, 需要当前的 todos, 可以通过<code>cache.readQuery</code>获取. </p>
<p>为了写入数据到 cache.可以使用<code>cache.writeQuery</code>,<code>cache.writeData</code>. 不同点在于<code>cache.writeQuery</code>需要传递 query,来验证 data的结构.  在底层,<code>cache.write</code>自动从<code>data</code>构建了 query.  </p>
<h2 id="writeFragment-和-readFragment">writeFragment 和 readFragment</h2><p><code>cache.writeFragment</code>,在有了 cache key 情况下, 可以灵活的读取数据.</p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br />6<br />7<br />8<br />9<br />10<br />11<br />12<br />13<br />14<br />15<br />16<br />17<br />18<br />19<br />20<br /></pre></td><td><pre>const todos = {<br />  resolvers: {<br />    Mutation: {<br />      toggleTodo: (_, variables, { cache }) =&gt; {<br />        const id = `TodoItem:${variables.id}`;<br />        const fragment = gql`<br />          fragment completeTodo on TodoItem {<br />            completed<br />          }<br />        `;<br />        const todo = cache.readFragment({ fragment, id });<br />        const data = { ...todo, completed: !todo.completed };<br /><br />// you can also do cache.writeData({ data, id }) here if you prefer<br />        cache.writeFragment({ fragment, id, data });<br />        return null;<br />      },<br />    },<br />  },<br />};<br /></pre></td></tr></tbody></table></figure>
<h2 id="client-directive">@client directive</h2><h2 id="Combining-local-and-remote-data">Combining local and remote data</h2><p>下面的例子中,我们从 server 获取到 username,从 apollo cache 获取到 cart 信息.两者在结果中融合在一起</p>
<figure><table><tbody><tr><td><pre>1<br />2<br />3<br />4<br />5<br />6<br />7<br />8<br />9<br />10<br />11<br />12<br />13<br />14<br /></pre></td><td><pre>const getUser = gql`<br />  query getUser($id: String) {<br />    user(id: $id) {<br />      id<br />      name<br />      cart @client {<br />        product {<br />          name<br />          id<br />        }<br />      }<br />    }<br />  }<br />`;<br /></pre></td></tr></tbody></table></figure>

      
    
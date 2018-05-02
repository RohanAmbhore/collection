<a href="https://github.com/sorrycc/blog/issues/18">https://github.com/sorrycc/blog/issues/18</a><div id="articleHeader"><h1>              12 步 30 分钟，完成用户管理的 CURD 应用 (react+dva+antd)            #18    </h1></div>


  <div>
    
    <div>
        <a href="/sorrycc" target="_blank">sorrycc</a>  opened this Issue
        <relative-time>on Dec 21, 2016</relative-time>
        · 315 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      

  
    
      
          <blockquote>
<p>本文仅适用于 dva@1，dva@2 的文档请移步 <a href="https://github.com/sorrycc/blog/issues/62" target="_blank">#62</a><br />
本文仅适用于 dva@1，dva@2 的文档请移步 <a href="https://github.com/sorrycc/blog/issues/62" target="_blank">#62</a><br />
本文仅适用于 dva@1，dva@2 的文档请移步 <a href="https://github.com/sorrycc/blog/issues/62" target="_blank">#62</a></p>
</blockquote>
<p>本文会一步步引导大家如何创建一个 CURD 应用，包含查询、编辑、删除、创建，以及分页处理，数据 mock，自动处理 loading 状态等，基于 react, <a href="https://github.com/dvajs/dva" target="_blank">dva</a> 和 <a href="https://github.com/ant-design/ant-design" target="_blank">antd</a> 。</p>
<p>最终效果：</p>
<p><a href="https://camo.githubusercontent.com/c2b2094ff4180d1afd132aefa0e0c1188c904697/68747470733a2f2f7a6f732e616c697061796f626a656374732e636f6d2f726d73706f7274616c2f6141534a624464426b686d7478786462744c43652e676966" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/c2b2094ff4180d1afd132aefa0e0c1188c904697/68747470733a2f2f7a6f732e616c697061796f626a656374732e636f6d2f726d73706f7274616c2f6141534a624464426b686d7478786462744c43652e676966" /></div></a></p>
<h2>开始之前：</h2>
<ul>
<li>确保 node 版本是 6.5 +</li>
<li>用 <a href="https://github.com/cnpm/cnpm" target="_blank">cnpm</a> 或 <a href="https://github.com/yarnpkg/yarn" target="_blank">yarn</a> 能节约你安装依赖的时间</li>
</ul>
<h2>Step 1. 安装 <a href="https://github.com/dvajs/dva-cli" target="_blank">dva-cli</a> 并创建应用</h2>
<p>先安装 dva-cli，并确保版本是 0.7.x。</p>
<div><pre>$ npm i dva-cli@0.7 -g
$ dva -v
0.7.0</pre></div>
<p>然后创建应用：</p>
<div><pre>$ dva new user-dashboard
$ cd user-dashboard </pre></div>
<h2>Step 2. 配置 <a href="https://github.com/ant-design/ant-design" target="_blank">antd</a> 和 <a href="https://github.com/ant-design/babel-plugin-import" target="_blank">babel-plugin-import</a></h2>
<p>babel-plugin-import 用于按需引入 antd 的 JavaScript 和 CSS，这样打包出来的文件不至于太大。</p>
<div><pre>$ npm i antd --save
$ npm i babel-plugin-import --save-dev</pre></div>
<p>修改 <code>.roadhogrc</code>，在 <code>"extraBabelPlugins"</code> 里加上：</p>
<div><pre>["import", { "libraryName": "antd", "style": "css" }]</pre></div>
<h2>Step 3. 配置代理，能通过 RESTFul 的方式访问 <a href="http://localhost:8000/api/users" target="_blank">http://localhost:8000/api/users</a></h2>
<p>修改 <code>.roadhogrc</code>，加上 <code>"proxy"</code> 配置：</p>
<div><pre>"proxy": {
  "/api": {
    "target": "http://jsonplaceholder.typicode.com/",
    "changeOrigin": true,
    "pathRewrite": { "^/api" : "" }
  }
},</pre></div>
<p>然后启动应用：(这个命令一直开着，后面不需要重启)</p>
<div><pre>$ npm start</pre></div>
<p>浏览器会自动开启，并打开 <a href="http://localhost:8000" target="_blank">http://localhost:8000</a> 。</p>
<p>访问 <a href="http://localhost:8000/api/users" target="_blank">http://localhost:8000/api/users</a> ，就能访问到 <a href="http://jsonplaceholder.typicode.com/users" target="_blank">http://jsonplaceholder.typicode.com/users</a> 的数据。(由于 typicode.com 服务的稳定性，偶尔可能会失败。不过没关系，正好便于我们之后对于出错的处理)</p>
<p><a href="https://camo.githubusercontent.com/14d5adf56ada88fbeb510a29d114f0616fb08527/68747470733a2f2f7a6f732e616c697061796f626a656374732e636f6d2f726d73706f7274616c2f6f4641504a6b78634959655a466a59415475554c2e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/14d5adf56ada88fbeb510a29d114f0616fb08527/68747470733a2f2f7a6f732e616c697061796f626a656374732e636f6d2f726d73706f7274616c2f6f4641504a6b78634959655a466a59415475554c2e706e67"   /></div></a></p>
<h2>Step 4. 生成 users 路由</h2>
<p>用 dva-cli 生成路由：</p>
<div><pre>$ dva g route users</pre></div>
<p>然后访问 <a href="http://localhost:8000/#/users" target="_blank">http://localhost:8000/#/users</a> 。</p>
<h2>Step 5. 构造 users model 和 service</h2>
<p>用 dva-cli 生成 Model ：</p>
<div><pre>$ dva g model users</pre></div>
<p>修改 <code>src/models/users.js</code> ：</p>
<div><pre>import * as usersService from '../services/users';

export default {
  namespace: 'users',
  state: {
    list: [],
    total: null,
  },
  reducers: {
    save(state, { payload: { data: list, total } }) {
      return { ...state, list, total };
    },
  },
  effects: {
    *fetch({ payload: { page } }, { call, put }) {
      const { data, headers } = yield call(usersService.fetch, { page });
      yield put({ type: 'save', payload: { data, total: headers['x-total-count'] } });
    },
  },
  subscriptions: {
    setup({ dispatch, history }) {
      return history.listen(({ pathname, query }) =&gt; {
        if (pathname === '/users') {
          dispatch({ type: 'fetch', payload: query });
        }
      });
    },
  },
};</pre></div>
<p>新增 <code>src/services/users.js</code>：</p>
<div><pre>import request from '../utils/request';

export function fetch({ page = 1 }) {
  return request(`/api/users?_page=${page}&_limit=5`);
}</pre></div>
<p>由于我们需要从 response headers 中获取 total users 数量，所以需要改造下 <code>src/utils/request.js</code>：</p>
<div><pre>import fetch from 'dva/fetch';

function checkStatus(response) {
  if (response.status &gt;= 200 && response.status &lt; 300) {
    return response;
  }

  const error = new Error(response.statusText);
  error.response = response;
  throw error;
}

/**
 * Requests a URL, returning a promise.
 *
 * @param  {string} url       The URL we want to request
 * @param  {object} [options] The options we want to pass to "fetch"
 * @return {object}           An object containing either "data" or "err"
 */
export default async function request(url, options) {
  const response = await fetch(url, options);

  checkStatus(response);

  const data = await response.json();

  const ret = {
    data,
    headers: {},
  };

  if (response.headers.get('x-total-count')) {
    ret.headers['x-total-count'] = response.headers.get('x-total-count');
  }

  return ret;
}</pre></div>
<p>切换到浏览器（会自动刷新），应该没任何变化，因为数据虽然好了，但并没有视图与之关联。但是打开 Redux 开发者工具，应该可以看到 <code>users/fetch</code> 和 <code>users/save</code> 的 action 以及相关的 state 。</p>
<p><a href="https://camo.githubusercontent.com/addc2482d3667d3ff6d79c0c26e5b278639a8263/68747470733a2f2f7a6f732e616c697061796f626a656374732e636f6d2f726d73706f7274616c2f44744e6f586a5141644d534a717a4f53455a416f2e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/addc2482d3667d3ff6d79c0c26e5b278639a8263/68747470733a2f2f7a6f732e616c697061796f626a656374732e636f6d2f726d73706f7274616c2f44744e6f586a5141644d534a717a4f53455a416f2e706e67" /></div></a></p>
<h2>Step 6. 添加界面，让用户列表展现出来</h2>
<p>用 dva-cli 生成 component：</p>
<div><pre>$ dva g component Users/Users</pre></div>
<p>然后修改生成出来的 <code>src/components/Users/Users.js</code> 和 <code>src/components/Users/Users.css</code>，并在 <code>src/routes/Users.js</code> 中引用他。具体参考这个 <a href="https://github.com/dvajs/dva-example-user-dashboard/commit/85a7b5ac61197227e9c9e92a851f227ce2902a22" target="_blank">Commit</a>。</p>
<p>需留意两件事：</p>
<ol>
<li>对 model 进行了微调，加入了 page 表示当前页</li>
<li>由于 components 和 services 中都用到了 pageSize，所以提取到 <code>src/constants.js</code></li>
</ol>
<p>改完后，切换到浏览器，应该能看到带分页的用户列表。</p>
<p><a href="https://camo.githubusercontent.com/2f75960f18fed0f5b5b705e323df8e380138b3b1/68747470733a2f2f7a6f732e616c697061796f626a656374732e636f6d2f726d73706f7274616c2f6763456c70527054446b7055456d72585247486e2e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/2f75960f18fed0f5b5b705e323df8e380138b3b1/68747470733a2f2f7a6f732e616c697061796f626a656374732e636f6d2f726d73706f7274616c2f6763456c70527054446b7055456d72585247486e2e706e67" /></div></a></p>
<h2>Step 7. 添加 layout</h2>
<p>添加 layout 布局，使得我们可以在首页和用户列表页之间来回切换。</p>
<ol>
<li>添加布局，<code>src/components/MainLayout/MainLayout.js</code> 和 CSS 文件</li>
<li>在 <code>src/routes</code> 文件夹下的文件中引用这个布局</li>
</ol>
<p>参考这个 <a href="https://github.com/dvajs/dva-example-user-dashboard/commit/94788e5167f9b2dd7b1ecdc70bb8e7bc91a9fb62" target="_blank">Commit</a>。</p>

<ol>
<li>页头的菜单会随着页面切换变化，高亮显示当前页所在的菜单项</li>
</ol>
<h2>Step 8. 通过 <a href="https://github.com/dvajs/dva-loading" target="_blank">dva-loading</a> 处理 loading 状态</h2>
<p>dva 有一个管理 effects 执行的 hook，并基于此封装了 dva-loading 插件。通过这个插件，我们可以不必一遍遍地写 showLoading 和 hideLoading，当发起请求时，插件会自动设置数据里的 loading 状态为 true 或 false 。然后我们在渲染 components 时绑定并根据这个数据进行渲染。</p>
<p>先安装 dva-loading ：</p>
<div><pre>$ npm i dva-loading --save</pre></div>
<p>修改 <code>src/index.js</code> 加载插件，在合适的地方加入下面两句：</p>
<div><pre>+ import createLoading from 'dva-loading';
+ app.use(createLoading());</pre></div>
<p>然后在 <code>src/components/Users/Users.js</code> 里绑定 loading 数据：</p>
<div><pre>+ loading: state.loading.models.users,</pre></div>
<p>具体参考这个 <a href="https://github.com/dvajs/dva-example-user-dashboard/commit/e256165312e5fe0e63c29cc1cba96909b66b5092" target="_blank">Commit</a> 。</p>
<p>切换到浏览器，你的用户列表有 loading 了没?</p>
<h2>Step 9. 处理分页</h2>
<p>只改一个文件 <code>src/components/Users/Users.js</code> 就好。</p>
<p>处理分页有两个思路：</p>
<ol>
<li>发 action，请求新的分页数据，保存到 model，然后自动更新页面</li>
<li>切换路由 (由于之前监听了路由变化，所以后续的事情会自动处理)</li>
</ol>
<p>我们用的是思路 2 的方式，好处是用户可以直接访问到 page 2 或其他页面。</p>
<p>参考这个 <a href="https://github.com/dvajs/dva-example-user-dashboard/commit/b6203eae7000225ae1d0954841c93aeec66df1d5" target="_blank">Commit</a> 。</p>
<h2>Step 10. 处理用户删除</h2>
<p>经过前面的 9 步，应用的整体脉络已经清晰，相信大家已经对整体流程也有了一定了解。</p>
<p>后面的功能调整基本都可以按照以下三步进行：</p>
<ol>
<li>service</li>
<li>model</li>
<li>component</li>
</ol>
<p>我们现在开始增加用户删除功能。</p>
<ol>
<li>service, 修改 <code>src/services/users.js</code>：</li>
</ol>
<div><pre>export function remove(id) {
  return request(`/api/users/${id}`, {
    method: 'DELETE',
  });
}</pre></div>
<ol>
<li>model, 修改 <code>src/models/users.js</code>：</li>
</ol>
<div><pre>*remove({ payload: id }, { call, put, select }) {
  yield call(usersService.remove, id);
  const page = yield select(state =&gt; state.users.page);
  yield put({ type: 'fetch', payload: { page } });
},</pre></div>
<ol>
<li>component, 修改 <code>src/components/Users/Users.js</code>，替换 <code>deleteHandler</code> 内容：</li>
</ol>
<div><pre>dispatch({
  type: 'users/remove',
  payload: id,
});</pre></div>
<p>切换到浏览器，删除功能应该已经生效。</p>
<h2>Step 11. 处理用户编辑</h2>
<p>处理用户编辑和前面的一样，遵循三步走：</p>
<ol>
<li>service</li>
<li>model</li>
<li>component</li>
</ol>
<p>先是 service，修改 <code>src/services/users.js</code>：</p>
<div><pre>export function patch(id, values) {
  return request(`/api/users/${id}`, {
    method: 'PATCH',
    body: JSON.stringify(values),
  });
}</pre></div>
<p>再是 model，修改 <code>src/models/users.js</code>：</p>
<div><pre>*patch({ payload: { id, values } }, { call, put, select }) {
  yield call(usersService.patch, id, values);
  const page = yield select(state =&gt; state.users.page);
  yield put({ type: 'fetch', payload: { page } });
},</pre></div>
<p>最后是 component，详见 <a href="https://github.com/dvajs/dva-example-user-dashboard/commit/ed7a4ee584eca368c1250cd0ff6d0daee22de124" target="_blank">Commit</a>。</p>
<p>需要注意的一点是，我们在这里如何处理 Modal 的 visible 状态，有几种选择：</p>
<ol>
<li>存 dva 的 model state 里</li>
<li>存 component state 里</li>
</ol>
<p>另外，怎么存也是个问题，可以：</p>
<ol>
<li>只有一个 visible，然后根据用户点选的 user 填不同的表单数据</li>
<li>几个 user 几个 visible</li>
</ol>
<p>此教程选的方案是 2-2，即存 component state，并且 visible 按 user 存。另外为了使用的简便，封装了一个 <code>UserModal</code> 的组件。</p>
<p>完成后，切换到浏览器，应该就能对用户进行编辑了。</p>
<h2>Step 12. 处理用户创建</h2>
<p>相比用户编辑，用户创建更简单些，因为可以共用 <code>UserModal</code> 组件。和 Step 11 比较类似，就不累述了，详见 <a href="https://github.com/dvajs/dva-example-user-dashboard/commit/72cd7366076c025473ff4acd99815fd9b585619e" target="_blank">Commit</a> 。</p>
<hr />
<p>到这里，我们已经完成了一个完整的 CURD 应用。但仅仅是完成，并不完善，比如：</p>
<ul>
<li>如何处理错误，比如请求等</li>
<li>如何处理请求超时</li>
<li>如何根据路由动态加载 JS 和 CSS</li>

</ul>
<p>请期待下一篇。</p>

      
<a href="https://github.com/sorrycc/blog/issues/1">https://github.com/sorrycc/blog/issues/1</a><div id="articleHeader"><h1>              React + Redux 最佳实践            #1    </h1></div>


  <div>
    
    <div>
        <a href="/sorrycc" target="_blank">sorrycc</a>  opened this Issue
        <relative-time>on Feb 29, 2016</relative-time>
        · 56 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  <div id="issue-137178303">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/sorrycc" target="_blank">sorrycc</a>
  

    </strong>

    commented

    <a href="#issue-137178303" target="_blank"><relative-time>on Feb 29, 2016</relative-time></a>


      
  •


  
    <summary>
      
          edited
      
      
    </summary>

    
  

  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>更新：我们基于此最佳实践做了一个封装方案：<a href="https://github.com/sorrycc/dva" target="_blank">dva</a>，可以简化使用 redux 和 redux-saga 时很多繁杂的操作。</p>
</blockquote>
<p><a href="https://camo.githubusercontent.com/21740ab2fdb2ba1504678bfddf39ab9943adfa39/68747470733a2f2f6f732e616c697061796f626a656374732e636f6d2f726d73706f7274616c2f506b4a564957464a62705a63776d532e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/21740ab2fdb2ba1504678bfddf39ab9943adfa39/68747470733a2f2f6f732e616c697061796f626a656374732e636f6d2f726d73706f7274616c2f506b4a564957464a62705a63776d532e706e67" /></div></a></p>
<p>前端变化虽快，但其实一直都围绕这几个概念在转：</p>
<ul>
<li>URL - 访问什么页面</li>
<li>Data - 显示什么信息</li>
<li>View - 页面长成什么样</li>
<li>Action - 对页面做了什么操作</li>
<li>API Server - Data 数据的来源</li>
</ul>
<p>在 redux 的生态圈内，每个环节有多种方案，比如 Data 可以是 <code>immutable</code> 或者 <code>plain object</code>，在你选了 <code>immutable</code> 之后，用 <a href="https://facebook.github.io/immutable-js/" target="_blank">immutable.js</a> 还是 <a href="https://github.com/rtfeldman/seamless-immutable" target="_blank">seamless-immutable</a>，以及是否用 <a href="https://github.com/gajus/redux-immutable" target="_blank">redux-immutable</a> 来辅助数据修改，都需要选择。</p>
<p>本文总结目前 react + redux 的最佳实践，解释原因，并提供可选方案。</p>
<p>心急的朋友可以直接看代码：<a href="https://github.com/sorrycc/github-stars" target="_blank">https://github.com/sorrycc/github-stars</a></p>
<h2>一、URL &gt; Data</h2>

<p>routing</p>

<p><a href="https://github.com/rackt/react-router" target="_blank">react-router</a> + <a href="https://github.com/rackt/react-router-redux" target="_blank">react-router-redux</a>: 前者是业界标准，后者可以同步 route 信息到 state，这样你可以在 view 根据 route 信息调整展现，以及通过 action 来修改 route 。</p>


<h2>二、Data</h2>

<p>为 redux 提供数据源，修改容易。</p>

<p><code>plain object</code>: 配合 combineReducer 已经可以满足需求。</p>
<p>同时在组织 Store 的时候，层次不要太深，尽量保持在 2 - 3 层。如果层次深，可以考虑用 <a href="https://github.com/substantial/updeep" target="_blank">updeep</a> 来辅助修改数据。</p>

<p><a href="https://facebook.github.io/immutable-js/" target="_blank">immutable.js</a>: 通过自定义的 api 来操作数据，需要额外的学习成本。不熟悉 immutable.js 的可以先尝试用 <a href="https://github.com/rtfeldman/seamless-immutable" target="_blank">seamless-immutable</a>，JavaScript 原生接口，无学习门槛。</p>
<p>另外，不推荐用 <a href="https://github.com/gajus/redux-immutable" target="_blank">redux-immutable</a> 以及 redux-immutablejs，一是没啥必要，具体看他们的实现就知道了，都比较简单；更重要的是他们都改写了 <code>combineReducer</code>，会带来潜在的一些兼容问题。</p>
<h2>三、Data &gt; View</h2>

<p>数据的过滤和筛选。</p>

<p><a href="https://github.com/reactjs/reselect" target="_blank">reselect</a>: store 的 select 方案，用于提取数据的筛选逻辑，让 Component 保持简单。选 reselct 看重的是 <code>可组合特性</code> 和 <code>缓存机制</code> 。</p>


<h2>四、View 之 CSS 方案</h2>

<p>合理的 CSS 方案，考虑团队协作。</p>

<p><a href="https://github.com/css-modules/css-modules" target="_blank">css-modules</a>: 配合 webpack 的 css-loader 进行打包，会为所有的 class name 和 animation name 加 local scope，避免潜在冲突。</p>
<p>直接看代码：</p>
<p>Header.jsx</p>
<div><pre>import style from './Header.less';
export default () =&gt; &lt;div className={style.normal} /&gt;;</pre></div>
<p>Header.less</p>
<div><pre>.normal { color: red; }</pre></div>
<p>编译后，文件中的 <code>style.normal</code> 和 <code>.normal</code> 在会被重命名为类似 <code>Header__normal___VI1de</code> 。</p>

<p><a href="https://en.bem.info/" target="_blank">bem</a>, <a href="http://rscss.io/" target="_blank">rscss</a> ，这两个都是基于约定的方案。但基于约定会带来额外的学习成本和不遍，比如 rscss 要求所有的 Component 都是两个词的连接，比如 <code>Header</code> 就必须换成类似 <code>HeaderBox</code> 这样。</p>
<p><a href="https://github.com/FormidableLabs/radium" target="_blank">radium</a>，inline css 方案，没研究。</p>
<h2>五、Action &lt;&gt; Store，业务逻辑处理</h2>

<p>统一处理业务逻辑，尤其是异步的处理。</p>

<p><a href="https://github.com/yelouafi/redux-saga" target="_blank">redux-saga</a>: 用于管理 action，处理异步逻辑。可测试、可 mock、声明式的指令。</p>

<p><a href="https://github.com/raisemarketplace/redux-loop" target="_blank">redux-loop</a>: 适用于相对简单点的场景，可以组合异步和同步的 action 。但他有个问题是改写了 <code>combineReducer</code>，会导致一些意想不到的兼容问题，比如我在特定场景下用不了 redux-devtool 。</p>
<p><a href="https://github.com/gaearon/redux-thunk" target="_blank">redux-thunk</a>, <a href="https://github.com/acdlite/redux-promise" target="_blank">redux-promise</a> 等: 相对原始的异步方案，适用于更简单的场景。在 action 需要组合、取消等操作时，会不好处理。</p>
<h3>saga 入门</h3>
<p>在 saga 之前，你可能会在 action creator 里处理业务逻辑，虽然能跑通，但是难以测试。比如：</p>
<div><pre>// action creator with thunking
function createRequest () {
  return (dispatch, getState) =&gt; {
    dispatch({ type: 'REQUEST_STUFF' });
    someApiCall(function(response) {
      // some processing
      dispatch({ type: 'RECEIVE_STUFF' });
    });
  };
}</pre></div>
<p>然后组件里可能这样：</p>
<div><pre>function onHandlePress () {
  this.props.dispatch({ type: 'SHOW_WAITING_MODAL' });
  this.props.dispatch(createRequest());
}</pre></div>
<p>这样通过 redux state 和 reducer 把所有的事情串联到起来。</p>
<p>但问题是：</p>
<blockquote>
<p>Code is everywhere.</p>
</blockquote>
<p>通过 saga，你只需要触发一个 action 。</p>
<div><pre>function onHandlePress () {
  // createRequest 触发 action `BEGIN_REQUEST`
  this.props.dispatch(createRequest());
}</pre></div>
<p>然后所有后续的操作都通过 saga 来管理。</p>
<div><pre>function *hello() {
  // 等待 action `BEGIN_REQUEST`
  yield take('BEGIN_REQUEST');
  // dispatch action `SHOW_WAITING_MODAL`
  yield put({ type: 'SHOW_WAITING_MODAL' });
  // 发布异步请求
  const response = yield call(myApiFunctionThatWrapsFetch);
  // dispatch action `PRELOAD_IMAGES`, 附上 response 信息
  yield put({ type: 'PRELOAD_IMAGES', response.images });
  // dispatch action `HIDE_WAITING_MODAL`
  yield put({ type: 'HIDE_WAITING_MODAL' });
}</pre></div>
<p>可以看出，调整之后的代码有几个优点：</p>
<ul>
<li>所有业务代码都存于 saga 中，不再散落在各处</li>
<li>全同步执行，就算逻辑再复杂，看起来也不会乱</li>
</ul>
<h2>六、Data &lt;&gt; API Server</h2>

<p>异步请求。</p>

<p><a href="https://github.com/matthew-andrews/isomorphic-fetch" target="_blank">isomorphic-fetch</a>: 便于在同构应用中使用，另外同时要写 node 和 web 的同学可以用一个库，学一套 api 。</p>
<p>然后通过 <code>async</code> + <code>await</code> 组织代码。</p>
<p>示例代码：</p>
<div><pre>import fetch from 'isomorphic-fetch';
export async function fetchUser(uid) {
  return await fetch(`/users/${uid}`).then(res =&gt; res.json());
};</pre></div>

<p><a href="https://github.com/ded/reqwest" target="_blank">reqwest</a></p>

<p><a href="https://camo.githubusercontent.com/068c4ff126977b861cff3338428bdde6927f7dad/68747470733a2f2f6f732e616c697061796f626a656374732e636f6d2f726d73706f7274616c2f43684d775a42755a6c614c725377652e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/068c4ff126977b861cff3338428bdde6927f7dad/68747470733a2f2f6f732e616c697061796f626a656374732e636f6d2f726d73706f7274616c2f43684d775a42755a6c614c725377652e706e67" /></div></a></p>

      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>

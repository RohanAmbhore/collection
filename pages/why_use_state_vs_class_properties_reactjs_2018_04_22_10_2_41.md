<a href="https://www.reddit.com/r/reactjs/comments/54gl72/why_use_state_vs_class_properties/">https://www.reddit.com/r/reactjs/comments/54gl72/why_use_state_vs_class_properties/</a><div id="articleHeader"><h1>Why use state vs class properties </h1></div><div><div><div><p>This is an archived post. You won't be able to vote or comment.</p>
</div>
</div><div id="siteTable"><div id="thing_t3_54gl72"><div><div><div><div><p>I'm very new to react. The tutorials and documentation online say to handle state variables in a component, use this.setState({});</p>

<p>But I just tested if using normal class properties on a component class (this.someprop = 5) would update the view when displayed in the render function, and it did. When I passed the class property to a child component as a component property, the child components view also updated accordingly.</p>

<p>If there is no difference I'd use the normal class properties because it's much less verbose to write. But I can't believe that to be true. So what am I missing?</p>
</div>
</div></div></div></div></div><div><div>all 7 comments</div><div><div>sorted by: </div></div><div id="siteTable_t3_54gl72"><div id="thing_t1_d81oyke"><div><p><a href="javascript:void(0)" target="_blank">[–]</a><a href="https://www.reddit.com/user/goshakkk" target="_blank">goshakkk</a> 6 points <time>1 year ago</time> <a href="javascript:void(0)" target="_blank">(0 children)</a></p><div><div><p>Are you sure there is nothing else causing the re-render? Like <code>forceUpdate</code>, any <code>setState</code> call, or its parent changing its props simultaneously? </p>

<p>Also, why the dislike of state? It draws a clear line between what's just there (e.g. an interval ID that you set somewhere) and what influences the rendering in some way.</p>
</div>
</div></div></div><div id="thing_t1_d81tvso"><div><p><a href="javascript:void(0)" target="_blank">[–]</a><a href="https://www.reddit.com/user/acemarke" target="_blank">acemarke</a> 5 points <time>1 year ago</time> <a href="javascript:void(0)" target="_blank">(0 children)</a></p><div><div><p>There are three things that cause a React component to re-render:</p>

<ul>
<li>The parent component re-rendered</li>
<li>The component called <code>this.setState()</code></li>
<li>The component called <code>this.forceUpdate()</code></li>
</ul>

<p>Setting a field directly on the component instance, like <code>this.someField = 42</code>, will <em>not</em> cause the component to actually re-render.</p>

<p>One of the core concepts of React is that a component's render output should be solely based on its props and state.  So, if you want to use something for rendering, you should put it in state, and the correct way to do that is with <code>this.setState()</code>.</p>

<p>I have a big list of links to high-quality tutorials on React and related topics, at <a href="https://github.com/markerikson/react-redux-links" target="_blank">https://github.com/markerikson/react-redux-links</a> .  There's a number of articles related to good use of <code>setState</code> in the <a href="https://github.com/markerikson/react-redux-links/blob/master/react-redux-architecture.md#react-component-management" target="_blank">React Architecture</a> category (which has gotten kind of big, and I really need to reorganize).  In particular, you might want to read <a href="https://medium.com/react-ecosystem/how-to-handle-state-in-react-6f2d3cd73a0c" target="_blank">How to handle state in React</a> and <a href="https://medium.freecodecamp.com/where-do-i-belong-a-guide-to-saving-react-component-data-in-state-store-static-and-this-c49b335e2a00" target="_blank">Where to Hold React Component Data</a>.</p>
</div>
</div></div></div><div id="thing_t1_d81r61f"><div><p><a href="javascript:void(0)" target="_blank">[–]</a><a href="https://www.reddit.com/user/GOT_IT_FOR_THE_LO_LO" target="_blank">GOT_IT_FOR_THE_LO_LO</a> 4 points <time>1 year ago</time> <a href="javascript:void(0)" target="_blank">(0 children)</a></p><div><div><p>I think there's some sort of side effect that happens to be re-rendering your component. Changing a property on a the component class should NOT cause a re-render.</p>

<p><code>this.setState</code> is verbose to ensure it's more explicit when the component's state is changing. This will make your life much easier in the future.</p>
</div>
</div></div></div><div id="thing_t1_d82a357"><div><p><a href="javascript:void(0)" target="_blank">[–]</a><a href="https://www.reddit.com/user/prewk" target="_blank">prewk</a> 4 points <time>1 year ago</time> <a href="javascript:void(0)" target="_blank">(1 child)</a></p><div><div><p>For the record; There's nothing inherently wrong in using class properties in React, they're just not part of state in the same manner as <code>setState</code> data is.</p>

<p>It is in fact often very useful to keep certain things out of state, but on the class, such as a timer id (<code>this.myTimer = setTimeout(..)</code>) for later clear in <code>componentWillUnmount</code> (<code>clearTimeout(this.myTimer)</code>).</p>
</div>
</div></div></div><div id="thing_t1_d81s5sb"><div><p><a href="javascript:void(0)" target="_blank">[–]</a><a href="https://www.reddit.com/user/SeerUD" target="_blank">SeerUD</a> 1 point <time>1 year ago</time> <a href="javascript:void(0)" target="_blank">(0 children)</a></p><div><div><p>I suppose one thing would be that certain life cycle methods wouldn't work. You wouldn't be able to react to some new state vs some old state without it. Take shouldComponentUpdate for example.</p>
</div>
</div></div></div><div id="thing_t1_d82thkh"><div><p><a href="javascript:void(0)" target="_blank">[–]</a><a href="https://www.reddit.com/user/Vae-victus" target="_blank">Vae-victus</a> 1 point <time>1 year ago</time> <a href="javascript:void(0)" target="_blank">(0 children)</a></p><div><div><p>if you would like this behaviour, use mobx. set your component as an @observer, and properties as @observable and you're set</p>
</div>
</div></div></div></div></div></div><div><h3>Like On Github</h3><div><div>*Title (label for the link)</div></div><div><div>*Comment (commit message)</div></div><div id="action-btns"><div id="logh_btn_save">Saving...</div><div id="logh_btn_cancel">Cancel</div></div></div>
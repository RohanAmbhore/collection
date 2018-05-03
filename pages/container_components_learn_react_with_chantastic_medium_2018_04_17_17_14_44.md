<a href="https://medium.com/@learnreact/container-components-c0e67432e005">https://medium.com/@learnreact/container-components-c0e67432e005</a><div id="articleHeader"><h1>Container Components</h1></div><p id="f51f">One React pattern that’s had the impact on my code is the <em>container component</em> pattern.</p><p id="7e3e">In Jason Bonta talk High Performance Components, there’s <a href="https://www.youtube.com/watch?v=KYzlpRvWZ6c&t=1351" target="_blank">this little gem about container components</a>.</p><p id="02d2">The idea is simple:</p><blockquote id="2a96">A container does data fetching and then renders its corresponding sub-component. That’s it.</blockquote><p id="a286">“Corresponding” meaning a component that shares the same name:</p><pre id="0d02">StockWidgetContainer =&gt; <strong>StockWidget</strong><br />TagCloudContainer =&gt; <strong>TagCloud</strong><br />PartyPooperListContainer =&gt; <strong>PartyPooperList</strong></pre><p id="68fb">You get the idea.</p><h3 id="176e">Why containers?</h3><p id="935d">Say you have a component that displays comments. You didn’t know about <em>container components</em>. So, you put everything in one place:</p><pre id="cde1">class <strong>CommentList</strong> extends React.Component {<br />  this.state = { comments: [] };<br /><br />componentDidMount() {<br />    fetchSomeComments(comments =&gt;<br />      this.setState({ comments: comments }));<br />  }</pre><pre id="0ac1">  render() {<br />    return (<br />      &lt;ul&gt;<br />        {this.state.comments.map(c =&gt; (<br />          &lt;li&gt;{c.body}—{c.author}&lt;/li&gt;<br />        ))}<br />      &lt;/ul&gt;<br />    );<br />  }<br />}</pre><p id="9fcd">Your component is responsible for both fetching data and presenting it. There’s nothing “wrong” with this but you miss out on a few benefits of React.</p><h4 id="b1a9">Reusability</h4><p id="fd8e"><strong>CommentList</strong> can’t be reused unless under the exact same circumstances.</p><h4 id="47af">Data structure</h4><p id="8ade">Your markup components should state expectations of the data they require. <a href="http://facebook.github.io/react/docs/reusable-components.html" target="_blank">PropTypes</a> are great for this.</p><p id="b233">Our component is opinionated about data structure but has no way of expressing those opinions. This component will break silently if the json endpoint change.</p><h3 id="be38">Once again. This time with a container</h3><p id="1380">First, lets pull out data-fetching into a <em>container component.</em></p><pre id="00d6">class <strong>CommentListContainer</strong> extends React.Component {<br />  state = { comments: [] };</pre><pre id="228e">  componentDidMount() {<br />    fetchSomeComments(comments =&gt;<br />      this.setState({ comments: comments }));<br />  }</pre><pre id="8348">  render() {<br />    return &lt;<strong>CommentList</strong> comments={this.state.comments} /&gt;;<br />  }<br />}</pre><p id="4c1e">Now, let’s rework CommentList to take <strong>comments</strong> as a prop.</p><pre id="fb26">const <strong>CommentList</strong> = props =&gt;<br />  &lt;ul&gt;<br />    {props.comments.map(c =&gt; (<br />      &lt;li&gt;{c.body}—{c.author}&lt;/li&gt;<br />    ))}<br />  &lt;/ul&gt;</pre><p id="d13a"><a href="http://codepen.io/chantastic/pen/Qpeevw?editors=0010" target="_blank"><em>Example Codepen</em></a></p><h3 id="1eee">So, what did we get?</h3><p id="a449">We actually got a lot…</p><p id="3e3c">We’ve separated our <strong>data-fetching</strong> and <strong>rendering</strong> concerns.</p><p id="2112">We’ve made our CommentList component <strong>reusable</strong>.</p><p id="be78">We’ve given CommentList the ability to set <strong>PropTypes</strong> and fail loudly.</p><p id="aeef">I’m a big fan of container components. They’re stepping up my React game a lot and making my components easier to read. Give them a try and <a href="https://www.youtube.com/watch?v=KYzlpRvWZ6c" target="_blank">watch Jason’s talk</a>. It’s excellent!</p><p id="f559">Carry on, nerds.</p>
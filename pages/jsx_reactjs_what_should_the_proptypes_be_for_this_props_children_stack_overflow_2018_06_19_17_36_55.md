<a href="https://stackoverflow.com/questions/42122522/reactjs-what-should-the-proptypes-be-for-this-props-children">https://stackoverflow.com/questions/42122522/reactjs-what-should-the-proptypes-be-for-this-props-children</a><div id="articleHeader"><h1>ReactJs: What should the PropTypes be for this.props.children?</h1></div>

<p>Given a simple component that renders its children:</p>

<pre><code>class ContainerComponent extends Component {
  static propTypes = {
    children: PropTypes.object.isRequired,
  }

  render() {
    return (
      &lt;div&gt;
        {this.props.children}
      &lt;/div&gt;
    );
  }
}

export default ContainerComponent;
</code></pre>

<p><strong>Question: What should the propType of the children prop be?</strong></p>

<p>When I set it as an object, it fails when I use the component with multiple children:</p>

<pre><code>&lt;ContainerComponent&gt;
  &lt;div&gt;1&lt;/div&gt;
  &lt;div&gt;2&lt;/div&gt;
&lt;/ContainerComponent&gt;
</code></pre>

<blockquote>
  <p>Warning: Failed prop type: Invalid prop <code>children</code> of type <code>array</code>
  supplied to <code>ContainerComponent</code>, expected <code>object</code>.</p>
</blockquote>

<p>If I set it as an array, it will fail if I give it only one child, i.e.: </p>

<pre><code>&lt;ContainerComponent&gt;
  &lt;div&gt;1&lt;/div&gt;
&lt;/ContainerComponent&gt;
</code></pre>

<blockquote>
  <p>Warning: Failed prop type: Invalid prop children of type object
  supplied to ContainerComponent, expected array.</p>
</blockquote>

<p>Please advise, should I just not bother doing a propTypes check for children elements?</p>
    
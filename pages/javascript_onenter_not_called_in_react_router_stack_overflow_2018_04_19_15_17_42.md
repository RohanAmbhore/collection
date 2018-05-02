<a href="https://stackoverflow.com/questions/42768620/onenter-not-called-in-react-router">https://stackoverflow.com/questions/42768620/onenter-not-called-in-react-router</a><div id="articleHeader"><h1>onEnter not called in React-Router</h1></div>

<p>Ok, I'm fed up trying.<br />
The <code>onEnter</code> method doesn't work. Any idea why is that? </p>

<pre><code>// Authentication "before" filter
function requireAuth(nextState, replace){
  console.log("called"); // =&gt; Is not triggered at all 
  if (!isLoggedIn()) {
    replace({
      pathname: '/front'
    })
  }
}

// Render the app
render(
  &lt;Provider store={store}&gt;
      &lt;Router history={history}&gt;
        &lt;App&gt;
          &lt;Switch&gt;
            &lt;Route path="/front" component={Front} /&gt;
            &lt;Route path="/home" component={Home} onEnter={requireAuth} /&gt;
            &lt;Route exact path="/" component={Home} onEnter={requireAuth} /&gt;
            &lt;Route path="*" component={NoMatch} /&gt;
          &lt;/Switch&gt;
        &lt;/App&gt;
      &lt;/Router&gt;
  &lt;/Provider&gt;,
  document.getElementById("lf-app")</code></pre>

<p>Edit: </p>

<p>The method is executed when I call <code>onEnter={requireAuth()}</code>, but obviously that is not the purpose, and I also won't get the desired parameters. </p>
    
<a href="https://stackoverflow.com/questions/45122800/react-router-switch-behavior">https://stackoverflow.com/questions/45122800/react-router-switch-behavior</a><div id="articleHeader"><h1>React router Switch behavior</h1></div>

<p>(<code>react-router-dom</code> version: 4.1.1)</p>

<p>I have working routes set up, but I'm a bit confused about why the <code>&lt;Switch&gt;</code> was necessary:</p>

<p>index.js</p>

<pre><code>import React from 'react';
import { HashRouter, Route, Switch } from 'react-router-dom';

import App from './components/App.jsx';
import FridgePage from './components/FridgePage.jsx';

ReactDOM.render(
    &lt;HashRouter&gt;
        &lt;Switch&gt;
            &lt;Route exact path="/" component={App} /&gt;
            &lt;Route path="/fridge" component={FridgePage} /&gt;
        &lt;/Switch&gt;
    &lt;/HashRouter&gt;,
    document.getElementById('root')
)
</code></pre>

<p>App.jsx</p>

<pre><code>import Header from './Header.jsx';
import {Link} from 'react-router-dom';

export default class App extends React.Component {
    render() {
        console.log(this.props);
        return (
            &lt;div&gt;
                &lt;h1&gt;Herbnew&lt;/h1&gt;
                &lt;Link to="fridge"&gt;Fridge&lt;/Link&gt;
                {this.props.children}
            &lt;/div&gt;
        );
    }
}
</code></pre>

<p>FridgePage.jsx</p>

<pre><code>import React from 'react';

export default class FridgePage extends React.Component {
    render() {
        return (
            &lt;div&gt;
                &lt;h1&gt;Fridge&lt;/h1&gt;
                You finally found the fridge!
            &lt;/div&gt;
        );
    }
}
</code></pre>

<p>I used to have a <code>div</code> wrapping the routes instead of a <code>Switch</code>. In that case, I see the <code>App</code> rendered and try to click the Fridge link, but nothing happens (the <code>FridgePage</code> isn't rendered), and no error is output into the console.</p>

<p>As I understand it, the only thing the <code>Switch</code> does is exclusively render the first route it matches, and the common problem as a result of omitting it is rendering both pages at once.  If my <code>"/"</code> route is exact, then even without the Switch, the Fridge should be the only route that matches, right? Why does it not render at all?</p>
    
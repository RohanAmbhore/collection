<a href="https://www.robinwieruch.de/create-react-app-mobx-decorators/">https://www.robinwieruch.de/create-react-app-mobx-decorators/</a><div id="articleHeader"><h1>MobX (with Decorators) in create-react-app</h1></div>

                            

                            <p>
    
        
    

    
        <time>
            October 10, 2017
        </time>
    

    
         - <a href="https://github.com/rwieruch/blog_robinwieruch_content/blob/master/create-react-app-mobx-decorators.md" target="_blank">
                Edit this Post on GitHub
            </a>
        
    
</p>

                            <div>
    <div>
        

        <div class="readableLargeImageContainer"><img src="/img/posts/create-react-app-mobx-decorators/banner_1024.jpg" alt="create-react-app mobx decorators" /></div>
    



<p>MobX is used for state management in modern applications. Often it is applied in a React.js application, but it is not necessarily bound to React. In addition, it is a <a href="https://www.robinwieruch.de/redux-mobx-confusion/" target="_blank">valuable alternative to Redux</a> as state management solution. If you are using <a href="https://github.com/facebookincubator/create-react-app" target="_blank">create-react-app</a> as your application boilerplate, you most likely run into the questions of how to setup MobX and how to use <a href="https://tc39.github.io/proposal-decorators/" target="_blank">decorators</a> in create-react-app. The article should give you the essential knowledge to use MobX without and with decorators in create-react-app.</p>

<h2 id="mobx-without-decorators">MobX in create-react-app without Decorators</h2>

<p>Basically using MobX without decorators in create-react-app is straight forward. After scaffolding your application with create-react-app on the command line, you can install <a href="https://github.com/mobxjs/mobx" target="_blank">mobx</a> and <a href="https://github.com/mobxjs/mobx-react" target="_blank">mobx-react</a>:</p>

<div><pre><code>npm install --save mobx mobx-react
</code></pre></div>


<p>Whereas the former is used as your state management solution, the latter is used to connect the state layer to your React view layer. Now you can use it to create state containers or, as in the following example, to leverage local component state instead of using React’s local state:</p>

<div><pre><code>import React, { Component } from 'react';
import { extendObservable } from 'mobx';
import { observer }  from 'mobx-react';

class App extends Component {
  constructor() {
    super();

    extendObservable(this, {
      counter: 0,
    })
  }

  onIncrement = () =&gt; {
    this.counter++;
  }

  onDecrement = () =&gt; {
    this.counter--;
  }

  render() {
    return (
      &lt;div&gt;
        {this.counter}

        &lt;button onClick={this.onIncrement} type="button"&gt;Increment&lt;/button&gt;
        &lt;button onClick={this.onDecrement} type="button"&gt;Decrement&lt;/button&gt;
      &lt;/div&gt;
    );
  }
}

export default observer(App);
</code></pre></div>


<p>Whereas the <code>extendObservable</code> makes sure to create an observable value, the <code>observer</code> makes sure that the <code>App</code> component reacts when an observable value changes. The reaction leads to a re-rendering of the component. After all, that would be all the essentials to use MobX without decorators in create-react-app.</p>

<h2 id="create-react-app-mobx">Alternative Boilerplate: create-react-app-mobx</h2>

<p>There exist a boilerplate project on GitHub, <a href="https://github.com/mobxjs/create-react-app-mobx" target="_blank">create-react-app-mobx</a>, that is maintained by Michel Weststrate the creator of MobX. It has MobX installed in a create-react-app bootstrapped application. The following commands are the installation instructions for the command line:</p>

<div><pre><code>git clone git@github.com:mobxjs/create-react-app-mobx.git
cd create-react-app-mobx
npm install
npm start
</code></pre></div>


<p>After that, you should find the running application in your browser. Furthermore, the GitHub repository is providing a git patch commit that you can use to upgrade your plain create-react-app to use MobX.</p>

<h2 id="mobx-with-decorators">But what about Decorators?</h2>

<p>Basically everything shown before demonstrates that MobX can be used without decorators at all. The <a href="https://mobx.js.org/best/decorators.html" target="_blank">official MobX documentation</a> showcases it as well. If someone says you have to use decorators in MobX, it isn’t true. You can use plain functions for it. So why using decorators?</p>

<p><strong>Advantages of using decorators:</strong></p>

<ul>
<li>minimizes boilerplate</li>
<li>declarative</li>
<li>easy to use and read</li>
<li>popular when using MobX</li>
</ul>

<p><strong>Disadvantages of using decorators:</strong></p>

<ul>
<li>not in native Javascript available, therefore needs transpiling (e.g. via Babel)</li>
<li>unstable specification</li>
</ul>

<p>MobX is not the only library using decorators. There are plenty of them and most of them provide a non decorator solution too. Then you can use both variations. In MobX, both alternatives look like the following:</p>

<div><pre><code>import React, { Component } from 'react';
import { observer } from 'mobx-react';

// non decorator usage

class App extends Component {
  ...
}

export default observer(App);

// decorator usage

@observer class App extends Component {
  ...
}

export default App;
</code></pre></div>


<p>The annotation on a variable definition with <code>@observer class App</code> is the same as <code>observer(App)</code> if App is defined. That way it is possible to compose several decorators onto one component with solutions such as compose from the <a href="https://github.com/acdlite/recompose" target="_blank">recompose</a> library:</p>

<div><pre><code>import React, { Component } from 'react';
import { observer, inject } from 'mobx-react';
import { compose } from 'recompose';

// non decorator usage

class App extends Component {
  render() {
    const { foo } = this.props;
    ...
  }
}

export default compose(
  observer,
  inject('foo')
)(App);

// decorator usage

@inject('foo') @observer
class App extends Component {
  render() {
    const { foo } = this.props;
    ...
  }
}

export default App;
</code></pre></div>


<p>So what about decorators in React and create-react-app?</p>

<h2 id="decorators-create-react-app">Decorators in create-react-app</h2>

<p>The current situation is that the maintainers of create-react-app are holding decorators back until Babel supports them in a stable stage:</p>

<blockquote>
<p><em>“Our position is simple: we add transforms that are either stable enough (like async/await) or heavily used by Facebook (like class properties). Only that lets us be confident in suggesting them, because if something changes in the standard, we’ll write and release a codemod to migrate away from them.”</em> (related issues <a href="https://github.com/facebookincubator/create-react-app/issues/411" target="_blank">1</a> & <a href="https://github.com/facebookincubator/create-react-app/issues/214" target="_blank">2</a>)</p>
</blockquote>

<p>But what if you want to use decorators for your create-react-app + MobX application right now?</p>

<div><pre><code>import React, { Component } from 'react';
import { observable } from 'mobx';
import { observer }  from 'mobx-react';

@observer
class App extends Component {
  @observable counter = 0;

  onIncrement = () =&gt; {
    this.counter++;
  }

  onDecrement = () =&gt; {
    this.counter--;
  }

  render() {
    return (
      &lt;div&gt;
        {this.counter}

        &lt;button onClick={this.onIncrement} type="button"&gt;Increment&lt;/button&gt;
        &lt;button onClick={this.onDecrement} type="button"&gt;Decrement&lt;/button&gt;
      &lt;/div&gt;
    );
  }
}

export default App;
</code></pre></div>


<p>Running this code in a plain create-react-app application will yield a <code>Unexpected token</code> error in the developer console. You would have to add decorators to your Babel configuration. However, create-react-app doesn’t give you access to the Babel configuration. There is only one way to access it: ejecting.</p>

<p><strong>Basically there are four steps to use decorators in create-react-app:</strong></p>

<ul>
<li>type <code>npm run eject</code> on the command line, if you have bootstrapped your app with create-react-app</li>
<li>install the necessary Babel plugin <code>npm install --save-dev babel-plugin-transform-decorators-legacy</code></li>
<li>add the following Babel configuration to your <em>package.json</em></li>
</ul>

<div><pre><code>"babel": {
  "plugins": [
    "transform-decorators-legacy"
  ],
  "presets": [
    "react-app"
  ]
},
</code></pre></div>


<ul>
<li>install mobx and mobx-react, if you didn’t do it already <code>npm install --save mobx mobx-react</code></li>
</ul>

<p>Now you should be able to use the @ annotation in create-react-app. The previous example has shown how to use decorators for MobX’s local state management in a React component.</p>

<h2 id="create-react-app-avoid-eject">How to avoid eject when using Decorators</h2>

<p>There is one <a href="https://github.com/kitze/custom-react-scripts" target="_blank">fork with custom-react-scripts</a> of create-react-app on GitHub where you can avoid ejecting your application. You would only have to follow the instructions in the GitHub repository to set it up. I will not write them down here, because they might change in the future.</p>

<p>But the fork of create-react-app has one drawback. Whereas create-react-app was designed to give you a simple to use, powerful yet zero-configuration boilerplate project for React, the fork of it comes with more complex configurations. Ultimately it’s up to you to make the decision. It is a choice between ejecting your puristic create-react-app to only add decorators for your use case or to use the fork of create-react-app with custom-react-scripts to add overhaul more flexibility to configure your project.</p>

<h2 id="nextjs-mobx-decorators">MobX and Decorators in Next.js</h2>

<p>The article is mainly about MobX with and without decorators in create-react-app. But what about its alternative Next.js for server-side rendered React applications? Fortunately there exists <a href="https://github.com/zeit/next.js/tree/master/examples/with-mobx" target="_blank">one sample project</a> that already demonstrates how to use MobX with decorators in a Next.js application.</p>

<p>In addition, you have access to the .babelrc file to configure Babel in your Next.js application. In a newly bootstrapped Next.js application, you would enable MobX with decorators with these two steps. First, install the dependencies of MobX and the decorator transpilation to your project:</p>

<div><pre><code>npm install --save mobx mobx-react
npm install --save-dev babel-plugin-transform-decorators-legacy
</code></pre></div>


<p>Second, add the decorator support to your <em>.babelrc</em> file at the root of the project:</p>

<div><pre><code>{
  "presets": [
    "next/babel"
  ],
  "plugins": [
    "transform-decorators-legacy"
  ]
}
</code></pre></div>


<p>After all, the choice is again up to you. You can either clone the Next.js with MobX example project or add MobX with or without decorators on your own to it.</p>

<hr />

<p>After showing all these different alternatives, using MobX with or without decorators in a plain React, a create-react-app or Next.js application, you have no excuse anymnore to give MobX as alternative to Redux a shot. Try it in your next side project.</p>


                            
<div>
    <hr />
    
    <p>
        I would like to hear your thoughts :-) Find me on <a href="https://twitter.com/rwieruch" target="_blank">Twitter</a> and <a href="https://github.com/rwieruch" target="_blank">GitHub</a>
    </p>
    
    
        <p>
            Did the article help you? You can share it with your friends on social media , support me on <a href="https://www.patreon.com/rwieruch" target="_blank">Patreon</a> or take one of my courses 
        </p>
    
</div>


                            
                                <div>
    <div>
        <h2>The Road to learn React</h2>
        
            <div>
                <img src="https://www.robinwieruch.de/img/page/cover.png" />
            </div>
        
        <p>
            Build a Hacker News App along the way. No setup configuration. No tooling. No Redux. Plain React in 190+ pages of learning material. Learn React like <strong>21.000+ readers</strong>.
        </p>
        <a href="https://www.getrevue.co/profile/rwieruch" target="_blank">
            Get the Book 
        </a>
    

                            
                        
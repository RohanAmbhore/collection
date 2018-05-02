<a href="https://semaphoreci.com/community/tutorials/testing-react-components-with-enzyme-and-mocha">https://semaphoreci.com/community/tutorials/testing-react-components-with-enzyme-and-mocha</a><div id="articleHeader"><h1>Testing React Components with Enzyme and Mocha</h1></div>

            <p>Get familiar with React.js, an increasingly popular JavaScript development tool, and learn to test simple React components using enzyme and Mocha.</p>

          

          
            <div>
  <strong>Brought to you by</strong>
  
  <h3>Semaphore</h3>
  <a href="https://semaphoreci.com" id="semaphore-learn-more" target="_blank">Learn More</a>
</div>


            
              <h2>Introduction</h2>

<p>React has become an increasingly popular and widely-used JavaScript
application tool for developing web applications. Popular frameworks like
Angular.js, Ember.js, and Backbone have traditionally been go-to choices for
front-end application development, but React came onto the scene in 2013 and
provided front-end engineers with another substantial alternative.</p>

<p>React was developed at Facebook in part as a response to what seemed to be a
particularly complicated codebase. As such, it has simplicity baked into its
design and API. With this simplicity come some key differences from
libraries and frameworks in the same space. Despite some fundamental
differences, React applications need testing just like any other software. We
will take a quick look at React and some tools you can use to test React
components.</p>

<p>By the end of this article, you should:</p>

<ul>
<li>Have a basic understanding of React.js</li>
<li>Know how to test simple React components using enzyme and Mocha</li>
<li>Understand different aspects of testing front-end applications</li>
</ul>

<p>The full source code for this tutorial can be found <a href="https://github.com/markthethomas/react-testing-components-enzyme" target="_blank">here</a>.</p>

<h2>Prerequisites</h2>

<ul>
<li>Node.js (available <a href="https://nodejs.org" target="_blank">here</a> or via <a href="https://github.com/creationix/nvm" target="_blank">nvm</a>
</li>
<li>npm (comes bundled with node)</li>
</ul>

<h2>React in 30 Seconds</h2>

<p>Simply put, React is technology for building user interfaces. Here are a few of
its notable characteristics:</p>

<ul>
<li>
<strong>UI-centric</strong>: React is not a framework and it has a fairly minimal API
surface. It is "just the view" and leaves you to make your own choices about
other concerns (application architecture, AJAX, etc.).</li>
<li>
<strong>Static mental model</strong>: This means that you can think of the application
state in a static, declarative way, rather than having to work through or keep
track of a series of mutations to the state in your head.</li>
<li>
<strong>Components:</strong> It is component-focused, and components are the primary
currency of React.</li>
<li>
<strong>Virtual DOM</strong>: React implements a virtual DOM and performs updates to the
real DOM in an efficient and performant way, so you do not have to. You are
freed up from dealing with view-binding logic, and can focus on key parts of
your application.</li>
<li>
<strong>Performance</strong>: React's use of a virtual DOM and other performance-conscious
designs ensure most React applications are incredibly fast and memory-efficient.
The virtual DOM is more about simplicity than performance, but it also plays a
role in contributing to good performance.</li>
<li>
<strong>JSX</strong>: You can write the markup for your components in <a href="https://facebook.github.io/jsx/" target="_blank">JSX</a>,
which allows you to completely bundle your components and create familiar
HTML-like view markup.</li>
<li>
<strong>One-way data-flow</strong>: Data flows through React from parent to child
components, meaning you do not have to deal with potentially confusing
bidirectional data-flow. Components are also further decoupled from each other,
as data is only passed down in place of side-effects.</li>
</ul>

<p>Now that we know a little bit about React, we can start to look at the testing
tools available to us and how we might go about testing a simple React
component.</p>

<h2>Testing Tools for React</h2>

<p>In many ways, testing front-end applications is no different from testing
server-side, or other types of software. Like always, there exists a spectrum of
testing types, and a well-tested application will be tested across the
applicable types. Generally, the two "ends" of the spectrum are unit and
end-to-end or system testing, with unit testing being the most "low-level" or
specific, and end-to-end being the most integrated and "high-level".</p>

<p>For example, more integrated, high-level tests for a back-end application might
involve interacting with other applications across the network barrier, or
mutating data in a test database. With front-end applications, an end-to-end
test will be more focused on user interaction and dealing with inputs, events,
and the like. Unit-testing in front-end applications is more similar to
unit-testing in general, as it focuses on the smallest units of an application,
and generally aims to determine correctness, e.g. "does a function return the
right value and type?".</p>



<p>One of the main source of challenges for testing front-end applications is
sometimes the nature of advanced technologies like Angular, Ember, and React. It
is not enough to simply <code>document.getElementById('myElement')</code>, run some
assertions against it, and move on. Most modern JavaScript application
technologies are doing far more advanced things than jQuerying-up
otherwise-static web pages. For example, React implements a virtual DOM as one
of its key components. So, ensuring that your components are rendering,
receiving props and state, and updating properly means end-to-end tests need to
be suited to React.</p>

<p>Specialized testing tools often need to be created for these sorts of
specialized frameworks and libraries. For example, you might have used or heard
of <a href="https://angular.github.io/protractor/#/" target="_blank">Protractor</a>, the end-to-end testing
tool from the Angular.js team. While it can be used for a wide variety of
projects, it takes special care to be oriented towards testing Angular
applications.</p>

<p>As it turns out, the "standard" tool for testing React applications, <a href="https://facebook.github.io/jest/" target="_blank">Jest</a>,
is still evolving along with the rest of the React ecosystem, making it a
somewhat difficult tool to teach and recommend to those who want to learn about
React and front-end testing. It also brings with it some features — for instance
auto-mocking — , that are a little too heavy for the purposes of a tutorial, and
might hinder our progress while learning about testing React components.</p>

<h3>Enzyme + Mocha</h3>

<p>We will move forward with what is likely to be a familiar tool to JavaScript
developers — <a href="https://mochajs.org/" target="_blank">Mocha</a>, and a well-developed new React
testing library called <a href="http://airbnb.io/enzyme/" target="_blank">enzyme</a>.</p>

<p>Mocha is a well-known and flexible test runner that you can use to run your
JavaScript tests on the server or in the browser. Enzyme, created by engineers
at Airbnb, is "a JavaScript Testing utility for React that makes it easier to
assert, manipulate, and traverse your React Components' output."</p>

<p>One of the nice things about this pairing is that you can substitute your
favorite testing framework for Mocha (<a href="https://github.com/substack/tape" target="_blank">tape</a>,
<a href="https://github.com/sindresorhus/ava" target="_blank">AVA</a>, <a href="http://jasmine.github.io/" target="_blank">Jasmine</a>,
etc.), and still be able to test your React application. Furthermore, because
of the way that React-Native is currently built with a dependency on the actual
React library, you can use Enzyme to test your React Native applications, too.</p>

<h2>Getting Set Up</h2>

<p>To keep up with the latest ECMAScript standard, we will be writing nearly all of
our code in the ES6 manner. Many aspects of the new ES6 specification do not yet
have native support, so we will use the popular <a href="https://babeljs.io/" target="_blank">Babel</a>
transpilation tools to ensure our code is able to run in browsers today. We will
also use <a href="https://webpack.github.io/" target="_blank">Webpack</a> to ensure everything gets
properly bundled together and can run in the browser in a single file. Babel and
Webpack are extremely flexible and complex tools in their own right, so we will
only be covering a very basic setup and usage of them.</p>

<p>Before we start, make sure that you have all the needed prerequisites installed
and have run <code>git init</code> in your directory. The directory structure we will use
will look like this:</p>

<pre><code>├── LICENSE
├── README.md
├── dist
├── lib
├── package.json
├── test
└── webpack.config.js
</code></pre>

<h3>Babel</h3>

<p>The Babel transpilation toolset lets you turn your ES6 code to ES5. To get it
working, first we will need to install some libraries:</p>

<div><pre>$ npm install --save babel-core babel-loader babel-preset-airbnb babel-preset-es2015 babel-preset-react babel-preset-stage-0
</pre></div>

<p><strong>Note</strong>: Feel free to refer to this <a href="https://github.com/markthethomas/react-testing-components-enzyme/blob/master/package.json" target="_blank">package.json</a>
to make sure all your npm modules are installed or see the full list of modules used throughout this tutorial.</p>

<p>We can break down the modules we just installed a little further:</p>

<ul>
<li>The key one is <code>babel-core</code>, which as you might guess is the core babel
library.</li>
<li>
<code>babel-loader</code> is a loader plugin for Webpack.</li>
<li>The rest of the libraries are presets for Babel that allow tuning and
customization.</li>
</ul>

<p>We also need to create a <code>.babelrc</code> dotfile in the root of your repository:</p>

<pre><code>{
  "presets": ["airbnb", "es2015", "stage-0"]
}
</code></pre>

<h3>Configuring Webpack</h3>

<p>Now that we have Babel set up and installed some of the presets will need, we
can configure Webpack. Webpack is a module bundling tool that we can use to
ensure all of our different files get combined into one meaningful file we can
use in the browser. As with Babel, Webpack is also a tool that deserves an
entire tutorial in its own right, so we will not be going through every aspect
of how it works or how to configure it.</p>

<p>First, let's ensure we have installed Webpack and the Webpack development
server:</p>

<div><pre>$ npm install --save-dev webpack webpack-dev-server
</pre></div>

<p>Next, we need to create a configuration file for Webpack. It will contain
options that will tell Webpack how to bundle our files, where the output should
go, and other customizations.</p>

<p><strong>webpack.config.js</strong></p>

<div><pre>const path = require('path');
const webpack = require('webpack');

// env
const buildDirectory = './dist/';

module.exports = {
  entry: './lib/main.jsx',
  devServer: {
    hot: true,
    inline: true,
    port: 7700,
    historyApiFallback: true,
  },
  resolve: {
    extensions: ['', '.js', '.jsx'],
  },
  output: {
    path: path.resolve(buildDirectory),
    filename: 'app.js',
    publicPath: 'http://localhost:7700/dist',
  },
  externals: {
    'cheerio': 'window',
    'react/lib/ExecutionEnvironment': true,
    'react/lib/ReactContext': true,
  },
  module: {
    loaders: [{
      test: /\.jsx?$/,
      exclude: /(node_modules|bower_components)/,
      loader: 'babel',
      query: {
        presets: ['react', 'es2015', 'stage-0'],
      },
    }],
  },
  plugins: [],
};
</pre></div>

<p>A few sections are worth looking more closely at to ensure we understand the
general idea of what we are telling Webpack to do.</p>

<p>This section is simply how we tell Webpack to create the final output of our
application script. We are also telling Webpack that we will make our script
publicly available at <code>http://localhost:7700/dist</code>:</p>

<div><pre>  output: {
    path: path.resolve(buildDirectory),
    filename: 'app.js',
    publicPath: 'http://localhost:7700/dist',
  },
</pre></div>

<p>This part of <code>webpack.config.js</code> will configure webpack-dev-server, which is an
extremely helpful tool that will serve up and help recompile our script for us
as we work:</p>

<div><pre>  devServer: {
    hot: true,
    inline: true,
    port: 7700,
    historyApiFallback: true,
  },
</pre></div>

<p>The last part of the webpack configuration we will spend some time on is
<code>externals</code>. These will help enable enzyme to work properly.</p>

<div><pre>externals: {
    'cheerio': 'window',
    'react/lib/ExecutionEnvironment': true,
    'react/lib/ReactContext': true,
  },
</pre></div>

<h3>Creating Our Index.html</h3>

<p>Next, we need to create a simple <code>index.html</code> file that we can open in a browser
to see what our component looks like. This file will only do a few things:
include our script, provide a render target, and include some boilerplate CSS.</p>

<p><strong>index.html</strong></p>

<div><pre>&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;Fun with react testing!&lt;/title&gt;
  &lt;meta charset="utf-8"&gt;
  &lt;meta http-equiv="X-UA-Compatible" content="IE=edge"&gt;
  &lt;meta name="viewport" content="width=device-width, minimum-scale=1.0"&gt;
  &lt;meta name="author" content="Mark Thomas"&gt;
  &lt;link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css"&gt;
&lt;/head&gt;

&lt;body&gt;
  &lt;div id="root"&gt;
    &lt;h1&gt;
      Loading!
    &lt;/h1&gt;
  &lt;/div&gt;
  &lt;script src='http://localhost:7700/dist/app.js'&gt;&lt;/script&gt;
&lt;/body&gt;

&lt;/html&gt;
</pre></div>

<p>After creating this file, your project directory should look like this:</p>

<pre><code>├── LICENSE
├── README.md
├── dist
├── index.html
├── lib
├── package.json
├── test
└── webpack.config.js
</code></pre>

<h3>Mocha and Company</h3>

<p>The last setup we need to do before we are ready to start writing our tests is
install mocha and some other modules to ensure we have everything ready for it
to run our enzyme tests.</p>

<p>We will install rest of testing tools: Mocha, jsdom, and
react-addons-test-utils. Enzyme needs 'react-addons-test-utils' and 'jsdom'
for some of its functionality in the way we will be using it.</p>

<div><pre>$ npm install --save-dev mocha jsdom react-addons-test-utils
</pre></div>

<p>Lastly, we will create a setup file that will ensure we can test our components
in a realistic browser environment using <a href="https://github.com/tmpvar/jsdom" target="_blank">jsdom</a>.</p>

<p><strong>test/helpers/browser.js</strong>[^1]</p>

<div><pre>require('babel-register')();

var jsdom = require('jsdom').jsdom;

var exposedProperties = ['window', 'navigator', 'document'];

global.document = jsdom('');
global.window = document.defaultView;
Object.keys(document.defaultView).forEach((property) =&gt; {
  if (typeof global[property] === 'undefined') {
    exposedProperties.push(property);
    global[property] = document.defaultView[property];
  }
});

global.navigator = {
  userAgent: 'node.js'
};

documentRef = document;
</pre></div>

<p>Our setup is now complete. We can run our tests with <code>npm test</code> and run our dev
server with <code>npm run dev:hot</code> by adding these scripts to our <code>package.json</code>:</p>

<div><pre>  "scripts": {
    "test": "mocha -w test/helpers/browser.js test/*.spec.js",
    "dev:hot": "webpack-dev-server --hot --inline --progress --colors --watch --display-error-details --display-cached --content-base ./"
  },
</pre></div>

<p>When you run <code>npm run dev:hot</code>, you will see Webpack bundling up all your assets
together into different chunks. Any errors in importing or exporting data will
cause it to throw an error and report it to you in the terminal.</p>

<h2>Testing Components</h2>

<p>Now that we have completely finished setting up our tools, we can get to writing
some tests. We will be creating a very simple component that will grab a profile
image from <a href="http://en.gravatar.com/" target="_blank">Gravatar</a> when a user puts their email in
and clicks a "fetch" button. Our tests will need to reflect these external
requirements and will serve as a guide once we start building the actual
components. One great thing about letting tests guide our development is that
when all of our tests pass, we can be fairly confident in our code and we know
we are done.</p>

<p>Our main component will have two sub-components that we want to test
individually. We will create one for the avatar image that will be displayed,
and one for the email input. If we were working on a full React application, we
might find other places to reuse and repurpose these components, or find that
they already existed in some form.</p>

<p>This is the test for the avatar component.
<strong>avatar.spec.js</strong></p>

<div><pre>import React from 'react';
import { mount, shallow } from 'enzyme';
import {expect} from 'chai';

import Avatar from '../lib/avatar';

describe('&lt;Avatar/&gt;', function () {
  it('should have an image to display the gravatar', function () {
    const wrapper = shallow(&lt;Avatar/&gt;);
    expect(wrapper.find('img')).to.have.length(1);
  });

  it('should have props for email and src', function () {
    const wrapper = shallow(&lt;Avatar/&gt;);
    expect(wrapper.props().email).to.be.defined;
    expect(wrapper.props().src).to.be.defined;
  });
});
</pre></div>

<p>Take note of this line, which you will see repeated in one form or another in
our other tests:</p>

<div><pre>const wrapper = shallow(&lt;Avatar/&gt;);
</pre></div>

<p>The <code>shallow</code> method from enzyme will allow us to "shallowly" render a
component. This type of rendering is used to isolate one component for testing
and ensure child components do not affect assertions. You can think of it as
rendering "just" the component you want it to.</p>

<p>Enzyme gives us several ways to render components for testing: using <code>shallow</code>,
<code>mount</code>, and <code>static</code>. We have already discussed shallow rendering. Mount is
"real" rendering that will actually render your component into a browser
environment. If you are creating full React components (and not just stateless
components), you will want to use <code>mount</code> to do testing on the lifecycle
methods of your component. We are using jsdom to accomplish rendering in a
browser-like environment, but you could just as easily run it in a browser of
your choosing.</p>

<p>The last major top-level rendering method enzyme gives us <code>static</code>, which is
used for analyzing the actual HTML output of a component and will not be used in
our tests. Both <code>shallow</code> and <code>mount</code> return wrappers that give us many helpful
methods we can use to find child components, check props, set state, and perform
other testing tasks. We will use <a href="http://chaijs.com/" target="_blank">chai</a>'s
<code>expect</code> assertion-style on these methods in our tests.</p>

<p>Now that we know a little bit more about how to use enzyme, we can finish up our
tests:</p>

<p><strong>email.spec.js</strong> This is the spec for the email component</p>

<div><pre>import React from 'react';
import { mount, shallow } from 'enzyme';
import {expect} from 'chai';

import Email from '../lib/email';

describe('&lt;Email&gt;', function () {
  it('should have an input for the email', function () {
    const wrapper = shallow(&lt;Email/&gt;);
    expect(wrapper.find('input')).to.have.length(1);
  });

  it('should have a button', function () {
    const wrapper = shallow(&lt;Email/&gt;);
    expect(wrapper.find('button')).to.have.length(1);
  });

  it('should have props for handleEmailChange and fetchGravatar', function () {
    const wrapper = shallow(&lt;Email/&gt;);
    expect(wrapper.props().handleEmailChange).to.be.defined;
    expect(wrapper.props().fetchGravatar).to.be.defined;
  });
});
</pre></div>

<p>Lastly, we need to create tests for the main component that will utilize the
other two components. Gravatar's API uses an <a href="https://en.wikipedia.org/wiki/MD5" target="_blank">MD5</a>
hash to obscure email addresses, so we will use the <strong>md5</strong> module to create a
hash of the email.</p>

<p><strong>gravatar.spec.js</strong> This is the main component we are building, and it should
contain the other two components we will create:</p>

<div><pre>import React from 'react';
import { mount, shallow } from 'enzyme';
import {expect} from 'chai';
import md5 from 'md5';

import Gravatar from '../lib/gravatar';
import Avatar from '../lib/avatar';
import Email from '../lib/email';

describe('&lt;Gravatar /&gt;', () =&gt; {
  it('contains an &lt;Avatar/&gt; component', function () {
    const wrapper = mount(&lt;Gravatar/&gt;);
    expect(wrapper.find(Avatar)).to.have.length(1);
  });

  it('contains an &lt;Email/&gt; component', function () {
    const wrapper = mount(&lt;Gravatar/&gt;);
    expect(wrapper.find(Email)).to.have.length(1);
  });

  it('should have an initial email state', function () {
    const wrapper = mount(&lt;Gravatar/&gt;);
    expect(wrapper.state().email).to.equal('someone@example.com');
  });

  it('should have an initial src state', function () {
    const wrapper = mount(&lt;Gravatar/&gt;);
    expect(wrapper.state().src).to.equal('http://placehold.it/200x200');
  });

  it('should update the src state on clicking fetch', function () {
    const wrapper = mount(&lt;Gravatar/&gt;);
    wrapper.setState({ email: 'hello@ifelse.io' });
    wrapper.find('button').simulate('click');
    expect(wrapper.state('email')).to.equal('hello@ifelse.io');
    expect(wrapper.state('src')).to.equal(`http://gravatar.com/avatar/${md5('markthethomas@gmail.com')}?s=200`);
  });
});
</pre></div>

<h3>Wrapping Up Our Tests</h3>

<p>Once you have finished writing your tests, your project directory should look
something like this:</p>

<pre><code>├── LICENSE
├── README.md
├── dist
├── index.html
├── lib
├── package.json
├── test
│   ├── avatar.spec.js
│   ├── email.spec.js
│   ├── gravatar.spec.js
│   └── helpers
│       └── browser.js
└── webpack.config.js
</code></pre>

<h2>Testing User Interactions</h2>

<p>Now that we have our tests set up and can run them via <code>npm test</code>, we can work
on building out our component. First, we need to create our sub-components:
<strong>avatar</strong> and <strong>email</strong>.</p>

<p>First, we can create the avatar component:</p>

<p><strong>avatar.jsx</strong></p>

<pre><code>import React, {PropTypes} from 'react';
export default class Avatar extends React.Component {
  render() {
    return (
      &lt;div className="avatar"&gt;
        &lt;p&gt;
          &lt;em&gt;{this.props.email}&lt;/em&gt;
        &lt;/p&gt;
        &lt;img src={this.props.src} className="img-rounded"/&gt;
      &lt;/div&gt;
    );
  }
}

Avatar.propTypes = {
  email: PropTypes.string,
  src: PropTypes.string,
};
</code></pre>

<p>Next, we will create our email component.</p>

<p><strong>Email.jsx</strong></p>

<pre><code>import React, {PropTypes} from 'react';
export default class Email extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      &lt;div className="form-group"&gt;
        &lt;input onChange={this.props.handleEmailChange} className="form-control" style={{
          width: 200
        }} type="text"/&gt;
        &lt;button onClick={this.props.fetchGravatar} className="btn-success btn "&gt;Fetch&lt;/button&gt;
      &lt;/div&gt;
    );
  }

Email.propTypes = {
  handleEmailChange: PropTypes.func,
  fetchGravatar: PropTypes.func,
};  
</code></pre>

<p>Lastly, we will create our main <code>&lt;Gravatar/&gt;</code> component that makes use of the
others we have created so far. It also uses a few simple functions to listen for
state changes and user click events. Note that these functions are passed as
props to our child components, keeping the view logic contained in our parent
component.</p>

<p><strong>Gravatar.jsx</strong></p>

<pre><code>import React, {propTypes} from 'react';
import md5 from 'md5';

import Avatar from './avatar';
import Email from './email';

export default class Gravatar extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      email: 'someone@example.com',
      src: 'http://placehold.it/200x200'
    }
  }

  updateGravatar() {
    this.setState({
      src: `http://gravatar.com/avatar/${md5(this.state.email)}?s=200`
    });
  }

  updateEmail(event) {
    this.setState({email: event.target.value});
  }

  render() {
    return (
      &lt;div className="react-gravatar"&gt;
        &lt;h4&gt;Avatar for:&lt;/h4&gt;
        &lt;Avatar email={this.state.email} src={this.state.src}/&gt;
        &lt;Email fetchGravatar={this.updateGravatar.bind(this)} handleEmailChange={this.updateEmail.bind(this)}/&gt;
      &lt;/div&gt;
    );
  }
}
</code></pre>

<p>If you run your tests again using <code>npm test</code>, you should get green results. Our
component is relatively small, but even at this scale you should be able to
notice that enzyme is a fairly speedy tool for testing components. End-to-end
tests or any that require a browser-like environment can often be slow to spin
up. While full integration tests will still likely be somewhat slower, enzyme's
shallow rendering allows for speedy unit-testing of components.</p>

<h3>Wrapping Up Creating Components</h3>

<p>At this point, your directory should be looking something like the following:</p>

<pre><code>├── LICENSE
├── README.md
├── dist
├── index.html
├── lib
│   ├── avatar.jsx
│   ├── email.jsx
│   ├── gravatar.jsx
│   └── main.jsx
├── package.json
├── test
│   ├── avatar.spec.js
│   ├── email.spec.js
│   ├── gravatar.spec.js
│   └── helpers
│       └── browser.js
└── webpack.config.js
</code></pre>

<h2>Summary</h2>

<p>We have worked through creating a simple component that will display the
gravatar image for a user based on the email they put in. We looked at testing
some static properties of components, hierarchy and existence of children, as
well as simulating some more integrational events like user clicks. Hopefully,
your appetite for writing elegant, testable React applications has been whetted,
and you are on your way to becoming a master of writing elegant, testable code
applications.</p>

<hr />

<p>[^1]: See <a href="https://github.com/lelandrichardson/enzyme-example-mocha" target="_blank">https://github.com/lelandrichardson/enzyme-example-mocha</a> for more
information</p>
            
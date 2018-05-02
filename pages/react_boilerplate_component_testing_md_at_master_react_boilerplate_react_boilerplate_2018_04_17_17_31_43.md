<a href="https://github.com/react-boilerplate/react-boilerplate/blob/master/docs/testing/component-testing.md">https://github.com/react-boilerplate/react-boilerplate/blob/master/docs/testing/component-testing.md</a><div id="articleHeader"><h1>Component testing</h1></div>
<p><a href="/react-boilerplate/react-boilerplate/blob/master/docs/testing/unit-testing.md" target="_blank">Unit testing your Redux actions and reducers</a> is nice, but you
can do even more to make sure nothing breaks your application. Since React is
the <em>view</em> layer of your app, let's see how to test Components too!</p>



<h2>Shallow rendering</h2>
<p>React provides us with a nice add-on called the Shallow Renderer. This renderer
will render a React component <strong>one level deep</strong>. Lets take a look at what that
means with a simple <code>&lt;Button&gt;</code> component...</p>
<p>This component renders a <code>&lt;button&gt;</code> element containing a checkmark icon and some
text:</p>
<div><pre>// Button.js

import React from 'react';
import CheckmarkIcon from './CheckmarkIcon';

function Button(props) {
  return (
    &lt;button className="btn" onClick={props.onClick}&gt;
      &lt;CheckmarkIcon /&gt;
      { React.Children.only(props.children) }
    &lt;/button&gt;
  );
}

export default Button;</pre></div>
<p><em>Note: This is a <a href="/react-boilerplate/react-boilerplate/blob/master/docs/js/README.md#architecture-components-and-containers" target="_blank">state<strong>less</strong> ("dumb") component</a></em></p>
<p>It might be used in another component like this:</p>
<div><pre>// HomePage.js

import Button from './Button';

class HomePage extends React.Component {
  render() {
    return(
      &lt;Button onClick={this.doSomething}&gt;Click me!&lt;/Button&gt;
    );
  }
}</pre></div>
<p><em>Note: This is a <a href="/react-boilerplate/react-boilerplate/blob/master/docs/js/README.md#architecture-components-and-containers" target="_blank">state<strong>ful</strong> ("smart") component</a>!</em></p>
<p>When rendered normally with the standard <code>ReactDOM.render</code> function, this will
be the HTML output
(<em>Comments added in parallel to compare structures in HTML from JSX source</em>):</p>
<div><pre>&lt;button&gt;                           &lt;!-- &lt;Button&gt;             --&gt;
  &lt;i class="fa fa-checkmark"&gt;&lt;/i&gt;  &lt;!--   &lt;CheckmarkIcon /&gt;  --&gt;
  Click Me!                        &lt;!--   { props.children } --&gt;
&lt;/button&gt;                          &lt;!-- &lt;/Button&gt;            --&gt;</pre></div>
<p>Conversely, when rendered with the shallow renderer, we'll get a String
containing this "HTML":</p>
<div><pre>&lt;button&gt;              &lt;!-- &lt;Button&gt;             --&gt;
  &lt;CheckmarkIcon /&gt;   &lt;!--   NOT RENDERED!      --&gt;
  Click Me!           &lt;!--   { props.children } --&gt;
&lt;/button&gt;             &lt;!-- &lt;/Button&gt;            --&gt;</pre></div>
<p>If we test our <code>Button</code> with the normal renderer and there's a problem
with the <code>CheckmarkIcon</code> then the test for the <code>Button</code> will fail as well...
but finding the culprit will be hard. Using the <em>shallow</em> renderer, we isolate
the problem's cause since we don't render any other components other than the
one we're testing!</p>
<p>The problem with the shallow renderer is that all assertions have to be done
manually, and you cannot do anything that needs the DOM.</p>
<p>Thankfully, <a href="https://twitter.com/AirbnbEng" target="_blank">AirBnB</a> has open sourced their
wrapper around the React shallow renderer and jsdom, called <code>enzyme</code>. <code>enzyme</code>
is a testing utility that gives us a nice assertion/traversal/manipulation API.</p>
<h2>Enzyme</h2>
<p>Lets test our <code>&lt;Button&gt;</code> component! We're going to assess three things: First,
that it renders a HTML <code>&lt;button&gt;</code> tag, second that it renders its children we
pass it and third that handles clicks!</p>
<p>This is our Jest setup:</p>
<div><pre>import React from 'react';
import { shallow } from 'enzyme';
import Button from '../Button.react';

describe('&lt;Button /&gt;', () =&gt; {
  it('renders a &lt;button&gt;', () =&gt; {});

  it('renders its children', () =&gt; {});

  it('handles clicks', () =&gt; {});
});</pre></div>
<p>Lets start with testing that it renders a <code>&lt;button&gt;</code>. To do that we first
<code>shallow</code> render it, and then <code>expect</code> that a <code>&lt;button&gt;</code> node exists.</p>
<div><pre>it('renders a &lt;button&gt;', () =&gt; {
  const renderedComponent = shallow(
    &lt;Button&gt;&lt;/Button&gt;
  );
  expect(
    renderedComponent.find('button').node
  ).toBeDefined();
});</pre></div>
<p>Nice! If somebody breaks our button component by having it render an <code>&lt;a&gt;</code> tag
or something else we'll immediately know! Let's do something a bit more advanced
now, and check that our <code>&lt;Button&gt;</code> renders its children.</p>
<p>We render our button component with some text, and then verify that our text
exists:</p>
<div><pre>it('renders its children', () =&gt; {
  const text = 'Click me!';
  const renderedComponent = shallow(
    &lt;Button&gt;{ text }&lt;/Button&gt;
  );
  expect(
    renderedComponent.contains(text)
  ).toEqual(true);
});</pre></div>
<p>Great! Onwards to our last and most advanced test: checking that our <code>&lt;Button&gt;</code> handles clicks correctly. We'll use a Spy for that. A Spy is a
function that knows if, and how often, it has been called. We create the Spy
(thoughtfully provided by <code>expect</code>), pass <em>it</em> as the <code>onClick</code> handler to our
component, simulate a click on the rendered <code>&lt;button&gt;</code> element and, lastly,
see that our Spy was called:</p>
<div><pre>it('handles clicks', () =&gt; {
  const onClickSpy = jest.fn();
  const renderedComponent = shallow(&lt;Button onClick={onClickSpy} /&gt;);
  renderedComponent.find('button').simulate('click');
  expect(onClickSpy).toHaveBeenCalled();
});</pre></div>
<p>Our finished test file looks like this:</p>
<div><pre>import React from 'react';
import { shallow } from 'enzyme';
import Button from '../Button.react';

describe('&lt;Button /&gt;', () =&gt; {
  it('renders a &lt;button&gt;', () =&gt; {
    const renderedComponent = shallow(
      &lt;Button&gt;&lt;/Button&gt;
    );
    expect(
      renderedComponent.find('button').node
    ).toBeDefined();
  });

  it('renders its children', () =&gt; {
    const text = 'Click me!';
    const renderedComponent = shallow(
      &lt;Button&gt;{ text }&lt;/Button&gt;
    );
    expect(
      renderedComponent.contains(text)
    ).toEqual(true);
  });

  it('handles clicks', () =&gt; {
    const onClickSpy = jest.fn();
    const renderedComponent = shallow(&lt;Button onClick={onClickSpy} /&gt;);
    renderedComponent.find('button').simulate('click');
    expect(onClickSpy).toHaveBeenCalled();
  });
});</pre></div>
<p>And that's how you unit test your components and make sure they work correctly!</p>
<p><em>Continue to learn how to test your components <a href="/react-boilerplate/react-boilerplate/blob/master/docs/testing/remote-testing.md" target="_blank">remotely</a>!</em></p>

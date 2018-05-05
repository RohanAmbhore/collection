<a href="https://github.com/airbnb/enzyme/issues/1002">https://github.com/airbnb/enzyme/issues/1002</a><div id="articleHeader"><h1>              Testing a Redux-connected component using Enzyme            #1002    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/sa-js" target="_blank">sa-js</a>  opened this Issue
        <relative-time>on Jun 23, 2017</relative-time>
        · 51 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-238100988">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <h1>Enzyme</h1>
<p>i) What is the least error-prone way to test a Redux-connected Componet using Enzyme?<br />
I have checked many links and articles but haven't found a satisfactory answer. It's confusing me a lot.<br />
ii)How can I test whether my component is getting certain props or not using Enzyme?</p>
<h1>Versions</h1>
<ul>
<li>React-Boilerplate : Current Version</li>
<li>Node/NPM: ^6</li>
<li>Browser: Chrome</li>
<li>Enzyme: Current Version</li>
</ul>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-310796612">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <div><pre>const wrapper = shallow(&lt;ConnectedComponent /&gt;).dive();</pre></div>
<p>and then make your assertions on the wrapped component.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-318087732">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Any update to this? I secondly this very strongly. Everything I have tried does not work.</p>
<p>I set the context like shown in the docs -- <a href="http://airbnb.io/enzyme/docs/api/ReactWrapper/setContext.html" target="_blank">http://airbnb.io/enzyme/docs/api/ReactWrapper/setContext.html</a></p>
<p>This also looked promising<br />
<a href="https://stackoverflow.com/questions/37798741/nested-components-testing-with-enzyme-inside-of-react-redux" target="_blank">https://stackoverflow.com/questions/37798741/nested-components-testing-with-enzyme-inside-of-react-redux</a></p>
<p>But usually everything leads me back to:</p>
<p><code>Invariant Violation: Could not find "store" in either the context or props of "Connect(DatePicker)". Either wrap the root component in a &lt;Provider&gt;, or explicitly pass "store" as a prop to "Connect(DatePicker)".</code></p>
<p><g-emoji>😢</g-emoji></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-318090746">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>There's no update needed; wrap your connected component and use .dive().</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-318101507">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Two things:</p>
<ol>
<li>This is not working for me.</li>
</ol>
<p><code>const wrapper = shallow(&lt;ConnectedDatePicker /&gt;).dive();</code></p>
<p>I still get the same ole error:</p>
<p><code>Invariant Violation: Could not find "store" in either the context or props of "Connect(DatePicker)". Either wrap the root component in a &lt;Provider&gt;, or explicitly pass "store" as a prop to "Connect(DatePicker)".</code></p>
<ol>
<li>I need to use <code>mount</code> anyways. If I try something like:</li>
</ol>
<p><code>const wrapper = shallow(&lt;ConnectedDatePicker store={store}/&gt;).dive();</code></p>

<p><code>Method “props” is only meant to be run on a single node. 0 found instead.</code></p>
<p>when my test tries to use the API method <code>find</code>.  (<code>wrapper.find('#startDate').simulate('focus');</code>)</p>
<p>I am assuming it cannot find it,  because it is trying to find an grandchild element of my DatePicker component.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-318102035">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'd generally recommend using only shallow as much as possible, and only making assertions on which components your thing renders - in other words, if A renders B which renders C, your A tests shouldn't know anything about C, and should only be asserting that A renders B with the right props. Your <em>B</em> tests should be asserting things about C.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-318106481">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Right. Makes sense. What I am trying to do is more of an integration test.</p>
<p>I am sort of new to making tests. Would this thinking be more correct:</p>
<p>If my <code>DatePicker</code> component has child components that send events up to my DatePicker Component (for example, when a user selects <code>July 21, 2017</code> a <code>&lt;div/&gt;</code> is clicked & the event bubbles up and eventually is handled by my DatePicker component's <code>onDateChange</code> function).</p>
<p>For my test, rather than simulating that click event. I should be directly testing my <code>onDateChange</code> function with mock data under various circumstances.</p>
<p>(I apologize if this got off scope a little bit, just trying to understand).</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-318106989">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Yes, you definitely should be unit-testing your onDateChange.</p>
<p>It's your date picker component's tests' job to ensure that onDateChange is called at the proper time.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-318108053">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>thank you, this has been very helpful</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-326782939">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ljharb" target="_blank">@ljharb</a> Is there any way to mock the inner component? Instead of shallow/dive.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-326818993">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/shakiba" target="_blank">@shakiba</a> Mocks make tests more brittle; but shallow rendering is kind of like automocking. Can you elaborate on what you're trying to achieve?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-326856707">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ljharb" target="_blank">@ljharb</a> The reason that shallow does not work for me is that there are other nested components which I want to be rendered, such as bootstrap-react layout components.  Basically instead of including specific components in rendering using dive, I want to exclude few components from being rendered. I solved it using <code>jest.mock</code>, but if you have any other idea please let me.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-326863573">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>enzyme v3 and React 16 will provide an API for that; short of that, that's probably the best option.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-331092729">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Maybe it will be helpful for someone:</p>
<p>If you want to find if connected component is rendered you can find it by <code>Connect(Component)</code> selector.</p>
<p>Example (StylePicker is connected with the store):</p>
<p>index.js</p>
<pre><code>render() {
        return (
            &lt;div&gt;
                &lt;Header&gt;Choose style&lt;/Header&gt;
                &lt;StylePicker {...{ styles }}/&gt;
                &lt;NavigationButtons
                    onPrev={this.goToHome}
                    onNext={this.goToLayoutPicker}
                /&gt;
            &lt;/div&gt;
        );
    }
</code></pre>
<p>index.test.js</p>
<pre><code>    it('should render &lt;StylePicker&gt;', () =&gt; {
        expect(shallow(&lt;MainComponent /&gt;).find('Connect(StylePicker)')).toHaveLength(1);
    });
</code></pre>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-331353411">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/przemuh" target="_blank">@przemuh</a> better would be <code>shallow(&lt;MainComponent /&gt;).dive()</code>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-332649071">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ljharb" target="_blank">@ljharb</a> regarding the question in <a href="https://github.com/airbnb/enzyme/issues/1002#issuecomment-318087732" target="_blank">#1002 (comment)</a>, don't we still need to use something like <code>redux-mock-store</code> in order for <code>shallow(&lt;MainComponent /&gt;)</code> to work? whether or not we use <code>.dive()</code> won't affect that <code>shallow(&lt;MainComponent /&gt;)</code> expects to have a store in either context or props, right?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-332651881">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/mstorus" target="_blank">@mstorus</a> correct, it won't affect that.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-333164465">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>sometimes <strong>you might have to <em>double</em> dive</strong> (<code>someContainer.dive().dive()</code> or whatever before you can start working on the component) depending on how your connected container is setup.</p>
<p>For example lets say you're wrapping your connected container in another wrapper like this, you'll possibly have to double dive I've found because you need to now get past the <strong>ReactTimeout HOC</strong> <em>and</em> dive to get past the react-redux <strong>connect wrapper HOC</strong> in order to work with the container.</p>
<pre><code>const TimeoutLive = ReactTimeout(connect(mapStateToProps, {
  fetchLive,
  fetchLivePanel,
  fetchLiveVideo,
  clearLive,
  saveLiveRestart,
})(Live));
</code></pre>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-333167751">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Totally correct - you need one <code>.dive()</code> per HOC.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-333168755">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>BAM! now that's what I'm talkin about!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-334038315">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Is there any syntactic sugar available for components wrapped with react-router's <code>withRouter</code> method?</p>
<p>Instead of a test like:</p>
<pre><code>shallow(
        &lt;StaticRouter context={{}}&gt;
          &lt;IndexPage /&gt;
        &lt;/StaticRouter&gt;
      ).dive().length
</code></pre>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-334046128">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/michaelBenin" target="_blank">@michaelBenin</a> <code>.dive()</code> <em>is</em> the sugar.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-340065900">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>If you don't need access to the redux store as part of your unit test, don't forget that you can also export the React component individually in addition to exporting the connected variant by default.</p>
<div><pre>export class Component extends React.Component {}

export default connect(({ someReducer }) =&gt; ({
  ...
}))(Component)</pre></div>
<p>In your test, just extract the "pure" Component rather than the connected one:</p>
<div><pre>import { mount } from 'enzyme'  
import { Component } from '../components/Component'
...
mount(&lt;Component /&gt;)</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-340081036">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>You shouldn't do that, however, because if it's never used by itself in production, there's no value in testing it by itself. Use <code>.dive()</code>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-340090555">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I wouldn't say that it has no value <a href="https://github.com/ljharb" target="_blank">@ljharb</a> but I also know what you mean. Using <code>shallow</code> with <code>dive</code> was not working for my use case. I got the error: <code>Method “props” is only meant to be run on a single node. 0 found instead</code></p>
<div><pre>renderComponent = (props = {}) =&gt; shallow(&lt;Component {...props} /&gt;).dive()

const dispatchMock = jest.fn()
const component = renderComponent({ dispatch: dispatchMock })

component.find('form').simulate('submit')
expect(dispatchMock.mock.calls.length).toBe(1)  </pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-340100026">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/trevorwhealy" target="_blank">@trevorwhealy</a> that's worth exploring - i don't see any <code>.props()</code> calls in that code, nor is <code>dispatchMock</code> used anywhere - but it doesn't change that exporting the "pure" component just for testing isn't a good practice.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-340103243">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ljharb" target="_blank">@ljharb</a> sure we can agree on that. updated the code to reflect the implementation more closely.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-347390257">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Referencing <a href="https://github.com/gecko25" target="_blank">@gecko25</a>'s comment above - I get that same error...</p>
<pre><code>shallow(&lt;Provider store={store}&gt;&lt;MyContainer/&gt;&lt;/Provider&gt;).dive()

...

Invariant Violation: Could not find "store" in either the context or props of "Connect(MyContainer)". Either wrap the root component in a &lt;Provider&gt;, or explicitly pass "store" as a prop to "Connect(MyContainer)"
</code></pre>
<p>The connected component has some internal state that I want to test.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-349472237">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>What happens if there are multiple children of the component, one of which is connected?</p>
<pre><code>&lt;Wrapper&gt;
    &lt;Component/&gt;
    &lt;ConnectedComponent/&gt;
&lt;/Wrapper&gt;
</code></pre>
<p>In that case <code>.dive()</code> won't work because I have multiple non-dom children.</p>
<p>I can get around this by doing</p>
<pre><code>shallow(&lt;Wrapper/&gt;).children().at(1).dive()
</code></pre>
<p>but that makes for a really fragile test. I suppose in that situation I can do what was suggested above:</p>
<pre><code>shallow(&lt;Wrapper/&gt;).find('Connect(ConnectedComponent)').dive()
</code></pre>
<p>but I'm curious if there's a better solution.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-349479952">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/WeishenMead" target="_blank">@WeishenMead</a> in that case, find the component and <code>.shallow()</code> it.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
      <div>
        <h3 id="ref-issue-272801606">
      
        
      
        
  <a href="/dlrandy" target="_blank">dlrandy</a>
  

      referenced this issue
        in <strong>dlrandy/note-issues</strong>
      <a href="#ref-issue-272801606" target="_blank">
        <relative-time>on Dec 14, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Open
    



    
      <h4>
        <a href="/dlrandy/note-issues/issues/18" target="_blank">
          jest 
          #18
        </a>
      </h4>
    

    


  

</div>


</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-352029970">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I have two children of a component.  One is connected and the second is just a raw img tag.  I was checking to make sure the img was there.  So before the test would work fine doing <code>wrapper.find(&lt;img /&gt;)</code>.  Now with the latest jest update I have to look for the string <code>'img'</code> instead.  Is this related to this once you add a connected component to a non connected component that you are unit testing?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-352064742">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/TroySchmidt" target="_blank">@TroySchmidt</a> hmm, <code>wrapper.find(&lt;img /&gt;)</code> never should have worked - <code>.find('img')</code> was always the way to find an HTML node.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-352072244">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ljharb" target="_blank">@ljharb</a> Well good to know the right way to do it.  I just did a bunch of package upgrades and making sure things were working and making the adjustments to stay current.  So, I know it was passing at some point in the past.  Interesting.  It might be because before it was purely a stateless component?  idk.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-352075954">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm not entirely sure :-/ it's really confusing to me that it worked, because <code>.find</code> only ever took a selector, which is a string or a component function.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-353548158">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I have the same issue as <a href="https://github.com/glosee" target="_blank">@glosee</a> and <a href="https://github.com/gecko25" target="_blank">@gecko25</a>:</p>
<pre><code>shallow(&lt;Provider store={store}&gt;&lt;MyContainer/&gt;&lt;/Provider&gt;).dive()

...

Invariant Violation: Could not find "store" in either the context or props of "Connect(MyContainer)". Either wrap the root component in a &lt;Provider&gt;, or explicitly pass "store" as a prop to "Connect(MyContainer)"
</code></pre>
<pre><code>"enzyme": "3.2.0"
"react": "16.1.1"
 "enzyme-adapter-react-16": "1.1.0"
</code></pre>
<hr />
<p>Why it happens if the <code>Provider</code> has the <code>store</code> in properties?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-353592037">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <div>I figured out how to get around the invariant violation. I'm not exactly
sure why it's necessary when you already pass `store` to `Provider`, but
this has worked for me. In the first call to dive you can explicitly pass
`store` in the context. Like so...

```
const store = mockStore(initialState);
const wrapper = mount(
  &lt;Provider store={store}&gt;
    &lt;MyContainer/&gt;
  &lt;/Provider&gt;
const myContainer = wrapper.dive({context: {store}}).dive();

// Now you can do stuff like...
myContainer.instance().someMethod()
```

Hope this helps. Forgive any typos or bad formatting as i wrote this on my
phone.

Cheers</div>
<a href="#" target="_blank">…</a>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-353652132">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/glosee" target="_blank">@glosee</a> it's necessary because of <a href="https://github.com/airbnb/enzyme/issues/1445" target="_blank">#1445</a> still being broken.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>



    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-354685264">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Thanks <a href="https://github.com/glosee" target="_blank">@glosee</a>! After digging around for a while, your suggestion is the first that works for me.</p>
<p><a href="https://github.com/ljharb" target="_blank">@ljharb</a> <a href="https://github.com/airbnb/enzyme/issues/1445" target="_blank">#1445</a> seems to be closed. Is <a href="https://github.com/airbnb/enzyme/issues/664" target="_blank">#664</a> the most relevant issue to track this problem?</p>
<p>To me it seems like ideal usage would be</p>
<pre><code>const store = mockStore(initialState);
const wrapper = mount(
  &lt;Provider store={store}&gt;
    &lt;MyContainer/&gt;
  &lt;/Provider&gt;
const myContainer = wrapper.dive(); 

</code></pre>
<p>without having to provide context for the dive.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-354691316">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-354691316" target="_blank"><relative-time>on Jan 2</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Yes, <a href="https://github.com/airbnb/enzyme/issues/664" target="_blank">#664</a> :-)</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-359948374">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>This whole shallow(), dive() ... API is so terribly confusing. I'm scratching my head for hours now to figure out how to test a component that is using react-intl to provide i18n which in itself is controlled by a redux store. So I have to provide all of these HOCs, but still have to call a component method on the wrapped-wrapped component, too. This seems to be quite impossible.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-361674998">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Oh I remember having issues with react-intl.  I don't remember how I worked around it honestly.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-361727664">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I ended up implementing an additional i18n provider mock that doesn't use redux at all. Did the same for redux and router. I couldn't find any other way to work with shallow() and dive() directly.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-364021777">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I have also faced same issue as <a href="https://github.com/glosee" target="_blank">@glosee</a> and <a href="https://github.com/gecko25" target="_blank">@gecko25</a> and <a href="https://github.com/ashgaliyev" target="_blank">@ashgaliyev</a>  and tried to all the things mentioned over here but could not find a way to wrap my component with store using shallow API.<br />
And getting error of  <strong>Invariant Violation:could not find store........</strong></p>
<h1>Below is my code snippet</h1>
<p><code>renderedView = shallow( &lt;Provider store={store}&gt; &lt;ChangeLogPanel /&gt; &lt;/Provider&gt; ).dive();</code></p>
<h1>Error is</h1>
<p><code>Invariant Violation: Could not find "store" in either the context or props of "Connect(ChangeLogPanel)". Either wrap the root component in a &lt;Provider&gt;, or explicitly pass "store" as a prop to "Connect(ChangeLogPanel)".</code></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    


    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-364053041">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ljharb" target="_blank">@ljharb</a><br />
I got solution for above error for my case.<br />
<code>renderedView = shallow( &lt;Provider store={store}&gt; &lt;ChangeLogPanel /&gt; &lt;/Provider&gt; )</code><br />
I was trying to print HTML in console using method <code>console.log(renderedView .html())</code>. it gives me above error but when I try to use <code>console.log(renderedView .text())</code> then error went away.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-364582835">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-364582835" target="_blank"><relative-time>on Feb 10</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Use <code>.debug()</code>; <code>.html()</code> does a full render.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-366671882">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/mx781" target="_blank">mx781</a>
  

    </strong>

    commented

    <a href="#issuecomment-366671882" target="_blank"><relative-time>on Feb 19</relative-time></a>


      
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

          <p>While <a href="https://github.com/glosee" target="_blank">@glosee</a> 's solution seems to be a fine workaround for now - I <em>had</em> to use <code>shallow</code> rather than <code>mount</code> (otherwise getting a "wrapper.dive is not a function" error). Is there a way to do a full <code>mount</code> on the parent before <code>dive</code>ing in to get a shallow wrapper? What am I missing?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-366905992">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-366905992" target="_blank"><relative-time>on Feb 20</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>If you're using <code>mount</code>, you'd <code>.find</code> down to the component you wanted, and then <code>.mount()</code>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-378750162">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I went down this rabbit hole as well until I realized that I was importing my component into the test file incorrectly. I didn't need to test the connected part, just the component itself.</p>
<p>YES: <code>import { MyComponent } from '../MyComponentFile';</code><br />
NO: <code>import MyComponent from '../MyComponentFile';</code></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-378768750">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-378768750" target="_blank"><relative-time>on Apr 5</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>In fact, “correctly” means testing the component you use in production - the connected one.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-378780719">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Providing an example of using <a href="https://github.com/arnaudbenard/redux-mock-store" target="_blank"><code>redux-mock-store</code></a>, since this thread still comes up a lot in searches.</p>
<p>This example includes <a href="https://github.com/gaearon/redux-thunk" target="_blank"><code>redux-thunk</code></a>, since it's a common middleware used with Redux (and is <a href="https://redux.js.org/advanced/async-actions#async-action-creators" target="_blank">mentioned</a> in the Advanced section of the Redux tutorial). If you don't use <code>redux-thunk</code>, just remove that part.</p>
<div><pre>import configureStore from 'redux-mock-store';
import thunk from 'redux-thunk';

const store = configureStore([
    thunk,
])();

const wrapper = shallow(
  &lt;MyComponent {...props} store={store} /&gt;
).dive();</pre></div>
<p>Tested with <code>"redux-thunk": "^2.1.0"</code> and <code>"redux-mock-store": "^1.5.1"</code>.</p>
<p>Note that using <code>.dive()</code> ensures that you are testing the connected component (which is actually used in production), rather than the unconnected component (which may not be directly used in production).</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

    
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-381135305">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/oakis" target="_blank">oakis</a>
  

    </strong>

    commented

    <a href="#issuecomment-381135305" target="_blank"><relative-time>22 days ago</relative-time></a>


      
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

          <p>I did kind of like <a href="https://github.com/mstorus" target="_blank">@mstorus</a></p>
<div><pre>const wrapper = shallow(&lt;Navbar store={store} /&gt;).dive();</pre></div>
<p>But with the actual store, not with redux-mock-store.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>








        </div>


        <div>
              
<div>
  

    
      



      <div>
        
          <div>
  


  
  <div>

    

    

        <p>
    
    
        Attach files by dragging & dropping,
        selecting them, or pasting
        from the clipboard.
    
    
    
    
    
    
    
    
    
  </p>


    
  </div>

  

  


  
</div>

          
      </div>

</div>


        </div>
      </div>

    </div>
    
  
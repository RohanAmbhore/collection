<a href="https://github.com/facebook/create-react-app/issues/3206">https://github.com/facebook/create-react-app/issues/3206</a><div id="articleHeader"><h1>              Error on tests when Enzyme is added            #3206    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/pedro-stanaka" target="_blank">pedro-stanaka</a>  opened this Issue
        <relative-time>on Sep 28, 2017</relative-time>
        · 15 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      


  
    
      

          <h3>Is this a bug report?</h3>

<h3>Can you also reproduce the problem with npm 4.x?</h3>

<h3>Which terms did you search for in User Guide?</h3>
<p>I searched about testing, about enzyme and on the troubleshooting page as well.</p>
<h3>Environment</h3>
<ol>
<li><code>node -v</code>: v6.11.3</li>
<li><code>npm -v</code>: 4.6.1</li>
<li><code>yarn --version</code> (if you use Yarn): 1.1.0</li>
<li><code>npm ls react-scripts</code> (if you haven’t ejected):  react-scripts@1.0.14</li>
</ol>
<p>Then, specify:</p>
<ol>
<li>Operating system: Windows</li>
</ol>
<h3>Steps to Reproduce</h3>
<ol>
<li>npm install -g create-react-app</li>
<li>create-react-app test-jest-enzyme</li>
<li>cd test-jest-enzyme</li>
<li>Change file src/App.test.js to be:</li>
</ol>
<div><pre>import React from 'react';
import App from './App';
import {shallow} from "enzyme";

it('renders without crashing', () =&gt; {
    shallow(&lt;App /&gt;);
});</pre></div>
<ol>
<li>npm test</li>
</ol>
<h3>Expected Behavior</h3>
<p>The tests would pass and no exception would be thrown.</p>
<h3>Actual Behavior</h3>
<p>Will give:</p>
<pre><code>          Enzyme Internal Error: Enzyme expects an adapter to be configured, but found none. To
          configure an adapter, you should call `Enzyme.configure({ adapter: new Adapter() })`
          before using any of Enzyme's top level APIs, where `Adapter` is the adapter
          corresponding to the library currently being tested. For example:

          import Adapter from 'enzyme-adapter-react-15';

          To find out more about this, see http://airbnb.io/enzyme/docs/installation/index.html


      at validateAdapter (node_modules/enzyme/build/validateAdapter.js:14:11)
      at Object.&lt;anonymous&gt;.it (src/App.test.js:6:25)
</code></pre>
<h3>Reproducible Demo</h3>
<p><a href="https://gitlab.com/DevLearn/jest-react-broken" target="_blank">https://gitlab.com/DevLearn/jest-react-broken</a></p>
      
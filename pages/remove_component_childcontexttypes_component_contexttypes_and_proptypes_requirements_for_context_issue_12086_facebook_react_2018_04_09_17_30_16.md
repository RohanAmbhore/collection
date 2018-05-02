<a href="https://github.com/facebook/react/issues/12086">https://github.com/facebook/react/issues/12086</a><div id="articleHeader"><h1>              Remove Component.childContextTypes / Component.contextTypes and PropTypes requirements for Context            #12086    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/dwjft" target="_blank">dwjft</a>  opened this Issue
        <relative-time>on Jan 24</relative-time>
        · 2 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      

  
    
      
          <p>Since there is currently undergoing work (<a href="https://github.com/facebook/react/pull/11818" target="_blank">#11818</a>) on the Context API, I feel like this may be a good time to bring this up.</p>
<hr />
<p>In my projects, the design decision to not use <code>PropTypes</code> in our internal components was made early on, under the assumption that if we were to use <code>PropTypes</code>, we may as well go the whole way and use <code>flow</code> or <code>TypeScript</code> as well.</p>
<p>Enforcing a <code>PropType</code> declaration on a single React feature doesn't make much sense. If <code>PropTypes</code> are optional on <code>props</code>, why are they required on <code>context</code>?</p>
<p>To get around this enforcement, my components end up looking like the following:</p>
<div><pre>// makeContext.js
import PropTypes from 'prop-types';

const makeContext = (keys) =&gt; {
  const obj = {};
  keys.forEach((key) =&gt; {
    obj[key] = PropTypes.any;
  });
  return obj;
};

export default makeContext;</pre></div>
<div><pre>// contextTypes.js
import makeContext from './makeContext';

export default makeContext([
  'someValue',
  'someOtherValue',
]);</pre></div>
<div><pre>// ParentComponent.js
import contextTypes from './contextTypes';
import ChildComponent from './ChildComponent';

class ParentComponent extends React.Component {
  getChildContext() {
    return { someValue: 1, someOtherValue: false };
  }
  render() {
    return &lt;ChildComponent /&gt;;
  }
}
ParentComponent.childContextTypes = contextTypes;</pre></div>
<div><pre>// ChildComponent.js
import contextTypes from './contextTypes';

const ChildComponent = (props, { someValue }) =&gt; (
  &lt;p&gt;{someValue}&lt;/p&gt;
);
ChildComponent.contextTypes = contextTypes;</pre></div>
<hr />
<p>As you can see, the declaration of both <code>childContextTypes</code> and <code>contextTypes</code> is essentially pointless, yet I am forced to do so because the API enforces it.</p>
<p>It seems that, much like <code>props</code> and <code>PropTypes</code>, it should be down to the developer to decide whether or not the rule should be enforced.</p>
      
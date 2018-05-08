<a href="https://github.com/airbnb/enzyme/issues/1081">https://github.com/airbnb/enzyme/issues/1081</a><div id="articleHeader"><h1>              .simulate('click') only working when done twice on the same component, through ID and Class            #1081    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/nxmohamad" target="_blank">nxmohamad</a>  opened this Issue
        <relative-time>on Aug 20, 2017</relative-time>
        · 17 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-251479737">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I have gone through existing issues and could not find one similar to this.</p>
<p>I have a button element like so, that sits within a <code>&lt;Contact/&gt;</code> component that I am testing:</p>
<pre><code>&lt;div&gt;
...
&lt;button id="Contact-button-submit" className="btn btn-primary btn-lg" onClick={this.handleSubmit}&gt;Submit&lt;/button&gt;
...
&lt;/div&gt;
</code></pre>
<p>and here is my test:</p>
<pre><code>it('calls handleSubmit when Submit button is clicked', () =&gt; {
	let wrapper = shallow(&lt;Contact {...mockProps} /&gt;);
	wrapper.instance().handleSubmit = jest.fn();
	let { handleSubmit } = wrapper.instance();
	expect(handleSubmit).toHaveBeenCalledTimes(0);
	wrapper.find('#Contact-button-submit').simulate('click'); // the only simulate click I want
	wrapper.find('.btn-primary').simulate('click'); // the simulate click I also had to add
	expect(handleSubmit).toHaveBeenCalledTimes(1);
});
</code></pre>
<p>The funny thing is that, when I only include the first simulate click (the ID one), the test fails at the last expect. The onClick function (handleSubmit) is never called.<br />
But when I add the second one that uses className, it passes.</p>
<p>It seems like they BOTH need to be present. It will fail if one is removed.</p>
<p>Are there any known causes for this? I'm scratching my head over this.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-323866479">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>(btw buttons have a default <code>type</code> of <code>submit</code>, so if you're not using it as a javascriptless submit button, you want <code>type="button"</code>)</p>
<p>In general, I don't recommend using <code>simulate</code> at all - I'd recommend <code>.prop('onClick')</code> and invoking it directly, and asserting that your mock is called - you don't need to test React's event wiring nor the browser's.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-323952001">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>by <code>type="button"</code> do you mean using that as the selector?</p>
<p>.prop('onClick') only returns it right? to call it I assumed it would be something like <code>wrapper.find(SELECTOR).props().onClick()</code>;</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-323956522">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>no, I mean using that in the jsx.</p>
<p>Correct, you'd do <code>wrapper.find(SELECTOR).prop('onClick')()</code>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-324009660">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>thank you.<br />
would there be any known issues whereby the onClick function wouldn't be called?</p>
<p>I tried to invoke with the example syntax you gave but it seems like it doesn't invoke the function (handleSubmit) I've assigned in onClick.</p>
<p>however, if I do,<br />
<code>onClick={(x) =&gt; console.log(x)}</code> , and then <code>wrapper.find(SELECTOR).prop('onClick')("test")</code> it does log to console. but it doesn't register any calls for handleSubmit based on how I have mocked it above</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-324011175">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>regarding using type="button" as the selector, is that considered best-practice?<br />
what if I have multiple buttons in the same wrapper component, is it not better to use ID?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-324014051">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>ok so similar issue again, the test passes when I do <code>wrapper.find(SELECTOR).prop('onClick')()</code> twice.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-324070258">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>My guess is some combination of using class properties, and storing a reference to the function prior to stubbing it out. Can you share 100% of the related code?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-324432764">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/nxmohamad" target="_blank">nxmohamad</a>
  

    </strong>

    commented

    <a href="#issuecomment-324432764" target="_blank"><relative-time>on Aug 24, 2017</relative-time></a>


      
  •


  
    <summary>
      
          edited by ljharb 
      
      
    </summary>

    
  

  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><em>Contact.js</em></p>
<div><pre>export class Contact extends Component {
	constructor() {
		super();
		this.state = {
			...
		}
		...
		this.handleSubmit = this.handleSubmit.bind(this);
	}
  	handleSubmit() {
  	 ...
  	}
        render() {
        ...
       &lt;button id="Contact-button-submit" className="btn btn-primary btn-lg" onClick=
       {this.handleSubmit}&gt;Submit&lt;/button&gt;
        ...
        }

}</pre></div>
<p><em>Contact.test.js</em></p>
<div><pre>import React from 'react';
import { shallow } from 'enzyme';
import { Contact } from './index';

const mockProps = {
	...
	submitMessageHandler: jest.fn(),
	...
};

afterEach(() =&gt; {
	mockProps.submitMessageHandler.mockReset();
	...
});

it('calls handleSubmit when Submit button is clicked', () =&gt; {
	let wrapper = shallow(&lt;Contact {...mockProps} /&gt;);
	wrapper.instance().handleSubmit = jest.fn();
	let { handleSubmit } = wrapper.instance();
	expect(handleSubmit).toHaveBeenCalledTimes(0);
	// below 2 lines are the original code and as I've mentioned calling onClick still needs to be done twice
	wrapper.find('#Contact-button-submit').simulate('click'); // first one through ID
	wrapper.find('.btn-primary').simulate('click'); // second one through classname
	expect(handleSubmit).toHaveBeenCalledTimes(1);
});</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-324485036">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>OK, so that's exactly the problem. You have to stub <code>Contact.prototype.handleSubmit</code> <em>before</em> shallow-rendering the component.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-324746121">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>is this correct?</p>
<pre><code>it('calls handleSubmit when Submit button is clicked', () =&gt; {
	Contact.prototype.handleSubmit = jest.fn();
	let wrapper = shallow(&lt;Contact {...mockProps} /&gt;);
	let { handleSubmit } = wrapper.instance();
	expect(handleSubmit).toHaveBeenCalledTimes(0);
	wrapper.find('#Contact-button-submit').prop('onClick')();
	expect(handleSubmit).toHaveBeenCalledTimes(1);
	Contact.prototype.handleSubmit.mockRestore();
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
    
  <div id="issuecomment-324747687">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ljharb" target="_blank">@ljharb</a> the above didn't work for me, but after your suggestion I came across a StackOverflow question that led me to something that did work, which is using <code>spyOn</code>.</p>
<p><a href="https://stackoverflow.com/a/43284406/6440036" target="_blank">https://stackoverflow.com/a/43284406/6440036</a></p>
<p>I would still like to know what is wrong with my attempt above. Thank you.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-325034547">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>your approach above should work just fine; except that <code>mockRestore</code> can't work because it can't possibly know what the original value of the function was. You definitely want to use <code>spyOn</code>, or else you have to manually preserve the original value and restore it with <code>=</code> at the end.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-325111841">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>somehow stubbing the prototype like in the above snippet didn't work, but I'll close this issue since I found a way to carry out what I needed.</p>
<p>thank you <a href="https://github.com/ljharb" target="_blank">@ljharb</a>  for the help</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-358759439">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/drFabio" target="_blank">drFabio</a>
  

    </strong>

    commented

    <a href="#issuecomment-358759439" target="_blank"><relative-time>on Jan 19</relative-time></a>


      
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

          <blockquote>
<p>OK, so that's exactly the problem. You have to stub Contact.prototype.handleSubmit before shallow-rendering the component.<br />
--</p>
</blockquote>
<p><a href="https://github.com/ljharb" target="_blank">@ljharb</a>  what if I want to test a bound method of some class for example:</p>
<div><pre>      const stub = sandbox.stub(targetComponent.instance(), 'createAccount')
      renderedComponent.find(CreateAccountButton).at(0).prop('onClick')()
      renderedComponent.update()
      renderedComponent.find(CreateAccountButton).at(0).prop('onClick')()
      renderedComponent.update()
      expect(stub.called).toEqual(true)</pre></div>
<p>On this case I'm needing to invoke it twice as well for it to work.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-358760749">

    
<div>
  

    
    
      Owner
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-358760749" target="_blank"><relative-time>on Jan 19</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>You have to stub it on the component prototype <em>before</em> creating the wrapper. In other words, you need to make sure that the thing that's "bound" is the stub.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-358796725">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Got it. Thanks!<br />
I could swear the instance binding worked before but I think probably the "referential identity is no longer preserved" is the cause it doesn't work anymore.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-378176362">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I finally found the solution to my <code>simulate('click')</code> problem here.  Thanks!</p>
<p>I'm sure we are not the only ones who experience this issue. Can we add this <code>.prop('onClick')</code> for buttons recommendation in the official docs? Spent a long time trying to figure out what the problem was and only managed to find it by chance here.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



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
    
  
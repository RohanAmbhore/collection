<a href="https://github.com/react-boilerplate/react-boilerplate/issues/1620">https://github.com/react-boilerplate/react-boilerplate/issues/1620</a><div id="articleHeader"><h1>              Setting state with initialState sets a Map, but setting state later sets an Object            #1620    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/TrevorHinesley" target="_blank">TrevorHinesley</a>  opened this Issue
        <relative-time>on Mar 2, 2017</relative-time>
        · 11 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-211182632">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I've noticed that if I set an initialState key like so:</p>
<pre><code>const initialState = fromJS({
  currentUser: { name: "John" }
})
</code></pre>
<p>Then accessing currentUser from the state store will (correctly) return a Map. But in the reducer, if I update the state like so:</p>
<pre><code>  case CUSTOMER_CREATE_SUCCESS:
      return state
        .set('currentUser', action.customer)
        .set('loading', false)
        .set('error', null)
</code></pre>
<p>Then currentUser is no longer a Map when I retrieve it from the store. It's a Javascript object. Am I missing something? I thought <code>state.set</code> was the proper way to manipulate immutable state.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  


          

          

  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-283467368">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I now realize that fromJS does a deep convert, hence why the object is a Map on initial set of the state, but not when I do <code>set</code> like above. I had to do this:</p>
<pre><code>case CUSTOMER_CREATE_SUCCESS:
      return state
        .set('currentUser', fromJS(action.customer))
        .set('loading', false)
        .set('error', null)
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-287887354">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Hey <a href="https://github.com/TrevorHinesley" target="_blank">@TrevorHinesley</a>  so should we always set the values of our state using fromJS? is that the recommended way to go? I'm confused because on the example code when they set the repoList they don't use fromJS  instead they do:  <code>state .setIn(['userData', 'repositories'], action.repos)</code></p>
<p>Could anybody share some light?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-287905402">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>@lrpalacios Did you see the docs on <a href="https://facebook.github.io/immutable-js/docs/#/fromJS" target="_blank"><code>fromjs()</code></a> and <a href="https://facebook.github.io/immutable-js/docs/#/Map/setIn" target="_blank"><code>setIn()</code></a> ?</p>
<p>Also <a href="http://stackoverflow.com/questions/32350575/how-can-i-set-a-deeply-nested-value-in-immutable-js" target="_blank">this</a> may help.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-287908384">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/gihrig" target="_blank">@gihrig</a> Yes I did,</p>
<p>If I understand correctly:</p>
<p>On the declaration of initial state, everything is immutable object since fromJs deeply convert the entire object</p>
<div><pre>const initialState = fromJS({
  loading: false,
  error: false,
  currentUser: false,
  userData: {
    repositories: false,
  },
});</pre></div>
<p>but when this line is executed:</p>
<div><pre>state.setIn(['userData', 'repositories'], action.repos)</pre></div>
<p>It returns a copy of the current state with the property repositories as a normal plain old javascript array which is no longer an immutable list or is it?</p>
<p>That is why I'm asking if I should always map to an immutable object when I have nested objects in my state</p>
<p>I mean shouldn't that line be something like</p>
<div><pre>state.setIn(['userData', 'repositories'], List(action.repos))</pre></div>
<p>Notice the List(action.repos) instead of just action.repos</p>
<p>Please bear with me I'm still a noob on all of this</p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-287922535">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>@lrpalacios Not being a great expert on the subject, I agree that Immutable.setIn() is minimally documented. <g-emoji>😄</g-emoji></p>
<p>Consider this from the setIn() docs:</p>
<blockquote>
<p>Returns a new Map having set value at this keyPath. If any keys in keyPath do not exist, a new immutable Map will be created at that key.</p>
</blockquote>
<p>I interpret this to mean that <code>setIn()</code> "Returns a new <em>immutable</em> Map".</p>
<p>Further consider:</p>
<div><pre>const newMap = originalMap.setIn(['subObject', 'subKey'], 'ha ha!')</pre></div>
<p>What may not be immediately clear is that <code>originalMap</code> (and thus <code>subObject</code> and <code>subKey</code>) are immutable to begin with. As shown in this example, the parameter <code>'ha ha'</code> is a simple value, a String, and is not immutable.</p>
<p>Presuming that <code>List</code> is immutable, that's why</p>
<div><pre>state.setIn(['userData', 'repositories'], List(action.repos))</pre></div>
<p>Would be incorrect. setIn() handles this conversion, though the docs don't mention that directly.</p>
<p>Does that help?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-287926695">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/gihrig" target="_blank">@gihrig</a> I don't think the array is being mapped unless I'm still lost</p>
<p><a href="https://camo.githubusercontent.com/bbba36e251689e476bc4a68e76eb3f29bf95bd20/687474703a2f2f6936372e74696e797069632e636f6d2f326a626d7673352e706e67" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/bbba36e251689e476bc4a68e76eb3f29bf95bd20/687474703a2f2f6936372e74696e797069632e636f6d2f326a626d7673352e706e67" alt="example" title="immutable" /></div></a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-288434145">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I am not sure what the confusion is here, but does this clear it up?</p>
<pre><code>    const state = fromJS({
      loading: false,
      error: false,
      currentUser: false,
      userData: {
        repositories: false,
      },
    });

    const state2 = state.setIn(['userData', 'repositories'], ['repo1', 'repo2']);
    expect(state2.getIn(['userData', 'repositories']) instanceof List).toBe(false);
    expect(state2.getIn(['userData', 'repositories']) instanceof Array).toBe(true);
    expect(state2.getIn(['userData', 'repositories', 0])).toBe(undefined);

    const state3 = state.setIn(['userData', 'repositories'], List(['repo1', 'repo2']));
    expect(state3.getIn(['userData', 'repositories']) instanceof List).toBe(true);
    expect(state3.getIn(['userData', 'repositories']) instanceof Array).toBe(false);
    expect(state3.getIn(['userData', 'repositories', 0])).toBe('repo1');
</code></pre>
<blockquote>
<p>On the declaration of initial state, everything is immutable object since fromJs deeply convert the entire object</p>
</blockquote>
<p>correct</p>
<blockquote>
<p>It returns a copy of the current state with the property repositories as a normal plain old javascript array which is no longer an immutable list or is it?</p>
</blockquote>
<p>correct<br />
(edit: to be more precise, it never was an immutable list, because it was initialised as a bool value. But if it had been a List before, then yes, it would be replaced by the 'normal' array)</p>
<blockquote>
<p>That is why I'm asking if I should always map to an immutable object when I have nested objects in my state</p>
</blockquote>
<p>As you can see, it is up to you. It is possible to put vanilla js structures inside an Immutable structure, but I wouldn't recommend it. I don't know why they did it this way in the example.</p>
<p>Cheers</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-288447602">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Thanks, <a href="https://github.com/devboell" target="_blank">@devboell</a> It has been a lot of info at the same time, causing me decisions fatigue. I've been going all around trying to decide if I should receive and use the immutable objects in my components/container or If I should call toJS at some point like in the selector or do like in the example code and set vanilla js structures inside an Immutable structure.</p>
<p>But I realize now that each has pros and cons I'm trying to figure out what is the common approach using this boilerplate</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-288461139">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>yeah, combining all these libraries & boilerplates can be overwhelming and exhausting, I know all about it :-)</p>
<p>Personally I try to be as consistent as possible with Immutable, ie: convert all incoming external data to Immutable right away, and keep it that way. It just prevents confusion.</p>
<p>There really shouldn't be a need to use toJS(). Immutablejs is a very good fit for React components/containers. I have never had a case where I had to convert back to JS.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-288467183">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>It is just that using the .get from within my components or containers does feels like a leaky abstraction and I don't know how will that play using third party components :/</p>
      </td>
    </tr>
  </tbody>
</table>


        



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

  

  


  


          
      




        
      

    
    
  
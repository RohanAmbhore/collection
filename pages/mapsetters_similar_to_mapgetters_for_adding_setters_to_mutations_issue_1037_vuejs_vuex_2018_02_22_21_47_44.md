<a href="https://github.com/vuejs/vuex/issues/1037">https://github.com/vuejs/vuex/issues/1037</a><div id="articleHeader"><h1>              mapSetters (similar to mapGetters) for adding setters to mutations            #1037    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/Shashwat986" target="_blank">Shashwat986</a>  opened this Issue
        <relative-time>on Nov 1, 2017</relative-time>
        · 11 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            





            
  <div id="issue-270301844">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <h3>What problem does this feature solve?</h3>
<p>There have been lots of situations where I have some variables in <code>state</code> that I need to assign values to. The correct way to modify the state tree is to create a mutation to set the value of the key in the state. This means a lot of repetitive code is written (as shown below):</p>
<pre><code>export default {
  state: {
    name: null,
    value: 0
  },
  mutations: {
    setName (state, name) {
      state.name = name;
    },
    setValue (state, value) {
      state.value = value;
    }
  }
};

$store.commit('setName', 'John Doe');
</code></pre>
<p><code>mapSetters</code> will allow users to create all these setters using a single like of code.</p>
<h3>What does the proposed API look like?</h3>
<pre><code>import { mapSetters } from 'vuex'

export default {
  state: {
    name: null,
    value: 0
  },
  mutations: {
    ...mapSetters(['name', 'value']),
    //...
  }
};
</code></pre>
<p>Usage: <code>$store.commit('name', "John Doe")</code> OR <code>$store.commit('setValue', 4)</code> depending on how it is implemented. I prefer the second approach myself.</p>

      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  

          

          

  
  


  
<div>
    
<div>
  





  
  <div id="issuecomment-341100537">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>I'm interested in working on this myself, so no effort beyond approval is required from anyone else's end.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-341198590">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>I wrote a simple function where I "bootstrap" the mutations and getters on my module, which might be useful to you:</p>
<div><pre>export function bootstrap (module) {
  if (module.getters === undefined) {
    module.getters = {}
  }

  if (module.mutations === undefined) {
    module.mutations = {}
  }

  Object.keys(module.state).forEach(key =&gt; {
    if (module.getters[key] === undefined) {
      module.getters[key] = state =&gt; state[key]
    }
    if (module.mutations[key] === undefined) {
      module.mutations[key] = (state, value) =&gt; {
        state[key] = value
      }
    }
  })

  return module
}</pre></div>
<div><pre>import { bootstrap } from '~/utilities/vuex'

export default bootstrap({
  namespaced: true,
  state: {
    name: '',
    email: ''
  }
})</pre></div>
<p>This means every state property gets its own mutator and getter, but if you already defined either of those, it will use yours over the bootstrapped defaults.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-341336839">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Exactly, something like this should be part of the actual vuex package.</p>
<p>In fact, with my implementation, your code would look something like:</p>
<pre><code>export default {
  namespaced: true,
  state: {
    name: '',
    email: ''
  },
  getters: mapGetters(['name', 'email']),
  mutations: mapSetters(['name', 'email'])
};
</code></pre>
<p>which isn't too bad, right?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-341473656">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Yup you could do that just as well. It certainly wouldn't hurt to add some more utilities, but at the end of the day it's also pretty trivial to implement it yourself. Who knows!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  


  
<div>
    
<div>
  





  
  <div id="issuecomment-343651865">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/shashwat986" target="_blank">@Shashwat986</a> I like this idea... i was hoping for something similar <a href="https://github.com/vuejs/vuex/issues/953" target="_blank">#953</a>. My only question on this proposal is what if the user wanted the setter to trigger an action. Could your proposal be modified to support that option? or do you feel this should only apply to mutations?</p>
<pre><code>  actions: {
    ...mapSetters(['name', 'value'])
  }
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-343835587">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>So, I was having this work by automatically generating the method to set the value in the <code>state</code>. How would that work for actions? If the action is doing the same task, it would be calling a mutation within it, one that would do the job just as well.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  


  
<div>
    
<div>
  





  
  <div id="issuecomment-344448231">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>This is similar discussion with <a href="https://github.com/vuejs/vuex/issues/91" target="_blank">#91</a>.<br />
As the helper could easily be implemented in userland, we would not include this.</p>
<p>Please see our policy for adding a new feature: <a href="https://github.com/vuejs/vue/issues/6004#issuecomment-312404196" target="_blank">vuejs/vue#6004 (comment)</a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  


  
<div>
    
<div>
  





  
  <div id="issuecomment-344524703">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>So, I don't mean to be rude, but, doesn't <a href="https://github.com/vuejs/vue/issues/6004#issuecomment-312404196" target="_blank">vuejs/vue#6004 (comment)</a> mention</p>
<blockquote>
<p>If a proposed API's functionality can be cleanly implemented in userland without hacks, we will pass <strong>unless it's strongly needed by a significant majority of the user base (i.e. we've seen it been raised/discussed multiple times)</strong>.</p>
</blockquote>
<p><em>(emphasis mine)</em></p>
<p>Past issues mentioning the same/similar problems:<br />
<a href="https://github.com/vuejs/vuex/issues/91" target="_blank">#91</a><br />
<a href="https://github.com/vuejs/vuex/issues/953" target="_blank">#953</a><br />
<a href="https://github.com/vuejs/vuex/issues/236#issuecomment-231022010" target="_blank">#236 (comment)</a><br />
<a href="https://github.com/vuejs/vuex/issues/236#issuecomment-231755035" target="_blank">#236 (comment)</a><br />
<a href="https://github.com/vuejs/vuex/issues/936" target="_blank">#936</a><br />
<a href="https://github.com/vuejs/vuex/issues/559" target="_blank">#559</a></p>
<p>Existing open-source projects that will greatly benefit from this:<br />
<a href="https://github.com/zhaohaodang/vue-WeChat/blob/master/src/vuex/mutations.js" target="_blank">https://github.com/zhaohaodang/vue-WeChat/blob/master/src/vuex/mutations.js</a><br />
<a href="https://github.com/Binaryify/vue-tetris/blob/master/src/vuex/mutations.js" target="_blank">https://github.com/Binaryify/vue-tetris/blob/master/src/vuex/mutations.js</a><br />
<a href="https://github.com/liangxiaojuan/vue-Meizi/blob/master/src/vuex/store.js" target="_blank">https://github.com/liangxiaojuan/vue-Meizi/blob/master/src/vuex/store.js</a><br />
<a href="https://github.com/ericjjj/douban/blob/douban/frontend/store/index.js" target="_blank">https://github.com/ericjjj/douban/blob/douban/frontend/store/index.js</a></p>
<p>I completely understand that we shouldn't add something that isn't useful, and just ends up making the package bloated, but the reason I'm pushing a little for this feature is because it's clearly something that will reduce a <strong>lot</strong> of dev effort. Having said that, if you feel it shouldn't be a part of <code>vuex</code>, that's fine.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-344639847">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Well, the issues/comments which you provided seem proposing different helpers each other. After reading them, I feel it would be better to leave such helpers in userland because there are various demand for each user.</p>
<p>Also IMO, the most of mutations would not only assign a payload to a state in real world applications. If many of your mutations become like so, it may be too separated or there are other modules for calculating a next state.</p>
<p>vue-tetris has many of mutations that just assign a payload into state but it looks like calculating the  app state out of the vuex. <a href="https://github.com/Binaryify/vue-tetris/blob/master/src/control/states.js" target="_blank">https://github.com/Binaryify/vue-tetris/blob/master/src/control/states.js</a><br />
I don't think such niche use case justifies to include this helper into the core.</p>
<p>Only thing it could be the case would be a form handling. I see some people binds all form elements with different mutations. Then the mutations are bloated. But creating mutation generator may not completely solve the problem because it cannot handle nested or dynamic form.</p>
<p>I'm still investigating about the form handling issue but I think it would make more sense to handle it in component local state and share a part of form data with store which is really needed in another component.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-344662862">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/ktsn" target="_blank">@ktsn</a>, IMO form handling should 100% be in userland b/c many real world applications will have different xhr things and ways they want to handle optimistic vs pessimistic updates for different forms.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  





  
<div>
    
<div>
  





  
  <div id="issuecomment-344710267">

    



    <div>
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Sounds good. Thanks for all the help!</p>
<p>(P.S.: I'm still keen to contribute because I'm a big fan of Vue. Do let me know if I can help in any way)</p>
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

  

  


  


          
      




        
      

    
    
  
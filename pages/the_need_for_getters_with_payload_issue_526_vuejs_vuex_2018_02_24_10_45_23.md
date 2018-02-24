<a href="https://github.com/vuejs/vuex/issues/526">https://github.com/vuejs/vuex/issues/526</a><div id="articleHeader"><h1>              The need for getters with payload            #526    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/andreiglingeanu" target="_blank">andreiglingeanu</a>  opened this Issue
        <relative-time>on Dec 15, 2016</relative-time>
        · 16 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            





            
  

    



    
      
<table>
  <tbody>
    <tr>
      <td>
          <p>Let me state right from the beginning, that's a feature request.</p>
<p>I saw the discussion inside <a href="https://github.com/vuejs/vuex/issues/52" target="_blank">#52</a>, especially quoting <a href="https://github.com/yyx990803" target="_blank">@yyx990803</a>:</p>
<blockquote>
<p>Why are you expecting payload inside getters? Computed getters do not take any arguments.</p>
</blockquote>
<hr />
<p>The thing is that I'm having a couple of use cases where being able to pass <em>payload</em> to getters would be <em>very</em> handy. I know, they're technically not functions thus you can't pass any arguments to them.</p>
<p>Right now, I'm forced to extract all of my logic in functions that accept current state as the first argument and payload as the second one (I'm naming them <code>helpers</code>, to be specific). I'm forced to do this often, practically every app I used to work on has the need of getters with some payload.</p>
<p>It would be nice if vuex will adapt this pattern into itself, I'm seeing its usage as follows:</p>
<div><pre>new Vuex.Store({
  helpers: {
    // type here is similar to what we have for mutations
    GET_SOME_DATA (state, { id, type }) {
      return my_awesome_computation(state, id);
    }
  }
})

// somewhere in my components
vm.$store.extract({type: 'GET_SOME_DATA', id: 1});
// or
vm.$store.extract('GET_SOME_DATA', {id: 1});
</pre></div>
<p>The most important thing is that they'll be integrated with the modules system vuex has, and that's most convenient thing to have.</p>
<p>Let me know what do you think?</p>
<p>I can even try my hand around getting a PR for you guys, if you approve my idea.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    
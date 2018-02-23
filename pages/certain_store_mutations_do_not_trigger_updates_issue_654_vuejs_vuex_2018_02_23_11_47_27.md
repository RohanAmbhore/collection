<a href="https://github.com/vuejs/vuex/issues/654">https://github.com/vuejs/vuex/issues/654</a><div id="articleHeader"><h1>              Certain store mutations do not trigger updates            #654    </h1></div>


  <div>
    
    <div>
        <a href="/quicky84" target="_blank">quicky84</a>  opened this Issue
        <relative-time>on Feb 24, 2017</relative-time>
        · 8 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            





            
  

    



    
      

  
    
      
          <p>Hi there,</p>
<p>I have a pretty basic Vue+Vuex setup.<br />
Let A be a component with a computed field which depends on the Vuex store and a lifecycle hook --- created() which dispatches an event to the store to request some data from a RESTful server.</p>
<p>The expected behavior and a deviation from it are as follows:</p>
<ol>
<li>created() dispatches an event to the store; <strong>goes well</strong></li>
<li>the store makes requests and commits data; <strong>goes well</strong></li>
<li>mutation updates the state; <strong>goes well</strong> (this can be seen in the developers tab of Vue in Chrome)</li>
<li>computed field is updated triggering a re-render of the template; <strong>it depends</strong></li>
</ol>
<p>The last procedure goes well, i.e., the component template is re-rendered after the updates, if the field of the store being updated is an array and this array is updated with methods like push(), splice() (may be others too, but I did not investigate further).</p>
<p>The last procedure does not go well, if the field of the store being updated is an array and this array is updated via index access, e.g., array[n] = data. Or if the field is an object.</p>
<p>I made a repository containing <a href="https://github.com/quicky84/vue-update" target="_blank">this example</a>.<br />
It contains a restful server which gives out some data and the Vue+Vuex setup I described. There in file store.ts I present two described options --- with the array and object --- they are marked with <code>!!!</code> in the beginnings of commented line.</p>
<p>By default the array option is active, so everything must update as expected. If you uncomment lines related to the object and comment those related to the array, no update of the component template will happen.</p>
      
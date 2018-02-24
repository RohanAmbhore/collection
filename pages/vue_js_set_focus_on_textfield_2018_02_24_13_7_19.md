<a href="https://laracasts.com/discuss/channels/vue/vuejs-set-focus-on-textfield">https://laracasts.com/discuss/channels/vue/vuejs-set-focus-on-textfield</a><div id="articleHeader"><h1>vue.js set focus on textfield</h1></div> <p><strong>Published 1 year ago
by <a href="https://laracasts.com/@Lars-Janssen" target="_blank">Lars-Janssen</a></strong></p> <div><div><div><div><p>Hello,</p> <p>How can I set focus on an input field in vue.js. I can't get it working...
And cannot find it in documentation?</p></div> <div><div><h5>Best Answer <small>
(As Selected By Lars-Janssen)
</small></h5> <div><div><div> <div> <div><div><p>Single page style app?</p> <p>I sgguest useing v-bind to set autofocus from false (default) to true when the component loads (ready()) inside a nextTick.</p> <p>Basically what this plugin does.
<a href="https://github.com/simplesmiler/vue-focus/blob/master/dist/vue-focus.js" target="_blank">https://github.com/simplesmiler/vue-focus/blob/master/dist/vue-focus.js</a></p> <p>As the page isn't refreshed and its entering the Dom the browser isn't exacuting the autofocus. But it will after the page is rendered on nextTick.</p></div>   <div><div><div> <div> <div><div><p>auto focus? use autofocus on the input tag as an attribute.</p> <pre><code>&lt;input type="text" autofocus /&gt;
</code></pre></div>    <div><div> <div> <div><div><p>Single page style app?</p> <p>I sgguest useing v-bind to set autofocus from false (default) to true when the component loads (ready()) inside a nextTick.</p> <p>Basically what this plugin does.
<a href="https://github.com/simplesmiler/vue-focus/blob/master/dist/vue-focus.js" target="_blank">https://github.com/simplesmiler/vue-focus/blob/master/dist/vue-focus.js</a></p> <p>As the page isn't refreshed and its entering the Dom the browser isn't exacuting the autofocus. But it will after the page is rendered on nextTick.</p></div>    <div><div> <div> <div><div><p>if you use Vue 2 and need set focus programmatic, use <code>ref</code> directive</p> <pre><code>&lt;input type='search' ref='search' placeholder='Keyword:'&gt;

&lt;script&gt;
export default{
   mounted(){
       this.$refs.search.focus();
   }
}
&lt;/script&gt;
</code></pre> <blockquote><p>UPDATED: use <code>mounted</code> instead of <code>created</code>
tanks to <a href="/@xkrupa12" target="_blank">@xkrupa12</a> for it.</p></blockquote></div>   <div><div> <div> <div><div><p><a href="/@alphaelf" target="_blank">@alphaelf</a> focus() should be called inside mounted() function, since in created(), ref might not be present yet.</p></div>   <div><div> <div> <div><div><p>Hi, the code below does not work for me.</p> <p>mounted() {
this.$refs.search.focus();
}</p></div>   <div><div> <div> <div><div><p>I simply did this and works great</p> <pre><code>&lt;template&gt;
   &lt;input type="text" v-focus&gt;
&lt;/template&gt;

&lt;script&gt;
 const focus = {
    inserted(el) {
      el.focus()
    },
  }

  export default {
    directives: { focus },
    // ... 
  }
&lt;/script&gt;
</code></pre></div>   <div><div> <div> <div><div><p>Sometimes you need to call focus in the next tick</p> <pre><code>    this.$nextTick(() =&gt; this.$refs.search.focus())
</code></pre></div>   <p>
Please <a href="#" target="_blank">sign in</a> or <a href="https://laracasts.com/signup?billing=none&title=You'll be posting on the forum in no time!" target="_blank">create an account</a> to participate in this conversation.
</p>
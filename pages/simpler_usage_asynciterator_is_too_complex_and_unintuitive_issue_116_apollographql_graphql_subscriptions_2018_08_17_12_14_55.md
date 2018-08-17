<a href="https://github.com/apollographql/graphql-subscriptions/issues/116">https://github.com/apollographql/graphql-subscriptions/issues/116</a><div id="articleHeader"><h1>              Simpler usage: AsyncIterator is too complex and unintuitive            #116    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/buckle2000" target="_blank">buckle2000</a>  opened this Issue
        <relative-time>on Oct 18, 2017</relative-time>
        · 14 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          <div>
            




            
<div id="issue-266386011">
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Is it possible to use this directly with node.js emitter? Current API is too complex.<br />
Or can we just use a callback function to achieve that?</p>
<div><pre>const resolvers = {
  Subscription: {
    somethingChanged: {
      subscribe: (cb) =&gt; {cb(null, value)}
    }
  }
}</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>

          </div>

          

  


  
<div>
    
  <div>

  




  
<div id="issuecomment-346703393">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm also wondering what the reasoning behind using an AsyncIterator rather than an EventEmitter or Observable.</p>
<p>It seems to me that in almost every case the data changes backing subscriptions would be events generated elsewhere in a system and this seems more suitable to a push paradigm rather than a pull one like AsyncIterator. Perhaps it simplifies other parts of the framework so I won't judge.</p>
<p>In any case the reference pubsub implementation uses an EventEmitter behind the scenes, and it is possible to pass this in during initialization, e.g.</p>
<pre><code>import { PubSub } from 'graphql-subscriptions';
...
export const pubsub = new PubSub({
  eventEmitter: yourEventEmitterHere
});
...
const resolvers = {
  Subscription: {
    somethingChanged: {
      subscribe: () =&gt; pubsub.asyncIterator(YOUR_TOPIC),
    }
  }
}
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
  <h3 id="event-1356473977">

    
      
    

    

        
  <a href="/buckle2000" target="_blank">buckle2000</a>
  


      
changed the title from
Simpler usage
to
Simpler usage: AsyncIterator is too complex and unintuitive


    <a href="#event-1356473977" target="_blank"><relative-time>on Nov 24, 2017</relative-time></a>

  </h3>
</div>



</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-346898579">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>On looking into it a bit more it seems that the reference implementation by the graphql team uses AsyncIterator: <a href="https://github.com/graphql/graphql-js/blob/master/src/subscription/subscribe.js" target="_blank">https://github.com/graphql/graphql-js/blob/master/src/subscription/subscribe.js</a> so there is probably not too much the Apollo team can do about it.</p>
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

  




  
<div id="issuecomment-347095363">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ravenscar" target="_blank">@ravenscar</a> Why can't they? IMHO, reference implementation does not mean much at this stage.<br />
Additionally, AsyncIterators and Observables can live side by side if needed for some reason.</p>
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

  




  
<div id="issuecomment-348885784">
    
  <div>

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/vjpr" target="_blank">vjpr</a>
  

    </strong>

    commented

    <a href="#issuecomment-348885784" target="_blank"><relative-time>on Dec 4, 2017</relative-time></a>


    
      <include-fragment>
            
  •


  
    <summary>
      <div>
        
            edited
        
        
      </div>
    </summary>
    
  

      </include-fragment>
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I found this odd too. AsyncIterator requires pulling data using <code>next</code>. But with web-sockets I generally want to push data when events occur. Only thing I can think of is that by using pull-based they can rate-limit or something.</p>
<hr />
<p>See <a href="https://github.com/facebook/graphql/blob/master/rfcs/Subscriptions.md" target="_blank">https://github.com/facebook/graphql/blob/master/rfcs/Subscriptions.md</a></p>
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

  




  
<div id="issuecomment-350793303">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Actually I think using AsyncIterators is pretty smart.  I believe they will be widespread in future reactive programming because they will be the first API built into standard JS VMs that can stream change events to observers, as well as the most generic API for doing so.</p>
<p>Although it seems like you pull data from an AsyncIterator, in truth it is more like a <strong>hybrid push-pull interface</strong> since calling <code>next</code> can wait any amount of time for the AsyncIterator to <code>yield</code> something (for example, when a Redis wrapper pushes data to it).  In fact, if you look at how they implemented the <code>EventEmitter</code> wrapper, it has <code>pullQueue</code> and <code>pushQueue</code> fields.</p>
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

  




  
<div id="issuecomment-350884025">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/amitport" target="_blank">@amitport</a> while that's true, I can understand why the authors of this package would prefer to conform to the current standard from the reference implementation rather than implement something proprietary.</p>
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

  




  
<div id="issuecomment-350884655">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/vjpr" target="_blank">@vjpr</a> to expand on my first comment, nothing about using <code>AsyncIterator</code>s prevents pushing data over the web sockets when events occur.  <code>graphql</code> will keep waiting for the <code>next</code> payload from the <code>AsyncIterator</code>, which it can <code>yield</code> whenever it wants.  (Synchronous <code>Iterators</code> wouldn't work at all for this case since you can't wait for them to <code>yield</code> something, but <code>AsyncIterator</code>s work just fine).</p>
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

  




  
<div id="issuecomment-350969344">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/jedwards1211" target="_blank">@jedwards1211</a> bottom line I think ease of development should count for something and that the current state of it is not very good. (without disregarding other factors, like reference implementation)</p>
<p>also, I'm not sure what you meant by "implement something propriety". I didn't advocate specific libraries, but there are some that are easy to use, very popular, stable, free and open source. (there's nothing wrong with using a library when appropriate)</p>
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

  




  
<div id="issuecomment-350974561">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>When I first commented in this thread I was fairly annoyed at having to use AsyncIterators when I though that callbacks/eventEmitters would do, however I have since changed my view as they solve a very important piece of functionality.</p>
<p>When you are on a mobile device and you step into an elevator/lose you connection all of your subscription events will stack up in a queue inside the AsyncIterator, and when your socket reconnects later, they will be delivered to you.</p>
<p>Just using callbacks/eventEmitters/observables to for subscriptions means that if you were disconnected then you would just miss out on the event.</p>
<p>This is a pretty strong case for using AsyncIterators when dealing with flakey websocket connections, however as others have mentioned it would be nice if this was used behind the scenes and we were given the option to use callbacks or eventEmitters directly in the API.</p>
<p>I guess it's new and this functionality may come.</p>
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

  




  
<div id="issuecomment-351093073">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/NeoPhi" target="_blank">NeoPhi</a>
  

    </strong>

    commented

    <a href="#issuecomment-351093073" target="_blank"><relative-time>on Dec 12, 2017</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>As mentioned above, the key reason AsyncIterator was used is that it is close to being added as a core language feature: <a href="https://github.com/tc39/proposal-async-iteration" target="_blank">https://github.com/tc39/proposal-async-iteration</a></p>
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

  




  
<div id="issuecomment-351123925">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/amitport" target="_blank">@amitport</a> <a href="https://github.com/buckle2000" target="_blank">@buckle2000</a> if you guys don't want to work with AsyncIterators directly, you could work with EventEmitters and then use their function to convert to an AsyncIterator: <a href="https://github.com/apollographql/graphql-subscriptions/blob/master/src/event-emitter-to-async-iterator.ts" target="_blank">https://github.com/apollographql/graphql-subscriptions/blob/master/src/event-emitter-to-async-iterator.ts</a></p>
<p>You could make a similar function for wrapping an RxJS stream or similar.  I think that's the other reason AsyncIterator was chosen: it's not very difficult to adapt other libraries to push data through an AsyncIterator.</p>
<p><a href="https://github.com/NeoPhi" target="_blank">@NeoPhi</a> I think we should extract a "PushAsyncIterator" class from event-emitter-to-async-iterator.ts that has a <code>push</code> method we can call from the EventEmitter listener or whatever else we want to push data from.  That would make it easier for folks to adapt proprietary libs.  Though I think stuff like this deserves to live in its own package that graphql-subscriptions consumes.</p>
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

  




  
<div id="issuecomment-351958387">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>if you want to use RxJs instead of not-comfortable AsyncIterators, you are welcome to use <code>graphql-rxjs</code> (<a href="https://github.com/DxCx/graphql-rxjs" target="_blank">https://github.com/DxCx/graphql-rxjs</a>)</p>
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

  




  
<div id="issuecomment-352142354">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/DxCx" target="_blank">@DxCx</a> does using that fork have some kind of advantages over using some utility function to wrap RxJS observables in an <code>AsyncIterator</code>?</p>
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

  




  
<div id="issuecomment-352165016">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/jedwards1211" target="_blank">@jedwards1211</a> this will give you 2 things:</p>
<ol>
<li>Execution engine patches to support live/defer directives</li>
<li>AsyncIterator wrappers from/to RxJs</li>
</ol>
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










        
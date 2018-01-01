<a href="https://stackoverflow.com/questions/20714460/break-promise-chain-and-call-a-function-based-on-the-step-in-the-chain-where-it">https://stackoverflow.com/questions/20714460/break-promise-chain-and-call-a-function-based-on-the-step-in-the-chain-where-it</a><div id="articleHeader"><h1>Break promise chain and call a function based on the step in the chain where it is broken (rejected)</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        85
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>37</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<h3>Update:</h3>

<p>To help future viewers of this post, I created <strong><a href="http://jsbin.com/EpaZIsIp/18/edit" target="_blank">this demo of pluma's answer</a>.</strong> </p>

<h2>Question:</h2>

<p>My goal seems fairly straightforward.</p>

<pre><code>  step(1)
  .then(function() {
    return step(2);
  }, function() {
    stepError(1);
    return $q.reject();
  })
  .then(function() {

  }, function() {
    stepError(2);
  });

  function step(n) {
    var deferred = $q.defer();
    //fail on step 1
    (n === 1) ? deferred.reject() : deferred.resolve();
    return deferred.promise;
  }
  function stepError(n) {
    console.log(n); 
  }</code></pre>

<p>The problem here is that if I fail on step 1, both <code>stepError(1)</code> AND <code>stepError(2)</code> are fired. If I don't <code>return $q.reject</code> then <code>stepError(2)</code> won't be fired, but <code>step(2)</code> will, which I understand. I've accomplished everything except what I'm trying to do.</p>

<p>How do I write promises so that I can call a function on rejection, without calling all of the functions in the error chain? Or is there another way to accomplish this?</p>

<p><a href="http://jsbin.com/EpaZIsIp/3/edit" target="_blank"><strong>Here's a live demo</strong></a> so you've got something work with.</p>

<h2>Update:</h2>

<p>I <strong><em>kind of</em></strong> have solved it. Here, I am catching the error at the end of the chain and passing the data to <code>reject(data)</code> so that I will know what issue to handle in the error function. This actually doesn't meet my requirements because I don't want to depend on the data. It would be lame, but in my case it would be cleaner to pass an error callback to the function rather than to depend on the returned data to determine what to do.</p>

<p><strong><a href="http://jsbin.com/EpaZIsIp/10/edit" target="_blank">Live demo here (click).</a></strong></p>

<pre><code>step(1)
  .then(function() {
    return step(2);
  })
  .then(function() {
    return step(3);
  })
  .then(false, 
    function(x) {
      stepError(x);
    }
  );
  function step(n) {
    console.log('Step '+n);
    var deferred = $q.defer();
    (n === 1) ? deferred.reject(n) : deferred.resolve(n);
    return deferred.promise;
  }
  function stepError(n) {
    console.log('Error '+n); 
  }</code></pre>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    <div id="comments-20714460">
		        <table>
                    <tbody>



    <tr id="comment-31031549">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                There is an async javascript lib that might Help if this becomes any more complicated
                    – <a href="/users/1366293/lucuma" title="16,231 reputation" target="_blank">lucuma</a>
                <a href="#comment31031549_20714460" target="_blank">Dec 21 '13 at 3:51</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-20714460">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-20715224">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        133
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>The reason your code doesn't work as expected is that it's actually doing something different from what you think it does.</p>

<p>Let's say you have something like the following:</p>

<pre><code>stepOne()
.then(stepTwo, handleErrorOne)
.then(stepThree, handleErrorTwo)
.then(null, handleErrorThree);</code></pre>

<p>To better understand what's happening, let's pretend this is synchronous code with <code>try</code>/<code>catch</code> blocks:</p>

<pre><code>try {
    try {
        try {
            var a = stepOne();
        } catch(e1) {
            a = handleErrorOne(e1);
        }
        var b = stepTwo(a);
    } catch(e2) {
        b = handleErrorTwo(e2);
    }
    var c = stepThree(b);
} catch(e3) {
    c = handleErrorThree(e3);
}</code></pre>

<p>The <code>onRejected</code> handler (the second argument of <code>then</code>) is essentially an error correction mechanism (like a <code>catch</code> block). If an error is thrown in <code>handleErrorOne</code>, it will be caught by the next catch block (<code>catch(e2)</code>), and so on.</p>

<p>This is obviously not what you intended.</p>

<p>Let's say we want the entire resolution chain to fail no matter what goes wrong:</p>

<pre><code>stepOne()
.then(function(a) {
    return stepTwo(a).then(null, handleErrorTwo);
}, handleErrorOne)
.then(function(b) {
    return stepThree(b).then(null, handleErrorThree);
});</code></pre>

<p>Note: We can leave the <code>handleErrorOne</code> where it is, because it will only be invoked if <code>stepOne</code> rejects (it's the first function in the chain, so we know that if the chain is rejected at this point, it can only be because of that function's promise).</p>

<p>The important change is that the error handlers for the other functions are not part of the main promise chain. Instead, each step has its own "sub-chain" with an <code>onRejected</code> that is only called if the step was rejected (but can not be reached by the main chain directly).</p>

<p>The reason this works is that both <code>onFulfilled</code> and <code>onRejected</code> are optional arguments to the <code>then</code> method. If a promise is fulfilled (i.e. resolved) and the next <code>then</code> in the chain doesn't have an <code>onFulfilled</code> handler, the chain will continue until there is one with such a handler.</p>

<p>This means the following two lines are equivalent:</p>

<pre><code>stepOne().then(stepTwo, handleErrorOne)
stepOne().then(null, handleErrorOne).then(stepTwo)</code></pre>

<p>But the following line is <em>not</em> equivalent to the two above:</p>

<pre><code>stepOne().then(stepTwo).then(null, handleErrorOne)</code></pre>

<p>Angular's promise library <code>$q</code> is based on kriskowal's <code>Q</code> library (which has a richer API, but contains everything you can find in <code>$q</code>). Q's <a href="https://github.com/kriskowal/q/wiki/API-Reference" target="_blank">API docs</a> on GitHub could prove useful. Q implements the <a href="http://promises-aplus.github.io/promises-spec/" target="_blank">Promises/A+ spec</a>, which goes into detail on how <code>then</code> and the promise resolution behaviour works exactly.</p>

<p>EDIT:</p>

<p>Also keep in mind that if you want to break out of the chain in your error handler, it needs to return a rejected promise or throw an Error (which will be caught and wrapped in a rejected promise automatically). If you don't return a promise, <code>then</code> wraps the return value in a resolve promise for you. </p>

<p><strong>This means that if you don't return anything, you are effectively returning a resolved promise for the value <code>undefined</code>.</strong></p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-20715224">
		        <table>
                    <tbody>



    <tr id="comment-47141765">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                80
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This part is gold: <code>if you don't return anything, you are effectively returning a resolved promise for the value undefined.</code> Thanks @pluma
                    – <a href="/users/1071793/colthreepv" title="848 reputation" target="_blank">colthreepv</a>
                <a href="#comment47141765_20715224" target="_blank">Apr 7 '15 at 12:16</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-52816166">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                4
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This is indeed. I'm editing it to give it the bold it deserves
                    – <a href="/users/4578952/cyril-chapon" title="647 reputation" target="_blank">Cyril CHAPON</a>
                <a href="#comment52816166_20715224" target="_blank">Sep 9 '15 at 11:01</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-54870342">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                does reject exit the current function? eg resolve will not be called if reject is called 1st     ` if (bad) {         reject(status);       }       resolve(results);`
                    – <a href="/users/3915717/superuberduper" title="3,453 reputation" target="_blank">SuperUberDuper</a>
                <a href="#comment54870342_20715224" target="_blank">Nov 5 '15 at 13:07</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-57857855">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                <code>stepOne().then(stepTwo, handleErrorOne)</code>    ` stepOne().then(null, handleErrorOne).then(stepTwo)`    Are these trully equivalent? I think in case of rejection in <code>stepOne</code> the second line of code will execute <code>stepTwo</code> but the first will only execute <code>handleErrorOne</code> and stop. Or am I missing something?
                    – <a href="/users/2067580/jeff" title="111 reputation" target="_blank">JeFf</a>
                <a href="#comment57857855_20715224" target="_blank">Jan 28 '16 at 16:52</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-59821570">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Does not really provide a clear solution for the question asked, good explanation nevertheless
                    – <a href="/users/1597656/yerken" title="1,605 reputation" target="_blank">Yerken</a>
                <a href="#comment59821570_20715224" target="_blank">Mar 18 '16 at 15:45</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-20715224">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-35503793">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        30
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Bit late to the party but this simple solution worked for me:</p>

<pre><code>function chainError(err) {
  return Promise.reject(err)
};

stepOne()
.then(stepTwo, chainError)
.then(stepThreee, chainError);</code></pre>

<p>This allows you to <em>break</em> out of the chain.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Feb 19 '16 at 11:06
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-35503793">
		        <table>
                    <tbody>



    <tr id="comment-70198570">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Helped me but FYI, you can return it in the then to break out in the catch like: <code>.then(user =&gt; { if (user) return Promise.reject('The email address already exists.') })</code>
                    – <a href="/users/2110294/craig-van-tonder" title="2,720 reputation" target="_blank">Craig van Tonder</a>
                <a href="#comment70198570_35503793" target="_blank">Jan 5 '17 at 22:56</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-71010526">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                @CraigvanTonder you can just throw within a promise and it will work the same as yours code: <code>.then(user =&gt; { if (user) throw 'The email address already exists.' }) </code>
                    – <a href="/users/938236/francisco-presencia" title="5,923 reputation" target="_blank">Francisco Presencia</a>
                <a href="#comment71010526_35503793" target="_blank">Jan 28 '17 at 20:41</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-72107265">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                This is the only correct answer. Otherwise step 3 will still execute even step 1 has error.
                    – <a href="/users/4596207/wdetac" title="239 reputation" target="_blank">wdetac</a>
                <a href="#comment72107265_35503793" target="_blank">Feb 27 '17 at 10:53</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-80660151">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Just to clarify, if an error takes place in stepOne(), then both the chainError gets invoked right? If this desirable. I have a snippet which does this, not sure if i misunderstood anything - <a href="https://runkit.com/embed/9q2q3rjxdar9" target="_blank">runkit.com/embed/9q2q3rjxdar9</a>
                    – <a href="/users/320550/user320550" title="376 reputation" target="_blank">user320550</a>
                <a href="#comment80660151_35503793" target="_blank">Oct 20 '17 at 19:48</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-35503793">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-34374132">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>When rejecting you should pass an rejection error, then wrap step error handlers in a function that checks whether the rejection should be processed or "rethrown" until the end of the chain :</p>

<pre><code>// function mocking steps
function step(i) {
    i++;
    console.log('step', i);
    return q.resolve(i);
}

// function mocking a failing step
function failingStep(i) {
    i++;
    console.log('step '+ i + ' (will fail)');
    var e = new Error('Failed on step ' + i);
    e.step = i;
    return q.reject(e);
}

// error handler
function handleError(e){
    if (error.breakChain) {
        // handleError has already been called on this error
        // (see code bellow)
        log('errorHandler: skip handling');
        return q.reject(error);
    }
    // firs time this error is past to the handler
    console.error('errorHandler: caught error ' + error.message);
    // process the error 
    // ...
    //
    error.breakChain = true;
    return q.reject(error);
}

// run the steps, will fail on step 4
// and not run step 5 and 6
// note that handleError of step 5 will be called
// but since we use that error.breakChain boolean
// no processing will happen and the error will
// continue through the rejection path until done(,)

  step(0) // 1
  .catch(handleError)
  .then(step) // 2
  .catch(handleError)
  .then(step) // 3
  .catch(handleError)
  .then(failingStep)  // 4 fail
  .catch(handleError)
  .then(step) // 5
  .catch(handleError)
  .then(step) // 6
  .catch(handleError)
  .done(function(){
      log('success arguments', arguments);
  }, function (error) {
      log('Done, chain broke at step ' + error.step);
  });</code></pre>

<p>What you'd see on the console :</p>

<pre><code>step 1
step 2
step 3
step 4 (will fail)
errorHandler: caught error 'Failed on step 4'
errorHandler: skip handling
errorHandler: skip handling
Done, chain broke at step 4</code></pre>

<p>Here is some working code
<a href="https://jsfiddle.net/8hzg5s7m/3/" target="_blank">https://jsfiddle.net/8hzg5s7m/3/</a></p>

<p>If you have specific handling for each step, your wrapper could be something like:</p>

<pre><code>/*
 * simple wrapper to check if rejection
 * has already been handled
 * @param function real error handler
 */
function createHandler(realHandler) {
    return function(error) {
        if (error.breakChain) {
            return q.reject(error);
        }
        realHandler(error);
        error.breakChain = true;
        return q.reject(error);    
    }
}</code></pre>

<p>then your chain</p>

<pre><code>step1()
.catch(createHandler(handleError1Fn))
.then(step2)
.catch(createHandler(handleError2Fn))
.then(step3)
.catch(createHandler(handleError3Fn))
.done(function(){
    log('success');
}, function (error) {
    log('Done, chain broke at step ' + error.step);
});</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 19 '15 at 18:43
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-34374132">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-33671978">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Attach error handlers as separate chain elements directly to the execution of the steps:</p>

<pre><code>        // Handle errors for step(1)
step(1).then(null, function() { stepError(1); return $q.reject(); })
.then(function() {
                 // Attach error handler for step(2),
                 // but only if step(2) is actually executed
  return step(2).then(null, function() { stepError(2); return $q.reject(); });
})
.then(function() {
                 // Attach error handler for step(3),
                 // but only if step(3) is actually executed
  return step(3).then(null, function() { stepError(3); return $q.reject(); });
});</code></pre>

<p>or using <code>catch()</code>:</p>

<pre><code>       // Handle errors for step(1)
step(1).catch(function() { stepError(1); return $q.reject(); })
.then(function() {
                 // Attach error handler for step(2),
                 // but only if step(2) is actually executed
  return step(2).catch(function() { stepError(2); return $q.reject(); });
})
.then(function() {
                 // Attach error handler for step(3),
                 // but only if step(3) is actually executed
  return step(3).catch(function() { stepError(3); return $q.reject(); });
});</code></pre>

<p>Note: This is basically the same pattern as <a href="https://stackoverflow.com/a/20715224/490560" target="_blank">pluma suggests in his answer</a> but using the OP's naming.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-33671978">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-20720618">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<pre><code>var s = 1;
start()
.then(function(){
    return step(s++);
})
.then(function() {
    return step(s++);
})
.then(function() {
    return step(s++);
})
.then(0, function(e){
   console.log(s-1); 
});</code></pre>

<p><a href="http://jsbin.com/EpaZIsIp/20/edit" target="_blank">http://jsbin.com/EpaZIsIp/20/edit</a></p>

<p>Or automated for any number of steps:</p>

<pre><code>var promise = start();
var s = 1;
var l = 3;
while(l--) {
    promise = promise.then(function() {
        return step(s++);
    });
}
promise.then(0, function(e){
   console.log(s-1); 
});</code></pre>

<p><a href="http://jsbin.com/EpaZIsIp/21/edit" target="_blank">http://jsbin.com/EpaZIsIp/21/edit</a></p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 21 '13 at 15:38
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-20720618">
		        <table>
                    <tbody>



    <tr id="comment-74230448">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                But If i will call <code>deferred.reject(n)</code> then I am getting warning that promise rejected with a nonError object
                    – <a href="/users/1367349/9me" title="557 reputation" target="_blank">9me</a>
                <a href="#comment74230448_20720618" target="_blank">Apr 24 '17 at 14:15</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-20720618">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-20716023">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>What you need is a repeating <code>.then()</code> chain with a special case to start and a special case to finish.</p>

<p>The knack is to get the step number of the failure case to ripple through to a final error handler.</p>

<ul>
<li>Start: call <code>step(1)</code> unconditionally.</li>
<li>Repeating pattern: chain a <code>.then()</code> with the following callbacks:

<ul>
<li>success: call step(n+1)</li>
<li>failure: throw the value with which the previous deferered was rejected or rethrow the error.</li>
</ul></li>
<li>Finish: chain a <code>.then()</code> with no success handler and a final error handler.</li>
</ul>

<p>You can write the whole thing out longhand but it's easier to demonstrate the pattern with named, generalised functions :</p>

<pre><code>function nextStep(n) {
    return step(n + 1);
}

function step(n) {
    console.log('step ' + n);
    var deferred = $q.defer();
    (n === 3) ? deferred.reject(n) : deferred.resolve(n);
    return deferred.promise;
}

function stepError(n) {
    throw(n);
}

function finalError(n) {
    console.log('finalError ' + n);
}
step(1)
    .then(nextStep, stepError)
    .then(nextStep, stepError)
    .then(nextStep, stepError)
    .then(nextStep, stepError)
    .then(nextStep, stepError)
    .then(null, finalError);});</code></pre>

<p>see <a href="http://jsfiddle.net/9z9fw/" target="_blank">demo</a></p>

<p>Note how in <code>step()</code>, the deferred is rejected or resolved with <code>n</code>, thus making that value available to the callbacks in the next <code>.then()</code> in the chain. Once <code>stepError</code> is called, the error is repeatedly rethrown until it is handled by <code>finalError</code>.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 21 '13 at 6:00
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-20716023">
		        <table>
                    <tbody>



    <tr id="comment-31032883">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Informative answer so it's worth keeping, but that's not the issue I'm facing. I mention this solution in my post and it is not what I'm looking for. See the demo at the top of my post.
                    – <a href="/users/1435655/m59" title="34,577 reputation" target="_blank">m59</a>
                <a href="#comment31032883_20716023" target="_blank">Dec 21 '13 at 6:10</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-31033230">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                m59, this is an answer to the question asked, "how do I write promises so that I can call a function on rejection, without calling all of the functions in the error chain?" and the title of the question, "Break promise chain and call a function based on the step in the chain where it is broken (rejected)"
                    – <a href="/users/1142252/beetroot-beetroot" title="16,265 reputation" target="_blank">Beetroot-Beetroot</a>
                <a href="#comment31033230_20716023" target="_blank">Dec 21 '13 at 6:37</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-31033328">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Right, like I said, it's informative and I even included this solution in my post (with less detail). This approach is intended for fixing things so that the chain can continue. While it <i>can</i> accomplish what I'm looking for, it's not as natural as the approach in the accepted answer. In other words, if you want to do what is expressed by the title and the question asked, take pluma's approach.
                    – <a href="/users/1435655/m59" title="34,577 reputation" target="_blank">m59</a>
                <a href="#comment31033328_20716023" target="_blank">Dec 21 '13 at 6:45</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-20716023">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-20714671">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>If I understand correctly, you want only the error for the failing step to show, right?</p>

<p>That should be as simple as changing the failure case of the first promise to this:</p>

<pre><code>step(1).then(function (response) {
    step(2);
}, function (response) {
    stepError(1);
    return response;
}).then( ... )</code></pre>

<p>By returning <code>$q.reject()</code> in the first step's failure case, you're rejecting that promise, which causes the errorCallback to be called in the 2nd <code>then(...)</code>.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 21 '13 at 2:07
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-20714671">
		        <table>
                    <tbody>



    <tr id="comment-31030604">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                What in the world...that's exactly what I did! See in my post that I did try that, but the chain would kick back in and run <code>step(2)</code>. Now I just tried it again it's not happening. I'm so confused.
                    – <a href="/users/1435655/m59" title="34,577 reputation" target="_blank">m59</a>
                <a href="#comment31030604_20714671" target="_blank">Dec 21 '13 at 2:13</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-31030622">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                1
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                I did see that you mentioned that. That's bizarre though. That function that contains <code>return step(2);</code> should only ever be called when <code>step(1)</code> resolves successfully.
                    – <a href="/users/749004/zajn" title="3,593 reputation" target="_blank">Zajn</a>
                <a href="#comment31030622_20714671" target="_blank">Dec 21 '13 at 2:15</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-31030632">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Scratch that - it definitely is happening. Like I said in my post, if you don't use <code>return $q.reject()</code>, the chain is going to keep going. In this case <code>return response</code> messed it up. See this: <a href="http://jsbin.com/EpaZIsIp/6/edit" target="_blank">jsbin.com/EpaZIsIp/6/edit</a>
                    – <a href="/users/1435655/m59" title="34,577 reputation" target="_blank">m59</a>
                <a href="#comment31030632_20714671" target="_blank">Dec 21 '13 at 2:16</a>
                        
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-31030643">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Hmm, okay. It appears to work in the jsbin you posted when I changed that, but I must have missed something.
                    – <a href="/users/749004/zajn" title="3,593 reputation" target="_blank">Zajn</a>
                <a href="#comment31030643_20714671" target="_blank">Dec 21 '13 at 2:17</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-31030664">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                  
                        </td>
                        <td>
                                <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                        </td>
                    </tr>
                        <tr>
                            <td> </td>
                                <td>
                                    <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                                </td>
                        </tr>
                </tbody>
            </table>
        </td>
        <td>
            <div>
                Yeah I definitely see that not working now. Back to the drawing board for me!
                    – <a href="/users/749004/zajn" title="3,593 reputation" target="_blank">Zajn</a>
                <a href="#comment31030664_20714671" target="_blank">Dec 21 '13 at 2:19</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-20714671">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>2</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/angularjs" title="show questions tagged 'angularjs'" target="_blank">angularjs</a> <a href="/questions/tagged/promise" title="show questions tagged 'promise'" target="_blank">promise</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
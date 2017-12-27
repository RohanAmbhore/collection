<a href="https://stackoverflow.com/questions/2833951/how-do-i-catch-an-ajax-query-post-error">https://stackoverflow.com/questions/2833951/how-do-i-catch-an-ajax-query-post-error</a><div id="articleHeader"><h1>How do I catch an Ajax query post error?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        140
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>24</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I would like to catch the error and show the appropriate message if the Ajax request fails.</p>

<p>My code is like the following, but I could not manage to catch the failing Ajax request.</p>

<pre><code>function getAjaxData(id)
{
     $.post("status.ajax.php", {deviceId : id}, function(data){

        var tab1;

        if (data.length&gt;0) {
            tab1 = data;
        }
        else {
            tab1 = "Error in Ajax";
        }

        return tab1;
    });
}</code></pre>

<p>I found out that, "Error in Ajax" is never executed when the Ajax request failed.</p>

<p>How do I handle the Ajax error and show the appropriate message if it fails?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-2833951">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-2833968">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        169
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>Since jQuery 1.5 you can use the deferred objects mechanism:</p>

<pre><code>$.post('some.php', {name: 'John'})
    .done(function(msg){  })
    .fail(function(xhr, status, error) {
        // error handling
    });</code></pre>

<p>Another way is using <code>.ajax</code>:</p>

<pre><code>$.ajax({
  type: "POST",
  url: "some.php",
  data: "name=John&location=Boston",
  success: function(msg){
        alert( "Data Saved: " + msg );
  },
  error: function(XMLHttpRequest, textStatus, errorThrown) {
     alert("some error");
  }
});</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-2833968">
		        <table>
                    <tbody>



    <tr id="comment-16200058">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                14
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
                @Yuck $.post can accept an error callback using deferred objects. Take a look at my answer below for an example.
                    – <a href="/users/91303/michael-venable" title="4,004 reputation" target="_blank">Michael Venable</a>
                <a href="#comment16200058_2833968" target="_blank">Aug 24 '12 at 21:18</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-20218575">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
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
                Also, I way to make <code>$.ajax</code> more readable is to use a hash for your <code>data</code>. For example: <code>{ name : 'John', location: 'Boston' }</code>
                    – <a href="/users/877095/briangonzalez" title="1,246 reputation" target="_blank">briangonzalez</a>
                <a href="#comment20218575_2833968" target="_blank">Jan 24 '13 at 15:56</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-30188184">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
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
                The success and error callbacks above are obsolete as of jQuery 1.8 <a href="http://api.jquery.com/jQuery.post/" target="_blank">api.jquery.com/jQuery.post</a>
                    – <a href="/users/137474/baldy" title="2,812 reputation" target="_blank">Baldy</a>
                <a href="#comment30188184_2833968" target="_blank">Nov 27 '13 at 11:53</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-43548101">
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
                @MichaelVeneble i think you can use <code>$.post().error()</code>
                    – <a href="/users/3635391/clintgh" title="1,018 reputation" target="_blank">clintgh</a>
                <a href="#comment43548101_2833968" target="_blank">Dec 19 '14 at 6:58</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-56513780">
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
            
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-2833968">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-2833972">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        78
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<pre><code>$.ajax({
  type: 'POST',
  url: 'status.ajax.php',
  data: {
     deviceId: id
  },
  success: function(data){
     // your code from above
  },
  error: function(xhr, textStatus, error){
      console.log(xhr.statusText);
      console.log(textStatus);
      console.log(error);
  }
});</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered May 14 '10 at 12:12
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
	    

        <div id="comments-link-2833972">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-2833973">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        10
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>A simple way is to implement <a href="http://api.jquery.com/ajaxError/" target="_blank">ajaxError</a>:</p>

<blockquote>
  <p>Whenever an Ajax request completes
  with an error, jQuery triggers the
  ajaxError event. Any and all handlers
  that have been registered with the
  .ajaxError() method are executed at
  this time.</p>
</blockquote>

<p>For example:</p>

<pre><code>$('.log').ajaxError(function() {
  $(this).text('Triggered ajaxError handler.');
});</code></pre>

<p>I would suggest reading the <a href="http://api.jquery.com/ajaxError/" target="_blank">ajaxError</a> documentation. It does more than the simple use-case demonstrated above - mainly its callback accepts a number of parameters:</p>

<pre><code>$('.log').ajaxError(function(e, xhr, settings, exception) {
  if (settings.url == 'ajax/missing.html') {
    $(this).text('Triggered ajaxError handler.');
  }
});</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-2833973">
		        <table>
                    <tbody>



    <tr id="comment-2875244">
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
                +1 - I would add that this handler gets several arguments, so you can display the actual error, response code, url, etc.
                    – <a href="/users/13249/nick-craver" title="489,984 reputation" target="_blank">Nick Craver♦</a>
                <a href="#comment2875244_2833973" target="_blank">May 14 '10 at 12:14</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-2875295">
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
            
        </td>
    </tr>
    <tr id="comment-2875298">
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
                Excellent...but you can't get a +2 out of me! :)
                    – <a href="/users/13249/nick-craver" title="489,984 reputation" target="_blank">Nick Craver♦</a>
                <a href="#comment2875298_2833973" target="_blank">May 14 '10 at 12:25</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-48051574">
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
                Note that as of jQuery 1.8, the .ajaxError() method should only be attached to document.
                    – <a href="/users/1992615/nanki" title="390 reputation" target="_blank">Nanki</a>
                <a href="#comment48051574_2833973" target="_blank">Apr 30 '15 at 11:00</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-2833973">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-12116790">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        237
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>jQuery 1.5 added deferred objects that handle this nicely. Simply call <code>$.post</code> and attach any handlers you'd like after the call. Deferred objects even allow you to attach multiple success and error handlers.</p>

<p>Example:</p>

<pre><code>$.post('status.ajax.php', {deviceId: id})
    .done( function(msg) { ... } )
    .fail( function(xhr, textStatus, errorThrown) {
        alert(xhr.responseText);
    });</code></pre>

<p>Prior to jQuery 1.8, the function <code>done</code> was called <code>success</code> and <code>fail</code> was called <code>error</code>.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-12116790">
		        <table>
                    <tbody>



    <tr id="comment-16201655">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                3
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
                +1 Very nice, but still not crazy about the syntax.  Hopefully it gets unified in a future release.
                    – <a href="/users/719034/yuck" title="34,250 reputation" target="_blank">Yuck</a>
                <a href="#comment16201655_12116790" target="_blank">Aug 24 '12 at 22:55</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-31236668">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                19
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
                This should be the accepted answer. The current accepted answer is "use a different method"; this answer says "here's how to make your method work". The latter is usually preferred on SO. Actually, this should be included in the $.post documentation!!!
                    – <a href="/users/122763/mehaase" title="15,769 reputation" target="_blank">mehaase</a>
                <a href="#comment31236668_12116790" target="_blank">Dec 29 '13 at 18:53</a>
                                                                            </div>
        </td>
    </tr>
    <tr id="comment-39698907">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
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
            
        </td>
    </tr>
    <tr id="comment-47450326">
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
                By the way there is also <code>responseJSON</code> property which is also very handy in case of ajax type is <code>json</code>.
                    – <a href="/users/837165/ivkremer" title="737 reputation" target="_blank">ivkremer</a>
                <a href="#comment47450326_12116790" target="_blank">Apr 15 '15 at 16:06</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-12116790">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-22106347">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        12
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<pre><code>$.post('someUri', { }, 
  function(data){ doSomeStuff })
 .fail(function(error) { alert(error.responseJSON) });</code></pre>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Feb 28 '14 at 21:39
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
	    <div id="comments-22106347">
		        <table>
                    <tbody>



    <tr id="comment-33535137">
        <td>
            <table>
                <tbody>
                    <tr>
                        <td>
                                2
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
                Adding a bit more explanation here would help future readers.
                    – <a href="/users/175201/eric-brown" title="11,943 reputation" target="_blank">Eric Brown</a>
                <a href="#comment33535137_22106347" target="_blank">Feb 28 '14 at 22:20</a>
                                                                            </div>
        </td>
    </tr>
                    </tbody>
		        </table>
	    </div>

        <div id="comments-link-22106347">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-41452110">
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
<p>I fixed this problem by declaring <code>datatype: 'json'</code> in my jQuery ajax call.</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-41452110">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/jquery" title="show questions tagged 'jquery'" target="_blank">jquery</a> <a href="/questions/tagged/ajax" title="show questions tagged 'ajax'" target="_blank">ajax</a> <a href="/questions/tagged/post" title="show questions tagged 'post'" target="_blank">post</a> <a href="/questions/tagged/error-handling" title="show questions tagged 'error-handling'" target="_blank">error-handling</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="https://stackoverflow.com/questions/41088022/how-to-get-onuploadprogress-in-axios">https://stackoverflow.com/questions/41088022/how-to-get-onuploadprogress-in-axios</a><div id="articleHeader"><h1>how to get onUploadProgress in axios?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        0
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>4</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I am little bit confused that how to upload progress evt with axios.Actually I am storing huge number files into aws s3.For that how to get uploaded progress I need this function onUploadProgress </p>

<p>Currently my Post request is like this</p>

<pre><code>export function uploadtoCdnAndSaveToDb(data) {
    return dispatch =&gt; {
        dispatch(showUnderLoader(true));
        return axios.post('/posttodb',{data:data},

        ).then((response) =&gt; {
            console.log(response.data)
        })
    }
}</code></pre>
    </div>
    
    <table>
    <tbody><tr>
    <td>
        
    </td>
    <td>
        <div>
    <div>
        asked Dec 11 '16 at 15:52
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</div>
</td>
        </tr>
                
        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-41088162">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        4
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>The Axios repository has a clear example on how to do this: <a href="https://github.com/mzabriskie/axios/blob/master/examples/upload/index.html" target="_blank">https://github.com/mzabriskie/axios/blob/master/examples/upload/index.html</a></p>

<p><strong>Excerpt from the Website</strong></p>

<p>When you make a request with axios, you can pass in request config. Part of that request config is the function to call when upload progresses.</p>

<pre><code>const config = {
    onUploadProgress: progressEvent =&gt; console.log(progressEvent.loaded)
}</code></pre>

<p>When you make the request using axios, you can pass in this config object.</p>

<pre><code>axios.put('/upload/server', data, config)</code></pre>

<p>And this function will be called whenever the upload progress changes.</p>

<p><strong>Just a note on your code</strong></p>

<p>I also noticed that you're not using ES6 to its fullest potential! </p>

<p><em>Object Declaration</em></p>

<p>It's got some nice syntax for stuff like this, for example, you have defined an object like: <code>{ data: data }</code>, but <code>{ data }</code> is sufficient.</p>

<p><em>Brackets on single argument functions</em></p>

<p>If you're creating a "Fat Arrow Function", you don't need brackets around the function arguments if there is only one, i.e</p>

<pre><code>(arg) =&gt; console.log('hello');</code></pre>

<p>is the same as</p>

<pre><code>arg =&gt; console.log('hello');</code></pre>

<p>I see that you've used both in your syntax. My recommendation would be to stick to one. It might be worth using a linter with some linting rules, with the most common being the <a href="https://github.com/airbnb/javascript" target="_blank">AirBnB style guide</a></p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Dec 11 '16 at 16:07
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
	    <div id="comments-41088162">
                <ul>



    <li id="comment-69381333">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Thx chris I will follow yours rules yes I am new to es6.And Your code is printing at the end of total bytes uploaded but i want the changing number of uploading progress
                    – <a href="/users/5947166/nane" title="168 reputation" target="_blank">Nane</a>
                <a href="#comment69381333_41088162" target="_blank">Dec 11 '16 at 16:18</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-69381405">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                How big is the file that you're uploading?
                    – <a href="/users/1870555/christopher" title="20,692 reputation" target="_blank">christopher</a>
                <a href="#comment69381405_41088162" target="_blank">Dec 11 '16 at 16:21</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-69382246">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        
    </li>
    <li id="comment-81651380">
        <div>
            
                <div>
                        <a title="this comment adds something useful to the post" target="_blank">upvote</a>
                </div>
                            <div>
                        <a title="Flag this comment for serious problems or moderator attention" target="_blank">flag</a>
                </div>
        </div>
        <div>
            <div>
                Also how can I cancel the upload process in between?
                    – <a href="/users/4002703/arun-mohan" title="274 reputation" target="_blank">Arun Mohan</a>
                <a href="#comment81651380_41088162" target="_blank">Nov 17 '17 at 11:37</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

                 
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-48412965">
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
<p>Just wanted to add on to previous answer some people having specific configuration may come onto.</p>

<p>This has to do with the 'problem' that it may turn out that <strong>onUploadProgress</strong> may be called only once or twice, usually once with the <strong>progressEvent.loaded === progressEvent.total</strong></p>

<p>So if the callback is being called at least once, there is nothing wrong with axios or measurement, actually the value is correct. You may arrive at this problem if for example you are doing <strong>development</strong> and your backend is responsible for uploading data to for example <strong>aws s3 bucket</strong></p>

<p>What happens there is that in development normally both frontend and backend are on same machine and there is no real time issue with sending packets (sending data to your dev backend is almost instant even for large files)</p>

<p>The trick and where the time is not measured (because this is backends job) is data transmission to s3, then you have to wait for the promise to resolve but you can't track this progresses unless using web sockets or so. </p>

<p>Most of the time this is not the problem in production env, let's say you're on aws, then most of the time is spent sending data from user to your backend and the backend part (which is ec2) sending data to s3 has really good upload speed it's about <strong>0.3s per 10MB uploaded (for Frankfurt area)</strong> so it's probably negligible compared to user -&gt; backend data transmission. </p>

<p>see this link with some <a href="https://blog.takipi.com/amazon-ec2-2015-benchmark-testing-speeds-between-aws-ec2-and-s3-regions/" target="_blank">benchmarks</a>. </p>

<p>Anyways to test that <strong>onUploadProgress</strong> is really being called multiple times as you would expect with large files is simply to switch network connection in network tab of developer tools.</p>

<p><a href="https://i.stack.imgur.com/TrFsJ.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/TrFsJ.png" alt="choose slow 3g for example to test" /></div></a></p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Jan 24 at 0:18
    </div>
    
    
</div>
    </td>
    </tr>
    </tbody></table>
</td>
        </tr>
    
    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    




<div id="post-editor">

    <div> 
        <div>
            <div id="mdhelp">
    <ul id="mdhelp-tabs">
        <li>Links</li>
        <li>Images</li>
        <li>Styling/Headers</li>
        <li>Lists</li>
        <li>Blockquotes</li>
        
        
        <li><a href="/editing-help" target="_blank">advanced help »</a></li>
    </ul>
    
    

    
    
    

    

    

    

    
</div>
            
        </div>
    </div>

    
    

    

    


    
    
    



</div>

                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/reactjs" title="show questions tagged 'reactjs'" target="_blank">reactjs</a> <a href="/questions/tagged/redux" title="show questions tagged 'redux'" target="_blank">redux</a> <a href="/questions/tagged/axios" title="show questions tagged 'axios'" target="_blank">axios</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
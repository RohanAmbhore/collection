<a href="https://stackoverflow.com/questions/23169941/what-does-bin-www-do-in-express-4-x">https://stackoverflow.com/questions/23169941/what-does-bin-www-do-in-express-4-x</a><div id="articleHeader"><h1>What does "./bin/www" do in Express 4.x?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        95
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>36</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>I just started to learn about Express 4.0 in my Node.js app, and I found that it generated <code>./bin/www</code> file, on which only the application server and port settings are written and everything others like middleware and routing is defined in <code>./app.js</code> file.</p>

<p>However, I'm not sure what this <code>./bin/www</code> does. I've used Express 3.x and I have always defined server and port settings as well as routing and middleware on the identical <code>./app.js</code> file, and launched my node app with <code>node app.js</code>. So what's the point of using the <code>./bin/www</code>? Does it only separate the server and port definition from others?</p>

<p>Right now, when I create the package using express-generator, the <code>package.json</code> includes the following definition:</p>

<pre><code>"scripts": {
    "start": "node ./bin/www"
}</code></pre>

<p>However, I wonder whether I should launch my app using <code>node ./bin/www</code>, or <code>npm start</code>. Which command should I run to start my app?</p>

<p>And also, when I deploy my app to heroku, what should I write in the <code>Procfile</code> file? Is <code>web: node app.js</code> enough?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-23169941">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-23249547">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        76
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p>In <strong>Express 3.0</strong>, you normally would use <code>app.configure()</code> (or <code>app.use()</code> ) to set up the required middleware you need. Those middleware you specified are bundled together with Express 3.0.</p>

<p>Example:</p>

<pre><code>var express = require('express');
var routes = require('./routes');
var user = require('./routes/user');
var http = require('http');
var path = require('path');

var app = express();

// all environments
app.set('port', process.env.PORT || 3000);
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'jade');
app.use(express.favicon());
app.use(express.logger('dev'));
app.use(express.compress());
app.use(express.json());
app.use(express.urlencoded());
app.use(express.methodOverride());</code></pre>

<p>In <strong>Express 4.0</strong> however, all middleware have been removed so that they can be maintained and update independently from the core Express (except the static middleware), thus they need to be called separately (what you see in <code>app.js</code>).</p>

<p>The <code>bin/</code> directory serve as a location where you can define your various <strong>startup scripts</strong>, the <code>www</code> is an example on how it should looks like, ultimately you could have startup script like <code>test</code>, <code>stop</code> or <code>restart</code> etc. Having this structure allows you to have different configurations without touching the <code>app.js</code>.</p>

<p>The correct way to start you Express app is </p>

<pre><code>npm start</code></pre>

<p>To deploy an <strong>Express 4.x</strong> app to <strong>Heroku</strong>, add this to your <code>Procfile</code>.  </p>

<pre><code>web: npm start</code></pre>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    <div id="comments-23249547">
                <ul>



    <li id="comment-35640410">
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
                Thanks. With your excellent explanation on the last two paragraphs, I finally got what's the point of using <code>www</code>. I'm not sure why it's named that way though - maybe named after World Wide Web?
                    – <a href="/users/2360798/blaszard" title="9,077 reputation" target="_blank">Blaszard</a>
                <a href="#comment35640410_23249547" target="_blank">Apr 25 '14 at 5:03</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-35978075">
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
                @NicolasS.Xu On the ExpressJS's Github repo <a href="https://github.com/visionmedia/express" target="_blank">github.com/visionmedia/express</a>, scroll down to the Quick start section
                    – <a href="/users/210085/andy" title="3,069 reputation" target="_blank">Andy</a>
                <a href="#comment35978075_23249547" target="_blank">May 5 '14 at 7:51</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-42412468">
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
                @Ved why "bin", though? I associate that with binary executables.
                    – <a href="/users/559515/regularmike" title="837 reputation" target="_blank">regularmike</a>
                <a href="#comment42412468_23249547" target="_blank">Nov 14 '14 at 15:56</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-42547511">
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
                @regularmike I guess, it could also means 'executable' scripts (like in the linux's environment)
                    – <a href="/users/210085/andy" title="3,069 reputation" target="_blank">Andy</a>
                <a href="#comment42547511_23249547" target="_blank">Nov 19 '14 at 6:07</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-42563945">
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
                @Ved yes, seems like a long time ago it evolved to mean anything executable. Common in Python, Perl, and unix/linux in general.
                    – <a href="/users/559515/regularmike" title="837 reputation" target="_blank">regularmike</a>
                <a href="#comment42563945_23249547" target="_blank">Nov 19 '14 at 14:45</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-23249547">

                
            <a href="#" title="expand to show all comments on this post" target="_blank">show <b>9</b> more comments</a>
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-23171936">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        5
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>Node apps like the Express 3.x  use non-standard startup files <code>app.js</code>, but it's the wrong file to run. </p>

<p><code>package.json</code> has</p>

<pre><code>   "scripts": {
     "start": "node ./bin/www"
   }</code></pre>

<p>which states the startup command line. It’s non-trivial because that potentially contains a full command line, and not just a path to the starter file.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Apr 19 '14 at 15:32
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
	    <div id="comments-23171936">
                <ul>



    <li id="comment-35929404">
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
                can you please help me answer this question? Thank you!
                    – <a href="/users/887103/nicolas-s-xu" title="2,347 reputation" target="_blank">Nicolas S.Xu</a>
                <a href="#comment35929404_23171936" target="_blank">May 3 '14 at 7:05</a>
                                                                            </div>
        </div>
    </li>
    <li id="comment-77766375">
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
                Why is it called bin? It doesn't contain binaries . . .
                    – <a href="/users/1236793/kinnard-hockenhull" title="622 reputation" target="_blank">Kinnard Hockenhull</a>
                <a href="#comment77766375_23171936" target="_blank">Jul 30 '17 at 18:10</a>
                                                                            </div>
        </div>
    </li>
                </ul>
				            
	    </div>

        <div id="comments-link-23171936">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-23598188">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        -1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>put this to Procfile <code>web: node ./bin/www</code>
and check if it works with <code>foreman start</code>.
The app should be available on port 5000</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered May 11 '14 at 21:34
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
	    

        <div id="comments-link-23598188">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>

  

<div id="answer-46010584">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </td>
            


<td>
    <div>
<p>if you are using express-generator, just look at your local file, <code>./bin</code>, there is <code>www</code> file inside of the ./bin. So when you run <code>node ./bin/www</code>, node.js will execute the code at <code>www</code> file. Nothing fancy.</p>
    </div>
    <table>
    <tbody><tr>
    <td>
                    </td>
            


    <td>   
       

    <div>
    <div>
        answered Sep 2 '17 at 4:51
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
	    

        <div id="comments-link-46010584">

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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/javascript" title="show questions tagged 'javascript'" target="_blank">javascript</a> <a href="/questions/tagged/node.js" title="show questions tagged 'node.js'" target="_blank">node.js</a> <a href="/questions/tagged/heroku" title="show questions tagged 'heroku'" target="_blank">heroku</a> <a href="/questions/tagged/express" title="show questions tagged 'express'" target="_blank">express</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
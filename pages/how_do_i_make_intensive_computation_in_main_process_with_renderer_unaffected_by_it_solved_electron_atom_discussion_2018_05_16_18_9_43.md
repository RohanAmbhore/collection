<a href="https://discuss.atom.io/t/how-do-i-make-intensive-computation-in-main-process-with-renderer-unaffected-by-it-solved/19499/10">https://discuss.atom.io/t/how-do-i-make-intensive-computation-in-main-process-with-renderer-unaffected-by-it-solved/19499/10</a><div id="articleHeader"><h1>How do I make intensive computation in main process with renderer unaffected by it [SOLVED]</h1></div>
      

<div id="ember850">
          <div id="ember999"><div><div><div><div><a title="Aug 2015" target="_blank">Aug 2015</a></div><div><div><div><div>10 / 14</div><div>Aug 2015</div></div></div></div><div><a title="Feb 2017" target="_blank">Feb 2017</a></div></div></div></div></div>

</div>
      <div>
        <section id="topic">

          <div>
            

            

              <div id="ember1039"><div><div><article id="post_4"><div><div><div><div><p>Thx, guys. Now I see.</p>
<p>I tried this:</p><aside>
  <header>
      <a href="https://gist.github.com/soswow/28547fb866c4236b4ed3" target="_blank">gist.github.com 14</a>
  </header>
  <article>
    <h4><a href="https://gist.github.com/soswow/28547fb866c4236b4ed3" target="_blank">https://gist.github.com/soswow/28547fb866c4236b4ed3</a></h4>
<h5>fib.coffee</h5>
<pre><code>f = (n) -&gt;
    if n is 0
        0
    else if n is 1
        1
    else
        f(n-1) + f(n-2)

module.exports = f</code></pre>

<h5>main.coffee</h5>
<pre><code>ipc = require 'ipc'
fib = require './fib'

ipc.on 'find-fib', (event, num) -&gt;
    console.log '2'
    setTimeout -&gt;
        console.log '5'
        event.sender.send 'fib-result', fib(45)
    , 2000
    console.log '3'</code></pre>

<h5>renderer.coffee</h5>
<pre><code>ipc = require 'ipc'

ipc.on 'fib-result', (result) -&gt;
    console.log '6'
    console.log result

$ -&gt;
    $('#fib-start').click -&gt;
        console.log '1'
        ipc.send 'find-fib', 45</code></pre>
This file has been truncated. <a href="https://gist.github.com/soswow/28547fb866c4236b4ed3" target="_blank">show original</a>

<br /><br /></article>
  
  
</aside>
<p>But this still hangs whole window.</p></div></div></div></div></article></div><div><article id="post_8"><div><div><div><div><p><a href="/u/leedohm" target="_blank">@leedohm</a> if by “schedule the calculation” you mean put it into setTimeout(, 0), then I tried it already too.<br />
Here is updated code with console.log numbers, that appear in the numerical order. Now after clicking a button I have 2 seconds of moving stuff around and then it freezes with colors wheel (on Mac means window is unresponsive)</p>
<aside>
  <header>
      <a href="https://gist.github.com/soswow/28547fb866c4236b4ed3/4c863a421fa3a1d110d1d5c605c61e2ce3f68a5c" target="_blank">gist.github.com 5</a>
  </header>
  <article>
    <h4><a href="https://gist.github.com/soswow/28547fb866c4236b4ed3/4c863a421fa3a1d110d1d5c605c61e2ce3f68a5c" target="_blank">https://gist.github.com/soswow/28547fb866c4236b4ed3/4c863a421fa3a1d110d1d5c605c61e2ce3f68a5c</a></h4>
<h5>fib.coffee</h5>
<pre><code>f = (n) -&gt;
    if n is 0
        0
    else if n is 1
        1
    else
        f(n-1) + f(n-2)

module.exports = f</code></pre>

<h5>main.coffee</h5>
<pre><code>ipc = require 'ipc'
fib = require './fib'

ipc.on 'find-fib', (event, num) -&gt;
    console.log '2'
    setTimeout -&gt;
        console.log '5'
        event.sender.send 'fib-result', fib(45)
    , 2000
    console.log '3'</code></pre>

<h5>renderer.coffee</h5>
<pre><code>ipc = require 'ipc'

ipc.on 'fib-result', (result) -&gt;
    console.log '6'
    console.log result

$ -&gt;
    $('#fib-start').click -&gt;
        console.log '1'
        ipc.send 'find-fib', 45</code></pre>
This file has been truncated. <a href="https://gist.github.com/soswow/28547fb866c4236b4ed3/4c863a421fa3a1d110d1d5c605c61e2ce3f68a5c" target="_blank">show original</a>

<br /><br /></article>
  
  
</aside>
</div></div></div></div></article></div><div><article id="post_9"><div><div><div><div><p>I’ve tried to use native <code>child_process.fork</code> functionality and it works well</p>
<aside>
  <header>
      <a href="https://gist.github.com/soswow/7c0793a79f18bdf3fe41" target="_blank">gist.github.com 41</a>
  </header>
  <article>
    <h4><a href="https://gist.github.com/soswow/7c0793a79f18bdf3fe41" target="_blank">https://gist.github.com/soswow/7c0793a79f18bdf3fe41</a></h4>
<h5>fib.coffee</h5>
<pre><code>f = (n) -&gt;
    if n is 0
        0
    else if n is 1
        1
    else
        f(n-1) + f(n-2)

process.on 'message', (input) -&gt;
    output = f(input)</code></pre>
This file has been truncated. <a href="https://gist.github.com/soswow/7c0793a79f18bdf3fe41" target="_blank">show original</a>
<h5>renderer.coffee</h5>
<pre><code>fork = require('child_process').fork
fibCp = fork(__dirname + '/fib')

fibCp.on 'message', (result) -&gt;
    console.log result
    
$ -&gt;
    $('#fib-start').click -&gt;
        fibCp.send 45</code></pre>


<br /><br /></article>
  
  
</aside>

<p>But I still hope to find out if electron IPC communication and renderer/main processes capable of.</p></div></div></div></div></article></div><div><div>1 year later</div></div><div><div>2 months later</div></div></div></div>

            
          </div>
          

<div id="ember865">  


              

                <div id="ember1041"><div>
    <p>Hey there! <img src="https://discourse-cdn-sjc1.com/business6/images/emoji/twitter/heart_eyes.png?v=5" alt="heart_eyes" title="heart_eyes" /> Looks like you're enjoying the discussion, but you're not signed up for an account.</p>
    <p>When you create an account, we remember exactly what you've read, so you always come right back where you left off. You also get notifications, here and via email, whenever new posts are made. And you can like posts to share the love. <img src="https://discourse-cdn-sjc1.com/business6/images/emoji/twitter/heartbeat.png?v=5" alt="heartbeat" title="heartbeat" /></p>

    <div>
      
      
      <a target="_blank">no thanks</a>
    </div>
  
</div>
</div>


                


                

</div>
        </section>
      </div>

    
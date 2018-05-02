<a href="https://alvinalexander.com/git/git-show-change-username-email-address">https://alvinalexander.com/git/git-show-change-username-email-address</a><div id="articleHeader"><h1>How to show or change your Git username or email address</h1></div>

  
    
      


    
        

            <div>By Alvin Alexander. Last updated: February 27 2018</div>

    
            
            <p>Git user FAQ: How do I show or change my <a href="https://git-scm.com/" target="_blank">Git</a> username (or email address)?</p>

<h2>How to <em>show</em> your Git username</h2>

<p>There are several ways to <em>show</em> your Git username. One way is with the <code>git config</code> command, like this:</p>

<pre>git config user.name
</pre>

<p>which in my case returns:</p>

<pre>Alvin Alexander
</pre>

<p>Another way to show your Git username is with this <code>git config</code> command:</p>

<pre>git config --list
</pre>

<p>which returns this output:</p>

<pre>user.name=Alvin Alexander
user.email=[omitted]
merge.tool=vimdiff
</pre>

<p>Finally, you can also see your Git username in the Git configuration file in your HOME directory on Unix systems, i.e., this file:</p>

<pre>~/.gitconfig
</pre>

<p>My file on my current test system looks like this:</p>

<pre>[user]
        name = Alvin J. Alexander
        email = [omitted]
[merge]
        tool = vimdiff
</pre>

<p>It’s important to note that this is your “global” Git username. You can also have a different username on a per-project basis (but I haven’t used that yet).</p>

<h2>How to <em>change</em> your Git username</h2>

<p>You can <em>change</em> your Git username like this:</p>

<pre>git config --global user.name "Alvin J. Alexander"
</pre>

<p>You can also just edit the Git config file in your HOME directory and change it there:</p>

<pre>vi ~/.gitconfig
</pre>

<p>I just did that on my test system, and it seems to work fine.</p>

<p>Again, it’s important to note that this is your “global” username. You can also have a different username on a per-project basis ... I just looked it up, and you should be able to change your Git username on a per-project basis like this, without the <code>--global</code> option:</p>

<pre>git config user.name "Alvin J. Alexander"
</pre>
<div><div><a href="http://amzn.to/2x6ry02" target="_blank" class="readableLinkWithMediumImage"><img src="/sites/default/files/inline-images/programming-in-scala.jpg" width="145" alt="Programming in Scala: Updated for Scala 2.12" title="Programming in Scala: Updated for Scala 2.12" />
     <br />Programming in Scala
     <br />Updated for Scala 2.12</a>
    </div> <div><a href="http://amzn.com/1495348784" target="_blank" class="readableLinkWithMediumImage"><img src="/sites/default/files/HISMB-160pxWide.jpg" width="145" alt="How I Sold My Business, A Personal Diary" title="How I Sold My Business, A Personal Diary" />
     <br />my book at amazon</a>
    </div></div>

<h2>How to change your Git email address</h2>

<p>While I’m in the Git username neighborhood, I’ll also add that you can <em>view</em> your Git email address with this command:</p>

<pre>git config user.email
</pre>

<p>And you can <em>change</em> your Git email address like this:</p>

<pre>git config --global user.email [your email address here]
</pre>

<p>Finally, you can also see your password by viewing the Git config file in your HOME directory:</p>

<pre>more ~/.gitconfig
</pre>

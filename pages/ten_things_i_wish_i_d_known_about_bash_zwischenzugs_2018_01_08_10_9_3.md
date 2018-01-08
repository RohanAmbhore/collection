<a href="https://zwischenzugs.com/2018/01/06/ten-things-i-wish-id-known-about-bash/">https://zwischenzugs.com/2018/01/06/ten-things-i-wish-id-known-about-bash/</a><div id="articleHeader"><h1>Ten Things I Wish I’d Known About bash</h1></div>

	
	
	
		<h2>Intro</h2>
<p>Recently I wanted to deepen my understanding of bash by researching as much of it as possible. Because I felt bash is an often-used (and under-understood) technology, I ended up writing a <a href="https://leanpub.com/learnbashthehardway" target="_blank">book on it</a>.</p>
<p>You don’t have to look hard on the internet to find plenty of useful one-liners in bash, or scripts. And there are guides to bash that seem somewhat intimidating through either their thoroughness or their focus on esoteric detail.</p>
<p>Here I’ve focussed on the things that either confused me or increased my power and productivity in bash significantly, and tried to communicate them (as in my book) in a way that emphasises getting the understanding right.</p>
<p>Enjoy!</p>
<h2>1)  <code>``</code> vs <code>$()</code></h2>
<p>These two operators do the same thing. Compare these two lines:</p>
<pre>$ echo `ls`
$ echo $(ls)</pre>
<p>Why these two forms existed confused me for a long time.</p>
<p>If you don’t know, both forms substitute the output of the command contained within it into the command.</p>
<p>The principal difference is that nesting is simpler.</p>
<p>Which of these is easier to read (and write)?</p>
<pre>    $ echo `echo \`echo \\\`echo inside\\\`\``
</pre>

<pre>    $ echo $(echo $(echo $(echo inside)))</pre>
<p>If you’re interested in going deeper, see <a href="http://mywiki.wooledge.org/BashFAQ/082" target="_blank">here</a> or <a href="https://stackoverflow.com/questions/4708549/what-is-the-difference-between-command-and-command-in-shell-programming" target="_blank">here</a>.</p>
<h2>2) globbing vs regexps</h2>
<p>Another one that can confuse if never thought about or researched.</p>
<p>While globs and regexps can look similar, they are not the same.</p>
<p>Consider this command:</p>
<pre>$ rename -n 's/(.*)/new$1/' *</pre>
<p>The two asterisks are interpreted in different ways.</p>
<p>The first is ignored by the shell (because it is in quotes), and is interpreted as ‘0 or more characters’ by the rename application. So it’s interpreted as a regular expression.</p>
<p>The second is interpreted by the shell (because it is not in quotes), and gets replaced by a list of all the files in the current working folder. It is interpreted as a glob.</p>
<p>So by looking at <code>man bash</code> can you figure out why these two commands produce different output?</p>
<pre>$ ls *
$ ls .*</pre>
<p>The second looks even more like a regular expression. But it isn’t!</p>
<h2>3) Exit Codes</h2>
<p>Not everyone knows that every time you run a shell command in bash, an ‘exit code’ is returned to bash.</p>
<p>Generally, if a command ‘succeeds’ you get an error code of <code>0</code>. If it doesn’t succeed, you get a non-zero code. <code>1</code> is a ‘general error’, and others can give you more information (eg which signal killed it, for example).</p>
<p>But these rules don’t always hold:</p>
<pre>$ grep not_there /dev/null
$ echo $?</pre>
<p><code>$?</code> is a special bash variable that’s set to the exit code of each command after it runs.</p>
<p>Grep uses exit codes to indicate whether it matched or not. I have to look up every time which way round it goes: does finding a match or not return <code>0</code>?</p>
<p>Grok this and a lot will click into place in what follows.</p>
<h2>4) <code>if</code> statements, <code>[</code> and <code>[[</code></h2>
<p>Here’s another ‘spot the difference’ similar to the backticks one above.</p>
<p>What will this output?</p>
<pre>if grep not_there /dev/null
then
    echo hi
else
    echo lo
fi</pre>
<p>grep’s return code makes code like this work more intuitively as a side effect of its use of exit codes.</p>
<p>Now what will this output?</p>
<p>a) <code>hihi</code><br />
b) <code>lolo</code><br />
c) something else</p>
<pre>if [ $(grep not_there /dev/null) = '' ]
then
    echo -n hi
else
    echo -n lo
fi
if [[ $(grep not_there /dev/null) = '' ]]
then
    echo -n hi
else
    echo -n lo
fi</pre>
<p>The difference between <code>[</code> and <code>[[</code> was another thing I never really understood. <code>[</code> is the original form for tests, and then <code>[[</code> was introduced, which is more flexible and intuitive. In the first <code>if</code> block above, the if statement barfs because the <code>$(grep not_there /dev/null)</code> is evaluated to nothing, resulting in this comparison:</p>
<p><code>[ = '' ]</code></p>
<p>which makes no sense. The double bracket form handles this for you.</p>
<p>This is why you occasionally see comparisons like this in bash scripts:</p>
<p><code>if [ x$(grep not_there /dev/null) = 'x' ]</code></p>
<p>so that if the command returns nothing it still runs.</p>
<h2>5) <code>set</code>s</h2>
<p>Bash has configurable options which can be set on the fly. I use two of these all the time:</p>
<pre>set -e</pre>
<p>exits from a script if any command returned a non-zero exit code (see above).</p>
<p>This outputs the commands that get run as they run:</p>
<pre>set -x</pre>
<p>So a script might start like this:</p>
<pre>#!/bin/bash
set -e
set -x
grep not_there /dev/null
echo $?</pre>
<p>What would that script output?</p>
<h2>6) &lt;()</h2>
<p>This is my favourite. It’s so under-used, perhaps because it can be initially baffling, but I use it all the time.</p>
<p>It’s similar to <code>$()</code> in that the output of the command inside is re-used.</p>
<p>In this case, though, the output is treated as a file. This file can be used as an argument to commands that take files as an argument.</p>
<p>Confused? Here’s an example.</p>
<p>Have you ever done something like this?</p>
<pre>$ grep somestring file1 &gt; /tmp/a
$ grep somestring file2 &gt; /tmp/b
$ diff /tmp/a /tmp/b</pre>
<p>That works, but instead you can write:</p>
<pre>diff &lt;(grep somestring file1) &lt;(grep somestring file2)</pre>
<p>Isn’t that neater?</p>
<h2>7) quoting</h2>
<p>Quoting’s a knotty subject in bash, as it is in many software contexts.</p>
<p>Firstly, variables in quotes:</p>
<pre>A='123'  
echo "$A"
echo '$A'</pre>
<p>Pretty simple – double quotes dereference variables, while single quotes go literal.</p>
<p>So what will this output?</p>
<pre>mkdir -p tmp
cd tmp
touch a
echo "*"
echo '*'</pre>
<p>Surprised? I was.</p>
<h2>8) Top three shortcuts</h2>
<p>There are plenty of shortcuts listed in <code>man bash</code>, and it’s not hard to find comprehensive lists. This list consists of the ones I use most often, in order of how often I use them.</p>
<p>Rather than trying to memorize them all, I recommend picking one, and trying to remember to use it until it becomes unconscious. Then take the next one. I’ll skip over the most obvious ones (eg <code>!!</code> – repeat last command, and <code>~</code> – your home directory).</p>
<p><code><strong>!$</strong></code></p>
<p>I use this dozens of times a day. It repeats the last argument of the last command. If you’re working on a file, and can’t be bothered to re-type it command after command it can save a lot of work:</p>
<pre>grep somestring /long/path/to/some/file/or/other.txt
vi !$</pre>
<p>​​<strong><code>!:1-$</code></strong></p>
<p>This bit of magic takes this further. It takes all the arguments to the previous command and drops them in. So:</p>
<pre>grep isthere /long/path/to/some/file/or/other.txt
egrep !:1-$
fgrep !:1-$</pre>
<p>The <code>!</code> means ‘look at the previous command’, the <code>:</code> is a separator, and the <code>1</code> means ‘take the first word’, the <code>-</code> means ‘until’ and the <code>$</code> means ‘the last word’.</p>
<p><code><strong>:h</strong></code></p>
<p>I use this one a lot too. If you put it after a filename, it will change that filename to remove everything up to the folder. Like this:</p>
<pre>grep isthere /long/path/to/some/file/or/other.txt
cd !$:h</pre>
<p>which can save a lot of work in the course of the day.</p>
<h2>9) startup order</h2>
<p>The order in which bash runs startup scripts can cause a lot of head-scratching. I keep this diagram handy (from <a href="https://blog.flowblok.id.au/2013-02/shell-startup-scripts.html" target="_blank">this</a> great page):</p>
<p><div class="readableLargeImageContainer"><img src="https://zwischenzugs.files.wordpress.com/2018/01/shell-startup-actual.png?w=840" alt="shell-startup-actual" /></div></p>
<p>It shows which scripts bash decides to run from the top, based on decisions made about the context bash is running in (which decides the colour to follow).</p>
<p>So if you are in a local (non-remote), non-login, interactive shell (eg when you run bash itself from the command line), you are on the ‘green’ line, and these are the order of files read:</p>
<pre>/etc/bash.bashrc
~/.bashrc
[bash runs, then terminates]
~/.bash_logout</pre>
<p>This can save you a hell of a lot of time debugging.</p>
<h2>10) getopts (cheapci)</h2>
<p>If you go deep with bash, you might end up writing chunky utilities in it. If you do, then getting to grips with <code>getopts</code> can pay large dividends.</p>
<p>For fun, I once wrote a <a href="https://github.com/ianmiell/cheapci/blob/master/cheapci" target="_blank">script</a> called <code>cheapci</code> which I used to work like a Jenkins job.</p>
<p>The code <a href="https://github.com/ianmiell/cheapci/blob/master/cheapci#L70-L96" target="_blank">here</a> implements the reading of the <a href="https://github.com/ianmiell/cheapci/blob/master/cheapci#L33-L51" target="_blank">two required, and 14 non-required arguments</a>. Better to learn this than to build up a bunch of bespoke code that can get very messy pretty quickly as your utility grows.</p>
<hr />
<p><strong>This is based on some of the contents of my book</strong> <a href="https://leanpub.com/learnbashthehardway" target="_blank">Learn Bash the Hard Way</a>, available at <a href="https://leanpub.com/learnbashthehardway" target="_blank">$5</a>:</p>
<p><a href="https://leanpub.com/learnbashthehardway" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer float"><img src="https://zwischenzugs.files.wordpress.com/2018/01/hero.png?w=188&h=300"   alt="hero" /></div></a></p>
<hr />
<p>I also wrote <a href="https://www.manning.com/books/docker-in-practice-second-edition?a_aid=zwischenzugs&a_bid=550032fc" target="_blank">Docker in Practice </a></p>
<p><a href="https://www.manning.com/books/docker-in-practice-second-edition?a_aid=zwischenzugs&a_bid=550032fc" target="_blank"><strong><em>Get 39% off with the code: 39miell2</em></strong></a></p>
<p><div class="readableLargeImageContainer"><img src="https://zwischenzugs.files.wordpress.com/2017/03/5d342-0v9jkbliyi3uzefqq.jpg?w=319"   /></div></p>
<div>
			<div>
				Advertisements
				
						
				
		
			</div>
		</div>	
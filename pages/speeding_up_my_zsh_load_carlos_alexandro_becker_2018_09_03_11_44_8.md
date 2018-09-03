<a href="https://carlosbecker.com/posts/speeding-up-zsh/">https://carlosbecker.com/posts/speeding-up-zsh/</a><div id="articleHeader"><h1>Speeding up my ZSH load</h1></div>
    
      <p>Carlos Alexandro Becker · <a href="https://www.google.com.br/maps/search/Joinville" target="_blank">Joinville</a>  · 2016-04-10</p>
    
  </header>
  
    <p>This is the story on how I speed up my terminal load time.</p>

<p>Some time ago I shared my
<a href="https://carlosbecker.com/posts/dotfiles-are-meant-to-be-forked/" target="_blank">dotfiles to the world</a>.</p>

<p>I was never really happy with the shell load time, though. Most of it was
spent by antigen loading the plugins I use. By then, my shell was taking
almost 10 seconds to load. To address that issue, I created
<a href="https://carlosbecker.com/posts/go-antibody/" target="_blank">antibody</a>. My shell went from almost
10 seconds to ~2 seconds. It was a huge step, still, I was no happy about it.</p>

<p>Today, I decided to go and figure out why. The first step was to gather data
on why it was so slow:</p>
<div><pre><code>for i in $(seq 1 10); do /usr/bin/time zsh -i -c exit; done
  1.11 real         0.48 user         0.57 sys
  0.82 real         0.47 user         0.42 sys
  0.83 real         0.47 user         0.43 sys
  0.86 real         0.48 user         0.44 sys
  0.82 real         0.47 user         0.42 sys
  1.21 real         0.48 user         0.42 sys
  0.80 real         0.46 user         0.41 sys
  0.82 real         0.47 user         0.42 sys
  0.82 real         0.47 user         0.42 sys
  1.40 real         0.48 user         0.42 sys</code></pre></div>
<p>As we can see, it took ~1 second for each shell load. It might feel fast, but
for a shell to open it is not.</p>

<p>So, to find out where the slowness was, I ran <code>zsh -i -c -x exit</code>. I spend
some time looking at all that debug info and found that much of that time was
being spent by <code>rbenv init</code> command. So, I lazy loaded it:</p>
<div><pre><code>-# shellcheck disable=SC2039
-if rbenv &&gt;/dev/null; then
-  eval "$(rbenv init -)"
-fi
+
+rbenv() {
+  eval "$(command rbenv init -)"
+  rbenv "$@"
+}
</code></pre></div>
<p>I know, I changed the way the program behave by doing that, but I think it’s
worth it.</p>

<p>I did the same with <code>antibody</code> and <code>pyenv</code> and remove some unneeded <code>if</code>
statements (e.g. <code>[ ! -d "$GOPATH" ] && mkdir -p "$GOPATH/bin"</code>) and
simplified some <code>PATH</code> changes (e.g. replacing to <code>export</code>s with one).</p>

<p>Then, I measured it again:</p>
<div><pre><code>for i in $(seq 1 10); do /usr/bin/time zsh -i -c exit; done
  0.73 real         0.43 user         0.35 sys
  0.72 real         0.42 user         0.34 sys
  1.10 real         0.43 user         0.35 sys
  0.72 real         0.42 user         0.35 sys
  0.75 real         0.44 user         0.36 sys
  0.73 real         0.43 user         0.35 sys
  0.74 real         0.43 user         0.35 sys
  0.73 real         0.43 user         0.34 sys
  0.73 real         0.43 user         0.35 sys
  0.73 real         0.43 user         0.34 sys</code></pre></div>
<p>That improved a little. But I wanted more.</p>

<p>So, I look for <code>if</code> statements that check if a program exists by calling it,
for example: <code>if gls &&gt;/dev/null; then</code>.</p>

<p>It turn out I had a lot of them. I fixed them by doing stuff like:</p>
<div><pre><code>-if gls &&gt;/dev/null; then
+if which gls &gt;/dev/null 2&gt;&1; then
</code></pre></div>
<p>And, measuring again:</p>
<div><pre><code>for i in $(seq 1 10); do /usr/bin/time zsh -i -c exit; done
  0.43 real         0.22 user         0.25 sys
  0.42 real         0.22 user         0.24 sys
  0.40 real         0.21 user         0.23 sys
  0.40 real         0.21 user         0.23 sys
  0.40 real         0.21 user         0.23 sys
  0.39 real         0.21 user         0.22 sys
  0.40 real         0.21 user         0.24 sys
  0.41 real         0.21 user         0.24 sys
  0.41 real         0.21 user         0.24 sys
  0.40 real         0.21 user         0.23 sys</code></pre></div>
<p><strong>Wow!</strong> The time went from ~0.7s to ~0.4s!</p>

<p>Still, I wanted more!</p>

<p>I looked for more stuff like this, and end up finding one more call to <code>rbenv</code>
to check if it exists and also some duplicated zsh completion code.</p>

<p>Fixed those issues and measuring again gave me this numbers:</p>
<div><pre><code>for i in $(seq 1 10); do /usr/bin/time zsh -i -c exit; done
  0.78 real         0.14 user         0.14 sys
  0.26 real         0.14 user         0.13 sys
  0.28 real         0.15 user         0.14 sys
  0.26 real         0.14 user         0.13 sys
  0.27 real         0.14 user         0.13 sys
  0.25 real         0.13 user         0.12 sys
  0.27 real         0.14 user         0.13 sys
  0.27 real         0.14 user         0.13 sys
  0.27 real         0.14 user         0.13 sys
  0.26 real         0.14 user         0.13 sys</code></pre></div>
<p>I was almost happy here, if it wasn’t for this <code>0.78</code>. I debugged a little more
and found out that <code>compinit</code> was taking more time on every new shell execution.</p>

<p>I found that it was because it was checking <code>~/.zcompdump</code> file every time.</p>

<p>I found a <a href="https://gist.github.com/ctechols/ca1035271ad134841284" target="_blank">hack on a gist</a>
and changed it a little to work on OSX, here is what I got:</p>
<div><pre><code>-autoload -U compinit && compinit
+autoload -Uz compinit
+if [ $(date +'%j') != $(stat -f '%Sm' -t '%j' ~/.zcompdump) ]; then
+  compinit
+else
+  compinit -C
+fi
</code></pre></div>
<p>And, measuring again:</p>
<div><pre><code>for i in $(seq 1 10); do /usr/bin/time zsh -i -c exit; done
  0.28 real         0.13 user         0.14 sys
  0.26 real         0.12 user         0.14 sys
  0.25 real         0.12 user         0.14 sys
  0.23 real         0.11 user         0.12 sys
  0.25 real         0.12 user         0.13 sys
  0.23 real         0.11 user         0.13 sys
  0.23 real         0.11 user         0.12 sys
  0.24 real         0.11 user         0.13 sys
  0.26 real         0.13 user         0.14 sys
  0.26 real         0.12 user         0.14 sys</code></pre></div>
<p>Way faster, huh?</p>

<p>Right now, the only ways I found to make it even faster is disabling completion
and/or using another prompt, without syntax highlight and history substring
search. I don’t want to do that right now, so, I’ll be happy with what I got.</p>

<p>Oh, I also graphed all these things (with 100 executions in a fresh shell):</p>



<p>For reference,
<a href="https://docs.google.com/spreadsheets/d/150esx1EvZSqSH6JbRiPjK5pPHYUMsD7yiwSvDCzoS0U" target="_blank">here</a>
is the table of mins, maxs, medians and modes for all of them too.</p>

<p>Also, here are the pull requests that did those changes:</p>


  
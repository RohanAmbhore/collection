<a href="https://www.nczonline.net/blog/2009/01/13/speed-up-your-javascript-part-1/">https://www.nczonline.net/blog/2009/01/13/speed-up-your-javascript-part-1/</a><div id="articleHeader"><h1>Speed up your JavaScript, Part 1</h1></div>
                            <p>Posted at January 13, 2009 by Nicholas C. Zakas</p>
                            <p>Tags:
                            
                            <a href="/blog/tag/arrays" target="_blank">Arrays</a>
                            
                            <a href="/blog/tag/javascript" target="_blank">JavaScript</a>
                            
                            <a href="/blog/tag/long-running-script" target="_blank">Long-Running Script</a>
                            
                            <a href="/blog/tag/performance" target="_blank">Performance</a>
                            
                        </p>
                        
                        
                    
                    <div>

<p>In my <a href="http://www.nczonline.net/blog/2009/01/05/what-determines-that-a-script-is-long-running/" title="What determines that a script is long running?" target="_blank">last post</a>, I talked about the conditions under which the dreaded long-running script dialog is displayed in browsers. Browsers will stop executing script either when they’ve executed too many statements (Internet Explorer) or when the JavaScript engine has been running for a specific amount of time (others). The problem, of course, isn’t the way that the browser is detecting long-running scripts, it’s that the script is taking too long to execute.</p>

<p>There are four main reasons why a script can take too long to execute:</p>

<ol>
<li>Too much happening in a loop.</li>
<li>Too much happening in a function.</li>
<li>Too much recursion.</li>
<li>Too much DOM interaction.</li>
</ol>

<p>In this post, I’m going to focus on the first issue: too much happening in a loop. Loop iterations happen synchronously, so the amount of time it takes to fully execute the loop is directly related to the number of iterations. There are, therefore, two situations that cause loops to run too long and lock up the browser. The first is that the loop body is doing too much for each iteration and the second is that the loop is running too many times. These can cause the browser to lock up and display the long-running script warning.</p>

<p>The secret to unraveling this problem is to evaluate the loop to answer two questions:</p>

<ol>
<li>Does the loop have to execute synchronously?</li>
<li>Does the order in which the loop’s data is processed matter?</li>
</ol>

<p>If the answer to both of these questions is “no,” then you have some options for splitting up the work done in the loop. The key is to examine the code closely to answer these questions. A typical loop looks like this:</p>
<div><pre><code>for(var i=0; i &lt; items.length; i++){
    process(items[i]);
}
</code></pre></div>
<p>This doesn’t look too bad though may take very long depending on the amount of time necessary to run the <code>process()</code> function. If there’s no code immediately after the loop that depends on the results of the loop executing, then the answer to the first question is “no.” You can clearly see that each iteration through the loop isn’t dependent on the previous iteration because it’s just dealing with one value at a time, so the answer to the second question is “no.” That means the loop can be split in a way that can free up the browser and avoid long-running script warnings.</p>

<p>In <a href="http://www.amazon.com/gp/product/047022780X?ie=UTF8&tag=nczonline-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=047022780X" target="_blank">Professional JavaScript, Second Edition</a>, I introduce the following function as a way to deal with loops that may take a significant amount of time to execute:</p>
<div><pre><code>function chunk(array, process, context){
    setTimeout(function(){
        var item = array.shift();
        process.call(context, item);

        if (array.length &gt; 0){
            setTimeout(arguments.callee, 100);
        }
    }, 100);
}
</code></pre></div>
<p>The <code>chunk()</code> function is designed to process an array in small chunks (hence the name), and accepts three arguments: a “to do” list of items, the function to process each item, and an optional context variable for setting the value of <code>this</code> within the <code>process()</code> function. A timer is used to delay the processing of each item (100ms in this case, but feel free to alter for your specific use). Each time through, the first item in the array is removed and passed to the <code>process()</code> function. If there’s still items left to process, another timer is used to repeat the process. The loop described earlier can be rewritten to use this function:</p>
<div><pre><code>chunk(items, process);
</code></pre></div>
<p>Note that the array is used as a queue and so is changed each time through the loop. If you want to maintain the array’s original state, there are two options. First, you can use the <code>concat()</code> method to clone the array before passing it into the function:</p>
<div><pre><code>chunk(items.concat(), process);
</code></pre></div>
<p>The second option is to change the <code>chunk()</code> function to do this automatically:</p>
<div><pre><code>function chunk(array, process, context){
    var items = array.concat();   //clone the array
    setTimeout(function(){
        var item = items.shift();
        process.call(context, item);

        if (items.length &gt; 0){
            setTimeout(arguments.callee, 100);
        }
    }, 100);
}
</code></pre></div>
<p>Note that this approach is safer than just saving an index and moving through the exist array, since the contents of the array that was passed in may change before the next timer is run.</p>

<p>The <code>chunk()</code> method presented here is just a starting point for how to deal with loop performance. You can certainly change it to provide more features, for instance, a callback method to execute when all items have been processed. Regardless of the changes you may or may not need to make to the function, it is a general pattern that can help optimize array processing to avoid long-running script warnings.</p>

<h2>Translations</h2>



<p>Disclaimer: Any viewpoints and opinions expressed in this article are those of Nicholas C. Zakas and do not, in any way, reflect those of my employer, my colleagues, <a href="http://www.wrox.com/" target="_blank">Wrox Publishing</a>, <a href="http://www.oreilly.com/" target="_blank">O'Reilly Publishing</a>, or anyone else. I speak only for myself, not for them.</p>







             
        
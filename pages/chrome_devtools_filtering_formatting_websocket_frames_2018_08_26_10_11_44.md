<a href="https://jasonlaster.github.io/devtools/js/2016/03/05/getting-websocket-frames.html">https://jasonlaster.github.io/devtools/js/2016/03/05/getting-websocket-frames.html</a><div id="articleHeader"><h1>Chrome DevTools - Filtering / Formatting Websocket frames</h1></div>

    <p>As of today, Chrome DevTools does not have great support for seeing web socket frames. Chrome DevTools uses it’s standard <code>DataTable</code> component, which supports columns with sorting. It does not support filtering, formatting objects, or adding additional columns.</p>

<p>These limitations are ironically probably best shown by inspecting the websocket connection from DevTools and the browser. DevTools is a rich app that sends hundreds of messages back and forth with a standard <code>{id, method, params, result}</code> format. There’s also a standard that DevTool requests are matched with responses with the same ID.</p>

<p>It’s easy to imagine a better UI for visualizing the request method and params, with the following response result and timing information.</p>

<p>In the meantime, we can do a little hacking and build a half decent substitute.</p>

<h4 id="original">Original</h4>

<p><div class="readableLargeImageContainer"><img src="http://f.cl.ly/items/070s0S1b1p3g2b3r0q0L/Screen%20Shot%202016-03-05%20at%2012.13.26%20PM.png"  /></div></p>

<h4 id="new-view">New View</h4>

<p><div class="readableLargeImageContainer"><img src="http://f.cl.ly/items/1b0N1f1l3d0j2G1u3O41/Screen%20Shot%202016-03-05%20at%2012.13.19%20PM.png"  /></div></p>

<p>What you need to do is to open a second DevTools (DT) to inspect the original. You can do this when DT is undocked and you hit <cmd> shift I. At this point, you can create a new snippet in the sources tab and add the code below. Or if you're feeling lazy drop the whole thing into the console.</cmd></p>

<div><div><pre><code>// Get the Network Tabs
var networkTabs  = WebInspector.panels.network._networkItemView.tabViews();

// Get the Websocket View from the network tabs
var WebsocketView = networkTabs[1];

// get the frames from the websocket table
var frames = WebsocketView._dataGrid._flatNodesList();

var frameData = frames.map(frame =&gt; JSON.parse(frame._dataText))

// log each frame

// frameData.forEach(frame =&gt; {
//     console.log(frame.id, frame.method, frame.params, frame.result);
// })

// show the table
var framesData = frameData.map(frame =&gt;  {
    var {id, method, params, result} = frame;
    var params = JSON.stringify(params);
    var result = JSON.stringify(result);
    return {id, method,params , result}
});

console.table(framesData);
</code></pre></div>

    <p>05 Mar 2016</p>

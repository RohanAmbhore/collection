<a href="https://www.reddit.com/r/electronjs/comments/7ny380/electronpreferences_a_simple_consistent_interface/">https://www.reddit.com/r/electronjs/comments/7ny380/electronpreferences_a_simple_consistent_interface/</a><div id="articleHeader"><h1>A simple, consistent interface for managing user preferences within an Electron application.：electronjs</h1></div><p>I created the following module in an attempt to get rid of some of the boilerplate that's often associated with managing user preferences within an Electron-based desktop application:</p>

<p><a href="https://github.com/tkambler/electron-preferences" target="_blank">electron-preferences</a></p>

<p>It provides you with an interface for saving / reading preference values, obviously. But it also provides a built-in visual interface that you can present to users. You don't have to muck around with CSS, HTML, etc... to modify it. The layout of the preferences window is defined via the API. If you click-through to the repo, you'll see a screenshot of the interface that users see.</p>

<p>The library includes built-in support for a number of field types, including:</p>

<ul>

<li>Dropdown</li>
<li>Folder selection</li>
<li>Generic message display</li>
</ul>

<p>If you're familiar with React, adding support for new field types is easy. PR's are welcome.</p>

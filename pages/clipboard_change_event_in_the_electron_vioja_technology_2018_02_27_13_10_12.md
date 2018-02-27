<a href="http://www.vioja.com/clipboard-change-event-in-the-electron/">http://www.vioja.com/clipboard-change-event-in-the-electron/</a><div id="articleHeader"><h1>Clipboard change event in the electron</h1></div>
          <p><a href="http://www.vioja.com/clipboard-change-event-in-the-electron/" target="_blank">2015-07-17</a> <em>Posted by  on <a href="http://www.vioja.com/category/javascript/" title="Javascript" target="_blank">Javascript</a></em></p>
        </header>
        <div>
          <div><div>Advertisement</div>




          <div>
            <div>
<p>  I would like to write a clipboard manager that monitors the clipboard systems.  Well, I found: https://github.com/atom/electron/blob/master/docs/api/clipboard.md, but could not find any events for the clipboard. </p><p>  Do clipboard events exist in electronics?  I mean that <code>void selectionChanged()</code> and <code>void dataChanged()</code> or that the owner of GTK has changed </p><p>  Currently, I retrieve the contents of the clipboard and look manually if the content has changed every 20ms, which should not be the preferred way.  It works but I should not really use a loop of polls ... </p>            </div>
			<h3>The answer</h3>
			<div><p>  Unfortunately Electron does not yet provide such an event. </p><p>  Currently, the Electron team is waiting for the Chromium project to implement this feature first.  But according to Chromium issue tracker, they only implemented support for ChromeOS and X11 and do not try to implement it for Windows / MacOS. </p><p>  You can find more information in the feature request at: https://github.com/electron/electron/issues/2280 </p></div>
          
          
        
      
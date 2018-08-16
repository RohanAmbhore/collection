<a href="https://stackoverflow.com/questions/44712495/what-are-the-differences-between-page-action-and-browser-action">https://stackoverflow.com/questions/44712495/what-are-the-differences-between-page-action-and-browser-action</a><div id="articleHeader"><h1><a href="https://developer.chrome.com/extensions/browserAction" target="_blank">Browser action</a> buttons</h1></div>

<p>Browser action buttons should be used when your button is valid for use most of the time, either on most pages, or not related to/dependent upon the page that is being displayed in the active tab. <strong>By default, browser action buttons are enabled on all tabs/URLs.</strong> You have to call <code>browserAction.disable()</code> to disable the button in each tab where you want it disabled (or generally disabled on all tabs). The browser action button does not change enabled/disabled state when the tab displays a different URL.</p>

<p>Chrome's <a href="https://developer.chrome.com/extensions/browserAction" target="_blank">browser action button</a> page says (some emphasis mine):</p>

<blockquote>
  <p>Use browser actions to put icons in the main Google Chrome toolbar, <strong>to the right of the address bar</strong>. In addition to its <a href="https://developer.chrome.com/extensions/browserAction#icon" target="_blank">icon</a>, a browser action can also have a <a href="https://developer.chrome.com/extensions/browserAction#tooltip" target="_blank">tooltip</a>, a <a href="https://developer.chrome.com/extensions/browserAction#badge" target="_blank">badge</a>, and a <a href="https://developer.chrome.com/extensions/browserAction#popups" target="_blank">popup</a>. </p>
</blockquote>



<blockquote>
  <ul>
  <li><strong>Do</strong> use browser actions for features that make sense on most pages.</li>
  <li><strong>Don't</strong> use browser actions for features that make sense for only a few pages. <strong>Use <a href="https://developer.chrome.com/extensions/pageAction" target="_blank">page actions</a> instead.</strong></li>
  <li><strong>Do</strong> use big, colorful icons that make the most of the 16x16-dip space. Browser action icons should seem a little bigger and heavier than page action icons.</li>
  <li><strong>Don't</strong> attempt to mimic Google Chrome's monochrome menu icon. That doesn't work well with themes, and anyway, extensions should stand out a little.</li>
  <li><strong>Do</strong> use alpha transparency to add soft edges to your icon. Because many people use themes, your icon should look nice on a variety of background colors.</li>
  <li><strong>Don't</strong> constantly animate your icon. That's just annoying. </li>
  </ul>
</blockquote>

<p>Browser actions have the following APIs:</p>

<ul>
<li>Types

</li>
<li>Methods

<ul>
<li><a href="https://developer.chrome.com/extensions/browserAction#method-disable" target="_blank">disable</a> − <code>browserAction.disable(integer tabId)</code></li>
<li><a href="https://developer.chrome.com/extensions/browserAction#method-enable" target="_blank">enable</a> − <code>browserAction.enable(integer tabId)</code></li>
<li><a href="https://developer.chrome.com/extensions/browserAction#method-getBadgeBackgroundColor" target="_blank">getBadgeBackgroundColor</a> − <code>browserAction.getBadgeBackgroundColor(object details, function callback)</code></li>
<li><a href="https://developer.chrome.com/extensions/browserAction#method-getBadgeText" target="_blank">getBadgeText</a> − <code>browserAction.getBadgeText(object details, function callback)</code></li>
<li><a href="https://developer.chrome.com/extensions/browserAction#method-getPopup" target="_blank">getPopup</a><sup>1</sup> − <code>browserAction.getPopup(object details, function callback)</code></li>
<li><a href="https://developer.chrome.com/extensions/browserAction#method-getTitle" target="_blank">getTitle</a><sup>1</sup> − <code>browserAction.getTitle(object details, function callback)</code></li>
<li><a href="https://developer.chrome.com/extensions/browserAction#method-setBadgeBackgroundColor" target="_blank">setBadgeBackgroundColor</a> − <code>browserAction.setBadgeBackgroundColor(object details)</code></li>
<li><a href="https://developer.chrome.com/extensions/browserAction#method-setBadgeText" target="_blank">setBadgeText</a> − <code>browserAction.setBadgeText(object details)</code></li>
<li><a href="https://developer.chrome.com/extensions/browserAction#method-setIcon" target="_blank">setIcon</a><sup>1</sup> − <code>browserAction.setIcon(object details, function callback)</code></li>
<li><a href="https://developer.chrome.com/extensions/browserAction#method-setPopup" target="_blank">setPopup</a><sup>1</sup> − <code>browserAction.setPopup(object details)</code></li>
<li><a href="https://developer.chrome.com/extensions/browserAction#method-setTitle" target="_blank">setTitle</a><sup>1</sup> − <code>browserAction.setTitle(object details)</code></li>
</ul></li>
<li>Events

<ul>
<li><a href="https://developer.chrome.com/extensions/browserAction#event-onClicked" target="_blank">onClicked</a><sup>1</sup></li>
</ul></li>
</ul>

<h1><a href="https://developer.chrome.com/extensions/pageAction" target="_blank">Page action</a> buttons</h1>

<p>Page action buttons should be used when the ability to use of your extension's button is dependent on the URL being shown in the active tab and when it is <em>usually</em> not available for use (i.e. only usable under some conditions, or on some URLs). <strong>By default, page action buttons are disabled/grayed out ("hidden") on all URLs.</strong> You have to call <code>pageAction.show()</code> to enable the button for each URL/tab you want it enabled. The page action button automatically becomes disabled/hidden if the tab displays a different URL.</p>

<p>Chrome's <a href="https://developer.chrome.com/extensions/pageAction" target="_blank">page action button</a> page says (some emphasis mine):</p>

<blockquote>
  <p>Use the <code>chrome.pageAction</code> API to put icons in the main Google Chrome toolbar, <strong>to the right of the address bar</strong>. Page actions represent actions that can be taken on the current page, but that aren't applicable to all pages. Page actions appear grayed out when inactive.</p>
</blockquote>



<blockquote>
  <p>Like browser actions, page actions can have an icon, a tooltip, and popup; they can't have badges, however. In addition, page actions can be grayed out. You can find information about icons, tooltips, and popups by reading about the browser action UI.</p>
  
  <p>You make a page action appear and be grayed out using the <a href="https://developer.chrome.com/extensions/pageAction#method-show" target="_blank">pageAction.show</a> and <a href="https://developer.chrome.com/extensions/pageAction#method-hide" target="_blank">pageAction.hide</a> methods, respectively. By default, a page action appears grayed out. When you show it, you specify the tab in which the icon should appear. The icon remains visible until the tab is closed or starts displaying a different URL (because the user clicks a link, for example).  </p>
</blockquote>



<blockquote>
  <ul>
  <li><strong>Do use</strong> page actions for features that make sense for only a few pages.</li>
  <li><strong>Don't</strong> use page actions for features that make sense for most pages. Use <a href="https://developer.chrome.com/extensions/browserAction" target="_blank">browser actions</a> instead.</li>
  <li><strong>Don't</strong> constantly animate your icon. That's just annoying. </li>
  </ul>
</blockquote>

<p>Page actions have the following APIs:</p>

<ul>
<li>Types

<ul>
<li><a href="https://developer.chrome.com/extensions/pageAction#type-ImageDataType" target="_blank">ImageDataType</a><sup>1</sup></li>
</ul></li>
<li>Methods

<ul>
<li><a href="https://developer.chrome.com/extensions/pageAction#method-getPopup" target="_blank">getPopup</a><sup>1</sup> − <code>pageAction.getPopup(object details, function callback)</code></li>
<li><a href="https://developer.chrome.com/extensions/pageAction#method-getTitle" target="_blank">getTitle</a><sup>1</sup> − <code>pageAction.getTitle(object details, function callback)</code></li>
<li><a href="https://developer.chrome.com/extensions/pageAction#method-hide" target="_blank">hide</a> − <code>chrome.pageAction.hide(integer tabId)</code></li>
<li><a href="https://developer.chrome.com/extensions/pageAction#method-setIcon" target="_blank">setIcon</a><sup>1</sup> − <code>pageAction.setIcon(object details, function callback)</code></li>
<li><a href="https://developer.chrome.com/extensions/pageAction#method-setPopup" target="_blank">setPopup</a><sup>1</sup> − <code>pageAction.setPopup(object details)</code></li>
<li><a href="https://developer.chrome.com/extensions/pageAction#method-setTitle" target="_blank">setTitle</a><sup>1</sup> − <code>pageAction.setTitle(object details)</code></li>
<li><a href="https://developer.chrome.com/extensions/pageAction#method-show" target="_blank">show</a> − <code>pageAction.show(integer tabId)</code></li>
</ul></li>
<li>Events

<ul>
<li><a href="https://developer.chrome.com/extensions/pageAction#event-onClicked" target="_blank">onClicked</a><sup>1</sup></li>
</ul></li>
</ul>

<hr />

<p><sup>1. This API is available for both browser actions and page actions. It does basically the same thing on both.</sup></p>
    
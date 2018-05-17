<a href="https://developer.apple.com/library/content/documentation/General/Conceptual/ExtensibilityPG/ExtensionOverview.html#//apple_ref/doc/uid/TP40014214-CH2-SW2">https://developer.apple.com/library/content/documentation/General/Conceptual/ExtensibilityPG/ExtensionOverview.html#//apple_ref/doc/uid/TP40014214-CH2-SW2</a><div id="articleHeader"><h1>Understand How an App Extension Works</h1></div>


  
  	<section>
  		<p>
  An app extension is not an app. It implements a specific, well scoped task that adheres to the policies defined by a particular extension point.
</p>

		</section> 


  <section>
  
  <h3>An App Extension’s Life Cycle</h3>
  <p>
  Because an app extension is not an app, its life cycle and environment are different. In most cases, an extension launches when a user chooses it from an app’s UI or from a presented activity view controller. An app that a user employs to choose an app extension is called a <em>host app</em>. A host app defines the context provided to the extension and kicks off the extension life cycle when it sends a request in response to a user action. An extension typically terminates soon after it completes the request it received from the host app.
</p><p>
  For example, imagine that a user selects some text in an OS X host app, activates the Share button, and chooses an app extension from the sharing list to help them post the text to a social sharing website. The host app responds to the user’s choice by issuing to the extension a request that contains the selected text. A generalized version of this situation is pictured in step 1 of Figure 2-1.
</p><figure>
  
  <strong>Figure 2-1</strong>The basic life cycle of an app extension
  <div class="readableLargeImageContainer"><img src="Art/app_extensions_lifecycle_2x.png"   alt="image: ../Art/app_extensions_lifecycle_2x.png" /></div>
</figure><p>
  In step 2 of Figure 2-1, the system instantiates the app extension identified in the host app’s request and sets up a communication channel between them. The extension displays its view within the context of the host app and then uses the items it received in the host app’s request to perform its task (in this example, the extension receives the selected text).
</p><p>
  In step 3 of Figure 2-1, the user performs or cancels the task in the app extension and dismisses it. In response to this action, the extension completes the host app’s request by immediately performing the user’s task or, if necessary, initiating a background process to perform it. The host app tears down the extension’s view and the user returns to their previous context within the host app. When the extension’s task is finished, whether immediately or later, a result may be returned to the host app. 
</p><p>
  Shortly after the app extension performs its task (or starts a background session to perform it), the system terminates the extension, as shown in step 4.
</p>
  
</section>
<section>
  
  <h3>How an App Extension Communicates</h3>
  <p>
  An app extension communicates primarily with its host app, and does so in terms reminiscent of transaction processing: There is a request from the host and a response from the extension. Figure 2-2 shows a simplified view of the relationship between a running extension, the host app that launched it, and the containing app.
</p><figure>
  
  <strong>Figure 2-2</strong>An app extension communicates directly only with the host app
  <div class="readableLargeImageContainer"><img src="Art/simple_communication_2x.png"   alt="image: ../Art/simple_communication.png" /></div>
</figure><p>
  There is no direct communication between an app extension and its containing app; typically, the containing app isn’t even running while a contained extension is running. An app extension’s containing app and the host app don’t communicate at all.
</p><p>
  In a typical request/response transaction, the system opens an app extension on behalf of a host app, conveying data in an <em>extension context</em> provided by the host. The extension displays a user interface, performs some work, and, if appropriate for the extension’s purpose, returns data to the host.
</p><p>
  The dotted line in Figure 2-2 represents the limited interaction available between an app extension and its containing app. A Today widget (and no other app extension type) can ask the system to open its containing app by calling the <code><a href="https://developer.apple.com/documentation/foundation/nsextensioncontext/1416791-openurl" target="_blank">openURL:completionHandler:</a></code> method of the <code><a href="https://developer.apple.com/documentation/foundation/nsextensioncontext" target="_blank">NSExtensionContext</a></code> class.   As indicated by the Read/Write arrows in Figure 2-3, any app extension and its containing app can access shared data in a privately defined shared container. The full vocabulary of communication between an extension, its host app, and its containing app is shown in simple form in Figure 2-3.
</p><figure>
  
  <strong>Figure 2-3</strong>An app extension can communicate indirectly with its containing app
  <div class="readableLargeImageContainer"><img src="Art/detailed_communication_2x.png"   alt="image: ../Art/detailed_communication.png" /></div>
</figure><div>
  
  <aside>
    
    	<p>Behind the scenes, the system uses interprocess communication to ensure that the host app and an app extension can work together to enable a cohesive experience. In your code, you never have to think about this underlying communication mechanism, because you use the higher-level APIs provided by the extension point and the system.
    	</p>
    
  </aside>
</div>
  
</section>
<section>
  
  <h3>Some APIs Are Unavailable to App Extensions</h3>
  <p>
  Because of its focused role in the system, an app extension is ineligible to participate in certain activities. An app extension cannot:
</p><ul>
  <li><p>
  Access a <code><a href="https://developer.apple.com/documentation/uikit/uiapplication/1622975-shared" target="_blank">sharedApplication</a></code> object, and so cannot use any of the methods on that object
</p>
</li><li><p>
  Use any API marked in header files with the <code>NS_EXTENSION_UNAVAILABLE</code> macro, or similar unavailability macro, or any API in an unavailable framework
</p>
<p>
  For example, in iOS 8.0, the HealthKit framework and EventKit UI framework are unavailable to app extensions.
</p>
</li><li><p>
  Access the camera or microphone on an iOS device (an iMessage app, unlike other app extensions, does have access to these resources, as long as it correctly configures the <a href="../../Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW24" target="_blank">NSCameraUsageDescription</a> and <a href="../../Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW25" target="_blank">NSMicrophoneUsageDescription</a> <code>Info.plist</code> keys)
</p>
</li><li><p>
  Perform long-running background tasks
</p>
<p>
  The specifics of this limitation vary by platform, as described in the extension point chapters in this document.
</p>
<p>
  (An app extension can initiate uploads or downloads using an <code><a href="https://developer.apple.com/documentation/foundation/nsurlsession" target="_blank">NSURLSession</a></code> object, with results of those operations reported to the containing app.)
</p>
</li><li><p>
  Receive data using AirDrop
</p>
<p>
  (An app extension can <em>send</em> data using AirDrop in the same way an app does: by employing the <code><a href="https://developer.apple.com/documentation/uikit/uiactivityviewcontroller" target="_blank">UIActivityViewController</a></code> class.)
</p>
</li>
</ul>
  
</section>

  	
 	

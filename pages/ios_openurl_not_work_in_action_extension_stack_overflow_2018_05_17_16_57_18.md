<a href="https://stackoverflow.com/questions/24297273/openurl-not-work-in-action-extension">https://stackoverflow.com/questions/24297273/openurl-not-work-in-action-extension</a><div id="articleHeader"><h1>openURL not work in Action Extension</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        39
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>36</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I add following code:</p>

<pre><code>- (IBAction)done {
    // Return any edited content to the host app.
    // This template doesn't do anything, so we just echo the passed in items.

    NSURL *url = [NSURL URLWithString:@"lister://today"];
    [self.extensionContext openURL:url completionHandler:^(BOOL success) {
        NSLog(@"fun=%s after completion. success=%d", __func__, success);
    }];
    [self.extensionContext completeRequestReturningItems:self.extensionContext.inputItems completionHandler:nil];

}</code></pre>

<p>after I create the Action Extension target. But it can not work.</p>

<p>My purpose is that: when user view a photo in Photos.app (the iOS's default Photos.app or called gallery), and he click the share button to launch our extension view.
We can transfer the image from Photos.app to my own app and deal or upload the image in my app.</p>

<p>I also try "CFBundleDocumentTypes" but it also can not work.</p>

<p>Any help will be appreciated.</p>
    </div>
    
    
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-24709883">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        19
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>This is by design. We don't want Custom Actions to become app launchers.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jul 12 '14 at 5:12
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-24297677">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>My guess is that this is intentionally not possible. The <code>openURL:completionHandler:</code> block says that it may not be supported in all extension types, and the action extension docs explicitly say:</p>

<blockquote>
  <p>If you want to help users share content on a social website or give users updates on information they care about, the Action extension point is not the right choice.</p>
</blockquote>

<p>I think a share extension might be more appropriate, but the docs for both types suggest that the experience should be embedded in the host app, not taking the users to your app, so it might not allow that for that either. So, perhaps follow the share extension docs and just upload your image from within the extension UI as it suggests?</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jun 19 '14 at 2:04
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-24305645">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>It seems to be a bug, because docs say:</p>

<blockquote>
  <p><strong>Opening the Containing App</strong></p>
  
  <p>In some cases, it can make sense for an extension to request its
  containing app to open. For example, the Calendar widget in OS X opens
  Calendar when users click an event. To ensure that your containing app
  opens in a way that makes sense in the context of the user’s current
  task, you need to define a custom URL scheme that both the app and its
  extensions can use.</p>
  
  <p>An extension doesn’t directly tell its containing app to open;
  instead, it uses the openURL:completionHandler: method of
  NSExtensionContext to tell the system to open its containing app. When
  an extension uses this method to open a URL, the system validates the
  request before fulfilling it.</p>
</blockquote>

<p>I reported it today: <a href="http://openradar.appspot.com/17376354" target="_blank">http://openradar.appspot.com/17376354</a> You should dupe it, if you have some free time.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-24614589">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        6
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>A possible workaround:
Create and add a small UIWebView to your view and run it's method loadRequest with the url scheme you set above.
This is a workaround and I'm not sure what Apple will say about it.
Good luck!</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jul 7 '14 at 15:45
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-25098195">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Not every app extension type supports "extensionContext openURL". </p>

<p>I tested on iOS 8 beta 4 and found Today extension supports it, but keyboard extension does not.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 2 '14 at 18:34
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-25189466">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Only the Today Extension seems to work.<br />
It's not 100% documented, but an apple employee specifically says that Keyboard extensions do not support openURL:completionHandler.<br />
The documentation says:</p>

<blockquote>
  <p>Each extension point determines whether to support this method, or under which conditions to support this method.</p>
</blockquote>

<p>So in practice, Share, Action, Keyboard, and Document provider do <strong>not</strong> work for anyone (beta 5) and only Today Extension supports it.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 7 '14 at 18:22
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-26396222">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>NSExtensionContext only support openURL function in today extension ,this is described in apple's documents about NSExtensionContext.The original words is "Each extension point determines whether to support this method, or under which conditions to support this method. In iOS 8.0, only the Today extension point supports this method."</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 16 '14 at 4:26
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-28037297">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        40
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>This is what I used to do:</p>

<pre><code>UIWebView * webView = [[UIWebView alloc] initWithFrame:CGRectMake(0, 0, 0, 0)];
NSString *urlString = @"https://itunes.apple.com/us/app/watuu/id304697459";
NSString * content = [NSString stringWithFormat : @"&lt;head&gt;&lt;meta http-equiv='refresh' content='0; URL=%@'&gt;&lt;/head&gt;", urlString];
[webView loadHTMLString:content baseURL:nil];
[self.view addSubview:webView];
[webView performSelector:@selector(removeFromSuperview) withObject:nil afterDelay:2.0];</code></pre>

<p>Please note that in this case I am instantiating this call from the UIInputViewController.</p>

<p>This method should also work using the URL scheme from the containing app</p>

<p><strong>UPDATE 04/17/2015: This does not work with iOS 8.3. We are looking for a solution and we will update the answer soon</strong></p>

<p><strong>UPDATE 06/01/2015: We found a solution that works in iOS 8.3</strong></p>

<pre><code>var responder = self as UIResponder?

while (responder != nil){
    if responder!.respondsToSelector(Selector("openURL:")) == true{
        responder!.callSelector(Selector("openURL:"), object: url, delay: 0)
    }
    responder = responder!.nextResponder()
}</code></pre>

<p>This will find a suitable responder to send the openURL to.</p>

<p>You need to add this extension that replaces the performSelector for swift and helps in the construction of the mechanism:</p>

<pre><code>extension NSObject {
    func callSelector(selector: Selector, object: AnyObject?, delay: NSTimeInterval) {
        let delay = delay * Double(NSEC_PER_SEC)
        let time = dispatch_time(DISPATCH_TIME_NOW, Int64(delay))

        dispatch_after(time, dispatch_get_main_queue(), {
            NSThread.detachNewThreadSelector(selector, toTarget:self, withObject: object)
        })
    }
}</code></pre>

<p><strong>UPDATE 06/15/2015: Objective-C</strong></p>

<p>Someone asked for the code in Objective-C so here it is. I am not going to run it as I don't have the time right now but it should be quite straightforward:</p>

<pre><code>UIResponder *responder = self;
while(responder){
    if ([responder respondsToSelector: @selector(OpenURL:)]){
        [responder performSelector: @selector(OpenURL:) withObject: [NSURL URLWithString:@"www.google.com" ]];
    }
    responder = [responder nextResponder];
}</code></pre>

<p>As mentioned, I have not run this Objective-C code, it is just a conversion from the Swift code. Please let me know if you encounter any issues and the solution and I will update it. Nowadays, I am just using swift and unfortunately my brain is deprecating Objective-C</p>

<p><strong>UPDATE 05/02/2016: Deprecated functions</strong></p>

<p>As pointed by @KyleKIM the Selector functions have been replaced in Swift 2.2 by #selector. Also, there is a function that is deprecated and will probably get removed in Swift 3.0 so I am doing some research to find an alternative.</p>

<p><strong>UPDATE 09/16/2016: XCode 8, Swift 3.0 and iOS10</strong>
The following code is still working on the mentioned versions. You will get some warnings:</p>

<pre><code>let url = NSURL(string:urlString)
let context = NSExtensionContext()
context.open(url! as URL, completionHandler: nil)

var responder = self as UIResponder?

while (responder != nil){
    if responder?.responds(to: Selector("openURL:")) == true{
        responder?.perform(Selector("openURL:"), with: url)
    }
    responder = responder!.next
}</code></pre>

<p><strong>UPDATE 6/15/2017: XCode 8.3.3</strong></p>

<pre><code>let url = NSURL(string: urlString)
let selectorOpenURL = sel_registerName("openURL:")
let context = NSExtensionContext()
context.open(url! as URL, completionHandler: nil)

var responder = self as UIResponder?

while (responder != nil){
    if responder?.responds(to: selectorOpenURL) == true{
        responder?.perform(selectorOpenURL, with: url)
    }
    responder = responder!.next
}</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-28185815">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>As apple document
" A Today widget (and no other app extension type) can ask the system to open its containing app by calling the openURL:completionHandler: method of the NSExtensionContext class."</p>

<p>For other Extension, I used this solution </p>

<pre><code>UIWebView * webView = [[UIWebView alloc] initWithFrame:CGRectMake(0, 0, 0, 0)];
NSString *urlString = @"ownApp://"; // Use other application url schema.

NSString * content = [NSString stringWithFormat : @"&lt;head&gt;&lt;meta http-equiv='refresh' content='0; URL=%@'&gt;&lt;/head&gt;", urlString];
[webView loadHTMLString:content baseURL:nil];
[self.view addSubview:webView];
[webView performSelector:@selector(removeFromSuperview) withObject:nil afterDelay:1.0];</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 28 '15 at 6:12
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-29554597">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        23
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Try this code.</p>

<pre><code>    UIResponder* responder = self;
    while ((responder = [responder nextResponder]) != nil)
    {
        NSLog(@"responder = %@", responder);
        if([responder respondsToSelector:@selector(openURL:)] == YES)
        {
            [responder performSelector:@selector(openURL:) withObject:[NSURL URLWithString:urlString]];
        }
    }</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Apr 10 '15 at 6:16
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-30980030">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        14
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Apple accepted the following solution, which is the "same" code that a host app would use. It works on all iOS 8 versions to date (tested on iOS 8.0 - iOS 8.3).</p>

<pre><code>NSURL *destinationURL = [NSURL URLWithString:@"myapp://"];

// Get "UIApplication" class name through ASCII Character codes.
NSString *className = [[NSString alloc] initWithData:[NSData dataWithBytes:(unsigned char []){0x55, 0x49, 0x41, 0x70, 0x70, 0x6C, 0x69, 0x63, 0x61, 0x74, 0x69, 0x6F, 0x6E} length:13] encoding:NSASCIIStringEncoding];
if (NSClassFromString(className)) {
    id object = [NSClassFromString(className) performSelector:@selector(sharedApplication)];
    [object performSelector:@selector(openURL:) withObject:destinationURL];
}</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jun 22 '15 at 12:29
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-33366267">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>An updated version of Julio Bailon's answer with modern Swift syntax:</p>

<pre><code>let url = NSURL(string: "scheme://")!
var responder: UIResponder? = self
while let r = responder {
    if r.respondsToSelector("openURL:") {
        r.performSelector("openURL:", withObject: url)
        break
    }
    responder = r.nextResponder()
}</code></pre>

<p>There is no need for an extension for NSObject now.  </p>

<p>Note: you must wait for the view to be attached to the view hierarchy before calling this code otherwise the responder chain can't be used.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 27 '15 at 11:03
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-34426815">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>Working solution (tested on iOS 9.2)</strong> for Keyboard Extension. This category adds special method for access to hidden <code>sharedApplication</code> object and then call <code>openURL:</code> on it.
(Of course then you have to use <code>openURL:</code> method with your app scheme.)</p>

<pre><code>extension UIInputViewController {

    func openURL(url: NSURL) -&gt; Bool {
        do {
            let application = try self.sharedApplication()
            return application.performSelector("openURL:", withObject: url) != nil
        }
        catch {
            return false
        }
    }

    func sharedApplication() throws -&gt; UIApplication {
        var responder: UIResponder? = self
        while responder != nil {
            if let application = responder as? UIApplication {
                return application
            }

            responder = responder?.nextResponder()
        }

        throw NSError(domain: "UIInputViewController+sharedApplication.swift", code: 1, userInfo: nil)
    }

}</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 23 '15 at 0:34
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-40675306">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        10
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Worked solution in Swift 3.0:</p>

<pre><code>// For skip compile error. 
func openURL(_ url: URL) {
    return
}

func openContainerApp() {
    var responder: UIResponder? = self as UIResponder
    let selector = #selector(openURL(_:))
    while responder != nil {
        if responder!.responds(to: selector) && responder != self {
            responder!.perform(selector, with: URL(string: "containerapp://")!)
            return
        }
        responder = responder?.next
    }
}</code></pre>

<p><strong>Explanation:</strong></p>

<p>In extension, api is limited by compiler to not let you use openURl(:URL) like in container app. However the api is still here.</p>

<p>And we can't perform method in our class until we declare it, what we really want is let UIApplication to perform this method.</p>

<p>Recall to responder chain, we can use</p>

<pre><code>    var responder: UIResponder? = self as UIResponder
    responder = responder?.next</code></pre>

<p>to loop to UIApplication object.</p>

<p>And my apps with this method pass the review process, so don't worry to use it.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-42879948">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Solution for the latest iOS SDK 10.2. All previous solutions use deprecated api. This solution is based on searching UIApplication UIResponder of the hosting application (This app which create execution context for our extension). The solution can only be provided in Objective-C because there is a 3 arguments method to invoke and this is impossible to do with <code>performSelector:</code> methods. To invoke this not deprecated method <code>openURL:options:completionHandler:</code> we need to use NSInvocation instance which is unavailable in Swift. The provided solution can be invoked from Objective-C and Swift (any version). I need to say that I don't know yet if provided solution will be valid for apple review process.</p>

<p><code>UIViewController+OpenURL.h</code></p>

<pre><code>#import &lt;UIKit/UIKit.h&gt;
@interface UIViewController (OpenURL)
- (void)openURL:(nonnull NSURL *)url;
@end</code></pre>

<p><code>UIViewController+OpenURL.m</code></p>

<pre><code>#import "UIViewController+OpenURL.h"

@implementation UIViewController (OpenURL)

- (void)openURL:(nonnull NSURL *)url {

    SEL selector = NSSelectorFromString(@"openURL:options:completionHandler:");

    UIResponder* responder = self;
    while ((responder = [responder nextResponder]) != nil) {
        NSLog(@"responder = %@", responder);
        if([responder respondsToSelector:selector] == true) {
            NSMethodSignature *methodSignature = [responder methodSignatureForSelector:selector];
            NSInvocation *invocation = [NSInvocation invocationWithMethodSignature:methodSignature];

            // Arguments
            NSDictionary&lt;NSString *, id&gt; *options = [NSDictionary dictionary];
            void (^completion)(BOOL success) = ^void(BOOL success) {
                NSLog(@"Completions block: %i", success);
            };

            [invocation setTarget: responder];
            [invocation setSelector: selector];
            [invocation setArgument: &url atIndex: 2];
            [invocation setArgument: &options atIndex:3];
            [invocation setArgument: &completion atIndex: 4];
            [invocation invoke];
            break;
        }
    }
}

@end</code></pre>

<p>From Swift 3 You can execute this only if Your view controller is in view hierarchy. This is the code how I'm using it:</p>

<pre><code>override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)

        let context = self.extensionContext!
        let userAuthenticated = self.isUserAuthenticated()

        if !userAuthenticated {
            let alert = UIAlertController(title: "Error", message: "User not logged in", preferredStyle: .alert)
            let cancel = UIAlertAction(title: "Cancel", style: .cancel) { _ in
                context.completeRequest(returningItems: nil, completionHandler: nil)
            }
            let login = UIAlertAction(title: "Log In", style: .default, handler: { _ in
                //self.openContainingAppForAuthorization()
                let url = URL(string: "fashionapp://login")!
                self.open(url)
                context.completeRequest(returningItems: nil, completionHandler: nil)
            })

            alert.addAction(cancel)
            alert.addAction(login)
            present(alert, animated: true, completion: nil)
        }
    }</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Mar 18 '17 at 21:13
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-44694703">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Following code works on <strong>Xcode 8.3.3, iOS10, Swift3</strong> and <strong>Xcode 9, iOS11, Swift4</strong> without any compiler warnings:</p>

<pre><code>func openUrl(url: URL?) {
    let selector = sel_registerName("openURL:")
    var responder = self as UIResponder?
    while let r = responder, !r.responds(to: selector) {
        responder = r.next
    }
    _ = responder?.perform(selector, with: url)
}

func canOpenUrl(url: URL?) -&gt; Bool {
    let selector = sel_registerName("canOpenURL:")
    var responder = self as UIResponder?
    while let r = responder, !r.responds(to: selector) {
        responder = r.next
    }
    return (responder!.perform(selector, with: url) != nil)
}</code></pre>

<p>Make sure your app supports Universal Links, otherwise it will open the link in browser. More info here: <a href="https://developer.apple.com/library/content/documentation/General/Conceptual/AppSearch/UniversalLinks.html" target="_blank">https://developer.apple.com/library/content/documentation/General/Conceptual/AppSearch/UniversalLinks.html</a></p>
    </div>
    
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    




<div id="post-editor">

    <div> 
        <div>
            <div id="mdhelp">
    <ul id="mdhelp-tabs">
        <li>Links</li>
        <li>Images</li>
        <li>Styling/Headers</li>
        <li>Lists</li>
        <li>Blockquotes</li>
        
        
        <li><a href="/editing-help" target="_blank">advanced help »</a></li>
    </ul>
    
    

    
    
    

    

    

    

    
</div>
            
        </div>
    </div>

    
    

    

    


    
    
    



</div>

                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/ios" title="show questions tagged 'ios'" target="_blank">ios</a> <a href="/questions/tagged/ios8" title="show questions tagged 'ios8'" target="_blank">ios8</a> <a href="/questions/tagged/ios-app-extension" title="show questions tagged 'ios-app-extension'" target="_blank">ios-app-extension</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
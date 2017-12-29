<a href="https://github.com/diffsky/chromedotfiles/issues/2">https://github.com/diffsky/chromedotfiles/issues/2</a><div id="articleHeader"><h1>              Unchecked runtime.lastError while running tabs.insertCSS: Failed to load file:            #2    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/lancejpollard" target="_blank">lancejpollard</a>  opened this Issue
        <relative-time>on Mar 22, 2015</relative-time>
        · 1 comment
    </div>
  



    <h2>Comments</h2>
    
      

      

        
          

  
  

    





      
  

    



    
      
        
          
            
                <p>Adding console.log to <code>background.js</code>, when going to create this issue it says:</p>
<pre><code>// i'm logging here
tab: https://github.com/diffsky/chromedotfiles/issues/new
match: Object {protocol: "https:", host: "github.com", hostname: "github.com", port: undefined, pathname: "/diffsky/chromedotfiles/issues/new"…}

// chrome throws these errors
extensions::sendRequest:82 Unchecked runtime.lastError while running tabs.insertCSS: Failed to load file: "chromedotfiles/github.com.css". 
    at chrome-extension://hocrtbokejcqajcfomloelehcgookikb/background.js:23:17
extensions::sendRequest:82 Unchecked runtime.lastError while running tabs.executeScript: Failed to load file: "chromedotfiles/github.com.js". 
    at chrome-extension://hocrtbokejcqajcfomloelehcgookikb/background.js:26:17
</code></pre>
<p>I tried placing a file in 2 different places to see if it'd work, but doesn't seem to:</p>
<pre><code>~/.chromedotfiles/github.com.js
~/chromedotfiles/github.com.js
</code></pre>
<p>Is there any other setup I have to do? Do you have to do anything with certificates like with dotjs?</p>
<p>Does it depend on a specific version of chrome or operating system? I haven't updated my mac in a while, still using 10.9.2, not sure if that's a problem.</p>
<p>Would love to get this working :)</p>
            
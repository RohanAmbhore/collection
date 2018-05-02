<a href="https://github.com/gaearon/react-hot-loader/issues/489">https://github.com/gaearon/react-hot-loader/issues/489</a><div id="articleHeader"><h1>              What is the difference using webpack-hot-middleware and using this react-hot-loader            #489    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/okaprinarjaya" target="_blank">okaprinarjaya</a>  opened this Issue
        <relative-time>on Feb 23, 2017</relative-time>
        · 13 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-209660572">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          
<p>I very curious, What is the difference using webpack-hot-middleware and using this react-hot-loader. Whether react-hot-loader can be combined with express ?</p>
<p>Thank You :)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  


          

          


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-282578912">

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/calesce" target="_blank">calesce</a>
  

    </strong>

    commented

    <a href="#issuecomment-282578912" target="_blank"><relative-time>on Feb 27, 2017</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Hi, React Hot Loader can be used alongside <code>webpack-hot-middleware</code> and Express. You'll also need to include <a href="https://github.com/webpack/webpack-dev-middleware" target="_blank">webpack-dev-middleware</a>. I actually have an example using both together <a href="https://github.com/calesce/react-hot-loader-examples" target="_blank">here</a>.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-311653303">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/calesce" target="_blank">@calesce</a> that's not a difference :)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-317240618">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>+1<br />
confused as well</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-320994199">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I understand that <code>react-hot-loader</code> makes a per-component hot reload rather than a full-page refresh and that it pairs nicely with <code>webpack-dev-server</code>. But if you're using <code>webpack-hot-middleware</code> with your own Express server, why would you like to also use <code>react-hot-loader</code> if <code>webpack-hot-middleware</code> already implements per-component hot reload?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-321225733">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>+1<br />
<a href="https://github.com/calesce" target="_blank">@calesce</a> I'd love to understand why, like <a href="https://github.com/antonioredondo" target="_blank">@AntonioRedondo</a> mentioned, you'd also use <code>react-hot-loader</code> if <code>webpack-hot-middleware</code> already implements per-component hot reloads?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-321239915">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/antonioredondo" target="_blank">@AntonioRedondo</a> after researching a bit on the matter, it looks to me that <code>react-hot-loader</code> adds some extra features on the mix if you are using <code>React</code> and or <code>Redux</code> <a href="http://gaearon.github.io/react-hot-loader/getstarted/#step-3-of-3-adding-react-hot-loader-to-preserve-component-state" target="_blank">such as keep the component state upon hot reloading</a> and it also facilitates the use of some other specific <a href="https://github.com/gaearon/redux-devtools" target="_blank">Redux dev tools</a> whereas <a href="https://github.com/glenjamin/webpack-hot-middleware" target="_blank">webpack-hot-middleware</a> takes care only of hot reloading a module. I have to say though that the whole thing feels rather confusing.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-328024496">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>So you don't need to use webpack-hot-middleware to use react-hot-loader?</p>
<p>If I were to use just react-hot-loader, what would the setup be like? Do I need to use the HMR plugin still?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-339097653">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>+1 to <a href="https://github.com/always-sunny" target="_blank">@Always-Sunny</a>'s question. Should we be using  react-hot-loader in combination with webpack-hot-middleware or instead of?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-339175946">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/dpoint01" target="_blank">@dpoint01</a> I believe it is in combination but I currently working on setting something up myself.</p>
<blockquote>
<p>This module is only concerned with the mechanisms to connect a browser client to a webpack server & receive updates. It will subscribe to changes from the server and execute those changes using webpack's HMR API. Actually making your application capable of using hot reloading to make seamless changes is out of scope, and usually handled by another library.</p>
</blockquote>
<blockquote>
<p>If you're using React then some common options are react-transform-hmr and react-hot-loader.</p>
</blockquote>
<p>from <a href="https://github.com/glenjamin/webpack-hot-middleware" target="_blank">webpack-hot-middleware</a> readme</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-346865169">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>In my project, I use webpack-hot-middleware with react-hot-loader on my own express server, when I totally remove react-hot-loader, I found it actually behave the same result.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-346899394">

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/theKashey" target="_blank">theKashey</a>
  

    </strong>

    commented

    <a href="#issuecomment-346899394" target="_blank"><relative-time>on Nov 25, 2017</relative-time></a>


      
  •


  

  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Webpack-hot-middleware stands for Server-Side. It detects changes and informs client side about it.<br />
It actually is the <strong>Hot Module Replacemen</strong>t.</p>
<p>In the same time react-hot-loader... do nothing. It’s goal is to stop and prevent updates. It’s purely front end and starts working after webpack did its job.</p>
<p>So, correct answer is simple - this is 2 different things, but they supposed to work together.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-361430792">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I can't get react-hot-loader work together with webpack-hot-middleware.<br />
Anyone has successful example to share?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-370048061">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Why does this have to be so damn complicated? And why isn't this written on one and the same doc page?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  
















        


        <div>
              
<div>
  

    
      



      <div>
        
          <div>
  


  
  <div>

    

    

        <p>
    
    
        Attach files by dragging & dropping,
        selecting them, or pasting
        from the clipboard.
    
    
    
    
    
    
    
    
    
  </p>


    
  </div>

  

  


  


          
      




        
      

    
    
  
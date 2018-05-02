<a href="https://github.com/chentsulin/electron-react-boilerplate/issues/712">https://github.com/chentsulin/electron-react-boilerplate/issues/712</a><div id="articleHeader"><h1>              Issue loading images in production package            #712    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/ivtpz" target="_blank">ivtpz</a>  opened this Issue
        <relative-time>on Feb 4, 2017</relative-time>
        · 16 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      

  
    
      

          
<p>I realise this issue has been referenced before, but I have tried the suggested solutions from <a href="https://github.com/chentsulin/electron-react-boilerplate/issues/250#issuecomment-227494838" target="_blank">#250</a> and am still unable to load images when I package my app.</p>
<p>I am accessing images in development two ways - both in CSS as follows:</p>
<p><code>background: url('../assets/image_to_load.png')</code></p>
<p>and in my .js files like this:</p>
<pre><code>var Logo = require('../assets/48x48.png');
&lt;img src={Logo} /&gt;
</code></pre>
<p>Both load fine on the dev server, but not in the production package. I tried <code>alert(Logo)</code> in dev and in production, and got<br />
<code>data:image/png;base64,iVBORw0KGgoA....</code> from the dev environment and<br />
<code>data:image/png;base64,bW9kdWxlLmV4....</code> in the prod package.</p>
<p>I have also tried using <code>import Logo from '../assets/48x48.png'</code>, and the production app errors out when it fails to find the images.</p>
<p>I am currently using <code>url-loader</code> in the webpack config for images. Any advice on how to proceed would be much appreciated. Thanks.</p>
      
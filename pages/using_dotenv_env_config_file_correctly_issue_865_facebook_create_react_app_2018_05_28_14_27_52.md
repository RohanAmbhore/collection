<a href="https://github.com/facebook/create-react-app/issues/865">https://github.com/facebook/create-react-app/issues/865</a><div id="articleHeader"><h1>              Using dotenv .env config file correctly            #865    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/georgelovegrove" target="_blank">georgelovegrove</a>  opened this Issue
        <relative-time>on Oct 7, 2016</relative-time>
        · 19 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-181468513">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <h3>Description</h3>
<p>How the .env file and imports should be setup for the project correctly as currently the build is breaking.</p>
<h3>Expected behavior</h3>
<ul>
<li>add .env file with config in root</li>
<li>npm install --save dotenv</li>
<li>import dotenv using require('dotenv').config(); or ES6 syntax in index.js file</li>
<li>consume using process.env.CONFIG_NAME across application</li>
</ul>
<h3>Actual behavior</h3>
<p><a href="https://cloud.githubusercontent.com/assets/6073296/19161705/bec80220-8bec-11e6-93a0-cf8f87141bb4.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/6073296/19161705/bec80220-8bec-11e6-93a0-cf8f87141bb4.png"  alt="screen shot 2016-10-06 at 17 45 24" /></div></a></p>
<p>Using the expected behaviour approach I get the above error. I've also tried both installing dotenv and not installing it (as ejecting the repository shows dotenv is already a dependency).</p>
<h3>Environment</h3>
<p>react-scripts@0.6.1<br />
node - v6.6.0<br />
npm - 3.10.8</p>
<p>Using a Chrome (53.0.2785.143) on a Mac.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-252094043">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm trying to get this working too, I don't think you are supposed to actually install dotenv. For some reason env variables are not being imported from my .env file though.... so I am having a similar problem.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  


  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-252139398">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Thanks but I have already. I have added the file. I'm using dotenv on other<br />
projects and it works fine. In this case, I'm on the latest version of<br />
create react app. Made a .env file at the root. Process.env is an empty<br />
object in the app. Really weird for sure....<br />
On Thu, Oct 6, 2016 at 22:29 Shriyans <a href="mailto:notifications@github.com" target="_blank">notifications@github.com</a> wrote:</p>
<blockquote>
<p><a href="https://github.com/georgelovegrove" target="_blank">@georgelovegrove</a> <a href="https://github.com/georgelovegrove" target="_blank">https://github.com/georgelovegrove</a> <a href="https://github.com/zackify" target="_blank">@zackify</a><br />
<a href="https://github.com/zackify" target="_blank">https://github.com/zackify</a><br />
Please have a look at this,for adding env variables.</p>
<p><a href="https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-custom-environment-variables" target="_blank">https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-custom-environment-variables</a></p>
<p>—<br />
You are receiving this because you were mentioned.<br />
Reply to this email directly, view it on GitHub<br />
<a href="https://github.com/facebook/create-react-app/issues/865#issuecomment-252139117" target="_blank">facebookincubator#865 (comment)</a>,<br />
or mute the thread<br />
<a href="https://github.com/notifications/unsubscribe-auth/AAbacLSpvpJBJEzMc7c2C42haipHxJqcks5qxa6XgaJpZM4KQK0" target="_blank">https://github.com/notifications/unsubscribe-auth/AAbacLSpvpJBJEzMc7c2C42haipHxJqcks5qxa6XgaJpZM4KQK0</a>_<br />
.</p>
</blockquote>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-252148907">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/shrynx" target="_blank">shrynx</a>
  

    </strong>

    commented

    <a href="#issuecomment-252148907" target="_blank"><relative-time>on Oct 7, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/georgelovegrove" target="_blank">@georgelovegrove</a> <a href="https://github.com/zackify" target="_blank">@zackify</a> Is your os sierra too ? i am unable to reproduce it.<br />
Also to add one more thing , in your .env file , what are the names of env variables. You have to append <strong>REACT_APP_</strong> to them , to make it work.<br />
eg:<br />
This works.</p>
<pre><code>REACT_APP_SECRET=mySecret  👍
</code></pre>
<p>and this doesn't</p>
<pre><code>SECRET=anotherSecret 👎 
</code></pre>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-252188651">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm on OS Sierra but <a href="https://github.com/shrynx" target="_blank">@shrynx</a> made me look closer at the information I read before. I missed the appending 'REACT_APP_' to the start of the key. That's a bit of a verbose pain to add that to every key, could that not be shortened or removed entirely in the scripts?</p>
<p>Closing now, thanks for help.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-252199527">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>It is intentionally verbose. Otherwise there is a risk of accidentally exposing a private key on the machine that happens to have the same name.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-252201441">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/gaearon" target="_blank">@gaearon</a> fair point, may be worth a one liner in the docs. p.s thanks for redux! aha</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-252207773">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/georgelovegrove" target="_blank">@georgelovegrove</a> PRs are welcome to the docs <g-emoji>😉</g-emoji></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-252208897">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/gaearon" target="_blank">@gaearon</a> Won't have the finesse to explain why that you will #juniordevforlife</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-252215588">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>But you know the right place to put it. We can polish the message later, PR is a start.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-252233720">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Haha! Knew there had to be something simple. Agree, it's a little confusing<br />
especially if you are used to setting up env files yourself.<br />
On Fri, Oct 7, 2016 at 06:53 Dan Abramov <a href="mailto:notifications@github.com" target="_blank">notifications@github.com</a> wrote:</p>
<blockquote>
<p>But you know the right place to put it. We can polish the message later,<br />
PR is a start.</p>
<p>—<br />
You are receiving this because you were mentioned.<br />
Reply to this email directly, view it on GitHub<br />
<a href="https://github.com/facebook/create-react-app/issues/865#issuecomment-252215588" target="_blank">facebookincubator#865 (comment)</a>,<br />
or mute the thread<br />
<a href="https://github.com/notifications/unsubscribe-auth/AAbacMKHz45JK1x8FrRQDY0vVXV8U64Dks5qxiSrgaJpZM4KQK0" target="_blank">https://github.com/notifications/unsubscribe-auth/AAbacMKHz45JK1x8FrRQDY0vVXV8U64Dks5qxiSrgaJpZM4KQK0</a>_<br />
.</p>
</blockquote>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-369413550">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>It is intentionally verbose. Otherwise there is a risk of accidentally exposing a private key on the machine that happens to have the same name.</p>
</blockquote>
<p>Can someone help me understand the security <em>risks</em> involved in having a sensitive value attached to <code>process.env</code>? It is my understanding that <code>process.env</code> won't be available during runtime.</p>
<p>If I understand that correctly, why is the code that exposes these variables so defensive? I guess what I'm looking for is a security use-case that would inform a design decision like this.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-375925569">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/wpcarro" target="_blank">@wpcarro</a> Say you were working on some other project and set an environment variable of <code>SECRET=my-secret-token</code>. If you then build your project that uses <code>process.env.SECRET</code> without specifying a new value, the app will then have <code>my-secret-token</code> baked into the source. This is now viewable by anyone with access to the built files (eg everyone if it's a public web app).</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-376202760">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/cdriehuys" target="_blank">@cdriehuys</a> thanks for the response. I still have a few questions regarding the security risks.</p>
<p>In the example you provided, isn't the only security offense including <code>process.env.SECRET</code> in the source code?</p>
<p>To me, it seems like including <code>process.env.SECRET</code> in any built source is a risk that CRA cannot <em>really</em> protect against. Is anything stopping someone from building <code>process.env.REACT_APP_SECRET</code>? Aren't the risks the same?</p>
<p>It's possible that I'm misunderstanding the problem, but if I'm not, this feels like CRA is creating the illusion of enhanced security without actually conferring the benefits. Would love to understand more though!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-376228275">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>My understanding of it is that its more likely for someone to accidentally set the environment variable <code>SECRET</code> for a different project and accidentally include it than it is for them to set a variable prefixed with <code>REACT_APP</code>. The prefix provides an indication when setting it that "hey, this will probably get bundled in a publicly available build. I should be careful with the information I pass in."</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-376290689">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/cdriehuys" target="_blank">@cdriehuys</a> At this point I think we're on the same page then in terms of our understanding. I definitely agree that it's <em>more</em> likely for someone to set <code>SECRET</code> and include <code>process.env.SECRET</code> than it is to set <code>REACT_APP_SECRET</code> and include <code>process.env.REACT_APP_SECRET</code>...</p>
<p>I feel like the only <em>security</em> concern here is anytime a developer includes <code>process.env.SOME_SECRET</code> in the build. I don't think that prepending <code>REACT_APP_</code> decreases these risks. I think it has the potential to introduce a false sense of security while introducing verboseness all for a small win.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-383809360">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/wpcarro" target="_blank">@wpcarro</a> the important bit is that the secret thing that gets included in the build is from <em>some other unrelated project</em>, that happens to be on the machine the build happens on. Like, that other project might set something like <code>API_URL=internal:secretpassword@api.clients.com</code>.</p>
<p>Meanwhile, the React project coincidentally also allows an API_URL to be set, coz sometimes you want <code>corp.net/testapi/</code> instead of <code>corp.net/api/</code>, but this build it notices there's an API_URL env var and rolls it into the build, and the whole world gets to see your client's password is <code>secretpassword</code>. It was okay for the React dev to allow the API url into the built code – it was never supposed to include a password. The problem was just that an environment var from some other project used the same name. That's the risk the explicit prefix is avoiding.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



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

  

  


  


          
      




        
      

    
    
  
<a href="https://github.com/facebook/create-react-app/issues/2070">https://github.com/facebook/create-react-app/issues/2070</a><div id="articleHeader"><h1>              How to hide unwanted warning            #2070    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/EasonWang01" target="_blank">EasonWang01</a>  opened this Issue
        <relative-time>on May 3, 2017</relative-time>
        · 19 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-225913862">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://cloud.githubusercontent.com/assets/11001914/25652882/e9e2be30-301c-11e7-8b61-e8e0fb1a7e99.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/11001914/25652882/e9e2be30-301c-11e7-8b61-e8e0fb1a7e99.png"  alt="2017-05-03 4 23 35" /></div></a></p>
<ol>
<li>
<p>How to hide the yellow block warning from webpack?</p>
</li>
<li>
<p>I'm not using PropTypes in my app so I guess the first red warning is from npm package,but how to know which package using this?I thought it's not a clear warning.</p>
</li>
</ol>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-298929156">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>I'm not using PropTypes in my app so I guess the first red warning is from npm package,but how to know which package using this?I thought it's not a clear warning.</p>
</blockquote>
<p>If you click on it you will see the callsite stack. Clicking on each item will show the source for each stack frame, so you can see where it is coming from.</p>
<blockquote>
<p>How to hide the yellow block warning from webpack?</p>
</blockquote>
<p>Why do you want to hide those warnings?<br />
It shouldn't be hard to fix those warnings, and <code>alt</code> tags are necessary for accessibility.</p>
<p>For example, you could fix <code>&lt;img src="pic.jpg" /&gt;</code> to be <code>&lt;img src="pic.jpg" alt="User profile" /&gt;</code>, and these warnings will go away. You can google the name of each warning (<code>jsx-a11y/img-has-alt</code> or <code>no-useless-concat</code>) to learn more about them and why fixing them is a good idea.</p>
<p>If you insist on ignoring them, the terminal prints a hint on how to do it.</p>
<p><a href="https://cloud.githubusercontent.com/assets/810438/25665553/e0d4c5ec-3015-11e7-8462-b424ce2561bc.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/810438/25665553/e0d4c5ec-3015-11e7-8462-b424ce2561bc.png"  alt="screen shot 2017-05-03 at 15 33 28" /></div></a></p>
<p>I hope this helps!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-299082221">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>If all from bundle.js how to know which function calling it.</p>
<p><a href="https://cloud.githubusercontent.com/assets/11001914/25688402/61d5dd2a-30b1-11e7-959b-61b3bd410cb8.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/11001914/25688402/61d5dd2a-30b1-11e7-959b-61b3bd410cb8.png"  alt="2017-05-04 10 06 07" /></div></a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-299083684">

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/Timer" target="_blank">Timer</a>
  

    </strong>

    commented

    <a href="#issuecomment-299083684" target="_blank"><relative-time>on May 4, 2017</relative-time></a>


      
  •


  
    <summary>
      
          edited
      
      
    </summary>

    
  

  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Interesting, chrome should be picking up on your sourcemap and give you the real locations.<br />
Can you try clicking on one of the "bundle.js" links and seeing if chrome recommends loading + turning on sourcemaps?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-299086815">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>ok,after turn on<br />
<a href="https://cloud.githubusercontent.com/assets/11001914/25689267/263bf166-30b9-11e7-9b3d-6d82d37effba.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/11001914/25689267/263bf166-30b9-11e7-9b3d-6d82d37effba.png"  alt="2017-05-04 11 02 04" /></div></a></p>
<p>It shows up the call stack</p>
<p><a href="https://cloud.githubusercontent.com/assets/11001914/25689277/380473e6-30b9-11e7-80a5-2bbdd5e21648.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/11001914/25689277/380473e6-30b9-11e7-80a5-2bbdd5e21648.png"  alt="2017-05-04 10 51 42" /></div></a></p>
<p>but the <code>propType</code> was used in third party npm package,so still can't fix it before pull request.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-299198662">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I’m not sure what exactly you are asking. If you click on those links, one of them will be a component (probably a third party one). File an issue with the repository of this component, and somebody will fix it and release an update that doesn’t rely on <code>React.PropTypes</code>.</p>
<p>This warning is also not urgent, and you can ignore it. It’s only here to prepare you for React 16 release.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-304321215">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hey <a href="https://github.com/gaearon" target="_blank">@gaearon</a> , while I like having the eslint warnings while linting, I don't really like them littering the chrome console. The reason being is that I often want to console log stuff to the chrome console and it always seems like I have about 10 of those warnings in the way (even if I do clean them up after).</p>
<p>Is there a way to make it so they just don't get output to the chrome console? Seems like this should be an easy option to tweak. Thanks!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-304326881">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>We cap warnings in the console by five files maximum.</p>
<p>Can you explain more about your use case of developing with many warnings? What kind of warnings are you seeing? Why are you ignoring them in development?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-304331658">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hey <a href="https://github.com/gaearon" target="_blank">@gaearon</a>,<br />
Thanks for replying so quickly :)</p>
<p>Okay, an example that happens all the time is that I'm editing a file and making changes, maybe commenting out a part of the code I think might be at the root of some issue.  This might cause several "unused variable" warnings. I don't immediately want to fix those warnings because I'll likely comment back in the code in a second once I've determined what the issue is. Everything is fine so far, but once I want to simultaneously console log some variable, the chrome warnings become very annoying.</p>
<p>I am sure other people are experiencing this because it is a common complaint of my coworkers as well.</p>
<p>The errors still show up in the terminal (which I like better because it doesn't get in the way of my console logs and I can actually click on the line in question and hop over to my editor and fix it) and I can still enforce that linting passes before allowing commits/PRs to be merged.</p>
<p>It doesn't seem too tough to allow for people to optionally turn these off. Can we do it?</p>
<p>Thanks!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-304332505">

    
<div>
  

    
    
      Member
    



  <h3>

    <strong>
      

  <a href="/gaearon" target="_blank">gaearon</a>
  

    </strong>

    commented

    <a href="#issuecomment-304332505" target="_blank"><relative-time>on May 27, 2017</relative-time></a>


      
  •


  
    <summary>
      
          edited
      
      
    </summary>

    
  

  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Can you show me a screenshot of this in practice?</p>
<blockquote>
<p>It doesn't seem too tough to allow for people to optionally turn these off. Can we do it?</p>
</blockquote>
<p>No. We don't do this because instead of fixing the problem it just introduces an obscure configuration flag that most people don't know about. We can either fix it for everybody, or not fix it at all.</p>
<p>I want to better understand what the problematic case looks like (a screenshot) so that I have a better idea of how to fix it for everybody.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-304340860">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Here are some screenshots:<br />
<a href="https://cloud.githubusercontent.com/assets/2730609/26504669/6761e482-41fa-11e7-825b-a0bf3c8418d5.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/2730609/26504669/6761e482-41fa-11e7-825b-a0bf3c8418d5.png" alt="image" /></div></a></p>
<p><a href="https://cloud.githubusercontent.com/assets/2730609/26504753/af8587fa-41fa-11e7-9609-dae777d9c9c7.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/2730609/26504753/af8587fa-41fa-11e7-9609-dae777d9c9c7.png" alt="image" /></div></a></p>
<p>Clearly there are other unused var issues that arise from us not always fixing these eslint warnings right away (usually because we are commenting out something that is in development).</p>
<p>While it definitely could be argued that we should just fix those issues before pushing any shared code, often it doesn't make sense to do so if it is a feature that will be added back in eventually.</p>
<p>Does that help you understand more where these linting warnings are coming from?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-304341943">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>We can either fix it for everybody, or not fix it at all.</p>
</blockquote>
<p>I'm not sure I agree with that statement. This doesn't seem like something that can be "fixed" for everybody. It seems like it is a feature that some people might want and others might not want. In my case, I like the terminal lint warnings, but I don't like the chrome lint warnings. For another person they might like both, or vice-versa.</p>
<p>Having an option to suppress the chrome lint warnings would make me happy :)</p>
<p>Thanks!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-304372059">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hey <a href="https://github.com/gaearon" target="_blank">@gaearon</a> I just upgraded to the most recent version and see that these warnings are now limited to 5 like you said:<br />
<a href="https://cloud.githubusercontent.com/assets/2730609/26510145/c24f6a52-4210-11e7-8d9e-68f69088303e.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/2730609/26510145/c24f6a52-4210-11e7-8d9e-68f69088303e.png" alt="image" /></div></a></p>
<p>So that should solve my issue. Thanks!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-304388424">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>That’s why I said it‘s better to fix for everyone <g-emoji>😉</g-emoji> There were two different issues: noisy bad output (which we fixed) and lack of limits (which we also fixed).</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-304388587">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Also, the "definition for rule was not found" warnings are related to something being wrong in your <code>node_modules</code>. Please remove the <code>node_modules</code> folder and run <code>npm install</code> again. If you have specific versions of plugins in your <code>package.json</code> please remove them because it is not supported.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-304388814">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Once you fix that you might see more noisy warnings (since each file has more than one warning). I'm happy to discuss this in a separate issue. For example we could only show warnings in the Chrome console for most recently edited file. I'm not sure if it's possible but happy to have someone look into it, if you're interested!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-304389102">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I filed <a href="https://github.com/facebook/create-react-app/issues/2378" target="_blank">facebookincubator#2378</a> as next step to improve this.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-326481681">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>Having an option to suppress the chrome lint warnings would make me happy :)</p>
</blockquote>
<p>Second this. There's times where I'm dropping gear and working across a number of files, and all I want to see in the chrome output is <em>my</em> console output. Having a limiter here would uber convenient (and a few engineers from various teams I've worked with agree)</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-326490792">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/dwelch2344" target="_blank">@dwelch2344</a> Could you clarify, what sort of warnings are you seeing there?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-381408211">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/Inlesco" target="_blank">Inlesco</a>
  

    </strong>

    commented

    <a href="#issuecomment-381408211" target="_blank"><relative-time>on Apr 15</relative-time></a>


      
  •


  
    <summary>
      
          edited
      
      
    </summary>

    
  

  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/gaearon" target="_blank">@gaearon</a> Is there still no way to disable all the <code>console.warn</code> (with yellow background) output in the Chrome dev console for ESLint errors/warnings?</p>
<p>Example:</p>
<pre><code>webpackHotDevClient.js:136 ./src/components/Cars/AddNewCarModal.js
  Line 73:  Expected a default case  default-case
</code></pre>
<p>Disabling this would be very useful</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>










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

  

  


  
</div>

          
      </div>

</div>


        </div>
      </div>

    </div>
    
  
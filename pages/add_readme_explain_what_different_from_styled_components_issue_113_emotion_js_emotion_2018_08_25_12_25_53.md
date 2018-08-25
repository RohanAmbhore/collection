<a href="https://github.com/emotion-js/emotion/issues/113">https://github.com/emotion-js/emotion/issues/113</a><div id="articleHeader"><h1>              Add readme explain what different from styled-components            #113    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/cncolder" target="_blank">cncolder</a>  opened this Issue
        <relative-time>on Jul 8, 2017</relative-time>
        · 10 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          <div>
            




            
<div id="issue-241457512">
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          
<p>Some people(like me) interesting emotion. Bcs emotion api same as styled-components.</p>
<p>But I cannot understand the different between these two modules without dig in source codes.</p>
<ul>
<li><code>emotion</code> version: latest</li>
<li><code>react</code> version: latest</li>
</ul>
<p>Relevant code.</p>

<p>What you did:</p>
<p>What happened:</p>

<p>Reproduction:</p>
<p>Problem description:</p>
<p>Suggested solution:</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>

          </div>

          

  


  


  
<div>
    
  <div>

  




  
<div id="issuecomment-334696675">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Given the <code>styled-components</code> have been out there for a while (with, effectively, same/very similar API), what is the difference? What are pros/cons of using the library over <code>styled-components</code>?</p>
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

  




  
<div id="issuecomment-334955156">
    
  <div>

    
<div>
  

    
    
      Member
    



  <h3>

    <strong>
      

  <a href="/tkh44" target="_blank">tkh44</a>
  

    </strong>

    commented

    <a href="#issuecomment-334955156" id="issuecomment-334955156-permalink" target="_blank"><relative-time>on Oct 8, 2017</relative-time></a>


    
      <include-fragment>
            
  •


  
    <summary>
      <div>
        
            edited
        
        
      </div>
    </summary>
    
  

      </include-fragment>
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm probably missing some things because I'm biased. These are just the things I could come up with off the top of my head.</p>
<p>Advantages of emotion</p>
<ul>
<li>smaller</li>
<li><code>css</code> api is much more powerful. You can use it by itself if you like that method of writing styles better.</li>
<li>source maps</li>
<li>better SSR story in my opinion</li>
<li>you can use the babel plugin for even more optimization</li>
<li>custom stylis plugins can be used (RTL plugins anyone?)</li>
<li>faster</li>
</ul>
<p>Disadvantages of emotion</p>
<ul>
<li>Missing <code>attr</code> (use withProps or wrap the component in a HoC)</li>
<li>Marketing and hype are much stronger for styled-components. This generally leads to an ecosystem that has to follow their lead. (We want dev tools support for prettier, IDEs, linters, etc)</li>
<li>styled-components docs are better as of right now and I imagine we will be playing catch up for a while.</li>
<li>There are less google results for issues and problems.</li>
</ul>
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

  




  
<div id="issuecomment-335215743">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/tkh44" target="_blank">@tkh44</a> Thank you for the explanation!</p>
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

  




  
<div id="issuecomment-357013858">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I've been keeping my eye on several css-in-js solutions for a while as I'm looking to phase out css modules and replace it with something a little bit more bundle friendly, fast, with dead code elimination, but also with the possibility to preparse anything that's not dynamic @ build-time. That last one is where most solutions fall flat. If I'm not mistaken the babel-plugin provides this, but it surprises me that this is not more prominently mentioned and documented, as for me this is definitely the biggest selling point.</p>
<p>Am I correct in assuming that css styles are parsed at build-time, unless they contain dynamic values? If so, is there any difference in how this is dealt with between object syntax & tagged template literal?</p>
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

  




  
<div id="issuecomment-357045927">
    
  <div>

    
<div>
  

    
    
      Member
    



  <h3>

    <strong>
      

  <a href="/tkh44" target="_blank">tkh44</a>
  

    </strong>

    commented

    <a href="#issuecomment-357045927" id="issuecomment-357045927-permalink" target="_blank"><relative-time>on Jan 12</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I don't sell the idea because I don't believe in it. We are making trade-offs. If you are are writing your css in javascript just so that you can use one less file you are kidding yourself. css-in-js is about flexibility and dynamic values both of which are severely handicapped by trying to statically extract them.</p>
<p>The view that css-in-js is some magic solution to the classic problems of css is a misguided one. There are still hard problems to figure out when writing apps with libraries like emotion, but that does not mean that css-in-js is the wrong choice. You have to make a choice at some point. Which set of issues would you like to deal with on a project? The issues of using CSS as we have in the past or the issues of using CSS in this way that we are now.</p>
<p>CSS-in-JS is a very, very simple process. You give me styles. I hash the content. I create a CSS Rule(s) using the hash as the class name. I put those Rule(s) into a stylesheet that exists somewhere in the DOM. This stylesheet uses the exact set of APIs that writing some CSS styles in an inline style tag and inserting it into the DOM would do.</p>
<p>What you believe is the biggest selling point is a myth. emotion is quite fast and able to handle some serious usage in its standard mode (100m+ views/month SSR sites). Do not let fear and uncertainty rule your decision of a library. Narrow down the problems you would like to solve and then ask yourself if CSS-in-JS is going to help you with those or avoid them altogether. Let's pretend it will. Ok, now you've got a new set of problems you are going to learn how to solve and they are much more interesting than the problems that classical css presents, but you still have to learn how to deal with them. That takes time and energy that is precious in development cycles.</p>
<p>My larger point is to think about why we chose to use a library, framework, or pattern. Sometimes we create a problem for ourselves just so we can try something new. That is perfectly fine and its how we learn but just know that the context of that decision is everything. From my experience, the better route is to learn about this new thing and gain some understanding of the context of its use but do not force it but rather wait for a situation to arise when it is needed. Just be patient.</p>
<blockquote>
<p>Am I correct in assuming that css styles are parsed at build-time, unless they contain dynamic values? If so, is there any difference in how this is dealt with between object syntax & tagged template literal?</p>
</blockquote>
<p>All styles are run through stylis on the fly to expand nested styles/media queries and auto prefix properties. We use a sort of (piece table)[https://en.wikipedia.org/wiki/Piece_table] to construct styles from cached fragments.</p>
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

  




  
<div id="issuecomment-360181843">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/tkh44" target="_blank">@tkh44</a> would you consider adding this to the readme? with some benchmarks?</p>
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

  




  
<div id="issuecomment-364051592">
    
  <div>

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/baba43" target="_blank">baba43</a>
  

    </strong>

    commented

    <a href="#issuecomment-364051592" id="issuecomment-364051592-permalink" target="_blank"><relative-time>on Feb 8</relative-time></a>


    
      <include-fragment>
            
  •


  
    <summary>
      <div>
        
            edited
        
        
      </div>
    </summary>
    
  

      </include-fragment>
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Well, the first thing that I did after reading an article about emotion was to google "emotion vs styled components". If you are presenting a new solution to the community, you really have to explain why people should give it a try over other solutions. Of course you have thousands of thoughts in your mind, but <em>we do not</em>. So, if you argue about popularity, keep this in mind.</p>
<p>Right now I have started using emotion for multiple smaller projects and it is working fine so far. I really like it, but I still do not really get the advantages over styled components. That said, I can not recommend it to other developers that are asking me <em>"Why not styled components or ..."</em>. So yes, it is up to the developer to compare different solutions, but I think you should make it as easy as possible if you want to reach many people.</p>
<p>And you should, because this project looks very promising! <g-emoji>👍</g-emoji><br />
Keep up your great work and thank you very much.</p>
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

  




  
<div id="issuecomment-364565430">
    
  <div>

    
<div>
  

    
    
      Member
    



  <h3>

    <strong>
      

  <a href="/tkh44" target="_blank">tkh44</a>
  

    </strong>

    commented

    <a href="#issuecomment-364565430" id="issuecomment-364565430-permalink" target="_blank"><relative-time>on Feb 10</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>Well, the first thing that I did after reading an article about emotion was to google "emotion vs styled components". If you are presenting a new solution to the community, you really have to explain why people should give it a try over other solutions. Of course you have thousands of thoughts in your mind, but we do not. So, if you argue about popularity, keep this in mind.</p>
</blockquote>
<p>The problem with your train of thought here is that you think I care about the number of devs using this library. It doesn't matter to me. I created this library to address a specific technical problem presented to me. I love having a community around it and having others contribute and the relationships that have formed while working on it. That is what is important to me. I can live without the big numbers.</p>
<blockquote>
<p>Right now I have started using emotion for multiple smaller projects and it is working fine so far. I really like it, but I still do not really get the advantages over styled components. That said, I can not recommend it to other developers that are asking me "Why not styled components or ...". So yes, it is up to the developer to compare different solutions, but I think you should make it as easy as possible if you want to reach many people.</p>
</blockquote>
<p>tbh, there probably isn't a huge advantage. Emotion can be a smaller download, especially if using emotion directly without react-emotion. That's really about it. The lib's performance characteristics start to diverge when doing SSR at <em>scale</em>. I can't honestly tell you the current performance numbers and if this is still true. Regardless, who cares, I like to create styles from fragments and mix css props, className, and styled components patterns. You just can't do that with other libraries. They force you to use the styled components or the css prop or some StyleSheet.create mechanic and on and on. All this strict, pick a style and force your developers in a box mantra you see is nonsense. Use the right pattern for the problem you are presented.</p>
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

  




  
<div id="issuecomment-370408423">
    
  <div>

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/seanchas" target="_blank">seanchas</a>
  

    </strong>

    commented

    <a href="#issuecomment-370408423" id="issuecomment-370408423-permalink" target="_blank"><relative-time>on Mar 5</relative-time></a>


    
      <include-fragment>
            
  •


  
    <summary>
      <div>
        
            edited
        
        
      </div>
    </summary>
    
  

      </include-fragment>
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I prefer emotion for styled components because of emotion's ability to have both components and class names. This makes easiest integration with packages like react-router (NavLink's activeClassName) and react-dropzone. No need to wrap components in HOCs to make them work out of the box.<br />
<a href="https://github.com/baba43" target="_blank">@baba43</a> <a href="https://github.com/tkh44" target="_blank">@tkh44</a></p>
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

  




  
<div id="issuecomment-376478642">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>One thing I've noticed is that styled components doesn't expose its api to allow creation of custom instances (or its not documented very well if you can do that). The only way I could get emotion to work for us was to create a custom instance of emotion and tie that into the nonce we generate on the server, in order to work with our CSP.</p>
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

  











        
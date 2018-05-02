<a href="https://github.com/styled-components/styled-components/issues/1226">https://github.com/styled-components/styled-components/issues/1226</a><div id="articleHeader"><h1>              styled(Component) does not apply styles to functional component that returns styled-component            #1226    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/garrettmaring" target="_blank">garrettmaring</a>  opened this Issue
        <relative-time>on Oct 10, 2017</relative-time>
        · 9 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-263976770">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          
<h2>Version</h2>
<p><strong>Styled Components</strong>: 2.1.1<br />
<strong>React</strong>: 16.0.0</p>
<h2>Steps to reproduce</h2>
<div><pre>const DataDefinitionListItem = ({ label, value }) =&gt; (
  &lt;Flex align="center" direction="column"&gt;
    &lt;Flex.Item&gt;
      &lt;DataDefinitionListItemValue&gt;
        {value.toString()}
      &lt;/DataDefinitionListItemValue&gt;
    &lt;/Flex.Item&gt;
    &lt;Flex.Item&gt;
      &lt;DataDefinitionListItemLabel&gt;
        {label}
      &lt;/DataDefinitionListItemLabel&gt;
    &lt;/Flex.Item&gt;
  &lt;/Flex&gt;
);

export default styled(DataDefinitionListItem)`
  display: none;
`;</pre></div>
<p>The <code>&lt;Flex&gt;</code> component is a styled component. The bug is also reproducible when wrapping the <code>&lt;Flex&gt;</code> inside a <code>&lt;div&gt;</code>.</p>
<h2>Expected Behavior</h2>
<p>This item should have the style <code>display: none</code> applied to its wrapper element created by styled-components.</p>
<h2>Actual Behavior</h2>
<p>The style is not applied.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  


          

          

  


  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-335240613">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Also btw, as best practice that often helps keep your styling code scalable:</p>
<p>Try to not wrap a structural component (like DataDefinitionListItem) in another styled component.</p>
<p>Styled components are presentational components. They render just some styled elements. While I often makes sense to wrap external, third party components, it doesn’t to wrap your own structural component again.</p>
<p>In short it’s advisable to try to keep to the following structure from top to bottom: container → structural → presentational components</p>
<p>When you think about wrapping your own components, this often moves UI logic around to a couple of places. If you keep them inside their respective structural and presentational components there’s always only one place where stylistic variants and differences (I.e. css classes and styles) can come from</p>
<p>Hope this helps as well :)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-335252205">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Ah, I absolutely just read over that! (Reading examples and not the documentation above is a bad habit). Apologies for missing something in the docs.</p>
<p>That being said, is it really needed to force users to do that on their own? Could it not be a prop that <code>styled components</code> deals with directly?</p>
<p>And thank you for the design tip! :)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-335257089">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>@garettmaring it is certainly possible by capturing the output of your component and replacing the React lifecycle for it, but I don't believe that's a good idea <g-emoji>😉</g-emoji> Probably a bad practice entirely</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-335258006">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Oh, that's a good point. Appreciate the quick replies!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-367715371">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/kitten" target="_blank">@kitten</a> May I ask why it is not a good practice to wrap an existing styled component ?<br />
In some cases, you have a component that you use it in several places but sometimes the same component and its logic but just with different style sheet, so doesn't it make sense when you wrap it and pass to it different styles in this case ?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-367766903">

    
<div>
  

    
    
      Member
    



  <h3>

    <strong>
      

  <a href="/kitten" target="_blank">kitten</a>
  

    </strong>

    commented

    <a href="#issuecomment-367766903" target="_blank"><relative-time>on Feb 23</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/sadokmtir" target="_blank">@sadokmtir</a> so to be break my last comment up there (<a href="https://github.com/styled-components/styled-components/issues/1226#issuecomment-335240613" target="_blank">#1226 (comment)</a>) down a little.</p>
<p>There's several ways to alter a StyledComponent once it's created and hence after a while you build up your component library quite a bit. There are some practices that avoid this library becoming less maintainable.</p>
<p>If you wrap some or one StyledComponents in a normal component to add logic, you basically create a structure of StyledComponents around them. This structure is best maintained when all presentational (read classes, styles) concerns are not inside these "structural components". This makes more sense when you think of them in a tree. You have some state in higher components, some structure in the middle, and your styles below. This specialises every part of your application to do one thing in a simple way.</p>
<p>Now, let's say you'd like to extend a structural component. Let's say you have a <code>Menu</code> (normal component) that wraps a couple of StyledComponents. It might be intuitive for you, depending on your thinking / background / etc, to just wrap it: <code>styled(Menu)</code>. This is not wrong, and <code>Menu</code> can subsequently accept a <code>className</code>, but the thing to remember is that you're most likely building a component library for an app, not a fully 100% reusable library for npm.</p>
<p>Effectively doing this will mix some presentational (styling) concerns <strong>above</strong> structural components. This means that in a refactor you now can't rely on a stable order, as outlined in my previous comment.</p>
<p>Instead you could pass props, utilise the theme, react to being wrapped in a certain component. But all in all, I can guarantee you that if you try to adhere to the structure I propose, where it's best to wrap/extend StyledComponents themselves <strong>first</strong> before trying anything else, you will find your styled-components-driven application to suddenly become a lot more maintainable, even past thousands of styles.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-367851842">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Styled-Component should rename itself as <code>styled-element</code> since it really does not style a real react component, even the simplest functional one ... no?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-367858545">

    
<div>
  

    
    
      Member
    



  <h3>

    <strong>
      

  <a href="/kitten" target="_blank">kitten</a>
  

    </strong>

    commented

    <a href="#issuecomment-367858545" target="_blank"><relative-time>on Feb 23</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/adamchenwei" target="_blank">@adamchenwei</a> very off topic, so please keep these types of things to Spectrum or sth casual like Twitter <g-emoji>😉</g-emoji> but the idea is that it's creating styled components. Even an element will be wrapped as a component.</p>
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

  

  


  


          
      




        
      

    
    
  
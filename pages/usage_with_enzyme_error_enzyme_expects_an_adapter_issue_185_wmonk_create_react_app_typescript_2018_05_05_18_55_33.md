<a href="https://github.com/wmonk/create-react-app-typescript/issues/185">https://github.com/wmonk/create-react-app-typescript/issues/185</a><div id="articleHeader"><h1>              Usage with Enzyme, error: Enzyme expects an adapter            #185    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/QuantumInformation" target="_blank">QuantumInformation</a>  opened this Issue
        <relative-time>on Nov 6, 2017</relative-time>
        · 12 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-271464724">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I have the following setup</p>
<p><a href="https://user-images.githubusercontent.com/216566/32441178-490e0950-c2ee-11e7-8f0a-69fbdba7d69c.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://user-images.githubusercontent.com/216566/32441178-490e0950-c2ee-11e7-8f0a-69fbdba7d69c.png" alt="image" /></div></a></p>
<p>but get this error:</p>
<pre><code> Enzyme Internal Error: Enzyme expects an adapter to be configured, but found none. To
          configure an adapter, you should call `Enzyme.configure({ adapter: new Adapter() })`
          before using any of Enzyme's top level APIs, where `Adapter` is the adapter
          corresponding to the library currently being tested. For example:

          import Adapter from 'enzyme-adapter-react-15';
</code></pre>
<p>I get the same error if I rename to <code>setupTests.ts</code></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-342922873">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Experiencing the same issue. I've tried changing between "setupFiles" and "setupTestFrameworkScriptFile", using 'require()', 'import * as'. Same error.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-343225684">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Similar to <a href="https://github.com/adepatie" target="_blank">@adepatie</a> and the stackoverflow above,</p>
<p>I have a working setup with the following:</p>
<p><strong>package.json</strong></p>
<div><pre>...
"enzyme": "^3.0.0",
"enzyme-adapter-react-16": "^1.0.2",
"@types/enzyme": "^3.1.0",
"react-scripts-ts": "2.8.0",
...</pre></div>
<p><strong>setupTests.ts</strong>:</p>
<div><pre>import * as enzyme from 'enzyme';
import * as Adapter from 'enzyme-adapter-react-16';
enzyme.configure({ adapter: new Adapter() });</pre></div>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-343767792">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Thanks for the workaround people <g-emoji>❤️</g-emoji></p>
<p>I've been having similar problems. It looks like src/setupTests.js is not running before every test file (<a href="https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#srcsetuptestsjs" target="_blank">as it should</a>). I work around the issue by adding:</p>
<div><pre>import * as Adapter from 'enzyme-adapter-react-15';

configure({ adapter: new Adapter() });</pre></div>
<p>to the test suite, which works fine for now since it's a small project with not many suites.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-343768881">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hey <a href="https://github.com/NirBenita" target="_blank">@NirBenita</a> have you tried renaming that file to setupTests.ts ?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-344047266">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Could someone submit a PR to get this working correctly?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-344495455">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><code>src/setupTests.ts</code> should be working correctly (is for me on 2.8.0)</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-347859620">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>It does not work at all for me</p>
<pre><code>"enzyme": "3.2.0",
"enzyme-adapter-react-16": "1.1.0",
"react-scripts-ts": "2.8.0",
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
    
  <div id="issuecomment-347874675">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <blockquote>
<p>It does not work at all for me</p>
</blockquote>
<p><a href="https://github.com/abenchi" target="_blank">@abenchi</a> , would you mind elaborating this ? "It does not work" lacks precision.<br />
If you follow these <a href="https://github.com/DorianGrey/create-react-app-typescript/blob/6277b60b13a2109b22bb96c73ee01b7fba5fc9a1/packages/react-scripts/template/README.md#testing-components" target="_blank">instructions</a> (that's from a PR, but it has only some minor differences from the original version <a href="https://github.com/facebookincubator/create-react-app/tree/master/packages/react-scripts/template#testing-components" target="_blank">here</a>), what <em>exactly</em> fails to work?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-348285685">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Instructions on how to setup <code>enzyme</code> have been adopted to conform to the particular typescript requirements.<br />
See <a href="https://github.com/wmonk/create-react-app-typescript/blob/master/packages/react-scripts/template/README.md#testing-components" target="_blank">here</a>. Yes, it's somewhat hidden, but in the same position as in the original CRA.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-348505655">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Indeed, it was my error, by doing the follwing to avoid the requestAnimationFrame warnings</p>
<pre><code>"test": "react-scripts test --env=jsdom --setupTestFrameworkScriptFile=raf/polyfill",
</code></pre>
<p>I override the setupTests...<br />
Thanks for your feedback</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-385572743">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/arbtfnf" target="_blank">arbtfnf</a>
  

    </strong>

    commented

    <a href="#issuecomment-385572743" target="_blank"><relative-time>4 days ago</relative-time></a>


      
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

          <p>This error occurs when you are using React16, and trying to install Enzyme@2 with "npm i --save-dev enzyme",<br />
Instead use the following code to run Enzyme with React-16<br />
<code>yarn add enzyme@3.0.0 enzyme-adapter-react-16@1.0.0 raf@3.3.2</code></p>
<blockquote>
<p>Here we have to use enzyme@3.0.0 to run it with react16, here we need to install adaptor also.<br />
So after running this code, inside test folder, create a file( name it eg: setupTest.js ) to wire-up adaptor with enzyme.<br />
In setupTest.js file copy/paste the following:</p>
</blockquote>
<p>import Enzyme from 'enzyme';<br />
import Adaptor from 'enzyme-adaptor-react-16';</p>
<p>Enzyme.configure({<br />
adaptor: new Adaptor()<br />
});</p>
<p>Now you need to add jest.config.json file on the root as it, this will tell to run raf then setupTests.js file<br />
<code>{ "setupFiles": [ "raf/polyfill", "&lt;rootDir&gt;/src/tests/setupTests.js" ] }</code></p>
<p>Update this in package.json file:<br />
"test": "jest --config=jest.config.json",</p>
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

  

  


  


          
      




        
      

    
    
  
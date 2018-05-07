<a href="https://github.com/facebook/jest/issues/4545">https://github.com/facebook/jest/issues/4545</a><div id="articleHeader"><h1>              requestAnimationFrame warning with React 16            #4545    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/taion" target="_blank">taion</a>  opened this Issue
        <relative-time>on Sep 27, 2017</relative-time>
        · 29 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  <div id="issue-261012707">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/taion" target="_blank">taion</a>
  

    </strong>

    commented

    <a href="#issue-261012707" target="_blank"><relative-time>on Sep 27, 2017</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><strong>Do you want to request a <em>feature</em> or report a <em>bug</em>?</strong><br />
Bug-ish</p>
<p><strong>What is the current behavior?</strong><br />
Warning emitted:</p>
<pre><code>  ● Console

    console.error node_modules/fbjs/lib/warning.js:33
      Warning: React depends on requestAnimationFrame. Make sure that you load a polyfill in older browsers. http://fb.me/react-polyfills
</code></pre>
<p><strong>If the current behavior is a bug, please provide the steps to reproduce and either a repl.it demo through <a href="https://repl.it/languages/jest" target="_blank">https://repl.it/languages/jest</a> or a minimal repository on GitHub that we can <code>yarn install</code> and <code>yarn test</code>.</strong><br />
Run any Jest tests with React 16</p>
<p><strong>What is the expected behavior?</strong><br />
No warning</p>
<p><strong>Please provide your exact Jest configuration and mention your Jest, node, yarn/npm version and operating system.</strong><br />
Jest v21.2.0<br />
jest-environment-jsdom-11.0.0 v20.0.9</p>
<p>This would be resolved by <a href="https://github.com/jsdom/jsdom/issues/1963" target="_blank">tmpvar/jsdom#1963</a> upstream. It's just sort of an annoying warning, and I don't want to define a custom environment just to stub polyfill rAF.</p>
<p>I think this is trackable here given that the React docs recommend Jest: <a href="https://facebook.github.io/react/docs/test-utils.html" target="_blank">https://facebook.github.io/react/docs/test-utils.html</a>, and that it'd be ideal for Jest tests to not emit warnings when used with the latest React release.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>

<a href="https://github.com/eslint/eslint/issues/4344">https://github.com/eslint/eslint/issues/4344</a><div id="articleHeader"><h1>              AssertionError: ImportDeclaration should appear when the mode is ES6 and in the module context            #4344    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/DmitrySoshnikov" target="_blank">DmitrySoshnikov</a>  opened this Issue
        <relative-time>on Nov 6, 2015</relative-time>
        · 16 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      


  
    
      

          <p>"version": "1.8.0"<br />
"escope": "^3.2.0"</p>
<p>This issue is coming from escope in general (feel free to redirect there instead), though not sure which config option in eslint exists to enable modules mode (other than <code>ecmaFeatures: { modules: true }</code> which we already use).</p>
<p>We use <code>ESLintTester</code> (which seems is deprecated now, so maybe issue can be related as well). Trying to test the:</p>
<div><pre>import Foo from 'Foo';

// Or type

import type Bar from 'Bar';</pre></div>
<p>Fails with the assertion in the escope:</p>
<pre><code>- AssertionError: ImportDeclaration should appear when the mode is ES6 and in the module context.
        at Referencer.ImportDeclaration (scripts/lint/eslint/node_modules/eslint/node_modules/escope/lib/referencer.js:711:17)
        at Referencer.Visitor.visit (scripts/lint/eslint/node_modules/eslint/node_modules/escope/node_modules/esrecurse/esrecurse.js:109:34)
        at Referencer.Visitor.visitChildren (scripts/lint/eslint/node_modules/eslint/node_modules/escope/node_modules/esrecurse/esrecurse.js:88:38)
        at Referencer.Program (scripts/lint/eslint/node_modules/eslint/node_modules/escope/lib/referencer.js:539:22)
        at Referencer.Visitor.visit (scripts/lint/eslint/node_modules/eslint/node_modules/escope/node_modules/esrecurse/esrecurse.js:109:34)
        at Object.analyze (scripts/lint/eslint/node_modules/eslint/node_modules/escope/lib/index.js:130:16)
        at EventEmitter.module.exports.api.verify (scripts/lint/eslint/node_modules/eslint/lib/eslint.js:736:35)
        at runRuleForItem (scripts/lint/eslint/node_modules/eslint/lib/testers/rule-tester.js:265:34)
        at testInvalidTemplate (scripts/lint/eslint/node_modules/eslint/lib/testers/rule-tester.js:302:26)
        at Spec.&lt;anonymous&gt; (scripts/lint/eslint/node_modules/eslint/lib/testers/rule-tester.js:370:21)
</code></pre>
<p>Is it a known issue? I didn't find other config options to allow <code>import</code> in the tests.</p>
<p>Thanks!</p>
      
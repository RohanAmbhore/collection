<a href="https://github.com/babel/babel-eslint/issues/312">https://github.com/babel/babel-eslint/issues/312</a><div id="articleHeader"><h1>              ESLint: 2.10.0 - Parsing error: Unexpected token =            #312    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/moroshko" target="_blank">moroshko</a>  opened this Issue
        <relative-time>on May 14, 2016</relative-time>
        · 13 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-154829416">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I'm using:</p>
<pre><code>eslint: 2.10.0
babel-eslint: 6.0.4
</code></pre>
<p>and getting the following error:</p>
<blockquote>
<p>Parsing error: Unexpected token =</p>
</blockquote>
<p>which points to class properties:</p>
<pre><code>export default class Autowhatever extends Component {
  static propTypes = {    // &lt;--- error points to this line
...
</code></pre>
<p>I expected <code>babel-eslint</code> to support class properties out of the box.</p>
<p>What am I missing?</p>
<p>Here is my eslint config:</p>
<div><pre>{
  "env": {
    "es6": true,
    "node": true,
    "browser": true
  },
  "parser": "babel-eslint",
  "parserOptions": {
    "sourceType": "module"
  }
}</pre></div>
      </td>
    </tr>
  </tbody>
</table>


        



    

  


          

          

  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-219212171">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I get the same error. It throws the error on windows but not osx.<br />
It looks to be a windows issue, sadly.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-219214513">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I get this error on osx. I don't see how this is related to <a href="https://github.com/eslint/eslint/issues/6158" target="_blank">eslint/eslint#6158</a> at all.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-219219893">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>It could be the same error as <a href="https://github.com/eslint/eslint/issues/6158" target="_blank">eslint/eslint#6158</a> in that 2.10 currently makes it so ESLint always uses the default parser and not babel-eslint. Try 2.9 and if it works then you should pin to 2.9 until a patch is released. Pretty sure that is the case.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
      


  <div>
  <h3 id="event-660716814">

    
      
    

    

        <img src="https://avatars3.githubusercontent.com/u/588473?s=60&v=4" width="16" height="16" alt="@hzoo" />
  <a href="/hzoo" target="_blank">hzoo</a>
  


      
changed the title from
Parsing error: Unexpected token =
to
ESLint: 2.10.0 - Parsing error: Unexpected token =


    <a href="#event-660716814" target="_blank"><relative-time>on May 14, 2016</relative-time></a>

  </h3>
</div>





  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-219223494">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I get this error on <code>eslint</code> 2.7, 2.9 and 2.10 on windows, using either <code>babel-eslint</code> 5.0.4 or 6.0.4.<br />
On OSX it seems to work for 2.7 with babel-eslint 5.0.4 for me.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-219229484">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Can someone check ESLint 2.10.1 which fixes the parser issue?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
      <div>
        <h3 id="ref-pullrequest-154853134">
      
        
      
        <img src="https://avatars1.githubusercontent.com/u/3165635?s=60&v=4" width="16" height="16" alt="@oliviertassinari" />
  <a href="/oliviertassinari" target="_blank">oliviertassinari</a>
  

      referenced this issue
        in <strong>mui-org/material-ui</strong>
      <a href="#ref-pullrequest-154853134" target="_blank">
        <relative-time>on May 15, 2016</relative-time>
      </a>
    </h3>

  
    
        
      Merged
    



    
      <h4>
        <a href="/mui-org/material-ui/pull/4262" target="_blank">
          [Examples] Simplify the examples
          #4262
        </a>
      </h4>
    

    

  
    2 of 3 tasks complete
    
      
    
  

  

</div>




  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-219248698">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I updated ESLint to 2.10.1 and this issue went away for me.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-219249705">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Same here, it's fixed <g-emoji>👍</g-emoji> .</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-219250103">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Cool. Yep, it basically turned off babel-eslint for everyone. If you don't don't get unexpected token there would of been an issue (or you don't need babel-eslint haha)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-219312110">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I'm still seeing the error. I'm using <code>eslint-loader</code> which could have to do with it, it looks like <a href="https://github.com/MoOx/eslint-loader/issues/92" target="_blank">more people</a> are seeing the issue as well.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-219313132">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I've gone back and forth, uninstalled everything concerning eslint locally and globally, then went back and tried installing <code>2.9.0</code> locally which <a href="https://github.com/hzoo" target="_blank">@hzoo</a> reported should work. I'm glad that version <code>2.9.0</code> works for me on windows after all. I must've tried too many things at once when I was testing different versions.<br />
I'll just use <code>2.9.0</code> until a better patch is released. Thanks <a href="https://github.com/hzoo" target="_blank">@hzoo</a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-317688758">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <h1><code>"parser": "babel-eslint"</code> is OK!</h1>
<div><pre>{
    "parser": "babel-eslint",
    "parserOptions": {
        "ecmaVersion": 6,
        "sourceType": "module",
        "ecmaFeatures": {
            "jsx": true,
            "modules": true,
            "experimentalObjectRestSpread": true
        }
    },
    "plugins": [
        "react"
    ],
    "extends": ["eslint:recommended", "plugin:react/recommended"],
    "rules": {
        "comma-dangle": 0,
        "react/jsx-uses-vars": 1,
        "react/display-name": 1,
        "no-unused-vars": "warn",
        "no-console": 1,
        "no-unexpected-multiline": "warn"
    },
    "settings": {
        "react": {
            "pragma": "React",
            "version": "15.6.1"
        }
    }
}
</pre></div>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  











        


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

  

  


  


          
      




        
      

    
    
  
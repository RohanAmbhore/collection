<a href="https://github.com/facebook/jest/issues/2663">https://github.com/facebook/jest/issues/2663</a><div id="articleHeader"><h1>              "Syntax Error: Invalid or unexpected token" with .png            #2663    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/matheusml" target="_blank">matheusml</a>  opened this Issue
        <relative-time>on Jan 22, 2017</relative-time>
        · 21 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-202323542">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm trying to test a simple module, but I'm getting this error:</p>
<pre><code>Test suite failed to run

    /home/matheusml/Projects/react-completo/src/assets/images/dribble-logo.png:1
    ({"Object.&lt;anonymous&gt;":function(module,exports,require,__dirname,__filename,global,jest){�PNG
                                                                                             ^
    SyntaxError: Invalid or unexpected token
      
      at transformAndBuildScript (node_modules/jest-runtime/build/transform.js:320:12)
      at Object.&lt;anonymous&gt; (src/components/container/Container.js:4:46)
      at Object.&lt;anonymous&gt; (src/components/App.js:4:44)

</code></pre>
<p>This is the test:</p>
<div><pre>import React from 'react';
import renderer from 'react-test-renderer';
import { Router } from 'react-router';

import App from './App';

test('App', () =&gt; {
  const component = renderer.create(
    &lt;App /&gt;
  );
  let tree = component.toJSON();
  expect(tree).toMatchSnapshot();
});</pre></div>
<p>This is my package.json:</p>
<div><pre>"jest": {
    "moduleNameMapper": {
      "\\.(jpg|jpeg|png|svg)$": "./src/config/fileMock.js",
      "\\.(css|scss)$": "identity-obj-proxy"
    }
  }</pre></div>
<p>And this is the fileMock.js:</p>
<div><pre>module.exports = 'test-file-stub';</pre></div>
<p>Thanks!</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  


          

          

  


  


  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-278547927">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/matheusml" target="_blank">@matheusml</a> did you solve this at all? <a href="https://github.com/cpojer" target="_blank">@cpojer</a> I can confirm I'm having this issue too. I have static assets outside my source. i.e. My directory structure looks like:</p>
<pre><code>public
|-fonts
|-img
\_styles
src
|-components
|-pages
...
</code></pre>
<p>My jest config looks similar to the example given in the link:</p>
<div><pre>"jest": {
    "collectCoverageFrom": [ "src/**/*.{js,jsx}" ],
    "moduleNameMapper": {
      "\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$": "tests/__mocks__/fileMock.js"
    }
  }</pre></div>
<p>My test fails when it tries to import the image:</p>
<div><pre>import thumbnail from 'img/thumbnail.png'</pre></div>
<p>I guess its important to note that if I don't include the <code>public</code> directory in <code>moduleDirectories</code>, then i get the error: <code>Cannot find module 'img/thumbnail.png' from 'MyModule.js'</code></p>
<p>Is this expected? Should it really validate the existence of an import event though the module mapping is already setup? Otherwise I get the same error as above. I haven't tried any other type of import in the name mapper.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-285915082">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I am facing the same issue, I am trying to have reactjs server rendering implemented. Any fix for this.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-285915192">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I have put this in my babelrc and things seem to be working:</p>
<p>{<br />
"presets": ["es2015", "react"]<br />
}</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-305498877">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Same type error</p>
<pre><code>SyntaxError: Unexpected token &lt;
      /media/sibin/F_WORK/&lt;path&gt;/&lt;icon-name&gt;.svg:1
      ({"Object.&lt;anonymous&gt;":function(module,exports,require,__dirname,__filename,global,jest){&lt;?xml version="1.0" encoding="UTF-8"?&gt;
                                                                                               ^
      SyntaxError: Unexpected token &lt;
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
    
  <div id="issuecomment-306870297">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I also seem to be having this issue as well. It only happens when I require the png.</p>
<pre><code>({"Object.&lt;anonymous&gt;":function(module,exports,require,__dirname,__filename,global,jest){�PNG
                                                                                             ^
    SyntaxError: Invalid or unexpected token
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
    
  <div id="issuecomment-311441266">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Same error as well. Does someone fix it?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-313613230">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Have the same error with .mp3, Nothing helps</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-313615154">

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/thymikee" target="_blank">thymikee</a>
  

    </strong>

    commented

    <a href="#issuecomment-313615154" target="_blank"><relative-time>on Jul 7, 2017</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Errors like this may also be a result of using a preset with absolute paths set in module name mapper for example. This case however will be fixed in the next release</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-317109798">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I had the same error and resolved it by creating a <strong>assetsTransformer.js</strong>:</p>
<pre><code>const path = require('path');

module.exports = {
  process(src, filename, config, options) {
    return 'module.exports = ' + JSON.stringify(path.basename(filename)) + ';';
  },
};
</code></pre>
<p>Then add this to your jest configuration in package.json:<br />
<code>"jest": { "moduleNameMapper": { "\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$": "&lt;rootDir&gt;/assetsTransformer.js", "\\.(css|less)$": "&lt;rootDir&gt;/assetsTransformer.js" } },</code></p>
<p>Source: <a href="https://facebook.github.io/jest/docs/webpack.html#content" target="_blank">https://facebook.github.io/jest/docs/webpack.html#content</a></p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-326381364">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>In my case, I didn't realize that <code>&lt;rootDir&gt;</code> is a <a href="https://facebook.github.io/jest/docs/en/webpack.html#configuring-jest-to-find-our-files" target="_blank">token supplied by Jest,</a> and assumed it was something I needed to replace. Adding it to the <code>moduleNameMapper</code> entries solved the issue.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-340243320">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I added the <code>assetTransformer.js</code> mentioned by @bombellos. Also followed instructions on <a href="https://facebook.github.io/jest/docs/webpack.html#content" target="_blank">Using with webpack</a>. But i still get the same errors.</p>

<pre><code> FAIL  components/__tests__/List.js
  ● Test suite failed to run

    /assets/images/logo-header.png:1
    ({"Object.&lt;anonymous&gt;":function(module,exports,require,__dirname,__filename,global,jest){�PNG
                                                                                             ^
    
    SyntaxError: Invalid or unexpected token
      
      at ScriptTransformer._transformAndBuildScript (node_modules/jest-runtime/build/script_transformer.js:305:17)
      at Object.&lt;anonymous&gt; (components/PageHeader.js:15:19)
      at Object.&lt;anonymous&gt; (components/Main.js:10:436)

</code></pre>

<pre><code> FAIL  ui/Button/__tests__/snapshot.test.js
  ● fixture 'TextAndIcon' snapshots are rendered correctly

    /assets/icons/fontawesome/regular.svg:1
    ({"Object.&lt;anonymous&gt;":function(module,exports,require,__dirname,__filename,global,jest){&lt;svg xmlns="http://www.w3.org/2000/svg" style="display: none;"&gt;
                                                                                             ^
    
    SyntaxError: Unexpected token &lt;
      
      at ScriptTransformer._transformAndBuildScript (node_modules/jest-runtime/build/script_transformer.js:305:17)
      at Icon (ui/Icon.js:31:17)
      at resolve (node_modules/react-dom/cjs/react-dom-server.node.development.js:2599:14)
      at ReactDOMServerRenderer.render (node_modules/react-dom/cjs/react-dom-server.node.development.js:2746:22)
      at ReactDOMServerRenderer.read (node_modules/react-dom/cjs/react-dom-server.node.development.js:2722:19)
      at Object.renderToStaticMarkup (node_modules/react-dom/cjs/react-dom-server.node.development.js:2991:25)
</code></pre>
<p>My folder structure is basically:</p>
<pre><code>&lt;rootDir&gt;
  assets
    *.png, *.svg, ...
  components
    *.js
  ui
    *.js
</code></pre>
<p>Apparently, the files are still loaded instead of mocked away, but i have no clue how to debug this.</p>
<p>.babelrc:</p>
<pre><code>{
  "presets": [
    ["es2015", {"modules": false}],
    "react",
    "stage-1",
    ["env", {
      "targets": {
        "browsers": [
          "last 3 versions",
          "&gt; 1%",
          "Firefox ESR",
          "iOS 9"
        ]
      }
    }]
    
  ],
  "plugins": [
    "react-hot-loader/babel",
    "transform-class-properties",
    "transform-react-jsx-source",
    "glamorous-displayname",
    "wildcard"
  ],
  "env": {
    "development": {
      "plugins": [
        ["transform-runtime", {
          "polyfill": true
        }]
      ]
    },
    "test": {
      "plugins": ["transform-es2015-modules-commonjs"]
    }
  }
}
</code></pre>
<p>package.json:</p>
<pre><code>  "jest": {
    "snapshotSerializers": [
      "jest-glamor-react",
      "enzyme-to-json/serializer"
    ],
    "moduleFileExtensions": ["js"],
    "moduleDirectories": ["node_modules"],
    "transform": {
      "\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$": "&lt;rootDir&gt;/config/jest/assetsTransformer.js"
    }
  },
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
    
  <div id="issuecomment-340257293">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I am dumb, i had another <code>jest.config.js</code> in my root folder which overwrote the settings in <code>package.json</code>. Although it's not runnning yet, i don't get this particular error anymore.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-340259853">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Got it working. Here are the important bits (please note that i have some additional config due to enzyme 3 with react 16):</p>
<p><code>.babelrc</code></p>
<pre><code>{
  "presets": [
    "es2015",
    "react",
    "stage-1",
    "env"

  ],
  "plugins": [
    "react-hot-loader/babel",
    "transform-class-properties",
    "transform-react-jsx-source",
    "glamorous-displayname",
    "wildcard"
  ],
  "env": {
    "development": {
      "plugins": [
        ["transform-runtime", {
          "polyfill": true
        }]
      ]
    }
  }
}
</code></pre>
<p><code>jest.config.js</code></p>
<pre><code>// this helps: https://github.com/facebook/jest/issues/2081#issuecomment-332406033
module.exports = {
  verbose: true,
  setupFiles: ['./jest.setup.js'],
  snapshotSerializers: ['jest-glamor-react', 'enzyme-to-json/serializer'],
  moduleFileExtensions: ['js', 'jsx'],
  transform: {
    '^.+\\.jsx?$': 'babel-jest',
    '\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$':
      '&lt;rootDir&gt;/config/jest/assetsTransformer.js',
  },
};
</code></pre>
<p><code>jest.setup.js</code></p>
<pre><code>import 'raf/polyfill';
import Enzyme from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

Enzyme.configure({ adapter: new Adapter() });
</code></pre>
<p>Hope that helps someone.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-340917152">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I was having issues with a <code>svg</code> file. I realized I could mock it with <code>identity-obj-proxy</code>:</p>
<pre><code>    "moduleNameMapper": {
      "\\.(css|scss|svg)$": "identity-obj-proxy"
    },
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
    
  <div id="issuecomment-341384494">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>For anyone looking into this issue <a href="https://github.com/timgivois" target="_blank">@timgivois</a> way works beautifully for me. You have to do install <code>npm install --save-dev identity-obj-proxy</code> to get the necessary dependencies.</p>
<pre><code>  "jest": {
    "moduleNameMapper": {
      ".+\\.(css|styl|less|sass|scss|png|jpg|ttf|woff|woff2)$": "identity-obj-proxy"
    }
  }
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
    
  <div id="issuecomment-344750178">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>While the solution by <a href="https://github.com/mbaranovski" target="_blank">@mbaranovski</a> works, I don't know if his intention was to use it as a transformer. It produces the following output (pay attention to the src attribute):</p>
<p><code>&lt;img alt="ImgName" height="28" src={ Object { "process": [Function], } } width="112" /&gt;</code></p>
<p>Essentially, it is mapping everything from that module to the place where I required an SVG. Thus, you could get away with that module simply being:</p>
<p><code>module.exports = {}</code></p>
<p>The other work-around as stated above is to use identity-obj-proxy.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-362261679">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/ashishjan" target="_blank">ashishjan</a>
  

    </strong>

    commented

    <a href="#issuecomment-362261679" target="_blank"><relative-time>on Feb 1</relative-time></a>


      
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

          <p><a href="https://github.com/magnusart" target="_blank">@magnusart</a></p>
<pre><code>"jest": {
    "moduleNameMapper": {
      ".+\\.(css|styl|less|sass|scss|png|jpg|ttf|woff|woff2)$": "identity-obj-proxy"
    }
  }
</code></pre>
<p>it saves my day. Thanks!!.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  





</div>

  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-363103646">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/mbaranovski" target="_blank">@mbaranovski</a> It worked just fine when I ran only jest for test. Sadly when I try to run through the react-scripts from create-react-app I get</p>
<p><code>Out of the box, Create React App only supports overriding these Jest options</code></p>
<p>Is there a workaround for this ? Or the only solution is to eject create-react-app?</p>
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
    
  <div id="issuecomment-363118174">

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/SimenB" target="_blank">SimenB</a>
  

    </strong>

    commented

    <a href="#issuecomment-363118174" target="_blank"><relative-time>on Feb 5</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I don't think CRA supports that option. I'm not sure why it wants to close down options, probably a good reason <g-emoji>🙂</g-emoji></p>
<p>/cc <a href="https://github.com/gaearon" target="_blank">@gaearon</a></p>
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
    
  <div id="issuecomment-369040789">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/eddyerburgh" target="_blank">eddyerburgh</a>
  

    </strong>

    commented

    <a href="#issuecomment-369040789" target="_blank"><relative-time>on Feb 28</relative-time></a>


  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Another workaround:</p>
<pre><code>npm i --save-dev jest-transform-stub
</code></pre>
<pre><code>"jest": {
  "transform": {
    ".+\\.(css|styl|less|sass|scss|png|jpg|ttf|woff|woff2)$": "jest-transform-stub"
  }
}
</code></pre>
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
  <h3 id="ref-commit-9cd9ff4">
    
      
    
    
  <a href="/yukihirop" target="_blank">yukihirop</a> 


      added a commit
        to yukihirop/onepage
      that referenced
      this issue

    <a href="#ref-commit-9cd9ff4" target="_blank">
      <relative-time>on Mar 3</relative-time>
    </a>
  </h3>

  
</div>

  <div>
        <h3 id="ref-pullrequest-317858630">
      
        
      
        
  <a href="/jedmao" target="_blank">jedmao</a>
  

      referenced this issue
        in <strong>react-navigation/react-navigation</strong>
      <a href="#ref-pullrequest-317858630" target="_blank">
        <relative-time>11 days ago</relative-time>
      </a>
    </h3>

  
    
        
      Merged
    



    
      <h4>
        <a href="/react-navigation/react-navigation/pull/4066" target="_blank">
          Fix "npm test" on Windows 10
          #4066
        </a>
      </h4>
    

    


  

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
    
  
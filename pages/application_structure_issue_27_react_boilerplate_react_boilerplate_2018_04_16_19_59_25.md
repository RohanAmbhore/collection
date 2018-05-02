<a href="https://github.com/react-boilerplate/react-boilerplate/issues/27">https://github.com/react-boilerplate/react-boilerplate/issues/27</a><div id="articleHeader"><h1>              Application Structure            #27    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/mxstbr" target="_blank">mxstbr</a>  opened this Issue
        <relative-time>on Dec 18, 2015</relative-time>
        · 75 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-122825214">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Changing the application structure might be worth thinking about, right now the thing might seem quite bloated and randomly thrown together for newcomers.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  


          

          

  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-165755980">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Maybe we should have a folder called <code>app</code>, which is the folder you write your application in and only contains the application files and folders, and a folder <code>config</code> (or <code>webpack</code>?) for all the webpack stuff. This would allow us to tell developers to simply write their application in the <code>app</code> folder and write tests in the <code>test</code> folder and don't care about the rest. (should the <code>test</code> folder be inside the <code>app</code> folder?)</p>
<p>The structure of the boilerplate would then be as follows:</p>
<pre><code>app/
|   js/
|   css/
|   img/    &lt;--- maybe rename this to "assets"
|   .htaccess
|   index.html
|   manifest.json
|   serviceworker.js
config/    &lt;--- maybe this should be called "webpack"
|   makewebpackconfig.js
|   server.js
|   webpack.dev.config.js
|   webpack.prod.config.js
docs/
|   COMMANDS.md
|   FILES.md
|   README.md
|   moretocomehere
test/    &lt;--- maybe rename this to "tests"
|   reducers/
|   actions/
.babelrc
.eslintignore
.eslintrc
.gitattributes
.gitignore
LICENSE.md
README.md
package.json
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
      <div>
  <h3 id="event-495745197">

    
      
    

    

        
  <a href="/mxstbr" target="_blank">mxstbr</a>
  


      
changed the title from
Moving all files possible to src folder
to
Application Structure


    <a href="#event-495745197" target="_blank"><relative-time>on Dec 18, 2015</relative-time></a>

  </h3>
</div>





  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-165858759">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I believe having the <code>test</code> (<code>tests</code>) folder inside the <code>app</code> folder makes sense. That way the separation of code-the-user-has-to-write and tooling is complete, and we can tell users they should only care about the <code>app</code> folder and let the boilerplate handle the rest.</p>
<p>The more I think about this structure, the more I like it. It makes using this boilerplate much easier and newcomer friendly. The structure would look like this:</p>
<pre><code>app/
|   js/
|   css/
|   img/    &lt;--- maybe rename this to "assets"
|   test/    &lt;--- maybe rename this to "tests"
|   |   reducers/
|   |   actions/
|   .htaccess
|   index.html
|   manifest.json
|   serviceworker.js
config/    &lt;--- maybe this should be called "webpack"
|   makewebpackconfig.js
|   server.js
|   webpack.dev.config.js
|   webpack.prod.config.js
docs/
|   COMMANDS.md
|   FILES.md
|   README.md
|   moretocomehere
.babelrc
.eslintignore
.eslintrc
.gitattributes
.gitignore
LICENSE.md
README.md
package.json
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-165866562">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Maybe <code>config</code> is the wrong name for the folder with boilerplate things. That might lead devs to think that they can configure their application in there, which the can't.</p>
<p>Maybe <code>tooling</code> is a better name? I don't want to call it <code>webpack</code>, because there might be other config we want to put somewhere later on.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-166370342">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I think calling it <code>webpack</code> is a good idea because it's very clear. <code>tooling</code> is somewhat ambiguous. You can always change the name later.</p>
<p><code>img</code> should probably be changed to assets, yeah, because you could add webfonts, etc. that way.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-166371404">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Also, I don't think tests should go inside app. They aren't the "app", technically... nothing there would transpile to the final build. A separate tests folder is fine... it's also probably more visible.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-166729807">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Good points. I've implemented this in the <a href="https://github.com/mxstbr/react-boilerplate/tree/v3.0.0" target="_blank">v3.0.0 branch</a>, check it out and report any problems you come across!</p>
<p>EDIT: Going to update the docs/FILES.md file soon.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-166822109">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Looks pretty good!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167371441">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>You could consider bundling the actions, constants and reducers into <em>redux modules</em> and create reducer bundles according to the <a href="https://github.com/erikras/ducks-modular-redux" target="_blank">"ducks" approach</a>.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167404500">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>As discussed in <a href="https://github.com/react-boilerplate/react-boilerplate/issues/33" target="_blank">#33</a>, having a folder for "smart" components and one for "dumb" components makes a lot of sense. The question is where do pages fit in?</p>
<p>I currently feel like this would be optimal - any other ideas?</p>
<pre><code>app/
|--- js/
    |--- containers/    &lt;--- stateful components
         |--- pages/
    |--- components/ &lt;--- stateless components
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167404508">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/hampusohlsson" target="_blank">@hampusohlsson</a> thanks for the link, I'll look into it!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167440290">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>You can probably put it in a subfolder if you need it. However, my (rather limited) experience with this structure is that page components end up being the only smart ones in the entire app, so you can just keep them under <code>containers</code> to remove the extra level</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167484890">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/philihp" target="_blank">philihp</a>
  

    </strong>

    commented

    <a href="#issuecomment-167484890" target="_blank"><relative-time>on Dec 28, 2015</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I would actually be in favor of putting css and javascript. For example:</p>
<pre><code>app/
    components/
               clicker.js
               clicker.css
               switcher.js
               switcher.css
</code></pre>
<p><code>clicker.css</code> is so intimately related to <code>clicker.js</code> that changes to one made by someone new to the codebase should probably want to check out the other file.</p>
<p>Since your build is a webpack bundle, it would also be cool to do this with tests as well. That would alleviate the need to have a <code>tests/</code> folder that tries to mirror the structure. Most projects don't do this because they transpile the <code>src/</code> folder, and you don't want that to include tests. Webpack is smarter about this.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167496809">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm considering switching to this layout, as it makes a lot of sense for bigger applications. No <code>tests/</code> and no <code>css/</code> folders anymore:</p>
<pre><code>app/
|- assets/
|- js/
|  |- components/
|    |- NavBar/
|      |- NavBar.react.js
|      |- NavBar.css
|      |- NavBar.test.js
|    |- Button/
|      |- Button.react.js
|      |- Button.css
|      |- Button.test.js
|  |- containers/
|    |- HomePage/
|      |- HomePage.react.js
|      |- HomePage.css
|      |- HomePage.test.js
|- .htaccess
|- index.html
|- manifest.json
|- serviceworker.js
</code></pre>
<p>With CSS Modules importing the CSS files of each component in the <code>.react.js</code> file. Webpack's <code>css-loader</code> (which we use anyway) has support for CSS modules, so it wouldn't be hard to switch.</p>
<p>Where do vendor CSS files and global CSS files (e.g. <code>variables.css</code>, <code>typography.css</code>,...) now fit in?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167496962">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>in that case - 'js' is not a good name for the parent folder <g-emoji>😄</g-emoji><br />
Also - why not 'jsx' extensions for files containing jsx? Looks nicer than '.react.js'.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167497186">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>True - any ideas for a better name for the parent folder?</p>
<p>To be honest, I can't remember why I adopted that naming. Submitted a new issue for this, see <a href="https://github.com/react-boilerplate/react-boilerplate/issues/50" target="_blank">#50</a></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167529358">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>This is my project structure. Hopes it helps.<br />
Whenever you see a file with <code>.dev.</code> in its name you know I alternate dev/production version of this file using NormalModuleReplacementPlugin.</p>
<pre><code>.
├── build (bundled files for production server)
├── lib
│   └── dev_server.js
├── package.json
├── src
│   ├── fonts (I like to provide everything from my server since it's better for on-premise installations)
│   ├── images
│   │   ├── app_logo.png
│   │  └── favicon.ico
│   ├── js
│   │   ├── api (server communication. 
│   │   │   ├── MOCK_DATA.js
│   │   │   ├── WebApi.dev.js (NormalModuleReplacementPlugin loads this on dev build - so I can get mock data for my "server calls"
│   │   │   └── WebApi.js
│   │   ├── constants
│   │   │   └── AppConstants.js
│   │   ├── core (wraps the state object)
│   │   │   ├── consts.js
│   │   │   └── core.js
│   │   ├── react
│   │   │   ├── components
│   │   │   │   ├── DateSpan.jsx
│   │   │   │   └── VisibilityFilter.jsx
│   │   │   ├── containers
│   │   │   │   ├── App.jsx (using Root helps keeping the App clean)
│   │   │   │   ├── DevTools.jsx
│   │   │   │   ├── Root.dev.jsx (split to dev and prod for different redux store initialization)
│   │   │   │   ├── Root.jsx
│   │   │   │   └── GalleryPage.jsx
│   │   │   ├── helpers
│   │   │   │   ├── canvas.js
│   │   │   │   └── state.js
│   │   │   └── main.jsx (entry point)
│   │   ├── redux
│   │   │   ├── actions
│   │   │   ├── constants.js
│   │   │   ├── helpers
│   │   │   │   └── create_reducer.js
│   │   │   ├── middleware
│   │   │   ├── persistence
│   │   │   ├── reducers
│   │   │   └── store
│   │   │       ├── configureStore.dev.js
│   │   │       └── configureStore.js
│   │   ├── routing
│   │   │   ├── constants.dev.js
│   │   │   ├── constants.js
│   │   │   ├── history.js
│   │   │   └── utils.js
│   │   └── utils
│   │       ├── JsonUtils.js
│   │       └── interval.js
│   ├── styles
│   └── templates
│       └── main_template.html
├── test
└── webpack.config.js


</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167564804">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>As image assets also are part of the "source", I usually make one directory called <code>src</code> that contains everything that will be processed by webpack. This is my own preference, but I like to name the js-files inside the components just <code>index.js</code> because that allows you to do something like this from another component:</p>
<div><pre>// Importing a button from the IndexPage would look like this
import Button from '../../components/Button' </pre></div>
<p>and inside Button/index.js you would import the styles</p>
<div><pre>// Include the styles
import styles from './style.scss' </pre></div>
<p>Images would obvioulsy have to be imported from the assets folder</p>
<div><pre>import Icon from '../../assets/images/icon.png'</pre></div>
<p>Here's an example of how I've structured one project (a bunch of stuff omitted for brevity)</p>
<pre><code>├── dist
│   ├── css &lt;-- webpack extracted css goes here
│   ├── img &lt;-- webpack processed images goes here
│   └── js &lt;-- webpack compiled js goes here
└── src
    ├── assets
    │   ├── images
    │   └── scss &lt;-- global css such as vendor, variables and typography
    ├── components
    │   ├── Button
    │   │   ├── index.js
    │   │   └── style.scss
    │   └── Table
    ├── containers
    │   └── IndexPage
    └── redux &lt;-- ducks goes in here
</code></pre>
<p>In the same manner, it would make a lot of sense to just add a file called <code>test.js</code> for every component. This way, we create a standardized way of how every component should look while keeping it simple. The name of the component is the folder name, which contains an <code>index.js</code> file, a <code>style.css</code> and a <code>test.js</code> file.</p>
<p>Re the global css; right now I'm combining the scss files that contains overall layout, variables and typography into one scss file called <code>base.scss</code> which I'm requiring in the file where I define my routes.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167584085">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/zavelevsky" target="_blank">@zavelevsky</a> that's very helpful, thanks! What do the <code>constants.js</code> in the <code>routing</code> folder do?</p>
<p><a href="https://github.com/hampusohlsson" target="_blank">@hampusohlsson</a> We have the <code>app/</code> folder, which is like your <code>src/</code> folder, and the <code>build/</code> folder, which is like your <code>dist/</code> folder. <g-emoji>👍</g-emoji><br />
I've thought about doing the <code>index.js</code> thing, but it's non-obvious for beginners that it gets exported by default. We have a lot of magic happening already, so I'd rather leave it as it is for now.<br />
I agree with the tests next to the components, that sounds good! It's dependent on <a href="https://github.com/react-boilerplate/react-boilerplate/issues/11" target="_blank">#11</a> though, I have yet to find a nice way to unit test components... (<a href="https://github.com/philihp" target="_blank">@philihp</a> <a href="https://twitter.com/philihp/status/681337757814267904" target="_blank">pinged me</a> on twitter about <a href="https://github.com/airbnb/enzyme" target="_blank">airbnb/enzyme</a> which looks really nice. I hope he tries implementing it!)</p>
<p>This is what I'm currently looking at:</p>
<pre><code>app/
|- assets/
|  |- img/
|  |- fonts/
|- css/    &lt;--- Global CSS stuff, variables, mixins etc.
|  |- vendor/
|  |- utils/
|  |- main.css    &lt;--- Main CSS file that imports everything
|- js/
|  |- actions/
|    |- AppActions.js    &lt;--- Global Actions
|  |- constants/
|    |- AppConstants.js/    &lt;--- Global Constants
|  |- components/    &lt;--- Stateless components
|    |- NavBar/
|      |- NavBar.react.js     |
|      |- NavBar.css          | &lt;--- Each stateless component has a .css file, a .js file and a .test.js file
|      |- NavBar.test.js      |
|    |- Button/
|      |- Button.react.js
|      |- Button.css
|      |- Button.test.js
|  |- containers/    &lt;--- Stateful components
|    |- HomePage/
|      |- HomePage.react.js           |
|      |- HomePage.css                |      
|      |- HomePage.test.js            | &lt;--- Each stateful component has the same files as the stateless ones
|      |- HomePageActions.js          |      and some actions, some constants and a reducer
|      |- HomePageConstants.js/       |       
|      |- HomePageReducer.js          |
|  |- reducers/
|    |- RootReducer.js    &lt;--- Global Reducer
|- .htaccess
|- index.html
|- manifest.json
|- serviceworker.js
</code></pre>
<p>Still not sure what to rename the <code>js/</code> folder to. Maybe <code>react/</code> or <code>redux/</code>? Whats the best name, for both advanced developers who know whats going on and beginners who have no idea?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167590234">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/mxstbr" target="_blank">@mxstbr</a> did not know about enzyme, looks good!</p>
<p>Regarding the renaming of the folder, I think it is hard to satisfy all developers, but I would not recommend using <code>redux</code>. There is another boilerplate <a href="https://github.com/erikras/react-redux-universal-hot-example" target="_blank">erikras/react-redux-universal-hot-example</a>, which uses <code>redux</code> for the ducks. As your project is gaining traction (congrats!) you have the opportunity to influence the recommended way of building redux apps. Especially for newcomers that might have seen the other repo, I think it would be a good idea to not mix it up too much as it will be confusing.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167636788">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>A few thoughts later:</p>
<pre><code>app/
|- assets/
|  |- img/
|  |- fonts/
|- global/    &lt;--- Can also put global actions/reducers/... in here as well
|  |- css/
|     |- vendor/
|     |- utils/
|     |- main.css
|- components/
|  |- NavBar/
|     |- NavBar.react.js
|     |- NavBar.css
|     |- NavBar.test.js
|  |- Button/
|     |- Button.react.js
|     |- Button.css
|     |- Button.test.js
|- containers/
|  |- HomePage/
|     |- HomePage.react.js
|     |- HomePage.css
|     |- HomePage.test.js
|     |- HomePageActions.js
|     |- HomePageConstants.js    
|     |- HomePageReducer.js
|- .htaccess
|- index.html
|- manifest.json
|- serviceworker.js
</code></pre>
<p>Main changes:</p>
<ul>
<li>No need for separate global actions/reducers/constants folders, lets put all of those plus the global CSS folder in a <code>global/</code> folder.</li>
<li>No need for another wrapping folder around containers and components, those can live comfortably in the root folder</li>
</ul>
<p>This one is much cleaner and smaller, while keeping the functionality fully intact.</p>
<p>The only question remaining for me is, where do we put <code>app.js</code> and <code>rootReducer.js</code>? In the <code>global/</code> folder, hidden behind a wall?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167644132">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I just noticed that <code>pages</code> can be both stateless or stateful. E.g. <code>NotFoundPage</code> and <code>ReadmePage</code> are stateless, while <code>HomePage</code> is stateful. Maybe we do need a seperate folder for pages? I'd like to keep them together if possible.</p>
<p>EDIT: Also, we should add a <code>tests</code> folder to the container folders, otherwise you end up with way too many files in there. An example stateful component, <code>HomePage</code>, would thus look like this:</p>
<pre><code>HomePage/
|- HomePage.react.js
|- HomePage.css
|- HomePageActions.js
|- HomePageConstants.js
|- HomePageReducer.js
|- tests/
|  |- HomePageActions.test.js
|  |- HomePageReducer.test.js
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167649671">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I've switched the <code>v3.0.0</code> branch of this repo to the above application structure and made it work. Have a look (or simply read through the comments above) and tell me what you think!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167782820">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Hey <a href="https://github.com/mxstbr" target="_blank">@mxstbr</a>, some first impression feedback on your structure. What is the reasoning behind having the HomePage{action,constants,reducers} together with the component (btw, using the ducks approach you would combine everything in one file)? What if you want to dispatch a common action that lives in the HomePage folder from another component, then you would have to either duplicate the actions or remember which component has the actions and include that.. feels a bit dirty <g-emoji>😛</g-emoji></p>
<p>Also, I would not put the redux root-reducer in the same folder as the css (why not put the css folder inside assets :) images are "global" too in a sense, as they can be included from anywhere).</p>
<p>A suggestion is to rename <code>global</code> to something that contains all reducer stuff such as <code>reducers/ducks/redux</code>, and move the css to assets.</p>
<pre><code>├── assets
│   ├── images
│   ├── fonts
│   └── css
│       ├── vendor
│       ├── utils
│       └── main.css
├── components
├── containers
└── reducers
    ├── HomePage
    │   ├── HomePage.js
    │   └── HomePage.test.js
    └── index.js &lt;-- root reducer
</code></pre>
<p>In this case your root reducer could look something like this</p>
<div><pre>import { combineReducers } from 'redux';
import { routeReducer } from 'redux-simple-router';

// Custom reducers
import HomePageReducer from './HomePage/HomePage';

// Combine all into one
export default combineReducers({
    HomePage: HomePageReducer,
    routing: routeReducer
});

// Expose individual reducers
export const HomePage = HomePageReducer;</pre></div>
<p>This would allow you to use the following imports</p>
<div><pre>// Import HomePage reducers
import { HomePage } from '../reducers'

// Import the root reducers
import RootReducer from '../reducers'</pre></div>
<p>I know you are not too fond of naming files <code>index.js</code> in favor of easy to understand for newbies ;) But it is a very common pattern when doing module development in Node.js, so why not utilize the feature and add it to repo documentation instead.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167794607">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/hampusohlsson" target="_blank">@hampusohlsson</a> thanks so much for checking it out and posting this amazing feedback!</p>
<hr />
<p>You're right about, I'm not fond of the <code>global/</code> folder either so I'm going to remove it and simply not have any global CSS. (See the discussion in <a href="https://github.com/react-boilerplate/react-boilerplate/issues/32" target="_blank">#32</a>) Not entirely sure where to put <code>normalize.css</code> yet...</p>
<p>I agree that the root reducers shouldn't be there either, I'm just going to put it in the root next to the <code>app.js</code> I think.</p>
<hr />
<p>The reasoning behind having the {actions,reducers,constants} in the same folder as the component:</p>
<p>Imagine you have a <code>NavBar</code>, that has an action <code>openNav</code> and an action <code>closeNav</code>. (with the corresponding constants) In the <code>HomePage</code>, you'd then do the following:</p>
<div><pre>import { openNav, closeNav } from '../NavBar/NavBarActions.js';</pre></div>
<p>Now you can open and close the NavBar from the HomePage! Which (in my mind) makes a lot of sense. The <code>openNav</code> does something with <code>NavBar</code>, so the action should be there.</p>
<p>I'm not sure one should ever have global actions. Do you have an example of an action that doesn't belong to a specific component?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167796284">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/mxstbr" target="_blank">@mxstbr</a> in your case, I agree it makes sense to put the navbar specific actions together with the <code>NavBar</code> component!</p>
<p>An example I'm thinking of is where you need to fetch/update a bunch of data from the server, e.g. populating a list of users. This list of users could be rendered in multiple components, and actions taken on that list from multiple places. Not sure where that kind of functionality should go.</p>
<p>Perhaps it is the same discussion as with global css <g-emoji>😛</g-emoji>  99% of the time we're going to end up having everything local alongside the component, but then you have a couple of edge cases where you need something to be available globally.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167796821">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I strongly advise against mixing redux actions with components. You should<br />
completely separate them. Passing action creators via props enables you to<br />
put as many abstractions as you'd like between actions and what the<br />
component sees as callbacks. Actions can be called by different components,<br />
e.g. a refresh action can be called by clicking a button or dispatched by<br />
another action.<br />
On Dec 29, 2015 3:53 PM, "Max Stoiber" <a href="mailto:notifications@github.com" target="_blank">notifications@github.com</a> wrote:</p>
<blockquote>
<p><a href="https://github.com/hampusohlsson" target="_blank">@hampusohlsson</a> <a href="https://github.com/hampusohlsson" target="_blank">https://github.com/hampusohlsson</a> thanks so much for</p>
<h2>checking it out and posting this amazing feedback!</h2>
<p>You're right about, I'm not fond of the global/ folder either so I'm<br />
going to remove it and simply not have any global CSS. (See the discussion<br />
in <a href="https://github.com/react-boilerplate/react-boilerplate/issues/32" target="_blank">#32</a> <a href="https://github.com/react-boilerplate/react-boilerplate/issues/32" target="_blank">mxstbr#32</a>) Not<br />
entirely sure where to put normalize.css yet...</p>
<p>I agree that the root reducers shouldn't be there either, I'm just going</p>
<h2>to put it in the root next to the app.js I think.</h2>
<p>The reasoning behind having the {actions,reducers,constants} in the same<br />
folder as the component:</p>
<p>Imagine you have a NavBar, that has an action openNav and an action<br />
closeNav. (with the corresponding constants) In the HomePage, you'd then<br />
do the following:</p>
<p>import { openNav, closeNav } from '../NavBar/NavBarActions.js';</p>
<p>Now you can open and close the NavBar from the HomePage! Which (in my<br />
mind) makes a lot of sense. The openNav does something with NavBar, so<br />
the action should be there.</p>
<p>I'm not sure one should ever have global actions. Do you have an example<br />
of an action that doesn't belong to a specific component?</p>
<p>—<br />
Reply to this email directly or view it on GitHub<br />
<a href="https://github.com/react-boilerplate/react-boilerplate/issues/27#issuecomment-167794607" target="_blank">mxstbr#27 (comment)</a><br />
.</p>
</blockquote>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167833352">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/zavelevsky" target="_blank">@zavelevsky</a> interesting, I don't fully agree though. (to be clear, I'm unhappy with the current <code>v3.0.0</code> structure as well)</p>
<p>As shown above, you can easily import a <code>NavBar</code> action from somewhere else, and contextually it makes more sense for actions that influence a component to be directly next to said component.</p>
<p>The problem of global actions/reducers/..., like the very common data-fetching pattern, still persists. Maybe we could rename the current <a href="https://github.com/mxstbr/react-boilerplate/tree/v3.0.0/app/containers/App" target="_blank"><code>App</code> container</a> to <code>Wrapper</code> (or something like that), have it not render anything at all except <code>{ this.props.children }</code>, and be responsible for global stuff like fetching data and global styles?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167835524">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Additional arguments against placing actions with components :</p>
<ul>
<li>forces a bottom-up way of thinking when designing your application -<br />
while redux encourages you to first think of your state and the things that<br />
modify it and then start creating components (top down). You can use TDD<br />
and fully cover your redux parts with unit tests before even writing a<br />
single component.</li>
<li>you couple components and actions, or at least use a structure that<br />
encourages it.</li>
<li>props exist for a reason. They are your means to provide data and<br />
functionality to your components in a way that doesn't make any assumptions<br />
regarding how you manage your state. A component expects a callback. You<br />
determine the concrete implementation of this callback elsewhere.
<ul>
<li>action creators belong together. They are aware of each other's<br />
implementation and aware of state. They are redux entities. They serve as<br />
the interface of the state and as its concrete implementation. Therefore<br />
they shouldn't be scattered with components.<br />
On Dec 29, 2015 7:16 PM, "Max Stoiber" <a href="mailto:notifications@github.com" target="_blank">notifications@github.com</a> wrote:</li>
</ul>
</li>
</ul>
<blockquote>
<p><a href="https://github.com/zavelevsky" target="_blank">@zavelevsky</a> <a href="https://github.com/zavelevsky" target="_blank">https://github.com/zavelevsky</a> interesting, I don't fully<br />
agree though. (to be clear, I'm unhappy with the current v3.0.0 structure<br />
as well)</p>
<p>As shown above, you can easily import a NavBar action from somewhere<br />
else, and contextually it makes more sense for actions that influence a<br />
component to be directly next to said component.</p>
<p>The problem of global actions/reducers/..., like the very common<br />
data-fetching pattern, still persists. Maybe we could rename the current<br />
App container<br />
<a href="https://github.com/mxstbr/react-boilerplate/tree/v3.0.0/app/containers/App" target="_blank">https://github.com/mxstbr/react-boilerplate/tree/v3.0.0/app/containers/App</a><br />
to Wrapper (or something like that), have it not render anything at all<br />
except { this.props.children }, and be responsible for global stuff like<br />
fetching data and global styles?</p>
<p>—<br />
Reply to this email directly or view it on GitHub<br />
<a href="https://github.com/react-boilerplate/react-boilerplate/issues/27#issuecomment-167833352" target="_blank">mxstbr#27 (comment)</a><br />
.</p>
</blockquote>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167971870">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/zavelevsky" target="_blank">@zavelevsky</a> thanks for pointing our the difference, did not think about top-down vs bottom-up approach before. Top down is what makes sense to me, keeping all state management code together.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-167987574">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I started out with a containers and dumb components approach but it didn't scale well as kept adding more and more routes and subroutes. My dumb components folder grew too much that it takes a few seconds for me find what I want. I think the approach proposed by <a href="https://github.com/ryanflorence" target="_blank">@ryanflorence</a> <a href="https://gist.github.com/ryanflorence/daafb1e3cb8ad740b346/" target="_blank">https://gist.github.com/ryanflorence/daafb1e3cb8ad740b346/</a> works best when you are building a large app.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>


  

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-169672812">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Hey guys, i'd like to share an application structure i've created and working with for a while. I found it very scalable and simple to understand.</p>
<p>I'm using <a href="https://github.com/css-modules/css-modules" target="_blank">css-modules</a>, so i can keep component's styles in the same directory as component's logic is (the same is for components tesing).</p>
<p><code>Units</code> folder is used for simple components like Article, Post, Comment etc.<br />
<code>Catalogs</code> simply wraps Units in array and have some logic like 'load more' buttons.<br />
<code>Pages</code> (or Screens, or Views) are routes for react-router and containers for redux (you can see there is no index.css files nearby). Also they can contain additional directory <code>_</code>, which contains specific components for certain page.<br />
<code>Modules</code> are reusable and complex components (like popups, headers, chats etc), which can also be redux containers and contain <code>_</code> directory for simplifing component's markup.</p>
<pre><code>├── README.md
├── app
│   ├── actions
│   │   ├── __tests__
│   │   │   └── appActions.spec.js
│   │   ├── appActions.js
│   ├── components
│   │   ├── App.js
│   │   ├── Catalogs
│   │   │   ├── NewsList
│   │   │   │   ├── index.css
│   │   │   │   ├── index.spec.js
│   │   │   │   └── index.js
│   │   │   └── index.js
│   │   ├── Base
│   │   │   ├── Button
│   │   │   │   ├── index.css
│   │   │   │   ├── index.spec.js
│   │   │   │   └── index.js
│   │   │   └── index.js
│   │   ├── Modules
│   │   │   ├── Footer
│   │   │   │   ├── index.css
│   │   │   │   ├── index.spec.js
│   │   │   │   └── index.js
│   │   │   └── index.js
│   │   ├── Pages
│   │   │   ├── AboutPage
│   │   │   │   ├── _
│   │   │   │   │  ├── AboutPageHeader
│   │   │   │   │   │   ├── index.css
│   │   │   │   │   │   ├── index.spec.js
│   │   │   │   │   │   └── index.js
│   │   │   │   └── index.js
│   │   ├── Units
│   │   │   ├── NewsUnit
│   │   │   │   ├── index.css
│   │   │   │   ├── index.spec.js
│   │   │   │   └── index.js
│   ├── constants
│   │   ├── actionTypes.js
│   │   ├── apiEndpoints.js
│   └── reducers
│       ├── __tests__
│       │   └── news.spec.js
│       └── news.js
├── client
│   └── index.js
├── config
│   ├── root.css
│   └── routes.js
├── index.js
├── karma.conf.js
├── package.json
├── public
│   ├── favicon-16x16.png
│   └── manifest.json
├── server
│   ├── index.js
├── utils
└── webpack
</code></pre>
<p>I reduced project's tree a lot, but i think it's clear to understand the base concept.<br />
Hope, it will help.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-169701898">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>@canvaskisa thanks for sharing, I have not seen this split between <code>Units</code>, <code>Catalogs</code>, <code>Pages</code> and <code>Modules</code> before, very interesting!</p>
<p>What exactly are the benefits of this classification? It seems a bit... wobbly, for the lack of a better word. (In the sense that it seems hard to draw an exact line between <code>Catalogs</code> and <code>Modules</code> and, to some extent probably, <code>Units</code>)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-169725666">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/mxstbr" target="_blank">@mxstbr</a> Currently i'm working on media apps, and this structure simplifies development lot, in my experience. Of course you can remove such concepts as <code>Catalogs</code> or <code>Units</code>, if there are not much of them in your app, and create something similar.</p>
<p>The main concept is to beware flat structure of your components, categorize them with reusable components (<code>Catalogs</code>, <code>Units</code>) and split into smaller modules (<code>_</code> directories). This categorization together with setting <code>NODE_PATH</code>, provides clear imports like:</p>
<div><pre>import { Footer } from 'Modules'; </pre></div>
<p>Also i'd like to add, that i don't think moving stateful components to containers folder is a good idea. It makes directory structure flat, which is bad, in my opinion.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-169733667">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>@canvaskisa interesting! How do you get those clear imports, did you use <code>resolve.modulesDirectories</code> in the webpack config?</p>
<p>Why do you believe a flat directory structure is inherently bad?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-169741917">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/mxstbr" target="_blank">@mxstbr</a> Yeah, <code>resolve.modulesDirectories: ['node_modules', 'components']</code> will do all the work, additionally you can set aliases for actions, reducers, etc like this:</p>
<pre><code>resolve: {
    alias: {
      constants: path.resolve(__dirname, '..', 'app', 'constants'),
      actions: path.resolve(__dirname, '..', 'app', 'actions'),
      reducers: path.resolve(__dirname, '..', 'app', 'reducers')
    }
}
</code></pre>
<p>On the server setting <code>NODE_PATH=.:app:app/components</code> will do the same.</p>
<p>Flat directory structure is ok, but only for small apps. When an app is getting bigger, it's a pain to maintain it with flat structure.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-172734796">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm new to this project, so I may be missing something obvious. However I'd like to suggest merging <code>app/components</code> and <code>app/containers</code>. Are they really so different to need such separation?</p>
<pre><code>app
├── assets
├── components      # React components
│   ├── Button
│   │   ├── Button.css
│   │   ├── Button.react.js
│   │   └── Button.test.js
│   ├── NavBar      # ...with component-sepecific actions, e.g. openNav, closeNav...
│   │   ├── NavBar.css
│   │   ├── NavBar.react.js
│   │   ├── NavBar.actions.js
│   │   ├── NavBar.constants.js
│   │   └── test
│   │       ├── NavBar.test.js
│   │       ├── NavBar.actions.test.js
│   │       └── NavBar.reducer.test.js
│   └── HomePage    # ...or without actions
│       ├── HomePage.css
│       ├── HomePage.test.js
│       └── HomePage.react.js
├── global          # Global a/c/r for data fetching and other edge cases
│   ├── global.actions.js
│   ├── global.constants.js
│   └── global.reducer.js
├── rootReducer.js
├── app.js
├── index.html
├── manifest.json
└── serviceworker.js
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-172786756">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ravinggenius" target="_blank">@ravinggenius</a> The problem is that you need some sort of separation between components. If you're building a big application, some day you'll have hundreds of components and having them all in one folder is a pain.</p>
<p>I like the <code>components</code> and <code>containers</code> structure, but it might not be enough. It forces you to think about which components have state and which ones don't, something you think about anyway. It still doesn't scale very well though, and I'm becoming a bigger and bigger fan of <a href="https://gist.github.com/ryanflorence/daafb1e3cb8ad740b346" target="_blank">Ryan's approach</a> with the nested structure, and it might work fine for small apps. Does anybody have experience building an app like that?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-172794898">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/okonet" target="_blank">okonet</a>
  

    </strong>

    commented

    <a href="#issuecomment-172794898" target="_blank"><relative-time>on Jan 19, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I didn't read it carefully so I might miss something but it seems this thread is mostly concerned about JS and not taking in account CSS and images.</p>
<p>I'm  strongly against putting CSS and <code>assets</code> apart from the JS code. The whole point of using PostCSS and CSS-modules is to write components — a dedicated blocks of code which will result in a component look & feel. To make things easy for mainatnace you should always put your assets to the appropriate components. Even if the component doesn't have JS implementation, you should put it into a sub-dir and just require your CSS in the <code>index.js</code>.</p>
<p>Take a look at BEM: <a href="https://en.bem.info/method/filesystem/" target="_blank">https://en.bem.info/method/filesystem/</a> — this is the idea behind CSS-modules.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-172795913">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Yeah, CSS will be next to the JS files. Take a look at the <a href="https://github.com/mxstbr/react-boilerplate/tree/v3.0.0" target="_blank"><code>v3.0.0</code> branch</a> – this is already implemented.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-172800440">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/okonet" target="_blank">okonet</a>
  

    </strong>

    commented

    <a href="#issuecomment-172800440" target="_blank"><relative-time>on Jan 19, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Yes, I saw that and that's cool. But what about non-CSS assets? You still have <code>assets</code> directory, which is bad IMO since it's completely disconnected from the source there these assets are being used. <em>All</em> assets (CSS, images, fonts etc.) should be in the component directory IMO. This the idea of BEM — put all related stuff together. Also this makes requiring images in CSS easy: <code>url("./myImg.png")</code></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-172803227">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I didn't think about images at all, but that makes sense. <g-emoji>👍</g-emoji></p>
<hr />
<p>I also think <a href="https://github.com/CrocoDillon" target="_blank">@CrocoDillon</a> and <a href="https://github.com/hampusohlsson" target="_blank">@hampusohlsson</a> were right. I'm not fond of the file-naming anymore:</p>
<pre><code>NavBar
├── NavBar.css
├── NavBar.react.js
├── NavBar.actions.js
└── NavBar.constants.js
</code></pre>
<p>I now much prefer this, as its much nicer to <code>import</code> with:</p>
<pre><code>NavBar
├── styles.css
├── index.js
├── actions.js
└── constants.js
</code></pre>
<p>This means you can just go <code>import NavBar from 'NavBar';</code>, because with the previous structure you'd have to go <code>import NavBar from 'NavBar/NavBar.react';</code> which was really annoying.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    


    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-172806854">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/okonet" target="_blank">okonet</a>
  

    </strong>

    commented

    <a href="#issuecomment-172806854" target="_blank"><relative-time>on Jan 19, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/mxstbr" target="_blank">@mxstbr</a> check <a href="https://github.com/react-boilerplate/react-boilerplate/pull/103" target="_blank">mxstbr#103</a> out</p>
<p>I think verbose file names are good because you'll be looking for stuff in IDE/editor by the name. But to reduce code for imports you could just use <code>index.js</code> file. In case of non-JS components (blocks in terms of BEM) you still could export a JS file with a reuire of CSS (which in turn requires images etc.).</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-172832386">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/okonet" target="_blank">@okonet</a>, I already mentioned the use of <code>index.js</code> as a proxy for nicer imports before, see <a href="https://github.com/react-boilerplate/react-boilerplate/issues/27#issuecomment-168244128" target="_blank">mxstbr#27 (comment)</a></p>
<p>It got overlooked though ;) Whatever the file names are I recommend this approach because you’ll have all exports for a module nicely listed in one small file (<code>index.js</code>).</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-172833205">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Yeah, you were right it is so much nicer to name them <code>index.js</code>. Added credits to comment above, thanks for reminding me!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-172851363">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/mxstbr" target="_blank">@mxstbr</a> glad you have realized the naming benefit of <code>index.js</code> :)</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-173651557">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I put the actual components in the <code>index.js</code> instead of simply exporting them from there (one file less!), have been working with this for the past week on a commercial project and I'm loving it.</p>
<pre><code>app
├── app.js
├── components
│   ├── Button
│   │   ├── Button.test.js
│   │   ├── index.js
│   │   └── styles.css
│   └── Img
│       ├── Img.test.js
│       └── index.js
├── containers
│   ├── App
│   │   ├── index.js
│   │   ├── logo.png
│   │   └── styles.css
│   ├── HomePage
│   │   ├── actions.js
│   │   ├── constants.js
│   │   ├── index.js
│   │   ├── reducer.js
│   │   ├── styles.css
│   │   └── tests
│   │       ├── actions.test.js
│   │       └── reducer.test.js
│   ├── NotFoundPage
│   │   └── index.js
│   └── ReadmePage
│       ├── index.js
│       └── styles.css
├── index.html
├── manifest.json
└── rootReducer.js
</code></pre>
<p>I still consider that in bad editors users won't be able to differentiate between the <code>index.js</code>, <code>actions.js</code> etc. files. Being held back by those few seems like a bad idea. If their editor can't do it, they can still rename them, but I recon enough people use Sublime/Atom/Brackets/... (which all show the path in the tab)</p>
<hr />
<p>Does anybody have comments about the app structure, something they dislike? Otherwise I'll consider this issue resolved & will close it.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-173668864">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/okonet" target="_blank">okonet</a>
  

    </strong>

    commented

    <a href="#issuecomment-173668864" target="_blank"><relative-time>on Jan 22, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/mxstbr" target="_blank">@mxstbr</a> it's not about showing path but about searching for a file. If you know you want to open <code>Button</code> component, you will be typing <code>Button</code> and not <code>index</code>, which will not include your <code>index</code>. So you will have to always type <code>Button/index</code> to open it. I think having one file less in repository isn't worth the pain you'll have every day. This is exactly what <a href="https://github.com/nikgraf" target="_blank">@nikgraf</a> was talking about as well.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-173671094">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/okonet" target="_blank">@okonet</a> Ah you're right, I totally forgot about that, damn. Too many reasons for too many things to keep track of...</p>
<p>Thanks for reminding me, I'll have another think about it!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-173685793">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/okonet" target="_blank">@okonet</a> Vim/Sublime/Atom each can find files via (case-insensitive) fuzzy searches. For instance you can type something like <code>buttinx</code> and be reasonably sure you will find what you're looking for, in this case <code>app/components/Button/index.js</code>. In many cases you can probably get away with typing less.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-173690749">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/nikgraf" target="_blank">nikgraf</a>
  

    </strong>

    commented

    <a href="#issuecomment-173690749" target="_blank"><relative-time>on Jan 22, 2016</relative-time></a>


  </h3>
</div>


    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ravinggenius" target="_blank">@ravinggenius</a> just my personal experience: we always have a couple components with similar names: <code>Trip</code>, <code>TripRow</code>, <code>Trips</code>. So you don't always want to pick the first and it was just my personal perception, but it felt better once we switched to an index.js separated from the component. The index file can be super simple e.g. <code>export default from './TripRow';</code></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-173693817">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I agree with <a href="https://github.com/nikgraf" target="_blank">@nikgraf</a>, especially if you're going with the <a href="https://medium.com/@learnreact/container-components-c0e67432e005" target="_blank">"hardcore" containers</a> there'll be lots of overlap between names.</p>
<p>I just don't think that adding a <code>TripRow.react.js</code> file will fix that, because then you have a <code>TripRow.react.js</code>, a <code>Trip.react.js</code> and a <code>Trips.react.js</code>. That's the same issue as with the <code>index.js</code>, which is that you have to write the full name of what you want, i.e. the question becomes typing <code>Trip.r</code> vs. typing <code>Trip/i</code>.</p>
<p>That doesn't really make a difference, but not having to add an "unnecessary" file each time you create a new component does make a difference, esp. for consistency with multiple devs, so I'm leaning towards the <code>index.js</code>-only-approach.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-174199875">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I've decided to go with the <code>index.js</code> approach, for the reasons listed above. If you feel like that's a mistake, please let me know!</p>
<p>I've been working with the boilerplate (non-<code>index.js</code> version) the last week on a commercial product with lots of components and data handling, and I'm very happy with the current structure, so I'm closing this issue. Thanks for the great discussions and inputs everybody, I'm definitely going to link to this issue in the future!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    


    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-225405399">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Sorry for jumping in late, but as I am starting to understand react-boilerplate, I wanted to suggest an alternate approach to application structure that might be more intuitive.</p>
<p>This is what we currently have: all <em>container</em> components under <code>containers</code> and all <em>presentational</em> (or <em>unconnected</em>) components under <code>components</code>. This is widely known as "folder-by-type" structure. Unfortunately it doesn't scale well for even medium-sized applications - components for a single feature will be scattered all over the place. For example, a <code>Dashboard</code> container may have six presentational components sitting under the <code>components</code> folder intermixed with presentational components from other containers. This can quickly get out of hand.</p>
<p>Instead of breaking things by type, wouldn't it be better to break things by feature? Using this approach, the Dashboard component will be a top-level folder with the 6 presentational components under it as 6 child folders. If there is a strong need to distinguish container components from presentational components, the developer can follow some naming conventions similar to those suggested by Dan Abramov in <a href="https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0" target="_blank">his article</a>, e.g. <code>StoryContainer</code> and <code>Story</code>. Also if there are components that are used in several places, they go under a <code>shared</code> folder. Based on these guidelines, the react-boilerplate example would be structured as follows:</p>
<pre><code>app
 |--- App
 |--- HomePage
 |     `--- RepoListItem
 |--- FeaturePage
 `--- Shared
      |--- List
      |--- ListItem
      `--- ...
</code></pre>
<p>This seems much more intuitive to me because it keeps all related components together. What do you think?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-225409725">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>FWIW, I have a structure similar to one mentioned by <a href="https://github.com/nareshbhatia" target="_blank">@nareshbhatia</a> except for one change - instead of having a Shared folder, I have the shared components grouped by type of functionality provided by those components, i.e. Buttons, Forms, Cards etc. Currently using it on a medium-large scale application and has scaled well and made my life easier.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  </div>
</div>

</div>

</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-225436901">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>

          <p>Good to know, <a href="https://github.com/oyeanuj" target="_blank">@oyeanuj</a>. I have been googling for articles on application structure best practices. Here's two that I found to be very good:</p>
<ol>
<li><a href="http://jaysoo.ca/2016/02/28/organizing-redux-application/" target="_blank">Rules For Structuring (Redux) Applications</a> by Jack Hsu</li>
<li><a href="https://angular.io/docs/ts/latest/guide/style-guide.html" target="_blank">Angular2 Style Guide</a> - This one is specific to Angular 2, but it focuses on the same basic issues. I like the structure of this guide because it not only lists the guidelines but also the reasons behind each.</li>
</ol>
      </td>
    </tr>
  </tbody>
</table>


        



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
    
  
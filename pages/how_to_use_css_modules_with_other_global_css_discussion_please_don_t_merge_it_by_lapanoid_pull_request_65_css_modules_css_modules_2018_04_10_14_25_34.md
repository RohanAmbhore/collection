<a href="https://github.com/css-modules/css-modules/pull/65">https://github.com/css-modules/css-modules/pull/65</a><div id="articleHeader"><h1>              How to use css-modules with other global css (discussion please don't merge it)            #65    </h1></div>


  <div>
    
    <div>
          <a href="/lapanoid" target="_blank">lapanoid</a>
   wants to merge 1 commit into



  css-modules:master

  

from

lapanoid:master



    </div>
  



      




    <h2>Conversation</h2>
    <div id="discussion_bucket">
      


<div>
  <div>

    <div>
      




      
<div>
  <div id="issue-46763286">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/markdalgleish" target="_blank">@markdalgleish</a> <a href="https://github.com/joshwnj" target="_blank">@joshwnj</a><br />
Initially I was trying to make two loaders working together</p>
<pre><code>{
      test: /\.less$/,
      loader: 'style!css?modules&importLoaders=2&sourceMap&localIdentName=[local]___[hash:base64:5]!less'
})
</code></pre>
<pre><code>{
      test: /\.less$/,
      loader: 'style!css!less'
})
</code></pre>
<p>and made an issue for this <a href="https://github.com/css-modules/css-modules/issues/59" target="_blank">#59</a><br />
Bottom line of this was:<br />
name all local css - *.module.(less|sass|whatever)<br />
keep all global css - *.(less|sass|whatever)<br />
and have these loaders</p>
<pre><code>{
      test: /\.module.less$/,
      loader: 'style-loader!css-loader?modules&importLoaders=2&sourceMap&localIdentName=[local]___[hash:base64:5]!less-loader'
}
{
      test: /^((?!\.module).)*less$/,
      loader: 'style!css!less'
}
</code></pre>
<p>This is ugly, but solves the problem on some level.<br />
As <a href="https://github.com/markdalgleish" target="_blank">@markdalgleish</a> said there a lot caveats of having both global and local css, so I hope this PR could be a good place to discuss these caveats. The goal of this PR make reasonable FAQ on this matter.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  


    

    

  


  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-145490217">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I will stress test <code>/^((?!\.module).)*less$/</code>approach tonight, now my .module.less files does not include any .less files in themselves, if they will I think there could be a conflicts with loaders.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-145677573">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <pre><code>@import "./global.less";
</code></pre>
<p>from <code>local.module.less</code></p>
<p>works just fine - no loaders conflicts</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-145688448">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Thanks <a href="https://github.com/lapanoid" target="_blank">@lapanoid</a> good to hear you got something working.  So when you use the code like in your example:</p>
<pre><code>@import "./global.less";
</code></pre>
<p>from <code>local.module.less</code>, does that apply <code>global.less</code> as global styles, or does it add them as exports of the <code>local.module.less</code> module?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-145689680">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>It add them as exports of the local.module.less module</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-150782333">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <blockquote>
<p>It add them as exports of the local.module.less module</p>
</blockquote>
<p>So what happen if I import <code>global.less</code> in second local module? Is that CSS duplicated?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-156995858">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/andresgutgon" target="_blank">@andresgutgon</a> I guess no - webpack treats this as any other module, when you require same js module it will just reuse it - not duplicate it in bundle, same is here</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-166365183">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Discussion seems stalled out... is there a recommended way to do this for the time being? Right now we're looking at gulp scripts doing a concat with a hardcoded list of "node_modules/..." paths, which is pretty janky to say the least :-P</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-187138664">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/lapanoid" target="_blank">@lapanoid</a> I came across this problem recently, trying to declare bootstrap dependencies from my CSS files that were later being processed into CSS Modules. For now I've settled with loading bootstrap externally, using another loader to accomplish this, but I realized we could write a PostCSS plugin that could parse a syntax that would just put a :global() block around the import.</p>
<p>For example, something like:</p>
<div><pre>@global-import from 'bootstrap/buttons';</pre></div>
<p>would turn into</p>
<div><pre>:global {
...
styles from 'bootstrap/buttons';
...
}</pre></div>
<p>This doesn't solve the problem with requiring global CSS in JS, but I would argue that since it's a CSS dependency, it'd be better as an import in the CSS.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-188249086">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/sohkai" target="_blank">@sohkai</a> thanks for feedback and I actually like the idea of post-css plugin, seems like right solution.<br />
Stupid question:<br />
If we just wrap all css in file with :global it will do the case?<br />
Of we need to wrap every class f.e.?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-188257122">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/lapanoid" target="_blank">@lapanoid</a> Hmm, good point; I had the impression that <code>:global</code> would work on nested classes just like that, but from what <a href="https://github.com/css-modules/css-modules/issues/115" target="_blank">#115</a>, <a href="https://github.com/css-modules/css-modules/issues/39" target="_blank">#39</a>, and <a href="https://github.com/css-modules/css-modules/issues/96" target="_blank">#96</a> have, it looks like the examples are just getting expanded with postcss-nested and applied before each nested class. That makes sense too, since the css module loaders probably don't understand nested CSS yet.</p>
<p>In that case, the plugin would require some more work, but I think it's quite feasible to look for classnames and add <code>:global()</code> to all of them after preprocessors and postcss-nested has run.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-188537742">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>We've solved this with standard <code>@import</code> syntax and <code>postcss-import</code> used in <code>postcssAfter</code>. Everything pulled in via <code>@import</code> will be pulled in un-modified as global css.</p>
<pre><code>@import 'node_modules/stuff-that-should-remain-global';

// regular css-modules stuff below here
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-188705905">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/lapanoid" target="_blank">@lapanoid</a> Actually, looking at the <a href="https://github.com/css-modules/postcss-modules-local-by-default" target="_blank">local-by-default</a> plugin, it looks like <code>:global</code> would work if we just wrapped it, but this would require <code>postcss-nested</code> to be run after:</p>
<div><pre>// your import; foo contains .foo .bar { }
@global-import 'foo';

// we wrap :global around it
:global {
.foo .bar { }
}

// then postcss-nested runs
:global .foo .bar { }

// then local by default runs
.foo .bar { }</pre></div>
<p>I don't like this due to the order dependencies (ie. <code>postcss-nested</code> having to run after; this is redundant if someone uses a preprocessor), so another solution would be to just add <code>:global</code> before every root-level class declaration:</p>
<div><pre>/**
 * Your import, assuming you're running postcss-nested after
 * rather than a preprocessor or postcss-nested before.
 * foo contains .foo .bar { }, .foo { .baz { } &-bar { } }
 */
@global-import 'foo';

// we add :global to all the class declarations
:global .foo .bar { }
:global .foo { .baz { } &-bar { } }

// postcss-nested runs
:global .foo .bar { }
:global .foo .baz { }
:global .foo-bar { }

// then local by default runs
.foo .bar { }
.foo .baz { }
.foo-bar { }</pre></div>
<p>This has the benefit of not needing to care about nested rules so users could choose if they wanted a preprocessor to do that or <code>postcss-nested</code>.</p>
<p><a href="https://github.com/themitchy" target="_blank">@themitchy</a> That's pretty neat! It's surprising how easy it is to set up this with browserify if you're just using postcss. I'd still argue for a new import syntax rather than the native <code>@import</code> to support preprocessors and other build systems (ie. webpack, where the order of the loaders prevents <code>postcss-import</code> from achieving this).</p>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-190343723">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/themitchy" target="_blank">@themitchy</a>,  I like your solution, but what do you mean by</p>
<blockquote>
<p>We've solved this with standard <a href="https://github.com/import" target="_blank">@import</a> syntax and postcss-import used in postcssAfter</p>
</blockquote>
<p>how do you configure this postcssAfter? I havent found how to do that with webpack and postcss</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-193848552">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/pgherveou" target="_blank">@pgherveou</a> I'm not sure this can be done in webpack due to the order of the loaders; the <code>postcssAfter</code> <a href="https://github.com/themitchy" target="_blank">@themitchy</a> was talking about is from <a href="https://github.com/css-modules/css-modulesify" target="_blank">css-modulesify</a> plugin for browserify.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-193851107">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Ok thks for your help</p>
<p>Sent from my iPhone</p>
<blockquote>
<p>On Mar 8, 2016, at 8:24 AM, Brett Sun <a href="mailto:notifications@github.com" target="_blank">notifications@github.com</a> wrote:</p>
<p><a href="https://github.com/pgherveou" target="_blank">@pgherveou</a> I'm not sure this can be done in webpack due to the order of the loaders; the postcssAfter <a href="https://github.com/themitchy" target="_blank">@themitchy</a> was talking about is from css-modulesify plugin for browserify.</p>
<p>—<br />
Reply to this email directly or view it on GitHub.</p>
</blockquote>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-194205705">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Yeah, my way of thinking is, <strong>a CSS Module should only import information relative to it.</strong></p>
<p>Basically, the CSS you write exists in a murky world. You're going to have user agent styles, plus a reset or a normalise, plus whatever global stuff you want to add, but the module file itself should be pure. It should feel like writing a new, better CSS. If you want to add global css, add it outside of a module file.</p>
<p>I'm not sure how easy webpack or browserify makes this. Maybe only invoke the css modules loader chain on files that don't match <code>.global.css</code> or something? But yeah, trying to shoehorn a file full of globals just so it passes nicely though the css modules postcss chain doesn't feel like the cleanest way.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-194966517">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/geelen" target="_blank">@geelen</a> I agree that the module file should be pure, but realistically, I think most people will still have to deal with global stylesheets that weren't written with CSS Modules in mind. <code>compose: ... from global</code> handles cases where I want to extend a global style nicely, but it'd also be nice to have a way to declare (and load) those global dependencies from within a CSS module without resorting to wrapping them in your own <code>.global.css</code> file.</p>
<p>I guess this is painfully obvious in hindsight, but importing into global works if you just nest the import in a <code>:global</code>, ie. <code>:global { @import 'foo' }</code>. See <a href="https://github.com/davezuko/react-redux-starter-kit/blob/master/src/styles/core.scss" target="_blank">https://github.com/davezuko/react-redux-starter-kit/blob/master/src/styles/core.scss</a>; this is simple enough that there doesn't need to be a plugin. <del>I think this also handles multiple modules importing the same file (ie. it's only imported once in the final file), assuming that all the modules have the import wrapped in a <code>:global</code>, but I haven't checked yet.</del> Edit: Unfortunately, with the way Sass does importing, having multiple modules importing the same file means that imported file will be duplicated multiple times.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-207827966">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/geelen" target="_blank">@geelen</a> is <a href="https://github.com/davezuko/react-redux-starter-kit/issues/701" target="_blank">davezuko/react-redux-starter-kit#701</a> not the recommended/a bad solution? Should I be importing normalize.css outside of css-modules, possibly as a webpack entry point instead?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  




</div>

  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-214221200">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Unfortunately, there's a bit of a gotcha with <code>:global { @import 'foo'; }</code>. This pattern doesn't work if you use a preprocessor / postcss plugin that allows the <code>&</code> operator; when the imported stylesheet uses a <code>&</code> to reference a root class and adds a class before it, that class doesn't fall inside the <code>:global</code> declaration. Simplified, the pattern looks like:</p>
<div><pre>// your file
:global { @import 'foo.scss'; }

// foo.scss
.foo {
    .bar & { }
}

// In your file, foo.scss gets generated to:
:global .foo { }
.bar :global .foo { }

// So .bar will be mistakenly localized</pre></div>
<p>A good live example of this is in <a href="https://github.com/twbs/bootstrap-sass/blob/master/assets/stylesheets/bootstrap/mixins/_buttons.scss#L24" target="_blank">bootstrap-sass</a>.</p>
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
    
  <div id="issuecomment-220996020">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I think it's super important to mention explicitly (because I struggled with this for a couple of days and didn't find this mentioned anywhere) that in order to use the syntax<br />
<code>:global { @import '../../node_modules/fixed-data-table/dist/fixed-data-table.min.css'; }</code><br />
for example, you must be using a pre-processor (such as sass in my case) that understands / handles nesting.</p>
<p>I have not found a way to import 3rd party css into the global scope using vanilla css + modules. If anyone can help with that it would be super appreciated, because it seems excessive to run my css through a pre-processor just for this one use case.</p>
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
    
  <div id="issuecomment-221007478">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/whtouche" target="_blank">@whtouche</a> Since you're already using css-modules, which relies on postcss, you could always grab <a href="https://github.com/postcss/postcss-nested" target="_blank">postcss-nested</a> to parse the nested syntax.</p>
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
    
  <div id="issuecomment-221033771">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/sohkai" target="_blank">@sohkai</a> Thanks so much for your quick reply; I didn't realize that css modules relied on postcss. You're right, using just that one plugin makes things a lot more lightweight.</p>
<p>I am nearly where I want to be but was hoping you could clarify a wrinkle I found. I installed the postcss-loader and postcss-nested and configured them in my webpack.config, and I am finally able to import 3rd party css into the global scope, which is great.</p>
<p>However, normal classes aren't coming through unless I prefix them with :local. I'm attaching screenshots to hopefully illustrate what I mean.</p>
<p>My question is, have I done something wrong? It doesn't seem like it should be required to prefix every class with :local to get the expected behavior.</p>
<p><a href="https://cloud.githubusercontent.com/assets/7044329/15478246/56c9cbc4-20e7-11e6-8d71-e306b479dc7f.JPG" target="_blank" class="readableLinkWithMediumImage"><img src="https://cloud.githubusercontent.com/assets/7044329/15478246/56c9cbc4-20e7-11e6-8d71-e306b479dc7f.JPG" alt="this-should-be-red" /></a></p>
<p><a href="https://cloud.githubusercontent.com/assets/7044329/15478248/5db5ac32-20e7-11e6-8f63-9bcdd47d7acf.JPG" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/7044329/15478248/5db5ac32-20e7-11e6-8f63-9bcdd47d7acf.JPG" alt="this-should-be-css" /></div></a></p>
<p><a href="https://cloud.githubusercontent.com/assets/7044329/15478253/630136b6-20e7-11e6-9664-edaf908c1efa.JPG" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://cloud.githubusercontent.com/assets/7044329/15478253/630136b6-20e7-11e6-9664-edaf908c1efa.JPG" alt="this-should-be-markup" /></div></a></p>
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
    
  <div id="issuecomment-221083536">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/whtouche" target="_blank">@whtouche</a> It might be helpful if you generate a tiny example repo to showcase this; otherwise it's hard to tell if it might be something in the code or the build configuration or a bug. I haven't tried using postcss-nested since I use sass anyway, but it looks like that plugin might be interfering with the <code>local-by-default</code> plugin that injects <code>:local</code> into classes.</p>
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
    
  <div id="issuecomment-222207739">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/sohkai" target="_blank">@sohkai</a> Sorry for the late response; I added postcss-modules-local-by-default and made it to run after postcss-nested, and now everything works as expected. It still feels like this should be an unnecessary step, but I'm satisfied with the workaround. Thanks so much for being responsive and helpful.</p>
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
    
  <div id="issuecomment-230308240">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>How are you including mixins in global scope from sass?</p>
<div><pre>//index.js
import './styles/core.scss'</pre></div>
<div><pre>//button.js
import styles from './button.scss'</pre></div>
<div><pre>//core.scss
@mixin example() {
    font-size: 16px;
}</pre></div>
<div><pre>//button.scss
.button {
    @include example;
    color: red;
}</pre></div>
<p>This will throw an error something like "No mixin named example"</p>
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
    
  <div id="issuecomment-230311351">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/bretthadley" target="_blank">@bretthadley</a> You probably need to include the sass file defining the mixin in <code>core.scss</code>. Sass is higher up the chain than CSS Modules and will run before CSS Modules does anything...</p>
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
    
  <div id="issuecomment-230315380">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/sohkai" target="_blank">@sohkai</a> Hi, Sorry I renamed the file now.</p>
<p>The core.scss gets processed first (from the index.js file) however when it comes to compiling the button component it throws an error saying "No mixin named example".</p>
<p>I was hoping to avoid having to include core.scss in every component local sass file...</p>
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
    
  <div id="issuecomment-230316177">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/bretthadley" target="_blank">@bretthadley</a> Unfortunately that's something that does happen with Sass. It's useful in keeping modules apart, but I agree, sometimes it can be tedious. If you're using webpack, you can check out <a href="https://github.com/shakacode/sass-resources-loader" target="_blank">sass-resources-loader</a> if you'd like to load your <code>core.scss</code> file in every Sass file.</p>
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
        <h3 id="ref-issue-165922401">
      
        
      
        <img src="https://avatars1.githubusercontent.com/u/12040845?s=60&v=4" width="16" height="16" alt="@jdelafon" />
  <a href="/jdelafon" target="_blank">jdelafon</a>
  

      referenced this pull request
        in <strong>kriasoft/react-firebase-starter</strong>
      <a href="#ref-issue-165922401" target="_blank">
        <relative-time>on Jul 16, 2016</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/kriasoft/react-firebase-starter/issues/112" target="_blank">
          Material Design CSS not rendering properly
          #112
        </a>
      </h4>
    

    


  

</div>


</div>


  

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-297552153">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/jamieshark" target="_blank">@jamieshark</a> - the two Webpack files I referenced form part of a larger Webpack config, that you can access by downloading my starter kit with <code>npm i -g reactql</code> and then <code>reactql new</code> to create a new project. See <a href="http://reactql.org" target="_blank">http://reactql.org</a> for full details.</p>
<p>You can also see the Webpack config files directly at <a href="https://github.com/reactql/kit/blob/master/kit/webpack/" target="_blank">https://github.com/reactql/kit/blob/master/kit/webpack/</a></p>
<p>The config I'm using is intended to generate a dev and production browser bundle as well as a production server bundle, so it has quite a comprehensive and has several interconnecting pieces that will make a lot more sense if you view the starter kit as a whole.</p>
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
    
  <div id="issuecomment-297646518">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/borela" target="_blank">@borela</a> Really interesting, thanks.</p>
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
    
  <div id="issuecomment-300195174">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I am trying to setup a SSR build where there are two webpack files, one for the <code>client</code>, and one for the <code>server</code>. This is setup this way due to the CMS I am using and how it handles SSR.</p>
<p>The examples in this thread work well for webpack itself. I am currently using multiple loaders with different targets:</p>
<pre><code>{
  test: /\.scss$/,
  include: [/\.global/, /bootstrap/],
  loader: ExtractTextPlugin.extract({
    fallback: 'style-loader',
    use: [
      {
        loader: 'css-loader',
        options: { modules: false }
      },
      { loader: 'postcss-loader' },
      { loader: 'sass-loader' }
    ]
  })
},
{
  test: /\.scss$/,
  exclude: [/\.global/, /bootstrap/, /node_modules/],
  use: ExtractTextPlugin.extract({
    fallback: 'style-loader',
    use: [
      {
        loader: 'css-loader',
        options: {
          modules: true,
          localIdentName: '[local]--[hash:base64:5]'
        }
      },
      { loader: 'postcss-loader' },
      { loader: 'sass-loader' }
    ]
  })
}
</code></pre>
<p>However this does not appear to work for SSR, I am using <a href="https://github.com/michalkvasnicak/babel-plugin-css-modules-transform" target="_blank">babel-plugin-css-modules-transform</a> to allow me to inline my prefixed classes into the SSR bundle, but ignore compiling or inlining the CSS values into the DOM. Once the client kicks in the CSS library that was bundled by the client library styles the view.</p>
<p>On my server bundle I have this config:</p>
<pre><code>{
  test: /\.js(x)?$/,
  use: {
    loader: 'babel-loader',
    options: {
      plugins: [
        [
          'css-modules-transform',
          {
            generateScopedName: '[local]--[hash:base64:5]',
            preprocessCss: './server/sassPreprocessor.js',
            extensions: ['.scss']
          }
        ]
      ]
    }
  }
}
</code></pre>
<p>Which properly inlines the CSS classes when <em>I do not import a global _vars file</em>. When I do import the global vars file the css is not compiled inline.</p>
<p>This does not work:</p>
<pre><code>@import '~client/styles/_vars.global.scss';

.nav {
  width: 96px;
  background-color: $blue;
}
</code></pre>
<p>This does:</p>
<pre><code>.nav {
  width: 96px;
}
</code></pre>
<p>What do you think?</p>
<p>My goal is to have the SSR file not contain any inline CSS, and no server CSS to be emitted.</p>
<p>Thanks</p>
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
    
  <div id="issuecomment-300199092">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/gregorskii" target="_blank">@gregorskii</a>, if you don't get a direct resolution to the code you posted, check out the way I handle SSR with css-modules in my <a href="https://github.com/reactql/kit/tree/master/kit/webpack" target="_blank">ReactQL starter kit config</a>.</p>
<p>You might find the configs a bit 'noisy' because it's crunching a lot of other stuff, but it should be pretty obvious how the CSS specific pipeline works.</p>
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
    
  <div id="issuecomment-300202008">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/leebenson" target="_blank">@leebenson</a> does your config output the CSS inline in the server bundle? I appears you are using a very similar config to my client config on your server. Am I mistaken in thinking I need the <code>babel-plugin-css-modules-transform</code> plugin to support this on the server?</p>
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
    
  <div id="issuecomment-300202617">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/gregorskii" target="_blank">@gregorskii</a> - it inlines the class names, but not the styles. Those are extracted out to a separate <code>dist/public/assets/styles.css</code> file, that is then loaded on the client side. The hashed class names, however, are the same both on the server and the client. Is that what you're intending to achieve?</p>
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
    
  <div id="issuecomment-300205137">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>My client webpack file creates the client CSS, the server one does not need to emit CSS. That's a finer detail though, because I guess it could be done on either side. But for curiosity sake, is it possible to have the server bundle only include the class names?</p>
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
    
  <div id="issuecomment-300206424">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Actually technically it does matter as the server files get emitted in a different place.</p>
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
    
  <div id="issuecomment-300208961">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/gregorskii" target="_blank">@gregorskii</a> - yes, that's exactly what my ReactQL config does. Specifically:</p>
<ol>
<li>The client config emits <code>style.css</code> (the server skips it)</li>
<li>Both the client and server emit the localised/global 'hashed' classnames in the resulting JS bundles</li>
</ol>
<p>End result - both environments have exactly the same classnames, but styles only get loaded in the browser when the resulting <code>style.css</code> is loaded via a <code>&lt;link&gt;</code> tag.</p>
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
    
  <div id="issuecomment-300287505">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/leebenson" target="_blank">@leebenson</a>, awesome, can you point out in the config how the server skips emitting it? :)</p>
<p>Thanks!</p>
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
    
  <div id="issuecomment-300292110">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/gregorskii" target="_blank">@gregorskii</a> - it's a bit tricky, because there's a lot more going on... but <a href="https://github.com/reactql/kit/blob/master/kit/webpack/server.js#L80-L99" target="_blank">these lines in server.js</a> tackle css-modules loading on the server.</p>
<p>TL;DR - just set your css loading to use <code>loader: 'css-loader/locals'</code> and only use <code>ExtractTextPlugin</code> on the client side.</p>
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
        <h3 id="ref-issue-227501315">
      
        
      
        <img src="https://avatars0.githubusercontent.com/u/1130448?s=60&v=4" width="16" height="16" alt="@gregorskii" />
  <a href="/gregorskii" target="_blank">gregorskii</a>
  

      referenced this pull request
        in <strong>michalkvasnicak/babel-plugin-css-modules-transform</strong>
      <a href="#ref-issue-227501315" target="_blank">
        <relative-time>on May 10, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/michalkvasnicak/babel-plugin-css-modules-transform/issues/46" target="_blank">
          Global/Local CSS imports
          #46
        </a>
      </h4>
    

    


  

</div>

  <div>
        <h3 id="ref-issue-228600307">
      
        
      
        <img src="https://avatars3.githubusercontent.com/u/15406202?s=60&v=4" width="16" height="16" alt="@nayucolony" />
  <a href="/nayucolony" target="_blank">nayucolony</a>
  

      referenced this pull request
        in <strong>nayucolony/til</strong>
      <a href="#ref-issue-228600307" target="_blank">
        <relative-time>on May 15, 2017</relative-time>
      </a>
    </h3>

  
    
          
      Closed
    



    
      <h4>
        <a href="/nayucolony/til/issues/1" target="_blank">
          react storybookめも
          #1
        </a>
      </h4>
    

    


  

</div>


</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-303907836">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>For anyone's interest, support for CSS Modules has been added to <a href="https://github.com/facebookincubator/create-react-app/pull/2285" target="_blank">Create-React-APP</a></p>
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
    
  <div id="issuecomment-310801342">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/cr101" target="_blank">@cr101</a> It has not been added yet, but there is an open Pull Request for adding this feature.</p>
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
  <h3 id="ref-commit-c9df0fa">
    
      
    
    
  <a href="/hustlrb" target="_blank">hustlrb</a> 


      pushed a commit
        to hustlrb/reactApp
      that referenced
      this pull request

    <a href="#ref-commit-c9df0fa" target="_blank">
      <relative-time>on Sep 15, 2017</relative-time>
    </a>
  </h3>

  
</div>


</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-331101125">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>is there a way to compose only the class name? this would help with using the DllPlugin, or be composing from a library that you are extracting into some kind of vendor.css file and avoid duplicate css.</p>
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
    
  <div id="issuecomment-349751051">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Guys I am developing some library for our project let's call it <code>ui-components</code> and we have main application let's call it <code>frontend</code>. We use bootstrap and I want to redefine some bootstrap classes with our fonts, which are defined in the library e.g.:</p>
<div><pre>:global {
  & .form-group {
    label {
      /*here I want to use .font-medium; from 'ui-components/src/common-styles/font.pcss'*/
      color: var(--N700);
      margin: 4px 0;
      width: 100%;
    }
  }
}</pre></div>
<p>So, I cannot compose it, because:</p>
<blockquote>
<p>label selector looks weird it is not :local</p>
</blockquote>
<p>But I need to inherit that, I do not want to write another class just to repeat myself, that's why we have components library.</p>
<p>How to achieve that?</p>
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
    
  <div id="issuecomment-350657310">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>you can't compose global styles because composing just concatenates the class name. you only compose when you also control the element's class name. for example:</p>
<p>with this:</p>
<pre><code>.font-medium {
   font-weight: 600;
   font-size: 16px;
}
</code></pre>
<p>and then this:</p>
<pre><code>.form-group-label {
    composes: font-medium from 'ui-components/src/common-styles/font.pcss';
    color: var(--N700);
    margin: 4px 0;
    width: 100%;
}
</code></pre>
<p>composing would do this by concatenating the class name:</p>
<pre><code>import styles from './styles.css';
styles['form-group-label'] // is a string with: ".form-group-label.font-medium"
</code></pre>
<p>rather than altering the css and doing (what i think you want it to do) this:</p>
<pre><code>.form-group-label {
   font-weight: 600;
   font-size: 16px;
   color: #000;
   margin: 4px 0;
   width: 100%;
}
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
        <h3 id="ref-pullrequest-285356529">
      
        
      
        <img src="https://avatars0.githubusercontent.com/u/3277097?s=60&v=4" width="16" height="16" alt="@0xcaff" />
  <a href="/0xcaff" target="_blank">0xcaff</a>
  

      referenced this pull request
        in <strong>postcss/postcss-import</strong>
      <a href="#ref-pullrequest-285356529" target="_blank">
        <relative-time>on Jan 2</relative-time>
      </a>
    </h3>

  
    
        
      Merged
    



    
      <h4>
        <a href="/postcss/postcss-import/pull/327" target="_blank">
          Added Filter Parameter
          #327
        </a>
      </h4>
    

    


  

</div>


</div>

    
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-354712147">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>This can be done easily with resource queries. Here's the webpack rule:</p>
<pre><code>{
  rules: [
    {
      oneOf: [
        {
          test: /\.css$/,
          resourceQuery: /^\?raw$/,
          use: [require.resolve("style-loader"), require.resolve("css-loader")]
        },
        {
          test: /\.css$/,
          use: [
            require.resolve("style-loader"),
            {
              loader: require.resolve("css-loader"),
              options: {
                importLoaders: 1,
                modules: true,
                localIdentName: "[name]__[local]___[hash:base64:5]"
              }
            },
            require("./postcss-loader")
          ]
        }
      ]
    }
  ];
}
</code></pre>
<p>Here's how you would use it:</p>
<pre><code>import './global.css?raw';
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
    
  <div id="issuecomment-355078216">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Thankyou for the above answer, <a href="https://github.com/0xcaff" target="_blank">@0xcaff</a>!</p>
<p>However it's throwing errors when adapting this technique to my webpack config. I think this is because there's nothing in the second rule to prevent <code>.css</code> files that had been matched from the rule above being matched again in the rule below.</p>
<p>I've adapted your answer to use webpack's <code>oneOf:[]</code>, so each variation can only be matched once.<br />
I also like this approach because it keeps the css config together, and uses fewer lines as there's<br />
only one <code>test: /\.css$/,</code>.</p>
<pre><code>rules: [{
    test: /\.css$/,
    oneOf: [{
        resourceQuery: /^\?raw$/,
        use: [
            require.resolve('style-loader'),
            require.resolve('css-loader')
        ]
    }, {
        use: [
            require.resolve('style-loader'),
            {
                loader: require.resolve('css-loader'),
                options: {
                    importLoaders: 1,
                    modules: true,
                    localIdentName: '[name]__[local]___[hash:base64:5]'
                }
            },
            require('./postcss-loader')
        ]
    }]
}]
</code></pre>
<p>Again, we can use</p>
<pre><code>import './global.css?raw'
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
    
  <div id="issuecomment-355092266">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Good catch <a href="https://github.com/joewestcott" target="_blank">@joewestcott</a>. There was a oneOf which I forgot to add back. I'll edit my post.</p>
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
    
  <div id="issuecomment-355971111">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I opted for postcss-modules as it has the <a href="https://github.com/css-modules/postcss-modules#generating-scoped-names" target="_blank">globalModulePaths</a> option. I also integrated <a href="https://github.com/gajus/babel-plugin-react-css-modules" target="_blank">babel-plugin-react-css-modules</a>.</p>
<div><pre>// Configuration taken from webpack.config.dev.js

{
  test: /\.css$/,
  use: [
    require.resolve('style-loader'),
    {
      loader: require.resolve('css-loader'),
      options: {
        importLoaders: 1,
        imports: false,
        modules: false,
        sourceMap: false
      }
    },
    {
      loader: require.resolve('postcss-loader'),
      options: {
        // Necessary for external CSS imports to work
        // https://github.com/facebookincubator/create-react-app/issues/2677
        ident: 'postcss',
        plugins: () =&gt; {
          const escapeRegex = require('escape-string-regexp');
          return [
            require('postcss-flexbugs-fixes'),
            autoprefixer({
              flexbox: 'no-2009',
            }),
            require('postcss-modules')({
              globalModulePaths: [escapeRegex(paths.appNodeModules)],
              generateScopedName: '[name]__[local]___[hash:base64:5]',
              getJSON: () =&gt; {},
            })
          ];
        }
      }
    }
  ]
};</pre></div>
<hr />
<p>The configuration was obtained from create-react-app after running eject.</p>
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
    
  <div id="issuecomment-357232526">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/aaronatmycujoo" target="_blank">@aaronatmycujoo</a> that really sucks... I want just to extend the class, which has already been written in one place, just to DRY, but I need to recreate it locally and then compose :(</p>
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
    
  <div id="issuecomment-357619011">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>But how can it compose a class name when you are targeting a generic element? And especially when you are using <code>:global:</code>. A mixin is probably what you are looking for.</p>
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
    
  <div id="issuecomment-358511980">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Is there already a best solution for importing external css? I'd like to add normalize.css and some other external css resources. Should I go for <a href="https://github.com/0xcaff" target="_blank">@0xcaff</a> approach? Or is there a better solution? I was thinking that maybe using the .pcss extension for all the project files and running css modules only on them could be a nice workaround</p>
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
    
  <div id="issuecomment-358830259">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/aaronatmycujoo" target="_blank">@aaronatmycujoo</a> just using postcss import won't make the imported libraries not use css modules so that's not enough. Looks like the workaround in the first post of this thread seems to be the best way until now - as long as no library or external file add ".module" to their css files.</p>
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
    
  <div id="issuecomment-359871109">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Ok I've tested the first suggestion, by the author of this thread. It works nice, but I found out it doesn't make sense to have .modules.css instead of global.css, because there's usually only one or few global css files. Having .module.css in all your components css file makes it harder to navigate between tabs in the editor and also it's more typing when importing. I changed the regex to this one, that allows a file called global.css or {name}.global.css:<br />
Modules: <code>/^((?!\.?global).)*css$/</code><br />
Global: <code>/\.?global.css$/</code></p>
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
    
  <div id="issuecomment-364643501">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><a href="https://github.com/pietrofxq" target="_blank">@pietrofxq</a> this worked perfectly for me! For the few third-party styles I need that aren't css-modules I can easily import this way.</p>
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
        


<div id="partial-pull-merging">

    <h2>Merge state</h2>
    <div>


      
  
<div>
  
    
  
  <div>
    <div>
      


      
      

      
  <div>
    

    <div>
      

      <h3>This branch has no conflicts with the base branch</h3>
        Only those with <a href="https://help.github.com/articles/what-are-the-different-access-permissions" target="_blank">write access</a> to this repository can merge pull requests.
    </div>

    
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

    

    

        <p>
    
    
        Attach files by dragging & dropping,
        selecting them, or pasting
        from the clipboard.
    
    
    
    
    
    
    
    
    
  </p>


    
  </div>

  

  


  
</div>

          
      </div>

    <div>
      
      <strong>ProTip!</strong>
      Add comments to specific lines under <a href="/css-modules/css-modules/pull/65/files" target="_blank">Files changed</a>.
    </div>
</div>


  </div>
</div>

    </div>
  
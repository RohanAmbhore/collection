<a href="https://glenmaddern.com/articles/css-modules">https://glenmaddern.com/articles/css-modules</a><div id="articleHeader"><h1>CSS Modules</h1></div><h2>Welcome to the Future</h2><time>2015-08-19</time></header><p>If you wanted to identify an inflection point in the recent development of CSS thinking, you’d probably pick Christopher Chedeau’s “CSS in JS” talk from NationJS in November, 2014. It was a watershed moment that set a bunch of different minds spiralling off in their own directions like particles after a high-energy collision. For instance, <a href="https://github.com/js-next/react-style" target="_blank">React Style</a>, <a href="https://github.com/petehunt/jsxstyle" target="_blank">jsxstyle</a> and <a href="https://github.com/FormidableLabs/radium" target="_blank">Radium</a> are three of the newest, cleverest, and most viable approaches to styling in React and all reference it <em>in their project Readme</em>. If invention is a case of exploring the <a href="http://www.practicallyefficient.com/home/2010/09/28/the-adjacent-possible" target="_blank">adjacent possible</a>, then Christopher is responsible for making a lot of what’s possible more adjacent.</p><figure><div class="readableLargeImageContainer"><img src="/assets/images/7_problems_css.jpg" alt="Christopher Chedeau's 7 problems with CSS at scale" /></div><figcaption>This slide really hit home for a lot of folks</figcaption></figure><p>These are all legitimate problems that affect most large CSS codebases in one way or another. Christopher points out that these all have good solutions if you move your styling to JavaScript, which is true but introduces its own complexities and idiosyncrasies. Just look at the range of approaches to handling <code>:hover</code> states among the projects I referenced earlier, something that has been solved in CSS for a <em>long</em> time.</p><p>The <a href="https://github.com/orgs/css-modules/people" target="_blank">CSS Modules team</a> felt we could attack the problem head-on — keep everything we liked about CSS, and build upon the good work that the styles-in-JS community was producing. So, while we’re bullish about our approach and firmly defend the virtues of CSS, we owe a debt of gratitude to those folks pushing the boundaries in the other direction. Thanks, friends! 👬👫👭</p><p>Let me tell you about what CSS Modules is, and why it’s the future.</p><figure><div class="readableLargeImageContainer"><img src="/assets/images/jony.jpg" alt="Jony Ive contemplates CSS Modules" /></div><figcaption>This is how intensely we’ve been thinking about CSS.</figcaption></figure><h2>Step 1. Local by default.</h2><p>In CSS Modules, each file is compiled separately so you can use simple class selectors with generic names — you don’t need to worry about polluting the global scope. Let’s say we were building a simple submit button with the following 4 states.</p><div><div>Normal</div><div>Disabled</div><div>Error</div><div>In Progress</div></div><h4>Before CSS Modules</h4><p>We might code this up using Suit/BEM-style classnames & plain old CSS & HTML like so:</p><pre><code>/* components/submit-button.css */
.Button { /* all styles for Normal */ }
.Button--disabled { /* overrides for Disabled */ }
.Button--error { /* overrides for Error */ }
.Button--in-progress { /* overrides for In Progress */</code></pre><pre><code>&lt;button class="Button Button--in-progress"&gt;Processing...&lt;/button&gt;</code></pre><p>It’s quite good, really. We have these four variants but BEM-style naming means we don’t have nested selectors. We’re starting <code>Button</code> with a capital letter so as to (hopefully) avoid clashes with any of our previous styles or any dependencies we’re pulling in. And we’re adopting the <code>--modifier</code> syntax to be clear that the variants require the base class to be applied.</p><p>All in all, this is reasonably explicit & maintainable code, but it requires an awful lot of cognitive effort around naming discipline. But it’s the best we can do with standard CSS.</p><h4>With CSS Modules</h4><p>CSS Modules means you never need to worry about your names being too generic, just use whatever makes the most sense:</p><pre><code>/* components/submit-button.css */
.normal { /* all styles for Normal */ }
.disabled { /* all styles for Disabled */ }
.error { /* all styles for Error */ }
.inProgress { /* all styles for In Progress */</code></pre><p>Notice that we don’t use the word <em>“button”</em> anywhere. Why would we? The file is already called <em>“submit-button.css”</em>. In any other language, you don’t have to prefix all your local variables with the name of the file you’re working on — CSS should be no different.</p><p>That’s made possible by the way CSS Modules is compiled — by using <code>require</code> or <code>import</code> to load the file from JavaScript:</p><pre><code>/* components/submit-button.js */
import styles from './submit-button.css';

buttonElem.outerHTML = `&lt;button class=${styles.normal}&gt;Submit&lt;/button&gt;`</code></pre><p>The actual classnames are automatically generated and guaranteed to be unique. CSS Modules takes care of all that for you, and compiles the files to a format called ICSS (<a href="interoperable-css" target="_blank">read my blog post about that</a>), which is how CSS and JS can communicate. So, when you run your app, you’ll see something like:</p><pre><code>&lt;button class="components_submit_button__normal__abc5436"&gt;
  Processing...
&lt;/button&gt;</code></pre><p>If you see that in your DOM, that means it’s working!</p><figure><div class="readableLargeImageContainer"><img src="/assets/images/gorilla_shark.jpg" alt="A gorilla high-fives a shark in front of an explosion" /></div><figcaption>You’re the gorilla. CSS Modules is the shark.<br />(credit: <a href="http://www.topatoco.com/merchant.mvc?Screen=PROD&Store_Code=TO&Product_Code=RB-HIGHFIVE&Category_Code=RB" target="_blank">Christopher Hastings</a>)</figcaption></figure><h4>Naming conventions</h4><p>Considering our button example again:</p><pre><code>/* components/submit-button.css */
.normal { /* all styles for Normal */ }
.disabled { /* all styles for Disabled */ }
.error { /* all styles for Error */ }
.inProgress { /* all styles for In Progress */</code></pre><p>Notice that all the classes are stand-alone, rather than one being the <em>“base”</em> and the rest being <em>“overrides”</em>. In CSS Modules <strong>each class should have all the styles needed for that variant</strong> (more on how that works in a minute). It makes a big difference to how you use these styles in JavaScript:</p><pre><code>/* Don't do this */
`class=${[styles.normal, styles['in-progress']].join(" ")}`

/* Using a single name makes a big difference */
`class=${styles['in-progress']}`

/* camelCase makes it even better */
`class=${styles.inProgress}`</code></pre><p>Of course, if you get paid by the keystroke, do what you want!</p><h4>A React Example</h4><p>There’s nothing about CSS Modules that’s React-specific. But React gives you a particularly excellent experience using CSS Modules, so it’s worth showing a slightly more complex example:</p><pre><code>/* components/submit-button.jsx */
import { Component } from 'react';
import styles from './submit-button.css';

export default class SubmitButton extends Component {
  render() {
    let className, text = "Submit"
    if (this.props.store.submissionInProgress) {
      className = styles.inProgress
      text = "Processing..."
    } else if (this.props.store.errorOccurred) {
      className = styles.error
    } else if (!this.props.form.valid) {
      className = styles.disabled
    } else {
      className = styles.normal
    }
    return &lt;button className={className}&gt;{text}&lt;/button&gt;
  }
}</code></pre><p>You can use your styles without ever worrying about what global-safe CSS classnames are being generated, which lets you focus on the <em>component</em>, not the styling. And once you’re rid of that constant context-switching, you’ll be amazed you ever put up with it.</p><p>But that’s just the start. When it <em>is</em> time to think about how your styles are put together, CSS Modules has your back.</p><h2>Step 2. Composition is everything</h2><p>Earlier I mentioned that each class should contain <em>all</em> the styles for the button in each different state, in contrast to BEM where it assumes you’d have more than one:</p><pre><code>/* BEM Style */
innerHTML = `&lt;button class="Button Button--in-progress"&gt;`

/* CSS Modules */
innerHTML = `&lt;button class="${styles.inProgress}"&gt;`</code></pre><p>But wait, how do you represent <em>shared</em> styles between all the states? The answer is probably CSS Modules’ most potent weapon, <strong>composition</strong>:</p><pre><code>.common {
  /* all the common styles you want */
}
.normal {
  composes: common;
  /* anything that only applies to Normal */
}
.disabled {
  composes: common;
  /* anything that only applies to Disabled */
}
.error {
  composes: common;
  /* anything that only applies to Error */
}
.inProgress {
  composes: common;
  /* anything that only applies to In Progress */
}</code></pre><p>The <code>composes</code> keyword says that <code>.normal</code> <em>includes</em> all the styles from <code>.common</code>, much like the <code>@extends</code> keyword in Sass. But while Sass rewrites your CSS selectors to make that happen, <strong>CSS Modules changes which classes are exported to JavaScript</strong>.</p><h4>In Sass</h4><p>Let’s take our BEM example from above and apply some of Sass’ <code>@extends</code>:</p><pre><code>.Button--common { /* font-sizes, padding, border-radius */ }
.Button--normal {
  @extends .Button--common;
  /* blue color, light blue background */
}
.Button--error {
  @extends .Button--common;
  /* red color, light red background */
}</code></pre><p>This compiles to this CSS:</p><pre><code>.Button--common, .Button--normal, .Button--error {
  /* font-sizes, padding, border-radius */
}
.Button--normal {
  /* blue color, light blue background */
}
.Button--error {
  /* red color, light red background */
}</code></pre><p>You can then just use <em>one</em> class in your markup <code>&lt;button class="Button--error"&gt;</code> and get the common & specific styles you want. It’s a really powerful concept, but the implementation has some edge cases & pitfalls that you should be aware of. A great summary of those issues and links to further reading is <a href="http://www.sitepoint.com/avoid-sass-extend/" target="_blank">available here</a>, thanks to Hugo Giraudel.</p><h4>With CSS Modules</h4><p>The <code>composes</code> keyword is conceptually similar to <code>@extends</code> but works differently. To demonstrate, let’s look at an example:</p><pre><code>.common { /* font-sizes, padding, border-radius */ }
.normal { composes: common; /* blue color, light blue background */ }
.error { composes: common; /* red color, light red background */ }</code></pre><p>That gets compiled and ends up looking like this by the time it reaches the browser:</p><pre><code>.components_submit_button__common__abc5436 { /* font-sizes, padding, border-radius */ }
.components_submit_button__normal__def6547 { /* blue color, light blue background */ }
.components_submit_button__error__1638bcd { /* red color, light red background */ }</code></pre><p>In your JS code, <code>import styles from "./submit-button.css"</code> returns:</p><pre><code>styles: {
  common: "components_submit_button__common__abc5436",
  normal: "components_submit_button__common__abc5436 components_submit_button__normal__def6547",
  error: "components_submit_button__common__abc5436 components_submit_button__error__1638bcd"
}</code></pre><p>So we can still just use <code>styles.normal</code> or <code>styles.error</code> in our code but <strong>we get multiple class rendered into the DOM</strong>.</p><pre><code>&lt;button class="components_submit_button__common__abc5436 
               components_submit_button__normal__def6547"&gt;
  Submit
&lt;/button&gt;</code></pre><p>This is the power of <code>composes</code>, you can combine multiple separate groups of styles without changing your markup or rewriting your CSS selectors 👌</p><h2>Step 3. Sharing between files</h2><p>Working with Sass or LESS, each file that you <code>@import</code> gets processed in the same global workspace. It’s how you can define variables or mixins in one file and use them in all your component files. It’s useful, but as soon as your variable names threaten to clash with each other (since it’s another global namespace), you inevitably refactor out a <code>variables.scss</code> or <code>settings.scss</code>, and you lose visibility into which components depend on which variables. And your settings file becomes <a href="https://github.com/twbs/bootstrap-sass/blob/master/assets/stylesheets/bootstrap/_variables.scss" target="_blank">unwieldy</a>.</p><p>There are better methodologies (in fact Ben Smithett’s <a href="http://bensmithett.com/smarter-css-builds-with-webpack/" target="_blank">post about using Sass & Webpack together</a> was a direct influence on the CSS Modules project and I encourage you to read it) but you’re still constrained by the global nature of Sass.</p><p>CSS Modules runs on a single file at a time, so there’s no global context to pollute. And like in JavaScript where we can <code>import</code> or <code>require</code> our dependencies, CSS Modules lets us <code>compose</code> from another file: </p><pre><code>/* colors.css */
.primary {
  color: #720;
}
.secondary {
  color: #777;
}
/* other helper classes... */</code></pre><pre><code>/* submit-button.css */
.common { /* font-sizes, padding, border-radius */ }
.normal {
  composes: common;
  composes: primary from "../shared/colors.css";
}</code></pre><p>Using composition, we are able to reach into a totally general file like <code>colors.css</code> and reference the one class we want using its local name. And since composition changes which classes get <em>exported</em>, not the CSS itself, the <code>composes</code> statements themselves get deleted from the CSS before it reaches the browser:</p><pre><code>/* colors.css */
.shared_colors__primary__fca929 {
  color: #720;
}
.shared_colors__secondary__acf292 {
  color: #777;
}</code></pre><pre><code>/* submit-button.css */
.components_submit_button__common__abc5436 { /* font-sizes, padding, border-radius */ }
.components_submit_button__normal__def6547 {}</code></pre><pre><code>&lt;button class="shared_colors__primary__fca929
               components_submit_button__common__abc5436 
               components_submit_button__normal__def6547"&gt;
  Submit
&lt;/button&gt;</code></pre><p>In fact, by the time it reaches the browser, our local name <em>“normal”</em> has no styles of its own. This is a good thing! It means we were able to add a new locally-meaningful object (an entity called <em>“normal”</em>) <strong>without adding a single new line of CSS</strong>. The more we can do this, the fewer visual inconsistencies that will creep into our site and the less bloat we’ll be shipping to our customers’ browsers.</p><p><small>Aside: These empty classes can easily be detected and removed by something like <a href="https://github.com/css/csso" target="_blank">csso</a></small></p><h2>Step 4. Single responsibility modules</h2><p>Composition is powerful because it lets you describe what an element <em>is</em>, not what styles make it up. It’s a different way of mapping conceptual entities (<em>elements</em>) to styling entities (<em>rules</em>). Let’s take a look at a simple example in plain-old-CSS:</p><pre><code>.some_element {
  font-size: 1.5rem;
  color: rgba(0,0,0,0);
  padding: 0.5rem;
  box-shadow: 0 0 4px -2px;
}</code></pre><p>This element, these styles. Simple. However, there’s a problem: the colour, font-size, box-shadow, the padding — everything is specified here in full detail despite the fact that <em>we probably want to reuse these styles elsewhere</em>. Let’s refactor it using Sass:</p><pre><code>$large-font-size: 1.5rem;
$dark-text: rgba(0,0,0,0);
$padding-normal: 0.5rem;
@mixin subtle-shadow {
  box-shadow: 0 0 4px -2px;
}

.some_element {
  @include subtle-shadow;
  font-size: $large-font-size;
  color: $dark-text;
  padding: $padding-normal;
}</code></pre><p>This is an improvement, but we’ve only extracted <em>half</em> of most of the lines. The fact that <code>$large-font-size</code> is for typography and <code>$padding-normal</code> is for layout is merely expressed by the name, not enforced anywhere. When the value of a declaration like <code>box-shadow</code> doesn’t lend itself to being a variable, we have to use a <code>@mixin</code> or <code>@extends</code>.</p><h4>With CSS Modules</h4><p>By using composition, we can declare our component <em>in terms of reusable parts</em>:</p><pre><code>.element {
  composes: large from "./typography.css";
  composes: dark-text from "./colors.css";
  composes: padding-all-medium from "./layout.css";
  composes: subtle-shadow from "./effect.css";
}</code></pre><p>The format naturally lends itself to having lots of single-purpose files, using the file system to delineate styles of different purposes rather than namespacing. And if you want to compose multiple classes from a single file, there’s a short hand for that:</p><pre><code>/* this short hand: */
.element {
  composes: padding-large margin-small from "./layout.css";
}

/* is equivalent to: */
.element {
  composes: padding-large from "./layout.css";
  composes: margin-small from "./layout.css";
}</code></pre><p>This opens up the possibility of using <em>extremely</em> granular classes to give aliases for every visual trait your site uses:</p><pre><code>.article {
  composes: flex vertical centered from "./layout.css";
}

.masthead {
  composes: serif bold 48pt centered from "./typography.css";
  composes: paragraph-margin-below from "./layout.css";
}

.body {
  composes: max720 paragraph-margin-below from "layout.css";
  composes: sans light paragraph-line-height from "./typography.css";
}</code></pre><p>This is a technique I’m really interested in exploring further. In my mind, it combines some of the best aspects of atomic CSS techniques like <a href="http://tachyons.io/" target="_blank">Tachyons</a>, the readability of something like <a href="http://semantic-ui.com/" target="_blank">Semantic UI</a> with true, dependable isolation.</p><p>But we’re only at the beginning of the CSS Modules story. We’d love for you to try it on your current next project and help us shape its future.</p><h1>Get started!</h1><p>With CSS Modules, we hope that we’re able to help you and your team maintain as much of your current knowledge of CSS and your product, but become vastly more comfortable and more productive. We’ve kept the syntax additions to a minimum and tried to ensure there are examples that are close to the way you’re already working. We have demo projects for <a href="https://github.com/css-modules/webpack-demo" target="_blank">Webpack</a>, <a href="https://github.com/css-modules/jspm-demo" target="_blank">JSPM</a> and <a href="https://github.com/css-modules/browserify-demo" target="_blank">Browserify</a> if you’re using one of those, and we’re always on the look-out for new environments where CSS Modules would work: support for server-side NodeJS is <a href="https://github.com/css-modules/css-modules-require-hook" target="_blank">happening</a> and Rails is on the horizon.</p><p>But to make things even easier, I’ve made a little Plunkr for you to <a href="http://plnkr.co/edit/FbcJpb?p=preview" target="_blank">play around with an example</a> without installing a thing! Give it a go:</p><p><a href="http://plnkr.co/edit/FbcJpb?p=preview" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="/assets/images/css_modules_plunkr.png" title="Try CSS Modules live" /></div></a></p><p>When you’re ready, take a look at the main <a href="http://github.com/css-modules/css-modules" target="_blank">CSS Modules</a> repo and if you have a question, please raise an issue to kick off a discussion. The <a href="https://github.com/orgs/css-modules/people" target="_blank">CSS Modules team</a> is small and we haven’t seen every use-case yet, so we’d love to hear from you.</p><h5>Style happy, friends!</h5>
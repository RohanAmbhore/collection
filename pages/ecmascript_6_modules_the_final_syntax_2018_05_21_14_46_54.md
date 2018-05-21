<a href="http://2ality.com/2014/09/es6-modules-final.html">http://2ality.com/2014/09/es6-modules-final.html</a><div id="articleHeader"><h1>ECMAScript 6 modules: the final syntax</h1></div><p><strong>Check out my book (free online): “<a href="http://exploringjs.com/es6/" target="_blank">Exploring ES6</a>”.</strong> Updated version of this blog post: chapter “<a href="http://exploringjs.com/es6/ch_modules.html" target="_blank">Modules</a>”.</p>
<hr />
<p>At the end of July 2014, TC39 <sup><a href="#fn1" id="fnref1" target="_blank">[1]</a></sup> had another <a href="https://github.com/rwaldron/tc39-notes/tree/master/es6/2014-07" target="_blank">meeting</a>, during which the last details of the ECMAScript 6 (ES6) module syntax were finalized. This blog post gives an overview of the complete ES6 module system.</p>

<h2 id="module-systems-for-current-javascript">Module systems for current JavaScript  <a href="#module-systems-for-current-javascript" target="_blank">#</a></h2>
<p>JavaScript does not have built-in support for modules, but the community has created impressive work-arounds. The two most important (and unfortunately incompatible) standards are:</p>
<ul>
<li><strong>CommonJS Modules:</strong> The dominant implementation of this standard is <a href="http://nodejs.org/api/modules.html" target="_blank">in Node.js</a> (Node.js modules have a few features that go beyond CommonJS). Characteristics:
<ul>
<li>Compact syntax</li>
<li>Designed for synchronous loading</li>
<li>Main use: server</li>
</ul>
</li>
<li><strong>Asynchronous Module Definition (AMD):</strong> The most popular implementation of this standard is <a href="http://requirejs.org/" target="_blank">RequireJS</a>. Characteristics:
<ul>
<li>Slightly more complicated syntax, enabling AMD to work without eval() (or a compilation step).</li>
<li>Designed for asynchronous loading</li>
<li>Main use: browsers</li>
</ul>
</li>
</ul>
<p>The above is but a grossly simplified explanation of the current state of affairs. If you want more in-depth material, take a look at “<a href="http://addyosmani.com/writing-modular-js/" target="_blank">Writing Modular JavaScript With AMD, CommonJS & ES Harmony</a>” by Addy Osmani.</p>
<h2 id="ecmascript-6-modules">ECMAScript 6 modules  <a href="#ecmascript-6-modules" target="_blank">#</a></h2>
<p>The goal for ECMAScript 6 modules was to create a format that both users of CommonJS and of AMD are happy with:</p>
<ul>
<li>Similar to CommonJS, they have a compact syntax, a preference for single exports and support for cyclic dependencies.</li>
<li>Similar to AMD, they have direct support for asynchronous loading and configurable module loading.</li>
</ul>
<p>Being built into the language allows ES6 modules to go beyond CommonJS and AMD (details are explained later):</p>
<ul>
<li>Their syntax is even more compact than CommonJS’s.</li>
<li>Their structure can be statically analyzed (for static checking, optimization, etc.).</li>
<li>Their support for cyclic dependencies is better than CommonJS’s.</li>
</ul>
<p>The ES6 module standard has two parts:</p>
<ul>
<li>Declarative syntax (for importing and exporting)</li>
<li>Programmatic loader API: to configure how modules are loaded and to conditionally load modules</li>
</ul>
<h2 id="an-overview-of-the-es6-module-syntax">An overview of the ES6 module syntax  <a href="#an-overview-of-the-es6-module-syntax" target="_blank">#</a></h2>
<p>There are two kinds of exports: named exports (several per module) and default exports (one per module).</p>
<h3 id="named-exports-several-per-module">Named exports (several per module)  <a href="#named-exports-several-per-module" target="_blank">#</a></h3>
<p>A module can export multiple things by prefixing their declarations with the keyword <code>export</code>. These exports are distinguished by their names and are called <em>named exports</em>.</p>
<pre><code>//------ lib.js ------
export const sqrt = Math.sqrt;
export function square(x) {
    return x * x;
}
export function diag(x, y) {
    return sqrt(square(x) + square(y));
}

//------ main.js ------
import { square, diag } from 'lib';
console.log(square(11)); // 121
console.log(diag(4, 3)); // 5
</code></pre>
<p>There are other ways to specify named exports (which are explained later), but I find this one quite convenient: simply write your code as if there were no outside world, then label everything that you want to export with a keyword.</p>
<p>If you want to, you can also import the whole module and refer to its named exports via property notation:</p>
<pre><code>//------ main.js ------
import * as lib from 'lib';
console.log(lib.square(11)); // 121
console.log(lib.diag(4, 3)); // 5
</code></pre>
<p><strong>The same code in CommonJS syntax:</strong> For a while, I tried several clever strategies to be less redundant with my module exports in Node.js. Now I prefer the following simple but slightly verbose style that is reminiscent of the <a href="http://christianheilmann.com/2007/08/22/again-with-the-module-pattern-reveal-something-to-the-world/" target="_blank">revealing module pattern</a>:</p>
<pre><code>//------ lib.js ------
var sqrt = Math.sqrt;
function square(x) {
    return x * x;
}
function diag(x, y) {
    return sqrt(square(x) + square(y));
}
module.exports = {
    sqrt: sqrt,
    square: square,
    diag: diag,
};

//------ main.js ------
var square = require('lib').square;
var diag = require('lib').diag;
console.log(square(11)); // 121
console.log(diag(4, 3)); // 5
</code></pre>
<h3 id="default-exports-one-per-module">Default exports (one per module)  <a href="#default-exports-one-per-module" target="_blank">#</a></h3>
<p>Modules that only export single values are very popular in the Node.js community. But they are also common in frontend development where you often have constructors/classes for models, with one model per module. An ECMAScript 6 module can pick a <em>default export</em>, the most important exported value. Default exports are especially easy to import.</p>
<p>The following ECMAScript 6 module “is” a single function:</p>
<pre><code>//------ myFunc.js ------
export default function () { ... };

//------ main1.js ------
import myFunc from 'myFunc';
myFunc();
</code></pre>
<p>An ECMAScript 6 module whose default export is a class looks as follows:</p>
<pre><code>//------ MyClass.js ------
export default class { ... };

//------ main2.js ------
import MyClass from 'MyClass';
let inst = new MyClass();
</code></pre>
<p>Note: The operand of the default export declaration is an <a href="http://speakingjs.com/es5/ch07.html#expr_vs_stmt" target="_blank">expression</a>, it often does not have a name. Instead, it is to be identified via its module’s name.</p>
<h3 id="having-both-named-exports-and-a-default-export-in-a-module">Having both named exports and a default export in a module  <a href="#having-both-named-exports-and-a-default-export-in-a-module" target="_blank">#</a></h3>
<p>The following pattern is surprisingly common in JavaScript: A library is a single function, but additional services are provided via properties of that function. Examples include jQuery and Underscore.js. The following is a sketch of Underscore as a CommonJS module:</p>
<pre><code>//------ underscore.js ------
var _ = function (obj) {
    ...
};
var each = _.each = _.forEach =
    function (obj, iterator, context) {
        ...
    };
module.exports = _;

//------ main.js ------
var _ = require('underscore');
var each = _.each;
...
</code></pre>
<p>With ES6 glasses, the function <code>_</code> is the default export, while <code>each</code> and <code>forEach</code> are named exports. As it turns out, you can actually have named exports and a default export at the same time. As an example, the previous CommonJS module, rewritten as an ES6 module, looks like this:</p>
<pre><code>//------ underscore.js ------
export default function (obj) {
    ...
};
export function each(obj, iterator, context) {
    ...
}
export { each as forEach };

//------ main.js ------
import _, { each } from 'underscore';
...
</code></pre>
<p>Note that the CommonJS version and the ECMAScript 6 version are only roughly similar. The latter has a flat structure, whereas the former is nested. Which style you prefer is a matter of taste, but the flat style has the advantage of being statically analyzable (why that is good is explained below). The CommonJS style seems partially motivated by the need for objects as namespaces, a need that can often be fulfilled via ES6 modules and named exports.</p>
<h4 id="the-default-export-is-just-another-named-export">The default export is just another named export  <a href="#the-default-export-is-just-another-named-export" target="_blank">#</a></h4>
<p>The default export is actually just a named export with the special name <code>default</code>. That is, the following two statements are equivalent:</p>
<pre><code>import { default as foo } from 'lib';
import foo from 'lib';
</code></pre>
<p>Similarly, the following two modules have the same default export:</p>
<pre><code>//------ module1.js ------
export default 123;

//------ module2.js ------
const D = 123;
export { D as default };
</code></pre>
<h4 id="why-do-we-need-named-exports">Why do we need named exports?  <a href="#why-do-we-need-named-exports" target="_blank">#</a></h4>
<p>You may be wondering – why do we need named exports if we could simply default-export objects (like CommonJS)? The answer is that you can’t enforce a static structure via objects and lose all of the associated advantages (described in the next section).</p>
<h2 id="design-goals">Design goals  <a href="#design-goals" target="_blank">#</a></h2>
<p>If you want to make sense of ECMAScript 6 modules, it helps to understand what goals influenced their design. The major ones are:</p>
<ul>
<li>Default exports are favored</li>
<li>Static module structure</li>
<li>Support for both synchronous and asynchronous loading</li>
<li>Support for cyclic dependencies between modules</li>
</ul>
<p>The following subsections explain these goals.</p>
<h3 id="default-exports-are-favored">Default exports are favored  <a href="#default-exports-are-favored" target="_blank">#</a></h3>
<p>The module syntax suggesting that the default export “is” the module may seem a bit strange, but it makes sense if you consider that one major design goal was to make default exports as convenient as possible. Quoting <a href="http://esdiscuss.org/topic/moduleimport#content-0" target="_blank">David Herman</a>:</p>
<blockquote>
<p>ECMAScript 6 favors the single/default export style, and gives the sweetest syntax to importing the default. Importing named exports can and even should be slightly less concise.</p>
</blockquote>
<h3 id="static-module-structure">Static module structure  <a href="#static-module-structure" target="_blank">#</a></h3>
<p>In current JavaScript module systems, you have to execute the code in order to find out what the imports and exports are. That is the main reason why ECMAScript 6 breaks with those systems: by building the module system into the language, you can syntactically enforce a static module structure. Let’s first examine what that means and then what benefits it brings.</p>
<p>A module’s structure being static means that you can determine imports and exports at compile time (statically) – you only have to look at the source code, you don’t have to execute it. The following are two examples of how CommonJS modules can make that impossible. In the first example, you have to run the code to find out what it imports:</p>
<pre><code>var mylib;
if (Math.random()) {
    mylib = require('foo');
} else {
    mylib = require('bar');
}
</code></pre>
<p>In the second example, you have to run the code to find out what it exports:</p>
<pre><code>if (Math.random()) {
    exports.baz = ...;
}
</code></pre>
<p>ECMAScript 6 gives you less flexibility, it forces you to be static. As a result, you get several benefits <sup><a href="#fn2" id="fnref2" target="_blank">[2]</a></sup>, which are described next.</p>
<h4 id="benefit-1-faster-lookup">Benefit 1: faster lookup  <a href="#benefit-1-faster-lookup" target="_blank">#</a></h4>
<p>If you require a library in CommonJS, you get back an object:</p>
<pre><code>var lib = require('lib');
lib.someFunc(); // property lookup
</code></pre>
<p>Thus, accessing a named export via <code>lib.someFunc</code> means you have to do a property lookup, which is slow, because it is dynamic.</p>
<p>In contrast, if you import a library in ES6, you statically know its contents and can optimize accesses:</p>
<pre><code>import * as lib from 'lib';
lib.someFunc(); // statically resolved
</code></pre>
<h4 id="benefit-2-variable-checking">Benefit 2: variable checking  <a href="#benefit-2-variable-checking" target="_blank">#</a></h4>
<p>With a static module structure, you always statically know which variables are visible at any location inside the module:</p>
<ul>
<li>Global variables: increasingly, the only completely global variables will come from the language proper. Everything else will come from modules (including functionality from the standard library and the browser). That is, you statically know all global variables.</li>
<li>Module imports: You statically know those, too.</li>
<li>Module-local variables: can be determined by statically examining the module.</li>
</ul>
<p>This helps tremendously with checking whether a given identifier has been spelled properly. This kind of check is a popular feature of linters such as JSLint and JSHint; in ECMAScript 6, most of it can be performed by JavaScript engines.</p>
<p>Additionally, any access of named imports (such as <code>lib.foo</code>) can also be checked statically.</p>
<h4 id="benefit-3-ready-for-macros">Benefit 3: ready for macros  <a href="#benefit-3-ready-for-macros" target="_blank">#</a></h4>
<p>Macros are still on the roadmap for JavaScript’s future. If a JavaScript engine supports macros, you can add new syntax to it via a library. <a href="http://sweetjs.org" target="_blank">Sweet.js</a> is an experimental macro system for JavaScript. The following is an example from the Sweet.js website: a macro for classes.</p>
<pre><code>// Define the macro
macro class {
    rule {
        $className {
                constructor $cparams $cbody
                $($mname $mparams $mbody) ...
        }
    } =&gt; {
        function $className $cparams $cbody
        $($className.prototype.$mname
            = function $mname $mparams $mbody; ) ...
    }
}

// Use the macro
class Person {
    constructor(name) {
        this.name = name;
    }
    say(msg) {
        console.log(this.name + " says: " + msg);
    }
}
var bob = new Person("Bob");
bob.say("Macros are sweet!");
</code></pre>
<p>For macros, a JavaScript engine performs a preprocessing step before compilation: If a sequence of tokens in the token stream produced by the parser matches the pattern part of the macro, it is replaced by tokens generated via the body of macro. The preprocessing step only works if you are able to statically find macro definitions. Therefore, if you want to import macros via modules then they must have a static structure.</p>
<h4 id="benefit-4-ready-for-types">Benefit 4: ready for types  <a href="#benefit-4-ready-for-types" target="_blank">#</a></h4>
<p>Static type checking imposes constraints similar to macros: it can only be done if type definitions can be found statically. Again, types can only be imported from modules if they have a static structure.</p>
<p>Types are appealing because they enable statically typed fast dialects of JavaScript in which performance-critical code can be written. One such dialect is <a href="http://lljs.org" target="_blank">Low-Level JavaScript</a> (LLJS). It currently compiles to <a href="http://2ality.com/2013/02/asm-js.html" target="_blank">asm.js</a>.</p>
<h4 id="benefit-5-supporting-other-languages">Benefit 5: supporting other languages  <a href="#benefit-5-supporting-other-languages" target="_blank">#</a></h4>
<p>If you want to support compiling languages with macros and static types to JavaScript then JavaScript’s modules should have a static structure, for the reasons mentioned in the previous two sections.</p>
<h3 id="support-for-both-synchronous-and-asynchronous-loading">Support for both synchronous and asynchronous loading  <a href="#support-for-both-synchronous-and-asynchronous-loading" target="_blank">#</a></h3>
<p>ECMAScript 6 modules must work independently of whether the engine loads modules synchronously (e.g. on servers) or asynchronously (e.g. in browsers). Its syntax is well suited for synchronous loading, asynchronous loading is enabled by its static structure: Because you can statically determine all imports, you can load them before evaluating the body of the module (in a manner reminiscent of AMD modules).</p>
<h3 id="support-for-cyclic-dependencies-between-modules">Support for cyclic dependencies between modules  <a href="#support-for-cyclic-dependencies-between-modules" target="_blank">#</a></h3>
<p>Two modules A and B are <a href="http://en.wikipedia.org/wiki/Circular_dependency" target="_blank">cyclically dependent</a> on each other if both A (possibly indirectly/transitively) imports B and B imports A. If possible, cyclic dependencies should be avoided, they lead to A and B being <em>tightly coupled</em> – they can only be used and evolved together.</p>
<h4 id="why-support-cyclic-dependencies">Why support cyclic dependencies?  <a href="#why-support-cyclic-dependencies" target="_blank">#</a></h4>
<p>Cyclic dependencies are not inherently evil. Especially for objects, you sometimes even want this kind of dependency. For example, in some trees (such as DOM documents), parents refer to children and children refer back to parents. In libraries, you can usually avoid cyclic dependencies via careful design. In a large system, though, they can happen, especially during refactoring. Then it is very useful if a module system supports them, because then the system doesn’t break while you are refactoring.</p>
<p>The Node.js documentation acknowledges the importance of cyclic dependencies <sup><a href="#fn3" id="fnref3" target="_blank">[3]</a></sup> and Rob Sayre provides additional <a href="https://mail.mozilla.org/pipermail/es-discuss/2014-July/038250.html" target="_blank">evidence</a>:</p>
<blockquote>
<p>Data point: I once implemented a system like [ECMAScript 6 modules] for Firefox. I got <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=384168#c7" target="_blank">asked</a> for cyclic dependency support 3 weeks after shipping.</p>
<p>That system that Alex Fritze invented and I worked on is not perfect, and the syntax isn't very pretty. But <a href="https://developer.mozilla.org/en-US/docs/Mozilla/JavaScript_code_modules/Using" target="_blank">it's still getting used</a> 7 years later, so it must have gotten something right.</p>
</blockquote>
<p>Let’s see how CommonJS and ECMAScript 6 handle cyclic dependencies.</p>
<h4 id="cyclic-dependencies-in-commonjs">Cyclic dependencies in CommonJS  <a href="#cyclic-dependencies-in-commonjs" target="_blank">#</a></h4>
<p>In CommonJS, if a module B requires a module A whose body is currently being evaluated, it gets back A’s exports object in its current state (line #1 in the following example). That enables B to refer to properties of that object inside its exports (line #2). The properties are filled in after B’s evaluation is finished, at which point B’s exports work properly.</p>
<pre><code>//------ a.js ------
var b = require('b');
exports.foo = function () { ... };

//------ b.js ------
var a = require('a'); // (1)
// Can’t use a.foo in module body,
// but it will be filled in later
exports.bar = function () {
    a.foo(); // OK (2)
};

//------ main.js ------
var a = require('a');
</code></pre>
<p>As a general rule, keep in mind that with cyclic dependencies, you can’t access imports in the body of the module. That is inherent to the phenomenon and doesn’t change with ECMAScript 6 modules.</p>
<p>The limitations of the CommonJS approach are:</p>
<ul>
<li>
<p>Node.js-style single-value exports don’t work. In Node.js, you can export single values instead of objects, like this:<br />
<code>module.exports = function () { ... }</code><br />
If you did that in module A, you wouldn’t be able to use the exported function in module B, because B’s variable <code>a</code> would still refer to A’s original exports object.</p>
</li>
<li>
<p>You can’t use named exports directly. That is, module B can’t import <code>a.foo</code> like this:<br />
<code>var foo = require('a').foo;</code><br />
<code>foo</code> would simply be <code>undefined</code>. In other words, you have no choice but to refer to <code>foo</code> via the exports object <code>a</code>.</p>
</li>
</ul>
<p>CommonJS has one unique feature: you can export before importing. Such exports are guaranteed to be accessible in the bodies of importing modules. That is, if A did that, they could be accessed in B’s body. However, exporting before importing is rarely useful.</p>
<h4 id="cyclic-dependencies-in-ecmascript-6">Cyclic dependencies in ECMAScript 6  <a href="#cyclic-dependencies-in-ecmascript-6" target="_blank">#</a></h4>
<p>In order to eliminate the aforementioned two limitations, ECMAScript 6 modules export bindings, not values. That is, the connection to variables declared inside the module body remains live. This is demonstrated by the following code.</p>
<pre><code>//------ lib.js ------
export let counter = 0;
export function inc() {
    counter++;
}

//------ main.js ------
import { inc, counter } from 'lib';
console.log(counter); // 0
inc();
console.log(counter); // 1
</code></pre>
<p>Thus, in the face of cyclic dependencies, it doesn’t matter whether you access a named export directly or via its module: There is an indirection involved in either case and it always works.</p>
<h2 id="more-on-importing-and-exporting">More on importing and exporting  <a href="#more-on-importing-and-exporting" target="_blank">#</a></h2>
<h3 id="importing">Importing  <a href="#importing" target="_blank">#</a></h3>
<p>ECMAScript 6 provides the following ways of importing <sup><a href="#fn4" id="fnref4" target="_blank">[4]</a></sup>:</p>
<pre><code>// Default exports and named exports
import theDefault, { named1, named2 } from 'src/mylib';
import theDefault from 'src/mylib';
import { named1, named2 } from 'src/mylib';

// Renaming: import named1 as myNamed1
import { named1 as myNamed1, named2 } from 'src/mylib';

// Importing the module as an object
// (with one property per named export)
import * as mylib from 'src/mylib';

// Only load the module, don’t import anything
import 'src/mylib';
</code></pre>
<h3 id="exporting">Exporting  <a href="#exporting" target="_blank">#</a></h3>
<p>There are two ways in which you can export things that are inside the current module <sup><a href="#fn5" id="fnref5" target="_blank">[5]</a></sup>. On one hand, you can mark declarations with the keyword <code>export</code>.</p>
<pre><code>export var myVar1 = ...;
export let myVar2 = ...;
export const MY_CONST = ...;

export function myFunc() {
    ...
}
export function* myGeneratorFunc() {
    ...
}
export class MyClass {
    ...
}
</code></pre>
<p>The “operand” of a default export is an expression (including function expressions and class expressions). Examples:</p>
<pre><code>export default 123;
export default function (x) {
    return x
};
export default x =&gt; x;
export default class {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
};
</code></pre>
<p>On the other hand, you can list everything you want to export at the end of the module (which is once again similar in style to the revealing module pattern).</p>
<pre><code>const MY_CONST = ...;
function myFunc() {
    ...
}

export { MY_CONST, myFunc };
</code></pre>
<p>You can also export things under different names:</p>
<pre><code>export { MY_CONST as THE_CONST, myFunc as theFunc };
</code></pre>
<p>Note that you can’t use <a href="http://speakingjs.com/es5/ch07.html#identifiers" target="_blank">reserved words</a> (such as <code>default</code> and <code>new</code>) as variable names, but you can use them as names for exports (you can also use them as property names in ECMAScript 5). If you want to directly import such named exports, you have to rename them to proper variables names.</p>
<h3 id="re-exporting">Re-exporting  <a href="#re-exporting" target="_blank">#</a></h3>
<p>Re-exporting means adding another module’s exports to those of the current module. You can either add all of the other module’s exports:</p>
<pre><code>export * from 'src/other_module';
</code></pre>
<p>Or you can be more selective (optionally while renaming):</p>
<pre><code>export { foo, bar } from 'src/other_module';

// Export other_module’s foo as myFoo
export { foo as myFoo, bar } from 'src/other_module';
</code></pre>
<h2 id="eval-and-modules">eval() and modules  <a href="#eval-and-modules" target="_blank">#</a></h2>
<p><code>eval()</code> does not support module syntax. It parses its argument according to the Script grammar rule and scripts don’t support module syntax (why is explained later). If you want to evaluate module code, you can use the module loader API (described next).</p>
<h2 id="the-ecmascript-6-module-loader-api">The ECMAScript 6 module loader API  <a href="#the-ecmascript-6-module-loader-api" target="_blank">#</a></h2>
<p>In addition to the declarative syntax for working with modules, there is also a <a href="https://people.mozilla.org/~jorendorff/es6-draft.html#sec-loader-objects" target="_blank">programmatic API</a>. It allows you to:</p>
<ul>
<li>Programmatically work with modules and scripts</li>
<li>Configure module loading</li>
</ul>
<p>Loaders handle resolving <em>module specifiers</em> (the string IDs at the end of <code>import...from</code>), loading modules, etc. Their constructor is <code>Reflect.Loader</code>. Each platform keeps a customized instance in the global variable <code>System</code> (the <em>system loader</em>), which implements its specific style of module loading.</p>
<h3 id="importing-modules-and-loading-scripts">Importing modules and loading scripts  <a href="#importing-modules-and-loading-scripts" target="_blank">#</a></h3>
<p>You can programmatically import a module, via an API based on <a href="http://www.html5rocks.com/en/tutorials/es6/promises/" target="_blank">ES6 promises</a>:</p>
<pre><code>System.import('some_module')
.then(some_module =&gt; {
    // Use some_module
})
.catch(error =&gt; {
    ...
});
</code></pre>
<p><code>System.import()</code> enables you to:</p>
<ul>
<li>Use modules inside <code>&lt;script&gt;</code> elements (where module syntax is not supported, consult Sect. “<a href="#further_information" target="_blank">Further information</a>” for details).</li>
<li>Load modules conditionally.</li>
</ul>
<p><code>System.import()</code> retrieves a single module, you can use <code>Promise.all()</code> to import several modules:</p>
<pre><code>Promise.all(
    ['module1', 'module2', 'module3']
    .map(x =&gt; System.import(x)))
.then(([module1, module2, module3]) =&gt; {
    // Use module1, module2, module3
});
</code></pre>
<p>More loader methods:</p>
<ul>
<li><a href="https://people.mozilla.org/~jorendorff/es6-draft.html#sec-reflect.loader.prototype.module" target="_blank"><code>System.module(source, options?)</code></a> evaluates the JavaScript code in <code>source</code> to a module (which is delivered asynchronously via a promise).</li>
<li><a href="https://people.mozilla.org/~jorendorff/es6-draft.html#sec-reflect.loader.prototype.set" target="_blank"><code>System.set(name, module)</code></a> is for registering a module (e.g. one you have created via <code>System.module()</code>).</li>
<li><a href="https://people.mozilla.org/~jorendorff/es6-draft.html#sec-reflect.loader.prototype.define" target="_blank"><code>System.define(name, source, options?)</code></a> both evaluates the module code in <code>source</code> and registers the result.</li>
</ul>
<h3 id="configuring-module-loading">Configuring module loading  <a href="#configuring-module-loading" target="_blank">#</a></h3>
<p>The module loader API has various hooks for configuration. It is still work in progress. A first system loader for browsers is currently being implemented and tested. The goal is to figure out how to best make module loading configurable.</p>
<p>The loader API will permit many customizations of the loading process. For example:</p>
<ol>
<li>Lint modules on import (e.g. via JSLint or JSHint).</li>
<li>Automatically translate modules on import (they could contain CoffeeScript or TypeScript code).</li>
<li>Use legacy modules (AMD, Node.js).</li>
</ol>
<p>Configurable module loading is an area where Node.js and CommonJS are limited.</p>
<h2 id="further-information">Further information  <a href="#further-information" target="_blank">#</a></h2>
<p>The following content answers two important questions related to ECMAScript 6 modules: How do I use them today? How do I embed them in HTML?</p>
<ul>
<li>
<p><strong>“<a href="http://2ality.com/2014/08/es6-today.html" target="_blank">Using ECMAScript 6 today</a>”</strong> gives an overview of ECMAScript 6 and explains how to compile it to ECMAScript 5. If you are interested in the latter, start reading in <a href="http://2ality.com/2014/08/es6-today.html#using_ecmascript_6_today" target="_blank">Sect. 2</a>. One intriguing minimal solution is the <a href="https://github.com/esnext/es6-module-transpiler" target="_blank">ES6 Module Transpiler</a> which only adds ES6 module syntax to ES5 and compiles it to either AMD or CommonJS.</p>
</li>
<li>
<p><strong>Embedding ES6 modules in HTML:</strong> The code inside <code>&lt;script&gt;</code> elements does not support module syntax, because the element’s synchronous nature is incompatible with the asynchronicity of modules. Instead, you need to use the new <code>&lt;module&gt;</code> element. The blog post “<a href="http://2ality.com/2013/11/es6-modules-browsers.html" target="_blank">ECMAScript 6 modules in future browsers</a>” explains how <code>&lt;module&gt;</code> works. It has several significant advantages over <code>&lt;script&gt;</code> and can be polyfilled in its alternative version <code>&lt;script type="module"&gt;</code>.</p>
</li>
<li>
<p><strong>CommonJS vs. ES6:</strong> “<a href="http://jsmodules.io/" target="_blank">JavaScript Modules</a>” (by <a href="https://github.com/wycats/jsmodules" target="_blank">Yehuda Katz</a>) is a quick intro to ECMAScript 6 modules. Especially interesting is a <a href="http://jsmodules.io/cjs.html" target="_blank">second page</a> where CommonJS modules are shown side by side with their ECMAScript 6 versions.</p>
</li>
</ul>
<h2 id="benefits-of-ecmascript-6-modules">Benefits of ECMAScript 6 modules  <a href="#benefits-of-ecmascript-6-modules" target="_blank">#</a></h2>
<p>At first glance, having modules built into ECMAScript 6 may seem like a boring feature – after all, we already have several good module systems. But ECMAScript 6 modules have features that you can’t add via a library, such as a very compact syntax and a static module structure (which helps with optimizations, static checking and more). They will also – hopefully – end the fragmentation between the currently dominant standards CommonJS and AMD.</p>
<p>Having a single, native standard for modules means:</p>
<ul>
<li>No more UMD (<a href="https://github.com/umdjs/umd" target="_blank">Universal Module Definition</a>): UMD is a name for patterns that enable the same file to be used by several module systems (e.g. both CommonJS and AMD). Once ES6 is the only module standard, UMD becomes obsolete.</li>
<li>New browser APIs become modules instead of global variables or properties of <code>navigator</code>.</li>
<li>No more objects-as-namespaces: Objects such as <code>Math</code> and <code>JSON</code> serve as namespaces for functions in ECMAScript 5. In the future, such functionality can be provided via modules.</li>
</ul>
<p><strong>Acknowledgements:</strong> Thanks to Domenic Denicola for <a href="http://esdiscuss.org/topic/es6-module-syntax-done#content-2" target="_blank">confirming</a> the final module syntax. Thanks for corrections of this blog post go to: Guy Bedford, John K. Paul, Mathias Bynens, Michael Ficarra.</p>
<h2 id="references">References  <a href="#references" target="_blank">#</a></h2>
<hr />
<section>
<ol>
<li id="fn1"><p><a href="http://2ality.com/2011/06/ecmascript.html" target="_blank">A JavaScript glossary: ECMAScript, TC39, etc.</a> <a href="#fnref1" target="_blank">↩︎</a></p>
</li>
<li id="fn2"><p>“<a href="http://calculist.org/blog/2012/06/29/static-module-resolution/" target="_blank">Static module resolution</a>” by David Herman <a href="#fnref2" target="_blank">↩︎</a></p>
</li>
<li id="fn3"><p>“<a href="http://nodejs.org/api/modules.html#modules_cycles" target="_blank">Modules: Cycles</a>” in the Node.js API documentation <a href="#fnref3" target="_blank">↩︎</a></p>
</li>
<li id="fn4"><p>“<a href="https://people.mozilla.org/~jorendorff/es6-draft.html#sec-imports" target="_blank">Imports</a>” (ECMAScript 6 specification) <a href="#fnref4" target="_blank">↩︎</a></p>
</li>
<li id="fn5"><p>“<a href="https://people.mozilla.org/~jorendorff/es6-draft.html#sec-exports" target="_blank">Exports</a>” (ECMAScript 6 specification) <a href="#fnref5" target="_blank">↩︎</a></p>
</li>
</ol>
</section>

<a href="https://stackoverflow.com/questions/41769880/how-to-manually-add-a-path-to-be-resolved-in-eslintrc">https://stackoverflow.com/questions/41769880/how-to-manually-add-a-path-to-be-resolved-in-eslintrc</a><div id="articleHeader"><h1>How to manually add a path to be resolved in eslintrc</h1></div>

<p>I have a folder in my project <code>main</code> that I am resolving like a module. For instance <code>import x from 'main/src'</code> imports <code>main/src/index.js</code>. This is done through webpack's resolve alias configuration.</p>

<p>An issue I am having is getting rid of the errors via eslint. I know eslint provides a webpack resolve plugin, however, I've been having trouble getting it to work. I suspect it is because I am on webpack 2 and using es6 in my webpack config files.</p>

<p>Is there a manual way to write a resolve setting that fixes this problem for my eslint?</p>

<hr />

<p>The only other hack I've seen work is using <code>import/core-modules</code> but then I have to list out every folder in the subdirectory tree <code>main/src/bar</code>, <code>main/src/foo</code>. This would not be ideal.</p>
    
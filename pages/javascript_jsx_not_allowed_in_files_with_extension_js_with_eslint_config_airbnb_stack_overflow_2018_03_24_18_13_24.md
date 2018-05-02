<a href="https://stackoverflow.com/questions/43031126/jsx-not-allowed-in-files-with-extension-js-with-eslint-config-airbnb">https://stackoverflow.com/questions/43031126/jsx-not-allowed-in-files-with-extension-js-with-eslint-config-airbnb</a><div id="articleHeader"><h1>JSX not allowed in files with extension ' .js' with eslint-config-airbnb</h1></div>

<p>I've installed <a href="https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb" target="_blank">eslint-config-airbnb</a> that is supposed to pre configure ESLINT for React:</p>

<blockquote>
  <p>Our default export contains all of our ESLint rules, including
  ECMAScript 6+ and React. It requires eslint, eslint-plugin-import,
  eslint-plugin-react, and eslint-plugin-jsx-a11y.</p>
</blockquote>

<p>My <code>.eslintrc</code> extending its configuration:</p>

<pre><code>{ "extends": "eslint-config-airbnb",
  "env": {
    "browser": true,
    "node": true,
    "mocha": true
  },
  "rules": {
    "new-cap": [2, { "capIsNewExceptions": ["List", "Map", "Set"] }],
    "react/no-multi-comp": 0,
    "import/default": 0,
    "import/no-duplicates": 0,
    "import/named": 0,
    "import/namespace": 0,
    "import/no-unresolved": 0,
    "import/no-named-as-default": 2,
    "comma-dangle": 0,  // not sure why airbnb turned this on. gross!
    "indent": [2, 2, {"SwitchCase": 1}],
    "no-console": 0,
    "no-alert": 0,
    "linebreak-style": 0
  },
  "plugins": [
    "react", "import"
  ],
  "settings": {
    "import/parser": "babel-eslint",
    "import/resolve": {
      "moduleDirectory": ["node_modules", "src"]
    }
  },
  "globals": {
    "__DEVELOPMENT__": true,
    "__CLIENT__": true,
    "__SERVER__": true,
    "__DISABLE_SSR__": true,
    "__DEVTOOLS__": true,
    "socket": true,
    "webpackIsomorphicTools": true
  }
}</code></pre>

<p>Unfortunatelly I'm getting the following error when linting a .js file with React JSX code inside it:</p>

<pre><code> error  JSX not allowed in files with extension '.js'              react/jsx-filename-extension</code></pre>

<p>Wasn't eslint-config-airbnb configured react to support JSX already, as stated ? </p>

<p>What should be done to remove that error ?</p>
    
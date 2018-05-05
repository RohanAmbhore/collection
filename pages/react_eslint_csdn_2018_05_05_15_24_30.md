<a href="https://blog.csdn.net/gdp12315_gu/article/details/54098810">https://blog.csdn.net/gdp12315_gu/article/details/54098810</a><div id="articleHeader"><h1>React用ESLint代码检测 常见问题</h1></div>
	<div>
		<div>
												2017年01月05日 22:18:26
			<div>
				阅读数：7511
											</div>
		
	
	
		
                    
                <p>在package.json中 添加 ESLint依赖，</p>



<pre><code>"eslint": "3.9.0",
    "eslint-config-airbnb": "12.0.0",
    "eslint-plugin-import": "2.0.1",
    "eslint-plugin-jsx-a11y": "2.2.3",
    "eslint-plugin-react": "6.4.1",
    "eslint-plugin-redux-saga": "0.1.5",</code></pre>





<pre><code>"eslintConfig": {
    "parser": "babel-eslint",
    "extends": "airbnb",
    "env": {
      "browser": true,
      "node": true,
      "mocha": true,
      "es6": true
    },
    "plugins": [
      "redux-saga",
      "react",
      "jsx-a11y"
    ],
    "parserOptions": {
      "ecmaVersion": 6,
      "sourceType": "module",
      "ecmaFeatures": {
        "jsx": true
      }
    },
    "rules": {
      "arrow-parens": [
        "error",
        "always"
      ],
      "arrow-body-style": [
        2,
        "as-needed"
      ],
      "comma-dangle": [
        2,
        "always-multiline"
      ],
      "indent": 0,
      "linebreak-style": [
        "error",
        "windows"
      ],
      "no-tabs": 0,
      "no-param-reassign": [
        "error",
        {
          "props": false
        }
      ],
      "no-constant-condition": [
        "error",
        {
          "checkLoops": false
        }
      ],
      "object-shorthand": 0,
      "no-unused-vars":[2, { "args": "none" }],
      "import/imports-first": 0,
      "import/newline-after-import": 0,
      "import/no-dynamic-require": 0,
      "import/no-extraneous-dependencies": 0,
      "import/no-named-as-default": 0,
      "import/no-unresolved": 0,
      "import/prefer-default-export": 0,
      "import/extensions": 0,
      "jsx-a11y/aria-props": 2,
      "jsx-a11y/heading-has-content": 0,
      "jsx-a11y/href-no-hash": 2,
      "jsx-a11y/label-has-for": 2,
      "jsx-a11y/mouse-events-have-key-events": 2,
      "jsx-a11y/role-has-required-aria-props": 2,
      "jsx-a11y/role-supports-aria-props": 2,
      "max-len": 0,
      "newline-per-chained-call": 0,
      "no-console": 1,
      "no-use-before-define": 0,
      "prefer-template": 2,
      "class-methods-use-this": 0,
      "react/forbid-prop-types": 0,
      "react/jsx-first-prop-new-line": [
        2,
        "multiline"
      ],
      "react/jsx-filename-extension": 0,
      "react/jsx-no-target-blank": 0,
      "react/require-extension": 0,
      "react/self-closing-comp": 0,
      "react/jsx-indent": [
        2,
        "tab"
      ],
      "react/jsx-indent-props": [
        2,
        "tab"
      ],
      "react/prefer-stateless-function": 0,
      "redux-saga/no-yield-in-race": 2,
      "redux-saga/yield-effects": 2,
      "require-yield": 0
    }</code></pre>



<h2 id="1-eslint运行">1 ESLint运行</h2>



<pre><code>eslint --color app/**/*.js</code></pre>

<p>添加  –fix  可以自动修复一些简单错误，一些规则  如： <br />
no-extra-parens   禁止冗余的括号 <br />
no-extra-semi     禁止多余的分号</p>

<p>点击这里 了解具体规则， <br />
<a href="http://eslint.cn/docs/rules/" target="_blank">http://eslint.cn/docs/rules/</a> </p>



<h2 id="2-常见错误">2 常见错误</h2>

<p>具体规则要求参考 <br />
<a href="https://github.com/yannickcr/eslint-plugin-react" target="_blank">https://github.com/yannickcr/eslint-plugin-react</a> <br />
<a href="https://github.com/evcohen/eslint-plugin-jsx-a11y" target="_blank">https://github.com/evcohen/eslint-plugin-jsx-a11y</a></p>



<h4 id="jsx-no-bind">jsx-no-bind</h4>

<p>含义： 将自定义函数在构造函数中绑定， 如果JSX prop 中存在bind，则每次render 生成一个新的function，这样会影响性能。 <br />
解决办法， 在构造函数中 绑定 this</p>

<pre><code>class Foo extends React.Component {
  constructor() {
    super();
    this._onClick = this._onClick.bind(this);
  }
  render() {
    return (
      &lt;div onClick={this._onClick}&gt;
        Hello!
      &lt;/div&gt;
    );
  }
  _onClick() {
    // Do whatever you like, referencing "this" as appropriate
  }
}</code></pre>



<h4 id="sort-comp">sort-comp</h4>

<p>含义：React中函数的先后顺序 <br />
默认的排序，其中everything-else是自定义函数</p>



<pre><code>{
  order: [
    'static-methods',
    'lifecycle',
    'everything-else',
    'render'
  ],
  groups: {
    lifecycle: [
      'displayName',
      'propTypes',
      'contextTypes',
      'childContextTypes',
      'mixins',
      'statics',
      'defaultProps',
      'constructor',
      'getDefaultProps',
      'getInitialState',
      'state',
      'getChildContext',
      'componentWillMount',
      'componentDidMount',
      'componentWillReceiveProps',
      'shouldComponentUpdate',
      'componentWillUpdate',
      'componentDidUpdate',
      'componentWillUnmount'
    ]
  }
}
static-methods is a spe</code></pre>



<h4 id="通过注释的方式-解决">通过注释的方式 解决</h4>

<p>/* eslint-disable */      某文件 ESLint不检测</p>

<p>/* global variable:false */  设置全局变量</p>            
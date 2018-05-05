<a href="https://github.com/babel/babel-eslint/issues/487">https://github.com/babel/babel-eslint/issues/487</a><div id="articleHeader"><h1>              Class properties resulting in false positive            #487    </h1></div>


  <div>
    
    <div>
        <a href="/damianobarbati" target="_blank">damianobarbati</a>  opened this Issue
        <relative-time>on Jun 13, 2017</relative-time>
        · 52 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      


  
    
      

          <p>In the following JS I get a "no-undef" on webpack compilation because of <code>inputPicks</code> and <code>contextTypes</code> static class properties but it does not happen firing ESLint from command line.</p>
<pre><code>export default class Input extends React.Component {
    static contextTypes = {
        formName: PropTypes.string.isRequired,
    }

    static inputPicks = ['minLength', 'maxLength', 'pattern']

    constructor(props) {
        super(props, context);
    }
...and so on
</code></pre>
<p>Package.json</p>
<pre><code>    "eslintConfig": {
        "parser": "babel-eslint",
        "parserOptions": {
            "ecmaVersion": 2017,
            "sourceType": "module",
            "impliedStrict": true,
            "ecmaFeatures": {
                "jsx": true,
                "experimentalObjectRestSpread": true
            }
        },
        "env": {
            "browser": true,
            "node": true,
            "jest": true,
            "es6": true
        },
        "plugins": [
            "import",
            "react",
            "jest"
        ],
        "extends": [
            "eslint:recommended",
            "plugin:react/recommended",
            "plugin:jest/recommended"
        ],
        "rules": {
            "no-console": "off",
            "no-unused-vars": "off",
            "no-unsafe-finally": "off",
            "react/no-unescaped-entities": "off",
            "react/prop-types": "off"
        }
    },
</code></pre>
<p>Dependencies:</p>
<pre><code>    "devDependencies": {
        "autobind-decorator": "^1.3.4",
        "autoprefixer": "^7.1.1",
        "babel-core": "^6.7.4",
        "babel-eslint": "^7.1.1",
        "babel-loader": "7.0.0",
        "babel-plugin-react-css-modules": "^2.6.0",
        "babel-plugin-syntax-class-properties": "^6.13.0",
        "babel-plugin-transform-decorators-legacy": "^1.3.4",
        "babel-polyfill": "^6.20.0",
        "babel-preset-env": "2.0.0-alpha.3",
        "babel-preset-react": "^6.5.0",
        "babel-preset-stage-0": "^6.16.0",
        "babili": "^0.1.2",
        "babili-webpack-plugin": "^0.1.1",
        "clean-webpack-plugin": "0.1.16",
        "compression-webpack-plugin": "^0.4.0",
        "css-loader": "^0.28.4",
        "cssnano": "^3.10.0",
        "eslint": "^4.0.0",
        "eslint-loader": "^1.6.1",
        "eslint-plugin-import": "^2.2.0",
        "eslint-plugin-jest": "^20.0.3",
        "eslint-plugin-react": "^7.0.1",
        "extract-text-webpack-plugin": "^2.1.0",
        "favicons-webpack-plugin": "^0.0.7",
        "file-loader": "^0.11.1",
        "history": "^4.6.1",
        "html-webpack-plugin": "^2.25.0",
        "img-loader": "^2.0.0",
        "json-loader": "^0.5.4",
        "material-ui": "^0.18.1",
        "material-ui-community-icons": "^0.15.0",
        "node-sass": "^4.1.1",
        "open-browser-webpack-plugin": "^0.0.5",
        "postcss-load-config": "^1.1.0",
        "postcss-loader": "^2.0.5",
        "postcss-scss": "^1.0.0",
        "query-string": "^4.3.4",
        "react": "^15.4.1",
        "react-addons-perf": "^15.4.2",
        "react-create-app": "^1.0.3",
        "react-create-store": "^1.0.4",
        "react-dimensions": "^1.3.0",
        "react-dom": "^15.4.1",
        "react-ga": "^2.2.0",
        "react-highcharts": "^12.0.0",
        "react-moment": "^0.2.4",
        "react-redux": "^5.0.1",
        "react-router": "^4.1.1",
        "react-router-dom": "^4.1.1",
        "react-router-redux": "next",
        "react-sizeme": "^2.3.2",
        "react-svg-inline": "^2.0.0",
        "react-swipeable-views": "^0.12.3",
        "react-tap-event-plugin": "^2.0.0",
        "react-transition-group": "^1.1.3",
        "recompose": "^0.23.4",
        "redux": "^3.6.0",
        "redux-action-buffer": "^1.0.1",
        "redux-actions": "^2.0.3",
        "redux-devtools-extension": "^2.13.2",
        "redux-logger": "^3.0.6",
        "redux-persist": "^4.1.0",
        "redux-persist-crosstab": "^3.5.2",
        "redux-promise": "^0.5.3",
        "redux-thunk": "^2.1.0",
        "sass-loader": "^6.0.5",
        "string-replace-loader": "^1.2.0",
        "style-loader": "^0.18.2",
        "stylelint-config-sass-guidelines": "^2.1.0",
        "stylelint-config-standard": "^16.0.0",
        "stylelint-scss": "^1.4.4",
        "stylelint-webpack-plugin": "^0.7.0",
        "url-loader": "^0.5.8",
        "webpack": "^2.5.1",
        "webpack-bundle-analyzer": "^2.8.2",
        "webpack-chunk-hash": "^0.4.0",
        "webpack-notifier": "^1.5.0"
    }
</code></pre>
      
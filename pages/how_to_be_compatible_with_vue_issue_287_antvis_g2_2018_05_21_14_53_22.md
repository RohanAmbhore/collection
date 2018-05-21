<a href="https://github.com/antvis/g2/issues/287">https://github.com/antvis/g2/issues/287</a><div id="articleHeader"><h1>              How to be compatible with Vue?             #287    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/NoraGithub" target="_blank">NoraGithub</a>  opened this Issue
        <relative-time>on Dec 14, 2017</relative-time>
        · 9 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          

          

  


  


  


  

    
  

  




  

    
  

    



    

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <div><pre>// index.vue
// father component
&lt;template&gt;
    &lt;pivotChart&gt;&lt;/pivotChart&gt;
&lt;/template&gt;
&lt;script&gt;
const pivotChart = ()=&gt;import( './g2pivotChart')
export default{
    ...
    components:{
        "pivotChart":pivotChart
    }
    ...
}
&lt;/script&gt;</pre></div>
<div><pre>// g2pivotChar.vue
// son component
&lt;template&gt;
&lt;/template&gt;
&lt;script&gt;
import G2 from './g2'
export default {
...
}
&lt;/script&gt;</pre></div>
<div><pre>// ./g2.js
// customed
const G2 = require('@antv/g2');
G2.track(false);
const Facets = require('@antv/g2/src/facet/index');
const Util = require('@antv/g2/src/util');
const Nested = require('./nested');
Facets.Nested = Nested;

G2.Chart.prototype.facet = function(type, cfg) {
    const cls = Facets[Util.upperFirst(type)];
    if (!cls) {
      throw new Error('Not support such type of facets as: ' + type);
    }
    const preFacets = this.get('facets');
    if (preFacets) {
      preFacets.destroy();
    }
    cfg.chart = this;
    const facets = new cls(cfg);
    this.set('facets', facets);
  }

module.exports = G2;
</pre></div>
<div><pre>// ./nested.js
// customed
const Base = require('@antv/g2/src/facet/base');
...
...
class Nested extends Base {
    ...
    ...
}
module.exports = Nested;</pre></div>
<div><pre>// webpack.base.config.js
const path = require('path')
const webpack = require('webpack')
const vueConfig = require('./vue-loader.config')
const ExtractTextPlugin = require('extract-text-webpack-plugin')
const FriendlyErrorsPlugin = require('friendly-errors-webpack-plugin')
var utils = require('./utils')

const isProd = process.env.NODE_ENV === 'production'

function resolve(dir) {
  return path.join(__dirname, '..', dir)
}

module.exports = {
  devtool: isProd
    ? false
    : '#cheap-module-source-map',
  output: {
    path: path.resolve(__dirname, '../dist'),
    publicPath: '/dist/',
    filename: '[name].[chunkhash].js'
  },
  resolve: {
    alias: {
      'public': path.resolve(__dirname, '../public'),
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
      '^': resolve('src/components'),
      'jquery': 'jquery'
    },
    extensions: ['.js', '.vue', '.json']
  },
  module: {
    noParse: /es6-promise\.js$/, // avoid webpack shimming process
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: vueConfig
      },
      {
        test: /\.js$/,
        loader: 'babel-loader',
        exclude: [/node_modules\/(?!(@antv\/g2\/src)\/).*/,/node_modules\/@antv\/g2\/node_modules/]
        //https://github.com/webpack/webpack/issues/2031#issuecomment-219040479
      },
      {
        test: /\.(png|jpg|gif|svg)$/,
        loader: 'url-loader',
        options: {
          limit: 10000,
          name: '[name].[ext]?[hash]'
        }
      },
      {
        test: /\.css$/,
        use: isProd
          ? ExtractTextPlugin.extract({
              use: 'css-loader?minimize',
              fallback: 'vue-style-loader'
            })
          : ['vue-style-loader', 'css-loader']
      },
      {
        test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
        loader: 'url-loader',
        options: {
          limit: 10000,
          name: utils.assetsPath('fonts/[name].[hash:7].[ext]')
        }
      }
    ]
  },
  performance: {
    maxEntrypointSize: 300000,
    hints: isProd ? 'warning' : false
  },
  plugins: isProd
    ? [
        new webpack.optimize.UglifyJsPlugin({
          compress: { warnings: false }
        }),
        new webpack.optimize.ModuleConcatenationPlugin(),
        new ExtractTextPlugin({
          filename: 'common.[chunkhash].css'
        })
      ]
    : [
        new FriendlyErrorsPlugin()
      ]
}
</pre></div>
<div><pre>.barbelrc
{
  "presets": [
    ["env", { "modules": false ,
    "targets": {
        "browsers": ["&gt; 1%", "last 2 versions", "not ie &lt;= 8"],
        "node":"current"
      }
    }], "stage-2"
  ],
  "plugins": ["transform-runtime","syntax-dynamic-import"],
  "env": {
    "test": {
      "presets": ["env", "stage-2"],
      "plugins": ["istanbul"]
    }
  }

}
</pre></div>
<p>If this is not clear enough, I'd better create a repo to show the code.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    
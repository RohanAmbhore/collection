<a href="https://scrimba.com/">https://scrimba.com/</a><div id="articleHeader"><h1>interactive coding screencasts</h1></div><p>the easiest way to teach and learn code</p><div><a href="/c/cKp6LhL" target="_blank">Read more</a></div></header><header><h2><a href="/playlist/pRB9Hw" target="_blank">Staff picks</a></h2><div>The latest and greatest from our community!</div></header><div><div><div><div><div><div><b>tutorial</b><b>index.js</b><b>index.html</b></div><pre><i> 1</i>  // like a number line
<i> 2</i>  // 0---1---2---3
<i> 3</i>  var roomsArray = ["Girl's room", "John's room", "Master bedroom"];
<i> 4</i>  
<i> 5</i>  // for(;;) loop
<i> 6</i>  for (let position = 0; position &lt; roomsArray.length; position = position + 1) {
<i> 7</i>      let room = roomsArray[position]
<i> 8</i>      if (room !== "John's room") {
<i> 9</i>          //console.log(room)    
<i>10</i>      }
<i>11</i>  }
<i>12</i>  
<i>13</i>  // "for of" loop
<i>14</i>  for(let name of roomsArray) {
<i>15</i>      // console.log(name)
<i>16</i>  }
<i>17</i>  
<i>18</i>  // "for in" loop</pre></div>25:43</div></div><div><div><div><div><b>tutorial</b><b>index.html</b><b>index.css</b></div><pre><i> 1</i>  &lt;html&gt;
<i> 2</i>      &lt;head&gt;
<i> 3</i>          &lt;link rel="stylesheet" href="index.css"&gt;
<i> 4</i>      &lt;/head&gt;
<i> 5</i>      &lt;body&gt;
<i> 6</i>          &lt;!-- inline styles --&gt;
<i> 7</i>          &lt;h1 style="color: blue;"&gt;Let's change color!&lt;/h1&gt;
<i> 8</i>          &lt;div style="color: red;"&gt;Some other text&lt;/div&gt;
<i> 9</i>          &lt;p style="color: green;"&gt;I like cheese.&lt;/p&gt;
<i>10</i>          
<i>11</i>          &lt;!-- uses classes frmo a stylesheet --&gt;
<i>12</i>          &lt;p class="wonderful"&gt;I like train sets&lt;/p&gt;
<i>13</i>          &lt;div class="beautiful"&gt;I like the fireplace. It is cozy.&lt;/div&gt;
<i>14</i>          &lt;p class="boringcolor"&gt;John likes Star Wars more than My Little Pony.&lt;/p&gt;
<i>15</i>          &lt;div class="cheesy"&gt;Cheese puffs make my fingers dirty&lt;/div&gt;
<i>16</i>      &lt;/body&gt;
<i>17</i>  &lt;/html&gt;</pre></div>11:54</div></div><div><div><div><div><b>tutorial</b><b>index.js</b><b>index.html</b></div><pre><i> 1</i>  function baz(param1, param2) {
<i> 2</i>    return 2 + param2(2);
<i> 3</i>  }
<i> 4</i>  
<i> 5</i>  function times2(param1) {
<i> 6</i>    return param1 * 2;
<i> 7</i>  }
<i> 8</i>  
<i> 9</i>  console.log(
<i>10</i>    baz(2, times2)
<i>11</i>  );</pre></div>27:17</div></div><div><div><div><div><b>tutorial</b><b>index.js</b><b>index.html</b></div><pre><i> 1</i>  x = 1
<i> 2</i>  
<i> 3</i>  console.log(x)</pre></div>10:26</div></div><div><div><div><div><b>tutorial</b><b>part1.js</b><b>index.html</b><b>input.js</b><b>part1.md</b><b>part2.js</b><b>part2.md</b></div><pre><i> 1</i>  import input from './input';
<i> 2</i>  
<i> 3</i>  var digits = input.match(/\d/g).map(c =&gt; parseInt(c, 10));
<i> 4</i>  
<i> 5</i>  var sum = 0;
<i> 6</i>  digits.forEach((digit, idx) =&gt; {
<i> 7</i>      var nextDigit = digits[idx + 1];
<i> 8</i>      if (digit == nextDigit) {
<i> 9</i>          sum += digit;
<i>10</i>      }
<i>11</i>  });
<i>12</i>  
<i>13</i>  console.log("Part 1", sum);
<i>14</i>  </pre></div>3:11</div></div><div><div><div><div><b>tutorial</b><b>part1.js</b><b>index.html</b><b>input.js</b><b>part1.md</b><b>part2.js</b><b>part2.md</b></div><pre><i> 1</i>  import input from './input';
<i> 2</i>  
<i> 3</i>  var lines = input.trim().split("\n").map(line =&gt; {
<i> 4</i>      return line.match(/\d+/g).map(c =&gt; parseInt(c, 10));
<i> 5</i>  });
<i> 6</i>  
<i> 7</i>  var sum = 0;
<i> 8</i>  
<i> 9</i>  lines.forEach(line =&gt; {
<i>10</i>      line.sort((a, b) =&gt; a - b);
<i>11</i>      
<i>12</i>      for (var i = 0; i &lt; line.length; i++) {
<i>13</i>          for (var j = i + 1; j &lt; line.length; j++) {
<i>14</i>              if (line[j] % line[i] == 0) {
<i>15</i>                  sum += line[j] / line[i];
<i>16</i>                  break;
<i>17</i>              }
<i>18</i>          }</pre></div>4:51</div></div><div><div><div><div><b>tutorial</b><b>part1.js</b><b>index.html</b><b>input.js</b><b>part1.md</b><b>part2.js</b><b>part2.md</b><b>index.js</b></div><pre><i> 1</i>  import input from './input';
<i> 2</i>  import regeneratorRuntime from 'regenerator-runtime';
<i> 3</i>  
<i> 4</i>  function* spiral() {
<i> 5</i>      var x = 0;
<i> 6</i>      var y = 0;
<i> 7</i>      
<i> 8</i>      yield [x, y];
<i> 9</i>      
<i>10</i>      var steps = 1;
<i>11</i>      
<i>12</i>      while (true) {
<i>13</i>          for (var i = 0; i &lt; steps; i++) {
<i>14</i>              x++;
<i>15</i>              yield [x, y];
<i>16</i>          }
<i>17</i>          
<i>18</i>          for (var i = 0; i &lt; steps; i++) {</pre></div>4:41</div></div><div><div><div><div><b>tutorial</b><b>index.html</b><b>index.css</b><b>index.js</b></div><pre><i> 1</i>  /*
<i> 2</i>  
<i> 3</i>      8 Useful Javascript Hacks to use in your code (except the last one!)
<i> 4</i>      2017 - GitHub.com/PCabralSoftware
<i> 5</i>  
<i> 6</i>  */
<i> 7</i>  
<i> 8</i>  var user = {
<i> 9</i>    name: "Peter",
<i>10</i>    cash: 2,
<i>11</i>    likesScrimba: true,
<i>12</i>    likesWatermelon: true
<i>13</i>  };
<i>14</i>  
<i>15</i>  // 1 - Conditions with the "&&" (and and) Operator
<i>16</i>  if (user.likesWatermelon) {
<i>17</i>    console.log("True!");
<i>18</i>  }</pre></div>9:49</div></div><div><div><div><div><b>tutorial</b><b>index.html</b><b>index.css</b><b>index.js</b><b>nature.jpg</b><b>nature.html</b></div><pre><i> 1</i>  &lt;html&gt;
<i> 2</i>      &lt;head&gt;
<i> 3</i>          &lt;link rel="stylesheet" href="index.css"&gt;
<i> 4</i>      &lt;/head&gt;
<i> 5</i>      &lt;body&gt;
<i> 6</i>          &lt;!-- https://medium.com/scrimba/scrimba-release-notes-november-675a65f118de --&gt;
<i> 7</i>          &lt;h1&gt;RELEASE NOTES&lt;/h1&gt;
<i> 8</i>            &lt;ul class="list"&gt;
<i> 9</i>              &lt;li&gt;FILE SYSTEM&lt;/li&gt;
<i>10</i>              &lt;li&gt;&lt;a href="nature.html"&gt;ASSET UPLOADING&lt;/a&gt;&lt;/li&gt;
<i>11</i>              &lt;li&gt;SKIP BACK AND FORTH&lt;/li&gt;
<i>12</i>              &lt;li&gt;NOTES&lt;/li&gt;
<i>13</i>              &lt;li&gt;POST PROCESSING&lt;/li&gt;
<i>14</i>              &lt;li&gt;SEARCH&lt;/li&gt;
<i>15</i>              &lt;li&gt;NEXT UP QUEUE&lt;/li&gt;
<i>16</i>          &lt;/ul&gt;
<i>17</i>      &lt;/body&gt;
<i>18</i>  &lt;/html&gt;</pre><div><div><div>jquery</div></div></div></div>3:07</div></div><div><div><div><div><b>tutorial</b><b>index.js</b><b>auth.ejs</b></div><pre><i> 1</i>  /*
<i> 2</i>  
<i> 3</i>      Authentication System using PassportJS with ExpressJS and Mongoose
<i> 4</i>      PCabralSoftware - 2017 - GitHub.com/PCabralSoftware
<i> 5</i>  
<i> 6</i>  */
<i> 7</i>  
<i> 8</i>  // ExpressJS Module
<i> 9</i>  var express = require('express'),
<i>10</i>      express_session = require('express-session'),
<i>11</i>      bodyParser = require('body-parser'),
<i>12</i>      app = express();
<i>13</i>  
<i>14</i>  var passport = require('passport'),
<i>15</i>      LocalStrategy = require('passport-local').Strategy;
<i>16</i>      
<i>17</i>  var Mongoose = require('mongoose'),
<i>18</i>      MConnection = Mongoose.createConnection("mongodb://yourip:27018");</pre></div>17:16</div></div><div><div><div><div><b>tutorial</b><b>index.html</b><b>index.css</b><b>index.js</b></div><pre><i> 1</i>  import Vue from 'vue';
<i> 2</i>  
<i> 3</i>  new Vue({ 
<i> 4</i>      el: '#app',
<i> 5</i>      data: {location : "Jomoni"}
<i> 6</i>  });
<i> 7</i>  </pre><div><div><div>vue-devtools</div></div></div></div>3:24</div></div><div><div><div><div><b>tutorial</b><b>index.html</b><b>index.css</b><b>examples.html</b><b>examples.css</b><b>basic.css</b></div><pre><i> 1</i>  &lt;html&gt;
<i> 2</i>      &lt;head&gt;
<i> 3</i>          &lt;link rel="stylesheet" href="basic.css"&gt;
<i> 4</i>          &lt;link rel="stylesheet" href="examples.css"&gt;
<i> 5</i>          &lt;link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css"&gt;
<i> 6</i>          &lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"&gt;&lt;/script&gt;
<i> 7</i>          &lt;script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"&gt;&lt;/script&gt;
<i> 8</i>      &lt;/head&gt;
<i> 9</i>      &lt;body&gt;
<i>10</i>          
<i>11</i>          &lt;!-- CSS Grid --&gt;
<i>12</i>          &lt;h1 class="title"&gt;CSS GRID&lt;/h1&gt;
<i>13</i>          &lt;div class="wrapper"&gt;
<i>14</i>              &lt;div class="header"&gt;HEADER&lt;/div&gt;
<i>15</i>              &lt;div class="menu"&gt;MENU&lt;/div&gt;
<i>16</i>              &lt;div class="content"&gt;CONTENT&lt;/div&gt;
<i>17</i>              &lt;div class="footer"&gt;FOOTER&lt;/div&gt;
<i>18</i>          &lt;/div&gt;</pre></div>4:51</div></div></div></div>
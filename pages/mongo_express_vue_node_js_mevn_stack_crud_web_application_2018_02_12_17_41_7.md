<a href="https://www.djamware.com/post/5a1b779f80aca75eadc12d6e/mongo-express-vue-nodejs-mevn-stack-crud-web-application">https://www.djamware.com/post/5a1b779f80aca75eadc12d6e/mongo-express-vue-nodejs-mevn-stack-crud-web-application</a><div id="articleHeader"><h1>Mongo Express Vue Node.js (MEVN Stack) CRUD Web Application</h1></div>
by Didin J. on 十一月 27, 2017
<div class="readableLargeImageContainer"><img src="https://s3-ap-southeast-1.amazonaws.com/djamblog/article-271117092533.png" alt="Mongo Express Vue Node.js (MEVN Stack) CRUD Web Application" /></div>
<blockquote><h2>Step by step tutorial of building Mongo, Express.js, Vue.js 2 and Node.js (MEVN Stack) create-read-update-delete (CRUD) web application.</h2></blockquote>
<div><p>A comprehensive step by step tutorial of building Mongo, Express, Vue.js 2 and Node.js (MEVN Stack) create-read-update-delete (CRUD) web application. Vue.js <a href="https://vuejs.org" target="_blank">https://vuejs.org</a> recently become a top Javascript framework along with Angular and React.js. So, we interesting to make a little experiment to integrate or create a full stack web application based on Node.js, Express, and MongoDB. Previously, we have done with <a href="https://www.djamware.com/post/5a0673c880aca7739224ee21/mean-stack-angular-5-crud-web-application-example" target="_blank">MEAN Stack (Angular 5)</a> and <a href="https://www.djamware.com/post/59faec0a80aca7739224ee1f/building-crud-web-application-using-mern-stack" target="_blank">MERN Stack (React.js)</a>.</p>
<p>Now, we have to make similar concept to make Vue.js works with Express.js. As usual, we use Express.js as backend and RESTful API server and Vue.js as Frontend. The following tools, frameworks, and modules are required for this tutorial:</p>
<p>- <a href="https://nodejs.org" target="_blank">Node.js</a> (use recommended version)<br />
- <a href="https://expressjs.com/" target="_blank">Express.js</a><br />
- <a href="https://www.mongodb.com/" target="_blank">MongoDB</a><br />
- <a href="https://mongoosejs.com/" target="_blank">Mongoose.js</a><br />
- <a href="https://vuejs.org" target="_blank">Vue.js</a><br />
- <a href="https://github.com/vuejs/vue-cli" target="_blank">Vue-CLI</a><br />
- IDE or Text Editor (we use Atom)</p>
<p>We assume that you have already installed Node.js and able to run Node.js command line (Windows) or `npm` on the terminal (MAC/Linux). Open the terminal or Node command line then type this command to install `vue-cli`.</p>
<pre><code>sudo npm install -g vue-cli</code></pre>
<p>That where we start the tutorial. We will create the MEVN stack CRUD web application from `vue-cli`.</p>
<h3><br />
<strong>1. Create a New Vue.js Application</strong></h3>
<p>To create a new Vue.js application using `vue-cli` simply type this command from terminal or Node command line.</p>
<pre><code>vue init webpack mevn-stack</code></pre>
<p>Next, go to the newly created Vue.js project folder then install all default required modules by type this command.</p>
<pre><code>cd ./mevn-stack
npm install</code></pre>
<p>Now, check the Vue.js application by running the application using this command.</p>
<pre><code>npm run dev</code></pre>
<p>You should see this page when everything still on the track.</p>
<p><div class="readableLargeImageContainer"><img src="https://s3-ap-southeast-1.amazonaws.com/djamblog/article-251117211558.png" alt="Mongo Express Vue Node.js (MEVN Stack) CRUD Web Application - Vue.js 2 home" /></div></p>
<h3><br />
<strong>2. Install Express.js as RESTful API Server</strong></h3>
<p>Close the running Vue.js app first by press `ctrl+c` then type this command for adding Express.js modules and it dependencies.</p>
<pre><code>npm install --save express body-parser morgan body-parser serve-favicon</code></pre>
<p>Next, create a new folder called `bin` then add a file called `www` on the root of Vue.js project folder.</p>
<pre><code>mkdir bin
touch bin/www</code></pre>
<p>Open and edit www file then add this lines of codes.</p>
<pre><code>#!/usr/bin/env node

/**
 * Module dependencies.
 */

var app = require('../app');
var debug = require('debug')('mean-app:server');
var http = require('http');

/**
 * Get port from environment and store in Express.
 */

var port = normalizePort(process.env.PORT || '3000');
app.set('port', port);

/**
 * Create HTTP server.
 */

var server = http.createServer(app);

/**
 * Listen on provided port, on all network interfaces.
 */

server.listen(port);
server.on('error', onError);
server.on('listening', onListening);

/**
 * Normalize a port into a number, string, or false.
 */

function normalizePort(val) {
  var port = parseInt(val, 10);

  if (isNaN(port)) {
    // named pipe
    return val;
  }

  if (port &gt;= 0) {
    // port number
    return port;
  }

  return false;
}

/**
 * Event listener for HTTP server "error" event.
 */

function onError(error) {
  if (error.syscall !== 'listen') {
    throw error;
  }

  var bind = typeof port === 'string'
    ? 'Pipe ' + port
    : 'Port ' + port;

  // handle specific listen errors with friendly messages
  switch (error.code) {
    case 'EACCES':
      console.error(bind + ' requires elevated privileges');
      process.exit(1);
      break;
    case 'EADDRINUSE':
      console.error(bind + ' is already in use');
      process.exit(1);
      break;
    default:
      throw error;
  }
}

/**
 * Event listener for HTTP server "listening" event.
 */

function onListening() {
  var addr = server.address();
  var bind = typeof addr === 'string'
    ? 'pipe ' + addr
    : 'port ' + addr.port;
  debug('Listening on ' + bind);
}</code></pre>
<p>Next, change the default server what run by `npm` command. Open and edit `package.json` then replace `start` value inside `scripts`.</p>
<pre><code>"scripts": {
  "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
  "start": "npm run build && node ./bin/www",
  "unit": "cross-env BABEL_ENV=test karma start test/unit/karma.conf.js --single-run",
  "e2e": "node test/e2e/runner.js",
  "test": "npm run unit && npm run e2e",
  "lint": "eslint --ext .js,.vue src test/unit/specs test/e2e/specs",
  "build": "node build/build.js"
},</code></pre>
<p>Now, create `app.js` in the root of project folder.</p>
<pre><code>touch app.js</code></pre>
<p>Open and edit `app.js` then add this lines of codes.</p>
<pre><code>var express = require('express');
var path = require('path');
var favicon = require('serve-favicon');
var logger = require('morgan');
var bodyParser = require('body-parser');

var book = require('./routes/book');
var app = express();

app.use(logger('dev'));
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({'extended':'false'}));
app.use(express.static(path.join(__dirname, 'dist')));
app.use('/books', express.static(path.join(__dirname, 'dist')));
app.use('/book', book);

// catch 404 and forward to error handler
app.use(function(req, res, next) {
  var err = new Error('Not Found');
  err.status = 404;
  next(err);
});

// error handler
app.use(function(err, req, res, next) {
  // set locals, only providing error in development
  res.locals.message = err.message;
  res.locals.error = req.app.get('env') === 'development' ? err : {};

  // render the error page
  res.status(err.status || 500);
  res.render('error');
});

module.exports = app;</code></pre>
<p>Next, create routes folder then create routes file for the book.</p>
<pre><code>mkdir routes
touch routes/book.js</code></pre>
<p>Open and edit `routes/book.js` file then add this lines of codes.</p>
<pre><code>var express = require('express');
var router = express.Router();

/* GET home page. */
router.get('/', function(req, res, next) {
  res.send('Express RESTful API');
});

module.exports = router;</code></pre>
<p>Now, run the server using this command.</p>
<pre><code>npm start</code></pre>
<p>You will see the previous Vue.js landing page when you point your browser to `<a href="http://localhost:3000" target="_blank">http://localhost:3000</a>`. When you change the address to `<a href="http://localhost:3000/book" target="_blank">http://localhost:3000/book</a>` you will see this page.</p>
<p><div class="readableLargeImageContainer"><img src="https://s3-ap-southeast-1.amazonaws.com/djamblog/article-111117063509.png" alt="Mongo Express Vue Node.js (MEVN Stack) CRUD Web Application - Express Restful API" /></div></p>
<p>If you find this error.</p>
<pre><code>Error: No default engine was specified and no extension was provided.</code></pre>
<p>Then add to `app.js` this line after `app.use`.</p>
<pre><code>app.set('view engine', 'html');</code></pre>
<p>And this is the new folders and files structure of Express.js and Vue.js web application.</p>
<pre><code>|-- README.md
|-- app.js
|-- bin
|   `-- www
|-- build
|-- config
|-- dist
|   |-- index.html
|   `-- static
|       |-- css
|       `-- js
|-- index.html
|-- node_modules
|-- package.json
|-- routes
|-- src
|-- static
`-- test
    |-- e2e
    `-- unit</code></pre>
<h3><br />
<strong>3. Install and Configure Mongoose.js</strong></h3>
<p>We need to access data from MongoDB. For that we will install and configure Mongoose.js. On the terminal type this command after stopping the running Express server.</p>
<pre><code>npm install --save mongoose bluebird</code></pre>
<p>Open and edit `app.js` then add this lines after another variable line.</p>
<pre><code>var mongoose = require('mongoose');
mongoose.Promise = require('bluebird');
mongoose.connect('mongodb://localhost/mean-angular5', { useMongoClient: true, promiseLibrary: require('bluebird') })
  .then(() =&gt;  console.log('connection succesful'))
  .catch((err) =&gt; console.error(err));</code></pre>
<p>Now, run MongoDB server on different terminal tab or command line or run from the service.</p>
<pre><code>mongod</code></pre>
<p>Next, you can test the connection to MongoDB run again the Node application and you will see this message on the terminal.</p>
<pre><code>connection succesful</code></pre>
<p>If you are still using built-in Mongoose Promise library, you will get this deprecated warning on the terminal.</p>
<pre><code>(node:42758) DeprecationWarning: Mongoose: mpromise (mongoose's default promise library) is deprecated, plug in your own promise library instead: <a href="http://mongoosejs.com/docs/promises.html" target="_blank">http://mongoosejs.com/docs/promises.html</a></code></pre>
<p>That's the reason why we added `bluebird` modules and register it as Mongoose Promise library.</p>
<h3><br />
<strong>4. Create Mongoose.js Model</strong></h3>
<p>Add a models folder on the root of project folder for hold Mongoose.js model files.</p>
<pre><code>mkdir models</code></pre>
<p>Create new Javascript file that uses for Mongoose.js model. We will create a model of Book collection.</p>
<pre><code>touch models/Book.js</code></pre>
<p>Now, open and edit that file and add Mongoose require.</p>
<pre><code>var mongoose = require('mongoose');</code></pre>
<p>Then add model fields like this.</p>
<pre><code>var BookSchema = new mongoose.Schema({
  isbn: String,
  title: String,
  author: String,
  description: String,
  published_year: String,
  publisher: String,
  updated_date: { type: Date, default: Date.now },
});</code></pre>
<p>That Schema will mapping to MongoDB collections called book. If you want to know more about Mongoose Schema Datatypes you can find it here <a href="http://mongoosejs.com/docs/schematypes.html" target="_blank">http://mongoosejs.com/docs/schematypes.html</a>. Next, export that schema.</p>
<pre><code>module.exports = mongoose.model('Book', BookSchema);</code></pre>
<h3><br />
<strong>5. Create Routes for Accessing Book Data via Restful API</strong></h3>
<p>Open and edit again "routes/book.js” then replace all codes with this.</p>
<pre><code>var express = require('express');
var router = express.Router();
var mongoose = require('mongoose');
var Book = require('../models/Book.js');

/* GET ALL BOOKS */
router.get('/', function(req, res, next) {
  Book.find(function (err, products) {
    if (err) return next(err);
    res.json(products);
  });
});

/* GET SINGLE BOOK BY ID */
router.get('/:id', function(req, res, next) {
  Book.findById(req.params.id, function (err, post) {
    if (err) return next(err);
    res.json(post);
  });
});

/* SAVE BOOK */
router.post('/', function(req, res, next) {
  Book.create(req.body, function (err, post) {
    if (err) return next(err);
    res.json(post);
  });
});

/* UPDATE BOOK */
router.put('/:id', function(req, res, next) {
  Book.findByIdAndUpdate(req.params.id, req.body, function (err, post) {
    if (err) return next(err);
    res.json(post);
  });
});

/* DELETE BOOK */
router.delete('/:id', function(req, res, next) {
  Book.findByIdAndRemove(req.params.id, req.body, function (err, post) {
    if (err) return next(err);
    res.json(post);
  });
});

module.exports = router;</code></pre>
<p>Run again the Express server then open the other terminal or command line to test the Restful API by type this command.</p>
<pre><code>curl -i -H "Accept: application/json" localhost:3000/book</code></pre>
<p>If that command return response like below then REST API is ready to go.</p>
<pre><code>HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 2
ETag: W/"2-l9Fw4VUO7kr8CvBlt4zaMCqXZ0w"
Date: Fri, 10 Nov 2017 23:53:52 GMT
Connection: keep-alive</code></pre>
<p>Now, let's populate Book collection with initial data that sent from RESTful API. Run this command to populate it.</p>
<pre><code>curl -i -X POST -H "Content-Type: application/json" -d '{ "isbn":"211333122, 98872233321123","title":"How to Build MEVN Stack","author": "Didin J.","description":"The comprehensive step by step tutorial on how to build MEVN (MongoDB, Express.js, Vue.js and Node.js) stack web application from scratch","published_year":"2017","publisher":"Djamware.com" }' localhost:3000/book</code></pre>
<p>You will see this response to the terminal if success.</p>
<pre><code>HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 378
ETag: W/"17a-monzg91k25p3x996snFiZXWIP4Q"
Date: Sat, 25 Nov 2017 23:27:18 GMT
Connection: keep-alive

{"__v":0,"isbn":"211333122, 98872233321123","title":"How to Build MEVN Stack","author":"Didin J.","description":"The comprehensive step by step tutorial on how to build MEVN (MongoDB, Express.js, Vue.js and Node.js) stack web application from scratch","published_year":"2017","publisher":"Djamware.com","_id":"5a19fc555819f62adde6d44e","updated_date":"2017-11-25T23:27:17.646Z"}</code></pre>
<h3><br />
<strong>7. Create Vue.js Component and Routing</strong></h3>
<p>Now, it's time for Vue.js or front end part. First, create or add the component of the book list, show, edit and create. Create all of those files inside components folder.</p>
<pre><code>touch src/components/BookList.vue
touch src/components/CreateBook.vue
touch src/components/EditBook.vue
touch src/components/ShowBook.vue</code></pre>
<p>Now, open and edit `src/router/index.js` then add the import for all above new components.</p>
<pre><code>import Vue from 'vue'
import Router from 'vue-router'
import BookList from '@/components/BookList'
import ShowBook from '@/components/ShowBook'
import CreateBook from '@/components/CreateBook'
import EditBook from '@/components/EditBook'</code></pre>
<p>Add the router to each component or page.</p>
<pre><code>export default new Router({
  routes: [
    {
      path: '/',
      name: 'BookList',
      component: BookList
    },
    {
      path: '/show-book/:id',
      name: 'ShowBook',
      component: ShowBook
    },
    {
      path: '/add-book',
      name: 'CreateBook',
      component: CreateBook
    },
    {
      path: '/edit-book/:id',
      name: 'EditBook',
      component: EditBook
    }
  ]
})</code></pre>
<h3><br />
<strong>8. Add Module for RESTful API Access and Styling UI</strong></h3>
<p>Previously, the file for book list component is created. For UI or styling, we are using Bootstrap Vue, to install it type this command on the terminal.</p>
<pre><code>npm i bootstrap-vue bootstrap@4.0.0-beta.2</code></pre>
<p>Open and edit `src/main.js` then add the imports for Bootstrap-Vue.</p>
<pre><code>import Vue from 'vue'
import BootstrapVue from 'bootstrap-vue'
import App from './App'
import router from './router'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'</code></pre>
<p>Add this line after `Vue.config`.</p>
<pre><code>Vue.use(BootstrapVue)</code></pre>
<p>Next, we are using Axio for accessing RESTful API that provided by Express.js. To install it, in the terminal type this command.</p>
<pre><code>npm install axios --save</code></pre>
<h3><br />
<strong>9. Modify Component of Book List</strong></h3>
<p>Now, open and edit `src/components/BookList.vue` then add this lines of codes.</p>
<pre><code>&lt;template&gt;
  &lt;b-row&gt;
    &lt;b-col cols="12"&gt;
      &lt;h2&gt;
        Book List
        &lt;b-link href="#/add-book"&gt;(Add Book)&lt;/b-link&gt;
      &lt;/h2&gt;
      &lt;b-table striped hover :items="books" :fields="fields"&gt;
        &lt;template slot="actions" scope="row"&gt;
          &lt;b-btn size="sm" @click.stop="details(row.item)"&gt;Details&lt;/b-btn&gt;
        &lt;/template&gt;
      &lt;/b-table&gt;
      &lt;ul v-if="errors && errors.length"&gt;
        &lt;li v-for="error of errors"&gt;
          {{error.message}}
        &lt;/li&gt;
      &lt;/ul&gt;
    &lt;/b-col&gt;
  &lt;/b-row&gt;
&lt;/template&gt;

&lt;script&gt;

import axios from 'axios'

export default {
  name: 'BookList',
  data () {
    return {
      fields: {
        isbn: { label: 'ISBN', sortable: true, 'class': 'text-center' },
        title: { label: 'Book Title', sortable: true },
        actions: { label: 'Action', 'class': 'text-center' }
      },
      books: [],
      errors: []
    }
  },
  created () {
    axios.get(`<a href="http://localhost:3000/book" target="_blank">http://localhost:3000/book</a>`)
    .then(response =&gt; {
      this.books = response.data
    })
    .catch(e =&gt; {
      this.errors.push(e)
    })
  },
  methods: {
    details (book) {
      this.$router.push({
        name: 'ShowBook',
        params: { id: book._id }
      })
    }
  }
}
&lt;/script&gt;</code></pre>
<p>There are template and script in one file. The template block contains HTML tags. Script block contains variables, page lifecycle and methods or functions.</p>
<h3><br />
<strong>10. Modify Component of Create Book</strong></h3>
<p>Now, open and edit `src/components/CreateBook.vue` then add this lines of codes.</p>
<pre><code>&lt;template&gt;
  &lt;b-row&gt;
    &lt;b-col cols="12"&gt;
      &lt;h2&gt;
        Add Book
        &lt;b-link href="#/"&gt;(Book List)&lt;/b-link&gt;
      &lt;/h2&gt;
      &lt;b-form @submit="onSubmit"&gt;
        &lt;b-form-group id="fieldsetHorizontal"
                  horizontal
                  :label-cols="4"
                  breakpoint="md"
                  label="Enter ISBN"&gt;
          &lt;b-form-input id="isbn" :state="state" v-model.trim="book.isbn"&gt;&lt;/b-form-input&gt;
        &lt;/b-form-group&gt;
        &lt;b-form-group id="fieldsetHorizontal"
                  horizontal
                  :label-cols="4"
                  breakpoint="md"
                  label="Enter Title"&gt;
          &lt;b-form-input id="title" :state="state" v-model.trim="book.title"&gt;&lt;/b-form-input&gt;
        &lt;/b-form-group&gt;
        &lt;b-form-group id="fieldsetHorizontal"
                  horizontal
                  :label-cols="4"
                  breakpoint="md"
                  label="Enter Author"&gt;
          &lt;b-form-input id="author" :state="state" v-model.trim="book.author"&gt;&lt;/b-form-input&gt;
        &lt;/b-form-group&gt;
        &lt;b-form-group id="fieldsetHorizontal"
                  horizontal
                  :label-cols="4"
                  breakpoint="md"
                  label="Enter Description"&gt;
            &lt;b-form-textarea id="description"
                       v-model="book.description"
                       placeholder="Enter something"
                       :rows="2"
                       :max-rows="6"&gt;{{book.description}}&lt;/b-form-textarea&gt;
        &lt;/b-form-group&gt;
        &lt;b-form-group id="fieldsetHorizontal"
                  horizontal
                  :label-cols="4"
                  breakpoint="md"
                  label="Enter Publisher Year"&gt;
          &lt;b-form-input id="published_year" :state="state" v-model.trim="book.published_year"&gt;&lt;/b-form-input&gt;
        &lt;/b-form-group&gt;
        &lt;b-form-group id="fieldsetHorizontal"
                  horizontal
                  :label-cols="4"
                  breakpoint="md"
                  label="Enter Publisher"&gt;
          &lt;b-form-input id="publisher" :state="state" v-model.trim="book.publisher"&gt;&lt;/b-form-input&gt;
        &lt;/b-form-group&gt;
        &lt;b-button type="submit" variant="primary"&gt;Save&lt;/b-button&gt;
      &lt;/b-form&gt;
    &lt;/b-col&gt;
  &lt;/b-row&gt;
&lt;/template&gt;

&lt;script&gt;

import axios from 'axios'

export default {
  name: 'CreateBook',
  data () {
    return {
      book: {}
    }
  },
  methods: {
    onSubmit (evt) {
      evt.preventDefault()
      axios.post(`<a href="http://localhost:3000/book" target="_blank">http://localhost:3000/book</a>`, this.book)
      .then(response =&gt; {
        this.$router.push({
          name: 'ShowBook',
          params: { id: response.data._id }
        })
      })
      .catch(e =&gt; {
        this.errors.push(e)
      })
    }
  }
}
&lt;/script&gt;</code></pre>
<p>That code contains the template for book form, the script that contains Vue.js 2 codes for hold book model and methods for saving book to RESTful API.</p>
<h3><br />
<strong>11. Modify Component of Show Book</strong></h3>
<p>Open and edit `src/components/ShowBook.vue` then add this lines of codes.</p>
<pre><code>&lt;template&gt;
  &lt;b-row&gt;
    &lt;b-col cols="12"&gt;
      &lt;h2&gt;
        Edit Book
        &lt;b-link href="#/"&gt;(Book List)&lt;/b-link&gt;
      &lt;/h2&gt;
      &lt;b-jumbotron&gt;
        &lt;template slot="header"&gt;
          {{book.title}}
        &lt;/template&gt;
        &lt;template slot="lead"&gt;
          ISBN: {{book.isbn}}&lt;br&gt;
          Author: {{book.author}}&lt;br&gt;
          Description: {{book.description}}&lt;br&gt;
          Published Year: {{book.published_year}}&lt;br&gt;
          Publisher: {{book.publisher}}&lt;br&gt;
        &lt;/template&gt;
        &lt;hr class="my-4"&gt;
        &lt;p&gt;
          Updated Date: {{book.updated_date}}
        &lt;/p&gt;
        &lt;b-btn variant="success" @click.stop="editbook(book._id)"&gt;Edit&lt;/b-btn&gt;
        &lt;b-btn variant="danger" @click.stop="deletebook(book._id)"&gt;Delete&lt;/b-btn&gt;
      &lt;/b-jumbotron&gt;
    &lt;/b-col&gt;
  &lt;/b-row&gt;
&lt;/template&gt;

&lt;script&gt;

import axios from 'axios'

export default {
  name: 'ShowBook',
  data () {
    return {
      book: []
    }
  },
  created () {
    axios.get(`<a href="http://localhost:3000/book/" target="_blank">http://localhost:3000/book/</a>` + this.$route.params.id)
    .then(response =&gt; {
      this.book = response.data
    })
    .catch(e =&gt; {
      this.errors.push(e)
    })
  },
  methods: {
    editbook (bookid) {
      this.$router.push({
        name: 'EditBook',
        params: { id: bookid }
      })
    },
    deletebook (bookid) {
      axios.delete('<a href="http://localhost:3000/book/" target="_blank">http://localhost:3000/book/</a>' + bookid)
      .then((result) =&gt; {
        this.$router.push({
          name: 'BookList'
        })
      })
      .catch(e =&gt; {
        this.errors.push(e)
      })
    }
  }
}
&lt;/script&gt;

&lt;style&gt;
  .jumbotron {
    padding: 2rem;
  }
&lt;/style&gt;</code></pre>
<p>Delete function also includes in this component inside methods block.</p>
<h3><br />
<strong>12. Modify Component of Edit Book</strong></h3>
<p>For editing book that chooses from show book page, open and edit `src/components/EditBook.vue` then add this lines of codes.</p>
<pre><code>&lt;template&gt;
  &lt;b-row&gt;
    &lt;b-col cols="12"&gt;
      &lt;h2&gt;
        Edit Book
        &lt;router-link :to="{ name: 'ShowBook', params: { id: book._id } }"&gt;(Show Book)&lt;/router-link&gt;
      &lt;/h2&gt;
      &lt;b-form @submit="onSubmit"&gt;
        &lt;b-form-group id="fieldsetHorizontal"
                  horizontal
                  :label-cols="4"
                  breakpoint="md"
                  label="Enter ISBN"&gt;
          &lt;b-form-input id="isbn" :state="state" v-model.trim="book.isbn"&gt;&lt;/b-form-input&gt;
        &lt;/b-form-group&gt;
        &lt;b-form-group id="fieldsetHorizontal"
                  horizontal
                  :label-cols="4"
                  breakpoint="md"
                  label="Enter Title"&gt;
          &lt;b-form-input id="title" :state="state" v-model.trim="book.title"&gt;&lt;/b-form-input&gt;
        &lt;/b-form-group&gt;
        &lt;b-form-group id="fieldsetHorizontal"
                  horizontal
                  :label-cols="4"
                  breakpoint="md"
                  label="Enter Author"&gt;
          &lt;b-form-input id="author" :state="state" v-model.trim="book.author"&gt;&lt;/b-form-input&gt;
        &lt;/b-form-group&gt;
        &lt;b-form-group id="fieldsetHorizontal"
                  horizontal
                  :label-cols="4"
                  breakpoint="md"
                  label="Enter Description"&gt;
            &lt;b-form-textarea id="description"
                       v-model="book.description"
                       placeholder="Enter something"
                       :rows="2"
                       :max-rows="6"&gt;{{book.description}}&lt;/b-form-textarea&gt;
        &lt;/b-form-group&gt;
        &lt;b-form-group id="fieldsetHorizontal"
                  horizontal
                  :label-cols="4"
                  breakpoint="md"
                  label="Enter Publisher Year"&gt;
          &lt;b-form-input id="published_year" :state="state" v-model.trim="book.published_year"&gt;&lt;/b-form-input&gt;
        &lt;/b-form-group&gt;
        &lt;b-form-group id="fieldsetHorizontal"
                  horizontal
                  :label-cols="4"
                  breakpoint="md"
                  label="Enter Publisher"&gt;
          &lt;b-form-input id="publisher" :state="state" v-model.trim="book.publisher"&gt;&lt;/b-form-input&gt;
        &lt;/b-form-group&gt;
        &lt;b-button type="submit" variant="primary"&gt;Update&lt;/b-button&gt;
      &lt;/b-form&gt;
    &lt;/b-col&gt;
  &lt;/b-row&gt;
&lt;/template&gt;

&lt;script&gt;

import axios from 'axios'

export default {
  name: 'EditBook',
  data () {
    return {
      book: {}
    }
  },
  created () {
    axios.get(`<a href="http://localhost:3000/book/" target="_blank">http://localhost:3000/book/</a>` + this.$route.params.id)
    .then(response =&gt; {
      this.book = response.data
    })
    .catch(e =&gt; {
      this.errors.push(e)
    })
  },
  methods: {
    onSubmit (evt) {
      evt.preventDefault()
      axios.put(`<a href="http://localhost:3000/book/" target="_blank">http://localhost:3000/book/</a>` + this.$route.params.id, this.book)
      .then(response =&gt; {
        this.$router.push({
          name: 'ShowBook',
          params: { id: this.$route.params.id }
        })
      })
      .catch(e =&gt; {
        this.errors.push(e)
      })
    }
  }
}
&lt;/script&gt;</code></pre>
<p>This component almost same as creating book component, except for load book data by id and method for update data using `PUT`.</p>
<h3><br />
<strong>13. Run The MEVN Stack CRUD Web Application</strong></h3>
<p>This time to test all complete the MEVN Stack configuration. Type this command to run again this web application.</p>
<pre><code>npm start</code></pre>
<p>And here the application looks like, you can test all CRUD functionality.</p>
<p><div class="readableLargeImageContainer"><img src="https://s3-ap-southeast-1.amazonaws.com/djamblog/article-271117092326.png" alt="Mongo Express Vue Node.js (MEVN Stack) CRUD Web Application - CRUD flow" /></div></p>
<p>That's it, you can find the full source code on our <a href="https://github.com/didinj/mevn-stack-vue.js-2-example.git" target="_blank">GitHub</a>.</p>
<p>That just the basic. If you need more deep learning about MongoDB, Express.js, Vue.js, and Node.js, you can find the following books:</p>

<p>For more detailed on MEVN stack and Node.js, you can take the following course:</p>

<p>Thanks!</p>

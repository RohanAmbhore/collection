<a href="https://github.com/axios/axios#cancellation">https://github.com/axios/axios#cancellation</a><div id="articleHeader"><h1>Promise based HTTP client for the browser and node.js</h1></div><h1>axios</h1>
<p>Promise based HTTP client for the browser and node.js</p>
<h2>Features</h2>
<ul>
<li>Make <a href="https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest" target="_blank">XMLHttpRequests</a> from the browser</li>
<li>Make <a href="http://nodejs.org/api/http.html" target="_blank">http</a> requests from node.js</li>
<li>Supports the <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise" target="_blank">Promise</a> API</li>
<li>Intercept request and response</li>
<li>Transform request and response data</li>
<li>Cancel requests</li>
<li>Automatic transforms for JSON data</li>
<li>Client side support for protecting against <a href="http://en.wikipedia.org/wiki/Cross-site_request_forgery" target="_blank">XSRF</a></li>
</ul>
<h2>Browser Support</h2>
<table>

<tbody>
<tr>
<td>Latest ✔</td>
<td>Latest ✔</td>
<td>Latest ✔</td>
<td>Latest ✔</td>
<td>Latest ✔</td>
<td>8+ ✔</td>
</tr></tbody></table>
<p><a href="https://saucelabs.com/u/axios" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/626c46cfd86214001b4143cda5d0ef27a25bd69f/68747470733a2f2f73617563656c6162732e636f6d2f6f70656e5f73617563652f6275696c645f6d61747269782f6178696f732e737667" alt="Browser Matrix" /></div></a></p>
<h2>Installing</h2>
<p>Using npm:</p>
<div><pre>$ npm install axios</pre></div>
<p>Using bower:</p>
<div><pre>$ bower install axios</pre></div>
<p>Using cdn:</p>
<div><pre>&lt;script src="https://unpkg.com/axios/dist/axios.min.js"&gt;&lt;/script&gt;</pre></div>
<h2>Example</h2>
<p>Performing a <code>GET</code> request</p>
<div><pre>// Make a request for a user with a given ID
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

// Optionally the request above could also be done as
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
  
// Want to use async/await? Add the `async` keyword to your outer function/method.
async function getUser() {
  try {
    const response = await axios.get('/user?ID=12345');
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}</pre></div>
<blockquote>
<p><strong>NOTE:</strong> <code>async/await</code> is part of ECMAScript 2017 and is not supported in Internet
Explorer and older browsers, so use with caution.</p>
</blockquote>
<p>Performing a <code>POST</code> request</p>
<div><pre>axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });</pre></div>
<p>Performing multiple concurrent requests</p>
<div><pre>function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

axios.all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {
    // Both requests are now complete
  }));</pre></div>
<h2>axios API</h2>
<p>Requests can be made by passing the relevant config to <code>axios</code>.</p>
<h5>axios(config)</h5>
<div><pre>// Send a POST request
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});</pre></div>
<div><pre>// GET request for remote image
axios({
  method:'get',
  url:'http://bit.ly/2mTM3nY',
  responseType:'stream'
})
  .then(function(response) {
  response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
});</pre></div>
<h5>axios(url[, config])</h5>
<div><pre>// Send a GET request (default method)
axios('/user/12345');</pre></div>
<h3>Request method aliases</h3>
<p>For convenience aliases have been provided for all supported request methods.</p>
<h5>axios.request(config)</h5>
<h5>axios.get(url[, config])</h5>
<h5>axios.delete(url[, config])</h5>
<h5>axios.head(url[, config])</h5>
<h5>axios.options(url[, config])</h5>
<h5>axios.post(url[, data[, config]])</h5>
<h5>axios.put(url[, data[, config]])</h5>
<h5>axios.patch(url[, data[, config]])</h5>

<p>When using the alias methods <code>url</code>, <code>method</code>, and <code>data</code> properties don't need to be specified in config.</p>
<h3>Concurrency</h3>
<p>Helper functions for dealing with concurrent requests.</p>
<h5>axios.all(iterable)</h5>
<h5>axios.spread(callback)</h5>
<h3>Creating an instance</h3>
<p>You can create a new instance of axios with a custom config.</p>
<h5>axios.create([config])</h5>
<div><pre>var instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});</pre></div>
<h3>Instance methods</h3>
<p>The available instance methods are listed below. The specified config will be merged with the instance config.</p>
<h5>axios#request(config)</h5>
<h5>axios#get(url[, config])</h5>
<h5>axios#delete(url[, config])</h5>
<h5>axios#head(url[, config])</h5>
<h5>axios#options(url[, config])</h5>
<h5>axios#post(url[, data[, config]])</h5>
<h5>axios#put(url[, data[, config]])</h5>
<h5>axios#patch(url[, data[, config]])</h5>
<h2>Request Config</h2>
<p>These are the available config options for making requests. Only the <code>url</code> is required. Requests will default to <code>GET</code> if <code>method</code> is not specified.</p>
<div><pre>{
  // `url` is the server URL that will be used for the request
  url: '/user',

  // `method` is the request method to be used when making the request
  method: 'get', // default

  // `baseURL` will be prepended to `url` unless `url` is absolute.
  // It can be convenient to set `baseURL` for an instance of axios to pass relative URLs
  // to methods of that instance.
  baseURL: 'https://some-domain.com/api/',

  // `transformRequest` allows changes to the request data before it is sent to the server
  // This is only applicable for request methods 'PUT', 'POST', and 'PATCH'
  // The last function in the array must return a string or an instance of Buffer, ArrayBuffer,
  // FormData or Stream
  // You may modify the headers object.
  transformRequest: [function (data, headers) {
    // Do whatever you want to transform the data

    return data;
  }],

  // `transformResponse` allows changes to the response data to be made before
  // it is passed to then/catch
  transformResponse: [function (data) {
    // Do whatever you want to transform the data

    return data;
  }],

  // `headers` are custom headers to be sent
  headers: {'X-Requested-With': 'XMLHttpRequest'},

  // `params` are the URL parameters to be sent with the request
  // Must be a plain object or a URLSearchParams object
  params: {
    ID: 12345
  },

  // `paramsSerializer` is an optional function in charge of serializing `params`
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function(params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },

  // `data` is the data to be sent as the request body
  // Only applicable for request methods 'PUT', 'POST', and 'PATCH'
  // When no `transformRequest` is set, must be of one of the following types:
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - Browser only: FormData, File, Blob
  // - Node only: Stream, Buffer
  data: {
    firstName: 'Fred'
  },

  // `timeout` specifies the number of milliseconds before the request times out.
  // If the request takes longer than `timeout`, the request will be aborted.
  timeout: 1000,

  // `withCredentials` indicates whether or not cross-site Access-Control requests
  // should be made using credentials
  withCredentials: false, // default

  // `adapter` allows custom handling of requests which makes testing easier.
  // Return a promise and supply a valid response (see lib/adapters/README.md).
  adapter: function (config) {
    /* ... */
  },

  // `auth` indicates that HTTP Basic auth should be used, and supplies credentials.
  // This will set an `Authorization` header, overwriting any existing
  // `Authorization` custom headers you have set using `headers`.
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },

  // `responseType` indicates the type of data that the server will respond with
  // options are 'arraybuffer', 'blob', 'document', 'json', 'text', 'stream'
  responseType: 'json', // default

  // `xsrfCookieName` is the name of the cookie to use as a value for xsrf token
  xsrfCookieName: 'XSRF-TOKEN', // default

  // `xsrfHeaderName` is the name of the http header that carries the xsrf token value
  xsrfHeaderName: 'X-XSRF-TOKEN', // default

  // `onUploadProgress` allows handling of progress events for uploads
  onUploadProgress: function (progressEvent) {
    // Do whatever you want with the native progress event
  },

  // `onDownloadProgress` allows handling of progress events for downloads
  onDownloadProgress: function (progressEvent) {
    // Do whatever you want with the native progress event
  },

  // `maxContentLength` defines the max size of the http response content allowed
  maxContentLength: 2000,

  // `validateStatus` defines whether to resolve or reject the promise for a given
  // HTTP response status code. If `validateStatus` returns `true` (or is set to `null`
  // or `undefined`), the promise will be resolved; otherwise, the promise will be
  // rejected.
  validateStatus: function (status) {
    return status &gt;= 200 && status &lt; 300; // default
  },

  // `maxRedirects` defines the maximum number of redirects to follow in node.js.
  // If set to 0, no redirects will be followed.
  maxRedirects: 5, // default

  // `socketPath` defines a UNIX Socket to be used in node.js.
  // e.g. '/var/run/docker.sock' to send requests to the docker daemon.
  // Only either `socketPath` or `proxy` can be specified.
  // If both are specified, `socketPath` is used.
  socketPath: null, // default

  // `httpAgent` and `httpsAgent` define a custom agent to be used when performing http
  // and https requests, respectively, in node.js. This allows options to be added like
  // `keepAlive` that are not enabled by default.
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // 'proxy' defines the hostname and port of the proxy server
  // Use `false` to disable proxies, ignoring environment variables.
  // `auth` indicates that HTTP Basic auth should be used to connect to the proxy, and
  // supplies credentials.
  // This will set an `Proxy-Authorization` header, overwriting any existing
  // `Proxy-Authorization` custom headers you have set using `headers`.
  proxy: {
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },

  // `cancelToken` specifies a cancel token that can be used to cancel the request
  // (see Cancellation section below for details)
  cancelToken: new CancelToken(function (cancel) {
  })
}</pre></div>
<h2>Response Schema</h2>
<p>The response for a request contains the following information.</p>
<div><pre>{
  // `data` is the response that was provided by the server
  data: {},

  // `status` is the HTTP status code from the server response
  status: 200,

  // `statusText` is the HTTP status message from the server response
  statusText: 'OK',

  // `headers` the headers that the server responded with
  // All header names are lower cased
  headers: {},

  // `config` is the config that was provided to `axios` for the request
  config: {},

  // `request` is the request that generated this response
  // It is the last ClientRequest instance in node.js (in redirects)
  // and an XMLHttpRequest instance the browser
  request: {}
}</pre></div>
<p>When using <code>then</code>, you will receive the response as follows:</p>
<div><pre>axios.get('/user/12345')
  .then(function(response) {
    console.log(response.data);
    console.log(response.status);
    console.log(response.statusText);
    console.log(response.headers);
    console.log(response.config);
  });</pre></div>
<p>When using <code>catch</code>, or passing a <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then" target="_blank">rejection callback</a> as second parameter of <code>then</code>, the response will be available through the <code>error</code> object as explained in the <a href="#handling-errors" target="_blank">Handling Errors</a> section.</p>
<h2>Config Defaults</h2>
<p>You can specify config defaults that will be applied to every request.</p>
<h3>Global axios defaults</h3>
<div><pre>axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';</pre></div>
<h3>Custom instance defaults</h3>
<div><pre>// Set config defaults when creating the instance
var instance = axios.create({
  baseURL: 'https://api.example.com'
});

// Alter defaults after instance has been created
instance.defaults.headers.common['Authorization'] = AUTH_TOKEN;</pre></div>
<h3>Config order of precedence</h3>
<p>Config will be merged with an order of precedence. The order is library defaults found in <a href="https://github.com/axios/axios/blob/master/lib/defaults.js#L28" target="_blank">lib/defaults.js</a>, then <code>defaults</code> property of the instance, and finally <code>config</code> argument for the request. The latter will take precedence over the former. Here's an example.</p>
<div><pre>// Create an instance using the config defaults provided by the library
// At this point the timeout config value is `0` as is the default for the library
var instance = axios.create();

// Override timeout default for the library
// Now all requests will wait 2.5 seconds before timing out
instance.defaults.timeout = 2500;

// Override timeout for this request as it's known to take a long time
instance.get('/longRequest', {
  timeout: 5000
});</pre></div>
<h2>Interceptors</h2>
<p>You can intercept requests or responses before they are handled by <code>then</code> or <code>catch</code>.</p>
<div><pre>// Add a request interceptor
axios.interceptors.request.use(function (config) {
    // Do something before request is sent
    return config;
  }, function (error) {
    // Do something with request error
    return Promise.reject(error);
  });

// Add a response interceptor
axios.interceptors.response.use(function (response) {
    // Do something with response data
    return response;
  }, function (error) {
    // Do something with response error
    return Promise.reject(error);
  });</pre></div>
<p>If you may need to remove an interceptor later you can.</p>
<div><pre>var myInterceptor = axios.interceptors.request.use(function () {/*...*/});
axios.interceptors.request.eject(myInterceptor);</pre></div>
<p>You can add interceptors to a custom instance of axios.</p>
<div><pre>var instance = axios.create();
instance.interceptors.request.use(function () {/*...*/});</pre></div>
<h2>Handling Errors</h2>
<div><pre>axios.get('/user/12345')
  .catch(function (error) {
    if (error.response) {
      // The request was made and the server responded with a status code
      // that falls out of the range of 2xx
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else if (error.request) {
      // The request was made but no response was received
      // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
      // http.ClientRequest in node.js
      console.log(error.request);
    } else {
      // Something happened in setting up the request that triggered an Error
      console.log('Error', error.message);
    }
    console.log(error.config);
  });</pre></div>
<p>You can define a custom HTTP status code error range using the <code>validateStatus</code> config option.</p>
<div><pre>axios.get('/user/12345', {
  validateStatus: function (status) {
    return status &lt; 500; // Reject only if the status code is greater than or equal to 500
  }
})</pre></div>
<h2>Cancellation</h2>
<p>You can cancel a request using a <em>cancel token</em>.</p>
<blockquote>
<p>The axios cancel token API is based on the withdrawn <a href="https://github.com/tc39/proposal-cancelable-promises" target="_blank">cancelable promises proposal</a>.</p>
</blockquote>
<p>You can create a cancel token using the <code>CancelToken.source</code> factory as shown below:</p>
<div><pre>var CancelToken = axios.CancelToken;
var source = CancelToken.source();

axios.get('/user/12345', {
  cancelToken: source.token
}).catch(function(thrown) {
  if (axios.isCancel(thrown)) {
    console.log('Request canceled', thrown.message);
  } else {
    // handle error
  }
});

axios.post('/user/12345', {
  name: 'new name'
}, {
  cancelToken: source.token
})

// cancel the request (the message parameter is optional)
source.cancel('Operation canceled by the user.');</pre></div>
<p>You can also create a cancel token by passing an executor function to the <code>CancelToken</code> constructor:</p>
<div><pre>var CancelToken = axios.CancelToken;
var cancel;

axios.get('/user/12345', {
  cancelToken: new CancelToken(function executor(c) {
    // An executor function receives a cancel function as a parameter
    cancel = c;
  })
});

// cancel the request
cancel();</pre></div>
<blockquote>
<p>Note: you can cancel several requests with the same cancel token.</p>
</blockquote>
<h2>Using application/x-www-form-urlencoded format</h2>
<p>By default, axios serializes JavaScript objects to <code>JSON</code>. To send data in the <code>application/x-www-form-urlencoded</code> format instead, you can use one of the following options.</p>
<h3>Browser</h3>
<p>In a browser, you can use the <a href="https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams" target="_blank"><code>URLSearchParams</code></a> API as follows:</p>
<div><pre>var params = new URLSearchParams();
params.append('param1', 'value1');
params.append('param2', 'value2');
axios.post('/foo', params);</pre></div>
<blockquote>
<p>Note that <code>URLSearchParams</code> is not supported by all browsers (see <a href="http://www.caniuse.com/#feat=urlsearchparams" target="_blank">caniuse.com</a>), but there is a <a href="https://github.com/WebReflection/url-search-params" target="_blank">polyfill</a> available (make sure to polyfill the global environment).</p>
</blockquote>
<p>Alternatively, you can encode data using the <a href="https://github.com/ljharb/qs" target="_blank"><code>qs</code></a> library:</p>
<div><pre>var qs = require('qs');
axios.post('/foo', qs.stringify({ 'bar': 123 }));</pre></div>
<h3>Node.js</h3>
<p>In node.js, you can use the <a href="https://nodejs.org/api/querystring.html" target="_blank"><code>querystring</code></a> module as follows:</p>
<div><pre>var querystring = require('querystring');
axios.post('http://something.com/', querystring.stringify({ foo: 'bar' }));</pre></div>
<p>You can also use the <a href="https://github.com/ljharb/qs" target="_blank"><code>qs</code></a> library.</p>
<h2>Semver</h2>
<p>Until axios reaches a <code>1.0</code> release, breaking changes will be released with a new minor version. For example <code>0.5.1</code>, and <code>0.5.4</code> will have the same API, but <code>0.6.0</code> will have breaking changes.</p>
<h2>Promises</h2>
<p>axios depends on a native ES6 Promise implementation to be <a href="http://caniuse.com/promises" target="_blank">supported</a>.
If your environment doesn't support ES6 Promises, you can <a href="https://github.com/jakearchibald/es6-promise" target="_blank">polyfill</a>.</p>
<h2>TypeScript</h2>
<p>axios includes <a href="http://typescriptlang.org" target="_blank">TypeScript</a> definitions.</p>
<div><pre>import axios from 'axios';
axios.get('/user?ID=12345');</pre></div>
<h2>Resources</h2>

<h2>Credits</h2>
<p>axios is heavily inspired by the <a href="https://docs.angularjs.org/api/ng/service/$http" target="_blank">$http service</a> provided in <a href="https://angularjs.org/" target="_blank">Angular</a>. Ultimately axios is an effort to provide a standalone <code>$http</code>-like service for use outside of Angular.</p>
<h2>License</h2>


<a href="https://apiko.com/blog/express-js-api-and-rest-api-organization-tips-examples-and-techniques/">https://apiko.com/blog/express-js-api-and-rest-api-organization-tips-examples-and-techniques/</a><div id="articleHeader"><h1>Express js API and REST API Organization: tips, examples and techniques</h1></div>

  
    
      
      

      
        <p>  
    <a href="http://expressjs.com/" target="_blank">Express js</a>
    is a <a href="https://nodejs.org/en/" target="_blank">Node.js</a> web application framework
    which is excellent for
    <a href="https://en.wikipedia.org/wiki/Representational_state_transfer" target="_blank">
        Rest API
    </a>
    development and is based on JavaScript. I won’t write the generic info
    on express in this article which you might find by simply hitting Express js API in the search tab. Instead, I would like to do the next 2 big things:
</p><ul>  
<li> Share our company’s  
    experience and personal best practices of proper Express js API organization when
    developing Express app.</li>
<li> Provide a clear strategy on how to set up Express js API correctly.</li>  
</ul>  
<p>  
    In this Express js API guide, I will try to unveil the answers to the following
    questions:
</p>

<ul>  
  <li>How to set up REST API and organize REST API structure? (with the example of using REST API) 
</li>  
<li>How to process the related errors and exceptions?</li>
<li>How to organize Express js API (+example of using Express js API) and manage REST requests organization?</li>
</ul>

<h3>  
    REST API structure. How to set up REST API correctly?
</h3>

<p>  
   REST API development is the ‘description of routes’ by which
    client-devices or other services refer to your server. That’s why it's important to organize you REST API properly and make these ‘routes’ intuitive.
    Consider it as a map. Large REST API server performs lots of operations.
    The most common mistake among REST API developers is that they create a
    separate route for each operation and don’t record it properly. The result
    is an uncontrolled increase of routes which eventually causes timing and
    knowledge obstacles on the way to understand your API.
</p>

<p>  
    To avoid this issue and minimize your API routes number, try keeping up to
    the REST logic pattern, which has <em><b>4 requests types:</b></em> GET, POST, UPDATE, DELETE.
</p>  

<p>  
    What I want to say in this REST API tutorial, is to include these requests into each operation.
    For example, if you need to update any entity, use UPDATE requests if
    delete - DELETE requests. Another tip is to correlate each route to the
    business logic model.  
</p>  

<p>  
    Take a look at the table below with 5 routes to process single business
    logic model. Consider it as the example of using REST API. 
</p>  

<table>  
<tbody><tr>  
<th>Route</th>  
<th>HTTP Verb</th>  
<th>Description</th>  
</tr>  
<tr>  
<td><code>/api/v1/models/</code></td>  
<td>GET</td>  
<td>Get list of models</td>  
</tr>  
<tr>  
<td><code>/api/v1/models/:modelId</code></td>  
<td>GET</td>  
<td>Get model item</td>  
</tr>  
<tr>  
<td><code>/api/v1/models/</code></td>  
<td>POST</td>  
<td>Crete model Item</td>  
</tr>  
<tr>  
<td><code>/api/v1/models/:modelId</code></td>  
<td>PUT</td>  
<td>Update model Item</td>  
</tr>  
<tr>  
<td><code>/api/v1/models/:modelId</code></td>  
<td>DELETE</td>  
<td>Remove model item</td>  
</tr>  
</tbody></table>

<p>  
    The table shows us the routes variations and corresponding methods
    aimed to provide CRUD (create, read, update, delete) requests to process a
    certain model. If you keep to this strategy for each model processing and
    don’t create additional routes, as described in this REST API guide, your API will instantly get understandable
    and clear.
</p>  

<h3>  
    Parameters
</h3>  

<p>  
    What about additional parameters? We want
    to return sorted and filtered models list. There’s no need to create an
    additional route, like <code>/api/v1/models/sorted/:param</code>.
</p>  

<p>  
    Using of query parameters should be enough, and after their implementation, the
    route will look like: <code>/API/v1/models?sort=name</code>.
</p>  

<p>  
    There may be a lot more of such parameters. They're not necessary but using query parameters will help you perform several
    operations on a single route.
</p>  

<p>  
    Although, such technique might seem tedious if you implement it for the client-side development, it's not. Below you’ll find some practical
    examples.
</p>  

<h3>  
    Code organization tips
</h3>  

<p>  
In this Express js API guide, I want to share the most helpful coding tips when I'm on my way to set up Express js API.  
</p>  

<ul>  
    <li>Start each route as <code>/api/v1/</code>. Don’t exclude the future possibility of
    rewriting the current API by preserving the functionality of the old one
    for some time.</li>
<li>Separate models from controllers. Models are business logic objects, and they
    should be stored in the models folder. Controllers contain routes business
    logic and should refer to controllers folder.</li>
<li>Don’t place routes of the same model in one file. It's better to create a  
    separate <code>modelName</code> folder for each entity and create a separate file for each GET,
    POST, DELETE operation. For instance, file
    <code>controllers/notifications/index.js</code> can look like this:</li>
</ul>  
<pre>const fetchNotifications = require('./fetch-notifications');
const updateNotification = require('./update-notification');
const removeNotification = require('./remove-notification');
/**
* Provide Api for Investors (user with articles)
**/

module.exports = ({ config, db }) =&gt; {
 api.get('/', authenticate, fetchNotifications({ config, db }));
 api.put('/:notificationId',authenticate, updateNotification({ config, db
    }));
 api.delete('/:notificationId', authenticate, removeNotification({ config,
    db }));
    return api;
    };</pre>

<ul>  
<li>Keep your controllers documented.</li>  
<li>Refactor/extract duplicated pieces of code  
    into utils/helpers folders.</li>
</ul>  
<h3>  
    REST API documentation
</h3>  

<p>  
    Take care of proper documentation records as it’s a vital part of the REST
    API development process and Express js API organization. Since such API might be requested by other
    developers (front-end, mobile developers) or 3rd party services, clear
    guidelines on how to interact with your API is a must have. To clarify
    everything on the spot, I would recommend doing the following:
</p>  

<ul>  
<li>Before creating any documentation, determine what is the purpose of this  
    API and who will use it. For the projects with internal
    API, you can record the routes both in README files of the repository and
    in the controllers/model/index.js files. Find the documentation example
    below:</li></ul>
<pre><code>/**
 Provide Api for Model

  Model list  GET /api/v1/models
  @header
         Authorization: Bearer {token}
  @optionalQueryParameters
         param1 {String} - description
         param2 {String} - description

  Model create  POST /api/v1/models
  @header
         Authorization: Bearer {token}
  @params
         param1 {string}
         param2 {boolean}
**/
</code></pre>
<p>  
    If it’s an API meant for external use, you should think of creating a
    complete, sorted and convenient in use reference/documentation. Here, take a
    look how
    <a href="https://developers.google.com/google-apps/calendar/v3/reference/" target="_blank">
        Google Calendar API
    </a>
    is managed. Another great example of using REST API. 
</p>  

<ul>
<li>Keep documentation reference for each of your routes. There’s no reason in route existence if  
    nobody knows about it. If your API users don’t have enough information,
    they can decide that you simply don’t support such functionality. That’s
    why again, I put a high emphasis on keeping each route documented since it's aimed at making your REST API organization better</li>
<li>Record the route at the moment of route creation. Don’t ‘I’ll do it
    tomorrow’ since you can simply forget about it or its parameters.</li></ul>
<h3>  
    REST API Error handling techniques
</h3>  

<p>  
    REST server has a large list of default
    <a href="http://www.restpatterns.org/HTTP_Status_Codes" target="_blank">
        HTTP Status Codes
    </a>
    (default errors included), so you don’t have to figure out your own error
    types. The advice is, it's better to write your own events processor and use it
    everywhere than do it for each router. For this, here comes the helping
    hand of
    <a href="https://www.npmjs.com/package/rest-api-errors" target="_blank">
        rest-API-errors
    </a>
    package. But before implementing the package, you should write a
    general processor:
</p>  

<pre><code>const { APIError, InternalServerError, Unauthorized } = require('rest-api-errors');
const { STATUS_CODES } = require('http');
const winston = require('winston');
module.exports = (err, req, res, next) =&gt; {
  let error = err instanceof APIError ? err : new InternalServerError();

  if(process.env.NODE_ENV !== 'production') {
    winston.log('error', '-----&gt; Unknown server error...');
    winston.log('error', err);
  }
  res
    .status(error.status || 500)
    .json({
      code: error.code || 500,
      message: error.message || STATUS_CODES[error.status],
    });
};
</code></pre>
<p>  
    And use it in Express
</p>  

<pre><code>const errorHandler = require('./utils/error-handler');
const app = express();
app.use(errorHandler);
</code></pre>
<p>  
    Now you can initiate error in any controller type
</p>  

<pre><code>const { MethodNotAllowed } = require('rest-api-errors');

api.use('/account', (req, res, next) =&gt; {
....
if(!user) {
  throw new Unauthorized(401, 'Unauthorized');
 }
});

</code></pre>
<h3>  
    Permission checker
</h3>  

<p>  
In this part of our REST API guide I'll touch upon permission levels with providing an example of using Express js API.  
    There’s often a need to provide separate permission levels for different
    user groups. Managers, for instance, could have more rights than regular users.
    The following snippet represents how to write compact permission
    checker which looks like this:
</p>  

<pre><code> import { hasPermissionTo, actions } from '../'
 api.use('/account', (req, res, next) =&gt; {
     const user = getUser();
     if (!hasPermissionTo(actions.GET_USER, user)) {
        throw new MethodNotAllowed();
     }
});
</code></pre>
<blockquote><p>  
Where to get a user object? It depends on the    <a href="http://passportjs.org/docs" target="_blank">authentication type</a> you’ve used.</p></blockquote>  

<p>  
    Let’s first describe all the actions available (we can extend these in
    the future) <code>utils/permission-checker/index.js</code>
</p>  

<pre><code>module.exports = {
  ALL_RIGHT: 'ALL_RIGHT',
  GET_USER: 'GET_USER',
};
</code></pre>
<p>  
    Let’s apply these actions to a certain user group
<code>utils/permission-checker/index.js</code></p>  
<pre><code>const actions = require('./constants');
module.exports = {
  owner: [
    actions.GET_USER,
  ],
  user: [],
  admin: [
    actions.ALL_RIGHT,
  ],
};
</code></pre>
<p>  
    Then we create <code>hasPermissionTo</code> method <code>utils/permission-checker/index.js</code>
</p>  

<pre><code>const _ = require('lodash');
const permissions = require('./permissions');
const actions = require('./constants');

const hasPermissionTo = (action, user) =&gt; {
  const isRoleHasPermission = action =&gt; role =&gt; _.includes(permissions[role], action);
  // get map user rolse into true false array
  const userPermissions = user.roles.map(isRoleHasPermission(action));

  if (!(userPermissions && _.includes(userPermissions, true))) {
    return false
  }

  return true;
};

module.exports = {
  hasPermissionTo,
  actions,
};
</code></pre>
<blockquote><p>  
    In the current example, the user has roles field ['owner', 'user'] , which
    points to what role he/she has. When user gets owner role which has
    GET_USER permission, then hasPermissionTo returns true value. You can also
    create your own logic of hasPermissionTo method.
</p></blockquote>  

<h3>  
    Client requests
</h3>  

<p>  
    You can organize client requests by different means and with the help of
    different libraries. Here’s my personal insight on how to organize the process
    properly.
</p>  

<ul>
<li>Use the libraries already developed for it, like <a href="https://www.npmjs.com/package/axios" target="_blank">axios</a></li>  
<li>Keep routes and codes at a distance. Don’t even think (seriously) of  
    hardcoding endpoint path directly in code that performs request:</li></ul>
<pre><code>axios.get('api/v1/users', {
    params: {}
  })
</code></pre>
<p>  
    Why do I insist on this? When you change something in the API, it will cause
    troubles looking for the routes in code. According to our own experience,
    it’s better to write storages for each route and keep them in one place,
    like this:
</p>  

<pre><code>export default {
  USERS: '/api/v1/amazonS3/',
};
</code></pre>
<p>  
    Now you can use this constant for 4 requests simultaneously.
</p>  

<pre><code>import ApiAdressses = from './utils/api/urls.js';
axios.get(ApiAdressses.USERS);
axios.post(ApiAdressses.USERS);
axios.put(ApiAdressses.USERS);
axios.delete(ApiAdressses.USERS);
</code></pre>

<ul>  
<li>Write an additional functionality for API interaction  
</li></ul>  
<p>  
    Usually, most of the requests contain authorization headers apart from data
    or query parameters. Thus writing it all in your code every time is not the
    best idea.
</p>  

<pre><code>axios({
      url: `ApiAdressses.USERS?limit=${limit};soty${sort}`,
      method: 'GET',
      headers: {
        'Authorization': 'Bearer token'
     }
    });

//    or

axios({
      url: `ApiAdressses.USERS`,
      method: 'POST',
      headers: {
        'Authorization': 'Bearer token'
        'Content-Type' : 'multipart/form-data'
     }
    });
</code></pre>
<p>  
    The better strategy to apply is to write the 4 methods which will look like
    the following example:
</p>  

<pre><code>import { get, post, put, remove, query, APIAddresses } from './utils/api';

const response = await get(`APIAddresses.USERS${query({ limit, sort })}`);
const response = await post(`APIAddresses.USERS`, formData);
const response = await put(`APIAddresses.USERS/${userId}`, formData);
const response = await remove(`APIAddresses.USERS/${userId}`);
</code></pre>
<p>  
    Methods get, post, put, remove of <code>makeRequest</code> method wrapper are created to
    provide the comfort of use. Query method creates query string from the
    entry parameters.
</p>  

<pre><code>import axios from 'axios';
import APIAddresses from './urls';

const makeRequest = async (type, url, data) =&gt; {
  try {
  const response =  await axios({
      url,
      data,
      method: type,
      headers:
        'Authorization': getTokenHeaderValue(),
        'Content-Type' : 'multipart/form-data'
      }
    });
    return response;
  } catch (error) {
    if(process.env.NODE_ENV !== 'production') {
      console.log(`Error: [${type}] - ${url}`);
      console.log(error);
    }
    return error;
  }
};

const get = url =&gt;  makeRequest('get', url, null);
const post = (url, data) =&gt; makeRequest('post', url, data);
const put = (url, data) =&gt;  makeRequest('put', url, data);
const remove = url =&gt; makeRequest('delete', url, null);
const query = data =&gt; `?${Object.keys(data).map(key =&gt; `${key}=${data[key]}`).join('&')}`;

export { APIAddresses, get, post, put, remove, query, postFile };

</code></pre>
<blockquote><p>  
    <code>APIAddresses</code> is imported and exported to make importing from a single
    source easier.
</p></blockquote>  

<p>  
    Following the current logic organization strategy, given in this example of using Express js API, you’ll get rid of
    unnecessary code snippets and improve the API concept for other developers or services overall. Take into account that if you change or update
    the API version, changing routes in one file will be enough.
</p>  

<h6>  
    Wrapping up
</h6>  

<p>  
    Every project is different in its idea and needs. I understand that it’s
    not always possible to keep up to a single development pattern, but any
    kind of personal experience can give light to a lot of things.
</p>  

<p>  
    Let’s shortly summarize the main ideas of the entire REST API tutorial:
</p>  

<ul>  
<li>Keep to REST logic</li>

<li>Organize Express js API (routes, events processing and permissions)</li>  
<li>Keep documentation on your API</li>  
<li>Organize your requests to avoid code duplications.</li>  
</ul>  

<p>  
    The correct organization techniques of your REST API will definitely reduce
    the development time and improve the overall quality of your project. Hope this Express js API tutorial will help you.
</p>  

<p>  
<a href="https://apiko.com/contact-us/" target="_blank">Let us know</a> if you've got something to add.  
</p>  


        
        

        
      
<a href="http://jasonwatmore.com/post/2017/09/16/react-redux-user-registration-and-login-tutorial-example">http://jasonwatmore.com/post/2017/09/16/react-redux-user-registration-and-login-tutorial-example</a><div id="articleHeader"><h1>React + Redux - User Registration and Login Tutorial & Example</h1></div>

        

        <p>Sep 27 2017 - Updated to <strong>React 16</strong>.</p>

<p>In this tutorial we'll cover how to implement user registration and login functionality with React and Redux. The tutorial demo is a React + Redux Boilerplate application that uses JWT authentication, it's based on the code from a real world secure web application I developed for a law firm in Sydney recently.</p>

<p>The project is available on GitHub at <a href="https://github.com/cornflourblue/react-redux-registration-login-example" target="_blank">https://github.com/cornflourblue/react-redux-registration-login-example</a>.</p>

<p>The boilerplate code uses a fake / mock backend that uses browser local storage for managing application data, to switch to a real backend api you just have to remove a couple of lines of code from the main react entry file (<code>/src/index.jsx</code>).</p>

<h2><br />
React + Redux Auth Boilerplate Demo</h2>

<p>Here's the login tutorial demo application in action on plunker.</p>

<p>(See on Plunker at <a href="http://plnkr.co/edit/eXV3Wa?p=preview" target="_blank">http://plnkr.co/edit/eXV3Wa?p=preview</a>)</p>

<p>Update History:</p>

<ul>
	<li>23 Oct 2017 - For an extended example with a real back-end API built with ASP.NET Core go to <a href="https://www.pointblankdevelopment.com.au/blog/124/react-redux-with-aspnet-core-20-login-registration-tutorial-example" target="_blank">React + Redux with ASP.NET Core 2.0 - Login & Registration Tutorial & Example</a></li>
	<li>27 Sep 2017 - Updated to <strong>React 16.0.0</strong></li>
	<li>16 Sep 2017 - For the same example built with Angular 2/4 check out <a href="/post/2016/09/29/angular-2-user-registration-and-login-example-tutorial" target="_blank">Angular 2/4 User Registration and Login Example & Tutorial</a></li>
	<li>16 Sep 2017 - Built with <strong>React 15.4.2</strong></li>
</ul>

<h2><br />
Running the React + Redux Boilerplate Demo Locally</h2>

<ol>
	<li>Install NodeJS and NPM from <a href="https://nodejs.org/en/download/" target="_blank">https://nodejs.org/en/download/</a>.</li>
	<li>Download or clone the project source code from <a href="https://github.com/cornflourblue/react-redux-registration-login-example" target="_blank">https://github.com/cornflourblue/react-redux-registration-login-example</a></li>
	<li>Install all required npm packages by running <code>npm install</code> from the command line in the project root folder (where the package.json is located).</li>
	<li>Start the application by running <code>npm start </code>from the command line in the project root folder, this will launch a browser displaying the application.</li>
</ol>

<h2><br />
React + Redux Project Structure</h2>

<p>All source code for the React + Redux tutorial app is located in the <code>/src</code> folder. Inside the src folder there is a folder per feature (App, HomePage, LoginPage, RegisterPage) and a bunch of folders for non-feature code that can be shared across different parts of the app (_actions, _components, _constants, _helpers, _reducers, _services).</p>

<p>I prefixed non-feature folders with an underscore "_" to group them together and make it easy to distinguish between features and non-features, it also keeps the project folder structure shallow so it's quick to see everything at a glance from the top level and to navigate around the project.</p>

<p>The index.js files in each folder are barrel files that group all the exported modules together so they can be imported using the folder path instead of the full module path and to enable importing multiple modules in a single import (e.g. <code>import { userActions, alertActions } from '../_actions'</code>).</p>

<p>Click any of the below links to jump down to a description of each file along with it's code:</p>





<h2>Redux Actions Folder</h2>

<div><strong>Path: /src/_actions</strong></div>

<p>The _actions folder contains all the Redux action creators for the project, I've organised the action creators into different files by action type (e.g. user actions, alert actions etc).</p>

<p>If you're not familiar with Redux actions or action creators you can learn about them at <a href="https://redux.js.org/basics/actions" target="_blank">https://redux.js.org/basics/actions</a>.</p>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Redux Alert Action Creators</h2>

<div><strong>Path: /src/_actions/alert.actions.js</strong></div>

<p>Contains Redux action creators for actions related to alerts / toaster notifications in the application. For example to display a success alert message with the text 'Registration Successful' you can call <code>dispatch(alertActions.success('Registration successful'));</code>.</p>

<p>I've wrapped the action methods in an <code>alertActions</code> object at the top of the file so it's easy to see all available actions at a glance and simplifies importing them into other files. The implementation details for each action creator are placed in the below functions.</p>

<div><div id="highlighter_757615"><table><tbody><tr><td></td><td><div><div><code>import { alertConstants } from </code><code>'../_constants'</code><code>;</code></div><div><code>export const alertActions = {</code></div><div><code>success,</code></div><div><code>error,</code></div><div><code>clear</code></div><div><code>};</code></div><div><code>function</code> <code>success(message) {</code></div><div><code>return</code> <code>{ type: alertConstants.SUCCESS, message };</code></div><div><code>}</code></div><div><code>function</code> <code>error(message) {</code></div><div><code>return</code> <code>{ type: alertConstants.ERROR, message };</code></div><div><code>}</code></div><div><code>function</code> <code>clear() {</code></div><div><code>return</code> <code>{ type: alertConstants.CLEAR };</code></div><div><code>}</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Redux User Action Creators</h2>

<div><strong>Path: /src/_actions/user.actions.js</strong></div>

<p>Contains Redux action creators for actions related to users. Public action creators are exposed via the <code>userActions</code> object at the top of the file and function implementations are located below, I like this structure because you can quickly see all of the actions that are available.</p>

<p>Most of the actions for users are async actions that are made up of multiple sub actions, this is because they have to make an http request and wait for the response before completing. Async actions typically dispatch a <code>request</code> action before performing an async task (e.g. an http request), and then dispatch a <code>success</code> or <code>error</code> action based on the result of the async task.</p>

<p>For example the <code>login()</code> action creator performs the following steps:</p>

<ol>
	<li>dispatches a <code>LOGIN_REQUEST</code> action with <code>dispatch(request({ username }));</code></li>
	<li>calls the async task <code>userService.login(username, password)</code></li>
	<li>dispatches a <code>LOGIN_SUCCESS</code> with <code>dispatch(success(user));</code> if login was successful, or dispatches a <code>LOGIN_FAILURE</code> action with <code>dispatch(failure(error));</code> if login failed</li>
</ol>

<p>To keep the code tidy I've put sub action creators into nested functions within each async action creator function. For example the <code>login()</code> function contains 3 nested action creator functions for <code>request()</code>, <code>success()</code> and <code>failure()</code> that return the actions <code>LOGIN_REQUEST</code>, <code>LOGIN_SUCCESS</code> and <code>LOGIN_FAILURE</code> respectively. Putting the sub action creators into nested functions also allows me to give them standard names like request, success and failure without clashing with other function names because they only exist within the scope of the parent function.</p>

<div><div id="highlighter_762637"><table><tbody><tr><td></td><td><div><div><code>import { userConstants } from </code><code>'../_constants'</code><code>;</code></div><div><code>import { userService } from </code><code>'../_services'</code><code>;</code></div><div><code>import { alertActions } from </code><code>'./'</code><code>;</code></div><div><code>import { history } from </code><code>'../_helpers'</code><code>;</code></div><div><code>export const userActions = {</code></div><div><code>login,</code></div><div><code>logout,</code></div><div><code>register,</code></div><div><code>getAll,</code></div><div><code>delete</code><code>: _delete</code></div><div><code>};</code></div><div><code>function</code> <code>login(username, password) {</code></div><div><code>return</code> <code>dispatch =&gt; {</code></div><div><code>dispatch(request({ username }));</code></div><div><code>userService.login(username, password)</code></div><div><code>.then(</code></div><div><code>user =&gt; { </code></div><div><code>dispatch(success(user));</code></div><div><code>history.push(</code><code>'/'</code><code>);</code></div><div><code>},</code></div><div><code>error =&gt; {</code></div><div><code>dispatch(failure(error));</code></div><div><code>dispatch(alertActions.error(error));</code></div><div><code>}</code></div><div><code>);</code></div><div><code>};</code></div><div><code>function</code> <code>request(user) { </code><code>return</code> <code>{ type: userConstants.LOGIN_REQUEST, user } }</code></div><div><code>function</code> <code>success(user) { </code><code>return</code> <code>{ type: userConstants.LOGIN_SUCCESS, user } }</code></div><div><code>function</code> <code>failure(error) { </code><code>return</code> <code>{ type: userConstants.LOGIN_FAILURE, error } }</code></div><div><code>}</code></div><div><code>function</code> <code>logout() {</code></div><div><code>userService.logout();</code></div><div><code>return</code> <code>{ type: userConstants.LOGOUT };</code></div><div><code>}</code></div><div><code>function</code> <code>register(user) {</code></div><div><code>return</code> <code>dispatch =&gt; {</code></div><div><code>dispatch(request(user));</code></div><div><code>userService.register(user)</code></div><div><code>.then(</code></div><div><code>user =&gt; { </code></div><div><code>dispatch(success());</code></div><div><code>history.push(</code><code>'/login'</code><code>);</code></div><div><code>dispatch(alertActions.success(</code><code>'Registration successful'</code><code>));</code></div><div><code>},</code></div><div><code>error =&gt; {</code></div><div><code>dispatch(failure(error));</code></div><div><code>dispatch(alertActions.error(error));</code></div><div><code>}</code></div><div><code>);</code></div><div><code>};</code></div><div><code>function</code> <code>request(user) { </code><code>return</code> <code>{ type: userConstants.REGISTER_REQUEST, user } }</code></div><div><code>function</code> <code>success(user) { </code><code>return</code> <code>{ type: userConstants.REGISTER_SUCCESS, user } }</code></div><div><code>function</code> <code>failure(error) { </code><code>return</code> <code>{ type: userConstants.REGISTER_FAILURE, error } }</code></div><div><code>}</code></div><div><code>function</code> <code>getAll() {</code></div><div><code>return</code> <code>dispatch =&gt; {</code></div><div><code>dispatch(request());</code></div><div><code>userService.getAll()</code></div><div><code>.then(</code></div><div><code>users =&gt; dispatch(success(users)),</code></div><div><code>error =&gt; { </code></div><div><code>dispatch(failure(error));</code></div><div><code>dispatch(alertActions.error(error))</code></div><div><code>}</code></div><div><code>);</code></div><div><code>};</code></div><div><code>function</code> <code>request() { </code><code>return</code> <code>{ type: userConstants.GETALL_REQUEST } }</code></div><div><code>function</code> <code>success(users) { </code><code>return</code> <code>{ type: userConstants.GETALL_SUCCESS, users } }</code></div><div><code>function</code> <code>failure(error) { </code><code>return</code> <code>{ type: userConstants.GETALL_FAILURE, error } }</code></div><div><code>}</code></div><div><code>// prefixed function name with underscore because delete is a reserved word in javascript</code></div><div><code>function</code> <code>_delete(id) {</code></div><div><code>return</code> <code>dispatch =&gt; {</code></div><div><code>dispatch(request(id));</code></div><div><code>userService.</code><code>delete</code><code>(id)</code></div><div><code>.then(</code></div><div><code>user =&gt; { </code></div><div><code>dispatch(success(id));</code></div><div><code>},</code></div><div><code>error =&gt; {</code></div><div><code>dispatch(failure(id, error));</code></div><div><code>}</code></div><div><code>);</code></div><div><code>};</code></div><div><code>function</code> <code>request(id) { </code><code>return</code> <code>{ type: userConstants.DELETE_REQUEST, id } }</code></div><div><code>function</code> <code>success(id) { </code><code>return</code> <code>{ type: userConstants.DELETE_SUCCESS, id } }</code></div><div><code>function</code> <code>failure(id, error) { </code><code>return</code> <code>{ type: userConstants.DELETE_FAILURE, id, error } }</code></div><div><code>}</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React Components Folder</h2>

<div><strong>Path: /src/_components</strong></div>

<p>The _components folder contains shared React components that can be used anywhere in the application.</p>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React Private Route Component</h2>

<div><strong>Path: /src/_components/PrivateRoute.jsx</strong></div>

<p>The react private route component renders a route component if the user is logged in, otherwise it redirects the user to the <code>/login</code> page.</p>

<p>The way it checks if the user is logged in is by checking that there is a <code>user</code> object in local storage. While it's possible to bypass this check by manually adding an object to local storage using browser dev tools, this would only give access to the client side component, it wouldn't give access to any real secure data from the server api because a valid authentication token (JWT) is required for this.</p>

<div><div id="highlighter_939651"><table><tbody><tr><td></td><td><div><div><code>import React from </code><code>'react'</code><code>;</code></div><div><code>import { Route, Redirect } from </code><code>'react-router-dom'</code><code>;</code></div><div><code>export const PrivateRoute = ({ component: Component, ...rest }) =&gt; (</code></div><div><code>&lt;Route {...rest} render={props =&gt; (</code></div><div><code>localStorage.getItem(</code><code>'user'</code><code>)</code></div><div><code>? &lt;Component {...props} /&gt;</code></div><div><code>: &lt;Redirect to={{ pathname: </code><code>'/login'</code><code>, state: { from: props.location } }} /&gt;</code></div><div><code>)} /&gt;</code></div><div><code>)</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Redux Action Constants Folder</h2>

<div><strong>Path: /src/_constants</strong></div>

<p>The _constants folder contains all of the redux action type constants used by redux action creators and reducers. It could be used for any other constants in the project as well, it doesn't have to be only for redux action types.</p>

<p>I decided to put redux action constants into their own files (rather than the same files as redux actions) to simplify my redux action files and keep them focused on one thing.</p>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Redux Alert Action Constants</h2>

<div><strong>Path: /src/_constants/alert.constants.js</strong></div>

<p>The alert constants object contains the redux alert action types used to display and clear alerts in the react application.</p>

<div><div id="highlighter_397945"><table><tbody><tr><td></td><td><div><div><code>export const alertConstants = {</code></div><div><code>SUCCESS: </code><code>'ALERT_SUCCESS'</code><code>,</code></div><div><code>ERROR: </code><code>'ALERT_ERROR'</code><code>,</code></div><div><code>CLEAR: </code><code>'ALERT_CLEAR'</code></div><div><code>};</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Redux User Action Constants</h2>

<div><strong>Path: /src/_constants/user.constants.js</strong></div>

<p>The user constants object contains the redux user action types that can be dispatched in the react application, async actions that perform http requests involve a request followed by a success or error response, so each of these three steps is represented by a redux action.</p>

<div><div id="highlighter_992621"><table><tbody><tr><td></td><td><div><div><code>export const userConstants = {</code></div><div><code>REGISTER_REQUEST: </code><code>'USERS_REGISTER_REQUEST'</code><code>,</code></div><div><code>REGISTER_SUCCESS: </code><code>'USERS_REGISTER_SUCCESS'</code><code>,</code></div><div><code>REGISTER_FAILURE: </code><code>'USERS_REGISTER_FAILURE'</code><code>,</code></div><div><code>LOGIN_REQUEST: </code><code>'USERS_LOGIN_REQUEST'</code><code>,</code></div><div><code>LOGIN_SUCCESS: </code><code>'USERS_LOGIN_SUCCESS'</code><code>,</code></div><div><code>LOGIN_FAILURE: </code><code>'USERS_LOGIN_FAILURE'</code><code>,</code></div><div><code>LOGOUT: </code><code>'USERS_LOGOUT'</code><code>,</code></div><div><code>GETALL_REQUEST: </code><code>'USERS_GETALL_REQUEST'</code><code>,</code></div><div><code>GETALL_SUCCESS: </code><code>'USERS_GETALL_SUCCESS'</code><code>,</code></div><div><code>GETALL_FAILURE: </code><code>'USERS_GETALL_FAILURE'</code><code>,</code></div><div><code>DELETE_REQUEST: </code><code>'USERS_DELETE_REQUEST'</code><code>,</code></div><div><code>DELETE_SUCCESS: </code><code>'USERS_DELETE_SUCCESS'</code><code>,</code></div><div><code>DELETE_FAILURE: </code><code>'USERS_DELETE_FAILURE'</code>   </div><div><code>};</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React + Redux Helpers Folder</h2>

<div><strong>Path: /src/_helpers</strong></div>

<p>The helpers folder contains all the bits and pieces that don't fit into other folders but don't justify having a folder of their own.</p>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React Auth Header</h2>

<div><strong>Path: /src/_helpers/auth-header.js</strong></div>

<p>Auth header is a helper function that returns an HTTP Authorization header containing the Json Web Token (JWT) of the currently logged in user from local storage. If the user isn't logged in an empty object is returned.</p>

<p>The auth header is used to make authenticated HTTP requests to the server api using JWT authentication.</p>

<div><div id="highlighter_713914"><table><tbody><tr><td></td><td><div><div><code>export </code><code>function</code> <code>authHeader() {</code></div><div><code>// return authorization header with jwt token</code></div><div><code>let user = JSON.parse(localStorage.getItem(</code><code>'user'</code><code>));</code></div><div><code>if</code> <code>(user && user.token) {</code></div><div><code>return</code> <code>{ </code><code>'Authorization'</code><code>: </code><code>'Bearer '</code> <code>+ user.token };</code></div><div><code>} </code><code>else</code> <code>{</code></div><div><code>return</code> <code>{};</code></div><div><code>}</code></div><div><code>}</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React Fake / Mock Backend</h2>

<div><strong>Path: /src/_helpers/fake-backend.js</strong></div>

<p>The fake backend is used for running the example api without a server api (backend-less). It monkey patches the <code>fetch()</code> function to intercept certain api requests and mimic the behaviour of a real api by managing data in browser local storage. Any requests that aren't intercepted get passed through to the real <code>fetch()</code> function.</p>

<div><div id="highlighter_946873"><table><tbody><tr><td></td><td><div><div><code>// array in local storage for registered users</code></div><div><code>let users = JSON.parse(localStorage.getItem(</code><code>'users'</code><code>)) || [];</code></div><div><code>export </code><code>function</code> <code>configureFakeBackend() {</code></div><div><code>let realFetch = window.fetch;</code></div><div><code>window.fetch = </code><code>function</code> <code>(url, opts) {</code></div><div><code>return</code> <code>new</code> <code>Promise((resolve, reject) =&gt; {</code></div><div><code>// wrap in timeout to simulate server api call</code></div><div><code>setTimeout(() =&gt; {</code></div><div><code>// authenticate</code></div><div><code>if</code> <code>(url.endsWith(</code><code>'/users/authenticate'</code><code>) && opts.method === </code><code>'POST'</code><code>) {</code></div><div><code>// get parameters from post request</code></div><div><code>let params = JSON.parse(opts.body);</code></div><div><code>// find if any user matches login credentials</code></div><div><code>let filteredUsers = users.filter(user =&gt; {</code></div><div><code>return</code> <code>user.username === params.username && user.password === params.password;</code></div><div><code>});</code></div><div><code>if</code> <code>(filteredUsers.length) {</code></div><div><code>// if login details are valid return user details and fake jwt token</code></div><div><code>let user = filteredUsers[0];</code></div><div><code>let responseJson = {</code></div><div><code>id: user.id,</code></div><div><code>username: user.username,</code></div><div><code>firstName: user.firstName,</code></div><div><code>lastName: user.lastName,</code></div><div><code>token: </code><code>'fake-jwt-token'</code></div><div><code>};</code></div><div><code>resolve({ ok: </code><code>true</code><code>, json: () =&gt; responseJson });</code></div><div><code>} </code><code>else</code> <code>{</code></div><div><code>// else return error</code></div><div><code>reject(</code><code>'Username or password is incorrect'</code><code>);</code></div><div><code>}</code></div><div><code>return</code><code>;</code></div><div><code>}</code></div><div><code>// get users</code></div><div><code>if</code> <code>(url.endsWith(</code><code>'/users'</code><code>) && opts.method === </code><code>'GET'</code><code>) {</code></div><div><code>// check for fake auth token in header and return users if valid, this security is implemented server side in a real application</code></div><div><code>if</code> <code>(opts.headers && opts.headers.Authorization === </code><code>'Bearer fake-jwt-token'</code><code>) {</code></div><div><code>resolve({ ok: </code><code>true</code><code>, json: () =&gt; users });</code></div><div><code>} </code><code>else</code> <code>{</code></div><div><code>// return 401 not authorised if token is null or invalid</code></div><div><code>reject(</code><code>'Unauthorised'</code><code>);</code></div><div><code>}</code></div><div><code>return</code><code>;</code></div><div><code>}</code></div><div><code>// get user by id</code></div><div><code>if</code> <code>(url.match(/\/users\/\d+$/) && opts.method === </code><code>'GET'</code><code>) {</code></div><div><code>// check for fake auth token in header and return user if valid, this security is implemented server side in a real application</code></div><div><code>if</code> <code>(opts.headers && opts.headers.Authorization === </code><code>'Bearer fake-jwt-token'</code><code>) {</code></div><div><code>// find user by id in users array</code></div><div><code>let urlParts = url.split(</code><code>'/'</code><code>);</code></div><div><code>let id = parseInt(urlParts[urlParts.length - 1]);</code></div><div><code>let matchedUsers = users.filter(user =&gt; { </code><code>return</code> <code>user.id === id; });</code></div><div><code>let user = matchedUsers.length ? matchedUsers[0] : </code><code>null</code><code>;</code></div><div><code>// respond 200 OK with user</code></div><div><code>resolve({ ok: </code><code>true</code><code>, json: () =&gt; user});</code></div><div><code>} </code><code>else</code> <code>{</code></div><div><code>// return 401 not authorised if token is null or invalid</code></div><div><code>reject(</code><code>'Unauthorised'</code><code>);</code></div><div><code>}</code></div><div><code>return</code><code>;</code></div><div><code>}</code></div><div><code>// register user</code></div><div><code>if</code> <code>(url.endsWith(</code><code>'/users/register'</code><code>) && opts.method === </code><code>'POST'</code><code>) {</code></div><div><code>// get new user object from post body</code></div><div><code>let newUser = JSON.parse(opts.body);</code></div><div><code>// validation</code></div><div><code>let duplicateUser = users.filter(user =&gt; { </code><code>return</code> <code>user.username === newUser.username; }).length;</code></div><div><code>if</code> <code>(duplicateUser) {</code></div><div><code>reject(</code><code>'Username "'</code> <code>+ newUser.username + </code><code>'" is already taken'</code><code>);</code></div><div><code>return</code><code>;</code></div><div><code>}</code></div><div><code>// save new user</code></div><div><code>newUser.id = Math.max(...users.map(user =&gt; user.id)) + 1;</code></div><div><code>users.push(newUser);</code></div><div><code>localStorage.setItem(</code><code>'users'</code><code>, JSON.stringify(users));</code></div><div><code>// respond 200 OK</code></div><div><code>resolve({ ok: </code><code>true</code><code>, json: () =&gt; ({}) });</code></div><div><code>return</code><code>;</code></div><div><code>}</code></div><div><code>// delete user</code></div><div><code>if</code> <code>(url.match(/\/users\/\d+$/) && opts.method === </code><code>'DELETE'</code><code>) {</code></div><div><code>// check for fake auth token in header and return user if valid, this security is implemented server side in a real application</code></div><div><code>if</code> <code>(opts.headers && opts.headers.Authorization === </code><code>'Bearer fake-jwt-token'</code><code>) {</code></div><div><code>// find user by id in users array</code></div><div><code>let urlParts = url.split(</code><code>'/'</code><code>);</code></div><div><code>let id = parseInt(urlParts[urlParts.length - 1]);</code></div><div><code>for</code> <code>(let i = 0; i &lt; users.length; i++) {</code></div><div><code>let user = users[i];</code></div><div><code>if</code> <code>(user.id === id) {</code></div><div><code>// delete user</code></div><div><code>users.splice(i, 1);</code></div><div><code>localStorage.setItem(</code><code>'users'</code><code>, JSON.stringify(users));</code></div><div><code>break</code><code>;</code></div><div><code>}</code></div><div><code>}</code></div><div><code>// respond 200 OK</code></div><div><code>resolve({ ok: </code><code>true</code><code>, json: () =&gt; ({}) });</code></div><div><code>} </code><code>else</code> <code>{</code></div><div><code>// return 401 not authorised if token is null or invalid</code></div><div><code>reject(</code><code>'Unauthorised'</code><code>);</code></div><div><code>}</code></div><div><code>return</code><code>;</code></div><div><code>}</code></div><div><code>// pass through any requests not handled above</code></div><div><code>realFetch(url, opts).then(response =&gt; resolve(response));</code></div><div><code>}, 500);</code></div><div><code>});</code></div><div><code>}</code></div><div><code>}</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React Router History</h2>

<div><strong>Path: /src/_helpers/history.js</strong></div>

<p>The history is a custom history object used by the React Router, the reason I used a custom history object instead of the built into React Router is to enable redirecting users from outside React components, for example from the user actions after successful login or registration.</p>

<div><div id="highlighter_13052"><table><tbody><tr><td></td><td><div><div><code>import { createBrowserHistory } from </code><code>'history'</code><code>;</code></div><div><code>export const history = createBrowserHistory();</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Redux Store</h2>

<div><strong>Path: /src/_helpers/store.js</strong></div>

<div><div id="highlighter_532184"><table><tbody><tr><td></td><td><div><div><code>import { createStore, applyMiddleware } from </code><code>'redux'</code><code>;</code></div><div><code>import thunkMiddleware from </code><code>'redux-thunk'</code><code>;</code></div><div><code>import { createLogger } from </code><code>'redux-logger'</code><code>;</code></div><div><code>import rootReducer from </code><code>'../_reducers'</code><code>;</code></div><div><code>const loggerMiddleware = createLogger();</code></div><div><code>export const store = createStore(</code></div><div><code>rootReducer,</code></div><div><code>applyMiddleware(</code></div><div><code>thunkMiddleware,</code></div><div><code>loggerMiddleware</code></div><div><code>)</code></div><div><code>);</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Redux Reducers Folder</h2>

<div><strong>Path: /src/_reducers</strong></div>

<p>The _reducers folder contains all the Redux reducers for the project, each reducer updates a different part of the application state in response to dispatched redux actions.</p>

<p>If you're not familiar with Redux reducers you can learn about them at <a href="https://redux.js.org/basics/reducers" target="_blank">https://redux.js.org/basics/reducers</a>.</p>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Redux Alert Reducer</h2>

<div><strong>Path: /src/_reducers/alert.reducer.js</strong></div>

<p>The redux alert reducer manages the application state for alerts / toaster notifications, it updates state when an alert action is dispatched from anywhere in the application, for example when an <code>alertConstants.SUCCESS</code> action is dispatched, the reducer updates the alert state to an object with <code>type: 'alert-success'</code> and <code>message: action.message</code>.</p>

<div><div id="highlighter_704644"><table><tbody><tr><td></td><td><div><div><code>import { alertConstants } from </code><code>'../_constants'</code><code>;</code></div><div><code>export </code><code>function</code> <code>alert(state = {}, action) {</code></div><div><code>switch</code> <code>(action.type) {</code></div><div><code>case</code> <code>alertConstants.SUCCESS:</code></div><div><code>return</code> <code>{</code></div><div><code>type: </code><code>'alert-success'</code><code>,</code></div><div><code>message: action.message</code></div><div><code>};</code></div><div><code>case</code> <code>alertConstants.ERROR:</code></div><div><code>return</code> <code>{</code></div><div><code>type: </code><code>'alert-danger'</code><code>,</code></div><div><code>message: action.message</code></div><div><code>};</code></div><div><code>case</code> <code>alertConstants.CLEAR:</code></div><div><code>return</code> <code>{};</code></div><div><code>default</code><code>:</code></div><div><code>return</code> <code>state</code></div><div><code>}</code></div><div><code>}</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Redux Authentication Reducer</h2>

<div><strong>Path: /src/_reducers/authentication.reducer.js</strong></div>

<p>The redux authentication reducer manages the state related to login (and logout) actions, on successful login the current user object and a loggedIn flag are stored in the <code>authentication</code> section of the application state. On logout or login failure the authentication state is set to an empty object, and during login (between login request and success/failure) the authentication state has a loggingIn flag set to true and a user object with the details of the user that is attempting to login.</p>

<div><div id="highlighter_188981"><table><tbody><tr><td></td><td><div><div><code>import { userConstants } from </code><code>'../_constants'</code><code>;</code></div><div><code>let user = JSON.parse(localStorage.getItem(</code><code>'user'</code><code>));</code></div><div><code>const initialState = user ? { loggedIn: </code><code>true</code><code>, user } : {};</code></div><div><code>export </code><code>function</code> <code>authentication(state = initialState, action) {</code></div><div><code>switch</code> <code>(action.type) {</code></div><div><code>case</code> <code>userConstants.LOGIN_REQUEST:</code></div><div><code>return</code> <code>{</code></div><div><code>loggingIn: </code><code>true</code><code>,</code></div><div><code>user: action.user</code></div><div><code>};</code></div><div><code>case</code> <code>userConstants.LOGIN_SUCCESS:</code></div><div><code>return</code> <code>{</code></div><div><code>loggedIn: </code><code>true</code><code>,</code></div><div><code>user: action.user</code></div><div><code>};</code></div><div><code>case</code> <code>userConstants.LOGIN_FAILURE:</code></div><div><code>return</code> <code>{};</code></div><div><code>case</code> <code>userConstants.LOGOUT:</code></div><div><code>return</code> <code>{};</code></div><div><code>default</code><code>:</code></div><div><code>return</code> <code>state</code></div><div><code>}</code></div><div><code>}</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Redux Registration Reducer</h2>

<div><strong>Path: /src/_reducers/registration.reducer.js</strong></div>

<p>The redux registration reducer manages the <code>registration</code> section of the application state, as you can see there isn't much to it, on registration request it just sets a <code>registering</code> flag set to true which the RegisterPage uses to show the loading spinner. On register success or failure it clears the registration state.</p>

<div><div id="highlighter_818256"><table><tbody><tr><td></td><td><div><div><code>import { userConstants } from </code><code>'../_constants'</code><code>;</code></div><div><code>export </code><code>function</code> <code>registration(state = {}, action) {</code></div><div><code>switch</code> <code>(action.type) {</code></div><div><code>case</code> <code>userConstants.REGISTER_REQUEST:</code></div><div><code>return</code> <code>{ registering: </code><code>true</code> <code>};</code></div><div><code>case</code> <code>userConstants.REGISTER_SUCCESS:</code></div><div><code>return</code> <code>{};</code></div><div><code>case</code> <code>userConstants.REGISTER_FAILURE:</code></div><div><code>return</code> <code>{};</code></div><div><code>default</code><code>:</code></div><div><code>return</code> <code>state</code></div><div><code>}</code></div><div><code>}</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Redux Users Reducer</h2>

<div><strong>Path: /src/_reducers/users.reducer.js</strong></div>

<p>The redux users reducer manages the <code>users</code> section of the application state which is used by the HomePage to display a list of users and enable deleting of users.</p>

<div><div id="highlighter_676075"><table><tbody><tr><td></td><td><div><div><code>import { userConstants } from </code><code>'../_constants'</code><code>;</code></div><div><code>export </code><code>function</code> <code>users(state = {}, action) {</code></div><div><code>switch</code> <code>(action.type) {</code></div><div><code>case</code> <code>userConstants.GETALL_REQUEST:</code></div><div><code>return</code> <code>{</code></div><div><code>loading: </code><code>true</code></div><div><code>};</code></div><div><code>case</code> <code>userConstants.GETALL_SUCCESS:</code></div><div><code>return</code> <code>{</code></div><div><code>items: action.users</code></div><div><code>};</code></div><div><code>case</code> <code>userConstants.GETALL_FAILURE:</code></div><div><code>return</code> <code>{ </code></div><div><code>error: action.error</code></div><div><code>};</code></div><div><code>case</code> <code>userConstants.DELETE_REQUEST:</code></div><div><code>// add 'deleting:true' property to user being deleted</code></div><div><code>return</code> <code>{</code></div><div><code>...state,</code></div><div><code>items: state.items.map(user =&gt;</code></div><div><code>user.id === action.id</code></div><div><code>? { ...user, deleting: </code><code>true</code> <code>}</code></div><div><code>: user</code></div><div><code>)</code></div><div><code>};</code></div><div><code>case</code> <code>userConstants.DELETE_SUCCESS:</code></div><div><code>// remove deleted user from state</code></div><div><code>return</code> <code>{</code></div><div><code>items: state.items.filter(user =&gt; user.id !== action.id)</code></div><div><code>};</code></div><div><code>case</code> <code>userConstants.DELETE_FAILURE:</code></div><div><code>// remove 'deleting:true' property and add 'deleteError:[error]' property to user </code></div><div><code>return</code> <code>{</code></div><div><code>...state,</code></div><div><code>items: state.items.map(user =&gt; {</code></div><div><code>if</code> <code>(user.id === action.id) {</code></div><div><code>// make copy of user without 'deleting:true' property</code></div><div><code>const { deleting, ...userCopy } = user;</code></div><div><code>// return copy of user with 'deleteError:[error]' property</code></div><div><code>return</code> <code>{ ...userCopy, deleteError: action.error };</code></div><div><code>}</code></div><div><code>return</code> <code>user;</code></div><div><code>})</code></div><div><code>};</code></div><div><code>default</code><code>:</code></div><div><code>return</code> <code>state</code></div><div><code>}</code></div><div><code>}</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React + Redux Services Folder</h2>

<div><strong>Path: /src/_services</strong></div>

<p>The _services layer handles all http communication with backend apis for the application, each service encapsulates the api calls for a content type (e.g. users) and exposes methods for performing various operations (e.g. CRUD operations). Services can also have methods that don't wrap http calls, for example the <code>userService.logout()</code> method just removes an item from local storage.</p>

<p>I like wrapping http calls and implementation details in a services layer, it provides a clean separation of concerns and simplifies the redux actions (and other modules) that use the services.</p>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React + Redux User Service</h2>

<div><strong>Path: /src/_services/user.service.js</strong></div>

<p>The user service encapsulates all backend api calls for performing CRUD operations on user data, as well as logging and out of the example application. The service methods are exported via the <code>userService</code> object at the top of the file, and the implementation of each method is located in the function declarations below.</p>

<div><div id="highlighter_993197"><table><tbody><tr><td></td><td><div><div><code>import { authHeader } from </code><code>'../_helpers'</code><code>;</code></div><div><code>export const userService = {</code></div><div><code>login,</code></div><div><code>logout,</code></div><div><code>register,</code></div><div><code>getAll,</code></div><div><code>getById,</code></div><div><code>update,</code></div><div><code>delete</code><code>: _delete</code></div><div><code>};</code></div><div><code>function</code> <code>login(username, password) {</code></div><div><code>const requestOptions = {</code></div><div><code>method: </code><code>'POST'</code><code>,</code></div><div><code>headers: { </code><code>'Content-Type'</code><code>: </code><code>'application/json'</code> <code>},</code></div><div><code>body: JSON.stringify({ username, password })</code></div><div><code>};</code></div><div><code>return</code> <code>fetch(</code><code>'/users/authenticate'</code><code>, requestOptions)</code></div><div><code>.then(response =&gt; {</code></div><div><code>if</code> <code>(!response.ok) { </code></div><div><code>return</code> <code>Promise.reject(response.statusText);</code></div><div><code>}</code></div><div><code>return</code> <code>response.json();</code></div><div><code>})</code></div><div><code>.then(user =&gt; {</code></div><div><code>// login successful if there's a jwt token in the response</code></div><div><code>if</code> <code>(user && user.token) {</code></div><div><code>// store user details and jwt token in local storage to keep user logged in between page refreshes</code></div><div><code>localStorage.setItem('user</code><code>', JSON.stringify(user));</code></div><div><code>}</code></div><div><code>return user;</code></div><div><code>});</code></div><div><code>}</code></div><div><code>function logout() {</code></div><div><code>// remove user from local storage to log user out</code></div><div><code>localStorage.removeItem('</code><code>user</code><code>');</code></div><div><code>}</code></div><div><code>function getAll() {</code></div><div><code>const requestOptions = {</code></div><div><code>method: '</code><code>GET</code><code>',</code></div><div><code>headers: authHeader()</code></div><div><code>};</code></div><div><code>return fetch('</code><code>/users</code><code>', requestOptions).then(handleResponse);</code></div><div><code>}</code></div><div><code>function getById(id) {</code></div><div><code>const requestOptions = {</code></div><div><code>method: '</code><code>GET</code><code>',</code></div><div><code>headers: authHeader()</code></div><div><code>};</code></div><div><code>return fetch('</code><code>/users/</code><code>' + _id, requestOptions).then(handleResponse);</code></div><div><code>}</code></div><div><code>function register(user) {</code></div><div><code>const requestOptions = {</code></div><div><code>method: '</code><code>POST</code><code>',</code></div><div><code>headers: { '</code><code>Content-Type</code><code>': '</code><code>application/json</code><code>' },</code></div><div><code>body: JSON.stringify(user)</code></div><div><code>};</code></div><div><code>return fetch('</code><code>/users/register</code><code>', requestOptions).then(handleResponse);</code></div><div><code>}</code></div><div><code>function update(user) {</code></div><div><code>const requestOptions = {</code></div><div><code>method: '</code><code>PUT</code><code>',</code></div><div><code>headers: { ...authHeader(), '</code><code>Content-Type</code><code>': '</code><code>application/json</code><code>' },</code></div><div><code>body: JSON.stringify(user)</code></div><div><code>};</code></div><div><code>return fetch('</code><code>/users/</code><code>' + user.id, requestOptions).then(handleResponse);;</code></div><div><code>}</code></div><div><code>// prefixed function name with underscore because delete is a reserved word in javascript</code></div><div><code>function _delete(id) {</code></div><div><code>const requestOptions = {</code></div><div><code>method: '</code><code>DELETE</code><code>',</code></div><div><code>headers: authHeader()</code></div><div><code>};</code></div><div><code>return fetch('</code><code>/users/' + id, requestOptions).then(handleResponse);;</code></div><div><code>}</code></div><div><code>function</code> <code>handleResponse(response) {</code></div><div><code>if</code> <code>(!response.ok) { </code></div><div><code>return</code> <code>Promise.reject(response.statusText);</code></div><div><code>}</code></div><div><code>return</code> <code>response.json();</code></div><div><code>}</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React + Redux App Folder</h2>

<div><strong>Path: /src/App</strong></div>

<p>The app folder is for react components and other code that is used only by the app component in the tutorial application.</p>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React + Redux App Component</h2>

<div><strong>Path: /src/App/App.jsx</strong></div>

<p>The app component is the root component for the react tutorial application, it contains the outer html, routes and global alert notification for the example app.</p>

<div><div id="highlighter_284850"><table><tbody><tr><td></td><td><div><div><code>import React from </code><code>'react'</code><code>;</code></div><div><code>import { Router, Route } from </code><code>'react-router-dom'</code><code>;</code></div><div><code>import { connect } from </code><code>'react-redux'</code><code>;</code></div><div><code>import { history } from </code><code>'../_helpers'</code><code>;</code></div><div><code>import { alertActions } from </code><code>'../_actions'</code><code>;</code></div><div><code>import { PrivateRoute } from </code><code>'../_components'</code><code>;</code></div><div><code>import { HomePage } from </code><code>'../HomePage'</code><code>;</code></div><div><code>import { LoginPage } from </code><code>'../LoginPage'</code><code>;</code></div><div><code>import { RegisterPage } from </code><code>'../RegisterPage'</code><code>;</code></div><div><code>class App extends React.Component {</code></div><div><code>constructor(props) {</code></div><div><code>super</code><code>(props);</code></div><div><code>const { dispatch } = </code><code>this</code><code>.props;</code></div><div><code>history.listen((location, action) =&gt; {</code></div><div><code>// clear alert on location change</code></div><div><code>dispatch(alertActions.clear());</code></div><div><code>});</code></div><div><code>}</code></div><div><code>render() {</code></div><div><code>const { alert } = </code><code>this</code><code>.props;</code></div><div><code>return</code> <code>(</code></div><div><code>&lt;div className=</code><code>"jumbotron"</code><code>&gt;</code></div><div><code>&lt;div className=</code><code>"container"</code><code>&gt;</code></div><div><code>&lt;div className=</code><code>"col-sm-8 col-sm-offset-2"</code><code>&gt;</code></div><div><code>{alert.message &&</code></div><div><code>&lt;div className={`alert ${alert.type}`}&gt;{alert.message}&lt;/div&gt;</code></div><div><code>}</code></div><div><code>&lt;Router history={history}&gt;</code></div><div><code>&lt;div&gt;</code></div><div><code>&lt;PrivateRoute exact path=</code><code>"/"</code> <code>component={HomePage} /&gt;</code></div><div><code>&lt;Route path=</code><code>"/login"</code> <code>component={LoginPage} /&gt;</code></div><div><code>&lt;Route path=</code><code>"/register"</code> <code>component={RegisterPage} /&gt;</code></div><div><code>&lt;/div&gt;</code></div><div><code>&lt;/Router&gt;</code></div><div><code>&lt;/div&gt;</code></div><div><code>&lt;/div&gt;</code></div><div><code>&lt;/div&gt;</code></div><div><code>);</code></div><div><code>}</code></div><div><code>}</code></div><div><code>function</code> <code>mapStateToProps(state) {</code></div><div><code>const { alert } = state;</code></div><div><code>return</code> <code>{</code></div><div><code>alert</code></div><div><code>};</code></div><div><code>}</code></div><div><code>const connectedApp = connect(mapStateToProps)(App);</code></div><div><code>export { connectedApp as App };</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React + Redux Home Page Folder</h2>

<div><strong>Path: /src/HomePage</strong></div>

<p>The home page folder is for react components and other code that is used only by the home page component in the tutorial application.</p>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React + Redux Home Page Component</h2>

<div><strong>Path: /src/HomePage/HomePage.jsx</strong></div>

<p>The home page component is displayed after signing in to the application, it shows the signed in user's name plus a list of all registered users in the tutorial application. The users are loaded into redux state by dispatching the redux action <code>userActions.getAll()</code> from the <code>componentDidMount()</code> react lifecycle hook.</p>

<p>Users can also be deleted from the user list, when the delete link is clicked it triggers the redux action <code>userActions.delete(id)</code> to be dispatched.</p>

<div><div id="highlighter_763520"><table><tbody><tr><td></td><td><div><div><code>import React from </code><code>'react'</code><code>;</code></div><div><code>import { Link } from </code><code>'react-router-dom'</code><code>;</code></div><div><code>import { connect } from </code><code>'react-redux'</code><code>;</code></div><div><code>import { userActions } from </code><code>'../_actions'</code><code>;</code></div><div><code>class HomePage extends React.Component {</code></div><div><code>componentDidMount() {</code></div><div><code>this</code><code>.props.dispatch(userActions.getAll());</code></div><div><code>}</code></div><div><code>handleDeleteUser(id) {</code></div><div><code>return</code> <code>(e) =&gt; </code><code>this</code><code>.props.dispatch(userActions.</code><code>delete</code><code>(id));</code></div><div><code>}</code></div><div><code>render() {</code></div><div><code>const { user, users } = </code><code>this</code><code>.props;</code></div><div><code>return</code> <code>(</code></div><div><code>&lt;div className=</code><code>"col-md-6 col-md-offset-3"</code><code>&gt;</code></div><div><code>&lt;h1&gt;Hi {user.firstName}!&lt;/h1&gt;</code></div><div><code>&lt;p&gt;You</code><code>'re logged in with React!!&lt;/p&gt;</code></div><div><code>&lt;h3&gt;All registered users:&lt;/h3&gt;</code></div><div><code>{users.loading && &lt;em&gt;Loading users...&lt;/em&gt;}</code></div><div><code>{users.items &&</code></div><div><code>&lt;ul&gt;</code></div><div><code>{users.items.map((user, index) =&gt;</code></div><div><code>&lt;li key={user.id}&gt;</code></div><div><code>{user.firstName + '</code> <code>' + user.lastName}</code></div><div><code>{</code></div><div><code>user.deleting ? &lt;em&gt; - Deleting...&lt;/em&gt;</code></div><div><code>: user.deleteError ? &lt;span className=</code><code>"error"</code><code>&gt; - ERROR: {user.deleteError}&lt;/span&gt;</code></div><div><code>: &lt;span&gt; - &lt;a onClick={</code><code>this</code><code>.handleDeleteUser(user.id)}&gt;Delete&lt;/a&gt;&lt;/span&gt;</code></div><div><code>}</code></div><div><code>&lt;/li&gt;</code></div><div><code>)}</code></div><div><code>&lt;/ul&gt;</code></div><div><code>}</code></div><div><code>&lt;p&gt;</code></div><div><code>&lt;Link to=</code><code>"/login"</code><code>&gt;Logout&lt;/Link&gt;</code></div><div><code>&lt;/p&gt;</code></div><div><code>&lt;/div&gt;</code></div><div><code>);</code></div><div><code>}</code></div><div><code>}</code></div><div><code>function</code> <code>mapStateToProps(state) {</code></div><div><code>const { users, authentication } = state;</code></div><div><code>const { user } = authentication;</code></div><div><code>return</code> <code>{</code></div><div><code>user,</code></div><div><code>users</code></div><div><code>};</code></div><div><code>}</code></div><div><code>const connectedHomePage = connect(mapStateToProps)(HomePage);</code></div><div><code>export { connectedHomePage as HomePage };</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React + Redux Login Page Folder</h2>

<div><strong>Path: /src/LoginPage</strong></div>

<p>The login page folder is for react components and other code that is used only by the login page component in the tutorial application.</p>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React + Redux Login Page Component</h2>

<div><strong>Path: /src/LoginPage/LoginPage.jsx</strong></div>

<p>The login page component renders a login form with username and password fields. It displays validation messages for invalid fields when the user attempts to submit the form. If the form is valid, submitting it causes the <code>userActions.login(username, password)</code> redux action to be dispatched.</p>

<p>In the <code>constructor()</code> function the <code>userActions.logout()</code> redux action is dispatched which logs the user out if they're logged in, this enables the login page to also be used as the logout page.</p>

<div><div id="highlighter_873333"><table><tbody><tr><td></td><td><div><div><code>import React from </code><code>'react'</code><code>;</code></div><div><code>import { Link } from </code><code>'react-router-dom'</code><code>;</code></div><div><code>import { connect } from </code><code>'react-redux'</code><code>;</code></div><div><code>import { userActions } from </code><code>'../_actions'</code><code>;</code></div><div><code>class LoginPage extends React.Component {</code></div><div><code>constructor(props) {</code></div><div><code>super</code><code>(props);</code></div><div><code>// reset login status</code></div><div><code>this</code><code>.props.dispatch(userActions.logout());</code></div><div><code>this</code><code>.state = {</code></div><div><code>username: </code><code>''</code><code>,</code></div><div><code>password: </code><code>''</code><code>,</code></div><div><code>submitted: </code><code>false</code></div><div><code>};</code></div><div><code>this</code><code>.handleChange = </code><code>this</code><code>.handleChange.bind(</code><code>this</code><code>);</code></div><div><code>this</code><code>.handleSubmit = </code><code>this</code><code>.handleSubmit.bind(</code><code>this</code><code>);</code></div><div><code>}</code></div><div><code>handleChange(e) {</code></div><div><code>const { name, value } = e.target;</code></div><div><code>this</code><code>.setState({ [name]: value });</code></div><div><code>}</code></div><div><code>handleSubmit(e) {</code></div><div><code>e.preventDefault();</code></div><div><code>this</code><code>.setState({ submitted: </code><code>true</code> <code>});</code></div><div><code>const { username, password } = </code><code>this</code><code>.state;</code></div><div><code>const { dispatch } = </code><code>this</code><code>.props;</code></div><div><code>if</code> <code>(username && password) {</code></div><div><code>dispatch(userActions.login(username, password));</code></div><div><code>}</code></div><div><code>}</code></div><div><code>render() {</code></div><div><code>const { loggingIn } = </code><code>this</code><code>.props;</code></div><div><code>const { username, password, submitted } = </code><code>this</code><code>.state;</code></div><div><code>return</code> <code>(</code></div><div><code>&lt;div className=</code><code>"col-md-6 col-md-offset-3"</code><code>&gt;</code></div><div><code>&lt;h2&gt;Login&lt;/h2&gt;</code></div><div><code>&lt;form name=</code><code>"form"</code> <code>onSubmit={</code><code>this</code><code>.handleSubmit}&gt;</code></div><div><code>&lt;div className={</code><code>'form-group'</code> <code>+ (submitted && !username ? </code><code>' has-error'</code> <code>: </code><code>''</code><code>)}&gt;</code></div><div><code>&lt;label htmlFor=</code><code>"username"</code><code>&gt;Username&lt;/label&gt;</code></div><div><code>&lt;input type=</code><code>"text"</code> <code>className=</code><code>"form-control"</code> <code>name=</code><code>"username"</code> <code>value={username} onChange={</code><code>this</code><code>.handleChange} /&gt;</code></div><div><code>{submitted && !username &&</code></div><div><code>&lt;div className=</code><code>"help-block"</code><code>&gt;Username is required&lt;/div&gt;</code></div><div><code>}</code></div><div><code>&lt;/div&gt;</code></div><div><code>&lt;div className={</code><code>'form-group'</code> <code>+ (submitted && !password ? </code><code>' has-error'</code> <code>: </code><code>''</code><code>)}&gt;</code></div><div><code>&lt;label htmlFor=</code><code>"password"</code><code>&gt;Password&lt;/label&gt;</code></div><div><code>&lt;input type=</code><code>"password"</code> <code>className=</code><code>"form-control"</code> <code>name=</code><code>"password"</code> <code>value={password} onChange={</code><code>this</code><code>.handleChange} /&gt;</code></div><div><code>{submitted && !password &&</code></div><div><code>&lt;div className=</code><code>"help-block"</code><code>&gt;Password is required&lt;/div&gt;</code></div><div><code>}</code></div><div><code>&lt;/div&gt;</code></div><div><code>&lt;div className=</code><code>"form-group"</code><code>&gt;</code></div><div><code>&lt;button className=</code><code>"btn btn-primary"</code><code>&gt;Login&lt;/button&gt;</code></div><div><code>{loggingIn &&</code></div><div><code>&lt;img src=</code><code>"data:image/gif;base64,R0lGODlhEAAQAPIAAP///wAAAMLCwkJCQgAAAGJiYoKCgpKSkiH/C05FVFNDQVBFMi4wAwEAAAAh/hpDcmVhdGVkIHdpdGggYWpheGxvYWQuaW5mbwAh+QQJCgAAACwAAAAAEAAQAAADMwi63P4wyklrE2MIOggZnAdOmGYJRbExwroUmcG2LmDEwnHQLVsYOd2mBzkYDAdKa+dIAAAh+QQJCgAAACwAAAAAEAAQAAADNAi63P5OjCEgG4QMu7DmikRxQlFUYDEZIGBMRVsaqHwctXXf7WEYB4Ag1xjihkMZsiUkKhIAIfkECQoAAAAsAAAAABAAEAAAAzYIujIjK8pByJDMlFYvBoVjHA70GU7xSUJhmKtwHPAKzLO9HMaoKwJZ7Rf8AYPDDzKpZBqfvwQAIfkECQoAAAAsAAAAABAAEAAAAzMIumIlK8oyhpHsnFZfhYumCYUhDAQxRIdhHBGqRoKw0R8DYlJd8z0fMDgsGo/IpHI5TAAAIfkECQoAAAAsAAAAABAAEAAAAzIIunInK0rnZBTwGPNMgQwmdsNgXGJUlIWEuR5oWUIpz8pAEAMe6TwfwyYsGo/IpFKSAAAh+QQJCgAAACwAAAAAEAAQAAADMwi6IMKQORfjdOe82p4wGccc4CEuQradylesojEMBgsUc2G7sDX3lQGBMLAJibufbSlKAAAh+QQJCgAAACwAAAAAEAAQAAADMgi63P7wCRHZnFVdmgHu2nFwlWCI3WGc3TSWhUFGxTAUkGCbtgENBMJAEJsxgMLWzpEAACH5BAkKAAAALAAAAAAQABAAAAMyCLrc/jDKSatlQtScKdceCAjDII7HcQ4EMTCpyrCuUBjCYRgHVtqlAiB1YhiCnlsRkAAAOwAAAAAAAAAAAA=="</code> <code>/&gt;</code></div><div><code>}</code></div><div><code>&lt;Link to=</code><code>"/register"</code> <code>className=</code><code>"btn btn-link"</code><code>&gt;Register&lt;/Link&gt;</code></div><div><code>&lt;/div&gt;</code></div><div><code>&lt;/form&gt;</code></div><div><code>&lt;/div&gt;</code></div><div><code>);</code></div><div><code>}</code></div><div><code>}</code></div><div><code>function</code> <code>mapStateToProps(state) {</code></div><div><code>const { loggingIn } = state.authentication;</code></div><div><code>return</code> <code>{</code></div><div><code>loggingIn</code></div><div><code>};</code></div><div><code>}</code></div><div><code>const connectedLoginPage = connect(mapStateToProps)(LoginPage);</code></div><div><code>export { connectedLoginPage as LoginPage };</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React + Redux Register Page Folder</h2>

<div><strong>Path: /src/RegisterPage</strong></div>

<p>The register page folder is for react components and other code that is used only by the register page component in the tutorial application.</p>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>React + Redux Register Page Component</h2>

<div><strong>Path: /src/RegisterPage/RegisterPage.jsx</strong></div>

<p>The register page component renders a simple registration form with fields for first name, last name, username and password. It displays validation messages for invalid fields when the user attempts to submit the form. If the form is valid, submitting it causes the <code>userActions.register(user)</code> redux action to be dispatched.</p>

<div><div id="highlighter_391086"><table><tbody><tr><td></td><td><div><div><code>import React from </code><code>'react'</code><code>;</code></div><div><code>import { Link } from </code><code>'react-router-dom'</code><code>;</code></div><div><code>import { connect } from </code><code>'react-redux'</code><code>;</code></div><div><code>import { userActions } from </code><code>'../_actions'</code><code>;</code></div><div><code>class RegisterPage extends React.Component {</code></div><div><code>constructor(props) {</code></div><div><code>super</code><code>(props);</code></div><div><code>this</code><code>.state = {</code></div><div><code>user: {</code></div><div><code>firstName: </code><code>''</code><code>,</code></div><div><code>lastName: </code><code>''</code><code>,</code></div><div><code>username: </code><code>''</code><code>,</code></div><div><code>password: </code><code>''</code></div><div><code>},</code></div><div><code>submitted: </code><code>false</code></div><div><code>};</code></div><div><code>this</code><code>.handleChange = </code><code>this</code><code>.handleChange.bind(</code><code>this</code><code>);</code></div><div><code>this</code><code>.handleSubmit = </code><code>this</code><code>.handleSubmit.bind(</code><code>this</code><code>);</code></div><div><code>}</code></div><div><code>handleChange(event) {</code></div><div><code>const { name, value } = event.target;</code></div><div><code>const { user } = </code><code>this</code><code>.state;</code></div><div><code>this</code><code>.setState({</code></div><div><code>user: {</code></div><div><code>...user,</code></div><div><code>[name]: value</code></div><div><code>}</code></div><div><code>});</code></div><div><code>}</code></div><div><code>handleSubmit(event) {</code></div><div><code>event.preventDefault();</code></div><div><code>this</code><code>.setState({ submitted: </code><code>true</code> <code>});</code></div><div><code>const { user } = </code><code>this</code><code>.state;</code></div><div><code>const { dispatch } = </code><code>this</code><code>.props;</code></div><div><code>if</code> <code>(user.firstName && user.lastName && user.username && user.password) {</code></div><div><code>dispatch(userActions.register(user));</code></div><div><code>}</code></div><div><code>}</code></div><div><code>render() {</code></div><div><code>const { registering  } = </code><code>this</code><code>.props;</code></div><div><code>const { user, submitted } = </code><code>this</code><code>.state;</code></div><div><code>return</code> <code>(</code></div><div><code>&lt;div className=</code><code>"col-md-6 col-md-offset-3"</code><code>&gt;</code></div><div><code>&lt;h2&gt;Register&lt;/h2&gt;</code></div><div><code>&lt;form name=</code><code>"form"</code> <code>onSubmit={</code><code>this</code><code>.handleSubmit}&gt;</code></div><div><code>&lt;div className={</code><code>'form-group'</code> <code>+ (submitted && !user.firstName ? </code><code>' has-error'</code> <code>: </code><code>''</code><code>)}&gt;</code></div><div><code>&lt;label htmlFor=</code><code>"firstName"</code><code>&gt;First Name&lt;/label&gt;</code></div><div><code>&lt;input type=</code><code>"text"</code> <code>className=</code><code>"form-control"</code> <code>name=</code><code>"firstName"</code> <code>value={user.firstName} onChange={</code><code>this</code><code>.handleChange} /&gt;</code></div><div><code>{submitted && !user.firstName &&</code></div><div><code>&lt;div className=</code><code>"help-block"</code><code>&gt;First Name is required&lt;/div&gt;</code></div><div><code>}</code></div><div><code>&lt;/div&gt;</code></div><div><code>&lt;div className={</code><code>'form-group'</code> <code>+ (submitted && !user.lastName ? </code><code>' has-error'</code> <code>: </code><code>''</code><code>)}&gt;</code></div><div><code>&lt;label htmlFor=</code><code>"lastName"</code><code>&gt;Last Name&lt;/label&gt;</code></div><div><code>&lt;input type=</code><code>"text"</code> <code>className=</code><code>"form-control"</code> <code>name=</code><code>"lastName"</code> <code>value={user.lastName} onChange={</code><code>this</code><code>.handleChange} /&gt;</code></div><div><code>{submitted && !user.lastName &&</code></div><div><code>&lt;div className=</code><code>"help-block"</code><code>&gt;Last Name is required&lt;/div&gt;</code></div><div><code>}</code></div><div><code>&lt;/div&gt;</code></div><div><code>&lt;div className={</code><code>'form-group'</code> <code>+ (submitted && !user.username ? </code><code>' has-error'</code> <code>: </code><code>''</code><code>)}&gt;</code></div><div><code>&lt;label htmlFor=</code><code>"username"</code><code>&gt;Username&lt;/label&gt;</code></div><div><code>&lt;input type=</code><code>"text"</code> <code>className=</code><code>"form-control"</code> <code>name=</code><code>"username"</code> <code>value={user.username} onChange={</code><code>this</code><code>.handleChange} /&gt;</code></div><div><code>{submitted && !user.username &&</code></div><div><code>&lt;div className=</code><code>"help-block"</code><code>&gt;Username is required&lt;/div&gt;</code></div><div><code>}</code></div><div><code>&lt;/div&gt;</code></div><div><code>&lt;div className={</code><code>'form-group'</code> <code>+ (submitted && !user.password ? </code><code>' has-error'</code> <code>: </code><code>''</code><code>)}&gt;</code></div><div><code>&lt;label htmlFor=</code><code>"password"</code><code>&gt;Password&lt;/label&gt;</code></div><div><code>&lt;input type=</code><code>"password"</code> <code>className=</code><code>"form-control"</code> <code>name=</code><code>"password"</code> <code>value={user.password} onChange={</code><code>this</code><code>.handleChange} /&gt;</code></div><div><code>{submitted && !user.password &&</code></div><div><code>&lt;div className=</code><code>"help-block"</code><code>&gt;Password is required&lt;/div&gt;</code></div><div><code>}</code></div><div><code>&lt;/div&gt;</code></div><div><code>&lt;div className=</code><code>"form-group"</code><code>&gt;</code></div><div><code>&lt;button className=</code><code>"btn btn-primary"</code><code>&gt;Register&lt;/button&gt;</code></div><div><code>{registering && </code></div><div><code>&lt;img src=</code><code>"data:image/gif;base64,R0lGODlhEAAQAPIAAP///wAAAMLCwkJCQgAAAGJiYoKCgpKSkiH/C05FVFNDQVBFMi4wAwEAAAAh/hpDcmVhdGVkIHdpdGggYWpheGxvYWQuaW5mbwAh+QQJCgAAACwAAAAAEAAQAAADMwi63P4wyklrE2MIOggZnAdOmGYJRbExwroUmcG2LmDEwnHQLVsYOd2mBzkYDAdKa+dIAAAh+QQJCgAAACwAAAAAEAAQAAADNAi63P5OjCEgG4QMu7DmikRxQlFUYDEZIGBMRVsaqHwctXXf7WEYB4Ag1xjihkMZsiUkKhIAIfkECQoAAAAsAAAAABAAEAAAAzYIujIjK8pByJDMlFYvBoVjHA70GU7xSUJhmKtwHPAKzLO9HMaoKwJZ7Rf8AYPDDzKpZBqfvwQAIfkECQoAAAAsAAAAABAAEAAAAzMIumIlK8oyhpHsnFZfhYumCYUhDAQxRIdhHBGqRoKw0R8DYlJd8z0fMDgsGo/IpHI5TAAAIfkECQoAAAAsAAAAABAAEAAAAzIIunInK0rnZBTwGPNMgQwmdsNgXGJUlIWEuR5oWUIpz8pAEAMe6TwfwyYsGo/IpFKSAAAh+QQJCgAAACwAAAAAEAAQAAADMwi6IMKQORfjdOe82p4wGccc4CEuQradylesojEMBgsUc2G7sDX3lQGBMLAJibufbSlKAAAh+QQJCgAAACwAAAAAEAAQAAADMgi63P7wCRHZnFVdmgHu2nFwlWCI3WGc3TSWhUFGxTAUkGCbtgENBMJAEJsxgMLWzpEAACH5BAkKAAAALAAAAAAQABAAAAMyCLrc/jDKSatlQtScKdceCAjDII7HcQ4EMTCpyrCuUBjCYRgHVtqlAiB1YhiCnlsRkAAAOwAAAAAAAAAAAA=="</code> <code>/&gt;</code></div><div><code>}</code></div><div><code>&lt;Link to=</code><code>"/login"</code> <code>className=</code><code>"btn btn-link"</code><code>&gt;Cancel&lt;/Link&gt;</code></div><div><code>&lt;/div&gt;</code></div><div><code>&lt;/form&gt;</code></div><div><code>&lt;/div&gt;</code></div><div><code>);</code></div><div><code>}</code></div><div><code>}</code></div><div><code>function</code> <code>mapStateToProps(state) {</code></div><div><code>const { registering } = state.registration;</code></div><div><code>return</code> <code>{</code></div><div><code>registering</code></div><div><code>};</code></div><div><code>}</code></div><div><code>const connectedRegisterPage = connect(mapStateToProps)(RegisterPage);</code></div><div><code>export { connectedRegisterPage as RegisterPage };</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Base Index HTML File</h2>

<div><strong>Path: /src/index.html</strong></div>

<p>The base index html file contains the outer html for the whole tutorial application. When the app is started with <code>npm start</code>, Webpack bundles up all of the react + redux code into a single javascript file and injects it into the body of the page.</p>

<div><div id="highlighter_714251"><table><tbody><tr><td></td><td><div><div><code>&lt;!DOCTYPE html&gt;</code></div><div><code>&lt;</code><code>html</code> <code>lang</code><code>=</code><code>"en"</code><code>&gt;</code></div><div><code>&lt;</code><code>head</code><code>&gt;</code></div><div><code>&lt;</code><code>meta</code> <code>charset</code><code>=</code><code>"UTF-8"</code><code>&gt;</code></div><div><code>&lt;</code><code>title</code><code>&gt;React + Redux - User Registration and Login Example & Tutorial&lt;/</code><code>title</code><code>&gt;</code></div><div><code>&lt;</code><code>link</code> <code>rel</code><code>=</code><code>"stylesheet"</code> <code>href</code><code>=</code><code>"<a href="https://netdna.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" target="_blank">https://netdna.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css</a>"</code> <code>/&gt;</code></div><div><code>&lt;</code><code>style</code><code>&gt;</code></div><div><code>a { cursor: pointer; }</code></div><div><code>.help-block { font-size: 12px; }</code></div><div><code>&lt;/</code><code>style</code><code>&gt;</code></div><div><code>&lt;/</code><code>head</code><code>&gt;</code></div><div><code>&lt;</code><code>body</code><code>&gt;</code></div><div><code>&lt;</code><code>div</code> <code>id</code><code>=</code><code>"app"</code><code>&gt;&lt;/</code><code>div</code><code>&gt;</code></div><div><code>&lt;/</code><code>body</code><code>&gt;</code></div><div><code>&lt;/</code><code>html</code><code>&gt;</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>



<h2>Main React Entry File</h2>

<div><strong>Path: /src/index.jsx</strong></div>

<p>The root index.jsx file bootstraps the react + redux tutorial application by rendering the <code>App</code> component (wrapped in a redux <code>Provider</code>) into the <code>app</code> div element defined in the base index html file above.</p>

<p>The boilerplate application uses a fake / mock backend that stores data in browser local storage, to switch to a real backend api simply remove the fake backend code below the comment <code>// setup fake backend</code>.</p>

<div><div id="highlighter_232374"><table><tbody><tr><td></td><td><div><div><code>import React from </code><code>'react'</code><code>;</code></div><div><code>import { render } from </code><code>'react-dom'</code><code>;</code></div><div><code>import { Provider } from </code><code>'react-redux'</code><code>;</code></div><div><code>import { store } from </code><code>'./_helpers'</code><code>;</code></div><div><code>import { App } from </code><code>'./App'</code><code>;</code></div><div><code>// setup fake backend</code></div><div><code>import { configureFakeBackend } from </code><code>'./_helpers'</code><code>;</code></div><div><code>configureFakeBackend();</code></div><div><code>render(</code></div><div><code>&lt;Provider store={store}&gt;</code></div><div><code>&lt;App /&gt;</code></div><div><code>&lt;/Provider&gt;,</code></div><div><code>document.getElementById(</code><code>'app'</code><code>)</code></div><div><code>);</code></div></div></td></tr></tbody></table></div></div>

<div><a href="#projectstructure" target="_blank">Back to top</a></div>

<h2>Web Development Sydney</h2>

<p>Feel free to <a href="/contact" target="_blank">drop me a line</a> if you're looking for a React or Redux web developer in Sydney Australia, I also provide remote contracting services for clients outside Sydney.</p>

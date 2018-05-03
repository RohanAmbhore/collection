<a href="https://stackoverflow.com/questions/35365595/store-credentials-in-redux-store-is-a-good-practice">https://stackoverflow.com/questions/35365595/store-credentials-in-redux-store-is-a-good-practice</a><div id="articleHeader"><h1>Store Credentials in Redux store is a good practice?</h1></div>

<p>I'm trying to develop a React/Redux application for learning purposes and I'm wondering if what I've done so far is a good practice or is not recommended.
The first thing that I had to deal with was handle the authorized requests.
I have a restfull api Rails back end. This server respond to the login request appending in the headers parameters such as access-token. 
This access-token is valid just for the next request, that in turn, return a new token valid for the next one and so on.</p>

<p>I implemented this flow in this way: 
The store dispatch the action that perform the login request passing username and password. Then when the response is ready I store the credentials in the redux store. 
When I need to perform an authorized request I set those parameters in the header request.
When I receive the response I update the credentials in the store with the new ones that I get from the response.</p>

<p>Here my code for more clearity:</p>

<pre><code>import { combineReducers } from 'redux'
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';

const initialState = {
  currentUser: {
    credentials: {},
    user: {}
  },
  test: {},
  users: []
}

export const SUBMIT_LOGIN = 'SUBMIT_LOGIN'
export const SET_USER = 'SET_USER'
export const TEST = 'TEST'
export const SET_USERS = 'SET_USERS'
export const SET_CREDENTIALS = 'SET_CREDENTIALS'

//actions
const submitLogin = () =&gt; (dispatch) =&gt; {
  return postLoginRequest()
    .then(response =&gt; {
      dispatch(setCredentials(
        response.headers.get('access-token'),
        response.headers.get('client'),
        response.headers.get('expiry'),
        response.headers.get('token-type'),
        response.headers.get('uid')
      ));
      return response
    })
    .then(response =&gt; {
      return response.json();
    })
    .then(
      (user) =&gt; dispatch(setUser(user.data)),
    );
}

const performRequest = (api) =&gt; (dispatch) =&gt; {
  return api()
    .then(response =&gt; {
      dispatch(setCredentials(
        response.headers.get('access-token'),
        response.headers.get('client'),
        response.headers.get('expiry'),
        response.headers.get('token-type'),
        response.headers.get('uid')
      ));
      return response
    })
    .then(response =&gt; {return response.json()})
    .then(json =&gt; {console.log(json)})
}

const setUsers = (users) =&gt; {
  return {
    type: SET_USERS,
    users
  }
}

const setUser = (user) =&gt; {
  return {
    type: SET_USER,
    user
  }
}

const setCredentials = (
  access_token,
  client,
  expiry,
  token_type,
  uid
) =&gt; {
  return {
    type: SET_CREDENTIALS,
    credentials: {
      'access-token': access_token,
      client,
      expiry,
      'token-type': token_type,
      uid
    }
  }
}

const currentUserInitialState = {
  credentials: {},
  user: {}
}

const currentUser = (state = currentUserInitialState, action) =&gt; {
  switch (action.type) {
    case SET_USER:
      return Object.assign({}, state, {user: action.user})
    case SET_CREDENTIALS:
      return Object.assign({}, state, {credentials: action.credentials})
    default:
      return state
  }
}

const rootReducer = combineReducers({
  currentUser,
  test
})

const getAuthorizedHeader = (store) =&gt; {
  const credentials = store.getState().currentUser.credentials
  const headers = new Headers(credentials)
  return headers
}

//store creation

const createStoreWithMiddleware = applyMiddleware(
  thunk
)(createStore);

const store = createStoreWithMiddleware(rootReducer);

const postLoginRequest = () =&gt; {
  return fetch('http://localhost:3000/auth/sign_in', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      email: 'test@test.com',
      password: 'password',
    })
  })
}

const getUsers = () =&gt; {
  const autorizedHeader = getAuthorizedHeader(store)
  debugger
  return fetch('http://localhost:3000/users',
    {
      method: 'GET',
      headers : autorizedHeader
    }
  )
}


store.dispatch(submitLogin())

setTimeout(() =&gt; {
  console.log(store.dispatch(performRequest(getUsers)))
}, 2000)
</code></pre>

<p>I'm wondering if store sensible data in the store in a good practice and if not I'm open to any suggestions to develop this workflow in a better way.</p>

<p>I have also this parameter on my server </p>

<pre><code>config.batch_request_buffer_throttle = 5.seconds
</code></pre>

<p>Sometimes it's necessary to make several requests to the API at the same time. In this case, each request in the batch will need to share the same auth token. This setting determines how far apart the requests can be while still using the same auth token.</p>

<p>In this way I could not dispatch the setCredentials action in my performRequest function if the token is still valid but I don't really have ideas how to check it.</p>

<p>Thanks</p>
    
<a href="https://github.com/jefflau/jest-fetch-mock">https://github.com/jefflau/jest-fetch-mock</a><div id="articleHeader"><h1>Jest Fetch Mock</h1></div>
<p>Fetch is the new way to do HTTP requests in the browser, and it can be used in other environments such as React Native. Jest Fetch Mock allows you to easily mock your <code>fetch</code> calls and return the response you need to fake the HTTP requests. It's easy to setup and you don't need a library like <code>nock</code> to get going and it uses Jest's built-in support for mocking under the surface. This means that any of the <code>jest.fn()</code> methods are also available. For more information on the jest mock API, check their docs <a href="https://facebook.github.io/jest/docs/en/mock-functions.html" target="_blank">here</a></p>
<p>It currently supports the mocking of the go-to isomorphic polyfill for fetch, <a href="https://github.com/matthew-andrews/isomorphic-fetch" target="_blank"><code>isomorphic-fetch</code></a>, so it supports Node.js and any browser-like runtime.</p>
<h2>Contents</h2>

<h2>Usage</h2>
<h3>Installation and Setup</h3>
<p>To setup your fetch mock you need to do the following things:</p>
<pre><code>$ npm install --save-dev jest-fetch-mock
</code></pre>
<p>Create a <code>setupJest</code> file to setup the mock or add this to an existing <code>setupFile</code>. :</p>
<div><pre>//setupJest.js or similar file
global.fetch = require('jest-fetch-mock')</pre></div>
<p>Add the setupFile to your jest config in <code>package.json</code>:</p>
<div><pre>"jest": {
  "automock": false,
  "setupFiles": [
    "./setupJest.js"
  ]
}</pre></div>
<h3>Using with Create-React-App</h3>
<p>If you are using <a href="https://github.com/facebookincubator/create-react-app" target="_blank">Create-React-App</a> (CRA), the code for <code>setupTest.js</code> above should be placed into <code>src/setupTests.js</code> in the root of your project. CRA automatically uses this filename by convention in the Jest configuration it generates. Similarly, changing to your <code>package.json</code> is not required as CRA handles this when generating your Jest configuration.</p>
<blockquote>
<p>Note: Keep in mind that if you decide to "eject" before creating src/setupTests.js, the resulting package.json file won't contain any reference to it, so you should manually create the property setupTestFrameworkScriptFile in the configuration for Jest, something like the <a href="https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#srcsetuptestsjs-1" target="_blank">following</a>:</p>
</blockquote>
<div><pre>"jest": {
  "setupTestFrameworkScriptFile": "&lt;rootDir&gt;/src/setupTests.js"
 }</pre></div>

<h3>Mock Responses</h3>
<ul>
<li><code>fetch.mockResponse(body, init): fetch</code> - Mock all fetch calls</li>
<li><code>fetch.mockResponseOnce(body, init): fetch</code> - Mock each fetch call independently</li>
<li><code>fetch.once(body, init): fetch</code> - Alias for mockResponseOnce</li>
<li><code>fetch.mockResponses(...responses): fetch</code> - Mock multiple fetch calls independently
<ul>
<li>Each argument is an array taking <code>[body, init]</code></li>
</ul>
</li>
<li><code>fetch.mockReject(error): fetch</code> - Mock all fetch calls, letting them fail directly</li>
<li><code>fetch.mockRejectOnce(error): fetch</code> - Let the next fetch call fail directly</li>
</ul>
<h3>Mock utilities</h3>
<ul>
<li><code>fetch.resetMocks()</code> - Clear previously set mocks so they do not bleed into other mocks</li>
<li><code>fetch.mock</code> - The mock state for your fetch calls. Make assertions on the arguments given to <code>fetch</code> when called by the functions you are testing. For more information check the <a href="https://facebook.github.io/jest/docs/en/mock-functions.html#mock-property" target="_blank">Jest docs</a></li>
</ul>
<p>For information on the arguments body and init can take, you can look at the MDN docs on the Response Constructor function, which <code>jest-fetch-mock</code> uses under the surface.</p>
<p><a href="https://developer.mozilla.org/en-US/docs/Web/API/Response/Response" target="_blank">https://developer.mozilla.org/en-US/docs/Web/API/Response/Response</a></p>
<p>Each mocked response or err
or will return a <a href="http://facebook.github.io/jest/docs/mock-function-api.html#content" target="_blank">Mock Function</a>. You can use methods like <code>.toHaveBeenCalledWith</code> to ensure that the mock function was called with specific arguments. For more methods detail, take a look at <a href="http://facebook.github.io/jest/docs/expect.html#content" target="_blank">this</a>.</p>
<h2>Examples</h2>
<p>In most of the complicated examples below, I am testing my action creators in Redux, but it doesn't have to be used with Redux.</p>
<h3>Simple mock and assert</h3>
<p>In this simple example I won't be using any libraries. It is a simple fetch request, in this case to google.com. First we setup the <code>beforeEach</code> callback to reset our mocks. This isn't strictly necessary in this example, but since we will probably be mocking fetch more than once, we need to reset it across our tests to assert on the arguments given to fetch.</p>
<p>Once we've done that we can start to mock our response. We want to give it an objectwith a <code>data</code> property and a string value of <code>12345</code> and wrap it in <code>JSON.stringify</code> to JSONify it. Here we use <code>mockResponseOnce</code>, but we could also use <code>once</code>, which is an alias.</p>
<p>We then call the function that we want to test with the arguments we want to test with. In the <code>then</code> callback we assert we have got the correct data back.</p>
<p>Finally we can assert on the <code>.mock</code> state that Jest provides for us to test what arguments were given to fetch and how many times it was called</p>
<div><pre>//api.js
export function APIRequest(who) {
  if (who === 'google') {
    return fetch('https://google.com').then(res =&gt; res.json())
  } else {
    return 'no argument provided'
  }
}</pre></div>
<div><pre>//api.test.js
import { APIRequest } from './api'

describe('testing api', () =&gt; {
  beforeEach(() =&gt; {
    fetch.resetMocks()
  })

  it('calls google and returns data to me', () =&gt; {
    fetch.mockResponseOnce(JSON.stringify({ data: '12345' }))

    //assert on the response
    APIRequest2('google').then(res =&gt; {
      expect(res.data).toEqual('12345')
    })

    //assert on the times called and arguments given to fetch
    expect(fetch.mock.calls.length).toEqual(1)
    expect(fetch.mock.calls[0][0]).toEqual('https://google.com')
  })
})</pre></div>
<h3>Mocking all fetches</h3>
<p>In this example I am mocking just one fetch call. Any additional fetch calls in the same function will also have the same mock response. For more complicated functions with multiple fetch calls, you can check out example 3.</p>
<div><pre>import configureMockStore from 'redux-mock-store' // mock store
import thunk from 'redux-thunk'

const middlewares = [thunk]
const mockStore = configureMockStore(middlewares)

import { getAccessToken } from './accessToken'

describe('Access token action creators', () =&gt; {
  it('dispatches the correct actions on successful fetch request', () =&gt; {
    fetch.mockResponse(JSON.stringify({ access_token: '12345' }))

    const expectedActions = [
      { type: 'SET_ACCESS_TOKEN', token: { access_token: '12345' } }
    ]
    const store = mockStore({ config: { token: '' } })

    return (
      store
        .dispatch(getAccessToken())
        //getAccessToken contains the fetch call
        .then(() =&gt; {
          // return of async actions
          expect(store.getActions()).toEqual(expectedActions)
        })
    )
  })
})</pre></div>
<h3>Mocking a failed fetch</h3>
<p>In this example I am mocking just one fetch call but this time using the <code>mockReject</code> function to simulate a failed request. Any additional fetch calls in the same function will also have the same mock response. For more complicated functions with multiple fetch calls, you can check out example 3.</p>
<div><pre>import configureMockStore from 'redux-mock-store' // mock store
import thunk from 'redux-thunk'

const middlewares = [thunk]
const mockStore = configureMockStore(middlewares)

import { getAccessToken } from './accessToken'

describe('Access token action creators', () =&gt; {
  it('dispatches the correct actions on a failed fetch request', () =&gt; {
    fetch.mockReject(new Error('fake error message'))

    const expectedActions = [
      { type: 'SET_ACCESS_TOKEN_FAILED', error: { status: 503 } }
    ]
    const store = mockStore({ config: { token: '' } })

    return (
      store
        .dispatch(getAccessToken())
        //getAccessToken contains the fetch call
        .then(() =&gt; {
          // return of async actions
          expect(store.getActions()).toEqual(expectedActions)
        })
    )
  })
})</pre></div>
<h3>Mocking multiple fetches with different responses</h3>
<p>In this next example, the store does not yet have a token, so we make a request to get an access token first. This means that we need to mock two different responses, one for each of the fetches. Here we can use <code>fetch.mockResponseOnce</code> or <code>fetch.once</code> to mock the response only once and call it twice. Because we return the mocked function, we can chain this jQuery style. It internally uses Jest's <code>mockImplementationOnce</code>. You can read more about it on the <a href="https://facebook.github.io/jest/docs/mock-functions.html#content" target="_blank">Jest documentation</a></p>
<div><pre>import configureMockStore from 'redux-mock-store'
import thunk from 'redux-thunk'

const middlewares = [thunk]
const mockStore = configureMockStore(middlewares)

import { getAnimeDetails } from './animeDetails'

describe('Anime details action creators', () =&gt; {
  it('dispatches requests for an access token before requesting for animeDetails', () =&gt; {
    fetch
      .once(JSON.stringify({ access_token: '12345' }))
      .once(JSON.stringify({ name: 'naruto' }))

    //once is an alias for .mockResponseOnce
    //

    const expectedActions = [
      { type: 'SET_ACCESS_TOKEN', token: { access_token: '12345' } },
      { type: 'SET_ANIME_DETAILS', animeDetails: { name: 'naruto' } }
    ]
    const store = mockStore({ config: { token: null } })

    return (
      store
        .dispatch(getAnimeDetails('21049'))
        //getAnimeDetails contains the 2 fetch calls
        .then(() =&gt; {
          // return of async actions
          expect(store.getActions()).toEqual(expectedActions)
        })
    )
  })
})</pre></div>
<h3>Mocking multiple fetches with <code>fetch.mockResponses</code></h3>
<p><code>fetch.mockResponses</code> takes as many arguments as you give it, all of which are arrays representing each Response Object. It will then call the <code>mockImplementationOnce</code> for each response object you give it. This reduces the amount of boilerplate code you need to write. An alternative is to use <code>.once</code> and chain it multiple times if you don't like wrapping each response arguments in a tuple/array.</p>
<p>In this example our actionCreator calls <code>fetch</code> 4 times, once for each season of the year and then concatenates the results into one final array. You'd have to write <code>fetch.mockResponseOnce</code> 4 times to achieve the same thing:</p>
<div><pre>describe('getYear action creator', () =&gt; {
  it('dispatches the correct actions on successful getSeason fetch request', () =&gt; {
    fetch.mockResponses(
      [
        JSON.stringify([{ name: 'naruto', average_score: 79 }]),
        { status: 200 }
      ],
      [
        JSON.stringify([{ name: 'bleach', average_score: 68 }]),
        { status: 200 }
      ],
      [
        JSON.stringify([{ name: 'one piece', average_score: 80 }]),
        { status: 200 }
      ],
      [
        JSON.stringify([{ name: 'shingeki', average_score: 91 }]),
        { status: 200 }
      ]
    )

    const expectedActions = [
      {
        type: 'FETCH_ANIMELIST_REQUEST'
      },
      {
        type: 'SET_YEAR',
        payload: {
          animes: [
            { name: 'naruto', average_score: 7.9 },
            { name: 'bleach', average_score: 6.8 },
            { name: 'one piece', average_score: 8 },
            { name: 'shingeki', average_score: 9.1 }
          ],
          year: 2016
        }
      },
      {
        type: 'FETCH_ANIMELIST_COMPLETE'
      }
    ]
    const store = mockStore({
      config: {
        token: { access_token: 'wtw45CmyEuh4P621IDVxWkgVr5QwTg3wXEc4Z7Cv' }
      },
      years: []
    })

    return (
      store
        .dispatch(getYear(2016))
        //This calls fetch 4 times, once for each season
        .then(() =&gt; {
          // return of async actions
          expect(store.getActions()).toEqual(expectedActions)
        })
    )
  })
})</pre></div>
<h3>Reset mocks between tests with <code>fetch.resetMocks</code></h3>
<p><code>fetch.resetMocks</code> resets the <code>fetch</code> mock to give fresh mock data in between tests. It only resets the <code>fetch</code> calls as to not disturb any other mocked functionality.</p>
<div><pre>describe('getYear action creator', () =&gt; {
  beforeEach(() =&gt; {
      fetch.resetMocks();
  });
  it('dispatches the correct actions on successful getSeason fetch request', () =&gt; {

    fetch.mockResponses(
      [
        JSON.stringify([ {name: 'naruto', average_score: 79} ]), { status: 200}
      ],
      [
        JSON.stringify([ {name: 'bleach', average_score: 68} ]), { status: 200}
      ]
    )

    const expectedActions = [
      {
        type: 'FETCH_ANIMELIST_REQUEST'
      },
      {
        type: 'SET_YEAR',
        payload: {
          animes: [
            {name: 'naruto', average_score: 7.9},
            {name: 'bleach', average_score: 6.8}
          ],
          year: 2016,
        }
      },
      {
        type: 'FETCH_ANIMELIST_COMPLETE'
      }
    ]
    const store = mockStore({
      config: { token: { access_token: 'wtw45CmyEuh4P621IDVxWkgVr5QwTg3wXEc4Z7Cv' }},
      years: []
    })

    return store.dispatch(getYear(2016))
      //This calls fetch 2 times, once for each season
      .then(() =&gt; { // return of async actions
        expect(store.getActions()).toEqual(expectedActions)
      })
  });
  it('dispatches the correct actions on successful getSeason fetch request', () =&gt; {

    fetch.mockResponses(
      [
        JSON.stringify([ {name: 'bleach', average_score: 68} ]), { status: 200}
      ],
      [
        JSON.stringify([ {name: 'one piece', average_score: 80} ]), { status: 200}
      ],
      [
        JSON.stringify([ {name: 'shingeki', average_score: 91} ]), { status: 200}
      ]
    )

    const expectedActions = [
      {
        type: 'FETCH_ANIMELIST_REQUEST'
      },
      {
        type: 'SET_YEAR',
        payload: {
          animes: [
            {name: 'bleach', average_score: 6.8},
            {name: 'one piece', average_score: 8},
            {name: 'shingeki', average_score: 9.1}
          ],
          year: 2016,
        }
      },
      {
        type: 'FETCH_ANIMELIST_COMPLETE'
      }
    ]
    const store = mockStore({
      config: { token: { access_token: 'wtw45CmyEuh4P621IDVxWkgVr5QwTg3wXEc4Z7Cv' }},
      years: []
    })

    return store.dispatch(getYear(2016))
      //This calls fetch 3 times, once for each season
      .then(() =&gt; { // return of async actions
        expect(store.getActions()).toEqual(expectedActions)
      })
      ,

  })
})</pre></div>
<h3>Using <code>fetch.mock</code> to inspect the mock state of each fetch call</h3>
<p><code>fetch.mock</code> by default uses <a href="https://facebook.github.io/jest/docs/en/mock-functions.html#mock-property" target="_blank">Jest's mocking functions</a>. Therefore you can make assertions on the mock state. In this example we have an arbitrary function that makes a different fetch request based on the argument you pass to it. In our test, we run Jest's <code>beforeEach()</code> and make sure to reset our mock before each <code>it()</code> block as we will make assertions on the arguments we are passing to <code>fetch()</code>. The most uses property is the <code>fetch.mock.calls</code> array. It can give you information on each call, and their arguments which you can use for your <code>expect()</code> calls. Jest also comes with some nice aliases for the most used ones.</p>
<div><pre>// api.js

import 'isomorphic-fetch'

export function APIRequest(who) {
  if (who === 'facebook') {
    return fetch('https://facebook.com')
  } else if (who === 'twitter') {
    return fetch('https://twitter.com')
  } else {
    return fetch('https://google.com')
  }
}</pre></div>
<div><pre>// api.test.js
import { APIRequest } from './api'

describe('testing api', () =&gt; {
  beforeEach(() =&gt; {
    fetch.resetMocks()
  })

  it('calls google by default', () =&gt; {
    fetch.mockResponse(JSON.stringify({ secret_data: '12345' }))
    APIRequest()

    expect(fetch.mock.calls.length).toEqual(1)
    expect(fetch.mock.calls[0][0]).toEqual('https://google.com')
  })

  it('calls facebook', () =&gt; {
    fetch.mockResponse(JSON.stringify({ secret_data: '12345' }))
    APIRequest('facebook')

    expect(fetch.mock.calls.length).toEqual(2)
    expect(fetch.mock.calls[0][0]).toEqual(
      'https://facebook.com/someOtherResource'
    )
    expect(fetch.mock.calls[1][0]).toEqual('https://facebook.com')
  })

  it('calls twitter', () =&gt; {
    fetch.mockResponse(JSON.stringify({ secret_data: '12345' }))
    APIRequest('twitter')

    expect(fetch).toBeCalled() // alias for expect(fetch.mock.calls.length).toEqual(1);
    expect(fetch).toBeCalledWith('https://twitter.com') // alias for expect(fetch.mock.calls[0][0]).toEqual();
  })
})</pre></div>

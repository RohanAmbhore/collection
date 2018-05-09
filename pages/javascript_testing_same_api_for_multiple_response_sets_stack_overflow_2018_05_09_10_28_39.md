<a href="https://stackoverflow.com/questions/44331178/testing-same-api-for-multiple-response-sets?rq=1">https://stackoverflow.com/questions/44331178/testing-same-api-for-multiple-response-sets?rq=1</a><div id="articleHeader"><h1>Testing same API for multiple response sets</h1></div>

<p>We've been trying to test an API exposed from a microservice (say GET /contacts) which is being consumed by another microservice.</p>

<p>In order to avoid integration tests, we created consumer-driven contract tests where the consumer microservice created pacts and published them to a broker from where the producer would verify the pact separately.</p>

<p>We've used <a href="https://docs.pact.io/" title="Pact IO" target="_blank">Pact IO</a> to achieve this and it has been quite good so far.</p>

<p>Now we are facing issues when trying to do exhaustive tests where we would want to see how an empty list is returned from GET /contacts.</p>

<p>The problem is: while adding interactions, we could use Provider States but we couldn't find a way to differentiate between writing tests for getting a list of contacts from GET /contacts once and getting an empty list in another test.</p>

<p>This is how we create pact tests in our consumer microservice:</p>

<pre><code>mockServer.start()
        .then(() =&gt; {
          provider = pact({
            // config
          })
          return provider.addInteraction({
            state: 'Get all contacts',
            uponReceiving: 'Get all contacts',
            withRequest: {
              method: 'GET',
              path: '/contacts',
              headers: {
                Accept: 'application/json; charset=utf-8'
              }
            },
            willRespondWith: {
              status: 200,
              body: //list of all contacts
            }
          })
        .then(() =&gt; {
          return provider.addInteraction({
            state: 'Get empty list of contacts',
            uponReceiving: 'Get empty list of contacts',
            withRequest: {
              method: 'GET',
              path: '/contacts',
              headers: {
                Accept: 'application/json; charset=utf-8'
              }
            },
            willRespondWith: {
              status: 200,
              body: [] // empty list
            }
          })
        })</code></pre>

<p>We cannot find a way to differentiate between these interations in our tests! :(</p>

<p>Any help would be appreciated!</p>

<p>Thanks.</p>
    
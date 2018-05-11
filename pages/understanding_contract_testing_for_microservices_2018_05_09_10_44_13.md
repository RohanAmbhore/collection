<a href="https://www.mabl.com/blog/understanding-contract-testing-microservices-mabl">https://www.mabl.com/blog/understanding-contract-testing-microservices-mabl</a><div id="articleHeader"><h1>Understanding Contract Testing for Microservices</h1></div>
                
                    <p><a href="http://microservices.io/patterns/microservices.html" target="_blank">Microservices</a> are becoming increasingly popular on the landscape of Service Oriented Architecture. More companies are becoming enamored with them and with good reason. Microservices provide a degree of granularity and flexibility that allows modern developers to adapt to the ever increasing demands of the marketplace. Microservices are discrete and when your <a href="https://www.mabl.com/blog/what-is-cicd" target="_blank">CI/CD</a> process is adjusted to accommodate the small size of microservices, you’ll find them very suited for scaling. Also, smaller development teams are needed to create, deploy and support them. It’s easier for a new developer to become productive on a microservice as opposed to a full blown, monolithic application.</p>

<p>There’s a lot to be said for using microservices provided you have a testing policy and procedures in place that ensures that the quality of the given microservice. A microservice that is not well tested is an accident waiting to happen. You just can’t put a bunch of of URLs out on the Internet and hope for the best. Believe me, most times anything that can go wrong will go wrong. But, I suspect I preach to the choir.</p>
<p>The people that know a thing or two about large scale system testing advocate using a variety of strategies to ensure that your microservices works as you intend them to. No argument here. I am a big supporter of comprehensive testing, all the way from automated unit testing to the higher level, human based, <a href="//cdn2.hubspot.net/hubfs/3937956/Mabl%20November2017/Pdf/QAIExploring.pdf?t=1525833326171" target="_blank">exploratory testing</a>.</p>
<h1>What is Contract Testing?</h1>
<p>One strategy that I find particularly useful for testing microservices is Contract Testing. Contract Testing has become quite mature and is covered extensively in the book, <a href="http://www.growing-object-oriented-software.com/" target="_blank">Growing Object-Oriented Software, Guided by Tests</a>. But the short version is this: Contract Testing is writing tests to ensure that the explicit and implicit contract of a microservice works as advertised.</p>
<p>There are two perspectives when it comes to Contract Tests, consumer and provider. As you might suspect, the consumer perspective is that of an entity using the microservice. The provider perspective is that of the entity providing the service. These perspectives have been in cultural conflict since the first punch card rolled through an <a href="https://en.wikipedia.org/wiki/IBM_700/7000_series#Scientific_Architecture_.28704.2F709.2F7090.2F7094.29" target="_blank">IBM 700</a>. It’s the difference between, “your service isn’t working the way that the spec said it would” (consumer) and “The service is working according to spec, RTFM” (provider). Thus, you can infer that it all comes down to the spec, in other words, the contract.</p>
<h1>Making the Contract Known</h1>
<p>Before any testing can take place, consumer or producer, a contract must be available to all parties. The more common way that a microservice’s contract is known is by way of the API documentation. Please know there are some more advanced API publishers that have embraced the self-discovery and <a href="https://sites.google.com/site/restframework/hypermedia-controls" target="_blank">hypermedia control</a> aspects of <a href="https://www.martinfowler.com/articles/richardsonMaturityModel.html#level3" target="_blank"> Richardson Maturity Model (RMM) Level 3</a>and thus can expose contract declaration via endpoint responses, whether real or mocked. But, for most of us grunting it out making APIs at <a href="https://www.martinfowler.com/articles/richardsonMaturityModel.html#level2" target="_blank">RMM, Level 2</a>, on the order of Etsy, NYTimes, Twitter and Shopify, the documentation is all we have.</p>
<p>Microservices need to be documented to a fine degree of detail so it’s very clear to the consumer as well as the team testing the structure and use of the endpoint. For example, when specifying the input and output for a POST method on a given endpoint, just declaring the input/output data as object is going to create work down the line. Test designers will have to guess about the structures to create to test your microservice’s API. Rather, you will do well to specify each attribute of the request and response objects, as well as the datatype of the given attribute therein.</p>
<p>When it comes to creating the documentation, life will be a lot easier when you use a standard API specification format. There are many tools out there that will automatically generate documentation when an API is defined against a known standard such as <a href="http://raml.org/developers/document-your-api" target="_blank">RAML</a>, <a href="http://swagger.io/specification/" target="_blank">OpenAPI</a> (neé Swagger by <a href="https://twitter.com/fehguy?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor" target="_blank">Tony Tam</a>) or <a href="https://apiary.io/" target="_blank">API Blueprint</a>.</p>
<p>You will find these tools helpful, no doubt. But the documentation produced will only be as good as the specification you create. If the specification lacks granularity in terms of well-defined request and response objects, you’ll find consumers submitting anything under the sun and then getting upset when the microservice’s API responds with the typically vague <a href="https://httpstatuses.com/400" target="_blank">400</a> error code. So again, put as much meaningful detail into your specification as you can.</p>
<h1>So What Do We Test and When?</h1>
<p>First let’s start with what not to test. The focus of a contract test is to make sure that things work as advertised in terms of the agreement. Typically, agreements are confined to the API specification presented by the microservice. Thus, do not plan to test service availability, load tolerance or deployment integrity. All we care about is testing against the contract. So far, so good. But, before I go on, let me admit two things.</p>
<p>First, my perspective is that of a microservice provider.  It’s rare for me to release the microservice specification independent of the microservice itself. I am a big proponent of <a href="http://www.codeguru.com/cpp/frameworks/the-value-of-specification-first-development-using-swagger.html" target="_blank">Specification First</a>, using a standard API specification format when I design an API. (in my case Swagger/OpenAPI.) I can definitely imagine larger enterprises that have many teams working in parallel needing to have a specification in hand before any provider code is delivered. But, my experience is more limited to delivering code along with the documentation.</p>
<p>Since I am taking the perspective of a provider, please know I test directly against an active endpoint, usually in Development or QA environments. When in DEV, I might mock an internal collaborator component or service within the service. But, the entry point of my testing will always be against an active METHOD/URL using HTTP.</p>
<p>Second, when it comes to test sensibilities, I have a bias to testing in terms of state as described by the Classic School of TDD. What is the Classic School of TDD approach? Imagine you have an endpoint api/customers/ that takes firstname, lastname and email as body parameters on a <a href="https://en.wikipedia.org/wiki/POST_(HTTP)" target="_blank">POST</a>. When you POST the data, you expect back an id that references an unique identifier for the resource item. Thus, taking the Classic approach, I send in the data and get back the id. If I want to know that the data stuck, I make a subsequent call, <a href="https://www.w3schools.com/tags/ref_httpmethods.asp" target="_blank">GET</a>  to api/customers/{id}. Still, all I care about is what I put in is good and what I get back is expected. Thus, I test the changing state of the microservice using a sequence of calls to various resource endpoints.</p>
<p>There is another school, the <a href="http://codemanship.co.uk/parlezuml/blog/?postid=987" target="_blank">London School of TDD</a> that promotes testing the entire behavior of the microservice contract including all collaborator components and services behind the endpoint. Internal components and services must be exercised and verified in terms of roles, responsibilities and interactions. Granted, the London School is much more comprehensive. Given that I think you can never have too much testing, the London School approach has very little downside provided the team has the appetite and the required staffing, time and expertise required for the London School approach.</p>
<p>Because I am taking the perspective of a provider in the Classic School, I am going write tests that confirm both the happy and unhappy paths for all the given endpoints and associated HTTP methods defined for the microservice. I will set up tests, execute, assert against the response and then teardown. When the documentation implies a sequence, for example, POSTing customer data the returns a customer_id that will allow me to GET the customer information later on, I will perform that sequence along the happy path. Also, I will test using a bogus customer_id to meet the unhappy path testing requirement. Granted, unhappy path testing can become a quest requiring infinite labor in order to imagine and test everything that can go wrong.</p>
<p>The shops I’ve worked in have adopted DevOps principles and thus have time constraints. It rare to have unlimited time to test.</p>
<h3><strong><em>I am pragmatic. I think that essential testing must be done. I think that all code written must be designed to be testable.  I think that any test written needs to pass. Also, I think that at some point in the entire testing process, there must be a set of passing tests that can prove that code, particularly functional code, has been adequately covered.</em></strong></h3>
<p>Thus, at the least, you should test using ranges of values against a given attribute value. Also test beyond the supported ranges of value and expected data types.  I am a big supporter of adding tests, happy and unhappy path during each development iteration. Also, I am a big believer in using tools when possible.</p>
<h1>Tools</h1>
<p>One the benefits of using a standard specification such as RAML, Swagger/OpenAPI or API Blueprint when designing an API for a microservice is that a lot has been done to create tools that will do test autogeneration against specification. For example, you use Vigia to create tests against a RAML specification.  If your spec is written in Swagger/OpenAPI, you can autogen tests using <a href="https://www.npmjs.com/package/swagger-test-templates" target="_blank">Swagger Test Templates</a>. For API Blueprint there’s <a href="https://github.com/apiaryio/dredd" target="_blank">Dredd</a>.</p>
<p>Having said this, when you find yourself in a position where you cannot use automated test generation to create tests, you can use any test environment that supports HTTP calls. Examples are <a href="http://mherman.org/blog/2015/09/10/testing-node-js-with-mocha-and-chai/#.WVFlCBPytTY" target="_blank">mocha/cha</a>i running <a href="https://www.npmjs.com/package/supertest" target="_blank">supertest</a> in a NodeJs environment, <a href="https://www.soapui.org/tutorials/rest-sample-project.html" target="_blank">SoapUI</a> which offers support for defining tests graphically, or the good old standby, <a href="http://www.testautomationguru.com/how-to-test-rest-api-using-jmeter/" target="_blank">JMeter</a>. You can run Mocha/Chai, <a href="https://www.blazemeter.com/blog/5-ways-launch-jmeter-test-without-using-jmeter-gui" target="_blank">SoapUI</a> and <a href="https://www.blazemeter.com/blog/5-ways-launch-jmeter-test-without-using-jmeter-gui" target="_blank">JMeter</a> all from the command line, which makes for seamless integration into your CI/CD process.</p>
<table>
<tbody>
<tr>
<td>
<h2><strong>Consumer Contract Testing Using Pact</strong></h2>
<p><a href="https://github.com/realestate-com-au/pact" target="_blank">Pact</a> is an excellent tool to use to do Contract Testing from a consumer’s perspective. Pact allows consumers to create, execute and evaluate tests against a “pact”, the contract, if you will. The provider is represented as a set of mock services. Then, later on in the Software Test Lifecycle that pact is executed against the provider to ensure that the contract is accurately in force.</p>
<p>Pact is one of the more popular tools for Contract Testing and it’s a good way to start writing consumer code while the provider behavior is underway in parallel.</p>
</td>
</tr>
</tbody>
</table>
<h1>When to Test</h1>
<p>Tests take time to run, even for microservices. Microservices that have one or two endpoints, with minimal response and request objects will not take as long as tests for services that support very complex data structures. Also, network latency will always contribute for the time it takes for a set of tests to run.</p>
<p>If you have a small microservice that supports limited data structures, running the contract tests associated with the service each time you deploy the microservice should not cause a great burden on your Continuous Integration/Continuous Deployment (CI/CD) pipeline. For microservices that support substantial data structures and do a lot of heavy lifting in terms of computing, <a href="https://devops.com/continuous-testing-devops-bottleneck/" target="_blank">bottlenecks can occur</a>.</p>
<table>
<tbody>
<tr>
<td>
<h2><strong>Using VCR to Avoid Bottlenecks</strong></h2>
<p>One interesting tool written in Ruby is <a href="https://github.com/vcr/vcr" target="_blank">VCR</a>. VCR will record an HTTP test and its result upon first execution of the test. Then, upon subsequent runs of the given test, execution will happen in a “disconnected” manner, without using HTTP. Thus, the tests will run faster because the trips via HTTP will have been avoided. Yet, your tests will still have the benefit of being subject to verification according to the test’s result.</p>
</td>
</tr>
</tbody>
</table>
<p>I am a pessimistic developer. I believe that anything that can go wrong, will go wrong. Thus, from a provider’s perspective, I advocate always running Contract Tests on each deployment. I’d rather slow down the assembly line to ensure that all products rolling off the end are of the highest quality.</p>
<p>Typically source control environment such as GitHub allow you to discover when the spec has changed, provided you are using a standard specification technology such as RAML, Swagger/OpenAPI or API Blueprint. Thus, your automated CI/CD process will be tipped off when it’s time to run the Contract Tests. If you are rolling-your-own in terms of specification definition, make sure you build in a way into your homegrown technique to detect API changes from source code.</p>
<h1>Putting It All Together</h1>
<p>As mentioned at the beginning of this piece, Contract Testing is but one of the many strategies that need to be incorporated into a comprehensive release process. Performing Contract Tests in combination with other test strategies such as automated unit testing, integration testing and load testing combined with manual, human based exploratory testing will provide the overall quality assurance process you need to make the applications and services your business provides reliable and desirable. Some of you might adhere to the Classic School of TDD, others to the London School. The important thing to remember is that Contract Testing counts. In the world of architectures that use microservices, the contract is the foundation upon which overall system integrity stands. Getting it right matters.</p>
                
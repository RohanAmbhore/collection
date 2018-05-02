<a href="https://jrsinclair.com/articles/2016/gentle-introduction-to-javascript-tdd-ajax/">https://jrsinclair.com/articles/2016/gentle-introduction-to-javascript-tdd-ajax/</a><div id="articleHeader"><h1>A Gentle Introduction to Javascript Test Driven Development: Part 2</h1></div>
          <p>
          Written by James Sinclair
          on the <time>17<sup>th</sup> April 2016</time>
          </p>
        </header>
        
          <p>This is part two of a three-part series introducing my personal approach to JavaScript TDD. In the last article we began creating a small application that loads image data from the Flickr API and displays it in a web page. We began by setting up modules and writing simple unit tests using the Mocha framework. In this article we’ll look at how to test asynchronous network calls (also known as AJAX).</p>



<h2 id="testingasynchronousnetworkajaxcalls">Testing asynchronous network (AJAX) calls</h2>

<p>In the last article I joked that I was procrastinating about testing the code where we call the Flickr API. And not without reason. I was procrastinating because testing network calls is a little bit complicated. There are three things that make this tricky:</p>

<ol>
<li>Testing an API call needs access to the network, which I can’t always guarantee;</li>
<li>Network calls in JavaScript are asynchronous. This means that when we make a network request we interrupt the normal code flow; and</li>
<li>The results from the network call change often. This is the whole point of the network call—but it makes it somewhat difficult to test.</li>
</ol>

<p>I <em>could</em> go ahead and just write a test that makes the network call and checks what comes back, but this would have a some drawbacks:</p>

<ul>
<li>The data coming back from the live Flickr API changes all the time. Unless I’m careful about how I write my tests, they would pass for maybe a minute before new data broke my test.</li>
<li>Making network calls can be slow, and the slower my tests, the less fun TDD becomes.</li>
<li>Doing things this way needs an internet connection. I regularly find myself writing code on a bus, or a train, or some other location without (fast) access to the internet.</li>
</ul>

<p>So, I need to think carefully here about what I want to test. I will create a method called <code>fetchFlickrData()</code> that grabs data from the Flickr API. For this to work, I need to make a network call. But to make a network call, I will be calling some sort of API. The simplest API for this purpose would jQuery’s <code>getJSON()</code> method. <code>getJSON()</code> takes a URL and returns a Promise for the JSON data. If you’re not familiar with Promises, it’s worth taking a moment to get the basic idea.<a href="#fn:1" title="see footnote" id="fnref:1" target="_blank"><sup>1</sup></a></p>

<p>Now, to handle this neatly, I need to think like a functional programmer. Network calls involve side effects, making my function impure. But, if I can isolate the impure part (i.e. <code>getJSON()</code>), then I have a pure, <em>testable</em> function. In other words, what if I made <code>getJSON()</code> a parameter that I passed into my function? The signature might look something like this: </p>

<pre><code>fetchFlickrData: function(apiKey, fetch) { 
    // Code goes in here
}
</code></pre>

<p>In the application code, I would pass <code>$.getJSON</code> as the <code>fetch</code> parameter (more on that later). In my <em>test</em> though, I can pass a <em>fake</em> <code>getJSON()</code> method that always returns a promise for the same data. Then I can check that my function returns exactly what I expect, without making a network call.</p>

<p>The other thing that is tricky about network calls with JavaScript is that they are <em>asyncrhonous</em>. This means that we need some way of telling our test runner (Mocha) to wait until all the tests finish. Mocha provides a parameter to the <code>it()</code> callback called <code>done</code> that allows us to tell Mocha when the test is complete.</p>

<p>Putting all this together, I can write my test like so:</p>

<pre><code>// flickr-fetcher-spec.js
describe('#fetchFlickrData()', function() {
    it(
        'should take an API key and fetcher function argument and return a promise for JSON data.',
        function(done) {
            var apiKey      = 'does not matter much what this is right now',
                fakeData    = {
                    'photos': {
                        'page':    1,
                        'pages':   2872,
                        'perpage': 100,
                        'total':   '287170',
                        'photo':   [{
                            'id':       '24770505034',
                            'owner':    '97248275@N03',
                            'secret':   '31a9986429',
                            'server':   '1577',
                            'farm':     2,
                            'title':    '20160229090898',
                            'ispublic': 1,
                            'isfriend': 0,
                            'isfamily': 0
                        }, {
                            'id':       '24770504484',
                            'owner':    '97248275@N03',
                            'secret':   '69dd90d5dd',
                            'server':   '1451',
                            'farm':     2,
                            'title':    '20160229090903',
                            'ispublic': 1,
                            'isfriend': 0,
                            'isfamily': 0
                        }]
                    }
                },
                fakeFetcher = function(url) {
                    var expectedURL = 'https://api.flickr.com/services/rest/?method=flickr.photos.search&api_key='
                                + apiKey + '&text=pugs&format=json&nojsoncallback=1'
                    expect(url).to.equal(expectedURL)
                    return Promise.resolve(fakeData);
                };
            FlickrFetcher.fetchFlickrData(apiKey, fakeFetcher).then(function(actual) {
                expect(actual).to.eql(fakeData);
                done();
            }
        );

    });
});
</code></pre>

<p>I’ve been a little bit clever here, and included an <code>expect()</code> inside the fake fetcher function. This allows me to check that I’m calling the right URL. Let’s run the test:</p>

<figure>
<div class="readableLargeImageContainer"><img src="/assets/fetchFlickrData-error.png" alt="Sad cat ASCII art. 3 passing tests. 1 failing test. 1) FlickrFetcher #fetchFlickrData() should take an API key and fetcher function argument and return a promise for JSON data.: TypeError: FlickrFetcher.fetchFlickrData is not a function" /></div>
<figcaption>The cat is sad because there is no function yet.</figcaption>
</figure>

<h2 id="stubs">Stubs</h2>

<p>Now that I have a failing test, let’s take a moment to talk about what this is doing. The <code>fakeFetcher()</code> function I’ve used to replace <code>$.getJSON()</code> is known as a <em>stub.</em> A stub is a piece of code that has the same API and behaviour as the ‘real’ code, but with much reduced functionality. Usually this means returning static data instead of interacting with some external resource.</p>

<p>Stubs can replace many different types of code besides network calls. Most often we use them for things functional programmers call <em>side effects.</em> Typical stubs might replace things like:</p>

<ul>
<li>Queries to a relational database;</li>
<li>Interaction with the file system;</li>
<li>Accepting user input; or</li>
<li>Complex computations that take a long time to calculate.</li>
</ul>

<p>Stubs don’t always have to replace asynchronous or even slow things. It may simply be a piece of code you haven’t written yet. A stub can replace almost anything.</p>

<p>Stubs are an important tool for TDD. They help us to keep tests running fast so our workflow doesn’t slow down. More importantly, they allow us to have consistent tests for things that are inherently variable (like network calls).</p>

<p>Stubs do take a little bit of effort to use well though. For instance, using a stub meant adding an extra parameter to the <code>fetchFlickrData()</code> function. However, if you are using a <a href="/articles/2016/gentle-introduction-to-functional-javascript-intro" target="_blank">slightly functional-flavoured style of programming</a>, then you will be thinking about things like side effects and pure functions anyway. I would also argue that making your code testable (whether that’s using stubs or not) is usually worth the effort.</p>

<p>But enough about stubs—back to the code…</p>

<hr />

<p>Running the tests, I get an error, but that’s still a sad cat (<em>red</em>), so I can write some code. In this case, returning the expected result isn’t that simple. I have two <code>expect()</code> calls in there, so I have to call the fetcher function as well as return a promise for the data. In this case it’s easiest to write the general code straight-up:</p>

<pre><code>// flickr-fetcher
fetchFlickrData: function(apiKey, fetch) {
    var url = 'https://api.flickr.com/services/rest/?method=flickr.photos.search&api_key='
            + apiKey + '&text=pugs&format=json&nojsoncallback=1'
    return fetch(url).then(function(data) {
        return data;
    });
}
</code></pre>

<p>Run the test again, and the cat is happy (<em>green</em>). So it’s time to refactor.</p>

<p>This time there are two things I want to refactor. First of all, there’s no need to use <code>.then()</code> in the <code>fetchFlickrData()</code> function. So I refactor to take out the redundant code:</p>

<pre><code>fetchFlickrData: function(apiKey, fetch) {
    var url = 'https://api.flickr.com/services/rest/?method=flickr.photos.search&api_key='
            + apiKey + '&text=pugs&format=json&nojsoncallback=1'
    return fetch(url);
}
</code></pre>

<p>Running the tests again, everything still passes. But I would also like to refactor my test code. Mocha actually provides <em>two</em> ways to handle asynchronous code. The first is the <code>done()</code> function as we saw before. The second is specifically for Promises. If you return a Promise from your test, Mocha will automatically wait for it to either resolve or reject:</p>

<pre><code>// flickr-fetcher-spec.js
describe('#fetchFlickrData()', function() {
    it(
        'should take an API key and fetcher function argument and return a promise for JSON data.',
        function() {
            var apiKey      = 'does not matter much what this is right now',
                fakeData    = {
                    'photos': {
                        'page':    1,
                        'pages':   2872,
                        'perpage': 100,
                        'total':   '287170',
                        'photo':   [{
                            'id':       '24770505034',
                            'owner':    '97248275@N03',
                            'secret':   '31a9986429',
                            'server':   '1577',
                            'farm':     2,
                            'title':    '20160229090898',
                            'ispublic': 1,
                            'isfriend': 0,
                            'isfamily': 0
                        }, {
                            'id':       '24770504484',
                            'owner':    '97248275@N03',
                            'secret':   '69dd90d5dd',
                            'server':   '1451',
                            'farm':     2,
                            'title':    '20160229090903',
                            'ispublic': 1,
                            'isfriend': 0,
                            'isfamily': 0
                        }]
                    }
                },
                fakeFetcher = function(url) {
                    var expectedURL = 'https://api.flickr.com/services/rest/?method=flickr.photos.search&api_key='
                                + apiKey + '&text=pugs&format=json&nojsoncallback=1'
                    expect(url).to.equal(expectedURL)
                    return Promise.resolve(fakeData);
                };
            return FlickrFetcher.fetchFlickrData(apiKey, fakeFetcher).then(function(actual) {
                expect(actual).to.eql(fakeData);
            }
        );

    });
});
</code></pre>

<p>Running my refactored code, the tests still pass, so it’s on to the next step.</p>

<h2 id="buildingup">Building up</h2>

<p>At this point, I need to stop and think. There is one final thing to test before I can declare the <code>FlickrFetcher</code> module done: Do the pieces fit together OK? Can I make a network call, get back the results, and transform them into the format I want? It would be most convenient if I could do all this with one function.</p>

<p>So, I write a test:</p>

<pre><code>describe('#fetchPhotos()', function() {
    it('should take an API key and fetcher function, and return a promise for transformed photos', function() {
        var apiKey   = 'does not matter what this is right now',
            expected = [{
                title: 'Dog goes to desperate measure to avoid walking on a leash',
                url:   'https://farm2.staticflickr.com/1669/25373736106_146731fcb7_b.jpg'
            }, {
                title: 'the other cate',
                url:   'https://farm2.staticflickr.com/1514/24765033584_3c190c104e_b.jpg'
            }],
            fakeData = {
                'photos': {
                    'page':    1,
                    'pages':   2872,
                    'perpage': 100,
                    'total':   '287170',
                    'photo':   [{
                        id:       '25373736106',
                        owner:    '99117316@N03',
                        secret:   '146731fcb7',
                        server:   '1669',
                        farm:     2,
                        title:    'Dog goes to desperate measure to avoid walking on a leash',
                        ispublic: 1,
                        isfriend: 0,
                        isfamily: 0
                    }, {
                        id:       '24765033584',
                        owner:    '27294864@N02',
                        secret:   '3c190c104e',
                        server:   '1514',
                        farm:     2,
                        title:    'the other cate',
                        ispublic: 1,
                        isfriend: 0,
                        isfamily: 0
                    }]
                }
            },
            fakeFetcher = function(url) {
                var expectedURL = 'https://api.flickr.com/services/rest/?method=flickr.photos.search&api_key='
                            + apiKey + '&text=pugs&format=json&nojsoncallback=1'
                expect(url).to.equal(expectedURL)
                return Promise.resolve(fakeData);
            };

        return FlickrFetcher.fetchPhotos(apiKey, fakeFetcher).then(function(actual) {
            expect(actual).to.eql(expected);
        });
    });
});
</code></pre>

<p>Note that I am still using a fake fetcher function as an external dependency. Running the test, I get an error. The cat is sad, so I can write some code.</p>

<p>Because I’m just calling two functions, it’s just as easy to write the general case as it is to return the expected value.</p>

<pre><code>fetchPhotos: function(apiKey, fetch) {
    return FlickrFetcher.fetchFlickrData(apiKey, fetch).then(function(data) {
        return data.photos.photo.map(FlickrFetcher.transformPhotoObj);
    });
}
</code></pre>

<p>Running the test again, my test passes—happy cat (<em>green</em>). So it is time to refactor. But, since this function is just three or four (depending how you count it) function calls, there’s not much to refactor.<a href="#fn:2" title="see footnote" id="fnref:2" target="_blank"><sup>2</sup></a> So, for the moment, I have completed my first module.</p>

<p>So, what have we covered? In this article we covered two main topics: Testing asynchronous code and using stubs to standardise things like network calls. The next article will focus on <a href="/articles/2016/gentle-introduction-to-javascript-tdd-html-dom" target="_blank">working with HTML and the DOM</a>.</p>

<div>
<hr />
<ol>

<li id="fn:1">
<p>Yes, if you‘re using a version of jQuery earlier than 3.0, it’s only Promise–like, but either way it's close enough for our purposes here.  <a href="#fnref:1" title="return to body" target="_blank"> ↩</a></p>
</li>

<li id="fn:2">
<p>It could be slightly more terse if I was using functional programming techniques, like a <code>mapWith()</code> function and/or <code>partial()</code>, but to use either of those I would have to introduce a dependency or write my own implementation. <a href="#fnref:2" title="return to body" target="_blank"> ↩</a></p>
</li>

</ol>
</div>
        
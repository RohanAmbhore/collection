<a href="https://jrsinclair.com/articles/2016/gentle-introduction-to-javascript-tdd-intro/">https://jrsinclair.com/articles/2016/gentle-introduction-to-javascript-tdd-intro/</a><div id="articleHeader"><h1>A Gentle Introduction to Javascript Test Driven Development: Part 1</h1></div>
          <p>
          Written by James Sinclair
          on the <time>11<sup>th</sup> April 2016</time>
          </p>
        </header>
        
          <p>This is part one of a three-part series outlining my personal approach to JavaScript Test Driven Development (TDD). Over the course of the series, I’ll work through developing a full application (albeit a small, simple one) in JavaScript that involves making network requests (also known as <abbr>AJAX</abbr>) and manipulating the <abbr>DOM</abbr>. The various parts are as follows:</p>



<h2 id="whytestdrivendevelopment">Why Test Driven Development?</h2>

<p>Getting started with test driven development can be daunting. It sounds tedious, boring and hard. The word ‘test’ conjures up associations with exams and stress and invigilators and all kinds of unpleasantness. And it does seem like a waste to write code that doesn’t <em>do</em> anything useful other than tell you that the code you wrote is working. On top of all that, there’s also a confusing array of frameworks and libraries out there. Some work on the server; some work in the browser; some do both… it can be hard to know where to start.</p>

<blockquote>
<p>The common predictable objections are “Writing unit tests takes too much time,” or “How could I write tests first if I don’t know what it does yet?” And then there’s the popular excuse: “Unit tests won’t catch all the bugs.” <a href="#fn:1" title="see footnote" id="fnref:1" target="_blank"><sup>1</sup></a></p>
</blockquote>

<p>There are, however, a lot of good reasons to give TDD a go. Here are three I think are important:</p>

<ol>
<li><strong>It forces one to think.</strong> This is a lot more useful than it sounds. Writing a test forces me to think clearly about what I am trying to achieve, down to the level of detail that a computer can check. It forces me to be specific about what I’m trying to do. Once I’ve got that clear in my head, it becomes much easier to write the code. If I’m struggling to write a test, then I know that I haven’t fully understood the problem I’m trying to solve.</li>
<li><strong>It makes debugging easier.</strong> While TDD won’t cause you to write less bugs (sadly), it does make it much easier to track them down when they inevitably pop up. And if I then write a test related to that bug, it gives me confidence that I know I’ve definitely fixed that particular bug. And I can re-run all my other tests to check that my bug-fix hasn’t broken other bits of my code.<a href="#fn:2" title="see footnote" id="fnref:2" target="_blank"><sup>2</sup></a></li>
<li><strong>It makes coding more fun.</strong> In my mind, this reason far outweighs the other two. Practicing the simple steps of TDD is kind of addictive and fun. The discipline of TDD takes a bit of getting used to, but once you’ve got the hang of it, coding becomes more enjoyable.</li>
</ol>

<p>Those aren’t the only reasons to take up TDD, but hopefully they are enough to convince you to give it a try. In a moment we’ll start working through a simple example, but first, let’s go over the basic outline of how it works.</p>

<h2 id="whatistdd">What is TDD?</h2>

<p>TDD is an approach to writing software where you write tests before you write application code. The basic steps are:</p>

<ol>
<li><strong>Red:</strong> Write a test and make sure it fails.</li>
<li><strong>Green:</strong> Write the simplest, easiest possible code to make the test pass.</li>
<li><strong>Refactor:</strong> Optimise and/or simplify the application code, making sure that all the tests still pass.</li>
</ol>

<p>Once we finish step 3, we start the cycle again by writing another test.</p>

<p>These three steps form the TDD mantra: ‘red, green, refactor’. We’ll examine each of these in detail as we go through an example. But first one final thing.</p>

<p>TDD is a form of self discipline—a life hack—it doesn’t magically make one a better coder. In theory, there’s no reason why a great coder couldn’t write exactly the same code as someone who doesn’t. But the reality is that the discipline of TDD strongly encourages one to:</p>

<ol>
<li>Write tests; and</li>
<li>Write smaller, easier-to-understand units of code.</li>
</ol>

<p>Personally, I find that if I’m not practicing TDD, I hardly ever write any tests at all, and the functions I write are larger and more complicated. That’s not to say I’m not testing—I’m hitting the refresh button in my one browser all the time—but my tests are useless to anyone else but myself.</p>

<h2 id="aworkedexample">A worked example</h2>

<p>Let’s take a fairly typical JavaScripty-type thing to do as our example: Fetch some data from a server (in this case, a list of photos from Flickr.com), transform it to HTML, and add it to a web page. You can <a href="http://codepen.io/jrsinclair/pen/EKQmwo" target="_blank">see the final result in action in this CodePen</a> (with a dash of added CSS).</p>

<p>For this example, we’ll use the <a href="http://mochajs.org/" target="_blank">Mocha</a> framework. I’ve chosen Mocha, not because it’s the most popular JavaScript testing framework (though it is); not because it is enormously better than other test frameworks (<a href="https://medium.com/javascript-scene/why-i-use-tape-instead-of-mocha-so-should-you-6aa105d8eaf4#.bb72m9mmf" target="_blank">it isn’t</a>); but for the simple reason that if I add the <code>--reporter=nyan</code> option on the command line, then my test report features a flying rainbow space cat. And that makes it <em><a href="/articles/2016/tdd-should-be-fun" target="_blank">more fun</a></em>:</p>

<pre><code>mocha --reporter=nyan
</code></pre>

<h2 id="settingup">Setting up</h2>

<p>For this tutorial, we’ll run all our tests on the command line using Node. Now you may be thinking, ‘Aren’t we writing a web application that will run entirely in the browser?’ And the answer is yes, we are. But running our tests in Node is much faster, and the differences between the browser and Node will help us to think carefully about how to structure the code (more on that later).</p>

<p>To get started, we will need Node installed, plus Mocha and one other module called Chai. If you are using OS X, then I recommend using Homebrew to install Node, as it is easy to keep up to date. Once you’ve got Homebrew set up, you can install Node from the command line as follows:</p>

<pre><code>$ brew install node
</code></pre>

<p>If you’re on Linux, then you can use your regular package manager system (like <code>apt-get</code> or <code>yum</code>) to install Node<a href="#fn:3" title="see footnote" id="fnref:3" target="_blank"><sup>3</sup></a>.</p>

<p>And if you’re using Windows, then I recommend visiting the Node website, and grabbing the installer.</p>

<p>Once we have Node installed, we can use the Node Package Manager (npm) to install Mocha and Chai for us. Make sure to change to the directory where you are going to write your code, and run these commands:</p>

<pre><code>cd /path/to/place/where/I/will/write/my/code
npm install mocha -g
npm install chai
</code></pre>

<p>Now that we have the prerequisites installed, we can start thinking about the application we want to build.</p>

<h2 id="thinking">Thinking</h2>

<p>So, while we said just a moment ago that there are only 3 steps to TDD, it’s not entirely true. There’s a step zero. You have to think first, then write a test. To put it another way: Before you write a test you have to have at least some idea of what you want to achieve and how you will structure your code. It’s test driven <em>development</em>, not test driven <em>design</em>.</p>

<p>Let’s first describe what we want to do in a little more detail:</p>

<ol>
<li>Send a request to the Flickr API, and retrieve a bunch of photograph data;</li>
<li>Transform the data into a single array of objects, each object containing just the data we need;</li>
<li>Convert the array of objects into an HTML list; and</li>
<li>Add the HTML to the page.</li>
</ol>

<p>Next I need to think about how to structure the code. Since it is a fairly simple task, I <em>could</em> put everything into one module. But, I have a few choices as to how I could perform the last two steps (making HTML and putting it into the page):</p>

<ul>
<li>I can change the DOM directly to add HTML to the page, using standard DOM interfaces;</li>
<li>I could use jQuery to add the HTML to the page; or</li>
<li>I could use a framework like React.js or a Backbone View.</li>
</ul>

<p>Since I will probably use jQuery to make the HTTP request to the server, it seems (at this stage, anyway) that the simplest approach will be to use jQuery to manipulate the DOM. But, in the future I might change my mind and use a React component. So, it makes sense to keep the fetch-and-transform bit of the application separate from the make-HTML-and-add-to-DOM bit. So, I will create two modules: one for fetching the data and transforming it; and another for managing the HTML.</p>

<p>With this in mind, I’ll create four files to house my code:</p>

<ol>
<li><code>flickr-fetcher.js</code> for the module that fetches the data and transforms it;</li>
<li><code>photo-lister.js</code> for the module that takes the list, converts it to HTML and adds it to the page;</li>
<li><code>flickr-fetcher-spec.js</code> for the code to test <code>flickr-fetcher.js</code>; and</li>
<li><code>photo-lister-spec.js</code> for the code to test <code>photo-lister.js</code>.</li>
</ol>

<h2 id="writingtests">Writing tests</h2>

<p>With these files in place I can start thinking about writing my first test. Now, I want to write the simplest test possible that will still move my codebase forward. So a useful thing to do at this point would be to test that I can load the module. In <code>flickr-fetcher-spec.js</code> I write:</p>

<pre><code>// flickr-fetcher-spec.js
'use strict';
var expect = require('chai').expect;

describe('FlickrFetcher', function() {
    it('should exist', function() {
        var FlickrFetcher = require('./flickr-fetcher.js');
        expect(FlickrFetcher).to.not.be.undefined;
    });
});
</code></pre>

<p>There are a few things to note here. First of all, because all these tests run using Node, this means that we import modules using the node-style <code>require()</code>.</p>

<p>The next thing to note is that we are using a ‘Behaviour Driven Development’ (BDD) style to write the tests. This is a variation on TDD where tests are written in the form: <em>Describe <strong>[thing]</strong>. It should <strong>[do something]</strong>.</em> The <em>[thing]</em> can be a module, or a class, or a method, or a function. Mocha includes built-in functions like <code>describe()</code> and <code>it()</code> to make writing in this style possible.</p>

<p>The third thing to note is the <code>expect()</code> chain that does the checking. In this case I am checking simply that my module is not <code>undefined</code>. Most of the time though, the pattern I will use is <code>expect(actualValue).to.equal.(expectedValue);</code>.</p>

<p>So, let’s run the test:</p>

<pre><code>mocha --reporter=nyan flickr-fetcher-spec.js
</code></pre>

<p>If everything is installed correctly, I see a happy cat like the one below.</p>

<figure>
<div class="readableLargeImageContainer"><img src="/assets/1-passing-test.png" alt="One passing test" /></div>
<figcaption>One passing test</figcaption>
</figure>

<p>Our test passes, which seems silly given that we haven’t written any module code. This is because my file <code>flickr-fetcher.js</code> exists (and Node gives you an empty object if you <code>require</code> a blank file). Since I don’t have a failing test though, I won’t write any module code. The rule is: No module code until there’s a failing test. So what do I do? I write another test—which means <em>thinking</em> again.</p>

<p>So, the first two things I want to achieve are:</p>

<ol>
<li>Fetch data from Flickr, and</li>
<li>Transform the data.</li>
</ol>

<p>Fetching data from Flickr involves making a network call though, so like a good functional programmer, <a href="https://twitter.com/ghewgill/status/25051171050" target="_blank">I’m going to put that off until later</a>.<a href="#fn:4" title="see footnote" id="fnref:4" target="_blank"><sup>4</sup></a> Instead, let’s focus on the data transformation.</p>

<p>I want to take each of the photo objects that Flickr gives us and transform it into an object that has just the information that I want—in this case, a title and image URL. The URL is tricky though because the Flickr API doesn’t return fully formed URLs. Instead, I have to <a href="https://www.flickr.com/services/api/misc.urls.html" target="_blank">construct a URL based on the size of photo I want</a>. Now, that seems like a good place to start for the next test: Something small, testable, that will move the codebase forward. I can now write a test.</p>

<pre><code>// flickr-fetcher-spec.js
var FlickrFetcher = require('./flickr-fetcher.js');

describe('#photoObjToURL()', function() {
    it('should take a photo object from Flickr and return a string', function() {
        var input = {
            id:       '24770505034',
            owner:    '97248275@N03',
            secret:   '31a9986429',
            server:   '1577',
            farm:     2,
            title:    '20160229090898',
            ispublic: 1,
            isfriend: 0,
            isfamily: 0
        };
        var expected = 'https://farm2.staticflickr.com/1577/24770505034_31a9986429_b.jpg';
        var actual = FlickrFetcher.photoObjToURL(input);
        expect(actual).to.eql(expected);
    });
});
</code></pre>

<p>Note that I have used <code>expect(actual).to.eql(expected);</code> here rather than <code>expect(actual).to.equal(expected);</code>. This tells Chai to to check that every single value inside <code>actual</code> matches every single value inside <code>expected</code>. The rule of thumb is, use <code>equal</code> when comparing numbers, strings, or booleans, and use <code>eql</code> when comparing arrays or objects.</p>

<p>So I run the test again and… sad cat. I have an error. This means I can write some code. Step one is simply to get the module structure in place:</p>

<pre><code>// flickr-fetcher.js
var FlickrFetcher;

FlickrFetcher = {
    photoObjToURL: function() {}
};

module.exports = FlickrFetcher;
</code></pre>

<p>If I run my test now, I get a failure rather than an error, but the cat is still sad (<em>red</em>), so I can keep writing code. The question now is, what is the simplest possible code that I could write to make this test pass? And the answer is, of course, to return the expected result:</p>

<pre><code>var FlickrFetcher;

FlickrFetcher = {
    photoObjToURL: function() {
        return 'https://farm2.staticflickr.com/1577/24770505034_31a9986429_b.jpg';
    }
};
</code></pre>

<p>Run the tests again and everything passes—happy cat (<em>green</em>).</p>

<p>The next step is to refactor. Is there any way I can make this function more efficient or clearer? At the moment I think this code is probably about as clear and efficient as it can be. But, we all know this function is pretty useless. You may well be thinking “if you pass in any other valid object, that function would not work”. And that’s a very good point. I should write another test and pass in another valid object:</p>

<pre><code>// flickr-fetcher-spec.js
describe('#photoObjToURL()', function() {
    it('should take a photo object from Flickr and return a string', function() {
        var input = {
            id:       '24770505034',
            owner:    '97248275@N03',
            secret:   '31a9986429',
            server:   '1577',
            farm:     2,
            title:    '20160229090898',
            ispublic: 1,
            isfriend: 0,
            isfamily: 0
        };
        var expected = 'https://farm2.staticflickr.com/1577/24770505034_31a9986429_b.jpg';
        var actual = FlickrFetcher.photoObjToURL(input);
        expect(actual).to.eql(expected);

        input = {
            id:       '24770504484',
            owner:    '97248275@N03',
            secret:   '69dd90d5dd',
            server:   '1451',
            farm:     2,
            title:    '20160229090903',
            ispublic: 1,
            isfriend: 0,
            isfamily: 0
        };
        expected = 'https://farm2.staticflickr.com/1451/24770504484_69dd90d5dd_b.jpg';
        actual = FlickrFetcher.photoObjToURL(input);
        expect(actual).to.eql(expected);
    });
});
</code></pre>

<p>I run the test, and it fails—sad cat.</p>

<p>Now that we have a new test, the question is, what is the simplest possible code we could write to make this test pass? With two tests the answer isn’t so simple. I <em>could</em> write an if- statement and return the second expected URL, but it’s almost the same amount of effort to write the general code, so I’ll do that instead.</p>

<pre><code>// flickr-fetcher.js
FlickrFetcher = {
    photoObjToURL: function(photoObj) {
        return 'https://farm' + photoObj.farm + '.staticflickr.com/' + photoObj.server + '/' + photoObj.id + '_' +
            photoObj.secret + '_b.jpg';
    }
};
</code></pre>

<p>Run the tests again—happy cat. I have a working function.</p>

<p>We’re back to the refactoring step. Now, this code is still fairly simple, but all those plus signs look a bit ugly to me. One way to get rid of them would be to use a template library of some sort (like Handlebars or <a href="http://mir.aculo.us/2011/03/09/little-helpers-a-tweet-sized-javascript-templating-engine/" target="_blank">something lighter-weight</a>), but it doesn’t seem worth adding the extra code just for this one function. Maybe I could try something else. If I put all the string parts into an array, I can glue them all together with the <code>join()</code> method. As an added bonus most JavaScript implementations will run array joins ever-so-slightly faster than concatenation. So I refactor to use <code>join()</code>:</p>

<pre><code>FlickrFetcher = {
    photoObjToURL: function(photoObj) {
        return [ 'https://farm',
            photoObj.farm, '.staticflickr.com/', 
            photoObj.server, '/',
            photoObj.id, '_',
            photoObj.secret, '_b.jpg'
        ].join('');
    }
};
</code></pre>

<p>I run the tests again, and my tests still pass, so I know everything works. Time to move to the next test…</p>

<p>At this point, if I were writing a module to be published with <a href="https://www.npmjs.com/" target="_blank">npm</a>, I would now write tests to cover all the crazy things someone might pass this function. For example:</p>

<ul>
<li>What should happen if someone passes a string instead of an object?</li>
<li>What should happen if someone passes no parameters?</li>
<li>What should happen if someone passes an object that has the wrong property names?</li>
<li>What should happen if someone passes in an object with the right property names but the values aren’t strings?</li>
</ul>

<p>All of these are good questions to ask, and test, but I won’t go through that process here: Firstly because it would be incredibly dull to read, and secondly because this is a toy project that isn’t mission-critical for anything. I won’t be losing anyone’s money or endangering anyone’s life if this code doesn’t handle an edge case gracefully. For now, I know that it does what I want it to do. If I <em>were</em> however, writing life-support software or handling credit card details, or anything remotely like that, then I definitely want to answer all of those questions.</p>

<p>We’ve been through the full cycle with a working function: <em>red</em>, <em>green</em>, <em>refactor</em>. Now it’s time to pick the next test. Time to <em>think</em>. I want to take the list of photo objects that Flickr gives us and transform it into a list of objects that have just the information that I want. If I’m going to process a list, that will probably involve some kind of <a href="/articles/2016/gentle-introduction-to-functional-javascript-arrays/#map" target="_blank">map operation</a>, so I want to create a function that will just process one object at a time. That gives me another nice, small, testable unit of code to test. So, I write some test code:</p>

<pre><code>// flickr-fetcher-spec.js
describe('#transformPhotoObj()', function() {
    it('should take a photo object and return an object with just title and URL', function() {
        var input = {
                id:       '25373736106',
                owner:    '99117316@N03',
                secret:   '146731fcb7',
                server:   '1669',
                farm:     2,
                title:    'Dog goes to desperate measure to avoid walking on a leash',
                ispublic: 1,
                isfriend: 0,
                isfamily: 0
            },
            expected = {
                title: 'Dog goes to desperate measure to avoid walking on a leash',
                url:   'https://farm2.staticflickr.com/1669/25373736106_146731fcb7_b.jpg'
            },
            actual = FlickrFetcher.transformPhotoObj(input);
        expect(actual).to.eql(expected);
    });
});
</code></pre>

<p>When I run the test, I get an error because the function does not exist:</p>

<figure>
<div class="readableLargeImageContainer"><img src="/assets/transformPhotoObj-error.png" alt="Sad cat ASCII art. 2 Passing tests. 1 Failing test. FlickrFetcher #transformPhotoObj() should take a photo object and return an object with just title and URL: TypeError: FlickrFetcher.transformPhotoObj is not a function" /></div>
<figcaption>The cat is sad because my function does not exist yet.</figcaption>
</figure>

<p>Now that I have a sad cat (<em>red</em>), I can write some code. What would be the simplest way to make this test pass? Again, just create a function that returns the expected result:</p>

<pre><code>    transformPhotoObj: function() {
        return {
            title: 'Dog goes to desperate measure to avoid walking on a leash',
            url:   'https://farm2.staticflickr.com/1669/25373736106_146731fcb7_b.jpg'
        };
    }
</code></pre>

<p>I re-run the tests, and the cat is happy again (<em>green</em>).</p>

<figure>
<div class="readableLargeImageContainer"><img src="/assets/3-passing-tests.png" alt="Happy cat ASCII art. 3 passing tests." /></div>
<figcaption>3 passing tests and a happy cat.</figcaption>
</figure>

<p>Can I refactor this code? Or all my code? At this stage probably not. But, this code is not terribly useful, as it can only handle one specific input, so I need to write another test:</p>

<pre><code>describe('#transformPhotoObj()', function() {
    it('should take a photo object and return an object with just title and URL', function() {
        var input = {
                id:       '25373736106',
                owner:    '99117316@N03',
                secret:   '146731fcb7',
                server:   '1669',
                farm:     2,
                title:    'Dog goes to desperate measure to avoid walking on a leash',
                ispublic: 1,
                isfriend: 0,
                isfamily: 0
            },
            expected = {
                title: 'Dog goes to desperate measure to avoid walking on a leash',
                url:   'https://farm2.staticflickr.com/1669/25373736106_146731fcb7_b.jpg'
            },
            actual = FlickrFetcher.transformPhotoObj(input);
        expect(actual).to.eql(expected);

        input = {
            id:       '24765033584',
            owner:    '27294864@N02',
            secret:   '3c190c104e',
            server:   '1514',
            farm:     2,
            title:    'the other cate',
            ispublic: 1,
            isfriend: 0,
            isfamily: 0
        };
        expected = {
            title: 'the other cate',
            url:   'https://farm2.staticflickr.com/1514/24765033584_3c190c104e_b.jpg'
        }
        actual = FlickrFetcher.transformPhotoObj(input);
        expect(actual).to.eql(expected);
    });
});
</code></pre>

<figure>
<div class="readableLargeImageContainer"><img src="/assets/transformPhotoObj-failing.png" alt="Sad cat ASCII art. 2 Passing tests. 1 failing test. 1) FlickrFetcher #transformPhotoObj() should take a photo object and return an object with just title and URL: AssertionError: expected { Object (title, url) } to deeply equal { Object (title, url) }" /></div>
<figcaption>The test is failing and our cat is sad.</figcaption>
</figure>

<p>Now, the simplest, easiest way to make these tests pass now is to write the full function code, making use of the <code>photoObjToURL()</code> function I created earlier:</p>

<pre><code>// flickr-fetcher.js
//… trimmed for brevity …
transformPhotoObj: function(photoObj) {
    return {
        title: photoObj.title,
        url:   FlickrFetcher.photoObjToURL(photoObj)
    };
}
</code></pre>

<p>I run my tests again, and we have a happy cat (<em>green</em>).</p>

<figure>
<div class="readableLargeImageContainer"><img src="/assets/3-passing-tests.png" alt="Happy cat ASCII art. 3 passing tests." /></div>
<figcaption>Three passing tests and a happy cat.</figcaption>
</figure>

<p>Next is refactoring. Could this function be improved? At this stage, probably not. But it’s important to keep asking that question every time. Refactoring is one of the delicacies of programming and should be savoured whenever possible.</p>

<p>By now you should have a feel for the basic steps of TDD: Red, green, refactor. In this article we’ve looked at how to get started writing code with TDD. We’ve also looked at how it’s important to think before you write a test—TDD is no replacement for good software design. In the next two articles, we’ll examine <a href="/articles/2016/gentle-introduction-to-javascript-tdd-ajax" target="_blank">how to handle asynchronous network calls</a> and <a href="/articles/2016/gentle-introduction-to-javascript-tdd-html-dom" target="_blank">how to test DOM-manipulating code without a browser.</a></p>

<div>
<hr />
<ol>

<li id="fn:1">
<p>Jeff Patton, 21 January 2005, <a href="http://www.stickyminds.com/article/test-driven-development-isnt-testing" target="_blank">Test–Driven Development Isn't Testing</a> <a href="#fnref:1" title="return to body" target="_blank"> ↩</a></p>
</li>

<li id="fn:2">
<p>Yes, I know what you‘re thinking, "re–running your tests doesn’t guarantee that you haven't introduced other bugs." That is correct. But re–running my tests to check for regression errors is a heck of a lot better than not checking at all. And if my comprehensive suite of tests passes, then I can have some level of confidence that the main business logic still works. <a href="#fnref:2" title="return to body" target="_blank"> ↩</a></p>
</li>

<li id="fn:3">
<p>And let‘s face it, if you’re using Linux and reading this article, you probably have Node installed already. <a href="#fnref:3" title="return to body" target="_blank"> ↩</a></p>
</li>

<li id="fn:4">
<p>See the next article for how to handle network calls. <a href="#fnref:4" title="return to body" target="_blank"> ↩</a></p>
</li>

</ol>
</div>
        
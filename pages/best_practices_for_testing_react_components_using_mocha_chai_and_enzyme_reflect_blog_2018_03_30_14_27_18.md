<a href="https://reflect.io/blog/js-testing-mocha-chai-enzyme/">https://reflect.io/blog/js-testing-mocha-chai-enzyme/</a><div id="articleHeader"><h1>Best practices for testing React components using Mocha, Chai, and Enzyme</h1></div>
                
                  <div class="readableLargeImageContainer"><img src="/assets/blog/react-large-logo-302852c5e828773bd25913ac9d64b1c320bbc19d26c047068f4dbe28828ea109.png" /></div>
                

                

                
                <p>As a data visualization company, our success is crucially dependent on the
front-end portion of our product. We subject our whole front-end stack, which
is largely based on React, to a thorough arsenal of unit tests, smoke tests,
and more.
</p>
                

                <p>Today we’d like to share some of the things that we’ve learned from testing
React components across multiple projects using an in-house testing stack
that we built using <a href="https://mochajs.org" target="_blank">Mocha</a>, <a href="http://chaijs.com" target="_blank">Chai</a>,
<a href="https://github.com/airbnb/enzyme" target="_blank">Enzyme</a>.</p>

<p>First, a more general lesson.</p>

<h2 id="dont-be-afraid-to-update-your-toolchain">Don’t be afraid to update your toolchain</h2>

<p>It’s easy to get sidetracked by the latest and greatest tools out there,
<a href="https://hackernoon.com/how-it-feels-to-learn-javascript-in-2016-d3a717dd577f#.dcwvlk1z8" target="_blank">especially</a>
in the world of front-end development. You’re <em>usually</em> better off sticking
with what works rather than making big investments in shiny new things. <strong>But
sometimes adopting newer tools and leaving behind more well-established ones
can really pay off</strong>.</p>

<p>In our case, we made a good move in deciding that
<a href="https://jasmine.github.io" target="_blank">Jasmine</a>, the core of our old testing stack, needed
to go. Jasmine does have its strengths but we found it to be too slow, too
cumbersome to work with, and too heavy on boilerplate to fit our needs. So we
decided to survey the ever-expanding galaxy of testing tools and put together
something that works better for us.</p>

<h3 id="our-new-hybrid-testing-stack">Our new hybrid testing stack</h3>

<p>In place of our previous Jasmine-based stack, we’ve adopted a testing stack
consisting of <a href="https://mochajs.org/" target="_blank">Mocha</a> as our test runner,
<a href="http://chaijs.com/" target="_blank">Chai</a> for assertions, and
<a href="https://github.com/airbnb/enzyme" target="_blank">Enzyme</a> for asserting on component output,
properties, and state. This stack has enabled us to write tests that are fast,
easy to write, and light on setup boilerplate.</p>

<p>Perhaps most importantly, we’ve <strong>standardized on this stack across all of our
front-end projects</strong> (all of which rely heavily on React). This has enabled us
to sharply reduce context switching costs for moving between projects, as our
front-end engineers can learn one toolset and use that knowledge anywhere.</p>

<p>Your testing stack might look quite different from ours, but you should work
toward standardization if at all possible. Both current and future team members
will thank you.</p>

<h2 id="use-shallow-rendering-whenever-possible">Use shallow rendering whenever possible</h2>

<p><a href="http://airbnb.io/enzyme/docs/api/shallow.html" target="_blank">Shallow rendering</a> enables you
to test a React component very efficiently because only the component and its
immediate children is rendered. The other approach, which involves
<a href="http://airbnb.io/enzyme/docs/api/mount.html" target="_blank">mounting</a> components, doesn’t
provide the same isolation and almost always leads to slower, less specific
tests.</p>

<p><code>mount()</code> is still great—and sometimes necessary—but if you’re not careful
in use it can easily turn what should be lean and speedy unit tests into
bulky integration tests. The point of unit tests is to test an individual unit
of work, and Enzyme’s shallow rendering enables us to do precisely that.</p>

<h2 id="avoid-sharing-enzyme-wrappers-between-test-cases">Avoid sharing Enzyme wrappers between test cases</h2>

<p>Recreating React components in every test case is fairly inexpensive, especially
when using shallow rendering. This allows us to isolate our test cases and easily
tell what is being tested. The drawback, of course, is duplication of components,
but we think that the trade-off is worth it.</p>



<p>In this example, a single <code>wrapper</code> object is used by two different tests:</p>

<div><pre><code>const wrapper = shallow(&lt;Thing name={'Steve'} /&gt;);

it('should do stuff', () =&gt; {
  expect(wrapper).to.doStuff();
});

it('should do different stuff', () =&gt; {
  expect(wrapper).to.doDifferentStuff();
});
</code></pre>
</div>



<p>In this example, two different tests use two (identical) <code>wrapper</code> objects,
which makes it immediately clear <em>within the test</em> which wrapper is being
tested:</p>

<div><pre><code>const defaultProps = { name: 'Steve'; };

it('should do stuff', () =&gt; {
  const wrapper = shallow(&lt;Thing {...defaultProps} /&gt;);
  expect(wrapper).to.doStuff();
});

it('should do different stuff', () =&gt; {
  const wrapper = shallow(&lt;Thing {...defaultProps} /&gt;);
  expect(wrapper).to.doDifferentStuff();
});
</code></pre>
</div>

<h2 id="only-pass-required-props-when-rendering-components">Only pass required props when rendering components</h2>

<p>As you saw above, one useful practice we’ve found is defining <code>defaultProps</code> in
a <code>describe</code> scope, then reusing those properties among your test cases. A
<code>defaultProps</code> object should usually be as bare as you can make it, and it
should mirror the required <code>propTypes</code> from the component under test.</p>

<p>Your component should be able to render with just the required props. To assert
on this, essentially every React component in our codebase contains the
following test:</p>

<div><pre><code>const defaultProps = {
  dispatch: () =&gt; {},
  manifest: { components: [] },
};

it('should render without blowing up', () =&gt; {
  const wrapper = shallow(&lt;Thing {...defaultProps} /&gt;);
  expect(wrapper.length).to.eql(1);
});
</code></pre>
</div>

<p>In every other test case, we only pass the props we absolutely need in order
for the case to pass. This makes it easy to precisely spot what’s going on as
well as which functionality is being tested.</p>

<h2 id="standardize-on-a-few-chai--enzyme-assertions">Standardize on a few Chai + Enzyme assertions</h2>

<p>Chai has a <em>huge</em> <a href="http://chaijs.com/api/assert/" target="_blank">assertions API</a>. This isn’t a
bad thing in itself, but it can be hard to keep track of all the possible ways
of asserting something, which in turn makes your test code less readable (even
if you’re using a tool like
<a href="https://github.com/producthunt/chai-enzyme" target="_blank">chai-enzyme</a>).</p>

<p>To give an example, Here are four different ways to assert on a class name (and
there are likely many others):</p>

<div><pre><code>expect(&lt;Component /&gt;).to.have.className('my-class');
expect(&lt;Component /&gt;).hasClass('my-class').to.be.true;
expect(&lt;Component /&gt;).html().to.contain('class="my-class"');
expect(&lt;Component /&gt;).hasClass('my-class').to.eql(true);
</code></pre>
</div>

<p>You can avoid this by choosing a preferred way to write a given assertion and
communicating that to the members of your team (e.g. in your internal
documentation).</p>

<h2 id="conclusion-rejoice-that-so-many-tools-are-available-but-adopt-them-wisely">Conclusion: rejoice that so many tools are available, but adopt them wisely</h2>

<p>It’s a great time to be a JavaScript developer. There are so many great new
frameworks, tools, libraries, and testing tools popping up all the time. Trying
them out is fun, but it’s important to be disciplined about it. Standardizing
on some best practices will give you the freedom to experiment with
bleeding-edge tools and shiny new objects without compromising your
productivity.</p>


                <div>
    
      <div>
        
          <img src="/assets/blog/authors/colby-52ee2ae371fb921896beac7fffe7064832ecbcc171989c31e1e77335f94892fd.jpg" />
        
        
          Colby Aley
        
        December 19, 2016
      </div>
    

  


              
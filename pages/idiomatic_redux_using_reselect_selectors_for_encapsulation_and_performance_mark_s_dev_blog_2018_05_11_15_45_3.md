<a href="http://blog.isquaredsoftware.com/2017/12/idiomatic-redux-using-reselect-selectors/">http://blog.isquaredsoftware.com/2017/12/idiomatic-redux-using-reselect-selectors/</a><div id="articleHeader"><h1>Idiomatic Redux: Using Reselect Selectors for Encapsulation and Performance</h1></div>
    
	
        
	    
    	<p>This is a post in the <a href="/series/idiomatic-redux" target="_blank"><b>Idiomatic Redux</b></a> series.
        </p><hr />
	 
  </header>
  
    <p><em>An overview of why and how to use Reselect with React and Redux</em></p>

<h2 id="intro">Intro</h2>

<p>In a good Redux architecture, you are encouraged to <a href="https://redux.js.org/docs/recipes/ComputingDerivedData.html" target="_blank">keep your store state minimal, and derive data from the state as needed</a>.  As part of that process, we recommend that you use "selector functions" in your application, and use the Reselect library to help create those selectors.  Here's a deeper look at why this is a good idea, and how to correctly use Reselect.</p>

<h2 id="basics-of-selectors">Basics of Selectors</h2>

<p>A "selector function" is simply any function that accepts the Redux store state (or part of the state) as an argument, and returns data that is based on that state.  Selectors don't have to be written using a special library, and it doesn't matter whether you write them as arrow functions or the <code>function</code> keyword.  For example, these are all selectors:</p>

<pre><code>const selectEntities = state =&gt; state.entities;

function selectItemIds(state) {
    return state.items.map(item =&gt; item.id);
}

const selectSomeSpecificField = state =&gt; state.some.deeply.nested.field;

function selectItemsWhoseNamesStartWith(items, namePrefix) {
     const filteredItems = items.filter(item =&gt; item.name.startsWith(namePrefix));
     return filteredItems;
}
</code></pre>

<p>You can call your selector functions whatever you want, but it's common to prefix them with <code>select</code> or <code>get</code>, or end the name with <code>Selector</code>, like <code>selectFoo</code>, <code>getFoo</code>, or <code>fooSelector</code> (see <a href="https://twitter.com/_jayphelps/status/739905438116806656" target="_blank">this Twitter poll on naming selectors</a> for discussion).</p>

<p>The first reason to use selector functions is for encapsulation and reusability. Let's say that one of your <code>mapState</code> functions looks like this:</p>

<pre><code>const mapState = (state) =&gt; {
    const data = state.some.deeply.nested.field;

    return {data};
}
</code></pre>

<p>That's a totally legal statement.  But, imagine that you've got several components that need to access that field.  What happens if you need to make a change to where that piece of state lives?  You would now have to go change <em>every</em> <code>mapState</code> function that references that value.  So, in the same way that <a href="/2016/10/idiomatic-redux-why-use-action-creators/" target="_blank">we recommend using action creators to encapsulate details of creating actions</a>, we recommend using selectors to encapsulate the knowledge of where a given piece of state lives.  <strong>Ideally, only your reducer functions and selectors should know the exact state structure, so if you change where some state lives, you would only need to update those two pieces of logic</strong>.</p>

<p>One common description of selectors is that they're like "queries into your state".  You don't care about exactly how the query came up with the data you needed, just that you asked for the data and got back a result.</p>

<h2 id="reselect-usage-and-memoization">Reselect Usage and Memoization</h2>

<p>The next reason to use selectors is to improve performance.  Performance optimization generally involves doing work faster, or finding ways to do less work.  For a React-Redux app, selectors can help us do less work in a couple different ways.</p>

<p>Let's imagine that we have a component that requires a very expensive filtering/sorting/transformation step for the data it needs.  To start with, its <code>mapState</code> function looks like this:</p>

<pre><code>const mapState = (state) =&gt; {
    const {someData} = state;

    const filteredData = expensiveFiltering(someData);
    const sortedData = expensiveSorting(filteredData);
    const transformedData = expensiveTransformation(sortedData);

    return {data : transformedData};
}
</code></pre>

<p>Right now, that expensive logic will re-run for <em>every</em> dispatched action that results in a state update, even if the store state that was changed was in a part of the state tree that this component doesn't care about.</p>

<p>What we really want is to only re-run these expensive steps if <code>state.someData</code> has actually changed.  This is where the idea of "memoization" comes in.</p>

<p>Memoization is a form of caching.  It involves tracking inputs to a function, and storing the inputs and the results for later reference.  If a function is called with the same inputs as before, the function can skip doing the actual work, and return the same result it generated the last time it received those input values.</p>

<p><strong>The <a href="https://github.com/reactjs/reselect" target="_blank">Reselect library</a> provides a way to create memoized selector functions.</strong>  Reselect's <code>createSelector</code> function accepts one or more "input selector" functions, and an "output selector" function, and returns a new selector function for you to use.</p>

<p><code>createSelector</code> can accept multiple input selectors, which can be provided as separate arguments or as an array.  The results from all the input selectors are provided as separate arguments to the output selector:</p>

<pre><code>const selectA = state =&gt; state.a;
const selectB = state =&gt; state.b;
const selectC = state =&gt; state.c;

const selectABC = createSelector(
    [selectA, selectB, selectC],
    (a, b, c) =&gt; {
        // do something with a, b, and c, and return a result
        return a + b + c;
    }
);

// Call the selector function and get a result
const abc = selectABC(state);

// could also be written as separate arguments, and works exactly the same
const selectABC2 = createSelector(
    selectA, selectB, selectC,
    (a, b, c) =&gt; {
        // do something with a, b, and c, and return a result
        return a + b + c;
    }
);
</code></pre>

<p>When you call the selector, Reselect will run your input selectors with all of the arguments you gave, and looks at the returned values.  If any of the results are <code>===</code> different than before, it will re-run the output selector, and pass in those results as the arguments.  If all of the results are the same as the last time, it will skip re-running the output selector, and just return the cached final result from before.</p>

<p>In typical Reselect usage, you write your top-level "input selectors" as plain functions, and use <code>createSelector</code> to create memoized selectors that look up nested values:</p>

<pre><code>
const state = {
    a : {
        first : 5
    },
    b : 10
};


const selectA = state =&gt; state.a;
const selectB = state =&gt; state.b;

const selectA1 = createSelector(
    [selectA],
    a =&gt; a.first
);

const selectResult = createSelector(
    [selectA1, selectB],
    (a1, b) =&gt; {
        console.log("Output selector running");
        return a1 + b;
    }
);

const result = selectResult(state);
// Log: "Output selector running"
console.log(result);
// 15

const secondResult = selectResult(state);
// No log output
console.log(secondResult);
// 15
</code></pre>

<p>Note that the second time we called <code>selectResult</code>, the "output selector" didn't execute.  Because the results of <code>selectA1</code> and <code>selectB</code> were the same as the first call, <code>selectResult</code> was able to return the memoized result from the first call.</p>

<p>It's important to note that by default, Reselect only memoizes the most recent set of parameters.  That means that if you call a selector repeatedly with different inputs, it will still return a result, but it will have to keep re-running the output selector to produce the result:</p>

<pre><code>const a = someSelector(state, 1); // first call, not memoized
const b = someSelector(state, 1); // same inputs, memoized
const c = someSelector(state, 2); // different inputs, not memoized
const d = someSelector(state, 1); // different inputs from last time, not memoized
</code></pre>

<p>Also, you can pass multiple arguments into a selector.  Reselect will call all of the input selectors with those exact inputs:</p>

<pre><code>const selectItems = state =&gt; state.items;  
const selectItemId = (state, itemId) =&gt; itemId;  
  
const selectItemById = createSelector(  
    [selectItems, selectItemId],  
    (items, itemId) =&gt; items[itemId]  
);  

const item = selectItemById(state, 42);

/*
Internally, Reselect does something like this:

const firstArg = selectItems(state, 42);  
const secondArg = selectItemId(state, 42);  
  
const result = outputSelector(firstArg, secondArg);  
return result;  
*/
</code></pre>

<p>Because of this, it's important that all of the "input selectors" you provide should accept the same types of parameters.  Otherwise, the selectors will break.</p>

<pre><code>const selectItems = state =&gt; state.items;  

// expects a number as the second argument
const selectItemId = (state, itemId) =&gt; itemId;  

// expects an object as the second argument
const selectOtherField (state, someObject) =&gt; someObject.someField;  
  
const selectItemById = createSelector(  
    [selectItems, selectItemId, selectOtherField],  
    (items, itemId, someField) =&gt; items[itemId]  
);  
</code></pre>

<p>In this example, <code>selectItemId</code> expects that its second argument will be some simple value, while <code>selectOtherField</code> expects that the second argument is an object.  If you call <code>selectItemById(state, 42)</code>, <code>selectOtherField</code> will break because it's trying to access <code>42.someField</code>.</p>

<p><strong>You can (and probably <em>should</em>) use selector functions <em>anywhere</em> in your application that you access the state tree</strong>.  That includes <code>mapState</code> functions, thunks, sagas, observables, middleware, and even reducers.</p>

<p>Selector functions are frequently co-located with reducers, since they both know about the state shape.  However, it's up to you where you put your selector functions and how you organize them.</p>

<h2 id="optimizing-performance-with-reselect">Optimizing Performance With Reselect</h2>

<p>Let's go back to the "expensive <code>mapState</code>" example from earlier.  We really want to only execute that expensive logic when <code>state.someData</code> has changed.  Putting the logic inside a memoized selector will do that.</p>

<pre><code>const selectSomeData = state =&gt; state.someData;

const selectFilteredSortedTransformedData = createSelector(
    selectSomeData,
    (someData) =&gt; {
         const filteredData = expensiveFiltering(someData);
         const sortedData = expensiveSorting(filteredData);
         const transformedData = expensiveTransformation(sortedData);

         return transformedData;
    }
)

const mapState = (state) =&gt; {
    const transformedData = selectFilteredSortedTransformedData (state);

    return {data : transformedData};
}
</code></pre>

<p>This is a big performance improvement, for two reasons.</p>

<p>First, now the expensive transformation only occurs if <code>state.someData</code> is different.  That means if we dispatch an action that updates <code>state.somethingElse</code>, we won't do any real work in this <code>mapState</code> function.</p>

<p>Second, the React-Redux <code>connect</code> function determines if your real component should re-render based on the contents of the objects you return from <code>mapState</code>, using "shallow equality" comparisons.  If any of the fields returned are <code>===</code> different than the last time, then <code>connect</code> will re-render your component.  That means that you should avoid creating new references in a <code>mapState</code> function unless needed.  Array functions like <code>concat()</code>, <code>map()</code>, and <code>filter()</code> always return new array references, and so does the object spread operator.  By using memoized selectors, we can return the same references if the data hasn't changed, and thus skip re-rendering the real component.</p>

<h2 id="advanced-optimizations-with-react-redux">Advanced Optimizations with React-Redux</h2>

<p>There's a specific performance issue that can occur when you use memoized selectors with a component that can be rendered multiple times.</p>

<p>Let's say that we have this component definition:</p>

<pre><code>const mapState = (state, ownProps) =&gt; {
    const item = selectItemForThisComponent(state, ownProps.itemId);

    return {item};
}

const SomeComponent = (props) =&gt; &lt;div&gt;Name: {props.item.name}&lt;/div&gt;;

export default connect(mapState)(SomeComponent);

// later
&lt;SomeComponent itemId={1} /&gt;
&lt;SomeComponent itemId={2} /&gt;
</code></pre>

<p>In this example, <code>SomeComponent</code> is passing <code>ownProps.itemId</code> as a parameter to the selector.  When we render multiple instances of <code>&lt;SomeComponent&gt;</code>, each of those instances are sharing the same instance of the <code>selectItemForThisComponent</code> function.  That means that when an action is dispatched, each separate instance of <code>&lt;SomeComponent&gt;</code> will separately call the function, like:</p>

<pre><code>// first instance
selectItemForThisComponent(state, 1);
// second instance
selectItemForThisComponent(state, 2);
</code></pre>

<p>As described earlier, Reselect only memoizes on the most recent inputs (ie, it has a cache size of 1).  That means that <code>selectItemForThisComponent</code> will <em>never</em> memoize correctly, because it's never being called with the same inputs back-to-back.</p>

<p>This code will still run and work, but it's not fully optimized.  For the absolute best performance, we need a separate copy of <code>selectItemForThisComponent</code> for each instance of <code>&lt;SomeComponent&gt;</code>.</p>

<p><strong>The React-Redux <code>connect</code> function supports a special "factory function" syntax for <code>mapState</code> and <code>mapDispatch</code> functions, which can be used to create unique instances of selector functions for each component instance.</strong></p>

<p>If the first call to a <code>mapState</code> or <code>mapDispatch</code> function returns a function instead of an object, <code>connect</code> will use that returned function as the <em>real</em> <code>mapState</code> or <code>mapDispatch</code> function.  This gives you the ability to create component-instance-specific selectors inside the closure:</p>

<pre><code>const makeUniqueSelectorInstance = () =&gt; createSelector(
    [selectItems, selectItemId],
    (items, itemId) =&gt; items[itemId]
);    


const makeMapState = (state) =&gt; {
    const selectItemForThisComponent = makeUniqueSelectorInstance();

    return function realMapState(state, ownProps) {
        const item = selectItemForThisComponent(state, ownProps.itemId);

        return {item};
    }
};

export default connect(makeMapState)(SomeComponent);
</code></pre>

<p>Both component 1 and component 2 will get their own unique copies of <code>selectItemForThisComponent</code>, and each copy will get called with consistently repeatable inputs, allowing proper memoization.</p>

<h2 id="final-thoughts">Final Thoughts</h2>

<p>Like <a href="/2017/05/idiomatic-redux-tao-of-redux-part-2/" target="_blank">other common Redux usage patterns</a>, <strong>you are not required to use selector functions in a Redux app</strong>.  If you want to write deeply nested state lookups directly in your <code>mapState</code> functions or thunks, you can.  Similarly, you don't <em>have</em> to use the Reselect library to create selectors - you can just write plain functions if you want.</p>

<p>Having said that, <strong>you are encouraged to use selector functions, and to use the Reselect library for memoized selectors</strong>.  There's also many other options for creating selectors, including using functional programming utility libraries like lodash/fp and Ramda, and other alternatives to Reselect.  There's also <a href="https://github.com/markerikson/redux-ecosystem-links/blob/master/utilities.md#selectors" target="_blank">utility libraries that build on Reselect to handle specific use cases</a>.</p>

<h2 id="further-information">Further Information</h2>


  
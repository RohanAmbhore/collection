<a href="https://github.com/reduxjs/reselect/issues/259">https://github.com/reduxjs/reselect/issues/259</a><div id="articleHeader"><h1>              Multiple components using the same selector            #259    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/sht5" target="_blank">sht5</a>  opened this Issue
        <relative-time>on Jun 13, 2017</relative-time>
        · 11 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-235426405">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>i have a lot of components which are each connected (in their stateProps) to a certain selector(implemented with reselect, lets refer to it as selector A). every time one of selector A's params(also selectors lets refer to as A,B,C) changes,  selector A recalculates and is invoked separately for each connected component. as this calculation is intensive this costs me a lot in performance. is there a way to avoid this and calculate once for all?<br />
thanks</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-307999525">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Either I'm not understanding this right or I'm talking about a slightly different problem.you and the docs are talking about using a factory to allow each component to have its own memoization and 'personal' selector. In my case i have a lot of components which get the same props at the same time. The selector is calculated again and again for each component.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-307999813">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Can you give an example of how your selectors are defined?  The point of memoization is that <em>if</em> all the inputs are the same, then any calculations are skipped and the previously determined value is returned.</p>
<p>There's definitely something about your situation I'm not quite getting.  First you said that the inputs to SelectorA keep changing, then you said that "a lot of components get the same props at the same time".</p>
<p>Really need to see some code to better understand what's going on here.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-308000338">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <div>Ok I'll add some code when i get to the office</div>
<a href="#" target="_blank">…</a>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-308029039">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Hey,<br />
i made a gist here <a href="https://gist.github.com/sht5/d496d1c988e77e88daa8e453038b7eed" target="_blank">https://gist.github.com/sht5/d496d1c988e77e88daa8e453038b7eed</a><br />
start from things_selector file: the selector "FilteredThingIDsSelector" which depends on other selectors is used as a prop to different components in the app. they all use redux's mapStateToProps method as in the pageWithFilterPanelContainer component.<br />
when one of the filteredThingHierarchySelector ( which FilteredThingIDsSelector depends upon) params changes i see that the filteredThingHierarchySelector selector is called for each component that uses FilteredThingIDsSelector independently.<br />
I don't see why it should be called once for every component when the param changes once.<br />
please notice i'm using createDeepEqualSelector as in the documention with lodash's isEqual method. let me know if anything is unclear.<br />
thanks</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-308188339">

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/markerikson" target="_blank">markerikson</a>
  

    </strong>

    commented

    <a href="#issuecomment-308188339" target="_blank"><relative-time>on Jun 14, 2017</relative-time></a>


      
  •


  
    <summary>
      
          edited
      
      
    </summary>

    
  

  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Okay, I see your main problem.</p>
<p>You're calling <code>toJS()</code> in your "input selectors" such as <code>thingHierarchySelector</code>.  This is a <strong>BAD IDEA</strong> for several reasons.  It will return new object references <em>every</em> time it is called, <em>and</em> <code>toJS()</code> is the single most expensive operation in the Immutable.js API.  I have links to several articles discussing why calling <code>toJS()</code> should be avoided in the <a href="https://github.com/markerikson/react-redux-links/blob/master/react-performance.md#immutable-data" target="_blank">React Performance#Immutable Data</a> section of my <a href="https://github.com/markerikson/react-redux-links" target="_blank">React/Redux links list</a>.</p>
<p>The second problem is that you're not making good use of Reselect's memoization.  You could sorta get away with calling <code>toJS()</code> inside of your selectors, <em>if</em> they were properly memoized.  But, not only are most of your selectors <em>not</em> memoized, you're also doing multi-level lookups every time.  A properly memoized version of <code>thingsHierarchySelector</code> would look like:</p>
<div><pre>export const selectThingsReducer = state =&gt; state[consts.TOP_LEVEL_STATE_REDUCERS.THINGS_REDUCER];
const selectThingsHierarchy = createSelector(
    selectThingsReducer,
    (thingsReducer) =&gt; thingsReducer.get(consts.STATE_INNER_OBJECT_NAMES.THINGS_HIERARCHY)
);

const selectThingsHierarchyJS = createSelector(
    selectThingsHierarchy,
    (thingsHierarchy) =&gt; thingsHierarchy.toJS()
);</pre></div>
<p>Third, a stylistic issue that also relates to performance.  I see that you've copy-pasted code like <code>(state) =&gt; state[consts.TOP_LEVEL_STATE_REDUCERS.FILTERING_THING_CAPABILITIES_REDUCER]</code> in every selector.  That's very hard to read, and also doesn't help with memoization.  Instead, you should have one selector that encapsulates looking up that state field, and then re-use that selector as an input to all the others, like:</p>
<div><pre>export const selectFilteringReducer = (state) =&gt; state[consts.TOP_LEVEL_STATE_REDUCERS.FILTERING_THING_CAPABILITIES_REDUCER];

export const selectAllOfLeftNavSelectedFilters = createSelector(
    selectFilteringReducer,
    (filteringReducer) =&gt; filteringReducer.get(consts.STATE_INNER_OBJECT_NAMES.LEFT_NAV_SELECTED_FILTER_PATHS).toJS();
);

export const selectSelectedSearchBarTerm = createSelector(
    selectFilteringReducer,
    (filteringReducer) =&gt; filteringReducer.get(consts.STATE_INNER_OBJECT_NAMES.SEARCH_BAR_TERM).toJS();
);</pre></div>
<p>Finally, I also suspect you don't actually need to use the Lodash <code>deepEqual</code> check, if you make proper use of memoization and immutability.</p>
<p>So, ultimately this is an issue with improper use of selector functions and Reselect.  Restructuring your selector functions so that they actually are created using memoization will fix the problem.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-308204090">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <div>wow mark thanks so much for the analysis and help. much appreciated.
i think i will get rid of immutable.js completely, i'm using it heavily
around the app and it might be one of the causes i'm experiencing such bad
performance.
thanks</div>
<a href="#" target="_blank">…</a>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-308206109">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Yeah, I personally advise against use of Immutable.js in general (personal opinion).  <a href="https://www.reddit.com/r/javascript/comments/4rcqpx/dan_abramov_redux_is_not_an_architecture_or/d51g4k4?context=3" target="_blank">I wrote up my reasons in a Reddit comment a while back</a>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-308274778">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <div>Hey again mark,
I'm implementing your suggestions,
wanted to ask about replacing default memoize with a better function. when
is this actually effective? when my selector-inputs aren't primitive
objects ?
thanks</div>
<a href="#" target="_blank">…</a>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-308279615">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Ah... I think you may be confusing two different things.</p>
<p>The default <em>memoization</em> capability is to only save the last input+output seen by the function (ie, a cache size of 1).  You can change that by using <code>createSelectorCreator</code> and passing in your own memoization function instead of Reselect's <code>defaultMemoize</code>.</p>
<p>However, part of that memoization is the <em>comparison</em> process - "how do I decide if these two values are equal?".  If you do use <code>createSelectorCreator(defaultMemoize)</code>, you can also pass in a custom equality check function such as Lodash's <code>isEqual</code>, as you were doing in your example.</p>
<p>I personally don't see a need to change the default equality checking logic unless you have a <em>very</em> specific use case.  If you're writing an idiomatic Redux application, you should be doing immutable data updates and be able to compare values with reference checks, whether you're using plain JS objects and arrays or Immutable.js Maps and Lists.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-308438862">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <div>Great.
I implemented the changes last night and performance was improved
significantly!
Thanks again for taking the time to guide me, i can't thank you enough.</div>
<a href="#" target="_blank">…</a>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    

  
















        


        <div>
              
<div>
  

    
      



      <div>
        
          <div>
  


  
  <div>

    

    

        <p>
    
    
        Attach files by dragging & dropping,
        selecting them, or pasting
        from the clipboard.
    
    
    
    
    
    
    
    
    
  </p>


    
  </div>

  

  


  


          
      




        
      

    
    
  
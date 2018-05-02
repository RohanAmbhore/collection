<a href="https://github.com/ReactTraining/react-router/issues/4490">https://github.com/ReactTraining/react-router/issues/4490</a><div id="articleHeader"><h1>              Clarify how &lt;Switch&gt; works in docs            #4490    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/pshrmn" target="_blank">pshrmn</a>  opened this Issue
        <relative-time>on Feb 9, 2017</relative-time>
        · 6 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/pshrmn" target="_blank">pshrmn</a>
  

    </strong>

    commented

    <a href="#issue-206252035" target="_blank"><relative-time>on Feb 9, 2017</relative-time></a>


  </h3>
</div>


    

      
<table>
  <tbody>
    <tr>
      <td>

          <p>I have been seeing a decent bit of confusion about how the <code>&lt;Switch&gt;</code> component works. I think that this is a mixture of the docs not being explicit about how <code>&lt;Switch&gt;</code> matches routes and people not having a complete understanding of the <code>children</code> prop (it's a <em>thing</em> of elements?!)</p>
<p>There are two problems that seem to be common:</p>
<ol>
<li>Wrapping a <code>&lt;Route&gt;</code> and not including all of the props to the route wrapper that will be necessary for it to match.</li>
<li>Placing non-<code>&lt;Route&gt;</code> components in the <code>&lt;Switch&gt;</code>, for example to nest layouts.</li>
</ol>
<p>Generally I explain that the <code>&lt;Route&gt;</code> components will actually be React elements and should be thought of as a configuration array.</p>
<div><pre>&lt;Switch&gt;
  &lt;Route exact path='/' component={Home} /&gt;
  &lt;Route path='/faq' component={FAQ} /&gt;
  &lt;Route component={NoMatch} /&gt;
&lt;/Switch&gt;
// can be thought of as
&lt;Switch routes={[
  { path: '/', exact: true, component: Home },
  { path: '/faq', component; FAQ },
  { component: NoMatch }
]} /&gt;</pre></div>
<p>(A <code>routes</code> array is simpler than saying <code>React.Children.toArray(props.children)</code> and then specifying that you have to access the <code>props</code> property of each element.)</p>
<p>I'm not really sure what the best approach to explaining this is in the docs is, but I imagine until (and even after <g-emoji>🙄</g-emoji>) this gets clarified, there will continue to confusion about it.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    
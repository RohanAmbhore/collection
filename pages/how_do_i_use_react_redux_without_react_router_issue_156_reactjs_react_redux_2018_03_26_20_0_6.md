<a href="https://github.com/reactjs/react-redux/issues/156">https://github.com/reactjs/react-redux/issues/156</a><div id="articleHeader"><h1>              How do I use React redux without react router?            #156    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/ccorcos" target="_blank">ccorcos</a>  opened this Issue
        <relative-time>on Oct 14, 2015</relative-time>
        · 6 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-111299793">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>How does this provider stuff work?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  


          

          


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-148035282">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Hi <a href="https://github.com/ccorcos" target="_blank">@ccorcos</a>, have you seen <a href="http://rackt.github.io/redux/docs/basics/UsageWithReact.html" target="_blank">this?</a> Check out the Connecting to Redux section.</p>
<p>If that doesn't answer your question, could you be a little more specific?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-148145837">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p><code>&lt;Provider&gt;</code> puts <code>store</code> to be available on React <a href="http://facebook.github.io/react/docs/context.html" target="_blank">context</a>.<br />
It doesn't do anything else and isn't related to routing.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-148155128">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Interesting. I've had to deal with piping tons of props from a top-level component all the way through. I think using the splats with props is easy enough though...</p>
<p>If my understanding is correct, then I can create my own provider something like this:</p>
<div><pre>let Provider = React.createClass({
  componentWillMount: function() {
    this.unsubscribe = this.props.store.subscribe(() =&gt; {
      this.setState(this.props.store.getState())
    })
  },
  componentWillUnmount: function() {
    this.unsubscribe()
  },
  render: function() {
    let Component = this.props.component
    return (
      &lt;Component {...this.state}/&gt;
    )
  }
})

React.render(
  &lt;Provider store={store} component={App}/&gt;, 
  document.getElementById('root')
)</pre></div>
      </td>
    </tr>
  </tbody>
</table>


        



    

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-148177845">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I'm missing your point.</p>
<p>What you seem to be describing is what <code>connect()</code> does. <code>&lt;Provider&gt;</code> itself just puts <code>store</code> in context so <code>connect()</code> can read it regardless of how deeply nested the component is in view hierarchy. You can use <code>connect()</code> without <code>&lt;Provider&gt;</code> as long as you pass <code>store</code> down manually via props; <code>&lt;Provider&gt;</code> is what lets you avoid this manual threading.</p>
<p>What's your use case?</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-148223813">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Ah. I see. My use case is that I'm just trying to understand Redux. I want to know whats really going on before I use all these magical functions.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-148223936">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I think I get it now though. Provider just makes store available via context. And connect does all the subscription stuff, piping store.getState() to props.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  
















        


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

  

  


  


          
      




        
      

    
    
  
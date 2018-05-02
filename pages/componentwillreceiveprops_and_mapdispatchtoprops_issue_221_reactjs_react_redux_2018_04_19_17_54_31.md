<a href="https://github.com/reactjs/react-redux/issues/221">https://github.com/reactjs/react-redux/issues/221</a><div id="articleHeader"><h1>              componentWillReceiveProps and mapDispatchToProps            #221    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/iammerrick" target="_blank">iammerrick</a>  opened this Issue
        <relative-time>on Dec 18, 2015</relative-time>
        · 3 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      

  
    
      

          <p>I am running into an issue where componentWillReceiveProps is being called to early, namely before React Redux has had the opportunity to bind a different function based on the props passed. The previous function is still bound when componentWillReceiveProps is called. Take for example this component:</p>
<div><pre>const App = ReactRedux.connect((state, props) =&gt; ({
  name: props.userId ? state.user.name : state.group.groupName
}), (dispatch, props) =&gt; {
  return Redux.bindActionCreators({
    load: props.userId ? loadUser : loadGroup
  }, dispatch);
})(class extends React.Component {
  componentWillMount() {
    this.props.load();
  }
  componentWillReceiveProps() {
    this.props.load();
  }
  render() {
    return &lt;div&gt;Hello {this.props.name}!&lt;/div&gt;;
  }
});</pre></div>
<p>We want to bind a different function to load (based on the userId prop) and a different data to props based on the property provided. Unfortunately when componentWillReceiveProps is called, the old function is still bound to load. This can be "hacked" by introducing a setTimeout in your componentWillReceiveProps that makes sure the next component is actually bound.</p>
<p>I've made a full example of this on jsbin: <a href="http://jsbin.com/faqama/edit?html,js,output" target="_blank">http://jsbin.com/faqama/edit?html,js,output</a></p>
      
<a href="https://github.com/charliekassel/vuejs-datepicker/issues/399">https://github.com/charliekassel/vuejs-datepicker/issues/399</a><div id="articleHeader"><h1>              Cannot assign to read only property 'exports' of object '#&lt;Object&gt;'            #399    </h1></div>


  <div>
    
    <div>
        <a href="/Audiohiis" target="_blank">Audiohiis</a>  opened this Issue
        <relative-time>on Jan 24</relative-time>
        · 5 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-291108939">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I'm trying to use this package with Vue.js and it gives me this error, since I need to use 'import' on Vue side and package's build.js uses 'module.exports'.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  


          

          

  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-361290432">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Same here :/ This <a href="https://github.com/webpack/webpack/issues/4039" target="_blank">webpack/webpack#4039</a> seems to be relevant, but still didn't find solution for this.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-361331649">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/xpuu" target="_blank">xpuu</a>
  

    </strong>

    commented

    <a href="#issuecomment-361331649" target="_blank"><relative-time>on Jan 30</relative-time></a>


      
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

          <p>I got that working by disabling <code>//"plugins": ["transform-runtime"]</code> in <code>.babelrc</code> config in module directory. Also it's important to disable <code>//exclude: /node_modules/</code> in <code>webpack.config.js</code>. Still it'd be nice if someone more experienced could give some explanation to this issue. Thanks in advance.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  


  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-377736477">

    
<div>
  

    



  <h3>

    <strong>
      

  <a href="/codedge" target="_blank">codedge</a>
  

    </strong>

    commented

    <a href="#issuecomment-377736477" target="_blank"><relative-time>on Apr 1</relative-time></a>


      
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

          <p><a href="https://github.com/georgeevans1995" target="_blank">@georgeevans1995</a> cannot confirm that the comment you referenced fixed the issue :(</p>
<p>I solved it that way:<br />
<strong>.babelrc</strong></p>
<pre><code>{
  "presets": [
    ...
  ],
  "plugins": ["transform-runtime"]
}
</code></pre>
<p>Adding the <code>plugins</code> section with the <code>transform-runtime</code> package. After adding this a new error occured, see <a href="https://stackoverflow.com/questions/36313885/babel-6-transform-runtime-export-is-not-a-function" target="_blank">https://stackoverflow.com/questions/36313885/babel-6-transform-runtime-export-is-not-a-function</a>.</p>
<p>This error can be tackled the following way, solution taken from the SO thread.</p>
<p><strong>webpack.config.js</strong><br />
Exclude the <code>node-modules</code>:</p>
<pre><code>module.exports = {
    ...
    module: {
        rules: [
            {
                ...
            },
            {
                test: /\.js$/,
                loader: 'babel-loader',
                exclude: /node_modules/, // THAT IS THE IMPORTANT LINE
                include: [/src/, /node_modules\/semantic-ui-vue2/],
            },
            ...
         ]
    },
}
</code></pre>
<p>Hope that helps.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  







  
<div>
    
  <div>

  




  
<div>
    
  <div id="issuecomment-377736983">

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Another way how to exclude node_modules but one using regexp. This works correctly in both Linux and Windows environment.</p>
<div><pre>module: {
            rules: [
                ...
                {
                    test: /\.js$/,
                    loader: 'babel-loader',
                    // Exclude node_modules but MY_MODULE
                    exclude: /node_modules(?!(\/|\\)MY_MODULE)/,
                },
                ...
                },
            ]
        },</pre></div>
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

  

  


  


          
      




        
      

    
    
  
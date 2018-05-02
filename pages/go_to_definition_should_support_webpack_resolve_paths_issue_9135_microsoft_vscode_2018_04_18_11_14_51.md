<a href="https://github.com/Microsoft/vscode/issues/9135">https://github.com/Microsoft/vscode/issues/9135</a><div id="articleHeader"><h1>              Go To Definition should support Webpack resolve paths            #9135    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/methyl" target="_blank">methyl</a>  opened this Issue
        <relative-time>on Jul 12, 2016</relative-time>
        · 7 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      

  
    
      

          <p>Currently Go To Definition works perfectly well for relative paths within application, eg:</p>
<pre><code>import something from './something'
</code></pre>
<p>However, after I add some resolve paths in Webpack config, like</p>
<pre><code>  resolve: {
    root: [
      path.resolve(rootPath, 'app/frontend/lib'),
</code></pre>
<p>I can import files like this</p>
<pre><code>import something from 'something'
// instead of 
// import something from 'app/frontend/lib/something' or
// import something from '../../lib/something'
</code></pre>
<p>The problem is that VSCode won't follow these resolve paths.</p>
<p>The solution could be to add configuration which will define additional resolve paths for Go To Definition functionality.</p>
      
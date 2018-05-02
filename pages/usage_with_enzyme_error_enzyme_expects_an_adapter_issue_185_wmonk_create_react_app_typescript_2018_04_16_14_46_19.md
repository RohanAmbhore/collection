<a href="https://github.com/wmonk/create-react-app-typescript/issues/185">https://github.com/wmonk/create-react-app-typescript/issues/185</a><div id="articleHeader"><h1>              Usage with Enzyme, error: Enzyme expects an adapter            #185    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/QuantumInformation" target="_blank">QuantumInformation</a>  opened this Issue
        <relative-time>on Nov 6, 2017</relative-time>
        · 11 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      

  
    
      

          <p>I have the following setup</p>
<p><a href="https://user-images.githubusercontent.com/216566/32441178-490e0950-c2ee-11e7-8f0a-69fbdba7d69c.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://user-images.githubusercontent.com/216566/32441178-490e0950-c2ee-11e7-8f0a-69fbdba7d69c.png" alt="image" /></div></a></p>
<p>but get this error:</p>
<pre><code> Enzyme Internal Error: Enzyme expects an adapter to be configured, but found none. To
          configure an adapter, you should call `Enzyme.configure({ adapter: new Adapter() })`
          before using any of Enzyme's top level APIs, where `Adapter` is the adapter
          corresponding to the library currently being tested. For example:

          import Adapter from 'enzyme-adapter-react-15';
</code></pre>
<p>I get the same error if I rename to <code>setupTests.ts</code></p>
      
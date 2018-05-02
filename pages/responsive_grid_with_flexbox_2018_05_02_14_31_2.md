<a href="https://codepen.io/irinakramer/pen/jcLlp">https://codepen.io/irinakramer/pen/jcLlp</a><div id="articleHeader"><h1>Local Revisions</h1></div>
    <p id="local-history-message">
      Your browser has a more recent version of this Pen stored. Click the timestamp and save your Pen to save the new version.
    </p>
    
  
</aside>


  <div>

    <div>

      

      <div id="box-html">

        

        <div>
          <div><div><div><div><div><div><div><div><pre>&lt;html lang="en"&gt;</pre></div><div><pre>&lt;head&gt;</pre></div><div><pre>  &lt;meta charset="UTF-8" /&gt;</pre></div><div><pre>  &lt;title&gt;Flexbox responsive grid&lt;/title&gt;</pre></div><div><pre>&lt;/head&gt;</pre></div><div><pre>&lt;body&gt;</pre></div><div><pre>  &lt;div class="wrapper"&gt;</pre></div><div><pre>    &lt;p&gt;Responsive grid with Flexbox&lt;/p&gt;</pre></div><div><pre>  &lt;h1&gt;Basic Grid&lt;/h1&gt;</pre></div><div><pre>    &lt;p&gt;&lt;/p&gt;</pre></div><div><pre>  &lt;div class="Grid Grid--full u-textCenter"&gt;</pre></div><div><pre>    &lt;div class="Grid-cell"&gt;&lt;div class="Demo content-1of1"&gt;&lt;/div&gt;&lt;/div&gt;</pre></div><div><pre>  &lt;/div&gt;</pre></div><div><pre>  &lt;div class="Grid Grid--gutters Grid--cols-2 u-textCenter"&gt;</pre></div><div><pre>    &lt;div class="Grid-cell"&gt;&lt;div class="Demo content-1of2"&gt;&lt;/div&gt;&lt;/div&gt;</pre></div><div><pre>    &lt;div class="Grid-cell"&gt;&lt;div class="Demo content-1of2"&gt;&lt;/div&gt;&lt;/div&gt;</pre></div><div><pre>  &lt;/div&gt;</pre></div><div><pre>  &lt;div class="Grid Grid--gutters Grid--cols-3 u-textCenter"&gt;</pre></div><div><pre>    &lt;div class="Grid-cell"&gt;&lt;div class="Demo content-1of3"&gt;&lt;/div&gt;&lt;/div&gt;</pre></div><div><pre>    &lt;div class="Grid-cell"&gt;&lt;div class="Demo content-1of3"&gt;&lt;/div&gt;&lt;/div&gt;</pre></div><div><pre>    &lt;div class="Grid-cell"&gt;&lt;div class="Demo content-1of3"&gt;&lt;/div&gt;&lt;/div&gt;</pre></div><div><pre>  &lt;/div&gt;</pre></div>
          
        

      


      


      <div id="box-css">

        

        <div>
          <div><div><div><div><div><div><div><div><pre>@import "compass/css3";</pre></div><div><pre>​</pre></div><div><pre>// VARIALBLES</pre></div><div><pre>// Demo colors:</pre></div><div><pre>$demoMain: rgba(51, 153, 204,.2);</pre></div><div><pre>$demoMainDark: rgba(51, 153, 204,.6);</pre></div><div><pre>$demoBorder: #33cccc;</pre></div><div><pre>$demoHolly: rgba(102, 51, 255, 0.1);</pre></div><div><pre>$demoHollyDark: rgba(102, 51, 255, 0.25);</pre></div><div><pre>​</pre></div><div><pre>​</pre></div><div><pre>body {</pre></div><div><pre>  color: #404040;</pre></div><div><pre>  font: 100 1em/150% "proxima-nova", Helvetica, sans-serif;</pre></div><div><pre>}</pre></div><div><pre>​</pre></div><div><pre>.wrapper{</pre></div><div><pre>  max-width: 1200px;</pre></div><div><pre>  margin: auto;</pre></div><div><pre>  //border: 1px solid red;</pre></div><div><pre>}</pre></div><div><pre>​</pre></div><div><pre>h1, h2, h3, h4 {  </pre></div>
          
        

      


      


      

    

    <div id="resizer"><div id="width-readout">999px</div>

    

  



  





  




  
  

  


  

  



  
  

  




  





<div><h3>Like On Github</h3><div><div>*Title (label for the link)</div><div><div>*Comment (commit message)</div><div id="action-btns"><div id="logh_btn_save">Saving...</div><div id="logh_btn_cancel">Cancel</div>
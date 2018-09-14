<a href="http://grid.malven.co/">http://grid.malven.co/</a><div id="articleHeader"><h1>A simple visual cheatsheet for CSS Grid Layout</h1></div>

<div>
    

  <div>container</div>
  
  
  <section>
    <h2>display</h2>
    <p>Establishes a new grid formatting context for children.</p>
    <div>
      


<div>
  
  
  <h3>display: grid;</h3>
</div>
      


<div>
  
  
  <h3>display: inline-grid;</h3>
</div>
      


<div>
  
  
  <h3>display: subgrid;</h3>
</div>
    </div>
  </section>
  
  
  <section>
    <h2>grid-template</h2>
    <p>Defines the rows and columns of the grid.</p>
    <div>
      


<div>
  
  
  <h3>grid-template-columns: 12px 12px 12px;<br />grid-template-rows: 12px 12px 12px;</h3>
</div>
      


<div>
  
  
  <h3>grid-template-columns: repeat(3, 12px);<br />grid-template-rows: repeat(3, auto);</h3>
</div>
      


<div>
  
  
  <h3>grid-template-columns: 8px auto 8px;<br />grid-template-rows: 8px auto 12px;</h3>
</div>
      


<div>
  
  
  <h3>grid-template-columns: 22% 22% auto;<br />grid-template-rows: 22% auto 22%;</h3>
</div>
    </div>
  </section>
  
  
  <section>
    <h2>grid-gap</h2>
    <p>Specifies the size of column and row gutters.</p>
    <div>
      


<div>
  
  
  <h3>grid-row-gap: 1px;<br />grid-column-gap: 9px;</h3>
</div>
      


<div>
  
  
  <h3>grid-gap: 1px 9px;</h3>
</div>
      


<div>
  
  
  <h3>grid-gap: 6px;</h3>
</div>
    </div>
  </section>
  
  
  <section>
    <h2>justify-items</h2>
    <p>Aligns content in a grid item along the row axis.</p>
    <div>
      


<div>
  
  
  <h3>justify-items: start;</h3>
</div>
      


<div>
  
  
  <h3>justify-items: end;</h3>
</div>
      


<div>
  
  
  <h3>justify-items: center;</h3>
</div>
      


<div>
  
  
  <h3>justify-items: stretch; (default)</h3>
</div>
    </div>
  </section>
  
  
  <section>
    <h2>align-items</h2>
    <p>Aligns content in a grid item along the column axis.</p>
    <div>
      


<div>
  
  
  <h3>align-items: start;</h3>
</div>
      


<div>
  
  
  <h3>align-items: end;</h3>
</div>
      


<div>
  
  
  <h3>align-items: center;</h3>
</div>
      


<div>
  
  
  <h3>align-items: stretch; (default)</h3>
</div>
    </div>
  </section>
  
  
  <section>
    <h2>justify-content</h2>
    <p>Justifies all grid content on row axis when total grid size is smaller than container.</p>
    <div>
      


<div>
  
  
  <h3>justify-content: start;</h3>
</div>
      


<div>
  
  
  <h3>justify-content: end;</h3>
</div>
      


<div>
  
  
  <h3>justify-content: center;</h3>
</div>
      


<div>
  
  
  <h3>justify-content: stretch;</h3>
</div>
      


<div>
  
  
  <h3>justify-content: space-around;</h3>
</div>
      


<div>
  
  
  <h3>justify-content: space-between;</h3>
</div>
      


<div>
  
  
  <h3>justify-content: space-evenly;</h3>
</div>
    </div>
  </section>
  
  
  <section>
    <h2>align-content</h2>
    <p>Justifies all grid content on column axis when total grid size is smaller than container.</p>
    <div>
      


<div>
  
  
  <h3>align-content: start;</h3>
</div>
      


<div>
  
  
  <h3>align-content: end;</h3>
</div>
      


<div>
  
  
  <h3>align-content: center;</h3>
</div>
      


<div>
  
  
  <h3>align-content: stretch;</h3>
</div>
      


<div>
  
  
  <h3>align-content: space-around;</h3>
</div>
      


<div>
  
  
  <h3>align-content: space-between;</h3>
</div>
      


<div>
  
  
  <h3>align-content: space-evenly;</h3>
</div>
    </div>
  </section>
  
  
  <section>
    <h2>grid-auto-flow</h2>
    <p>Algorithm for automatically placing grid items that aren't explictly placed.</p>
    <div>
      


<div>
  
  
  <h3>grid-auto-flow: row;</h3>
</div>
      


<div>
  
  
  <h3>grid-auto-flow: column;</h3>
</div>
      


<div>
  
  
  <h3>grid-auto-flow: dense;</h3>
</div>
    </div>
  </section>
  
  <div>children</div>
  
  
  <section>
    <h2>grid-column</h2>
    <p>Determines an items column-based location within the grid.</p>
    <div>
      


<div>
  
  
  <h3>grid-column-start: 1;<br />grid-column-end: 3;</h3>
</div>
      


<div>
  
  
  <h3>grid-column-start: span 3;</h3>
</div>
      


<div>
  
  
  <h3>grid-column-start: 2;<br />grid-column-end: 4;</h3>
</div>
      


<div>
  
  
  <h3>grid-column: 2 / 3</h3>
</div>
      


<div>
  
  
  <h3>grid-column: 2 / span 2</h3>
</div>
    </div>
  </section>
  
  
  <section>
    <h2>grid-row</h2>
    <p>Determines an items row-based location within the grid.</p>
    <div>
      


<div>
  
  
  <h3>grid-row-start: 1;<br />grid-row-end: 3;</h3>
</div>
      


<div>
  
  
  <h3>grid-row-start: span 3;</h3>
</div>
      


<div>
  
  
  <h3>grid-row-start: 2;<br />grid-row-end: 4;</h3>
</div>
      


<div>
  
  
  <h3>grid-row: 1 / 3;</h3>
</div>
      


<div>
  
  
  <h3>grid-row: 1 / span 3;</h3>
</div>
    </div>
  </section>
  
  
  <section>
    <h2>grid-row + grid-column</h2>
    <p>Combining grid rows with grid columns.</p>
    <div>
      


<div>
  
  
  <h3>grid-row: 1 / span 2;<br />grid-column: 1 / span 2;</h3>
</div>
      


<div>
  
  
  <h3>grid-row: 2 / span 2;<br />grid-column: 2 / span 2;</h3>
</div>
    </div>
  </section>
  
  
  <section>
    <h2>justify-self</h2>
    <p>Aligns content for a specific grid item along the row axis.</p>
    <div>
      


<div>
  
  
  <h3>justify-self: start;</h3>
</div>
      


<div>
  
  
  <h3>justify-self: end;</h3>
</div>
      


<div>
  
  
  <h3>justify-self: center;</h3>
</div>
      


<div>
  
  
  <h3>justify-self: stretch; (default)</h3>
</div>
    </div>
  </section>
  
  
  <section>
    <h2>align-self</h2>
    <p>Aligns content for a specific grid item along the column axis.</p>
    <div>
      


<div>
  
  
  <h3>align-self: start;</h3>
</div>
      


<div>
  
  
  <h3>align-self: end;</h3>
</div>
      


<div>
  
  
  <h3>align-self: center;</h3>
</div>
      


<div>
  
  
  <h3>align-self: stretch; (default)</h3>
</div>
    </div>
  </section>

  <footer>
    <p>GRID was created by <a href="https://malven.co" target="_blank">Malven Co.</a> an interactive design + development shop.</p>

    <p>Want more like this? Check out <a href="http://flexbox.malven.co" target="_blank">FLEX</a></p>
  </footer>
</div>










<div id="notie-alert-outer"><div id="notie-alert-inner"><div id="notie-alert-content">The code was copied to your clipboard.</div></div></div><div><h3>Like On Github</h3><div><div>*Title (label for the link)</div></div><div><div>*Comment (commit message)</div></div><div id="action-btns"><div id="logh_btn_save">Saving...</div><div id="logh_btn_favorite">Favorite</div><div id="logh_btn_cancel">Cancel</div></div></div>
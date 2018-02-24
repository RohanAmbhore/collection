<a href="https://www.bootply.com/130682">https://www.bootply.com/130682</a><div id="articleHeader"><h1>Bootstrap textbox clear snippet</h1></div>
    <div>
        <div>
            <div><code>javascript</code></div>
            <div><div><div><div><div><div><pre>1</pre><pre>2</pre><pre>3</pre><pre>4</pre><pre>5</pre><pre>6</pre><pre>7</pre><pre>8</pre><pre>9</pre><pre>10</pre><pre>11</pre></div></div><div><div><div><pre>$(".hasclear").keyup(function () {</pre><pre>  var t = $(this);</pre><pre>  t.next('span').toggle(Boolean(t.val()));</pre><pre>});</pre><pre>$(".clearer").hide($(this).prev('input').val());</pre><pre>$(".clearer").click(function () {</pre><pre>  $(this).prev('input').val('').focus();</pre><pre>  $(this).hide();</pre><pre>});</pre></div></div></div></div></div></div></div>
        </div>
        <div>
            <div><code>css</code></div>
            <div><div><div><div><div><div><pre>1</pre></div></div><div><div><div><pre>x</pre></div></div></div></div></div></div></div>
        </div>
    </div>
    <div id="htmlPane">
        
        
        <div><code>html</code></div>
        <div><div><div><div><div><div><pre>1</pre><pre>2</pre><pre>3</pre><pre>4</pre><pre>5</pre><pre>6</pre><pre>7</pre><pre>8</pre><pre>9</pre><pre>10</pre><pre>11</pre><pre>12</pre><pre>13</pre><pre>14</pre><pre>15</pre><pre>16</pre><pre>17</pre><pre>18</pre><pre>19</pre><pre>20</pre><pre>21</pre><pre>22</pre><pre>23</pre><pre>24</pre><pre>25</pre></div></div><div><div><div><pre>        &lt;span class="clearer glyphicon glyphicon-remove-circle form-control-feedback"&gt;&lt;/span&gt;</pre></div><div><pre>&lt;div class="container"&gt;</pre><pre>  &lt;form class="form-horizontal"&gt;</pre><pre>    &lt;div class="form-group has-feedback"&gt;</pre><pre>      &lt;label for="txt1" class="col-sm-2 control-label"&gt;Label 1&lt;/label&gt;</pre><pre>      &lt;div class="col-sm-10"&gt;</pre><pre>        &lt;input id="txt1" type="text" class="form-control hasclear" placeholder="Textbox 1"&gt;</pre><pre>        &lt;span class="clearer glyphicon glyphicon-remove-circle form-control-feedback"&gt;&lt;/span&gt;</pre><pre>      &lt;/div&gt;</pre><pre>    &lt;/div&gt;</pre><pre>    &lt;div class="form-group has-feedback"&gt;</pre><pre>      &lt;label for="txt2" class="col-sm-2 control-label"&gt;Label 2&lt;/label&gt;</pre><pre>        &lt;div class="col-sm-10"&gt;</pre><pre>          &lt;input id="txt2" type="text" class="form-control hasclear" placeholder="Textbox 2"&gt;</pre><pre>          &lt;span class="clearer glyphicon glyphicon-remove-circle form-control-feedback"&gt;&lt;/span&gt;</pre><pre>        &lt;/div&gt;</pre><pre>    &lt;/div&gt;</pre><pre>    &lt;div class="form-group has-feedback"&gt;</pre><pre>      &lt;label for="txt3" class="col-sm-2 control-label"&gt;Label 3&lt;/label&gt;</pre><pre>      &lt;div class="col-sm-10"&gt;</pre><pre>        &lt;input id="txt3" type="text" class="form-control hasclear" placeholder="Textbox 3"&gt;</pre><pre>        &lt;span class="clearer glyphicon glyphicon-remove-circle form-control-feedback"&gt;&lt;/span&gt;</pre><pre>      &lt;/div&gt;   </pre><pre>    &lt;/div&gt;</pre><pre>  &lt;/form&gt;</pre><pre>&lt;/div&gt;</pre></div></div></div></div></div></div></div>
        
        
        
	</div>

<a href="https://github.com/elastic/elasticsearch-rails/issues/761">https://github.com/elastic/elasticsearch-rails/issues/761</a><div id="articleHeader"><h1>              Failed to parse value [not_analyzed] as only [true] or [false] are allowed.            #761    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/nrvakil" target="_blank">nrvakil</a>  opened this Issue
        <relative-time>on Dec 14, 2017</relative-time>
        · 2 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        


          


    
  

    





      
  

    



    
      
<table>
  <tbody>
    <tr>
      <td>
          <p>I get the following error:</p>
<div><pre>Elasticsearch::Transport::Transport::Errors::BadRequest: [400] {"error":{"root_cause":[{"type":"mapper_parsing_exception","reason":"Failed to parse mapping [note]: Could not convert [raw.index] to boolean"}],"type":"mapper_parsing_exception","reason":"Failed to parse mapping [note]: Could not convert [raw.index] to boolean","caused_by":{"type":"illegal_argument_exception","reason":"Could not convert [raw.index] to boolean","caused_by":{"type":"illegal_argument_exception","reason":"Failed to parse value [not_analyzed] as only [true] or [false] are allowed."}}},"status":400}</pre></div>
<p>Model: (ploymorphic)</p>
<div><pre>class Note &lt; ApplicationRecord
  include Elasticsearch::Model
  include Elasticsearch::Model::Callbacks

  mappings dynamic: 'false' do
      indexes :noteable_type, type: 'text', index: :not_analyzed
  end
 
  # ...
end

Note.__elasticsearch__.create_index! force: true</pre></div>
<p>Am am I doing something wrong? Or some syntax has changed again? Please help. Thanks.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    
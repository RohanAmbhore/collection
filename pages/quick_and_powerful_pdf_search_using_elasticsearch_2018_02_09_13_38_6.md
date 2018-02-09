<a href="https://qbox.io/blog/powerful-pdf-search-elasticsearch-mapper-attachment">https://qbox.io/blog/powerful-pdf-search-elasticsearch-mapper-attachment</a><div id="articleHeader"><h1>Quick and Powerful PDF Search Using Elasticsearch</h1></div>
                  <p>Are you looking for full-text search and highlight capability on .PDF, .doc, or .epub files that you have in your system? In this tutorial, we show you how with the mapper-attachment-plugin</p>

        <p>This tutorial is for pre-5.x elasticsearch scenarios.  For 5.x and on, see this tutorial on <a href="https://qbox.io/blog/how-to-index-attachments-and-files-to-elasticsearch-5-0-using-ingest-api?utm_source=qbox.io&utm_medium=article&utm_campaign=powerful-pdf-search-elasticsearch-mapper-attachment" target="_blank">how to index attachments and files to elasticsearch using the Ingest API</a>.</p>
<h3>Mapper Attachment Plugin</h3>
<p>Mapper attachment plugin is a plugin available for Elasticsearch to index different type of files such as PDFs, .epub, .doc, etc. This plugin uses the open source Apache Tika libraries for the text extraction purposes.</p>
<p>Try out the plugin and make a pdf document to be indexed and made searchable. Here is how document is indexed using this plugin in elasticsearch:</p>
<p><strong><strong><div class="readableLargeImageContainer"><img src="https://qbox.io/img/blog/pdf-to-elasticsearch.png" alt="pdf-to-elasticsearch.png#asset:1529" /></div></strong></strong></p>
<p>As you can see from above, the JSON document is first converted to base64 format using any code, and then passed to the elasticsearch (plugin part). Now the required parser library is selected and applied to the document to extract its text and metadata, and then indexed to elasticsearch. </p>
<h3>Plugin Installation</h3>
<p>The plugin can be installed using the command below:</p>
<pre>bin/plugin install elasticsearch/elasticsearch-mapper-attachments/github</pre>
<p>The above command is for the installation of the plugin for Elasticsearch 2.3.3. For other versions, you can look up to the plugin's Github repo<a href="https://github.com/elastic/elasticsearch-mapper-attachments" target="_blank"> here</a>.</p>
<h3>Applying the Mapping</h3>
<p>It is not enough to install the plugin and then pass the document to the elasticsearch as base64. We need to specify in the type mapping that the specified index type contains files like .pdf, .doc, etc., as attached to it. To do this we need to apply the mapping to the required type of the index as below:</p>
<pre>curl -X PUT "&lt;a&gt;http://$hostname:9200/pdf-test&lt;/a&gt;" -d '{
 "mappings": {
   "person": {
     "properties": {
       "file": {
         "type": "attachment",
         "fields": {
           "content": {
             "store": "yes"
           },
           "title": {
             "store": "yes"
           },
           "date": {
             "store": "yes"
           },
           "author": {
             "store": "yes"
           },
           "keywords": {
             "store": "yes"
           },
           "content_type": {
             "store": "yes"
           },
           "content_length": {
             "store": "yes"
           },
           "language": {
             "store": "yes"
           }
         }
       }
     }
   }
 }
}'</pre>
<p>Here we have defined mapping for the type named <code>"person"</code> under which you can see the <code>"file"</code> is given the type <code>"attachment"</code>.   </p>
<h3>Indexing Files</h3>
<p>As we said earlier, the document to be indexed is to be converted to the base64 format. You can employ any familiar language for the process. In the below code, we have used a Perl script for doing that, and then it is indexed to the elasticsearch index, too:</p>
<pre>encodedPdf=`cat testDocument.pdf | perl -MMIME::Base64 -ne 'print encode_base64($_)'`
json="{\"file\":\"${encodedPdf}\"}"
echo "$json" &gt; json.file
curl -X POST "localhost:9200/pdf-/test/person/" -d @json.file
Searching on the pdf</pre>
<p><strong>Check out our <a href="https://supergiant.io/solutions" target="_blank">Kubernetes Development Support Packages</a></strong></p>
<p>The extracted content is indexed and mapped as string type under the <code>"fields"</code> under the field <code>"content"</code>.  When we are querying for data present in the file, we should use the same field. A sample query is as below:</p>
<pre>curl -XPOST&lt;a href="http://localhost:9200/pdf-test/_search"&gt; http://localhost:9200/pdf-test/_search&lt;/a&gt; -d '{
 "from": 0,
 "fields": [
   "file.content"
 ],
 "query": {
   "match": {
     "file.content": "Easy"
   }
 },
 "highlight": {
   "fields": {
     "file.content": {}
   }
 }
}'</pre>
<p>The response for the above query would have the the search keyword (here <code>"Easy"</code>) in the "content" field. Also, since the highlighting is used in the above query, it will be given inside the <code>&lt;em&gt;</code> tag under the <code>"highlight"</code> field of the response. </p>
<h3>Default Limit in Character Extraction</h3>
<p>Sometimes when we index a large PDF file, there is a chance that indexing might not happen due to the limitation in the number of characters that can be extracted. By default, a maximum of 100,000 characters are extracted. Any exceeding of this limit will result in an extraction error. This can be overcome by changing the settings, like below:</p>
<pre>index.mapping.attachment.indexed_chars : -1</pre>
<p>This would allow for an unlimited extracted characters. </p>
<h3>Ingest Attachment Plugin</h3>
<p>Mapper attachment plugin is deprecated for the new release (5 and above) of Elasticsearch. It is replaced with a similar plugin named <a href="https://qbox.io/blog/how-to-index-attachments-and-files-to-elasticsearch-5-0-using-ingest-api?utm_source=qbox.io&utm_medium=article&utm_campaign=powerful-pdf-search-elasticsearch-mapper-attachment" target="_blank">ingest attachment plugin</a>. The IAP also uses the Apache Tika libraries, and the usage is similar. For more information you can refer to the documentation<a href="https://www.elastic.co/guide/en/elasticsearch/plugins/5.x/ingest-attachment.html" target="_blank"> here</a>.</p>
<h3>Conclusion</h3>
<p>In this tutorial, we covered how to index commonly used file types (PDF in this case) in elasticsearch using the mapper-attachment plugin. We also executed a full text search and highlighted the results on the indexed PDF document.  </p>

        <aside id="article-end-form-container">
  <h3>Get the Next Article</h3>

  <div>
    <div>
      <p>Sign up for our newsletter, and don't miss out on our top articles.</p>

      
      
        

        </div>

    
  </div>

  

</aside>

        

        
            
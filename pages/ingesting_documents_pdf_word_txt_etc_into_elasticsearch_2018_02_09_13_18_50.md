<a href="https://blog.ambar.cloud/ingesting-documents-pdf-word-txt-etc-into-elasticsearch/">https://blog.ambar.cloud/ingesting-documents-pdf-word-txt-etc-into-elasticsearch/</a><div id="articleHeader"><h1>Ingesting Documents (pdf, word, txt, etc) Into ElasticSearch</h1></div>

        <section>
            <p>ElasticSearch is a great tool for full-text search over billions of records. But what if you want to search through files with help of ElastricSearch? How should you extract and index files? After googling for <em>"ElasticSearch searching PDFS"</em>, <em>"ElasticSearch index binary files"</em> I didn't find any suitable solution, so I decided to make this post about available options.</p>

<h4 id="ingestattachmentplugin">Ingest Attachment Plugin</h4>

<p><em><a href="https://www.elastic.co/guide/en/elasticsearch/plugins/master/ingest-attachment.html" target="_blank">Official site</a></em></p>

<p>The simplest and easy to use solution is Ingest Attachment. It's a plugin for ElasticSearch that extracts content from almost all document types (thanks Tika). It's a good choice for a quick start. Ingest Attachment can't be fine tuned, and that's why it can't handle large files. We post about pitfalls of Ingest Attachment before, read it <a href="https://blog.ambar.cloud/ingest-attachment-plugin-for-elasticsearch-should-you-use-it/" target="_blank">here</a>. <br />
Installation process is straightforward, check out official ElasticSearch site for details.</p>

<h4 id="apachetika">Apache Tika</h4>

<p><em><a href="https://tika.apache.org/" target="_blank">Official site</a></em></p>

<p>Apache Tika is a de-facto standard for extracting content from files. Roughly speaking, Tika is a combination of open-source libraries that extract files content, joined into a single library. It's open source and it has a REST API. You have to be experienced to setup and configure it on your server. For example, I had issues with setting up Tesseract to do OCR inside Tika. Also you should notice that Tika doesn't work well with some kinds of PDFs (the ones with images inside) and REST API works much slower than direct Java calls, even on localhost.</p>

<p>So, you installed Tika, what's next? You need to create some kind of wrapper that:</p>

<ol>
<li>Downloads a file  </li>
<li>Calls Tika to extract file content  </li>
<li>Submits parsed content to ElasticSearch</li>
</ol>

<p>To make ElasticSearch search fast through large files you have to tune it yourself. Details in <a href="https://blog.ambar.cloud/highlighting-large-documents-in-elasticsearch/" target="_blank">this</a> and <a href="https://blog.ambar.cloud/making-elasticsearch-perform-well-with-large-text-fields/" target="_blank">this</a> posts.</p>

<p>To sum up, Tika is a great solution but it requires a lot of code-writing and fine-tuning, especially for edge cases: for Tika it's weird PDF's and OCR.</p>

<h4 id="fscrawler">FsCrawler</h4>

<p><em><a href="https://github.com/dadoonet/fscrawler" target="_blank">GitHub</a></em></p>

<p>FsCrawler is a "quick and dirty" open-source solution for those who wants to index documents from their local filesystem and over SSH. It crawls your filesystem and indexes new files, updates existing ones and removes old ones. FsCrawler is written in Java and requires some additional work to install and configure it. It supports scheduled crawling (e.g. every 15 minutes), also it has some basic API for submitting files and schedule management. FsCrawler uses Tika inside, and generally speaking you can use FsCrawler as a glue between Tika and ElasticSearch.</p>

<h4 id="ambar">Ambar</h4>

<p><em><a href="https://ambar.cloud" target="_blank">Official site</a>, <a href="https://github.com/RD17/ambar" target="_blank">GitHub</a></em></p>

<p>After dealing with every solution described above, we decided to create our own enterprise-ready solution. Ambar includes all the best from existing solutions, and adds some cool new features. </p>

<ul>
<li>It handles large files (&gt;100 MB) well</li>
<li>It extracts content from PDF (even poorly formatted and with embedded images) and does OCR on images</li>
<li>It provides user with simple and easy to use REST API and WEB UI</li>
<li>It is extremely easy to deploy (thanks Docker)</li>
<li>It is open-sourced under Fair Source 1 v0.9 license</li>
<li>Provides user with parse and instant search experience out-of-the box</li>
</ul>

<p>The details on how Ambar works are <a href="https://blog.ambar.cloud/ambar-under-the-hood/" target="_blank">here</a>.</p>

<p>That's it! Hope you can select one option that suits you best.</p>
        </section>

        <footer>


            

            


            <section>
                <h4>Share this post</h4>
                
                                                
            </section>

            
            
            
                                

            <section>
                <h3>Subscribe to Ambar Blog. How we made your docs searchable</h3>
                <p>Get the latest posts delivered right to your inbox.</p>
                
    

    
    
    



                or subscribe <a href="http://cloud.feedly.com/#subscription/feed/http://blog.ambar.cloud/rss/" target="_blank">via RSS</a> with Feedly!
            </section>

        </footer>

    
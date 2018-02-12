<a href="https://discuss.elastic.co/t/fetching-position-of-keyword-in-matched-document/94291/2">https://discuss.elastic.co/t/fetching-position-of-keyword-in-matched-document/94291/2</a><div id="articleHeader"><h1>Fetching position of keyword in matched document</h1></div>
    





    

    

      


















      

    <section id="main">
    <div id="ember682">




<div id="main-outlet">
  <div>
      <div id="ember731"><div id="rtp-container"><header>
<pre><strong>Community Newsletter:  </strong><a href="https://www.elastic.co/community/newsletter?baymax=rtp&elektra=discuss&iesrc=ctr" target="_blank">Sign-up and Learn More</a></pre>
</header></div>
</div>
    
    
  </div>
  <div id="ember749">    
    <div>
      <div id="ember761">  <div>
    <div id="banner">
      
      <div id="banner-content">
        <p><strong>Elastic Stack 6.2.0 released</strong></p>
<p>Hi all,</p>
<p>We’ve just released version 6.2.0 of the Elastic Stack. Plus, <a href="https://www.elastic.co/blog/elastic-apm-ga-released" target="_blank">Elastic APM is now GA</a>.</p>
<p>Learn more about the latest and greatest in the blog posts:</p><aside>
  <header>
      <img src="https://www.elastic.co/favicon-32x32.png" width="32" height="32" />
      <a href="https://www.elastic.co/blog/elastic-stack-6-2-0-released" title="06:28PM - 06 February 2018" target="_blank">Elastic Blog – 6 Feb 18</a>
  </header>
  <article>
    

<h3><a href="https://www.elastic.co/blog/elastic-stack-6-2-0-released" target="_blank">Elastic Stack 6.2.0 Released
	  	 | Elastic</a></h3>

<p>6.2.0 is here. Never one to pause adding features to software, we are pleased to introduce you to the capabilities of 6.2.0. You should download it now or use it on Elastic Cloud (your favourite hoste...</p>


  </article>
  
  
</aside>
<br />
<aside>
  <header>
      <img src="https://www.elastic.co/favicon-32x32.png" width="32" height="32" />
      <a href="https://www.elastic.co/blog/elasticsearch-6-2-0-released" title="02:23PM - 06 February 2018" target="_blank">Elastic Blog – 6 Feb 18</a>
  </header>
  <article>
    

<h3><a href="https://www.elastic.co/blog/elasticsearch-6-2-0-released" target="_blank">Elasticsearch 6.2.0 released</a></h3>

<p>Today we are pleased to announce the release of Elasticsearch 6.2.0, based on Lucene 7.2.1. This is the latest stable release, and is already available for deployment on Elastic Cloud, our Elasticsearch-as-a-service platform.</p>


  </article>
  
  
</aside>
<br />
<aside>
  <header>
      <img src="https://www.elastic.co/favicon-32x32.png" width="32" height="32" />
      <a href="https://www.elastic.co/blog/kibana-6-2-0-released" title="02:30PM - 06 February 2018" target="_blank">Elastic Blog – 6 Feb 18</a>
  </header>
  <article>
    

<h3><a href="https://www.elastic.co/blog/kibana-6-2-0-released" target="_blank">Kibana 6.2.0 is released
	  	 | Elastic</a></h3>

<p>Welcome to the 6.2.0 release of Kibana! It’s Kibana release time again, and you’re gonna like this one. It has some hotly anticipated features. Download Kibana 6.2.0 Kibana 6.2.0 release not...</p>


  </article>
  
  
</aside>
<br />
<aside>
  <header>
      <img src="https://www.elastic.co/favicon-32x32.png" width="32" height="32" />
      <a href="https://www.elastic.co/blog/logstash-6-2-0-released" title="05:00PM - 06 February 2018" target="_blank">Elastic Blog – 6 Feb 18</a>
  </header>
  <article>
    

<h3><a href="https://www.elastic.co/blog/logstash-6-2-0-released" target="_blank">Logstash 6.2.0 Released
	  	 | Elastic</a></h3>

<p>Logstash 6.2.0 has been released, and it is bringing lots of new goodies. Please refer to the release notes for a complete list. You can download Logstash 6.2.0 from our downloads page. If you are upg...</p>


  </article>
  
  
</aside>
<br />
<aside>
  <header>
      <img src="https://www.elastic.co/favicon-32x32.png" width="32" height="32" />
      <a href="https://www.elastic.co/blog/beats-6-2-0-released" title="04:00PM - 06 February 2018" target="_blank">Elastic Blog – 6 Feb 18</a>
  </header>
  <article>
    

<h3><a href="https://www.elastic.co/blog/beats-6-2-0-released" target="_blank">Beats 6.2.0 released
	  	 | Elastic</a></h3>

<p>We’re pleased to announce the Beats 6.2.0 release, coming with plenty of new features including central monitoring, a passwords keystore, Auditbeat GA, Kubernetes autodiscovery, and a Filebeat module ...</p>


  </article>
  
  
</aside>
<br />
<aside>
  <header>
      <img src="https://www.elastic.co/favicon-32x32.png" width="32" height="32" />
      <a href="https://www.elastic.co/blog/es-hadoop-6-2-0-released" title="05:00PM - 06 February 2018" target="_blank">Elastic Blog – 6 Feb 18</a>
  </header>
  <article>
    

<h3><a href="https://www.elastic.co/blog/es-hadoop-6-2-0-released" target="_blank">Elasticsearch for Apache Hadoop 6.2.0 Released</a></h3>

<p>I am excited to announce the release of Elasticsearch for Apache Hadoop (aka ES-Hadoop) 6.2.0 built against Elasticsearch 6.2.0.</p>


  </article>
  
  
</aside>
<p>Try out 6.2 today: <a href="https://www.elastic.co/downloads" target="_blank">https://www.elastic.co/downloads</a></p>
      </div>
    </div>
  </div>
</div>
    </div>

  


    <div>
      


      <div>
        <section id="topic">

          <div>
            

            

              <div id="ember819"><div><div><article id="post_1"><div><div><div><div><p>Hello there,</p>
<p>I'm trying to highlight searched keyword in matched document with some custom works. Therefore, I need to know position (or offset) of that keyword in document. However, I found no documentation showing clearly how to do that. I know that when set "index_options" to "offsets" or "term_vector" to "with_positions_offsets", position for token will be generated and is stored together with token, but I don't know how to fetch those values.</p>
<p>Please give me some suggestions. Any help would be appreciated!</p></div><div>
            <aside>
              
              <blockquote>
                You can supply custom markup tags e.g.instead of &lt;em&gt; you could have  &lt;somethingMyAppUnderstands&gt; but this won't return the offsets. 
I expect the most likely solution would be to implement a custom highlighter plugin (see <a href="https://github.com/wikimedia/search-highlighter" target="_blank">example</a>)  because these are given the resources you need to get hold of the q…
              </blockquote>
            </aside></div></div><div><section><ul><li>6<h4>replies</h4></li><li>256<h4>views</h4></li><li>3<h4>users</h4></li><li>4<h4>links</h4></li></ul></section></div></div></div></article></div><div><article id="post_3"><div><div><div><div><p>Thank you Mark for your support. It's useful but seems we need to do multi-steps to get those information, like:<br />
Step 1: Get term vector of document<br />
Step 2: Filter search keyword from result of step 1</p>
<p>So, in the case with query:</p>
<pre><code>curl -XGET 'localhost:9200/my_index/_search?pretty' -H 'Content-Type: application/json' -d'
{
  "query": {
    "match": {
      "text": "brown fox"
    }
  },
  "highlight": {
    "fields": {
      "text": {} 
    }
  }
}
</code></pre>
<p>I would like to know if we can get offset position in result (for example in highlight, because elastic engine has ability to return highlighted text with pre & post tags, I assume that it knows text positions), so we don't need extra step.</p>
<pre><code>{
  "took" : 113,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 1,
    "max_score" : 0.5063205,
    "hits" : [
      {
        "_index" : "my_index",
        "_type" : "my_type",
        "_id" : "1",
        "_score" : 0.5063205,
        "_source" : {
          "text" : "Quick brown fox"
        },
        "highlight" : {
          "text" : [
            "Quick &lt;em&gt;brown&lt;/em&gt; &lt;em&gt;fox&lt;/em&gt;"
          ]
        }
      }
    ]
  }
}
</code></pre>
<p>Thank you again Mark!</p></div></div></div></div></article></div><div><article id="post_6"><div><div><div><div><p>Finally, by using <a href="https://github.com/wikimedia/search-highlighter" target="_blank">search-highlighter16</a> plugin, I can get highlight text offset, by query for example:</p>
<pre><code>curl -XGET 'localhost:9200/_search?pretty' -H 'Content-Type: application/json' -d'
{
    "_source": ["content"],
    "query" : {
        "match_phrase" : { "content" : "test keyword" }
    },
    "highlight" : {
    	"pre_tags" : ["&lt;b&gt;"],
        "post_tags" : ["&lt;/b&gt;"],
        "fields" : {
            "content" : {
            	"fragment_size" : 30, 
            	"number_of_fragments" : 10, 
            	"type": "experimental",
            	"options": {"return_offsets": true}
            }
        },
        "order" : "score"
    }
}
'
</code></pre>
<p>Thank you <a href="/u/mark_harwood" target="_blank">@Mark_Harwood</a> for your help!</p></div></div></div></div></article></div><div><div>28 days later</div></div><div id="post_7"><div><p>closed Aug 26, '17</p><div><p>This topic was automatically closed 28 days after the last reply. New replies are no longer allowed.</p></div></div></div></div></div>

            
          </div>
          


        </section>
      </div>

    </div>

  

</div>
  

</div>


  <div id="ember905"><div id="copyright">
	<p>
		© 2016. All Rights Reserved - Elasticsearch
	</p>
	<ul>
		<li>Elasticsearch is a trademark of Elasticsearch BV, registered in the U.S. and in other countries</li>
		<li><a href="https://www.elastic.co/legal/trademarks" id="footer_trademarks" target="_blank">Trademarks</a></li>
		<li><a href="https://www.elastic.co/legal/terms-of-use" id="footer_terms" target="_blank">Terms</a></li>
		<li><a href="https://www.elastic.co/legal/privacy-policy" id="footer_privacy" target="_blank">Privacy</a></li>
		<li><a href="https://www.elastic.co/brand" id="footer_brand" target="_blank">Brand</a></li>
		<li><a href="https://www.elastic.co/community/codeofconduct" id="codeofconduct" target="_blank">Code of Conduct</a></li>
	</ul>
	<p>
		Apache, Apache Lucene, Apache Hadoop, Hadoop, HDFS and the yellow elephant logo are trademarks of the <a href="http://www.apache.org/" target="_blank">Apache Software Foundation</a> in the United States and/or other countries.
	</p>
</div>


</div>





</div></section>

    

      
        
        
        
        
      

      

    

    







      
    
  

<div><h3>Like On Github</h3><div><div>*Title (label for the link)</div></div><div><div>*Comment (commit message)</div></div><div id="action-btns"><div id="logh_btn_save">Saving...</div><div id="logh_btn_cancel">Cancel</div></div></div>
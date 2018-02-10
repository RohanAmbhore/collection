<a href="https://engineuring.wordpress.com/2017/07/02/some-facts-on-sci-hub-that-wikipedia-gets-wrong/">https://engineuring.wordpress.com/2017/07/02/some-facts-on-sci-hub-that-wikipedia-gets-wrong/</a><div id="articleHeader"><h1>Some facts on Sci-Hub that Wikipedia gets wrong</h1></div>
					
							<p>
			Posted by: <a href="https://engineuring.wordpress.com/author/engineuring/" title="View all posts by ringo-ring" target="_blank">ringo-ring</a> on: <a href="https://engineuring.wordpress.com/2017/07/02/some-facts-on-sci-hub-that-wikipedia-gets-wrong/" title="3:42 PM" target="_blank">02/07/2017</a>			</p>
			

	

	
		<p>(and some history of Sci-Hub too)</p>
<p>Like most people, I routinely use Wikipedia to lookup information. Sometimes however, the information in Wikipedia does not represent the true facts about reality. That happened to<a href="https://en.wikipedia.org/wiki/Sci-Hub" target="_blank"> Sci-Hub wikipedia article</a>, too.</p>
<p>Starting from the first paragraph, it says:</p>
<blockquote><p><b>Sci-Hub</b> is an online search engine with over 62,000,000 academic papers and articles available for direct download, bypassing publisher paywalls. New papers are uploaded daily when accessed through educational institution proxies, and papers that have been accessed through Sci-Hub are stored in the <a href="https://en.wikipedia.org/wiki/LibGen" title="LibGen" target="_blank">LibGen</a> repository.</p></blockquote>
<p>What inaccuracies are present in this paragraph?</p>
<p>First of all and important, <strong>Sci-Hub is not a search engine</strong>.</p>
<p>A search engine is a program that takes some keywords from user, and provides the user with documents most relevant to these keywords.</p>
<p><strong>Does Sci-Hub have keywords search? No</strong>. The user needs to provide Sci-Hub with an exact reference to the paywalled paper. The reference can be an URL, or a DOI, or title of the paper, or a scientific reference.</p>
<p>Even if Sci-Hub had keywords search, and I want to add it in future, it would still be incorrect to call it a search engine. Because in search engine the possibility to lookup relevant documents by keywords <strong>is primary and most important function</strong>. But Sci-Hub function is very different.</p>
<p><strong>The core of Sci-Hub is a script that downloads HTML and PDF pages from the Web</strong>. In that sense, Sci-Hub is technically more similar to a web scraper.</p>
<blockquote><p><b>Web scraping</b> is data scraping used for extracting data from websites. Web scraping software may access the World Wide Web directly using the Hypertext Transfer Protocol, or through a web browser. While web scraping can be done manually by a software user, the term typically refers to automated processes implemented using a bot or web crawler. It is a form of copying, in which specific data is gathered and copied from the web, typically into a central local database or spreadsheet, for later retrieval or analysis <em>[from Wikipedia]</em></p></blockquote>
<p>What is specific about Sci-Hub is that it can copy data hidden behind paywalls, and provide it to the user. Sci-Hub can do this either on itself or by user request.</p>
<p>The download script of Sci-Hub is complicated and<strong> that is the part where most developer efforts were invested</strong>. Not on search.</p>
<p>The next small inaccuracy is:</p>
<blockquote><p>New papers are uploaded daily when accessed through educational institution proxies</p></blockquote>
<p>That is true, but some papers are downloaded directly from publishers, too. And Sci-Hub also downloads papers by itself. So the paper can be uploaded not only when requested by user, but in advance.</p>
<p>Perhaps the most widely distributed inaccuracy about Sci-Hub is the last sentence of the paragraph:</p>
<blockquote><p>papers that have been accessed through Sci-Hub are stored in the LibGen repository</p></blockquote>
<p><strong>Sci-Hub stores papers in its own repository</strong>, and additionaly the papers downloaded by Sci-Hub are also stored in LibGen.</p>
<p>In the next section, the Wikipedia article expands:</p>
<blockquote><p>If a requested paper is available through that database <em>[LibGen]</em>, it will be deployed to the user without needing to utilize any credentials</p></blockquote>
<p><strong>The article will be deployed from one of the Sci-Hub repositories</strong>, not LibGen.</p>
<p>The Wikipedia article is unclear here now, however previously, and on many other websites, not Wikipedia only, Sci-Hub operation was described as:</p>
<ul>
<li>first, check if the copy is available in LibGen, and if yes, serve paper from LibGen repository</li>
<li>if not, download the paper</li>
</ul>
<p>In fact, Sci-Hub operated in that way from spring of 2013 to the end of 2014.</p>
<p>Sci-Hub was created in September, 2011 and to the spring of 2013<strong> operated without any repository</strong>. Research articles would be downloaded by users, and deleted 6 hours later. The user had to provide an URL of the paywalled page on the Internet, and Sci-Hub would open it through random university proxy. If the paper was still not available, user could manually switch to another university by pressing a green button. Even with that simple mode of operation, Sci-Hub gained huge popularity in a local research community, downloading a few research articles every minute.</p>
<p>The Library Genesis project originally was dedicated to books only. In 2012, they started collecting research articles, too and indexed them by DOI. They wanted to include papers downloaded by Sci-Hub to their database.</p>
<p>In the spring of 2013, Sci-Hub gained popularity in China. The number of requests exploded. It became not possible anymore to download each paper requested, so I started extracting DOI from pages and redirecting users to LibGen if paper was already available there. Thankfully to this, Sci-Hub survived.</p>
<p>Later in 2013 LibGen experienced problems with its hard drives, around 40,000 collected papers were completely lost. There was only one copy! I started a crowdfunding campaign on Sci-Hub to buy additional drives, and soon had my own copy of the database collected by LibGen, around 21 million papers. Around one million of these papers was uploaded from Sci-Hub, the other, as I was told, came from databases that were downloaded on the Internet/Darknet.</p>
<p>Since I had my own copy now, I wanted to expand it. In 2014, I analyzed what publishers are most requested by Sci-Hub users, and created a list of papers that were not yet available in database. The code of Sci-Hub was rewritten from the beginning, and the ability to download papers automatically was introduced. Now Sci-Hub started to collect papers on itself. And users could enjoy much-awaited function: just point Sci-Hub to the article, and it will check all proxies and download the paper by itself. Before, users had to manually browse the publishers website through Sci-Hub.</p>
<p>In the end of 2014, few additional copies of the database was created. They became a mirrors from which Sci-Hub is serving content now. Those are Sci-Hub only repositories, separate from LibGen.</p>
<p>Efforts were invested to establish these mirrors so that papers could be served to Sci-Hub users quickly and without interruptions. Even further, people behind LibGen had a strong position not to contact journalists and work semi-underground. My view is different: to spread the idea that science has to be freely accessible by everyone. If Sci-Hub wasn’t autonomous from LibGen, and relied on LibGen infrastructure, perhaps I wouldn’t be able to spread the message.</p>
<p>In that sense, <strong>Sci-Hub technically is by itself a repository</strong>, or a library if you like, and not a search engine for some other repository. But of course, the most important part in Sci-Hub is not a repository, but the script that can download papers closed behind paywalls.</p>
<p>Currently, the Sci-Hub does not store books, for books users are redirected to LibGen, but not for research papers. In future, I also want to expand the Sci-Hub repository and add books too.</p>
<p>The next inaccuracy in Wikipedia article is:</p>
<blockquote><p>in April 2016, Elbakyan told <i>Science</i> that many anonymous academics from around the world donate their credentials voluntarily, while publishers have claimed that Sci-Hub relies on credentials obtained by phishing</p></blockquote>
<p>I did not tell Science how credentials were donated: either voluntarily or not. I only told that I cannot disclose the source of the credentials. I assume that some credentials coming to Sci-Hub could have been obtained by phishing. Anyway, Sci-Hub is not doing any phishing by itself. The credentials are used only to download papers.</p>
<p><em>By Wikipedia rules, I cannot edit article about Sci-Hub myself</em></p>
<div>
			<div>
				Advertisements
				
						
				
		
			</div>
		</div>
		

		
			
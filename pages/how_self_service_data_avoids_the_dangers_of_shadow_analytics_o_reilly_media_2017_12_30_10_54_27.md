<a href="https://www.oreilly.com/ideas/how-self-service-data-avoids-the-dangers-of-shadow-analytics">https://www.oreilly.com/ideas/how-self-service-data-avoids-the-dangers-of-shadow-analytics</a><div id="articleHeader"><h1>How self-service data avoids the dangers of “shadow analytics”</h1></div>

      <p>Without the proper cataloging, curation, and security that self-service data platforms allow, companies are left vulnerable to cybersecurity threats and misinformation.</p>
  

  <div>
  By <a href="/people/82fb1-kelly-stirman" target="_blank">Kelly Stirman</a>
</div> <time>December 6, 2017</time>

</header>

      

      
        
                              <figure>
  <div class="readableLargeImageContainer"><img src="https://d3tdunqjn7n0wj.cloudfront.net/360x240/pexels-photo-136351_crop-ac69d16316eba86269c237ca119e241d.jpg" alt="Shadow chess" /></div>
  <figcaption>Shadow chess
          
                  (source: <a href="https://www.pexels.com/photo/light-black-and-white-dark-shadow-136351/" target="_blank">Pexels</a>)
        
        
      
    
    
  </figcaption></figure>
          
                      

          
        

        

        <p>In our personal lives, data makes the world go round. You can answer almost any question in a second thanks to Google. Booking travel anywhere on the planet is just a few clicks away. And your smartphone has apps for pretty much anything you can think of, and more. It’s a great time to love coffee and craft beer. And it’s a great time to be a consumer of data. Life has never been better.</p>

<p>When we get to work, however, our relationship with data isn’t nearly as friendly. While everyone’s job depends on data, most of us struggle to use it as seamlessly as we do in our personal lives. At work, data is hard to find. It’s slow to access. Each data set has its own tools and “cheat sheet” to use successfully. Frequently, the data we need isn’t available to us in a shape we need, so we open a ticket with IT, then wait and hope for the best. Collaborating with other users to work with data is far from simple, and typically the solution is to copy the data into Excel and email it to someone. Alternately, we might set up a BI server or database we manage ourselves, even potentially on a server hiding in a closet or under someone’s desk.</p><div>              <h4>Strata Data Conference</h4>                            <div>            <a href="https://conferences.oreilly.com/strata/strata-ca/public/register?intcmp=il-data-confreg-lp-stca18_20171023_new_site_right_rail_custom_cta_strata_sj_2018" target="_blank" class="readableLinkWithMediumImage"><img src="https://d3ansictanv2wj.cloudfront.net/strata_san_jose_700x500-1a0bc3a8d6459f67b4652616737d4d58.jpg" /></a>                      </div>                          <div>        <h2><a href="https://conferences.oreilly.com/strata/strata-ca/public/register?intcmp=il-data-confreg-lp-stca18_20171023_new_site_right_rail_custom_cta_strata_sj_2018" target="_blank">Strata Data Conference in San Jose, March 5-8, 2018</a></h2>              </div>            <div>                                      <a href="https://conferences.oreilly.com/strata/strata-ca/public/register?intcmp=il-data-confreg-lp-stca18_20171023_new_site_right_rail_custom_cta_strata_sj_2018" target="_blank">          Early price ends January 19.    <svg>    <title>arrow-right</title>      </svg>        </a>          </div></div>

<h2>We’ve seen this rodeo before</h2>

<p>If this sounds familiar, it should. For the past decade, workers have found ways to work around limitations in the hardware and software provided by IT—a trend we call “shadow IT<em>.</em>” Workers started to bring their own laptops, iPads, and smartphones until IT either made these devices available or adopted “bring your own device” policies. Popular apps like Evernote, Dropbox, and Gmail, as well as cloud service providers like AWS and Google Cloud, quickly became everyday tools for millions of people in the workplace, opening up companies to massive security vulnerabilities that most are still trying to address today.</p>

<p>Companies learned that simply shutting down access to these systems and keeping the status quo was not an option. They learned to improve the quality of hardware and software in order to keep people using governed systems, removing the need to take matters into their own hands.</p>

<h2>A new trend: Shadow analytics</h2>

<p>What we saw with software and hardware over the past decade is now happening with data, a phenomenon we call “shadow analytics.” People want to do their jobs, and they’ll find a way to be more productive if IT organizations don’t provide the right tools. They are frustrated with their inability to access and use data, and they’re finding workarounds by moving data into ungoverned environments that sidestep the essential controls put in place by organizations. For example, users download data into spreadsheets, load data into cloud applications, and even run their own database and analytics software on their desktops.</p>

<p>Shadow analytics creates an environment where users can reach misleading conclusions. Because data is disconnected from the source, users can lose important updates in their copies, and the answers to questions they developed may no longer apply. In addition, with each user managing their own copy of the data, each copy can be wrong in different ways. As a result, IT organizations are frequently asked, “My colleague and I have different answers to an essential question—why?”</p>

<h2>Why shadow analytics is a big deal</h2>

<p>Data is the greatest asset—and the greatest liability—of most organizations. Cybersecurity threats are evolving rapidly. In the past few years, <a href="https://www.symantec.com/en/uk/security-center/threat-report" target="_blank">phishing attacks</a> and <a href="http://www.pwc.com/gx/en/issues/cyber-security/information-security-survey.html" target="_blank">intellectual property theft </a><a href="http://www.pwc.com/gx/en/issues/cyber-security/information-security-survey.html" target="_blank">have grown by over 50%</a>, <a href="http://newsroom.emea.intelsecurity.com/threat-reports-and-security-predictions/ransomware-2/" target="_blank">ransomware is up over 160%</a>, and the <a href="http://www.cisco.com/c/m/en_us/offers/sc04/2016-midyear-cybersecurity-report/index.html" target="_blank">average time to detect compromises has reached 200 days</a>. Consider a few of the recent headlines for major companies such as Equifax, Yahoo, and Target—billions of people were affected.</p>

<p>The main driver for the expansion of these threats is that the surface area for possible cyberattacks has radically increased in the past decade, and the number of threat actors has exploded. With each new device (e.g., smartphones, IoT, automated sensors), each new application, and every copy of data, a new vulnerability is created that potentially opens the door to the entire organization.</p><div>          <div>Get O'Reilly's weekly data newsletter</div>                                <div>            <a target="_blank" class="readableLinkWithMediumImage"><img src="https://cdn.oreillystatic.com/oreilly/email/data-newsletter-20160205.jpg" /></a>                      </div>                                                 </div>

<p>Every organization’s data and systems are potential targets for attack from armies of hackers-for-hire, well-organized criminal gangs, and state-sponsored initiatives. Threats are becoming more sophisticated with the emergence of social engineering, advanced persistent threats (APTs), ransomware, and fraud committed through digital identity theft. Cybersecurity software and services are not enough because once you've lost control over your data, your chances of airtight protection are slim, even with the most sophisticated network and endpoint security systems.</p>

<h2>A new paradigm emerges: Self-service data</h2>

<p>Organizations have focused on several functional areas to improve the safety, accessibility, and usability of their data. Today, organizations understand that self-service data is essential to avoid the risks associated with shadow analytics. With self-service data, organizations can now provide data consumers with an experience that makes them more productive than they would be taking matters into their own hands.</p>

<p>Let's take a closer look at the essential functional areas of data analytics to examine their importance and the benefits of a <a href="https://www.dremio.com/product" target="_blank">self-service approach</a>.</p>


<table>
	<tbody>
		<tr>
			<td><strong>Functional area</strong></td>
			<td><strong>Why is this important?</strong></td>
			<td><strong>Self-service data approach</strong></td>
		</tr>
		<tr>
			<td><strong>Data acceleration</strong></td>
			<td>The nature of analysis and data science is iterative. Data consumers ask questions that lead to new ideas and follow-on questions. Each query needs to be interactive, no matter the source or size of the data, and using any tool, such as Tableau or Python.<br /><br />With shadow analytics, users create BI extracts or OLAP cubes to accelerate access to data. Because each person works independently, many redundant copies are created, each potentially ungoverned and disconnected from the source. In addition, these copies are slow to update and create additional cognitive load on the user (i.e., which cube do I connect to for a given query?)</td>
			<td>It is impractical to scan all data for each query. For decades, systems have applied techniques to accelerate access to data, such as indexes, sorting, partitioning, and aggregating data to support various query patterns. Traditionally, these approaches are created by an administrator and end users must understand which optimization is best for their given query. In the self-service data approach, these optimizations are invisible to an end user. The system must be able to use them when appropriate without relying on the end-user. In addition, the system must be capable of autonomously identifying the best optimizations and adapting to emerging query patterns over time.</td>
		</tr>
		<tr>
			<td><strong>Data catalog</strong></td>
			<td>Data consumers struggle to find data that is important to their work. Not all data is created equal—it is important to identify specific data sets as vetted and authoritative for all users.<br /><br />With shadow analytics, there is no central catalog. Instead, users keep private notes about data sources and data quality, meaning there is no governance and there is no vetted sense of meaning across the organization.</td>
			<td>In the self-service approach, the catalog is automatic—as new data sources are brought online, the system must discover the underlying schema automatically, and it must adapt as the source evolves. Organizations develop rich semantic descriptions of their data that should be searchable as well. In addition, data sets that are created by end users must also be cataloged for easy discovery and analysis.</td>
		</tr>
		<tr>
			<td><strong>Data virtualization</strong></td>
			<td>It is virtually impossible for an organization to centralize all data in a single system. Analytical tools, including BI tools like Tableau and data science tools like Python and R, assume that all data resides in a single relational database.<br /><br />With shadow analytics, data is moved from one system into a format that is accessible by tools such as Tableau or Python, typically CSV. This creates a copy that is ungoverned and disconnected from the source data.</td>
			<td>Data consumers need to be able to access all data sets equally well, regardless of the underlying technology or location of the system. Access should be through SQL, as it is widely supported by all tools and well understood by most users.</td>
		</tr>
		<tr>
			<td><strong>Data curation</strong></td>
			<td>There is no single “shape” of data that works for everyone. Each data consumer needs data in a particular form that is useful for the task at hand. This can mean filtering data in various ways, blending multiple data sets together, converting data types, formatting the data in different ways, and more.<br /><br />With shadow analytics, curation is performed by making copies of data that are typically ungoverned and disconnected from their sources.</td>
			<td>Data consumers need the ability to interact with data sets from the context of the data itself, not exclusively from simple metadata that fails to tell the whole story. Data consumers should be capable of reshaping data to their own needs without writing any code or learning new languages. In the self-service data approach, these capabilities are provided without making copies of the data—no organization wants thousands of copies of their data.</td>
		</tr>
		<tr>
			<td><strong>Data lineage</strong></td>
			<td>As data is accessed by data consumers and in different processes, it is important to track the provenance of the data, who accessed the data, how the data was accessed, what tools were used, and what results were obtained. In cases of sensitive data, erroneous data, or data breaches, it is critical to be able to establish the full lineage of data.<br /><br />In shadow analytics, data is accessed and copied independent of any governing process. There is no clear record of data lineage or custody.</td>
			<td>With each data consumer capable of creating data sets for themselves, the importance of data lineage becomes paramount—no company wants to govern thousands of copies of each data set. It is critical this lineage be tracked automatically—organizations cannot rely on end users to record and register their work in a central system themselves. Instead, as users reshape and share data sets with one another through a virtual context, a self-service data platform can seamlessly track these actions and all states of data along the way, providing full audit capabilities as well.</td>
		</tr>
		<tr>
			<td>
<strong>Open source</strong>
			</td>
			<td>Because data is essential to every area of every business, the underlying data formats and technologies used to access and process the data should be open source. Organizations should not be locked into a specific vendor or commercial model.<br /><br />In shadow analytics, users decide for themselves which tools are used, including proprietary tools from unknown vendors, and cloud services whose access is not controlled by the organization (e.g., if the employee leaves, how will the data be accessed?)</td>
			<td>Self-service data platforms build on <a href="https://www.dremio.com/open-source" target="_blank">open source standards</a> like Apache Parquet, Apache Arrow, and Apache Calcite to store, query, and analyze data from any source. In addition, the end user interface is also open source and runs in any modern browser, while providing access to visualization and analytical tools over open standards like ODBC, JDBC, and REST.</td>
		</tr>
		<tr>
			<td><strong>Security controls</strong></td>
			<td>Organizations safeguard their data assets with security controls that govern authentication (you are who you say you are), authorization (you can perform specific actions), auditing (a record of the actions you take), and encryption (you can only read the data if you have the right key). In shadow analytics, users download data into environments that are outside these central controls, exposing companies to unnecessary risk.</td>
			<td>Self-service data platforms integrate with existing security controls of the organization, such as LDAP and Kerberos. They respect the controls of underlying data sources and do not create copies of data that are outside of these controls.</td>
		</tr>
	</tbody>
</table>

<h2>Conclusion</h2>

<p>In terms of data, companies need to find the right balance between control and convenience—control of the data and systems in a safe and auditable way, and convenience for end users so they don’t invent ways to work around these controls. Self-service data platforms are a new open source approach that helps to prevent shadow analytics. They preserve and extend existing security controls, and give data consumers a way to use data that makes them more productive than taking matters into their own hands.</p>


        
                  
        

                  <div>
  Article image: Shadow chess
          
                  (source: <a href="https://www.pexels.com/photo/light-black-and-white-dark-shadow-136351/" target="_blank">Pexels</a>).
        
        
      
    
    
</div>
        

        

      
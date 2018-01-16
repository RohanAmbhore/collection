<a href="https://archive.org/details/documentation-dump.7z">https://archive.org/details/documentation-dump.7z</a><div id="articleHeader"><h1>      <div>texts</div>Stack Overflow Documentation Data Dump    </h1></div>

          
      
    
          <div>
                  <div>    by

    <a href="/search.php?query=creator%3A%22Stack+Exchange%2C+Inc.%22" target="_blank">Stack Exchange, Inc.</a>
    </div>              
    
    <div>
        Publication date <a href="/search.php?query=date:2017-09-08" target="_blank">
          2017-09-08
        </a>
              </div>
    
          <div>
        Usage       </div>
    
          <div>
        Topics <a href="/search.php?query=subject%3A%22stackoverflow+documentation%22" target="_blank">stackoverflow documentation</a>
      </div>
    
    <div>    Collection

    <a href="/details/opensource" target="_blank">opensource</a>
    </div>
    
    
    
    
          <div>
        <div>    Language

    <a href="/search.php?query=%28language%3Aeng+OR+language%3A%22English%22%29" target="_blank">English</a>
    </div>      
    
    
    
    
    

    <div id="descript">Stack Overflow Documentation Data Dump
</div>


        
        <div>
                  <div>
          Identifier

    documentation-dump.7z
        </div>
                      <div>
          Identifier-ark

    ark:/13960/t0jt5vn75
        </div>
                      <div>
          Scanner

    Internet Archive HTML5 Uploader 1.6.3
        </div>
                      <div>
          Year

    <a href="/search.php?query=year%3A%222017%22" target="_blank">2017</a>
        </div>
          
          

    






    <div id="reviews">
      <h2>
        
        <div>comment</div>
        Reviews
      </h2>
      
          <div>
      <b>Reviewer:</b>
              <a href="https://archive.org/details/%40tony_dallimore" target="_blank">Tony Dallimore</a>
            -
      favoritefavoritefavoritefavorite      -
      October 24, 2017      <br />
      <b>Subject:</b>
      Easy to use but unusable dates      <div>
        Summary<br /><br />I found it relatively easy to extract the data I wanted from the archive.  My only serious criticism is the obscure (to non-Unix users) date format.  I do not need dates but, if they are thought to be important, I believe the archive should be recreated with standard JSON dates<br /><br />Detail<br /><br />I had started writing an introduction to Outlook VBA within Stack Overflow Documentation, which I did not wish to lose.  I have started extracting my text from the website but had not finished when the documentation was taken down so if I was to find my text I would have to extract it from the archive.<br /><br />File “<a href="http://documentation-dump.7z" target="_blank">documentation-dump.7z</a>” was easy to download.  WinZip extracted its contents just as easily.  No doubt, your favourite extraction utility will work just as effectively.<br /><br />The file “<a href="http://readme.txt" target="_blank">readme.txt</a>” seemed the obvious start point.  This file lists the other files each with what look like a list of field names.  There is no other documentation that I have found.  I have decoded the files of interest to me without difficulty so perhaps no more documentation was necessary.  On the other hand, I have had much practice at decoding undocumented files so others may find this lack of documentation more troubling.<br /><br />Most of the files had an extension of “json” which meant nothing to me.  A search for “json” found <a href="http://json.org/" target="_blank">http://json.org/</a> which provided an adequate definition of the format of JavaScript Object Notation which is a lightweight data-interchange format.  Before the days of XML I was a specialist in electronic data interchange so again I may not be the best judge of the adequacy of this definition.<br /><br />Starting with the first file, “<a href="http://contributors.json" target="_blank">contributors.json</a>”, I found:<br /><br />[<br />
  {<br />
    "Id": 1,<br />
    "DocTopicId": 1,<br />
    "UserId": 80572,<br />
    "DocContributorTypeId": 2,<br />
    "CreationDate": "\/Date(1446697142040-0500)\/"<br />
  },<br />
  {<br />
    "Id": 2,<br />
   and so on<br /><br />With my newly acquired knowledge of this format, I knew “{name/value pair, name/value pair, …}” was an object and “[” was the start of an array so the file was an array of these simple objects.  The names and values looked obvious enough and with the one exception of "\/Date(1446697142040-0500)\/".<br /><br />When searching for “json”, “json date format” is the first suggestion.  Apparently, "\/Date(1446697142040)\/" is milliseconds since<a href="/details/documentation-dump.7z?start=0" target="_blank"> 0:00 </a>on 1 January 1970.  I can find nothing to explain “-0500” which seems to be a private SO addition; I assume it is something to do with a time zone.  Apparently, JSON does not define date formats and conventions have changed over the years.  However, a Stack Overflow answer with a score of 1140 recommends ISO 8601’s format: “2012-04-23T18:25:43.511Z”.  Apparently this format is endorsed by everyone that matters. The only reason for considering milliseconds since 1970 seems to be that it is a standard within Unix and even the oldest libraries have routines that can read it. This is not a standard that appeals to non-Unix users.  I do not know if dates are important to anyone; certainly they are not important to me.  If they are thought to be important, I believe the archive should be recreated with dates in ISO 8601 format so everyone can use them.<br /><br />I searched “<a href="http://contributors.json" target="_blank">contributors.json</a>” for my user id and found enough occurrences to match the number of examples I had written.<br /><br />I tend to use Excel and VBA for this type of investigation.  VBA is an adequate language and Excel worksheets are a convenient repository for poorly understood data.  I wrote code to extract each object containing my user id and save it as a row within an Excel worksheet. The first few rows and columns of that worksheet contain:<pre>Row|  A  |     B    |      C     |   D  |          E         |             F            |<br />
   |-----+----------+------------+------+--------------------+--------------------------|<br />
  1|   Id|DocTopicId|DocExampleId|UserId|DocContributorTypeId|CreationDate              |<br />
   |-----+----------+------------+------+--------------------+--------------------------|<br />
  2|79143|          |       26136|973283|                   2|/Date(1484774756887-0500)/|<br />
   |-----+----------+------------+------+--------------------+--------------------------|<br />
  3|79144|      8111|            |973283|                   2|/Date(1484774756887-0500)/|<br />
   |-----+----------+------------+------+--------------------+--------------------------|<br />
  4|79145|          |       27558|973283|                   2|/Date(1484774756887-0500)/|<br />
   |-----+----------+------------+------+--------------------+--------------------------|<br />
  5|79350|          |       27628|973283|                   2|/Date(1485051525857-0500)/|<br />
   |-----+----------+------------+------+--------------------+--------------------------|</pre><br /><br />Sorry if the above if difficult to read.  SO's pre-formatting of text does not work here.<br /><br />The column “DocExampleId” looked interesting so I looked at the file “<a href="http://examples.json" target="_blank">examples.json</a>” which starts:<br /><br />[<br />
  {<br />
    "Id": 1,<br />
    "DocTopicId": 1,<br />
    "Title": "Basic Usage",<br />
    "CreationDate": "\/Date(1446697142040-0500)\/",<br />
    "LastEditDate": "\/Date(1469351669667-0400)\/",<br />
    "Score": 6,<br />
    "ContributorCount": 2,<br />
    "BodyHtml": "<pre><code>using StackExchange.Redis;\r\n\r\n// ...\r\n\r\n// connect to the server\r\nConnectionMultiplexer connection = ConnectionMultiplexer.Connect("localhost");\r\n\r\n// select a database (by default, DB = 0)\r\nIDatabase db = connection.GetDatabase();\r\n\r\n// run a command, in this case a GET\r\nRedisValue myVal = db.StringGet("mykey");\r\n</code></pre>\r\n\r\n",<br />
    "BodyMarkdown": "    using StackExchange.Redis;\n\n    // ...\n\n    // connect to the server\n    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect(\"localhost\");\n    \n    // select a database (by default, DB = 0)\n    IDatabase db = connection.GetDatabase();\n\n    // run a command, in this case a GET\n    RedisValue myVal = db.StringGet(\"mykey\");",<br />
    "IsPinned": false<br />
  },<br />
  {<br />
    "Id": 2,<br />
    "DocTopicId": 2, <br /><br />Again an array of objects with “BodyHtml” perhaps the text I sought.  I searched for one of the DocExampleIds against my UserId and found the html I sought.<br /><br />I wrote code to extract each object containing a DocExampleId for which I was listed as a contributor which I saved as a row within another Excel worksheet.  This worksheet contained all the text I wanted together with links to my images.<br /><br />I had problems reading “<a href="http://examples.json" target="_blank">examples.json</a>” which is 92Mb and uses UTF-8 encoding. I suspect my problems are unique to VBA.  If you are interested in these problems, see: <a href="https://stackoverflow.com/q/46838258/973283." target="_blank">https://stackoverflow.com/q/46838258/973283.</a><br /><br />Conclusion<br /><br />The summary section is my review of the SO documentation archive. The detail section is intended to justify my review and to help and encourage anyone who wishes to extract information from this archive but is intimidated by the format.      </div>
    
        
    

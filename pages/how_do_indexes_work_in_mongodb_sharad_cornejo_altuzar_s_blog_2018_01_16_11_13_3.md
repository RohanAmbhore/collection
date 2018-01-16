<a href="https://blogs.msdn.microsoft.com/shacorn/2015/11/14/how-do-indexes-work-in-mongodb/">https://blogs.msdn.microsoft.com/shacorn/2015/11/14/how-do-indexes-work-in-mongodb/</a><div id="articleHeader"><h1>How do indexes work in MongoDB</h1></div>				
		
		<hr />
	</header>

	
		<p>This year I have been working on <a href="http://www.respawn.com/news/lets-talk-about-the-xbox-live-cloud/" target="_blank">Xbox Live Compute</a> (or <a href="http://www.polygon.com/2015/8/11/9132195/crackdown-3-multiplayer-cloud-xbox-one-gamescom-2015" target="_blank">Thunderhead</a> as we know it internally). This is a product that uses MongoDB as its main Database. So I have had to learn how to investigate performance and scalability issues with this document DB.</p>
<p>It’s been very fun! Here are some of my learnings related to indexes and how they are different to other DBs. Hoping this will save people some time when they need to work with MongoDb. </p>
<h2>How are Indexes special in MongoDB?</h2>
<p>MongoDB allows you to do different operations to the data you store in it. A very big feature compared to other Document DBs is that it supports secondary indexes on its collections. You can create simple and complex indexes and they will be used for speeding up finds (queries), matches (in aggregates) and sorts. It has support for indexes on multiple fields, on arrays, on geospatial fields and even text indexes to speed up searching for string content.</p>
<p><strong>There ain't no such thing as a free lunch </strong>though<strong>: </strong></p>
<ul>
<li>Indexes speed up queries significantly but they slow down writes.</li>
<li>Updates are a special case: they might speed up finding your document but if the value on any indexed fields is changed the index needs to be updated. So you might get a similar impact as in inserts.</li>
<li>In my measurements I saw reads could improve up to 1000% but writes slowed down almost 30%. Overall it should be a big gain since we do a lot more reads than inserts.</li>
<li>Something of note is that they not only affect write operations. They might slow down read operations as well (such as aggregations). This is because aggregations yield to writes so if your writes are slower your aggregation will take longer to complete. So make sure you measure your performance interleaving writes+reads (or run in stress).</li>
</ul>
<p>  I think MongoDB’s QueryOptimizer does a good job. It can be overriden (.hints and $natural for forcing full collection scans) but I could not find a place where it's needed. It's nice having the option of course. </p>
<h2>How to know if an index is being used?</h2>
<p> In the Mongo shell you can use .explain() for normal queries and runCommand+explain for aggregates. Examples:</p>
<p>1)      db.myCollection.find({}).explain()</p>
<p>2)       db.runCommand({ aggregate: "myCollection", pipeline: [{"$match":{}}], explain: true }) </p>
<h2>Compound indexes</h2>
<p>Compound index is when you have more than one field as part of your index. Like this:</p>
<p><strong>Index</strong>: {ServiceId, LastRecordedState}</p>
<p><strong>Query:</strong> {ServiceId, LastRecordedState} – Uses the index of course</p>
<p><strong>Query:</strong> {ServiceId} - it WILL also use the index. This is pretty nice. Because of this once you have a compound index you can remove your simpler indexes if the compound index is a superset.</p>
<p><strong>Query:</strong> {LastRecordedState} - index will not be used because there is no ServiceId in the query</p>
<p><strong>SORTS:</strong></p>
<p>db.collectionName.find().sort({ServiceId: 1,LastRecordedState:1}).explain() uses the index</p>
<p>db.collectionName.find().sort({ServiceId:-1,LastRecordedState:-1}).explain() uses the index</p>
<p>db.collectionName.find().sort({ServiceId: 1,LastRecordedState:-1}).explain() does not use the index</p>
<p>db.collectionName.find().sort({ServiceId:-1,LastRecordedState:1}).explain() does not use the index</p>
<h2>Intersect indexes</h2>
<p> If you have these two indexes:</p>
<p><strong>Index:</strong> {ServiceId}</p>
<p><strong>Index:</strong> {LastRecordedState}</p>
<p> Mongo will try to combine the results of the indexes. You can verify this by looking at the “explain” for your query and find a stage named: AND_SORTED</p>
<p><strong>Query:</strong> {ServiceId, LastRecordedState} could try to combine both queries. However, this depends on the Query performance. In my tests the query with the simple Index would be selected always. (Because LastRecordedState would return too much data)  </p>
<h2>Names for your indexes</h2>
<p>You can use up 31 fields in a compound index, but the default name will be too long. So you should pass a different name:</p>
<table>
<tbody>
<tr>
<td>
<p>var indexOptions = new IndexOptionsBuilder();</p>
<p>indexOptions.SetName("ServiceId_LastRecordedState ");</p>
<p>collection.CreateIndex(keys, indexOptions);</p>
</td>
</tr>
</tbody>
</table>
<p>Other tips:</p>
<ul>
<li>You can create indexes before the field exists in the collection. Or even before the collection exists</li>
<li>You can query if indexes exist: db.system.indexes.find({ns:"databaseName.collectionName"})</li>
</ul>
<p>If the query uses information that exists in the index the result could be much faster. Most of the time this won’t be the case (you might need to disable some fields using a projection), you can see in the explain if the INDEXONLY value is true or fales. </p>
<h2> How to make sense of the output of Explain:</h2>
<p>As mentioned before you can use the .Explain option to evaluate if a given query is using indexes or why it’s taking so long to execute. Here are some tips on how to make sense of the output of this:</p>
<p>"queryPlanner" : {</p>
<p>        "plannerVersion" : 1,</p>
<p>        "namespace" : "databaseName.collectionName",</p>
<p>        "indexFilterSet" : false,</p>
<p>        "parsedQuery" : {</p>
<p>            "$and" : []</p>

<p>        "winningPlan" : {</p>
<p>            "stage" : "COLLSCAN",</p>
<p>            "filter" : {</p>
<p>                "$and" : []</p>

<p>            "direction" : "forward"</p>

<p>        "rejectedPlans" : []</p>

<p>"executionStats" : {</p>
<p>        "executionSuccess" : true,</p>
<p>        "nReturned" : 12191,</p>
<p>        "executionTimeMillis" : 16,</p>
<p>        "totalKeysExamined" : 12191,</p>
<p>        "totalDocsExamined" : 12191,</p>
<p>WINNINGPLAN is the plan that Query Analyzer picked because it finished faster. It will cache it and reuse it for future queries (until you add indexes, reindex, make changes to the collection, etc)</p>
<p><strong>Stages:</strong></p>
<p>COLLSCAN for a full collection scan (did not use your index. You do NOT want this)</p>
<p>IXSCAN for scanning index keys (used the index to find)</p>
<p>FETCH for retrieving documents that it found (most of the time you will see this combined with IXSCAN)</p>
<p>KEEP_MUTATIONS stage: When documents are deleted or updated some Query stages can receive invalidation notices. Some stages flag documents that are deleted. The set of flagged documents is then read by the KEEP_MUTATIONS stage, which re-checks these documents against the query and returns them if they still match. Note that this is not used for the WiredTiger engine, only for the MMAPv1.</p>
<p>"AND_SORTED": You will see this when Mongo used a combined index</p>
<p>queryPlanner.winningPlan.inputStage.stage displays IXSCAN to indicate index use.</p>
<p>executionStats.nReturned displays 12191 to indicate that the query matches and returns 12191 documents.</p>
<p>executionStats.totalKeysExamined display 12191 to indicate that MongoDB scanned 12191 index entries (Note that this is a Full table scan).</p>
<p>executionStats.totalDocsExamined display 12191 to indicate that MongoDB scanned 12191 documents.</p>
	
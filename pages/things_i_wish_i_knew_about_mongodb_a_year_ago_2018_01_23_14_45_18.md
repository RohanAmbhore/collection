<a href="http://snmaynard.com/2012/10/17/things-i-wish-i-knew-about-mongodb-a-year-ago/">http://snmaynard.com/2012/10/17/things-i-wish-i-knew-about-mongodb-a-year-ago/</a><div id="articleHeader"><h1>Things I wish I knew about MongoDB a year ago</h1></div>
  <h2>October 17, 2012</h2>



  <p>I’ve used MongoDB for over a year at scale at both <a href="http://www.heyzap.com" target="_blank">Heyzap</a> and <a href="https://bugsnag.com" target="_blank">Bugsnag</a> and I’ve found it to be a very capable database. As with all databases, there are some gotchas, and here is a summary of the things I wish someone had told me earlier.</p>

<h2 id="selective_counts_are_slow_even_if_indexed">Selective counts are slow even if indexed</h2>

<p>For example, when paginating a users feed of activity, you might see something like,</p>
<div><pre><code>db.collection.count({username: "my_username"});
</code></pre></div>
<p>In MongoDB this count can take orders of magnitude longer than you would expect. There is an <a href="https://jira.mongodb.org/browse/SERVER-1752" target="_blank">open ticket</a> and is currently slated for 2.4, so here’s hoping they’ll get it out. Until then you are left aggregating the data yourself. You could store the aggregated count in mongo itself using the <a href="http://www.mongodb.org/display/DOCS/Updating#Updating-%24inc" target="_blank"><code>$inc</code> command</a> when inserting a new document.</p>

<h2 id="inconsistent_reads_in_replica_sets">Inconsistent reads in replica sets</h2>

<p>When you start using replica sets to distribute your reads across a cluster, you can get yourself in a whole world of trouble. For example, if you write data to the primary a subsequent read may be routed to a secondary that has yet to have the data replicated to it. This can be demonstrated by doing something like,</p>
<div><pre><code>// Writes the object to the primary
db.collection.insert({_id: ObjectId("505bd76785ebb509fc183733"), key: "value"});
    
// This find is routed to a read-only secondary, and finds no results
db.collection.find({_id: ObjectId("505bd76785ebb509fc183733")});
</code></pre></div>
<p>This is compounded if you have performance issues that cause the replication lag between a primary and its secondaries to increase to minutes or even hours in some cases.</p>

<p>You can control whether a query is <a href="http://www.mongodb.org/display/DOCS/Querying#Querying-slaveOk%28QueryingSecondaries%29" target="_blank">run on secondaries</a> and also how many secondaries are replicated to <a href="http://docs.mongodb.org/manual/applications/replication/#replica-set-write-concern" target="_blank">during the insert</a>, but this will affect performance and could block forever in some cases!</p>

<h2 id="range_queries_are_indexed_differently">Range queries are indexed differently</h2>

<p>I have found that range queries use indexes slightly differently to other queries. Ordinarily you would have the key used for sorting as the last element in a compound index. However, when using a range query like <code>$in</code> for example, Mongo applies the sort before it applies the range. This can cause the sort to be done on the documents in memory, which is pretty slow!</p>
<div><pre><code>// This doesn't use the last element in a compound index to sort
db.collection.find({_id: {$in : [
  ObjectId("505bd76785ebb509fc183733"), 
  ObjectId("505bd76785ebb509fc183734"),
  ObjectId("505bd76785ebb509fc183735"),
  ObjectId("505bd76785ebb509fc183736")
]}}).sort({last_name: 1});
</code></pre></div>
<p>At Heyzap we worked around the problem by building a caching layer for the query in Redis, but you can also run the same query twice if you only have two values in your <code>$in</code> statement or adjust your index if you have the RAM available.</p>

<p>You can read more about the <a href="http://blog.mongolab.com/2012/06/cardinal-ins/" target="_blank">issue</a> or view a <a href="https://jira.mongodb.org/browse/SERVER-3310" target="_blank">ticket</a>.</p>

<h2 id="mongos_bson_id_is_awesome">Mongo’s BSON ID is awesome</h2>

<p>Mongo’s BSON ID provides you with a load of useful functionality, but when I first started using Mongo, I didn’t realize half the things you can do with them. For example, the creation time of a BSON ID is stored in the ID. You can extract that time and you have a created_at field for free!</p>
<div><pre><code>// Will return the time the ObjectId was created
ObjectId("505bd76785ebb509fc183733").getTimestamp();
</code></pre></div>
<p>The BSON ID will also increment over time, so sorting by id will sort by creation date as well. The column is also indexed automatically, so these queries are super fast. You can read more about it on the <a href="http://www.mongodb.org/display/DOCS/Optimizing+Object+IDs" target="_blank">10gen site</a>.</p>

<h2 id="index_all_the_queries">Index all the queries</h2>

<p>When I first started using Mongo, I would sometimes run queries on an ad-hoc basis or from a cron job. I initially left those queries unindexed, as they weren’t user facing and weren’t run often. However this caused performance problems for other indexed queries, as the unindexed queries do a lot of disk reads, which impacted the retrieval of any documents that weren’t cached. I decided to make sure the queries are at least partially indexed to prevent things like this happening.</p>

<h2 id="always_run_explain_on_new_queries">Always run explain on new queries</h2>

<p>This may seem obvious, and will certainly be familiar if you’ve come from a relational background, but it is equally important with Mongo. When adding a new query to an app, you should run the query on production data to check its speed. You can also ask Mongo to <a href="http://www.mongodb.org/display/DOCS/Explain" target="_blank">explain</a> what its doing when running the query, so you can check things like which index its using etc.</p>
<div><pre><code>db.collection.find(query).explain()
{
    // BasicCursor means no index used, BtreeCursor would mean this is an indexed query
    "cursor" : "BasicCursor",
    
    // The bounds of the index that were used, see how much of the index is being scanned
    "indexBounds" : [ ],
    
    // Number of documents or indexes scanned
    "nscanned" : 57594,
    
    // Number of documents scanned
    "nscannedObjects" : 57594,
    
    // The number of times the read/write lock was yielded
    "nYields" : 2 ,
    
    // Number of documents matched
    "n" : 3 ,
    
    // Duration in milliseconds
    "millis" : 108,
    
    // True if the results can be returned using only the index
    "indexOnly" : false,
    
    // If true, a multikey index was used
    "isMultiKey" : false
}
</code></pre></div>
<p>I’ve seen code deployed with new queries that would take the site down because of a slow query that hadn’t been checked on production data before deploy. It’s relatively quick and easy to do so, so there is no real excuse not to!</p>

<h2 id="profiler">Profiler</h2>

<p>MongoDB comes with a very useful <a href="http://www.mongodb.org/display/DOCS/Database+Profiler" target="_blank">profiler</a>. You can tune the profiler to only profile queries that take at least a certain amount of time depending on your needs. I like to have it recording all queries that take over 100ms.</p>
<div><pre><code>// Will profile all queries that take 100 ms
db.setProfilingLevel(1, 100);

// Will profile all queries
db.setProfilingLevel(2);

// Will disable the profiler
db.setProfilingLevel(0);
</code></pre></div>
<p>The profiler saves all the profile data into the <a href="http://www.mongodb.org/display/DOCS/Capped+Collections" target="_blank">capped collection</a> system.profile. This is just like any other collection so you can run some queries on it, for example</p>
<div><pre><code>// Find the most recent profile entries
db.system.profile.find().sort({$natural:-1});
    
// Find all queries that took more than 5ms
db.system.profile.find( { millis : { $gt : 5 } } );
    
// Find only the slowest queries
db.system.profile.find().sort({millis:-1});
</code></pre></div>
<p>You can also run the <code>show profile</code> helper to show some of the recent profiler output.</p>

<p>The profiler itself does add some <a href="http://www.mongodb.org/display/DOCS/Database+Profiler#DatabaseProfiler-ProfilerOverhead" target="_blank">overhead</a> to each query, but in my opinion it is essential. Without it you are blind. I’d much rather add small overhead to the overall speed of the database to give me visibility of which queries are causing problems. Without it you may just be blissfully unaware of how slow your queries actually are for a set of your users.</p>

<h2 id="useful_mongo_commands">Useful Mongo commands</h2>

<p>Heres a summary of useful commands you can run inside the mongo shell to get an idea of how your server is acting. These can be scripted so you can pull out some values and chart or monitor them if you want.</p>

<ul>
<li><a href="http://www.mongodb.org/display/DOCS/Viewing+and+Terminating+Current+Operation" target="_blank">db.currentOp()</a> - shows you all currently running operations</li>

<li><a href="http://www.mongodb.org/display/DOCS/Viewing+and+Terminating+Current+Operation" target="_blank">db.killOp(opid)</a> - lets you kill long running queries</li>

<li><a href="http://docs.mongodb.org/manual/reference/server-status-index/#server-status-example-instance-information" target="_blank">db.serverStatus()</a> - shows you stats for the entire server, very useful for monitoring</li>

<li><a href="http://docs.mongodb.org/manual/reference/database-statistics/" target="_blank">db.stats()</a> - shows you stats for the selected db</li>

<li><a href="http://docs.mongodb.org/manual/reference/collection-statistics/" target="_blank">db.collection.stats()</a> - stats for the specified collection</li>
</ul>

<h2 id="monitoring">Monitoring</h2>

<p>While monitoring production instances of Mongo over the last year or so, I’ve built up a list of key metrics that should be monitored.</p>

<h3 id="index_sizes">Index sizes</h3>

<p>Seeing as how in MongoDB you really need your working set to fit in RAM, this is essential. At Heyzap for example, we would need our entire indexes to sit in memory, as we would quite often query our entire dataset when viewing older games or user profiles.</p>

<p>Charting the index size allowed Heyzap to accurately predict when we would need to scale the machine, drop an index or deal with growing index size in some other way. We would be able to predict to within a day or so when we would start to have problems with the current growth of index.</p>

<h3 id="current_ops">Current ops</h3>

<p>Charting your current number of operations on your mongo database will show you when things start to back up. If you notice a spike in currentOps, you can go and look at your other metrics to see what caused the problem. Was there a slow query at that time? An increase in traffic? How can we mitigate this issue? When current ops spike, it quite often leads to replication lag if you are using a replica set, so getting on top of this is essential to preventing inconsistent reads across the replica set.</p>

<h3 id="index_misses">Index misses</h3>

<p>Index misses are when MongoDB has to hit the disk to load an index, which generally means your working set is starting to no longer fit in memory. Ideally, this value is 0. Depending on your usage it may not be. Loading an index from disk occasionally may not adversely affect performance too much. You should be keeping this number as low as you can however.</p>

<h3 id="replication_lag">Replication lag</h3>

<p>If you use replication as a means of backup, or if you read from those secondaries you should monitor your replication lag. Having a backup that is hours behind the primary node could be very damaging. Also reading from a secondary that is many hours behind the primary will likely cause your users confusion.</p>

<h3 id="io_performance">I/O performance</h3>

<p>When you run your MongoDB instance in the cloud, using Amazon’s EBS volumes for example, it’s pretty useful to be able to see how the drives are doing. You can get random drops of I/O performance and you will need to correlate those with performance indicators such as the number of current ops to explain the spike in current ops. Monitoring something like <a href="http://en.wikipedia.org/wiki/Iostat" target="_blank">iostat</a> will give you all the information you need to see whats going on with your disks.</p>

<h3 id="monitoring_commands">Monitoring commands</h3>

<p>There are some pretty cool utilities that come with Mongo for monitoring your instances.</p>

<ul>
<li><a href="http://docs.mongodb.org/manual/reference/mongotop/" target="_blank">mongotop</a> - shows how much time was spend reading or writing each collection over the last second</li>

<li><a href="http://docs.mongodb.org/manual/reference/mongostat/" target="_blank">mongostat</a> - brilliant live debug tool, gives a view on all your connected MongoDB instances</li>
</ul>

<h3 id="monitoring_frontends">Monitoring frontends</h3>

<ul>
<li><a href="http://www.10gen.com/mongodb-monitoring-service" target="_blank">MMS</a> - 10gen’s hosted mongo monitoring service. Good starting point.</li>

<li><a href="http://kibana.org/" target="_blank">Kibana</a> - Logstash frontend. Trend analysis for Mongo logs. Pretty useful for good visibility.</li>
</ul>

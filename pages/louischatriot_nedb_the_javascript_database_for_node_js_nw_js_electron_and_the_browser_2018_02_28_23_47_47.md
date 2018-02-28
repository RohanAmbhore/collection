<a href="https://github.com/louischatriot/nedb">https://github.com/louischatriot/nedb</a><div id="articleHeader"><h1>The JavaScript Database</h1></div>
<p><strong>Embedded persistent or in memory database for Node.js, nw.js, Electron and browsers, 100% JavaScript, no binary dependency</strong>. API is a subset of MongoDB's and it's <a href="#speed" target="_blank">plenty fast</a>.</p>
<p><strong>IMPORTANT NOTE</strong>: Please don't submit issues for questions regarding your code. Only actual bugs or feature requests will be answered, all others will be closed without comment. Also, please follow the <a href="#bug-reporting-guidelines" target="_blank">bug reporting guidelines</a> and check the <a href="https://github.com/louischatriot/nedb/wiki/Change-log" target="_blank">change log</a> before submitting an already fixed bug :)</p>
<h2>Support NeDB development</h2>
<p><a href="https://camo.githubusercontent.com/69dead7777fe52b91fccc6d8cb4516bd48e0ac75/687474703a2f2f692e696d6775722e636f6d2f6d707769346c662e6a7067" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/69dead7777fe52b91fccc6d8cb4516bd48e0ac75/687474703a2f2f692e696d6775722e636f6d2f6d707769346c662e6a7067" /></div></a></p>
<p>No time to <a href="#pull-requests" target="_blank">help out</a>? You can support NeDB development by sending money or bitcoins!</p>
<p>Money: </p>
<p>Bitcoin address: 1dDZLnWpBbodPiN8sizzYrgaz5iahFyb1</p>
<h2>Installation, tests</h2>
<p>Module name on npm and bower is <code>nedb</code>.</p>
<pre><code>npm install nedb --save    # Put latest version in your package.json
npm test                   # You'll need the dev dependencies to launch tests
bower install nedb         # For the browser versions, which will be in browser-version/out
</code></pre>

<p>It is a subset of MongoDB's API (the most used operations).</p>

<h3>Creating/loading a database</h3>
<p>You can use NeDB as an in-memory only datastore or as a persistent datastore. One datastore is the equivalent of a MongoDB collection. The constructor is used as follows <code>new Datastore(options)</code> where <code>options</code> is an object with the following fields:</p>
<ul>
<li><code>filename</code> (optional): path to the file where the data is persisted. If left blank, the datastore is automatically considered in-memory only. It cannot end with a <code>~</code> which is used in the temporary files NeDB uses to perform crash-safe writes.</li>
<li><code>inMemoryOnly</code> (optional, defaults to <code>false</code>): as the name implies.</li>
<li><code>timestampData</code> (optional, defaults to <code>false</code>): timestamp the insertion and last update of all documents, with the fields <code>createdAt</code> and <code>updatedAt</code>. User-specified values override automatic generation, usually useful for testing.</li>
<li><code>autoload</code> (optional, defaults to <code>false</code>): if used, the database will automatically be loaded from the datafile upon creation (you don't need to call <code>loadDatabase</code>). Any command issued before load is finished is buffered and will be executed when load is done.</li>
<li><code>onload</code> (optional): if you use autoloading, this is the handler called after the <code>loadDatabase</code>. It takes one <code>error</code> argument. If you use autoloading without specifying this handler, and an error happens during load, an error will be thrown.</li>
<li><code>afterSerialization</code> (optional): hook you can use to transform data after it was serialized and before it is written to disk. Can be used for example to encrypt data before writing database to disk. This function takes a string as parameter (one line of an NeDB data file) and outputs the transformed string, <strong>which must absolutely not contain a <code>\n</code> character</strong> (or data will be lost).</li>
<li><code>beforeDeserialization</code> (optional): inverse of <code>afterSerialization</code>. Make sure to include both and not just one or you risk data loss. For the same reason, make sure both functions are inverses of one another. Some failsafe mechanisms are in place to prevent data loss if you misuse the serialization hooks: NeDB checks that never one is declared without the other, and checks that they are reverse of one another by testing on random strings of various lengths. In addition, if too much data is detected as corrupt, NeDB will refuse to start as it could mean you're not using the deserialization hook corresponding to the serialization hook used before (see below).</li>
<li><code>corruptAlertThreshold</code> (optional): between 0 and 1, defaults to 10%. NeDB will refuse to start if more than this percentage of the datafile is corrupt. 0 means you don't tolerate any corruption, 1 means you don't care.</li>
<li><code>compareStrings</code> (optional): function compareStrings(a, b) compares
strings a and b and return -1, 0 or 1. If specified, it overrides
default string comparison which is not well adapted to non-US characters
in particular accented letters. Native <code>localCompare</code> will most of the
time be the right choice</li>
<li><code>nodeWebkitAppName</code> (optional, <strong>DEPRECATED</strong>): if you are using NeDB from whithin a Node Webkit app, specify its name (the same one you use in the <code>package.json</code>) in this field and the <code>filename</code> will be relative to the directory Node Webkit uses to store the rest of the application's data (local storage etc.). It works on Linux, OS X and Windows. Now that you can use <code>require('nw.gui').App.dataPath</code> in Node Webkit to get the path to the data directory for your application, you should not use this option anymore and it will be removed.</li>
</ul>
<p>If you use a persistent datastore without the <code>autoload</code> option, you need to call <code>loadDatabase</code> manually.
This function fetches the data from datafile and prepares the database. <strong>Don't forget it!</strong> If you use a
persistent datastore, no command (insert, find, update, remove) will be executed before <code>loadDatabase</code>
is called, so make sure to call it yourself or use the <code>autoload</code> option.</p>
<p>Also, if <code>loadDatabase</code> fails, all commands registered to the executor afterwards will not be executed. They will be registered and executed, in sequence, only after a successful <code>loadDatabase</code>.</p>
<div><pre>// Type 1: In-memory only datastore (no need to load the database)
var Datastore = require('nedb')
  , db = new Datastore();


// Type 2: Persistent datastore with manual loading
var Datastore = require('nedb')
  , db = new Datastore({ filename: 'path/to/datafile' });
db.loadDatabase(function (err) {    // Callback is optional
  // Now commands will be executed
});


// Type 3: Persistent datastore with automatic loading
var Datastore = require('nedb')
  , db = new Datastore({ filename: 'path/to/datafile', autoload: true });
// You can issue commands right away


// Type 4: Persistent datastore for a Node Webkit app called 'nwtest'
// For example on Linux, the datafile will be ~/.config/nwtest/nedb-data/something.db
var Datastore = require('nedb')
  , path = require('path')
  , db = new Datastore({ filename: path.join(require('nw.gui').App.dataPath, 'something.db') });


// Of course you can create multiple datastores if you need several
// collections. In this case it's usually a good idea to use autoload for all collections.
db = {};
db.users = new Datastore('path/to/users.db');
db.robots = new Datastore('path/to/robots.db');

// You need to load each database (here we do it asynchronously)
db.users.loadDatabase();
db.robots.loadDatabase();</pre></div>
<h3>Persistence</h3>
<p>Under the hood, NeDB's persistence uses an append-only format, meaning that all updates and deletes actually result in lines added at the end of the datafile, for performance reasons. The database is automatically compacted (i.e. put back in the one-line-per-document format) every time you load each database within your application.</p>
<p>You can manually call the compaction function with <code>yourDatabase.persistence.compactDatafile</code> which takes no argument. It queues a compaction of the datafile in the executor, to be executed sequentially after all pending operations. The datastore will fire a <code>compaction.done</code> event once compaction is finished.</p>
<p>You can also set automatic compaction at regular intervals with <code>yourDatabase.persistence.setAutocompactionInterval(interval)</code>, <code>interval</code> in milliseconds (a minimum of 5s is enforced), and stop automatic compaction with <code>yourDatabase.persistence.stopAutocompaction()</code>.</p>
<p>Keep in mind that compaction takes a bit of time (not too much: 130ms for 50k records on a typical development machine) and no other operation can happen when it does, so most projects actually don't need to use it.</p>
<p>Compaction will also immediately remove any documents whose data line has become corrupted, assuming that the total percentage of all corrupted documents in that database still falls below the specified <code>corruptAlertThreshold</code> option's value.</p>
<p>Durability works similarly to major databases: compaction forces the OS to physically flush data to disk, while appends to the data file do not (the OS is responsible for flushing the data). That guarantees that a server crash can never cause complete data loss, while preserving performance. The worst that can happen is a crash between two syncs, causing a loss of all data between the two syncs. Usually syncs are 30 seconds appart so that's at most 30 seconds of data. <a href="http://oldblog.antirez.com/post/redis-persistence-demystified.html" target="_blank">This post by Antirez on Redis persistence</a> explains this in more details, NeDB being very close to Redis AOF persistence with <code>appendfsync</code> option set to <code>no</code>.</p>
<h3>Inserting documents</h3>
<p>The native types are <code>String</code>, <code>Number</code>, <code>Boolean</code>, <code>Date</code> and <code>null</code>. You can also use
arrays and subdocuments (objects). If a field is <code>undefined</code>, it will not be saved (this is different from
MongoDB which transforms <code>undefined</code> in <code>null</code>, something I find counter-intuitive).</p>
<p>If the document does not contain an <code>_id</code> field, NeDB will automatically generated one for you (a 16-characters alphanumerical string). The <code>_id</code> of a document, once set, cannot be modified.</p>
<p>Field names cannot begin by '$' or contain a '.'.</p>
<div><pre>var doc = { hello: 'world'
               , n: 5
               , today: new Date()
               , nedbIsAwesome: true
               , notthere: null
               , notToBeSaved: undefined  // Will not be saved
               , fruits: [ 'apple', 'orange', 'pear' ]
               , infos: { name: 'nedb' }
               };

db.insert(doc, function (err, newDoc) {   // Callback is optional
  // newDoc is the newly inserted document, including its _id
  // newDoc has no key called notToBeSaved since its value was undefined
});</pre></div>
<p>You can also bulk-insert an array of documents. This operation is atomic, meaning that if one insert fails due to a unique constraint being violated, all changes are rolled back.</p>
<div><pre>db.insert([{ a: 5 }, { a: 42 }], function (err, newDocs) {
  // Two documents were inserted in the database
  // newDocs is an array with these documents, augmented with their _id
});

// If there is a unique constraint on field 'a', this will fail
db.insert([{ a: 5 }, { a: 42 }, { a: 5 }], function (err) {
  // err is a 'uniqueViolated' error
  // The database was not modified
});</pre></div>
<h3>Finding documents</h3>
<p>Use <code>find</code> to look for multiple documents matching you query, or <code>findOne</code> to look for one specific document. You can select documents based on field equality or use comparison operators (<code>$lt</code>, <code>$lte</code>, <code>$gt</code>, <code>$gte</code>, <code>$in</code>, <code>$nin</code>, <code>$ne</code>). You can also use logical operators <code>$or</code>, <code>$and</code>, <code>$not</code> and <code>$where</code>. See below for the syntax.</p>
<p>You can use regular expressions in two ways: in basic querying in place of a string, or with the <code>$regex</code> operator.</p>
<p>You can sort and paginate results using the cursor API (see below).</p>
<p>You can use standard projections to restrict the fields to appear in the results (see below).</p>
<h4>Basic querying</h4>
<p>Basic querying means are looking for documents whose fields match the ones you specify. You can use regular expression to match strings.
You can use the dot notation to navigate inside nested documents, arrays, arrays of subdocuments and to match a specific element of an array.</p>
<div><pre>// Let's say our datastore contains the following collection
// { _id: 'id1', planet: 'Mars', system: 'solar', inhabited: false, satellites: ['Phobos', 'Deimos'] }
// { _id: 'id2', planet: 'Earth', system: 'solar', inhabited: true, humans: { genders: 2, eyes: true } }
// { _id: 'id3', planet: 'Jupiter', system: 'solar', inhabited: false }
// { _id: 'id4', planet: 'Omicron Persei 8', system: 'futurama', inhabited: true, humans: { genders: 7 } }
// { _id: 'id5', completeData: { planets: [ { name: 'Earth', number: 3 }, { name: 'Mars', number: 2 }, { name: 'Pluton', number: 9 } ] } }

// Finding all planets in the solar system
db.find({ system: 'solar' }, function (err, docs) {
  // docs is an array containing documents Mars, Earth, Jupiter
  // If no document is found, docs is equal to []
});

// Finding all planets whose name contain the substring 'ar' using a regular expression
db.find({ planet: /ar/ }, function (err, docs) {
  // docs contains Mars and Earth
});

// Finding all inhabited planets in the solar system
db.find({ system: 'solar', inhabited: true }, function (err, docs) {
  // docs is an array containing document Earth only
});

// Use the dot-notation to match fields in subdocuments
db.find({ "humans.genders": 2 }, function (err, docs) {
  // docs contains Earth
});

// Use the dot-notation to navigate arrays of subdocuments
db.find({ "completeData.planets.name": "Mars" }, function (err, docs) {
  // docs contains document 5
});

db.find({ "completeData.planets.name": "Jupiter" }, function (err, docs) {
  // docs is empty
});

db.find({ "completeData.planets.0.name": "Earth" }, function (err, docs) {
  // docs contains document 5
  // If we had tested against "Mars" docs would be empty because we are matching against a specific array element
});


// You can also deep-compare objects. Don't confuse this with dot-notation!
db.find({ humans: { genders: 2 } }, function (err, docs) {
  // docs is empty, because { genders: 2 } is not equal to { genders: 2, eyes: true }
});

// Find all documents in the collection
db.find({}, function (err, docs) {
});

// The same rules apply when you want to only find one document
db.findOne({ _id: 'id1' }, function (err, doc) {
  // doc is the document Mars
  // If no document is found, doc is null
});</pre></div>
<h4>Operators ($lt, $lte, $gt, $gte, $in, $nin, $ne, $exists, $regex)</h4>
<p>The syntax is <code>{ field: { $op: value } }</code> where <code>$op</code> is any comparison operator:</p>
<ul>
<li><code>$lt</code>, <code>$lte</code>: less than, less than or equal</li>
<li><code>$gt</code>, <code>$gte</code>: greater than, greater than or equal</li>
<li><code>$in</code>: member of. <code>value</code> must be an array of values</li>
<li><code>$ne</code>, <code>$nin</code>: not equal, not a member of</li>
<li><code>$exists</code>: checks whether the document posses the property <code>field</code>. <code>value</code> should be true or false</li>
<li><code>$regex</code>: checks whether a string is matched by the regular expression. Contrary to MongoDB, the use of <code>$options</code> with <code>$regex</code> is not supported, because it doesn't give you more power than regex flags. Basic queries are more readable so only use the <code>$regex</code> operator when you need to use another operator with it (see example below)</li>
</ul>
<div><pre>// $lt, $lte, $gt and $gte work on numbers and strings
db.find({ "humans.genders": { $gt: 5 } }, function (err, docs) {
  // docs contains Omicron Persei 8, whose humans have more than 5 genders (7).
});

// When used with strings, lexicographical order is used
db.find({ planet: { $gt: 'Mercury' }}, function (err, docs) {
  // docs contains Omicron Persei 8
})

// Using $in. $nin is used in the same way
db.find({ planet: { $in: ['Earth', 'Jupiter'] }}, function (err, docs) {
  // docs contains Earth and Jupiter
});

// Using $exists
db.find({ satellites: { $exists: true } }, function (err, docs) {
  // docs contains only Mars
});

// Using $regex with another operator
db.find({ planet: { $regex: /ar/, $nin: ['Jupiter', 'Earth'] } }, function (err, docs) {
  // docs only contains Mars because Earth was excluded from the match by $nin
});</pre></div>
<h4>Array fields</h4>
<p>When a field in a document is an array, NeDB first tries to see if the query value is an array to perform an exact match, then whether there is an array-specific comparison function (for now there is only <code>$size</code> and <code>$elemMatch</code>) being used. If not, the query is treated as a query on every element and there is a match if at least one element matches.</p>
<ul>
<li><code>$size</code>: match on the size of the array</li>
<li><code>$elemMatch</code>: matches if at least one array element matches the query entirely</li>
</ul>
<div><pre>// Exact match
db.find({ satellites: ['Phobos', 'Deimos'] }, function (err, docs) {
  // docs contains Mars
})
db.find({ satellites: ['Deimos', 'Phobos'] }, function (err, docs) {
  // docs is empty
})

// Using an array-specific comparison function
// $elemMatch operator will provide match for a document, if an element from the array field satisfies all the conditions specified with the `$elemMatch` operator
db.find({ completeData: { planets: { $elemMatch: { name: 'Earth', number: 3 } } } }, function (err, docs) {
  // docs contains documents with id 5 (completeData)
});

db.find({ completeData: { planets: { $elemMatch: { name: 'Earth', number: 5 } } } }, function (err, docs) {
  // docs is empty
});

// You can use inside #elemMatch query any known document query operator
db.find({ completeData: { planets: { $elemMatch: { name: 'Earth', number: { $gt: 2 } } } } }, function (err, docs) {
  // docs contains documents with id 5 (completeData)
});

// Note: you can't use nested comparison functions, e.g. { $size: { $lt: 5 } } will throw an error
db.find({ satellites: { $size: 2 } }, function (err, docs) {
  // docs contains Mars
});

db.find({ satellites: { $size: 1 } }, function (err, docs) {
  // docs is empty
});

// If a document's field is an array, matching it means matching any element of the array
db.find({ satellites: 'Phobos' }, function (err, docs) {
  // docs contains Mars. Result would have been the same if query had been { satellites: 'Deimos' }
});

// This also works for queries that use comparison operators
db.find({ satellites: { $lt: 'Amos' } }, function (err, docs) {
  // docs is empty since Phobos and Deimos are after Amos in lexicographical order
});

// This also works with the $in and $nin operator
db.find({ satellites: { $in: ['Moon', 'Deimos'] } }, function (err, docs) {
  // docs contains Mars (the Earth document is not complete!)
});</pre></div>
<h4>Logical operators $or, $and, $not, $where</h4>
<p>You can combine queries using logical operators:</p>
<ul>
<li>For <code>$or</code> and <code>$and</code>, the syntax is <code>{ $op: [query1, query2, ...] }</code>.</li>
<li>For <code>$not</code>, the syntax is <code>{ $not: query }</code></li>
<li>For <code>$where</code>, the syntax is <code>{ $where: function () { /* object is "this", return a boolean */ } }</code></li>
</ul>
<div><pre>db.find({ $or: [{ planet: 'Earth' }, { planet: 'Mars' }] }, function (err, docs) {
  // docs contains Earth and Mars
});

db.find({ $not: { planet: 'Earth' } }, function (err, docs) {
  // docs contains Mars, Jupiter, Omicron Persei 8
});

db.find({ $where: function () { return Object.keys(this) &gt; 6; } }, function (err, docs) {
  // docs with more than 6 properties
});

// You can mix normal queries, comparison queries and logical operators
db.find({ $or: [{ planet: 'Earth' }, { planet: 'Mars' }], inhabited: true }, function (err, docs) {
  // docs contains Earth
});
</pre></div>
<h4>Sorting and paginating</h4>
<p>If you don't specify a callback to <code>find</code>, <code>findOne</code> or <code>count</code>, a <code>Cursor</code> object is returned. You can modify the cursor with <code>sort</code>, <code>skip</code> and <code>limit</code> and then execute it with <code>exec(callback)</code>.</p>
<div><pre>// Let's say the database contains these 4 documents
// doc1 = { _id: 'id1', planet: 'Mars', system: 'solar', inhabited: false, satellites: ['Phobos', 'Deimos'] }
// doc2 = { _id: 'id2', planet: 'Earth', system: 'solar', inhabited: true, humans: { genders: 2, eyes: true } }
// doc3 = { _id: 'id3', planet: 'Jupiter', system: 'solar', inhabited: false }
// doc4 = { _id: 'id4', planet: 'Omicron Persei 8', system: 'futurama', inhabited: true, humans: { genders: 7 } }

// No query used means all results are returned (before the Cursor modifiers)
db.find({}).sort({ planet: 1 }).skip(1).limit(2).exec(function (err, docs) {
  // docs is [doc3, doc1]
});

// You can sort in reverse order like this
db.find({ system: 'solar' }).sort({ planet: -1 }).exec(function (err, docs) {
  // docs is [doc1, doc3, doc2]
});

// You can sort on one field, then another, and so on like this:
db.find({}).sort({ firstField: 1, secondField: -1 }) ...   // You understand how this works!</pre></div>
<h4>Projections</h4>
<p>You can give <code>find</code> and <code>findOne</code> an optional second argument, <code>projections</code>. The syntax is the same as MongoDB: <code>{ a: 1, b: 1 }</code> to return only the <code>a</code> and <code>b</code> fields, <code>{ a: 0, b: 0 }</code> to omit these two fields. You cannot use both modes at the time, except for <code>_id</code> which is by default always returned and which you can choose to omit. You can project on nested documents.</p>
<div><pre>// Same database as above

// Keeping only the given fields
db.find({ planet: 'Mars' }, { planet: 1, system: 1 }, function (err, docs) {
  // docs is [{ planet: 'Mars', system: 'solar', _id: 'id1' }]
});

// Keeping only the given fields but removing _id
db.find({ planet: 'Mars' }, { planet: 1, system: 1, _id: 0 }, function (err, docs) {
  // docs is [{ planet: 'Mars', system: 'solar' }]
});

// Omitting only the given fields and removing _id
db.find({ planet: 'Mars' }, { planet: 0, system: 0, _id: 0 }, function (err, docs) {
  // docs is [{ inhabited: false, satellites: ['Phobos', 'Deimos'] }]
});

// Failure: using both modes at the same time
db.find({ planet: 'Mars' }, { planet: 0, system: 1 }, function (err, docs) {
  // err is the error message, docs is undefined
});

// You can also use it in a Cursor way but this syntax is not compatible with MongoDB
db.find({ planet: 'Mars' }).projection({ planet: 1, system: 1 }).exec(function (err, docs) {
  // docs is [{ planet: 'Mars', system: 'solar', _id: 'id1' }]
});

// Project on a nested document
db.findOne({ planet: 'Earth' }).projection({ planet: 1, 'humans.genders': 1 }).exec(function (err, doc) {
  // doc is { planet: 'Earth', _id: 'id2', humans: { genders: 2 } }
});</pre></div>
<h3>Counting documents</h3>
<p>You can use <code>count</code> to count documents. It has the same syntax as <code>find</code>. For example:</p>
<div><pre>// Count all planets in the solar system
db.count({ system: 'solar' }, function (err, count) {
  // count equals to 3
});

// Count all documents in the datastore
db.count({}, function (err, count) {
  // count equals to 4
});</pre></div>
<h3>Updating documents</h3>
<p><code>db.update(query, update, options, callback)</code> will update all documents matching <code>query</code> according to the <code>update</code> rules:</p>
<ul>
<li><code>query</code> is the same kind of finding query you use with <code>find</code> and <code>findOne</code></li>
<li><code>update</code> specifies how the documents should be modified. It is either a new document or a set of modifiers (you cannot use both together, it doesn't make sense!)
<ul>
<li>A new document will replace the matched docs</li>
<li>The modifiers create the fields they need to modify if they don't exist, and you can apply them to subdocs. Available field modifiers are <code>$set</code> to change a field's value, <code>$unset</code> to delete a field, <code>$inc</code> to increment a field's value and <code>$min</code>/<code>$max</code> to change field's value, only if provided value is less/greater than current value. To work on arrays, you have <code>$push</code>, <code>$pop</code>, <code>$addToSet</code>, <code>$pull</code>, and the special <code>$each</code> and <code>$slice</code>. See examples below for the syntax.</li>
</ul>
</li>
<li><code>options</code> is an object with two possible parameters
<ul>
<li><code>multi</code> (defaults to <code>false</code>) which allows the modification of several documents if set to true</li>
<li><code>upsert</code> (defaults to <code>false</code>) if you want to insert a new document corresponding to the <code>update</code> rules if your <code>query</code> doesn't match anything. If your <code>update</code> is a simple object with no modifiers, it is the inserted document. In the other case, the <code>query</code> is stripped from all operator recursively, and the <code>update</code> is applied to it.</li>
<li><code>returnUpdatedDocs</code> (defaults to <code>false</code>, not MongoDB-compatible) if set to true and update is not an upsert, will return the array of documents matched by the find query and updated. Updated documents will be returned even if the update did not actually modify them.</li>
</ul>
</li>
<li><code>callback</code> (optional) signature: <code>(err, numAffected, affectedDocuments, upsert)</code>. <strong>Warning</strong>: the API was changed between v1.7.4 and v1.8. Please refer to the <a href="https://github.com/louischatriot/nedb/wiki/Change-log" target="_blank">change log</a><img src="chrome-extension://mgjbfkmfbcfklmchjdbfhhlegmnhhgpi/images/star-yellow.svg" />7,876 to see the change.
<ul>
<li>For an upsert, <code>affectedDocuments</code> contains the inserted document and the <code>upsert</code> flag is set to <code>true</code>.</li>
<li>For a standard update with <code>returnUpdatedDocs</code> flag set to <code>false</code>, <code>affectedDocuments</code> is not set.</li>
<li>For a standard update with <code>returnUpdatedDocs</code> flag set to <code>true</code> and <code>multi</code> to <code>false</code>, <code>affectedDocuments</code> is the updated document.</li>
<li>For a standard update with <code>returnUpdatedDocs</code> flag set to <code>true</code> and <code>multi</code> to <code>true</code>, <code>affectedDocuments</code> is the array of updated documents.</li>
</ul>
</li>
</ul>
<p><strong>Note</strong>: you can't change a document's _id.</p>
<div><pre>// Let's use the same example collection as in the "finding document" part
// { _id: 'id1', planet: 'Mars', system: 'solar', inhabited: false }
// { _id: 'id2', planet: 'Earth', system: 'solar', inhabited: true }
// { _id: 'id3', planet: 'Jupiter', system: 'solar', inhabited: false }
// { _id: 'id4', planet: 'Omicron Persia 8', system: 'futurama', inhabited: true }

// Replace a document by another
db.update({ planet: 'Jupiter' }, { planet: 'Pluton'}, {}, function (err, numReplaced) {
  // numReplaced = 1
  // The doc #3 has been replaced by { _id: 'id3', planet: 'Pluton' }
  // Note that the _id is kept unchanged, and the document has been replaced
  // (the 'system' and inhabited fields are not here anymore)
});

// Set an existing field's value
db.update({ system: 'solar' }, { $set: { system: 'solar system' } }, { multi: true }, function (err, numReplaced) {
  // numReplaced = 3
  // Field 'system' on Mars, Earth, Jupiter now has value 'solar system'
});

// Setting the value of a non-existing field in a subdocument by using the dot-notation
db.update({ planet: 'Mars' }, { $set: { "data.satellites": 2, "data.red": true } }, {}, function () {
  // Mars document now is { _id: 'id1', system: 'solar', inhabited: false
  //                      , data: { satellites: 2, red: true }
  //                      }
  // Not that to set fields in subdocuments, you HAVE to use dot-notation
  // Using object-notation will just replace the top-level field
  db.update({ planet: 'Mars' }, { $set: { data: { satellites: 3 } } }, {}, function () {
    // Mars document now is { _id: 'id1', system: 'solar', inhabited: false
    //                      , data: { satellites: 3 }
    //                      }
    // You lost the "data.red" field which is probably not the intended behavior
  });
});

// Deleting a field
db.update({ planet: 'Mars' }, { $unset: { planet: true } }, {}, function () {
  // Now the document for Mars doesn't contain the planet field
  // You can unset nested fields with the dot notation of course
});

// Upserting a document
db.update({ planet: 'Pluton' }, { planet: 'Pluton', inhabited: false }, { upsert: true }, function (err, numReplaced, upsert) {
  // numReplaced = 1, upsert = { _id: 'id5', planet: 'Pluton', inhabited: false }
  // A new document { _id: 'id5', planet: 'Pluton', inhabited: false } has been added to the collection
});

// If you upsert with a modifier, the upserted doc is the query modified by the modifier
// This is simpler than it sounds :)
db.update({ planet: 'Pluton' }, { $inc: { distance: 38 } }, { upsert: true }, function () {
  // A new document { _id: 'id5', planet: 'Pluton', distance: 38 } has been added to the collection  
});

// If we insert a new document { _id: 'id6', fruits: ['apple', 'orange', 'pear'] } in the collection,
// let's see how we can modify the array field atomically

// $push inserts new elements at the end of the array
db.update({ _id: 'id6' }, { $push: { fruits: 'banana' } }, {}, function () {
  // Now the fruits array is ['apple', 'orange', 'pear', 'banana']
});

// $pop removes an element from the end (if used with 1) or the front (if used with -1) of the array
db.update({ _id: 'id6' }, { $pop: { fruits: 1 } }, {}, function () {
  // Now the fruits array is ['apple', 'orange']
  // With { $pop: { fruits: -1 } }, it would have been ['orange', 'pear']
});

// $addToSet adds an element to an array only if it isn't already in it
// Equality is deep-checked (i.e. $addToSet will not insert an object in an array already containing the same object)
// Note that it doesn't check whether the array contained duplicates before or not
db.update({ _id: 'id6' }, { $addToSet: { fruits: 'apple' } }, {}, function () {
  // The fruits array didn't change
  // If we had used a fruit not in the array, e.g. 'banana', it would have been added to the array
});

// $pull removes all values matching a value or even any NeDB query from the array
db.update({ _id: 'id6' }, { $pull: { fruits: 'apple' } }, {}, function () {
  // Now the fruits array is ['orange', 'pear']
});
db.update({ _id: 'id6' }, { $pull: { fruits: $in: ['apple', 'pear'] } }, {}, function () {
  // Now the fruits array is ['orange']
});

// $each can be used to $push or $addToSet multiple values at once
// This example works the same way with $addToSet
db.update({ _id: 'id6' }, { $push: { fruits: { $each: ['banana', 'orange'] } } }, {}, function () {
  // Now the fruits array is ['apple', 'orange', 'pear', 'banana', 'orange']
});

// $slice can be used in cunjunction with $push and $each to limit the size of the resulting array.
// A value of 0 will update the array to an empty array. A positive value n will keep only the n first elements
// A negative value -n will keep only the last n elements.
// If $slice is specified but not $each, $each is set to []
db.update({ _id: 'id6' }, { $push: { fruits: { $each: ['banana'], $slice: 2 } } }, {}, function () {
  // Now the fruits array is ['apple', 'orange']
});

// $min/$max to update only if provided value is less/greater than current value
// Let's say the database contains this document
// doc = { _id: 'id', name: 'Name', value: 5 }
db.update({ _id: 'id1' }, { $min: { value: 2 } }, {}, function () {
  // The document will be updated to { _id: 'id', name: 'Name', value: 2 }
});

db.update({ _id: 'id1' }, { $min: { value: 8 } }, {}, function () {
  // The document will not be modified
});</pre></div>
<h3>Removing documents</h3>
<p><code>db.remove(query, options, callback)</code> will remove all documents matching <code>query</code> according to <code>options</code></p>
<ul>
<li><code>query</code> is the same as the ones used for finding and updating</li>
<li><code>options</code> only one option for now: <code>multi</code> which allows the removal of multiple documents if set to true. Default is false</li>
<li><code>callback</code> is optional, signature: err, numRemoved</li>
</ul>
<div><pre>// Let's use the same example collection as in the "finding document" part
// { _id: 'id1', planet: 'Mars', system: 'solar', inhabited: false }
// { _id: 'id2', planet: 'Earth', system: 'solar', inhabited: true }
// { _id: 'id3', planet: 'Jupiter', system: 'solar', inhabited: false }
// { _id: 'id4', planet: 'Omicron Persia 8', system: 'futurama', inhabited: true }

// Remove one document from the collection
// options set to {} since the default for multi is false
db.remove({ _id: 'id2' }, {}, function (err, numRemoved) {
  // numRemoved = 1
});

// Remove multiple documents
db.remove({ system: 'solar' }, { multi: true }, function (err, numRemoved) {
  // numRemoved = 3
  // All planets from the solar system were removed
});

// Removing all documents with the 'match-all' query
db.remove({}, { multi: true }, function (err, numRemoved) {
});</pre></div>
<h3>Indexing</h3>
<p>NeDB supports indexing. It gives a very nice speed boost and can be used to enforce a unique constraint on a field. You can index any field, including fields in nested documents using the dot notation. For now, indexes are only used to speed up basic queries and queries using <code>$in</code>, <code>$lt</code>, <code>$lte</code>, <code>$gt</code> and <code>$gte</code>. The indexed values cannot be of type array of object.</p>
<p>To create an index, use <code>datastore.ensureIndex(options, cb)</code>, where callback is optional and get passed an error if any (usually a unique constraint that was violated). <code>ensureIndex</code> can be called when you want, even after some data was inserted, though it's best to call it at application startup. The options are:</p>
<ul>
<li><strong>fieldName</strong> (required): name of the field to index. Use the dot notation to index a field in a nested document.</li>
<li><strong>unique</strong> (optional, defaults to <code>false</code>): enforce field uniqueness. Note that a unique index will raise an error if you try to index two documents for which the field is not defined.</li>
<li><strong>sparse</strong> (optional, defaults to <code>false</code>): don't index documents for which the field is not defined. Use this option along with "unique" if you want to accept multiple documents for which it is not defined.</li>
<li><strong>expireAfterSeconds</strong> (number of seconds, optional): if set, the created index is a TTL (time to live) index, that will automatically remove documents when the system date becomes larger than the date on the indexed field plus <code>expireAfterSeconds</code>. Documents where the indexed field is not specified or not a <code>Date</code> object are ignored</li>
</ul>
<p>Note: the <code>_id</code> is automatically indexed with a unique constraint, no need to call <code>ensureIndex</code> on it.</p>
<p>You can remove a previously created index with <code>datastore.removeIndex(fieldName, cb)</code>.</p>
<p>If your datastore is persistent, the indexes you created are persisted in the datafile, when you load the database a second time they are automatically created for you. No need to remove any <code>ensureIndex</code> though, if it is called on a database that already has the index, nothing happens.</p>
<div><pre>db.ensureIndex({ fieldName: 'somefield' }, function (err) {
  // If there was an error, err is not null
});

// Using a unique constraint with the index
db.ensureIndex({ fieldName: 'somefield', unique: true }, function (err) {
});

// Using a sparse unique index
db.ensureIndex({ fieldName: 'somefield', unique: true, sparse: true }, function (err) {
});


// Format of the error message when the unique constraint is not met
db.insert({ somefield: 'nedb' }, function (err) {
  // err is null
  db.insert({ somefield: 'nedb' }, function (err) {
    // err is { errorType: 'uniqueViolated'
    //        , key: 'name'
    //        , message: 'Unique constraint violated for key name' }
  });
});

// Remove index on field somefield
db.removeIndex('somefield', function (err) {
});

// Example of using expireAfterSeconds to remove documents 1 hour
// after their creation (db's timestampData option is true here)
db.ensureIndex({ fieldName: 'createdAt', expireAfterSeconds: 3600 }, function (err) {
});

// You can also use the option to set an expiration date like so
db.ensureIndex({ fieldName: 'expirationDate', expireAfterSeconds: 0 }, function (err) {
  // Now all documents will expire when system time reaches the date in their
  // expirationDate field
});
</pre></div>
<p><strong>Note:</strong> the <code>ensureIndex</code> function creates the index synchronously, so it's best to use it at application startup. It's quite fast so it doesn't increase startup time much (35 ms for a collection containing 10,000 documents).</p>
<h2>Browser version</h2>
<p>The browser version and its minified counterpart are in the <code>browser-version/out</code> directory. You only need to require <code>nedb.js</code> or <code>nedb.min.js</code> in your HTML file and the global object <code>Nedb</code> can be used right away, with the same API as the server version:</p>
<pre><code>&lt;script src="nedb.min.js"&gt;&lt;/script&gt;
&lt;script&gt;
  var db = new Nedb();   // Create an in-memory only datastore
  
  db.insert({ planet: 'Earth' }, function (err) {
   db.find({}, function (err, docs) {
     // docs contains the two planets Earth and Mars
   });
  });
&lt;/script&gt;
</code></pre>
<p>If you specify a <code>filename</code>, the database will be persistent, and automatically select the best storage method available (IndexedDB, WebSQL or localStorage) depending on the browser. In most cases that means a lot of data can be stored, typically in hundreds of MB. <strong>WARNING</strong>: the storage system changed between v1.3 and v1.4 and is NOT back-compatible! Your application needs to resync client-side when you upgrade NeDB.</p>
<p>NeDB is compatible with all major browsers: Chrome, Safari, Firefox, IE9+. Tests are in the <code>browser-version/test</code> directory (files <code>index.html</code> and <code>testPersistence.html</code>).</p>
<p>If you fork and modify nedb, you can build the browser version from the sources, the build script is <code>browser-version/build.js</code>.</p>
<h2>Performance</h2>
<h3>Speed</h3>
<p>NeDB is not intended to be a replacement of large-scale databases such as MongoDB, and as such was not designed for speed. That said, it is still pretty fast on the expected datasets, especially if you use indexing. On a typical, not-so-fast dev machine, for a collection containing 10,000 documents, with indexing:</p>
<ul>
<li>Insert: <strong>10,680 ops/s</strong></li>
<li>Find: <strong>43,290 ops/s</strong></li>
<li>Update: <strong>8,000 ops/s</strong></li>
<li>Remove: <strong>11,750 ops/s</strong></li>
</ul>
<p>You can run these simple benchmarks by executing the scripts in the <code>benchmarks</code> folder. Run them with the <code>--help</code> flag to see how they work.</p>
<h3>Memory footprint</h3>
<p>A copy of the whole database is kept in memory. This is not much on the
expected kind of datasets (20MB for 10,000 2KB documents).</p>
<h2>Use in other services</h2>
<ul>

<li>If you mostly use NeDB for logging purposes and don't want the memory footprint of your application to grow too large, you can use <a href="https://github.com/louischatriot/nedb-logger" target="_blank">NeDB Logger</a><img src="chrome-extension://mgjbfkmfbcfklmchjdbfhhlegmnhhgpi/images/star-blue.svg" />35 to insert documents in a NeDB-readable database</li>
<li>If you've outgrown NeDB, switching to MongoDB won't be too hard as it is the same API. Use <a href="https://github.com/louischatriot/nedb-to-mongodb" target="_blank">this utility</a><img src="chrome-extension://mgjbfkmfbcfklmchjdbfhhlegmnhhgpi/images/star-blue.svg" />55 to transfer the data from a NeDB database to a MongoDB collection</li>

</ul>
<h2>Pull requests</h2>
<p>If you submit a pull request, thanks! There are a couple rules to follow though to make it manageable:</p>
<ul>
<li>The pull request should be atomic, i.e. contain only one feature. If it contains more, please submit multiple pull requests. Reviewing massive, 1000 loc+ pull requests is extremely hard.</li>
<li>Likewise, if for one unique feature the pull request grows too large (more than 200 loc tests not included), please get in touch first.</li>
<li>Please stick to the current coding style. It's important that the code uses a coherent style for readability.</li>
<li>Do not include sylistic improvements ("housekeeping"). If you think one part deserves lots of housekeeping, use a separate pull request so as not to pollute the code.</li>
<li>Don't forget tests for your new feature. Also don't forget to run the whole test suite before submitting to make sure you didn't introduce regressions.</li>
<li>Do not build the browser version in your branch, I'll take care of it once the code is merged.</li>
<li>Update the readme accordingly.</li>
<li>Last but not least: keep in mind what NeDB's mindset is! The goal is not to be a replacement for MongoDB, but to have a pure JS database, easy to use, cross platform, fast and expressive enough for the target projects (small and self contained apps on server/desktop/browser/mobile). Sometimes it's better to shoot for simplicity than for API completeness with regards to MongoDB.</li>
</ul>
<h2>Bug reporting guidelines</h2>
<p>If you report a bug, thank you! That said for the process to be manageable please strictly adhere to the following guidelines. I'll not be able to handle bug reports that don't:</p>
<ul>
<li>Your bug report should be a self-containing gist complete with a package.json for any dependencies you need. I need to run through a simple <code>git clone gist; npm install; node bugreport.js</code>, nothing more.</li>
<li>It should use assertions to showcase the expected vs actual behavior and be hysteresis-proof. It's quite simple in fact, see this example: <a href="https://gist.github.com/louischatriot/220cf6bd29c7de06a486" target="_blank">https://gist.github.com/louischatriot/220cf6bd29c7de06a486</a></li>
<li>Simplify as much as you can. Strip all your application-specific code. Most of the time you will see that there is no bug but an error in your code :)</li>
<li>50 lines max. If you need more, read the above point and rework your bug report. If you're <strong>really</strong> convinced you need more, please explain precisely in the issue.</li>
<li>The code should be Javascript, not Coffeescript.</li>
</ul>
<h3>Bitcoins</h3>
<p>You don't have time? You can support NeDB by sending bitcoins to this address: 1dDZLnWpBbodPiN8sizzYrgaz5iahFyb1</p>
<h2>License</h2>
<p>See <a href="/louischatriot/nedb/blob/master/LICENSE" target="_blank">License</a></p>

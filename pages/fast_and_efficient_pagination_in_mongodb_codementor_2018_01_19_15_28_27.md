<a href="https://www.codementor.io/arpitbhayani/fast-and-efficient-pagination-in-mongodb-9095flbqr">https://www.codementor.io/arpitbhayani/fast-and-efficient-pagination-in-mongodb-9095flbqr</a><div id="articleHeader"><h1>Fast and Efficient Pagination in MongoDB</h1></div><div><div><small>Published Jun 13, 2017</small></div><div><div><div class="readableLargeImageContainer"><img src="https://process.filestackapi.com/cache=expiry:max/resize=width:20/DaH9QAEcSmimAd617cj8" alt="Fast and Efficient Pagination in MongoDB" /></div><div class="readableLargeImageContainer"><img src="https://process.filestackapi.com/cache=expiry:max/resize=width:1050/compress/DaH9QAEcSmimAd617cj8" alt="Fast and Efficient Pagination in MongoDB" /></div><div><div><div><p><a href="https://www.mongodb.com/" target="_blank">MongoDB</a> is a document based data store and hence pagination is one of the most common use case of it. So when do you paginate the response? The answer is pretty neat; you paginate whenever you want to process result in chunks. Some common scenarios are</p>
<ul>
<li>Batch processing</li>
<li>Showing huge set of results on user interface</li>
</ul>
<p>Paginating on client and server side are both really very expensive and should not be considered. Hence pagination is generally handled at database level and databases are optimized for such needs too.</p>
<p>Below I shall explain you the 2 approaches through which you can easily paginate your MongoDB responses.<br />
Sample Document</p>
<pre><code>    {
        "_id" : ObjectId("5936d17263623919cd5165bd"),
        "name" : "Lisa Rogers",
        "marks" : 34
    }
</code></pre>
<h2 id="approach-1-using-cursorskip-and-cursorlimit"> Approach 1: Using <code>cursor.skip</code> and <code>cursor.limit</code></h2>
<p>MongoDB cursor has two methods that makes paging easy; they are</p>
<ul>
<li><code>cursor.skip()</code></li>
<li><code>cursor.limit()</code></li>
</ul>
<p><code>skip(n)</code> will skip <code>n</code> documents from the cursor while <code>limit(n)</code> will cap the number of documents to be returned from the cursor. Thus combination of two naturally paginates the response.</p>
<p>In Mongo Shell your pagination code looks something like this</p>
<pre><code>    // Page 1
    db.students.find().limit(5)

    // Page 2
    db.students.find().skip(5).limit(5)

    // Page 3
    db.students.find().skip(5).limit(5)
</code></pre>
<p><code>.find()</code> will return a cursor pointing to all documents of the collection and then for each page we skip some and consume some. Through continuous skip and limit we get pagination in MongoDB.</p>
<p>I am fond of Python and hence here is a small trivial function to implement pagination:</p>
<pre><code>    def skiplimit(page_size, page_num):
        """returns a set of documents belonging to page number `page_num`
        where size of each page is `page_size`.
        """
        # Calculate number of documents to skip
        skips = page_size * (page_num - 1)

        # Skip and limit
        cursor = db['students'].find().skip(skips).limit(page_size)

        # Return documents
        return [x for x in cursor]
</code></pre>
<h2 id="approach-2-using-id-and-limit"> Approach 2: Using <code>_id</code> and <code>limit</code></h2>
<p>This approach will make effective use of default index on <code>_id</code> and nature of <code>ObjectId</code>.<br />
I bet you didn’t know that a <a href="https://docs.mongodb.com/manual/reference/bson-types/#objectid" target="_blank">Mongodb ObjectId</a> is a 12 byte structure containing</p>
<ul>
<li>a 4-byte value representing the seconds since the Unix epoch,</li>
<li>a 3-byte machine identifier,</li>
<li>a 2-byte process id, and</li>
<li>a 3-byte counter, starting with a random value.</li>
</ul>
<p>Even I didn’t until I read the <a href="https://docs.mongodb.com/manual/reference/bson-types/#objectid" target="_blank">documentation</a>. Apart from its structure there is one very interesting property of ObjectId; which is - <em>ObjectId has natural ordering</em></p>
<p>What does it mean? It simplifies that we can apply all the <em>less-than-s</em> and all the <em>greater-than-s you</em> want to it. If you don’t believe me, open Mongo shell and execute following set of commands</p>
<pre><code>    &gt; ObjectId("5936d49863623919cd56f52d") &gt;  ObjectId("5936d49863623919cd56f52e")
    false
    &gt; ObjectId("5936d49863623919cd56f52d") &gt;  ObjectId("5936d49863623919cd56f52a")
    true
</code></pre>
<p>Using this property of ObjectId and also taking into consideration the fact that <code>_id</code> is always indexed, we can devise following approach for pagination:</p>
<ol>
<li>Fetch a page of documents from database</li>
<li>Get the document id of the last document of the page</li>
<li>Retrieve documents greater than that id</li>
</ol>
<p>In Mongo Shell your pagination code looks something like this</p>
<pre><code>    // Page 1
    db.students.find().limit(10)

    // Page 2
    last_id = ...  # logic to get last_id
    db.students.find({'_id': {'$gt': last_id}}).limit(10)

    // Page 3
    last_id = ... # logic to get last_id
    db.students.find({'_id': {'$gt': last_id}}).limit(10)
</code></pre>
<p>Again, I am fond of Python and here is the Python implementation of this approach.</p>
<pre><code>    def idlimit(page_size, last_id=None):
        """Function returns `page_size` number of documents after last_id
        and the new last_id.
        """
        if last_id is None:
            # When it is first page
            cursor = db['students'].find().limit(page_size)
        else:
            cursor = db['students'].find({'_id': {'$gt': last_id}}).limit(page_size)

        # Get the data      
        data = [x for x in cursor]

        if not data:
            # No documents left
            return None, None

        # Since documents are naturally ordered with _id, last document will
        # have max id.
        last_id = data[-1]['_id']

        # Return data and last_id
        return data, last_id
</code></pre>
<blockquote>
<p>If you are using a field other than <code>_id</code> for offset, make sure the field is indexed and properly ordered else the performance will suffer.</p>
</blockquote>
<h2 id="closing-remarks"> Closing Remarks</h2>
<p>Both of the above approaches are valid and correct. But as we know, in field of Computer Science, whenever there are multiple options to achieve something, one always outperforms the other. Same is the situation here as well.</p>
<p>Turns out, there is a severe problem with skip function. I have tried to jot it down in <a href="http://arpitbhayani.me/techie/mongodb-cursor-skip-is-slow.html" target="_blank">this blog post</a>. Because of which second approach has advantage over first. But that is not it; I wrote a simple <a href="https://github.com/arpitbbhayani/mongo-pagination-benchmark" target="_blank">python code</a> to benchmark the two approaches for various combinations and it turns out <code>skip</code> performs better in some case. The results are compiled into <a href="http://arpitbhayani.me/techie/benchmark-and-compare-pagination-approach-in-mongodb.html" target="_blank">this blog post</a>.</p>
<p>This article is originally pupblished on my blog <a href="http://arpitbhayani.me/techie/fast-and-efficient-pagination-in-mongodb.html" target="_blank">Amazon's Kinesis and SQS - Which one should you choose and when?</a>. To read more of my blog post, visit <a href="http://arpitbhayani.me" target="_blank">arpitbhayani.me</a>.</p>
</div>
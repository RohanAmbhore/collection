<a href="https://mixmax.com/blog/api-paging-built-the-right-way">https://mixmax.com/blog/api-paging-built-the-right-way</a><div id="articleHeader"><h1>API Paging Built The Right Way</h1></div>

          
            
              <p><b>Wednesday, Sep 13th, 2017</b></p>

              <p><em>Mixmax is a communications platform that brings professional communication & email into the 21st century.</em></p>
              <p>Mixmax has a very extensive <a href="https://developer.mixmax.com/docs/getting-started-with-the-api" target="_blank">list of APIs</a> that give our users direct access to all of their data. Some APIs, such as <a href="https://developer.mixmax.com/docs/contacts" target="_blank">Contacts</a> can return <em>millions</em> of results. We obviously can't return all of them at once, so we need to return a subset - or a <em>page</em> - at a time. This technique is called <em>paging</em> and is common to most APIs. Paging can be implemented in many different ways, some better than others. In this post we discuss various implementation approaches and how we ultimately implemented our own approach to serve data stored in <a href="https://www.mongodb.com/" target="_blank">MongoDB</a>. We also introduce a <a href="https://github.com/mixmaxhq/mongo-cursor-pagination" target="_blank">new npm module</a> to easily allow you to do the same.</p>
<h4>Common paging implementation approach #1: Offset-based paging (“numbered pages”)</h4>
<p>This is one of the more common pagination approaches. The caller of the API passes a <code>page</code>  (aka <code>offset</code> or <code>skip</code>) and <code>limit</code> (aka <code>count</code> or <code>per_page</code>) parameters. The limit is the number of results it wants and the offset is how many items to “skip” over before starting to return results. For example, Github offers an <a href="https://developer.github.com/v3/#pagination" target="_blank">offset-based</a> API for fetching Github Repos that looks like this:</p>
<p><code>curl https://api.github.com/user/repos?page=2&per_page=100</code></p>
<p>This pattern has a big flaw: if the results list has changed between calls to the API, the indices would shift and cause an item to be either returned twice or skipped and never returned. So in the above example, if a Github repo is deleted after you query the first page of results, then the previous 101st entry (that wasn’t in your original first page of 100) will now be the 100th entry, so it won’t be included in your second page of results (that starts at 101).</p>
<h4>Common paging implementation approach #2: Time-based paging</h4>
<p>A second approach is time-based paging. So if your API (in this case, /items) returns results sorted by newest-first, you could pass the <code>created</code> date of the last item in the list to get the next page of items created before it:</p>
<p>Example API</p>
<p><code>curl https://api.mywebsite.com/items?created_before_timestamp=1505086265160&limit=50</code></p>
<p>This solves the problem in Common Approach #1 above because results are no longer skipped. If you query the first page, and then a new item is deleted, it won’t shift the results in your second page and all is fine. However, this approach has a major flaw: what if there is more than one item that was created at the same time? So if there were 51 items with the <code>created</code> timestamp of exactly <code>1505086265160</code>, then when we query the next page, we’ll miss the 51st entry because we’re querying items created before 1505086265160. You’ll miss results.</p>
<h4>The right approach: Cursor-based paging</h4>
<p>The best way to build API pagination in a safe way is for the API to return a “cursor”, or opaque string, with the list of results. This token is usually called <a href="https://developer.mixmax.com/docs/getting-started-with-the-api#pagination" target="_blank"><code>next</code></a> or <a href="https://dev.twitter.com/overview/api/cursoring" target="_blank"><code>next_cursor</code></a> or <a href="https://stripe.com/docs/api#pagination-starting_after" target="_blank"><code>starting_after</code></a> This token can be passed with the next API request to request the next page.</p>
<p>Here’s an example from the Twitter API:</p>
<p><code>curl https://api.twitter.com/1.1/followers/ids.json?screen_name=theSeanCook&cursor=1374004777531007833</code></p>
<p>By returning a “cursor”, the API guarantees that it will return the exactly the next entry in the list, regardless of what changes happen to the collection between API calls. Think of the cursor as permanent marker in the list that says “we left off here”.</p>
<h3>Implementing cursor-based pagination (in MongoDB)</h3>
<p>So we’ve described cursors as the right approach for API pagination, but how do we actually implement them? If you happen to be using Node and MongoDB, you’re in luck, because we recently published a library that will do it for you. It’s called <a href="https://github.com/mixmaxhq/mongo-cursor-pagination" target="_blank">mongo-cursor-pagination</a>. I’ll briefly describe how it’s implemented and our thinking behind it.</p>
<p>Since a cursor is just a marker to say “we left off here”, we can simply make it the value of a field in the collection. However, that field must satisfy the following properties:</p>
<ul>
<li><p><strong>Unique.</strong> This value must be unique for all documents in the collection. Otherwise we’ll run into the problem in Common Approach #2: if multiple documents have the same value, then we can’t “pick up exactly where we left off” because not all documents can be distinguished from one another. This also means that all documents must have this field set to something, otherwise MongoDB considers it null.</p>
</li>
<li><p><strong>Orderable.</strong> Every value of this field must be able to be compared to every other value. This is because we need to sort by this field in order to get a list of results to then return in pages. If the field is a number <code>int</code>, <code>string</code>, or any other sortable datatype in MongoDB, then it satisfies this.</p>
</li>
<li><p><strong>Immutable.</strong> The value in this field cannot change, otherwise the pages wouldn’t return the right information. For example, if you select the field “name” as the cursor field, and a name is changed while someone is fetching results, then that entry might be skipped.</p>
</li>
</ul>
<p>So let’s say that we’re choosing the standard MongoDB field <code>_id</code> for cursor pagination. This is a reasonable choice as it satisfies the above criteria and always exists on all documents in MongoDB. In this example, we’ll implement an API that returns 2 items. It will return a “cursor” (really just the string value of the last <code>_id</code>) that the caller can pass to get the next page:</p>
<p><code>curl https://api.mixmax.com/items?limit=2</code></p>
<pre><code>const items = db.items.find({}).sort({
   _id: -1
}).limit(2);

const next = items[items.length - 1]._id
res.json({ items, next })
</code></pre>
<p>Then, when the user wants to get the second page, they pass the cursor (as <code>next</code>) on the URL:</p>
<p><code>curl https://api.mixmax.com/items?limit=2&next=590e9abd4abbf1165862d342</code></p>
<pre><code>const items = db.items.find({
  _id: { $lt: req.query.next }
}).sort({
   _id: -1
}).limit(2);

const next = items[items.length - 1]._id
res.json({ items, next })
</code></pre>
<p>This solution works great because we’re returning results sorted by <code>_id</code>, which in MongoDB happens to the creation time rounded to the nearest second plus some other entropy. But let’s say we want to return results in a different order, such as the date the item was introduced into an online store, <code>launchDate</code>. To make it clear in the example, we’ll add <code>sort=launchDate</code> to the querystring:</p>
<p><code>curl https://api.mixmax.com/items?limit=2&sort=launchDate</code></p>
<pre><code>const items = db.items.find({}).sort({
   launchDate: -1
}).limit(2);

const next = items[items.length - 1].launchDate;
res.json({ items, next })
</code></pre>
<p>Then, to fetch the second page, they’d pass the <code>next</code> cursor (which happens to be launch date encoded as a string):</p>
<p><code>curl https://api.mixmax.com/items?limit=2&sort=launchDate&next=2017-09-11T00%3A44%3A54.036Z</code></p>
<pre><code>const items = db.items.find({
  launchDate: { $lt: req.query.next }
}).sort({
   _id: -1
}).limit(2);

const next = items[items.length - 1].launchDate;
res.json({ items, next });
</code></pre>
<p>However, what if we launched a bunch of items on the same day and time? Now our <code>launchDate</code> field is no longer unique and doesn’t satisfy the above requirements. We can’t use it as a cursor field. But wait, there is a way: we could use two fields to generate the cursor! Since we know that the <code>_id</code> field in MongoDB always satisfies the above three criteria, we know that if we use it alongside our <code>launchDate</code> field, the combination of the two fields would satisfy the requirements and could be together used as a cursor field. This would also allow the user to continue to get the response sorted by <code>launchDate</code>:</p>
<p><code>curl https://api.mixmax.com/items?limit=2&sort=launchDate</code></p>
<pre><code>const items = db.items.find({}).sort({
   launchDate: -1,
  _id: -1 // secondary sort in case there are duplicate launchDate values
}).limit(2);

const lastItem = items[items.length - 1];
// The cursor is a concatenation of the two cursor fields, since both are needed to satisfy the requirements of being a cursor field
const next = `${lastItem.launchDate}_${lastItem._id}`;
res.json({ items, next });
</code></pre>
<p>Then to fetch the subsequent page we’d call:</p>
<p><code>curl https://api.mixmax.com/items?limit=2&sort=launchDate&next=2017-09-11T00%3A44%3A54.036Z_590e9abd4abbf1165862d342</code></p>
<pre><code>const [nextLaunchDate, nextId] = req.query.next.split(‘_’);
const items = db.items.find({
  $or: [{
    launchDate: { $lt: nextLaunchDate }
  }, {
    // If the launchDate is an exact match, we need a tiebreaker, so we use the _id field from the cursor.
    launchDate: nextLaunchDate,
  _id: { $lt: nextId }
  }]
}).sort({
   _id: -1
}).limit(2);

const lastItem = items[items.length - 1];
// The cursor is a concatenation of the two cursor fields, since both are needed to satisfy the requirements of being a cursor field
const next = `${lastItem.launchDate}_${lastItem._id}`;
res.json({ items, next });
</code></pre>
<p>Now we have exactly what we want: an API that allows the user to get paginated results sorted by launch date. As new items are launched and old items are deleted, the paged results won’t be disrupted and an item will never be duplicated or missed in a response.</p>
<p>The above code examples explain our thinking behind building the <a href="https://github.com/mixmaxhq/mongo-cursor-pagination" target="_blank">mongo-cursor-pagination</a> library. If you use the library, you won’t need to write the above code - the module will do it for you. We’re already using mongo-cursor-pagination at Mixmax to serve millions of documents via our <a href="https://developer.mixmax.com/" target="_blank">developer API</a>.</p>
<h3>A note about MongoDB indexes</h3>
<p>When using the module that runs queries similar the example code above, it’s important that you create the proper MongoDB indexes. This is especially important for large collections (&gt;1k records) as you might accidentally slow your database. So for the above query, always be sure to create a index (as explained <a href="https://github.com/mixmaxhq/mongo-cursor-pagination#indexes-for-sorting" target="_blank">here</a>) that covers all the properties used in the query along with the cursor field (called the paginatedField in the module) and the <code>_id</code> field.</p>
<h2>Conclusion</h2>
<p>Using our cursor-based paging technique and MongoDB, we're able to serve millions of API requests a day. Our <a href="http://developer.mixmax.com" target="_blank">APIs</a> respond in the same amount of time regardless of how many resources they're serving, or which page is be queried.</p>
<p><em>Do you want to create cool open source modules with us? <a href="https://mixmax.com/careers" target="_blank">Drop us a line</a>.</em></p>

              <ul>
                <li>
                  Share on
                </li>
                
                
                
              </ul>
            
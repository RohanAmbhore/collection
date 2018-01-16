<a href="https://www.elastic.co/guide/en/elasticsearch/reference/6.x/removal-of-types.html">https://www.elastic.co/guide/en/elasticsearch/reference/6.x/removal-of-types.html</a><div id="articleHeader"><h1>Elasticsearch Reference [6.x]</h1></div>
            
<div>You are looking at preliminary documentation for a future release.
Not what you want? See the
<a href="../current/index.html" target="_blank">current release documentation</a>.
</div><div><div><div><h2>Removal of mapping types<a href="https://github.com/elastic/elasticsearch/edit/6.x/docs/reference/mapping/removal_of_types.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h2></div></div></div><div><div><img src="images/icons/important.png" alt="Important" /></div><div><p>Indices created in Elasticsearch 6.0.0 or later may only contain a
single <a href="mapping.html#mapping-type" title="Mapping Typeedit" target="_blank">mapping type</a>.  Indices created in 5.x with multiple
mapping types will continue to function as before in Elasticsearch 6.x.
Mapping types will be completely removed in Elasticsearch 7.0.0.</p></div></div><h3>What are mapping types?<a href="https://github.com/elastic/elasticsearch/edit/6.x/docs/reference/mapping/removal_of_types.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h3><p>Since the first release of Elasticsearch, each document has been stored in a
single index and assigned a single mapping type.  A mapping type was used to
represent the type of document or entity being indexed, for instance a
<code>twitter</code> index might have a <code>user</code> type and a <code>tweet</code> type.</p><p>Each mapping type could have its own fields, so the <code>user</code> type might have a
<code>full_name</code> field, a <code>user_name</code> field, and an <code>email</code> field, while the
<code>tweet</code> type could have a <code>content</code> field, a <code>tweeted_at</code> field and, like the
<code>user</code> type, a <code>user_name</code> field.</p><p>Each document had a <code>_type</code> meta-field containing the type name, and searches
could be limited to one or more types by specifying the type name(s) in the
URL:</p><div><pre>GET twitter/user,tweet/_search
{
  "query": {
    "match": {
      "user_name": "kimchy"
    }
  }
}</pre></div><p>The <code>_type</code> field was combined with the document’s <code>_id</code> to generate a <code>_uid</code>
field, so documents of different types with the same <code>_id</code> could exist in a
single index.</p><p>Mapping types were also used to establish a
<a href="mapping-parent-field.html" title="_parent field" target="_blank">parent-child relationship</a>
between documents, so documents of type <code>question</code> could be parents to
documents of type <code>answer</code>.</p><h3>Why are mapping types being removed?<a href="https://github.com/elastic/elasticsearch/edit/6.x/docs/reference/mapping/removal_of_types.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h3><p>Initially, we spoke about an “index” being similar to a “database” in an
SQL database, and a “type” being equivalent to a
“table”.</p><p>This was a bad analogy that led to incorrect assumptions. In an SQL database,
tables are independent of each other.  The columns in one table have no
bearing on columns with the same name in another table.  This is not the case
for fields in a mapping type.</p><p>In an Elasticsearch index, fields that have the same name in different mapping
types are backed by the same Lucene field internally.  In other words, using
the example above, the <code>user_name</code> field in the <code>user</code> type is stored in
exactly the same field as the <code>user_name</code> field in the <code>tweet</code> type, and both
<code>user_name</code> fields must have the same mapping (definition) in both types.</p><p>This can lead to frustration when, for example, you want <code>deleted</code> to be a
<code>date</code> field in one type and a <code>boolean</code> field in another type in the same
index.</p><p>On top of that, storing different entities that have few or no fields in
common in the same index leads to sparse data and interferes with Lucene’s
ability to compress documents efficiently.</p><p>For these reasons, we have decided to remove the concept of mapping types from
Elasticsearch.</p><h3>Alternatives to mapping types<a href="https://github.com/elastic/elasticsearch/edit/6.x/docs/reference/mapping/removal_of_types.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h3><h4>Index per document type<a href="https://github.com/elastic/elasticsearch/edit/6.x/docs/reference/mapping/removal_of_types.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>The first alternative is to have an index per document type.  Instead of
storing tweets and users in a single <code>twitter</code> index, you could store tweets
in the <code>tweets</code> index and users in the <code>user</code> index. Indices are completely
independent of each other and so there will be no conflict of field types
between indices.</p><p>This approach has two benefits:</p><div><ul><li>
Data is more likely to be dense and so benefit from compression techniques
  used in Lucene.
</li><li>
The term statistics used for scoring in full text search are more likely to
  be accurate because all documents in the same index represent a single
  entity.
</li></ul></div><p>Each index can be sized appropriately for the number of documents it will
contain: you can use a smaller number of primary shards for <code>users</code> and a
larger number of primary shards for <code>tweets</code>.</p><h4>Custom type field<a href="https://github.com/elastic/elasticsearch/edit/6.x/docs/reference/mapping/removal_of_types.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>Of course, there is a limit to how many primary shards can exist in a cluster
so you may not want to waste an entire shard for a collection of only a few
thousand documents.  In this case, you can implement your own custom <code>type</code>
field which will work in a similar way to the old <code>_type</code>.</p><p>Let’s take the <code>user</code>/<code>tweet</code> example above.  Originally, the workflow would
have looked something like this:</p><div><pre>PUT twitter
{
  "mappings": {
    "user": {
      "properties": {
        "name": { "type": "text" },
        "user_name": { "type": "keyword" },
        "email": { "type": "keyword" }
      }
    },
    "tweet": {
      "properties": {
        "content": { "type": "text" },
        "user_name": { "type": "keyword" },
        "tweeted_at": { "type": "date" }
      }
    }
  }
}

PUT twitter/user/kimchy
{
  "name": "Shay Banon",
  "user_name": "kimchy",
  "email": "shay@kimchy.com"
}

PUT twitter/tweet/1
{
  "user_name": "kimchy",
  "tweeted_at": "2017-10-24T09:00:00Z",
  "content": "Types are going away"
}

GET twitter/tweet/_search
{
  "query": {
    "match": {
      "user_name": "kimchy"
    }
  }
}</pre></div><p>You could achieve the same thing by adding a custom <code>type</code> field as follows:</p><div><pre>PUT twitter
{
  "mappings": {
    "_doc": {
      "properties": {
        "type": { "type": "keyword" }, <img src="images/icons/callouts/1.png" />
        "name": { "type": "text" },
        "user_name": { "type": "keyword" },
        "email": { "type": "keyword" },
        "content": { "type": "text" },
        "tweeted_at": { "type": "date" }
      }
    }
  }
}

PUT twitter/_doc/user-kimchy
{
  "type": "user", <img src="images/icons/callouts/2.png" />
  "name": "Shay Banon",
  "user_name": "kimchy",
  "email": "shay@kimchy.com"
}

PUT twitter/_doc/tweet-1
{
  "type": "tweet", <img src="images/icons/callouts/3.png" />
  "user_name": "kimchy",
  "tweeted_at": "2017-10-24T09:00:00Z",
  "content": "Types are going away"
}

GET twitter/_search
{
  "query": {
    "bool": {
      "must": {
        "match": {
          "user_name": "kimchy"
        }
      },
      "filter": {
        "match": {
          "type": "tweet" <img src="images/icons/callouts/4.png" />
        }
      }
    }
  }
}</pre></div><div><table><tbody><tr><td></td><td><p>
The explicit <code>type</code> field takes the place of the implicit <code>_type</code> field.
</p></td></tr></tbody></table></div><h4>Parent/Child without mapping types<a href="https://github.com/elastic/elasticsearch/edit/6.x/docs/reference/mapping/removal_of_types.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>Previously, a parent-child relationship was represented by making one mapping
type the parent, and one or more other mapping types the children.  Without
types, we can no longer use this syntax.  The parent-child feature will
continue to function as before, except that the way of expressing the
relationship between documents has been changed to use the new
<a href="parent-join.html" title="join datatype" target="_blank"><code>join</code> field</a>.</p><h3>Schedule for removal of mapping types<a href="https://github.com/elastic/elasticsearch/edit/6.x/docs/reference/mapping/removal_of_types.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h3><p>This is a big change for our users, so we have tried to make it as painless as
possible.  The change will roll out as follows:</p><div><dl><dt>
Elasticsearch 5.6.0
</dt><dd><div><ul><li>
Setting <code>index.mapping.single_type: true</code> on an index will enable the
  single-type-per-index behaviour which will be enforced in 6.0.
</li><li>
The <a href="parent-join.html" title="join datatype" target="_blank"><code>join</code> field</a> replacement for parent-child is available
  on indices created in 5.6.
</li></ul></div></dd><dt>
Elasticsearch 6.x
</dt><dd><div><ul><li>
Indices created in 5.x will continue to function in 6.x as they did in 5.x.
</li><li>
Indices created in 6.x only allow a single-type per index.  Any name
  can be used for the type, but there can be only one. The preferred type name
  is <code>_doc</code>, so that index APIs have the same path as they will have in 7.0:
  <code>PUT {index}/_doc/{id}</code> and <code>POST {index}/_doc</code>
</li><li>
The <code>_type</code> name can no longer be combined with the <code>_id</code> to form the <code>_uid</code>
  field. The <code>_uid</code> field has become an alias for the <code>_id</code> field.
</li><li>
New indices no longer support the old-style of parent/child and should
  use the <a href="parent-join.html" title="join datatype" target="_blank"><code>join</code> field</a> instead.
</li><li>
The <code>_default_</code> mapping type is deprecated.
</li></ul></div></dd><dt>
Elasticsearch 7.x
</dt><dd><div><ul><li>
The <code>type</code> parameter in URLs are optional.  For instance, indexing
  a document no longer requires a document <code>type</code>.  The new index APIs
  are <code>PUT {index}/_doc/{id}</code> in case of explicit ids and <code>POST {index}/_doc</code>
  for auto-generated ids.
</li><li>
The <code>GET|PUT _mapping</code> APIs support a query string parameter
  (<code>include_type_name</code>) which indicates whether the body should include
  a layer for the type name. It defaults to <code>true</code>. 7.x indices which
  don’t have an explicit type will use the dummy type name <code>_doc</code>.
</li><li>
The <code>_default_</code> mapping type is removed.
</li></ul></div></dd><dt>
Elasticsearch 8.x
</dt><dd><div><ul><li>
The <code>type</code> parameter is no longer supported in URLs.
</li><li>
The <code>include_type_name</code> parameter defaults to <code>false</code>.
</li></ul></div></dd><dt>
Elasticsearch 9.x
</dt><dd><div><ul><li>
The <code>include_type_name</code> parameter is removed.
</li></ul></div></dd></dl></div><h3>Migrating multi-type indices to single-type<a href="https://github.com/elastic/elasticsearch/edit/6.x/docs/reference/mapping/removal_of_types.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h3><p>The <a href="docs-reindex.html" title="Reindex API" target="_blank">Reindex API</a> can be used to convert multi-type indices to
single-type indices. The following examples can be used in Elasticsearch 5.6
or Elasticsearch 6.x.  In 6.x, there is no need to specify
<code>index.mapping.single_type</code> as that is the default.</p><h4>Index per document type<a href="https://github.com/elastic/elasticsearch/edit/6.x/docs/reference/mapping/removal_of_types.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>This first example splits our <code>twitter</code> index into a <code>tweets</code> index and a
<code>users</code> index:</p><div><pre>PUT users
{
  "settings": {
    "index.mapping.single_type": true
  },
  "mappings": {
    "_doc": {
      "properties": {
        "name": {
          "type": "text"
        },
        "user_name": {
          "type": "keyword"
        },
        "email": {
          "type": "keyword"
        }
      }
    }
  }
}

PUT tweets
{
  "settings": {
    "index.mapping.single_type": true
  },
  "mappings": {
    "_doc": {
      "properties": {
        "content": {
          "type": "text"
        },
        "user_name": {
          "type": "keyword"
        },
        "tweeted_at": {
          "type": "date"
        }
      }
    }
  }
}

POST _reindex
{
  "source": {
    "index": "twitter",
    "type": "user"
  },
  "dest": {
    "index": "users"
  }
}

POST _reindex
{
  "source": {
    "index": "twitter",
    "type": "tweet"
  },
  "dest": {
    "index": "tweets"
  }
}</pre></div><h4>Custom type field<a href="https://github.com/elastic/elasticsearch/edit/6.x/docs/reference/mapping/removal_of_types.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>This next example adds a custom <code>type</code> field and sets it to the value of the
original <code>_type</code>.  It also adds the type to the <code>_id</code> in case there are any
documents of different types which have conflicting IDs:</p><div><pre>PUT new_twitter
{
  "mappings": {
    "_doc": {
      "properties": {
        "type": {
          "type": "keyword"
        },
        "name": {
          "type": "text"
        },
        "user_name": {
          "type": "keyword"
        },
        "email": {
          "type": "keyword"
        },
        "content": {
          "type": "text"
        },
        "tweeted_at": {
          "type": "date"
        }
      }
    }
  }
}


POST _reindex
{
  "source": {
    "index": "twitter"
  },
  "dest": {
    "index": "new_twitter"
  },
  "script": {
    "source": """
      ctx._source.type = ctx._type;
      ctx._id = ctx._type + '-' + ctx._id;
      ctx._type = '_doc';
    """
  }
}</pre></div>
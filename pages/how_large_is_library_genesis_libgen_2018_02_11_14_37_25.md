<a href="https://www.reddit.com/r/libgen/comments/5enkqr/how_large_is_library_genesis/">https://www.reddit.com/r/libgen/comments/5enkqr/how_large_is_library_genesis/</a><div id="articleHeader"><h1>How large is Library Genesis? </h1></div><div><div><p>This is an archived post. You won't be able to vote or comment.</p>
</div>
</div><div id="siteTable"><div id="thing_t3_5enkqr"><br /><br /><div><div><div><div><p>There are around 50-55 million papers on Sci-Hub. Does anyone know how many book titles Libgen has? Growth statistics also welcome.</p>
</div>
</div></div></div></div></div><div>all 15 comments</div><div><div>sorted by: </div></div><div><p><a href="javascript:void(0)" target="_blank">[–]</a><a href="https://www.reddit.com/user/ebookfarm" target="_blank">ebookfarm</a> 5 points <time>1 year ago</time><time>*</time> <a href="javascript:void(0)" target="_blank">(8 children)</a></p><div><div><p>I havent checked in a while but from a database dump from few weeks ago (using SQL):
1,571,314 books taking 20.43 TB</p>

<p>But most of it are duplicates (and duplicates of duplicates), bad quality scans and junk (random files uploaded for whatever reason)</p>

<p>Ebook Farm (<a href="https://ebooklogin.com" target="_blank">https://ebooklogin.com</a>) has on other hand 3,200,060 ebooks @ 12.22 TB in its exclusive collection (barely any duplicates, high quality raw files) at 1 cent to 1/15th the amazon cost, with a further 1,357,237 free books on offer taking 13TB in its free collection (fast speeds)</p>
</div>
</div></div><div><div id="siteTable_t1_dahptrk"><div id="thing_t1_dbbbsna"><div><div id="siteTable_t1_dbbbsna"><div id="thing_t1_dbbcina"><div><p><a href="javascript:void(0)" target="_blank">[–]</a><a href="https://www.reddit.com/user/ebookfarm" target="_blank">ebookfarm</a> 2 points <time>1 year ago</time> <a href="javascript:void(0)" target="_blank">(4 children)</a></p><div><div><p>If you import their database into mysql and run this query you will get exact total byte size</p>

<p>SELECT SUM(updated.Filesize) FROM updated</p>

<p>then convert that to TB using "X bytes in TB" search query in google</p>
</div>
</div></div><div><div id="siteTable_t1_dbbcina"><div id="thing_t1_dbbco31"><div><p><a href="javascript:void(0)" target="_blank">[–]</a><a href="https://www.reddit.com/user/eleitl" target="_blank">eleitl</a> 1 point <time>1 year ago</time><time>*</time> <a href="javascript:void(0)" target="_blank">(3 children)</a></p><div><div><p>Thanks. Making the PHP/mysql part of LG work to query it is on my TODO. It is strange that nobody has attempted to map the backend to a key-value store a la S3 instead of serving from the file system.</p>
</div>
</div></div><div><div id="siteTable_t1_dbbco31"><div id="thing_t1_dbbdrmu"><div><p><a href="javascript:void(0)" target="_blank">[–]</a><a href="https://www.reddit.com/user/ebookfarm" target="_blank">ebookfarm</a> 4 points <time>1 year ago</time> <a href="javascript:void(0)" target="_blank">(2 children)</a></p><div><div><p>Be careful! your S3 account is mapped to your name/credit card hence if publishers complain...</p>
</div>
</div></div><div><div id="siteTable_t1_dbbdrmu"><div id="thing_t1_dbberot"><div><p><a href="javascript:void(0)" target="_blank">[–]</a><a href="https://www.reddit.com/user/eleitl" target="_blank">eleitl</a> 3 points <time>1 year ago</time><time>*</time> <a href="javascript:void(0)" target="_blank">(1 child)</a></p><div><div><p>Sure thing. I'm obviously not suicidal. But you can encrypt the blobs and decrypt them on the fly at application layer while serving and S3 is compatible to <a href="https://ceph.com/dev-notes/s3-compatible-object-storage-with-radosgw/" target="_blank">https://ceph.com/dev-notes/s3-compatible-object-storage-with-radosgw/</a></p>

<p>Beats having lots of crappy disks with JBOD or a huge RAID few people can afford. And IOPS are quite nice.</p>

<p>EDIT: Obviously, if commercial cloud this is a hidden service, and you have to hope that the TLAs are not sufficiently interested in you to track it down.</p>
</div>
</div></div></div></div></div></div></div></div></div></div></div></div></div></div></div><div id="thing_t1_dbcjz8y"><div><p><a href="javascript:void(0)" target="_blank">[–]</a><a href="https://www.reddit.com/user/eleitl" target="_blank">eleitl</a> 1 point <time>1 year ago</time> <a href="javascript:void(0)" target="_blank">(0 children)</a></p><div><div><p>Don't see how I can sign up for ebookfarm. This is not an open source effort, right?</p>

<p>Libgen certainly needs some curating. A subset excluding the huge scans and trimming the chaff could bring down the dataset size to a more manageable one.</p>
</div>
</div></div></div></div></div>
<a href="https://dev.mysql.com/doc/refman/5.7/en/load-data.html">https://dev.mysql.com/doc/refman/5.7/en/load-data.html</a><div id="articleHeader"><h1>13.2.6 LOAD DATA INFILE Syntax</h1></div>
<div><pre><code>LOAD DATA [LOW_PRIORITY | CONCURRENT] [LOCAL] INFILE '<em>file_name</em>'
    [REPLACE | IGNORE]
    INTO TABLE <em>tbl_name</em>
    [PARTITION (<em>partition_name</em> [, <em>partition_name</em>] ...)]
    [CHARACTER SET <em>charset_name</em>]
    [{FIELDS | COLUMNS}
        [TERMINATED BY '<em>string</em>']
        [[OPTIONALLY] ENCLOSED BY '<em>char</em>']
        [ESCAPED BY '<em>char</em>']
    ]
    [LINES
        [STARTING BY '<em>string</em>']
        [TERMINATED BY '<em>string</em>']
    ]
    [IGNORE <em>number</em> {LINES | ROWS}]
    [(<em>col_name_or_user_var</em>
        [, <em>col_name_or_user_var</em>] ...)]
    [SET <em>col_name</em>={<em>expr</em> | DEFAULT},
        [, <em>col_name</em>={<em>expr</em> | DEFAULT}] ...]</code></pre></div><p>
      The <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> statement reads rows from a text file into a
      table at a very high speed.
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> is the complement of
      <a href="select-into.html" title="13.2.9.1 SELECT ... INTO Syntax" target="_blank"><code>SELECT ... INTO
      OUTFILE</code></a>. (See <a href="select-into.html" title="13.2.9.1 SELECT ... INTO Syntax" target="_blank">Section 13.2.9.1, “SELECT ... INTO Syntax”</a>.) To write
      data from a table to a file, use
      <a href="select-into.html" title="13.2.9.1 SELECT ... INTO Syntax" target="_blank"><code>SELECT ... INTO
      OUTFILE</code></a>. To read the file back into a table, use
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a>. The syntax of the <code>FIELDS</code> and
      <code>LINES</code> clauses is the same for both statements.
      Both clauses are optional, but <code>FIELDS</code> must
      precede <code>LINES</code> if both are specified.
    </p><p>
      You can also load data files by using the
      <a href="mysqlimport.html" title="4.5.5 mysqlimport — A Data Import Program" target="_blank"><strong>mysqlimport</strong></a> utility; it operates by sending a
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> statement to the server. The
      <a href="mysqlimport.html#option_mysqlimport_local" target="_blank"><code>--local</code></a> option causes
      <a href="mysqlimport.html" title="4.5.5 mysqlimport — A Data Import Program" target="_blank"><strong>mysqlimport</strong></a> to read data files from the client
      host. You can specify the
      <a href="mysqlimport.html#option_mysqlimport_compress" target="_blank"><code>--compress</code></a> option to get
      better performance over slow networks if the client and server
      support the compressed protocol. See
      <a href="mysqlimport.html" title="4.5.5 mysqlimport — A Data Import Program" target="_blank">Section 4.5.5, “<strong>mysqlimport</strong> — A Data Import Program”</a>.
    </p><p>
      For more information about the efficiency of
      <a href="insert.html" title="13.2.5 INSERT Syntax" target="_blank"><code>INSERT</code></a> versus
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> and speeding up
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a>, see <a href="insert-optimization.html" title="8.2.4.1 Optimizing INSERT Statements" target="_blank">Section 8.2.4.1, “Optimizing INSERT Statements”</a>.
    </p><p>
      The file name must be given as a literal string. On Windows,
      specify backslashes in path names as forward slashes or doubled
      backslashes. The
      <a href="server-system-variables.html#sysvar_character_set_filesystem" target="_blank"><code>character_set_filesystem</code></a> system
      variable controls the interpretation of the file name.
    </p><p>
      <code>LOAD DATA</code> supports explicit partition selection
      using the <code>PARTITION</code> option with a list of one
      or more comma-separated names of partitions, subpartitions, or
      both. When this option is used, if any rows from the file cannot
      be inserted into any of the partitions or subpartitions named in
      the list, the statement fails with the error Found a
      row not matching the given partition set. For more
      information and examples, see
      <a href="partitioning-selection.html" title="22.5 Partition Selection" target="_blank">Section 22.5, “Partition Selection”</a>.
    </p><p>
      For partitioned tables using storage engines that employ table
      locks, such as <a href="myisam-storage-engine.html" title="15.2 The MyISAM Storage Engine" target="_blank"><code>MyISAM</code></a>, <code>LOAD
      DATA</code> cannot prune any partition locks. This does not
      apply to tables using storage engines which employ row-level
      locking, such as <a href="innodb-storage-engine.html" title="Chapter 14 The InnoDB Storage Engine" target="_blank"><code>InnoDB</code></a>. For more
      information, see
      <a href="partitioning-limitations-locking.html" title="22.6.4 Partitioning and Locking" target="_blank">Section 22.6.4, “Partitioning and Locking”</a>.
    </p><p>
      The server uses the character set indicated by the
      <a href="server-system-variables.html#sysvar_character_set_database" target="_blank"><code>character_set_database</code></a> system
      variable to interpret the information in the file.
      <a href="set-names.html" title="13.7.4.3 SET NAMES Syntax" target="_blank"><code>SET NAMES</code></a> and the setting of
      <a href="server-system-variables.html#sysvar_character_set_client" target="_blank"><code>character_set_client</code></a> do not
      affect interpretation of input. If the contents of the input file
      use a character set that differs from the default, it is usually
      preferable to specify the character set of the file by using the
      <code>CHARACTER SET</code> clause. A character set of
      <code>binary</code> specifies “no conversion.”
    </p><p>
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> interprets all fields in the file as having the
      same character set, regardless of the data types of the columns
      into which field values are loaded. For proper interpretation of
      file contents, you must ensure that it was written with the
      correct character set. For example, if you write a data file with
      <a href="mysqldump.html" title="4.5.4 mysqldump — A Database Backup Program" target="_blank"><strong>mysqldump -T</strong></a> or by issuing a
      <a href="select-into.html" title="13.2.9.1 SELECT ... INTO Syntax" target="_blank"><code>SELECT ... INTO
      OUTFILE</code></a> statement in <a href="mysql.html" title="4.5.1 mysql — The MySQL Command-Line Tool" target="_blank"><strong>mysql</strong></a>, be sure
      to use a <code>--default-character-set</code> option so that
      output is written in the character set to be used when the file is
      loaded with <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a>.
</p>
<div>


<p>
        It is not possible to load data files that use the
        <code>ucs2</code>, <code>utf16</code>,
        <code>utf16le</code>, or <code>utf32</code>
        character set.
</p>
</div>
<p>
      If you use <code>LOW_PRIORITY</code>, execution of the
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA</code></a> statement is delayed
      until no other clients are reading from the table. This affects
      only storage engines that use only table-level locking (such as
      <code>MyISAM</code>, <code>MEMORY</code>, and
      <code>MERGE</code>).
    </p><p>
      If you specify <code>CONCURRENT</code> with a
      <code>MyISAM</code> table that satisfies the condition for
      concurrent inserts (that is, it contains no free blocks in the
      middle), other threads can retrieve data from the table while
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA</code></a> is executing. This option
      affects the performance of <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD
      DATA</code></a> a bit, even if no other thread is using the table
      at the same time.
    </p><p>
      With row-based replication, <code>CONCURRENT</code> is
      replicated regardless of MySQL version. With statement-based
      replication <code>CONCURRENT</code> is not replicated prior
      to MySQL 5.5.1 (see Bug #34628). For more information, see
      <a href="replication-features-load-data.html" title="16.4.1.18 Replication and LOAD DATA INFILE" target="_blank">Section 16.4.1.18, “Replication and LOAD DATA INFILE”</a>.
    </p><p>
      The <code>LOCAL</code> keyword affects expected location of
      the file and error handling, as described later.
      <code>LOCAL</code> works only if your server and your client
      both have been configured to permit it. For example, if
      <a href="mysqld.html" title="4.3.1 mysqld — The MySQL Server" target="_blank"><strong>mysqld</strong></a> was started with the
      <a href="server-system-variables.html#sysvar_local_infile" target="_blank"><code>local_infile</code></a> system variable
      disabled, <code>LOCAL</code> does not work. See
      <a href="load-data-local.html" title="6.1.6 Security Issues with LOAD DATA LOCAL" target="_blank">Section 6.1.6, “Security Issues with LOAD DATA LOCAL”</a>.
    </p><p>
      The <code>LOCAL</code> keyword affects where the file is
      expected to be found:
</p>
<div>
<ul><li><p>
          If <code>LOCAL</code> is specified, the file is read by
          the client program on the client host and sent to the server.
          The file can be given as a full path name to specify its exact
          location. If given as a relative path name, the name is
          interpreted relative to the directory in which the client
          program was started.
        </p><p>
          When using <code>LOCAL</code> with
          <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA</code></a>, a copy of the file
          is created in the server's temporary directory. This is
          <em>not</em> the directory determined by the value
          of <a href="server-system-variables.html#sysvar_tmpdir" target="_blank"><code>tmpdir</code></a> or
          <a href="replication-options-slave.html#sysvar_slave_load_tmpdir" target="_blank"><code>slave_load_tmpdir</code></a>, but rather
          the operating system's temporary directory, and is not
          configurable in the MySQL Server. (Typically the system
          temporary directory is <code>/tmp</code> on Linux
          systems and <code>C:\WINDOWS\TEMP</code> on Windows.)
          Lack of sufficient space for the copy in this directory can
          cause the <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
          LOCAL</code></a> statement to fail.
        </p></li><li><p>
          If <code>LOCAL</code> is not specified, the file must be
          located on the server host and is read directly by the server.
          The server uses the following rules to locate the file:
</p>
<div>
<ul><li><p>
              If the file name is an absolute path name, the server uses
              it as given.
            </p></li><li><p>
              If the file name is a relative path name with one or more
              leading components, the server searches for the file
              relative to the server's data directory.
            </p></li><li><p>
              If a file name with no leading components is given, the
              server looks for the file in the database directory of the
              default database.
</p></li></ul>
</div>
</li></ul>

<p>
      In the non-<code>LOCAL</code> case, these rules mean that a
      file named as <code>./myfile.txt</code> is read from the
      server's data directory, whereas the file named as
      <code>myfile.txt</code> is read from the database
      directory of the default database. For example, if
      <code>db1</code> is the default database, the following
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA</code></a> statement reads the file
      <code>data.txt</code> from the database directory for
      <code>db1</code>, even though the statement explicitly loads
      the file into a table in the <code>db2</code> database:
    </p><div><pre><code>LOAD DATA INFILE 'data.txt' INTO TABLE db2.my_table;</code></pre></div><p>
      Non-<code>LOCAL</code> load operations read text files
      located on the server. For security reasons, such operations
      require that you have the <a href="privileges-provided.html#priv_file" target="_blank"><code>FILE</code></a>
      privilege. See <a href="privileges-provided.html" title="6.2.1 Privileges Provided by MySQL" target="_blank">Section 6.2.1, “Privileges Provided by MySQL”</a>. Also,
      non-<code>LOCAL</code> load operations are subject to the
      <a href="server-system-variables.html#sysvar_secure_file_priv" target="_blank"><code>secure_file_priv</code></a> system variable
      setting. If the variable value is a nonempty directory name, the
      file to be loaded must be located in that directory. If the
      variable value is empty (which is insecure), the file need only be
      readable by the server.
    </p><p>
      Using <code>LOCAL</code> is a bit slower than letting the
      server access the files directly, because the contents of the file
      must be sent over the connection by the client to the server. On
      the other hand, you do not need the
      <a href="privileges-provided.html#priv_file" target="_blank"><code>FILE</code></a> privilege to load local files.
    </p><p>
      <code>LOCAL</code> also affects error handling:
</p>
<div>
<ul><li><p>
          With <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
          INFILE</code></a>, data-interpretation and duplicate-key errors
          terminate the operation.
        </p></li><li><p>
          With <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
          LOCAL INFILE</code></a>, data-interpretation and duplicate-key
          errors become warnings and the operation continues because the
          server has no way to stop transmission of the file in the
          middle of the operation. For duplicate-key errors, this is the
          same as if <code>IGNORE</code> is specified.
          <code>IGNORE</code> is explained further later in this
          section.
</p></li></ul>
</div>
<p>
      The <code>REPLACE</code> and <code>IGNORE</code>
      keywords control handling of input rows that duplicate existing
      rows on unique key values:
</p>
<div>
<ul><li><p>
          If you specify <code>REPLACE</code>, input rows replace
          existing rows. In other words, rows that have the same value
          for a primary key or unique index as an existing row. See
          <a href="replace.html" title="13.2.8 REPLACE Syntax" target="_blank">Section 13.2.8, “REPLACE Syntax”</a>.
        </p></li><li><p>
          If you specify <code>IGNORE</code>, rows that duplicate
          an existing row on a unique key value are discarded. For more
          information, see <a href="sql-mode.html#ignore-strict-comparison" title="Comparison of the IGNORE Keyword and Strict SQL Mode" target="_blank">Comparison of the IGNORE Keyword and Strict SQL Mode</a>.
        </p></li><li><p>
          If you do not specify either option, the behavior depends on
          whether the <code>LOCAL</code> keyword is specified.
          Without <code>LOCAL</code>, an error occurs when a
          duplicate key value is found, and the rest of the text file is
          ignored. With <code>LOCAL</code>, the default behavior
          is the same as if <code>IGNORE</code> is specified; this
          is because the server has no way to stop transmission of the
          file in the middle of the operation.
</p></li></ul>
</div>
<p>
      To ignore foreign key constraints during the load operation, issue
      a <code>SET foreign_key_checks = 0</code> statement before
      executing <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA</code></a>.
    </p><p>
      If you use <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> on an empty <code>MyISAM</code> table, all
      nonunique indexes are created in a separate batch (as for
      <a href="repair-table.html" title="13.7.2.5 REPAIR TABLE Syntax" target="_blank"><code>REPAIR TABLE</code></a>). Normally, this makes
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> much faster when you have many indexes. In some
      extreme cases, you can create the indexes even faster by turning
      them off with <code>ALTER TABLE ... DISABLE KEYS</code>
      before loading the file into the table and using <code>ALTER
      TABLE ... ENABLE KEYS</code> to re-create the indexes after
      loading the file. See <a href="insert-optimization.html" title="8.2.4.1 Optimizing INSERT Statements" target="_blank">Section 8.2.4.1, “Optimizing INSERT Statements”</a>.
    </p><p>
      For both the <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> and
      <a href="select-into.html" title="13.2.9.1 SELECT ... INTO Syntax" target="_blank"><code>SELECT ... INTO
      OUTFILE</code></a> statements, the syntax of the
      <code>FIELDS</code> and <code>LINES</code> clauses is
      the same. Both clauses are optional, but <code>FIELDS</code>
      must precede <code>LINES</code> if both are specified.
    </p><p>
      If you specify a <code>FIELDS</code> clause, each of its
      subclauses (<code>TERMINATED BY</code>,
      <code>[OPTIONALLY] ENCLOSED BY</code>, and <code>ESCAPED
      BY</code>) is also optional, except that you must specify at
      least one of them.
    </p><p>
      If you specify no <code>FIELDS</code> or
      <code>LINES</code> clause, the defaults are the same as if
      you had written this:
    </p><div><pre><code>FIELDS TERMINATED BY '\t' ENCLOSED BY '' ESCAPED BY '\\'
LINES TERMINATED BY '\n' STARTING BY ''</code></pre></div><p>
      (Backslash is the MySQL escape character within strings in SQL
      statements, so to specify a literal backslash, you must specify
      two backslashes for the value to be interpreted as a single
      backslash. The escape sequences <code>'\t'</code> and
      <code>'\n'</code> specify tab and newline characters,
      respectively.)
    </p><p>
      In other words, the defaults cause
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> to act as follows when reading input:
</p>
<div>
<ul><li><p>
          Look for line boundaries at newlines.
        </p></li><li><p>
          Do not skip over any line prefix.
        </p></li><li><p>
          Break lines into fields at tabs.
        </p></li><li><p>
          Do not expect fields to be enclosed within any quoting
          characters.
        </p></li><li><p>
          Interpret characters preceded by the escape character
          <code>\</code> as escape sequences. For example,
          <code>\t</code>, <code>\n</code>, and
          <code>\\</code> signify tab, newline, and backslash,
          respectively. See the discussion of <code>FIELDS ESCAPED
          BY</code> later for the full list of escape sequences.
</p></li></ul>
</div>
<p>
      Conversely, the defaults cause
      <a href="select-into.html" title="13.2.9.1 SELECT ... INTO Syntax" target="_blank"><code>SELECT ... INTO
      OUTFILE</code></a> to act as follows when writing output:
</p>
<div>
<ul><li><p>
          Write tabs between fields.
        </p></li><li><p>
          Do not enclose fields within any quoting characters.
        </p></li><li><p>
          Use <code>\</code> to escape instances of tab, newline,
          or <code>\</code> that occur within field values.
        </p></li><li><p>
          Write newlines at the ends of lines.
</p></li></ul>
</div>
<div>

<p>
        If you have generated the text file on a Windows system, you
        might have to use <code>LINES TERMINATED BY '\r\n'</code>
        to read the file properly, because Windows programs typically
        use two characters as a line terminator. Some programs, such as
        <strong>WordPad</strong>, might use <code>\r</code> as a
        line terminator when writing files. To read such files, use
        <code>LINES TERMINATED BY '\r'</code>.
</p>
</div>
<p>
      If all the lines you want to read in have a common prefix that you
      want to ignore, you can use <code>LINES STARTING BY
      '<em><code>prefix_string</code></em>'</code> to skip over
      the prefix, <em>and anything before it</em>. If a line
      does not include the prefix, the entire line is skipped. Suppose
      that you issue the following statement:
    </p><div><pre><code>LOAD DATA INFILE '/tmp/test.txt' INTO TABLE test
  FIELDS TERMINATED BY ','  LINES STARTING BY 'xxx';</code></pre></div><p>
      If the data file looks like this:
    </p><div><pre><code>xxx"abc",1
something xxx"def",2
"ghi",3</code></pre></div><p>
      The resulting rows will be <code>("abc",1)</code> and
      <code>("def",2)</code>. The third row in the file is skipped
      because it does not contain the prefix.
    </p><p>
      The <code>IGNORE <em><code>number</code></em>
      LINES</code> option can be used to ignore lines at the start of
      the file. For example, you can use <code>IGNORE 1
      LINES</code> to skip over an initial header line containing
      column names:
    </p><div><pre><code>LOAD DATA INFILE '/tmp/test.txt' INTO TABLE test IGNORE 1 LINES;</code></pre></div><p>
      When you use <a href="select-into.html" title="13.2.9.1 SELECT ... INTO Syntax" target="_blank"><code>SELECT
      ... INTO OUTFILE</code></a> in tandem with
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> to write data from a database into a file and
      then read the file back into the database later, the field- and
      line-handling options for both statements must match. Otherwise,
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> will not interpret the contents of the file
      properly. Suppose that you use
      <a href="select-into.html" title="13.2.9.1 SELECT ... INTO Syntax" target="_blank"><code>SELECT ... INTO
      OUTFILE</code></a> to write a file with fields delimited by commas:
    </p><div><pre><code>SELECT * INTO OUTFILE 'data.txt'
  FIELDS TERMINATED BY ','
  FROM table2;</code></pre></div><p>
      To read the comma-delimited file back in, the correct statement
      would be:
    </p><div><pre><code>LOAD DATA INFILE 'data.txt' INTO TABLE table2
  FIELDS TERMINATED BY ',';</code></pre></div><p>
      If instead you tried to read in the file with the statement shown
      following, it wouldn't work because it instructs
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> to look for tabs between fields:
    </p><div><pre><code>LOAD DATA INFILE 'data.txt' INTO TABLE table2
  FIELDS TERMINATED BY '\t';</code></pre></div><p>
      The likely result is that each input line would be interpreted as
      a single field.
    </p><p>
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> can be used to read files obtained from external
      sources. For example, many programs can export data in
      comma-separated values (CSV) format, such that lines have fields
      separated by commas and enclosed within double quotation marks,
      with an initial line of column names. If the lines in such a file
      are terminated by carriage return/newline pairs, the statement
      shown here illustrates the field- and line-handling options you
      would use to load the file:
    </p><div><pre><code>LOAD DATA INFILE 'data.txt' INTO TABLE <em>tbl_name</em>
  FIELDS TERMINATED BY ',' ENCLOSED BY '"'
  LINES TERMINATED BY '\r\n'
  IGNORE 1 LINES;</code></pre></div><p>
      If the input values are not necessarily enclosed within quotation
      marks, use <code>OPTIONALLY</code> before the
      <code>ENCLOSED BY</code> keywords.
    </p><p>
      Any of the field- or line-handling options can specify an empty
      string (<code>''</code>). If not empty, the <code>FIELDS
      [OPTIONALLY] ENCLOSED BY</code> and <code>FIELDS ESCAPED
      BY</code> values must be a single character. The
      <code>FIELDS TERMINATED BY</code>, <code>LINES STARTING
      BY</code>, and <code>LINES TERMINATED BY</code> values
      can be more than one character. For example, to write lines that
      are terminated by carriage return/linefeed pairs, or to read a
      file containing such lines, specify a <code>LINES TERMINATED BY
      '\r\n'</code> clause.
    </p><p>
      To read a file containing jokes that are separated by lines
      consisting of <code>%%</code>, you can do this
    </p><div><pre><code>CREATE TABLE jokes
  (a INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  joke TEXT NOT NULL);
LOAD DATA INFILE '/tmp/jokes.txt' INTO TABLE jokes
  FIELDS TERMINATED BY ''
  LINES TERMINATED BY '\n%%\n' (joke);</code></pre></div><p>
      <code>FIELDS [OPTIONALLY] ENCLOSED BY</code> controls
      quoting of fields. For output
      (<a href="select-into.html" title="13.2.9.1 SELECT ... INTO Syntax" target="_blank"><code>SELECT ... INTO
      OUTFILE</code></a>), if you omit the word
      <code>OPTIONALLY</code>, all fields are enclosed by the
      <code>ENCLOSED BY</code> character. An example of such
      output (using a comma as the field delimiter) is shown here:
    </p><div><pre><code>"1","a string","100.20"
"2","a string containing a , comma","102.20"
"3","a string containing a \" quote","102.20"
"4","a string containing a \", quote and comma","102.20"</code></pre></div><p>
      If you specify <code>OPTIONALLY</code>, the
      <code>ENCLOSED BY</code> character is used only to enclose
      values from columns that have a string data type (such as
      <a href="char.html" title="11.4.1 The CHAR and VARCHAR Types" target="_blank"><code>CHAR</code></a>,
      <a href="binary-varbinary.html" title="11.4.2 The BINARY and VARBINARY Types" target="_blank"><code>BINARY</code></a>,
      <a href="blob.html" title="11.4.3 The BLOB and TEXT Types" target="_blank"><code>TEXT</code></a>, or
      <a href="enum.html" title="11.4.4 The ENUM Type" target="_blank"><code>ENUM</code></a>):
    </p><div><pre><code>1,"a string",100.20
2,"a string containing a , comma",102.20
3,"a string containing a \" quote",102.20
4,"a string containing a \", quote and comma",102.20</code></pre></div><p>
      Occurrences of the <code>ENCLOSED BY</code> character within
      a field value are escaped by prefixing them with the
      <code>ESCAPED BY</code> character. Also, if you specify an
      empty <code>ESCAPED BY</code> value, it is possible to
      inadvertently generate output that cannot be read properly by
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a>. For example, the preceding output just shown
      would appear as follows if the escape character is empty. Observe
      that the second field in the fourth line contains a comma
      following the quote, which (erroneously) appears to terminate the
      field:
    </p><div><pre><code>1,"a string",100.20
2,"a string containing a , comma",102.20
3,"a string containing a " quote",102.20
4,"a string containing a ", quote and comma",102.20</code></pre></div><p>
      For input, the <code>ENCLOSED BY</code> character, if
      present, is stripped from the ends of field values. (This is true
      regardless of whether <code>OPTIONALLY</code> is specified;
      <code>OPTIONALLY</code> has no effect on input
      interpretation.) Occurrences of the <code>ENCLOSED BY</code>
      character preceded by the <code>ESCAPED BY</code> character
      are interpreted as part of the current field value.
    </p><p>
      If the field begins with the <code>ENCLOSED BY</code>
      character, instances of that character are recognized as
      terminating a field value only if followed by the field or line
      <code>TERMINATED BY</code> sequence. To avoid ambiguity,
      occurrences of the <code>ENCLOSED BY</code> character within
      a field value can be doubled and are interpreted as a single
      instance of the character. For example, if <code>ENCLOSED BY
      '"'</code> is specified, quotation marks are handled as shown
      here:
    </p><div><pre><code>"The ""BIG"" boss"  -&gt; The "BIG" boss
The "BIG" boss      -&gt; The "BIG" boss
The ""BIG"" boss    -&gt; The ""BIG"" boss</code></pre></div><p>
      <code>FIELDS ESCAPED BY</code> controls how to read or write
      special characters:
</p>
<div>
<ul><li><p>
          For input, if the <code>FIELDS ESCAPED BY</code>
          character is not empty, occurrences of that character are
          stripped and the following character is taken literally as
          part of a field value. Some two-character sequences that are
          exceptions, where the first character is the escape character.
          These sequences are shown in the following table (using
          <code>\</code> for the escape character). The rules for
          <code>NULL</code> handling are described later in this
          section.
</p>
<div>
<table><colgroup><col /><col /></colgroup><thead><tr><th>Character</th><th>Escape Sequence</th></tr></thead><tbody><tr><td><code>\0</code>

                  

                  </td><td>An ASCII NUL (<code>X'00'</code>) character</td></tr><tr><td><code>\b</code>

                  

                  </td><td>A backspace character</td></tr><tr><td><code>\n</code>

                  

                  

                  

                  </td><td>A newline (linefeed) character</td></tr><tr><td><code>\r</code>

                  

                  

                  </td><td>A carriage return character</td></tr><tr><td><code>\t</code>

                  

                  </td><td>A tab character.</td></tr><tr><td><code>\Z</code>

                  

                  </td><td>ASCII 26 (Control+Z)</td></tr><tr><td><code>\N</code>

</td><td>NULL</td></tr></tbody></table>
</div>
<p>
          For more information about <code>\</code>-escape syntax,
          see <a href="string-literals.html" title="9.1.1 String Literals" target="_blank">Section 9.1.1, “String Literals”</a>.
        </p><p>
          If the <code>FIELDS ESCAPED BY</code> character is
          empty, escape-sequence interpretation does not occur.
        </p></li><li><p>
          For output, if the <code>FIELDS ESCAPED BY</code>
          character is not empty, it is used to prefix the following
          characters on output:
</p>
<div>
<ul><li><p>
              The <code>FIELDS ESCAPED BY</code> character
            </p></li><li><p>
              The <code>FIELDS [OPTIONALLY] ENCLOSED BY</code>
              character
            </p></li><li><p>
              The first character of the <code>FIELDS TERMINATED
              BY</code> and <code>LINES TERMINATED BY</code>
              values
            </p></li><li><p>
              ASCII <code>0</code> (what is actually written
              following the escape character is ASCII
              <code>0</code>, not a zero-valued byte)
</p></li></ul>
</div>
<p>
          If the <code>FIELDS ESCAPED BY</code> character is
          empty, no characters are escaped and <code>NULL</code>
          is output as <code>NULL</code>, not
          <code>\N</code>. It is probably not a good idea to
          specify an empty escape character, particularly if field
          values in your data contain any of the characters in the list
          just given.
</p></li></ul>

<p>
      In certain cases, field- and line-handling options interact:
</p>
<div>
<ul><li><p>
          If <code>LINES TERMINATED BY</code> is an empty string
          and <code>FIELDS TERMINATED BY</code> is nonempty, lines
          are also terminated with <code>FIELDS TERMINATED
          BY</code>.
        </p></li><li><p>
          If the <code>FIELDS TERMINATED BY</code> and
          <code>FIELDS ENCLOSED BY</code> values are both empty
          (<code>''</code>), a fixed-row (nondelimited) format is
          used. With fixed-row format, no delimiters are used between
          fields (but you can still have a line terminator). Instead,
          column values are read and written using a field width wide
          enough to hold all values in the field. For
          <a href="integer-types.html" title="11.2.1 Integer Types (Exact Value) - INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT" target="_blank"><code>TINYINT</code></a>,
          <a href="integer-types.html" title="11.2.1 Integer Types (Exact Value) - INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT" target="_blank"><code>SMALLINT</code></a>,
          <a href="integer-types.html" title="11.2.1 Integer Types (Exact Value) - INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT" target="_blank"><code>MEDIUMINT</code></a>,
          <a href="integer-types.html" title="11.2.1 Integer Types (Exact Value) - INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT" target="_blank"><code>INT</code></a>, and
          <a href="integer-types.html" title="11.2.1 Integer Types (Exact Value) - INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT" target="_blank"><code>BIGINT</code></a>, the field widths are 4,
          6, 8, 11, and 20, respectively, no matter what the declared
          display width is.
        </p><p>
          <code>LINES TERMINATED BY</code> is still used to
          separate lines. If a line does not contain all fields, the
          rest of the columns are set to their default values. If you do
          not have a line terminator, you should set this to
          <code>''</code>. In this case, the text file must
          contain all fields for each row.
        </p><p>
          Fixed-row format also affects handling of
          <code>NULL</code> values, as described later.
</p>
<div>


<p>
            Fixed-size format does not work if you are using a multibyte
            character set.
</p>
</div>
</li></ul>

<p>
      Handling of <code>NULL</code> values varies according to the
      <code>FIELDS</code> and <code>LINES</code> options in
      use:
</p>
<div>
<ul><li><p>
          For the default <code>FIELDS</code> and
          <code>LINES</code> values, <code>NULL</code> is
          written as a field value of <code>\N</code> for output,
          and a field value of <code>\N</code> is read as
          <code>NULL</code> for input (assuming that the
          <code>ESCAPED BY</code> character is
          <code>\</code>).
        </p></li><li><p>
          If <code>FIELDS ENCLOSED BY</code> is not empty, a field
          containing the literal word <code>NULL</code> as its
          value is read as a <code>NULL</code> value. This differs
          from the word <code>NULL</code> enclosed within
          <code>FIELDS ENCLOSED BY</code> characters, which is
          read as the string <code>'NULL'</code>.
        </p></li><li><p>
          If <code>FIELDS ESCAPED BY</code> is empty,
          <code>NULL</code> is written as the word
          <code>NULL</code>.
        </p></li><li><p>
          With fixed-row format (which is used when <code>FIELDS
          TERMINATED BY</code> and <code>FIELDS ENCLOSED
          BY</code> are both empty), <code>NULL</code> is
          written as an empty string. This causes both
          <code>NULL</code> values and empty strings in the table
          to be indistinguishable when written to the file because both
          are written as empty strings. If you need to be able to tell
          the two apart when reading the file back in, you should not
          use fixed-row format.
</p></li></ul>
</div>
<p>
      An attempt to load <code>NULL</code> into a <code>NOT
      NULL</code> column causes assignment of the implicit default
      value for the column's data type and a warning, or an error in
      strict SQL mode. Implicit default values are discussed in
      <a href="data-type-defaults.html" title="11.7 Data Type Default Values" target="_blank">Section 11.7, “Data Type Default Values”</a>.
    </p><p>
      Some cases are not supported by
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a>:
</p>
<div>
<ul><li><p>
          Fixed-size rows (<code>FIELDS TERMINATED BY</code> and
          <code>FIELDS ENCLOSED BY</code> both empty) and
          <a href="blob.html" title="11.4.3 The BLOB and TEXT Types" target="_blank"><code>BLOB</code></a> or
          <a href="blob.html" title="11.4.3 The BLOB and TEXT Types" target="_blank"><code>TEXT</code></a> columns.
        </p></li><li><p>
          If you specify one separator that is the same as or a prefix
          of another, <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD
          DATA INFILE</code></a> cannot interpret the input properly. For
          example, the following <code>FIELDS</code> clause would
          cause problems:
        </p><div><pre><code>FIELDS TERMINATED BY '"' ENCLOSED BY '"'</code></pre></div></li><li><p>
          If <code>FIELDS ESCAPED BY</code> is empty, a field
          value that contains an occurrence of <code>FIELDS ENCLOSED
          BY</code> or <code>LINES TERMINATED BY</code>
          followed by the <code>FIELDS TERMINATED BY</code> value
          causes <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
          INFILE</code></a> to stop reading a field or line too early.
          This happens because
          <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
          INFILE</code></a> cannot properly determine where the field or
          line value ends.
</p></li></ul>

<p>
      The following example loads all columns of the
      <code>persondata</code> table:
    </p><div><pre><code>LOAD DATA INFILE 'persondata.txt' INTO TABLE persondata;</code></pre></div><p>
      By default, when no column list is provided at the end of the
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> statement, input lines are expected to contain a
      field for each table column. If you want to load only some of a
      table's columns, specify a column list:
    </p><div><pre><code>LOAD DATA INFILE 'persondata.txt' INTO TABLE persondata (col1,col2,...);</code></pre></div><p>
      You must also specify a column list if the order of the fields in
      the input file differs from the order of the columns in the table.
      Otherwise, MySQL cannot tell how to match input fields with table
      columns.
    </p><p>
      The column list can contain either column names or user variables.
      With user variables, the <code>SET</code> clause enables you
      to perform transformations on their values before assigning the
      result to columns.
    </p><p>
      User variables in the <code>SET</code> clause can be used in
      several ways. The following example uses the first input column
      directly for the value of <code>t1.column1</code>, and
      assigns the second input column to a user variable that is
      subjected to a division operation before being used for the value
      of <code>t1.column2</code>:
    </p><div><pre><code>LOAD DATA INFILE 'file.txt'
  INTO TABLE t1
  (column1, @var1)
  SET column2 = @var1/100;</code></pre></div><p>
      The <code>SET</code> clause can be used to supply values not
      derived from the input file. The following statement sets
      <code>column3</code> to the current date and time:
    </p><div><pre><code>LOAD DATA INFILE 'file.txt'
  INTO TABLE t1
  (column1, column2)
  SET column3 = CURRENT_TIMESTAMP;</code></pre></div><p>
      You can also discard an input value by assigning it to a user
      variable and not assigning the variable to a table column:
    </p><div><pre><code>LOAD DATA INFILE 'file.txt'
  INTO TABLE t1
  (column1, @dummy, column2, @dummy, column3);</code></pre></div><p>
      Use of the column/variable list and <code>SET</code> clause
      is subject to the following restrictions:
</p>
<div>
<ul><li><p>
          Assignments in the <code>SET</code> clause should have
          only column names on the left hand side of assignment
          operators.
        </p></li><li><p>
          You can use subqueries in the right hand side of
          <code>SET</code> assignments. A subquery that returns a
          value to be assigned to a column may be a scalar subquery
          only. Also, you cannot use a subquery to select from the table
          that is being loaded.
        </p></li><li><p>
          Lines ignored by an <code>IGNORE</code> clause are not
          processed for the column/variable list or
          <code>SET</code> clause.
        </p></li><li><p>
          User variables cannot be used when loading data with fixed-row
          format because user variables do not have a display width.
</p></li></ul>
</div>
<p>
      When processing an input line, <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD
      DATA</code></a> splits it into fields and uses the values according
      to the column/variable list and the <code>SET</code> clause,
      if they are present. Then the resulting row is inserted into the
      table. If there are <code>BEFORE INSERT</code> or
      <code>AFTER INSERT</code> triggers for the table, they are
      activated before or after inserting the row, respectively.
    </p><p>
      If an input line has too many fields, the extra fields are ignored
      and the number of warnings is incremented.
    </p><p>
      If an input line has too few fields, the table columns for which
      input fields are missing are set to their default values. Default
      value assignment is described in
      <a href="data-type-defaults.html" title="11.7 Data Type Default Values" target="_blank">Section 11.7, “Data Type Default Values”</a>.
    </p><p>
      An empty field value is interpreted different from a missing
      field:
</p>
<div>
<ul><li><p>
          For string types, the column is set to the empty string.
        </p></li><li><p>
          For numeric types, the column is set to <code>0</code>.
        </p></li><li><p>
          For date and time types, the column is set to the appropriate
          “zero” value for the type. See
          <a href="date-and-time-types.html" title="11.3 Date and Time Types" target="_blank">Section 11.3, “Date and Time Types”</a>.
</p></li></ul>
</div>
<p>
      These are the same values that result if you assign an empty
      string explicitly to a string, numeric, or date or time type
      explicitly in an <a href="insert.html" title="13.2.5 INSERT Syntax" target="_blank"><code>INSERT</code></a> or
      <a href="update.html" title="13.2.11 UPDATE Syntax" target="_blank"><code>UPDATE</code></a> statement.
    </p><p>
      Treatment of empty or incorrect field values differs from that
      just described if the SQL mode is set to a restrictive value. For
      example, if <a href="server-system-variables.html#sysvar_sql_mode" target="_blank"><code>sql_mode</code></a> is set to
      <a href="sql-mode.html#sqlmode_traditional" target="_blank"><code>TRADITIONAL</code></a>, conversion of an
      empty value or a value such as <code>'x'</code> for a
      numeric column results in an error, not conversion to 0. (With
      <code>LOCAL</code> or <code>IGNORE</code>, warnings
      occur rather than errors, even with a restrictive
      <a href="server-system-variables.html#sysvar_sql_mode" target="_blank"><code>sql_mode</code></a> value, and the row is
      inserted using the same closest-value behavior used for
      nonrestrictive SQL modes. This occurs because the server has no
      way to stop transmission of the file in the middle of the
      operation.)
    </p><p>
      <a href="datetime.html" title="11.3.1 The DATE, DATETIME, and TIMESTAMP Types" target="_blank"><code>TIMESTAMP</code></a> columns are set to the
      current date and time only if there is a <code>NULL</code>
      value for the column (that is, <code>\N</code>) and the
      column is not declared to permit <code>NULL</code> values,
      or if the <a href="datetime.html" title="11.3.1 The DATE, DATETIME, and TIMESTAMP Types" target="_blank"><code>TIMESTAMP</code></a> column's
      default value is the current timestamp and it is omitted from the
      field list when a field list is specified.
    </p><p>
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> regards all input as strings, so you cannot use
      numeric values for <a href="enum.html" title="11.4.4 The ENUM Type" target="_blank"><code>ENUM</code></a> or
      <a href="set.html" title="11.4.5 The SET Type" target="_blank"><code>SET</code></a> columns the way you can with
      <a href="insert.html" title="13.2.5 INSERT Syntax" target="_blank"><code>INSERT</code></a> statements. All
      <a href="enum.html" title="11.4.4 The ENUM Type" target="_blank"><code>ENUM</code></a> and
      <a href="set.html" title="11.4.5 The SET Type" target="_blank"><code>SET</code></a> values must be specified as
      strings.
    </p><p>
      <a href="bit-type.html" title="11.2.4 Bit-Value Type - BIT" target="_blank"><code>BIT</code></a> values cannot be loaded
      directly using binary notation (for example,
      <code>b'011010'</code>). To work around this, use the
      <code>SET</code> clause to strip off the leading
      <code>b'</code> and trailing <code>'</code> and
      perform a base-2 to base-10 conversion so that MySQL loads the
      values into the <a href="bit-type.html" title="11.2.4 Bit-Value Type - BIT" target="_blank"><code>BIT</code></a> column
      properly:
    </p><div><pre><code>shell&gt; cat /tmp/bit_test.txt
b'10'
b'1111111'
shell&gt; mysql test
mysql&gt; LOAD DATA INFILE '/tmp/bit_test.txt'
       INTO TABLE bit_test (@var1)
       SET b = CAST(CONV(MID(@var1, 3, LENGTH(@var1)-3), 2, 10) AS UNSIGNED);
Query OK, 2 rows affected (0.00 sec)
Records: 2  Deleted: 0  Skipped: 0  Warnings: 0

mysql&gt; SELECT BIN(b+0) FROM bit_test;
+----------+
| BIN(b+0) |
+----------+
| 10       |
| 1111111  |
+----------+
2 rows in set (0.00 sec)</code></pre></div><p>
      For <a href="bit-type.html" title="11.2.4 Bit-Value Type - BIT" target="_blank"><code>BIT</code></a> values in
      <code>0b</code> binary notation (for example,
      <code>0b011010</code>), use this <code>SET</code>
      clause instead to strip off the leading <code>0b</code>:
    </p><div><pre><code>SET b = CAST(CONV(MID(@var1, 3, LENGTH(@var1)-2), 2, 10) AS UNSIGNED)</code></pre></div><p>
      On Unix, if you need <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA</code></a> to
      read from a pipe, you can use the following technique (the example
      loads a listing of the <code>/</code> directory into the
      table <code>db1.t1</code>):
    </p><div><pre><code>mkfifo /mysql/data/db1/ls.dat
chmod 666 /mysql/data/db1/ls.dat
find / -ls &gt; /mysql/data/db1/ls.dat &
mysql -e "LOAD DATA INFILE 'ls.dat' INTO TABLE t1" db1</code></pre></div><p>
      Here you must run the command that generates the data to be loaded
      and the <a href="mysql.html" title="4.5.1 mysql — The MySQL Command-Line Tool" target="_blank"><strong>mysql</strong></a> commands either on separate
      terminals, or run the data generation process in the background
      (as shown in the preceding example). If you do not do this, the
      pipe will block until data is read by the <a href="mysql.html" title="4.5.1 mysql — The MySQL Command-Line Tool" target="_blank"><strong>mysql</strong></a>
      process.
    </p><p>
      When the <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> statement finishes, it returns an information
      string in the following format:
    </p><div><pre><code>Records: 1  Deleted: 0  Skipped: 0  Warnings: 0</code></pre></div><p>
      Warnings occur under the same circumstances as when values are
      inserted using the <a href="insert.html" title="13.2.5 INSERT Syntax" target="_blank"><code>INSERT</code></a> statement
      (see <a href="insert.html" title="13.2.5 INSERT Syntax" target="_blank">Section 13.2.5, “INSERT Syntax”</a>), except that
      <a href="load-data.html" title="13.2.6 LOAD DATA INFILE Syntax" target="_blank"><code>LOAD DATA
      INFILE</code></a> also generates warnings when there are too few or
      too many fields in the input row.
    </p><p>
      You can use <a href="show-warnings.html" title="13.7.5.40 SHOW WARNINGS Syntax" target="_blank"><code>SHOW WARNINGS</code></a> to get a
      list of the first <a href="server-system-variables.html#sysvar_max_error_count" target="_blank"><code>max_error_count</code></a>
      warnings as information about what went wrong. See
      <a href="show-warnings.html" title="13.7.5.40 SHOW WARNINGS Syntax" target="_blank">Section 13.7.5.40, “SHOW WARNINGS Syntax”</a>.
    </p><p>
      If you are using the C API, you can get information about the
      statement by calling the
      <a href="mysql-info.html" title="27.8.7.36 mysql_info()" target="_blank"><code>mysql_info()</code></a> function. See
      <a href="mysql-info.html" title="27.8.7.36 mysql_info()" target="_blank">Section 27.8.7.36, “mysql_info()”</a>.
</p>

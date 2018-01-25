<a href="https://www.elastic.co/guide/en/elasticsearch/reference/2.3/setup-configuration.html#settings">https://www.elastic.co/guide/en/elasticsearch/reference/2.3/setup-configuration.html#settings</a><div id="articleHeader"><h1>Elasticsearch Reference [2.3]</h1></div><div><div><div><h2>Configuration<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h2></div></div></div><h3>Environment Variables<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h3><p>Within the scripts, Elasticsearch comes with built in <code>JAVA_OPTS</code> passed
to the JVM started. The most important setting for that is the <code>-Xmx</code> to
control the maximum allowed memory for the process, and <code>-Xms</code> to
control the minimum allocated memory for the process (<em>in general, the
more memory allocated to the process, the better</em>).</p><p>Most times it is better to leave the default <code>JAVA_OPTS</code> as they are,
and use the <code>ES_JAVA_OPTS</code> environment variable in order to set / change
JVM settings or arguments.</p><p>The <code>ES_HEAP_SIZE</code> environment variable allows to set the heap memory
that will be allocated to elasticsearch java process. It will allocate
the same value to both min and max values, though those can be set
explicitly (not recommended) by setting <code>ES_MIN_MEM</code> (defaults to
<code>256m</code>), and <code>ES_MAX_MEM</code> (defaults to <code>1g</code>).</p><p>It is recommended to set the min and max memory to the same value, and
enable <a href="setup-configuration.html#setup-configuration-memory" title="Memory Settingsedit" target="_blank"><code>mlockall</code></a>.</p><h3>System Configuration<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h3><h4>File Descriptors<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>Make sure to increase the number of open files descriptors on the
machine (or for the user running elasticsearch). Setting it to 32k or
even 64k is recommended.</p><p>In order to test how many open files the process can open, start it with
<code>-Des.max-open-files</code> set to <code>true</code>. This will print the number of open
files the process can open on startup.</p><p>Alternatively, you can retrieve the <code>max_file_descriptors</code> for each node
using the <a href="cluster-nodes-info.html" title="Nodes Info" target="_blank"><em>Nodes Info</em></a> API, with:</p><div><pre>curl localhost:9200/_nodes/stats/process?pretty</pre></div><h4>Virtual memory<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>Elasticsearch uses a <a href="index-modules-store.html#default_fs" target="_blank"><code>hybrid mmapfs / niofs</code></a> directory by default to store its indices.  The default
operating system limits on mmap counts is likely to be too low, which may
result in out of memory exceptions.  On Linux, you can increase the limits by
running the following command as <code>root</code>:</p><div><pre>sysctl -w vm.max_map_count=262144</pre></div><p>To set this value permanently, update the <code>vm.max_map_count</code> setting in
<code>/etc/sysctl.conf</code>.</p><div><div><img src="images/icons/note.png" alt="Note" /></div><div><p>If you installed Elasticsearch using a package (.deb, .rpm) this setting will be changed automatically.  To verify, run <code>sysctl vm.max_map_count</code>.</p></div></div><h4>Memory Settings<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>Most operating systems try to use as much memory as possible for file system
caches and eagerly swap out unused application memory, possibly resulting
in the elasticsearch process being swapped. Swapping is very bad for
performance and for node stability, so it should be avoided at all costs.</p><p>There are three options:</p><div><ul><li><p>
<strong>Disable swap</strong>
</p><p>The simplest option is to completely disable swap. Usually Elasticsearch
is the only service running on a box, and its memory usage is controlled
by the <code>ES_HEAP_SIZE</code> environment variable.  There should be no need
to have swap enabled.</p><p>On Linux systems, you can disable swap temporarily
by running: <code>sudo swapoff -a</code>. To disable it permanently, you will need
to edit the <code>/etc/fstab</code> file and comment out any lines that contain the
word <code>swap</code>.</p><p>On Windows, the equivalent can be achieved by disabling the paging file entirely
via <code>System Properties → Advanced → Performance → Advanced → Virtual memory</code>.</p></li><li><p>
<strong>Configure <code>swappiness</code></strong>
</p><p>The second option is to ensure that the sysctl value <code>vm.swappiness</code> is set
to <code>0</code>. This reduces the kernel’s tendency to swap and should not lead to
swapping under normal circumstances, while still allowing the whole system
to swap in emergency conditions.</p><div><div><img src="images/icons/note.png" alt="Note" /></div><div><p>From kernel version 3.5-rc1 and above, a <code>swappiness</code> of <code>0</code> will
cause the OOM killer to kill the process instead of allowing swapping.
You will need to set <code>swappiness</code> to <code>1</code> to still allow swapping in
emergencies.</p></div></div></li><li><p>
<strong><code>mlockall</code></strong>
</p><p>The third option is to use
<a href="http://opengroup.org/onlinepubs/007908799/xsh/mlockall.html" target="_blank">mlockall</a> on Linux/Unix systems, or <a href="https://msdn.microsoft.com/en-us/library/windows/desktop/aa366895%28v=vs.85%29.aspx" target="_blank">VirtualLock</a> on Windows, to
try to lock the process address space into RAM, preventing any Elasticsearch
memory from being swapped out.  This can be done, by adding this line
to the <code>config/elasticsearch.yml</code> file:</p><div><pre>bootstrap.mlockall: true</pre></div><p>After starting Elasticsearch, you can see whether this setting was applied
successfully by checking the value of <code>mlockall</code> in the output from this
request:</p><div><pre>curl http://localhost:9200/_nodes/process?pretty</pre></div><p>If you see that <code>mlockall</code> is <code>false</code>, then it means that the <code>mlockall</code>
request has failed.  The most probable reason, on Linux/Unix systems, is that
the user running Elasticsearch doesn’t have permission to lock memory.  This can
be granted by running <code>ulimit -l unlimited</code> as <code>root</code> before starting Elasticsearch.</p><p>Another possible reason why <code>mlockall</code> can fail is that the temporary directory
(usually <code>/tmp</code>) is mounted with the <code>noexec</code> option. This can be solved by
specifying a new temp directory, by starting Elasticsearch with:</p><div><pre>./bin/elasticsearch -Djna.tmpdir=/path/to/new/dir</pre></div><div><div><img src="images/icons/warning.png" alt="Warning" /></div><div><p><code>mlockall</code> might cause the JVM or shell session to exit if it tries
to allocate more memory than is available!</p></div></div></li></ul></div><h3>Elasticsearch Settings<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h3><p><strong>elasticsearch</strong> configuration files can be found under <code>ES_HOME/config</code>
folder. The folder comes with two files, the <code>elasticsearch.yml</code> for
configuring Elasticsearch different
<a href="modules.html" title="Modules" target="_blank">modules</a>, and <code>logging.yml</code> for
configuring the Elasticsearch logging.</p><p>The configuration format is <a href="http://www.yaml.org/" target="_blank">YAML</a>. Here is an
example of changing the address all network based modules will use to
bind and publish to:</p><div><pre>network :
    host : 10.0.0.4</pre></div><h4>Paths<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>In production use, you will almost certainly want to change paths for
data and log files:</p><div><pre>path:
  logs: /var/log/elasticsearch
  data: /var/data/elasticsearch</pre></div><h4>Cluster name<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>Also, don’t forget to give your production cluster a name, which is used
to discover and auto-join other nodes:</p><div><pre>cluster:
  name: &lt;NAME OF YOUR CLUSTER&gt;</pre></div><p>Make sure that you don’t reuse the same cluster names in different
environments, otherwise you might end up with nodes joining the wrong cluster.
For instance you could use <code>logging-dev</code>, <code>logging-stage</code>, and <code>logging-prod</code>
for the development, staging, and production clusters.</p><h4>Node name<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>You may also want to change the default node name for each node to
something like the display hostname. By default Elasticsearch will
randomly pick a Marvel character name from a list of around 3000 names
when your node starts up.</p><div><pre>node:
  name: &lt;NAME OF YOUR NODE&gt;</pre></div><p>The hostname of the machine is provided in the environment
variable <code>HOSTNAME</code>. If on your machine you only run a
single elasticsearch node for that cluster, you can set
the node name to the hostname using the <code>${...}</code> notation:</p><div><pre>node:
  name: ${HOSTNAME}</pre></div><h4>Configuration styles<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>Internally, all settings are collapsed into "namespaced" settings. For
example, the above gets collapsed into <code>node.name</code>. This means that
its easy to support other configuration formats, for example,
<a href="http://www.json.org" target="_blank">JSON</a>. If JSON is a preferred configuration format,
simply rename the <code>elasticsearch.yml</code> file to <code>elasticsearch.json</code> and
add:</p><div><pre>{
    "network" : {
        "host" : "10.0.0.4"
    }
}</pre></div><p>It also means that its easy to provide the settings externally either
using the <code>ES_JAVA_OPTS</code> or as parameters to the <code>elasticsearch</code>
command, for example:</p><div><pre>$ elasticsearch -Des.network.host=10.0.0.4</pre></div><p>Another option is to set <code>es.default.</code> prefix instead of <code>es.</code> prefix,
which means the default setting will be used only if not explicitly set
in the configuration file.</p><p>Another option is to use the <code>${...}</code> notation within the configuration
file which will resolve to an environment setting, for example:</p><div><pre>{
    "network" : {
        "host" : "${ES_NET_HOST}"
    }
}</pre></div><p>Additionally, for settings that you do not wish to store in the configuration
file, you can use the value <code>${prompt.text}</code> or <code>${prompt.secret}</code> and start
Elasticsearch in the foreground. <code>${prompt.secret}</code> has echoing disabled so
that the value entered will not be shown in your terminal; <code>${prompt.text}</code>
will allow you to see the value as you type it in. For example:</p><div><pre>node:
  name: ${prompt.text}</pre></div><p>On execution of the <code>elasticsearch</code> command, you will be prompted to enter
the actual value like so:</p><div><pre>Enter value for [node.name]:</pre></div><div><div><img src="images/icons/note.png" alt="Note" /></div><div><p>Elasticsearch will not start if <code>${prompt.text}</code> or <code>${prompt.secret}</code>
is used in the settings and the process is run as a service or in the background.</p></div></div><h3>Index Settings<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h3><p>Indices created within the cluster can provide their own settings. For
example, the following creates an index with a refresh interval of 5
seconds instead of the default refresh interval (the format can be either
YAML or JSON):</p><div><pre>$ curl -XPUT http://localhost:9200/kimchy/ -d \
'
index:
    refresh_interval: 5s
'</pre></div><p>Index level settings can be set on the node level as well, for example,
within the <code>elasticsearch.yml</code> file, the following can be set:</p><div><pre>index :
    refresh_interval: 5s</pre></div><p>This means that every index that gets created on the specific node
started with the mentioned configuration will use a refresh interval of
5 seconds <strong>unless the index explicitly sets it</strong>. In other words, any
index level settings override what is set in the node configuration. Of
course, the above can also be set as a "collapsed" setting, for example:</p><div><pre>$ elasticsearch -Des.index.refresh_interval=5s</pre></div><p>All of the index level configuration can be found within each
<a href="index-modules.html" title="Index Modules" target="_blank">index module</a>.</p><h3>Logging<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h3><p>Elasticsearch uses an internal logging abstraction and comes, out of the
box, with <a href="http://logging.apache.org/log4j/1.2/" target="_blank">log4j</a>. It tries to simplify
log4j configuration by using <a href="http://www.yaml.org/" target="_blank">YAML</a> to configure it,
and the logging configuration file is <code>config/logging.yml</code>. The
<a href="http://en.wikipedia.org/wiki/JSON" target="_blank">JSON</a> and
<a href="http://en.wikipedia.org/wiki/.properties" target="_blank">properties</a> formats are also
supported. Multiple configuration files can be loaded, in which case they will
get merged, as long as they start with the <code>logging.</code> prefix and end with one
of the supported suffixes (either <code>.yml</code>, <code>.yaml</code>, <code>.json</code> or <code>.properties</code>).
The logger section contains the java packages and their corresponding log
level, where it is possible to omit the <code>org.elasticsearch</code> prefix. The
appender section contains the destinations for the logs. Extensive information
on how to customize logging and all the supported appenders can be found on
the <a href="http://logging.apache.org/log4j/1.2/manual.html" target="_blank">log4j documentation</a>.</p><p>Additional Appenders and other logging classes provided by
<a href="http://logging.apache.org/log4j/extras/" target="_blank">log4j-extras</a> are also available,
out of the box.</p><h4>Deprecation logging<a href="https://github.com/elastic/elasticsearch/edit/2.3/docs/reference/setup/configuration.asciidoc" title="Edit this page on GitHub" target="_blank">edit</a></h4><p>In addition to regular logging, Elasticsearch allows you to enable logging
of deprecated actions. For example this allows you to determine early, if
you need to migrate certain functionality in the future. By default,
deprecation logging is disabled. You can enable it in the <code>config/logging.yml</code>
file by setting the deprecation log level to <code>DEBUG</code>.</p><div><pre>deprecation: DEBUG, deprecation_log_file</pre></div><p>This will create a daily rolling deprecation log file in your log directory.
Check this file regularly, especially when you intend to upgrade to a new
major version.</p>
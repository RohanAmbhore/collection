<a href="https://help.github.com/articles/searching-code/">https://help.github.com/articles/searching-code/</a><div id="articleHeader"><h1>Searching code</h1></div>

        


        
          <div>

          <p>You can search for code by using search qualifiers in any combination to narrow your search results.</p>

          </div>

          <p>Code in <a href="/articles/about-forks" target="_blank">forks</a> is only searchable if the fork has more stars than the parent repository. To include forks with more stars than their parent in the search results, you will need to add <code>fork:true</code> or <code>fork:only</code> to your query. For more information, see "<a href="/articles/searching-in-forks" target="_blank">Searching in forks</a>."</p>

<div>

<p><strong>Tips:</strong></p>

<ul>
<li>For a list of search syntaxes that you can add to any search qualifier to further improve your results, see "<a href="/articles/understanding-the-search-syntax" target="_blank">Understanding the search syntax</a>".</li>
<li>Use quotations around multi-word search terms. For example, if you want to search for issues with the label "In progress," you'd search for <code>label:"in progress"</code>. Search is not case sensitive.</li>
</ul>

</div>

<div>

<p><strong>Note:</strong> You must be logged in to search for code across all public repositories.</p>

</div>

<h3>
Considerations for code search</h3>

<p>Due to the complexity of searching code, there are a few restrictions on how searches are performed:</p>

<ul>
<li>Only the <em>default branch</em> is indexed for code search. In most cases, this will be the <code>master</code> branch.</li>
<li>Forks with fewer stars than the parent repository are <strong>not</strong> indexed for code search. For more information, see "<a href="/articles/searching-in-forks" target="_blank">Searching in forks</a>."</li>
<li>Only files smaller than 384 KB are searchable.</li>
<li>Only repositories with fewer than 500,000 files are searchable.</li>
<li>Logged in users can search all public repositories while anonymous searches must include a limit on <code>org:</code>, <code>user:</code>, or <code>repo:</code>.</li>
<li>Except with <a href="#search-by-filename" target="_blank"><code>filename</code></a> searches, you must always include at least one search term when searching source code. For example, searching for <a href="https://github.com/search?utf8=%E2%9C%93&q=language%3Ajavascript&type=Code&ref=searchresults" target="_blank"><code>language:javascript</code></a> is not valid, while <a href="https://github.com/search?utf8=%E2%9C%93&q=amazing+language%3Ajavascript&type=Code&ref=searchresults" target="_blank"><code>amazing language:javascript</code></a> is.</li>
<li>At most, search results can show two fragments from the same file, but there may be more results within the file.</li>
<li>You can't use the following wildcard characters as part of your search query: <code>. , : ; / \ ` ' " = * ! ? # $ & + ^ | ~ &lt; &gt; ( ) { } [ ]</code>. The search will simply ignore these symbols.</li>
</ul>

<h3>
Scope the search fields</h3>

<p>The <code>in</code> qualifier limits what fields are searched. With this qualifier, you can restrict your search to the source code, the file path, or both. Without the qualifier, only the file contents are searched.</p>

<table>
<thead>
<tr>
<th>Qualifier</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>in:file</code></td>
<td>
<a href="https://github.com/search?q=octocat+in%3Afile&type=Code" target="_blank"><strong>octocat in:file</strong></a> matches code where "octocat" appears in the file contents.</td>
</tr>
<tr>
<td><code>in:path</code></td>
<td>
<a href="https://github.com/search?q=octocat+in%3Apath&type=Code" target="_blank"><strong>octocat in:path</strong></a> matches code where "octocat" appears in the path name.</td>
</tr>
<tr>
<td></td>
<td>
<a href="https://github.com/search?q=octocat+in%3Afile%2Cpath&type=Code" target="_blank"><strong>octocat in:file,path</strong></a> matches code where "octocat" appears in the file contents or the path name.</td>
</tr>
</tbody>
</table>

<h3>
Search by language</h3>

<p>You can search for code based on what language it's written in.</p>

<table>
<thead>
<tr>
<th>Qualifier</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>language:<em>LANGUAGE</em></code></td>
<td>
<a href="https://github.com/search?q=element+language%3Axml+size%3A100&type=Code" target="_blank"><strong>element language:xml size:100</strong></a> matches code with the word "element" that's marked as being XML and has exactly 100 bytes.</td>
</tr>
<tr>
<td></td>
<td>
<a href="https://github.com/search?q=display+language%3Ascss&type=Code" target="_blank"><strong>display language:scss</strong></a> matches code with the word "display," that's marked as being SCSS.</td>
</tr>
<tr>
<td></td>
<td>
<a href="https://github.com/search?utf8=%E2%9C%93&q=org%3Amozilla+language%3Amarkdown&type=Code" target="_blank"><strong>org:mozilla language:markdown</strong></a> matches code from all @mozilla's repositories that's marked as Markdown.</td>
</tr>
</tbody>
</table>

<h3>
Search by the source code file size</h3>

<p>The <code>size</code> qualifier uses <a href="/articles/understanding-the-search-syntax" target="_blank">greater than, less than, and range qualifiers</a> to filter results based on the byte size of the file in which the code is found.</p>

<table>
<thead>
<tr>
<th>Qualifier</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>size:<em>n</em></code></td>
<td>
<a href="https://github.com/search?q=function+size%3A%3E10000+language%3Apython&type=Code" target="_blank"><strong>function size:&gt;10000 language:python</strong></a> matches code with the word "function," written in Python, in files that are larger than 10 KB.</td>
</tr>
</tbody>
</table>

<h3>
Search by the location of a file within the repository</h3>

<p>By including the <code>path</code> qualifier, you specify that resulting source code must appear at a specific location in a repository. Subfolders are considered during the search, so be as specific as possible. You can also use <code>path:/</code> to restrict the search results to the root level of the project.</p>

<table>
<thead>
<tr>
<th>Qualifier</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>path:<em>PATH/TO/DIRECTORY</em></code></td>
<td>
<a href="https://github.com/search?q=console+path%3A%22app%2Fpublic%22+language%3Ajavascript&type=Code" target="_blank"><strong>console path:app/public language:javascript</strong></a> matches JavaScript files with the word "console" in an <em>app/public</em> directory or its subdirectories (even if they reside in <em>app/public/js/form-validators</em>).</td>
</tr>
<tr>
<td><code>path:<em>DIRECTORY</em></code></td>
<td>
<a href="https://github.com/search?q=form+path%3Acgi-bin+language%3Aperl&type=Code" target="_blank"><strong>form path:cgi-bin language:perl</strong></a> matches Perl files with the word "form" in a <em>cgi-bin</em> directory.</td>
</tr>
<tr>
<td><code>path:/</code></td>
<td>
<a href="https://github.com/search?utf8=%E2%9C%93&q=octocat+filename%3Areadme+path%3A%2F&type=Code" target="_blank"><strong>octocat filename:readme path:/</strong></a> matches files named <em>readme</em> with the word "octocat" located at the root level of a repository.</td>
</tr>
</tbody>
</table>

<h3>
Search by filename</h3>

<p>You can use the <code>filename</code> qualifier if there's a specific file you're looking for.</p>

<table>
<thead>
<tr>
<th>Qualifier</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>filename:<em>FILENAME</em></code></td>
<td>
<a href="https://github.com/search?utf8=%E2%9C%93&q=filename%3Alinguist&type=Code" target="_blank"><strong>filename:linguist</strong></a> matches files named "linguist."</td>
</tr>
<tr>
<td></td>
<td>
<a href="https://github.com/search?q=filename%3A.vimrc+commands&type=Code" target="_blank"><strong>filename:.vimrc commands</strong></a> matches <em>.vimrc</em> files with the word "commands."</td>
</tr>
<tr>
<td></td>
<td>
<a href="https://github.com/search?q=minitest+filename%3Atest_helper+path%3Atest+language%3Aruby&type=Code" target="_blank"><strong>filename:test_helper path:test language:ruby</strong></a> matches Ruby files named <em>test_helper</em> within the <em>test</em> directory.</td>
</tr>
</tbody>
</table>

<h3>
Search by the file extension</h3>

<p>The <code>extension</code> qualifier matches code files with a certain file extension.</p>

<table>
<thead>
<tr>
<th>Qualifier</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>extension:<em>EXTENSION</em></code></td>
<td>
<a href="https://github.com/search?q=form+path%3Acgi-bin+extension%3Apm&type=Code" target="_blank"><strong>form path:cgi-bin extension:pm</strong></a> matches code with the word "form," under <em>cgi-bin</em>, with the <em>.pm</em> file extension.</td>
</tr>
<tr>
<td></td>
<td>
<a href="https://github.com/search?utf8=%E2%9C%93&q=icon+size%3A%3E200000+extension%3Acss&type=Code" target="_blank"><strong>icon size:&gt;200000 extension:css</strong></a> matches files larger than 200 KB that end in .css and have the word "icon."</td>
</tr>
</tbody>
</table>

<h3>
Search within a user's or organization's repositories</h3>

<p>To grab a list of code from all repositories owned by a certain user or organization, you can use the  <code>user</code> or <code>org</code> qualifier. For getting a list of code from a specific repository, you can use the <code>repo</code> qualifier.</p>

<table>
<thead>
<tr>
<th>Qualifier</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>user:<em>USERNAME</em></code></td>
<td>
<a href="https://github.com/search?q=user%3Agithub+extension%3Arb&type=Code" target="_blank"><strong>user:defunkt extension:rb</strong></a> matches code from @defunkt that ends in <em>.rb</em>.</td>
</tr>
<tr>
<td><code>org:<em>ORGNAME</em></code></td>
<td>
<a href="https://github.com/search?utf8=%E2%9C%93&q=org%3Agithub+extension%3Ajs&type=Code" target="_blank"><strong>org:github extension:js</strong></a> matches code from GitHub that ends in <em>.js</em>.</td>
</tr>
<tr>
<td><code>repo:<em>USERNAME/REPOSITORY</em></code></td>
<td>
<a href="https://github.com/search?q=repo%3Amozilla%2Fshumway+extension%3Aas&type=Code" target="_blank"><strong>repo:mozilla/shumway extension:as</strong></a> matches code from @mozilla's shumway project that ends in <em>.as</em>.</td>
</tr>
</tbody>
</table>

<h3>
Further reading</h3>


        
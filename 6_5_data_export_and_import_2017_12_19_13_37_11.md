<a href="https://dev.mysql.com/doc/workbench/en/wb-admin-export-import.html">https://dev.mysql.com/doc/workbench/en/wb-admin-export-import.html</a><div id="articleHeader"><h1>6.5 Data Export and Import</h1></div>

<p>
      There are three ways to export and import data in MySQL Workbench,
      each serving a different purpose.
    </p>
<div>
<p><b>Table 6.1 Methods to Export or Import data in MySQL Workbench</b></p>
<div><table>
<colgroup>
<col />
<col />
<col />
<col />
<col />
</colgroup>
<thead><tr>
<th>GUI Location</th>
<th>Data Set</th>
<th>Export Types</th>
<th>Import Types</th>
<th>Additional Details</th>
</tr></thead>
<tbody>
<tr>
<td>Object Browser context menu</td>
<td>Tables</td>
<td>JSON, CSV</td>
<td>JSON, CSV</td>
<td>Simple table operations, includes moderate control over the output type
              (this method was added in version 6.3.0)</td>
</tr>
<tr>
<td>Result Grid menu under the SQL editor</td>
<td>Result set (after performing an SQL query)</td>
<td>CSV, HTML, JSON, SQL, XML, Excel XML, TXT</td>
<td>CSV</td>
<td>Simple data operations, includes little control</td>
</tr>
<tr>
<td>Management Navigator</td>
<td>Databases and/or Tables</td>
<td>SQL</td>
<td>SQL</td>
<td>Detailed database and table operations, standard backup/restore behavior
              using the <strong>mysqldump</strong> command and meta
              data, includes control over how data is handled, and
              includes meta data</td>
</tr>
<tr>
<td>Management Navigator</td>
<td>Databases and/or Tables</td>
<td>SQL</td>
<td>SQL</td>
<td>Detailed database and table operations, includes control over how data
              is handled, can be scheduled and incremental, includes
              meta data, uses
              <a href="wb-mysql-enterprise-backup.html" title="6.7 MySQL Enterprise Backup Interface" target="_blank">MySQL Enterprise Backup</a>
              (commercial)</td>
</tr>
</tbody>
</table></div>



                
        
         

                     
<div id="docs-comments">
    <div> User Comments</div>

    

        <div>
        <a href="https://dev.mysql.com/auth/register/?dest=https%3A%2F%2Fdev.mysql.com%2Fdoc%2Fworkbench%2Fen%2Fwb-admin-export-import.html%3Facf%3D1%23add-comment" target="_blank">Sign Up</a>
        <a href="https://dev.mysql.com/auth/login/?dest=https%3A%2F%2Fdev.mysql.com%2Fdoc%2Fworkbench%2Fen%2Fwb-admin-export-import.html%3Facf%3D1%23add-comment" target="_blank">Login</a>
        You must be logged in to post a comment.
    </div>
    
              
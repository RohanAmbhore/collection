<a href="http://crud-admin-generator.com/">http://crud-admin-generator.com/</a><div id="articleHeader"><h1>CRUD Admin Generator</h1></div>
        <p><strong>An open source tool to generate a complete backend from a MySql database.</strong></p> <a href="https://github.com/jonseg/crud-admin-generator" target="_blank">Download now!</a>

<div id="share-buttons">

Share: 
 


 


 


 


 


 


 


 


 
</div>



    <div>
      
      <div> <div class="readableLargeImageContainer"><img src="images/main_laptop.png" /></div> 
    
  
</section>

<section id="whatis">
  <div>
    
    <div>
      
      <div> <div class="readableLargeImageContainer"><img src="images/full_screen2.png" /></div> <a href="https://github.com/jonseg/crud-admin-generator" target="_blank">Download now!</a> 
      
    
  
</section>

<section id="installation">
  <div>
    <div>
      
      <div>
        <h1>Installation</h1>Clone GitHub repository:<pre>git clone https://github.com/jonseg/crud-admin-generator.git admingenerator</pre>
<pre>cd admingenerator</pre>
<br />
Download composer:<pre>curl -sS https://getcomposer.org/installer | php</pre>
<br />
Install vendors:<pre>php composer.phar install</pre>
<br />
You need point the document root of your virtual host to /path_to/admingenerator/web<br /><br />This is an example of VirtualHost:<pre>&lt;VirtualHost *:80&gt;
   DocumentRoot /path_to/admingenerator/web
   DirectoryIndex index.php
   &lt;Directory "/path_to/admingenerator/web"&gt;
        Options Indexes FollowSymLinks
        Order Allow,Deny
        Allow from all
        AllowOverride all
        &lt;IfModule mod_php5.c&gt;
           php_admin_flag engine on
           php_admin_flag safe_mode off
           php_admin_value open_basedir none
        &lt;/ifModule&gt;
   &lt;/Directory&gt;
&lt;/VirtualHost&gt;
</pre>
<br />

You can customize the url using the .htaccess file, maybe this will help you:<br />
<a href="http://stackoverflow.com/questions/24952846/how-do-i-remove-the-web-from-my-url/24953439#24953439" target="_blank">http://stackoverflow.com/questions/24952846/how-do-i-remove-the-web-from-my-url/24953439#24953439</a>

<h1>Generate CRUD backend</h1>


Edit the file /path_to/admingenerator/src/app.php and set your database conection data:<pre>$app-&gt;register(new Silex\Provider\DoctrineServiceProvider(), array(
    'dbs.options' =&gt; array(
        'db' =&gt; array(
            'driver'   =&gt; 'pdo_mysql',
            'dbname'   =&gt; 'DATABASE_NAME',
            'host'     =&gt; 'localhost',
            'user'     =&gt; 'DATABASE_USER',
            'password' =&gt; 'DATABASE_PASS',
            'charset'  =&gt; 'utf8',
        ),
    )
));
</pre>
<br />
You need to set the url of the resources folder.
<br />
Change this line:
<pre>$app['asset_path'] = '/resources';
</pre>
<br />
For the url of your project, for example:
<pre>$app['asset_path'] = 'http://domain.com/crudadmin/resources';
</pre>
<br />
Now, execute the command that will generate the CRUD backend:<pre>php console generate:admin</pre>
<br />
<strong>This is it!</strong> Now access with your favorite web browser.<br /><br />The command generates one menu section for each database table. <strong>Now will be much easier to list, create, edit and delete rows!</strong>
        </div>
    
  
   
</section>


<section id="screenshots">
  <div> 
    <div>
      <div>
        <h1>Screenshots</h1>
      </div>
    
    <div>

          <div id="carousel-example-generic">
            
            

            
            <div>
              <div>
                <div class="readableLargeImageContainer"><img src="images/database.png" alt="Database" /></div>
              
              
              
              
              
            

            
            
            
              
        
  
   
</section>  

<section id="author">
  <div>
    <div>
      <div>
        <h1>Author</h1>
      </div>
    
    <div>
      
      <div> <a href="http://jonsegador.com/" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="images/Jon-Segador.png" /></div></a>
        <h3>Jon Segador</h3>
        Developer
        
<br /><br /><img src="https://www.paypalobjects.com/es_ES/i/scr/pixel.gif" width="1" height="1" />


      
    
    
    
  
</section>






 
 
 
 
 

 
 


<a href="https://github.com/jonseg/crud-admin-generator" target="_blank" class="readableLinkWithMediumImage"><img src="https://camo.githubusercontent.com/c6286ade715e9bea433b4705870de482a654f78a/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f6c6566745f77686974655f6666666666662e706e67" alt="Fork me on GitHub" /></a>





<div><h3>Like On Github</h3><div><div>*Title (label for the link)</div><div><div>*Comment (commit message)</div><div id="action-btns"><div id="logh_btn_save">Saving...</div><div id="logh_btn_cancel">Cancel</div>
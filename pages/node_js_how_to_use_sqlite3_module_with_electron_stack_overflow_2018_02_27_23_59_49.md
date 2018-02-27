<a href="https://stackoverflow.com/questions/32504307/how-to-use-sqlite3-module-with-electron">https://stackoverflow.com/questions/32504307/how-to-use-sqlite3-module-with-electron</a><div id="articleHeader"><h1>How to use sqlite3 module with electron?</h1></div>

<p>I want to develop desktop app using <a href="http://electron.atom.io/" target="_blank">electron</a> that uses sqlite3 package installed via npm with the command</p>

<pre><code>npm install --save sqlite3</code></pre>

<p>but it gives the following error in electron browser console</p>

<pre><code>Uncaught Error: Cannot find module 'E:\allcode\eapp\node_modules\sqlite3\lib\binding\node-v45-win32-x64\node_sqlite3.node'</code></pre>

<p>My development environment is windows 8.1 x64
node version 12.7</p>

<p>my <strong>package.json</strong> file looks like this:</p>

<pre><code>{
  "name": "eapp",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "electron ."
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "electron-prebuilt": "^0.32.1"
  },
  "dependencies": {
    "angular": "^1.3.5",   
    "sqlite3": "^3.1.0"
  }
}</code></pre>

<p><strong>index.js file</strong></p>

<pre><code>var app = require('app');
var BrowserWindow = require('browser-window'); 
require('crash-reporter').start();
var mainWindow = null;


app.on('window-all-closed', function() {  
    if (process.platform != 'darwin') {
        app.quit();
    }
});

app.on('ready', function() {
    // Create the browser window.
    mainWindow = new BrowserWindow({width: 800, height: 600}); 
    mainWindow.loadUrl('file://' + __dirname + '/index.html');   
    mainWindow.openDevTools();  
    mainWindow.on('closed', function() {       
        mainWindow = null;
    });
});</code></pre>

<p><strong>my.js file</strong> </p>

<pre><code>var sqlite3 = require('sqlite3').verbose();
var db = new sqlite3.Database('mydb.db');

db.serialize(function() {
    db.run("CREATE TABLE if not exists lorem (info TEXT)");

    var stmt = db.prepare("INSERT INTO lorem VALUES (?)");
    for (var i = 0; i &lt; 10; i++) {
        stmt.run("Ipsum " + i);
    }
    stmt.finalize();

    db.each("SELECT rowid AS id, info FROM lorem", function(err, row) {
        console.log(row.id + ": " + row.info);
    });
});

db.close();</code></pre>

<p><strong>index.html file</strong></p>

<pre><code>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head lang="en"&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;title&gt;&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;div &gt;
    &lt;div&gt;
        &lt;h2&gt;Hello&lt;/h2&gt;
    &lt;/div&gt;

&lt;/div&gt;
&lt;!--&lt;script src="js/jquery-1.11.3.min.js"&gt;&lt;/script&gt;--&gt;
&lt;script src="js/my.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
    
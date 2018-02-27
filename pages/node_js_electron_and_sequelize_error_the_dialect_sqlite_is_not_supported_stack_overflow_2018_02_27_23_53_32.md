<a href="https://stackoverflow.com/questions/32423097/electron-and-sequelize-error-the-dialect-sqlite-is-not-supported">https://stackoverflow.com/questions/32423097/electron-and-sequelize-error-the-dialect-sqlite-is-not-supported</a><div id="articleHeader"><h1>Electron and sequelize error: the dialect sqlite is not supported</h1></div>

<p>I'm trying to use <a href="http://sequelizejs.com" target="_blank">sequelize</a> and sqlite with <a href="http://electron.atom.io/" target="_blank">electron</a> in a desktop application but get the following error when running the app via <code>npm start</code> (which runs <code>node_modules/.bin/electron .</code>):</p>

<blockquote>
  <p>Uncaught Error: The dialect sqlite is not supported. (Error: Please install sqlite3 package manually)</p>
</blockquote>

<p>I've installed sequelize and sqlite with <code>npm install --save sequelize sqlite</code>. When I run the models file directly via <code>node models.js</code>, everything works fine:</p>

<pre><code>$ node models.js
Executing (default): CREATE TABLE IF NOT EXISTS `Users` (`id` INTEGER PRIMARY KEY AUTOINCREMENT, `username` VARCHAR(255), `birthday` DATETIME, `createdAt` DATETIME NOT NULL, `updatedAt` DATETIME NOT NULL);
Executing (default): PRAGMA INDEX_LIST(`Users`)
Executing (default): INSERT INTO `Users` (`id`,`username`,`birthday`,`updatedAt`,`createdAt`) VALUES (NULL,'janedoe','1980-07-19 22:00:00.000 +00:00','2015-09-06 11:18:52.412 +00:00','2015-09-06 11:18:52.412 +00:00');
{ id: 1,
  username: 'janedoe',
  birthday: Sun Jul 20 1980 00:00:00 GMT+0200 (CEST),
  updatedAt: Sun Sep 06 2015 13:18:52 GMT+0200 (CEST),
  createdAt: Sun Sep 06 2015 13:18:52 GMT+0200 (CEST) }</code></pre>

<p>So the problem is specific to using sequelize with electron. All files are shown below.</p>

<p><strong>package.json</strong></p>

<pre><code>{
  "name": "example",
  "version": "0.0.0",
  "description": "",
  "main": "app.js",
  "scripts": {
    "start": "node_modules/.bin/electron .",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "devDependencies": {
    "electron-prebuilt": "^0.31.1"
  },
  "dependencies": {
    "jquery": "^2.1.4",
    "sequelize": "^3.7.1",
    "sqlite3": "^3.0.10"
  }
}</code></pre>

<p><strong>app.js</strong></p>

<pre><code>var app = require('app');
var BrowserWindow = require('browser-window');

require('crash-reporter').start();

var mainWindow = null;

app.on('window-all-closed', function() {
    if (process.platform !== 'darwin') {
        app.quit();
    }
});

app.on('ready', function() {
    mainWindow = new BrowserWindow({width: 800, height: 600});
    mainWindow.loadUrl('file://' + __dirname + '/index.html');
    mainWindow.on('closed', function() {
        mainWindow = null;
    });
});</code></pre>

<p><strong>index.html</strong></p>

<pre><code>&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
    &lt;head&gt;
        &lt;!-- Required meta tags always come first --&gt;
        &lt;meta charset="utf-8"&gt;
        &lt;meta name="viewport" content="width=device-width, initial-scale=1"&gt;
        &lt;meta http-equiv="x-ua-compatible" content="ie=edge"&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;p&gt;Example&lt;/p&gt;

        &lt;script src="models.js"&gt;&lt;/script&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>

<p><strong>models.js</strong></p>

<pre><code>var Sequelize = require('sequelize');
var sequelize = new Sequelize('bdgt', 'username', 'password', {
    dialect: 'sqlite',
    storage: 'example.db',
});

var User = sequelize.define('User', {
    username: Sequelize.STRING,
    birthday: Sequelize.DATE
});

sequelize.sync().then(function() {
    return User.create({
        username: 'janedoe',
        birthday: new Date(1980, 6, 20)
    });
}).then(function(jane) {
    console.log(jane.get({
        plain: true
    }));
});</code></pre>

<p>Install the dependencies using <code>npm install</code> and reproduce the problem using <code>npm start</code>. Running <code>node models.js</code> will show sequelize works one its own.</p>
    
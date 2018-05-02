<a href="https://stackoverflow.com/questions/37165871/cheerio-cssproperty-always-returns-null?rq=1">https://stackoverflow.com/questions/37165871/cheerio-cssproperty-always-returns-null?rq=1</a><div id="articleHeader"><h1>Cheerio .css([property]) always returns null?</h1></div>

<p>I've recently started to work with <strong>NodeJS</strong> together with <strong>Cheerio</strong>. 
I'm getting an external URL, and loading the html with Cheerio.</p>

<p>I've stumbled upon an issue, whenever I'm trying to get the css properties of an element, <code>$.css([property])</code> always returns <code>null</code>, no matter what selector or property I give it.</p>

<p>What I'm doing: </p>

<pre><code>var express = require('express');
var fs = require('fs');
var request = require('request');
var cheerio = require('cheerio');
app = express();

app.get('/something_something', function (req, res) {
   request('some_url', function (error, response, html) {
       var $ = cheerio.load(html)
//
       console.log($('body').css('width'));
   }
}</code></pre>

<p>This will always log <code>null</code>, no matter what selector or css property it has. (Please bear in mind I've over-checked if the jQuery object $('body') exists, and this happens no matter what URL there is)</p>

<p>Also, if I set <code>$('body').css('width', '100px')</code> 
and then <code>console.log($('body').css('width'))</code>, it will display 100px. So I'm guessing it's not the css() method itself, but the way Cheerio gets / doesn't get the styles of elements</p>

<p>*Other Cheerio methods work, such as <code>text()</code>, <code>val()</code>, <code>remove()</code>.</p>

<p>I'm still a NodeJS/Cheerio newbie, so any help, explanation, suggestion or info would be golden,</p>

<p>Cheerio!</p>
    
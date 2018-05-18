<a href="https://www.christianengvall.se/electron-localization/">https://www.christianengvall.se/electron-localization/</a><div id="articleHeader"><h1>Electron localization</h1></div> <header> <figure> <a href="/electron-localization/" target="_blank" class="readableLinkWithLargeImage"> <div class="readableLargeImageContainer"><img src="https://www.christianengvall.se/wp-content/uploads/2016/10/Electron-localization-1024x535.png"   alt="Electron localization" /></div>  </a> </figure> <h2> Electron localization </h2> <time> 27 October 2016 </time> </header> <section> <div> <div> <p>Let us add localization to the <a href="https://github.com/crilleengvall/electron-tutorial-app" target="_blank">electron tutorial app</a>. We will look at translating both in the main and renderer process.</p> <p>I tried some of the already existing npm-packages that helps with translating your app. They were good but didn’t feel 100% right to me. Some of them used .po-files, some of them were too advanced. So I decided to write a simpler one on my own. This is just a matter of taste. If you find another way that suits you better you should do it like that instead.</p> <p>The localization script will store translations in .js files with a json-structure. It will use english as a fallback language, and try to use the users language by default. If no translation is found the original phrase will be sent back to be used.</p> <h2 id="1adding-the-script">1.Adding the script</h2> <p>Create a new folder in the project called translations. Create a new .js file and copy the contents below and save the file as i18n.js (<a href="https://en.wikipedia.org/wiki/Internationalization_and_localization" target="_blank">why i18n?</a>)</p> <figure><pre><code>const path = require("path")
const electron = require('electron')
const fs = require('fs');
let loadedLanguage;
let app = electron.app ? electron.app : electron.remote.app

module.exports = i18n;

function i18n() {
    if(fs.existsSync(path.join(__dirname, app.getLocale() + '.js'))) {
         loadedLanguage = JSON.parse(fs.readFileSync(path.join(__dirname, app.getLocale() + '.js'), 'utf8'))
    }
    else {
         loadedLanguage = JSON.parse(fs.readFileSync(path.join(__dirname, 'en.js'), 'utf8'))
    }
}

i18n.prototype.__ = function(phrase) {
    let translation = loadedLanguage[phrase]
    if(translation === undefined) {
         translation = phrase
    }
    return translation
}</code></pre></figure> <p>In the i18n <strong>constructor</strong> the script first checks if a language file for the current users locale exists. If it does that file is loaded. If the file does not exist the script loads the fallback language in en.js.</p> <p>the <strong>__</strong> function takes a phrase as an argument and checks if that is translated in the loadedLanguage. If it’s not it returns the phrase sent to the function.</p> <p>This line takes care of loading app from either the main(mainmenu.js) or renderer(from index.html) process.</p> <figure><pre><code>let app = electron.app ? electron.app : electron.remote.app</code></pre></figure> <h2 id="2adding-translation-files">2.Adding translation files</h2> <p>Since i am from Sweden I will locate the tutorial app into Swedish. So I will create en.js and sv.js in the translations folder. To know what you should name your file so that the i18n script will find it and load it you can add this to main.js which will log the locale to the terminal(just add .js to it):</p> <figure><pre><code>console.log(app.getLocale())</code></pre></figure> <p>This is how the structure in the translation files should look. This is what <strong>en.js</strong> will look like:</p> <figure><pre><code>{
 "Edit": "Edit",
 "Undo": "Undo",
 "Redo": "Redo",
 "Cut": "Cut",
 "Copy": "Copy",
 "Paste": "Paste",
 "Delete": "Delete",
 "Select all": "Select all",
 "View": "View",
 "Speech": "Speech",
 "Start speaking": "Start speaking",
 "Stop speaking": "Stop speaking",
 "Actual size": "Actual size",
 "Zoom in": "Zoom in",
 "Zoom out": "Zoom out",
 "Toggle fullscreen": "Toggle fullscreen",
 "Window": "Window",
 "Minimize": "Minimize",
 "Close": "Close",
 "Help": "Help",
 "Learn more": "Learn more",
 "About": "About",
 "Services": "Services",
 "Hide": "Hide",
 "Hide others": "Hide others",
 "Unhide": "Unhide",
 "Quit": "Quit",
 "Zoom": "Zoom",
 "Bring all to front": "Bring all to front"
}</code></pre></figure> <p>And this is what my <strong>sv.js</strong> looks like:</p> <figure><pre><code>{
 "Edit": "Redigera",
 "Undo": "Ångra",
 "Redo": "Gör om",
 "Cut": "Klipp ut",
 "Copy": "Kopiera",
 "Paste": "Klistra in",
 "Delete": "Radera",
 "Select all": "Markera allt",
 "Speech": "Tal",
 "Start speaking": "Börja tala",
 "Stop speaking": "Sluta tala",
 "View": "Visa",
 "Actual size": "Faktisk storlek",
 "Zoom in": "Zooma in",
 "Zoom out": "Zooma ut",
 "Zoom": "Zooma",
 "Toggle fullscreen": "Helskärmsläge",
 "Window": "Fönster",
 "Minimize": "Minimera",
 "Close": "Stäng",
 "Help": "Hjälp",
 "Learn more": "Läs mer",
 "About": "Om",
 "Services": "Tjänster",
 "Hide" : "Göm",
 "Hide others": "Göm övriga",
 "Unhide": "Visa alla",
 "Quit": "Avsluta",
 "Bring all to front": "Flytta fram alla"
}</code></pre></figure> <h2 id="3translating-the-menu-main-process">3.Translating the menu (Main process)</h2> <p>As you might have guessed when reading the translation they look like menu items. So let us translate the <a href="/electron-menu/" target="_blank">menu</a> that was added in the last tutorial.</p> <p>Open up <strong>mainmenu.js</strong> that is located in the menu folder and add this require statement to the top of the file:</p> <figure><pre><code>const {Menu} = require('electron')
const electron = require('electron')
const app = electron.app
var i18n = new(require('../translations/i18n'))</code></pre></figure> <p>Now all we need to do is call i18n.__() for every menu item. These are what the first three looks like, here is the fully <a href="https://github.com/crilleengvall/electron-tutorial-app/blob/154ec39afe55ab46d1867bb8d83359d23d719fd7/menu/mainmenu.js" target="_blank">translated menu file</a>.</p> <figure><pre><code>const {Menu} = require('electron')
const electron = require('electron')
const app = electron.app
var i18n = new(require('../translations/i18n'))

const template = [
 {
     label: i18n.__('Edit'),
     submenu: [
     {
         role: 'undo', label: i18n.__('Undo')
     },
     {
         role: 'redo', label: i18n.__('Redo')
     },
....</code></pre></figure> <p>What you do is add the <strong>label:</strong> attribute to the menu item, which gets the translated value from i18n__().</p> <h2 id="4translating-navigation-menu-in-indexjs-renderer-process">4.Translating navigation menu in index.js (Renderer process)</h2> <p>Create a new file in assets/js/ called <strong>translations.js</strong>. In this one we’ll use jquery to set the translated strings to our html-markup.</p> <p>Open index.html and add i18n int the list of scripts.</p> <figure><pre><code> &lt;!-- Scripts --&gt;
 &lt;script&gt;window.$ = window.jQuery = require('./assets/js/jquery.min.js');&lt;/script&gt;
 &lt;script&gt;window.i18n = new(require('./translations/i18n'));&lt;/script&gt;
 &lt;script src="assets/js/jquery.scrollex.min.js"&gt;&lt;/script&gt;
 &lt;script src="assets/js/jquery.scrolly.min.js"&gt;&lt;/script&gt;
 &lt;script src="assets/js/skel.min.js"&gt;&lt;/script&gt;
 &lt;script src="assets/js/util.js"&gt;&lt;/script&gt;
 &lt;script src="assets/js/main.js"&gt;&lt;/script&gt;
 &lt;script&gt;
 require('./assets/js/menu')
 require('./assets/js/translations')
 &lt;/script&gt;
 &lt;/body&gt;
&lt;/html&gt;</code></pre></figure> <p>In translations.js it’s plain jquery to set the text of the elements that you wish to translate:</p> <figure><pre><code>window.localization = window.localization || {},
function(n) {
     localization.translate = {

     menu: function() {
         $('#welcome-menu').text(i18n.__('Welcome'));
    },

   welcome: function() {
       $('#welcome .inner p').text(i18n.__('Hopefully this helps someone to get up to speed with electron.'));
   },

   init: function() {
         this.welcome();
         this.menu();
   }
 };

 n(function() {
     localization.translate.init();
 })

}(jQuery);</code></pre></figure> <p>This is just two translations that are added. You can see the <a href="https://github.com/crilleengvall/electron-tutorial-app/blob/154ec39afe55ab46d1867bb8d83359d23d719fd7/assets/js/translations.js" target="_blank">full file here</a>.</p> <p>The app now looks like this when running it on an os set to Swedish language:</p> <div> <a href="/wp-content/uploads/2016/10/Electron-tutorial-app-windows-translated-swedish.png" target="_blank" class="readableLinkWithLargeImage"> <div class="readableLargeImageContainer"><img src="/wp-content/uploads/2016/10/Electron-tutorial-app-windows-translated-swedish-1024x565.png"   alt="electron tutorial app windows - translated to swedish" /></div>  </a> <p>electron tutorial app windows - translated to swedish</p> </div> <p><a href="http://www.freepik.com/free-vector/cute-globe-icon_820866.htm" target="_blank">Designed by Freepik</a></p>  </div>    </div> </section> 
<a href="https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image">https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image</a><div id="articleHeader"><h1>Paste Image</h1></div>
<p>Paste image directly from clipboard to markdown/asciidoc(or other file)!</p>
<p><strong>Support Mac/Windows/Linux!</strong> And support config destination folder.</p>
<p><div class="readableLargeImageContainer"><img src="https://raw.githubusercontent.com/mushanshitiancai/vscode-paste-image/master/res/vscode-paste-image.gif" alt="paste-image" /></div></p>
<h2 id="user-content-usage">Usage</h2>
<ol>
<li>capture screen to clipboard</li>
<li>Open the command palette: <code>Ctrl+Shift+P</code> (<code>Cmd+Shift+P</code> on Mac)</li>
<li>Type: "Paste Image" or you can use default keyboard binding: <code>Ctrl+Alt+V</code> (<code>Cmd+Alt+V</code> on Mac).</li>
<li>Image will be saved in the folder that contains current editing file</li>
<li>The relative path will be paste to current editing file</li>
</ol>
<h2 id="user-content-config">Config</h2>
<ul>
<li>
<p><code>pasteImage.defaultName</code></p>
<p>The default image file name.</p>
<p>The value of this config will be pass to the 'format' function of moment library(a js time manipulation library), you can read document <a href="https://momentjs.com/docs/#/displaying/format/" target="_blank">https://momentjs.com/docs/#/displaying/format/</a> for advanced usage.</p>
<p>And you can use variable:</p>
<ul>
<li><code>${currentFileName}</code>: the current file name with ext.</li>
<li><code>${currentFileNameWithoutExt}</code>: the current file name without ext.</li>
</ul>
<p>Default value is <code>Y-MM-DD-HH-mm-ss</code>.</p>
</li>
<li>
<p><code>pasteImage.path</code></p>
<p>The destination to save image file.</p>
<p>You can use variable:</p>
<ul>
<li><code>${currentFileDir}</code>: the path of directory that contain current editing file.</li>
<li><code>${projectRoot}</code>: the path of the project opened in vscode.</li>
<li><code>${currentFileName}</code>: the current file name with ext.</li>
<li><code>${currentFileNameWithoutExt}</code>: the current file name without ext.</li>
</ul>
<p>Default value is <code>${currentFileDir}</code>.</p>
</li>
<li>
<p><code>pasteImage.basePath</code></p>
<p>The base path of image url.</p>
<p>You can use variable:</p>
<ul>
<li><code>${currentFileDir}</code>: the path of directory that contain current editing file.</li>
<li><code>${projectRoot}</code>: the path of the project opened in vscode.</li>
<li><code>${currentFileName}</code>: the current file name with ext.</li>
<li><code>${currentFileNameWithoutExt}</code>: the current file name without ext.</li>
</ul>
<p>Default value is <code>${currentFileDir}</code>.</p>
</li>
<li>
<p><code>pasteImage.forceUnixStyleSeparator</code></p>
<p>Force set the file separator styel to unix style. If set false, separator styel will follow the system style.</p>
<p>Default is <code>true</code>.</p>
</li>
<li>
<p><code>pasteImage.prefix</code></p>
<p>The string prepend to the resolved image path before paste.</p>
<p>Default is <code>""</code>.</p>
</li>
<li>
<p><code>pasteImage.suffix</code></p>
<p>The string append to the resolved image path before paste.</p>
<p>Default is <code>""</code>.</p>
</li>
<li>
<p><code>pasteImage.encodePath</code></p>
<p>How to encode image path before insert to editor. Support options:</p>
<ul>
<li><code>none</code>: do nothing, just insert image path to text</li>
<li><code>urlEncode</code>: url encode whole image path</li>
<li><code>urlEncodeSpace</code>: url encode only space character(sapce to %20)</li>
</ul>
<p>Defalut is <code>urlEncodeSpace</code>.</p>
</li>
<li>
<p><code>pasteImage.namePrefix</code></p>
<p>The string prepend to the image file name.</p>
<p>You can use variable:</p>
<ul>
<li><code>${currentFileDir}</code>: the path of directory that contain current editing file.</li>
<li><code>${projectRoot}</code>: the path of the project opened in vscode.</li>
<li><code>${currentFileName}</code>: the current file name with ext.</li>
<li><code>${currentFileNameWithoutExt}</code>: the current file name without ext.</li>
</ul>
<p>Default is <code>""</code>.</p>
</li>
<li>
<p><code>pasteImage.nameSuffix</code></p>
<p>The string append to the image name.</p>
<p>You can use variable:</p>
<ul>
<li><code>${currentFileDir}</code>: the path of directory that contain current editing file.</li>
<li><code>${projectRoot}</code>: the path of the project opened in vscode.</li>
<li><code>${currentFileName}</code>: the current file name with ext.</li>
<li><code>${currentFileNameWithoutExt}</code>: the current file name without ext.</li>
</ul>
<p>Default is <code>""</code>.</p>
</li>
<li>
<p><code>pasteImage.insertPattren</code></p>
<p>The pattern of string that would be pasted to text.</p>
<p>You can use variable:</p>
<ul>
<li><code>${imageFilePath}</code>: the image file path, with <code>pasteImage.prefix</code>, <code>pasteImage.suffix</code>, and url encoded.</li>
<li><code>${imageOriginalFilePath}</code>: the image file path.</li>
<li><code>${imageFileName}</code>:  the image file name with ext.</li>
<li><code>${imageFileNameWithoutExt}</code>: the image file name without ext.</li>
<li><code>${currentFileDir}</code>: the path of directory that contain current editing file.</li>
<li><code>${projectRoot}</code>: the path of the project opened in vscode.</li>
<li><code>${currentFileName}</code>: the current file name with ext.</li>
<li><code>${currentFileNameWithoutExt}</code>: the current file name without ext.</li>
<li><code>${imageSyntaxPrefix}</code>: in markdown file it would be <code>![](<a href="https://github.com/mushanshitiancai/vscode-paste-image/raw/master/" target="_blank">https://github.com/mushanshitiancai/vscode-paste-image/raw/master/</a></code>, in asciidoc file it would be <code>image::</code>, in other file it would be empty string</li>
<li><code>${imageSyntaxSuffix}</code>: in markdown file it would be <code>)</code>, in asciidoc file it would be <code>[]</code>, in other file it would be empty string</li>
</ul>
<p>Defalut is <code>${imageSyntaxPrefix}${imageFilePath}${imageSyntaxSuffix}</code>.</p>
</li>
</ul>
<h2 id="user-content-config-example">Config Example</h2>
<p>I use vscode to edit my hexo blog. The folder struct like this:</p>
<pre><code>blog/source/_posts  (articles)
blog/source/img     (images)
</code></pre>
<p>I want to save all image in <code>blog/source/img</code>, and insert image url to article. And hexo will generate <code>blog/source/</code> as the website root, so the image url shoud be like <code>/img/xxx.png</code>. So I can config pasteImage in <code>blog/.vscode/setting.json</code> like this:</p>
<pre><code>"pasteImage.path": "${projectRoot}/source/img",
"pasteImage.basePath": "${projectRoot}/source",
"pasteImage.forceUnixStyleSeparator": true,
"pasteImage.prefix": "/"
</code></pre>
<p>If you want to save image in separate directory:</p>
<pre><code>"pasteImage.path": "${projectRoot}/source/img/${currentFileNameWithoutExt}",
"pasteImage.basePath": "${projectRoot}/source",
"pasteImage.forceUnixStyleSeparator": true,
"pasteImage.prefix": "/"
</code></pre>
<p>If you want to save image with article name as prefix:</p>
<pre><code>"pasteImage.namePrefix": "${currentFileNameWithoutExt}_",
"pasteImage.path": "${projectRoot}/source/img",
"pasteImage.basePath": "${projectRoot}/source",
"pasteImage.forceUnixStyleSeparator": true,
"pasteImage.prefix": "/"
</code></pre>
<p>If you want to use html in markdown:</p>
<pre><code>"pasteImage.insertPattern": "&lt;img&gt;${imageFileName}&lt;/img&gt;"
"pasteImage.path": "${projectRoot}/source/img",
"pasteImage.basePath": "${projectRoot}/source",
"pasteImage.forceUnixStyleSeparator": true,
"pasteImage.prefix": "/"
</code></pre>
<h2 id="user-content-format">Format</h2>
<h3 id="user-content-file-name-format">File name format</h3>
<p>If you selected some text in editor, then extension will use it as the image file name. <strong>The selected text can be a sub path like <code>subFolder/subFolder2/nameYouWant</code>.</strong></p>
<p>If not the image will be saved in this format: "Y-MM-DD-HH-mm-ss.png". You can config default image file name by <code>pasteImage.defaultName</code>.</p>
<h3 id="user-content-file-link-format">File link format</h3>
<p>When you editing a markdown, it will pasted as markdown image link format <code>![](https://github.com/mushanshitiancai/vscode-paste-image/raw/master/imagePath)</code>.</p>
<p>When you editing a asciidoc, it will pasted as asciidoc image link format <code>image::imagePath[]</code>.</p>
<p>In other file, it just paste the image's path.</p>
<p>Now you can use configuration <code>pasteImage.insertPattern</code> to config the fomat of file link.</p>
<h2 id="user-content-contact">Contact</h2>
<p>If you have some any question or advice, Welcome to <a href="https://github.com/mushanshitiancai/vscode-paste-image/issues" target="_blank">issue</a></p>

<ul>
<li> support win (by @kivle)</li>
<li> support linux</li>
<li> support use the selected text as the image name</li>
<li> support config (@ysknkd in #4)</li>
<li> support config relative/absolute path (@ysknkd in #4)</li>
<li> support asciidoc</li>
<li> supoort use variable ${projectRoot} and ${currentFileDir} in config</li>
<li> support config basePath</li>
<li> support config forceUnixStyleSeparator</li>
<li> support config prefix</li>
<li> support config suffix</li>
<li> supoort use variable ${currentFileName} and ${currentFileNameWithoutExt} in config</li>
<li> support check if the dest directory is a file</li>
<li> support select text as a sub path with multi new directory like <code>a/b/c/d/imageName</code> or <code>../a/b/c/d/imageName</code></li>
<li> support config default image name pattern</li>
<li> support config the text format</li>
</ul>
<h2 id="user-content-license">License</h2>
<p>The extension and source are licensed under the <a href="https://github.com/mushanshitiancai/vscode-paste-image/blob/master/LICENSE.txt" target="_blank">MIT license</a>.</p>
<h2 id="user-content-donate">Donate</h2>
<p>If you like this plugin, you can donate to me to support me develop it better, thank you!</p>
<p>PayPal:</p>
<p><div class="readableLargeImageContainer"><img src="https://raw.githubusercontent.com/mushanshitiancai/vscode-paste-image/master/res/alipay.png" alt="alipay" /></div></p>
<p>微信支付:</p>
<p><div class="readableLargeImageContainer"><img src="https://raw.githubusercontent.com/mushanshitiancai/vscode-paste-image/master/res/weixin.png" alt="weixin" /></div></p>
<p>Donator list：</p>
<ul>

<li>Paul Egbert</li>
<li>CallOnISS</li>
</ul>

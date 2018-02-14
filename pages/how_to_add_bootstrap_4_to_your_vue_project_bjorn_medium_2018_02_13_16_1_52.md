<a href="https://medium.com/@BjornKrols/integrating-and-customising-bootstrap-4-in-vue-js-cbc29ba7688e">https://medium.com/@BjornKrols/integrating-and-customising-bootstrap-4-in-vue-js-cbc29ba7688e</a><div id="articleHeader"><h1>How to add Bootstrap 4 to your Vue project</h1></div><p id="4052">This small tutorial covers how to add Bootstrap 4 (with customizations) to your Vue.js project.</p><p id="2f5d">This is aimed at Webpack users and targets version 4 of Bootstrap (<a href="https://getbootstrap.com/" target="_blank">https://getbootstrap.com/</a>).</p><p id="1b2d">This tutorial does not cover anything jQuery related. If you do want rapid out-of-the box JS functionality I recommend <a href="https://bootstrap-vue.js.org/" target="_blank">https://bootstrap-vue.js.org/</a> which is a Vue wrapper for Bootstrap and is 100% compatible with this tutorial.</p><p id="8f01">The starting point of this tutorial will be the vue-cli webpack-simple template.<br /><a href="https://github.com/vuejs-templates/webpack-simple" target="_blank">https://github.com/vuejs-templates/webpack-simple</a></p><p id="eb80">You can get the full code of this tutorial on github here: <a href="https://github.com/Botre/make-bootstrap-sexy-again" target="_blank">https://github.com/Botre/make-bootstrap-sexy-again</a></p><h3 id="521a">Installing Bootstrap</h3><p id="ca28"><code>npm install bootstrap --save</code></p><h3 id="28f8">Installing Node-sass</h3><p id="c00d">Node-sass is a library that provides binding for Node.js to <a href="https://github.com/sass/libsass" target="_blank">LibSass</a>, the C version of the popular stylesheet preprocessor, Sass.</p><p id="0443">It allows you to natively compile .scss files to css at incredible speed and automatically via a connect middleware.</p><p id="d8e8"><code>npm install node-sass --save --dev</code></p><h3 id="d50a"><strong>Installing sass-loader for Webpack</strong></h3><p id="9dd7">Loads SASS/SCSS and compiles it to CSS.</p><p id="604a"><code>npm install sass-loader --save --dev</code></p><h3 id="d47e">Adapting your Webpack configuration</h3><p id="e2b7">2 actions:</p><p id="2ed5"><strong>Update </strong>existing rule: add the sass-loader to the .vue$ rule</p><p id="4228"><strong>Create </strong>a new rulefor .scss$</p><h3 id="ffaa">Importing bootstrap.scss file in entry component</h3><p id="1829">This will usually be called App.vue.</p><p id="1ec0">Any future bootstrap-specific customization should be declared <strong>before</strong> this import</p><p id="f6ff">That’s it for the integration part, at this point you should be able to add vanilla-looking Bootstrap components to your application.</p><h3 id="3dc3">Creating your customization file</h3><p id="2f2a">You don’t need to declare your customization in a separate file, but let’s not clutter our Vue component unnecessarily.</p><p id="c587">I created a ‘custom-bootstrap.scss’ file (you can name it anything you want) with the following contents:</p><h3 id="8949">Importing your customization file</h3><p id="37d6">Now it’s just a matter off importing the file.</p><p id="7269">Please do make sure the new import is added<strong> before</strong> the bootstrap.scss file!</p><h3 id="2de0">Final implementation (with HTML)</h3><figure id="554a"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/90/1*yf2Dl3bVln3CJdnYZmYkdg.png?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/2000/1*yf2Dl3bVln3CJdnYZmYkdg.png" /></div></figure><h3 id="b198">Github</h3><p id="fa4a">In case you get stuck you can get the full code on github here: <a href="https://github.com/Botre/make-bootstrap-sexy-again" target="_blank">https://github.com/Botre/make-bootstrap-sexy-again</a></p><h3 id="7122">Done!</h3><p id="dc6f">Hope this was helpful. Feedback of any kind is always appreciated.</p><p id="1ae1">Twitter: <a href="https://twitter.com/KrolsBjorn" target="_blank">https://twitter.com/KrolsBjorn</a></p>
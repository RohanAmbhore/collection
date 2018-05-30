<a href="https://medium.com/@thejasonfile/using-dotenv-package-to-create-environment-variables-33da4ac4ea8f">https://medium.com/@thejasonfile/using-dotenv-package-to-create-environment-variables-33da4ac4ea8f</a><div id="articleHeader"><h1>Using dotenv package to create environment variables</h1></div><figure id="ee7f"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/66/1*2P4-bzXEpF6JwTprV2oCwA.jpeg?q=20" /><div class="readableLargeImageContainer"><img src="https://cdn-images-1.medium.com/max/1760/1*2P4-bzXEpF6JwTprV2oCwA.jpeg" /></div><figcaption><a href="https://stocksnap.io/photo/BLM201LYCH" target="_blank">https://stocksnap.io/photo/BLM201LYCH</a></figcaption></figure><p id="92a9">Applications that rely on third-party sources for data will at some point need to include things like OAuth tokens, SSH keys, or API credentials. This becomes an issue when the code for the application gets pushed up to a public facing source control like GitHub. Once the code is up there it is accessible to anyone that sees it. And so are your keys.</p><p id="8071">GitHub <a href="https://github.com/blog/1390-secrets-in-the-code" target="_blank">knows this is a problem</a> and includes steps in their <a href="https://help.github.com/articles/removing-sensitive-data-from-a-repository/" target="_blank">documentation</a> to get around it.</p><p id="5326">How do you get around this?</p><p id="3c04">There are <a href="https://github.com/dxa4481/truffleHog" target="_blank">tools being developed</a> that search through repositories and find strings that could be sensitive information. This is a great idea but you would be relying on the code to find the strings.</p><p id="fda2">You could add all of the files with sensitive information to your .gitignore file? You could, but then this would prevent all needed files from getting into source control. And anyone wanting to help write the code wouldn’t have a complete version.</p><p id="f3d6">You could fill in the files with dummy data and push them up. But then anytime you wanted to work on the real code you’d have to remember to swap out the dummy data with real data. Then remember to swap it back in when you push the code up. Kind of defeats the purpose of source control and quickly becomes a headache.</p><p id="4d0f">One solution for this is to use environment variables. These are local variables that are made available to an application. Creating these variables is made easy with a tool like <a href="https://www.npmjs.com/package/dotenv" target="_blank">dotenv</a>. This module loads environment variables from a .env file that you create and adds them to the process.env object that is made available to the application.</p><h4 id="9173">Using dotenv</h4><p id="69e4">It’s pretty simple to use. First, install the package.</p><pre id="4960">npm install dotenv --save</pre><p id="12b1">Next add the following line to your app.</p><pre id="bf2f">require('dotenv').config()</pre><p id="d370">Then create a <code>.env</code> file at the root directory of your application and add the variables to it.</p><pre id="e227">//contents of .env</pre><pre id="cb06">SECRET_KEY=abcd1234</pre><p id="d08d">Finally, add ‘.env’ to your ‘.gitignore’ file so that Git ignores it and it never ends up on GitHub. You can add any keys you want to this file.</p><p id="24f9">That’s it. Four simple steps.</p><p id="74ee">Now, from within the app, any variables you’ve added to the file will be available. For example, if I add the above name/value to the .env file and console out the contents of process.env I should see this at the end of the object:</p><figure id="b7cc"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/66/1*PhmXOVYutds61LML-hKLzQ.png?q=20" /><div class="readableLargeImageContainer"><img /></div></figure><p id="8d46">To take this a step further, I can display this information in a browser to confirm the app can read it.</p><p id="4a27">After creating a basic express server I can send the key to the ‘/’ route so that it gets rendered to the page.</p><pre id="bc37">const express = require('express');<br />const app = express();<br />const port = process.env.PORT || 3000;</pre><pre id="e1dd">require('dotenv').config();</pre><pre id="47da">app.get('/', (req, res) =&gt; {<br />    res.send(process.env.SECRET_KEY);<br />})</pre><pre id="0e5e">app.listen(port, () =&gt; {<br />    console.log(`Server is running on port ${port}.`)<br />})</pre><p id="b877">This code will look like this:</p><figure id="86c4"><div><div><img src="https://cdn-images-1.medium.com/freeze/max/66/1*E_pMxvE78su7HLKvh3eEFw.png?q=20" /><div class="readableLargeImageContainer"><img /></div></figure><p id="fcf9">Dotenv is a simple way to allow you to create secret keys that your application needs to function and keep them from going public.</p><p id="5592">The code for this example can be found <a href="https://github.com/thejasonfile/dotenv_example" target="_blank">here</a>.</p>
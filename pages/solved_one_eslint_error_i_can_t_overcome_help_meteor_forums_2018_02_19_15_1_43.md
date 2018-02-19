<a href="https://forums.meteor.com/t/solved-one-eslint-error-i-cant-overcome/25715">https://forums.meteor.com/t/solved-one-eslint-error-i-cant-overcome/25715</a><div id="articleHeader"><h1>[Solved] One esLint error I can't overcome</h1></div><div><p>I’m trying to upgrade the Meteor Mantra Kickstarter to Meteor 1.3.4.1.</p>
<p>I have cleaned up all but one linting errors.</p>
<p>The problem is on line 13 of <a href="https://github.com/warehouseman/meteor-mantra-kickstarter/blob/v0.2.1/client/modules/_users/composers/users/single.jsx#L13" target="_blank">this file1</a>.</p>
<p>The error message is :</p>
<pre><code> 13:22  error  Parsing error: Unexpected token .. 
</code></pre>
<p>Column 22 is the <code>spread</code> operator  ( . . . ).</p>
<p>I have tried, unsuccessfully, to recreate the problem outside the app.  It seems to be illegal JavaScript, but it works in jsx.  Inspecting line 13 with browser developer tools, I see it has been redacted from . . .</p>
<pre><code>  onData(null, {...user.profile, role, user, email, error});
</code></pre>
<p>. . . to . . .</p>
<pre><code>  onData(null, (0, _extends3['default'])({}, user.profile, { role: role, user: user, email: email, error: error }));
</code></pre>
<p>I have searched the web for solutions and applied the following suggested settings to my  <a href="https://github.com/warehouseman/meteor-mantra-kickstarter/blob/v0.2.1/.eslintrc" target="_blank">.eslintrc</a> file :</p>
<pre><code>"env": {
  "es6": true,
"plugins": [
  "react"
],
"ecmaFeatures": {
   "objectLiteralShorthandMethods": true,
   "objectLiteralShorthandProperties": true,
   "restParams": true,
   "spread": true,
</code></pre>
<p>My <a href="https://github.com/warehouseman/meteor-mantra-kickstarter/blob/develop/package.json" target="_blank">package.json</a> has the following relevant settings (not yet committed) :</p>
<pre><code>"devDependencies": {
  "eslint": "^2.13.1",
  "eslint-plugin-react": "^5.5.2",
</code></pre>
<p>What else can I do ?</p></div>
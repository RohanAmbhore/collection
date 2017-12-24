<a href="https://tyil.nl/articles/funding-yourself-as-free-software-developer.html">https://tyil.nl/articles/funding-yourself-as-free-software-developer.html</a><div id="articleHeader"><h1>Funding Yourself As A Free Software Developer</h1></div>
<div>
<h3 id="bountysource">BountySource</h3>
<div>
<table>
<tbody><tr>
<td>

</td>
<td>
<div>
<ul>
<li>
<p>Requires 3rd-party <a href="/articles/on-cloudflare" target="_blank">Cloudflare</a>-hosted
JavaScript sources to function.</p>
</li>
</ul>
</div>
</td>
</tr>
</tbody></table>
</div>
<div>
<p>BountySource lets people donate money towards an issue on Github your projects.
Once an issue gets fixed, you can claim the "bounty" that was on this issue.
This can also help in making clear which issue you should aim for next, and
can increase interest in contributors for your project.</p>
</div>
<div>
<p>There’s also BountySource Salt, which is a recurring donation platform.
Projects or teams can use this to gain monthly income to sustain the
development of their project(s).</p>
</div>
<div>
<p>Support for this platform is offered through the IRC channel
<a href="https://kiwiirc.com/client/chat.freenode.net:+6697/#bountysource" target="_blank"><code>#bountysource</code>
on Freenode</a>.</p>
</div>
<div>
<p>The BountySource platform itself is also free software, and the source code
for it can be found <a href="https://github.com/bountysource/core" target="_blank">on github</a>.</p>
</div>
<div>
<p>You can find BountySource at <a href="https://www.bountysource.com/" target="_blank">https://www.bountysource.com/</a>.</p>
</div>
</div>
<div>
<h3 id="liberapay">LiberaPay</h3>
<div>
<p>This service seems to be completely free as in freedom. They even
<a href="https://github.com/liberapay/liberapay.com" target="_blank">publish their source on GitHub</a>.
Their own funding comes through donations on their own platform, instead of
taking a cut of each donation like most other services.</p>
</div>
<div>
<p>It’s possible to connect other accounts to your LiberaPay account. While this
feature in general is pretty common, they allow you to link to sites which are
interesting to show as developer, such as GitHub, GitLab, and BitBucket. They
also let you link to a Mastodon account, if you have one.</p>
</div>
<div>
<p>To let people know you’re accepting donations through LiberaPay, you can use
one of the widgets they make available for you. This will show a donate button
which will link to you profile. Do note, this is not a regular HTML button or
cleverly implemented anchor tag, but a JavaScript-based button.</p>
</div>
<div>
<p>Another thing LiberaPay lacks is a rewards system. Most other platforms allow
you to set reward tiers, which allow you to give certain benefits to donors.</p>
</div>
<div>
<p>You can find Liberapay at <a href="https://liberapay.com/" target="_blank">https://liberapay.com/</a>.</p>
</div>
</div>
<div>
<h3 id="makersupport">MakerSupport</h3>
<div>
<table>
<tbody><tr>
<td>

</td>
<td>
<div>
<ul>
<li>
<p>The site requires a 3rd-party hosted jQuery.</p>
</li>
<li>
<p>You have to solve a Google reCaptcha in order to register a new account.</p>
</li>
</ul>
</div>
</td>
</tr>
</tbody></table>
</div>
<div>
<p>MakerSupport seems to be another option, aimed at content creators who might
need freedom of speech more than others. It seems to be less focused on
software development, as you cannot link to any of the major git hosting
platforms.</p>
</div>
<div>
<p>There are options here to set up "tiers" for your donors; which is a convenient
way to provide them with perks for their support. For a free software
developer, this might be something like access to more direct support from the
developer.</p>
</div>
<div>
<p>Sadly, registration wasn’t as smooth as most other platforms. My preferred
username, "tyil" is too short. There’s no indication of the requirements of any
of the fields, you just get a popup on submission of the form saying a field is
wrong.</p>
</div>
<div>
<p>Additionally, the registration form requires some 3rd-party JavaScript to work,
and a Google reCaptcha to be solved in order to get the submit button to show
up. As I have set up uMatrix in my browser, this cost me some extra time to
finish registration.</p>
</div>
<div>
<p>Setting a profile image proved to be a little harder. First off, I’m still
using uMatrix so I had to allow a 3rd-party (Amazon, in this case) XHR
requests. Secondly, their error when uploading a "wrong" format is also not
very user friendly, as it won’t give you any details on why it’s disallowed,
nor what images are allowed instead.</p>
</div>
<div>
<table>
<tbody><tr>
<td>

</td>
<td>
<div>
<p>It seems they check the extension of the uploaded image’s filename. As far as I
can tell, you’re allowed to upload files that end with <code>.jpg</code> and <code>.png</code>.</p>
</div>
</td>
</tr>
</tbody></table>
</div>
<div>
<p>You can find MakerSupport at <a href="https://www.makersupport.com/" target="_blank">https://www.makersupport.com/</a>.</p>
</div>
</div>
<div>
<h3 id="patreon">Patreon</h3>
<div>
<table>
<tbody><tr>
<td>

</td>
<td>
<div>
<ul>
<li>
<p>Requires 3rd-party <a href="/articles/on-cloudflare" target="_blank">Cloudflare</a>-hosted
JavaScript sources to function.</p>
</li>
<li>
<p>You have to solve a Google reCaptcha in order to register a new account.</p>
</li>
</ul>
</div>
</td>
</tr>
</tbody></table>
</div>
<div>
<p>Patreon is possibly the most famous donation-based funding platform available
right now. Its popularity is a good thing, since this means there’s probably
many donors already using this platform.</p>
</div>
<div>
<p>At Patreon, you can set up so-called goals. Goals are the thing I haven’t found
with other funding platforms. It allows you to set a goal for an amount of
money, and add a reward to this. This way, you can inform your donors you will
be creating a certain kind of content once a one-time goal has been reached.
Basically, you can show your donors what you’re going to do with the money
they’re donating to you.</p>
</div>
<div>
<p>Another interesting thing that I haven’t seen on other platforms is the option
to charge donors per creation, instead of per month. While this may seem less
fitting for software developers (unless you want to get paid per commit, I
guess), it’s an interesting feature that’s pretty unique. If you publish many
tutorials, guides or other posts, this might fit you very well.</p>
</div>
<div>
<p>You can link your account to other services, similarly to other platforms, but
it seems to only allow you to be linked with proprietary social media
platforms.</p>
</div>
<div>
<p>You can find Patreon at <a href="https://www.patreon.com/home" target="_blank">https://www.patreon.com/home</a>.</p>
</div>
</div>
<div>
<h3 id="dis-honorable-mentions">(Dis)honorable mentions</h3>
<div>
<h4 id="hatreon">Hatreon</h4>
<div>
<p>I’ve included this because I found people talking about it on IRC. However, it
seems to be nothing more than a joke that’s gone too far. Its main reason for
existing seems to be to get away from the political correctness found with
earlier crowdfunding platforms, yet their site is invite-only, so those who are
actually interested can’t even use it. It seems that pledging is currently
disabled as well, and has been for at least 10 days.</p>
</div>
</div>
</div>

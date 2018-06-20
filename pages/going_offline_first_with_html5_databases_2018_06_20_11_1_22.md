<a href="http://nolanlawson.github.io/offline-first-presentation/">http://nolanlawson.github.io/offline-first-presentation/</a><div id="articleHeader"><h1>Going Offline-First with HTML5 Databases</h1></div>

    <h2><a href="https://twitter.com/nolanlawson" target="_blank">@nolanlawson</a></h2>
  </td>
  <td><div class="readableLargeImageContainer"><img src="1.png" /></div></td>
</tr>
<tr>
  <td><p>Hi, I'm <a href="http://nolanlawson.com" target="_blank">Nolan Lawson</a>. I work at <a href="http://www.squarespace.com/" target="_blank">Squarespace</a>, and in
    my spare time I help maintain <a href="http://pouchdb.com" target="_blank">PouchDB</a>,
    which is a JavaScript database that runs in the browser.</p></td>
  <td><div class="readableLargeImageContainer"><img src="2.png" /></div></td>
</tr>
<tr>
  <td><p> So first off, let me tell you a little story, about offline experiences.</p></td>
  <td><div class="readableLargeImageContainer"><img src="3.png" /></div></td>
</tr>
<tr>
  <td><p> I moved to New York about a month ago, and I take the subway to work every day. And one
    of
    the things that surprised me about the subway is that, as soon as you go underground, your
    phone
    loses its lifeline to the Internet. Your bars go down to zero; you're offline.</p>

    <p> That's not to say your phone becomes a brick. Lots of apps still work fine offline.</p>
  </td>
  <td><div class="readableLargeImageContainer"><img src="4.png" /></div></td>
</tr>
<tr>
  <td><p> For instance, the Twitter app. This is great; I can still read my feed, because it was
    synced in the background. I can't see all the images, because not all of them were cached, but
    it's still usable.</p></td>
  <td><div class="readableLargeImageContainer"><img src="5.png" /></div></td>
</tr>
<tr>
  <td><p> How about Amazon Kindle? Great offline experience. I can download my books before I hop
    on
    the subway, and it automatically syncs my last read page once I'm back online. I use this a
    lot
    during my commute.</p></td>
  <td><div class="readableLargeImageContainer"><img src="6.png" /></div></td>
</tr>
<tr>
  <td><p> How about email? We tend to take it for granted, but email was designed from the
    bottom-up
    to work well offline. I can read all my emails, respond to them, and they just go in the
    outbox,
    getting sent out as soon I'm back online. I can even have a conversation, thanks to the little
    windows of connectivity I get during between stops.</p></td>
  <td><div class="readableLargeImageContainer"><img src="7.png" /></div></td>
</tr>
<tr>
  <td><p> Other apps? Well, they don't work so great offline. Either they throw up an error
    message,
    or they don't give any indication that something's happening. This sucks. I don't use these
    apps
    much on the subway.</p></td>
  <td><div class="readableLargeImageContainer"><img src="8.png" /></div></td>
</tr>
<tr>
  <td><p> There's also one app I definitely don't use on the subway, because it's guaranteed to
    never
    work. As web developers, this is a big problem for us. Most of the apps we write are trapped
    behind that little icon.</p>

    <p> So what can we do about this? I've talked a lot about mobile apps, but we can solve this
      problem in our webapps as well. There's this phrase that's been going around in the web
      development community that I like a lot: "offline first."</p></td>
  <td><div class="readableLargeImageContainer"><img src="9.png" /></div></td>
</tr>
<tr>
  <td><p> I think it was coined by Jan Lenhardt, and basically the idea is that you stop thinking
    of
    "offline" as being this horrible edge case where your app has to self-destruct, and instead
    just
    treat it as a fact of life.
  </p></td>
  <td><div class="readableLargeImageContainer"><img src="10.png" /></div></td>
</tr>
<tr>
  <td><p>In practice, this usually means querying the local database and then
    only syncing back to the remote server when you have a connection. There's a lot of wisdom in
    this
    approach.</p>

    <p> And in a sense, "offline first" is the new "mobile first," because it's really hard to
      shoehorn in after you've already got a completed app. You have to be cognizant of it from
      the
      beginning.</p>

    <p> So why should we care about "offline first"? Who cares about offline users?</p></td>
  <td><div class="readableLargeImageContainer"><img src="11.png" /></div></td>
</tr>
<tr>
  <td><p> Well, here's the thing. As developers living in New York City, and testing our webapps
    on
    our super-fast MacBook Pros, using our super-fast Ethernet connections that we probably have
    at
    work and at home, I think we live in a bubble. And that makes us blind to the problems that a
    lot
    of our user base experiences on a day-to-day basis.
  </p>

    <p>And it's tempting to think that this is only a
      temporary problem of the early 21st century, and that eventually everyone will have
      omnipresent
      gigabit Internet, so "offline" will go away. But that's just not true. How about:</p></td>
  <td><div class="readableLargeImageContainer"><img src="12.png" /></div></td>
</tr>
<tr>
  <td><p>People traveling, who don't want to pay exorbitant roaming fees?</p></td>
  <td><div class="readableLargeImageContainer"><img src="13.png" /></div></td>
</tr>
<tr>
  <td><p>People using spotty hotel wi-fi? spotty conference wi-fi?</p></td>
  <td><div class="readableLargeImageContainer"><img src="14.png" /></div></td>
</tr>
<tr>
  <td><p>People who don't live in the US? You know, in Australia they have a whole mirror of npm,
    because it's just so painful to sync from California and back. In the US, we're so used to all
    of
    our cloud services being hosted here, that we have no idea what people in Europe or New
    Zealand
    are experiencing.</p></td>
  <td><div class="readableLargeImageContainer"><img src="15.png" /></div></td>
</tr>
<tr>
  <td><p> There are more people who benefit from "offline first." How about people going
    camping?</p>
  </td>
  <td><div class="readableLargeImageContainer"><img src="16.png" /></div></td>
</tr>
<tr>
  <td><p>People on the subway?</p></td>
  <td><div class="readableLargeImageContainer"><img src="17.png" /></div></td>
</tr>
<tr>
  <td><p>
    People driving on the highway in Montana?</p></td>
  <td><div class="readableLargeImageContainer"><img src="18.png" /></div></td>
</tr>
<tr>
  <td><p>
    People living in the developing world? Their only source of Internet may be a cheap Android
    phone with a 2G connection. When are <em>they</em> going to get their gigabit Internet?</p>
  </td>
  <td><div class="readableLargeImageContainer"><img src="19.png" /></div></td>
</tr>
<tr>
  <td><p> Or how about this: people living in any universe where the speed of light is not equal
    to
    infinity? The important thing to remember is, it's always going to be faster to round-trip
    from
    your screen to your hard drive and back, than it is to round-trip from California and
    back.</p>
  </td>
  <td><div class="readableLargeImageContainer"><img src="20.png" /></div></td>
</tr>
<tr>
  <td>

    <p> When you do "offline first," you give your users a better experience, even when they're
      online. Buttery-smooth UIs that are eerily fast, because they don't have to go to the
      network at
      all. Your users will be shocked, because with desktop webapps, most of us aren't used to UIs
      that
      respond that quickly.</p>

    <p> If you want to see an example of this, I invite you all to go to <a href="http://php.net" target="_blank">php.net</a>
      and see how
      their
      autosuggestion bar works. It's all localStorage, and it's super fast. I love this, because it
      really shows how shockingly fast the local data store can be.</p></td>
  <td><div class="readableLargeImageContainer"><img src="21.png" /></div></td>
</tr>
<tr>
  <td><p> So what can we do, as web developers? Well luckily for us, HTML5 has come along and
    given us
    some solutions. Unfortunately, it's HTML5, so it's given us 3 solutions. But that's okay,
    because
    we're programmers - we can make this work.</p>
  </td>
  <td><div class="readableLargeImageContainer"><img src="22.png" /></div></td>
</tr>
<tr>
  <td><p> First there's localStorage, also known as Web Storage. This one's been around for
    awhile,
    and it's pretty simple and widely-supported, so you've probably all used it. Basically it's a
    key-value store, but it's got some problems: you can only store up to 1 megabyte on some
    browsers,
    you can only store strings, it's a dumb key-value store (i.e no iteration), and it's
    synchronous,
    so it can block the DOM. It's still good in a pinch for small bits of application state, but
    we
    haven't got a real database yet.</p></td>
  <td><div class="readableLargeImageContainer"><img src="23.png" /></div></td>
</tr>
<tr>
  <td><p> So around 2009, Google and Apple tried to solve this problem by giving us the Web SQL
    database, which is basically SQLite with some web APIs thrown on top. If you're not familiar
    with
    SQLite, it's essentially the de-facto standard for iOS, Android, and now Windows Phone
    development.</p></td>
  <td><div class="readableLargeImageContainer"><img src="24.png" /></div></td>
</tr>

<tr>
  <td>

    <p>However, Firefox and IE refused to implement it because it didn't fit the
      "independent implementations" criterion, since the spec basically just described SQLite
      as-is.</p>

  </td>
  <td><div class="readableLargeImageContainer"><img src="25.png" /></div></td>
</tr>
<tr>
  <td>
    <p>So
      the spec is now dead.</p>
  </td>
  <td><div class="readableLargeImageContainer"><img src="26.png" /></div></td>
</tr>

<tr>
  <td><p> So nowadays we have IndexedDB, which can be thought of as the NoSQL answer to Web SQL.
    And
    it was supposed to be the compromise that all the browser vendors could agree upon, but...
  </p>
  </td>
  <td><div class="readableLargeImageContainer"><img src="27.png" /></div></td>
</tr>

<tr>
  <td>
    <p>We're
      not quite there yet.</p></td>
  <td><div class="readableLargeImageContainer"><img src="28.png" /></div></td>
</tr>

<tr>

  <td><p>It's only supported in Android 4.4+, which if you don't know Android, is
    about 15% of all devices, so it's nothing. On iOS and Safari it won't be available until 8, so
    we'll see about that.</p></td>
  <td><div class="readableLargeImageContainer"><img src="29.png" /></div></td>
</tr>

<tr>
  <td><p> Luckily, there are a lot of libraries out there that can abstract away the underlying
    browser database and give you a single API over all of them. I've already mentioned PouchDB,
    but
    there's also localForage, ydn-db, Lawnchair, and lots of others.</p></td>
  <td><div class="readableLargeImageContainer"><img src="30.png" /></div></td>
</tr>
<tr>
  <td><p> And you should definitely use them, because even in the imaginary happy future where
    every
    browser has IndexedDB, the API still looks like <a href="http://www.html5rocks.com/en/tutorials/indexeddb/todo/" target="_blank">this</a>. Yeah, if this
    doesn't give you
    flashbacks to
    <code>xhr.onreadystatechange = function() {}</code>, then you haven't been doing web dev for
    very
    long.</p>
  </td>
  <td><div class="readableLargeImageContainer"><img src="31.png" /></div></td>
</tr>
<tr>
  <td><p>Yeah.</p>

    <p> And there are also lots of browser bugs that make IndexedDB work slightly differently on
      different browsers. I could probably rattle off a dozen ways IndexedDB differs between IE,
      Firefox, and Chrome, and no doubt soon Safari, but I don't need to bore you.</p></td>
  <td><div class="readableLargeImageContainer"><img src="32.png" /></div></td>
</tr>
<tr>
  <td><p> Essentially, I think the situation with browser databases in 2014 looks a lot like the
    situation with the DOM before jQuery came along. There are lots of browser-specific quirks and
    bugs, and even if you somehow navigate that minefield, the core API is just horrid to work
    with.
    So you're better off using PouchDB or localForage, or one of the other ones, in the same way
    you're still better off using jQuery or Zepto or some similar library to work with the
    DOM.</p>
  </td>
  <td><div class="readableLargeImageContainer"><img src="33.png" /></div></td>
</tr>
<tr>
  <td><p> OK, so let's do a demo to show you what kinds of cool offline-first experiences you can
    build using HTML5 databases. This is one I built using PouchDB and AngularJS over a couple
    months,
    and I invite you all to follow along on your phones or laptops: just go to <a href="http://npm-browser.com" target="_blank">npm-browser.com</a>.</p>

    <p> I don't know if you know this, but npm stores data in CouchDB, and since PouchDB can
      sync
      with CouchDB, that means you can sync all of npm to your browser. In this app, we're only
      syncing
      the metadata, but it's still pretty sweet. You can go offline, and still search locally for
      packages you've already synced.</p>

    <p> And after you've replicated all of npm, which takes a couple minutes, it actually
      switches
      to local mode, meaning all your searches become super fast, because it doesn't need to query
      the
      remote database anymore.</p>

    <p> Plus, since CouchDB has this concept of "continuous" replication, we can just listen to
      the
      changes feed, and as new packages are published or updated, our app gets updated in real time.
      Neat, huh?</p>
  </td>
  <td><div class="readableLargeImageContainer"><img src="34.png" /></div></td>
</tr>
<tr>
  <td>

    <p> So that's offline first. If you don't assume that your users have an omnipresent
      connection
      to the Internet, you can build better apps that work great whether they're offline or online.
      Thank you.
    </p>
  </td>
  <td><div class="readableLargeImageContainer"><img src="34.png" /></div></td>
</tr>
</tbody></table>


<div><h3>Like On Github</h3><div><div>*Title (label for the link)</div><div><div>*Comment (commit message)</div><div id="action-btns"><div id="logh_btn_save">Saving...</div><div id="logh_btn_favorite">Favorite</div><div id="logh_btn_cancel">Cancel</div>
<a href="https://www.w3.org/International/questions/qa-what-is-encoding">https://www.w3.org/International/questions/qa-what-is-encoding</a><div id="articleHeader"><h1>Character encodings for beginners</h1></div>
	<h2 id="answer"><a href="#answer" target="_blank">Answer</a></h2>
  <section>
    <h3 id="why"><a href="#why" target="_blank"> First, why should I care?</a></h3>
    <p>If you use anything other than the most basic  English text, people may not be able to read the content you create
      unless you say what character encoding you used. </p>
    <p>For example, you may intend the text to look like this: </p>
    <p><img src="qa-what-is-encoding-data/mojibake1.gif" width="540" height="46" alt="mojibake1.gif" /> </p>
    <p>but it may actually display like this: </p>
    <p><img src="qa-what-is-encoding-data/mojibake2.gif" width="541" height="52" alt="mojibake2.gif" /> </p>
    <p>Not only does lack of character encoding information spoil the readability of displayed text, but it may mean that your data cannot be found
      by a search engine, or reliably processed by machines in a number of other ways. </p>
  </section>
  
  <section>
    <h3 id="what"><a href="#what" target="_blank"> So what's a character encoding?</a></h3>
    <div>
      <p>Words and sentences in text are created from <dfn>characters</dfn>. Examples of characters include the Latin letter <a href="qa-what-is-encoding-data/225.png" target="_blank">á</a> or the Chinese ideograph <a href="qa-what-is-encoding-data/35531.png" target="_blank">請</a> or the Devanagari character <a href="qa-what-is-encoding-data/2361.png" target="_blank">ह</a>. </p>
      <aside>
      <p>You may not be able to see some of the characters in this page because you don't have the necessary fonts. If you click on the place where you expected to see a character you will link to a graphic version. This page is encoded in UTF-8.</p>
      </aside>
    </div>
    <p>Characters that are needed for a specific purpose are grouped into a <dfn>character set</dfn> (also called a <dfn>repertoire</dfn>). (To refer to characters in an unambiguous way, each character is associated with a number, called a <dfn>code point</dfn>.)</p>
    <p>The characters are stored in the computer as one or more <dfn>bytes</dfn>. </p>
    <div>
    <p>Basically, you can visualise this by assuming that all characters are stored in computers using a special code, like the ciphers used in espionage. A <dfn>character encoding</dfn> provides a key to unlock (ie. crack) the code. It is a set of mappings between the bytes  in the computer and the  characters in the  character set. Without the key, the data looks like garbage.</p>
          <aside>
      <p>The misleading term <dfn>charset</dfn> is often used to refer to what are in reality character encodings. You should
      be aware of this usage, but stick to using the term character encodings whenever you can.</p>
      </aside>
</div>

    <p>So, when you input text using a keyboard or in some other way, the character encoding  maps characters you choose to specific bytes in computer memory, and then to display the text it reads the bytes back into characters.    </p>
    <p>Unfortunately, there are many different character sets and character encodings, ie. many different ways of mapping between bytes,
      code points and characters. The section <a href="#additionaldetails" target="_blank">Additional information</a> provides a little more detail for those who are interested.</p>
    <p>Most of the time, however, you will not need to know the details. You will just need to be sure that you consider the advice in the
      section <a href="#how" target="_blank">How does this affect me?</a> below.</p>
  </section>
  
  <section>
    <h3 id="fonts"><a href="#fonts" target="_blank">How do fonts fit into this?</a></h3>
    <p>A <dfn>font</dfn> is a collection of glyph definitions, ie. definitions of the shapes used to display characters. </p>
    <p>Once your browser or app has worked out what characters it is dealing with, it will then look in the font for glyphs it can use to display
      or print those characters. (Of course, if the encoding information was wrong, it will be looking up glyphs for the wrong characters.) </p>
    <p>A given font will usually cover a single character set, or in the case of a large character set like Unicode, just a subset of all the
      characters in the set. If your font doesn't have a glyph for a particular character, some browsers or software applications will look for the missing glyphs in other
      fonts on your system (which will mean that the glyph will look different from the surrounding text, like a ransom note). Otherwise you will typically
      see a square box, a question mark or some other character instead. For example: </p>
    <p><img src="qa-what-is-encoding-data/mojibake3.gif" width="526" height="53" alt="mojibake3.gif" /> </p>
  </section>
  
  <section>
    <h3 id="how"><a href="#how" target="_blank"> How does this affect me?</a></h3>
    <p>As a content author or developer, you should nowadays always <a href="/International/questions/qa-choosing-encodings" title="1" target="_blank">choose the UTF-8
      character encoding</a> for your content or data. This <a href="/International/articles/definitions-characters/#unicode" title="2" target="_blank">Unicode</a> encoding is a good choice because you can use a single character encoding to handle  any character you are likely to need. This greatly simplifies things. Using Unicode
      throughout your system also removes the need to track and convert between various character encodings. </p>
    <p>Content authors  need to find out how to <a href="/International/questions/qa-html-encoding-declarations" title="3" target="_blank">declare the character
      encoding</a> used for the document format they are working with.</p>
    <p>Note that just
    declaring a different encoding in your page won't change the bytes; you need to <strong>save</strong> the text in that encoding too. </p>
    <p>As a content author, you need to check what encoding your editor or scripts are saving text in, and how to save text in UTF-8. (It's usually the default these days.) You may also need to <a href="/International/questions/qa-headers-charset" title="4" target="_blank">check that your server is serving documents with the right HTTP
      declarations</a>. </p>
    <p>Developers need to ensure that the various parts of the system can communicate with each other, understand which character encodings
      are being used, and support all the necessary encodings and characters. (Ideally, you would use UTF-8 throughout, and be spared this trouble.)</p>
    <p>The links below provide some further reading on these topics. </p>
  </section>

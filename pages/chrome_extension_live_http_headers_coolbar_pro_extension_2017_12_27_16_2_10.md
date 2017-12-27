<a href="https://gist.github.com/mala/e87973df5029d96c9269d9431fcef5cb">https://gist.github.com/mala/e87973df5029d96c9269d9431fcef5cb</a><div id="articleHeader"><h1>Chrome ExtensionのLive HTTP Headersの調査(CoolBar.Pro導入 Extensionが何を行うかの調査)</h1></div>
    <div>
  <div>
    Chrome ExtensionのLive HTTP Headersの調査(CoolBar.Pro導入 Extensionが何を行うかの調査)
  </div>
</div>


        
  
      
    
  
    <p>Chrome ExtensionのLive HTTP Headersを調査した。Firefox用のものではない。Firefox用のものではない。</p>
<ul>
<li><a href="https://chrome.google.com/webstore/detail/live-http-headers/iaiioopjkcekapmldfgbebdclcnpgnlo" target="_blank">https://chrome.google.com/webstore/detail/live-http-headers/iaiioopjkcekapmldfgbebdclcnpgnlo</a></li>
</ul>
<p>11/7追記</p>
<ul>
<li>類似 or 同様の方法で難読化scriptを埋め込んでいる拡張機能が大量にあったため、Googleに報告済み。</li>
<li><a href="https://twitter.com/bulkneets/status/795260268221636608" target="_blank">https://twitter.com/bulkneets/status/795260268221636608</a></li>
</ul>
<p>English version: <a href="https://translate.google.com/translate?sl=ja&tl=en&js=y&prev=_t&hl=ja&ie=UTF-8&u=https%3A%2F%2Fgist.github.com%2Fmala%2Fe87973df5029d96c9269d9431fcef5cb&edit-text=&act=url" target="_blank">https://translate.google.com/translate?sl=ja&tl=en&js=y&prev=_t&hl=ja&ie=UTF-8&u=https%3A%2F%2Fgist.github.com%2Fmala%2Fe87973df5029d96c9269d9431fcef5cb&edit-text=&act=url</a></p>
<p>Summary in english.</p>
<ul>
<li>
<p>I've investigated TOP5000 installed extension from <a href="https://crx.dam.io" target="_blank">https://crx.dam.io</a></p>
</li>
<li>
<p>36 extensions contains same obfuscated script.</p>
</li>
<li>
<p>21 extensions already removed from webstore (2016-11-06)</p>
</li>
<li>
<p>Recently updated ones are not included(eg: http headers, live http headers) so there is more malicious extension.</p>
</li>
<li>
<p>I have not made my own crawler for webstore yet, so I have not investigated completely.</p>
</li>
<li>
<p>Many these extensions has common features, css changer for popular websites, copy and paste code, landing page.</p>
</li>
<li>
<p>There are stories that popular extensions are acquired by high prices, but many simple extensions was created by malware / adware dealers, I think.</p>
</li>
<li>
<p>I have not investigated "adware" function, I say "malicious" because it remove CSP header without explanation.</p>
</li>
<li>
<p>Some extensions that have webRequestBlocking permission remove CSP header</p>
</li>
</ul>
<p><a href="https://gist.github.com/mala/e87973df5029d96c9269d9431fcef5cb#file-blob-js-L24" target="_blank">https://gist.github.com/mala/e87973df5029d96c9269d9431fcef5cb#file-blob-js-L24</a></p>
<pre><code>                "object" == typeof a.responseHeaders[b] && "content-security-policy" === a.responseHeaders[b].name.toLowerCase() && a.responseHeaders.splice(b, 1);
</code></pre>
<hr />
<h2>background.min</h2>
<ul>
<li>画像からjsを切り出してblobを作って読み込む処理がある、addScriptはbackground.htmlに対して行われる(拡張機能context)</li>
<li>拡張機能用のlocalStorageのTが未定義だったら、4568904ミリ秒後に現在時刻がセットされる。</li>
<li>現在時刻がセットされていたら、画像からscriptの読み込みを行う。</li>
</ul>
<h2>画像内のscript</h2>
<ul>
<li>
<p>localStorageのIDが未定義だったら、3600000ミリ秒後に現在時刻をセットする。</p>
</li>
<li>
<p>さらに、IDの値と現在時刻の差分が 86400000 ミリ秒以上だったら、web requestに対してイベントハンドラを設定する。</p>
</li>
<li>
<p>動的に外部scriptを読み込んでいるのは、background pageではなくて、表示しているwebページに対して行っている。</p>
</li>
<li>
<p>その際に、CSPヘッダがあれば無効にするということをやっている。</p>
</li>
</ul>
<hr />
<h2>何が起きるか(事実)</h2>
<ul>
<li>拡張機能をインストールしてから、約1日以上経過しているなら、webサイトに対するscript injectionが有効化されている</li>
<li>有効化されるとwebサイト側に設定してあるCSPが無効化されてしまう。</li>
<li>有効化されているかどうかは、CSPが有効なサイトでCSP違反する操作を行えば分かる。例えばgithubでdeveloper consoleを表示して <code>document.write("&lt;script&gt;alert(1)&lt;/script&gt;")</code> など打ち込めば分かる(本来blockされる)</li>
<li>動的にロードされるscriptについてはまだ未調査。保全はしてある。</li>
</ul>
<h2>何が起こりうるか(可能性)</h2>
<ul>
<li>
<p>原理的には拡張機能の権限であれば、送受信するhttp headerも含めて取得できることになるが、動的にロードするscriptはwebページのcontextで実行されているため、そこまでは取れない</p>
</li>
<li>
<p>response headerを改変する部分は、拡張機能内に静的に書かれている。</p>
</li>
<li>
<p>取得できるのは、webページ上でのユーザーの操作、表示しているコンテンツ、httponlyがついていないcookie, etc</p>
</li>
<li>
<p>Chrome ExtensionのデフォルトのCSPは、拡張機能のcontextに対して外部scriptのロードを許可しない <a href="https://developer.chrome.com/extensions/contentSecurityPolicy" target="_blank">https://developer.chrome.com/extensions/contentSecurityPolicy</a></p>
</li>
<li>
<p>そのため、manifest.json で外部scriptを許可するようなCSPを定義していなければ、拡張機能のcontextではどういったscriptが実行されるのかは不変</p>
</li>
<li>
<p>webページに対するscript injectionの手法であれば、インストールした瞬間に全てのデータが抜かれる、といったことは起きない。</p>
</li>
<li>
<p>あくまで拡張機能が有効化されている間に訪問したサイトに対して影響がある。</p>
</li>
</ul>
<h2>提供元について</h2>
<ul>
<li>拡張機能内のプライバシーポリシーのhtmlと、AWSのscriptのURLから coolbar.pro というサービスを使っている。</li>
<li>サイトには拡張機能向けのマネタイズサービスと書かれている</li>
<li>拡張機能が買収されているのか、拡張機能の作者自身がマネタイズ目的で組み込んでいるのか、どちらか不明。</li>
<li>invite codeが無いと登録が出来ないので、どういったメニューがあるのかわからなかった。</li>
</ul>

<ul>
<li>
<p>一定時間経過後に有効化されるので外部scriptのロードなど、不審な動きを検知しにくくなっている</p>
</li>
<li>
<p>画像内に入れるのも、自動的なスキャンで引っかかりにくくなるだろう</p>
</li>
<li>
<p>検知しにくくするための方法がマルウェアが使う手法そのもの</p>
</li>
<li>
<p>webサイト側のCSPを無効化している時点で、少なくともwebサイトに対して害悪がある</p>
</li>
</ul>

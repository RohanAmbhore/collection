<a href="https://gist.github.com/BigstickCarpet/5d31c053d0b1d52389eb2723f7550907">https://gist.github.com/BigstickCarpet/5d31c053d0b1d52389eb2723f7550907</a><div id="articleHeader"><h1>GitHub Markdown Theme for Visual Studio Code</h1></div>
<p>This CSS stylesheet allows you to preview markdown files in VSCode using GitHub's mardown theme.  This CSS was taken directly from <a href="https://github.com/sindresorhus/github-markdown-css" target="_blank">the official GitHub Markdown repo</a>. I replaced their top-level <code>.markdown-body</code> class with the <code>body</code> tag so it would work in VSCode, and added styling for the <code>html</code> tag to match GitHub's fixed-width container.</p>
<h2>Instructions</h2>

</article>
  

  


        
  
      
    

  
      <table>
      <tbody><tr>
        <td id="file-github-markdown-css-L1"></td>
        <td id="file-github-markdown-css-LC1">@font-face {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L2"></td>
        <td id="file-github-markdown-css-LC2">  font-family: octicons-link;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L3"></td>
        <td id="file-github-markdown-css-LC3">  src: url(data:font/woff;charset=utf-8;base64,d09GRgABAAAAAAZwABAAAAAACFQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABEU0lHAAAGaAAAAAgAAAAIAAAAAUdTVUIAAAZcAAAACgAAAAoAAQAAT1MvMgAAAyQAAABJAAAAYFYEU3RjbWFwAAADcAAAAEUAAACAAJThvmN2dCAAAATkAAAABAAAAAQAAAAAZnBnbQAAA7gAAACyAAABCUM+8IhnYXNwAAAGTAAAABAAAAAQABoAI2dseWYAAAFsAAABPAAAAZwcEq9taGVhZAAAAsgAAAA0AAAANgh4a91oaGVhAAADCAAAABoAAAAkCA8DRGhtdHgAAAL8AAAADAAAAAwGAACfbG9jYQAAAsAAAAAIAAAACABiATBtYXhwAAACqAAAABgAAAAgAA8ASm5hbWUAAAToAAABQgAAAlXu73sOcG9zdAAABiwAAAAeAAAAME3QpOBwcmVwAAAEbAAAAHYAAAB/aFGpk3jaTY6xa8JAGMW/O62BDi0tJLYQincXEypYIiGJjSgHniQ6umTsUEyLm5BV6NDBP8Tpts6F0v+k/0an2i+itHDw3v2+9+DBKTzsJNnWJNTgHEy4BgG3EMI9DCEDOGEXzDADU5hBKMIgNPZqoD3SilVaXZCER3/I7AtxEJLtzzuZfI+VVkprxTlXShWKb3TBecG11rwoNlmmn1P2WYcJczl32etSpKnziC7lQyWe1smVPy/Lt7Kc+0vWY/gAgIIEqAN9we0pwKXreiMasxvabDQMM4riO+qxM2ogwDGOZTXxwxDiycQIcoYFBLj5K3EIaSctAq2kTYiw+ymhce7vwM9jSqO8JyVd5RH9gyTt2+J/yUmYlIR0s04n6+7Vm1ozezUeLEaUjhaDSuXHwVRgvLJn1tQ7xiuVv/ocTRF42mNgZGBgYGbwZOBiAAFGJBIMAAizAFoAAABiAGIAznjaY2BkYGAA4in8zwXi+W2+MjCzMIDApSwvXzC97Z4Ig8N/BxYGZgcgl52BCSQKAA3jCV8CAABfAAAAAAQAAEB42mNgZGBg4f3vACQZQABIMjKgAmYAKEgBXgAAeNpjYGY6wTiBgZWBg2kmUxoDA4MPhGZMYzBi1AHygVLYQUCaawqDA4PChxhmh/8ODDEsvAwHgMKMIDnGL0x7gJQCAwMAJd4MFwAAAHjaY2BgYGaA4DAGRgYQkAHyGMF8NgYrIM3JIAGVYYDT+AEjAwuDFpBmA9KMDEwMCh9i/v8H8sH0/4dQc1iAmAkALaUKLgAAAHjaTY9LDsIgEIbtgqHUPpDi3gPoBVyRTmTddOmqTXThEXqrob2gQ1FjwpDvfwCBdmdXC5AVKFu3e5MfNFJ29KTQT48Ob9/lqYwOGZxeUelN2U2R6+cArgtCJpauW7UQBqnFkUsjAY/kOU1cP+DAgvxwn1chZDwUbd6CFimGXwzwF6tPbFIcjEl+vvmM/byA48e6tWrKArm4ZJlCbdsrxksL1AwWn/yBSJKpYbq8AXaaTb8AAHja28jAwOC00ZrBeQNDQOWO//sdBBgYGRiYWYAEELEwMTE4uzo5Zzo5b2BxdnFOcALxNjA6b2ByTswC8jYwg0VlNuoCTWAMqNzMzsoK1rEhNqByEyerg5PMJlYuVueETKcd/89uBpnpvIEVomeHLoMsAAe1Id4AAAAAAAB42oWQT07CQBTGv0JBhagk7HQzKxca2sJCE1hDt4QF+9JOS0nbaaYDCQfwCJ7Au3AHj+LO13FMmm6cl7785vven0kBjHCBhfpYuNa5Ph1c0e2Xu3jEvWG7UdPDLZ4N92nOm+EBXuAbHmIMSRMs+4aUEd4Nd3CHD8NdvOLTsA2GL8M9PODbcL+hD7C1xoaHeLJSEao0FEW14ckxC+TU8TxvsY6X0eLPmRhry2WVioLpkrbp84LLQPGI7c6sOiUzpWIWS5GzlSgUzzLBSikOPFTOXqly7rqx0Z1Q5BAIoZBSFihQYQOOBEdkCOgXTOHA07HAGjGWiIjaPZNW13/+lm6S9FT7rLHFJ6fQbkATOG1j2OFMucKJJsxIVfQORl+9Jyda6Sl1dUYhSCm1dyClfoeDve4qMYdLEbfqHf3O/AdDumsjAAB42mNgYoAAZQYjBmyAGYQZmdhL8zLdDEydARfoAqIAAAABAAMABwAKABMAB///AA8AAQAAAAAAAAAAAAAAAAABAAAAAA==) format('woff');</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L6"></td>
        <td id="file-github-markdown-css-LC6">html {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L7"></td>
        <td id="file-github-markdown-css-LC7">  width: 880px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L8"></td>
        <td id="file-github-markdown-css-LC8">  padding: 45px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L9"></td>
        <td id="file-github-markdown-css-LC9">  margin-top: 25px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L10"></td>
        <td id="file-github-markdown-css-LC10">  margin-bottom: 125px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L11"></td>
        <td id="file-github-markdown-css-LC11">  border: 1px solid #ddd;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L12"></td>
        <td id="file-github-markdown-css-LC12">  border-radius: 3px;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L15"></td>
        <td id="file-github-markdown-css-LC15">body {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L16"></td>
        <td id="file-github-markdown-css-LC16">  -ms-text-size-adjust: 100%;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L17"></td>
        <td id="file-github-markdown-css-LC17">  -webkit-text-size-adjust: 100%;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L18"></td>
        <td id="file-github-markdown-css-LC18">  line-height: 1.5;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L19"></td>
        <td id="file-github-markdown-css-LC19">  color: #333;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L20"></td>
        <td id="file-github-markdown-css-LC20">  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L21"></td>
        <td id="file-github-markdown-css-LC21">  font-size: 16px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L22"></td>
        <td id="file-github-markdown-css-LC22">  line-height: 1.5;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L23"></td>
        <td id="file-github-markdown-css-LC23">  word-wrap: break-word;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L26"></td>
        <td id="file-github-markdown-css-LC26">body .pl-c {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L27"></td>
        <td id="file-github-markdown-css-LC27">  color: #969896;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L30"></td>
        <td id="file-github-markdown-css-LC30">body .pl-c1,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L31"></td>
        <td id="file-github-markdown-css-LC31">body .pl-s .pl-v {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L32"></td>
        <td id="file-github-markdown-css-LC32">  color: #0086b3;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L35"></td>
        <td id="file-github-markdown-css-LC35">body .pl-e,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L36"></td>
        <td id="file-github-markdown-css-LC36">body .pl-en {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L37"></td>
        <td id="file-github-markdown-css-LC37">  color: #795da3;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L40"></td>
        <td id="file-github-markdown-css-LC40">body .pl-smi,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L41"></td>
        <td id="file-github-markdown-css-LC41">body .pl-s .pl-s1 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L42"></td>
        <td id="file-github-markdown-css-LC42">  color: #333;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L45"></td>
        <td id="file-github-markdown-css-LC45">body .pl-ent {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L46"></td>
        <td id="file-github-markdown-css-LC46">  color: #63a35c;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L49"></td>
        <td id="file-github-markdown-css-LC49">body .pl-k {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L50"></td>
        <td id="file-github-markdown-css-LC50">  color: #a71d5d;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L53"></td>
        <td id="file-github-markdown-css-LC53">body .pl-s,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L54"></td>
        <td id="file-github-markdown-css-LC54">body .pl-pds,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L55"></td>
        <td id="file-github-markdown-css-LC55">body .pl-s .pl-pse .pl-s1,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L56"></td>
        <td id="file-github-markdown-css-LC56">body .pl-sr,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L57"></td>
        <td id="file-github-markdown-css-LC57">body .pl-sr .pl-cce,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L58"></td>
        <td id="file-github-markdown-css-LC58">body .pl-sr .pl-sre,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L59"></td>
        <td id="file-github-markdown-css-LC59">body .pl-sr .pl-sra {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L60"></td>
        <td id="file-github-markdown-css-LC60">  color: #183691;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L63"></td>
        <td id="file-github-markdown-css-LC63">body .pl-v {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L64"></td>
        <td id="file-github-markdown-css-LC64">  color: #ed6a43;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L67"></td>
        <td id="file-github-markdown-css-LC67">body .pl-id {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L68"></td>
        <td id="file-github-markdown-css-LC68">  color: #b52a1d;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L71"></td>
        <td id="file-github-markdown-css-LC71">body .pl-ii {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L72"></td>
        <td id="file-github-markdown-css-LC72">  color: #f8f8f8;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L73"></td>
        <td id="file-github-markdown-css-LC73">  background-color: #b52a1d;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L76"></td>
        <td id="file-github-markdown-css-LC76">body .pl-sr .pl-cce {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L77"></td>
        <td id="file-github-markdown-css-LC77">  font-weight: bold;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L78"></td>
        <td id="file-github-markdown-css-LC78">  color: #63a35c;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L81"></td>
        <td id="file-github-markdown-css-LC81">body .pl-ml {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L82"></td>
        <td id="file-github-markdown-css-LC82">  color: #693a17;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L85"></td>
        <td id="file-github-markdown-css-LC85">body .pl-mh,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L86"></td>
        <td id="file-github-markdown-css-LC86">body .pl-mh .pl-en,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L87"></td>
        <td id="file-github-markdown-css-LC87">body .pl-ms {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L88"></td>
        <td id="file-github-markdown-css-LC88">  font-weight: bold;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L89"></td>
        <td id="file-github-markdown-css-LC89">  color: #1d3e81;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L92"></td>
        <td id="file-github-markdown-css-LC92">body .pl-mq {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L93"></td>
        <td id="file-github-markdown-css-LC93">  color: #008080;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L96"></td>
        <td id="file-github-markdown-css-LC96">body .pl-mi {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L97"></td>
        <td id="file-github-markdown-css-LC97">  font-style: italic;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L98"></td>
        <td id="file-github-markdown-css-LC98">  color: #333;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L101"></td>
        <td id="file-github-markdown-css-LC101">body .pl-mb {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L102"></td>
        <td id="file-github-markdown-css-LC102">  font-weight: bold;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L103"></td>
        <td id="file-github-markdown-css-LC103">  color: #333;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L106"></td>
        <td id="file-github-markdown-css-LC106">body .pl-md {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L107"></td>
        <td id="file-github-markdown-css-LC107">  color: #bd2c00;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L108"></td>
        <td id="file-github-markdown-css-LC108">  background-color: #ffecec;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L111"></td>
        <td id="file-github-markdown-css-LC111">body .pl-mi1 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L112"></td>
        <td id="file-github-markdown-css-LC112">  color: #55a532;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L113"></td>
        <td id="file-github-markdown-css-LC113">  background-color: #eaffea;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L116"></td>
        <td id="file-github-markdown-css-LC116">body .pl-mdr {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L117"></td>
        <td id="file-github-markdown-css-LC117">  font-weight: bold;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L118"></td>
        <td id="file-github-markdown-css-LC118">  color: #795da3;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L121"></td>
        <td id="file-github-markdown-css-LC121">body .pl-mo {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L122"></td>
        <td id="file-github-markdown-css-LC122">  color: #1d3e81;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L125"></td>
        <td id="file-github-markdown-css-LC125">body .octicon {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L126"></td>
        <td id="file-github-markdown-css-LC126">  display: inline-block;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L127"></td>
        <td id="file-github-markdown-css-LC127">  vertical-align: text-top;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L128"></td>
        <td id="file-github-markdown-css-LC128">  fill: currentColor;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L131"></td>
        <td id="file-github-markdown-css-LC131">body a {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L132"></td>
        <td id="file-github-markdown-css-LC132">  background-color: transparent;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L133"></td>
        <td id="file-github-markdown-css-LC133">  -webkit-text-decoration-skip: objects;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L136"></td>
        <td id="file-github-markdown-css-LC136">body a:active,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L137"></td>
        <td id="file-github-markdown-css-LC137">body a:hover {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L138"></td>
        <td id="file-github-markdown-css-LC138">  outline-width: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L141"></td>
        <td id="file-github-markdown-css-LC141">body strong {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L142"></td>
        <td id="file-github-markdown-css-LC142">  font-weight: inherit;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L145"></td>
        <td id="file-github-markdown-css-LC145">body strong {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L146"></td>
        <td id="file-github-markdown-css-LC146">  font-weight: bolder;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L149"></td>
        <td id="file-github-markdown-css-LC149">body h1 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L150"></td>
        <td id="file-github-markdown-css-LC150">  font-size: 2em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L151"></td>
        <td id="file-github-markdown-css-LC151">  margin: 0.67em 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L154"></td>
        <td id="file-github-markdown-css-LC154">body img {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L155"></td>
        <td id="file-github-markdown-css-LC155">  border-style: none;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L158"></td>
        <td id="file-github-markdown-css-LC158">body svg:not(:root) {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L159"></td>
        <td id="file-github-markdown-css-LC159">  overflow: hidden;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L162"></td>
        <td id="file-github-markdown-css-LC162">body code,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L163"></td>
        <td id="file-github-markdown-css-LC163">body kbd,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L164"></td>
        <td id="file-github-markdown-css-LC164">body pre {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L165"></td>
        <td id="file-github-markdown-css-LC165">  font-family: monospace, monospace;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L166"></td>
        <td id="file-github-markdown-css-LC166">  font-size: 1em;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L169"></td>
        <td id="file-github-markdown-css-LC169">body hr {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L170"></td>
        <td id="file-github-markdown-css-LC170">  box-sizing: content-box;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L171"></td>
        <td id="file-github-markdown-css-LC171">  height: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L172"></td>
        <td id="file-github-markdown-css-LC172">  overflow: visible;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L175"></td>
        <td id="file-github-markdown-css-LC175">body input {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L176"></td>
        <td id="file-github-markdown-css-LC176">  font: inherit;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L177"></td>
        <td id="file-github-markdown-css-LC177">  margin: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L180"></td>
        <td id="file-github-markdown-css-LC180">body input {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L181"></td>
        <td id="file-github-markdown-css-LC181">  overflow: visible;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L184"></td>
        <td id="file-github-markdown-css-LC184">body [type="checkbox"] {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L185"></td>
        <td id="file-github-markdown-css-LC185">  box-sizing: border-box;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L186"></td>
        <td id="file-github-markdown-css-LC186">  padding: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L189"></td>
        <td id="file-github-markdown-css-LC189">body * {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L190"></td>
        <td id="file-github-markdown-css-LC190">  box-sizing: border-box;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L193"></td>
        <td id="file-github-markdown-css-LC193">body input {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L194"></td>
        <td id="file-github-markdown-css-LC194">  font-family: inherit;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L195"></td>
        <td id="file-github-markdown-css-LC195">  font-size: inherit;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L196"></td>
        <td id="file-github-markdown-css-LC196">  line-height: inherit;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L199"></td>
        <td id="file-github-markdown-css-LC199">body a {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L200"></td>
        <td id="file-github-markdown-css-LC200">  color: #4078c0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L201"></td>
        <td id="file-github-markdown-css-LC201">  text-decoration: none;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L204"></td>
        <td id="file-github-markdown-css-LC204">body a:hover,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L205"></td>
        <td id="file-github-markdown-css-LC205">body a:active {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L206"></td>
        <td id="file-github-markdown-css-LC206">  text-decoration: underline;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L209"></td>
        <td id="file-github-markdown-css-LC209">body strong {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L210"></td>
        <td id="file-github-markdown-css-LC210">  font-weight: 600;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L213"></td>
        <td id="file-github-markdown-css-LC213">body hr {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L214"></td>
        <td id="file-github-markdown-css-LC214">  height: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L215"></td>
        <td id="file-github-markdown-css-LC215">  margin: 15px 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L216"></td>
        <td id="file-github-markdown-css-LC216">  overflow: hidden;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L217"></td>
        <td id="file-github-markdown-css-LC217">  background: transparent;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L218"></td>
        <td id="file-github-markdown-css-LC218">  border: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L219"></td>
        <td id="file-github-markdown-css-LC219">  border-bottom: 1px solid #ddd;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L222"></td>
        <td id="file-github-markdown-css-LC222">body hr::before {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L223"></td>
        <td id="file-github-markdown-css-LC223">  display: table;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L224"></td>
        <td id="file-github-markdown-css-LC224">  content: "";</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L227"></td>
        <td id="file-github-markdown-css-LC227">body hr::after {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L228"></td>
        <td id="file-github-markdown-css-LC228">  display: table;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L229"></td>
        <td id="file-github-markdown-css-LC229">  clear: both;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L230"></td>
        <td id="file-github-markdown-css-LC230">  content: "";</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L233"></td>
        <td id="file-github-markdown-css-LC233">body table {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L234"></td>
        <td id="file-github-markdown-css-LC234">  border-spacing: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L235"></td>
        <td id="file-github-markdown-css-LC235">  border-collapse: collapse;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L238"></td>
        <td id="file-github-markdown-css-LC238">body td,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L239"></td>
        <td id="file-github-markdown-css-LC239">body th {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L240"></td>
        <td id="file-github-markdown-css-LC240">  padding: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L243"></td>
        <td id="file-github-markdown-css-LC243">body h1,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L244"></td>
        <td id="file-github-markdown-css-LC244">body h2,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L245"></td>
        <td id="file-github-markdown-css-LC245">body h3,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L246"></td>
        <td id="file-github-markdown-css-LC246">body h4,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L247"></td>
        <td id="file-github-markdown-css-LC247">body h5,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L248"></td>
        <td id="file-github-markdown-css-LC248">body h6 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L249"></td>
        <td id="file-github-markdown-css-LC249">  margin-top: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L250"></td>
        <td id="file-github-markdown-css-LC250">  margin-bottom: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L253"></td>
        <td id="file-github-markdown-css-LC253">body h1 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L254"></td>
        <td id="file-github-markdown-css-LC254">  font-size: 32px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L255"></td>
        <td id="file-github-markdown-css-LC255">  font-weight: 600;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L258"></td>
        <td id="file-github-markdown-css-LC258">body h2 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L259"></td>
        <td id="file-github-markdown-css-LC259">  font-size: 24px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L260"></td>
        <td id="file-github-markdown-css-LC260">  font-weight: 600;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L263"></td>
        <td id="file-github-markdown-css-LC263">body h3 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L264"></td>
        <td id="file-github-markdown-css-LC264">  font-size: 20px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L265"></td>
        <td id="file-github-markdown-css-LC265">  font-weight: 600;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L268"></td>
        <td id="file-github-markdown-css-LC268">body h4 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L269"></td>
        <td id="file-github-markdown-css-LC269">  font-size: 16px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L270"></td>
        <td id="file-github-markdown-css-LC270">  font-weight: 600;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L273"></td>
        <td id="file-github-markdown-css-LC273">body h5 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L274"></td>
        <td id="file-github-markdown-css-LC274">  font-size: 14px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L275"></td>
        <td id="file-github-markdown-css-LC275">  font-weight: 600;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L278"></td>
        <td id="file-github-markdown-css-LC278">body h6 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L279"></td>
        <td id="file-github-markdown-css-LC279">  font-size: 12px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L280"></td>
        <td id="file-github-markdown-css-LC280">  font-weight: 600;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L283"></td>
        <td id="file-github-markdown-css-LC283">body p {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L284"></td>
        <td id="file-github-markdown-css-LC284">  margin-top: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L285"></td>
        <td id="file-github-markdown-css-LC285">  margin-bottom: 10px;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L288"></td>
        <td id="file-github-markdown-css-LC288">body blockquote {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L289"></td>
        <td id="file-github-markdown-css-LC289">  margin: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L292"></td>
        <td id="file-github-markdown-css-LC292">body ul,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L293"></td>
        <td id="file-github-markdown-css-LC293">body ol {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L294"></td>
        <td id="file-github-markdown-css-LC294">  padding-left: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L295"></td>
        <td id="file-github-markdown-css-LC295">  margin-top: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L296"></td>
        <td id="file-github-markdown-css-LC296">  margin-bottom: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L299"></td>
        <td id="file-github-markdown-css-LC299">body ol ol,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L300"></td>
        <td id="file-github-markdown-css-LC300">body ul ol {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L301"></td>
        <td id="file-github-markdown-css-LC301">  list-style-type: lower-roman;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L304"></td>
        <td id="file-github-markdown-css-LC304">body ul ul ol,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L305"></td>
        <td id="file-github-markdown-css-LC305">body ul ol ol,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L306"></td>
        <td id="file-github-markdown-css-LC306">body ol ul ol,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L307"></td>
        <td id="file-github-markdown-css-LC307">body ol ol ol {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L308"></td>
        <td id="file-github-markdown-css-LC308">  list-style-type: lower-alpha;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L311"></td>
        <td id="file-github-markdown-css-LC311">body dd {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L312"></td>
        <td id="file-github-markdown-css-LC312">  margin-left: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L315"></td>
        <td id="file-github-markdown-css-LC315">body code {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L316"></td>
        <td id="file-github-markdown-css-LC316">  font-family: Consolas, "Liberation Mono", Menlo, Courier, monospace;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L317"></td>
        <td id="file-github-markdown-css-LC317">  font-size: 12px;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L320"></td>
        <td id="file-github-markdown-css-LC320">body pre {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L321"></td>
        <td id="file-github-markdown-css-LC321">  margin-top: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L322"></td>
        <td id="file-github-markdown-css-LC322">  margin-bottom: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L323"></td>
        <td id="file-github-markdown-css-LC323">  font: 12px Consolas, "Liberation Mono", Menlo, Courier, monospace;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L326"></td>
        <td id="file-github-markdown-css-LC326">body .octicon {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L327"></td>
        <td id="file-github-markdown-css-LC327">  vertical-align: text-bottom;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L330"></td>
        <td id="file-github-markdown-css-LC330">body input {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L331"></td>
        <td id="file-github-markdown-css-LC331">  -webkit-font-feature-settings: "liga" 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L332"></td>
        <td id="file-github-markdown-css-LC332">  font-feature-settings: "liga" 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L335"></td>
        <td id="file-github-markdown-css-LC335">body::before {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L336"></td>
        <td id="file-github-markdown-css-LC336">  display: table;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L337"></td>
        <td id="file-github-markdown-css-LC337">  content: "";</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L340"></td>
        <td id="file-github-markdown-css-LC340">body::after {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L341"></td>
        <td id="file-github-markdown-css-LC341">  display: table;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L342"></td>
        <td id="file-github-markdown-css-LC342">  clear: both;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L343"></td>
        <td id="file-github-markdown-css-LC343">  content: "";</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L346"></td>
        <td id="file-github-markdown-css-LC346">body&gt;*:first-child {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L347"></td>
        <td id="file-github-markdown-css-LC347">  margin-top: 0 !important;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L350"></td>
        <td id="file-github-markdown-css-LC350">body&gt;*:last-child {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L351"></td>
        <td id="file-github-markdown-css-LC351">  margin-bottom: 0 !important;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L354"></td>
        <td id="file-github-markdown-css-LC354">body a:not([href]) {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L355"></td>
        <td id="file-github-markdown-css-LC355">  color: inherit;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L356"></td>
        <td id="file-github-markdown-css-LC356">  text-decoration: none;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L359"></td>
        <td id="file-github-markdown-css-LC359">body .anchor {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L360"></td>
        <td id="file-github-markdown-css-LC360">  float: left;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L361"></td>
        <td id="file-github-markdown-css-LC361">  padding-right: 4px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L362"></td>
        <td id="file-github-markdown-css-LC362">  margin-left: -20px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L363"></td>
        <td id="file-github-markdown-css-LC363">  line-height: 1;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L366"></td>
        <td id="file-github-markdown-css-LC366">body .anchor:focus {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L367"></td>
        <td id="file-github-markdown-css-LC367">  outline: none;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L370"></td>
        <td id="file-github-markdown-css-LC370">body p,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L371"></td>
        <td id="file-github-markdown-css-LC371">body blockquote,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L372"></td>
        <td id="file-github-markdown-css-LC372">body ul,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L373"></td>
        <td id="file-github-markdown-css-LC373">body ol,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L374"></td>
        <td id="file-github-markdown-css-LC374">body dl,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L375"></td>
        <td id="file-github-markdown-css-LC375">body table,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L376"></td>
        <td id="file-github-markdown-css-LC376">body pre {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L377"></td>
        <td id="file-github-markdown-css-LC377">  margin-top: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L378"></td>
        <td id="file-github-markdown-css-LC378">  margin-bottom: 16px;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L381"></td>
        <td id="file-github-markdown-css-LC381">body hr {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L382"></td>
        <td id="file-github-markdown-css-LC382">  height: 0.25em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L383"></td>
        <td id="file-github-markdown-css-LC383">  padding: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L384"></td>
        <td id="file-github-markdown-css-LC384">  margin: 24px 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L385"></td>
        <td id="file-github-markdown-css-LC385">  background-color: #e7e7e7;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L386"></td>
        <td id="file-github-markdown-css-LC386">  border: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L389"></td>
        <td id="file-github-markdown-css-LC389">body blockquote {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L390"></td>
        <td id="file-github-markdown-css-LC390">  padding: 0 1em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L391"></td>
        <td id="file-github-markdown-css-LC391">  color: #777;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L392"></td>
        <td id="file-github-markdown-css-LC392">  border-left: 0.25em solid #ddd;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L395"></td>
        <td id="file-github-markdown-css-LC395">body blockquote&gt;:first-child {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L396"></td>
        <td id="file-github-markdown-css-LC396">  margin-top: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L399"></td>
        <td id="file-github-markdown-css-LC399">body blockquote&gt;:last-child {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L400"></td>
        <td id="file-github-markdown-css-LC400">  margin-bottom: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L403"></td>
        <td id="file-github-markdown-css-LC403">body kbd {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L404"></td>
        <td id="file-github-markdown-css-LC404">  display: inline-block;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L405"></td>
        <td id="file-github-markdown-css-LC405">  padding: 3px 5px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L406"></td>
        <td id="file-github-markdown-css-LC406">  font-size: 11px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L407"></td>
        <td id="file-github-markdown-css-LC407">  line-height: 10px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L408"></td>
        <td id="file-github-markdown-css-LC408">  color: #555;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L409"></td>
        <td id="file-github-markdown-css-LC409">  vertical-align: middle;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L410"></td>
        <td id="file-github-markdown-css-LC410">  background-color: #fcfcfc;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L411"></td>
        <td id="file-github-markdown-css-LC411">  border: solid 1px #ccc;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L412"></td>
        <td id="file-github-markdown-css-LC412">  border-bottom-color: #bbb;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L413"></td>
        <td id="file-github-markdown-css-LC413">  border-radius: 3px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L414"></td>
        <td id="file-github-markdown-css-LC414">  box-shadow: inset 0 -1px 0 #bbb;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L417"></td>
        <td id="file-github-markdown-css-LC417">body h1,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L418"></td>
        <td id="file-github-markdown-css-LC418">body h2,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L419"></td>
        <td id="file-github-markdown-css-LC419">body h3,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L420"></td>
        <td id="file-github-markdown-css-LC420">body h4,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L421"></td>
        <td id="file-github-markdown-css-LC421">body h5,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L422"></td>
        <td id="file-github-markdown-css-LC422">body h6 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L423"></td>
        <td id="file-github-markdown-css-LC423">  margin-top: 24px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L424"></td>
        <td id="file-github-markdown-css-LC424">  margin-bottom: 16px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L425"></td>
        <td id="file-github-markdown-css-LC425">  font-weight: 600;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L426"></td>
        <td id="file-github-markdown-css-LC426">  line-height: 1.25;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L429"></td>
        <td id="file-github-markdown-css-LC429">body h1 .octicon-link,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L430"></td>
        <td id="file-github-markdown-css-LC430">body h2 .octicon-link,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L431"></td>
        <td id="file-github-markdown-css-LC431">body h3 .octicon-link,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L432"></td>
        <td id="file-github-markdown-css-LC432">body h4 .octicon-link,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L433"></td>
        <td id="file-github-markdown-css-LC433">body h5 .octicon-link,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L434"></td>
        <td id="file-github-markdown-css-LC434">body h6 .octicon-link {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L435"></td>
        <td id="file-github-markdown-css-LC435">  color: #000;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L436"></td>
        <td id="file-github-markdown-css-LC436">  vertical-align: middle;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L437"></td>
        <td id="file-github-markdown-css-LC437">  visibility: hidden;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L440"></td>
        <td id="file-github-markdown-css-LC440">body h1:hover .anchor,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L441"></td>
        <td id="file-github-markdown-css-LC441">body h2:hover .anchor,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L442"></td>
        <td id="file-github-markdown-css-LC442">body h3:hover .anchor,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L443"></td>
        <td id="file-github-markdown-css-LC443">body h4:hover .anchor,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L444"></td>
        <td id="file-github-markdown-css-LC444">body h5:hover .anchor,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L445"></td>
        <td id="file-github-markdown-css-LC445">body h6:hover .anchor {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L446"></td>
        <td id="file-github-markdown-css-LC446">  text-decoration: none;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L449"></td>
        <td id="file-github-markdown-css-LC449">body h1:hover .anchor .octicon-link,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L450"></td>
        <td id="file-github-markdown-css-LC450">body h2:hover .anchor .octicon-link,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L451"></td>
        <td id="file-github-markdown-css-LC451">body h3:hover .anchor .octicon-link,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L452"></td>
        <td id="file-github-markdown-css-LC452">body h4:hover .anchor .octicon-link,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L453"></td>
        <td id="file-github-markdown-css-LC453">body h5:hover .anchor .octicon-link,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L454"></td>
        <td id="file-github-markdown-css-LC454">body h6:hover .anchor .octicon-link {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L455"></td>
        <td id="file-github-markdown-css-LC455">  visibility: visible;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L458"></td>
        <td id="file-github-markdown-css-LC458">body h1 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L459"></td>
        <td id="file-github-markdown-css-LC459">  padding-bottom: 0.3em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L460"></td>
        <td id="file-github-markdown-css-LC460">  font-size: 2em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L461"></td>
        <td id="file-github-markdown-css-LC461">  border-bottom: 1px solid #eee;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L464"></td>
        <td id="file-github-markdown-css-LC464">body h2 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L465"></td>
        <td id="file-github-markdown-css-LC465">  padding-bottom: 0.3em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L466"></td>
        <td id="file-github-markdown-css-LC466">  font-size: 1.5em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L467"></td>
        <td id="file-github-markdown-css-LC467">  border-bottom: 1px solid #eee;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L470"></td>
        <td id="file-github-markdown-css-LC470">body h3 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L471"></td>
        <td id="file-github-markdown-css-LC471">  font-size: 1.25em;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L474"></td>
        <td id="file-github-markdown-css-LC474">body h4 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L475"></td>
        <td id="file-github-markdown-css-LC475">  font-size: 1em;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L478"></td>
        <td id="file-github-markdown-css-LC478">body h5 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L479"></td>
        <td id="file-github-markdown-css-LC479">  font-size: 0.875em;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L482"></td>
        <td id="file-github-markdown-css-LC482">body h6 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L483"></td>
        <td id="file-github-markdown-css-LC483">  font-size: 0.85em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L484"></td>
        <td id="file-github-markdown-css-LC484">  color: #777;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L487"></td>
        <td id="file-github-markdown-css-LC487">body ul,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L488"></td>
        <td id="file-github-markdown-css-LC488">body ol {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L489"></td>
        <td id="file-github-markdown-css-LC489">  padding-left: 2em;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L492"></td>
        <td id="file-github-markdown-css-LC492">body ul ul,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L493"></td>
        <td id="file-github-markdown-css-LC493">body ul ol,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L494"></td>
        <td id="file-github-markdown-css-LC494">body ol ol,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L495"></td>
        <td id="file-github-markdown-css-LC495">body ol ul {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L496"></td>
        <td id="file-github-markdown-css-LC496">  margin-top: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L497"></td>
        <td id="file-github-markdown-css-LC497">  margin-bottom: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L500"></td>
        <td id="file-github-markdown-css-LC500">body li&gt;p {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L501"></td>
        <td id="file-github-markdown-css-LC501">  margin-top: 16px;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L504"></td>
        <td id="file-github-markdown-css-LC504">body li+li {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L505"></td>
        <td id="file-github-markdown-css-LC505">  margin-top: 0.25em;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L508"></td>
        <td id="file-github-markdown-css-LC508">body dl {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L509"></td>
        <td id="file-github-markdown-css-LC509">  padding: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L512"></td>
        <td id="file-github-markdown-css-LC512">body dl dt {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L513"></td>
        <td id="file-github-markdown-css-LC513">  padding: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L514"></td>
        <td id="file-github-markdown-css-LC514">  margin-top: 16px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L515"></td>
        <td id="file-github-markdown-css-LC515">  font-size: 1em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L516"></td>
        <td id="file-github-markdown-css-LC516">  font-style: italic;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L517"></td>
        <td id="file-github-markdown-css-LC517">  font-weight: bold;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L520"></td>
        <td id="file-github-markdown-css-LC520">body dl dd {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L521"></td>
        <td id="file-github-markdown-css-LC521">  padding: 0 16px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L522"></td>
        <td id="file-github-markdown-css-LC522">  margin-bottom: 16px;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L525"></td>
        <td id="file-github-markdown-css-LC525">body table {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L526"></td>
        <td id="file-github-markdown-css-LC526">  display: block;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L527"></td>
        <td id="file-github-markdown-css-LC527">  width: 100%;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L528"></td>
        <td id="file-github-markdown-css-LC528">  overflow: auto;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L531"></td>
        <td id="file-github-markdown-css-LC531">body table th {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L532"></td>
        <td id="file-github-markdown-css-LC532">  font-weight: bold;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L535"></td>
        <td id="file-github-markdown-css-LC535">body table th,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L536"></td>
        <td id="file-github-markdown-css-LC536">body table td {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L537"></td>
        <td id="file-github-markdown-css-LC537">  padding: 6px 13px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L538"></td>
        <td id="file-github-markdown-css-LC538">  border: 1px solid #ddd;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L541"></td>
        <td id="file-github-markdown-css-LC541">body table tr {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L542"></td>
        <td id="file-github-markdown-css-LC542">  background-color: #fff;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L543"></td>
        <td id="file-github-markdown-css-LC543">  border-top: 1px solid #ccc;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L546"></td>
        <td id="file-github-markdown-css-LC546">body table tr:nth-child(2n) {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L547"></td>
        <td id="file-github-markdown-css-LC547">  background-color: #f8f8f8;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L550"></td>
        <td id="file-github-markdown-css-LC550">body img {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L551"></td>
        <td id="file-github-markdown-css-LC551">  max-width: 100%;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L552"></td>
        <td id="file-github-markdown-css-LC552">  box-sizing: content-box;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L553"></td>
        <td id="file-github-markdown-css-LC553">  background-color: #fff;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L556"></td>
        <td id="file-github-markdown-css-LC556">body code {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L557"></td>
        <td id="file-github-markdown-css-LC557">  padding: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L558"></td>
        <td id="file-github-markdown-css-LC558">  padding-top: 0.2em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L559"></td>
        <td id="file-github-markdown-css-LC559">  padding-bottom: 0.2em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L560"></td>
        <td id="file-github-markdown-css-LC560">  margin: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L561"></td>
        <td id="file-github-markdown-css-LC561">  font-size: 85%;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L562"></td>
        <td id="file-github-markdown-css-LC562">  background-color: rgba(0,0,0,0.04);</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L563"></td>
        <td id="file-github-markdown-css-LC563">  border-radius: 3px;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L566"></td>
        <td id="file-github-markdown-css-LC566">body code::before,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L567"></td>
        <td id="file-github-markdown-css-LC567">body code::after {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L568"></td>
        <td id="file-github-markdown-css-LC568">  letter-spacing: -0.2em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L569"></td>
        <td id="file-github-markdown-css-LC569">  content: "\00a0";</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L572"></td>
        <td id="file-github-markdown-css-LC572">body pre {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L573"></td>
        <td id="file-github-markdown-css-LC573">  word-wrap: normal;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L576"></td>
        <td id="file-github-markdown-css-LC576">body pre&gt;code {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L577"></td>
        <td id="file-github-markdown-css-LC577">  padding: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L578"></td>
        <td id="file-github-markdown-css-LC578">  margin: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L579"></td>
        <td id="file-github-markdown-css-LC579">  font-size: 100%;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L580"></td>
        <td id="file-github-markdown-css-LC580">  word-break: normal;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L581"></td>
        <td id="file-github-markdown-css-LC581">  white-space: pre;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L582"></td>
        <td id="file-github-markdown-css-LC582">  background: transparent;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L583"></td>
        <td id="file-github-markdown-css-LC583">  border: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L586"></td>
        <td id="file-github-markdown-css-LC586">body .highlight {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L587"></td>
        <td id="file-github-markdown-css-LC587">  margin-bottom: 16px;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L590"></td>
        <td id="file-github-markdown-css-LC590">body .highlight pre {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L591"></td>
        <td id="file-github-markdown-css-LC591">  margin-bottom: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L592"></td>
        <td id="file-github-markdown-css-LC592">  word-break: normal;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L595"></td>
        <td id="file-github-markdown-css-LC595">body .highlight pre,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L596"></td>
        <td id="file-github-markdown-css-LC596">body pre {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L597"></td>
        <td id="file-github-markdown-css-LC597">  padding: 16px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L598"></td>
        <td id="file-github-markdown-css-LC598">  overflow: auto;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L599"></td>
        <td id="file-github-markdown-css-LC599">  font-size: 85%;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L600"></td>
        <td id="file-github-markdown-css-LC600">  line-height: 1.45;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L601"></td>
        <td id="file-github-markdown-css-LC601">  background-color: #f7f7f7;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L602"></td>
        <td id="file-github-markdown-css-LC602">  border-radius: 3px;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L605"></td>
        <td id="file-github-markdown-css-LC605">body pre code {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L606"></td>
        <td id="file-github-markdown-css-LC606">  display: inline;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L607"></td>
        <td id="file-github-markdown-css-LC607">  max-width: auto;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L608"></td>
        <td id="file-github-markdown-css-LC608">  padding: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L609"></td>
        <td id="file-github-markdown-css-LC609">  margin: 0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L610"></td>
        <td id="file-github-markdown-css-LC610">  overflow: visible;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L611"></td>
        <td id="file-github-markdown-css-LC611">  line-height: inherit;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L612"></td>
        <td id="file-github-markdown-css-LC612">  word-wrap: normal;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L613"></td>
        <td id="file-github-markdown-css-LC613">  background-color: transparent;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L614"></td>
        <td id="file-github-markdown-css-LC614">  border: 0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L617"></td>
        <td id="file-github-markdown-css-LC617">body pre code::before,</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L618"></td>
        <td id="file-github-markdown-css-LC618">body pre code::after {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L619"></td>
        <td id="file-github-markdown-css-LC619">  content: normal;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L622"></td>
        <td id="file-github-markdown-css-LC622">body .pl-0 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L623"></td>
        <td id="file-github-markdown-css-LC623">  padding-left: 0 !important;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L626"></td>
        <td id="file-github-markdown-css-LC626">body .pl-1 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L627"></td>
        <td id="file-github-markdown-css-LC627">  padding-left: 3px !important;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L630"></td>
        <td id="file-github-markdown-css-LC630">body .pl-2 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L631"></td>
        <td id="file-github-markdown-css-LC631">  padding-left: 6px !important;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L634"></td>
        <td id="file-github-markdown-css-LC634">body .pl-3 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L635"></td>
        <td id="file-github-markdown-css-LC635">  padding-left: 12px !important;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L638"></td>
        <td id="file-github-markdown-css-LC638">body .pl-4 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L639"></td>
        <td id="file-github-markdown-css-LC639">  padding-left: 24px !important;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L642"></td>
        <td id="file-github-markdown-css-LC642">body .pl-5 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L643"></td>
        <td id="file-github-markdown-css-LC643">  padding-left: 36px !important;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L646"></td>
        <td id="file-github-markdown-css-LC646">body .pl-6 {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L647"></td>
        <td id="file-github-markdown-css-LC647">  padding-left: 48px !important;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L650"></td>
        <td id="file-github-markdown-css-LC650">body .full-commit .btn-outline:not(:disabled):hover {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L651"></td>
        <td id="file-github-markdown-css-LC651">  color: #4078c0;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L652"></td>
        <td id="file-github-markdown-css-LC652">  border: 1px solid #4078c0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L655"></td>
        <td id="file-github-markdown-css-LC655">body kbd {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L656"></td>
        <td id="file-github-markdown-css-LC656">  display: inline-block;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L657"></td>
        <td id="file-github-markdown-css-LC657">  padding: 3px 5px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L658"></td>
        <td id="file-github-markdown-css-LC658">  font: 11px Consolas, "Liberation Mono", Menlo, Courier, monospace;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L659"></td>
        <td id="file-github-markdown-css-LC659">  line-height: 10px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L660"></td>
        <td id="file-github-markdown-css-LC660">  color: #555;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L661"></td>
        <td id="file-github-markdown-css-LC661">  vertical-align: middle;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L662"></td>
        <td id="file-github-markdown-css-LC662">  background-color: #fcfcfc;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L663"></td>
        <td id="file-github-markdown-css-LC663">  border: solid 1px #ccc;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L664"></td>
        <td id="file-github-markdown-css-LC664">  border-bottom-color: #bbb;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L665"></td>
        <td id="file-github-markdown-css-LC665">  border-radius: 3px;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L666"></td>
        <td id="file-github-markdown-css-LC666">  box-shadow: inset 0 -1px 0 #bbb;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L669"></td>
        <td id="file-github-markdown-css-LC669">body :checked+.radio-label {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L670"></td>
        <td id="file-github-markdown-css-LC670">  position: relative;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L671"></td>
        <td id="file-github-markdown-css-LC671">  z-index: 1;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L672"></td>
        <td id="file-github-markdown-css-LC672">  border-color: #4078c0;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L675"></td>
        <td id="file-github-markdown-css-LC675">body .task-list-item {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L676"></td>
        <td id="file-github-markdown-css-LC676">  list-style-type: none;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L679"></td>
        <td id="file-github-markdown-css-LC679">body .task-list-item+.task-list-item {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L680"></td>
        <td id="file-github-markdown-css-LC680">  margin-top: 3px;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L683"></td>
        <td id="file-github-markdown-css-LC683">body .task-list-item input {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L684"></td>
        <td id="file-github-markdown-css-LC684">  margin: 0 0.2em 0.25em -1.6em;</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L685"></td>
        <td id="file-github-markdown-css-LC685">  vertical-align: middle;</td>
      </tr>
      
      
      <tr>
        <td id="file-github-markdown-css-L688"></td>
        <td id="file-github-markdown-css-LC688">body hr {</td>
      </tr>
      <tr>
        <td id="file-github-markdown-css-L689"></td>
        <td id="file-github-markdown-css-LC689">  border-bottom-color: #eee;</td>
      </tr>
      
</tbody></table>


  
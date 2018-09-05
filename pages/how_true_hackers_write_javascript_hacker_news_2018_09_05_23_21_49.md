<a href="https://news.ycombinator.com/item?id=17915560">https://news.ycombinator.com/item?id=17915560</a><div id="articleHeader"><h1>How true hackers write JavaScript</h1></div><table id="hnmain">
        <tbody>
<tr><td>
  <table>
            <tbody><tr id="17917993"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Everything has a context. If your site has:<pre><code>  - minimal functionality
  - rarely if ever changes
  - is maintained by a very small group (Hacker News)
</code></pre>
...then something like the example linked is perfect. Most web app developers don't live in this world. The more common situation is:<pre><code>  - large and/or transient teams
  - large quantity of inter-dependent features
  - constant changes
</code></pre>
...which means that the thing you need to optimize for isn't pretty/fast code. It's clarity and resiliency in the code. Can a junior and senior dev both work on the same code base? Can someone new to the project be effective with minimal ramp up time? Can you work on a feature without accidentally stepping on another persons current task?<p>Modern web apps are less about being performant and minimal, and more about dealing with the complexities of large software teams
              </p><div>        <p>
                      <u><a href="reply?id=17917993&goto=item%3Fid%3D17915560%2317917993" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17918161"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  &gt;&gt; Modern web apps are less about being performant and minimal, and more about dealing with the complexities of large software teams<p>If that's true, then the app will likely have what I call a "programmer's interface" (which is especially common in most enterprise web apps I encounter). Those apps might be solid from a code perspective, but don't tend to be very user friendly.</p><p>I tend to think that modern web apps are more about dealing with the complexities of balancing functionality with ease of use to the end user <i>while</i> still dealing with the complexities of large <i>product</i> teams, which include but are not limited to designers, UX experts and developers.
              </p><div>        <p>
                      <u><a href="reply?id=17918161&goto=item%3Fid%3D17915560%2317918161" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17918488"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  The fancy-lookin' sites are the ones which hijack basic keyboard functionality, scroll in weird ways, etc.<p>I can't be the only person who finds browser default behavior more intuitive and usable in general.</p><p>Why does "UX" so often mean mouse-heavy and <i>always</i> favor the beginner over the power-user.
              </p><div>        <p>
                      <u><a href="reply?id=17918488&goto=item%3Fid%3D17915560%2317918488" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17918477"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Yes, and just to express the same idea from a different perspective... you need to deliver the features needed by your business.<p>In a small, simple, established site, those needs don't change often, so the code doesn't change often, and you can focus more on performance than maintainability, as well as spend your efforts on non-coding tasks.</p><p>In a startup when you are finding your market and seeking product/market fit, and you've got investors demanding speedy delivery of a product to customers, the attempted solution is often a large team with fast and numerous code changes. And then you do have to optimize for the devs, because even though the final goal is customer satisfaction, devs need to perform efficiently to hit that goal.</p><p>The needs of the codebase still tie back to the needs of the business. One answer does not fit all.
              </p><div>        <p>
                      <u><a href="reply?id=17918477&goto=item%3Fid%3D17915560%2317918477" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17918737"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  The code style is fine, it's practical.<p>But how about what it does?  Has anyone ever tried to collapse or expand a 100+ comment thread here?  It can lag for 1-2s.  So all the talk of "it's simple code that serves its purpose" is not really true.</p><p>That said, please don't solve my complaint by adding a bunch of SPA stuff to HN.  I love how fast the base content loads here and how there's nothing dynamic.
              </p><div>        <p>
                      <u><a href="reply?id=17918737&goto=item%3Fid%3D17915560%2317918737" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17917019"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Way better than loading megabytes of .js just to display stupid animations and other useless gimmicky stuff.<p>This file is just in consonance with this website's style: concise, terse, to-the-point and with minimal bs.</p><p>Of all of my currently in-rotation news websites, this loads and reacts the fastest, no matter where I am or how crippled my current connection is. I am sure they are factoring load times and speed over 'shiny new features'.</p><p>Keep going, YC!
              </p><div>        <p>
                      <u><a href="reply?id=17917019&goto=item%3Fid%3D17915560%2317917019" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917394"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Animations being badly/over used aside, this is a bit of a straw man argument.<p>If you load megabytes of JS to do animations, as opposed to using CSS, then yes you are just doing it wrong.</p><p>Things aren't either exactly right and done one way, or else terrible. You can of course have bells and whistles like animations if your usecase requires them (HN doesn't!) and still have a fast loading site with clean code, if you do it right.
              </p><div>        <p>
                      <u><a href="reply?id=17917394&goto=item%3Fid%3D17915560%2317917394" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917448"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  I agree with you. And the animations example was simply one of the bad offenders (merely one of the symptoms of the disease).<p>The disease is overutilizing buckloads of js scaffolding which is blatant in the majority of the websites right now. Even a small blog now "has to have" the latest xzibit framework which pulls 32 foobar dependencies, all gulped into one huge blob of minified compressed clusterfuck-pack.
              </p><div>        <p>
                      <u><a href="reply?id=17917448&goto=item%3Fid%3D17915560%2317917448" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917680"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  Yeah, I guess it is a tradeoff between engineering productivity and performance. Both are features. Past a certain level of complexity it <i>is</i> usually the correct decision to choose the framework and toolchain so that you can deliver and maintain features <i>at all</i>. "Make it work -&gt; make it good -&gt; make it fast" is very relevant here.<p>Though I agree about what you're saying for blogs and other content sites, where the tradeoff is clearly inappropriate in a lot of cases. With that said, things like <a href="https://www.gatsbyjs.org/" target="_blank">https://www.gatsbyjs.org/</a> offer an interesting '3rd way' here, allowing you to keep the productive toolchain and framework stuff but still serve a blazing fast static content site.
              </p><div>        <p>
                      <u><a href="reply?id=17917680&goto=item%3Fid%3D17915560%2317917680" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917943"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I was at the bottom of Africa last month with unstable internet connection barely faster than dial-up. HN was the only site I could connect before getting timeouts and bs.
              <div>        <p>
                      <u><a href="reply?id=17917943&goto=item%3Fid%3D17915560%2317917943" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17916352"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I don't understand why people are dissing this.<p>It does what it's designed to do, and fills a specific need for <i>one</i> website. It's not there as a teaching aid, nor is it meant to be shared for other people to use elsewhere.</p><p>Not everything has to be gold-standard code full of perfect variable names, extensive comments and good whitespacing. If you have a day job that isn't primarily writing code, and/or you are likely to be the only person ever working on that code, who cares if it's not up to the standard that people around here seem to expect of every project?</p><p>As long as the code works, anything else is just gravy. If you were to peel back the layers on all the major websites out there, I'm sure you'd find less than stellar code everywhere.
              </p><div>        <p>
                      <u><a href="reply?id=17916352&goto=item%3Fid%3D17915560%2317916352" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916511"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  There are some polarized opinions in this thread. Someone wrote <i>That might be one of the most readable pieces of code that I've ever read.</i> Apparently it improves readability immensely to rename 'forEach' to 'aeach'.<p>To be honest the code is not very readable, but it <i>is</i> very simple and self contained. It would be very easy to dive into to fix a bug because there are no external dependencies or frameworks you have to understand.</p><p>The list of one-liners at the top seem like a very minimal 'jQuery'-like layer. Perfectly fine except for the l33t identifier names.</p><p>But there is also some really fragile coupling to the HTML, e.g.:</p><pre><code>   for (var i=0; i &lt; 3; i++) { remEl($(id).nextSibling) }
</code></pre>
I wouldn't dare to modify the HTML when the JavaScript looks like this! What are the three elements which are being removed? Why exactly three? Probably the author and maintainer of the code knows, but this is the kind of coupling where nobody except the original author would dare to change anything. Perhaps this why HN still uses tables for presentation - nobody dares to change it?
              <div>        <p>
                      <u><a href="reply?id=17916511&goto=item%3Fid%3D17915560%2317916511" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916998"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  I think the purpose of 'aeach' is not to rename, but to provide a conversion. 'aeach' converts to an array in order to be able to perform a 'forEach' on the non-array NodeLists.<p>The 3 elements being removed are the tr containing the story options, a literal whitespace node, and a tr used as a spacer.</p><p>I agree it is a coupling, and while accurate to describe as fragile or even really fragile, I personally would not have used those words.</p><p>I would feel more comfortable daring to make changes in this html and JavaScript than any other front-end code I've worked with in the last 15 years of my career. If for no other reason, the sheer small size of it and lack of external dependencies that you mentioned.
              </p><div>        <p>
                      <u><a href="reply?id=17916998&goto=item%3Fid%3D17915560%2317916998" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17917521"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  You could reach a happy medium if everything was well commented. Introduce a build step to strip comments if you have to. But you would get maintainability while still having full visibility into all the code that is executing.
              <div>        <p>
                      <u><a href="reply?id=17917521&goto=item%3Fid%3D17915560%2317917521" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916869"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Perhaps this why HN still uses tables for presentation - nobody dares to change it?<p>There's also simply no reason to change it, it works.
              </p><div>        <p>
                      <u><a href="reply?id=17916869&goto=item%3Fid%3D17915560%2317916869" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917296"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  Sure, don't fix it if it ain't broken. Today there is no reason to use tables for presentation, but that was probably not the case when HN was initially designed many years ago.
              <div>        <p>
                      <u><a href="reply?id=17917296&goto=item%3Fid%3D17915560%2317917296" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17918300"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  When I last looked into it, tables caused issues for screenreaders and the like.
              <div>        <p>
                      <u><a href="reply?id=17918300&goto=item%3Fid%3D17915560%2317918300" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916924"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  &gt; <i>There's also simply no reason to change it, it works.</i><p>It works, and it's arguably simpler than the div-soup with extensive styling, which is the "kosher" way of doing this.
              </p><div>        <p>
                      <u><a href="reply?id=17916924&goto=item%3Fid%3D17915560%2317916924" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917248"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  Well using divs would at least make you able to group the elements semantically so you could remove a single node rather than having a for loop which removes exactly three nodes. This would be significantly simpler in my opinion. And it would be less fragile since now you can redesign everything inside this node without the JavaScript breaking.
              <div>        <p>
                      <u><a href="reply?id=17917248&goto=item%3Fid%3D17915560%2317917248" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17918652"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="200" height="1" /></td><td></td><td><div>
                  Agreed. But getting divs to do what you want has also gotten considerably easier in the last 10 years. It used to be a lot more work/boilerplate to get a consistent div-based layout across all browsers down to IE 6.<p>As for the redesign, the total amount of code (HTML/CSS/JS) you’d need to touch is still small. Do web designers still exist that only do HTML/CSS but no JS?
              </p><div>        <p>
                      <u><a href="reply?id=17918652&goto=item%3Fid%3D17915560%2317918652" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17917770"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="200" height="1" /></td><td></td><td><div>
                  I expect the layout would also be simpler in another way:  Give every "child" div a static indentation, nothing more.  They'll nest and the indentation will stack the deeper the comments go.<p>Right now there's already nested tables-within-tables, just to work around how table columns work in order to handle indentation (and each row's indentation is handled separately with a stretched 1x1 image with a width attribute that's calculated server-side).
              </p><div>        <p>
                      <u><a href="reply?id=17917770&goto=item%3Fid%3D17915560%2317917770" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17917795"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  I'd argue it's far from ideal. Mainly because closing a large tree of comments can often hang the UI for a second or so while this JS runs to find and hide all the children that need to be hidden.<p>But it is simple, and it does get the job done for the most part.
              </p><div>        <p>
                      <u><a href="reply?id=17917795&goto=item%3Fid%3D17915560%2317917795" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
          <tr id="17918568"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I think there are two ways of looking at this.<p>From the top down (strategic), and from the bottom up (tactical).</p><p>Depending on your perspective, you will likely fixate on different things.</p><p>If you're starting from the bottom, you'll probably be more interested in the coding choices made by the developer.</p><p>If you're coming from the top, you'll probably look at the goals of the site and whether the code met them, and then consider other details like optimization and cleanliness to be secondary ('gravy').</p><p>When I was in biz-school in the 90s, we used to spend a lot of time talking about effectiveness (the end result does what it needs to do) and efficiency (the end result does what it needs to do and is optimized for -insert criteria here-).</p><p>Ideally, you get to be both effective and efficient. If, however, you can only be one, it's better to be effective.
              </p><div>        <p>
                      <u><a href="reply?id=17918568&goto=item%3Fid%3D17915560%2317918568" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916544"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I believe there is a difference between gold-standard perfect code and just making "beginners mistakes".<p>It costs almost nothing more to write "event" instead of "ev" or "removeElement" instead of "remEl", but it makes the code much more readable. You might gain 1s for writting remEl instead of removeElement but you will loose more seconds in the future trying to remember what remEl stands for, or having to check what abbreviation you chose for that function.</p><p>It's just something programmers learn with experience (even when working alone) : abbreviations are a false good idea, and people are just pointing that out.
              </p><div>        <p>
                      <u><a href="reply?id=17916544&goto=item%3Fid%3D17915560%2317916544" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916762"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  &gt; It costs almost nothing more to write "event" instead of "ev" or "removeElement" instead of "remEl", but it makes the code much more readable.<p>No, it doesn't. Unless you're an absolute beginner, it takes you a couple of seconds to realize that in this codebase, "ev" (or "evt" or even "e") means "event". The same goes for "remEl". If that's consistent, then it's not a big deal at all.</p><p>Having less characters makes code more readable (or rather "scannable") as well, it's just another tradeoff.
              </p><div>        <p>
                      <u><a href="reply?id=17916762&goto=item%3Fid%3D17915560%2317916762" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17918708"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  &gt; Having less characters makes code more readable (or rather "scannable") as well, it's just another tradeoff.<p>It might, in a specific circumstance, while in another circumstance it might make the code significantly less readable. That is an indication that number of characters is probably not a good metric for adjusting readability.
              </p><div>        <p>
                      <u><a href="reply?id=17918708&goto=item%3Fid%3D17915560%2317918708" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916788"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  &gt;Having less characters makes code more readable (or rather "scannable") as well, it's just another tradeoff.<p>Only to a point, otherwise minified js would be more legible than plain source. It takes "a couple of seconds" to scan the codebase and find out what el or ev refer to, but it would take zero seconds if they were just called "event" or "element."[0] There's no gain in readability from shaving off one or two characters in that case. It just "feels" more efficient because it resembles the common style of lower level code.</p><p>[0]Assuming those aren't reserved words in javascript, I don't know.
              </p><div>        <p>
                      <u><a href="reply?id=17916788&goto=item%3Fid%3D17915560%2317916788" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917232"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  Of course, up to a point. The same goes for very long but extremely descriptive variable names. Hence, it is a tradeoff.
              <div>        <p>
                      <u><a href="reply?id=17917232&goto=item%3Fid%3D17915560%2317917232" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
            <tr id="17917815"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  Less characters really only makes sense in some scenarios, e.g. "unimportant" variables (for loops, temporary storage inside a procedure).  Verbose 'variablesToKeepTrackOfPositionInThisLoop' is obviously pointless when 'i' will do.<p>However renaming "important" things to make it quicker to read or type is, in my experience, a mistake if your code base is more than just a handful of files. Descriptive names make it much easier to <i>understand</i> the code which is more important in my experience. As the number of code files gets beyond a few files any benefits you get are rapidly lost because now you need to keep all that knowledge in your head and start having to jump around between 5, 10, 20 or more files to work out what everything <i>is</i> let alone what it is <i>doing</i>. This is why naming stuff in code is so important (and sometimes so hard).</p><p>Golang has a good philosophy on this front: <a href="https://github.com/golang/go/wiki/CodeReviewComments#variable-names" target="_blank">https://github.com/golang/go/wiki/CodeReviewComments#variabl...</a> tl-dr: the further from its declaration that a name is used, the more descriptive it should be.</p><p>This sort of attitude about brevity & speed appears to be a common problem with some developers I come across - they are absolutely <i>obsessed</i> with "productivity" when it comes to writing code.  They've just <i>got to</i> have their 97 plugins/extensions to their editor and they <i>simply must</i> have their finely-honed emacs keybindings. If you are focusing on just churning out code as fast as humanly possible (i.e. "productivity"), then your job as a programmer can probably be safely replaced with a couple of shell-scripts.</p><p>I've <i>never</i> been in a situation where the limiting factor in programming has been how fast I can read it or write it - the limiting factor has <i>always</i> been understanding the problem at hand, and designing a solution that solves the problem and is maintainable.
              </p><div>        <p>
                      <u><a href="reply?id=17917815&goto=item%3Fid%3D17915560%2317917815" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917938"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  &gt; Verbose 'variablesToKeepTrackOfPositionInThisLoop' is obviously pointless when 'i' will do<p>Based on a Fortran convention, IIRC. Within a web setting, "el" and "ev" are <i>extremely</i> conventional.
              </p><div>        <p>
                      <u><a href="reply?id=17917938&goto=item%3Fid%3D17915560%2317917938" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17918611"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  &gt; tl-dr: the further from its declaration that a name is used, the more descriptive it should be.<p>Interestingly, this results in more or less the opposite of entropy coding
              </p><div>        <p>
                      <u><a href="reply?id=17918611&goto=item%3Fid%3D17915560%2317918611" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17916789"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  Having anything take a couple of seconds more to read something is by definition making something less readable.<p>Okay so perhaps a couple of seconds doesn't matter. How many seconds does?
              </p><div>        <p>
                      <u><a href="reply?id=17916789&goto=item%3Fid%3D17915560%2317916789" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916835"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  There's an objective definition for readable?
              <div>        <p>
                      <u><a href="reply?id=17916835&goto=item%3Fid%3D17915560%2317916835" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    
          <tr id="17917867"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  &gt; As long as the code works, anything else is just gravy.<p>Nonsense. Maintainability almost always matters.</p><p>As the adage goes: code shouldn't <i>merely</i> work, it should <i>clearly</i> work.</p><p>&gt; If you were to peel back the layers on all the major websites out there, I'm sure you'd find less than stellar code everywhere.</p><p>Indeed, but Sturgeon's Law shouldn't make us feel better.
              </p><div>        <p>
                      <u><a href="reply?id=17917867&goto=item%3Fid%3D17915560%2317917867" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917902"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  In this <i>particular</i> case, the fact that the code is so terse makes it immensely more maintainable than a whole architecture + framework.<p>The HN code is meant to be understood as a self-contained piece, and that's contextually very different from most code out there.
              </p><div>        <p>
                      <u><a href="reply?id=17917902&goto=item%3Fid%3D17915560%2317917902" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17918206"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  &gt; Nonsense. Maintainability almost always matters.<p>The last three large corporations I worked for never cared about maintainability because the application or portal would only be in use for maybe a year or 18 months before a complete rewrite or total redesign.</p><p>All of the recent projects I've been on take the same approach. Get it stood up, make it look pretty and release it. Because agile development makes business owners believe it only takes a few days to build Rome now, maintainability is never a consideration on any of the projects I've been on. Even senior devs are saying, "It's pretty hacky to get this to work, but it works" is a common troupe on our teams. I agree maintainability should be important, but on the agile projects I've been on, nobody cares about it.</p><p>To some degree I think executives do it on purpose so they can create more work for themselves in the future. They can pick it apart, ask for a bigger budget, hire more devs and use some shiny new technology to build it over again. Rinse, repeat.
              </p><div>        <p>
                      <u><a href="reply?id=17918206&goto=item%3Fid%3D17915560%2317918206" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17918691"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  &gt; The last three large corporations I worked for never cared about maintainability because the application or portal would only be in use for maybe a year or 18 months before a complete rewrite or total redesign.<p>The first significant web app that I wrote had a similar approach. I was a new developer, but I had a good idea and they hired a manager and a couple of other developers to flesh it out. No need to hire a senior dev, because it was just a POC. We weren't even part of IT, so anything we built would <i>of course</i> only be in use for a few months before IT would allocated "real" developers to rewrite it.</p><p>Four years after I left that job, I got a call one day that the site was down and they couldn't fix it. After ten minutes on the phone with a former colleague reading me the logs out loud while I read through an old copy of the code that I (thankfully) still had on an archived drive, it turns out that the LDAP server's address had changed. We updated that and it came back.</p><p>Out of curiosity, I had them run `uptime` on that box. It had been up for <i>six years</i> - the two years I was there, and the four since I'd left. Not only had the application continued to function and be used... the box it was running on hadn't been updated restarted since it was built. It hadn't gotten updates since I'd left either.</p><p>The point of this story is simple: there is no such thing as code where maintainability doesn't matter, because there is no such thing as "temporary" code. Code can get retired or refactored away, sure, but there is absolutely no way to tell ahead of time if any given code snippet falls into that category.
              </p><div>        <p>
                      <u><a href="reply?id=17918691&goto=item%3Fid%3D17915560%2317918691" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916372"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  &gt;If you have a day job that isn't primarily writing code, and/or you are likely to be the only person ever working on that code, who cares if it's not up to the standard that people around here seem to expect of every project?<p>Future you that has to decipher the code. Why make it hard on yourself? Software is a living thing eventually a decision will need to be made about it and without understanding what it does it's easier to make suboptimal assumptions.
              </p><div>        <p>
                      <u><a href="reply?id=17916372&goto=item%3Fid%3D17915560%2317916372" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916619"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Eh, it's only 150 lines of simple functions without external dependencies. It's simple enough to understand and modify on the spot. As long as these are not expected to grow significantly in the future, I don't see why it'd be making it hard on yourself (and if it does grow, then it can always be refactored).
              <div>        <p>
                      <u><a href="reply?id=17916619&goto=item%3Fid%3D17915560%2317916619" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916945"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  This 100x times. There is <i>very little code there</i>. Any effort in trying to bring it up to modern webdev standards would likely make the code expand significantly, and that's not even counting the complexity of the deployment pipeline. This here, it's just 150 lines of plain code. It's not hard to work with something like this.
              <div>        <p>
                      <u><a href="reply?id=17916945&goto=item%3Fid%3D17915560%2317916945" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917811"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  I'm not saying a rewrite is necessary at all, but refactoring this code to use more modern standards would NOT increase the line count at all, my guess it it might cut it by 15%+ in total size if you leveraged the beautiful builtin functions. Compare these:<pre><code>    function addClass (el, cl) { if (el) { var a = el.className.split(' '); if (!afind(cl, a)) { a.unshift(cl); el.className = a.join(' ')}} }

</code></pre>
Could turn into something like this:<pre><code>  const addClass = (el, cl) =&gt; el.classList.add(cl)
</code></pre>
Not only is is shorter, but it's more readable too!
              <div>        <p>
                      <u><a href="reply?id=17917811&goto=item%3Fid%3D17915560%2317917811" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17918356"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="200" height="1" /></td><td></td><td><div>
                  &gt; <i>Not only is is shorter, but it's more readable too!</i><p>And won't work on IE. Not just because of el.classList, but also because of the arrow notation. So by doing this change, you either have to ditch one of still used browsers, or introduce a stupidly complex transpilation chain into the mix.
              </p><div>        <p>
                      <u><a href="reply?id=17918356&goto=item%3Fid%3D17915560%2317918356" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17918049"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="200" height="1" /></td><td></td><td><div>
                  el.classList isn't supported by IE &lt; 10
              <div>        <p>
                      <u><a href="reply?id=17918049&goto=item%3Fid%3D17915560%2317918049" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17918090"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="240" height="1" /></td><td></td><td><div>
                  And is it accurate to describe IE &lt; 10 as "more modern"?
              <div>        <p>
                      <u><a href="reply?id=17918090&goto=item%3Fid%3D17915560%2317918090" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17918651"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="280" height="1" /></td><td></td><td><div>
                  It isn't, and I don't think I have.<p>My point was that using a "more modern standard" would break hn for people using legacy browsers.
              </p></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17917040"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  The code is entirely self-contained. That's what makes it easier for future-you to understand and decipher. Dependencies won't have gone out of date, library versions won't have moved on, APIs won't have disappeared, etc.
              <div>        <p>
                      <u><a href="reply?id=17917040&goto=item%3Fid%3D17915560%2317917040" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916455"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  &gt; Future you that has to decipher the code. Why make it hard on yourself? Software is a living thing eventually a decision will need to be made about it and without understanding what it does it's easier to make suboptimal assumptions.<p>To the defense of the title, in my experience, whenever label "hacker" was used on programmer or code, it meant "difficult to read, full of hard to maintain shortcuts and tricks" kind of code. Really always, I don't ever remember it to be used in any other sense.
              </p><div>        <p>
                      <u><a href="reply?id=17916455&goto=item%3Fid%3D17915560%2317916455" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        
        <tr id="17917244"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  The code is readable. There is no problem.<p>&gt; As long as the code works, anything else is just gravy.</p><p>How did you end up with this opinion? That's an unpopular opinion even when considering the qualifiers you've listed in the paragraph above.
              </p><div>        <p>
                      <u><a href="reply?id=17917244&goto=item%3Fid%3D17915560%2317917244" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916621"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  &gt; <i>As long as the code works, anything else is just gravy</i><p>I'll try to incorporate this in my next job interview :)
              </p><div>        <p>
                      <u><a href="reply?id=17916621&goto=item%3Fid%3D17915560%2317916621" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17916386"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Um, is this supposed to be a criticism?<p>Because this is MUCH better than sites loading megabytes worth of scripts to do nothing more than render text, have dozens of floating elements everywhere, auto playing videos that follow you, "use our app" buttons, etc...</p><p>JS is the assembly of the web, do you also criticize games written in assembly?
              </p><div>        <p>
                      <u><a href="reply?id=17916386&goto=item%3Fid%3D17915560%2317916386" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916854"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I don't know if the author is experienced or not. But something I do know, is that the more experience I get, the more I fear dependencies and the more I value simplicity.<p>HN is a simple website. I'm glad that they decided to keep the code simple as well. I love the fact that the code almost fits in a single screen. Zero dependencies. You can understand the entire code in a few minutes.</p><p>I think new developers greatly underestimate the negative impact of dependencies. Today, something like create-react-app downloads hundreds of megabytes of dependencies. Libraries, transpilers, compiler extensions, and various tooling. Of course all those things come with many advantages, but what most people miss is the huge cost of all that. The increased complexity introduced by dependencies. The unnecessary bloat.</p><p>Sure, the way you name your variables have an impact on readability. But it's nothing compared to adding thousands of dependencies to your project.
              </p><div>        <p>
                      <u><a href="reply?id=17916854&goto=item%3Fid%3D17915560%2317916854" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916611"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  macOS just notified me that one tab in Safari was using so much memory it was threatening performance of my laptop. The website in question? <a href="https://idioms.thefreedictionary.com/" target="_blank">https://idioms.thefreedictionary.com/</a> It was close to 2Gb RAM usage. Bunch of ad-tracking stuff, I assume, as Firefox and its related processes seem to be using less than 1250mb with 6 tabs open, including the site mentioned in 2 tabs. My firefox has uBlock origin installed.<p>Seemed related to the second paragraph in your comment
              </p><div>        <p>
                      <u><a href="reply?id=17916611&goto=item%3Fid%3D17915560%2317916611" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917339"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Last week my bandwidth grounded to a halt which is usually the result of someone uploading on my network.<p>I went to my girlfriend's computer to see if she was syncing with Dropbox or something. Nope. She quit all of her applications just to be sure. Except for a single browser tab opened to a recipe for pita bread.</p><p>Yep, turned out that a recipe for pita bread was saturating our router because what looked to be buggy error-handling for ad-related network code. I think her ad-blocker only partially maimed it, so it went apeshit.
              </p><div>        <p>
                      <u><a href="reply?id=17917339&goto=item%3Fid%3D17915560%2317917339" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        
    
              <tr id="17916521"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  &gt;JS is the assembly of the web, do you also criticize games written in assembly?<p>No it isn't, any more than C++ is the assembly of your operating system.</p><p>Assembly has the terseness that it does because of constraints that javascript doesn't have -- this javascript looks the way it does because the author wanted it to look like lisp code, not because it has to.
              </p><div>        <p>
                      <u><a href="reply?id=17916521&goto=item%3Fid%3D17915560%2317916521" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917820"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  At least it's the lowest level programming language for browsers I know. So perhaps I should have said "machine language of the web" because assembly isn't the lowest level :)
              <div>        <p>
                      <u><a href="reply?id=17917820&goto=item%3Fid%3D17915560%2317917820" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17916626"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  &gt; JS is the assembly of the web, do you also criticize games written in assembly?<p>If it's a typical platformer from 1980s, now. If it's a modern game with a modern game's complexity, it would never be finished in assembly anyway.
              </p><div>        <p>
                      <u><a href="reply?id=17916626&goto=item%3Fid%3D17915560%2317916626" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917014"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Then again, clones of games from 1980s in modern engines are considered toy projects. The equivalent on the web is considered standard practice.
              <div>        <p>
                      <u><a href="reply?id=17917014&goto=item%3Fid%3D17915560%2317917014" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17916851"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  &gt; JS is the assembly of the web, do you also criticize games written in assembly?<div>        <p>
                      <u><a href="reply?id=17916851&goto=item%3Fid%3D17915560%2317916851" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17918639"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I'm not sure if this was linked fatously, but this is actually pretty good JS.<p>- All functions</p><p>- The functions are simple and decomposed into smaller functions</p><p>- No usages of "this" (except one necessary one in an event handler)</p><p>- No ham fisted attempts at doing OOP with JS</p><p>Only complaints really are naming and code style is overly compact which would potentially make it harder to understand, but in this context I think that is ok. There is nothing overly complex going on here. The code seems reasonably easy to understand.</p><p>If there are criticism I'd like to hear them.
              </p><div>        <p>
                      <u><a href="reply?id=17918639&goto=item%3Fid%3D17915560%2317918639" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17918016"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I feel like this was written in this particular style assuming it was not going to be minified. I think it's ok to use this style if only maintained by a couple of people, or for a small project like this. I do like it's conciseness, but I don't feel the title is appropriate.
              <div>        <p>
                      <u><a href="reply?id=17918016&goto=item%3Fid%3D17915560%2317918016" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17916086"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  The authors is quite lazy or cannot type fast enough, so he has to create all those cryptic abbreviations: `rks` for `ranks`, `unv` for `unvote`, etc. Which makes it really hard to read.<p>But it's especially the inconsistent use of camelcase in function names than makes me think it's pretty amateurish.
              </p><div>        <p>
                      <u><a href="reply?id=17916086&goto=item%3Fid%3D17915560%2317916086" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916199"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Hard to read?  The sum total of the script fits on 2-3 pages at most, no single function exceeds about 10 lines, if you have trouble reading and reasoning about that code then something is wrong.
              <div>        <p>
                      <u><a href="reply?id=17916199&goto=item%3Fid%3D17915560%2317916199" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916565"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  functions will not be any line longer by writing ranks instead of rks, but it will greatly improve readability.<p>You can have the exact same code wihtout abbreviations, and I can assure you that it will still be 2-3 pages long, with very short functions.
              </p><div>        <p>
                      <u><a href="reply?id=17916565&goto=item%3Fid%3D17915560%2317916565" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17917458"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Yeah, I also like to minify the code before reading. It makes up to 5 times less code and it's fun to guess which letter stands for which function.
              <div>        <p>
                      <u><a href="reply?id=17917458&goto=item%3Fid%3D17915560%2317917458" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17916130"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Yeah, just looks like a grease monkey script I would have banged out a decade ago in about an hour. Nothing wrong with that. It's far more interesting how much people are reading into this code haha. It was clearly not written to be read by us today IMHO.
              <div>        <p>
                      <u><a href="reply?id=17916130&goto=item%3Fid%3D17915560%2317916130" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17918282"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  A real amateur would have figured out how to write everything in a single function.
              <div>        <p>
                      <u><a href="reply?id=17918282&goto=item%3Fid%3D17915560%2317918282" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17918350"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  This is the only part that I thought could be significantly improved for the use case they have here.  But to each his own.
              <div>        <p>
                      <u><a href="reply?id=17918350&goto=item%3Fid%3D17915560%2317918350" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916572"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  &gt;But it's especially the inconsistent use of camelcase in function names than makes me think it's pretty amateurish.<p>Despite its size, this .js file has been modified throughout many many years probably by various authors.
              </p><div>        <p>
                      <u><a href="reply?id=17916572&goto=item%3Fid%3D17915560%2317916572" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916374"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Maybe the author used to write C
              <div>        <p>
                      <u><a href="reply?id=17916374&goto=item%3Fid%3D17915560%2317916374" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17915780"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Not all that impressive, considering non-consistent code style and the like.<p>Also not a fan of unnecessarily cryptic variable names.
              </p><div>        <p>
                      <u><a href="reply?id=17915780&goto=item%3Fid%3D17915560%2317915780" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        
                <tr id="17915734"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  This is neat (how the up/downvote onclick handler sends the info to the server).<pre><code>    new Image().src = el.href;
</code></pre>
Where href looks like this:<pre><code>    vote?id=xxxxxxxx&how=up&auth=yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy&goto=item%3Fid%3Dzzzzzzzz#wwwwwwww</code></pre>
              <div>        <p>
                      <u><a href="reply?id=17915734&goto=item%3Fid%3D17915560%2317915734" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916282"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Is this a GET request? 
What if my browser wants to peek ahead on some links?
              <div>        <p>
                      <u><a href="reply?id=17916282&goto=item%3Fid%3D17915560%2317916282" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916894"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  If the Image is being created dynamically there won't be anything for browser to peek ahead at.<p>Edit: I'd be more worried about repeated calls - but presumably the service being called is idempotent.
              </p><div>        <p>
                      <u><a href="reply?id=17916894&goto=item%3Fid%3D17915560%2317916894" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        
      <tr id="17916682"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  This would indeed be problematic :-) The up/down vote buttons are plain anchor elements.
              <div>        <p>
                      <u><a href="reply?id=17916682&goto=item%3Fid%3D17915560%2317916682" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17917418"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Image makes the HTTP request without appending the Image to the DOM? TIL
              <div>        <p>
                      <u><a href="reply?id=17917418&goto=item%3Fid%3D17915560%2317917418" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917516"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  That's how most tracking scripts operate...
              <div>        <p>
                      <u><a href="reply?id=17917516&goto=item%3Fid%3D17915560%2317917516" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17915823"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Maybe it's neat but this is not how anyone would write it today. This is the legacy code still left from the time before ajax was invented.
              <div>        <p>
                      <u><a href="reply?id=17915823&goto=item%3Fid%3D17915560%2317915823" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915872"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Hacker News was launched 2007.<p>XMLHttpRequest has been around for about 7 years then and using it was called Ajax for about 2 years already.
              </p><div>        <p>
                      <u><a href="reply?id=17915872&goto=item%3Fid%3D17915560%2317915872" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915924"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  Not to mention the "ajax" function in the script...
              <div>        <p>
                      <u><a href="reply?id=17915924&goto=item%3Fid%3D17915560%2317915924" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17916007"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  It is strange. I wonder if it's an approach that lets duplicate vote attempts get automatically responded to by the webserver cache rather than passing through to be detected computationally at the application server level, which would also involve a DB call.<p>Conceivably this would make the architecture more robust against vote-spamming attacks, and the approach would also provide an enhanced version of this benefit if using an external caching reverse-proxy service like CloudFlare or similar (though I  believe HN does not use CloudFlare).</p><p>This is complete supposition on my part.
              </p><div>        <p>
                      <u><a href="reply?id=17916007&goto=item%3Fid%3D17915560%2317916007" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17915944"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  There's also an XMLHttpRequest wrapper for when they care about the response.<p>This is used for write-only GET requests (with graceful fallback when JS is disabled since those are plain anchor elements).
              </p><div>        <p>
                      <u><a href="reply?id=17915944&goto=item%3Fid%3D17915560%2317915944" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17915868"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Probably. I wonder though if they are trying not to use any libraries and Image was just easier than xhr.
              <div>        <p>
                      <u><a href="reply?id=17915868&goto=item%3Fid%3D17915560%2317915868" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                  <tr id="17916339"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  It works... every criticism beyond that is just an argument about taste, although personally I think it's unnecessarily terse.<p>I've written uglier code and gotten paid for it.  ¯\_(ツ)_/¯
              </p><div>        <p>
                      <u><a href="reply?id=17916339&goto=item%3Fid%3D17915560%2317916339" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917346"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Not necessarily. Sure, all code has to work, but unless you're going to ship a product and then never, ever return to it, it has to be maintainable as well.<p>There are a few arguments in this thread about poor maintainability of this code, when coupled to the HTML it affects (which always must be considered, otherwise this code is pointless), and I tend to agree with them.</p><p>Personally, I wouldn't mind some less terse names and some more semantic groupings of HTML nodes.</p><p>Thankfully, it <i>is</i> simple. I'm pretty sure doing that would be the task of an afternoon, though I would definitely want to accomplish that before trying to change anything else on the page.
              </p><div>        <p>
                      <u><a href="reply?id=17917346&goto=item%3Fid%3D17915560%2317917346" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916729"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  And no doubt I've written single methods/functions that where uglier.
              <div>        <p>
                      <u><a href="reply?id=17916729&goto=item%3Fid%3D17915560%2317916729" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17915670"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  That might be one of the most readable pieces of code that I've ever read.
              <div>        <p>
                      <u><a href="reply?id=17915670&goto=item%3Fid%3D17915560%2317915670" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915773"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Really? Plenty of needlessly abbreviated function names IMO. At a quick glance is it immediately obvious what posf or arem are without looking into the context in which they're being used?
Don't get me wrong it's a nice piece of code but super-readable it isn't.
              <div>        <p>
                      <u><a href="reply?id=17915773&goto=item%3Fid%3D17915560%2317915773" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915800"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Well, I disagree. It is abbreviated, but since the whole file is self-contained and the definitions are put at the beginning, there is enough information to infer the function's semantics without being excessively specific. I think well defined organization of abstractions is an often overlooked but surprisingly effective way to achieve readability
              <div>        <p>
                      <u><a href="reply?id=17915800&goto=item%3Fid%3D17915560%2317915800" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915929"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  &gt; there is enough information to infer the function's semantics without being excessively specific<p>You mean you can just read the function definition to see what it does?
              </p><div>        <p>
                      <u><a href="reply?id=17915929&goto=item%3Fid%3D17915560%2317915929" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916006"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  He doesn't like being excessively specific with his writing I guess. Plus it makes you sound more like an engineer when you speak like this.
              <div>        <p>
                      <u><a href="reply?id=17916006&goto=item%3Fid%3D17915560%2317916006" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
          <tr id="17916063"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  It's also a piece of code that hasn't been rewritten to fit whatever buzz is the buzz today. I wish more of the world was written with code that need not be rewritten every five years.
              <div>        <p>
                      <u><a href="reply?id=17916063&goto=item%3Fid%3D17915560%2317916063" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17915918"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I think the main reason this is somewhat readable is because there's hardly any code. Which is fine.
              <div>        <p>
                      <u><a href="reply?id=17915918&goto=item%3Fid%3D17915560%2317915918" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916997"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  The supreme art of war is to subdue the enemy without fighting.<p>-sun tzu
              </p><div>        <p>
                      <u><a href="reply?id=17916997&goto=item%3Fid%3D17915560%2317916997" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
            <tr id="17915916"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  It seems some of the one-liners are simply renaming JavaScript built-ins like forEach to aeach and slice to acut. Maybe this is to make it look more like the Lisp backend? But taken on its own it does not really improve readability.
              <div>        <p>
                      <u><a href="reply?id=17915916&goto=item%3Fid%3D17915560%2317915916" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916244"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  No, it is because some array-like objects like node lists actually aren't Arrays and don't have those functions in their prototype.
              <div>        <p>
                      <u><a href="reply?id=17916244&goto=item%3Fid%3D17915560%2317916244" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916742"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  this is why I usually go for something like const $ = (el) =&gt; [...document.querySelectorAll(el)]
              <div>        <p>
                      <u><a href="reply?id=17916742&goto=item%3Fid%3D17915560%2317916742" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915787"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Really? It has horrendous naming and it isn't even using es6<p>function byClass (el, cl) { return el ? el.getElementsByClassName(cl) : [] }</p><p>const byClass = (el, cl) =&gt; el ? el.getElementsByClassName(cl) : []
              </p><div>        <p>
                      <u><a href="reply?id=17915787&goto=item%3Fid%3D17915560%2317915787" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915905"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Your code is not more readable, it is just shorter.<p>In fact, using the online babel transpiler, it transpiles the es6 version you provided precisely into hn's version:</p><p><a href="https://bit.ly/2MPmjK7" target="_blank">https://bit.ly/2MPmjK7</a></p><p>To use es6 to achieve what this tiny piece of javascript could already do, you probably need to introduce some tremendous dependency like babel just to be compatible with all kinds of weird browsers out there. What does es6 give here? Not very much in my opinion.
              </p><div>        <p>
                      <u><a href="reply?id=17915905&goto=item%3Fid%3D17915560%2317915905" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917334"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  It's 2018. Unless you're using Internet Explorer arrow functions are supported natively.
              <div>        <p>
                      <u><a href="reply?id=17917334&goto=item%3Fid%3D17915560%2317917334" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917468"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  And I bet there are some people here using IE.  And old  browsers.
              <div>        <p>
                      <u><a href="reply?id=17917468&goto=item%3Fid%3D17915560%2317917468" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17918137"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="200" height="1" /></td><td></td><td><div>
                  I would REALLY love to see the browser usage statistics for HN :)
              <div>        <p>
                      <u><a href="reply?id=17918137&goto=item%3Fid%3D17915560%2317918137" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
          <tr id="17916267"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  You're still returning a live HTMLCollection or an Array.<p>It's still bad code. Using newer syntax to do the same thing didn't actually improve anything.
              </p><div>        <p>
                      <u><a href="reply?id=17916267&goto=item%3Fid%3D17915560%2317916267" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17915825"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  How does es6 improve readability in this case? It barely removes `{}` and replaces very clear word `function` with `const` that in most languages is associated with constant values, not with functions
              <div>        <p>
                      <u><a href="reply?id=17915825&goto=item%3Fid%3D17915560%2317915825" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915874"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  It removes the brackets and the return keyword, const is in fact a constant but this not ES6 it is just doing a function expression instead a function declaration (you create a const variable and assign an anonymous function to it instead of using the keyword 'function')<p>This is used for readability and to avoid hoisting that can be confusing.
              </p><div>        <p>
                      <u><a href="reply?id=17915874&goto=item%3Fid%3D17915560%2317915874" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916233"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  Given that brackets and the return keyword (and the function keyword!) are core parts of functions (a scope and a value to return to the caller), I would argue that removing these key parts of a function makes it harder for someone not familiar with ES6 to see that it is a function.<p>This reminds me of Ruby's return-the-last-evaluated-thing-in-a-function semantics (which sadly Rust copied). Having to type one extra word is not such a burden that you should add cognitive overhead each time someone not intimately familiar with the language has to read your code.</p><p>If the argument is that only ES6 experts should only ever have to read or write ES6 code, then I would argue that any syntax argument is pointless because only experts can comment on a languages syntax -- and thus COBOL objectively has the best syntax and you cannot disagree unless you are a COBOL expert.
              </p><div>        <p>
                      <u><a href="reply?id=17916233&goto=item%3Fid%3D17915560%2317916233" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916850"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="200" height="1" /></td><td></td><td><div>
                  It does seem strange if you think of it as “return the last evaluated thing from the function.” But that’s not the semantic; the semantic is “everything is an expression and expressions evaluate to a value.” Removing this behavior would make these languages less consistent.<p>(And yes, in both Ruby and Rust not literally everything is an expression, but almost everything is.)
              </p><div>        <p>
                      <u><a href="reply?id=17916850&goto=item%3Fid%3D17915560%2317916850" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917060"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="240" height="1" /></td><td></td><td><div>
                  I agree that because of common uses of things like match in Rust it makes it consistent to also do it for functions. I don't agree that the reason why it's consistent is because a function body is an expression (though of course you have more expertise than me on this one -- and Rust does actually treat scopes much more strictly than most other languages so you could argue every scope has the smell of a function call associated with it).
              <div>        <p>
                      <u><a href="reply?id=17917060&goto=item%3Fid%3D17915560%2317917060" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917507"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="280" height="1" /></td><td></td><td><div>
                  Here's the citation: <a href="https://doc.rust-lang.org/reference/items/functions.html" target="_blank">https://doc.rust-lang.org/reference/items/functions.html</a><p>&gt; A function consists of a block, along with a name and a set of parameters.</p><p><a href="https://doc.rust-lang.org/reference/expressions/block-expr.html" target="_blank">https://doc.rust-lang.org/reference/expressions/block-expr.h...</a></p><p>&gt; Blocks are always value expressions and evaluate the last expression in value expression context.
              </p><div>        <p>
                      <u><a href="reply?id=17917507&goto=item%3Fid%3D17915560%2317917507" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916783"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="200" height="1" /></td><td></td><td><div>
                  &gt; This reminds me of Ruby's return-the-last-evaluated-thing-in-a-function semantics (which sadly Rust copied). Having to type one extra word is not such a burden that you should add cognitive overhead each time someone not intimately familiar with the language has to read your code.<p>I think the concept of returning by default is fundamental enough that doing so or not is mostly a matter of what you're used to. If I'd started out with Elixir or Ruby I'd probably find it strange that I have to manually return stuff from a function.</p><p>Furthermore, at this point ES6 is common enough that knowing at least some of the core additions (among them arrow functions with their implicit return) should be something any front-ender knows.
              </p><div>        <p>
                      <u><a href="reply?id=17916783&goto=item%3Fid%3D17915560%2317916783" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
          <tr id="17915842"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  The es6 syntax is LESS readable. It's less declarative. Just quicker to type if you don't have a nice editor setup.<p>My issue with this method is the name more than anything. I would also guess if it's even needed - probably bad application logic is requiring that ternary statement but didn't read it yet.</p><p>Ideal method name is already given - getEmementsByClassName... Really should just have a utility to default return types.
              </p><div>        <p>
                      <u><a href="reply?id=17915842&goto=item%3Fid%3D17915560%2317915842" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916142"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Probably not worth setting up a babel transpiler for that small amount of JS tbh<p>Makes supporting older browsers a lot easier
              </p><div>        <p>
                      <u><a href="reply?id=17916142&goto=item%3Fid%3D17915560%2317916142" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17915835"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  It was almost certainly written long before ES6 was widely supported.
              <div>        <p>
                      <u><a href="reply?id=17915835&goto=item%3Fid%3D17915560%2317915835" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                  <tr id="17915789"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  In most places this code would never pass a code review and would be considered plain unacceptable. I guess I'd prefer some place where this code style is the norm.
              <div>        <p>
                      <u><a href="reply?id=17915789&goto=item%3Fid%3D17915560%2317915789" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916000"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Go into academia. You'll receive <i>no</i> code review, and you'll deal with pretty bad code, but you'll be free to write however you want as long as it works and can be published.
              <div>        <p>
                      <u><a href="reply?id=17916000&goto=item%3Fid%3D17915560%2317916000" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916024"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  "pretty bad code"? That's an euphemism.
              <div>        <p>
                      <u><a href="reply?id=17916024&goto=item%3Fid%3D17915560%2317916024" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        
        <tr id="17916192"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  So you would like to work a place with no code review? You will be happy to hear that many many workplaces have no code review at all.
              <div>        <p>
                      <u><a href="reply?id=17916192&goto=item%3Fid%3D17915560%2317916192" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916613"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  &gt; So you would like to work a place with no code review?<p>How does this follow from my statement?
              </p><div>        <p>
                      <u><a href="reply?id=17916613&goto=item%3Fid%3D17915560%2317916613" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                  <tr id="17915772"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Hacker News also works pretty well without JavaScript at all, which is really nice. Not something that I use often, but it comes in handy when you want to post a comment from your potato device that can't handle the modern web.
              <div>        <p>
                      <u><a href="reply?id=17915772&goto=item%3Fid%3D17915560%2317915772" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917428"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I usually read HN using w3m.  It's entirely usable with no javascript.
              <div>        <p>
                      <u><a href="reply?id=17917428&goto=item%3Fid%3D17915560%2317917428" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916434"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I once managed to open HN on a Nokia 3110 classic. Scrolling hanged and eventually rebooted the phone, but nevertheless the signature "HN orange" could be seen.
              <div>        <p>
                      <u><a href="reply?id=17916434&goto=item%3Fid%3D17915560%2317916434" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17917650"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Write it with all the modern "proper" approaches, and good luck even just recompiling it in 10 years. While this code - however imperfect - remains just as maintainable today as it was when originally written (which is probably more than 10 years ago).
              <div>        <p>
                      <u><a href="reply?id=17917650&goto=item%3Fid%3D17915560%2317917650" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917872"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  That's true if you're talking about using React, Vue, etc. but do you really think ES5 JavaScript is more likely to be supported in the future than ES6?
              <div>        <p>
                      <u><a href="reply?id=17917872&goto=item%3Fid%3D17915560%2317917872" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917936"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  I'm talking about NPM modules and the build toolchain (which consists of even more NPM modules). This stuff goes stale very quickly (at the 10-year scale). It's good for a project that is kept continuously alive (i.e. when there is a team of developers that is continuously making changes to the project), but not when the project sits on a shelf for 10 years and then needs to be modified.
              <div>        <p>
                      <u><a href="reply?id=17917936&goto=item%3Fid%3D17915560%2317917936" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17918368"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  This is a good point, but if you take NPM / Yarn / Bower (RIP) with a grain of salt and secure your codebase against failures, they work nicely as a toolchain.
              <div>        <p>
                      <u><a href="reply?id=17918368&goto=item%3Fid%3D17915560%2317918368" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17918609"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  Do you mean committing node_modules to the Git repository? Unfortunately, that's not a panacea with build tools, because some of them contain non-JS code that is tightly coupled to Node and OS versions.
              <div>        <p>
                      <u><a href="reply?id=17918609&goto=item%3Fid%3D17915560%2317918609" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17918190"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  Right, my point was that this is a subset of modern approaches.
              <div>        <p>
                      <u><a href="reply?id=17918190&goto=item%3Fid%3D17915560%2317918190" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        
                      <tr id="17915899"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  This style is very similar to one which is used by expert C programmers, it seems that most people that write like this have had experience writing parsers and compilers too. It's not their fault that most people don't just think purely in terms of function composition :P
              <div>        <p>
                      <u><a href="reply?id=17915899&goto=item%3Fid%3D17915560%2317915899" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916150"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I'm sure the code works very well for its intended purpose, but I'm kind of wary of the idea that using obscure abbreviations like 'posf', 'arem', 'vis', 'ind' etc. makes you "expert hacker".<p>I don't agree that code should always be designed to be perfectly readable by outsiders. If such abbreviations works for the people who have to maintain the code, more power to them. But I disagree than this is somehow proof of superior skill.
              </p><div>        <p>
                      <u><a href="reply?id=17916150&goto=item%3Fid%3D17915560%2317916150" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17918411"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I think there are several different types of C programmers, and that terseness and functional design are very different.
              <div>        <p>
                      <u><a href="reply?id=17918411&goto=item%3Fid%3D17915560%2317918411" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17916579"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  If there's one take away from this, it is that programmers have widely differing opinions on what constitutes good code.
              <div>        <p>
                      <u><a href="reply?id=17916579&goto=item%3Fid%3D17915560%2317916579" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917091"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  The spectrum seems to span from APL at one extreme, and Enterprise Java/C# at the other. This is closer to the former but still not that extreme (I personally lean toward that direction too, mostly working with Asm and C.)
              <div>        <p>
                      <u><a href="reply?id=17917091&goto=item%3Fid%3D17915560%2317917091" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17916076"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div><pre><code>    function hidestory (ev, el, id) {
      for (var i=0; i &lt; 3; i++) {
</code></pre>
That 3 there is the problem with “simple” JS. It’s tightly coupled to the HTML but they live in completely different places.<p>On a side note this 3 should be at least assigned to a variable with a meaningful name.
              </p><div>        <p>
                      <u><a href="reply?id=17916076&goto=item%3Fid%3D17915560%2317916076" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916812"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Except there isn't any problem here whatsoever. Yes, it's coupled, but it doesn't matter. No, this kind of code doesn't scale. It doesn't <i>have to</i>.<p>The time you spent writing this comment was longer than what it took writing this code. Considering what kind of site this is, that code may work indefinitely. Or, if necessary, someone from the future will need to change that 3 to a 4 at some point. In terms of total cost, it's almost certainly the cheapest solution.
              </p><div>        <p>
                      <u><a href="reply?id=17916812&goto=item%3Fid%3D17915560%2317916812" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917536"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  And how will that someone know what that 3 stands for ? At the minimum a comment above that line would have been nice.
              <div>        <p>
                      <u><a href="reply?id=17917536&goto=item%3Fid%3D17915560%2317917536" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17916091"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  hidestory() is not even used anywhere ; why is it here for? Debugging?
              <div>        <p>
                      <u><a href="reply?id=17916091&goto=item%3Fid%3D17915560%2317916091" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916356"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  It's called by the "hide" link under each story on the top page.
              <div>        <p>
                      <u><a href="reply?id=17916356&goto=item%3Fid%3D17915560%2317916356" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916184"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  It is probably called in an onclick=“” in the HTML somewhere
              <div>        <p>
                      <u><a href="reply?id=17916184&goto=item%3Fid%3D17915560%2317916184" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17916300"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Like JS is never attached to a HTML template ?
              <div>        <p>
                      <u><a href="reply?id=17916300&goto=item%3Fid%3D17915560%2317916300" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    
                  <tr id="17916466"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  There might be more appreciation for "how future maintainers write JavaScript", but that's not cool and it takes a couple of decades more experience.<p>Looks a lot like "read-only" web code I've encountered on projects, where waves of people decided it's easier to work around what's already there than amend it (and that's also how you end up with 20,000 line CSS files).
              </p><div>        <p>
                      <u><a href="reply?id=17916466&goto=item%3Fid%3D17915560%2317916466" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17916049"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Thanks for sharing this nice bit of code; we always learn from examples, we should see more of this.<p>I feel the naming is too short, things are just a little too specifically compact and slightly cryptic ... almost like the author is trying to say something ...</p><p>I've never said this before about code ... but I think that code is 'smug'!</p><p>Like odd facial hair, or one of those valley-specific t-shirts ... the code trying to project how cool it thinks it is!</p><p>That code is 'humble-bragging' ...
              </p><div>        <p>
                      <u><a href="reply?id=17916049&goto=item%3Fid%3D17915560%2317916049" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916082"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Really? It just looks compact and efficient to me.
              <div>        <p>
                      <u><a href="reply?id=17916082&goto=item%3Fid%3D17915560%2317916082" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916162"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  "Compact" (abbreviated) names are negligibly more efficient when machines read them, and they're wildly less efficient when humans read them. Code is read many more times than it's written, so it doesn't make sense to optimize for fewer keystrokes when typing the code.<p>This is especially true with modern IDEs that autocomplete everything.
              </p><div>        <p>
                      <u><a href="reply?id=17916162&goto=item%3Fid%3D17915560%2317916162" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916918"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  &gt; Code is read many more times than it's written, so it doesn't make sense to optimize for fewer keystrokes when typing the code.<p>That's actually probably <i>not</i> the case with JavaScript, so it may indeed make more sense to write it to be more efficient to execute.
              </p><div>        <p>
                      <u><a href="reply?id=17916918&goto=item%3Fid%3D17915560%2317916918" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917483"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="160" height="1" /></td><td></td><td><div>
                  Post-processors do that much better than a human and can also tree-shake. There's no reason for a human to do it.
              <div>        <p>
                      <u><a href="reply?id=17917483&goto=item%3Fid%3D17915560%2317917483" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
          <tr id="17916090"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Exactly, those function names hurt my brain:<p>remClass -&gt; does it hurt to write removeClass ?</p><p>what is vis, ind, posf? I shouldn't have to decipher the function to figure out what its name might mean.</p><p>Hacker? no. 
Smug? yes
              </p><div>        <p>
                      <u><a href="reply?id=17916090&goto=item%3Fid%3D17915560%2317916090" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17917484"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Here's something maybe productive to take away from this kibitzing thread:<p>Consider this code and the range of comments on it while doing (or undergoing) your next non-trivial code review.</p><p>(For one thing, it reminds me that a great value of adopting comprehensive code standards is that it resolves these kinds arguments, letting teams get on with the important stuff.)
              </p><div>        <p>
                      <u><a href="reply?id=17917484&goto=item%3Fid%3D17915560%2317917484" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17917314"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  "var", "function", one explicit "return" at the end of function body, working directly with the DOM? I still do this sometimes and the Angular/React/TypeScript kids look at me like at some alien wizard, while Java/.NET folks still think "it's just a dumb website".
              <div>        <p>
                      <u><a href="reply?id=17917314&goto=item%3Fid%3D17915560%2317917314" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17916890"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  While everyone's freaking out over the code I'm remembering the old code that was only 2 functions[0], which leaves me to believe this code was changed not too long ago. I wish we had a github or something of some of these front-end changes to HN just to see how things change over time. I figure it wouldn't be too much, but still.<p>The original JS was inlined and contained two functions: hide and vote.</p><p>[0] <a href="https://news.ycombinator.com/item?id=11307758" target="_blank">https://news.ycombinator.com/item?id=11307758</a>
              </p><div>        <p>
                      <u><a href="reply?id=17916890&goto=item%3Fid%3D17915560%2317916890" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17918169"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Lol this title is literally a recipe for fighting. That said, I love how they eliminated the need for JQuery with all the functions up top. Super minimalist.
              <div>        <p>
                      <u><a href="reply?id=17918169&goto=item%3Fid%3D17915560%2317918169" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17916475"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  This is very similar to what I'd do for my small projects, I really love the small size and the brevity of it.<p>On the contrary, it's not what I'd do at work for one of our bigger web apps.</p><p>No need to criticize, it does what it's supposed to.
              </p><div>        <p>
                      <u><a href="reply?id=17916475&goto=item%3Fid%3D17915560%2317916475" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17915766"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  The code is very much readable, without suffering from being concise. Love it.
              <div>        <p>
                      <u><a href="reply?id=17915766&goto=item%3Fid%3D17915560%2317915766" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17915688"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div><pre><code>    function onready () {
      recoll();
    }

    document.addEventListener("DOMContentLoaded", onready);
</code></pre>
Just attach recoll() directly. There's no benefit of going via onready().
              <div>        <p>
                      <u><a href="reply?id=17915688&goto=item%3Fid%3D17915560%2317915688" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916276"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  You don't have to make every piece of code 100% tight. onready is actually the kind of function that you very likely want to add more lines to in the future, so why not leave it in? (I'm willing to bet it had more lines at some point in the past.)
              <div>        <p>
                      <u><a href="reply?id=17916276&goto=item%3Fid%3D17915560%2317916276" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916397"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  <i>onready is actually the kind of function that you very likely want to add more lines to in the future, so why not leave it in?</i><p>I'm a fan of writing the code you need when you need it. Adding or leaving things things there 'just in case' leads to code that's harder to reason about in the future because it's full of things that may or may not be used.
              </p><div>        <p>
                      <u><a href="reply?id=17916397&goto=item%3Fid%3D17915560%2317916397" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17915703"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  `recoll(apse)` is a verb. `onready` is an event condition. They are not interchangable. (Though it might be combined into a single line with an anonymous function argument to addEventListener.)
              <div>        <p>
                      <u><a href="reply?id=17915703&goto=item%3Fid%3D17915560%2317915703" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17916023"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Love it. Looks like lisp (can almost tell pg or rtm wrote it?), functions all over. No bloat...
              <div>        <p>
                      <u><a href="reply?id=17916023&goto=item%3Fid%3D17915560%2317916023" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17915898"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div><pre><code>    function aeach (fn, a) { return Array.prototype.forEach.call(a, fn) }
</code></pre>
Does this win anything over using forEach directly?
              <div>        <p>
                      <u><a href="reply?id=17915898&goto=item%3Fid%3D17915560%2317915898" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916073"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  This works with array-like objects which aren't arrays. It's important if you want to support older browsers which don't implement NodeList.forEach(). Well, it's really just for old IE.<p>If you're targeting modern browsers this is no longer an issue, as they all support NodeList.forEach(). It's worth noting that many DOM APIs return live collections, so depending on what you're doing you might want to clone it first. Luckily now with ES2015 you can use Array.from(list) or just [...list].
              </p><div>        <p>
                      <u><a href="reply?id=17916073&goto=item%3Fid%3D17915560%2317916073" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17915925"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  A lot of things like this will  work on both arrays (thta have a .forEach method) and things that behave enough like arrays such that Array.prototype.forEach works for them.<p>The downside of this approach (if you subscribe to the ideology of OO) is that if you make something completely unlike an array internally, like a linked list, you can’t use this function on it. Whereas, if you wrote a .forEach method for it, you could use it interchangeably with arrays anywhere the code calls .forEach.</p><p>Without trying it, I’ll guess that this is used on the arguments magic parameter. It’s notorious for being array-like but not an array.
              </p><div>        <p>
                      <u><a href="reply?id=17915925&goto=item%3Fid%3D17915560%2317915925" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916058"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  DOM functions like getElementsByClassName return a nodelist, which as you say behaves like an array.
              <div>        <p>
                      <u><a href="reply?id=17916058&goto=item%3Fid%3D17915560%2317916058" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17915940"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  This function could be used to iterate over the `arguments` array like object, but I do not think it is used for that purpose here.
              <div>        <p>
                      <u><a href="reply?id=17915940&goto=item%3Fid%3D17915560%2317915940" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915985"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  It's used to iterate over HTMLCollection objects here.
              <div>        <p>
                      <u><a href="reply?id=17915985&goto=item%3Fid%3D17915560%2317915985" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                  <tr id="17917357"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  He/she could have put much of the function in the top under the $() to make a super mini jquery. That's close to what I use with Vue. It's made even easier to write considering I almost never find a need for jquery's default behaviour of running its methods on multiple nodes. 99% of the time in my projects I just need to do something with one node.
              <div>        <p>
                      <u><a href="reply?id=17917357&goto=item%3Fid%3D17915560%2317917357" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917437"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I’ve replaced jQuery on several projects with $ = querySelector, $$ = querySelectorAll (wrapped in Array.from if you need to support IE11 so you can use all of the new array methods which their NodeList implementation didn’t get until Edge), classList and fetch.<p>Beyond the code size savings, I find the newer standard methods are generally easier to understand when scanning code.
              </p><div>        <p>
                      <u><a href="reply?id=17917437&goto=item%3Fid%3D17915560%2317917437" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917546"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  I like what this guy did, talking about native methods. However it's <i>too</i> flexible for me, I prefer to have the most minimal functionality in order to ensure consistency in my code. But maybe that's just me. If the library opens up too many possibilities, then I have both the "problem of choice" when writing code, and also it's more difficult to refactor down the line if you want to change lib. Whereas using your own super simple solution (as long as it's sufficient), you can also do a simple abstract layer when including some vendor API.<p><a href="https://github.com/eorroe/NodeList.js/" target="_blank">https://github.com/eorroe/NodeList.js/</a>
              </p><div>        <p>
                      <u><a href="reply?id=17917546&goto=item%3Fid%3D17915560%2317917546" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917665"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  I've been using this for years – it's not the end of web development but an awful lot of projects don't need more framework than can fit in a tweet:<pre><code>    let $ = (selector, scope=document) =&gt; {
        return scope.querySelector(selector);
    };

    let $$ = (selector, scope=document) =&gt; {
        return Array.from(scope.querySelectorAll(selector));
    };</code></pre>
              <div>        <p>
                      <u><a href="reply?id=17917665&goto=item%3Fid%3D17915560%2317917665" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                    <tr id="17915969"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Looks like pretty average code to me.
              <div>        <p>
                      <u><a href="reply?id=17915969&goto=item%3Fid%3D17915560%2317915969" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17917274"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I thought I was smart...<p>BEFORE</p><p>function vis(el, on) { if (el) { on ? remClass(el, 'nosee') : addClass(el, 'nosee') } }</p><p>AFTER</p><p>function vis(el, on) { if (el) { window[on ? 'remClass' : 'addClass'](el, 'nosee') } }</p><p>...sadly we have to add window when using the square brackets so it's not much shorter. Oh well.
              </p><div>        <p>
                      <u><a href="reply?id=17917274&goto=item%3Fid%3D17915560%2317917274" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917319"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Why not:<p>function vis(el, on) { if (el) { (on ? remClass : addClass)(el, 'nosee') } }</p><div>        <p>
                      <u><a href="reply?id=17917319&goto=item%3Fid%3D17915560%2317917319" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917377"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Ahh thanks! I forgot about that. I'm guessing I didn't think about it because I'm used to the following pattern ,which is actually useful from time to time in my projects. And typically it happens in an object/class:<pre><code>  this[expr ? 'method1' : 'method2'](args)
</code></pre>
So I have to add "this" as the methods are not global. Now if I overlooked something again I'm definitely getting rusty :)
              <div>        <p>
                      <u><a href="reply?id=17917377&goto=item%3Fid%3D17915560%2317917377" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                  <tr id="17918192"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  "True Hackers" can write LISP in any language?
              <div>        <p>
                      <u><a href="reply?id=17918192&goto=item%3Fid%3D17915560%2317918192" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17916138"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  This code would be a bit shorter and simpler if it dropped support for old browsers (specifically, Internet Explorer).<p>Some examples:</p><p>The functions hasClass, addClass, and remClass could be replaced by Element.classList [0].</p><p>Another one is remEl, which can be replaced with a direct call to ChildNode.remove() [1].</p><p>I was going to give more examples, but I don't feel like rewriting the whole script.</p><p>[0] <a href="https://developer.mozilla.org/en-US/docs/Web/API/Element/classList" target="_blank">https://developer.mozilla.org/en-US/docs/Web/API/Element/cla...</a></p><p>[1] <a href="https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/remove" target="_blank">https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/r...</a>
              </p><div>        <p>
                      <u><a href="reply?id=17916138&goto=item%3Fid%3D17915560%2317916138" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916445"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Why should anyone invest lifetime to remove compatibility from a perfectly working application? Just to prove that not everyone is using an evergreen browser?
              <div>        <p>
                      <u><a href="reply?id=17916445&goto=item%3Fid%3D17915560%2317916445" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17918039"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  we are way overdue for a source code and architecture evolution history here. the way this started as a toy and exploded without any noticeable performance problems shpuld be a good case study.
              <div>        <p>
                      <u><a href="reply?id=17918039&goto=item%3Fid%3D17915560%2317918039" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17915778"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  To me this looks more like transpiler output ...
              <div>        <p>
                      <u><a href="reply?id=17915778&goto=item%3Fid%3D17915560%2317915778" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915952"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  It would if the variable names were all a,b,c. But they're not, they are almost Polish Notation. There's a all right, but fn, cl, tag for callbacks classes and tags. Also n and m for integers in a range and x for iterable integers.<p>This is the work of someone with a ton of experience. You take 10 minutes to look at the code and understand it, then you are groking complex ideas and operations quickly. I'd love to work with whoever wrote that code.
              </p><div>        <p>
                      <u><a href="reply?id=17915952&goto=item%3Fid%3D17915560%2317915952" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17916716"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Criticisms and bizarre fawning over beauty that a couple of people have made aside, the one thing that bugs me the most is the inconsistent usage of ;
              <div>        <p>
                      <u><a href="reply?id=17916716&goto=item%3Fid%3D17915560%2317916716" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917581"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  To my eyes semicolons are like comments in JS code which indicate "this has been linted for publication". But this &gt; (one); (occasion) where a semicolon can have meaning in JS leaps out of the screen - even easier if they are not blanketed everywhere. The incomplete blanketing in this code is very casual. I see it no more than an invitation to hand-lint what I want to touch.
              <div>        <p>
                      <u><a href="reply?id=17917581&goto=item%3Fid%3D17915560%2317917581" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17917624"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I dunno. Is posf really better than indexOf?  Why not use more conventional names for the underscore-ish functions they made?
              <div>        <p>
                      <u><a href="reply?id=17917624&goto=item%3Fid%3D17915560%2317917624" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17916655"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I can eventually see this coming up on SO asking how to, "make this work. I copied it from the internet."<p>It will be tagged <i>javascript</i> and <i>jquery</i>. =(
              </p><div>        <p>
                      <u><a href="reply?id=17916655&goto=item%3Fid%3D17915560%2317916655" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17915890"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  &gt; function addClass (el, cl) { if (el) { var a = el.className.split(' '); if (!afind(cl, a)) { a.unshift(cl); el.className = a.join(' ')}} }<p>Why does it use `unshift` rather than `push` ?</p><p>The only reason I can think of is that the last class added will be faster to remove when iterating over the array...
              </p><div>        <p>
                      <u><a href="reply?id=17915890&goto=item%3Fid%3D17915560%2317915890" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17917020"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Yep, that's about how much JS your site should contain if you're a sane person.
              <div>        <p>
                      <u><a href="reply?id=17917020&goto=item%3Fid%3D17915560%2317917020" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17915644"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  ...for a site as simple as hn<div>        <p>
                      <u><a href="reply?id=17915644&goto=item%3Fid%3D17915560%2317915644" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915676"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Most bloated sites don't even have an excuse to be more complicated than this.
              <div>        <p>
                      <u><a href="reply?id=17915676&goto=item%3Fid%3D17915560%2317915676" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        
      <tr id="17915660"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  True
Because hackers need much more code lines than those.
              <div>        <p>
                      <u><a href="reply?id=17915660&goto=item%3Fid%3D17915560%2317915660" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17916938"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Seriously though... do you guys declare variables with var or let?  I thought let was the new standard for scoping reasons.  I'm not trying to start a holy war, I'm just a junior looking to learn.
              <div>        <p>
                      <u><a href="reply?id=17916938&goto=item%3Fid%3D17915560%2317916938" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917053"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  let and const are good practice in code that will be transpiled, or in Node.js, but they're newish features that don't have 100% browser support yet, so they shouldn't be used if your code has to run directly in a browser.<p><a href="https://caniuse.com/#feat=let" target="_blank">https://caniuse.com/#feat=let</a>
              </p><div>        <p>
                      <u><a href="reply?id=17917053&goto=item%3Fid%3D17915560%2317917053" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17917103"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  var is maximally compatible with older browsers. let and const are more tightly scoped, and that can help you write more maintainable code.<p>I think maintainability was not a first class concern in the writing of this script (consider the terse naming of variables), but it doesn't really matter; it's short, and you can understand it all because there's not all that much to understand. It does the job, and works everywhere.
              </p><div>        <p>
                      <u><a href="reply?id=17917103&goto=item%3Fid%3D17915560%2317917103" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17917524"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  const. I always use const and if I need to mutate a variable, then let.<p>var is pretty much just for legacy codes. Yes, it has unique behaviors,  but better stick to the new keywords, can prevent some headaches.
              </p><div>        <p>
                      <u><a href="reply?id=17917524&goto=item%3Fid%3D17915560%2317917524" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17916072"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  More garbage ycombinator hero worship. 'True Hackers' ? Grow up!
              <div>        <p>
                      <u><a href="reply?id=17916072&goto=item%3Fid%3D17915560%2317916072" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916272"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  One trait of true hackers is that they actually create things. As in "hack something together".<p>And yeah, this playful attitude to "just do it" tends to goes away when people become adults.</p><p>So in my book, it is better to grow down!
              </p><div>        <p>
                      <u><a href="reply?id=17916272&goto=item%3Fid%3D17915560%2317916272" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916531"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  In defense of some adults, I think a key point here is to realize that it's very different to do something alone, basically for yourself, and with the idea of (mostly) learning and exploring, that working with other people, for other people, and expecting the thing you are working on to keep functioning for the foreseable future.<p>I think it's important to understand both contexts (and practice them!).
              </p><div>        <p>
                      <u><a href="reply?id=17916531&goto=item%3Fid%3D17915560%2317916531" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17916145"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I understood it to be a tongue-in-cheek title
              <div>        <p>
                      <u><a href="reply?id=17916145&goto=item%3Fid%3D17915560%2317916145" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916990"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  You do things ironically long enough, you end up just doing the thing...
              <div>        <p>
                      <u><a href="reply?id=17916990&goto=item%3Fid%3D17915560%2317916990" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    
                  <tr id="17916454"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Looks like they are wrapping javascript functions instead of just using the functions.
              <div>        <p>
                      <u><a href="reply?id=17916454&goto=item%3Fid%3D17915560%2317916454" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916473"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Someone else points out that older versions of IE didn't support array methods like forEach on nodelists. So it is basically a thin compatibility layer.
              <div>        <p>
                      <u><a href="reply?id=17916473&goto=item%3Fid%3D17915560%2317916473" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17916103"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Is this some Arc-to-JS transpilation?
              <div>        <p>
                      <u><a href="reply?id=17916103&goto=item%3Fid%3D17915560%2317916103" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917050"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Probably not yet, but I've heard this might be the case in the future.
              <div>        <p>
                      <u><a href="reply?id=17917050&goto=item%3Fid%3D17915560%2317917050" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17915870"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  It's just a pile of functions; no actual processes are scripted to execute.
              <div>        <p>
                      <u><a href="reply?id=17915870&goto=item%3Fid%3D17915560%2317915870" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17915775"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I actually think this code is nice! 
Love the one liners. 
Variable names could be a little more....explicit.
              <div>        <p>
                      <u><a href="reply?id=17915775&goto=item%3Fid%3D17915560%2317915775" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17917358"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  It works reliably and quickly, so mission accomplished.
              <div>        <p>
                      <u><a href="reply?id=17917358&goto=item%3Fid%3D17915560%2317917358" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17915700"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  <a href="https://twitter.com/triskweline/status/798443082740023296" target="_blank">https://twitter.com/triskweline/status/798443082740023296</a><p>&gt; Valve's Steam Store renders on the server, uses ancient jQuery 1.8, loads 12 unminified JavaScripts.</p><p>&gt; It moved 3.5 billion dollars in 2015.
              </p><div>        <p>
                      <u><a href="reply?id=17915700&goto=item%3Fid%3D17915560%2317915700" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915934"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I'm not sure of what it's supposed to prove, who knows how many clients and how much money Steam lost because of slow loading/painting times or just plain broken JS. From experience I can tell that I gave up buying a game on Steam at least once because of broken jQuery.<p>There are real metrics from top industry leaders[1][2] to prove that loading time has a clear impact on conversion rates.</p><p>&gt;Consider this when you need 5000 npm modules and a team of 10 to compile your startup's login form.</p><p>Unminified JavaScripts files and bloated JS are both wrong, once again: not sure of what's the point of comparing both.</p><p>[1] <a href="https://medium.com/@vikigreen/impact-of-slow-page-load-time-on-website-performance-40d5c9ce568a" target="_blank">https://medium.com/@vikigreen/impact-of-slow-page-load-time-...</a>
[2] <a href="http://glinden.blogspot.com/2006/11/marissa-mayer-at-web-20.html" target="_blank">http://glinden.blogspot.com/2006/11/marissa-mayer-at-web-20....</a>
              </p><div>        <p>
                      <u><a href="reply?id=17915934&goto=item%3Fid%3D17915560%2317915934" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917113"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  What it proves is that it’s good enough to make tons of money.<p>You’re arguing from a hypothetical alternate reality where they could have been better off, but there’s no point in that. It’s like saying “Sure Usain bolt can run a sub 10sec 100m.... but if he’d gone into politics perhaps he’d made even more money and been twice as famous, we have no way of knowing, so how does that sub 10s 100m really prove anything about whether or not he’s fast?”</p><p>Usain bolt is fast, and that code made money. It’s just facts, accept them.
              </p><div>        <p>
                      <u><a href="reply?id=17917113&goto=item%3Fid%3D17915560%2317917113" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17915737"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  And burned 3.5 trillion developer brain cells just this january. Sensationalist metrics like this belong in the same trash bin as 'js is objectively bad and non-serious' bs.
              <div>        <p>
                      <u><a href="reply?id=17915737&goto=item%3Fid%3D17915560%2317915737" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915761"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  so actual information is bad and "3.5 trillion brain cells burned" is good?  Hrm....yeah, I'm going to Steam approach and focus on features that matter to the user rather than pedantic code which serves nothing but the developers ego in a vast majority of cases.
              <div>        <p>
                      <u><a href="reply?id=17915761&goto=item%3Fid%3D17915560%2317915761" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916376"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  I haven't had my morning coffee yet.<p>That's a piece of factual information for you, yet it has no bearing in this discussion.</p><p>Valve's revenue might be factual, but it also does very little to further this discussion. Valve has almost no effective competition, and people will put up with a lot of shit from them because of it — which makes their JS engineering practices largely unrelated to their revenue.
              </p><div>        <p>
                      <u><a href="reply?id=17916376&goto=item%3Fid%3D17915560%2317916376" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17915764"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  your choice, it's your cells :) I would not want to dot that to my sanity.
              <div>        <p>
                      <u><a href="reply?id=17915764&goto=item%3Fid%3D17915560%2317915764" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                    
              <tr id="17915747"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  While I appreciate the JS on this page (for usability reasons), I was surprised by the amount (149 lines) that is used for a page which looks like plain HTML.<p>Nevertheless, the code looks kinda beautiful.
              </p><div>        <p>
                      <u><a href="reply?id=17915747&goto=item%3Fid%3D17915560%2317915747" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17915859"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Barely readable but I think there's a lot of optimization going on here... I don't think that optimization is done correctly but that is why it's hard to read.
              <div>        <p>
                      <u><a href="reply?id=17915859&goto=item%3Fid%3D17915560%2317915859" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17917485"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  There's minimal optimization (as in tricks), but lots of optimization (as in readability and common sense).<p>It's also incredibly readable; I'm puzzled as to what the bar for "readability" is if this doesn't meet it.
              </p><div>        <p>
                      <u><a href="reply?id=17917485&goto=item%3Fid%3D17915560%2317917485" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                <tr id="17916092"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  document.querySelector('pre').style.color = '#17c517';
              <div>        <p>
                      <u><a href="reply?id=17916092&goto=item%3Fid%3D17915560%2317916092" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17917104"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Yeah this is nothing bad at all just some code. I’m fact I can grok it on my phone so I’d say it’s good code.
              <div>        <p>
                      <u><a href="reply?id=17917104&goto=item%3Fid%3D17915560%2317917104" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17915760"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Either run it through a minifier or have the whole thing unminified, these single lined functions look horrific, and are saving characters for the sake of it.<p>Terrible naming, e.g. 'vis' -&gt; reading the function it means toggle visibility, so it should be called 'toggleVisibility', you shouldn't have to read what the function is doing to understand what it will do.</p><p>You ever get a bug in your code, It's not fun to look back at badly maintained code and go 'oh, shit, what does this do again?'.
              </p><div>        <p>
                      <u><a href="reply?id=17915760&goto=item%3Fid%3D17915560%2317915760" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916361"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  &gt; Terrible naming, e.g. 'vis' -&gt; reading the function it means toggle visibility, so it should be called 'toggleVisibility'<p>But it doesn't toggle visibility. It sets visibility.
              </p><div>        <p>
                      <u><a href="reply?id=17916361&goto=item%3Fid%3D17915560%2317916361" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916394"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Yeah, you're right, I misread the code. It should be called 'setVisibility' then.<p>A problem that wouldn't exist if it was named correctly in the first place ;)
              </p><div>        <p>
                      <u><a href="reply?id=17916394&goto=item%3Fid%3D17915560%2317916394" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                  <tr id="17916681"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  any example on how to use this JS code?
              <div>        <p>
                      <u><a href="reply?id=17916681&goto=item%3Fid%3D17915560%2317916681" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916801"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Yes, the page you are currently reading.
              <div>        <p>
                      <u><a href="reply?id=17916801&goto=item%3Fid%3D17915560%2317916801" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                
              <tr id="17915743"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  any more javascript than this and you're probably making something that's full of ads
              <div>        <p>
                      <u><a href="reply?id=17915743&goto=item%3Fid%3D17915560%2317915743" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915884"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Or something that has features?
              <div>        <p>
                      <u><a href="reply?id=17915884&goto=item%3Fid%3D17915560%2317915884" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        
                  
              <tr id="17915808"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  It only exists because DOM APIs are crap, and jQuery is too big. So it ends up reimplementing parts of jQuery needed to run.
              <div>        <p>
                      <u><a href="reply?id=17915808&goto=item%3Fid%3D17915560%2317915808" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17915881"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  For the record, jQuery 3.3.1 (production, normal) is at 30kb [1]; if you don't want effects (production, slim), you can get it for less than 24kb [2]. For the value it provides, that does not sound "too big" to me.<p>[1]: <a href="https://code.jquery.com/jquery-3.3.1.min.js" target="_blank">https://code.jquery.com/jquery-3.3.1.min.js</a>
[2]: <a href="https://code.jquery.com/jquery-3.3.1.slim.min.js" target="_blank">https://code.jquery.com/jquery-3.3.1.slim.min.js</a>
              </p><div>        <p>
                      <u><a href="reply?id=17915881&goto=item%3Fid%3D17915560%2317915881" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916029"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  In contrast, hn.js only weighs 2.1kb and contains all the business logic.
              <div>        <p>
                      <u><a href="reply?id=17916029&goto=item%3Fid%3D17915560%2317916029" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17916106"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="120" height="1" /></td><td></td><td><div>
                  And it isn't even minified. So if there would be a problem in production it would be easily debuggable.
              <div>        <p>
                      <u><a href="reply?id=17916106&goto=item%3Fid%3D17915560%2317916106" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                    <tr id="17916519"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  The less lines of code, the less chance for a bug.
              <div>        <p>
                      <u><a href="reply?id=17916519&goto=item%3Fid%3D17915560%2317916519" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
            </tbody></table>
      </td></tr>
<tr><td><img src="s.gif" width="0" height="10" /><br /><a href="newsguidelines.html" target="_blank">Guidelines</a>
        | <a href="newsfaq.html" target="_blank">FAQ</a>
        | <a href="mailto:hn@ycombinator.com" target="_blank">Support</a>
        | <a href="https://github.com/HackerNews/API" target="_blank">API</a>
        | <a href="security.html" target="_blank">Security</a>
        | <a href="lists" target="_blank">Lists</a>
        | <a href="bookmarklet.html" target="_blank">Bookmarklet</a>
        | <a href="http://www.ycombinator.com/legal/" target="_blank">Legal</a>
        | <a href="http://www.ycombinator.com/apply/" target="_blank">Apply to YC</a>
        | <a href="mailto:hn@ycombinator.com" target="_blank">Contact</a><br /><br />Search:
          
            </td></tr>
      </tbody></table>
  
<div><h3>Like On Github</h3><div><div>*Title (label for the link)</div></div><div><div>*Comment (commit message)</div></div><div id="action-btns"><div id="logh_btn_save">Saving...</div><div id="logh_btn_favorite">Favorite</div><div id="logh_btn_cancel">Cancel</div></div></div>
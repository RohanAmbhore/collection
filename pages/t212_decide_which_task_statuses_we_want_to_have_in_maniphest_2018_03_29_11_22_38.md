<a href="https://phabricator.wikimedia.org/T212">https://phabricator.wikimedia.org/T212</a><div id="articleHeader"><h1><div><div>Decide which task statuses we want to have in Maniphest<div>Closed, Resolved<a href="/policy/explain/PHID-TASK-xs7dd22v62cbr3tksryr/view/" target="_blank">Public</a></div></div></div></h1></div><div><div><div><div><div><h1><div><div>Description</div></h1><div><div><div><div><p><strong>Proposed statuses:</strong></p>

<div><table>
<tbody><tr><td><strong>Status name in Phab</strong></td><td><strong>Explanation</strong></td><td><strong>Resembling in Bugzilla</strong></td></tr>
<tr><td>open</td><td>Default state</td><td>{UNCONFIRMED, NEW, ASSIGNED, REOPENED, PATCH_TO_REVIEW*} {}</td></tr>
<tr><td>stalled</td><td>Stalled</td><td></td></tr>
<tr><td>resolved</td><td>A change that fixes the task has been merged.</td><td>{RESOLVED, VERIFIED, CLOSED} FIXED</td></tr>
<tr><td>invalid</td><td>This is not a task, or it is out of scope in Wikimedia Phabricator.</td><td>{RESOLVED, VERIFIED, CLOSED} INVALID</td></tr>
<tr><td>declined</td><td>Bad idea, can not be reproduced, missing information has not been provided, or an acceptable alternative exists.</td><td>{RESOLVED, VERIFIED, CLOSED} {WONTFIX, LATER, WORKSFORME}</td></tr>
<tr><td><em>(marked as duplicate)</em></td><td></td><td>RESOLVED DUPLICATE</td></tr>

</tbody></table></div>

<p>*For PATCH_TO_REVIEW, create a project and add it to Phab tasks. See <a href="/T169" target="_blank">T169</a>.</p>

<hr /><p>For historical reasons: Initial task description:</p>

<p>By default, Phabricator offers OPEN, RESOLVED, WONTFIX, INVALID as statuses (and we can resolve tasks as duplicates).<br />
Custom statuses can be added via /config/edit/maniphest.statuses/</p>

<p>Subtasks I see here:</p>

<ul>
<li>Bugzilla also offers WORKSFORME (CANNOT_REPRODUCE). DO we want this?</li>
<li>NEEDINFO/NEEDS_MORE_INFO: marking an item as not actionable is a recurring request for Bugzilla, see <a href="https://bugzilla.wikimedia.org/show_bug.cgi?id=36064" target="_blank">https://bugzilla.wikimedia.org/show_bug.cgi?id=36064</a></li>
<li>INVALID sounds harsh so we might want to bikeshed on a better wording.</li>
</ul><div><div><h1><div><div>Details</div></h1><div><div><div><dl><dt>Reference </dt><dd>fl359 </dd></dl></div><div id="UQ0_8"><div>There are a very large number of changes, so older changes are hidden. <a href="/transactions/showolder/PHID-TASK-xs7dd22v62cbr3tksryr/?after=2807&quoteTargetID=UQ0_1&quoteRef=T212" target="_blank">Show Older Changes</a></div><div id="anchor-2807"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>greg</strong> wrote on <tt>2014-05-30 16:27:05 (UTC)</tt></p>

<blockquote>
<div>In <a href="/T359#10" target="_blank">T359#10</a>, @jdforrester wrote:</div>
<div><blockquote>

<div><p>I don't find "works for me" useful. If anything, it should be called "works, period" aka "not a bug". The "for me" part bothers me.</p></div>
</blockquote>

<p>I agree that it's a bit sucky; normally it's used for</p>

<ol>
<li>"this is a fault you're experiencing due to something else not in our control",</li>
<li>"this may be a fault, but you've given insufficient information to reproduce", or occasionally</li>
<li>"this was fixed since it was filed but I don't know exactly how so, so I'm not going to mark as FIXED"
<br /><br />… so use case (2) is no longer needed if we add "INCOMPLETE" or "NEEDSINFO" or whatever, and case (1) <em>could</em> be marked as "NOTABUG"/"INVALID"; for case (3) we could just be more lax about marking things as FIXED even when we don't know for sure that they are.</li>
</ol>
</blockquote>

<p>Agreed. Or even NotABug for that last one. Doesn't really matter in the long run.</p>

<blockquote><blockquote><p>I also find "won't fix" not useful. If it's not a bug, mark it as such. If it's way low priority, set the priority as such. Since we can have multiple projects in use by a team to track sprints and such, the product owner argument of "I want a clean backlog" doesn't apply.</p></blockquote>

<p>I strongly disagree, and I think the term "bug" rather than "task" skews this.</p>

<p>There are totally "valid" requests for new features or feature enhancements which are incompatible with the direction that we want to take a product (<em>e.g.</em> "Change the FOSS policy for Tool Labs so I can run Windows on it" or "Let me upload MPEG files to Commons" or "I want to have a button in VisualEditor to block the last editor if there are spelling mistakes"). "Lowest" priority for these is totally wrong – these are "No, we will not do this ever, and we will work to stop other people doing this if they try".</p></blockquote>

<p>Those all read like NotABug to me. "Won't Fix" is just a special type of NotABug. One that has reasoning based in 'product' versus 'actual code breakage.' It's the same thing in the end.</p>

<blockquote><blockquote><p>Boy do I wish we could have separate statuses per project per task (eg: Fixed in master but open in 1.23.0)</p></blockquote>

<p>Yeah, deployment/release statuses would be a lovely nice-to-have, but maybe for post-initial-switch?</p></blockquote>

<div id="anchor-2808"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>jdforrester</strong> wrote on <tt>2014-05-30 18:34:42 (UTC)</tt></p>

<p>[Updated] proposed set:</p>

<ul>

<li>RESOLVED</li>
<li>DECLINED (rather than WONTFIX)</li>
<li>NOTABUG (rather than INVALID, also replacing WORKSFORME)</li>
<li>NEEDSINFO (consistent with not using "_"s, INCOMPLETE sounds like it's about the task, not the request)</li>
</ul>

<p>Will validate these with other Product people.</p>

<p>(Do we want to represent PATCH_FOR_REVIEW or DEPLOYED states somehow?)</p></div><div id="anchor-2809"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-05-30 19:04:51 (UTC)</tt></p>

<p>What you are saying is that we can keep the current behavior, just changing the strings:</p>

<ul>
<li>Open --&gt; Open</li>
<li>Resolved --&gt; Resolved</li>
<li>Wontfix --&gt; Not a Bug</li>
<li>Invalid --&gt; Needs Info</li>
</ul>

<blockquote><p>Boy do I wish we could have separate statuses per project per task (eg: Fixed in master but open in 1.23.0)</p></blockquote>

<p>Remove the task from "MediaWiki" but keep it in "MediaWiki 1.23.0"?</p></div><div id="anchor-2810"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>swalling</strong> wrote on <tt>2014-05-30 19:19:46 (UTC)</tt></p>

<p>We should strive for absolutely simplicity and as small a number of states as possible. The more choices we provide the more confusing things are for all users. My thoughts, also replicated on the Product list are thus...</p>

<blockquote><p>[Updated] proposed set from @jdforrester:</p>

<p>OPEN<br />
RESOLVED<br />
DECLINED (rather than WONTFIX)<br />
NOTABUG (rather than INVALID, also replacing WORKSFORME)<br />
NEEDSINFO (consistent with not using "_"s, INCOMPLETE sounds like it's about the task, not the request)</p></blockquote>

<p>I don't think we need INVALID/NOTABUG or NEEDSINFO.</p>

<p>INVALID is required when Bugzilla has a "Resolved fixed" status. (If something is not a bug, you can't mark it as fixed.)  We just have a resolved state now, and an issue is resolved whether we fix it with a patch or if we investigate and it was never an issue to begin with.</p>

<p>NEEDSINFO is just adding additional state complexity to Needs Triage. Either leave something in Needs Triage, or triage is as lowest possible priority, while requesting more info. If someone can't provide more info, then mark it as Resolved.</p>

<p>Declined is definitely better than WONTFIX. I will keep thinking on options there, but would be comfortable using that language.</p></div><div id="anchor-2811"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-05-30 19:25:02 (UTC)</tt></p>

<p>The problem with making "Needs Info" equivalent to "Needs triage" is that it is difficult to know who to blame. While "Needs triage" means that the ball is in the field of the triagers / maintainers, "Needs Info" shows that it is he reporter who need to do some homework.</p></div><div id="anchor-2812"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>swalling</strong> wrote on <tt>2014-05-30 19:31:31 (UTC)</tt></p>

<blockquote><p>The problem with making "Needs Info" equivalent to "Needs triage" is that it is difficult to know who to blame. While &gt;"Needs triage" means that the ball is in the field of the triagers / maintainers, "Needs Info" shows that it is he reporter &gt;who need to do some homework</p></blockquote>

<p>Someone needs to be responsible for shepherding a task forward. Adding complexity to the state of tasks doesn't really help. They need to just step up and manage the state of the task. This is why we have maintainers, product managers, bugmeister, and other people in these roles.</p></div><div id="anchor-2813"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>jdforrester</strong> wrote on <tt>2014-05-30 21:02:13 (UTC)</tt></p>

<p>Steven – Please warn if you're forking the conversation so I don't have to respond in two places! :-)</p>

<p>I agree with Quim and disagree with Steven re. the appropriacy of not having a NEEDSINFO state in terms of user interaction.</p>

<p>I also disagree with Steven re. polluting the "RESOLVED" status space with bugs that are not resolved but instead weren't appropriate bugs for whatever reason (like problems with gadgets, configuration mistakes, or issues with a localisation string or whatever else is a problem not tracked in Phabricator).</p></div><div id="anchor-2814"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>swalling</strong> wrote on <tt>2014-05-30 21:18:28 (UTC)</tt></p>

<p>Think about the best, most beloved issue trackers currently in use (Trello, for instance). Then compare to Bugzilla, which everyone except random volunteers, Platform, and VisualEditor have pretty much abandoned as their canonical issue tracker.</p>

<p>Trello and most other good trackers: only two states: archived/resolved or open.<br />
Bugzilla: too many status, priority, target and other state options to bother counting.</p>

<p>This should be indicative how you're overcomplicating things.</p></div><div id="anchor-2815"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>scfc</strong> wrote on <tt>2014-05-31 02:25:24 (UTC)</tt></p>

<blockquote>

<div><p>The problem with making "Needs Info" equivalent to "Needs triage" is that it is difficult to know who to blame. While "Needs triage" means that the ball is in the field of the triagers / maintainers, "Needs Info" shows that it is he reporter who need to do some homework.</p></div>
</blockquote>

<p>"Need(s) info" (as a concept) isn't necessarily limited to the reporter.  It can also be used to indicate that input from ops, legal, design, etc. is needed.  In general, it should move a bug from the dashboard of the assignee to that of the designated person.</p>

<blockquote>

<div><p>What you are saying is that we can keep the current behavior, just changing the strings:</p></div>
</blockquote>



<blockquote><ul>
<li>Open --&gt; Open</li>
<li>Resolved --&gt; Resolved</li>
<li>Wontfix --&gt; Not a Bug</li>
<li>Invalid --&gt; Needs Info [...]</li>
</ul></blockquote>

<p>This doesn't make sense to me.  In Bugzilla, INVALID is used when someone complains that "expr 2 + 2" doesn't output 5 (and it shouldn't), WORKSFORME when the complaint is that it doesn't output 4, but for the triager it does, and WONTFIX if someone wants "expr 2.1 + 1.9" to work, but the developers consider this outside the scope of expr.</p>

<p>Also, IMHO in general if Phabricator has a different (default) set of statuses, I would be very hesitant to change them without a very good reason as it will introduce another little unnecessary hurdle for contributors.</p><div id="anchor-2816"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>avive</strong> wrote on <tt>2014-05-31 20:40:59 (UTC)</tt></p>

<blockquote>

<div><p>Boy do I wish we could have separate statuses per project per task (eg: Fixed in master but open in 1.23.0)</p></div>
</blockquote>

<p>Workboards kinda-sorta-coulda support this:</p><div id="anchor-2817"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>aklapper</strong> wrote on <tt>2014-06-02 18:30:11 (UTC)</tt></p>

<p>CC'ing those top 10 bug closers listed on <a href="http://korma.wmflabs.org/browser/its.html" target="_blank">http://korma.wmflabs.org/browser/its.html</a> who have an account here:</p>

<p>Are any specific thoughts on task/ticket statuses in Phabricator, based on your experience in Bugzilla?</p></div><div id="anchor-2818"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>greg</strong> wrote on <tt>2014-06-02 20:25:20 (UTC)</tt></p>

<p>[removing not useful part of this comment]</p>

<p>Bugzilla is still officially canonical, for the record.</p></div></div></div></div></div></div></div><div id="anchor-2819"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>greg</strong> wrote on <tt>2014-06-02 20:26:02 (UTC)</tt></p>

<blockquote>
<div>In <a href="/T359#22" target="_blank">T359#22</a>, @avive wrote:</div>
<div><blockquote>

<div><p>Boy do I wish we could have separate statuses per project per task (eg: Fixed in master but open in 1.23.0)</p></div>
</blockquote>

<p>Workboards kinda-sorta-coulda support this:</p></div>
</blockquote>

<p>Interesting.... That's a hack, but yeah, that could do it.</p></div></div></div></div></div></div></div><div id="anchor-2820"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>parent5446</strong> wrote on <tt>2014-07-10 17:35:20 (UTC)</tt></p>

<blockquote>

<div><p>This doesn't make sense to me.  In Bugzilla, INVALID is used when someone complains that "expr 2 + 2" doesn't output 5 (and it shouldn't), WORKSFORME when the complaint is that it doesn't output 4, but for the triager it does, and WONTFIX if someone wants "expr 2.1 + 1.9" to work, but the developers consider this outside the scope of expr.</p></div>
</blockquote>

<p>Agreed with this. WONTFIX, WORKSFORME, and INVALID are all three different, distinct resolutions, each representing a different community consensus concerning the bug reported.</p>

<p>Also, keep in mind that in Bugzilla, all of those (as well as FIXED and DUPLICATE) are not separate statuses, but rather all kept under the umbrella of RESOLVED. In reality, Bugzilla only has five statuses: UNCONFIRMED, NEW, ASSIGNED, PATCH_TO_REVIEW, and RESOLVED (we don't really use VERIFIED, so I left it out). With that in mind, ASSIGNED is really unnecessary in both Bugzilla and Phabricator, and PATCH_TO_REVIEW also is not necessary in Phabricator.</p>

<p>That brings us down to just three statuses: UNCONFIRMED, NEW, and RESOLVED. If there was a way to sub-categorize statuses in Phabricator, that would make things a lot simpler. In the end, though, I think it is necessary to keep the various sub-categories of RESOLVED (there names could be changed; I don't care about the naming).</p></div></div></div></div></div></div></div><div id="anchor-2821"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-07-11 13:44:43 (UTC)</tt></p>

<p>Revisiting this topic, I think we can use better the possibilities of Phabricator that were limitations in Bugzilla, requiring all these different types of statuses.</p>

<p>What about this:</p>

<ul>

<li>Needs Info</li>
<li>Resolved</li>
<li>Declined + optional tag project</li>
</ul>

<p>"Open" means that a task is actionable. The rest is defined by its current priority and details like having someone assigned to it, or visible activity in the form of mockups, patches...</p>

<p>"Needs Info" deserves an own status to raise attention. These tasks may be declined (automagically?) if no info is received after some period.</p>

<p>"Resolved" means that the task is considered completed.</p>

<p>"Declined" means that the maintainers are removing the task from the plate. Reasons will differ, but the end result is the same: reporters and other contributors must do some homework if they want to reactivate them. Project tags can be used optionally to catalog tasks that might interest someone. Think of projects like "Non Reproducible" or "Out Of Scope".</p>

<p>Bugzilla-Phabricator mapping:</p>

<div><table>
<tbody><tr><th>Bugzilla</th><th>Phabricator</th></tr>
<tr><td>UNCONFIRMED (default)</td><td>Open + Needs Triage (default)</td></tr>
<tr><td>NEW</td><td>Open</td></tr>
<tr><td>ASSIGNED</td><td>Open + Assigned To</td></tr>
<tr><td>PATCH_TO_REVIEW</td><td>Open + Code Revisions</td></tr>
<tr><td>NEED_INFO</td><td>Needs Info</td></tr>
<tr><td>RESOLVED FIXED</td><td>Resolved</td></tr>
<tr><td>RESOLVED INVALID</td><td>Declined</td></tr>
<tr><td>RESOLVED WONTFIX</td><td>Declined + project "Out Of Scope"</td></tr>
<tr><td>RESOLVED WORKSFORME</td><td>Declined + project "Non Reproducible"</td></tr>
<tr><td>RESOLVED DUPLICATE</td><td>(merged)</td></tr>
</tbody></table></div></div></div></div></div></div></div></div><div id="anchor-2822"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>parent5446</strong> wrote on <tt>2014-07-11 14:19:18 (UTC)</tt></p>

<p><a href="/p/Qgil/" target="_blank">@Qgil</a>, that looks pretty good. There's just a small error in your mapping table. UNCONFIRMED should map to "Needs Info", since, like you mentioned earlier, triage has more to do with the maintainers deciding the priority rather than the bug needing more information.</p></div></div></div></div></div></div></div><div id="anchor-2823"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>aklapper</strong> wrote on <tt>2014-07-14 11:30:27 (UTC)</tt></p>

<p><a href="/p/Qgil/" target="_blank">@Qgil</a>: Thanks, this looks really really good indeed (though I wonder a little bit with regard to workflow how tedious it'll be to change task status to Declined plus also add a "Out Of Scope" / "Non reproducible" project to that task). I guess that "Out of scope" would also cover "should be fixed in upstream" as it's "not our bug".</p></div></div></div></div></div></div></div><div id="anchor-2824"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-07-14 12:43:56 (UTC)</tt></p>

<p><a href="/p/Parent5446/" target="_blank">@Parent5446</a>, if I'm not mistaken, in Bugzilla reports are by default UNCONFIRMED until some action makes them NEW. The equivalent default status in Phabricator is Open + Needs Triage. "Needs Info" is a status that must be set manually, therefore it cannot be the default for all new tasks.</p>

<p><a href="/p/Aklapper/" target="_blank">@Aklapper</a>, adding projects to declined tasks should be optional, and done when such projects help the task and the reporter somehow. Also, adding one tag-project can save you the work of typing a manual comment.</p>

<p>If "should be fixed in upstream" means "we won't work on it", then it can be Declined + project Upstream, and additionally we could even add a project for the specific upstream e.g. "Elasticsearch" if that helps us tracking tasks. We can also have tasks that must be fixed upstream, but our maintainers are planning to work on them, as it is the case already now here with certain Phabricator tasks.</p></div></div></div></div></div></div></div><div id="anchor-2825"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>aklapper</strong> wrote on <tt>2014-07-14 14:16:53 (UTC)</tt></p>

<p>VERIFIED status in Bugzilla is being used by the Wikidata team - wondering how important it is to them in their development workflow, and if they could live without it for the sake of keeping it simple and stupid. I've pinged Lydia on IRC as I couldn't find an account here.</p></div></div></div></div></div></div></div><div id="anchor-2826"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>aklapper</strong> wrote on <tt>2014-07-14 14:26:09 (UTC)</tt></p>

<p>Hmm, same VERIFIED question goes to the VE team, actually (@jdforrester).</p>

<p>&lt;Lydia_WMDE&gt; we do use it for basically acceptance confirmation. ie ideally dev sets it to resolved fixed and then i go and set it to verified. doesn't entirely work atm though<br />
&lt;andre&gt; the question is probably "what would you lose if it wasn't available anymore". Plus VE and Wikidata seem to be the only teams using VERIFIED.<br />
&lt;Lydia_WMDE&gt; we would lose a second stage of review/confirmation.<br />
&lt;Lydia_WMDE&gt; so i can live without it but i think we should have it<br />
&lt;andre&gt; does anybody ever query for VERIFIED specifically (or excluding that from RESOLVED tickets)? What if this was just added as a comment instead?<br />
&lt;Lydia_WMDE&gt; i query for all resolved fixed ones to go through them and verify<br />
&lt;andre&gt; so if you could query for resolved tickets and exclude those which have a "has been verified" comment, would that also work? :D<br />
&lt;Lydia_WMDE&gt; doesn't feel very nice/clean<br />
&lt;andre__&gt; I'm wondering if adding a "Wikidata verified" (or so) project instead might work. Need to think about it.</p></div></div></div></div></div></div></div><div id="anchor-2827"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>Rush</strong> wrote on <tt>2014-07-14 15:03:38 (UTC)</tt></p>

<p>could verified be a workboard status rather than a full on issue status?</p>

<p>some of the team specific workflow can be handled at the alternative abstraction layer I think</p></div></div></div></div></div></div></div><div id="anchor-2828"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-07-14 15:13:43 (UTC)</tt></p>

<p>@Rush was faster than me. I was also about to say that workboards offer all the degrees you need between Open and Resolved.</p></div></div></div></div></div></div></div><div id="anchor-2829"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>Rush</strong> wrote on <tt>2014-07-14 16:00:34 (UTC)</tt></p>

<blockquote><p>Bugzilla-Phabricator mapping:</p>

<div><table>
<tbody><tr><th>Bugzilla</th><th>Phabricator</th></tr>
<tr><td>UNCONFIRMED (default)</td><td>Open + Needs Triage (default)</td></tr>
<tr><td>NEW</td><td>Open</td></tr>
<tr><td>ASSIGNED</td><td>Open + Assigned To</td></tr>
<tr><td>PATCH_TO_REVIEW</td><td>Open + Code Revisions</td></tr>
<tr><td>NEED_INFO</td><td>Needs Info</td></tr>
<tr><td>RESOLVED FIXED</td><td>Resolved</td></tr>
<tr><td>RESOLVED INVALID</td><td>Declined</td></tr>
<tr><td>RESOLVED WONTFIX</td><td>Declined + project "Out Of Scope"</td></tr>
<tr><td>RESOLVED WORKSFORME</td><td>Declined + project "Non Reproducible"</td></tr>
<tr><td>RESOLVED DUPLICATE</td><td>(merged)</td></tr>

</tbody></table></div></blockquote>

<p>I think this is a stupid question on my part, but are you suggesting a literal "out of scope" project that tasks are added to for this? or that there is a ticket state for which the option would be "declined - out of project scope'.  The first I don't think will work across the gamut just because it's too big of a bucket to be meaningful across all the projects / teams / workflows, etc,.  The second seems like a very specific category of declined?</p>

<p>Declined does seems more diplomatic than won't fix :)</p>

<p>Work-for-me is a terrible state for a ticket to be in as it doesn't mean anything.  It just means two people had different experiences.  It doesn't mean something needs more work, and it doesn't mean something _doesn't_ need more work.  It's not a task or issue state so much as it could be the genesis of an open/closed state, yet is neither.  It doesn't seem meaningful, and could literally be a less valuable version of NEEDS_INFO.</p>

<p>INVALID = this cannot be done.</p>

<p>And, dear god please forgive me for even bikeshedding to this degree, but resolved fixed is less good than resolved closed (phab default).  Closed is wide enough to include hey we talked about it and decided it's a no, but good question.  Fixed implies changes...maybe only to me...whereas an issue can definitely be moved out of an open state without anything being modified other than a requesters state of mind :)</p>

<p>I think in some cases for resolved subtypes we are trying to cram a lot of information into this basic ticket state that doesn't necessarily fit there.  We could conceivably make a separate ticket field to indicate the resolved reasoning as in.</p>

<p>Resolved....</p>

<p>RATIONALE...wonfix/invalid/fixed/foo/bar/whatever/</p>

<p>The only thing I feel is a strong point is that invalid is a distinct state for a ticket to be in outside of normal resolution, and it is important to distinguish between this isn't possible and we are not doing this</p></div></div></div></div></div></div></div><div id="anchor-2830"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-07-14 17:01:42 (UTC)</tt></p>

<blockquote>
<div>In <a href="/T359#40" target="_blank">T359#40</a>, @Rush wrote:</div>
<div><p>are you suggesting a literal "out of scope" project that tasks are added to for this? or that there is a ticket state for which the option would be "declined - out of project scope'.</p></div>
</blockquote>

<p>The former, but using the project just as a tag. Those tasks will be declined. We can forget about them. No team, sprint, dashboard, etc, will be assigned to those. You can always make elaborate queries if you need them: which tasks were "Declined" (Status) as "Out Of Scope" (tag-project) in "Visual Editor" (project-project)?</p>

<blockquote><p>Work-for-me is a terrible state for a ticket to be in as it doesn't mean anything.</p></blockquote>

<p>Following the proposal above, the migration script should convert Bugzilla's WORKSFORME reports in Declined + project "Non Reproducible" tasks. In Bugzilla WORKSFORME sometimes is used as "what you see as a bug is correct behavior in my eyes", which is different than "Non Reproducible". I would still apply the same rule and leave the old bugs Rest In Peace.</p>

<blockquote><p>resolved fixed is less good than resolved closed</p></blockquote>

<p>For the sake of the migration skip, I would treat both as equal.</p>

<blockquote><p>The only thing I feel is a strong point is that invalid is a distinct state for a ticket to be in outside of normal resolution, and it is important to distinguish between this isn't possible and we are not doing this</p></blockquote>

<p>Declined + project "Invalid" for the migration? No matter what, they are still declined tasks. I just want to avoid if possible to have an option in the Status that will not be used in the 92% of cases (if we have to trust Bugzilla stats). Besides, if we dig deeper in the current INVALID reports we will find different reasons to reach to that resolution, including out of scope, spam, poorly written, and more.</p>

<p>Having one "Declined" resolution and specific tag projects allow us to be (optionally) more precise without cluttering the Status field.</p></div></div></div></div></div></div></div><div id="anchor-2831"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>aklapper</strong> wrote on <tt>2014-07-15 17:09:46 (UTC)</tt></p>

<p><strong>Generally speaking:</strong> It's all about "keep it simple and stupid" vs "I want to categorize everything" and finding a good compromise. Before commenting, everybody should question themselves whether they do care a lot about expressing a reason <em>via task status</em> and if they really query for tickets and differentiate on that status, or if they can also survive having the reason in a project workboard column or comment only which is harder to search for.</p>

<p>Regarding the proposal to <strong>set projects in addition to the "Declined" status</strong>, I've in the meantime gotten afraid that people won't do that. I cannot exactly prove it and the quote refers to fixed issues, but: "Of course, the developer could change the issue category after resolution---but this happens rarely. In many cases there exists no real motivation to change the issue category once the cause for a problem is found and fixed." from <a href="http://www.st.cs.uni-saarland.de/softevo/bugclassify/paper/icse2013-bugclassify.pdf" target="_blank">http://www.st.cs.uni-saarland.de/softevo/bugclassify/paper/icse2013-bugclassify.pdf</a> page 396.</p>

<p><strong>A status called "Invalid":</strong> There are opinions in Mozilla ( <a href="http://eaves.ca/2011/07/27/lessons-for-open-source-communities-an-example-for-bug-tracking-more-efficient/" target="_blank">http://eaves.ca/2011/07/27/lessons-for-open-source-communities-an-example-for-bug-tracking-more-efficient/</a> and <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=592533" target="_blank">https://bugzilla.mozilla.org/show_bug.cgi?id=592533</a> ) that average users who incorrectly filed a support request (configuration, on-wiki gadget issues) as a task/bug report and who are not used to dev workflows/terms, that "invalid" can feel derogative, but I really cannot come up with a better term after looking at other issue trackers and their terms, so I naively call it "Invalid here" instead of "Invalid".</p>

<p>I am probably less afraid of <strong>cluttering the status field</strong> if people <em>really</em> want to differentiate reasons for closing. The ~dozen of Bugzillas I sometimes interact with have 5-9 statuses and 6-13 resolutions. Combining that in one field in Phab, I think we're not too bad if we ended up with 7 or 8 task statuses.</p>

<p><strong>Summary:</strong></p>

<ul>
<li>Needs Triage</li>

<li>Needs Info</li>
<li>Resolved</li>
<li>Invalid Here (resembling "Invalid", "Nothing for a Phab task", "Spam", "Support request", "On-Wiki issue", "Upstream it", "Works as intended" etc.)</li>
<li>Declined (resembling "Wontfix", "Out of scope", "Actively against fixing this", "Overcome by events" etc.)</li>
<li>Unreproducible (resembling "Works for me", "Insufficient data", "Feedback Timeout", "Your computer got hacked by an interwebs virus that displays ads on Wikipedia" etc.)</li>
</ul>



<ul>
<li>"Verified" as an optional workboard column per $project if $project wants it.</li>
</ul></div></div></div></div></div></div></div><div id="anchor-2832"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>Rush</strong> wrote on <tt>2014-07-15 20:01:46 (UTC)</tt></p>

<p>andre as usual you come up with good stuff.</p>

<p>@qgil...I really liked your thoughts, over the evening yesterday tho I became less convinced people would actually do it :)  I think it's a really cool idea within domains for people to utilize, ops could do this for their own stuff, andre could do it too.  Anyone who can ensure their own consistency it would work out for, but I don't feel like the <br />
workflow of a task lends itself to the status+project combo being a good default mindset sort for the big 3 or 4 or even 5 cases.</p>

<p>I think the real difference tho is I don't view invalid as a subset of declined.  I do look at declined tasks as having value in a historical sense, and invalid tasks are really waiting to be purged out when they become cumbersome enough.</p>

<p>I don't see a difference between unreproducible and declined.  Do we not decline as unreproducible?  But in general, if it's a broad enough brush to be it's own bucket.  Fine with me.</p>

<p>I also think, unreproducible could be a form of needs_info.  that probably makes the most sense to me.</p>

<p>Needs triage is a priority right?  Not a status.</p>

<p>needs_info seems kind of odd, why not the suggested [incomplete]</p>

<p>That means the status's would be something like:</p>

<div><table>
<tbody><tr><td>open</td><td>default state</td></tr>
<tr><td>needs_info</td><td>stalled</td></tr>
<tr><td>resolved</td><td>closed</td></tr>
<tr><td>invalid</td><td>no historical value will be purged eventually (spam, etc)</td></tr>
<tr><td>declined</td><td>we have decided not too -- even though we could</td></tr>

</tbody></table></div>

<p>-&gt;</p>

<div><table>
<tbody><tr><td>unreproducible</td><td>needs more info to reproduce?  should be merged with needs_info?</td></tr>

</tbody></table></div>

<p>invalid and declined here are also taking the place of reject which exists in rt.  we do get spam there as well.</p>

<p>Also, really liking andre's 'resembling' identities for the categories.</p></div></div></div></div></div></div></div><div id="anchor-2833"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-07-16 10:38:30 (UTC)</tt></p>

<p>Ok, we can forget about tag-projects for Day one (and therefore the migration). They can always be added to the process at a later stage if somebody misses them or has a better idea of what to do with them.</p>

<p>I agree that Unreproducible is a variant of Needs Info.</p>

<blockquote>
<div>In <a href="/T359#43" target="_blank">T359#43</a>, @Rush wrote:</div>

</blockquote>

<div><table>
<tbody><tr><td>open</td><td>default state</td></tr>
<tr><td>needs_info</td><td>stalled</td></tr>
<tr><td>resolved</td><td>closed</td></tr>
<tr><td>invalid</td><td>no historical value will be purged eventually (spam, etc)</td></tr>
<tr><td>declined</td><td>we have decided not too -- even though we could</td></tr>

</tbody></table></div>

<p>I agree with these statuses; descriptions to be fine tuned.</p></div></div></div></div></div></div></div><div id="anchor-2835"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>aklapper</strong> wrote on <tt>2014-07-16 13:28:23 (UTC)</tt></p>

<p>Assuming that "Declined" covers both "sorry but we really could not reproduce" and "we are against fixing it", this is probably the smallest set of statuses one could come up with. Thank you Quim. :)</p>

<p>One aspect left: <strong>Gerrit patch notifications</strong> in Phab in <a href="/T277" target="_blank">T277</a> (as long as we have not killed Gerrit in <a href="/T42" target="_blank">T42</a>): I have no idea yet if or how we want to implement the behavior of the "Patch to review" status in Bugzilla. Another status, temporarily until we've fixed <a href="/T42" target="_blank">T42</a>? (as I have a hard time to imagine notifications triggering changes to a column in a project's workboard, as the naming scheme of columns in per project)</p></div></div></div></div></div></div></div><div id="anchor-2837"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-07-16 15:01:29 (UTC)</tt></p>

<p>Since those Gerrit patch notifications are created by a bot, here we could apply the idea of Open + project "Patches For Review".</p>

<p>The same bot could remove that project if the patch is merged/abandoned.</p></div></div></div></div></div></div></div><div id="anchor-2838"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>Rush</strong> wrote on <tt>2014-07-16 15:25:24 (UTC)</tt></p>

<p><a href="/p/Aklapper/" target="_blank">@Aklapper</a> can you help me understand more about what you mean by gerrit patch notifications?</p>

<p>I know there is some interaction between bugzilla and gerrit, but haven't used it myself.</p></div></div></div></div></div></div></div><div id="anchor-2839"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>greg</strong> wrote on <tt>2014-07-16 16:53:22 (UTC)</tt></p>

<blockquote>
<div>In <a href="/T359#48" target="_blank">T359#48</a>, @Rush wrote:</div>
<div><p><a href="/p/Aklapper/" target="_blank">@Aklapper</a> can you help me understand more about what you mean by gerrit patch notifications?</p>

<p>I know there is some interaction between bugzilla and gerrit, but haven't used it myself.</p></div>
</blockquote>

<p>Basically, since there is no tight integration between Gerrit and BZ, all we have is a bot that comments on BZ bugs when there's a new related patch, eg <a href="https://bugzilla.wikimedia.org/show_bug.cgi?id=67270#c26" target="_blank">https://bugzilla.wikimedia.org/show_bug.cgi?id=67270#c26</a> and when said patch is merged eg <a href="https://bugzilla.wikimedia.org/show_bug.cgi?id=67270#c27" target="_blank">https://bugzilla.wikimedia.org/show_bug.cgi?id=67270#c27</a> (and similar message for abandoned). When it comments that there's a related patch, it also changes the STATUS to PATCH_TO_REVIEW.</p>

<p>You get the fancy behavior by including "Bug: 12345" at the bottom of the change commit message (right before the change-id gerrit needs at the very bottom).</p>

<p>I personally think there should be an "in-progress" or whatever status as well, that says "someone is actively working on this, check the assignee field for who". The Gerrit bot could set that status when it has a related patch. (We basically use "ASSIGNED" in BZ for that now.)</p>

<p>The PATCH_TO_REVIEW status in BZ is a hack, I believe, because BZ doesn't have a nice way of querying bugs that have linked Gerrit commits associated with a bug. ie: the issue that will be solved when we also transition code review to Phab from Gerrit.</p></div></div></div></div></div></div></div><div id="anchor-2840"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>aklapper</strong> wrote on <tt>2014-07-16 17:13:05 (UTC)</tt></p>

<blockquote><p>The PATCH_TO_REVIEW status in BZ is a hack, I believe,</p></blockquote>

<p>Yes, it's done by <a href="https://gerrit-review.googlesource.com/#/admin/projects/plugins/its-bugzilla" target="_blank">https://gerrit-review.googlesource.com/#/admin/projects/plugins/its-bugzilla</a> set up by qchris and setting up a status looked like the most visible way (in additional to the comment created by that plugin). See <a href="http://lists.wikimedia.org/pipermail/wikitech-l/2012-December/065046.html" target="_blank">http://lists.wikimedia.org/pipermail/wikitech-l/2012-December/065046.html</a> and <a href="https://gerrit.wikimedia.org/r/#/c/69843/" target="_blank">https://gerrit.wikimedia.org/r/#/c/69843/</a> for historical data.</p>

<blockquote><p>"someone is actively working on this, check the assignee field for who"</p></blockquote>

<p>That's what workboards are for, IMHO?</p></div></div></div></div></div></div></div><div id="anchor-2841"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>greg</strong> wrote on <tt>2014-07-16 17:24:13 (UTC)</tt></p>

<blockquote>

<div><blockquote><p>"someone is actively working on this, check the assignee field for who"</p></blockquote>

<p>That's what workboards are for, IMHO?</p></div>
</blockquote>

<p>If the task is in one and only one project, and that project uses workboards (not all will), sure. But if there's any deviation from that, no, not really.</p></div></div></div></div></div></div></div><div id="anchor-2842"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-07-16 18:46:35 (UTC)</tt></p>

<p>Bugzilla has so many ASSIGNED reports where it is not true that "someone is actively working on this, check the assignee field for who".</p>

<p>I'd rather have us rely on Open + Assigned To + workboard OR the assignee commenting about their intentions (so nobody else steps on their toes).</p></div></div></div></div></div></div></div><div id="anchor-2843"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>Rush</strong> wrote on <tt>2014-07-16 18:53:44 (UTC)</tt></p>

<p>so seems like we can mimic this gerrit bot that notifies bugzilla with phab, but without a PATCH_TO_REVIEW  status that step would be replaced by another comment linking to the merged patch?</p></div></div></div></div></div></div></div><div id="anchor-2844"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>greg</strong> wrote on <tt>2014-07-16 23:33:21 (UTC)</tt></p>

<blockquote>

<div><p>Bugzilla has so many ASSIGNED reports where it is not true that "someone is actively working on this, check the assignee field for who".</p></div>
</blockquote>

<p>fwiw: I actively use that as a means to track work my team is doing. Some other projects/components don't have people tending the garden actively.</p></div></div></div></div></div></div></div><div id="anchor-2845"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>Rush</strong> wrote on <tt>2014-07-17 14:48:37 (UTC)</tt></p>

<p><a href="/p/greg/" target="_blank">@greg</a>, would it work for you if there was an automated tag for issues in this state for now instead?</p>

<p>so you could go do phab.wm.com/tag/patch_to_review and see all tasks in this status.</p>

<p>That way we don't end up with an unused ticket status in the future, and since it's automated we can ensure consistency.</p></div></div></div></div></div></div></div><div id="anchor-2846"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>greg</strong> wrote on <tt>2014-07-17 16:31:00 (UTC)</tt></p>

<blockquote>
<div>In <a href="/T359#55" target="_blank">T359#55</a>, @Rush wrote:</div>
<div><p><a href="/p/greg/" target="_blank">@greg</a>, would it work for you if there was an automated tag for issues in this state for now instead?</p>

<p>so you could go do phab.wm.com/tag/patch_to_review and see all tasks in this status.</p>

<p>That way we don't end up with an unused ticket status in the future, and since it's automated we can ensure consistency.</p></div>
</blockquote>

<p>For me, yeah, probably. How are tags added/removed? I can't seem to find it in "Edit task"</p></div></div></div></div></div></div></div><div id="anchor-2847"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>Rush</strong> wrote on <tt>2014-07-17 17:01:14 (UTC)</tt></p>

<p>@greg...I will forgo my speech on projects and organization :D</p>

<p>But really it's that all projects function as tags at the basic level.  So we make a patch_to_review project and add and remove as appropriate for filtering.</p></div></div></div></div></div></div></div><div id="anchor-2848"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>scfc</strong> wrote on <tt>2014-07-17 22:55:59 (UTC)</tt></p>

<p>A recurring problem in Bugzilla with PATCH_TO_REVIEW as a status is that, as it is used as a flag, when a patch is merged/abandoned, one has to go through all the comments to see if this was the only patch to have triggered setting the flag in the first place (and if it previously was UNCONFIRMED, NEW or ASSIGNED).  A Phabricator replacement should take into account that there is a n:m relationship between bugs and patches and ensure that the UI provides a clear picture of the existence of open patches.</p></div></div></div></div></div></div></div><div id="anchor-2849"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>greg</strong> wrote on <tt>2014-07-17 23:13:16 (UTC)</tt></p>

<blockquote>

<div><p>A recurring problem in Bugzilla with PATCH_TO_REVIEW as a status is that, as it is used as a flag, when a patch is merged/abandoned, one has to go through all the comments to see if this was the only patch to have triggered setting the flag in the first place (and if it previously was UNCONFIRMED, NEW or ASSIGNED).  A Phabricator replacement should take into account that there is a n:m relationship between bugs and patches and ensure that the UI provides a clear picture of the existence of open patches.</p></div>
</blockquote>

<p>In phase 1 (ie: after we've only transitioned Bugzilla to Phab, not Gerrit), that's out of scope.</p>

<p>For phase 2 (ie: after we've also transitioned Gerrit), that will be implicit in that fact that we use Phabricator :)</p>

<p>You can see a good example of what that looks like on the upstream Phabricator instance where a Task has many Diffs associated with it, and you can quickly see how many are merged/open: <a href="https://secure.phabricator.com/T2772" target="_blank">https://secure.phabricator.com/T2772</a></p></div></div></div></div></div></div></div><div id="anchor-2850"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>jdforrester</strong> wrote on <tt>2014-07-23 16:14:19 (UTC)</tt></p>

<blockquote>

<div><div><table>
<tbody><tr><td>invalid</td><td>no historical value will be purged eventually (spam, etc)</td></tr>

</tbody></table></div></div>
</blockquote>

<p>This is a pretty big change in semantics – right now, INVALID and WONTFIX are used to distinguish between different shades of declines. I'd roughly categorise them as:</p>

<ul>
<li>"truly invalid" – spam reports</li>
<li>"misplaced" – things filed in Bugzilla which aren't dealt with in Bugzilla</li>
<li>"overtaken by changes" – things asking for changes that made sense at the time but don't now</li>
<li>"mistaken" – things which are this way by design (more often labelled WONTFIX).</li>
</ul>

<p>We'll need to make sure people are careful not to use "invalid" the way they've been using INVALID. Maybe purging isn't the best idea</p></div></div></div></div></div></div></div><div id="anchor-2851"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>Nemo_bis</strong> wrote on <tt>2014-07-24 01:02:24 (UTC)</tt></p>

<blockquote><p>(marked as duplicate)</p></blockquote>

<p>Can this status be searched?</p></div></div></div></div></div></div></div><div id="anchor-2852"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-07-24 10:37:59 (UTC)</tt></p>

<p>The status that appears at the top of merged tasks is "Closed, Duplicate", so it should be as searchable (or not, see below) as the rest of statuses.</p>

<p>As far as I can see, users can only search tasks by status Open/Closed. At least I can't see a checkbox for the different Closed statuses at the Advanced Search. Querying "Merged into" will get you pretty close (<a href="https://secure.phabricator.com/search/query/HY2OHkK_zrvW/" target="_blank">I hope this URL works</a>).</p></div></div></div></div></div></div></div><div id="anchor-2853"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>aklapper</strong> wrote on <tt>2014-07-24 11:14:45 (UTC)</tt></p>

<blockquote>

<div><blockquote><p>(marked as duplicate)</p></blockquote>

<p>Can this status be searched?</p></div>
</blockquote>

<p>See "Status" section on <a href="http://fab.wmflabs.org/maniphest/query/advanced/" target="_blank">http://fab.wmflabs.org/maniphest/query/advanced/</a> - there is an explicit "Duplicate" checkbox.</p></div></div></div></div></div></div></div><div id="anchor-2854"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-07-24 11:17:36 (UTC)</tt></p>

<p>True! I was looking at the general advanced search instead of Maniphests' advanced search. Problem solved, then.</p></div></div></div></div></div></div></div><div id="anchor-2855"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-07-24 11:32:59 (UTC)</tt></p>

<p>James, I think the statuses and their descriptions listed at the top of this task satisfy your concerns. I agree that we cannot just delete all what is marked Invalid. In fact, Phabricator doesn't bring any need to change the current policy for deleting reports in Bugzilla.</p>

<blockquote>
<div>In <a href="/T359#63" target="_blank">T359#63</a>, @jdforrester wrote:</div>
<div><ul>
<li>"truly invalid" – spam reports</li>
</ul></div>
</blockquote>

<p>These will indeed be unpublished/deleted as soon as they are detected. Maybe we can have a "Spam" project in order to allow users to report spam. Then the right team with the right permissions can unpublish them.</p>

<blockquote><ul>
<li>"misplaced" – things filed in Bugzilla which aren't dealt with in Bugzilla</li>
<li>"overtaken by changes" – things asking for changes that made sense at the time but don't now</li>
</ul></blockquote>

<p>"This is not a task, or it is out of scope in Wikimedia Phabricator." Clearly "Invalid". Will stay.</p>

<blockquote><ul>
<li>"mistaken" – things which are this way by design (more often labelled WONTFIX).</li>
</ul></blockquote>

<p>"Bad idea, cannot be reproduced, missing information has not been provided, or an acceptable alternative exists." Clearly Declined. Will stay.</p></div></div></div></div></div></div></div><div id="anchor-2856"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>aklapper</strong> wrote on <tt>2014-07-24 12:31:01 (UTC)</tt></p>

<p>I assume good faith when editing the description, but I'd STILL appreciate if no wrong data was entered. ;) Fixed.</p></div></div></div></div></div></div></div><div id="anchor-2857"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>Nemo_bis</strong> wrote on <tt>2014-07-25 19:01:48 (UTC)</tt></p>

<blockquote>

<div><p>I'd STILL appreciate if no wrong data was entered. ;) Fixed.</p></div>
</blockquote>

<p>After <a href="http://fab.wmflabs.org/transactions/detail/PHID-XACT-TASK-xukns75c3p24el7/" target="_blank">http://fab.wmflabs.org/transactions/detail/PHID-XACT-TASK-xukns75c3p24el7/</a> it's ok; I have merely copied the official descriptions from mediawiki.org, UNCONFIRMED and REOPENED are practically equivalent now so they should be in the same group.</p></div></div></div></div></div></div></div><div id="anchor-2858"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>Rush</strong> wrote on <tt>2014-08-13 20:12:41 (UTC)</tt></p>

<p>ran into a problem here:</p>

<p>needs_info is a not a valid possible status</p>

<p>[Core Exception/Exception] Key "needs_info" is not a valid status constant. Status constants must be 1-12 characters long and contain only lowercase letters (a-z) and digits (0-9). For example, "open" or "closed" are reasonable choices.</p></div></div></div></div></div></div></div><div id="anchor-2859"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>Rush</strong> wrote on <tt>2014-08-13 20:13:01 (UTC)</tt></p>

<p>trying just "stalled" as a needs info alternative</p></div></div></div></div></div></div></div><div id="anchor-2860"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-08-14 12:00:11 (UTC)</tt></p>

<p>Maybe this refers to the value, being different to the string shown in the UI? This instance is showing "Resolved", "Wontfix", "Invalid" in upper case.</p>

<p>If this is the case, we could have "needsinfo" as value and "Needs Info" as UI string.</p></div></div></div></div></div></div></div><div id="anchor-2861"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-08-14 12:00:39 (UTC)</tt></p>

<p>Ooops, sorry for resolving accidentally.</p></div></div></div></div></div></div></div><div id="anchor-2862"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>Rush</strong> wrote on <tt>2014-08-14 19:57:33 (UTC)</tt></p>

<p>tinker...tinker...tinker...I got it to work I think.</p>

<p>I updated the values on this install to match what i have for prod.  this install is kinda of a pain since everthing is a one-off and I can't just use the same config.</p>

<p>anyhoo -- check it out.</p></div></div></div></div></div></div></div><div id="anchor-2863"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-08-15 11:45:56 (UTC)</tt></p>

<p>Great!</p>

<p>Task completed? I volunteer documenting this in <a href="https://www.mediawiki.org/wiki/Phabricator/Help" target="_blank">https://www.mediawiki.org/wiki/Phabricator/Help</a></p></div></div></div></div></div></div></div><div id="anchor-2864"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>qgil</strong> wrote on <tt>2014-08-18 21:16:06 (UTC)</tt></p>

<p>Currently we can see messages talking about tasks moving <tt>from "Unknown Status" to "Declined"</tt>. See for instance at the end of <a href="/T432" target="_blank">T432</a>. What is this "Unknown Status"? Looks like it's "Open", although maybe there is another factor in play.</p></div></div></div></div></div></div></div><div id="anchor-2865"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p><strong>aklapper</strong> wrote on <tt>2014-08-18 21:20:42 (UTC)</tt></p>

<p>Re last comment: We renamed some statuses in this fab.wmflabs.org instance to "implement"/reflect the decisions made in <a href="/T359" target="_blank">T359</a>, and we realized that when a status (in this case the previously existing WONTFIX) goes away, Phab resets a task's status to unknown. Next time we know better, and I fixed that manually now to not run into inconsistencies for <a href="/T336" target="_blank">T336</a>.</p></div></div></div></div></div></div></div><div id="anchor-2867"><div><div><div><div><a href="/p/flimport/" target="_blank">flimport</a> closed this task as Resolved.<a href="#2867" target="_blank">Sep 12 2014, 1:37 AM</a></div></div></div></div></div><div id="anchor-4660"><div><div><div><div><a href="/p/Qgil/" target="_blank">Qgil</a> reopened this task as Open.<a href="#4660" target="_blank">Sep 17 2014, 7:46 PM</a></div><div><a href="/p/Qgil/" target="_blank">Qgil</a> added a subscriber: <a href="/p/Qgil/" target="_blank">Qgil</a>.</div></div></div></div></div><div id="anchor-4707"><div><div><div><div><div><a href="/p/Qgil/" target="_blank">Qgil</a> closed this task as Resolved.</div><a href="#" target="_blank">Comment Actions</a><div><div><p>This one is implemented as well. Sorry for the noise.</p></div></div></div></div></div></div></div><div id="anchor-19938"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p>In RT we actually use "Stalled" sometimes, with meaning which is quite different from "Needs Info". Needs Info implies we're waiting on someone to provide info to be able to make progress with a bug.</p>

<p>"Stalled" for us can mean things like:</p>

<ul>
<li>Waiting on a 3rd party to do/implement/deliver something (vendor or whatever)</li>
</ul>

<p>It's not really "needs info", it's also not blocked on a task we can resolve ourselves, but we can't make progress on this task either</p>



<ul>
<li>We're going to do this, we keep track of it, but the right time (or some other precondition) for it hasn't come yet</li>
</ul>

<p>For example, "decommission server X at date Y." Of course, in some such cases, being able to list the precondition (such as a defer date) in ticket metadata would be even better.</p>

<p>Since "Stalled" is more generic than "Info" and can be used for a wider variety of things, we'd still like to have this status available for our projects...</p></div></div></div></div></div></div></div><div id="anchor-19940"><div><div><div><div><a href="/p/mark/" target="_blank">mark</a> reopened this task as Open.<a href="#19940" target="_blank">Nov 7 2014, 4:15 PM</a></div></div></div></div></div><div id="anchor-19956"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p>Have you considered using column workboards for these specific conditions? Then the label of the column appears in the description of the task. Like here, above, you can see "(Need Discussion)" now, you would have al the flexibility to decide other conditions your tasks are stuck on i.e. "Stalled".</p>

<p>Also for what is worth, I have been thinking about proposing tags like "2015-03" to denote tasks that need to be acted upon at a certain point in the future, but not now.</p></div></div></div></div></div></div></div><div id="anchor-19959"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p>Hmm, maybe, we can experiment with it.</p>

<p>I do think that "Needs Info" is a rather specific case of a status for a ticket which can't progress, wouldn't it be better to use something more generic (like stalled)?</p></div></div></div></div></div></div></div><div id="anchor-19962"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p>I agree that "Needs Info" can be renamed to something more generic. Also, we put a lot of effort trying to reduce the number of options for Status and other selectors compared to Bugzilla, and this is why you can feel my resistance to add a new status. Nothing against RT practices personally.</p>

<p>So what about "Waiting". This would mark tasks as "Open, Waiting", showing clearly that even if the task is assigned and has "Unbreak Now!" priority (hypothetical extreme case", the owner explicitly cannot do anything but wait for another event. Then we can define the reason for the wait via tags or workboard columns, tbd and in the ways that works better for every team.</p>

<p><a href="/p/Aklapper/" target="_blank">@Aklapper</a>, does this work for you?</p></div></div></div></div></div></div></div><div id="anchor-19966"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p>In my brain "Needs info" vaguely translates to "blocked on somebody or something" which is close enough to "Stalled" or "Waiting". Both works for me.</p>

<p>We need to document that well, otherwise people might come up with interpretations like "I'm waiting for a developer to take a look at this and fix this!!!" or such. ;)</p></div></div></div></div></div></div></div><div id="anchor-20645"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p>The (small) problem I see with "Stalled" is that it is a bit of an idiom that might confuse our international and/or non-tech userbase.</p>

<p>A synonym of Stalled that would rhyme with Resolved, and Declined is "Paused". The more I see it, the better I prefer it over "Waiting". What do you think?</p>

<p>Whatever it is, will be decided latest by our meeting on Monday.  :)</p></div></div></div></div></div></div></div><div id="anchor-20735"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p>"Paused" is an alternative, sometimes appropriate, other times it's not: "Paused" feels more voluntarily put in waiting than "Stalled" does. But sometimes that's exactly what we want/mean.</p>

<p>I don't particularly care that much, and I don't want to get into bikeshedding over this. All of this is better than the more specific "Needs info" IMHO.</p></div></div></div></div></div></div></div><div id="anchor-20737"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p>FWIW I would just go w/ stalled.  We already use it in one of the originating import system cases, and if it is truly an issue we can revisit at a later date.</p></div></div></div></div></div></div></div><div id="anchor-20742"><div><div><div><div><a href="#" target="_blank">Comment Actions</a><div><div><p>Stalled, then. Moving on. Thanks!</p></div></div></div></div></div></div></div><div id="anchor-20744"><div><div><div><div><a href="/p/Qgil/" target="_blank">Qgil</a> closed this task as Resolved.<a href="#20744" target="_blank">Nov 10 2014, 3:09 PM</a></div></div></div></div></div></div><div><a href="/login/?next=" target="_blank">Log In to Comment</a></div></div></div></div></div></div><div>Content licensed under Creative Commons Attribution-ShareAlike 3.0 (CC-BY-SA) unless otherwise noted; code licensed under GNU General Public License (GPL) or other open source licenses. By using this site, you agree to the Terms of Use, Privacy Policy, and Code of Conduct. · <a href="https://www.wikimediafoundation.org/" target="_blank">Wikimedia Foundation</a> · <a href="https://wikimediafoundation.org/wiki/Privacy_policy" target="_blank">Privacy Policy</a> · <a href="https://www.mediawiki.org/wiki/Code_of_Conduct" target="_blank">Code of Conduct</a> · <a href="https://wikimediafoundation.org/wiki/Terms_of_Use/Phabricator" target="_blank">Terms of Use</a> · <a href="https://wikimediafoundation.org/wiki/Wikimedia:General_disclaimer" target="_blank">Disclaimer</a> · <a href="https://creativecommons.org/licenses/by-sa/3.0/" target="_blank">CC-BY-SA</a> · <a href="https://www.gnu.org/licenses/old-licenses/gpl-2.0.html" target="_blank">GPL</a></div></div></div></div><div><h3>Like On Github</h3><div><div>*Title (label for the link)</div></div><div><div>*Comment (commit message)</div></div><div id="action-btns"><div id="logh_btn_save">Saving...</div><div id="logh_btn_cancel">Cancel</div></div></div>
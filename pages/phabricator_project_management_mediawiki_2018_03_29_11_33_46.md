<a href="https://www.mediawiki.org/wiki/Phabricator/Project_management">https://www.mediawiki.org/wiki/Phabricator/Project_management</a><div id="articleHeader"><h1>Phabricator/Project management</h1></div>			
								<div id="contentSub">&lt; <a href="/wiki/Phabricator" title="Phabricator" target="_blank">Phabricator</a></div>
								
				<p>You have a <a href="/wiki/Phabricator/Requesting_a_new_project" title="Phabricator/Requesting a new project" target="_blank">project</a> in Phabricator that you maintain or manage. Now what? There are many possible ways to run a project successfully. This document focuses on the common expectations for Wikimedia projects. Following this guideline should help you being productive and interacting better with other contributors and projects in the Wikimedia community.
</p>


<h2>Why use Phabricator for managing your project?[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=1" title="Edit section: Why use Phabricator for managing your project?" target="_blank">edit</a>]</h2>
<p><a href="/wiki/Wikimedia_Engineering" title="Wikimedia Engineering" target="_blank">Wikimedia engineering teams</a> and Wikimedia-related projects are encouraged to use Phabricator for managing their project(s). This keeps projects more visible by managing them in the same place as one another as well as where issues are reported. This also makes collaborating between and across teams easier, as it is trivial for tasks to be shared and moved around from team to team, project to project. Further, it is particularly valuable to be able to manage your workflow in the same place where bugs/issues are reported. This eliminates the need for hacks like <a href="https://wikitech.wikimedia.org/wiki/Bingle" title="wikitech:Bingle" target="_blank">Bingle</a> and keeps the visibility of bugs/issues high by not spreading teams' focus across multiple tools.
</p><p>Phabricator is an open source project primarily written in PHP. Patches to Phabricator are <a href="/wiki/Phabricator/Code" title="Phabricator/Code" target="_blank">welcome after discussion</a>. :)
</p>
<h2>Tasks[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=2" title="Edit section: Tasks" target="_blank">edit</a>]</h2>
<p>Tasks are the basic building block of Phabricator. A Phabricator task is something that can define things like bugs, user stories, feature requests, etc. While a task can represent different kinds of things, all tasks have certain properties, like title, author (creator), assignee, description, projects/tags, etc. Unlike many other project management and issue tracking tools, a task can have a one-to-many relationship with 'projects' - that is, a single task can be associated with more than one 'project'.
</p>
<h3>Scope of tasks[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=3" title="Edit section: Scope of tasks" target="_blank">edit</a>]</h3>
<p>The basics: <a href="/wiki/Phabricator/Help#Creating_a_task" title="Phabricator/Help" target="_blank">Phabricator/Help#Creating a task</a>.
</p><p>Tasks need to describe an achievable objective. Ideally, tasks are defined with a scope that can be resolved by one person with a decent amount of effort. Huge tasks that take several people and several days will be more manageable when you identify the subtasks required to complete them. Trivial subtasks that one person can complete in a moment but should be documented can be just added as a checklist in a description of the main task. A good principle to follow is that a task should be completable within a single iteration - for teams/individuals not working with iterations, think ~2 weeks maximum. If a task is larger than this, it should be broken down into smaller tasks. Also consider this piece of advice: does your task require more than a couple of hours of work? Then you may want to add it to Phabricator. Would there be nasty consequences if you forgot executing that task? Avoid this by adding it to Phabricator.
</p><p>Team-level goals are often called "Epics". There is an "<a href="https://phabricator.wikimedia.org/tag/epic/" title="phab:tag/epic/" target="_blank">epic</a>" tag, which is used for <a href="/wiki/Wikimedia_Engineering/2015-16_Q1_Goals" title="Wikimedia Engineering/2015-16 Q1 Goals" target="_blank"> goals identified in the quarterly planning process of the Wikimedia Foundation</a>.
There is also a "<a href="https://phabricator.wikimedia.org/tag/release" title="phab:tag/release" target="_blank">release</a>" tag for identifying software releases.
</p>
<h4>Invalid tasks[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=4" title="Edit section: Invalid tasks" target="_blank">edit</a>]</h4>
<p>If a task fails defining an actionable objective (e.g. never-ending tasks, support questions, generic complaints...) they might be resolved as Invalid. Users resolving a task as Invalid should explain their reasons in a comment (also see the <a href="/wiki/Bug_management/Bug_report_life_cycle" title="Bug management/Bug report life cycle" target="_blank">Bug report life cycle</a>). Tasks are fully editable, and if the causes for the Invalid resolution have been addressed, they can be reopened.
</p>
<h3>Use plain language, define actions and expected results[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=5" title="Edit section: Use plain language, define actions and expected results" target="_blank">edit</a>]</h3>
<p>Since tasks are the primary building block of Phabricator and they are generally public and visible to everyone, they are valuable ways of communicating not just with people who will be completing the work, but with other stakeholders as well. It is considered best practice to keep tasks written as plainly as possible - in language that can generally be understood by most people. One easy way to achieve this is by describing an action taken (or to be taken) and the desired (or expected) result - and there's a handy pattern for achieving this known as <a href="https://en.wikipedia.org/wiki/Given-When-Then" title="w:Given-When-Then" target="_blank">'given/when/then'</a>. As an example:
</p>
<pre>Given that I am viewing an article on English Wikipedia and am not logged in,
When I click the link from the left navigation that says 'Random',
Then I am taken to a random article on English Wikipedia in the main namespace.
</pre>
<p>In the case of a bug, say 'Random' link isn't working, you could include the language above and add to it:
</p>
<pre>This is not currently working as expected. Clicking the 'random' link from the left
navigation menu currently takes me to the article 'Entropy' every single time I
click on it. However, when I am logged in, the 'random' link works as expected'.
</pre>
<p>As opposed to:
</p>
<pre>Special:Random is broken
</pre>
<p>The former example is generally understandable by anybody, the latter may only make sense to a MediaWiki software engineer who is intimately familiar with Special:Random. Of course you do not need to follow the formula specifically if you don't want to, but hopefully the examples make the principle clear: define tasks in simple language and in a way that can be understood by a broad audience. Also see <a href="/wiki/How_to_report_a_bug" title="How to report a bug" target="_blank">How to report a bug</a>.
</p>
<h3>Assigning tasks[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=6" title="Edit section: Assigning tasks" target="_blank">edit</a>]</h3>
<p>In principle, a task gets assigned to whomever will take ownership of it. Even in formal teams with a product owner, the idea is that the project owner says what needs to get done, and the team itself figures out whom will work on what.
</p><p>You should have a task assigned to yourself only when you are prepared to work on it. There is no use in having tasks assigned that haven't been or won't be touched for a long time. See also: <i><a href="https://en.wiktionary.org/wiki/cookie_licking" title="wiktionary:cookie licking" target="_blank">cookie licking</a></i>.
</p>
<h3>Setting task priorities[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=7" title="Edit section: Setting task priorities" target="_blank">edit</a>]</h3>
<p>One task can have only one set priority at a time. Priority should normally be set by product managers, maintainers, community liaisons, or developers who plan to work on the task, or by the <a href="/wiki/Bugwrangler" title="Bugwrangler" target="_blank">bugwrangler</a> or experienced community members, <i>not by the reporter filing the bug report or by outside observers</i>. When in doubt, do not change the Priority field value, but <a href="/wiki/Bug_management/Phabricator_etiquette" title="Bug management/Phabricator etiquette" target="_blank">add a comment suggesting the change and convincing reasons for it</a>.
</p><p>When an assignee is already set for a task, its priority should not be changed without agreement of the assignee or development team first.
</p><p>In the event the priority of a task is repeatedly and inappropriately set, the task may become protected and made modifiable only by specific people.
</p>
<h4>Priority levels[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=8" title="Edit section: Priority levels" target="_blank">edit</a>]</h4>
<dl><dd><i>See also <a href="/wiki/Language_portal/Task_Priority" title="Language portal/Task Priority" target="_blank">Language portal/Task Priority</a> and other <a href="/wiki/Special:Search/priority_incategory:%22Wikimedia_Foundation_teams_internals%22" title="Special:Search/priority incategory:"Wikimedia Foundation teams internals"" target="_blank">Wikimedia Foundation teams internals</a></i>.</dd></dl>
<p>Wikimedia Phabricator offers these priority levels to allow developers to plan their work:
</p>
<ul><li>Needs Triage - Default option, signaling that the priority has not yet been determined.</li>
<li>Unbreak Now! - Something is broken and needs to be fixed immediately, setting anything else aside.</li>
<li>High - Someone is working or planning to work on this task soon.</li>
<li>Normal - Less priority than High, but someone is still planning to work on it.</li>
<li>Low - Less priority than Normal, but someone is still planning to work on it. This does not necessarily mean the task is not important; it is just not on the to-do list of anybody as the task is not considered urgent.</li>
<li>Lowest - Nobody plans to work on this task, but we would be happy if someone does.</li></ul>
<p>Usually the tricky part is to handle High - Normal - Low in a consistent way, especially for tasks that are still unassigned. One way to approach this for development teams:
</p>
<ul><li>High priority for tasks committed for the current <a href="#Scrum_in_Phabricator" target="_blank">sprint</a>, or that need to find an owner who can start working on them soon.</li>
<li>Normal priority for tasks that are not critical for the current sprint or candidates for a next sprint.</li>
<li>Low priority for tasks that we can live without, usually sitting in the backlog, sometimes added to a sprint.</li></ul>
<h4>Limiting high priority tasks assigned to a single person[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=9" title="Edit section: Limiting high priority tasks assigned to a single person" target="_blank">edit</a>]</h4>
<p>While priority setting and assignment are generally up to teams and individuals to figure out, it is not appropriate for a single person to be assigned more than a few open High priority tasks. As a <a href="https://en.wikipedia.org/wiki/Rule_of_thumb" title="w:Rule of thumb" target="_blank">rule of thumb</a>, limit High priority task assignments for a single person to three, five in exceptional times.
</p>
<h3>Associating tasks with projects[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=10" title="Edit section: Associating tasks with projects" target="_blank">edit</a>]</h3>
<p>A task in Phabricator can be associated with multiple 'projects'. Any Phabricator user will be able to create a task in a 'project' corresponding to the old bugzilla "Component", for example <i>MediaWiki-extensions-Flow.</i> The one task can be associated with additional 'projects': tags such as <i>easy</i> or <i>design</i>, and project management boards such as <i>Flow-design-backlog</i> or <i>sprint-Flow-current</i>.
</p>
<h3>Tasks that cannot be worked on yet[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=11" title="Edit section: Tasks that cannot be worked on yet" target="_blank">edit</a>]</h3>
<div>See also: <a href="/wiki/Phabricator/Help#Parent_tasks_and_subtasks" title="Phabricator/Help" target="_blank">Phabricator/Help#Parent_tasks_and_subtasks</a></div>
<p>Certain tasks might not be <i>actionable</i> until an action has been performed outside of the task itself. 
</p><p>If a task depends on another task in Phabricator, you should set the number of that other task under "Edit Related Tasks... &gt; Edit Subtasks". Afterwards, the other (sub)task will be displayed under "Task Graph".
</p><p>If a task depends on a third party (e.g. upstream developers or further information from the reporter which has not responded), you can explicitly set the status to "stalled" (also see the <a href="/wiki/Bug_management/Bug_report_life_cycle" title="Bug management/Bug report life cycle" target="_blank">Bug report life cycle</a>).
</p>
<h3>Tasks which have a deadline[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=12" title="Edit section: Tasks which have a deadline" target="_blank">edit</a>]</h3>
<p>You can create a task with a due date by using <a href="https://phabricator.wikimedia.org/maniphest/task/edit/form/37/" title="phab:maniphest/task/edit/form/37/" target="_blank">this form</a> however note that <a href="https://phabricator.wikimedia.org/T76094#3454607" title="phab:T76094" target="_blank">this is still work in progress</a>.
</p>
<h3>Closing a task[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=13" title="Edit section: Closing a task" target="_blank">edit</a>]</h3>
<p>A task can be closed as Resolved, Declined, or Invalid. It can also be merged as a duplicate of another task (<a href="/wiki/Bug_management/Bug_report_life_cycle" title="Bug management/Bug report life cycle" target="_blank">details</a>). When a task is associated with multiple projects, care should be taken to coordinate the closing of a task with any relevant stakeholders. Anyone marking a task as declined or invalid should include a comment explaining why. 
</p><p>Many (but not all) tasks relate to projects that have specific "owners", such as a volunteer maintainer, or a team within the foundation. That owner would most often be responsible for updating the status of tasks within their project, and they might rely on a specific workflow. For example, marking a task "resolved" might mean that a patch has been merged, or that the product owner has verified the fix, or that the change has been deployed to production. The owner would also typically be in the best position to determine that the task should (or should not) be marked as declined or invalid. 
</p><p>In some cases, it would be appropriate for the task's status to be updated by someone other than the task's owner, such as the task author, a phabricator administrator, or an observer. But generally the owner of a task, if there is one, should have the final say on its status. For tasks that don't have a clear owner, the task author should generally be consulted about potentially controversial status changes. 
</p><p>In the event a task is repeatedly closed inappropriately, the task may become protected and made closable only by specific people.
</p>
<h3>See also[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=14" title="Edit section: See also" target="_blank">edit</a>]</h3>
<ul><li><a href="/wiki/Bug_management/Bug_report_life_cycle" title="Bug management/Bug report life cycle" target="_blank">Bug management/Bug report life cycle</a></li></ul>
<h3>Creating custom forms for Task Creation and Editing[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=15" title="Edit section: Creating custom forms for Task Creation and Editing" target="_blank">edit</a>]</h3>
<p>Phabricator allows <a href="https://phabricator.wikimedia.org/people/query/DktdoFyuGYMN/#R" target="_blank">Phabricator administrators</a> to create custom forms for task creation and editing. <a href="https://secure.phabricator.com/book/phabricator/article/forms/" target="_blank">Upstream documentation is available</a> and <a href="https://phabricator.wikimedia.org/maniphest/task/edit/form/17/" title="phab:maniphest/task/edit/form/17/" target="_blank">a custom form just to demonstrate the possibility is available.</a>
</p><p>Some likely use cases include:
</p>
<ul><li>Custom markup at the top of forms</li>
<li>Pre-filling information in fields</li>
<li>Hiding certain fields</li>
<li>Bug reporting and template tasks can be entered more easily</li></ul>
<p>A great deal of caution is required when using this new functionality. Form creation is limited to administrators because it is currently too easy to accidentally override existing forms when someone creates a new form without fully understanding the subtleties of the new system. Anyone with a use-case for a custom form can <a href="https://phabricator.wikimedia.org/maniphest/task/edit/form/17/?projects=Phabricator" target="_blank">request that one be set up by Phabricator administrators</a>. We have not established a formal process for this yet.
</p>
<h2>Projects[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=16" title="Edit section: Projects" target="_blank">edit</a>]</h2>
<div>See also: <a href="/wiki/Phabricator/Projects" title="Phabricator/Projects" target="_blank">Phabricator/Projects</a></div>
<p>Projects are the basic organizational method in Phabricator; they are a way to organize tasks and manage workflow or to "tag" for queries and general organization.  
</p><p>You might <a href="/wiki/Phabricator/Creating_and_renaming_projects" title="Phabricator/Creating and renaming projects" target="_blank">create a project in Phabricator</a> to organize all of the work and workflow for a particular product, a single iteration or work sprint for your team, to provide a custom view for tasks in a bunch of other Projects, etc. In short, a Project in Phabricator is simply a tag that can be applied to tasks, which you can then use to visualize and track those tasks in different ways.
</p><p>Since February 2016, Phabricator supports nested projects (subprojects, see below), so Projects do not have to be at the top level anymore. Naming conventions are used to communicate the intention of hierarchical relationships. 
</p>
<h3>Types of Projects[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=17" title="Edit section: Types of Projects" target="_blank">edit</a>]</h3>
<p><a href="/wiki/File:Phabricator_project_labels_6.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="//upload.wikimedia.org/wikipedia/commons/0/09/Phabricator_project_labels_6.png"   alt="Phabricator project labels 6.png" /></div></a>
</p><p>There are several types of top-level Projects in Wikimedia Phabricator. Each type must follow the purpose, color, and icon defined in these guidelines.
</p>
<ul><li>Types you can <a href="/wiki/Phabricator/Creating_and_renaming_projects#Creating_new_projects" title="Phabricator/Creating and renaming projects" target="_blank">directly create as a member of Project-Admins</a>:
<ul><li><b>Component</b> is the default option. A component corresponds to a distinct and recognizable piece of software, service, event or any set of periodically occurring tasks of the same type (ie. access or any other requests). If you are unsure, go for this. <i>Icon+Color: Briefcase+Blue.</i>
<ul><li><b>Umbrella</b> Projects could be used for larger Projects that do not have a distinct code base and that consist of several (sub)components. Umbrella Projects can be automatically added to (sub)component tasks by <a href="/wiki/Phabricator/Help#Global_Herald_rules" title="Phabricator/Help" target="_blank">requesting a global Herald rule</a>. <i>Icon+Color: Umbrella+Blue.</i></li></ul></li>
<li><b>Group</b> (formerly <b>Team</b>) corresponds to an existing team. If you belong to a group that will manage several projects, then create a Project for your group. Group Projects can be automatically added to (sub)component tasks by <a href="/wiki/Phabricator/Help#Global_Herald_rules" title="Phabricator/Help" target="_blank">requesting a global Herald rule</a>. <i>Icon+Color: Group+Violet.</i></li>
<li><b>Goal</b> can be used for Projects without a defined ending date but which can definitely realistically be defined as finished at some point. <i>Icon+Color: Goal+Orange.</i></li>
<li><b>User</b> (formerly <b>Personal</b>) Projects allow to track progress of personal tasks. They currently are a test only, see <a href="https://phabricator.wikimedia.org/T555" title="phab:T555" target="_blank">T555</a>. <i>Icon+Color: User+Checkered.</i></li></ul></li>
<li>Types that must <a href="https://phabricator.wikimedia.org/maniphest/task/create/?projects=Project-Creators" target="_blank">be proposed and discussed before being created</a>:
<ul><li><b>Tag</b> is used as a cross-component keyword (like "accessibility"), a "never-ending" project. <i>Icon+Color: Tag+Yellow</i></li>
<li><b>ACL</b> projects are used to enforce policy restrictions, especially for <a href="/wiki/Phabricator/Creating_and_renaming_projects#Restricting_access_via_Space_policies" title="Phabricator/Creating and renaming projects" target="_blank">Spaces</a>. This type should be used instead of locking down normal projects such as Teams, so that anyone may still join and <a href="/wiki/Phabricator/Help#Receiving_updates_and_notifications" title="Phabricator/Help" target="_blank">watch</a> such Team projects. See <a href="https://phabricator.wikimedia.org/T90491" title="phab:T90491" target="_blank">T90491</a>. <i>Icon+Color: Policy+Red.</i></li></ul></li>
<li>Types deprecated by <a href="/wiki/Phabricator/Project_management#Parent_Projects.2C_Subprojects_and_Milestones" title="Phabricator/Project management" target="_blank">Milestones</a> (there can still be valid reasons to have such "detached" top-level projects though, <a href="/wiki/Phabricator/Creating_and_renaming_projects/Project_types" title="Phabricator/Creating and renaming projects/Project types" target="_blank">if milestones do not fulfill your needs</a>):
<ul><li><b>Sprint</b> is used for projects of a team being worked on in a certain time frame. Specify the start and end dates. Unless the extra flexibility (and subsequent manual maintenance) of a separate detached Sprint project is needed, it is recommended to create a <a href="/wiki/Phabricator/Project_management#Parent_Projects.2C_Subprojects_and_Milestones" title="Phabricator/Project management" target="_blank">Milestone</a> of the sprint's parent project, instead of a separate detached Sprint project. <i>Icon+Color: Timeline+Green.</i></li>
<li><b>Release</b> is for planning a specific deployment of a project, defined by a date or a (future) software version. Unless the extra flexibility (and subsequent manual maintenance) of a separate detached Sprint project is needed, it is recommended to create a <a href="/wiki/Phabricator/Project_management#Parent_Projects.2C_Subprojects_and_Milestones" title="Phabricator/Project management" target="_blank">Milestone</a> of the release's parent project, instead of a separate detached Release project. <i>Icon+Color: Release+Orange.</i></li></ul></li>
<li>Special cases (only listed for completeness):
<ul><li>The <b>Patch-For-Review</b> project is automatically added to a task <a href="/wiki/Gerrit/Commit_message_guidelines" title="Gerrit/Commit message guidelines" target="_blank">when a related patch in Gerrit links to that task</a>.</li>
<li><b>Meta</b> projects are used to tag code repositories with special behaviors and workflows. These behaviors are triggered by custom <a href="/wiki/Phabricator/Help/Herald_Rules" title="Phabricator/Help/Herald Rules" target="_blank">Herald rules</a>. See <a href="https://phabricator.wikimedia.org/T128161" title="phabricator:T128161" target="_blank">task T128161</a>. Icon+color: Meta (gears)+Grey.</li></ul></li></ul>
<p>The icons and colors associated with different types of Projects are a convention, not enforced by software.
</p>
<h3>Parent Projects, Subprojects and Milestones[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=18" title="Edit section: Parent Projects, Subprojects and Milestones" target="_blank">edit</a>]</h3>
<p>Phabricator provides Subprojects and Milestones as special cases of Projects. The <a href="https://secure.phabricator.com/book/phabricator/article/projects/#subprojects-and-mileston" target="_blank">upstream documentation provides great detail.</a> To create a subproject or milestone, you must do so through its parent project. From the project that you want to become the parent, click on the subprojects icon in the left navbar. From there, you should see options to create a subproject or milestone. Converting an existing project to become a subproject or milestone requires shell access on the Phabricator server.
</p>
<div>
<table>
<tbody><tr>
<th>[<a target="_blank">Expand</a>]<a href="/wiki/Phabricator/Creating_and_renaming_projects/Project_types" title="Phabricator/Creating and renaming projects/Project types" target="_blank">Feature comparison for projects, subprojects, milestones, and workboard columns</a>   
</th>
</tr></tbody></table></div>
<p><b>Here are some highlights:</b> 
</p>
<ul><li>Searching
<ul><li>Searching for a parent project also returns results from the subprojects.</li></ul></li>
<li>Users and members
<ul><li>Membership in a project ("joining") is different from subscribing. Subscribing to a project is sufficient to get notifications, so actual membership might not be needed.</li>
<li>Subprojects, and projects that don't have subprojects, can have members.</li>
<li>Projects that are parents of subprojects cannot specify members. Instead, the members of all its subprojects are treated as being is members.</li>
<li>Milestones (which are NOT considered subprojects) cannot specify members. Instead, the members of its parent project are treated as being its members.</li>
<li>If a project has no subprojects, but then one is added, the existing Project becomes a “parent” Project and all of its members shift to that first Subproject.</li></ul></li>
<li>Data Modelling
<ul><li>Subprojects can have their own Subprojects (up 16 subprojects deep).</li>
<li>Parent projects can have their own tasks.</li>
<li>Subprojects at the same level can share tasks.</li>
<li>Subprojects on different levels in different subproject hierarchies can share tasks.</li>
<li>Tasks in Milestones can only be in one Milestone.</li></ul></li>
<li>Interface and workboards
<ul><li>Subprojects and Milestones have their own workboard.</li>
<li>Milestones exist as columns within the subproject's workboard.</li>
<li>Milestones will show up in the board of the associated subproject.</li></ul></li></ul>
<h4>Converting projects into subprojects / milestones[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=19" title="Edit section: Converting projects into subprojects / milestones" target="_blank">edit</a>]</h4>
<p>To request conversion of one or more projects, please <a href="https://phabricator.wikimedia.org/maniphest/task/edit/form/1/?tags=Project-Admins&title=Convert+{My+Project}+to+milestone+of+{Parent+Project}" target="_blank">file a task</a> and be sure to include these crucial details:
</p>
<ul><li>The name of the project which will become the parent project</li>
<li>The names of projects that should be converted</li>
<li>For each of the converted projects, describe whether it should be a subproject or a milestone.</li>
<li>If the converted project will become a milestone:
<ul><li>Milestones cannot have members, therefore, what should happen to the members of that project? There are two choices:
<ul><li>Either the members get added to the parent project, or</li>
<li>The list of members is discarded when the project becomes a milestone.</li></ul></li></ul></li></ul>
<h3>Creating and renaming projects[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=20" title="Edit section: Creating and renaming projects" target="_blank">edit</a>]</h3>
<p>The basics: <a href="/wiki/Phabricator/Creating_and_renaming_projects" title="Phabricator/Creating and renaming projects" target="_blank">Phabricator/Creating and renaming projects</a>.
</p><p>Projects are <a href="/wiki/Phabricator/Project_management/Tracking_tasks" title="Phabricator/Project management/Tracking tasks" target="_blank">favored over 'tracking tasks' with dependencies</a>.
</p>
<h3>Archiving a project[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=21" title="Edit section: Archiving a project" target="_blank">edit</a>]</h3>
<p>If/when your Project is complete, abandoned, or otherwise no longer active, it should be archived. This prevents clutter and signals to others that the Project is inactive.
</p><p>Assuming you have appropriate permissions, to archive a Project:
</p>
<ol><li>go to your Project page (e.g. <a href="https://phabricator.wikimedia.org/tag/phabricator/" title="phab:tag/phabricator/" target="_blank">https://phabricator.wikimedia.org/tag/phabricator/</a>);</li>
<li>click the <b>Manage</b> item in the navigation bar on the left;</li>
<li>click <b>Archive Project</b>.</li></ol>
<p>Make sure to handle the <i>open tasks</i> of your archived Project: Either associate the tasks with at least one other active Project, or close the tasks as declined in combination with an explanatory comment.
</p><p>If your archived Project has been <i>superseded</i> by another Project, click <b>Edit Details</b> and edit the task description accordingly, This allow others to find the newer Project.
</p><p>It is not possible to delete a Project in Phabricator.
</p>
<h2>Boards[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=22" title="Edit section: Boards" target="_blank">edit</a>]</h2>

<p>The workboard is the primary user interface for viewing and manipulating tasks that belong to a project.  Projects which are used solely as supplemental "flags", for example <a href="https://phabricator.wikimedia.org/project/view/156/" target="_blank">i18n</a>, may not use their boards.  Boards are useful to follow the development status of tasks within a 'project'. Keep in mind that boards are not just a means of managing the flow of work. It's a communication tool both for your team/project/etc as well as to the public/stakeholders/etc. Boards should be used and maintained with this in mind; the simpler and clearer the language used, as well as the clarity of organization of your board, the better for communicating to a broader audience (see <a href="#Use_plain_language,_define_actions_and_expected_results" target="_blank">#Use plain language, define actions and expected results</a>).
</p><p>Every 'project' has one single board. You can access it by clicking the Workboard icon in the left-side menu of the project. If there is no such icon, the board is disabled. You can enable it via "Manage" in the left-side menu and then choosing "Edit Menu" on the right.
</p>
<h3>Columns[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=23" title="Edit section: Columns" target="_blank">edit</a>]</h3>
<p>Project boards may display the tasks in the project in multiple columns.  A project that is itself used as a tag (<i>i18n</i>, <i><a href="https://phabricator.wikimedia.org/project/view/418/" title="phab:project/view/418/" target="_blank">Need-volunteer</a></i>) may not use its board and thus will not have columns.
</p><p>When you first set up the board for a project, you can choose "New Empty Board" which starts with a single "Backlog" column; or you can choose "Import board columns from another project" to use another board's set of columns as a starting point. Thereafter you can create arbitrary columns in the board such as <i>In development</i>, <i>Blocked with questions</i>, <i>Code review</i>, <i>Product review</i>, and <i>Done</i>.
Then much like other 'project' management tools you can drag and drop tasks within and between columns to recategorize them.  The order of tasks within each column is maintained, and you can drag and drop tasks up and down, so it is common to treat this as another kind of prioritization or stack ranking.  A task can belong to only one column within each board.
</p><p>In Phabricator a project can only have one board, but a task can be in multiple projects each with its own board. In comparison Mingle directly supports identifying tasks in the current sprint, and in Trello it's common to have separate boards for the current sprint and backlog, or even a separate board for each sprint.
</p><p>The default board filter only shows "Open Tasks", but you can change Filter to "All Tasks" or "Assigned to Me", or a custom filter.
</p>
<div><div><a href="/wiki/File:Phabricator_column_numbers_screenshot.png" target="_blank" class="readableLinkWithMediumImage"><img src="//upload.wikimedia.org/wikipedia/commons/thumb/e/eb/Phabricator_column_numbers_screenshot.png/220px-Phabricator_column_numbers_screenshot.png" width="220" height="188" /></a>  <div>The top example is a column that has 29 tasks, with 145 story points. The bottom example has 4 tasks, with 8 story points out of a maximum of 1 story point.</div></div></div>
<p>Each column has two numbers at the top, number of cards, and current "story point" count. If the column has a story point restriction (i.e. "this column should have a maximum of 20 story points between all tasks") then it will show the second number as a fraction (current over maximum). When the points exceed the limit, the numbers turn red.
</p><p>It is not possible to delete a column, however you can hide a column.
</p>
<h3>Typical uses of workboards[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=24" title="Edit section: Typical uses of workboards" target="_blank">edit</a>]</h3>
<ul><li>Workflow
<ul><li>Typical columns track the state of tasks, such as TODO, DOING, DONE.</li>
<li>This supports both Scrum-style sprint iterations, and Kanban-style continuous work.</li>
<li>An example is <i><a href="https://phabricator.wikimedia.org/project/view/1729/" title="phab:project/view/1729/" target="_blank">Dumps-Rewrite</a></i>, with <i>Tracking</i>, <i>Up Next</i>, <i>active</i>, etc.</li>
<li>Usually the Phabricator built-in states are integrated with the columns in that all tasks are kept <i>open</i> until they reach a terminal column, after which they are <i>resolved</i>.</li>
<li>Tasks are moved from column to column regularly as work progresses.</li></ul></li>
<li>Planning
<ul><li>These boards divide tasks into temporal or sequential categories.</li>
<li>Each column might represent a target release (<i>version 2</i>), or general timeframe (e.g. <i>2016</i>).</li>
<li>Tasks generally don't change columns other than in re-planning.  Thus they will change from <i>open</i> to <i>resolved</i> without moving columns.</li></ul></li>
<li>Categories
<ul><li>Columns might group Tasks by component, functional area, or even complexity</li>
<li>An example of sub-categorization is <i><a href="https://phabricator.wikimedia.org/project/view/372/" title="phab:project/view/372/" target="_blank">Mobile</a>, which has as columns </i>Needs triage<i>, </i>Not MobileFrontend specific<i>, and </i>MobileFrontend Specific<i>.  Note that this blends a little bit of state with the categorization, which is very common.</i></li></ul></li></ul>
<h4>Examples[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=25" title="Edit section: Examples" target="_blank">edit</a>]</h4>
<p>Good examples that you can use to import your own board (you can also create your own columns, but check out these alternatives before):
</p>
<ul><li>Backlog, Need Discussion, Ready To Go, Doing (links to examples)</li>
<li>Backlog, Doing, Review, Done (<a href="https://phab08.wmflabs.org/project/sprint/board/15/query/all/" target="_blank">Test instance</a>)</li>
<li>To Do, In Progress, In Review, Done</li>
<li>Sprint X (X is different for each sprint board), In Development, Code Review, Product Review, <a href="/wiki/Scrum_of_scrums" title="Scrum of scrums" target="_blank">Scrum-of-scrums</a> interdependencies (<a href="https://phabricator.wikimedia.org/project/sprint/board/1050/" title="phab:project/sprint/board/1050/" target="_blank">Collaboration-Team</a>)</li>
<li>Backlog, Needs plan, Needs Code, Non-Code, Non-core-API stuff, In Dev, Needs Review (<a href="https://phabricator.wikimedia.org/tag/MediaWiki-API/" title="phab:tag/MediaWiki-API/" target="_blank">MediaWiki-API</a>; <a href="https://phabricator.wikimedia.org/T90003" title="phab:T90003" target="_blank">T90003</a>)</li>
<li>Please add more</li></ul>
<h4>Tips for forcing multiple columns to fit in the window[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=26" title="Edit section: Tips for forcing multiple columns to fit in the window" target="_blank">edit</a>]</h4>
<p>If the workboard has many columns, it might not all fit in your screen. This makes dragging tasks between columns more difficult (although you can use your keyboard's arrow-keys to scroll sideways), and seeing all the columns at once impossible. Here are two ways to override the default display
</p><p>Using <a href="https://userstyles.org/styles/120549/phabricator-show-all-workboard-columns-on-screen" target="_blank">Stylish/userstyles.org</a> in any browser.
</p><p>Using <a href="https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/" target="_blank">Greasemonkey</a> in Firefox:
</p>
<pre>GM_addStyle(".aphront-multi-column-fixed .phui-workpanel-view, .phui-workpanel-view .phui-header-shell { width: auto; }");
</pre>
<p>Using Firefox's <a href="http://kb.mozillazine.org/UserContent.css" target="_blank">userContent.css</a> (browser restart required):
</p>
<pre>@-moz-document domain(phabricator.wikimedia.org) {.aphront-multi-column-fixed .phui-workpanel-view, .phui-workpanel-view .phui-header-shell { width: auto !important; }}
</pre>
<p>Try using your <b>PageUp/PageDn keys while dragging a task</b>. (This seems to work well in Chrome on Linux but not in Firefox/Iceweasel.)
</p>
<h3>Maintaining Boards[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=27" title="Edit section: Maintaining Boards" target="_blank">edit</a>]</h3>
<p>In principle, people assigned to tasks of a 'project' are the ones managing the board of such 'project', and especially the position of the tasks they are working on. 
</p><p>Formal teams might have formal meetings to update the board, and they might also have a product/project owner in charge of keeping the Board up to date.
</p><p>There are 2 ways to move a task from one workboard column to another:
</p>
<ul><li>While viewing the workboard, drag the task and drop it in the destination column at a specific vertical position
<ul><li>NOTE: If you need to drag a card to a position in a column that is out of reach, you can click the card to hold it and, without leaving the mouse, scroll up/down with the arrow keys or two fingers in your touchpad.</li></ul></li>
<li>While viewing a task, choose the "Move on Workboard" action in a dropdown near the bottom</li></ul>
<p>The current implementation of Boards does <a href="https://secure.phabricator.com/T4900" target="_blank">not automatically update with task status changes</a>, so if you are viewing a workboard while other people are editing or moving tasks, you will have to user the refresh feature of the browser to see the updates. 
</p><p>Custom Board column to Status mapping <a href="https://secure.phabricator.com/T5474" target="_blank">may be possible in the future</a>...
</p>
<h2>Implementing Common Project Management Practices in Phabricator[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=28" title="Edit section: Implementing Common Project Management Practices in Phabricator" target="_blank">edit</a>]</h2>
<p>Phabricator can support all of the common development practices used with Wikimedia, with varying degrees of completeness.  See also <a href="/wiki/Phabricator/Wikimedia_Use_Cases_for_Phabricator" title="Phabricator/Wikimedia Use Cases for Phabricator" target="_blank">Wikimedia Use Cases for Phabricator</a>.
</p>
<h3>Legend for diagrams[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=29" title="Edit section: Legend for diagrams" target="_blank">edit</a>]</h3>
<p>Different colors represent different categories, compoments, or subprojects of a master project.  For example, "Database", "UI", "Reporting".  Each "category" may be a distinct Phabricator project, or a column within a project, or may just be a conceptual category that is tracked manually and through task titles.  
A white box with shaded black border represents the default column for new tasks, typically "To Triage".
In these examples, the colored bars represent lists of tasks, not single tasks of varying size.
</p>
<div><div><a href="/wiki/File:Mockup_of_task_board_with_different_columns.svg" target="_blank" class="readableLinkWithMediumImage"><img src="//upload.wikimedia.org/wikipedia/commons/thumb/1/1f/Mockup_of_task_board_with_different_columns.svg/220px-Mockup_of_task_board_with_different_columns.svg.png" width="220" height="124" alt="Mockup of task board with different columns.svg" /></a>  </div></div>
<p>Different shades of the same color represent tasks in progressive changes of status, such as "In design", "In development", "In Testing".
</p>
<div><div><a href="/wiki/File:Mockup_of_task_tracking_with_status_columns_and_legend.svg" target="_blank" class="readableLinkWithMediumImage"><img src="//upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Mockup_of_task_tracking_with_status_columns_and_legend.svg/220px-Mockup_of_task_tracking_with_status_columns_and_legend.svg.png" width="220" height="124" alt="Mockup of task tracking with status columns and legend.svg" /></a>  </div></div>
<p>Tasks are often prioritized within each column, with the most important to the top.
</p>

<h3>Single Board[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=30" title="Edit section: Single Board" target="_blank">edit</a>]</h3>
<h4>Simple List[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=31" title="Edit section: Simple List" target="_blank">edit</a>]</h4>
<p>The simplest way to use Phabricator to manage a project is as a to-do list.
</p>
<ul><li>Keep all tasks in one Project</li>
<li>Use the default column in the project to maintain a ranked list</li>
<li>Work from the top of the list.</li>
<li>Note that new tasks (including existing tasks that somebody else tags with this project) will mix with the existing list of tasks.  A separate default column would make this clearer.</li></ul>
<h4>Columns show status[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=32" title="Edit section: Columns show status" target="_blank">edit</a>]</h4>
<p>A team uses its Team Project Workboard to track workflow.  Each column on the board reflects a different, progressive status.  Tasks move through columns like INBOX, IN PROGRESS, IN REVIEW, and DONE.  Tasks added to the board default to a "To Triage" column at the left side.  Tasks are not systemically differentiated into categories, though tasks' other projects are visible as tags within the task boxes. Example: <a href="https://phabricator.wikimedia.org/project/view/1030/" title="phab:project/view/1030/" target="_blank">Analytics-Kanban</a>.  See below for more information on Kanban in Phabricator.
</p><p><a href="/wiki/File:Project_Board_with_status_column.svg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="//upload.wikimedia.org/wikipedia/commons/thumb/5/5c/Project_Board_with_status_column.svg/512px-Project_Board_with_status_column.svg.png"   alt="Project Board with status column.svg" /></div></a>
</p>
<h4>Columns show categories[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=33" title="Edit section: Columns show categories" target="_blank">edit</a>]</h4>
<p>A team uses its Team Project Workboard to track workflow.  Each column on the board reflects a different category of work within the overall project.  Tasks are moved to columns to indicate which category they belong to.  Task status is effectively binary, where open tasks are visible and resolved tasks are hidden.  Tasks do not usually change columns.  Tasks added to the board default to a "To Triage" column at the left side.  Example: <a href="https://phabricator.wikimedia.org/project/view/483/" title="phab:project/view/483/" target="_blank">VisualEditor</a>.
</p><p><a href="/wiki/File:Project_board_with_different_colored_columns.svg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="//upload.wikimedia.org/wikipedia/commons/thumb/7/75/Project_board_with_different_colored_columns.svg/512px-Project_board_with_different_colored_columns.svg.png"   alt="Project board with different colored columns.svg" /></div></a>
</p>
<h3>Multiple Boards[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=34" title="Edit section: Multiple Boards" target="_blank">edit</a>]</h3>
<p>Many teams and many products require more than one Project in order to efficiently organize their activity, because a workflow-oriented board is not well-suited for tracking and organizing future tasks and planning over a longer term.
</p><p>There are different implementations of this principle. Check these examples and choose the way that works best for you (more real examples are welcome)
</p>
<h4>One project board and one status board[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=35" title="Edit section: One project board and one status board" target="_blank">edit</a>]</h4>
<p>A team may use one board to track all tasks, with different columns showing different categories, and then use a second board to track status of work in progress.  The tasks may belong to both boards, or to just one board.
</p><p><a href="/wiki/File:Project_mockup_of_Scrum_boards.svg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="//upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Project_mockup_of_Scrum_boards.svg/512px-Project_mockup_of_Scrum_boards.svg.png"   alt="Project mockup of Scrum boards.svg" /></div></a>
</p>
<h4>One project board and one board per iteration.[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=36" title="Edit section: One project board and one board per iteration." target="_blank">edit</a>]</h4>
<p>A team may use one board to track all tasks, and then track status in a separate board, using a different status board for each iteration.  This is the most common configuration for Scrum (see the section below for more details).
</p><p>A team Project acts as default backlog, pushing some tasks to regular sprints: <a href="https://phabricator.wikimedia.org/project/view/11/" title="phab:project/view/11/" target="_blank">Analytics-Engineering</a>, <a href="https://phabricator.wikimedia.org/tag/engineering-community/" title="phab:tag/engineering-community/" target="_blank">Engineering-Community</a>.  In this mockup, tasks from different categories are all in one long Backlog column on the main board, in priority order by individual task.
</p><p><a href="/wiki/File:Project_board_with_multiple_sprints.svg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="//upload.wikimedia.org/wikipedia/commons/thumb/3/3a/Project_board_with_multiple_sprints.svg/512px-Project_board_with_multiple_sprints.svg.png"   alt="Project board with multiple sprints.svg" /></div></a>
</p><p>A team Project could also use different columns to track different categories, and sprint boards to track status:
</p><p><a href="/wiki/File:Project_board_with_multiple_sprint_boards.svg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="//upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Project_board_with_multiple_sprint_boards.svg/512px-Project_board_with_multiple_sprint_boards.svg.png"   alt="Project board with multiple sprint boards.svg" /></div></a>
</p>
<h4>One project board, different tags for components, and a status board.[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=37" title="Edit section: One project board, different tags for components, and a status board." target="_blank">edit</a>]</h4>
<p>A team may use one board to track all tasks, with additional tags to track each category, and then track status in a separate board.  In this diagram, the Project board shows all tasks from all categories in a single unified backlog column.  
</p><p><a href="/wiki/File:Project_board_with_per-category_projects_and_sprint_board.svg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="//upload.wikimedia.org/wikipedia/commons/thumb/5/5f/Project_board_with_per-category_projects_and_sprint_board.svg/512px-Project_board_with_per-category_projects_and_sprint_board.svg.png"   alt="Project board with per-category projects and sprint board.svg" /></div></a>
</p><p>If the categories are often used by other people outside the context of the team board, an admin can create a <a href="/wiki/Phabricator/Help/Herald_Rules#Global_Herald_rules" title="Phabricator/Help/Herald Rules" target="_blank">global Herald rule</a> so that tasks added directly to the subproject boards are automatically added to the parent board.
</p>
<h4>Other Designs[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=38" title="Edit section: Other Designs" target="_blank">edit</a>]</h4>
<ul><li>A team Project acts as default backlog, pushing some tasks to specialized categories: <a href="https://phabricator.wikimedia.org/tag/phabricator/" title="phab:tag/phabricator/" target="_blank">Phabricator</a>...</li></ul>
<h4>Other considerations[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=39" title="Edit section: Other considerations" target="_blank">edit</a>]</h4>
<p>If you know you will require more than one Project for your product, team, Project, etc.:
</p>
<ul><li>Use a top-level Project as your default backlog. This keeps it easy to find and will give you a place to maintain a basic level of prioritization, eg 'Cool-Project'.  This project should have a "To Triage" or other column as default that makes it clear when new tasks are added but have not yet been reviewed.</li>
<li>Use naming to group iterations, components, etc., eg 'Cool-Project-Sprint-1' or 'Cool-Project-Some-Component'</li>
<li>Consider the pros and cons of using subprojects and milestones.  These features are in flux in Phabricator and there are currently (May 2016) no recommendations for how best to use them. Refer to <a href="#Parent_Projects,_Subprojects_and_Milestones" target="_blank">#Parent Projects, Subprojects and Milestones</a> to understand pros and cons.</li></ul>
<h3>Kanban in Phabricator[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=40" title="Edit section: Kanban in Phabricator" target="_blank">edit</a>]</h3>
<p><a href="https://en.wikipedia.org/wiki/Kanban_(development)" title="w:Kanban (development)" target="_blank">Kanban</a> is a lean development approach. It focuses on limiting Work In Progress (work started but not done) and reducing "batch size" so more work gets accomplished faster.
</p><p>Phabricator's workboards can facilitate some parts of Kanban. Set up a column for each state of Work In Progress, leading to a Done column. You can set a story point limit for each column in workboard view &gt; Edit column &gt; Point Limit. Note that it is not a hard limit--there will just be a visual indicator at the top of the column if the sum of story points of open tasks exceeds the limit. 
</p><p>Phabricator doesn't yet support Kanban's <a href="https://en.wikipedia.org/wiki/Cumulative_flow_diagram" title="w:Cumulative flow diagram" target="_blank">w:Cumulative flow diagrams</a> showing cycle time and lead time. Experimental work is being done on this by <a href="/wiki/Phlogiston" title="Phlogiston" target="_blank">Phlogiston</a>.
</p>
<h4>Multiple boards in Kanban[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=41" title="Edit section: Multiple boards in Kanban" target="_blank">edit</a>]</h4>
<p>Very similar to the Simple Scrum case, the team might use its Project Workboard as a roadmap. The team could just create a single permanent Sprint Workboard to act as the Kanban (workflow) board forever, but it would probably be better to rotate out a new Kanban "Sprint" Project periodically (e.g. quarterly).
</p>
<h4>Examples[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=42" title="Edit section: Examples" target="_blank">edit</a>]</h4>
<p>The Analytics Engineering team has an<a href="https://phabricator.wikimedia.org/tag/analytics-kanban/" title="phab:tag/analytics-kanban/" target="_blank"> Analytics-Kanban</a> workboard with limits on the number of tasks in some columns. The <a href="https://phabricator.wikimedia.org/project/view/11/" title="phab:project/view/11/" target="_blank">Analytics-Backlog</a> board feeds into this.
</p>
<h3>Scrum in Phabricator[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=43" title="Edit section: Scrum in Phabricator" target="_blank">edit</a>]</h3>
<p>Some projects/teams organize their work around <a href="https://en.wikipedia.org/wiki/Sprint_(software_development)" title="w:Sprint (software development)" target="_blank">sprints</a> (also known as iterations). Sprints are of a fixed duration, usually somewhere between one and three weeks. In Phabricator, a sprint is a Project with some additional features. Before early 2016, support for sprints was handled by the Sprint Extension. However, Phabricator now natively allows tasks to have estimates. 
</p><p>You can optionally enter a numeric estimate of the amount of work a task represents in its Story Points field. ("Story points" is a common <a href="/wiki/Agile" title="Agile" target="_blank">Agile</a> software development term for an estimate.) For burndown or burnup charts, consider <a href="/wiki/Phragile" title="Phragile" target="_blank">Phragile</a> or <a href="/wiki/Phlogiston" title="Phlogiston" target="_blank">Phlogiston</a>. 
</p><p>A sprint project could be a subproject, a normal project, or a milestone. Milestones are relatively new, so they aren't used much yet. However, it is expected that most sprints would eventually be milestone projects. 
</p><p>Sprints are typically named "<i>ProjectOrTeam Name</i>-Sprint <i>StartDateOrNumber</i>"  At the start of a sprint, add tasks from your prioritized backlog(s) to the current sprint by adding the sprint's tag to each task's Projects field. When your sprint is complete, you can archive it. If you did not complete a task, add the next sprint's tag to its Projects field.
</p><p>One approach in Phabricator is to have a "SomeProjectX-currentSprint" project as well as "SomeProjectX", and add the former Project to those tasks in "SomeProjectX" which you plan to work on in that current sprint. 
</p>
<h4>Typical Scrum[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=44" title="Edit section: Typical Scrum" target="_blank">edit</a>]</h4>
<p>A team might use its Team Project Workboard as a roadmap, with columns like INBOX, NEXT SPRINT, THIS QUARTER, NEXT QUARTER, LATER. Then, at the start of each sprint, they would create a Sprint Project, and add to its Workboard the tasks representing the sprint backlog. By the end of each sprint, most of the tasks in that sprint's Workboard should be in the DONE column. Teams may change task state from ''open'' to ''resolved'' as tasks are moved to the DONE column or all at once at the end.  Old Sprint Projects would typically be archived (so would no longer be visible to normal users). 
</p><p>If the team has multiple sub-teams or components, each of those will have its own Workboard. The team might configure those Workboards to group tasks by category. It would be possible to set up roadmaps at that level, but managing multiple levels of roadmaps containing the same tasks could be redundant. In that case, one option would be to keep the low-level tasks at the component/sub-team level, and only bring Epics and <a href="/wiki/Phabricator/Help#.22Tracking.22_tasks" title="Phabricator/Help" target="_blank">"Tracking" Tasks</a> up to the team's main Workboard.
</p>
<h3>Examples from teams that actively use Phabricator workboards for project management[<a href="/w/index.php?title=Phabricator/Project_management&action=edit&section=45" title="Edit section: Examples from teams that actively use Phabricator workboards for project management" target="_blank">edit</a>]</h3>





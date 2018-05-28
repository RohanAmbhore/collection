<a href="http://guides.beanstalkapp.com/deployments/best-practices.html">http://guides.beanstalkapp.com/deployments/best-practices.html</a><div id="articleHeader"><h1>Deployments Best Practices</h1></div>

				

				<h2>Table of Contents<a href="#" title="Show detailed TOC" target="_blank">Toggle</a></h2>

				

				

<h2 id="introduction">Introduction</h2>
<p>This guide is aimed to help you better understand how to better deal with deployments in your development workflow and provide some best practices for deployments. Sometimes a bad production deployment can ruin all the effort you invested in a development process. Having a solid deployment workflow can become one of the greatest advantages of your team.</p>
<p>Before you start, I recommend reading our <a href="http://guides.beanstalkapp.com/version-control/branching-best-practices.html" target="_blank">Developing and Deploying with Branches</a> guide first to get a general idea of how branches should be setup in your repository to be able to fully utilize tips from this guide. It’s a great read.</p>

<h3 id="note-on-development-branch">Note on Development Branch</h3>
<p>In this guide you will see a lot of references to a branch called <i>development</i>. In your repository you can use <i>master</i> (Git), <i>trunk</i> (Subversion) or <i>default</i> (Mercurial) for the same purpose, there’s no need to create a branch specifically called “development”. I chose this name because it’s universal for all version control systems.</p>

<h3 id="web-development-disclaimer">Web Development Disclaimer</h3>
<p>Our team makes web applications exclusively (<a href="http://beanstalkapp.com/" target="_blank">Beanstalk</a> and <a href="https://postmarkapp.com/" target="_blank">Postmark</a>), so we don’t have much experience when it comes to deploying something that’s not based in the internet. That’s why this guide will probably be more useful for a team like us. I’m sure you can apply some of the tips in other areas too, but if your deployment process drastically differs from the way web applications are usually deployed, be prepared for some clash of concepts in this guide.</p>

<h2 id="the-workflow">The Workflow</h2>
<p>Deployments should be treated as part of a development workflow, not as an afterthought. If you are developing a web site or an application, your workflow will usually include at least three environments: Development, Staging and Production. In that case the workflow might look like this:</p>
<ul>
	<li>Developers work on bugs and features in separate branches. Really minor updates can be committed directly to the stable development branch.</li>
	<li>Once features are implemented, they are merged into the staging branch and deployed to the Staging environment for quality assurance and testing.</li>
	<li>After testing is complete, feature branches are merged into the development branch.</li>
	<li>On the release date, the development branch is merged into production and then deployed to the Production environment.</li>
</ul>
<p>Let’s take a closer look at each environment to see what are the most efficient way to deploy each one of them.</p>

<h2 id="development-environment">Development Environment</h2>
<p>If you make web applications, you don’t need a remote development environment, every developer should have their own local setup.</p>
<p>We noticed in Beanstalk that some teams have Development environments set up with automatic deployments on every commit or push. While this gives developers a small advantage of not installing the site or the application on their computers to perform testing locally, it also wastes <em>a lot</em> of time. Every tiny change must be committed, pushed, deployed, and only then it can be verified. If the change was made by mistake, a developer will have to revert it, push it, then redeploy.</p>
<p>Testing on a local computer removes the need to commit, push and deploy completely. Every change can be verified locally first, then, once it’s more or less stable, it can be pushed to a Staging environment for proper quality assurance testing.</p>
<p><strong>We do not recommend using deployments for rapidly changing development environments. Running your software locally is the best choice for that sort of testing.</strong></p>

<h2 id="staging-environment">Staging Environment</h2>
<p>Once the features are implemented and considered fairly stable, they get merged into the staging branch and then automatically deployed to the Staging environment. This is when quality assurance kicks in: testers go to staging servers and verify that the code works as intended.</p>
<p>It is very handy to have a separate branch called <i>staging</i> to represent your staging environment. It will allow developers to deploy multiple branches to the same server simultaneously, simply by merging everything that needs to be deployed to the staging branch. It will also help testers understand what exactly is on staging servers at the moment, just by looking inside the staging branch.</p>
<p><strong>We recommend to deploy to the staging environment automatically on every commit or push.</strong></p>

<h2 id="production-environment">Production Environment</h2>
<p>Once the feature is implemented and tested, it can be deployed to production. If the feature was implemented in a separate branch, it should be merged into a stable development branch first. The branches should be deleted after they are merged to avoid confusion between team members.</p>
<p>The next step is to make a diff between the production and development branches to take a quick look at the code that will be deployed to production. This gives you one last chance to spot something that’s not ready or not intended for production. Stuff like debugger breakpoints, verbose logging or incomplete features.</p>
<p>Once the diff review is finished, you can merge the development branch into production and then initialize a deployment of the production branch to your Production environment by hand. Specify a meaningful message for your deployment so that your team knows exactly what you deployed.</p>
<p>Make sure to only merge development branch into production when you actually plan to deploy. Don’t merge anything into production in advance. Merging on time will make files in your production branch match files on your actual production servers and will help everyone better understand the state of your production environment.</p>
<p><strong>We recommend always deploying major releases to production at a scheduled time, of which the whole team is aware of.</strong> Find the time when your application is least active and use that time to roll out updates. This may sound obvious, but make sure that it’s not too late, because someone needs to be around after the deployment for at least a few hours to monitor the application and make sure the deployment went fine. Urgent production fixes can be deployed at any time.</p>
<p>After deployment finishes make sure to verify it. It is best to check all the features or fixes that you deployed to make sure they work properly in production. It is a big win if your deployment tool can send an email to all team members with a summary of changes after every deployment. This helps team members to understand what exactly went live and how to communicate it to customers. Beanstalk does this for you automatically.</p>
<p>Your deployment to production is now complete, pop champagne and celebrate with your team!</p>

<h3 id="rolling-back">Rolling Back</h3>
<p>Sometimes deployments don’t go as planned and things break. In that case you have the possibility to rollback. However, you should be as careful with rollbacks as with production deployments themselves. Sometimes a rollback bring more havoc than the issue it was trying to fix. So first of all stay calm and don’t make any sudden moves. Before performing a rollback, answer the following questions:</p>

<h4>Did it break because of the code that I deployed, or did something else break?</h4>
<p>You can only rollback files that you deployed, so if the source of the issues is something else a rollback won’t be much help.</p>

<h4>Is it possible to rollback this release?</h4>
<p>Not all releases can be rolled back. Sometimes a release introduces a new database structure that is incompatible with the previous release. In that case if you rollback, your application will break.</p>

<p>If the answer to both questions is “yes”, you can rollback safely. After rollback is done, make sure to fix the bug that you discovered and commit it to either the development branch (if it was minor) or a separate bug-fix branch. Then proceed with the regular bug-fix branch → staging; bug-fix → development → production integration workflow.</p>

<h3 id="deploying-urgent-fixes">Deploying Urgent Fixes</h3>
<p>Sometimes you need to deploy a bug-fix to production quickly, when your development branch is not ready for release yet. The workflow in that case stays the same as described above, but instead of merging the development branch into production you actually merge your bug-fix branch first into the development branch, then separately into production, without merging development into production. Then deploy the production branch as usual. This will ensure that only your bug-fix will be deployed to the Production environment without all the other stuff from the development branch that’s not ready yet.</p>
<p>It is important to merge the bug-fix branch to both the development and production branches in this case, because your production branch should never include anything that doesn’t exist in your stable development branch. The development branch is where developers work all day, so if your fix is only in the production branch they will never see it and it can cause confusion.</p>

<h3 id="automatic-deployments-to-production">Automatic Deployments to Production?</h3>
<p>I can’t stress enough how important it is for all production deployments to be performed and verified by a responsible human being. Using automatic deployments for Production environment is dangerous and can lead to unexpected results. If every commit is deployed to your production site automatically, imagine what happens when someone commits something by mistake or commits an incomplete feature in the middle of the night when the rest of the team is sleeping? <strong>Using automatic deployments makes your Production environment very vulnerable. Please don’t do that, always deploy to production manually.</strong></p>

<h2 id="permissions">Permissions</h2>
<p>Every developer should be able to deploy to the Staging environment. They just need to make sure they don’t overwrite each other’s changes when they do. That's exactly why the staging branch is a great help: all changes from all developers are getting merged into it so it contains all of them.</p>
<p>Your Production environment, ideally, should only be accessible to a limited number of experienced developers. These guys should always be prepared to fix the servers immediately after a deployment went rogue.</p>

<h2 id="conclusion">Conclusion</h2>
<p>We’ve been using this workflow in our team internally for many years to deploy Beanstalk and Postmark. Some of these things were learned the hard way, through broken production servers. These days our production deployments are incredibly smooth and don’t cause any stress at all. (And we deploy to several dozens of servers simultaneously!) We really hope this guide will help you streamline your deployments too.</p>

				
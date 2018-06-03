<a href="https://news.ycombinator.com/item?id=17217210">https://news.ycombinator.com/item?id=17217210</a><div id="articleHeader"><h1>Ask HN: What's your favorite way of getting a web app up quickly in 2018?</h1></div><table id="hnmain">
        <tbody>
<tr><td><table>
        <tbody><tr id="17217210">
      <td></td>      <td></td><td><a href="item?id=17217210" target="_blank">Ask HN: What's your favorite way of getting a web app up quickly in 2018?</a></td></tr><tr><td colspan="2"></td><td>
        54 points by <a href="user?id=westoncb" target="_blank">westoncb</a> <a href="item?id=17217210" target="_blank">2 hours ago</a>  | <a href="hide?id=17217210&goto=item%3Fid%3D17217210&auth=60e8237d38d89c636787d9b5723f214c59600845" target="_blank">hide</a> | <a href="https://hn.algolia.com/?query=Ask%20HN%3A%20What's%20your%20favorite%20way%20of%20getting%20a%20web%20app%20up%20quickly%20in%202018%3F&sort=byDate&dateRange=all&type=story&storyText=false&prefix&page=0" target="_blank">past</a> | <a href="https://www.google.com/search?q=Ask%20HN%3A%20What's%20your%20favorite%20way%20of%20getting%20a%20web%20app%20up%20quickly%20in%202018%3F" target="_blank">web</a> | <a href="fave?id=17217210&auth=60e8237d38d89c636787d9b5723f214c59600845" target="_blank">favorite</a> | <a href="item?id=17217210" target="_blank">41 comments</a>              </td></tr>
      <tr><td colspan="2"></td><td>I am still frustrated with the amount of incidental complexity required whenever I want to do this. My latest attempt was to use a Digital Ocean droplet with Django pre-installed. I guess the biggest issue there was setting up something so that I could easily deploy my local version to the droplet (ended up using git/Github), and ensuring those two environments were in sync. I looked into Docker in some detail about a year ago, and I think it's the only pretty good solution for this I've come across—but there's a steep up front cost in learning/setup etc. (or so it seems).<p>What services and technologies do you use when you'd like to quickly build a web app which may never be more than a prototype, but may also turn into something real? A big aspect of what I'm wondering is about automatically setting something up for keeping local/production environments in sync, quickly deploying to production, and not having to mess with a bunch of server configuration things, user accounts, security, etc.</p></td></tr>
        
  </tbody></table><table>
            <tbody><tr id="17217720"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Quickly? Firebase + React.<p>Seriously, don’t overlook this combo. Auth just works. Hosting built in, no backend or database server to maintain. No API, just subscribe to a collection right from the view. It just works (and is easily swapped for the real deal if you need it).</p><p>I made a guide/boilerplate to show you how (includes auth, CRUD, full text search, stripe subscriptions):</p><p><a href="http://getfirefly.org/" target="_blank">http://getfirefly.org/</a>
              </p><div>        <p>
                      <u><a href="reply?id=17217720&goto=item%3Fid%3D17217210%2317217720" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217662"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I write the server-side in Go, cross-compile to a Linux binary, and set that up as a service on a vanilla Ubuntu box (usually Digital Ocean). Deploying a new version is a matter of sftp'ing the new binary (and any templates, images, etc) over the top of the old one and restarting the service.<p>If I need a database then I use Postgres, and the setup for that can be a pain, so I get it documented/scripted using Ansible.</p><p>If I need something more complex than plain HTML on the client side then I use a Makefile to synchronise Webpack + Babel + React (and the hot reload during development), and the compiled bundle.js becomes another file to copy over.</p><p>I realise it's not very 2018, but to be honest I've kinda lost the will to live over learning anything more meta at this point.
              </p><div>        <p>
                      <u><a href="reply?id=17217662&goto=item%3Fid%3D17217210%2317217662" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17217686"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  This is about as 2018 as it gets. Go and Rust are the only modern languages where you don't have to second-guess the stdlib for bad choices (looking at you php/ruby/javascript/etc..) yet provide amazing performance.<p>Backend: Go (optional embed db: ledisdb / boltdb / leveldb / rocksdb / etc...)</p><p>Frontend: create-react-app / create-react-native-app
              </p><div>        <p>
                      <u><a href="reply?id=17217686&goto=item%3Fid%3D17217210%2317217686" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
    <tr id="17217723"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  I second this; Go + React.js <i>(Vue.js in my case)</i><p>I talked about it just a couple of hours ago [1].</p><p>[1] <a href="https://news.ycombinator.com/item?id=17215658" target="_blank">https://news.ycombinator.com/item?id=17215658</a>
              </p><div>        <p>
                      <u><a href="reply?id=17217723&goto=item%3Fid%3D17217210%2317217723" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17217756"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  That's interesting... I think I'll spend a couple of days playing with Vue to see if I can get rid of Webpack and Babel, because they're an enormous pain to set up (especially as they keep changing their config schema every major version release - I think I've climbed Webpack's config learning cliff three times now).
              <div>        <p>
                      <u><a href="reply?id=17217756&goto=item%3Fid%3D17217210%2317217756" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                  <tr id="17217757"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Rails + heroku is pretty much instant. If you want to pay a little little less a single vps instance can run the web app and the postgres server at the same time.
              <div>        <p>
                      <u><a href="reply?id=17217757&goto=item%3Fid%3D17217210%2317217757" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217761"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I'm using Meteor with React and Semantic-UI-React. Not everything has to be realtime with Meteor; use Meteor.methods() instead. For most projects, I can definitely recommend using this stack.
              <div>        <p>
                      <u><a href="reply?id=17217761&goto=item%3Fid%3D17217210%2317217761" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217749"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I use Django and jQuery on top of a pythonanywhere. A bunch of people say that you need PostgresSQL and MySQL setup. Or that you need gunicorn behind a nginx setup . I just don't do those things and run Django with Debugging off on pythonanywhere.com or on a VPS like Amazon Lightsail.<p>If you only need a static site though I have used Cactus but Jekyll could work.
              </p><div>        <p>
                      <u><a href="reply?id=17217749&goto=item%3Fid%3D17217210%2317217749" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              
              <tr id="17217737"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  The last couple prototypes I put up for work were using Flask and Vue on Heroku. I've been really happy with both how quickly they went up, but also how understandable everything is even a year later (they are only used internally).<p>The piece I wouldn't mind cutting out is heroku. If you do end up going the docker route, docker-machine is nice for being able to quickly put things up, "push" updates to digital ocean:</p><p><a href="https://docs.docker.com/machine/examples/ocean/" target="_blank">https://docs.docker.com/machine/examples/ocean/</a>
              </p><div>        <p>
                      <u><a href="reply?id=17217737&goto=item%3Fid%3D17217210%2317217737" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              
              <tr id="17217765"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Rails (server side rendering) + Heroku.
              <div>        <p>
                      <u><a href="reply?id=17217765&goto=item%3Fid%3D17217210%2317217765" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217763"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Heroku, I don’t think it can be any easier.
              <div>        <p>
                      <u><a href="reply?id=17217763&goto=item%3Fid%3D17217210%2317217763" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217739"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I use Elixir/Phoenix mainly because I think it is fun and think that side projects should be fun. If it has the potential to become something more, I believe that it is a great production language for a company and would stake my business on it. Usually deploy to Heroku free tier for my up and fast prototypes.<p>Frontend will either be React or plain ol' JS depending on how complex the idea is.
              </p><div>        <p>
                      <u><a href="reply?id=17217739&goto=item%3Fid%3D17217210%2317217739" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217702"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  I use Swagger/OpenAPI to define the REST API, which is fast and makes the API including the main data types easily visible.<p>To implement the server side I typically generate Java JAX-RS skeleton code that can run in Jetty using Swagger codegen.  You fill out implementation code and the app is off and running.</p><p>On the client side I generate Angular client stubs using Swagger codegen, then fill build services and UI components on top. For CLIs or other tools you can take a similar approach or just write the REST calls directly.</p><p>Code generation from an OpenAPI spec makes this process a lot quicker as it takes care of most of the boilerplate code necessary to process REST requests. It's especially helpful for making quick changes and also helps you to get to a stable, easily understandable API which is necessary if you decide to turn the service(s) into a real product.</p><p>Docker is incidentally a godsend for systems with multiple services, especially if you work in polyglot environments.
              </p><div>        <p>
                      <u><a href="reply?id=17217702&goto=item%3Fid%3D17217210%2317217702" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              
              <tr id="17217699"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Rails + whatever framework works for the desired frontend
              <div>        <p>
                      <u><a href="reply?id=17217699&goto=item%3Fid%3D17217210%2317217699" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217693"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Heroku is still a great choice if you're willing to pay to never think about infrastructure.<p>On the other hand if you're willing to ask for help there are plenty of freelance IT admins who would set up a digital ocean box with the DIY equivalent of Heroku.
              </p><div>        <p>
                      <u><a href="reply?id=17217693&goto=item%3Fid%3D17217210%2317217693" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17217745"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Not trying to be snarky but... how is it cheaper to hire a freelance IT person to set up something for you, and help you when it breaks/changes, than $7/mo for Heroku?
              <div>        <p>
                      <u><a href="reply?id=17217745&goto=item%3Fid%3D17217210%2317217745" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17217753"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  The issue with Heroku is it <i>rapidly</i> gets more than $7/month if you hit <i>any</i> sort of scale.
              <div>        <p>
                      <u><a href="reply?id=17217753&goto=item%3Fid%3D17217210%2317217753" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
                  <tr id="17217567"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Imo Docker doesn't have too high a learning curve at the start. It's just when you move up to docker compose, Kubernetes that it can be overwhelming.<p>My opinion is that when you're starting out, just go with a PaaS like Heroku. You can simply maintain a separate dev/prod branch and it'll automatically update the server.</p><p>All the issues you mentioned can be solved it just takes some investment somewhere (time if you do it today yourself / money to pay a PaaS or someone else to do it).</p><p>We personally use Kubernetes to solve these issues since we get stateless builds and simply have environment variables that change things like database connections, api keys, etc between our various environments. But again this took a few weeks to setup.
              </p><div>        <p>
                      <u><a href="reply?id=17217567&goto=item%3Fid%3D17217210%2317217567" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217685"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  1) Spring Boot on Google App Engine free tier<p>2) Managed Postgres on GCP/AWS</p><p>3) Frontend framework of the day, like React or Vue.</p><p>4) Take 1-2 hours in the beginning to set up ci/cd (like Circle) to make things 10x more convenient.
              </p><div>        <p>
                      <u><a href="reply?id=17217685&goto=item%3Fid%3D17217210%2317217685" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              
              
              
              
              <tr id="17217708"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  The most recent one I created was with Laravel hosted on Fortrabbit. If you want it to be even easier, try Laravel Spark. It is really easy to launch something simple.
              <div>        <p>
                      <u><a href="reply?id=17217708&goto=item%3Fid%3D17217210%2317217708" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              
              <tr id="17217706"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  ember new my-app<p>Yes Ember is still great. Ember data has gotten bloated though so I say pull that shit out IMO unless you are really used to it.</p><p>Ember v3.0 is all modular now, so you can just strip out modules until you get down to Glimmer. Versus React or Vue where you start with basically nothing and build upwards.</p><p>Exact opposite philosophy, but way faster for building 90% of CRUD apps.
              </p><div>        <p>
                      <u><a href="reply?id=17217706&goto=item%3Fid%3D17217210%2317217706" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217682"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  It may be too simplistic for most people’s needs but I’m a big fan of <a href="http://surge.sh/" target="_blank">http://surge.sh/</a> for publishing simple, static sites.
              <div>        <p>
                      <u><a href="reply?id=17217682&goto=item%3Fid%3D17217210%2317217682" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              
              <tr id="17217630"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  1) ASP MVC .NET Core 2 project
2) Get a linux vm
3) Write a WSL Script to push to linux vm (lftp + sshpass)
              <div>        <p>
                      <u><a href="reply?id=17217630&goto=item%3Fid%3D17217210%2317217630" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217687"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  create-react-app + netlify on the frontend. For the backend services, kubernetes on gcp with Ambassador from Datawire. It’s an extremely solid and easy to use gateway based on the Envoy load balancer. I have a few templates I’ve created that has reduced creating a new app/service down to a few keystrokes.
              <div>        <p>
                      <u><a href="reply?id=17217687&goto=item%3Fid%3D17217210%2317217687" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217701"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Flask hosted on pythonanywhere. Recommend highly.
              <div>        <p>
                      <u><a href="reply?id=17217701&goto=item%3Fid%3D17217210%2317217701" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217628"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Heroku and node with any frontend framework of the moment
              <div>        <p>
                      <u><a href="reply?id=17217628&goto=item%3Fid%3D17217210%2317217628" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217639"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  1. flask-base for back-end<p>2. create-react-app for front-end</p><p>3. digital ocean for hosting</p><p>I just cp files from local to server and use a couple different bash scripts for dev vs prod.
              </p><div>        <p>
                      <u><a href="reply?id=17217639&goto=item%3Fid%3D17217210%2317217639" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              <tr id="17217675"><td>
            <table>  <tbody><tr>    <td></td><td></td><td><div>
                  Zeit Now, without a doubt.<p>1. npm install -g now</p><p>2. run 'now' command in the folder containing your app files</p><p>The files are uploaded, your app is deployed and your clipboard contains the URL. So simple it's like cheating.</p><p><a href="https://zeit.co/now" target="_blank">https://zeit.co/now</a>
              </p><div>        <p>
                      <u><a href="reply?id=17217675&goto=item%3Fid%3D17217210%2317217675" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
              
        <tr id="17217418"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  That's purely front-end tech if I'm not mistaken. My question here is primarily about the back-end aspects of a project (especially syncing local and production environments, etc.).
              <div>        <p>
                      <u><a href="reply?id=17217418&goto=item%3Fid%3D17217210%2317217418" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
        <tr id="17217645"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="80" height="1" /></td><td></td><td><div>
                  Django. Use Cookie cutter and call it a day.
              <div>        <p>
                      <u><a href="reply?id=17217645&goto=item%3Fid%3D17217210%2317217645" target="_blank">reply</a></u>
                  
      </p></div></div></td></tr>
      </tbody></table></td></tr>
      <tr id="17217327"><td>
            <table>  <tbody><tr>    <td><img src="s.gif" width="40" height="1" /></td><td></td><td><div>
                  Same. As for deployment depends somewhat on the back-end but I tend to use elastic bean stalk if I’m aws.
              <div>        <p>
                      <u><a href="reply?id=17217327&goto=item%3Fid%3D17217210%2317217327" target="_blank">reply</a></u>
                  
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
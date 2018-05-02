<a href="https://daveceddia.com/react-practice-projects/">https://daveceddia.com/react-practice-projects/</a><div id="articleHeader"><h1>5 Projects to Help You Learn React</h1></div>
      <footer>
        
        
        
        <time> August 29, 2017</time>
        
        
        
        
      </footer>
      <a href="https://twitter.com/intent/follow?screen_name=dceddia" id="twitter-follow" target="_blank">
	 Follow @dceddia</a>


      <div>
        <div class="readableLargeImageContainer"><img src="https://daveceddia.com/images/react-practice-projects@2x.png"   alt="5 Projects to Help You Learn React" /></div>
        <p>If you’re in the middle of trying to learn React, you have probably run into the “the gap.”</p>

<p>You have a handle on the basics: components, props, state. You’ve done a tutorial or two, and probably built a few To Do apps. Though your skills aren’t <em>quite</em> at the level of building a real app yet, you know enough that building more To Do apps won’t take you any further.</p>

<p>In this post I’ll show you 5 projects that will be fun to build, stretch your abilities a bit, and do not involve any todos.</p>

<h2 id="tooling">Tooling</h2>

<p>I suggest using <a href="https://github.com/facebookincubator/create-react-app" target="_blank">Create React App</a> to bootstrap these projects.</p>

<h2 id="social-card">Social Card</h2>

<p>We’ll start off with an easy one. This is more of a component than a full-blown app, but it’s a good place to start.</p>

<p><div class="readableLargeImageContainer"><img src="https://daveceddia.com/images/social-card@2x.png"   alt="social card" /></div></p>

<p>Variations of this UI can be found all over the web – <a href="https://twitter.com" target="_blank">Twitter</a>, Facebook, Pinterest, <a href="https://www.airbnb.com/" target="_blank">Airbnb</a>, <a href="https://www.redfin.com/" target="_blank">Redfin</a>, and so on – and it serves as a solid building block for the sort of app where you want to display an image + some data.</p>

<p>It’s also good practice for breaking down a UI into React components.</p>

<p>Once you have a single <code>SocialCard</code> component rendering, try making a list of them with some fake data.</p>

<h2 id="weather-app">Weather App</h2>

<p>Display a 5-day weather forecast, where each day shows the high and low temperatures, and an image for sunny/rainy/cloudy/snowy. Use fake, hard-coded data until you’ve got everything rendering correctly.</p>

<p><div class="readableLargeImageContainer"><img src="https://daveceddia.com/images/weather@2x.png"   alt="Weather App" /></div></p>

<p>You might notice that the “days” look a lot like social cards…</p>

<p>For added practice, here are a few ways you could expand on the app:</p>

<ul>
  <li>Add the ability to click on a day, and see its hourly forecast. You can just maintain the current view in the top-level App state.</li>
  <li>Add React Router to the project (<code>npm install react-router</code>) and follow the quick start guide <a href="https://reacttraining.com/react-router/web/guides/quick-start" target="_blank">here</a> to add routes, such that <code>/</code> shows the 5-day forecast, and <code>/[name-of-day]</code> shows the hourly forecast for a particular day.</li>
  <li>Sign up for a free API key from <a href="https://openweathermap.org" target="_blank">Open Weather Map</a>, fetch a real 5-day forecast, and feed that data into your app.</li>
  <li>Want to get really fancy? Add a graphics library like <a href="https://vx-demo.now.sh/" target="_blank">vx</a> and follow the examples <a href="https://medium.com/vx-code/getting-started-with-vx-1756bb661410" target="_blank">here</a> to add a graph of the temperature over the course of a week or day.</li>
</ul>

<p>You can see how this app starts off simple, but can be expanded at will to increase the challenge and the learning.</p>

<h2 id="hacker-hunt">Hacker Hunt</h2>

<p>Hacker Hunt is an aggregator of Hacker News stories with categories, but more importantly, it’s a good app to build for React practice.</p>

<p><a href="https://hackerhunt.co" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://daveceddia.com/images/hackerhunt@2x.png"   alt="Hacker Hunt screenshot" /></div></a></p>

<p>It has been said that all web apps are basically just lists. This app will give you some practice with lists of components that are a little more complicated than todos.</p>

<p>Use static data at first, and if you want a little more of a challenge, fetch stories from their API. From what I can glean from devtools, this is just a single route, <a href="https://hackerhunt.co/api/daily/0" target="_blank">https://hackerhunt.co/api/daily/0</a>, and you can replace the 0 with a different page number.</p>

<p>You could go a step further and replicate their routing structure with React Router.</p>

<h2 id="calculator">Calculator</h2>

<p><div class="readableLargeImageContainer"><img src="https://daveceddia.com/images/calculator@2x.png"   alt="Calculator mockup" /></div></p>

<p>You probably already know how these work. Add, subtract, multiply, divide… Clicking the numbers or the operations should perform the action.</p>

<p>For added challenge, respond to keyboard input too. You shouldn’t need to add an <code>&lt;input&gt;</code> element to make this work. If you do use an <code>&lt;input&gt;</code>, make it so that the user doesn’t need to focus the input control to type into it.</p>

<p>Spend a little time thinking about how the state will be represented. Do you need to store more than just the numbers on the display? When you type a new number, does it replace the display with that number, or append it to the end?</p>

<p>Add some <a href="/snapshot-testing-react-with-jest/" target="_blank">snapshot tests with Jest</a> to test that the calculator works correctly.</p>

<h2 id="github-issues-page">Github Issues Page</h2>

<p>Make a simplified version of Github’s Issues page. <a href="https://github.com/facebookincubator/create-react-app/issues" target="_blank">Here’s an example</a>. To keep the scope small, just focus on implementing the list of issues, and ignore the stuff in the header (search, filtering, stars, etc).</p>

<p><div class="readableLargeImageContainer"><img src="https://daveceddia.com/images/github-issue-list@2x.png"   alt="Github issue list" /></div></p>

<p>Start by fetching open issues from <a href="https://developer.github.com/v3/issues/" target="_blank">Github’s API</a> and displaying them in a list. You could use static data for this too.</p>

<p>Then add a pagination control to allow navigating through the entire list of issues. You might find it useful to add React Router too, so that you can navigate directly to a given page.</p>

<p>For added difficulty, implement the issue detail page too. Render the issue’s Markdown text and its comments using something like <a href="https://github.com/rexxars/react-markdown" target="_blank">react-markdown</a>.</p>

<p><div class="readableLargeImageContainer"><img src="https://daveceddia.com/images/github-issue-detail@2x.png"   alt="Github issue detail" /></div></p>

<p><a href="https://github.com/dceddia/github-issues-viewer" target="_blank">Here is a working example</a> using React, Redux, and React Router that implements the features above plus a few more.</p>

<h2 id="what-next">What Next?</h2>

<p>Hopefully I’ve given you some ideas for the kinds of things to build to help advance your React skills. For more along these lines, read about <a href="/learn-react-with-copywork/" target="_blank">Learning with Copywork</a> and follow along to build a <a href="/build-metronome-react/" target="_blank">metronome in React</a>.</p>

        
          <div>
  <p>
    Learning React can be a struggle -- so many libraries and tools!<br />
    My advice? Ignore all of them :)<br />
    For a step-by-step approach, read my book <a href="https://daveceddia.com/pure-react/?utm_campaign=after-post" target="_blank">Pure React</a>.
  </p>
  <div>
    <div>
      Loved it! Very well written and put together. Love that you focused only on React. Wish I had stumbled onto your book first before I messed around with all those scary "boilerplate" projects.
    </div>
    <div>
      <div>— John Lyon-Smith</div>
    
  


        
        
    <div><div>
  
<div>
  <div>
    <h3>Get 5 more practice projects</h3>
    <div>
      
        
      
      <p><img src="https://convertkit.s3.amazonaws.com/assets/pictures/13404/830322/content_Screen_Shot_2017-10-17_at_12.12.31_AM.png" width="159" height="213" /></p><p>Sign up and get more 5 project ideas and weekly articles about React and JavaScript.</p>
    </div>
  

  








	

        
          
          




        
      
    
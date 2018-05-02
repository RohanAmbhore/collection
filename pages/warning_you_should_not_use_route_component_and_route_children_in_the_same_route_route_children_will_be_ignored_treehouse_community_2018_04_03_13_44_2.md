<a href="https://teamtreehouse.com/community/warning-you-should-not-use-route-component-and-route-children-in-the-same-route-route-children-will-be-ignored">https://teamtreehouse.com/community/warning-you-should-not-use-route-component-and-route-children-in-the-same-route-route-children-will-be-ignored</a><div id="articleHeader"><h1>Warning: You should not use &lt;Route component&gt; and &lt;Route children&gt; in the same route; &lt;Route children&gt; will be ignored</h1></div>

  <div>
    <p>In the console I get the message "Warning: You should not use &lt;Route component&gt; and &lt;Route children&gt; in the same route; &lt;Route children&gt; will be ignored".</p>

<p>What would be the best way to nest the routes since it creates this conflict in React Router v4?</p>
  </div>




		<div id="comment-1967742">
  <div id="show-comment-1967742">
    
  <div><a href="/dennylouis" target="_blank">Denny Louis  <div>
    <h6>Denny Louis</h6>



      
        9,340 Points
      
</div></a> <time>on Mar 19, 2017</time>

  <div>
    <div>
      <p>Hey Jonathan,</p>

<p>Thanks for that, that worked for this part of the routing. Can I ask what you did for the routing on the Courses page that is part of the challenge later on in the course?</p>

<p>Also, it won't let me mark your answer as correct because I think you did it as a comment rather than as an answer.</p>

<p>Thanks!</p>
    </div>
  





	




      <div id="forum-post-answers-container">

          <div>
            <h2>6 Answers</h2>
          </div>

        <div id="featurette-5">

  <div id="answer-3060002">

    <div id="show-answer-3060002">

    
  <div><a href="/jonathandewitt" target="_blank">Jonathan Dewitt  <div>
    <h6>Jonathan Dewitt</h6>



      
        8,099 Points
      
</div></a> <time>on Mar 19, 2017</time>

  <div>
    <div>
      <p>Adding my original answer to this one --</p>

<p>I got around this first issue by changing my render function accordingly:</p>

<div><pre>// Render
render((
    &lt;Router&gt;
        &lt;App&gt;
            &lt;Route exact={true} path="/" component={Home} /&gt;
            &lt;Route path="/about" component={About} /&gt;
            &lt;Route path="/courses" component={Courses} /&gt;
            &lt;Route path="/teachers" component={Teachers} /&gt;
        &lt;/App&gt;
    &lt;/Router&gt;
), document.getElementById('root'));
</pre></div>

<p>I had some trouble with that next lesson as well (I just did it today) -- it seems like React has changed the ability to nest routes as taught in the videos. To include the sub-route, I researched and used a &lt;Switch&gt; tag within Courses.js file.</p>

<p>Also, it seems NavLink is now part of react-router-dom, so you can just include the module instead of making your own. </p>

<p>Here's what I came up with:</p>

<p><strong>Courses.js - underneath the closing &lt;/ul&gt;&lt;/div&gt;</strong></p>

<div><pre>        &lt;Redirect from="/courses/" to="/courses/html" /&gt;
        &lt;Switch&gt;
            &lt;Route path="/courses/html" component={HTML} /&gt;
            &lt;Route path="/courses/css" component={CSS} /&gt;
            &lt;Route path="/courses/javascript" component={JavaScript} /&gt;
        &lt;/Switch&gt;
</pre></div>

<p>Be sure to import the three components into your file, and also be sure to include the needed modules in the react-router-dom import (NavLink, Redirect, Switch)</p>
    
  


  


<div>
  <div>
    <div id="comment-1967762">
  <div id="show-comment-1967762">
    
  <div><a href="/dennylouis" target="_blank">Denny Louis  <div>
    <h6>Denny Louis</h6>



      
        9,340 Points
      
</div></a> <time>on Mar 19, 2017</time>

  <div>
    <div>
      <p>Thank you! Got it working.
They really need to update the videos for this.</p>

<p>Thanks again</p>
    </div>
  




<div id="comment-2024942">
  <div id="show-comment-2024942">
    
  <div><a href="/sarahellis2" target="_blank">Sarah Ellis  <div>
    <h6>Sarah Ellis</h6>



      
        959 Points
      
</div></a> <time>on May 3, 2017</time>

  <div>
    <div>
      <p>I found an easier way. You don't need to use the Redirect in the <strong><em>Courses.js</em></strong>. In the <strong><em>Router.js</em></strong> you can set the Switch like so:</p>

<div><pre>// Libs
import React from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

// Components
import App from './components/App';
import Home from './components/Home';
import About from './components/About';
import Teachers from './components/Teachers';
import Courses from './components/Courses';

// Components -- Courses
import HTML from './components/courses/HTML';
import CSS from './components/courses/CSS';
import JavaScript from './components/courses/JavaScript';

// Routes
// contain all routes into a variable to be imported into index.js
const routes = (
    &lt;Router&gt;
        {/* If path is / then load the Home component */}
        &lt;App&gt;
            &lt;Switch&gt;
                &lt;Route exact path="/" component={Home} /&gt;
                &lt;Route path="/about" component={About} /&gt;
                &lt;Route path="/teachers" component={Teachers} /&gt;
                &lt;Courses&gt;
                    &lt;Route path="/courses/html" component={HTML} /&gt;
                    &lt;Route path="/courses/css" component={CSS} /&gt;
                    &lt;Route path="/courses/javascript" component={JavaScript} /&gt;
                &lt;/Courses&gt;
            &lt;/Switch&gt;
        &lt;/App&gt;
    &lt;/Router&gt;
);

export default routes;
</pre></div>

<p>This is all using V4</p>
    
  





  

<div id="featurette-12">

  <div id="answer-3111472">

    <div id="show-answer-3111472">

    
  <div><a href="/guil" target="_blank">Guil Hernandez  <div>
    <h6>Guil Hernandez</h6>


      
        Treehouse Teacher
      

</div></a> <time>on Apr 13, 2017</time>

  <div>
    <div>
      <p>Hi <a href="https://teamtreehouse.com/darrenanderson" target="_blank">Darren Anderson</a>,</p>

<p>Now that React Router v4 has shipped (and stable), I'm currently working on a course refresh. Stay tuned. :)</p>
    </div>
  


  



<div id="featurette-16">

  <div id="answer-3105842">

    <div id="show-answer-3105842">

    <div id="avatar-928ebd">
    
    
    <div>
      <img src="https://secure.gravatar.com/avatar/c308339d665e5a8b505186c984168086?s=96&d=https%3A%2F%2Fstatic.teamtreehouse.com%2Fassets%2Fcontent%2Fdefault_avatar-ea7cf6abde4eec089a4e03cc925d0e893e428b2b6971b12405a9b118c837eaa2.png&r=pg" alt="Darren Anderson" />
    </div>
    
    
      <div>
    <h6>Darren Anderson</h6>



      
        274 Points
      
</div>

  <div>Darren Anderson  <div>
    <h6>Darren Anderson</h6>



      
        274 Points
      
</div> <time>on Apr 11, 2017</time>

  <div>
    <div>
      <p>This really needs to be updated. At this point these videos are incredibly frustrating to follow. Feels like I'm stopping in every video to try to find a solution to code not working.</p>
    </div>
  


  









<div id="featurette-26">

  <div id="answer-3178452">

    <div id="show-answer-3178452">

    <div id="avatar-2bcfc1">
    
    
    <div>
      <img src="https://secure.gravatar.com/avatar/c0976c4ca379be4d34b0ee7aef7c9fec?s=96&d=https%3A%2F%2Fstatic.teamtreehouse.com%2Fassets%2Fcontent%2Fdefault_avatar-ea7cf6abde4eec089a4e03cc925d0e893e428b2b6971b12405a9b118c837eaa2.png&r=pg" alt="Andrew Sams" />
    </div>
    
    
      <div>
    <h6>Andrew Sams</h6>



      
        4,859 Points
      
</div>

  <div>Andrew Sams  <div>
    <h6>Andrew Sams</h6>



      
        4,859 Points
      
</div> <time>on May 17, 2017</time>

  


  




      

      

      
  
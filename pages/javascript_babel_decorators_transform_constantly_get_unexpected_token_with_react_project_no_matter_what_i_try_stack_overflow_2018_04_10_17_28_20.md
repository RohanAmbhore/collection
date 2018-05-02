<a href="https://stackoverflow.com/questions/44746518/babel-decorators-transform-constantly-get-unexpected-token-with-react-project">https://stackoverflow.com/questions/44746518/babel-decorators-transform-constantly-get-unexpected-token-with-react-project</a><div id="articleHeader"><h1>Babel Decorators transform, constantly get unexpected token (with react project) no matter what I try</h1></div>

<p>I've done a fair amount of searching through StackO trying to find an answer but I keep coming up with the same error, <code>unexpected token</code></p>

<p>Whenever I use the text decorator transpile to correct the error, I still get the same problem in my component.</p>

<p>My error is this:</p>

<pre><code>./src/components/pages/projectpages/dnd2/Card.js
Syntax error: Unexpected token (71:0)

  69 | };
  70 | 
&gt; 71 | @DropTarget(ItemTypes.CARD, cardTarget, connect =&gt; ({
     | ^
  72 |   connectDropTarget: connect.dropTarget(),
  73 | }))
  74 | @DragSource(ItemTypes.CARD, cardSource, (connect, monitor) =&gt; ({</code></pre>

<p>and this is how I have it setup in my package.json (and I've tried Stage 1 with no success either)</p>

<pre><code>{
  "name": "my-app",
  "version": "0.1.0",
  "babel": {
    "plugins": [
      "transform-decorators"
    ]
  },
  "stage": 0,
  "private": true,
  "dependencies": {
    "babel-plugin-transform-class-properties": "^6.24.1",
    "babel-plugin-transform-decorators-legacy": "^1.3.4",
    "date-fns": "^1.28.5",
    "dragula": "^3.7.2",
    "flexbox-react": "^4.3.3",
    "moment": "^2.18.1",
    "moment-timezone": "^0.5.13",
    "react": "^15.6.1",
    "react-css-transition-replace": "^2.2.1",
    "react-dnd": "^2.4.0",
    "react-dnd-html5-backend": "^2.4.1",
    "react-dom": "^15.6.1",
    "react-dragula": "^1.1.17",
    "react-fa": "^4.2.0",
    "react-flexbox-grid": "^1.1.3",
    "react-fontawesome": "^1.6.1",
    "react-image-compare": "0.0.1",
    "react-jsonschema-form": "^0.49.0",
    "react-modal": "^1.9.4",
    "react-moment": "^0.2.4",
    "react-router-dom": "^4.1.1",
    "react-toggle-display": "^2.2.0",
    "react-transition-group": "^1.2.0",
    "simple-react-forms": "^1.3.0",
    "styled-components": "^1.4.6",
    "styled-props": "^0.2.0"
  },
  "devDependencies": {
    "babel-plugin-transform-decorators": "^6.24.1",
    "babel-plugin-transform-decorators-legacy": "^1.3.4",
    "react-scripts": "1.0.7"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
}</code></pre>

<p>What else am I missing here?</p>
    
<a href="https://stackoverflow.com/questions/36778260/is-it-ok-to-put-proptypes-and-defaultprops-as-static-props-inside-react-class">https://stackoverflow.com/questions/36778260/is-it-ok-to-put-proptypes-and-defaultprops-as-static-props-inside-react-class</a><div id="articleHeader"><h1>Is it OK to put propTypes and defaultProps as static props inside React class?</h1></div>

            

<div id="question">

        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        23
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>4</b></div>


</div>

            </div>

            
<div>
    <div>

<p>This is the way I've been doing it for quite some time now:</p>

<pre><code>export default class AttachmentCreator extends Component {
  render() {
    return &lt;div&gt;
      &lt;RaisedButton primary label="Add Attachment" /&gt;
    &lt;/div&gt;
  }
}

AttachmentCreator.propTypes = {
  id: PropTypes.string,
};
</code></pre>

<p>But I've seen people doing it this way:</p>

<pre><code>export default class AttachmentCreator extends Component {
  static propTypes = {
    id: PropTypes.string,
  };

  render() {
    return &lt;div&gt;
      &lt;RaisedButton primary label="Add Attachment" /&gt;
    &lt;/div&gt;
  }
}
</code></pre>

<p>And in fact I've seen people setting initial state outside the constructor as well. Is this good practice? It's been bugging me, but I remember a discussion somewhere where someone said that setting default props as a static is not a good idea - I just don't remember why.</p>
    </div>
    
    
</div>

                
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-36780483">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>
<p>non-function properties are not currently supported for es2015 classes. its a proposal for es2016. the second method is considerably more convenient, but a plugin would be required to support the syntax (<a href="http://babeljs.io/docs/plugins/transform-class-properties/" target="_blank">theres a very common babel plugin for it</a>).</p>

<p>On the other end, a hand full of open source projects are beginning to treat proptypes like TypeScript interfaces, or ActionConstants and actually create separate folders/files that house various component prop types and are then imported into the component.</p>

<p>So in summary, both syntaxes are ok to use. but if you want to only use strictly ES2015, the latter syntax is not yet supported in the specification.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-36778923">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        26
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>In fact, it's exactly the same in terms of performance. React.JS is a relatively new technology, so it's not clear yet what are considered good practices or don't. If you want to trust someone, check this AirBNB's styleguide:</p>

<p><a href="https://github.com/airbnb/javascript/tree/master/react#ordering" target="_blank">https://github.com/airbnb/javascript/tree/master/react#ordering</a></p>

<div>
<div>
<pre><code>import React, { PropTypes } from 'react';

const propTypes = {
  id: PropTypes.number.isRequired,
  url: PropTypes.string.isRequired,
  text: PropTypes.string,
};

const defaultProps = {
  text: 'Hello World',
};

class Link extends React.Component {
  static methodsAreOk() {
    return true;
  }

  render() {
    return &lt;a href={this.props.url} data-id={this.props.id}&gt;{this.props.text}&lt;/a&gt;
  }
}

Link.propTypes = propTypes;
Link.defaultProps = defaultProps;

export default Link;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
<p>They are declaring a const with the propTypes object literals, keep the class pretty clean and assign them later to the static properties. I personally like this approach :)</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Apr 21 '16 at 19:36
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-36780088">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>If the component is state-less, meaning it does not change it's own state at all, you should declare it as a stateless component (<code>export default function MyComponent(props)</code>) and declare the <code>propTypes</code> outside.</p>

<p>Whether it's good practice to put initial state declaration in constructor is up to you. In our project we declare initial state in <code>componentWillMount()</code> just because we do not like the <code>super(props)</code> boilerplate you have to use with the constructor.</p>
    </div>
    
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    




<div id="post-editor">

    <div> 
        <div>
            <div id="mdhelp">
    <ul id="mdhelp-tabs">
        <li>Links</li>
        <li>Images</li>
        <li>Styling/Headers</li>
        <li>Lists</li>
        <li>Blockquotes</li>
        
        
        <li><a href="/editing-help" target="_blank">advanced help »</a></li>
    </ul>
    
    

    
    
    

    

    

    

    
</div>
            
        </div>
    </div>

    
    

    

    


    
    
    



</div>

                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/class" title="show questions tagged 'class'" target="_blank">class</a> <a href="/questions/tagged/reactjs" title="show questions tagged 'reactjs'" target="_blank">reactjs</a> <a href="/questions/tagged/ecmascript-next" title="show questions tagged 'ecmascript-next'" target="_blank">ecmascript-next</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
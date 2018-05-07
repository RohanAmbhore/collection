<a href="https://stackoverflow.com/questions/32911630/how-do-i-deal-with-localstorage-in-jest-tests">https://stackoverflow.com/questions/32911630/how-do-i-deal-with-localstorage-in-jest-tests</a><div id="articleHeader"><h1>How do I deal with localStorage in jest tests?</h1></div>

            

<div id="question">

    
    
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        51
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>14</b></div>


</div>

            </div>

            
<div>
    <div>

<p>I keep getting "localStorage is not defined" in Jest tests which makes sense but what are my options? Hitting brick walls.</p>
    </div>
    <div>
        <a href="/questions/tagged/jestjs" title="show questions tagged 'jestjs'" target="_blank">jestjs</a> 
    </div>
    <div>
    

    <div>
        <div>
    <div>
        asked Oct 2 '15 at 16:25
    </div>
    
    
</div>
    </div>
    </div>
</div>

                
            </div>
</div>



        <div id="answers">

                
                




  

<div id="answer-32911774">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        57
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Figured it out with help from this: <a href="https://groups.google.com/forum/#!topic/jestjs/9EPhuNWVYTg" target="_blank">https://groups.google.com/forum/#!topic/jestjs/9EPhuNWVYTg</a></p>

<p>Setup a file with the following contents:</p>

<div>
<div>
<pre><code>var localStorageMock = (function() {
  var store = {};
  return {
    getItem: function(key) {
      return store[key];
    },
    setItem: function(key, value) {
      store[key] = value.toString();
    },
    clear: function() {
      store = {};
    },
    removeItem: function(key) {
      delete store[key];
    }
  };
})();
Object.defineProperty(window, 'localStorage', { value: localStorageMock });</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
<p>Then you add the following line to your package.json under your Jest configs</p>

<p><code>"setupTestFrameworkScriptFile":"PATH_TO_YOUR_FILE",</code></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-41434763">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        69
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Great solution from <a href="https://stackoverflow.com/users/2015685/chiedo" target="_blank">@chiedo</a></p>

<p>However, we use ES2015 syntax and I felt it was a little cleaner to write it this way.</p>

<div>
<div>
<pre><code>class LocalStorageMock {
  constructor() {
    this.store = {};
  }

  clear() {
    this.store = {};
  }

  getItem(key) {
    return this.store[key] || null;
  }

  setItem(key, value) {
    this.store[key] = value.toString();
  }

  removeItem(key) {
    delete this.store[key];
  }
};

global.localStorage = new LocalStorageMock;</code></pre>
<div><div><div><a target="_blank">Expand snippet</a></div></div></div></div>
</div>
</div>
    
</div>
    
        </div>
</div>

  

<div id="answer-43716474">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        9
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>A better alternative which handles <code>undefined</code> values (it doesn't have <code>toString()</code>) and returns <code>null</code> if value doesn't exist. Tested this with <code>react</code> v15, <code>redux</code> and <code>redux-auth-wrapper</code> </p>

<pre><code>class LocalStorageMock {
  constructor() {
    this.store = {}
  }

  clear() {
    this.store = {}
  }

  getItem(key) {
    return this.store[key] || null
  }

  setItem(key, value) {
    this.store[key] = value
  }

  removeItem(key) {
    delete this.store[key]
  }
}

global.localStorage = new LocalStorageMock
</code></pre>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-46931891">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        7
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>or you just take a mock package like this:</p>

<p><a href="https://www.npmjs.com/package/jest-localstorage-mock" target="_blank">https://www.npmjs.com/package/jest-localstorage-mock</a></p>

<p>it handles not only the storage functionality but also allows you test if the store was actually called.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 25 '17 at 12:00
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-47641203">
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
<p>Riffed off some other answers here to solve it for a project with Typescript. I created a LocalStorageMock like this:</p>

<pre><code>export class LocalStorageMock {

    private store = {}

    clear() {
        this.store = {}
    }

    getItem(key: string) {
        return this.store[key] || null
    }

    setItem(key: string, value: string) {
        this.store[key] = value
    }

    removeItem(key: string) {
        delete this.store[key]
    }
}
</code></pre>

<p>Then I created a LocalStorageWrapper class that I use for all access to local storage in the app instead of directly accessing the global local storage variable. Made it easy to set the mock in the wrapper for tests.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-47897345">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        8
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>If using create-react-app, there is a simpler and straightforward solution explained in the <a href="https://github.com/facebookincubator/create-react-app/blob/ed5c48c81b2139b4414810e1efe917e04c96ee8d/packages/react-scripts/template/README.md#initializing-test-environment" target="_blank">documentation</a>.</p>

<p>Create <code>src/setupTests.js</code> and put this in it :</p>

<pre><code>const localStorageMock = {
  getItem: jest.fn(),
  setItem: jest.fn(),
  clear: jest.fn()
};
global.localStorage = localStorageMock;
</code></pre>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 20 '17 at 0:52
    </div>
    
    
</div>
    </div>
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
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/jestjs" title="show questions tagged 'jestjs'" target="_blank">jestjs</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        
<a href="https://scotch.io/tutorials/bookshop-with-react-redux-ii-async-requests-with-thunks">https://scotch.io/tutorials/bookshop-with-react-redux-ii-async-requests-with-thunks</a><div id="articleHeader"><h1>Bookshop With React & Redux II: Async Requests With Thunks</h1></div>
<div>
<div>
<a href="https://github.com/scotch-io/react-redux-bookshop/tree/part-2" target="_blank">


Code
</a>
</div> 





<p><a href="https://scotch.io/tutorials/build-a-bookshop-with-react-redux-i-react-redux-flow" target="_blank">Previously</a>, we got ourselves started with React with Redux fundamentals and touched all the core concepts of Redux including Actions, Reducers and Stores. We also had a look at the features of React-Redux library including <code>connect</code> and <code>Provider</code>.</p>
<p><div class="readableLargeImageContainer"><img src="https://cdn.scotch.io/1/g15cPkIRKWqqgSKpaoGg_BU675PP.jpg" alt="Book Page" /></div></p>
<p>What we can do now is move further to complexity and reality by fleshing out the application we already started building to have more consumable features and tackle real situations.</p>
<h2 id="redux-thunk">
    <a href="#toc-redux-thunk" target="_blank">
      #
      Redux Thunk
    </a> 
  </h2>
<p>Redux Thunk is a middleware for Redux written by Dan, the father of Redux. Normally, your action creators return an object of payload but with Thunk, you can return a <em>defer-able</em> function. This means, you can handle asynchronous requests in a React Redux environment using Redux Thunk.</p>
<p>We can apply the middleware to our store during configuration as discussed in the previous article:</p>
<pre><code>// ./src/store/configureStore.js
import {createStore, compose, applyMiddleware} from 'redux';
// Import thunk middleware
import thunk from 'redux-thunk';
import rootReducer from '../reducers';

export default function configureStore(initialState) {
  return createStore(rootReducer, initialState,
    // Apply to store
    applyMiddleware(thunk)
  );
}</code></pre>
<p>That sets up everything for Redux Thunk. Now, let's make use of it in our existing app.</p>
<h2 id="our-first-thunk">
    <a href="#toc-our-first-thunk" target="_blank">
      #
      Our First Thunk
    </a> 
  </h2>
<p>We already had a React Redux application from our previous post on this tutorial. At the moment, the sample is based on a static array for its data source. We can use <a href="http://mockapi.io" target="_blank">Mock API</a> to create some sample API data and see how we can use thunks to consume this data and make them available in our React application. The following is the endpoint and it is public:</p>
<pre><code>
http://57c62fdcc1fc8711008f2a7e.mockapi.io/api/book
</code></pre>
<p>I populated the API with mock data so we can have something fake to test with.</p>
<h3>Create Async Action</h3>
<p>As we discussed, actions that returns object are not good enough for async operations because the the payload is used as a later time different from when the action was dispatched. Rather, it returns a function that takes dispatch as its only argument and dispatches an action when th: promise resolves:</p>
<pre><code>// ./src/actions/bookActions.js
// API URL
const apiUrl = 'http://57c62fdcc1fc8711008f2a7e.mockapi.io/api/book';
// Sync Action
export const fetchBooksSuccess = (books) =&gt; {
  return {
    type: 'FETCH_BOOKS_SUCCESS',
    books
  }
};
//Async Action
export const fetchBooks = () =&gt; {
  // Returns a dispatcher function
  // that dispatches an action at a later time
  return (dispatch) =&gt; {
    // Returns a promise
    return Axios.get(apiUrl)
      .then(response =&gt; {
        // Dispatch another action
        // to consume data
        dispatch(fetchBooksSuccess(response.data))
      })
      .catch(error =&gt; {
        throw(error);
      });
  };
};</code></pre>
<p>The <strong>dispatcher</strong> function returned by the <strong>action creator</strong> function must return a promise which when resolved, dispatches another synchronous action to handle the data that was returned. </p><div>Related Course: <a href="https://bit.ly/2qktDOA" target="_blank">Getting Started with React</a></div>
<blockquote>
<p>In Redux, a popular convention to keep track of application state is to append the status at the end of the action. Eg: <strong>_SUCCESS<strong> is appended to </strong>FETCH_BOOKS</strong> action to indicate that the books were retrieved successfully. </p>
<p>If you choose to handle errors you can dispatch <strong>FETCH_BOOKS_ERROR</strong> in the error callback or <strong>FETCH_BOOKS_LOADING</strong> before the the request to indicate an ongoing request.</p>
</blockquote>
<p>The HTTP request is made with <a href="https://github.com/mzabriskie/axios" target="_blank">Axios</a>, an <code>npm</code> package. Install via <code>npm</code> by running:</p>
<pre><code>npm install axios --save</code></pre>
<p>Include in the calling code, in our case the <code>bookActions.js</code> file:</p>
<pre><code>import Axios from 'axios';</code></pre>
<h3>Update Reducer To Handle Aync Actions</h3>
<p>Our reducer just needs to return the state as it is from the server when the the <code>FETCH_BOOK_SUCCESS</code> action is dispatched:</p>
<pre><code>// ./src/reducers/bookReducer.js
export default (state = [], action) =&gt; {
  switch (action.type) {
    case 'FETCH_BOOKS_SUCCESS':
          return action.books;
    default:
          return state;
  }
};
</code></pre>
<h3>Dispatch On Page Load</h3>
<p>We need to start the application with some state and the way to go is dispatch the <code>FETCH_BOOKS</code> action on page load. This can be done immediately after configuring the store using the <code>dispatch</code> API:</p>
<pre><code>// .../src/index.js
// ..preceeding codes
const store = configureStore();
store.dispatch(bookActions.fetchBooks());
// ..rest of code</code></pre>
<p>Of course you must import the actions before they can be dispatched:</p>
<pre><code>import * as bookActions from './actions/bookActions';</code></pre>
<p><div class="readableLargeImageContainer"><img src="http://imgur.com/xGGQMn1.jpg" alt="First Thunk" /></div></p>
<p>Applications that just reads that are not so interesting. Let's try to write by posting to our API endpoint. The thunk to do this is not so different from what we already had for read:</p>
<pre><code>// ./src/actions/bookActions.js
export const createBook = (book) =&gt; {
  return (dispatch) =&gt; {
    return Axios.post(apiUrl, book)
      .then(response =&gt; {
        // Dispatch a synchronous action
        // to handle data
        dispatch(createBookSuccess(response.data))
      })
      .catch(error =&gt; {
        throw(error);
      });
  };
};</code></pre>
<p>Then the corresponding synchronous <code>CREATE_BOOK_SUCCES</code> action:</p>
<pre><code>// ./src/actions/bookActions.js
export const createBookSuccess = (book) =&gt; {
  return {
    type: 'CREATE_BOOK_SUCCESS',
    book
  }
};</code></pre>
<p>The thunk will update the data on the server and return the new created <strong>book</strong>. For the sake of UX, rather than do a re-fetch of all the data, we just append the single returned to <strong>book</strong> to the existing <strong>books</strong> state:</p>
<pre><code>// ./src/reducers/bookReducer.js
export default (state = [], action) =&gt; {
  switch (action.type){
    case 'CREATE_BOOK_SUCCESS':
        return [
          ...state,
          Object.assign({}, action.book)
        ];
    case 'FETCH_BOOKS_SUCCESS':
          return action.books;
    default:
          return state;
  }
};</code></pre>
<h2 id="refactor-bookpage">
    <a href="#toc-refactor-bookpage" target="_blank">
      #
      Refactor BookPage
    </a> 
  </h2>
<p>It would be frowned at, if we leave the <code>BookPage</code> component to house the form. What if we have different pages that use this form? It won't be reasonable to re-create it. A better solution is to make the form a component also to improve re-use:</p>
<pre><code>// ./src/components/book/BookForm.js
import React from 'react';

const BookForm = (props) =&gt; {
    // Collector variables
    let titleInput, authorInput, priceInput, yearInput = null;
    return (
      &lt;form onSubmit={e =&gt; {
            e.preventDefault();
            // Assemble data into object
            var input = {
              title: titleInput.value,
              author: authorInput.value,
              price: priceInput.value,
              year: yearInput.value
            };
            // Call method from parent component
            // to handle submission
            props.submitBook(input);
            // Reset form
            e.target.reset();
          }}
            className="form-horizontal"
      &gt;
        &lt;div className="input-group"&gt;
          &lt;label className="col-sm-2 control-label"&gt;Title: &lt;/label&gt;
          &lt;div className="col-sm-10"&gt;
            &lt;input
              type="text"
              name="title"
              ref={node =&gt; titleInput = node}
              className="form-control" /&gt;
          &lt;/div&gt;
        &lt;/div&gt;
        &lt;br/&gt;
        &lt;div className="input-group"&gt;
          &lt;label className="col-sm-2 control-label"&gt;Author: &lt;/label&gt;
          &lt;div className="col-sm-10"&gt;
            &lt;input
              type="text"
              name="author"
              ref={node =&gt; authorInput = node}
              className="form-control" /&gt;
          &lt;/div&gt;
        &lt;/div&gt;
        &lt;br/&gt;
        &lt;div className="input-group"&gt;
          &lt;label className="col-sm-2 control-label"&gt;Price: &lt;/label&gt;
          &lt;div className="col-sm-10"&gt;
            &lt;input
              type="number"
              name="price"
              ref={node =&gt; priceInput = node}
              className="form-control" /&gt;
          &lt;/div&gt;
        &lt;/div&gt;
        &lt;br/&gt;
        &lt;div className="input-group"&gt;
          &lt;label className="col-sm-2 control-label"&gt;Year: &lt;/label&gt;
          &lt;div className="col-sm-10"&gt;
            &lt;input
              type="text"
              name="year"
              ref={node =&gt; yearInput = node}
              className="form-control" /&gt;
          &lt;/div&gt;
        &lt;/div&gt;
        &lt;br/&gt;
        &lt;div className="input-group"&gt;
          &lt;div className="col-sm-offset-2 col-sm-10"&gt;
            &lt;input type="submit" className="btn btn-default"/&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/form&gt;
    );
};

export default BookForm;</code></pre>
<p>Not only did we extract this form, we also added more fields including <strong>Author</strong>, <strong>Price</strong> and <strong>Year</strong>.</p>
<p>There is no need for the luxury of a class component so we used a stateless functional component and to manage events, we delegate them to the parent components by passing them down to the children via <code>props</code>. This is what happens with the <code>submitBook</code> method.</p>
<p>Let's now see what happens with <code>BookPage</code> component after extracting parts of it's JSX:</p>
<pre><code>// ./src/components/book/BookPage.js
import React from 'react';
import { connect } from 'react-redux';
import BookForm from './BookForm';
import { Link } from 'react-router';
import * as bookActions from '../../actions/bookActions';

class Book extends React.Component{
  constructor(props){
    super(props);
  }

  submitBook(input){
    this.props.createBook(input);
  }

  render(){
    let titleInput;
    return(
      &lt;div className="row"&gt;
        &lt;div className="col-md-6"&gt;
          &lt;h3&gt;Books&lt;/h3&gt;
          &lt;table className="table"&gt;
            &lt;thead&gt;
              &lt;th&gt;
                &lt;td&gt;Title&lt;/td&gt;
                &lt;td&gt;&lt;/td&gt;
              &lt;/th&gt;
            &lt;/thead&gt;
            &lt;tbody&gt;
            {this.props.books.map((b, i) =&gt; &lt;tr key={i}&gt;
              &lt;td&gt;{b.title}&lt;/td&gt;
              &lt;td&gt;&lt;Link to={`/books/${b.id}`}&gt;View&lt;/Link&gt;&lt;/td&gt;
            &lt;/tr&gt; )}
            &lt;/tbody&gt;
          &lt;/table&gt;
        &lt;/div&gt;
        &lt;div className="col-md-6"&gt;
          &lt;h3&gt;New Book&lt;/h3&gt;
          {/* Import and inject Book form */}
         &lt;BookForm submitBook={this.submitBook.bind(this)} /&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    )
  }
}
// ... rest of the component code</code></pre>
<p>All we just need to do is to import the <code>BookForm</code> component and inject into the <code>BookPage</code> component. The key line is the one below:</p>
<pre><code>&lt;BookForm submitBook={this.submitBook.bind(this)} /&gt;</code></pre>
<h2 id="book-details-page">
    <a href="#toc-book-details-page" target="_blank">
      #
      Book Details Page
    </a> 
  </h2>
<p>We are making progress and it's a good thing. Next thing to cross off our list is the details page by creating. Just like the <code>BookPage</code> component, we create a wrapper container component and a UI presentation component to display the content. Let's start with the wrapper component:</p>
<pre><code>// ./src/components/book/BookDetailsPage.js
import React, {PropTypes} from 'react';
import {connect} from 'react-redux';
import {bindActionCreators} from 'redux';
import BookDetails from './BookDetails'

class BookDetailsPage extends React.Component {
    constructor(props, context) {
        super(props, context);
    }

    render() {
        return (
            &lt;div&gt;
                &lt;h1&gt;Book Details Page&lt;/h1&gt;
                &lt;BookDetails /&gt;
            &lt;/div&gt;
        );
    }
}

const mapStateToProps = (state, ownProps) =&gt; {
    return {
        // state mappings here
    };
}

const mapDispatchToProps = (dispatch) =&gt; {
    return {
        // actions mappings here
    };
}

export default connect(mapStateToProps, mapDispatchToProps)(BookDetailsPage);</code></pre>
<p>This is an almost empty component which we will build upon as we move on. The only thing to check out is that the <code>BookDetails</code> component is imported and added to the JSX. Let's create that:</p>
<pre><code>// ./sec/components/book/BookDetails.js
import React, {PropTypes} from 'react';

const BookDetails = (props) =&gt; {
    return (
      &lt;div className="media"&gt;
        &lt;div className="media-left"&gt;
          &lt;a href="#"&gt;
            &lt;img className="media-object" src="http://placehold.it/200/450" alt="Placehold" /&gt;
          &lt;/a&gt;
        &lt;/div&gt;
        &lt;div className="media-body"&gt;
          &lt;h4 className="media-heading"&gt;Title&lt;/h4&gt;
          &lt;ul&gt;
            &lt;li&gt;&lt;stron&gt;Author: &lt;/stron&gt; Author&lt;/li&gt;
            &lt;li&gt;&lt;stron&gt;Price: &lt;/stron&gt; Price&lt;/li&gt;
            &lt;li&gt;&lt;stron&gt;Year: &lt;/stron&gt; Year&lt;/li&gt;
            &lt;br/&gt;
            &lt;button className="btn btn-primary"&gt;Buy&lt;/button&gt;
          &lt;/ul&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    );
};

export default BookDetails;</code></pre>
<p><div class="readableLargeImageContainer"><img src="http://imgur.com/5PqxP9a.jpg" alt="Dump Book Details Page" /></div></p>
<p>Basically markup and just showing what we are up to. Now let's move further and consult Redux. Let's begin by adding more actions to our actions file:</p>
<pre><code>// ./src/actions/bookActions.js
// Sync Action
export const fetchBookByIdSuccess = (book) =&gt; {
  return {
    type: actionTypes.FETCH_BOOK_BY_ID_SUCCESS,
    book
  }
};
// Async Action
export const fetchBookById = (bookId) =&gt; {
  return (dispatch) =&gt; {
    return Axios.get(apiUrl + '/' +bookId)
      .then(response =&gt; {
        // Handle data with sync action
        dispatch(fetchBookByIdSuccess(response.data));
      })
      .catch(error =&gt; {
        throw(error);
      });
  };
};</code></pre>
<p>Just like every other async actions we have encountered but this time takes a parameter which is the ID of the book.</p>
<p><code>actionTypes</code> contains all our actions and makes it easy for us to re-use rather than hard-code the action name strings every time:</p>
<pre><code>// ./src/actions/actionTypes.js
export const CREATE_BOOK_SUCCESS = 'CREATE_BOOK_SUCCESS';
export const FETCH_BOOKS_SUCCESS = 'FETCH_BOOKS_SUCCESS';
export const FETCH_BOOK_BY_ID_SUCCESS = 'FETCH_BOOK_BY_ID_SUCCESS';

export const ADD_TO_CART_SUCCESS = 'ADD_TO_CART_SUCCESS';
export const FETCH_CART_SUCCESS = 'FETCH_CART_SUCCESS';</code></pre>
<p>There are more than one options to handle state update in the reducer. Either we just filter the already existing books for the book with the ID we are looking for or fetch the book with the ID from the API and handle with a different reducer.</p>
<p>We will go with the second option I listed above just to demonstrate that it is possible to have multiple reducers in your Redux app. So back to <code>bookReducers</code>, update the content with:</p>
<pre><code>// ./src/reducers/bookReducers.js
// For handling array of books
export const booksReducer = (state = [], action) =&gt; {
  switch (action.type) {
    case actionTypes.CREATE_BOOK_SUCCESS:
        return [
          ...state,
          Object.assign({}, action.book)
        ];
    case actionTypes.FETCH_BOOKS_SUCCESS:
          return action.books;
    default:
          return state;
  }
};

// For handling a single book
export const bookReducer = (state = [], action) =&gt; {
  switch (action.type) {
    // Handle fetch by Id
    case actionTypes.FETCH_BOOK_BY_ID_SUCCESS:
      return action.book;
    default:
      return state;
  }
};</code></pre>
<p>This time the reducers are named so we can use named import to gain access to them from the root reducer file:</p>
<pre><code>// ./src/reducers/index.js
import { combineReducers } from 'redux';
import {booksReducer, bookReducer} from './bookReducers'

export default combineReducers({
  books: booksReducer,
  book: bookReducer
});</code></pre>
<p>Now, we can map our state and actions to the props in the <code>BookDetailsPage</code> component. As usual, we create two functions to handle the tasks and connect these functions to the component:</p>
<pre><code>// ./src/components/book/BookDetailsPage.js
// Map state to props
const mapStateToProps = (state, ownProps) =&gt; {
    return {
      book: state.book
    };
};
// Map dispatch to props
const mapDispatchToProps = (dispatch) =&gt; {
    return {
      // This dispatch will trigger 
      // the Ajax request we setup
      // in our actions
      fetchBookById: bookId =&gt; dispatch(bookActions.fetchBookById(bookId))
    };
};

export default connect(mapStateToProps, mapDispatchToProps)(BookDetailsPage);</code></pre>
<p>We fire the <code>fetchById</code>action method in the component's <code>componentDidMount</code> lifecycle which will start the process immediately the component is ready:</p>
<pre><code>componentDidMount(){
   this.props.fetchBookById(this.props.params.id);
}</code></pre>
<p>Next is to pass down the <strong>book</strong> to <code>BookDetails</code> component via props:</p>
<pre><code>// ./src/components/book/BookDetailsPage.js
&lt;BookDetails book={this.props.book}/&gt;</code></pre>
<p>Then update the <code>BookDetails</code> component to bind the props content to the view:</p>
<pre><code>// ./src/components/book/BookDetails.js
import React from 'react';

const BookDetails = ({book}) =&gt; {
    return (
      &lt;div className="media"&gt;
        &lt;div className="media-left"&gt;
          &lt;a href="#"&gt;
            &lt;img className="media-object" src="http://placehold.it/200/550" alt="Placehold" /&gt;
          &lt;/a&gt;
        &lt;/div&gt;
        &lt;div className="media-body"&gt;
          &lt;h4 className="media-heading"&gt;{book.title}&lt;/h4&gt;
          &lt;ul&gt;
            &lt;li&gt;&lt;stron&gt;Author: &lt;/stron&gt; {book.author}&lt;/li&gt;
            &lt;li&gt;&lt;stron&gt;Price: &lt;/stron&gt; ${book.price}&lt;/li&gt;
            &lt;li&gt;&lt;stron&gt;Year: &lt;/stron&gt; {book.year}&lt;/li&gt;
            &lt;br/&gt;
            &lt;button className="btn btn-primary"&gt;Buy&lt;/button&gt;
          &lt;/ul&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    );
};

export default BookDetails;</code></pre>
<h2 id="persisted-shopping-cart">
    <a href="#toc-persisted-shopping-cart" target="_blank">
      #
      Persisted Shopping Cart
    </a> 
  </h2>
<p>Just to go through the process of Async actions, let's treat one more entity, the <strong>cart</strong>. The logic behind a shopping cart is largely complex compared to just persisting the users cart items on the server but we just need to learn Redux Thunk without considering so much about carts conventions.</p>
<p>Let's iterate through the process as a numbered step so it can serve as a reference for you anytime you have anything to do with React, Redux and Redux Thunk:</p>
<h3>1. Create Components</h3>
<p>We need to create a cart page component but before that, let's update <code>BookDetails</code> so as to handle click event for the <strong>buy</strong> button:</p>
<pre><code>// ./src/components/book/BookDetails.js
import React from 'react';

const BookDetails = ({book, addToCart}) =&gt; {
    return (
      &lt;div className="media"&gt;
        &lt;div className="media-left"&gt;
          &lt;a href="#"&gt;
            &lt;img className="media-object" src="http://placehold.it/200x280" alt="Placehold" /&gt;
          &lt;/a&gt;
        &lt;/div&gt;
        &lt;div className="media-body"&gt;
          &lt;h4 className="media-heading"&gt;{book.title}&lt;/h4&gt;
          &lt;ul&gt;
            &lt;li&gt;&lt;stron&gt;Author: &lt;/stron&gt; {book.author}&lt;/li&gt;
            &lt;li&gt;&lt;stron&gt;Price: &lt;/stron&gt; ${book.price}&lt;/li&gt;
            &lt;li&gt;&lt;stron&gt;Year: &lt;/stron&gt; {book.year}&lt;/li&gt;
            &lt;br/&gt;
            {/* onClick event */}
            &lt;button className="btn btn-primary" onClick={e =&gt; addToCart(book)}&gt;Buy&lt;/button&gt;
          &lt;/ul&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    );
};

export default BookDetails;</code></pre>
<p>The event is handled by a method on the props which is passed down by the parent container so we destructure to get the method. The method is called passing it a book instance. Add the method to <code>BookDetailsPage</code> so it won't be undefined:</p>
<pre><code>addToCart(book){
      const item = {
        title: book.title,
        price: book.price
      };
      this.props.addToCart(item);
    }</code></pre>
<p>Next we create a <code>CartPage</code> to handle items in the cart:</p>
<pre><code>// ./src/components/cart/CartPage.js
import React, {PropTypes} from 'react';
import {connect} from 'react-redux';
import * as bookActions from '../../actions/bookActions';

class CartPage extends React.Component {
    constructor(props, context) {
        super(props, context);
    }

  componentDidMount(){
    this.props.fetchCart();
  }

    render() {
        return (
            &lt;div&gt;
                &lt;h1&gt;Cart Page&lt;/h1&gt;
                &lt;table className="table"&gt;
                  &lt;tr&gt;
                    &lt;th&gt;Title&lt;/th&gt;
                    &lt;th&gt;Price&lt;/th&gt;
                  &lt;/tr&gt;
                  {this.props.items.map((item, index) =&gt; {
                    return (
                      &lt;tr key={index}&gt;
                        &lt;td&gt;{item.title}&lt;/td&gt;
                        &lt;td&gt;{item.price}&lt;/td&gt;
                      &lt;/tr&gt;
                    );
                  })}
                &lt;/table&gt;
            &lt;/div&gt;
        );
    }
}

export default CartPage;</code></pre>
<p>The props will be mapped using React-Redux's connect later but for now, we will stick to the steps. The lifecycle method is also calling a method on the props which is also yet to be mapped but will serve load the cart data once the component mounts.</p>
<p>Finally in this step, we add an extra routes to our existing routes to serve the cart page:</p>
<pre><code>// ./src/routes.js
&lt;Route path="/" component={App}&gt;
   &lt;IndexRoute component={Home}&gt;&lt;/IndexRoute&gt;
   &lt;Route path="/about" component={About}&gt;&lt;/Route&gt;
   &lt;Route path="/books" component={BookPage}&gt;&lt;/Route&gt;
   &lt;Route path="/books/:id" component={BookDetailsPage}&gt;&lt;/Route&gt;
   {/* Extra route to serve Cart. Don't forget to import*/}
   &lt;Route path="/cart" component={CartPage}&gt;&lt;/Route&gt;
 &lt;/Route&gt;</code></pre>
<h3>2 Actions & Action Creators</h3>
<p>We need to adding items and fetching items and each of this process will have an async action which use thunk to do the API fetch and a sync action which is dispatched with async's returned data:</p>
<pre><code>// ./src/actions/bookActions.js
// Sync add to cart
export const addToCartSuccess = (item) =&gt; {
  return {
    type: 'ADD_TO_CART_SUCCESS',
    item
  }
};
// Async add to cart
export const addToCart = (item) =&gt; {
  return (dispatch) =&gt; {
    return Axios.post('http://57c64baac1fc8711008f2a82.mockapi.io/Cart', item)
      .then(response =&gt; {
        dispatch(addToCartSuccess(response.data))
      })
      .catch(error =&gt; {
        throw(error);
      });
  };
};
// Sync load cart
export const fetchCartSuccess = (items) =&gt; {
  return {
    type: 'FETCH_CART_SUCCESS',
    items
  }
};
// Async load cart
export const fetchCart = () =&gt; {
  return (dispatch) =&gt; {
    return Axios.get('http://57c64baac1fc8711008f2a82.mockapi.io/Cart')
      .then(response =&gt; {
        dispatch(fetchCartSuccess(response.data))
      })
      .catch(error =&gt; {
        throw(error);
      });
  };
};</code></pre>
<h3>3. State Reducers For Actions</h3>
<p>With the actions set, we can set up reducers to update state based on the actions we created. The reducers for cart is simple:</p>
<pre><code>// ./src/reducers/cartReducers.js
export default (state = [], action) =&gt; {
  switch (action.type) {
    case 'ADD_TO_CART_SUCCESS':
      return action.item;
    case 'FETCH_CART_SUCCESS':
      return action.items;
    default:
      return state;
  }
};
</code></pre>
<h3>4. Connect Component</h3>
<p>Most boilerplate task like configuring and creating store was skipped because we already did that in the previous article. We just need to connect our <code>CartPage</code> component and then map states and actions to it's props:</p>
<pre><code>// ./src/components/cart/CartPage.js
// ...rest of component body
const mapStateToProps = (state, ownProps) =&gt; {
    return {
      items: state.cart
    };
};

const mapDispatchToProps = (dispatch) =&gt; {
    return {
      fetchCart: bookId =&gt; dispatch(bookActions.fetchCart()),
    };
};

export default connect(mapStateToProps, mapDispatchToProps)(CartPage);</code></pre>
<p>Now the <code>items</code> and <code>fetchCart</code> props which we were making use of in the component body are now defined and has a value.</p>
<p><div class="readableLargeImageContainer"><img alt="Cart Page" /></div></p>
<h2 id="wrap-up">
    <a href="#toc-wrap-up" target="_blank">
      #
      Wrap up
    </a> 
  </h2>
<p>Glad to we got to the end of this tutorial. Redux Thunk has alternatives like <a href="https://github.com/yelouafi/redux-saga" target="_blank">Redux Saga</a> which makes use of ES6 generators and you can check out. </p>
<p>You could observe the the app is not frictionless and shows stale data for a while before updating while navigating. What you could do is use a loading indicator to delay display until the new data is ready.</p>
<p>Also checkout <a href="https://github.com/reactjs/react-router-redux" target="_blank">React-Rouer-Redux</a> which keeps everything in sync between React, Redux and React Router.</p>

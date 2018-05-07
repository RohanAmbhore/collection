<a href="https://github.com/on3iro/Trigen/blob/12a12040f620bb48400eaf2028fd0fcc160d40d5/src/containers/Auth/ducks/tests/sagas.test.js">https://github.com/on3iro/Trigen/blob/12a12040f620bb48400eaf2028fd0fcc160d40d5/src/containers/Auth/ducks/tests/sagas.test.js</a><div id="articleHeader"><h1>Trigen/sagas.test.js at 12a12040f620bb48400eaf2028fd0fcc160d40d5 · on3iro/Trigen</h1></div>
      <table>
      <tbody><tr>
        <td id="L1"></td>
        <td id="LC1">import { takeLatest, call, put } from 'redux-saga/effects';</td>
      </tr>
      <tr>
        <td id="L2"></td>
        <td id="LC2">import axios from 'axios';</td>
      </tr>
      
      <tr>
        <td id="L4"></td>
        <td id="LC4">import * as sagas from '../sagas';</td>
      </tr>
      <tr>
        <td id="L5"></td>
        <td id="LC5">import * as types from '../actionTypes';</td>
      </tr>
      
      
      <tr>
        <td id="L8"></td>
        <td id="LC8">describe('handleAuthSaga', () =&gt; {</td>
      </tr>
      <tr>
        <td id="L9"></td>
        <td id="LC9">  const handleAuthSaga = sagas.handleAuth();</td>
      </tr>
      
      <tr>
        <td id="L11"></td>
        <td id="LC11">  it('should start task to watch LOGIN_SUBMIT', () =&gt; {</td>
      </tr>
      <tr>
        <td id="L12"></td>
        <td id="LC12">    const takeLatestDescriptor = handleAuthSaga.next().value;</td>
      </tr>
      <tr>
        <td id="L13"></td>
        <td id="LC13">    const expectedYield = takeLatest(types.LOGIN_SUBMIT, sagas.requestLogin);</td>
      </tr>
      <tr>
        <td id="L14"></td>
        <td id="LC14">    expect(takeLatestDescriptor).toMatchSnapshot();</td>
      </tr>
      
      
      <tr>
        <td id="L17"></td>
        <td id="LC17">  it('should start taks to watch REGISTER_SUBMIT', () =&gt; {</td>
      </tr>
      <tr>
        <td id="L18"></td>
        <td id="LC18">    const takeLatestDescriptor = handleAuthSaga.next().value;</td>
      </tr>
      <tr>
        <td id="L19"></td>
        <td id="LC19">    const expectedYield = takeLatest(types.REGISTER_SUBMIT, sagas.requestRegister);</td>
      </tr>
      <tr>
        <td id="L20"></td>
        <td id="LC20">    expect(takeLatestDescriptor).toMatchSnapshot();</td>
      </tr>
      
      
      
      <tr>
        <td id="L24"></td>
        <td id="LC24">describe('login', () =&gt; {</td>
      </tr>
      
      <tr>
        <td id="L26"></td>
        <td id="LC26">  describe('requestLogin generator', () =&gt; {</td>
      </tr>
      <tr>
        <td id="L27"></td>
        <td id="LC27">    const action = {</td>
      </tr>
      <tr>
        <td id="L28"></td>
        <td id="LC28">      payload: {</td>
      </tr>
      <tr>
        <td id="L29"></td>
        <td id="LC29">        test: 'test',</td>
      </tr>
      
      
      <tr>
        <td id="L32"></td>
        <td id="LC32">    let requestLoginGenerator;</td>
      </tr>
      
      <tr>
        <td id="L34"></td>
        <td id="LC34">    beforeEach(() =&gt; {</td>
      </tr>
      <tr>
        <td id="L35"></td>
        <td id="LC35">      requestLoginGenerator = sagas.requestLogin(action);</td>
      </tr>
      
      
      <tr>
        <td id="L38"></td>
        <td id="LC38">    it('should call axios.post', () =&gt; {</td>
      </tr>
      <tr>
        <td id="L39"></td>
        <td id="LC39">      const callDescriptor = requestLoginGenerator.next().value;</td>
      </tr>
      <tr>
        <td id="L40"></td>
        <td id="LC40">      const expectedYield = call(axios.post, 'http://localhost:3030/api/auth/login', action.payload, { headers: {'Content-Type': 'application/json'}});</td>
      </tr>
      <tr>
        <td id="L41"></td>
        <td id="LC41">      expect(callDescriptor).toMatchSnapshot();</td>
      </tr>
      
      
      <tr>
        <td id="L44"></td>
        <td id="LC44">    it('should put LOGIN_SUCCESS action with payload', () =&gt; {</td>
      </tr>
      <tr>
        <td id="L45"></td>
        <td id="LC45">      const response = {</td>
      </tr>
      <tr>
        <td id="L46"></td>
        <td id="LC46">        data: {</td>
      </tr>
      <tr>
        <td id="L47"></td>
        <td id="LC47">          id: 1,</td>
      </tr>
      <tr>
        <td id="L48"></td>
        <td id="LC48">          email: 'foo@bar.com',</td>
      </tr>
      <tr>
        <td id="L49"></td>
        <td id="LC49">          name: 'foo',</td>
      </tr>
      <tr>
        <td id="L50"></td>
        <td id="LC50">          token: 'abc123',</td>
      </tr>
      
      
      <tr>
        <td id="L53"></td>
        <td id="LC53">      requestLoginGenerator.next().value;</td>
      </tr>
      <tr>
        <td id="L54"></td>
        <td id="LC54">      const putDescriptor = requestLoginGenerator.next(response).value;</td>
      </tr>
      <tr>
        <td id="L55"></td>
        <td id="LC55">      const expectedYield = put({ type: types.LOGIN_SUCCESS, payload: {</td>
      </tr>
      <tr>
        <td id="L56"></td>
        <td id="LC56">        id: 1,</td>
      </tr>
      <tr>
        <td id="L57"></td>
        <td id="LC57">        email: 'foo@bar.com',</td>
      </tr>
      <tr>
        <td id="L58"></td>
        <td id="LC58">        name: 'foo',</td>
      </tr>
      <tr>
        <td id="L59"></td>
        <td id="LC59">        token: 'abc123',</td>
      </tr>
      
      <tr>
        <td id="L61"></td>
        <td id="LC61">      expect(putDescriptor).toMatchSnapshot();</td>
      </tr>
      
      
      <tr>
        <td id="L64"></td>
        <td id="LC64">    it('should put LOGIN_ERROR action', () =&gt; {</td>
      </tr>
      <tr>
        <td id="L65"></td>
        <td id="LC65">      const response = new Error('Some error');</td>
      </tr>
      <tr>
        <td id="L66"></td>
        <td id="LC66">      requestLoginGenerator.next().value;</td>
      </tr>
      <tr>
        <td id="L67"></td>
        <td id="LC67">      const putDescriptor = requestLoginGenerator.throw(response).value;</td>
      </tr>
      <tr>
        <td id="L68"></td>
        <td id="LC68">      const expectedYield = put({ type: types.LOGIN_ERROR, payload: 'Some error'  });</td>
      </tr>
      <tr>
        <td id="L69"></td>
        <td id="LC69">      expect(putDescriptor).toMatchSnapshot();</td>
      </tr>
      
      
      
      
      <tr>
        <td id="L74"></td>
        <td id="LC74">describe('register', () =&gt; {</td>
      </tr>
      
      <tr>
        <td id="L76"></td>
        <td id="LC76">  describe('requestRegister generator', () =&gt; {</td>
      </tr>
      <tr>
        <td id="L77"></td>
        <td id="LC77">    const action = {</td>
      </tr>
      <tr>
        <td id="L78"></td>
        <td id="LC78">      payload: {</td>
      </tr>
      <tr>
        <td id="L79"></td>
        <td id="LC79">        test: 'test'</td>
      </tr>
      
      
      <tr>
        <td id="L82"></td>
        <td id="LC82">    let requestRegisterGenerator;</td>
      </tr>
      
      <tr>
        <td id="L84"></td>
        <td id="LC84">    beforeEach(() =&gt; {</td>
      </tr>
      <tr>
        <td id="L85"></td>
        <td id="LC85">      requestRegisterGenerator = sagas.requestRegister(action);</td>
      </tr>
      
      
      <tr>
        <td id="L88"></td>
        <td id="LC88">    it('should call axios.post', () =&gt; {</td>
      </tr>
      <tr>
        <td id="L89"></td>
        <td id="LC89">      const callDescriptor = requestRegisterGenerator.next().value;</td>
      </tr>
      <tr>
        <td id="L90"></td>
        <td id="LC90">      const expectedYield = call(axios.post, 'http://localhost:3030/api/auth/register', action.payload, { headers: {'Content-Type': 'application/json'}});</td>
      </tr>
      <tr>
        <td id="L91"></td>
        <td id="LC91">      expect(callDescriptor).toMatchSnapshot();</td>
      </tr>
      
      
      <tr>
        <td id="L94"></td>
        <td id="LC94">    it('should put REGISTER_SUCCESS action with payload', () =&gt; {</td>
      </tr>
      <tr>
        <td id="L95"></td>
        <td id="LC95">      const response = {</td>
      </tr>
      <tr>
        <td id="L96"></td>
        <td id="LC96">        data: {</td>
      </tr>
      <tr>
        <td id="L97"></td>
        <td id="LC97">          id: 1,</td>
      </tr>
      <tr>
        <td id="L98"></td>
        <td id="LC98">          email: 'foo@bar.com',</td>
      </tr>
      <tr>
        <td id="L99"></td>
        <td id="LC99">          name: 'foo',</td>
      </tr>
      <tr>
        <td id="L100"></td>
        <td id="LC100">          token: 'abc123',</td>
      </tr>
      
      
      <tr>
        <td id="L103"></td>
        <td id="LC103">      requestRegisterGenerator.next().value;</td>
      </tr>
      <tr>
        <td id="L104"></td>
        <td id="LC104">      const putDescriptor = requestRegisterGenerator.next(response).value;</td>
      </tr>
      <tr>
        <td id="L105"></td>
        <td id="LC105">      const expectedYield = put({ type: types.REGISTER_SUCCESS, payload: {</td>
      </tr>
      <tr>
        <td id="L106"></td>
        <td id="LC106">        id: 1,</td>
      </tr>
      <tr>
        <td id="L107"></td>
        <td id="LC107">        email: 'foo@bar.com',</td>
      </tr>
      <tr>
        <td id="L108"></td>
        <td id="LC108">        name: 'foo',</td>
      </tr>
      <tr>
        <td id="L109"></td>
        <td id="LC109">        token: 'abc123',</td>
      </tr>
      
      <tr>
        <td id="L111"></td>
        <td id="LC111">      expect(putDescriptor).toMatchSnapshot();</td>
      </tr>
      
      
      <tr>
        <td id="L114"></td>
        <td id="LC114">    it('should put REGISTER_ERROR action', () =&gt; {</td>
      </tr>
      <tr>
        <td id="L115"></td>
        <td id="LC115">      const response = new Error('Some error');</td>
      </tr>
      <tr>
        <td id="L116"></td>
        <td id="LC116">      requestRegisterGenerator.next().value;</td>
      </tr>
      <tr>
        <td id="L117"></td>
        <td id="LC117">      const putDescriptor = requestRegisterGenerator.throw(response).value;</td>
      </tr>
      <tr>
        <td id="L118"></td>
        <td id="LC118">      const expectedYield = put({ type: types.REGISTER_ERROR, payload: 'Some error'  });</td>
      </tr>
      <tr>
        <td id="L119"></td>
        <td id="LC119">      expect(putDescriptor).toMatchSnapshot();</td>
      </tr>
      
      
      
</tbody></table>

  

  
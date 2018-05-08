<a href="https://github.com/vuhieu2610/smartAdmin/blob/1564c641ba29eea38e2a709bb362e5821ab99454/src/app/routes/systems/component/branch.js">https://github.com/vuhieu2610/smartAdmin/blob/1564c641ba29eea38e2a709bb362e5821ab99454/src/app/routes/systems/component/branch.js</a><div id="articleHeader"><h1>smartAdmin/branch.js at 1564c641ba29eea38e2a709bb362e5821ab99454 · vuhieu2610/smartAdmin</h1></div>
      <table>
      <tbody><tr>
        <td id="L1"></td>
        <td id="LC1">import React, { Component } from 'react';</td>
      </tr>
      <tr>
        <td id="L2"></td>
        <td id="LC2">import { bindActionCreators } from 'redux';</td>
      </tr>
      <tr>
        <td id="L3"></td>
        <td id="LC3">import {connect} from 'react-redux';</td>
      </tr>
      <tr>
        <td id="L4"></td>
        <td id="LC4">import ReactTable from 'react-table';</td>
      </tr>
      <tr>
        <td id="L5"></td>
        <td id="LC5">import {Checkbox, Button, Icon, Modal, message} from 'antd';</td>
      </tr>
      <tr>
        <td id="L6"></td>
        <td id="LC6">import * as systemActions from '../systemActions';</td>
      </tr>
      <tr>
        <td id="L7"></td>
        <td id="LC7">import { config } from '../../../config/config';</td>
      </tr>
      <tr>
        <td id="L8"></td>
        <td id="LC8">import { BigBreadcrumbs } from '../../../components';</td>
      </tr>
      
      
      <tr>
        <td id="L11"></td>
        <td id="LC11">const confirm = Modal.confirm;</td>
      </tr>
      
      <tr>
        <td id="L13"></td>
        <td id="LC13">function mapStateToProps(state) {</td>
      </tr>
      <tr>
        <td id="L14"></td>
        <td id="LC14">  return { system: state.system };</td>
      </tr>
      
      <tr>
        <td id="L16"></td>
        <td id="LC16">function mapDispatchToProps(dispatch) {</td>
      </tr>
      <tr>
        <td id="L17"></td>
        <td id="LC17">  return bindActionCreators(systemActions, dispatch);</td>
      </tr>
      
      
      <tr>
        <td id="L20"></td>
        <td id="LC20">function resizeTable(){</td>
      </tr>
      <tr>
        <td id="L21"></td>
        <td id="LC21">  document.querySelector('.ReactTable').style.height = document.body.offsetHeight - document.querySelector('#header').offsetHeight - document.querySelector('.control-box').offsetHeight - document.querySelector('#bigBreadcrumbs').offsetHeight - 20  + 'px';</td>
      </tr>
      
      
      
      <tr>
        <td id="L25"></td>
        <td id="LC25">let self_ = null;</td>
      </tr>
      <tr>
        <td id="L26"></td>
        <td id="LC26">class System extends Component {</td>
      </tr>
      <tr>
        <td id="L27"></td>
        <td id="LC27">  constructor(props){</td>
      </tr>
      <tr>
        <td id="L28"></td>
        <td id="LC28">    super(props);</td>
      </tr>
      <tr>
        <td id="L29"></td>
        <td id="LC29">    this.onFetchData = this.onFetchData.bind(this);</td>
      </tr>
      <tr>
        <td id="L30"></td>
        <td id="LC30">    self_ = this;</td>
      </tr>
      
      
      <tr>
        <td id="L33"></td>
        <td id="LC33">  componentDidMount(){</td>
      </tr>
      <tr>
        <td id="L34"></td>
        <td id="LC34">    this.loadData();</td>
      </tr>
      <tr>
        <td id="L35"></td>
        <td id="LC35">    resizeTable();</td>
      </tr>
      <tr>
        <td id="L36"></td>
        <td id="LC36">    window.addEventListener('resize', resizeTable, true);</td>
      </tr>
      
      
      <tr>
        <td id="L39"></td>
        <td id="LC39">  loadData(){</td>
      </tr>
      <tr>
        <td id="L40"></td>
        <td id="LC40">    const {  system } = self_.props;</td>
      </tr>
      <tr>
        <td id="L41"></td>
        <td id="LC41">    let { pageSize, countSkip } = system.catBranch || {};</td>
      </tr>
      <tr>
        <td id="L42"></td>
        <td id="LC42">    pageSize = pageSize || 10;</td>
      </tr>
      <tr>
        <td id="L43"></td>
        <td id="LC43">    countSkip = countSkip || 0;</td>
      </tr>
      <tr>
        <td id="L44"></td>
        <td id="LC44">    const params = {countSkip,pageSize};</td>
      </tr>
      <tr>
        <td id="L45"></td>
        <td id="LC45">    this.props.catData({url: `${config.cdn}/api/w/v1/catbranch`, params});</td>
      </tr>
      
      
      <tr>
        <td id="L48"></td>
        <td id="LC48">  renderCheckbox(element){</td>
      </tr>
      <tr>
        <td id="L49"></td>
        <td id="LC49">    const { original } = element;</td>
      </tr>
      <tr>
        <td id="L50"></td>
        <td id="LC50">    const { selectedElement } = self_.props.system || [];</td>
      </tr>
      <tr>
        <td id="L51"></td>
        <td id="LC51">    const isChecked = selectedElement.indexOf(original) &gt; -1;</td>
      </tr>
      <tr>
        <td id="L52"></td>
        <td id="LC52">    return(</td>
      </tr>
      <tr>
        <td id="L53"></td>
        <td id="LC53">      &lt;Checkbox checked={isChecked}  onChange={e=&gt;self_.props.selectedElement(e.target.checked, original)} /&gt;</td>
      </tr>
      
      
      
      <tr>
        <td id="L57"></td>
        <td id="LC57">  async removeItems(arr){</td>
      </tr>
      <tr>
        <td id="L58"></td>
        <td id="LC58">    for(let i = 0; i &lt; arr.length; i++ ){</td>
      </tr>
      <tr>
        <td id="L59"></td>
        <td id="LC59">      const item = arr[i];</td>
      </tr>
      <tr>
        <td id="L60"></td>
        <td id="LC60">      let req = await self_.props.removeItem(`${config.cdn}/api/w/v1/catbranch/id`, item);</td>
      </tr>
      <tr>
        <td id="L61"></td>
        <td id="LC61">      const { msg } = req.data;</td>
      </tr>
      <tr>
        <td id="L62"></td>
        <td id="LC62">      if(msg !== 'SUC_ACTION'){</td>
      </tr>
      <tr>
        <td id="L63"></td>
        <td id="LC63">        message.error(`Can't remove this item, something went wrong!`);</td>
      </tr>
      <tr>
        <td id="L64"></td>
        <td id="LC64">        return;</td>
      </tr>
      
      
      <tr>
        <td id="L67"></td>
        <td id="LC67">    message.success('Removing Successful!');</td>
      </tr>
      <tr>
        <td id="L68"></td>
        <td id="LC68">    self_.loadData();</td>
      </tr>
      <tr>
        <td id="L69"></td>
        <td id="LC69">    return;</td>
      </tr>
      
      
      <tr>
        <td id="L72"></td>
        <td id="LC72">  renderActionsCell(e){</td>
      </tr>
      <tr>
        <td id="L73"></td>
        <td id="LC73">    return(</td>
      </tr>
      <tr>
        <td id="L74"></td>
        <td id="LC74">      &lt;div&gt;</td>
      </tr>
      <tr>
        <td id="L75"></td>
        <td id="LC75">        &lt;Button</td>
      </tr>
      <tr>
        <td id="L76"></td>
        <td id="LC76">          type="ghost"</td>
      </tr>
      <tr>
        <td id="L77"></td>
        <td id="LC77">          size="large"</td>
      </tr>
      <tr>
        <td id="L78"></td>
        <td id="LC78">        &gt;&lt;Icon type="edit" /&gt;&lt;/Button&gt;</td>
      </tr>
      <tr>
        <td id="L79"></td>
        <td id="LC79">        &lt;Button</td>
      </tr>
      <tr>
        <td id="L80"></td>
        <td id="LC80">          type="danger"</td>
      </tr>
      <tr>
        <td id="L81"></td>
        <td id="LC81">          size="large"</td>
      </tr>
      <tr>
        <td id="L82"></td>
        <td id="LC82">          onClick={el =&gt; self_.showConfirm('Do you Want to remove this items?', [e.original.id])}</td>
      </tr>
      <tr>
        <td id="L83"></td>
        <td id="LC83">        &gt;&lt;Icon type="delete" /&gt;&lt;/Button&gt;</td>
      </tr>
      <tr>
        <td id="L84"></td>
        <td id="LC84">      &lt;/div&gt;</td>
      </tr>
      
      
      
      <tr>
        <td id="L88"></td>
        <td id="LC88">  onFetchData(state, instance){</td>
      </tr>
      <tr>
        <td id="L89"></td>
        <td id="LC89">    const {pageSize, page} = state;</td>
      </tr>
      <tr>
        <td id="L90"></td>
        <td id="LC90">    self_.props.catData({url: `${config.cdn}/api/w/v1/catbranch`, params: {countSkip:(page*pageSize),pageSize}});</td>
      </tr>
      
      
      <tr>
        <td id="L93"></td>
        <td id="LC93">  showConfirm(title, id){</td>
      </tr>
      <tr>
        <td id="L94"></td>
        <td id="LC94">    confirm({</td>
      </tr>
      <tr>
        <td id="L95"></td>
        <td id="LC95">      title: title,</td>
      </tr>
      <tr>
        <td id="L96"></td>
        <td id="LC96">      okText: 'Yes',</td>
      </tr>
      <tr>
        <td id="L97"></td>
        <td id="LC97">      okType: 'danger',</td>
      </tr>
      <tr>
        <td id="L98"></td>
        <td id="LC98">      cancelText: 'No',</td>
      </tr>
      <tr>
        <td id="L99"></td>
        <td id="LC99">      destroyOnClose: true,</td>
      </tr>
      <tr>
        <td id="L100"></td>
        <td id="LC100">      async onOk(){</td>
      </tr>
      <tr>
        <td id="L101"></td>
        <td id="LC101">        await self_.removeItems(id);</td>
      </tr>
      
      
      
      
      <tr>
        <td id="L106"></td>
        <td id="LC106">  render(){</td>
      </tr>
      <tr>
        <td id="L107"></td>
        <td id="LC107">    const { system } = this.props;</td>
      </tr>
      <tr>
        <td id="L108"></td>
        <td id="LC108">    const {pageSize, countSkip, data, totalRecords} = system.catBranch || {};</td>
      </tr>
      <tr>
        <td id="L109"></td>
        <td id="LC109">    const ids = data?data.map(item=&gt;item.id):[];</td>
      </tr>
      <tr>
        <td id="L110"></td>
        <td id="LC110">    return(</td>
      </tr>
      <tr>
        <td id="L111"></td>
        <td id="LC111">      &lt;div id="content"&gt;</td>
      </tr>
      <tr>
        <td id="L112"></td>
        <td id="LC112">        &lt;div className="row" id="bigBreadcrumbs"&gt;</td>
      </tr>
      <tr>
        <td id="L113"></td>
        <td id="LC113">          &lt;BigBreadcrumbs</td>
      </tr>
      <tr>
        <td id="L114"></td>
        <td id="LC114">            items={['Systems', 'Branch']}</td>
      </tr>
      <tr>
        <td id="L115"></td>
        <td id="LC115">            icon="fa fa-fw fa-table"</td>
      </tr>
      <tr>
        <td id="L116"></td>
        <td id="LC116">            className="col-xs-12 col-sm-7 col-md-7 col-lg-4"</td>
      </tr>
      <tr>
        <td id="L117"></td>
        <td id="LC117">          /&gt;</td>
      </tr>
      <tr>
        <td id="L118"></td>
        <td id="LC118">          &lt;div className="col-xs-12 col-sm-5 col-md-5 col-lg-8 ta-r"&gt;</td>
      </tr>
      <tr>
        <td id="L119"></td>
        <td id="LC119">            &lt;Button size="large"&gt;Export Data&lt;/Button&gt;</td>
      </tr>
      <tr>
        <td id="L120"></td>
        <td id="LC120">          &lt;/div&gt;</td>
      </tr>
      <tr>
        <td id="L121"></td>
        <td id="LC121">        &lt;/div&gt;</td>
      </tr>
      <tr>
        <td id="L122"></td>
        <td id="LC122">        &lt;div className="control-box"&gt;</td>
      </tr>
      <tr>
        <td id="L123"></td>
        <td id="LC123">          &lt;Button.Group&gt;</td>
      </tr>
      <tr>
        <td id="L124"></td>
        <td id="LC124">            &lt;Button</td>
      </tr>
      <tr>
        <td id="L125"></td>
        <td id="LC125">              type     = "danger"</td>
      </tr>
      <tr>
        <td id="L126"></td>
        <td id="LC126">              disabled = {system.selectedElement.length &gt; 0?false:true}</td>
      </tr>
      <tr>
        <td id="L127"></td>
        <td id="LC127">              onClick  = {e =&gt; self_.showConfirm('Do you Want to remove these items?', self_.removeItems(ids))}</td>
      </tr>
      <tr>
        <td id="L128"></td>
        <td id="LC128">            &gt;Remove Selected&lt;/Button&gt;</td>
      </tr>
      <tr>
        <td id="L129"></td>
        <td id="LC129">            &lt;Button type="primary"&gt;Add New&lt;/Button&gt;</td>
      </tr>
      <tr>
        <td id="L130"></td>
        <td id="LC130">          &lt;/Button.Group&gt;</td>
      </tr>
      <tr>
        <td id="L131"></td>
        <td id="LC131">        &lt;/div&gt;</td>
      </tr>
      <tr>
        <td id="L132"></td>
        <td id="LC132">        &lt;ReactTable</td>
      </tr>
      <tr>
        <td id="L133"></td>
        <td id="LC133">          defaultPageSize = { pageSize }</td>
      </tr>
      <tr>
        <td id="L134"></td>
        <td id="LC134">          data            = { data }</td>
      </tr>
      <tr>
        <td id="L135"></td>
        <td id="LC135">          className       = "-striped -highlight"</td>
      </tr>
      <tr>
        <td id="L136"></td>
        <td id="LC136">          sortable        = {false}</td>
      </tr>
      <tr>
        <td id="L137"></td>
        <td id="LC137">          filterable      =  {false}</td>
      </tr>
      <tr>
        <td id="L138"></td>
        <td id="LC138">          columns         = {[</td>
      </tr>
      
      <tr>
        <td id="L140"></td>
        <td id="LC140">              Header: e =&gt; (&lt;Checkbox checked={data && system.selectedElement.length === data.length} onChange={el=&gt;self_.props.selectAll(el.target.checked?[...data]:[])} /&gt;),</td>
      </tr>
      <tr>
        <td id="L141"></td>
        <td id="LC141">              accessor: 'id',</td>
      </tr>
      <tr>
        <td id="L142"></td>
        <td id="LC142">              style: {textAlign: 'center'},</td>
      </tr>
      <tr>
        <td id="L143"></td>
        <td id="LC143">              Cell: e=&gt; self_.renderCheckbox(e),</td>
      </tr>
      <tr>
        <td id="L144"></td>
        <td id="LC144">              maxWidth: 50,</td>
      </tr>
      <tr>
        <td id="L145"></td>
        <td id="LC145">              resizable: false,</td>
      </tr>
      
      <tr>
        <td id="L147"></td>
        <td id="LC147">              Header: 'Name',</td>
      </tr>
      <tr>
        <td id="L148"></td>
        <td id="LC148">              accessor: 'name',</td>
      </tr>
      <tr>
        <td id="L149"></td>
        <td id="LC149">              width: 250</td>
      </tr>
      
      <tr>
        <td id="L151"></td>
        <td id="LC151">              Header: 'Code',</td>
      </tr>
      <tr>
        <td id="L152"></td>
        <td id="LC152">              accessor: 'code',</td>
      </tr>
      <tr>
        <td id="L153"></td>
        <td id="LC153">              width: 150</td>
      </tr>
      
      <tr>
        <td id="L155"></td>
        <td id="LC155">              Header: 'Description',</td>
      </tr>
      <tr>
        <td id="L156"></td>
        <td id="LC156">              accessor: 'description',</td>
      </tr>
      <tr>
        <td id="L157"></td>
        <td id="LC157">              width: 250</td>
      </tr>
      
      <tr>
        <td id="L159"></td>
        <td id="LC159">              Header: 'Is Active',</td>
      </tr>
      <tr>
        <td id="L160"></td>
        <td id="LC160">              accessor: 'isActive',</td>
      </tr>
      <tr>
        <td id="L161"></td>
        <td id="LC161">              Cell: e=&gt; (&lt;Checkbox defaultChecked={e.value} disabled={true} /&gt;),</td>
      </tr>
      <tr>
        <td id="L162"></td>
        <td id="LC162">              style: {textAlign: 'center'},</td>
      </tr>
      <tr>
        <td id="L163"></td>
        <td id="LC163">              resizable: false,</td>
      </tr>
      <tr>
        <td id="L164"></td>
        <td id="LC164">              maxWidth: 80</td>
      </tr>
      
      <tr>
        <td id="L166"></td>
        <td id="LC166">              Header: 'Company Name',</td>
      </tr>
      <tr>
        <td id="L167"></td>
        <td id="LC167">              accessor: 'catCompanyName',</td>
      </tr>
      <tr>
        <td id="L168"></td>
        <td id="LC168">              width: 150</td>
      </tr>
      
      <tr>
        <td id="L170"></td>
        <td id="LC170">              Header: 'Actions',</td>
      </tr>
      <tr>
        <td id="L171"></td>
        <td id="LC171">              accessor: 'id',</td>
      </tr>
      <tr>
        <td id="L172"></td>
        <td id="LC172">              Cell: self_.renderActionsCell,</td>
      </tr>
      <tr>
        <td id="L173"></td>
        <td id="LC173">              style: {textAlign: 'center'},</td>
      </tr>
      <tr>
        <td id="L174"></td>
        <td id="LC174">              resizable: false,</td>
      </tr>
      <tr>
        <td id="L175"></td>
        <td id="LC175">              width: 150</td>
      </tr>
      
      
      <tr>
        <td id="L178"></td>
        <td id="LC178">          pages           = {Math.ceil(totalRecords / pageSize)}</td>
      </tr>
      <tr>
        <td id="L179"></td>
        <td id="LC179">          manual</td>
      </tr>
      <tr>
        <td id="L180"></td>
        <td id="LC180">          onFetchData     = {(state, instance) =&gt; self_.onFetchData(state, instance)}</td>
      </tr>
      <tr>
        <td id="L181"></td>
        <td id="LC181">        /&gt;</td>
      </tr>
      <tr>
        <td id="L182"></td>
        <td id="LC182">      &lt;/div&gt;</td>
      </tr>
      
      
      
      
      <tr>
        <td id="L187"></td>
        <td id="LC187">export default connect(mapStateToProps, mapDispatchToProps)(System);</td>
      </tr>
</tbody></table>

  

  
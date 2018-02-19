<a href="http://blog.csdn.net/qq_24122593/article/details/53585378">http://blog.csdn.net/qq_24122593/article/details/53585378</a><div id="articleHeader"><h1>        <a href="/qq_24122593/article/details/53585378" target="_blank">        vuejs学习“递归组件”                           </a>                     </h1></div>


    
    <div>
        <div>
            2016-12-12 18:05
            2364人阅读
             <a href="#comments" target="_blank">评论</a>(0)
             <a href="javascript:void(0);" title="收藏" target="_blank">收藏</a>
              <a href="#report" title="举报" target="_blank">举报</a>

        </div>
        
    
      








<p>
　　学习vue有一段时间了，最近使用vue做了一套后台管理系统，其中使用最多就是递归组件，也因为自己对官方文档的不熟悉使得自己踩了不少坑，今天写出来和大家一起分享。</p>

<p>
　　组件在它的模板内可以递归地调用自己，只有当它有 <code>name</code> 选项时才可以。 在官网这句话就是关键定义组件是一定要有name属性。按照这个思路我们开动吧。</p>
<p>
　　实现最终效果图：</p>
<p>
　　　　<div class="readableLargeImageContainer float"><img src="http://images2015.cnblogs.com/blog/981750/201611/981750-20161117181216185-2102001765.png" /></div></p>
<p>
　　模拟数据格式如下：</p>
<div>

<pre>var data = [{
                "id": "1",
                "data": {
                    "menuName": "项目管理",
                    "menuCode": "",
                },
                "childTreeNode": [{
                    "data": {
                        "menuName": "项目",
                        "menuCode": "BusProject",
                    },
                    "childTreeNode": []
                }, {
                    "data": {
                        "menuName": "我的任务",
                        "menuCode": "BusProject",
                    },
                    "childTreeNode": []
                }, {
                    "data": {
                        "menuName": "人员周报",
                        "menuCode": "BusProject",
                    },
                    "childTreeNode": []
                }]
            }, {
                "id": "2",
                "data": {
                    "menuName": "数据统计",
                    "menuCode": "BusClock",
                },
                "childTreeNode": []
            }, {
                "id": "3",
                "data": {
                    "menuName": "人事管理",
                    "menuCode": "",
                },
                "childTreeNode": []
            }, {
                "id": "4",
                "data": {
                    "menuName": "基础管理",
                    "menuCode": "",
                },
                "childTreeNode": []
            }]</pre>

</div>
<p>
html我们思路按照ul里面套li，无限ul套li，标题用div元素包裹，</p>
<div>

<pre>&lt;li&gt;
    &lt;div @click='toggle'&gt;<br />　　
         &lt;i v-if='isFolder' class="fa " :class="[open?'fa-folder-open':'fa-folder']"&gt;&lt;/i&gt;<br />　　　　　&lt;!--isFolder判断是否存在子级改变图标--&gt;
         &lt;i v-if='!isFolder' class="fa fa-file-text"&gt;&lt;/i&gt; {{model.data.menuName}}
     &lt;/div&gt;
     &lt;ul v-show="open" v-if='isFolder'&gt;
          &lt;items v-for='cel in model.childTreeNode' :model='cel'&gt;&lt;/items&gt;
     &lt;/ul&gt;<br /> &lt;/li&gt;</pre>

</div>
<p>
官方文档里面写的递归组件强调了使用name属性</p>
<div>
<pre>export default {
    name: 'items',
    props: ['model'],
    components: {},
}</pre>
</div>
<p>
按照vue的思想，不操作Dom树，我们定义两个变量，一个显示隐藏子菜单(open),一个存不存子菜单修改图标(isFolder)。</p>
<div>
<pre>data() {
        return {
             open: false,
             isFolder: true
        }
}</pre>
</div>
<p>
利用vue计算属性动态改变isFolder的值，修改图标，判断存在不子级和子级长度</p>
<div>
<pre>computed: {
    isFolder() {
        return this.model.childTreeNode && this.model.childTreeNode.length
    }
}        </pre>
</div>
<p>
显示隐藏事件</p>
<div>

<pre>methods: {<br />　　toggle: function() {
      if(this.isFolder) {
          this.open = !this.open
      }
　　}<br />}</pre>

</div>
<p>
写到这里我们已经做完一个树形菜单了如下，最终样式就留给大家自己去实现了我在贴出完整代码供大家参考。</p>
<p>
<img src="http://images2015.cnblogs.com/blog/981750/201611/981750-20161117190225857-566273599.png" /></p>
<div>

<pre>&lt;template&gt;
    &lt;li&gt;
        &lt;div @click='toggle'&gt;
            &lt;i v-if='isFolder' class="fa " :class="[open?'fa-folder-open':'fa-folder']"&gt;&lt;/i&gt;
            &lt;!--isFolder判断是否存在子级改变图标--&gt;
            &lt;i v-if='!isFolder' class="fa fa-file-text"&gt;&lt;/i&gt; {{model.data.menuName}}
        &lt;/div&gt;
        &lt;ul v-show="open" v-if='isFolder'&gt;
            &lt;items v-for='cel in model.childTreeNode' :model='cel'&gt;&lt;/items&gt;
        &lt;/ul&gt;
    &lt;/li&gt;
&lt;/template&gt;
&lt;script type="text/javascript"&gt;
    export default {
        name: 'items',
        props: ['model'],
        components: {},
        data() {
            return {
                open: false,
                isFolder: true
            }
        },
        computed: {
            isFolder: function() {
                return this.model.childTreeNode && this.model.childTreeNode.length
            }
        },
        methods: {
            toggle: function() {
                if(this.isFolder) {
                    this.open = !this.open
                }
            },
        }
    }
&lt;/script&gt;</pre>

</div>
<p>
公司最开始是使用easyui做的管理系统，我接手后用vue完整模仿了一些easyui的东西，下面就是在树形菜单基础上模仿出了树形表格，对此感兴趣或者需要的可以联系我。下图为完整图</p>
<p>
<div class="readableLargeImageContainer"><img src="http://images2015.cnblogs.com/blog/981750/201611/981750-20161117191349263-1768555416.png" /></div></p>
<p>渲染什么意思</p>
<p>把高维度信息变成低维度信息，比如把3D场景变成2D的图片。</p>
   

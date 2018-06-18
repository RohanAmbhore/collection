<a href="https://www.jianshu.com/p/2b09156ee5b1">https://www.jianshu.com/p/2b09156ee5b1</a><div id="articleHeader"><h1>基于Hexo搭建博客并部署到Github Pages</h1></div>

        
        <div>
                    <div>
            <a href="/u/4943cb2c6ea4" target="_blank">sunhaiyu</a>
            
            <a target="_blank">关注</a>
            
            <div>
              
                2016.09.22 17:21*
              字数 2027
            阅读 2207评论 4喜欢 7</div>
          
          
        


        
        
          
            <blockquote>
<p>之前在<a href="https://www.jianshu.com/users/4943cb2c6ea4/latest_articles" target="_blank">简书</a>上写东西，觉得自己还是太浮躁。本来打算用Flask自己写一个，以为是微框架就比较简单，naive。HTML、CSS、JS等都要学啊，我几乎没有这方面的基础，写到Web表单那儿果断弃了，转向简单的Hexo + Github Pages。不过要想搭建博客的同时巩固Python，Flask确实是一个不错的选择。</p>
</blockquote>
<h2>获取Github Pages</h2>
<ol>
<li><p>去<a href="https://link.jianshu.com?t=https://github.com/" target="_blank">Github官网</a>注册账号</p></li>
<li>
<p>新建一个repo，<strong>注意名称一定是<code>your_username.github.io</code>这样的格式。</strong></p>
<blockquote>
<p>比如你的用户名为zhangsan，<code>Repository name</code>里面就填上<code>zhangsan.github.io</code></p>
</blockquote>
</li>
<li><p>进入刚新建的仓库，点击<code>Setting</code>，一直拖到最下面，选择<code>Automatic Page Generator</code>，随便选个主题然后发布即可。</p></li>
</ol>
<p>详细步骤见<a href="https://link.jianshu.com?t=http://www.cnblogs.com/purediy/archive/2013/03/07/2948892.html" target="_blank">这个博客</a></p>
<h2>Hexo搭建静态博客</h2>
<p>hexo是一款基于Node.js的静态博客框架，Github官方推荐的是<a href="https://link.jianshu.com?t=https://help.github.com/articles/using-jekyll-with-pages" target="_blank">Jekyll</a>。对比了下，大多认为hexo比较简单，于是我选择了它。我们需要安装如下软件</p>

<h3>配置SSH</h3>
<p>使用Github for windows首次登录时就自动在本地生成了密钥，并远程添加到了Github。自动配置好SSH还是很省事的。</p>
<h3>安装hexo</h3>
<blockquote>
<p>详细步骤见<a href="https://www.jianshu.com/p/35e197cb1273" target="_blank">iHTCboy的简书</a>以及<a href="https://link.jianshu.com?t=http://lovenight.github.io/2015/11/10/Hexo-3-1-1-%E9%9D%99%E6%80%81%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA%E6%8C%87%E5%8D%97/?" target="_blank">岁月如歌的博客</a>。我是跟着他们写的一步步来的，别人说的很详细的我也没必要再重复。我粗略写下来只是为了记录个人学习过程。</p>
</blockquote>
<p>打开Git Shell，cd到你想搭建博客的路径，比如<code>D:\My Documents\GitHub\blog</code>。依次输入</p>
<pre><code>npm install hexo-cli -g  #安装hexo
hexo init                # 初始化，安装所需包
npm install              # 其实此句不是必须，新版本的Hexo在初始化时就安装好了依赖包)
hexo g                   # 生成
hexo s                   # 运行
</code></pre>
<p>然后在浏览器输入<code>localhost:4000</code>就能在本地预览我们新搭建的博客了。hexo的常用指令不多，主要如下</p>
<pre><code>hexo n          # 新建文章，在\source\_posts文件夹里
hexo new page   # 新建页面，比如想在导航栏新增一个“关于我”的页面
hexo clean      # 清除本地的数据库和生成的public文件夹
hexo g          # 生成博客文件
hexo s          # 运行在本地浏览器，可当预览使用
hexo d          # 部署博客到Github等
</code></pre>
<blockquote>
<p><strong>注意所有命令需要在cd后的新路径中进行</strong></p>
</blockquote>

<p>键入<code>hexo n "name"</code>即可在<code>\source\_posts</code>文件夹里生成<code>name.md</code>的Markdown文件，文件结构如下</p>
<blockquote>
<pre><code>---
title: HelloWorld！ # 文章页面上的显示名称，可以任意修改，不会出现在URL中
date: 2015-11-09 15:56:26 # 文章生成时间，一般不改
categories:   # 文章分类目录，参数可省略
    - 随笔 # 此为一级目录
    - 瞬间 # 此为二级目录
    - 关于 # 此为三级目录
tags:   # 文章标签，参数可省略
    - hexo
    - blog # 个数不限，单个可直接跟在tags后面
---
这里开始是正文
</code></pre>
</blockquote>
<p>如果想生成的文件默认带categories，那么打开根目录下<code>\scaffolds\post.md</code>新增一行<code>categories :</code>就修改好了模板文件。如果想在主页中以摘要形式显示你的文章，要么正文中加入``即可屏蔽该语句下面的内容。</p>
<h3>部署到Github Pages</h3>
<p>在根目录下<code>_config.yml</code>里面任意位置新增以下语句</p>
<pre><code>deploy:
  type: git
  # 填上你自己的仓库名，注意后面有`.git`
  repository: git@github.com:your_username/your_username.github.io.git 
  branch: master
</code></pre>
<blockquote>
<ul>
<li>
<p>最好不要采用http形式的如<code>https://github.com/your_username/your_username.github.io.git</code>而采用SSH换版本的<code>git@github.com:your_username/your_username.github.io.git</code>，如下图点击<code>Use SSH</code>后再复制。</p>

</li>
<li><p>所有冒号后面必须键入一个空格</p></li>
</ul>
</blockquote>
<p>好了现在可以部署到Github了。输入<code>npm install hexo-deployer-git --save</code>，然后再执行<code>hexo d</code>来部署。否则会出现<code>Deployer not found:git</code>的错误。耐心等待，出现<code>Deployer done: git</code>表示你部署成功了！输入网址<code>your_username.github.io</code>去看看吧。一般来说如果出现莫名的问题，按照以下步骤即可解决。</p>
<ol>
<li>删除<code>.deploy_git</code>文件夹</li>
<li><code>hexo clean</code></li>
<li><code>hexo g</code></li>
<li><code>hexo d</code></li>
</ol>
<h2>个性化你的博客</h2>

<p>在根目录<code>_config.yml</code>里进行全局配置。</p>
<pre><code># Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: 海之声 #主页标题
subtitle: 参差多态乃是幸福本源 #副标题
description: 参差多态乃是幸福本源 # 网站描述，可以加一句自己喜欢的座右铭
author: haiyusun #作者，左下角显示
avatar: /images/avatar.jpg #设置头像，放在\themes\next\source\images里
language: zh-Hans # 选择中文简体
timezone:
since: 2016 #建站日期，左下角显示

# 多说 ShortName
duoshuo_shortname: your_username # 多说评论，后面填写用户名
# 百度分析
baidu_analytics: your_id # 填写自己获得的id

# Social links
social:
  Github: https://github.com/haiyusun
  Email: mailto:haiyu19931121@163.com

# title, chinese available
links_title: 友情链接
# links
links:
  我的简书: http://www.jianshu.com/users/4943cb2c6ea4

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://haiyusun.github.io/ #填自己的github pages网址
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
# 本地搜索
search:
  path: search.xml
  field: post

# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:

# Writing
new_post_name: :title.md # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
future: true
# 语法高亮
highlight:
  enable: true
  line_number: true
  auto_detect: true
  tab_replace:

# Category & Tag
default_category: uncategorized
category_map:
tag_map:

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
# 百度网站地图
plugins:
baidusitemap: # 需要安装插件 npm install hexo-generator-baidu-sitemap@0.1.1 --save
  path: baidusitemap.xml

# 主题切换
theme: next
# RSS订阅
feed:
  type: atom
  path: atom.xml
  limit: 0

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
    type: git
    repo: git@github.com:your-username/haiyusun.github.io.git
    branch: master

# ---------------下面选项需要对应插件的支持---------------
# npm install hexo-generator-index --save
# npm install hexo-generator-archive --save
# npm install hexo-generator-category --save
# npm install hexo-generator-tag --save

index_generator:
  per_page: 10 ##首页默认10篇文章标题 如果值为0不分页

archive_generator:
  per_page: 20 ##归档页面默认20篇文章标题
  yearly: true  ##生成年视图
  monthly: true ##生成月视图

tag_generator:
  per_page: 10 ##标签分类页面默认10篇文章

category_generator:
  per_page: 10 ###分类页面默认10篇文章
</code></pre>

<p>自带的landscape主题不太好看，我选了<a href="https://link.jianshu.com?t=https://github.com/iissnan/hexo-theme-next" target="_blank">NexT</a>。将其克隆到本地，在根目录下<code>theme</code>文件夹下新建<code>next</code>文件夹，把刚才下载的全放进去，然后在根目录<code>_config.yml</code>里找到<code>theme: landscape</code>将其替换成<code>next</code>即启用该主题。官方给出的<a href="https://link.jianshu.com?t=http://theme-next.iissnan.com/getting-started.html" target="_blank">NexT主题使用教程</a>十分详细，建议先看看，配合着<a href="https://link.jianshu.com?t=http://lovenight.github.io/2015/11/10/Hexo-3-1-1-%E9%9D%99%E6%80%81%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA%E6%8C%87%E5%8D%97/?" target="_blank">岁月如歌的博客</a>应该能做出效果不错的个人博客了。至此我们的博客就带有RSS订阅、百度统计、来访/阅读次数统计、网站地图、评论系统、分享服务、本地搜索等功能了。</p>
<p>以下针对我自己的问题作个记录。</p>


<p>默认导航栏只有首页、归档、标签、分类四项。如果想增加其他如C++、随笔等。需要打开<code>\themes\next\_config.yml</code>找到如下</p>
<pre><code># When running the site in a subdirectory (e.g. domain.tld/blog), remove the leading slash (/archives -&gt; archives)
menu:
  home: /
  categories: /categories
  tags: /tags
  archives: /archives
  # 这里是新增的，程序猿是一级目录，C是二级目录，同理随笔是一级目录
  c++: /categories/程序猿/C/
  python: /categories/程序猿/Python/
  essay: /categories/随笔/
  # 注意这里没有/categories
  about: /about
</code></pre>
<p>假如我想新建C++、Python、随笔三个导航按钮，并且打开他们的效果如下图。</p>

<p>需要注意的是前面要加上<code>/categories</code>，格式是这样<code>python: /categories/这里是文章的一级目录/这里是文章的二级目录/</code>。结尾要加上<code>/</code>分隔符。<strong>这几个页面是不需要通过<code>hexo new page</code>来生成的。</strong>关于导航栏及侧栏所用的图标来自<a href="https://link.jianshu.com?t=http://fontawesome.io/" target="_blank">fontawesome</a>。在<code>\themes\next\_config.yml</code>里配置。</p>
<pre><code># 导航栏的图标，输入网站内图标的对应单词
menu_icons:
  enable: true
  #KeyMapsToMenuItemKey: NameOfTheIconFromFontAwesome
  home: home
  about: user
  categories: th
  tags: tags
  archives: archive
  c++: keyboard-o
  python: keyboard-o
  essay: pencil
  commonweal: heartbeat
  # 社交网络图标
  social_icons:
  enable: true
  # Icon Mappings.
  # KeyMapsToSocalItemKey: NameOfTheIconFromFontAwesome
  GitHub: github
  Email: envelope
</code></pre>
<p>写文章的时候只要分类目录对应就可以被正确归类到导航栏里。如下</p>
<pre><code>---
title: Python爬虫初学（三）—— 模拟登录知乎
date: 2016-09-18 17:10:59
# 对应于/categories/程序猿/Python/
categories:
    - 程序猿
    - Python
tags:
    - Python
    - 爬虫
---
</code></pre>
<h4>新增关于我页面</h4>
<p>这个需要<code>hexo new page "about"</code>生成一个新页面，<code>menu</code>里面新增<code>about: /about</code>。在新增的<code>about</code>文件夹可以看到<code>index.md</code>，对其直接编辑就可，注意不要对此文件加<code>tags</code>和 <code>categories</code>，否则会出错。</p>
<h3>公益404页面</h3>
<blockquote>
<p><strong>HTTP 404</strong>或<strong>Not Found</strong>错误信息是<a href="https://link.jianshu.com?t=http://baike.baidu.com/view/9472.htm" target="_blank">HTTP</a>的其中一种“标准回应信息”（<a href="https://link.jianshu.com?t=http://baike.baidu.com/view/1790469.htm" target="_blank">HTTP状态码</a>），此信息代表客户端在浏览网页时，<a href="https://link.jianshu.com?t=http://baike.baidu.com/view/899.htm" target="_blank">服务器</a>无法正常提供信息，或是服务器无法回应且不知原因。</p>
</blockquote>
<p>按照<a href="https://link.jianshu.com?t=http://theme-next.iissnan.com/theme-settings.html#volunteer-404" target="_blank">NexT主题使用教程</a>添加404页面对我来说好像不可用。在<a href="https://link.jianshu.com?t=https://www.zhihu.com/question/21650209" target="_blank">知乎的这个回答中</a>复制了某匿名用户的的代码，拷贝到<code>\themes\next\source\404.html</code>可行。代码如下，其中重定向链接改成你自己的主页，还可以自定义背景图片。</p>
<pre><code>&lt;html&gt;
&lt;head&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;title&gt;404 Not Found&lt;/title&gt;
    &lt;style&gt;
        *{margin:0;padding:0;outline:none;font-family:\5FAE\8F6F\96C5\9ED1,ו;-webkit-user-select:none;-moz-user-select:none;-ms-user-select:none;-khtml-user-select:none;user-select:none;cursor:default;font-weight:lighter;}
        .center{margin:0 auto;}
        .whole{width:100%;height:100%;line-height:100%;position:fixed;bottom:0;left:0;z-index:-1000;overflow:hidden;}
        .whole img{width:100%;height:100%;}
        .mask{width:100%;height:100%;position:absolute;top:0;left:0;background:#000;opacity:0.6;filter:alpha(opacity=60);}
        .b{width:100%;text-align:center;height:400px;position:absolute;top:50%;margin-top:-230px}.a{width:150px;height:50px;margin-top:30px}.a a{display:block;float:left;width:150px;height:50px;background:#fff;text-align:center;line-height:50px;font-size:18px;border-radius:25px;color:#333}.a a:hover{color:#000;box-shadow:#fff 0 0 20px}
        p{color:#fff;margin-top:40px;font-size:24px;}
        #num{margin:0 5px;font-weight:bold;}
        .plan{color: black;background: white;font-size: 30px; margin-top: 20px;}
        .plan:hover{color: white;background: black;font-size: 30px;}

            #gg {
               position: absolute;
    width: 654px;
    height: 470px;
    left: 50%;
    top: 50%;
    margin-left: -377px;
    margin-top: -235px;
        }
    &lt;/style&gt;
&lt;/head&gt;
&lt;body onload="redirect();"&gt;
      &lt;div id="gg"&gt;
        &lt;!--以下网址为益播生成的404页面--&gt;
       &lt;iframe   class="gg" scrolling='no' frameborder='0' src='https://yibo.iyiyun.com/Home/Distribute/ad404/1182245' width='654' height='470' style='display:block;'&gt;
    &lt;/iframe&gt;
    &lt;/div&gt;
&lt;div class="whole"&gt;
  &lt;!--这里是自定义图片的地址--&gt;
    ![](http://upload-images.jianshu.io/upload_images/2726327-4ae4ff22fb6c19da.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>


<h2>继续美化博客</h2>
<h3>修改文章宽度</h3>
<p>如果嫌博客页面两边大量留白，文章宽度不够，可以修改。见<a href="https://link.jianshu.com?t=https://www.zhihu.com/question/24422335" target="_blank">知乎-高爷的回答</a>。</p>
<blockquote>
<p>如何修改文章宽度？</p>
<ol>
<li>\themes\next\source\css_common\components\post\post-expand.styl</li>
</ol>
<p>@media (max-width: 767px)<br />
改为：<br />
@media (max-width: 1280px)</p>
<ol>
<li>\themes\next\source\css\ _variables\base.styl中：</li>
</ol>
<p>$main-desktop = 960px<br />
$content-desktop = 700px<br />
改成：<br />
$main-desktop = 1280px<br />
$content-desktop = 960px</p>
</blockquote>
<p>我个人觉得这个又太宽了。于是改成<code>@media (max-width: 1080px)</code>、<code>$main-desktop = 1080px</code>、<br />
<code>$content-desktop = 810px</code>，可凭喜好自己修改。我设置的文章宽度如下</p>

<h3>配色与字体</h3>
<p>继续在<code>\themes\next\source\css\ _variables\base.styl</code>折腾。</p>
<h4>字号与行高</h4>
<p>字号默认14px，虽然是主流，我个人觉得还是太小了点，看多了眼睛难受，设置成16px好多了。<br />
找到<code>$font-size-base = 14px</code>，修改即可。该主题默认行高2.0，移动设备访问可见行高过高，找到<code>$line-height-base = 2</code>。修改成1.8个人觉得最为合适。至于代码块的字体，默认的13px确实有点小了。不过最好不要修改，否则会出现糟糕的滚动条。</p>

<p>主要是修改网页背景色，修改超链接颜色。自定义颜色见<a href="https://link.jianshu.com?t=http://www.114la.com/other/rgb.htm" target="_blank">颜色表</a>。</p>
<pre><code>//
// Variables
// =================================================
// Colors
// colors for use across theme.
// --------------------------------------------------
$whitesmoke   = #f5f5f5
$gainsboro    = #eee
$mycolor     = #EEE5DE
$gray-lighter = #ddd
$grey-light   = #ccc
$grey         = #bbb
$grey-dark    = #999
$grey-dim     = #666
$black-light  = #555
$black-dim    = #333
$black-deep   = #222
$red          = #ff2a2a
$blue-bright  = #87daff
$blue         = #0684bd
// 这是我自定义的颜色
$myblue    = #4682B4   
$blue-deep    = #262a30
$orange       = #fc6423
$mylink      = #36648B

// Scaffolding
// Settings for some of the most global styles.
// --------------------------------------------------
// Global text color on &lt;body&gt;
$text-color                   = $black-deep
// 修改超链接颜色
// Global link color.
$link-color                   = $myblue
$link-hover-color             = $mylink
$link-decoration-color        = $gray-lighter 
$link-decoration-hover-color  = $mylink

// Global border color.
$border-color                 = $black-light

// Background color for &lt;body&gt;
// 背景色，默认white，我认为太刺眼就换成了烟灰色
$body-bg-color                = whitesmoke
// 鼠标选择区域
// Selection
$selection-bg                 = $blue-deep
$selection-color              = white
</code></pre>
<p>我就折腾了这么多，至此博客搭建完成。</p>
<hr />
<p>by @sunhaiyu</p>
<p>2016.9.22</p>

          
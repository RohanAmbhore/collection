<a href="http://blog.csdn.net/lxcao/article/details/52809939">http://blog.csdn.net/lxcao/article/details/52809939</a><div id="articleHeader"><h1>Web前端面试指导(四十三)：请描述一下 cookies，sessionStorage 和 localStorage 的区别？</h1></div>
        
        
                            
                        

这是一种对比性比较强的问题，可以先说他们的相同点，然后就是要详细阐述他们的不同点，而不同点不要刻意去对比，只要说出各自的特点，自然他们的不同点就出来了。<br />
解决方法<br />
<strong>相同点：</strong>都存储在客户端<br />
<strong>不同点：</strong><blockquote>1.存储大小</blockquote>
<blockquote>

<ul>
<li>cookie数据大小不能超过4k。</li><li>sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。</li></ul>
</blockquote>
<blockquote>2.有效时间</blockquote>
<blockquote>

<ul>
<li>localStorage    存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；</li><li>sessionStorage  数据在当前浏览器窗口关闭后自动删除。</li><li>cookie          设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭</li></ul>

</blockquote>
<blockquote>3. 数据与服务器之间的交互方式</blockquote>
<blockquote>

<ul>
<li>cookie的数据会自动的传递到服务器，服务器端也可以写cookie到客户端</li><li>sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。</li></ul>
</blockquote>
<p><strong>----------------------------------------------------------------------------------------------------------------------------------------</strong></p>
<p><strong>额外拓展【加分项】：</strong>Cookie的操作（有点小难度）防止面试官细问cookie的操作。</p>
<p><strong>设置Cookie </strong></p>
<blockquote>
<p><strong>cookie的几个要素</strong></p>
<p>cookie的内容：采用 key=value;key=value……存储，参数名自定义</p>
<p>cookie的过期时间：使用参数expires</p>
<p>cookie的路径：使用参数path，"/"表示这个网站的页面，不推荐!容易产生冲突</p>
<p><strong>注意：</strong>形如“/pro/index.html”路径，在google浏览器正常，在IE浏览器得不到值 </p>
</blockquote>
<blockquote>
<p><strong>cookie的表示方式示例</strong></p>
<div><ol><li>var name = "jack";  </li><li>var pwd = "123";  </li><li>var now = new Date();  </li><li>now.setTime(now.getTime() +1 * 24 * 60 * 60 * 1000);//转毫秒  </li><li>var path = "/";//可以是具体的网页  </li><li>document.cookie = "name=" + name + ";expires=" + now.toUTCString() + ";path=" + path;//姓名  </li><li>document.cookie= "pwd=" + pwd + ";expires=" + now.toUTCString()+ ";path=" + path; //密码  </li></ol></div><pre>var name = "jack";
var pwd = "123";
var now = new Date();
now.setTime(now.getTime() +1 * 24 * 60 * 60 * 1000);//转毫秒
var path = "/";//可以是具体的网页
document.cookie = "name=" + name + ";expires=" + now.toUTCString() + ";path=" + path;//姓名
document.cookie= "pwd=" + pwd + ";expires=" + now.toUTCString()+ ";path=" + path; //密码</pre>
</blockquote>
<p><strong>读取cookie</strong></p>
<blockquote>
<p>获取cookie内容</p>
<div><ol><li>vardata=document.cookie;//获取对应页面的cookie  </li></ol></div><pre>vardata=document.cookie;//获取对应页面的cookie</pre>
<p>解析cookie</p>
<p>方式1：截取字符串</p>
<div><ol><li>function getKey(key) {  </li><li>    var data = document.cookie;  </li><li>    var findStr = key + "=";  </li><li>    //找到key的位置  </li><li>    var index = data.indexOf(findStr);  </li><li>    if (index == -1)  </li><li>        return null;  </li><li>    var subStr = data.substring(index +findStr.length);  </li><li>    var lastIndex = subStr.indexOf(";");  </li><li>    if (lastIndex == -1) {  </li><li>        return subStr;  </li><li> } else {  </li><li>        return subStr.substring(0,lastIndex);  </li></ol></div><pre>function getKey(key) {
    var data = document.cookie;
    var findStr = key + "=";
    //找到key的位置
    var index = data.indexOf(findStr);
    if (index == -1)
        return null;
    var subStr = data.substring(index +findStr.length);
    var lastIndex = subStr.indexOf(";");
    if (lastIndex == -1) {
        return subStr;
 } else {
        return subStr.substring(0,lastIndex);
 }
}</pre>
<p>方式2：使用正则表达式+JSON</p>
<div><ol><li>function getKey(key) {  </li><li>    return JSON.parse("{\"" +document.cookie.replace(/;\s+/gim, "\",\"").replace(/=/gim, "\":\"") + "\"}")[key];  </li></ol></div><pre>function getKey(key) {
    return JSON.parse("{\"" +document.cookie.replace(/;\s+/gim, "\",\"").replace(/=/gim, "\":\"") + "\"}")[key];
}</pre></blockquote>
<p><strong>清除cookie</strong></p>
<blockquote><div><ol><li>var name = null;  </li><li>var pwd = null;  </li><li>var now = new Date();  </li><li>var path = "/";//可以是具体的网页  </li><li>document.cookie= "name=" + name + ";expires=" + now.toUTCString()+ ";path=" + path;//姓名  </li><li>document.cookie = "pwd=" + pwd + ";expires=" + now.toUTCString()+ ";path=" + path; //密码  </li></ol></div><pre>var name = null;
var pwd = null;
var now = new Date();
var path = "/";//可以是具体的网页
document.cookie= "name=" + name + ";expires=" + now.toUTCString()+ ";path=" + path;//姓名
document.cookie = "pwd=" + pwd + ";expires=" + now.toUTCString()+ ";path=" + path; //密码</pre>
</blockquote>
                
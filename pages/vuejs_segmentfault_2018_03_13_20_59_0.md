<a href="https://segmentfault.com/q/1010000006938552/a-1020000006939230">https://segmentfault.com/q/1010000006938552/a-1020000006939230</a><div id="articleHeader"><h1>为什么vuejs无法检测到下列数组变化 - 挺问中原的回答 - SegmentFault 思否</h1></div>
                <article>
                    

                    <div>
                        <div>
                                                            
<p>在vuejs官方文档中看到：</p>
<p>因为 JavaScript 的限制，<strong>Vue.js</strong> 不能检测到下面数组变化：</p>

<p>据说vuejs是遍历对象的所有属性和方法加上钩子，为什么无法检测到上面这两种变化。</p>

                            
                        </div>


                                                                                                                        
                        
                        


                        
                    </div>
                    
                </article>

                                
                
                    
                <h2>
            <a href="/q/1010000006938552" target="_blank">查看全部 2 个回答</a>
        </h2>
                
    
            


    
        

        
            
                                    
<p>是这样的，你console.log一下跟vue绑在一起的<em>data里面属性</em>，你会发现那些打印出来多了两个东西：</p>
<ul>
<li><p>setter</p></li>
<li><p>getter</p></li>
</ul>
<p>没错，vue检测数组变动靠的就是这两个属性<br />而这两个属性，根据vue文档的说法，它是使用了js原生的<code>Object.defineProperty()</code>（其实准确来讲应该是es的东西）<br />简单地讲，就是js属性的属性。。。怎么那么别扭。。。就是描述Array或者Json等Object类型里面的值的属性，比如一个<code>arr=[1,2,3,4]</code>,属性的属性就是里面的1具有的属性。。。而且还有两个：数据属性和访问器属性。<br />比如数据属性中的 Enumberable,如果它为false，那么即使它描述的那个属性存在于json里面，也不会被for-in遍历到。</p>
<p>好，回到正题，也就是vue对数组的检测方法<br />它使用是Object类型底层的访问器属性来检测数组变动的。<br />访问器属性存在两个方法（姑且叫做方法吧，原文是叫attribute，但翻译成属性的话感觉太乱了。。而它们的作用又如同面向对象里面的方法一样）</p>
<ul>
<li><p>Get ：在读取时调用的函数。默认值为undefined</p></li>
<li><p>Set ：在写入时调用的函数，默认值为undefined</p></li>
</ul>
<p>Vue的数组检测变动就基于上面这两个方法。<br />然而，都说了是es底层定义的东西，js是不可能直接就修改访问上面的Get和Set，必须通过Object.defineProperty这个方法进行修改：</p>
<pre><code>    var json={
        a:1
    };
    /*当json.a变动时打印修改信息*/
    Object.defineProperty(json,'a',{
        set:function(newValue){
            console.log(this.value+'-&gt;'+newValue)
        },
        get:function(){
            console.log(this.value)
        }
    })</code></pre>
<p>据说，第一个实现Object.defineProperty方法的浏览器是IE8，想不到吧，渣渣IE居然是第一个实现的。。。这也是为什么vuejs不支持ie8以下的垃圾ie了的原因了。</p>
<p>而且，vue为了检测push这些操作造成的数组变动，都是将这些Api重新封装了一遍的。。。<br />所以当你直接 <code>vm.items[0]={}</code>这样的时候，vue根本没法给你做一个Object.defineProperty处理，自然也搞不出setter和getter，自然无法检测数组变动。。。</p>
<p>=========2016年9月19日15:51:17 补充==========<br />首先更正我的一个错误，就是之前我说console.log跟vue绑定的数组，但是我自己试了一下发现是json才存在getter和setter，数组里面没有setter和getter。只有一个__ob__，看了一下1.026的源码，vue封装的数组方法都在里面。<br />那这个setter和getter是什么时候生成的，文档里说了，是在实例初始化的时候。当然你使用vue数组方法进行数组修改的时候，也会触发这个<code>Object.defineProperty</code>的访问器属性。<br />所以按照文档说的，用<code>$set</code>这个方法代替索引赋值，<code>$remove</code>方法清空数组</p>

                            
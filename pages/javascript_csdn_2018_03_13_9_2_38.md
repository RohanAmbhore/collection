<a href="http://blog.csdn.net/sinat_25127047/article/details/51605009">http://blog.csdn.net/sinat_25127047/article/details/51605009</a><div id="articleHeader"><h1>                                    <a href="http://blog.csdn.net/sinat_25127047/article/details/51605009" target="_blank">                                                     [置顶]                                                                        javascript理解之变量作用域与闭包                    </a>                            </h1></div>
        <div>
        
        <div>
        2016年06月12日 17:33:11
        1466人阅读
         <a href="javascript:void(0);" target="_blank">评论</a>(2)
        
            <a href="javascript:void(0);" title="收藏" target="_blank">收藏</a>
        
                
            <a href="javascript:void(0);" title="举报" target="_blank">举报</a>
        
                    </div>


                
                <div>
                        <p>
                版权声明：本文为博主原创文章，未经博主允许不得转载。                http://blog.csdn.net/sinat_25127047/article/details/51605009            </p>
                    </div>
        
                    
                

<p>闭包是指能够访问自由变量的函数 (变量在本地使用，但在闭包中定义)。换句话说，定义在闭包中的函数可以“记忆”它被创建时候的环境。</p>



<h2 id="函数作用域与声明提前">函数作用域与声明提前</h2>



<pre><code>var scope= "global scope";
function f(){
  console.log(scope); //undefined，并没有出现"global scope"
  var scope="local scope";
  console.log(scope);//local scope
}</code></pre>

<p>为什么会这样呢？ <br />
Javascript的函数作用域是指在函数内声明的所有变量在函数体内始终是可见的，这个特性也被叫做“提前声明”。 <br />
即Javascript函数里所有声明的变量（但不涉及赋值）都被提前至函数体的顶部。 <br />
上面的代码类似于</p>



<pre><code>var scope= "global scope";
function f(){
  var scope;
  console.log(scope); 
  scope="local scope";
  console.log(scope);
}</code></pre>





<p>首先，每一段代码（全局代码或函数）都有一个与之关联的作用域链（scope chain），这个作用域链可以是一个对象列表或者链表，这组对象定义了这段代码“作用域中”的变量。 <br />
当javscript需要查找变量x的值时候（变量解析（variable resolution）），它会从链中的第一个对象开始查找，如果这个对象有名为x的属性，就会使用这个x的值；否则，找链中的下一个对象；以此类推，直到最顶端，如果仍然没有找到，就抛出引用错误（ReferenceError）异常。</p>

<p>在Javascript的最顶层代码，作用域链由一个全局对象组成。 <br />
在不包含嵌套的函数体内，作用域链上有两个对象：第一个是定义的函数参数(lenth, caller, arguments… )和局部变量的对象；第二个是全局对象。 <div class="readableLargeImageContainer"><img src="http://img.blog.csdn.net/20160612172612049" alt="这里写图片描述" /></div>
在一个嵌套的函数体内，作用域链上至少有三个对象。 <div class="readableLargeImageContainer"><img src="http://img.blog.csdn.net/20160612172924037" alt="这里写图片描述" /></div>
对于嵌套函数而言，每次调用外部函数，内部函数又会重新定义一遍。 <br />
因为虽然。内部函数的代码不同，但是作用域链发生了变化。</p>





<p>各种专业文献上的”闭包”（closure）定义非常抽象，很难看懂。我的理解是，闭包就是能够读取其他函数内部变量的函数。 <br />
由于在Javascript语言中，只有函数内部的子函数才能读取局部变量，因此可以把闭包简单理解成”定义在一个函数内部的函数”。 <br />
所以，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。</p>



<h3 id="用途一外部函数可以读取内部函数的变量">用途一：外部函数可以读取内部函数的变量</h3>



<pre><code>　　function f1(){
　　　　var n=999;
　　　　function f2(){
　　　　　　alert(n); 
　　　　}
　　　　return f2;
　　}
　　var result=f1();
　　result(); // 999</code></pre>

<p>这里外部函数可以读取f1()中的n，是因为内部函数f2()可以读取f1的局部变量，通过返回f2，f2的作用域链有n，因此可以获取n的值。 <br />
我的理解： <div class="readableLargeImageContainer"><img src="http://img.blog.csdn.net/20160613102605082" alt="这里写图片描述" /></div></p>



<h3 id="用途二使内部函数的变量一直在内存中">用途二：使内部函数的变量一直在内存中</h3>



<pre><code>var uniqueInteger = (function() {
    var counter = 0;
    return function() {
        return counter++;
    }
}());</code></pre>

<p><div class="readableLargeImageContainer"><img src="http://img.blog.csdn.net/20160613101541260" alt="这里写图片描述" /></div></p>



<h2 id="实用的闭包">实用的闭包</h2>

<p>一般说来，可以使用只有一个方法的对象的地方，都可以使用闭包。</p>



<pre><code>var makeCounter = function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  }  
};

var Counter1 = makeCounter();
var Counter2 = makeCounter();
console.log(Counter1.value()); /* logs 0 */
Counter1.increment();
Counter1.increment();
console.log(Counter1.value()); /* logs 2 */
Counter1.decrement();
console.log(Counter1.value()); /* logs 1 */
console.log(Counter2.value()); /* logs 0 */</code></pre>

<p>在一个Counter里面，increment，decrement，value共享作用域环境，即可以访问同一个privateCounter和changeBy()，这样就可以实现一个简单的技术器。 <br />
这也是闭包内存共享的一个优点。 <br />
而Counter1和Counter2 的创建环境不一样，作用域链也不同，访问的privateCounter和changeBy()在不同的内存地址。 <br />
每次调用 makeCounter() 函数期间，其环境是不同的。每次调用中， privateCounter 中含有不同的实例。</p>



<h2 id="在循环中创建闭包一个常见错误">在循环中创建闭包：一个常见错误</h2>



<pre><code>&lt;p id="help"&gt;Helpful notes will appear here&lt;/p&gt;
&lt;p&gt;E-mail: &lt;input type="text" id="email" name="email"&gt;&lt;/p&gt;
&lt;p&gt;Name: &lt;input type="text" id="name" name="name"&gt;&lt;/p&gt;
&lt;p&gt;Age: &lt;input type="text" id="age" name="age"&gt;&lt;/p&gt;</code></pre>



<pre><code>function showHelp(help) {
  document.getElementById('help').innerHTML = help;
}

function setupHelp() {
  var helpText = [
      {'id': 'email', 'help': 'Your e-mail address'},
      {'id': 'name', 'help': 'Your full name'},
      {'id': 'age', 'help': 'Your age (you must be over 16)'}
    ];

  for (var i = 0; i &lt; helpText.length; i++) {
    var item = helpText[i];
    document.getElementById(item.id).onfocus = function() {
      showHelp(item.help);
    }
  }

}

setupHelp(); ////每次都停留在'Your age (you must be over 16)'</code></pre>



<pre><code>    //我们想要的效果
    document.getElementById(helpText[0].id).onfocus = function() {
        showHelp(helpText[0].help);
    };
    document.getElementById(helpText[1].id).onfocus = function() {
        showHelp(helpText[1].help);
    };
    document.getElementById(helpText[2].id).onfocus = function() {
        showHelp(helpText[2].help);
    };
    //实际效果
    document.getElementById(helpText[0].id).onfocus = function() {
        showHelp(helpText[2].help);
    };
    document.getElementById(helpText[1].id).onfocus = function() {
        showHelp(helpText[2].help);
    };
    document.getElementById(helpText[2].id).onfocus = function() {
        showHelp(helpText[2].help);
    };</code></pre>

<p>该问题的原因在于赋给 onfocus 是闭包（setupHelp）中的匿名函数而不是闭包对象；在闭包（setupHelp）中一共创建了三个匿名函数（这里指的匿名函数是说的getElenmentById(..).onfocus() =fucntion (){…}） <br />
但是它们都<strong>共享同一个环境（item）</strong>。在 <strong>onfocus 的回调被执行时，循环早已经完成</strong>，且此时 item 变量（由所有三个闭包所共享）已经指向了 helpText 列表中的最后一项。</p>

<p>理解：执行setupHelp()函数创建函数环境，调用getElenmentById(..).onfocus()的时候实质上都是对同一环境中的item进行修改。 <br />
在初始化环境的时候，showHelp（helpText[2].help）就已经执行完毕了。 <br />
三次循环先执行结束，实际上在执行onfocus() 的时候，传入showHelp的都是都是对 helpText[2].help了。</p>

<p>解决这个问题的一种方案是使onfocus指向一个新的闭包对象。</p>



<pre><code>function showHelp(help) {
  document.getElementById('help').innerHTML = help;
}

function makeHelpCallback(help) {
  return function() {
    showHelp(help);
  };
}

function setupHelp() {
  var helpText = [
      {'id': 'email', 'help': 'Your e-mail address'},
      {'id': 'name', 'help': 'Your full name'},
      {'id': 'age', 'help': 'Your age (you must be over 16)'}
    ];

  for (var i = 0; i &lt; helpText.length; i++) {
    var item = helpText[i];
    document.getElementById(item.id).onfocus = makeHelpCallback(item.help);
  }
}

setupHelp();</code></pre>



<h2 id="最后使用闭包要慎重的">最后，使用闭包要慎重的</h2>

<p>因为涉及到占用内存，因为每次生成一个函数对象就会在内存中开辟一定的空间来存储它的环境，因此，适当的使用闭包。</p>



<pre><code>function MyObject(name, message) {
  this.name = name.toString();
  this.message = message.toString();
  this.getName = function() {
    return this.name;
  };

  this.getMessage = function() {
    return this.message;
  };
}
var newobj1=MyObject('x','hello');
var newobj2=MyObject('y','javascript');
newobj1.getName()==newobj2.getName();//false</code></pre>

<p>这样写的坏处就是，每次构造MyObject的时候都会为getName()和getMessage()划分新的内存，这样是很不划算的。 <br />
而把他写成下面的形式就好了。 <br />
因为原型中的方法指向同一片内存（突然在想可不可以把prototype理解为指针，它指向的区域放了原型函数以及用户定义的原型函数）</p>

<pre><code>function MyObject(name, message) {
  this.name = name.toString();
  this.message = message.toString();
}
MyObject.prototype = {
  getName: function() {
    return this.name;
  },
  getMessage: function() {
    return this.message;
  }
};
var newobj1=MyObject('x','hello');
var newobj2=MyObject('y','javascript');
newobj1.getName()==newobj2.getName();//true</code></pre>

<hr />

<p>这篇文章参考了《javascript权威指南》 <br />
以及<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures" target="_blank">https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures</a> <br />
以及<a href="http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html" target="_blank">http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html</a> <br />
务必把闭包弄清楚</p>            
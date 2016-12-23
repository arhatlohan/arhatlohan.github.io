---
title: JavaScript DOM 编程艺术：DOM
date: 2016-12-21 15:30:46
tags: [笔记, JavaScript]
---


### 文档：DOM中的“D”
如果没有document（文档），DOM也就无从谈起。当创建了一个网页并把它加载到Web浏览器时，DOM就在幕后悄然而生。它把你编写的网页文档转换为一个文档对象。

### 对象：DOM中的“O”
与某个特定对象相关联的变量被称为这个对象的属性，只能通过某个特定对象去调用的函数被称为这个对象的方法。

JavaScript语言里的对象可以分为三种类型：
+ 用户定义对象（user-defined object）:由程序员自行创建的对象。
+ 内建对象（native object）：内建在JavaScript语言里的对象。
+ 宿主对象（host object）：由浏览器提供的对象。

即使在JavaScript的最初版本里，对编写脚本来说非常重要的一些宿主对象就已经可用了，它们当中最基础的对象是window对象。
window对象对应着浏览器窗口本身，这个对象的属性和方法通常统称为BOM（浏览器对象模型），但我觉得称为Window Object Model（窗口对象模型）更为贴切。BOM提供了`window.open`和`window.blur`等方法，这些方法某种程度上要为到处被滥用的各种弹出窗口和下拉菜单负责。
document对象的主要功能就是处理网页内容。

### 模型：DOM中的“M”
DOM中的M代表着“Model”（模型），但说它代表着“Map”（地图）也未尝不可。
浏览器提供了网页的地图（或者说模型），而我们可以通过JavaScript去读这张地图。

### 节点 node
节点（node）表示网络中的一个连接点，一个网络就是由一些节点构成的集合。
+ 元素节点（element node）
  文本段落元素的名字是`p`，无序清单元素的名字是`ul`，列表项元素的名字是`li`。
+ 文本节点（text node）
  文本节点总是被包含在元素节点内部。
+ 属性节点（attribute node)
  属性节点用来对元素做出更具体的描述。

例如：
```JavaScript
<p title="a gentle reminder">Don't forget to buy this stuff.</p>
```
在上面DOM中，`title="a gentle reminder"`是一个属性节点，`p`是一个元素节点，`Don't forget to buy this stuff.`是文本节点。
如图：
![节点](/sourcepictures/20161221/node.jpg)


**CSS**
DOM并不是与网页结构打交道的唯一技术。我们还可以使用CSS（层叠样式表）告诉浏览器应该如何显示一份文档的内容。

### 获取元素
获取元素的方法主要有：getElementById()、getElementsByTagName()、getElementsByClassName()、getElementsByName()、
#### getElementById
返回对拥有指定ID的第一个对象的引用。
JavaScript区分大小写。
它是document对象特有的函数。在脚本代码里，函数名的后面必须跟有一对圆括号，这对圆括号包含着函数的参数。`getElementById`方法只有一个参数：你想获得的那个元素的id属性的值，这个id值必须放在单引号或双引号里。
`document.getElementById(id)`
e.g:
```JavaScript
document.getElementById("purchases")
```
#### getElementsByTagName
返回带有指定标签名的对象的集合。这个方法只有一个参数，它的参数是标签的名字：
`element.getElementsByTagName(tag)`
注意，它返回的是一个**数组**。
e.g:
```javascript
document.getElementsByTagName("li")
```
getElementsByTagName允许把一个通配符作为它的参数，而这意味着文档里的每个元素都将在这个函数所返回的数组里占有一席之地。通配符必须放在引号里，这是为了让通配符和乘法操作符有所区别。如果你想知道某份文档里总共有多少元素节点，代码如下：
```javascript
document.getElementsByTagName("*").length
```
e.g:
```javascript
var shopping = document.getElementById("purchase");
var items = document.getElementsByTagName("*");
```
#### getElementsByClassName
返回文档中所有指定类名的元素集合。其只接受一个参数，就是类名：
`getElementsByClassName(class)`
其返回结果为数组。
使用这个方法还可以查找那些带有多个类名的元素。要指定多个类名，只要在字符串参数中用空格分割类名即可。eg：
```javascript
document.getElementsByClassName("important sale")
```
上述代码将会匹配同时带有“important”和“sale”的对象。
一些老版本的浏览器不支持getElementsByClassName,可以使用以下代码：
```JavaScript
function getElementsByClassName(node, classname){
  if (node.getElementsByClassName){
    //使用现有方法
    return node.getElementsByClassName(classname);
  }
  else{
    var results = new Array();
    var elems = node.getElementByTagName("*");
    for(var i=0; i<elems.length; i++){
      if(elems[i].className.indexOf(classname) != -1){
        results[results.length] = elems[i];
      }
    }
  return results;
  }
}

```

#### getElementsByName
该方法与getElementById()方法相类似，但是它查询的是元素的`name`属性，而不是`id`属性。
因为一个文档中的name属性可能不唯一，所以它返回的方法是元素的数组，而不是一个元素。

#### getElementsByTagNameNS(ns,name)
返回带有指定名称和命名空间的所有元素的一个节点列表。
该方法与 getElementsByTagName() 方法相似，只是它根据命名空间和名称来检索元素。只有使用命名空间的 XML 文档才会使用它。
参数：
+ ns，字符串值，规定需要检索的命名空间名称。
+ name, 字符串值，规定要检索的标签名。


---
### 获取和设置属性
我们已经知道获取元素的方法：getElementById()、getElementsByName()、getElementsByTagName()、getElementsByClassName()
得到元素之后，我们可以设法获取它的属性。
#### getAttribute（）
获取属性
`object.getAttribute(attribute)`
getAttribute方法不属于document对象，所以不能通过document对象调用。它只能通过元素节点对象调用。
```javascript
document.getElementsByTagName("a")[107]
输出：<a class="strong" href="http://ln.ifeng.com/a/20161223/5258480_0.shtml" target="_blank">辽宁:向25个单位反馈巡视情况 一针见血指出问题</a>

document.getElementsByTagName("a")[107].getAttribute("href")
输出："http://ln.ifeng.com/a/20161223/5258480_0.shtml"
```
#### setAttribute()
对属性节点的值作出修改。
`object.setAttribute(attribute, value)`
```javascript
#接上例
document.getElementsByTagName("a")[107].setAttribute("href","flamepeak.com")
##然后
document.getElementsByTagName("a")[107].getAttribute("href")
#输出
“flamepeak.com”
```

#### childNodes属性
一棵节点树上，childNodes属性可以用来获取任何一个元素的所有子元素，它一个包含这个元素全部子元素的数组。
*element.childNodes*

#### nodeType属性
由childNodes属性返回的数组包含所有类型的节点，而不仅仅是元素节点。事实上，文档里几乎每一样东西都是一个节点，甚至连空格和换行符都会被解释为节点，而它们也全部包含在childNodes属性所返回的数组当中。
还好，每一个节点都有一个nodeType属性，这个个属性可以让我们知道自己正在和哪种节点打交道，差劲的一点是nodeType的值并不是英文。
获取节点的nodeType属性的语法是：
*node.nodeType*
nodeType属性共有12种可取的值，但其中最重要的是：
+ **元素节点**的nodeType属性值是1.
+ **属性节点**的nodeType属性值是2.
+ **文本节点**的nodeType属性值是3.
+ **注释**的nodeType属性值是8.
+ **文档**的nodeType属性值是9.

---
### 事件处理函数
事件处理函数的作用是，在特定事件发生时调用特定的JavaScript代码。
添加事件处理函数的语法是：
*event* = *"JavaScript statement(s)"*
需要注意的是，JavaScript代码包含在一对引号之间。可以吧任意数量的JavaScript语句放在这对引号之间，只要把各条语句用分号隔开即可。
例如：`onClick = "showPic(this)"`
其中，`this`关键字代表当前这个语句。

事件处理函数的工作机制：
在给某个元素添加了事件处理函数后，一旦事件发生，相应的JavaScript代码就会得到执行。被调用的JavaScript代码可以返回一个值，这个值将会被传递给那个事件处理函数。例如，我们可以给某个链接添加一个onClick事件处理函数，并让这个处理函数触发的JavaScript代码返回值是true或者false。这样一来，当这个链接不点击时，如果那段JavaScript代码返回的是true，onClick事件处理函数就认为“这个链接被点击了”，反之，如果返回值是false，onClick事件处理函数就认为“这个链接没有被点击”。
例如，下面的代码：
```javascript
<a href="images/fire.jpg" onclick="showPic(this);">Fire</a>
```
其在点击后会调用showPic(this)，然后跳转打开链接。
更改为下面的之后：
```javascript
<a href="images/fire.jpg" onclick="showPic(this);return false;">Fire</a>
```
这样，点击后调用执行showPic(this)，然后执行return false, 这样不会跳转。










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

**CSS**
DOM并不是与网页结构打交道的唯一技术。我们还可以使用CSS（层叠样式表）告诉浏览器应该如何显示一份文档的内容。

### 获取元素
有3中DOM方法可以获取元素节点，分别是通过元素ID、通过标签名字和通过类名字来获取。
#### getElementById
这个方法将返回一个与那个有着给定id属性值的元素节点对应的对象。
JavaScript区分大小写。
它是document对象特有的函数。在脚本代码里，函数名的后面必须跟有一对圆括号，这对圆括号包含着函数的参数。`getElementById`方法只有一个参数：你想获得的那个元素的id属性的值，这个id值必须放在单引号或双引号里。
`document.getElementById(id)`
e.g:
```JavaScript
document.getElementById("purchases")
```
#### getElementsByTagName
该方法返回一个对象数组，每个对象分别对应着文档里有这给定标签的一个元素。这个方法只有一个参数，它的参数是标签的名字：
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
这个方法让我们能够通过class属性中的类名来访问元素。其只接受一个参数，就是类名：
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









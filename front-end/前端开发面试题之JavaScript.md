![](http://upload-images.jianshu.io/upload_images/1714316-71dd9f7c05c24792.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> “每18至24个月，前端都会难一倍”
> 
> ——赫门 “2015深JS大会《前端服务化之路》主题演讲”

 
#### 知识点
`数据类型`、`运算`、`对象`、`function`、`继承`、`闭包`、`作用域`、`原型链`、`事件`、`RegExp`、`JSON`、`Ajax`、`DOM`、`BOM`、`内存泄漏`、`跨域`、`异步加载`、`模板引擎`、`前端MVC`、`前端MVVM`、`路由`、`模块化`、`Canvas`、`jQuery`、`ECMAScript 2015（ES6）`、`Node.js`、`AngularJS`、`React`、`CommonJS`、`AMD`、`CMD` ......


#### 题目&答案
- 介绍一下 JS 的基本数据类型。
```
Undefined、Null、Boolean、Number、String
```


- 介绍一下 JS 有哪些内置对象。
```
Object 是 JavaScript 中所有对象的父对象
数据封装类对象：Object、Array、Boolean、Number、String
其他对象：Function、Argument、Math、Date、RegExp、Error
```


- 列举几条 JavaScript 的基本代码规范。
```
（1）不要在同一行声明多个变量
（2）如果你不知道数组的长度，使用 push
（3）请使用 ===/!== 来比较 true/false 或者数值
（4）对字符串使用单引号 ''(因为大多时候我们的字符串。特别html会出现")
（5）使用对象字面量替代 new Array 这种形式
（6）绝对不要在一个非函数块里声明一个函数，把那个函数赋给一个变量。浏览器允许你这么做，但是它们解析不同
（7）不要使用全局函数
（8）总是使用 var 来声明变量，如果不这么做将导致产生全局变量，我们要避免污染全局命名空间
（9）Switch 语句必须带有 default 分支
（10）使用 /**...*/ 进行多行注释，包括描述，指定类型以及参数值和返回值
（11）函数不应该有时候有返回值，有时候没有返回值
（12）语句结束一定要加分号
（13）for 循环必须使用大括号
（14）if 语句必须使用大括号
（15）for-in 循环中的变量应该使用 var 关键字明确限定作用域，从而避免作用域污染
（16）避免单个字符名，让你的变量名有描述意义
（17）当命名对象、函数和实例时使用驼峰命名规则
（18）给对象原型分配方法，而不是用一个新的对象覆盖原型，覆盖原型会使继承出现问题
（19）当给事件附加数据时，传入一个哈希而不是原始值，这可以让后面的贡献者加入更多数据到事件数据里，而不用找出并更新那个事件的事件处理器
```


- 介绍一下 JavaScript 原型，原型链，它们有何特点？
```
每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，
于是就这样一直找下去，也就是我们平时所说的原型链的概念。
关系：instance.constructor.prototype = instance.__proto__
//
特点：JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本，当我们修改原型时，与之相关的对象也会继承这一改变。
//
当我们需要一个属性时，JavaScript引擎会先看当前对象中是否有这个属性，如果没有的话，就会查找它的prototype对象是否有这个属性，如此递推下去，一致检索到Object内建对象。
function Func(){}
Func.prototype.name = "Xiaosong";
Func.prototype.getInfo = function() {
    return this.name;
}
var person = new Func();
console.log(person.getInfo());
//"Xiaosong"
console.log(Func.prototype);
//Func { name = "Xiaosong", getInfo = function() }
```


- JavaScript 有几种类型的值？能否画一下它们的内存图？
```
栈：原始数据类型（Undefined，Null，Boolean，Number，String）
堆：引用数据类型（对象、数组、函数）
两种类型的区别：存储位置不同
//
原始数据类型直接存储在栈(stack)中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；
引用数据类型存储在堆(heap)中的对象,占据空间大、大小不固定,如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体。
```



- JavaScript 如何实现继承？
```
(1)构造继承
(2)原型继承
(3)实例继承
(4)拷贝继承
//
原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式。
function Parent() {
    this.name = 'song';
}
function Child() {
    this.age = 28;
}
Child.prototype = new Parent(); //通过原型,继承了Parent
//
var demo = new Child()l;
alert(demo.age);
alert(demo.name); //得到被继承的属性
```



- JavaScript 有哪几种创建对象的方式？
```
javascript创建对象简单的说,无非就是使用内置对象或各种自定义对象，当然还可以用JSON；但写法有很多种，也能混合使用。
//
(1)对象字面量的方式
person={firstname:"Mark",lastname:"Yun",age:25,eyecolor:"black"};
(2)用function来模拟无参的构造函数
function Person(){}
var person = new Person(); //定义一个function，如果使用new"实例化",该function可以看作是一个Class
person.name = "Xiaosong";
person.age = "23";
person.work = function() {
    alert("Hello " + person.name);
}
person.work();
(3)用function来模拟参构造函数来实现（用this关键字定义构造的上下文属性）
function Person(name,age,hobby) {
    this.name = name; //this作用域：当前对象
    this.age = age;
    this.work = work;
    this.info = function() {
        alert("我叫" + this.name + "，今年" + this.age + "岁，是个" + this.work);
    }
}
var Xiaosong = new Person("WooKong",23,"程序猿"); //实例化、创建对象
Xiaosong.info(); //调用info()方法
(4)用工厂方式来创建（内置对象）
var jsCreater = new Object();
jsCreater.name = "Brendan Eich"; //JavaScript的发明者
jsCreater.work = "JavaScript";
jsCreater.info = function() {
    alert("我是"+this.work+"的发明者"+this.name);
}
jsCreater.info();
(5)用原型方式来创建
function Standard(){}
Standard.prototype.name = "ECMAScript";
Standard.prototype.event = function() {
    alert(this.name+"是脚本语言标准规范");
}
var jiaoben = new Standard();
jiaoben.event();
(6)用混合方式来创建
function iPhone(name,event) {
    this.name = name;
    this.event = event;
}
iPhone.prototype.sell = function() {
    alert("我是"+this.name+"，我是iPhone5s的"+this.event+"~ haha!");
}
var SE = new iPhone("iPhone SE","官方翻新机");
SE.sell();
```



- eval 是做什么的？
```
它的功能是把对应的字符串解析成JS代码并运行；
应该避免使用eval，因为不安全，非常耗性能（2次，一次解析成js语句，一次执行）。
```



- 什么是 document 对象？什么是 window 对象？



- null 和 undefined 有何区别？
```
null        表示一个对象被定义了，值为“空值”；
undefined   表示不存在这个值。
//
typeof undefined
    //"undefined"
    undefined :是一个表示"无"的原始值或者说表示"缺少值"，就是此处应该有一个值，但是还没有定义。当尝试读取时会返回 undefined； 
    例如变量被声明了，但没有赋值时，就等于undefined。
//
typeof null
    //"object"
    null : 是一个对象(空对象, 没有任何属性和方法)；
    例如作为函数的参数，表示该函数的参数不是对象；
//
注意：
    在验证null时，一定要使用　=== ，因为 == 无法分别 null 和　undefined
```



- 能否写一个通用的事件侦听器函数？
```
//Event工具集，from:github.com/markyun
markyun.Event = {
    //页面加载完成后
    readyEvent: function(fn) {
        if (fn == null) {
            fn = document;
        }
        var oldonload = window.onload;
        if (typeof window.onload != 'function') {
            window.onload = fn;
        }else{
            window.onload = function() {
                oldonload();
                fn();
            };
        }
    },
    //视能力分别使用 demo0 || demo1 || IE 方式来绑定事件
    //参数：操作的元素，事件名称，事件处理程序
    addEvent: function(element,type,handler) {
        if (element.addEventListener) {
            //事件类型、需要执行的函数、是否捕捉
            element.addEventListener(type,handler,false);
        }else if (element.attachEvent) {
            element.attachEvent('on' + type, function() {
                handler.call(element);
            });
        }else {
            element['on' + type] = handler;
        }
    },
    //移除事件
    removeEvent: function(element,type,handler) {
        if (element.removeEventListener) {
            element.removeEventListener(type,handler,false);
        }else if (element.datachEvent) {
            element.datachEvent('on' + type,handler);
        }else{
            element['on' + type] = null;
        }
    },
    //阻止事件（主要是事件冒泡，因为IE不支持事件捕获）
    stopPropagation: function(ev) {
        if (ev.stopPropagation) {
            ev.stopPropagation();
        }else {
            ev.cancelBubble = true;
        }
    },
    //取消事件的默认行为
    preventDefault: function(event) {
        if (event.preventDefault) {
            event.preventDefault();
        }else{
            event.returnValue = false;
        }
    },
    //获取事件目标
    getTarget: function(event) {
        return event.target || event.srcElemnt;
    },
    //获取event对象的引用，取到事件的所有信息，确保随时能使用event；
    getEvent: function(e) {
        var ev = e || window.event;
        if (!ev) {
            var c = this.getEvent.caller;
            while(c) {
                ev = c.argument[0];
                if (ev && Event == ev.constructor) {
                    break;
                }
                c = c.caller;
            }
        }
        retrun ev;
    }
};
```



- ["1","2","3"].map(parseInt) 的答案是多少？
```
[1,NaN,NaN]
因为 parseInt 需要两个参数(val,radix)，其中 radix 表示解析时用的基数。
map 传了3个(element,index,array)，对应的 radix 不合法导致解析失败。
```



- 事件是什么？IE与火狐的事件机制有何区别？如何阻止冒泡？
```
(1)我们在网页中的某个操作（有的操作对应多个事件）。例如：当我们点击一个按钮就会产生一个事件。是可以被 JavaScript 侦测到的行为。
(2)事件处理机制：IE是事件冒泡、Firefox同时支持两种事件模型，也就是：捕获型事件和冒泡型事件；
(3)ev.stopPropagation();（旧ie的方法 ev.cancelBubble = true;）
```



- 什么是闭包(closure)，为什么要用它？
```
闭包是指有权访问另一个函数作用域中变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量，利用闭包可以突破作用链域，将函数内部的变量和方法传递到外部。
//
闭包特性：
(1)函数内再嵌套函数
(2)内部函数可以引用外层的参数和变量
(3)参数和变量不会被垃圾回收机制回收
//li节点的onclick事件都能正确的弹出当前被点击的li索引
<ul>
    <li> index = 0 </li>
    <li> index = 1 </li>
    <li> index = 2 </li>
    <li> index = 3 </li>
</ul>
<script type="text/javascript">
    var nodes = document.getElementsByTagName('li');
    for(i = 0;i<nodes.length;i+=1) {
        nodes[i].onclick = function() {
            console.log(i+1); //不使用闭包的话，值每次都是4
        }(4);
    }
</script>
```


- JavaScript 代码中的 "use strict"; 是什么意思？使用它的区别是什么？
```
use strict是一种ECMAscript 5 添加的（严格）运行模式,这种模式使得 Javascript 在更严格的条件下运行,使JS编码更加规范化的模式,消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为。
默认支持的糟糕特性都会被禁用，比如不能用with，也不能在意外的情况下给全局变量赋值;
全局变量的显示声明,函数必须声明在顶层，不允许在非函数代码块内声明函数,arguments.callee也不允许使用；
消除代码运行的一些不安全之处，保证代码运行的安全,限制函数中的arguments修改，严格模式下的eval函数的行为和非严格模式的也不相同;
提高编译器效率，增加运行速度；
为未来新版本的Javascript标准化做铺垫。
```



- new 操作符具体干了什么呢？
```
(1)创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
(2)属性和方法被加入到 this 引用的对象中。
(3)新创建的对象由 this 所引用，并且最后隐式的返回 this 。
//
var obj = {};
obj.__proto__ = Base.prototype;
Base.call(obj);
```



- 用原生的 JavaScript 实现过什么功能吗？



- JavaScript 中，有一个函数，执行对象查找时，永远不会去查找原型，这个函数是哪个？
```
hasOwnProperty
//
JavaScript 中 hasOwnProperty 函数方法是返回一个布尔值，指出一个对象是否具有指定名称的属性。此方法无法检查该对象的原型链中是否具有该属性；该属性必须是对象本身的一个成员。
//
使用方法：
object.hasOwnProperty(proName)
其中参数object是必选项，一个对象的实例。
proName是必选项，一个属性名称的字符串值。
//
如果 object 具有指定名称的属性，那么JavaScript中hasOwnProperty函数方法返回 true，反之则返回 false。
```



- 你对 JSON 了解吗？
```
JSON(JavaScript Object Notation)是一种轻量级的数据交换格式。
它是基于JavaScript的一个子集。数据格式简单，易于读写，占用带宽小。
如：
{"age":"12", "name":"back"}
```



- js延迟加载的方式有哪些？
```
defer和async、动态创建DOM方式（用得最多）、按需异步载入js
```



- Ajax 是什么？如何创建一个 Ajax ？
```
ajax的全称：Asynchronous Javascript And XML。
异步传输+js+xml。
所谓异步，在这里简单地解释就是：向服务器发送请求的时候，我们不必等待结果，而是可以同时做其他的事情，等到有了结果它自己会根据设定进行后续操作，与此同时，页面是不会发生整页刷新的，提高了用户体验。
//
(1)创建XMLHttpRequest对象,也就是创建一个异步调用对象
(2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息
(3)设置响应HTTP请求状态变化的函数
(4)发送HTTP请求
(5)获取异步调用返回的数据
(6)使用JavaScript和DOM实现局部刷新
```



- 同步和异步的区别？
```
同步的概念应该是来自于操作系统中关于同步的概念:
不同进程为协同完成某项工作而在先后次序上调整(通过阻塞,唤醒等方式)。同步强调的是顺序性，谁先谁后；异步则不存在这种顺序性。
//
同步：浏览器访问服务器请求，用户看得到页面刷新，重新发请求,等请求完，页面刷新，新内容出现，用户看到新内容,进行下一步操作。
//
异步：浏览器访问服务器请求，用户正常操作，浏览器后端进行请求。等请求完，页面不刷新，新内容也会出现，用户看到新内容。
```



- 如何解决跨域问题？
```
jsonp、iframe、window.name、window.postMessage、服务器上设置代理页面
```



- 页面编码和被请求的资源编码如果不一致如何处理？



- 谈一谈你对 ECMAScript6 的了解？
```
ECMAScript 6 是JavaScript语言的下一代标准，已经在2015年6月正式发布了。它的目标，是使得JavaScript语言可以用来编写复杂的大型应用程序，成为企业级开发语言。
标准的制定者有计划，以后每年发布一次标准，使用年份作为标准的版本。因为当前版本的ES6是在2015年发布的，所以又称ECMAScript 2015。也就是说，ES6就是ES2015
```



- ECMAScript 6 怎么写 class ，为何会出现 class？
```
ES6的class可以看作只是一个语法糖，它的绝大部分功能，ES5都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。
//定义类
class Point {
    constructor(x,y) {  //构造方法
        this.x = x;  //this关键字代表实例对象
        this.y = y;
    }
    toString() {
        return '(' + this.x + ',' + this.y + ')';
    }
}
```



- 异步加载 JS 的方式有哪些？
```
(1)defer，只支持 IE
(2)async:
(3)创建 script，插入到 DOM 中，加载完毕后 callBack
```



- document.write 和 innerHTML 有何区别？
```
document.write 只能重绘整个页面
innerHTML 可以重绘页面的一部分
```



- DOM 操作——怎样添加、移除、移动、复制、创建和查找节点？
```
(1)创建新节点
  createDocumentFragment()    //创建一个DOM片段
  createElement()   //创建一个具体的元素
  createTextNode()   //创建一个文本节点
(2)添加、移除、替换、插入
  appendChild()
  removeChild()
  replaceChild()
  insertBefore() //在已有的子节点前插入一个新的子节点
(3)查找
  getElementsByTagName()    //通过标签名称
  getElementsByName()    //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
  getElementById()    //通过元素Id，唯一性
```



- 数组和对象有哪些原生方法？能否列举一下？



- 如何编写高性能 JavaScript ？
详细文章：[浅谈编写高性能的Javascript代码](http://developer.51cto.com/art/200906/131335.htm)


- 哪些操作会造成内存泄漏？
```
内存泄漏是指任何对象在您不再拥有或需要它之后任然存在。
垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量，如果一个对象的引用数量为0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收。
//
setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）
```



- 是否看过 jQuery 的源码？能否简单概括一下它的实现原理？



- jQuery.fn 的 init 方法返回的 this 指的是什么对象？为什么要返回 this ？



- jQuery 中如何将数组转化为 json 字符串，然后再转化回来？
```
jQuery 中没有提供这个功能，所以需要先编写两个 jQuery 的扩展：
$.fn.stringifyArray = function(array) {
    return JSON.stringify(array)
}
$.fn.parseArray = function(array) {
    return JSON.parse(array)
}
//
然后调用:
$("").stringifyArray(array)
```



- jQuery 的属性拷贝（extend）的实现原理是什么？如何实现深拷贝？



- jQuery.extend 与 jQuery.fn.extend 有何区别？



- jQuery 的队列是如何实现的？队列可以用在哪些地方？



- jQuery 中一个对象可以同时绑定多个事件，这是如何实现的？



- 是否了解针对 jQuery 性能的优化方法？
```
基于Class的选择性的性能相对于Id选择器开销很大，因为需遍历所有DOM元素。
//
频繁操作的DOM，先缓存起来再操作。用Jquery的链式调用更好。
 比如：var str=$("a").attr("href");
 //
for (var i = size; i < arr.length; i++) {}
for 循环每一次循环都查找了数组 (arr) 的.length 属性，在开始循环的时候设置一个变量来存储这个数字，可以让循环跑得更快：
for (var i = size, length = arr.length; i < length; i++) {}
```



- jQuery 与 jQuery UI 有何区别？
```
`jQuery`是一个js库，主要提供的功能是选择器，属性修改和事件绑定等等。
`jQuery UI`则是在jQuery的基础上，利用jQuery的扩展性，设计的插件。提供了一些常用的界面元素，诸如对话框、拖动行为、改变大小行为等等
```



- jQuery UI 如何自定义组件？



- 如何判断当前脚本运行在浏览器还是 node 环境中？（阿里）
```
通过判断 Global 对象是否为 window ，如果不为 window ，当前脚本没有运行在浏览器中
```



- 什么是“前端路由”？什么时候适合使用“前端路由”？“前端路由”有哪些优点和缺点？



- 怎样用js实现千位分隔符？
```
正则 + replace
function commafy(num) {
    num = num + '';
    var reg = /(-?d+)(d{3})/;
    if (reg.test(num)) {
        num = num.replace(reg, '$1,$2');
    }
    return num;
}
```



- 检测浏览器版本有哪些方式？
```
功能检测、userAgent 特征检测
比如：navigator.userAgent
//"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.101 Safari/537.36"
```



- 谈谈你对 JavaScript 中的模块规范 CommonJS、AMD、CMD 的了解？
```
//个人拙见
|   CommonJS   |   AMD   |   CMD   |
|--------------|---------|---------|
|    Node.js   |RequireJS|  SeaJS  |
```
详细文章：[浅析JS中的模块规范（CommonJS，AMD，CMD）](http://www.2cto.com/kf/201411/348276.html)、[关于 CommonJS AMD CMD UMD](http://my.oschina.net/felumanman/blog/263330?p=1)



- 前端 MVC、MVVM
1、MVC
![MVC](http://upload-images.jianshu.io/upload_images/1714316-f5f3378c71fa8a2c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
模型（Model）：数据保存
视图（View）：用户界面
控制器（Controller）：业务逻辑
(1)View 传送指令到 Controller
(2)Controller 完成业务逻辑后，要求 Model 改变状态
(3)Model 将新的数据发送到 View ，用户得到反馈
所有通信都是单向的。
```
2、MVVM
![MVVM](http://upload-images.jianshu.io/upload_images/1714316-235c293d0a018e28.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
模型（Model）
视图（View）
视图模型（ViewModel）
(1)各部分间都是双向通信
(2)View 与 Model 不发生联系，都通过 ViewModel 传递
(3)View 非常薄，不部署任何业务逻辑，称为“被动视图”（Passive View），即没有任何主动性；而 ViewModel 非常厚，所有逻辑都部署在那里
采用双向绑定（data-binding）：View 的变动，自动反映在 ViewModel ，反之亦然。
```

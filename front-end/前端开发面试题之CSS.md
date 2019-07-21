![](http://upload-images.jianshu.io/upload_images/1714316-f8804a9415d4a244.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


> “每18至24个月，前端都会难一倍”
> 
> ——赫门 “2015深JS大会《前端服务化之路》主题演讲”



#### 知识点
`布局`、`盒子模型`、`选择器优先级`、`CSS3`、`Flexbox`、`浮动元素`、`Sass`、`Less`......



#### 题目&答案
- 介绍一下CSS的盒子模型。
```
(1)有两种， IE 盒子模型、标准 W3C 盒子模型；IE的content部分包含了 border 和 pading；
(2)盒模型： 内容(content)、填充(padding)、边界(margin)、 边框(border)。
```



- CSS选择符有哪些？哪些属性可以继承？
```
(1)id选择器（#classId）
(2)类选择器（.className）
(3)标签选择器（div，h1，p，span，table）
(4)相邻选择器（h1 + p）
(5)子选择器（ul > li）
(6)后代选择器（li a）
(7)通配符选择器（*）
(8)属性选择器（a[rel = "external"]）
(9)伪类选择器（a:hover，li:nth-child）
//
可继承的样式：font-size，font-family，color，UL，LI，DL，DD，DT
//
不可继承的样式：border，padding，margin，width，height
```



- CSS 如何计算优先级？
```
就近原则，同权重情况下以样式定义最近者为准；
载入样式以最后载入的定位为准；
优先级：
    !important > id > class > tag
    important 比 内联优先级高
```



- CSS3 新增的伪类有哪些？
```
CSS3新增伪类举例：
    p:first-of-type 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。
    p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。
    p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。
    p:only-child    选择属于其父元素的唯一子元素的每个 <p> 元素。
    p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。
    :enabled        :disabled 控制表单控件的禁用状态。
    :checked        单选框或复选框被选中。
```



- 如何居中div？如何居中一个浮动元素？如何让绝对定位的div居中？
  *给 div 设置一个宽度，然后添加 margin: 0 auto 属性*
  ```
  div{
    width: 200px;
    margin: 0 auto;
  }
  ```
  *居中一个浮动元素*
  ```
  确定容器的宽高（500*300）
  设置层的外边距
  .element{
    width: 500px;
    height: 300px;               //高度可以不设
    margin: -150px 0 0 -250px;
    position: relative;          //相对定位
    background-color: red;       //显示效果
    left: 50%;
    top: 50%;
  }
  ```
  *让绝对定位的 div 居中*
  ```
  .element{
    position: absolute;
    width: 1200px;
    background: none;
    margin: 0 auto;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
  }
  ```



- display 有哪些值？各有何作用？
```
block 象块类型元素一样显示。
none 缺省值。象行内元素类型一样显示。
inline-block 象行内元素一样显示，但其内容象块类型元素一样显示。
list-item 象块类型元素一样显示，并添加样式列表标记。
```



- position 中的 relative 和 absolute 的定位原点是什么？
```
absolute
    生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。
//
fixed （老IE不支持）
    生成绝对定位的元素，相对于浏览器窗口进行定位。
//
relative
    生成相对定位的元素，相对于其正常位置进行定位。
//
static
    默认值。没有定位，元素出现在正常的流中
   （忽略 top, bottom, left, right z-index 声明）。
//
inherit
    规定从父元素继承 position 属性的值。
```



- CSS3 有哪些新特性？
```
圆角-半径（border-radius:8px），
阴影（box-shadow:10px），
文字特效（text-shadow、），
线性渐变（gradient），
旋转（transform）
transform:rotate(9deg) scale(0.85,0.90) translate(0px,-30px) skew(-9deg,0deg);//旋转,缩放,定位,倾斜
增加了更多的CSS选择器
多背景 rgba
```



- 解释一下 CSS3 的 Flexbox （弹性盒布局模型），以及适用场景？



- 用纯 CSS 创建一个三角形的原理是什么？
```
把上、左、右三条边隐藏掉（颜色设为 transparent）
#demo {
    width:0;
    height: 0;
    border-width: 20px;
    border-style: solid;
    border-color: transparent transparent red transparent;
}
```



- 如何设计一个满屏“品”字布局？
```
简单的方式：
    上面的div宽100%，
    下面的两个div分别宽50%，
    用float或inline使其不换行。
```



- 常见兼容性问题有哪些？
```
(1)png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8。
(2)浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一。
(3)IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。
(4)IE下,可以使用获取常规属性的方法来获取自定义属性,也可以使用getAttribute()获取自定义属性;
Firefox下,只能使用getAttribute()获取自定义属性；
解决方法:统一通过getAttribute()获取自定义属性。
(5)
IE下,even对象有x,y属性,但是没有pageX,pageY属性;
Firefox下,event对象有pageX,pageY属性,但是没有x,y属性；
解决方法：（条件注释）缺点是在IE浏览器下可能会增加额外的HTTP请求数。
(6)Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示,可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决。
```



- li与li之间有看不见的空白间隔是什么原因引起的？有什么解决办法？




- 经常遇到的浏览器的兼容性有哪些？原因，解决方法是什么，常用hack的技巧？




- 为什么要初始化CSS样式？
```
因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没对CSS初始化往往会出现浏览器之间的页面显示差异。
当然，初始化样式会对SEO有一定的影响，但鱼和熊掌不可兼得，但力求影响最小的情况下初始化。
//
最简单的初始化方法： * {padding: 0; margin: 0;} （强烈不建议）
//
淘宝的样式初始化代码：
body, h1, h2, h3, h4, h5, h6, hr, p, blockquote, dl, dt, dd, ul, ol, li, pre, form, fieldset, legend, button, input, textarea, th, td { margin:0; padding:0; }
body, button, input, select, textarea { font:12px/1.5tahoma, arial, \5b8b\4f53; }
h1, h2, h3, h4, h5, h6{ font-size:100%; }
address, cite, dfn, em, var { font-style:normal; }
code, kbd, pre, samp { font-family:couriernew, courier, monospace; }
small{ font-size:12px; }
ul, ol { list-style:none; }
a { text-decoration:none; }
a:hover { text-decoration:underline; }
sup { vertical-align:text-top; }
sub{ vertical-align:text-bottom; }
legend { color:#000; }
fieldset, img { border:0; }
button, input, select, textarea { font-size:100%; }
table { border-collapse:collapse; border-spacing:0; }
```




- absolute 的 containing block（容器块）计算方式跟正常流有什么不同？
```
无论属于哪种，都要先找到其祖先元素中最近的 position 值不为 static 的元素，然后再判断：
(1)若此元素为 inline 元素，则 containing block 为能够包含这个元素生成的第一个和最后一个 inline box 的 padding box (除 margin, border 外的区域) 的最小矩形；
(2)否则,则由这个祖先元素的 padding box 构成。
如果都找不到，则为 initial containing block。
//
补充：
(1)static(默认的)/relative：简单说就是它的父元素的内容框（即去掉padding的部分）
(2)absolute: 向上找最近的定位为absolute/relative的元素
(3)fixed: 它的containing block一律为根元素(html/body)，根元素也是initial containing block
```



- CSS 里的 visibility 属性有个 collapse 属性值是干嘛用的？在不同浏览器下有什么区别？




- position 跟display、margin collapse、overflow、float这些特性相互叠加后会怎么样？




- 谈谈你对 BFC 规范（块级格式化上下文：block formatting context）的理解？
```
（W3C CSS 2.1 规范中的一个概念,它是一个独立容器，决定了元素如何对其内容进行定位,以及与其他元素的关系和相互作用。）
 一个页面是由很多个 Box 组成的,元素的类型和 display 属性,决定了这个 Box 的类型。
 不同类型的 Box,会参与不同的 Formatting Context（决定如何渲染文档的容器）,因此Box内的元素会以不同的方式渲染,也就是说BFC内部的元素和外部的元素不会互相影响。
```



- CSS 定义的权重
```
以下是权重的规则：标签的权重为1，class的权重为10，id的权重为100，以下例子是演示各种定义的权重值：
/*权重为1*/
div{
}
/*权重为10*/
.class1{
}
/*权重为100*/
#id1{
}
/*权重为100+1=101*/
#id1 div{
}
/*权重为10+1=11*/
.class1 div{
}
/*权重为10+10+1=21*/
.class1 .class2 div{
}
//
如果权重相同，则最后定义的样式会起作用，但是应该避免这种情况出现
```



- 请解释一下为什么会出现浮动？什么时候需要清除浮动？以及清除浮动的方式是什么？



- 移动端的布局用过媒体查询吗？



- CSS 优化、提高性能的方法有哪些？



- 浏览器是怎样解析 CSS 选择器的？



- 在网页中应该使用奇数还是偶数的字体？为什么？



- margin 和 padding 分别适合什么场景使用？



- 抽离样式模块怎么写？说出思路，有无实践经验？（阿里）



- 元素竖向的百分比设定是相对于容器的高度吗？



- 全屏滚动的原理是什么？用到了 CSS 的哪些属性？



- 什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的IE？



- 视差滚动效果，如何给每页做不同的动画？（回到顶部，向下滑动要再次出现，和只出现一次分别怎么做？）



- ::before 和 :after 中双冒号和单冒号有什么区别？解释一下这2个伪元素的作用。



- 如何修改 Chrome 记住密码后自动填充表单的黄色背景？



- 你对 line-height 是如何理解的？



- 设置元素浮动后，该元素的 display 值是多少？（自动变成display:block）



- 怎么让 Chrome 支持小于12px的字符？



- 让页面里的字体变清晰、变细用 CSS 怎么做？（-webkit-font-smoothing: antialiased;）



- font-style 属性可以让它赋值为“oblique”，oblique 是什么意思？




- position: fixed; 在 Android 下无效怎么处理？



- 如果需要手动写动画，你认为最小时间间隔是多久？为什么？（阿里）
```
多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小时间间隔为 1/6*1000ms = 16.7ms
```



- overflow: scroll 时不能平滑滚动的问题怎么处理？



- png、jpg、gif 这些图片格式解释一下，分别什么时候用。有没有了解过webp、jpg-large？



- 什么是 Cookie 隔离？（或者说：请求资源的时候不要让它带cookie怎么做）
```
如果静态文件都放在主域名下，那静态文件请求的时候都带有的cookie的数据提交给server的，非常浪费流量，所以不如隔离开。
因为cookie有域的限制，因此不能跨域提交请求，故使用非主要域名的时候，请求头中就不会带有cookie数据，这样可以降低请求头的大小，降低请求时间，从而达到降低整体请求延时的目的。
同时这种方式不会将cookie传入Web Server，也减少了Web Server对cookie的处理分析环节，提高了webserver的http请求的解析速度。
```



- 介绍一下 Sass 和 Less 是什么？它们有何区别？
```
Sass (Syntactically Awesome Stylesheets)是一种动态样式语言，语法跟css一样(但多了些功能)，比css好写，而且更容易阅读。Sass语法类似与Haml，属于缩排语法（makeup），用意就是为了快速写Html和Css。
Less一种动态样式语言. 将CSS赋予了动态语言的特性，如变量，继承，运算， 函数. LESS 既可以在客户端上运行 (支持IE 6+, Webkit, Firefox)，也可一在服务端运行 (借助 Node.js)。
区别：
(1))Sass是基于Ruby的，是在服务端处理的，而Less是需要引入less.js来处理Less代码输出Css到浏览器，也可以在开发环节使用Less，然后编译成Css文件，直接放到项目中，也有Less.app、SimpleLess、CodeKit.app这样的工具，也有在线编译地址。
(2)变量符不一样，less是@，而Scss是$，而且变量的作用域也不一样，后面会讲到。
(3)输出设置，Less没有输出设置，Sass提供4中输出选项：nested, compact, compressed 和 expanded。
(4)Sass支持条件语句，可以使用if{}else{},for{}循环等等。而Less不支持。
```


-----
> 资料搜集整理自 网络
> 同时发布在 [GitHub-前端开发面试题之HTML](https://github.com/YuanXiaosong/Front-End-Interview/blob/master/前端开发面试题之HTML.mdown)、[GitBook-《WEB-DE》前端开发面试题之HTML](https://wookong.gitbooks.io/web-de/content/02-Front-End%20Interview%20about%20HTML.html)

## 前端开发面试题之HTML

![](http://upload-images.jianshu.io/upload_images/1714316-3063f0220faa8f03.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

-----

> “每18至24个月，前端都会难一倍”
> 
> ——赫门 “2015深JS大会《前端服务化之路》主题演讲”

 
#### 知识点
`对Web标准的理解`、`浏览器内核差异`、`兼容性`、`hack`、`HTML5`......

#### 题目&答案
- Doctype作用？标准模式与兼容模式各有什么区别？
```
（1）<!DOCTYPE>声明位于HTML文档中的第一行，处于<html>标签之前，用于告知浏览器的解析器用什么文档标准解析这个文档。DOCTYPE不存在或格式不正确会导致文档以兼容模式呈现。
（2）标准模式的排版和JS运作模式都是以该浏览器支持的最高标准运行。在兼容模式中，页面以宽松的向后兼容的方式显示，模拟老式浏览器的行为以防止站点无法工作。
```

- HTML5为什么只需要写<!DOCTYPE HTML>？
```
HTML5不基于SGML，因此不需要对DTD进行引用，但是需要DOCTYPE来规范浏览器的行为（让浏览器按照它们应该的方式来运行）；
HTML4.01基于SGML，所以需要对DTD进行引用，才能让浏览器知道该文档所使用的文档类型。
```

- 行内元素有哪些？块级元素有哪些？空（void）元素有哪些？
```
声明：CSS规范规定，每个元素都有display属性，确定该元素的类型，每个元素都有默认的display值，如div的display默认值为“block”，则为“块级”元素；span默认display属性值为“inline”，是“行内”元素。

（1）行内元素有：a b span img input select strong（强调的语气）
（2）块级元素有：div ul ol li dl dt dd h1 h2 h3 h4…p
（3）常见的空元素：
    <br> <hr> <img> <input> <link> <meta>
     鲜为人知的空元素：
    <area> <base> <col> <command> <embed> <keygen> <param> <source> <track> <wbr>
```

 - 页面导入样式时，使用`Link`和`@import`有什么区别？
 
```
（1）link属于XHTML标签，除了加载CSS外，还能用于定义RSS, 定义rel连接属性等作用；而@import是CSS提供的，只能用于加载CSS;
（2）页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载;
（3）import是CSS2.1 提出的，只在IE5以上才能被识别，而link是XHTML标签，无兼容问题;
```

- 介绍一下你对浏览器内核的理解
```
主要分成两部分：渲染引擎(layout engineer或Rendering Engine)和JS引擎。
（1）渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。
（2）JS引擎则：解析和执行javascript来实现网页的动态效果。

最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。
```

- 常见的浏览器内核有哪些？

```
Trident内核：IE,MaxThon,TT,The World,360,搜狗浏览器等。[又称MSHTML]
Gecko内核：Netscape6及以上版本，FF,MozillaSuite/SeaMonkey等
Presto内核：Opera7及以上。      [Opera内核原为：Presto，现为：Blink;]
Webkit内核：Safari,Chrome等。   [ Chrome的：Blink（WebKit的分支）]
EdgeHTML内核：Microsoft Edge    [此内核其实是从MSHTML fork而来，删掉了几乎所有的IE私有特性]
```
详细文章：[浏览器内核的解析和对比——依水间](http://www.cnblogs.com/fullhouse/archive/2011/12/19/2293455.html)

- HTML5有哪些新特性、移除了哪些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？
```
* HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
      绘画 canvas;
      用于媒介回放的 video 和 audio 元素;
      本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失;
      sessionStorage 的数据在浏览器关闭后自动删除;
      语意化更好的内容元素，比如 article、footer、header、nav、section;
      表单控件，calendar、date、time、email、url、search;
      新的技术webworker, websockt, Geolocation;

  移除的元素：
      纯表现的元素：basefont，big，center，font, s，strike，tt，u;
      对可用性产生负面影响的元素：frame，frameset，noframes；

* 支持HTML5新标签：
     IE8/IE7/IE6支持通过document.createElement方法产生的标签，
     可以利用这一特性让这些浏览器支持HTML5新标签，
     浏览器支持新标签后，还需要添加标签默认的样式。

     当然最好的方式是直接使用成熟的框架、比如html5shim;
     <!--[if lt IE 9]>
        <script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
     <![endif]-->

* 区分方法： DOCTYPE声明\新增的结构元素\功能元素
```


- 简述一下你对HTML语义化的理解。
```
用正确的标签做正确的事情。

HTML语义化让页面的内容结构化，结构更清晰，便于对浏览器、搜索引擎解析；
即使在没有样式CSS的情况下也能以一种文档格式显示，并且是容易阅读的；
搜索引擎的爬虫也依赖于HTML标记来确定上下文和各个关键字的权重，有利于SEO；
使阅读源代码的人更容易将网站分块，便于阅读、维护和理解。
```


- HTML5的离线存储怎么使用？能否解释一下工作原理？
```
在用户没有连接英特网时，可以正常访问站点和应用；在用户连接英特网时，更新用户机器上的缓存文件。

原理：HTML5的离线存储是基于一个新建的 `.appcache` 文件的缓存机制（并非存储技术），通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储下来。之后当网络处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示。

使用方法：
1. 在页面头部像下面一样加入一个 manifest 的属性；
2. 在 cache.manifest 文件里编写离线存储资源；
       CACHE MANIFEST
       #v0.11
       CACHE：
           js/app.js
           css/style.css
       NETWORK:
           resource/logo.png
       FALLBACK：
           / /offline.html
3. 在离线状态时，操作 window.applicationCache 进行需求实现
```
详细使用教程：[有趣的HTML5：离线存储——segmentfault](https://segmentfault.com/a/1190000000732617)

- 浏览器是怎么对HTML5的离线存储资源进行管理和加载的？
```
在线情况下，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app，那么浏览器就会根据manifest文件的内容下载相应的资源并且进行离线存储。如果已经访问过app并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。

离线情况下，浏览器就直接使用离线存储的资源。
```


- 请描述一下 cookies，sessionStorage 和 localStorage 的区别？
```
`cookie`是网站为了标识用户身份而储存在用户本地终端（Client Side）上的数据（通常已经过加密）。cookie数据始终在同源的http请求中携带（即使不需要），也会在浏览器和服务器间来回传递。
`sessionStorage`和`localStorage`不会自动把数据发给服务器，仅在本地保存。

存储大小：
    cookie数据大小不能超过4K。
    sessionStorage和localStorage虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。

有效时间：
    cookie          设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭
    sessionStorage  数据在当前浏览器窗口关闭后自动删除
    localStorage    存储持久数据，浏览器关闭后数据不丢失除非主动删除数据
```


- iframe 有哪些缺点？
```
iframe会阻塞主页面的Onload事件；
搜索引擎的检索程序无法解读这种页面，不利于SEO；
iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。

使用iframe之前需要考虑这两个缺点。如果需要使用iframe，最好通过JavaScript动态给iframe添加src属性值，这样可以绕开以上两个问题。
```


- Label的作用是什么？如何使用？
```
label标签来定义表单控制间的关系，当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。

<label for="Name">Number:</label>
<input type="text" name="Name" id="Name" />

<label>Date:<input type="text" name="B" /></label>
```


- HTML5的form如何关闭自动完成功能？
```
给不想要提示的 form 或下面某个 input 设置为 `autocomplete = off`。
```


- 如何实现浏览器内多个标签页之间的通信？（阿里）
```
调用 localStorage、cookies 等本地存储方式
```


- webSocket 如何兼容低浏览器？（阿里）
```
Adobe Flash Socket
ActiveX HTMLFile（IE）
基于 multipart 编码发送 XHR
基于长轮询的 XHR
```


- 页面可见性（Page Visibility） API可以有哪些用途？
```
在页面被切换到其他后台进程的时候，自动暂停音乐或视频的播放。
```


- 如何在页面上实现一个圆形的可点击区域？
```
1. map + area 或者 svg
2. border-radius
3. 纯js实现，需要求一个点在不在圆上的简单算法、获取鼠标坐标等等
```


- 实现 不使用 border 画出 1px 高的线，在不同浏览器的标准模式与怪异模式下都能保持一致的效果。
```
<div style="height:1px;overflow:hidden;background:#ccc"></div>
```


- 网页验证码是干什么用的？是为了解决什么安全问题？
```
区分用户是计算机还是人的公共全自动程序。可以防止：恶意破解密码、刷票、论坛灌水；
有效防止黑客对某一个特定注册用户用特定程序通过暴力破解的方式进行不断的登录尝试。
```

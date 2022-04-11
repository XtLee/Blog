# HTML

### HTML、XML、XHTML有什么区别？

##### HTML

>超文本标记语言（HyperText Markup Language，简称：HTML）是一种用于创建网页的标准标记语言。 HTML是一种基础技术，常与CSS、JavaScript一起被众多网站用于设计令人赏心悦目的网页、网页应用程序以及移动应用程序的用户界面。


##### XML

>可扩展标记语言（英语：Extensible Markup Language，简称：XML），是一种标记语言。标记指计算机所能理解的信息符号，通过此种标记，计算机之间可以处理包含各种信息的文章等。如何定义这些标记，既可以选择国际通用的标记语言，比如HTML，也可以使用像XML这样由相关人士自由决定的标记语言，这就是语言的可扩展性。XML是从标准通用标记语言（SGML）中简化修改出来的。它主要用到的有可扩展标记语言、可扩展样式语言（XSL）、XBRL等。


##### XHTML

>可扩展超文本标记语言（英语：Extensible HyperText Markup Language，简称：XHTML），是一种标记语言，表现方式与超文本标记语言（HTML）类似，不过语法上更加严格。从继承关系上讲，HTML是一种基于标准通用标记语言（SGML）的应用，是一种非常灵活的置标语言，而XHTML则基于可扩展标记语言（XML），XML是SGML的一个子集。XHTML 1.0在2000年1月26日成为W3C的推荐标准。


### 怎样理解 HTML 语义化

>语义化的含义就是用正确的标签做正确的事情，html语义化就是让页面的内容结构化，便于对浏览器、搜索引擎解析；在没有样式CCS情况下也以一种文档格式显示，并且是容易阅读的。搜索引擎的爬虫依赖于标记来确定上下文和各个关键字的权重，利于 SEO。使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。


### 怎样理解内容与样式分离的原则

写 HTML 的时候先不管样式, 重点放在HTML的结构和语义化上，让 HTML 能体现页面结构或者内容。之后再去写样式。
写 JS 的时候，尽量不要用 JS 去直接操作样式，而是通过给元素添加删除class来控制样式变化。
HTML 内不允许出现属性样式，尽量不要出现行内样式。

### 有哪些常见的meta标签

`<meta charset='utf-8' />`：申明网页编码
` <meta name="renderer" content="webkit|ie-comp|ie-stand">`：浏览器内核控制
`<meta http-equiv="Pragma" content="no-cache">`：禁止浏览器从本地计算机的缓存中访问页面内容
`<meta name="mobile-agent"content="format=[wml|xhtml|html5]; url=url">`：站点适配
`<meta name="keywords" content="your tags" />`：页面关键词
`<meta name="description" content="150 words" />`：页面描述
`<meta name="apple-mobile-web-app-title" content="标题">`：添加到主屏后的标题


### 文档声明的作用?严格模式和混杂模式指什么?<!doctype html> 的作用?

为了告诉浏览器你的HTML是用哪一个版本所写，浏览器会根据你的版本执行不同版本的解码方式。

- 严格模式：在该模式下，浏览器会严格按照你所写的HTML和CSS对页面进行解析、渲染。
- 混杂模式：由来是一个历史问题。在互联网早期，网页一般写成两个版本：一个写给网景公司的 Navigator浏览器，一个写给微软公司的IE浏览器。当W3C制定了 Web 标准后，这两个浏览器不能马上开始按标准来解析渲染页面，因为这样会破坏当时大部分页面的显示效果。所以各浏览器就引入了混杂模式，在该模式下，浏览器会模拟Navigator 4和IE5的非标准行为来解析渲染页面，这样做就是为了兼容在W3C标准出现之前就存在的那些“不标准”的页面。

`<!doctype html>` 的作用是为了让浏览器执行严格模式来解析我们所写的HTML。


### 浏览器乱码的原因是什么？如何解决

一般情况下，浏览器在解析网页时所产生的乱码都是由于当初没有声明自身编写时所用的编码方式，或声明的编码方式与编写时使用的不符导致。因此，在写网页时一定要声明正确的编码方式预防乱码。


### 常见的浏览器有哪些，什么内核

常见的浏览器内核一般有Trident，Gecko，Webkit，Chromium/Bink这四种；与之对应的代表浏览器分别是IE、Mozilla FireFox、Safari、Google chrome。


### 列出常见的标签，并简单介绍这些标签用在什么场景


`div`：用于组合其他元素，本身并无什么意义。
`h1~h6, p, span, strong`：用于设置文本，对文本样式进行更改
`ul, li, ol, dl, dt, dd`：设置所有带列表内容
`form`：对表单进行设置
`table`：对表格进行设置
`img, canvas`：用于图像显示
`a`：设置链接


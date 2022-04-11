# 什么是BFC？

 **本文总结自饥人谷—方方老师：CSS深入浅出**

什么是BFC？为什么这个概念一直被提起？？为什么每一个人都解释不清BFC？？？

### 什么是BFC？

BFC 全称为 块格式化上下文 (Block Formatting Context) 。

从这个概念里你能看出来什么吗？

这个名字给我们的信息只有 “块” “格式化” “上下文” 。我们大概可以了解到这个东西是对上下文起作用的。
那里的上下文？？ HTML文档！
它大概的作用，貌似是格式化上下文？？可能不是我们通常意义中的格式化。

我们没有从这个名字中得到太多有用的信息，仅仅知道它是一种功能，针对于 HTML文档 起作用。

那我们去看看官方是怎么解释的。

**MDN：**
> 一个块格式化上下文（block formatting context） 是Web页面的可视化CSS渲染出的一部分。它是块级盒布局出现的区域，也是浮动层元素进行交互的区域。
一个块格式化上下文由以下之一创建：
> - 根元素或其它包含它的元素
> - 浮动元素 (元素的 float 不是 none)
> - 绝对定位元素 (元素具有 position 为 absolute 或 fixed)
> - 内联块 (元素具有 display: inline-block)
> - 表格单元格 (元素具有 display: table-cell，HTML表格单元格默认属性)
> - 表格标题 (元素具有 display: table-caption, HTML表格标题默认属性)
> - 具有overflow 且值不是 visible 的块元素，
> - display: flow-root
> - column-span: all 应当总是会创建一个新的格式化上下文，即便具有 column-span: all 的元素并不被包裹在一个多列容器中。
> - 一个块格式化上下文包括创建它的元素内部所有内容，除了被包含于创建新的块级格式化上下文的后代元素内的元素。
>
>块格式化上下文对于定位 (参见 float) 与清除浮动 (参见 clear) 很重要。定位和清除浮动的样式规则只适用于处于同一块格式化上下文内的元素。浮动不会影响其它块格式化上下文中元素的布局，并且清除浮动只能清除同一块格式化上下文中在它前面的元素的浮动。


我们发现一个什么问题！貌似看不懂哎！！

为什么会产生这样的原因？？

你能解释一下什么是桌子吗？？

仔细想想，发现好像并不能合理的解释它。

BFC 也是如此，只有特性(功能)，没有定义。

> I know it when i see it.


### BFC 特性(功能)


1. 使 BFC 内部浮动元素不会到处乱跑；
2. 和浮动元素产生边界。


#### 使 BFC 内部的浮动元素不会到处乱跑

![HTML](http://upload-images.jianshu.io/upload_images/6874766-ea17635c0fce844d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![没有产生 BFC](http://upload-images.jianshu.io/upload_images/6874766-6d653a57e10b289d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![CSS](http://upload-images.jianshu.io/upload_images/6874766-584b5099d583d80c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


在正常的文档流中，块级元素是按照从上自下，内联元素从左到右的顺序排列的。

如果我给里面的元素一个 float 或者绝对定位，它就会脱离普通文档流中。

![没有产生 BFC](http://upload-images.jianshu.io/upload_images/6874766-b1004d68354da7a6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

此时如果我们还想让外层元素包裹住内层元素该如果去做？？

让外层元素产生一个 BFC 。(产生 BFC 的方法 MDN 文档里有写)


![产生 BFC](http://upload-images.jianshu.io/upload_images/6874766-8e20e1906fb635b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**这就是 BFC 的第一个作用：使 BFC 内部的浮动元素不会到处乱跑。**


#### 和浮动元素产生边界

![HTML](http://upload-images.jianshu.io/upload_images/6874766-be3a24601f074424.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![CSS](http://upload-images.jianshu.io/upload_images/6874766-677110a2ac122553.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![没有产生 BFC](http://upload-images.jianshu.io/upload_images/6874766-217d6deeffa5d5d3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


一般情况下如果没有 BFC的话，我们想要让普通元素与浮动元素产生左右边距，需要将 maring 设置为浮动元素的宽度加上你想要产生边距的宽度。

这里的浮动元素的宽度为 200px ，如果想和它产生 20px 的右边距，需要将非浮动元素的 margin-left 设置为 200px+20px 。

![产生了 BFC](http://upload-images.jianshu.io/upload_images/6874766-5e7f183b642cb3d7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 总结


**不要试图去讲解 BFC 的定义！！**

**如何说明 BFC ，举例子！！不要试图去讲定义！！**

>I know it when i see it.
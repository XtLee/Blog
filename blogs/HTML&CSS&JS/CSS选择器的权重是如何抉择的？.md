# CSS选择器的权重是如何抉择的？

在解决这个问题之前我们先来看一下css选择器都有哪些。

## 一、选择器类型

#### 1、元素选择器  Element Selectors

```css
p {
  color: red;
}
div {
  color: blue;
}
```

这样子对某一个元素进行赋予就是元素选择器。

#### 2、ID选择器  ID Selectors

```
// html
<p id="notification">通知：明天放假</p>

// css
notification {
    font-size: 24px;
}
```

这个给元素一个ID并对ID进行赋予的就是ID选择器。

#### 3、类选择器  Class Selectors

```
// html
<ul>
  <li class="first done">起床</li>
  <li class="second done">刷牙</li>
  <li class="third">洗脸</li>
</ul>

// css
.first {
  font-weight: bold;
}
.done {
  text-decoration: line-through;
}
```

一个元素可以应用多个类，一个类也可以赋予给多个元素。

#### 4、通用选择器  Universal Selector

```css
*{
  box-sizing: border-box;
}
.flex-container * {
  flex-basis: 100%;
}
```

这种使用 * 号来写的就是通用选择器，它是对全局进行赋予的。

#### 5、属性选择器  Attribute Selectors
```css
[disabled] {
  cursor: not-allowed;
}
```

这种针对某一种特殊的属性进行赋予的是属性选择器。所有拥有这种属性的元素都会被赋予。

#### 6、伪类  Pseudo-classes

```css
a:link { ... }
a:visited { ... }
a:hover { ... }
a:active { ... }

li:first-child { ... }
li:last-child { ... }

body :not(p) { ... }
p:not(.warning) { ... }
```

这些特殊的类都是伪类。

#### 7、伪元素  Pseudo-elements

```css
::after
::before
::selection
::backdrop
::first-letter
::first-line
::-webkit-input-placeholder
```

#### 8、组合选择器  Combinators

```css
.author, .famous {
  font-weight: bold;
}
.article a {
  color: #384ebf;
}
.warriors > li {
  background-image: url(../images/warrior.svg);
}
.cavs .lbj + li {
  text-shadow: 1px 1px 5px #ccc;
}
.cavs .lbj ~ li {
  text-shadow: 1px 1px 5px #ccc;
}
```

#### 9、多个选择器  Multiple Selectors

```css
.players .player.curry, .player.mvp, #lebron-james {
  background-image: url(../images/mvp.png);
}
```

一次性对多个标签进行赋予。


## 二、权重计算规则

1. 第一等：代表内联样式，如: style=””，权值为1000。
2. 第二等：代表ID选择器，如：#content，权值为0100。
3. 第三等：代表类，伪类和属性选择器，如.content，权值为0010。
4. 第四等：代表类型选择器和伪元素选择器，如div p，权值为0001。
5. 通配符、子选择器、相邻选择器等的。如*、>、+,权值为0000。
6. 继承的样式没有权值。


## 三、比较规则

1. 1,0,0,0 > 0,99,99,99。也就是说从左往右逐个等级比较，前一等级相等才往后比。
2. 无论是行间、内部和外部样式，都是按照这个规则来进行比较。而不是直观的行间>内部>外部样式；ID>class>元素。之所以有这样的错觉，是因为确实行间为第一等的权重，所以它的权重是最高的。而内部样式可能一般写在了外部样式引用了之后，所以覆盖掉了之前的。
3. 在权重相同的情况下，后面的样式会覆盖掉前面的样式。
4. 通配符、子选择器、相邻选择器等的。虽然权值为0000，但是也比继承的样式优先。

## 四、!important

```css
.better {
  background-color: gray;
  border: none !important;
}
```

**[!important] 大于任何的规则，所有的权重里面，它排名第一。**（覆盖此!important声明的唯一方法是在源顺序中包含相同特异性的另一个!important声明。）


理解选择器的特殊性很重要，特别是在修复bug的时候，因为你需要了解哪些规则优先及其原因。
如果你遇到了似乎没有起作用的CSS规则，很可能是出现了特殊性冲突。请在你的选择器中添加他的一个父元素的ID，从而提高它的特殊性。如果这能解决问题，就说明样式表中其他地方很可能有更特殊的规则，它覆盖了你的规则。如果是这种情况，你可能需要检查代码，解决特殊性冲突，让代码尽可能简洁。
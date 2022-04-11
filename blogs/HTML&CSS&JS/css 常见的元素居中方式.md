# css 常见的元素居中方式

### 元素居中分为水平居中和垂直居中两种。

### 一、水平居中


**text-align**

```css
.container {
  text-align: center;
}
```

在元素的父元素上设置text-align的值为center就可以使文字/图片变为水平居中。设置为left/right的时候是左对齐/右对齐。

**margin**

```css
.container {
  width: 80%;
  margin-left: auto;
  margin-right: auto;
}
```

给元素的左和右的margin设置为auto并且元素在设置宽度之后就可以实现水平居中。

#### 区别：text-align:center设置为文本或img标签等一些内联对象（或与之类似的元素）的居中。margin:0 auto是设置块元素（或与之类似的元素）的居中。


### 二、垂直居中

**line-height**
设置元素的line-height值与height值相等即可实现元素垂直居中。适用于单行元素。

**table-cell**
```css
.box{
  width: 300px;
  height: 200px;
  display: table-cell;
  vertical-align: middle;
  text-align: center;
}
```

设置元素的display值为table-cell，适用于所有元素。

**绝对定位**
用absolute来设置元素的位置，适用于所有元素。

**vertical-align**
设置vertical-align的值为middle，可实现元素垂直居中，适用于所有元素。

**flex**
```css
.space {
  width: 100vw;
  height: 100vh; 
  display: flex; 
  align-items: center;  
}
```

利用display: flex来进行垂直居中，设置align-items为center，可实现元素垂直居中。



#### 这些方法使用时要根据情况来确定。



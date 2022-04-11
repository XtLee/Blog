# URL 如何编码解码？为什么要编码？

#### 为什么 URL 要进行编码？为什么要解码？？
原因很简单，因为 URL 只能使用 ASCII 字符集来通过因特网进行发送，**不支持中文！！不支持中文！！**

![](http://upload-images.jianshu.io/upload_images/6874766-6bd2f74a313993ca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在浏览器中的 URL 所展现的样式包含有中文字符，但是当你将这行 URL 复制粘贴时你就会发现，实际上的内容和你所看到的是不一样的。

![](http://upload-images.jianshu.io/upload_images/6874766-577172ed4d2228dd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

所以说 URL 编码只是针对非英文字母、阿拉伯数字和某些标点符号起作用的。

#### 那么 URL 是如何编码的呢？？

URL 编码的原则就是使用安全的字符（没有特殊用途或者特殊意义的可打印字符）去表示那些不安全的字符。

>首先需要把该字符的 ASCII 的值表示为两个16进制的数字，然后在其前面放置转义字符("`%`")，置入 URL 中的相应位置。(对于非 ASCII 字符, 需要转换为 UTF-8 字节序, 然后每个字节按照上述方式表示.)

例如说我们有这样一条 URL ：``www.hahaha.com/你好?a=1&b=2``，我们如何可以把它合法的在因特网中传播呢？？

使用 ``encodeURIComponent(str)`` 这个方法来将 utf-8 的字符编码为合法的 URL 。

上面的那条网址合法的传输形式为 `window.encodeURIComponent('www.hahaha.com/你好?a=1&b=2')` 。


![编码后的网址](http://upload-images.jianshu.io/upload_images/6874766-5735b24258c7b9e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#### 既然有编码，同样也有解码。

想要解码的时候只需要使用 `decodeURIComponent(str)` 这个方法就可以解码你所得到的
 URL 。

同样还是刚才的网址，我们得到解码后的网址为 `www.hahaha.com%2F%E4%BD%A0%E5%A5%BD%3Fa%3D1%26b%3D2` ，我们想要得到一个可读性比较高的网址，只需要 `decodeURIComponent('www.hahaha.com%2F%E4%BD%A0%E5%A5%BD%3Fa%3D1%26b%3D2')` 。



![解码后的网址](http://upload-images.jianshu.io/upload_images/6874766-c871da6293c50f05.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



如果哪天所有字符都可以在因特网内直接发送的话，可能就不需要在对 URL 进行编码和解码了......

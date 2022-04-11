# Vue组件通信

参考自[vue.js 官方文档](https://cn.vuejs.org/v2/guide/components.html)

如果你使用 Vue 进行开发的话，你不得不了解的一项就是 Vue 的组件(Component)。

组件是 Vue 中一项很强大的功能，它可以扩展 Html 元素，封装可重用代码，减少工作量。

在使用组件开发时的一大问题就是组件之间如何进行通信？？如果组件之间不能通信的话，那么它将大大减少的开发效率以及工作乐趣。

Vue 中的组件通信分为 **父子组件通信** 、 **兄弟组件通信** 这两大类。


### 父子组件通信

在 Vue 中，父子组件的关系可以理解为 **props向下传递** 、 **事件向上传递** 。

组件之间的作用域是孤立的，无法直接引用其他组件之内的数据。

如果子组件想要使用父组件内的数据应该如何去做呢？？

子组件需要通过 **props** 来声明预期的数据，而父组件通过直接在子组件内传值的方式将数据传给子组件。


![父子组件传值](http://upload-images.jianshu.io/upload_images/6874766-26e4cd670b81eb17.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![展示效果](http://upload-images.jianshu.io/upload_images/6874766-194e55afa9c390f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


如果你想要动态传值，只需要使用`v-bind`绑定所传的值。

![动态绑定](http://upload-images.jianshu.io/upload_images/6874766-49fd2ec45d6f8549.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![结果同步更新](http://upload-images.jianshu.io/upload_images/6874766-3fbc4074cc5e293c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### 兄弟组件通信

有人可能发现为什么父子组件通信中只写了父组件将数据传递给子组件的方法，却没有写如何在子组件中将数据传递给父组件？？

因为在子组件中，如果想要把数据传递给父组件，需要用到的方法和兄弟组件通信的方法是一样的。

这个时候就需要用到 Vue 的自定义事件 `$on(eventName)` 和 `$emit(eventName)` 来进行监听和触发事件。

![监听触发事件](http://upload-images.jianshu.io/upload_images/6874766-3255ef0388309a01.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)




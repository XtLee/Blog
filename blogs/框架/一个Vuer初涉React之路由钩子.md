# 一个Vuer初涉React之路由钩子

> 作为一个将近四年的Vuer，最近为了run开始学起了react。一开始以为现代前端框架都是大差不差的东西，想不到一上来就让我栽了个坑。

总所周知，vue-router提供了各种各样的钩子函数，且函数内还支持通过回调控制页面渲染。想着react这么大的框架应该也有差不多的东西，结果现实却狠狠打了脸。（中文母语者写的文档果然要比英文翻译的好(๑•̀ㅂ•́)و✧）

## 文档

咱也不知道是我英语差还是咋滴，先吐槽一波这个文档写的也太简陋了。要啥啥没有，啥啥也找不到。

![react-router](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2b44f1b2879b49148f8957c8757d6418~tplv-k3u1fbpfcp-watermark.image?)

看看人家隔壁的vue-router


![vue-router](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4038570a00524831a2b29f1c5900a635~tplv-k3u1fbpfcp-watermark.image?)

看人这示例代码的量，对于我这种CV选手太友好了。

## 开发

目前react的推荐写法为hooks，因此这次这次的尝试也是选择了hooks写法。


### 第一个坑：官方文档里没见过的元素

react-router的文档里，通篇的写法大都是直接通过Route元素确定一个路由。看到这里的时候我已经开始头大了。

这玩意是人写的东西？？？组件多一些，路由结构复杂一些，这玩意还能要？？？不得谁接手谁骂娘。

但是没办法啊，人文档都这么写了，咱能咋办，抄呗。于是开始吭哧吭哧的写。

路由有了，全局钩子咋弄啊？我这个组件展示之前是有用户身份验证的。

这里就不得不说一个问题，也是在后来解决react上遇到的问题的一个思路。Vue是一款前端开发框架，而React我更喜欢称他为开发库。框架里，所有的东西都是按照作者提供的方式确定好的，而你只需要在对应的时机进行对应的操作即可；但是，库却完全不同。库提供的是一个辅助方法，只有在需要的时候才需要库的介入，因此用库开发的前提是，你要认识到你是用JS+CSS+HTML进行开发，因此好多时候需要考虑如何使用JS去解决一些问题，而不是一味的找对应的api。

作为react小白，遇到不会的当然是去不在的网站上查询一下前辈的方案。然而，在前辈的方法里发现了一些没见过的东西。

```jsx
  <BrowserRouter>
    <Routes>
      <Route path="/" element={<App />}></Route>
    </Routes>
  </BrowserRouter>
```

这是官网的示例，我们可以看到外层使用`BrowserRouter`和`Routes`进行包裹，里面用`Route`定义单个路由。

但是我找到的大部分示例却是这样的：

```jsx
  <BrowserRouter>
    <Switch>
      <Route path="/" element={<App />}></Route>
    </Switch>
  </BrowserRouter>
```

**`Switch`是个啥玩意？？为啥文档里找不到？我瞎了嘛？**

在我仔仔细细的翻了两天文档后，还是在一个前辈的文章里了解到，这玩意是`Routes`的前身。

成吧，我忍了..

### 第二个坑：就是想用hooks

在不断寻找全局前置钩子的解决方案时，看到了`useRoutes`，仔细看看对应的写法，这不就跟vue一样吗，可算是找到了个我会的东西。

在仔细阅读过文档后，将代码改为了如下的形式：

```jsx
const router = [
    {
        path: '/',
        element: <App />,
    }
]

const App = () => {
    const myRoute = useRoutes(couter)
    return (
        <BrowserRouter>
            {myRoute}
        </BrowserRouter>
     )
}
```
看起来没啥大问题是吧？文档里说返回的是个router列表，且最外层使用的是`Routes`包裹，而且编译器还没报错。

然而当我决定启动项目看一下的时候，问题来了：


![router bug](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b721bc3f07a642e889f0d721831bff2b~tplv-k3u1fbpfcp-watermark.image?)

眼熟嘛？翻译一下就是`useRouters`只能在`Router`组件上下文内使用。

前辈的代码看多了，好歹我知道这个`Router`指的是`HashRouter`和`BrowserRouter`，但你告我，我那没有在他的上下文中用了！子组件不算上下文嘛？？

当我直接把`{myRoute}`改为`<MyRoute />`时，又提示我`<MyRoute />`元素不具有任何构造签名或调用签名。

**Emm...意思就是啥啥都不好使呗！
亏得你是个代码，你敢来线下看我削不削你就完了！！！**

没办法，为了run，为了多挣钱，还得学啊

又在大量调研了前辈的代码后，我发现了：

```jsx
const MyRoute = () => {
    const myRoute = useRoutes(couter)
    return myRoute
}

const App = () => {
    return (
        <BrowserRouter>
            <MyRoute />
        </BrowserRouter>
     )
}
```

我\*\*这有啥区别？？？（希望大佬能在评论区指点我一下，谢谢，给大佬提前拜年了）

### 第三个坑：网上的示例不能直接照抄啊

经过大量的研究和调研，大致思路如下：
1.  router对象的Element的值需要为一个组件，可以选择在这里下手；
2.  在自定义组件内部增加一些判断逻辑，根据结果渲染不同内容；

有了这个思路后，就开始着手准备写（Copy）代码。

```
包裹组件 {
    如果有处理函数：调用处理函数
    返回Element元素
}
```

到这里并没有什么问题，然而问题就出在了处理函数上。

众所周知，鬼知道后人拿你写的代码去干一些什么事情，所以最好你的代码能应付大部分场景。可是我能找到的解决方案里，都默认处理函数是个同步函数，这就导致了一旦有一些异步操作时，这玩意就不好使了哈！

这时，聪明的我想到了`useState`，给组件内部设置一个变量，给处理函数一个回调函数，回调里把变量变了，组件内根据变量的值返回子组件或null不就好了嘛。

讲真一开始的时候真的没想到这个，因为vue写的多，总考虑有没有什么办法能在处理函数执行时等待，甚至写上了`yield`。这里就是前面我提到的，从vue转变到react时，思维方式的转变很重要。


## 小结

方法的使用转换容易，思维方式转变起来就比较麻烦。这还只是刚开始，谁知道还会遇到什么问题呢。

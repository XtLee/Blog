# 一个Vuer初涉React之便捷开发配置

> 本人项目使用CRA（create-react-app）创建，因此本文仅针对由此方式进行构建的项目

在开发的时候，为了让import的路径短一点，通常都会用alias来处理，例如`../../../components/Button`会用`@/components/Button`来做为取代。

## Vue

在Vue内，使用`vue.config.js`来进行webpack配置的修改。而且写法大都同webpack相同，包含接口的代理也写在里面，配置完后直接起服务就可以了。

```js
// vue.config.js
vueConfig = {
    ...
    chainWebpack: (config) => {
        config.resolve.alias
          .set('@$', resolve('src'))
    },
    devServer: {
        proxy: {
            '/api': {
                target: 'host',
                changeOrigin: true,
                pathRewrite: {
                    '^/api': ''
                }
            }
        }
    }
}
```

这是一个常见的vue项目配置，里面设置了一个alias为`@`；一个监听以`/api`开头的请求代理，并将代理重定向到`host`地址，且将`/api`重写为`''`。

这种配置在一起的好处就是修改内容时很方便，而且有人接手项目时可以一眼看到之前的一些配置信息。

## React

### Alias

在第一次写react项目，秉着同本同源的逻辑，在项目内大肆搜索了一番，并未找到相关的配置文件，因此不得不去求助万能的Google。

网上找到的解决方案大致为两种：
- `npm run eject`放出默认配置进行修改；
- 使用`react-app-rewired` `craco`之类的插件，创建额外文件进行配置混入；

除了常见的这两种，其实还有一个最简单的法子：**js(ts)config.json**

```json
{
    ...
    "baseUrl": "./src",
    "paths": {
      "@/*": ["*"]
    }
}
```

关键点就在这两个字段

`baseUrl`：指定访问路径的根目录，例如访问路径为`src/views/Index/Index`，则根目录为src，访问路径就可以写为`views/Index/Index`；

`paths`：简单理解为指定一个别名，别名的访问路径为根据`bashUrl`指定；其实就是常说的alias，只不过写法不太一样；这里就是指定一个别名`@`，访问路径为src目录。


### Proxy

官方的推荐为，简单配置可直接在`package.json`里增加proxy字段，并赋值为字符串；复杂的使用`http-proxy-middleware`进行配置，创建`src/setupProxy.js`文件进行配置；

如果看过react打包时执行的代码的话，会产生一个问题，为什么基础配置只支持字符串，明明代码里只是获取`package.json`里的proxy字段进行合并。

于是我尝试改造我的`package.json`，将proxy的配置写入
```json
{
    ...
    "proxy": {
        "/api": {
            "target": "host",
            "ws": false,
            "changeOrigin": true,
            "pathRewrite": {
                "^/api": ""
            }
        }
    },
}
```

然而在我执行`yarn start`时，控制台会提示`When specified, "proxy" in package.json must be a string. Instead, the type of "proxy" was "object". Either remove "proxy" from package.json, or make it a string.`。我在配置文件内根本找不到这个提示，突然想到，会不会是在依赖里。经过搜索后，发现`react-dev-utils/WebpackDevServerUtils.js`有类型判断。

其实我这里不是很懂，react为什么不把配置给放开，这样相对来说会简单一些，希望大佬能在评论区给我一些解答。


---

至此，react项目的基本开发配置就完成，接下来就可以正式进入开发


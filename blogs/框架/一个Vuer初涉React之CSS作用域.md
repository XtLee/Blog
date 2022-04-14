# 一个Vuer初涉React之CSS作用域

> 开始学习的时候，按照官网的例子敲了一遍，有些问题根本没有暴露出来。自己写项目的时候才发现，React没有类似于Vue style scoped这个东西，所有的样式默认都是全局样式，导致会有样式覆盖。

遇到问题首先要求助万能的搜索引擎，这是一个程序员的基本操作

得到的解决方案如下：
- 内联样式（inline style）
- CSS in JS
- CSS modules
- 命名空间（namespaces）

## 内联样式（inline style）

```js
const styles = {
    width: '200px',
    height: '200px',
    background: 'red'
}

const App = () => {
    return <div style={styles}></div>
}
```

优点：上手简单，学习成本低；

缺点：无法支持CSS所有选择器，没有良好的代码提示；

## CSS in JS

```js
// styled-components
const ButtonWrap = styled.div`
    display: inline-block;
    padding: .5rem 0;
`

const Button = () => {
    return <ButtonWrap>这是个div元素</ButtonWrap>
}

```

优点：保留css功能的情况下，融入了js的部分功能，更加灵活；

缺点：引入第三方库，需要额外的学习成本；

## CSS Modues

```css
// style.module.css
.container {
    width: 200px;
    height: 200px;
}

.container .title {
    font-size: 30px;
    font-weight: bold;
    color: red;
}
```
```js
import style from 'style.module.css'

const App = () => {
    return (
        <div className={style.container}>
            <div className="title">这是个红色标题</div>
        </div>
     )
}
```
类似于命名空间的原理，只不过可以构建唯一命名；同样支持less、sass等；

优点：无额外学习成本，使用简单；

缺点：使用css时，部分层级可能嵌套过深，书写麻烦；需要webpack支持；

## 命名空间（namespaces）

```css
// style.css
.app .title {
    color: red
}
.other .title {
    color: blue;
}
```
```js
import 'style.css';

const Title = () => <div className="title">我是啥色看我爹</div>

const App = () => {
    return (
        <>
            <div className="app">
                <Title />
            </div>
            <div className="other">
                <Title />
            </div>
        </>
    )
}
```

优点：简单；

缺点：当项目量级足够大的时候，起出来不重复的名字也挺费劲的；

## 总结

方式 | 优点 | 缺点
---|---|---
内联样式（inline style） | 上手简单，学习成本低； |  无法支持CSS所有选择器，没有良好的代码提示；
CSS in JS | 保留css功能的情况下，融入了js的部分功能，更加灵活；| 引入第三方库，需要额外的学习成本；
CSS Modues | 无额外学习成本，使用简单； | 使用css时，部分层级可能嵌套过深，书写麻烦；需要webpack支持；
命名空间（namespaces） | 简单； | 当项目量级足够大的时候，起出来不重复的名字也挺费劲的；

没有绝对的好坏，使用时可以根据情况需求；当项目足够小的时候，直接css一把梭不香嘛？！
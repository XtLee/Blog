# TypeScript学习笔记—枚举和接口

> 前一阵子忙了一阵子，所以停止了学习TS。最近开始闲了，于是又捡起了看了个开头的TS来继续学习。

这次主要来聊一下TS的特殊类型：枚举和接口；

## 枚举

我们先来看一下官方对枚举类型的定义：
> 1、使用枚举我们可以定义一些带名字的常量。 
> 2、使用枚举可以清晰地表达意图或创建一组有区别的用例。 

![image](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/6/12/16b4ac48791dfcd9~tplv-t2oaga2asx-image.image)

常量？？`const`？？用例？？`const obj = {}`？？
```js
const obj = {
  a: '属性1',
  b: '属性2',
  c: '属性3'
}
```
常量√
有区别的用例√

那么问题来了！**枚举有什么用啊！**

区别就是：**枚举里每一项的值会根据前一项的值自动加一**；
~~少写俩数~~ 定义简单、方便；
```ts
// 默认为当前下标
enum X {
  a, // 0
  b, // 1
  c // 2
}
// 给定值后，后续元素值会自动加一
enum X {
  a = 1,
  b, // 2
  c // 3
}
enum X {
  a, // 0
  b = 2, // 2
  c // 3
}
```
除了数字之外，枚举的成员的值也可以是字符串。
```ts
enum X {
  a = 'a',
  b = 'b',
  c = 'c'
}
```
如果选择字符串作为成员的值，则其它枚举成员都需要有初始值（第一个除外）；
```ts
enum X {
  a, // 0
  b = 'b', // 'b'
  c // 报错：必须要有一个初始值
}
```

## 接口

首先是定义：
> 在TypeScript里，接口的作用就是为这些类型命名和为你的代码或第三方代码定义契约。

![image](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/6/12/16b4ac4879306f69~tplv-t2oaga2asx-image.image)

定义**契约**？？



简单来说，接口的作用就是声明某一类对象，需要拥有哪些属性。

![image](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/6/12/16b4ac48796c9725~tplv-t2oaga2asx-image.image)

```js
const person = {
  name: '名字',
  body: '身体'
}
```

我们定义了一个对象`person`；
它拥有`name`和`body`两个属性，那么如果我们想判断另一个对象`man`是不是`person`。我们可以定义一个接口，通过接口来判断`man`，是否符合我们对`person`的定义。

```ts
interface Person {
  name: string;
  body: string
}

const man: Person = {
  name: 'Bob',
  body: 'body'
}

const dog: Person = {
  name: 'Dog',
  body: 'body',
  voice: '汪'
} 
```
`man`没有报错，所以我们可以肯定`man`这个对象是`person`;
`dog`报错了，所以这个对象不是`person`;

![image](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/6/12/16b4ac487988880b~tplv-t2oaga2asx-image.image)

如果有时候有的属性我们不确定有没有怎么办？？

```ts
interface Person {
  name: string;
  body: string;
  kid?: number;
}
const man: Person = {
  name: 'Bob',
  body: 'body'
}
const woman: Person = {
  name: 'Alice',
  body: 'body',
  kid: 1
} 
```

只需要在属性名称后面加上`?`就可以表示：这个属性我不确定要不要，但是不管有没有，这个家伙都是我的！

![image](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/6/12/16b4ac487b2f71a8~tplv-t2oaga2asx-image.image)

除了属性以外，接口里还可以定义方法；

```ts
interface Person {
  name: string;
  body: string;
  say(something: string): void
}
```
假设我们有一些不想让人更改的属性，我们可以给它加上`readonly`关键字；
这类属性只有在初始化的时候可以赋值，之后不可以更改。

```ts
interface Person {
  readonly name: string;
  body: string;
  say(something: string): void
}
```

另外接口也可以继承接口；
```ts
interface Animal {
  body: string
}
interface Person extends Animal {
  readonly name: string;
  say(something: string): void
}
```

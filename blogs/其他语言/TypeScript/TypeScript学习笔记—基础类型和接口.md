# TypeScript学习笔记—基础类型和接口

> 这篇文章是我在学习ts时所做的笔记，可能会有一些遗落或者问题，欢迎大家交流、指点。

很早之前就收到过ts的安利，但是由于业务本身是开发微信小程序，ts用起来不是很方便，所以一直放在一边。这几天小程序开发工具更新后，发现小程序开始支持ts，趁此机会抓紧学习一下。

## 0. 基础类型

基础类型和原生js的类型基本是一样的，像是布尔值、数字、字符串...

|类型|表示方式|规则|
|---|---|---|
|布尔值|`boolean`|true/false，同js|
|数字|`number`|十进、十六进、二进和八进，同js|
|字符串|`string`|‘ / “ / `，同js|
|数组|`T[]/Array<T>`|T为元素类型，表示当前数组内元素的类型|
|元组|`[T1，T2...]`|已知元素数量和类型的数组。非元组内表明的元素，会以当前已知元素类型作为基础类型（T1/T2）|
|枚举|`enum 对象名 {对象内容1 = 下标（默认0），对象内容2，对象内容3...}`|类似于数组类型，可通过 “对象名[下标]” 的方式来获取下标处内容|
|任意类型|`any`|任意值，可调用任意类型的方法|
|void|`void`|非死循环且无返回值的函数，或为`undefined`和`null`的值|
|null和undefined|`null undefined`|默认为所有类型的子类型|
|never|`never`|其他类型的子类型，永不存在的值。返回为Error或者存在死循环的函数，也可做变量类型注解|
|Object|`object`|非原始类型，除`number`, `string`, `boolean`, `symbol`, `null`或`undefined`之外的类型|
|类型断言|`<T>value/value as T`|强制类型转换|

## 1. 接口

### 接口定义

```Typescript
interface ValueName { 
    value1?: T,
    value2: T
}
```

使用`interface`关键字来定义一个值的结构类型。

```Typescript
// 定义值的结构
interface PrintObj {
    value: string; // 可用分号或者逗号结尾
    name: string;
    desc?: string;
}
// 具体应用
function printSome(printObj: PrintObj):void {
    let content: string;
    if(printObj.desc) {
        content = `Hello! name: ${printObj.name}, value: ${printObj.value}, desc: ${printObj.desc}`
    } else {
        content = `Hello! name: ${printObj.name}, value: ${printObj.value}`
    }
}

printSome({name: 'content', value: 'empty', desc: 'none'});
```

ts类型检查只包含所声明的值，其他未声明的值不在检查范围内；

### 可选属性

```Typescript
interface PrintObj {
    value: string,
    name: string,
    desc?: string;
}
```

属性名定义后加`?`表示当前属性未可选属性，非必填；在引用不存在的属性时会报错。

### 只读属性

```Typescript
interface PrintObj {
    readonly value: string;
    readonly name: string;
}
```

只读属性，创建后不可更改。

### 可索引类型

```Typescript
interface PrintObj {
    [index: number]: string;
}
```

索引签名表示使用对应的属性去索引接口时得到相应类型的返回值。在上面这个例子中就是使用`number`类型去索引，可以得到`string`类型的返回值。

ts支持字符串索引和数字索引两种类型。**可以同时使用两种类型的索引，但是数字索引的返回值必须是字符串索引返回值的子类型。**

当接口内只定义了一个字符串索引时，其余属性的返回值必须要与索引的返回值类型相同。

```Typescript
interface PrintObj {
    [index: string]: string;
    used: boolean;
}
// 报错，used的类型与索引类型的返回值的类型不匹配。
```

索引签名也可以设置为只读，只需要在签名前加上`readonly`。

### 类类型

```Typescript
interface ClockInterface {
    currentTime: Date;
    setTime(d: Date);
}

class Clock implements ClockInterface {
    currentTime: Date;
    setTime(d: Date) {
        this.currentTime = d;
    }
    constructor(h: number, m: number) { }
}
```

明确强制一个Class符合某种定义。接口只描述Class的公共部分，不会检查Class是否具有某些私有成员。

当一个类实现一个接口的时候，只会对其实例部分进行检查，`constructor`存在于类的静态部分，所以不再检查范围内。

### 继承接口

```Typescript
interface Shape {
    color: string;
}

interface Square extends Shape {
    sideLength: number;
}
```

接口继承类似于Class继承，我们可以将一个接口成员复制到另一个接口里；一个接口可以继承多个接口，创建出多个接口的合成接口。

```Typescript
interface Shape {
    color: string;
}

interface PenStroke {
    penWidth: number;
}

interface Square extends Shape, PenStroke {
    sideLength: number;
}
```

### 接口继承类

接口可继承Class类型，它会继承Class的成员但不包括其实现。

```Typescript
class Control {
  private state: any;
}

interface SelectableControl extends Control {
  select(): void;
}

class Button extends Control implements SelectableControl {
  select() { }
}

class TextBox extends Control {
  select() { }
}

// 错误：“Image”类型缺少“state”属性。
class Image implements SelectableControl {
  select() { }
}
```

在这里，`SelectableControl`包含了`Control`所有的成员，包括私有成员。这里的`Image`类没有继承自`Control`，不包含私有成员`state`，所以这里的类型验证会失败。
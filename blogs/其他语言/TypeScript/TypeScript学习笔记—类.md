# TypeScript学习笔记—类

## 何为类

es6之前：没有**类**这个概念，当时听到最多的是原型对象以及原型链；  
es6之后：简单理解为`类 === class`；  
Java的里面的解释：**类是一个模板，它描述一类对象的行为和状态**；

简单理解为，**类**是一张图纸，它描述了一种东西，我们可以根据图纸来把这个东西做出来；假设我们要做一个杯子，那么**类**就是这个杯子的图纸。我们制作杯子的这个过程叫做**类的实例化**；因此我们可以得知，**类**与**接口**一样，用来描述一类东西；

前面我们说过，TypeScript是JavaScript的超集，所以ts的语法和js是一样的；在js里，我们用`class`来创建一个类，同样，在ts里，我们也可以用`class`来创建类。

## 类与接口的区别

前面我们说了**类**和**接口**一样，都是用来描述一种东西需要的特性，那么它们有什么区别吗？  
就像高r和高尔夫，高配和低配的区别；

```TypeScript
interface Human {
    name: string;
    speak(something: string): void;
}
class Human {
    name: string;
    constructor(name: string) {
        this.name = name;
    }
    speak(something: string): void {
        console.log(something);
    }
}
```

假设我们现在有如上的代码，此时我们想声明一个对象或者变量，它的类型是上面的一个，我们应该怎么写？

```TypeScript
// interface
let man: Human = {
    name: 'X-man',
    speak(something) {
        console.log(something);
    }
}
// class
let man2 = new Human('T-man');
```

发现了吗？  
高配的虽然写起来比较麻烦，但是实例化的时候很简单。

那么问题来了！

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/7/2/16bb1db5236b5654~tplv-t2oaga2asx-image.image)

## 语法

### 声明类

使用关键字`class`

```TypeScript
class Something {}
```

### 调用类

同js语法

```TypeScript
class Something {}

let a = new Something();
```

### constructor

不要忘了在你的类里写上`constructor`

```TypeScript
class A {
    constructor(/** 这里是实例化类的时候需要传递的参数 **/) {
        /** 这里可以初始化参数 **/
    }
}
```

### 类的属性

在你创建一个类的时候，你以为你写的所有属性都是类的属性，其实它们都是实例化对象的属性。如果想要添加类的属性，需要在属性前加上关键字`static`

```TypeScript
class A {
    static num: number = 1;    
    str: string = 'hello';
    
    static say(something: string): void {
        console.log(something)
    }
}
let a = new A();

a.str // 'hello'
a.num // Property 'num' is a static member of type 'A'
a.say // Property 'say' is a static member of type 'A'
```

### this

在js里人人都会遇到的问题，以及人人都知道的问题。在写某一个地方的时候，此时，劳资的`this`到底tm的是个啥？？

在这里，`this`代指的是你在写的类。你写在类里的方法或者属性都可以通过`this`来调用；

```TypeScript
class A {
    b: string;
    constructor() {
        console.log(this)
        this.b = 'b';
    }
}
let a = new A(); // class A
```

## 继承

同样，继承和js里类的继承语法是一样的，通过`子类 extends  父类`来进行继承；

```TypeScript
class Words {
    a: string;
}
class EnglishWords extends Words {
    b: string;
}

let english = new EnglishWords();
```

同样记得，如果在子类里声明了`constructor`，别忘了在`constructor`里起始位置调用`super()`；


```TypeScript
class Words {
    a: string;
}
class EnglishWords extends Words {
    b: string;
    construct() {
        super(); // 不声明会报错：Constructors for derived classes must contain a 'super' call.
    }
}

let english = new EnglishWords();
```

## 修饰符

实际上修饰符有三个，分别是：`public`、`private`、`protected`。但是ts里默认类里面所有的属性都是`public`，所以一般情况下我们可以直接忽略`public`。

### private 

直译为：私人的，私有； 

我们可以理解为，一旦你给类里面的属性添加了`private`修饰符，那么这个属性就是一个私有属性，只能在当前声明类的内部使用；相当于给当前类添加了一个单独的作用域；

```TypeScript
class A {
    a: number = 1;
    private b: number = 2;
}
class B extends A {
    c: number = 3;
}
let b = new B();
b.b // Property 'b' is private and only accessible within class 'A'.
```

所谓的私有即是：只有我可以用，别人谁都不可以；

```TypeScript
class A {
    a: number = 1;
    private b: number = 2;
}
class B extends A {
    c: number = 3;
    constructor() {
        super(); // 不写会报错
        this.b // Property 'b' is private and only accessible within class 'A'.
    }
}
```

### protected

直译为：保护，防护，保卫……

其实逻辑上来说，这个修饰符的命名有些问题。因为实际上他的作用和他的名字没有半毛钱关系；

要理解这个修饰符的话，我们需要对比`private`来看。

一个属性如果有`private`修饰符的话，那么他只能在创建它的类中使用；如果改成`protected`的话，那么创建类以及所有的子类中都可以使用。**（实例化对象仍然无法访问）**

```TypeScript
class A {
    a: number = 1;
    protected b: number = 2;
}
class B extends A {
    c: number = 3;
    constructor() {
        super(); // 不写会报错
        this.b // 不会报错
    }
}
let b = new B();
b.b // Property 'b' is protected and only accessible within class 'A' and its subclasses.
```

## 存取器

我们来看这样一段代码：

```TypeScript
class Human {
    name: string;
    age: number;
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}

const Li = new Human('Li', 20);
```

没有任何问题！ 是吧！

假如这个时候出现了一个**智者**，他把你对象的属性给你改了！

```TypeScript
Li.age = -1;
```

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/7/3/16bb5dc1e902009c~tplv-t2oaga2asx-image.image)

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/7/3/16bb5dc47150e514~tplv-t2oaga2asx-image.image)

你能怎么办？？？

所谓的**存取器**其实最大的作用就是，~~把真正的屎隐藏起来，展示给使用者优美的代码就好了~~。方便控制数据，不会出现以外的问题。



```TypeScript
class Human {
    _name: string;
    get name(): string {
        return this._name;
    }
    _age: number;
    get age(): number {
        return this._age
    }
    set age(val: number): void {
        if (val > 0) this._age = val; 
        else this._age = 0;
    }
    constructor(name: string, age: number) {
        this._name = name;
        this._age = age;
    }
}

const Li = new Human('Li', 20);

Li.name // 'Li'
Li.age // 20
Li.age = 21
Li.age // 21
Li.age = -1
Li.age // 0
```

**注意**： 在使用存取器之后，原本的类里面会增加对应属性。在上面的例子里，`Human`类在实例化之后会有四个属性，分别是：`_age`, `age`, `_name`, `name`。如果不想展示内部数据的话，在对应数据之前加上`private`修饰符。



```TypeScript
class Human {
    private _name: string;
    get name(): string {
        return this._name;
    }
    private _age: number;
    get age(): number {
        return this._age
    }
    set age(val: number): void {
        if (val > 0) this._age = val; 
        else this._age = 0;
    }
    constructor(name: string, age: number) {
        this._name = name;
        this._age = age;
    }
}
```


## 抽象类

> 抽象类做为其它派生类的基类使用。 它们一般不会直接被实例化。（作者：看不懂）

简化：抽象类做为其它派生类的基类使用 = 父类；它们一般不会直接被实例化 = 不会被实例化。  
结论：不会被实例化的父类。

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/7/3/16bb695a3dafabeb~tplv-t2oaga2asx-image.image)



```TypeScript
interface A {
    a: number;
    b(x: string): void;
}
```

这是一个接口，我们通过接口定义了一个类型`A`。仔细观察，你会发现我们只定义了它的组成，并没有定义具体的实现。


```TypeScript
class A {
    a: number;
    b(x: string): void;
}
```

同样的，接口也可这样定义。但是如果只是这样定义的话，ts会提示我们`Function implementation is missing or not immediately following the declaration.`，不可以声明未实现的函数。我们可以在~~不想写~~未实现的函数前面加上`abstract`修饰符，同时也需要在函数前加上`abstract`。因为`abstract`只能出现在`abstract`函数内。


```TypeScript
abstract class A {
    a: number;
    abstract b(x: string): void;
}
```

注意：抽象类不能实例化，必须要由子类继承。


```TypeScript
// 报错
abstract class A {
    a: number;
    abstract b(x: string): void;
}
let a = new A(); // Cannot create an instance of an abstract class.

// 正确
abstract class A {
    a: number;
    abstract b(x: string): void;
}
class B extends A {
    b(x: string) {
        console.log(x)
    }
}
let a = new B();
```
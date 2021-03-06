# JavaScript基本语法（一）

## 一、语句

JavaScript语言的执行单位为line，也就是一行一行的执行。一般情况下，每一行为一个语句。

语句是为了完成某种任务而进行的操作。

```js
var a = 1 + 1
```
这是赋值语句。用`var`命令，声明了变量`a`，然后将`1+1`的运算结果赋值给`a`。
`1+1`叫做**表达式**，表达式是一个为了得到返回值的计算式。
语句和表达式的区别在于：
- 语句是为了进行某种操作，一般是不需要返回值的。
- 表达式是为了得到返回值的式子，一定会返回一个值。

（所有预期为值的地方都可以使用表达式。一条语句可以包含多个表达式）

语句以分号结束，一个分号表示一条语句结束。多个语句可以写在同一行内。

```js
var a; a = 1;
```

如果分号前面没有任何内容的话，JavaScript会将其视为空语句。

```js
;;;;;
```

这就表示五个空语句。
大多数情况下，如果你省略了句尾的分号，JavaScript会自动添加。但是，如果下一行的第一个字元是（‘（’、‘[’、‘/’、‘+’以及‘-’）这五个其中之一的话，JavaScript将不会对上一行的句尾添加分号。

```js
a = b 
(function () {
    ……
}) ();
```

这样的代码等同于：

```js
a = b(function (){ ……}) ();
```

因此，不要省略句末的分号。

表达式不需要分号结尾。一旦在表达式后面添加分号，JavaScript引擎会将表达式识别为语句，这样会产生一些没有任何意义的语句。

```js
1 + 1;
true;
```

因为表达式的作用只是返回一个值，并没有任何其他的操作。所以这两条语句并没有什么意义。

## 二、变量

#### 1.概念

变量是对“值”的引用，使用变量等同于引用一个值。每一个变量都需要有一个变量名。

```js
var a = 1;
```

这条语句是先使用`var`这个命令声明变量`a`，然后将等号后面的表达式即`1`，赋值给了变量`a`。以后，当引用变量`a`的时候，就会得到数值`1`。

变量声明和变量赋值其实是分开的两个步骤，一般情况下合在一起，实际上他们是这样：

```js
var a;
a = 1;
```

如果只是声明变量而没有赋值，则该变量的值是`underfined`。`underfined`是JavaScript的一个关键字，表示“无定义”。（由于没有定义或者没有赋值，所以此处暂时没有任何值）

```js
var a;
a // underfined
```

如果一个变量没有生命就直接使用，JavaScript就会报错，告诉你变量未定义。

```js
b
// Uncaught ReferenceError: b is not defined
```

可以在同一条`var`命令中声明多个变量。

```js
var a, b;
```

JavaScript是一种动态类型语言，所以变量的类型没有限制，可以赋予各种类型的值。

```js
var a = 1;
a = 'hello';
```

这段代码中，变量`a`起先被赋值为1，而后又重新被赋值为一个字符串。第二次赋值的时候，因为变量已经存在，所以不需要使用`var`命令。
如果变量之前已经被赋值，后面在赋值时会顶替掉前面已有的赋值。

```js
var a = 1;
a = 'hello';
a // 'hello'
```

#### 2.变量提升

JavaScript工作方式是，先解析所有代码，获取所有被声明的变量，然后再一行一行的运行。这造成的结果就是，所有的变量声明的代码都会被提升到代码的头部，这就是**变量提升**。

```js
console.log(a);
var a = 1;
```

上面的代码虽然先使用了`console.log`的方法，在控制台中显示变量`a`的值，但是这时`a`还没有被声明，是一种错误的方法。但实际上并不会报错，因为存在着变量提升，真正运行的是：

```js
var a;
console.log(a);
a = 1;
```

最终的显示结果为`underfined`，因为变量`a`只是被声明，还没有赋值。
变量提升只对`var`声明的变量有效，如果一个变量不是用`var`声明命令所写，就不会发生变量提升。


##  三、标识符

标识符是用来识别具体对象的一个名称。最常见的标识符就是变量名以及函数名。
标识符的命名规则如下：
- 第一个字符，可以是任意Unicode字母（包括英文字母和其他语言字母），以及美元符号（$）和下划线（_）。
- 第二个及后面的字符，出了Unicode字母、美元符号以及下划线之外，还可以使用数字0-9.

```
合法标识符：
$$
_list
targe0
π

不合法标识符：
1a
123
**
a+b
-b
```

中文也是合法的标识符，也可以作为变量名。

**另：JavaScript有一些保留字，不能用作标识符。**
> 例如：arguments、break、case、catch、class、const、continue、debugger、default、delete、do、else、enum、eval、export、extends、false、finally、for、function、if、implements、import、in、instanceof、interface、let、new、null、package、private、protected、public、return、static、super、switch、this、throw、true、try、typeof、var、void、while、with、yield。

出了这些，还有三个有特殊含义的词也不能作为标识符：`Infinity`、`NaN`、`undefined`。

##  四、注释

源码中被JavaScript忽略的部分就是注释，它的作用是对代码进行解释。

```js
//  这是单行注释方法

<!--  同样是单行注释
-->  同样也是单行注释（只有在行首时才是注释，否则就是一个运算符）
/*
这是
多行
注释
*/
```


##  五、区块

JavaScript使用大括号，将多个相关的语句组合在一起，称为“区块”。JavaScript的区块不构成单独的作用域，也就是说，区块中的变量与区块外的变量，同属于一个作用域。

```js
{
   var a = 1;
}
a // 1
```

虽然代码在区块内部声明并赋值，但是在区块外部，变量`a`同样有效。


（内容参考自[阮一峰js教程](http://javascript.ruanyifeng.com)）
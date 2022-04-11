# JavaScript条件语句

条件语句的作用是，当用户满足某个特定的条件时，才会执行相应的语句。

##  if 结构

`if`结构是先判断一个表达式的布尔值，然后根据布尔值的结果，执行不同的语句。

```js
if (condition){
    //true statement
} else {
    //false statement
}
```
`condition`可以是任意表达式，JavaScript解释器会自动调用`Boolean()`将表达式的结果转换为布尔值。如果结果为`true`，则执行第一个代码块内的语句；如果为`false``，则执行第二个代码块内的语句。

if语句可以单独使用，也可以和多个`else`连续使用。

```js
if (a = 1){
    // statement
}

if (a == 1){
} else if (a == 2){
} else if (a == 3){
}
```

## label 标签

label是很多熟练的jser都会忽略的知识。语句的前面有标签（label），相当于定位符，用于跳转到程序的任意位置。
label语法：

```js
labelname: statement;
```

标签可以是任意的标识符，但是不能使保留字，语句部分可以是任意语句。


##  switch 结构


switch 语句和if 语句的关系密切，当多个`if...else`连在一起使用的时候，可以转为更方便的`switch`结构。

```js
switch(expresstion){
    case value1:
        statement;
        break;

    case value2:
        statement;
        break;

    default:
        statement;
}
```

`switch`语句会根据输入的变量`expresstion`的值，选择执行相应的`case`。如果所有的`case`都不符合，则执行最后的`default`部分。
需要注意的是，每个`case`代码内部的`break`语句不能少，否则会接下去执行下一个`case`代码块，而不是跳出`switch`结构。
虽然JavaScript的switch语句是参考C语言的写法，但是也有特殊性：
- switch和case可以使用任意表达式，不一定是常量。
- switch语句进行比较的时候是严格相等（===）运算，不是相等（==）运算。所以并不会发生类型的转换。


## while和do-while

while语句属于前测试循环语句，也就是在循环体内的代码被执行之前，先对条件进行检测，不符合的话就不会执行后面的代码。

```js
while(expression) {
    statement;
}
```
看个例子

```js
var i = 0;
while(i < 10) {
    console.log(i);
    i++;
}
```
结果会输出从0-9十个数字。

所以，我们在使用`while`循环语句时，一定要给它设定一个具体的范围。否则就会一直执行下去，你会发现网页会被卡死，什么也做不了。

do-while是后测试循环语句，在出口条件判断之前就会执行一次代码

```js
do {
    statement;
} while(expression);
```

不管条件是否为真，`do...while`循环至少运行一次。**另外，`while`语句后面的分号不能省略。**

##  for 循环语句

for语句也是前测试循环语句，但具备在执行循环代码以前初始化变量和定义循环后要执行代码的能力。它可以指定循环的起点、终点和终止条件。

```js
for(var i = 1, i < 3, i++) {
    console.log(i);
}
```

`for`语句后面的括号里有三个表达式：
- 初始化表达式：确定循环的初始值，只在循环开始时执行一次。
- 测试表达式：检查循环条件，只要为真（true）就进行后续的操作。
- 递增表达式：完成后续操作，然后返回上一步，再一次检查循环条件。

**如果省略的`for`语句表达式的三个部分，或者没有设置循环的终点，就会导致一个无限循环。**

##  break 和 continue

`break`和`continue`都具有跳转作用，可以让代码不按既有的顺序执行。
- `break`用于强制退出循环体，执行循环后面的语句
- `continue`用于退出本次循环，执行下次循环

```js
for(var i = 1; i< 10; i++){
    if(i % 4 === 0){
        break;
    }
    console.log(i);
}


for(var i = 1; i< 10; i++){
    if(i % 4 === 0){
        continue;
    }
    console.log(i);
}
```

**如果存在多重循环，不带参数的`break`和`continue`都只针对最内层循环。**


# if(xx)和xx==xx的判断

if和==这两个判断方式虽然都是通过布尔值来判断结果的，但是这两个判断方式的原理还是有很大差距的。

## if（xx）的判断方式

关于if的判断方式，来看几个例子。

> if ("hello") {
    console.log("hello")
}
if ("") {
    console.log('empty')
}
if (" ") {
    console.log('blank')
}

##### 结果是什么？  

第一个输出“hello”；第二个没有结果输出；第三个输出“blank”。

##### 为什么呢？？

我们前面说过，if与==都是通过布尔值来判断结果的。因此，if会把后面括号内的元素强制转换为布尔值，根据转化后的结果进行判断。

##### 转化规则

类型 | 结果
--- | ---
Undefined | false 
Null | false
Boolean | 直接判断
Number | +0, −0, 或者 NaN 为 false, 其他为 true
String | 空字符串为 false,其他都为 true
Object | true

根据这个规则我们可以很清楚的知道这个式子的结果，也可控制式子得到我们想要的结果。


## ==的判断方式

在了解==的判断方式之前我们需要先了解一下他的运算规则。

##### ==的运算规则

==是进行值的比较，而===则是进行属性与值的比较。前者在比较的时候Javascript会自动的帮我们进行属性的转换，但是有时候会有一些很奇怪的问题出现，这时候我们就需要知道它的转换规则。

- 如果两个值类型相等，就会严格的执行相等的运算
- 如果两个值类型不相等：
   1. 如果一个是null，一个是undefined，那么相等
   2. 如果一个是数字，一个是字符串，先将字符串转为数字，然后比较
   3. 如果一个值是true/false则将其转为1/0比较
   4. 如果一个值是对象，一个是数字或字符串，则尝试使用valueOf和toString转换后比较
   5. 其它就不相等了

##### ==的判断规则

我们还是先来看几个例子 

> "" == 0 
"" == false
" " == true 
"hello" == true
"0.00" == false

##### 结果是什么？  

第一个结果为true，第二个结果为true，第三个结果为false，第四个结果为false，第五个结果为true。

##### 为什么呢？？

x | y | 结果
--- | --- | ---
null | undefined | true
Number | String | x == toNumber(y)
Boolean | (any) | toNumber(x) == y
Object | String or Number | toPrimitive(x) == y
otherwise | otherwise | false

这是==在计算时的大体转化规则，具体的某些计算方式如下：

**toNumber**

类型 | 返回结果
--- | ---
Undefined | NaN
Null | 0
Boolean | ture -> 1, false -> 0
String | “abc” -> NaN, “123” -> 123

**toPrimitive**

对于 Object 类型，先尝试调用 .valueOf 方法获取结果。 如果没定义，再尝试调用 .toString方法获取结果。



这些是if（xx）和 “==”的判断规则。有时候搞清楚原理有助于我们更好的工作，写出不被评价为烂代码的东西。


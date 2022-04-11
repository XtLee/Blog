# JavaScript数据类型及运算符

## 数据类型

JavaScript 语言的每一个值，都属于某一种数据类型。JavaScript 的数据类型，共有七种。

- 数值（number）：整数和小数。例如：1、2、3、0.1、0.2、0.3...
- 字符串（string）：字符组成的文本。例如："hello world"、"你好"
- 布尔值（boolean）：true 和 false 两个特定值，不存在其他值。
- undefined：表示未定义或不存在。由于目前没有定义值，所以没有任何值。
- null：表示"无"值，此时的值就是“无”。
- 对象（object）：各种值组成的集合。
- 符号（Symbols）：symbols是ECMAScript第六版新定义的。它的值是唯一且不可修改的。

通常，我们将数值、字符串、布尔值、符号称为原始类型（primitive type）的值，即它们是最基本的数据类型，不能再细分了。而将对象称为合成类型（complex type）的值，因为一个对象往往是多个原始类型的值的合成，可以看作是一个存放各种值的容器。至于undefined和null，一般将它们看成两个特殊值。

#### 如何判断一个变量的属性？

JavaScript有三种方法可以判断变量的属性。
- typeof 
- instanceof
- Object.prototype.toString

利用这三种运算符可以判断当前变量的属性。

![原始类型返回属性](http://upload-images.jianshu.io/upload_images/6874766-fa666310afe966f1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![函数返回属性为function](http://upload-images.jianshu.io/upload_images/6874766-487bb8e9741db6ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 运算符 


#### 算数运算符

- 加法运算符（Addition）：x + y
- 减法运算符（Subtraction）： x - y
- 乘法运算符（Multiplication）： x * y
- 除法运算符（Division）：x / y
- 余数运算符（Remainder）：x % y
- 自增运算符（Increment）：++x 或者 x++
- 自减运算符（Decrement）：--x 或者 x--
- 求负运算符（Negate）：-x
- 数值运算符（Convert to number）： +x

#### 赋值运算符

>x += y // 等同于 x = x + y
x -= y // 等同于 x = x - y
x *= y // 等同于 x = x * y
x /= y // 等同于 x = x / y
x %= y // 等同于 x = x % y
x >>= y // 等同于 x = x >> y
x <<= y // 等同于 x = x << y
x >>>= y // 等同于 x = x >>> y
x &= y // 等同于 x = x & y
x |= y // 等同于 x = x | y
x ^= y // 等同于 x = x ^ y

#### 比较运算符

比较运算符的作用是比较两个值，然后返回一个布尔值。

- ==：相等，属性转换之后相等。
- ===：严格相等，值及属性完全相等。
- ！=：不相等，属性转换之后不相等。
- ！==：严格不相等，值及属性完全不相等。
- <：小于，前者的值小于后者的值。
- < =：小于或等于
- &gt;：大于，前者的值大于后者的值。
- &gt;=：大于或等于




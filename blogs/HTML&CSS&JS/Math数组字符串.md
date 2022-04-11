# Math数组字符串

写一个函数，生成一个长度为n的随机字符串，字符串字符的取值范围包括0-9，a-z，A-Z。

```js
function getRandStr(len){
    var dictionary = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
    var str = '';
    for(var i = 0; i < len, i++) {
        var newStr = Math.floor(Math.random()*dictionary.length);
        str += dictionary[newStr];
    }
    return str
}
var str = getRandStr(10);
```

#### Math.floor()

返回小于参数值的最大整数

```js
Math.floor(3.5); // 3
Math.floor(-3.5); // -4
```

####  Math.ceil()

返回大于该参数的最小整数

```js
Math.ceil(3.2) // 4
Math.ceil(-3.2) // -3
```

#### Math.randow()

返回0-1之间的一个伪随机数，可能等于0，但是一定小于1。当获取随机字符的时候要定义字符列表，给定一个取值范围。

```js
Math.random(); // 0.20851793009900121
Math.random(); // 0.1760216709379414
```
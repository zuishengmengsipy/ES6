# JavaScript 的基本语法

## JavaScript语言基础

### 组成

一个完整的 JavaScript 实现是由以下 3 个不同部分组成的：

* 核心（ECMAScript） 
* 文档对象模型（DOM） Document object model \(整合js，css，html\)
* 浏览器对象模型（BOM） Broswer object model（整合js和浏览器）

### JavaScript引入方式

#### Script标签内写代码

```markup
<script>
  // 在这里写你的JS代码
</script>
```

#### 引入额外的JS文件

```markup
<script src="myscript.js"></script>
```

### 注释

```javascript
// 这是单行注释

/*
这是
多行注释
*/
```

### 结束符

JavaScript中的语句要以分号（;）为结束符，以防被压缩成一行被误解

## 变量  <a id="&#x53D8;&#x91CF;"></a>

### 变量规范命名

1. JavaScript的变量名可以使用\_，数字，字母，$组成，不能以数字开头。
2. 声明变量使用 var 变量名; 的格式来进行声明
3. JavaScript 的变量名区分大小写，`A`和`a`是两个不同的变量。
4. 如果只是声明变量而没有赋值，则该变量的值是`undefined`。`undefined`是一个特殊的值，表示“无定义”。

```javascript
var name = "Alex";
var age = 18;
```

### 变量提升  <a id="&#x53D8;&#x91CF;&#x63D0;&#x5347;"></a>

JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）。

```javascript
console.log(a);
var a = 1;
```

上面代码首先使用`console.log`方法，在控制台（console）显示变量`a`的值。这时变量`a`还没有声明和赋值，所以这是一种错误的做法，但是实际上不会报错。因为存在变量提升，真正运行的是下面的代码。

```javascript
var a;
console.log(a);
a = 1;
```

最后的结果是显示`undefined`，表示变量`a`已声明，但还未赋值。

## 区块  <a id="&#x533A;&#x5757;"></a>

JavaScript 使用大括号，将多个相关的语句组合在一起，称为“区块”（block），对于`var`命令来说，JavaScript 的区块不构成单独的作用域（scope）。首先在函数内部查找变量，找不到则到外层函数查找，逐步找到最外层。

```javascript
{
  var a = 1;
}
```

### **局部变量**

在JavaScript函数内部声明的变量（使用 var）是局部变量，所以只能在函数内部访问它（该变量的作用域是函数内部）。只要函数运行完毕，本地变量就会被删除。

### **全局变量**

在函数外声明的变量是全局变量，网页上的所有脚本和函数都能访问它。

## 流程控制 <a id="&#x6761;&#x4EF6;&#x8BED;&#x53E5;"></a>

### if-else

```javascript
var a = 10;
if (a > 5){
  console.log("yes");
}else {
  console.log("no");

```

#### if-else if-else <a id="autoid-1-8-1"></a>

```javascript
var a = 10;
if (a > 5){
  console.log("a > 5");
}else if (a < 5) {
  console.log("a < 5");
}else {
  console.log("a = 5");

```

### switch

```javascript
var day = new Date().getDay();
switch (day) {
  case 0:
  console.log("Sunday");
  break;
  case 1:
  console.log("Monday");
  break;
default:
  console.log("...")
}
```

switch中的case子句通常都会加break语句，否则程序会继续执行后续case中的语句。如果所有`case`都不符合，则执行最后的`default`部分

### for

```javascript
for (var i=0;i<10;i++) {
  console.log(i);
}
```

### while

```javascript
var i = 0;
while (i < 10) {
  console.log(i);
  i++;
}
```

### 三元运算符

```javascript
var a = 1;
var b = 2;
var c = a > b ? a : b
var msg = '数字' + n + '是' + (n % 2 === 0 ? '偶数' : '奇数');
//字符串添加
```

### 标签（label）  <a id="&#x6807;&#x7B7E;&#xFF08;label&#xFF09;"></a>

JavaScript 语言允许，语句的前面有标签（label），相当于定位符，用于跳转到程序的任意位置标签可以是任意的标识符，但不能是保留字，语句部分可以是任意语句。标签通常与`break`语句和`continue`语句配合使用，跳出特定的循环。

```javascript
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) break top;
      console.log('i=' + i + ', j=' + j);
    }
  }
```

上面代码为一个双重循环区块，`break`命令后面加上了`top`标签（注意，`top`不用加引号），满足条件时，直接跳出双层循环。如果`break`语句后面不使用标签，则只能跳出内层循环，进入下一次的外层循环。

标签也可以用于跳出代码块

```text
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) continue top;
      console.log('i=' + i + ', j=' + j);
    }
  }
```

上面代码中，`continue`命令后面有一个标签名，满足条件时，会跳过当前循环，直接进入下一轮外层循环。如果`continue`语句后面不使用标签，则只能进入下一轮的内层循环。

## 数据类型

**JavaScript拥有动态类型**

```javascript
var x;  // 此时x是undefined
var x = 1;  // 此时x是数字
var x = "Alex"  // 此时x是字符串 
```

### **数值\(Number\)**

JavaScript不区分整型和浮点型，就只有一种数字类型。还有一种NaN，表示不是一个数字（Not a Number）。

```javascript
var a = 12.34;
var b = 20;
var c = 123e5;  // 12300000
var d = 123e-5;  // 0.00123
parseInt("123")  // 返回123
parseInt("ABC")  // 返回NaN,NaN属性是代表非数字值的特殊值。该属性用于指示某个值不是数字。
parseFloat("123.456")  // 返回123.456
```

### **字符串\(String\)**

```javascript
var a = "Hello"
var b = "world;
var c = a + b; 
console.log(c);  // 得到Helloworld
```

常用方法：

| 方法 | 说明 |
| :---: | :---: |
| .length | 返回长度 |
| .trim\(\) | 移除空白 |
| .trimLeft\(\) | 移除左边的空白 |
| .trimRight\(\) | 移除右边的空白 |
| .charAt\(n\) | 返回第n个字符 |
| .concat\(value, ...\) | 拼接 |
| .indexOf\(substring, start\) | 子序列位置 |
| .substring\(from, to\) | 根据索引获取子序列 |
| .slice\(start, end\) | 切片 |
| .toLowerCase\(\) | 小写 |
| .toUpperCase\(\) | 大写 |
| .split\(delimiter, limit\) | 分割 |

拼接字符串一般使用“+”

### 布尔值\(Boolean\)

区别于Python，true和false都是小写。

```javascript
var a = true;
var b = false;
//""(空字符串)、0、null、undefined、NaN都是false。
```

### null和undefined

* null表示值是空，一般在需要指定或清空一个变量时才会使用，如 name=null;
* undefined表示当声明一个变量但未初始化时，该变量的默认值是undefined。还有就是函数无明确的返回值时，返回的也是undefined。

null表示变量的值是空，undefined则表示只声明了变量，但还没有赋值。还不明白，上图吧！

![](https://images2018.cnblogs.com/blog/867021/201802/867021-20180226115608671-110898150.jpg)![](https://images2018.cnblogs.com/blog/867021/201802/867021-20180226114954211-338562205.jpg)

### 对象\(Object\)

JavaScript 中的所有事物都是对象：字符串、数值、数组、函数...此外，js 允许自定义对象JavaScript 提供多个内建对象，比如 String、Date、Array 等等。对象只是带有属性和方法的特殊数据类型。

### **数组**

数组对象的作用是：使用单独的变量名来存储一系列的值。类似于Python中的列表。

```javascript
var a = [123, "ABC"];
console.log(a[1]);  // 输出"ABC"
```

 常用方法：

| 方法 | 说明 |
| :---: | :---: |
| .length | 数组的大小 |
| .push\(ele\) | 尾部追加元素 |
| .pop\(\) | 获取尾部的元素 |
| .unshift\(ele\) | 头部插入元素 |
| .shift\(\) | 头部移除元素 |
| .slice\(start, end\) | 切片 |
| .reverse\(\) | 反转 |
| .join\(seq\) | 将数组元素连接成字符串 |
| .concat\(val, ...\) | 连接数组 |
| .sort\(\) | 排序 |
| .forEach\(\) | 将数组的每个元素传递给回调函数 |
| .splice\(\) | 删除元素，并向数组添加新元素。 |
| .map\(\) | 返回一个数组元素调用函数处理后的值的新数组 |

关于sort\(\)需要注意：

如果调用该方法时没有使用参数，将按字母顺序对数组中的元素进行排序，说得更精确点，是按照字符编码的顺序进行排序。要实现这一点，首先应把数组的元素都转换成字符串（如有必要），以便进行比较。

如果想按照其他标准进行排序，就需要提供比较函数，该函数要比较两个值，然后返回一个用于说明这两个值的相对顺序的数字。比较函数应该具有两个参数 a 和 b，其返回值如下：

若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。  
若 a 等于 b，则返回 0。  
若 a 大于 b，则返回一个大于 0 的值。

```javascript
function sortNumber(a,b){
    return a - b
}
var arr1 = [11, 100, 22, 55, 33, 44]
arr1.sort(sortNumber)
```

关于遍历数组中的元素，可以使用下面的方式：

```text
var a = [10, 20, 30, 40];
for (var i=0;i<a.length;i++) {
  console.log(a[i]);
}
```

#### forEach\(\) <a id="autoid-1-6-5"></a>

**语法：**forEach\(function\(currentValue, index, arr\), thisValue\)

| 参数 | 描述 |
| :--- | :--- |
| _function\(currentValue, index, arr\)_ | 必需。 数组中每个元素需要调用的函数。 函数参数: |
| _thisValue_ | 可选。传递给函数的值一般用 "this" 值。 如果这个参数为空， "undefined" 会传递给 "this" 值 |

#### splice\(\) <a id="autoid-1-6-6"></a>

**语法：**splice\(index,howmany,item1,.....,itemX\)

| 参数 | 描述 |
| :--- | :--- |
| _index_ | 必需。规定从何处添加/删除元素。 该参数是开始插入和（或）删除的数组元素的下标，必须是数字。 |
| _howmany_ | 必需。规定应该删除多少元素。必须是数字，但可以是 "0"。 如果未规定此参数，则删除从 index 开始到原数组结尾的所有元素。 |
| _item1_, ..., _itemX_ | 可选。要添加到数组的新元素 |

#### map\(\) <a id="autoid-1-6-7"></a>

**语法：**map\(function\(currentValue,index,arr\), thisValue\)

| 参数 | 描述 |
| :--- | :--- |
| _function\(currentValue, index,arr\)_ | 必须。函数，数组中的每个元素都会执行这个函数 函数参数:  |
| _thisValue_ | 可选。对象作为该执行回调时使用，传递给函数，用作 "this" 的值。 如果省略了 thisValue ，"this" 的值为 "undefined" |

**补充：**

ES6新引入了一种新的原始数据类型（Symbol），表示独一无二的值。它是JavaScript语言的第7种数据类型。

#### 类型查询 <a id="autoid-1-6-8"></a>

```javascript
typeof "abc"  // "string"
typeof null  // "object"
typeof true  // "boolean"
typeof 123 // "number"
```

typeof是一个一元运算符（就像++，--，！，- 等一元运算符），不是一个函数，也不是一个语句。

对变量或值调用 typeof 运算符将返回下列值之一：

* undefined - 如果变量是 Undefined 类型的
* boolean - 如果变量是 Boolean 类型的
* number - 如果变量是 Number 类型的
* string - 如果变量是 String 类型的
* object - 如果变量是一种引用类型或 Null 类型的

### 函数 <a id="autoid-1-8-6"></a>

#### 函数定义 <a id="autoid-1-9-0"></a>

JavaScript中的函数和Python中的非常类似，只是定义方式有点区别。[![&#x590D;&#x5236;&#x4EE3;&#x7801;](https://common.cnblogs.com/images/copycode.gif)](javascript:void%280%29;)

```text
// 普通函数定义
function f1() {
  console.log("Hello world!");
}

// 带参数的函数
function f2(a, b) {
  console.log(arguments);  // 内置的arguments对象
  console.log(arguments.length);
  console.log(a, b);
}

// 带返回值的函数
function sum(a, b){
  return a + b;
}
sum(1, 2);  // 调用函数

// 匿名函数方式
var sum = function(a, b){
  return a + b;
}
sum(1, 2);

// 立即执行函数
(function(a, b){
  return a + b;
})(1, 2);
```

[![&#x590D;&#x5236;&#x4EE3;&#x7801;](https://common.cnblogs.com/images/copycode.gif)](javascript:void%280%29;)

_补充：_

ES6中允许使用“箭头”（=&gt;）定义函数。

```text
var f = v => v;
// 等同于
var f = function(v){
  return v;
}
```

如果箭头函数不需要参数或需要多个参数，就是用圆括号代表参数部分：[![&#x590D;&#x5236;&#x4EE3;&#x7801;](https://common.cnblogs.com/images/copycode.gif)](javascript:void%280%29;)

```text
var f = () => 5;
// 等同于
var f = function(){return 5};

var sum = (num1, num2) => num1 + num2;
// 等同于
var sum = function(num1, num2){
  return num1 + num2;
}
```

[![&#x590D;&#x5236;&#x4EE3;&#x7801;](https://common.cnblogs.com/images/copycode.gif)](javascript:void%280%29;)

#### 函数中的arguments参数 <a id="autoid-1-9-1"></a>

[![&#x590D;&#x5236;&#x4EE3;&#x7801;](https://common.cnblogs.com/images/copycode.gif)](javascript:void%280%29;)

```text
function add(a,b){
  console.log(a+b);
  console.log(arguments.length)
}

add(1,2)
```

[![&#x590D;&#x5236;&#x4EE3;&#x7801;](https://common.cnblogs.com/images/copycode.gif)](javascript:void%280%29;)

输出：

```text
3
2
```

_注意：_

函数只能返回一个值，如果要返回多个值，只能将其放在数组或对象中返回。


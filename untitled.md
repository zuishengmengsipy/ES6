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

JavaScript中的语句要以分号（;）为结束符，以防被压缩误解，分号作用不小

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

JavaScript 使用大括号，将多个相关的语句组合在一起，称为“区块”（block），对于`var`命令来说，JavaScript 的区块不构成单独的作用域（scope）。

```javascript
{
  var a = 1;
}

a 
```

上面代码在区块内部，使用`var`命令声明并赋值了变量`a`，然后在区块外部，变量`a`依然有效，区块对于`var`命令不构成单独的作用域，与不使用区块的情况没有任何区别。在 JavaScript 语言中，单独使用区块并不常见，区块往往用来构成其他更复杂的语法结构，比如`for`、`if`、`while`、`function`等。

## 条件语句 [\#]() <a id="&#x6761;&#x4EF6;&#x8BED;&#x53E5;"></a>

JavaScript 提供`if`结构和`switch`结构，完成条件判断，即只有满足预设的条件，才会执行相应的语句。

### if 结构 [\#]() <a id="if-&#x7ED3;&#x6784;"></a>

`if`结构先判断一个表达式的布尔值，然后根据布尔值的真伪，执行不同的语句。所谓布尔值，指的是 JavaScript 的两个特殊值，`true`表示真，`false`表示`伪`。

```text
if (布尔值)
  语句;


if (布尔值) 语句;
```

上面是`if`结构的基本形式。需要注意的是，“布尔值”往往由一个条件表达式产生的，必须放在圆括号中，表示对表达式求值。如果表达式的求值结果为`true`，就执行紧跟在后面的语句；如果结果为`false`，则跳过紧跟在后面的语句。

```text
if (m === 3)
  m = m + 1;
```

上面代码表示，只有在`m`等于3时，才会将其值加上1。

这种写法要求条件表达式后面只能有一个语句。如果想执行多个语句，必须在`if`的条件判断之后，加上大括号，表示代码块（多个语句合并成一个语句）。

```text
if (m === 3) {
  m += 1;
}
```

建议总是在`if`语句中使用大括号，因为这样方便插入语句。

注意，`if`后面的表达式之中，不要混淆赋值表达式（`=`）、严格相等运算符（`===`）和相等运算符（`==`）。尤其是赋值表达式不具有比较作用。

```text
var x = 1;
var y = 2;
if (x = y) {
  console.log(x);
}

```

上面代码的原意是，当`x`等于`y`的时候，才执行相关语句。但是，不小心将严格相等运算符写成赋值表达式，结果变成了将`y`赋值给变量`x`，再判断变量`x`的值（等于2）的布尔值（结果为`true`）。

这种错误可以正常生成一个布尔值，因而不会报错。为了避免这种情况，有些开发者习惯将常量写在运算符的左边，这样的话，一旦不小心将相等运算符写成赋值运算符，就会报错，因为常量不能被赋值。

```text
if (x = 2) { 
if (2 = x) { 
```

至于为什么优先采用“严格相等运算符”（`===`），而不是“相等运算符”（`==`），请参考《运算符》章节。

### if...else 结构 [\#]() <a id="ifelse-&#x7ED3;&#x6784;"></a>

`if`代码块后面，还可以跟一个`else`代码块，表示不满足条件时，所要执行的代码。

```text
if (m === 3) {
  
} else {
  
}
```

上面代码判断变量`m`是否等于3，如果等于就执行`if`代码块，否则执行`else`代码块。

对同一个变量进行多次判断时，多个`if...else`语句可以连写在一起。

```text
if (m === 0) {
  
} else if (m === 1) {
  
} else if (m === 2) {
  
} else {
  
}
```

`else`代码块总是与离自己最近的那个`if`语句配对。

```text
var m = 1;
var n = 2;

if (m !== 1)
if (n === 2) console.log('hello');
else console.log('world');
```

上面代码不会有任何输出，`else`代码块不会得到执行，因为它跟着的是最近的那个`if`语句，相当于下面这样。

```text
if (m !== 1) {
  if (n === 2) {
    console.log('hello');
  } else {
    console.log('world');
  }
}
```

如果想让`else`代码块跟随最上面的那个`if`语句，就要改变大括号的位置。

```text
if (m !== 1) {
  if (n === 2) {
    console.log('hello');
  }
} else {
  console.log('world');
}

```

### switch 结构 [\#]() <a id="switch-&#x7ED3;&#x6784;"></a>

多个`if...else`连在一起使用的时候，可以转为使用更方便的`switch`结构。

```text
switch (fruit) {
  case "banana":
    
    break;
  case "apple":
    
    break;
  default:
    
}
```

上面代码根据变量`fruit`的值，选择执行相应的`case`。如果所有`case`都不符合，则执行最后的`default`部分。需要注意的是，每个`case`代码块内部的`break`语句不能少，否则会接下去执行下一个`case`代码块，而不是跳出`switch`结构。

```text
var x = 1;

switch (x) {
  case 1:
    console.log('x 等于1');
  case 2:
    console.log('x 等于2');
  default:
    console.log('x 等于其他值');
}



```

上面代码中，`case`代码块之中没有`break`语句，导致不会跳出`switch`结构，而会一直执行下去。正确的写法是像下面这样。

```text
switch (x) {
  case 1:
    console.log('x 等于1');
    break;
  case 2:
    console.log('x 等于2');
    break;
  default:
    console.log('x 等于其他值');
}
```

`switch`语句部分和`case`语句部分，都可以使用表达式。

```text
switch (1 + 3) {
  case 2 + 2:
    f();
    break;
  default:
    neverHappens();
}
```

上面代码的`default`部分，是永远不会执行到的。

需要注意的是，`switch`语句后面的表达式，与`case`语句后面的表示式比较运行结果时，采用的是严格相等运算符（`===`），而不是相等运算符（`==`），这意味着比较时不会发生类型转换。

```text
var x = 1;

switch (x) {
  case true:
    console.log('x 发生类型转换');
    break;
  default:
    console.log('x 没有发生类型转换');
}

```

上面代码中，由于变量`x`没有发生类型转换，所以不会执行`case true`的情况。这表明，`switch`语句内部采用的是“严格相等运算符”，详细解释请参考《运算符》一节。

### 三元运算符 ?: [\#]() <a id="&#x4E09;&#x5143;&#x8FD0;&#x7B97;&#x7B26;-"></a>

JavaScript 还有一个三元运算符（即该运算符需要三个运算子）`?:`，也可以用于逻辑判断。

```text
(条件) ? 表达式1 : 表达式2
```

上面代码中，如果“条件”为`true`，则返回“表达式1”的值，否则返回“表达式2”的值。

```text
var even = (n % 2 === 0) ? true : false;
```

上面代码中，如果`n`可以被2整除，则`even`等于`true`，否则等于`false`。它等同于下面的形式。

```text
var even;
if (n % 2 === 0) {
  even = true;
} else {
  even = false;
}
```

这个三元运算符可以被视为`if...else...`的简写形式，因此可以用于多种场合。

```text
var myVar;
console.log(
  myVar ?
  'myVar has a value' :
  'myVar does not have a value'
)

```

上面代码利用三元运算符，输出相应的提示。

```text
var msg = '数字' + n + '是' + (n % 2 === 0 ? '偶数' : '奇数');
```

上面代码利用三元运算符，在字符串之中插入不同的值。

## 循环语句 [\#]() <a id="&#x5FAA;&#x73AF;&#x8BED;&#x53E5;"></a>

循环语句用于重复执行某个操作，它有多种形式。

### while 循环 [\#]() <a id="while-&#x5FAA;&#x73AF;"></a>

`While`语句包括一个循环条件和一段代码块，只要条件为真，就不断循环执行代码块。

```text
while (条件)
  语句;


while (条件) 语句;
```

`while`语句的循环条件是一个表达式，必须放在圆括号中。代码块部分，如果只有一条语句，可以省略大括号，否则就必须加上大括号。

```text
while (条件) {
  语句;
}
```

下面是`while`语句的一个例子。

```text
var i = 0;

while (i < 100) {
  console.log('i 当前为：' + i);
  i = i + 1;
}
```

上面的代码将循环100次，直到`i`等于100为止。

下面的例子是一个无限循环，因为循环条件总是为真。

```text
while (true) {
  console.log('Hello, world');
}
```

### for 循环 [\#]() <a id="for-&#x5FAA;&#x73AF;"></a>

`for`语句是循环命令的另一种形式，可以指定循环的起点、终点和终止条件。它的格式如下。

```text
for (初始化表达式; 条件; 递增表达式)
  语句



for (初始化表达式; 条件; 递增表达式) {
  语句
}
```

`for`语句后面的括号里面，有三个表达式。

* 初始化表达式（initialize）：确定循环变量的初始值，只在循环开始时执行一次。
* 条件表达式（test）：每轮循环开始时，都要执行这个条件表达式，只有值为真，才继续进行循环。
* 递增表达式（increment）：每轮循环的最后一个操作，通常用来递增循环变量。

下面是一个例子。

```text
var x = 3;
for (var i = 0; i < x; i++) {
  console.log(i);
}



```

上面代码中，初始化表达式是`var i = 0`，即初始化一个变量`i`；测试表达式是`i < x`，即只要`i`小于`x`，就会执行循环；递增表达式是`i++`，即每次循环结束后，`i`增大1。

所有`for`循环，都可以改写成`while`循环。上面的例子改为`while`循环，代码如下。

```text
var x = 3;
var i = 0;

while (i < x) {
  console.log(i);
  i++;
}
```

`for`语句的三个部分（initialize、test、increment），可以省略任何一个，也可以全部省略。

```text
for ( ; ; ){
  console.log('Hello World');
}
```

上面代码省略了`for`语句表达式的三个部分，结果就导致了一个无限循环。

### do...while 循环 [\#]() <a id="dowhile-&#x5FAA;&#x73AF;"></a>

`do...while`循环与`while`循环类似，唯一的区别就是先运行一次循环体，然后判断循环条件。

```text
do
  语句
while (条件);


do {
  语句
} while (条件);
```

不管条件是否为真，`do...while`循环至少运行一次，这是这种结构最大的特点。另外，`while`语句后面的分号注意不要省略。

下面是一个例子。

```text
var x = 3;
var i = 0;

do {
  console.log(i);
  i++;
} while(i < x);
```

### break 语句和 continue 语句 [\#]() <a id="break-&#x8BED;&#x53E5;&#x548C;-continue-&#x8BED;&#x53E5;"></a>

`break`语句和`continue`语句都具有跳转作用，可以让代码不按既有的顺序执行。

`break`语句用于跳出代码块或循环。

```text
var i = 0;

while(i < 100) {
  console.log('i 当前为：' + i);
  i++;
  if (i === 10) break;
}
```

上面代码只会执行10次循环，一旦`i`等于10，就会跳出循环。

`for`循环也可以使用`break`语句跳出循环。

```text
for (var i = 0; i < 5; i++) {
  console.log(i);
  if (i === 3)
    break;
}




```

上面代码执行到`i`等于3，就会跳出循环。

`continue`语句用于立即终止本轮循环，返回循环结构的头部，开始下一轮循环。

```text
var i = 0;

while (i < 100){
  i++;
  if (i % 2 === 0) continue;
  console.log('i 当前为：' + i);
}
```

上面代码只有在`i`为奇数时，才会输出`i`的值。如果`i`为偶数，则直接进入下一轮循环。

如果存在多重循环，不带参数的`break`语句和`continue`语句都只针对最内层循环。

### 标签（label） [\#]() <a id="&#x6807;&#x7B7E;&#xFF08;label&#xFF09;"></a>

JavaScript 语言允许，语句的前面有标签（label），相当于定位符，用于跳转到程序的任意位置，标签的格式如下。

```text
label:
  语句
```

标签可以是任意的标识符，但不能是保留字，语句部分可以是任意语句。

标签通常与`break`语句和`continue`语句配合使用，跳出特定的循环。

```text
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) break top;
      console.log('i=' + i + ', j=' + j);
    }
  }




```

上面代码为一个双重循环区块，`break`命令后面加上了`top`标签（注意，`top`不用加引号），满足条件时，直接跳出双层循环。如果`break`语句后面不使用标签，则只能跳出内层循环，进入下一次的外层循环。

标签也可以用于跳出代码块。

```text
foo: {
  console.log(1);
  break foo;
  console.log('本行不会输出');
}
console.log(2);


```

上面代码执行到`break foo`，就会跳出区块。

`continue`语句也可以与标签配合使用。

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




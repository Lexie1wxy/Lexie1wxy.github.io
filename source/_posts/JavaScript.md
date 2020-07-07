---
title: JavaScript
date: 2020-07-06 10:02:40
tags: [前端,JavaScript]
categories:
- web前端
- JavaScript
typora-root-url: ../_posts
---

# 前言

Html和CSS、JavaScript的关系，学习web前端开发基础技术需要掌握：HTML、CSS、JavaScript语言。下面我们就来了解下这三门技术都是用来实现什么的：

1. HTML：提供网页的结构，提供网页中的内容
2. CSS: 用来美化网页
3. JavaScript: 可以用来控制网页内容，给网页增加动态的效果

# 简介

## 1 JavaScript定义

JavaScript是一种运行在***客户端*** 的***脚本语言***
JavaScript的解释器被称为JavaScript引擎，为浏览器的一部分，广泛用于客户端的脚本语言，最早是在HTML（标准通用标记语言下的一个应用）网页上使用，用来给HTML网页增加动态功能。所有现代的 HTML 页面都使用 JavaScript，可以用于改进设计、验证表单、检测浏览器、创建cookies等。

## 2 JavaScript组成

![img](/../images/JavaScript/20190411102957329.png)

（1）核心（ECMAScript）：这一部分主要是js的基本语法。

（2）BOM：Brower Object Model（浏览器对象模型），主要是获取浏览器信息或操作浏览器的，例如：浏览器的前进与后退、浏览器弹出提示框、浏览器地址栏输入网址跳转等操作等。

（3）DOM：Document Object Model（文档对象模型），此处的文档暂且理解为html，html加载到浏览器的内存中，可以使用js的DOM技术对内存中的html节点进行修改，用户从浏览器看到的是js动态修改后的页面。（增删改查）

## 3 特点：

1. 交互性（它可以做的就是信息的动态交互）
2. 安全性（不允许直接访问本地硬盘）
3. 跨平台性（只要是可以解析js的浏览器都可以执行，和平台无关）

## 4 与java区别

![img](/../images/JavaScript/20180921084329128.png)

## 5 作用

JavaScript 被用来改进设计、验证表单、检测浏览器、创建cookies，等等。JavaScript 是因特网上最流行的脚本语言，并且可在所有主要的浏览器中运行。

在目前学习阶段只要记住最常用的二个：（1）动态修改html及css代码 （2）验证表单

# 书写位置

HTML 中的脚本必须位于 < script> 与 < /script> 标签之间。

脚本可被放置在 HTML 页面的 < body> 和 < head> 部分中。

## 内嵌式：

理论上js可以书写在页面的任意位置。

```js
<script >
alert("内嵌式")
</script>
```

## 外链式：

首先新建一个文件类型为.js的文件，然后在该文件中写js语句，通过script标签对引入到html页面中。

````js
<script src="js文件路径地址">这里不能写js语句</script>
````

## 行内式：

直接书写在标签身上，是一个简写的事件，所以又称之为事件属性

```js
onclick单击事件
<input type="button" value="点我呀!" onclick="alert('点我干啥!^6^');">
<button onclick="alert('恭喜你,中 500 万.');">点我呀!</button>
```

# 输出

JavaScript 没有任何打印或者输出的函数。

JavaScript 可以通过不同的方式来输出数据：

- 使用 **window.alert()** 弹出警告框。
- 使用 **document.write()** 方法将内容写到 HTML 文档中。
- 使用 **innerHTML** 写入到 HTML 元素。
- 使用 **console.log()** 写入到浏览器的控制台。

# 语法

## javascipt 字面量

在编程语言中，一个字面量是一个常量，如 3.14。

**数字（Number）字面量** 可以是整数或者是小数，或者是科学计数(e)；

**字符串（String）字面量** 可以使用单引号或双引号 ；

**表达式字面量** 用于计算；

**数组（Array）字面量** 定义一个数组；

**对象（Object）字面量** 定义一个对象；

**函数（Function）字面量** 定义一个函数

```js
function myFunction(a, b) { return a * b;}
```

## JavaScript 变量

在编程语言中，变量用于存储数据值。JavaScript 变量的生命期从它们被声明的时间开始。

局部变量会在函数运行以后被删除。

全局变量会在页面关闭后被删除。

JavaScript 使用关键字 **var** 来定义变量， 使用等号来为变量赋值：

`````js
var 变量名称 = 存储的数据; (variable 变量)
数值型：var i = 1;	var d = 2.35;
字符串：var str = "用心学习";
布尔型：var b = true;
`````

![img](/../images/JavaScript/1470709911288582.gif)

##  JavaScript 操作符

### **算术运算符**

````js
+	-	*	/	%	++	--
````

注意：

1. 由于js中的小数和整数都是number类型，不存在类似整数除以整数还是整数的结论。
2. 字符串和其他的数据使用+号运算，会连接成一个新的字符串。
3. 字符串使用除了+以外的运算符：如果字符串本身是一个数字，那么会自动转成number进行运算
   ，否则就会返回一个NaN的结果，表示这不是一个数字。NaN：not a number

### **关系（比较）运算符**

```js
>		>=		<		<=  	!=		
==	等于（只比较内容）	===	恒等于（比较内容的同时还要比较数据类型）
注意：关系运算符返回的结果只有两个：true / false
```

### **算术运算符**

````js
+	-	*	/	%	++	--
````

注意：

1. 由于js中的小数和整数都是number类型，不存在类似整数除以整数还是整数的结论。
2. 字符串和其他的数据使用+号运算，会连接成一个新的字符串。
3. 字符串使用除了+以外的运算符：如果字符串本身是一个数字，那么会自动转成number进行运算
   ，否则就会返回一个NaN的结果，表示这不是一个数字。NaN：not a number

### **关系（比较）运算符**

```js
>		>=		<		<=  	!=		
==	等于（只比较内容）	===	恒等于（比较内容的同时还要比较数据类型）
注意：关系运算符返回的结果只有两个：true / false
```

### **逻辑运算符**

````js
&&	 	与		true&&false		====>false
|| 		或		true||false			====>true
！ 		非		!true				====>false
false（理解）：false,  0,  null,  undefined 
true（理解）：true, 非0,  非null,  非undefined
````

### **三元运算符：**

````js
条件？表达式1：表达式2
如果条件为true，返回表达式1的结果
如果条件为false，返回表达式2的结果
````

## JavaScript 数据类型：

### 类型介绍：

````js
数值型：number
字符串：string（凡是引号包裹起来的内容全部都是字符串）
布尔：boolean（true、false）
对象类型：object（特殊取值null）
空：null
未定义型：undefined
JavaScript 有多种数据类型：数字，字符串，数组，对象等等：

var length = 16;                                  // Number 通过数字字面量赋值 
var points = x * 10;                              // Number 通过表达式字面量赋值 
var lastName = "Johnson";                         // String 通过字符串字面量赋值 
var cars = ["Saab", "Volvo", "BMW"];              // Array  通过数组字面量赋值 
var person = {firstName:"John", lastName:"Doe"};  // Object 通过对象字面量赋值
// Object 有两种寻址方式
name=person.lastname;
name=person["lastname"];

Undefined 和 Null
Undefined 这个值表示变量不含有值。
可以通过将变量的值设置为 null 来清空变量。
````

![img](/../images/JavaScript/1470710140220491.gif)

## JavaScript 类型转换

Number() 转换为数字， String() 转换为字符串， Boolean() 转化为布尔值。

````js
在 JavaScript 中有 5 种不同的数据类型：
- string（凡是引号包裹起来的内容全部都是字符串）
- number（凡是数字都是数值型，不区分整数和小数）
- boolean（true、false）
- object（特殊取值null）
- function

3 种对象类型：
- Object
- Date
- Array

2 个不包含任何值的数据类型：
- null
- undefined
````

### typeof操作符

typeof(value); 或者typeof value;     返回这个变量的类型. 
说明 : 同一个变量, 可以进行不同类型的数据赋值.

```js
<script type="text/javascript">
```


```js
<script type="text/javascript">
typeof "John"                 // 返回 string 
typeof 3.14                   // 返回 number
typeof NaN                    // 返回 number 
typeof false                  // 返回 boolean
typeof [ 1,2,3,4]              // 返回 object
typeof {name: 'John', age:34}  // 返回 object
typeof new Date()             // 返回 object
typeof function () {}         // 返回 function
typeof myCar                  // 返回 undefined (if myCar is not declared) 
typeof null                   // 返回 object
</script>

-------------------------------------请注意------------------------------------------------
NaN 的数据类型是 number
数组(Array)的数据类型是 object
日期(Date)的数据类型为 object
null 的数据类型是 object
未定义变量的数据类型为 undefined
如果对象是 JavaScript Array 或 JavaScript Date ，我们就无法通过 typeof 来判断他们的类型，因为都是 返回 Object。
```

### constructor 属性

**constructor** 属性返回所有 JavaScript 变量的构造函数。

````js
"John".constructor                 // 返回函数 String()  { [native code] }
(3.14).constructor                 // 返回函数 Number()  { [native code] } 
false.constructor                  // 返回函数 Boolean() { [native code] }
[1,2, 3,4].constructor              // 返回函数 Array()   { [native code] }
{name:'John', age:34}.constructor  // 返回函数 Object()  { [native code] }
new Date().constructor             // 返回函数 Date()    { [native code] }
function() {}.constructor         // 返回函数 Function(){ [native code] }

你可以使用 constructor 属性来查看对象是否为数组 (包含字符串 "Array"):
function isArray(myArray) { 
    return myArray.constructor.toString().indexOf("Array") > -1; 
}
你可以使用 constructor 属性来查看是对象是否为日期 (包含字符串 "Date"):
function isDate(myDate) { 
    return myDate.constructor.toString().indexOf("Date") > -1; 
}
````

## JavaScript 变量：

1、定义：就是存放数据的、内部可以存储任意数据

2、声明变量：3、变量命名规范：

1.	只能由字母、数字、_（下划线）、$（美元符号）组成。
2.	不能以数字开头。
3.	命名中不能出现-（js会理解成减号进行减法的操作），不能和关键字冲突。
**js是弱类型语言，不重视类型的定义，但js会根据为变量赋值的情况自定判断该变量是何种类型：**

````js
数值型：var i = 1;	var d = 2.35;
字符串：var str = "用心学习";
布尔型：var b = true;
````

## JavaScript 函数

JavaScript 语句可以写在函数内，函数可以重复引用：

### **引用一个函数**

引用一个函数= 调用函数(执行函数内的语句)。

```js
function 函数名(形式参数){函数体}
调用函数：函数名(实际参数);

function myFunction(a, b) { 
    return a * b;                                // 返回 a 乘于 b 的结果 
}
//如果函数需要传递参数、不需要指定参数的类型、直接使用变量即可
//js中出现二个重名的函数名、后者会把前面的覆盖掉
```

### 匿名函数

匿名函数是没有名字的函数

```js
function(形式参数){函数体}
调用方式：将匿名函数赋值给一个变量，通过变量名调用函数
定义函数并赋值给变量：var fn = function(形式参数){函数体}
调用函数：fn(实际参数);

//举例
<script type="text/javascript">
 
    // 匿名函数 : 没有名称的函数
    var func = function(i, u) {
        alert(i + " love " + u);
    }
 
    // 调用函数 :
   func("柳岩", "小白");//显示柳岩love小白
 
</script>
```

## JavaScript 语句

JavaScript 语句向浏览器发出的命令。语句的作用是告诉浏览器该做什么。

循环语句和语句标识符和java类似，其他需要注意的如下：

### 空格

JavaScript 会忽略多余的空格。您可以向脚本添加空格，来提高其可读性。

### 对代码行进行折行

您可以在文本字符串中使用反斜杠对代码行进行换行。下面的例子会正确地显示：        

```js
document.write("你好 \ W3Cschool!");
\不过，您不能像这样折行：       
document.write \ ("你好W3Cschool!");
```

### JavaScript 注释：

```js
单行注释：		//	注释语句		快捷键ctrl+/
多行注释：		/* 注释语句 */    快捷键ctrl+shift+/   
注意：多行注释相互不能嵌套使用，只能在多行注释里面使用单行注释！
```

## JavaScript正则表达式

正则表达式（英语：Regular Expression，在代码中常简写为regex、regexp或RE）使用单个字符串来描述、匹配一系列符合某个句法规则的字符串搜索模式。

搜索模式可用于文本搜索和文本替换。在 JavaScript 中，正则表达式通常用于两个字符串方法 : search() 和 replace()。

**search() 方法** 用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串，并返回子字符串的起始位置。

**replace() 方法** 用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子字符串。

### 使用 RegExp 对象

在 JavaScript 中，RegExp 对象是一个预定义了属性和方法的正则表达式对象。

**test() 方法**是一个正则表达式方法，用于检测一个字符串是否匹配某个模式，如果字符串中含有匹配的文本，则返回 true，否则返回 false。

**exec() 方法**是一个正则表达式方法。exec() 方法用于检索字符串中的正则表达式的匹配。该函数返回一个数组，其中存放匹配的结果。如果未找到匹配，则返回值为 null。

![image-20200707114925112](/../images/JavaScript/image-20200707114925112.png)

### 思维导图

![img](/../images/JavaScript/1470710362109508.gif)

## JavaScript 调试

### console.log() 方法

如果浏览器支持调试，你可以使用 console.log() 方法在调试窗口上打印 JavaScript 值：

### 设置断点

在调试窗口中，你可以设置 JavaScript 代码的断点。

在每个断点上，都会停止执行 JavaScript 代码，以便于我们检查 JavaScript 变量的值。

在检查完毕后，可以重新执行代码（如播放按钮）。

### debugger 关键字

**debugger** 关键字用于停止执行 JavaScript，并调用调试函数。这个关键字与在调试工具中设置断点的效果是一样的。如果没有调试可用，debugger 语句将无法工作。

````js
var x = 15 * 5;
debugger;
document.getElementbyId("demo").innerHTML = x;
````

### 主要浏览器的调试工具

通常，浏览器启用调试工具一般是按下 F12 键，并在调试菜单中选择 "Console" 。

各浏览器的步骤如下:

#### Chrome 浏览器

- 打开浏览器。
- 在菜单中选择工具。
- 在工具中选择开发者工具。
- 最后，选择 Console。

## JavaScript 表单验证

JavaScript 可用来在数据被送往服务器前对 HTML 表单中的这些输入数据进行验证。

表单数据经常需要使用 JavaScript 来验证其正确性：

- 验证表单数据是否为空？
- 验证输入是否是一个正确的email地址？
- 验证日期是否输入正确？
- 验证表单输入内容是否为数字型？

## JavaScript JSON

JSON 是用于存储和传输数据的格式。

JSON 通常用于服务端向网页传递数据 。

### 什么是 JSON?

- JSON 英文全称 **J**ava**S**cript **O**bject **N**otation
- JSON 是一种轻量级的数据交换格式。
- JSON是独立的语言 *****
- JSON 易于理解。

注意： JSON 使用 JavaScript 语法，但是 JSON 格式仅仅是一个文本。  文本可以被任何编程语言读取及作为数据格式传递。

JSON实例

````json
{"employees":[ 
    {"firstName":"John", "lastName":"Doe"}, 
    {"firstName":"Anna", "lastName":"Smith"}, 
    {"firstName":"Peter", "lastName":"Jones"} 
]} 

JSON 字符串转换为 JavaScript 对象
通常我们从服务器中读取 JSON 数据，并在网页中显示数据。
简单起见，我们网页中直接设置 JSON 字符串:
首先，创建 JavaScript 字符串，字符串为 JSON 格式的数据：
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>W3Cschool教程(w3cschool.cn)</title>
</head>
<body>

<h2>为 JSON 字符串创建对象</h2>
<p id="demo"></p>
<script>
var text = '{"employees":[' +
	'{"firstName":"John","lastName":"Doe" },' +
	'{"firstName":"Anna","lastName":"Smith" },' +
	'{"firstName":"Peter","lastName":"Jones" }]}';
obj = JSON.parse(text);
document.getElementById("demo").innerHTML =
	obj.employees[1].firstName + " " + obj.employees[1].lastName;
</script>

</body>
</html>
````

## javascript:void(0) 含义

我们经常会使用到 javascript:void(0) 这样的代码，那么在 JavaScript 中 javascript:void(0) 代表的是什么意思呢？

javascript:void(0) 中最关键的是 void 关键字， void 是 JavaScript 中非常重要的关键字，该操作符指定要计算一个表达式但是不返回值。

### href="#"与href="javascript:void(0)"的区别

**#** 包含了一个位置信息，默认的锚是**#top** 也就是网页的上端。

而javascript:void(0), 仅仅表示一个死链接。

在页面很长的时候会使用 **#** 来定位页面的具体位置，格式为：**# + id**。

如果你要定义一个死链接请使用 javascript:void(0) 。

**注意：**void()仅仅是代表不返回任何值，但是括号内的表达式还是要运行

## JavaScript 代码规范

所有的 JavaScript 项目适用同一种规范。代码规范通常包括以下几个方面:

- 变量和函数的命名规则
- 空格，缩进，注释的使用规则。
- 其他常用规范……

`````js
变量：变量名推荐使用驼峰法来命名(camelCase)
运算符：通常运算符 ( = + - * / ) 前后需要添加空格
代码缩进：通常使用 4 个空格符号来缩进代码块
           
语句规则：
简单语句:一条语句通常以分号作为结束符。
复杂语句的通用规则:
将左花括号放在第一行的结尾。
左花括号前添加一空格。
将右花括号独立放在一行。
不要以分号结束一个复杂的声明。
if (time < 20) {
    greeting = "Good day";
} else {
    greeting = "Good evening";
}
           
对象规则
对象定义的规则:
将左花括号与类名放在同一行。
冒号与属性值间有个空格。
字符串使用双引号，数字不需要。
最后一个属性-值对后面不要添加逗号。
将右花括号独立放在一行，并以分号作为结束符号。
短的对象代码可以直接写成一行:
var person = {
    firstName: "John",
    lastName: "Doe",
    age: 50,
    eyeColor: "blue"
};

每行代码字符小于 80
为了便于阅读每行字符建议小于数 80 个。
如果一个 JavaScript 语句超过了 80 个字符，建议在 运算符或者逗号后换行。

命名规则
一般很多代码语言的命名规则都是类似的，例如:
变量和函数为驼峰法（ camelCase）
全局变量为大写 (UPPERCASE )
常量 (如 PI) 为大写 (UPPERCASE )

HTML 和 CSS 的横杠(-)字符:
HTML5 属性可以以 data- (如：data-quantity, data-price) 作为前缀。
CSS 使用 - 来连接属性名 (font-size)。
注意:- 通常在 JavaScript 中被认为是减法，所以不允许使用。


下划线:
很多程序员比较喜欢使用下划线(如：date_of_birth), 特别是在 SQL 数据库中。
PHP 语言通常都使用下划线。

HTML 载入外部 JavaScript 文件
使用简洁的格式载入 JavaScript 文件 ( type 属性不是必须的):
<script src="myscript.js">
使用 JavaScript 访问 HTML 元素
一个糟糕的 HTML 格式可能会导致 JavaScript 执行错误。

使用小写文件名
大多 Web 服务器 (Apache, Unix) 对大小写敏感： london.jpg 不能通过 London.jpg 访问。
其他 Web 服务器 (Microsoft, IIS) 对大小写不敏感： london.jpg 可以通过 London.jpg 或 london.jpg 访问。
你必须保持统一的风格，我们建议统一使用小写的文件名。
`````







## Javascript案例:轮播图

```js
说明1 : script 标签需要放在 body 标签之后.

说明2 : window.setInterval(“字符串函数名称()”, 时间毫秒数);
说明3 : window.setInterval(函数名称, 时间毫秒数);
说明4 : window.setInterval(匿名函数, 时间毫秒数);            推荐使用
```

````js
<head>
    <meta charset="UTF-8">
    <title>轮播图</title>
    <style>
        div {
            width: 80%;
            margin: 50px auto;
        }
        img {
            width: 100%;
        }
    </style>
</head>
<body>
    <div class="container">
        <img src="../img/01.jpg" alt="图片">
    </div>
</body>
````

```js
//实现1：

<script>
    // 需求 : 动态获取页面中的 img 标签, 然后修改 img 标签的 src 属性.
    // 1. 获取 img 标签
    var img = document.getElementById("img");
    // alert(img);
    // 定义一个变量
    var count = 1;
    // 1.2 定义一个函数
    function changeImageSrc() {
        count++;
        img.src = "../img/0"+count+".jpg";
        // 判断
        if (count == 8) {
            count = 0;
        }
    }
    // 2. 循环切换图片
    // window.setInterval(函数, 时间毫秒); 在指定的时间毫秒间隔, 不断调用第一个参数传入的函数.
    // 调用方式一 :
    // window.setInterval("changeImageSrc()", 1000);
    // 调用方式二 :
    window.setInterval(changeImageSrc, 1000);
</script>
```

````js
//实现2：

<script>
 
    // 需求 : 动态获取页面中的 img 标签, 然后修改 img 标签的 src 属性.
    // 1. 获取 img 标签
    var img = document.getElementById("img");
    // alert(img);
 
    // 定义一个变量
    var count = 1;
 
    // 2. 循环切换图片
    // window.setInterval(匿名函数, 时间毫秒); 在指定的时间毫秒间隔, 不断调用第一个参数传入的匿名函数.
    window.setInterval(function() {
        count++;
        img.src = "../img/0"+count+".jpg";
 
        // 判断
        if (count == 8) {
            count = 0;
        }
    }, 1000);
 
</script>
````

## JavaScript事件

### 事件概述

```js
事件三要素：
1.	事件源：被监听的html元素（就是这个事件加给谁），就是某个（某些）html标签
2.	事件类型：某类动作，例如点击事件，移入移除事件，敲击键盘事件等
3.	执行指令：事件触发后需要执行的代码，一般使用函数进行封装
语法格式：事件源.事件类型=执行指令
```

### 常用事件

![img](/../images/JavaScript/20180921101943914.png)

### 举例

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件</title>
 
    <script>
        // 窗口 : window 对象提供了一个事件类型  onload 页面加载完成事件.
        // 事件源 : window事件类型 : 页面加载完成事件 (onload)  执行指令: 就是赋值的 function 函数.
        window.onload = function () {
 
            // 获取页面的 btn 按钮
            var btn = document.getElementById("btn");
            // alert(btn);
 
            // 给 btn 按钮绑定一个事件 (单击事件 onclick)
            // 事件源 : btn按钮    事件类型 : 单击事件 (onclick)  执行指令: 就是赋值的 function 函数.
            btn.onclick = function () {
                alert("恭喜你, 中了 500 万!");
            }
        }
 
    </script>
 
</head>
<body>
    <button id="btn">按钮</button>
</body>
</html>
```

# js对象

## 一、Object类型

### 概述：

  到目前为止，我们使用的引用类型最多的可能就是Object 类型了。虽然Object 的实例不具备多少功能，但对于在应用程序中的存储和传输数据而言，它是非常理想的选择。
创建Object 类型有两种。一种是使用new 运算符，一种是字面量表示法。

```js
1.使用new 运算符创建Object
        var box = new Object(); //new 方式
        box.name = '李四'; //创建属性字段
        box.age = 28; //创建属性字段
 
 2.new 关键字可以省略
        var box = Object(); //省略了new 关键字
 
3.使用字面量方式创建Object
        var box = { //字面量方式
            name : '李四', //创建属性字段
            age : 28
        };
 
4.属性字段也可以使用字符串创建
        var box = {
            'name' : '李四', //也可以用字符串形式
            'age' : 28
        };
 
5.使用字面量及传统复制方式
        var box = {}; //字面量方式声明空的对象
        box.name = '李四'; //点符号给属性复制
        box.age = 28;
 
6.两种属性输出方式
        alert(box.age); //点表示法输出
        alert(box['age']); //中括号表示法输出，注意引号
        PS：在使用字面量声明Object 对象时，不会调用Object()构造函数(Firefox 除外)。
 
7.给对象创建方法
        var box = {
            run : function () { //对象中的方法
                return '运行';
            }
        }
        alert(box.run()); //调用对象中的方法
 
8.使用delete 删除对象属性
        delete box.name; //删除属性
        在实际开发过程中，一般我们更加喜欢字面量的声明方式。因为它清晰，语法代码少，
而且还给人一种封装的感觉。字面量也是向函数传递大量可选参数的首选方式。
 
function box(obj) { //参数是一个对象
    if (obj.name != undefined) alert(obj.name); //判断属性是否存在
    if (obj.age != undefined) alert(obj.age);
}
        box({ //调用函数传递一个对象
            name : '李四',
            age : 28
        });
```

## 二、对象们

![img](/../images/JavaScript/20180921104023978.png)

### Array对象

Array对象是数组对象，跟java中的数组一个意思，但是使用语法上稍微有些区别。

Java：可以保存多种类型相同的数据。在Java中数组的长度是固定的，类型也固定的。

js：可以保存不同类型的数据，同时长度不固定。可以把其理解成Java中的ArrayList。

```js
创建空数组：var arr = new Array();
创建指定容量的数组：var arr = new Array(size);
创建数组并填充元素：var arr = new Array(a,b,c...);
创建元素数组：var arr = [a,b,c...];
```

### Date对象

```js
创建当前日期时间：var date = new Date();
创建指定日期时间：var date = new Date(毫秒值);
其中毫秒值为1970-01-01至今的时间毫秒值

年：getFullYear()			以四位数字返回年份 
月：getMonth()			    返回月份 (0 ~ 11)
日：getDate() 				返回一个月中的某一天
星期：getDay()			    返回一周中的某一天 (0 ~ 6)，0代表周日
小时：getHours() 			返回小时（0 ~ 23）
分：getMinutes() 			返回分钟（0 ~ 59）
秒：getSeconds() 			返回秒数（0 ~ 59）
毫秒值：getTime()			返回 1970 年 1 月 1 日至今的毫秒数
toLocaleString()			把Date对象转换为字符串
toLocaleDateString()		把Date对象的日期部分转换为字符串
toLocaleTimeString()		把Date对象的时间部分转换为字符串
```

### Math对象

Math对象是数学对象，是一个工具对象，因此Math对象不用使用new的方式创建，直接使用Math就可以调用对象内部的方法。

````js
Math.random() 返回 0.0 ~ 1.0 之间的随机double小数 
````

## 三、全局函数

### 转换函数

![img](/../images/JavaScript/20180921105518443.png)

`````js
全局函数：
parseInt(num); 	// 取整，不会四舍五入
Math.round(num);// 取整，会四舍五入
`````

### 编码解码函数

![img](/../images/JavaScript/20180921105850342-1594053033028.png)

```js
  <script>
 
        var str = "https://www.baidu.com?wd=编码解码函数";
 
        // encodeURI 编码字符串(资源路径)
        str = window.encodeURI(str);
        document.write(str + "<br />");
 
        // decodeURI 解码字符串
        str = window.decodeURI(str);
        document.write(str + "<br />");
 
    </script>
```

![img](/../images/JavaScript/20180921110034490.png)

## 四、BOM

### 1、概述

BOM（Browser Object Mode），浏览器对象模型，是将我们使用的浏览器抽象成对象模型，例如我们打开一个浏览器，会呈现出以下页面，通过js提供浏览器对象模型对象我们可以模拟浏览器功能。

HTML DOM树

![DOM HTML tree](/../images/JavaScript/pic_htmltree.gif)

通过可编程的对象模型，JavaScript 获得了足够的能力来创建动态的 HTML。

- JavaScript 能够改变页面中的所有 HTML 元素
- JavaScript 能够改变页面中的所有 HTML 属性
- JavaScript 能够改变页面中的所有 CSS 样式
- JavaScript 能够对页面中的所有事件做出反应

### 2、查找 HTML 元素

通常，通过 JavaScript，您需要操作 HTML 元素。

为了做到这件事情，您必须首先找到该元素。有三种方法来做这件事：

- 通过 id 找到 HTML 元素getElementsById
- 通过标签名找到 HTML 元素getElementsByTagName
- 通过类名找到 HTML 元素getElementsByClassName

### 3、HTML DOM 改变 HTML 内容

#### 改变 HTML 输出流

1. JavaScript 能够创建动态的 HTML 内容：

在 JavaScript 中，[document.write()]可用于直接向 HTML 输出流写内容。

2. 修改 HTML 内容的最简单的方法是使用 innerHTML 属性]

document.getElementById(*id*).innerHTML=*new HTML*

3. 改变 HTML 属性如需改变 HTML 元素的属性，请使用这个语法：

document.getElementById(*id*).*attribute=new value*

#### 改变CSS

如需改变 HTML 元素的样式，请使用这个语法：    

document.getElementById(*id*).style.*property*=*new style*    

### 4、HTML DOM EventListener

1. addEventListener() 方法用于向指定元素添加事件句柄。

- addEventListener() 方法添加的事件句柄不会覆盖已存在的事件句柄。
- 你可以向一个元素添加多个事件句柄。
- 你可以向同个元素添加多个同类型的事件句柄，如：两个 "click" 事件。
- 你可以向同个元素添加不同类型的事件：
- addEventListener() 方法允许你在 HTML DOM 对象添加事件监听， HTML DOM 对象如： HTML 元素, HTML 文档, window 对象。或者其他支出的事件对象如: xmlHttpRequest 对象。
- addEventListener() 方法可以更简单的控制事件（冒泡与捕获）。
- 当你使用 addEventListener() 方法时, JavaScript 从 HTML 标记中分离开来，可读性更强， 在没有控制HTML标记时也可以添加事件监听。
- 你可以使用 removeEventListener() 方法来移除事件的监听。 

````js
element.addEventListener(event, function, useCapture);
第一个参数是事件的类型 (如 "click" 或 "mousedown").
第二个参数是事件触发后调用的函数。
第三个参数是个布尔值用于描述事件是冒泡还是捕获。该参数是可选的。
注意:不要使用 "on" 前缀。 例如，使用 "click" ,而不是使用 "onclick"。

向原元素添加事件句柄
实例
当用户点击元素时弹出 "Hello World!" :
element.addEventListener("click", function(){ alert("Hello World!"); });

向同一个元素中添加多个事件句柄
addEventListener() 方法允许向同个元素添加多个事件，且不会覆盖已存在的事件：
实例
element.addEventListener("click", myFunction); 
element.addEventListener("click", mySecondFunction); 

你可以向同个元素添加不同类型的事件：
实例
element.addEventListener("mouseover", myFunction); 
element.addEventListener("click", mySecondFunction); 
element.addEventListener("mouseout", myThirdFunction);

向 Window 对象添加事件句柄
addEventListener() 方法允许你在 HTML DOM 对象添加事件监听， HTML DOM 对象如： HTML 元素, HTML 文档, window 对象。或者其他支出的事件对象如: xmlHttpRequest 对象。
实例
当用户重置窗口大小时添加事件监听：
window.addEventListener("resize", function(){ 
    document.getElementById("demo").innerHTML = sometext; 
});

传递参数
当传递参数值时，使用"匿名函数"调用带参数的函数：
实例
element.addEventListener("click", function(){ myFunction(p1, p2); });

事件冒泡或事件捕获？
事件传递有两种方式：冒泡与捕获。
事件传递定义了元素事件触发的顺序。 如果你将 <p> 元素插入到 <div> 元素中，用户点击 <p> 元素, 哪个元素的 "click" 事件先被触发呢？
在冒泡中，内部元素的事件会先被触发，然后再触发外部元素，即： <p> 元素的点击事件先触发，然后会触发 <div> 元素的点击事件。
在捕获中，外部元素的事件会先被触发，然后才会触发内部元素的事件，即： <div> 元素的点击事件先触发 ，然后再触发 <p> 元素的点击事件。
addEventListener() 方法可以指定 "useCapture" 参数来设置传递类型：

removeEventListener() 方法
removeEventListener() 方法移除由 addEventListener() 方法添加的事件句柄:
实例
element.removeEventListener("mousemove", myFunction);
````

### 5、HTML DOM 元素

在文档对象模型 (DOM) 中，每个节点都是一个对象。DOM 节点有三个重要的属性，分别是：

1. nodeName : 节点的名称
2. nodeValue ：节点的值
3. nodeType ：节点的类型

#### **创建新的 HTML 元素**

```js
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>W3Cschool教程(w3cschool.cn)</title>
</head>
<body>

<div id="div1">
<p id="p1">这是一个段落。</p>
<p id="p2">这是另一个段落。</p>
</div>
<script>
var para=document.createElement("p");
var node=document.createTextNode("这是一个新段落。");
para.appendChild(node);
var element=document.getElementById("div1");
element.appendChild(para);
</script>

</body>
</html>
```

#### **删除已有的 HTML 元素**

```js
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>W3Cschool教程(w3cschool.cn)</title>
</head>
<body>

<div id="div1">
	<p id="p1">这是一个段落。</p>
	<p id="p2">这是另一个段落。</p>
</div>
<script>
var parent=document.getElementById("div1");
var child=document.getElementById("p1");
parent.removeChild(child);
</script>

</body>
</html>
```


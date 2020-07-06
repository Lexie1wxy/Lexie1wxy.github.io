---
title: CSS
date: 2020-07-05 16:10:51
tags: [前端] [CSS]
categories: 
- web前端
- CSS
typora-root-url: ../_posts
---

# 前言

Html和CSS、JavaScript的关系，学习web前端开发基础技术需要掌握：HTML、CSS、JavaScript语言。下面我们就来了解下这三门技术都是用来实现什么的：

1. HTML是网页内容的载体，是名词。内容就是网页制作者放在页面上想要让用户浏览的信息，可以包含文字、图片、视频等。
2. CSS样式是表现。就像网页的外衣，是形容词。比如，标题字体、颜色变化，或为标题加入背景图片、边框等。所有这些用来改变内容外观的东西称之为表现。
3. JavaScript是用来实现网页上的特效效果，是动词。如：鼠标滑过弹出下拉菜单。或鼠标滑过表格的背景颜色改变。还有焦点新闻（新闻图片）的轮换。可以这么理解，有动画的，有交互的一般都是用JavaScript来实现的。

# CSS定义

层叠样式表全称为“层叠样式表 (Cascading Style Sheets)”，它主要是用于定义HTML内容在浏览器内的显示样式，如文字大小、颜色、字体加粗等。属性和属性值用冒号分隔开，以分号结尾(这些符号都是英文的)。

使用CSS样式的一个好处是通过定义某个样式，可以让不同网页位置的文字有着统一的字体、字号或者颜色等。

## CSS的引入方式

从CSS 样式代码插入的形式来看基本可以分为：内联式、嵌入式和外部式三种

## 内联式css样式

就是把css代码直接写在现有的HTML标签中，如下面代码：

```css
<p style="color:red">这里文字是红色。</p>

<!-- css样式代码要写在style=""双引号中，如果有多条css样式代码设置可以写在一起，分号隔开。如下代码：-->
<p style="color:red;font-size:12px">这里文字是红色。</p>
```

## 嵌入式css样式，

就是可以把css样式表放到head中用<style type="text/css"></style>标签包裹起来。如下面代码实现把三个<span>标签中的文字设置为红色。

嵌入式css样式必须写在<style></style>之间，并且一般情况下嵌入式css样式写在<head></head>之间。

```css
<head>
    ...
    <style type="text/css">
        color:red;
        ...此处写CSS样式
    </style>
</head>
```

## 外部式css样式

外联式：就是把css代码写一个单独的外部文件中，这个css样式文件以“.css”为扩展名，在<head>内（注意不是在<style>标签内）使用<link>标签将css样式文件链接到HTML文件内，如下面代码：

```css
<link href="base.css" rel="stylesheet" type="text/css" />
```

注意：
1、css样式文件名称以有意义的英文字母命名，如 main.css。
2、rel="stylesheet" ，type="text/css" 是固定写法不可修改。
3、<link>标签位置一般写在<head>标签之内。

如果非要写在<style>标签，可以这样

```css
<head>
    ...
    <style type="text/css">
        @import "My.css"; 此处注意.css文件的路径
    </style>
</head>
```

## 样式的应用顺序：

- 行内样式优先级最高
- 针对相同的样式属性，不同的样式属性将以合并的方式呈现
- 相同样式并且相同属性，呈现方式在<head>中的顺序决定，后面会覆盖前面属性
- !important 指定样式规则应用最优先

# CSS选择器

## 定义

CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明，形式如下：

```css
selector {property: value;property: value;property: value;property: value;}
```

在{}之前的部分就是“选择器”，“选择器”指明了{}中的“样式”的作用对象，也就是“样式”作用于网页中的哪些元素

## 类型

### 基本选择器

#### 1 标签选择器

标签选择器其实就是html代码中的标签。如的<html>、<body>、<h1>、<p>、<img>。

例如下面代码：

```css
<html>
<head>
<style type="text/css">
html {color:black;}
h1 {color:blue;}
h2 {color:silver;}
</style>
</head>

<body>
<h1>这是 heading 1</h1>
<h2>这是 heading 2</h2>
<p>这是一段普通的段落。</p>
</body>
</html>
```

例如，如果您想把很多元素显示为灰色，可以使用类似如下的规则：

```css
body, h2, p, table, th, td, pre, strong, em 
{font: 28px Verdana; color: white; background: black;}
```

#### 2 类选择器

匹配所有class属性中包含info的元素，（类名不能以数字开头，类名要区分大小写。）

**在 CSS 中，类选择器以一个点号显示：**

```css
.类名 {text-align: center}
```

注意：
1、英文圆点开头
2、其中类选器名称可以任意起名（但不要起中文噢）
使用方法：

第一步：使用合适的标签把要修饰的内容标记起来，如下：

第二步：使用class="类选择器名称"，为标签设置一个类，如下：

第三步：设置类选器css样式，如下：

```css
.stress{color:red;}/*类前面要加入一个英文圆点*/
<span>胆小如鼠</span>
<span class="stress">胆小如鼠</span>
```

#### 3 ID选择器

使用id属性来调用样式，在一个网页中id值唯一（是W3C规范而不是规则，不会报错）。

语法：#ID名{样式}（ID名不能以数字开头)

```css
#Mycolor {color: yellow}
<h3 id="Mycolor">H3</h3>
```

#### 4 类和ID选择器的区别

相同点：可以应用于任何元素

不同点：

1、ID选择器只能在文档中使用一次。与类选择器不同，在一个HTML文档中，ID选择器只能使用一次，而且仅一次。而类选择器可以使用多次。

```css
下面代码是正确的：
<p>三年级时，我还是一个<span class="stress">胆小如鼠</span>的小女孩，上课从来不敢回答老师提出的问题，生怕回答错了老师会批评我。就一直没有这个<span class="stress">勇气</span>来回答老师提出的问题。</p>

<!--而下面代码是错误的：-->
 <p>三年级时，我还是一个<span id="stress">胆小如鼠</span>的小女孩，上课从来不敢回答老师提出的问题，生怕回答错了老师会批评我。就一直没有这个<span id="stress">勇气</span>来回答老师提出的问题。</p>
```

2、可以使用类选择器词列表方法为一个元素同时设置多个样式。我们可以为一个元素同时设多个样式，但只可以用类选择器的方法实现，ID选择器是不可以的（不能使用 ID 词列表）。

```css
<!--下面的代码是正确的-->
.stress{
    color:red;
}
.bigsize{
    font-size:25px;
}
<p>到了<span class="stress bigsize">三年级</span>下学期时，我们班上了一节公开课...</p>

<!--下面的代码是不正确的-->
#stressid{
    color:red;
}
#bigsizeid{
    font-size:25px;
}
<p>到了<span id="stressid bigsizeid">三年级</span>下学期时，我们班上了一节公开课...</p>
```

#### 5 通用选择器

通用选择器是功能最强大的选择器，它使用一个（*）号指定，它的作用是匹配html中任意标签元素，如下使用下面代码使用html中任意标签元素字体颜色全部设置为红色：

```css
* {color:red;}
```

### 属性选择器

![image-20200705184339230](/../images/CSS/image-20200705184339230.png)

````css
1.[title] & P[title]
        设置所有具有title属性的标签元素；
        设置所有具有title属性的P标签元素。
[title]
{color: yellow;}
p[title]
    {color: yellow;}
<div title>hello</div>
<p title>hello</p>
2.[title=mk]
        设置所有title属性等于“mk”的标签元素。 
[title="mk"]
{color: yellow;}
<p title="mk">mk</p>
    
2.[title~=mk]
　　设置所有title属性具有多个空格分隔的值、其中一个值等于“mk”的标签元素。
[title~="mk"]
{color: yellow;}
  
<p title="mk Jenny">Mk</p>
<p title="Jenny mk">Mk</p>
    
 4.[title|=mk]
        设置所有title属性具有多个连字号分隔（hyphen-separated）的值、其中一个值以"mk"开头的标签元素。
        例：lang属性："en"、"en-us"、"en-gb"等等
[title|="mk"]
{color: yellow;}
  
<p title="mk-Jenny">mk</p>
 5.[title^=Nick]
        设置属性值以指定值开头的每个标签元素。
[title^="mk"]
    {color: yellow;}
<p title="mkJenny">mk</p>
    
 6.[title$=Nick]
        设置属性值以指定值结尾的每个标签元素。
[title$="mk"]
    {color: yellow;}
<p title="Jenny mk">mk</p>
    
 7.[title*=Nick]
        设置属性值中包含指定值的每个元素
[title*="mk"]
    {color: yellow;}
<p title="SmkJenny">mk</p>
````

### 组合选择器

#### 1 多元素组合选择器

同时匹配两个或多个标签，用逗号隔开

```css
p，a，div{color: yellow;}
<p>段落</p>
<a>link</a>
<div>kuai</div>
```

#### 2 后代元素选择器

 **后代选择器（descendant selector）又称为包含选择器。后代选择器可以选择作为某元素后代的元素。**

```css
匹配所有div标签里嵌套的P标签，之间用空格分隔。
div p {color: yellow;}
  
<div>
    <p>pppppp</p>
    <div>
        <p>pppppp</p>
    </div>
</div>
```

#### 3 子代元素选择器

　**与后代选择器相比，子元素选择器（Child selectors）只能选择作为某元素子元素的元素。**　

即，它不能选择多重嵌套的子标签进行样式更改，只能更改指定的嵌套位置。

```css
匹配所有div标签里嵌套的子P标签，之间用>分隔。
div > p {color: yellow;}
  
<div>
    <p>div</p>
    <p>div</p>
</div>
```

#### 4 毗邻元素选择器

　　 匹配所有紧随div标签之后的同级标签P，之间用+分隔（只能匹配一个）。

```css
div + p {color: yellow;}
  
<div>div</div>
<p>ppp</p>
```

### 伪类选择器：

它允许给html不存在的标签设置样式，比如给html中一个标签元素鼠标滑过的状态设置字体颜色：

```css
a:hover{color:red;}
这行代码会使被<a></a>标签包裹的文字内容中的“胆小如鼠”字体颜色在鼠标滑过时变为红色
```

**1. link、hover、active、visited**

-  a:link（未访问的链接状态）,用于定义了常规的链接状态。 
-  a:visited（已访问过的链接状态）,可以看出已经访问过的链接。
-  a:hover（鼠标放在链接上的状态）,用于产生视觉效果。
-  a:active（在链接上按下鼠标时的状态）。

当为链接的不同状态设置样式时，请按照以下次序规则：

- a:hover 必须位于 a:link 和 a:visited 之后
- a:active 必须位于 a:hover 之后

**2.** **before、after**

- P:before 在每个<p>元素的内容之前插入内容;
- P:after 在每个<p>元素的内容之后插入内容。

# 常用的属性

## 1. 颜色属性：

### **color**

- HEX（十六进制色：color: #FFFF00 --> 缩写：#FF0）
- RGB（红绿蓝，使用方式：color:rgb(255,255,0)或者color:rgb(100%,100%,0%)）
- RGBA（红绿蓝透明度，A是透明度在0~1之间取值。使用方式：color:rgba(255,255,0,0.5)）
- HSL（CSS3有效,H表示色调，S表示饱和度，L表示亮度，使用方式：color:hsl(360,100%,50%)）
- HSLA（和HSL相似，A表示Alpha透明度，取值0~1之间。）

### **transparent**

- 全透明，使用方式：color: transparent

### **opacity**

- 元素的透明度，语法：opacity: 0.5;
- 属性值在0.0到1.0范围内，0表示透明，1表示不透明。
- filter滤镜属性（只适用于早期的IE浏览器，语法：filter:alpha(opacity:20);）。

## 2. 字体属性:

![image-20200705203844882](/../images/CSS/image-20200705203844882.png)

###  **font-style: 用于规定斜体文本**

- normal  文本正常显示
- italic  文本斜体显示
- oblique  文本倾斜显示

###  **font-weight: 设置文本的粗细**

- normal（默认）
- bold（加粗）
- bolder（相当于<strong>和<b>标签）
- lighter （常规）
- 100 ~ 900 整百（400=normal，700=bold）

###  **font-size: 设置字体的大小**

- 默认值：medium
- <absolute-size>可选参数值：xx-small、 x-small、 small、 medium、 large、 x-large、 xx-large
- <relative-size>相对于父标签中字体的尺寸进行调节。可选参数值：smaller、 larger
- <percentage>百分比指定文字大小。
- <length>用长度值指定文字大小，不允许负值。

### **font-family：字体名称**

- 使用逗号隔开多种字体（优先级从前向后，如果系统中没有找到当前字体，则往后面寻找）

### **font：简写属性**

- 语法：font：字体大小/行高 字体;（字体要在最后）

## 3. 文本属性:

![image-20200705203626058](/../images/CSS/image-20200705203626058.png) 

###  **white-space: 设置元素中空白的处理方式**

- normal：默认处理方式。
- pre：保留空格，当文字超出边界时不换行
- nowrap：不保留空格，强制在同一行内显示所有文本，直到文本结束或者碰到br标签
- pre-wrap：保留空格，当文字碰到边界时换行
- pre-line：不保留空格，保留文字的换行，当文字碰到边界时换行

### **direction: 规定文本的方向** 

- ltr 默认，文本方向从左到右。
- rtl 文本方向从右到左。

### **text-align:** **文本的水平对齐方式** 

- left
- center
- right

### **line-height:** **文本行高**

- normal 默认

### **vertical-align: \**文本\**所在行高的垂直对齐方式**

- baseline 默认
- sub 垂直对齐文本的下标，和<sub>标签一样的效果
- super 垂直对齐文本的上标，和<sup>标签一样的效果
- top 对象的顶端与所在容器的顶端对齐
- text-top 对象的顶端与所在行文字顶端对齐
- middle 元素对象基于基线垂直对齐
- bottom 对象的底端与所在行的文字底部对齐
- text-bottom 对象的底端与所在行文字的底端对齐

###  **text-indent: 文本缩进**

###  **letter-spacing: 添加字母之间的空白**

###  **word-spacing: 添加每个单词之间的空白**

###  **text-transform: 属性控制文本的大小写**

- capitalize 文本中的每个单词以大写字母开头。
- uppercase 定义仅有大写字母。
- lowercase 定义仅有小写字母。

###  **text-overflow:** **文本溢出样式**

- clip 修剪文本。
- ellipsis 显示省略符号...来代表被修剪的文本。
- string 使用给定的字符串来代表被修剪的文本

### **text-decoration: 文本的装饰**

- none 默认。
- underline 下划线。
- overline 上划线。
- line-through 中线。

### **text-shadow：文本阴影**

- 第一个参数是左右位置
- 第二个参数是上下位置
- 第三个参数是虚化效果
- 第四个参数是颜色
- text-shadow: 5px 5px 5px #888;

### **word-wrap：自动换行**

- word-wrap: break-word;

## 4. 背景属性

![image-20200705203749036](/../images/CSS/image-20200705203749036.png)

###  **background-color:** **背景颜色**

###  **background-image 设置图像为背景**

- url("http://images.cnblogs.com/cnblogs_com/suoning/845162/o_ns.png");  图片地址

- background-image:linear-gradient(green,blue,yellow,red,black); 颜色渐变效果

###  **background-position 设置背景图像的位置坐标**

- background-position: center center; 图片置中，x轴center，y轴center
- 1px -195px  截取图片某部分，分别代表坐标x，y轴

###  **background-repeat 设置背景图像不重复平铺**

- - no-repeat 设置图像不重复，常用
  - round 自动缩放直到适应并填充满整个容器
  - space 以相同的间距平铺且填充满整个容器

### **background-attachment 背景图像是否固定或者随着页面的其余部分滚动**

###  **background 简写**

- background: url("o_ns.png") no-repeat 0 -196px;
- background: url("o_ns.png") no-repeat center bottom 15px;
- background: url("o_ns.png") no-repeat left 30px bottom 15px;

## 5. 列表属性

![image-20200705204458622](/../images/CSS/image-20200705204458622.png)

###  **list-style-type: 列表项标志的类型**

- none 去除标志
- decimal-leading-zero;  02.
- square;  方框
- circle;  空心圆
- upper-alph; & disc; 实心圆

###  **list-style-image：将图象设置为列表项标志**

###  **list-style-position：列表项标志的位置**

- inside
- outside

###  **list-style：缩写**

## 页面布局：

### 1. 边框

![image-20200705204716733](/../images/CSS/image-20200705204716733.png)

###  **border-style：边框样式**

- solid 默认，实线
- double 双线
- dotted 点状线条
- dashed 虚线

### border-color：边框颜色

###  **border-width：边框宽度**

###  **border-radius：圆角**

- 1个参数：四个角都应用
- 2个参数：第一个参数应用于 左上、右下；第二个参数应用于 左下、右上
- 3个参数：第一个参数应用于 左上；第二个参数应用于 左下、右上；第三个参数应用于右下
- 4个参数：左上、右上、右下、左下（顺时针

###  **border: 简写**

- border: 2px yellow solid;

### **box-shadow：边框阴影**

- 第一个参数是左右位置
- 第二个参数是上下位置
- 第三个参数是虚化效果
- 第四个参数是颜色
- box-shadow: 10px 10px 5px #888;

# 不常用的属性：

查看官方文档对应属性

# CSS的继承、层叠和特殊性。
## 1继承性
CSS的某些样式是具有继承性的，那么什么是继承呢？继承是一种规则，它允许样式不仅应用于某个特定html标签元素，而且应用于其后代。比如下面代码：如某种颜色应用于p标签，这个颜色设置不仅应用p标签，还应用于p标签中的所有子元素文本，这里子元素为span标签。
但注意有一些css样式是不具有继承性的。如border:1px solid red;

## 2权值

根据权值来判断使用哪个css样式。浏览器是根据权值来判断使用哪种css样式的，权值高的就使用哪种css样式。下面是权值的规则：
标签的权值为1，类选择符的权值为10，ID选择符的权值最高为100。例如下面的代码：

```css
p{color:red;} /*权值为1*/
p span{color:green;} /*权值为1+1=2*/
.warning{color:white;} /*权值为10*/
p span.warning{color:purple;} /*权值为1+1+10=12*/
#footer .note p{color:yellow;} /*权值为100+10+1=111*/
```


注意：还有一个权值比较特殊--继承也有权值但很低，有的文献提出它只有0.1，所以可以理解为继承的权值最低

## 3层叠
我们来思考一个问题：如果在html文件中对于同一个元素可以有多个css样式存在并且这多个css样式具有相同权重值怎么办？好，这一小节中的层叠帮你解决这个问题。
层叠就是在html文件中对于同一个元素可以有多个css样式存在，当有相同权重的样式存在时，会根据这些css样式的前后顺序来决定，处于最后面的css样式会被应用。
所以前面的css样式优先级就不难理解了：
内联样式表（标签内部）> 嵌入样式表（当前文件中）> 外部样式表（外部文件中）。

## 4重要性

我们在做网页代码的时，有些特殊的情况需要为某些样式设置具有最高权值，怎么办？这时候我们可以使用!important来解决。
如下代码：

```css
p{color:red!important;}
p{color:green;}
<p class="first">三年级时，我还是一个<span>胆小如鼠</span>的小女孩。</p>
```

这时 p 段落中的文本会显示的red红色。注意：!important要写在分号的前面

# CSS盒模型
## 1元素分类

在讲解CSS布局之前，我们需要提前知道一些知识，在CSS中，html中的标签元素大体被分为三种不同的类型：

块状元素、内联元素和内联块状元素。

````css
常用的块状元素有：
<div>、<p>、<h1>...<h6>、<ol>、<ul>、<dl>、<table>、<address>、<blockquote> 、<form>
常用的内联元素有：
<a>、<span>、<br>、<i>、<em>、<strong>、<label>、<q>、<var>、<cite>、<code>
常用的内联块状元素有：
<img>、<input>
````

## 2元素分类--块级元素

什么是块级元素？在html中< div>、 < p>、< h1>、< form>、< ul> 和 < li>就是块级元素。设置display:block就是将元素显示为块级元素。如下代码就是将行内元素a转换为块状元素，从而使用a元素具有块状元素特点。
a{display:block;}
块级元素特点：
1、每个块级元素都从新的一行开始，并且其后的元素也另起一行。（一个块级元素独占一行）
2、元素的高度、宽度、行高以及顶和底边距都可设置。
3、元素宽度在不设置的情况下，是它本身父容器的100%（和父元素的宽度一致），除非设定一个宽度。

## 3元素分类--行内元素

在html中，< span>、< a>、< label>、< input>、 < img>、 < strong> 和< em>就是典型的行内元素（inline）元素。当然块状元素也可以通过代码display:inline将元素设置为行内元素。
行内元素特点：
1、和其他元素都在一行上；
2、元素的高度、宽度、行高及顶部和底部边距不可设置；
3、元素的宽度就是它包含的文字或图片的宽度，不可改变。

## 4元素分类--内联块状元素

内联块状元素（inline-block）就是同时具备内联元素、块状元素的特点，代码display:inline-block就是将元素设置为内联块状元素。(css2.1新增)，< img>、< input>标签就是这种内联块状标签。
inline-block元素特点：
1、和其他元素都在一行上；
2、元素的高度、宽度、行高以及顶和底边距都可设置。

# CSS框模型

**CSS 框模型 (Box Model) 规定了元素框处理元素内容、[内边距]、[边框]和 [外边距]的方式。**

元素框的最内部分是实际的内容，直接包围内容的是内边距。内边距呈现了元素的背景。内边距的边缘是边框。边框以外是外边距，外边距默认是透明的，因此不会遮挡其后的任何元素。

**提示：**背景应用于由内容和内边距、边框组成的区域。

内边距、边框和外边距都是可选的，默认值是零。但是，许多元素将由用户代理样式表设置外边距和内边距。可以通过将元素的 margin 和 padding 设置为零来覆盖这些浏览器样式。这可以分别进行，也可以使用通用选择器对所有元素进行设

![image-20200705211243112](/../images/CSS/image-20200705211243112.png)

![image-20200705212214750](/../images/CSS/image-20200705212214750.png)

```css
盒模型--边框（一）
盒子模型的边框就是围绕着内容及补白的线，这条线你可以设置它的粗细、样式和颜色(边框三个属性)。
如下面代码为div来设置边框粗细为2px、样式为实心的、颜色为红色的边框：
div{
    border:2px  solid  red;
}
上面是border代码的缩写形式，可以分开写：
div{
    border-width:2px;
    border-style:solid;
    border-color:red;
}
注意：
1、border-style（边框样式）常见样式有：
dashed（虚线）| dotted（点线）| solid（实线）。
2、border-color（边框颜色）中的颜色可设置为十六进制颜色，如:
border-color:#888;//前面的#号不要忘掉。


盒模型--边框（二）
现在有一个问题，如果有想为p标签单独设置下边框，而其它三边都不设置边框样式怎么办呢？css样式中允许只为一个方向的边框设置样式：
div{border-bottom:1px solid red;}
同样可以使用下面代码实现其它三边上、右、左边框的设置：
border-top:1px solid red;
border-right:1px solid red; 
border-left:1px solid red;

盒模型--边界
元素与其它元素之间的距离可以使用边界（margin）来设置。边界也是可分为上、右、下、左。如下代码：
div{margin:20px 10px 15px 30px;}
也可以分开写：
div{
   margin-top:20px;
   margin-right:10px;
   margin-bottom:15px;
   margin-left:30px;
}
如果上下左右的边界都为10px;可以这么写：
div{ margin:10px;}
如果上下边界一样为10px，左右一样为20px，可以这么写：
div{ margin:10px 20px;}
总结一下：padding和margin的区别，padding在边框里，margin在边框外。


盒模型--填充
元素内容与边框之间是可以设置距离的，称之为填充。填充也可分为上、右、下、左。如下代码：
div{padding:20px 10px 15px 30px;}
顺序一定不要搞混。可以分开写上面代码：
div{
   padding-top:20px;
   padding-right:10px;
   padding-bottom:15px;
   padding-left:30px;
}
如果上、右、下、左的填充都为10px;可以这么写
div{padding:10px;}
如果上下填充一样为10px，左右一样为20px，可以这么写：
div{padding:10px 20px;}
```

```css
盒模型代码简写
还记得在讲盒模型时外边距(margin)、内边距(padding)和边框(border)设置上下左右四个方向的边距是按照顺时针方向设置的：上右下左。具体应用在margin和padding的例子如下：
margin:10px 15px 12px 14px;/*上设置为10px、右设置为15px、下设置为12px、左设置为14px*/
通常有下面三种缩写方法:
1、如果top、right、bottom、left的值相同，如下面代码：
margin:10px 10px 10px 10px;
可缩写为：
margin:10px;
2、如果top和bottom值相同、left和 right的值相同，如下面代码：
margin:10px 20px 10px 20px;
可缩写为：
margin:10px 20px;
3、如果left和right的值相同，如下面代码：
margin:10px 20px 30px 20px;
可缩写为：
margin:10px 20px 30px;
注意：padding、border的缩写方法和margin是一致的。
```

```css
颜色值缩写
关于颜色的css样式也是可以缩写的，当你设置的颜色是16进制的色彩值时，如果每两位的值相同，可以缩写一半。
例子1：
p{color:#000000;}
可以缩写为：
p{color: #000;}
例子2：
p{color: #336699;}
可以缩写为：
p{color: #369;}
```

# CSS布局模型(定位)

清楚了CSS 盒模型的基本概念、 盒模型类型， 我们就可以深入探讨网页布局的基本模型了。CSS包含3种基本的布局模型，用英文概括为：Flow、Layer 和 Float。
在网页中，元素有三种布局模型：
1、流动模型（Flow）
2、浮动模型 (Float)
3、层模型（Layer）

## 1流动模型（一）

流动（Flow）：自上而下。
先来说一说流动模型，流动（Flow）是默认的网页布局模式。也就是说网页在默认状态下的 HTML 网页元素都是根据流动模型来分布网页内容的。
流动布局模型具有2个比较典型的特征：


第一点，块状元素都会在所处的包含元素内自上而下按顺序垂直延伸分布，因为在默认状态下，块状元素的宽度都为100%。实际上，块状元素都会以行的形式占据位置。如右侧代码编辑器中三个块状元素标签(div，h1，p)宽度显示为100%。

第二点，在流动模型下，内联元素都会在所处的包含元素内从左到右水平分布显示。（内联元素可不像块状元素这么霸道独占一行）

## 2浮动模型（二）

块状元素这么霸道都是独占一行，如果现在我们想让两个块状元素并排显示，怎么办呢？不要着急，设置元素浮动就可以实现这一愿望。任何元素在默认情况下是不能浮动的，但可以用CSS定义为浮动，如div、p、table、img等元素都可以被定义为浮动。如下代码可以实现两个div元素一行显示。

```css
div{
    width:200px;
    height:200px;
    border:2px red solid;
    float:left;
}
<div id="div1"></div>
<div id="div2"></div>
```


注意：设置浮动的同时一定要先设置块状元素的宽度，且需要浮动的几个元素宽度加起来一定要小于容器元素的宽度。

## 3什么是层模型？
什么是层布局模型？层布局模型就像是图像软件PhotoShop中非常流行的图层编辑功能一样，每个图层能够精确定位操作，但在网页设计领域，由于网页大小的活动性，层布局没能受到热捧。但是在网页上局部使用层布局还是有其方便之处的。下面我们来学习一下html中的层布局。
如何让html元素在网页中精确定位，就像图像软件PhotoShop中的图层一样可以对每个图层能够精确定位操作。CSS定义了一组定位（positioning）属性来支持层布局模型。
层模型有三种形式：
1、绝对定位(position: absolute)
2、相对定位(position: relative)
3、固定定位(position: fixed)

```css
CSS position 属性
通过使用 position 属性，我们可以选择 4 种不同类型的定位，这会影响元素框生成的方式。

position 属性值的含义：
static
元素框正常生成。块级元素生成一个矩形框，作为文档流的一部分，行内元素则会创建一个或多个行框，置于其父元素中。
relative
元素框偏移某个距离。元素仍保持其未定位前的形状，它原本所占的空间仍保留。
absolute
元素框从文档流完全删除，并相对于其包含块定位。包含块可能是文档中的另一个元素或者是初始包含块。元素原先在正常文档流中所占的空间会关闭，就好像元素原来不存在一样。元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框。
fixed
元素框的表现类似于将 position 设置为 absolute，不过其包含块是视窗本身。
```

1，层模型--绝对定位（相对于父类）
如果想为元素设置层模型中的绝对定位，需要设置position:absolute(表示绝对定位)，这条语句的作用将元素从文档流中拖出来，然后使用left、right、top、bottom属性相对于其最接近的一个具有定位属性的父包含块进行绝对定位。如果不存在这样的包含块，则相对于body元素，即相对于浏览器窗口。
如下面代码可以实现div元素相对于浏览器窗口向右移动100px，向下移动50px。

```css
div{
    width:200px;
    height:200px;
    border:2px red solid;
    position:absolute;
    left:100px;
    top:50px;
}
<div id="div1"></div>
```

2，层模型--相对定位（相对于以前）
如果想为元素设置层模型中的相对定位，需要设置position:relative（表示相对定位），它通过left、right、top、bottom属性确定元素在正常文档流中的偏移位置。相对定位完成的过程是首先按static(float)方式生成一个元素(并且元素像层一样浮动了起来)，然后相对于以前的位置移动，移动的方向和幅度由left、right、top、bottom属性确定，偏移前的位置保留不动。
如下代码实现相对于以前位置向下移动50px，向右移动100px;

```css
#div1{
    width:200px;
    height:200px;
    border:2px red solid;
    position:relative;
    left:100px;
    top:50px;
}
<div id="div1"></div>
```

3，层模型--固定定位（相对于网页窗口）
固定住某一坐标。
fixed：表示固定定位，与absolute定位类型类似，但它的相对移动的坐标是视图（屏幕内的网页窗口）本身。由于视图本身是固定的，它不会随浏览器窗口的滚动条滚动而变化，除非你在屏幕中移动浏览器窗口的屏幕位置，或改变浏览器窗口的显示大小，因此固定定位的元素会始终位于浏览器窗口内视图的某个位置，不会受文档流动影响，这与background-attachment:fixed?属性功能相同。以下代码可以实现相对于浏览器视图向右移动100px，向下移动50px。并且拖动滚动条时位置固定不变。

```css
#div1{
    width:200px;
    height:200px;
    border:2px red solid;
    position:fixed;
    left:100px;
    top:50px;
}
<div id="div1"></div>
```

## Relative与Absolute组合使用
小伙伴们学习了12-6小节的相对定位的方法：使用position:absolute可以实现被设置元素相对于浏览器（body）设置定位以后，大家有没有想过可不可以相对于其它元素进行定位呢？答案是肯定的，当然可以。使用position:relative来帮忙，但是必须遵守下面规范：

1、参照定位的元素必须是相对定位元素的前辈元素：

```css
<div id="box1"><!--参照定位的元素-->
    <div id="box2">相对参照元素进行定位</div><!--相对定位元素-->
</div>
```

2、参照定位的元素必须加入position:relative;

```css
#box1{
    width:200px;
    height:200px;
    position:relative;        
}
```

3、定位元素加入position:absolute，便可以使用top、bottom、left、right来进行偏移定位了。

```css
#box2{
    position:absolute;
    top:20px;
    left:30px;         
}
```


这样box2就可以相对于父元素box1定位了(这里注意参照物就不是浏览器了，而可以自由设置了）



# 参考链接及其文档

https://blog.csdn.net/qiushi_1990/article/details/40260447?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase

https://www.w3cschool.cn/css/dict

https://www.w3school.com.cn/cssref/pr_class_float.asp

https://www.cnblogs.com/caoyc/p/5757005.html

官方文档

链接：https://pan.baidu.com/s/1nDuFor3KZryIjIv-4PIiHg 
提取码：x0r0
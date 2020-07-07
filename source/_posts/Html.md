---
title: Html
date: 2020-07-05 16:50:10
tags: [前端,html]
categories: 
- web前端
- Html
typora-root-url: ../_posts
---

## 前言

Html和CSS、JavaScript的关系，学习web前端开发基础技术需要掌握：HTML、CSS、JavaScript语言。下面我们就来了解下这三门技术都是用来实现什么的：
1. HTML是网页内容的载体，是名词。内容就是网页制作者放在页面上想要让用户浏览的信息，可以包含文字、图片、视频等。
2. CSS样式是表现。就像网页的外衣，是形容词。比如，标题字体、颜色变化，或为标题加入背景图片、边框等。所有这些用来改变内容外观的东西称之为表现。
3. JavaScript是用来实现网页上的特效效果，是动词。如：鼠标滑过弹出下拉菜单。或鼠标滑过表格的背景颜色改变。还有焦点新闻（新闻图片）的轮换。可以这么理解，有动画的，有交互的一般都是用JavaScript来实现的。

## HTML

HyperText Markup Language，全名为超文本标记语言，这里的**超文本**指的是**超链接**。HTML 是用来描述网页的一种语言。HTML 是一种在 Web 上使用的通用标记语言。HTML 允许你格式化文本，添加图片，创建链接、输入表单、框架和表格等等，并可将之存为文本文件，浏览器即可读取和显示，HTML文档也叫做 web 页面

ps： HTML标签不区分大小写，<h1>和<H1>是一样的，但建议小写，因为大部分程序员都以小写为准。

## 标准结构

```html
<!doctype html>     声明文档类型为 HTML5 文档
<html>         HTML根标签,元素是 HTML 页面的根元素
<head>         头标签元素包含了文档的元（meta）数据，如 <meta charset="utf-8"> 定义网页编码格式为 utf-8（由于在大部分浏览器中直接输出中文会出现乱码，所以要在头部将字符声明为UTF-8）
    <title>...</title>
    <meta>元素可提供有关页面的元信息（meta-information）,必需属性content定义与 http-equiv 或 name 属性相关的元信息
    <link>
    <style>...</style>
    <script>...</script>
</head>        
<body>         主题标签
    <h1> 元素定义一个大标题
    <p> 元素定义一个段落
    ...
</body>
</html>
```

## 各种标签

### 1 标题段落标签

```html
<!--我是一个注释-->
<body>
<h1>标题1</h1>
<h2>标题2</h2>
<h3>标题3</h3>
<h4>标题4</h4>
<h5>标题5</h5>
<h6>标题6</h6>
我是换行<br/>
我是水平线<hr/>
<p>我是一个段落</p>
<!--<p>和<br/>标签的不同是：<p>标签自动换行，并生成空白行而<br/>不会生成空白行。-->
</body>
```

### 2 文本标签及格式化

```html
<font size=“6” color="red">我是一句话</font>
<small>更小的文本</small>
<strong>重要的文本</strong>
<b>粗体文本</b>
<code>计算机代码</code>
<em>强调文本</em>
<i>斜体文本</i>
<kbd>键盘输入</kbd> 
<pre>预格式化文本</pre>
 
<abbr> （缩写）</abbr> 
<address> （联系地址，显示斜体）</address> 
<bdo> （文字方向）</bdo> 
<q>（短文本引用）</q>
<blockquote> （长文本引用）</blockquote> 
<cite> （工作的名称）</cite> 
<del> （删除的文本）</del> 
<ins> （插入的文本）</ins> 
<sub> （下标文本）</sub> 
<sup> （上标文本）</sup> 
```

### 3 链接

````html
普通的链接：<a href="http://www.example.com/">链接文本</a>
图像链接： <a href="http://www.example.com/"><img src="URL" alt="替换文本"></a>
邮件链接： <a href="mailto:webmaster@example.com">发送e-mail</a>
书签：
<a id="tips">提示部分</a>
<a href="#tips">跳到提示部分</a>
````

### 4 图片

```html
<img src="URL" alt="替换文本" height="42" width="42"/>
```

### 5 样式/区块

```html
<style type="text/css">
h1 {color:red;}
p {color:blue;}
</style>
<div>文档中的块级元素,换行，文档布局</div>
<span>文档中的内联元素，不换行，组合行内元素</span>
```

### 6 列表

```html
<ul>
    <li>无序列表</li>
    <li>无序列表</li>
    <li>无序列表</li>
</ul>
<ol>
    <li>有序列表</li>
    <li>有序列表</li>
</ol>
<dl>
  <dt>定义列表——项目 1</dt>
    <dd>描述项目 1</dd>
  <dt>定义列表——项目 2</dt>
    <dd>描述项目 2</dd>
</dl>
```

### 7 表格

```html
<table border="1">
  <tr>
    <th>表格标题</th>
    <th>表格标题</th>
  </tr>
  <tr>
    <td>表格数据</td>
    <td>表格数据</td>
  </tr>
</table>
*jyICLegw1qm
```

### 8 框架

```html
<!--iframe 用于在网页内显示网页。-->
<iframe src="url" frameborder="0" width="200" height="200"></iframe>
```

### 9 表单

```html
<!--HTML 表单用于搜集不同类型的用户输入。-->
<form action="demo_form.php" method="post/get"> 

<!--<input> 元素————最重要的表单元素。
1、type：指定input类型
2、name：为文本框命名，以备后台程序ASP 、PHP使用。
3、value：为文本输入框设置默认值。(一般起到提示作用)-->
单行文本框:<br>
<input type="text" name="text1" size="40" maxlength="50"> 
<br>

<!--单选多选框-->
<input   type="radio/checkbox"   value="值"    name="名称"   checked="checked"/>
<!--1、type:
   当type="radio"时，控件为单选框
   当type="checkbox"时，控件为复选框
2、value：提交数据到服务器的值（后台程序PHP使用）
3、name：为控件命名，以备后台程序ASP、PHP使用
4、checked：当设置checked="checked"时，该选项被默认选中-->
<input type="checkbox" name="hobby" value="sing">唱歌
<input type="checkbox" name="hobby" value="dance" checked="checked">跳舞
<input type="checkbox" name="hobby" value="basketball">打球
单选按钮：<br>
<input type="radio" name="sex" value="male" checked>Male
<br>
<input type="radio" name="sex" value="female">Female
<br>
    
submit定义用于向表单处理程序（form-handler）提交表单的按钮。<br> 
<input type="submit" value="Send">
<br>
    
密码输入框：<br>
<input type="password" name="pwd"/>
<br>
    
<button type="button" onclick="alert('Hello World!')">我是个按钮，点我!</button>
 
<input type="reset" value="重置">
</form>
```

```html
<!--HTML 表单用于搜集不同类型的用户输入。-->
<form action="demo_form.php" method="post/get"> 
<!--<datalist> 元素为 <input> 元素规定预定义选项列表。
用户会在他们输入数据时看到预定义选项的下拉列表。
<input> 元素的 list 属性必须引用 <datalist> 元素的 id 属性。-->
<input list="browsers">
<datalist id="browsers">
   <option value="Internet Explorer">
   <option value="Firefox">
   <option value="Chrome">
   <option value="Opera">
   <option value="Safari">
</datalist> 
<br>

<!--<select> 元素定义下拉列表： multiple可以多选ctrl+单击
语法：<option value="提交值">选项</option>-->
<select name="cars" multiple="multiple">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
<option value="fiat">Fiat</option>
<option value="audi">Audi</option>
</select>
<input type="submit">
 <br>
 
<!--<textarea> 元素定义多行输入字段（文本域）,cols 限制每行最多输入字符数,rows 限制输入的行数：-->
<textarea name="message" rows="10" cols="30">
The cat was playing in the garden.
</textarea>
<br>
   

</form>
```

### 10 实体

**HTML 中的预留字符必须被替换为字符实体**

![image-20200705163639943](/../images/Html/image-20200705163639943.png)
---
title: javax.annotation不可见
date: 2020-07-08 13:27:55
tags: [bug]
categories: 
- Bug
- 程序包problem
typora-root-url: ../_posts
---

### java: 程序包 javax.annotation 不可见,@Resource注解无法使用 【解决方法】

### **方法：**

这是JDK9 出现的问题，降低版本设置为JDK8问题就解决了。

1、Ctrl+Alt+s 快捷键或者（鼠标右击File，再选择Settings）进入idea设置Settings页面,更改java Compiler的jdk到1.8

2、进入Project Structure的Project和modules都改改jdk

### 欧克了


---
title: 'Error:Java不支持发行版本5'
date: 2020-07-08 13:19:42
tags: [bug]
categories: 
- Bug
- idea
typora-root-url: ../_posts
---

### Intellij idea 报错：Error : java 不支持发行版本5，如下所示

![img](../images/Error-Java%E4%B8%8D%E6%94%AF%E6%8C%81%E5%8F%91%E8%A1%8C%E7%89%88%E6%9C%AC5/20180904232438840.png)

 本地运行用的是JDK9，测试Java的Stream操作，报错应该是项目编译配置使用的Java版本不对，需要检查一下项目及环境使用的Java编译版本配置。

### 《1》

在Intellij中点击“File” -->“Project Structure”，看一下“Project”和“Module”栏目中Java版本是否与本地一致：

![img](../images/Error-Java%E4%B8%8D%E6%94%AF%E6%8C%81%E5%8F%91%E8%A1%8C%E7%89%88%E6%9C%AC5/20180904233036107.png)

![img](../images/Error-Java%E4%B8%8D%E6%94%AF%E6%8C%81%E5%8F%91%E8%A1%8C%E7%89%88%E6%9C%AC5/20180904233152909.png)

如果不一致，改成本地使用的Java版本。

### 《2》

点击“Settings”-->“Bulid, Execution,Deployment”-->“Java Compiler”，**Target bytecode version**设为本地Java版本。

![img](../images/Error-Java%E4%B8%8D%E6%94%AF%E6%8C%81%E5%8F%91%E8%A1%8C%E7%89%88%E6%9C%AC5/201809042343056.png)

### 《3》

点击“Other Setting”-->“Setting for new Project”-->“Java Compiler”，Target bytecode version设为本地Java版本。（可以在Default Settings中把Project bytecode version 一劳永逸地配置成本地Java版本

![image-20200708132242555](../images/Error-Java%E4%B8%8D%E6%94%AF%E6%8C%81%E5%8F%91%E8%A1%8C%E7%89%88%E6%9C%AC5/image-20200708132242555.png)

### 三步完成后就不报错啦！
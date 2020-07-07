---
title: maven安装
date: 2020-07-07 23:00:31
tags: [Maven]
categories: 
- 安装教程
- Maven
typora-root-url: ../_posts
---

#### 1、去官网下载bin.zip包，3.4.x版本就行，太新了有bug

http://maven.apache.org/download.cgi



#### 2、第二步，解压文件包

 1.apache-maven-3.5.2-bin.zip   直接解压到指定安装路径。

 2.apache-maven-3.5.2-src.zip   maven源码包。



####  3、第三步，配置环境变量，类似jdk环境配置

1.创建MAVEN_HOME环境变量，指向maven的安装目录。

2.并将%MAVEN_HOME%\bin追加到PATH路径中。

3.调试是否安装成功，在cmd中输入 mvn -version



#### 4、第四步，将本地仓库（jar包目录）配置到指定路径（*可以不进行配置，默认在C盘）
 在maven解压目录中，conf的目录中修改settings.xml文件（D:\maven-3.5.2\conf\settings.xml）

可以添加新的仓库路径< localRepository>D:\maven-3.5.2\repository< /localRepository>
![img](../images/maven%E5%AE%89%E8%A3%85/20180125104049378.png)



#### 5、第五步，配置中央仓库的镜像：（换成了阿里的，比较稳定）

setting.xml文件中Ctrl+R找mirrors，在里面加这个

```xml
  <mirrors>
    <mirror> 
        <id>alimaven</id> 
        <name>aliyun maven</name> 
        <url>http://maven.aliyun.com/nexus/content/groups/public/</url> 
        <mirrorOf>central</mirrorOf>         
    </mirror> 
  </mirrors>
```

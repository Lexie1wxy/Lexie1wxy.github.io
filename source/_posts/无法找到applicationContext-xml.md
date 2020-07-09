---
title: 无法找到applicationContext-*.xml
date: 2020-07-08 13:34:37
tags: [bug]
categories: 
- BUg
- 配置文件
typora-root-url: ../_posts
---

### 问题：
用Maven搭建spring、springmvc、mybatis时，运行报错：

org.springframework.beans.factory.BeanDefinitionStoreException: Could not resolve bean definition resource pattern 
[classpath:spring/applicationContext-*.xml]; nested exception is java.io.FileNotFoundException: class path resource [spring/] cannot be resolved to URL because it does not exist

意思是说： 
无法找到applicationContext-*.xml这个配置文件，因为这些文件不存在

### 解决方案

我们知道，maven在扫描java文件夹时，不会扫描其中的.xml文件，因为它默认是扫描java文件的，这样mapper.xml就会丢失而导致报错，所以我们会在pom文件中添加这样的配置：

pom.xml中添加这样的语句：

````xml
<build> 
    <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
       由于修改了默认的resource目录，导致src/main/resources的所有文件都不能被扫描，因此还要配多一个
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>
````


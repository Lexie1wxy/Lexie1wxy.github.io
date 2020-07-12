---
title: Mybatis逆向工程
date: 2020-07-10 16:58:13
tags: [Mybatis]
categories: 
- 项目
- SSM
typora-root-url: ../_posts
---

## Mybatis逆向工程简介

MyBatis逆向工程是指用数据库的表直接生成Java代码，利用MyBatis官方提供的逆向工程，可以针对单表自动生MyBatis执行所需要的代码（如pojo实体类，mapper接口和mapper.xml）。

## MAVEN配置步骤

### 1 pom.xml

**——————只需要改一下项目名和generator.xml的路径就行**

````xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>

<groupId>org.example</groupId>
<artifactId>MybatisGenerator01</artifactId>
<version>1.0-SNAPSHOT</version>

<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>

<dependencies>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.35</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis.generator</groupId>
        <artifactId>mybatis-generator-core</artifactId>
        <version>1.3.2</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.4.5</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>1.3.1</version>
    </dependency>
</dependencies>

<build>
    <pluginManagement>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
                <version>3.3</version>
            </plugin>
            <plugin>
                <groupId>org.mybatis.generator</groupId>
                <artifactId>mybatis-generator-maven-plugin</artifactId>
                <version>1.3.2</version>
                <dependencies>
                    <dependency>
                        <groupId>mysql</groupId>
                        <artifactId>mysql-connector-java</artifactId>
                        <version>5.1.35</version>
                    </dependency>
                </dependencies>
                <configuration>
                    <!--配置文件的路径-->
                    <configurationFile>src/main/resources/generatorConfig.xml</configurationFile>
                    <overwrite>true</overwrite>
                </configuration>
            </plugin>
        </plugins>
    </pluginManagement>
</build>
</project>
````



### 2 在src/main/resource目录下新建配置文件generatorConfig.xml

**————————更改表名和想要的包的路径**

`````xml
<?xml version="1.0" encoding="UTF-8"?>
        <!DOCTYPE generatorConfiguration
                PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
                "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>
    <!--导入属性配置-->
    <properties resource="generator.properties"></properties>

    <!--指定特定数据库的jdbc驱动jar包的位置-->
    <classPathEntry location="${jdbc.driverLocation}"/>

    <context id="default" targetRuntime="MyBatis3">

        <!-- optional，旨在创建class时，对注释进行控制 -->
        <commentGenerator>
            <property name="suppressDate" value="true"/>
            <property name="suppressAllComments" value="true"/>
        </commentGenerator>

        <!--jdbc的数据库连接 -->
        <jdbcConnection
                driverClass="${jdbc.driverClass}"
                connectionURL="${jdbc.connectionURL}"
                userId="${jdbc.userId}"
                password="${jdbc.password}">
        </jdbcConnection>


        <!-- 非必需，类型处理器，在数据库类型和java类型之间的转换控制-->
        <javaTypeResolver>
            <property name="forceBigDecimals" value="false"/>
        </javaTypeResolver>


        <!-- Model模型生成器,用来生成含有主键key的类，记录类 以及查询Example类
            targetPackage     指定生成的model生成所在的包名
            targetProject     指定在该项目下所在的路径
        -->
        <javaModelGenerator targetPackage="com.slx.zsxt.model"
                            targetProject="src/main/java">

            <!-- 是否允许子包，即targetPackage.schemaName.tableName -->
            <property name="enableSubPackages" value="false"/>
            <!-- 是否对model添加 构造函数 -->
            <property name="constructorBased" value="true"/>
            <!-- 是否对类CHAR类型的列的数据进行trim操作 -->
            <property name="trimStrings" value="true"/>
            <!-- 建立的Model对象是否 不可改变  即生成的Model对象不会有 setter方法，只有构造方法 -->
            <property name="immutable" value="false"/>
        </javaModelGenerator>

        <!--Mapper映射文件生成所在的目录 为每一个数据库的表生成对应的SqlMap文件 -->
        <sqlMapGenerator targetPackage="com.slx.zsxt.mapper"
                         targetProject="src/main/java">
            <property name="enableSubPackages" value="false"/>
        </sqlMapGenerator>

        <!-- 客户端代码，生成易于使用的针对Model对象和XML配置文件 的代码
                type="ANNOTATEDMAPPER",生成Java Model 和基于注解的Mapper对象
                type="MIXEDMAPPER",生成基于注解的Java Model 和相应的Mapper对象
                type="XMLMAPPER",生成SQLMap XML文件和独立的Mapper接口
        -->
        <javaClientGenerator targetPackage="com.slx.zsxt.dao"
                             targetProject="src/main/java" type="XMLMAPPER">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>

        <!--以下example为false，表示不会生成example类，否则将自动生成example类
        <table schema="" tableName="%"
               enableCountByExample="false"
               enableUpdateByExample="false"
               enableDeleteByExample="false"
               enableSelectByExample="false"
               selectByExampleQueryId="false">
        </table>-->

        <table tableName="user" domainObjectName="User"></table>
        <table tableName="userlogin" domainObjectName="UserLogin"></table>
        <table tableName="role" domainObjectName="Role"></table>
        <table tableName="student" domainObjectName="Student"></table>
    </context>
</generatorConfiguration>
`````

### 3 添加properties文件

**————————driver的路径可以在idea直接复制maven仓库里jar包的绝对路径（要改反斜线）**

````properties
jdbc.driverLocation=D:/tools/Maven/apache-maven-3.5.2-bin/repository/mysql/mysql-connector-java/5.1.35/mysql-connector-java-5.1.35.jar
jdbc.driverClass=com.mysql.jdbc.Driver
jdbc.connectionURL=jdbc:mysql://localhost:3306/examination_system?useUnicode=true&characterEncoding=utf-8&serverTimezone=UTC
jdbc.userId=root
jdbc.password=root
````

### 4 添加Maven运行查看是否成功生成

**————————Edit Configuration**           

**Parameters页面——>name填项目名——>Command line填 mybatis-generator:generate -e**

 **——> Apply——>OK**

![image-20200710174745474](../images/Mybatis%E9%80%86%E5%90%91%E5%B7%A5%E7%A8%8B/image-20200710174745474.png)

### 5 成功

**————————生成的项目结构**

![image-20200710175237234](../images/Mybatis%E9%80%86%E5%90%91%E5%B7%A5%E7%A8%8B/image-20200710175237234.png)








---
title: SSM整合
tags: [SSM]
categories: 
- 框架
- SSM
typora-root-url: ../_posts
---



## 前言：

### 搭建整合环境

原博客https://blog.csdn.net/qq_44543508/article/details/100192558

#### 整合说明

XML+注解

#### 整合的思路：

1、搭建整合的环境

2、Spring的配置搭建完成

3、再使用Spring整合SpringMVC框架

4、之后使用Spring整合MyBatis框架

5、最后spring整合mybatis框架配置事务（Spring的声明式事务管理）

#### 创建数据库和表结构语句：

```java
create database ssm;
use ssm;
create table account (
id int primary key auto_increment,
name varchar(50),
money double
);
```

#### 创建maven的工程

1. 创建Twossm父工程（打包方式选择pom，必须的）

   不勾选模块，删除src,更改pom的<packaging>标签

   <font color="red">***创建java jar、pom项目时创建maven-archetype-quickstart***</font>

   <font color="red">***创建java war项目时创建maven-archetype-webapp***</font>

2. 创建Twossm_web子模块（打包方式是war包）

   父工程下new->module->选择webapp模块创建，更改pom的<packaging>标签

3. 创建Twossm_service子模块（打包方式是jar包）

   父工程下new->module->选择quickstart模块创建，更改pom的<packaging>标签

4. 创建Twossm_dao子模块（打包方式是jar包）----同上

5. 创建Twossm_domain子模块（打包方式是jar包）

   *web依赖于service，service依赖于dao，dao依赖于domain*

6. 在Twossm_parent的pom.xml文件中引入坐标依赖
   找到对应的< properties >标签，以及< dependencies >标签，复制粘贴即可
   版本控制是在< properties >标签中控制，从坐标依赖中可以看出版本号：spring5X、MySQL5.1.44、mybatis3.4.5

7. 部署Twossm_web的项目，只要把Twossm_web项目加入到tomcat服务器中即可

   这一段后边都改了，直接创建一个工程就行，其他子模块改成包

```xml
<!--版本控制-->
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.7</maven.compiler.source>
        <maven.compiler.target>1.7</maven.compiler.target>
        <spring.version>5.0.2.RELEASE</spring.version>
        <slf4j.version>1.6.6</slf4j.version>
        <log4j.version>1.2.12</log4j.version>
        <mysql.version>5.1.44</mysql.version>
        <mybatis.version>3.4.5</mybatis.version>
    </properties>

<!--添加依赖-->
    <dependencies>
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.6.8</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aop</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-tx</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>compile</scope>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>${mysql.version}</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>servlet-api</artifactId>
            <version>2.5</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.0</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>jstl</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency> <!-- log start -->
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>${log4j.version}</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>${slf4j.version}</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>${slf4j.version}</version>
        </dependency> <!-- log end -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>${mybatis.version}</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>1.3.0</version>
        </dependency>
        <dependency>
            <groupId>c3p0</groupId>
            <artifactId>c3p0</artifactId>
            <version>0.9.1.2</version>
            <type>jar</type>
            <scope>compile</scope>
        </dependency>
    </dependencies>
```

#### 编写实体类：Twossm_domain项目

1. 首先介绍一些快捷键：

```
IDEA查找接口的实现类： ctrl + alt +B 
IDEA快速实现接口： Alt + Shift + P （很常用，基本上一实现接口就得用）
Get/Set/toString方法快捷键：Esc
自动补全返回值类型的快捷键：Ctrl + Alt+ V
快速生成语句快速生成Main()方法: psvm + 回车 （老铁，是不是更习惯main+Alt+/ ？）
快速生成输出语句: sout + 回车 (其实我想说我也喜欢syso，Alt+/ )
内容提示,代码补全键：Ctrl+Alt+空格
格式化代码：Ctrl+Alt+L
查找所有，你没看错是所有：Shift + Shift
自由切换：Ctrl+Tab
删除整行：Ctrl+X
```

2. 然后编写数据表对应的实体类

```java
package com.gx.domain;

import java.io.Serializable;

public class Account implements Serializable {
    private Integer id;
    private String name;
    private Double money;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Double getMoney() {
        return money;
    }

    public void setMoney(Double money) {
        this.money = money;
    }

    @Override
    public String toString() {
        return "Account{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", money=" + money +
                '}';
    }
}

```



#### 编写dao接口

```java
package com.gx.dao;

import com.gx.domain.Account;
import org.apache.ibatis.annotations.Insert;
import org.apache.ibatis.annotations.Select;
import org.springframework.stereotype.Repository;

import java.util.List;

public interface IAccountdao {

    public List<Account> findAll();

    public void saveAccount(Account account);
}
```



#### 编写service接口和实现类

例如：IAccountService 以及  AccountServiceImpl

```java
package com.gx.service;

import com.gx.domain.Account;

import java.util.List;

public interface AccountService {
    // 查询所有账户
    public List<Account> findAll();

    // 保存帐户信息
    public void saveAccount(Account account);
}
```

```java
package com.gx.service.Impl;

import com.gx.domain.Account;
import com.gx.service.AccountService;
import org.springframework.stereotype.Service;

import java.util.List;
@Service("accountService")
public class AccountServiceImpl implements AccountService {

    @Override
    public List<Account> findAll() {
        System.out.println("Service业务层：查询所有账户...");
        return null;
    }

    @Override
    public void saveAccount(Account account) {
        System.out.println("Service业务层：保存帐户...");
    }
}
```

到这里整合环境就搭建好了，现在开始搭建Spring的配置

## Spring框架代码的编写

### 创建resources的资源文件目录管理XML配置文件

Mark Directory as--->Resources Root

### 编写applicationContext.xml的配置文件

resources--->New--->File----->applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
	http://www.springframework.org/schema/beans/spring-beans.xsd
	http://www.springframework.org/schema/context
	http://www.springframework.org/schema/context/spring-context.xsd
	http://www.springframework.org/schema/aop
	http://www.springframework.org/schema/aop/spring-aop.xsd
	http://www.springframework.org/schema/tx
	http://www.springframework.org/schema/tx/spring-tx.xsd">

    <!--开启注解的扫描，希望处理service和dao，controller不需要Spring框架去处理-->
    <context:component-scan base-package="com.gx" >
        <!--配置哪些注解不扫描-->
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller" />
    </context:component-scan>
    
</beans>
```

记得一起加个log4j.properties配置文件

```properties
log4j.rootLogger=debug, stdout, R

log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout

# Pattern to output the caller's file name and line number.
log4j.appender.stdout.layout.ConversionPattern=%5p [%t] (%F:%L) - %m%n

log4j.appender.R=org.apache.log4j.RollingFileAppender
log4j.appender.R.File=example.log

log4j.appender.R.MaxFileSize=100KB
# Keep one backup file
log4j.appender.R.MaxBackupIndex=5

log4j.appender.R.layout=org.apache.log4j.PatternLayout
log4j.appender.R.layout.ConversionPattern=%p %t %c - %m%n
```

### 在项目中编写测试方法，进行测试

```java
package com.gx.test;

import com.gx.service.AccountService;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class TestSpring {
    @Test
    public void run1(){
        ApplicationContext ac = new ClassPathXmlApplicationContext("classpath:applicationContext.xml");
        AccountService as = (AccountService) ac.getBean("accountService");
        as.findAll();
    }
}
```

## SpringMVC框架代码的编写

### 在web.xml中配置DispatcherServlet前端控制器以及DispatcherServlet过滤器解决中文乱码

```xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns="http://java.sun.com/xml/ns/javaee"
        xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
        version="3.0">
  <display-name>Archetype Created Web Application</display-name>
    <!--配置Spring的监听器，默认只加载WEB-INF目录下的applicationContext.xml配置文件-->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    <!--设置配置文件的路径-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:applicationContext.xml</param-value>
    </context-param>
    <!--配置前端控制器-->
  <servlet>
     <servlet-name>dispatcherServlet</servlet-name>
      <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
      <!--加载springmvc.xml配置文件-->
      <init-param>
          <param-name>contextConfigLocation</param-name>
          <param-value>classpath:springmvc.xml</param-value>
      </init-param>
      <!--启动服务器，创建该servlet-->
      <load-on-startup>1</load-on-startup>
  </servlet>
    <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <!--解决中文乱码的过滤器-->
    <filter>
        <filter-name>characterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>characterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
</web-app>
```

### resources文件夹下创建springmvc.xml的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">
    <!--开启注解扫描，只扫描Controller注解-->
    <context:component-scan base-package="com.gx">
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>

    <!--配置的视图解析器对象-->
    <bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/pages/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
    <!--过滤静态资源-->
    <mvc:resources location="/css" mapping="/css/**"/>
    <mvc:resources location="/images/" mapping="/images/**"/>
    <mvc:resources location="/js/" mapping="/js/**"/>
    <!--开启SpringMVC注解的支持-->
    <mvc:annotation-driven/>
</beans>

```

### 创建jsp页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<body>
<a href="account/findAll">测试SpringMVC查询</a>
</body>
</html>
```

### 编写controller代码

```java
package com.gx.controller;

import com.gx.domain.Account;
import com.gx.service.AccountService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

import java.util.List;

@Controller
public class AccountController {

    @RequestMapping("/account/findAll")
    public String findAll(){
        System.out.println("Controller表现层：查询所有账户...");
        return "list";  //在视图解析器中配置了前缀后缀
    }
}
```

### 跳转界面jsp

WEB-INF---->pages---->list.jsp

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%--
  Created by IntelliJ IDEA.
  User: Bule
  Date: 2019/9/2
  Time: 7:32
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>

<html>
<head>
    <title>Title</title>
</head>
<body>
            <h2>查询所有的账户</h2>
          
</body>
</html>
```

### 部署Tomcat进行测试

测试成功就说明搭建好了~~~

## Spring整合SpringMVC的框架

### Spring整合SpringMVC的框架原理分析

整合成功的表现：

1. 在controller（SpringMVC）中能成功的调用service（Spring）对象中的方法。

要想在controller中调用service方法，就要注入service到controller中来，有service对象才可以调用service方法，方法是这样没有错，但是有一个问题:

就是启动Tomcat之后试想一下，在web.xml中配置有前端控制器，web容器会帮我们加载springmvc.xml配置文件，在springmvc.xml配置文件中我们配置情况是只扫描controller，别的不扫，而spring.xml文件就从头到尾没有执行过，spring中的配置扫描自然也不会去扫描，就相当于没有将spring交到IOC容器当中去。

所以，现在的解决方案就是，在启动服务器时就加载spring配置文件,怎么实现呢？这时候监听器listener就派上用场了，具体实现如下：

![img](/../images/SSM整合/20190902171005382.png)

### 在web.xml中配置ContextLoaderListener监听器

在项目启动的时候，就去加载applicationContext.xml的配置文件，在web.xml中配置ContextLoaderListener监听器（该监听器只能加载WEB-INF目录下的applicationContext.xml的配置文件）。要想加载applicationContext.xml的配置文件有两种方法

第一种（不建议）：把applicationContext.xm配置文件配置到WEB-INF目录下

第二种（强烈建议）：在web.xml中配置加载路径(方便管理和维护)

```xml
 <!--配置Spring的监听器，默认只加载WEB-INF目录下的applicationContext.xml配置文件-->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
 <!--设置配置文件的路径-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:applicationContext.xml</param-value>
    </context-param>
```

### controller中注入service对象，调用service对象方法并测试

```java
package com.gx.controller;

import com.gx.domain.Account;
import com.gx.service.AccountService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

import java.util.List;

@Controller
public class AccountController {

    @Autowired   //按类型注入
    private AccountService accountService;

    @RequestMapping("/account/findAll")
    public String findAll(Model model){
        System.out.println("Controller表现层：查询所有账户...");

        List<Account> list = accountService.findAll();
        return "list";
    }
}

```

到这里，总算是整合完了spring、springmvc，同学你还能看到这里，我也挺欣慰的哈哈，手动再给你点个赞，接下来编写MyBatis环境惹！

## MyBatis框架代码的编写

一看到Mybatis，就要想到dao，没错，MyBatis环境搭建首先是dao，搭建mybatis，之前要编写mapper映射的配置文件，其实挺麻烦的，所以选择使用注解！

### 在IAccountdao接口方法上添加注解，编写SQL语句

```java
package com.gx.dao;

import com.gx.domain.Account;
import org.apache.ibatis.annotations.Insert;
import org.apache.ibatis.annotations.Select;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository  //此注解代表这是一个持久层，用法类似@controller、@service
public interface IAccountdao {

    @Select("select * from account")
    public List<Account> findAll();
    @Insert("insert into account (name,money) value(#{name},#{money})")
    public void saveAccount(Account account);
}
```

### 创建SqlMapConfig.xml的配置文件并编写

```xml
<?xml version="1.0" encoding="UTF-8"?> <!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--mybatis配置文件-->
<configuration>
    <environments default="mysql">
        <environment id="mysql">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql:///ssm?useSSL=false&amp;serverTimezone=UTC"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </dataSource>
        </environment>
    </environments>
    <!-- 使用的是注解 -->
    <mappers>
        <!-- <mapper class="com.gx.dao.IAccountdao"/> --> <!-- 该包下所有的dao接口都可以使用 -->
        <package name="com.gx.dao"/>
    </mappers>
</configuration>
```

![img](/../images/SSM整合/20190902181214119.png)

### 创建并编写Mybatis测试方法

```java
package com.gx.test;

import com.gx.dao.IAccountdao;
import com.gx.domain.Account;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import java.io.IOException;
import java.io.InputStream;
import java.util.List;

public class TestMyBatis {

    @Test
    public void run1() throws IOException {
        Account account =new Account();
        account.setName("杜永蓝");
        account.setMoney(200d);
        // 加载配置文件
        InputStream in = Resources.getResourceAsStream("SqlMapConfig.xml");
        // 创建SqlSessionFactory对象
        SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(in);
        // 创建SqlSession对象
        SqlSession session = factory.openSession();
        // 获取到代理对象
        IAccountdao dao = session.getMapper(IAccountdao.class);

        // 保存
        dao.saveAccount(account);

        // 提交事务
        session.commit();

        // 关闭资源
        session.close();
        in.close();
    }
    
    @Test
    public void run2() throws Exception {
        InputStream in = Resources.getResourceAsStream("SqlMapConfig.xml");

        SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(in);

        SqlSession session = factory.openSession();

        IAccountdao dao = session.getMapper(IAccountdao.class);

        List<Account> list = dao.findAll();
        for (Account account: list ) {
            System.out.println(account);
        }

        session.close();
        in.close();
    }
}
```

到这Mybatis框架搭建完成；

## Spring整合MyBatis框架

### Spring整合MyBatis的框架原理分析

Spring整合MyBatis框架之前，先想一想，怎样才算整合成功呢？

其实，这和之前的spring整合springMVC的套路差不多，其实就是，Service能成功调用dao对象，能够做查询操作或者新增数据能存进数据库。

现在spring已经是在IOC容器中了，dao是一个接口，可以通过程序帮这个接口生成代理对象，我们要是可以把这个代理对象也放进IOC容器，那么service就可以拿到这个对象，之后在service中做一个注入，service从而调用dao代理对象的方法，那么我们怎么去实现dao接口生成的代理对象放入IOC容器呢？其实很简单，只需要如下操作！

**整合目的：把SqlMapConfig.xml配置文件中的内容配置到applicationContext.xml配置文件中**

### 在applicationContext.xml中配置数据库连接池

```java
    <!--Spring整合MyBatis框架-->
    <!--配置连接池-->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource" destroy-method="close">
        <property name="driverClass" value="com.mysql.cj.jdbc.Driver"/>
        <property name="jdbcUrl" value="jdbc:mysql:///ssm?useSSL=false&amp;serverTimezone=UTC"/>
        <property name="user" value="root"/>
        <property name="password" value="root"/>
    </bean>
```

### 在applicationContext.xml中配置SqlSessionFactory工厂

```java
    <!--配置SqlSessionFactory工厂-->
    <bean id="sqlSessonFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
    </bean>
```

### 在applicationContext.xml中配置IAccountdao接口所在包

因为工厂有了，SqlSession也有了，那代理谁呢，所以我们要配置IAccountdao接口所在包，告诉SqlSession去代理接口所在包中的代理，从而存到IOC容器中

```java
    <!--配置IAccountdao接口所在包-->
    <bean id="mapperScanner" class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="com.gx.dao"/>
    </bean>
```

### 小结上面的三个配置

其实，上面的操作就是**把mybatis中的配置（SqlMapConfig.xml）转移到spring中去，让它产生代理并存到IOC容器中**！

### 完善Service/Controller层代码，完善list.jsp页面

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Bule
  Date: 2019/9/2
  Time: 7:32
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" isELIgnored="false" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<html>
<head>
    <title>Title</title>
</head>
<body>
<h2>查询所有的账户</h2>
<c:forEach items="${list}" var="account">
    ${account.name}
</c:forEach>
</body>
</html>
```

### 运行测试

界面跳转成功就说明ssm框架整合成功啦！！！！！！！！！！！！！！！！！！！！！！！！

快犒劳一下自己！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

最后一步！！！！！！！！！

## spring整合mybatis框架配置事务（Spring声明式事务管理）

在整合spring、mybatis测试的时候（TestMybatis中），新增数据保存的时候会手动的提交过事务session.commit()，如果不写这一句，就会出现数据没提交的情况，因此为了完美的整合ssm，我们必须配置Spring的声明式事务管理！

### 在applicationContext.xml中配置Spring框架声明式事务管理

```xml
 <!--配置Spring框架声明式事务管理-->
    <!--配置事务管理器-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource" />
    </bean>

    <!--配置事务通知-->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <tx:attributes>
            <tx:method name="find*" read-only="true"/>
            <tx:method name="*" isolation="DEFAULT"/>
        </tx:attributes>
    </tx:advice>

    <!--配置AOP增强-->
    <aop:config>
        <aop:advisor advice-ref="txAdvice" pointcut="execution(* com.gx.service.Impl.*ServiceImpl.*(..))"/>
    </aop:config>
```

### 完善index.jsp页面

```c
<form action="account/save" method="post">
    姓名：<input type="text" name="name" /><br/>
    金额：<input type="text" name="money" /><br/>
    <input type="submit" value="保存"/><br/>
</form>
```

### 完善Service层、Controller层代码

```c
    @Override
    public void saveAccount(Account account) {
        System.out.println("Service业务层：保存帐户...");
        iaccountdao.saveAccount(account);  //调用service中的saveAccount(account)方法
    }

```

```c
    @RequestMapping("/account/save")
    public void save(Account account, HttpServletRequest request, HttpServletResponse response) throws IOException {
        accountService.saveAccount(account);
        response.sendRzedirect(request.getContextPath()+"/account/findAll");
        return;
    }

```

### 测试运行

完lalalalalala！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

### 源码、源码、源码~

链接：https://pan.baidu.com/s/1rJ5zy1cMuiHYvFHz1wFuOg 
提取码：yjx3 
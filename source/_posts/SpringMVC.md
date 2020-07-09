---
title: SpringMVC
tags: [SSM,SpringMVC]
categories: 
- 框架
- SpringMVC
typora-root-url: ../_posts
---

# SpringMVC第一天

## 第一章

### 1.1三层架构和MVC

咱们开发服务器端程序，一般都基于两种形式，一种C/S架构程序，一种B/S架构程序

使用Java语言基本上都是开发B/S架构的程序，B/S架构又分成了三层架构

#### 1.1.1 三层架构

表现层：WEB层，用来和客户端进行数据交互的。表现层一般会采用MVC的设计模型

业务层：处理公司具体的业务逻辑的

持久层：用来操作数据库的

#### 1.1.2 MVC模型

MVC全名是Model View Controller 模型视图控制器，每个部分各司其职。

Model：数据模型，JavaBean的类，用来进行数据封装。

View：指JSP、HTML用来展示数据给用户

Controller：用来接收用户的请求，整个流程的控制器。用来进行数据校验等。

![image-20200702202459954](/../images/SpringMVC/image-20200702202459954.png)

### 1.2 SpringMVC的基本概念

#### 1.2.1 SpringMVC的概述

是一种基于Java实现的MVC设计模型的请求驱动类型的轻量级WEB框架。Spring MVC属于SpringFrameWork的后续产品，已经融合在Spring Web Flow里面。Spring 框架提供了构建 Web 应用程序的全功能 MVC 模块。

使用 Spring 可插入的 MVC 架构，从而在使用Spring进行WEB开发时，可以选择使用Spring的
SpringMVC框架或集成其他MVC开发框架.

## 第二章

### 2.1 SpringMVC的入门程序步骤

![image-20200702202536795](/../images/SpringMVC/image-20200702202536795.png)

#### 2.1.1环境搭建

1. 创建webapp程序
2. 加入键值对：archetypeCatalog——intenal
3. 创建java和resource文件夹
4. 复制pom.xml文件导入依赖
5. web.xml配置Servlet前端控制器
6. resource->new->xml配置文件->spring config（文件名springmvc->是spring框架的配置文件）

#### 2.1.2项目服务器部署

1. tomcat配置server
2. Deployment->(+)->Artifact(exploded文件)->context路径配置（可以选择不配）->Apply

#### 2.1.3程序编写

1. index.jsp 

```java
<a href="hello">入门程序</a>//超链接
```

2. 控制器

```java
类：@Controller
方法：@RequestMapping(path="/hello")
```

3. 配置web.xml和springmvc.xml

#### 2.1.4流程图解

![image-20200702202625481](/../images/SpringMVC/image-20200702202625481.png)

### 2.2入门案例的分析执行流程

#### 2.2.1入门案例的分析执行流程

![image-20200702202644714](/../images/SpringMVC/image-20200702202644714.png)

1. 当启动Tomcat服务器的时候，因为配置了load-on-startup标签，所以会创建DispatcherServlet对象，就会加载springmvc.xml配置文件.
2. 开启了注解扫描，那么HelloController对象就会被创建
3. 从index.jsp发送请求，请求会先到达DispatcherServlet核心控制器，根据配置@RequestMapping注解找到执行的具体方法
4. 根据执行方法的返回值，再根据配置的视图解析器，去指定的目录下查找指定名称的JSP文件
5. Tomcat服务器渲染页面，做出响应
6. SpringMVC官方提供图形

#### 2.2.2 入门案例中的组件分析

1. 前端控制器（DispatcherServlet）
2. 处理器映射器（HandlerMapping）
3. 处理器（Handler）
4. 处理器适配器（HandlAdapter）
5. 视图解析器（View Resolver）
6. 视图（View）

### 2.3 RequestMapping注解

1. RequestMapping注解的作用是建立请求URL和处理方法之间的对应关系

2. RequestMapping注解可以作用在方法和类上

- 作用在类上：第一级的访问目录
- 作用在方法上：第二级的访问目录
- 细节：路径可以不编写 / 表示应用的根目录开始
- 细节：${ pageContext.request.contextPath }也可以省略不写，但是路径上不能写 /

3. RequestMapping的属性

- path 指定请求路径的url
- value value属性和path属性是一样的
- mthod 指定该方法的请求方式
- params 指定限制请求参数的条件
- headers 发送的请求中必须包含的请求头

## 第三章：请求参数的绑定

### 3.1绑定说明

#### 3.1.1 请求参数的绑定说明

1. 绑定机制

- 表单提交的数据都是k=v格式的 username=haha&password=123
- SpringMVC的参数绑定过程是把表单提交的请求参数，作为控制器中方法的参数进行绑定的
- 要求：提交表单的name和参数的名称是相同的

2. 支持的数据类型

- 基本数据类型和字符串类型
- 实体类型（JavaBean）
- 集合数据类型（List、map集合等）

#### 3.1,2 基本数据类型和字符串类型

1. 提交表单的name和参数的名称是相同的
2. 区分大小写

#### 3.1.3 实体类型（JavaBean）

1. 提交表单的name和JavaBean中的属性名称需要一致
2. 如果一个JavaBean类中包含其他的引用类型，那么表单的name属性需要编写成：对象.属性 例如：
   address.name

#### 3.1.4 给集合属性数据封装

JSP页面编写方式：list[0].属性

#### 3.1.5 请求参数中文乱码的解决

在web.xml中配置Spring提供的过滤器类

### 3.2 特殊情况

3.2.1 自定义类型转换器

1. 表单提交的任何数据类型全部都是字符串类型，但是后台定义Integer类型，数据也可以封装上，说明Spring框架内部会默认进行数据类型转换。

2. 如果想自定义数据类型转换，可以实现Converter的接口
   1. 注册自定义类型转换器
   2. 在springmvc.xml配置文件中编写配置 

## 第四章 注解

### 4.1 RequestParam注解

#### 4.1.1 作用

把请求中的指定名称的参数传递给控制器中的形参赋值

#### 4.1.2 属性

value：请求参数中的名称

required：请求参数中是否必须提供此参数，默认值是true，必须提供4.2 RequestBody注解

### 4.2 RequestBody注解

#### 4.2.1 作用

用于获取请求体的内容（注意：get方法不可以）

#### 4.2.2 属性

### 4.3 PathVaribale注解

#### 4.3.1 作用

 用于绑定url中的占位符。例如：请求url中 /delete/**{id}**，这个{id}就是url占位符。 url支持占位符是spring3.0之后加入的。是springmvc支持rest风格URL的一个重要标志。 

#### 4.3.2 属性

 value：用于指定url中占位符名称。

 required：是否必须提供占位符。

#### 4.3.3 REST风格URL

1. 请求路径一样，可以根据不同的请求方式去执行后台的不同方法

2. restful风格的URL优点：结构清晰\符合标准\易于理解\扩展方便

3. HTTP协议，是一个无状态协议，即所有的状态都保存在服务器端。因此，如果客户端想要操作服务器，必须通过某种手段，让服务器端发生“状态转化”（State Transfer）。而这种转化是建立在表现层之上的，所以就是 “表现层状态转化”。具体说，就是 HTTP 协议里面，四个表示操作方式的动词：GET、POST、PUT、DELETE。它们分别对应四种基本操作：**GET 用来获取资源，POST 用来新建资源，PUT 用来更新资源，DELETE 用来删除资源。**

4. restful的示例： 

   | /account/1 HTTP GET ：   | 得到 id = 1 的 account |
   | ------------------------ | ---------------------- |
   | /account/1 HTTP DELETE： | 删除 id = 1的 account  |
   | /account/1 HTTP PUT：    | 更新id = 1的 account   |
   | /account HTTP POST：     | 新增id = 1 account     |

![image-20200702202748227](/../images/SpringMVC/image-20200702202748227.png)

#### 4.3.4 基于HiddentHttpMethodFilter的示例

**作用：** 由于浏览器 form 表单只支持 GET 与 POST 请求，而DELETE、PUT 等 method 并不支持，Spring3.0 添加了一个过滤器，可以将浏览器请求改为指定的请求方式，发送给我们的控制器方法，使得支持 GET、POST、PUT 与DELETE 请求。

 **使用方法：** 第一步：在web.xml中配置该过滤器。 第二步：请求方式必须使用post请求。 第三步：按照要求提供_method请求参数，该参数的取值就是我们需要的请求方式。

### 4.4 RequestHeader注解

#### 4.4.1 作用

获取指定请求头的值

#### 4.4.2 属性

value：请求头的名称

### 4.5 CookieValue注解

#### 4.5.1 作用

用于获取指定cookie的名称的值

#### 4.5.2 属性

value：cookie的名称

### 4.6 ModelAttribute注解

#### 4.6.1 作用

出现在方法上：表示当前方法会在控制器方法执行前线执行。

出现在参数上：获取指定的数据给参数赋值。

#### 4.6.2 应用场景

当提交表单数据不是完整的实体数据时，保证没有提交的字段使用数据库原来的数据

#### 4.6.3 应用方式

根据方法是否有返回值来确定两种方式，代码在笔记上

### 4.7 SessionAttribute注解

#### 4.7.1作用

用于多次执行控制器方法间的参数共享(存入session域或者request中)

#### 4.7.2 属性

value：指定存入属性的名称

# SpringMVC第二天

看随堂笔记吧

## 异常抛出流程

![image-20200702202725180](/../images/SpringMVC/image-20200702202725180.png)

## 第四章：SpringMVC框架中的拦截器

## 4.1拦截器的概述

1. SpringMVC框架中的拦截器用于对处理器进行预处理和后处理的技术。

2. 可以定义拦截器链，连接器链就是将拦截器按着一定的顺序结成一条链，在访问被拦截的方法时，拦截器链中的拦截器会按着定义的顺序执行。

3. 拦截器和过滤器的功能比较类似，有区别

   过滤器是Servlet规范的一部分，任何框架都可以使用过滤器技术。

   拦截器是SpringMVC框架独有的。

   过滤器配置了/*，可以拦截任何资源。

   拦截器只会对控制器中的方法进行拦截。

4. 拦截器也是AOP思想的一种实现方式

5. 想要自定义拦截器，需要实现HandlerInterceptor接口。

## 4.2 HandlerInterceptor接口中的方法

1. preHandle方法是controller方法执行前拦截的方法

- 可以使用request或者response跳转到指定的页面
- return true放行，执行下一个拦截器，如果没有拦截器，执行controller中的方法。
- return false不放行，不会执行controller中的方法。

2. postHandle是controller方法执行后执行的方法，在JSP视图执行前。

- 可以使用request或者response跳转到指定的页面
- 如果指定了跳转的页面，那么controller方法跳转的页面将不会显示。

3.  postHandle方法是在JSP执行后执行

- request或者response不能再跳转页面了

# SpringMVC第三天

## 第一章：搭建整合环境

1. 搭建整合环境
2. 整合说明：SSM整合可以使用多种方式，咱们会选择XML + 注解的方式
3. 整合的思路

- 先搭建整合的环境
- 先把Spring的配置搭建完成
- 再使用Spring整合SpringMVC框架
- 最后使用Spring整合MyBatis框架
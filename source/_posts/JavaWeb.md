---
title: JavaWeb
date: 2021-04-24 10:00:57
tags: study
---

# JavaWeb



# 1、基本概念

## 1.1、前言

web开发：

- web，网页的意思
- 静态web
  - html，css
  - 提供给所有人看的数据始终不会发生变化
- 动态web
  - 淘宝，几乎是所有网站
  - 提供给所有人看的数据始终会发生变化，每个人在不同的时间，不同的地点看到的信息各不相同
  - 技术栈：Servlet/JSP，ASP，PHP

在Java中，动态的web资源开发的技术统称为JavaWeb

## 1.2、web应用程序

web应用程序：可以提供浏览器访问的程序

- a.html、b.html...多个web资源，这些web资源可以被外界访问，对外界提供服务；
- 能访问到的任何一个页面或者资源，都存在于这个世界的某一个角落的计算机上
- URL
- 这个统一的web资源会被放在同一个文件夹下，web应用程序-->Tomcat：服务器
- 一个web应用由多部份组成（静态web，动态web）
  - html，css，js
  - jsp，servlet
  - java程序
  - jar包
  - 配置文件（properties）

web应用程序编写完毕后，若想提供给外界访问：需要一个服务器来统一管理

## 1.3、静态web

- *.html，这些都是网页的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取。

![image-20210207150939976](https://raw.githubusercontent.com/acacac13/picBed/master/20210424100214.png)

- 静态web存在的缺点
  - Web页面无法动态更新，所有用户看到的都是同一个页面
    - 轮播图，点击特效：伪动态
    - JavaScript【实际开发中，用的最多】
    - VBScript
  - 无法和数据库交互（数据无法持久化，用户无法交互）

## 1.4、动态web

页面会动态展示：“Web页面的展示因人而异”

![image-20210207151438984](https://raw.githubusercontent.com/acacac13/picBed/master/20210424100221.png)

缺点

- 假如服务器的动态web资源出现了错误，我们需要重新编写我们的**后台程序**，重新发布；
  - 停机维护

优点

- Web页面可以动态更新，所有用户看到的不是同一个页面
- 可以与数据库交互（数据持久化：注册，商品信息，注册信息..）

![image-20210207151648636](https://raw.githubusercontent.com/acacac13/picBed/master/20210424100227.png)

# 2、web服务器

## 2.1、技术讲解

**ASP：**

- 微软：国内最早流行的就是ASP

- 在HTML中嵌入了VB的脚本，ASP+COM

- 在ASP开发中，基本一个页面都有几千行业务代码，页面极其混乱

- 维护成本高

- C#

- IIS

  ```html
  <h1>
      <h1><h1>
          <h1>
              <h1>
                  <h1>
          <h1>
              <%
                 System.out.println("hello")
                 %>
                  <h1>
                      <h1>
      <h1><h1>
  <h1>
  ```



**PHP：**

- PHP开发速度很快，功能很强大，跨平台，代码很简单（70%，WP）
- 无法承载大访问量的情况（局限性）



**JSP/Serlet：**

B/S：浏览器和服务器

C/S：客户端和服务器

* sun公司主推的B/S架构
* 基于Java语言的（所有大公司，或者一些开源的组件，都是用Java写的）
* 可以承载三高问题带来的影响
* 语法像ASP，ASP-->JSP，加强市场强度



## 2.2、web服务器

服务器是一种被动的操作，用来处理用户的一些请求和给用户一些响应信息



**IIS**

微软的；ASP...，Windows中自带的

**Tomacat**

![image-20210207153227878](https://raw.githubusercontent.com/acacac13/picBed/master/20210424100234.png)

面向百度编程

Tomcat是Apache 软件基金会（Apache Software Foundation）的Jakarta 项目中的一个核心项目，由[Apache](https://baike.baidu.com/item/Apache/6265)、Sun 和其他一些公司及个人共同开发而成。由于有了Sun 的参与和支持，最新的Servlet 和JSP 规范总是能在Tomcat 中得到体现，Tomcat 5支持最新的Servlet 2.4 和JSP 2.0 规范。因为Tomcat 技术先进、性能稳定，而且**免费**，因而深受Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web 应用服务器。

Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用[服务器](https://baike.baidu.com/item/服务器)，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。对于一个初学者来说，它是最佳的选择。

Tomcat 实际上运行JSP 页面和Servlet。。目前Tomcat最新版本为9.0.41**。**

# 3、Tomcat

## 3.1、安装Tomcat

## 3.2、Tomcat启动和配置

## 3.3、配置

可以配置启动的端口号

- tomcat的默认端口号为：8080
- mysql：3306
- http：80
- https：443

可以配置的主机的名称

- 默认的主机名为：localhost->127.0.0.1
- 默认网站应用存放的位置为：webapps



**高难度面试题：**

请你谈谈网站是如何进行访问的

- 1.输入一个域名；回车

- 2.检查本机的C:\Windows\System32\drivers\etc\hosts配置文件下有没有这个域名映射；

  - 有：直接返回对应的ip地址，在这个地址中，有我们需要访问的web程序，可以直接访问

    ```java
    127.0.0.1	www.xxx.com
    ```

  - 没有：去DNS服务器找，找得到的话就返回，找不到就返回找不到

![image-20210207172807129](https://raw.githubusercontent.com/acacac13/picBed/master/20210424100240.png)



## 3.4、发布一个web网站

- 将自己写的网站，放到服务器（Tomcat）中指定的web应用的文件夹（webapps）下，就可以访问了

网站应该有的结构

```java
--webapps：Tomcat服务器的web目录
    -ROOT
    -xxxx：网站的目录名
    	- WEB-INF
    		-classes：java程序
    		-lib：web应用所依赖的jar包
    		-web.xml：网站配置文件
    	- index.html：默认的首页
    	- static
    		-css
    			-style.css
    		-js
    		-img
    	- ...
```

# 4、Http

## 4.1、什么是HTTP

超文本传输协议（Hypertext Transfer Protocol，HTTP）是一个简单的请求-响应协议，它通常运行在[TCP](https://baike.baidu.com/item/TCP/33012)之上。

- 文本：html，字符串，~...
- 超文本：图片，音乐，视频，定位，地图...
- 80

Https：安全的

- 443

## 4.2、两个时代

- http1.0
  - HTTP/1.0：客户端可以与web服务器连接，只能获得一个web资源，断开连接
- http2.0
  - HTTP/1.1：客户端可以与web服务器连接，可以获得多个web资源

## 4.3、Http请求

- 客户端--发请求（Request）--服务器

百度：

```java
Request URL: https://www.baidu.com/		请求地址
Request Method: GET		get方法/post方法
Status Code: 200 OK		状态码：200
Remote Address: 36.152.44.95:443
Referrer Policy: strict-origin-when-cross-origin
```

```java
Accept:text/html
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9		语言
Cache-Control: max-age=0
Connection: keep-alive
```

### 1、请求行

- 请求行中的请求方式：GET
- 请求方式：**Get，Post**，HEAD，DELETE，PUT，TRACT...
  - get：请求能够携带的参数比较少，大小有限制，会在浏览器的URL地址栏显示数据内容，不安全，但高效
  - post：请求能够携带的参数没有限制，大小没有限制，不会在浏览器的URL地址栏显示数据内容，安全，但不高效

### 2、消息头

```java
Accept: 告诉浏览器，它所支持的数据类型
Accept-Encoding: 支持哪种编码格式	GBK	UTF-8	GB2312	ISO8859-1
Accept-Language: 告诉浏览器，它的语言环境
Cache-Control: 缓存控制 
Connection: 告诉浏览器，请求完成是断开还是保持连接
HOST：主机.../
```



## 4.4、Http响应

- 服务器--响应--客户端

```java
Cache-Control: private		缓存控制
Connection: keep-alive		连接
Content-Encoding: gzip		编码
Content-Type: text/html;charset=utf-8	类型
```

### 1、响应体

```java
Accept: 告诉浏览器，它所支持的数据类型
Accept-Encoding: 支持哪种编码格式	GBK	UTF-8	GB2312	ISO8859-1
Accept-Language: 告诉浏览器，它的语言环境
Cache-Control: 缓存控制 
Connection: 告诉浏览器，请求完成是断开还是保持连接
HOST：主机.../
Reflush：告诉客户端，多久刷新一次
Location：让网页重新定位
```

### 2、响应状态码（重点）

200：请求响应成功	200

3**：请求重定向

- 重定向：重新到我给你的新位置去

4**：找不到资源    404

- 资源不存在

5**：服务器代码错误    500    502网关错误



**常见面试题：**

当你的浏览器中地址栏输入地址并回车的瞬间到页面能够展示回来，经历了什么？



# 5、Maven

自动导入和配置jar包

## 5.1、Maven项目架构管理工具

目前用来就是方便导入jar包

Maven的核心思想：约定大于配置

- 有约束，不要去违反

Maven会规定好你该如何去编写java代码，必须要按照这个规范来

## 5.2、下载和安装Maven



## 5.3、配置环境变量

![image-20210208094435345](https://raw.githubusercontent.com/acacac13/picBed/master/20210424100250.png)

![image-20210208094511783](https://raw.githubusercontent.com/acacac13/picBed/master/20210424100254.png)

## 5.4、阿里云镜像

- 镜像：mirrors
  - 作用：加速下载
- 国内建议使用阿里云的镜像

```xml
      <mirror>
        <id>nexus-aliyun</id>
        <mirrorOf>*</mirrorOf>
        <name>Nexus aliyun</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public</url>
     </mirror> 
```

## 5.5、本地仓库

在本地的仓库，远程仓库

**建立一个本地仓库：**localRepository

```xml
<localRepository>D:\IDEA2020\env\apache-maven-3.6.1\maven-repository</localRepository>
```

## 5.6、在IDEA中使用Maven

![image-20210208095602078](https://raw.githubusercontent.com/acacac13/picBed/master/20210424100300.png)

标记文件夹功能

![image-20210208100930346](https://raw.githubusercontent.com/acacac13/picBed/master/20210424100307.png)

配置tomcat

![image-20210208101512412](https://raw.githubusercontent.com/acacac13/picBed/master/20210424100312.png)

![image-20210208102417683](https://raw.githubusercontent.com/acacac13/picBed/master/20210424100318.png)

# 6、Servlet

## 6.1、Servlet简介

- Servlet就是sun公司开发动态web的一门技术
- sun公司在这些API中提供了一个接口叫做：Servlet，如果你像开发一个Servlet程序，只需要完成两个小步骤：
  - 编写一个类，实现Servlet接口
  - 把开发好的java类部署到web服务器中

**把实现了Servlet接口的java程序叫做Servlet**

## 6.2、HelloServlet

Servlet接口在sun公司有两个默认的实现类：HttpServlet，GenericServlet

1.构建一个普通的Maven项目，删掉里面的src目录，在里面建立module，这个空工程就是Maven主工程

2.关于Maven父子工程的理解：

父项目中会有

```xml
<modules>
    <module>servlet-01</module>
</modules>
```

子项目中会有

```xml
<parent>
  <artifactId>javaweb-02-servlet</artifactId>
  <groupId>org.example</groupId>
  <version>1.0-SNAPSHOT</version>
</parent>
```

父项目的java子项目可以直接使用

3.Maven环境优化

- 修改web.xml为最新的
- 将maven的结构搭建完整

4.编写一个Servlet程序

- 编写一个普通类

- 实现Servlet接口，这里继承HttpServlet

  ```java
  public class HelloServlet extends HttpServlet {
  
      //由于get和post只是请求实现的不同方式，可以相互调用，业务逻辑都一样
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
  
          PrintWriter writer = resp.getWriter();
          writer.println("Hello Servlet!");
      }
  
      @Override
      protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          doGet(req,resp);
      }
  }
  ```

5.编写Servlet的映射

​	为什么需要映射：我们写的是java程序，但是要通过浏览器访问，而浏览器需要连接web服务器，使用我们需要在web服务中注册我们写的Servlet，还需给他一个浏览器能够访问的路径；

```xml
<!--注册Servlet-->
<servlet>
    <servlet-name>hello</servlet-name>
    <servlet-class>com.acacac.servlet.HelloServlet</servlet-class>
</servlet>
<!--Servlet的请求路径-->
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

6.配置Tomcat

​	注意：配置项目发布的路径即可

7.启动测试

## 6.3、Servlet原理

Servlet是由Web服务器调用，web服务器在受到浏览器请求后，会

![image-20210214091314342](https://raw.githubusercontent.com/acacac13/picBed/master/20210424100325.png)

## 6.4、Mapping问题

1.一个Servlet可以指定一个映射路径

```xml
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

2.一个Servlet可以指定多个映射路径

3.一个Servlet可以指定通用映射路径

4.指定一些后缀或者前缀等等
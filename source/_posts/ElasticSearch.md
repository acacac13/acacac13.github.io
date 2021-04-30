---
title: ElasticSearch
date: 2021-04-30 17:37:22
tags:
  - 搜索
  - ElasticSearch
  - Kibana
categories: Java后端
---

# ElasticSearch概述

Elasticsearch是一个基于Apache Lucene(TM)的开源的==高扩展==的==分布式全文检索引擎==，无论在开源还是专有领域，Lucene可以被认为是迄今为止最先进、性能最好的、功能最全的搜索引擎库。 
但是，Lucene只是一个库。想要发挥其强大的作用，你需使用Java并要将其集成到你的应用中。Lucene非常复杂，你需要深入的了解检索相关知识来理解它是如何工作的。 
Elasticsearch也是使用Java编写并使用Lucene来建立索引并实现搜索功能，但是它的目的是通过简单连贯的==RESTful API==让全文搜索变得简单并隐藏Lucene的复杂性。 
不过，Elasticsearch不仅仅是Lucene和全文搜索引擎，它还提供：

- 分布式的实时文件存储，每个字段都被索引并可被搜索
- 实时分析的分布式搜索引擎
- 可以扩展到上百台服务器，处理PB级结构化或非结构化数据

而且，所有的这些功能被集成到一台服务器，你的应用可以通过简单的RESTful API、各种语言的客户端甚至命令行与之交互。上手Elasticsearch非常简单，它提供了许多合理的缺省值，并对初学者隐藏了复杂的搜索引擎理论。它开箱即用（安装即可使用），只需很少的学习既可在生产环境中使用。Elasticsearch在Apache 2 license下许可使用，可以免费下载、使用和修改。 
随着知识的积累，你可以根据不同的问题领域定制Elasticsearch的高级特性，这一切都是可配置的，并且配置非常灵活。

# ES和solr的差别

## Solr简介

Solr是Apache下的一个顶级开源项目，采用Java开发，它是基于Lucene的全文搜索服务器。Solr提供了比Lucene更为丰富的查询语言，同时实现了可配置、可扩展，并对索引、搜索性能进行了优化

Solr可以独立运行，运行在/etty、Tomcat等这些Servlet容器中，Solr索引的实现方法很简单，==用POST方法向Solr服务器发送一个描述Field 及其内容的XML文档，Solr根据xml文档添加、删除、更新索引==Solr搜索只需要发送HTTP GET请求，然后对Solr返回Xml、json等格式的查询结果进行解析，组织页面布局。Solr不提供构建UI的功能，Solr提供了一个管理界面，通过管理界面可以查询Solr的配置和运行情况。

Solr是基于lucene开发企业级搜索服务器，实际上就是封装了lucene。

Solr是一个独立的企业级搜索应用服务器，它对外提供类似于Web-service的API接口。用户可以通过http请求，向搜索引擎服务器提交一定格式的文件，生成索引;也可以通过提出查找请求，并得到返回结果。

## Lucene简介

 Lucene是apache软件基金会4 jakarta项目组的一个子项目，是一个开放源代码的全文检索引擎工具包，但它不是一个完整的全文检索引擎，而是一个全文检索引擎的架构，提供了完整的查询引擎和索引引擎，部分文本分析引擎（英文与德文两种西方语言)。Lucene的目的是为软件开发人员提供一个简单易用的工具包，以方便的在目标系统中实现全文检索的功能，或者是以此为基础建立起完整的全文检索引擎。Lucene是一套用于全文检索和搜寻的开源程式库，由Apache软件基金会支持和提供。Lucene提供了一个简单却强大的应用程式接口，能够做全文索引和搜寻。==在Java开发环境里Lucene是一个成熟的免费开源工具。就其本身而言，Lucene是当前以及最近几年最受欢迎的免费Java信息检索程序库。==人们经常提到信息检索程序库，虽然与搜索引擎有关，但不应该将信息检索程序库与搜索引擎相混淆。

Lucene是一个全文检索引擎的架构。那什么是全文搜索引擎?

全文搜索引擎是名副其实的搜索引擎，国外具代表性的有Google、Fast/AlTheWeb、AltaVista、Inktomi、Teoma、WiseNut等，国内著名的有百度(Baidu )。它们都是通过从互联网上提取的各个网站的信息（以网页文字为主)而建立的数据库中，检索与用户查询条件匹配的相关记录，然后按一定的排列顺序将结果返回给用户，因此他们是真正的搜索引擎。

从搜索结果来源的角度，全文搜索引擎又可细分为两种，一种是拥有自己的检索程序(Ilndexer )，俗称"蜘蛛" ( Spider )程序或"机器人"( Robot )程序，并自建网页数据库，搜索结果直接从自身的数据库中调用，如上面提到的7家引擎;另一种则是租用其他引擎的数据库，并按自定的格式排列搜索结果，如Lycos引擎。

## Elasticsearch和Solar比较

- 当单纯的对已有数据进行搜索时，Solr更快
- 当实时建立索引时，Solr会产生io阻塞，查询性能较差，Elasticsearch具有明显的优势
- 随着数据量的增加，Solr的搜索效率会变得更低，而Elasticsearch却没有明显的变化

**Elasticsearch vs Solr总结**

1. es基本是开箱即用（解压就能用），非常简单。Solr安装略微复杂一丢丢!
2. Solr利用Zookeeper进行分布式管理，而Elasticsearch自身带有分布式协调管理功能。
3. Solr支持更多格式的数据，比如JSON、XML、CSV，而Elasticsearch 仅支持json文件格式。
4. Solr官方提供的功能更多，而Elasticsearch本身更注重于核心功能，高级功能多有第三方插件提供，例如图形化界面需要kibana友好支撑
5. Solr查询快，但更新索引时慢（即插入删除慢），用于电商等查询多的应用;
   - ES建立索引快（即查询慢），==即实时性查询快==，用于facebook新浪等搜索。
   - Solr是传统搜索应用的有力解决方案，但Elasticsearch更适用于新兴的实时搜索应用。
6. Solr比较成熟，有一个更大，更成熟的用户、开发和贡献者社区，而Elasticsearch相对开发维护者较少，更新太快，学习使用成本较高。

# ElasticSearch安装

声明：JDK1.8，最低要求！ElasticSearch客户端，界面工具！

> 下载

官网：https://www.elastic.co/

> window下安装

1. 解压就可以使用了

   ![解压目录](https://gitee.com/acacac13/images/raw/master/image-20210430190355544.png)

2. 熟悉目录

   ```bash
   bin 启动文件
   config 配置文件
   	log4j	日志配置文件
   	jvm.options	java 虚拟机相关的配置
   	elasticsearch.yml	elasticsearch 的配置文件	默认9200端口 跨域
   lib		相关jar包
   logs	日志
   modules	功能模块
   plugins	插件
   ```

3. 启动

![启动](https://gitee.com/acacac13/images/raw/master/image-20210430191321976.png)

![访问9200端口](https://gitee.com/acacac13/images/raw/master/image-20210430191459782.png)

> 安装可视化界面 es head的插件

1. 下载

2. 启动

   ```bash
   npm install
   npm run start
   ```

   

3. 连接测试发现存在跨域问题：配置es

   ```bash
   http.cors.enabled: true
   heep.cors.allow-origin: "*"
   ```

   

4. 重启es服务器，然后再次连接

![](https://gitee.com/acacac13/images/raw/master/20210430194321.png)

把es当作一个数据库（可以建立索引（库），文档（库中的数据））

> 这个head当作是一个数据展示工具，后面的查询使用Kibana


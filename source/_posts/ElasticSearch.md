---
title: ElasticSearch
date: 2021-04-30 17:37:22
index_img: ../picture/20210814145231.jpg
banner_img: ../picture/20210814145231.jpg
tags:
  - 搜索
  - ElasticSearch
  - Kibana
categories: Java后端
---

# ElasticSearch概述

`Elasticsearch`是一个基于`Apache Lucene(TM)`的开源的**高扩展**的**分布式全文检索引擎**，无论在开源还是专有领域，Lucene 可以被认为是迄今为止最先进、性能最好的、功能最全的搜索引擎库。 
但是，Lucene只是一个库。想要发挥其强大的作用，你需使用Java并要将其集成到你的应用中。Lucene 非常复杂，你需要深入的了解检索相关知识来理解它是如何工作的。 
`Elasticsearch`也是使用 Java 编写并使用 Lucene 来建立索引并实现搜索功能，但是它的目的是通过简单连贯的`RESTful API`让全文搜索变得简单并隐藏 Lucene 的复杂性。 
不过，`Elasticsearch`不仅仅是 Lucene 和全文搜索引擎，它还提供：

- 分布式的实时文件存储，每个字段都被索引并可被搜索
- 实时分析的分布式搜索引擎
- 可以扩展到上百台服务器，处理PB级结构化或非结构化数据

而且，所有的这些功能被集成到一台服务器，你的应用可以通过简单的RESTful API、各种语言的客户端甚至命令行与之交互。上手Elasticsearch非常简单，它提供了许多合理的缺省值，并对初学者隐藏了复杂的搜索引擎理论。它开箱即用（安装即可使用），只需很少的学习既可在生产环境中使用。Elasticsearch在Apache 2 license下许可使用，可以免费下载、使用和修改。 
随着知识的积累，你可以根据不同的问题领域定制Elasticsearch的高级特性，这一切都是可配置的，并且配置非常灵活。

# ES和solr的差别

## Solr 简介

Solr 是 Apache 下的一个顶级开源项目，采用 Java 开发，它是基于 Lucene 的全文搜索服务器。Solr 提供了比 Lucene 更为丰富的查询语言，同时实现了可配置、可扩展，并对索引、搜索性能进行了优化

Solr 可以独立运行，运行在 Jetty、Tomcat 等这些 Servlet 容器中，Solr索引的实现方法很简单，用 POST 方法向 Solr 服务器发送一个描述Field 及其内容的XML文档，Solr 根据 xml 文档添加、删除、更新索引 Solr 搜索只需要发送 HTTP GET 请求，然后对 Solr 返回 Xml、json 等格式的查询结果进行解析，组织页面布局。Solr 不提供构建 UI 的功能，Solr 提供了一个管理界面，通过管理界面可以查询Solr的配置和运行情况。

Solr 是基于 lucene 开发企业级搜索服务器，实际上就是封装了 lucene。

Solr 是一个独立的企业级搜索应用服务器，它对外提供类似于 Web-service 的 API 接口。用户可以通过 http 请求，向搜索引擎服务器提交一定格式的文件，生成索引；也可以通过提出查找请求，并得到返回结果。

## Lucene简介

 Lucene是apache软件基金会4 jakarta项目组的一个子项目，是一个开放源代码的全文检索引擎工具包，但它不是一个完整的全文检索引擎，而是一个全文检索引擎的架构，提供了完整的查询引擎和索引引擎，部分文本分析引擎（英文与德文两种西方语言)。Lucene的目的是为软件开发人员提供一个简单易用的工具包，以方便的在目标系统中实现全文检索的功能，或者是以此为基础建立起完整的全文检索引擎。Lucene是一套用于全文检索和搜寻的开源程式库，由Apache软件基金会支持和提供。Lucene提供了一个简单却强大的应用程式接口，能够做全文索引和搜寻。**在Java开发环境里Lucene是一个成熟的免费开源工具。就其本身而言，Lucene是当前以及最近几年最受欢迎的免费Java信息检索程序库。**人们经常提到信息检索程序库，虽然与搜索引擎有关，但不应该将信息检索程序库与搜索引擎相混淆。

Lucene是一个全文检索引擎的架构。那什么是全文搜索引擎?

全文搜索引擎是名副其实的搜索引擎，国外具代表性的有 Google、Fast/AlTheWeb、AltaVista、Inktomi、Teoma、WiseNut 等，国内著名的有百度(Baidu)。它们都是通过从互联网上提取的各个网站的信息（以网页文字为主）而建立的数据库中，检索与用户查询条件匹配的相关记录，然后按一定的排列顺序将结果返回给用户，因此他们是真正的搜索引擎。

从搜索结果来源的角度，全文搜索引擎又可细分为两种，一种是拥有自己的检索程序(Indexer)，俗称"蜘蛛" (Spider) 程序或"机器人"(Robot)程序，并自建网页数据库，搜索结果直接从自身的数据库中调用，如上面提到的7家引擎;另一种则是租用其他引擎的数据库，并按自定的格式排列搜索结果，如 Lycos 引擎。

## Elasticsearch 和 Solr 比较

- 当单纯的对已有数据进行搜索时，Solr 更快
- 当实时建立索引时，Solr 会产生 io 阻塞，查询性能较差，Elasticsearch 具有明显的优势
- 随着数据量的增加，Solr 的搜索效率会变得更低，而 Elasticsearch 却没有明显的变化

**Elasticsearch vs Solr 总结**

1. es 基本是开箱即用（解压就能用），非常简单。Solr 安装略微复杂一丢丢!
2. Solr 利用 Zookeeper 进行分布式管理，而 Elasticsearch 自身带有分布式协调管理功能。
3. Solr支持更多格式的数据，比如 JSON、XML、CSV，而 Elasticsearch **仅支持** json 文件格式。
4. Solr官方提供的功能更多，而Elasticsearch本身更注重于核心功能，高级功能多有第三方插件提供，例如图形化界面需要kibana友好支撑
5. Solr查询快，但更新索引时慢（即插入删除慢），用于电商等查询多的应用;
   - ES 建立索引快，**即实时性查询快**，用于 facebook 新浪等搜索。
   - Solr 是传统搜索应用的有力解决方案，但 Elasticsearch 更适用于新兴的实时搜索应用。
6. Solr 比较成熟，有一个更大，更成熟的用户、开发和贡献者社区，而 Elasticsearch 相对开发维护者较少，更新太快，学习使用成本较高。

# ElasticSearch 安装

声明：JDK1.8，最低要求！ElasticSearch客户端，界面工具！

> 下载

官网：https://www.elastic.co/

> window下安装

1. 解压就可以使用了

   ![解压目录](ElasticSearch/image-20210430190355544.png)

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

   双击 elasticsearch.bat 文件

![](ElasticSearch/20210831144336.png)

![启动](ElasticSearch/image-20210430191321976.png)

![访问9200端口](ElasticSearch/image-20210430191459782.png)

> 安装可视化界面 es head的插件

1. 下载

2. 启动

   ```bash
   npm install
   npm run start
   ```

   

3. 连接测试发现存在跨域问题：配置 es

   ```bash
   http.cors.enabled: true
   heep.cors.allow-origin: "*"
   ```

   

4. 重启 es 服务器，然后再次连接

把 es 当作一个数据库（可以建立索引（库），文档（库中的数据））

这个head当作是一个数据展示工具，后面的查询使用Kibana

> 了解 ELK

ELK 是 Elasticsearch、Logstash、Kibana 三大开源框架首字母大写简称。市面上也被成为 Elastic Stack。其中 Elasticsearch 是一个基于 Lucene 、分布式、通过 Restful 方式进行交互的近实时搜索平台框架。像类似百度、谷歌这种大数据全文搜索引擎的场景都可以使用Elasticsearch作为底层支持框架，可见 Elasticsearch 提供的搜索能力确实强大,市面上很多时候我们简称 Elasticsearch 为 es.Logstash 是 ELK 的中央数据流引擎，用于从不同目标（文件/数据存储/MQ）收集的不同格式数据，经过过滤后支持输出到不同目的地（文件/MQ/redis/elasticsearch/kafka等)。Kibana可以将elasticsearch的数据通过友好的页面展示出来，提供实时分析的功能。

市面上很多开发只要提到 ELK 能够一致说出它是一个日志分析架构技术栈总称，但实际上 ELK 不仅仅适用于日志分析，它还可以支持其它任何数据分析和收集的场景，日志分析和收集只是更具有代表性。并非唯一性。

![](ElasticSearch/20210502095342.png)

> 安装 Kibana

Kibana 是一个针对 Elasticsearch 的开源分析及可视化平台，用来搜索、查看交互存储在 Elasticsearch 索引中的数据。使用 Kibana ,可以通过各种图表进行高级数据分析及展示。Kibana 让海量数据更容易理解。它操作简单，基于浏览器的用户界面可以快速创建仪表板( dashboard )实时显示 Elasticsearch 查询动态。设置 Kibana 非常简单。无需编码或者额外的基础架构，几分钟内就可以完成 Kibana 安装并启动 Elasticsearch 索引监测。

**Kibana版本要与ES一致**

# ES 核心概念

1. 索引
2. 字段类型（type）
3. 文档（documents）

> 概述

**集群，节点，索引，类型，文档，分片，映射是什么**

> elasticsearch 是面向文档，关系型数据库和 elasticsearch 客观的对比

![](ElasticSearch/20210502100322.png)

elasticsearch（集群）中可以包含多个索引（数据库），每个索引中可以包含多个类型（表），每个类型下又包含多个文档（行），每个文档中又包含多个字段（列）

**物理设计：**

elasticsearch **在后台把每个索引划分成多个分片**，每个分片可以在集群中的不听服务器间迁移

一个人就是一个集群

**逻辑设计：**

一个索引类型中，包含多个文档，比如说文档1，文档2。我们索引一篇文档时，可以通过这样一个顺序找到：索引 > 类型 > 文档id，通过这个组合我们就能索引到某个具体的文档。注意：id不必是整数，实际上它是个字符串。

> 文档

之前说 elasticsearch 是面向文档的，那么就意味着索引和搜索数据的最小单位是文档，elasticsearch 中，文档有几个重要属性:

- 自我包含，一篇文档同时包含字段和对应的值，也就是同时包含key:value !
- 可以是层次型的，一个文档中包含自文档，复杂的逻辑实体就是这么来的!
- 灵活的结构，文档不依赖预先定义的模式，我们知道关系型数据库中，要提前定义字段才能使用，在elasticsearch中，对于字段是非常灵活的，有时候，我们可以忽略该字段，或者动态的添加一个新的字段。

尽管我们可以随意的新增或者忽略某个字段，但是，每个字段的类型非常重要，比如一个年龄字段类型，可以是字符串也可以是整形。因为 elasticsearch 会保存字段和类型之间的映射及其他的设置。这种映射具体到每个映射的每种类型，这也是为什么在 elasticsearch 中，类型有时候也称为映射类型。

> 类型

类型是文档的逻辑容器，就像关系型数据库一样，表格是行的容器。类型中对于字段的定义称为映射，比如 name 映射为字符串类型。我们说文档是无模式的，它们不需要拥有映射中所定义的所有字段，比如新增一个字段，那么 elasticsearch 是怎么做的呢？ elasticsearch 会自动的将新字段加入映射，但是这个字段的不确定它是什么类型，elasticsearch 就开始猜，如果这个值是18，那么 elasticsearch 会认为它是整形。但是 elasticsearch 也可能猜不对，所以最安全的方式就是提前定义好所需要的映射，这点跟关系型数据库殊途同归了，先定义好字段，然后再使用。

> 索引

索引是映射类型的容器，elasticsearch 中的索引是一个非常大的文档集合。索引存储了映射类型的字段和其他设置。然后它们被存储到了各个分片上了。我们来研究下分片是如何工作的。

**物理设计：节点和分片 如何工作**

一个集群至少有一个节点，而一个节点就是一个 elasricsearch 进程，节点可以有多个索引默认的，如果你创建索引，那么索引将会有个5个分片( primary shard ,又称主分片)构成的，每一个主分片会有一个副本( replica shard ,又称复制分片)

![](ElasticSearch/20210502102147.png)

上图是一个有3个节点的集群，可以看到主分片和对应的复制分片都不会在同一个节点内，这样有利于某个节点挂掉了，数据也不至于丢失。实际上，一个分片是一个 Lucene 索引，一个包含**倒排索引**的文件目录，倒排索引的结构使得 elasticsearch 在不扫描全部文档的情况下，就能告诉你哪些文档包含特定的关键字。

- Primary shard 用于文档存储，每个新的索引会自动创建 5 个Primary shard （数量可自定义）
- Replica shard 是 Primary Shard 的副本，用于冗余数据及提高搜索性能

每个shard（分片）包含多个segment（段），每一个segment都是一个倒排索引。

> 倒排索引

elasticsearch 使用的是一种称为倒排索引的结构，采用 Lucene 倒排索作为底层。这种结构适用于快速的全文搜索，一个索引由文档中所有不重复的列表构成，对于每一个词，都有一个包含它的文档列表。例如，现在有两个文档，每个文档包含如下内容︰

```bash
Study every day, good good up to forever	# 文档1包含的内容
To forever, study every day, good good up	# 文档2包含的内容
```

为了创建倒排索引，我们首先要将每个文档拆分成独立的词(或称为词条或者tokens)，然后创建一个包含所有不重复的词条的排序列表，然后列出每个词条出现在哪个文档：

![](ElasticSearch/20210502102631.png)

现在搜索to forever，只需要查看包含每个词条的文档

![](ElasticSearch/20210502103014.png)

两个文档都匹配，但是第一个文档比第二个匹配程度更高。如果没有别的条件，现在，这两个包含关键字的文档都将返回。再来看一个示例，比如我们通过博客标签来搜索博客文章。那么倒排索引列表就是这样的一个结构：

elasticsearch 的索引和 Lucene 的索引对比
在 elasticsearch 中，索引这个词被频繁使用，这就是术语的使用。在 elasticsearch 中，索引被分为多个分片，每份分片是一个 Lucene 的索引。所以一个 elasticsearch 索引是由多个Lucene索引组成的。别问为什么，谁让 elasticsearch 使用 Lucene 作为底层呢!如无特指，说起索引都是指 elasticsearch 的索引。

## IK 分词器

分词︰即把一段中文或者别的划分成一个个的关键字，我们在搜索时候会把自己的信息进行分词，会把数据库中或者索引库中的数据进行分词，然后进行一个匹配操作，默认的中文分词是将每个字看成一个词，比如“我叫张三”会被分为"我""叫""张""三”，这显然是不符合要求的，所以我们需要安装中文分词器ik来解决这个问题。
IK提供了两个分词算法: ik smart和ik_max_word，其中 ik_ smart为最少切分，ik_max_word为最细粒度划分

> 安装

下载完毕后放入到  elasticsearch 插件即可，然后重启观察 ES

> 查看不同的分词效果

![ik_smart](ElasticSearch/20210507105039.png)

![ik_max_word](ElasticSearch/20210507105253.png)

> ik 分词器也可以增加自己的配置

![配置文件](ElasticSearch/20210507105517.png)

## Rest 风格说明

一种软件架构风格，而不是栋准，只是提供了一组设计原则和约束条件。它主要用于客户端和服务器交互类的软件。基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存等机制。

基本Rest命令说明：

| **method** |                   **url地址**                   |        **描述**        |
| :--------: | :---------------------------------------------: | :--------------------: |
|    PUT     |     localhost:9200/索引名称/类型名称/文档id     | 创建文档（指定文档id） |
|    POST    |        localhost:9200/索引名称/类型名称         | 创建文档（指定文档id） |
|    POST    | localhost:9200/索引名称/类型名称/文档id/_update |        修改文档        |
|   DELETE   |     localhost:9200/索引名称/类型名称/文档id     |        删除文档        |
|    GET     |     localhost:9200/索引名称/类型名称/文档id     |   查询文档通过文档id   |
|    POST    |    localhost:9200/索引名称/类型名称/_search     |      查询所有数据      |

# ES的操作

## 关于索引的基本操作

![](ElasticSearch/20210507105954.png)

![](ElasticSearch/20210507110031.png)

扩展︰通过命令 elasticsearch 索引情况!通过 get _cat/ 可以获得es的当前的很多信息！

![](ElasticSearch/20210507110145.png)

## 关于文档的基本操作

> 基本操作

1. 添加数据

   ```json
   PUT /test2/user/1
   {
     "name": "张三",
     "age": 20,
     "birth": "2001-05-07"
   }
   ```

2. 获取数据

   ```json
   GET test2/user/1
   ```

3. 更新数据

   ![](ElasticSearch/20210507110853.png)

   更推荐 post  _update这种更新方式

4. 搜索

   查询参数体

   ```json
   GET /question/_search
   {
     "query": {
       "match": {
         "content": "问题"
       }
     }
   }
   ```

   ![](ElasticSearch/20210507111212.png)

   如果存在多条查询出来的结果，匹配度越高则分值越高

# 工作原理

## 启动过程

当 ElasticSearch 的节点启动后，它会利用多播（multicast）（或者单播，如果用户更改了配置）寻找集群中的其它节点，并与之建立连接。这个过程如下图所示：

![es 启动过程](ElasticSearch/image-202208261408.png)

## 写入过程

1. 客户端随机选择一个 node 发送请求过去，这个 node 就是 coordinate node（协调节点）
2. coordinate node，对 document 进行路由，将请求转发给对应的 node（有 primary shard ）
3. 实际的 node 上的 primary shard 处理请求，然后将数据同步到 replica node
4. coordinate node，如果发现 primary node 和所有 replica node 都搞定之后，就返回响应结果给客户端

在写 primary 的过程中同时还要持久到本地 ：

![es 写入过程](ElasticSearch/image-202208261411.png)

1. 不断将 Document 写入到 In-memory buffer （内存缓冲区），同时将数据写入 translog 日志文件。
2. 当满足一定条件后内存缓冲区中的 Documents 刷新到 高速缓存（cache）。
3. 生成新的 segment ，这个 segment 还在 cache 中。
4. 这时候还没有 commit ，但是已经可以被读取了。

数据从 buffer 到 cache 的过程是定期每秒刷新一次，这个过程叫 refresh。所以新写入的 Document 最慢 1 秒就可以在 cache 中被搜索到。这也就是为什么说 Elasticsearch 是**准实时**的。

## 读数据过程

1. 客户端发送请求到任意一个node，称为 coordinate node
2. 这个节点将请求转发到对应的 node，此时会使用 round-robin 随机轮询算法，在 primary shard以及其所有 replica 中随机选择一个，让读请求负载均衡
3. 接收请求的 node 返回 document 给 coordinate node
4. coordinate node返回document给客户端

## 搜索过程

1. 客户端发送请求到一个 coordinate node
2. 协调节点将搜索请求转发到所有的 shard 对应的 primary shard 或 replica shard
3. query phase：每个 shard 将自己的搜索结果（其实就是一些doc id），返回给协调节点，由协调节点进行数据的合并、排序、分页等操作，产出最终结果
4. fetch phase：接着由协调节点，根据doc id去各个节点上拉取实际的document数据，最终返回给客户端

## 脑裂问题

集群中存在2个master，2个大脑，就是脑裂问题。

![脑裂问题](ElasticSearch/image-202208261413.png)

master 集群中非常重要的角色，主宰了集群状态的维护，以及 shard 分片的分配，如果存在2个 master，可能会导致数据异常。

如何避免脑裂发生？

过半机制就可与避免脑裂问题的发生。只要集群中超过半数节点投票就可以选出 master。

![避免脑裂问题](ElasticSearch/image-202208261416.png)

# 结合项目

最近实验室有个项目需要实现基础的智能问答功能。因此准备利用 es 的搜索功能搜索到问答库中匹配度最高的问题，再找到其对应的回答内容并返回，来实现简单的智能问答。

下面简要介绍集成 es 到 springboot 项目的步骤，以及部分相关的业务代码。

## 导入依赖

```xml
<!--Elasticsearch相关依赖-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-elasticsearch</artifactId>
</dependency>
```

## 修改配置文件

```yaml
  # Elasticsearch相关配置
  data:
    elasticsearch:
      repositories:
        enabled: true
        cluster-nodes: 127.0.0.1:9300 # es的连接地址及端口号
        cluster-name: elasticsearch # es集群的名称
```

## 创建config 类

```java
@Configuration
public class EsClientConfig {

    @Bean
    public RestHighLevelClient restHighLevelClient(){
        RestHighLevelClient restHighLevelClient = new RestHighLevelClient(RestClient.builder(new 				HttpHost("127.0.0.1", 9200, "http")));
        return restHighLevelClient;
    }
}
```

## service 层增加相关接口

```java
/**
 * 从数据库中导入所有问题到ES
 * @return : int
 * @author AoCan
 * @date 2021/4/29 19:54
 */
Boolean importAll() throws IOException;

/**
 * 根据关键字搜索问题
 * @return : 返回匹配度最高的问题id
 * @param content : 问题内容
 * @author AoCan
 * @date 2021/4/29 19:56
 */
Integer search(String content) throws IOException;
```

相关 service 实现类

```java
 @Override
    public Boolean importAll() throws IOException {
        //批量插入数据
        BulkRequest bulkRequest = new BulkRequest();
        bulkRequest.timeout("10s");

        List<Question> list = questionMapper.getAnswerPassList();

        for (int i = 0; i < list.size(); i++) {
            bulkRequest.add(new IndexRequest(QUESTION).id(""+(i+1)).source(JSON.toJSONString(list.get(i)), XContentType.JSON));
        }
        BulkResponse bulkResponse = client.bulk(bulkRequest, RequestOptions.DEFAULT);
        System.out.println(bulkResponse.hasFailures());
        return bulkResponse.hasFailures();
    }

    @Override
    public Integer search(String content) throws IOException {
        Integer questionId = null;
        SearchRequest request = new SearchRequest(QUESTION);
        //构建搜索条件
        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

        //查询条件，我们可以使用QueryBuilders 工具来实现
        BoolQueryBuilder boolQueryBuilder = QueryBuilders.boolQuery()
                .should(QueryBuilders.matchQuery("content", content));
        sourceBuilder.query(boolQueryBuilder);
        sourceBuilder.timeout(new TimeValue(60, TimeUnit.SECONDS));

        request.source(sourceBuilder);

        SearchResponse searchResponse = client.search(request, RequestOptions.DEFAULT);
//        if (searchResponse.getHits().getTotalHits().value != 0 && searchResponse.getHits().getMaxScore() > MIN_SCORE){
        if (searchResponse.getHits().getTotalHits().value != 0){
            isSearched = true;
            questionId = (Integer) searchResponse.getHits().getAt(0).getSourceAsMap().get("id");
            String questionContent = (String) searchResponse.getHits().getAt(0).getSourceAsMap().get("content");
        }
        return questionId;
    }
```

## Controller 层编写

```java
@ApiOperation(value = "根据用户的问题获取答案", notes = "用户提问后获取回答，若获取不到则返回固定字符串")
@ApiImplicitParams({
@ApiImplicitParam(name = "content", value = "消息内容", required = true, dataType = "Integer",paramType = "query")
 })
@RequestMapping(value = "/getAnswerByMessage", method = RequestMethod.GET)
 @ResponseBody
public CommonResult<String> getAnswerByMessage(@RequestParam("content") String content) throws IOException {
     Integer userId = RequestAttributeUtil.getUserIdInRequest();
     Answer answer = inquiryService.getAnswerByQuestion(userId, content);
     if (answer.getContent() != null){
          return CommonResult.success(answer.getContent());
     }else {
          return CommonResult.success(noAnswerTips);
     }
}
```

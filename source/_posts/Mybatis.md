---
title: Mybatis学习
date: 2021-04-05 11:04:11
index_img: ../picture/20210814145158.jpg
banner_img: ../picture/20210814145158.jpg
tags: ssm
categories: Java后端
---

# Mybatis

回顾：

- JDBC
- Mysql
- java基础
- Maven
- Junit

# 1、简介

## 1.1、什么是Mybatis

![image-20210126204430750](Mybatis/image-20210126204430750.png)

- MyBatis 是一款优秀的**持久层框架**
- 它支持自定义 SQL、存储过程以及高级映射。
- MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。
- MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。
- MyBatis 本是apache的一个[开源项目](https://baike.baidu.com/item/开源项目/3406069)iBatis, 2010年这个[项目](https://baike.baidu.com/item/项目/477803)由apache software foundation 迁移到了[google code](https://baike.baidu.com/item/google code/2346604)，并且改名为MyBatis 。
- 2013年11月迁移到[Github](https://baike.baidu.com/item/Github/10145341)。

如何获得Mybatis？

* Maven仓库

  ```xml
  <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
  <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.5</version>
  </dependency>
  ```

* Github：https://github.com/mybatis/mybatis-3/releases

* 中文文档：https://mybatis.org/mybatis-3/zh/index.html

## 1.2、持久化

数据持久化

- 持久化就是将程序的数据在持久状态和瞬时状态转化的过程
- 内存：**断电即失**
- 数据库(jdbc)，io文件持久化。
- 生活：冷藏

**为什么需要持久化？**

- 有一些对象，不能让他丢掉。
- 内存太贵了



## 1.3、持久层

Dao层，Service层，Controller层

- 完成持久化工作的代码块
- 层界限十分明显



## 1.4、为什么需要Mybatis？

- 帮助程序员把数据存入数据库中
- 方便
- 传统的JDBC代码太复杂了。简化 框架 自动化
- 不用Mybatis也可以。更容易上手。
- 优点：
  - **简单易学**：本身就很小且简单。没有任何第三方依赖，最简单安装只要两个jar文件+配置几个sql映射文件易于学习，易于使用，通过文档和源代码，可以比较完全的掌握它的设计思路和实现。
  - **灵活**：mybatis不会对应用程序或者数据库的现有设计强加任何影响。 sql写在xml里，便于统一管理和优化。通过sql语句可以满足操作数据库的所有需求。
  - 解除sql与程序代码的耦合：通过提供DAO层，将业务逻辑和数据访问逻辑分离，使系统的设计更清晰，更易维护，更易单元测试。**sql和代码的分离，提高了可维护性**。
  - **提供映射标签，支持对象与数据库的orm字段关系映射**
  - **提供对象关系映射标签，支持对象关系组建维护**
  - **提供xml标签，支持编写动态sql**。

**最重要的一点：使用的人多**

Spring SpringMVC SpringBoot

# 2、第一个Mybatis程序

思路：搭建环境 --> 导入Mybatis --> 编写代码 --> 测试

## 2.1、搭建环境

搭建数据库

新建项目

1.新建一个普通的maven项目

2.删除src目录

3.导入maven依赖

```xml
<!--导入依赖-->
<dependencies>
    <!--mysql驱动-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.20</version>
    </dependency>
    <!--mybatis-->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.5</version>
    </dependency>
    <!--junit-->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

## 2.2、创建一个模块

- 编写mybatis的核心配置文件

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE configuration
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-config.dtd">
  <!--configuration核心配置文件-->
  <configuration>
  
      <environments default="development">
          <environment id="development">
              <transactionManager type="JDBC"/>
              <dataSource type="POOLED">
                  <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                  <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                  <property name="username" value="root"/>
                  <property name="password" value="root"/>
              </dataSource>
          </environment>
      </environments>
  
  </configuration>
  ```

- 编写mybatis工具类

```java
//sqlSessionFactory --> sqlSession
public class MybatisUtils {

    private static SqlSessionFactory sqlSessionFactory;

    static {
        try {
            //使用Mybatis第一步：获取sqlSessionFactory对象
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    //既然有了SqlSessionFactory，顾名思义，我们就可以从中获得SqlSession的实例了
    //SqlSession完全包含了面向数据库执行SQL命令所需的所有方法
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }

}
```

## 2.3、编写代码

- 实体类

  ```java
  //实体类
  public class User {
  
      private int id;
      private String name;
      private String pwd;
  
      public User() {
      }
  
      public User(int id, String name, String pwd) {
          this.id = id;
          this.name = name;
          this.pwd = pwd;
      }
  
      public int getId() {
          return id;
      }
  
      public void setId(int id) {
          this.id = id;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public String getPwd() {
          return pwd;
      }
  
      public void setPwd(String pwd) {
          this.pwd = pwd;
      }
  
      @Override
      public String toString() {
          return "User{" +
                  "id=" + id +
                  ", name='" + name + '\'' +
                  ", pwd='" + pwd + '\'' +
                  '}';
      }
  }
  ```

- Dao接口

  ```java
  public interface UserDao {
      List<User> getUserList();
  }
  ```

- 接口实现类由原来的UserDaoImpl转变为一个Mapper配置文件

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <!--namespace绑定一个对应的Dao/Mapper接口-->
  <mapper namespace="com.acacac.dao.UserDao">
      <select id="getUserList" resultType="com.acacac.pojo.User">
      select * from mybatis.user
    </select>
  </mapper>
  ```

## 2.4、测试

注意点：

org.apache.ibatis.binding.BindingException: Type interface com.acacac.dao.UserDao is not known to the MapperRegistry.

**MapperRegistry是什么？**

核心配置文件中注册mappers

![image-20210127214318311](Mybatis/image-20210127214318311.png)

注意

```xml
<!--在build中配置resources，来防止我们资源导出失败的问题-->
<build>
    <resources>
        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>true</filtering>
        </resource>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>false</filtering>
        </resource>
    </resources>
</build>
```

- Junit测试

```java
public class UserDaoTest {

    @Test
    public void test(){

        //第一步：获得SqlSession对像
        SqlSession sqlSession = MybatisUtils.getSqlSession();

        //方式一：getMapper
        UserDao userDao = sqlSession.getMapper(UserDao.class);
        List<User> userList = userDao.getUserList();

        for (User user : userList) {
            System.out.println(user);
        }

        //关闭SqlSession
        sqlSession.close();
    }
}
```

可能遇到的问题：

- 1.配置文件没有注册
- 2.绑定接口错误
- 3.方法名不对
- 4.返回类型不对
- 5.Maven导出资源问题
- **6.mybatis-config不能有中文注释**

# 3、CRUD

## 1、namespace

namespace中的包名要和Dao/mapper接口的包名一致

## 2、select

选择，查询语句；

- id：就是对应的namespace中的方法名；
- resultTypr：Sql语句执行的返回值
- parameterType：参数类型



1.编写接口

```java
//根据ID查询用户
User getUserById(int id);
```

2.编写对应的mapper中的sql语句

```xml
<select id="getUserById" parameterType="int" resultType="com.acacac.pojo.User">
    select * from mybatis.user where id = #{id}
</select>
```

3.测试

```java
@Test
public void getUserById(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();

    UserMapper mapper = sqlSession.getMapper(UserMapper.class);

    User user = mapper.getUserById(1);
    System.out.println(user);


    sqlSession.close();
}
```

## 3、Insert

```xml
<!--对象中的属性，可以直接取出来-->
<insert id="addUser" parameterType="com.acacac.pojo.User">
    insert into mybatis.user(id,name,pwd) values (#{id},#{name},#{pwd});
</insert>
```

## 4、update

```xml
<update id="updateUser" parameterType="com.acacac.pojo.User">
    update mybatis.user set name=#{name},pwd=#{pwd} where id=#{id};
</update>
```

## 5、delete

```xml
<delete id="deleteUser" parameterType="int">
    delete from mybatis.user where id = #{id};
</delete>
```

注意点：

- **增删改需要提交事务**

## 6、常见错误

- 标签不要匹配错
- resource绑定mapper，需要使用路径
- 程序配置文件必须符合规范
- NullPointerException，没有注册到资源
- 输出的xml文件存在中文乱码问题
- maven资源没有导出问题

## 7、万能Map

假设，我们的实体类，或者数据库中的表，字段或者参数过多，我们应当考虑使用Map

```java
//万能的Map
int addUser2(Map<String,Object> map);
```



```xml
<insert id="addUser2" parameterType="map">
    insert into mybatis.user(id,pwd) values (#{userid},#{password});
</insert>
```



```java
@Test
public void addUser2(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);

    Map<String,Object> map = new HashMap<String, Object>();
    map.put("userid",5);
    map.put("password","222333");
    mapper.addUser2(map);
    sqlSession.commit();
    sqlSession.close();
}
```

Map传递参数，直接在sql中取出key即可	【parameterType="map"】

对象传递参数，直接在sql中取对象的属性即可	【parameterType="Object"】

只有一个基本类型参数的情况下，可以直接在sql中取到

多个参数用Map，**或者注解**

## 8、思考题

模糊查询怎么写？

1.Java代码执行的时候，传递通配符% %

```java
List<User> userList = mapper.getUserLike("%李%");
```

2.在sql拼接中使用通配符

```mysql
select * from mybatis.user where name like  "%"#{value}"%"
```

# 4、配置解析

## 1、核心配置文件

- mybatis-config.xml
- MyBatis的配置文件包含了会深深影响MyBatis行为的设置和属性信息

```
configuration（配置）
properties（属性）
settings（设置）
typeAliases（类型别名）
typeHandlers（类型处理器）
objectFactory（对象工厂）
plugins（插件）
environments（环境配置）
environment（环境变量）
transactionManager（事务管理器）
dataSource（数据源）
databaseIdProvider（数据库厂商标识）
mappers（映射器）
```



## 2、环境配置（environments）

MyBatis 可以配置成适应多种环境

**不过要记住：尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。**

学会使用配置多套运行环境

Mybatis默认的事务管理器就是JDBC，连接池：POOLED

## 3、属性（properties）

我们可以通过properties属性来实现引用配置文件

这些属性都是可外部配置且可动态替换的，既可以在典型的java属性文件中配置，亦可通过properties元素的子元素来传递。【db.properties】

![image-20210128172423088](Mybatis/image-20210128172423088.png)

编写一个配置文件

db.properties

```properties
driver = com.mysql.cj.jdbc.Driver
url = jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=utf-8&serverTimezone=GMT&nullCatalogMeansCurrent = true
username = root
password = root
```

在核心配置文件中引入

```xml
<!--引入外部配置文件-->
<properties resource="db.properties">
    <property name="username" value="root"/>
    <property name="password" value="root"/>
</properties>
```

- 可以直接引入外部文件
- 可以在其中增加一些属性配置
- 如果两个文件有同一个字段，优先使用外部配置文件的

## 4、类型别名（typeAliases）

- 类型别名是为Java类型设置一个短的名字
- 存在的意义仅存在于用来减少类完全限定名的冗余

```xml
<!--可以给实体类起别名-->
<typeAliases>
    <typeAlias type="com.acacac.pojo.User" alias="User"/>
</typeAliases>
```

也可以指定一个包名，MyBatis 会在包名下面搜索需要的 Java Bean，比如：

扫描实体类的包，它的默认别名就为这个类的类名，首字母小写

```xml
<!--可以给实体类起别名-->
<typeAliases>
    <package name="com.acacac.pojo"/>
</typeAliases>
```

在实体类比较少的时候，使用第一种方式。

如果实体类十分多，建议使用第二种。

第一种可以DIY别名，第二种则不行，如果非要改，需要在实体类上增加注解

```java
@Ailas("user")
public class User{
```

## 5、设置

这是MyBtis中极为重要的调整设置，它们会改变MyBatis的运行时行为。

![image-20210128180332104](Mybatis/image-20210128180332104.png)

![image-20210128180413580](Mybatis/image-20210128180413580.png)

## 6、其他配置

- [typeHandlers（类型处理器）](https://mybatis.org/mybatis-3/zh/configuration.html#typeHandlers)
- [objectFactory（对象工厂）](https://mybatis.org/mybatis-3/zh/configuration.html#objectFactory)
- plugins（插件）
  - mybatis-generator-core
  - mybatis-plus
  - 通用mapper

## 7、映射器（mappers）

MapperRegistry：注册绑定我们的Mapper文件

方式一：【推荐使用】

```xml
<mappers>
    <mapper resource="com/acacac/dao/UserMapper.xml"/>
</mappers>
```

方式二：使用class文件绑定注册

```xml
    <mappers>
<!--        <mapper resource="com/acacac/dao/UserMapper.xml"/>-->
        <mapper class="com.acacac.dao.UserMapper"/>
    </mappers>
```

注意点：

- 接口和他的Mapper配置文件必须同名
- 接口和他的Mapper配置文件必须在同一个包下

方式三：使用扫描包进行注入绑定

```xml
    <mappers>
<!--        <mapper resource="com/acacac/dao/UserMapper.xml"/>-->
<!--        <mapper class="com.acacac.dao.UserMapper"/>-->
        <package name="com.acacac.dao"/>
    </mappers>
```

注意点：

- 接口和他的Mapper配置文件必须同名
- 接口和他的Mapper配置文件必须在同一个包下

## 8、生命周期和作用域

![image-20210129095212057](Mybatis/image-20210129095212057.png)

作用域和生命周期类别是至关重要的，因为错误的使用会导致非常严重的**并发问题**。

**SqlSessionFactoryBuilder**：

- 一旦创建了SqlSessionFactory，就不再需要它了
- 局部变量

**SqlSessionFactory**：

- 说白了就是可以想象为：数据库连接池
- SqlSessionFactory 一旦被创建就应该在应用的运行期间一直存在，**没有任何理由丢弃它或重新创建另一个实例**
- 因此 SqlSessionFactory 的最佳作用域是应用作用域
- 最简单的就是使用**单例模式**或者**静态单例模式**

**SqlSession**：

- 连接到连接池的一个请求
- SqlSession 的实例不是线程安全的，因此是不能被共享的，所以它的最佳的作用域是请求或方法作用域
- 用完之后需要赶紧关闭，否则资源被占用

![image-20210129095853276](image-20210129095853276.png)

这里面的每一个Mapper，就代表一个具体的业务

# 5、解决属性名和字段名不一致的问题

## 1、问题

数据库中的字段：

![image-20210129100239054](Mybatis/image-20210129100239054.png)

新建一个项目，拷贝之前的，测试实体类字段不一致的情况

```java
public class User {

    private int id;
    private String name;
    private String password;
}
```

测试出现问题

![image-20210129101449601](Mybatis/image-20210129101449601.png)

```xml
//        select * from mybatis.user where id = #{id}

//类型处理器
//        select id,name,pwd from mybatis.user where id = #{id}
```



解决方法：

- 起别名

  ```xml
  <select id="getUserById" parameterType="int" resultType="com.acacac.pojo.User">
      select id,name,pwd as password from mybatis.user where id = #{id}
  </select>
  ```

## 2、resultMap

结果集映射

```
id	name	pwd
id	name	password
```

```xml
<!--结果集映射-->
<resultMap id="UserMap" type="User">
    <!--column数据库中的字段，property实体类中的属性-->
    <result column="id" property="id"/>
    <result column="name" property="name"/>
    <result column="pwd" property="password"/>
</resultMap>

<select id="getUserById" resultMap="UserMap">
    select * from mybatis.user where id = #{id}
</select>
```

- resultMap 元素是 MyBatis 中最重要最强大的元素
- ResultMap 的设计思想是，对简单的语句做到零配置，对于复杂一点的语句，只需要描述语句之间的关系就行了
- ResultMap 的优秀之处——你完全可以不用显式地配置它们
- 如果世界总使这么简单就好了

# 6、日志

## 6.1、日志工厂

如果一个数据库操作，出现了异常，我们需要排错。日志就是最好的助手

曾经：sout、debug

现在：日志工厂

![image-20210129104446062](Mybatis/image-20210129104446062.png)

- SLF4J 
- LOG4J 【掌握】
- LOG4J2 
- JDK_LOGGING 
- COMMONS_LOGGING 
- STDOUT_LOGGING 【掌握】
- NO_LOGGING

在Mybatis中具体使用哪一个日志实现，在设置中设定

**STDOUT_LOGGING标准日志输出**

在mybatis核心配置文件中，配置我们的日志

```xml
<settings>
    <setting name="logImpl" value="STDOUT_LOGGING"/>
</settings>
```

![image-20210129110120211](Mybatis/image-20210129110120211.png)

## 6.2、Log4j

- Log4j是[Apache](https://baike.baidu.com/item/Apache/8512995)的一个开源项目，通过使用Log4j，我们可以控制日志信息输送的目的地是[控制台](https://baike.baidu.com/item/控制台/2438626)、文件、[GUI](https://baike.baidu.com/item/GUI)组件
- 我们也可以控制每一条日志的输出格式
- 通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程
- 通过一个[配置文件](https://baike.baidu.com/item/配置文件/286550)来灵活地进行配置，而不需要修改应用的代码

1.先导入log4j的包

```xml
<!-- https://mvnrepository.com/artifact/log4j/log4j -->
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

2.log4j.properties

```properties
#将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
log4j.rootLogger=DEBUG,console,file

#控制台输出的相关配置
log4j.appender.console=org.apache.log4j.ConsoleAppender
log4j.appender.console.Target=System.out
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout=org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=[%c]-%m%n

#文件输出的相关配置
log4j.appender.file=org.apache.log4j.RollingFileAppender
log4j.appender.file.File=.log/ac.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-mm-dd}][%c]%m%n

#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.ResultSet=DEBUG
log4j.logger.java.sql.PreparedStatement=DEBUG
```

3.配置log4j为日志的实现

```xml
<settings>
    <setting name="logImpl" value="LOG4J"/>
</settings>
```

4.Log4j的使用，直接测试刚才的查询

![image-20210130124844186](Mybatis/image-20210130124844186.png)

**简单使用**

​	1.在要使用Log4j的类中，导入包 import org.apache.log4j.Logger;

​	2.日志对象，参数为当前类的class

```java
static Logger logger = Logger.getLogger(UserDaoTest.class);
```

​	3.日志级别

```java
logger.info("info:进入了testLog4j");
logger.debug("debug:进入了testLog4j");
logger.error("error:进入了testLog4j");
```

问题：生成log文件打不开

解决：https://blog.csdn.net/weixin_43837880/article/details/111567307

![image-20210130131532793](Mybatis/image-20210130131532793.png)

# 7、分页

**思考：为什么要分页？**

- 减少数据的处理量



## 7.1、使用Limit分页

```sql
语法：SELECT * from user limit startIndex,pageSize;
SELECT * from user limit 3; #[0,n]
```



使用Mybatis实现分页，核心是SQL

​	1.接口

```java
//分页
List<User> getUserByLimit(Map<String,Integer> map);
```

​	2.Mapper.xml

```xml
<select id="getUserByLimit" parameterType="map" resultMap="UserMap">
    select * from mybatis.user limit #{startIndex},#{pageSize}
</select>
```

​	3.测试

```java
@Test
public void getUserByLimit(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);

    HashMap<String, Integer> map = new HashMap<String, Integer>();
    map.put("startIndex",1);
    map.put("pageSize",2);

    List<User> userList = mapper.getUserByLimit(map);
    for (User user : userList) {
        System.out.println(user);
    }

    sqlSession.close();
}
```

## 7.2、RowBounds分页（不常用）

不使用SQL实现分页

## 7.3、分页插件

![image-20210130214207059](Mybatis/image-20210130214207059.png)

了解即可

# 8、使用注解开发

## 8.1、面向接口编程

- **根本原因：解耦，可拓展，提高复用，分层开发中，上层不用管具体的实现，大家都遵守共同的标准，使得开发变得容易，规范性更好**
- 在一个面向对象的系统中，系统的各种功能是由许许多多不同对象协作完成的。在这种情况下，各个对象内部是如何实现自己的，对系统设计人员来讲就不那么重要了；
- 而各个对象之间的协作关系则成为系统设计的关键。消到不同类之间的通信，大到各模块之间的交互，在系统设计之初都是要着重考虑的，这也是系统设计的主要工作内容。面向接口编程就是按照这种思想来编程。



**关于接口的理解**

- 接口从更深层次的理解，应是定义（规范，约束）与实现（名实分离的原则）的分离
- 接口本身反映了系统设计人员对系统的抽象理解
- 接口应有两类：
  - 第一类是对一个个体的抽象，它可对应为一个抽象体（abstract class）；
  - 第二类是对一个个体某一方面的抽象，即形成一个抽象面（interface）；
- 一个个体可能有多个抽象面。抽象面与抽象体是有区别的



**三个面向区别**

- 面向对象是指，我们考虑问题时，以对象为单位，考虑它的属性和方法
- 面向过程是指，我们考虑问题时，以一个具体的流程（事务过程）为单位，考虑它的实现
- 接口设计与非接口设计是针对复用技术而言的，与面向对象（过程）不是一个问题，更多的体现就是对系统整体的架构



## 8.2、使用注解开发

1.注解在接口上实现

```java
@Select("select * from user")
List<User> getUsers();
```

2.需要在核心配置文件中绑定接口

```xml
<!--绑定接口-->
<mappers>
    <mapper class="com.acacac.dao.UserMapper"/>
</mappers>
```

3.测试

本质：反射机制实现

底层：动态代理

![image-20210201113534920](Mybatis/image-20210201113534920.png)

**Mybatis详细的执行流程**

![image-20210201140903631](Mybatis/image-20210201140903631.png)

## 8.3、CRUD

我们可以在工具类创建的时候实现自动提交事务

```java
public static SqlSession getSqlSession(){
    return sqlSessionFactory.openSession(true);
}
```



编写接口，增加注解

```java
public interface UserMapper {

    @Select("select * from user")
    List<User> getUsers();

    //方法存在多个参数，所有的参数前面必须加上@Param("id")注解
    @Select("select * from user where id = #{id}")
    User getUserById(@Param("id") int id);

    @Insert("insert into user(id,name,pwd) values (#{id},#{name},#{password})")
    int addUser(User user);

    @Update("update user set name=#{name},pwd=#{password} where id = #{id}")
    int updateUser(User user);

    @Delete("delete from user where id = #{uid}")
    int deleteUser(@Param("uid") int id);
}
```

测试类

【注意：我们必须要将接口注册绑定到我们的核心配置文件中】

**关于@Param()注解**

- 基本类型的参数或者String类型，需要加上
- 引用类型不需要加
- 如果只有一个基本类型的话，可以忽略，但是建议都加上
- 我们在SQL中引用的就是我们这里的@Param()中设定的属性名

**#{}   ￥{}区别**

尽量使用#{}，前者可以防止SQL注入，后者不行

# 9、Lombok

```java
Project Lombok is a java library that automatically plugs into your editor and build tools, spicing up your java.
Never write another getter or equals method again, with one annotation your class has a fully featured builder, Automate your logging variables, and much more.
```

- Java library
- plugs
- build tools
- with one annotation your class

使用步骤：

- 1.在IDEA中安装Lombok插件

- 2.在项目中导入lombok的jar包

- 3.在实体类上加注解即可

  ```java
  @Data
  @AllArgsConstructor
  @NoArgsConstructor
  ```

- 

  ```java
  @Getter and @Setter
  @FieldNameConstants
  @ToString
  @EqualsAndHashCode
  @AllArgsConstructor, @RequiredArgsConstructor and @NoArgsConstructor
  @Log, @Log4j, @Log4j2, @Slf4j, @XSlf4j, @CommonsLog, @JBossLog, @Flogger, @CustomLog
  @Data
  @Builder
  @SuperBuilder
  @Singular
  @Delegate
  @Value
  @Accessors
  @Wither
  @With
  @SneakyThrows
  @val
  @var
  ```

  说明：

  ```java
  @Data：无参构造，get、set、toString、hashcode、equals
  @AllArgsConstructor
  @NoArgsConstructor
  @Getter
  @Setter
  ```

  

# 10、多对一处理

多对一：

![image-20210201160828144](Mybatis/image-20210201160828144.png)

- 多个学生，对应一个老师
- 对于学生这边而言，**关联**.. 多个学生，关联一个老师 【多对一】
- 对于老师而言，**集合**，一个老师，有很多学生 【一对多】

![image-20210201163322262](Mybatis/image-20210201163322262.png)

SQL：

```sql
CREATE table teacher(
	id INT(10) NOT NULL,
	name VARCHAR(30) DEFAULT NULL,
	PRIMARY KEY(id)
)ENGINE=INNODB DEFAULT CHARSET=utf8

INSERT INTO teacher(id, name) VALUES (1, '张老师');

CREATE TABLE student(
	id INT(10) NOT NULL,
	name VARCHAR(30) DEFAULT NULL,
	tid INT(10) DEFAULT NULL,
	PRIMARY KEY (id),
	KEY fktid (tid),
	CONSTRAINT fktid FOREIGN KEY (tid) REFERENCES teacher (id)
)ENGINE=INNODB DEFAULT CHARSET=utf8

INSERT INTO student (id,name,tid) VALUES (1,'小明',1);
INSERT INTO student (id,name,tid) VALUES (2,'小红',1);
INSERT INTO student (id,name,tid) VALUES (3,'小张',1);
INSERT INTO student (id,name,tid) VALUES (4,'小李',1);
INSERT INTO student (id,name,tid) VALUES (5,'小王',1);
```

## 测试环境搭建

- 1.导入lombok
- 2.新建实体类Teacher，Student
- 3.建立Mapper接口
- 4.建立Mapper.xml文件
- 5.在核心配置文件中绑定注册我们的Mapper接口或文件  【方式很多，随心选】
- 6.测试查询是否能够成功

## 按照查询嵌套处理

```xml
<!--
思路：
	1.查询所有的学生信息
	2.根据查询出来的学生的tid，寻找对应的老师		子查询
-->

<select id="getStudent" resultMap="StudentTeacher">
    select * from mybatis.student;
</select>

<resultMap id="StudentTeacher" type="com.acacac.pojo.Student">
    <result property="id" column="id"/>
    <result property="name" column="name"/>
    <association property="teacher" column="tid" javaType="com.acacac.pojo.Teacher" select="getTeacher"/>
</resultMap>

<select id="getTeacher" resultType="com.acacac.pojo.Teacher">
    select * from mybatis.teacher where id = #{id}
</select>
```



## 按照结果嵌套处理

```xml
<!--按照结果嵌套处理-->
<select id="getStudent2" resultMap="StudentTeacher2">
    select s.id sid,s.name sname,t.name tname
    from mybatis.student s, mybatis.teacher t
    where s.tid = t.id;
</select>

<resultMap id="StudentTeacher2" type="com.acacac.pojo.Student">
    <result property="id" column="sid"/>
    <result property="name" column="sname"/>
    <association property="teacher" javaType="com.acacac.pojo.Teacher">
        <result property="name" column="tname"/>
    </association>
</resultMap>
```



回顾Mysql多对一查询方式

- 子查询
- 联表查询

# 11、一对多处理

比如：一个老师拥有多个学生

对于老师而言，就是一对多的关系

## 环境搭建

**实体类**

```java
@Data
public class Student {

    private int id;
    private String name;
    private int tid;
}
```

```java
@Data
public class Teacher {

    private int id;
    private String name;

    //一个老师拥有多个学生
    private List<Student> students;
}
```

## 按照结果嵌套处理

```xml
<!--按照结果嵌套查询-->
<select id="getTeacher" resultMap="TeacherStudent">
    SELECT s.id sid, s.name sname, t.name tname,t.id tid
    from mybatis.student s, mybatis.teacher t
    where s.tid = t.id and t.id = #{tid};
</select>

<resultMap id="TeacherStudent" type="com.acacac.pojo.Teacher">
    <result property="id" column="tid"/>
    <result property="name" column="tname"/>
	<!--复杂的属性，我们需要单独处理 对象：association  集合：collection
	javaType="" 指定属性的类型
	集合中的泛型信息，我们使用ofType获取
	-->
    <collection property="students" ofType="com.acacac.pojo.Student">
        <result property="id" column="sid"/>
        <result property="name" column="sname"/>
        <result property="tid" column="tid"/>
    </collection>
</resultMap>
```

## 按照查询嵌套处理

```xml
<select id="getTeacher2" resultMap="TeacherStudent2">
    select * from mybatis.teacher where id = #{tid};
</select>
<resultMap id="TeacherStudent2" type="com.acacac.pojo.Teacher">
    <collection property="students" javaType="ArrayList" ofType="Student" select="getStudentByTeacherId" column="id"/>
</resultMap>
<select id="getStudentByTeacherId" resultType="com.acacac.pojo.Student">
    select * from mybatis.student where tid = #{tid};
</select>
```



## 小结

- 1.关联 - association 【多对一】
- 2.集合 - collection 【一对多】
- 3.javaType & ofType
  - javaType用来指定实体类中属性的类型
  - ofType用来指定映射到List或者集合中的pojo类型，泛型中的约束类型



注意点：

- 保证SQL的可读性，尽量保证通俗易懂
- 注意一对多和多对一中，属性名和字段的问题
- 如果问题不好排查错误，可以使用日志，建议使用Log4j

# 12、动态SQL

==**什么是动态SQL：动态SQL就是指根据不同的条件生成不同的SQL语句**==

```xml
如果你之前用过 JSTL 或任何基于类 XML 语言的文本处理器，你对动态 SQL 元素可能会感觉似曾相识。在 MyBatis 之前的版本中，需要花时间了解大量的元素。借助功能强大的基于 OGNL 的表达式，MyBatis 3 替换了之前的大部分元素，大大精简了元素种类，现在要学习的元素种类比原来的一半还要少。

if
choose (when, otherwise)
trim (where, set)
foreach
```

## 搭建环境

```sql
CREATE TABLE blog(
	id VARCHAR(50) NOT NULL COMMENT '博客id',
	title varchar(100) NOT NULL COMMENT '博客标题',
	author varchar(30) NOT NULL COMMENT '博客作者',
	create_time datetime NOT NULL COMMENT '创建时间',
	views int(30) NOT NULL COMMENT '浏览量'
)ENGINE=INNODB DEFAULT CHARSET=utf8
```



创建一次基础工程

- 1.导包

- 2.编写配置文件

- 3.编写实体类

- ```java
  @Data
  public class Blog {
  
      private int id;
      private String title;
      private String author;
      private Date createTime;
      private int views;
  }
  ```

- 4.编写实体类对应Mapper接口和Mapper.xml文件



## IF

```xml
<select id="queryBlogIF" parameterType="map" resultType="com.acacac.pojo.Blog">
    select * from mybatis.blog where 1=1
    <if test="title != null">
        and title = #{title}
    </if>
    <if test="author != null">
        and author = #{author}
    </if>
</select>
```



## choose (when, otherwise)

```xaml
<select id="queryBlogChoose" parameterType="map" resultType="com.acacac.pojo.Blog">
    select * from mybatis.blog
    <where>
        <choose>
            <when test="title != null">
                title = #{title}
            </when>
            <when test="author != null">
                and author = #{author}
            </when>
            <otherwise>
                and views = #{views}
            </otherwise>
        </choose>
    </where>
</select>
```



## trim (where, set)

```xml
select * from mybatis.blog
<where>
    <if test="title != null">
        title = #{title}
    </if>
    <if test="author != null">
        and author = #{author}
    </if>
</where>
```

```xml
<update id="updateBlog" parameterType="map">
    update mybatis.blog
    <set>
        <if test="title != null">
            title = #{title},
        </if>
        <if test="author != null">
            author = #{author},
        </if>
    </set>
    where id = #{id}
</update>
```



==**所谓的动态SQL，本质还是SQL语句，知识我们可以在SQL层面，去执行一个逻辑代码**==



## Foreach

```sql
select * from user where 1=1 and 

  <foreach item="id" collection="ids"
      open="(" separator="or" close=")">
        #{id}
  </foreach>

(id=1 or id=2 or id=3)
```

![image-20210203120637938](Mybatis/image-20210203120637938.png)

![image-20210203120719677](Mybatis/image-20210203120719677.png)

```xaml
<!--
    select * from mybatis.blog where 1=1 and (id=1 or id=2 or id=3)
	现在传递一个万能的map，这个map中可以存在一个集合
-->
<select id="queryBlogForeach" parameterType="map" resultType="com.acacac.pojo.Blog">
    select * from mybatis.blog
    <where>
        <foreach collection="ids" item="id" open="and (" close=")" separator="or">
            id = #{id}
        </foreach>
    </where>
</select>
```

==动态SQL就是在拼接SQL语句，我们只要保证SQL的正确性，按照SQL的格式，去排列组合即可==

建议：

- 先在Mysql中写出完整的SQL，再对应的去修改成为我们的动态SQL实现通用即可

## SQL片段

有的时候，我们可能会将一些功能的部分抽取出来，方便复用

- 1.使用SQL标签抽取公共的部分

  ```sql
  <sql id="if-title-author">
      <if test="title != null">
          title = #{title}
      </if>
      <if test="author != null">
          and author = #{author}
      </if>
  </sql>
  ```

- 2.在需要使用的地方使用include标签引用即可

  ```sql
  <select id="queryBlogIF" parameterType="map" resultType="com.acacac.pojo.Blog">
      select * from mybatis.blog
      <where>
          <include refid="if-title-author"></include>
      </where>
  </select>
  ```

注意事项：

- 最好基于单表来定义SQL片段
- 不要存在where标签

# 13、缓存（了解）

## 13.1、简介

```
查询：连接数据库，耗资源
	一次查询的结果，给他暂存在一个可以直接取到的地方！ --> 内存：缓存
	
我们再次查询相同数据的时候，直接走缓存，就不用走数据库了
```

1.什么是缓存【Cache】？

	- 存在内存中的临时数据
	- 将用户经常查询的数据放在缓存（内存）中，用户去查询数据就不用从磁盘上(关系型数据库数据文件)查询，从缓存中查询，从而提高查询效率，解决了高并发系统的性能问题。

2.为什么使用缓存?

- 减少和数据库的交互次数，减少系统开销，提高系统效率。

3.什么样的数据能使用缓存?

- 经常查询并且不经常改变的数据。【可以使用缓存】

## 13.2、Mybatis缓存

- MyBatis包含一个非常强大的查询缓存特性，它可以非常方便地定制和配置缓存。缓存可以极大的提升查询效率
- MyBatis系统中默认定义了两级缓存：**一级缓存**和**二级缓存**
  - 默认情况下，只有一级缓存开启。(SqlSession级别的缓存，也称为本地缓存)
  - 二级缓存需要手动开启和配置，他是基于namespace级别的缓存
  - 为了提高扩展性，MyBatis定义了缓存接口Cache。我们可以通过实现Cache接口来自定义二级缓存

## 13.3、一级缓存

- 一级缓存也叫本地缓存：SqlSession
  - 与数据库同一次绘画期间查询到的数据会放在本地缓存中
  - 以后如果需要获取相同的数据，直接从缓存中拿，没必须再去查询数据库

测试步骤：

- 1.开启日志
- 2.测试在一个Session中查询两次相同记录
- 3.查看日志输出

![image-20210203155702652](Mybatis/image-20210203155702652.png)

缓存失效的情况：

- 1.查询不同的东西

- 2.增删改操作，可能会改变原来的数据，所以必定会刷新缓存

  ![image-20210203160134963](Mybatis/image-20210203160134963.png)

- 3.查询不同的Mapper.xml

- 4.手动清理缓存

  ![image-20210203160336527](Mybatis/image-20210203160336527.png)

小结：一级缓存默认是开启的，只在一次SqlSession中有效，也就是拿到连接到关闭连接这个区间段

一级缓存就是一个Map

## 13.4、二级缓存

- 二级缓存也叫全局缓存，一级缓存作用域太低了，所以诞生了二级缓存
- 基于namespace级别的缓存，一个名称空间，对应一个二级缓存
- 工作机制
  - 一个会话查询一条数据，这个数据就会被放在当前会话的一级缓存中
  - 如果当前会话关闭了，这个会话对应的一级缓存就没了；但是我们想要的是，会话关闭了，一级缓存在中的数据被保存到二级缓存中
  - 新的会话查询信息，就可以从二级缓存中获取内容
  - 不同的mapper查出的数据会放在自己对应的缓存（map）中

步骤：

- 1.开启全局缓存

  ```xml
  <!--显式的开启全局缓存-->
  <setting name="cacheEnabled" value="true"/>
  ```

- 2.在要使用二级缓存的Mapper中开启

  ```xml
  <!--在当前Mapper.xml中使用二级缓存-->
  <cache/>
  ```

  也可以自定义参数

  ```xml
  <!--在当前Mapper.xml中使用二级缓存-->
  <cache eviction="FIFO" flushInterval="60000" size="512" readOnly="true"/>
  ```

- 3.测试

  - 1.问题：我们需要将实体类序列化，否则就会报错

    ```java
    Caused by: java.io.NotSerializableException: com.acacac.pojo.User
    ```

小结：

- 只要开启了二级缓存，在同一个Mapper下就有效
- 所有的数据都会先放在一级缓存中
- 只有当前会话提交，或者关闭的时候，才会提交到二级缓存中



## 13.5、缓存原理

![image-20210203162940760](Mybatis/image-20210203162940760.png)



## 13.6、自定义缓存-ehcache

```
Ehcache是一种广泛使用的开源Java分布式缓存。主要面向通用缓存
```



要在程序中使用ehcache，先要导包

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis.caches/mybatis-ehcache -->
<dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.2.1</version>
</dependency>
```

在mapper中指定使用我们的ehcache实现

```xml
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
```

ehcache.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd">

    <!-- 磁盘缓存位置 -->
    <diskStore path="java.io.tmpdir/ehcache"/>

    <!-- 默认缓存 -->
    <defaultCache
            maxEntriesLocalHeap="10000"
            eternal="false"
            timeToIdleSeconds="120"
            timeToLiveSeconds="120"
            maxEntriesLocalDisk="10000000"
            diskExpiryThreadIntervalSeconds="120"
            memoryStoreEvictionPolicy="LRU">
        <persistence strategy="localTempSwap"/>
    </defaultCache>

    <!-- helloworld缓存 -->
    <cache name="HelloWorldCache"
           maxElementsInMemory="1000"
           eternal="false"
           timeToIdleSeconds="5"
           timeToLiveSeconds="5"
           overflowToDisk="false"
           memoryStoreEvictionPolicy="LRU"/>
</ehcache>
```



Redis数据库做缓存	K-V 





**参考：[狂神说](https://www.bilibili.com/video/BV1S54y1R7SB)**
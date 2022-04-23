---
title: Spring学习
date: 2021-04-22 20:52:19
index_img: picture/20210814145514.jpg
banner_img: picture/20210814145514.jpg
tags: ssm
categories: Java后端
---

# 1、Spring

## 1.1 、简介

* Spring：春天--->给软件行业带来了春天
* 2002，首次推出了Spring框架的雏形：interface21框架！
* Spring框架即以interface21框架为基础，经过重新设计，并不断丰富其内涵，于2004年3月24日，发布了1.0正式版
* *Rod Johnson*，Spring Framework创始人，著名作者。很难想象Rod Johnson的学历，他是悉尼大学的博士，然而专业学不是计算机而是音乐学
* Spring理念：使现有的技术更加容易使用，本身是一个大杂烩，整合现有的技术框架！



* SSH：Struct2 + Spring + Hibernate！
* SSM：SpringMVC + Sping + Mybatis！



官网：https://spring.io/projects/spring-framework#overview

官方下载地址：[http://repo.spring.io/release/org/springframework/spring](https://repo.spring.io/release/org/springframework/spring)

GitHub：https://github.com/spring-projects/spring-framework



```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.12.RELEASE</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.2.12.RELEASE</version>
</dependency>
```

## 1.2 、优点

* Spring是一个开源的免费的框架（容器）
* Spring是一个轻量级的、非入侵式的框架
* 控制反转（IOC），面向切面编程（AOP）
* 支持事务的处理，对框架整合的支持



总结：Spring就是一个轻量级的控制反转（IOC）和面向切面编程（AOP）的框架

## 1.3 、组成

![image-20210121154020298](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090725.png)

## 1.4 、拓展

在Spring的官网有这个介绍：现代化的java开发！说白就是基于Spring的开发

![image-20210121154404827](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090732.png)

* Spring Boot
  * 一个快速开发的脚手架
  * 基于SpringBoot可以快速的开发单个微服务
  * 约定大于配置！
* SpringCloud
  * SpringCloud是基于SpringBoot实现的



因为现在大多数公司都在使用SpringBoot进行快速开发，学习SpringBoot的前提，需要完全掌握Spring及SpringMVC！承上启下的作用！



**弊端：发展了太久之后，违背了原来的理念！配置十分繁琐，人称“配置地狱”**

# 2、IOC理论推导

1.UserDao 接口

2.UserDaoImpl 实现类

3.UserService 业务接口

4.UserServiceImpl 业务实现类

在我们之前的业务中，用户的需求可能会影响我们原来的代码，我们需要根据用户的需求去修改原代码！如果程序代码量十分大，修改一次的成本代价十分昂贵！

我们使用一个set接口实现，已经发生革命性的变化

```java
private UserDao userDao;

//利用set进行动态实现值的注入
public void setUserDao(UserDao userDao) {
    this.userDao = userDao;
}
```

* 之前，程序是主动创建对象，控制权在程序员手上
* 使用了set注入后，程序不再具有主动性，而是变成了被动的接收对象

这种思想，从本质上解决了问题，我们程序员不用再去管理对象的创建了，系统的耦合性大大降低，从而更加专注的在业务的实现上，这是IOC的原型

![image-20210121170827182](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090745.png)

![image-20210121170846076](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090755.png)

## IOC本质

**控制反转IoC(Inversion of Control)，是一种设计思想，DI(依赖注入)是实现IoC的一种方法**，也有人认为DI只是IoC的另一种说法。没有IoC的程序中 , 我们使用面向对象编程 , 对象的创建与对象间的依赖关系完全硬编码在程序中，对象的创建由程序自己控制，控制反转后将对象的创建转移给第三方，个人认为所谓控制反转就是：获得依赖对象的方式反转了。

采用XML方式配置Bean的时候，Bean的定义信息是和实现分离的，而采用注解的方式可以把两者合为一体，Bean的定义信息直接以注解的形式定义在实现类中，从而达到了零配置的目的。

**控制反转是一种通过描述（XML或注解）并通过第三方去生产或获取特定对象的方式。在Spring中实现控制反转的是IoC容器，其实现方法是依赖注入（Dependency Injection,DI）。**

# 3、HelloSpring

## 1.导入Spring相关jar包

注：spring需要导入commons-logging进行日志记录.我们利用maven，他会自动下载对应的依赖项

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.12.RELEASE</version>
</dependency>
```

## 2.编写相关代码

2.1编写一个Hello实体类

```java
package com.acacac.pojo;

public class Hello {

    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void show() {
		System.out.println("Hello" + name);
    }
}
```

2.2编写我们的spring文件，这里我们命名为beans.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- 使用Spring来创建对象，在Spring这些都称为Bean

     类型 变量名 = new 类型();
     Hello hello = new Hello();

     id = 变量名
     class = new 的对象;
     property 相当于给对象中的属性设置一个值

     -->
    <bean id="hello" class="com.acacac.pojo.Hello">
        <property name="name" value="Spring"/>
    </bean>

</beans>
```

2.3测试

```java
public class MyTest {

    public static void main(String[] args) {
        //获取Spring的上下文对象
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        //我们的对象现在都在Spring中的管理了，我们要使用，直接去里面取出来就可以！
        Hello hello = (Hello) context.getBean("hello");
        hello.show();
    }
}
```



![image-20210121210705632](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090806.png)

# 4、IOC创建对象的方式

1.使用无参构造创建对象，默认

2.假设我们要使用有参构造创建对象

​		1.下标赋值

```xml
<bean id="user" class="com.acacac.pojo.User">
<property name="name" value="张三"/>
</bean>
```

​		2.类型赋值

```xml
<bean id="user" class="com.acacac.pojo.User">
    <constructor-arg type="java.lang.String" value="张三"/>
</bean>
```

​		3.参数名

```xml
<bean id="user" class="com.acacac.pojo.User">
    <constructor-arg name="name" value="张三"/>
</bean>
```

总结：在配置文件加载的时候，容器中管理的对象就已经初始化了

# 5、Spring配置

## 5.1、别名

```xml
<!-- 别名，如果添加了别名，我们也可以使用别名获取到这个对象 -->
<alias name="user" alias="userNew"/>
```

## 5.2、Bean的配置

```xml
<!--
 id：bean的唯一标识符，也就是相当于我们学的对象名
 class：bean对象所对应的全限定名：包名 + 类型
 name：也是别名，而且name可以同时取多个别名
 -->
<bean id="userT" class="com.acacac.pojo.UserT" name="user2,u2">
    <property name="name" value="李四"/>
</bean>
```

## 5.3、import

这个import，一般用于团队开发使用，他可以将多个配置文件，导入合并一个

假设，现在项目中有多个人开发，这三个人肤质不同的类开发，不同的类需要注册在不同的bean中，我们可以利用import将所有人的beans.xml合并为一个总的

* 张三

* 李四

* 王五

* applicationContext.xml

  ```xml
  <import resource="beans.xml"/>
  <import resource="beans2.xml"/>
  <import resource="beans3.xml"/>
  ```

使用的时候直接使用总的配置就可以了

# 6、依赖注入

## 6.1、构造器注入

前面已经说过了

## 6.2、Set方式注入【重点】

* 依赖注入：Set注入
  * 依赖：bean对象的创建依赖于容器
  * 注入：bean对象中的所有属性，由容器来注入

【环境搭建】

* 1.复杂类型

  ```java
  public class Address {
  
      private String address;
  
      public String getAddress() {
          return address;
      }
  
      public void setAddress(String address) {
          this.address = address;
      }
  }
  ```

* 2.真实测试对象

  ```java
  public class Student {
  
      private String name;
      private Address address;
      private String[] books;
      private List<String> hobbies;
      private Map<String,String> card;
      private Set<String> games;
      private String wife;
      private Properties info;
  }
  ```

* 3.beans.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd">
  
      <bean id="student" class="com.acacac.pojo.Student">
          <!-- 第一种，普通值注入，value -->
          <property name="name" value="张三"/>
      </bean>
  
  </beans>
  ```

* 4.测试类

  ```java
  public class MyTest {
      public static void main(String[] args) {
          ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
          Student student = (Student)context.getBean("student");
          System.out.println(student.getName());
      }
  }
  ```

完善注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="address" class="com.acacac.pojo.Address">
        <property name="address" value="武汉"/>
    </bean>

    <bean id="student" class="com.acacac.pojo.Student">
        <!-- 第一种，普通值注入，value -->
        <property name="name" value="张三"/>

        <!-- 第二种，Bean注入，ref -->
        <property name="address" ref="address"/>

        <!-- 数组 -->
        <property name="books">
            <array>
                <value>红楼梦</value>
                <value>水浒传</value>
                <value>西游记</value>
                <value>三国演义</value>
            </array>
        </property>

        <!--List-->
        <property name="hobbies">
            <list>
                <value>听歌</value>
                <value>写代码</value>
                <value>看电影</value>
            </list>
        </property>

        <!--Map-->
        <property name="card">
            <map>
                <entry key="身份证" value="1234567891211"/>
                <entry key="银行卡" value="545435435435435"/>
            </map>
        </property>

        <!--Set-->
        <property name="games">
            <set>
                <value>LOL</value>
                <value>BOB</value>
                <value>COC</value>
            </set>
        </property>

        <!--null-->
        <property name="wife">
            <null/>
        </property>

        <!--Properties-->
        <property name="info">
            <props>
                <prop key="学号">20210122</prop>
                <prop key="url">www.baidu.com</prop>
                <prop key="username">root</prop>
                <prop key="password">123456</prop>
            </props>
        </property>

    </bean>

</beans>
```

## 6.3、拓展方式注入

我们可以使用p命名空间和c命名空间进行注入

官方解释：

![image-20210122160909606](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090826.png)

使用：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--p命名空间注入，可以直接注入属性的值：property-->
    <bean id="user" class="com.acacac.pojo.User" p:name="张三" p:age="20"/>

    <!--c命名空间注入，通过构造器注入：construct-args-->
    <bean id="user2" class="com.acacac.pojo.User" c:name="李四" c:age="18"/>

</beans>
```

测试：

```java
@Test
public void test2(){
    ApplicationContext context = new ClassPathXmlApplicationContext("userbeans.xml");
    User user = context.getBean("user2",User.class);
    System.out.println(user.toString());
}
```

注意点：p命名和c命名空间不能直接使用，需要导入xml约束

```xml
 xmlns:p="http://www.springframework.org/schema/p"
 xmlns:c="http://www.springframework.org/schema/c"
```

## 6.4、bean的作用域

![image-20210122161358630](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090840.png)

1.单例模式（Spring默认机制）

```xml
<bean id="user" class="com.acacac.pojo.User" p:name="张三" p:age="20" scope="singleton"/>
```

2.原型模式：每次从容器中get的时候，都会产生一个新对象

```xml
<bean id="user2" class="com.acacac.pojo.User" c:name="李四" c:age="18" scope="prototype"/>
```

3.其余的request、session、application这些个都只能在web开发中使用到

# 7、Bean的自动装配

* 自动装配是Spring满足Bean依赖的一种方式
* Spring会在上下文中自动寻找，并自动给bean装配属性

在Spring中有三种自动装配的方式

* 1.在Spring中有三种装配的方式
* 2.在java中显示配置
* 3.隐式的自动装配bean【重要】

## 7.1、测试

环境搭建：一个人有两个宠物

## 7.2、ByName自动装配

```xml
    <!--
    byName：会自动在容器上下文中查找，和自己对象set方法后面的值对应的beanid
    -->
    <bean id="person" class="com.acacac.pojo.Person" autowire="byName">
        <property name="name" value="ac"/>
    </bean>
```

## 7.3、ByType自动装配

```xml
    <bean class="com.acacac.pojo.Cat"/>
    <bean class="com.acacac.pojo.Dog"/>
    <!--
    byName：会自动在容器上下文中查找，和自己对象set方法后面的值对应的beanid
    byType：会自动在容器上下文中查找，和自己对象属性类型相同的的bean
    -->
    <bean id="person" class="com.acacac.pojo.Person" autowire="byType">
        <property name="name" value="ac"/>
    </bean>
```

小结：

* byname的时候，需要保证所有的bean的id唯一，并且这个bean需要和自动注入的属性的set方法的值一致
* bytype的时候，需要保证所有的bean的class唯一，并且这个bean需要和自动注入的属性的类型一致

## 7.4、使用注解实现自动装配

jdk1.5支持的注解，Spring2.5就支持注解了

The introduction of annotation-based configuration raised the question of whether this approach is “better” than XML. 

要使用注解须知：

 * 1.导入约束。 context约束

 * **<u>2.配置注解的支持：<context:annotation-config/></u>**    **【重要】**

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/context
           https://www.springframework.org/schema/context/spring-context.xsd">
   
       <context:annotation-config/>
   
   </beans>
   ```

   @Autowired

   直接在属性上使用即可，也可以在set方式上使用

   使用Autowired我们可以不用编写Set方法了，前提是你这个自动装配的属性在IOC（Spring）容器中存在，且符合名字byname

   科普：

   ```xml
   @Nullable	字段标记了这个注解，说明这个字段可以为null
   ```

   ```java
   public @interface Autowired {
       boolean required() default true;
   }
   ```

   测试代码

   ```java
   public class Person {
   
       //如果显示定义了Autowired的required属性为false，说明这个对象可以为null，否则不允许为空
       @Autowired(required = false)
       private Cat cat;
       @Autowired
       private Dog dog;
       private String name;
   }
   ```

   如果@Autowired自动装配的环境比较复杂，自动装配无法通过一个注解【@Autowired】完成的时候，我们可以使用@Qualifier(value="xxx")去配置@Autowired的使用，指定一个唯一的bean对象注入

   ```java
   public class Person {
       //如果显示定义了Autowired的required属性为false，说明这个对象可以为null，否则不允许为空
       @Autowired
       @Qualifier(value = "cat111")
       private Cat cat;
       @Autowired
       @Qualifier(value = "dog123")
       private Dog dog;
       private String name;
   }
   ```

   **@Resource注解**

   ```java
   public class Person(){
       
       @Resource(name = "cat2")
       private Cat cat;
       
       @Resource
       private Dog dog;
   }
   ```

   小结：

   @Resource和@Autowired的区别：

   * 都是用来自动装配的，都可以放在属性字段上
   * @Autowired默认按**byType**装配（这个注解是属于spring的），默认情况下必须要求依赖对象必须存在，如果要允许null值，可以设置它的required属性为false。如果Autowired不能唯一自动装配上属性，则需要@Qualifier(value = "xxx")
   * @Resource（这个注解属于J2EE的），默认按照**byName**进行装配，名称可以通过name属性进行指定，如果没有指定name属性，当注解写在字段上时，默认取字段名进行安装名称查找，如果注解写在setter方法上默认取属性名进行装配。当找不到与名称匹配的bean时才按照类型进行装配。但是需要注意的是，如果name属性一旦指定，就只会按照名称进行装配。
   * 执行顺序不同：@Autowired通过byType的方式实现   @Resource默认通过哦byName的方式实现
   * 推荐使用：@Resource注解在字段上，这样就不用写setter方法了，并且这个注解是属于J2EE的，减少了与spring的耦合。这样代码看起就比较优雅。

# 8、使用注解开发

在Spring4之后，要使用注解开发，必须保证app的包导入了

![image-20210123104028014](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090853.png)

使用注解需要导入context约束，增加注解的支持

1.bean

2.属性如何注入

```java
@Component
public class User {

    public String name;

    //相当于 <property name="name" value="123">
    @Value("123")
    public void setName(String name) {
        this.name = name;
    }
}
```

3.衍生的注解

​	@Component有几个衍生注解，我们在web开发中，会按照mvc三层架构分层

 * dao	【@Repository】

 * service   【@Service】

 * controller   【@Controller】

   这四个注解功能是一样的，都是代表将某个类注册到Spring中，装配Bean

4.自动装配置

```
- @Autowired：自动装配通过类型，名字
    如果Autowired不能唯一自动装配上属性，则需要通过@Qualifier(value="xxx")
- @Nullable   字段标记了这个注解，说明这个字段可以为null
- @Resource   自动装配通过名字，类型
```

5.作用域

```java
@Component
@Scope("prototype")
public class User {

    public String name;

    //相当于 <property name="name" value="123">
    @Value("123")
    public void setName(String name) {
        this.name = name;
    }
}
```

6.小结

xml与注解：

	* xml更加万能，适用于任何场合，维护简单方便
	* 注解 不是自己的类使用不了，维护相对复杂

xml与注解最佳实践

	* xml用来管理Bean
	* 注解只负责完成属性的注入
	* 我们在使用的过程中，只需要注意一个问题：必须让注解生效，就需要开启对注解的支持

```xml
<!--指定要扫描的包，这个包下的注解就会生效-->
<context:component-scan base-package="com.acacac"/>
<context:annotation-config/>
```

# 9、使用Java的方式配置Spring

我们现在完全不使用Spring的xml配置了，全权交给Java来做

JavaConfig是Spring的一个子项目，在Spring4之后，它成为了一个核心功能

![image-20210123115219957](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090904.png)

实体类

```java
//这里这个注解的意思，就是说明这个类被Spring接管了，注册到了容器中
@Component
public class User {

    private String name;

    public String getName() {
        return name;
    }

    @Value("qwe") //属性注入值
    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                '}';
    }
}

```

配置文件

```java
package com.acacac.pojo.config;

import com.acacac.pojo.User;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Import;

//这个也会被Spring容器接管，注册到容器中，因为它本来就是一个@Component，
//@Configuration代表这是一个配置类，就和我们之前看的beans.xml一样

@Configuration
@ComponentScan("com.acacac.pojo")
@Import(TestConfig.class)
public class TestConfig {

    //注册一个bean，就相当于我们之前写的一个bean标签
    //这个方法的名字，就相当于bean标签中的id属性
    //这个方法的返回值，就相当于bean标签中的class属性
    @Bean
    public User getUser(){
        return new User();  //就是返回要注入bean的对象
    }
}
```

测试类

```java
public class MyTest {

    public static void main(String[] args) {
        //如果完全使用了配置类的方式去做，我们就只能通过AnnotationConfig上下文来获取容器，通过配置类的class对象加载
        ApplicationContext context = new AnnotationConfigApplicationContext(TestConfig.class);
        User getUser = context.getBean("user",User.class);
        System.out.println(getUser.getName());
    }
}
```

这种纯Java的配置方式，在SpringBoot中随处可见

# 10、代理模式

为什么要学习代理模式？因为这就是SpringAOP的底层  【SpringAOP和SpringMVC】

代理模式的分类：

* 静态代理
* 动态代理

![image-20210124092423271](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090915.png)

## 10.1、静态代理

角色分析：

* 抽象角色：一般会使用接口或者抽象类来解决
* 真实角色：被代理的角色
* 代理角色：代理真实角色，代理真实角色后，我们一般会做一些附属操作
* 客户：访问代理对象的人

代码步骤：

1.接口

```java
//租房
public interface Rent {
    public void rent();
}
```

2.真实角色

```java
//房东
public class Host implements Rent{
    public void rent() {
        System.out.println("房东要出租房子");
    }
}
```

3.代理角色

```java
public class Proxy implements Rent{

    private Host host;

    public Proxy() {
    }

    public Proxy(Host host) {
        this.host = host;
    }


    public void rent() {
        seeHouse();
        host.rent();
        heTong();
        fare();
    }

    //看房
    public void seeHouse(){
        System.out.println("中介带你看房");
    }

    //收中介费
    public void fare(){
        System.out.println("收中介费");
    }

    //签合同
    public void heTong(){
        System.out.println("签租赁合同");
    }

}
```

4.客户端访问代理角色

```java
public class Client {
    public static void main(String[] args) {
        //房东要租房子
        Host host = new Host();
        //代理，中介帮房租租房子
        Proxy proxy = new Proxy(host);
        //不用面对房东，直接找中介租房
        proxy.rent();
    }
}
```

代理模式的好处：

* 可以使真实角色的操作更加纯粹，不用去关注一些公共的业务
* 公共业务交给代理角色，实现了业务的分工
* 公共业务发生扩展的时候，方便集中管理

缺点：

* 一个真实角色就会产生一个代理角色，代码量会翻倍，开发效率会变低

## 10.2、加深理解

代码：对应08-demo02

![image-20210124103455415](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090925.png)

## 10.3、动态代理

* 动态代理和静态代理角色一样
* 动态代理的代理类是动态生成的，不是我们直接写好的
* 动态代理分为两大类：基于接口的动态代理，基于类的动态代理
  * 基于接口---JDK动态代理 【我们在这里使用】
  * 基于类：cglib
  * java字节码实现：javasist

需要了解两个类：Proxy，InvokationHandler：



动态代理的好处：

* 可以使真实角色的操作更加纯粹，不用去关注一些公共的业务
* 公共业务交给代理角色，实现了业务的分工
* 公共业务发生扩展的时候，方便集中管理
* 一个动态代理类代理的是一个接口，一般就是对应的一类业务
* 一个动态代理类可以代理多个类，只要是实现了同一个接口即可

# 11、AOP

## 11.1、什么是 AOP

AOP（Aspect Oriented Programming）意为：面向切面编程，通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术。AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

![640](C:\Users\Administrator\Desktop\640.png)



## 11.2、AOP在Spring中的作用

==提供声明式事务；允许用户自定义切面==

==以下名词需要了解下：==

- 横切关注点：跨越应用程序多个模块的方法或功能。即是，与我们业务逻辑无关的，但是我们需要关注的部分，就是横切关注点。如日志 , 安全 , 缓存 , 事务等等 ....
- 切面（ASPECT）：横切关注点 被模块化 的特殊对象。即，它是一个类。
- 通知（Advice）：切面必须要完成的工作。即，它是类中的一个方法。
- 目标（Target）：被通知对象。
- 代理（Proxy）：向目标对象应用通知之后创建的对象。
- 切入点（PointCut）：切面通知 执行的 “地点”的定义。
- 连接点（JointPoint）：与切入点匹配的执行点。

![图片](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090945)

SpringAOP中，通过Advice定义横切逻辑，Spring中支持5种类型的Advice:

![图片](https://raw.githubusercontent.com/acacac13/picBed/master/20210423090953)

即 Aop 在 不改变原有代码的情况下 , 去增加新的功能 .

## 11.3、使用Spring实现AOP

【重点】使用AOP织入，需要导入一个依赖包！

```xml
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
   <groupId>org.aspectj</groupId>
   <artifactId>aspectjweaver</artifactId>
   <version>1.9.4</version>
</dependency>
```

**第一种方式**

**通过 Spring API 实现**

首先编写我们的业务接口和实现类

```java
public interface UserService {

   public void add();

   public void delete();

   public void update();

   public void search();

}
```

```java
public class UserServiceImpl implements UserService{

   @Override
   public void add() {
       System.out.println("增加用户");
  }

   @Override
   public void delete() {
       System.out.println("删除用户");
  }

   @Override
   public void update() {
       System.out.println("更新用户");
  }

   @Override
   public void search() {
       System.out.println("查询用户");
  }
}
```

然后去写我们的增强类 , 我们编写两个 , 一个前置增强 一个后置增强

```java
public class Log implements MethodBeforeAdvice {

   //method : 要执行的目标对象的方法
   //objects : 被调用的方法的参数
   //Object : 目标对象
   @Override
   public void before(Method method, Object[] objects, Object o) throws Throwable {
       System.out.println( o.getClass().getName() + "的" + method.getName() + "方法被执行了");
  }
}
```

```java
public class AfterLog implements AfterReturningAdvice {
   //returnValue 返回值
   //method被调用的方法
   //args 被调用的方法的对象的参数
   //target 被调用的目标对象
   @Override
   public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
       System.out.println("执行了" + target.getClass().getName()
       +"的"+method.getName()+"方法,"
       +"返回值："+returnValue);
  }
}
```

最后去spring的文件中注册 , 并实现aop切入实现 , 注意导入约束 .

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:aop="http://www.springframework.org/schema/aop"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/aop
       http://www.springframework.org/schema/aop/spring-aop.xsd">

   <!--注册bean-->
   <bean id="userService" class="com.kuang.service.UserServiceImpl"/>
   <bean id="log" class="com.kuang.log.Log"/>
   <bean id="afterLog" class="com.kuang.log.AfterLog"/>

   <!--aop的配置-->
   <aop:config>
       <!--切入点 expression:表达式匹配要执行的方法-->
       <aop:pointcut id="pointcut" expression="execution(* com.kuang.service.UserServiceImpl.*(..))"/>
       <!--执行环绕; advice-ref执行方法 . pointcut-ref切入点-->
       <aop:advisor advice-ref="log" pointcut-ref="pointcut"/>
       <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>
   </aop:config>

</beans>
```

测试

```java
public class MyTest {
   @Test
   public void test(){
       ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
       UserService userService = (UserService) context.getBean("userService");
       userService.search();
  }
}
```

Aop的重要性 : 很重要 . 一定要理解其中的思路 , 主要是思想的理解这一块 .

==Spring的Aop就是将公共的业务 (日志 , 安全等) 和领域业务结合起来 , 当执行领域业务时 , 将会把公共业务加进来 . 实现公共业务的重复利用 . 领域业务更纯粹 , 程序猿专注领域业务 , 其本质还是动态代理 .== 

**第二种方式**

**自定义类来实现Aop**

目标业务类不变依旧是userServiceImpl

第一步 : 写我们自己的一个切入类

```java
public class DiyPointcut {

   public void before(){
       System.out.println("---------方法执行前---------");
  }
   public void after(){
       System.out.println("---------方法执行后---------");
  }
   
}
```

去spring中配置

```xml
<!--第二种方式自定义实现-->
<!--注册bean-->
<bean id="diy" class="com.kuang.config.DiyPointcut"/>

<!--aop的配置-->
<aop:config>
   <!--第二种方式：使用AOP的标签实现-->
   <aop:aspect ref="diy">
       <aop:pointcut id="diyPonitcut" expression="execution(* com.kuang.service.UserServiceImpl.*(..))"/>
       <aop:before pointcut-ref="diyPonitcut" method="before"/>
       <aop:after pointcut-ref="diyPonitcut" method="after"/>
   </aop:aspect>
</aop:config>
```

测试：

```java
public class MyTest {
   @Test
   public void test(){
       ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
       UserService userService = (UserService) context.getBean("userService");
       userService.add();
  }
}
```

**第三种方式**

**使用注解实现**

第一步：编写一个注解实现的增强类

```java
package com.kuang.config;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;

@Aspect
public class AnnotationPointcut {
   @Before("execution(* com.kuang.service.UserServiceImpl.*(..))")
   public void before(){
       System.out.println("---------方法执行前---------");
  }

   @After("execution(* com.kuang.service.UserServiceImpl.*(..))")
   public void after(){
       System.out.println("---------方法执行后---------");
  }

   @Around("execution(* com.kuang.service.UserServiceImpl.*(..))")
   public void around(ProceedingJoinPoint jp) throws Throwable {
       System.out.println("环绕前");
       System.out.println("签名:"+jp.getSignature());
       //执行目标方法proceed
       Object proceed = jp.proceed();
       System.out.println("环绕后");
       System.out.println(proceed);
  }
}
```

第二步：在Spring配置文件中，注册bean，并增加支持注解的配置

```xml
    <!--第三种方式:注解实现-->
    <bean id="annotationPointcut" class="com.acacac.diy.AnnotationPointCut"/>
    <!--开启注解支持-->
    <aop:aspectj-autoproxy/>
```

aop:aspectj-autoproxy：说明

```
通过aop命名空间的<aop:aspectj-autoproxy />声明自动为spring容器中那些配置@aspectJ切面的bean创建代理，织入切面。当然，spring 在内部依旧采用AnnotationAwareAspectJAutoProxyCreator进行自动代理的创建工作，但具体实现的细节已经被<aop:aspectj-autoproxy />隐藏起来了
```

```
<aop:aspectj-autoproxy />有一个proxy-target-class属性，默认为false，表示使用jdk动态代理织入增强，当配为<aop:aspectj-autoproxy  poxy-target-class="true"/>时，表示使用CGLib动态代理技术织入增强。不过即使proxy-target-class设置为false，如果目标类没有声明接口，则spring将自动使用CGLib动态代理。
```

# 12、整合Mybatis

步骤：

1.导入相关jar包

- junit
- mybatis
- mysql数据库
- spring相关
- aop织入
- mybatis-spring  【new】

2.编写配置文件

3.测试

## 12.1、回忆mybatis

1.编写实体类

2.编写核心配置文件

3.编写接口

4.编写Mapper.xml

5.测试

## 12.2、Mybatis-Spring

1.编写数据源配置

2.sqlSessionFactory

3.sqlSessionTemplate

4.需要给接口加实现类【】

5.将自己写的实现类，注入到Spring中

6.测试

# 13、声明式事务

## 1、回顾事务

- 把一组业务当成一个业务来做，要么都成功，要么都失败
- 事务在项目开发中，十分重要，涉及到数据的一致性问题
- 确保完整性和一致性

事务ACID原则：

- 原子性
- 一致性
- 隔离性
  - 多个业务可能操作同一个资源，防止数据损坏
- 持久性
  - 事务一旦提交，无论系统发生什么问题，结果都不会再被影响，被持久化的写到存储器中



**参考：[狂神说](https://www.bilibili.com/video/BV1S54y1R7SB)**
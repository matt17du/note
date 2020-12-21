ioc：

读取配置文件application.xml，将文件中的内容解析为一个dom树，之后把从根节点开始解析构造beandefitionholder对象，存储在beandefitionmap,key是beanfition,解决依赖，设置属性。









# SpringBoot

## idea创建项目

![image-20201212221110224](img/image-20201212221110224.png)



![image-20201212221150594](img/image-20201212221150594.png)





![image-20201212221227773](img/image-20201212221227773.png)





![image-20201212221238278](img/image-20201212221238278.png)



基本就是next即可。



## 配置文件

![image-20201212221452323](img/image-20201212221452323.png)



### yml语法

可以写三种类型基本值、对象和数组

**基本属性**

```yml
server:
  port: 9000


person:
  name: matt
  age: 17
```

""：双引号；不会转义字符串里面的特殊字符；特殊字符会作为本身想表示的意思

```java
name: "zhangsan \n lisi"
//输出；zhangsan 换行  lisi
```



''：单引号；会转义特殊字符，特殊字符最终只是一个普通的字符串数据



```java
name: 'zhangsan \n lisi'
// 输出；zhangsan \n  lisi
```

**对象**

俩种写法行内和非行内

```yml
person:
  name: matt
  age: 17
  dog:
    name: dog
    age: 11
  cat: {name: cat,age: 13}
```

**数组**

```yml
person:
  name: matt
  age: 17
  dog:
    name: dog
    age: 11
  cat: {name: cat,age: 13}
  arr:
    - 1
    - 2
    - 3
  arr1: [1,2,3,4]
```

#### 注意

**key和值中间的冒号还有一个空格**

### 配置文件的值写入类

首先引入

```xml
<!--导入配置文件处理器，配置文件进行绑定就会有提示-->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-configuration-processor</artifactId>
			<optional>true</optional>
		</dependency>
```



```java
@Component
// 读取配置文件前缀为该值
@ConfigurationProperties(prefix = "cat")
public class Cat {
    
    @Value(value = "#{cat.name}")
    private String name;
    private Integer age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Cat{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

```

```yml
cat:
  name: cat
  age: 10
```

**解决properties文件乱码问题**

![image-20201212222910987](img/image-20201212222910987.png)





#### @Value获取值和@ConfigurationProperties获取值比较

|                      | @ConfigurationProperties | @Value     |
| -------------------- | ------------------------ | ---------- |
| 功能                 | 批量注入配置文件中的属性 | 一个个指定 |
| 松散绑定（松散语法） | 支持                     | 不支持     |
| SpEL                 | 不支持                   | 支持       |
| JSR303数据校验       | 支持                     | 不支持     |
| 复杂类型封装         | 支持//比如map类型        | 不支持     |



```java
@Component
@ConfigurationProperties(prefix = "person")
@Validated
public class Person {

    /**
     * <bean class="Person">
     *      <property name="lastName" value="字面量/${key}从环境变量、配置文件中获取值/#{SpEL}"></property>
     * <bean/>
     */

   //lastName必须是邮箱格式
    @Email
    //@Value("${person.last-name}")
    private String lastName;
    //@Value("#{11*2}")
    private Integer age;
    //@Value("true")
    private Boolean boss;

    private Date birth;
    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;
```

### @PropertySource

该类加载指定的配置文件

```java
@Component
@ConfigurationProperties(prefix = "cat")
@PropertySource(value = {"classpath:cat.properties"})
public class Cat {

    @Value(value = "#{cat.name}")
    private String name;
    private Integer age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Cat{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

```

### @ImportResource

导入指定的配置文件

```java
@Configuration
@ImportResource(locations = {"classpath:cat.properties"})
public class MyConfig {
}
```

### @Bean

```java
@Configuration
//@ImportResource(locations = {"classpath:cat.properties"})
public class MyConfig {
    
    /*
     * 功能描述: 容器中导入bean
     *  可以通过@Bean的value值指定bean的id,默认就是方法名
     * @Param: []
     * @Return: com.matt.study.springhello03.bean.Person
     * @Author: matt
     * @Date: 2020/12/12 22:44
     */
    @Bean
    public Person person() {
        return new Person();
    }
}
```

### 占位符

①${random.long}使用random函数

②使用已经定义的值${person.age}

```java
person.name=hello_${random.long}_${person.age}
person.age=11
```

### 多配置文件

#### profiles

![image-20201212225445741](img/image-20201212225445741.png)

使用spring.profiles.active=pro来决定激活哪个文件

#### yml多文档

![image-20201212225735612](img/image-20201212225735612.png)



```java
spring:
  profiles:
    active: pro
---

spring:
  profiles: pro

---

spring:
  profiles: dev
```

#### 激活配置文件



1、在配置文件中指定  spring.profiles.active=dev

2、命令行：

```java
java -jar spring-boot-02-config-0.0.1-SNAPSHOT.jar --spring.profiles.active=dev
```

3、虚拟机参数；

```java
-Dspring.profiles.active=dev
```

![image-20201212230013560](img/image-20201212230013560.png)		

#### 配置文件的加载位置

```java
./config  项目的config目录下
./   项目目录下
./classpath:/config/
./classpath

```

从上往下优先级有高到低



#### 加载顺序

命令行参数

```java
java -jar spring-boot-02-config-02-0.0.1-SNAPSHOT.jar --server.port=8087  --server.context-path=/abc

多个配置用空格分开； --配置项=值
```

==**由jar包外向jar包内进行寻找；**==

==**优先加载带profile**==

**jar包外部的application-{profile}.properties或application.yml(带spring.profile)配置文件**

**jar包内部的application-{profile}.properties或application.yml(带spring.profile)配置文件**



==**再来加载不带profile**==

**jar包外部的application.properties或application.yml(不带spring.profile)配置文件**

**jar包内部的application.properties或application.yml(不带spring.profile)配置文件**



@Configuration注解类上的@PropertySource

**从上往下优先级有高到低**



## 日志

### 概述

日志门面：日志的抽象层

日志实现：日志的实现



**常用的框架**

JUL、JCL、Jboss-logging、logback、log4j、log4j2、slf4j....

| 日志门面  （日志的抽象层）                                   | 日志实现                                             |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| ~~JCL（Jakarta  Commons Logging）~~    SLF4j（Simple  Logging Facade for Java）    **~~jboss-logging~~** | Log4j  JUL（java.util.logging）  Log4j2  **Logback** |



日志门面：  SLF4J；

日志实现：Logback；



SpringBoot：底层是Spring框架，Spring框架默认是用JCL；

​	**SpringBoot选用 SLF4j和logback**



### 使用

[可以参考](https://github.com/matt17du/base)

首先我们需要引入

```java
  <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-logging</artifactId>
  </dependency>
```

之后在application配置文件和logback-spring.xml做一些配置

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201219224414.png)



### 存在的问题

在整合一些框架时可能某些框架需要依赖别的日志框架这时候我们就需要特殊处理这些问题

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201219224833.png)





1. 将原有的日志实现进行排除

2. 引入转换包（其他框架的门面到该框架的门面）

3. 引入实现

   



## Web

### 静态资源

所有 /webjars/** ，都去 classpath:/META-INF/resources/webjars/ 找资源；

webjars：以jar包的方式引入静态资源；可以使用maven使用添加前端资源的依赖，不过现在的项目大多数前后端分离，所以这部分内容使用不会太多。

[webjars](https://www.webjars.org/)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201219225655.png)



项目的静态资源/

```java
"classpath:/META-INF/resources/", 
"classpath:/resources/",
"classpath:/static/", 
"classpath:/public/" 
"/"：当前项目的根路径
```

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201219225834.png)



注意：基本都会放在项目的/resource/static下了



### 模板

#### thymeleaf

[thymeleaf](https://www.thymeleaf.org/)







## 原理

### 自动配置原理

首先springboot的启动类有@SpringBootApplication注解,从该注解点进去

```java
@SpringBootApplication
public class Springhello03Application {

    public static void main(String[] args) {
        SpringApplication.run(Springhello03Application.class, args);
    }

}
```

因为是自动注入，所以我们可以从@EnableAutoConfiguration点进去

![image-20201212231057892](img/image-20201212231057892.png)



从下图中的@Import注解可知，它向容器中导入了AutoConfigurationImportSelector类，我们不妨可以观察该类



![image-20201212231201577](img/image-20201212231201577.png)



可以观察selectImports方法的这行代码，根据方法名我们可以猜测他是获取配置类

![image-20201212234527374](img/image-20201212234527374.png)



从上图的方法的实现点进去可以跳转到下图的方法，我们知道是从该红色部分获得的配置，不妨点进去

![image-20201212234654929](img/image-20201212234654929.png)

它的实现方法有俩个选择第一个即可

**![image-20201212234834728](img/image-20201212234834728.png)**

得到下图，我们继续点进去到他的实现

![image-20201212234925075](img/image-20201212234925075.png)



![image-20201212235026972](img/image-20201212235026972.png)





![image-20201212235127694](img/image-20201212235127694.png)



读取上图的方法我们知道读取META-INF/spring.factories并把它封装为Properties,从properties中获取到EnableAutoConfiguration.class类（类名）对应的值，然后把他们添加在容器中。





![image-20201212235940401](img/image-20201212235940401.png)





![image-20201213000006035](img/image-20201213000006035.png)



当然也不是所有配置类都加载到容器中，每一个配置类都会有@Conditional注解，只有满足某个条件才会加载到容器中。
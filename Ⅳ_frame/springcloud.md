## 介绍



微服务架构是一种架构模式，它提倡将单一应用程序划分成一组小的服务，服务之间互相协调、互相配合，为用户提供最终价值。每个服务运行在其独立的进程中，服务与服务间采用轻量级的通信机制互相协作（通常是基于 HTTP 协议的 RESTful API) 。每个服务都围绕看具本业务进行构建，并且能够被独立的部署到生产环境、类生产环境等。

### 官网

[springcloud](https://cloud.spring.io/spring-cloud-static/Hoxton.SR1/reference/htmlsingle/)



[springcloud 中文](https://www.bookstack.cn/read/spring-cloud-docs/docs-index.md)



[springboot](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/)

## 版本的选择

[springcloud](https://spring.io/projects/spring-cloud#overview)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210511101846.png)







cloud:Hoxton.SR1

boot:2.2.2.RELEASE

cloud Alibaba:2.1.0.RELEASE

java:JAVA8

maven:3.5及以上

mysql:5.7及以上



如果只是用 boot 可以选择最新的，但是使用 cloud 就会有影响， cloud 决定 boot 版本。









## 部分组件停更



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507143756.png)





<img src="https://raw.githubusercontent.com/matt17du/img/main/img/20210507151323.png" style="zoom:900%;" />

 



**推荐使用：**

- nacos
- sentienl
- gateway



## 配置与项目搭建



### 父工程



#### 1.创建一个 maven 项目

记得选择存储位置



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507153317.png)



#### 2.字符编码



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210511103526.png)





#### 3.注解生效激活



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507153847.png)





#### 4.编译版本



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210511103816.png)





#### 5.删除src

父工程删除src



#### 6.pom.xml

在别的项目中下载lombok，因为depencyment并不引入



```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.matt.springcloud</groupId>
    <artifactId>studycloud</artifactId>
    <version>1.0-SNAPSHOT</version>
    <modules>
        <module>cloud-provider-payment8001</module>
        <module>cloud-consumer-order80</module>
        <module>cloud-api-commons</module>
        <module>cloud-eureka-server7001</module>
        <module>cloud-eureka-server7002</module>
        <module>cloud-provider-payment8002</module>
        <module>cloud-provider-payment8004</module>
        <module>cloud-consumerzk-order80</module>
        <module>cloud-providerconsul-payment8006</module>
        <module>cloud-consumerconsul-order80</module>
    </modules>
    <packaging>pom</packaging>


    <!-- 统一管理jar包版本 -->
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
        <junit.version>4.12</junit.version>
        <log4j.version>1.2.17</log4j.version>
        <lombok.version>1.16.18</lombok.version>
        <mysql.version>5.1.47</mysql.version>
        <druid.version>1.1.16</druid.version>
        <mybatis.spring.boot.version>1.3.0</mybatis.spring.boot.version>
    </properties>

    <!-- 子模块继承之后，提供作用：锁定版本+子modlue不用写groupId和version  -->
    <!--子模块不用指定版本dependencyManagement：并不引入-->
    <dependencyManagement>
        <dependencies>
            <!--spring boot 2.2.2-->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.2.2.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <!--spring cloud Hoxton.SR1-->
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>Hoxton.SR1</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>

            <dependency>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>2.1.0.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>

            <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
            <dependency>
                <groupId>mysql</groupId>
                <artifactId>mysql-connector-java</artifactId>
                <version>${mysql.version}</version>
            </dependency>


            <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>druid</artifactId>
                <version>${druid.version}</version>
            </dependency>
            <dependency>
                <groupId>org.mybatis.spring.boot</groupId>
                <artifactId>mybatis-spring-boot-starter</artifactId>
                <version>${mybatis.spring.boot.version}</version>
            </dependency>
            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>${junit.version}</version>
            </dependency>
            <dependency>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
                <version>${log4j.version}</version>
            </dependency>

            <dependency>
                <groupId>org.projectlombok</groupId>
                <artifactId>lombok</artifactId>
                <version>${lombok.version}</version>
                <optional>true</optional>
            </dependency>


        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <fork>true</fork>
                    <addResources>true</addResources>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>


```





#### 7.跳过测试

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507165150.png)





#### 8.父工程安装在仓库



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210511105115.png)





### cloud-provider-payment8001





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507165842.png)



#### 1.建model

cloud-provider-payment8001

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507170030.png)







#### 2.写pom.xml



```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>studycloud</artifactId>
        <groupId>com.matt.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-provider-payment8001</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>

      

        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-web -->
        <!--web actuator写在一块-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-web -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-web -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>

        <!-- https://mvnrepository.com/artifact/com.alibaba/druid -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-jdbc -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-devtools -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-test -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

        <dependency>
            <groupId>com.matt.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>


    </dependencies>



</project>
```

#### 3.写yml



```yaml
server:
  port: 8001


spring:
  application:
    name: cloud-payment-service
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource
    driver-class-name: org.gjt.mm.mysql.Driver
    url: jdbc:mysql://localhost:3306/db2019?useUnicode=true&characterEncoding=utf-8&useSSL=false
    username: root
    password: root



mybatis:
  mapperLocations: classpath:mapper/*.xml
  type-aliases-package: com.atguigu.springcloud.entities

```







#### 4.主启动

```java
@SpringBootApplication
public class PaymentMain8001 {

    public static void main(String[] args) {
        SpringApplication.run(PaymentMain8001.class, args);
    }
}
```





#### 5.业务类

##### 1.sql

```sql
 CREATE TABLE payment (
 id BIGINT(20) NOT NULL AUTO_INCREMENT COMMENT 'ID',
 `serial` VARCHAR(200),
 PRIMARY KEY(id)
) ENGINE=INNODB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8
```

##### 2.entities



```java
@Data // get set
@AllArgsConstructor // 构造器
@NoArgsConstructor
public class Payment implements Serializable {

    private Long id;
    private String serial;

}
```

统一返回结果

```java
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class CommonResult <T>{

    private Integer code;
    private String message;
    private T data;

    public CommonResult(Integer code,String message){
        this(code,message,null);
    }
}
 

```

##### 3.dao



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210511110707.png)



PaymentDao

```java
import com.matt.springcloud.entities.Payment;
import org.apache.ibatis.annotations.Mapper;
import org.apache.ibatis.annotations.Param;


/**
 * @author matt
 * @create 2021-05-07 17:29
 */
@Mapper
public interface PaymentDao {

    public Integer create(Payment payment);

    public Payment getPaymentById(@Param(value = "id") Long id);
}
```



PaymentMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.matt.springcloud.dao.PaymentDao">

    <!--public Integer create(Payment payment);-->
    <insert id="create" parameterType="com.matt.springcloud.entities.Payment" useGeneratedKeys="true" keyProperty="id">
        insert into payment(serial) values(#{serial})
    </insert>

    <resultMap id="BaseResultMap" type="com.matt.springcloud.entities.Payment">
        <id column="id" property="id" jdbcType="BIGINT"></id>
        <id column="serial" property="serial" jdbcType="VARCHAR"></id>
    </resultMap>

    <!--public Payment getPaymentById(@Param(value = "id") Long id);-->
    <select id="getPaymentById"  parameterType="Long" resultMap="BaseResultMap">
        select * from payment where id=#{id}
    </select>


</mapper>

```



##### 4.service





```java
import com.matt.springcloud.entities.Payment;
import org.apache.ibatis.annotations.Param;

/**
 * @author matt
 * @create 2021-05-07 17:44
 */
public interface PaymentService {

    public Integer create(Payment payment);

    public Payment getPaymentById(Long id);
}
```





```java
import com.matt.springcloud.dao.PaymentDao;
import com.matt.springcloud.entities.Payment;
import com.matt.springcloud.service.PaymentService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

/**
 * @author matt
 * @create 2021-05-07 17:45
 */
@Service
public class PaymentServiceImpl implements PaymentService {

    // @Resouce:java自带
    @Autowired
    private PaymentDao paymentDao;

    @Override
    public Integer create(Payment payment) {
        return paymentDao.create(payment);
    }

    @Override
    public Payment getPaymentById(Long id) {
        return paymentDao.getPaymentById(id);
    }
}

```



##### 5.控制器

```java
import com.matt.springcloud.entities.CommonResult;
import com.matt.springcloud.entities.Payment;
import com.matt.springcloud.service.PaymentService;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.cloud.client.ServiceInstance;
import org.springframework.cloud.client.discovery.DiscoveryClient;
import org.springframework.web.bind.annotation.*;

import javax.annotation.Resource;
import java.util.List;

/**
 * @author matt
 * @create 2021-05-07 18:52
 */
@RestController
@Slf4j
public class PaymentController {

    @Resource
    private PaymentService paymentService;

    @Resource
    private DiscoveryClient discoveryClient;

    @Value("${server.port}")
    private String serverPort;

    @PostMapping(value = "/payment/create")
    public CommonResult<Payment> create(@RequestBody Payment payment) {

        log.info(payment.toString());

        int result = paymentService.create(payment);
        log.info("插入结果" + result);

        if (result > 0) {
            return new CommonResult(200, "插入数据库库成功" + serverPort, result);
        }
        return new CommonResult(444, "插入失败", null);
    }

    @GetMapping(value = "/payment/get/{id}")
    public CommonResult<Payment> getPaymentById(@PathVariable(value = "id") Long id) {

        Payment payment = paymentService.getPaymentById(id);
        log.info(payment.toString() + "1111");

        if (payment != null) {
            return new CommonResult(200, "payment" + serverPort, payment);
        }
        return new CommonResult(444, "payment不存在", null);
    }


    @GetMapping(value = "/payment/discovery")
    public Object discovery() {

        List<String> services = discoveryClient.getServices();
        for (String element : services) {
            log.info("***** element:"+element);
        }
        List<ServiceInstance> instances = discoveryClient.getInstances("CLOUD-PAYMENT-SERVICE");
        for (ServiceInstance instance : instances) {
            log.info(instance.getServiceId()+"\t"+instance.getHost()+"\t"+instance.getPort()+"\t"+instance.getUri());
        }


        return this.discoveryClient;

    }


}

```



### 总结

**建model->改pom.xml->写yml->主启动类->业务类**





### **热部署**

项目改变不需要自己重启





#### 1.项目中添加



```
<!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-devtools -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
   <scope>runtime</scope>
    <optional>true</optional>
</dependency>

```



#### 2.父工程中添加



```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
      <configuration>
        <fork>true</fork>
        <addResources>true</addResources>
      </configuration>
    </plugin>
  </plugins>
</build>

```



#### 3.Enabling automatic build 

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507192156.png)



#### 4.Update the value of



CTRL+SHIFT+ALT+/：触发



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210511111900.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210511112047.png)





#### 5.重启IDEA	



### cloud-consumer-order80



#### 1.建model



#### 2.改pom.xml





```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>studycloud</artifactId>
        <groupId>com.matt.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-consumer-order80</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>


    <dependencies>

       

        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-web -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-web  -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-devtools -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-test -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

        <dependency>
            <groupId>com.matt.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>

    </dependencies>



</project>
```



#### 3.yml

```yaml
server:
  port: 80

spring:
  application:
    name: cloud-order-service
```



#### 4.业务类

##### 1.创建实体类和统一返回值类



##### 2.注入 RestTemplate

RestTemplate:http访问工具的方法

```java
import org.springframework.cloud.client.loadbalancer.LoadBalanced;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.client.RestTemplate;

/**
 * @author matt
 * @create 2021-05-07 19:48
 */
@Configuration
public class ApplicationContextConfig {

    @Bean
    public RestTemplate getRestTemplate(){
        return new RestTemplate();
    }

}
```



##### 3.控制器



```java
import com.atguigu.springcloud.entities.CommonResult;
import com.atguigu.springcloud.entities.Payment;
import lombok.extern.slf4j.Slf4j;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.client.RestTemplate;

import javax.annotation.Resource;

@RestController
@Slf4j
public class OrderController {

    public static final String PAYMENT_URL = "http://localhost:8001";

    @Resource
    private RestTemplate restTemplate;

    @GetMapping("/consumer/payment/create")
    public CommonResult<Payment>   create(Payment payment){
        return restTemplate.postForObject(PAYMENT_URL+"/payment/create",payment,CommonResult.class);  //写操作
    }

    @GetMapping("/consumer/payment/get/{id}")
    public CommonResult<Payment> getPayment(@PathVariable("id") Long id){
        return restTemplate.getForObject(PAYMENT_URL+"/payment/get/"+id,CommonResult.class);
    }
}
 
 

```



#### **不要忘记@RequestBody注解**



先clean 后install

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507204456.png)







注册中心：专家有几个，病人有几个





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210508100402.png)





**switchhost**

不要使用aa.com使用aa











```bash
Caused by: org.apache.zookeeper.KeeperException$UnimplementedException: KeeperErrorCode = Unimplemented for /services/cloud-provider-payment/27178f0f-2017-4893-b9a9-ece0b7628a98
```

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210509144653.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210509144802.png)





项目中3.5.3

linux中 3.5.0







### consul

开发模式下启动

```bash
consul agent -dev
```









<iframe   src="https://carbon.now.sh/embed?bg=rgba%28171%2C+184%2C+195%2C+1%29&t=seti&wt=none&l=text%2Fx-java&ds=true&dsyoff=20px&dsblur=68px&wc=true&wa=true&pv=56px&ph=56px&ln=false&fl=1&fm=Hack&fs=14px&lh=133%25&si=false&es=2x&wm=false&code=%2540RestController%250A%2540Slf4j%250Apublic%2520class%2520OrderController%2520%257B%250A%250A%2520%2520%2520%2520%252F%252F%2520public%2520static%2520final%2520String%2520PAYMENT_URL%2520%253D%2520%2522http%253A%252F%252Flocalhost%253A8001%2522%253B%250A%2520%2520%2520%2520public%2520static%2520final%2520String%2520PAYMENT_URL%2520%253D%2520%2522http%253A%252F%252FCLOUD-PAYMENT-SERVICE%2522%253B%250A%250A%2520%2520%2520%2520%2540Resource%250A%2520%2520%2520%2520private%2520RestTemplate%2520restTemplate%253B%250A%250A%250A%2520%2520%2520%2520%252F**%250A%2520%2520%2520%2520%2520*%2520%25E5%258A%259F%25E8%2583%25BD%25EF%25BC%259A%25E6%25B6%2588%25E8%25B4%25B9%25E8%2580%2585%25E4%25B8%258B%25E5%258D%2595%250A%2520%2520%2520%2520%2520*%2520%2540author%2520matt%250A%2520%2520%2520%2520%2520*%2520%2540date%25202021%252F5%252F7%250A%2520%2520%2520%2520%2520*%2520%2540param%2520payment%250A%2520%2520%2520%2520%2520*%2520%2540return%2520com.matt.springcloud.entities.CommonResult%253Ccom.matt.springcloud.entities.Payment%253E%250A%2520%2520%2520%2520*%252F%250A%2520%2520%2520%2520%2540PostMapping%28value%2520%253D%2520%2522%252Fconsumer%252Fpayment%252Fcreate%2522%29%250A%2520%2520%2520%2520public%2520CommonResult%253CPayment%253E%2520create%28Payment%2520payment%29%2520%257B%250A%2520%2520%2520%2520%2520%2520%2520%2520log.info%28payment.toString%28%29%2520%252B%2520%25221111%2522%29%253B%250A%2520%2520%2520%2520%2520%2520%2520%2520return%2520restTemplate.postForObject%28PAYMENT_URL%2520%252B%2520%2522%252Fpayment%252Fcreate%2522%252C%2520payment%252C%2520CommonResult.class%29%253B%250A%2520%2520%2520%2520%257D%250A%250A%2520%2520%2520%2520%2540GetMapping%28value%2520%253D%2520%2522%252Fconsumer%252Fpayment%252Fget%252F%257Bid%257D%2522%29%250A%2520%2520%2520%2520public%2520CommonResult%253CPayment%253E%2520getPayment%28%2540PathVariable%28value%2520%253D%2520%2522id%2522%29%2520Long%2520id%29%2520%257B%250A%250A%2520%2520%2520%2520%2520%2520%2520%2520return%2520restTemplate.getForObject%28PAYMENT_URL%2520%252B%2520%2522%252Fpayment%252Fget%252F%2522%2520%252B%2520id%252C%2520CommonResult.class%29%253B%250A%2520%2520%2520%2520%257D%250A%250A%250A%257D%250A%250A"   style="width: 1024px; height: 834px; border:0; transform: scale(1); overflow:hidden;"   sandbox="allow-scripts allow-same-origin"> </iframe>















<iframe   src="https://carbon.now.sh/embed?bg=rgba%28171%2C+184%2C+195%2C+1%29&t=seti&wt=none&l=text%2Fx-java&ds=true&dsyoff=20px&dsblur=68px&wc=true&wa=true&pv=56px&ph=56px&ln=false&fl=1&fm=Hack&fs=14px&lh=133%25&si=false&es=2x&wm=false&code=%2540RestController%250A%2540Slf4j%250Apublic%2520class%2520OrderController%2520%257B%250A%250A%2520%2520%2520%2520%252F%252F%2520public%2520static%2520final%2520String%2520PAYMENT_URL%2520%253D%2520%2522http%253A%252F%252Flocalhost%253A8001%2522%253B%250A%2520%2520%2520%2520public%2520static%2520final%2520String%2520PAYMENT_URL%2520%253D%2520%2522http%253A%252F%252FCLOUD-PAYMENT-SERVICE%2522%253B%250A%250A%2520%2520%2520%2520%2540Resource%250A%2520%2520%2520%2520private%2520RestTemplate%2520restTemplate%253B%250A%250A%250A%2520%2520%2520%2520%252F**%250A%2520%2520%2520%2520%2520*%2520%25E5%258A%259F%25E8%2583%25BD%25EF%25BC%259A%25E6%25B6%2588%25E8%25B4%25B9%25E8%2580%2585%25E4%25B8%258B%25E5%258D%2595%250A%2520%2520%2520%2520%2520*%2520%2540author%2520matt%250A%2520%2520%2520%2520%2520*%2520%2540date%25202021%252F5%252F7%250A%2520%2520%2520%2520%2520*%2520%2540param%2520payment%250A%2520%2520%2520%2520%2520*%2520%2540return%2520com.matt.springcloud.entities.CommonResult%253Ccom.matt.springcloud.entities.Payment%253E%250A%2520%2520%2520%2520*%252F%250A%2520%2520%2520%2520%2540PostMapping%28value%2520%253D%2520%2522%252Fconsumer%252Fpayment%252Fcreate%2522%29%250A%2520%2520%2520%2520public%2520CommonResult%253CPayment%253E%2520create%28Payment%2520payment%29%2520%257B%250A%2520%2520%2520%2520%2520%2520%2520%2520log.info%28payment.toString%28%29%2520%252B%2520%25221111%2522%29%253B%250A%2520%2520%2520%2520%2520%2520%2520%2520return%2520restTemplate.postForObject%28PAYMENT_URL%2520%252B%2520%2522%252Fpayment%252Fcreate%2522%252C%2520payment%252C%2520CommonResult.class%29%253B%250A%2520%2520%2520%2520%257D%250A%250A%2520%2520%2520%2520%2540GetMapping%28value%2520%253D%2520%2522%252Fconsumer%252Fpayment%252Fget%252F%257Bid%257D%2522%29%250A%2520%2520%2520%2520public%2520CommonResult%253CPayment%253E%2520getPayment%28%2540PathVariable%28value%2520%253D%2520%2522id%2522%29%2520Long%2520id%29%2520%257B%250A%250A%2520%2520%2520%2520%2520%2520%2520%2520return%2520restTemplate.getForObject%28PAYMENT_URL%2520%252B%2520%2522%252Fpayment%252Fget%252F%2522%2520%252B%2520id%252C%2520CommonResult.class%29%253B%250A%2520%2520%2520%2520%257D%250A%250A%250A%257D%250A%250A"   style="width: 1024px; height: 834px; border:0; transform: scale(1); overflow:hidden;"   sandbox="allow-scripts allow-same-origin"> </iframe>









<iframe   src="https://carbon.now.sh/embed?bg=rgba%28171%2C+184%2C+195%2C+1%29&t=seti&wt=none&l=text%2Fx-java&ds=true&dsyoff=20px&dsblur=68px&wc=true&wa=true&pv=56px&ph=56px&ln=false&fl=1&fm=Hack&fs=14px&lh=133%25&si=false&es=2x&wm=false&code=%2540RestController%250A%2540Slf4j%250Apublic%2520class%2520OrderController%2520%257B%250A%250A%2520%2520%2520%2520%252F%252F%2520public%2520static%2520final%2520String%2520PAYMENT_URL%2520%253D%2520%2522http%253A%252F%252Flocalhost%253A8001%2522%253B%250A%2520%2520%2520%2520public%2520static%2520final%2520String%2520PAYMENT_URL%2520%253D%2520%2522http%253A%252F%252FCLOUD-PAYMENT-SERVICE%2522%253B%250A%250A%2520%2520%2520%2520%2540Resource%250A%2520%2520%2520%2520private%2520RestTemplate%2520restTemplate%253B%250A%250A%250A%2520%2520%2520%2520%252F**%250A%2520%2520%2520%2520%2520*%2520%25E5%258A%259F%25E8%2583%25BD%25EF%25BC%259A%25E6%25B6%2588%25E8%25B4%25B9%25E8%2580%2585%25E4%25B8%258B%25E5%258D%2595%250A%2520%2520%2520%2520%2520*%2520%2540author%2520matt%250A%2520%2520%2520%2520%2520*%2520%2540date%25202021%252F5%252F7%250A%2520%2520%2520%2520%2520*%2520%2540param%2520payment%250A%2520%2520%2520%2520%2520*%2520%2540return%2520com.matt.springcloud.entities.CommonResult%253Ccom.matt.springcloud.entities.Payment%253E%250A%2520%2520%2520%2520*%252F%250A%2520%2520%2520%2520%2540PostMapping%28value%2520%253D%2520%2522%252Fconsumer%252Fpayment%252Fcreate%2522%29%250A%2520%2520%2520%2520public%2520CommonResult%253CPayment%253E%2520create%28Payment%2520payment%29%2520%257B%250A%2520%2520%2520%2520%2520%2520%2520%2520log.info%28payment.toString%28%29%2520%252B%2520%25221111%2522%29%253B%250A%2520%2520%2520%2520%2520%2520%2520%2520return%2520restTemplate.postForObject%28PAYMENT_URL%2520%252B%2520%2522%252Fpayment%252Fcreate%2522%252C%2520payment%252C%2520CommonResult.class%29%253B%250A%2520%2520%2520%2520%257D%250A%250A%2520%2520%2520%2520%2540GetMapping%28value%2520%253D%2520%2522%252Fconsumer%252Fpayment%252Fget%252F%257Bid%257D%2522%29%250A%2520%2520%2520%2520public%2520CommonResult%253CPayment%253E%2520getPayment%28%2540PathVariable%28value%2520%253D%2520%2522id%2522%29%2520Long%2520id%29%2520%257B%250A%250A%2520%2520%2520%2520%2520%2520%2520%2520return%2520restTemplate.getForObject%28PAYMENT_URL%2520%252B%2520%2522%252Fpayment%252Fget%252F%2522%2520%252B%2520id%252C%2520CommonResult.class%29%253B%250A%2520%2520%2520%2520%257D%250A%250A%250A%257D%250A%250A"   style="width: 1024px; height: 834px; border:0; transform: scale(1); overflow:hidden;"   sandbox="allow-scripts allow-same-origin"> </iframe>
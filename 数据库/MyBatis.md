# 学习

## 项目搭建

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231172903.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231172938.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231173006.png)









### pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.12.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.matt.study</groupId>
    <artifactId>mybaits0</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>mybaits0</name>
    <description>Demo project for Spring Boot</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>

        <!--web模块-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>


        <!--mysql jdbc-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>

        <!-- druid数据源 -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>

        <!-- mybatis -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>1.3.2</version>
        </dependency>



        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
            <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>

```



### application.properties

```java
server.port=8080

# 数据库连接
spring.datasource.name=study_mybatis
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/study_mybatis?useUnicode=true&characterEncoding=UTF-8&useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=root

# 使用druid数据源
spring.datasource.type=com.alibaba.druid.pool.DruidDataSource
spring.datasource.driverClassName=com.mysql.jdbc.Driver

# spring.mvc.throw-exception-if-no-handler-found=true
# spring.resources.add-mappings=false

# sql映射文件
mybatis.mapperLocations=classpath:mapping/*.xml
# 指定全局配置文件
mybatis.config-location=classpath:mybatis-config.xml
```

### **The server time zone value is unrecogni....**

数据库连接后面添加&serverTimezone=UTC即可





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231172823.png)

### mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <!--<settings>-->
    <!--    <setting name="mapUnderscoreToCamelCase" value="true"/>-->
    <!--</settings>-->
</configuration>
```

### CatalogMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.matt.study.mybaits0.mapper.CatalogMapper">


    <!--int saveCatalog(Catalog catalog);-->
    <insert id="saveCatalog" parameterType="com.matt.study.mybaits0.dataobject.Catalog"
        useGeneratedKeys="true" keyProperty="id">
        insert into catalog(name)
        VALUE(#{name})
    </insert>

    <!--int removeCatalogById(Integer id);-->
    <delete id="removeCatalogById" >
        DELETE FROM catalog
        WHERE id = #{id}
    </delete>

    <!--int updateCatalogByParimaryKey;-->
    <update id="updateCatalogByParimaryKey" >
        UPDATE catalog
        SET name = #{name}
        WHERE id = #{id}
    </update>


    <!--List<Catalog> listCatalog();-->
    <select id="listCatalog" resultType="com.matt.study.mybaits0.dataobject.Catalog">
        select * from catalog
    </select>


</mapper>
```

### 启动类

```java
package com.matt.study.mybaits0;

import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
@MapperScan(value = {"com.matt.study.mybaits0.mapper"})
public class Mybaits0Application {

    public static void main(String[] args) {
        SpringApplication.run(Mybaits0Application.class, args);
    }

}
```

### DruidConfig

**com.alibaba.druid.pool.DruidDataSource**

```java
package com.matt.study.mybaits0.config;

import com.alibaba.druid.pool.DruidDataSource;
import com.alibaba.druid.support.http.StatViewServlet;
import com.alibaba.druid.support.http.WebStatFilter;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.boot.web.servlet.FilterRegistrationBean;
import org.springframework.boot.web.servlet.ServletRegistrationBean;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.sql.DataSource;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

/**
 * @author matt
 * @create 2020-12-13 16:35
 */

@Configuration
public class DruidConfig {


    @ConfigurationProperties(prefix = "spring.datasource")
    @Bean
    public DataSource druid(){
        return  new DruidDataSource();
    }

    //配置Druid的监控
    //1、配置一个管理后台的Servlet
    @Bean
    public ServletRegistrationBean statViewServlet(){
        ServletRegistrationBean bean = new ServletRegistrationBean(new StatViewServlet(), "/druid/*");
        Map<String,String> initParams = new HashMap<>();

        initParams.put("loginUsername","admin");
        initParams.put("loginPassword","123456");
        initParams.put("allow","");//默认就是允许所有访问


        bean.setInitParameters(initParams);
        return bean;
    }


    //2、配置一个web监控的filter
    @Bean
    public FilterRegistrationBean webStatFilter(){
        FilterRegistrationBean bean = new FilterRegistrationBean();
        bean.setFilter(new WebStatFilter());

        Map<String,String> initParams = new HashMap<>();
        initParams.put("exclusions","*.js,*.css,/druid/*");

        bean.setInitParameters(initParams);

        bean.setUrlPatterns(Arrays.asList("/*"));

        return  bean;
    }
}

```











![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231172727.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231172755.png)



## SQL映射文件





### mybatis中的${}和#{}

如果是字符串在使用${}需要自己添加字符串，而#{}不需要自己添加，它会自动添加

${}类似于Statement字符串拼接而#{}类似于PrepareStatement预编译

大多数情况下推荐使用#{}，而在比如模糊查询${}可能更加适合
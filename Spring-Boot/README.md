#Study2
## SpringBoot简介


## 新建一个SpringBoot
1、新建一个Maven托管的项目

2、配置POM.xml
```xml
<modelVersion>4.0.0</modelVersion>

    <groupId>trs.com.cn</groupId>
    <artifactId>SpringBoot_Test</artifactId>
    <version>1.0-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.4.1.BUILD-SNAPSHOT</version>
    </parent>

    <repositories>
        <repository>
            <id>spring-snapshots</id>
            <url>http://repo.spring.io/snapshot</url>
            <snapshots><enabled>true</enabled></snapshots>
        </repository>
        <repository>
            <id>spring-milestones</id>
            <url>http://repo.spring.io/milestone</url>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>spring-snapshots</id>
            <url>http://repo.spring.io/snapshot</url>
        </pluginRepository>
        <pluginRepository>
            <id>spring-milestones</id>
            <url>http://repo.spring.io/milestone</url>
        </pluginRepository>
    </pluginRepositories>
```

3、由于正在开发web应用，将添加spring-boot-starter-web依赖-但在此之前，让我们先看下目前的依赖
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

4、编写控制层代码
```java
package com.str.controller;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.web.bind.annotation.*;
/**
 * Created by wangjie on 2016/10/10 0010.
 */
@RestController
/**
 * 构造型（stereotype）注解。它为阅读代码的人提供暗示（这是一个支持REST的控制器），
 * 对于Spring，该类扮演了一个特殊角色。在本示例中，我们的类是一个web @Controller，
 * 所以当web请求进来时，Spring会考虑是否使用它来处理。
 */
@EnableAutoConfiguration
/**
 * 这个注解告诉Spring Boot根据添加的jar依赖猜测你想如何配置Spring。
 * 由于spring-boot-starter-web添加了Tomcat和Spring MVC，
 * 所以auto-configuration将假定你正在开发一个web应用，并对Spring进行相应地设置。
 */
public class SampleSpringBootController {

    @RequestMapping("/")
    /**
     * 注解提供路由信息，它告诉Spring任何来自"/"路径的HTTP请求都应该被映射到home方法。
     * @RestController 注解告诉Spring以字符串的形式渲染结果，并直接返回给调用者。
     *  此处表示只拦截并处理对“/”的访问
     */
    String home(){
        return "HelloWorld";
    }

    public static void main(String[] args){
        /**
         * 我们的main方法通过调用run，将业务委托给了Spring Boot的SpringApplication类。
         * SpringApplication将引导我们的应用，启动Spring，
         * 相应地启动被自动配置的Tomcat web服务器。
         * 我们需要将SampleSpringBootController.class作为参数传递给run方法，以此告诉SpringApplication谁是主要的Spring组件，
         * 并传递args数组以暴露所有的命令行参数。
         */
        SpringApplication.run(SampleSpringBootController.class,args);
    }
}
```
5、运行项目代码，即可在浏览器中看到 HelloWorld

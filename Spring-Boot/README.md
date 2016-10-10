#Study2
## SpringBoot简介
    Spring Boot简化了基于Spring的应用开发，你只需要"run"就能创建一个独立的，产品级别的Spring应用。 
    我们为Spring平台及第三方库提供开箱即用的设置，这样你就可以有条不紊地开始。多数Spring Boot应用只需要很少的Spring配置。
    你可以使用Spring Boot创建Java应用，并使用java -jar启动它或采用传统的war部署方式。

### SpringBoot主要的目标是：
    1、为所有Spring开发提供一个从根本上更快，且随处可得的入门体验。
    2、开箱即用，但通过不采用默认设置可以快速摆脱这种方式。
    3、提供一系列大型项目常用的非功能性特征，比如：内嵌服务器，安全，指标，健康检测，外部化配置。
    4、绝对没有代码生成，也不需要XML配置。

### SpringBoot提供四个主要的特性：
    1、Spring Boot Starter：它将常用的依赖分组进行进行整合，将其合并到一个依赖中，这样就可以一次性添加项目的Maven或Gradle构建中。
    2、自动配置：Spring Boot的自动配置特性利用了Spring4对条件化配置的支持，合理的推测应用所使用的Bean并自动化装配他们。
    3、命令行接口：Spring Boot的CLI发挥了Groovy编程语言的优势，并结合自动配置进一步简化程序开发。
    4、Actuator：他为Spring Boot应用添加了一定的管理特性。

## 新建一个SpringBoot
1、新建一个Maven托管的项目

2、配置POM.xml
```xml
<modelVersion>4.0.0</modelVersion>

    <groupId>trs.com.cn</groupId>
    <artifactId>SpringBoot_Test</artifactId>
    <version>1.0-SNAPSHOT</version>

    <parent>
        <!--继承spring-boot-starter-parent后我们可以继承一些默认的依赖，这样就无需添加一堆相应的依赖，把依赖配置最小化 -->
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
5、运行项目代码，即可在浏览器中访问http://localhost:8080/ ，看到 HelloWorld

6、添加如下配置，打包使用mvn package就可以将该项目打包成一个可执行的Jar文件，该Jar文件存在于项目中的target目录下。
```xml
<build>   <!-- 构建Jar文件 -->
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```
7、在任何一个有安装Java的平台中，运行java -jar Jar包的名称，就可以在浏览器中使用http://localhost:8080/ 使用该项目。

---
{"dg-publish":true,"permalink":"/Blog/开发程序/java/java-logback/","title":"Spring Boot 整合 Logback","tags":["java"],"noteIcon":"1","created":"2023-05-28T13:40:53+08:00","updated":""}
---


# Logback 

以下是 Logback 的主要特点和组件：

1. 速度和性能：Logback的设计追求极致的性能，使用了非常高效的算法和数据结构，以减少日志输出对应用程序性能的影响。
    
2. 灵活的配置：Logback支持多种配置方式，包括通过XML配置文件、Groovy脚本或编程API来定义日志输出的行为。这使得开发人员可以根据实际需求轻松定制和调整日志记录的行为。
    
3. 分层结构：Logback的架构采用分层结构，允许使用不同的日志输出器（Appender）和日志格式化器（Layout）来满足各种日志需求。您可以根据不同的日志级别将日志输出到不同的目标。
    
4. 支持异步日志：Logback支持异步日志记录，它可以将日志输出任务委托给独立的线程，从而避免日志记录对应用程序主线程的阻塞，提高了应用程序的性能。
    
5. 条件化日志：Logback支持通过条件判断来决定是否输出某条日志，这样可以根据实际情况灵活地控制日志的输出。
    
6. 多种日志级别：Logback支持不同的日志级别，包括TRACE、DEBUG、INFO、WARN和ERROR，开发人员可以根据需求选择合适的日志级别来输出日志。
    
7. 可扩展性：Logback具有良好的可扩展性，您可以使用插件来增强其功能，例如使用SLF4J作为日志门面。
    

总的来说，Logback 是一个功能强大、灵活且高效的日志框架，非常适合用于 Java 应用程序的日志记录需求。它已经成为许多 Java 项目的首选日志框架，提供了丰富的配置选项和性能优势，帮助开发人员更好地管理和调试应用程序。

# 开始使用

中文文档：[核心特性](https://springdoc.cn/spring-boot/features.html#features.logging)

## 引入

由于 SpringBoot 默认使用的就是 logback，不需要额外进行引入依赖。


## 配置

可以根据下面的配置文件进行更改

```xml
<!--  
configuration 有三个属性：  
scan：当此属性设置为true时，配置文件如果发生改变，将会被重新加载，默认值为true。  
scanPeriod：设置监测配置文件是否有修改的时间间隔，如果没有给出时间单位，默认单位是毫秒当scan为true时，此属性生效。默认的时间间隔为1分钟。  
debug：当此属性设置为true时，将打印出logback内部日志信息，实时查看logback运行状态。默认值为false。  
-->  
<configuration>  
    <include resource="org/springframework/boot/logging/logback/defaults.xml" />  
    <!-- 定义日志文件名称 -->  
    <property name="APP_NAME" value="sb-start" />  
    <!-- 定义日志文件的路径 -->  
    <property name="LOG_PATH" value="./logs" />  
    <!-- 定义日志的文件名 -->  
    <property name="LOG_FILE" value="./logs/sb-start.log" />  
  
    <!-- 滚动记录日志，先将日志记录到指定文件，当符合某个条件时，将日志记录到其他文件 -->  
    <appender name="APPLICATION"  
              class="ch.qos.logback.core.rolling.RollingFileAppender">  
        <!-- 指定日志文件的名称 -->  
        <file>${LOG_FILE}</file>  
        <!--  
          当发生滚动时，决定 RollingFileAppender 的行为，涉及文件移动和重命名  
          TimeBasedRollingPolicy： 最常用的滚动策略，它根据时间来制定滚动策略，既负责滚动也负责触发滚动。  
          -->  
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">  
            <!--  
           滚动时产生的文件的存放位置及文件名称  
           %d{yyyy-MM-dd}：按天进行日志滚动  
           %i：当文件大小超过maxFileSize时，按照i进行文件滚动  
           -->  
            <fileNamePattern>${LOG_FILE}.%d{yyyy-MM-dd}.%i.log</fileNamePattern>  
            <!--  
           可选节点，控制保留的归档文件的最大数量，超出数量就删除旧文件。假设设置每天滚动，  
           且maxHistory是7，则只保存最近7天的文件，删除之前的旧文件。  
           注意，删除旧文件时，那些为了归档而创建的目录也会被删除。           -->  
            <maxHistory>7</maxHistory>  
            <!--  
           当日志文件超过maxFileSize指定的大小时，根据上面提到的%i进行日志文件滚动  
           注意此处配置SizeBasedTriggeringPolicy是无法实现按文件大小进行滚动的，  
           必须配置timeBasedFileNamingAndTriggeringPolicy  
           -->            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">  
                <maxFileSize>50MB</maxFileSize>  
            </timeBasedFileNamingAndTriggeringPolicy>  
        </rollingPolicy>  
        <!-- 日志输出格式： -->  
        <layout class="ch.qos.logback.classic.PatternLayout">  
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [ %thread ] - [ %-5level ] [ %logger{50} : %line ] - %msg%n</pattern>  
        </layout>  
    </appender>  
    <!-- ch.qos.logback.core.ConsoleAppender 表示控制台输出 -->  
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">  
        <!--  
       日志输出格式：  
           %d表示日期时间，%green 绿色  
           %thread表示线程名，%magenta 洋红色  
           %-5level：级别从左显示5个字符宽度 %highlight 高亮色  
           %logger{36} 表示logger名字最长36个字符，否则按照句点分割 %yellow 黄色  
           %msg：日志消息  
           %n是换行符  
       -->  
        <layout class="ch.qos.logback.classic.PatternLayout">  
            <pattern>%green(%d{yyyy-MM-dd HH:mm:ss.SSS}) [%magenta(%thread)] %highlight(%-5level) %yellow(%logger{36}): %msg%n</pattern>  
        </layout>  
    </appender>  
  
    <!--  
   root与logger是父子关系，没有特别定义则默认为root，任何一个类只会和一个logger对应，  
   要么是定义的logger，要么是root，判断的关键在于找到这个logger，然后判断这个logger的appender和level。  
   -->  
    <root level="info">  
        <appender-ref ref="CONSOLE" />  
        <appender-ref ref="APPLICATION" />  
    </root>  
</configuration>

```

#  使用 lombok 进行日志记录

## 首先引入依赖

```xml
<dependency>
  <groupId>org.projectlombok</groupId>
  <artifactId>lombok</artifactId>
</dependency>

```

## 使用

在类上加上 `@Slf4j` 注解，之后就可以直接使用 log（添加 `@Slf4j` 注解后会自动添加一个 log 字段）来记录日志了。

```java
package com.example.sbstart.controller;  
  
import com.example.sbstart.entity.Role;  
import com.example.sbstart.service.impl.RoleService;  
import io.swagger.annotations.Api;  
import io.swagger.annotations.ApiOperation;  
import lombok.extern.slf4j.Slf4j;  
import org.springframework.web.bind.annotation.GetMapping;  
import org.springframework.web.bind.annotation.RequestMapping;  
import org.springframework.web.bind.annotation.RestController;  
  
import javax.annotation.Resource;  
import java.util.Collections;  
import java.util.List;  
  
@Api("角色管理")  
@RestController  
@RequestMapping("/role")  
@Slf4j  
public class RoleController {  
  
    @Resource  
    RoleService roleService;  
    @ApiOperation("角色列表")  
    @GetMapping("/")  
    public List<Role> list(){  
        List<Role> roleList = roleService.list();  
        log.info("roleList:{}",roleList);  
        if (roleList != null && !roleList.isEmpty())  
            return roleList;  
        else  
            return Collections.emptyList();  
    }  
  
}
```
---
{"dg-publish":true,"permalink":"/Blog/开发程序/java/springboot-start/","title":"SpringBoot-项目创建及配置","tags":["java"],"noteIcon":"1","created":"2023-05-28T13:40:53+08:00","updated":""}
---


本文在 ChatGPT 协助下进行完成，如有错误请指正。

# SpringBoot 介绍

官方介绍：[Spring Boot](https://spring.io/projects/spring-boot#learn)

2.7.14 版本文档：[Spring Boot Reference Documentation](https://docs.spring.io/spring-boot/docs/2.7.14/reference/html/)

开发环境  JDK 及 Maven 请见：  [[Blog/开发程序/java/java_env\|java_env]]

## 新建项目

1. 使用 SpringBoot 官方的 initializr [Spring Initializr](https://start.spring.io/)
2. 使用 IDEA 的 new project，需要安装 Spring Initializr 插件。

![_resources/springboot-start/e159be91eee0b9247cd3777e4e098dc8_MD5.png](/img/user/_resources/springboot-start/e159be91eee0b9247cd3777e4e098dc8_MD5.png)

![_resources/springboot-start/3118d674ce1a1845bc25402b0802e58b_MD5.png](/img/user/_resources/springboot-start/3118d674ce1a1845bc25402b0802e58b_MD5.png)

## 启动项目及配置

推荐使用 yaml 的方式配置应用，层级分明，数组、对象都支持。可以自动直接注入配置到一个配置类的属性上。

### 应用所有的配置

属性及说明 ：[Common Application Properties](https://docs.spring.io/spring-boot/docs/2.7.14/reference/html/application-properties.html#appendix.application-properties)

![](https://s3.caoayu.eu.org/2023/07/31.png)

### 添加监控 

方便查看所有的方便查看所有的 bean，mappings 健康状况等。

![](https://s3.caoayu.eu.org/2023/07/31.png)

或者手动在 pom 文件里添加依赖


```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

```

## 连接数据库

### 添加依赖

使用 mysql-connector-java ,mybatis plus 连接并操作数据库。

```xml
<dependency>  
    <groupId>org.projectlombok</groupId>  
    <artifactId>lombok</artifactId>  
</dependency>  
  
<dependency>  
    <groupId>com.baomidou</groupId>  
    <artifactId>mybatis-plus-boot-starter</artifactId>  
    <version>3.4.3.4</version>  
</dependency>  
<dependency>  
    <groupId>mysql</groupId>  
    <artifactId>mysql-connector-java</artifactId>  
    <version>5.1.49</version>  
</dependency>
<dependency>  
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-devtools</artifactId>  
</dependency>

```

### 配置数据库连接


```yaml
spring:  
  datasource:  
    driver-class-name: com.mysql.jdbc.Driver  
    url: jdbc:mysql://localhost:3306/demo?useUnicode=true&characterEncoding=utf-8&useSSL=false  
    username: root  
    password: root

```

### 连接及查询

#### 首先生成 mapper，实体类。

![](https://s3.caoayu.eu.org/2023/07/31.jpg)

#### 编写 service 及实现

service 接口

```java
package com.example.sbstart.service;

import com.baomidou.mybatisplus.extension.service.IService;
import com.example.sbstart.entity.User;

public interface IUserService extends IService<User> {
}

```

实现类

```java
package com.example.sbstart.service.impl;  
  
import com.baomidou.mybatisplus.extension.service.impl.ServiceImpl;  
import com.example.sbstart.entity.User;  
import com.example.sbstart.mapper.UserMapper;  
import com.example.sbstart.service.IUserService;  
import org.springframework.stereotype.Service;  
  
@Service  
public class UserService extends ServiceImpl<UserMapper, User> implements IUserService {  
  
}
```

修改 Mapper ，继承 Mybatis 的 Mapper

```java
package com.example.sbstart.mapper;  
  
import com.baomidou.mybatisplus.core.mapper.BaseMapper;  
import com.example.sbstart.entity.User;  
import org.apache.ibatis.annotations.Mapper;  
  
@Mapper  
public interface UserMapper extends BaseMapper<User> {  
    int deleteByPrimaryKey(Integer id);  
  
    int insert(User record);  
  
    int insertSelective(User record);  
  
    User selectByPrimaryKey(Integer id);  
  
    int updateByPrimaryKeySelective(User record);  
  
    int updateByPrimaryKey(User record);  
}
```

#### 添加路由及 controller

```java
package com.example.sbstart.controller;  
  
import com.example.sbstart.entity.User;  
import com.example.sbstart.service.impl.UserService;  
import org.springframework.web.bind.annotation.GetMapping;  
import org.springframework.web.bind.annotation.RequestMapping;  
import org.springframework.web.bind.annotation.RestController;  
  
import javax.annotation.Resource;  
import java.util.Collections;  
import java.util.List;  
  
@RestController  
@RequestMapping("/user")  
public class UserController {  
    @Resource  
    UserService userService;  
  
    @GetMapping("/")  
    public List<User> users() {  
        List<User> users = userService.list();  
        if (users == null || users.isEmpty()) {  
            return Collections.emptyList();  
        }  
        return userService.list();  
    }  
}
```

访问 /users 可以看到所有的数据，没有数据为空数组。

##  整合 Swagger-UI

参考链接： https://springboot.io/t/topic/4613

国际惯例先引入依赖

```xml
<dependency>
	<groupId>com.github.xiaoymin</groupId>
	<artifactId>knife4j-spring-boot-starter</artifactId>
	<version>3.0.3</version>
</dependency>

```

如果 springboot 版本大于 2.6，那么可能启动会提示  **Failed to start bean ‘documentationPluginsBootstrapper’; nested exception is java.lang.NullPointerException** 

由于 Springfox 使用的路径匹配是基于 AntPathMatcher，而 Spring Boot 2.6.X 使用的是 PathPatternMatcher，所以将 MVC 的路径匹配规则改成 AntPathMatcher，在配置文件中加入如下参数即可（如果没有报错，可以跳过这个环节）

```yaml
spring:
  mvc:
    pathmatch:
      # Springfox使用的路径匹配是基于AntPathMatcher的，而Spring Boot 2.6.X使用的是PathPatternMatcher
      # 所以需要配置此参数
      matching-strategy: ant_path_matcher
```

如果还报错，那就检查下是否引入了 spring-boot-starter-actuator 这个依赖，目前测试引入这个也会报错，把这个去掉就能正常启动了。

访问 `localhost:8080/doc.html` 就可以看到在线文档了

![](https://s3.caoayu.eu.org/2023/07/31/202307312357271.png)
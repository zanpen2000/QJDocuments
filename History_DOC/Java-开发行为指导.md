# java 开发行为指导

|修订人|版本号|
|-|-|
|王帅，孙靖武|1.0|

## 1、Java后端项目主要技术介绍

> 前后端分离的微服务架构

### 1.1、Spring Boot
- 使用 Spring 项目引导页面可以在几秒构建一个项目
- 方便对外输出各种形式的服务，如 REST API、WebSocket、Web、Streaming、Tasks
- 实现了自动配置，降低了项目搭建的复杂度，告别spring mvc的xml配置
- 支持运行期内嵌容器，如 Tomcat、Jetty
- 支持各种 IED，如 IntelliJ IDEA 、NetBeans

### 1.2、Spring Cloud
- 是一系列有序框架的集合，简单易懂、易部署易维护的分布式系统开发工具包、
- Spring Cloud依赖于SpringBoot，利用SpringBoot开放的便捷性可以简化分布式系统基础设施的开发。
- 包含服务发现注册、配置中心、消息总线、负载均衡、断路器、数据监控等。

### 1.3、Spring-Data-JPA
- Spring data jpa是在JPA规范下提供了Repository层的实现，但是使用哪一种ORM需要你来决定
- ORM目前为**Hibernate**

### 1.4、mysql
- mysql数据库，是当前应用非常广泛的一款关系型数据库

### 1.5、elaticsearch
- ES是一个搜索引擎，是基于Lucene的。它是一个提供了基于RESTful 的web接口，能够达到实时，稳定，可靠，快速的搜索引擎。
- 分布式的实时文件存储，每个字段都被索引并可被搜索
- 分布式的实时分析搜索引擎
- 可以扩展到上百台服务器，处理PB级结构化或非结构化数据

### 1.6、redis
- 一个开源的key-value，内存中的数据结构存储系统，它可以用作数据库、缓存和消息中间件。
- Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
- Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。
- Redis支持数据的备份，即master-slave模式的数据备份。

## 2 、项目目录结构

![](https://www.w3cschool.cn/attachments/image/20180928/1538100640532351.png)

- doc：项目文档目录，存放项目流程图，时序图，类图和开发设计文档
- src：代码存储文件夹
- com.allqj.项目名：项目目录
- business：业务代码目录，内存放各个领域目录，领域目录正常会存放 控制层，实体，dao层，服务层三个目录
- common：项目公共代码
- configuration：项目配置类目录
- enums：枚举类
- exception：自定义错误类
- filter：过滤器类
- interceptor：拦截器类、
- util：工具类
- resources：静态资源文件，因采用前后端分离架构，一般只会存储`.yml`配置文件
- pom.xml：maven项目管理文件
- README.md：项目进度记录文件
- Dockerfile：项目docker  镜像制作文件（运维人员编写）
- .gitlab-ci.yml：项目自动化部署脚本。（运维人员编写）

## 3、spring boot demo项目建立

Flie-》New-》Project-》选择Spring Initializr-》一直Next即可

在pom.xml中需要添加的jar包，以简化开发

↓↓↓

### 3.1、Lombok

Lombok是一种Java™实用工具，可用来帮助开发人员消除Java的冗长代码，尤其是对于简单的Java对象（POJO）。

```
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.16.10</version>
</dependency>
```

- 需要IntelliJ安装Lombok，通过IntelliJ的插件中心安装
- 安装成功后可在类上添加注解，`@Setter  @Getter`来省去手动生成getter，setter方法，使代码简洁；`@Slf4j`来打印日志功能，`log.info();`
- lombok还有其他众多功能，由于某些功能会与其他jar包功能产生冲突，除以上三个注解外不建议使用。

### 3.2、Spring Data JPA

JPA诞生的缘由是为了整合第三方ORM框架，在ORM框架中，Hibernate是一支很大的部队，使用很广泛，也很方便，能力也很强，同时Hibernate也是和JPA整合的比较良好，我们可以认为JPA是标准，事实上也是，JPA几乎都是接口，实现都是Hibernate在做，宏观上面看，在JPA的统一之下Hibernate很良好的运行。

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

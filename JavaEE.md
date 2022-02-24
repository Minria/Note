# Spring 核心容器

## 简介

本模块由 spring-core , spring-beans , spring-context , spring-context-support , and springexpression
(Spring Expression Language) 4 个模块组成。

## IoC和DI

**什么叫IoC**

IoC (Inversion of Control，控制反转) ，是面向对象编程中的一种设计原则，可以用来减低计算机代码之间的耦合度。只是因为该理论时间成熟相对较晚，并没有包含在GoF中。

系统中通过引入实现了IoC模式的IoC容器，即可由IoC容器来管理对象的生命周期、依赖关系等，从而使得应用程序的配置和依赖性规范与实际的应用程序代码分离。

从使用上看，以前手动new对象，并设置对象中属性的方式，控制权是掌握在应用程序自身。现在则全部转移到了容器，由容器来统一进行管理对象。因为控制权发生了扭转，所以叫控制反转。
**什么又是IoC容器**

实现了IoC思想的容器就是IoC容器，比如：SpringFremework, Guice（Google开源的轻量级DI框架）
**什么是DI**

DI (Dependency Injection，依赖注入) 是实现IoC的方法之一。所谓依赖注入，就是由IOC容器在运行期
间，动态地将某种依赖关系注入到对象之中。

所以，依赖注入（DI）和控制反转（IoC）是从不同的角度的描述的同一件事情，就是指通过引入 IoC 容
器，利用依赖关系注入的方式，实现对象之间的解耦。

## Spring使用流程

![1](https://gitee.com/wang-fuming/dawning/raw/master/1.jpg)





# Spring Boot

## 项目建立

通过start.spring.io建立

## 开发说明

SpringBoot 已经集成了 Tomcat，以后就不用像传统 Web 开发那样还需要下载一个 Tomcat 程序，配
置启动了。只需要启动生成的启动类即可。

## 默认的Web资源文件夹
SpringBoot 默认会使用 src/main/resources 目录下的如下文件夹作为Web资源文件夹：

1. /static：静态资源文件夹，如html，js，css等存放
2. /public：静态资源文件夹，同上
3. /templates：模版资源文件夹（后端模版框架使用的模版文件，会解析变量后再生成动态 html，
    我们不学，了解即可）
    注：在以上路径中的资源，服务路径不需要在前边再加 /static，/public。如在 static 文件夹下的
    home.html ，服务路径为：/home.html
    如果是使用普通Maven项目搭建，可以自行创建以上文件夹，在 src/main/resources 下创建
    public 和 static 文件夹即可。

##  默认的自动扫描

SpringBoot默认会扫描启动类所在包，只要位于该包以下的使用了Spring注解的类，都可以注册到容器
中，如以前学过的@Controller，@Service等。
示例：如启动类为 org.example.Application ，则可以扫描到
org.example.controller.LoginController 中的类注解@Controller。

## 默认的配置文件

SpringBoot默认使用 src/main/resource/application.properties 作为启动的配置文件，可以自
定义如启动端口等等配置。
如果是使用普通Maven项目搭建，在 src/main/resources 下创建 application.properties ，内容
为空即可。

## 默认的应用上下文路径

SpringBoot启动的Web项目，应用上下文路径默认为 /

## 启动类

如果是使用普通Maven项目搭建，可以自行编写启动类：类上使用 @SpringBootApplication 注解：

# Spring MVC

![Snipaste_2022-02-23_16-04-02](https://gitee.com/wang-fuming/dawning/raw/master/Snipaste_2022-02-23_16-04-02.png)

**Model（模型）**是应用程序中用于处理应用程序数据逻辑的部分。

通常模型对象负责在数据库中存取数据。
**View（视图）**是应用程序中处理数据显示的部分。

通常视图是依据模型数据创建的。
**Controller（控制器）**是应用程序中处理用户交互的部分。

通常控制器负责从视图读取数据，控制用户输入，并向模型发送数据。
说明：一般现在主流的前后端分离的开发模式，后端人员不再写前端代码，我们也不学习前端，对应
MVC中View的部分，我们也就不关心了。

## 分析

### @Controller

@Controller注解标注是一个类是Web控制器，其和@Component注解等价，只不过在Web层使用，其

便于区分类的作用。

### @RequestMapping

@RequestMapping是Spring Web应用程序中最常被用到的注解之一。

在对SpringMVC进行配置的时候，需要指定请求与处理方法之间的映射关系，这时候就需要使用

@RequestMapping注解。该注解可以在控制器类的级别和其方法级别上使用。如以下控制器（注：返

回值可以参考下一章节《控制器方法的返回》）：

```java
@Controller
@RequestMapping("/mvc")
public class MVCController {
    private static final Logger logger = LoggerFactory.getLogger(MVCController.class);

    @RequestMapping("/index1")
    public String getIndex(){
        logger.error("我是index.html");
        return "redirect:/index.html";
    }

    @RequestMapping("/index2")
    public String getIndex2(){
        logger.error("我是index2.html");
        return "forward:/index.html";
    }

    @RequestMapping("/index3")
    public void getIndex4(HttpServletResponse resp) {
        logger.error("我是index3.html");
        resp.setStatus(301);
        resp.setHeader("Location", "/index.html");
    }
}
```

@RequestMapping注解能够处理的HTTP请求方法有： GET, HEAD, POST, PUT, PATCH, DELETE,
OPTIONS, TRACE 。
为了能够将一个请求映射到一个特定的HTTP方法，你需要在@RequestMapping中使用method参数声
明HTTP请求所使用的方法类型。

```java
@RequestMapping(value="/index3",method = RequestMethod.GET)
```


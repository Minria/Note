# 简介

本模块由 spring-core , spring-beans , spring-context , spring-context-support , and springexpression
(Spring Expression Language) 4 个模块组成。

# IoC和DI

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

# Spring使用流程

![1](https://gitee.com/wang-fuming/dawning/raw/master/1.jpg)





# 
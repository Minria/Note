

**JVM 执行流程**
程序在执行之前先要把java代码转换成字节码（class文件），JVM 首先需要把字节码通过一定的方式
**类加载器（ClassLoader）** 把文件加载到内存中 **运行时数据区（Runtime Data Area）** ，而字节码
文件是 JVM 的一套指令集规范，并不能直接交个底层操作系统去执行，因此需要特定的命令解析器 执
行引擎（Execution Engine）将字节码翻译成底层系统指令再交由CPU去执行，而这个过程中需要调
用其他语言的接口 本地库接口（Native Interface） 来实现整个程序的功能，这就是这4个主要组成部
分的职责与功能。

# 1. JVM中的内存区域划分

![Java运行时数据区域JDK1.8.5c3da749](https://gitee.com/wang-fuming/dawning/raw/master/Java%E8%BF%90%E8%A1%8C%E6%97%B6%E6%95%B0%E6%8D%AE%E5%8C%BA%E5%9F%9FJDK1.8.5c3da749.png)

JVM的内存从哪来？来自于操作系统，启动后从操作系统申请空间，然后在分配空间

堆（运行时常量池）:new的对象就放在堆中

方法区:加载好的类就放在方法区，静态成员也在

栈（JVM栈和本地方法栈）:局部变量

程序计数器:本质是地址，用于记录程序执行

多个线程之间公用同一份栈和方法区，每个线程有自己的栈和程序计数器

```java
Test test=new Test();
```

此时`test`在哪里？

> 如果它是局部变量就在栈上
>
> 如果它是成员变量就在堆上
>
> 如果他是静态变量在方法区

**1、如何理解基础数据类型和引用数据类型？**

引用类型保存的是一个地址，就是一个低配版的指针。通过地址找到本体

基础数据类型在内存中保存的直接是数值

**2、如何理解引用和对象？**

引用是一个地址，对象是本体，通过地址可以找到本体

**3、如何理解局部变量、成员变量以及静态变量？**

局部变量在栈上，成员变量在堆中，静态变量在方法区

**4、如何理解递归方法的执行过程？**

**5、static和普通方法的区别？**

普通方法中有this，和实例相关

static方法中没有this，和类相关

# 2. GC

## 2.1 GC要干啥

## 2.2 GC处理哪些内存

堆：**主要是回收这里的内存**

方法区：**GC也需要回收方法区的内存**，但是方法区的空间很小，数据失去作用的概率很低

栈：**不需要回收。**栈上的内存何时释放时机是明确的。

程序计数器：**不需要回收**，只是存了一个地址

## 2.3 回收的基本单位

内存的单位是字节，但是回收内存是按照对象为单位来回收

堆中存在正在使用，已经不用的以及将要使用的对象

GC主要回收已经不用的对象。

如果存在对象一半使用，一半不使用，我们认为这个是正在使用的对象

GC用来处理完全已经用完的对象、

## 3.3 回收对象的思路

通常有标记和回收两步

1）标记：找出这个对象到底需不需要回收

2）回收：把死了的对象回收回去

通常使用的标记方法

1）引用计数法[python以及php使用]

2）可达性分析[java使用]

3）针对方法区对象的回收（类对象）[和上面有差别]

通常使用的回收方法

1）标记-清楚

2）标记-复制

3）标记-整理

### 3.3.1 引用计数法

记录当前这个对象是否有对象引用，以及有几个对象引用

分配一个引用计数器，当有新的引用指向这个对象时，计数器+1

当有引用不再指向这个对象时，计数器-1

计数器为0表示该对象没有被引用了，可以被垃圾回收了

但是，具有致命的缺陷，无法解决循环引用的问题

```java
class Test{
    Test t=null;
}
public class Main{
    public static void main(String[] args){
        Test t1=new Test();//对象1
        Test t2=new Test();//对象2
        t1.t=t2;
        t2.t=t1;
        t1=null;
        t2=null;
    }
}
```

> 第一行：对象1的引用计数器值为1
>
> 第二行：对象2的引用计数器值为1
>
> 第三行：对象2的引用计数器值为2
>
> 第四行：对象1的引用计数器值为2
>
> 第五行：对象1的引用计数器值为1
>
> 第六行：对象2的引用计数器值为1

看来我们的引用计数器的值都是1不为0

但是我们以及无法找到对象1和对象2了

使用对象1->找到对象1的引用->引用在对象2中->使用对象2->找到对象2的引用->引用在对象1中->使用对象1

这样就由回到开始

### 3.3.2 可达性分析

在对象之间是有关联关系，它们构成一个有向图

遍历这个有向图，如果某个对象是可以被遍历到的，就不是垃圾

对于一棵树，我们有他的根节点就可以访问它的所有节点

如果执行`root.right=null`，右子树便不能通过根节点进行访问，就是不可达，需要回收

那么从哪里开始遍历？

首先从每个线程的每个栈帧的局部变量表

然后从常量池引用的对象

最后是静态变量引用的对象

遍历的起点不是一个，而是有很多个，把每个起点都要往下遍历

### 3.3.3 类对象回收

1）该类的所有实例都已经被回收了

2）加载该类的ClassLoader也已经被回收了

3）该类对象在代码中被使用（静态成员以及反射机制）

同时满足上面三个条件，就可认为是可以被回收的

### 3.3.4 清除

1）标记清除

标记的对象直接被释放掉

优点：简单高效

缺点：造成内存碎片问题

2）标记复制

内存区一份为2

把不是垃圾的对象，拷贝到内存区域另一边，然后整体释放这一侧的内存区域

优点：能够解决内存碎片问题，保证内存回收后不存在碎片

缺点：需要一块额外的内存空间，如果对象较多，就会比较低效

3）标记整理

保留的对象多，而删除的对象少的时候，不适合采用标记复制的方法，采用标记整理

有点类似与顺序表的删除

优点：不在像复制一样依赖更大的内存，也没有内存碎片

缺点：搬运的效率比较低，不太适合频繁的进行

## 分代回收机制

按照对象的年龄，把堆内存分为新生代、老年代

新生代分为伊甸园、生存区1、生存区2

1、对象诞生于新生代伊甸区。新对象的内存就是伊甸区的内存

2、第一轮GC扫描后，就会把大量的对象干掉，少数没有被干掉的对象就会被拷贝的生存区

3、进入生存区的对象也会被GC扫描，如果发现不可达，就会被拷贝到另一个生存区

4、对象在生存区进行若干次拷贝之后，也没有被回收，此时说明对象存活时间比较久，拷贝到老年代

5、老年代的对象也要进行GC扫描。由于老年代的对象存活时间比较稳定，扫描周期要长的很多
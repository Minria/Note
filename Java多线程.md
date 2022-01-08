

# 1. 认识线程

## 创建线程

1、run和start的区别

run就是普通的方法调用，没有创建新的线程

start是创建一个线程，并由线程来执行run方法

进程为一个工厂的话，那么线程就是工厂中的若干个流水线

1、线程是包含在进程当中的

2、一个进程中可能会有多个线程

3、每个线程都有一段自己要执行的指令，每个线程都是一个独立的“执行流”

4、同一个进程中的很多线程之间，共享一些资源

线程可以理解为一种轻量级的进程，也是一种实现并发编程的方式

创建一个线程比创建一个一个进程成本低，销毁也是如此

同一个进程的多个线程之间共享的资源主要是两个方面

1、内存资源

2、打开的文件

一些资源不会共享

1、上下文、状态、优先级、记账信息

2、栈空间，每个线程独立

创建线程的代码写法

1、通过显示继承Thread并通过重写run方法

```java
class MyThread extends Thread{
    @Override
    public void run() {
        System.out.println("hello word，这是一个线程");
    }
}
public class Main{
    public static void main(String[] args) {
        //当 Thread 对象被创建出来的时候, 内核中并没有随之产生一个线程(PCB).
        Thread myThread=new MyThread();
        //调用start后，代码执行后内核创建（线程）PCB
        //执行上面run方法的代码
        myThread.start();
    }
}
```

2、通过匿名类部类的方式并重写run方法

```java
public class Main{
    public static void main(String[] args) {
        Thread t=new Thread(){
            @Override
            public void run() {
                System.out.println("这是一个新线程");
            }
        };
        t.start();
    }    
}
```



3、显示创建一个类，实现Runnable接口，然后吧这个接口实例关联到Thread实例

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("我是一个新线程");
    }
}
public class Main {


    public static void main(String[] args) {
        Thread t=new Thread(new MyRunnable());
        t.start();
    }
}
```



4、通过匿名内部类来实现Runnable接口

```java
public class Main {
    public static void main(String[] args) {
        Runnable runnable=new Runnable() {
            @Override
            public void run() {
                System.out.println("这是一个线程");
            }
        };
        Thread t=new Thread(runnable);
        t.start();
    }
```



5、使用lambda表达式

```java
public class Main {

    public static void main(String[] args) {
        Thread t=new Thread(()-> System.out.println("这是一个新线程"));
        t.start();
    }
}
```





# 2.Thread类及常见方法

## 2.1 Thread的构造方法

| 方法                                      | 说明                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| Thread()                                  | 创建线程对象                                                 |
| Thread(Runnable target)                   | 使用 Runnable 对象创建线程对象                               |
| Thread(String name)                       | 创建线程对象，并命名                                         |
| Thread(Runnable target,String name)       | 使用 Runnable 对象创建线程对象，并命名                       |
| Thread(ThreadGroup group,Runnable target) | 线程可以被用来分组管理，分好的组即使线程组，这个目前我们了解即可 |



## 2.2 Thread的属性

| 属性         | 方法            | 说明                                                  |
| ------------ | --------------- | ----------------------------------------------------- |
| ID           | getId()         | ID 是线程的唯一标识，不同线程不会重复                 |
| 名称         | getName()       | 名称是各种调试工具用到                                |
| 状态         | getState()      | 状态表示线程当前所处的一个情况，下面我们会进一步说明  |
| 优先级       | getPriority()   | 优先级高的线程理论上来说更容易被调度到                |
| 是否后台线程 | isDaemon()      | JVM会在一个进程的所有非后台线程结束后，才会结束运行。 |
| 是否存活     | isAlive()       | 是否存活，即简单的理解，为 run 方法是否运行结束了     |
| 是否中断     | isInterrupted() | 线程的中断问题                                        |

## 2.3 中断一个线程

中断一个线程通常有两种方式

1、通过一个共享标记来结束进程

2、通过interrupt来结束一个行程

```java
public class Main{
    private static boolean isQuit=false;
    public static void main1(String[] args) {
        Thread t=new Thread(){
            public void run(){
               while(!isQuit){
                   System.out.println("正在执行");
                   try {
                       Thread.sleep(100);
                   } catch (InterruptedException e) {
                       e.printStackTrace();
                   }
               }
                System.out.println("终止执行");
            }
        };
        t.start();
        try {
            Thread.sleep(500);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("请求终止执行");
        isQuit=true;

    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Thread t=new Thread(){
            @Override
            public void run() {
                while(!Thread.currentThread().isInterrupted()){
                    System.out.println("正在执行");
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                        break;
                    }
                }
            }
        };
        t.start();
        try {
            Thread.sleep(500);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("请求终止执行");
        t.interrupt();
    }
}
```

1. 如果线程调用了 wait/join/sleep 等方法而阻塞挂起，则以 InterruptedException 异常的形式通知，清除
    中断标志
2. 否则，只是内部的一个中断标志被设置，thread 可以通过
   1. `Thread.interrupted()` 判断当前线程的中断标志被设置，**清除中断标志**
   2. `Thread.currentThread().isInterrupted()` 判断指定线程的中断标志被设置，**不清除中断标志**



## 2.4 等待一个进程

| 方法                                     | 说明                             |
| ---------------------------------------- | -------------------------------- |
| public void join()                       | 等待线程结束                     |
| public void join(long millis)            | 等待线程结束，最多等 millis 毫秒 |
| public void join(long millis, int nanos) | 同理，但可以更高精度             |

## 2.5 获取当前线程的引用

| 方法                                  | 说明                   |
| ------------------------------------- | ---------------------- |
| public static Thread currentThread(); | 返回当前线程对象的引用 |

## 2.6 休眠当前线程

因为线程的调度是不可控的，所以，这个方法只能保证休眠时间是大于等于休眠时间的。

| 方法                                                         | 说明                     |
| ------------------------------------------------------------ | ------------------------ |
| public static void sleep(long millis) throws InterruptedException | 休眠当前线程 millis 毫秒 |
| public static void sleep(long millis, int nanos) throws InterruptedException | 可以更高精度的休眠       |

# 3. 线程的状态

## 3.1 线程的所有状态

| 状态          | 说明                                 |
| ------------- | ------------------------------------ |
| NEW           | Thread对象创建，但是PCB还没有        |
| RUNNABLE      | 线程正在CPU上执行或者将要到CPU上执行 |
| WAITING       | wait导致                             |
| TIMED_WAITING | sleep方法                            |
| BLOCKED       | 等待锁                               |
| TERMINATED    | 对象还在，但是OCB对象没有了          |



## 3.2 线程的状态以及状态转移的意义

## 3.3 线程的状态转移

# 4. 线程安全问题

## 4.1 线程不安全实例

```java
public class ThreadDemo6 {
    /**
     * 各自增加1万次，理论上为2万次
     */
    static class Counter{
        public int count=0;
        public void increase(){
            count++;
        }
    }
    public static void main(String[] args) {
        Counter counter=new Counter();
        Thread t1=new Thread(){
          public void run(){
              for(int i=0;i<10000;i++){
                  counter.increase();
              }
          }
        };
        Thread t2=new Thread(){
            public void run(){
                for(int i=0;i<10000;i++){
                    counter.increase();
                }
            }
        };
        t1.start();
        t2.start();
        try {
            t1.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        try {
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(counter.count);
    }
}
```



## 4.2 线程安全的概念

线程不安全：多线程并发执行某个代码时，产生了逻辑上的错误，就是不安全

线程安全：多线程并发执行某个代码时，逻辑上没有错误，这就是线程安全

## 4.3 线程不安全的原因及解决方案

<font color="red">**1、线程是抢占式执行的----根本原因**</font>

解决方案：没有，这是操作系统内核实现的

<font color="red">**2、run方法里面的操作可能不是原子性的**</font>

解决方案：通过锁，可以实现原子性

> 以上面为例，自增需要三步，读入cpu，cpu里加一，写入内存。线程1读入0，线程2读入0，线程1CPU+1，线程2CPU+1，线程1将1写入内存，线程2将1写入内存。自增2次，但却是加了一次。通过锁可以将三步合一

<font color="red">**3、多个线程尝试修改同一个变量**</font>

解决方案：需要看需求

<font color="red">**4、内存可见性导致的不安全**</font>

<font color="red">**5、指令重排序**</font>

# 5. synchronized关键字

synchronized的底层是使用操作系统的mutex lock实现的。
1、当线程释放锁时，JMM会把该线程对应的工作内存中的共享变量刷新到主内存中

2、当线程获取锁时，JMM会把该线程对应的本地内存置为无效。从而使得被监视器保护的临界区代码必须从主内
存中读取共享变量

synchronized同步快对同一条线程来说是可重入的，不会出现自己把自己锁死的问题；

同步块在已进入的线程执行完之前，会阻塞后面其他线程的进入。

1、锁对象

```java
public class SynchronizedDemo {
	public synchronized void methond() {
	}
	public static void main(String[] args) {
		SynchronizedDemo demo = new SynchronizedDemo();
		demo.method(); // 进入方法会锁 demo 指向对象中的锁；出方法会释放 demo 指向的对象中的锁
	}
}
```

2、锁类对象

```java
public class SynchronizedDemo {
    public synchronized static void method() {
    }
    public static void main(String[] args) {
        method(); // 进入方法会锁 SynchronizedDemo.class 指向对象中的锁；出方法会释放
        //SynchronizedDemo.class 指向的对象中的锁
    }
}
```

3、明确锁的对象

```java
public class SynchronizedDemo {
    public void method() {
// 进入代码块会锁 this 指向对象中的锁；出代码块会释放 this 指向的对象中的锁
        synchronized (this) {
        }
    }
    public static void main(String[] args) {
        SynchronizedDemo demo = new SynchronizedDemo();
        demo.method();
    }
}

```


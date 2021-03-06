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

1、ID 是线程的唯一标识，不同线程不会重复
2、名称是各种调试工具用到
3、状态表示线程当前所处的一个情况，下面我们会进一步说明
4、优先级高的线程理论上来说更容易被调度到
5、关于后台线程，需要记住一点：JVM会在一个进程的所有非后台线程结束后，才会结束运行。
6、是否存活，即简单的理解，为 run 方法是否运行结束了
7、线程的中断问题，下面我们进一步说明

## 2.3 中断一个线程

中断一个线程通常有两种方式

1、通过一个共享标记来结束进程

2、通过interrupt来结束一个行程

```java
public class Main{
private static boolean isQuit=false;
    public static void main(String[] args) {
        Thread t=new Thread(){
            @Override
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

1. 如果线程调用了 wait/join/sleep 等方法而阻塞挂起，则以 InterruptedException 异常的形式通知，清除中断标志
2. 否则，只是内部的一个中断标志被设置，thread 可以通过
   1. `Thread.interrupted()` 判断当前线程的中断标志被设置，**清除中断标志**
   2. `Thread.currentThread().isInterrupted()` 判断指定线程的中断标志被设置，**不清除中断标志**

| 方法                                | 说明                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| public void interrupt()             | 中断对象关联的线程，如果线程正在阻塞，则以异常方式通知，否则设置标志位 |
| public static boolean interrupted() | 判断当前线程的中断标志位是否设置，调用后清除标志位           |
| public boolean isInterrupted()      | 判断对象关联的线程的标志位是否设置，调用后不清除标志位       |



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

![dxc1](../picture/java/dxc1.png)

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
// 进入代码块会锁 this 指向对象中的锁；出代码块会释放this指向的对象中的锁
        synchronized (this) {
        }
    }
    public static void main(String[] args) {
        SynchronizedDemo demo = new SynchronizedDemo();
        demo.method();
    }
}

```

# 6. volatile关键字

修饰的共享变量，可以保证可见性，部分保证顺序性

```java
class ThraedDemo {
	private volatile int n;
}
```

```JAVA
public class ThreadDemo7 {
    static class Counter{
        public volatile int count=0;
    }
    public static void main(String[] args) {
        Counter counter=new Counter();
        Thread t1=new Thread(){
            @Override
            /**
             * 线程1的核心代码中，循环什么也没有干，只是在反复的快速地的比较循环条件
             * 在当前线程中并没有改变count的值，所以编译器错误的优化了以后直接从cpu中读取数据
             * 其他线程改变内存的数据后，但是线程1已经不会从内存中读取数据了
             * 可以通过valatile禁止优化
             * 使用场景：一个线程读，一个线程写，就需要使用valatile来防止优化
             * 对于两个线程同时写无法使用这个来解决，只能用锁来解决
             */
            public void run() {
                while(counter.count==0){
                }
                System.out.println("线程1结束了");
            }
        };
        t1.start();
        Thread t2= new Thread(() -> {
            Scanner scanner=new Scanner(System.in);
            System.out.print("输入一个整数>>");
            counter.count=scanner.nextInt();

        });
        t2.start();
    }
}
```

# 7. 对象的等待集

1、wait()的作用是让当前线程进入等待状态，同时，wait()也会让当前线程释放它所持有的锁。“直到其他线程调用此对象的 notify() 方法或 notifyAll() 方法”，当前线程被唤醒(进入“就绪状态”)

2、notify()和notifyAll()的作用，则是唤醒当前对象上的等待线程；notify()是唤醒单个线程，而notifyAll()是唤醒所有的线程。

3、wait(long timeout)让当前线程处于“等待(阻塞)状态”，“直到其他线程调用此对象的notify()方法或 notifyAll() 方法，或者超过指定的时间量”，当前线程被唤醒(进入“就绪状态”)。

```java
public class ThreadDemo8 {

    public static void main(String[] args) {
        Object locker = new Object();

        Thread t1 = new Thread() {
            @Override
            public void run() {
                synchronized (locker) {
                    while (true) {
                        try {
                            System.out.println("wait 开始");
                            locker.wait();
                            System.out.println("wait 结束");
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                }
            }
        };

        Thread t2 = new Thread() {
            @Override
            public void run() {
                Scanner scanner = new Scanner(System.in);
                System.out.println("输入任意一个整数, 继续执行 notify");
                int num = scanner.nextInt();
                synchronized (locker) {
                    System.out.println("notify 开始");
                    locker.notify();
                    System.out.println("notify 结束");
                }
            }
        };
        t2.start();
        t1.start();
    }
}
```

1、wait()的作用是使当前执行代码的线程进行等待，wait()方法是Object类的方法，该方法是用来将当前线程
置入“预执行队列”中，并且在wait()所在的代码处停止执行，直到接到通知或被中断为止。

2、wait()方法只能在同步方法中或同步块中调用。如果调用wait()时，没有持有适当的锁，会抛出异常。

3、wait()方法执行后，当前线程释放锁，线程与其它线程竞争重新获取锁。

4、方法notify()也要在同步方法或同步块中调用，该方法是用来通知那些可能等待该对象的对象锁的其它线程，对
其发出通知notify，并使它们重新获取该对象的对象锁。如果有多个线程等待，则有线程规划器随机挑选出一个
呈wait状态的线程。

5、在notify()方法后，当前线程不会马上释放该对象锁，要等到执行notify()方法的线程将程序执行完，也就是退出同步代码块之后才会释放对象锁。

需要注意的是：

wait，notify必须使用在synchronized同步方法或者代码块内。

wait会有三步操作，释放锁，等待通知，尝试重新获取锁

notify也有三步操作，获取锁，通知，然后释放锁

如果释放锁之后，notify通知在wait的等待通知之前，那么是不是就错过通知了？

不，wait的前两步是原子性的，确保能接受通知。要是在wait释放锁通知就会造成死锁

# 8. 多线程案例

## 8.1 单例模式

顾名思义，就是这个类只有一个实例对象

分为饿汉模式和懒汉模式

前者在类加载的时候就会有实例，后者在需要的时候就会有实例

饿汉模式代码

```java
public class Singleton{
    //构造方法私有化就不能通过new构造实例
    private Singleton(){}
    //在类加载的时候就实例化
    Singleton insetance=new Singleton();
    public Singleton getInsetance(){
        return insetance;
    }
}
```

懒汉模式代码

```java
public class Singleton{
    private Singleton(){}
    Singleton instance=null;
    public Singleton getInsetance(){
        if(instance==null){
            instance=new Singleton();
        }
        return instance;
    }
}
```

但是懒汉模式这样写是不安全的，上文中有

线程不安全的原因就是多个变量尝试同时修改一个变量时，那么他可能就是线程不安全的

对于饿汉模式，多个线程尝试读取一个变量，这线程安全

对于懒汉模式，当类没有实例化的时候，就会有多少线程修改，这不安全，在实例化后就会安全

那么加上锁就好了

```java
public class Singleton{
    private Singleton(){}
    Singleton instance=null;
    public  static Singledog getInstance(){
        synchronized (Singledog.class){
            if (instance==null){
                instance = new Singledog();
            }
            return instance;
        }
    }
}
```

但是，加上锁之后就和高性能没有关系，需要减小锁的范围

```java
public class Singleton{
    private Singleton(){}
    Singleton volatile instance=null;
	public Singledog getInstance() {
        if(instance==null){
            synchronized (Singledog.class){
                if (instance==null){
                    instance=new Singledog();
                }
            }
        }
        return instance;
    }
}
```

## 8.2 阻塞队列

生产者消费者模式，

```java
public class BlockingQueue{
    private int[] array=new int[1000];
    private int front=0;
    private int rear=0;
//    private int size=0;
    //防止频繁读取而优化
    private volatile int size=0;
    public BlockingQueue(){};
        public void put(int value){
            synchronized (this){
                while(size==array.length){
                    try {
                        wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                array[rear]=value;
                rear++;
                if(rear==array.length){
                    rear=0;
                }
                size++;
                notify();
            }
        }
        public int take(){
            synchronized (this){
                while(size==0){
                    try {
                        wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                int ans=array[front];
                front++;
                if(front==array.length){
                    front=0;
                }
                size--;
                notify();
                return ans;
            }
        }
    
}
```

需要注意的是：

1、原先队列满入队的执行逻辑是返回空，队列空出队的逻辑是返回-1，现在就是让线程等待

2、线程等待后当其他线程执行入队，出队的操作后，需要通知前面的等待结束

3、留意等待处罚的条件，不会出现死锁问题

4、操作不是原子性的，需要加上锁让他的操作变成原子性

## 8.3 定时器

定时器构成要素

1、使用一个Task来描述任务，同时要记录任务执行时间（里面有一个Runnable和时间，由于需要排序所以要加一个接口）

2、使用一个阻塞优先队列，来组织我们的任务

3、一个工作线程来扫描任务时间，检测队首任务的执行时间，如果需要执行的化就去执行任务

4、一个类用来启动定时器以及向里面添加任务

```java
public class Task implements Comparable<Task>{
    //通过Runnable来描述任务
    public Runnable command;
    private long time;
    //这里的after是相对时间，描述多少时间后执行任务
    public Task(Runnable command,long after){
        this.command=command;
        this.time=System.CurrentTimes()+after;
    }
    //任务执行
    public void run(){
        command.run():
    }
    //比较接口，便于在在阻塞队列中进行比较
    public int compareTo(Task o){
        return (int)(this.time-o.time);
}
public class Work extends Thread {
    private PriorityBlockingQueue<Task> queue = null;
    private Object mailBox = null;
    //需要将队列传输进行进行扫描，锁的作用在下文
    public Worker(PriorityBlockingQueue<Task> queue, Object mailBox) {
        this.queue = queue;
        this.mailBox = mailBox;
    }
    @Override
    public void run() {
        // 实现具体的线程执行的内容
        while (true) {
            try {
                // 1. 取出队首元素, 检查时间是否到了
                Task task = queue.take();
                // 2. 检查当前任务时间是否到了
                long curTime = System.currentTimeMillis();
                if (task.time > curTime) {
                    // 时间还没到~, 就把任务再塞回队列中
                    queue.put(task);
                    //我们已经知道还有多长时间执行任务，就不要一直扫描了。
                    //将他锁住，知道时间到了，或者有了新任务进来
                    synchronized (mailBox) {
                        /**
                         * 加上时间就不会一直等，到时间就不等了
                         * 有了新任务也需要扫描
                         */
                        mailBox.wait(task.time - curTime);
                    }
                } else {
                    task.run();
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
                break;
            }
        }
    }
}

public class Timer{
    PriorityBlockingQueue<Task> queue=new PriorityBlockingQueue<>();
    Object blocker=new Object();
    Public Timer(){
        Work work=new Work(queue,blocker);
        work.start();
    }
    //这是一个接口，需要t
    public void schedule(Runnable command, long after) {
        Task task = new Task(command, after);
        queue.put(task);
        synchronized (mailBox) {
            //有了新任务就要去通知解除等待
            mailBox.notify();
        }
    }
}
```

## 8.4 线程池

具体操作：

1、execute：将任务加入线程池

2、shutdown：销毁线程池

线程池组成部分：

1、工作类，表示工作线程

2、一个类描述线程的具体工作是什么（借助Runnable接口）

3、用一个数据结构来组织任务，用阻塞队列

4、用一个数据结构在组织若干个线程，线性表

```java
public class MyThreadPool{
    BlockQueue<Runnable> queue=new BlockQueue<>();
    List<Work> list=new ArrayList<>();
    public void execute(Runnable command){
        if(list.size()<10){
            Work work=new Work();
            work.start():
            list.add(work);
        }
        queue.put(command);
    }
     public void shutdown() throws InterruptedException {
            // 终止掉所有的线程.
         for (Work work : list) {
             worker.interrupt();
         }
            // 还需要等待每个线程执行结束.
         for (Work work : list) {
             work.join();
         }
     }
}
public class Work expends Thread{
    BlockQueue<Runnable> queue=null;
    public Work(BlockQueue<Runnable> queue){
        this.queue=queue;
    }
    public void run(){
        try{
            while(!Thread.currentThread().isInterrupted()){
                Runnable command=queue.take();
                command.run();
            }
        }catch (InterruptedException e){
            System.out.println("线程终止");
        }            
    }
        
}
```

# 9. 常见锁策略

## 9.1 乐观锁VS悲观锁

乐观锁：乐观锁假设认为数据一般情况下不会产生并发冲突，所以在数据进行提交更新的时候，才会正式对数据是

否产生并发冲突进行检测，如果发现并发冲突了，则让返回用户错误的信息，让用户决定如何去做。

悲观锁：总是假设最坏的情况，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样

别人想拿这个数据就会阻塞直到它拿到锁。

悲观锁的问题：总是需要竞争锁，进而导致发生线程切换，挂起其他线程；所以性能不高。

乐观锁的问题：并不总是能处理所有问题，所以会引入一定的系统复杂度。

乐观锁：多个线程竞争一把锁的概率会很低（效率高）

悲观锁：多个线程竞争一把锁的概率会很高（安全高）

## 9.2 读写锁

多线程之间，数据的读取方之间不会产生线程安全问题，但数据的写入方互相之间以及和读者之间都需要进行互

斥。如果两种场景下都用同一个锁，就会产生极大的性能损耗。所以读写锁因此而产生。

读写锁（readers-writer lock），看英文可以顾名思义，在执行加锁操作时需要额外表明读写意图，复数读者之间

并不互斥，而写者则要求与任何人互斥。

加锁操作分为两个步骤读锁和写锁

读锁与读锁之间是没有互斥的，也就是不存在锁竞争

读锁和写锁、写锁和写锁之间才是互斥的

场景：一写多读

## 9.3 重量级锁VS轻量级锁

加锁需要保证原子性。原子性功能来自与硬件操作。

在加锁过程中，如果整个加锁操作都是依赖操作系统内核，这就是重量级锁。（代码在内核执行开销大）

大部分操作都是用户都是自己完成，少数操作有内核完成。这就是轻量级锁

## 9.4 挂起等待锁VS自旋锁

挂起等待锁表示当前取锁失败后，对应的线程就要在内核中挂起（放弃CPU，进入等待队列），需要在锁释放后由操作系统唤醒。（通常是重量级锁）

自旋锁表示在获取锁失败后，不会立即放弃CPU，而是快速频繁询问锁的持有状态，一旦锁被释放，就能立刻获取到锁。（通常是轻量级锁。）

## 9.5 公平锁VS非公平锁

当锁释放之后，恰好又来了一个新的线程也要获取锁。

公平锁：保证之前先来的线程优先获取到锁

非公平锁：新来的线程直接获取到锁，之前的线程继续等待。

## 9.6 可重复锁

可重入锁的字面意思是“可以重新进入的锁”，即允许同一个线程多次获取同一把锁。

比如一个递归函数里有加锁操作，递归过程中这个锁会阻塞自己吗？

如果不会，那么这个锁就是可重入锁（因为这个原因可重入锁也叫做递归锁）。

Java里只要以Reentrant开头命名的锁都是可重入锁，而且JDK提供的所有现成的Lock实现类，包括synchronized

关键字锁都是可重入的。

一个线程针对一把锁，连续加锁两次，不会死锁。

死锁：

一个线程针对一把锁联系加锁两次

两个线程针对两把锁分别加锁

N个线程针对N把锁分别加锁

# 10. CAS

compare and swap（比较并交换）

```
我们假设内存中的原数据V，旧的预期值A，需要修改的新值B。 1. 比较 A 与 V 是否相等。（比较） 2. 如果
比较相等，将 B 写入 V。（交换） 3. 返回操作是否成功。
```

当多个线程同时对某个资源进行CAS操作，只能有一个线程操作成功，但是并不会阻塞其他线程,其他线程只会收到操作失败的信号。可见 CAS 其实是一个乐观锁。

应用场景

无锁编程：不使用锁，而是使用CAS来保证线程安全

## CAS 是怎么实现的

针对不同的操作系统，JVM 用到了不同的 CAS 实现原理，简单来讲：

1. java 的 CAS 利用的的是 unsafe 这个类提供的 CAS 操作；
2. unsafe 的 CAS 依赖了的是 jvm 针对不同的操作系统实现的 Atomic::cmpxchg；
3. Atomic::cmpxchg 的实现使用了汇编的 CAS 操作，并使用 cpu 硬件提供的 lock 机制保证其原子性。

简而言之，是因为硬件予以了支持，软件层面才能做到。

## CAS的应用

```java
//实现自旋锁
public class SpinLock {
	private AtomicReference<Thread> sign =new AtomicReference<>();
    public void lock(){
		Thread current = Thread.currentThread();
		// 不放弃 CPU，一直在这里旋转判断
		while(!sign .compareAndSet(null, current)){
		}
	}
	public void unlock (){
		Thread current = Thread.currentThread();
		sign.compareAndSet(current, null);
	}
}
//实现原子类
public class AtomicInteger {
	public final int incrementAndGet() {
		return unsafe.getAndAddInt(this, valueOffset, 1) + 1;
	}
}
public class Unsafe {
	public final int getAndAddInt(Object var1, long var2, int var4) {
		int var5;
		do {
			var5 = this.getIntVolatile(var1, var2);
		} while(!this.compareAndSwapInt(var1, var2, var5, var5 + var4));
		return var5;
	}
}
```

## ABA问题

ABA 的问题，就是一个值从A变成了B又变成了A，而这个期间我们不清楚这个过程。
解决方法：加入版本信息，例如携带 AtomicStampedReference 之类的时间戳作为版本信息，保证不会出现老的
值。

# 11. 锁优化-sychronized

```
面试题:
1. 什么是偏向锁?

2. java 的 synchronized 是怎么实现的，有了解过么？

3. synchronized 实现原理 是什么？
```

一些提高锁优化的策略

1、锁消除：编译器+JVM会根据代码运行的情况只能判断锁是否必要。

2、偏向锁：第一个尝试加锁的线程，不会真的加锁，而是进入偏向锁状态。直到其他线程来竞争这个锁的时，才会取消这个状态，真正进行加锁。

3、自旋锁：真的多个线程竞争锁的时候，偏向锁状态被消除，此刻线程使用自旋锁的方式尝试获取锁

4、锁膨胀：锁竞争更加激烈的时候，就会从自旋锁状态膨胀为重量级锁（挂起等待锁）

5、锁粗化：如果段逻辑中，需要多次加锁解锁，并且在解锁的过程中没有其他的线程进行竞争，就会把多组加锁合并在一起。

## JUC

1、原子类

```java
java.util.concurrent.atomic
```

2、locks 包含了其他的锁

3、Callable/Future/FutureTask

创建线程的方式

1. 直接创建类，继承Thread，重写run方法（具名类/匿名类）
2. 创建Runnable接口，重写run方法，设置到Thread中（具名类/匿名类）
3. 使用lambda表达式
4. 使用Callable搭配FutureTask创建线程

```java
Callable<Integer> callable = new Callable<>(){
    @Override
    public Integer call(){
        int ret=0;
        for(int i=0;i<100;i++){
            ret+=i;
        }
        return ret;
    }
}
```

4、Executors/ExectorService ThreadPoolExecutor

5、Semaphore信号量

# 12.线程安全集合类

Vector，Srack，HashTable线程安全，其他的线程不安全

对于ArrayList来说

自己加锁或者Collection.sychronizedList

对于HashMap来说

自己加锁，HashTable，ConcurrentMap

# 面试

其实理论上 wait 和 sleep 完全是没有可比性的，因为一个是用于线程之间的通信的，一个是让线程阻塞一段时间，
唯一的相同点就是都可以让线程放弃执行一段时间。用生活中的例子说的话就是婚礼时会吃糖，和家里自己吃糖之间
有差别。说白了放弃线程执行只是 wait 的一小段现象。
当然为了面试的目的，我们还是总结下：
1. wait 之前需要请求锁，而wait执行时会先释放锁，等被唤醒时再重新请求锁。这个锁是 wait 对像上的 monitor
lock
2. sleep 是无视锁的存在的，即之前请求的锁不会释放，没有锁也不会请求。
3. wait 是 Object 的方法
4. sleep 是 Thread 的静态方法



11.1 线程的优点
1. 创建一个新线程的代价要比创建一个新进程小得多
2. 与进程之间的切换相比，线程之间的切换需要操作系统做的工作要少很多
3. 线程占用的资源要比进程少很多
4. 能充分利用多处理器的可并行数量
5. 在等待慢速I/O操作结束的同时，程序可执行其他的计算任务
5. 计算密集型应用，为了能在多处理器系统上运行，将计算分解到多个线程中实现
7. I/O密集型应用，为了提高性能，将I/O操作重叠。线程可以同时等待不同的I/O操作。

11.2 进程与线程的区别
1. 进程是系统进行资源分配和调度的一个独立单位，线程是程序执行的最小单位。
2. 进程有自己的内存地址空间，线程只独享指令流执行的必要资源，如寄存器和栈。
3. 由于同一进程的各线程间共享内存和文件资源，可以不通过内核进行直接通信。
4. 线程的创建、切换及终止效率更高。

```
1、**说下乐观锁悲观锁**
2、object类的原生方法有哪些？
3、说下b树和b+树
4、**说下hashmap实现原理，为什么线程不安全？**
5、**Concurrenthashmap如何实现线程安全？**
6、**Concurrenthashmap在jdk1.8做了哪些优化？**
7、知道BIO和NIO吗？
8、仔细讲讲Websockt
9、说说Tcp断开连接的过程
10、Hashcode方法有什么作用？
12、说下equals和＝＝的区别
13、如果判断一个链表有环，环的入口在哪
14、一共100个乒乓，每次拿一到六个，我和你轮流拿，能拿到最后一个球的人获胜，你先拿，你怎么才能赢？
15、有4个g的数据，给你256m的空间，怎么把它排序，然后写进另一个文件里？
16、知道类加载器吗？有哪些？说说类加载机制
17、你知道哪些异常？说说异常的执行过程
18、**你自己如何实现一个线程池，要用什么数据结构？**
19、**知道threatlocal吗？说一下原理**
20、用过哪些数据库，MySQL如何保证安全？有哪些锁？
21、静态方法和实例方法的区别，在内存中存放的位置
22、说下http协议，http1.0、http1.1、http2.0有什么区别？https呢？如何保证安全的？
```


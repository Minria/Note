[TOC]



# JavaSE

## 八大基本数据类型

### 1.1 整型(4)

基本语法格式

```java
byte num1=1;
short nums=1;
int num3=1;
long num4=1L;//后面有一个L,可以不带
```

在Java中，int占有4个字节，与操作系统无关

```java
System.out.println(Integer.MAX_VALUE);//整型数据最大值
System.out.println(Integer.MIN_VALUE);//整型数据最小值
```

如果对其进行+1或者-1操作就会溢出报错

### 1.2 浮点型(2)

基本语法格式

```java
float num1=10.1F;//这个后面不带Fh
double num2=10.1;
```

在 Java 中, int 除以 int 的值仍然是 int，后面的小数点被舍去，如果需要得到小数，就需要转换为浮点数进行运算

### 1.3 字符类型(1)

基本语法格式

```java
char name = data;
```

实例

```JAVA
char ch = 'A';
char ch = '啊';
```

需要注意的是，**Java中字符类型占两个字节**，与C语言中所占一个字节有区别

### 1.4 布尔类型变量(1)

基本语法格式

```java
boolean name = data;
```

实例

```java
boolean value = true;
boolean value = false;
```

**注意**

1. boolean 类型的变量只有两种取值, true 表示真, false 表示假.
2. Java 的 boolean 类型和 int 不能相互转换, 不存在 1 表示 true, 0 表示 false 这样的用法.
3. boolean 类型有些 JVM 的实现是占 1 个字节, 有些是占 1 个比特位, 这个没有明确规定.

### 1.5 BigInteger and BigDecimal

```java
	BigInteger add(BigIntger o)
    BigInteger subtract(BigIntger o)
    BigInteger multiply(BigIntger o)
    BigInteger divide(BigIntger o)
    BigInteger mod(BigIntger o)
    BigInteger compareTo(BigIntger o)
    static BigInteger valueOf(long x)
    BigDecimal add(BigDecimal o)
    BigDecimal subtract(BigDecimal o)
    BigDecimal multiply(BigDecimal o)
    BigDecimal divide(BigDecimal o)
    BigDecimal mod(BigDecimal o)
    BigDecimal compareTo(BigDecimal o)
    static BigDecimal valueOf(long x)
    static BigDecimal valueOf(long x,int scale)
```

 

## String类型变量

在C语言中没有字符串类型，但是在Java中有字符串类型

```java
String name = "data";
```

区分

```java
char ch='A';
String str="A";
```

**注意**

1. Java 使用 双引号 + 若干字符 的方式表示字符串字面值。
2. 和上面的类型不同, String 不是基本类型, 而是引用类型。
3. 字符串中的一些特定的不太方便直接表示的字符需要进行转义

### 2.1 字符串的创建

```java
String str1 = "abcdefg";
String str2 = new String("abcdefg");
char[] array = {'a','b','c'};
String str3 = new String(array);
```

###  2.2 字符串相等的比较

```java
String str1 = "abcdefhg";
String str2 = "abcdefhg";
System.out.println(str1==str2);
System.out.println(str1.equals(str2));
System.out.println("abcdefhg"==str2);
System.out.println("abcdefhg".equals(str1));
```

### 2.3 字符串的不可变性

双引号引起的是字面值常量，无法修改

### 2.4 字符与字符串

字符串内部包含一个字符数组，String 可以和 char[] 相互转换.

```java
public String(char[] value);
//将字符数组中的内容变为字符串
public String(char[] value,int offset,int count);
//将字符数组的部分内容变为字符串
public char charAt(int index);
//获得指定索引位置的字符，索引从0开始
public char[] toCharArray();
//将字符串变为字符数组返回
```

### 2.5 字节与字符串

```java
public String(byte bytes[]);
//将字节数组中的内容变为字符串
public String(byte bytes[],int offset,int count);
//将字节数组的部分内容变为字符串
public byte[] getBytes();
//字符串以字节的形式返回
```

### 2.6 字符串的常见的操作

**字符串比较**

```java
//区分大小写比较
public boolean equals(Object anObject);
//不区分大小写比较
public boolean equalsIgnoreCase(String anotherString);
//比较两个字符串大小关系
public int compareTo(String anotherString);
```

**字符串查找**

```java
//判断子字符串是否存在
public boolean contains(CharSequence s);
//查找子串的起始位置，没有返回-1
public int indexOf(String s);
//指定起始位置查询
public int indexOf(String s,int fromIndex);
//后向前查找
public int lastIndexOf(String s);
//从指定位置后向前查找
public int lastIndexOf(String s,int fromIndex);
//判断是否以指定字符串开头
public boolean starsWith(String prefix);
//从指定位置判断是否以指定字符串开头
public boolean starsWith(String prefix,int toffset);
//判断是否指定字符串结尾
public boolean endsWith(String suffix);
```

**字符串替换**

```java
//替换所有
public String replaceAll(String regex,String replacement);
//替换第一个
public String replaceFirst(String regex,String replacement);
```

**字符串拆分**

```java
//将字符串全部拆分
public String[] split(String regex);
//将字符串部分拆分
public String[] split(String regex,int limit);
```

**字符串截取**

```java
public String substring(int beginIndex);
public String sunstring(int beginIndex,int endIndex);
```

**其他操作方法**

```java
public String trim();//清理前后空格
public String toUpperCase();//字符串转大写
public String toLowerCase();//转小写
public native String intern();//字符串入池
public String concat(String str);//字符串连接，不入池
public int length();
public boolean isEmpty();
```

###  2.7 StringBuilder与StringBuffer

字符串是不可变的那么字符串的拼接是怎么完成的

这么是一个例子

```java
    public static void main(String[] args) {
        String str="abcdefg";
        for(int i=0;i<10;i++){
            StringBuilder sb=new StringBuilder();
            sb.append(str).append(i);
            str=sb.toString();
        }
        System.out.println(str);
    }
```

我们可以看到在拼接的过程中产生了大量的临时对象，对其进行改进

```java
    public static void main(String[] args) {
        StringBuilder sb=new StringBuilder();
        String str="abcdefg";
        sb.append(str);
        for(int i=0;i<10;i++){
            sb.append(i);
        }
        str=sb.toString();
        System.out.println(str);
    }
```

在此过程仅有一个对象，当在循环内进行大量拼接时，建议使用StringBuilder进行拼接

### 2.8  转义字符

| 字符 | 意义       |
| ---- | ---------- |
| \n   | 换行       |
| \t   | 水平制表符 |
| \\'  | 单引号     |
| \\"  | 双引号     |
| \\\  | 反斜杠     |

## 3. 常量

### 3.1 字面值常量

```java
10 // int 字面值常量(十进制)
010 // int 字面值常量(八进制) 由数字 0 开头. 010 也就是十进制的 8
0x10 // int 字面值常量(十六进制) 由数字 0x 开头. 0x10 也就是十进制的 16
10L // long 字面值常量. 也可以写作 10l (小写的L)
1.0 // double 字面值常量. 也可以写作 1.0d 或者 1.0D
1.5e2 // double 字面值常量. 科学计数法表示. 相当于 1.5 * 10^2
1.0f // float 字面值常量, 也可以写作 1.0F
true // boolen 字面值常量, 同样的还有 false
'a' // char 字面值常量, 单引号中只能有一个字符
"abc" // String 字面值常量, 双引号中可以有多个字符.
```

### 3.2 final修饰常量

```java
final int a = 10;
a = 20; // 编译出错,提示无法为最终变量a分配值
```

> 有点类似C语言中的const修饰变量
>
> java: 无法为最终变量a分配值

### 3.3 类型转换

**int和long/double相互转换**

```java
int a = 10;
long b =20;
a = b;// 编译出错, 提示可能会损失精度.
b = a;// 编译通过
int a = 10;
double b = 1.0;
a = b; // 编译出错, 提示可能会损失精度.
b = a; // 编译通过.
```

long 表示的范围更大, 可以将 int 赋值给 long, 但是不能将 long 赋值给 int.

double 表示的范围更大, 可以将 int 赋值给 double, 但是不能将 double 赋值给 int.

结论: **不同数字类型的变量之间赋值, 表示范围更小的类型能隐式转换成范围较大的类型, 反之则不行.**

**强制类型转换**

```java
int a = 0;
double b = 10.5;
a = (int)b;
int a = 10;
boolean b = false;
b = (boolean)a; // 编译出错, 提示不兼容的类型.
```

结论:使用 (类型) 的方式可以将 double 类型强制转成 int. 但是

1. 强制类型转换可能会导致精度丢失. 如刚才的例子中, 赋值之后, 10.5 就变成 10 了, 小数点后面的部分被忽略.
2. 强制类型转换不是一定能成功, 互不相干的类型之间无法强转.

总结：

1. 不同数字类型的变量之间赋值, 表示范围更小的类型能隐式转换成范围较大的类型.
2. 如果需要把范围大的类型赋值给范围小的, 需要强制类型转换, 但是可能精度丢失.
3. 将一个字面值常量进行赋值的时候, Java 会自动针对数字范围进行检查.

**数值提升**

**int和long混合运算**

```java
int a=10;
long b=20;
int c=a+b;
long d=a+b;
```

**byte和byte的运算**

```java
byte a = 10;
byte b = 20;
byte c = a + b;
System.out.println(c);
```



## 4. 方法

Java中的方法实质上就是C语言中的函数.

### 4.1 方法的重载

```java
public class Main {
    public static void main(String[] args) {
        int a = 10;
        int b = 20;
        int ret = add(a, b);
        System.out.println("ret = " + ret);
        double a2 = 10.5;
        double b2 = 20.5;
        double ret2 = add(a2, b2);
        System.out.println("ret2 = " + ret2);
        double a3 = 10.5;
        double b3 = 10.5;
        double c3 = 20.5;
        double ret3 = add(a3, b3, c3);
        System.out.println("ret3 = " + ret3);
    }
    public static int add(int x, int y) {
        return x + y;
    }
    public static double add(double x, double y) {
        return x + y;
    }
    public static double add(double x, double y, double z) {
        return x + y + z;
    }
}
```

> ret = 30
> ret2 = 31.0
> ret3 = 41.5

方法的名字都叫 add. 但是有的 add 是计算 int 相加, 有的是 double 相加; 有的计算两个数字相加, 有的是计算三个数字相加.

同一个方法名字, 提供不同版本的实现, 称为**方法重载**

需要注意的是

1. 方法名相同
2. 方法的参数不同(参数个数或者参数类型)
3. 方法的返回值类型不影响重载.

区分的重点是函数名字后面的参数（类型或者数量）

## 5. 数组

### 5.1 数组是什么

数组本质上就是一组相同数据类型的数据结构。

### 5.2 创建数组

Java数组创建和C语言有所不同。

下面以整型数组为例

```java
int[] nums1 = new int[]{1,2,3};//1>>>动态初始化
int[] nums2 = new int[3];//2>>>长度为3，默认初始化为0
int[] arr1 = {1,2,3};//3>>>静态初始化
int[] arr2 = new int[n];//可以要求n不是常量
int[][] nums3 = new int[][]{{1,2,3},{1,2,3}};
int[][] nums4 = new int[2][3];
int[][] arr3 = {{1,2,3},{1,2,3}};
```

需要注意的是：

1. 定义数组的时候不能写具体的数字，如`int[3] num={1,2,3};`
2. 动态初始化的第二个[]也不能写具体数字，如`int [] num=new int[3]{1,2,3};`

### 5.3 数组使用

一般是获取数组长度以及根据下标访问数组

需要注意的是

1. 在Java中使用.length得到数组的长度
2. 下标访问不可越界,范围是[0,arr.length)

**有关二维数组长度**

```java
int[][] nums={{1,2,3},{2,4,5}};
int m=nums.length;//行
int n=nums[0].length;//列
```

**遍历数组**

常见有三种实现方式

1. 通过for-i循环实现
2. 通过for-each循环实现
3. 通过Arrays类中自带的功能实现

显现附上代码

```java
    public static void main(String[] args) {
        int[] array={1,2,3,4,5,6};
        //for-i循环
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i]+" ");
        }
        System.out.println();
        //for-each循环
        for (int x:array) {
            System.out.print(x+" ");
        }
        System.out.println();
        //Arrays功能，可以自行查看
        System.out.println(Arrays.toString(array));
    }
```

> 1 2 3 4 5 6 
> 1 2 3 4 5 6 
> [1, 2, 3, 4, 5, 6]

对于二维数组

```java
    public static void main(String[] args) {
        int[][] nums={{1,2,3},{4,5,6}};
        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < nums[0].length; j++) {
                System.out.print(nums[i][j]+" ");
            }
            System.out.println();
        }
        System.out.println("--------------------------------");
        for (int[] ret: nums) {
            for(int x: ret)
                System.out.print(x+" ");
            System.out.println();
        }
        System.out.println("--------------------------------");
        System.out.println(Arrays.deepToString(nums));
    }
```

> 1 2 3 
>
> 4 5 6 
> --------------------------------
>
> 1 2 3 
>
> 4 5 6 
> --------------------------------
>
> [[1, 2, 3], [4, 5, 6]]

区别：for循环可以拿到下标，而后者不能拿到下标，更多用到访问集合中的元素

**二维数组的不规则性**

### 5.4 数组和方法

**数组作为方法的参数**

最长的就是写一个函数打印内容

附上一个实现的代码

```java
    public static void main(String[] args) {
        int[] arr={1,2,3,4,5,6};
        printfArr(arr);
    }
    public static void printfArr(int[] nums){
        for (int x: nums) {
            System.out.print(x+" ");
        }
    }
```

> 1 2 3 4 5 6 

**Java中的应用类型**

在C语言中有传值调用还有传值调用

```java
    public static void main(String[] args) {
        int num=10;
        changeNum(num);
        System.out.println(num);
    }
    public static void changeNum(int x){
        x=0;
    }
```

在执行完后num的值仍然为10，而不会改变称为0。

```java
    public static void main(String[] args) {
        int[] arr={0,0,0,0,0,0};
        changeArr(arr);
        for (int x:
             arr) {
            System.out.print(x+" ");
        }
    }
    public static void changeArr(int[] arr){
        arr[0]=1;
        arr[1]=2;
    }
```

> 1 2 0 0 0 0 

通过数组引用却又改变了数值，对应了C语言中的传址调用。

**数组作为方法的返回值**

```java
public static void main(String[] args) {
        String s=getStr();
        System.out.println(s);
    }

    public static String getStr() {
        String s="abcdefg";
        return s;
    }
```

> abcdefg

如果是整型数组，返回类型由`String`改变为`int[]`

如果是浮点型数组，改变为`double[]`

###  Arrays方法

1. fill函数（填充函数）

```java
    public static void main(String[] args) {
        int[] arr1=new int[10];
        int[] arr2=new int[10];
        Arrays.fill(arr1,1);//将所有元素填充为1
        Arrays.fill(arr2,1,3,9);//将下标[1,3)填充为9
        System.out.println(Arrays.toString(arr1));
        System.out.println(Arrays.toString(arr2));
    }
```

> [1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
> [0, 9, 9, 0, 0, 0, 0, 0, 0, 0]

2. sort排序函数

```java
    public static void main(String[] args) {
        int[] arr={1,2,1,4,3,90,3452,21,23,2,34,6,5,78};
        Arrays.sort(arr);
        System.out.println(Arrays.toString(arr));
    }
```

>  [1, 1, 2, 2, 3, 4, 5, 6, 21, 23, 34, 78, 90, 3452]

3. copyOf()拷贝函数和clone()克隆

```java
	public static void main(String[] args) {
        int[] arr1={1,2,3,4,5,6,7};
        int[] arr2=Arrays.copyOf(arr1,arr1.length);//拷贝所有
        int[] arr3=Arrays.copyOfRange(arr1,1,3);//拷贝下标[1,3)之间的元素
        int[] arr4=arr1.clone();//拷贝所有
        System.out.println(Arrays.toString(arr2));
        System.out.println(Arrays.toString(arr3));
        System.out.println(Arrays.toString(arr4));
    }
```

> [1, 2, 3, 4, 5, 6, 7]
> [2, 3]
> [1, 2, 3, 4, 5, 6, 7]

## 6. 面向对象

### 6.1 类和对象

#### 类

类是构造对象的模板或蓝图。由类构造对象的过程称为创建类的实例。

类的成员可以包含以下：

1. 字段、属性或者成员，又分普通成员变量和静态成员变量

   普通成员变量：属于对象，放在堆区，通过对象访问

   **静态成员变量：属于类，放在方法区，又称类变量，通过类名访问**

2. 方法

3. 代码块

4. 内部类

5. 接口

#### 普通成员

```java
class Person{
    public String name;
    public int age;
    public void eat(){
        System.out.println(name+" is eat");
    }//方法
}
public class Main {
    public static void main(String[] args) {
        Person play1=new Person();//类实例化为对象
        System.out.println(play1.name);
        System.out.println(play1.age);
        play1.eat();
    }
}
```

> null
> 0
> null is eat

我们在使用时没有初始化，**引用类型默认字符串为null，整型为0，布尔型为false**

我们对其初始化后，再进行访问

```java
public class Main {
    public static void main(String[] args) {
        Person play1=new Person();
        play1.name="number1";
        play1.age=18;
        Person play2=new Person();
        play2.name="number2";
        play2.age=19;
        System.out.println("名字:"+play1.name+" 年龄:"+play1.age);
        System.out.println("名字:"+play2.name+" 年龄:"+play2.age);
    }
}
```

> 名字:number1 年龄:18
> 名字:number2 年龄:19

由此我们看出，普通成员变量是属于对象，我们对实例化第二个对象并且初始化赋值的时候并不会影响第一个对象的值。

#### 静态成员变量

普通成员变量属于对象，而静态成员属于类

```java
class Person{
    public String name;
    public int age;
    public static int count;
}
public class Main {
    public static void main(String[] args) {
        Person play1=new Person();
        Person play2=new Person();
        play1.count=1;
        play2.count=2;
        System.out.println(play1.count);
        System.out.println(play2.count);
    }
}
```

> 2
> 2

我们看见

1. 通过对象访问静态变量有警告
2. “初始化”不同但是输出结果相同并且以结果第二个

事实上，**静态成员变量属于类，我们可以通过类直接访问静态变量而不需要实例化一个对象**

我们知道引用放在栈区上，对象放在堆区，那么静态变量放在那里？放在方法区

与此对应的还有静态方法，我们通过类就能直接访问方法。

static定义的变量属于类，叫做类变量；定义的方法叫做类方法。

需要注意的是

1. 普通成员方法内不能定义静态变量。（可以看见直接报错，语法不支持。）

2. 静态方法内部不可以调用普通方法（调用普通方法需要对象）

3. 普通方法内部可以调用静态方法
4. 静态方法内部可以访问静态变量但是不能定义静态变量



### 封装

#### private实现封装

private和public这两个关键字表示"访问权限控制"。

1. 被public修饰的成员变量或者成员方法，可以被类直接调用者调用。
2. 被private修饰的成员变量或者成员方法，不能被类的调用者调用。

> 换句话说, 类的使用者根本不需要知道, 也不需要关注一个类都有哪些 private 的成员. 从而让类调用者以更低的成本来使用类。

#### getter和setter方法

```java
class Person{
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
public class Main {
    public static void main(String[] args) {
        Person person =new Person();
        person.setAge(18);
        person.setName("number");
        System.out.println(person.getAge());
        System.out.println(person.getName());
    }
}
```

需要注意的是

set和get方法再idea编译器中提供，可以直接生成。

注意以下错误

```java
public void setAge(int age) {
        age = age;//不会赋值，两个age是相同age（局部变量有限）
}
```



### 构造方法

定义：方法名和类名是相同的，并且构造方法没有返回值。

步骤：为对象分配内存---->调用**合适的**分配方法

合适的意味着调用方法不止一个。

需要注意的有

1. 方法名称必须与类名称相同
2. 构造方法没有返回值类型声明
3. 每一个类中一定至少存在一个构造方法（没有明确定义，则系统自动生成一个无参构造）
4. 如果类中没有提供任何的构造函数，那么编译器会默认生成一个不带有参数的构造函数
5. 若类中定义了构造方法，则默认的无参构造将不再生成.
6. 构造方法支持重载. 规则和普通方法的重载一致.

```java
class Person{
    public String name;
    public int age;

    public Person(String name,int age){
        this.age=age;
        this.name=name;
    }
    public Person(String name){
        this.name=name;
    }
    public Person(){
        System.out.println("无参数");
    }
}
public class Main {
    public static void main(String[] args) {
        Person person1 =new Person();
        Person person2 =new Person("zhangsan");
        Person person3 =new Person("lisi",18);
        System.out.println(person1.name+"   "+person1.age);
        System.out.println(person2.name+"   "+person2.age);
        System.out.println(person3.name+"   "+person3.age);

    }
}
```

> 无参数
> null   0
> zhangsan   0
> lisi   18

### 初始化顺序

- 静态属性：static开头定义的属性
- 静态方法块：static{}包起来的代码块
- 普通属性：非static定义的属性
- 普通方法块：0包起来的代码块
- 构造函数：类名相同的方法
- 方法：普通方法

### 关键字this

this和super有什么区别？

this.data--------调用当前对象的属性

this.func()------调用当前对象的方法

this()-------------调用当前对象的其他构造方法，只能存放在构造函数中，必须放到第一行

### 代码块

本地代码块

实例代码块

静态代码块

同步代码块

```java
class Person{
    public String name;
    public int age;
    {
        System.out.println("实例代码块");
    }
    static {
        System.out.println("静态代码块");
    }
    static int a=0;
}
public class Main {
    public static void main(String[] args) {
        Person person=new Person();
        System.out.println(person);
    }
}
```

> 静态代码块
> 实例代码块
> Person@1b6d3586

我们可以看见静态代码块是最先被执行的并且**静态代码块只会被执行一次**

并且静态代码块不用实例化对象也会被执行



代码块怎么被调用？

静态代码块执行在实例代码块前，并且静态代码块只执行一次

就算不用实例化为对象也会执行一次

## 面向对象

### 包

包 (package) 是组织类的一种方式.
使用包的主要目的是保证类的唯一性.

> 例如, 你在代码中写了一个 Test 类. 然后你的同事也可能写一个 Test 类. 如果出现两个同名的类, 就会冲突, 导致代码不能编译通过.

### 导入包中的类

Java 中已经提供了很多现成的类供我们使用. 例如

```java
public class Test {
    public static void main(String[] args) {
        java.util.Date date = new java.util.Date();
    	// 得到一个毫秒级别的时间戳
    	System.out.println(date.getTime());
	}
}
```

可以使用` java.util.Date` 这种方式引入 `java.util` 这个包中的 Date 类。

但是这种写法比较麻烦一些, 可以使用` import` 语句导入包.

```java
import java.util.Date;
public class Test {
	public static void main(String[] args) {
		Date date = new Date();
		// 得到一个毫秒级别的时间戳
		System.out.println(date.getTime());
	}
}
```

如果需要使用`java.util` 中的其他类, 可以使用 `import java.util.*`

```java
import java.util.*;
public class Test {
	public static void main(String[] args) {
		Date date = new Date();
		// 得到一个毫秒级别的时间戳
		System.out.println(date.getTime());
	}
}
```

但是我们更建议显式的指定要导入的类名. 否则还是容易出现冲突的情况.

```java
import java.util.*;
import java.sql.*;
public class Test {
	public static void main(String[] args) {
		// util 和 sql 中都存在一个 Date 这样的类, 此时就会出现歧义, 编译出错
		Date date = new Date();
		System.out.println(date.getTime());
	}
}
```

> Error:(5, 9) java: 对Date的引用不明确
> java.sql 中的类 java.sql.Date 和 java.util 中的类 java.util.Date 都匹配

在这种情况下需要使用完整的类名

```java
import java.util.*;
import java.sql.*;
public class Test {
	public static void main(String[] args) {
		java.util.Date date = new java.util.Date();
		System.out.println(date.getTime());
	}
}
```

注意事项: `import` 和 C++ 的 `#include` 差别很大. C++ 必须 `#include` 来引入其他文件内容, 但是 Java 不需要.
`import `只是为了写代码的时候更方便. `import` 更类似于 C++ 的 `namespace` 和 `using`

### 静态导入

使用`import static` 可以导入包中的静态的方法和字段.

```java
import static java.lang.System.*;
public class Test {
	public static void main(String[] args) {
		out.println("hello");
	}
}
```

使用这种方式可以更方便的写一些代码, 例如

```java
import static java.lang.Math.*;
public class Test {
	public static void main(String[] args) {
		double x = 30;
		double y = 40;
		// 静态导入的方式写起来更方便一些.
		// double result = Math.sqrt(Math.pow(x, 2) + Math.pow(y, 2));
		double result = sqrt(pow(x, 2) + pow(y, 2));
		System.out.println(result);
	}
}
```

#### 将类放到包中

基本规则
1、在文件的最上方加上一个 package 语句指定该代码在哪个包中.
2、包名需要尽量指定成唯一的名字, 通常会用公司的域名的颠倒形式(例如` com.bit.demo1 `).

3、包名要和代码路径相匹配. 例如创建 `com.bit.demo1`的包, 那么会存在一个对应的路径 `com/bit/demo1` 来存储代码.
3、如果一个类没有 package 语句, 则该类被放到一个默认包中.

上面的流程就是我们在`com.bit.demo1`新建了了`Main`类。

#### 包的访问权限

我们已经了解了类中的 public 和 private. private 中的成员只能被类的内部使用.

如果某个成员不包含 public 和 private 关键字, 此时这个成员可以在包内部的其他类使用, 但是不能在包外部的类使用.

下面的代码给了一个示例. Demo1 和 Demo2 是同一个包中, Main 是其他包中.

```java
package com.bit.demo1;

public class Demo1 {
        int value = 0;
}
```

```java
package com.bit.demo1;

public class Demo2 {
    public static void Main(String[] args) {
        Demo1 demo = new Demo1();
        System.out.println(demo.value);
    }
}
```

```java
import com.bit.demo1.Demo1;
public class Main {
    public static void main(String[] args) {
        Demo1 demo = new Demo1();
        System.out.println(demo.value);
    }
}
```

#### 常见的系统包

常见的系统包

1. java.lang:系统常用基础类(String、Object),此包从JDK1.1后自动导入。
2. java.lang.reflect:java 反射编程包;
3. java.net:进行网络编程开发包。
4. java.sql:进行数据库开发的支持包。
5. java.util:是java提供的工具程序包。(集合类等) 非常重要
6. java.io:I/O编程开发包。

### 继承

#### 背景

代码中创建的类, 主要是为了抽象现实中的一些事物(包含属性和方法).

有的时候客观事物之间就存在一些关联关系, 那么在表示成类和对象的时候也会存在一定的关联.
例如, 设计一个类表示动物

**注意**, 我们可以给每个类创建一个单独的 java 文件. 类名必须和 .java 文件名匹配(大小写敏感).

```java
// Animal.java
public class Animal {
	public String name;
	public Animal(String name) {
		this.name = name;
	}
	public void eat(String food) {
		System.out.println(this.name + "正在吃" + food);
	}
}
// Cat.java
class Cat {
	public String name;
	public Cat(String name) {
		this.name = name;
	}
	public void eat(String food) {
		System.out.println(this.name + "正在吃" + food);
	}
}
// Bird.java
class Bird {
	public String name;
	public Bird(String name) {
		this.name = name;
	}
	public void eat(String food) {
		System.out.println(this.name + "正在吃" + food);
	}
	public void fly() {
		System.out.println(this.name + "正在飞 ︿(￣︶￣)︿");
	}
}

```

这个代码我们发现其中存在了大量的冗余代码.

仔细分析, 我们发现 Animal 和 Cat 以及 Bird 这几个类中存在一定的关联关系:

1、这三个类都具备一个相同的 eat 方法, 而且行为是完全一样的.

2、这三个类都具备一个相同的 name 属性, 而且意义是完全一样的。

从逻辑上讲, Cat 和 Bird 都是一种 Animal (**is - a 语义**).

此时我们就可以让 Cat 和 Bird 分别继承 Animal 类, 来达到代码重用的效果.

此时, Animal 这样被继承的类, 我们称为**父类** , **基类** 或 **超类**, 对于像 Cat 和 Bird 这样的类, 我们称为 **子类**,或者**派生类**

和现实中的儿子继承父亲的财产类似, 子类也会继承父类的字段和方法, 以达到代码重用的效果.

#### 语法规则

```java
class 子类 extends 父类 {

}
```

使用 extends 指定父类.
1、Java 中一个子类只能继承一个父类 (而C++/Python等语言支持多继承).
2、子类会继承父类的所有 **public 的字段和方法**.
3、对于父类的 private 的字段和方法, 子类中是无法访问的.
4、子类的实例中, 也包含着父类的实例. **可以使用 super 关键字得到父类实例的引用.**

对于上面的代码, 可以使用继承进行改进. 此时我们让 Cat 和 Bird 继承自 Animal 类, 那么 Cat 在定义的时候就不必再写 name 字段和 eat 方法.

```java
class Animal {
	public String name;
	public Animal(String name) {
		this.name = name;
	}
	public void eat(String food) {
		System.out.println(this.name + "正在吃" + food);
	}
}

class Cat extends Animal {
	public Cat(String name) {
		// 使用 super 调用父类的构造方法.
		super(name);
	}
}

class Bird extends Animal {
	public Bird(String name) {
    	super(name);
	}
	public void fly() {
		System.out.println(this.name + "正在飞 ︿(￣︶￣)︿");
	}
}
public class Test {
	public static void main(String[] args) {
		Cat cat = new Cat("小黑");
		cat.eat("猫粮");
		Bird bird = new Bird("圆圆");
		bird.fly();
	}
}
```

> 小黑正在吃猫粮
> 圆圆正在飞 ︿(￣︶￣)︿

> extends 英文原意指 "扩展". 而我们所写的类的继承, 也可以理解成基于父类进行代码上的 "扩展".
> 例如我们写的 Bird 类, 就是在 Animal 的基础上扩展出了 fly 方法.

需要注意的是：在构造之类时需要**先**帮助父类构造

如果我们把 name 改成 private, 那么此时子类就不能访问了.

```java
class Bird extends Animal {
	public Bird(String name) {
		super(name);
	}
	public void fly() {
		System.out.println(this.name + "正在飞 ︿(￣︶￣)︿");
	}
}
```

> Error:(19, 32) java: name 在 Animal 中是 private 访问控制

### protected 关键字

刚才我们发现, 如果把字段设为 private, 子类不能访问. 但是设成 public, 又违背了我们 "封装" 的初衷.

两全其美的办法就是 protected 关键字.

1、对于类的调用者来说, protected 修饰的字段和方法是不能访问的

2、对于**类的子类** 和 **同一个包的其他类** 来说, protected 修饰的字段和方法是可以访问的

```java
// Animal.java
public class Animal {
	protected String name;
	public Animal(String name) {
    	this.name = name;
	}
	public void eat(String food) {
		System.out.println(this.name + "正在吃" + food);
	}
}
// Bird.java
public class Bird extends Animal {
	public Bird(String name) {
		super(name);
	}
	public void fly() {
	// 对于父类的 protected 字段, 子类可以正确访问
		System.out.println(this.name + "正在飞 ︿(￣︶￣)︿");
	}
}
// Test.java 和 Animal.java 不在同一个 包 之中了.
public class Test {
	public static void main(String[] args) {
		Animal animal = new Animal("小动物");
		System.out.println(animal.name); // 此时编译出错, 无法访问 name
	}
}
```

小结: Java 中对于字段和方法共有四种访问权限



|                | public | protected | default | private |
| -------------- | ------ | --------- | ------- | ------- |
| 同包同类       | true   | true      | true    | true    |
| 同包不同类     | true   | true      | true    |         |
| 同包不同类继承 | true   | true      | true    |         |
| 不同包继承     | true   | true      |         |         |
| 不同包无关系   | true   |           |         |         |



### 组合

和继承类似, 组合也是一种表达类之间关系的方式, 也是能够达到代码重用的效果.
例如表示一个学校:

```java
public class Student {
...
}
public class Teacher {
...
}
public class School {
	public Student[] students;
	public Teacher[] teachers;
}
```

组合并没有涉及到特殊的语法(诸如 extends 这样的关键字), 仅仅是将一个类的实例作为另外一个类的字段.
这是我们设计类的一种常用方式之一.

**组合**表示 **has - a** 语义
在刚才的例子中, 我们可以理解成一个学校中 "包含" 若干学生和教师.
**继承**表示 **is - a** 语义
在上面的 "动物和猫" 的例子中, 我们可以理解成一只猫也 "是" 一种动物.

### 多态

同时发生向上转型和动态绑定

向上转型：父类引用指向子类的实例

动态绑定：子类重写父类同名方法，并由父类引用调用方法

#### 向上转型

在刚才的例子中, 我们写了形如下面的代码

```java
Bird bird = new Bird("圆圆");
```

这个代码也可以写成这个样子

```java
Bird bird = new Bird("圆圆");
Animal bird2 = bird;
// 或者写成下面的方式
Animal bird2 = new Bird("圆圆");
```

此时 bird2 是一个父类 (Animal) 的引用, 指向一个子类 (Bird) 的实例. 这种写法称为 **向上转型**.

> 向上转型这样的写法可以结合 is - a 语义来理解.
> 例如, 我让我媳妇去喂圆圆, 我就可以说, "媳妇你喂小鸟了没?", 或者 "媳妇你喂鹦鹉了没?"
>
> 因为圆圆确实是一只鹦鹉, 也确实是一只小鸟~~

为啥叫 "向上转型"?

在面向对象程序设计中, 针对一些复杂的场景(很多类, 很复杂的继承关系), 程序猿会画一种 UML 图的方式来表示类之间的关系. 此时父类通常画在子类的上方. 所以我们就称为 "向上转型" , 表示往父类的方向转.

向上转型发生的时机:

1. 直接赋值
2. 方法传参
3. 方法返回

直接赋值的方式我们已经演示了. 另外两种方式和直接赋值没有本质区别.

方法传参

```java
public class Main {
	public static void main(String[] args) {
		Bird bird = new Bird("圆圆");
		feed(bird);
	}
	public static void feed(Animal animal) {
		animal.eat("谷子");
	}
}
```

此时形参 animal 的类型是 Animal (基类), 实际上对应到 Bird (父类) 的实例.

方法返回

```java
public class Main {
	public static void main(String[] args) {
		Animal animal = findMyAnimal();
	}
	public static Animal findMyAnimal() {
		Bird bird = new Bird("圆圆");
		return bird;
	}
}
```

此时方法 findMyAnimal 返回的是一个 Animal 类型的引用, 但是实际上对应到 Bird 的实例.

#### 动态绑定

当子类和父类中出现同名方法的时候, 再去调用会出现什么情况呢?

对前面的代码稍加修改, 给 Bird 类也加上同名的 eat 方法, 并且在两个 eat 中分别加上不同的日志.

```java
// Animal.java
public class Animal {
	protected String name;
	public Animal(String name) {
	this.name = name;
	}
	public void eat(String food) {
		System.out.println("我是一只小动物");
		System.out.println(this.name + "正在吃" + food);
	}
}
// Bird.java
public class Bird extends Animal {
	public Bird(String name) {
		super(name);
	}
	public void eat(String food) {
		System.out.println("我是一只小鸟");
		System.out.println(this.name + "正在吃" + food);
	}
}
// Test.java
public class Test {
	public static void main(String[] args) {
		Animal animal1 = new Animal("圆圆");
		animal1.eat("谷子");
		Animal animal2 = new Bird("扁扁");
		animal2.eat("谷子");
	}
}
```

> 我是一只小动物
> 圆圆正在吃谷子
> 我是一只小鸟
> 扁扁正在吃谷子

此时, 我们发现:
`animal1 `和 `animal2` 虽然都是` Animal` 类型的引用, 但是` animal1 `指向` Animal` 类型的实例, `animal2 `指向`Bird` 类型的实例.
针对 `animal1` 和` animal2` 分别调用 `eat` 方法, 发现 `animal1.eat()` 实际调用了父类的方法, `animal2.eat() `实际调用了子类的方法.
因此, 在 Java 中, 调用某个类的方法, 究竟执行了哪段代码 (是父类方法的代码还是子类方法的代码) , 要看究竟这个引用指向的是父类对象还是子类对象. 这个过程是程序运行时决定的(而不是编译期), 因此称为 **动态绑定**.

动态绑定的条件

1、父类引用引用子类的对象

2、通过这个父类应用调用父类和子类的同名覆盖函数

#### 方法重写

针对刚才的 eat 方法来说:
子类实现父类的同名方法, 并且参数的类型和个数完全相同, 这种情况称为 ==覆写/重写/覆盖==(Override).
关于重写的注意事项

1. 重写和重载完全不一样. 不要混淆(思考一下, 重载的规则是啥?)
2. 普通方法可以重写, **static 修饰的静态方法不能重写.**
3. 重写中子类的方法的访问权限不能低于父类的方法访问权限.
4. 重写的方法返回值类型不一定和父类的方法相同(但是建议最好写成相同, 特殊情况除外).

方法权限示例: 将子类的 eat 改成 private

```java
// Animal.java
public class Animal {
	public void eat(String food) {
	...
	}
}
// Bird.java
public class Bird extends Animal {
// 将子类的 eat 改成 private
	private void eat(String food) {
	...
	}
}
```

> // 编译出错
> Error:(8, 10) java: com.bit.Bird中的eat(java.lang.String)无法覆盖com.bit.Animal中的
> eat(java.lang.String)
> 正在尝试分配更低的访问权限; 以前为public



另外, 针对重写的方法, 可以使用 @Override 注解来显式指定.

```java
// Bird.java
public class Bird extends Animal {
	@Override
	private void eat(String food) {
	...
	}
}
```

有了这个注解能帮我们进行一些合法性校验. 例如不小心将方法名字拼写错了 (比如写成 aet), 那么此时编译器就会发现父类中没有 `eat` 方法, 就会编译报错, 提示无法构成重写.
我们推荐在代码中进行重写方法时显式加上` @Override` 注解.

#### 理解多态

```java
 public class Shape {
     public void draw(){

     }
}
class Cycle extends Shape{
    @Override
    public void draw() {
        System.out.println("这是一个圆>>⚪");
    }
}
class Flower extends Shape{
    @Override
    public void draw() {
        System.out.println("这是一朵花>>❀");
    }
}

public class Main {
    public void draw(Shape a){
        a.draw();
    }
    public static void main(String[] args) {
        Shape a=new Cycle();
        Shape b=new Flower();
        Main main=new Main();
        main.draw(a);
        main.draw(b);
    }
}
```



### 抽象类

父类 `Shape` 中的 `draw` 方法好像并没有什么实际工作, 主要的绘制图形都是由`Shape` 的各种子类的 `draw` 方法来完成的. 像这种没有实际工作的方法, 我们可以把它设计成一个 抽象方法(abstract method), 包含抽象方法的类我们称为 抽象类(abstract class)。

```java
abstract class Shape {
	abstract public void draw();
}
```



- 在 draw 方法前加上 abstract 关键字, 表示这是一个抽象方法. 同时**抽象方法没有方法体**(没有 { }, 不能执行具体代码).
- 对于包含抽象方法的类, 必须加上 abstract 关键字表示这是一个抽象类.

1、**抽象类不能实例化被对象**

```java
Shape shape=new Shape();
```

> Shape是抽象的; 无法实例化

2、**抽象方法不能是 private 的**

```java
abstract private void draw2();
```

> java: 非法的修饰符组合: abstract和private

3、**抽象类中可以包含其他的非抽象方法, 也可以包含字段. 这个非抽象方法和普通方法的规则都是一样的, 可以被重写,也可以被子类直接调用**

4、**唯一的作用是被继承，继承后普通类必须重写抽象类所有抽象方法**

5、**一个抽象类A，如果继承了一个抽象类B，可以不用实现父类B的抽象方法**

6、**但是如果有普通类继承A，还是需要重写抽象方法，A和B的都有重写。**

7、**抽象类不能被final修饰，抽象方法也不能被final修饰**

### 接口

在抽象类中，还可以包含非抽象方法, 和字段。而接口中包含的方法**都是**抽象方法, 字段**只能**包含静态常量（final static）

1、**使用interface来修饰**

2、**接口里面的普通方法不能有具体的方法实现。如果非要实现可以加一个default来修饰。**

3、**接口里面可以有static方法**

4、**里面所有的方法都是public，可以省略public**

5、**方法一定是抽象方法，可以省略abstract，字段一定是静态常量**

6、**接口不能通过new来实例化**

### 实现多个接口

有的时候我们需要让一个类同时继承自多个父类. 这件事情在有些编程语言通过 多继承 的方式来实现的.然而 Java 中**只支持单继承**, 一个类只能 extends 一个父类. 但是可以同时实现多个接口, 也能达到多继承类似的效果.

### 三个常用接口

#### Comparable

```java
class Stu implements Comparable<Stu>{
    String name;
    String number;
    double score;
    public Stu(String name, String number, double score) {
        this.name = name;
        this.number = number;
        this.score = score;
    }

    @Override
    public String toString() {
        return "TestStu{" +
                "name='" + name + '\'' +
                ", number='" + number + '\'' +
                ", score=" + score +
                '}';
    }

    @Override
    public int compareTo(Stu o) {
        if(this.score<o.score){
            return 1;
        }else if(this.score==o.score){
            return 0;
        }else{
            return -1;
        }
    }
}
public class Main {
    public static void main(String[] args) {
        Stu[] students=new Stu[5];
        students[0]=new Stu("zhangsan","0002",98.76);
        students[1]=new Stu("lisi","0001",98.45);
        students[2]=new Stu("wangwu","0003",78.56);
        students[3]=new Stu("wangermazi","0005",89.56);
        students[4]=new Stu("wangyi","0004",90.87);
        Arrays.sort(students);
        System.out.println(Arrays.toString(students));
    }
}
```

#### Compartor

```java
import java.util.Arrays;
import java.util.Comparator;

class Stu{
    String name;
    String number;
    double score;
    public Stu(String name, String number, double score) {
        this.name = name;
        this.number = number;
        this.score = score;
    }

    @Override
    public String toString() {
        return "TestStu{" +
                "name='" + name + '\'' +
                ", number='" + number + '\'' +
                ", score=" + score +
                '}';
    }
}
class ScoreComparator implements Comparator<Stu>{
    @Override
    public int compare(Stu o1, Stu o2) {
        if(o1.score> o2.score){
            return -1;
        }else if(o1.score==o2.score){
            return 0;
        }else{
            return 1;
        }
    }
}
class NameComparator implements Comparator<Stu>{
    @Override
    public int compare(Stu o1, Stu o2) {
        return o1.name.compareTo(o2.name);
    }
}
class NumberCompartor implements Comparator<Stu>{
    @Override
    public int compare(Stu o1, Stu o2) {
        return o1.number.compareTo(o2.number);
    }
}
public class Main {
    public static void printArr(Stu[] studengts){
        for (Stu numbers: studengts) {
            System.out.println(numbers);
        }
        System.out.println("---------------------------------");
    }
    public static void main(String[] args) {
        Stu[] students=new Stu[5];
        students[0]=new Stu("张三","0002",98.76);
        students[1]=new Stu("李四","0001",98.45);
        students[2]=new Stu("王五","0003",78.56);
        students[3]=new Stu("王二麻子","0005",89.56);
        students[4]=new Stu("马牛逼","0004",90.87);
        ScoreComparator scoreComparator=new ScoreComparator();
        NameComparator nameComparator=new NameComparator();
        NumberCompartor numberCompartor=new NumberCompartor();
        Arrays.sort(students,scoreComparator);
        printArr(students);
        Arrays.sort(students,numberCompartor);
        printArr(students);
        Arrays.sort(students,nameComparator);
        printArr(students);
    }
}
```

> TestStu{name='张三', number='0002', score=98.76}
> TestStu{name='李四', number='0001', score=98.45}
> TestStu{name='马牛逼', number='0004', score=90.87}
> TestStu{name='王二麻子', number='0005', score=89.56}
>
> TestStu{name='王五', number='0003', score=78.56}
>
> -----------------------------------------------------------------------
>
> TestStu{name='李四', number='0001', score=98.45}
> TestStu{name='张三', number='0002', score=98.76}
> TestStu{name='王五', number='0003', score=78.56}
> TestStu{name='马牛逼', number='0004', score=90.87}
>
> TestStu{name='王二麻子', number='0005', score=89.56}
>
> ------------------------------------------------------------
>
> TestStu{name='张三', number='0002', score=98.76}
> TestStu{name='李四', number='0001', score=98.45}
> TestStu{name='王二麻子', number='0005', score=89.56}
> TestStu{name='王五', number='0003', score=78.56}
>
> TestStu{name='马牛逼', number='0004', score=90.87}

**Compareable和Comparator对比**

前者对类的侵入性强，比较方法直接写在类里面，如果需要按照其他方式排序，需要修改代码

后者没有侵入类，如果需要其他比较方法调用其他比较器就可以了

#### Cloneable

Cloneable接口是一个空接口，是一个标志，表示类可以被克隆

```java
class TestStu implements Cloneable{
    String name;
    String number;
    double score;
    public TestStu(String name, String number, double score) {
        this.name = name;
        this.number = number;
        this.score = score;
    }

    @Override
    public String toString() {
        return "TestStu{" +
                "name='" + name + '\'' +
                ", number='" + number + '\'' +
                ", score=" + score +
                '}';
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
/*-------------------分割线------------------------------------------------*/
public class TestDemo{
    public static void main(String[] args)throws CloneNotSupportedException {
        TestStu student1=new TestStu("zhangsan","0001",90.78);
        TestStu student2=(TestStu) student1.clone();
        System.out.println(student2);
    }
}
```

需要注意的是：

1、需要有Cloneable标志接口

2、需要重写clone方法

3、需要抛出异常

## 异常

### 异常的背景

在先前的编程中就已经接触一些异常

**除以0**

```java
System.out.println(10 / 0);
```

> Exception in thread "main" java.lang.ArithmeticException: / by zero

**数组越界访问**

```java
int[] arr = {1, 2, 3};
System.out.println(arr[100]);
```

> Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 100

**空指针异常**

```java
public class Test {
	public int num = 10;
	public static void main(String[] args) {
		Test t = null;
		System.out.println(t.num);
	}
}
```

> Exception in thread "main" java.lang.NullPointerException

异常就是在程序**运行时**出现的错误，与编译时错误要分别开

### LBYL&&EAFP

**LBYL**: Look Before You Leap.
**EAFP**: It's Easier to Ask Forgiveness than Permission.

前者在程序执行前解决问题，后者出现问题后解决

### 异常的好处

下面给出一个例子

LBYL风格

```java
boolean ret = false;
ret = 登陆游戏();
if (!ret) {
	//处理登陆游戏错误;
	return;
}
ret = 开始匹配();
if (!ret) {
	//处理匹配错误;
	return;
}
ret = 游戏确认();
if (!ret) {
	//处理游戏确认错误;
	return;
}
ret = 选择英雄();
if (!ret) {
	//处理选择英雄错误;
	return;
}
ret = 载入游戏画面();
if (!ret) {
	//处理载入游戏错误;
	return;
}
```

```java
try {
	//登陆游戏();
	//开始匹配();
	//游戏确认();
	//选择英雄();
	//载入游戏画面();
	//...
} catch (登陆游戏异常) {
	//处理登陆游戏异常;
} catch (开始匹配异常) {
	//处理开始匹配异常;
} catch (游戏确认异常) {
	//处理游戏确认异常;
} catch (选择英雄异常) {
	//处理选择英雄异常;
} catch (载入游戏画面异常) {
	//处理载入游戏画面异常;
}
```

### 异常的用法

#### 捕获异常

一般通过`try catch`对异常进行捕捉

```java
try{
    //可能出现异常的部分
}catch(异常类型 异常对象){
    //执行程序
}finally{
    //执行语句
}
/**
*1、try 代码块中放的是可能出现异常的代码.
*2、catch 代码块中放的是出现异常后的处理行为.
*3、finally 代码块中的代码用于处理善后工作, 会在最后执行.
*4、其中 catch 和 finally 都可以根据情况选择加或者不加.
*5、finally语句无条件执行
*/
```

```java
public class Ex {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3};
        System.out.println("before");
        System.out.println(arr[100]);
        System.out.println("after");
    }
}
```

> before
> Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 100
> 	at TestException.main(TestException.java:5)

```java
int[] arr = {1, 2, 3};
try {
	System.out.println("before");
	System.out.println(arr[100]);
	System.out.println("after");
} catch (ArrayIndexOutOfBoundsException e) {
// 打印出现异常的调用栈
	e.printStackTrace();
}
System.out.println("after try catch");
```

> before
> after try catch
> java.lang.ArrayIndexOutOfBoundsException: 100
> 	at TestException.main(TestException.java:6)

我们发现, 一旦 try 中出现异常, 那么 try 代码块中的程序就不会继续执行, 而是交给 catch 中的代码来执行. catch 执行完毕会继续往下执行.

#### 异常处理

**有关异常的处理**

1、异常的种类有很多, 我们要根据不同的业务场景来决定.

2、对于比较严重的问题(例如和算钱相关的场景), 应该让程序直接崩溃, 防止造成更严重的后果

3、对于不太严重的问题(大多数场景), 可以记录错误日志, 并通过监控报警程序及时通知程序员

4、对于可能会恢复的问题(和网络相关的场景), 可以尝试进行重试.

5、在我们当前的代码中采取的是经过简化的第二种方式. 我们记录的错误日志是出现异常的方法调用信息, 能很快速的让我们找到出现异常的位置. 以后在实际工作中我们会采取更完备的方式来记录异常信息.

**流程**

1、程序先执行 try 中的代码

2、如果 try 中的代码出现异常, 就会结束 try 中的代码, 看和 catch 中的异常类型是否匹配.

3、如果找到匹配的异常类型, 就会执行 catch 中的代码

4、如果没有找到匹配的异常类型, 就会将异常向上传递到上层调用者.

5、无论是否找到匹配的异常类型, finally 中的代码都会被执行到(在该方法结束之前执行).

6、如果上层调用者也没有处理的了异常, 就继续向上传递.

一直到 main 方法也没有合适的代码处理异常, 就会交给 JVM 来进行处理, 此时程序就会异常终止.

#### 异常声明

我们在处理异常的时候, 通常希望知道这段代码中究竟会出现哪些可能的异常.

我们可以使用 throws 关键字, 把可能抛出的异常显式的标注在方法定义的位置. 从而提醒调用者要注意捕获这些异常

```java
public static int divide(int x, int y) throws ArithmeticException {
	if (y == 0) {
		throw new ArithmeticException("抛出除 0 异常");
	}
	return x / y;
}
```

### Java异常体系

### 自定义异常

```java
package day1125;

import java.util.Scanner;

class UserError extends Exception {
    public UserError(String message) {
        super(message);
    }
}
class PasswordError extends Exception {
    public PasswordError(String message) {
        super(message);
    }
}
public class Login {
    private static String userName = "admin";
    private static String password = "123456";

    public static void main(String[] args) {
        Scanner scanner =new Scanner(System.in);
        System.out.print("输入用户名>>");
        String name= scanner.nextLine();
        System.out.print("输入密码>>");
        String password=scanner.nextLine();
        try {
            login(name, password);
        } catch (UserError userError) {
            userError.printStackTrace();
        } catch (PasswordError passwordError) {
            passwordError.printStackTrace();
        }
    }
    public static void login(String userName, String password) throws UserError,
            PasswordError {
        if (!Login.userName.equals(userName)) {
            throw new UserError("用户名错误");
        }
        if (!Login.password.equals(password)) {
            throw new PasswordError("密码错误");
        }
        System.out.println("登陆成功");
    }
}

```

### 有关throws和throw

1、位置不同：throws在方法的声明后面，后面跟的是异常类名，而throw在方法的内部，后面跟的是异常的类名

2、抛出数量不同：throws可以抛出多个异常类，用逗号隔开，而throw只能抛出一个异常对象

3、处理方法不同：throws抛出后由该方法的调用者来处理，后者由由该方法体内的语句来处理

4、可能性不同：throws表示有出现异常的可能性，并不一定出现这些异常，throw一定有异常

可以对比上面自定义登录的例子

可以看见`throws`后面抛出类，`throw`后面抛出对象

`throws`抛出账户错误和密码错误两个类，后着抛出一个准确的对象

当账户密码正确`throws`就不会抛出异常

# JavaIO

## 1. File文件操作类

在`java.io`包之中，用`File`类来对文件进行创建、删除、取得信息等操作

### 1.1 对象实例化

`java.io.File` 类是一个普通的类,如果要实例化对象,则常用到两个构造方法

| 方法                                      | 说明                 |
| ----------------------------------------- | -------------------- |
| `public File(String pathname)`            | 创建指定路径文件对象 |
| `public File(String parent,String child)` | 指明父路径和子路径   |

### 1.2 基本文件操作

| 方法                                                | 说明                           |
| --------------------------------------------------- | ------------------------------ |
| `public boolean exists()`                           | 指定路径中文件或者目录是否存在 |
| `public boolean isDirectory()`                      | 判定一个文件是目录             |
| `public boolean isFile()`                           | 判定是否是文件                 |
| `public boolean delete()`                           | 删除文件                       |
| `public boolean createNewFile() throws IOException` | 创建一个新文件                 |

 ```java
public class IODemo1 {
    public static void main(String[] args) throws IOException{
        File file=new File("D:\\Github\\Java\\JavaIO\\io.txt");
        System.out.println("文件是否存在>>"+file.exists());
        System.out.println("文件是否时普通文件>>"+file.isFile());
        System.out.println("文件是否是目录>>"+file.isDirectory());
        file.delete();
        System.out.println("文件是否存在>>"+file.exists());
        System.out.println("文件创建是否成功>>"+file.createNewFile());
        System.out.println("文件是否存在>>"+file.exists());
    }
}
 ```



### 1.3 目录操作

| 方法                          | 说明                                   |
| ----------------------------- | -------------------------------------- |
| `public boolean mkdir()`      | 创建一个空目录                         |
| `public boolean mkdirs()`     | 创建目录(无论有多少级父目录，都会创建) |
| `public String getParent()`   | 取得父路径                             |
| `public File getParentFile()` | 取得父File对象                         |

```java
public class IODemo1 {

    public static void main(String[] args) {
        File file=new File("D:\\Github\\Java\\JavaIO\\io");
        System.out.println("文件是否存在>>"+file.exists());
        if(!file.exists()){
            file.mkdir();
        }
        System.out.println("是否是目录>>"+file.isDirectory());
    }
}
```

```java
    public static void main(String[] args) {
        File file=new File("D:\\Github\\Java\\JavaIO\\io\\io1\\io2\\io3\\io4");
        System.out.println("文件是否存在>>"+file.exists());
        if(!file.exists()){
            file.mkdirs();
        }
        System.out.println(file.getParent());
    }
```



### 1.4 文件属性

| 方法                       | 说明               |
| -------------------------- | ------------------ |
| public long length()       | 取得文件大小(字节) |
| public long lastModified() | 最后一次修改日期   |

 ### 1.5 其他操作

| 方法                        | 说明                       |
| --------------------------- | -------------------------- |
| `public File[] listFiles()` | 列出一个目录指定的全部组成 |

```java
public class IODemo1 {

    public static void main(String[] args) {
        File file=new File("D:\\Github\\Java\\JavaIO\\io");
        listAllFile(file);
    }
    private static void listAllFile(File file){
        if(file.isDirectory()){
            File[] list=file.listFiles();
            if(list!=null){
                for(File f:list){
                    listAllFile(f);
                }
            }
        }else{
            System.out.println(file);
        }
    }
    
```



## 2. 流

### 2.1 流的概念

在 Java中所有数据都是使用流读写的。流是一组有顺序的，有起点和终点的字节集合，是对数据传
输的总称或抽象。即数据在两设备间的传输称为流，流的本质是数据传输，根据数据传输特性将流抽象
为各种类，方便更直观的进行数据操作。

### 2.2 输入输出流

输入就是将数据从各种输入设备（包括文件、键盘等）中读取到内存中。
输出则正好相反，是将数据写入到各种输出设备（比如文件、显示器、磁盘等）。
例如键盘就是一个标准的输入设备，而显示器就是一个标准的输出设备，但是文件既可以作为输入设
备，又可以作为输出设备。

### 2.3 字节流字符流

File类不支持文件内容处理，如果要处理文件内容，必须要通过流的操作模式来完成。
在java.io包中，流分为两种：字节流与字符流
1、字节流：数据流中最小的数据单元是字节 。InputStream、OutputStream
2、字符流：数据流中最小的数据单元是字符， Java中的字符是Unicode编码，一个字符占用两个字节。Reader、Writer

![3](D:/Github/Note/picture/java/202201111827001.jpg)

### 2.4 字节流

1、`FileInputStream`和`FileOutputStream`

```java
public class FileInputStream extends InputStream {}
```

`FileInputStream` 从文件系统中的某个文件中获得输入字节。
`FileInputStream` 用于读取诸如图像数据之类的原始字节流。

| 方法                           | 说明                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| `FileInputStream(File file)`   | 通过打开与实际文件的连接创建一个 FileInputStream ，该文件由文件系统中的File 对象file 命名 |
| `FileInputStream(String name)` | 通过打开与实际文件的连接来创建一个 FileInputStream ，该文件由文件系统中的路径名 name 命名。 |

```java
public class FileOutputStream extends OutputStream
```

1、文件输出流是用于将数据写入到输出流File 或一个FileDescriptor 。 文件是否可用或可能被创建取决于底层平台。
2、特别是某些平台允许一次只能打开一个文件来写入一个FileOutputStream （或其他文件写入对象）。 在这种情况下，如果所涉及的文件已经打开，则此类中的构造函数将失败。

| 方法                            | 说明                                               |
| ------------------------------- | -------------------------------------------------- |
| `FileOutputStream(File file)`   | 创建文件输出流以写入由指定的 File 对象表示的文件。 |
| `FileOutputStream(String name)` | 创建文件输出流以指定的名称写入文件。               |

2、字节缓冲流BufferedInputStream和BufferedOutputStream
问题一：为什么需要有缓冲流？
答：当我们用read()读取文件时，每读一个字节，访问一次硬盘，效率很低 。文件过大时，操作
起来也不是很方便。因此我们需要用到buffer缓存流，当创建buffer对象时，会创建一个缓冲区
数组。当我们读一个文件时，先从硬盘中读到缓冲区，然后直接从缓冲区输出即可，效率会更
高。

```java
public class BufferedInputStream extends FilterInputStream
```

1、BufferedInputStream 为另一个输入流添加了功能，即缓冲输入和支持mark 和reset 方法的功
能。 当创建BufferedInputStream 时，将创建一个内部缓冲区数组。
2、当从流中读取或跳过字节时，内部缓冲区将根据需要从所包含的输入流中重新填充，一次有多个字
节。 mark 操作会记住输入流中的一点，并且reset 操作会导致从最近的mark 操作之后读取的所
有字节在从包含的输入流中取出新的字节之前重新读取。

| 方法                                          | 说明                                                         |
| --------------------------------------------- | ------------------------------------------------------------ |
| BufferedInputStream(InputStream in)           | 创建一个 BufferedInputStream 并保存其参数，输入流 in ，供以后使用。 |
| BufferedInputStream(InputStream in, int size) | 创建 BufferedInputStream 具有指定缓冲区大小，并保存其参数，输入流 in ，供以后使用。 |

```java
public class BufferedOutputStream extends FilterOutputStream
```

该类实现缓冲输出流。 通过设置这样的输出流，应用程序可以向底层输出流写入字节，而不必为写入的每个字节导致底层系统的调用。

| 方法                                             | 说明                                                         |
| ------------------------------------------------ | ------------------------------------------------------------ |
| BufferedOutputStream(OutputStream out)           | 创建一个新的缓冲输出流，以将数据写入指定的底层输出流。       |
| BufferedOutputStream(OutputStream out, int size) | 创建一个新的缓冲输出流，以便以指定的缓冲区大小将数据写入指定的底层输出流。 |

### 2.5 字符流

1、`FileReader`和`FileWriter`

```java
public class FileReader extends InputStreamReader{}
```

如果要从文件中读取内容，可以直接使用`FileReader` 子类。
`FileReader` 是用于读取字符流。 要读取原始字节流，请考虑使用`FileInputStream` 。

| 方法                        | 说明                                               |
| --------------------------- | -------------------------------------------------- |
| FileReader(File file)       | 创建一个新的 FileReader ，给出 File 读取。         |
| FileReader(String fileName) | 创建一个新的 FileReader ，给定要读取的文件的名称。 |

```java
public class FileWriter extends OutputStreamWriter
```

1、如果是向文件中写入内容，应该使用FileWriter 子类
2、FileWriter 是用于写入字符流。 要编写原始字节流，请考虑使用FileOutputStream

| 方法                          | 说明                                   |
| ----------------------------- | -------------------------------------- |
| `FileWriter(File file)`       | 给一个File对象构造一个FileWriter对象。 |
| `FileWriter(String fileName)` | 构造一个给定文件名的FileWriter对象。   |

2、字符缓冲流BufferedReader和BufferedWriter
为了提高字符流读写的效率，引入了缓冲机制，进行字符批量的读写，提高了单个字符读写的效率。
BufferedReader 用于加快读取字符的速度， BufferedWriter 用于加快写入的速度。
BufferedReader 和BufferedWriter 类各拥有8192个字符的缓冲区。当BufferedReader在读取文
本文件时，会先尽量从文件中读入字符数据并放满缓冲区，而之后若使用read()方法，会先从缓冲区中
进行读取。如果缓冲区数据不足，才会再从文件中读取，使用BufferedWriter 时，写入的数据并不会
先输出到目的地，而是先存储至缓冲区中。如果缓冲区中的数据满了，才会一次对目的地进行写出。

```java
public class BufferedReader extends Reader
```

1、BufferedInputStream 为另一个输入流添加了功能，即缓冲输入和支持mark 和reset 方法的功
能。 当创建BufferedInputStream 时，将创建一个内部缓冲区数组。
2、当从流中读取或跳过字节时，内部缓冲区将根据需要从所包含的输入流中重新填充，一次有多个字
节。 mark 操作会记住输入流中的一点，并且reset 操作会导致从最近的mark 操作之后读取的所
有字节在从包含的输入流中取出新的字节之前重新读取。

| 方法                              | 说明                                           |
| --------------------------------- | ---------------------------------------------- |
| BufferedReader(Reader in)         | 创建使用默认大小的输入缓冲区的缓冲字符输入流。 |
| BufferedReader(Reader in, int sz) | 创建使用指定大小的输入缓冲区的缓冲字符输入流。 |

```java
public class BufferedWriter extends Writer
```

该类实现缓冲输出流。 通过设置这样的输出流，应用程序可以向底层输出流写入字节，而不必为写入的每个字节导致底层系统的调用。

| 方法                               | 说明                                                   |
| ---------------------------------- | ------------------------------------------------------ |
| BufferedWriter(Writer out)         | 创建使用默认大小的输出缓冲区的缓冲字符输出流。         |
| BufferedWriter(Writer out, int sz) | 创建一个新的缓冲字符输出流，使用给定大小的输出缓冲区。 |

### 2.6 字节流和字符流的转换

```java
public class InputStreamReader extends Reader
```

| 方法                                         | 说明                                        |
| -------------------------------------------- | ------------------------------------------- |
| InputStreamReader(InputStream in)            | 创建一个使用默认字符集的InputStreamReader。 |
| InputStreamReader(InputStream in,Charset cs) | 创建一个使用给定字符集的InputStreamReader。 |

# Java集合

![java-collection-hierarchy.71519bdb](D:/Github/Note/picture/ds/202201201611256.png)

## 线性表

### 顺序表ArrayList

|                    方法                     | 作用                                |
| :-----------------------------------------: | ----------------------------------- |
|              boolean add(E e)               | 尾插 e                              |
|       void add(int index, E element)        | 将 e 插入到 index 位置              |
|  boolean addAll(Collection<? extends E> c)  | 尾插 c 中的元素                     |
|             E remove(int index)             | 删除 index 位置元素                 |
|          boolean remove(Object o)           | 删除遇到的第一个 o                  |
|              E get(int index)               | 获取下标 index 位置元素             |
|         E set(int index, E element)         | 将下标 index 位置元素设置为 element |
|                void clear()                 | 清空                                |
|         boolean contains(Object o)          | 判断 o 是否在线性表中               |
|            int indexOf(Object o)            | 返回第一个 o 所在下标               |
|          int lastIndexOf(Object o)          | 返回最后一个 o 的下标               |
| List<E> subList(int fromIndex, int toIndex) | 截取部分 list                       |

| 构造方法                             | 作用                               |
| ------------------------------------ | ---------------------------------- |
| ArrayList()                          | 无参构造                           |
| ArrayList(Collection<? extends E> c) | 利用其他 Collection 构建 ArrayList |
| ArrayList(int initialCapacity)       | 指定顺序表初始容量                 |

需要注意的是

ArrayList是线程不安全的，如果需要线程安全

```java
List list = Collections.synchronizedList(new ArrayList(...))
```



### 链表LinkedList

| 构造方法     | 作用     |
| ------------ | -------- |
| LinkedList() | 无参构造 |

也是线程不安全的

```java
List list = Collections.synchronizedList(new LinkedList(...))
```



## 栈Stack

Java中的栈继承与矢量，但是矢量在Java中已经过时

栈的底层是一个数组，现在推荐使用下面这种方式创建一个栈

```java
		Deque<Integer> stack=new ArrayDeque<>();
```

| 方法             | 作用           |
| ---------------- | -------------- |
| E push(E item)   | 压栈           |
| E pop()          | 出栈           |
| E peek()         | 查看栈顶元素   |
| boolean empty()  | 判断栈是否为空 |
| boolean search() | 查找某个元素   |
| int size()       | 得到长度       |

## 队列Queue

| 处理         | 抛出异常  | 返回特殊值 |
| ------------ | --------- | ---------- |
| 入队         | add(e)    | offer(e)   |
| 出队         | remove()  | poll()     |
| 查看队头元素 | element() | peek()     |

用add方法抛出异常，使用offer返回特殊值

## 双端队列Deque

| 头部/尾部 | 头部元素（队首） |               |              | 尾部元素（队尾） |
| --------- | ---------------- | ------------- | ------------ | ---------------- |
| 错误处理  | 抛出异常         | 返回特殊值    | 抛出异常     | 返回特殊值       |
| 入队      | addFirst(e)      | offerFirst(e) | addLast(e)   | offerLast(e)     |
| 出队      | removeFirst()    | pollFirst()   | removeLast() | pollLast()       |
| 获取元素  | getFirst()       | peekFirst()   | getLast()    | peekLast()       |



## Map

| 方法                                       | 作用                                          |
| ------------------------------------------ | --------------------------------------------- |
| V get(Objiect key)                         | 返回key对应的value                            |
| V getOrDefault(Object key,V default Value) | 返回key对应的value，如果key不存在，返回默认值 |
| V put(K key,V value)                       | 设置key对应的value                            |
| V remove(Object key)                       | 删除key对应的映射关系                         |
| Set<K> keySet()                            | 返回所有key不重复的集合                       |
| Collection<V> values()                     | 返回所有value的可重复集合                     |
| Set<Map.Entry<K,V>> entrySet()             | 返回所有的key-value映射关系                   |
| boolean containsKey(Object key)            | 判断是否包含key                               |
| boolean containsValue(Object value)        | 判断是否包含value                             |

## Set

| 方法                                     | 作用                             |
| ---------------------------------------- | -------------------------------- |
| boolean add(E e)                         | 添加元素，重复元素不会被添加     |
| void clear()                             | 清空集合                         |
| boolean contains(Object o)               | 判断o是否在集合中                |
| Iterator<E> iterator()                   | 返回迭代器                       |
| boolean remove(Object o)                 | 删除集合中的o                    |
| int size()                               | 返回元素个数                     |
| boolean isEmpty()                        | 检查是否为空                     |
| Object[] toArray()                       | 将元素转换为数组返回             |
| boolean containsAll(Collection<?> c)     | 判断一个集合的元素是否都在集合内 |
| boolean addAll(Collection<?extends E> c) | 将c的元素加入集合，可以去重      |

## 源码分析

### ArrayList

```java
package java.util;

import java.util.function.Consumer;
import java.util.function.Predicate;
import java.util.function.UnaryOperator;


public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
{
    private static final long serialVersionUID = 8683452581122892189L;

    //默认初始容量大小
    private static final int DEFAULT_CAPACITY = 10;

    //空数组（用于空实例）。构造函数传入参数为0
    private static final Object[] EMPTY_ELEMENTDATA = {};

     //用于默认大小空实例的共享空数组实例。
     //我们把它从EMPTY_ELEMENTDATA数组中区分出来，以知道在添加第一个元素时容量需要增加多少。
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};

    /**
     * 保存ArrayList数据的数组
     */
    transient Object[] elementData; // non-private to simplify nested class access

    /**
     * ArrayList 所包含的元素个数
     */
    private int size;

    /**
     * 带初始容量参数的构造函数（用户可以在创建ArrayList对象时自己指定集合的初始大小）
     */
    public ArrayList(int initialCapacity) {
        if (initialCapacity > 0) {
            //如果传入的参数大于0，创建initialCapacity大小的数组
            this.elementData = new Object[initialCapacity];
        } else if (initialCapacity == 0) {
            //如果传入的参数等于0，创建空数组
            this.elementData = EMPTY_ELEMENTDATA;
        } else {
            //其他情况，抛出异常
            throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        }
    }

    /**
     *默认无参构造函数
     *DEFAULTCAPACITY_EMPTY_ELEMENTDATA 为0.初始化为10，也就是说初始其实是空数组 当添加第一个元素的时候数组容量才变成10
     */
    public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }

    /**
     * 构造一个包含指定集合的元素的列表，按照它们由集合的迭代器返回的顺序。
     */
    public ArrayList(Collection<? extends E> c) {
        //将指定集合转换为数组
        elementData = c.toArray();
        //如果elementData数组的长度不为0
        if ((size = elementData.length) != 0) {
            // 如果elementData不是Object类型数据（c.toArray可能返回的不是Object类型的数组所以加上下面的语句用于判断）
            if (elementData.getClass() != Object[].class)
                //将原来不是Object类型的elementData数组的内容，赋值给新的Object类型的elementData数组
                elementData = Arrays.copyOf(elementData, size, Object[].class);
        } else {
            // 其他情况，用空数组代替
            this.elementData = EMPTY_ELEMENTDATA;
        }
    }

    /**
     * 修改这个ArrayList实例的容量是列表的当前大小。 应用程序可以使用此操作来最小化ArrayList实例的存储。
     */
    public void trimToSize() {
        modCount++;
        if (size < elementData.length) {
            elementData = (size == 0)
              ? EMPTY_ELEMENTDATA
              : Arrays.copyOf(elementData, size);
        }
    }
	//下面是ArrayList的扩容机制
	//ArrayList的扩容机制提高了性能，如果每次只扩充一个，
	//那么频繁的插入会导致频繁的拷贝，降低性能，而ArrayList的扩容机制避免了这种情况。
    /**
     * 如有必要，增加此ArrayList实例的容量，以确保它至少能容纳元素的数量
     * @param   minCapacity   所需的最小容量
     */
    public void ensureCapacity(int minCapacity) {
        //如果是true，minExpand的值为0，如果是false,minExpand的值为10
        int minExpand = (elementData != DEFAULTCAPACITY_EMPTY_ELEMENTDATA)
            // any size if not default element table
            ? 0
            // larger than default for default empty table. It's already
            // supposed to be at default size.
            : DEFAULT_CAPACITY;
        //如果最小容量大于已有的最大容量
        if (minCapacity > minExpand) {
            ensureExplicitCapacity(minCapacity);
        }
    }
   //1.得到最小扩容量
   //2.通过最小容量扩容
    private void ensureCapacityInternal(int minCapacity) {
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
              // 获取“默认的容量”和“传入参数”两者之间的最大值
            minCapacity = Math.max(DEFAULT_CAPACITY, minCapacity);
        }

        ensureExplicitCapacity(minCapacity);
    }
  //判断是否需要扩容
    private void ensureExplicitCapacity(int minCapacity) {
        modCount++;

        // overflow-conscious code
        if (minCapacity - elementData.length > 0)
            //调用grow方法进行扩容，调用此方法代表已经开始扩容了
            grow(minCapacity);
    }

    /**
     * 要分配的最大数组大小
     */
    private static final int MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8;

    /**
     * ArrayList扩容的核心方法。
     */
    private void grow(int minCapacity) {
        // oldCapacity为旧容量，newCapacity为新容量
        int oldCapacity = elementData.length;
        //将oldCapacity 右移一位，其效果相当于oldCapacity /2，
        //我们知道位运算的速度远远快于整除运算，整句运算式的结果就是将新容量更新为旧容量的1.5倍，
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        //然后检查新容量是否大于最小需要容量，若还是小于最小需要容量，那么就把最小需要容量当作数组的新容量，
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        //再检查新容量是否超出了ArrayList所定义的最大容量，
        //若超出了，则调用hugeCapacity()来比较minCapacity和 MAX_ARRAY_SIZE，
        //如果minCapacity大于MAX_ARRAY_SIZE，则新容量则为Interger.MAX_VALUE，否则，新容量大小则为 MAX_ARRAY_SIZE。
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // minCapacity is usually close to size, so this is a win:
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
    //比较minCapacity和 MAX_ARRAY_SIZE
    private static int hugeCapacity(int minCapacity) {
        if (minCapacity < 0) // overflow
            throw new OutOfMemoryError();
        return (minCapacity > MAX_ARRAY_SIZE) ?
            Integer.MAX_VALUE :
            MAX_ARRAY_SIZE;
    }

    /**
     *返回此列表中的元素数。
     */
    public int size() {
        return size;
    }

    /**
     * 如果此列表不包含元素，则返回 true 。
     */
    public boolean isEmpty() {
        //注意=和==的区别
        return size == 0;
    }

    /**
     * 如果此列表包含指定的元素，则返回true 。
     */
    public boolean contains(Object o) {
        //indexOf()方法：返回此列表中指定元素的首次出现的索引，如果此列表不包含此元素，则为-1
        return indexOf(o) >= 0;
    }

    /**
     *返回此列表中指定元素的首次出现的索引，如果此列表不包含此元素，则为-1
     */
    public int indexOf(Object o) {
        if (o == null) {
            for (int i = 0; i < size; i++)
                if (elementData[i]==null)
                    return i;
        } else {
            for (int i = 0; i < size; i++)
                //equals()方法比较
                if (o.equals(elementData[i]))
                    return i;
        }
        return -1;
    }

    /**
     * 返回此列表中指定元素的最后一次出现的索引，如果此列表不包含元素，则返回-1。.
     */
    public int lastIndexOf(Object o) {
        if (o == null) {
            for (int i = size-1; i >= 0; i--)
                if (elementData[i]==null)
                    return i;
        } else {
            for (int i = size-1; i >= 0; i--)
                if (o.equals(elementData[i]))
                    return i;
        }
        return -1;
    }

    /**
     * 返回此ArrayList实例的浅拷贝。 （元素本身不被复制。）
     */
    public Object clone() {
        try {
            ArrayList<?> v = (ArrayList<?>) super.clone();
            //Arrays.copyOf功能是实现数组的复制，返回复制后的数组。参数是被复制的数组和复制的长度
            v.elementData = Arrays.copyOf(elementData, size);
            v.modCount = 0;
            return v;
        } catch (CloneNotSupportedException e) {
            // 这不应该发生，因为我们是可以克隆的
            throw new InternalError(e);
        }
    }

    /**
     *以正确的顺序（从第一个到最后一个元素）返回一个包含此列表中所有元素的数组。
     *返回的数组将是“安全的”，因为该列表不保留对它的引用。 （换句话说，这个方法必须分配一个新的数组）。
     *因此，调用者可以自由地修改返回的数组。 此方法充当基于阵列和基于集合的API之间的桥梁。
     */
    public Object[] toArray() {
        return Arrays.copyOf(elementData, size);
    }

    /**
     * 以正确的顺序返回一个包含此列表中所有元素的数组（从第一个到最后一个元素）;
     *返回的数组的运行时类型是指定数组的运行时类型。 如果列表适合指定的数组，则返回其中。
     *否则，将为指定数组的运行时类型和此列表的大小分配一个新数组。
     *如果列表适用于指定的数组，其余空间（即数组的列表数量多于此元素），则紧跟在集合结束后的数组中的元素设置为null 。
     *（这仅在调用者知道列表不包含任何空元素的情况下才能确定列表的长度。）
     */
    @SuppressWarnings("unchecked")
    public <T> T[] toArray(T[] a) {
        if (a.length < size)
            // 新建一个运行时类型的数组，但是ArrayList数组的内容
            return (T[]) Arrays.copyOf(elementData, size, a.getClass());
            //调用System提供的arraycopy()方法实现数组之间的复制
        System.arraycopy(elementData, 0, a, 0, size);
        if (a.length > size)
            a[size] = null;
        return a;
    }

    // Positional Access Operations

    @SuppressWarnings("unchecked")
    E elementData(int index) {
        return (E) elementData[index];
    }

    /**
     * 返回此列表中指定位置的元素。
     */
    public E get(int index) {
        rangeCheck(index);

        return elementData(index);
    }

    /**
     * 用指定的元素替换此列表中指定位置的元素。
     */
    public E set(int index, E element) {
        //对index进行界限检查
        rangeCheck(index);

        E oldValue = elementData(index);
        elementData[index] = element;
        //返回原来在这个位置的元素
        return oldValue;
    }

    /**
     * 将指定的元素追加到此列表的末尾。
     */
    public boolean add(E e) {
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        //这里看到ArrayList添加元素的实质就相当于为数组赋值
        elementData[size++] = e;
        return true;
    }

    /**
     * 在此列表中的指定位置插入指定的元素。
     *先调用 rangeCheckForAdd 对index进行界限检查；然后调用 ensureCapacityInternal 方法保证capacity足够大；
     *再将从index开始之后的所有成员后移一个位置；将element插入index位置；最后size加1。
     */
    public void add(int index, E element) {
        rangeCheckForAdd(index);

        ensureCapacityInternal(size + 1);  // Increments modCount!!
        //arraycopy()这个实现数组之间复制的方法一定要看一下，下面就用到了arraycopy()方法实现数组自己复制自己
        System.arraycopy(elementData, index, elementData, index + 1,
                         size - index);
        elementData[index] = element;
        size++;
    }

    /**
     * 删除该列表中指定位置的元素。 将任何后续元素移动到左侧（从其索引中减去一个元素）。
     */
    public E remove(int index) {
        rangeCheck(index);

        modCount++;
        E oldValue = elementData(index);

        int numMoved = size - index - 1;
        if (numMoved > 0)
            System.arraycopy(elementData, index+1, elementData, index,
                             numMoved);
        elementData[--size] = null; // clear to let GC do its work
      //从列表中删除的元素
        return oldValue;
    }

    /**
     * 从列表中删除指定元素的第一个出现（如果存在）。 如果列表不包含该元素，则它不会更改。
     *返回true，如果此列表包含指定的元素
     */
    public boolean remove(Object o) {
        if (o == null) {
            for (int index = 0; index < size; index++)
                if (elementData[index] == null) {
                    fastRemove(index);
                    return true;
                }
        } else {
            for (int index = 0; index < size; index++)
                if (o.equals(elementData[index])) {
                    fastRemove(index);
                    return true;
                }
        }
        return false;
    }

    /*
     * Private remove method that skips bounds checking and does not
     * return the value removed.
     */
    private void fastRemove(int index) {
        modCount++;
        int numMoved = size - index - 1;
        if (numMoved > 0)
            System.arraycopy(elementData, index+1, elementData, index,
                             numMoved);
        elementData[--size] = null; // clear to let GC do its work
    }

    /**
     * 从列表中删除所有元素。
     */
    public void clear() {
        modCount++;

        // 把数组中所有的元素的值设为null
        for (int i = 0; i < size; i++)
            elementData[i] = null;

        size = 0;
    }

    /**
     * 按指定集合的Iterator返回的顺序将指定集合中的所有元素追加到此列表的末尾。
     */
    public boolean addAll(Collection<? extends E> c) {
        Object[] a = c.toArray();
        int numNew = a.length;
        ensureCapacityInternal(size + numNew);  // Increments modCount
        System.arraycopy(a, 0, elementData, size, numNew);
        size += numNew;
        return numNew != 0;
    }

    /**
     * 将指定集合中的所有元素插入到此列表中，从指定的位置开始。
     */
    public boolean addAll(int index, Collection<? extends E> c) {
        rangeCheckForAdd(index);

        Object[] a = c.toArray();
        int numNew = a.length;
        ensureCapacityInternal(size + numNew);  // Increments modCount

        int numMoved = size - index;
        if (numMoved > 0)
            System.arraycopy(elementData, index, elementData, index + numNew,
                             numMoved);

        System.arraycopy(a, 0, elementData, index, numNew);
        size += numNew;
        return numNew != 0;
    }

    /**
     * 从此列表中删除所有索引为fromIndex （含）和toIndex之间的元素。
     *将任何后续元素移动到左侧（减少其索引）。
     */
    protected void removeRange(int fromIndex, int toIndex) {
        modCount++;
        int numMoved = size - toIndex;
        System.arraycopy(elementData, toIndex, elementData, fromIndex,
                         numMoved);

        // clear to let GC do its work
        int newSize = size - (toIndex-fromIndex);
        for (int i = newSize; i < size; i++) {
            elementData[i] = null;
        }
        size = newSize;
    }

    /**
     * 检查给定的索引是否在范围内。
     */
    private void rangeCheck(int index) {
        if (index >= size)
            throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
    }

    /**
     * add和addAll使用的rangeCheck的一个版本
     */
    private void rangeCheckForAdd(int index) {
        if (index > size || index < 0)
            throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
    }

    /**
     * 返回IndexOutOfBoundsException细节信息
     */
    private String outOfBoundsMsg(int index) {
        return "Index: "+index+", Size: "+size;
    }

    /**
     * 从此列表中删除指定集合中包含的所有元素。
     */
    public boolean removeAll(Collection<?> c) {
        Objects.requireNonNull(c);
        //如果此列表被修改则返回true
        return batchRemove(c, false);
    }

    /**
     * 仅保留此列表中包含在指定集合中的元素。
     *换句话说，从此列表中删除其中不包含在指定集合中的所有元素。
     */
    public boolean retainAll(Collection<?> c) {
        Objects.requireNonNull(c);
        return batchRemove(c, true);
    }


    /**
     * 从列表中的指定位置开始，返回列表中的元素（按正确顺序）的列表迭代器。
     *指定的索引表示初始调用将返回的第一个元素为next 。 初始调用previous将返回指定索引减1的元素。
     *返回的列表迭代器是fail-fast 。
     */
    public ListIterator<E> listIterator(int index) {
        if (index < 0 || index > size)
            throw new IndexOutOfBoundsException("Index: "+index);
        return new ListItr(index);
    }

    /**
     *返回列表中的列表迭代器（按适当的顺序）。
     *返回的列表迭代器是fail-fast 。
     */
    public ListIterator<E> listIterator() {
        return new ListItr(0);
    }

    /**
     *以正确的顺序返回该列表中的元素的迭代器。
     *返回的迭代器是fail-fast 。
     */
    public Iterator<E> iterator() {
        return new Itr();
    }



```

# Java多线程

## 1. 认识线程

### 创建线程

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





## 2.Thread类及常见方法

### 2.1 Thread的构造方法

| 方法                                      | 说明                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| Thread()                                  | 创建线程对象                                                 |
| Thread(Runnable target)                   | 使用 Runnable 对象创建线程对象                               |
| Thread(String name)                       | 创建线程对象，并命名                                         |
| Thread(Runnable target,String name)       | 使用 Runnable 对象创建线程对象，并命名                       |
| Thread(ThreadGroup group,Runnable target) | 线程可以被用来分组管理，分好的组即使线程组，这个目前我们了解即可 |



### 2.2 Thread的属性

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

### 2.3 中断一个线程

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



### 2.4 等待一个进程

| 方法                                     | 说明                             |
| ---------------------------------------- | -------------------------------- |
| public void join()                       | 等待线程结束                     |
| public void join(long millis)            | 等待线程结束，最多等 millis 毫秒 |
| public void join(long millis, int nanos) | 同理，但可以更高精度             |

### 2.5 获取当前线程的引用

| 方法                                  | 说明                   |
| ------------------------------------- | ---------------------- |
| public static Thread currentThread(); | 返回当前线程对象的引用 |

### 2.6 休眠当前线程

因为线程的调度是不可控的，所以，这个方法只能保证休眠时间是大于等于休眠时间的。

| 方法                                                         | 说明                     |
| ------------------------------------------------------------ | ------------------------ |
| public static void sleep(long millis) throws InterruptedException | 休眠当前线程 millis 毫秒 |
| public static void sleep(long millis, int nanos) throws InterruptedException | 可以更高精度的休眠       |

## 3. 线程的状态

### 3.1 线程的所有状态

| 状态          | 说明                                 |
| ------------- | ------------------------------------ |
| NEW           | Thread对象创建，但是PCB还没有        |
| RUNNABLE      | 线程正在CPU上执行或者将要到CPU上执行 |
| WAITING       | wait导致                             |
| TIMED_WAITING | sleep方法                            |
| BLOCKED       | 等待锁                               |
| TERMINATED    | 对象还在，但是OCB对象没有了          |

![dxc1](D:/Github/Note/picture/java/dxc1.png)

### 3.2 线程的状态以及状态转移的意义

### 3.3 线程的状态转移

## 4. 线程安全问题

### 4.1 线程不安全实例

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



### 4.2 线程安全的概念

线程不安全：多线程并发执行某个代码时，产生了逻辑上的错误，就是不安全

线程安全：多线程并发执行某个代码时，逻辑上没有错误，这就是线程安全

### 4.3 线程不安全的原因及解决方案

<font color="red">**1、线程是抢占式执行的----根本原因**</font>

解决方案：没有，这是操作系统内核实现的

<font color="red">**2、run方法里面的操作可能不是原子性的**</font>

解决方案：通过锁，可以实现原子性

> 以上面为例，自增需要三步，读入cpu，cpu里加一，写入内存。线程1读入0，线程2读入0，线程1CPU+1，线程2CPU+1，线程1将1写入内存，线程2将1写入内存。自增2次，但却是加了一次。通过锁可以将三步合一

<font color="red">**3、多个线程尝试修改同一个变量**</font>

解决方案：需要看需求

<font color="red">**4、内存可见性导致的不安全**</font>

<font color="red">**5、指令重排序**</font>

## 5. synchronized关键字

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

## 6. volatile关键字

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

## 7. 对象的等待集

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

## 8. 多线程案例

### 8.1 单例模式

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

### 8.2 阻塞队列

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

### 8.3 定时器

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

### 8.4 线程池

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

## 9. 常见锁策略

### 9.1 乐观锁VS悲观锁

乐观锁：乐观锁假设认为数据一般情况下不会产生并发冲突，所以在数据进行提交更新的时候，才会正式对数据是

否产生并发冲突进行检测，如果发现并发冲突了，则让返回用户错误的信息，让用户决定如何去做。

悲观锁：总是假设最坏的情况，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样

别人想拿这个数据就会阻塞直到它拿到锁。

悲观锁的问题：总是需要竞争锁，进而导致发生线程切换，挂起其他线程；所以性能不高。

乐观锁的问题：并不总是能处理所有问题，所以会引入一定的系统复杂度。

乐观锁：多个线程竞争一把锁的概率会很低（效率高）

悲观锁：多个线程竞争一把锁的概率会很高（安全高）

### 9.2 读写锁

多线程之间，数据的读取方之间不会产生线程安全问题，但数据的写入方互相之间以及和读者之间都需要进行互

斥。如果两种场景下都用同一个锁，就会产生极大的性能损耗。所以读写锁因此而产生。

读写锁（readers-writer lock），看英文可以顾名思义，在执行加锁操作时需要额外表明读写意图，复数读者之间

并不互斥，而写者则要求与任何人互斥。

加锁操作分为两个步骤读锁和写锁

读锁与读锁之间是没有互斥的，也就是不存在锁竞争

读锁和写锁、写锁和写锁之间才是互斥的

场景：一写多读

### 9.3 重量级锁VS轻量级锁

加锁需要保证原子性。原子性功能来自与硬件操作。

在加锁过程中，如果整个加锁操作都是依赖操作系统内核，这就是重量级锁。（代码在内核执行开销大）

大部分操作都是用户都是自己完成，少数操作有内核完成。这就是轻量级锁

### 9.4 挂起等待锁VS自旋锁

挂起等待锁表示当前取锁失败后，对应的线程就要在内核中挂起（放弃CPU，进入等待队列），需要在锁释放后由操作系统唤醒。（通常是重量级锁）

自旋锁表示在获取锁失败后，不会立即放弃CPU，而是快速频繁询问锁的持有状态，一旦锁被释放，就能立刻获取到锁。（通常是轻量级锁。）

### 9.5 公平锁VS非公平锁

当锁释放之后，恰好又来了一个新的线程也要获取锁。

公平锁：保证之前先来的线程优先获取到锁

非公平锁：新来的线程直接获取到锁，之前的线程继续等待。

### 9.6 可重复锁

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

## 10. CAS

compare and swap（比较并交换）

```
我们假设内存中的原数据V，旧的预期值A，需要修改的新值B。 1. 比较 A 与 V 是否相等。（比较） 2. 如果
比较相等，将 B 写入 V。（交换） 3. 返回操作是否成功。
```

当多个线程同时对某个资源进行CAS操作，只能有一个线程操作成功，但是并不会阻塞其他线程,其他线程只会收到操作失败的信号。可见 CAS 其实是一个乐观锁。

应用场景

无锁编程：不使用锁，而是使用CAS来保证线程安全

### CAS 是怎么实现的

针对不同的操作系统，JVM 用到了不同的 CAS 实现原理，简单来讲：

1. java 的 CAS 利用的的是 unsafe 这个类提供的 CAS 操作；
2. unsafe 的 CAS 依赖了的是 jvm 针对不同的操作系统实现的 Atomic::cmpxchg；
3. Atomic::cmpxchg 的实现使用了汇编的 CAS 操作，并使用 cpu 硬件提供的 lock 机制保证其原子性。

简而言之，是因为硬件予以了支持，软件层面才能做到。

### CAS的应用

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

### ABA问题

ABA 的问题，就是一个值从A变成了B又变成了A，而这个期间我们不清楚这个过程。
解决方法：加入版本信息，例如携带 AtomicStampedReference 之类的时间戳作为版本信息，保证不会出现老的
值。

## 11. 锁优化-sychronized

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

### JUC

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

## 12.线程安全集合类

Vector，Srack，HashTable线程安全，其他的线程不安全

对于ArrayList来说

自己加锁或者Collection.sychronizedList

对于HashMap来说

自己加锁，HashTable，ConcurrentMap

## 面试

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
6. 计算密集型应用，为了能在多处理器系统上运行，将计算分解到多个线程中实现
7. I/O密集型应用，为了提高性能，将I/O操作重叠。线程可以同时等待不同的I/O操作。

11.2 进程与线程的区别

1. 进程是系统进行资源分配和调度的一个独立单位，线程是程序执行的最小单位。
2. 进程有自己的内存地址空间，线程只独享指令流执行的必要资源，如寄存器和栈。
3. 由于同一进程的各线程间共享内存和文件资源，可以不通过内核进行直接通信。
4. 线程的创建、切换及终止效率更高。

````
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
18、**你自己如何实现一个线程池，要用什么数据结构？**
19、**知道threatlocal吗？说一下原理**
20、用过哪些数据库，MySQL如何保证安全？有哪些锁？
21、静态方法和实例方法的区别，在内存中存放的位置
22、说下http协议，http1.0、http1.1、http2.0有什么区别？https呢？如何保证安全的？
````

# SpringBoot

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

## 默认的自动扫描

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

## 缓存

## 工作原理

![de6d2b213f112297298f3e223bf08f28](D:\Github\Note\picture\spring\de6d2b213f112297298f3e223bf08f28.png)

1. 客户端（浏览器）发送请求，直接请求到 `DispatcherServlet`。
2. `DispatcherServlet` 根据请求信息调用 `HandlerMapping`，解析请求对应的 `Handler`。
3. 解析到对应的 `Handler`（也就是我们平常说的 `Controller` 控制器）后，开始由 `HandlerAdapter` 适配器处理。
4. `HandlerAdapter` 会根据 `Handler`来调用真正的处理器开处理请求，并处理相应的业务逻辑。
5. 处理器处理完业务后，会返回一个 `ModelAndView` 对象，`Model` 是返回的数据对象，`View` 是个逻辑上的 `View`。
6. `ViewResolver` 会根据逻辑 `View` 查找实际的 `View`。
7. `DispaterServlet` 把返回的 `Model` 传给 `View`（视图渲染）。
8. 把 `View` 返回给请求者（浏览器）
9. 

# SpringCore

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

![s2](D:/Github/Note/picture/java/s2.jpg)





## 初始化/注册bean

### 类注解

在类上使用注解 `@Controller` ， `@Service` ， `@Repository` ， `@Component `。需要保证该类会被Spring
扫描到，这种定义方式默认会注册一个名称为类名首字母小写的Bean对象到容器中。

定义好了Bean对象，注册到容器中以后，就可以获取Bean对象了，在入口类 org.example.App 中，可以通过 ApplicationContext 对象获取Bean，有两种方式获取：

1、通过类型获取：这种获取方式要求该类型的Bean只能有一个
2、通过名称获取：同一个类型的Bean可以有多个

```java
package org.example.dao;
import org.example.model.User;
import org.springframework.stereotype.Repository;
@Repository
public class LoginRepository {
}

package org.example;
import org.example.dao.LoginRepository;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
public class App {
	public static void main(String[] args) {
		//根据Spring配置文件路径创建容器：应用上下文对象
		ApplicationContext context = new
		ClassPathXmlApplicationContext("beans.xml");
		LoginRepository loginRepository1 =(LoginRepository)context.getBean("loginRepository");
		LoginRepository loginRepository2 =context.getBean(LoginRepository.class);
        System.out.printf("loginRepository: %s%n", loginRepository1 ==loginRepository2);
        //关闭容器
		((ClassPathXmlApplicationContext) context).close();
	}
}
```



### @Bean

当前类被 Spring 扫描到时，可以在方法上使用 @Bean 注解，通过方法返回类型，也可以定义、注册
Bean对象，默认使用方法名作为Bean的名称。

```java
package org.example.model;
import lombok.Getter;
import lombok.Setter;
import lombok.ToString;
@Getter
@Setter
@ToString
public class User {
	private String username;
	private String password;
}
@Bean
public User user1(){
	User user = new User();
	user.setUsername("abc");
	user.setPassword("123");
	return user;
}
@Bean
public User user2(){
	User user = new User();
	user.setUsername("qwe");
	user.setPassword("123");
	return user;
}
```

### @Configuration

```java
package org.example.config;
import org.springframework.context.annotation.Configuration;
@Configuration
public class AppConfig {
}
```



### FactoryBean接口

#### 依赖注入

当前类被 Spring 扫描到时，可以在属性上使用 `@Autowired` 注解，会将容器中的Bean对象装配进来。

以下是在 `org.example.service.LoginService` 对象注册时，将`loginRepository` 对象从容器中装配到属性：

```java
package org.example.service;
import org.example.dao.LoginRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
@Service
public class LoginService {
	@Autowired
	private LoginRepository loginRepository;
}
//使用setter方法进行注入
package org.example.service;
import org.example.dao.LoginRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
@Service
public class LoginServiceBySetter {
	private LoginRepository loginRepository;
	public LoginRepository getLoginRepository() {
		return loginRepository;
	}
	@Autowired
	public void setLoginRepository(LoginRepository loginRepository) {
		System.out.printf("LoginServiceBySetter: loginRepository=%s%n",loginRepository);
		this.loginRepository = loginRepository;
	}
}
//使用构造方法进行构造（推荐使用）
package org.example.service;
import org.example.dao.LoginRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
@Service
public class LoginServiceByConstructor {
	private LoginRepository loginRepository;
	@Autowired
	public LoginServiceByConstructor(LoginRepository loginRepository){
		System.out.printf("LoginServiceByConstructor: %s%n", loginRepository);
		this.loginRepository = loginRepository;
	}
}
```

### 注入指定的Bean：@Qualifier

同类型的Bean有多个时，注入该类型Bean需要指定Bean的名称：
属性名或方法参数名设置为Bean的名称属性名或方法参数设置 @Qualifier("名称") 注解，注解内的字符串是Bean对象的名称
以下 loginController 中定义了5个用户对象，且在方法参数中注入了Bean对象

```java
package org.example.controller;
import org.example.model.User;
import org.example.service.LoginService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.context.annotation.Bean;
import org.springframework.stereotype.Controller;
@Controller
public class LoginController {
	@Autowired
	private LoginService loginService;
	@Autowired
	@Qualifier("user1")
	private User u;
	@Autowired
	private User user1;
	@Bean
	public User user1(){
		User user = new User();
		user.setUsername("abc");
		user.setPassword("123");
		return user;
	}
	@Bean
	public User user2(){
		User user = new User();
		user.setUsername("我不是汤神");
		user.setPassword("tang");
		return user;
	}
	@Bean
	public User user3(LoginService loginService){
		System.out.printf("user3: %s%n", loginService == this.loginService);
		return new User();
	}
	@Bean
	public User user4(User user1){
		System.out.printf("user4: user1=%s%n", user1);
		return new User();
	}
	@Bean
	public User user5(@Qualifier("user2") User u){
		System.out.printf("user5: user2=%s%n", u);
		return new User();
	}
}
```

## Spring AOP

AOP（Aspect Oriented Programming）称为面向切面编程，在程序开发中主要用来解决一些系统层面
上的问题，比如日志，事务，权限等等。

AOP利用一种称为"横切"的技术，将那些影响了多个类的公共行为封装到一个可重用模块，并将其命名
为"Aspect"，即切面。

使用"横切"技术，AOP把软件系统分为两个部分：核心关注点和横切关注点。业务处理的主要流程是核
心关注点，与之关系不大的部分是横切关注点。

横切关注点的一个特点是，他们经常发生在核心关注点的多处，而各处基本相似，比如权限认证、日
志、事物。AOP的作用在于分离系统中的各种关注点，将核心关注点和横切关注点分离开来。



### 使用场景以及应用

对以上统一业务来说，常见的切面业务如：

1. 响应统一的数据格式
2. 统一异常处理
3. 统一日志记录，如跟踪用户访问信息
4. 用户统一会话管理、权限管理
5. 方法执行时间计算
6. 事务管理
7. 其他

### 组成

**切面（Aspect）**
切面（Aspect）由 切点（Pointcut）和通知（Advice）组成，它既包含了横切逻辑的定义，也包括了连
接点的定义。Spring AOP就是负责实施切面的框架，它将切面所定义的横切逻辑织入到切面所指定的连
接点中。

**连接点（Join Point）**
应用执行过程中能够插入切面的一个点，这个点可以是方法调用时，抛出异常时，甚至修改字段时。切
面代码可以利用这些点插入到应用的正常流程之中，并添加新的行为。
在 Spring AOP 中，Join Point 总是方法的执行点, 即只有方法连接点。所以使用SpringAOP，无需使用
连接点的代码

**切点（Pointcut）**
Pointcut是匹配 Join Point 的谓词。
在 Spring 中, 所有的方法都可以认为是 Join Point，但是我们并不希望在所有的方法上都添加 Advice，
而 Pointcut 的作用就是提供一组规则（使用 AspectJ pointcut expression language 来描述）来匹配
Join Point，给满足规则的 Join Point 添加 Advice。

**通知（Advice）**
切面也是有目标的 ——它必须完成的工作。在AOP术语中，切面的工作被称之为通知。
通知：定义了切面是什么，何时使用，其描述了切面要完成的工作，还解决何时执行这个工作的问题。
Spring切面类中，可以在方法上使用以下注解，会设置方法为通知方法，在满足条件后会通知本方法进
行调用：
**前置通知**
使用@Before：通知方法会在目标方法调用之前执行。
**后置通知**
使用@After：通知方法会在目标方法返回或者抛出异常后调用。
**返回之后通知**
使用@AfterReturning：通知方法会在目标方法返回后调用。
**抛异常后通知**
使用@AfterThrowing：通知方法会在目标方法抛出异常后调用。
**环绕通知**
使用@Around：通知包裹了被通知的方法，在被通知的方法通知之前和调用之后执行自定义的行
为。

# SpringMVC

## 设计模式

![s1](D:/Github/Note/picture/java/s1.png)

**Model（模型）**是应用程序中用于处理应用程序数据逻辑的部分。

通常模型对象负责在数据库中存取数据。
**View（视图）**是应用程序中处理数据显示的部分。

通常视图是依据模型数据创建的。
**Controller（控制器）**是应用程序中处理用户交互的部分。

通常控制器负责从视图读取数据，控制用户输入，并向模型发送数据。

## @Controller

`@Controller`注解标注是一个类是Web控制器，其和`@Component`注解等价，只不过在Web层使用，其

便于区分类的作用。

## @RequestMapping

`@RequestMapping`是Spring Web应用程序中最常被用到的注解。

在对SpringMVC进行配置的时候，需要指定请求与处理方法之间的映射关系，这时候就需要使用

`@RequestMapping`注解。该注解可以在控制器类的级别和其方法级别上使用。

`@RequestMapping`注解能够处理的HTTP请求方法有：` GET, HEAD, POST, PUT, PATCH, DELETE,
OPTIONS, TRACE `。
为了能够将一个请求映射到一个特定的HTTP方法，你需要在@RequestMapping中使用method参数声
明HTTP请求所使用的方法类型。

```java
@RequestMapping("/test)
@RequestMapping(value="/index3",method = RequestMethod.GET)
```

## 控制器的方法返回

### String返回类型

有两种使用方式：

1. 返回 URI 资源路径的字符串，可以使用 redirect:/服务路径 **表示重定向到某个路径**，
   forward:/服务路径 **表示转发到某个路径**，如果前边不写**默认就是转发**。
2. `@RequestMapping`结合`@ResponseBody`，返回的字符串会作为响应体内容。此时响应的
   `Content-Type`为 `text/plain` 普通文本。

没有注解返回的就是页面，有注解返回文本

```java
    //进行重定向
	@RequestMapping("/index1")
    public String getIndex1(){
        logger.error("这是跳转链接");
        System.out.println("这是跳转连接");
        return "redirect:/index.html";
    }
//进行转发
    @RequestMapping("/index2")
    public String getIndex2(){
        logger.error("这是请求转发");
        System.out.println("请求转发");
        return "forward:/index.html";
    }
//默认转发
    @GetMapping("/index4")
    public String getIndex4(){
        logger.error("我是 index4");
        return "/index.html";
    }
//返回字符串
    @ResponseBody
    @RequestMapping("/index6")
    public String getIndex6(){
        System.out.println("index6");
        return "index/html";
    }
```

### 返回普通的Java类型

返回类型为Object，一般使用带Getter，Setter方法的模型类

结合@ResponseBody使用，表示将对象序列化后的数据放在响应体返回

在SpringBoot中默认响应的Content-Type为 application/json

非字符串对象会自动序列化为 json 字符串

```java
	private final ObjectMapper mapper =new ObjectMapper();
    @RequestMapping("/index7")
    @ResponseBody
    public String getIndex7() throws JsonProcessingException {
        System.out.println("index7");
        User user=new User();
        user.setUsername("Java");
        user.setPassword("最好的语言");
        logger.error("index7函数");
        return mapper.writeValueAsString(user);
    }

    @RequestMapping("/index8")
    @ResponseBody
    public User getIndex8(){
        System.out.println("index8");
        User user=new User();
        user.setUsername("Java");
        user.setPassword("最好的语言");
        return user;
    }
```

**返回ResponseEntity**

### @ResponseBody

1. 返回类型为String，表示响应`Content-Type: text/plain`，且响应体为控制器方法的字符串返回值
2. 返回类型为普通Java类型，表示响应`Content-Type: application/json`，以返回对象序列化为json后
   作为响应体。
3. `@ResponseBody`可以使用在类上，表示该类中所有方法都是默认以返回值作为响应体，也就是所
   有方法都使用`@ResponseBody`。

### 控制器方法支持的参数类型

#### @PathVariable

一般的 URI 服务路径都是固定的，SpringMVC提供了 restful 风格可以变化的 URI。

作用：使用URL的动态参数作为方法的参数

```java
    @RequestMapping("/people/{pid}/pets/{aid}")
    public String method1(@PathVariable("pid") String id1,@PathVariable("aid") String id2) {
        logger.error("用户id:"+id1+",宠物id:"+id2);
        return "用户id:"+id1+",宠物id:"+id2;
    }
```

1、{}是将服务路径 URI 中的部分定义为变量，之后在方法参数中获取该路径变量。更多格式可参考URI格式。
2、请求 /people/1/pets/2 ，显示的网页内容为： 主人id：1, 宠物id：2 。
3、变量已经定义了为String字符串，所以不能转换为字符串的 URI 都会报错。
4、变量名ownerId，petId必须和 URI 中的定义名称一致。

#### @RequestParam

当请求数据要绑定到某个简单对象时，可以使用@RequestParam。

1、URL 中的请求数据queryString

2、请求头，Content-Type为表单默认提交的格式` application/x-www-form-urlencoded` ，请求体中的数据

3、请求头，Content-Type为 `multipart/form-data` ，请求体中的数据。form-data 可以提交文本数据，也可以提交二进制文件。

以上简单对象包括：基本数据类型、包装类型、MultipartFile（接收二进制文件）

### POJO对象

POJO（Plain Ordinary Java Object）：简单的 java 对象，实际就是属性提供了Getter，Setter方法的普通对象。

使用 java 对象和使用@RequestParam注解非常类似，只是有点细节不同：

@RequestParam是以方法参数变量名和传入的键对应，POJO对象作为方法参数时，是以POJO对象中的属性名对应传入的键

@RequestParam默认必须传入该请求数据，而 POJO 对象是根据请求数据来填充属性，如果请求
数据没有，则属性就是默认值（new对象时每个属性的默认值)。

```java
//和@RequestParam一样
@PostMapping("/pojo1")
public Object pojo1(String username, Integer count){
	Map<String, String> map = new HashMap<>();
	map.put("用户名", username);
	map.put("count", String.valueOf(count));
	return map;
}
//传入参数需要与字段对应
@PostMapping("/pojo2")
	public Object pojo2(User user){
	Map<String, String> map = new HashMap<>();
	map.put("用户名", user.getUsername());
	map.put("密码", user.getPassword());
	return map;
}
@PostMapping("/pojo3")
public Object pojo3(User user, MultipartFile file) throws IOException {
	Map<String, String> map = new HashMap<>();
	map.put("用户名", user.getUsername());
	map.put("密码", user.getPassword());
	map.put("文件名", file.getName()+", "+file.getOriginalFilename());
	map.put("文件类型", file.getContentType());
	map.put("文件大小", file.getSize()/1024+"KB");
	map.put("文件内容（二进制转字符串）", new String(file.getBytes()));
	return map;
}
```

### @RequestBody

4、当请求的数据类型Content-Type为` application/json `时，需要显示的使用`@RequestBody`注解

```java
    private static final String USERNAME="username";
    private static final String PASSWORD="password";
    @RequestMapping("/login")
    @ResponseBody
    public String login(@RequestBody User user, HttpServletRequest req){
        if(USERNAME.equals(user.getUsername())&&PASSWORD.equals(user.getPassword())){
            req.getSession().setAttribute("user",user);
            return "登录成功";
        }else{
            return "登录失败";
        }
    }
```

### @RequestPart

对于请求的数据类型Content-Type为 multipart/form-data 时，二进制文件除了以上@RequestParam和 POJO 对象的方式外，还可以使用@RequestPart

```java
    @RequestMapping("/register")
    public Object register(String username, @RequestPart MultipartFile file) throws IOException {
        //动态获取路径
        String path= Objects.requireNonNull(Objects.requireNonNull(ClassUtils.getDefaultClassLoader()).getResource("static")).getPath();
        System.out.println(username);
        logger.error(path);
        path+="/upload/";
        //获取文件名字，目的是获取文件格式
        String fileType=file.getOriginalFilename();
        assert fileType != null;
        fileType=fileType.substring(fileType.lastIndexOf("."));
        String fileName= UUID.randomUUID() +fileType;
        file.transferTo(new File(path+fileName));
        return null;
    }
```

### Servlet API

在控制器方法参数中，可以使用Servlet相关API，SpringMVC会自动将相关Servlet对象装配到方法参数
中，如 `HttpServletRequest `、`HttpServletResponse` 、`HttpSession` 等。

返回值设置为void，此时和在Servlet中开发差不多了。

当然也可以使用返回值，`SpringMVC`会自动跳转
页面（无`@ResponseBody`，返回类型为`String`），或返回`Content-Type: text/html`的网页内容（使用

`@ResponseBody`，返回类型为`String`），或返回 `json` 字符串（`@ResponseBody`，返回` POJO `对象）

### @RequestHeader

```java
@GetMapping("/header")
public String header(@RequestHeader("Accept-Encoding") String encoding,
@RequestHeader("User-Agent") String userAgent) {
return String.format("<p>Accept-Encoding: %s</p><p>User-Agent: %s</p>",
encoding, userAgent);
}
```

### CookieValue

```java
@GetMapping("/cookie")
public String cookie(@CookieValue("JSESSIONID") String cookie) {
	return String.format("JSESSIONID: %s", cookie);
}
```

### 自定义后端路径映射

SpringBoot中使用SpringMVC非常方便，SpringBoot提供了大部分的MVC默认功能，并且需要自定义

某部分功能也非常方便，在配置类中实现 WebMvcConfigurer 接口，根据需要重写方法即可：

```java
//注意事项1：这个注解将类注册，托管给框架
@Configuration
public class AppConfig implements WebMvcConfigurer {、
    @Override
    public void configurePathMatch(PathMatchConfigurer configurer) {
        configurer.addPathPrefix("api",c->true);
    }

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        System.out.println("拦截器启动");
        registry.addInterceptor(new LoginInterceptor()).addPathPatterns("/**");
    }
}
```

```java
@Override
public void configurePathMatch(PathMatchConfigurer configurer) {
	//Controller路径，统一添加请求的路径前缀，第二个参数，c是Controller类，返回boolean表示是否添加前缀
	//所有Controller请求路径，都要带/api的前缀
	configurer.addPathPrefix("api", c->true);
}
```

### 自定义拦截器

```java
//注意事项1：实现接口
@RestController
public class LoginInterceptor implements HandlerInterceptor {
    @Override
	public boolean preHandle(HttpServletRequest request, HttpServletResponseresponse, Object handler) throws Exception {
		HttpSession session = request.getSession(false);
		//session不为空，表示已登录
		if(session != null){
		//返回true，允许继续执行Controller中的方法
			return true;
		}
		//响应状态码设置为401
		response.setStatus(HttpStatus.UNAUTHORIZED.value());
		//返回false，不再执行Controller中的方法，直接响应一个空的响应体
		return false;
    }|
}

```

```java
@Override
public void addInterceptors(InterceptorRegistry registry) {
	registry.addInterceptor(new LoginInterceptor())
	.addPathPatterns("/api/**")//添加路径拦截规则，**表示下级多级目录的任意字符匹配
	.excludePathPatterns("/api/user/login");//排除登录路径
}
```

### @ControllorAdvice

**统一异常处理**

```java
//注意事项1：//在SpringBoot中使用，会扫描启动类所在包下所有@Controller类
@ControllerAdvice
public class ErrorException {
    //注意事项2：如果客户端请求，执行控制器方法抛Exception异常，会执行本方法
    @ExceptionHandler(Exception.class)
    //注意事项3：返回json字符串
    @ResponseBody
    public Object method1(Exception e){
        Map<String,Object> map=new HashMap<>();
        map.put("status",-1);
        map.put("data","");
        map.put("msg",e.getMessage());
        return map;
    }
}
```

**统一返回**

```java
//注意事项1：实现ResponseBodyAdvice接口，表示可以根据条件对返回的数据重写
public class MyResponseBody implements ResponseBodyAdvice {
    //注意事项2：Sring框架注入
    @Autowired
    private ObjectMapper objectMapper;

    //注意事项3：true表示开启，false表示关闭
    @Override
    public boolean supports(MethodParameter returnType, Class converterType) {
        return false;
    }

    @SneakyThrows
    @Override
    public Object beforeBodyWrite(Object body,
                                  MethodParameter returnType,
                                  MediaType selectedContentType,
                                  Class selectedConverterType,
                                  ServerHttpRequest request,
                                  ServerHttpResponse response) {
        HashMap<String,Object> map=new HashMap<>();
        map.put("status",0);
        map.put("data",body);
        map.put("msg","");
        //注意事项4：如果控制器方法返回类型为字符串，响应的Content-Type为text/plain，手动设置为json，并重写为序列化后的json字符串
        if(body instanceof String){
            response.getHeaders().setContentType(MediaType.APPLICATION_JSON);
            return objectMapper.writeValueAsString(map);
        }
        return map;
    }
}
create table user(
    id int primary key auto_increment,
    username varchar(50) not null,
    password varchar(32) not null,
    photo varchar(100) not null,
    createtime datetime default now(),
    updatetime datetime default now()
);
```


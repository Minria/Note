# 1. 八大基本数据类型

## 1.1 整型(4)

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

## 1.2 浮点型(2)

基本语法格式

```java
float num1=10.1F;//这个后面不带Fh
double num2=10.1;
```

在 Java 中, int 除以 int 的值仍然是 int，后面的小数点被舍去，如果需要得到小数，就需要转换为浮点数进行运算

## 1.3 字符类型(1)

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

## 1.4 布尔类型变量(1)

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

## 1.5 BigInteger and BigDecimal

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

 

# String类型变量

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

## 2.1 字符串的创建

```java
String str1 = "abcdefg";
String str2 = new String("abcdefg");
char[] array = {'a','b','c'};
String str3 = new String(array);
```

##  2.2 字符串相等的比较

```java
String str1 = "abcdefhg";
String str2 = "abcdefhg";
System.out.println(str1==str2);
System.out.println(str1.equals(str2));
System.out.println("abcdefhg"==str2);
System.out.println("abcdefhg".equals(str1));
```

## 2.3 字符串的不可变性

双引号引起的是字面值常量，无法修改

## 2.4 字符与字符串

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

## 2.5 字节与字符串

```java
public String(byte bytes[]);
//将字节数组中的内容变为字符串
public String(byte bytes[],int offset,int count);
//将字节数组的部分内容变为字符串
public byte[] getBytes();
//字符串以字节的形式返回
```

## 2.6 字符串的常见的操作

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

##  2.7 StringBuilder与StringBuffer

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

## 2.8  转义字符

| 字符 | 意义       |
| ---- | ---------- |
| \n   | 换行       |
| \t   | 水平制表符 |
| \\'  | 单引号     |
| \\"  | 双引号     |
| \\\  | 反斜杠     |

# 3. 常量

## 3.1 字面值常量

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

## 3.2 final修饰常量

```java
final int a = 10;
a = 20; // 编译出错,提示无法为最终变量a分配值
```

> 有点类似C语言中的const修饰变量
>
> java: 无法为最终变量a分配值

## 3.3 类型转换

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



# 4. 方法

Java中的方法实质上就是C语言中的函数.

## 4.1 方法的重载

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

# 5. 数组

## 5.1 数组是什么

数组本质上就是一组相同数据类型的数据结构。

## 5.2 创建数组

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

## 5.3 数组使用

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

## 5.4 数组和方法

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

##  Arrays方法

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

# 6. 面向对象

## 6.1 类和对象

## 类

类是构造对象的模板或蓝图。由类构造对象的过程称为创建类的实例。

类的成员可以包含以下：

1. 字段、属性或者成员，又分普通成员变量和静态成员变量

   普通成员变量：属于对象，放在堆区，通过对象访问

   **静态成员变量：属于类，放在方法区，又称类变量，通过类名访问**

2. 方法

3. 代码块

4. 内部类

5. 接口

### 普通成员

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

### 静态成员变量

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



## 封装

### private实现封装

private和public这两个关键字表示"访问权限控制"。

1. 被public修饰的成员变量或者成员方法，可以被类直接调用者调用。
2. 被private修饰的成员变量或者成员方法，不能被类的调用者调用。

> 换句话说, 类的使用者根本不需要知道, 也不需要关注一个类都有哪些 private 的成员. 从而让类调用者以更低的成本来使用类。

### getter和setter方法

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



## 构造方法

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



## 关键字this

this和super有什么区别？

this.data--------调用当前对象的属性

this.func()------调用当前对象的方法

this()-------------调用当前对象的其他构造方法，只能存放在构造函数中

必须放到第一行

## 代码块

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

# 面向对象

## 包

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

### 将类放到包中

基本规则
1、在文件的最上方加上一个 package 语句指定该代码在哪个包中.
2、包名需要尽量指定成唯一的名字, 通常会用公司的域名的颠倒形式(例如` com.bit.demo1 `).

3、包名要和代码路径相匹配. 例如创建 `com.bit.demo1`的包, 那么会存在一个对应的路径 `com/bit/demo1` 来存储代码.
3、如果一个类没有 package 语句, 则该类被放到一个默认包中.

上面的流程就是我们在`com.bit.demo1`新建了了`Main`类。

### 包的访问权限

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

### 常见的系统包

常见的系统包
1. java.lang:系统常用基础类(String、Object),此包从JDK1.1后自动导入。
2. java.lang.reflect:java 反射编程包;
3. java.net:进行网络编程开发包。
4. java.sql:进行数据库开发的支持包。
5. java.util:是java提供的工具程序包。(集合类等) 非常重要
6. java.io:I/O编程开发包。

## 继承

### 背景

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

### 语法规则

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



## 组合
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

## 多态

同时发生向上转型和动态绑定

向上转型：父类引用指向子类的实例

动态绑定：子类重写父类同名方法，并由父类引用调用方法

### 向上转型

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

### 动态绑定

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

### 方法重写

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

### 理解多态

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



## 抽象类

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

## 接口

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

# 异常

## 异常的背景

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

## LBYL&&EAFP

**LBYL**: Look Before You Leap.
**EAFP**: It's Easier to Ask Forgiveness than Permission.

前者在程序执行前解决问题，后者出现问题后解决

## 异常的好处

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

## 异常的用法

### 捕获异常

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

### 异常处理

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

### 异常声明

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

## Java异常体系

## 自定义异常

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

## 有关throws和throw

1、位置不同：throws在方法的声明后面，后面跟的是异常类名，而throw在方法的内部，后面跟的是异常的类名

2、抛出数量不同：throws可以抛出多个异常类，用逗号隔开，而throw只能抛出一个异常对象

3、处理方法不同：throws抛出后由该方法的调用者来处理，后者由由该方法体内的语句来处理

4、可能性不同：throws表示有出现异常的可能性，并不一定出现这些异常，throw一定有异常

可以对比上面自定义登录的例子

可以看见`throws`后面抛出类，`throw`后面抛出对象

`throws`抛出账户错误和密码错误两个类，后着抛出一个准确的对象

当账户密码正确`throws`就不会抛出异常


# 数据类型

## 变量和类型

### 整型

基本语法格式

```java
int name = data;
```

实例

```java
int num = 1;//定义一个整型变量，数值为1
System.out.println(num);
```

```java
System.out.println(Integer.MAX_VALUE);//整型数据最大值
System.out.println(Integer.MIN_VALUE);//整型数据最小值
```

### 长整型变量

基本语法格式

```java
long name = data;
```

实例

```java
long num=1L;//定义一个长整型变量，初始值为 1L 
long num2=1l;//后面的字母也可以用小写，但是小写特别像1，改用大些用以区分
```

### 双精度浮点型

基本语法格式

```java
double name = data;
```

实例

```java
double num = 1.0;
```

### 单精度浮点型

基本语法格式

```java
float name = data;
```

实例

```java
float num = 1.0f;
float num2=2.0F;
```

### 字符类型

基本语法格式

```java
char name = data;
```

实例

```JAVA
char ch = 'A';
```

需要注意的是，**Java中字符类型占两个字节**，与C语言中所占一个字节有区别

### 字节类型变量

基本语法格式

```java
byte name = data;
```

实例

```JAVA
byte value=0;
```

在C语言中没有这个类型，这个类型占一个字节。

### 短整型变量

基本语法格式

```java
short name = data;
```

### 布尔类型变量

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

### 字符串类型变量

在C语言中没有字符串类型，但是在Java中有字符串类型

```java
String name = "data";
```

实例

```java
String name = "java";
```

区分

```java
char ch='A';
String str="A";
```

**注意**

1. Java 使用 双引号 + 若干字符 的方式表示字符串字面值。
2. 和上面的类型不同, String 不是基本类型, 而是引用类型。
3. 字符串中的一些特定的不太方便直接表示的字符需要进行转义。

**字符串的子串**

使用String类的substring方法可以从一个较大的字符串中提出一个字串

```java
public class TestPratice {
    public static void main(String[] args) {
        String a="abcdefgh";
        String b=a.substring(0,2);
        System.out.println(b);
    }
}
//预计输出ab
```



![Snipaste_2021-10-15_16-03-33](https://gitee.com/wang-fuming/dawning/raw/master/202110151604178.png)

**字符串的拼接**

```java
String a = "hello";
String b = "world";
String c = a + b;
System.out.println(c);
```

```java
String str = "result = ";
int a = 10;
int b = 20;
String result = str + a + b;
System.out.println(result);
```

### 转义字符

| 字符 | 意义       |
| ---- | ---------- |
| \n   | 换行       |
| \t   | 水平制表符 |
| \\'  | 单引号     |
| \\"  | 双引号     |
| \\\  | 反斜杠     |

## 常量

### 字面值常量

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



### final修饰常量

```java
final int a = 10;
a = 20; // 编译出错,提示无法为最终变量a分配值
```

> 有点类似C语言中的const修饰变量

![](https://gitee.com/wang-fuming/dawning/raw/master/202110131647709.png)

## 类型转换

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

![Snipaste_2021-10-12_20-56-56](https://gitee.com/wang-fuming/dawning/raw/master/202110122058078.png)

![Snipaste_2021-10-12_20-57-47](https://gitee.com/wang-fuming/dawning/raw/master/202110122058761.png)

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



## 运算符

### 基本四则运算符

整型相除还是整型，如果需要得到小数就需要double型变量进行运算

### 关系运算符

```== != < > <= >=```

```java
int a = 10;
int b = 20;
System.out.println(a == b);
System.out.println(a != b);
System.out.println(a < b);
System.out.println(a > b);
System.out.println(a <= b);
System.out.println(a >= b);
```

![Snipaste_2021-10-11_16-39-27](https://gitee.com/wang-fuming/dawning/raw/master/202110111639797.png)

### 逻辑运算符

```&& || !```

逻辑于------->两者都为真时为真

逻辑或------->一个为真时即为真

取反---------->真变假，假变真

对于```a&&b```如果a为假则结束，不在判断b是真是假

对于```a||b```如果a为真则结束，不在判断b是真是假

### 位运算符

```&  | ~ ^```

**注意**：位操作符是对**二进制**位进行运算

```a&b```--------->二进制位都是1则为1，否则取0

```a|b```--------->二进制位只要有一个为1就是1

```~a```---------->取反，二进制位是1则变0，0则变为1

```a^b```--------->二进制位相同为0，相异为1

> a=11001B=25
>
> b=10110B=22
>
> a&b=10000B=16
>
> a||b=11111=31
>
> a的补码0....11001取反1....00110--->原码1....11010=  -26
>
> a^b=01111=15

![Snipaste_2021-10-12_21-28-01](https://gitee.com/wang-fuming/dawning/raw/master/202110122128424.png)

# 逻辑结构

## 分支结构

### if

```java
//格式1
if(a){
    
}
//格式2
if(a){
    
}else{
    
}
//格式3
if(a){
    
}else if(b){
    
}else if(c){
    
}else{
    
}
```

需要注意的是，**条件必须是布尔表达式**

在C语言中```if(1)```表示进入执行，在Java中必须是```if(true)```

C语言中0代表false，非0代表true，但是在java中必须是true或者false

**需要注意的else的悬垂问题**

```java
int x = 10;
int y = 20;
if(x==10)
    if(y==10)
        System.out.println("true");
else
    System.out.println("false");
    
```

我们很容易看见else和第一个if在同一个缩进上，所以什么也不输出？

![Snipaste_2021-10-16_19-50-03](https://gitee.com/wang-fuming/dawning/raw/master/202110161951201.png)

我们看到输出了false，看来是进入到else和第二个循环是一起的

**else和它最近的if在一起**

在idea编译器中，敲下回车，自动缩进在第二个if。

### switch

```java
switch(整数|枚举|字符|字符串){
    case 内容1 : {
        内容满足时执行语句;
        [break;]
    }
    case 内容2 : {
        内容满足时执行语句;
        [break;]
    }
    default:{
        内容都不满足时执行语句;
        [break;]
    }
}
```

整数和字符很常见，字符串类型好像没有见过，下面给出例子

![Snipaste_2021-10-16_19-55-41](https://gitee.com/wang-fuming/dawning/raw/master/202110161955595.png)

## 循环结构

### while循环

```java
while(a){
    
}
```

### for循环

```java
for(a;b;c){
    
}
```

### do while循环

```java
do{
    
}while(a);
```

需要注意的是，**do while循环先执行后判断，while先判断后执行**

![Snipaste_2021-10-16_20-00-18](https://gitee.com/wang-fuming/dawning/raw/master/202110162000811.png)

### break和continue

两者都是让循环结束，但是不同的是

break会直接结束整个循环

continue结束当前循环，进入下一个循环。

## 输入输出

### 输出

```java
System.out.println(data); // 输出一个字符串, 带换行
System.out.print(data); // 输出一个字符串, 不带换行
System.out.printf(format, data); // 格式化输出,类似C语言中的printf
```



### 输入

Java中输入比较复杂

```java
import java.util.Scanner; // 需要导入 util 包
Scanner scanner = new Scanner(System.in);
System.out.println("请输入你的姓名：");
String name = scanner.nextLine();
System.out.println("请输入你的年龄：");
int age = scanner.nextInt();
System.out.println("请输入你的工资：");
float salary = scanner.nextFloat();
System.out.println("你的信息如下：");
System.out.println("姓名: "+name+"\n"+"年龄："+age+"\n"+"工资："+salary);
sc.close(); // 注意, 要记得调用关闭方法
```

如果需要多组输入

```java
Scanner sc = new Scanner(System.in);
double sum = 0.0;
int num = 0;
while (sc.hasNextDouble()) {
    double tmp = sc.nextDouble();
    sum += tmp;
    num++;
}
System.out.println("sum = " + sum);
System.out.println("avg = " + sum / num);
sc.close();
```





# 方法

Java中的方法实质上就是C语言中的函数。

来一个求和方法

```java
public static int addSum(int n){
    int sum = 0;
    for(int i=1;i<=n;i++){
        sum+=i;
    }
    return sum;
}
```

## 方法的重载

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

![Snipaste_2021-10-23_15-47-53](https://gitee.com/wang-fuming/dawning/raw/master/202110231548032.png)

方法的名字都叫 add. 但是有的 add 是计算 int 相加, 有的是 double 相加; 有的计算两个数字相加, 有的是计算三个数字相加.

同一个方法名字, 提供不同版本的实现, 称为**方法重载**

需要注意的是

1. 方法名相同
2. 方法的参数不同(参数个数或者参数类型)
3. 方法的返回值类型不影响重载.

区分的重点是函数名字后面的参数（类型或者数量）

## 方法的递归

一个方法在执行的过程中自身调用自身的过程就称为递归。

为了避免死循环，递归必须要有中止条件

# 数组

## 数组基础

### 数组是什么

数组本质上就是一堆相同类型的变量。

### 创建数组

Java数组创建和C语言有所不同

下面以整型数组为例

```java
int[] num = new int[]{1,2,3};//动态初始化
int[] arr = {1,2,3};//静态初始化
```

### 数组使用

一般是获取数组长度以及根据下标访问数组

```java
        int[] arr={1,2,3,4,5};
        int len= arr.length;
        for(int i=0;i<len;++i){
            System.out.println(arr[i]);
        }
```

![Snipaste_2021-10-13_20-01-16](https://gitee.com/wang-fuming/dawning/raw/master/202110132001300.png)

需要注意的是

1. 在Java中使用.length得到数组的长度
2. 下标访问不可越界

# 类和对象

类有些像C语言中的结构体，对象则对应结构体变量。

## 类的成员

类的成员可以包含以下：

1. 字段
2. 方法
3. 代码块
4. 内部类
5. 接口

### 字段

```java
class Person{
    public String name;
    public int age;
}
class Main(){
    public static void main(String[] args){
        Person person = new Person;
        System.out.println(person.name);
        System.out.println(person.age);
        
    }
}
```



## 封装

### private实现封装

private和public这两个关键字表示"访问权限控制"。

1. 被public修饰的成员变量或者成员方法，可以被类直接调用者调用。
2. 被private修饰的成员变量或者成员方法，不能被类的调用者调用。

> 换句话说, 类的使用者根本不需要知道, 也不需要关注一个类都有哪些 private 的成员. 从而让类调用者以更低的成本来使用类.

# String类

## 字符串的创建

```java
String str1 = "abcdefg";

String str2 = new String("abcdefg");

char[] array = {'a','b','c'};
String str3 = new String(array);
```

## 字符串相等的比较

```java
String str1 = "abcdefhg";
String str2 = "abcdefhg";
System.out println(str1==str2);
System.out println(str1.equals(str2));
System.out println("abcdefg"==str2);
System.out println("abcdefg".equals(str1));
```

## 字符串的不可变型

## 字符，字节与字符串

### 字符与字符串

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

### 字节与字符串

```java
public String(byte bytes[]);
//将字节数组中的内容变为字符串
public String(byte bytes[],int offset,int count);
//将字节数组的部分内容变为字符串
public byte[] getBytes();
//字符串以字节的形式返回

```


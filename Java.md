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

### 字节类型变量

基本语法格式

```java
byte name = data;
```

实例

```JAVA
byte value=0;
```

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

在C语言中没有字符串类型，但是在java中有字符串类型

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

# 分支和循环

## 分支结构

```java
//格式1
if(a){
    
}
//格式2
if(a){
    
}
else{
    
}
//格式3
if(a){
    
}
else if(b){
    
}
else if(c){
    
}
else{
    
}
```

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

### break和continue

两者都是让循环结束，但是不同的是

break会直接结束整个循环

continue结束当前循环，进入下一个循环


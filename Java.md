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

```java
String name = "data";
```

实例

```java
String name = "java";
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


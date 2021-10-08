﻿﻿﻿﻿﻿﻿﻿﻿﻿﻿﻿﻿﻿﻿[TOC]

# 数组

##  一维数组

### 什么是数组

数组是一组相同类型元素的集合。
有整型数组，字符型数组等。

### 数组的创建

```c
type_t   arr_name   [const_n];
//type_t 是指数组的元素类型
//const_n 是一个常量表达式，用来指定数组的大小
int arr1[10];
char arr2[10]
float arr3[10];
double arr[10];
```

注：数组创建， [] 中要给一个**常量**才可以，不能使用变量

### 数组的初始化

数组的初始化是指，在创建数组的同时给数组的内容一些合理初始值（初始化）。

```c
int arr1[10]={1,2,3};
char arr2[10]="ancd";
char arr3[10]={'a','b','c','d','\0'};//'\0'是字符串结束标志
int arr4[]={1,2,3,4};
char arr5[]="abcdef";
char arr6[]={'a','b','c'};
```

需要说明的是

>字符型数组"abcde"创建在末尾自动包含结束标识'\0'

### 数组的使用

对数组的使用都是从下标开始的访问元素

>C语言数组的下标是从0开始的。

```c
int arr[5]={1,2,3,4,5};
int a=arr[0];
int b=arr[1];
int c=arr[2];
int d=arr[3];
int e=arr[4];
int f=arr[5];
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/e571ddd27f014875bc4e0cd6a9601aba.png#pic_center)

==可以看到a,b,c,d,e的值一一对应，而f的值不存在就是一个随机值。==

###  一维数组在内存中的存储

![在这里插入图片描述](https://img-blog.csdnimg.cn/4826447d6da4448db02af691a518f573.png#pic_center)

==由此可见一维数组地址是连续存放并且递增的。==

## 二维数组

### 数组的创建

```c
int arr[3][3];
char arr1[3][3];
double arr2[3][3];
```

### 数组的初始化

```c
int arr[3][3]={1,2,3,4,5,6,7,8,9};
int arr2[3][3]={{1,2,3},{4,5,6},{7,8,9}};
int arr2[][3]={{1,2,3},{4,5,6},{7,8,9}};//初始化才可以省略行，不初始化不能
```

### 数组的使用

同样也是引用下标来实现，规定行列从0开始，第一行的第一列元素的下标为[0] [0].

### 数组在内存中的存储

```c
#include <stdio.h>
int main(){
	int arr[3][4] = { 1,2,3,4,5,6,7,8,9 };
	int i = 0;
	for (i = 0; i < 3; i++){
		int j = 0;
		for (j = 0; j < 4; j++){
			printf("&arr[%d][%d] = %p\n", i, j, &arr[i][j]);
		}
	}
	return 0;
}
```

![Snipaste_2021-10-07_18-18-20](https://gitee.com/wang-fuming/dawning/raw/master/202110071818836.png)  

​       ==二维数组的地址也是连续存放且递增的。==



# 函数

## 函数是什么

维基百科定义为：子程序

## 库函数

使用库函数必须引用头文件

>⭐️有关C语言库函数👉🔑[C++库函数](http://www.cplusplus.com/reference/)⭐️

这里解析库函数字符串赋值函数strcpy

```c
//字符串赋值函数strcpy
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<string.h>
int main() {
	char str1[20] ="xxxxxxxxx";
	printf("%s\n", str1);
	char str2[20]= "hello";
	strcpy(str1, str2);
	printf("%s\n", str1);
	return 0;
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/4067a1b35e6a421ca40aa373f0986ee2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

>字符串结束标志'\0'不占长度但占空间
>
> memset 函数

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<string.h>
int main() {
	char str[] = "hello bit";
	memset(str, 'x', 5);
	printf("%s\n", str);

}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/4863f9caf80b4cf4b8303c19185cc895.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

## 自定义函数

库函数那么方便，为什么还要自定义函数？

>库函数不能解决所有需求，所以需要自定义函数

库函数和自定义函数有什么区别？

>基本没有什么区别，只是实现的功能不同，和库函数一样，有返回类型，函数名，函数参数

下面是自定义一个两个数交换的函数

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
void swap(int a, int b);
int main() {
	int a = 10;
	int b = 20;
	swap(a, b);
	printf("%d %d",a,b);
	return 0;
}
void swap(int a, int b) {
	a = a - b;
	b = a + b;
	a = b - a;
	printf("%d %d\n", a, b);
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/a1835cab90ba41f591ef1b55ae177dd9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


>上面程序运行的结果，我们发现我们自定义的swap函数虽然实现了两个数的交换并输出，然而在main函数中输出的a，b并没有交换，这需要后面函数的调用来解释为什么main函数中没有交换并说明怎么实现

## 函数的参数

### 实际参数（实参)

  >真实传给函数的参数，叫实参。实参可以是：常量、变量、表达式、函数等。无论实参是何种类型的量，在进行函数调用时，它们都必须有确定的值，以便把这些值传送给形参。

### 形式参数（形参）

 >形式参数是指函数名后括号中的变量，因为形式参数只有在函数被调用的过程中才实例化（分配内存单元），所以叫形式参数。形式参数当函数调用完成之后就自动销毁了。因此形式参数只在函数中有效。
 >由上面函数代码执行可以知道：**形参是实参的临时拷贝,改变形参的值并不会改变实参的值。**

## 函数的调用

### 传值调用

>函数的形参和实参分别占有不同内存块，对形参的修改不会影响实参。

### 传址调用

>传址调用是把函数外部创建变量的内存地址传递给函数参数的一种调用函数的方式。这种传参方式可以让函数和函数外边的变量建立起正真的联系，也就是函数内部可以直接操作函数外部的变量。
>我们上面的函数就是传值调用，这样的调用由于形参知识实参的临时拷贝，并不会改变实参的值。但是通过传址调用则可以改变实参的值。

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
void swap(int a, int b);
int main() {
	int a = 10;
	int b = 20;
	swap(&a, &b);//将a，b的地址传过去
	printf("%d %d", a, b);
	return 0;
}
void swap(int *a, int *b) {
	*a = *a - *b;
	*b = *a + *b;
	*a = *b - *a;
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/42f8ec99588c4c3ab6adc49ff45f1ac3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

下面是执行结果，我们可以看见a，b的值已经交换。

## 函数的嵌套调用和链式访问

函数和函数之间可以有机的组合的。

### 嵌套调用

函数中调用其他函数，最容易理解的就是主函数中调用输入输出函数等。

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
void funtion1(int x, int y) {

}
void funtion2(int x, int y) {
	funtion1(x, y);
}
void function3(int x, int y) {
	function2(x, y);
}
int main(){
	int a, b;
	function3(a, b);
	return 0;
}
```

以上就是函数间的嵌套使用

>我们看见fun2函数调用fun1函数，fun3函数调用fun2函数，main函数调用fun3函数

### 链式访问

把一个函数的返回值作为另外一个函数的参数。


```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
int main()
{
    char arr[20] = "hello";
    printf("%d\n", strlen(strcat(arr, "bit")));
    return 0;
}
```

这里我们直接将strlen返回值当作参数输入printf函数中。

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
int main(){
    printf("%d", printf("%d", printf("%d", 43)));
    //结果是啥？
    return 0;
}
```

![Snipaste_2021-10-07_18-19-55](https://gitee.com/wang-fuming/dawning/raw/master/202110071820479.png)

## 函数的声明和定义

### 函数声明

>1. 告诉编译器有一个函数叫什么，参数是什么，返回类型是什么。但是具体是不是存在，无关紧要。
>2. 函数的声明一般出现在函数的使用之前。要满足先声明后使用。
>3. 函数的声明一般要放在头文件中的。

### 函数定义

  >函数的定义是指函数的具体实现，交待函数的功能实现。

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
void swap(int x, int y) {

}
int main() {
	int a=10, b=20;
	swap(a,b);
	return 0;
}
```

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
void swap(int x, int y);
int main() {
	int a=10, b=20;
	swap(a,b);
	return 0;
}
void swap(int x, int y) {

}
```

⭐️⭐️⭐️

>注意：函数的定义代码块不可以写在其他函数。

## 函数递归

### 什么是递归

>程序调用自身的编程技巧称为递归（ recursion）。 
>递归做为一种算法在程序设计语言中广泛应用。 一个过程或函数在其定义或说明中有直接或间接调用自身的一种方法，它通常把一个大型复杂的问题层层转化为一个与原问题相似的规模较小的问题来求解，递归策略只需少量的程序就可描述出解题过程所需要的多次重复计算，大大地减少了程序的代码量。 

>递归的主要思考方式在于：把大事化小。例如在求阶乘，求n时我们只需要求n-1，求n-1只需要n-2，最后编程求1

代码如下

```c
int fact(int n) {
	if (n <= 1)
		return 1;
	else
		return n * fact(n - 1);
}
```

行不行呢直接开跑

```c
#include<stdio.h>
int fact(int n) {
	if (n <= 1)
		return 1;
	else
		return n * fact(n - 1);
}
int main() {
	int ret = fact(5);
	printf("%d", ret);
	printf("\n\n\n\n\n\n\n");
	return 0;
}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/302e87a0f9a540f1a771531997a76175.png#pic_center)

### 递归思想

>只要解决了递归思想，就很容易写出程序。例如汉诺塔，移走n个次数为f(n),移走n-1个次数为f(n-1),两者有什么关系呢，显然f(n)=2f(n-1)+1,这样就很容易写出递归的程序。

### 递归思想非递归写法

> ❗❗❗❗❗通过递归函数来写程序虽然很简单，很简明，很利于人来理解，但是计算机很不愿意来执行，同样的思想用递归和循环计算机执行时间远远不同

>⭐️习题链接直达：🔑[汉诺塔问题](https://leetcode-cn.com/problems/climbing-stairs/)⭐️



```c
int climbStairs(int n){
    int predata=1;
    int nowdata=2;
    int nextdata=0;
    if(n==1){
        return 1;
    }
    else{
        while(n-2){
            nextdata=nowdata+predata;
            predata=nowdata;
            nowdata=nextdata;
            --n;
        }
    }
    return nowdata;
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/b2c8ea64406e4136b8c0cd794af1112f.png#pic_center)



# 指针

## 什么是指针
地址指向了一个确定的内存空间，所以地址形参的被称为指针

例如创建int a=10；必有地址0x0012ff40-43地址是随机编的，指针指向0x0012ff40，指向第一个地址

指针是一个变量，用来存放地址
## 指针的类型
指针的类型决定了指针解引用时一次访问几个字节

也决定加减整数的时候的步长(跳过几个字节)

char*指向一个字节

int*指向四个字节

## 野指针

成因1：
>指针未初始化



```c
#include<stdio.h>
int main() {
  int* p;//未初始化默认为随机值
  *p = 20;
  return 0;
}
```
成因2：
>指针越界访问

例如，建立一个10的数组，指针指向了第11个位置

或者指针指向的空间已被释放

## 指针和数组

![在这里插入图片描述](https://img-blog.csdnimg.cn/277df1ba4a4649c8b8226a590b2f5eb0.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dhbmdfZm0=,size_16,color_FFFFFF,t_70#pic_center)


由此可见：==数组名表示的是数组首元素的地址。==

有例外:==在sizeof中处理不是首元素地址，而是整个数组的大小==；
需要注意的是：

   >&arr不是首元素地址，而是整个数组的值

## 指针运算

### 指针加减整数

```c
#include<stdio.h>
#define MAX 5
int main() {
    float values[MAX];
    float* vp;
    for (vp = &values[0]; vp < &values[MAX];) {
        *vp++ = 0;
    }
    for (vp = &values[0]; vp < &values[MAX]; vp++)
        printf("%d ", *vp);
    return 0;
}
//初始vp指向数组第一个元素，赋值为0后自增1，直到直到最后一个地址
//减减向前越界可能出差错
```
指针地址减减运算可能出错，我们一般不考虑减减运算。

### 指针减去指针

指针加指针，意味地址加地址，这好像没有意义

所以我们主要讨论的都是指针减去指针

```c
#include<stdio.h>
int main() {
  int arr[10] = { 1,2,3,4,5,6,7,8,9,0 };
  printf("%d", &arr[9] - &arr[0]);
  return 0;
}
//输出的值是9
//指针减指针，得到的值是指针和指针的元素个数
//注意:必须是两个指针同一个数组
#include<stdio.h>
int my_strlen(char* str) {
  char* p1 = str;
  while (*p1 != '\0')
    p1++;
  return p1 - str;
}
int main() {
  char str[] = "abcdefg";
  printf("%d", my_strlen(str));
  return 0;
}

```



## 二级指针

这里类推指针的概念，知道它是用来保存指针的地址。
```c
int main() {
  int a = 10;
  int* p1 = &a;//以及指针
  int** p2 = &p1;//二级指针，因为一级指针也有地址，理论上可以无线套娃
}
```

## 指针的进阶

### 字符指针

```c
#include<stdio.h>
int main() {
  char ch = 'w';
  char* p1 = &ch;
  char* p2 = "hello word";//将常量字符串的第一个值地址赋给指针
  printf("%c\n", *(p2 + 1));//打印字符e
  printf("%s\n", p2);//打印字符串hello world
  return 0;
}

```

上面的代码char* p2 = "hello word";

真的将字符串存到p2里面了吗？

不不不，其实只存了首字符地址进去
字符指针只能指向一个字符的地址。
但是可以通过首元素的地址打印整个字符串，这和我们在打印字符串只需要输入数组名是一致的。

```c
#include <stdio.h>
int main()
{
  char str1[] = "hello bit.";
  char str2[] = "hello bit.";
  const char* str3 = "hello bit.";
  const char* str4 = "hello bit.";
  if (str1 == str2)
    printf("str1 and str2 are same\n");
  else
    printf("str1 and str2 are not same\n");
  if (str3 == str4)
    printf("str3 and str4 are same\n");
  else
    printf("str3 and str4 are not same\n");
  return 0;
}
```
![Snipaste_2021-10-07_18-21-12](https://gitee.com/wang-fuming/dawning/raw/master/202110071821865.png)


为什么呢?str1和str2是两个数组，数组的创立在两个独立的内存中存储，虽然内容相同，但没有关联。比较数组名即比较地址。可以通过修改str1的内容来判断str2的内容是否改变。

str3和str4指向的都是常量字符串，常量字符串不可修改，存储的方式就是两个指针指向同一个地址。

### 指针数组

>存放指针的数组
>它是一个数组，用来存放指针
>也就是说它的每个元素是一个指针。

int* parr[5];

[ ]的优先级高于\*，所以现有parr[5]，这是一个数组，然后与*结合形成一个存放地址的数组，叫做指针数组。

int* 整形指针数组，parr为数组名字，5为数组大小，能放5个指针

```c
#include<stdio.h>
int main() {
  int a = 10;
  int b = 20;
  int c = 30;
  int* arr[3] = { &a,&b,&c };
  for (int i = 0;i < 3; i++)
    printf("%d ", *(arr[i]));
  return 0;
}
```

### 数组指针

它是一个指针，用来存放数组

int (*parr)[10]  它是一个指针，指向一个数组，数组有10个整形元素

*先于parr结合形成指针，然后指向一个大小为10的数组，int 表明存储整形

```c
int main() {
  int arr[10] = { 0 };
  int* p = arr;//arr是数组首元素地址
  int (*parr)[10] = &arr;
  return 0;
}

```


int arr[5]  一个数组

int *arr1[10]  一个指针数组

int (*arr2)[10]   一个数组指针

int (*arr[10])[5] 是什么？

先看*arr[10] 由于[]的优先级高，所以它是一个数组

在看 int (*p)[5]这是一个数组指针，我们可以该指针指向的数组有5个元素

int (* arr[10])[5]就可以看做arr[10]是一个数组，每个元素是指向数组元素为5的指针。

## 数组传参和指针传参

### 一维数组传参

```c
#include <stdio.h>
void test(int arr[]){
}
void test(int arr[10]){
}
void test(int* arr){
}
void test2(int* arr[20]){
}
void test2(int** arr){
}
int main(){
  int arr[10] = { 0 };
  int* arr2[20] = { 0 };
  test(arr);
  test2(arr2);
  return 0;
}
```

### 二维数组传参

二维数组传参必须指明列数。
```c
void test(int arr[][5]){
}
void test(int arr[3][5]) {

}
void test(int(*arr)[5]) {

}
```

### 一级指针传参

```c
void print(int* p, int sz){
  int i = 0;
  for (i = 0; i < sz; i++)
    printf("%d ", *(p + i));
}
int main(){
  int arr[10] = { 1,2,3,4,5,6,7,8,9 };
  int* p = arr;
  int sz = sizeof(arr) / sizeof(arr[0]);
  print(p, sz);//一级指针p传参到函数print
  return 0;
}
```

### 二级指针传参

```c
#include <stdio.h>
void test(int** ptr)
{
  printf("num = %d\n", **ptr);
}
int main()
{
  int n = 10;
  int* p = &n;
  int** pp = &p;
  test(pp);
  test(&p);
  return 0;
}
```

## 函数指针

存放函数的地址

>意义在于我们有时候不一定能够拿到函数名，而是得到了函数的地址
>这时候可以用函数指针来调用

与前面数组不一样的是
>函数名和&函数名都是函数的地址

```c
#include <stdio.h>
void test()
{
  printf("hehe\n");
}
int main()
{
  printf("%p\n", test);
  printf("%p\n", &test);
  return 0;
}
```


```c
int add(int x, int y) {
  return x + y;
}
int (*p)(int,int)=add;
//可以类比数组指针
//由于函数指针的特殊性，在函数指针解引用时可以不加*号，也可以多加*号
ret=(*p)(1,2);
ret=(p)(1,2);
```

### 函数指针数组

将函数指针放到一个数组里面；
这就很简单了嘛
有了前面的基础，我们只需要把指针换成一个数组即可

```c
int (*parr1[10]])(int,int);
```

## 习题部分

### 习题1

```c
int main() {
	char arr[] = { 'a','b','c','d','e','f' };
	printf("%d\n", sizeof(arr));//6
	printf("%d\n", sizeof(arr + 0));//4/8
	printf("%d\n", sizeof(*arr));//1
	printf("%d\n", sizeof(arr[1]));//1
	printf("%d\n", sizeof(&arr));//4/8
	printf("%d\n", sizeof(&arr + 1));//4/8
	printf("%d\n", sizeof(&arr[0] + 1));//4/8
	//strlen函数输入地址，找到0为止
	printf("%d\n", strlen(arr));//随机值b
	printf("%d\n", strlen(arr + 0));//随机值b
	printf("%d\n", strlen(*arr));//错误
	printf("%d\n", strlen(arr[1]));//错误
	printf("%d\n", strlen(&arr));//随机值b
	printf("%d\n", strlen(&arr + 1));//随机值b-6
	printf("%d\n", strlen(&arr[0] + 1));//随机值b-1
	return 0;
}
```
>sizeof是一个操作符，strlen是C语言库函数，接受的是一个地址

在前面我们知道数组名代表首元素地址，但是有例外，例如sizeof和数组直接使用时，这时候数组名代表整个数组。
经过我们分析可以知道
>1. arr直接使用代表整个数组，sizeof(arr)的值是6；
>2. arr+0是一个地址，所以sizeof(arr+0)的值是4或8，具体答案取决32或64平台
>3. *arr是首元素a的引用，所以sizeof(*arr)的值是1；
>4. arr[0]也是首元素a，与上面相同，它的值也是1；
>5. &arr是一个地址，所以它的值是4或者8；
>6. &arr+1是一个地址，所以它的值是4或者8；
>7. &arr[0]+1也是一个地址，所以它的地址是4或者8；

具体答案是不是我们分析的那样，用VS2019编译器进行验证
![在这里插入图片描述](https://img-blog.csdnimg.cn/4a1fb2fc2a4241fd90c10aaeb6ba2e4a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
接下来分析strlen函数
我们知道<font color=#FF1493>strlen接受字符串地址，然后往后找到/0结束</font>
但是我们在题目中初始化时没有给'\0',这样就会造成他会一直往后走找到结束标志'\0'。

>1. arr是首元素地址，但是我们不知道结束的0在哪，所以长度未知，设为len
>2. arr+0也是首元素地址，未知结束标志在哪，长度未知，并且和上一个长度相同，也是len
>3. *arr是什么？它是首元素a，数值97，不是一个地址，所以会报错
>4. arr[1]是元素b，不是一个地址，也会报错
>5. &arr是一个地址，是整个元素地址，但是和首元素地址相同，所以它的值也是len
>6. &arr+1是一个地址，但是它不是第二个元素的地址，而是跳过了整个数组的地址，指向f后面一个元素地址，跳过了6个元素，所以它的值len-6
>7. &arr[0]+1是一个地址，这个才是指向了第二个元素地址，值是len-1
>
>![在这里插入图片描述](https://img-blog.csdnimg.cn/7289c4c8c9ee4c25ba67117343a2222e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
>让我们通过VS2019编译器进行验证
>![在这里插入图片描述](https://img-blog.csdnimg.cn/8c7ca727d1984c91ae506050bde8c3f8.png#pic_center)
>
>
>
>由于3，4两行代码会报错从而导致程序终止运行，我们将它屏蔽掉，最右边是运行结果，这与我们的分析是一致的。

###  习题2

```c
int main() {
	char arr[] = "abcdef";
	printf("%d\n", sizeof(arr));//7
	printf("%d\n", sizeof(arr + 0));//4/8
	printf("%d\n", sizeof(*arr));//1
	printf("%d\n", sizeof(arr[1]));//1
	printf("%d\n", sizeof(&arr));//4/8
	printf("%d\n", sizeof(&arr + 1));//4/8
	printf("%d\n", sizeof(&arr[0] + 1));//4/8
	printf("%d\n", strlen(arr));//6
	printf("%d\n", strlen(arr + 0));//6
	//printf("%d\n", strlen(*arr));//错误
	//printf("%d\n", strlen(arr[1]));//错误
	printf("%d\n", strlen(&arr));//6
	printf("%d\n", strlen(&arr + 1));//随机
	printf("%d\n", strlen(&arr[0] + 1));//5
}

```
这题和上面题只是多了一个结束的0，在结果上略有不同。
![](https://img-blog.csdnimg.cn/9d9b10258b4840859016b87c85fd5172.png#pic_center)

所以它包含7个元素，这和上面的多了一个'\0'
所以sizeof(arr)的值是7
strlen函数我们知道了结束的标志在哪里，所以可以轻松判断字符串长度
而&arr+1跳过了整个字符串，下一个'\0'是未知的，所以是随机值

###  习题3

```c
int main() {
	char* p = "abcdef";
	printf("%d\n", sizeof(p));//4/8
	printf("%d\n", sizeof(p + 1));//4/8
	printf("%d\n", sizeof(*p));//1
	printf("%d\n", sizeof(p[0]));//1
	printf("%d\n", sizeof(&p));//4/8
	printf("%d\n", sizeof(&p + 1));//4/8
	printf("%d\n", sizeof(&p[0] + 1));//4/8
	printf("%d\n", strlen(p));//6
	printf("%d\n", strlen(p + 1));//5
	//printf("%d\n", strlen(*p));
	//printf("%d\n", strlen(p[0]));
	printf("%d\n", strlen(&p));//随机值a
	printf("%d\n", strlen(&p + 1));//随机值b
	printf("%d\n", strlen(&p[0] + 1));//5
}
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/826828bf175949768f9e3ee0b98f7359.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
我们需要知道的是，这是一个常量字符串，一个cha* 的指针不可能包含整个字符串，它指向的是首元素a。也就是说*p\==a，p是首元素的地址。
我们知道sizeof(地址)的值是4或者8
p，p+1，&p，&p+1,&p[0]+1它们都是地址
*p和p[0]代表首元素a，所以所占空间是1
当首元素的地址传进strlen函数时，直到往后找到'\0'，由此我们可以判断strlen(p)\==6，strlen(p+1)==5;
这里需要注意的是，<font color=#DC143C>我们这里&p和上面一个题的&arr是两个概念，&p是地址的地址，指针p的地址，与原来字符串数组关系不大了。</font>

###  习题4

```c
int main(){
	int a[5] = { 1, 2, 3, 4, 5 };
	int* ptr1 = (int*)(&a + 1);
	printf("%d,%d", *(a + 1), *(ptr1 - 1));
	return 0;
}
```
>1.  元素名代表首元素地址，a+1代表第二个元素地址，解引用得到第二个元素的值
>2.    &a+1跳过整个数组，它的类型是int  ( * )[5]，这里强制类型转换为int*，&a+1代表跳过整个数组，指向a[5]（不存在）
>![在这里插入图片描述](https://img-blog.csdnimg.cn/63063caa4aa645b1bc401d2a074e4da3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

>我们分析出他的值是2，5
>
>![在这里插入图片描述](https://img-blog.csdnimg.cn/b9cedbc8a5a946bc9d44c473e8753ec5.png#pic_center)

###  习题5

```c
int main(){
	int a[4] = { 1, 2, 3, 4 };
	int* ptr1 = (int*)(&a + 1);
	int* ptr2 = (int*)((int)a + 1);
	printf("%x,%x", ptr1[-1], *ptr2);
	return 0;
}
```
>1. 这个分析和上面一题相同，==ptr[-1]等价于*(ptr-1)==
>2. 第二个问题需要考虑大小端的问题，在博主vs2019机器中是小端存储，int占有4个字节

![在这里插入图片描述](https://img-blog.csdnimg.cn/48742c1c25804319aac0404bad07c334.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
>最开始a指向01，a+1就会指向02，但是通过强制类型转换后(int)a+1地址就是01后面00的地址，在强制类型转换为指针就指向了00 00 00 02
>![在这里插入图片描述](https://img-blog.csdnimg.cn/64904a64bf3c4ca89fbaf97c99b59c64.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
>最后的到的值就是20000000
>![在这里插入图片描述](https://img-blog.csdnimg.cn/edd6838021114182a0f1674c5733c4e8.png#pic_center)
>
>![在这里插入图片描述](https://img-blog.csdnimg.cn/d482d0b6af2d451c9bf29103cdbc1d04.png#pic_center)



###  习题6

```c
int main(){
	int a[3][2] = { (0, 1), (2, 3), (4, 5) };
	int* p;
	p = a[0];
	printf("%d", p[0]);
	return 0;
}
```
>1. 对于二维数组我们可以看成3个元素，它的每一行是一个元素，p=a[0]就是指向了第一行，p=*a，p[0]就是 a[0] [0],我们知道他是第一行第一个元素。
>2. 但是需要注意的是，我们数组里面有逗号表达式，里面存的元素是arr[3] [2]={1,3,5},第一个元素就是1



### 习题7

```c
int main(){
	int a[5][5];
	int(*p)[4];//这个一个指针，指向有四个元素的数组
	p = a;//a有五个元素，强行将p指向a，下面有警告
	printf("%p,%d\n", &p[4][2] - &a[4][2], &p[4][2] - &a[4][2]);
	return 0;
}
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/ff14f2ecb53e4f4d9d5d4b1af3f69274.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
int (*p)[4]是一个指针，指向一个4个元素的数组，但是我们的a有5个元素，这里也可以指向。
我们知道a[4] [2]元素是23，而p[4] [2]是19，他们中间差了4个元素
按照十进制输出就是-4，十六进制输出就是FFFFFFFC

### 习题8

```c
int main(){
	char* a[] = { "work","at","alibaba" };
	char** pa = a;
	pa++;
	printf("%s\n", *pa);
	return 0;
}
```
>1. 指针数组，数组里面存放的是指针
>2. pa指向数组第一个元素，自增运算后指向第二个元素
>3. 解引用就是第二个指针的地址

![在这里插入图片描述](https://img-blog.csdnimg.cn/a2b3886e24864af089ed0416e83e02cb.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/068f902df5aa46a68eac623f42c1ee2c.png#pic_center)

###  习题9

```c
int main(){
	char* c[] = { "ENTER","NEW","POINT","FIRST" };
	char** cp[] = { c + 3,c + 2,c + 1,c };
	char*** cpp = cp;
	printf("%s\n", **++cpp);//point
	printf("%s\n", *-- * ++cpp + 3);//er
	printf("%s\n", *cpp[-2] + 3);//st
	printf("%s\n", cpp[-1][-1] + 1);//ew
	return 0;
}
```
>1. char* c[]是一个指针数组，里面存放的是指针
>2. char** cp[]是一个指针数组，里面存放的是上一个指针的地址
>3. char*** cpp指向cp数组第一个元素
>4. 自增运算会改变指针的指向位置，从而会对后面的结果造成影响
>5. ++优先级别高，cpp指向cp数组第二个元素，解引用一次得到c+2的值，再解引用得到POINT的指针地址
>6. ++运算后指向cp第三个元素，解引用得到c+1，自减运算后得到c，此时cp[]={c+3,c+2,c,c},解引用得到ENTER指针地址，+3指向ENTER字符串中E的地址
>7.  *cpp[-2]等价于*(*(cpp-2));cpp-2指向c+3，解引用得到c+3的值，再次解引用得到FIRST指针地址，+3指向S
>8. 价于*(*(cpp-1)-1),cpp-1指向c+2，解引用猴得到c+2空间，减去1变成c+1，解引用得到NEW指针地址，+1指向E
>9. 本题建议画图分析

# 常见库函数

## 字符串函数

### strlen

求字符串长度函数是我们经常使用的函数，这里不再赘述，下面提供三种方法以供参考

```c
size_t my_strlen_1(char* s) {
	size_t count = 0;
	while (*s++) {
		++count;
	}
	return count;
}
size_t my_strlen_2(char*s){
	if (*s == 0)
		return 0;
	else
		return 1 + my_strlen_2(++s);
}
size_t my_strlen_3(char* s) {
	char* p = s;
	while (*p++) {

	}
	return p - s-1;
}
```

>1. 常见的有一个非'\0'加一法，最后返回一个值
>2. 不用创建临时变量的函数迭代法
>3. 指针相减法

### strcmp

strcmp函数是string compare(字符串比较)的缩写，用于比较两个字符串并根据比较结果返回整数。
基本形式为strcmp(str1,str2)

>1. 若str1=str2，则返回零；
>2. 若str1<str2，则返回负数；
>3. 若str1>str2，则返回正数。

```c
int my_strcmp(const char* s1, const char* s2) {
	assert(s1 && s2);
	while (*s1 == *s2) {
		if (*s1 == 0)
			return 0;
		++s1;
		++s2;
	}
	return *s1 - *s2;
}
```

### strncmp

这个函数与strcmp的区别在于strcmp比较完整个字符串，而strncmp只比较前n个字符

```c
int myStrncmp(const char* s1, const char* s2, size_t n) {
	if (n == 0)
		return 0;
	size_t i = 0;
	while (*(s1 + i) && *(s2 + i)&&i<n-1) {
		if (*(s1 + i) != *(s2 + i))
			break;
		++i;
	}
	return *(s1 + i) - *(s2 + i);
}
```

>1. 要注意记录比较的个数
>2. 要注意如果两个字符串提前结束

### strcat

字符串追加函数

>1. 把src所指向的字符串（包括“\0”）复制到dest所指向的字符串后面（删除* dest原来末尾的“\0”）。要保证* dest足够长，以容纳被复制进来的*src。*src中原有的字符不变。返回指向dest的指针。
>2. 需要注意的是，dest数组要有足够长来存放追加内容。

```c
char* my_strcat(char* dest, const char* src) {
	assert(dest && src);
	char* p = dest;
	while (*dest) {
		++dest;
	}
	while ((*dest++ = *src++)) {
		;
	}
	return p;
}
```

### strncat

```c
char* my_strcat(char* dest, const char* src,size_t n) {
	assert(dest && src);
	char* p = dest;
	size_t i = 0;
	while (*dest) {
		++dest;
	}
	while (i<n&&*src) {
		*dest++=*src++;
		++i;
	}
	*dest = '\0';
	return p;
}
```

>1. 记录追加个数
>2. 注意src提前结束

### strcpy

strcpy把含有'\0'结束符的字符串复制到另一个地址空间，返回值的类型为char*。

```c
char* my_strcpy(char* dest, const char* src) {
	assert(dest&&src);
	char* p = dest;
	while (*dest++ = *src++) {

	}
	return p;
}
```

### strncpy

复制前n个字符

```c
char* myStrncpy(char* dest, const char* src, size_t n) {
	assert(dest && src);
	size_t i = 0;
	while (*(src + i) && i < n) {
		*(dest + i) = *(src + i);
		++i;
	}
	*(dest + i) = '\0';
	return dest;
}
```

>1. 要记录复制字符数
>2. 要注意原字符提前结束

### strstr

strstr(str1,str2) 函数用于判断字符串str2是否是str1的子串。如果是，则该函数返回 str1字符串从 str2第一次出现的位置开始到 str1结尾的字符串；否则，返回NULL。
在我们的设定中如果不是字串就返回-1；

```c
int strStr(char* haystack, char* needle) {
    int n = strlen(haystack);
    int m = strlen(needle);
    for (int i = 0; i + m <= n; i++) {
        int flag = 1;
        for (int j = 0; j < m; j++) {
            if (haystack[i + j] != needle[j]) {
                flag = 0;
                break;
            }
        }
        if (flag) {
            return i;
        }
    }
    return -1;
}
```

> ⭐️点击直达🔑[力扣—模拟strStr](https://leetcode-cn.com/problems/implement-strstr/)⭐️

## 内存操作函数

### memcpy

memcpy指的是C和C++使用的内存拷贝函数，函数原型为

```c
void *memcpy(void *dest, void *src, size_t count)；
```

函数的功能是从源内存地址的起始位置开始拷贝若干个字节到目标内存地址中，即从源src中拷贝n个字节到目标dest中。
我们需要注意的是:

>1. src和dest所指的内存区域可能重叠，但是如果source和destin所指的内存区域重叠,那么这个函数并不能够确保source所在重叠区域在拷贝之前不被覆盖。而使用memmove可以用来处理重叠区域。也就是说需要拷贝与粘贴的内存空间不能重合
>2. memcpy函数会覆盖原先内存内容
>3. src和dest都不一定是数组，任意的可读写的空间均可。

有了上面的信息，我们可以实现memcpy函数

```c
void* my_memcpy(void* dest, const void* src, size_t n) {
    while (n--) {
        *((char*)dest + n) = *((char*)src + n);
    }
    return dest;//                                         (1)
}
```

代码解释：

>（1）采用了从后向前拷贝，并没有改变dest指针，所以可以直接返回dest指针；如果从前向后拷贝，可能需要改变dest指针，这时候我们需要提前创建一个变量存储dest然后用来返回


上文介绍了字符串拷贝函数strcpy好像与memcpy很相似，下面分它们的区别
strcpy和memcpy主要有以下3方面的区别。

>1. 复制的内容不同。strcpy只能复制字符串，而memcpy可以复制任意内容，例如字符数组、整型、结构体、类等。
>2. 复制的方法不同。strcpy不需要指定长度，它遇到被复制字符的串结束符"\0"才结束，所以容易溢出。memcpy则是根据其第3个参数决定复制的长度。
>3. 用途不同。通常在复制字符串时用strcpy，而需要复制其他类型数据时则一般用memcpy。

### memmove

上面函数我们知道了memcpy的拷贝不能用于重叠空间，原因是覆盖后内容消失，memmove就是来解决这个问题的，那要怎么解决呢？
很简单，判断重叠情况，讨论拷贝方式从前往后还是从后往前，从何规避从重叠内存造成的影响
简而言之，重叠空间先使用后覆盖
下面我们将要对情况进行讨论
![在这里插入图片描述](https://img-blog.csdnimg.cn/e828709e0641442d9f66fcaf0d94d0ac.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

>情况1
>我们看到两者没有任何重叠空间，所以从前拷贝还是从后拷贝都可以

>情况2
>我们看到src前部分被覆盖，若是从前拷贝的话即使被覆盖也不会有影响，所以它只能从前拷贝

>情况3
>根据情况2分析，我们只能从后拷贝

>情况4
>可以从前或者从后拷贝

我们可以将情况2或者情况3归为一类，其他一类
我选择将情况3归为一类，它对应的条件是

```c
      dest>=src&&(char*)dest<(char*)src+count;
```

函数内部操作

```c
void* my_memmove(void* dest, const void* src, size_t count) {
    assert(dest && src);
    char* p = dest;
    if (dest >= src && (char*)dest <= (char*)src + count) {
        while (count--){
            *((char*)dest + count) = *((char*)src + count); //（1）
        }
    }
    else {
        while (count--) {
            *(char*)dest = *(char*)src;
            dest = (char*)dest + 1;	
            src = (char*)src + 1;
        }
    }//(2)
    return p;
}
```

代码解释

>(1) 从后向前拷贝
>(2) 从前向后拷贝





# 动态内存

在C语言中我们开辟内存的方式是

```c
int data=10;
int arr[10]={0};
```

对于这种开辟方式

>1. 空间开辟大小是固定的。
>2. 数组在申明的时候，必须指定数组的长度，它所需要的内存在编译时分配。

但是，很多时候我们需要的空间大小在程序运行的时候才能知道，那数组的编译时开辟空间的方式就不能满足了。 这时候就只能试试动态存开辟了。

##  动态内存函数分析

下面将分析一些C语言库中动态内存开辟以及释放的函数，这些函数有malloc，free，calloc，realloc；

### malloc

函数原型是

```c
void* malloc(size_t count);
```

函数作用是

>1. 如果开辟成功，则返回一个指向开辟好空间的指针。
>2. 如果开辟失败，则返回一个NULL指针，因此malloc的返回值一定要做检查。
>3. 返回值的类型是void* ，所以malloc函数并不知道开辟空间的类型，具体在使用的时候使用者自己来决定。
>4. 如果参数size 为0，malloc的行为是标准是未定义的，取决于编译器。

使用实例

```c
	int* ptr1 = (int*)malloc(10 * sizeof(int));
	int* ptr2 = (char*)malloc(10 * sizeof(char));
```

我们知道这是开辟字节数，例如第一个就是开辟10个整型空间（40 Byte），第二个就是开辟10个字符型空间（10 Byte）。
但是，函数的返回型是空指针类型，这就需要强制类型转换。

### free

函数原型是

```c
void free (void* ptr);
```

函数作用是

>1. free函数用来释放动态开辟的内存。
>2. 如果参数ptr 指向的空间不是动态开辟的，那free函数的行为是未定义的。
>3. 如果参数ptr 是NULL指针，则函数什么事都不做。

⭐️⭐️⭐️⭐️⭐️
需要注意的是

>1. free释放p的内存，但还能找到p的地址。
>2. free释放的空间必须是动态内存开辟的。

下面对上面两个函数进行实战使用
如下代码，将采用调试的方式进行分析

```c
int main() {
	int n = 0;
	scanf("%d", &n);
	int* arr = (int*)malloc(n * sizeof(int));         //(1)
	if (arr) {
		for (int i = 0; i < n; ++i) {
			*(arr + i) = i;
		}
	}
	else {
		printf("动态内存开辟失败");
	}                                               //(2)
	for (int i = 0; i < n; ++i)
		printf("%d ", *(arr + i));
	free(arr);                                      //(3)
	arr = NULL;                                     //(4)
	return 0;
}
```

代码分析

> (1)开辟n个整型空间，相当于arr[n]，但在C语言中是不能这样实现的，可以看见数组里面的数都还是随机的

![在这里插入图片描述](https://img-blog.csdnimg.cn/6bd269b484a74d3585d866ffdb7d39bf.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

> (2) 初始化赋值
>
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/b62dac732ad347c48281a3fc3cf9ae2e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
> (3) 释放空间，可以看见数值都回归随机值。


![在这里插入图片描述](https://img-blog.csdnimg.cn/f723dbcc3525453ebdc1856627f22ae0.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

> (4) 虽然数组都回归了，但是我们仍然可以找到地址，我们可以看见arr的地址是没有变化的，经过arr=NULL就找不到了。

![在这里插入图片描述](https://img-blog.csdnimg.cn/5fc04be8c93443bcbc5632dc9a67bf4b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### calloc

函数的原型是

```c
void* calloc(size_t num,size_t size);
```

函数的作用是

>1. num是元素个数，size是一个元素所占字节数;
>2. 开辟一个数组，每个元素初始化为0;

通过上面的描述，我们知道它带有初始化作用
在上文描述的

```c
int* ptr=(int*)malloc(10*sizeof(int))
```

起始可以看作

```c
int* ptr=(int*)malloc(num*size);
```

与malloc相比，calloc多了一个初始化为0的效果。
说了这么多，直接看实例

![在这里插入图片描述](https://img-blog.csdnimg.cn/e3f8dad42e4f4dc298bc2c3e19d1b1a3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### reaclloc

函数原型是

```c
void* realloc(void* memblock,size_t size);
```

函数的功能是

>1. memblock是要调整的内存地址
>2. size 调整之后新大小
>3. 返回值为调整之后的内存起始位置。
>4. 这个函数调整原内存空间大小的基础上，还会将原来内存中的数据移动到新的空间。

⭐️⭐️⭐️⭐️⭐️
我们需要注意的是

>1. 调整内存大小不一定是在原地址上追加，如果原空间后面足够大，直接在后面追加，如果没有足够空间，就开辟新的空间，并将内容拷贝到新的空间
>2. 函数也会开辟内存失败，不能使用memblock=realloc(memblock,size)
>     如果开辟失败反而会将原先的地址丢失

实例使用

```c
int main(){	int* ptr = malloc(100);	if (ptr != NULL){	}	else{		exit(EXIT_FAILURE);	}	int* p = NULL;//建立临时空间存放地址，避免开辟失败导致原地址丢失	p = realloc(ptr, 1000);	if (p != NULL){		ptr = p;	}	free(ptr);	return 0;}
```

### 内存开辟失败情况

在上文中我们说到了可能存在内存开辟失败的情况，那究竟是什么情况呢？
这里提供一种很容易想到的情况------开辟空间过大导致失败
对于32位机器，他的内存最大是4G，知道我们开辟的内存大于4G，那必然就会开辟失败。
下面提供开辟空间过大导致失败的运行截图。

![在这里插入图片描述](https://img-blog.csdnimg.cn/1e3e879c394d487e88b0d49a60986ae2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

## 常见内存错误

### 对NULL指针的解引用操作

```c
void test(){
    int* p = (int*)malloc(INT_MAX*sizeof(int));
    *p = 20;//如果p的值是NULL，就会有问题
    free(p);
}
```

### 越界访问

```c
void test(){
    int i = 0;
    int* p = (int*)malloc(10 * sizeof(int));
    if (NULL == p){	
        exit(EXIT_FAILURE);
    }
    for (i = 0; i <= 10; i++){
        *(p + i) = i;//当i是10的时候越界访问	
    }
    free(p);
}
```

### 对非动态开辟内存使用free释放

```c
void test(){
    int a = 10;
    int* p = &a;
    free(p);//ok?
}
```

### 使用free释放一块动态开辟内存的一部分

```c
void test() {
    int* p = (int*)malloc(100);
    p++;	
    free(p);//p不再指向动态内存的起始位置
}
```

### 对同一块动态内存多次释放

```c
void test(){
    int* p = (int*)malloc(100);
    free(p);
    free(p);//重复释放
}
```

### 内存泄漏

```c
void test(){
    int* p = (int*)malloc(100);
    if (NULL != p){	
        *p = 20;	
    }
}
int main(){	
    test();	
    while (1);
}
```

## 动态内存错误笔试题分析

### 笔试题1

以下代码执行效果

```c
void GetMemory(char* p){
    p = (char*)malloc(100);
}
void Test(){
    char* str = NULL;
    GetMemory(str);
    strcpy(str, "hello world");
    printf("%s",str);
}
int main() {
    Test();
    return 0;
}
```

>执行后：程序会崩溃

分析如下：
我们经过调试发现再执行`GetMemory(str);` 后str的地址还是等于NULL，那这是为什么呢？
那肯定是这个函数处理不当？
突然想起函数传递参数--传值调用，如下

```c
void change(int a) {
    a = a + 1;
}
int main() {
    int a = 0;
    change(a);
    return 0;
}
```

在执行完后看似a的值加一，但是我们发现它还是0
对于这种情况也是一样，传值调用并不能改变值，要想达到目的需要进行传址调用。

```c
void GetMemory(char** p){
    *p = (char*)malloc(100);
}
void Test(){
    char* str = NULL;
    GetMemory(&str);
    strcpy(str, "hello world");
    printf(str);
}
int main() {
    Test();
    return 0;
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/d31fe4475bb54b86a66275049c2f5081.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### 笔试题2

```c
char* GetMemory(void){
    char p[] = "hello world";
    return p;
}
void Test(void){
    char* str = NULL;
    str = GetMemory();
    printf(str);
}
int main() {
    Test();
    return 0;
}
```

>输出随机值

str接受了p的地址，但是在GetMemory函数结束后销毁，p函数中内存内容也被随机化，虽然拿到了地址，但是内容不再是hello world
这种情况对应野指针，指针指向的内容已被释放，对其解引用就会出错

```c
int* change() {
    int n = 10;
    return &n;
}int main() {
    int* p = change();
    printf(" \n");
    printf("%d", *p);
    return 0;
}
```

> 输出的不是我们想要的10

![在这里插入图片描述](https://img-blog.csdnimg.cn/38fb69b141fb4e0daeb18d6d289f67d3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### 笔试题3

```c
void GetMemory(char** p, int num){
    *p = (char*)malloc(num);
}
void Test(void){
    char* str = NULL;
    GetMemory(&str, 100);
    strcpy(str, "hello");
    printf(str);
}
int main() {
    Test();
    return 0;
}
```

这道题就是笔试题1的正确写法，输出

>hello

### 笔试题4

```c
void Test(void){
    char* str = (char*)malloc(100);
    strcpy(str, "hello");
    free(str);
    if (str != NULL){
        strcpy(str, "world");
        printf(str);
    }
}
int main() {
    Test();
    return 0;
}
```

>输出hello，word

分析：
        &#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;对于第一个输出hello很容易判断，在释放后str的内容虽然丢失了，但是str的地址还在，不为空，所以world被拷贝进去。
        ![在这里插入图片描述](https://img-blog.csdnimg.cn/c5e7525eabc84c0abdeb7acb261221f6.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5b6A5piO,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
这也是前文介绍在释放后需要把指针指向NULL

自定义类型与内存对齐

# 结构体

结构是一些值的集合，这些值称为成员变量。结构的每个成员可以是不同类型的变量。

## 结构体的声明

```c
struct tag{
	member_list;
}variable_list;
```

例如我们描述一个学生

```c
struct Stu
{
	char name[20];//名字
	int age;//年龄
	char sex[5];//性别
	char id[20];//学号
};//分号不能丢
```

结构体是特殊声明

## 结构体的自引用

在结构中包含一个类型为该结构本身的成员是否可以呢？

```c
struct Node{
	int data;
	struct Node* next;
};
```

## 结构体变量的定义和初始化

```c
struct Point{
	int x;
	int y;
}p1; //声明类型的同时定义变量p1

struct Point p2; //定义结构体变量p2

//初始化：定义变量的同时赋初值。
struct Point p3 = { x, y };

struct Stu {
	char name[15];//名字
	int age; //年龄
};
struct Stu s = { "zhangsan", 20 };//初始化

struct Node{
	int data;
	struct Point p;
	struct Node* next;
}n1 = { 10, {4,5}, NULL }; //结构体嵌套初始化

struct Node n2 = { 20, {5, 6}, NULL };//结构体嵌套初始化
```



## 结构体的内存对齐

我们已经掌握了结构体的基本使用了。

现在我们深入讨论一个问题：计算结构体的大小。

这也是一个特别热门的考点： 结构体内存对齐

要计算内存对齐那肯定要知道怎么计算，下面给出计算规则

> 1. 第一个成员在与结构体变量偏移量为0的地址处。
> 2. 其他成员变量要对齐到某个数字（对齐数）的整数倍的地址处。
>    1. 对齐数 = 编译器默认的一个对齐数 与 该成员大小的较小值。
>    2. VS中默认的值为8,Linux中的默认值为4
> 3. 结构体总大小为最大对齐数（每个成员变量都有一个对齐数）的整数倍。
> 4. 如果嵌套了结构体的情况，嵌套的结构体对齐到自己的最大对齐数的整数倍处，结构体的整体大小就是所有最大对齐数（含嵌套结构体的对齐数）的整数倍。

下面给出一些例题，博主测试机器为VS2019

```c
int main() {
	struct S1{
		char c1;
		int i;
		char c2;
	};
	printf("%d\n", sizeof(struct S1));
	return 0;
}
```

根据2

| 变量 | 成员大小 | 默认对齐数 | 对齐数 |
| ---- | -------- | ---------- | ------ |
| c1   | 1        | 8          | 1      |
| i    | 4        | 8          | 4      |
| c2   | 1        | 8          | 1      |

第一个变量占据下标0的位置（第一条）

第二个变量占据下标4，5，6，7的位置（4为4的倍数）

第三个变量占据下标为8的位置（8为1的倍数）

那么大小是9？

不不不，大小还要说最大对齐数的倍数，4的倍数为12。

结果是12

![Snipaste_2021-10-07_18-26-34](https://gitee.com/wang-fuming/dawning/raw/master/202110071826009.png)

```c
int main() {
	struct S2
	{
		char c1;
		char c2;
		int i;
	};
	printf("%d\n", sizeof(struct S2));
	return 0;
}
```

| 变量 | 成员大小 | 默认对齐数 | 对齐数 |
| ---- | -------- | ---------- | ------ |
| c1   | 1        | 8          | 1      |
| c2   | 1        | 8          | 1      |
| i    | 4        | 8          | 4      |

第一个占据下标为0的位置

第二个占据下标为1的位置

第三个占据下标为4，5，6，7的位置

计算大小是8，恰好满足是最大对齐数4的倍数，结果就是8

![Snipaste_2021-10-07_18-27-19](https://gitee.com/wang-fuming/dawning/raw/master/202110071827288.png)

```c
int main() {
	struct S3{
		double d;
		char c;
		int i;
	};
	printf("%d\n", sizeof(struct S3));
	return 0;
}
```

| 变量 | 成员大小 | 默认对齐数 | 对齐数 |
| ---- | -------- | ---------- | ------ |
| d    | 8        | 8          | 8      |
| c    | 1        | 8          | 1      |
| i    | 4        | 8          | 4      |

第一个成员要占据8个位置，也就是0-7

第二个成员要占据8

第三个成员要占据12，13，14，15

计算大小是16，满足8的倍数

![](https://gitee.com/wang-fuming/dawning/raw/master/202110071828033.png)

```c
int main() {
	struct S3 {
		double d;
		char c;
		int i;
	};
	struct S4
	{
		char c1;
		struct S3 s3;
		double d;
	};
	printf("%d\n", sizeof(struct S4));
}
```

| 变量 | 成员大小 | 默认对齐数 | 对齐数 |
| ---- | -------- | ---------- | ------ |
| c1   | 1        | 8          | 1      |
| s3   | 16       |            | 8      |
| d    | 8        | 8          | 8      |

第一个变量占据0的位置

第二个变量占据16个位置，也就是8-23

第三个变量占据8个位置，也就是24-31

计算大小为32，满足8的倍数

![](https://gitee.com/wang-fuming/dawning/raw/master/202110071829130.png)



为什么存在内存对齐?
大部分的参考资料都是如是说的：

1. 平台原因(移植原因)： 不是所有的硬件平台都能访问任意地址上的任意数据的；某些硬件平台只能在某些地址
   处取某些特定类型的数据，否则抛出硬件异常。
2. 性能原因： 数据结构(尤其是栈)应该尽可能地在自然边界上对齐。 原因在于，为了访问未对齐的内存，处理器
   需要作两次内存访问；而对齐的内存访问仅需要一次访问。

总体来说：

> 结构体的内存对齐是拿空间来换取时间的做法。

那在设计结构体的时候，我们既要满足对齐，又要节省空间，如何做到：

> 让占用空间小的成员尽量集中在一起。

### 修改默认对齐数

不讨论

## 结构体传参

```c
struct S{
    int data[1000];
    int num;
};
struct S s = { {1,2,3,4}, 1000 };//结构体传参
void print1(struct S s){
    printf("%d\n", s.num);
}//结构体地址传参
void print2(struct S* ps){
    printf("%d\n", ps->num);
}
int main(){
    print1(s); //传结构体
    print2(&s); //传地址
    return 0;
}
```

上面的print1 和print2 函数哪个好些？
答案是：首选print2函数。 原因：

> 函数传参的时候，参数是需要压栈，会有时间和空间上的系统开销。
> 如果传递一个结构体对象的时候，结构体过大，参数压栈的的系统开销比较大，所以会导致性能的下降。

结论： 结构体传参的时候，要传结构体的地址。

# 位段

## 什么是位段

位段的声明和结构是类似的，有两个不同：

> 1. 位段的成员必须是int、unsigned int 或signed int 。
> 2. 位段的成员名后边有一个冒号和一个数字。

```c
struct A{	int _a : 2;	int _b : 5;	int _c : 10;	int _d : 30;};
```

## 位段的内存分配

位段的内存分配

>1. 位段的成员可以是int unsigned int signed int 或者是char （属于整形家族）类型
>2. 位段的空间上是按照需要以4个字节（ int ）或者1个字节（ char ）的方式来开辟的。
>3. 位段涉及很多不确定因素，位段是不跨平台的，注重可移植的程序应该避免使用位段。

位段的跨平台问题

> 1. int 位段被当成有符号数还是无符号数是不确定的。
> 2. 位段中最大位的数目不能确定。（16位机器最大16，32位机器最大32，写成27，在16位机器会出问题。
> 3. 位段中的成员在内存中从左向右分配，还是从右向左分配标准尚未定义。
> 4. 当一个结构包含两个位段，第二个位段成员比较大，无法容纳于第一个位段剩余的位时，是舍弃剩余的位
>    还是利用，这是不确定的。



总结：跟结构相比，位段可以达到同样的效果，但是可以很好的节省空间，但是有跨平台的问题存在。

## 位段的应用



# 枚举

## 什么是枚举

枚举顾名思义就是一一列举。
把可能的取值一一列举。
比如我们现实生活中：

> 一周的星期一到星期日是有限的7天，可以一一列举。
> 性别有：男、女、保密，也可以一一列举。
> 月份有12个月，也可以一一列举
> 颜色也可以一一列举。

## 枚举类型的定义

```c
enum Day{
    Mon,
    Tues,
    Wed,
    Thur,
    Fri,
    Sat,
    Sun
};
enum Sex {
    MALE,
    FEMALE,
    SECRET
};
enum Color{
    RED,
    GREEN,
    BLUE
};
```

以上定义的`enum Day ， enum Sex ， enum Color` 都是枚举类型。 {}中的内容是枚举类型的可能取值，也叫枚举常
量。
这些可能取值都是有值的，默认从0开始，一次递增1，当然在定义的时候也可以赋初值

```c
enum Color{	
    RED = 1,
    GREEN = 2,
    BLUE = 4
};
```

我们可以使用#define 定义常量，为什么非要使用枚举？ 枚举的优点：

1. 增加代码的可读性和可维护性
2. 和#define定义的标识符比较枚举有类型检查，更加严谨。
3. 防止了命名污染（封装）
4. 便于调试
5. 使用方便，一次可以定义多个常量

# 联合（共用体）

联合也是一种特殊的自定义类型 这种类型定义的变量也包含一系列的成员，特征是这些成员公用同一块空间（所以联合也叫共用体）。

```c
//联合类型的声明
union Un{
    char c;
    int i;
};
//联合变量的定义
union Un un;
//计算连个变量的大小
printf("%d\n", sizeof(un));
```

##  联合的特点

联合的成员是共用同一块内存空间的，这样一个联合变量的大小，至少是最大成员的大小（因为联合至少得有能力保存最大的那个成员）。

## 联合大小的计算

联合大小的计算

> 1. 联合的大小至少是最大成员的大小。
> 2. > 当最大成员大小不是最大对齐数的整数倍的时候，就要对齐到最大对齐数的整数倍。

```c
int main() {
    union Un1{
        char c[5];
        int i;
    };
    union Un2{
        short c[7];
        int i;
    };	//下面输出的结果是什么？
    printf("%d\n", sizeof(union Un1));
    printf("%d\n", sizeof(union Un2));
    return 0;
}
```

![Snipaste_2021-10-07_18-30-03](https://gitee.com/wang-fuming/dawning/raw/master/202110071830065.png)

程序环境和预处理

# 程序的翻译环境和执行环境



1. 翻译环境，在这个环境中源代码被转换为可执行的机器指令。
2. 执行环境，它用于实际执行代码.



## 编译

### 翻译环境

1. 组成一个程序的每个源文件通过编译过程分别转换成目标代码（object code）
2. 每个目标文件由链接器（linker）捆绑在一起，形成一个单一而完整的可执行程序。
3. 链接器同时也会引入标准C函数库中任何被该程序所用到的函数，而且它可以搜索程序员个人的程序库，将其需要的函数也链接到程序中。

### 运行环境

1. 程序必须载入内存中。在有操作系统的环境中：一般这个由操作系统完成。在独立的环境中，程序的载入必须由手工安排，也可能是通过可执行代码置入只读内存来完成。
2. 程序的执行便开始。接着便调用main函数。
3. 开始执行程序代码。这个时候程序将使用一个运行时堆栈（stack），存储函数的局部变量和返回地址。程序同
    时也可以使用静态（static）内存，存储于静态内存中的变量在程序的整个执行过程一直保留他们的值。
4. 终止程序。正常终止main函数；也有可能是意外终止。

## 预编译

头文件的包含

#define 定义符号的替换

删除注释

C语言源代码转换为汇编代码

1. 语法分析
2. 词法分析
3. 语义分析
4. 符号汇总

```c
__FILE__ //进行编译的源文件
__LINE__ //文件当前的行号
__DATE__ //文件被编译的日期
__TIME__ //文件被编译的时间
__STDC__ //如果编译器遵循ANSI C，其值为1，否则未定义
```

![](https://gitee.com/wang-fuming/dawning/raw/master/202110082038021.png)

**#define**

1. 可以定义符号
2. 可以定义宏

语法

```c
#define name stuff
```

```c
#define MAX 1000
#define reg register //为 register这个关键字，创建一个简短的名字
#define do_forever for(;;) //用更形象的符号来替换一种实现
#define CASE break;case //在写case语句的时候自动把 break写上。
// 如果定义的 stuff过长，可以分成几行写，除了最后一行外，每行的后面都加一个反斜杠(续行符)。
#define DEBUG_PRINT printf("file:%s\tline:%d\t \
date:%s\ttime:%s\n" ,\
__FILE__,__LINE__ , \
__DATE__,__TIME__ )
```

> 后面不加;，否则可能产生错误

**定义宏**

> #define 机制包括了一个规定，允许把参数替换到文本中，这种实现通常称为宏（macro）或定义宏（definemacro）。

声明方法

``#define name( parament-list ) stuff`` 其中的parament-list 是一个由逗号隔开的符号表，它们可能出现在stuff中

**#define的替换规则**

在程序中扩展#define定义符号和宏时，需要涉及几个步骤。
1. 在调用宏时，首先对参数进行检查，看看是否包含任何由#define定义的符号。如果是，它们首先被替换。
2. 替换文本随后被插入到程序中原来文本的位置。对于宏，参数名被他们的值替换。
3. 最后，再次对结果文件进行扫描，看看它是否包含任何由#define定义的符号。如果是，就重复上述处理过程。

注意：

1. 宏参数和#define 定义中可以出现其他#define定义的变量。但是对于宏，不能出现递归。
2. 当预处理器搜索#define定义的符号的时候，字符串常量的内容并不被搜索。

**#和##**

> 如何将参数插入字符串中？

##将两个字符合并

#### 宏和函数对比

那为什么不用函数来完成这个任务？ 原因有二：
1. 用于调用函数和从函数返回的代码可能比实际执行这个小型计算工作所需要的时间更多。所以宏比函数在程序
    的规模和速度方面更胜一筹。
2. 更为重要的是函数的参数必须声明为特定的类型。所以函数只能在类型合适的表达式上使用。反之这个宏怎可以适用于整形、长整型、浮点型等可以用于>来比较的类型。宏是类型无关的。

当然和宏相比函数也有劣势的地方：

1. 每次使用宏的时候，一份宏定义的代码将插入到程序中。除非宏比较短，否则可能大幅度增加程序的长度。
2. 宏是没法调试的。
3. 宏由于类型无关，也就不够严谨。
4. 宏可能会带来运算符优先级的问题，导致程容易出现错。

宏有时候可以做函数做不到的事情。比如：宏的参数可以出现类型，但是函数做不到。


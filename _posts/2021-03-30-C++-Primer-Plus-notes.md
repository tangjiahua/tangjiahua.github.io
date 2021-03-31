---
title: C++ Primer Plus 精华笔记
date: 2021-03-30 15:52:33 +0800
categories: [基础技术]
tags: [技术]
pin: true

toc: true
comments: true
Typora-root-url: ..
math: false
mermaid: true

#image:
#  src: 
#  alt: 

---

# 第2章：开始学习C++

让程序访问名称空间std的方法有如下4种：

1. using namespace std; 放在函数定义之前，让函数能够使用空间std的所有元素；
2. using namespace std;放在函数中；
3. 在特定函数使用using std::cout；
4. 完全不用using，而是直接std::cout；

# 第4章：复合类型

面向对象编程与传统的过程性编程的区别在于，OOP强调的是在运行阶段（而不是编译阶段）进行决策。

在运行阶段做决策并非OOP独有的，但使用C++编写这样的代码比使用C语言简单。

int *p1, p2;	// 对于每一个指针变量名，都需要一个星号。

C++中，int*是一种复合类型，是指向int类型的指针。

一定要在对指针应用解除引用运算符（*）之前，将指针初始化为一个确定的、适当的地址。

```c++
int *pt;
pt = 0xB8000000;	// type mismatch
pt = (int *)0xB8000000;	//type match
```

在C99标准发布之前，C语言允许这样赋值。但C++在类型一致方面的要求更严格，编译器将显示一条错误消息，通告类型不匹配。

指针的真正用武之地在于，在运行阶段分配未命名的内存以存储值。

```c++
int *pn = new int;	// pn指向的内存不是变量

int higgens;
int *pt = &higgens;	//pt指向的内存是变量	
```

C++提供了检测并处理内存分配失败的工具。

只能用delete来释放使用new分配的内存。然而，对空指针使用delete是安全的。

用new分配内存之后，程序确实跟踪了分配的内存量，以便以后使用delete []运算符的时候能够正确的释放这些内存。但这种信息不是公用的，例如，不能使用sizeof运算符来确定动态分配的数组包含的字节数。

```c++
double *p3 = new double [3];
p3 = p3 + 1;	// ok! this is ok for pointers, but not ok for array names, because it's const;
```

**对数组取地址的时候，数组名也不会被解释为其地址。数组名被解析成为其第一个元素的地址，而对数组名应用地址运算符时，得到的是整个数组的地址！例外情况是，将sizeof运算符用于数组名时，此时将返回整个数组的长度（单位为字节）**// 数组名是一个复合类型，不要简单的把它当成一个指针！

```c++
是个指针 -> short (*pas)[20]; -> 指向长度为20 的数组的指针
是个数组 -> shor *pas [20]; -> 指向一个数组，该数组是关于short指针的数组
```

数组退化为指针：数组名只在同一个栈空间拥有数组特性，不同栈空间中是指向首地址的普通指针。

```c++
tacos[0] means *tacos
tacos[3] means *(tacos+3)
```

c语言风格的字符串复制操作中，应该使用strncpy而不是strcpy，strncpy的第三个参数可以确定复制的最大字符数：

```c++
char food[20] = "carrots";
strncpy(food, "a prisadfdsa fdsaf sda fdasf sda fdas ", 19);
food[19] = '\0';
```

根据分配内存的方法，C++有3种管理数据内存的方式：

1. 自动存储=自动变量=局部变量（栈中）
2. 静态存储=整个程序执行期间都存在的存储方式
   1. 在函数外面定义它
   2. 在声明变量的时候使用关键字static
3. 动态存储=new和delete=内存池里面的自由存储空间（free store）或堆（heap）

**关于const和*的存放位置与区分**

Bjarne 在他的《The C++ Programming Language》里面给出过一个助记的方法——“以 ***** 分界，把一个声明**从右向左**读”。
注意语法，* 读作 pointer to (指向...的指针)，const (常量) 是形容词，char (变量类型) 和 p (变量名) 当然都是名词。 
1) const char * p 读作：p is a pointer to a const char，译：p 是一个指针(变量)，它指向一个常量字符(const char)。
2) char * const p 读作：p is a const pointer to a char，译：p 是一个常量指针(const p)，它指向一个字符(变量)。

另外请再注意下面的情况。
先看 const int a 和 int const a，这里没有分界符 *，虽然 const 的位置不同，但意思不变，它 const 修饰的是 int，常量整数。
再看 const char * p 和 char const * p，首先以 * 分界，虽然 const 的位置改变了，但它都是在修饰 char，常量字符。

**关于*与[]数组的问题**

从右到左结合，[]的结合性比*要高

```c++
int *a[10];	// 一个数组，元素都是int指针
int (*a)[10];	// 一个指针，指向10个元素的int数组
```

**C++对于类型的要求是比较严格的**

```c++
antarctica_years_end s01, s02, s03;
const antarctica_years_end * arp[3] = {&s01, &s02, &s03};
// 指向一个常量数组
const antarctica_years_end* (*arp2)[3] = &arp;
```

# 第7章：函数——C++的编程模块

**数组退化与函数参数中的指针**

```c++
cookies == &cookies[0];
int sum = sum_arr(cookies, arSize);
int sum_arr(int arr[], int n); // 下面两种函数是一样的
int sum_arr(int *arr, int n); // 根据C++规则，cookies是其第一个元素的地址，因此函数传递的是地址，由于数组的元素的类型为int，因此cookies的类型必须是int指针，即int*。
```

**数组名和指针对应是一件好事吗？**

是的。将数组地址作为参数可以节省复制整个数组所需的时间和内存，数组很大的时候，系统拷贝的开销是很大的；程序不仅需要更多的计算机内存，还需要花费时间来复制大块的数据。另一方面，使用原始数据增加了破坏数据的风险。经典C语言中这是一个问题，但是ANSI C和C++中的const限定符提供了解决这种问题的方法。

**关于指针和指针变量**

比较严格的说法是这样的： 
系统为每一个内存单元分配一个地址值，C/C++把这个地址值称为“指针”。如有int i=5;，存放变量i的内存单元的编号(地址)&i被称为指针。 
“指针变量”则是存放前述“地址值”的变量，也可以表述为，“指针变量”是存放变量所占内存空间“首地址”的变量(因为一个变量通常要占用连续的多个字节空间)。比如在int i=5;后有一句int *p=&i;，就把i的指针&i赋给了int *型指针变量p，也就是说p中存入着&i。所以说指针变量是存放指针的变量。

**typedef和define的区别**

```
关键字typedef在编译阶段有效，由于是在编译阶段，因此typedef有类型检查的功能。
#define则是宏定义，发生在预处理阶段，也就是编译之前，它只进行简单而机械的字符串替换，而不进行任何检查。
```



typedef的好处用途：

1. typedef定义一种类型的别名，而不只是简单的宏替换。可以用作同时声明指针型的多个对象。

2. 用在旧的C代码中（具体多旧没有查），帮助struct，简化代码。C++不用非得带上struct。

3. ```
   用typedef来定义与平台无关的类型。
   比如定义一个叫   REAL   的浮点类型，在目标平台一上，让它表示最高精度的类型为：
   typedef   long   double   REAL;  
   在不支持   long   double   的平台二上，改为：
   typedef   double   REAL;  
   在连   double   都不支持的平台三上，改为：
   typedef   float   REAL;  
   也就是说，当跨平台时，只要改下   typedef   本身就行，不用对其他源码做任何修改。
   标准库就广泛使用了这个技巧，比如size_t。
   另外，因为typedef是定义了一种类型的新别名，不是简单的字符串替换，所以它比宏来得稳健（虽然用宏有时也可以完成以上的用途）。
   ```

4. 为复杂的声明定义一个新的简单的别名。方法是：在原来的声明里逐步用别名替换一部分复杂声明，如此循环，把带变量名的部分留到最后替换，得到的就是原声明的最简化版。

**关于函数指针**

函数的地址可以用函数名（后面不跟参数）来获取。如果think()是一个函数，则think则是函数的地址。

```c++
// 声明函数指针应当指定函数的返回类型以及函数的特征标（参数列表）
double pam(int);	// prototype
// 则正确的指针类型声明如下：
double (*pf)(int);	// pf points to a function that takes one int argument and that returns type double
```

通常，要声明指向特定类型的函数的指针，可以首先编写这种函数的原型，然后用(*pf)替换函数名，这样pf就是这类函数的指针。

```c++
double (*pf)(int);	// pf是一个指针
double *pf(int);	// pf是一个函数
// 原因：括号的优先级比*运算符高，因此*pf(int)意味着pf()是一个返回指针的函数，而(*pf)(int)意味着pf是一个指向函数的指针。
```

使用指针来调用函数的时候，pf(3)和(*pf)(3)是一样的效果。

为什么呢？一种学派认为，由于pf是函数指针，而\*pf是函数，那么肯定用(\*pf)()调用函数；另一种学派认为，由于函数名是指向该函数的指针，指向函数的指针的行为应该与函数名相似，因此用pf()的方法调用。C++对于两种方式都同意。



trick一下，如果你想要使用一个数组，该数组中的元素是函数指针的话，应该如何定义呢？并且返回值是一个double指针

```c++
const double * (*pa[3])(const double *, int) = {f1, f2, f3};	// 其中f1等都是函数指针
// 也许你会问能不能用auto？其实是不行的，自动类型推断只能用于单值初始化，不能用于初始化列表
```

ss
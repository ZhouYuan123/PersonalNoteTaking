# C 语言

## 1. 简介

助记符，汇编语言。

计算机语言：人和计算机交流的语言。

1972年上线，面向过程，由B语言发展而来，贝尔实验室。

国际标准：C89/C90

广泛应用于底层软件开发(OS, 驱动)。

```c
#include <stdio.h>
int main()
{
	printf("Hello World\n");
	return 0;
}
```

## 2. 数据类型

**基本类型，构造类型，指针类型，空类型。**

### 2.1 基本类型

| 内置类型	|长度(Byte)      |
| --------- | ---- |
| char       | 1 |
| short | 2 |
| int  | 4 |
| long      | 4 (C语言标准：sizeof(long)>=sizeof(int) 就可以了) |
| long long | 8 |
| float     | 4, 定义: `1.0f` |
| double    | 8 |

正整数：原码，反码，补码相同。

负整数：

>原码：最高位是1.
>
>反码：原码符号位不变，其他位取反。
>
>补码：反码+1. (内存中存放的是补码)

小端字节序:

把数据的低位字节序的内容存放在低地址处，高位字节序的内容存放在高地址处。

大端字节序:

把数据的低位字节序的内容存放在高地址处，高位字节序的内容存放在低地址处。

| 开头   |          |
| ------ | -------- |
| 0b或0B | 二进制   |
| 0      | 八进制   |
| 0x或0X | 十六进制 |

### 2.2 构造类型

#### 2.2.1 数组

`int arr[5]`: 创建。

`int arr[] = {1, 2, 3, 4, 5}`: 完全初始化。五个元素。

`int arr[10] = {1, 2, 3, 4, 5}`: 不完全初始化，剩余默认为0.

数组名是数组首元素的地址，可以认为是指针。`&arr` 是数组的地址。 `&arr[index]` 取数组中元素的地址。

二维数组数组名是数组首行的地址，作为参数需要数组指针接收，数组大小等于列。

> 例外：
>
> sizeof(数组名) ：数组名表示整个数组。
>
> &数组名 ： 数组名表示整个数组。所以，(arr + 1) = 下一个元素地址; (&arr + 1) = 增加sizeof(数组名) 。

数组 arr 做传参仅仅传递数组首元素地址(数组长度可写可不写),  所以数组做形参不代表数组。

`int sz = sizeof(arr)/sizeof(arr[0]);`： 求数组大小。(arr不能是形参)

`int arr[3][4] = {1,2,3,4,5,6,7,8,9,10,11,12};` : 自动三行四列。

`int arr[][4] = {{1,2},{3,4},{4,5}};` : 不完全初始化。// 行(3)可以省略，列(4)不行。

```c
// 可能程序死循环 
#include <stdio.h>
int main()
{
	int i=0;
    int arr[] = {1,2,3,4,5,6,7,8,9,10};
    for(i=0;i<12;i++)
    {
    	arr[i] = 0; // arr[11] 地址 = i地址
        printf("Hello World\n");   
    }
	return 0;    
}
```

## 3. 变量与常量

### 3.1 变量
|          | 局部变量         | 全局变量                                                   |
| -------- | ---------------- | ---------------------------------------------------------- |
| 位置     | 在大括号内部     | 在大括号外部                                               |
| 作用域   | 变量所在局部范围 | 整个工程 （使用时需要声明外部文件定义的extern int g_val;） |
| 生命周期 | 作用域内         | 作用域内（程序的生命周期）                                 |
| 未初始化 | 随机值           | 默认值                                                     |
| 内存     | 栈中先高地址后低 |                                                            |

### 3.2 常量

| 分类       |                                                              |
| ---------- | ------------------------------------------------------------ |
| 字面常量   | 3.14，10 ，‘a’， ”hello“                                     |
| 常变量     | const 修饰的                                                 |
| 标识符常量 | define是一个预处理指令 <br />#define MAX 1000. 定义了一个常量<br />#define ADD(X,Y) X+Y .定义了宏 (宏就是替换) 4\*ADD(2, 3) = 4\*2 + 3 |
| 枚举常量   |                                                              |

```c
enum Sex					enum Sex         
{							{
	MALE,		or				MALE = 3,
    FEMALE						FEMALE
}							}
// 每个值默认从0开始
```

## 4. 字符串

双引号。

> 隐式最后一个字符是`\0`, 这是字符串的结束标志。
>
> 是常量字符串，不能被修改。
>
> > `char arr[] = “hello”;` : 可以修改元素字符。
> >
> > `char * arr = “hello” ` :不可以修改元素字符。
>
> 存放在静态区，只会被存储一次。

char arr[] = “hello”; or char arr[] = {'a', 'b' ,'c', '\0'};

```c
#include <string.h>
int len = strlen("abc"); // 3，sizeof("abc") 是 4。
// 字符串比较不能使用 == ，使用 strcmp() 函数。
char arr[] = "bit";				// 字符串结尾是 '\0'.	四个元素。
char arr[] = {'b', 'i', 't'}; 	// 三个元素。strlen(arr) 结果是随机值, 因为遇到\0才停止。
```

`??)` : 三字母词，等于 ]

`\a` : 响铃

`\123` : 跟一至三个八进制数字

`\x12`: 跟两个十六进制数字

## 5. 常见关键字

| 关键字            |                                                              |
| ----------------- | ------------------------------------------------------------ |
| auto              | 局部变量默认都是用auto修饰的. 自动创建自动销毁               |
| extern            | 用来声明外部符号的。                                         |
| register          | 建议将该值存放到寄存器中。                                   |
| typedef 原名 新名 | 类型重定义                                                   |
| static            | 修饰局部变量，只初始化一次，方法结束不销毁。<br />修饰全局变量，只能在自己所在源文件使用，切断外部链接。<br />修饰函数，只能在自己所在源文件使用，切断外部链接。 |
| const             |                                                              |

## 6. 指针

编号 == 地址 == 指针

指针变量：指针类型的变量。

大小：

1. 所有类型指针大小相同。32位是4字节，64位8字节。
2. 不同类型指针决定了：解引用的权限有多大。
3. 不同类型指针决定了：指针+1跳过的字节数量 (步长)。

>void * : 就是指向任何类型的指针，在编译的时候不会确定其指向的类型，是在程序中进行指向的
>
>void*仅仅包含地址信息。int *不仅仅包含地址信息，还包含类型信息。

野指针：

1. 指针没有初始化。
2. 指针越界。
3. 指针指向的空间已经被释放。

`int * const p;` ： 指针常量，不能修改地址。

`const int *p;` ： 常量指针，不能修改值。

<font color=blue>**== 指针运算 ==**</font>

指针类型决定了指针的运算。

`指针-指针 = 指针之间的元素个数` ：前提是在同一片内存中。

p[2] == *(p+2)

**NOTE:** 允许指向数组元素的指针与指向数组最后一个元素后面的那个内存位置的指针比较，但是不允许与指向第一个元素之前的那个内存位置的指针进行比较。

<font color=blue>**== 指针类型 ==**</font>

**指针数组：**存放指针的数组

`int * parr[5];` ：存放五个指针。

**数组指针：** 指向数组的指针

`int (*parr)[10] = &arr;` : 指针`parr`指向有十个元素的数组，数组元素类型是int.

`int (*parr[10])[5];` ：有十个元素的数组, 每个元素类型是`int (*)[5]` （数组指针数组）

**函数指针：** 

`void (*p)(int,int) = &方法名/方法名`  : 调用的时候可以 (*p)(3, 5);或者p(3, 5);

```java
//代码1
(*(void (*)())0)(); // void (*)() - 函数指针类型
//代码2
void (*signal(int, void(*)(int)))(int);
//1. signal 和()先结合，说明signal是函数名
//2. signal函数的第一个参数的类型是int，第二个参数的类型是函数指针，该函数指针，指向一个参数为int，返回类型是void的函数
//3. siqnal函数的返回类型也是一个函数指针，该函数指针，指向一个参数为int，返回类型是void的函数
// signal是一个函数的声明 
//4. 等于 void(*) (int) signal(int, void(*) (int))，但该写法语法不支持。
//typedef - 对类型进行重定义
typedef void(*pfun_t) (int); //对void(*) (int)的函数指针类型重命名为pfun_t
typedef unsigned int uint;
pfun_t signal(int, pfun t);
```

**函数指针数组：** 存放函数指针的数组

`void (*p[2])(int,int) = {方法名1, 方法名2}`  : 去掉`p[2]` 就是数组中元素类型。

```c
// 应用：这样的功能的语句称为转移表
int (*pfArr[5]) (int, int) = { NULL, Add, Sub, Mul, Div };
int x = 0;
int y = 0;
int ret = 0;
printf("请选择:>");
scanf("%d", &input); 
printf("请输入2个操作数>:");
scanf("%d %d", &x, &y);
ret = (pfArr[input])(x, y); 
printf("ret = %d\n", ret);
```

**函数指针数组的指针：**

`void (* (*p)[2])(int, int)`:`(*p)` 代表是个指针，指向`[2]`数组，数组中每个元素`void (*)(int, int)`

**Note** : 数组去掉名字就是数据类型。

## 7. 结构体

<font color=blue>**== 定义结构体变量三种方式 ==**</font>

```c
// 1、先定义结构体类型再定义结构体变量
struct Stu
{
    char name[20];
    int age;
}
struct Stu s = { "zs" , 20}; // 定义并初始化
s.name;
struct Stu * sp = &s;
sp -> name;
// 2、定义结构体类型的同时定义结构体变量
struct Stu
{
    char name[20];
    int age;
}stu1,stu2;
// 3、直接定义结构体变量
struct
{
    char name[20];
    int age;
}stu1,stu2;
```

## 8. 流程控制

1. switch （整型表达式）

   ```c
   int input = 0;
   switch (input)
   {
   case 1:
       break;
   case 2:
       break;
   default:
   	break;        
   }
   ```

2. goto: 别用。不能跨函数跳转。

3. 循环
   1. while
   2. do while
   3. for 

```c
int main()
{
    int ch = 0;
    // windows下，在输入的空行位置，按ctrl+z可产生EOF。Linux下，按ctrl+d可产生EOF
    while((ch = getchar()) != EOF) 
        putchar(ch); // 在终端输出
    retrun 0;
}
flag:
	goto flag;
// for
int i;
for (i = 0; i < 10; i++) {
    printf("%d ", i);
}
```

## 9. 函数

### 9.1 函数分类

<font color="#4169E1">**==库函数==**</font>

网站：www.cplusplus.com/reference, http://en.cppreference.com

SDK: MSDN

<font color="#4169E1">**==自定义函数==**</font>

不写返回值类型默认为int。

可以在方法里函数声明。

### 9.2 库函数

<font color="#4169E1">**== qsort() ==**</font>

```c
struct Stu
{
	char name[20];
	int age;
}
int sort_by_age(const void* e1, const void* e2)
{
    // 升序
    return ((struct Stu*)e1)->age - ((struct Stu*)e2)->age;
}
void test2()
{
    struct Stu s[3] = { {"zhangsan", 30}, {"lisi"，34), {"wangwu"，20) } };
    int sz = sizeof(s) / sizeof(s[0]);
    //按照年龄来排序
    qsort(s, sz, sizeof(s[0]), sort_by_age);
}
```

## 10. 内存

https://www.stackoverflow.com 

| 栈区                                                         | 堆区           | 静态区                         |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| 局部变量，函数形参，返回值                                   | 动态内存分配的 | 全局变量，静态变量, 字符串常量 |
| 每次调用方法开辟栈帧空间                                     |                |                                |
| 局部变量在栈中大端存储。<br />数组地址是随index由低到高变化。 |                |                                |

## 11. 操作符

<font color=blue>**1. 算术操作符**</font>

`+ - * / %`

<font color=blue>**2. 移位操作符**</font>

`<< >>` 内存中存放的是补码。

左移：左边丢弃，右边补0.

右移：右边丢弃，左边补原符号位.

不会改变原变量值。

<font color=blue>**3. 位操作符**</font>

`&` : 二进制每一对应位都1为1。

`|` : 二进制每一对应位有1为1。

`^` : 二进制每一对应位不同为1。

只能是两个整数进行运算。

<font color=blue>**4. 赋值操作符**</font>

复合赋值符: `+= >>==`

<font color=blue>**5. 单目操作符**</font>

`!` : 逻辑反。

`-` : 负值。`+` : 正值 。

`sizeof` : 可以 `sizeof(a), sizeof(int), sizeof a` , 返回int类型，单位是字节。`sizeof(中的表达式不参与运算)`

`&` : 取地址。 

`~` : 对一个数的补码的二进制位取反。 

`--` : 前置或后置。

`++` : 前置或后置。

`*` : 间接访问操作符。

`(类型)` : 强制类型转换。

<font color=blue>**6. 关系操作符**</font>

`>=, <=, !=, ==`

`-1 > sizeof(int)` : 先将-1转成无符号整型(超级大)。

<font color=blue>**7. 逻辑操作符**</font>

`&&, ||`

<font color=blue>**8. 条件操作符**</font>

也叫三目操作符。`b = a > 5 ? 1: -1`

<font color=blue>**逗号表达式**</font>

`, ` : 逗号操作符，从左向右依次执行，赋值时会使用最后一个表达式的值。

<font color=blue>**9. 下标引用操作符**</font>

`[]` : 数组访问元素时使用。可以arr[2], 也可以2[arr]。

<font color=blue>**10. 函数调用操作符**</font>

`()` : 

<font color=blue>**11. 结构成员访问操作符**</font>

`.` : 

`->` : 

## 12. sizeof 详解

```c
// sizeof 详解
int a[] = { 1,2,3,4 };
printf("%d\n", sizeof(a));				// 16
printf("%d\n", sizeof(a + 0));			// 4 or 8
printf("%d\n", sizeof(*a));				// 4
printf("%d\n", sizeof(a + 1));			// 4 or 8
printf("%d\n", sizeof(a[1]));			// 4

printf("%d\n", sizeof(&a));				// 4 or 8
printf("%d\n", sizeof(*&a));			// 16 [*& 抵消了]
printf("%d\n", sizeof(&a + 1));			// 4 or 8
printf("%d\n", sizeof(&a[0]));			// 4 or 8
printf("%d n", sizeof(&a[0] + 1));		// 4 or 8

char arr[] = {'a','b','c','d','e','f'};
printf("%d\n", sizeof(arr)); 			// 6
printf("%d\n", sizeof(arr + 0));		// 4 or 8
printf("%d\n", sizeof(*arr));			// 1
printf("%d\n", sizeof(arr[1]));			// 1
printf("%d\n", sizeof(&arr));			// 4 or 8
printf("%d\n", sizeof(&arr + 1));		// 4 or 8
printf("%d\n", sizeof(&arr[0] + 1));	// 4 or 8

printf("%d\n", strlen(arr)); 			// 随机值
printf("%d\n", strlen(arr + 0));		// 随机值
printf("%d\n", strlen(*arr));			// error
printf("%d\n", strlen(arr[1]));			// error
printf("%d\n", strlen(&arr));			// 随机值
printf("%d\n", strlen(&arr + 1));		// 随机值 - 6
printf("%d\n", strlen(&arr[0] + 1));	// 随机值 - 1

char arr[] = "abcdef";					// 0 就是 \0
printf("%d\n", sizeof(arr)); 			// 7
printf("%d\n", sizeof(arr + 0));		// 4 or 8
printf("%d\n", sizeof(*arr));			// 1
printf("%d\n", sizeof(arr[1]));			// 1
printf("%d\n", sizeof(&arr));			// 4 or 8 char(*)[7]
printf("%d\n", sizeof(&arr + 1));		// 4 or 8
printf("%d\n", sizeof(&arr[0] + 1));	// 4 or 8

printf("%d\n", strlen(arr)); 			// 6
printf("%d\n", strlen(arr + 0));		// 6
printf("%d\n", strlen(*arr));			// error
printf("%d\n", strlen(arr[1]));			// error
printf("%d\n", strlen(&arr));			// 6
printf("%d\n", strlen(&arr + 1));		// 随机值 
printf("%d\n", strlen(&arr[0] + 1));	// 5

char* p = "abcdef";
printf("%d\n", sizeof(p));				// 4 or 8
printf("%d\n", sizeof(p + 1));			// 4 or 8
printf("%d\n", sizeof(*p));				// 1
printf("%d\n", sizeof(p[0]));			// 1 == *(p+0)
printf("%d\n", sizeof(&p));				// 4 or 8
printf("%d\n", sizeof(&p + 1));			// 4 or 8
printf("%d\n", sizeof(&p[0] + 1));		// 4 or 8

printf("%d\n", strlen(p));				// 6
printf("%d\n", strlen(p + 1));			// 5
printf("%d\n", strlen(*p));				// error
printf("%d\n", strlen(p[0]));			// error
printf("%d\n", strlen(&p));				// 随机值
printf("%d\n", strlen(&p + 1));			// 随机值
printf("%d\n", strlen(&p[0] + 1));		// 5

// 二维数组
int a[3][4] ={ 0 };
printf("%d\n", sizeof(a));				// 48
printf("%d\n", sizeof(a[0][0]));		// 4
printf("%d\n", sizeof(a[0]));			// 16
printf("%d\n", sizeof(a[0] + 1));		// 4 第一行第二个元素地址
printf("%d\n", sizeof(*(a[0] + 1)));	// 4
printf("%d\n", sizeof(a + 1));			// 4 第二行地址
printf("%d\n", sizeof(*(a + 1)));		// 16
printf("%d\n", sizeof(&a[0] + 1));		// 4 第二行地址
printf("%d\n", sizeof(*(&a[0] + 1)));	// 16
printf("%d\n", sizeof(*a));				// 16 第一行地址 *(a+0) -> a[0]
printf("%d\n", sizeof(a[3]));			// 16
```

## 13. 调试

Release 和 debug 版本。

release版本会优化代码。

F5停到断点之后，调试 --> 窗口

## NOTE:

### 1. 库函数

利用C语言语法实现的函数。

| name                                                         |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| printf("Hello World");<br />printf(“%d\n”, sizeof(a));       | <stdio.h>, <br />%d：十进制整数<br />%x: 十六进制<br />%2d：不够左边用空格填充<br />%-2d：不够右边用空格填充<br />%f: float<br />%lf: double<br />%c: 字符<br />%s: 字符串<br />%p: 地址<br />%u: 无符号整型。 |
| scanf(“%d %d”，&a, &b);                                      | 输入函数，scanf_s是VS自带的。不能读空格。                    |
| getchar();                                                   | 获取缓冲区                                                   |
| Sleep(n);                                                    | <windows.h>                                                  |
| system("cls");                                               | 清屏                                                         |
| int rand(void);<br />void srand(unsigned int seed)<br />time(NULL) | <stdlib.h> 返回 [0-0xfff]<br />seed决定rand()值<br /><time.h> 返回时间戳，可以(unsigned int)time(NULL); |
| sqrt()                                                       | 开平方。                                                     |
| system()<br />system("shutdown -s -t 60")                    | 执行系统命令<br />60s后关机, shutdown -a取消关机。           |
| memset()                                                     | 设置内存，可以用来修改数组。                                 |
| strcap(desArray, srcArray);                                  | 复制字符串。<string.h>                                       |
| size_t strlen(const char *str)                               | <string.h> 返回字符串长度。                                  |
| assert()                                                     | 断言                                                         |
| char * gets(char * str)                                      | 接收有空格字符串。                                           |
| pow()                                                        | \<math.h>                                                    |
|                                                              |                                                              |
### 2. 标准库类型

| name   |              |
| ------ | ------------ |
| size_t | unsigned int |
|        |              |
|        |              |

### 3. 库文件

| 文件    |                          |
| ------- | ------------------------ |
| float.h | 定义浮点数最大最小值。   |
| limis.h | 定义整数类型最大最小值。 |
|         |                          |



# THE END

# Java

## 1. 简介

### 1.1 基础知识

冯诺依曼体系结构：
输入，输出，存储，运算和控制 (Central Processing Unit)。

摩尔定律，安第-比尔定律，反摩尔定律。

TB PB EB ZB YB

URI： 统一资源标识符（Uniform Resource Identifier）
URL: URL是URI的一个子集，统一资源定位符，uniform resource locator。URL是URI概念的一种实现方式。只要能唯一表示资源的就是URI，在URI的基础上给出其资源的访问方式的就是URL。
http: 超文本传输协议（Hyper Text Transfer Protocol)。

软件：数据和指令的集合。

GUI: Graphical  User Interface
CLI: Command Line Interface

### 1.2 常见DOS命令

|        |             |
| ------ | ----------- |
| md     | 创建目录        |
| rd     | 删除目录        |
| del    | 删除文件        |
| del 目录 | 提示是否删除目录下文件 |

### 1.3 历史

机器语言，汇编语言，高级语言。
SUN (Stanford University Network)

> <font color="#000000">1991年，Green项目, Oak。</font>
> <font color="#000000">1994年，Oak适合于互联网。</font>
> <font color="#000000">1995年，开发。</font>
> <font color="#000000">1996年，JDK1.0</font>
> <font color="#000000">2004年，JDK1.5，为突出版本的重要性，更名为JDK5.0。</font>
> <font color="#000000">2014年，JDK8.0。</font>

<font color="#cc9900">**舍弃了C的：指针，运算符重载，多重继承（接口代替）**</font>

"Write once, Run Anywhere"

JDK包括了JRE。

javadoc命令生成文档注释。

一个文件中多个类会生成多个字节码文件。

true, false, null不是关键字。保留字： goto, const.

标识符: 可以取名字的地方。

强类型语言。

## 2. 数据类型

### 2.1 数据类型

#### 2.1.1 基本数据类型

byte 		byte b = 128;// 编译不通过
short 	2byte
int      	4byte
long 		8byte
float 		4byte 表示范围比long要大
double 	8byte
char 		2byte  '\u0043' Unicode值是一个字符，CodeChars.pdf所有字符集。有且一个字符。a:97， A:65。默认值是0或者‘\u0000’
boolean   Java规范中，没有明确指出boolean的大小。在《Java虚拟机规范》给出了4个字节，和boolean数组1个字节的定义，具体还要看虚拟机实现是否按照规范来，所以1个字节、4个字节都是有可能的。

#### 2.1.2 数组

`int [] arr = {1, 2, 3, 4, 5}`: 可以省略等号右边的 new int []

### 2.2 进制

二进制 （binary）, 0b或者0B开头。
十进制 （decimal）。
八进制 （octal）, 0开头。
十六进制 （hex）, 0x或者0X开头。

### 2.3 运算符

`>>>` : 无符号右移，没有 `<<<`

```java
num1 = num1 ^ num2; // 只适用于数值类型变量值交换
num2 = num1 ^ num2;
num1 = num1 ^ num2;
```

优先级：

switch 表达式类型：byte，short，char, int, 枚举(1.5)，String(1.7)

## NOTE: 

### 1. Eclipse 快捷方式

|                  |                |
| ---------------- | -------------- |
| Shift + Enter    | 快速新建下一行 |
| Ctrl + 1 + Enter | 接收变量名     |
|                  |                |



1. eclipse设置
   1. 在workspace根目录 `.metadata` 中

`break label 和 continue label 不太一样`

1.简单名称（Simple Name）没有类型和参数修饰的方法或字段名称例如inc方法和字段name

2.全类名全类名是某个文件在项目中的位置，格式为包名.类名

3.全限定名（Fully Qualified Name）一个类的全限定名是将类全名的.全部替换为/例如com/itheima/dao/IUserDao.xml

4.路径分为相对路径和绝对路径。绝对路径是指这个文件在操作系统中的位置，相对路径通过这个文件的上一级 ./ 或下一级/ 来指定文件内容

5.描述符（Descriptor）A descriptor is a string representing the type of a field or method.

6.签名（Signatures）Java代码层面的方法特征签名：方法名称 + 参数顺序 + 参数类型字节码层面的方法特征签名： + 返回值 + 受查异常表

7.符号引用符号引用包括域和方法的符号引用，符号引用由两部分组成：1）所属的类或接口2）字段和方法 名字+描述符————————————————

# THE END

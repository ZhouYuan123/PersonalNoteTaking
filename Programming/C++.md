# C++

## 1. 简介

1979 - 1981: C with classes

从1982年开始，C++开始定位作为一个新的编程语言，使用编译技术重新实现了「带类的C」，对应的编译器为Cfront

1983年底，C++正式被命名。

```c++
#include <iostream>
using namespace std;
int main()
{
    cout << "Hello World" << endl;
    return 0;
}
```

转换后的C加上前缀C，没有扩展名，例如 `cstdio`, `cmath`，`ctype`等。

`#include <cstdio> ` : `cstdio` 源文件中还是 `#include <stdio.h> `

`\n ` 与 `endl` : 前者只换行，后者换行并 + `fflush(stdin)`(立即输出)

## 2. 与C

主存(main memory)也叫随机访问存储器RAM(Random Access Memory)

新的数据类型string。

```c++
// 1.强制以小数的方式显示
cout << fixed;
// 2.控制显示的小数的位数 <iomanip>
cout << cout.setprecision(2);
// 3.设置打印宽度 <iomanip> 默认右对齐
cout << left;
cout << setfill('_');
cout << setw(n) << 3.14;
// 可以打印出 'true' 'false'
cout << boolalpha;

int num;
char ch1, ch2;
cin >> num; // 可以一次输入13ab，然后程序执行成功，分开读取
cin >> ch1;
cin >> ch2;
```

文档注释 : `/** 文档注释 */`

## 1. 运算符重载

对于内置数据类型不能实现运算符重载。

**加号运算符+**

```c++
Object operator+(Object &o)
{
    //语句
    return
}
```

**左移运算符<<**

```c++
ostream& operator<<(ostream &cout, Object &o)
{
    cout << "" << "";
    return cout;
}
```

**递增运算符++**

```c++
Object& operator++()
{
    //语句
    return
}
Object operator++(int) //后置递增，不要返回引用
{
    //语句
    return
}
```

**赋值运算符=**

```c++
new int(); // 返回的是 int *
Object& operator=(Object &o)
{
    //语句
    return *this;
}
```

**仿函数()**

```c++
void operation()(string test)
{

}
对象名("AAA"); // 调用
```

## 2. 文件操作

### 2.1 文本文件格式

文本以ASCII码的形式存储在计算机中。

```c++
#include <fstream> // 读写流
ofstream ofs;
ofs.open("文件路径", ios::out); // 写文件
ofs << "内容1" << endl;
ofs << "内容2" << endl;
ofs.close();
```

```c++
#include <fstream>
ifstream ifs
ifs.open("文件路径", ios::in);
if(ifs.is_open()){
    char buf[1024] = {0};
    // 第一种
    while (ifs >> buf){
        cout << buf << endl;
    }
    // 第二种
    while (ifs.getline(buf, sizeof(buf))){
        cout << buf << endl;
    }
    // 第三种
    string buf;
    while (getline(ifs, buf)){ 
        cout << buf << endl;
    }
    // 第四种
    char c;
    while ((c = ifs.get()) != EOF){ 
        cout << c;
    }
}
ifs.close();
```

### 2.2 二进制文件

二进制存储，无法读懂。

同理：只需要使用 `ofs.open("文件路径", ios::out | ios::binary);`

==========

## 快捷键：

| 删除行  | ctrl + L        |
|:---- |:--------------- |
| 快速复制 | ctrl + D        |
| 提示   | ctrl + J        |
| 纵向多选 | alt + shif + 鼠标 |

# C++

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

# Python

## 1. 简介

​    胶水语言，背后有强大的代码库。动态语言。

​    1991年，荷兰人。

​    现在版本python3。 2020年python2停止更行。

* 跨平台 
* 解释型语言
* 一种交互式语言
* 面向对象 （一切皆对象）

## 2. 安装

### 2.1 安装python解释器

​    官网：www.python.org

​    下载：www.python.org/downloads/release/python-381/

Files --> 下载第二个：[Windows x86-64 executable installer](https://www.python.org/ftp/python/3.8.1/python-3.8.1-amd64.exe)

运行： 

IDLE: 开发环境。new file: 写长的代码

Python: 交互式的。

Python Manuals: 官方手册。

Python module docs: 已经安装的。

### 2.2 PyCharm

community 下载这个就可以。

### 2.3 Hello World

```python
#!/usr/bin/python
print("Hello World")
```

**node：**关于脚本第一行的的解释，只对 Linux/Unix 用户适用，用来指定本脚本用什么解释器来执行。有这句的，加上执行权限后，可以直接用 ./ 执行，不然会出错，因为找不到 python 解释器。

## 3. 转义字符

\b，退格=backspace

字符串前面加r或者R，使转义失效。

Unicode表规定什么字符用什么数字。UTF-8决定什么字符用几个字节。

## 4. 数据类型

**int:** 0b: 二进制。0o：八进制。0x: 十六进制。

**float:**

**bool:** True = 1, false = 0. 可以直接参与数值结算。

**str:** 单引号和双引号只能在一行，三当引号三双引号可以在多行。

<u>数据类型转换：</u>

不同数据类型不能直接连接操作。

`type(variable)` : 返回数据类型

| str(variable) | int(variable) 不能转小数字符串 | float() |
| ------------- | ---------------------- | ------- |

## 5. 注释

`#` : 单行注释。没有多行注释，但是可以用三引号充当多行注释。

`#coding:GBK` : 文档第一行申明编码类型。

```python
present = input('请输入你的内容:') #input 函数
print(present)
```

## 6. 运算符

<u>算术运算符 :</u>
`+ - * / //(整除) % **(幂运算)` 

<u>赋值运算符：</u>
`a=b=c=8` ：链式赋值
`a+=30` ： 参数赋值 	`a=b,b=a` 就可以实现参数值得互换 
`a,b,c=20,30,40`: 系列解包赋值

<u>比较运算符：</u>
一个变量组成：标识（id），类型，值。
`==`：比较值。
`is, is not  ` : 比较id。

<u>布尔运算符：</u>
`and, or, not, in, not in   ` 

<u>位运算符：</u>
`&, |, <<, >> `

优先级：算术运算符 > 位运算符 > 比较运算符 > 布尔运算符 > 赋值运算符

## 7. 程序的组织结构

任何简单或复杂的算法：顺序结构，选择结构，循环结构。

```python
if 条件表达式:
	执行语句
else:
	执行语句
# 多分支
if 90<=score<=100:
	执行语句
elif 条件表达式:
	执行语句
[else:]
	执行语句
```

```python
#条件表达式
x if 判断条件 else y #返回x或者y
```

```python
while 条件表达式:
    条件执行体
else:
    条件执行体 # 循环在没有遇到break正常结束后会执行else
    
for 自定义的变量 in 可迭代的对象:
    条件执行体 
    break
    continue
else:
    条件执行体 # 循环在没有遇到break正常结束后会执行else
```

`pass` : 占一个语句位置。

## 8. 对象的布尔值

一切皆对象，所有对象都有一个布尔值。

- 0的布尔值为False，非0布尔值为True.

## 9. 数据结构

### 9.1 列表

有序，索引访问，可重复，类型可混存，动态分配内存和自动内存回收

```python
# 列表创建
lst=[] or lst() #空列表
lst=['hello','world',98]
lst2=list(['hello','world',98])

# 查询
lst.index('hello') # 返回相同元素第一个的index，不存在抛异常 ValueError
lst.index('hello',1,3) # [1-3)之间是否存在hello
lst[N] or lst[-N] # -N从-1开始，没有索引抛异常 
lst[start:stop:step] # 切片原列表，不包括stop, 三个值都可以省略。step为-1，反序切。

# 判断
元素 in lst
元素 not in lst

# 遍历
for _ in lst:
    print(_)
for index,value in enumerate(lst):
    pass

# 增
lst.append(100)
lst.extend(lst2)
lst.insert(index, 100)
lst[1:] = lst2 # index1 之后的内容用新的列表替换掉

# 删
lst.remove(100) # 只移除重复元素第一个，如果元素不存在 ValueError
lst.pop(index) # 删除索引位置元素，如果不存在 Index Error
lst.pop() # 删除最后一个元素
new_list = lst[1:3] # 原列表没有变化
lst[1:3] = [] # 间接删除原列表
lst.clear() # 清空
del lst # 删除变量定义 再使用undefined

# 排序
lst.sort()
lst.sort(reverse=True) # 降序
new_list=sorted(lst) # 产生新的列表对象
new_list=sorted(lst,reverse=True) # 降序

#列表生成式 
[i for i in range(1, 10)] #后面的i都放到前面里,也可以[i*i for i in range(1, 10)]
```

### 9.2 字典

无序，key必须是不可变序列，key不重复value可以重复，内存较大(根据key的hash值确定位置)空间换时间
```python
# 字典创建
d={} or dict() # 空字典
d={'hello':'world','张三':98}
d=dict(name='hello',age=98)
d=dict(zip(list1,list2))

# 获取
d['张三'] # KeyError
d.get('张三') # 不会报错，返回None
d.get('张三', 99) # 不存在时返回99

d.keys() # type(d.keys()) <class 'dict_keys'>
list(d.keys()) # [k]
d.values() # type(d.values()) <class 'dict_values'>
list(d.values()) # [v]
d.items() # type(d.items()) <class 'dict_items'>
list(d.items()) # [(k,v)]

# 判断
key in d
key not in d
for key in d:
    print(key) #注意：是key

# 增改
d['张三'] = 98

# 删 
del d['张三'] # 删除键值对
d.clear() # 变为空字典

#字典生成式 
items = ['a','b','c']
prices = [1,2,3]
{item.upper():price for item,price in zip(items,prices)} # 以元素少的list为基准生成元素个数。
```

### 9.3 元组

有序，内置数据结构，不可变序列(元素引用不可变，数据可变)
```python
# 元组创建
t=() or tuple() # 空元组
t=('hello','world',98)
t2='hello','world',98
t3=('hello',) # 只有一个元素必须加逗号
t=tuple(('hello','world',98))

# 查询
t[N] # 没有索引抛异常 
```

### 9.4 集合

无序，内置数据结构，可变序列，只有key (数据不重复)

```python
# 集合创建
s={'hello','world',98}
s=set(range(6))
s=set(['hello','world',98])
s=set(('hello','world',98))
s=set('hello') # {'o','h','e','l'}
s=set({'hello','world',98})
s={} # 空字典
s=set() # 空集合

# 判断
元素 in s
元素 not in s

# 增加
s.add(98)
s.update({200,400,300}) # 增加了
s.update([200,400,300])
s.update((200,400,300))

# 删 
s.remove(98) # 如果元素不存在，KeyError
s.discard(98) # 如果元素不存在，不抛异常
s.pop() # 删除第一个元素（第一个元素本身就是随机的）
s.clear()

# 
s1==s2 # 集合元素是否相等
s1.issubset(s2) # s1 是 s2的子集？
s1.issupperset(s2) # s1 是 s2的超集？
s1.isdisjoint(s2) # s1， s2是否没有交集？
s1.intersection(s2) or s1 & s2 # 取交集
s1.union(s2) or s1 | s2 # 取并集
s1.difference(s2) or s1 - s2 # 取差集
s1.symmetric_difference(s2) or s1^ s2 # 取对称差集

#集合生成式 
{i for i in range(1, 10)} #后面的i都放到前面里,也可以{i*i for i in range(1, 10)}
```

## 10. 字符串

是一个基本数据类型，不可变。== 比较的是内容。

### 10.1 字符串驻留机制

相同的字符串，指向同一个地址的条件：

1. 字符串长度为0或者1
2. 符合标识符的字符串
3. 只在编译时驻留
4. -5,256 之间的驻留

强制驻留，sys.interna(a)。 PyCharm对字符串进行了优化，会自动驻留。

### 10.2 字符串处理

| 方法                                                         |                                          |
| ------------------------------------------------------------ | ---------------------------------------- |
| .index('')                                                   | 找不到，ValueError                       |
| .find('')                                                    | 找不到，返回 -1                          |
| .rindex('')                                                  | 最后一个指定字串, 找不到，ValueError     |
| .rfind('')                                                   | 最后一个指定字串, 找不到，返回 -1        |
| .upper(), lower(), swapcase(), capitalize(), title()         | 产生新的转换的字符串。                   |
| center(totalNumber, ‘填充符’),                               | 左右填充，默认填充空格，超过返回原字符串 |
| ljust(totalNumber, ‘填充符’), rjust(totalNumber, ‘填充符’),  | 右填充, 左填充。                         |
| zfill(宽度)                                                  | 右对齐，左边0填充。                      |
| split(sep='指定分隔符')                                      | 默认用空格分割，返回列表                 |
| split(sep='指定分隔符', maxsplit=1)                          |                                          |
| rsplit(sep='指定分隔符'), split(sep='指定分隔符', maxsplit=1) |                                          |
| isidentifier()                                               | 是不是合法标识符                         |
| isspace()                                                    | 是不是空白字符，包括\t \n \r             |
| isalpha()                                                    | 是否由全字母组成                         |
| .isdigit()                                                   | 是不是数字。                             |
| isdecimal()                                                  | 是否全部由十进制数字组成                 |
| isnumeric()                                                  | 是否全部由数字组成 （123四）true         |
| isalnum()                                                    | 是否由数字和字母组成                     |
| replace('Pythoin', 'Java')<br />replace('Pythoin', 'Java', 指定次数) | 用Java替换Python                         |
| '\|'.join(lst)，'*'.join(t)，                                | lst转为字符串用指定字符拼接              |

```python
# 使用zfill方法：给字符串或者数字前面补0，例如123，补足5位，显示为00123;
n="123"
s=n.zfill(5)
print(s) # 00123

# 字符串里的不一定需要是数字，其余字符也可以：
n="xyz"
s=n.zfill(5)
print(s) # 00xyz

# 对于纯数字，不能用zfill，可以参考C语言中的方法：
n=123
s="%05d"%n
print(s) # 00123
```

### 10.3 字符串的比较

内置函数ord()获取原始值。

`'a'>'b'` : 97>98, False

`==` : 判断内容，is 判断地址。

### 10.4 字符串切片

切片后返回新的字符串。

`s[:5]` : 前五个字符的串。

`s[6:]`:  从六到最后。

`s[6::2]`: 步长为2。`s[::-1]`: 反转了字符串。

### 10.5 格式化字符串

```python
print('%s%d' % (name,age))
print('%10d' % 99) # 10表示宽度
print('%.3f' % 3.1415926) # 3个小数 3.142
print('%10.3f' % 3.1415926) # 同时设置 			3.142

print('{0}{1}{0}'.format(name,age))
print('{0:.3'.format(3.1415926)) # 3位 3.14
print('{0:.3f'.format(3.1415926)) # 3个小数 3.142
print(f'{name}{age}')
```

### 10.6 字符串编码转换

`print(s.encode(encoding='GBK'))` : 一个中文占两个字节

`print(s.encode(encoding='UTF-8'))` : 一个中文占三个字节

`print(b.decode(encoding='UTF-8'))` : 一个中文占三个字节

## 11. 函数

```python
def calc(a, b):
calc(20, 10) # 位置实参   
calc(*lst) # 结构列表，不然会因为参数不对应报错。字典：calc(**dict) 
calc(b=10, a=20); # 关键字实参   

# 只有一个返回值返回原值。
# 返回值是多个返回元组。

# 参数默认值
def calc(a, b=10):
    
# 可变位置参数
def fun(*args):
    print(args)
# 可变关键字参数
def fun1(**args): # 结果是一个字典
    print(args)
fun1(a=1,b=2) # {'a':1, 'b':2}
```

局部变量作用域只在函数内部。需要global a变为全局。

## 12. 异常

```python
try:
	执行语句
except ZeroDivisionError:
    执行语句
except ValueError as e:
    print(e)
else:
    执行语句 # 只有没有expection的时候，才会执行
finally:
    总是执行
```

常见异常：`ZeroDivisionError, IndexError, KeyError, NameError, SyntaxError, ValueError`

traceback模块：

```python
import traceback
	traceback.print_exc()
```

## 13. 类

### 13.1 类定义

```python
class Student:
    a = 'a' # 类属性
    def eat(self): # 实例方法， 类之外称为函数，类之内叫作方法。
        pass
    @staticmethod
    def sm(): # 静态方法
        pass
    @classmethod
    def cm(cls): # 类方法，调用 Student.cm() // 不需要传参
        pass
    
    def __init__(self,name,age): # 初始化方法
        self.name = name # self.name 实例属性
        self.age = age
        
```

### 13.2 对象创建

```python
stu = Student('zs', 20)
print(stu) # 实例对象
print(Student) # 类对象
stu.eat() # 方法调用
Student.eat(stu) # 方法调用

stu.gender='女' # 动态绑定
def show():
    pass
stu.show = show # 动态绑定方法
```

## 14. 面向对象

封装，继承和多态。

### 14.1 继承

```python
class 子类类名( 父类1，父类2 ):
    pass

class Person(object): # 继承了object，不写也是默认继承
    def __init__(self,name,age):
        self.name = name
        self.age = age
    def info(self):
        pass
class Student(Person):
    def __init__(self,name,age,stu_no):
        super().__init__(name,age)
        self.stu_no=stu_no
    def info(self): # 方法重写
        pass 
	def __str__(self): # 重写
        return '我的名字是{0}'.format(self.name) 
    
```

动态语言的多态，只关心行为。

## 15. 特殊属性和特殊方法

下划线的属性和方法。

| 特殊属性           |                              |
| ------------------ | ---------------------------- |
| \_\_dict\_\_       | 实例对象、类对象属性的字典。 |
| \_\_class\_\_      | 对象所属的类。               |
| \_\_bases\_\_      | 父类类型的元组。             |
| \_\_base_\_        | 第一个父类。                 |
| \_\_mro\_\_        | 类的层次结构。               |
| \_\_subclasses\_\_ | 子类类型的列表。             |

| 特殊方法           |                            |
| ------------------ | -------------------------- |
| \_\_add\_\_()      | 加号操作底层调用的方法     |
| \_\_len\_\_()      | 内置方法len(lst)调用的方法 |
| \_\_init\_\_(self) | 初始化对象                 |
| \_\_new\_\_(cls)   | 创建对象                   |
| \_\_str\_\_()      | 对象的描述                 |

## 16. 拷贝

```python
import copy
obj2 = copy.copy(obj1) # 浅拷贝
obj3 = copy.deepcopy(obj1) # 深拷贝
```

## 17. 模块

### 17.1 模块

一个 .py 文件就是一个模块。

```python
import 模块名称 [as 别名]
from 模块名称 import 函数/变量/类
```

PyCharm导入自定义模块：

在模块所在文件夹右击 --> Mark Directory as  Sources Root

package中 默认包含\_\_int\_\_.py文件

```python
if __name__ == '__main__'
	pass # 只有当前模块作为主程序运行才会执行

```

### 17.2 常用内置模块

| 常用内置模块 |                                                              |
| ------------ | ------------------------------------------------------------ |
| sys          | sys.getsizeof(a)                                             |
| time         | time.time()： 秒<br />time.localtime(time.time()) : 转成本地时间 |
| urllib       | .request.urlopen('http://www.baidu.com')                     |
| re           | 正则                                                         |
| math         | .pi : 圆周率                                                 |
| decimal      |                                                              |

### 17.3 第三方模块

`pip install 模块名 `： 在线安装， DOS窗口中执行。

`python`：进入python交互程序。

`import 模块名`：验证是否报错。

## 18. 编码与持久化

Python的解释器使用的是Unicode内存，.py文件在磁盘上使用UTF-8存储外存。

```python
#encoding=gbk #指定编码格式
file = open('a.txt', 'a')
file.write('Python')
file.writelines(['Python','java']) # 同一行
# print('内容', file=file)
file.close()

file = open('a.txt', 'r')
file.read() # 读出所有 file.read(n) n:字符个数
file.readline() 
file.readlines() # 返回列表
file.seek(2) # 跳过字节的个数 seek(offset[,whence]) offset:负数反向。whence：0，从开头开始计算。1：从当前位置计算。2：从文件尾开始计算。
file.tell() # 告诉指针当前位置
file.flush()
file.close()

#with 语句, 不需要手动关闭
with open('a.txt', 'r') as file: # file 文件重写了上下文管理器
    pass 
```

| 打开方式 |                        |
| -------- | ---------------------- |
| r        | 只读                   |
| w        | 创建或者覆盖           |
| a        | 创建或者追加           |
| b        | 以二进制打开，rb or wb |
| +        | 读写方式打开           |

## 19. os

```python
import os
os.system('notepad.exe') # 打开记事本
os.system('calc.exe') # 打开计算器
os.startfile('路径') # 打开程序
```

| os.                                                  |                            |
| ---------------------------------------------------- | -------------------------- |
| getcwd()                                             | 返回当前工作目录           |
| listdir('../文件夹')                                 | 列出文件和目录             |
| mkdir(path[,mode])<br />makedirs(path1/path2[,mode]) | 创建目录<br />创建多级目录 |
| rmdir(path)<br />removedirs('')                      |                            |
| chdir(path)                                          | 切换工作目录               |
| walk(path)                                           | 返回对象列表               |

| os.path          |                    |
| ---------------- | ------------------ |
| abspath(path)    |                    |
| exists(path)     |                    |
| join(path, name) | 拼接名字。         |
| split(path)      | 分离路径和文件名。 |
| splittext(path)  | 分离文件和后缀名。 |
| basename(path)   | 提取文件名。       |
| dirname(path)    | 提取目录。         |
| isdir(path)      |                    |

## NOTE：

### 1. 内置函数

#### 1.1 print

```python
print("Hello",end ="") # 默认换行，用end参数来设置你想要的结束符号

# \033[显示方式;字体色;背景色m打印内容\033[0m
print("\033[0;31;40mHello World\033[0m")
print("\033[0;31;40m")
print("Hello World")
print("\033[0m")
```

| 显示方式 | 效果         |
| -------- | ------------ |
| 0        | 终端默认设置 |
| 1        | 高亮显示     |
| 4        | 使用下划线   |
| 5        | 闪烁         |
| 7        | 反白显示     |
| 8        | 不可见       |

| 字体色 | 背景色 | 颜色描述 |
| ------ | ------ | -------- |
| 30     | 40     | 黑色     |
| 31     | 41     | 红色     |
| 32     | 42     | 绿色     |
| 33     | 43     | 黄色     |
| 34     | 44     | 蓝色     |
| 35     | 45     | 紫红色   |
| 36     | 46     | 青蓝色   |
| 37     | 47     | 白色     |

#### 1.2 others

```python
range(stop) # 返回一个[0-stop)的序列，步长为1
range(start,stop,step)
input('提示') # 从键盘接收
dir(stu) # 返回当前范围内变量
id(stu)
type(stu) # 数据类型
'{0}{1}'.format('内容1','内容2')
'{:>8}{:a>8}'.format('内容1','内容2') # '     内容1','aaaaa内容2'， ^<>中左右对其
# 进制 精度 format等等

# sorted(iterable, cmp=None, key=None, reverse=False)，其中
# iterable是可迭代对象，包括列表、元组、字典、字符串；
# cmp代表比较函数；
# key代表迭代对象中的某个属性，如某个元素的下标；
# reverse代表升序或者降序

add = lambda x,y:x+y
add(1,2) # 结果是3
lambda x, y: x*y			# 函数输入是x和y，输出是它们的积x*y
lambda:None					# 函数没有输入参数，输出是None
lambda *args: sum(args)		# 输入是任意个数参数，输出是它们的和(隐性要求输入参数必须能进行算术运算)
lambda **kwargs: 1			# 输入是任意键值对参数，输出是1

eval('1+1') 
# 结果为2。
# 将字符串当成有效的表达式来求值，并返回计算结果
# 所谓表达式就是：eval这个函数会把里面的字符串参数的引号去掉，把中间的内容当成Python的代码，eval函数会执行这段代码并且返回执行结果

```

### 2. 命名规范

| Type                       | Public             | Internal                                                     |
| -------------------------- | ------------------ | ------------------------------------------------------------ |
| Modules                    | lower_with_under   | _lower_with_under                                            |
| Packages                   | lower_with_under   |                                                              |
| Classes                    | CapWords           | _CapWords                                                    |
| Exceptions                 | CapWords           |                                                              |
| Functions                  | lower_with_under() | _lower_with_under()                                          |
| Global/Class Constants     | CAPS_WITH_UNDER    | _CAPS_WITH_UNDER                                             |
| Global/Class Variables     | lower_with_under   | _lower_with_under                                            |
| Instance Variables         | lower_with_under   | _lower_with_under (protected) or __lower_with_under (private) |
| Method Names               | lower_with_under() | _lower_with_under() (protected) or __lower_with_under() (private) |
| Function/Method Parameters | lower_with_under   |                                                              |
| Local Variables            | lower_with_under   |                                                              |

# THE END

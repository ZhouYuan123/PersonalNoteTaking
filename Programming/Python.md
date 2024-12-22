# Python

## 1. 简介与安装

​    胶水语言，背后有强大的代码库。动态语言。

​    1991年，荷兰人，吉多·范罗苏姆 (Guido van Rossum)。

​    现在版本python3不兼容前版本。 2020年python2停止更行。官方提供过渡版本python2.6 2.7

* 跨平台 
* 解释型语言
* 一种交互式语言

Python三大特点：完全面向对象 (一切皆对象)，强大标准库，大量第三方模块。

**安装python解释器**

​    官网：www.python.org

​    下载：www.python.org/downloads/release/python-381/

Files --> 下载第二个：[Windows x86-64 executable installer](https://www.python.org/ftp/python/3.8.1/python-3.8.1-amd64.exe)

安装：勾选 Add Python 3.10 to PATH --> customize installation --> disable path length limit --> dos中输入`python` 验证

**运行：**

IDLE: 开发环境。new file: 写长的代码

Python: 交互式的。(Linux中用命令ipython3打开)

Python Manuals: 官方手册。

Python module docs: 已经安装的。

**安装PyCharm**

https://www.jetbrains.com.cn/en-us/pycharm/download/?section=windows --> 下载community社区版

new project --> 自定义location --》选择Previously configured interpreter --》add interpreter --》选择System interpreter(会自动读取到环境变量指定的python.exe) --> create

打开当前项目之后，会在项目根目录出现 `.idea` 目录。保存项目相关的信息，例如: 解释器版本、项目
包含的文件等等。

home下面出现配置目录隐藏文件。

## 2. 基本语法

代码量，一般情况下是java的 1/5

🟩 **Hello World** 🟩

```python
#!/usr/bin/python
print("Hello World")

# 单行注释。
"""
没有多行注释，但是可以用三引号（单引号或者双引号）充当多行注释。
"""
```

执行：`python xxx.py` or `python3 xxx.py` （python3的命令）

**node：**脚本第一行，shebang，只对 Linux/Unix 用户适用。

`# TODO(author)` : 用于标记将要做的 (pycharm拥有TODO视图)。

`#coding:GBK` : 文档第一行申明编码类型。

🟩 **命名规范** 🟩

* 字母、下划线 和 数字 组成。

* 不能以数字开头。

代码规范：https://peps.python.org/pep-0008/

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

提示: Python 中并没有真正意义的常量，只是通过命名的约定

* 所有字母都是大写的就是常量，开发时不要轻易的修改

## 3. 数据类型

数字(number)：整数(int)，浮点数(float)，布尔(bool)，复数 (complex)。

非数字型：字符串(string)，列表(list)，元组(tuple)，集合(set)，字典(dictionary)。

**int:** 0b: 二进制。0o：八进制。0x: 十六进制。

**float:**

**bool:** True = 1, False = 0. 可以直接参与数值结算。

* 0的布尔值为False，非0布尔值为True.

**str:** 单引号和双引号只能在一行，三单引号三双引号可以在多行。

python2.x中存在 **long** 类型

```python
# 数字类型
i = 10
f = 10.5
b = True
i + f  # 20.5
i + b  # 11
f - b  # 9.5
i * f  # 105.0

# 数字类型和str不能计算
i + "10"  # error

# 转义字符
# 需要被转义的：单双引号
# \b 退格=backspace
# 字符串前面加r或者R，使转义失效。
# Unicode表规定什么字符用什么数字。UTF-8决定什么字符用几个字节。
```

**数据类型转换：**无法转化会 TypeError

`type(variable)` : 返回数据类型

`int(variable)` : 不能转小数字符串

`  float(variable)` :

`str(variable)` :

## 4. 运算符

**算术运算符 :**  先幂然后乘除再加减

`+ - * / //(整除) % **(幂运算)` 

```tex
10 / 20 = 0.5
9 // 2 = 4
2 ** 3 = 8
```

**赋值运算符：**

`a=b=c=8` ：链式赋值

`a+=30` ： 参数赋值。列表的 `+=` 调用的是`extend()`方法

`a=b,b=a` 就可以实现参数值得互换

`a,b,c=20,30,40`: 系列解包赋值

**比较运算符：**

一个变量组成：标识（id），类型，值。

`==`：比较值。

`is, is not  ` : 比较id, 类似 `id(x) == id(y)`。 python 中对 `None` 进行判断建议使用 `is`

**逻辑运算符：** `and, or, not, in, not in   `

**位运算符：** `&, |, <<, >> `

优先级：算术运算符 > 位运算符 > 比较运算符 > 布尔运算符 > 赋值运算符

## 5. 流程控制

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
# 条件表达式
x if 判断条件 else y  #返回x或者y
```

```python
while 条件表达式:
    条件执行体
else:
    条件执行体  # 循环在没有遇到break正常结束后会执行else
    
for 自定义的变量 in 可迭代的对象:
    条件执行体 
    break
    continue
else:
    条件执行体  # 循环在没有遇到break正常结束后会执行else
```

`pass` : 占一个语句位置。

🟨 **注意:** 🟨

* 代码的缩进为一个 tab 键，或者4 个空格 -- 建议使用空格
* 在Python 开发中Tab 和空格不要混用

## 6. 非数字类型

🟩 **列表** 🟩

有序，索引访问，可重复，类型可混存，动态分配内存和自动内存回收

```python
# 列表创建
lst=[] or list() #空列表
lst=['hello','world',98]
lst2=list(['hello','world',98])
lst = list(元组)
[1, 2] * 2  # [1, 2, 1, 2] 适用于字符串、列表、元组

# 查询
lst.index('hello') # 返回相同元素第一个的index，不存在抛异常 ValueError
lst.index('hello',1,3) # [1-3)之间是否存在hello
lst[N] or lst[-N] # -N从-1开始，没有索引抛异常 
len(lst)  # 列表中元素的总数
lst.count('zs')  # 统计指定数据出现的字数

# 判断
元素 in lst
元素 not in lst
[1, 2, 3] < [2, 2, 3]  # 按照元素位进行比较。如果长度不同，短的列表认为小。

# 遍历
for _ in lst:
    print(_)
for index,value in enumerate(lst):
    pass

# 增
lst.append(100)
lst.extend(lst2)  # 修改了调用这个方法的列表的内容
lst.insert(index, 100)
lst[1:] = lst2 # index1 之后的内容用新的列表替换掉

# 改
lst[1] = ""  # 超过index会数组越界error
lst[start:stop:step] # 切片原列表，不包括stop, 三个值都可以省略。step为-1，反序切。
[1, 2] + [3, 4]  # [1,2,3,4] 合并, 适用于字符串、列表、元组

# 删
lst.remove(100) # 只移除重复元素第一个，如果元素不存在 ValueError
lst.pop(index) # 删除索引位置元素，如果不存在 Index Error
lst.pop() # 删除最后一个元素
new_list = lst[1:3] # 原列表没有变化
lst[1:3] = [] # 间接删除原列表
lst.clear() # 清空
del lst[index]  # 删除指定索引位置元素
del lst # 删除变量定义 再使用undefined

# 排序
lst.sort()  # 原列表变为升序
lst.sort(reverse=True) # 降序
lst.reverse()  # 列表反转
new_list=sorted(lst) # 产生新的列表对象
new_list=sorted(lst,reverse=True) # 降序

#列表生成式 
[i for i in range(1, 10)] #后面的i都放到前面里,也可以[i*i for i in range(1, 10)]
```

🟩 **字典** 🟩

dictionary，无序，key必须是不可变序列，key不重复value可以重复，内存较大(根据key的hash值确定位置)空间换时间
```python
# 字典创建
d={} or dict() # 空字典
d={'hello':'world','zs':98}
d=dict(name='hello',age=98)
d=dict(zip(list1,list2))

# 获取
d['zs'] # KeyError
d.get('zs') # 不会报错，返回None
d.get('zs', 99) # 不存在时返回99

len(d)  # 统计键值对数量(多少对)
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
d['zs'] = 98
d.update(d1)  # d字典被更新，d1和d合并，d1中的相同的键值对会覆盖d中的

# 删 
del d['zs']  # 删除键值对
d.pop['zs']  # 删除键值对, 如果不存在 KeyError
d.clear() # 变为空字典

#字典生成式 
items = ['a','b','c']
prices = [1,2,3]
{item.upper():price for item,price in zip(items,prices)} # 以元素少的list为基准生成元素个数。
```

🟩 **元组** 🟩

有序，内置数据结构，不可变序列(每个元素本身引用不可变，引用的元素的数据可变)
```python
# 元组创建
t=() or tuple() # 空元组
t=('hello','world',98)
t2='hello','world',98
t3 = (5)  # type(t3) 是int类型
t3=('hello',) # 只有一个元素必须加逗号
t=tuple(('hello','world',98))
t = tuple(列表)

# 查询
t[N] # 没有索引抛Error
t.index('zs')
t.count('zs')
```

🟩 **集合** 🟩

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

## 7. 字符串

### 7.1 字符串处理

🟩 **判断类型 -10** 🟩

| str.方法名  |                                       |
| ----------- | ------------------------------------- |
| isspace()   | 是否只包含空白字符 (包括\t \n \r)     |
| isalpha()   | 是否由全字母组成                      |
| isalnum()   | 是否由数字和字母组成                  |
| isdecimal() | 是否全部由十进制数字组成 (1.1是False) |
| isdigit()   | 是不是数字，额外包括 `(1), \u00b2`    |
| isnumeric() | 是不是数字，额外包括 `(1), \u00b2, 汉字数字(一千零一)` |
| istitle()   | 是否每个单词的首写字母大写            |
| islower()   | 是否都是小写                          |
| isupper()   | 是否都是大写                          |
| isidentifier() | 是不是合法标识符 |

🟩 **查找和替换 -9** 🟩

```python
str = "HW"
len(str)  # 字符串长度
str.count('abc')  # str中abc出现的次数
str.startswith('abc')
str.endswith('abc')
str.index('abc')  # 找不到，ValueError
str.find('abc')  # 找不到，返回 -1
str.replace('oldString','newString' [,指定次数])  # 不会修改原有字符串的内容
str.rindex('abc')  # 最后一个指定字串, 找不到，ValueError
str.rfind('abc')  # 最后一个指定字串, 找不到，返回 -1
```

🟩 **大小写转换和对其 -8** 🟩

| str.方法名                   |                                                    |
| ---------------------------- | -------------------------------------------------- |
| capitalize()                 | 把字符串第一个字符大写                             |
| title()                      | 把字符串的每个单词首写字母大写                     |
| lower()                      |                                                    |
| upper()                      |                                                    |
| swapcase()                   | 翻转string中的大小写                               |
| ljust(width [, '指定字符'])  | 左对齐，空白处用指定字符填充。默认使用半角空格填充 |
| rjust(width [, '指定字符'])  |                                                    |
| center(width [, '指定字符']) |                                                    |

 🟩 **字符串处理 -8** 🟩

```python
'''去除空白字符'''
str = "HW"
str.strip()  #  去除字符串左右的空白字符
str.rstrip()
str.lstrip()

'''字符串拼接'''
str.split('指定分隔符' [,num])  # 默认用空格(包括/r/n/t)分割，返回列表。 num指定分割的次数
'指定拼接符'.join(lst)  # lst转为字符串用指定字符拼接
string.partition(str)  # 把字符串 string 分成一个3元素的元组(str前面, str, str后面)
string.rpartition(str)  # 类似于 partition()方法，不过是从右边开始查找
string.splitlines()  # 按照行(\r;\n; n分隔，返回一个包含各行作为元素的列表

'''字符串切片'''
# 切片后返回新的字符串。
str[start:stop:step]  # 前包括后不包括
str[2:5]  # 截取了第3-5 (index 2到4)
str[:5]  # 前五个字符的串 (index 0到4)
str[5:]  # 第六到最后 (index 5到最后)
str[5::2]  # 步长为2。
str[-1]  # 倒序索引，拿到最后一个字符
str[-2:]  # 倒序索引，拿到最后两个字符
str[2:-1]  # index 2到倒数第二
str[0::-1]  # 只截取了第一个字符
str[-1::-1]  # 反转了字符串。-1可以省略：str[::-1]

'''字符串填充'''
# zfill(宽度)右对齐，左边0填充。
n = "123"
s = n.zfill(5)  # 00123

# 字符串里的不一定需要是数字，其余字符也可以：
n = "xyz"
s = n.zfill(5)  # 00xyz

# 对于纯数字，不能用zfill，可以参考C语言中的方法：
n = 123
s = "%05d" % n  # 00123
```


```python
"-" * 5  # 拼接出字符串 '-----'
```

🟩 **格式化字符串** 🟩

```python
name = "name"
age = 18

print('%s%d' % (name, age))  # %d: 十进制 %x:十六进制
info = ('zs', 18)  # 元组类型
print('%s 的年龄是 %d' % info)

print('%10d' % 99)  # 10表示宽度, 左边8个空格 (超过就按原格式输出)
print('%010d' % 99)  # 10表示宽度, 左边8个0
print('%.3f' % 3.1415926)  # 3个小数  3.142
print('%010.3f' % 3.1415926)  # 同时设置  000003.142
print('%010.3f%%' % 3.1415926)  # %%打印%  000003.142%

print('{0}{1}{0}'.format(name,age))
print('{0:.3'.format(3.1415926)) # 3位 3.14
print('{0:.3f'.format(3.1415926)) # 3个小数 3.142
print(f'{name}{age}')

'{:>6}{:a>6}'.format('内容1','内容2')  # 右对齐。'   内容1','aaa内容2'， ^<> 分别表示中左右对齐
```

### 7.2 其他

是一个基本数据类型，不可变。

内置函数ord()获取原始值。

`'a'>'b'` : 97>98, False

`==` : 判断内容，is 判断地址。

**字符串驻留机制**

相同的字符串，指向同一个地址的条件：

1. 字符串长度为0或者1
2. 符合标识符的字符串
3. 只在编译时驻留
4. -5,256 之间的驻留

强制驻留，sys.interna(a)。 PyCharm对字符串进行了优化，会自动驻留。

**字符串编码转换**

`print(s.encode(encoding='GBK'))` : 一个中文占两个字节

`print(s.encode(encoding='UTF-8'))` : 一个中文占三个字节

`print(b.decode(encoding='UTF-8'))` : 一个中文占三个字节

## 8. 函数

### 8.1 函数

```python
def 函数名(para1, para2):
    """
    :param para1: 注释内容
    :param para2: 注释内容
    :return: 内容
    函数文档注释方式
    """
	函数封装的代码

# 需要先定义后使用
def calc(a, b):
calc(20, 10) # 位置实参   
calc(b=10, a=20); # 关键字实参   

# 只有一个返回值返回原值。
def getNum():
    return 1  # 没有返回值就是None

# 返回值是多个返回元组。
def getNum():
    return 1, 2
a, b = getNum()  # 可以使用多个变量接收结果。变量数量不对应会报错。

# 参数默认值，具有默认值的参数就叫做 缺省参数。只能在参数列表末尾。
def calc(a, b=10, c=True):
    pass
# 调用带有多个缺省参数的函数, 可以指定参数名
calc(10, c=False)

# 可变位置参数，参数个数不确定
def fun(*args):  # 接收元组
    print(args)
# 可变关键字参数
def fun1(**kwargs):  # 接收一个字典
    print(kwargs)
fun(1, 2, 3)
fun(*lst)  # 拆包传递
fun1(a=1,b=2) # {'a':1, 'b':2}
fun2(**dict)  # 拆包传递

# 参数和返回值都是传递数据的引用 (对可变类型的参数的修改会影响原数据)
```

🟩 **变量** 🟩

* 局部变量是在函数内部定义的变量，只能在函数内部使用
  * 函数执行结束后，函数内部的局部变量，会被系统回收
* 全局变量是在函数外部定义的变量，所有函数都可以使用这个变量
  * 函数内部不允许直接修改全局变量的引用 -- 使用赋值语句修改全局变量的值，会在函数内部重新定义了一个局部变量。
  * 需要用global关键字将其变为全局, 才能进行修改。
  * 全局变量名前应该增加`g_`或者`gl_`的前缀


```python
num = 1
def demo():
    global num
    num = 99

# 变量交换
a, b = (b, a)
a, b = b, a  # 等号右边是一个元组，小括号被省略了
```

### 8.2 内置函数

| 不需要import就可以使用的函数 |                                           |
| ---------------------------- | ----------------------------------------- |
| len(item)                    | 计算容器中元素个数                        |
| del(item)                    | 删除变量                                  |
| del(item[index])             | 删除元素                                  |
| max(item)                    | 返回容器中最大值。如果是字典，比较的是key |
| min(item)                    |                                           |
| cmp(item1, item2)            | 小于返回-1。python3中被移除               |
| range(stop)                  | 返回一个[0-stop)的序列，步长为1           |
| range(start,stop,step)       | 返回一个[start-stop)的序列, 步长为step    |

```python
present = input('请输入你的内容:') #input 函数
print(present)

eval('1+1')
eval("__import__('os').system('ls')")
# 返回结果2。
# 将字符串当成有效的表达式来求值，并返回计算结果
# 所谓表达式就是：eval这个函数会把里面的字符串参数的引号去掉，把中间的内容当成Python的代码，eval函数会执行这段代码并且返回执行结果

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
```

🟩 **print** 🟩

```python
print("Hello",end ="")  # 默认换行，用end参数来设置你想要的结束符号
print("Hello",end ="---")  # "Hello---"

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

## 9. 异常

程序在运行时，如果Python解释器遇到到一个错误，会停止程序的执行，并且提示一些错误信息就是异常

程序停止执行并且提示错误信息这个动作，我们通常称之为: 抛出(raise)异常

```python
try:
	执行语句
except ZeroDivisionError:
    执行语句
except (错误类型2，错误类型3):
    # 针对错误类型2 和 3，对应的代码处理
    pass
except ValueError as e:
    print(e)
except Exception as e:  # 未知错误
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

异常具有传递性。自动向上一层调用者传递。

```python
# 主动抛出异常
ex = Exception("异常信息")
raise ex
```

## 10. 面向对象

面向对象三大特性: 封装，继承和多态。

🟩 **类定义** 🟩

类名大驼峰命令法

```python
class Student:
    a = 'a' # 类属性

    def eat(self): # 实例方法， 类之外称为函数，类之内叫作方法。
        pass
    def eat(self, 参数列表):  # self:指向当前对象的引用
        pass

    def __init__(self,name,age): # 初始化方法
        self.name = name # self.name 实例属性
        self.__age = age  # 两个下划线伪私有属性和伪私有方法，只能在内部访问
        Tool.a = 'b'  # 修改类属性的值

    @classmethod
    def cm(cls): # 类方法，调用 Student.cm() 调用不需要传参。cls 当前类的引用
         cls.name = name  # 类属性

    @staticmethod
    def sm(): # 静态方法。使用场景：不需要访问类属性，也不需要访问对象属性的时候
        pass
```

🟩 **对象创建** 🟩

```python
# 实例对象
对象变量 = 类名()
stu = Student('zs', 20)
print(stu) # 实例对象
print(Student) # 类对象
stu.age  # 如果在运行时，没有找到属性，程序会报错
stu.eat() # 方法调用
Student.eat(stu) # 方法调用

stu.gender='女' # 动态绑定
def show():
    pass
stu.show = show # 动态绑定方法

# 强行访问私有属性或私有方法
stu._类名__变量名

dir(stu)  # 返回对象所有属性和方法
id(stu)  # 返回变量指向的数据的地址

# 类对象 类是一个特殊的对象，内存中只有一份
类名.类属性
对象.类属性 # (不推荐)， 先找实例属性，再找类属性
对象.类属性 = 'a'  # 只会新加一个实例属性

# 单例模式. 重写__new__方法
class Student(object):
    instance = None
    def __new__(cls, *args, **kwargs):
        # 1.判断类属性是否是空对象
        if cls.instance is None
            # 2. 为对象分配空间
            cls.instance = super().__new__(cls)
        # 3. 返回对象的引用
        return cls.instance

    # 记录是否执行过初始化动作
    init_flag = False
    def __init__(self):
        # 判断是否执行过初始化动作
        if Student.init_flag:
            return
        Student.init_flag = True
```

| 内置属性或方法     |                                                        |
| ------------------ | ------------------------------------------------------ |
| \_\_new\_\_        | 为分配内存空间，返回对象引用。创建对象时，会被自动调用 |
| \_\_init\_\_       | 为对象的属性设置初始值。对象被初始化时，会被自动调用,  |
| \_\_del\_\_        | 对象被从内存中销毁前，会被自动调用方法                 |
| \_\_str\_\_        | 返回对象的描述信息，print 函数输出使用                 |
| \_\_dict\_\_       | 实例对象、类对象属性的字典。                           |
| \_\_class\_\_      | 对象所属的类。                                         |
| \_\_bases\_\_      | 父类类型的元组。                                       |
| \_\_base_\_        | 第一个父类。                                           |
| \_\_subclasses\_\_ | 子类类型的列表。                                       |
| \_\_add\_\_()      | 加号操作底层调用的方法                                 |
| \_\_len\_\_()      | 内置方法len(lst)调用的方法                             |

🟩 **继承** 🟩

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
        Person.__init__(self)
        self.stu_no=stu_no
    def info(self): # 方法重写
        pass
	def __str__(self): # 重写
        return '我的名字是{0}'.format(self.name)

# MRO是 method resolution order，主要用于在多继承时判断方法、属性的调用路径
print(Student.__mro__)
```

动态语言的多态，只关心行为。

🟩 **新式类与旧式(经典)类** 🟩

* 新式类: 以object为基类的类，推荐使用 (Python 3.x)
* 经典类: 不以 object 为基类的类，不推荐使用 (Python 2.x)
* 新式类和经典类在多继承时-- 会影响到方法的搜索顺序

```python
# 为了保证Python 2.x 和 Pthon 3x 兼容!在定义类时，如果没有父类，建议统一继承自 object
class 类名(object):
    pass
```

## 11. 模块

一个 .py 文件就是一个模块。每一个文件都应该是可以被导入的。

```python
import 模块名称 [as 别名]  # 推荐，每次导入一个模块，独占一行
模块名称.变量
模块名称.函数

# 使用了from导入的可以直接使用。同名的时候后面的覆盖前面。可以通过取不同的别名解决。
from 模块名称 import 函数/变量/类
from 模块名称 import *  # 导入所有工具

# 优先搜索当前目录指定模块名的文件，如果有就直接导入。如果没有，再搜索系统目录
# Python 中每一个模块都有一个内置属性 __file__可以查看模块的完整路径
import random
print(random.__file__)
```

| 模块内置属性 |                                                              |
| ------------ | ------------------------------------------------------------ |
| \_\_file\_\_ |                                                              |
| \_\_name_\_  | 直接执行该模块时，就是：\_\_main\_\_ 如果是被其他文件导入的\_\_name_\_就是模块名 |
|              |                                                              |

```python
if __name__ == '__main__'
	pass # 只有当前模块作为主程序运行才会执行
```

🟩 **常用内置模块** 🟩

```python
# 关键字
import keyword
print(keyword.kwlist)

# 随机数
import random
random.randint(a，b)  # 返回[a，b]之间的整数，包含a和b

# copy
import copy
obj2 = copy.copy(obj1) # 浅拷贝
obj3 = copy.deepcopy(obj1) # 深拷贝
```

| 常用内置模块 |                                                              |
| ------------ | ------------------------------------------------------------ |
| sys          | sys.getsizeof(a)                                             |
| time         | time.time()： 秒<br />time.localtime(time.time()) : 转成本地时间 |
| urllib       | .request.urlopen('http://www.baidu.com')                     |
| re           | 正则                                                         |
| math         | .pi : 圆周率                                                 |
| decimal      |                                                              |

🟩 **第三方模块** 🟩

`[sudo ]pip install 模块名 `： 在线安装， DOS窗口中执行。

`[sudo ]pip uninstall 模块名 `: 卸载

python3.x : `[sudo ]pip3 install 模块名 ` ，`[sudo ]pip3 uninstall 模块名 `

🟩 **包（Package）** 🟩

* 包是一个包含多个模块的特殊目录
* 目录下有一个特殊的文件\_\_init\_\_.py
* 包名的命名方 和变量名一致，小写字母 + 下划线

在模块所在文件夹右击 --> Mark Directory as  Sources Root

new python package操作 => 默认包含\_\_int\_\_.py文件

PyCharm导入自定义模块：(导入之后会自动创建缓存文件pyc)

```python
# 要在外界使用包中的模块，需要在__int__.py中指定对外界提供的模块列表
# 从当前目录 导入模块列表
from . import send_message
from . import receive_message

# 外界 import 包名
```

🟩 **发布与安装模块** 🟩

1. 创建setup.py （略）
2. 构建模块（略）
3. 生成发布压缩包（略）

安装：`sudo python3 setup.py install`

卸载：直接从安装目录下，把安装模块的 目录 删除就可以（`.__file__` 查找目录）

`$ cd /usr/local/lib/python3.5/dist-packages/`

`$ sudo rm -r 刚刚安装的*`

## 12. 编码与持久化

文本文件: 可以使用文本编辑软件查看, 本质上还是二进制文件。

二进制文件: 不能使用文本编辑软件查看。

Python的解释器使用的是Unicode内存，.py文件在磁盘上使用UTF-8存储外存。

```python
# coding:gbk #文件首行指定编码格式
# 或者
# *-* coding:utf8 *-*
# 引号前面的u告诉解释器这是一个utf8编码格式的字符串
hello_str = u"hello世界"

file = open('a.txt', 'a')
file.write('Python')
file.writelines(['Python','java']) # 同一行
# print('内容', file=file)
file.close()

file = open('a.txt', 'r')
text = file.read()  # 一次性读出所有内容(str), 文件指针移动到文件末尾, 再次调用read()返回空
file.read(n)  # n:字符个数
file.readline()  # 每读取一行的未尾已经有了一个'\n'
file.readlines() # 返回列表
file.seek(2) # 跳过字节的个数 seek(offset[,whence]) offset:负数反向。whence：0，从开头开始计算。1：从当前位置计算。2：从文件尾开始计算。
file.tell() # 告诉指针当前位置
file.flush()
file.close()

#with 语句, 不需要手动关闭
with open('a.txt', 'r') as file: # file 文件重写了上下文管理器
    pass 
```

| 打开方式 |                                                              |
| -------- | ------------------------------------------------------------ |
| r        | 只读。如果文件不存在，会抛出异常                             |
| w        | 创建或者覆盖                                                 |
| a        | 创建或者追加                                                 |
| r+       | 以读写方式打开文件。文件的指针将会放在文件的开头。如果文件不存在，抛出异常。 |
| w+       | 以读写方式打开文件。如果文件存在会被覆盖。如果文件不存在，创建新文件。 |
| a+       | 以读写方式打开文件。如果该文件已存在，文件指针将会放在文件的结尾。如果文件不存在，创建新文件进行写入。 |
| b        | 以二进制打开，rb or wb                                       |

## 13. os

```python
import os
os.system('notepad.exe') # 打开记事本
os.system('calc.exe') # 打开计算器
os.startfile('路径') # 打开程序
```

| os.                                                  |                            |
| ---------------------------------------------------- | -------------------------- |
| rename(源文件名，目标文件名)                         | 重命名文件                 |
| remove(文件名)                                       | 删除文件                   |
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
| isdir(path)      | 是否是一个目录     |

# THE END

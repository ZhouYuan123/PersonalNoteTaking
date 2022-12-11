# Python

## 1. 简介

​    胶水语言，背后有强大的代码库。
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

## 3. 转义字符

\b，退格=backspace
字符串前面加r或者R，使转义失效。

Unicode表规定什么字符用什么数字。UTF-8决定什么字符用几个字节。

## 4. 数据类型

**int:** 
0b: 二进制。0o：八进制。0x: 十六进制。

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
for _ in lst:
    print(_)

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

|                                                              |                                          |
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
| isdecimal()                                                  | 是否全部由十进制数字组成                 |
| isnumeric()                                                  | 是否全部由数字组成 （123四）true         |
| isalnum()                                                    | 是否由数字和字母组成                     |
| replace('Pythoin', 'Java')<br />replace('Pythoin', 'Java', 指定次数) | 用Java替换Python                         |
| '\|'.join(lst)，'*'.join(t)，                                | lst转为字符串用指定字符拼接              |

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

## NOTE：

### 1. 内置函数

```python
print("Hello",end ="") # 默认换行，用end参数来设置你想要的结束符号
range(stop) # 返回一个[0-stop)的序列，步长为1
range(start,stop,step)
```

# THE END

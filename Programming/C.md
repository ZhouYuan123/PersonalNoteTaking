# C 语言

## 1. 简介

助记符，汇编语言。

计算机语言：人和计算机交流的语言。

1972年上线，面向过程，由B语言发展而来，贝尔实验室。

国际标准：C89/C90

广泛应用于底层软件开发(OS, 驱动)。

## 2. 数据类型

| 类型	   |长度(Byte)      |
| --------- | ---- |
| char       | 1 |
| short | 2 |
| int  | 4 |
| long      | 4 (C语言标准：sizeof(long)>=sizeof(int) 就可以了) |
| long long | 8 |
| float     | 4 |
| double    | 8 |

## NOTE:

### 1. visual studio快捷键
| Ctrl + F5 | 编译+链接+运行 |
| --------- | -------------- |
| Ctrl + L  | 删除一行       |
|           |                |
|           |                |
### 2. 内置函数
| printf("Hello World");<br />printf(“%d\n”, sizeof(a)); | <stdio.h>, <br />%d：整数<br />%f: float<br />%lf: double |
| --------- | -------------- |
| scanf(“%d %d”，&a, &b); | 输入函数，scanf_s是VS自带的 |
|           |                |
|           |                |

## THE END

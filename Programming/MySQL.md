# MySQL

## 1. 简介

开放源代码的关系型数据库管理系统。支持千万级别数据量的存储。1995年瑞典MySQL AB (创始人Michael Widenius) 公司开发。MySQL 的创造者担心MySQL有闭源的风险，因此创建了 MySQL的分支项目 MariaDB。

发布之后语法几乎没有变化。

* SQL-86、SQL-89、SQL:2003、SQL:2008、SQL:2011和SQL:2016
* SQL92 (SQL-2标准)、SQL99 (SQL-3标准)

<font color=green>**安装与配置**</font>

官网：www.mysql.com

Downloads --> 企业版/社区版(MySQL Community(GPL) Downloads) --> MySQL Community Server --> MySQL Installer MSI Go to Download Page --> 非web版本

Install --> custom --> select MySQL Server 8.0.34 - X64 to right --> select the right MySQL Server 8.0.34 - X64 to select advanced options to modify the path (server folder, data folder) --> execute --> config type: development computer --> 取消开机自启动

环境变量配置：bin目录加入到path

查看字符集：登录mysql之后，
show variables like 'character\_%';
show variables like 'collation\_%';

修改字符集：安装的data路径/my.ini 中添加

```	bash
# 5.7默认是Latin, 8.0默认是utf8
default-character-set=utf8

character-set-server=utf8
collation-server=utf8_general_ci
```

## 2. 数据库

`net start mysql服务名` ：启动MySQL服务。

DB: 数据库 (Database)

* 即存储数据的“仓库”，其本质是一个文件系统。它保存了一系列有组织的数据

DBMS: 数据库管理系统 (Database Management System)

* 是一种操纵和管理数据库的大型软件，用于建立、使用和维护数据库，对数据库进行统一管理和控制。用户通过数据库管理系统访问数据库中表内的数据。
* RDBMS： 把复杂的数据结构归结为简单的 二元关系
* 非RDBMS，基于键值对存储数据，不需要经过SQL层的解析性能非常高。同时，通过减少不常用的功能，进一步提高性能。

<font color=green>**其他DBMS**</font>

**0racle**

1979 年，0racle 2诞生，它是第一个商用的 RDBMS(关系型数据库管理系统)。随着 0racle 软件的名气越来越大，公司也改名叫oracle 公司。

2008年，SUN以10亿美金收购MySQL。

2009年，总计74亿美金收购SUN。

2016年，MySQL8.0推出。

**SQL Server**

SQL Server 是微软开发的大型商业数据库，诞生于 1989 年。

**DB2**

IBM公司的数据库产品,收费的。常应用在银行系统中。

**PostgreSQL**

PostgresQL 的稳定性极强，最符合SQL标准，开放源码，具备商业级DBMS质量。PG对数据量大的文本以及SQL处理较快。

**SQLite**

嵌入式的小型数据库，应用在手机端。零配置，SQlite3不用安装，不用配置，不用启动，关闭或者配置数据库实例。当系统崩溃后不用做任何恢复操作，再下次使用数据库的时候自动恢复。

**informix**
IBM公司出品，取自Information 和Unix的结合，它是第一个被移植到Linux上的商业数据库产品。仅运行于unix/linux平台，命令行操作。性能较高，支持集群，适应于安全性要求极高的系统，尤其是银行，证券系统的应用。

* 键值型数据库: Redis
* 文档型数据库: MongoDB
* 搜索引擎数据库: ES、Solr
* 列式数据库: HBase
* 图形数据库: InfoGrid

**DB-Engines Ranking:** https://db-engines.com/en/ranking

## 3. SQL

SQL: 结构化查询语言 (Structured Query Language)

* 专门用来与数据库通信的语言。

![](../imgs/MySQL/db.jpg)



1974 年，IBM 研究员发布了一篇揭开数据库技术的论文《SEQUEL：一门结构化的英语查询语言》，直到今天这门结构化的查询语言并没有太大的变化。SQL92, SQL99两个标准。

**命令行执行已有sql：** source d:\mysqldb .sql

**连接数据库：**

```bash
mysql -u用户名 -p密码 # windows
mysql -u用户名 -p密码 -h主机名 或 localhost # Linux
```

### 3.1 规则规范

**基本规则**

1. SQL可以写在一行或者多行。为了提高可读性，各子句分行写，必要时使用缩进。
2. 每条命令以 `;` 或 \\g 或 \\G结束
3. 关键字不能被缩写也不能分行

**规范**

MySQL 在 Windows 环境下是大小写不敏感的，MySQL 在 Linux 环境下是大小写敏感的

* 数据库名、表名、表别名、字段名、字段别名等都小写
* SQL 关键字、函数名、绑定变量等都大写

```sql
单行注释: # 注释文字(MySQL特有的方式)
单行注释:-- 注释文字(--后面必须包含一个空格。)
多行注释: /*注释文宁 */
```

### 3.2 SQL分类

* DDL (Data Definition Languages 数据定义语言)

这些语句定义了不同的数据库、表、视图、索引等数据库对象，还可以用来创建、删除、修改数据库和数据表的结构。主要的语句关键字包括 CREATE 、DROP、ALTER、RENAME 等

* DML (Data Manipulation Languages 数据操作语言)

用于添加、删除、更新和查询数据库记录，并检查数据完整性。主要的语句关键字包括 INSERT、DELETE、UPDATE、SELECT 等

* DCL (Data Control Languages 数据控制语言)

用于定义数据库、表、字段、用户的访问权限和安全级别。
主要的语句关键字包括GRANT、REVOKE、COMMIT、ROLLBACK、SAVEPOINT 等

( SELECT会单独拿出来叫DQL 数据查询语言 )

( COMMIT、ROLLBACK有可能会单独拿出来叫做TCL Transaction Control Language，事务控制语言)

### 3.3 DQL

```mysql
-- 显示表结构
DESCRIBE 表名;
DESC 表名;
```

#### 3.3.1 select

🟦 **SELECT** 🟦

```mysql
SELECT 1 + 1, 3*2 [DUAL]; # DUAL 是伪表
-- 返回
+-----+
| 1+1 |
+-----+
|   2 |
+-----+

-- 别名, 使用双引号
SELECT 列名1 别名1,列名2 别名2
FROM 表名;
SELECT 列名1,列名2 AS 别名2
FROM 表名;
SELECT 列名1 AS 别名1,列名2 "别名2"
FROM 表名;

-- 去除重复行
SELECT DISTINCT 列名1
FROM 表名;
SELECT DISTINCT 列名1,列名2 # 两个都不重复才会去重
FROM 表名;
SELECT 列名1,DISTINCT 列名2 # 报错
FROM 表名;

-- 着重号 (反引号) 跟关键字重名的时候使用。(oracle不支持着重号)
SELECT * FROM `order`;

-- 查询常数，每一行数据都会添加
SELECT 列名1,列名2,'abc'
FROM 表名;
```

🟦 **WHERE** 🟦

```mysql
SELECT *
FROM 表名
WHERE last_name = 'King'; # 过滤.
-- 1. 内容区分大小写，但是MySQL不严谨，依旧可以查询出，oracle无法查询出。
-- 2. MySQL字段值可以双引号，但oracle报错
```

🟦 **运算符** 🟦

```mysql
-- 算术运算符
SELECT A + B FROM DUAL;
# 1.0 + 1 = 2.0, 结果是浮点数。
# 1 + '1' = 2, MySQL中+没有字符串拼接这个功能
# 100 + 'a' = 100, 不会转化a
# 100 + NULL = NULL, NULL值参与运算结果为NULL

SELECT A - B FROM DUAL;
SELECT A * B FROM DUAL;
SELECT 列名1 * 12 '别名1' # 查出列1的数据的12倍
FROM 表名;

SELECT A/B # 或者 SELECT A DIV B
# 100 DIV 0 = NULL
SELECT A % B # 或者 SELECT A MOD B

-- 比较运算符
=
SELECT 1 = 2 FROM DUAL; 	# 返回0代表false
SELECT 1 = '1' FROM DUAL;	# 1, 隐式类型转换
SELECT 1 = 'a' FROM DUAL;	# 0, 如果字符串转换成数值不成功，就是0
SELECT 0 = 'a' FROM DUAL;	# 1
SELECT 'a' = 'a' FROM DUAL;	# 1, 不需要进行隐式类型转换
# 100 = NULL = NULL, NULL值参与运算结果为NULL
# NULL = NULL = NULL, NULL值参与运算结果为NULL

<=>
# 安全等于，没有NULL参与时和 = 一样
# 100 = NULL = 0
# NULL = NULL = 1

<> # 不等于
!= # 不等于

IS NULL, IS NOT NULL, ISNULL
... WHERE 列名 IS NULL;	#
... WHERE ISNULL(列名);	#

LEAST('a','b','c'); # 最小的
GREATEST('a','b','c'); # 最大的

WHERE salary BETWEEN 6000 AND 8000; # 包括6000和8000, 必须前小后大
WHERE salary NOT BETWEEN 6000 AND 8000;
WHERE salary < 6000 OR salary > 8000;
WHERE salary [NOT] IN (6000, 7000, 8000);
WHERE last_name LIKE '%a%';	# 模糊查询，且忽略了大小写。 LIKE 'a%':查询以a开头的。
WHERE last_name LIKE '_a%';	# 查询第二个字符是a的。_代表一个不确定的字符。
WHERE last_name LIKE '\_$_a%';	# \和$都可以表示转义
SELECT
'shkstart' REGEXP '^shk',
'shkstart' REGEXP 't$',
'shkstart' REGEXP 'hk'
'shkstart' REGEXP '[k]' # 包含k
FROM DUAL;	# 1,1,1 或者使用RLIKE

-- 逻辑运算符
# AND 优先级会高于 OR
```

| 运算符     | 用作     | 示例                              |
| ---------- | -------- | --------------------------------- |
| NOT 或 !   | 逻辑非   | SELECT NOT A                      |
| AND 或 &&  | 逻辑与   | SELECT A AND B<br />SELECT A && B |
| OR 或 \|\| | 逻辑或   | SELECT A OR B<br />SELECT A  B    |
| XOR        | 逻辑异或 | SELECT A XOR B                    |

![](../imgs/MySQL/operator_priority.jpg)

```mysql
-- 位运算符
SELECT A & B;
SELECT A | B;
SELECT A ^ B;
SELECT ~ A; # 按位取反
SELECT A >> 2;
SELECT B << 2;
```

🟦 **排序** 🟦

```mysql
-- 默认按照插入顺序
SELECT salary * 12 abc
FROM DUAL
ORDER BY abc ASC; # 默认就是升序，DESC降序
# 🟥 WHERE 后面不可以使用SELECT中的别名，ORDER BY是可以的

-- 二级排序
ORDER BY a ASC, b DESC;
ORDER BY a, b DESC;
```
🟦 **分页** 🟦

```mysql
SELECT a
FROM DUAL
LIMIT 0, 20; # 偏移位置，偏移量。第一条开始，显示20条。

SELECT a
FROM DUAL
WHERE salary > 6000
ORDER BY salary DESC
LIMIT 0, 10; # LIMIT 10; 默认就是从偏移量0开始。
# LIMIT 10 OFFSET 0; 8.0新特性 偏移量, 偏移位置

-- 其他数据库
# SQL Server 和 Access : TOP
SELECT TOP 5 name, hp_max FROM heros ORDER BY hp_max DESC
# DB2 : FETCH FIRST 5 ROWS ONLY
SELECT name, hp_max FROM heros ORDER BY hp_max DESC FETCH FIRST 5 ROWS ONLY
# Oracle : ROWNUM
SELECT rownum, last_name, salary FROM employees WHERE rownum < 5 ORDER BY salary DESC;
```

#### 3.3.2 多表查询

笛卡尔积错误 —— 缺少了多表连接的条件，出现n*m 条数据。CROSS JOIN

![](../imgs/MySQL/multi_table.jpg)

**job_grades表**

| grade_level | lowest_sal | highest_sal |
| ----------- | ---------- | ----------- |
| A           | 1000       | 2999        |
| B           | 3000       | 5999        |
| C           | 6000       | 9999        |
| D           | 10000      | 14999       |

```mysql
--
SELECT employee_id, department_name
FROM employees, departments
# 两个表的连接条件
WHERE employees.`department_id` = departments.`department_id`;

-- 如果查询语句中出现了多个表中都存在的字段，则必须指明此字段所在的表。
-- 从SQL优化的角度，建议多表查询时，每个字段前都指明其所在的表

-- 可以给表起别名 一旦在SELECT或WHERE中使用表名的话，则必须使用表的别名，而不能再使用表的原名
SELECT emp.employee_id, dept.department_name
FROM employees emp, departments dept
WHERE emp.`department_id` = dept.`department_id`;
```

🟩 **等值连接 vs 非等值连接** 🟩

```mysql
-- 查询出所在等级 ABCD
SELECT last_name,salary,grade_level
FROM employees e,job_grades j
WHERE e.`salary` BETWEEN j.`lowest_sal` AND j.`highest_sal`; # 非等值连接
```

🟩 **自连接 vs 非自连接** 🟩

```mysql
-- 查询员工id,员工姓名及其管理者的id和姓名 (两者在同一个表中)
SELECT emp.employee_id, emp.last_name, mgr.employee_id,mgr.last_name
FROM employees emp, employees mgr
WHERE emp.`manager_id` = mgr.`employee_id`; # 自连接
```

🟩 **内连接 vs 外连接** 🟩

内连接: 合并具有同一列的两个以上的表的行，结果集中不包含一个表与另一个表不匹配的行。

外连接: 合并具有同一列的两个以上的表的行，结果集中除了包含一个表与另一个表匹配的行之外, 还查询到了左表 或 右表中不匹配的行。(查询所有肯定是一个外连接)

```mysql
SELECT employee_id, department_name
FROM employees e, departments d
WHERE e.`department_id` = d.`department_id`;

-- SQL92 实现外连接：使用 + (MySQL 不支持这种写法)
SELECT employee_id, department_name
FROM employees e, departments d
WHERE e.`department_id` = d.`department_id`(+); # 左外连接 (注意不是右, 左边多，右边写加号)

-- SQL99 实现外连接：使用 JOIN ...ON
-- 内连接
SELECT employee_id, department_name
FROM employees e [INNER] JOIN departments d
ON e.`department_id` = d.`department_id`; # 继续加表继续加 JOIN ...ON
-- 外连接
SELECT employee_id, department_name
FROM employees e LEFT [OUTER] JOIN departments d # 左外连接 (左表全)
ON e.`department_id` = d.`department_id`;
SELECT employee_id, department_name
FROM employees e RIGHT [OUTER] JOIN departments d # 右外连接 (右表全)
ON e.`department_id` = d.`department_id`;
```




# MySQL

## 1. 简介

开放源代码的关系型数据库管理系统。1995年瑞典MySQL AB (创始人Michael Widenius) 公司开发。MySQL 的创造者担心MySQL有闭源的风险，因此创建了 MySQL的分支项目 MariaDB。

E-R (entity-relationship，实体-联系)模型。

DB: 数据库 (Database)

* 即存储数据的“仓库”，其本质是一个文件系统。它保存了一系列有组织的数据

DBMS: 数据库管理系统 (Database Management System)

* 是一种操纵和管理数据库的大型软件，用于建立、使用和维护数据库，对数据库进行统一管理和控制。用户通过数据库管理系统访问数据库中表内的数据。
* RDBMS： 把复杂的数据结构归结为简单的 二元关系
* 非RDBMS，基于键值对存储数据，不需要经过SQL层的解析性能非常高。同时，通过减少不常用的功能，进一步提高性能。

SQL: 结构化查询语言 (Structured Query Language)

* 专门用来与数据库通信的语言。

![](../imgs/MySQL/db.jpg)

DB-Engines Ranking: https://db-engines.com/en/ranking

**0racle**

1979 年，0racle 2诞生，它是第一个商用的 RDBMS(关系型数据库管理系统)。随着 0racle 软件的名气越来越大，公司也改名叫oracle 公司。

2008年，SUN以10亿美金收购MySQL。

2009年，总计74亿美金收购SUN。

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

## 2. 安装与配置

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

# Java Virtual Machine

## 1. 概述

JVM运行字节码文件, 二进制字节码的运行环境。

编译成字节码文件的语言：Kotlin, Clojure, Groovy, Scala, Jython, JRuby, JavaScript

虚拟机可以分为 **系统虚拟机** 和 **程序虚拟机** 。

> ​	大名鼎鼎的Visual Box，VMware就属于系统虚拟机，它们完全是对物理计算机的仿真，提供了一个可运行完整操作系统的软件平台。
>
> ​	程序虚拟机的典型代表就是Java虚拟机，它专门为执行单个计算机程序而设计，在Java虚拟机中执行的指令我们称为Java字节码指令。

### 1.1 历史

**Sun Classic VM**

早在1996年Javal.0版本的时候，Sun公司发布了一款名为Sun classicVM的Java虚拟机，它同时也是世界上第一款商用Java虚拟机，JDK1.4时完全被淘汰。

这款虚拟机内部只提供解释器。

如果使用JIT编译器，就需要进行外挂。但是一旦使用了JIT编译器，JIT就会接管虚拟机的执行系统。解释器就不再工作。解释器和编译器不能配合工作。

现在hotspot内置了此虚拟机。

**Exact VM**

为了解决上一个虚拟机问题，idk1.2时，sun提供了此虚拟机。

Exact Memory Management:准确式内存管理

> 也可以叫Non-Conservative/Accurate Memory Management
>
> 虚拟机可以知道内存中某个位置的数据具体是什么类型

具备现代高性能虚拟机的雏形

> 热点探测
>
> 编译器与解释器混合工作模式

只在Solaris平台短暂使用，其他平台上还是classic vm

> 英雄气短，终被Hotspot虚拟机替换

**SUN公司的 HotSpot VM**

HotSpot历史

> 最初由一家名为“Longview Technologies”的小公司设计
>
> 1997年，此公司被sun收购;
>
> 2009年，sun公司被甲骨文收购
>
> JDK1.3时，HotSpot VM成为默认虚拟机

目前Hotspot占有绝对的市场地位，称霸武林。

> 不管是现在仍在广泛使用的JDK6，还是使用比例较多的JDK8中，默认的虚拟机都是HotSpot
>
> Sun/oracle JDK 和 OpenJDK的默认虚拟机
>
> 因此本课程中默认介绍的虚拟机都是HotSpot，相关机制也主要是指HotSpot的GC机制。(比如其他两个商用虚拟机都没有方法区的概念)

从服务器、桌面到移动端、嵌入式都有应用。

名称中的Hotspot指的就是它的热点代码探测技术。

> 通过计数器找到最具编译价值代码，触发即时编译或栈上替换
>
> 通过编译器与解释器协同工作，在最优化的程序响应时间与最佳执行性能中取得平衡

**BEA 的 JRockit**

专注于服务器端应用

>它可以不太关注程序启动速度，因此JRockit内部不包含解析器实现，全部代码都靠即时编译器编译后执行。

大量的行业基准测试显示，JRockit JVM是世界上最快的JVM。

> 使用JRockit产品，客户已经体验到了显著的性能提高(一些超过了70% )和硬件成本的减少(达50%)

优势:全面的Java运行时解决方案组合

> JRockit面向延迟敏感型应用的解决方案JRockit Real Time提供以毫秒或微秒级的JVM响应时间，适合财务、军事指挥、电信网络的需要
>
> MissionControl服务套件，它是一组以极低的开销来监控、管理和分析生产环境中的应用程序的工具。

2008年，BEA被Oracle收购。

oracle表达了整合两大优秀虚拟机的工作，大致在JDK 8中完成。整合的方式是在HotSpot的基础上，移植JRockit的优秀特性。

高斯林:目前就职于谷歌，研究人工智能和水下机器人

**IBM的J9**

全称: IBM Technology for Java Virtual Machine，简称IT4J，内部代号: J9

市场定位与HotSpot接近，服务器端、桌面应用、嵌入式等多用途VM

广泛用于IBM的各种Java产品。

目前，有影响力的三大商用虚拟机之一，也号称是世界上最快的Java虚拟机。

2017年左右，IBM发布了开源J9 VM，命名为OpenJ9，交给Eclipse基金会管理，也称为 Eclipse openJ9

### 1.2 指令集

Java编译器输入的指令流基本上是一种基于栈的指令集架构。

> 基于栈式架构的特点
>
> 1. 设计和实现更简单，适用于<font color=black>**资源受限的系统**</font>
> 2. 避开了寄存器的分配难题: 使用零地址指令方式分配。
> 3. 指令流中的指令大部分是零地址指令，其执行过程依赖于操作栈。<font color=black> **指令集更小**</font>, 编译器容易实现。
> 4. 不需要硬件支持，可移植性更好，<font color=black> **更好实现跨平台** </font>
>
> 基于寄存器架构的特点
>
> 1. 典型的应用是x86的二进制指令集:比如传统的PC以及Android的Davlik虚拟机。
> 2. 指令集架构则完全依赖硬件，可移植性差。
> 3. <font color=black> **性能优秀和执行更高效** </font>
> 4. 花费<font color=black> **更少的指令** </font>去完成一项操作。
> 5. 在大部分情况下，基于寄存器架构的指令集往往都以一地址指令、二地址指令和三地址指令为主，而基于栈式架构的指令集却是以零地址指令为主。

### 1.3 生命周期

**虚拟机的启动**

Java虚拟机的启动是通过引导类加载器(bootstrap class loader)创建个初始类(initial class)来完成的，这个类是由虚拟机的具体实现指定的。

**虚拟机的执行**

一个运行中的Java虚拟机有着一个清晰的任务: 执行Java程序。

程序开始执行时他才运行，程序结束时他就停止。

执行一个所谓的Java程序的时候，真真正正在执行的是一个叫做Java虚拟机的进程。

**虚拟机的退出**

* 程序正常执行结束

* 程序在执行过程中遇到了异常或错误而异常终止
* 由于操作系统出现错误而导致Java虚拟机进程终止
* 某线程调用Runtime类或System类的exit方法，或 Runtime类的halt方法，并且Java安全管理器也允许这次exit或halt操作。
* 除此之外，JNI (Java Native Interface)规范描述了用JNIInvocation API来加载或卸载 Java虚拟机时，Java虚拟机的退出情况

## 2. 字节码与类加载

## 3. 内存与垃圾回收

## 4. 性能监控与调优

## 5. 大厂面试
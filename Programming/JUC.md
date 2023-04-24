# Java Util Concurrent

## 1. 进程与线程

**程序：** program。为完成特定任务，用某种语言编写的一组指令的集合。即指一段静态的代码，静态对象。

**进程：** process。进程就可以视为程序的一个实例。是程序的一次执行过程，或是正在运行的一个程序。是一个动态过程：生命周期。

**线程：** thread。是一个程序内部的一条执行路径。

> 作为调度和执行的单位，每个线程拥有独立的运行栈和程序计数器(pc)。
>
> 一个进程中的多个线程共享相同的内存单元。

同步: 需要等待结果返回，才能继续运行。

异步: 不需要等待结果返回，就能继续运行。

### 1.1 创建

```java
extends Thread{
    @Override
	run(){
        // 重写run方法，然后 start()调用
        // 一个线程只能start()一次。
        Thread.currentThread().getName();
    }
}

implements Runnable{
    @Override
	run(){
        // 重写run方法，然后new Thread(this).start()调用
    }
}
```

### 1.2 方法


| 方法                         |                                                 |
| ---------------------------- | ----------------------------------------------- |
| getPriority();setPriority(); | MAX_PRIORITY: 10MIN_PRIORITY: 1NORM_PRIORITY: 5 |
|                              |                                                 |
|                              |                                                 |

# NOTE

1. windows下CPU时间片约为 15 ms.
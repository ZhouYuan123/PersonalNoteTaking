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

## 2. 创建

```java
// 方法一，直接使用Thread
Thread t = new Thread("线程名"){
	public void run(){
       // 要执行的任务
    }
}
// 启动线程
t.start();
// 例如：
extends Thread{
    @Override
	run(){
        // 重写run方法，然后 start()调用
        // 一个线程只能start()一次。
        Thread.currentThread().getName();
    }
}
// 方法二，使用Runnable
Runnable runnable = new Runnable() {
    public void run(){
        // 要执行的任务
    }
}
Thread t = new Thread( runnable ); // this.target = runnable
// 启动线程
t.start();
// 例如：
implements Runnable{
    @Override
	run(){
        // 重写run方法，然后new Thread(this).start()调用
    }
}

// Thread 源码
@Override
public void run() {
    if (target != null) {
        target.run();
    }
}

// 方法三，FutureTask 配合Thread。FutureTask能够接收Callable 类型的参数，用来处理有返回结果的情况。
FutureTask<Integer> task = new FutureTask<>(new Callable<Integer>(){
	@Override
	public Integer call() throws Exception{
        Thread.sleep(2000);
		return 100;
    }
}
Thread t1 = new Thread(task, "t1");
t1.start();
Integer result = task.get(); // 等待线程结果的返回。
```

## 3. 查看

windows：

`tasklist | findstr java` ，`jps` , `taskkill /F /PID 123456`

Linux:

`ps -ef | grep java `  , `jps` :  查看所有Java进程。

`top -H -p pid` ，`jstack pid` : 查看进程中的线程。

`jconsole` : 查看进程中的线程 (图形化)。

## 4. 运行原理

<font color=blue>**== 栈与栈帧 ==**</font>

Java Virtual Machine Stacks (Java 虚拟机栈)

每个线程启动后，虚拟机就会为其分配一块栈内存。

每个栈由多个栈帧(Frame)组成，对应着每次方法调用时所占用的内存。

每个线程只能有一个活动栈帧，对应着当前正在执行的那个方法。

栈：

>程序计数器
>
>栈帧：
>
>>局部变量表
>>
>>返回值地址

### 1.2 方法


| 方法                         |                                                 |
| ---------------------------- | ----------------------------------------------- |
| getPriority();setPriority(); | MAX_PRIORITY: 10MIN_PRIORITY: 1NORM_PRIORITY: 5 |
|                              |                                                 |
|                              |                                                 |

# NOTE

1. windows下CPU时间片约为 15 ms.
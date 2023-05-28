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

## 2. 创建和运行

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

## 3. 查看进程与线程

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

每个线程只能有一个活动栈帧，对应着当前正在执行的那个方法。

每个栈由多个栈帧(Frame)组成，对应着每次方法调用时所占用的内存。

栈：

>程序计数器(Program Counter Register)：作用是记住下一条jvm指令的执行地址，是线程私有的。
>
>栈帧：
>
>>局部变量表
>>
>>返回值地址

<font color=blue>**== 线程上下文切换(Thread Context Switch) ==**</font>

CPU不再执行当前的线程，转而执行另一个线程的代码。原因:

1. 线程的CPU时间片用完
2. 垃圾回收
3. 有更高优先级的线程需要运行
4. 线程自己调用了 sleep、yield、wait、join、park、synchronized、lock 等方法

当Context Switch 发生时，需要由操作系统保存当前线程的状态，并恢复另一个线程的状态。

* 状态包括程序计数器、虚拟机栈中每个栈顿的信息，如局部变量、操作数栈、返回地址等
* Context Switch 频繁发生会影响性能

## 5. 常见方法

```java
/**
 * 1. 启动一个新线程，在新的线程运行run方法中的代码。
 * 2. start 方法只是让线程进入就绪，里面代码不一定立刻运行(CPU的时间片还没分给它)。
 * 3. 每个线程对象的start方法只 能调用一次，如果调用了多次会出现IllegalThreadStateException.
 */
start();

/**
 * 新线程启动后会调用的方法。
 * 如果在构造Thread 对象时传递了 Runnable 参数，则线程启动后会调用Runnable中的run方法。
 */
run();

/**
 * 1. 让当前线程从Running 进入Timed_Waiting状态。
 * 2. 其它线程可以使用 interrupt 方法打断正在睡眠的线程，这时sleep 方法会抛出InterruptedException.
 * 3. 睡眠结束后的线程未必会立刻得到执行。
 * 4. 建议用TimeUnit的sleep 代替Thread的sleep 来获得更好的可读性。
 */
Thread.sleep(ms); // while 循环中必须sleep防止cpu占用100%。只需要1ms.

/**
 * 1. 调用yield会让当前线程从Running进入Runnable 就绪状态，然后调度执行其它线程
 * 2. 具体的实现依赖于操作系统的任务调度器 (可能没让出去)。
 */
yield();

join(); 			// 等待join进来的线程运行结束。
join(long n); 		// 等待join进来的线程运行结束，最多等待n毫秒
getId();			// 获取线程长整型的id
getName(); 			// 获取线程名
setName(String);
getPriority();
setPriority(int); 	// 优先级是1~10的整数，较大的优先级能提高该线程被CPU调度的机率。
getState(); 		// 获取线程状态. NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING

/**
 * 1. 如果线程处于被阻塞状态，线程将立即退出并抛出一个InterruptedException。
 * 2. 如果线程处于正常活动状态，那么会将该线程的中断标志设置为true，但线程仍将继续正常运行。
 */
interrupt();
boolean isInterrupted();   // 打断阻塞线程为false，否则为true。不会清除打断标记
static boolean interrupted(); // 会清除打断标记
```

## 6. 终止线程

在一个线程 t1 中如何“优雅”终止线程 t2 ？

>错误思路
>
>1. 使用线程对象的 stop()方法停止线程
>
>   stop 方法会真正杀死线程，如果这时线程锁住了共享资源，那么当它被杀死后就再也没有机会释放锁，其它线程将永远无法获取锁
>
>2. 使用System.exit(int)方法停止线程
>
>   目的仅是停止一个线程，但这种做法会让整个程序都停止

**两阶段终止模式 Two Phase Termination**

```java
class TwoPhaseTermination{
    private Thread monitor;
	//启动监控线程
	public void start() {
        monitor = new Thread(() -> {
			while(true) {
				Thread current = Thread.currentThread();
                if(current.isInterrupted()) {
                    log.debug("料理后事");
					break;
                }
				try {
					Thread.sleep(1000); // 情况1
                    log.debug(”执行监控记录”); // 情况2
                } catch (InterruptedException e) {
					e.printStackTrace();
                    // 重新设置打断标记
                    current.interrupt();
                }
            }
        });
        monitor.start();
    }
	// 停止监控线程
	public void stop() {monitor.interrupt();}
}
```

`LockSupport.park();` 可以用interrupt()打断，打断标记, 然后线程继续执行。再次`LockSupport.park();`无效, 需要使用 `interrupted()` 重置打断标记才能再次打断。

不推荐使用的过时方法：stop(), suspend(), resume()

**守护线程：** 默认情况下，Java 进程需要等待所有线程都运行结束，才会结束。有一种特殊的线程叫做守护线程，只要其它非守护线程运行结束了，即使守护线程的代码没有执行完，也会强制结束。`t1.setDaemon(true);` 设置t1线程为当前线程守护线程。

## 7. 线程状态

从 **操作系统** 层面：**五种** 状态

> [初始状态] 仅是在语言层面创建了线程对象，还未与操作系统线程关联
>
> [可运行状态] (就绪状指该线程已经被创建 (与操作系统线程关联)，可以由CPU 调度执行
>
> [运行状态] 指获取了 CPU 时间片运行中的状态
>
> >  当CPU 时间片用完，会从[运行状态] 转换至[可运行状态]，会导致线程的上下文切换
>
> [阻塞状态]
>
> > 如果调用了阻塞API，如 BIO 读写文件，这时该线程实际不会用到 CPU，会导致线程上下文切换，进入[阻塞状态]
> >
> > 等 BIO 操作完毕，会由操作系统唤醒阻塞的线程，转换至[可运行状态)
> >
> > 与[可运行状态]的区别是，对[阻塞状态]的线程来说只要它们一直不唤醒，调度器就一直不会考
> > 虑调度它们
>
> [终止状态] 表示线程已经执行完毕，生命周期已经结束，不会再转换为其它状态

从 **Java API** 层面：根据 `Thread.State` 枚举，分为 **六种** 状态

1. **NEW** : 线程刚被创建，但是还没有调用 `start()` 方法
2. **RUNNABLE** : 当调用了 start()方法之后，Java API层面的 **RUNNABLE** 状态涵盖了操作系统层面的 [可运行状态]、[运行状态] 和 [阻塞状态] (由于 BIO 导致的线程阻塞，在Java 里无法区分，仍然认为是可运行)
3. **TERMINATED** : 当线程代码运行结束
4. **BLOCKED**，**WAITING**，**TIMED_WAITING** 都是Java API层面对 [阻塞状态] 的细分

## 8. 多线程

Critical Section: 一段代码块内如果存在对共享资源的多线程读写操作，称这段代码块为临界区。

**synchronized**

```java
synchronized(对象) // 线程1， 线程2(blocked)
{
	临界区
}

synchronized 在方法上 锁对象是 this (同一对象不同方法互斥)
synchronized 在静态方法上 锁对象是 Test.class
```



| 方法                         |                                                 |
| ---------------------------- | ----------------------------------------------- |
| getPriority();setPriority(); | MAX_PRIORITY: 10MIN_PRIORITY: 1NORM_PRIORITY: 5 |
|                              |                                                 |
|                              |                                                 |

# NOTE

1. windows下CPU时间片约为 15 ms.
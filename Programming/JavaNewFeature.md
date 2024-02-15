# Java Versions

## 名词解释

* JEP(JDK Enhancement Proposals): jdk 改进提案，每当需要有新的设想时候，JEP 可以在JCP(java community Process)之前或者同时提出非正式的规范(specification)，被正式认可的 JEP 正式写进 JDK 的发展路线图并分配版本号。

* JSR(Java Specification Requests): java 规范提案，新特性的规范出现在这一阶段，是指向JCP(Java Community Process)提出新增一个标准化技术规范的正式请求。请求可以来自于小组/项目、JEP、JCP成员或者 java 社区(community)成员的提案，每个 java 版本都由相应的JSR支持。

* Java11开始小步快跑，快速迭代。

  * 孵化器模块(Incubator/孵化版/实验版)

    尚未定稿的API/工具，主要用于从Java社区收集使用反馈，稳定性无保障，后期有较大可能性移除

    使用预览 *-Xlint:preview 重新编译。*

  * 预览特性(Preview/预览版)

    规格已成型，实现已确定，但还未最终定稿。这些特性还是存在被移除的可能性，但一般来说最后都会被固定下来

## Java 8

2014年3月18日。<font color=red>**LTS (Long-Term-Support)**</font> 50+ JEP

### 1. Lambda

函数式接口：只有一个方法的接口。可以使用注解`@FunctionalInterface`标识.

本质：作为函数式接口的实例。

```java
Runnable runnable = new Runnable() {
	@Override
	public void run() {
		System.out.println();				
	}
};
// lambda1： 无参数无返回值
Runnable runnable = () -> System.out.println();
// lambda2： 有参数无返回值
Consumer<String> c = (String s) -> System.out.println(s);
// lambda3： 类型推断
Consumer<String> c = (s) -> System.out.println(s);
// lambda4： 只有一个入参省略括号
Consumer<String> c = s -> System.out.println(s);
// lambda5： 多个参数
Comparator<Integer> c = (o1, o2) -> {
    return o1.compareTo(o2)
};
// lambda6： 只有一条语句，return 和 {}都可以省略
Comparator<Integer> c = (o1,o2) -> o1.compareTo(o2);
```

| 内置函数式接口                                | 参数类型和返回类型                                           |
| --------------------------------------------- | ------------------------------------------------------------ |
| Consumer\<T\>                                 | **void** accept(T t);                                        |
| Supplier\<T\>                                 | T get();                                                     |
| Function<T, R>                                | R apply(T t);                                                |
| Predicate\<T\>                                | **boolean** test(T t);                                       |
| BiFunction<T, U, R>                           | R apply(T t, U u);                                           |
| UnaryOperator\<T\> **extends** Function<T, T> | 对类型为T的对象进行一元运算，并返回T类型的结果。包含方法为:T apply(T t); |
| BiFunction<T, U, R>                           | R apply(T t, U u);                                           |

### 2. 方法引用

当要传递给Lambda体的操作，已经有实现的方法了，可以使用方法引用！

方法引用使用的要求: 

> 要求接口中的抽象方法的形参列表和返回值类型与方法引用的方法的<font color=black>**形参列表**</font>和返回值类型相同!
>
> 要求接口中的抽象方法的形参列表和返回值类型与方法引用的方法的<font color=black>**变量顺序**</font>和返回值类型相同!

```java
// 对象 :: 非静态方法
Consumer<String> c = s -> System.out::println;
Employee emp = newEmployee("Tom");
Supplier<String> sup1 = emp::getName;
// 类 :: 静态方法
Comparator<Integer> com1 = Integer::compare;
// 类 :: 非静态方法
Comparator<String> com2 = String::compareTo;
// 构造方法引用
E::new;
// 数组引用
String[]::new;
```

### 3. Stream API

Stream API(java.util.stream) 把真正的函数式编程风格引入到Java中！

Stream是数据渠道，用于操作数据源(集合、数组等)所生成的元素序列。

>1. Stream 自己不会存储元素
>2. Stream 不会改变源对象。相反，他们会返回一个持有结果的新Stream.
>3. Stream 操作是延迟执行的。这意味着他们会等到需要结果的时候才执行.

Stream 和 Collection 集合的区别: Collection 是一种静态的内存数据结构，而 Stream 是有关计算的。前者是主要面向内存，存储在内存中，后者主要是面向 CPU，通过 CPU 实现计算。“集合讲的是数据，Stream讲的是计算!”

<font color=blue>**1. 创建 Stream**</font>

```java
// 通过集合
List<Employee> employees = EmployeeData.getEmployees();
Stream<Employee> stream = employees.stream(); // 返回一个顺序流
Stream<Employee> parallelStream = employees.parallelStream();// 返回一个井行流
// 通过数组
Arrays.stream(arr);
// Stream.of()
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6);
//创建 stream方式四: 创建无限流
// public static<T> Stream<T> iterate(final T seed, final UnaryOperator<T> f)
//遍历前5个偶数
Stream.iterate(0, t -> t + 2).limit(5).forEach(System.out::println);//0 2 4 6 8
// 指定类型 IntStream.iterate(...)
```

<font color=blue>**2. Stream 中间操作**</font>

**筛选与切片**

```java
// filter(Predicate p)一接收 Lambda ， 从流中排除某些元素
List<Employee> list = EmployeeData.getEmployees();
Stream<Employee> stream = list.stream();
stream.filter(e -> e.getSalary() > 7000).forEach(System.out::println);
// 截断流，取前三个
stream.limit(3).forEach(System.out::println);
// 跳过前三个元素
stream.skip(3).forEach(System.out::println);
// 去除重复
stream.distinct().forEach(System.out::println);
```

**映射**

```java
// map(Function f)一接收一个函数作为参数，将元素转换成其他形式或提取信息，该函数会被应用到每个元素上，并将其映射成一个新的元素
List<String> list = Arrays.asList("aa", "bb", "dd");
list.stream().map(str -> str.toupperCase()).forEach(System.out::printIn);
// fLatMap(Function f)一接收一个函载作为参，流中的每个值都换成另一个流，然后把所有流连接成一个流。

// NOTE:
// mapToDouble(ToDoubleFunction f)
// mapTolnt(TolntFunction f)
// mapToLong(ToLongFunction f)
// 接收一个函数作为参数，该函数会被应用到每个元素上，产生一个新的 DoubleStream。
// 接收一个函数作为参数，该函数会被应用到每个元素上，产生一个新的 IntStream。
// 接收一个函数作为参数，该函数会被应用到每个元素上，产生一个新的 LongStream。
```

**排序**

```java
// sorted()一自然排序
List<Integer> list = Arrays.asList(12, 43, 65, 34, 87, 0,-98, 7);
list.stream().sorted().forEach(System.out::println);
// sorted(Comparator com)一-定制排序
```

<font color=blue>**3. Stream 终止操作**</font>

匹配与查找

```java
// alLMatch(Predicate p)一检查是否匹配所有元素。
// noneMatch(Predicate p)一检查是否没有匹配的元素。
// findFirst()一返回第一个元素
// findAny()一返回当前流中的任意元素
// count()一返回流中元素的总个数
// max(Comparator c)一返回流中最大值
// min(Comparator c)一返回流中最小值
```

归约

```java
// reduce(T identity, BinaryOperator b) 可以将流中元素反复结合起来，得到一个值。返回T
List<Integer> list = Arrays.asList(1,2,3,4,5,6,7,8,9,10);
list.stream().reduce(0, Integer::sum); // 初始值0
// reduce(BinaryOperator) -可以将流中元素反复结合起来，得到一个值。返回 Optional<T>
List<Employee> employees = EmployeeData.getEmployees();
Stream<Double> salaryStream = employees.stream().map(Employee::getSalary);
Optional<Double> sumMoney = salaryStream.reduce(Double::sum);
```

收集

```java
// collect(collector c)一将流转换为其他形式。接收一个 Collector接口的实现，用于给Stream中元素做汇总的方法
List<Employee> employees = EmployeeData.getEmployees();
employees.stream().filter(e -> e.getsalary() > 6000).collect(Collectors.toList()):

// javagosql
Stream.of("java", "go", "sql").collect(Collectors.joining());
// java, go, sql
Stream.of("java", "go", "sql").collect(Collectors.joining(", "));
// 【java, go, sql】 prefix and suffix
Stream.of("java", "go", "sql").collect(Collectors.joining(", ", "【", "】"));
```

| 方法           | 返回类型             | 作用                                   |
| -------------- | -------------------- | -------------------------------------- |
| toList         | List\<T\>            | 把流中元素收集到List                   |
| toSet          | Set\<T>              | 把流中元素收集到Set                    |
| toCollection   | Collection\<T>       | 把流中元素收集到创建的集合             |
| counting       | Long                 | 计算流中元素的个数                     |
| summingint     | Integer              | 对流中元素的整数属性求和               |
| averagingInt   | Double               | 计算流中元素Integer属性的平均值        |
| summarizinglnt | IntSummaryStatistics | 收集流中Integer属性的统计值。如:平均值 |

### 4. Optional

| method                                             |                     |
| -------------------------------------------------- | ------------------- |
| of(T t)                                            | t必须是非null       |
| empty()                                            | 生成空的optional    |
| ofNullable(T t)                                    |                     |
| orElse(T t)                                        | 原封装值为空则返回t |
| **boolean** isPresent()                            |                     |
| ifPresent(Consumer<? **super** T> action)          | 执行action          |
| ifPresentOrElse(Consumer<? **super** T>, Runnable) |                     |

### 5. 接口方法

JDK 7: 只能

> 全局常量：public static final 的
>
> 抽象方法：public abstract 的

JDK 8: 可以

> 静态方法 (只能通过接口调用)：public static + 方法体。
>
> 默认方法：public default.
>
> > 如果父类和接口方法相同，默认优先调用父类。
>
> > 实现了相同方法的多个接口，必须要显示重写。
>
> > 接口方法调用，接口名.super.方法名。

### 6. try

```java
// jdk 7
InputStreamReader reader = null;
try {
    reader = new InputStreamReader(System.in);
    reader.read();
} catch (I0Exception e) {
    e.printstackTrace();
} finally {
    //资源的关闭操作
    if(reader != null){
        try {
            reader.close();
        } catch (I0Exception e) {
            e.printstackTrace();
        }
    }
}

// 自动关闭流
try(InputStreamReader reader = new InputStreamReader(System.in)){

} catch (IOException e) {
    e.printStackTrace();
}
```

### 7. 其他

支持Javascript运行

## Java 9

2017年9月21日。

java 9 提供了超过 150 项新功能特性，91个JEP。

包括备受期待的模块化系统可交互的 REPL 工具: jshell，JDK 编译工具，Java 公共 API 和私有代码，以及安全增强、扩展提升、性能管理改善等。可以说 Java 9 是一个庞大的系统工程，完全做了个整体改变。

1. 目录改变

   ![](../imgs/JavaNewFeature/jdk8.jpg)

   ![](../imgs/JavaNewFeature/jdk9.jpg)

   > /jre : 被移除
   >
   > /jre/bin 移动到 /bin
   >
   > /src.zip --> /lib/src.zip

2. modularity

   1. Java 运行环境的膨胀和臃肿。每次JVM启动的时候，至少会有30~60MB的内存加载，主要原因是IVM需要加载rt.jar，不管其中的类是否被classloader加载，第一步整个jar都会被JVM加载到内存当中去(而模块化可以根据模块的需要加载程序运行需要的class) --> jlink工具, 订制运行时环境。
   2. 模块(module)的概念，就是在package外再裹一层。也就是说,用模块来管理各个package,通过声明某个package暴露，不声明默认就是隐藏。因此，模块化使得代码组织上更安全，因为它可以指定哪些部分可以暴露，哪些部分隐藏。


```java
// 创建 module-info.java
module name{
    // exports package path
    exports com.bean;
}
module name{
    // requires module name
    requires java9demo;
}
```

​	![](../imgs/JavaNewFeature/java9module.jpg)

3. jShell命令 (REPL工具 Read-Evaluate-Print Loop)

   ![](../imgs/JavaNewFeature/jshell.jpg)

   可以重复定义方法名，会覆盖。

   可以tab补全。

   没有受检异常。

   > /help: 查看可用命令。
   >
   > /edit: 查看已经编辑所有代码并支持修改。
   >
   > /edit 方法名: 修改方法。
   >
   > /imports: 查看已经导入 (默认导入的包)
   >
   > /open 文件名: 类似脚本语言，执行这个文件。
   >
   > /list: 查看历史操作。
   >
   > /vars: 查看定义的变量
   >
   > /method: 查看定义的方法
   >
   > /exit: 退出

4. 接口中可以定义private方法。

   ```java
   interface MyInterface{

       // jdk 7: 只能声明全局常量(public static final)和抽象方法(public abstract)
       void method1();

       // jdk 8: 声明静态方法 和 默认方法
       public static void method2() {
           System.out.println("method2");
       }
       default void method3() {
           System.out.println("method3");
           method4();
       }

       // jdk 9: 声明私有方法
       private void method4() {
           System.out.println("私有方法");
       }
   }
   ```

5. 钻石操作符：匿名内部类可以省略指定泛型。

   ```java
   // jdk 8
   Set<String> set = new HashSet<String>(){};
   // jdk 9
   Set<String> set = new HashSet<>(){};
   ```

6. try 语句自动关闭流

```java
// 可以在try外面实例化, reader此时是final
InputStreamReader reader = new InputStreamReader(System.in);
try(reader){ // 默认成为final变量。多个对象用分号隔开

} catch (IOException e) {
    e.printStackTrace();
}
```

7. String变更。`char[] value --> byte[] value`
8. 只读集合。

```java
// JDK 9之前
List<String> list = new ArrayList<>();
list.add("aaa");
list.add("bbb");
list.add("ccc");
List<String> newList = Collections.unmodifiablelist(list); // contains: 调用入参list的contains方法
// 或者
newList = Collections.unmodifiableList(Arrays.asList(1,2,3)); // contains入参可以为空

// JDK 9
List.of("aaa", "bbb", "ccc") // contains的入参 Objects.requireNonNull(o);
```

9. Input Stream加强。

```java
ClassLoader cl = this.getClass().getClassLoader();
try (InputStream is = cl.getResourceAsStream("hello.txt");
    OutputStream os = new FileOutputStream("src\\hello1.txt")) {
    is.transferTo(os); // 把输入流中的所有数据直接自动地复制到输出流中
} catch (IOException e) { 
    e.printStackTrace();
}
```

10. 增强Stream API

```java
// takeWhile(Predicate<? super T>) 一旦出现不满足就结束，后面数据丢弃。
List<Integer> list = Arrays.asList(45,43,76,87,42,77,90,73,67,88);
list.stream().takeWhile(x -> x < 50).forEach(System.out::println);// 45,43

// dropWhile(Predicate<? super T>) 一旦出现不满足就结束，后面数据全保留。

// of(T... t), 可以包含null值，可以多个null值，但不能单独null值。
Stream.of(1,2,3,null);// .count()是4
// ofNullable(T t), 可以单个null值。
Stream.ofNullable(null); // .count()是0，打印空“”

// 新的 iterate() 重载
// 以前
Stream.iterate(0, x -> x + 1).limit(5).forEach(System.out::println); // 0 1 2 3 4
// 中间多了一个Predicate<? super T> hasNext参数的重载方法。
Stream.iterate(0, x -> x < 7, x -> x + 2).limit(5).forEach(System.out::println);//0 2 4 6
```

11. Optional类中stream()的使用

```java
List<String> list = new ArrayList<>();
list.add("Tom");
list.add("Jerry");
list.add("Tim");
Optional<List<String>> optional = Optional.ofNullable(list);
Stream<List<String>> stream = optional.stream(); // value非空，返回仅包含此value的Stream;否则，返回一个空的Stream
stream.forEach(System.out::println); // [Tom Jerry Tim]
stream.flatMap(x -> x.stream()).forEach(System.out::printIn); // Tom Jerry Tim

// value非空，执行参数1功能;如果value为空，执行参数2功能
optional.ifPresentOrElse(Consumer<? super T> action, Runnable emptyAction);

// value非空，返回对应的Optional;value为空，返回形参封装的Optional
Optional<T> or(Supplier<? extends Optional<? extends T>>supplier);
```

12. 禁止变量取名直接就是`_`, 编译报错。

13. new Integer(int) 废弃。(Java 16 forRemoval)

    推荐使用`Integer.valueOf(int)`。

14. 多版本jar支持。多版本兼容 JAR 功能能让你创建仅在特定版本的 Java 环境中运行库程序时选择使用的 class 版本。

15. 多分辨率图像 API. Java 程序在高分辨率屏幕上看起来很小。程序只需要提供一组不同分辨率的图像，而API会根据当前设备的分辨率自动选择合适的图像。

15. 全新的 HTTP 客户端 API

    1. HTTP，用于传输网页的协议，早在1997 年就被采用在目前的 1.1版本 (1999年) 中。直到 2015 年，HTTP2 才成为标准。
    2. HttpClient.java

17. 移除

    1. Applet API

17. 其他

    1. 智能编译工具 sjavac
    2. 统一的 JVM 日志系统
    3. javadoc支持 HTML5支持 search
    4. Javascript 引擎升级：Nashorn。JDK 9 包含一个用来解析 Nashorn 的 ECMAScript 语法树的 API。 这个 API 使得IDE 和服务端框架不需要依赖 Nashorn 项目的内部实现类， 就能够分析ECMAScript 代码。
    5. AOT (试验阶段)


## Java 10

2018年3月21日。109个新特性，12个JEP。

> JEP 286: 局部变量的类型推断。该特性在社区讨论了很久并做了调查，可查看 JEP 286 调查结果
>
> JEP 296: 将 JDK 的多个代码仓库合并到一个储存库中
>
> JEP 304: 垃圾收集器接口。通过引入一个干净的垃圾收集器（GC）接口，改善不同垃圾收集器的源码隔离性。
>
> JEP 307: 向 G1 引入并行 Full GC
>
> JEP 310: 应用类数据共享。为改善启动和占用空间，在现有的类数据共享（“CDS”）功能上再次拓展，以允许应用类放置在共享存档中
>
> JEP 312: 线程局部管控。允许停止单个线程，而不是只能启用或停止所有线程
>
> JEP 313: 移除 Native-Header Generation Tool (javah)
>
> JEP 314: 额外的 Unicode 语言标签扩展。包括：cu (货币类型)、fw (每周第一天为星期几)、rg (区域覆盖)、tz (时区) 等
>
> JEP 316: 在备用内存设备上分配堆内存。允许 HotSpot 虚拟机在备用内存设备上分配 Java 对象堆
>
> JEP 317: 基于 Java 的 JIT 编译器 (试验版本) (JIT jdk 1.2)
>
> JEP 319: 根证书。开源 Java SE Root CA 程序中的根证书
>
> JEP 322: 基于时间的版本发布模式。“Feature releases” 版本将包含新特性，“Update releases” 版本仅修复 Bug

1. 局部变量类型推断。var不是一个关键字。

```java
var num = 10;
for(var i : list){
    
}
// 以下写法会编译错误
var num1; // 没有初始化
var num1 = null;
var sup = () -> Math.random();
var con = System.out::println;
var arr = {1,2,3,4}; // 数组正确的静态初始化 int[] arr = {1,2,3,4};
public var method(var num); // 不能是方法返回值类型, 不能是参数类型
var num = 10; // 不能是成员变量，因为成员变量会存在默认值。
try(){
}catch(var e){ // 不能是异常类型
}
```

2. `List.copyOf()` : 创建一个只读集合。

```java
//示例1:
var list1 = List.of("Java", "python","c");
var copy1 = List.copyof(list1);
System.out.println(list1 == copy1); // true
//示例2:
var list2 = new ArrayLis<String>();
var copy2 = List.copyof(Iist2);
System.out.printn(list2 == copy2); // false
// 本身就是只读集合，没有必要再新创建集合。

// 新方法 toUnmodifiableList、toUnmodifiableSet 和 toUnmodifiableMap 已添加到 Stream 包中的 Collectors 类，这些方法适合于将 stream 最终转换成不可变集合
```

3. Optional

```java
// value非空，返回value; 否则抛异常NoSuchElementException
T orElseThrow();
```

## Java 11 (LTS)

2018年9月26日。<font color=red>**LTS (Long-Term-Support)**</font> 更新17个JEP。

> JEP 181: 嵌套类可见性控制
>
> JEP 309: 动态文件常量
>
> JEP 315: 改进 Aarch64 Intrinsics
>
> JEP 318: Epsilon–一个无操作的垃圾收集器
>
> JEP 320: 删除 Java EE 和 CORBA 模块
>
> JEP 321: Http Client (Standard)
>
> JEP 323: 用于 Lambda 参数的局部变量语法
>
> JEP 324: Curve25519 和 Curve448 算法的密钥协议
>
> JEP 327: Unicode 10
>
> JEP 328: Flight Recorder(飞行记录器)
>
> JEP 329: haCha20 和 Poly1305 加密算法支持
>
> JEP 330: Launch Single-File Source-Code Programs（启动单一文件的源代码程序）
>
> JEP 331: 低开销的 Heap Profiling
>
> JEP 332: Transport Layer Security (TLS) 1.3支持
>
> JEP 333: ZGC: A Scalable Low-Latency Garbage Collector（可伸缩低延迟垃圾收集器）
>
> JEP 335: 弃用 Nashorn JavaScript 引擎
>
> JEP 336: 弃用 Pack200 工具和 API

1. String 增强

```java
"   ".isBlank(); // true, \t \n 都是blank
"   ".strip(); // 去除blank, \t \n 都是blank
"".stripTrailing();
"".stripLeading();
"".repeat(n); // 复制次数。
"".lines.count(); // 行数, 根据\n区分

readString();
writeString();
String str = Files.readString(Path.of("123.txt"));
String modified = modify(str);
Files.writeString(Path.of("123-mod.txt"), modified);

Path path = Files.writeString(Files.createTempFile("test", ".txt"), "This was posted on JD");
String s = Files.readString(path);
```

2. Optional增强

```java
isEmpty(); // 判断value是否为空
```

3. lambda参数可以加注解。

4. 全新的http客户端API。再次更新`Java.net.HttpClient.java`

5. 可以直接 `java Hello.java` 执行文件。(只会执行第一个类包含的main方法)

6. 废弃 Nashorn。（只能用GraalVM虚拟机）

7. ZGC，A Scalable Low-Latency Garbage Collector (Experimental)

8. 反射内部类。getNestHost()、getNestMembers() 和 isNestmateOf()。

7. 新的 Collection.toArray(IntFunction<T[]> generator) 方法

```java
// 在 Java 11 之前，Collection 接口提供了两个 toArray() 方法来将集合转换为数组。
// 返回一个 Object 数组
List<String> list = List.of("foo", "bar", "baz");
Object[] strings1 = list.toArray();

//  toArray() 方法需要一个请求类型的数组。如果此数组至少与集合一样大，则元素将存储在此数组中 (strings2a)。否则，将创建所需大小的新数组 (strings2b)。
String[] strings2a = list.toArray(new String[list.size()]);
String[] strings2b = list.toArray(new String[0]);

// Java 11 开始，我们还可以编写以下代码：
String[] strings = list.toArray(String[]::new);
```

10. Path.of()

```java
// Relative path foo/bar/baz
Path tmp = Path.of("foo/bar/baz");
Path.of("foo", "bar/baz");
Path.of("foo", "bar", "baz");

// Absolute path /foo/bar/baz
Path.of("/foo/bar/baz");
Path.of("/foo", "bar", "baz");
Path.of("/", "foo", "bar", "baz");
// 要定义绝对路径，在 Linux 和 macOS 上，第一部分必须以“/”开头，Windows 上以驱动器号开头，例如 “C:”。

Path tmp = Path.of(URI.create("http://codefx.org"));
```

11. lamda 表达式更新

```java
// Predicate.not(Predicate)
Stream.of("a", "b", "", "c").filter(Predicate.not(String::isBlank))
.forEach(System.out::println); // a b c

// "Pattern:asMatchPredicate" 处理正则表达式. JDK 8
Pattern nonWordCharacter = Pattern.compile("\\W");
Stream.of("abc", "def").filter(nonWordCharacter.asPredicate()).forEach(System.out::println);

// "Pattern:asMatchPredicate" JDK 11
// asPredicate 会检查字符串或者其字串是否符合这个正则（他的行为像 s -> this.matcher(s).find() ）
// asMatchPredicate 只会检查整个字符串是否符合这个正则（他的行为像 s -> this.matcher(s).matchs()）
```

## Java 12

2019年3月19日。8个JEP

> JEP 189: Shenandoah: A Low-Pause-Time Garbage Collector (Experimental) ：新增一个名为 Shenandoah 的垃圾回收器，它通过在 Java 线程运行的同时进行疏散 (evacuation) 工作来减少停顿时间。
>
> JEP 230: Microbenchmark Suite：新增一套微基准测试，使开发者能够基于现有的 Java Microbenchmark Harness（JMH）轻松测试 JDK 的性能，并创建新的基准测试。
>
> JEP 325: Switch Expressions (Preview) ：对 switch 语句进行扩展，使其可以用作语句或表达式，简化日常代码。
>
> JEP 334: JVM Constants API ：引入一个 API 来对关键类文件 (key class-file) 和运行时工件的名义描述（nominal descriptions）进行建模，特别是那些可从常量池加载的常量。
>
> JEP 340: One AArch64 Port, Not Two ：删除与 arm64 端口相关的所有源码，保留 32 位 ARM 移植和 64 位 aarch64 移植。
>
> JEP 341: Default CDS Archives ：默认生成类数据共享（CDS）存档。
>
> JEP 344: Abortable Mixed Collections for G1 ：当 G1 垃圾回收器的回收超过暂停目标，则能中止垃圾回收过程。
>
> JEP 346: Promptly Return Unused Committed Memory from G1 ：改进 G1 垃圾回收器，以便在空闲时自动将 Java 堆内存返回给操作系统。

预览：预览语言功能的想法是在 2018年初被引入Java 中的，本质上讲，这是一种引入新特性的测试版的方法。通过这种方式，能够根据用户反馈进行升级、更改。在极端情况下，如果没有被很好的接纳，则可以完全删除该功能。预览功能的关键在于它们没有被包含在Java SE 规范中。

1. switch改动.（预览）（正式版：Java 14）

```java
switch(fruit){
    case PEAR -> System.out.println("4");
    case APPLE,GRAPE,MANGO -> System.out.println("5");
    case ORANGE,PAPAYA -> System.out.println("6");
    default ->new IllegalStateException("No Such Fruit:" + fruit);
}

int dayNumber = switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> 6;
    case TUESDAY                -> 7;
    case THURSDAY, SATURDAY     -> 8;
    case WEDNESDAY              -> 9;
    default                     -> throw new IllegalStateException("Huh? " + day);
}
```
2. String

```java
// indent 方法给每一行前面都加空格
String result = "foo".indent(4);
String result = "foo\nbar\nbar2".indent(4);

public <R> R transform(Function<? super String, ? extends R> f);
String info1 = "hello".transform(info -> info + "world"); // hello world
String.transform(StringUtils::toCamelCase)；
```
3. Files

```java
Files.mismatch(Path, Path);
// 返回一个 long 值，这个值表示第一处不匹配的字节位置。如果返回-1，说明两个文件相等
```
4. NumberFormat

```java
// 例子：3.6M比3,600,000容易读得多
// Java 12 引入了一个叫做 NumberFormat.getCompactNumberInstance(Locale, NumberFormat.Style)的静态方法。用于创建紧凑数字表示形式，
NumberFormat fmt = NumberFormat.getCompactNumberInstance(Locale.US, NumberFormat.Style.SHORT);
String result = fmt.format(1000); // 1k or 1千
```

5. Shenandoah GC: 低停顿时间的GC (预览)（正式版：Java 15）

   主要目标是 99.9% 的暂停小于 10ms,暂停与堆大小无关等。

   Shenandoah和ZGC的关系呢:

   * 相同点: 性能几乎可认为是相同的
   * 不同点: ZGC是Oracle JDK的，根正苗红。而shenandoah只存在于Open JDK中，因此使用时需注意你的JDK版本

6. JVM 常量 API `java.lang.constant`.实现包中借口，加载从常量池，速度更快。

## Java 13

2019年9月17日。5个JEP

> JEP 350：动态CDS档案 (类数据共享机制Class Data Sharing, 多个JVM之间共享)
>
> JEP-351：ZGC：Uncommit Unused Memory 未使用的堆内存归还操作系统
>
> JEP-353：重新实现旧版套接字API `java.net.Socket`
>
> JEP-354：switch表达式（预览）
>
> JEP-355：文本块（预览）

1. switch新的关键字yield（预览）（正式版：Java 14）

```java
// yield与return的区别在于，yield只会跳出switch块，return是跳出当前方法或循环。
final DayOfWeek day = DayOfWeek.SATURDAY;
final String typeOfDay = switch (day) {
    case MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY -> {
        System.out.println("Working Day: " + day);
        yield "Working Day";
    }
    case SATURDAY, SUNDAY -> {
        System.out.println("Day Off: " + day);
        yield "Day Off";
    }
};
// "Day Off"
```
2. 文本块（预览）（正式版：Java 15）

```java
// Text Block
// 不需要再通过 \n 逐行拼接 (依旧支持额外的 \n \t 等转义字符)
// 文本块中的双引号不再需要转义， 如果需要显示三引号：\""" 表示三个引号
// 文本块可以跟字符串拼接
String json2 = """
        {
          "wechat": "hellokanshan",
          "wechatName": "看山",
          "mp": "kanshanshuo",
          "mpName": "看山的小屋"
        }
        """;

String text1 = """
abc"""; // length: 3
String text2 = """
abc
"""; // lenght: 4 (最后多一个\n)
String text3 = "abc"; // text1 == text3 != text2);

String text4 = """
"""; // 表示空字符串

// 根据行结束符的位置自动删除多余空格
String text5 = """
  abc
   def
  """; // abc前面两个空格去除，def前面保留一个空格。每行结尾空格删除

// 占位替换 $
String type = "abc";
String code1 ="""
public void print($type o) {
    System.out.println(objects.tostring(o));
}
""".replace("$type", type);

String code2 =String.format("""
public void print(%s o) {
    System.out.println(objects.tostring(o));
}
""", type);
```

3. 新增 FileSystems.newFileSystem

java.nio.file.FileSystems 添加了三个新方法，使可以更方便的使用 FileSystem.

- newFileSystem(Path)
- newFileSystem(Path, Map<String, ?>)
- newFileSystem(Path, Map<String, ?>, ClassLoader)

## Java 14

2020年3月17日。16个JEP

> JEP 305: instanceof的模式匹配 (预览)
>
> JEP 343: 打包工具 (Incubator)
>
> JEP 345: G1的NUMA内存分配优化
>
> JEP 349: JFR (JDK Flight Recorder) 事件流
>
> JEP 352: 非原子性的字节缓冲区映射
>
> JEP 358: 友好的空指针异常
>
> JEP 359: Records (预览)
>
> JEP 361: Switch 表达式 (标准)
>
> JEP 362: 弃用Solaris和SPARC端口
>
> JEP 363: 移除 CMS （Concurrent Mark Sweep）垃圾收集器
>
> JEP 364: macOS 系统上的ZGC
>
> JEP 365: Windows系统上的ZGC
>
> JEP 366: 弃用ParallelScavenge + SerialOld GC组合
>
> JEP 367: 移除Pack200 Tools和API
>
> JEP 368: 文本块 (第二个预览版)
>
> JEP 370: 外部存储器API (Incubator)

1. instanceof (预览)（正式版：Java 16）

```java
if (!(obj instanceof String str)) {
    .. str.contains(..)..// 不必再声明str对象进行强制类型转换
} else {
    .. str....
}		
		
if (obj instanceof String str && str.length() > 5) {.. str.contains(..)..}
if (obj instanceof String str || str.length() > 5) {.. str.contains(..)..}
```
2. record (预览)（正式版：Java 16）

```java
// record 是一种全新的类型，它本质上是一个 final 类，(默认且只能继承Record类)
// 所有属性都是private final 修饰，它会自动编译出 public get、hashcode、equals、toString 等方法，减少了代码编写量。
// 还可以声明静态的属性、静态的方法、构造器、实例方法
// 不可以非静态属性，abstract，不能继承其他类
public record Cat(String name, Integer age) {
}

public class Test {
    public static void main(String[] args) {
        test();
    }
    private static void test() {
        Cat c1 = new Cat("tomcat", 1);
        Cat c2 = new Cat("tomcat", 1);
        Cat c3 = new Cat("jerry", 2);
        System.out.println(c1 == c2); // true
        System.out.println(c1.name()); // 类似于原有的针对于实例变量的get()
    }
}

// 在 java.lang.Class 中引入了下面两个新方法：
RecordComponent[] getRecordComponents()
boolean isRecord()   
```
3. Text block (预览)（正式版：Java 15）

```java
// 不使用文本块
String literal = "two escape sequences first is for newlines " +
"and, second is to signify white space " +
"or single space.";
 
// 其一，用\换行书写，实际同一行。
// 其二，用\s表示一个空格
// 使用 \ 看起来像这样：实际内容是在同一行 (取消换行操作)
String text = """
                two escape sequences first is for newlines \
                and, second is to signify white space \
                or single space.\
                """;
```

4. JEP 358: Helpful NullPointerExceptions

`-XX:+ShowCodeDetailsInExceptionMessages` VM options中开启，可以显示具体行的具体位置空指针

5. 货币

```Java
final NumberFormat format = NumberFormat.getCurrencyInstance(Locale.CHINA);
System.out.println(format.format(0.5)); // ¥0.50
```

## Java 15

2020年9月15日。14个JEP.

> 339    Edwards-Curve Digital Signature Algorithm (EdDSA)    爱德华兹曲线数字签名算法
>
> 360    Sealed Classes (Preview)    密封类(预览)
>
> 371    Hidden Classes    隐藏类
>
> 372    Remove the Nashorn JavaScript Engine    移除nasorn JavaScript引擎
>
> 373    Reimplement the Legacy DatagramSocket API    重新实现旧的DatagramSocket API
>
> 374    Disable and Deprecate Biased Locking    禁用和弃用偏置锁
>
> 375    Pattern Matching for instanceof (Second Preview)    模式匹配的instanceof(第二次预览)(并没有任何修改)
>
> 377    ZGC: A Scalable Low-Latency Garbage Collector    ZGC:一个可扩展的低延迟垃圾收集器
>
> 378    Text Blocks    文本块
>
> 379    Shenandoah: A Low-Pause-Time Garbage Collector    Shenandoah:低暂停时间垃圾收集器
>
> 381    Remove the Solaris and SPARC Ports    移除Solaris和SPARC端口
>
> 383    Foreign-Memory Access API (Second Incubator)    外部内存访问API(第二个孵化器)
>
> 384    Records (Second Preview)    记录(第二次预览)(并没有任何修改)
>
> 385    Deprecate RMI Activation for Removal    建议移除RMI激活

1. Sealed Classes (Preview)（正式版：Java 17）

```java
// sealed 密封的类，permits指定继承的类
public abstract sealed class Person permits Employee, Manager {
    //...
}

// 任何继承密封类的类本身必须被声明为final、non-sealed的或sealed的。
final class Employee extends Person {
}

// non-sealed 类，与一般的类没有区别
non-sealed class Manager extends Person {
}

// 如果没有一个密封的类，编译器就不能合理地确定所有可能的子类都被我们的 if-else 语句所覆盖。如果末尾没有 else 子句，编译器可能会发出警告，表明我们的逻辑没有涵盖所有的情况。
if (person instanceof Employee) {
    return ((Employee) person).getEmployeeId();
} else if (person instanceof Manager) {
    return ((Manager) person).getSupervisorId();
}
```

2. Hidden Classes(隐藏类)

   该提案通过启用标准 API 来定义无法发现且具有有限生命周期的隐藏类，从而提高 JVM 上所有语言的效率。JDK内部和外部的框架将能够动态生成类，而这些类可以定义隐藏类。通常来说基于JVM的很多语言都有动态生成类的机制，这样可以提高语言的灵活性和效率。

   * 隐藏类天生为框架设计的，在运行时生成内部的class。

   * 隐藏映只能通过反射访问，不能直接被其他类的字节码访问。

   * 隐藏类可以独立于其他类加载、卸载，这可以减少框架的内存占用。

   Hidden classes就是不能直接被其他class的二进制代码使用的class。Hidden classes主要被一些框架用来生成运行时类，但是这些类不是被用来直接使用的，而是通过反射机制来调用。比如

   * 不会将lambda表达式转换成为专门的类，而是在运行时将相应的字节码动态生成相应的类对象。
   * 另外使用动态代理也可以为某些类生成新的动态类。

3. `TreeMap` 新引入了下面这些方法：

   - `putIfAbsent()`
   - `computeIfAbsent()`
   - `computeIfPresent()`
   - `compute()`
   - `merge()`

## Java 16

2021年3月16日。17个JEP.

> 338    Vector API(孵化器)
>
> 347    启用 C++14 语言功能 (在 JDK 源代码中)
>
> 357    从 Mercurial 迁移到 Git
>
> 369    迁移到 GitHub
>
> 376    ZGC:并发线程堆栈处理
>
> 380    Unix 域套接字通道
>
> 386    Alpine Linux 端囗
>
> 387    弹性元空间
>
> 388    Windows/AArch64
>
> 389    端口外链 API(孵化器)
>
> 390    基于值的类的警告
>
> 392    打包工具
>
> 393    外内存访问API(第三孵化器)
>
> 394    instanceof 的模式匹配
>
> 395    Records
>
> 396    默认情况下强封装JDK内部
>
> 397    密封类(第二次预览)

1. 使用反射执行接口中的默认实现方法
2. DateTimeFormatter 的一个新成员是日周期符号 "B"，它提供了一个上午/下午格式的替代方案。

```java
LocalTime date = LocalTime.now();
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("B h:m");
System.out.println(date.format(formatter)); // 下午 1:01
```

3. Stream.toList()

```java
List<String> lst = Arrays.asList("1", "2", "3");
// before jdk 16
List<Integer> ints = lst.stream().map(Integer::parseInt).collect(Collectors.toList());
// jdk 16+
List<Integer> ints = lst.stream().map(Integer::parseInt).toList();
```

4. new Integer(int) 在这个版本 forRemoval

5. Integer 类增加注解 `@jdk.internal.ValueBased`

   ```java
   // 对`@jdk.internal.ValueBased`注解加入了基于值的类的告警，在 Synchronized 同步块中使用值类型，将会在编译期和运行期产生警告，甚至是异常。
   public void inc(Integer count) {
       for (int i = 0; i < 10; i++) {
           new Thread(() -> {
               synchronized (count) { // 这里会产生编译警告
                   count++;
               }
           }).start();
       }
   }
   ```

## Java 17 (LTS)

2021年9月14日。<font color=red>**LTS (Long-Term-Support)**</font> 14个JEP

> 306：恢复始终严格的浮点语义
>
> 356：增强型伪随机数发生器
>
> 382：新的 macOS 渲染管道
>
> 391：macOS/AArch64 端口
>
> 398：弃用即将删除的 Applet API
>
> 403：强封装JDK的内部API
>
> 406：Switch模式匹配（预览）
>
> 407：删除 RMI 激活
>
> 409：密封类
>
> 410：删除实验性 AOT 和 JIT 编译器
>
> 411：弃用即将删除安全管理器
>
> 412：外部函数和内存 API（孵化器）
>
> 414：Vector API（第二次进行特性孵化）
>
> 415：特定于上下文的反序列化过滤器

1. 增强伪随机数字生成 RandomGenerator
   1. `SplittableRandomGenerator`
   2. `JumpableRandomGenerator`
   3. `LeapableRandomGenerator`
   4. `ArbitrarilyJumpableRandomGenerator`


```java
RandomGenerator randomGenerator = RandomGenerator.of("L32X64MixRandom");
int randomInt = randomGenerator.nextInt();
System.out.println("randomInt = " + randomInt);
```

2. switch （预览）（正式版：Java 21）

```java
// Old code
static String formatter(Object o) {
    String formatted = "unknown";
    if (o instanceof Integer i) {
        formatted = String.format("int %d", i);
    } else if (o instanceof Long l) {
        formatted = String.format("long %d", l);
    } else if (o instanceof Double d) {
        formatted = String.format("double %f", d);
    } else if (o instanceof String s) {
        formatted = String.format("String %s", s);
    }
    return formatted;
}

// New code
static String formatterPatternSwitch(Object o) {
    return switch (o) {
        case Integer i -> String.format("int %d", i);
        case Long l    -> String.format("long %d", l);
        case Double d  -> String.format("double %f", d);
        case String s  -> String.format("String %s", s);
        default        -> o.toString();
    };
}
// 对于 null 值的判断也进行了优化。
// Old code
static void testFooBar(String s) {
    if (s == null) {
        System.out.println("oops!");
        return;
    }
    switch (s) {
        case "Foo", "Bar" -> System.out.println("Great");
        default           -> System.out.println("Ok");
    }
}

// New code
static void testFooBar(String s) {
    switch (s) {
        case null         -> System.out.println("Oops");
        case "Foo", "Bar" -> System.out.println("Great");
        case int[] ia     -> System.out.println("Array of ints of length " + ia.length);
        default           -> System.out.println("Ok");
    }
}
```

3. 引入工具类 java.util.HexFormat 提供了十六进制和格式化和解析。

```java
System.out.println(HexFormat.fromHexDigits("5e"));//94
// 获取字符在十六进制中表示的数据
System.out.println(HexFormat.fromHexDigit('A'));// 10
byte b = 94;
System.out.println(HexFormat.of().toHexDigits(b));// 5e
System.out.println(HexFormat.fromHexDigit('X'));// 异常 ：not a hexadecimal digit
```

4. 添加 java.time.InstantSource

```java
InstantSource system = InstantSource.system();
// 等价于 System.currentTimeMillis()
System.out.println(system.millis());
InstantSource oneDayLater = InstantSource.offset(system, Duration.ofDays(1L));
System.out.println(oneDayLater.millis());
```

5. 获取字符集

```java
// 获取系统的原生字符集名称。windows 系统默认设置会输出 GBK
System.out.println(System.getProperty("native.encoding"));

// 检查Java应用程序是否与一个控制台环境关联，并打印该环境的字符集名称。
Console console = System.console();
if(console!=null){
    System.out.println(console.charset());
}
// 虚拟机是否具有控制台取决于底层平台，还取决于调用虚拟机的方式。如果虚拟机从一个交互式命令行开始启动，且没有重定向标准输入和输出流，那么其控制台将存在，并且通常连接到键盘并从虚拟机启动的地方显示。如果虚拟机是自动启动的（例如，由后台作业调度程序启动），那么它通常没有控制台。
```
## Java 18

2022年3月22日。 9个JEP

> 400：默认 UTF-8 字符编码
>
> 408：简单的 Web 服务器
>
> 413：Javadoc 中支持代码片段
>
> 416：使用方法句柄重新实现反射核心功能
>
> 417：Vector API（三次孵化）
>
> 418：互联网地址解析 SPI
>
> 419：Foreign Function & Memory API (第二次孵化）
>
> 420：switch 表达式（二次预览）
>
> 421：Deprecate Finalization for Removal

1. 废弃Object中的finalize方法，Thread中的stop方法将在未来被移除,
2. `@snippet` , 简化包含示例代码的 api 文档

```java
// 在之前, 可能要使用 html 的 pre 标签加 @code 标签,像这样:
/**
<pre>{@code
    lines of source code
}</pre>
*/

// 现在
/**
 * The following code shows how to use {@code Optional.isPresent}:
 * {@snippet :
 * if (v.isPresent()) {
 *     System.out.println("v: " + v.get());
 * }
 * }
 */
```

3. 其他

```java
// 当给定的字符名称不被支持时,回退到默认值
Charset charset = Charset.forName("utf-9", StandardCharsets.UTF_8);
System.out.println("charset = " + charset);// charset = UTF-8

// 引入新的系统属性 java.properties.date ,支持程序控制调用 java.util.Properties::store 时使用的默认日期注释.
Properties properties = new Properties();
properties.setProperty("host", "java.com");
StringWriter writer = new StringWriter();
properties.store(writer, "test configuration");
System.out.println(writer);
// 默认输出会带上当前时间的日期注释(第二行):
#test configuration
#Mon Nov 28 19:20:58 CST 2022
host=java.com
```
# END
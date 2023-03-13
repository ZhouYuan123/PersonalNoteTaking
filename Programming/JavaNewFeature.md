## Java 8

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
//遍历前10个偶数
Stream.iterate( seed:0, t -> t + 2).limit(10).forEach(System.out::println);
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
stream.distinct.forEach(System.out::println);
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
List<Integer> list = Arrays.asList(12, 43, 65，34, 87, 0,-98, 7);
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
employees.stream().filter(e -> e.getsalary() > 6000).collect(Collectors.tolist()):
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

## Java 9



# END
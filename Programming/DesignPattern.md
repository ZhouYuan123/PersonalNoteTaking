# 设计模式

## 1. 概述

1990年软件工程界开始研讨设计模式的话题，后来召开了多次关于设计模式的研讨会。直到1995 年，艾瑞克·伽马(Erich Gamma)理查德海尔姆(Richard Helm)、拉尔夫约翰森(Ralph Johnson)、约威利斯迪斯(John Vlissides)等 4 位作者合出版了《设计模式:可复用面向对象软件的基础》一书，在此书中吸录了 23 个设计模式，这是设计模式领域里程碑的事件，导致了软件设计模式的突破。这 4 位作者在软件开发领域里也以他们的“四人组”(Gang of Four，GoF)著称。

### 1.1 UML

统一建模语言 (Unified Modeling Language), UML 从目标系统的不同角度出发，定义了用例图、类图、对象图、状态图、活动图、时序图、协作图、构件图、部署图等 9 种图。

<font color=blue>**== 类图 ==**</font>

* `+` : 表示public
* `-` : 表示private
* `#` : 表示protected

属性的完整表示方式是:  可见性  名称 : 类型\[ = 缺省值]

方法的完整表示方式是:  可见性  名称(参数列表)[ : 返回类型]

```mermaid
classDiagram
class Example {
	- name : String
	+ work() : void
	# method2(int par1, String par2):int
}
```
### 1.2 类之间关系

<font color=blue>**== 关联关系(Association) ==**</font>

表示类之间的引用关系

箭头指向：

* 单向关联用一个带箭头的实线表示，箭头从使用类指向被关联的类；
* 双向关联用没有箭头的实线来表示;
* 自关联

```mermaid
classDiagram
Student --> Course
Customer -- Product
Node --> Node
class Customer{
	- products : List<Product>
}
class Product{
- customer : Customer
}
class Node{
- subNode : Node
}
```

上图中在Customer类中维护一个List\<Product>，表示一个顾客可以购买多个商品;在Product类中维护一个Customer类型的成员变量表示这个产品被哪个顾客所购买。

<font color=blue>**== 聚合关系(Aggregation) ==**</font>

聚合关系是关联关系的一种，是强关联关系，是整体和部分之间的关系。

```mermaid
classDiagram
class University{
-teas : List<Teacher>
}
class Teacher{
- name : String
+ teach() : void
}
University o-- Teacher

```

<font color=blue>**== 组合关系(Composition) ==**</font>

组合表示类之间的整体与部分的关系，但它是一种更强烈的聚合关系。

```mermaid
classDiagram
class Head{
- mouth : Mouth
}
class Mouth
Head *-- Mouth
```
<font color=blue>**== 依赖关系(Dependency) ==**</font>

依赖关系是一种使用关系，它是对象之间耦合度最弱的一种关联方式，是临时性的关联。

```mermaid
classDiagram
class Driver{
- name : String
+ drrive(Car car) : void
}
class Car
Car <.. Driver
```

<font color=blue>**== 泛化关系(Generalization) ==**</font>

泛化是学术名称，通俗来讲，泛化指的是类与类之间的继承关系和类与接口之间的实现关系。

<font color=blue>**== 继承关系(Inheritance) ==**</font>

继承关系是对象之间耦合度最大的一种关系。

```mermaid
classDiagram
Person <|-- Student
```
<font color=blue>**== 实现关系(Realization) ==**</font>

```mermaid
classDiagram
Vehicle <|.. Car
```

### 1.3 软件设计原则

1. **开闭原则:** 对扩展开放，对修改关闭。
2. **里氏代换原则:** 任何基类可以出现的地方，子类一定可以出现。通俗理解: 子类可以扩展父类的功能，但不能改变父类原有的功能。换句话说，子类继承父类时，除添加新的方法完成新增功能外，尽量不要重写父类的方法。
3. **依赖倒转原则** : 高层模块不应该依赖低层模块，两者都应该依赖其抽象。抽象不应该依赖细节，细节应该依赖抽象。简单的说就是要求对抽象进行编程，不要对实现进行编程，这样就降低了客户与实现模块间的耦合。
4. **接口隔离原则** : 客户端不应该被迫依赖于它不使用的方法，一个类对另一个类的依赖应该建立在最小的接口上。
5. **迪米特法则** : 迪米特法则又叫最少知道原则。只和你的直接朋友交谈，不跟"陌生人"说话 (Talk only to your immediate friends and not to strangers)。其含义是:如果两个软件实体无须直接通信，那么就不应当发生直接的相互调用，可以通过第三方转发该调用。其目的是降低类之间的精合度，提高模块的相对独立性.
   迪米特法则中的“朋友”是指: 当前对象本身、当前对象的成员对象、当前对象所创建的对象、当前对象的方法参数等，这些对象同当前对象存在关联、聚合或组合关系，可以直接访问这些对象的方法。
6. **合成复用原则** : 尽量先使用组合或者聚合等关联关系来实现，其次才考虑使用继承关系来实现。通常类的复用分为继承复用和合成复用两种。
   1. 继承复用虽然有简单和易实现的优点，但它也存在以下缺点
      1. 继承复用破坏了类的封装性，因为继承会将父类的实现细节暴露给子类，父类对子类是透明的，所以这种复用又称为“白箱”复用。
      2. 子类与父类的糟合度高。父类的实现的任何改变都会导致子类的实现发生变化，这不利于类的扩展与维护
      3. 它限制了复用的灵活性。从父类继承而来的实现是静态的，在编译时已经定义，所以在运行时不可能发生变化.
   2. 采用组合或聚合复用时，可以将已有对象纳入新对象中，使之成为新对象的一部分，新对象可以调用已有对象的功能，它有以下优点:
      1. 它维持了类的封装性。因为成分对象的内部细节是新对象看不见的，所以这种复用又称为“黑箱”复用。
      2. 对象间的耦合度低。可以在类的成员位置声明抽象
      3. 复用的灵活性高。这种复用可以在运行时动态进行，新对象可以动态地引用与成分对象类型相同的对象。


## 2. 创建者模式

### 2.1 单例模式

单例设计模式分类两种

饿汉式: 类加载就会导致该单实例对象被创建

懒汉式: 类加载不会导致该单实例对象被创建，而是首次使用该对象时才会创建。

```java
/**
 * 饿汉式-1: 静态成员变量
 */
public class Singleton {
	//1. 私有构造方法
    private singleton() {}
    //2. 在本类中创建本类对象
    private static Singleton instance = new Singleton();
    //3. 提供一个公共的访问方式，让外界获取该对象
    public static Singleton getInstance() {
        return instance;
    }
}

/**
 * 饿汉式-2: 静态代码块
 */
public class Singleton {
	//1. 私有构造方法
    private singleton() {}
    //2. 在本类中创建本类对象
    private static Singleton instance; // null
    static {
		instance = new Singleton();
    }
    //3. 提供一个公共的访问方式，让外界获取该对象
    public static Singleton getInstance() {
        return instance;
    }
}
```



### 2.2 工厂方法模式

### 2.3 抽象工程模式

### 2.4 原型模式

### 2.5 建造者模式

## 3. 结构型模式

## 4. 行为型模式

### 动态代理

1. 静态代理
2. 动态代理 (JDK 代理)
3. Cglib代理

```java
// 被代理类
public class Renter implements Person{
	@Override
	public void rentHouse() {
		System.out.println("租客租房成功！");
	}
}

public class RenterInvocationHandler<T> implements InvocationHandler{
	//被代理类的对象
	private T target;
	public RenterInvocationHandler(T target){
		this.target = target;
	}
	/**
     * proxy: 动态代理对象
     * method：正在执行的方法
     * args：调用目标方法时传入的实参
     */
	@Override
	public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
		//代理过程中插入其他操作
		System.out.println("租客和中介交流");
		Object result = method.invoke(target, args);
		return result;
	}
}

public class ProxyTest {
	public static void main(String[] args) {
		//创建被代理的实例对象
		Person renter = new Renter();
		//创建InvocationHandler对象
		InvocationHandler renterHandler = new RenterInvocationHandler<Person>(renter);
		//创建代理对象,代理对象的每个执行方法都会替换执行Invocation中的invoke方法
		Person renterProxy = (Person) Proxy.newProxyInstance(
            Person.class.getClassLoader(), new Class<?>[]{Person.class}, renterHandler);
		renterProxy.rentHouse();
		
		//也可以使用下面的方式创建代理类对象，Proxy.newProxyInstance其实就是对下面代码的封装
		/*try {
			//使用Proxy类的getProxyClass静态方法生成一个动态代理类renterProxy 
			Class<?> renterProxyClass = Proxy.getProxyClass(Person.class.getClassLoader(), new Class<?>[]{Person.class});
			//获取代理类renterProxy的构造器，参数为InvocationHandler
			Constructor<?> constructor = renterProxyClass.getConstructor(InvocationHandler.class);
			//使用构造器创建一个代理类实例对象
			Person renterProxy = (Person)constructor.newInstance(renterHandler);
			renterProxy.rentHouse();
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}*/
	}

}

```

# Implementing Domain-Specific Languages with Xtext and Xtend

## 1. 缩写

EMF (Eclipse Modeling Framework) : http://www.eclipse.org/modeling/emf

GPL (General Purpose Languages)

ANTLR (ANother Tool for Language Recognition) pronounced Antler

AST (Abstract Syntax Tree)

MWE2 (Modeling Workflow Engine 2)

JDT (Java Development Tools)

## 2. xtext

Xtext is an Eclipse framework for implementing programming languages and  DSLs.

documentation: https://www.eclipse.org/Xtext/documentation/

Git repository: https://github.com/LorenzoBettini/packtpub-xtext-book-2nd-examples

创建一个名为 org.example.entities 的 xtext 项目

```java
grammar org.example.entities.Entities with org.eclipse.xtext.common.Terminals

generate entities "http://www.example.org/entities/Entities"

Model:
	entities+=Entity*; // +=: 是一个集合。 *：0个或者多个 (+:至少一个)

Entity:
    // 用双引号或者单引号表示关键字。()?：optional part
	'entity' name=ID ('extends' superType=[Entity])? '{'
	attributes+=Attribute*
	'}';

Attribute:
	type=[Entity] array?=('[]')? name=ID ';';

// 可以对Attribute进行优化写法
Attribute:
	type=AttributeType name=ID ';';

AttributeType:
	elementType=[ElementType] (array?='[' (length=INT)? ']')?;

ElementType:
	BasicType | EntityType;

BasicType:
	typeName=('string' | 'int' | 'boolean');

EntityType:
	entity=[Entity];
```

## 3. xtend

documentation: https://www.eclipse.org/xtend/documentation/

1. Methods are public by default
2. you can declare multiple  public top-level types per file, and they will be compiled into separate Java files
2. constructor

```java
class MyFirstXtendClass {
    new () { // public by default
        ...
    }
    new (String s) {
        ...
    }
}
```

4. method
   1. The type of method parameters must always be specified
   2. Method parameters are always implicitly final

```java
class MyFirstXtendClass {
    def m1() {
        ""
    }
    def String m2() {
        ""
    }
    def m3() {
        return ""
    }
    def String m4() {
        return ""
    }
}
```

5. Fields and Variables
   1. val (for final fields and variables) Fields are private by default
   2. var (for non-final fields and variables)

```java
val s = 'my variable' // final variable
var myList = new LinkedList<Integer> // non final variable, type inferred
val aList = newArrayList
aList += "" // now the type of aList is inferred as ArrayList<String>
```

6. Operators
   1. `==` : 调用equals方法
   2. `===` : 表示 `==`
   3. 扩展了针对list的运算符

```java
val l1 = newArrayList("a")
l1 += "b"
val l2 = newArrayList("c")
val l3 = l1 + l2
println(l3) // [a, b, c]
```

7. 其他

```java
o.name = ... // 调用get set方法

val s1 = "my 'string'"
val s2 = 'my "string"'

// immutable collections and arrays
val aList = #["a", "b"] // creates a list of strings
val String[] anArray = #["a", "b"] // creates an array of strings
val aMap = #{"a" -> 0, "b" -> 1} // creates a Map<String, Integer>
```

8. Extension methods

```java
e.m() // m(e)
o.foo().bar() // bar(foo(o))
"my string".toFirstUpper // StringExtensions.toFirstUpper("my string")

val list = newArrayList("a", "b", "c")
println(list.head) // prints a
println(list.last) // prints b

// 静态导入
import static extension java.util.Collections.*

class ExtensionMethods {
    def myListMethod(List<?> list) {
        // some implementation
    }
    def m() {
        val list = new ArrayList<String>
        list.myListMethod // 默认可以作为 Extension methods 使用
    }
}

// 使用其他类实例方法作为extension methods
class MyListExtensions {

 def aListMethod(List<?> list) {
 // some implementation
 }

 def anotherListMethod(List<?> list) {
 // some implementation
 }
}
// 1. a field
class C {
 extension MyListExtensions e = new MyListExtensions
 def m() {
     val list = new ArrayList<String>
     list.aListMethod // equivalent to e.aListMethod(list)
     list.anotherListMethod // equivalent to e.anotherListMethod(list)
 }
}
// 2. a local variable
def m() {
 val extension MyListExtensions e = new MyListExtensions
 val list = new ArrayList<String>
 list.aListMethod
 list.anotherListMethod
}
// 3. a parameter declaration
def m(extension MyListExtensions e) {
 val list = new ArrayList<String>
 list.aListMethod
 list.anotherListMethod
}
```

9. it

```java
class ItExamples {
 def trans1(String it) {
     toLowerCase // it.toLowerCase
 }

 def trans2(String s) {
     var it = s
     toLowerCase // it.toLowerCase
 }
}
```

10. Lambda expressions

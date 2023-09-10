# Java Script

## 1. 序

是一门弱数据类型语言。

JavaScript权威网站: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript (MDN)

VS code插件： 

Error Lens. 	One Dark Pro.	Live Server(浏览器自动刷新)

1. JavaScript (是什么?) 是一种运行在客户端 (浏览器) 的编程语言，实现人机交互效果。
2. 作用(做什么?)
   * 网页特效 (监听用户的一些行为让网页作出对应的反馈)
   * 表单验证 (针对表单数据的合法性进行判断)
   * 数据交互 (获取后台的数据染到前端）
   * 服务端编程 (node.js)

3. JavaScript的组成(有什么? )
   * ECMAScript (规定了js基础语法核心知识)
   * Web APIs
     * DOM (Document Object Model——文档对象模型) 操作文档，比如对页面元素进行移动、大小、添加删除等操作
     * BOM (Browser Object Model) 操作浏览器，比如页面弹窗，检测窗口宽度、存储数据到浏览器等等

## 2. 书写

<font color=green>**书写位置**</font>

* 内部

* 外部
* 行内

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Document</title>
</head>
<body>
    <!-- 内联js -->
    <button onclick="alert('逗你玩~~~')">点击我月薪过万</button>

    <!-- 内部js -->
    <!-- 放在body结束的位置，保证页面元素已经加载完了之后 -->
    <script>
        alert('你好，js~')
    </script>

    <!-- 外部js -->
    <!-- 标签中间不要写代码，写的内容会被忽略 -->
    <script src="my.js"></script>
</body>
</html>
```

<font color=green>**注释**</font>

单行注释： `/`

多行注释： `/* */`

<font color=green>**语法**</font>

结束符：`;` ，可以加也可以不加

<font color=green>**输出**</font>

```javascript
// 1. 文档输出内容
// 作用:向body内输出内容
// 注意:如果输出的内容写的是标签，也会被解析成网页元素
document.write("我是div标签')
document.write("<h1>我是标题</h1>')
// 2. 页面弹出警告对话框
alert('要出的内容')
// 3. 控制台输出语法
console.log('控制台打印')
console.log(a, b) // 打印多个
```

<font color=green>**输入**</font>

```js
// 3.输入语句
let name = prompt('请输入您的年龄:‘)
```

## 3. 变量

命令规则：

* 不能是关键字
* 只能用数字、字母、下划线、$组成，数字不能开头
* 严格区分大小写，如 Age 和 age

命名规范：驼峰命名法。

```js
// 声明多个变量
let age = 18, name = 'zs'

// let 和 var
function example() {
  var x = 10;
  if (true) {
    var x = 20;
    console.log(x); // 输出20
  }
  console.log(x); // 输出20
}
example();

function example2() {
  let y = 10;
  if (true) {
    let y = 20;
    console.log(y); // 输出20
  }
  console.log(y); // 输出10
}
example2();

// 常量，不能被重新赋值
const PI = 3.14 // 声明的时候必须赋值
```

var的局限性：

>可以先使用再声明(不合理)
>
>var声明过的变量可以重复声明(不合理)
>
>变量提升、全局变量、没有块级作用域等等

## 4. 数据类型

<font color="green">**基本数据类型**</font>

| 类型      |                                  |
| --------- | -------------------------------- |
| number    | NaN也是数字类型                  |
| string    | 单引号、双引号或反引号包裹的数据 |
| boolean   | true, false                      |
| undefined | 声明变量但不赋值的默认值         |
| null      | 赋值了，但内容为空。null是对象   |

```javascript
console.log(undefined + 1) // NaN
console.log(null + 1) // 1
NaN === NaN // 返回NaN

// 模版字符串, 反引号 + $
let age = 18
document.write(`我${age}岁了`) // ES6(2015年)
document.write(`我${age + age2}岁了`)
```

对于一些特定的值，JavaScript会将其转换为`false`，这些值包括：

- `false`（布尔类型的`false`）
- `0`（数字类型的零）
- `''`（空字符串）
- `null`
- `undefined`
- `NaN`

<font color="green">**引用数据类型：object对象**</font>

***数组：***

```js
let arr = []
arr[0] = 1
arr[2] = 3 // 数据长度为3，arr[1]的值为undefined

let arr = [元素1, 元素2, 元素n] // 可以是不同的数据类型
let arr = new Array(1, 2, 3, 4)
arr[下标]
arr.lenght // 数组长度

arr.push(元素1, ..., 元素n) // 在数组末尾添加数据，返回该数组长度
arr.unshift(元素1, ..., 元素n) // 在数组开头添加数据，返回该数组长度
arr.pop() // 删除数组最后一个元素，返回删除元素，空数组返回undefined
arr.shift() // 删除数组第一个元素，返回删除元素，空数组返回undefined
arr.splice(startIndex, deleteCount) // 指定删除，批量删除
```

`typeof 变量` , `typeof(变量)` ：数据类型

<font color="green">**隐式数据类型转换**</font>

* `+`号两边只要有一个是字符串，都会把另外一个转成字符
* 串除了+以外的算术运算符 比如 `- ,*, /,==` 等都会把两个数据转成数字类型

```javascript
console.log(1 + 'a') // 字符串拼接 1a
console.log('abc' - 1) // NaN, NaN 是粘性的。任何对 NaN 的操作都会返回 NaN
console.log(+'123') // 转换为数字类型
```

<font color="green">**显示数据类型转换**</font>

```javascript
Number(变量)

parseInt(数据) // 只保留整数
console.log(parseInt('12px')) // 12
console.log(parseInt('12.34px')) // 12
console.log(parseInt('12.94px')) // 12

parseFloat(数据) // 可以保留小数
console.log(parseFloat('12px')) // 12
console.log(parseFloat('12.34px')) // 12.34
console.log(parseFloat('12.94px')) // 12.94
```

## 5. 运算符

**赋值运算符：**`+=,-=,*=,/=,%=`

**一元运算符：**`++,--`， 后置++先使用再自加

```javascript
let i = 1
console.log(i++ + ++i + i) // 7
```

**比较运算符：**

`==` : 只判断值 (一般不用)

`===` : 全等，值和数据类型

`!==` : 判断值是否一样

```js
// 不同类型之间会有隐式转换
console.log(2 == '2') // true
console.log(undefined == null) // true

console.log(2 === '2') // false
console.log(NaN === NaN) // false

if (num = 2){
    // 永远为真
}

// 字符串比较，是比较的字符对应的ASCII码
```

**逻辑运算符：** `&&, ||, !`

**运算符优先级：**

![](D:\myGit\note-taking\imgs\js\priority.jpg)

## 6. 流程控制

语句：不一定有值。

表达式：有结果。

```js
// 1. if 语句
if (condition) {
    // 只有一个语句大括号可以省略
} else if () {

} else {

}
// 2. switch 语句
switch (任何类型值) { // 使用的是严格相等（===）的比较操作符来进行匹配
    case 'case1':
        console.log('This is case 1')
        break
    case 'case2':
        console.log('This is case 2')
        break
    case 'case3':
        console.log('This is case 3')
        break
    default:
        console.log('This is the default case')
}

// 3. while
while (循环条件) {
	continue
    break
}

// 4. do while
do {

} while (循环条件)

// 5. for 循环
for (let i = 0; i < 5; i++) {

}
```

`条件 ? 满足条件执行的代码 : 不满足条件执行的代码` ：三元运算符

## 7. 函数

**function**

```javascript
// 具名函数
function myFunction(para1 = 0, para2 = 1) { // 形参不需要let; 默认值
    // 在这里编写你的代码
    // 如果需要返回值，没有就是返回undefined
    return 20
}

// 没有方法重载，函数名唯一，参数不匹配也能调用
myFunction(1)
myFunction(1, 2, 3)

// 匿名函数

```

**Debug:**

* 单步跳过：F10

* 进入方法：F11
* 跳出方法：Shift + F11

**作用域：**

* 全局作用域：整个script 标签内部 或者 一个独立的js文件。
* 局部作用域：函数作用域。

**Note: **

> 如果函数内部，变量没有声明，直接赋值，也当全局变量看，但是强烈不推荐。
>
> 函数内部的形参可以看做是局部变量。
>
> 变量访问：就近原则


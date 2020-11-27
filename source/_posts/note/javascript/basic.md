---
title: Javascript 基础
layout: post
comments: true
tags:
    - Javascript
categories:
    - - 笔记
      - Javascript
hidden: true
date: 2020-11-27 17:45:00
updated:
permalink: note/js/basic
---

[笔记索引](note/js/index)

# js 基础

## 数据类型

属于内置对象的一部分

### Number

```javascript
// <script src="Basic.js"></script>
"use strict"; // 开启严格模式

/* Number */
var x = 1; // 声明变量 ***建议使用let***
1 / 3 === 1 - 2 / 3; // false，存在计算误差。
123; // 整数123
0.456; // 浮点数0.456
1.2345e3; // 科学计数法表示1.2345x1000，等同于1234.5
-99; // 负数
0o10; // 八进制字面量
0b11; // 二进制字面量
NaN; // NaN表示Not a Number，当无法计算结果时用NaN表示
Infinity; // Infinity表示无限大，当数值超过了JavaScript的Number所能表示的最大值时，就表示为Infinity
```

<!--more-->

### 布尔

```javascript
/* 布尔 */
true === false;
isNaN(NaN);
var a = null; // 与 undedifined (未定义) 不同，null为"空".
```

### 可迭代 itrable

数组、键值对、集合可以用 forEach 方法遍历元素

```javascript
a.forEach(function (element, index, array) {
    // element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向指定对象本身
    console.log(element + ", index = " + index);
});
```

#### 数组

注意越界访问

```javascript
var arr = [1, 2, 3.14, "Hello", null, true]; // 允许越界访问
arr.length();
```

#### 键值对

```javascript
var m = new Map([
    ["Michael", 95],
    ["Bob", 75],
    ["Tracy", 85],
]);
```

#### 集合

```javascript
var s = new Set([1, 2, 3, 3, "3"]); // 3不会重复
```

### 对象

```javascript
var person = {
    name: "Bob",
    age: 20,
    tags: ["js", "web", "mobile"],
    city: { Beijing: "Capital" },
    hasCar: true,
    zipcode: null,
    "middle-school": "No.1 Middle School", // 特殊字符
    function: function name(params) {}, // 新写法见 OOP 一节
    get getter() {}, // getter & setter，见 Function 一节
    super: super.name(); // 对象超类
};
person.age; // 访问成员
person["middle-school"]; // 数组风格访问
person.zip; // undefined 不存在
delete person.city; // 删除
"hasCar" in person; // 判断是否存在
```

### 字符串

```javascript
('I\'m "OK"!');
("\x41"); // ASCII完全等同于 'A'
("\u4e2d\u6587"); // Unicode完全等同于 '中文'
`这是一个
多行
字符串`;

var str = "小明";
var age = 20;
var message = `你好, ${str}, 你今年${age}岁了!`; // 模板字符串

String.length();
name[0]; // 可以访问但不可被赋值
```

## 作用域

```javascript
// 自内到外查找变量名，全局作用域以对象window呈现
// 函数的局部变量应该在头部完成全部初始化 ***使用let以避免***
// 建议建立自己的全局变量空间
var a = 2; // var 拥有函数作用域，还有变量提升等复杂问题
let b = 16; // 块级变量声明
const c = 15; // 块级常量声明
```

## 变量提升

var 变量的声明会被提到代码最前方，初始化和调用则不会

## 表达式

```javascript
this // 指向函数的执行上下文
function // 定义了函数表达式
class // 定义了类表达式
function* // 定义了一个 generator 函数表达式
yield // 暂停和恢复 generator 函数
yield* // 委派给另外一个generator函数或可迭代的对象
async function // 定义一个异步函数表达式
await // 暂停或恢复执行异步函数，并等待promise的resolve/reject回调
[] // 数组初始化/字面量语法
{} // 对象初始化/字面量语法
/ab+c/i // 正则表达式字面量语法
() // 分组操作符
```

### 左表达式

左边的值是赋值的目标

### 属性访问符

```javascript
new // 运算符创建了构造函数实例
super([arguments]); // 调用 父对象/父类 的构造函数
super.functionOnParent([arguments]); // 关键字调用父类的构造器.
```

### 一元运算符

一元运算符只有一个操作数.

```javascript
delete expression; // 运算符用来删除对象的属性.
void expression; // 运算符表示表达式放弃返回值.
typeof expression; // 运算符用来判断给定对象的类型.
~expression; // 按位非运算符.
```

### 关系运算符

比较运算符比较二个操作数并返回基于比较结果的 Boolean 值
`=>` 不是运算符，而是箭头函数的表示符

```javascript
Number in Array; // 对象是否拥有给定属性.
Number instanceof Object; // 一个对象是否是另一个对象的实例.
```

### 相等运算符

```javascript
a == b; // 相等
c != d; // 不等
null === null; // 全等
a !== a; // 非全等
```

### 二元逻辑运算符

逻辑运算符典型的用法是用于 boolean(逻辑)值运算, 它们返回 boolean 值

```javascript
true && false; //逻辑与.
false || true; //逻辑或.
```

### 三元运算符

```javascript
condition ? ifTrue : ifFalse;
```

### 解构赋值

```javascript
var [x, y, z] = ["hello", "JavaScript", "ES6"]; // 使x、y、z分别对应数组当中的变量
var [, , z] = ["hello", "JavaScript", "ES6"]; // 可以选择性地赋值
var { name, single = true } = { name: "小明", x: 100, y: 200 }; // 可以带有默认值，否则返回undefined
({ x, y } = { name: "小明", x: 100, y: 200 }); // 对于已声明变量，需要小括号以防止被当作块解析
```

## 语句与声明

### 流程控制

#### 条件

JavaScript 把 null、undefined、0、NaN 和空字符串''视为 false，其他值一概视为 true

```javascript
if (person.age >= 18) {
    alert("adult");
} else if (age >= 6) {
    alert("teenager");
} else {
    alert("kid");
}
```

#### 循环

##### for

-   for in 依 Index 循环，常用于对象
-   for of 依 内容 循环，多用于数组等可迭代对象
-   forEach 依 内容 循环方法，多用于数组等可迭代对象
-   for await...of 异步循环，存在兼容问题

```javascript
var x;
var i;
for (i = 1; i <= 10000; i++) {
    x = x + i;
}
```

##### while

```javascript
var n;
while (n > 0) {
    x = x + n;
    n = n - 2;
}
```

##### switch

```javascript
switch (key) {
    case value1:
    case value2:
        // 多对一
        break;
    case value:
        // 匹配
        break;
    default:
        // 无匹配
        break;
}
```

##### do while,

do 内至少会执行一遍

```javascript
loop1: do {
    n = n + 1;
    continue loop1;
} while (n < 100);

break; // 跳出
continue; // 下一迭代
// lable 见上例，配合上二者使用
Empty; // 空
```

## 声明

var 变量，会被提升，拥有函数作用域
let 块级变量
const 常量

## 其他

```javascript
debugger; // 添加断点

// 导入
import {} from "module";

// 导入时需要名称对应
export let name1, name2; // 导出单个特性
export { name1, name2, nameN }; // 导出列表
export { variable1 as name1, variable2 as name2, nameN }; // 重命名导出
export const { name1, name2: bar } = o; // 解构导出并重命名
// 默认导出，导入时不需要名称对应
export default expression; // 一个模块只能有一个默认导出
export * from "module"; // 模块桥接，非默认到处
```

## 面向对象

### 基于类

-   类声明不会受到变量提升影响，且默认严格
-   本质是基于原型的语法糖

#### 声明

1.  声明

    ```javascript
    class Student {
        // 构造函数
        constructor(name) {
            // 实例属性（各个对象在初始化时定义）
            this.name = name;
            this.age = super.age(); // 调用超类
        }
        // 原型方法（共有）
        hello() {
            alert(`Hello, ${this.name}!`);
        }
        // 静态方法
        static bye() {
            alert(`Bye, ${this.name}!`);
        }
        // 调用自身静态方法
        rebonjour() {
            this.bye();
        }
        // getter & setter
        get value() {
            return this.name;
        }
        // 异步函数
        async aurevoir() {
            return;
        }
        // 生成器
        *generator() {
            yield;
        }
        // 异步生成器
        async *asyncGenerator() {}
    }
    ```

2.  类表达式

    -   匿名类

    ```javascript
    let Rectangle = class {
        constructor(height, width) {
            this.height = height;
            this.width = width;
        }
    };
    ```

    -   具名类

    ```javascript
    let Rectangle = class Rectangle2 {
        constructor(height, width) {
            this.height = height;
            this.width = width;
        }
    };
    ```

#### 继承

```javascript
class PrimaryStudent extends Student {
    constructor(name, grade) {
        super(name); // 调用父类实例属性
        super.hello(); // 调用父类原型方法
        this.grade = grade;
    }
}
```

-   Mix-in

    没有多继承，但可以通过继承声明新的类，在其中添加

    ```javascript
    var firstMixin = (Base) =>
        return class extends Base {
            first() {}
        };// 返回匿名类

    var secondMixin = (Base) =>
        return class extends Base {
            second() {}
        };// 返回匿名类

    class Foo {}
    class Bar extends firstMixin(secondMixin(Foo)) {}
    ```

### 基于原型

-   与基于类 JS 不区分对象与类，所有对象都可以作为`原型`使用，实例化类似于继承

```javascript
// 构造函数
function Student(name) {
    this.name = name; // 成员变量
    this.hello = function () {
        // 成员函数
        alert("Hello, " + this.name + "!");
    };
}

let me = new Student("我"); // 使用 new 将 me 声明为对象

// 此时原型链为 me -> Student.prototype -> Object.prototype -> null
// Student.prototype.constructor 指向 Student

Student.prototype.hello = function () {
    // 原型方法，各实例共有
    alert("Hello, " + this.name + "!");
};
```

#### 继承

原型继承，强行构造原型链

```javascript
// new someone -> Child.prototype -> F.prototype = Parent.prototype-> Object.prototype-> null
//

function inherits(Child, Parent) {
var F = function () {}; // 中介
F.prototype = Parent.prototype; // F 原型指向 Parent 原型
Child.prototype = new F(); // 构造 Child.prototype -> F.prototype
Child.prototype.constructor = Child; // 修复 constructor 指向
}
···
```

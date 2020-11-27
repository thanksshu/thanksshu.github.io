---
title: Javascript 函数
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
permalink: note/js/function
---

[笔记索引](note/js/index)

# js 函数

## 声明

```js
// 表达式赋值
var x = function (a) {
    alert(a);
};

// 声明
function y(a) {
    alert(a);
}

// 函数构造（慢，不推荐）
new Function(arguments, functionBody);
```

<!--more-->

## 调用

可以任意传参，注意参数类型
可以默认传参
另有 argument 代表所有传入参数，类似数组

```js
function z(a = 12, b, ...rest) {
    rest; // rest 变量用于多余的参数：Spread/Rest 操作符
    arguments[0]; // argument 对象，以数组形式储存参数
}
```

## 对象方法

```js
var xiaoming = {
    age: function () {
        var y = new Date().getFullYear();
        return y - this.birth;
        // this 会指向对象本身，
        // 但是如果是函数内的函数、或者处于全局空间下，即出错（为 window 或 未定义）
        // 函数内函数可以在外层函数将 this 赋值保留再在内层使用
    },
};
// 使用传参解决，指定 this（可以为null）
y.apply(对象, [参数1, 参数2]); // 用数组传参
y.call(对象, 参数1, 参数2); // 逐个传参
y.bind(对象, 参数1, 参数2); // 返回新的函数
```

## 对象 getter & setter

在对象内定义 getter setter 函数
每次访问、修改都会触发相应函数

```js
const obj = {
    get getter() {
        return "getter";
    },
    set setter() {
        return "setter";
    },
};
```

## 一种装饰器

```js
var count = 0;
var oldParseInt = parseInt; // 保存原函数

window.parseInt = function () {
    count += 1;
    return oldParseInt.apply(null, arguments); // 调用原函数
};
```

## 高阶函数

接受函数作为参数的函数

```js
let arr = [1, 2, 3, 5, 9, 0];
arr.map(x); // 以 x 函数对 arr 内元素逐个运算并返回这个数组
arr.reduce(x); // [x1, x2, x3, x4].reduce(f) = f(f(f(x1, x2), x3), x4)
arr.filter(z); // 根据 z 返回的 true 或者 false 决定是否丢弃元素
arr.sort(y); // y 为排序函数，对于两个元素x和y，如果认为x < y，则返回-1，如果认为x == y，则返回0，如果认为x > y，则返回1
```

另外的高阶函数：

-   `every()` 判断数组的所有元素是否满足测试条件，
-   `find()` 查找返回符合条件的第一个元素，否则返回 undefined
-   `findIndex()` 返回第一个找到元素的位置
-   `forEach()` 把每个元素依次作用于传入的函数，但不会返回新的数组，用于遍历

## 箭头函数

其实就是匿名函数
使得 apply() 方法的第一个参数始终指向相应对象
没有 this、arguments，如果能调用，一定来自父级函数作用域

```js
var Power2 = (argu) => x _ x; // 当函数块内只有一行，可以省略块标记
// 等同于
var Power2 = function (argu) {
return argu _ argu;
};
```

如果想要返回对象

```js
(x) => ({ foo: x }); // 记得加括号
```

创建一个匿名函数并立刻执行

```js
((i) => {
    console.log(i);
})(i);
```

对于创建匿名函数并即刻运行也可以使用声明式，+ 可以换为其他运算符

```js
(function name(params) {
    console.log(params);
})(params);
```

## 生成器

生成可迭代对象

```js
function* fib(max) {
    // 记得 function 带 * 号
    (a = 0), (b = 1), (n = 0);
    while (n < max) {
        yield a; // 返回值
        yield* [1, 2, 3]; // 委托给另外的 iteratable 对象
        [a, b] = [b, a + b];
        n++;
    }
    return;
} // 用 next() 、 for of 、 forEach 循环
// 或
new GeneratorFunction(arguments, functionBody);
```

## 异步函数

`async function name([param[, param[, ... param]]]) { statements }`
可以结合 Promise 使用
返回的 Promise 对象会运行执行(resolve)异步函数的返回结果，或者运行拒绝(reject)
跨浏览器性能注意

```js
async function async() {} // 一般声明
async () => {}; // 箭头函数

// [return_value] = await expression; // expression 不是 Promise 时会转换并等待结果
// await 使得 async function 等待一个 Promise 的结果再继续运行
async function async() {
    return await 20; // 20
}
```

链式回调重写

从

```js
function getProcessedData(url) {
    return downloadData(url) // 返回一个 promise 对象和下一级的 e
        .catch((e) => {
            return downloadFallbackData(url); // 返回一个 promise 对象和下一级的 v
        })
        .then((v) => {
            return processDataInWorker(v); // 返回一个 promise 对象
        });
}
```

到

```js
async function getProcessedData(url) {
    let v;
    try {
        v = await downloadData(url); // 等待返回一个 promise 对象和 v
    } catch (error) {
        v = await downloadFallbackData(url); // 等待返回一个 promise 对象和 v
    }
    return processDataInWorker(v); // 返回一个 promise 对象
    // async function 会隐式传返回值给 Promise.resolve，不再需要 await
}

// 并行，同时开始
var parallel = async function () {
    await Promise.all([
        (async () => {
            return console.log(await resolveAfter2Seconds());
        })(),
        (async () => {
            return console.log(await resolveAfter1Second());
        })(),
    ]);
};
```

## 闭包

-   在一个内部函数中对外部作用域的变量进行引用，内部函数即形成闭包
-   闭包可以使函数有 固定 的 “私有环境”，外部无法访问
-   高阶函数返回值是一个函数，可以返回闭包

```javascript
function generateClosure() {
    // 外层
    let x = 1;
    return function f() {
        // 内层
        return x; // 声明时引用了外部的 x 变量，无关传参
    };
}
let closure = generateClosure(); // 外层函数执行时返回值形成闭包
```

### 循环闭包

```javascript
function generateFunctions() {
    let f_list = [];
    for (var i = 0; i < 5; i++) {
        function f() {
            return i;
        }
        f_list.push(f);
    }
    return f_list;
}
f_list = generateAnotherClosure();
```

`f_list[0]()` 直到 `f_list[4]()` 都返回 5，而不是 0、1、2、3、4，f 内的 i 是在 for 结束时确定的，所以为 5

闭包解决,创建一个函数并执行形成闭包

```javascript
function generateFunctionsWithClosure() {
    let f_list = [];
    for (var i = 0; i < 5; i++) {
        function g(i) {
            // 外层
            return function f() {
                // 内层，此函数将在 g 被调用时形成闭包，与它本身是否被返回无关
                return i;
            };
        }
        f_list.push(g(i)); // 执行外层函数使其返回闭包
    }
    return f_list;
}
f_list = generateFunctionsWithClosure();
```

不过，闭包对性能不友好

### let

如果不使用闭包，可以用 let 解决，使每个块有自己的作用域

```javascript
for (var i = 0; i < 5; i++) {
let item = i;
setTimeout(function () {
console.log(item);
}, 1000 _ i);
}
```

同样地：

```javascript
for (let i = 0; i < 5; i++) {
setTimeout(function () {
console.log(item);
}, 1000 \_ i);
}

```

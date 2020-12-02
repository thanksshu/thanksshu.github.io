---
title: Javascript 全局对象
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
permalink: /note/js/global-object
---

[笔记索引](/note/js/index)

# 全局对象

## 对象相关

值属性

```js
Infinity; // 超过 Number 容量
NaN; // 不是 Number
undefined; // 未定义
null; // 空
```

<!--more-->

属性方法

```js
eval(string); // 将 string 当作脚本执行
isFinite(); // 判断是否是……
isNaN();
parseFloat(); // 转换为……
parseInt();
decodeURI(encodedURI); // 解码含有特殊字符的完整 URL
decodeURIComponent(); // 解码含有特殊字符的 URL
encodeURI(encodedURI); // 编码
encodeURIComponent();
```

## 基本对象

```js
Object;
Function;
Boolean;
Symbol; // 创建一个全局唯一的对象，无法使用 new
Error; // 以及 Error 一家
```

## 数字类

```js
Number; // 双精度IEEE 754 64位浮点
Number.isInteger(xxx); // 确定传递的值类型是 Number ，且是整数。
Number.isSafeInteger(xxx); // 确定是否在 +-(2^53 - 1) 之间

Math; // 数学类
```

## 包装对象

注意：

-   不要使用 new Number()、new Boolean()、new String() 创建包装对象
-   用 parseInt() 或 parseFloat() 来转换任意类型到 number
-   用 String() 来转换任意类型到 string ，或者 toString() 方法；例如 (123).toString()，注意小括号
-   通常不必把任意类型转换为 boolean 再判断，因为可以直接写 if (myVar) {...}
-   typeof 操作符可以判断出 number、boolean、string、function 和 undefined
-   判断 Array 要使用 Array.isArray(arr)
-   判断 null 请使用 myVar === null
-   判断某个全局变量是否存在用 typeof window.myVar === 'undefined'
-   函数内部判断某个变量是否存在用 typeof myVar === 'undefined'

```js
var n = new Number(123);
typeof n; // Object

/* getter */
const obj = {
    log: ["a", "b", "c"],
    get latest() {
        return this.log[this.log.length - 1];
    },
};

obj.latest; // 给予一个对象伪属性，用来读取

/* setter */
const obj = {
    log: ["a", "b", "c"],
    set latest(value) {
        this.log.push(value);
    },
};

obj.latest; // 给予一个对象伪属性，用来读取
```

## Date 日期对象

```js
new Date(); // 实例化时的时间
new Date(value); // Unix 时间戳
new Date("2015-06-24T19:49:22.875+08:00"); // 符合 ISO8601 的时间，不建议使用
new Date(year, monthIndex, day, hours, minutes, seconds, milliseconds); // 可以只精确到月份

//成员方法
Date.prototype.getxxx(); // 成员 getter 方法 **_月份从 0 开始_**
Date.prototype.setxxx(); // 成员 setter 方法
Date.prototype.toxxx(); // 成员 conversion getter 方法

// 静态方法
Date.now(); // 当前 Unix 时间戳
Date.UTC(year, month, date, hrs, min, sec, ms); // 转换时间到 UTC Unix 时间戳
Date.parse; // 解析 ISO8601 字符串，**_不推荐_**
```

## Error 错误处理

```js
// 捕捉
try {
    // 执行代码
    throw new Error(); // 实例化并抛出一个错误对象
} catch (error) {
    // 出错时执行
    if (error instanceof Error) {
        // 使用 Error 类分类错误
    }
} finally {
    // 最后一定执行
}
```

错误被抛出后会层层向上（冒泡），直到引擎报错，可以在合适位置“一网打尽”

## JSON 对象

```js
var s = JSON.stringify(); // 将对象序列化为 json 对象
JSON.parse(); // 反序列化
```

## Promise 承诺对象

### 创建

```js
let promise = new Promise(function (resolve, reject) {
    // 初始化时状态为 Pending
    if (success) {
        // 如果成功调用 resolve()
        resolve(value); // 改写状态为 fulfilled，并返回 value 给回调函数（success_value）
    } else {
        // 失败则调用 reject()
        reject(error); // 改写状态为 rejected，并返回 error 给回调函数（reject_error）
    }
});
```

### 调用

```js
promise.then(
    (success_value) => {
        console.log(success_value); // success_value 来自 resolve 传递的 value
    }, // 成功的回调函数
    (reject_error) => {
        console.log(reject_error); // reject_error 来自 reject 传递的 error
    } // 失败的回调函数
);
```

### 实例化方法，返回一个对象

```js
new Promise.all(iterable); // 内部承诺对象都成功才会成功
new Promise.race(iterable); // 内部任意一个承诺对象有结果则立即回调
new Promise.reject(reason); // 返回一个失败的对象，并立即回调
new Promise.resolve(value); // 如果有 then 则正常执行，否则直接 fulfilled 回调
```

### 成员方法

```js
Promise.prototype.catch(onRejected); // 添加一个拒绝回调，返回一个新的 promise 并传参
Promise.prototype.then(onFulfilled, onRejected); // 添加解决和拒绝回调，返回一个新的 promise 并传参
Promise.prototype.finally(onFinally); // 添加无论成功与否都会回调，返回新 promise
```

### 使函数拥有 promise 功能

若欲使函数拥有 promise 功能，需让其返回一个 promise

```js
let promise = function (value) {
    value; // 可以处理传入参数
    new Promise((resolve, reject) => {
        Empty; // 异步处理
    });
};
```

### 通过连续使用 then 实现链式回调

从回调地狱

```js
doSomething(function (result) {
    doSomethingElse(
        result, // doSomething() 的返回值
        function (newResult) {
            // 新的回调
            doThirdThing(
                newResult, // doSomethingElse() 的返回值
                function (finalResult) {
                    console.log("Got the final result: " + finalResult);
                },
                failureCallback
            );
        },
        failureCallback
    );
}, failureCallback);
```

到链式调用

```js
doSomething()
    .then(function (result) {
        return doSomethingElse(result);
        // 返回一个 promise 对象 和下一级的 newResult，result 来源于 doSomething() 的 resolve
    })
    .then(function (newResult) {
        return doThirdThing(newResult);
        // 返回一个 promise 对象，newResult 来自于 doSomethingElse () 的 resolve
    })
    .then(function (finalResult) {
        console.log("Got the final result: " + finalResult);
    })
    .catch(failureCallback);
```

### 错误传递

抛出的错误会一直向后传递直到找到处理他的回调函数

## RegExp 正则对象

### 创建对象

```js
var re1 = /ABC\-001/; // 注意转义符
var re2 = new RegExp("ABC\\-001");
```

### 常用方法

```js
re.test("010-12345"); // 检查是否符合正则

"a,b, c d".split(/[\s\,]+/); // ['a', 'b', 'c', 'd'] // 用于切分字符串
```

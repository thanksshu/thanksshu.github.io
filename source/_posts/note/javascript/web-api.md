---
title: Javascript WebAPI
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
permalink: note/js/web-api
---

[笔记索引](note/js/index)

# Web API

由浏览器提供的一系列 API

## DOM 树对象

Document -> Node -> EventTarget

```js
document; // 是本网页，属于 Document 实例

Document.title; // title 内容
Document.body; // body 内容
Document.cookie; // cookie 内容；注意安全性，js可以被第三方调用，后端应配合使用 httpOnly 的 cookie
```

<!--more-->

### 编辑 DOM 树

#### 获取

```js
Document.getElementById(); // 通过ID获取
Document.getElementsByTagName(); // 通过标签获取，标签不唯一
Document.lastElementChild; //最后一个子节点
Document.children; // 所有直属子节点
Document.querySelector(); // 通过 选择器 获取
Document.querySelectorAll();
```

getElement 返回一个（多个）HTMLElement， HTMLElement -> Element -> Node -> EventTarget
getElements 返回 HTMLCollection , 内有多个 Element

#### 更新

```js
Element.innerHTML = 'ABC <span style="color:red">RED</span> XYZ'; // 无编码，有XSS注入风险
HTMLElement.innerText = '<script>alert("Hi")</script>'; // 自动编码
Element.style.alignContent = "true"; // 更改CSS，CSS的横线被理解为小驼峰
Element.setAttribute(); // 设置属性
Element.setProperty();
```

#### 添加

```js
Element.appendChild(newElement); // 添加到最后
Element.insertBefore(newElement, referenceElement); // 指定插入位置的前面
```

referenceElement 可以通过遍历 children 获得

#### 删除

```js
Element.removeChild(); // 删除子节点，一般会调用父节点删除自己
```

#### 操作表单

```js
Element.value; // 用于 text、password、hidden 以及 select 以获得值
Element.checked; // 用于复选框，为布尔值
Element.value = ""; // 改值
```

上传文件使用 <input type="file">
表单的`enctype`必须指定为`multipart/form-data`，`method`必须指定为`post`

## URL 对象

```js
Document.location.href; // URL
Document.location.protocol; // 'http'
Document.location.host; // 'www.example.com'
Document.location.port; // '8080'
Document.location.pathname; // '/path/index.html'
Document.location.search; // '?a=1&b=2'
Document.location.hash; // 'TOP'

Document.location.assign(); // 加载新页面
Document.location.reload(); // 刷新
```

## 关于 DOM

### 节点

-   元素节点 `Node.ELEMENT_NODE(1)` 对应标签元素
-   属性节点 `Node.ATTRIBUTE_NODE(2)` 对应标签的属性
-   文本节点 `Node.TEXT_NODE(3)` 对应标签内容

-   CDATA 节点 `Node.CDATA_SECTION_NODE(4)` XML 节点
-   实体引用名称节点 `Node.ENTRY_REFERENCE_NODE(5)`
-   实体名称节点 `Node.ENTITY_NODE(6)`
-   处理指令节点 `Node.PROCESSING_INSTRUCTION_NODE(7)`

-   注释节点 `Node.COMMENT_NODE(8)` 对应注释
-   文档节点 `Node.DOCUMENT_NODE(9)` 对应 document 对象即根节点
-   文档类型节点 `Node.DOCUMENT_TYPE_NODE(10)` 对应 `<!DOCTYPE XXX>`
-   文档片段节点 `Node.DOCUMENT_FRAGMENT_NODE(11)` 对应 DocumentFragment 节点

-   DTD 声明节点 `Node.NOTATION_NODE(12)` 声明 DTD

## Event 事件对象

> Event -> EventTarget

1. 注册事件监听器

可以存在多个回调

```javascript
EventTarget.addEventListener(
    "Event",
    // 这里的 Litsener 必须是一个实现了 EventListener 接口的对象
    {
        handleEvent: function (event) {
            // 表达式函数
            // event 参数为基于 Event 的对象
            event.stopPropagation(); // 阻止冒泡
            event.preventDefault(); // 阻止默认事件
            return false; // 阻止默认事件，并阻止冒泡
        },
    },
    false // useCapture 是否捕获事件
);
```

2. 从事件队列删除

```javascript
EventTarget.removeEventListener("Event", function (event) {
    listener;
});
```

3. 使用事件处理器（onEvent）注册，回调唯一

```javascript
EventTarget.onEvent = function (event) {
    handler;
};
```

4. 创建事件

```javascript
var event = new Event("build"); // 创建 CustomEvent -> Event 亦可
EventTarget.dispatchEvent(event); // 分发绑定
EventTarget.addEventListener(
    "build",
    function listener(event) {
        listener;
    },
    false
);
```

5. 事件委托

-   `Event.target` 引用分发事件的元素
-   `Event.currentTarget` 则引用绑定事件的元素，常用于复用监听器

```javascript
function hide(e) {
    if (e.target.nodeName.toLocaleLowerCase === "li") {
        // e.target 引用子元素
        console.log("the content is: ", target.innerHTML);
    }
}

// 添加监听事件到列表，当每个子元素被点击的时候都会触发。
ul.addEventListener("click", hide, false);
```

## window 窗口对象

```js
window.navigator; // navigator 浏览器对象
window.screen; // screen 屏幕对象
```

## 历史对象

```js
window.history; // 历史对象

History.length; // 历史记录数量
History.state; // 历史堆栈顶部的状态

// History 接口不继承任何方法

History.back(); // 后退
History.forword(); // 前进
History.go(-2); // 以现在为 0 前、后跳转

History.pushState(state_obj, title, url); // 将记录压入历史堆栈
History.replaceState(state_obj, title, url); // 将当前记录替换
// state_obj 是一个 对象；popstate 事件被触发时，其 state 属性包含 state_obj 的副本
window.onpopstate = function (event) {
    alert(event.state);
};
```

title 为标题，一般使用空字符串
url 可选
会改变 URL 但是页面不会跳转（onpopstate 不被触发）
这两个方法通常与 window.onpopstate 事件合用
每当处于激活状态的历史记录条目发生变化时（后退、前进、跳转），popstate 事件就会在对应 window 对象上触发
可以取代 #Hash 实现单页面应用

## XHR 网络请求对象

XMLHttpRequest -> XMLHttpRequestEventTarget -> EventTarget

```js
XMLHttpRequest(); // 构造函数
```

### 属性

```js
XMLHttpRequest.readyState; // 返回请求的状态码
```

0 UNSENT 代理被创建，但尚未调用 open() 方法
1 OPENED open() 方法已经被调用
2 HEADERS_RECEIVED send() 方法已经被调用，并且头部和状态已经可获得
3 LOADING 下载中，此时 responseText 属性已经包含部分数据
4 DONE 下载操作已完成

```js
XMLHttpRequest.UNSENT === 0; // true
```

```js
XMLHttpRequest.response; // 返回整个响应体（response body）。
XMLHttpRequest.responseText; // 返回对请求的响应，如果请求未成功或尚未发送，则返回 null。
XMLHttpRequest.responseType; // 一个用于定义响应类型的枚举值（enumerated value）。
XMLHttpRequest.responseURL; // 返回响应的序列化（serialized）URL，如果该 URL 为空，则返回空字符串。
XMLHttpRequest.responseXML; // 返回一个XML响应，如不能则返回 null。
XMLHttpRequest.status; // 返回请求的响应状态。
```

### 方法

```js
XMLHttpRequest.open(method, url, async, user, password); // 初始化请求，重复调用等同 abort()
// url 为相对，跨域访问需要特别设置
XMLHttpRequest.setRequestHeader(header, value); // 设置请求头
XMLHttpRequest.sent(body); // 发送请求，异步请求即刻返回
XMLHttpRequest.abort(); // 中止请求
```

### 事件

```js
abort; // 停止 XMLHttpRequest.abort()
error; // 错误
load; // 成功
loadend; // 结束，无论结果
loadstart; // 开始接收
progress; // 开始接收后周期触发
timeout; // 超时
```

### 跨域访问

可以设置后端代理
使用 JSONP ，只响应 GET，返回 JS 代码
使用 CORS，需要对方设置 Access-Control-\* 参数

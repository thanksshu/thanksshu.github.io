---
title: Markdown语法笔记
layout: post
comments: true
tags:
    - Markdown
categories:
    - 笔记
    - Markdown
date: 2018-12-27 16:56:03
updated:
permalink: /note/md
---

在这里简单记下 MD 的语法以备后续使用

> 2020/03/31 根据 [CommonMark Spec 0.29](https://spec.commonmark.org/0.29/) 更新

<!-- more -->

---

1. 换行

```markdown
换行

换行
```

解析为 `<p>强制</p><p>换行</p>`

```markdown
硬\
换行
```

解析为 `<p>硬<br />换行</p>`

---

2. 多级标题

```markdown
# 一级标题

## 二级标题
```

```markdown
# 一级标题

## 二级标题

### 三级标题

#### 四级标题

##### 五级标题

###### 六级标题
```

标题最多六级

---

3. 字体样式

```markdown
_这是倾斜的文字_

_这是倾斜的文字_

**这是加粗的文字**

**这是加粗的文字**

**_这是斜体加粗的文字_**

**_这是斜体加粗的文字_**
```

---

4. 引用

```markdown
> 引用内容

> > [_斜体引用链接_](超链接地址 "title")

> > ---

> > > > > > > _斜体引用_
```

---

5. 分割线

```markdown
---
```

```markdown
---
```

```markdown
---
```

---

6. 链接

```markdown
[_斜体显示名_](/链接地址 "title")
```

```markdown
![显示名](/图片地址 "title")
```

```markdown
<链接地址>
```

```markdown
[参考链接名]: /链接地址 "title"
```

参考链接是不可见的

---

7. 列表

```markdown
-   列表内容

*   列表内容

-   列表内容
```

````markdown
1. 列表内容
2. 列表内容

````markdown
```markdown
1. 列表内容
2. 列表内容
```
````
````

```markdown
4. 列表内容
    1. 列表内容
    - `列表代码内容`
    - ***
```

---

8.  代码块

```markdown
`单行代码`
```

`````markdown
````语言名称
多行代码
  以及缩进

```语言名称
代码块内代码块
  以及缩进
```
````
`````

    使用四个空格的代码块
      以及缩进

```
~~~语言名称
多行代码
~~~
```

---

9. HTML

```markdown
<HTML 标签>
```

---

---
title: 前端工程化
date: 2022-11-25 13:36:45
tags: 工程化
---

**一、html**

**1、基本规范**

1.1 使用 <!Doctype html> 文档类型声明，h5 的最新声明方式

```html
<!DOCTYPE html>
```

1.2 设置网页的编码以及文档类型

```html
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
```

1.3 设置网页的渲染模式，按照最新的模式渲染

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
```

**2**、CSS 和 JavaScript 引入 \* \*

2.1 引入 CSS 时必须指明 rel="stylesheet"

```html
<link rel="stylesheet" href="page.css" />
```

2.2 JavaScript 应当放在页面末尾，或采用异步加载。

```html
<body>
  <!-- a lot of elements -->
  <script src="’init-behavior.js’"></script>
</body>
```

**二、CSS**

**1、书写**

1.1 禁止使用层级过深的选择器，允许最多三级

```css
.container .box .text {
  color: #000000;
}
```

1.2 属性书写顺序遵循以下规则

```css
.container {

  /* 位置属性 */
  display: block;
  float: left;
  position: absolute;
  top: 10px;
  right: 10px;
  /* 盒模型 */
  box-sizing: border-box;
  width: 1000px;
  height: 500px;
  margin-top: 10px;
  margin-right: 10px;

  /* 文本属性 */
  color: #000;
  text-align: center;
  font-size: 16px;
  font-weight: bold;
  / * 背景属性  */
  background-color: #fff;
  / * 其他  */
  z-index: 1;
}
```

**2、命名**
选择器命名必须使用小写，单词间使用-分隔，命名语义化

```css
/* 应用列表 */
.application-manage-list {
  width: 1000px;
}
```

**三、JS**

**1**、变量

命名方式：[小驼峰]()

命名规范：[前缀名词]()

命名建议：语义化

```js
// 友好
let maxCount = 10;
let tableTitle = "LoginTable";

// 不友好
let setCount = 10;
let getTitle = "LoginTable";
```

**2**、常量

命名方式：[全部大写]()

命名规范：[使用大写字母和下划线来组合命名，下划线用以分割单词]()

命名建议：语义化

```js
const MAX_COUNT = 10;
const URL = "http://www.foreverz.com";
```

**3**、函数

命名方式：[小驼峰式命名法]()。

命名规范：[前缀应当为动词]()。

命名建议：语义化

```js
// 是否可阅读
function canRead() {
  return true;
}

// 获取名称
function getName() {
  return this.name;
}
```

**4、构造函数**

命名方式：大驼峰式命名法，首字母大写

命名规范：前缀为名称。

命名建议：语义化

```js
// 例子:
const getPromise = new Promise((resolve) => {
  resolve();
  // 或 reject()
});
```

**5**、函数/方法 注释必须包含函数说明，有参数和返回值时必须使用注释标注，参考下面样例。参考 jsdoc

```js
正例：
/**
* 函数描述 *
* @param {string} p1 参数1的说明
* @param {string} p2 参数2的说明，比较长
*     那就换行了.
* @param {number=} p3 参数3的说明（可选）
* @return {Object} 返回值描述
*/
function foo(p1, p2, p3) {
    var p3 = p3 || 10;
    return {
        p1: p1,
        p2: p2,
        p3: p3
    };
}
```

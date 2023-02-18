---
title: 前端工程化
date: 2020-05-19 20:36:45
tags: 工程化
categories: 工程化
excerpt: "简单来说，前端工程化可以提升开发体验、提高开发效率和质量、提升应用的访问性能，一切以提高效率、降低成本、质量保证为目的的手段都属于工程化。注意：本文在前端研发生命周期仅包含 基本代码书写 的规范。"
---

## 基本规范

**一、html**

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

## vue

### 全局方法、事件，组件，js

1、禁止业务逻辑的 mixins 进行全局注册
2、使用 addEventListener 注册事件，注意需要销毁，防止内存泄漏等。
3、若不需要双向绑定数据，尽量把变量定义为 data 函数的内部变量，不用添加在 return 对象里。
4、全局组件的 name 统一前缀加'p',参考 src/components/remote-select/index.vue 组件的 name 命名方式

### css

1、vue 文件尽量使用 scoped 限制作用范围

### 权限方面

按钮权限命名要求： 模块名:请求 api 路径 例如 sku:/wawa-open-common-server/upload/image
菜单创建要求：每创建一个菜单需要创建一个对应的查看按钮权限

### 文件目录结构

项目文件结构一般都大同小异，可以参考 scm 项目的文件说明

- api: 存放整个项目的请求 api
- assets: 存放项目静态资源
- common: 公共 js 功能，一般挂载在 vue.prototype 上
- components: 公共组件，包括框架基础界面布局，基于业务的通用组件
- config: 配置文件，配置全局请求的域名,项目公共的数据，配置全局表格的方法
- constants: 存放整个项目的不同模块所需的枚举值，供./filter 过滤器使用
- filter: 存放过滤器函数
- mixin: 存放混合函数，一般不全局混合注册，按需注册
- router: 全局路由，定义项目所有的路由，在登录的时候根据接口返回，按需注册路由，进行菜单权限控制
- store: 存放 vuex 一些函数，目前保存菜单路由，全局表格 vxe-table 的高度计算函数
- until: 一些工具函数,按需导入使用
- views: 业务页面
- .gitlab-cli.yml: gitlab 自动部署配置的文件，一般只需要更改 scripts 与 tags 里的内容

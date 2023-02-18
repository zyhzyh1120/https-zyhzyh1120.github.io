---
title: require.context(自动加载js模块等作用)
date: 2022-12-21 23:21:10
tags: router
categories: vue-router
excerpt: vue-router
---

## vue-router

**使用的简单记录，备忘。**

### 路由懒加载

_vue 作为单页面应用, 如果不采用按需加载的方式, 首屏加载是非常慢的,即使做了 loading 也是严重影响用户体验，所以按需加载路由是一个项目的基础构建。(首屏加载优化...后续会记录)_

#### 目前常用的方法

##### Vue 异步组件

```js
// 一个组件生成一个js文件
{
  path: '/',
  name: 'Index',
  component: resolve => require(['@/view/index'], resolve)
},{
  path: '/my',
  name: 'My',
  component: resolve => require(['@/view/my/index'], resolve)
},{
  path: '/setting',
  name: 'Setting',
  component: resolve => require(['@/view/setting/index'], resolve)
}
```

#### 使用 import

```js
// router.js
// 可以指定 webpackChunkName (如下列 /* webpackChunkName: 'Setting ' */, 则会打包为一个模块文件),
// 不指定则单独打包为一个js文件
const Index = () => import("@/view/index");
const My = () => import("@/view/my/index");
const Setting = () =>
  import(/* webpackChunkName: 'Setting ' */ "@/view/setting/index ");
const SettingAbout = () =>
  import(/* webpackChunkName: 'Setting ' */ "@/view/setting/about ");
```

```js
// build/webpack.base.conf.js
// 在 build/webpack.base.conf.js 下的output属性，新增 chunkFilename属性
output: {
 filename: '[name].js',
 //新增chunFilename属性
 chunkFilename: '[name].js'
}
```
